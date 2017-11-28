---
title: "didacticiel de développement d’application aaaJava à l’aide de la base de données Azure Cosmos | Documents Microsoft"
description: "Ce didacticiel de l’application web Java vous montre comment toouse hello de base de données Azure Cosmos hello API DocumentDB toostore et accéder aux données à partir d’une application Java hébergée sur des sites Web Azure."
keywords: "Développement d’applications, didacticiel de base de données, application java, didacticiel de l’application web java, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a><span data-ttu-id="829cf-104">Créer une application web de Java à l’aide de la base de données Azure Cosmos et hello API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="829cf-104">Build a Java web application using Azure Cosmos DB and hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="829cf-105">.NET</span><span class="sxs-lookup"><span data-stu-id="829cf-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="829cf-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="829cf-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="829cf-107">Java</span><span class="sxs-lookup"><span data-stu-id="829cf-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="829cf-108">Python</span><span class="sxs-lookup"><span data-stu-id="829cf-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="829cf-109">Ce didacticiel de l’application web Java vous montre comment toouse hello [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) service toostore et accéder aux données à partir d’une application Java hébergée sur Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="829cf-109">This Java web application tutorial shows you how toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="829cf-110">Dans cette rubrique, vous allez apprendre à :</span><span class="sxs-lookup"><span data-stu-id="829cf-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="829cf-111">Comment toobuild une application Java Server Pages (JSP) de base dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="829cf-111">How toobuild a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="829cf-112">Comment toowork avec hello Azure Cosmos DB service à l’aide de hello [Kit de développement Java Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="829cf-112">How toowork with hello Azure Cosmos DB service using hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="829cf-113">Ce didacticiel d’application Java vous montre des tâches d’application de gestion des tâches toocreate sur le web qui permet de marquer, récupérer et vous toocreate comme étant exécutée, comme indiqué dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="829cf-113">This Java application tutorial shows you how toocreate a web-based task-management application that enables you toocreate, retrieve, and mark tasks as complete, as shown in hello following image.</span></span> <span data-ttu-id="829cf-114">Chacune des tâches hello dans la liste de tâches hello sont stockés sous forme de documents JSON dans la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="829cf-114">Each of hello tasks in hello ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Application Java My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="829cf-116">Ce didacticiel de développement d’applications part du principe que vous avez déjà utilisé Java.</span><span class="sxs-lookup"><span data-stu-id="829cf-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="829cf-117">Si vous êtes tooJava nouveau ou hello [outils requis](#Prerequisites), nous vous recommandons de télécharger hello complète [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projet à partir de GitHub et de la création à l’aide de [hello instructions à fin hello de ce l’article](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="829cf-117">If you are new tooJava or hello [prerequisite tools](#Prerequisites), we recommend downloading hello complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [hello instructions at hello end of this article](#GetProject).</span></span> <span data-ttu-id="829cf-118">Une fois que vous avez créé, vous pouvez consulter les informations de toogain d’article hello sur le code hello dans le contexte de hello du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="829cf-118">Once you have it built, you can review hello article toogain insight on hello code in hello context of hello project.</span></span>  
> 
> 

## <span data-ttu-id="829cf-119"><a id="Prerequisites"></a>Conditions préalables à l’exécution de ce didacticiel d’application web Java</span><span class="sxs-lookup"><span data-stu-id="829cf-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="829cf-120">Avant de commencer ce didacticiel de développement d’application, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="829cf-120">Before you begin this application development tutorial, you must have hello following:</span></span>

* <span data-ttu-id="829cf-121">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="829cf-121">An active Azure account.</span></span> <span data-ttu-id="829cf-122">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="829cf-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="829cf-123">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="829cf-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="829cf-124">OU</span><span class="sxs-lookup"><span data-stu-id="829cf-124">OR</span></span>

    <span data-ttu-id="829cf-125">Une installation locale de hello [Azure Cosmos DB émulateur](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="829cf-125">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="829cf-126">[Kit de développement logiciel Java (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)</span><span class="sxs-lookup"><span data-stu-id="829cf-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="829cf-127">Environnement de développement intégré (IDE) Eclipse pour développeurs Java EE.</span><span class="sxs-lookup"><span data-stu-id="829cf-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="829cf-128">Un site web Azure avec un environnement d’exécution Java (Tomcat ou Jetty, par exemple) activé.</span><span class="sxs-lookup"><span data-stu-id="829cf-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="829cf-129">Si vous installez ces outils pour hello première fois, coreservlets.com fournit une vue d’ensemble du processus d’installation hello dans la section de démarrage rapide de hello de leurs [didacticiel : installation TomCat7 et son utilisation avec Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) l’article.</span><span class="sxs-lookup"><span data-stu-id="829cf-129">If you're installing these tools for hello first time, coreservlets.com provides a walk-through of hello installation process in hello Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="829cf-130"><a id="CreateDB"></a>Étape 1 : création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="829cf-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="829cf-131">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="829cf-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="829cf-132">Si vous déjà disposez d’un compte ou si vous utilisez hello Azure Cosmos DB émulateur pour ce didacticiel, vous pouvez ignorer trop[étape 2 : créer l’application de Java JSP hello](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="829cf-132">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create hello Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="829cf-133"><a id="CreateJSP"></a>Étape 2 : Créer l’application de Java JSP hello</span><span class="sxs-lookup"><span data-stu-id="829cf-133"><a id="CreateJSP"></a>Step 2: Create hello Java JSP application</span></span>
<span data-ttu-id="829cf-134">hello toocreate application JSP :</span><span class="sxs-lookup"><span data-stu-id="829cf-134">toocreate hello JSP application:</span></span>

1. <span data-ttu-id="829cf-135">Tout d'abord, nous allons commencer par la création d'un projet Java.</span><span class="sxs-lookup"><span data-stu-id="829cf-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="829cf-136">Démarrez Eclipse, puis cliquez sur **File** (Fichier), sur **New** (Nouveau), puis sur **Dynamic Web Project** (Projet web dynamique).</span><span class="sxs-lookup"><span data-stu-id="829cf-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="829cf-137">Si vous ne voyez pas **projet Web dynamique** répertorié sous forme de projet disponible, procédez comme hello suivant : cliquez sur **fichier**, cliquez sur **nouveau**, cliquez sur **projet**..., développez **Web**, cliquez sur **projet Web dynamique**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="829cf-137">If you don’t see **Dynamic Web Project** listed as an available project, do hello following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Développement d’applications Java JSP](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="829cf-139">Entrez un nom de projet Bonjour **nom du projet** zone et Bonjour **Runtime cible** menu déroulant, sélectionnez éventuellement une valeur (par exemple, Apache Tomcat v7.0), puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="829cf-139">Enter a project name in hello **Project name** box, and in hello **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="829cf-140">Sélection d’un runtime cible permet de vous toorun votre projet localement par le biais d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="829cf-140">Selecting a target runtime enables you toorun your project locally through Eclipse.</span></span>
3. <span data-ttu-id="829cf-141">Dans Eclipse, dans la vue de l’Explorateur de projets hello, développez votre projet.</span><span class="sxs-lookup"><span data-stu-id="829cf-141">In Eclipse, in hello Project Explorer view, expand your project.</span></span> <span data-ttu-id="829cf-142">Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)**, puis sur **JSP File (Fichier JSP)**.</span><span class="sxs-lookup"><span data-stu-id="829cf-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="829cf-143">Bonjour **nouveau fichier JSP** boîte de dialogue, le nom de fichier hello **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="829cf-143">In hello **New JSP File** dialog box, name hello file **index.jsp**.</span></span> <span data-ttu-id="829cf-144">Conservez le dossier parent hello **WebContent**, comme indiqué dans hello après l’illustration, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="829cf-144">Keep hello parent folder as **WebContent**, as shown in hello following illustration, and then click **Next**.</span></span>
   
    ![Création d’un fichier JSP - Didacticiel d’application web Java](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="829cf-146">Bonjour **sélectionner un modèle JSP** boîte de dialogue, à des fins de hello de ce didacticiel, sélectionnez **nouveau fichier JSP (html)**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="829cf-146">In hello **Select JSP Template** dialog box, for hello purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="829cf-147">Lorsque le fichier de hello index.jsp s’ouvre dans Eclipse, ajoutez le texte toodisplay **Hello World !**</span><span class="sxs-lookup"><span data-stu-id="829cf-147">When hello index.jsp file opens in Eclipse, add text toodisplay **Hello World!**</span></span> <span data-ttu-id="829cf-148">dans hello existant <body> élément.</span><span class="sxs-lookup"><span data-stu-id="829cf-148">within hello existing <body> element.</span></span> <span data-ttu-id="829cf-149">Votre mise à jour <body> contenu doit ressembler à hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="829cf-149">Your updated <body> content should look like hello following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="829cf-150">Enregistrez le fichier index.jsp de hello.</span><span class="sxs-lookup"><span data-stu-id="829cf-150">Save hello index.jsp file.</span></span>
8. <span data-ttu-id="829cf-151">Si vous définissez un runtime cible à l’étape 2, vous pouvez cliquer sur **projet** , puis **exécuter** toorun localement votre application JSP :</span><span class="sxs-lookup"><span data-stu-id="829cf-151">If you set a target runtime in step 2, you can click **Project** and then **Run** toorun your JSP application locally:</span></span>
   
    ![Hello World – Didacticiel d’application Java](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="829cf-153"><a id="InstallSDK"></a>Étape 3 : Installer hello DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="829cf-153"><a id="InstallSDK"></a>Step 3: Install hello DocumentDB Java SDK</span></span>
<span data-ttu-id="829cf-154">Bonjour toopull de façon plus simple de hello DocumentDB Java SDK et ses dépendances est via [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="829cf-154">hello easiest way toopull in hello DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="829cf-155">toodo, vous devez tooconvert votre projet de maven tooa en effectuant hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="829cf-155">toodo this, you will need tooconvert your project tooa maven project by completing hello following steps:</span></span>

1. <span data-ttu-id="829cf-156">Avec le bouton droit de votre projet dans l’Explorateur de projets de hello, cliquez sur **configurer**, cliquez sur **convertir tooMaven projet**.</span><span class="sxs-lookup"><span data-stu-id="829cf-156">Right-click your project in hello Project Explorer, click **Configure**, click **Convert tooMaven Project**.</span></span>
2. <span data-ttu-id="829cf-157">Bonjour **créer nouveau POM** fenêtre, acceptez les valeurs par défaut hello et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="829cf-157">In hello **Create new POM** window, accept hello defaults and click **Finish**.</span></span>
3. <span data-ttu-id="829cf-158">Dans **Explorateur de projets**, ouvrez fichier pom.xml de hello.</span><span class="sxs-lookup"><span data-stu-id="829cf-158">In **Project Explorer**, open hello pom.xml file.</span></span>
4. <span data-ttu-id="829cf-159">Sur hello **dépendances** onglet hello **dépendances** volet, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="829cf-159">On hello **Dependencies** tab, in hello **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="829cf-160">Bonjour **sélectionner une dépendance** fenêtre, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="829cf-160">In hello **Select Dependency** window, do hello following:</span></span>
   
   * <span data-ttu-id="829cf-161">Bonjour **Id de groupe** , entrez com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="829cf-161">In hello **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="829cf-162">Bonjour **Id d’artefact** , entrez azure documentdb.</span><span class="sxs-lookup"><span data-stu-id="829cf-162">In hello **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="829cf-163">Bonjour **Version** , entrez 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="829cf-163">In hello **Version** box, enter 1.5.1.</span></span>
     
   ![Installation du Kit de développement logiciel (SDK) d’applications Java DocumentDB](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="829cf-165">Ou ajouter une dépendance de hello XML pour l’Id de groupe et l’Id d’artefact directement toohello pom.xml via un éditeur de texte :</span><span class="sxs-lookup"><span data-stu-id="829cf-165">Or add hello dependency XML for Group Id and Artifact Id directly toohello pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="829cf-166"><dependency><groupId>com.microsoft.azure</groupId><artifactId>azure-documentdb</artifactId><version>1.9.1</version></dependency></span><span class="sxs-lookup"><span data-stu-id="829cf-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="829cf-167">Cliquez sur **OK** et Maven installera hello DocumentDB Java SDK.</span><span class="sxs-lookup"><span data-stu-id="829cf-167">Click **OK** and Maven will install hello DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="829cf-168">Enregistrez le fichier de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="829cf-168">Save hello pom.xml file.</span></span>

## <span data-ttu-id="829cf-169"><a id="UseService"></a>Étape 4 : À l’aide de service de base de données Azure Cosmos hello dans une application Java</span><span class="sxs-lookup"><span data-stu-id="829cf-169"><a id="UseService"></a>Step 4: Using hello Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="829cf-170">Tout d’abord, nous allons définir objet TodoItem de hello dans TodoItem.java :</span><span class="sxs-lookup"><span data-stu-id="829cf-170">First, let's define hello TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="829cf-171">Dans ce projet, nous utilisons [Lombok du projet](http://projectlombok.org/) toogenerate hello constructeur, accesseurs Get, Set et un générateur.</span><span class="sxs-lookup"><span data-stu-id="829cf-171">In this project, we are using [Project Lombok](http://projectlombok.org/) toogenerate hello constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="829cf-172">Ou bien, vous pouvez écrire ce code manuellement ou laisser hello IDE sa génération.</span><span class="sxs-lookup"><span data-stu-id="829cf-172">Alternatively, you can write this code manually or have hello IDE generate it.</span></span>
2. <span data-ttu-id="829cf-173">service de base de données Azure Cosmos tooinvoke hello, vous devez instancier un nouvel **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="829cf-173">tooinvoke hello Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="829cf-174">En règle générale, il s’agit des meilleures tooreuse hello **DocumentClient** - plutôt que de construire un nouveau client pour chaque demande ultérieure.</span><span class="sxs-lookup"><span data-stu-id="829cf-174">In general, it is best tooreuse hello **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="829cf-175">Nous pouvons réutiliser client de hello en encapsulant client hello dans un **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="829cf-175">We can reuse hello client by wrapping hello client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="829cf-176">Dans DocumentClientFactory.java, vous devez vous avez enregistré le Presse-papiers tooyour dans valeur d’URI et la clé primaire de hello toopaste [étape 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="829cf-176">In DocumentClientFactory.java, you need toopaste hello URI and PRIMARY KEY value you saved tooyour clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="829cf-177">Remplacez [YOUR\_ENDPOINT\_HERE] par l’URI et [YOUR\_KEY\_HERE] par votre CLÉ PRIMAIRE.</span><span class="sxs-lookup"><span data-stu-id="829cf-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="829cf-178">Maintenant nous allons créer un tooabstract objet d’accès aux données (DAO) conserver notre tooAzure d’éléments ToDo Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="829cf-178">Now let's create a Data Access Object (DAO) tooabstract persisting our ToDo items tooAzure Cosmos DB.</span></span>
   
    <span data-ttu-id="829cf-179">Commander les éléments de tâche toosave tooa collection, hello client a besoin de tooknow le toopersist collecte et de la base de données trop (référencé par Self-Link).</span><span class="sxs-lookup"><span data-stu-id="829cf-179">In order toosave ToDo items tooa collection, hello client needs tooknow which database and collection toopersist too(as referenced by self-links).</span></span> <span data-ttu-id="829cf-180">En règle générale, il s’agit de collecte lorsque cela est possible et base de données de meilleure toocache hello toohello base de données des allers-retours supplémentaires tooavoid.</span><span class="sxs-lookup"><span data-stu-id="829cf-180">In general, it is best toocache hello database and collection when possible tooavoid additional round-trips toohello database.</span></span>
   
    <span data-ttu-id="829cf-181">Hello de code suivant illustre comment tooretrieve notre base de données et de la collection, si elle existe, ou créez-en un nouveau si elle n’existe pas :</span><span class="sxs-lookup"><span data-stu-id="829cf-181">hello following code illustrates how tooretrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="829cf-182">étape suivante de Hello est toowrite certaines hello toopersist de code TodoItems dans toohello collection.</span><span class="sxs-lookup"><span data-stu-id="829cf-182">hello next step is toowrite some code toopersist hello TodoItems in toohello collection.</span></span> <span data-ttu-id="829cf-183">Dans cet exemple, nous allons utiliser [Gson](https://code.google.com/p/google-gson/) tooserialize et désérialiser des documents tooJSON TodoItem brut objets Java ancien (POJO).</span><span class="sxs-lookup"><span data-stu-id="829cf-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) tooserialize and de-serialize TodoItem Plain Old Java Objects (POJOs) tooJSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="829cf-184">De même que les collections et les bases de données Azure Cosmos DB, les documents sont référencés par des liens réflexifs.</span><span class="sxs-lookup"><span data-stu-id="829cf-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="829cf-185">Hello suivant permet de fonction d’assistance que nous récupérer les documents par un autre attribut (par exemple, « id ») au lieu de l’élément Self-link :</span><span class="sxs-lookup"><span data-stu-id="829cf-185">hello following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. <span data-ttu-id="829cf-186">Nous pouvons utiliser la méthode d’assistance de hello dans l’étape 5 tooretrieve un document TodoItem JSON par id et de le désérialiser tooa POJO :</span><span class="sxs-lookup"><span data-stu-id="829cf-186">We can use hello helper method in step 5 tooretrieve a TodoItem JSON document by id and then deserialize it tooa POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="829cf-187">Nous pouvons également utiliser hello DocumentClient tooget une collection ou une liste de TodoItems à l’aide de SQL de DocumentDB :</span><span class="sxs-lookup"><span data-stu-id="829cf-187">We can also use hello DocumentClient tooget a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="829cf-188">Il existe de nombreuses façons tooupdate un document avec hello DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="829cf-188">There are many ways tooupdate a document with hello DocumentClient.</span></span> <span data-ttu-id="829cf-189">Dans notre application de liste Todo, nous souhaitons tootoggle en mesure de toobe si un objet TodoItem est terminé.</span><span class="sxs-lookup"><span data-stu-id="829cf-189">In our Todo list application, we want toobe able tootoggle whether a TodoItem is complete.</span></span> <span data-ttu-id="829cf-190">Cela peut être obtenue en mettant à jour d’attribut de « terminée » hello dans le document de hello :</span><span class="sxs-lookup"><span data-stu-id="829cf-190">This can be achieved by updating hello "complete" attribute within hello document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="829cf-191">Enfin, nous souhaitons hello capacité toodelete un TodoItem de notre liste.</span><span class="sxs-lookup"><span data-stu-id="829cf-191">Finally, we want hello ability toodelete a TodoItem from our list.</span></span> <span data-ttu-id="829cf-192">toodo, nous pouvons utiliser la méthode d’assistance de hello nous a écrit précédemment tooretrieve hello Self-link et alors indiquer au hello client toodelete il :</span><span class="sxs-lookup"><span data-stu-id="829cf-192">toodo this, we can use hello helper method we wrote earlier tooretrieve hello self-link and then tell hello client toodelete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="829cf-193"><a id="Wire"></a>Étape 5 : Ensemble reste hello Hello du projet de développement d’applications Java de câblage</span><span class="sxs-lookup"><span data-stu-id="829cf-193"><a id="Wire"></a>Step 5: Wiring hello rest of hello of Java application development project together</span></span>
<span data-ttu-id="829cf-194">Maintenant que nous avons terminé fun de hello bits - tout ce qui reste est toobuild une interface utilisateur rapide et le connecter tooour DAO.</span><span class="sxs-lookup"><span data-stu-id="829cf-194">Now that we've finished hello fun bits - all that's left is toobuild a quick user interface and wire it up tooour DAO.</span></span>

1. <span data-ttu-id="829cf-195">Tout d’abord, nous pouvons commencer à la création d’un contrôleur toocall notre DAO :</span><span class="sxs-lookup"><span data-stu-id="829cf-195">First, let's start with building a controller toocall our DAO:</span></span>
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    <span data-ttu-id="829cf-196">Dans une application plus complexe, le contrôleur de hello peut héberger la logique métier complexe par-dessus hello DAO.</span><span class="sxs-lookup"><span data-stu-id="829cf-196">In a more complex application, hello controller may house complicated business logic on top of hello DAO.</span></span>
2. <span data-ttu-id="829cf-197">Ensuite, nous allons créer un contrôleur de servlet tooroute HTTP demandes toohello :</span><span class="sxs-lookup"><span data-stu-id="829cf-197">Next, we'll create a servlet tooroute HTTP requests toohello controller:</span></span>
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. <span data-ttu-id="829cf-198">Nous avons besoin d’un utilisateur de toohello toodisplay interface web utilisateur.</span><span class="sxs-lookup"><span data-stu-id="829cf-198">We'll need a web user interface toodisplay toohello user.</span></span> <span data-ttu-id="829cf-199">Nous allons réécrire hello index.jsp créée précédemment :</span><span class="sxs-lookup"><span data-stu-id="829cf-199">Let's re-write hello index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="829cf-200">Et enfin, écrire une interface utilisateur de côté client JavaScript tootie hello web et hello servlet ensemble :</span><span class="sxs-lookup"><span data-stu-id="829cf-200">And finally, write some client-side JavaScript tootie hello web user interface and hello servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. <span data-ttu-id="829cf-201">Génial !</span><span class="sxs-lookup"><span data-stu-id="829cf-201">Awesome!</span></span> <span data-ttu-id="829cf-202">Tout ce qui reste est maintenant application hello de tootest.</span><span class="sxs-lookup"><span data-stu-id="829cf-202">Now all that's left is tootest hello application.</span></span> <span data-ttu-id="829cf-203">Exécuter des application hello localement et ajouter des éléments de tâche en remplissant la catégorie et le nom de l’élément hello en cliquant sur **ajouter une tâche**.</span><span class="sxs-lookup"><span data-stu-id="829cf-203">Run hello application locally, and add some Todo items by filling in hello item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="829cf-204">Une fois que l’élément de hello s’affiche, vous pouvez mettre à jour si elle est terminée en activant la case à cocher hello en cliquant sur **mettre à jour les tâches**.</span><span class="sxs-lookup"><span data-stu-id="829cf-204">Once hello item appears, you can update whether it's complete by toggling hello checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="829cf-205"><a id="Deploy"></a>Étape 6 : Déployer votre tooAzure d’application Java Sites Web</span><span class="sxs-lookup"><span data-stu-id="829cf-205"><a id="Deploy"></a>Step 6: Deploy your Java application tooAzure Web Sites</span></span>
<span data-ttu-id="829cf-206">Les Sites Web Azure permettent de déployer facilement des applications Java en les exportant sous forme de fichiers WAR et en les chargeant par le biais du contrôle de code source (GIT, par exemple) ou par FTP.</span><span class="sxs-lookup"><span data-stu-id="829cf-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="829cf-207">tooexport votre application sous forme de fichier WAR, avec le bouton droit sur votre projet dans **Explorateur de projets**, cliquez sur **exporter**, puis cliquez sur **le fichier WAR**.</span><span class="sxs-lookup"><span data-stu-id="829cf-207">tooexport your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="829cf-208">Bonjour **WAR exporter** fenêtre, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="829cf-208">In hello **WAR Export** window, do hello following:</span></span>
   
   * <span data-ttu-id="829cf-209">Dans la zone de projet Web hello, entrez exemple azure-documentdb-java.</span><span class="sxs-lookup"><span data-stu-id="829cf-209">In hello Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="829cf-210">Dans la zone de Destination hello, choisissez un fichier WAR de destination toosave hello.</span><span class="sxs-lookup"><span data-stu-id="829cf-210">In hello Destination box, choose a destination toosave hello WAR file.</span></span>
   * <span data-ttu-id="829cf-211">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="829cf-211">Click **Finish**.</span></span>
3. <span data-ttu-id="829cf-212">Maintenant que vous avez un fichier WAR dans main, vous pouvez simplement télécharger tooyour Site Web Azure **webapps** active.</span><span class="sxs-lookup"><span data-stu-id="829cf-212">Now that you have a WAR file in hand, you can simply upload it tooyour Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="829cf-213">Pour obtenir des instructions sur le téléchargement du fichier de hello, consultez [ajouter un tooAzure d’application Java App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="829cf-213">For instructions on uploading hello file, see [Add a Java application tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="829cf-214">Une fois le fichier WAR hello toohello téléchargé WebApp active, l’environnement d’exécution hello détectera que vous l’avez ajouté et chargez automatiquement.</span><span class="sxs-lookup"><span data-stu-id="829cf-214">Once hello WAR file is uploaded toohello webapps directory, hello runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="829cf-215">tooview votre produit fini, accédez toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ et commencez à ajouter vos tâches !</span><span class="sxs-lookup"><span data-stu-id="829cf-215">tooview your finished product, navigate toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="829cf-216"><a id="GetProject"></a>Obtenir le projet de hello à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="829cf-216"><a id="GetProject"></a>Get hello project from GitHub</span></span>
<span data-ttu-id="829cf-217">Tous les exemples hello dans ce didacticiel sont inclus dans hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projet sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="829cf-217">All hello samples in this tutorial are included in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="829cf-218">projet de todo tooimport hello dans Eclipse, assurez-vous d’avoir les logiciels hello et les ressources répertoriées dans hello [conditions préalables](#Prerequisites) section, puis hello suivant :</span><span class="sxs-lookup"><span data-stu-id="829cf-218">tooimport hello todo project into Eclipse, ensure you have hello software and resources listed in hello [Prerequisites](#Prerequisites) section, then do hello following:</span></span>

1. <span data-ttu-id="829cf-219">Installez [Project Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="829cf-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="829cf-220">Lombok est utilisé toogenerate constructeurs, accesseurs Get, SET dans le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="829cf-220">Lombok is used toogenerate constructors, getters, setters in hello project.</span></span> <span data-ttu-id="829cf-221">Une fois que vous avez téléchargé le fichier de lombok.jar hello, double-cliquez dessus tooinstall il ou installez-le à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="829cf-221">Once you have downloaded hello lombok.jar file, double-click it tooinstall it or install it from hello command line.</span></span>
2. <span data-ttu-id="829cf-222">Si Eclipse est ouvert, fermez-le et redémarrez-le tooload Lombok.</span><span class="sxs-lookup"><span data-stu-id="829cf-222">If Eclipse is open, close it and restart it tooload Lombok.</span></span>
3. <span data-ttu-id="829cf-223">Dans Eclipse, sur hello **fichier** menu, cliquez sur **importation**.</span><span class="sxs-lookup"><span data-stu-id="829cf-223">In Eclipse, on hello **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="829cf-224">Bonjour **importation** fenêtre, cliquez sur **Git**, cliquez sur **projets à partir de Git**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="829cf-224">In hello **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="829cf-225">Sur hello **sélectionner une Source de référentiel** , cliquez sur **Clone URI**.</span><span class="sxs-lookup"><span data-stu-id="829cf-225">On hello **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="829cf-226">Sur hello **référentiel de code Source Git** écran, Bonjour **URI** zone, entrez https://github.com/Azure-Samples/java-todo-app.git, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="829cf-226">On hello **Source Git Repository** screen, in hello **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="829cf-227">Sur hello **sélection de la branche** écran, vérifiez que **master** est sélectionné, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="829cf-227">On hello **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="829cf-228">Sur hello **Local de Destination** , cliquez sur **Parcourir** tooselect un dossier dans lequel les référentiel hello peuvent être copiés, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="829cf-228">On hello **Local Destination** screen, click **Browse** tooselect a folder where hello repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="829cf-229">Sur hello **sélectionner un toouse de l’Assistant pour importer des projets** écran, vérifiez que **importer des projets existants** est sélectionné, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="829cf-229">On hello **Select a wizard toouse for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="829cf-230">Sur hello **importation projets** écran, désélectionnez hello **DocumentDB** de projet, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="829cf-230">On hello **Import Projects** screen, unselect hello **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="829cf-231">projet de DocumentDB Hello contient hello Azure Cosmos DB Java SDK, nous allons ajouter en tant que dépendance à la place.</span><span class="sxs-lookup"><span data-stu-id="829cf-231">hello DocumentDB project contains hello Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="829cf-232">Dans **Explorateur de projets**, accédez tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java et remplacer des valeurs d’hôte et MASTER_KEY hello avec hello URI et une clé primaire pour votre compte de base de données Azure Cosmos, puis enregistrer le fichier hello.</span><span class="sxs-lookup"><span data-stu-id="829cf-232">In **Project Explorer**, navigate tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace hello HOST and MASTER_KEY values with hello URI and PRIMARY KEY for your Azure Cosmos DB account, and then save hello file.</span></span> <span data-ttu-id="829cf-233">Pour plus d'informations, consultez l'[Étape 1. Créez un compte de base de données Azure Cosmos DB](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="829cf-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="829cf-234">Dans **Explorateur de projets**, cliquez avec le bouton droit sur hello **documentdb azure-exemple java**, cliquez sur **générer le chemin d’accès**, puis cliquez sur **configurer Build chemin d’accès**.</span><span class="sxs-lookup"><span data-stu-id="829cf-234">In **Project Explorer**, right click hello **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="829cf-235">Sur hello **chemin d’accès de Build Java** de l’écran, dans le volet droit de hello, sélectionnez hello **bibliothèques** onglet, puis cliquez sur **ajouter le fichiers JAR externe**.</span><span class="sxs-lookup"><span data-stu-id="829cf-235">On hello **Java Build Path** screen, in hello right pane, select hello **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="829cf-236">Accédez emplacement toohello du fichier de lombok.jar hello, puis cliquez sur **ouvrir**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="829cf-236">Navigate toohello location of hello lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="829cf-237">Hello d’utilisation étape 12 tooopen **propriétés** à nouveau, fenêtre, puis dans le volet gauche de hello cliquez sur **ciblée des Runtimes**.</span><span class="sxs-lookup"><span data-stu-id="829cf-237">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="829cf-238">Sur hello **ciblée des Runtimes** , cliquez sur **nouveau**, sélectionnez **Apache Tomcat v7.0**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="829cf-238">On hello **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="829cf-239">Hello de tooopen utilisation étape 12 **propriétés** fenêtre à nouveau, puis dans le volet gauche de hello cliquez sur **facettes de projet**.</span><span class="sxs-lookup"><span data-stu-id="829cf-239">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="829cf-240">Sur hello **projet facettes** écran, sélectionnez **Module Web dynamique** et **Java**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="829cf-240">On hello **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="829cf-241">Sur hello **serveurs** onglet bas hello écran hello, avec le bouton droit **Tomcat v7.0 serveur à localhost** puis cliquez sur **ajouter et supprimer des**.</span><span class="sxs-lookup"><span data-stu-id="829cf-241">On hello **Servers** tab at hello bottom of hello screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="829cf-242">Sur hello **ajouter et supprimer des** fenêtre, déplacer **documentdb azure-exemple java** toohello **configuré** zone, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="829cf-242">On hello **Add and Remove** window, move **azure-documentdb-java-sample** toohello **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="829cf-243">Bonjour **serveurs** droit **Tomcat v7.0 serveur à localhost**, puis cliquez sur **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="829cf-243">In hello **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="829cf-244">Dans un navigateur, accédez à toohttp://localhost:8080 / documentdb azure-exemple java / et commencer à ajouter la liste des tâches tooyour.</span><span class="sxs-lookup"><span data-stu-id="829cf-244">In a browser, navigate toohttp://localhost:8080/azure-documentdb-java-sample/ and start adding tooyour task list.</span></span> <span data-ttu-id="829cf-245">Notez que si vous avez modifié les valeurs de port par défaut, modifiez la valeur de toohello de 8080 que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="829cf-245">Note that if you changed your default port values, change 8080 toohello value you selected.</span></span>
22. <span data-ttu-id="829cf-246">reportez-vous à votre projet de tooan les site web Azure, toodeploy [étape 6. Déployer votre application de tooAzure Sites Web](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="829cf-246">toodeploy your project tooan Azure web site, see [Step 6. Deploy your application tooAzure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
