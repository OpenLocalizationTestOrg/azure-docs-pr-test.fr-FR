---
title: "Comment utiliser le plug-in Maven pour Azure Web Apps pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service"
description: "Ce didacticiel vous guide à travers les étapes pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service à l’aide d’un plug-in Maven."
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
ms.openlocfilehash: f47ee59d72ea49d62be2cb435ebaf8bc841e4198
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="89006-103">Comment utiliser le plug-in Maven pour Azure Web Apps pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="89006-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="89006-104">Le **[Spring Framework]** est une infrastructure open source populaire qui aide les développeurs Java à créer des applications web, mobiles et API.</span><span class="sxs-lookup"><span data-stu-id="89006-104">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="89006-105">Ce didacticiel utilise un exemple d’application créé à l’aide de [Spring Boot], une approche orientée par une convention permettant de prendre en main et d’utiliser Spring rapidement.</span><span class="sxs-lookup"><span data-stu-id="89006-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="89006-106">Cet article explique comment déployer un exemple d’application Spring Boot dans Azure Container Registry, puis utiliser le plug-in Maven pour Azure Web Apps pour déployer votre application dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="89006-106">This article demonstrates how to deploy a sample Spring Boot application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="89006-107">Le plug-in Maven pour Azure Web Apps est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="89006-107">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="89006-108">Pour l’instant, seule la publication FTP est prise en charge, mais des fonctionnalités supplémentaires sont envisagées pour le futur.</span><span class="sxs-lookup"><span data-stu-id="89006-108">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="89006-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="89006-109">Prerequisites</span></span>

<span data-ttu-id="89006-110">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="89006-110">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="89006-111">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="89006-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="89006-112">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="89006-112">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="89006-113">Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="89006-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="89006-114">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="89006-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="89006-115">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="89006-115">A [Git] client.</span></span>
* <span data-ttu-id="89006-116">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="89006-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="89006-117">En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.</span><span class="sxs-lookup"><span data-stu-id="89006-117">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="89006-118">Cloner l’exemple Spring Boot sur l’application web Docker</span><span class="sxs-lookup"><span data-stu-id="89006-118">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="89006-119">Dans cette section, vous clonez une application Spring Boot en conteneur et vous la testez localement.</span><span class="sxs-lookup"><span data-stu-id="89006-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="89006-120">Ouvrez une invite de commandes ou une fenêtre de terminal et créez un répertoire local pour y stocker votre application Spring Boot, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="89006-121">- ou -</span><span class="sxs-lookup"><span data-stu-id="89006-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="89006-122">Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire que vous venez de créer. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-122">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="89006-123">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="89006-124">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="89006-125">Lorsque l’application web a été créée, démarrez l’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="89006-126">Testez l’application web en y accédant localement via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="89006-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="89006-127">Par exemple, vous pouvez utiliser la commande suivante si curl est disponible :</span><span class="sxs-lookup"><span data-stu-id="89006-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="89006-128">Vous devez normalement voir le message suivant : **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="89006-128">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="89006-130">Créer un principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="89006-130">Create an Azure service principal</span></span>

<span data-ttu-id="89006-131">Dans cette section, vous créez un principal du service Azure utilisé par le plug-in Maven lors du déploiement de votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89006-131">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="89006-132">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="89006-132">Open a command prompt.</span></span>

