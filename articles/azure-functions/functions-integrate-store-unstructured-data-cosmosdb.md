---
title: "aaaStore des données non structurées à l’aide des fonctions d’Azure et Cosmos DB"
description: "Stocker des données non structurées à l’aide d’Azure Functions et de Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, Cosmos DB, calcul dynamique, architecture sans serveur"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a><span data-ttu-id="a333f-104">Stocker des données non structurées à l’aide d’Azure Functions et de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a333f-104">Store unstructured data using Azure Functions and Cosmos DB</span></span>

<span data-ttu-id="a333f-105">[Base de données Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) est un toostore excellent moyen non structurée et les données JSON.</span><span class="sxs-lookup"><span data-stu-id="a333f-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way toostore unstructured and JSON data.</span></span> <span data-ttu-id="a333f-106">Combiné à Azure Functions, Cosmos DB rend le stockage de données simple et rapide avec beaucoup moins de code que pour stocker des données dans une base de données relationnelle.</span><span class="sxs-lookup"><span data-stu-id="a333f-106">Combined with Azure Functions, Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.</span></span>

<span data-ttu-id="a333f-107">Dans les fonctions d’Azure, les liaisons d’entrée et de sortie fournissent une données de service de façon déclarative tooconnect tooexternal à partir de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="a333f-107">In Azure Functions, input and output bindings provide a declarative way tooconnect tooexternal service data from your function.</span></span> <span data-ttu-id="a333f-108">Dans cette rubrique, découvrez comment tooupdate un existant c# fonction tooadd une liaison de sortie qui stocke des données non structurées dans un document de base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a333f-108">In this topic, learn how tooupdate an existing C# function tooadd an output binding that stores unstructured data in a Cosmos DB document.</span></span> 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a><span data-ttu-id="a333f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a333f-110">Prerequisites</span></span>

<span data-ttu-id="a333f-111">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="a333f-111">toocomplete this tutorial:</span></span>

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a><span data-ttu-id="a333f-112">Ajouter une liaison de sortie</span><span class="sxs-lookup"><span data-stu-id="a333f-112">Add an output binding</span></span>

1. <span data-ttu-id="a333f-113">Développez à la fois votre application de fonction et votre fonction.</span><span class="sxs-lookup"><span data-stu-id="a333f-113">Expand both your function app and your function.</span></span>

