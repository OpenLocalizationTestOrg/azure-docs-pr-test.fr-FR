---
title: "Découvrez comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot en conteneur dans Azure"
description: "Découvrez comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot dans Azure."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 883040590291cee94daa227fbc6715ad4be0b393
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a><span data-ttu-id="58cc7-103">Découvrez comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot en conteneur dans Azure</span><span class="sxs-lookup"><span data-stu-id="58cc7-103">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>

<span data-ttu-id="58cc7-104">Le [plug-in Maven pour Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) pour [Apache Maven](http://maven.apache.org/) assure une intégration transparente d’Azure App Service dans les projets Maven et rationalise le processus pour permettre aux développeurs de déployer des applications web dans Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="58cc7-104">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service .</span></span>

<span data-ttu-id="58cc7-105">Cet article présente l’utilisation du plug-in Maven pour Azure Web Apps afin de déployer un exemple d’application Spring Boot dans un conteneur Docker dans Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="58cc7-105">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application in a Docker container to Azure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="58cc7-106">Le plug-in Maven pour Azure Web Apps est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="58cc7-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="58cc7-107">Pour l’instant, seule la publication FTP est prise en charge, mais des fonctionnalités supplémentaires sont envisagées pour le futur.</span><span class="sxs-lookup"><span data-stu-id="58cc7-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="58cc7-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="58cc7-108">Prerequisites</span></span>

<span data-ttu-id="58cc7-109">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="58cc7-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="58cc7-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="58cc7-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="58cc7-111">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="58cc7-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="58cc7-112">Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="58cc7-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="58cc7-113">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="58cc7-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="58cc7-114">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="58cc7-114">A [Git] client.</span></span>
* <span data-ttu-id="58cc7-115">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="58cc7-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="58cc7-116">En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.</span><span class="sxs-lookup"><span data-stu-id="58cc7-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="58cc7-117">Cloner l’exemple Spring Boot sur l’application web Docker</span><span class="sxs-lookup"><span data-stu-id="58cc7-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="58cc7-118">Dans cette section, vous clonez une application Spring Boot en conteneur et vous la testez localement.</span><span class="sxs-lookup"><span data-stu-id="58cc7-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="58cc7-119">Ouvrez une invite de commandes ou une fenêtre de terminal et créez un répertoire local pour y stocker votre application Spring Boot, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58cc7-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="58cc7-120">- ou -</span><span class="sxs-lookup"><span data-stu-id="58cc7-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="58cc7-121">Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire que vous venez de créer. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58cc7-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="58cc7-122">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58cc7-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="58cc7-123">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58cc7-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="58cc7-124">Lorsque l’application web a été créée, démarrez l’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="58cc7-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="58cc7-125">Testez l’application web en y accédant localement via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="58cc7-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="58cc7-126">Par exemple, vous pouvez utiliser la commande suivante si curl est disponible :</span><span class="sxs-lookup"><span data-stu-id="58cc7-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="58cc7-127">Vous devez normalement voir le message suivant : **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="58cc7-127">You should see the following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="58cc7-128">Créer un principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="58cc7-128">Create an Azure service principal</span></span>

<span data-ttu-id="58cc7-129">Dans cette section, vous créez un principal du service Azure utilisé par le plug-in Maven lors du déploiement de votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="58cc7-129">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="58cc7-130">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="58cc7-130">Open a command prompt.</span></span>

1. <span data-ttu-id="58cc7-131">Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="58cc7-131">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="58cc7-132">Suivez les instructions pour terminer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="58cc7-132">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="58cc7-133">Créez un principal du service Azure :</span><span class="sxs-lookup"><span data-stu-id="58cc7-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="58cc7-134">Où `uuuuuuuu` est le nom d’utilisateur et `pppppppp` est le mot de passe du principal du service.</span><span class="sxs-lookup"><span data-stu-id="58cc7-134">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="58cc7-135">Azure répond avec un texte JSON similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="58cc7-135">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="58cc7-136">Vous utiliserez les valeurs de cette réponse JSON lors de la configuration du plug-in Maven pour déployer votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="58cc7-136">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="58cc7-137">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` et `tttttttt` sont des valeurs d’espace réservé qui sont utilisées dans cet exemple pour faciliter le mappage de ces valeurs avec leurs éléments respectifs lorsque vous configurerez votre fichier `settings.xml` Maven dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="58cc7-137">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="58cc7-138">Configurer Maven pour utiliser votre principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="58cc7-138">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="58cc7-139">Dans cette section, vous utilisez les valeurs de votre principal du service Azure pour configurer l’authentification qui sera utilisée par Maven lors du déploiement de votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="58cc7-139">In this section, you use the values from your Azure service principal to configure the authentication that Maven will use when deploying your container to Azure.</span></span>

1. <span data-ttu-id="58cc7-140">Ouvrez votre fichier `settings.xml` Maven dans un éditeur de texte ; ce fichier peut avoir un chemin d’accès similaire aux exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="58cc7-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="58cc7-141">Ajoutez les paramètres de votre principal du service Azure de la section précédente de ce didacticiel à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58cc7-141">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="58cc7-142">Où :</span><span class="sxs-lookup"><span data-stu-id="58cc7-142">Where:</span></span>
   <span data-ttu-id="58cc7-143">Élément</span><span class="sxs-lookup"><span data-stu-id="58cc7-143">Element</span></span> | <span data-ttu-id="58cc7-144">Description</span><span class="sxs-lookup"><span data-stu-id="58cc7-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="58cc7-145">Spécifie un nom unique que Maven utilise pour rechercher vos paramètres de sécurité lorsque vous déployez votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="58cc7-145">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="58cc7-146">Contient la valeur `appId` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="58cc7-146">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="58cc7-147">Contient la valeur `tenant` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="58cc7-147">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="58cc7-148">Contient la valeur `password` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="58cc7-148">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="58cc7-149">Définit l’environnement de cloud Azure cible, qui est `AZURE` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="58cc7-149">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="58cc7-150">(Une liste complète des environnements est disponible dans la documentation [Maven Plugin for Azure Web Apps])</span><span class="sxs-lookup"><span data-stu-id="58cc7-150">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="58cc7-151">Enregistrez et fermez le fichier *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="58cc7-151">Save and close the *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a><span data-ttu-id="58cc7-152">FACULTATIF : Déployer votre fichier Docker local dans Docker Hub</span><span class="sxs-lookup"><span data-stu-id="58cc7-152">OPTIONAL: Deploy your local Docker file to Docker Hub</span></span>

<span data-ttu-id="58cc7-153">Si vous avez un compte Docker, vous pouvez générer votre image de conteneur Docker localement et la placer dans Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="58cc7-153">If you have a Docker account, you can build your Docker container image locally and push it to Docker Hub.</span></span> <span data-ttu-id="58cc7-154">Pour ce faire, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="58cc7-154">To do so, use the following steps.</span></span>

1. <span data-ttu-id="58cc7-155">Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="58cc7-155">Open the `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="58cc7-156">Recherchez l’élément `<imageName>` enfant de l’élément `<containerSettings>`.</span><span class="sxs-lookup"><span data-stu-id="58cc7-156">Locate the `<imageName>` child element of the `<containerSettings>` element.</span></span>

1. <span data-ttu-id="58cc7-157">Mettez à jour la valeur `${docker.image.prefix}` avec le nom de votre compte Docker :</span><span class="sxs-lookup"><span data-stu-id="58cc7-157">Update the `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="58cc7-158">Choisissez l’une des méthodes de déploiement suivantes :</span><span class="sxs-lookup"><span data-stu-id="58cc7-158">Choose one of the following deployment methods:</span></span>

   * <span data-ttu-id="58cc7-159">Générez votre image de conteneur localement avec Maven, puis utilisez Docker pour placer votre conteneur dans Docker Hub :</span><span class="sxs-lookup"><span data-stu-id="58cc7-159">Build your container image locally with Maven, and then use Docker to push your container to Docker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="58cc7-160">Si vous avez le [plug-in Docker pour Maven] installé, vous pouvez générer automatiquement votre image de conteneur dans Docker Hub à l’aide du paramètre `-DpushImage` :</span><span class="sxs-lookup"><span data-stu-id="58cc7-160">If you have the [Docker plugin for Maven] installed, you can automatically build and your container image to Docker Hub by using the `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a><span data-ttu-id="58cc7-161">FACULTATIF : Personnaliser votre fichier pom.xml avant de déployer votre conteneur dans Azure</span><span class="sxs-lookup"><span data-stu-id="58cc7-161">OPTIONAL: Customize your pom.xml before deploying your container to Azure</span></span>

<span data-ttu-id="58cc7-162">Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte et recherchez l’élément `<plugin>` pour `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="58cc7-162">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="58cc7-163">Cet élément doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="58cc7-163">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
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

<span data-ttu-id="58cc7-164">Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in Maven ; une description détaillée de chacun de ces éléments est disponible dans la documentation [Maven Plugin for Azure Web Apps] (Plug-in Maven pour Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="58cc7-164">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="58cc7-165">Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :</span><span class="sxs-lookup"><span data-stu-id="58cc7-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="58cc7-166">Élément</span><span class="sxs-lookup"><span data-stu-id="58cc7-166">Element</span></span> | <span data-ttu-id="58cc7-167">Description</span><span class="sxs-lookup"><span data-stu-id="58cc7-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="58cc7-168">Spécifie la version du [Maven Plugin for Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="58cc7-168">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="58cc7-169">Vous devez vérifier la version répertoriée dans le [référentiel Maven central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) pour vous assurer que vous utilisez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="58cc7-169">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="58cc7-170">Spécifie les informations d’authentification pour Azure, qui dans cet exemple comportent un élément `<serverId>` contenant `azure-auth` ; Maven utilise cette valeur pour rechercher les valeurs du principal du service Azure dans votre fichier *settings.xml* Maven que vous avez défini dans une section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="58cc7-170">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="58cc7-171">Spécifie le groupe de ressources cible, qui est `maven-plugin` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="58cc7-171">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="58cc7-172">Il sera créé au cours du déploiement s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="58cc7-172">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="58cc7-173">Spécifie le nom cible de votre application web.</span><span class="sxs-lookup"><span data-stu-id="58cc7-173">Specifies the target name for your web app.</span></span> <span data-ttu-id="58cc7-174">Dans cet exemple, le nom cible est `maven-linux-app-${maven.build.timestamp}`, où le suffixe `${maven.build.timestamp}` est ajouté dans cet exemple pour éviter tout conflit.</span><span class="sxs-lookup"><span data-stu-id="58cc7-174">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="58cc7-175">(L’horodatage est facultatif ; vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application.)</span><span class="sxs-lookup"><span data-stu-id="58cc7-175">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="58cc7-176">Spécifie la région cible, qui dans cet exemple est `westus`.</span><span class="sxs-lookup"><span data-stu-id="58cc7-176">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="58cc7-177">(Une liste complète est disponible dans la documentation [Maven Plugin for Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="58cc7-177">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="58cc7-178">Spécifie des paramètres uniques que Maven utilisera lors du déploiement de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="58cc7-178">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="58cc7-179">Dans cet exemple, un élément `<property>` contient une paire nom/valeur d’éléments enfants qui spécifie le port pour votre application.</span><span class="sxs-lookup"><span data-stu-id="58cc7-179">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="58cc7-180">Les paramètres de modification du numéro de port fournis dans cet exemple sont nécessaires uniquement lorsque vous modifiez le port à partir de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="58cc7-180">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

## <a name="build-and-deploy-your-container-to-azure"></a><span data-ttu-id="58cc7-181">Créer et déployer votre conteneur dans Azure</span><span class="sxs-lookup"><span data-stu-id="58cc7-181">Build and deploy your container to Azure</span></span>

<span data-ttu-id="58cc7-182">Une fois que vous avez configuré tous les paramètres dans les sections précédentes de cet article, vous êtes prêt à déployer votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="58cc7-182">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your container to Azure.</span></span> <span data-ttu-id="58cc7-183">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="58cc7-183">To do so, use the following steps:</span></span>

1. <span data-ttu-id="58cc7-184">À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="58cc7-184">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="58cc7-185">Déployez votre application web dans Azure à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="58cc7-185">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="58cc7-186">Maven déploiera votre application web dans Azure. Si l’application web n’existe pas déjà, elle sera créée.</span><span class="sxs-lookup"><span data-stu-id="58cc7-186">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="58cc7-187">Si la région que vous spécifiez dans l’élément `<region>` de votre fichier *pom.xml* n’a pas suffisamment de serveurs disponibles lorsque vous démarrez votre déploiement, vous pouvez voir un message d’erreur similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="58cc7-187">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="58cc7-188">Dans ce cas, vous pouvez spécifier une autre région et ré-exécuter la commande Maven pour déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="58cc7-188">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="58cc7-189">Lorsque votre application web aura été déployée, vous serez en mesure de la gérer à l’aide du [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="58cc7-189">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="58cc7-190">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="58cc7-190">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="58cc7-192">Et l’URL de votre application web sera répertoriée dans la **Vue d’ensemble** de votre application web :</span><span class="sxs-lookup"><span data-stu-id="58cc7-192">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Détermination de l’URL de votre application web][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="58cc7-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58cc7-194">Next steps</span></span>

<span data-ttu-id="58cc7-195">Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="58cc7-195">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="58cc7-196">[Maven Plugin for Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="58cc7-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="58cc7-197">Se connecter à Azure à partir de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="58cc7-197">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="58cc7-198">Comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot dans Azure App Services </span><span class="sxs-lookup"><span data-stu-id="58cc7-198">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="58cc7-199">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="58cc7-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="58cc7-200">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="58cc7-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="58cc7-201">[plug-in Docker pour Maven]</span><span class="sxs-lookup"><span data-stu-id="58cc7-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

<span data-ttu-id="58cc7-202">[Azure CLI]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="58cc7-202">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
<span data-ttu-id="58cc7-203">[portail Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="58cc7-203">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="58cc7-204">[client Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="58cc7-204">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="58cc7-205">[plug-in Docker pour Maven]: https://github.com/spotify/docker-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="58cc7-205">[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin</span></span>
<span data-ttu-id="58cc7-206">[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="58cc7-206">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="58cc7-207">[client Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="58cc7-207">[Git]: https://github.com/</span></span>
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
<span data-ttu-id="58cc7-208">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="58cc7-208">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="58cc7-209">[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="58cc7-209">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
[Spring Boot]: http://projects.spring.io/spring-boot/
<span data-ttu-id="58cc7-210">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="58cc7-210">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
[Spring Framework]: https://spring.io/
<span data-ttu-id="58cc7-211">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="58cc7-211">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span></span>

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
