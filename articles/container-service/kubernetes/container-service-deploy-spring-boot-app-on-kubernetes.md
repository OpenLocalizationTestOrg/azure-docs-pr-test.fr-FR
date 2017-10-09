---
title: "aaaDeploy une application de démarrage ressort sur Kubernetes dans le Service de conteneur Azure | Documents Microsoft"
description: "Ce didacticiel vous guidera cependant hello étapes toodeploy une application de démarrage du ressort dans un cluster Kubernetes sur Microsoft Azure."
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
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a><span data-ttu-id="9da6c-103">Déployer une Application de démarrage ressort sur un Kubernetes Cluster Bonjour Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="9da6c-103">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>

<span data-ttu-id="9da6c-104">Hello  **[Spring Framework]**  est une infrastructure open source populaire qui permet aux développeurs Java de créer des applications web, mobiles et API.</span><span class="sxs-lookup"><span data-stu-id="9da6c-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="9da6c-105">Ce didacticiel utilise un exemple d’application créé à l’aide de [ressort démarrage], une approche pilotée par convention pour l’utilisation du ressort tooget démarrer rapidement.</span><span class="sxs-lookup"><span data-stu-id="9da6c-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="9da6c-106">**[Kubernetes]**  et  **[client Docker]**  solutions en open source qui aident les développeurs sont automatiser hello déploiement, mise à l’échelle et la gestion de leurs applications en cours d’exécution dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="9da6c-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate hello deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="9da6c-107">Ce didacticiel vous guide si la combinaison de ces deux technologies populaires, open source de toodevelop et déployer un tooMicrosoft d’application de démarrage du ressort Azure.</span><span class="sxs-lookup"><span data-stu-id="9da6c-107">This tutorial walks you though combining these two popular, open-source technologies toodevelop and deploy a Spring Boot application tooMicrosoft Azure.</span></span> <span data-ttu-id="9da6c-108">Plus spécifiquement, vous utilisez  *[ressort démarrage]*  pour le développement d’applications,  *[Kubernetes]*  pour le déploiement de conteneur et hello [Conteneur de Service (ACS) de azure] toohost votre application.</span><span class="sxs-lookup"><span data-stu-id="9da6c-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and hello [Azure Container Service (ACS)] toohost your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9da6c-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9da6c-109">Prerequisites</span></span>

* <span data-ttu-id="9da6c-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="9da6c-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9da6c-111">Hello [Azure Interface de ligne de commande (CLI)].</span><span class="sxs-lookup"><span data-stu-id="9da6c-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="9da6c-112">Un [JDK (Java Developer Kit)] à jour.</span><span class="sxs-lookup"><span data-stu-id="9da6c-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="9da6c-113">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="9da6c-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="9da6c-114">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="9da6c-114">A [Git] client.</span></span>
* <span data-ttu-id="9da6c-115">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="9da6c-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9da6c-116">En raison des exigences de la virtualisation toohello de ce didacticiel, vous ne peut pas suivre les étapes de hello dans cet article sur un ordinateur virtuel ; Vous devez utiliser un ordinateur physique avec les fonctionnalités de virtualisation activées.</span><span class="sxs-lookup"><span data-stu-id="9da6c-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="9da6c-117">Créer hello ressort démarrage sur Docker prise en main d’application web</span><span class="sxs-lookup"><span data-stu-id="9da6c-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="9da6c-118">Hello suit vous guide dans la création d’une application web de démarrage du ressort et le tester localement.</span><span class="sxs-lookup"><span data-stu-id="9da6c-118">hello following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="9da6c-119">Ouvrez une invite de commandes et créer un répertoire local de toohold votre application, puis accédez au répertoire toothat ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="9da6c-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="9da6c-120">- ou -</span><span class="sxs-lookup"><span data-stu-id="9da6c-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="9da6c-121">Hello du clone [démarrage ressort sur Docker mise en route] exemple de projet dans l’annuaire de hello.</span><span class="sxs-lookup"><span data-stu-id="9da6c-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="9da6c-122">Changer le projet Active toohello s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="9da6c-122">Change directory toohello completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="9da6c-123">Utilisez Maven toobuild et exécution hello, exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="9da6c-123">Use Maven toobuild and run hello sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="9da6c-124">Application web, test hello en parcourant toohttp://localhost:8080 ou avec les éléments suivants de hello `curl` commande :</span><span class="sxs-lookup"><span data-stu-id="9da6c-124">Test hello web app by browsing toohttp://localhost:8080, or with hello following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="9da6c-125">Vous devez voir hello message suivant s’affiche : **Hello World de Docker**</span><span class="sxs-lookup"><span data-stu-id="9da6c-125">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="9da6c-127">Créer un Registre de conteneur Azure à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="9da6c-127">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="9da6c-128">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="9da6c-128">Open a command prompt.</span></span>

