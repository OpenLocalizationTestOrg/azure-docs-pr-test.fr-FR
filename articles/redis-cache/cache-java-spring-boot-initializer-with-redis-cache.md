---
title: Guide pratique pour configurer une application Spring Boot Initializer pour utiliser le Cache Redis
description: "Découvrez comment configurer une application Spring Boot créée avec Spring Boot Initializr pour utiliser le Cache Redis Azure."
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
ms.openlocfilehash: fb3fc96a2136b7c326bb0eb291b7204e7acf0190
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a><span data-ttu-id="f0419-104">Guide pratique pour configurer une application Spring Boot Initializer pour utiliser le Cache Redis</span><span class="sxs-lookup"><span data-stu-id="f0419-104">How to configure a Spring Boot Initializer app to use Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="f0419-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f0419-105">Overview</span></span>

<span data-ttu-id="f0419-106">**[L’infrastructure Spring]** est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="f0419-106">The **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="f0419-107">Un des projets les plus connus créé sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="f0419-107">One of the more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="f0419-108">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="f0419-108">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="f0419-109">En plus de choisir parmi la liste des projets Spring Boot de base, **[Spring Initializr]** permet aux développeurs de commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="f0419-109">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="f0419-110">Cet article explique comment créer un cache Redis par le biais du portail Azure, utiliser **Spring Initializr** pour créer une application personnalisée, puis créer une application web Java qui stocke et récupère des données à l’aide de votre cache Redis.</span><span class="sxs-lookup"><span data-stu-id="f0419-110">This article walks you through creating a Redis cache using the Azure portal, then using the **Spring Initializr** to create a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0419-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f0419-111">Prerequisites</span></span>

<span data-ttu-id="f0419-112">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f0419-112">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="f0419-113">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="f0419-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="f0419-114">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f0419-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="f0419-115">[Apache Maven](http://maven.apache.org/) version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f0419-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="f0419-116">Créer un Cache Redis sur Azure</span><span class="sxs-lookup"><span data-stu-id="f0419-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="f0419-117">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et cliquez sur l’élément **+Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="f0419-117">Browse to the Azure portal at <https://portal.azure.com/> and click the item for **+New**.</span></span>

   ![Portail Azure][AZ01]

1. <span data-ttu-id="f0419-119">Cliquez sur **Base de données**, puis sur **Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="f0419-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Portail Azure][AZ02]

1. <span data-ttu-id="f0419-121">Dans la page **Nouveau cache Redis**, entrez le **Nom DNS** de votre cache, puis spécifiez votre **Abonnement**, **Groupe de ressources**, **Emplacement** et **Niveau tarifaire**.</span><span class="sxs-lookup"><span data-stu-id="f0419-121">On the **New Redis Cache** page, enter the **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="f0419-122">Une fois que vous avez défini ces options, cliquez sur **Créer** pour créer votre cache.</span><span class="sxs-lookup"><span data-stu-id="f0419-122">When you have specified these options, click **Create** to create your cache.</span></span>

   ![Portail Azure][AZ03]

1. <span data-ttu-id="f0419-124">Une fois votre cache terminé, il est répertorié dans votre **Tableau de bord** Azure et dans les pages **Toutes les ressources** et **Caches Redis**.</span><span class="sxs-lookup"><span data-stu-id="f0419-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="f0419-125">Vous pouvez cliquer sur le cache à l’un de ces emplacements pour ouvrir la page des propriétés de votre cache.</span><span class="sxs-lookup"><span data-stu-id="f0419-125">You can click on your cache on any of those locations to open the properties page for your cache.</span></span>

   ![Portail Azure][AZ04]

1. <span data-ttu-id="f0419-127">Quand la page qui contient la liste des propriétés de votre cache est affichée, cliquez sur **Clés d’accès** et copiez vos clés d’accès pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="f0419-127">When the page which contains the list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Portail Azure][AZ05]

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="f0419-129">Créer une application personnalisée à l’aide de Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="f0419-129">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="f0419-130">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="f0419-130">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="f0419-131">Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="f0419-131">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="f0419-133">Spring Initializr utilisera les noms de **Groupe** et d’**Artefact** pour créer le nom du package ; par exemple : *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="f0419-133">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="f0419-134">Faites défiler jusqu’à la section**Web** et cochez la case **Web**, faites défiler jusqu’à la section **NoSQL** et cochez la case **Redis**, puis faites défiler jusqu’au bas de la page et cliquez sur le bouton pour **générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="f0419-134">Scroll down to the **Web** section and check the box for **Web**, then scroll down to the **NoSQL** section and check the box for **Redis**, then scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Options complètes de Spring Initializr][SI02]

