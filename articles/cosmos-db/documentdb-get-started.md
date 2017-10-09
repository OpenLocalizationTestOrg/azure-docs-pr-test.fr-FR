---
title: "Azure Cosmos DB : Didacticiel sur la prise en main de l’API DocumentDB | Microsoft Docs"
description: "Un didacticiel qui crée une base de données en ligne et une application console c# à l’aide de hello API DocumentDB."
keywords: "didacticiel nosql, base de données en ligne, application console c#"
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a>Azure Cosmos DB : Didacticiel sur la prise en main de l’API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js pour MongoDB](mongodb-samples.md)
> * [Node.JS](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bienvenue toohello API de DocumentDB de base de données Azure Cosmos route ! À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB.

Nous allons aborder les points suivants :

* Création et connexion de compte de base de données Azure Cosmos tooan
* Configuration de votre solution Visual Studio
* Création d’une base de données en ligne
* Création d’une collection
* Création de documents JSON
* Interrogation de collection de hello
* Remplacement d'un document
* Suppression d’un document
* Suppression de la base de données hello

Vous n’avez pas le temps ? Ne vous inquiétez pas ! solution complète de Hello est disponible sur [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). Raccourcis toohello [obtenir la section de solution du didacticiel hello complète NoSQL](#GetSolution) pour obtenir des instructions rapides.

Par la suite, veuillez utiliser hello des boutons de vote haut de hello ou du bas de cette page de toogive nous vos commentaires. Si vous souhaitez que nous toocontact vous directement, vous pouvez tooinclude libre votre adresse de messagerie dans vos commentaires.

Commençons dès maintenant !

## <a name="prerequisites"></a>Composants requis
Vérifiez que vous avez hello suivantes :

* Un compte Azure actif. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/). 
    * Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) pour ce didacticiel.
