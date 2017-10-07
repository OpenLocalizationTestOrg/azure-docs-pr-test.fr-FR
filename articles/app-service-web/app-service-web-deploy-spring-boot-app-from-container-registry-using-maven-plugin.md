---
title: "aaaHow toouse hello Maven du plug-in pour les applications Web Azure toodeploy une application de démarrage du ressort dans le Registre de conteneur Azure tooAzure du Service d’applications"
description: "Ce didacticiel vous guidera cependant hello étapes toodeploy une application de démarrage du ressort dans le Registre de conteneur Azure tooAzure tooAzure du Service d’applications à l’aide d’un plug-in Maven."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="39a96-103">Comment toouse hello plug-in Maven pour les applications Web Azure toodeploy, une application de démarrage du ressort dans le Registre de conteneur Azure tooAzure du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="39a96-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="39a96-104">Hello  **[Spring Framework]**  est une infrastructure open source populaire qui permet aux développeurs Java de créer des applications web, mobiles et API.</span><span class="sxs-lookup"><span data-stu-id="39a96-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="39a96-105">Ce didacticiel utilise un exemple d’application créé à l’aide de [ressort démarrage], une approche pilotée par convention pour l’utilisation du ressort tooget démarrer rapidement.</span><span class="sxs-lookup"><span data-stu-id="39a96-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="39a96-106">Cet article explique comment toodeploy un tooAzure d’application exemple ressort démarrage Registre de conteneur, puis utiliser hello plug-in Maven pour les applications Web Azure toodeploy votre tooAzure d’application du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="39a96-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="39a96-107">Hello Maven les plug-in pour les applications Web Azure est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="39a96-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="39a96-108">Pour l’instant, seule la publication FTP est pris en charge, bien que des fonctionnalités supplémentaires qui vont hello futures.</span><span class="sxs-lookup"><span data-stu-id="39a96-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="39a96-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="39a96-109">Prerequisites</span></span>

<span data-ttu-id="39a96-110">Commande toocomplete hello étapes décrites dans ce didacticiel, vous devez hello toohave suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="39a96-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="39a96-111">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="39a96-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="39a96-112">Hello [Azure Interface de ligne de commande (CLI)].</span><span class="sxs-lookup"><span data-stu-id="39a96-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="39a96-113">Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="39a96-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="39a96-114">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="39a96-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="39a96-115">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="39a96-115">A [Git] client.</span></span>
* <span data-ttu-id="39a96-116">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="39a96-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="39a96-117">En raison des exigences de la virtualisation toohello de ce didacticiel, vous ne peut pas suivre les étapes de hello dans cet article sur un ordinateur virtuel ; Vous devez utiliser un ordinateur physique avec les fonctionnalités de virtualisation activées.</span><span class="sxs-lookup"><span data-stu-id="39a96-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="39a96-118">Cloner l’exemple hello ressort démarrage sur l’application web de Docker</span><span class="sxs-lookup"><span data-stu-id="39a96-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="39a96-119">Dans cette section, vous clonez une application Spring Boot en conteneur et vous la testez localement.</span><span class="sxs-lookup"><span data-stu-id="39a96-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="39a96-120">Ouvrez une invite de commandes ou d’une fenêtre de terminal et créer un répertoire local de toohold votre application de démarrage du ressort et remplacez le répertoire toothat ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="39a96-121">- ou -</span><span class="sxs-lookup"><span data-stu-id="39a96-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="39a96-122">Hello du clone [démarrage ressort sur Docker mise en route] exemple de projet dans le répertoire hello créé ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="39a96-123">Changer le projet toohello terminée Active ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="39a96-124">Générer le fichier JAR hello à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="39a96-125">Lorsque l’application hello web a été créée, démarrer l’application hello web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="39a96-126">Tester l’application web hello en parcourant tooit localement à l’aide d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="39a96-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="39a96-127">Par exemple, vous pouvez utiliser hello commande suivante si vous avez curl disponible :</span><span class="sxs-lookup"><span data-stu-id="39a96-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="39a96-128">Vous devez voir hello message suivant s’affiche : **Hello World de Docker**</span><span class="sxs-lookup"><span data-stu-id="39a96-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="39a96-130">Créer un principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="39a96-130">Create an Azure service principal</span></span>

<span data-ttu-id="39a96-131">Dans cette section, vous créez Azure principal du service qui hello utilise de plug-in Maven lors du déploiement de votre tooAzure de conteneur.</span><span class="sxs-lookup"><span data-stu-id="39a96-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="39a96-132">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="39a96-132">Open a command prompt.</span></span>