1. <span data-ttu-id="89006-133">Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="89006-133">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="89006-134">Suivez les instructions pour terminer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="89006-134">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="89006-135">Créez un principal du service Azure :</span><span class="sxs-lookup"><span data-stu-id="89006-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="89006-136">Où `uuuuuuuu` est le nom d’utilisateur et `pppppppp` est le mot de passe du principal du service.</span><span class="sxs-lookup"><span data-stu-id="89006-136">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="89006-137">Azure répond avec un texte JSON similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="89006-137">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="89006-138">Vous utiliserez les valeurs de cette réponse JSON lors de la configuration du plug-in Maven pour déployer votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89006-138">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="89006-139">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` et `tttttttt` sont des valeurs d’espace réservé qui sont utilisées dans cet exemple pour faciliter le mappage de ces valeurs avec leurs éléments respectifs lorsque vous configurerez votre fichier `settings.xml` Maven dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="89006-139">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="89006-140">Créer un registre de conteneurs Azure à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="89006-140">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="89006-141">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="89006-141">Open a command prompt.</span></span>

1. <span data-ttu-id="89006-142">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="89006-142">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="89006-143">Créez un groupe de ressources pour les ressources Azure que vous utiliserez dans cet article :</span><span class="sxs-lookup"><span data-stu-id="89006-143">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="89006-144">Remplacez `wingtiptoysresources` dans cet exemple par un nom unique pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="89006-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="89006-145">Créez un registre de conteneurs Azure privé dans le groupe de ressources pour votre application Spring Boot :</span><span class="sxs-lookup"><span data-stu-id="89006-145">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="89006-146">Remplacez `wingtiptoysregistry` dans cet exemple par un nom unique pour votre registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="89006-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="89006-147">Récupérez le mot de passe pour votre registre de conteneurs :</span><span class="sxs-lookup"><span data-stu-id="89006-147">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="89006-148">Azure répond avec votre mot de passe ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="89006-149">Ajouter votre registre de conteneurs Azure et votre principal du service Azure à vos paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="89006-149">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="89006-150">Ouvrez votre fichier `settings.xml` Maven dans un éditeur de texte ; ce fichier peut avoir un chemin d’accès similaire aux exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="89006-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="89006-151">Ajoutez les paramètres d’accès de votre registre de conteneurs Azure de la section précédente de cet article à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-151">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="89006-152">Où :</span><span class="sxs-lookup"><span data-stu-id="89006-152">Where:</span></span>
   <span data-ttu-id="89006-153">Élément</span><span class="sxs-lookup"><span data-stu-id="89006-153">Element</span></span> | <span data-ttu-id="89006-154">Description</span><span class="sxs-lookup"><span data-stu-id="89006-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="89006-155">Contient le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="89006-155">Contains the name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="89006-156">Contient le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="89006-156">Contains the name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="89006-157">Contient le mot de passe que vous avez récupéré dans la section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="89006-157">Contains the password you retrieved in the previous section of this article.</span></span>

1. <span data-ttu-id="89006-158">Ajoutez vos paramètres du principal de service Azure d’une section précédente de cet article à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-158">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="89006-159">Où :</span><span class="sxs-lookup"><span data-stu-id="89006-159">Where:</span></span>
   <span data-ttu-id="89006-160">Élément</span><span class="sxs-lookup"><span data-stu-id="89006-160">Element</span></span> | <span data-ttu-id="89006-161">Description</span><span class="sxs-lookup"><span data-stu-id="89006-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="89006-162">Spécifie un nom unique que Maven utilise pour rechercher vos paramètres de sécurité lorsque vous déployez votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89006-162">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="89006-163">Contient la valeur `appId` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="89006-163">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="89006-164">Contient la valeur `tenant` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="89006-164">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="89006-165">Contient la valeur `password` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="89006-165">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="89006-166">Définit l’environnement de cloud Azure cible, qui est `AZURE` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="89006-166">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="89006-167">(Une liste complète des environnements est disponible dans la documentation [Maven Plugin for Azure Web Apps])</span><span class="sxs-lookup"><span data-stu-id="89006-167">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="89006-168">Enregistrez et fermez le fichier *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="89006-168">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="89006-169">Créer votre image conteneur Docker et la placer dans votre registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="89006-169">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="89006-170">Accédez au répertoire du projet terminé pour votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="89006-170">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="89006-171">Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la valeur du serveur de connexion pour votre registre de conteneurs Azure de la section précédente de ce didacticiel. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-171">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="89006-172">Où :</span><span class="sxs-lookup"><span data-stu-id="89006-172">Where:</span></span>
   <span data-ttu-id="89006-173">Élément</span><span class="sxs-lookup"><span data-stu-id="89006-173">Element</span></span> | <span data-ttu-id="89006-174">Description</span><span class="sxs-lookup"><span data-stu-id="89006-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="89006-175">Spécifie le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="89006-175">Specifies the name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="89006-176">Spécifie l’URL de votre registre de conteneurs Azure privé qui est obtenue en ajoutant « .azurecr.io » au nom de votre registre de conteneurs privé.</span><span class="sxs-lookup"><span data-stu-id="89006-176">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span>

1. <span data-ttu-id="89006-177">Vérifiez que `<plugin>` pour le plug-in Docker dans votre fichier *pom.xml* contient les propriétés appropriées de connexion pour l’adresse du serveur et le nom du registre mentionnées à l’étape précédente de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="89006-177">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="89006-178">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-178">For example:</span></span>

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
   <span data-ttu-id="89006-179">Où :</span><span class="sxs-lookup"><span data-stu-id="89006-179">Where:</span></span>
   <span data-ttu-id="89006-180">Élément</span><span class="sxs-lookup"><span data-stu-id="89006-180">Element</span></span> | <span data-ttu-id="89006-181">Description</span><span class="sxs-lookup"><span data-stu-id="89006-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="89006-182">Spécifie la propriété contenant le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="89006-182">Specifies the property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="89006-183">Spécifie la propriété contenant l’URL de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="89006-183">Specifies the property which contains the URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="89006-184">Accédez au répertoire du projet terminé de votre application Spring Boot, et exécutez la commande suivante pour régénérer l’application et placer le conteneur dans votre registre de conteneurs Azure :</span><span class="sxs-lookup"><span data-stu-id="89006-184">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="89006-185">FACULTATIF : accédez au [portail Azure] et vérifiez qu’il existe une image de conteneur Docker nommée **gs-spring-boot-docker** dans le registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="89006-185">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Vérification du conteneur dans le portail Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="89006-187">Personnaliser votre pom.xml, puis créer et déployer votre conteneur dans Azure</span><span class="sxs-lookup"><span data-stu-id="89006-187">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="89006-188">Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte et recherchez l’élément `<plugin>` pour `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="89006-188">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="89006-189">Cet élément doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="89006-189">This element should resemble the following example:</span></span>

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

