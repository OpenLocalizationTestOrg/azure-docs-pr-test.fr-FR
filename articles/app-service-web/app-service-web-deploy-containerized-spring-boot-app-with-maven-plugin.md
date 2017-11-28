---
title: "aaaHow toouse hello Maven du plug-in pour les applications Web Azure toodeploy un tooAzure application de démarrage du ressort en conteneur"
description: "Découvrez comment toouse hello plug-in Maven pour les applications Web Azure toodeploy, un tooAzure d’application de démarrage du ressort."
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
ms.openlocfilehash: e7e760d4ef5bd4c92a4126a50a2b12e5c8f2b4a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a><span data-ttu-id="cb6e5-103">Comment toouse hello plug-in Maven pour les applications Web Azure toodeploy, un tooAzure d’application ressort démarrage en conteneur</span><span class="sxs-lookup"><span data-stu-id="cb6e5-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>

<span data-ttu-id="cb6e5-104">Hello [Maven les plug-in pour les applications Web Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) pour [Apache Maven](http://maven.apache.org/) permet une intégration transparente du Service d’application Azure dans des projets Maven et simplifie les processus hello pour les développeurs toodeploy web apps tooAzure du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service .</span></span>

<span data-ttu-id="cb6e5-105">Cet article illustre l’utilisation de hello Maven du plug-in pour les applications Web Azure toodeploy un exemple d’application de démarrage du ressort dans un tooAzure de conteneur Docker des Services d’application.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application in a Docker container tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cb6e5-106">Hello Maven les plug-in pour les applications Web Azure est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="cb6e5-107">Pour l’instant, seule la publication FTP est pris en charge, bien que des fonctionnalités supplémentaires qui vont hello futures.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="cb6e5-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cb6e5-108">Prerequisites</span></span>

<span data-ttu-id="cb6e5-109">Commande toocomplete hello étapes décrites dans ce didacticiel, vous devez hello toohave suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="cb6e5-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="cb6e5-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="cb6e5-111">Hello [Azure Interface de ligne de commande (CLI)].</span><span class="sxs-lookup"><span data-stu-id="cb6e5-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="cb6e5-112">Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="cb6e5-113">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="cb6e5-114">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="cb6e5-114">A [Git] client.</span></span>
* <span data-ttu-id="cb6e5-115">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="cb6e5-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cb6e5-116">En raison des exigences de la virtualisation toohello de ce didacticiel, vous ne peut pas suivre les étapes de hello dans cet article sur un ordinateur virtuel ; Vous devez utiliser un ordinateur physique avec les fonctionnalités de virtualisation activées.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="cb6e5-117">Cloner l’exemple hello ressort démarrage sur l’application web de Docker</span><span class="sxs-lookup"><span data-stu-id="cb6e5-117">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="cb6e5-118">Dans cette section, vous clonez une application Spring Boot en conteneur et vous la testez localement.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="cb6e5-119">Ouvrez une invite de commandes ou d’une fenêtre de terminal et créer un répertoire local de toohold votre application de démarrage du ressort et remplacez le répertoire toothat ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-119">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="cb6e5-120">- ou -</span><span class="sxs-lookup"><span data-stu-id="cb6e5-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="cb6e5-121">Hello du clone [démarrage ressort sur Docker mise en route] exemple de projet dans le répertoire hello créé ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="cb6e5-122">Changer le projet toohello terminée Active ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-122">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="cb6e5-123">Générer le fichier JAR hello à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-123">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="cb6e5-124">Lorsque l’application hello web a été créée, démarrer l’application hello web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-124">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="cb6e5-125">Tester l’application web hello en parcourant tooit localement à l’aide d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="cb6e5-126">Par exemple, vous pouvez utiliser hello commande suivante si vous avez curl disponible :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-126">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="cb6e5-127">Vous devez voir hello message suivant s’affiche : **Hello World de Docker**</span><span class="sxs-lookup"><span data-stu-id="cb6e5-127">You should see hello following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="cb6e5-128">Créer un principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="cb6e5-128">Create an Azure service principal</span></span>

<span data-ttu-id="cb6e5-129">Dans cette section, vous créez Azure principal du service qui hello utilise de plug-in Maven lors du déploiement de votre tooAzure de conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-129">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="cb6e5-130">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-130">Open a command prompt.</span></span>

1. <span data-ttu-id="cb6e5-131">Connectez-vous à votre compte Azure à l’aide de hello CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-131">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="cb6e5-132">Suivez hello instructions toocomplete hello processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-132">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="cb6e5-133">Créez un principal du service Azure :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="cb6e5-134">Où `uuuuuuuu` est le nom d’utilisateur hello et `pppppppp` hello de mot de passe de principal du service hello.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-134">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="cb6e5-135">Azure répond avec JSON qui ressemble à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-135">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="cb6e5-136">Vous allez utiliser les valeurs de hello à partir de cette réponse JSON lorsque vous configurez hello Maven plug-in toodeploy tooAzure de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-136">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="cb6e5-137">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, et `tttttttt` sont des valeurs d’espace réservé, qui sont utilisées dans cet exemple toomake toomap plus facilement ces éléments de tootheir respectifs valeurs lorsque vous configurez votre Maven `settings.xml` fichier ensuite Bonjour section.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-137">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="cb6e5-138">Configurer Maven toouse votre principal de service Azure</span><span class="sxs-lookup"><span data-stu-id="cb6e5-138">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="cb6e5-139">Dans cette section, vous utilisez les valeurs hello à partir de votre authentification service Azure principal tooconfigure hello Maven utilisera lors du déploiement de votre tooAzure de conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-139">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven will use when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="cb6e5-140">Ouvrez votre Maven `settings.xml` de fichiers dans un éditeur de texte ; ce fichier peut être dans un chemin d’accès comme hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="cb6e5-141">Ajoutez vos paramètres de principal du service Azure à partir de la section précédente de hello de ce didacticiel toohello `<servers>` collection Bonjour *settings.xml* fichier ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-141">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="cb6e5-142">Où :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-142">Where:</span></span>
   <span data-ttu-id="cb6e5-143">Élément</span><span class="sxs-lookup"><span data-stu-id="cb6e5-143">Element</span></span> | <span data-ttu-id="cb6e5-144">Description</span><span class="sxs-lookup"><span data-stu-id="cb6e5-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="cb6e5-145">Spécifie un nom unique qui Maven utilise toolook vos paramètres de sécurité lorsque vous déployez votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-145">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="cb6e5-146">Contient hello `appId` valeur à partir de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-146">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="cb6e5-147">Contient hello `tenant` valeur à partir de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-147">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="cb6e5-148">Contient hello `password` valeur à partir de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-148">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="cb6e5-149">Définit l’environnement de cloud computing Azure cible hello, qui est `AZURE` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-149">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="cb6e5-150">(Une liste complète des environnements est disponible dans hello [Maven les plug-in pour les applications Web Azure] documentation)</span><span class="sxs-lookup"><span data-stu-id="cb6e5-150">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="cb6e5-151">Enregistrez et fermez hello *settings.xml* fichier.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-151">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a><span data-ttu-id="cb6e5-152">FACULTATIF : Déployer votre tooDocker de fichier local Docker Hub</span><span class="sxs-lookup"><span data-stu-id="cb6e5-152">OPTIONAL: Deploy your local Docker file tooDocker Hub</span></span>

<span data-ttu-id="cb6e5-153">Si vous avez un compte de Docker, vous pouvez générer votre Docker image de conteneur localement et poussez-le tooDocker Hub.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-153">If you have a Docker account, you can build your Docker container image locally and push it tooDocker Hub.</span></span> <span data-ttu-id="cb6e5-154">toodo utilisez donc hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-154">toodo so, use hello following steps.</span></span>

1. <span data-ttu-id="cb6e5-155">Ouvrez hello `pom.xml` fichier de votre application de démarrage du ressort dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-155">Open hello `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="cb6e5-156">Recherchez hello `<imageName>` élément enfant de hello `<containerSettings>` élément.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-156">Locate hello `<imageName>` child element of hello `<containerSettings>` element.</span></span>

1. <span data-ttu-id="cb6e5-157">Hello de mise à jour `${docker.image.prefix}` valeur avec le nom de votre compte de Docker :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-157">Update hello `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="cb6e5-158">Choisissez une des hello les méthodes de déploiement suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-158">Choose one of hello following deployment methods:</span></span>

   * <span data-ttu-id="cb6e5-159">Générez votre image de conteneur localement avec Maven et utilisez Docker toopush votre tooDocker conteneur Hub :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-159">Build your container image locally with Maven, and then use Docker toopush your container tooDocker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="cb6e5-160">Si vous avez hello [plug-in de Docker pour Maven] installé, vous pouvez générer automatiquement et votre tooDocker d’image de conteneur concentrateur à l’aide de hello `-DpushImage` paramètre :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-160">If you have hello [Docker plugin for Maven] installed, you can automatically build and your container image tooDocker Hub by using hello `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a><span data-ttu-id="cb6e5-161">FACULTATIF : Personnaliser votre pom.xml avant de déployer votre tooAzure de conteneur</span><span class="sxs-lookup"><span data-stu-id="cb6e5-161">OPTIONAL: Customize your pom.xml before deploying your container tooAzure</span></span>

<span data-ttu-id="cb6e5-162">Ouvrez hello `pom.xml` de fichiers pour votre application de démarrage du ressort dans un éditeur de texte et recherchez hello `<plugin>` , élément pour `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-162">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="cb6e5-163">Cet élément doit ressembler à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-163">This element should resemble hello following example:</span></span>

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

<span data-ttu-id="cb6e5-164">Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in de hello Maven et une description détaillée de chacun de ces éléments est disponible dans hello [Maven les plug-in pour les applications Web Azure] documentation.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-164">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="cb6e5-165">Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="cb6e5-166">Élément</span><span class="sxs-lookup"><span data-stu-id="cb6e5-166">Element</span></span> | <span data-ttu-id="cb6e5-167">Description</span><span class="sxs-lookup"><span data-stu-id="cb6e5-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="cb6e5-168">Spécifie la version de hello de hello [Maven les plug-in pour les applications Web Azure].</span><span class="sxs-lookup"><span data-stu-id="cb6e5-168">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="cb6e5-169">Vous devez vérifier la version de hello répertoriée dans hello [référentiel Central Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que vous utilisez hello version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-169">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="cb6e5-170">Spécifie les informations d’authentification hello pour Azure, qui dans cet exemple contient un `<serverId>` élément contenant `azure-auth`; Maven utilise ce toolook valeur des valeurs de principal de service Azure hello dans votre Maven *settings.xml* fichier que vous avez définie dans une section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-170">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="cb6e5-171">Spécifie le groupe de ressources cible hello, qui est `maven-plugin` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-171">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="cb6e5-172">groupe de ressources Hello sera créé au cours du déploiement s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-172">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="cb6e5-173">Spécifie le nom de la cible hello pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-173">Specifies hello target name for your web app.</span></span> <span data-ttu-id="cb6e5-174">Dans cet exemple, le nom de la cible hello est `maven-linux-app-${maven.build.timestamp}`, où hello `${maven.build.timestamp}` suffixe est ajouté dans ce conflit de tooavoid exemple.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-174">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="cb6e5-175">(vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application hello ; hello timestamp est facultative.)</span><span class="sxs-lookup"><span data-stu-id="cb6e5-175">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="cb6e5-176">Spécifie la région cible hello, qui, dans cet exemple est `westus`.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-176">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="cb6e5-177">(Une liste complète est Bonjour [Maven les plug-in pour les applications Web Azure] documentation.)</span><span class="sxs-lookup"><span data-stu-id="cb6e5-177">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="cb6e5-178">Spécifie des paramètres uniques pour Maven toouse lors du déploiement de votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-178">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="cb6e5-179">Dans cet exemple, un `<property>` élément contient une paire nom/valeur des éléments enfants qui spécifient le port hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-179">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cb6e5-180">numéro de port Hello paramètres toochange hello dans cet exemple ne sont nécessaires lorsque vous modifiez le port de hello à partir de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-180">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

## <a name="build-and-deploy-your-container-tooazure"></a><span data-ttu-id="cb6e5-181">Générer et déployer votre tooAzure de conteneur</span><span class="sxs-lookup"><span data-stu-id="cb6e5-181">Build and deploy your container tooAzure</span></span>

<span data-ttu-id="cb6e5-182">Une fois que vous avez configuré tous les paramètres de hello Bonjour précédant les sections de cet article, vous êtes prêt toodeploy tooAzure de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-182">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your container tooAzure.</span></span> <span data-ttu-id="cb6e5-183">toodo utilisez donc hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-183">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="cb6e5-184">À partir d’invite de commandes hello ou fenêtre de Terminal Server que vous utilisiez précédemment, régénérez le fichier JAR hello à l’aide de Maven si vous avez apporté les modifications de toohello *pom.xml* fichier ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-184">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="cb6e5-185">Déployer votre tooAzure d’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-185">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="cb6e5-186">Maven déploierez votre tooAzure d’application web ; Si l’application hello web n’existe pas déjà, il sera créé.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-186">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cb6e5-187">Si la région hello que vous spécifiez dans hello `<region>` élément de votre *pom.xml* fichier n’a pas suffisamment de serveurs disponibles lorsque vous démarrez votre déploiement, vous pouvez voir un toohello similaire erreur l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-187">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
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
> <span data-ttu-id="cb6e5-188">Si cela se produit, vous pouvez spécifier qu'une autre région et exécutez de nouveau hello Maven commande toodeploy votre application.</span><span class="sxs-lookup"><span data-stu-id="cb6e5-188">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="cb6e5-189">Lorsque votre site web a été déployée, vous serez en mesure de toomanage à l’aide de hello [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="cb6e5-189">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="cb6e5-190">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-190">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="cb6e5-192">Et hello URL pour votre application web s’afficheront dans hello **vue d’ensemble** pour votre application web :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-192">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Détermination des URL hello pour votre application web][AP02]

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

## <a name="next-steps"></a><span data-ttu-id="cb6e5-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cb6e5-194">Next steps</span></span>

<span data-ttu-id="cb6e5-195">Pour plus d’informations sur hello diverses technologies abordées dans cet article, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="cb6e5-195">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="cb6e5-196">[Maven les plug-in pour les applications Web Azure]</span><span class="sxs-lookup"><span data-stu-id="cb6e5-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="cb6e5-197">Connectez-vous à tooAzure de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="cb6e5-197">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="cb6e5-198">Comment toouse hello plug-in Maven pour les applications Web Azure toodeploy, un tooAzure d’application ressort démarrage du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="cb6e5-198">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="cb6e5-199">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cb6e5-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="cb6e5-200">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="cb6e5-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="cb6e5-201">[plug-in de Docker pour Maven]</span><span class="sxs-lookup"><span data-stu-id="cb6e5-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure Interface de ligne de commande (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[client Docker]: https://www.docker.com/
[plug-in de Docker pour Maven]: https://github.com/spotify/docker-maven-plugin
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[démarrage ressort sur Docker mise en route]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Maven les plug-in pour les applications Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