1. <span data-ttu-id="39a96-133">Connectez-vous à votre compte Azure à l’aide de hello CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="39a96-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="39a96-134">Suivez hello instructions toocomplete hello processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="39a96-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="39a96-135">Créez un principal du service Azure :</span><span class="sxs-lookup"><span data-stu-id="39a96-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="39a96-136">Où `uuuuuuuu` est le nom d’utilisateur hello et `pppppppp` hello de mot de passe de principal du service hello.</span><span class="sxs-lookup"><span data-stu-id="39a96-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="39a96-137">Azure répond avec JSON qui ressemble à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="39a96-137">Azure responds with JSON that resembles hello following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="39a96-138">Vous allez utiliser les valeurs de hello à partir de cette réponse JSON lorsque vous configurez hello Maven plug-in toodeploy tooAzure de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="39a96-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="39a96-139">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, et `tttttttt` sont des valeurs d’espace réservé, qui sont utilisées dans cet exemple toomake toomap plus facilement ces éléments de tootheir respectifs valeurs lorsque vous configurez votre Maven `settings.xml` fichier ensuite Bonjour section.</span><span class="sxs-lookup"><span data-stu-id="39a96-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="39a96-140">Créer un Registre de conteneur Azure à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="39a96-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="39a96-141">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="39a96-141">Open a command prompt.</span></span>

