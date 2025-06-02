![Screenshot 2025-06-02 102225](https://github.com/user-attachments/assets/530b877f-7b99-4163-8410-ac88df43dc23)
![Screenshot 2025-06-02 110705](https://github.com/user-attachments/assets/f7716af3-f73c-41fb-b25a-eb3067d69d38)
![Screenshot 2025-06-02 112127](https://github.com/user-attachments/assets/9b6939ed-67fd-480a-a738-d655aa02226c)
![Screenshot 2025-06-02 112141](https://github.com/user-attachments/assets/d5547459-3725-4533-90d4-18831074ac21)
![Screenshot 2025-06-02 112151](https://github.com/user-attachments/assets/10a5ddd1-0d9e-4082-8b2d-95692108fdb1)

![Screenshot 2025-06-02 112202](https://github.com/user-attachments/assets/866591d3-4a4a-43bb-83e4-2911335dcc40)
![Screenshot 2025-06-02 112213](https://github.com/user-attachments/assets/55042aeb-117f-4a8f-86e0-02829d5ec171)


PS C:\k8s-demo> kubectl apply -f deployment.yaml
deployment.apps/nginx-deployment unchanged
PS C:\k8s-demo> kubectl apply -f service.yaml
service/nginx-service unchanged
PS C:\k8s-demo> minikube ip
192.168.49.2
PS C:\k8s-demo> kubectl get services
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP        40m
nginx-service   NodePort    10.105.90.187   <none>        80:30007/TCP   8m1s
PS C:\k8s-demo> kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
nginx-deployment-96b9d695-2nxwp   1/1     Running   0          11m
nginx-deployment-96b9d695-9pqxw   1/1     Running   0          11m
PS C:\k8s-demo> kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
nginx-deployment-96b9d695-2nxwp   1/1     Running   0          14m
nginx-deployment-96b9d695-9pqxw   1/1     Running   0          14m
PS C:\k8s-demo> kubectl get service nginx-service
NAME            TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
nginx-service   NodePort   10.105.90.187   <none>        80:30007/TCP   11m
PS C:\k8s-demo> minikube service nginx-service
|-----------|---------------|-------------|---------------------------|
| NAMESPACE |     NAME      | TARGET PORT |            URL            |
|-----------|---------------|-------------|---------------------------|
| default   | nginx-service |          80 | http://192.168.49.2:30007 |
|-----------|---------------|-------------|---------------------------|
🏃  Starting tunnel for service nginx-service.
|-----------|---------------|-------------|------------------------|
| NAMESPACE |     NAME      | TARGET PORT |          URL           |
|-----------|---------------|-------------|------------------------|
| default   | nginx-service |             | http://127.0.0.1:56286 |
|-----------|---------------|-------------|------------------------|
🎉  Opening service default/nginx-service in default browser...
❗  Because you are using a Docker driver on windows, the terminal needs to be open to run it.

PS C:\k8s-demo> kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
nginx-deployment-96b9d695-2nxwp   1/1     Running   0          18m
nginx-deployment-96b9d695-9pqxw   1/1     Running   0          18m
PS C:\k8s-demo> kubectl get services
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP        48m
nginx-service   NodePort    10.105.90.187   <none>        80:30007/TCP   15m
PS C:\k8s-demo> kubectl scale deployment nginx-deployment --replicas=4
deployment.apps/nginx-deployment scaled
PS C:\k8s-demo> kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
nginx-deployment-96b9d695-2nxwp   1/1     Running   0          20m
nginx-deployment-96b9d695-9pqxw   1/1     Running   0          20m
nginx-deployment-96b9d695-nzv7w   1/1     Running   0          18s
nginx-deployment-96b9d695-qrl9q   1/1     Running   0          18s
PS C:\k8s-demo> kubectl get deployment nginx-deployment
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   4/4     4            4           21m
PS C:\k8s-demo> kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
nginx-deployment-96b9d695-2nxwp   1/1     Running   0          24m
nginx-deployment-96b9d695-9pqxw   1/1     Running   0          24m
nginx-deployment-96b9d695-nzv7w   1/1     Running   0          3m48s
nginx-deployment-96b9d695-qrl9q   1/1     Running   0          3m48s
PS C:\k8s-demo> kubectl describe pod nginx-deployment-96b9d695-2nxwp
Name:             nginx-deployment-96b9d695-2nxwp
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Mon, 02 Jun 2025 10:50:17 +0530
Labels:           app=nginx
                  pod-template-hash=96b9d695
Annotations:      <none>
Status:           Running
IP:               10.244.0.3
IPs:
  IP:           10.244.0.3
Controlled By:  ReplicaSet/nginx-deployment-96b9d695
Containers:
  nginx:
    Container ID:   docker://a6b7e514ee280fe0d75e15ce2fcf99b48c49a27b7eaec55b1f619da89d22965d
    Image:          nginx:latest
    Image ID:       docker-pullable://nginx@sha256:fb39280b7b9eba5727c884a3c7810002e69e8f961cc373b89c92f14961d903a0
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Mon, 02 Jun 2025 10:51:45 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-fnr8j (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-fnr8j:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                From               Message
  ----     ------     ----               ----               -------
  Normal   Scheduled  24m                default-scheduler  Successfully assigned default/nginx-deployment-96b9d695-2nxwp to minikube
  Warning  Failed     23m                kubelet            Failed to pull image "nginx:latest": Error response from daemon: Head "https://registry-1.docker.io/v2/library/nginx/manifests/latest": Get "https://auth.docker.io/token?scope=repository%3Alibrary%2Fnginx%3Apull&service=registry.docker.io": net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)
  Warning  Failed     23m                kubelet            Error: ErrImagePull
  Normal   BackOff    23m                kubelet            Back-off pulling image "nginx:latest"
  Warning  Failed     23m                kubelet            Error: ImagePullBackOff
  Normal   Pulling    23m (x2 over 24m)  kubelet            Pulling image "nginx:latest"
  Normal   Pulled     23m                kubelet            Successfully pulled image "nginx:latest" in 6.145s (6.145s including waiting). Image size: 192457322 bytes.
  Normal   Created    23m                kubelet            Created container: nginx
  Normal   Started    23m                kubelet            Started container nginx
PS C:\k8s-demo> kubectl logs nginx-deployment-96b9d695-2nxwp
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2025/06/02 05:21:45 [notice] 1#1: using the "epoll" event method
2025/06/02 05:21:45 [notice] 1#1: nginx/1.27.5
2025/06/02 05:21:45 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2025/06/02 05:21:45 [notice] 1#1: OS: Linux 5.15.167.4-microsoft-standard-WSL2
2025/06/02 05:21:45 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2025/06/02 05:21:45 [notice] 1#1: start worker processes
2025/06/02 05:21:45 [notice] 1#1: start worker process 29
2025/06/02 05:21:45 [notice] 1#1: start worker process 30
2025/06/02 05:21:45 [notice] 1#1: start worker process 31
2025/06/02 05:21:45 [notice] 1#1: start worker process 32
2025/06/02 05:21:45 [notice] 1#1: start worker process 33
2025/06/02 05:21:45 [notice] 1#1: start worker process 34
2025/06/02 05:21:45 [notice] 1#1: start worker process 35
2025/06/02 05:21:45 [notice] 1#1: start worker process 36
2025/06/02 05:21:45 [notice] 1#1: start worker process 37
2025/06/02 05:21:45 [notice] 1#1: start worker process 38
2025/06/02 05:21:45 [notice] 1#1: start worker process 39
2025/06/02 05:21:45 [notice] 1#1: start worker process 40
2025/06/02 05:21:45 [notice] 1#1: start worker process 41
2025/06/02 05:21:45 [notice] 1#1: start worker process 42
2025/06/02 05:21:45 [notice] 1#1: start worker process 43
2025/06/02 05:21:45 [notice] 1#1: start worker process 44
10.244.0.1 - - [02/Jun/2025:05:36:29 +0000] "GET / HTTP/1.1" 200 615 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36 Edg/137.0.0.0" "-"
10.244.0.1 - - [02/Jun/2025:05:36:29 +0000] "GET /favicon.ico HTTP/1.1" 404 555 "http://127.0.0.1:56286/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36 Edg/137.0.0.0" "-"
2025/06/02 05:36:29 [error] 30#30: *1 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 10.244.0.1, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "127.0.0.1:56286", referrer: "http://127.0.0.1:56286/"
PS C:\k8s-demo> kubectl logs nginx-deployment-96b9d695-2nxwp -c nginx
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2025/06/02 05:21:45 [notice] 1#1: using the "epoll" event method
2025/06/02 05:21:45 [notice] 1#1: nginx/1.27.5
2025/06/02 05:21:45 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2025/06/02 05:21:45 [notice] 1#1: OS: Linux 5.15.167.4-microsoft-standard-WSL2
2025/06/02 05:21:45 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2025/06/02 05:21:45 [notice] 1#1: start worker processes
2025/06/02 05:21:45 [notice] 1#1: start worker process 29
2025/06/02 05:21:45 [notice] 1#1: start worker process 30
2025/06/02 05:21:45 [notice] 1#1: start worker process 31
2025/06/02 05:21:45 [notice] 1#1: start worker process 32
2025/06/02 05:21:45 [notice] 1#1: start worker process 33
2025/06/02 05:21:45 [notice] 1#1: start worker process 34
2025/06/02 05:21:45 [notice] 1#1: start worker process 35
2025/06/02 05:21:45 [notice] 1#1: start worker process 36
2025/06/02 05:21:45 [notice] 1#1: start worker process 37
2025/06/02 05:21:45 [notice] 1#1: start worker process 38
2025/06/02 05:21:45 [notice] 1#1: start worker process 39
2025/06/02 05:21:45 [notice] 1#1: start worker process 40
2025/06/02 05:21:45 [notice] 1#1: start worker process 41
2025/06/02 05:21:45 [notice] 1#1: start worker process 42
2025/06/02 05:21:45 [notice] 1#1: start worker process 43
2025/06/02 05:21:45 [notice] 1#1: start worker process 44
10.244.0.1 - - [02/Jun/2025:05:36:29 +0000] "GET / HTTP/1.1" 200 615 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36 Edg/137.0.0.0" "-"
10.244.0.1 - - [02/Jun/2025:05:36:29 +0000] "GET /favicon.ico HTTP/1.1" 404 555 "http://127.0.0.1:56286/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36 Edg/137.0.0.0" "-"
2025/06/02 05:36:29 [error] 30#30: *1 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 10.244.0.1, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "127.0.0.1:56286", referrer: "http://127.0.0.1:56286/"
PS C:\k8s-demo>
