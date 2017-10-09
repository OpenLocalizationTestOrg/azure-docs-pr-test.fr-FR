---
title: aaaCreate une application de conteneur Azure Service Fabric sur Linux | Documents Microsoft
description: "Créez votre première application de conteneur Linux sur Microsoft Azure Service Fabric.  Créer une image Docker avec votre application, push de Registre de conteneur hello image tooa, générer et déployer une application de conteneur de Service Fabric."
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
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="4304d-104">Créer votre première application de conteneur Service Fabric sur Linux</span><span class="sxs-lookup"><span data-stu-id="4304d-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4304d-105">Windows</span><span class="sxs-lookup"><span data-stu-id="4304d-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="4304d-106">Linux</span><span class="sxs-lookup"><span data-stu-id="4304d-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="4304d-107">Exécution d’une application existante dans un conteneur de Linux sur un cluster Service Fabric ne requiert pas n’importe quelle application tooyour de modifications.</span><span class="sxs-lookup"><span data-stu-id="4304d-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="4304d-108">Cet article vous guide dans la création d’une image Docker qui contient une Python [ballon](http://flask.pocoo.org/) web application et déploiement de cluster du Service Fabric tooa.</span><span class="sxs-lookup"><span data-stu-id="4304d-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="4304d-109">Vous allez également partager votre application en conteneur via [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="4304d-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="4304d-110">Cet article suppose une connaissance élémentaire de Docker.</span><span class="sxs-lookup"><span data-stu-id="4304d-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="4304d-111">Vous pouvez en savoir plus sur Docker par la lecture de hello [vue d’ensemble de Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="4304d-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4304d-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4304d-112">Prerequisites</span></span>
* <span data-ttu-id="4304d-113">Un ordinateur de développement exécutant :</span><span class="sxs-lookup"><span data-stu-id="4304d-113">A development computer running:</span></span>
  * <span data-ttu-id="4304d-114">[Outils et SDK Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4304d-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="4304d-115">[Docker CE pour Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="4304d-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="4304d-116">Interface de ligne de commande de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4304d-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="4304d-117">Un registre dans Azure Container Registry. [Créez un registre de conteneurs](../container-registry/container-registry-get-started-portal.md) dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4304d-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="4304d-118">Définir le conteneur Docker de hello</span><span class="sxs-lookup"><span data-stu-id="4304d-118">Define hello Docker container</span></span>
<span data-ttu-id="4304d-119">Générer une image basée sur hello [image de Python](https://hub.docker.com/_/python/) situé sur le Hub d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="4304d-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="4304d-120">Définissez votre conteneur Docker dans un fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="4304d-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="4304d-121">Hello Dockerfile contient des instructions pour configurer l’environnement hello à l’intérieur de votre conteneur, chargement de l’application hello souhaité toorun et mapper les ports.</span><span class="sxs-lookup"><span data-stu-id="4304d-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="4304d-122">Hello Dockerfile est toohello d’entrée de hello `docker build` commande qui crée l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="4304d-123">Créer un répertoire vide et créer le fichier de hello *Dockerfile* (avec aucune extension de fichier).</span><span class="sxs-lookup"><span data-stu-id="4304d-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="4304d-124">Ajouter hello suivant trop*Dockerfile* et enregistrer vos modifications :</span><span class="sxs-lookup"><span data-stu-id="4304d-124">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="4304d-125">Hello de lecture [informations de référence](https://docs.docker.com/engine/reference/builder/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4304d-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="4304d-126">Créer une application web simple</span><span class="sxs-lookup"><span data-stu-id="4304d-126">Create a simple web application</span></span>
<span data-ttu-id="4304d-127">Créez une application web Flask écoutant le port 80 qui renvoie « Hello World! ».</span><span class="sxs-lookup"><span data-stu-id="4304d-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="4304d-128">Dans l’hello même répertoire, créez le fichier de hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="4304d-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="4304d-129">Ajoutez hello suivant et enregistrez vos modifications :</span><span class="sxs-lookup"><span data-stu-id="4304d-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="4304d-130">Créer également des hello *app.py* de fichiers et ajoutez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="4304d-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="4304d-131">Générer l’image de hello</span><span class="sxs-lookup"><span data-stu-id="4304d-131">Build hello image</span></span>
<span data-ttu-id="4304d-132">Exécutez hello `docker build` commande toocreate hello image qui exécute votre application web.</span><span class="sxs-lookup"><span data-stu-id="4304d-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="4304d-133">Ouvrez une fenêtre PowerShell et accédez trop*c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="4304d-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="4304d-134">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4304d-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="4304d-135">Cette commande builds hello nouvelle image à l’aide des instructions de hello dans votre fichier Dockerfile, d’affectation de noms (-t marquage) l’image hello « helloworldapp ».</span><span class="sxs-lookup"><span data-stu-id="4304d-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="4304d-136">Génération d’une image extrait l’image de base hello vers le bas à partir du Hub d’ancrage et crée une image qui ajoute votre application sur l’image de base hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="4304d-137">Une fois la commande de génération hello terminée, exécutez hello `docker images` toosee plus d’informations sur la nouvelle image de hello de commandes :</span><span class="sxs-lookup"><span data-stu-id="4304d-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="4304d-138">Exécutez hello application localement</span><span class="sxs-lookup"><span data-stu-id="4304d-138">Run hello application locally</span></span>
<span data-ttu-id="4304d-139">Vérifiez que votre application en conteneur s’exécute localement avant d’en exécutant un push du Registre de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="4304d-140">Exécutez l’application hello, mappage du conteneur de votre ordinateur port 4000 toohello exposées le port 80 :</span><span class="sxs-lookup"><span data-stu-id="4304d-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="4304d-141">*nom* donne un toohello nom du conteneur (au lieu de l’ID de conteneur hello) en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4304d-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="4304d-142">Se connecter toohello conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4304d-142">Connect toohello running container.</span></span>  <span data-ttu-id="4304d-143">Ouvrez un navigateur web pointant adresse toohello renvoyé sur le port 4000, par exemple « http://localhost:4000 ».</span><span class="sxs-lookup"><span data-stu-id="4304d-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="4304d-144">Vous devez voir hello titre « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="4304d-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="4304d-145">afficher dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-145">display in hello browser.</span></span>

![Hello World!][hello-world]

<span data-ttu-id="4304d-147">toostop votre conteneur, exécutez :</span><span class="sxs-lookup"><span data-stu-id="4304d-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="4304d-148">Supprimer le conteneur de hello à partir de votre ordinateur de développement :</span><span class="sxs-lookup"><span data-stu-id="4304d-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="4304d-149">Registre de conteneur push hello image toohello</span><span class="sxs-lookup"><span data-stu-id="4304d-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="4304d-150">Après avoir vérifié que l’application hello s’exécute dans Docker, push de Registre de tooyour hello image dans le Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="4304d-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="4304d-151">Exécutez `docker login` toolog dans le Registre de conteneur tooyour avec votre [informations d’identification du Registre](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4304d-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="4304d-152">Hello exemple suivant passe hello ID et mot de passe d’Azure Active Directory [principal du service](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="4304d-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="4304d-153">Par exemple, vous avez peut-être affectés un Registre tooyour principal de service pour un scénario d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="4304d-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="4304d-154">Ou bien, vous pouvez vous connecter à l’aide de votre nom d’utilisateur de registre et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4304d-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="4304d-155">Hello commande suivante crée une balise ou un alias de l’image de hello, avec un Registre tooyour de chemin d’accès qualifié complet.</span><span class="sxs-lookup"><span data-stu-id="4304d-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="4304d-156">Cet exemple place hello image Bonjour `samples` encombrement de l’espace de noms tooavoid dans la racine du Registre de hello hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="4304d-157">Registre de conteneur tooyour push hello image :</span><span class="sxs-lookup"><span data-stu-id="4304d-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="4304d-158">Le package d’image de Docker hello avec Yeoman</span><span class="sxs-lookup"><span data-stu-id="4304d-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="4304d-159">Hello SDK de l’infrastructure de Service pour Linux comprend un [Yeoman](http://yeoman.io/) générateur qui rend toocreate facilement votre application et ajouter une image de conteneur.</span><span class="sxs-lookup"><span data-stu-id="4304d-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="4304d-160">Nous allons utiliser Yeoman toocreate appelée par une application avec un seul conteneur Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="4304d-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="4304d-161">toocreate une application conteneur de l’infrastructure de Service, ouvrez une fenêtre de terminal et exécutez `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="4304d-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="4304d-162">Nommez votre application (par exemple, « mycontainer »).</span><span class="sxs-lookup"><span data-stu-id="4304d-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="4304d-163">Fournir les URL de hello pour les images de conteneur hello dans un Registre de conteneur (par exemple, « »).</span><span class="sxs-lookup"><span data-stu-id="4304d-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="4304d-164">Cette image a une charge de travail-point d’entrée défini, donc besoin tooexplicitly de spécifier des commandes d’entrée (les commandes exécutées à l’intérieur du conteneur hello, qui conserve conteneur hello en cours d’exécution après le démarrage).</span><span class="sxs-lookup"><span data-stu-id="4304d-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="4304d-165">Spécifiez un nombre d’instances de « 1 ».</span><span class="sxs-lookup"><span data-stu-id="4304d-165">Specify an instance count of "1".</span></span>

![Générateur Yeoman Service Fabric pour les conteneurs][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="4304d-167">Configurer l’authentification de référentiel de conteneur et le mappage de port</span><span class="sxs-lookup"><span data-stu-id="4304d-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="4304d-168">Votre service en conteneur a besoin d’un point de terminaison pour la communication.</span><span class="sxs-lookup"><span data-stu-id="4304d-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="4304d-169">Maintenant ajouter hello protocole, port et type tooan `Endpoint` dans le fichier ServiceManifest.xml de hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="4304d-170">Pour cet article, hello placées dans des conteneurs service écoute le port 4000 :</span><span class="sxs-lookup"><span data-stu-id="4304d-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="4304d-171">Fournissant hello `UriScheme` automatiquement registres hello le point de terminaison de conteneur avec hello Service Fabric d’affectation de noms de service pour la fonctionnalité de découverte.</span><span class="sxs-lookup"><span data-stu-id="4304d-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="4304d-172">Un exemple de fichier ServiceManifest.xml complète est fournie à la fin de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="4304d-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="4304d-173">Configurer le mappage de port de port du conteneur-hôte hello en spécifiant un `PortBinding` stratégie dans `ContainerHostPolicies` du fichier de ApplicationManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="4304d-174">Pour cet article, `ContainerPort` est 80 (conteneur de hello expose le port 80, comme spécifié dans hello Dockerfile) et `EndpointRef` est « myserviceTypeEndpoint » (point de terminaison d’hello défini dans le manifeste de service hello).</span><span class="sxs-lookup"><span data-stu-id="4304d-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="4304d-175">Les demandes entrantes du service sur le port 4000 toohello sont mappées tooport 80 sur le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="4304d-176">Si votre conteneur doit tooauthenticate avec un référentiel privé, puis ajoutez `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="4304d-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="4304d-177">Pour cet article, ajouter le nom du compte hello et un mot de passe pour le Registre de conteneur myregistry.azurecr.io hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="4304d-178">Génération et package d’application de Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="4304d-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="4304d-179">modèles de Service Fabric Yeoman Hello incluent un script de génération pour [Gradle](https://gradle.org/), vous pouvez utiliser application hello toobuild hello Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="4304d-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="4304d-180">toobuild et package d’application hello, exécutez hello suivante :</span><span class="sxs-lookup"><span data-stu-id="4304d-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="4304d-181">Déployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="4304d-181">Deploy hello application</span></span>
<span data-ttu-id="4304d-182">Une fois que l’application hello est générée, vous pouvez le déployer toohello cluster local à l’aide de hello CLI de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="4304d-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="4304d-183">Connectez le cluster Service Fabric local de toohello.</span><span class="sxs-lookup"><span data-stu-id="4304d-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="4304d-184">Hello d’utilisation script d’installation fournies dans hello modèle toocopy application hello magasin d’images du cluster toohello du package, inscrire le type d’application hello et créer une instance de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="4304d-185">Ouvrez un navigateur et accédez tooService Fabric Explorer dans http://localhost:19080/Explorateur (remplacer localhost avec adresse IP privée hello Hello machine virtuelle si vous utilisez Vagrant sur Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="4304d-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="4304d-186">Développez le nœud Applications de hello et notez qu’il existe désormais une entrée pour votre type d’application et un autre pour la première instance de ce type de hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="4304d-187">Se connecter toohello conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4304d-187">Connect toohello running container.</span></span>  <span data-ttu-id="4304d-188">Ouvrez un navigateur web pointant adresse toohello renvoyé sur le port 4000, par exemple « http://localhost:4000 ».</span><span class="sxs-lookup"><span data-stu-id="4304d-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="4304d-189">Vous devez voir hello titre « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="4304d-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="4304d-190">afficher dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-190">display in hello browser.</span></span>

![Hello World!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="4304d-192">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="4304d-192">Clean up</span></span>
<span data-ttu-id="4304d-193">Utiliser un script de désinstallation hello fournies dans l’instance d’application hello modèle toodelete hello du cluster de développement local hello et annuler l’inscription du type de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="4304d-194">Une fois que vous effectuez un push Registre de conteneur toohello hello image, vous pouvez supprimer les images locales hello à partir de votre ordinateur de développement :</span><span class="sxs-lookup"><span data-stu-id="4304d-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="4304d-195">Exemples complets de manifestes d’application et de service Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4304d-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="4304d-196">Voici complète du service hello et des manifestes d’application utilisés dans cet article.</span><span class="sxs-lookup"><span data-stu-id="4304d-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="4304d-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="4304d-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="4304d-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="4304d-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
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
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="4304d-199">Ajout d’application existante de plusieurs services tooan</span><span class="sxs-lookup"><span data-stu-id="4304d-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="4304d-200">effectuer d’une autre application tooan service conteneur déjà créée à l’aide d’yeoman, tooadd hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4304d-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="4304d-201">Modifier la racine toohello du répertoire d’application existant hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="4304d-202">Par exemple, `cd ~/YeomanSamples/MyApplication`si `MyApplication` est l’application hello créée par Yeoman.</span><span class="sxs-lookup"><span data-stu-id="4304d-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="4304d-203">Exécutez `yo azuresfcontainer:AddService`.</span><span class="sxs-lookup"><span data-stu-id="4304d-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="4304d-204">Configurer l’intervalle de temps d’attente avant l’arrêt forcé du conteneur</span><span class="sxs-lookup"><span data-stu-id="4304d-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="4304d-205">Vous pouvez configurer un intervalle de temps pour hello runtime toowait avant la suppression du conteneur de hello après que hello suppression du service (ou un nœud de tooanother move) a démarré.</span><span class="sxs-lookup"><span data-stu-id="4304d-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="4304d-206">Intervalle de temps hello configuration envoie hello `docker stop <time in seconds>` conteneur toohello de commande.</span><span class="sxs-lookup"><span data-stu-id="4304d-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="4304d-207">Pour plus d’informations, consultez [Arrêt du docker](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="4304d-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="4304d-208">toowait d’intervalle de temps Hello est spécifié sous hello `Hosting` section.</span><span class="sxs-lookup"><span data-stu-id="4304d-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="4304d-209">Hello suivant extrait de manifeste de cluster montre comment tooset hello délai d’attente :</span><span class="sxs-lookup"><span data-stu-id="4304d-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="4304d-210">Hello intervalle de temps par défaut a la valeur too10 secondes.</span><span class="sxs-lookup"><span data-stu-id="4304d-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="4304d-211">Étant donné que cette configuration est dynamique, une configuration uniquement mettre à niveau sur le délai d’attente de hello cluster mises à jour hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="4304d-212">Configurer hello runtime tooremove les images de conteneur inutilisé</span><span class="sxs-lookup"><span data-stu-id="4304d-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="4304d-213">Vous pouvez configurer tooremove de cluster Service Fabric hello des images de conteneur inutilisé à partir du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="4304d-214">Cette configuration permet de toobe d’espace disque rétabli si trop d’images de conteneur sont présents sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="4304d-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="4304d-215">tooenable cette fonctionnalité, la mise à jour hello `Hosting` section dans le manifeste du cluster hello, comme indiqué dans hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="4304d-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="4304d-216">Pour les images qui ne doivent pas être supprimés, vous pouvez les spécifier sous hello `ContainerImagesToSkip` paramètre.</span><span class="sxs-lookup"><span data-stu-id="4304d-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="4304d-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4304d-217">Next steps</span></span>
* <span data-ttu-id="4304d-218">En savoir plus sur l’exécution des [conteneurs sur Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4304d-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="4304d-219">Hello de lecture [déployer une application .NET dans un conteneur](service-fabric-host-app-in-a-container.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4304d-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="4304d-220">En savoir plus sur hello Service Fabric [cycle de vie des applications](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="4304d-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="4304d-221">Hello d’extraction [exemples de code de Service Fabric conteneur](https://github.com/Azure-Samples/service-fabric-dotnet-containers) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="4304d-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
