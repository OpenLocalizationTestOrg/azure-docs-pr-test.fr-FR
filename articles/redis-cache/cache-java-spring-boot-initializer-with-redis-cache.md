---
title: "aaaHow tooconfigure un toouse d’application ressort initialisation initialiseur du Cache Redis"
description: "Découvrez comment tooconfigure une application de démarrage du ressort créé avec hello ressort Initializr toouse Cache Redis Azure."
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Redis Cache
ms.assetid: 
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 7/21/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ad532c88d2d67b97079eeb0e0e392add29ac365b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a><span data-ttu-id="41930-104">Comment tooconfigure un toouse d’application ressort initialisation initialiseur du Cache Redis</span><span class="sxs-lookup"><span data-stu-id="41930-104">How tooconfigure a Spring Boot Initializer app toouse Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="41930-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="41930-105">Overview</span></span>

<span data-ttu-id="41930-106">Hello  **[Spring Framework]**  est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="41930-106">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="41930-107">Un des projets de plus-populaires hello qui est créé de plateforme est [ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="41930-107">One of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="41930-108">les développeurs de toohelp prise en main du ressort démarrage, plusieurs exemples de packages de démarrage du ressort sont disponibles à <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="41930-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="41930-109">En outre toochoosing à partir de la liste de hello de démarrage de la base de projets, hello  **[ressort Initializr]**  permet aux développeurs de commencer à créer des applications personnalisées ressort démarrage.</span><span class="sxs-lookup"><span data-stu-id="41930-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="41930-110">Cet article vous guide dans la création d’un cache Redis à l’aide de hello portail Azure, puis à l’aide de hello **ressort Initializr** toocreate une application personnalisée, puis en créant un Java web application qui stocke et récupère des données à l’aide de votre Cache redis.</span><span class="sxs-lookup"><span data-stu-id="41930-110">This article walks you through creating a Redis cache using hello Azure portal, then using hello **Spring Initializr** toocreate a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41930-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="41930-111">Prerequisites</span></span>

<span data-ttu-id="41930-112">Hello, suivant les conditions préalables est requises dans l’ordre toofollow hello étapes décrites dans cet article :</span><span class="sxs-lookup"><span data-stu-id="41930-112">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="41930-113">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="41930-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="41930-114">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="41930-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="41930-115">[Apache Maven](http://maven.apache.org/) version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="41930-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="41930-116">Créer un Cache Redis sur Azure</span><span class="sxs-lookup"><span data-stu-id="41930-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="41930-117">Parcourir toohello Azure portail à <https://portal.azure.com/> et cliquez sur l’élément hello pour **+ nouveau**.</span><span class="sxs-lookup"><span data-stu-id="41930-117">Browse toohello Azure portal at <https://portal.azure.com/> and click hello item for **+New**.</span></span>

   ![Portail Azure][AZ01]

1. <span data-ttu-id="41930-119">Cliquez sur **Base de données**, puis sur **Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="41930-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Portail Azure][AZ02]

1. <span data-ttu-id="41930-121">Sur hello **nouveau Cache Redis** , entrez hello **nom DNS** pour votre cache, puis spécifiez votre **abonnement**, **groupe de ressources**,  **Emplacement**, et **niveau tarifaire**.</span><span class="sxs-lookup"><span data-stu-id="41930-121">On hello **New Redis Cache** page, enter hello **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="41930-122">Lorsque vous avez défini ces options, cliquez sur **créer** toocreate votre cache.</span><span class="sxs-lookup"><span data-stu-id="41930-122">When you have specified these options, click **Create** toocreate your cache.</span></span>

   ![Portail Azure][AZ03]

1. <span data-ttu-id="41930-124">Une fois que votre cache est terminé, vous verrez répertorié sur votre Azure **tableau de bord**, ainsi que sous hello **toutes les ressources**, et **les Caches Redis** pages.</span><span class="sxs-lookup"><span data-stu-id="41930-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under hello **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="41930-125">Vous pouvez cliquer sur votre cache sur n’importe quel ces emplacements tooopen hello page des propriétés pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="41930-125">You can click on your cache on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Portail Azure][AZ04]

1. <span data-ttu-id="41930-127">Lorsque la page hello qui contient la liste hello des propriétés pour votre cache s’affiche, cliquez sur **clés d’accès** et copiez vos clés d’accès pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="41930-127">When hello page which contains hello list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Portail Azure][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a><span data-ttu-id="41930-129">Créer une application personnalisée à l’aide de hello ressort Initializr</span><span class="sxs-lookup"><span data-stu-id="41930-129">Create a custom application using hello Spring Initializr</span></span>

1. <span data-ttu-id="41930-130">Parcourir trop<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="41930-130">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="41930-131">Spécifiez que vous souhaitez toogenerate un **Maven** projet avec **Java**, entrez hello **groupe** et **Aritifact** noms pour votre application, puis cliquez sur le lien de hello trop**version complète de commutateur toohello** Hello ressort Initializr.</span><span class="sxs-lookup"><span data-stu-id="41930-131">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Aritifact** names for your application, and then click hello link too**Switch toohello full version** of hello Spring Initializr.</span></span>

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="41930-133">Hello ressort Initializr utilisera hello **groupe** et **Aritifact** nom du package hello noms toocreate ; par exemple : *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="41930-133">hello Spring Initializr will use hello **Group** and **Aritifact** names toocreate hello package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="41930-134">Défilement vers le bas toohello **Web** section et hello la case pour **Web**, puis faites défiler vers le bas toohello **NoSQL** section et hello la case pour **Redis**, faites défiler vers le bas toohello de page de hello et cliquez sur le bouton de hello trop**générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="41930-134">Scroll down toohello **Web** section and check hello box for **Web**, then scroll down toohello **NoSQL** section and check hello box for **Redis**, then scroll toohello bottom of hello page and click hello button too**Generate Project**.</span></span>

   ![Options complètes de Spring Initializr][SI02]

1. <span data-ttu-id="41930-136">Lorsque vous y êtes invité, téléchargez hello projet tooa chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="41930-136">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Télécharger un projet Spring Boot personnalisé][SI03]

1. <span data-ttu-id="41930-138">Une fois que vous avez extrait les fichiers hello sur votre système local, votre application de démarrage du ressort personnalisée sera prête pour la modification.</span><span class="sxs-lookup"><span data-stu-id="41930-138">After you have extracted hello files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Fichiers de projet Spring Boot personnalisé][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a><span data-ttu-id="41930-140">Configurer votre toouse ressort démarrage personnalisée à votre Cache Redis</span><span class="sxs-lookup"><span data-stu-id="41930-140">Configure your custom Spring Boot toouse your Redis Cache</span></span>

1. <span data-ttu-id="41930-141">Recherchez hello *application.properties* fichier Bonjour *ressources* répertoire de votre application, ou créez le fichier de hello si elle n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="41930-141">Locate hello *application.properties* file in hello *resources* directory of your app, or create hello file if it does not already exist.</span></span>

   ![Recherchez le fichier de application.properties hello][RE01]

1. <span data-ttu-id="41930-143">Ouvrez hello *application.properties* de fichiers dans un éditeur de texte, ajouter hello lignes toohello fichier suivant et remplacer des valeurs d’exemple hello avec les propriétés appropriées de hello à partir de votre cache :</span><span class="sxs-lookup"><span data-stu-id="41930-143">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties from your cache:</span></span>

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Modification du fichier application.properties hello][RE02]

