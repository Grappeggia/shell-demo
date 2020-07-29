# Creating and Deploying containerized web application

## Introduction

This tutorial shows how to create a containerized web application, test it on a
local Kubernetes cluster for validation and deploy it in a Google Kubernetes
Engine (GKE) cluster. By the end of this tutorial you will understand how to

1.  Create a sample Hello World Kubernetes application
2.  Build/test this application on a local Kubernetes cluster
3.  Edit and debug a Kubernetes application
4.  View and navigate through your app logs
5.  Create a Google Kubernetes Engine Cluster
6.  Deploy application in GKE

## Creating your web application

For this tutorial, we'll be using the
Cloud Shell IDE as our environment for
creating our application, pre-loaded with the tools needed for Cloud
development. To create your application:

*   Launch the
    <walkthrough-editor-spotlight spotlightId="cloud-code-status-bar">Cloud
    code</walkthrough-editor-spotlight> menu from the status bar
*   In the Command Palette, select the
    <walkthrough-editor-spotlight spotlightId="cloud-code-new-app">New
    Application</walkthrough-editor-spotlight> option
*   Select the "Kubernetes application" option
*   On the list of sample Kubernetes applications across multiple languages,
    select the "Go:Hello World" option
*   Next, select a folder for your application location and press "Enter".
*   Once your IDE is finished reloading and your new app is created, you should
    see your it in on your
    <walkthrough-editor-spotlight spotlightId="file-explorer">explorer
    view</walkthrough-editor-spotlight>.

Next, let's build and test this application.

## Testing your application in a local cluster

Now that your app is created, let's run it in a local Kubernetes cluster in
Cloud Shell.

*   Click on the
    <walkthrough-editor-spotlight spotlightId="cloud-code-k8s-icon">Cloud Code -
    Kubernetes</walkthrough-editor-spotlight> icon in the navigation bar
*   You can see the
    <walkthrough-editor-spotlight spotlightId="cloud-code-k8s-explorer">Kubernetes
    Explorer</walkthrough-editor-spotlight> panel, with the clusters available
    for running your app
*   In your
    <walkthrough-spotlight-pointer target="cloudshell" spotlightId="toggle-terminal">terminal</walkthrough-spotlight-pointer>,
    run the command below

    ```bash
    minikube start
    ```

*   Once your local cluster Cloud Shell is set-up, you should see the following
    message

    ```terminal
    Done! kubectl is now configured to use "minikube"
    ```

Now let's build and run this application

*   Click on
    <walkthrough-editor-spotlight spotlightId="cloud-code-status-bar">Cloud
    code</walkthrough-editor-spotlight> in the status bar
*   Select <walkthrough-editor-spotlight spotlightId="cloud-code-run-on-k8s">Run
    on Kubernetes</walkthrough-editor-spotlight>
*   Confirm that you want to use the "minikube" context
*   An
    <walkthrough-editor-spotlight spotlightId="output">Output</walkthrough-editor-spotlight>
    panel should pop-up after a few seconds, displaying the progress as your app
    is built/deployed
*   Once your app is built (should take a few minutes), you can launch it via
    <walkthrough-spotlight-pointer target="cloudshell" spotlightId="devshell-web-preview-button">Web
    Preview</walkthrough-spotlight-pointer> using the port 4503, which will open
    a new tab displaying the "Hello, world!" Message
*   Keep this extra tab open for now, since we'll be soon modifying our
    application

