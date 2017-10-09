---
title: "aaaHow toouse hello Starter de démarrage du ressort avec une API de DocumentDB de base de données Azure Cosmos"
description: "Découvrez comment tooconfigure créer une application hello ressort initialisation initialiseur par hello API de DocumentDB de base de données Azure Cosmos."
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Cosmos DB
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/08/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a2c6de678f850676cb2887e224e5c12950db0e53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>Comment toouse hello Starter de démarrage du ressort avec les API de DocumentDB de base de données Azure Cosmos

## <a name="overview"></a>Vue d'ensemble

Hello  **[Spring Framework]**  est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise. Un des projets plus-populaires hello qui est créé de plateforme est [ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonomes. les développeurs de toohelp prise en main du ressort démarrage, plusieurs exemples de packages de démarrage du ressort sont disponibles à <https://github.com/spring-guides/>. En outre toochoosing à partir de la liste de hello de démarrage de la base de projets, hello  **[ressort Initializr]**  permet aux développeurs de commencer à créer des applications personnalisées ressort démarrage.

Base de données Cosmos Azure est un service de base de données de distribution globale qui permet aux développeurs toowork avec les données à l’aide de diverses API standard, tels que DocumentDB, MongoDB, graphique et API de Table. Démarrage de démarrage du ressort de Microsoft permet aux développeurs toouse ressort démarrage applications qui s’intégrer facilement avec la base de données Azure Cosmos à l’aide de DocumentDB APIs.

Cet article illustre la création d’une base de données Azure Cosmos, à l’aide de hello portail Azure, puis à l’aide de hello **ressort Initializr** toocreate une application java personnalisées, puis ajoutez hello ressort démarrage Starter fonctionnalité tooyour personnalisé données d’application toostore dans et extraire des données de votre base de données Azure Cosmos à l’aide de hello API DocumentDB.

## <a name="prerequisites"></a>Composants requis

Hello, suivant les conditions préalables est requises dans l’ordre toofollow hello étapes décrites dans cet article :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].

* Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.

* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a>Créer une base de données Azure Cosmos à l’aide de hello portail Azure

1. Parcourir toohello Azure portail à <https://portal.azure.com/> et cliquez sur **+ nouveau**.

   ![Portail Azure][AZ01]

1. Cliquez sur **Bases de données**, puis sur **Azure Cosmos DB**.

   ![Portail Azure][AZ02]

1. Sur hello **base de données Azure Cosmos** , entrez hello informations suivantes :

   * Entrez une valeur unique **ID**, que vous utiliserez comme hello URI pour votre base de données. Par exemple : *wingtiptoysdata.documents.azure.com*.
   * Choisissez **SQL (base de données de Document)** pour hello API.
   * Choisissez hello **abonnement** toouse souhaité pour votre base de données.
   * Spécifiez si toocreate un nouveau **groupe de ressources** pour votre base de données, ou choisissez un groupe de ressources existant.
   * Spécifiez hello **emplacement** pour votre base de données.
   
   Lorsque vous avez défini ces options, cliquez sur **créer** toocreate votre base de données.

   ![Portail Azure][AZ03]

1. Lorsque votre base de données a été créé, il est répertorié sous votre Azure **tableau de bord**, ainsi que sous hello **toutes les ressources** et **base de données Azure Cosmos** pages. Vous pouvez cliquer sur votre base de données sur n’importe quel ces emplacements tooopen hello page des propriétés pour votre cache.

   ![Portail Azure][AZ04]

