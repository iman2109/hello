# hello
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
      nodePort: 30001 
  type: NodePort   


apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: aymanhussain21/eeman:latest
          ports:
            - containerPort: 3000
  


# Use the official Node.js image as a base
FROM node:20


WORKDIR /app

COPY package*.json ./

# Install dependencies
RUN npm install
# If you use yarn:
# RUN yarn install

# Copy the rest of the application code
COPY . .

# Expose the port your app runs on
EXPOSE 3000

# Command to run your app
CMD ["node", "index.js"]
# If using Next.js:
# CMD ["npm", "run", "dev"]
