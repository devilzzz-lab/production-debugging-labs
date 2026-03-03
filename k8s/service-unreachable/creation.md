# 🛠 Creating the Broken Scenario

## Step 1: Create Deployment

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
      - name: nginx
        image: nginx

kubectl apply -f deployment.yaml

---

## Step 2: Create Service (With Wrong Selector)

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: wrong-label   # ❌ Wrong label
  ports:
  - port: 80
    targetPort: 80

kubectl apply -f service.yaml

---

## Step 3: Test

kubectl run test --rm -it --image=busybox -- sh

Inside pod:
wget -qO- nginx-service