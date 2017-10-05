---
title: "Créer une application de conteneur Microsoft Azure Service Fabric | Microsoft Docs"
description: "Créez votre première application de conteneur Windows sur Microsoft Azure Service Fabric.  Concevez une image Docker avec une application Python, envoyez l’image vers un registre de conteneurs, créez et déployez une application de conteneur Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: 025bde02b3f342ec3399d51819d1fa8a91f11374
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="f1839-104">Créer votre première application de conteneur Service Fabric sur Windows</span><span class="sxs-lookup"><span data-stu-id="f1839-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1839-105">Windows</span><span class="sxs-lookup"><span data-stu-id="f1839-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="f1839-106">Linux</span><span class="sxs-lookup"><span data-stu-id="f1839-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="f1839-107">L’exécution d’une application existante dans un conteneur Windows sur un cluster Service Fabric ne nécessite aucune modification de votre application.</span><span class="sxs-lookup"><span data-stu-id="f1839-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="f1839-108">Cet article vous accompagne dans la création d’une image Docker contenant une application web [Flask](http://flask.pocoo.org/) Python et le déploiement dans un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f1839-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="f1839-109">Vous allez également partager votre application en conteneur via [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="f1839-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="f1839-110">Cet article suppose une connaissance élémentaire de Docker.</span><span class="sxs-lookup"><span data-stu-id="f1839-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="f1839-111">Pour en savoir plus sur Docker, consultez la [présentation de Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="f1839-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1839-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f1839-112">Prerequisites</span></span>
<span data-ttu-id="f1839-113">Un ordinateur de développement exécutant :</span><span class="sxs-lookup"><span data-stu-id="f1839-113">A development computer running:</span></span>
* <span data-ttu-id="f1839-114">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f1839-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="f1839-115">[Outils et SDK Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f1839-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="f1839-116">Docker pour Windows.</span><span class="sxs-lookup"><span data-stu-id="f1839-116">Docker for Windows.</span></span>  <span data-ttu-id="f1839-117">[Obtenez Docker CE pour Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="f1839-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="f1839-118">Après l’installation et le démarrage de Docker, cliquez avec le bouton droit de la souris sur l’icône de la barre d’état, puis sélectionnez **Switch to Windows containers** (Basculer vers les conteneurs Windows).</span><span class="sxs-lookup"><span data-stu-id="f1839-118">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="f1839-119">Cette action est nécessaire pour exécuter des images Docker basées sur Windows.</span><span class="sxs-lookup"><span data-stu-id="f1839-119">This is required to run Docker images based on Windows.</span></span>

<span data-ttu-id="f1839-120">Un cluster Windows avec au moins trois nœuds s’exécutant sur Windows Server 2016 avec conteneurs. [Créez un cluster](service-fabric-cluster-creation-via-portal.md) ou [essayez gratuitement Service Fabric](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="f1839-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="f1839-121">Un registre dans Azure Container Registry. [Créez un registre de conteneurs](../container-registry/container-registry-get-started-portal.md) dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f1839-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-the-docker-container"></a><span data-ttu-id="f1839-122">Définir le conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="f1839-122">Define the Docker container</span></span>
<span data-ttu-id="f1839-123">Créez une image basée sur [l’image Python](https://hub.docker.com/_/python/) située sur Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="f1839-123">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="f1839-124">Définissez votre conteneur Docker dans un fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="f1839-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="f1839-125">Le fichier Dockerfile contient des instructions pour la configuration de l’environnement à l’intérieur de votre conteneur, le chargement de l’application que vous souhaitez exécuter et le mappage des ports.</span><span class="sxs-lookup"><span data-stu-id="f1839-125">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="f1839-126">Le fichier Dockerfile est l’entrée de la commande `docker build`, qui crée l’image.</span><span class="sxs-lookup"><span data-stu-id="f1839-126">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span>

<span data-ttu-id="f1839-127">Créez un répertoire vide et créez le fichier *Dockerfile* (sans extension de fichier).</span><span class="sxs-lookup"><span data-stu-id="f1839-127">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="f1839-128">Ajoutez ce qui suit au fichier *Dockerfile* et enregistrez vos modifications :</span><span class="sxs-lookup"><span data-stu-id="f1839-128">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="f1839-129">Pour plus d'informations, consultez les [références Dockerfile](https://docs.docker.com/engine/reference/builder/).</span><span class="sxs-lookup"><span data-stu-id="f1839-129">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="f1839-130">Créer une application web simple</span><span class="sxs-lookup"><span data-stu-id="f1839-130">Create a simple web application</span></span>
<span data-ttu-id="f1839-131">Créez une application web Flask écoutant le port 80 qui renvoie « Hello World! ».</span><span class="sxs-lookup"><span data-stu-id="f1839-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="f1839-132">Dans le même répertoire, créez le fichier *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="f1839-132">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="f1839-133">Ajoutez ce qui suit et enregistrez vos modifications :</span><span class="sxs-lookup"><span data-stu-id="f1839-133">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="f1839-134">Créez également le fichier *app.py* et ajoutez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="f1839-134">Also create the *app.py* file and add the following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-the-image"></a><span data-ttu-id="f1839-135">Créer l’image</span><span class="sxs-lookup"><span data-stu-id="f1839-135">Build the image</span></span>
<span data-ttu-id="f1839-136">Exécutez la commande `docker build` pour créer l’image qui exécute votre application web.</span><span class="sxs-lookup"><span data-stu-id="f1839-136">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="f1839-137">Ouvrez une fenêtre PowerShell et accédez au répertoire contenant le fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="f1839-137">Open a PowerShell window and navigate to the directory containing the Dockerfile.</span></span> <span data-ttu-id="f1839-138">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f1839-138">Run the following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="f1839-139">Cette commande crée la nouvelle image en suivant les instructions de votre fichier Dockerfile, et la nomme (balisage -t) « helloworldapp ».</span><span class="sxs-lookup"><span data-stu-id="f1839-139">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="f1839-140">La création d’une image extrait l’image de base de Docker Hub et crée une image qui vient s’ajouter à votre application par-dessus l’image de base.</span><span class="sxs-lookup"><span data-stu-id="f1839-140">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="f1839-141">Une fois la création terminée, exécutez la commande `docker images` pour afficher des informations sur la nouvelle image :</span><span class="sxs-lookup"><span data-stu-id="f1839-141">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="f1839-142">Exécution locale de l'application</span><span class="sxs-lookup"><span data-stu-id="f1839-142">Run the application locally</span></span>
<span data-ttu-id="f1839-143">Vérifiez votre image en local avant de l’envoyer dans le registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="f1839-143">Verify your image locally before pushing it the container registry.</span></span>  

<span data-ttu-id="f1839-144">Exécutez l'application :</span><span class="sxs-lookup"><span data-stu-id="f1839-144">Run the application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="f1839-145">*name* donne un nom au conteneur en cours d’exécution (au lieu d’utiliser l’ID de conteneur).</span><span class="sxs-lookup"><span data-stu-id="f1839-145">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="f1839-146">Une fois le conteneur démarré, recherchez son adresse IP pour vous connecter à votre conteneur en cours d’exécution à partir d’un navigateur :</span><span class="sxs-lookup"><span data-stu-id="f1839-146">Once the container starts, find its IP address so that you can connect to your running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="f1839-147">Connectez le conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f1839-147">Connect to the running container.</span></span>  <span data-ttu-id="f1839-148">Ouvrez un navigateur web qui pointe vers l’adresse IP renvoyée, par exemple « http://172.31.194.61 ».</span><span class="sxs-lookup"><span data-stu-id="f1839-148">Open a web browser pointing to the IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="f1839-149">Vous devez voir le titre « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="f1839-149">You should see the heading "Hello World!"</span></span> <span data-ttu-id="f1839-150">s’afficher dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="f1839-150">display in the browser.</span></span>

<span data-ttu-id="f1839-151">Pour arrêter votre conteneur, exécutez :</span><span class="sxs-lookup"><span data-stu-id="f1839-151">To stop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="f1839-152">Supprimez le conteneur de votre ordinateur de développement :</span><span class="sxs-lookup"><span data-stu-id="f1839-152">Delete the container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="f1839-153">Envoyer l’image dans le registre de conteneurs</span><span class="sxs-lookup"><span data-stu-id="f1839-153">Push the image to the container registry</span></span>
<span data-ttu-id="f1839-154">Après avoir vérifié que le conteneur s’exécute sur votre ordinateur de développement, envoyez l’image à votre registre dans Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="f1839-154">After you verify that the container runs on your development machine, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="f1839-155">Exécutez ``docker login`` pour vous connecter à votre Registre de conteneur à l’aide de vos [informations d’identification du Registre](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f1839-155">Run ``docker login`` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="f1839-156">L’exemple suivant transmet l’ID et le mot de passe d’un [principal du service](../active-directory/active-directory-application-objects.md) Azure Active Directory .</span><span class="sxs-lookup"><span data-stu-id="f1839-156">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="f1839-157">Par exemple, vous pouvez avoir affecté un principal du service à votre Registre pour un scénario d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="f1839-157">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span> <span data-ttu-id="f1839-158">Ou bien, vous pouvez vous connecter à l’aide de votre nom d’utilisateur de registre et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f1839-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="f1839-159">La commande suivante crée une balise, ou un alias, de l’image, avec un chemin d’accès qualifié complet vers votre registre.</span><span class="sxs-lookup"><span data-stu-id="f1839-159">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="f1839-160">Cet exemple place l’image dans l’espace de noms ```samples``` pour éviter un encombrement à la racine du registre.</span><span class="sxs-lookup"><span data-stu-id="f1839-160">This example places the image in the ```samples``` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="f1839-161">Envoyez l’image vers votre registre de conteneurs :</span><span class="sxs-lookup"><span data-stu-id="f1839-161">Push the image to your container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-the-containerized-service-in-visual-studio"></a><span data-ttu-id="f1839-162">Créer le service en conteneur dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f1839-162">Create the containerized service in Visual Studio</span></span>
<span data-ttu-id="f1839-163">Le kit de développement logiciel Service Fabric fournit un modèle de service pour vous aider à créer une application en conteneur.</span><span class="sxs-lookup"><span data-stu-id="f1839-163">The Service Fabric SDK and tools provide a service template to help you create a containerized application.</span></span>

1. <span data-ttu-id="f1839-164">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1839-164">Start Visual Studio.</span></span>  <span data-ttu-id="f1839-165">Sélectionnez **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="f1839-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="f1839-166">Sélectionnez **Service Fabric application** (Application Service Fabric), nommez-la « MyFirstContainer », puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1839-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="f1839-167">Sélectionnez **Guest Container** (Conteneur invité) dans la liste des **modèles de service**.</span><span class="sxs-lookup"><span data-stu-id="f1839-167">Select **Guest Container** from the list of **service templates**.</span></span>
4. <span data-ttu-id="f1839-168">Sous **Nom de l’image**, entrez « myregistry.azurecr.io/samples/helloworldapp », c’est-à-dire l’image que vous avez envoyée à votre référentiel de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="f1839-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", the image you pushed to your container repository.</span></span>
5. <span data-ttu-id="f1839-169">Donnez un nom à votre service et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1839-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="f1839-170">Configurer la communication</span><span class="sxs-lookup"><span data-stu-id="f1839-170">Configure communication</span></span>
<span data-ttu-id="f1839-171">Le service en conteneur a besoin d’un point de terminaison pour la communication.</span><span class="sxs-lookup"><span data-stu-id="f1839-171">The containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="f1839-172">Ajoutez un élément `Endpoint` ainsi que le protocole, le port et le type au fichier ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="f1839-172">Add an `Endpoint` element with the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="f1839-173">Dans cet article, le service en conteneur écoute le port 8081 :</span><span class="sxs-lookup"><span data-stu-id="f1839-173">For this article, the containerized service listens on port 8081.</span></span>  <span data-ttu-id="f1839-174">Dans cet exemple, un port fixe 8081 est utilisé.</span><span class="sxs-lookup"><span data-stu-id="f1839-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="f1839-175">Si aucun port n’est spécifié, un port aléatoire de la plage de ports de l’application est choisi.</span><span class="sxs-lookup"><span data-stu-id="f1839-175">If no port is specified, a random port from the application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="f1839-176">En définissant un point de terminaison, Service Fabric publie le point de terminaison sur le service d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="f1839-176">By defining an endpoint, Service Fabric publishes the endpoint to the Naming service.</span></span>  <span data-ttu-id="f1839-177">D’autres services qui s’exécutent dans le cluster peuvent résoudre ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="f1839-177">Other services running in the cluster can resolve this container.</span></span>  <span data-ttu-id="f1839-178">Vous pouvez également effectuer la communication de conteneur à conteneur à l’aide du [proxy inversé](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="f1839-178">You can also perform container-to-container communication using the [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="f1839-179">Pour établir la communication, vous devez fournir le port d’écoute HTTP associé au proxy inversé et le nom des services avec lesquels vous souhaitez communiquer en tant que variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="f1839-179">Communication is performed by providing the reverse proxy HTTP listening port and the name of the services that you want to communicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="f1839-180">Configurer et définir des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="f1839-180">Configure and set environment variables</span></span>
<span data-ttu-id="f1839-181">Il est possible de spécifier des variables d’environnement pour chaque package de code dans le manifeste de service.</span><span class="sxs-lookup"><span data-stu-id="f1839-181">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="f1839-182">Cette fonctionnalité est disponible pour tous les services, qu’ils soient déployés sous forme de conteneurs, de processus ou d’exécutables invités.</span><span class="sxs-lookup"><span data-stu-id="f1839-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="f1839-183">Vous pouvez remplacer les valeurs de variable d’environnement dans le manifeste de l’application, ou les spécifier lors du déploiement, en tant que paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="f1839-183">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="f1839-184">L’extrait de code XML du manifeste de service suivant illustre la méthode à suivre pour spécifier des variables d’environnement pour un package de code :</span><span class="sxs-lookup"><span data-stu-id="f1839-184">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="f1839-185">Ces variables d’environnement peuvent être remplacées dans le manifeste de l’application :</span><span class="sxs-lookup"><span data-stu-id="f1839-185">These environment variables can be overridden in the application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="f1839-186">Configuration du mappage des ports de conteneur aux ports hôtes et de la détection de conteneur à conteneur</span><span class="sxs-lookup"><span data-stu-id="f1839-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="f1839-187">Configurez un port de l’hôte utilisé pour communiquer avec le conteneur.</span><span class="sxs-lookup"><span data-stu-id="f1839-187">Configure a host port used to communicate  with the container.</span></span> <span data-ttu-id="f1839-188">La liaison de port mappe le port sur lequel le service écoute, à l’intérieur du conteneur, à un port sur l’hôte.</span><span class="sxs-lookup"><span data-stu-id="f1839-188">The port binding maps the port on which the service is listening inside the container to a port on the host.</span></span> <span data-ttu-id="f1839-189">Ajoutez un élément `PortBinding` dans l’élément `ContainerHostPolicies` du fichier ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="f1839-189">Add a `PortBinding` element in `ContainerHostPolicies` element of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="f1839-190">Dans cet article, `ContainerPort` est 80 (le conteneur expose le port 80, tel que spécifié dans le fichier Dockerfile) et `EndpointRef` est « Guest1TypeEndpoint » (le point de terminaison défini précédemment dans le manifeste de service).</span><span class="sxs-lookup"><span data-stu-id="f1839-190">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (the endpoint previously defined in the service manifest).</span></span>  <span data-ttu-id="f1839-191">Les demandes entrantes pour le service sur le port 8081 sont mappées au port 80 dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="f1839-191">Incoming requests to the service on port 8081 are mapped to port 80 on the container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="f1839-192">Configurer l’authentification au registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="f1839-192">Configure container registry authentication</span></span>
<span data-ttu-id="f1839-193">Configurez l’authentification au registre de conteneurs en ajoutant l’élément `RepositoryCredentials` à l’élément `ContainerHostPolicies` du fichier ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="f1839-193">Configure container registry authentication by adding `RepositoryCredentials` to `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span> <span data-ttu-id="f1839-194">Ajoutez le compte et le mot de passe pour le registre de conteneurs myregistry.azurecr.io. Cela permet au service de télécharger l’image de conteneur à partir du référentiel.</span><span class="sxs-lookup"><span data-stu-id="f1839-194">Add the account and password for the myregistry.azurecr.io container registry, which allows the service to download the container image from the repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="f1839-195">Nous vous recommandons de chiffrer le mot de passe du référentiel à l’aide d’un certificat de chiffrement qui est déployé sur tous les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="f1839-195">We recommend that you encrypt the repository password by using an encipherment certificate that's deployed to all nodes of the cluster.</span></span> <span data-ttu-id="f1839-196">Lorsque Service Fabric déploie le package de service sur le cluster, le certificat de chiffrement est utilisé pour déchiffrer le texte chiffré.</span><span class="sxs-lookup"><span data-stu-id="f1839-196">When Service Fabric deploys the service package to the cluster, the encipherment certificate is used to decrypt the cipher text.</span></span>  <span data-ttu-id="f1839-197">Le cmdlet Invoke-ServiceFabricEncryptText est utilisé pour créer le texte chiffré du mot de passe, qui est ensuite ajouté au fichier ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="f1839-197">The Invoke-ServiceFabricEncryptText cmdlet is used to create the cipher text for the password, which is added to the ApplicationManifest.xml file.</span></span>

<span data-ttu-id="f1839-198">Le script suivant crée un nouveau certificat auto-signé et l’exporte vers un fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="f1839-198">The following script creates a new self-signed certificate and exports it to a PFX file.</span></span>  <span data-ttu-id="f1839-199">Le certificat est importé dans un coffre de clés existant, puis est déployé sur le cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f1839-199">The certificate is imported into an existing key vault and then deployed to the Service Fabric cluster.</span></span>

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export to PFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import the certificate to an existing key vault.  The key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add the certificate to all the VMs in the cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="f1839-200">Chiffrez le mot de passe à l’aide du cmdlet [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f1839-200">Encrypt the password using the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="f1839-201">Remplacez le mot de passe avec le texte chiffré renvoyé par le cmdlet [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) et définissez `PasswordEncrypted` sur « true ».</span><span class="sxs-lookup"><span data-stu-id="f1839-201">Replace the password with the cipher text returned by the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` to "true".</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a><span data-ttu-id="f1839-202">Configurer le mode d’isolation</span><span class="sxs-lookup"><span data-stu-id="f1839-202">Configure isolation mode</span></span>
<span data-ttu-id="f1839-203">Windows prend en charge deux modes d’isolation pour les conteneurs : Processus et Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f1839-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="f1839-204">Avec le mode d’isolation Processus, tous les conteneurs s’exécutant sur le même hôte partagent le noyau avec l’hôte.</span><span class="sxs-lookup"><span data-stu-id="f1839-204">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="f1839-205">Avec le mode d’isolation Hyper-V, les noyaux sont isolés entre chaque conteneur Hyper-V et l’hôte du conteneur.</span><span class="sxs-lookup"><span data-stu-id="f1839-205">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="f1839-206">Le mode d’isolation est défini dans l’élément `ContainerHostPolicies` dans le fichier manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="f1839-206">The isolation mode is specified in the `ContainerHostPolicies` element in the application manifest file.</span></span> <span data-ttu-id="f1839-207">Les modes d’isolation qui peuvent être définis sont `process`, `hyperv` et `default`.</span><span class="sxs-lookup"><span data-stu-id="f1839-207">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="f1839-208">Par défaut, le mode d’isolation est défini sur `process` sur les hôtes Windows Server, et sur `hyperv` sur les hôtes Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f1839-208">The default isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="f1839-209">L’extrait de code suivant montre comment le mode d’isolation est spécifié dans le fichier manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="f1839-209">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="f1839-210">Configurer la gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="f1839-210">Configure resource governance</span></span>
<span data-ttu-id="f1839-211">La [gouvernance des ressources](service-fabric-resource-governance.md) limite les ressources que le conteneur peut utiliser sur l’hôte.</span><span class="sxs-lookup"><span data-stu-id="f1839-211">[Resource governance](service-fabric-resource-governance.md) restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="f1839-212">L’élément `ResourceGovernancePolicy`, spécifié dans le manifeste de l’application, est utilisé pour déclarer des limites relatives aux ressources pour un package de code de service.</span><span class="sxs-lookup"><span data-stu-id="f1839-212">The `ResourceGovernancePolicy` element, which is specified in the application manifest, is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="f1839-213">Des limites de ressources peuvent être définies pour les ressources suivantes : mémoire, MemorySwap, CpuShares (poids relatif du processeur), MemoryReservationInMB, BlkioWeight (poids relatif de l’élément BlockIO).</span><span class="sxs-lookup"><span data-stu-id="f1839-213">Resource limits can be set for the following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="f1839-214">Dans cet exemple, le package de service Guest1Pkg obtient un cœur sur les nœuds de cluster où il est placé.</span><span class="sxs-lookup"><span data-stu-id="f1839-214">In this example, service package Guest1Pkg gets one core on the cluster nodes where it is placed.</span></span>  <span data-ttu-id="f1839-215">Les limites de mémoire sont absolues, ce qui signifie que le package de code est limité à 1024 Mo de mémoire (avec une garantie de réservation identique).</span><span class="sxs-lookup"><span data-stu-id="f1839-215">Memory limits are absolute, so the code package is limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="f1839-216">Les packages de code (conteneurs ou processus) ne sont pas en mesure d’allouer plus de mémoire que cette limite. Toute tentative en ce sens conduit à une exception de mémoire insuffisante.</span><span class="sxs-lookup"><span data-stu-id="f1839-216">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="f1839-217">Pour pouvoir appliquer la limite de ressources, des limites de mémoire doivent être spécifiées pour tous les packages de code au sein d’un package de service.</span><span class="sxs-lookup"><span data-stu-id="f1839-217">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-the-container-application"></a><span data-ttu-id="f1839-218">Déployer l’application de conteneur</span><span class="sxs-lookup"><span data-stu-id="f1839-218">Deploy the container application</span></span>
<span data-ttu-id="f1839-219">Enregistrez toutes les modifications et générez l’application.</span><span class="sxs-lookup"><span data-stu-id="f1839-219">Save all your changes and build the application.</span></span> <span data-ttu-id="f1839-220">Pour publier votre application, cliquez avec le bouton droit de la souris sur **MyFirstContainer** dans l’Explorateur de solutions, puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="f1839-220">To publish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="f1839-221">Dans **Point de terminaison de connexion**, entrez le point de terminaison de gestion pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="f1839-221">In **Connection Endpoint**, enter the management endpoint for the cluster.</span></span>  <span data-ttu-id="f1839-222">Par exemple : « containercluster.westus2.cloudapp.azure.com:19000 ».</span><span class="sxs-lookup"><span data-stu-id="f1839-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="f1839-223">Vous trouverez le point de terminaison de connexion client dans le panneau d’aperçu de votre cluster dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1839-223">You can find the client connection endpoint in the Overview blade for your cluster in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="f1839-224">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="f1839-224">Click **Publish**.</span></span>

<span data-ttu-id="f1839-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) est un outil web dédié à l’inspection et à la gestion d’applications et de nœuds dans un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f1839-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="f1839-226">Ouvrez un navigateur et accédez à http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/, puis suivez le déploiement de l’application.</span><span class="sxs-lookup"><span data-stu-id="f1839-226">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow the application deployment.</span></span>  <span data-ttu-id="f1839-227">L’application se déploie mais se trouve dans un état d’erreur jusqu’à ce que l’image soit téléchargée sur les nœuds du cluster (ce qui peut prendre du temps, selon la taille de l’image) : ![Erreur][1]</span><span class="sxs-lookup"><span data-stu-id="f1839-227">The application deploys but is in an error state until the image is downloaded on the cluster nodes (which can take some time, depending on the image size): ![Error][1]</span></span>

<span data-ttu-id="f1839-228">L’application est prête lorsqu’elle est à l’état ```Ready``` : ![Prête][2]</span><span class="sxs-lookup"><span data-stu-id="f1839-228">The application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="f1839-229">Ouvrez un navigateur et accédez à http://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="f1839-229">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="f1839-230">Vous devez voir le titre « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="f1839-230">You should see the heading "Hello World!"</span></span> <span data-ttu-id="f1839-231">s’afficher dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="f1839-231">display in the browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="f1839-232">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="f1839-232">Clean up</span></span>
<span data-ttu-id="f1839-233">Vous continuez à être facturé tant que le cluster est en cours d’exécution. Pensez à [supprimer votre cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="f1839-233">You continue to incur charges while the cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="f1839-234">Les [clusters d’essai](http://tryazureservicefabric.westus.cloudapp.azure.com/) sont automatiquement supprimés après quelques heures.</span><span class="sxs-lookup"><span data-stu-id="f1839-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="f1839-235">Une fois l’image publiée dans le registre de conteneurs, vous pouvez supprimer l’image locale de votre ordinateur de développement :</span><span class="sxs-lookup"><span data-stu-id="f1839-235">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="f1839-236">Exemples complets de manifestes d’application et de service Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f1839-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="f1839-237">Voici les manifestes d’application et de service complets utilisés dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f1839-237">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="f1839-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f1839-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="f1839-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f1839-239">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="f1839-240">Configurer l’intervalle de temps d’attente avant l’arrêt forcé du conteneur</span><span class="sxs-lookup"><span data-stu-id="f1839-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="f1839-241">Vous pouvez configurer un intervalle de temps d’attente pour le runtime avant que le conteneur ne soit supprimé après le début de la suppression du service (ou d’un déplacement vers un autre nœud).</span><span class="sxs-lookup"><span data-stu-id="f1839-241">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="f1839-242">Le fait de configurer l’intervalle de temps envoie la commande `docker stop <time in seconds>` au conteneur.</span><span class="sxs-lookup"><span data-stu-id="f1839-242">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="f1839-243">Pour plus d’informations, consultez [Arrêt du docker](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="f1839-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="f1839-244">L’intervalle de temps d’attente est spécifié dans la section `Hosting`.</span><span class="sxs-lookup"><span data-stu-id="f1839-244">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="f1839-245">L’extrait de manifeste de cluster suivant montre comment définir l’intervalle d’attente :</span><span class="sxs-lookup"><span data-stu-id="f1839-245">The following cluster manifest snippet shows how to set the wait interval:</span></span>

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
<span data-ttu-id="f1839-246">L’intervalle de temps par défaut est défini sur 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="f1839-246">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="f1839-247">Étant donné que cette configuration est dynamique, une mise à niveau uniquement de la configuration sur un cluster met à jour le délai d’expiration.</span><span class="sxs-lookup"><span data-stu-id="f1839-247">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="f1839-248">Configurer le runtime pour supprimer les images conteneur inutilisées</span><span class="sxs-lookup"><span data-stu-id="f1839-248">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="f1839-249">Vous pouvez configurer le cluster Service Fabric pour supprimer des images conteneur inutilisées à partir du nœud.</span><span class="sxs-lookup"><span data-stu-id="f1839-249">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="f1839-250">Cette configuration permet à l’espace disque d’être rétabli si trop d’images conteneur sont présentes sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="f1839-250">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="f1839-251">Pour activer cette fonctionnalité, mettez à jour la section `Hosting` du manifeste de cluster, comme indiqué dans l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="f1839-251">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


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

<span data-ttu-id="f1839-252">Vous pouvez les spécifier les images qui ne doivent pas être supprimées à l’aide du paramètre `ContainerImagesToSkip`.</span><span class="sxs-lookup"><span data-stu-id="f1839-252">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="f1839-253">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1839-253">Next steps</span></span>
* <span data-ttu-id="f1839-254">En savoir plus sur l’exécution des [conteneurs sur Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f1839-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="f1839-255">Consultez le didacticiel [Déployer une application .NET dans un conteneur vers Azure Service Fabric](service-fabric-host-app-in-a-container.md).</span><span class="sxs-lookup"><span data-stu-id="f1839-255">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="f1839-256">En savoir plus sur le [cycle de vie des applications](service-fabric-application-lifecycle.md) Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f1839-256">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="f1839-257">Consulter les [exemples de code de conteneur Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="f1839-257">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