1. <span data-ttu-id="9da6c-129">Ouvrez une session dans tooyour compte Azure :</span><span class="sxs-lookup"><span data-stu-id="9da6c-129">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="9da6c-130">Créer un groupe de ressources pour hello ressources Azure utilisés dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9da6c-130">Create a resource group for hello Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="9da6c-131">Créer un Registre de conteneur Azure privée dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="9da6c-131">Create a private Azure container registry in hello resource group.</span></span> <span data-ttu-id="9da6c-132">didacticiel de Hello transmet hello, exemple d’application en tant que Docker image toothis Registre dans les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="9da6c-132">hello tutorial pushes hello sample app as a Docker image toothis registry in later steps.</span></span> <span data-ttu-id="9da6c-133">Remplacez `wingtiptoysregistry` par un nom unique pour votre registre.</span><span class="sxs-lookup"><span data-stu-id="9da6c-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a><span data-ttu-id="9da6c-134">Push de votre Registre de conteneur d’application toohello</span><span class="sxs-lookup"><span data-stu-id="9da6c-134">Push your app toohello container registry</span></span>

1. <span data-ttu-id="9da6c-135">Parcourir le répertoire de configuration toohello pour votre installation Maven (valeur par défaut ~/.m2/ ou C:\Users\username\.m2) et ouvrez hello *settings.xml* fichier avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="9da6c-135">Navigate toohello configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="9da6c-136">Récupérer un mot de passe hello pour votre Registre de conteneur de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="9da6c-136">Retrieve hello password for your container registry from hello Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="9da6c-137">Ajouter votre tooa Registre de conteneur Azure id et mot de passe nouveau `<server>` collection Bonjour *settings.xml* fichier.</span><span class="sxs-lookup"><span data-stu-id="9da6c-137">Add your Azure Container Registry id and password tooa new `<server>` collection in hello *settings.xml* file.</span></span>
<span data-ttu-id="9da6c-138">Hello `id` et `username` sont nom hello du Registre de hello.</span><span class="sxs-lookup"><span data-stu-id="9da6c-138">hello `id` and `username` are hello name of hello registry.</span></span> <span data-ttu-id="9da6c-139">Hello d’utilisation `password` valeur à partir de la commande précédente hello (sans guillemets).</span><span class="sxs-lookup"><span data-stu-id="9da6c-139">Use hello `password` value from hello previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="9da6c-140">Accédez répertoire du projet pour votre application de démarrage du ressort toohello terminée (par exemple, «*C:\SpringBoot\gs-spring-boot-docker\complete*« ou »*/users/robert/SpringBoot/gs-spring-boot-docker / complète*») et ouvrez hello *pom.xml* fichier avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="9da6c-140">Navigate toohello completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="9da6c-141">Hello de mise à jour `<properties>` collection Bonjour *pom.xml* fichier avec la valeur hello du serveur de connexion pour votre Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="9da6c-141">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="9da6c-142">Hello de mise à jour `<plugins>` collection Bonjour *pom.xml* de fichiers afin que hello `<plugin>` contient hello adresse et du Registre nom du serveur pour votre Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="9da6c-142">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="9da6c-143">Accédez répertoire du projet pour votre application de démarrage du ressort toohello s’est terminée et exécutez les hello suivant commande toobuild hello Docker conteneur et push hello image toohello du Registre :</span><span class="sxs-lookup"><span data-stu-id="9da6c-143">Navigate toohello completed project directory for your Spring Boot application and run hello following command toobuild hello Docker container and push hello image toohello registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="9da6c-144">Vous pouvez recevoir un message d’erreur est similaire tooone suivants de hello lorsque Maven pousse hello image tooAzure :</span><span class="sxs-lookup"><span data-stu-id="9da6c-144">You may receive an error message that is similar tooone of hello following when Maven pushes hello image tooAzure:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="9da6c-145">Si vous obtenez cette erreur, ouvrez une session dans tooAzure à partir de la ligne de commande Docker hello.</span><span class="sxs-lookup"><span data-stu-id="9da6c-145">If you get this error, log in tooAzure from hello Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="9da6c-146">Envoyez ensuite votre conteneur :</span><span class="sxs-lookup"><span data-stu-id="9da6c-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a><span data-ttu-id="9da6c-147">Créer un Cluster de Kubernetes sur ACS à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="9da6c-147">Create a Kubernetes Cluster on ACS using hello Azure CLI</span></span>

