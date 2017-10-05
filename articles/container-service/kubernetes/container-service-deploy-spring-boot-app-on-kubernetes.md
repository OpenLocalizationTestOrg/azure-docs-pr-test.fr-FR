---
title: "Déployer une application Spring Boot sur Kubernetes dans Azure Container Service | Microsoft Docs"
description: "Ce didacticiel vous guidera à travers les étapes à suivre pour déployer une application Spring Boot dans un cluster Kubernetes sur Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 7f726436b2d459b8c16abb02e07de099abfd8974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="f84b1-103">Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f84b1-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="f84b1-104">Le **[Spring Framework]** est une infrastructure open source populaire qui aide les développeurs Java à créer des applications web, mobiles et API.</span><span class="sxs-lookup"><span data-stu-id="f84b1-104">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="f84b1-105">Ce didacticiel utilise un exemple d’application créé à l’aide de [Spring Boot], une approche orientée par une convention permettant de prendre en main et d’utiliser Spring rapidement.</span><span class="sxs-lookup"><span data-stu-id="f84b1-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="f84b1-106">**[Kubernetes]** et **[client Docker]** sont des solutions open source qui aident les développeurs à automatiser le déploiement, la mise à l’échelle et la gestion de leurs applications s’exécutant dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="f84b1-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="f84b1-107">Ce didacticiel vous guidera à travers le processus de combinaison de ces deux technologies open source populaires afin de développer et de déployer une application Spring Boot sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f84b1-107">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="f84b1-108">Plus précisément, vous utilisez *[Spring Boot]* pour le développement d’applications, *[Kubernetes]* pour le déploiement du conteneur, et [Azure Container Service (ACS)] pour l’hébergement votre application.</span><span class="sxs-lookup"><span data-stu-id="f84b1-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (ACS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f84b1-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f84b1-109">Prerequisites</span></span>

* <span data-ttu-id="f84b1-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="f84b1-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="f84b1-111">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="f84b1-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="f84b1-112">Un [JDK (Java Developer Kit)] à jour.</span><span class="sxs-lookup"><span data-stu-id="f84b1-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="f84b1-113">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="f84b1-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="f84b1-114">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="f84b1-114">A [Git] client.</span></span>
* <span data-ttu-id="f84b1-115">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="f84b1-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="f84b1-116">En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.</span><span class="sxs-lookup"><span data-stu-id="f84b1-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="f84b1-117">Créer l’application web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="f84b1-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="f84b1-118">Les étapes suivantes vous guident à travers la création d’une application web Spring Boot et vous aident à effectuer le test en local.</span><span class="sxs-lookup"><span data-stu-id="f84b1-118">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="f84b1-119">Ouvrez une invite de commandes et créez un répertoire local pour y stocker votre application, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f84b1-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="f84b1-120">- ou -</span><span class="sxs-lookup"><span data-stu-id="f84b1-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="f84b1-121">Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="f84b1-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="f84b1-122">Accédez au répertoire du projet terminé.</span><span class="sxs-lookup"><span data-stu-id="f84b1-122">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="f84b1-123">Utilisez Maven pour créer et exécuter l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="f84b1-123">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="f84b1-124">Testez l’application web en accédant à l’URL http://localhost:8080, ou avec la commande `curl` suivante :</span><span class="sxs-lookup"><span data-stu-id="f84b1-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="f84b1-125">Vous devez normalement voir le message suivant : **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="f84b1-125">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="f84b1-127">Créer un registre de conteneurs Azure à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f84b1-127">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="f84b1-128">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="f84b1-128">Open a command prompt.</span></span>

1. <span data-ttu-id="f84b1-129">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="f84b1-129">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="f84b1-130">Créer un groupe de ressources pour les ressources Azure utilisées dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f84b1-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="f84b1-131">Créez un registre de conteneurs Azure privé dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f84b1-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="f84b1-132">Au cours des dernières étapes, le didacticiel envoie au registre l’exemple d’application en tant qu’image Docker.</span><span class="sxs-lookup"><span data-stu-id="f84b1-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="f84b1-133">Remplacez `wingtiptoysregistry` par un nom unique pour votre registre.</span><span class="sxs-lookup"><span data-stu-id="f84b1-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="f84b1-134">Envoyer l’application dans le registre de conteneurs</span><span class="sxs-lookup"><span data-stu-id="f84b1-134">Push your app to the container registry</span></span>