1. Lorsque la page de propriétés hello pour votre base de données s’affiche, cliquez sur **clés d’accès** et copiez votre URI et clés d’accès pour votre base de données ; vous allez utiliser ces valeurs dans votre application de démarrage du ressort.

   ![Portail Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a>Créer une application de démarrage du ressort simple avec hello ressort Initializr

1. Parcourir trop<https://start.spring.io/>.

1. Spécifiez que vous souhaitez toogenerate un **Maven** projet avec **Java**, entrez hello **groupe** et **artefact** noms pour votre application, et puis cliquez sur le bouton de hello trop**générer le projet**.

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Hello ressort Initializr utilise hello **groupe** et **artefact** nom du package hello noms toocreate ; par exemple : *com.example.wintiptoys*.
   >

1. Lorsque vous y êtes invité, téléchargez hello projet tooa chemin d’accès sur votre ordinateur local.

   ![Télécharger un projet Spring Boot personnalisé][SI02]

1. Une fois que vous avez extrait les fichiers hello sur votre système local, votre application de démarrage du ressort simple sera prête pour la modification.

   ![Fichiers de projet Spring Boot personnalisé][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a>Configurer votre hello de toouse ressort démarrage application Azure ressort démarrage Starter

1. Recherchez hello *pom.xml* fichier répertoire hello de votre application ; par exemple :

   `C:\SpringBoot\wingtiptoys\pom.xml`

   -ou-

   `/users/example/home/wingtiptoys/pom.xml`

   ![Recherchez le fichier de pom.xml hello][PM01]

1. Ouvrez hello *pom.xml* dans un éditeur de texte et ajoutez hello suivant toolist de lignes de `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Modification du fichier pom.xml hello][PM02]

1. Enregistrez et fermez hello *pom.xml* fichier.

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a>Configurer votre toouse d’application de démarrage du ressort de votre base de données Azure Cosmos

1. Recherchez hello *application.properties* fichier Bonjour *ressources* répertoire de votre application, par exemple :

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   -ou-

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Recherchez le fichier de application.properties hello][RE01]

1. Ouvrez hello *application.properties* de fichiers dans un éditeur de texte, ajouter hello lignes toohello fichier suivant et remplacez les exemples de valeurs hello avec les propriétés appropriées de hello pour votre base de données :

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Modification du fichier application.properties hello][RE02]

1. Enregistrez et fermez hello *application.properties* fichier.

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a>Ajouter des fonctionnalités de base de données exemple code tooimplement

Dans cette section, vous créez deux classes Java pour le stockage des données utilisateur, et puis modifier votre toocreate de classe d’application principale une instance de la classe d’utilisateur hello et enregistrez-le tooyour de base de données.

### <a name="define-a-basic-class-for-storing-user-data"></a>Définir une classe de base pour le stockage des données utilisateur

1. Créer un nouveau fichier nommé *User.java* Bonjour même répertoire que votre fichier de Java principale de l’application.

1. Ouvrez hello *User.java* de fichiers dans un éditeur de texte, puis ajoutez les lignes suivantes de hello toohello fichier toodefine une classe d’utilisateur générique qui stocke et récupérer des valeurs dans votre base de données :

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. Enregistrez et fermez hello *User.java* fichier.

### <a name="define-a-data-repository-interface"></a>Définir une interface de référentiel de données

1. Créer un nouveau fichier nommé *UserRepository.java* Bonjour même répertoire que votre fichier de Java principale de l’application.

1. Ouvrez hello *UserRepository.java* de fichiers dans un éditeur de texte, puis ajoutez les lignes suivantes de hello toohello fichier toodefine une interface utilisateur référentiel qui étend l’interface de référentiel DocumentDB hello par défaut :

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. Enregistrez et fermez hello *UserRepository.java* fichier.

### <a name="modify-hello-main-application-class"></a>Modifier la classe de l’application principale hello

1. Localiser le fichier de Java principale de l’application hello dans hello package de votre application ; par exemple :

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   -ou-

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Recherchez le fichier Java de l’application hello][JV01]

1. Ouvrez le fichier Java de principale de l’application hello dans un éditeur de texte et ajoutez hello lignes toohello fichier suivant :

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. Enregistrez et fermez le fichier de Java hello principale de l’application.

## <a name="build-and-test-your-app"></a>Générer et tester votre application

1. Ouvrez une invite de commandes et de modifier le dossier toohello du répertoire où votre *pom.xml* fichier se trouve, par exemple :

   `cd C:\SpringBoot\wingtiptoys`

   -ou-

   `cd /users/example/home/wingtiptoys`

1. Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. Votre application affiche plusieurs messages d’exécution, et vous devez voir le message de type hello `User: testFirstName testLastName` affiché tooindicate que les valeurs ont été correctement stockés et récupérés à partir de votre base de données.

   ![Sortie réussie à partir de l’application hello][JV02]

1. FACULTATIF : Vous pouvez utiliser hello tooview portail Azure hello contenu de votre base de données Azure Cosmos à partir de la page de propriétés hello votre base de données en cliquant sur **Document Explorer**et puis en sélectionnant et élément de hello de tooview liste hello affiché contenu.

   ![À l’aide de tooview de l’Explorateur de documents hello vos données][JV03]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation de la base de données Azure Cosmos et Java, consultez hello suivant des articles :

* [Documentation Azure Cosmos DB]

* [Base de données Cosmos Azure : Génération d’une application API DocumentDB avec Java et hello portail Azure][Build a DocumentDB API app with Java]

Pour plus d’informations sur l’utilisation des applications de démarrage du ressort sur Azure, consultez hello suivant des articles :

* [Spring Boot DocumenDB Starter pour Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [Déployer un toohello ressort démarrage Application Azure App Service](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Une Application de démarrage ressort en cours d’exécution sur un Kubernetes Cluster Bonjour Service de conteneur Azure](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].

<!-- URL List -->

[Documentation Azure Cosmos DB]: /azure/cosmos-db/
[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[ressort démarrage]: http://projects.spring.io/spring-boot/
[ressort Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ01.png
[AZ02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ02.png
[AZ03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ03.png
[AZ04]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ04.png
[AZ05]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ05.png

[SI01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI01.png
[SI02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI02.png
[SI03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI03.png

[RE01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE01.png
[RE02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE02.png

[PM01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM01.png
[PM02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM02.png

[JV01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV01.png
[JV02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV02.png
[JV03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV03.png