1. <span data-ttu-id="9da6c-148">Créez un cluster Kubernetes dans Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="9da6c-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="9da6c-149">Hello de commande suivant crée un *kubernetes* cluster Bonjour *wingtiptoys-kubernetes* ressource groupe avec *wingtiptoys-containerservice* en tant que cluster de hello nom, et *wingtiptoys-kubernetes* en tant que préfixe DNS hello :</span><span class="sxs-lookup"><span data-stu-id="9da6c-149">hello following command creates a *kubernetes* cluster in hello *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as hello cluster name, and *wingtiptoys-kubernetes* as hello DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="9da6c-150">Cette commande peut prendre un certain temps toocomplete.</span><span class="sxs-lookup"><span data-stu-id="9da6c-150">This command may take a while toocomplete.</span></span>

1. <span data-ttu-id="9da6c-151">Installer `kubectl` à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="9da6c-151">Install `kubectl` using hello Azure CLI.</span></span> <span data-ttu-id="9da6c-152">Les utilisateurs Linux peuvent avoir tooprefix cette commande avec `sudo` , car il déploie hello Kubernetes CLI trop`/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="9da6c-152">Linux users may have tooprefix this command with `sudo` since it deploys hello Kubernetes CLI too`/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="9da6c-153">Télécharger les informations de configuration de cluster hello vous pouvez de gérer votre cluster à partir de l’interface web hello Kubernetes et `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="9da6c-153">Download hello cluster configuration information so you can manage your cluster from hello Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a><span data-ttu-id="9da6c-154">Déployer hello image tooyour Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="9da6c-154">Deploy hello image tooyour Kubernetes cluster</span></span>

<span data-ttu-id="9da6c-155">Ce didacticiel déploie à l’aide d’application hello `kubectl`, puis vous autoriser le déploiement de hello tooexplore via l’interface web hello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="9da6c-155">This tutorial deploys hello app using `kubectl`, then allow you tooexplore hello deployment through hello Kubernetes web interface.</span></span>

### <a name="deploy-with-hello-kubernetes-web-interface"></a><span data-ttu-id="9da6c-156">Déployer avec l’interface web hello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="9da6c-156">Deploy with hello Kubernetes web interface</span></span>

1. <span data-ttu-id="9da6c-157">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="9da6c-157">Open a command prompt.</span></span>

1. <span data-ttu-id="9da6c-158">Ouvrez le site Web de configuration hello pour votre cluster Kubernetes dans votre navigateur par défaut :</span><span class="sxs-lookup"><span data-stu-id="9da6c-158">Open hello configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="9da6c-159">Lorsque le site Web de configuration hello Kubernetes s’ouvre dans votre navigateur, cliquez sur le lien de hello trop**déployer une application en conteneur**:</span><span class="sxs-lookup"><span data-stu-id="9da6c-159">When hello Kubernetes configuration website opens in your browser, click hello link too**deploy a containerized app**:</span></span>

   ![Site web de configuration Kubernetes][KB01]

1. <span data-ttu-id="9da6c-161">Hello lorsque **déployer une application en conteneur** page s’affiche, spécifiez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="9da6c-161">When hello **Deploy a containerized app** page is displayed, specify hello following options:</span></span>

   <span data-ttu-id="9da6c-162">a.</span><span class="sxs-lookup"><span data-stu-id="9da6c-162">a.</span></span> <span data-ttu-id="9da6c-163">Sélectionnez **Spécifier les détails de l’application ci-dessous**.</span><span class="sxs-lookup"><span data-stu-id="9da6c-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="9da6c-164">b.</span><span class="sxs-lookup"><span data-stu-id="9da6c-164">b.</span></span> <span data-ttu-id="9da6c-165">Entrez votre nom d’application de démarrage du ressort pour hello **nom de l’application**; par exemple : «*gs-spring-démarrage-docker*».</span><span class="sxs-lookup"><span data-stu-id="9da6c-165">Enter your Spring Boot application name for hello **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="9da6c-166">c.</span><span class="sxs-lookup"><span data-stu-id="9da6c-166">c.</span></span> <span data-ttu-id="9da6c-167">Entrez votre image de conteneur et du serveur de connexion à partir de précédemment pour hello **image de conteneur**; par exemple : «*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*».</span><span class="sxs-lookup"><span data-stu-id="9da6c-167">Enter your login server and container image from earlier for hello **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="9da6c-168">d.</span><span class="sxs-lookup"><span data-stu-id="9da6c-168">d.</span></span> <span data-ttu-id="9da6c-169">Choisissez **externe** pour hello **Service**.</span><span class="sxs-lookup"><span data-stu-id="9da6c-169">Choose **External** for hello **Service**.</span></span>

   <span data-ttu-id="9da6c-170">e.</span><span class="sxs-lookup"><span data-stu-id="9da6c-170">e.</span></span> <span data-ttu-id="9da6c-171">Spécifiez les ports internes et externes dans hello **Port** et **cible port** zones de texte.</span><span class="sxs-lookup"><span data-stu-id="9da6c-171">Specify your external and internal ports in hello **Port** and **Target port** text boxes.</span></span>

   ![Site web de configuration Kubernetes][KB02]


1. <span data-ttu-id="9da6c-173">Cliquez sur **déployer** conteneur de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9da6c-173">Click **Deploy** toodeploy hello container.</span></span>

   ![Déployer le conteneur][KB05]

1. <span data-ttu-id="9da6c-175">Une fois que votre application a été déployée, vous verrez votre application Spring Boot répertoriée sous **Services**.</span><span class="sxs-lookup"><span data-stu-id="9da6c-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Services Kubernetes][KB06]

1. <span data-ttu-id="9da6c-177">Si vous cliquez sur le lien hello pour **points de terminaison externes**, vous pouvez voir votre application ressort démarrage en cours d’exécution sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9da6c-177">If you click hello link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Services Kubernetes][KB07]

   ![Parcourir l’exemple d’application sur Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="9da6c-180">Déployer avec kubectl</span><span class="sxs-lookup"><span data-stu-id="9da6c-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="9da6c-181">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="9da6c-181">Open a command prompt.</span></span>

1. <span data-ttu-id="9da6c-182">Exécuter votre conteneur dans le cluster de Kubernetes hello à l’aide de hello `kubectl run` commande.</span><span class="sxs-lookup"><span data-stu-id="9da6c-182">Run your container in hello Kubernetes cluster by using hello `kubectl run` command.</span></span> <span data-ttu-id="9da6c-183">Donnez un nom de service pour votre application dans Kubernetes et le nom de l’image complète hello.</span><span class="sxs-lookup"><span data-stu-id="9da6c-183">Give a service name for your app in Kubernetes and hello full image name.</span></span> <span data-ttu-id="9da6c-184">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9da6c-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="9da6c-185">Dans cette commande :</span><span class="sxs-lookup"><span data-stu-id="9da6c-185">In this command:</span></span>

   * <span data-ttu-id="9da6c-186">nom du conteneur Hello `gs-spring-boot-docker` est spécifié immédiatement après hello `run` commande</span><span class="sxs-lookup"><span data-stu-id="9da6c-186">hello container name `gs-spring-boot-docker` is specified immediately after hello `run` command</span></span>

   * <span data-ttu-id="9da6c-187">Hello `--image` paramètre spécifie hello combinées de serveur de connexion et le nom de l’image en tant que`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="9da6c-187">hello `--image` parameter specifies hello combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="9da6c-188">Exposer votre cluster Kubernetes en externe à l’aide de hello `kubectl expose` commande.</span><span class="sxs-lookup"><span data-stu-id="9da6c-188">Expose your Kubernetes cluster externally by using hello `kubectl expose` command.</span></span> <span data-ttu-id="9da6c-189">Spécifiez le nom de votre service, hello publique TCP port utilisé tooaccess hello application et le port de cible interne hello écouté par votre application.</span><span class="sxs-lookup"><span data-stu-id="9da6c-189">Specify your service name, hello public-facing TCP port used tooaccess hello app, and hello internal target port your app listens on.</span></span> <span data-ttu-id="9da6c-190">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9da6c-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="9da6c-191">Dans cette commande :</span><span class="sxs-lookup"><span data-stu-id="9da6c-191">In this command:</span></span>

   * <span data-ttu-id="9da6c-192">nom du conteneur Hello `gs-spring-boot-docker` est spécifié immédiatement après hello `expose deployment` commande</span><span class="sxs-lookup"><span data-stu-id="9da6c-192">hello container name `gs-spring-boot-docker` is specified immediately after hello `expose deployment` command</span></span>

   * <span data-ttu-id="9da6c-193">Hello `--type` paramètre spécifie que le cluster hello utilise l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="9da6c-193">hello `--type` parameter specifies that hello cluster uses load balancer</span></span>

   * <span data-ttu-id="9da6c-194">Hello `--port` paramètre spécifie le port TCP 80 hello publics.</span><span class="sxs-lookup"><span data-stu-id="9da6c-194">hello `--port` parameter specifies hello public-facing TCP port of 80.</span></span> <span data-ttu-id="9da6c-195">Vous accéder à application hello sur ce port.</span><span class="sxs-lookup"><span data-stu-id="9da6c-195">You access hello app on this port.</span></span>

   * <span data-ttu-id="9da6c-196">Hello `--target-port` paramètre spécifie hello interne le port TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="9da6c-196">hello `--target-port` parameter specifies hello internal TCP port of 8080.</span></span> <span data-ttu-id="9da6c-197">équilibrage de charge Hello transfère application tooyour de demandes sur ce port.</span><span class="sxs-lookup"><span data-stu-id="9da6c-197">hello load balancer forwards requests tooyour app on this port.</span></span>