1. <span data-ttu-id="f84b1-135">Accédez au répertoire de configuration de l’installation de Maven (par défaut sous ~/.m2/ ou C:\Users\username\.m2) et ouvrez le fichier *settings.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="f84b1-135">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="f84b1-136">Récupérez le mot de passe pour votre registre de conteneurs à partir de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="f84b1-136">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="f84b1-137">Ajoutez votre identifiant de registre de conteneurs Azure et votre mot de passe à une nouvelle collection `<server>` dans le fichier *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="f84b1-137">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="f84b1-138">Le `id` et `username` correspondent au nom du registre.</span><span class="sxs-lookup"><span data-stu-id="f84b1-138">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="f84b1-139">Utilisez la valeur `password` de la commande précédente (sans guillemets).</span><span class="sxs-lookup"><span data-stu-id="f84b1-139">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="f84b1-140">Accédez au répertoire de projet terminé de votre application Spring Boot (par exemple, « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="f84b1-140">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="f84b1-141">Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la valeur du serveur de connexion de votre registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="f84b1-141">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="f84b1-142">Mettez à jour la collection `<plugins>` dans le fichier *pom.xml* de manière que `<plugin>` contienne l’adresse du serveur de connexion et le nom de registre de votre registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="f84b1-142">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="f84b1-143">Pour créer le conteneur Docker et envoyer l’image dans le registre, accédez au répertoire de projet terminé de votre application Spring Boot et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f84b1-143">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="f84b1-144">Lorsque Maven envoie l’image vers Azure, vous pouvez recevoir un message d’erreur semblable au message suivant :</span><span class="sxs-lookup"><span data-stu-id="f84b1-144">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="f84b1-145">Si vous obtenez cette erreur, connectez-vous à Azure à partir de la ligne de commande Docker.</span><span class="sxs-lookup"><span data-stu-id="f84b1-145">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="f84b1-146">Envoyez ensuite votre conteneur :</span><span class="sxs-lookup"><span data-stu-id="f84b1-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-the-azure-cli"></a><span data-ttu-id="f84b1-147">Créer un cluster Kubernetes sur ACS à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f84b1-147">Create a Kubernetes Cluster on ACS using the Azure CLI</span></span>

1. <span data-ttu-id="f84b1-148">Créez un cluster Kubernetes dans Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="f84b1-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="f84b1-149">La commande suivante crée un cluster *kubernetes* dans le groupe de ressources *wingtiptoys-kubernetes*, avec *wingtiptoys-containerservice* comme nom du cluster et *wingtiptoys-kubernetes* comme préfixe du serveur DNS :</span><span class="sxs-lookup"><span data-stu-id="f84b1-149">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="f84b1-150">Cette commande peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="f84b1-150">This command may take a while to complete.</span></span>

1. <span data-ttu-id="f84b1-151">Installez `kubectl` à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="f84b1-151">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="f84b1-152">Les utilisateurs Linux doivent ajouter cette commande en préfixe sur `sudo` car elle déploie l’interface de ligne de commande Kubernetes dans `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="f84b1-152">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="f84b1-153">Téléchargez les informations de configuration du cluster afin de pouvoir gérer votre cluster à partir de l’interface web Kubernetes et de `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="f84b1-153">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="f84b1-154">Déployer l’image sur votre cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="f84b1-154">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="f84b1-155">Ce didacticiel déploie l’application à l’aide de `kubectl`, puis vous permet d’explorer le déploiement via l’interface web Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f84b1-155">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="f84b1-156">Déployer avec l’interface web de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="f84b1-156">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="f84b1-157">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="f84b1-157">Open a command prompt.</span></span>

1. <span data-ttu-id="f84b1-158">Ouvrez le site web de configuration de votre cluster Kubernetes dans votre navigateur par défaut :</span><span class="sxs-lookup"><span data-stu-id="f84b1-158">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="f84b1-159">Lorsque le site web de configuration Kubernetes s’ouvre dans votre navigateur, cliquez sur le lien afin de **déployer une application en conteneur** :</span><span class="sxs-lookup"><span data-stu-id="f84b1-159">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Site web de configuration Kubernetes][KB01]

