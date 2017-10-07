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
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a>Comment tooconfigure un toouse d’application ressort initialisation initialiseur du Cache Redis

## <a name="overview"></a>Vue d'ensemble

Hello  **[Spring Framework]**  est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise. Un des projets de plus-populaires hello qui est créé de plateforme est [ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonomes. les développeurs de toohelp prise en main du ressort démarrage, plusieurs exemples de packages de démarrage du ressort sont disponibles à <https://github.com/spring-guides/>. En outre toochoosing à partir de la liste de hello de démarrage de la base de projets, hello  **[ressort Initializr]**  permet aux développeurs de commencer à créer des applications personnalisées ressort démarrage.

Cet article vous guide dans la création d’un cache Redis à l’aide de hello portail Azure, puis à l’aide de hello **ressort Initializr** toocreate une application personnalisée, puis en créant un Java web application qui stocke et récupère des données à l’aide de votre Cache redis.

## <a name="prerequisites"></a>Composants requis

Hello, suivant les conditions préalables est requises dans l’ordre toofollow hello étapes décrites dans cet article :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].

* Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.

* [Apache Maven](http://maven.apache.org/) version 3.0 ou ultérieure.

## <a name="create-a-redis-cache-on-azure"></a>Créer un Cache Redis sur Azure

1. Parcourir toohello Azure portail à <https://portal.azure.com/> et cliquez sur l’élément hello pour **+ nouveau**.

   ![Portail Azure][AZ01]

1. Cliquez sur **Base de données**, puis sur **Cache Redis**.

   ![Portail Azure][AZ02]

1. Sur hello **nouveau Cache Redis** , entrez hello **nom DNS** pour votre cache, puis spécifiez votre **abonnement**, **groupe de ressources**,  **Emplacement**, et **niveau tarifaire**. Lorsque vous avez défini ces options, cliquez sur **créer** toocreate votre cache.

   ![Portail Azure][AZ03]

1. Une fois que votre cache est terminé, vous verrez répertorié sur votre Azure **tableau de bord**, ainsi que sous hello **toutes les ressources**, et **les Caches Redis** pages. Vous pouvez cliquer sur votre cache sur n’importe quel ces emplacements tooopen hello page des propriétés pour votre cache.

   ![Portail Azure][AZ04]

1. Lorsque la page hello qui contient la liste hello des propriétés pour votre cache s’affiche, cliquez sur **clés d’accès** et copiez vos clés d’accès pour votre cache.

   ![Portail Azure][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a>Créer une application personnalisée à l’aide de hello ressort Initializr

1. Parcourir trop<https://start.spring.io/>.

1. Spécifiez que vous souhaitez toogenerate un **Maven** projet avec **Java**, entrez hello **groupe** et **Aritifact** noms pour votre application, puis cliquez sur le lien de hello trop**version complète de commutateur toohello** Hello ressort Initializr.

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Hello ressort Initializr utilisera hello **groupe** et **Aritifact** nom du package hello noms toocreate ; par exemple : *com.contoso.myazuredemo*.
   >

1. Défilement vers le bas toohello **Web** section et hello la case pour **Web**, puis faites défiler vers le bas toohello **NoSQL** section et hello la case pour **Redis**, faites défiler vers le bas toohello de page de hello et cliquez sur le bouton de hello trop**générer le projet**.

   ![Options complètes de Spring Initializr][SI02]

1. Lorsque vous y êtes invité, téléchargez hello projet tooa chemin d’accès sur votre ordinateur local.

   ![Télécharger un projet Spring Boot personnalisé][SI03]

1. Une fois que vous avez extrait les fichiers hello sur votre système local, votre application de démarrage du ressort personnalisée sera prête pour la modification.

   ![Fichiers de projet Spring Boot personnalisé][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a>Configurer votre toouse ressort démarrage personnalisée à votre Cache Redis

1. Recherchez hello *application.properties* fichier Bonjour *ressources* répertoire de votre application, ou créez le fichier de hello si elle n’existe pas déjà.

   ![Recherchez le fichier de application.properties hello][RE01]

1. Ouvrez hello *application.properties* de fichiers dans un éditeur de texte, ajouter hello lignes toohello fichier suivant et remplacer des valeurs d’exemple hello avec les propriétés appropriées de hello à partir de votre cache :

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Modification du fichier application.properties hello][RE02]

1. Enregistrez et fermez hello *application.properties* fichier.

1. Créez un dossier nommé *contrôleur* sous le dossier source de hello pour votre package, par exemple :

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   -ou-

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Créer un nouveau fichier nommé *HelloController.java* Bonjour *contrôleur* dossier. Ouvrez le fichier de hello dans un éditeur de texte et ajoutez les hello suivant tooit de code :

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
   
   Où vous devez tooreplace `com.contoso.myazuredemo` avec le nom du package hello pour votre projet.

1. Enregistrez et fermez hello *HelloController.java* fichier.

1. Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Tester l’application web hello en parcourant toohttp://localhost:8080 à l’aide d’un navigateur web, ou utilisez la syntaxe hello comme hello l’exemple suivant, si vous avez curl disponible :

   ```shell
   curl http://localhost:8080
   ```

   Vous devez voir hello « Hello World ! » doit s’afficher. Il est extrait de manière dynamique à partir de votre cache Redis.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation des applications de démarrage du ressort sur Azure, consultez hello suivant des articles :

* [Déployer un toohello ressort démarrage Application Azure App Service](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Une Application de démarrage ressort en cours d’exécution sur un Kubernetes Cluster Bonjour Service de conteneur Azure](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].

Pour plus d’informations sur la prise en main de Cache Redis avec Java sur Azure, consultez [toouse comment Azure Redis Cache avec Java][Redis Cache with Java].

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
