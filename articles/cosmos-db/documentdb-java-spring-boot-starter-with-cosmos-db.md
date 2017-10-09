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
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="18367-104">Comment toouse hello Starter de démarrage du ressort avec les API de DocumentDB de base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="18367-104">How toouse hello Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="18367-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="18367-105">Overview</span></span>

<span data-ttu-id="18367-106">Hello  **[Spring Framework]**  est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="18367-106">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="18367-107">Un des projets plus-populaires hello qui est créé de plateforme est [ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="18367-107">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="18367-108">les développeurs de toohelp prise en main du ressort démarrage, plusieurs exemples de packages de démarrage du ressort sont disponibles à <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="18367-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="18367-109">En outre toochoosing à partir de la liste de hello de démarrage de la base de projets, hello  **[ressort Initializr]**  permet aux développeurs de commencer à créer des applications personnalisées ressort démarrage.</span><span class="sxs-lookup"><span data-stu-id="18367-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="18367-110">Base de données Cosmos Azure est un service de base de données de distribution globale qui permet aux développeurs toowork avec les données à l’aide de diverses API standard, tels que DocumentDB, MongoDB, graphique et API de Table.</span><span class="sxs-lookup"><span data-stu-id="18367-110">Azure Cosmos DB is a globally-distributed database service that allows developers toowork with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="18367-111">Démarrage de démarrage du ressort de Microsoft permet aux développeurs toouse ressort démarrage applications qui s’intégrer facilement avec la base de données Azure Cosmos à l’aide de DocumentDB APIs.</span><span class="sxs-lookup"><span data-stu-id="18367-111">Microsoft's Spring Boot Starter enables developers toouse Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="18367-112">Cet article illustre la création d’une base de données Azure Cosmos, à l’aide de hello portail Azure, puis à l’aide de hello **ressort Initializr** toocreate une application java personnalisées, puis ajoutez hello ressort démarrage Starter fonctionnalité tooyour personnalisé données d’application toostore dans et extraire des données de votre base de données Azure Cosmos à l’aide de hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="18367-112">This article demonstrates creating an Azure Cosmos DB using hello Azure portal, then using hello **Spring Initializr** toocreate a custom java application, and then add hello Spring Boot Starter functionality tooyour custom application toostore data in and retrieve data from your Azure Cosmos DB by using hello DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18367-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="18367-113">Prerequisites</span></span>

<span data-ttu-id="18367-114">Hello, suivant les conditions préalables est requises dans l’ordre toofollow hello étapes décrites dans cet article :</span><span class="sxs-lookup"><span data-stu-id="18367-114">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="18367-115">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="18367-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="18367-116">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="18367-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="18367-117">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="18367-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a><span data-ttu-id="18367-118">Créer une base de données Azure Cosmos à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="18367-118">Create an Azure Cosmos DB by using hello Azure portal</span></span>

1. <span data-ttu-id="18367-119">Parcourir toohello Azure portail à <https://portal.azure.com/> et cliquez sur **+ nouveau**.</span><span class="sxs-lookup"><span data-stu-id="18367-119">Browse toohello Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Portail Azure][AZ01]

1. <span data-ttu-id="18367-121">Cliquez sur **Bases de données**, puis sur **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="18367-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Portail Azure][AZ02]

1. <span data-ttu-id="18367-123">Sur hello **base de données Azure Cosmos** , entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="18367-123">On hello **Azure Cosmos DB** page, enter hello following information:</span></span>

   * <span data-ttu-id="18367-124">Entrez une valeur unique **ID**, que vous utiliserez comme hello URI pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="18367-124">Enter a unique **ID**, which you will use as hello URI for your database.</span></span> <span data-ttu-id="18367-125">Par exemple : *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="18367-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="18367-126">Choisissez **SQL (base de données de Document)** pour hello API.</span><span class="sxs-lookup"><span data-stu-id="18367-126">Choose **SQL (Document DB)** for hello API.</span></span>
   * <span data-ttu-id="18367-127">Choisissez hello **abonnement** toouse souhaité pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="18367-127">Choose hello **Subscription** you want toouse for your database.</span></span>
   * <span data-ttu-id="18367-128">Spécifiez si toocreate un nouveau **groupe de ressources** pour votre base de données, ou choisissez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="18367-128">Specify whether toocreate a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="18367-129">Spécifiez hello **emplacement** pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="18367-129">Specify hello **Location** for your database.</span></span>
   
   <span data-ttu-id="18367-130">Lorsque vous avez défini ces options, cliquez sur **créer** toocreate votre base de données.</span><span class="sxs-lookup"><span data-stu-id="18367-130">When you have specified these options, click **Create** toocreate your database.</span></span>

   ![Portail Azure][AZ03]

1. <span data-ttu-id="18367-132">Lorsque votre base de données a été créé, il est répertorié sous votre Azure **tableau de bord**, ainsi que sous hello **toutes les ressources** et **base de données Azure Cosmos** pages.</span><span class="sxs-lookup"><span data-stu-id="18367-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under hello **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="18367-133">Vous pouvez cliquer sur votre base de données sur n’importe quel ces emplacements tooopen hello page des propriétés pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="18367-133">You can click on your database on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Portail Azure][AZ04]

1. <span data-ttu-id="18367-135">Lorsque la page de propriétés hello pour votre base de données s’affiche, cliquez sur **clés d’accès** et copiez votre URI et clés d’accès pour votre base de données ; vous allez utiliser ces valeurs dans votre application de démarrage du ressort.</span><span class="sxs-lookup"><span data-stu-id="18367-135">When hello properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Portail Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a><span data-ttu-id="18367-137">Créer une application de démarrage du ressort simple avec hello ressort Initializr</span><span class="sxs-lookup"><span data-stu-id="18367-137">Create a simple Spring Boot application with hello Spring Initializr</span></span>

1. <span data-ttu-id="18367-138">Parcourir trop<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="18367-138">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="18367-139">Spécifiez que vous souhaitez toogenerate un **Maven** projet avec **Java**, entrez hello **groupe** et **artefact** noms pour votre application, et puis cliquez sur le bouton de hello trop**générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="18367-139">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Artifact** names for your application, and then click hello button too**Generate Project**.</span></span>

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="18367-141">Hello ressort Initializr utilise hello **groupe** et **artefact** nom du package hello noms toocreate ; par exemple : *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="18367-141">hello Spring Initializr uses hello **Group** and **Artifact** names toocreate hello package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="18367-142">Lorsque vous y êtes invité, téléchargez hello projet tooa chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="18367-142">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Télécharger un projet Spring Boot personnalisé][SI02]

