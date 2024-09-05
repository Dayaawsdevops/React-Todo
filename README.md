
*a. Clone the React Application Repository*

bash
git clone https://github.com/MaheshRautrao/React-Todo-list
cd React-Todo-list

### STEPS

# Create a Dockerfile*



### 2. Deploy the Docker Image to Kubernetes




*c. Create a Kubernetes Deployment Configuration*



*d. Create a Kubernetes Service Configuration*



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
