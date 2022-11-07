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

Step1- Create a file named Docker.

Step2- Clean the meaven using the maven plugin.

Step3- Do a Package build using maven plugin.

Step4- If, build is succesful move to the target folder you will find a jar file that you have given in your docker config.


Now, if the build has succesfully created. Time to run the file to create a Image.


### Steps to Build Docker Image:

Step1- Go to the terminal and type "Docker run {package name}"

Step2- If, run succesful you will see the spring book stating on your terminal.


Finally, you have create the docker image for your spring boot application.

Now, you can check if it is working or not by visiting the localhost url along with the port given in the Docker file.


### Steps to install Kubernates:

Step1-Download and install minikube

Step2-Install Minikube with driver docker setting.

Step3- Using "**kubectl create deployment {yourpackagename --imagename:tag}**"

Step4- Using kubectl **expose deployment {packagename} --type=NodePort --port{yourport}**.

Step5- We, can check if the service is running or not by "**kubectl get service web**" command.

Step6- use "**kubectl get service web --url**" command to open the url in the browser.


### Screenshorts:
![](https://i.imgur.com/wg8hLCv.png)
![](https://i.imgur.com/hUQBnc4.png)
![](https://i.imgur.com/BcBE5MS.png)
![](https://i.imgur.com/BpkFilH.png)
![](https://i.imgur.com/EJGuRmP.png)
![](https://i.imgur.com/BpkFilH.png)
![](https://i.imgur.com/1cjlcqw.png)
![](https://i.imgur.com/S8qDLgS.png)





