---
title: "Utilisation de la bibliothèque cliente gérée App Service Mobile Apps (Windows) | Microsoft Docs"
description: "Apprenez à utiliser un client .NET pour Azure App Service Mobile Apps avec des applications Windows et Xamarin."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: 5f4cc3e97ba7adde2aaac471951a3130d79910f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="29be9-103">Utilisation du client géré pour Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="29be9-103">How to use the managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="29be9-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="29be9-104">Overview</span></span>
<span data-ttu-id="29be9-105">Ce guide vous montre comment mettre en place des scénarios courants à l’aide de la bibliothèque cliente gérée pour Azure App Service Mobile Apps pour les applications Windows et Xamarin.</span><span class="sxs-lookup"><span data-stu-id="29be9-105">This guide shows you how to perform common scenarios using the managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="29be9-106">Si vous débutez avec Mobile Apps, suivez le didacticiel [Démarrage rapide avec Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="29be9-106">If you are new to Mobile Apps, you should consider first completing the [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="29be9-107">Dans ce guide, nous nous concentrons sur le Kit de développement logiciel (SDK) géré côté client.</span><span class="sxs-lookup"><span data-stu-id="29be9-107">In this guide, we focus on the client-side managed SDK.</span></span> <span data-ttu-id="29be9-108">Pour plus d’informations sur les Kits de développement logiciel (SDK) côté serveur pour Mobile Apps, consultez la documentation du [SDK .NET Server][2] ou du [SDK Node.js Server][3].</span><span class="sxs-lookup"><span data-stu-id="29be9-108">To learn more about the server-side SDKs for Mobile Apps, see the documentation for the [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="29be9-109">Documentation de référence</span><span class="sxs-lookup"><span data-stu-id="29be9-109">Reference documentation</span></span>
<span data-ttu-id="29be9-110">La documentation de référence du Kit de développement logiciel (SDK) client se trouve ici : [Référence du client .NET Azure Mobile Apps][4].</span><span class="sxs-lookup"><span data-stu-id="29be9-110">The reference documentation for the client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="29be9-111">Vous trouverez plusieurs exemples de client dans le [référentiel GitHub d’exemples Azure][5].</span><span class="sxs-lookup"><span data-stu-id="29be9-111">You can also find several client samples in the [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="29be9-112">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="29be9-112">Supported Platforms</span></span>
<span data-ttu-id="29be9-113">La plate-forme .NET prend en charge les plates-formes suivantes :</span><span class="sxs-lookup"><span data-stu-id="29be9-113">The .NET Platform supports the following platforms:</span></span>

* <span data-ttu-id="29be9-114">Versions Xamarin Android pour API 19 à 24 (KitKat jusqu’à Nougat)</span><span class="sxs-lookup"><span data-stu-id="29be9-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="29be9-115">Versions Xamarin iOS pour iOS 8.0 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="29be9-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="29be9-116">Plateforme Windows universelle</span><span class="sxs-lookup"><span data-stu-id="29be9-116">Universal Windows Platform</span></span>
* <span data-ttu-id="29be9-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="29be9-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="29be9-118">Windows Phone 8.0, à l’exception des applications Silverlight</span><span class="sxs-lookup"><span data-stu-id="29be9-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="29be9-119">L’authentification « serveur flux » utilise un mode d’affichage WebView pour l’interface utilisateur présentée.</span><span class="sxs-lookup"><span data-stu-id="29be9-119">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="29be9-120">Si l’appareil n’est pas en mesure de présenter une interface utilisateur WebView, d’autres méthodes d’authentification sont alors nécessaires.</span><span class="sxs-lookup"><span data-stu-id="29be9-120">If the device is not able to present a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="29be9-121">Ce SDK ne convient donc pas au type Watch ou d’autres appareils restreints similaires.</span><span class="sxs-lookup"><span data-stu-id="29be9-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="29be9-122"><a name="setup"></a>Configuration et conditions préalables</span><span class="sxs-lookup"><span data-stu-id="29be9-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="29be9-123">Nous supposons que vous avez déjà créé et publié votre projet de backend Mobile Apps et qu'il comprend au moins une table.</span><span class="sxs-lookup"><span data-stu-id="29be9-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="29be9-124">Dans le code utilisé dans cette rubrique, la table s'intitule `TodoItem` et contient les colonnes suivantes : `Id`, `Text` et `Complete`.</span><span class="sxs-lookup"><span data-stu-id="29be9-124">In the code used in this topic, the table is named `TodoItem` and it has the following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="29be9-125">Il s’agit de la table créée lors du démarrage rapide d’[Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="29be9-125">This table is the same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="29be9-126">Le type côté client typé en C# correspondant est la classe suivante :</span><span class="sxs-lookup"><span data-stu-id="29be9-126">The corresponding typed client-side type in C# is the following class:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

<span data-ttu-id="29be9-127">L’attribut [JsonPropertyAttribute][6] est utilisé pour définir le mappage *PropertyName* entre le champ client et le champ de la table.</span><span class="sxs-lookup"><span data-stu-id="29be9-127">The [JsonPropertyAttribute][6] is used to define the *PropertyName* mapping between the client field and the table field.</span></span>

<span data-ttu-id="29be9-128">Pour savoir comment créer des tables dans votre backend Mobile Apps, consultez la rubrique relative au [Kit de développement logiciel (SDK) .NET Server][7] ou au [Kit de développement logiciel (SDK) Node.js Server][8].</span><span class="sxs-lookup"><span data-stu-id="29be9-128">To learn how to create tables in your Mobile Apps backend, see the [.NET Server SDK topic][7] or the [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="29be9-129">Si vous avez créé votre backend Mobile Apps dans le portail Azure avec le démarrage rapide, vous pouvez également utiliser le paramètre **Tables facile** dans le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="29be9-129">If you created your Mobile App backend in the Azure portal using the QuickStart, you can also use the **Easy tables** setting in the [Azure portal].</span></span>

### <a name="how-to-install-the-managed-client-sdk-package"></a><span data-ttu-id="29be9-130">Comment : installer le package du Kit de développement logiciel (SDK) client géré</span><span class="sxs-lookup"><span data-stu-id="29be9-130">How to: Install the managed client SDK package</span></span>
<span data-ttu-id="29be9-131">Utilisez l’une des méthodes suivantes pour installer le package du Kit de développement logiciel (SDK) client géré pour Mobile Apps à partir de [NuGet][9] :</span><span class="sxs-lookup"><span data-stu-id="29be9-131">Use one of the following methods to install the managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="29be9-132">**Visual Studio** Cliquez avec le bouton droit sur votre projet, puis cliquez sur **Gérer les packages NuGet**, recherchez le package `Microsoft.Azure.Mobile.Client` et cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="29be9-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="29be9-133">**Xamarin Studio** Cliquez avec le bouton droit sur votre projet, cliquez sur **Ajouter** > **Ajouter des packages NuGet**, recherchez le package `Microsoft.Azure.Mobile.Client `, puis cliquez sur **Ajouter un package**.</span><span class="sxs-lookup"><span data-stu-id="29be9-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="29be9-134">Dans votre fichier d’activité principal, pensez à ajouter l’instruction **using** suivante :</span><span class="sxs-lookup"><span data-stu-id="29be9-134">In your main activity file, remember to add the following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="29be9-135"><a name="symbolsource"></a>Instructions : Utilisation des symboles de débogage dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29be9-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="29be9-136">Les symboles de l’espace de noms Microsoft.Azure.Mobile sont disponibles sur [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="29be9-136">The symbols for the Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="29be9-137">Consultez les [instructions SymbolSource][11] pour intégrer SymbolSource à Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29be9-137">Refer to the [SymbolSource instructions][11] to integrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="29be9-138"><a name="create-client"></a>Création du client Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="29be9-138"><a name="create-client"></a>Create the Mobile Apps client</span></span>
<span data-ttu-id="29be9-139">Le code suivant permet de créer l’objet [MobileServiceClient][12] utilisé pour accéder à votre backend Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="29be9-139">The following code creates the [MobileServiceClient][12] object that is used to access your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="29be9-140">Dans le code précédent, remplacez `MOBILE_APP_URL` par l’URL du backend Mobile Apps, qui se trouve dans le panneau de votre backend Mobile Apps du [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="29be9-140">In the preceding code, replace `MOBILE_APP_URL` with the URL of the Mobile App backend, which is found in the blade for your Mobile App backend in the [Azure portal].</span></span> <span data-ttu-id="29be9-141">L’objet MobileServiceClient doit être un singleton.</span><span class="sxs-lookup"><span data-stu-id="29be9-141">The MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="29be9-142">Utilisation des tables</span><span class="sxs-lookup"><span data-stu-id="29be9-142">Work with Tables</span></span>
<span data-ttu-id="29be9-143">La section suivante explique comment rechercher et récupérer les enregistrements et modifier les données dans la table.</span><span class="sxs-lookup"><span data-stu-id="29be9-143">The following section details how to search and retrieve records and modify the data within the table.</span></span>  <span data-ttu-id="29be9-144">Cet article contient les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="29be9-144">The following topics are covered:</span></span>

* [<span data-ttu-id="29be9-145">Création d'une référence de table</span><span class="sxs-lookup"><span data-stu-id="29be9-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="29be9-146">Données de requête</span><span class="sxs-lookup"><span data-stu-id="29be9-146">Query data</span></span>](#querying)
* [<span data-ttu-id="29be9-147">Filtrer les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="29be9-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="29be9-148">Trier les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="29be9-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="29be9-149">Renvoyer les données de pages</span><span class="sxs-lookup"><span data-stu-id="29be9-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="29be9-150">Sélectionner des colonnes spécifiques</span><span class="sxs-lookup"><span data-stu-id="29be9-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="29be9-151">Rechercher un enregistrement par ID</span><span class="sxs-lookup"><span data-stu-id="29be9-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="29be9-152">Traitement des requêtes non typées</span><span class="sxs-lookup"><span data-stu-id="29be9-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="29be9-153">Insertion de données</span><span class="sxs-lookup"><span data-stu-id="29be9-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="29be9-154">Mise à jour des données</span><span class="sxs-lookup"><span data-stu-id="29be9-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="29be9-155">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="29be9-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="29be9-156">Résolution des conflits et accès concurrentiel optimiste</span><span class="sxs-lookup"><span data-stu-id="29be9-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="29be9-157">Liaison à une Interface utilisateur Windows</span><span class="sxs-lookup"><span data-stu-id="29be9-157">Binding to a Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="29be9-158">Modification de la taille de page</span><span class="sxs-lookup"><span data-stu-id="29be9-158">Changing the Page Size</span></span>](#pagesize)

### <span data-ttu-id="29be9-159"><a name="instantiating"></a>Procédure : création d'une référence de table</span><span class="sxs-lookup"><span data-stu-id="29be9-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="29be9-160">L’ensemble du code permettant d’accéder aux données d’une table du backend ou de les modifier appelle des fonctions sur l’objet `MobileServiceTable` .</span><span class="sxs-lookup"><span data-stu-id="29be9-160">All the code that accesses or modifies data in a backend table calls functions on the `MobileServiceTable` object.</span></span> <span data-ttu-id="29be9-161">Obtenez une référence à la table en appelant la méthode [GetTable] , comme suit :</span><span class="sxs-lookup"><span data-stu-id="29be9-161">Obtain a reference to the table by calling the [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="29be9-162">L’objet renvoyé utilise le modèle de sérialisation typé.</span><span class="sxs-lookup"><span data-stu-id="29be9-162">The returned object uses the typed serialization model.</span></span> <span data-ttu-id="29be9-163">Les modèles de sérialisation non typés sont également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="29be9-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="29be9-164">L’exemple de code suivant [crée une référence à une table non typée] :</span><span class="sxs-lookup"><span data-stu-id="29be9-164">The following example [creates a reference to an untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="29be9-165">Dans les requêtes non typées, vous devez spécifier la chaîne de requête OData sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="29be9-165">In untyped queries, you must specify the underlying OData query string.</span></span>

### <span data-ttu-id="29be9-166"><a name="querying"></a>Interrogation des données à partir de votre application mobile</span><span class="sxs-lookup"><span data-stu-id="29be9-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="29be9-167">Cette section explique comment émettre des requêtes à destination du backend Mobile Apps, qui inclut les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="29be9-167">This section describes how to issue queries to the Mobile App backend, which includes the following functionality:</span></span>

* [<span data-ttu-id="29be9-168">Filtrer les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="29be9-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="29be9-169">Trier les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="29be9-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="29be9-170">Renvoyer les données de pages</span><span class="sxs-lookup"><span data-stu-id="29be9-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="29be9-171">Sélectionner des colonnes spécifiques</span><span class="sxs-lookup"><span data-stu-id="29be9-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="29be9-172">Rechercher des données par ID</span><span class="sxs-lookup"><span data-stu-id="29be9-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="29be9-173">Une taille de page gérée par le serveur est imposée pour empêcher le renvoi de toutes les lignes.</span><span class="sxs-lookup"><span data-stu-id="29be9-173">A server-driven page size is enforced to prevent all rows from being returned.</span></span>  <span data-ttu-id="29be9-174">La pagination permet d'éviter que les requêtes par défaut associées à des jeux de données volumineux aient un impact négatif sur le service.</span><span class="sxs-lookup"><span data-stu-id="29be9-174">Paging keeps default requests for large data sets from negatively impacting the service.</span></span>  <span data-ttu-id="29be9-175">Pour obtenir le renvoi de plus de 50 lignes, utilisez les méthodes `Skip` et `Take`, comme décrit dans la section [Renvoyer les données dans les pages](#paging).</span><span class="sxs-lookup"><span data-stu-id="29be9-175">To return more than 50 rows, use the `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="29be9-176"><a name="filtering"></a>Procédure : filtrage des données renvoyées</span><span class="sxs-lookup"><span data-stu-id="29be9-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="29be9-177">Le code suivant montre comment filtrer des données en incluant une clause `Where` dans une requête.</span><span class="sxs-lookup"><span data-stu-id="29be9-177">The following code illustrates how to filter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="29be9-178">Il renvoie tous les éléments de `todoTable` dont la propriété `Complete` est égale à `false`.</span><span class="sxs-lookup"><span data-stu-id="29be9-178">It returns all items from `todoTable` whose `Complete` property is equal to `false`.</span></span> <span data-ttu-id="29be9-179">La fonction [Where] applique un prédicat de filtrage de ligne à la requête au niveau de la table.</span><span class="sxs-lookup"><span data-stu-id="29be9-179">The [Where] function applies a row filtering predicate to the query against the table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="29be9-180">Vous pouvez afficher l’URI de la requête envoyée au backend en utilisant un logiciel d’inspection des messages, par exemple les outils destinés aux développeurs de navigateurs ou [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="29be9-180">You can view the URI of the request sent to the backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="29be9-181">Si vous examinez l’URI de requête, vous remarquerez que la chaîne de requête elle-même est modifiée :</span><span class="sxs-lookup"><span data-stu-id="29be9-181">If you look at the request URI, notice that the query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="29be9-182">Cette requête OData est traduite en requête SQL par le Kit de développement logiciel (SDK) de serveur :</span><span class="sxs-lookup"><span data-stu-id="29be9-182">This OData request is translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="29be9-183">La fonction transmise à la méthode `Where` peut avoir un nombre de conditions arbitraire.</span><span class="sxs-lookup"><span data-stu-id="29be9-183">The function that is passed to the `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="29be9-184">Cet exemple serait traduit en requête SQL par le Kit de développement logiciel (SDK) de serveur :</span><span class="sxs-lookup"><span data-stu-id="29be9-184">This example would be translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="29be9-185">Cette requête peut également être fractionnée en plusieurs clauses :</span><span class="sxs-lookup"><span data-stu-id="29be9-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="29be9-186">Les deux méthodes sont équivalentes et peuvent être utilisées de manière interchangeable.</span><span class="sxs-lookup"><span data-stu-id="29be9-186">The two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="29be9-187">La dernière option&mdash;qui consiste à concaténer plusieurs prédicats dans une même requête&mdash;est plus compacte. C'est celle que nous recommandons.</span><span class="sxs-lookup"><span data-stu-id="29be9-187">The former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="29be9-188">La clause `Where` prend en charge les opérations traduites dans le sous-ensemble OData.</span><span class="sxs-lookup"><span data-stu-id="29be9-188">The `Where` clause supports operations that be translated into the OData subset.</span></span> <span data-ttu-id="29be9-189">Les opérations incluent :</span><span class="sxs-lookup"><span data-stu-id="29be9-189">Operations include:</span></span>

* <span data-ttu-id="29be9-190">les opérateurs relationnels (==, !=, <, <=, >, >=),</span><span class="sxs-lookup"><span data-stu-id="29be9-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="29be9-191">les opérateurs arithmétiques (+, -, /, *, %),</span><span class="sxs-lookup"><span data-stu-id="29be9-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="29be9-192">la précision des nombres (Math.Floor, Math.Ceiling),</span><span class="sxs-lookup"><span data-stu-id="29be9-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="29be9-193">les fonctions de chaîne (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span><span class="sxs-lookup"><span data-stu-id="29be9-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="29be9-194">les propriétés de date (Year, Month, Day, Hour, Minute, Second),</span><span class="sxs-lookup"><span data-stu-id="29be9-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="29be9-195">les propriétés d’accès d’un objet, ainsi que</span><span class="sxs-lookup"><span data-stu-id="29be9-195">Access properties of an object, and</span></span>
* <span data-ttu-id="29be9-196">les expressions qui combinent toutes ces opérations.</span><span class="sxs-lookup"><span data-stu-id="29be9-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="29be9-197">Quand vous envisagez ce que le SDK Serveur prend en charge, vous pouvez consulter la [documentation OData v3].</span><span class="sxs-lookup"><span data-stu-id="29be9-197">When considering what the Server SDK supports, you can consider the [OData v3 Documentation].</span></span>

### <span data-ttu-id="29be9-198"><a name="sorting"></a>Procédure : tri des données renvoyées</span><span class="sxs-lookup"><span data-stu-id="29be9-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="29be9-199">Le code suivant montre comment trier les données en incluant une fonction [OrderBy] ou [OrderByDescending] dans la requête.</span><span class="sxs-lookup"><span data-stu-id="29be9-199">The following code illustrates how to sort data by including an [OrderBy] or [OrderByDescending] function in the query.</span></span> <span data-ttu-id="29be9-200">Il renvoie des éléments de `todoTable`, triés par ordre croissant dans le champ `Text`.</span><span class="sxs-lookup"><span data-stu-id="29be9-200">It returns items from `todoTable` sorted ascending by the `Text` field.</span></span>

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <span data-ttu-id="29be9-201"><a name="paging"></a>Procédure : renvoi de données dans les pages</span><span class="sxs-lookup"><span data-stu-id="29be9-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="29be9-202">Par défaut, le backend renvoie uniquement les 50 premières lignes.</span><span class="sxs-lookup"><span data-stu-id="29be9-202">By default, the backend returns only the first 50 rows.</span></span> <span data-ttu-id="29be9-203">Vous pouvez augmenter le nombre de lignes renvoyées en appelant la méthode [Take] .</span><span class="sxs-lookup"><span data-stu-id="29be9-203">You can increase the number of returned rows by calling the [Take] method.</span></span> <span data-ttu-id="29be9-204">Associez `Take` à la méthode [Skip] pour demander une « page » spécifique du jeu de données total renvoyé par la requête.</span><span class="sxs-lookup"><span data-stu-id="29be9-204">Use `Take` along with the [Skip] method to request a specific "page" of the total dataset returned by the query.</span></span> <span data-ttu-id="29be9-205">Lorsqu'elle est exécutée, la requête suivante renvoie les trois premiers éléments de la table.</span><span class="sxs-lookup"><span data-stu-id="29be9-205">The following query, when executed, returns the top three items in the table.</span></span>

```
// Define a filtered query that returns the top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="29be9-206">La requête révisée ci-dessous ignore les trois premiers résultats et renvoie les trois résultats suivants.</span><span class="sxs-lookup"><span data-stu-id="29be9-206">The following revised query skips the first three results and returns the next three results.</span></span> <span data-ttu-id="29be9-207">Cette requête produit la deuxième « page » de données, dont la taille est de trois éléments.</span><span class="sxs-lookup"><span data-stu-id="29be9-207">This query produces the second "page" of data, where the page size is three items.</span></span>

```
// Define a filtered query that skips the top 3 items and returns the next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="29be9-208">La méthode [IncludeTotalCount] demande le nombre total de *tous* les enregistrements qui auront été renvoyés, en ignorant toute clause de pagination/limite spécifiée :</span><span class="sxs-lookup"><span data-stu-id="29be9-208">The [IncludeTotalCount] method requests the total count for *all* the records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="29be9-209">Dans une application réelle, vous pouvez utiliser des requêtes semblables à celles de l’exemple précédent avec un contrôle pager ou une interface utilisateur comparable pour permettre la navigation entre les pages.</span><span class="sxs-lookup"><span data-stu-id="29be9-209">In a real world app, you can use queries similar to the preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="29be9-210">Pour remplacer la limite de 50 lignes dans un backend Mobile Apps, vous devez également appliquer l’attribut [EnableQueryAttribute] à la méthode GET publique et spécifier le comportement de pagination.</span><span class="sxs-lookup"><span data-stu-id="29be9-210">To override the 50-row limit in a Mobile App backend, you must also apply the [EnableQueryAttribute] to the public GET method and specify the paging behavior.</span></span> <span data-ttu-id="29be9-211">Lorsqu'il est appliqué à la méthode, l'exemple suivant définit le nombre maximal de lignes renvoyées à 1 000 :</span><span class="sxs-lookup"><span data-stu-id="29be9-211">When applied to the method, the following sets the maximum returned rows to 1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="29be9-212"><a name="selecting"></a>Procédure : sélection de colonnes spécifiques</span><span class="sxs-lookup"><span data-stu-id="29be9-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="29be9-213">Vous pouvez indiquer le jeu de propriétés à inclure dans les résultats en ajoutant une clause [Select] à la requête.</span><span class="sxs-lookup"><span data-stu-id="29be9-213">You can specify which set of properties to include in the results by adding a [Select] clause to your query.</span></span> <span data-ttu-id="29be9-214">Par exemple, le code suivant montre comment sélectionner un seul champ et comment sélectionner et mettre en forme plusieurs champs :</span><span class="sxs-lookup"><span data-stu-id="29be9-214">For example, the following code shows how to select just one field and also how to select and format multiple fields:</span></span>

```
// Select one field -- just the Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

<span data-ttu-id="29be9-215">Toutes les fonctions décrites jusqu’ici étant cumulatives, nous pouvons les concaténer.</span><span class="sxs-lookup"><span data-stu-id="29be9-215">All the functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="29be9-216">Chaque appel chaîné aura plus de répercussions sur la requête.</span><span class="sxs-lookup"><span data-stu-id="29be9-216">Each chained call affects more of the query.</span></span> <span data-ttu-id="29be9-217">Un exemple supplémentaire :</span><span class="sxs-lookup"><span data-stu-id="29be9-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="29be9-218"><a name="lookingup"></a>Procédure : recherche de données par ID</span><span class="sxs-lookup"><span data-stu-id="29be9-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="29be9-219">La fonction [LookupAsync] permet de rechercher des objets dans la base de données à partir d'un ID particulier.</span><span class="sxs-lookup"><span data-stu-id="29be9-219">The [LookupAsync] function can be used to look up objects from the database with a particular ID.</span></span>

```
// This query filters out the item with the ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="29be9-220"><a name="untypedqueries"></a>Exécution de requêtes non typées</span><span class="sxs-lookup"><span data-stu-id="29be9-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="29be9-221">Quand vous exécutez une requête avec un objet de table non typé, vous devez spécifier explicitement la chaîne de requête OData en appelant [ReadAsync], comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="29be9-221">When executing a query using an untyped table object, you must explicitly specify the OData query string by calling [ReadAsync], as in the following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="29be9-222">Vous obtenez en retour des valeurs JSON que vous pouvez utiliser comme conteneur de propriétés.</span><span class="sxs-lookup"><span data-stu-id="29be9-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="29be9-223">Pour plus d’informations sur JToken et Newtonsoft Json.NET, consultez le site [Json.NET] .</span><span class="sxs-lookup"><span data-stu-id="29be9-223">For more information on JToken and Newtonsoft Json.NET, see the [Json.NET] site.</span></span>

### <span data-ttu-id="29be9-224"><a name="inserting"></a>Insertion de données dans un backend Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="29be9-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="29be9-225">Tous les types clients doivent contenir un membre nommé **Id**, par défaut une chaîne.</span><span class="sxs-lookup"><span data-stu-id="29be9-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="29be9-226">Cet **Id** est requis pour effectuer des opérations CRUD et de synchronisation hors connexion.</span><span class="sxs-lookup"><span data-stu-id="29be9-226">This **Id** is required to perform CRUD operations and for offline sync.</span></span> <span data-ttu-id="29be9-227">Le code suivant montre comment utiliser la méthode [InsertAsync] pour insérer de nouvelles lignes dans une table.</span><span class="sxs-lookup"><span data-stu-id="29be9-227">The following code illustrates how to use the [InsertAsync] method to insert new rows into a table.</span></span> <span data-ttu-id="29be9-228">Le paramètre contient les données à insérer sous forme d'objet .NET.</span><span class="sxs-lookup"><span data-stu-id="29be9-228">The parameter contains the data to be inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="29be9-229">Si aucune valeur ID personnalisée unique n’est incluse dans `todoItem` lors d’une insertion, le serveur génère un GUID.</span><span class="sxs-lookup"><span data-stu-id="29be9-229">If a unique custom ID value is not included in the `todoItem` during an insert, a GUID is generated by the server.</span></span>
<span data-ttu-id="29be9-230">Vous pouvez récupérer l’Id généré en examinant l’objet après le retour de l’appel.</span><span class="sxs-lookup"><span data-stu-id="29be9-230">You can retrieve the generated Id by inspecting the object after the call returns.</span></span>

<span data-ttu-id="29be9-231">Pour insérer des données non typées, vous pouvez tirer parti de Json.NET :</span><span class="sxs-lookup"><span data-stu-id="29be9-231">To insert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="29be9-232">Voici un exemple utilisant une adresse de messagerie comme ID de chaîne unique :</span><span class="sxs-lookup"><span data-stu-id="29be9-232">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="29be9-233">Utilisation de valeurs d'ID</span><span class="sxs-lookup"><span data-stu-id="29be9-233">Working with ID values</span></span>
<span data-ttu-id="29be9-234">Mobile Apps prend en charge des valeurs de chaîne personnalisées uniques pour la colonne **id** de la table.</span><span class="sxs-lookup"><span data-stu-id="29be9-234">Mobile Apps supports unique custom string values for the table's **id** column.</span></span> <span data-ttu-id="29be9-235">Une valeur de chaîne permet aux applications d’utiliser des valeurs personnalisées telles que les adresses de messagerie ou des noms d’utilisateur pour l’ID.</span><span class="sxs-lookup"><span data-stu-id="29be9-235">A string value allows applications to use custom values such as email addresses or user names for the ID.</span></span>  <span data-ttu-id="29be9-236">Les ID de chaîne fournissent les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="29be9-236">String IDs provide you with the following benefits:</span></span>

* <span data-ttu-id="29be9-237">Les ID sont générés sans effectuer d’aller-retour vers la base de données.</span><span class="sxs-lookup"><span data-stu-id="29be9-237">IDs are generated without making a round trip to the database.</span></span>
* <span data-ttu-id="29be9-238">Il est plus facile de fusionner des enregistrements de plusieurs tables ou bases de données.</span><span class="sxs-lookup"><span data-stu-id="29be9-238">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="29be9-239">Les valeurs d’ID peuvent mieux s’intégrer à la logique d’une application.</span><span class="sxs-lookup"><span data-stu-id="29be9-239">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="29be9-240">Lorsque la valeur d’ID d’une chaîne n’est pas définie sur un enregistrement inséré, le backend Mobile Apps génère une valeur unique pour l’ID.</span><span class="sxs-lookup"><span data-stu-id="29be9-240">When a string ID value is not set on an inserted record, the Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="29be9-241">Vous pouvez utiliser la méthode [Guid.NewGuid] pour générer vos propres valeurs d’ID, sur le client ou dans le backend.</span><span class="sxs-lookup"><span data-stu-id="29be9-241">You can use the [Guid.NewGuid] method to generate your own ID values, either on the client or in the backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="29be9-242"><a name="modifying"></a>Modification de données dans un backend Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="29be9-242"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="29be9-243">Le code suivant montre comment utiliser la méthode [UpdateAsync] pour mettre à jour un enregistrement existant avec le même ID avec des informations nouvelles.</span><span class="sxs-lookup"><span data-stu-id="29be9-243">The following code illustrates how to use the [UpdateAsync] method to update an existing record with the same ID with new information.</span></span> <span data-ttu-id="29be9-244">Le paramètre contient les données à mettre à jour sous forme d'objet .NET.</span><span class="sxs-lookup"><span data-stu-id="29be9-244">The parameter contains the data to be updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="29be9-245">Pour mettre à jour des données non typées, vous pouvez utiliser [Json.NET] ainsi :</span><span class="sxs-lookup"><span data-stu-id="29be9-245">To update untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="29be9-246">Vous devez spécifier un champ `id` si vous effectuez une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="29be9-246">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="29be9-247">Le backend utilise le champ `id` pour identifier la ligne à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="29be9-247">The backend uses the `id` field to identify which row to update.</span></span> <span data-ttu-id="29be9-248">Le champ `id` peut être obtenu à partir du résultat de l’appel de `InsertAsync`.</span><span class="sxs-lookup"><span data-stu-id="29be9-248">The `id` field can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="29be9-249">Si vous essayez de mettre à jour un élément sans fournir de valeur `ArgumentException`, une `id` se déclenche.</span><span class="sxs-lookup"><span data-stu-id="29be9-249">An `ArgumentException` is raised if you try to update an item without providing the `id` value.</span></span>

### <span data-ttu-id="29be9-250"><a name="deleting"></a>Suppression de données dans un backend Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="29be9-250"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="29be9-251">Le code suivant montre comment utiliser la méthode [DeleteAsync] pour supprimer une instance existante.</span><span class="sxs-lookup"><span data-stu-id="29be9-251">The following code illustrates how to use the [DeleteAsync] method to delete an existing instance.</span></span> <span data-ttu-id="29be9-252">L’instance est identifiée par le champ `id` défini au niveau de `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="29be9-252">The instance is identified by the `id` field set on the `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="29be9-253">Pour supprimer des données non typées, vous pouvez utiliser Json.NET ainsi :</span><span class="sxs-lookup"><span data-stu-id="29be9-253">To delete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="29be9-254">Vous devez spécifier un ID lorsque vous effectuez une requête de suppression.</span><span class="sxs-lookup"><span data-stu-id="29be9-254">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="29be9-255">Les autres propriétés ne sont pas transmises au service ou sont ignorées au niveau du service.</span><span class="sxs-lookup"><span data-stu-id="29be9-255">Other properties are not passed to the service or are ignored at the service.</span></span> <span data-ttu-id="29be9-256">Le résultat d’un appel `DeleteAsync` a généralement la valeur `null`.</span><span class="sxs-lookup"><span data-stu-id="29be9-256">The result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="29be9-257">L'ID à transmettre peut être obtenu à partir du résultat de l'appel `InsertAsync` .</span><span class="sxs-lookup"><span data-stu-id="29be9-257">The ID to pass in can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="29be9-258">Une `MobileServiceInvalidOperationException` est levée quand vous essayez de supprimer un élément sans spécifier le champ `id`.</span><span class="sxs-lookup"><span data-stu-id="29be9-258">A `MobileServiceInvalidOperationException` is thrown when you try to delete an item without specifying the `id` field.</span></span>

### <span data-ttu-id="29be9-259"><a name="optimisticconcurrency"></a>Procédure : Utilisation de l’accès concurrentiel optimiste pour résoudre les conflits</span><span class="sxs-lookup"><span data-stu-id="29be9-259"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="29be9-260">Plusieurs clients peuvent écrire à un même moment des modifications dans un même élément.</span><span class="sxs-lookup"><span data-stu-id="29be9-260">Two or more clients may write changes to the same item at the same time.</span></span> <span data-ttu-id="29be9-261">En l'absence de détection de conflits, la dernière écriture remplace les mises à jour précédentes.</span><span class="sxs-lookup"><span data-stu-id="29be9-261">Without conflict detection, the last write would overwrite any previous updates.</span></span> <span data-ttu-id="29be9-262">**contrôle d'accès concurrentiel optimiste** considère que chaque transaction peut être validée et, qu’à ce titre, elle ne fait appel à aucun verrouillage de ressources.</span><span class="sxs-lookup"><span data-stu-id="29be9-262">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="29be9-263">Avant de valider une transaction, le contrôle d'accès concurrentiel optimiste vérifie qu'aucune autre transaction n'a modifié les données.</span><span class="sxs-lookup"><span data-stu-id="29be9-263">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified the data.</span></span> <span data-ttu-id="29be9-264">Si les données ont été modifiées, la transaction de validation est annulée.</span><span class="sxs-lookup"><span data-stu-id="29be9-264">If the data has been modified, the committing transaction is rolled back.</span></span>

<span data-ttu-id="29be9-265">Mobile Apps prend en charge le contrôle d'accès concurrentiel optimiste en suivant les modifications apportées à chaque élément à l'aide de la colonne de la propriété système `version` définie pour chaque table de votre serveur principal Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="29be9-265">Mobile Apps supports optimistic concurrency control by tracking changes to each item using the `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="29be9-266">Chaque fois qu’un enregistrement est mis à jour, Mobile Apps attribue une nouvelle valeur à la propriété `version` de cet enregistrement.</span><span class="sxs-lookup"><span data-stu-id="29be9-266">Each time a record is updated, Mobile Apps sets the `version` property for that record to a new value.</span></span> <span data-ttu-id="29be9-267">À chaque demande de mise à jour, la propriété `version` de l'enregistrement inclus dans la demande est comparée à celle de l'enregistrement basé sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="29be9-267">During each update request, the `version` property of the record included with the request is compared to the same property for the record on the server.</span></span> <span data-ttu-id="29be9-268">Si la version transmise avec la demande ne correspond pas à celle du serveur principal, la bibliothèque cliente déclenche une exception `MobileServicePreconditionFailedException<T>` .</span><span class="sxs-lookup"><span data-stu-id="29be9-268">If the version passed with the request does not match the backend, then the client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="29be9-269">Le type inclus avec l’exception est l’enregistrement du backend contenant la version serveur de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="29be9-269">The type included with the exception is the record from the backend containing the servers version of the record.</span></span> <span data-ttu-id="29be9-270">À partir de cette information, l’application peut décider ou non d’exécuter à nouveau la requête de mise à jour avec la valeur `version` correcte du serveur principal pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="29be9-270">The application can then use this information to decide whether to execute the update request again with the correct `version` value from the backend to commit changes.</span></span>

<span data-ttu-id="29be9-271">Pour activer l’accès concurrentiel optimiste, l’application définit une colonne sur la classe table de la propriété système `version` .</span><span class="sxs-lookup"><span data-stu-id="29be9-271">Define a column on the table class for the `version` system property to enable optimistic concurrency.</span></span> <span data-ttu-id="29be9-272">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="29be9-272">For example:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

<span data-ttu-id="29be9-273">Dans le cas des applications utilisant des tables non typées, l'accès concurrentiel optimiste est activé en définissant l'indicateur `Version` au niveau de la propriété `SystemProperties` de la table, comme suit.</span><span class="sxs-lookup"><span data-stu-id="29be9-273">Applications using untyped tables enable optimistic concurrency by setting the `Version` flag on the `SystemProperties` of the table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="29be9-274">Outre l’activation de l’accès concurrentiel optimiste, vous devez également intercepter l’exception `MobileServicePreconditionFailedException<T>` dans votre code au moment de l’appel [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="29be9-274">In addition to enabling optimistic concurrency, you must also catch the `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="29be9-275">Résolvez le conflit en appliquant la `version` correcte pour l’enregistrement mis à jour et appelez [UpdateAsync] avec l’enregistrement résolu.</span><span class="sxs-lookup"><span data-stu-id="29be9-275">Resolve the conflict by applying the correct `version` to the updated record and call [UpdateAsync] with the resolved record.</span></span> <span data-ttu-id="29be9-276">Le code suivant montre comment résoudre un conflit d’écriture une fois qu’il est détecté :</span><span class="sxs-lookup"><span data-stu-id="29be9-276">The following code shows how to resolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at the remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, the item has changed since the last query
        // Resolve the conflict between the local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user to choose the resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // To resolve the conflict, update the version of the item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while the user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="29be9-277">Pour en savoir plus, consultez la rubrique [Synchronisation des données hors connexion dans Azure Mobile Apps] .</span><span class="sxs-lookup"><span data-stu-id="29be9-277">For more information, see the [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="29be9-278"><a name="binding"></a>Procédure : liaison de données Mobile Apps à une interface utilisateur Windows</span><span class="sxs-lookup"><span data-stu-id="29be9-278"><a name="binding"></a>How to: Bind Mobile Apps data to a Windows user interface</span></span>
<span data-ttu-id="29be9-279">Cette section montre comment afficher des objets de données renvoyés à l'aide d'éléments d'interface utilisateur dans une application Windows.</span><span class="sxs-lookup"><span data-stu-id="29be9-279">This section shows how to display returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="29be9-280">L’exemple de code suivant est lié à la source de la liste avec une requête pour les éléments incomplets.</span><span class="sxs-lookup"><span data-stu-id="29be9-280">The following example code binds to the source of the list with a query for incomplete items.</span></span> <span data-ttu-id="29be9-281">[MobileServiceCollection] permet de créer une collection de liaisons prenant en charge Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="29be9-281">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound to a UI list control
IEnumerable itemsControl  = items;

// Bind this to a ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="29be9-282">Certains contrôles dans l’exécution gérée prennent en charge une interface appelée [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="29be9-282">Some controls in the managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="29be9-283">Cette interface permet aux contrôles de demander des données supplémentaires lorsque l'utilisateur fait défiler l'écran.</span><span class="sxs-lookup"><span data-stu-id="29be9-283">This interface allows controls to request extra data when the user scrolls.</span></span> <span data-ttu-id="29be9-284">Une prise en charge de cette interface peut être intégrée aux applications Windows universelles par le biais de [MobileServiceIncrementalLoadingCollection], qui traite automatiquement les appels en provenance des contrôles.</span><span class="sxs-lookup"><span data-stu-id="29be9-284">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from the controls.</span></span> <span data-ttu-id="29be9-285">Utilisez `MobileServiceIncrementalLoadingCollection` dans les applications Windows, comme suit :</span><span class="sxs-lookup"><span data-stu-id="29be9-285">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="29be9-286">Pour utiliser la nouvelle collection sur les applications Windows Phone 8 et « Silverlight », utilisez les méthodes d’extension `ToCollection` au niveau de `IMobileServiceTableQuery<T>` et `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="29be9-286">To use the new collection on Windows Phone 8 and "Silverlight" apps, use the `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="29be9-287">Pour charger les données, appelez `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="29be9-287">To load data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="29be9-288">Lorsque vous utilisez la collection créée par l'appel de `ToCollectionAsync` ou `ToCollection`, vous obtenez une collection qui peut être liée aux contrôles d'interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="29be9-288">When you use the collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound to UI controls.</span></span>  <span data-ttu-id="29be9-289">Cette collection prend en charge la pagination.</span><span class="sxs-lookup"><span data-stu-id="29be9-289">This collection is paging-aware.</span></span>  <span data-ttu-id="29be9-290">Comme la collection charge les données à partir du réseau, le chargement peut échouer.</span><span class="sxs-lookup"><span data-stu-id="29be9-290">Since the collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="29be9-291">Pour gérer ces échecs, ignorez la méthode `OnException` au niveau de `MobileServiceIncrementalLoadingCollection` pour traiter les exceptions résultant des appels vers `LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="29be9-291">To handle such failures, override the `OnException` method on `MobileServiceIncrementalLoadingCollection` to handle exceptions resulting from calls to `LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="29be9-292">Imaginez que votre table contient de nombreux champs, mais que vous ne souhaitez en afficher qu'une partie dans votre contrôle.</span><span class="sxs-lookup"><span data-stu-id="29be9-292">Consider if your table has many fields but you only want to display some of them in your control.</span></span> <span data-ttu-id="29be9-293">Vous pouvez suivre les instructions fournies dans la section précédente «[Sélectionner des colonnes spécifiques](#selecting)» pour sélectionner les colonnes à afficher dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="29be9-293">You may use the guidance in the preceding section "[Select specific columns](#selecting)" to select specific columns to display in the UI.</span></span>

### <span data-ttu-id="29be9-294"><a name="pagesize"></a>Modifier la taille de page</span><span class="sxs-lookup"><span data-stu-id="29be9-294"><a name="pagesize"></a>Change the Page size</span></span>
<span data-ttu-id="29be9-295">Par défaut, Azure Mobile Apps retourne au maximum 50 éléments par demande.</span><span class="sxs-lookup"><span data-stu-id="29be9-295">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="29be9-296">Vous pouvez modifier la taille de pagination en augmentant la taille de page maximale à la fois sur le client et sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="29be9-296">You can change the paging size by increasing the maximum page size on both the client and server.</span></span>  <span data-ttu-id="29be9-297">Pour augmenter la taille de page demandée, spécifiez `PullOptions` lorsque vous utilisez `PullAsync()` :</span><span class="sxs-lookup"><span data-stu-id="29be9-297">To increase the requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="29be9-298">Si vous définissez sur une valeur `PageSize` égale ou supérieure à 100 sur le serveur, une requête renvoie jusqu’à 100 éléments.</span><span class="sxs-lookup"><span data-stu-id="29be9-298">Assuming you have made the `PageSize` equal to or greater than 100 within the server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="29be9-299"><a name="#offlinesync"></a>Utilisation de tables hors connexion</span><span class="sxs-lookup"><span data-stu-id="29be9-299"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="29be9-300">Les tables hors connexion utilisent une banque de données SQLite locale pour stocker les données pour une utilisation en mode hors connexion.</span><span class="sxs-lookup"><span data-stu-id="29be9-300">Offline tables use a local SQLite store to store data for use when offline.</span></span>  <span data-ttu-id="29be9-301">Toutes les opérations de table sont effectuées sur la banque de données SQLite locale au lieu de la banque de données du serveur distant.</span><span class="sxs-lookup"><span data-stu-id="29be9-301">All table operations are done against the local SQLite store instead of the remote server store.</span></span>  <span data-ttu-id="29be9-302">Pour créer une table hors connexion, préparez tout d’abord votre projet :</span><span class="sxs-lookup"><span data-stu-id="29be9-302">To create an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="29be9-303">Dans Visual Studio, cliquez sur la solution > **Gérer les packages NuGet pour la solution...**, puis recherchez et installez le package NuGet **Microsoft.Azure.Mobile.Client.SQLiteStore** pour tous les projets dans la solution.</span><span class="sxs-lookup"><span data-stu-id="29be9-303">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="29be9-304">(Facultatif) Pour prendre en charge des appareils Windows, installez l’un des packages runtime SQLite suivants :</span><span class="sxs-lookup"><span data-stu-id="29be9-304">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="29be9-305">**Windows 8.1 Runtime :** installez [SQLite pour Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="29be9-305">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="29be9-306">**Windows Phone 8.1 :** installez [SQLite pour Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="29be9-306">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="29be9-307">**Plateforme Windows universelle** : installez [SQLite pour plateforme Windows universelle][5].</span><span class="sxs-lookup"><span data-stu-id="29be9-307">**Universal Windows Platform** Install [SQLite for the Universal Windows][5].</span></span>
3. <span data-ttu-id="29be9-308">(Facultatif).</span><span class="sxs-lookup"><span data-stu-id="29be9-308">(Optional).</span></span> <span data-ttu-id="29be9-309">Pour les appareils Windows, cliquez sur **Références** > **Ajouter une référence**, développez le dossier **Windows** > **Extensions**, puis activez le Kit de développement logiciel (SDK) **SQLite pour Windows** approprié en même temps que le Kit de développement logiciel (SDK) **Runtime Visual C++ 2013 pour Windows**.</span><span class="sxs-lookup"><span data-stu-id="29be9-309">For Windows devices, click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**, then enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="29be9-310">Les noms de SDK SQLite varient légèrement en fonction de la plateforme Windows utilisée.</span><span class="sxs-lookup"><span data-stu-id="29be9-310">The SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="29be9-311">Avant que vous ne puissiez créer une référence de table, la banque de données locale doit être préparée :</span><span class="sxs-lookup"><span data-stu-id="29be9-311">Before a table reference can be created, the local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes the SyncContext using the default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="29be9-312">L’initialisation de la banque de données est normalement effectuée immédiatement après la création du client.</span><span class="sxs-lookup"><span data-stu-id="29be9-312">Store initialization is normally done immediately after the client is created.</span></span>  <span data-ttu-id="29be9-313">**L’OfflineDbPath** doit être un nom de fichier approprié pour une utilisation sur toutes les plates-formes prises en charge.</span><span class="sxs-lookup"><span data-stu-id="29be9-313">The **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="29be9-314">Si le chemin d’accès est un chemin d’accès qualifié complet (autrement dit, s’il commence par une barre oblique), ce chemin d’accès est utilisé.</span><span class="sxs-lookup"><span data-stu-id="29be9-314">If the path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="29be9-315">Si le chemin d’accès n’est pas complet, le fichier est placé dans un emplacement spécifique à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="29be9-315">If the path is not fully qualified, the file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="29be9-316">Pour les appareils iOS et Android, le chemin d’accès par défaut est le dossier des fichiers personnels.</span><span class="sxs-lookup"><span data-stu-id="29be9-316">For iOS and Android devices, the default path is the "Personal Files" folder.</span></span>
* <span data-ttu-id="29be9-317">Pour les appareils Windows, le chemin d’accès par défaut est le dossier « AppData » spécifiques à l’application.</span><span class="sxs-lookup"><span data-stu-id="29be9-317">For Windows devices, the default path is the application-specific "AppData" folder.</span></span>

<span data-ttu-id="29be9-318">Une référence de table peut être obtenue à l’aide de la `GetSyncTable<>` méthode :</span><span class="sxs-lookup"><span data-stu-id="29be9-318">A table reference can be obtained using the `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="29be9-319">Il est inutile de s’authentifier pour utiliser une table hors connexion.</span><span class="sxs-lookup"><span data-stu-id="29be9-319">You do not need to authenticate to use an offline table.</span></span>  <span data-ttu-id="29be9-320">Il vous suffit de vous authentifier lorsque vous communiquez avec le service backend.</span><span class="sxs-lookup"><span data-stu-id="29be9-320">You only need to authenticate when you are communicating with the backend service.</span></span>

### <span data-ttu-id="29be9-321"><a name="syncoffline"></a>Synchronisation d’une table hors connexion</span><span class="sxs-lookup"><span data-stu-id="29be9-321"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="29be9-322">Les tables hors connexion ne sont pas synchronisées avec le backend par défaut.</span><span class="sxs-lookup"><span data-stu-id="29be9-322">Offline tables are not synchronized with the backend by default.</span></span>  <span data-ttu-id="29be9-323">La synchronisation est divisée en deux parties.</span><span class="sxs-lookup"><span data-stu-id="29be9-323">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="29be9-324">Vous pouvez transmettre des modifications en dehors du processus de téléchargement de nouveaux éléments.</span><span class="sxs-lookup"><span data-stu-id="29be9-324">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="29be9-325">Voici une méthode de synchronisation typique :</span><span class="sxs-lookup"><span data-stu-id="29be9-325">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //The first parameter is a query name that is used internally by the client SDK to implement incremental sync.
            //Use a different query name for each unique query in your program
            "allTodoItems",
            this.todoTable.CreateQuery());
    }
    catch (MobileServicePushFailedException exc)
    {
        if (exc.PushResult != null)
        {
            syncErrors = exc.PushResult.Errors;
        }
    }

    // Simple error/conflict handling. A real application would handle the various errors like network conditions,
    // server conflicts and others via the IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting to server's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="29be9-326">Si le premier argument de `PullAsync` est null, la synchronisation incrémentielle n’est pas utilisée.</span><span class="sxs-lookup"><span data-stu-id="29be9-326">If the first argument to `PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="29be9-327">Chaque opération de synchronisation récupère tous les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="29be9-327">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="29be9-328">Le Kit de développement logiciel (SDK) effectue une `PushAsync()` implicite avant l’extraction des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="29be9-328">The SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="29be9-329">La gestion des conflits s’effectue par le biais d’une méthode `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="29be9-329">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="29be9-330">Vous pouvez traiter les conflits de la même manière que les tables en ligne.</span><span class="sxs-lookup"><span data-stu-id="29be9-330">You can deal with conflicts in the same way as online tables.</span></span>  <span data-ttu-id="29be9-331">Le conflit est généré lorsque `PullAsync()` est appelée à la place de ou pendant l’insertion, la mise à jour ou la suppression.</span><span class="sxs-lookup"><span data-stu-id="29be9-331">The conflict is produced when `PullAsync()` is called instead of during the insert, update, or delete.</span></span> <span data-ttu-id="29be9-332">Si plusieurs conflits se produisent, les opérations sont regroupées dans une seule MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="29be9-332">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="29be9-333">Gérez chaque défaillance séparément.</span><span class="sxs-lookup"><span data-stu-id="29be9-333">Handle each failure separately.</span></span>

## <span data-ttu-id="29be9-334"><a name="#customapi"></a>Utilisation d’une API personnalisée</span><span class="sxs-lookup"><span data-stu-id="29be9-334"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="29be9-335">Une API personnalisée vous permet de définir des points de terminaison exposant une fonctionnalité de serveur qui ne mappe pas vers une opération d'insertion, de mise à jour, de suppression ou de lecture.</span><span class="sxs-lookup"><span data-stu-id="29be9-335">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="29be9-336">En utilisant une API personnalisée, vous pouvez exercer davantage de contrôle sur la messagerie, notamment lire et définir des en-têtes de message HTTP et définir un format de corps de message autre que JSON.</span><span class="sxs-lookup"><span data-stu-id="29be9-336">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="29be9-337">Vous appelez une API personnalisée en appelant l'une des méthodes [InvokeApiAsync] sur le client.</span><span class="sxs-lookup"><span data-stu-id="29be9-337">You call a custom API by calling one of the [InvokeApiAsync] methods on the client.</span></span> <span data-ttu-id="29be9-338">Par exemple, la ligne de code suivante envoie une requête POST à l’API **completeAll** sur le backend :</span><span class="sxs-lookup"><span data-stu-id="29be9-338">For example, the following line of code sends a POST request to the **completeAll** API on the backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="29be9-339">Il s’agit d’un appel de méthode typé pour lequel le type de renvoi **MarkAllResult** doit être défini.</span><span class="sxs-lookup"><span data-stu-id="29be9-339">This form is a typed method call and requires that the **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="29be9-340">Les méthodes typées et non typées sont toutes deux prises en charge.</span><span class="sxs-lookup"><span data-stu-id="29be9-340">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="29be9-341">La méthode InvokeApiAsync() ajoute « /api/ » à l’API que vous souhaitez appeler, sauf si l’API commence par « / ».</span><span class="sxs-lookup"><span data-stu-id="29be9-341">The InvokeApiAsync() method prepends '/api/' to the API that you wish to call unless the API starts with a '/'.</span></span>
<span data-ttu-id="29be9-342">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="29be9-342">For example:</span></span>

* <span data-ttu-id="29be9-343">`InvokeApiAsync("completeAll",...)` appelle /api/completeAll sur le serveur principal</span><span class="sxs-lookup"><span data-stu-id="29be9-343">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on the backend</span></span>
* <span data-ttu-id="29be9-344">`InvokeApiAsync("/.auth/me",...)` appelle /.auth/me sur le serveur principal</span><span class="sxs-lookup"><span data-stu-id="29be9-344">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on the backend</span></span>

<span data-ttu-id="29be9-345">Vous pouvez utiliser InvokeApiAsync pour appeler des API web, y compris si celles-ci ne sont pas définies avec Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="29be9-345">You can use InvokeApiAsync to call any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="29be9-346">Lorsque vous utilisez InvokeApiAsync(), les en-têtes appropriés, y compris les en-têtes d’authentification, sont envoyés avec la demande.</span><span class="sxs-lookup"><span data-stu-id="29be9-346">When you use InvokeApiAsync(), the appropriate headers, including authentication headers, are sent with the request.</span></span>

## <span data-ttu-id="29be9-347"><a name="authentication"></a>Authentification des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="29be9-347"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="29be9-348">Mobile Apps prend en charge l’authentification et l’autorisation des utilisateurs d’applications via divers fournisseurs d’identité externes : Facebook, Google, Microsoft Account, Twitter et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29be9-348">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="29be9-349">Vous pouvez définir des autorisations sur les tables pour limiter l'accès à certaines opérations aux seuls utilisateurs authentifiés.</span><span class="sxs-lookup"><span data-stu-id="29be9-349">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="29be9-350">Vous pouvez également utiliser l'identité des utilisateurs authentifiés pour implémenter des règles d'autorisation dans les scripts serveur.</span><span class="sxs-lookup"><span data-stu-id="29be9-350">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="29be9-351">Pour plus d'informations, consultez le didacticiel [Ajout de l'authentification à votre application].</span><span class="sxs-lookup"><span data-stu-id="29be9-351">For more information, see the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="29be9-352">Deux flux d’authentification sont pris en charge : le flux *géré par le client* et le flux *géré par le serveur*.</span><span class="sxs-lookup"><span data-stu-id="29be9-352">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="29be9-353">Le flux géré par le serveur fournit l'authentification la plus simple, car il repose sur l'interface d'authentification Web du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="29be9-353">The server-managed flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="29be9-354">En revanche, le flux géré par le client est celui qui s'intègre le plus profondément aux fonctionnalités propres à l'appareil, car il s'appuie sur les Kits de développement logiciel (SDK) propres au fournisseur et à l'appareil.</span><span class="sxs-lookup"><span data-stu-id="29be9-354">The client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="29be9-355">Nous vous recommandons d’utiliser un flux géré par le client dans vos applications de production.</span><span class="sxs-lookup"><span data-stu-id="29be9-355">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="29be9-356">Pour configurer l’authentification, vous devez inscrire votre application avec un ou plusieurs fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="29be9-356">To set up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="29be9-357">Le fournisseur d’identité génère un ID client et une clé secrète client pour votre application.</span><span class="sxs-lookup"><span data-stu-id="29be9-357">The identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="29be9-358">Ces valeurs sont ensuite définies dans votre backend pour activer l’authentification/autorisation d’Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="29be9-358">These values are then set in your backend to enable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="29be9-359">Pour plus d’informations, suivez les instructions détaillées dans le didacticiel [Ajout de l'authentification à votre application].</span><span class="sxs-lookup"><span data-stu-id="29be9-359">For more information, follow the detailed instructions in the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="29be9-360">Les rubriques traitées dans cette section sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="29be9-360">The following topics are covered in this section:</span></span>

* [<span data-ttu-id="29be9-361">Authentification gérée par le client</span><span class="sxs-lookup"><span data-stu-id="29be9-361">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="29be9-362">Authentification gérée par le serveur</span><span class="sxs-lookup"><span data-stu-id="29be9-362">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="29be9-363">Mise en cache du jeton d’authentification</span><span class="sxs-lookup"><span data-stu-id="29be9-363">Caching the authentication token</span></span>](#caching)

### <span data-ttu-id="29be9-364"><a name="clientflow"></a>Authentification gérée par le client</span><span class="sxs-lookup"><span data-stu-id="29be9-364"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="29be9-365">Votre application peut contacter le fournisseur d’identité de manière indépendante, puis fournir le jeton renvoyé pendant la connexion à votre backend.</span><span class="sxs-lookup"><span data-stu-id="29be9-365">Your app can independently contact the identity provider and then provide the returned token during login with your backend.</span></span> <span data-ttu-id="29be9-366">Le flux client permet de proposer l'authentification unique aux utilisateurs ou de récupérer d'autres données utilisateur auprès du fournisseur d'identité.</span><span class="sxs-lookup"><span data-stu-id="29be9-366">This client flow enables you to provide a single sign-on experience for users or to retrieve additional user data from the identity provider.</span></span> <span data-ttu-id="29be9-367">L’authentification par flux client est préférable à l’utilisation d’un flux géré par le serveur, car le SDK du fournisseur d’identité offre une interface UX native plus simple et permet une personnalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="29be9-367">Client flow authentication is preferred to using a server flow as the identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="29be9-368">Des exemples sont fournis pour les modèles suivants d’authentification gérée par le client :</span><span class="sxs-lookup"><span data-stu-id="29be9-368">Examples are provided for the following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="29be9-369">Bibliothèque d’authentification Active Directory</span><span class="sxs-lookup"><span data-stu-id="29be9-369">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="29be9-370">Facebook ou Google</span><span class="sxs-lookup"><span data-stu-id="29be9-370">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="29be9-371">Kit de développement logiciel (SDK) Live</span><span class="sxs-lookup"><span data-stu-id="29be9-371">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="29be9-372"><a name="adal"></a>Authentification des utilisateurs avec la bibliothèque ADAL (Active Directory Authentication Library)</span><span class="sxs-lookup"><span data-stu-id="29be9-372"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="29be9-373">Vous pouvez utiliser la bibliothèque d’authentification Active Directory (ADAL) pour initier l’authentification des utilisateurs à partir du client via l’authentification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29be9-373">You can use the Active Directory Authentication Library (ADAL) to initiate user authentication from the client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="29be9-374">Si vous souhaitez configurer le backend de votre application mobile pour utiliser la connexion AAD, suivez le didacticiel [Configurer votre application App Service pour utiliser la connexion Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="29be9-374">Configure your mobile app backend for AAD sign-on by following the [How to configure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="29be9-375">Bien que cette étape soit facultative, veillez à inscrire une application cliente native.</span><span class="sxs-lookup"><span data-stu-id="29be9-375">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="29be9-376">Dans Visual Studio ou Xamarin Studio, ouvrez votre projet et ajoutez une référence au package NuGet `Microsoft.IdentityModel.CLients.ActiveDirectory` .</span><span class="sxs-lookup"><span data-stu-id="29be9-376">In Visual Studio or Xamarin Studio, open your project and add a reference to the `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="29be9-377">Au cours de la recherche, incluez les versions préliminaires.</span><span class="sxs-lookup"><span data-stu-id="29be9-377">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="29be9-378">Ajoutez le code suivant à votre application, en fonction de la plateforme utilisée.</span><span class="sxs-lookup"><span data-stu-id="29be9-378">Add the following code to your application, according to the platform you are using.</span></span> <span data-ttu-id="29be9-379">Dans chaque cas, effectuez les remplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="29be9-379">In each, make the following replacements:</span></span>

   * <span data-ttu-id="29be9-380">Remplacez **INSERT-AUTHORITY-HERE** par le nom du client dans lequel vous avez approvisionné votre application.</span><span class="sxs-lookup"><span data-stu-id="29be9-380">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="29be9-381">Le format doit être https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="29be9-381">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="29be9-382">Cette valeur peut être copiée depuis l’onglet Domaine de votre Azure Active Directory dans le [portail Azure Classic].</span><span class="sxs-lookup"><span data-stu-id="29be9-382">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="29be9-383">Remplacez **INSERT-RESOURCE-ID-HERE** par l’ID client du serveur principal de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="29be9-383">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="29be9-384">Vous pouvez obtenir l’ID client sur le portail, sous l’onglet **Avancé** du menu **Paramètres Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29be9-384">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="29be9-385">Remplacez **INSERT-CLIENT-ID-HERE** par l’ID client que vous avez copié depuis l’application cliente native.</span><span class="sxs-lookup"><span data-stu-id="29be9-385">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="29be9-386">Remplacez **INSERT-REDIRECT-URI-HERE** par le point de terminaison */.auth/login/done* de votre site, en utilisant le modèle HTTPS.</span><span class="sxs-lookup"><span data-stu-id="29be9-386">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="29be9-387">Cette valeur doit être semblable à *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="29be9-387">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="29be9-388">Voici le code nécessaire pour chaque plateforme :</span><span class="sxs-lookup"><span data-stu-id="29be9-388">The code needed for each platform follows:</span></span>

     <span data-ttu-id="29be9-389">**Windows :**</span><span class="sxs-lookup"><span data-stu-id="29be9-389">**Windows:**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     <span data-ttu-id="29be9-390">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="29be9-390">**Xamarin.iOS**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     <span data-ttu-id="29be9-391">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="29be9-391">**Xamarin.Android**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <span data-ttu-id="29be9-392"><a name="client-facebook"></a>Authentification unique à l’aide d’un jeton Facebook ou Google</span><span class="sxs-lookup"><span data-stu-id="29be9-392"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="29be9-393">Vous pouvez utiliser le flux client comme indiqué dans cet extrait de code pour Facebook ou Google.</span><span class="sxs-lookup"><span data-stu-id="29be9-393">You can use the client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using the Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // to MobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <span data-ttu-id="29be9-394"><a name="client-livesdk"></a>Authentification unique à l’aide d’un compte Microsoft avec le Kit de développement logiciel (SDK) Live</span><span class="sxs-lookup"><span data-stu-id="29be9-394"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with the Live SDK</span></span>
<span data-ttu-id="29be9-395">Pour authentifier les utilisateurs, vous devez inscrire votre application auprès du Centre des développeurs de compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29be9-395">To authenticate users, you must register your app at the Microsoft account Developer Center.</span></span> <span data-ttu-id="29be9-396">Configurez les détails de l’inscription sur votre backend Mobile App.</span><span class="sxs-lookup"><span data-stu-id="29be9-396">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="29be9-397">Pour créer une inscription de compte Microsoft et la connecter à votre backend Mobile App, effectuez les étapes décrites dans la rubrique [Inscrire votre application pour utiliser un compte Microsoft pour l’authentification].</span><span class="sxs-lookup"><span data-stu-id="29be9-397">To create a Microsoft account registration and connect it to your Mobile App backend, complete the steps in [Register your app to use a Microsoft account login].</span></span> <span data-ttu-id="29be9-398">Si vous disposez des versions Windows Store et Windows Phone 8/Silverlight de votre application, inscrivez d'abord la version Windows Store.</span><span class="sxs-lookup"><span data-stu-id="29be9-398">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register the Windows Store version first.</span></span>

<span data-ttu-id="29be9-399">Le code suivant s’authentifie à l’aide du SDK Live et utilise le jeton retourné pour se connecter à votre backend Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="29be9-399">The following code authenticates using Live SDK and uses the returned token to sign in to your Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get the URL the Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create the authentication client for Windows Store using the service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create the authentication client for Windows Phone using the client ID of the registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request the authentication token from the Live authentication service.
        // The wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about the logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use the Microsoft account auth token to sign in to App Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

<span data-ttu-id="29be9-400">Pour plus d’informations, consultez la documentation du [Kit de développement logiciel (SDK) Windows Live] .</span><span class="sxs-lookup"><span data-stu-id="29be9-400">For more information, see the [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="29be9-401"><a name="serverflow"></a>Authentification gérée par le serveur</span><span class="sxs-lookup"><span data-stu-id="29be9-401"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="29be9-402">Une fois que vous avez inscrit votre fournisseur d’identité, appelez la méthode [méthode LoginAsync] sur le [MobileServiceClient] avec la valeur [MobileServiceAuthenticationProvider] de votre fournisseur.</span><span class="sxs-lookup"><span data-stu-id="29be9-402">Once you have registered your identity provider, call the [LoginAsync] method on the [MobileServiceClient] with the [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="29be9-403">Par exemple, le code suivant initie une connexion de flux serveur via Facebook.</span><span class="sxs-lookup"><span data-stu-id="29be9-403">For example, the following code initiates a server flow sign-in by using Facebook.</span></span>

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

<span data-ttu-id="29be9-404">Si vous utilisez un fournisseur d'identité autre que Facebook, remplacez la valeur de [MobileServiceAuthenticationProvider] par la valeur de votre fournisseur.</span><span class="sxs-lookup"><span data-stu-id="29be9-404">If you are using an identity provider other than Facebook, change the value of [MobileServiceAuthenticationProvider] to the value for your provider.</span></span>

<span data-ttu-id="29be9-405">Dans un flux serveur, Azure App Service gère le flux d’authentification OAuth en affichant la page de connexion du fournisseur sélectionné.</span><span class="sxs-lookup"><span data-stu-id="29be9-405">In a server flow, Azure App Service manages the OAuth authentication flow by displaying the sign-in page of the selected provider.</span></span>  <span data-ttu-id="29be9-406">Après le retour du fournisseur identité, Azure App Service génère un jeton d’authentification App Service.</span><span class="sxs-lookup"><span data-stu-id="29be9-406">Once the identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="29be9-407">La [méthode LoginAsync] renvoie un [MobileServiceUser], qui fournit à la fois [l'UserId] de l'utilisateur authentifié et le [MobileServiceAuthenticationToken], sous la forme d'un jeton Web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="29be9-407">The [LoginAsync] method returns a [MobileServiceUser], which provides both the [UserId] of the authenticated user and the [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="29be9-408">Ce jeton peut être mis en cache et réutilisé jusqu'à ce qu'il arrive à expiration.</span><span class="sxs-lookup"><span data-stu-id="29be9-408">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="29be9-409">Pour plus d'informations, consultez la section [Mise en cache du jeton d'authentification](#caching).</span><span class="sxs-lookup"><span data-stu-id="29be9-409">For more information, see [Caching the authentication token](#caching).</span></span>

### <span data-ttu-id="29be9-410"><a name="caching"></a>Mise en cache du jeton d’authentification</span><span class="sxs-lookup"><span data-stu-id="29be9-410"><a name="caching"></a>Caching the authentication token</span></span>
<span data-ttu-id="29be9-411">Dans certains cas, il est possible d’éviter l’appel à la méthode de connexion après la première authentification réussie en stockant le jeton d’authentification à partir du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="29be9-411">In some cases, the call to the login method can be avoided after the first successful authentication by storing the authentication token from the provider.</span></span>  <span data-ttu-id="29be9-412">Les applications Windows Store et UWP peuvent utiliser [PasswordVault] pour mettre en cache le jeton d’authentification en cours après une connexion réussie, comme suit :</span><span class="sxs-lookup"><span data-stu-id="29be9-412">Windows Store and UWP apps can use [PasswordVault] to cache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="29be9-413">La valeur UserId est stockée en tant que nom d’utilisateur des informations d’identification et le jeton est stocké en tant que mot de passe.</span><span class="sxs-lookup"><span data-stu-id="29be9-413">The UserId value is stored as the UserName of the credential and the token is the stored as the Password.</span></span> <span data-ttu-id="29be9-414">Lors des démarrages suivants, vous pouvez vérifier les informations d’identification mises en cache dans **PasswordVault**.</span><span class="sxs-lookup"><span data-stu-id="29be9-414">On subsequent start-ups, you can check the **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="29be9-415">L’exemple suivant utilise les informations d’identification mises en cache si elles sont trouvées. Sinon, il tente à nouveau l’authentification avec le backend :</span><span class="sxs-lookup"><span data-stu-id="29be9-415">The following example uses cached credentials when they are found, and otherwise attempts to authenticate again with the backend:</span></span>

```
// Try to retrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create the current user from the stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache the token as shown above.
}
```

<span data-ttu-id="29be9-416">Lorsque vous déconnectez un utilisateur, vous devez également supprimer les informations d’identifications stockées, comme suit :</span><span class="sxs-lookup"><span data-stu-id="29be9-416">When you sign out a user, you must also remove the stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="29be9-417">Les applications Xamarin utilisent les API [Xamarin.Auth] pour stocker de manière sécurisée les informations d’identification dans un objet **Account** .</span><span class="sxs-lookup"><span data-stu-id="29be9-417">Xamarin    apps use the [Xamarin.Auth] APIs to securely store credentials in an **Account** object.</span></span> <span data-ttu-id="29be9-418">Pour obtenir un exemple d’utilisation de ces API, consultez le fichier de code [AuthStore.cs] dans [l’exemple de partage de photos ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="29be9-418">For an example of using these APIs, see the [AuthStore.cs] code file in the [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="29be9-419">Lorsque vous utilisez l’authentification gérée par le client, vous pouvez également mettre en cache le jeton d’accès obtenu à partir du fournisseur (par exemple, Facebook ou Twitter).</span><span class="sxs-lookup"><span data-stu-id="29be9-419">When you use client-managed authentication, you can also cache the access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="29be9-420">Ce jeton peut être fourni pour demander un nouveau jeton d’authentification à partir du backend, comme suit :</span><span class="sxs-lookup"><span data-stu-id="29be9-420">This token can be supplied to request a new authentication token from the backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using the access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="29be9-421"><a name="pushnotifications"></a>Notifications Push</span><span class="sxs-lookup"><span data-stu-id="29be9-421"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="29be9-422">Les rubriques suivantes traitent des notifications Push :</span><span class="sxs-lookup"><span data-stu-id="29be9-422">The following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="29be9-423">Inscription aux notifications Push</span><span class="sxs-lookup"><span data-stu-id="29be9-423">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="29be9-424">Obtention d’un SID de package Windows Store</span><span class="sxs-lookup"><span data-stu-id="29be9-424">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="29be9-425">Inscription avec des modèles inter-plateformes</span><span class="sxs-lookup"><span data-stu-id="29be9-425">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="29be9-426"><a name="register-for-push"></a>Procédure : inscription aux notifications Push</span><span class="sxs-lookup"><span data-stu-id="29be9-426"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="29be9-427">Le client Mobile Apps permet de s’inscrire aux notifications Push avec Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="29be9-427">The Mobile Apps client enables you to register for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="29be9-428">Lors de l'inscription, vous obtenez un handle à partir de spécifique à la plate-forme Push Notification Service (PNS).</span><span class="sxs-lookup"><span data-stu-id="29be9-428">When registering, you obtain a handle that you obtain from the platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="29be9-429">Vous fournissez ensuite cette valeur, ainsi que toutes les balises lorsque vous créez l'inscription.</span><span class="sxs-lookup"><span data-stu-id="29be9-429">You then provide this value along with any tags when you create the registration.</span></span> <span data-ttu-id="29be9-430">Le code suivant inscrit votre application Windows aux notifications push avec le service de notification Windows (Windows Notification Service, WNS) :</span><span class="sxs-lookup"><span data-stu-id="29be9-430">The following code registers your Windows app for push notifications with the Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using the new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="29be9-431">Si vous déployez vers WNS, alors vous DEVEZ [obtenir un SID de package Windows Store](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="29be9-431">If you are pushing to WNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="29be9-432">Pour plus d'informations sur les applications Windows, y compris l'enregistrement pour les inscriptions de modèle, consultez la page [Ajout de notifications push à votre application].</span><span class="sxs-lookup"><span data-stu-id="29be9-432">For more information on Windows apps, including how to register for template registrations, see [Add push notifications to your app].</span></span>

<span data-ttu-id="29be9-433">La requête de balises à partir du client n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="29be9-433">Requesting tags from the client is not supported.</span></span>  <span data-ttu-id="29be9-434">Les requêtes de balises sont supprimées de manière silencieuse à partir de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="29be9-434">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="29be9-435">Si vous souhaitez inscrire votre appareil avec des balises, créez une API personnalisée qui utilise l’API Notification Hubs pour effectuer l’inscription de votre part.</span><span class="sxs-lookup"><span data-stu-id="29be9-435">If you wish to register your device with tags, create a Custom API that uses the Notification Hubs API to perform the registration on your behalf.</span></span>  <span data-ttu-id="29be9-436">[Appelez l’API personnalisée](#customapi) au lieu de la méthode `RegisterNativeAsync()`.</span><span class="sxs-lookup"><span data-stu-id="29be9-436">[Call the Custom API](#customapi) instead of the `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="29be9-437"><a name="package-sid"></a>Obtention d'un SID de package Windows Store</span><span class="sxs-lookup"><span data-stu-id="29be9-437"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="29be9-438">Un SID de package est nécessaire pour l’activation des notifications Push dans les applications Windows Store.</span><span class="sxs-lookup"><span data-stu-id="29be9-438">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="29be9-439">Pour recevoir un SID de package, enregistrez votre application auprès du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="29be9-439">To receive a package SID, register your application with the Windows Store.</span></span>

<span data-ttu-id="29be9-440">Pour obtenir cette valeur :</span><span class="sxs-lookup"><span data-stu-id="29be9-440">To obtain this value:</span></span>

1. <span data-ttu-id="29be9-441">Dans l’Explorateur de solutions de Visual Studio, cliquez avec le bouton droit sur le projet d’application Windows Store, puis cliquez sur **Store** > **Associer l’application au Windows Store...**.</span><span class="sxs-lookup"><span data-stu-id="29be9-441">In Visual Studio Solution Explorer, right-click the Windows Store app project, click **Store** > **Associate App with the Store...**.</span></span>
2. <span data-ttu-id="29be9-442">Dans l'Assistant, cliquez sur **Suivant**, connectez-vous à votre compte Microsoft, saisissez un nom pour votre application dans **Réserver un nouveau nom d'application**, puis cliquez sur **Réserver**.</span><span class="sxs-lookup"><span data-stu-id="29be9-442">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="29be9-443">Une fois l’inscription de l’application effectuée, sélectionnez son nom, cliquez sur **Suivant**, puis sur **Associer**.</span><span class="sxs-lookup"><span data-stu-id="29be9-443">After the app registration is successfully created, select the app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="29be9-444">Connectez-vous au [Centre de développement Windows] à l’aide de votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29be9-444">Log in to the [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="29be9-445">Sous **Mes applications**, cliquez sur l’inscription de l’application que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="29be9-445">Under **My apps**, click the app registration you created.</span></span>
5. <span data-ttu-id="29be9-446">Cliquez sur **Gestion des applications** > **Identité de l'application**, puis faites défiler jusqu'à trouver votre **SID de package**.</span><span class="sxs-lookup"><span data-stu-id="29be9-446">Click **App management** > **App identity**, and then scroll down to find your **Package SID**.</span></span>

<span data-ttu-id="29be9-447">De nombreuses utilisations du SID de package traitent ce dernier comme une URI, auquel cas vous devez utiliser *ms-app://* comme schéma.</span><span class="sxs-lookup"><span data-stu-id="29be9-447">Many uses of the package SID treat it as a URI, in which case you need to use *ms-app://* as the scheme.</span></span> <span data-ttu-id="29be9-448">Prenez note de la version de votre package SID formé en concaténant cette valeur comme préfixe.</span><span class="sxs-lookup"><span data-stu-id="29be9-448">Make note of the version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="29be9-449">Les applications Xamarin nécessitent un code supplémentaire pour pouvoir enregistrer une application en cours d’exécution sur les plateformes Android ou iOS.</span><span class="sxs-lookup"><span data-stu-id="29be9-449">Xamarin apps require some additional code to be able to register an app running on the iOS or Android platforms.</span></span> <span data-ttu-id="29be9-450">Pour plus d’informations, consultez la rubrique pour votre plateforme :</span><span class="sxs-lookup"><span data-stu-id="29be9-450">For more information, see the topic for your platform:</span></span>

* [<span data-ttu-id="29be9-451">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="29be9-451">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="29be9-452">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="29be9-452">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="29be9-453"><a name="register-xplat"></a>Inscription de modèles de notifications Push pour envoyer des notifications multiplateforme</span><span class="sxs-lookup"><span data-stu-id="29be9-453"><a name="register-xplat"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="29be9-454">Pour enregistrer les modèles, utilisez la méthode `RegisterAsync()` avec les modèles, comme suit :</span><span class="sxs-lookup"><span data-stu-id="29be9-454">To register templates, use the `RegisterAsync()` method with the templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="29be9-455">Vos modèles doivent être de type `JObject` et peuvent contenir plusieurs modèles au format JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="29be9-455">Your templates should be `JObject` types and can contain multiple templates in the following JSON format:</span></span>

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

<span data-ttu-id="29be9-456">La méthode **RegisterAsync()** accepte également les mosaïques secondaires :</span><span class="sxs-lookup"><span data-stu-id="29be9-456">The method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="29be9-457">Toutes les balises sont supprimées lors de l’inscription pour la sécurité.</span><span class="sxs-lookup"><span data-stu-id="29be9-457">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="29be9-458">Pour ajouter des balises à des installations ou des modèles dans des installations, consultez [Utiliser le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="29be9-458">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="29be9-459">Pour envoyer des notifications à l’aide de ces modèles inscrits, consultez les [API Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="29be9-459">To send notifications utilizing these registered templates, refer to the [Notification Hubs APIs].</span></span>

## <span data-ttu-id="29be9-460"><a name="misc"></a>Rubriques diverses</span><span class="sxs-lookup"><span data-stu-id="29be9-460"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="29be9-461"><a name="errors"></a>Procédure : gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="29be9-461"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="29be9-462">Quand une erreur se produit sur le backend, le Kit de développement logiciel (SDK) client déclenche une `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="29be9-462">When an error occurs in the backend, the client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="29be9-463">L’exemple suivant montre comment gérer une exception renvoyée par le backend :</span><span class="sxs-lookup"><span data-stu-id="29be9-463">The following example shows how to handle an exception that is returned by the backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into the database. When the operation completes
    // and App Service has assigned an Id, the item is added to the CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

<span data-ttu-id="29be9-464">Vous trouverez un autre exemple de traitement des conditions d’erreur dans l’ [exemple de fichiers Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="29be9-464">Another example of dealing with error conditions can be found in the [Mobile Apps Files Sample].</span></span> <span data-ttu-id="29be9-465">L’exemple [LoggingHandler] fournit un gestionnaire de délégué de journalisation pour consigner les requêtes envoyées au backend.</span><span class="sxs-lookup"><span data-stu-id="29be9-465">The [LoggingHandler] example provides a logging delegate handler to log the requests being made to the backend.</span></span>

### <span data-ttu-id="29be9-466"><a name="headers"></a>Procédure de personnalisation des en-têtes de requête</span><span class="sxs-lookup"><span data-stu-id="29be9-466"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="29be9-467">Pour prendre en charge votre scénario d’application en particulier, vous devrez peut-être personnaliser la communication avec le backend Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="29be9-467">To support your specific app scenario, you might need to customize communication with the Mobile App backend.</span></span> <span data-ttu-id="29be9-468">Par exemple, il est possible que vous vouliez ajouter un en-tête personnalisé à chaque demande sortante ou même modifier le code d'état des réponses.</span><span class="sxs-lookup"><span data-stu-id="29be9-468">For example, you may want to add a custom header to every outgoing request or even change responses status codes.</span></span> <span data-ttu-id="29be9-469">Pour cela, utilisez un [DelegatingHandler]personnalisé, comme dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="29be9-469">You can use a custom [DelegatingHandler], as in the following example:</span></span>

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change the request-side here based on the HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do the request
        var response = await base.SendAsync(request, cancellationToken);

        // Change the response-side here based on the HttpResponseMessage

        // Return the modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

<span data-ttu-id="29be9-470">[Ajout de l'authentification à votre application]: app-service-mobile-windows-store-dotnet-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="29be9-470">[Add authentication to your app]: app-service-mobile-windows-store-dotnet-get-started-users.md</span></span>
<span data-ttu-id="29be9-471">[Synchronisation des données hors connexion dans Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="29be9-471">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="29be9-472">[Ajout de notifications push à votre application]: app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="29be9-472">[Add push notifications to your app]: app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="29be9-473">[Inscrire votre application pour utiliser un compte Microsoft pour l’authentification]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="29be9-473">[Register your app to use a Microsoft account login]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="29be9-474">[Configurer votre application App Service pour utiliser la connexion Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="29be9-474">[How to configure App Service for Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>

<!-- Microsoft URLs. -->
<span data-ttu-id="29be9-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-481">[crée une référence à une table non typée]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-481">[creates a reference to an untyped table]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-486">[méthode LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span></span>
<span data-ttu-id="29be9-495">[l'UserId]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span></span>
<span data-ttu-id="29be9-497">[portail Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="29be9-497">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="29be9-498">[portail Azure Classic]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="29be9-498">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="29be9-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span></span>
<span data-ttu-id="29be9-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span></span>
<span data-ttu-id="29be9-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span></span>
<span data-ttu-id="29be9-502">[Centre de développement Windows]: https://dev.windows.com/en-us/overview</span><span class="sxs-lookup"><span data-stu-id="29be9-502">[Windows Dev Center]: https://dev.windows.com/en-us/overview</span></span>
<span data-ttu-id="29be9-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span></span>
<span data-ttu-id="29be9-504">[Kit de développement logiciel (SDK) Windows Live]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span></span>
<span data-ttu-id="29be9-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span></span>
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
<span data-ttu-id="29be9-506">[API Notification Hubs]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span><span class="sxs-lookup"><span data-stu-id="29be9-506">[Notification Hubs APIs]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span></span>
<span data-ttu-id="29be9-507">[exemple de fichiers Mobile Apps]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span><span class="sxs-lookup"><span data-stu-id="29be9-507">[Mobile Apps Files Sample]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span></span>
<span data-ttu-id="29be9-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span><span class="sxs-lookup"><span data-stu-id="29be9-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span></span>

<!-- External URLs -->
<span data-ttu-id="29be9-509">[documentation OData v3]: http://www.odata.org/documentation/odata-version-3-0/</span><span class="sxs-lookup"><span data-stu-id="29be9-509">[OData v3 Documentation]: http://www.odata.org/documentation/odata-version-3-0/</span></span>
<span data-ttu-id="29be9-510">[Fiddler]: http://www.telerik.com/fiddler</span><span class="sxs-lookup"><span data-stu-id="29be9-510">[Fiddler]: http://www.telerik.com/fiddler</span></span>
<span data-ttu-id="29be9-511">[Json.NET]: http://www.newtonsoft.com/json</span><span class="sxs-lookup"><span data-stu-id="29be9-511">[Json.NET]: http://www.newtonsoft.com/json</span></span>
<span data-ttu-id="29be9-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span><span class="sxs-lookup"><span data-stu-id="29be9-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span></span>
<span data-ttu-id="29be9-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span><span class="sxs-lookup"><span data-stu-id="29be9-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span></span>
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
