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
