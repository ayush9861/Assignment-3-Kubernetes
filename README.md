# Assignment-3-Kubernetes

## What is Docker?

**Docker** is a platform as a service that use OS-level virtualisation to deliver software called cointainer. The software that host the package is called docker engine.

## What is Kubernetes?

**Kubernetes** automates operational tasks of cointainers management including built-in commands for devloping, deploying and rolling changes to application for scaling and optimizing the application. 

### Versions:

**Docker: 20.10.13**

**Kubernetes: 1.25**

### Plugins Used: 

**Maven**

### Steps to Build Docker Image:

Step1- First of all open your sping boot project and a file name **Dockerfile** and write all your docker configuration data like what version of **openjdk** you are using, your output file name, port you want to expose for the cointainer etc and save it.

Step2- In, this step you will have to clean your project using the **Maven** clean function.

Step3- In, this step you will have to package your project. You can do this by using **Maven** install function.

Step4- If, your packaging is succesfull a new folder will be create named target and inside it you will find your required jar file to build your docker image.

Step5- After, this navigate to your project in file explorer and open command promt or powershell and write the following command:-

```
Docker build -t {your jar finename} .
```
Step6:- If everything goew well your docker image will be created succesfully and you can confirm it by typing this command:-

```
Docker images
```

### Steps to install Kubernates:

Step1- Download and install minikube using this command:-

```
New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force
Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing
```

Step2- After, downloading its time to configure the downloaded binary file ``` PATH ``` of the minikube package. We can do this using the following command:-

```
$oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
if ($oldPath.Split(';') -inotcontains 'C:\minikube'){ `
  [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine) `
}
```
Step3- After, configuring the path its time to test if the program is working file or not. But, vefore teting make sure to start the windows docker server and open the commandpromnt or powershell and type ```minikube start```.

Step4- If, it is succesfull installed it will show you all the commands.


### Installing and Configuring MongoDB

Step1- First, of all start your Windows Docker server and open the power shell or command promnt.

Step2- After, opening you will have to pull the **MongoDB** image from the docke hub. You can do this by using the following commands:-

```
docker pull mongo:latest 
```
Step3- After Pulling the latest image its time deploy it in  **Kubernetes** server.

Step4- To, deploy our mongo server in kubernetes we will have to create some configuration files. The names of the files are:-

- mongo-secret.yml
- mongo-config.yml
- mongo-pv.yml
- mongo-pvc.yml
- mongo-deployment.yml

Step5- After, creating all the files. Its time to exectute the files. We can do it using the **Kubectl** and executing the following command:-

```
kubectl apply -f {file name}.yml
```
### MongoDB Config Files:

These are the files that I have used to configure the mongodb in the Kubernetes cluster.
**mongo-secret.yml**
```
apiVersion: v1
kind: Secret
metadata:
   name: mongo-secret
data:
  username: YWRtaW4=
  password: YWRtaW4=
  ```
**Explination:-** In the above code we have configured and Secret file and given username and password for our mongodb server which is going to run in the kubernetes. Here, you can note the user name is in encrypted format. For the encryption of the username and password we have used base64. 

  **mongo-config.yml**
   ```
   apiVersion: v1
kind: ConfigMap
metadata:
   name: mongo-conf
data:
 host: mongodb-service
 database: admin
 ```
 **Explination:-** In the above code we have configured a ConfigMap File. Basically a Configmap file is a API object which stores the data in key value pair. Pods can take the values from ConfigMap file and utilize them as enviroment variables and configuration files.
 
 **mongo-pv.yml**
 ```
kind: PersistentVolume
apiVersion: v1
metadata:
  name: mongo-pv-volume
  labels:
    type: local
    app: mongo
spec:
  storageClassName: manual
  capacity:
    storage: 250Mi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/mnt/data"
 
    ```
**Explination:-** Configuring Volume is a messy problem for computers and takle this issue Kubernetes use the API PersistentVolume. Using PersistentVolume we can configure how the storgae is provided and how we are going to consume it. In specific PersistentVolume is a storage in the the cluster just like node in cluster resources. PV's have a life cycle independent from the pods.  

**mongo-pvc.yml**
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongo-pv-claim
  labels:
    app: mongo
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 260Mi
      
 ```
 **Explination:-** pvc are similar to pods consumes Node resources and pvc consumes pv resources. pods can request specific leve of resources but claims can request specific size and access mode.
 
**mongo-deployment.yml**

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo
  labels:
    app: mongo
spec:
  selector: 
    matchLabels:
      app: mongo
  replicas: 2
  template:
    metadata:
      labels:
        app: mongo
      name: mongodb-service
    spec:
      containers:
      - image: mongo:latest
        name: mongo
        
        env:
          - name: MONGO_INITDB_ROOT_USERNAME
            valueFrom:
              secretKeyRef:
                name: mongo-secret
                key: username
          - name: MONGO_INITDB_ROOT_PASSWORD
            valueFrom:
              secretKeyRef:
                name: mongo-secret
                key: password
        ports:
        - containerPort: 27017
          name: mongo                
        volumeMounts:
        - name: mongo-persistent-storage
          mountPath: /data/db 
      volumes:
      - name: mongo-persistent-storage
        persistentVolumeClaim:
          claimName: mongo-pv-claim 
 ```
 
**Explination:-** This, is the file which cointains the mian configuration. In this file we are going to give the replicas we want to create, metadata,template details and most importantly image name with version. This is the file in which we are going to compile all other components like mongo-secret, mongo-pv,mongo-pv-claim etc.



### Screenshorts:

### Docker
![](https://i.imgur.com/wg8hLCv.png)
![](https://i.imgur.com/hUQBnc4.png)
![](https://i.imgur.com/BcBE5MS.png)
![](https://i.imgur.com/BpkFilH.png)
![](https://i.imgur.com/EJGuRmP.png)
![](https://i.imgur.com/BpkFilH.png)
![](https://i.imgur.com/1cjlcqw.png)
![](https://i.imgur.com/S8qDLgS.png)

### Kubernetes:

#### Succesful Deploy:
![](https://i.imgur.com/6pUDHVI.png)
#### Show Pods:
![](https://i.imgur.com/ymRsM8Q.png)
#### Spring Logs:
![](https://i.imgur.com/fMELjJR.png)
#### Mongo Logs:
![](https://i.imgur.com/DhKhiZ1.png)
#### Get Data:
![](https://i.imgur.com/BWQOKG9.png)
#### Update Data:
![](https://i.imgur.com/CVhNB3A.png)