1. <span data-ttu-id="9da6c-198">Une fois que l’application hello est déployée toohello cluster, une adresse IP externe hello de requête et l’ouvrir dans votre navigateur web :</span><span class="sxs-lookup"><span data-stu-id="9da6c-198">Once hello app is deployed toohello cluster, query hello external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Parcourir l’exemple d’application sur Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="9da6c-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9da6c-200">Next steps</span></span>

<span data-ttu-id="9da6c-201">Pour plus d’informations sur l’utilisation de démarrage du ressort sur Azure, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="9da6c-201">For more information about using Spring Boot on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="9da6c-202">Déployer un toohello ressort démarrage Application Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9da6c-202">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="9da6c-203">Déployer une application de démarrage du ressort sur Linux Bonjour Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="9da6c-203">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="9da6c-204">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="9da6c-204">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="9da6c-205">Pour plus d’informations sur hello ressort démarrage sur l’exemple de projet Docker, consultez [démarrage ressort sur Docker mise en route].</span><span class="sxs-lookup"><span data-stu-id="9da6c-205">For more information about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="9da6c-206">Hello suivant liens fournit des informations supplémentaires sur la création d’applications de démarrage du ressort :</span><span class="sxs-lookup"><span data-stu-id="9da6c-206">hello following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="9da6c-207">Pour plus d’informations sur la création d’une application de démarrage du ressort simple, consultez hello ressort Initializr à https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="9da6c-207">For more information about creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="9da6c-208">Hello liens suivants fournissent des informations supplémentaires sur l’utilisation de Kubernetes avec Azure :</span><span class="sxs-lookup"><span data-stu-id="9da6c-208">hello following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="9da6c-209">Prise en main d’un cluster Kubernetes dans Container Service</span><span class="sxs-lookup"><span data-stu-id="9da6c-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="9da6c-210">À l’aide de hello Kubernetes web l’interface utilisateur avec le Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="9da6c-210">Using hello Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="9da6c-211">Plus d’informations sur l’utilisation d’une interface de ligne Kubernetes est disponible dans hello **kubectl** guide de l’utilisateur à <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="9da6c-211">More information about using Kubernetes command-line interface is available in hello **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="9da6c-212">site Web de Kubernetes Hello comporte plusieurs articles qui traitent de l’utilisation d’images dans les registres privés :</span><span class="sxs-lookup"><span data-stu-id="9da6c-212">hello Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="9da6c-213">[Configuration des comptes de service pour des pods]</span><span class="sxs-lookup"><span data-stu-id="9da6c-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="9da6c-214">[Espaces de noms]</span><span class="sxs-lookup"><span data-stu-id="9da6c-214">[Namespaces]</span></span>
* <span data-ttu-id="9da6c-215">[Extraction d’une image à partir d’un registre privé]</span><span class="sxs-lookup"><span data-stu-id="9da6c-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="9da6c-216">Pour obtenir des exemples supplémentaires pour comment toouse personnalisé Docker images avec Azure, consultez [à l’aide d’une image Docker personnalisée pour l’application Web Azure sous Linux].</span><span class="sxs-lookup"><span data-stu-id="9da6c-216">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure Interface de ligne de commande (CLI)]: /cli/azure/overview
[Conteneur de Service (ACS) de azure]: https://azure.microsoft.com/services/container-service/
[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[à l’aide d’une image Docker personnalisée pour l’application Web Azure sous Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[client Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[ressort démarrage]: http://projects.spring.io/spring-boot/
[démarrage ressort sur Docker mise en route]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configuration des comptes de service pour des pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Espaces de noms]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Extraction d’une image à partir d’un registre privé]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

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
