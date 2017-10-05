---
title: "Créer une application de conteneur Microsoft Azure Service Fabric sur Linux | Microsoft Docs"
description: "Créez votre première application de conteneur Linux sur Microsoft Azure Service Fabric.  Concevez une image Docker avec votre application, envoyez l’image vers un registre de conteneurs, créez et déployez une application de conteneur Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 8355478cb2fff3a63bc4a9b359ec8e2b132c80f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="a1b3b-104">Créer votre première application de conteneur Service Fabric sur Linux</span><span class="sxs-lookup"><span data-stu-id="a1b3b-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1b3b-105">Windows</span><span class="sxs-lookup"><span data-stu-id="a1b3b-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="a1b3b-106">Linux</span><span class="sxs-lookup"><span data-stu-id="a1b3b-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="a1b3b-107">L’exécution d’une application existante dans un conteneur Linux sur un cluster Service Fabric ne nécessite aucune modification de votre application.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="a1b3b-108">Cet article vous accompagne dans la création d’une image Docker contenant une application web [Flask](http://flask.pocoo.org/) Python et le déploiement dans un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="a1b3b-109">Vous allez également partager votre application en conteneur via [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="a1b3b-110">Cet article suppose une connaissance élémentaire de Docker.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="a1b3b-111">Pour en savoir plus sur Docker, consultez la [présentation de Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1b3b-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a1b3b-112">Prerequisites</span></span>
* <span data-ttu-id="a1b3b-113">Un ordinateur de développement exécutant :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-113">A development computer running:</span></span>
  * <span data-ttu-id="a1b3b-114">[Outils et SDK Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="a1b3b-115">[Docker CE pour Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="a1b3b-116">Interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a1b3b-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="a1b3b-117">Un registre dans Azure Container Registry. [Créez un registre de conteneurs](../container-registry/container-registry-get-started-portal.md) dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-the-docker-container"></a><span data-ttu-id="a1b3b-118">Définir le conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="a1b3b-118">Define the Docker container</span></span>
<span data-ttu-id="a1b3b-119">Créez une image basée sur [l’image Python](https://hub.docker.com/_/python/) située sur Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-119">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="a1b3b-120">Définissez votre conteneur Docker dans un fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="a1b3b-121">Le fichier Dockerfile contient des instructions pour la configuration de l’environnement à l’intérieur de votre conteneur, le chargement de l’application que vous souhaitez exécuter et le mappage des ports.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-121">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="a1b3b-122">Le fichier Dockerfile est l’entrée de la commande `docker build`, qui crée l’image.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-122">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span> 

<span data-ttu-id="a1b3b-123">Créez un répertoire vide et créez le fichier *Dockerfile* (sans extension de fichier).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-123">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="a1b3b-124">Ajoutez ce qui suit au fichier *Dockerfile* et enregistrez vos modifications :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-124">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="a1b3b-125">Pour plus d'informations, consultez les [références Dockerfile](https://docs.docker.com/engine/reference/builder/).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-125">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="a1b3b-126">Créer une application web simple</span><span class="sxs-lookup"><span data-stu-id="a1b3b-126">Create a simple web application</span></span>
<span data-ttu-id="a1b3b-127">Créez une application web Flask écoutant le port 80 qui renvoie « Hello World! ».</span><span class="sxs-lookup"><span data-stu-id="a1b3b-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="a1b3b-128">Dans le même répertoire, créez le fichier *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-128">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="a1b3b-129">Ajoutez ce qui suit et enregistrez vos modifications :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-129">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="a1b3b-130">Créez également le fichier *app.py* et ajoutez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-130">Also create the *app.py* file and add the following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-the-image"></a><span data-ttu-id="a1b3b-131">Créer l’image</span><span class="sxs-lookup"><span data-stu-id="a1b3b-131">Build the image</span></span>
<span data-ttu-id="a1b3b-132">Exécutez la commande `docker build` pour créer l’image qui exécute votre application web.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-132">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="a1b3b-133">Ouvrez une fenêtre PowerShell et accédez à *c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-133">Open a PowerShell window and navigate to *c:\temp\helloworldapp*.</span></span> <span data-ttu-id="a1b3b-134">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-134">Run the following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="a1b3b-135">Cette commande crée la nouvelle image en suivant les instructions de votre fichier Dockerfile, et la nomme (balisage -t) « helloworldapp ».</span><span class="sxs-lookup"><span data-stu-id="a1b3b-135">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="a1b3b-136">La création d’une image extrait l’image de base de Docker Hub et crée une image qui vient s’ajouter à votre application par-dessus l’image de base.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-136">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="a1b3b-137">Une fois la création terminée, exécutez la commande `docker images` pour afficher des informations sur la nouvelle image :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-137">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="a1b3b-138">Exécution locale de l'application</span><span class="sxs-lookup"><span data-stu-id="a1b3b-138">Run the application locally</span></span>
<span data-ttu-id="a1b3b-139">Vérifiez que votre application en conteneur s’exécute en local avant de l’envoyer dans le registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-139">Verify that your containerized application runs locally before pushing it the container registry.</span></span>  

<span data-ttu-id="a1b3b-140">Exécutez l’application, en mappant le port 4000 de votre ordinateur au port 80 exposé du conteneur :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-140">Run the application, mapping your computer's port 4000 to the container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="a1b3b-141">*name* donne un nom au conteneur en cours d’exécution (au lieu d’utiliser l’ID de conteneur).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-141">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="a1b3b-142">Connectez le conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-142">Connect to the running container.</span></span>  <span data-ttu-id="a1b3b-143">Ouvrez un navigateur web qui pointe vers l’adresse IP renvoyée sur le port 4000, par exemple « http://localhost:4000 ».</span><span class="sxs-lookup"><span data-stu-id="a1b3b-143">Open a web browser pointing to the IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="a1b3b-144">Vous devez voir le titre « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="a1b3b-144">You should see the heading "Hello World!"</span></span> <span data-ttu-id="a1b3b-145">s’afficher dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-145">display in the browser.</span></span>

![Hello World!][hello-world]

<span data-ttu-id="a1b3b-147">Pour arrêter votre conteneur, exécutez :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-147">To stop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="a1b3b-148">Supprimez le conteneur de votre ordinateur de développement :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-148">Delete the container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="a1b3b-149">Envoyer l’image dans le registre de conteneurs</span><span class="sxs-lookup"><span data-stu-id="a1b3b-149">Push the image to the container registry</span></span>
<span data-ttu-id="a1b3b-150">Après avoir vérifié que l’application s’exécute dans Docker, envoyez l’image à votre registre dans Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-150">After you verify that the application runs in Docker, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="a1b3b-151">Exécutez `docker login` pour vous connecter à votre Registre de conteneur à l’aide de vos [informations d’identification du Registre](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-151">Run `docker login` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="a1b3b-152">L’exemple suivant transmet l’ID et le mot de passe d’un [principal du service](../active-directory/active-directory-application-objects.md) Azure Active Directory .</span><span class="sxs-lookup"><span data-stu-id="a1b3b-152">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="a1b3b-153">Par exemple, vous pouvez avoir affecté un principal du service à votre Registre pour un scénario d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-153">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>  <span data-ttu-id="a1b3b-154">Ou bien, vous pouvez vous connecter à l’aide de votre nom d’utilisateur de registre et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="a1b3b-155">La commande suivante crée une balise, ou un alias, de l’image, avec un chemin d’accès qualifié complet vers votre registre.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-155">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="a1b3b-156">Cet exemple place l’image dans l’espace de noms `samples` pour éviter un encombrement à la racine du registre.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-156">This example places the image in the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="a1b3b-157">Envoyez l’image vers votre registre de conteneurs :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-157">Push the image to your container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-the-docker-image-with-yeoman"></a><span data-ttu-id="a1b3b-158">Placer l’image Docker dans un package avec Yeoman</span><span class="sxs-lookup"><span data-stu-id="a1b3b-158">Package the Docker image with Yeoman</span></span>
<span data-ttu-id="a1b3b-159">Le Kit de développement logiciel (SDK) Service Fabric pour Linux comprend un générateur [Yeoman](http://yeoman.io/) qui facilite la création de votre application et l’ajout d’une image de conteneur.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-159">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="a1b3b-160">Nous allons utiliser Yeoman pour créer une application avec un seul conteneur Docker appelé *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-160">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="a1b3b-161">Pour créer une application de conteneur Service Fabric, ouvrez une fenêtre de terminal et exécutez `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-161">To create a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="a1b3b-162">Nommez votre application (par exemple, « mycontainer »).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="a1b3b-163">Fournissez l’URL de l’image conteneur dans un registre de conteneurs (par exemple, « »).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-163">Provide the URL for the container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="a1b3b-164">Cette image possède un point d’entrée de charge de travail défini, vous devrez alors spécifier des commandes d’entrée explicitement (les commandes s’exécutent dans le conteneur et garderont le conteneur en exécution après le démarrage).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-164">This image has a workload entry-point defined, so need to explicitly specify input commands (commands run inside the container, which will keep the container running after startup).</span></span> 

<span data-ttu-id="a1b3b-165">Spécifiez un nombre d’instances de « 1 ».</span><span class="sxs-lookup"><span data-stu-id="a1b3b-165">Specify an instance count of "1".</span></span>

![Générateur Yeoman Service Fabric pour les conteneurs][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="a1b3b-167">Configurer l’authentification de référentiel de conteneur et le mappage de port</span><span class="sxs-lookup"><span data-stu-id="a1b3b-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="a1b3b-168">Votre service en conteneur a besoin d’un point de terminaison pour la communication.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="a1b3b-169">Ajoutez maintenant le protocole, le port et le type à un `Endpoint` dans le fichier ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-169">Now add the protocol, port, and type to an `Endpoint` in the ServiceManifest.xml file.</span></span> <span data-ttu-id="a1b3b-170">Dans cet article, le service en conteneur écoute le port 4000 :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-170">For this article, the containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="a1b3b-171">Fournir `UriScheme` enregistre automatiquement le point de terminaison du conteneur avec le service Service Fabric Naming pour la découverte.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-171">Providing the `UriScheme` automatically registers the container endpoint with the Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="a1b3b-172">Un exemple de fichier ServiceManifest.xml complet est fourni à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-172">A full ServiceManifest.xml example file is provided at the end of this article.</span></span> 

<span data-ttu-id="a1b3b-173">Configurez le mappage port/hôte du conteneur en spécifiant une stratégie `PortBinding` dans `ContainerHostPolicies` dans le fichier ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-173">Configure the container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="a1b3b-174">Dans cet article, `ContainerPort` est 80 (le conteneur expose le port 80, tel que spécifié dans le fichier Dockerfile) et `EndpointRef` est « myserviceTypeEndpoint » (le point de terminaison défini dans le manifeste de service).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-174">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (the endpoint defined in the service manifest).</span></span>  <span data-ttu-id="a1b3b-175">Les demandes entrantes pour le service sur le port 4000 sont mappées au port 80 dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-175">Incoming requests to the service on port 4000 are mapped to port 80 on the container.</span></span>  <span data-ttu-id="a1b3b-176">Si votre conteneur doit s’authentifier auprès d’un référentiel privé, ajoutez `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-176">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="a1b3b-177">Pour cet article, ajoutez le nom de compte et le mot de passe du registre de conteneurs myregistry.azurecr.io.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-177">For this article, add the account name and password for the myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-the-service-fabric-application"></a><span data-ttu-id="a1b3b-178">Créer et placer l’application Service Fabric dans un package</span><span class="sxs-lookup"><span data-stu-id="a1b3b-178">Build and package the Service Fabric application</span></span>
<span data-ttu-id="a1b3b-179">Les modèles Yeoman Service Fabric incluent un script de build pour [Gradle](https://gradle.org/), que vous pouvez utiliser pour générer l’application à partir du terminal.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-179">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span></span> <span data-ttu-id="a1b3b-180">Pour générer et placer l’application dans un package, exécutez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-180">To build and package the application, run the following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-the-application"></a><span data-ttu-id="a1b3b-181">Déployer l’application</span><span class="sxs-lookup"><span data-stu-id="a1b3b-181">Deploy the application</span></span>
<span data-ttu-id="a1b3b-182">Une fois que l’application est générée, vous pouvez la déployer vers le cluster local à l’aide de l’interface de ligne de commande Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-182">Once the application is built, you can deploy it to the local cluster using the Service Fabric CLI.</span></span>

<span data-ttu-id="a1b3b-183">Connectez-vous au cluster Service Fabric local.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-183">Connect to the local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="a1b3b-184">Utilisez le script d’installation fourni dans le modèle pour copier le package d’application dans le magasin d’images du cluster, inscrire le type d’application et créer une instance de l’application.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-184">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="a1b3b-185">Ouvrez un navigateur et accédez à Service Fabric Explorer à l’adresse http://localhost:19080/Explorer (remplacez localhost par l’adresse IP privée de la machine virtuelle si vous utilisez Vagrant sur Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-185">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="a1b3b-186">Développez le nœud Applications et notez qu’il existe désormais une entrée pour votre type d’application et une autre pour la première instance de ce type.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-186">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

<span data-ttu-id="a1b3b-187">Connectez le conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-187">Connect to the running container.</span></span>  <span data-ttu-id="a1b3b-188">Ouvrez un navigateur web qui pointe vers l’adresse IP renvoyée sur le port 4000, par exemple « http://localhost:4000 ».</span><span class="sxs-lookup"><span data-stu-id="a1b3b-188">Open a web browser pointing to the IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="a1b3b-189">Vous devez voir le titre « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="a1b3b-189">You should see the heading "Hello World!"</span></span> <span data-ttu-id="a1b3b-190">s’afficher dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-190">display in the browser.</span></span>

![Hello World!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="a1b3b-192">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="a1b3b-192">Clean up</span></span>
<span data-ttu-id="a1b3b-193">Utilisez le script de désinstallation fourni dans le modèle pour supprimer l’instance de l’application du cluster de développement local et annuler l’inscription du type d’application.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-193">Use the uninstall script provided in the template to delete the application instance from the local development cluster and unregister the application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="a1b3b-194">Une fois l’image publiée dans le registre de conteneurs, vous pouvez supprimer l’image locale de votre ordinateur de développement :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-194">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="a1b3b-195">Exemples complets de manifestes d’application et de service Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a1b3b-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="a1b3b-196">Voici les manifestes d’application et de service complets utilisés dans cet article.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-196">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="a1b3b-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="a1b3b-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="a1b3b-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="a1b3b-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion 
       should match the Name and Version attributes of the ServiceManifest element defined in the 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using the 
         ServiceFabric PowerShell module.
         
         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount to 1.  On a multi-node production 
      cluster, set InstanceCount to -1 for the container service to run on every node in 
      the cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="a1b3b-199">Ajout d’autres services à une application existante</span><span class="sxs-lookup"><span data-stu-id="a1b3b-199">Adding more services to an existing application</span></span>

<span data-ttu-id="a1b3b-200">Pour ajouter un autre service de conteneur à une application déjà créée à l’aide de Yeoman, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-200">To add another container service to an application already created using yeoman, perform the following steps:</span></span>

1. <span data-ttu-id="a1b3b-201">Accédez au répertoire à la racine de l’application existante.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-201">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="a1b3b-202">Par exemple, `cd ~/YeomanSamples/MyApplication`, si `MyApplication` est l’application créée par Yeoman.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="a1b3b-203">Exécutez `yo azuresfcontainer:AddService`.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="a1b3b-204">Configurer l’intervalle de temps d’attente avant l’arrêt forcé du conteneur</span><span class="sxs-lookup"><span data-stu-id="a1b3b-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="a1b3b-205">Vous pouvez configurer un intervalle de temps d’attente pour le runtime avant que le conteneur ne soit supprimé après le début de la suppression du service (ou d’un déplacement vers un autre nœud).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-205">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="a1b3b-206">Le fait de configurer l’intervalle de temps envoie la commande `docker stop <time in seconds>` au conteneur.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-206">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="a1b3b-207">Pour plus d’informations, consultez [Arrêt du docker](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="a1b3b-208">L’intervalle de temps d’attente est spécifié dans la section `Hosting`.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-208">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="a1b3b-209">L’extrait de manifeste de cluster suivant montre comment définir l’intervalle d’attente :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-209">The following cluster manifest snippet shows how to set the wait interval:</span></span>

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
<span data-ttu-id="a1b3b-210">L’intervalle de temps par défaut est défini sur 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-210">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="a1b3b-211">Étant donné que cette configuration est dynamique, une mise à niveau uniquement de la configuration sur un cluster met à jour le délai d’expiration.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-211">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="a1b3b-212">Configurer le runtime pour supprimer les images conteneur inutilisées</span><span class="sxs-lookup"><span data-stu-id="a1b3b-212">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="a1b3b-213">Vous pouvez configurer le cluster Service Fabric pour supprimer des images conteneur inutilisées à partir du nœud.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-213">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="a1b3b-214">Cette configuration permet à l’espace disque d’être rétabli si trop d’images conteneur sont présentes sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-214">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="a1b3b-215">Pour activer cette fonctionnalité, mettez à jour la section `Hosting` du manifeste de cluster, comme indiqué dans l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="a1b3b-215">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

<span data-ttu-id="a1b3b-216">Vous pouvez les spécifier les images qui ne doivent pas être supprimées à l’aide du paramètre `ContainerImagesToSkip`.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-216">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="a1b3b-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1b3b-217">Next steps</span></span>
* <span data-ttu-id="a1b3b-218">En savoir plus sur l’exécution des [conteneurs sur Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="a1b3b-219">Consultez le didacticiel [Déployer une application .NET dans un conteneur vers Azure Service Fabric](service-fabric-host-app-in-a-container.md).</span><span class="sxs-lookup"><span data-stu-id="a1b3b-219">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="a1b3b-220">En savoir plus sur le [cycle de vie des applications](service-fabric-application-lifecycle.md) Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-220">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="a1b3b-221">Consulter les [exemples de code de conteneur Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a1b3b-221">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
