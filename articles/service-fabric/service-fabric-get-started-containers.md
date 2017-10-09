---
title: aaaCreate une application de conteneur Azure Service Fabric | Documents Microsoft
description: "Créez votre première application de conteneur Windows sur Microsoft Azure Service Fabric.  Créer une image Docker avec une application de Python, push de Registre de conteneur hello image tooa, générer et déployer une application de conteneur de Service Fabric."
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
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="59d09-104">Créer votre première application de conteneur Service Fabric sur Windows</span><span class="sxs-lookup"><span data-stu-id="59d09-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59d09-105">Windows</span><span class="sxs-lookup"><span data-stu-id="59d09-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="59d09-106">Linux</span><span class="sxs-lookup"><span data-stu-id="59d09-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="59d09-107">Exécution d’une application existante dans un conteneur Windows sur un cluster Service Fabric ne requiert pas n’importe quelle application tooyour de modifications.</span><span class="sxs-lookup"><span data-stu-id="59d09-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="59d09-108">Cet article vous guide dans la création d’une image Docker qui contient une Python [ballon](http://flask.pocoo.org/) web application et déploiement de cluster du Service Fabric tooa.</span><span class="sxs-lookup"><span data-stu-id="59d09-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="59d09-109">Vous allez également partager votre application en conteneur via [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="59d09-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="59d09-110">Cet article suppose une connaissance élémentaire de Docker.</span><span class="sxs-lookup"><span data-stu-id="59d09-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="59d09-111">Vous pouvez en savoir plus sur Docker par la lecture de hello [vue d’ensemble de Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="59d09-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59d09-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="59d09-112">Prerequisites</span></span>
<span data-ttu-id="59d09-113">Un ordinateur de développement exécutant :</span><span class="sxs-lookup"><span data-stu-id="59d09-113">A development computer running:</span></span>
* <span data-ttu-id="59d09-114">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="59d09-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="59d09-115">[Outils et SDK Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="59d09-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="59d09-116">Docker pour Windows.</span><span class="sxs-lookup"><span data-stu-id="59d09-116">Docker for Windows.</span></span>  <span data-ttu-id="59d09-117">[Obtenez Docker CE pour Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="59d09-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="59d09-118">Une fois l’installation et démarrage de Docker, avec le bouton droit sur l’icône de barre d’état hello et sélectionnez **basculer les conteneurs tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="59d09-118">After installing and starting Docker, right-click on hello tray icon and select **Switch tooWindows containers**.</span></span> <span data-ttu-id="59d09-119">Il s’agit de toorun requis Docker images basées sur Windows.</span><span class="sxs-lookup"><span data-stu-id="59d09-119">This is required toorun Docker images based on Windows.</span></span>

<span data-ttu-id="59d09-120">Un cluster Windows avec au moins trois nœuds s’exécutant sur Windows Server 2016 avec conteneurs. [Créez un cluster](service-fabric-cluster-creation-via-portal.md) ou [essayez gratuitement Service Fabric](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="59d09-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="59d09-121">Un registre dans Azure Container Registry. [Créez un registre de conteneurs](../container-registry/container-registry-get-started-portal.md) dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="59d09-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-hello-docker-container"></a><span data-ttu-id="59d09-122">Définir le conteneur Docker de hello</span><span class="sxs-lookup"><span data-stu-id="59d09-122">Define hello Docker container</span></span>
<span data-ttu-id="59d09-123">Générer une image basée sur hello [image de Python](https://hub.docker.com/_/python/) situé sur le Hub d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="59d09-123">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="59d09-124">Définissez votre conteneur Docker dans un fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="59d09-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="59d09-125">Hello Dockerfile contient des instructions pour configurer l’environnement hello à l’intérieur de votre conteneur, chargement de l’application hello souhaité toorun et mapper les ports.</span><span class="sxs-lookup"><span data-stu-id="59d09-125">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="59d09-126">Hello Dockerfile est toohello d’entrée de hello `docker build` commande qui crée l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-126">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span>

<span data-ttu-id="59d09-127">Créer un répertoire vide et créer le fichier de hello *Dockerfile* (avec aucune extension de fichier).</span><span class="sxs-lookup"><span data-stu-id="59d09-127">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="59d09-128">Ajouter hello suivant trop*Dockerfile* et enregistrer vos modifications :</span><span class="sxs-lookup"><span data-stu-id="59d09-128">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="59d09-129">Hello de lecture [informations de référence](https://docs.docker.com/engine/reference/builder/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="59d09-129">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="59d09-130">Créer une application web simple</span><span class="sxs-lookup"><span data-stu-id="59d09-130">Create a simple web application</span></span>
<span data-ttu-id="59d09-131">Créez une application web Flask écoutant le port 80 qui renvoie « Hello World! ».</span><span class="sxs-lookup"><span data-stu-id="59d09-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="59d09-132">Dans l’hello même répertoire, créez le fichier de hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="59d09-132">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="59d09-133">Ajoutez hello suivant et enregistrez vos modifications :</span><span class="sxs-lookup"><span data-stu-id="59d09-133">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="59d09-134">Créer également des hello *app.py* de fichiers et ajoutez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="59d09-134">Also create hello *app.py* file and add hello following:</span></span>

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
## <a name="build-hello-image"></a><span data-ttu-id="59d09-135">Générer l’image de hello</span><span class="sxs-lookup"><span data-stu-id="59d09-135">Build hello image</span></span>
<span data-ttu-id="59d09-136">Exécutez hello `docker build` commande toocreate hello image qui exécute votre application web.</span><span class="sxs-lookup"><span data-stu-id="59d09-136">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="59d09-137">Ouvrez une fenêtre PowerShell et accédez répertoire toohello contenant hello Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="59d09-137">Open a PowerShell window and navigate toohello directory containing hello Dockerfile.</span></span> <span data-ttu-id="59d09-138">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="59d09-138">Run hello following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="59d09-139">Cette commande builds hello nouvelle image à l’aide des instructions de hello dans votre fichier Dockerfile, d’affectation de noms (-t marquage) l’image hello « helloworldapp ».</span><span class="sxs-lookup"><span data-stu-id="59d09-139">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="59d09-140">Génération d’une image extrait l’image de base hello vers le bas à partir du Hub d’ancrage et crée une image qui ajoute votre application sur l’image de base hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-140">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="59d09-141">Une fois la commande de génération hello terminée, exécutez hello `docker images` toosee plus d’informations sur la nouvelle image de hello de commandes :</span><span class="sxs-lookup"><span data-stu-id="59d09-141">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="59d09-142">Exécutez hello application localement</span><span class="sxs-lookup"><span data-stu-id="59d09-142">Run hello application locally</span></span>
<span data-ttu-id="59d09-143">Vérifiez votre image localement avant d’en exécutant un push du Registre de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-143">Verify your image locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="59d09-144">Exécutez l’application hello :</span><span class="sxs-lookup"><span data-stu-id="59d09-144">Run hello application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="59d09-145">*nom* donne un toohello nom du conteneur (au lieu de l’ID de conteneur hello) en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="59d09-145">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="59d09-146">Une fois le conteneur de hello démarre, trouver son adresse IP afin de pouvoir vous connecter tooyour conteneur en cours d’exécution à partir d’un navigateur :</span><span class="sxs-lookup"><span data-stu-id="59d09-146">Once hello container starts, find its IP address so that you can connect tooyour running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="59d09-147">Se connecter toohello conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="59d09-147">Connect toohello running container.</span></span>  <span data-ttu-id="59d09-148">Ouvrez un navigateur web pointant toohello adresse IP retournée, par exemple « http://172.31.194.61 ».</span><span class="sxs-lookup"><span data-stu-id="59d09-148">Open a web browser pointing toohello IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="59d09-149">Vous devez voir hello titre « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="59d09-149">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="59d09-150">afficher dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-150">display in hello browser.</span></span>

<span data-ttu-id="59d09-151">toostop votre conteneur, exécutez :</span><span class="sxs-lookup"><span data-stu-id="59d09-151">toostop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="59d09-152">Supprimer le conteneur de hello à partir de votre ordinateur de développement :</span><span class="sxs-lookup"><span data-stu-id="59d09-152">Delete hello container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="59d09-153">Registre de conteneur push hello image toohello</span><span class="sxs-lookup"><span data-stu-id="59d09-153">Push hello image toohello container registry</span></span>
<span data-ttu-id="59d09-154">Après avoir vérifié que le conteneur de hello s’exécute sur votre ordinateur de développement, push de Registre de tooyour hello image dans le Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="59d09-154">After you verify that hello container runs on your development machine, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="59d09-155">Exécutez ``docker login`` toolog dans le Registre de conteneur tooyour avec votre [informations d’identification du Registre](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="59d09-155">Run ``docker login`` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="59d09-156">Hello exemple suivant passe hello ID et mot de passe d’Azure Active Directory [principal du service](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="59d09-156">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="59d09-157">Par exemple, vous avez peut-être affectés un Registre tooyour principal de service pour un scénario d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="59d09-157">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span> <span data-ttu-id="59d09-158">Ou bien, vous pouvez vous connecter à l’aide de votre nom d’utilisateur de registre et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="59d09-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="59d09-159">Hello commande suivante crée une balise ou un alias de l’image de hello, avec un Registre tooyour de chemin d’accès qualifié complet.</span><span class="sxs-lookup"><span data-stu-id="59d09-159">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="59d09-160">Cet exemple place hello image Bonjour ```samples``` encombrement de l’espace de noms tooavoid dans la racine du Registre de hello hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-160">This example places hello image in hello ```samples``` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="59d09-161">Registre de conteneur tooyour push hello image :</span><span class="sxs-lookup"><span data-stu-id="59d09-161">Push hello image tooyour container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a><span data-ttu-id="59d09-162">Créer un service de hello placées dans des conteneurs dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59d09-162">Create hello containerized service in Visual Studio</span></span>
<span data-ttu-id="59d09-163">Hello Service Fabric SDK et outils fournissent une toohelp de modèle de service vous créez une application en conteneur.</span><span class="sxs-lookup"><span data-stu-id="59d09-163">hello Service Fabric SDK and tools provide a service template toohelp you create a containerized application.</span></span>

1. <span data-ttu-id="59d09-164">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59d09-164">Start Visual Studio.</span></span>  <span data-ttu-id="59d09-165">Sélectionnez **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="59d09-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="59d09-166">Sélectionnez **Service Fabric application** (Application Service Fabric), nommez-la « MyFirstContainer », puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="59d09-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="59d09-167">Sélectionnez **invité conteneur** à partir de la liste des hello **les modèles de service**.</span><span class="sxs-lookup"><span data-stu-id="59d09-167">Select **Guest Container** from hello list of **service templates**.</span></span>
4. <span data-ttu-id="59d09-168">Dans **nom de l’Image** Entrez « myregistry.azurecr.io/samples/helloworldapp », image hello envoyées de référentiel de conteneurs tooyour.</span><span class="sxs-lookup"><span data-stu-id="59d09-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", hello image you pushed tooyour container repository.</span></span>
5. <span data-ttu-id="59d09-169">Donnez un nom à votre service et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="59d09-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="59d09-170">Configurer la communication</span><span class="sxs-lookup"><span data-stu-id="59d09-170">Configure communication</span></span>
<span data-ttu-id="59d09-171">service de Hello en conteneur a besoin d’un point de terminaison pour la communication.</span><span class="sxs-lookup"><span data-stu-id="59d09-171">hello containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="59d09-172">Ajouter un `Endpoint` élément avec le fichier ServiceManifest.xml toohello du type, le port et protocole de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-172">Add an `Endpoint` element with hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="59d09-173">Pour cet article, hello placées dans des conteneurs service écoute le port 8081.</span><span class="sxs-lookup"><span data-stu-id="59d09-173">For this article, hello containerized service listens on port 8081.</span></span>  <span data-ttu-id="59d09-174">Dans cet exemple, un port fixe 8081 est utilisé.</span><span class="sxs-lookup"><span data-stu-id="59d09-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="59d09-175">Si aucun port n’est spécifié, un port aléatoire à partir de la plage de ports d’application hello est choisi.</span><span class="sxs-lookup"><span data-stu-id="59d09-175">If no port is specified, a random port from hello application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="59d09-176">En définissant un point de terminaison, l’infrastructure de Service publie toohello de point de terminaison hello Naming service.</span><span class="sxs-lookup"><span data-stu-id="59d09-176">By defining an endpoint, Service Fabric publishes hello endpoint toohello Naming service.</span></span>  <span data-ttu-id="59d09-177">Autres services qui s’exécutent dans un cluster de hello peuvent résoudre ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="59d09-177">Other services running in hello cluster can resolve this container.</span></span>  <span data-ttu-id="59d09-178">Vous pouvez également effectuer la communication de conteneur à l’autre à l’aide de hello [proxy inverse](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="59d09-178">You can also perform container-to-container communication using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="59d09-179">Communication est effectuée en fournissant le port d’écoute hello proxy inverse HTTP et le nom hello de services hello que vous souhaitez toocommunicate avec comme variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="59d09-179">Communication is performed by providing hello reverse proxy HTTP listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="59d09-180">Configurer et définir des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="59d09-180">Configure and set environment variables</span></span>
<span data-ttu-id="59d09-181">Variables d’environnement peuvent être spécifiées pour chaque package de code dans le manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-181">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="59d09-182">Cette fonctionnalité est disponible pour tous les services, qu’ils soient déployés sous forme de conteneurs, de processus ou d’exécutables invités.</span><span class="sxs-lookup"><span data-stu-id="59d09-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="59d09-183">Vous pouvez remplacer la variable d’environnement valeurs dans une application hello manifeste ou spécifient durant le déploiement en tant que paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="59d09-183">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="59d09-184">Hello service manifeste XML extrait de code suivant illustre un exemple de variables d’environnement toospecify pour un package de code :</span><span class="sxs-lookup"><span data-stu-id="59d09-184">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="59d09-185">Ces variables d’environnement peuvent être remplacées dans le manifeste de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="59d09-185">These environment variables can be overridden in hello application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="59d09-186">Configuration du mappage des ports de conteneur aux ports hôtes et de la détection de conteneur à conteneur</span><span class="sxs-lookup"><span data-stu-id="59d09-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="59d09-187">Configurer un toocommunicate de port utilisé hôte avec le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-187">Configure a host port used toocommunicate  with hello container.</span></span> <span data-ttu-id="59d09-188">liaison de port Hello mappe le port de hello sur quel hello service écoute à l’intérieur de hello conteneur tooa port sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-188">hello port binding maps hello port on which hello service is listening inside hello container tooa port on hello host.</span></span> <span data-ttu-id="59d09-189">Ajouter un `PortBinding` élément `ContainerHostPolicies` élément du fichier de ApplicationManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-189">Add a `PortBinding` element in `ContainerHostPolicies` element of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="59d09-190">Pour cet article, `ContainerPort` est 80 (conteneur de hello expose le port 80, comme spécifié dans hello Dockerfile) et `EndpointRef` est « Guest1TypeEndpoint » (hello de point de terminaison défini précédemment dans le manifeste de service hello).</span><span class="sxs-lookup"><span data-stu-id="59d09-190">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (hello endpoint previously defined in hello service manifest).</span></span>  <span data-ttu-id="59d09-191">Les demandes entrantes sur le port 8081 du service toohello sont mappées tooport 80 sur le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-191">Incoming requests toohello service on port 8081 are mapped tooport 80 on hello container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="59d09-192">Configurer l’authentification au registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="59d09-192">Configure container registry authentication</span></span>
<span data-ttu-id="59d09-193">Configurer l’authentification de Registre de conteneur en ajoutant `RepositoryCredentials` trop`ContainerHostPolicies` du fichier de ApplicationManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-193">Configure container registry authentication by adding `RepositoryCredentials` too`ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span> <span data-ttu-id="59d09-194">Ajoutez hello et mot de passe pour le Registre de conteneur hello myregistry.azurecr.io, ce qui permet l’image de conteneur hello service toodownload hello à partir du référentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-194">Add hello account and password for hello myregistry.azurecr.io container registry, which allows hello service toodownload hello container image from hello repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="59d09-195">Nous vous conseillons de chiffrer un mot de passe hello référentiel en utilisant un certificat de chiffrement qui a déployé tooall des nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-195">We recommend that you encrypt hello repository password by using an encipherment certificate that's deployed tooall nodes of hello cluster.</span></span> <span data-ttu-id="59d09-196">Lorsque le Service Fabric déploie hello service package toohello de cluster, certificat de chiffrement hello est texte de chiffrement utilisé toodecrypt hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-196">When Service Fabric deploys hello service package toohello cluster, hello encipherment certificate is used toodecrypt hello cipher text.</span></span>  <span data-ttu-id="59d09-197">applet de commande Invoke-ServiceFabricEncryptText Hello est le texte de chiffrement hello toocreate utilisé pour le mot de passe hello, qui est ajouté toohello ApplicationManifest.xml fichier.</span><span class="sxs-lookup"><span data-stu-id="59d09-197">hello Invoke-ServiceFabricEncryptText cmdlet is used toocreate hello cipher text for hello password, which is added toohello ApplicationManifest.xml file.</span></span>

<span data-ttu-id="59d09-198">Bonjour script suivant crée un certificat auto-signé et il exporte le fichier PFX tooa.</span><span class="sxs-lookup"><span data-stu-id="59d09-198">hello following script creates a new self-signed certificate and exports it tooa PFX file.</span></span>  <span data-ttu-id="59d09-199">certificat de Hello est importé dans un coffre de clés existant et puis déployé cluster Service Fabric de toohello.</span><span class="sxs-lookup"><span data-stu-id="59d09-199">hello certificate is imported into an existing key vault and then deployed toohello Service Fabric cluster.</span></span>

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

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="59d09-200">Chiffrer le mot de passe hello à l’aide de hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="59d09-200">Encrypt hello password using hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="59d09-201">Remplacez le mot de passe de hello avec le texte de chiffrement hello retourné par hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) applet de commande et la valeur `PasswordEncrypted` trop à la valeur « true ».</span><span class="sxs-lookup"><span data-stu-id="59d09-201">Replace hello password with hello cipher text returned by hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` too"true".</span></span>

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

## <a name="configure-isolation-mode"></a><span data-ttu-id="59d09-202">Configurer le mode d’isolation</span><span class="sxs-lookup"><span data-stu-id="59d09-202">Configure isolation mode</span></span>
<span data-ttu-id="59d09-203">Windows prend en charge deux modes d’isolation pour les conteneurs : Processus et Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="59d09-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="59d09-204">Avec le mode d’isolation du processus de hello, en cours d’exécution tous les conteneurs de hello hello même hôte ordinateur partage hello du noyau avec l’hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-204">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="59d09-205">Avec le mode d’isolation hello Hyper-V, les noyaux hello sont isolées entre chaque conteneur Hyper-V et l’hôte de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-205">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="59d09-206">le mode d’isolation Hello est spécifié dans hello `ContainerHostPolicies` élément dans le fichier manifeste d’application hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-206">hello isolation mode is specified in hello `ContainerHostPolicies` element in hello application manifest file.</span></span> <span data-ttu-id="59d09-207">modes d’isolation Hello qui peuvent être spécifiées sont `process`, `hyperv`, et `default`.</span><span class="sxs-lookup"><span data-stu-id="59d09-207">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="59d09-208">mode d’isolement Hello par défaut est trop`process` sur Windows Server héberge et la valeur par défaut est trop`hyperv` sur des hôtes Windows 10.</span><span class="sxs-lookup"><span data-stu-id="59d09-208">hello default isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="59d09-209">Hello extrait de code suivant montre comment le mode d’isolation hello est défini dans le fichier manifeste d’application hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-209">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="59d09-210">Configurer la gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="59d09-210">Configure resource governance</span></span>
<span data-ttu-id="59d09-211">[Gouvernance des ressources](service-fabric-resource-governance.md) restreint hello ressources hello conteneur peuvent utiliser sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-211">[Resource governance](service-fabric-resource-governance.md) restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="59d09-212">Hello `ResourceGovernancePolicy` élément, qui est spécifié dans le manifeste de l’application hello, est utilisé toodeclare des limites de ressources pour un package de code de service.</span><span class="sxs-lookup"><span data-stu-id="59d09-212">hello `ResourceGovernancePolicy` element, which is specified in hello application manifest, is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="59d09-213">Les limites de ressources peuvent être définies pour hello suivant des ressources : mémoire, MemorySwap, CpuShares (poids relatif de l’UC), MemoryReservationInMB, BlkioWeight (BlockIO le poids relatif).</span><span class="sxs-lookup"><span data-stu-id="59d09-213">Resource limits can be set for hello following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="59d09-214">Dans cet exemple, le package de service Guest1Pkg Obtient un cœur sur les nœuds de cluster hello où il est placé.</span><span class="sxs-lookup"><span data-stu-id="59d09-214">In this example, service package Guest1Pkg gets one core on hello cluster nodes where it is placed.</span></span>  <span data-ttu-id="59d09-215">Limites de la mémoire étant absolus, le package de code hello est limitée too1024 Mo de mémoire (et une réservation soft-garantie de hello même).</span><span class="sxs-lookup"><span data-stu-id="59d09-215">Memory limits are absolute, so hello code package is limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="59d09-216">Packages de code (conteneurs ou processus) ne sont pas en mesure de tooallocate plus de mémoire que cette limite et de tenter de toodo engendre une exception de mémoire insuffisante.</span><span class="sxs-lookup"><span data-stu-id="59d09-216">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="59d09-217">Pour toowork de mise en œuvre de limite de ressource, tous les packages de code au sein d’un package de service doivent avoir des limites de mémoire spécifiées.</span><span class="sxs-lookup"><span data-stu-id="59d09-217">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a><span data-ttu-id="59d09-218">Déployer l’application de conteneur hello</span><span class="sxs-lookup"><span data-stu-id="59d09-218">Deploy hello container application</span></span>
<span data-ttu-id="59d09-219">Enregistrer toutes vos modifications et générer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-219">Save all your changes and build hello application.</span></span> <span data-ttu-id="59d09-220">toopublish votre application, avec le bouton droit sur **MyFirstContainer** dans l’Explorateur de solutions, puis sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="59d09-220">toopublish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="59d09-221">Dans **connexion de point de terminaison**, entrez le point de terminaison de gestion hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-221">In **Connection Endpoint**, enter hello management endpoint for hello cluster.</span></span>  <span data-ttu-id="59d09-222">Par exemple : « containercluster.westus2.cloudapp.azure.com:19000 ».</span><span class="sxs-lookup"><span data-stu-id="59d09-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="59d09-223">Vous pouvez trouver la connexion de client hello point de terminaison dans le panneau de vue d’ensemble de hello pour votre cluster Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="59d09-223">You can find hello client connection endpoint in hello Overview blade for your cluster in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="59d09-224">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="59d09-224">Click **Publish**.</span></span>

<span data-ttu-id="59d09-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) est un outil web dédié à l’inspection et à la gestion d’applications et de nœuds dans un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="59d09-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="59d09-226">Ouvrez un navigateur et accédez toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorateur et suivez le déploiement de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-226">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow hello application deployment.</span></span>  <span data-ttu-id="59d09-227">application Hello déploie mais se trouve dans un état d’erreur jusqu'à ce que l’image de hello est téléchargé sur les nœuds de cluster hello (qui peuvent prendre un certain temps, en fonction de la taille de l’image hello) : ![erreur][1]</span><span class="sxs-lookup"><span data-stu-id="59d09-227">hello application deploys but is in an error state until hello image is downloaded on hello cluster nodes (which can take some time, depending on hello image size): ![Error][1]</span></span>

<span data-ttu-id="59d09-228">application Hello est prête, lorsqu’il est dans ```Ready``` état : ![prêt][2]</span><span class="sxs-lookup"><span data-stu-id="59d09-228">hello application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="59d09-229">Ouvrez un navigateur et accédez toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="59d09-229">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="59d09-230">Vous devez voir hello titre « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="59d09-230">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="59d09-231">afficher dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-231">display in hello browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="59d09-232">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="59d09-232">Clean up</span></span>
<span data-ttu-id="59d09-233">Vous continuer tooincur frais pendant l’exécution du cluster de hello, envisagez de [la suppression de votre cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="59d09-233">You continue tooincur charges while hello cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="59d09-234">Les [clusters d’essai](http://tryazureservicefabric.westus.cloudapp.azure.com/) sont automatiquement supprimés après quelques heures.</span><span class="sxs-lookup"><span data-stu-id="59d09-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="59d09-235">Une fois que vous effectuez un push Registre de conteneur toohello hello image, vous pouvez supprimer les images locales hello à partir de votre ordinateur de développement :</span><span class="sxs-lookup"><span data-stu-id="59d09-235">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="59d09-236">Exemples complets de manifestes d’application et de service Service Fabric</span><span class="sxs-lookup"><span data-stu-id="59d09-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="59d09-237">Voici complète du service hello et des manifestes d’application utilisés dans cet article.</span><span class="sxs-lookup"><span data-stu-id="59d09-237">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="59d09-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="59d09-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="59d09-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="59d09-239">ApplicationManifest.xml</span></span>
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
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
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
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="59d09-240">Configurer l’intervalle de temps d’attente avant l’arrêt forcé du conteneur</span><span class="sxs-lookup"><span data-stu-id="59d09-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="59d09-241">Vous pouvez configurer un intervalle de temps pour hello runtime toowait avant la suppression du conteneur de hello après que hello suppression du service (ou un nœud de tooanother move) a démarré.</span><span class="sxs-lookup"><span data-stu-id="59d09-241">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="59d09-242">Intervalle de temps hello configuration envoie hello `docker stop <time in seconds>` conteneur toohello de commande.</span><span class="sxs-lookup"><span data-stu-id="59d09-242">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="59d09-243">Pour plus d’informations, consultez [Arrêt du docker](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="59d09-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="59d09-244">toowait d’intervalle de temps Hello est spécifié sous hello `Hosting` section.</span><span class="sxs-lookup"><span data-stu-id="59d09-244">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="59d09-245">Hello suivant extrait de manifeste de cluster montre comment tooset hello délai d’attente :</span><span class="sxs-lookup"><span data-stu-id="59d09-245">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="59d09-246">Hello intervalle de temps par défaut a la valeur too10 secondes.</span><span class="sxs-lookup"><span data-stu-id="59d09-246">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="59d09-247">Étant donné que cette configuration est dynamique, une configuration uniquement mettre à niveau sur le délai d’attente de hello cluster mises à jour hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-247">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="59d09-248">Configurer hello runtime tooremove les images de conteneur inutilisé</span><span class="sxs-lookup"><span data-stu-id="59d09-248">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="59d09-249">Vous pouvez configurer tooremove de cluster Service Fabric hello des images de conteneur inutilisé à partir du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-249">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="59d09-250">Cette configuration permet de toobe d’espace disque rétabli si trop d’images de conteneur sont présents sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="59d09-250">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="59d09-251">tooenable cette fonctionnalité, la mise à jour hello `Hosting` section dans le manifeste du cluster hello, comme indiqué dans hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="59d09-251">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="59d09-252">Pour les images qui ne doivent pas être supprimés, vous pouvez les spécifier sous hello `ContainerImagesToSkip` paramètre.</span><span class="sxs-lookup"><span data-stu-id="59d09-252">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="59d09-253">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59d09-253">Next steps</span></span>
* <span data-ttu-id="59d09-254">En savoir plus sur l’exécution des [conteneurs sur Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59d09-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="59d09-255">Hello de lecture [déployer une application .NET dans un conteneur](service-fabric-host-app-in-a-container.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="59d09-255">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="59d09-256">En savoir plus sur hello Service Fabric [cycle de vie des applications](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="59d09-256">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="59d09-257">Hello d’extraction [exemples de code de Service Fabric conteneur](https://github.com/Azure-Samples/service-fabric-dotnet-containers) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="59d09-257">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