1. <span data-ttu-id="18367-144">Une fois que vous avez extrait les fichiers hello sur votre système local, votre application de démarrage du ressort simple sera prête pour la modification.</span><span class="sxs-lookup"><span data-stu-id="18367-144">After you have extracted hello files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Fichiers de projet Spring Boot personnalisé][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a><span data-ttu-id="18367-146">Configurer votre hello de toouse ressort démarrage application Azure ressort démarrage Starter</span><span class="sxs-lookup"><span data-stu-id="18367-146">Configure your Spring Boot app toouse hello Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="18367-147">Recherchez hello *pom.xml* fichier répertoire hello de votre application ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="18367-147">Locate hello *pom.xml* file in hello directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="18367-148">-ou-</span><span class="sxs-lookup"><span data-stu-id="18367-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Recherchez le fichier de pom.xml hello][PM01]

1. <span data-ttu-id="18367-150">Ouvrez hello *pom.xml* dans un éditeur de texte et ajoutez hello suivant toolist de lignes de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="18367-150">Open hello *pom.xml* file in a text editor, and add hello following lines toolist of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Modification du fichier pom.xml hello][PM02]

1. <span data-ttu-id="18367-152">Enregistrez et fermez hello *pom.xml* fichier.</span><span class="sxs-lookup"><span data-stu-id="18367-152">Save and close hello *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a><span data-ttu-id="18367-153">Configurer votre toouse d’application de démarrage du ressort de votre base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="18367-153">Configure your Spring Boot app toouse your Azure Cosmos DB</span></span>

