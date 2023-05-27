✏️# High-level steps for project implementation✅

✅ Step 1-Server setup and installations

First of all,we would need to setup server for our project.In this,we will create 2 EC2-instances.
    1. Jenkins_Server(t2.medium)
    2. Minikube cluster(t2.medium)



✅ Step 2-Jenkins Runner Configuration

Here,we will add an extension Jenkins Runner in vscode.
Steps:
    -Create .vscode folder in vscode under out project directory
    -Create settings.json file in .vscode folder and add below code
```css
{
    "jenkins-runner.jobs": {
        "Gitops_ArgoCD_CI": {
            "isDefault": true,
            "runWith": "jenkins-master",
            "name": "Gitops_ArgoCD_CI",
        }
    },

    "jenkins-runner.hostConfigs": {
        "jenkins-master": {
            "url": "http://13.232.122.175:8080/",
            "user": "admin",
            "password": "admin",
            "useCrumbIssuer": true,
        },
      
    }
}
```

✅Step 3-Advance Declarative Jenkinsfile creation(Groovy scripting)


✅Trigger Jenkins job using VScode itself(It will trigger the jenkns job automatically with the help of Jenkins Runner plugin in vscode)

✅Webhook configurations

✅Python Application overview

✅Dockerizing python application

✅Kubernetes manifest file creation

✅Connect kubernetes node to ArgoCD

✅Connect private GitHub repo to ArgoCD for CD part

✅Trigger CD Jenkins job using Curl command and Pass variables from CI pipelines.