1. <span data-ttu-id="f0419-136">À l’invite, téléchargez le projet vers un emplacement sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="f0419-136">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger un projet Spring Boot personnalisé][SI03]

1. <span data-ttu-id="f0419-138">Une fois que vous avez extrait les fichiers sur votre système local, votre application Spring Boot personnalisée est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="f0419-138">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Fichiers de projet Spring Boot personnalisés][SI04]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a><span data-ttu-id="f0419-140">Configurer votre Spring Boot personnalisé pour utiliser votre Cache Redis</span><span class="sxs-lookup"><span data-stu-id="f0419-140">Configure your custom Spring Boot to use your Redis Cache</span></span>

1. <span data-ttu-id="f0419-141">Recherchez le fichier *application.properties* dans le répertoire *resources* de votre application, ou créez le fichier s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="f0419-141">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Rechercher le fichier application.properties][RE01]

1. <span data-ttu-id="f0419-143">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez les lignes suivantes au fichier et remplacez les exemples de valeurs par les propriétés appropriées de votre cache :</span><span class="sxs-lookup"><span data-stu-id="f0419-143">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties from your cache:</span></span>

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6380

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Modification du fichier application.properties][RE02]

1. <span data-ttu-id="f0419-145">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="f0419-145">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="f0419-146">Créez un dossier nommé *controller* sous le dossier source de votre package, par exemple :</span><span class="sxs-lookup"><span data-stu-id="f0419-146">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="f0419-147">-ou-</span><span class="sxs-lookup"><span data-stu-id="f0419-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="f0419-148">Créez un fichier nommé *HelloController.java* dans le dossier *controller*.</span><span class="sxs-lookup"><span data-stu-id="f0419-148">Create a new file named *HelloController.java* in the *controller* folder.</span></span> <span data-ttu-id="f0419-149">Ouvrez le fichier dans un éditeur de texte, puis ajoutez-y le code suivant :</span><span class="sxs-lookup"><span data-stu-id="f0419-149">Open the file in a text editor and add the following code to it:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve the DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve the port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve the access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define the Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object to connect to your Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object to store/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string to your cache.
         jedis.set("greeting", "Hello World!");

         // Return the string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   <span data-ttu-id="f0419-150">Où vous devez remplacer `com.contoso.myazuredemo` par le nom du package de votre projet.</span><span class="sxs-lookup"><span data-stu-id="f0419-150">Where you will need to replace `com.contoso.myazuredemo` with the package name for your project.</span></span>

1. <span data-ttu-id="f0419-151">Enregistrez et fermez le fichier *HelloController.java*.</span><span class="sxs-lookup"><span data-stu-id="f0419-151">Save and close the *HelloController.java* file.</span></span>

1. <span data-ttu-id="f0419-152">Générez votre application Spring Boot avec Maven et exécutez-la, par exemple :</span><span class="sxs-lookup"><span data-stu-id="f0419-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="f0419-153">Testez l’application web en accédant à http://localhost:8080 avec un navigateur web, ou utilisez la syntaxe de l’exemple suivant si vous disposez de curl :</span><span class="sxs-lookup"><span data-stu-id="f0419-153">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="f0419-154">Le message « Hello World! » de votre exemple de contrôleur</span><span class="sxs-lookup"><span data-stu-id="f0419-154">You should see the "Hello World!"</span></span> <span data-ttu-id="f0419-155">doit s’afficher. Il est extrait de manière dynamique à partir de votre cache Redis.</span><span class="sxs-lookup"><span data-stu-id="f0419-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0419-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0419-156">Next steps</span></span>

<span data-ttu-id="f0419-157">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="f0419-157">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="f0419-158">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f0419-158">Deploy a Spring Boot Application to the Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="f0419-159">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f0419-159">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="f0419-160">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="f0419-160">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="f0419-161">Pour plus d’informations sur la prise en main du Cache Redis avec Java sur Azure, consultez [Utilisation du Cache Redis Azure avec Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="f0419-161">For more information about getting started using Redis Cache with Java on Azure, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<!-- URL List -->

<span data-ttu-id="f0419-162">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="f0419-162">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="f0419-163">[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="f0419-163">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="f0419-164">[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="f0419-164">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="f0419-165">[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="f0419-165">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="f0419-166">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="f0419-166">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="f0419-167">[Spring Initializr]: https://start.spring.io/</span><span class="sxs-lookup"><span data-stu-id="f0419-167">[Spring Initializr]: https://start.spring.io/</span></span>
<span data-ttu-id="f0419-168">[L’infrastructure Spring]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="f0419-168">[Spring Framework]: https://spring.io/</span></span>
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
