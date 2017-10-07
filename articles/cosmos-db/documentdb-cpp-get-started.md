---
title: "aaaC ++ didacticiel de base de données Azure Cosmos | Documents Microsoft"
description: "Un didacticiel C++ qui crée une application de console et de base de données C++ à l’aide d’un kit de développement logiciel (SDK) approuvé par Azure Cosmos DB pour C++. Azure Cosmos DB est un service de base de données à l’échelle de la planète."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a>Cosmos Azure DB : Didacticiel d’application console C++ pour hello API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js pour MongoDB](mongodb-samples.md)
> * [Node.JS](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

Didacticiel de C++ toohello Bienvenue pour hello Azure Cosmos DB DocumentDB API visé SDK pour C++ ! À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB, y compris une base de données C++.

Nous allons aborder les points suivants :

* Création et connexion de compte de base de données Azure Cosmos tooan
* Configuration de votre application
* Création d’une base de données Azure Cosmos DB C++
* Création d’une collection
* Création de documents JSON
* Interrogation de collection de hello
* Remplacement d'un document
* Suppression d’un document
* Suppression de base de données de la base de données C++ Azure Cosmos hello

Vous n’avez pas le temps ? Ne vous inquiétez pas ! solution complète de Hello est disponible sur [GitHub](https://github.com/stalker314314/DocumentDBCpp). Consultez [obtenir la solution complète de hello](#GetSolution) pour obtenir des instructions rapides.

Une fois que vous avez terminé le didacticiel de C++ hello, veuillez utiliser hello des boutons de vote bas hello toogive de cette page nous vos commentaires. 

Si vous souhaitez que nous toocontact vous directement, vous pouvez tooinclude libre votre adresse de messagerie dans vos commentaires ou [atteindre ici toous](https://www.research.net/r/8BKRJ3Z). 

Commençons dès maintenant !

## <a name="prerequisites-for-hello-c-tutorial"></a>Configuration requise pour le didacticiel de hello C++
Vérifiez que vous avez hello suivantes :

* Un compte Azure actif. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit des services Azure](https://azure.microsoft.com/pricing/free-trial/)dès aujourd’hui.
* [Visual Studio](https://www.visualstudio.com/downloads/), avec les composants de langage hello C++ installés.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Étape 1 : créer un compte Azure Cosmos DB
Commençons par créer un compte Azure Cosmos DB. Si vous avez déjà un compte que vous souhaitez toouse, vous pouvez passer trop[le programme d’installation de votre application C++](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupC++"></a>Étape 2 : configurer votre application C++
1. Ouvrez Visual Studio, puis sous hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**. 
2. Bonjour **nouveau projet** fenêtre hello **installé** volet, développez **Visual C++**, cliquez sur **Win32**, puis cliquez sur  **Application Console Win32**. Nom hello projet hellodocumentdb, puis **OK**. 
   
    ![Capture d’écran de l’Assistant Nouveau projet d’hello](media/documentdb-cpp-get-started/hello.png)
3. Démarrage de l’Assistant Application Win32 de hello, cliquez sur **Terminer**.
4. Une fois le projet de hello a été créé, ouvrez le Gestionnaire de package NuGet hello en double-cliquant sur hello **hellodocumentdb** projet **l’Explorateur de solutions** et en cliquant sur **gérer les Packages NuGet**. 
   
    ![Capture d’écran de gérer le NuGet Package dans le menu de projet hello](media/documentdb-cpp-get-started/nuget.png)
5. Bonjour **NuGet : hellodocumentdb** , cliquez sur **Parcourir**, puis recherchez *documentdbcpp*. Dans les résultats de hello, sélectionnez DocumentDbCPP, comme indiqué dans hello suivant capture d’écran. Ce package installe les références tooC ++ reste SDK, qui est une dépendance pour hello DocumentDbCPP.  
   
    ![Package de DocumentDbCpp capture d’écran hello mis en surbrillance](media/documentdb-cpp-get-started/cpp.png)
   
    Après ont ajouté les packages hello tooyour projet, nous sommes tous ensemble toostart écrire du code.   

## <a id="Config"></a>Étape 3 : copier les détails de la connexion à partir du portail Azure pour votre base de données Azure Cosmos DB
Afficher [portail Azure](https://portal.azure.com) et parcourir le compte de base de données de base de données Azure Cosmos toohello vous avez créé. Nous devons hello URI et la clé primaire de hello à partir du portail Azure dans hello prochaine étape tooestablish une connexion à partir de notre extrait de code C++. 

![Azure Cosmos DB URI et les clés dans hello portail Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a>Étape 4 : Connexion de compte de base de données Azure Cosmos tooan
1. Ajouter hello après les en-têtes et les espaces de noms de code source tooyour, après `#include "stdafx.h"`.
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. Ajoutez ensuite hello code suivant tooyour main (fonction) et configuration de compte hello et toomatch de clé primaire vos paramètres de base de données Azure Cosmos à l’étape 3. 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    Maintenant que vous possédez hello code tooinitialize hello documentdb client, examinons une utilisation des ressources de base de données Azure Cosmos.

## <a id="CreateDBColl"></a>Étape 5 : créer une base de données C++ et une collection
Avant cette étape, nous allons interagissent entre une base de données, de collection et de documents pour ceux qui sont nouveaux tooAzure Cosmos DB. Une [base de données](documentdb-resources.md#databases) est un conteneur logique de stockage de documents réparti entre des collections. A [collection](documentdb-resources.md#collections) est un conteneur de documents JSON et hello logique d’application JavaScript. Vous pouvez en savoir plus sur les concepts et le modèle de ressource hiérarchique de base de données Azure Cosmos hello [concepts et modèle de ressource hiérarchiques de base de données Azure Cosmos](documentdb-resources.md).

toocreate une base de données et la collection correspondante ajoutent hello suivant fin toohello de code de votre fonction principale. Cette opération crée une base de données appelé « FamilyRegistry » et une collection appelée « FamilyCollection » à l’aide de la configuration du client hello déclarée à l’étape précédente de hello.

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a>Étape 6 : créer un document
Les [documents](documentdb-resources.md#documents) correspondent à du contenu JSON (arbitraire) défini par l’utilisateur. Vous pouvez maintenant insérer un document dans Azure Cosmos DB. Vous pouvez créer un document en copiant hello après le code en fin de Bonjour de main (fonction) hello. 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

toosummarize, ce code crée une base de données de la base de données Azure Cosmos, la collection et les documents, vous pouvez rechercher dans l’Explorateur de documents dans le portail Azure. 

![Didacticiel C++ - diagramme illustrant la relation hiérarchique de hello entre le compte de hello, la base de données hello, collection de hello et documents de hello](media/documentdb-cpp-get-started/docs.png)

## <a id="QueryDB"></a>Étape 7 : interroger les ressources Azure Cosmos DB
Azure Cosmos DB prend en charge les [requêtes enrichies](documentdb-sql-query.md) sur les documents JSON stockés dans chaque collection. Hello exemple de code suivant montre une requête effectuée à l’aide de la syntaxe SQL que vous pouvez exécuter par rapport aux documents de hello que nous créé à l’étape précédente de hello.

fonction de Hello utilise comme arguments hello identificateur unique ou l’id de ressource pour la base de données hello et collection hello en même temps que le client du document hello. Ajoutez ce code avant la fonction main.

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Replace"></a>Étape 8 : remplacer un document
Azure Cosmos DB prend en charge en remplaçant les documents JSON, comme illustré dans hello suivant de code. Ajoutez ce code après la fonction d’executesimplequery hello.

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <a id="Delete"></a>Étape 9 : supprimer un document
Azure Cosmos DB prend en charge la suppression de documents JSON, vous pouvez le faire par copie et collage de hello après le code après la fonction de replacedocument hello. 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="DeleteDB"></a>Étape 10 : supprimer une base de données
Base de données de suppression hello créé supprime de la base de données hello et toutes les ressources enfants (collections, documents, etc.).

Copiez et collez hello suivant extrait de code (nettoyage de la fonction) après la base de données hello deletedocument fonction tooremove hello et toutes les ressources enfants de hello.

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a>Étape 11 : exécuter l’ensemble votre application C++ !
Nous avez maintenant ajouté le code toocreate, interroger, modifier et supprimer des ressources de base de données Azure Cosmos différents.  Nous maintenant associer ce en ajoutant des appels des fonctions différentes toothese de notre fonction principale dans hellodocumentdb.cpp, ainsi que certains messages de diagnostic.

Vous pouvez le faire en remplaçant hello principale fonction de votre application avec hello suivant de code. Cette écritures hello account_configuration_uri et primary_key que vous avez copié dans le code hello à l’étape 3, par conséquent, réenregistrez qui ligne ou la copie des valeurs hello dans à partir du portail de hello. 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

Vous devez maintenant être en mesure de toobuild et exécuter votre code dans Visual Studio en appuyant sur F5 ou également dans la fenêtre de terminal hello en recherchant des application hello et en cours d’exécution hello exécutable. 

Vous devez voir la sortie hello de votre application démarrée get. sortie de Hello doit correspondre au hello suivant capture d’écran.

![Sortie de l’application Azure Cosmos DB C++](media/documentdb-cpp-get-started/console.png)

Félicitations ! Vous avez terminé hello C++ didacticiel et que vous avez votre première application de console de base de données Azure Cosmos !

## <a id="GetSolution"></a>Obtenir la solution didacticiel hello complète C++
toobuild hello GetStarted solution qui contient tous les exemples hello dans cet article hello éléments suivants sont nécessaires :

* [Un compte Azure Cosmos DB][create-account].
* Hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution disponible sur GitHub.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[surveiller un compte de base de données Azure Cosmos](monitor-accounts.md).
* Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).
* En savoir plus sur le modèle de programmation hello Bonjour section développer Hello [page de documentation de base de données Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account


