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
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a>Guide pratique pour configurer une application Spring Boot Initializer pour utiliser le Cache Redis

## <a name="overview"></a>Vue d'ensemble

**[L’infrastructure Spring]** est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise. Un des projets les plus connus créé sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes. Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>. En plus de choisir parmi la liste des projets Spring Boot de base, **[Spring Initializr]** permet aux développeurs de commencer à créer des applications Spring Boot personnalisées.

Cet article explique comment créer un cache Redis par le biais du portail Azure, utiliser **Spring Initializr** pour créer une application personnalisée, puis créer une application web Java qui stocke et récupère des données à l’aide de votre cache Redis.

## <a name="prerequisites"></a>Composants requis

Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].

* Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.

* [Apache Maven](http://maven.apache.org/) version 3.0 ou ultérieure.

## <a name="create-a-redis-cache-on-azure"></a>Créer un Cache Redis sur Azure

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et cliquez sur l’élément **+Nouveau**.

   ![Portail Azure][AZ01]

1. Cliquez sur **Base de données**, puis sur **Cache Redis**.

   ![Portail Azure][AZ02]

1. Dans la page **Nouveau cache Redis**, entrez le **Nom DNS** de votre cache, puis spécifiez votre **Abonnement**, **Groupe de ressources**, **Emplacement** et **Niveau tarifaire**. Une fois que vous avez défini ces options, cliquez sur **Créer** pour créer votre cache.

   ![Portail Azure][AZ03]

1. Une fois votre cache terminé, il est répertorié dans votre **Tableau de bord** Azure et dans les pages **Toutes les ressources** et **Caches Redis**. Vous pouvez cliquer sur le cache à l’un de ces emplacements pour ouvrir la page des propriétés de votre cache.

   ![Portail Azure][AZ04]

1. Quand la page qui contient la liste des propriétés de votre cache est affichée, cliquez sur **Clés d’accès** et copiez vos clés d’accès pour votre cache.

   ![Portail Azure][AZ05]

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Créer une application personnalisée à l’aide de Spring Initializr

1. Accédez à <https://start.spring.io/>.

1. Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr utilisera les noms de **Groupe** et d’**Artefact** pour créer le nom du package ; par exemple : *com.contoso.myazuredemo*.
   >

1. Faites défiler jusqu’à la section**Web** et cochez la case **Web**, faites défiler jusqu’à la section **NoSQL** et cochez la case **Redis**, puis faites défiler jusqu’au bas de la page et cliquez sur le bouton pour **générer le projet**.

   ![Options complètes de Spring Initializr][SI02]

1. À l’invite, téléchargez le projet vers un emplacement sur votre ordinateur local.

   ![Télécharger un projet Spring Boot personnalisé][SI03]

1. Une fois que vous avez extrait les fichiers sur votre système local, votre application Spring Boot personnalisée est prête à être modifiée.

   ![Fichiers de projet Spring Boot personnalisés][SI04]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a>Configurer votre Spring Boot personnalisé pour utiliser votre Cache Redis

1. Recherchez le fichier *application.properties* dans le répertoire *resources* de votre application, ou créez le fichier s’il n’existe pas.

   ![Rechercher le fichier application.properties][RE01]

1. Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez les lignes suivantes au fichier et remplacez les exemples de valeurs par les propriétés appropriées de votre cache :

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6380

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Modification du fichier application.properties][RE02]

1. Enregistrez et fermez le fichier *application.properties*.

1. Créez un dossier nommé *controller* sous le dossier source de votre package, par exemple :

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   -ou-

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Créez un fichier nommé *HelloController.java* dans le dossier *controller*. Ouvrez le fichier dans un éditeur de texte, puis ajoutez-y le code suivant :

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
   
   Où vous devez remplacer `com.contoso.myazuredemo` par le nom du package de votre projet.

1. Enregistrez et fermez le fichier *HelloController.java*.

1. Générez votre application Spring Boot avec Maven et exécutez-la, par exemple :

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Testez l’application web en accédant à http://localhost:8080 avec un navigateur web, ou utilisez la syntaxe de l’exemple suivant si vous disposez de curl :

   ```shell
   curl http://localhost:8080
   ```

   Le message « Hello World! » de votre exemple de contrôleur doit s’afficher. Il est extrait de manière dynamique à partir de votre cache Redis.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Déployer une application Spring Boot sur Azure App Service](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].

Pour plus d’informations sur la prise en main du Cache Redis avec Java sur Azure, consultez [Utilisation du Cache Redis Azure avec Java][Redis Cache with Java].

<!-- URL List -->

[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[L’infrastructure Spring]: https://spring.io/
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
