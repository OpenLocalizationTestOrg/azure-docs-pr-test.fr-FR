---
title: "aaaDeploy un toohello d’Application de démarrage du ressort du Service d’applications Azure | Documents Microsoft"
description: "Ce didacticiel vous guide les développeurs via hello étapes toodeploy hello ressort démarrage route web application tooAzure du Service d’applications."
services: app-service\web
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
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a><span data-ttu-id="779f0-103">Déployer un toohello ressort démarrage Application Azure App Service</span><span class="sxs-lookup"><span data-stu-id="779f0-103">Deploy a Spring Boot Application toohello Azure App Service</span></span>

<span data-ttu-id="779f0-104">Hello  **[Spring Framework]**  une solution open source qui permet aux développeurs Java de créer des applications d’entreprise, et l’autre des projets courants de plus de hello qui s’appuie sur cette plateforme [Ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="779f0-104">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="779f0-105">Ce didacticiel vous aidera à cependant création exemple hello ressort démarrage prise en main d’application web et les déployer trop[Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="779f0-105">This tutorial will walk you though creating hello sample Spring Boot Getting Started web app and deploying it too[Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="779f0-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="779f0-106">Prerequisites</span></span>

<span data-ttu-id="779f0-107">Dans l’ordre toocomplete hello étapes décrites dans ce didacticiel, vous toohave hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="779f0-107">In order toocomplete hello steps in this tutorial, you need toohave hello following:</span></span>

* <span data-ttu-id="779f0-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="779f0-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="779f0-109">Un [JDK (Java Developer Kit)] à jour.</span><span class="sxs-lookup"><span data-stu-id="779f0-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="779f0-110">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="779f0-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="779f0-111">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="779f0-111">A [Git] client.</span></span>

## <a name="create-hello-spring-boot-getting-started-web-app"></a><span data-ttu-id="779f0-112">Créer hello ressort démarrage prise en main de l’application web</span><span class="sxs-lookup"><span data-stu-id="779f0-112">Create hello Spring Boot Getting Started web app</span></span>

<span data-ttu-id="779f0-113">Hello étapes suivantes vous guidera à travers les étapes de hello toocreate requis une application web de démarrage du ressort simple et de le tester localement.</span><span class="sxs-lookup"><span data-stu-id="779f0-113">hello following steps will walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="779f0-114">Ouvrez une invite de commandes et créer un répertoire local de toohold votre application, puis accédez au répertoire toothat ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="779f0-114">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="779f0-115">- ou -</span><span class="sxs-lookup"><span data-stu-id="779f0-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="779f0-116">Hello du clone [ressort démarrage prise en main] exemple de projet dans l’annuaire hello vous venez de créer ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="779f0-116">Clone hello [Spring Boot Getting Started] sample project into hello directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="779f0-117">Changer le projet toohello terminée Active ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="779f0-117">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="779f0-118">Générer le fichier JAR hello à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="779f0-118">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="779f0-119">Une fois que l’application hello web a été créée, modifiez le fichier JAR de toohello active et démarrer l’application hello web ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="779f0-119">Once hello web app has been created, change directory toohello JAR file and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="779f0-120">Tester l’application web hello en parcourant toohttp://localhost:8080 à l’aide d’un navigateur web, ou utilisez la syntaxe hello comme hello l’exemple suivant, si vous avez curl disponible :</span><span class="sxs-lookup"><span data-stu-id="779f0-120">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="779f0-121">Vous devez voir hello message suivant s’affiche : **Greetings de démarrage du ressort !**</span><span class="sxs-lookup"><span data-stu-id="779f0-121">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Parcourir l’exemple d’application][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="779f0-123">Créer une application web Azure à utiliser avec Java</span><span class="sxs-lookup"><span data-stu-id="779f0-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="779f0-124">Hello suit sera vous guident tout hello étapes toocreate une application Web Azure, configurer les paramètres requis de hello pour Java et configurer vos informations d’identification FTP.</span><span class="sxs-lookup"><span data-stu-id="779f0-124">hello following steps will walk you through hello steps toocreate an Azure Web App, configure hello required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="779f0-125">Parcourir toohello [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="779f0-125">Browse toohello [Azure portal] and log in.</span></span>

1. <span data-ttu-id="779f0-126">Une fois que vous êtes connecté à votre compte sur hello portail Azure, cliquez sur icône du menu hello pour **des Services d’application**:</span><span class="sxs-lookup"><span data-stu-id="779f0-126">Once you have logged into your account on hello Azure portal, click hello menu icon for **App Services**:</span></span>
   
   ![Portail Azure][AZ01]

1. <span data-ttu-id="779f0-128">Hello lorsque **des Services d’application** page s’affiche, cliquez sur **+ ajouter** toocreate un nouveau Service d’application.</span><span class="sxs-lookup"><span data-stu-id="779f0-128">When hello **App Services** page is displayed, click **+ Add** toocreate a new App Service.</span></span>

   ![Créer un App Service][AZ02]

1. <span data-ttu-id="779f0-130">Lors de la liste de hello des modèles d’application web s’affiche, cliquez sur lien hello hello base l’application Web Microsoft.</span><span class="sxs-lookup"><span data-stu-id="779f0-130">When hello list of web app templates is displayed, click hello link for hello basic Microsoft Web App.</span></span>

   ![Modèles d’application web][AZ03]

1. <span data-ttu-id="779f0-132">Lorsque la page d’informations hello pour le modèle d’application Web hello s’affiche, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="779f0-132">When hello information page for hello Web App template is displayed, click **Create**.</span></span>

   ![Créer une application web][AZ04]

1. <span data-ttu-id="779f0-134">Indiquez un nom unique pour votre application web et spécifiez les éventuels paramètres supplémentaires, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="779f0-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Créer les paramètres d’une application web][AZ05]

1. <span data-ttu-id="779f0-136">Une fois que votre application web a été créée, cliquez sur icône du menu hello pour **des Services d’application**, puis cliquez sur votre application web de nouvellement créé :</span><span class="sxs-lookup"><span data-stu-id="779f0-136">Once your web app has been created, click hello menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Répertorier les applications web][AZ06]

1. <span data-ttu-id="779f0-138">Lorsque votre application web s’affiche, spécifiez une version Java hello à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="779f0-138">When your web app is displayed, specify hello Java version by using hello following steps:</span></span>

   <span data-ttu-id="779f0-139">a.</span><span class="sxs-lookup"><span data-stu-id="779f0-139">a.</span></span> <span data-ttu-id="779f0-140">Cliquez sur hello **paramètres de l’Application** élément de menu.</span><span class="sxs-lookup"><span data-stu-id="779f0-140">Click hello **Application Settings** menu item.</span></span>

   <span data-ttu-id="779f0-141">b.</span><span class="sxs-lookup"><span data-stu-id="779f0-141">b.</span></span> <span data-ttu-id="779f0-142">Choisissez **Java 8** pour une version Java hello.</span><span class="sxs-lookup"><span data-stu-id="779f0-142">Choose **Java 8** for hello Java version.</span></span>

   <span data-ttu-id="779f0-143">c.</span><span class="sxs-lookup"><span data-stu-id="779f0-143">c.</span></span> <span data-ttu-id="779f0-144">Choisissez **plus récent** pour la version de Java secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="779f0-144">Choose **Newest** for hello minor Java version.</span></span>

   <span data-ttu-id="779f0-145">d.</span><span class="sxs-lookup"><span data-stu-id="779f0-145">d.</span></span> <span data-ttu-id="779f0-146">Choisissez **les plus récents Tomcat 8.5** pour le conteneur de hello web.</span><span class="sxs-lookup"><span data-stu-id="779f0-146">Choose **Newest Tomcat 8.5** for hello web container.</span></span> <span data-ttu-id="779f0-147">(Ce conteneur n'est pas réellement utilisé ; Azure utilise conteneur hello à partir de votre application de démarrage du ressort.)</span><span class="sxs-lookup"><span data-stu-id="779f0-147">(This container will not actually be used; Azure will use hello container from your Spring Boot application.)</span></span>

   <span data-ttu-id="779f0-148">e.</span><span class="sxs-lookup"><span data-stu-id="779f0-148">e.</span></span> <span data-ttu-id="779f0-149">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="779f0-149">Click **Save**.</span></span>

   ![Paramètres de l’application][AZ07]

1. <span data-ttu-id="779f0-151">Spécifier vos informations d’identification de déploiement FTP à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="779f0-151">Specify your FTP deployment credentials by using hello following steps:</span></span>

   <span data-ttu-id="779f0-152">a.</span><span class="sxs-lookup"><span data-stu-id="779f0-152">a.</span></span> <span data-ttu-id="779f0-153">Cliquez sur hello **informations d’identification de déploiement** élément de menu.</span><span class="sxs-lookup"><span data-stu-id="779f0-153">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="779f0-154">b.</span><span class="sxs-lookup"><span data-stu-id="779f0-154">b.</span></span> <span data-ttu-id="779f0-155">Spécifiez votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="779f0-155">Specify your username and password.</span></span>

   <span data-ttu-id="779f0-156">c.</span><span class="sxs-lookup"><span data-stu-id="779f0-156">c.</span></span> <span data-ttu-id="779f0-157">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="779f0-157">Click **Save**.</span></span>

   ![Spécifier les informations d’identification de déploiement][AZ08]

1. <span data-ttu-id="779f0-159">Récupérer les informations de connexion FTP à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="779f0-159">Retrieve your FTP connection information by using hello following steps:</span></span>

   <span data-ttu-id="779f0-160">a.</span><span class="sxs-lookup"><span data-stu-id="779f0-160">a.</span></span> <span data-ttu-id="779f0-161">Cliquez sur hello **informations d’identification de déploiement** élément de menu.</span><span class="sxs-lookup"><span data-stu-id="779f0-161">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="779f0-162">b.</span><span class="sxs-lookup"><span data-stu-id="779f0-162">b.</span></span> <span data-ttu-id="779f0-163">Copiez vos nom d’utilisateur complet de FTP et les URL et les enregistrer pour la section suivante de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="779f0-163">Copy your full FTP username and URL and save them for hello next section of this tutorial.</span></span>

   ![URL et informations d’identification FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a><span data-ttu-id="779f0-165">Déployer votre tooAzure d’application de web ressort démarrage</span><span class="sxs-lookup"><span data-stu-id="779f0-165">Deploy your Spring Boot web app tooAzure</span></span>

<span data-ttu-id="779f0-166">Hello suit vous guidera hello étapes toodeploy votre tooAzure d’application de web ressort démarrage.</span><span class="sxs-lookup"><span data-stu-id="779f0-166">hello following steps will walk you through hello steps toodeploy your Spring Boot web app tooAzure.</span></span>

1. <span data-ttu-id="779f0-167">Ouvrez un éditeur de texte tel que le bloc-notes de Windows et collez hello après le texte dans un nouveau document, puis enregistrer le fichier hello sous *web.config*:</span><span class="sxs-lookup"><span data-stu-id="779f0-167">Open a text editor such as Windows Notepad and paste hello following text into a new document, then save hello file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="779f0-168">Après avoir enregistré hello *web.config* tooyour système de fichiers, connecter tooyour l’application web via FTP à l’aide des URL de hello, nom d’utilisateur et mot de passe de hello précédant la section de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="779f0-168">After you have saved hello *web.config* file tooyour system, connect tooyour web app via FTP using hello URL, username, and password from hello preceding section of this tutorial.</span></span> <span data-ttu-id="779f0-169">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="779f0-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="779f0-170">Modification hello répertoire distant toohello dossier racine de votre application web, (qui est à */site/wwwroot*), puis copiez le fichier JAR hello à partir de votre application de démarrage du ressort et hello *web.config* précédemment.</span><span class="sxs-lookup"><span data-stu-id="779f0-170">Change hello remote directory toohello root folder of your web app, (which is at */site/wwwroot*), then copy hello JAR file from your Spring Boot application and hello *web.config* from earlier.</span></span> <span data-ttu-id="779f0-171">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="779f0-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="779f0-172">Après avoir déployé votre JAR et *web.config* fichiers tooyour web app, vous devez toorestart votre application web à l’aide de hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="779f0-172">After you have deployed your JAR and *web.config* files tooyour web app, you need toorestart your web app using hello Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="779f0-173">Tester l’application web hello en parcourant les URL de l’application tooyour web à l’aide d’un navigateur web, ou utilisez la syntaxe hello comme hello l’exemple suivant, si vous avez curl disponible :</span><span class="sxs-lookup"><span data-stu-id="779f0-173">Test hello web app by browsing tooyour web app's URL using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="779f0-174">Vous devez voir hello message suivant s’affiche : **Greetings de démarrage du ressort !**</span><span class="sxs-lookup"><span data-stu-id="779f0-174">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Parcourir l’exemple d’application][SB02]

## <a name="next-steps"></a><span data-ttu-id="779f0-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="779f0-176">Next steps</span></span>

<span data-ttu-id="779f0-177">Pour plus d’informations sur l’utilisation des applications de démarrage du ressort sur Azure, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="779f0-177">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="779f0-178">Déployer une Application de démarrage ressort sur Linux Bonjour Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="779f0-178">Deploy a Spring Boot Application on Linux in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="779f0-179">Déployer une Application de démarrage ressort sur un Kubernetes Cluster Bonjour Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="779f0-179">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="779f0-180">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="779f0-180">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="779f0-181">Pour plus d’informations sur les tooAzure d’applications web depoying à l’aide de FTP, consultez [déployer votre tooAzure d’application du Service d’applications à l’aide de FTP/S].</span><span class="sxs-lookup"><span data-stu-id="779f0-181">For additional information about depoying web apps tooAzure using FTP, see [Deploy your app tooAzure App Service using FTP/S].</span></span>

<span data-ttu-id="779f0-182">Pour plus d’informations sur l’exemple de projet de démarrage du ressort hello, consultez [ressort démarrage prise en main].</span><span class="sxs-lookup"><span data-stu-id="779f0-182">For further details about hello Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="779f0-183">Pour avec prise en main de vos propres applications ressort démarrage, consultez hello **ressort Initializr** à https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="779f0-183">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="779f0-184">Pour plus d’informations sur la configuration de paramètres supplémentaires pour votre application web, consultez [Configurer des applications web dans Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="779f0-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[Configurer des applications web dans Azure App Service]: /azure/app-service-web/web-sites-configure
[déployer votre tooAzure d’application du Service d’applications à l’aide de FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Ressort démarrage]: http://projects.spring.io/spring-boot/
[ressort démarrage prise en main]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
