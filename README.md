
*a. Clone the React Application Repository*

bash
git clone https://github.com/MaheshRautrao/React-Todo-list
cd React-Todo-list


*b. Create a Dockerfile*

In the root directory of your project, create a file named Dockerfile with the following content:

Dockerfile
# Use an official Node.js runtime as a parent image
FROM node:18

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install any needed packages specified in package.json
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Build the React application
RUN npm run build

# Set the environment variable for the port
ENV PORT=3000

# Expose the port that the app runs on
EXPOSE 3000

# Define the command to run the app
CMD ["npm", "start"]


*c. Build the Docker Image*

bash
docker build -t react-todo-app .


### 2. Deploy the Docker Image to Kubernetes

*a. Install MicroK8s*

Follow the installation guide from [MicroK8s](https://microk8s.io/) for your OS.

*b. Start MicroK8s*

bash
microk8s start


*c. Create a Kubernetes Deployment Configuration*

Create a file named deployment.yaml with the following content:

yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: react-todo-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: react-todo-app
  template:
    metadata:
      labels:
        app: react-todo-app
    spec:
      containers:
      - name: react-todo-app
        image: react-todo-app
        ports:
        - containerPort: 3000


*d. Create a Kubernetes Service Configuration*

Create a file named service.yaml with the following content:

yaml
apiVersion: v1
kind: Service
metadata:
  name: react-todo-service
spec:
  selector:
    app: react-todo-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
  type: LoadBalancer


*e. Apply the Configurations*

bash
microk8s kubectl apply -f deployment.yaml
microk8s kubectl apply -f service.yaml


*f. Verify Deployment*

To ensure your application is running and accessible, use:

bash
microk8s kubectl get pods
microk8s kubectl get services


Find the external IP of your service and navigate to it in your browser.