1. <span data-ttu-id="18367-154">Recherchez hello *application.properties* fichier Bonjour *ressources* répertoire de votre application, par exemple :</span><span class="sxs-lookup"><span data-stu-id="18367-154">Locate hello *application.properties* file in hello *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="18367-155">-ou-</span><span class="sxs-lookup"><span data-stu-id="18367-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Recherchez le fichier de application.properties hello][RE01]

1. <span data-ttu-id="18367-157">Ouvrez hello *application.properties* de fichiers dans un éditeur de texte, ajouter hello lignes toohello fichier suivant et remplacez les exemples de valeurs hello avec les propriétés appropriées de hello pour votre base de données :</span><span class="sxs-lookup"><span data-stu-id="18367-157">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties for your database:</span></span>

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Modification du fichier application.properties hello][RE02]

1. <span data-ttu-id="18367-159">Enregistrez et fermez hello *application.properties* fichier.</span><span class="sxs-lookup"><span data-stu-id="18367-159">Save and close hello *application.properties* file.</span></span>

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a><span data-ttu-id="18367-160">Ajouter des fonctionnalités de base de données exemple code tooimplement</span><span class="sxs-lookup"><span data-stu-id="18367-160">Add sample code tooimplement basic database functionality</span></span>

<span data-ttu-id="18367-161">Dans cette section, vous créez deux classes Java pour le stockage des données utilisateur, et puis modifier votre toocreate de classe d’application principale une instance de la classe d’utilisateur hello et enregistrez-le tooyour de base de données.</span><span class="sxs-lookup"><span data-stu-id="18367-161">In this section you create two Java classes for storing user data, and then you modify your main application class toocreate an instance of hello user class and save it tooyour database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="18367-162">Définir une classe de base pour le stockage des données utilisateur</span><span class="sxs-lookup"><span data-stu-id="18367-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="18367-163">Créer un nouveau fichier nommé *User.java* Bonjour même répertoire que votre fichier de Java principale de l’application.</span><span class="sxs-lookup"><span data-stu-id="18367-163">Create a new file named *User.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="18367-164">Ouvrez hello *User.java* de fichiers dans un éditeur de texte, puis ajoutez les lignes suivantes de hello toohello fichier toodefine une classe d’utilisateur générique qui stocke et récupérer des valeurs dans votre base de données :</span><span class="sxs-lookup"><span data-stu-id="18367-164">Open hello *User.java* file in a text editor, and add hello following lines toohello file toodefine a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="18367-165">Enregistrez et fermez hello *User.java* fichier.</span><span class="sxs-lookup"><span data-stu-id="18367-165">Save and close hello *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="18367-166">Définir une interface de référentiel de données</span><span class="sxs-lookup"><span data-stu-id="18367-166">Define a data repository interface</span></span>

1. <span data-ttu-id="18367-167">Créer un nouveau fichier nommé *UserRepository.java* Bonjour même répertoire que votre fichier de Java principale de l’application.</span><span class="sxs-lookup"><span data-stu-id="18367-167">Create a new file named *UserRepository.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="18367-168">Ouvrez hello *UserRepository.java* de fichiers dans un éditeur de texte, puis ajoutez les lignes suivantes de hello toohello fichier toodefine une interface utilisateur référentiel qui étend l’interface de référentiel DocumentDB hello par défaut :</span><span class="sxs-lookup"><span data-stu-id="18367-168">Open hello *UserRepository.java* file in a text editor, and add hello following lines toohello file toodefine a user repository interface that extends hello default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="18367-169">Enregistrez et fermez hello *UserRepository.java* fichier.</span><span class="sxs-lookup"><span data-stu-id="18367-169">Save and close hello *UserRepository.java* file.</span></span>

