Kubernetes Deployment (k8s)
===========================

This directory contains the Kubernetes manifests required to orchestrate the Todo application using a microservices architecture.

📂 Structure
------------

-   `backend.yaml`: Defines the Backend Deployment and ClusterIP Service.

-   `frontend.yaml`: Defines the Frontend Deployment and ClusterIP Service.

🚀 Deployment Steps
-------------------

1.  **Navigate to the directory:**

    ```
    cd k8s/

    ```

2.  **Apply the manifests:**

    ```
    kubectl apply -f backend.yaml
    kubectl apply -f frontend.yaml

    ```

3.  **Verify the resources:**

    ```
    kubectl get pods
    kubectl get svc

    ```

🌐 Accessing the Application
----------------------------

Since the services are type `ClusterIP`, you can access them locally using port-forwarding:

-   **Frontend:**

    ```
    kubectl port-forward svc/frontend-service 3000:3000

    ```

    Access at: `http://localhost:3000`

-   **Backend:**

    ```
    kubectl port-forward svc/backend-service 5000:5000

    ```

    Access at: `http://localhost:5000`

🔗 Internal Networking
----------------------

The Frontend is configured to communicate with the Backend using the Kubernetes DNS name: `http://backend-service:5000`.
