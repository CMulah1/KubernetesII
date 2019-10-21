---
apiVersion: v1
kind: ReplicationController
metadata:
  name: frontend-v4
spec:
  replicas: 2
  selector:
    app: frontend
    version: v4
  template:
    metadata:
      name: frontend-v4
      labels:
        app: frontend
        version: v4
    spec:
      containers:
      - name: frontend
        imagePullPolicy: Always
        image: elseks/els-frontend:v4
        env:
        - name: MONGO_AUTH
          value: "false"
        ports:
        - name: web
          containerPort: 3000

---
apiVersion: v1
kind: Service
metadata:
  name: frontend-v4
spec:
  selector:
    app: frontend
    version: v3
  ports:
    - protocol: TCP
      port: 80
      targetPort: web
  type: LoadBalancer

---
apiVersion: v1
kind: ReplicationController
metadata:
  name: mongodb
spec:
  replicas: 1
  selector:
    app: mongo
    version: v1
  template:
    metadata:
      name: mongo-v1
      labels:
        app: mongo
        version: v1
    spec:
      containers:
      - name: db
        image: elseks/backend
        ports:
        - name: dbport
          containerPort: 27017

---
apiVersion: v1
kind: Service
metadata:
  name: mongo
spec:
  selector:
    app: mongo
    version: v1
  ports:
    - protocol: TCP
      port: 27017
      targetPort: dbport
