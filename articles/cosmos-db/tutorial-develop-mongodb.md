---
title: API de DB Cosmos aaaUse Azure pour MongoDB toobuild une application web | Documents Microsoft
description: "Un didacticiel de base de données Azure Cosmos qui crée une application web de base de données en ligne à l’aide des API de hello pour MongoDB."
keywords: exemples mongodb
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 61a2ab3a-2fc3-4d49-a263-ed87c66628f6
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 6dfa7fef49fc53ea2fcfcfbad3b3fcf97ac18e94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a><span data-ttu-id="36f97-104">Azure Cosmos DB : Se connecter à application de MongoDB tooa à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="36f97-104">Azure Cosmos DB: Connect tooa MongoDB app using .NET</span></span>

<span data-ttu-id="36f97-105">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="36f97-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="36f97-106">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="36f97-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="36f97-107">Ce didacticiel montre comment un compte de base de données Azure Cosmos à l’aide de toocreate hello portail Azure, et comment toocreate une base de données et les données de toostore de collection à l’aide de hello [MongoDB API](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="36f97-107">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and how toocreate a database and collection toostore data using hello [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="36f97-108">Ce didacticiel couvre hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="36f97-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="36f97-109">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="36f97-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="36f97-110">Mettre à jour votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="36f97-110">Update your connection string</span></span>
> * <span data-ttu-id="36f97-111">Créer une application MongoDB sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="36f97-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="36f97-112">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="36f97-112">Create a database account</span></span>

<span data-ttu-id="36f97-113">Commençons par la création d’un compte de base de données Azure Cosmos Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="36f97-113">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="36f97-114">Possédez-vous un compte Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="36f97-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="36f97-115">Dans ce cas, passez directement trop[configurer votre solution Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="36f97-115">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="36f97-116">Possédiez-vous un compte Azure DocumentDB ?</span><span class="sxs-lookup"><span data-stu-id="36f97-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="36f97-117">Si votre compte est maintenant un compte de base de données Azure Cosmos, et que vous pouvez passer trop[configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="36f97-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="36f97-118">Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[configurer votre Solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="36f97-118">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="36f97-119">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="36f97-119">Update your connection string</span></span>

1. <span data-ttu-id="36f97-120">Bonjour portail Azure, Bonjour **base de données Azure Cosmos** , sélectionnez API hello pour MongoDB compte.</span><span class="sxs-lookup"><span data-stu-id="36f97-120">In hello Azure portal, in hello **Azure Cosmos DB** page, select hello API for MongoDB account.</span></span> 
2. <span data-ttu-id="36f97-121">Dans la barre de gauche hello du Panneau de compte hello, cliquez sur **démarrage rapide**.</span><span class="sxs-lookup"><span data-stu-id="36f97-121">In hello left bar of hello account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="36f97-122">Choisissez votre plateforme (*Pilote .NET*, *Pilote Node.js*, *Pilote MongoDB*, *Pilote Java*, *Pilote Python*).</span><span class="sxs-lookup"><span data-stu-id="36f97-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="36f97-123">Si votre pilote ou outil n'est pas répertorié, ne vous inquiétez pas, nous développons en permanence d'autres extraits de code de connexion.</span><span class="sxs-lookup"><span data-stu-id="36f97-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="36f97-124">Copiez et collez l’extrait de code hello dans votre application MongoDB, et que vous êtes prêt toogo.</span><span class="sxs-lookup"><span data-stu-id="36f97-124">Copy and paste hello code snippet into your MongoDB app, and you are ready toogo.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="36f97-125">Configurer votre application MongoDB</span><span class="sxs-lookup"><span data-stu-id="36f97-125">Set up your MongoDB app</span></span>

<span data-ttu-id="36f97-126">Vous pouvez utiliser hello [créer une application web dans Azure qui se connecte tooMongoDB en cours d’exécution sur un ordinateur virtuel](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) (didacticiel), avec une modification minimale, le programme d’installation de tooquickly une application MongoDB (soit localement ou publié tooan Azure web) qui se connecte API tooan pour MongoDB compte.</span><span class="sxs-lookup"><span data-stu-id="36f97-126">You can use hello [Create a web app in Azure that connects tooMongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, tooquickly setup a MongoDB application (either locally or published tooan Azure web app) that connects tooan API for MongoDB account.</span></span>  

1. <span data-ttu-id="36f97-127">Suivez le didacticiel hello, avec une modification.</span><span class="sxs-lookup"><span data-stu-id="36f97-127">Follow hello tutorial, with one modification.</span></span>  <span data-ttu-id="36f97-128">Remplacez le code de Dal.cs hello avec ce :</span><span class="sxs-lookup"><span data-stu-id="36f97-128">Replace hello Dal.cs code with this:</span></span>

    ```csharp   
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;
    using System.Security.Authentication;
   
    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            //private MongoServer mongoServer = null;
            private bool disposed = false;
   
            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";
   
            // Default constructor.        
            public Dal()
            {
            }
   
            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }
   
            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }
   
            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
   
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            # region IDisposable
   
            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }
   
            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                    }
                }
   
                this.disposed = true;
            }
   
            # endregion
        }
    }
    ```

2. <span data-ttu-id="36f97-129">Modifiez hello suivant des variables dans le fichier de Dal.cs hello par les paramètres de votre compte à partir de la page de clés hello Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="36f97-129">Modify hello following variables in hello Dal.cs file per your account settings from hello Keys page in hello Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="36f97-130">Utilisez l’application hello !</span><span class="sxs-lookup"><span data-stu-id="36f97-130">Use hello app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="36f97-131">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="36f97-131">Clean up resources</span></span>

<span data-ttu-id="36f97-132">Si vous n’allez toocontinue toouse cette application, utilisez hello suivant toodelete suit toutes les ressources créées par ce didacticiel Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="36f97-132">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span> 

1. <span data-ttu-id="36f97-133">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="36f97-133">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="36f97-134">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="36f97-134">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36f97-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36f97-135">Next steps</span></span>

<span data-ttu-id="36f97-136">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="36f97-136">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="36f97-137">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="36f97-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="36f97-138">Mettre à jour votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="36f97-138">Update your connection string</span></span>
> * <span data-ttu-id="36f97-139">Créer une application MongoDB sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="36f97-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="36f97-140">Vous pouvez continuer l’étape suivante du didacticiel toohello et importer votre tooAzure de données MongoDB Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="36f97-140">You can proceed toohello next tutorial and import your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="36f97-141">Importer des données MongoDB dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="36f97-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