1. <span data-ttu-id="39a96-142">Ouvrez une session dans tooyour compte Azure :</span><span class="sxs-lookup"><span data-stu-id="39a96-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="39a96-143">Créer des ressources Azure, que vous allez utiliser un groupe de ressources pour hello dans cet article :</span><span class="sxs-lookup"><span data-stu-id="39a96-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="39a96-144">Remplacez `wingtiptoysresources` dans cet exemple par un nom unique pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="39a96-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="39a96-145">Créer un Registre de conteneur Azure privée dans le groupe de ressources hello pour votre application de démarrage du ressort :</span><span class="sxs-lookup"><span data-stu-id="39a96-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="39a96-146">Remplacez `wingtiptoysregistry` dans cet exemple par un nom unique pour votre registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="39a96-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="39a96-147">Récupérer le mot de passe hello pour votre Registre de conteneur :</span><span class="sxs-lookup"><span data-stu-id="39a96-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="39a96-148">Azure répond avec votre mot de passe ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="39a96-149">Ajouter votre Registre de conteneur Azure et les paramètres du service Azure principal tooyour Maven</span><span class="sxs-lookup"><span data-stu-id="39a96-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="39a96-150">Ouvrez votre Maven `settings.xml` de fichiers dans un éditeur de texte ; ce fichier peut être dans un chemin d’accès comme hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="39a96-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="39a96-151">Ajouter des paramètres du Registre de conteneur Azure d’accès à partir de hello précédente section de cet article de toohello `<servers>` collection Bonjour *settings.xml* fichier ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="39a96-152">Où :</span><span class="sxs-lookup"><span data-stu-id="39a96-152">Where:</span></span>
   <span data-ttu-id="39a96-153">Élément</span><span class="sxs-lookup"><span data-stu-id="39a96-153">Element</span></span> | <span data-ttu-id="39a96-154">Description</span><span class="sxs-lookup"><span data-stu-id="39a96-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="39a96-155">Contient le nom hello du Registre de votre conteneur Azure privée.</span><span class="sxs-lookup"><span data-stu-id="39a96-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="39a96-156">Contient le nom hello du Registre de votre conteneur Azure privée.</span><span class="sxs-lookup"><span data-stu-id="39a96-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="39a96-157">Contient le mot de passe hello récupéré à la section précédente de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="39a96-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="39a96-158">Ajoutez vos paramètres de principal du service Azure à partir d’une section précédente de cet article de toohello `<servers>` collection Bonjour *settings.xml* fichier ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="39a96-159">Où :</span><span class="sxs-lookup"><span data-stu-id="39a96-159">Where:</span></span>
   <span data-ttu-id="39a96-160">Élément</span><span class="sxs-lookup"><span data-stu-id="39a96-160">Element</span></span> | <span data-ttu-id="39a96-161">Description</span><span class="sxs-lookup"><span data-stu-id="39a96-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="39a96-162">Spécifie un nom unique qui Maven utilise toolook vos paramètres de sécurité lorsque vous déployez votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="39a96-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="39a96-163">Contient hello `appId` valeur à partir de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="39a96-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="39a96-164">Contient hello `tenant` valeur à partir de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="39a96-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="39a96-165">Contient hello `password` valeur à partir de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="39a96-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="39a96-166">Définit l’environnement de cloud computing Azure cible hello, qui est `AZURE` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="39a96-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="39a96-167">(Une liste complète des environnements est disponible dans hello [Maven les plug-in pour les applications Web Azure] documentation)</span><span class="sxs-lookup"><span data-stu-id="39a96-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="39a96-168">Enregistrez et fermez hello *settings.xml* fichier.</span><span class="sxs-lookup"><span data-stu-id="39a96-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="39a96-169">Générer votre Docker image de conteneur et le Registre de conteneur Azure tooyour pousser</span><span class="sxs-lookup"><span data-stu-id="39a96-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="39a96-170">Accédez répertoire du projet pour votre application de démarrage du ressort, toohello terminée (par exemple) «*C:\SpringBoot\gs-spring-boot-docker\complete*« ou »*/users/robert/SpringBoot/gs-spring-boot-docker/complete*») et ouvrez hello *pom.xml* de fichiers avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="39a96-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="39a96-171">Hello de mise à jour `<properties>` collection Bonjour *pom.xml* fichier avec la valeur hello du serveur de connexion pour votre Registre de conteneur Azure à partir de la section précédente de hello de ce didacticiel ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="39a96-172">Où :</span><span class="sxs-lookup"><span data-stu-id="39a96-172">Where:</span></span>
   <span data-ttu-id="39a96-173">Élément</span><span class="sxs-lookup"><span data-stu-id="39a96-173">Element</span></span> | <span data-ttu-id="39a96-174">Description</span><span class="sxs-lookup"><span data-stu-id="39a96-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="39a96-175">Spécifie le nom hello du Registre de votre conteneur Azure privée.</span><span class="sxs-lookup"><span data-stu-id="39a96-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="39a96-176">Spécifie l’URL hello de votre Registre de conteneur Azure privée, qui est dérivé en ajoutant «. azurecr.io « nom toohello du Registre de votre conteneur privé.</span><span class="sxs-lookup"><span data-stu-id="39a96-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="39a96-177">Vérifiez que `<plugin>` pour le plug-in de Docker hello dans votre *pom.xml* fichier contient des propriétés de correct hello pour hello adresse et du Registre nom du serveur à partir de l’étape précédente de hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="39a96-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="39a96-178">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-178">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="39a96-179">Où :</span><span class="sxs-lookup"><span data-stu-id="39a96-179">Where:</span></span>
   <span data-ttu-id="39a96-180">Élément</span><span class="sxs-lookup"><span data-stu-id="39a96-180">Element</span></span> | <span data-ttu-id="39a96-181">Description</span><span class="sxs-lookup"><span data-stu-id="39a96-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="39a96-182">Spécifie la propriété hello qui contient le nom de votre Registre de conteneur Azure privée.</span><span class="sxs-lookup"><span data-stu-id="39a96-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="39a96-183">Spécifie la propriété hello qui contient l’URL de hello du Registre de votre conteneur Azure privée.</span><span class="sxs-lookup"><span data-stu-id="39a96-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="39a96-184">Accédez répertoire du projet pour votre application de démarrage du ressort toohello s’est terminée et exécutez hello après application de commande toorebuild hello push hello conteneur tooyour Registre de conteneur Azure :</span><span class="sxs-lookup"><span data-stu-id="39a96-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="39a96-185">FACULTATIF : Parcourir toohello [portail Azure] et vérifiez qu’il existe une image de conteneur Docker nommée **gs-spring-démarrage-docker** dans le Registre de conteneur.</span><span class="sxs-lookup"><span data-stu-id="39a96-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Vérification du conteneur dans le portail Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="39a96-187">Personnaliser votre pom.xml, puis créez et déployez votre tooAzure de conteneur</span><span class="sxs-lookup"><span data-stu-id="39a96-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="39a96-188">Ouvrez hello `pom.xml` de fichiers pour votre application de démarrage du ressort dans un éditeur de texte et recherchez hello `<plugin>` , élément pour `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="39a96-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="39a96-189">Cet élément doit ressembler à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="39a96-189">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="39a96-190">Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in de hello Maven et une description détaillée de chacun de ces éléments est disponible dans hello [Maven les plug-in pour les applications Web Azure] documentation.</span><span class="sxs-lookup"><span data-stu-id="39a96-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="39a96-191">Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :</span><span class="sxs-lookup"><span data-stu-id="39a96-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="39a96-192">Élément</span><span class="sxs-lookup"><span data-stu-id="39a96-192">Element</span></span> | <span data-ttu-id="39a96-193">Description</span><span class="sxs-lookup"><span data-stu-id="39a96-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="39a96-194">Spécifie la version de hello de hello [Maven les plug-in pour les applications Web Azure].</span><span class="sxs-lookup"><span data-stu-id="39a96-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="39a96-195">Vous devez vérifier la version de hello répertoriée dans hello [référentiel Central Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que vous utilisez hello version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="39a96-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="39a96-196">Spécifie les informations d’authentification hello pour Azure, qui dans cet exemple contient un `<serverId>` élément contenant `azure-auth`; Maven utilise ce toolook valeur des valeurs de principal de service Azure hello dans votre Maven *settings.xml* fichier que vous avez définie dans une section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="39a96-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="39a96-197">Spécifie le groupe de ressources cible hello, qui est `wingtiptoysresources` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="39a96-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="39a96-198">groupe de ressources Hello sera créé au cours du déploiement s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="39a96-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="39a96-199">Spécifie le nom de la cible hello pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="39a96-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="39a96-200">Dans cet exemple, le nom de la cible hello est `maven-linux-app-${maven.build.timestamp}`, où hello `${maven.build.timestamp}` suffixe est ajouté dans ce conflit de tooavoid exemple.</span><span class="sxs-lookup"><span data-stu-id="39a96-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="39a96-201">(vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application hello ; hello timestamp est facultative.)</span><span class="sxs-lookup"><span data-stu-id="39a96-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="39a96-202">Spécifie la région cible hello, qui, dans cet exemple est `westus`.</span><span class="sxs-lookup"><span data-stu-id="39a96-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="39a96-203">(Une liste complète est Bonjour [Maven les plug-in pour les applications Web Azure] documentation.)</span><span class="sxs-lookup"><span data-stu-id="39a96-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="39a96-204">Spécifie les propriétés hello qui contiennent le nom de hello et l’URL de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="39a96-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="39a96-205">Spécifie des paramètres uniques pour Maven toouse lors du déploiement de votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="39a96-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="39a96-206">Dans cet exemple, un `<property>` élément contient une paire nom/valeur des éléments enfants qui spécifient le port hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="39a96-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="39a96-207">numéro de port Hello paramètres toochange hello dans cet exemple ne sont nécessaires lorsque vous modifiez le port de hello à partir de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="39a96-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="39a96-208">À partir d’invite de commandes hello ou fenêtre de Terminal Server que vous utilisiez précédemment, régénérez le fichier JAR hello à l’aide de Maven si vous avez apporté les modifications de toohello *pom.xml* fichier ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="39a96-209">Déployer votre tooAzure d’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="39a96-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="39a96-210">Maven déploierez votre tooAzure d’application web ; Si l’application hello web n’existe pas déjà, il sera créé.</span><span class="sxs-lookup"><span data-stu-id="39a96-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="39a96-211">Si la région hello que vous spécifiez dans hello `<region>` élément de votre *pom.xml* fichier n’a pas suffisamment de serveurs disponibles lorsque vous démarrez votre déploiement, vous pouvez voir un toohello similaire erreur l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="39a96-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="39a96-212">Si cela se produit, vous pouvez spécifier qu'une autre région et exécutez de nouveau hello Maven commande toodeploy votre application.</span><span class="sxs-lookup"><span data-stu-id="39a96-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="39a96-213">Lorsque votre site web a été déployée, vous serez en mesure de toomanage à l’aide de hello [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="39a96-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="39a96-214">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="39a96-214">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="39a96-216">Et hello URL pour votre application web s’afficheront dans hello **vue d’ensemble** pour votre application web :</span><span class="sxs-lookup"><span data-stu-id="39a96-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Détermination des URL hello pour votre application web][AP02]

## <a name="next-steps"></a><span data-ttu-id="39a96-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39a96-218">Next steps</span></span>

<span data-ttu-id="39a96-219">Pour plus d’informations sur hello diverses technologies abordées dans cet article, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="39a96-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="39a96-220">[Maven les plug-in pour les applications Web Azure]</span><span class="sxs-lookup"><span data-stu-id="39a96-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="39a96-221">Connectez-vous à tooAzure de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="39a96-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="39a96-222">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="39a96-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="39a96-223">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="39a96-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="39a96-224">[Plug-in Docker pour Maven]</span><span class="sxs-lookup"><span data-stu-id="39a96-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure Interface de ligne de commande (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[Maven les plug-in pour les applications Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[client Docker]: https://www.docker.com/
[Plug-in Docker pour Maven]: https://github.com/spotify/docker-maven-plugin
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[ressort démarrage]: http://projects.spring.io/spring-boot/
[démarrage ressort sur Docker mise en route]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