1. <span data-ttu-id="f84b1-161">Lorsque la page **Déployer une application en conteneur** s’affiche, spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="f84b1-161">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="f84b1-162">a.</span><span class="sxs-lookup"><span data-stu-id="f84b1-162">a.</span></span> <span data-ttu-id="f84b1-163">Sélectionnez **Spécifier les détails de l’application ci-dessous**.</span><span class="sxs-lookup"><span data-stu-id="f84b1-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="f84b1-164">b.</span><span class="sxs-lookup"><span data-stu-id="f84b1-164">b.</span></span> <span data-ttu-id="f84b1-165">Entrez votre nom d’application Spring Boot comme **Nom de l’application**, par exemple : « *gs-spring-boot-docker* ».</span><span class="sxs-lookup"><span data-stu-id="f84b1-165">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="f84b1-166">c.</span><span class="sxs-lookup"><span data-stu-id="f84b1-166">c.</span></span> <span data-ttu-id="f84b1-167">Entrez votre serveur de connexion et votre conteneur d’image vus précédemment dans la catégorie **Conteneur d’image**, par exemple : « *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest* ».</span><span class="sxs-lookup"><span data-stu-id="f84b1-167">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="f84b1-168">d.</span><span class="sxs-lookup"><span data-stu-id="f84b1-168">d.</span></span> <span data-ttu-id="f84b1-169">Choisissez **Externe** pour le **Service**.</span><span class="sxs-lookup"><span data-stu-id="f84b1-169">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="f84b1-170">e.</span><span class="sxs-lookup"><span data-stu-id="f84b1-170">e.</span></span> <span data-ttu-id="f84b1-171">Spécifiez les ports internes et externes dans les zones de texte **Port** et **Port cible**.</span><span class="sxs-lookup"><span data-stu-id="f84b1-171">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Site web de configuration Kubernetes][KB02]


1. <span data-ttu-id="f84b1-173">Cliquez sur **Déployer** pour déployer le conteneur.</span><span class="sxs-lookup"><span data-stu-id="f84b1-173">Click **Deploy** to deploy the container.</span></span>

   ![Déployer le conteneur][KB05]

1. <span data-ttu-id="f84b1-175">Une fois que votre application a été déployée, vous verrez votre application Spring Boot répertoriée sous **Services**.</span><span class="sxs-lookup"><span data-stu-id="f84b1-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Services Kubernetes][KB06]