1. <span data-ttu-id="41930-145">Enregistrez et fermez hello *application.properties* fichier.</span><span class="sxs-lookup"><span data-stu-id="41930-145">Save and close hello *application.properties* file.</span></span>

1. <span data-ttu-id="41930-146">Créez un dossier nommé *contrôleur* sous le dossier source de hello pour votre package, par exemple :</span><span class="sxs-lookup"><span data-stu-id="41930-146">Create a folder named *controller* under hello source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="41930-147">-ou-</span><span class="sxs-lookup"><span data-stu-id="41930-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="41930-148">Créer un nouveau fichier nommé *HelloController.java* Bonjour *contrôleur* dossier.</span><span class="sxs-lookup"><span data-stu-id="41930-148">Create a new file named *HelloController.java* in hello *controller* folder.</span></span> <span data-ttu-id="41930-149">Ouvrez le fichier de hello dans un éditeur de texte et ajoutez les hello suivant tooit de code :</span><span class="sxs-lookup"><span data-stu-id="41930-149">Open hello file in a text editor and add hello following code tooit:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve hello DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve hello port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve hello access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define hello Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object tooconnect tooyour Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object toostore/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string tooyour cache.
         jedis.set("greeting", "Hello World!");

         // Return hello string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   <span data-ttu-id="41930-150">Où vous devez tooreplace `com.contoso.myazuredemo` avec le nom du package hello pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="41930-150">Where you will need tooreplace `com.contoso.myazuredemo` with hello package name for your project.</span></span>

1. <span data-ttu-id="41930-151">Enregistrez et fermez hello *HelloController.java* fichier.</span><span class="sxs-lookup"><span data-stu-id="41930-151">Save and close hello *HelloController.java* file.</span></span>

1. <span data-ttu-id="41930-152">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="41930-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="41930-153">Tester l’application web hello en parcourant toohttp://localhost:8080 à l’aide d’un navigateur web, ou utilisez la syntaxe hello comme hello l’exemple suivant, si vous avez curl disponible :</span><span class="sxs-lookup"><span data-stu-id="41930-153">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="41930-154">Vous devez voir hello « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="41930-154">You should see hello "Hello World!"</span></span> <span data-ttu-id="41930-155">doit s’afficher. Il est extrait de manière dynamique à partir de votre cache Redis.</span><span class="sxs-lookup"><span data-stu-id="41930-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41930-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="41930-156">Next steps</span></span>

<span data-ttu-id="41930-157">Pour plus d’informations sur l’utilisation des applications de démarrage du ressort sur Azure, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="41930-157">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="41930-158">Déployer un toohello ressort démarrage Application Azure App Service</span><span class="sxs-lookup"><span data-stu-id="41930-158">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="41930-159">Une Application de démarrage ressort en cours d’exécution sur un Kubernetes Cluster Bonjour Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="41930-159">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="41930-160">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="41930-160">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="41930-161">Pour plus d’informations sur la prise en main de Cache Redis avec Java sur Azure, consultez [toouse comment Azure Redis Cache avec Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="41930-161">For more information about getting started using Redis Cache with Java on Azure, see [How toouse Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<!-- URL List -->

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[ressort démarrage]: http://projects.spring.io/spring-boot/
[ressort Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: cache-java-get-started.md

<!-- IMG List -->

[AZ01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ01.png
[AZ02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ02.png
[AZ03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ03.png
[AZ04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ04.png
[AZ05]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ05.png

[SI01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI01.png
[SI02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI02.png
[SI03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI03.png
[SI04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI04.png

[RE01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE01.png
[RE02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE02.png