Congratulations! You've just built/run your first application on Kubernetes
using [Cloud Code](https://cloud.google.com/code). Next step, let's modify and
recompile our application.

## Editing and Recompiling your app

Let's start by reviewing the high level application
<walkthrough-editor-open-file filePath="README.md">diagram</walkthrough-editor-open-file>,
where you can see our application is composed of

*   A basic "go-hello-world" web application, implemented by
    <walkthrough-editor-open-file filePath="cmd/hello-world/main.go">main.go</walkthrough-editor-open-file>,
    which returns "Hello, world!" to all received requests
*   A load balancer "go-hello-world-external" service which exposes our app to
    the internet. This is implemented by our
    <walkthrough-editor-open-file filePath="kubernetes-manifests/hello.service.yaml">hello.service.yaml</walkthrough-editor-open-file>,
    which describes a Kubernetes Service resource (details
    [here](https://kubernetes.io/docs/concepts/services-networking/service/))

To modify and recompile our application:

*   Change your
    <walkthrough-editor-select-line filePath="cmd/hello-world/main.go" startLine="29" endLine="30" startCharacterOffset="0" endCharacterOffset="0">main.go</walkthrough-editor-select-line>
    file to print the "Hello, Kubernetes!" message
*   You'll notice in your
    <walkthrough-editor-spotlight spotlightId="output">Output</walkthrough-editor-spotlight>
    that your app automatically starts rebuilding
*   Once you app finishes building and deploying, you can refresh your sample
    application and see the updated text

## View and navigate the logs

To analyze your app while it's running, you can see the logs for your
application using the integrated Log Viewer.

*   Launch the Log Viewer by typing "Cloud Code: View Logs" using the Command
    Palette (accessible with Ctrl/Cmd+Shift+P)
*   This view allows you to filter and navigate the logs for your app. Select
    the
    <walkthrough-editor-spotlight spotlightId="cloud-code-logs-viewer-deployment">Deployment</walkthrough-editor-spotlight>
    or
    <walkthrough-editor-spotlight spotlightId="cloud-code-logs-viewer-pod">Pod</walkthrough-editor-spotlight>
    to see the logs for your application (go-hello-world)
*   Refresh your app in the browser, once you click the
    <walkthrough-editor-spotlight spotlightId="cloud-code-logs-viewer-refresh">Logs
    refresh button</walkthrough-editor-spotlight>, you should see the new logs
    generated

## Creating a Google Kubernetes Engine Cluster

So far, we've been running our app locally. Let's now create a Google Kubernetes
Cluster(GKE) and deploy our application to this new cluster.

This will require that you create/select a project and enable billing for your
resources

<walkthrough-project-setup billing=True></walkthrough-project-setup>

After your project is selected:

*   Click on the
    <walkthrough-editor-spotlight spotlightId="cloud-code-k8s-icon">Cloud Code -
    Kubernetes</walkthrough-editor-spotlight> icon in the navigation bar
*   After hovering the
    <walkthrough-editor-spotlight spotlightId="cloud-code-gke-explorer">GKE
    Explorer</walkthrough-editor-spotlight>, click on the "+" sign to create a
    new GKE cluster
*   In the Create Cluster wizard, select your project, a zone/region where your
    cluster will be physically located (e.g. us-east1-b) and a Cluster Name of
    your choice (e.g. test-gke-cluster)
*   Click on **Create Cluster**
*   The Cluster creation takes a couple of minutes. Once created, your cluster
    will be listed under the
    <walkthrough-editor-spotlight spotlightId="cloud-code-gke-explorer">GKE
    Explorer</walkthrough-editor-spotlight>
*   Right click on your new cluster, then click on "Set as Active Cluster",
    making it the new context for deploying your app

Now let's redeploy the application on the new cluster

*   Launch
    <walkthrough-editor-spotlight spotlightId="cloud-code-status-bar">Cloud
    code</walkthrough-editor-spotlight> from the status bar
*   Select <walkthrough-editor-spotlight spotlightId="cloud-code-run-on-k8s">Run
    on Kubernetes</walkthrough-editor-spotlight>
*   Confirm that you're using your newly created cluster as context for running
    the application
*   Confirm the default option for the image registry(Container Registry details
    [here](https://cloud.google.com/container-registry))
*   Your app should now be built and deployed again
*   Once deployed, you can launch it via
    <walkthrough-spotlight-pointer target="cloudshell" spotlightId="devshell-web-preview-button">Web
    Preview</walkthrough-spotlight-pointer> using the port 4503

## Conclusion

<walkthrough-conclusion-trophy></walkthrough-conclusion-trophy>

Congratulations! You've just created and run your first Kubernetes app on GKE.
Don't forget to delete your cluster on the
    <walkthrough-editor-spotlight spotlightId="cloud-code-gke-explorer">GKE
    Explorer</walkthrough-editor-spotlight>
to avoid any unwanted charges.

<walkthrough-inline-feedback></walkthrough-inline-feedback>

Here are some additional tutorials for using Cloud Code to develop you apps on GCP

<walkthrough-tutorial-card url="https://www.google.com" icon="KUBERNETES_SECTION" label="cloudSql">
**Cloud Code for VSCode** Migrate your application to your local VSCode IDE
</walkthrough-tutorial-card>

<walkthrough-tutorial-card url="https://www.google.com" icon="KUBERNETES_SECTION" label="cloudSql">
**Cloud Code for IntelliJ** Migrate your application to your local IntelliJ IDE
</walkthrough-tutorial-card>

<walkthrough-tutorial-card url="https://www.google.com" icon="SERVERLESS_SECTION" label="cloudSql">
**Cloud Run** Create a serverless app from your browser
</walkthrough-tutorial-card>

<walkthrough-tutorial-card url="https://www.google.com" icon="API_SECTION" label="cloudSql">
**Cloud Code API Explorer** Integrate a the Translate Cloud API to an existing
app </walkthrough-tutorial-card>

<walkthrough-tutorial-card url="https://www.google.com" icon="CLOUD_BUILD_SECTION" label="cloudSql">
**Skaffold** Automate your builds/deployment as you code
</walkthrough-tutorial-card>
