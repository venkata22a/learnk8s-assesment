# Kubernetes challenge

Deploy this application to [Minikube](https://github.com/kubernetes/minikube) and customise the environment variable to display your name.

```
$ curl $(minikube ip)
Hello edara
```

## Instructions

- Fork this repo
- Build the Docker image
- Write yaml files for a deployment, service, ingress and configmap
- Deploy your application to Minikube
- You should be able to `curl` Minikube's ip and retrieve the string `Hello {yourname}!`
- Commit your files to Github

## Notes

There's no need to push the Docker image to a Docker registry. You should be able to build and use the image from within Minikube.

You can expose Minikube's Docker daemon with:

```shell
eval $(minikube docker-env)
```

```mermaid
sequenceDiagram
    participant U as User/kubectl
    participant A as API Server
    participant E as etcd
    participant S as Scheduler
    participant C as Controllers
    participant K as Kubelet
    participant R as Container Runtime
    
    Note over U,R: Control Plane Operations (1-6)
    U->>+A: 1. Send deployment request
    A->>E: 2. Validate & Store request
    E-->>A: Confirmation
    A->>+S: 3. Schedule pods
    S-->>-A: Node assignment
    A->>+C: 4. Controller processes
    C-->>-A: Deployment config
    A->>E: 5. Update state
    E-->>A: Confirmed
    A->>+K: 6. Create pod instruction
    
    Note over U,R: Data Plane Operations (7-10)
    K->>+R: 7. Create containers
    R-->>-K: Container status
    K->>A: 8. Update pod status
    A->>E: 9. Store new state
    E-->>A: Confirmed
    A-->>-U: 10. Success response```


![image](https://github.com/user-attachments/assets/a938eb4c-43e0-49bb-bf38-b4c8608c6354)

