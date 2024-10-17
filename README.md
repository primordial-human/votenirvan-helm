

# Votenirvan Helm Chart

This Helm chart is used to deploy the **Votenirvan** application, which includes a Spring Boot backend and a React frontend, into a Kubernetes cluster. The chart also configures an NGINX Ingress controller to expose the application on `localhost:8080`.

## Prerequisites

Before you begin, ensure you have the following installed:

- [Helm](https://helm.sh/docs/intro/install/) (v3+)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/) (or any Kubernetes cluster)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) (v1.19+)
- NGINX Ingress Controller (if not installed, instructions are below)

## Installation Steps

### 1. Start Minikube

Start your Minikube cluster if it’s not already running: 
Recommended 4GB+ Memory , 2 CPU

```bash
minikube start
```

### 2. (Optional) Install NGINX Ingress Controller

If the NGINX Ingress controller is not already installed in your Minikube cluster, you can install it using Helm:

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx
```

### 3. Deploy Votenirvan Helm Chart

Run the following command to deploy the Votenirvan application using Helm:

```bash
helm install votenirvan ./votenirvan-chart
```

This will install the application with default values.

### 4. Verify the Deployment

Check that the application’s resources (pods, services, etc.) are running successfully:

```bash
kubectl get all
```

### 5. Expose the Application

To access the application, expose the NGINX Ingress controller:

```bash
 kubectl port-forward --namespace ingress-nginx svc/ingress-nginx-controller 8080:80
```

Note the URL provided in the terminal, which will look like:

```
ntroller 8080:80
Forwarding from 127.0.0.1:8080 -> 80
Forwarding from [::1]:8080 -> 80
Handling connection for 8080
```

### 6. Access the Application

Once exposed, open your browser and navigate to:

```
http://localhost:8080
```

The React frontend will load, and any API calls will be routed through the Spring Boot backend via the configured ingress paths.


### 8. Uninstall the Application

To remove the Votenirvan application and clean up resources, run:

```bash
helm uninstall votenirvan
```

---

## Configuration

You can customize the Helm chart by modifying the `values.yaml` file in the chart directory.


## Troubleshooting

- **Ingress Not Accessible:** Ensure that the NGINX Ingress controller is running and properly exposed.
- **Minikube Service Issues:** Verify that the service is correctly mapped to `localhost:8080` and that no other service is using the port.

---


Note : If you not getting OTP's probably  trial account is expired , reach out to me to how to integrate new twilio api keys.