<span data-ttu-id="89006-190">Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in Maven ; une description détaillée de chacun de ces éléments est disponible dans la documentation [Maven Plugin for Azure Web Apps] (Plug-in Maven pour Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="89006-190">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="89006-191">Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :</span><span class="sxs-lookup"><span data-stu-id="89006-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="89006-192">Élément</span><span class="sxs-lookup"><span data-stu-id="89006-192">Element</span></span> | <span data-ttu-id="89006-193">Description</span><span class="sxs-lookup"><span data-stu-id="89006-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="89006-194">Spécifie la version du [Maven Plugin for Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="89006-194">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="89006-195">Vous devez vérifier la version répertoriée dans le [référentiel Maven central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) pour vous assurer que vous utilisez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="89006-195">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="89006-196">Spécifie les informations d’authentification pour Azure, qui dans cet exemple comportent un élément `<serverId>` contenant `azure-auth` ; Maven utilise cette valeur pour rechercher les valeurs du principal du service Azure dans votre fichier *settings.xml* Maven que vous avez défini dans une section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="89006-196">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="89006-197">Spécifie le groupe de ressources cible, qui est `wingtiptoysresources` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="89006-197">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="89006-198">Il sera créé au cours du déploiement s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="89006-198">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="89006-199">Spécifie le nom cible de votre application web.</span><span class="sxs-lookup"><span data-stu-id="89006-199">Specifies the target name for your web app.</span></span> <span data-ttu-id="89006-200">Dans cet exemple, le nom cible est `maven-linux-app-${maven.build.timestamp}`, où le suffixe `${maven.build.timestamp}` est ajouté dans cet exemple pour éviter tout conflit.</span><span class="sxs-lookup"><span data-stu-id="89006-200">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="89006-201">(L’horodatage est facultatif ; vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application.)</span><span class="sxs-lookup"><span data-stu-id="89006-201">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="89006-202">Spécifie la région cible, qui dans cet exemple est `westus`.</span><span class="sxs-lookup"><span data-stu-id="89006-202">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="89006-203">(Une liste complète est disponible dans la documentation [Maven Plugin for Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="89006-203">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="89006-204">Spécifie les propriétés qui contiennent le nom et l’URL de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="89006-204">Specifies the properties which contain the name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="89006-205">Spécifie des paramètres uniques que Maven utilisera lors du déploiement de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89006-205">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="89006-206">Dans cet exemple, un élément `<property>` contient une paire nom/valeur d’éléments enfants qui spécifie le port pour votre application.</span><span class="sxs-lookup"><span data-stu-id="89006-206">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="89006-207">Les paramètres de modification du numéro de port fournis dans cet exemple sont nécessaires uniquement lorsque vous modifiez le port à partir de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="89006-207">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="89006-208">À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-208">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="89006-209">Déployez votre application web dans Azure à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="89006-209">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="89006-210">Maven déploiera votre application web dans Azure. Si l’application web n’existe pas déjà, elle sera créée.</span><span class="sxs-lookup"><span data-stu-id="89006-210">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="89006-211">Si la région que vous spécifiez dans l’élément `<region>` de votre fichier *pom.xml* n’a pas suffisamment de serveurs disponibles lorsque vous démarrez votre déploiement, vous pouvez voir un message d’erreur similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="89006-211">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="89006-212">Dans ce cas, vous pouvez spécifier une autre région et ré-exécuter la commande Maven pour déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="89006-212">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="89006-213">Lorsque votre application web aura été déployée, vous serez en mesure de la gérer à l’aide du [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="89006-213">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="89006-214">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="89006-214">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="89006-216">Et l’URL de votre application web sera répertoriée dans la **Vue d’ensemble** de votre application web :</span><span class="sxs-lookup"><span data-stu-id="89006-216">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Détermination de l’URL de votre application web][AP02]

## <a name="next-steps"></a><span data-ttu-id="89006-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89006-218">Next steps</span></span>

<span data-ttu-id="89006-219">Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="89006-219">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="89006-220">[Maven Plugin for Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="89006-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="89006-221">Se connecter à Azure à partir de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="89006-221">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="89006-222">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="89006-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="89006-223">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="89006-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="89006-224">[Plug-in Docker pour Maven]</span><span class="sxs-lookup"><span data-stu-id="89006-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

<span data-ttu-id="89006-225">[Azure CLI]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="89006-225">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
<span data-ttu-id="89006-226">[portail Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="89006-226">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="89006-227">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="89006-227">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span></span>
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
<span data-ttu-id="89006-228">[client Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="89006-228">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="89006-229">[Plug-in Docker pour Maven]: https://github.com/spotify/docker-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="89006-229">[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin</span></span>
<span data-ttu-id="89006-230">[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="89006-230">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="89006-231">[client Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="89006-231">[Git]: https://github.com/</span></span>
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
<span data-ttu-id="89006-232">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="89006-232">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="89006-233">[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="89006-233">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="89006-234">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="89006-234">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="89006-235">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="89006-235">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="89006-236">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="89006-236">[Spring Framework]: https://spring.io/</span></span>

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
