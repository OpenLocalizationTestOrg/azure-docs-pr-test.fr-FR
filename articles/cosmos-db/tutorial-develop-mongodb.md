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
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a>Azure Cosmos DB : Se connecter à application de MongoDB tooa à l’aide de .NET

Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur. 

Ce didacticiel montre comment un compte de base de données Azure Cosmos à l’aide de toocreate hello portail Azure, et comment toocreate une base de données et les données de toostore de collection à l’aide de hello [MongoDB API](mongodb-introduction.md). 

Ce didacticiel couvre hello tâches suivantes :

> [!div class="checklist"]
> * Création d’un compte Azure Cosmos DB 
> * Mettre à jour votre chaîne de connexion
> * Créer une application MongoDB sur une machine virtuelle 


## <a name="create-a-database-account"></a>Création d'un compte de base de données

Commençons par la création d’un compte de base de données Azure Cosmos Bonjour portail Azure.  

> [!TIP]
> * Possédez-vous un compte Azure Cosmos DB ? Dans ce cas, passez directement trop[configurer votre solution Visual Studio](#SetupVS)
> * Possédiez-vous un compte Azure DocumentDB ? Si votre compte est maintenant un compte de base de données Azure Cosmos, et que vous pouvez passer trop[configurer votre solution Visual Studio](#SetupVS).  
> * Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[configurer votre Solution Visual Studio](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a>Mise à jour de votre chaîne de connexion

1. Bonjour portail Azure, Bonjour **base de données Azure Cosmos** , sélectionnez API hello pour MongoDB compte. 
2. Dans la barre de gauche hello du Panneau de compte hello, cliquez sur **démarrage rapide**. 
3. Choisissez votre plateforme (*Pilote .NET*, *Pilote Node.js*, *Pilote MongoDB*, *Pilote Java*, *Pilote Python*). Si votre pilote ou outil n'est pas répertorié, ne vous inquiétez pas, nous développons en permanence d'autres extraits de code de connexion. 
4. Copiez et collez l’extrait de code hello dans votre application MongoDB, et que vous êtes prêt toogo.

## <a name="set-up-your-mongodb-app"></a>Configurer votre application MongoDB

Vous pouvez utiliser hello [créer une application web dans Azure qui se connecte tooMongoDB en cours d’exécution sur un ordinateur virtuel](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) (didacticiel), avec une modification minimale, le programme d’installation de tooquickly une application MongoDB (soit localement ou publié tooan Azure web) qui se connecte API tooan pour MongoDB compte.  

1. Suivez le didacticiel hello, avec une modification.  Remplacez le code de Dal.cs hello avec ce :

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

2. Modifiez hello suivant des variables dans le fichier de Dal.cs hello par les paramètres de votre compte à partir de la page de clés hello Bonjour portail Azure :

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. Utilisez l’application hello !

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’allez toocontinue toouse cette application, utilisez hello suivant toodelete suit toutes les ressources créées par ce didacticiel Bonjour portail Azure. 

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé. 
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Création d’un compte Azure Cosmos DB 
> * Mettre à jour votre chaîne de connexion
> * Créer une application MongoDB sur une machine virtuelle

Vous pouvez continuer l’étape suivante du didacticiel toohello et importer votre tooAzure de données MongoDB Cosmos DB.  

> [!div class="nextstepaction"]
> [Importer des données MongoDB dans Azure Cosmos DB](mongodb-migrate.md)

