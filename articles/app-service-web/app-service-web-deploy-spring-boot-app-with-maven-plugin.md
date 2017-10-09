---
title: "aaaHow toouse hello Maven du plug-in pour les applications Web Azure toodeploy un tooAzure d’application de démarrage du ressort"
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
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a><span data-ttu-id="edfd7-103">Comment toouse hello plug-in Maven pour les applications Web Azure toodeploy, un tooAzure d’application de démarrage du ressort</span><span class="sxs-lookup"><span data-stu-id="edfd7-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure</span></span>

<span data-ttu-id="edfd7-104">Hello [Maven les plug-in pour les applications Web Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) pour [Apache Maven](http://maven.apache.org/) permet une intégration transparente du Service d’application Azure dans des projets Maven et simplifie les processus hello pour les développeurs toodeploy web apps tooAzure du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="edfd7-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service.</span></span>

<span data-ttu-id="edfd7-105">Cet article montre comment utiliser hello plug-in Maven pour les applications Web Azure toodeploy un tooAzure d’application exemple ressort démarrage des Services d’application.</span><span class="sxs-lookup"><span data-stu-id="edfd7-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="edfd7-106">Hello Maven les plug-in pour les applications Web Azure est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="edfd7-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="edfd7-107">Pour l’instant, seule la publication FTP est pris en charge, bien que des fonctionnalités supplémentaires qui vont hello futures.</span><span class="sxs-lookup"><span data-stu-id="edfd7-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="edfd7-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="edfd7-108">Prerequisites</span></span>

<span data-ttu-id="edfd7-109">Commande toocomplete hello étapes décrites dans ce didacticiel, vous devez hello toohave suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="edfd7-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="edfd7-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="edfd7-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="edfd7-111">Hello [Azure Interface de ligne de commande (CLI)].</span><span class="sxs-lookup"><span data-stu-id="edfd7-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="edfd7-112">Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="edfd7-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="edfd7-113">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="edfd7-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="edfd7-114">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="edfd7-114">A [Git] client.</span></span>

## <a name="clone-hello-sample-spring-boot-web-app"></a><span data-ttu-id="edfd7-115">Clone hello exemple ressort démarrage d’application web</span><span class="sxs-lookup"><span data-stu-id="edfd7-115">Clone hello sample Spring Boot web app</span></span>

<span data-ttu-id="edfd7-116">Dans cette section, vous clonez une application Spring Boot terminée et vous la testez localement.</span><span class="sxs-lookup"><span data-stu-id="edfd7-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="edfd7-117">Ouvrez une invite de commandes ou d’une fenêtre de terminal et créer un répertoire local de toohold votre application de démarrage du ressort et remplacez le répertoire toothat ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="edfd7-117">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="edfd7-118">- ou -</span><span class="sxs-lookup"><span data-stu-id="edfd7-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="edfd7-119">Hello du clone [ressort démarrage prise en main] exemple de projet dans le répertoire hello créé ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="edfd7-119">Clone hello [Spring Boot Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="edfd7-120">Changer le projet toohello terminée Active ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="edfd7-120">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="edfd7-121">Générer le fichier JAR hello à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="edfd7-121">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="edfd7-122">Lorsque l’application hello web a été créée, démarrer l’application hello web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="edfd7-122">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="edfd7-123">Tester l’application web hello en parcourant tooit localement à l’aide d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="edfd7-123">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="edfd7-124">Par exemple, vous pouvez utiliser hello commande suivante si vous avez curl disponible :</span><span class="sxs-lookup"><span data-stu-id="edfd7-124">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="edfd7-125">Vous devez voir hello message suivant s’affiche : **Greetings de démarrage du ressort !**</span><span class="sxs-lookup"><span data-stu-id="edfd7-125">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="edfd7-126">Créer un principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="edfd7-126">Create an Azure service principal</span></span>

<span data-ttu-id="edfd7-127">Dans cette section, vous créez Azure principal du service qui hello utilise de plug-in Maven lors du déploiement de votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="edfd7-127">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="edfd7-128">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="edfd7-128">Open a command prompt.</span></span>

1. <span data-ttu-id="edfd7-129">Connectez-vous à votre compte Azure à l’aide de hello CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="edfd7-129">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="edfd7-130">Suivez hello instructions toocomplete hello processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="edfd7-130">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="edfd7-131">Créez un principal du service Azure :</span><span class="sxs-lookup"><span data-stu-id="edfd7-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="edfd7-132">Où `uuuuuuuu` est le nom d’utilisateur hello et `pppppppp` hello de mot de passe de principal du service hello.</span><span class="sxs-lookup"><span data-stu-id="edfd7-132">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="edfd7-133">Azure répond avec JSON qui ressemble à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="edfd7-133">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="edfd7-134">Vous allez utiliser les valeurs hello à partir de cette réponse JSON lorsque vous configurez hello Maven plug-in toodeploy votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="edfd7-134">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your web app tooAzure.</span></span> <span data-ttu-id="edfd7-135">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, et `tttttttt` sont des valeurs d’espace réservé, qui sont utilisées dans cet exemple toomake toomap plus facilement ces éléments de tootheir respectifs valeurs lorsque vous configurez votre Maven `settings.xml` fichier ensuite Bonjour section.</span><span class="sxs-lookup"><span data-stu-id="edfd7-135">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="edfd7-136">Configurer Maven toouse votre principal de service Azure</span><span class="sxs-lookup"><span data-stu-id="edfd7-136">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="edfd7-137">Dans cette section, vous utilisez les valeurs hello dans votre service Azure principal tooconfigure hello de l’authentification par Maven lors du déploiement de votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="edfd7-137">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="edfd7-138">Ouvrez votre Maven `settings.xml` de fichiers dans un éditeur de texte ; ce fichier peut être dans un chemin d’accès comme hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="edfd7-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="edfd7-139">Ajoutez vos paramètres de principal du service Azure à partir de la section précédente de hello de ce didacticiel toohello `<servers>` collection Bonjour *settings.xml* fichier ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="edfd7-139">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="edfd7-140">Où :</span><span class="sxs-lookup"><span data-stu-id="edfd7-140">Where:</span></span>
   <span data-ttu-id="edfd7-141">Élément</span><span class="sxs-lookup"><span data-stu-id="edfd7-141">Element</span></span> | <span data-ttu-id="edfd7-142">Description</span><span class="sxs-lookup"><span data-stu-id="edfd7-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="edfd7-143">Spécifie un nom unique qui Maven utilise toolook vos paramètres de sécurité lorsque vous déployez votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="edfd7-143">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="edfd7-144">Contient hello `appId` valeur à partir de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="edfd7-144">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="edfd7-145">Contient hello `tenant` valeur à partir de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="edfd7-145">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="edfd7-146">Contient hello `password` valeur à partir de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="edfd7-146">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="edfd7-147">Définit l’environnement de cloud computing Azure cible hello, qui est `AZURE` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="edfd7-147">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="edfd7-148">(Une liste complète des environnements est disponible dans hello [Maven les plug-in pour les applications Web Azure] documentation)</span><span class="sxs-lookup"><span data-stu-id="edfd7-148">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="edfd7-149">Enregistrez et fermez hello *settings.xml* fichier.</span><span class="sxs-lookup"><span data-stu-id="edfd7-149">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a><span data-ttu-id="edfd7-150">FACULTATIF : Personnaliser votre pom.xml avant de déployer votre tooAzure d’application web</span><span class="sxs-lookup"><span data-stu-id="edfd7-150">OPTIONAL: Customize your pom.xml before deploying your web app tooAzure</span></span>

<span data-ttu-id="edfd7-151">Ouvrez hello `pom.xml` de fichiers pour votre application de démarrage du ressort dans un éditeur de texte et recherchez hello `<plugin>` , élément pour `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="edfd7-151">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="edfd7-152">Cet élément doit ressembler à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="edfd7-152">This element should resemble hello following example:</span></span>

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
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="edfd7-153">Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in de hello Maven et une description détaillée de chacun de ces éléments est disponible dans hello [Maven les plug-in pour les applications Web Azure] documentation.</span><span class="sxs-lookup"><span data-stu-id="edfd7-153">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="edfd7-154">Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :</span><span class="sxs-lookup"><span data-stu-id="edfd7-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="edfd7-155">Élément</span><span class="sxs-lookup"><span data-stu-id="edfd7-155">Element</span></span> | <span data-ttu-id="edfd7-156">Description</span><span class="sxs-lookup"><span data-stu-id="edfd7-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="edfd7-157">Spécifie la version de hello de hello [Maven les plug-in pour les applications Web Azure].</span><span class="sxs-lookup"><span data-stu-id="edfd7-157">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="edfd7-158">Vous devez vérifier la version de hello répertoriée dans hello [référentiel Central Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que vous utilisez hello version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="edfd7-158">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="edfd7-159">Spécifie les informations d’authentification hello pour Azure, qui dans cet exemple contient un `<serverId>` élément contenant `azure-auth`; Maven utilise ce toolook valeur des valeurs de principal de service Azure hello dans votre Maven *settings.xml* fichier que vous avez définie dans une section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="edfd7-159">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="edfd7-160">Spécifie le groupe de ressources cible hello, qui est `maven-plugin` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="edfd7-160">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="edfd7-161">groupe de ressources Hello est créé au cours du déploiement, si elle n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="edfd7-161">hello resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="edfd7-162">Spécifie le nom de la cible hello pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="edfd7-162">Specifies hello target name for your web app.</span></span> <span data-ttu-id="edfd7-163">Dans cet exemple, le nom de la cible hello est `maven-web-app-${maven.build.timestamp}`, où hello `${maven.build.timestamp}` suffixe est ajouté dans ce conflit de tooavoid exemple.</span><span class="sxs-lookup"><span data-stu-id="edfd7-163">In this example, hello target name is `maven-web-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="edfd7-164">(vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application hello ; hello timestamp est facultative.)</span><span class="sxs-lookup"><span data-stu-id="edfd7-164">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="edfd7-165">Spécifie la région cible hello, qui, dans cet exemple est `westus`.</span><span class="sxs-lookup"><span data-stu-id="edfd7-165">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="edfd7-166">(Une liste complète est Bonjour [Maven les plug-in pour les applications Web Azure] documentation.)</span><span class="sxs-lookup"><span data-stu-id="edfd7-166">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="edfd7-167">Spécifie la version du runtime Java hello pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="edfd7-167">Specifies hello Java runtime version for your web app.</span></span> <span data-ttu-id="edfd7-168">(Une liste complète est Bonjour [Maven les plug-in pour les applications Web Azure] documentation.)</span><span class="sxs-lookup"><span data-stu-id="edfd7-168">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="edfd7-169">Spécifie le type de déploiement de votre application web.</span><span class="sxs-lookup"><span data-stu-id="edfd7-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="edfd7-170">Pour l’instant, seul `ftp` est pris en charge, bien que la prise en charge d’autres types de déploiement soit en cours de développement.</span><span class="sxs-lookup"><span data-stu-id="edfd7-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="edfd7-171">Spécifie les ressources et les destinations de cibles qui Maven utilise lors du déploiement de votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="edfd7-171">Specifies resources and target destinations which Maven uses when deploying your web app tooAzure.</span></span> <span data-ttu-id="edfd7-172">Dans cet exemple, deux `<resource>` éléments spécifient que Maven déploient des fichiers JAR de hello pour votre application web et le hello *web.config* fichier de projet de démarrage du ressort hello.</span><span class="sxs-lookup"><span data-stu-id="edfd7-172">In this example, two `<resource>` elements specify that Maven will deploy hello JAR file for your web app and hello *web.config* file from hello Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-tooazure"></a><span data-ttu-id="edfd7-173">Générer et déployer votre tooAzure d’application web</span><span class="sxs-lookup"><span data-stu-id="edfd7-173">Build and deploy your web app tooAzure</span></span>

<span data-ttu-id="edfd7-174">Une fois que vous avez configuré tous les paramètres de hello Bonjour précédant les sections de cet article, vous êtes prêt toodeploy votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="edfd7-174">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your web app tooAzure.</span></span> <span data-ttu-id="edfd7-175">toodo utilisez donc hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="edfd7-175">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="edfd7-176">À partir d’invite de commandes hello ou fenêtre de Terminal Server que vous utilisiez précédemment, régénérez le fichier JAR hello à l’aide de Maven si vous avez apporté les modifications de toohello *pom.xml* fichier ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="edfd7-176">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="edfd7-177">Déployer votre tooAzure d’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="edfd7-177">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="edfd7-178">Maven déploierez votre tooAzure d’application web ; Si l’application hello web n’existe pas déjà, il sera créé.</span><span class="sxs-lookup"><span data-stu-id="edfd7-178">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

<span data-ttu-id="edfd7-179">Lorsque votre site web a été déployée, vous serez en mesure de toomanage à l’aide de hello [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="edfd7-179">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="edfd7-180">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="edfd7-180">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="edfd7-182">Et hello URL pour votre application web s’afficheront dans hello **vue d’ensemble** pour votre application web :</span><span class="sxs-lookup"><span data-stu-id="edfd7-182">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="edfd7-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="edfd7-184">Next steps</span></span>

<span data-ttu-id="edfd7-185">Pour plus d’informations sur hello diverses technologies abordées dans cet article, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="edfd7-185">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="edfd7-186">[Maven les plug-in pour les applications Web Azure]</span><span class="sxs-lookup"><span data-stu-id="edfd7-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="edfd7-187">Connectez-vous à tooAzure de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="edfd7-187">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="edfd7-188">Comment toouse hello plug-in Maven pour les applications Web Azure toodeploy, un tooAzure d’application ressort démarrage en conteneur</span><span class="sxs-lookup"><span data-stu-id="edfd7-188">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="edfd7-189">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="edfd7-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="edfd7-190">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="edfd7-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Interface de ligne de commande (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[ressort démarrage prise en main]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven les plug-in pour les applications Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
