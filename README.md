# Deployment Mysql to Kubernetes

🚢[Docker Image](https://hub.docker.com/_/mysql)

### Running On Premise 
- Ubuntu 20.04 LTS
- Storage Class Rook Ceph Block

### Specification My Cluster
- Master node vCPU 2 Memory 8Gb
- Worker node1 vCPU 2 Memory 4Gb
- Worker node2 vCPU 2 Memory 4Gb
- Worker node3 vCPU 2 Memory 4Gb

### Installation
1. Clone this project.
    ```sh
    $ git clone https://github.com/skyapps-id/K8s-Mysql-Standalone.git
    ```

2. Create the Secret resource in your Kubernetes cluster by using the kubectl apply command.
    ```sh
    $ cd  K8s-Mysql/
    $ kubectl apply -f configmap-and-secret.yml
    ```
     - NOTE Secrets data are stored as Base64 encoded strings. command : ```$ echo -n 'example' | base64 ``` example mysql password is ``adminpassword``

4. Creating a Presistance Volume Claim resource in your Kubernetes cluster by using the kubectl apply command.
    ```sh
    $ kubectl apply -f persistence-volume-mysql.yaml
    ```

5. Deployment Mysql resource in your Kubernetes cluster by using the kubectl apply command.
    ```sh
    $ kubectl apply -f deployment-mysql.yaml
    ```

6. Creating a Service resource in your Kubernetes cluster by using the kubectl apply command.
    ```sh
    $ kubectl apply -f service-mysql.yaml
    ```

7. Testing Mysql Service.
    ```sh
    $ kubectl get pods
    NAME                     READY   STATUS    RESTARTS   AGE
    mysql-5b5fd56b6d-4kjc5   1/1     Running   0          16m

    $ kubectl exec -it mysql-5b5fd56b6d-4kjc5 -- mysql -p
    DEnter password:
    Welcome to the MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 3
    Server version: 5.6.51 MySQL Community Server (GPL)

    Copyright (c) 2000, 2021, Oracle and/or its affiliates. All rights reserved.

    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

    mysql>
    ```

### Licence

This work is under [MIT](LICENCE) licence.