1. <span data-ttu-id="f84b1-177">Si vous cliquez sur le lien **Point de terminaison d’entrée**, vous pouvez voir votre application Spring Boot fonctionner sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f84b1-177">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Services Kubernetes][KB07]

   ![Parcourir l’exemple d’application sur Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="f84b1-180">Déployer avec kubectl</span><span class="sxs-lookup"><span data-stu-id="f84b1-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="f84b1-181">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="f84b1-181">Open a command prompt.</span></span>

1. <span data-ttu-id="f84b1-182">Exécutez votre conteneur dans le cluster Kubernetes en utilisant la commande `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="f84b1-182">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="f84b1-183">Donnez un nom de service à votre application dans Kubernetes et saisissez le nom complet de l’image.</span><span class="sxs-lookup"><span data-stu-id="f84b1-183">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="f84b1-184">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f84b1-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="f84b1-185">Dans cette commande :</span><span class="sxs-lookup"><span data-stu-id="f84b1-185">In this command:</span></span>

   * <span data-ttu-id="f84b1-186">Le nom du conteneur `gs-spring-boot-docker` est spécifié directement après la commande `run`.</span><span class="sxs-lookup"><span data-stu-id="f84b1-186">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="f84b1-187">Le paramètre `--image` spécifie le nom combiné du nom de serveur et du nom de l’image en tant que `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="f84b1-187">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="f84b1-188">Exposez votre cluster Kubernetes en externe à l’aide de la commande `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="f84b1-188">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="f84b1-189">Spécifiez le nom de votre service, le port TCP destiné au public permettant d’accéder à l’application, et le port cible interne que votre application écoutera.</span><span class="sxs-lookup"><span data-stu-id="f84b1-189">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="f84b1-190">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f84b1-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="f84b1-191">Dans cette commande :</span><span class="sxs-lookup"><span data-stu-id="f84b1-191">In this command:</span></span>

   * <span data-ttu-id="f84b1-192">Le nom du conteneur `gs-spring-boot-docker` est spécifié directement après la commande `expose deployment`.</span><span class="sxs-lookup"><span data-stu-id="f84b1-192">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="f84b1-193">Le paramètre `--type` spécifie que le cluster utilise l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="f84b1-193">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="f84b1-194">Le paramètre `--port` spécifie le port TCP 80 destiné au public.</span><span class="sxs-lookup"><span data-stu-id="f84b1-194">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="f84b1-195">Vous accédez à l’application sur ce port.</span><span class="sxs-lookup"><span data-stu-id="f84b1-195">You access the app on this port.</span></span>

   * <span data-ttu-id="f84b1-196">Le paramètre `--target-port` spécifie le port TCP interne 8080.</span><span class="sxs-lookup"><span data-stu-id="f84b1-196">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="f84b1-197">L’équilibreur de charge transmet les demandes à votre application sur ce port.</span><span class="sxs-lookup"><span data-stu-id="f84b1-197">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="f84b1-198">Une fois que l’application est déployée sur le cluster, faites la demande de l’adresse IP externe et ouvrez-la dans votre navigateur web :</span><span class="sxs-lookup"><span data-stu-id="f84b1-198">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Parcourir l’exemple d’application sur Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="f84b1-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f84b1-200">Next steps</span></span>

<span data-ttu-id="f84b1-201">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="f84b1-201">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="f84b1-202">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f84b1-202">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="f84b1-203">Déployer une application Spring Boot sur Linux dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f84b1-203">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="f84b1-204">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="f84b1-204">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="f84b1-205">Pour plus d’informations sur l’exemple de projet Spring Boot sur Docker, consultez [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="f84b1-205">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="f84b1-206">Les liens suivants fournissent des informations supplémentaires sur la création d’applications Spring Boot :</span><span class="sxs-lookup"><span data-stu-id="f84b1-206">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="f84b1-207">Pour plus d’informations sur la création d’une application Spring Boot simple, consultez Spring Initializr à l’adresse https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="f84b1-207">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="f84b1-208">Les liens suivants fournissent des informations supplémentaires sur l’utilisation de Kubernetes avec Azure :</span><span class="sxs-lookup"><span data-stu-id="f84b1-208">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="f84b1-209">Prise en main d’un cluster Kubernetes dans Container Service</span><span class="sxs-lookup"><span data-stu-id="f84b1-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="f84b1-210">Utilisation de l’interface utilisateur Web Kubernetes avec Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f84b1-210">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="f84b1-211">Plus d’informations sur l’utilisation de l’interface de ligne de commande Kubernetes sont disponibles dans le guide de l’utilisateur **kubectl** à l’adresse <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="f84b1-211">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="f84b1-212">Le site web Kubernetes comporte plusieurs articles traitant de l’utilisation d’images dans les registres privés :</span><span class="sxs-lookup"><span data-stu-id="f84b1-212">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="f84b1-213">[Configuration des comptes de service pour des pods]</span><span class="sxs-lookup"><span data-stu-id="f84b1-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="f84b1-214">[Espaces de noms]</span><span class="sxs-lookup"><span data-stu-id="f84b1-214">[Namespaces]</span></span>
* <span data-ttu-id="f84b1-215">[Extraction d’une image à partir d’un registre privé]</span><span class="sxs-lookup"><span data-stu-id="f84b1-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="f84b1-216">Pour obtenir des exemples supplémentaires sur l’utilisation d’images Docker personnalisées avec Azure, consultez [Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux].</span><span class="sxs-lookup"><span data-stu-id="f84b1-216">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="f84b1-217">[Azure CLI]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="f84b1-217">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="f84b1-218">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="f84b1-218">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="f84b1-219">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="f84b1-219">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
<span data-ttu-id="f84b1-220">[Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="f84b1-220">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="f84b1-221">[client Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="f84b1-221">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="f84b1-222">[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="f84b1-222">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="f84b1-223">[client Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="f84b1-223">[Git]: https://github.com/</span></span>
<span data-ttu-id="f84b1-224">[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="f84b1-224">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="f84b1-225">[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="f84b1-225">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="f84b1-226">[Kubernetes]: https://kubernetes.io/</span><span class="sxs-lookup"><span data-stu-id="f84b1-226">[Kubernetes]: https://kubernetes.io/</span></span>
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
<span data-ttu-id="f84b1-227">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="f84b1-227">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="f84b1-228">[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="f84b1-228">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="f84b1-229">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="f84b1-229">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="f84b1-230">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="f84b1-230">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="f84b1-231">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="f84b1-231">[Spring Framework]: https://spring.io/</span></span>
<span data-ttu-id="f84b1-232">[Configuration des comptes de service pour des pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span><span class="sxs-lookup"><span data-stu-id="f84b1-232">[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span></span>
<span data-ttu-id="f84b1-233">[Espaces de noms]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span><span class="sxs-lookup"><span data-stu-id="f84b1-233">[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span></span>
<span data-ttu-id="f84b1-234">[Extraction d’une image à partir d’un registre privé]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span><span class="sxs-lookup"><span data-stu-id="f84b1-234">[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span></span>

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
