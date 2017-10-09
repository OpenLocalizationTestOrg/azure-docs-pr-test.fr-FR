---
title: "aaaDeploy une application de Web démarrage ressort sur Linux dans le Service de conteneur Azure | Documents Microsoft"
description: "Ce didacticiel vous guide cependant hello étapes toodeploy une application de démarrage du ressort comme une application web de Linux sur Microsoft Azure."
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
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a><span data-ttu-id="170eb-103">Déployer une application de démarrage du ressort sur Linux Bonjour Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="170eb-103">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>

<span data-ttu-id="170eb-104">Hello  **[Spring Framework]**  est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="170eb-104">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="170eb-105">Un des projets plus-populaires hello qui est créé de plateforme est [ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="170eb-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="170eb-106">**[client Docker]**  solutions en open source qui permet aux développeurs d’automatiser hello déploiement, mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="170eb-106">**[Docker]** is open-source solutions that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="170eb-107">Ce didacticiel vous guide à l’aide de Docker toodevelop et déployer un hôte Linux de démarrage du ressort application tooa Bonjour [Azure conteneur de Service (ACS)].</span><span class="sxs-lookup"><span data-stu-id="170eb-107">This tutorial walks you through using Docker toodevelop and deploy a Spring Boot application tooa Linux host in hello [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="170eb-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="170eb-108">Prerequisites</span></span>

<span data-ttu-id="170eb-109">Commande toocomplete hello étapes décrites dans ce didacticiel, vous devez hello toohave suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="170eb-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="170eb-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="170eb-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="170eb-111">Hello [Azure Interface de ligne de commande (CLI)].</span><span class="sxs-lookup"><span data-stu-id="170eb-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="170eb-112">Un [JDK (Java Developer Kit)] à jour.</span><span class="sxs-lookup"><span data-stu-id="170eb-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="170eb-113">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="170eb-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="170eb-114">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="170eb-114">A [Git] client.</span></span>
* <span data-ttu-id="170eb-115">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="170eb-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="170eb-116">En raison des exigences de la virtualisation toohello de ce didacticiel, vous ne peut pas suivre les étapes de hello dans cet article sur un ordinateur virtuel ; Vous devez utiliser un ordinateur physique avec les fonctionnalités de virtualisation activées.</span><span class="sxs-lookup"><span data-stu-id="170eb-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="170eb-117">Créer hello ressort démarrage sur Docker prise en main d’application web</span><span class="sxs-lookup"><span data-stu-id="170eb-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="170eb-118">Hello étapes suivantes vous guident étapes hello toocreate requis une application web de démarrage du ressort simple et de le tester localement.</span><span class="sxs-lookup"><span data-stu-id="170eb-118">hello following steps walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="170eb-119">Ouvrez une invite de commandes et créer un répertoire local de toohold votre application, puis accédez au répertoire toothat ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="170eb-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="170eb-120">- ou -</span><span class="sxs-lookup"><span data-stu-id="170eb-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="170eb-121">Hello du clone [démarrage ressort sur Docker mise en route] exemple de projet dans le répertoire hello créé ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="170eb-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="170eb-122">Changer le projet toohello terminée Active ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="170eb-122">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="170eb-123">Générer le fichier JAR hello à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="170eb-123">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="170eb-124">Une fois que l’application hello web a été créée, modifier le répertoire toohello `target` répertoire dans lequel le fichier JAR hello se trouve et démarrer l’application web hello ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="170eb-124">Once hello web app has been created, change directory toohello `target` directory where hello JAR file is located and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="170eb-125">Tester l’application web hello en parcourant tooit localement à l’aide d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="170eb-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="170eb-126">Par exemple, si vous avez curl disponible et vous configuré hello Tomcat server toorun sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="170eb-126">For example, if you have curl available and you configured hello Tomcat server toorun on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="170eb-127">Vous devez voir hello message suivant s’affiche : **Docker de Hello World !**</span><span class="sxs-lookup"><span data-stu-id="170eb-127">You should see hello following message displayed: **Hello Docker World!**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a><span data-ttu-id="170eb-129">Créer un toouse de Registre de conteneur Azure comme un Registre Docker privé</span><span class="sxs-lookup"><span data-stu-id="170eb-129">Create an Azure Container Registry toouse as a Private Docker Registry</span></span>

<span data-ttu-id="170eb-130">Hello étapes suivantes vous guident à l’aide de hello toocreate portail Azure un Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="170eb-130">hello following steps walk you through using hello Azure portal toocreate an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="170eb-131">Si vous souhaitez toouse hello CLI d’Azure au lieu de hello portail Azure, suivez les étapes de hello dans [créer un Registre de conteneur Docker privé à l’aide de hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="170eb-131">If you want toouse hello Azure CLI instead of hello Azure portal, follow hello steps in [Create a private Docker container registry using hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="170eb-132">Parcourir toohello [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="170eb-132">Browse toohello [Azure portal] and sign in.</span></span>

   <span data-ttu-id="170eb-133">Une fois que vous avez connecté compte tooyour sur hello portail Azure, vous pouvez suivre les étapes de hello Bonjour [créer un Registre de conteneur Docker privé à l’aide de hello portail Azure] article, qui sont paraphrase Bonjour comme suit pour hello exploration d’opportunité.</span><span class="sxs-lookup"><span data-stu-id="170eb-133">Once you have signed in tooyour account on hello Azure portal, you can follow hello steps in hello [Create a private Docker container registry using hello Azure portal] article, which are paraphrased in hello following steps for hello sake of expediency.</span></span>

1. <span data-ttu-id="170eb-134">Cliquez sur icône du menu hello pour **+ nouveau**, puis cliquez sur **conteneurs**, puis cliquez sur **Registre de conteneur Azure**.</span><span class="sxs-lookup"><span data-stu-id="170eb-134">Click hello menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Créer un registre de conteneurs Azure][AR01]

1. <span data-ttu-id="170eb-136">Lorsque la page d’informations hello pour le modèle de Registre de conteneur Azure hello s’affiche, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="170eb-136">When hello information page for hello Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Créer un registre de conteneurs Azure][AR02]

1. <span data-ttu-id="170eb-138">Hello lorsque **Registre de conteneur créer** page s’affiche, entrez votre **nom de Registre** et **groupe de ressources**, choisissez **activer** pour Hello **utilisateur Admin**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="170eb-138">When hello **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for hello **Admin user**, and then click **Create**.</span></span>

   ![Configurer les paramètres du registre de conteneurs Azure][AR03]

1. <span data-ttu-id="170eb-140">Une fois votre Registre de conteneur a été créé, accédez de Registre de conteneur tooyour Bonjour portail Azure, puis cliquez sur **clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="170eb-140">Once your container registry has been created, navigate tooyour container registry in hello Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="170eb-141">Prenez note du nom d’utilisateur hello et un mot de passe pour les étapes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="170eb-141">Take note of hello username and password for hello next steps.</span></span>

   ![Clés d’accès du registre de conteneurs Azure][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a><span data-ttu-id="170eb-143">Configurer Maven toouse vos clés d’accès de Registre de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="170eb-143">Configure Maven toouse your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="170eb-144">Parcourir le répertoire de configuration toohello pour votre installation Maven et ouvrez hello *settings.xml* fichier avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="170eb-144">Navigate toohello configuration directory for your Maven installation and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="170eb-145">Ajouter des paramètres du Registre de conteneur Azure d’accès à partir de la section précédente de hello de ce didacticiel toohello `<servers>` collection Bonjour *settings.xml* fichier ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="170eb-145">Add your Azure Container Registry access settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="170eb-146">Accédez répertoire du projet pour votre application de démarrage du ressort, toohello terminée (par exemple : «*C:\SpringBoot\gs-spring-boot-docker\complete*« ou »*/users/robert/SpringBoot/gs-spring-boot-docker / complète*») et ouvrez hello *pom.xml* fichier avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="170eb-146">Navigate toohello completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="170eb-147">Hello de mise à jour `<properties>` collection Bonjour *pom.xml* fichier avec la valeur hello du serveur de connexion pour votre Registre de conteneur Azure à partir de la section précédente de hello de ce didacticiel ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="170eb-147">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="170eb-148">Hello de mise à jour `<plugins>` collection Bonjour *pom.xml* de fichiers afin que hello `<plugin>` contient hello adresse et du Registre nom du serveur pour votre Registre de conteneur Azure à partir de la section précédente de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="170eb-148">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry from hello previous section of this tutorial.</span></span> <span data-ttu-id="170eb-149">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="170eb-149">For example:</span></span>

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

1. <span data-ttu-id="170eb-150">Accédez répertoire du projet pour votre application de démarrage du ressort toohello s’est terminée et exécutez hello après application de commande toorebuild hello push hello conteneur tooyour Registre de conteneur Azure :</span><span class="sxs-lookup"><span data-stu-id="170eb-150">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="170eb-151">Lorsque vous transmettez vos tooAzure de conteneur Docker, vous pouvez recevoir un message d’erreur est similaire tooone de hello suivant même si votre conteneur Docker a été créé avec succès :</span><span class="sxs-lookup"><span data-stu-id="170eb-151">When you are pushing your Docker container tooAzure, you may receive an error message that is similar tooone of hello following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="170eb-152">Dans ce cas, vous devrez peut-être toosign dans tooyour compte Azure à partir de la ligne de commande Docker hello ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="170eb-152">If this happens, you may need toosign in tooyour Azure account from hello Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="170eb-153">Vous pouvez ensuite distribuer votre conteneur à partir de la ligne de commande hello ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="170eb-153">You can then push your container from hello command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="170eb-154">Créer une application web sur Linux sur Azure App Service en utilisant votre image de conteneur</span><span class="sxs-lookup"><span data-stu-id="170eb-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="170eb-155">Parcourir toohello [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="170eb-155">Browse toohello [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="170eb-156">Cliquez sur icône du menu hello pour **+ nouveau**, puis cliquez sur **Web + Mobile**, puis cliquez sur **l’application Web sur Linux**.</span><span class="sxs-lookup"><span data-stu-id="170eb-156">Click hello menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Créer une application web Bonjour portail Azure][LX01]

1. <span data-ttu-id="170eb-158">Hello lorsque **l’application Web sur Linux** page s’affiche, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="170eb-158">When hello **Web App on Linux** page is displayed, enter hello following information:</span></span>

   <span data-ttu-id="170eb-159">a.</span><span class="sxs-lookup"><span data-stu-id="170eb-159">a.</span></span> <span data-ttu-id="170eb-160">Entrez un nom unique pour hello **nom de l’application**; par exemple : «*wingtiptoyslinux*. »</span><span class="sxs-lookup"><span data-stu-id="170eb-160">Enter a unique name for hello **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="170eb-161">b.</span><span class="sxs-lookup"><span data-stu-id="170eb-161">b.</span></span> <span data-ttu-id="170eb-162">Choisissez votre **abonnement** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="170eb-162">Choose your **Subscription** from hello drop-down list.</span></span>

   <span data-ttu-id="170eb-163">c.</span><span class="sxs-lookup"><span data-stu-id="170eb-163">c.</span></span> <span data-ttu-id="170eb-164">Sélectionnez un existant **groupe de ressources**, ou spécifiez un nom de toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="170eb-164">Choose an existing **Resource Group**, or specify a name toocreate a new resource group.</span></span>

   <span data-ttu-id="170eb-165">d.</span><span class="sxs-lookup"><span data-stu-id="170eb-165">d.</span></span> <span data-ttu-id="170eb-166">Cliquez sur **configurer conteneur** et entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="170eb-166">Click **Configure container** and enter hello following information:</span></span>

      * <span data-ttu-id="170eb-167">Choisissez **Registre privé**.</span><span class="sxs-lookup"><span data-stu-id="170eb-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="170eb-168">**Image et étiquette facultative** : spécifiez le nom de votre conteneur utilisé plus haut, par exemple : « *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest* »</span><span class="sxs-lookup"><span data-stu-id="170eb-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="170eb-169">**URL du serveur**: spécifiez l’URL du registre déclaré plus haut, par exemple : « *https://wingtiptoysregistry.azurecr.io* »</span><span class="sxs-lookup"><span data-stu-id="170eb-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="170eb-170">**Nom d’utilisateur de connexion** et **Mot de passe** : spécifiez vos informations d’identification de connexion des **clés d’accès** que vous avez utilisées dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="170eb-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="170eb-171">e.</span><span class="sxs-lookup"><span data-stu-id="170eb-171">e.</span></span> <span data-ttu-id="170eb-172">Une fois que vous avez entré toutes hello au-dessus des informations, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="170eb-172">Once you have entered all of hello above information, click **OK**.</span></span>

   ![Configurer les paramètres de l’application web][LX02]

1. <span data-ttu-id="170eb-174">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="170eb-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="170eb-175">Azure mappera automatiquement serveur Internet demandes tooembedded Tomcat qui s’exécute sur des ports standard hello de 80 ou 8080.</span><span class="sxs-lookup"><span data-stu-id="170eb-175">Azure will automatically map Internet requests tooembedded Tomcat server that is running on hello standard ports of 80 or 8080.</span></span> <span data-ttu-id="170eb-176">Toutefois, si vous avez configuré votre toorun du serveur Tomcat incorporée sur un port personnalisé, vous devez tooadd une application web de variable tooyour environnement qui définit le port hello pour votre serveur Tomcat incorporé.</span><span class="sxs-lookup"><span data-stu-id="170eb-176">However, if you configured your embedded Tomcat server toorun on a custom port, you need tooadd an environment variable tooyour web app that defines hello port for your embedded Tomcat server.</span></span> <span data-ttu-id="170eb-177">toodo utilisez donc hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="170eb-177">toodo so, use hello following steps:</span></span>
>
> 1. <span data-ttu-id="170eb-178">Parcourir toohello [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="170eb-178">Browse toohello [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="170eb-179">Cliquez sur icône hello **des Services d’application**.</span><span class="sxs-lookup"><span data-stu-id="170eb-179">Click hello icon for **App Services**.</span></span> <span data-ttu-id="170eb-180">(Consultez l’article #1 dans l’image hello ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="170eb-180">(See item #1 in hello image below.)</span></span>
>
> 3. <span data-ttu-id="170eb-181">Sélectionnez votre application web à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="170eb-181">Select your web app from hello list.</span></span> <span data-ttu-id="170eb-182">(Élément #2 dans l’image hello ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="170eb-182">(Item #2 in hello image below.)</span></span>
>
> 4. <span data-ttu-id="170eb-183">Cliquez sur **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="170eb-183">Click **Application Settings**.</span></span> <span data-ttu-id="170eb-184">(Élément #3 dans l’image hello ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="170eb-184">(Item #3 in hello image below.)</span></span>
>
> 5. <span data-ttu-id="170eb-185">Bonjour **paramètres de l’application** section, ajoutez une nouvelle variable d’environnement nommée **PORT** et entrez votre numéro de port personnalisé pour la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="170eb-185">In hello **App settings** section, add a new environment variable named **PORT** and enter your custom port number for hello value.</span></span> <span data-ttu-id="170eb-186">(Élément #4 dans l’image hello ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="170eb-186">(Item #4 in hello image below.)</span></span>
>
> 6. <span data-ttu-id="170eb-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="170eb-187">Click **Save**.</span></span> <span data-ttu-id="170eb-188">(Article #5 image hello ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="170eb-188">(Item #5 in hello image below.)</span></span>
>
> ![L’enregistrement d’un numéro de port personnalisé Bonjour portail Azure][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="170eb-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="170eb-190">Next steps</span></span>

<span data-ttu-id="170eb-191">Pour plus d’informations sur l’utilisation des applications de démarrage du ressort sur Azure, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="170eb-191">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="170eb-192">Déployer un toohello ressort démarrage Application Azure App Service</span><span class="sxs-lookup"><span data-stu-id="170eb-192">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="170eb-193">Déployer une Application de démarrage ressort sur un Kubernetes Cluster Bonjour Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="170eb-193">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="170eb-194">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="170eb-194">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="170eb-195">Pour plus d’informations sur hello ressort démarrage sur l’exemple de projet Docker, consultez [démarrage ressort sur Docker mise en route].</span><span class="sxs-lookup"><span data-stu-id="170eb-195">For further details about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="170eb-196">Pour avec prise en main de vos propres applications ressort démarrage, consultez hello **ressort Initializr** à https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="170eb-196">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="170eb-197">Pour plus d’informations sur la prise en main de la création d’une application de démarrage du ressort simple, consultez hello ressort Initializr à https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="170eb-197">For more information about getting started with creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="170eb-198">Pour obtenir des exemples supplémentaires pour comment toouse personnalisé Docker images avec Azure, consultez [à l’aide d’une image Docker personnalisée pour l’application Web Azure sous Linux].</span><span class="sxs-lookup"><span data-stu-id="170eb-198">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure Interface de ligne de commande (CLI)]: /cli/azure/overview
[Azure conteneur de Service (ACS)]: https://azure.microsoft.com/services/container-service/
[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[créer un Registre de conteneur Docker privé à l’aide de hello portail Azure]: /azure/container-registry/container-registry-get-started-portal
[à l’aide d’une image Docker personnalisée pour l’application Web Azure sous Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[client Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[ressort démarrage]: http://projects.spring.io/spring-boot/
[démarrage ressort sur Docker mise en route]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