1. <span data-ttu-id="a333f-114">Sélectionnez **intégrer** et **+ nouvelle sortie**, qui est à hello haut à droite de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="a333f-114">Select **Integrate** and **+ New Output**, which is at hello top right of hello page.</span></span> <span data-ttu-id="a333f-115">Choisissez **Azure Cosmos DB**, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="a333f-115">Choose **Azure Cosmos DB**, and click **Select**.</span></span>

    ![Ajouter une liaison de sortie Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. <span data-ttu-id="a333f-117">Hello d’utilisation **sortie de la base de données Azure Cosmos** paramètres comme spécifié dans la table de hello :</span><span class="sxs-lookup"><span data-stu-id="a333f-117">Use hello **Azure Cosmos DB output** settings as specified in hello table:</span></span> 

    ![Configurer la liaison de sortie Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | <span data-ttu-id="a333f-119">Paramètre</span><span class="sxs-lookup"><span data-stu-id="a333f-119">Setting</span></span>      | <span data-ttu-id="a333f-120">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="a333f-120">Suggested value</span></span>  | <span data-ttu-id="a333f-121">Description</span><span class="sxs-lookup"><span data-stu-id="a333f-121">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="a333f-122">**Nom du paramètre de document**</span><span class="sxs-lookup"><span data-stu-id="a333f-122">**Document parameter name**</span></span> | <span data-ttu-id="a333f-123">taskDocument</span><span class="sxs-lookup"><span data-stu-id="a333f-123">taskDocument</span></span> | <span data-ttu-id="a333f-124">Nom qui fait référence d’objet de base de données Cosmos toohello dans le code.</span><span class="sxs-lookup"><span data-stu-id="a333f-124">Name that refers toohello Cosmos DB object in code.</span></span> |
    | <span data-ttu-id="a333f-125">**Nom de la base de données**</span><span class="sxs-lookup"><span data-stu-id="a333f-125">**Database name**</span></span> | <span data-ttu-id="a333f-126">taskDatabase</span><span class="sxs-lookup"><span data-stu-id="a333f-126">taskDatabase</span></span> | <span data-ttu-id="a333f-127">Nom de documents toosave de base de données.</span><span class="sxs-lookup"><span data-stu-id="a333f-127">Name of database toosave documents.</span></span> |
    | <span data-ttu-id="a333f-128">**Nom de la collection**</span><span class="sxs-lookup"><span data-stu-id="a333f-128">**Collection name**</span></span> | <span data-ttu-id="a333f-129">TaskCollection</span><span class="sxs-lookup"><span data-stu-id="a333f-129">TaskCollection</span></span> | <span data-ttu-id="a333f-130">Nom de la collection de bases de données Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a333f-130">Name of collection of Cosmos DB databases.</span></span> |
    | <span data-ttu-id="a333f-131">**Si la valeur est true, crée la collection et la base de données de la base de données Cosmos hello**</span><span class="sxs-lookup"><span data-stu-id="a333f-131">**If true, creates hello Cosmos DB database and collection**</span></span> | <span data-ttu-id="a333f-132">Activé</span><span class="sxs-lookup"><span data-stu-id="a333f-132">Checked</span></span> | <span data-ttu-id="a333f-133">collection de Hello n’existe déjà, donc le créer.</span><span class="sxs-lookup"><span data-stu-id="a333f-133">hello collection doesn't already exist, so create it.</span></span> |

4. <span data-ttu-id="a333f-134">Sélectionnez **nouveau** toohello suivant **connexion de document de base de données Cosmos** d’étiquette, puis sélectionnez **+ créer**.</span><span class="sxs-lookup"><span data-stu-id="a333f-134">Select **New** next toohello **Cosmos DB document connection** label, and select **+ Create new**.</span></span> 

5. <span data-ttu-id="a333f-135">Hello d’utilisation **nouveau compte** paramètres comme spécifié dans la table de hello :</span><span class="sxs-lookup"><span data-stu-id="a333f-135">Use hello **New account** settings as specified in hello table:</span></span> 

    ![Configurer la connexion au document Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | <span data-ttu-id="a333f-137">Paramètre</span><span class="sxs-lookup"><span data-stu-id="a333f-137">Setting</span></span>      | <span data-ttu-id="a333f-138">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="a333f-138">Suggested value</span></span>  | <span data-ttu-id="a333f-139">Description</span><span class="sxs-lookup"><span data-stu-id="a333f-139">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="a333f-140">**Identifiant**</span><span class="sxs-lookup"><span data-stu-id="a333f-140">**ID**</span></span> | <span data-ttu-id="a333f-141">Nom de base de données</span><span class="sxs-lookup"><span data-stu-id="a333f-141">Name of database</span></span> | <span data-ttu-id="a333f-142">ID unique de la base de données de la base de données Cosmos hello</span><span class="sxs-lookup"><span data-stu-id="a333f-142">Unique ID for hello Cosmos DB database</span></span>  |
    | <span data-ttu-id="a333f-143">**API**</span><span class="sxs-lookup"><span data-stu-id="a333f-143">**API**</span></span> | <span data-ttu-id="a333f-144">SQL (DocumentDB)</span><span class="sxs-lookup"><span data-stu-id="a333f-144">SQL (DocumentDB)</span></span> | <span data-ttu-id="a333f-145">Sélectionnez les API de base de données de document hello.</span><span class="sxs-lookup"><span data-stu-id="a333f-145">Select hello document database API.</span></span>  |
    | <span data-ttu-id="a333f-146">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="a333f-146">**Subscription**</span></span> | <span data-ttu-id="a333f-147">Abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="a333f-147">Azure Subscription</span></span> | <span data-ttu-id="a333f-148">Abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="a333f-148">Azure Subscription</span></span>  |
    | <span data-ttu-id="a333f-149">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="a333f-149">**Resource Group**</span></span> | <span data-ttu-id="a333f-150">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a333f-150">myResourceGroup</span></span> |  <span data-ttu-id="a333f-151">Utilisez hello groupe de ressources existant qui contient votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="a333f-151">Use hello existing resource group that contains your function app.</span></span> |
    | <span data-ttu-id="a333f-152">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="a333f-152">**Location**</span></span>  | <span data-ttu-id="a333f-153">WestEurope</span><span class="sxs-lookup"><span data-stu-id="a333f-153">WestEurope</span></span> | <span data-ttu-id="a333f-154">Sélectionner un emplacement près de tooeither votre application de la fonction ou tooother les applications qui utilisent hello documents stockés.</span><span class="sxs-lookup"><span data-stu-id="a333f-154">Select a location near tooeither your function app or tooother apps that use hello stored documents.</span></span>  |

6. <span data-ttu-id="a333f-155">Cliquez sur **OK** base de données toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="a333f-155">Click **OK** toocreate hello database.</span></span> <span data-ttu-id="a333f-156">Il peut prendre la base de données de quelques minutes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="a333f-156">It may take a few minutes toocreate hello database.</span></span> <span data-ttu-id="a333f-157">Après la création de la base de données hello, chaîne de connexion de base de données hello est stockée comme paramètre d’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="a333f-157">After hello database is created, hello database connection string is stored as a function app setting.</span></span> <span data-ttu-id="a333f-158">nom Hello de ce paramètre d’application est inséré dans **connexion au compte de base de données Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="a333f-158">hello name of this app setting is inserted in **Cosmos DB account connection**.</span></span> 
 
8. <span data-ttu-id="a333f-159">Une fois que la chaîne de connexion hello est définie, sélectionnez **enregistrer** liaison de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a333f-159">After hello connection string is set, select **Save** toocreate hello binding.</span></span>

## <a name="update-hello-function-code"></a><span data-ttu-id="a333f-160">Mettre à jour le code de la fonction hello</span><span class="sxs-lookup"><span data-stu-id="a333f-160">Update hello function code</span></span>

<span data-ttu-id="a333f-161">Remplacez hello existant c# code de fonction hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="a333f-161">Replace hello existing C# function code with hello following code:</span></span>

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
<span data-ttu-id="a333f-162">Cet exemple de code lit les chaînes de requête hello requête HTTP et les affecte toofields Bonjour `taskDocument` objet.</span><span class="sxs-lookup"><span data-stu-id="a333f-162">This code sample reads hello HTTP Request query strings and assigns them toofields in hello `taskDocument` object.</span></span> <span data-ttu-id="a333f-163">Hello `taskDocument` liaison envoie les données d’objet hello à partir de cette toobe de paramètre de liaison stocké dans la base de données du document lié hello.</span><span class="sxs-lookup"><span data-stu-id="a333f-163">hello `taskDocument` binding sends hello object data from this binding parameter toobe stored in hello bound document database.</span></span> <span data-ttu-id="a333f-164">base de données Hello créée hello première fonction hello s’exécute.</span><span class="sxs-lookup"><span data-stu-id="a333f-164">hello database is created hello first time hello function runs.</span></span>

## <a name="test-hello-function-and-database"></a><span data-ttu-id="a333f-165">Fonction hello de test et de la base de données</span><span class="sxs-lookup"><span data-stu-id="a333f-165">Test hello function and database</span></span>

1. <span data-ttu-id="a333f-166">Développez la fenêtre de droite hello et sélectionnez **Test**.</span><span class="sxs-lookup"><span data-stu-id="a333f-166">Expand hello right window and select **Test**.</span></span> <span data-ttu-id="a333f-167">Sous **requête**, cliquez sur **+ ajouter un paramètre** et ajoutez hello suivant de chaîne de requête toohello paramètres :</span><span class="sxs-lookup"><span data-stu-id="a333f-167">Under **Query**, click **+ Add parameter** and add hello following parameters toohello query string:</span></span>

    + `name`
    + `task`
    + `duedate`

2. <span data-ttu-id="a333f-168">Cliquez sur **Exécuter** et vérifiez que l’état 200 est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="a333f-168">Click **Run** and verify that a 200 status is returned.</span></span>

    ![Configurer la liaison de sortie Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. <span data-ttu-id="a333f-170">Sur hello à gauche de hello portail Azure, développez la barre d’icônes hello, type `cosmos` Bonjour rechercher le champ, puis sélectionnez **base de données Azure Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="a333f-170">On hello left side of hello Azure portal, expand hello icon bar, type `cosmos` in hello search field, and select **Azure Cosmos DB**.</span></span>

    ![Rechercher le service de base de données Cosmos](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. <span data-ttu-id="a333f-172">Base de données Sélectionnez hello vous avez créé, puis sélectionnez **Explorateur de données**.</span><span class="sxs-lookup"><span data-stu-id="a333f-172">Select hello database you created, then select **Data Explorer**.</span></span> <span data-ttu-id="a333f-173">Développez hello **Collections** nœuds, sélectionnez hello nouveau document et vérifiez qu’un document hello contient vos valeurs de chaîne de requête, ainsi que des métadonnées supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a333f-173">Expand hello **Collections** nodes, select hello new document, and confirm that hello document contains your query string values, along with some additional metadata.</span></span> 

    ![Vérifiez l’entrée Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

<span data-ttu-id="a333f-175">Vous avez ajouté un déclencheur HTTP tooyour liaison qui stockent les données non structurées dans une base de données de la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a333f-175">You have successfully added a binding tooyour HTTP trigger that stores unstructured data in a Cosmos DB database.</span></span>

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="a333f-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a333f-176">Next steps</span></span>

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="a333f-177">Pour plus d’informations sur la base de données de liaison tooa Cosmos DB, consultez [les liaisons de base de données Azure fonctions Cosmos](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="a333f-177">For more information about binding tooa Cosmos DB database, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>