* [Visual Studio Community 2017](http://www.visualstudio.com/).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Étape 1 : créer un compte Azure Cosmos DB
Commençons par créer un compte Azure Cosmos DB. Si vous avez déjà un compte que vous souhaitez toouse, vous pouvez passer trop[le programme d’installation de votre Solution Visual Studio](#SetupVS). Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[le programme d’installation de votre Solution Visual Studio](#SetupVS).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Étape 2 : configurer votre solution Visual Studio
1. Ouvrez **Visual Studio 2017** sur votre ordinateur.
2. Sur hello **fichier** menu, sélectionnez **nouveau**, puis choisissez **projet**.
3. Bonjour **nouveau projet** boîte de dialogue, sélectionnez **modèles** / **Visual C#** / **Application Console**, nom votre projet, puis cliquez sur **OK**.
   ![Capture d’écran de la fenêtre de nouveau projet hello](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)
4. Bonjour **l’Explorateur de solutions**, cliquez avec le bouton droit sur votre nouvelle application console qui se trouve sous votre solution Visual Studio, et puis cliquez sur **gérer les Packages NuGet...**
    
    ![Capture d’écran de hello droite Menu Clicked hello projet](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. Bonjour **Nuget** , cliquez sur **Parcourir**et le type **azure documentdb** dans la zone de recherche hello.
6. Dans les résultats de hello, recherchez **Microsoft.Azure.DocumentDB** et cliquez sur **installer**.
   ID de package Hello pour hello Azure Cosmos DB DocumentDB API Client Library est [bibliothèque cliente de Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).
   ![Capture d’écran de hello Menu de Nuget pour la recherche de base de données Client SDK Azure Cosmos](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)

    Si vous obtenez un message sur la vérification des modifications toohello solution, cliquez sur **OK**. Si vous obtenez un message concernant l’acceptation de la licence, cliquez sur **J’accepte**.

Parfait ! Maintenant que nous avons terminé le programme d’installation Bonjour, nous pouvons commencer l’écriture du code. Vous trouverez le projet de code complet de ce didacticiel dans [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).

## <a id="Connect"></a>Étape 3 : Relier le compte de base de données Azure Cosmos tooan
Tout d’abord, ajoutez ces références début toohello de votre application c#, dans le fichier Program.cs de hello :

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> Dans le didacticiel de commande toocomplete hello, assurez-vous que vous ajoutez des dépendances hello ci-dessus.
> 
> 

Maintenant, ajoutez ces deux constantes et votre variable *client* dans votre classe publique *Program*.

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

Ensuite, head sauvegarde toohello [Azure Portal](https://portal.azure.com) tooretrieve votre URL de point de terminaison et la clé primaire. URL de point de terminaison Hello et la clé primaire sont nécessaires pour votre application toounderstand où tooconnect et de base de données Azure Cosmos tootrust connexion de votre application.

Dans hello portail Azure, accédez de compte de base de données Azure Cosmos tooyour, puis cliquez sur **clés**.

Copiez hello URI à partir du portail de hello, puis collez-la dans `<your endpoint URL>` dans le fichier program.cs de hello. Copie hello clé primaire à partir du portail de hello et collez-la dans `<your primary key>`.

![Capture d’écran de hello portail Azure utilisée par hello toocreate de didacticiel NoSQL une application console c#. Indique une base de données Azure Cosmos compte, avec un concentrateur actif de hello mis en surbrillance, hello bouton les clés de mise en surbrillance dans le panneau de compte de base de données Azure Cosmos hello et valeurs d’URI, clés primaires et secondaires hello mis en surbrillance sur hello Panneau de clés][keys]

Ensuite, nous allons commencer application hello en créant une nouvelle instance de hello **DocumentClient**.

Ci-dessous hello **principal** méthode, ajoutez cette nouvelle tâche asynchrone appelée **GetStartedDemo**, qui instancie notre nouveau **DocumentClient**.

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

Ajouter le code suivant de hello toorun votre tâche asynchrone à partir de votre **Main** (méthode). Hello **Main** méthode intercepter les exceptions et les écrire toohello console.

    static void Main(string[] args)
    {
            // ADD THIS PART tooYOUR CODE
            try
            {
                    Program p = new Program();
                    p.GetStartedDemo().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key tooexit.");
                    Console.ReadKey();
            }

Appuyez sur **F5** toorun votre application. sortie de la fenêtre console Hello affiche le message de type hello `End of demo, press any key tooexit.` confirmant que la connexion de hello a été effectuée.  Vous pouvez ensuite fermer la fenêtre de console hello. 

Félicitations ! Vous avez correctement connecté le compte de base de données Azure Cosmos tooan, maintenant examinons une utilisation des ressources de base de données Azure Cosmos.  

## <a name="step-4-create-a-database"></a>Étape 4 : créer une base de données
Avant d’ajouter de code hello pour la création d’une base de données, ajoutez une méthode d’assistance pour l’écriture de toohello console.

Copiez et collez hello **WriteToConsoleAndPromptToContinue** méthode après hello **GetStartedDemo** (méthode).

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Votre base de données Azure Cosmos [base de données](documentdb-resources.md#databases) peuvent être créés à l’aide de hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) méthode Hello **DocumentClient** classe. Une base de données est un conteneur logique de hello JSON de stockage de documents partitionné entre des collections.

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après la création du client hello. Ce faisant, vous créez la base de données *FamilyDB*.

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

Appuyez sur **F5** toorun votre application.

Félicitations ! Vous avez créé une base de données Azure Cosmos DB.  

## <a id="CreateColl"></a>Étape 5 : créer une collection
> [!WARNING]
> **CreateDocumentCollectionIfNotExistsAsync** crée une collection avec un débit réservé, ce qui a des conséquences sur la tarification. Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

A [collection](documentdb-resources.md#collections) peuvent être créés à l’aide de hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) méthode Hello **DocumentClient** classe. Une collection est un conteneur de documents JSON. Elle est associée à une logique d'application JavaScript.

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après la création de base de données hello. Ce faisant, vous créez la collection de documents *FamilyCollection*.

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

Appuyez sur **F5** toorun votre application.

Félicitations ! Vous avez créé une collection de documents Azure Cosmos DB.  

## <a id="CreateDoc"></a>Étape 6 : Création de documents JSON
A [document](documentdb-resources.md#documents) peuvent être créés à l’aide de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) méthode Hello **DocumentClient** classe. Les documents correspondent à du contenu JSON (arbitraire) défini par l'utilisateur. Nous pouvons maintenant insérer un ou plusieurs documents. Si vous avez déjà des données que vous souhaitez toostore dans votre base de données, vous pouvez utiliser hello Azure Cosmos DB [l’outil de Migration de données](import-data.md) tooimport les données de salutation dans une base de données.

Tout d’abord, nous devons toocreate un **famille** classe représentant des objets stockés dans la base de données Azure Cosmos dans cet exemple. Nous allons également créer les sous-classes **Parent**, **Child**, **Pet** et **Address** qui seront utilisées dans **Family**. Notez que les documents doivent avoir une propriété **Id** sérialisée comme **id** dans JSON. Créer ces classes en ajoutant hello suivant sous-classes internes après hello **GetStartedDemo** (méthode).

Copiez et collez hello **famille**, **Parent**, **enfant**, **animal de compagnie**, et **adresse** classes après hello **WriteToConsoleAndPromptToContinue** (méthode).

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
    }

    // ADD THIS PART tooYOUR CODE
    public class Family
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        public string LastName { get; set; }
        public Parent[] Parents { get; set; }
        public Child[] Children { get; set; }
        public Address Address { get; set; }
        public bool IsRegistered { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class Parent
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
    }

    public class Child
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
        public string Gender { get; set; }
        public int Grade { get; set; }
        public Pet[] Pets { get; set; }
    }

    public class Pet
    {
        public string GivenName { get; set; }
    }

    public class Address
    {
        public string State { get; set; }
        public string County { get; set; }
        public string City { get; set; }
    }

Copiez et collez hello **CreateFamilyDocumentIfNotExists** méthode sous votre **adresse** classe.

    // ADD THIS PART tooYOUR CODE
    private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
            this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
                this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
            }
            else
            {
                throw;
            }
        }
    }

Et insérez les deux documents, un pour chacun des hello Andersen famille et hello Wakefield famille.

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après la création de la collection de document hello.

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART tooYOUR CODE
    Family andersenFamily = new Family
    {
            Id = "Andersen.1",
            LastName = "Andersen",
            Parents = new Parent[]
            {
                    new Parent { FirstName = "Thomas" },
                    new Parent { FirstName = "Mary Kay" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FirstName = "Henriette Thaulow",
                            Gender = "female",
                            Grade = 5,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Fluffy" }
                            }
                    }
            },
            Address = new Address { State = "WA", County = "King", City = "Seattle" },
            IsRegistered = true
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

    Family wakefieldFamily = new Family
    {
            Id = "Wakefield.7",
            LastName = "Wakefield",
            Parents = new Parent[]
            {
                    new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                    new Parent { FamilyName = "Miller", FirstName = "Ben" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FamilyName = "Merriam",
                            FirstName = "Jesse",
                            Gender = "female",
                            Grade = 8,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Goofy" },
                                    new Pet { GivenName = "Shadow" }
                            }
                    },
                    new Child
                    {
                            FamilyName = "Miller",
                            FirstName = "Lisa",
                            Gender = "female",
                            Grade = 1
                    }
            },
            Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
            IsRegistered = false
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

Appuyez sur **F5** toorun votre application.

Félicitations ! Vous avez créé deux documents Azure Cosmos DB.  

![Diagramme illustrant relation hiérarchique hello entre le compte de hello, base de données en ligne hello, la collection de hello et documents hello utilisés par hello toocreate de didacticiel NoSQL une application console c#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Étape 7 : interroger les ressources Azure Cosmos DB
Azure Cosmos DB prend en charge les [requêtes](documentdb-sql-query.md) enrichies sur les documents JSON stockés dans chaque collection.  Hello exemple de code suivant montre différentes requêtes - à l’aide de la base de données SQL Azure Cosmos syntaxe ainsi que LINQ - ce que nous pouvons exécuter par rapport aux documents que nous insérés à l’étape précédente de hello hello.

Copiez et collez hello **ExecuteSimpleQuery** méthode après votre **CreateFamilyDocumentIfNotExists** (méthode).

    // ADD THIS PART tooYOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find hello Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute hello same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après la création d’un deuxième document hello.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Appuyez sur **F5** toorun votre application.

Félicitations ! Vous avez interrogé une collection Azure Cosmos DB.

Hello diagramme suivant illustre la requête SQL de base de données Azure Cosmos de hello syntaxe est appelée sur la collection de hello créée et hello même logique s’applique également les requêtes LINQ toohello.

![Diagramme illustrant la portée de hello et la signification de la requête de hello utilisé par toocreate de didacticiel hello NoSQL, une application console c#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

Hello [FROM](documentdb-sql-query.md#FromClause) mot clé est facultatif dans la requête de hello, car les requêtes de base de données Azure Cosmos sont déjà incluses dans l’étendue tooa unique collection. Par conséquent, « FROM Families f » peut être remplacé par «FROM root r » ou par tout autre nom de variable que vous choisissez. Base de données Azure Cosmos déduira familles, racine ou le nom de la variable hello choisie, référence hello de collection actuel par défaut.

## <a id="ReplaceDocument"></a>Étape 8 : remplacer le document JSON
Azure Cosmos DB prend en charge le remplacement des documents JSON.  

Copiez et collez hello **ReplaceFamilyDocument** méthode après votre **ExecuteSimpleQuery** (méthode).

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après l’exécution de requête hello, à fin hello de méthode hello. Après le remplacement de document de hello, hello s’exécute même interroger à nouveau tooview hello modifié document.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Appuyez sur **F5** toorun votre application.

Félicitations ! Vous avez remplacé un document Azure Cosmos DB.

## <a id="DeleteDocument"></a>Étape 9 : supprimer le document JSON
Azure Cosmos DB prend en charge la suppression des documents JSON.  

Copiez et collez hello **DeleteFamilyDocument** méthode après votre **ReplaceFamilyDocument** (méthode).

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après hello deuxième exécution de la requête à fin hello de méthode hello.

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

Appuyez sur **F5** toorun votre application.

Félicitations ! Vous avez supprimé un document Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Étape 10 : Supprimer la base de données hello
Suppression hello créé la base de données supprime de la base de données hello et toutes les ressources enfants (collections, documents, etc.).

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après le document de hello supprimer la base de données entière toodelete hello et toutes les ressources enfants.

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

Appuyez sur **F5** toorun votre application.

Félicitations ! Vous avez supprimé une base de données Azure Cosmos DB.

## <a id="Run"></a>Étape 11 : exécuter votre application de console C#
Dans l’application de hello toobuild Visual Studio en mode débogage, appuyez sur F5.

Vous devez voir la sortie hello de votre application démarrée get dans une fenêtre de console. sortie de Hello affiche les résultats de hello Hello requêtes, nous avons ajouté et doit correspondre au texte d’exemple hello ci-dessous.

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
    Press any key toocontinue ...
    Created Family Andersen.1
    Press any key toocontinue ...
    Created Family Wakefield.7
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key tooexit.

Félicitations ! Vous avez terminé le didacticiel de hello et que vous avez une application de console c# de travail !

## <a id="GetSolution"></a>Obtenir la solution du didacticiel complet hello
Si vous n’avez pas ont toocomplete hello dans ce didacticiel, ou simplement que vous souhaitez toodownload hello exemples de code pour les étapes, vous pouvez l’obtenir à partir de [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). 

solution de GetStarted toobuild hello, vous devrez suivant de hello :

* Un compte Azure actif. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).
* Un [compte Azure Cosmos DB][cosmos-db-create-account].
* Hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution disponible sur GitHub.

toorestore hello références toohello Azure Cosmos DB .NET SDK dans Visual Studio, avec le bouton droit hello **GetStarted** solution dans l’Explorateur de solutions, puis cliquez sur **activer la restauration des packages NuGet**. Ensuite, dans le fichier App.config hello, mettre à jour les valeurs EndpointUrl et AuthorizationKey hello comme décrit dans [connecter compte de base de données Azure Cosmos tooan](#Connect).

Voilà, vous n’avez plus qu’à générer l’élément pour être sur la bonne voie !


## <a name="next-steps"></a>Étapes suivantes
* Vous voulez un didacticiel ASP.NET MVC plus complexe ? Reportez-vous à la page [Didacticiel ASP.NET MVC : développement d’applications web avec Azure Cosmos DB](documentdb-dotnet-application.md).
* Vous souhaitez tooperform mise à l’échelle et des tests de performances avec la base de données Azure Cosmos ? Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md).
* Découvrez comment trop[surveiller les demandes, l’utilisation et le stockage Azure Cosmos DB](monitor-accounts.md).
* Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).
* toolearn savoir plus sur la base de données Azure Cosmos, consultez [Bienvenue tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