### <a name="modify-hello-main-application-class"></a><span data-ttu-id="18367-170">Modifier la classe de l’application principale hello</span><span class="sxs-lookup"><span data-stu-id="18367-170">Modify hello main application class</span></span>

1. <span data-ttu-id="18367-171">Localiser le fichier de Java principale de l’application hello dans hello package de votre application ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="18367-171">Locate hello main application Java file in hello package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="18367-172">-ou-</span><span class="sxs-lookup"><span data-stu-id="18367-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Recherchez le fichier Java de l’application hello][JV01]

1. <span data-ttu-id="18367-174">Ouvrez le fichier Java de principale de l’application hello dans un éditeur de texte et ajoutez hello lignes toohello fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="18367-174">Open hello main application Java file in a text editor, and add hello following lines toohello file:</span></span>

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

1. <span data-ttu-id="18367-175">Enregistrez et fermez le fichier de Java hello principale de l’application.</span><span class="sxs-lookup"><span data-stu-id="18367-175">Save and close hello main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="18367-176">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="18367-176">Build and test your app</span></span>

1. <span data-ttu-id="18367-177">Ouvrez une invite de commandes et de modifier le dossier toohello du répertoire où votre *pom.xml* fichier se trouve, par exemple :</span><span class="sxs-lookup"><span data-stu-id="18367-177">Open a command prompt and change directory toohello folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="18367-178">-ou-</span><span class="sxs-lookup"><span data-stu-id="18367-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="18367-179">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="18367-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="18367-180">Votre application affiche plusieurs messages d’exécution, et vous devez voir le message de type hello `User: testFirstName testLastName` affiché tooindicate que les valeurs ont été correctement stockés et récupérés à partir de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="18367-180">Your application will display several runtime messages, and you should see hello message `User: testFirstName testLastName` displayed tooindicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Sortie réussie à partir de l’application hello][JV02]

1. <span data-ttu-id="18367-182">FACULTATIF : Vous pouvez utiliser hello tooview portail Azure hello contenu de votre base de données Azure Cosmos à partir de la page de propriétés hello votre base de données en cliquant sur **Document Explorer**et puis en sélectionnant et élément de hello de tooview liste hello affiché contenu.</span><span class="sxs-lookup"><span data-stu-id="18367-182">OPTIONAL: You can use hello Azure portal tooview hello contents of your Azure Cosmos DB from hello properties page for your database by clicking  **Document Explorer**, and then selecting and item from hello displayed list tooview hello contents.</span></span>

   ![À l’aide de tooview de l’Explorateur de documents hello vos données][JV03]

## <a name="next-steps"></a><span data-ttu-id="18367-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18367-184">Next steps</span></span>

<span data-ttu-id="18367-185">Pour plus d’informations sur l’utilisation de la base de données Azure Cosmos et Java, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="18367-185">For more information about using Azure Cosmos DB and Java, see hello following articles:</span></span>

* <span data-ttu-id="18367-186">[Documentation Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="18367-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="18367-187">[Base de données Cosmos Azure : Génération d’une application API DocumentDB avec Java et hello portail Azure][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="18367-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and hello Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="18367-188">Pour plus d’informations sur l’utilisation des applications de démarrage du ressort sur Azure, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="18367-188">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="18367-189">Spring Boot DocumenDB Starter pour Azure</span><span class="sxs-lookup"><span data-stu-id="18367-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="18367-190">Déployer un toohello ressort démarrage Application Azure App Service</span><span class="sxs-lookup"><span data-stu-id="18367-190">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="18367-191">Une Application de démarrage ressort en cours d’exécution sur un Kubernetes Cluster Bonjour Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="18367-191">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="18367-192">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="18367-192">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

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
