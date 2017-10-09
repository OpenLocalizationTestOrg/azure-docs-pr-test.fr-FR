---
title: "Azure Cosmos DB : Didacticiel sur la prise en main de l’API DocumentDB avec .NET Core | Microsoft Docs"
description: "Un didacticiel qui crée une base de données en ligne et une application console c# à l’aide de hello Azure Cosmos API DB DocumentDB .NET Core SDK."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a>Azure Cosmos DB : Prise en main de hello API DocumentDB et .NET Core
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js pour MongoDB](mongodb-samples.md)
> * [Node.JS](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bienvenue toohello API DocumentDB de base de données Azure Cosmos mise en route du didacticiel de .NET Core ! À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB.

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

Vous n’avez pas le temps ? Ne vous inquiétez pas ! solution complète de Hello est disponible sur [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started). Raccourcis toohello [obtenir la section de solution complète hello](#GetSolution) pour obtenir des instructions rapides.

Voulez toobuild un Xamarin iOS, Android ou des formulaires à l’aide de l’application hello API DocumentDB et Kit de développement .NET Core ? Consultez la page [Créer des applications mobiles avec Xamarin et Azure Cosmos DB](mobile-apps-with-xamarin.md).

> [!NOTE]
> Bonjour Azure Cosmos DB .NET Core SDK est utilisé dans ce didacticiel n’est pas encore compatible avec les applications de plateforme Windows universelle (UWP). Pour une version préliminaire du Kit de développement .NET Core qui ne prend pas en charge les applications UWP de hello, envoyer un courrier électronique trop[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

Commençons dès maintenant !

## <a name="prerequisites"></a>Composants requis
Vérifiez que vous avez hello suivantes :

* Un compte Azure actif. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/). 
    * Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) pour ce didacticiel.
* [Visual Studio 2017](https://www.visualstudio.com/vs/) 
    * Si vous travaillez sur MacOS ou Linux, vous pouvez développer des applications .NET Core à partir de ligne de commande de hello en installant hello [le Kit de développement .NET Core](https://www.microsoft.com/net/core#macos) pour la plateforme hello de votre choix. 
    * Si vous travaillez sur Windows, vous pouvez développer des applications .NET Core à partir de ligne de commande de hello en installant hello [le Kit de développement .NET Core](https://www.microsoft.com/net/core#windows). 
    * Vous pouvez utiliser votre propre éditeur, ou télécharger [Visual Studio Code](https://code.visualstudio.com/) qui est disponible gratuitement et fonctionne sous Windows, Linux et Mac OS. 

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Étape 1 : créer un compte Azure Cosmos DB
Commençons par créer un compte Azure Cosmos DB. Si vous avez déjà un compte que vous souhaitez toouse, vous pouvez passer trop[le programme d’installation de votre Solution Visual Studio](#SetupVS). Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[le programme d’installation de votre Solution Visual Studio](#SetupVS).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Étape 2 : configurer votre solution Visual Studio
1. Ouvrez **Visual Studio 2017** sur votre ordinateur.
2. Sur hello **fichier** menu, sélectionnez **nouveau**, puis choisissez **projet**.
3. Bonjour **nouveau projet** boîte de dialogue, sélectionnez **modèles** / **Visual C#** / **.NET Core** / **L’Application console (.NET Core)**, nommez votre projet **DocumentDBGettingStarted**, puis cliquez sur **OK**.

   ![Capture d’écran de la fenêtre de nouveau projet hello](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. Bonjour **l’Explorateur de solutions**, cliquez avec le bouton droit sur **DocumentDBGettingStarted**.
5. Sans quitter le menu de hello, cliquez sur **gérer les Packages NuGet...** .

   ![Capture d’écran de hello droite Menu Clicked hello projet](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. Bonjour **NuGet** , cliquez sur **Parcourir** haut hello fenêtre hello et type **azure documentdb** dans la zone de recherche hello.
7. Dans les résultats de hello, recherchez **Microsoft.Azure.DocumentDB.Core** et cliquez sur **installer**.
   ID de package Hello pour hello bibliothèque cliente de DocumentDB pour .NET Core est [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core). Si vous ciblez une version de .NET Framework (net461, par exemple) qui n’est pas prise en charge par ce package NuGet .NET Core, utilisez [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) qui prend en charge toutes les versions de .NET Framework à partir de la version 4.5.
8. Aux invites de hello, acceptez les installations des packages NuGet hello et contrat de licence hello.

Parfait ! Maintenant que nous avons terminé le programme d’installation Bonjour, nous pouvons commencer l’écriture du code. Vous trouverez le projet de code complet de ce didacticiel dans [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).

## <a id="Connect"></a>Étape 3 : Relier le compte de base de données Azure Cosmos tooan
Tout d’abord, ajoutez ces références début toohello de votre application c#, dans le fichier Program.cs de hello :

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> Dans l’ordre toocomplete ce didacticiel, veillez à qu'ajouter des dépendances de hello ci-dessus.

Maintenant, ajoutez ces deux constantes et votre variable *client* dans votre classe publique *Program*.

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

Ensuite, head toohello [Azure Portal](https://portal.azure.com) tooretrieve votre URI et la clé primaire. Hello URI de base de données Azure Cosmos et la clé primaire sont nécessaires pour votre application toounderstand où tooconnect et de base de données Azure Cosmos tootrust connexion de votre application.

Dans hello portail Azure, accédez de compte de base de données Azure Cosmos tooyour, puis cliquez sur **clés**.

Copiez hello URI à partir du portail de hello, puis collez-la dans `<your endpoint URI>` dans le fichier program.cs de hello. Copie hello clé primaire à partir du portail de hello et collez-la dans `<your key>`. Si vous utilisez hello Azure Cosmos DB émulateur, utilisez `https://localhost:8081` en tant que point de terminaison hello et clé d’autorisation bien défini hello [comment l’à l’aide de toodevelop hello Azure Cosmos DB émulateur](local-emulator.md). Assurez-vous que tooremove hello < et >, mais laissez hello des guillemets doubles autour de votre point de terminaison et la clé.

![Capture d’écran de hello portail Azure utilisée par hello toocreate de didacticiel NoSQL une application console c#. Indique une base de données Azure Cosmos compte, avec un concentrateur actif de hello mis en surbrillance, hello bouton les clés de mise en surbrillance dans le panneau de compte de base de données Azure Cosmos hello et valeurs d’URI, clés primaires et secondaires hello mis en surbrillance sur hello Panneau de clés][keys]

Nous allons commencer l’application démarrée lors de l’obtention de hello en créant une nouvelle instance de hello **DocumentClient**.

Ci-dessous hello **principal** méthode, ajoutez cette nouvelle tâche asynchrone appelée **GetStartedDemo**, qui instancie notre nouveau **DocumentClient**.

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

Ajouter le code suivant de hello toorun votre tâche asynchrone à partir de votre **Main** (méthode). Hello **Main** méthode intercepter les exceptions et les écrire toohello console.

```csharp
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
```

Hello de presse **DocumentDBGettingStarted** bouton toobuild et exécuter l’application hello.

Félicitations ! Vous avez correctement connecté le compte de base de données Azure Cosmos tooan, maintenant examinons une utilisation des ressources de base de données Azure Cosmos.  

## <a name="step-4-create-a-database"></a>Étape 4 : créer une base de données
Avant d’ajouter de code hello pour la création d’une base de données, ajoutez une méthode d’assistance pour l’écriture de toohello console.

Copiez et collez hello **WriteToConsoleAndPromptToContinue** méthode sous hello **GetStartedDemo** (méthode).

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

Votre base de données Azure Cosmos [base de données](documentdb-resources.md#databases) peuvent être créés à l’aide de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) méthode Hello **DocumentClient** classe. Une base de données est un conteneur logique de hello JSON de stockage de documents partitionné entre des collections.

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode en dessous de la création du client hello. Ce faisant, vous créez la base de données *FamilyDB*.

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.

Félicitations ! Vous avez créé une base de données Azure Cosmos DB.  

## <a id="CreateColl"></a>Étape 5 : créer une collection
> [!WARNING]
> **CreateDocumentCollectionAsync** crée une collection avec un débit réservé, ce qui a des conséquences sur la tarification. Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).

A [collection](documentdb-resources.md#collections) peuvent être créés à l’aide de hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) méthode Hello **DocumentClient** classe. Une collection est un conteneur de documents JSON. Elle est associée à une logique d'application JavaScript.

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode en dessous de la création de base de données hello. Ce faisant, vous créez la collection de documents *FamilyCollection_oa*.

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.

Félicitations ! Vous avez créé une collection de documents Azure Cosmos DB.  

## <a id="CreateDoc"></a>Étape 6 : Création de documents JSON
A [document](documentdb-resources.md#documents) peuvent être créés à l’aide de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) méthode Hello **DocumentClient** classe. Les documents correspondent à du contenu JSON (arbitraire) défini par l'utilisateur. Nous pouvons maintenant insérer un ou plusieurs documents. Si vous avez déjà des données que vous souhaitez toostore dans votre base de données, vous pouvez utiliser Azure Cosmos DB [l’outil de Migration de données](import-data.md).

Tout d’abord, nous devons toocreate un **famille** classe représentant des objets stockés dans la base de données Azure Cosmos dans cet exemple. Nous allons également créer les sous-classes **Parent**, **Child**, **Pet** et **Address** qui seront utilisées dans **Family**. Notez que les documents doivent avoir une propriété **Id** sérialisée comme **id** dans JSON. Créer ces classes en ajoutant hello suivant sous-classes internes après hello **GetStartedDemo** (méthode).

Copiez et collez hello **famille**, **Parent**, **enfant**, **animal de compagnie**, et **adresse** classes sous Hello **WriteToConsoleAndPromptToContinue** (méthode).

```csharp
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
```

Copiez et collez hello **CreateFamilyDocumentIfNotExists** méthode sous votre **CreateDocumentCollectionIfNotExists** (méthode).

```csharp
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
```

Et insérez les deux documents, un pour chacun des hello Andersen famille et hello Wakefield famille.

Copiez et collez le code hello qui suit `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** méthode en dessous de la création de la collection de document hello.

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.

Félicitations ! Vous avez créé deux documents Azure Cosmos DB.  

![Diagramme illustrant relation hiérarchique hello entre le compte de hello, base de données en ligne hello, la collection de hello et documents hello utilisés par hello toocreate de didacticiel NoSQL une application console c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Étape 7 : interroger les ressources Azure Cosmos DB
Azure Cosmos DB prend en charge les [requêtes](documentdb-sql-query.md) enrichies sur les documents JSON stockés dans chaque collection.  Hello exemple de code suivant montre différentes requêtes - à l’aide de la base de données SQL Azure Cosmos syntaxe ainsi que LINQ - ce que nous pouvons exécuter par rapport aux documents que nous insérés à l’étape précédente de hello hello.

Copiez et collez hello **ExecuteSimpleQuery** méthode sous votre **CreateFamilyDocumentIfNotExists** (méthode).

```csharp
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
```

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode en dessous de la création d’un deuxième document hello.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.

Félicitations ! Vous avez interrogé une collection Azure Cosmos DB.

Hello diagramme suivant illustre la requête SQL de base de données Azure Cosmos de hello syntaxe est appelée sur la collection de hello créée et hello même logique s’applique également les requêtes LINQ toohello.

![Diagramme illustrant la portée de hello et la signification de la requête de hello utilisé par toocreate de didacticiel hello NoSQL, une application console c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

Hello [FROM](documentdb-sql-query.md#FromClause) mot clé est facultatif dans la requête de hello, car les requêtes de base de données Azure Cosmos sont déjà incluses dans l’étendue tooa unique collection. Par conséquent, « FROM Families f » peut être remplacé par «FROM root r » ou par tout autre nom de variable que vous choisissez. DocumentDB déduira familles, racine ou le nom de la variable hello choisie, référence hello de collection actuel par défaut.

## <a id="ReplaceDocument"></a>Étape 8 : remplacer le document JSON
Azure Cosmos DB prend en charge le remplacement des documents JSON.  

Copiez et collez hello **ReplaceFamilyDocument** méthode sous votre **ExecuteSimpleQuery** (méthode).

```csharp
// ADD THIS PART tooYOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode en dessous de l’exécution des requêtes hello. Après le remplacement de document de hello, hello s’exécute même interroger à nouveau tooview hello modifié document.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.

Félicitations ! Vous avez remplacé un document Azure Cosmos DB.

## <a id="DeleteDocument"></a>Étape 9 : supprimer le document JSON
Azure Cosmos DB prend en charge la suppression des documents JSON.  

Copiez et collez hello **DeleteFamilyDocument** méthode sous votre **ReplaceFamilyDocument** (méthode).

```csharp
// ADD THIS PART tooYOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode en dessous de l’exécution de la deuxième requête hello.

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.

Félicitations ! Vous avez supprimé un document Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Étape 10 : Supprimer la base de données hello
Suppression hello créé la base de données supprime de la base de données hello et toutes les ressources enfants (collections, documents, etc.).

Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode sous le document de hello supprimer toute base de données toodelete hello et toutes les ressources enfants.

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.

Félicitations ! Vous avez supprimé une base de données Azure Cosmos DB.

## <a id="Run"></a>Étape 11 : exécuter votre application de console C#
Hello de presse **DocumentDBGettingStarted** bouton dans Visual Studio toobuild hello application en mode débogage.

Vous devez voir la sortie hello de votre application démarrée get dans la fenêtre de console hello. sortie de Hello affiche les résultats de hello Hello requêtes, nous avons ajouté et doit correspondre au texte d’exemple hello ci-dessous.

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
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
```

Félicitations ! Vous avez terminé le didacticiel de hello et que vous avez une application de console c# de travail !

## <a id="GetSolution"></a>Obtenir la solution du didacticiel complet hello
toobuild hello GetStarted solution qui contient tous les exemples hello dans cet article vous serez hello éléments suivants sont nécessaires :

* Un compte Azure actif. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).
* Un [compte Azure Cosmos DB][create-documentdb-dotnet.md#create-account].
* Hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution disponible sur GitHub.

toorestore hello références toohello API DocumentDB Azure Cosmos DB Core du SDK pour .NET dans Visual Studio, avec le bouton droit hello **GetStarted** solution dans l’Explorateur de solutions, puis cliquez sur **activer la restauration des packages NuGet**. Ensuite, dans le fichier Program.cs de hello, mettre à jour les valeurs EndpointUrl et AuthorizationKey hello comme décrit dans [connecter compte de base de données Azure Cosmos tooan](#Connect).

## <a name="next-steps"></a>Étapes suivantes
* Vous voulez un didacticiel ASP.NET MVC plus complexe ? Reportez-vous à la page [Didacticiel ASP.NET MVC : développement d’applications web avec Azure Cosmos DB](documentdb-dotnet-application.md).
* Voulez toodevelop un Xamarin iOS, Android ou des formulaires à l’aide de l’application hello API DocumentDB pour le Kit de développement logiciel Azure Cosmos DB .NET Core ? Consultez la page [Créer des applications mobiles avec Xamarin et Azure Cosmos DB](mobile-apps-with-xamarin.md).
* Vous souhaitez tooperform mise à l’échelle et des tests de performances avec la base de données Azure Cosmos ? Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md).
* Découvrez comment trop[demandes analyse Azure Cosmos DB, l’utilisation et stockage](monitor-accounts.md).
* Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).
* toolearn en savoir plus sur le modèle de programmation hello, consultez [base de données Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
