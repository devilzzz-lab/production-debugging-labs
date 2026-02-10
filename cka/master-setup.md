Part 1: Kubernetes Fundamentals and Lab Setup
Section 1.3: Setting Up Your CKA Practice Environment
This section sets up a single-node Kubernetes cluster using kubeadm, closely mirroring the CKA exam environment.


Part 2: Bootstrapping a Multi-Node Cluster with kubeadm
🧱 Target Architecture

k8s-master   (Control Plane)
k8s-worker   (Worker Node)
🖥️ Step 0: Create a New VM (Worker)
Create 1 new VM with:
OS: Ubuntu 22.04
RAM: 2 GB minimum (4 GB better)
CPU: 2 vCPU
Network: Same network as master (very important)
After login, set hostname:
sudo hostnamectl set-hostname k8s-worker
exec bash
Update /etc/hosts on worker:
sudo nano /etc/hosts
Add:
127.0.1.1   k8s-worker
<MASTER_PRIVATE_IP> k8s-master

master_priate_ip = ip a 

🧠 Step 1: Run COMMON setup on Worker
👉 Run EXACT same steps as Section 1 – Step 1 & Step 2
✔ On k8s-worker run:
# Kernel modules
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter
# Sysctl
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward               = 1
EOF

sudo sysctl --system
# Install containerd
sudo apt-get update
sudo apt-get install -y containerd

sudo mkdir -p /etc/containerd
sudo containerd config default | sudo tee /etc/containerd/config.toml
sudo sed -i 's/SystemdCgroup = false/SystemdCgroup = true/' /etc/containerd/config.toml

sudo systemctl restart containerd
sudo systemctl enable containerd
# Disable swap
sudo swapoff -a
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
# Install kubeadm tools
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gpg

sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | \
sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] \
https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /" | \
sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

Step 3: Configure a Single-Node Cluster (Control Plane)
1. Initialize the control-plane node
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
⚠️ Save the kubeadm join command if shown.
2. Configure kubectl for the admin user
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
3. Remove control-plane taint (single-node cluster)
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
4. Install Flannel CNI plugin
kubectl apply -f \
https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
5. Verify the cluster
kubectl get nodes
kubectl get pods -n kube-system
Expected:
Node status: Ready
All kube-system pods: Running
✅ CKA Notes
containerd + systemd cgroup = exam-safe
kubeadm init + Flannel = classic CKA lab setup
Single-node cluster is allowed for practice
Always disable swap (CKA strict rule)



Part 2: Bootstrapping a Multi-Node Cluster with kubeadm
🧱 Target Architecture
🚫 DO NOT run kubeadm init on worker
🧩 Step 2: Prepare Control Plane (Master)
On k8s-master, get join command:
sudo kubeadm token create --print-join-command
Example output:
kubeadm join 192.168.1.10:6443 \
--token abcdef.0123456789abcdef \
--discovery-token-ca-cert-hash sha256:xxxx
🔗 Step 3: Join Worker to Cluster
👉 Run on k8s-worker
sudo kubeadm join <MASTER_IP>:6443 \
--token <token> \
--discovery-token-ca-cert-hash sha256:<hash>
Wait for:
This node has joined the cluster
✅ Step 4: Verify Cluster (Master)
kubectl get nodes -o wide
Expected:
k8s-master   Ready
k8s-worker   Ready
🔥 Common Errors & Fixes (Exam Gold)
Issue	Fix
Worker NotReady	CNI not ready yet
join fails	Check firewall / IP
kubelet crash	containerd cgroup
hostname mismatch	reset + rejoin
Reset worker if needed:
sudo kubeadm reset -f
🧠 CKA Notes (IMPORTANT)
Workers do NOT need kubectl
CNI runs only once from master
Pod CIDR must match CNI:
Calico → 192.168.0.0/16
Flannel → 10.244.0.0/16
🚀 You’re now here
✔ Single-node cluster ✅
✔ Multi-node cluster ✅
✔ kubeadm mastery 🔥