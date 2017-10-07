---
title: "aaaWorking avec hello App Service Mobile Apps gérés bibliothèque cliente (Windows | Documents Microsoft"
description: "Découvrez comment toouse un client .NET pour Azure App Service Mobile Apps avec les applications Windows et Xamarin."
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
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="0f9da-103">Comment toouse hello gérées client pour les applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="0f9da-103">How toouse hello managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="0f9da-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0f9da-104">Overview</span></span>
<span data-ttu-id="0f9da-105">Ce guide vous explique comment tooperform des scénarios courants utilisant hello gérées bibliothèque cliente pour les applications Azure App Service Mobile applications pour Windows et Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0f9da-105">This guide shows you how tooperform common scenarios using hello managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="0f9da-106">Si vous êtes tooMobile de nouvelles applications, vous devez envisager la première hello fin [démarrage rapide des applications mobiles Azure] [ 1] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0f9da-106">If you are new tooMobile Apps, you should consider first completing hello [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="0f9da-107">Dans ce guide, nous nous concentrer sur hello côté client géré SDK.</span><span class="sxs-lookup"><span data-stu-id="0f9da-107">In this guide, we focus on hello client-side managed SDK.</span></span> <span data-ttu-id="0f9da-108">toolearn savoir plus sur hello des kits de développement logiciel côté serveur pour les applications mobiles, consultez la documentation de hello pour hello [le Kit de développement .NET Server] [ 2] ou [Node.js serveur SDK] [ 3].</span><span class="sxs-lookup"><span data-stu-id="0f9da-108">toolearn more about hello server-side SDKs for Mobile Apps, see hello documentation for hello [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="0f9da-109">Documentation de référence</span><span class="sxs-lookup"><span data-stu-id="0f9da-109">Reference documentation</span></span>
<span data-ttu-id="0f9da-110">Hello documentation de référence pour le client hello SDK se trouve ici : [référence de client Azure Mobile Apps .NET][4].</span><span class="sxs-lookup"><span data-stu-id="0f9da-110">hello reference documentation for hello client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="0f9da-111">Vous pouvez également trouver des exemples de plusieurs clients Bonjour [référentiel GitHub d’exemples de Azure][5].</span><span class="sxs-lookup"><span data-stu-id="0f9da-111">You can also find several client samples in hello [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="0f9da-112">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="0f9da-112">Supported Platforms</span></span>
<span data-ttu-id="0f9da-113">Hello plateforme .NET prend en charge hello suivant plates-formes :</span><span class="sxs-lookup"><span data-stu-id="0f9da-113">hello .NET Platform supports hello following platforms:</span></span>

* <span data-ttu-id="0f9da-114">Versions Xamarin Android pour API 19 à 24 (KitKat jusqu’à Nougat)</span><span class="sxs-lookup"><span data-stu-id="0f9da-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="0f9da-115">Versions Xamarin iOS pour iOS 8.0 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="0f9da-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="0f9da-116">Plateforme Windows universelle</span><span class="sxs-lookup"><span data-stu-id="0f9da-116">Universal Windows Platform</span></span>
* <span data-ttu-id="0f9da-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="0f9da-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="0f9da-118">Windows Phone 8.0, à l’exception des applications Silverlight</span><span class="sxs-lookup"><span data-stu-id="0f9da-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="0f9da-119">l’authentification de « flux de serveur » Hello utilise un WebView hello affiche l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0f9da-119">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="0f9da-120">Si l’appareil de hello n’est pas en mesure de toopresent un UI WebView, autres méthodes d’authentification sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="0f9da-120">If hello device is not able toopresent a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="0f9da-121">Ce SDK ne convient donc pas au type Watch ou d’autres appareils restreints similaires.</span><span class="sxs-lookup"><span data-stu-id="0f9da-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="0f9da-122"><a name="setup"></a>Configuration et conditions préalables</span><span class="sxs-lookup"><span data-stu-id="0f9da-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="0f9da-123">Nous supposons que vous avez déjà créé et publié votre projet de backend Mobile Apps et qu'il comprend au moins une table.</span><span class="sxs-lookup"><span data-stu-id="0f9da-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="0f9da-124">Dans le code hello utilisé dans cette rubrique, table de hello est nommée `TodoItem` et qu’il a hello suivant colonnes : `Id`, `Text`, et `Complete`.</span><span class="sxs-lookup"><span data-stu-id="0f9da-124">In hello code used in this topic, hello table is named `TodoItem` and it has hello following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="0f9da-125">Cette table est hello même table créé lorsque vous complétez le [démarrage rapide des applications mobiles Azure][1].</span><span class="sxs-lookup"><span data-stu-id="0f9da-125">This table is hello same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="0f9da-126">Hello typé côté client type correspondant dans c# est hello suivant classe :</span><span class="sxs-lookup"><span data-stu-id="0f9da-126">hello corresponding typed client-side type in C# is hello following class:</span></span>

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

<span data-ttu-id="0f9da-127">Hello [JsonPropertyAttribute] [ 6] est utilisé toodefine hello *PropertyName* le mappage entre les champs de client hello et hello table.</span><span class="sxs-lookup"><span data-stu-id="0f9da-127">hello [JsonPropertyAttribute][6] is used toodefine hello *PropertyName* mapping between hello client field and hello table field.</span></span>

<span data-ttu-id="0f9da-128">toolearn comment toocreate les tables de votre serveur principal Mobile Apps, consultez hello [rubrique du serveur de développement .NET SDK] [ 7] ou hello [rubrique du SDK du serveur Node.js] [ 8] .</span><span class="sxs-lookup"><span data-stu-id="0f9da-128">toolearn how toocreate tables in your Mobile Apps backend, see hello [.NET Server SDK topic][7] or hello [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="0f9da-129">Si vous avez créé votre serveur principal de l’application Mobile Bonjour Azure à l’aide de portail hello démarrage rapide, vous pouvez également utiliser hello **tables facile** paramètre Bonjour [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="0f9da-129">If you created your Mobile App backend in hello Azure portal using hello QuickStart, you can also use hello **Easy tables** setting in hello [Azure portal].</span></span>

### <a name="how-to-install-hello-managed-client-sdk-package"></a><span data-ttu-id="0f9da-130">Comment : installer hello managed package SDK de client</span><span class="sxs-lookup"><span data-stu-id="0f9da-130">How to: Install hello managed client SDK package</span></span>
<span data-ttu-id="0f9da-131">Utilisez une des hello suivant hello tooinstall de méthodes managées package SDK de client pour les applications mobiles à partir de [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="0f9da-131">Use one of hello following methods tooinstall hello managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="0f9da-132">**Visual Studio** avec le bouton droit de votre projet, cliquez sur **gérer les Packages NuGet**, recherchez hello `Microsoft.Azure.Mobile.Client` du package, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="0f9da-133">**Xamarin Studio** avec le bouton droit de votre projet, cliquez sur **ajouter** > **ajouter des Packages NuGet**, recherchez hello `Microsoft.Azure.Mobile.Client `du package, puis cliquez sur **ajouter Package**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="0f9da-134">Dans votre fichier de l’activité principale, n’oubliez pas de suivant de hello tooadd **à l’aide de** instruction :</span><span class="sxs-lookup"><span data-stu-id="0f9da-134">In your main activity file, remember tooadd hello following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="0f9da-135"><a name="symbolsource"></a>Instructions : Utilisation des symboles de débogage dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f9da-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="0f9da-136">symboles Hello pour l’espace de noms hello Microsoft.Azure.Mobile sont disponibles sur [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="0f9da-136">hello symbols for hello Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="0f9da-137">Consultez toothe [SymbolSource instructions] [ 11] toointegrate SymbolSource avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f9da-137">Refer toothe [SymbolSource instructions][11] toointegrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="0f9da-138"><a name="create-client"></a>Créer le client des applications mobiles hello</span><span class="sxs-lookup"><span data-stu-id="0f9da-138"><a name="create-client"></a>Create hello Mobile Apps client</span></span>
<span data-ttu-id="0f9da-139">Hello de code suivant crée hello [MobileServiceClient] [ 12] objet tooaccess utilisé votre serveur principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="0f9da-139">hello following code creates hello [MobileServiceClient][12] object that is used tooaccess your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="0f9da-140">Bonjour précédant le code, remplacez `MOBILE_APP_URL` avec hello l’URL du serveur principal de l’application Mobile hello, qui se trouve dans le panneau pour le service principal de votre application Mobile Bonjour [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="0f9da-140">In hello preceding code, replace `MOBILE_APP_URL` with hello URL of hello Mobile App backend, which is found in the blade for your Mobile App backend in hello [Azure portal].</span></span> <span data-ttu-id="0f9da-141">MobileServiceClient (objet) Hello doit être un singleton.</span><span class="sxs-lookup"><span data-stu-id="0f9da-141">hello MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="0f9da-142">Utilisation des tables</span><span class="sxs-lookup"><span data-stu-id="0f9da-142">Work with Tables</span></span>
<span data-ttu-id="0f9da-143">Hello suivant section détaille comment toosearch et récupérer les enregistrements et modifier des données de hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-143">hello following section details how toosearch and retrieve records and modify hello data within hello table.</span></span>  <span data-ttu-id="0f9da-144">Hello rubriques suivantes est traitée :</span><span class="sxs-lookup"><span data-stu-id="0f9da-144">hello following topics are covered:</span></span>

* [<span data-ttu-id="0f9da-145">Création d'une référence de table</span><span class="sxs-lookup"><span data-stu-id="0f9da-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="0f9da-146">Données de requête</span><span class="sxs-lookup"><span data-stu-id="0f9da-146">Query data</span></span>](#querying)
* [<span data-ttu-id="0f9da-147">Filtrer les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="0f9da-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="0f9da-148">Trier les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="0f9da-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="0f9da-149">Renvoyer les données de pages</span><span class="sxs-lookup"><span data-stu-id="0f9da-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="0f9da-150">Sélectionner des colonnes spécifiques</span><span class="sxs-lookup"><span data-stu-id="0f9da-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="0f9da-151">Rechercher un enregistrement par ID</span><span class="sxs-lookup"><span data-stu-id="0f9da-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="0f9da-152">Traitement des requêtes non typées</span><span class="sxs-lookup"><span data-stu-id="0f9da-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="0f9da-153">Insertion de données</span><span class="sxs-lookup"><span data-stu-id="0f9da-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="0f9da-154">Mise à jour des données</span><span class="sxs-lookup"><span data-stu-id="0f9da-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="0f9da-155">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="0f9da-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="0f9da-156">Résolution des conflits et accès concurrentiel optimiste</span><span class="sxs-lookup"><span data-stu-id="0f9da-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="0f9da-157">Liaison tooa Interface utilisateur Windows</span><span class="sxs-lookup"><span data-stu-id="0f9da-157">Binding tooa Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="0f9da-158">Hello, taille de la Page de modification</span><span class="sxs-lookup"><span data-stu-id="0f9da-158">Changing hello Page Size</span></span>](#pagesize)

### <span data-ttu-id="0f9da-159"><a name="instantiating"></a>Procédure : création d'une référence de table</span><span class="sxs-lookup"><span data-stu-id="0f9da-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="0f9da-160">Tout code hello qui accède ou modifie des données dans une table principale appelle des fonctions sur hello `MobileServiceTable` objet.</span><span class="sxs-lookup"><span data-stu-id="0f9da-160">All hello code that accesses or modifies data in a backend table calls functions on hello `MobileServiceTable` object.</span></span> <span data-ttu-id="0f9da-161">Obtenir une table de toohello de référence en appelant hello [GetTable] méthode, comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f9da-161">Obtain a reference toohello table by calling hello [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="0f9da-162">Hello retourné d’objet utilise le modèle de sérialisation typé hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-162">hello returned object uses hello typed serialization model.</span></span> <span data-ttu-id="0f9da-163">Les modèles de sérialisation non typés sont également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0f9da-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="0f9da-164">L’exemple suivant [crée un tableau typé de référence tooan]:</span><span class="sxs-lookup"><span data-stu-id="0f9da-164">The following example [creates a reference tooan untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="0f9da-165">Dans les requêtes non typés, vous devez spécifier hello sous-jacent de chaîne de requête OData.</span><span class="sxs-lookup"><span data-stu-id="0f9da-165">In untyped queries, you must specify hello underlying OData query string.</span></span>

### <span data-ttu-id="0f9da-166"><a name="querying"></a>Interrogation des données à partir de votre application mobile</span><span class="sxs-lookup"><span data-stu-id="0f9da-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="0f9da-167">Cette section décrit comment tooissue interroge le principal de l’application Mobile toohello, qui inclut hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="0f9da-167">This section describes how tooissue queries toohello Mobile App backend, which includes hello following functionality:</span></span>

* [<span data-ttu-id="0f9da-168">Filtrer les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="0f9da-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="0f9da-169">Trier les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="0f9da-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="0f9da-170">Renvoyer les données de pages</span><span class="sxs-lookup"><span data-stu-id="0f9da-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="0f9da-171">Sélectionner des colonnes spécifiques</span><span class="sxs-lookup"><span data-stu-id="0f9da-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="0f9da-172">Rechercher des données par ID</span><span class="sxs-lookup"><span data-stu-id="0f9da-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="0f9da-173">Une taille de page d’orientée serveur est appliquée tooprevent toutes les lignes soit retourné.</span><span class="sxs-lookup"><span data-stu-id="0f9da-173">A server-driven page size is enforced tooprevent all rows from being returned.</span></span>  <span data-ttu-id="0f9da-174">La pagination conserve les requêtes par défaut pour les grands jeux de données à partir d’un effet négatif sur les service hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-174">Paging keeps default requests for large data sets from negatively impacting hello service.</span></span>  <span data-ttu-id="0f9da-175">tooreturn plus de 50 lignes, utilisez hello `Skip` et `Take` (méthode), comme décrit dans [retourner des données dans les pages](#paging).</span><span class="sxs-lookup"><span data-stu-id="0f9da-175">tooreturn more than 50 rows, use hello `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="0f9da-176"><a name="filtering"></a>Procédure : filtrage des données renvoyées</span><span class="sxs-lookup"><span data-stu-id="0f9da-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="0f9da-177">Hello de code suivant illustre comment les données toofilter en incluant un `Where` clause dans une requête.</span><span class="sxs-lookup"><span data-stu-id="0f9da-177">hello following code illustrates how toofilter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="0f9da-178">Il retourne tous les éléments de `todoTable` dont `Complete` propriété équivaut trop`false`.</span><span class="sxs-lookup"><span data-stu-id="0f9da-178">It returns all items from `todoTable` whose `Complete` property is equal too`false`.</span></span> <span data-ttu-id="0f9da-179">Hello [où] fonction applique une prédicat de requête de hello sur la table de hello de filtrage de ligne.</span><span class="sxs-lookup"><span data-stu-id="0f9da-179">hello [Where] function applies a row filtering predicate to hello query against hello table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="0f9da-180">Vous pouvez afficher hello URI du back-end du toohello hello demande envoyée à l’aide du logiciel de contrôle du message, telles que les outils de développement de navigateur ou [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="0f9da-180">You can view hello URI of hello request sent toohello backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="0f9da-181">Si vous examinez l’URI de la demande hello, notez que la chaîne de requête hello est modifié :</span><span class="sxs-lookup"><span data-stu-id="0f9da-181">If you look at hello request URI, notice that hello query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="0f9da-182">Cette requête OData est traduite par une requête SQL par hello SDK du serveur :</span><span class="sxs-lookup"><span data-stu-id="0f9da-182">This OData request is translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="0f9da-183">Hello fonction passée toohello `Where` méthode peut avoir un nombre arbitraire de conditions.</span><span class="sxs-lookup"><span data-stu-id="0f9da-183">hello function that is passed toohello `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="0f9da-184">Cet exemple se traduirait en une requête SQL par hello SDK du serveur :</span><span class="sxs-lookup"><span data-stu-id="0f9da-184">This example would be translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="0f9da-185">Cette requête peut également être fractionnée en plusieurs clauses :</span><span class="sxs-lookup"><span data-stu-id="0f9da-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="0f9da-186">Bonjour, deux méthodes sont équivalentes et peuvent être utilisés indifféremment.</span><span class="sxs-lookup"><span data-stu-id="0f9da-186">hello two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="0f9da-187">Hello première option&mdash;de la concaténation de plusieurs prédicats dans une requête&mdash;est plus compact et recommandé.</span><span class="sxs-lookup"><span data-stu-id="0f9da-187">hello former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="0f9da-188">Hello `Where` clause prend en charge les opérations d’être traduit en un sous-ensemble d’OData hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-188">hello `Where` clause supports operations that be translated into hello OData subset.</span></span> <span data-ttu-id="0f9da-189">Les opérations incluent :</span><span class="sxs-lookup"><span data-stu-id="0f9da-189">Operations include:</span></span>

* <span data-ttu-id="0f9da-190">les opérateurs relationnels (==, !=, <, <=, >, >=),</span><span class="sxs-lookup"><span data-stu-id="0f9da-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="0f9da-191">les opérateurs arithmétiques (+, -, /, *, %),</span><span class="sxs-lookup"><span data-stu-id="0f9da-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="0f9da-192">la précision des nombres (Math.Floor, Math.Ceiling),</span><span class="sxs-lookup"><span data-stu-id="0f9da-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="0f9da-193">les fonctions de chaîne (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span><span class="sxs-lookup"><span data-stu-id="0f9da-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="0f9da-194">les propriétés de date (Year, Month, Day, Hour, Minute, Second),</span><span class="sxs-lookup"><span data-stu-id="0f9da-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="0f9da-195">les propriétés d’accès d’un objet, ainsi que</span><span class="sxs-lookup"><span data-stu-id="0f9da-195">Access properties of an object, and</span></span>
* <span data-ttu-id="0f9da-196">les expressions qui combinent toutes ces opérations.</span><span class="sxs-lookup"><span data-stu-id="0f9da-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="0f9da-197">Lorsque le compte tenu que hello serveur SDK prend en charge, vous pouvez envisager hello [OData v3 Documentation].</span><span class="sxs-lookup"><span data-stu-id="0f9da-197">When considering what hello Server SDK supports, you can consider hello [OData v3 Documentation].</span></span>

### <span data-ttu-id="0f9da-198"><a name="sorting"></a>Procédure : tri des données renvoyées</span><span class="sxs-lookup"><span data-stu-id="0f9da-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="0f9da-199">Hello de code suivant illustre comment les données toosort en incluant un [OrderBy] ou [OrderByDescending] fonction de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-199">hello following code illustrates how toosort data by including an [OrderBy] or [OrderByDescending] function in hello query.</span></span> <span data-ttu-id="0f9da-200">Elle renvoie les éléments de `todoTable` triée par ordre croissant par hello `Text` champ.</span><span class="sxs-lookup"><span data-stu-id="0f9da-200">It returns items from `todoTable` sorted ascending by hello `Text` field.</span></span>

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

### <span data-ttu-id="0f9da-201"><a name="paging"></a>Procédure : renvoi des données de pages</span><span class="sxs-lookup"><span data-stu-id="0f9da-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="0f9da-202">Par défaut, hello principal retourne hello uniquement les 50 premières lignes.</span><span class="sxs-lookup"><span data-stu-id="0f9da-202">By default, hello backend returns only hello first 50 rows.</span></span> <span data-ttu-id="0f9da-203">Vous pouvez augmenter le nombre hello de lignes retournées par l’appelant hello [prendre] (méthode).</span><span class="sxs-lookup"><span data-stu-id="0f9da-203">You can increase hello number of returned rows by calling hello [Take] method.</span></span> <span data-ttu-id="0f9da-204">Utilisez `Take` avec hello [ignorer] méthode toorequest une spécifique « page » du jeu de données total hello retournée par la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-204">Use `Take` along with hello [Skip] method toorequest a specific "page" of hello total dataset returned by hello query.</span></span> <span data-ttu-id="0f9da-205">Hello requête suivante, lors de l’exécution, retourne hello trois premiers éléments de tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-205">hello following query, when executed, returns hello top three items in hello table.</span></span>

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="0f9da-206">ignore la requête modifiée suivante Hello hello trois premiers résultats et retourne hello trois résultats.</span><span class="sxs-lookup"><span data-stu-id="0f9da-206">hello following revised query skips hello first three results and returns hello next three results.</span></span> <span data-ttu-id="0f9da-207">Cette requête produit hello deuxième « page » de données, où la taille de la page hello est trois éléments :</span><span class="sxs-lookup"><span data-stu-id="0f9da-207">This query produces hello second "page" of data, where hello page size is three items.</span></span>

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="0f9da-208">Hello [IncludeTotalCount] méthode demande hello nombre total de *tous les* hello enregistrements qui auraient été retournés, en ignorant toute clause de pagination/limitation spécifiée :</span><span class="sxs-lookup"><span data-stu-id="0f9da-208">hello [IncludeTotalCount] method requests hello total count for *all* hello records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="0f9da-209">Dans une application réelle, vous pouvez utiliser toohello similaire de requêtes précédent exemple avec un contrôle pager ou d’une interface utilisateur comparable à naviguer entre les pages.</span><span class="sxs-lookup"><span data-stu-id="0f9da-209">In a real world app, you can use queries similar toohello preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="0f9da-210">limite de 50 lignes toooverride hello dans un service principal de l’application Mobile, vous devez également appliquer hello [EnableQueryAttribute] toohello public GET (méthode) et spécifier le comportement de pagination hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-210">toooverride hello 50-row limit in a Mobile App backend, you must also apply hello [EnableQueryAttribute] toohello public GET method and specify hello paging behavior.</span></span> <span data-ttu-id="0f9da-211">Lorsque toohello appliqué méthode, hello suivant définit le nombre maximal de lignes retourné too1000 :</span><span class="sxs-lookup"><span data-stu-id="0f9da-211">When applied toohello method, hello following sets the maximum returned rows too1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="0f9da-212"><a name="selecting"></a>Procédure : sélection de colonnes spécifiques</span><span class="sxs-lookup"><span data-stu-id="0f9da-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="0f9da-213">Vous pouvez indiquer quel jeu de propriétés des tooinclude Bonjour génère en ajoutant un [sélectionnez] requête tooyour de clause.</span><span class="sxs-lookup"><span data-stu-id="0f9da-213">You can specify which set of properties tooinclude in hello results by adding a [Select] clause tooyour query.</span></span> <span data-ttu-id="0f9da-214">Par exemple, hello suivant de code montre comment tooselect à un seul champ et également comment tooselect et mettre en forme plusieurs champs :</span><span class="sxs-lookup"><span data-stu-id="0f9da-214">For example, hello following code shows how tooselect just one field and also how tooselect and format multiple fields:</span></span>

```
// Select one field -- just hello Text
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

<span data-ttu-id="0f9da-215">Tous les hello fonctions décrites jusqu'à présent sont additives, donc nous pouvons conserver liant.</span><span class="sxs-lookup"><span data-stu-id="0f9da-215">All hello functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="0f9da-216">Chaque appel chaînée affecte plus de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-216">Each chained call affects more of hello query.</span></span> <span data-ttu-id="0f9da-217">Un exemple supplémentaire :</span><span class="sxs-lookup"><span data-stu-id="0f9da-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="0f9da-218"><a name="lookingup"></a>Procédure : recherche de données par ID</span><span class="sxs-lookup"><span data-stu-id="0f9da-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="0f9da-219">Hello [LookupAsync] fonction peut être utilisé toolook des objets de base de données hello avec un ID particulier.</span><span class="sxs-lookup"><span data-stu-id="0f9da-219">hello [LookupAsync] function can be used toolook up objects from hello database with a particular ID.</span></span>

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="0f9da-220"><a name="untypedqueries"></a>Exécution de requêtes non typées</span><span class="sxs-lookup"><span data-stu-id="0f9da-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="0f9da-221">Lorsque vous exécutez une requête à l’aide d’un objet de table non typé, vous devez spécifier explicitement de chaîne de requête OData hello en appelant [ReadAsync], comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0f9da-221">When executing a query using an untyped table object, you must explicitly specify hello OData query string by calling [ReadAsync], as in hello following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="0f9da-222">Vous obtenez en retour des valeurs JSON que vous pouvez utiliser comme conteneur de propriétés.</span><span class="sxs-lookup"><span data-stu-id="0f9da-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="0f9da-223">Pour plus d’informations sur JToken et Newtonsoft Json.NET, consultez hello [Json.NET] site.</span><span class="sxs-lookup"><span data-stu-id="0f9da-223">For more information on JToken and Newtonsoft Json.NET, see hello [Json.NET] site.</span></span>

### <span data-ttu-id="0f9da-224"><a name="inserting"></a>Insertion de données dans un backend Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="0f9da-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="0f9da-225">Tous les types clients doivent contenir un membre nommé **Id**, par défaut une chaîne.</span><span class="sxs-lookup"><span data-stu-id="0f9da-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="0f9da-226">Cela **Id** est requis pour effectuer des opérations CRUD et de synchronisation hors connexion. Pourquoi suivant de code illustre comment toouse hello [InsertAsync] méthode tooinsert nouvelles lignes dans une table.</span><span class="sxs-lookup"><span data-stu-id="0f9da-226">This **Id** is required to perform CRUD operations and for offline sync. hello following code illustrates how toouse hello [InsertAsync] method tooinsert new rows into a table.</span></span> <span data-ttu-id="0f9da-227">paramètre Hello contient hello toobe de données insérée en tant qu’objet .NET.</span><span class="sxs-lookup"><span data-stu-id="0f9da-227">hello parameter contains hello data toobe inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="0f9da-228">Si une valeur d’ID unique personnalisée n’est pas incluse dans hello `todoItem` lors d’une insertion, un GUID est généré par le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-228">If a unique custom ID value is not included in hello `todoItem` during an insert, a GUID is generated by hello server.</span></span>
<span data-ttu-id="0f9da-229">Vous pouvez récupérer hello des Id généré en examinant l’objet de hello après le retour de l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-229">You can retrieve hello generated Id by inspecting hello object after hello call returns.</span></span>

<span data-ttu-id="0f9da-230">tooinsert non typées de données, vous pouvez tirer parti de Json.NET :</span><span class="sxs-lookup"><span data-stu-id="0f9da-230">tooinsert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="0f9da-231">Voici un exemple utilisant une adresse de messagerie comme ID de chaîne unique :</span><span class="sxs-lookup"><span data-stu-id="0f9da-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="0f9da-232">Utilisation de valeurs d'ID</span><span class="sxs-lookup"><span data-stu-id="0f9da-232">Working with ID values</span></span>
<span data-ttu-id="0f9da-233">Applications mobiles prend en charge les valeurs de chaîne personnalisé unique pour la table hello **id** colonne.</span><span class="sxs-lookup"><span data-stu-id="0f9da-233">Mobile Apps supports unique custom string values for hello table's **id** column.</span></span> <span data-ttu-id="0f9da-234">Valeur de chaîne permet aux applications toouse des valeurs personnalisées telles que les adresses de messagerie ou les noms d’utilisateur pour l’ID de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-234">A string value allows applications toouse custom values such as email addresses or user names for hello ID.</span></span>  <span data-ttu-id="0f9da-235">ID de chaîne fournissent hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0f9da-235">String IDs provide you with hello following benefits:</span></span>

* <span data-ttu-id="0f9da-236">Un ID est généré sans passer d’une base de données toohello aller-retour.</span><span class="sxs-lookup"><span data-stu-id="0f9da-236">IDs are generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="0f9da-237">Les enregistrements sont toomerge plus facile à partir de différentes tables ou bases de données.</span><span class="sxs-lookup"><span data-stu-id="0f9da-237">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="0f9da-238">Les valeurs d’ID peuvent mieux s’intégrer à la logique d’une application.</span><span class="sxs-lookup"><span data-stu-id="0f9da-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="0f9da-239">Lorsqu’une valeur d’ID de chaîne n’est pas définie sur un enregistrement inséré, le principal de l’application Mobile hello génère une valeur unique pour le code.</span><span class="sxs-lookup"><span data-stu-id="0f9da-239">When a string ID value is not set on an inserted record, hello Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="0f9da-240">Vous pouvez utiliser hello [Guid.NewGuid] toogenerate méthode votre propre ID de valeurs, soit sur le client de hello hello principal.</span><span class="sxs-lookup"><span data-stu-id="0f9da-240">You can use hello [Guid.NewGuid] method toogenerate your own ID values, either on hello client or in hello backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="0f9da-241"><a name="modifying"></a>Modification de données dans un backend Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="0f9da-241"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="0f9da-242">Hello de code suivant illustre comment toouse hello [UpdateAsync] méthode tooupdate un enregistrement existant avec hello même ID avec de nouvelles informations.</span><span class="sxs-lookup"><span data-stu-id="0f9da-242">hello following code illustrates how toouse hello [UpdateAsync] method tooupdate an existing record with hello same ID with new information.</span></span> <span data-ttu-id="0f9da-243">paramètre Hello contient hello toobe de données mis à jour en tant qu’objet .NET.</span><span class="sxs-lookup"><span data-stu-id="0f9da-243">hello parameter contains hello data toobe updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="0f9da-244">tooupdate non typées de données, vous pouvez tirer parti de [Json.NET] comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f9da-244">tooupdate untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="0f9da-245">Vous devez spécifier un champ `id` si vous effectuez une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="0f9da-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="0f9da-246">Hello principal utilise hello `id` tooidentify de champ qui tooupdate de ligne.</span><span class="sxs-lookup"><span data-stu-id="0f9da-246">hello backend uses hello `id` field tooidentify which row tooupdate.</span></span> <span data-ttu-id="0f9da-247">Hello `id` champ peut être obtenu à partir du résultat de hello Hello `InsertAsync` appeler.</span><span class="sxs-lookup"><span data-stu-id="0f9da-247">hello `id` field can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="0f9da-248">Un `ArgumentException` est générée si vous essayez de tooupdate un élément sans fournir de hello `id` valeur.</span><span class="sxs-lookup"><span data-stu-id="0f9da-248">An `ArgumentException` is raised if you try tooupdate an item without providing hello `id` value.</span></span>

### <span data-ttu-id="0f9da-249"><a name="deleting"></a>Suppression de données dans un backend Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="0f9da-249"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="0f9da-250">Hello de code suivant illustre comment toouse hello [DeleteAsync] méthode toodelete une instance existante.</span><span class="sxs-lookup"><span data-stu-id="0f9da-250">hello following code illustrates how toouse hello [DeleteAsync] method toodelete an existing instance.</span></span> <span data-ttu-id="0f9da-251">instance de Hello est identifiée par hello `id` champ ensemble sur hello `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="0f9da-251">hello instance is identified by hello `id` field set on hello `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="0f9da-252">toodelete non typées de données, vous pouvez tirer parti de Json.NET comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f9da-252">toodelete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="0f9da-253">Vous devez spécifier un ID lorsque vous effectuez une requête de suppression.</span><span class="sxs-lookup"><span data-stu-id="0f9da-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="0f9da-254">Autres propriétés ne sont pas transmises toohello service ou sont ignorées au niveau de service de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-254">Other properties are not passed toohello service or are ignored at hello service.</span></span> <span data-ttu-id="0f9da-255">Hello du résultat d’une `DeleteAsync` appel est généralement `null`.</span><span class="sxs-lookup"><span data-stu-id="0f9da-255">hello result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="0f9da-256">toopass de code Hello dans peut être obtenu à partir du résultat de hello Hello `InsertAsync` appeler.</span><span class="sxs-lookup"><span data-stu-id="0f9da-256">hello ID toopass in can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="0f9da-257">A `MobileServiceInvalidOperationException` est levée lorsque vous essayez de toodelete un élément sans spécifier hello `id` champ.</span><span class="sxs-lookup"><span data-stu-id="0f9da-257">A `MobileServiceInvalidOperationException` is thrown when you try toodelete an item without specifying hello `id` field.</span></span>

### <span data-ttu-id="0f9da-258"><a name="optimisticconcurrency"></a>Procédure : Utilisation de l’accès concurrentiel optimiste pour résoudre les conflits</span><span class="sxs-lookup"><span data-stu-id="0f9da-258"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="0f9da-259">Deux ou plusieurs clients peuvent écrire les modifications toohello même élément à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="0f9da-259">Two or more clients may write changes toohello same item at hello same time.</span></span> <span data-ttu-id="0f9da-260">Sans la détection de conflit, dernière écriture de hello remplace toutes les mises à jour précédentes.</span><span class="sxs-lookup"><span data-stu-id="0f9da-260">Without conflict detection, hello last write would overwrite any previous updates.</span></span> <span data-ttu-id="0f9da-261">**contrôle d'accès concurrentiel optimiste** considère que chaque transaction peut être validée et, qu’à ce titre, elle ne fait appel à aucun verrouillage de ressources.</span><span class="sxs-lookup"><span data-stu-id="0f9da-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="0f9da-262">Avant de valider une transaction, contrôle d’accès concurrentiel optimiste vérifie qu’aucune autre transaction n’a modifié les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0f9da-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified hello data.</span></span> <span data-ttu-id="0f9da-263">Si les données de salutation a été modifiées, hello validation de la transaction est restaurée.</span><span class="sxs-lookup"><span data-stu-id="0f9da-263">If hello data has been modified, hello committing transaction is rolled back.</span></span>

<span data-ttu-id="0f9da-264">Applications mobiles prend en charge le contrôle d’accès concurrentiel optimiste en effectuant le suivi d’élément de tooeach de modifications à l’aide de hello `version` colonne de propriété système qui est défini pour chaque table dans votre service principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="0f9da-264">Mobile Apps supports optimistic concurrency control by tracking changes tooeach item using hello `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="0f9da-265">Chaque fois un enregistrement est mis à jour, les applications mobiles définit hello `version` propriété pour cet enregistrement tooa nouvelle valeur.</span><span class="sxs-lookup"><span data-stu-id="0f9da-265">Each time a record is updated, Mobile Apps sets hello `version` property for that record tooa new value.</span></span> <span data-ttu-id="0f9da-266">Lors de chaque demande de mise à jour, hello `version` propriété d’enregistrement hello inclus avec la demande de hello est toohello comparé même propriété pour l’enregistrement hello sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-266">During each update request, hello `version` property of hello record included with hello request is compared toohello same property for hello record on hello server.</span></span> <span data-ttu-id="0f9da-267">Si la version passée avec la demande de hello ne correspond pas à hello principal, puis déclenche de la bibliothèque cliente de hello un `MobileServicePreconditionFailedException<T>` exception.</span><span class="sxs-lookup"><span data-stu-id="0f9da-267">If the version passed with hello request does not match hello backend, then hello client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="0f9da-268">type Hello inclus avec l’exception de hello est enregistrement hello de hello principal contenant hello serveurs version de l’enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-268">hello type included with hello exception is hello record from hello backend containing hello servers version of hello record.</span></span> <span data-ttu-id="0f9da-269">Hello application peut ensuite utiliser cette toodecide informations si demande de mise à jour tooexecute hello avec hello correct `version` valeur à partir de modifications toocommit hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-269">hello application can then use this information toodecide whether tooexecute hello update request again with hello correct `version` value from hello backend toocommit changes.</span></span>

<span data-ttu-id="0f9da-270">Définir une colonne sur la classe de table hello pour hello `version` système propriété tooenable l’accès concurrentiel optimiste.</span><span class="sxs-lookup"><span data-stu-id="0f9da-270">Define a column on hello table class for hello `version` system property tooenable optimistic concurrency.</span></span> <span data-ttu-id="0f9da-271">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0f9da-271">For example:</span></span>

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

<span data-ttu-id="0f9da-272">Applications à l’aide de tables non typés activer l’accès concurrentiel optimiste en définissant un hello `Version` indicateur sur le `SystemProperties` de hello table comme suit.</span><span class="sxs-lookup"><span data-stu-id="0f9da-272">Applications using untyped tables enable optimistic concurrency by setting hello `Version` flag on the `SystemProperties` of hello table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="0f9da-273">En outre tooenabling d’accès concurrentiel optimiste, vous devez également intercepter hello `MobileServicePreconditionFailedException<T>` exception dans votre code lors de l’appel [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="0f9da-273">In addition tooenabling optimistic concurrency, you must also catch hello `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="0f9da-274">Résoudre le conflit de hello en appliquant hello correct `version` toothe mis à jour l’enregistrement et l’appel [UpdateAsync] avec hello résolu l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="0f9da-274">Resolve hello conflict by applying hello correct `version` toothe updated record and call [UpdateAsync] with hello resolved record.</span></span> <span data-ttu-id="0f9da-275">Hello suivant de code montre comment tooresolve un conflit d’écriture une fois détectée :</span><span class="sxs-lookup"><span data-stu-id="0f9da-275">hello following code shows how tooresolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
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
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="0f9da-276">Pour plus d’informations, consultez hello [synchronisation des données hors connexion dans les applications mobiles Azure] rubrique.</span><span class="sxs-lookup"><span data-stu-id="0f9da-276">For more information, see hello [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="0f9da-277"><a name="binding"></a>Comment : interface utilisateur de liaison Mobile Apps données tooa Windows</span><span class="sxs-lookup"><span data-stu-id="0f9da-277"><a name="binding"></a>How to: Bind Mobile Apps data tooa Windows user interface</span></span>
<span data-ttu-id="0f9da-278">Cette section montre comment toodisplay retourné des objets de données à l’aide des éléments d’interface utilisateur dans une application Windows.</span><span class="sxs-lookup"><span data-stu-id="0f9da-278">This section shows how toodisplay returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="0f9da-279">L’exemple de code suivant lie la source toohello de liste hello avec une requête pour des éléments incomplets.</span><span class="sxs-lookup"><span data-stu-id="0f9da-279">The following example code binds toohello source of hello list with a query for incomplete items.</span></span> <span data-ttu-id="0f9da-280">[MobileServiceCollection] permet de créer une collection de liaisons prenant en charge Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="0f9da-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="0f9da-281">Certains contrôles Bonjour gérés prise en charge du runtime une interface appelée [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="0f9da-281">Some controls in hello managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="0f9da-282">Cette interface permet à des contrôles toorequest des données supplémentaires lorsque hello utilisateur fait défiler.</span><span class="sxs-lookup"><span data-stu-id="0f9da-282">This interface allows controls toorequest extra data when hello user scrolls.</span></span> <span data-ttu-id="0f9da-283">Il existe une prise en charge intégrée pour cette interface pour les applications Windows universelles via [MobileServiceIncrementalLoadingCollection], qui gère automatiquement les appels à partir de contrôles de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from hello controls.</span></span> <span data-ttu-id="0f9da-284">Utilisez `MobileServiceIncrementalLoadingCollection` dans les applications Windows, comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f9da-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="0f9da-285">toouse hello nouveau regroupement sur les applications Windows Phone 8 et « Silverlight », utilisez hello `ToCollection` méthodes d’extension sur `IMobileServiceTableQuery<T>` et `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="0f9da-285">toouse hello new collection on Windows Phone 8 and "Silverlight" apps, use hello `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="0f9da-286">les données tooload, appelez `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="0f9da-286">tooload data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="0f9da-287">Lorsque vous utilisez collection hello créée en appelant `ToCollectionAsync` ou `ToCollection`, vous obtenez une collection qui peut être liée tooUI contrôles.</span><span class="sxs-lookup"><span data-stu-id="0f9da-287">When you use hello collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound tooUI controls.</span></span>  <span data-ttu-id="0f9da-288">Cette collection prend en charge la pagination.</span><span class="sxs-lookup"><span data-stu-id="0f9da-288">This collection is paging-aware.</span></span>  <span data-ttu-id="0f9da-289">Étant donné que la collection de hello est chargement des données à partir du réseau, le chargement parfois échoue.</span><span class="sxs-lookup"><span data-stu-id="0f9da-289">Since hello collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="0f9da-290">toohandle ces défaillances, substituez hello `OnException` méthode sur `MobileServiceIncrementalLoadingCollection` toohandle les exceptions résultant des appels trop`LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="0f9da-290">toohandle such failures, override hello `OnException` method on `MobileServiceIncrementalLoadingCollection` toohandle exceptions resulting from calls too`LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="0f9da-291">Prendre en compte si votre table comporte plusieurs champs, mais que vous voulez uniquement toodisplay certaines d'entre elles dans votre contrôle.</span><span class="sxs-lookup"><span data-stu-id="0f9da-291">Consider if your table has many fields but you only want toodisplay some of them in your control.</span></span> <span data-ttu-id="0f9da-292">Vous pouvez utiliser les conseils hello Bonjour précédant la section «[sélectionner des colonnes spécifiques](#selecting)« toodisplay de colonnes spécifiques tooselect Bonjour l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0f9da-292">You may use hello guidance in hello preceding section "[Select specific columns](#selecting)" tooselect specific columns toodisplay in hello UI.</span></span>

### <span data-ttu-id="0f9da-293"><a name="pagesize"></a>Hello de modifier la taille de Page</span><span class="sxs-lookup"><span data-stu-id="0f9da-293"><a name="pagesize"></a>Change hello Page size</span></span>
<span data-ttu-id="0f9da-294">Par défaut, Azure Mobile Apps retourne au maximum 50 éléments par demande.</span><span class="sxs-lookup"><span data-stu-id="0f9da-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="0f9da-295">Vous pouvez modifier la taille de la pagination hello en augmentant la taille de page maximale hello sur hello client et le serveur.</span><span class="sxs-lookup"><span data-stu-id="0f9da-295">You can change hello paging size by increasing hello maximum page size on both hello client and server.</span></span>  <span data-ttu-id="0f9da-296">tooincrease hello la taille de la page demandée, spécifiez `PullOptions` lors de l’utilisation `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="0f9da-296">tooincrease hello requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="0f9da-297">Si vous avez apporté hello `PageSize` tooor égal supérieure à 100 au sein du serveur de hello, une demande renvoie jusqu'à 100 éléments.</span><span class="sxs-lookup"><span data-stu-id="0f9da-297">Assuming you have made hello `PageSize` equal tooor greater than 100 within hello server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="0f9da-298"><a name="#offlinesync"></a>Utilisation de tables hors connexion</span><span class="sxs-lookup"><span data-stu-id="0f9da-298"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="0f9da-299">Des tables hors connexion utilisent un toostore de magasin local SQLite données pour une utilisation en mode hors connexion.</span><span class="sxs-lookup"><span data-stu-id="0f9da-299">Offline tables use a local SQLite store toostore data for use when offline.</span></span>  <span data-ttu-id="0f9da-300">Tableau de toutes les opérations sont effectuées par rapport à hello local SQLite stocker au lieu de la banque du serveur distant hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-300">All table operations are done against hello local SQLite store instead of hello remote server store.</span></span>  <span data-ttu-id="0f9da-301">toocreate une table en mode hors connexion, d’abord préparer votre projet :</span><span class="sxs-lookup"><span data-stu-id="0f9da-301">toocreate an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="0f9da-302">Dans Visual Studio, cliquez sur la solution de hello > **gérer les Packages NuGet pour la Solution...** , puis recherchez et installez le **Microsoft.Azure.Mobile.Client.SQLiteStore** package NuGet pour tous les projets dans la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-302">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="0f9da-303">Toosupport (facultatif) les appareils Windows, installez un de hello suivant SQLite runtime packages :</span><span class="sxs-lookup"><span data-stu-id="0f9da-303">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="0f9da-304">**Windows 8.1 Runtime :** installez [SQLite pour Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="0f9da-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="0f9da-305">**Windows Phone 8.1 :** installez [SQLite pour Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="0f9da-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="0f9da-306">**Plateforme Windows universelle** installer [SQLite pour hello Windows universelles][5].</span><span class="sxs-lookup"><span data-stu-id="0f9da-306">**Universal Windows Platform** Install [SQLite for hello Universal Windows][5].</span></span>
3. <span data-ttu-id="0f9da-307">(Facultatif).</span><span class="sxs-lookup"><span data-stu-id="0f9da-307">(Optional).</span></span> <span data-ttu-id="0f9da-308">Pour les appareils Windows, cliquez sur **références** > **ajouter une référence...** , développez hello **Windows** dossier > **Extensions**, puis activer hello approprié **SQLite pour Windows** SDK avec hello  **Visual C++ 2013 Runtime pour Windows** Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="0f9da-308">For Windows devices, click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**, then enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="0f9da-309">Hello SQLite SDK noms varient légèrement avec chaque plate-forme Windows.</span><span class="sxs-lookup"><span data-stu-id="0f9da-309">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="0f9da-310">Avant de pouvoir créer une référence de table, le magasin local de hello doit être préparée :</span><span class="sxs-lookup"><span data-stu-id="0f9da-310">Before a table reference can be created, hello local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="0f9da-311">L’initialisation du magasin est normalement effectuée immédiatement après que hello client est créé.</span><span class="sxs-lookup"><span data-stu-id="0f9da-311">Store initialization is normally done immediately after hello client is created.</span></span>  <span data-ttu-id="0f9da-312">Hello **OfflineDbPath** doit être un nom de fichier pouvant être utilisée sur toutes les plateformes prises en charge.</span><span class="sxs-lookup"><span data-stu-id="0f9da-312">hello **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="0f9da-313">Si le chemin d’accès hello est un chemin d’accès qualifié complet (autrement dit, il commence par une barre oblique), ce chemin d’accès est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0f9da-313">If hello path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="0f9da-314">Si le chemin d’accès hello n’est pas pleinement qualifié, fichier de hello est placé dans un emplacement spécifique à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="0f9da-314">If hello path is not fully qualified, hello file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="0f9da-315">Pour les appareils iOS et Android, chemin d’accès par défaut de hello est hello « personnel » temporaires.</span><span class="sxs-lookup"><span data-stu-id="0f9da-315">For iOS and Android devices, hello default path is hello "Personal Files" folder.</span></span>
* <span data-ttu-id="0f9da-316">Pour les appareils Windows, le chemin d’accès de hello par défaut est dossier de « AppData » hello spécifiques à l’application.</span><span class="sxs-lookup"><span data-stu-id="0f9da-316">For Windows devices, hello default path is hello application-specific "AppData" folder.</span></span>

<span data-ttu-id="0f9da-317">Une référence de table peut être obtenue à l’aide de hello `GetSyncTable<>` méthode :</span><span class="sxs-lookup"><span data-stu-id="0f9da-317">A table reference can be obtained using hello `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="0f9da-318">Vous n’avez pas besoin de tooauthenticate toouse une table en mode hors connexion.</span><span class="sxs-lookup"><span data-stu-id="0f9da-318">You do not need tooauthenticate toouse an offline table.</span></span>  <span data-ttu-id="0f9da-319">Vous ne devez tooauthenticate lorsque vous communiquez avec le service principal de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-319">You only need tooauthenticate when you are communicating with hello backend service.</span></span>

### <span data-ttu-id="0f9da-320"><a name="syncoffline"></a>Synchronisation d’une table hors connexion</span><span class="sxs-lookup"><span data-stu-id="0f9da-320"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="0f9da-321">Les tables en mode hors connexion ne sont pas synchronisées avec le serveur principal hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="0f9da-321">Offline tables are not synchronized with hello backend by default.</span></span>  <span data-ttu-id="0f9da-322">La synchronisation est divisée en deux parties.</span><span class="sxs-lookup"><span data-stu-id="0f9da-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="0f9da-323">Vous pouvez transmettre des modifications en dehors du processus de téléchargement de nouveaux éléments.</span><span class="sxs-lookup"><span data-stu-id="0f9da-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="0f9da-324">Voici une méthode de synchronisation typique :</span><span class="sxs-lookup"><span data-stu-id="0f9da-324">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
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

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
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

<span data-ttu-id="0f9da-325">Si hello premier argument trop`PullAsync` a la valeur null, puis la synchronisation incrémentielle n’est pas utilisée.</span><span class="sxs-lookup"><span data-stu-id="0f9da-325">If hello first argument too`PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="0f9da-326">Chaque opération de synchronisation récupère tous les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0f9da-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="0f9da-327">Hello SDK effectue implicite `PushAsync()` avant l’extraction des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0f9da-327">hello SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="0f9da-328">La gestion des conflits s’effectue par le biais d’une méthode `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="0f9da-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="0f9da-329">Vous pouvez traiter les conflits Bonjour même manière que les tables en ligne.</span><span class="sxs-lookup"><span data-stu-id="0f9da-329">You can deal with conflicts in hello same way as online tables.</span></span>  <span data-ttu-id="0f9da-330">conflit de Hello est généré lorsque `PullAsync()` est appelé à la place de lors de hello insert, update ou delete.</span><span class="sxs-lookup"><span data-stu-id="0f9da-330">hello conflict is produced when `PullAsync()` is called instead of during hello insert, update, or delete.</span></span> <span data-ttu-id="0f9da-331">Si plusieurs conflits se produisent, les opérations sont regroupées dans une seule MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="0f9da-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="0f9da-332">Gérez chaque défaillance séparément.</span><span class="sxs-lookup"><span data-stu-id="0f9da-332">Handle each failure separately.</span></span>

## <span data-ttu-id="0f9da-333"><a name="#customapi"></a>Utilisation d’une API personnalisée</span><span class="sxs-lookup"><span data-stu-id="0f9da-333"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="0f9da-334">Une API personnalisée vous permet de toodefine points de terminaison personnalisés qui exposent les fonctionnalités de serveur qui ne pas mapper tooan insérer, mettre à jour, supprimer ou opération de lecture.</span><span class="sxs-lookup"><span data-stu-id="0f9da-334">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="0f9da-335">En utilisant une API personnalisée, vous pouvez exercer davantage de contrôle sur la messagerie, notamment lire et définir des en-têtes de message HTTP et définir un format de corps de message autre que JSON.</span><span class="sxs-lookup"><span data-stu-id="0f9da-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="0f9da-336">Vous appelez une API personnalisée en appelant une de hello [InvokeApiAsync] méthodes sur le client de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-336">You call a custom API by calling one of hello [InvokeApiAsync] methods on hello client.</span></span> <span data-ttu-id="0f9da-337">Par exemple, hello ligne de code suivante envoie un toohello de la demande POST **completeAll** API sur hello principal :</span><span class="sxs-lookup"><span data-stu-id="0f9da-337">For example, hello following line of code sends a POST request toohello **completeAll** API on hello backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="0f9da-338">Ce formulaire est un appel de méthode typée et requiert que hello **MarkAllResult** retourner le type est défini.</span><span class="sxs-lookup"><span data-stu-id="0f9da-338">This form is a typed method call and requires that hello **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="0f9da-339">Les méthodes typées et non typées sont toutes deux prises en charge.</span><span class="sxs-lookup"><span data-stu-id="0f9da-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="0f9da-340">Hello InvokeApiAsync() méthode ajoute/api/API toohello que vous le souhaitez toocall, sauf si hello API commence par un « / ».</span><span class="sxs-lookup"><span data-stu-id="0f9da-340">hello InvokeApiAsync() method prepends '/api/' toohello API that you wish toocall unless hello API starts with a '/'.</span></span>
<span data-ttu-id="0f9da-341">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0f9da-341">For example:</span></span>

* <span data-ttu-id="0f9da-342">`InvokeApiAsync("completeAll",...)`appelle /api/completeAll sur hello principal</span><span class="sxs-lookup"><span data-stu-id="0f9da-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on hello backend</span></span>
* <span data-ttu-id="0f9da-343">`InvokeApiAsync("/.auth/me",...)`appelle /.auth/me sur hello principal</span><span class="sxs-lookup"><span data-stu-id="0f9da-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on hello backend</span></span>

<span data-ttu-id="0f9da-344">Vous pouvez utiliser InvokeApiAsync toocall tout WebAPI, y compris les WebAPIs qui ne sont pas définis avec les applications mobiles Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9da-344">You can use InvokeApiAsync toocall any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="0f9da-345">Lorsque vous utilisez InvokeApiAsync(), en-têtes appropriés hello, y compris les en-têtes d’authentification sont envoyés avec la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-345">When you use InvokeApiAsync(), hello appropriate headers, including authentication headers, are sent with hello request.</span></span>

## <span data-ttu-id="0f9da-346"><a name="authentication"></a>Authentification des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="0f9da-346"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="0f9da-347">Mobile Apps prend en charge l’authentification et l’autorisation des utilisateurs d’applications via divers fournisseurs d’identité externes : Facebook, Google, Microsoft Account, Twitter et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0f9da-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="0f9da-348">Vous pouvez définir des autorisations sur l’accès aux toorestrict de tables pour des opérations spécifiques aux utilisateurs de tooonly authentifié.</span><span class="sxs-lookup"><span data-stu-id="0f9da-348">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="0f9da-349">Vous pouvez également utiliser l’identité hello des règles d’autorisation de tooimplement utilisateurs authentifiés dans les scripts de serveur.</span><span class="sxs-lookup"><span data-stu-id="0f9da-349">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="0f9da-350">Pour plus d’informations, consultez le didacticiel de hello [ajouter l’authentification tooyour application].</span><span class="sxs-lookup"><span data-stu-id="0f9da-350">For more information, see hello tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="0f9da-351">Deux flux d’authentification sont pris en charge : le flux *géré par le client* et le flux *géré par le serveur*.</span><span class="sxs-lookup"><span data-stu-id="0f9da-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="0f9da-352">Hello géré par le serveur fournit expérience d’authentification la plus simple hello, car il repose sur l’interface d’authentification web du fournisseur hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-352">hello server-managed flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="0f9da-353">flux de Hello client géré permet une intégration plus étroite avec des fonctionnalités spécifiques à l’appareil comme il s’appuie sur les kits de développement logiciel spécifique au fournisseur spécifique à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="0f9da-353">hello client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="0f9da-354">Nous vous recommandons d’utiliser un flux géré par le client dans vos applications de production.</span><span class="sxs-lookup"><span data-stu-id="0f9da-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="0f9da-355">tooset l’authentification, vous devez inscrire votre application avec un ou plusieurs fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="0f9da-355">tooset up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="0f9da-356">fournisseur d’identité Hello génère un ID client et une clé secrète du client pour votre application.</span><span class="sxs-lookup"><span data-stu-id="0f9da-356">hello identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="0f9da-357">Ces valeurs sont ensuite définies dans votre tooenable de principal du Service d’applications Azure d’authentification ou d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="0f9da-357">These values are then set in your backend tooenable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="0f9da-358">Pour plus d’informations, suivez hello des instructions détaillées dans le didacticiel [ajouter l’authentification tooyour application].</span><span class="sxs-lookup"><span data-stu-id="0f9da-358">For more information, follow hello detailed instructions in the tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="0f9da-359">Hello rubriques suivantes est traitée dans cette section :</span><span class="sxs-lookup"><span data-stu-id="0f9da-359">hello following topics are covered in this section:</span></span>

* [<span data-ttu-id="0f9da-360">Authentification gérée par le client</span><span class="sxs-lookup"><span data-stu-id="0f9da-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="0f9da-361">Authentification gérée par le serveur</span><span class="sxs-lookup"><span data-stu-id="0f9da-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="0f9da-362">Jeton d’authentification hello mise en cache</span><span class="sxs-lookup"><span data-stu-id="0f9da-362">Caching hello authentication token</span></span>](#caching)

### <span data-ttu-id="0f9da-363"><a name="clientflow"></a>Authentification gérée par le client</span><span class="sxs-lookup"><span data-stu-id="0f9da-363"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="0f9da-364">Votre application peut indépendamment contactez le fournisseur d’identité hello et fournissez jeton retourné de hello lors de la connexion avec votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="0f9da-364">Your app can independently contact hello identity provider and then provide hello returned token during login with your backend.</span></span> <span data-ttu-id="0f9da-365">Ce flux du client vous permet de tooprovide une expérience d’authentification unique pour les utilisateurs ou les données d’utilisateur supplémentaires tooretrieve hello fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="0f9da-365">This client flow enables you tooprovide a single sign-on experience for users or tooretrieve additional user data from hello identity provider.</span></span> <span data-ttu-id="0f9da-366">L’authentification du client flux est préféré toousing un flux de serveur comme fournisseur d’identité hello SDK fournit un aspect d’expérience utilisateur plus natif et permet la personnalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="0f9da-366">Client flow authentication is preferred toousing a server flow as hello identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="0f9da-367">Exemples sont fournis pour hello suivant des modèles de flux du client d’authentification :</span><span class="sxs-lookup"><span data-stu-id="0f9da-367">Examples are provided for hello following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="0f9da-368">Bibliothèque d’authentification Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f9da-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="0f9da-369">Facebook ou Google</span><span class="sxs-lookup"><span data-stu-id="0f9da-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="0f9da-370">Kit de développement logiciel (SDK) Live</span><span class="sxs-lookup"><span data-stu-id="0f9da-370">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="0f9da-371"><a name="adal"></a>Authentifier les utilisateurs avec hello bibliothèque d’authentification Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f9da-371"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="0f9da-372">Vous pouvez utiliser l’authentification utilisateur tooinitiate du hello Active Directory Authentication Library (ADAL) à partir du client de hello à l’aide de l’authentification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0f9da-372">You can use hello Active Directory Authentication Library (ADAL) tooinitiate user authentication from hello client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="0f9da-373">Configurer le service principal de votre application mobile pour l’authentification AAD par hello suivant [comment tooconfigure application de Service pour la connexion Active Directory] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0f9da-373">Configure your mobile app backend for AAD sign-on by following hello [How tooconfigure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="0f9da-374">Assurez-vous qu’étape facultative toocomplete hello d’inscription d’une application cliente native.</span><span class="sxs-lookup"><span data-stu-id="0f9da-374">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="0f9da-375">Dans Visual Studio ou Xamarin Studio, ouvrez votre projet et ajouter une référence toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` package NuGet.</span><span class="sxs-lookup"><span data-stu-id="0f9da-375">In Visual Studio or Xamarin Studio, open your project and add a reference toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="0f9da-376">Au cours de la recherche, incluez les versions préliminaires.</span><span class="sxs-lookup"><span data-stu-id="0f9da-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="0f9da-377">Ajoutez hello après application de code tooyour, selon la plateforme toohello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="0f9da-377">Add hello following code tooyour application, according toohello platform you are using.</span></span> <span data-ttu-id="0f9da-378">Dans chacune, apportez hello suivant remplacements :</span><span class="sxs-lookup"><span data-stu-id="0f9da-378">In each, make hello following replacements:</span></span>

   * <span data-ttu-id="0f9da-379">Remplacez **INSERT-autorité-ici** avec nom hello du client hello dans lequel vous avez configuré votre application.</span><span class="sxs-lookup"><span data-stu-id="0f9da-379">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="0f9da-380">Le format doit être https://login.microsoftonline.com/contoso.onmicrosoft.com. Cette valeur peut être copiée à partir de l’onglet du domaine hello dans Azure Active Directory Bonjour [portail Azure classic].</span><span class="sxs-lookup"><span data-stu-id="0f9da-380">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="0f9da-381">Remplacez **INSERT-RESOURCE-ID-ici** avec l’ID de client hello pour le service principal de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="0f9da-381">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="0f9da-382">Vous pouvez obtenir l’ID de client hello de hello **avancé** onglet sous **paramètres Azure Active Directory** dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-382">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="0f9da-383">Remplacez **INSERT-CLIENT-ID-ici** avec l’ID de client hello copié à partir de l’application cliente native de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-383">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="0f9da-384">Remplacez **INSERT-REDIRECT-URI-ici** avec de votre site */.auth/login/done* point de terminaison, à l’aide du schéma HTTPS de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-384">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="0f9da-385">Cette valeur doit être similaire trop*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="0f9da-385">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="0f9da-386">code Hello nécessaire pour chaque plateforme suivante :</span><span class="sxs-lookup"><span data-stu-id="0f9da-386">hello code needed for each platform follows:</span></span>

     <span data-ttu-id="0f9da-387">**Windows :**</span><span class="sxs-lookup"><span data-stu-id="0f9da-387">**Windows:**</span></span>

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

     <span data-ttu-id="0f9da-388">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="0f9da-388">**Xamarin.iOS**</span></span>

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

     <span data-ttu-id="0f9da-389">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="0f9da-389">**Xamarin.Android**</span></span>

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

#### <span data-ttu-id="0f9da-390"><a name="client-facebook"></a>Authentification unique à l’aide d’un jeton Facebook ou Google</span><span class="sxs-lookup"><span data-stu-id="0f9da-390"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="0f9da-391">Vous pouvez utiliser des flux hello du client comme indiqué dans cet extrait de code pour Facebook ou Google.</span><span class="sxs-lookup"><span data-stu-id="0f9da-391">You can use hello client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
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
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
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

#### <span data-ttu-id="0f9da-392"><a name="client-livesdk"></a>L’authentification unique à l’aide de Microsoft Account hello Live SDK</span><span class="sxs-lookup"><span data-stu-id="0f9da-392"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with hello Live SDK</span></span>
<span data-ttu-id="0f9da-393">les utilisateurs tooauthenticate, vous devez inscrire votre application à hello le compte Microsoft Centre de développement.</span><span class="sxs-lookup"><span data-stu-id="0f9da-393">tooauthenticate users, you must register your app at hello Microsoft account Developer Center.</span></span> <span data-ttu-id="0f9da-394">Configurez les détails de l’inscription sur votre backend Mobile App.</span><span class="sxs-lookup"><span data-stu-id="0f9da-394">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="0f9da-395">toocreate Microsoft d’enregistrement de compte et le connecter principal de l’application Mobile tooyour, hello terminé les étapes [inscrire votre application de toouse une connexion au compte Microsoft].</span><span class="sxs-lookup"><span data-stu-id="0f9da-395">toocreate a Microsoft account registration and connect it tooyour Mobile App backend, complete hello steps in [Register your app toouse a Microsoft account login].</span></span> <span data-ttu-id="0f9da-396">Si vous avez Windows Store et Windows Phone 8/Silverlight les versions de votre application, inscrire tout d’abord version du magasin de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-396">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register hello Windows Store version first.</span></span>

<span data-ttu-id="0f9da-397">Hello code suivant authentifie à l’aide du Kit de développement logiciel Live et utilise hello retourné toosign jeton dans le service principal de l’application Mobile tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f9da-397">hello following code authenticates using Live SDK and uses hello returned token toosign in tooyour Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
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

<span data-ttu-id="0f9da-398">Pour plus d’informations, consultez hello [Windows Live SDK] documentation.</span><span class="sxs-lookup"><span data-stu-id="0f9da-398">For more information, see hello [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="0f9da-399"><a name="serverflow"></a>Authentification gérée par le serveur</span><span class="sxs-lookup"><span data-stu-id="0f9da-399"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="0f9da-400">Une fois que vous avez enregistré votre fournisseur d’identité, appelez hello [LoginAsync] méthode sur hello [MobileServiceClient] avec hello [MobileServiceAuthenticationProvider] la valeur de votre fournisseur.</span><span class="sxs-lookup"><span data-stu-id="0f9da-400">Once you have registered your identity provider, call hello [LoginAsync] method on hello [MobileServiceClient] with hello [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="0f9da-401">Par exemple, hello de code suivant initialise un flux de connexion de serveur à l’aide de Facebook.</span><span class="sxs-lookup"><span data-stu-id="0f9da-401">For example, hello following code initiates a server flow sign-in by using Facebook.</span></span>

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

<span data-ttu-id="0f9da-402">Si vous utilisez un fournisseur d’identité autre que Facebook, modifiez la valeur hello [MobileServiceAuthenticationProvider] valeur toohello pour votre fournisseur.</span><span class="sxs-lookup"><span data-stu-id="0f9da-402">If you are using an identity provider other than Facebook, change hello value of [MobileServiceAuthenticationProvider] toohello value for your provider.</span></span>

<span data-ttu-id="0f9da-403">Dans un flux de serveur, du Service d’applications Azure gère les flux d’authentification OAuth hello en affichant hello-page de connexion du fournisseur sélectionné de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-403">In a server flow, Azure App Service manages hello OAuth authentication flow by displaying hello sign-in page of hello selected provider.</span></span>  <span data-ttu-id="0f9da-404">Une fois retourne de fournisseur hello identité, Azure App Service génère un jeton d’authentification du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="0f9da-404">Once hello identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="0f9da-405">Hello [LoginAsync] méthode retourne un [MobileServiceUser], qui fournit les deux hello [UserId] Hello authentifié l’utilisateur et hello [ MobileServiceAuthenticationToken], comme jeton web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="0f9da-405">hello [LoginAsync] method returns a [MobileServiceUser], which provides both hello [UserId] of hello authenticated user and hello [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="0f9da-406">Ce jeton peut être mis en cache et réutilisé jusqu'à ce qu'il arrive à expiration.</span><span class="sxs-lookup"><span data-stu-id="0f9da-406">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="0f9da-407">Pour plus d’informations, consultez [jeton d’authentification mise en cache hello](#caching).</span><span class="sxs-lookup"><span data-stu-id="0f9da-407">For more information, see [Caching hello authentication token](#caching).</span></span>

### <span data-ttu-id="0f9da-408"><a name="caching"></a>Jeton d’authentification hello mise en cache</span><span class="sxs-lookup"><span data-stu-id="0f9da-408"><a name="caching"></a>Caching hello authentication token</span></span>
<span data-ttu-id="0f9da-409">Dans certains cas, méthode de connexion toohello hello appel peut être évitée après une authentification réussie première hello en stockant le jeton d’authentification hello du fournisseur de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-409">In some cases, hello call toohello login method can be avoided after hello first successful authentication by storing hello authentication token from hello provider.</span></span>  <span data-ttu-id="0f9da-410">Les applications du Windows Store et UWP peuvent utiliser [PasswordVault] toocache l’authentification en cours de jeton après une réussite sign-in, comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f9da-410">Windows Store and UWP apps can use [PasswordVault] toocache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="0f9da-411">Hello identificateur de l’utilisateur est stocké comme hello nom d’utilisateur des informations d’identification hello et jeton de hello est stockée en tant que mot de passe de hello hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-411">hello UserId value is stored as hello UserName of hello credential and hello token is hello stored as hello Password.</span></span> <span data-ttu-id="0f9da-412">Sous naissantes suivantes, vous pouvez vérifier hello **PasswordVault** pour des informations d’identification mises en cache.</span><span class="sxs-lookup"><span data-stu-id="0f9da-412">On subsequent start-ups, you can check hello **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="0f9da-413">Hello exemple suivant utilise les informations d’identification mises en cache lorsqu’ils sont trouvés et sinon tente tooauthenticate à nouveau avec le serveur principal hello :</span><span class="sxs-lookup"><span data-stu-id="0f9da-413">hello following example uses cached credentials when they are found, and otherwise attempts tooauthenticate again with hello backend:</span></span>

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

<span data-ttu-id="0f9da-414">Lorsque vous vous déconnectez un utilisateur, vous devez également supprimer des informations d’identification de hello stockée, comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f9da-414">When you sign out a user, you must also remove hello stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="0f9da-415">Applications Xamarin utilisent hello [Xamarin.Auth] informations d’identification du magasin API toosecurely dans un **compte** objet.</span><span class="sxs-lookup"><span data-stu-id="0f9da-415">Xamarin    apps use hello [Xamarin.Auth] APIs toosecurely store credentials in an **Account** object.</span></span> <span data-ttu-id="0f9da-416">Pour obtenir un exemple d’utilisation de ces API, consultez hello [AuthStore.cs] fichier de code dans hello [photo ContosoMoments partage exemple](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="0f9da-416">For an example of using these APIs, see hello [AuthStore.cs] code file in hello [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="0f9da-417">Lorsque vous utilisez l’authentification de client géré, vous pouvez également mettre en cache jeton d’accès hello obtenu à partir de votre fournisseur tel que Facebook ou Twitter.</span><span class="sxs-lookup"><span data-stu-id="0f9da-417">When you use client-managed authentication, you can also cache hello access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="0f9da-418">Ce jeton peut être fourni toorequest un nouveau jeton d’authentification de serveur principal hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f9da-418">This token can be supplied toorequest a new authentication token from hello backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="0f9da-419"><a name="pushnotifications"></a>Notifications Push</span><span class="sxs-lookup"><span data-stu-id="0f9da-419"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="0f9da-420">Hello rubriques suivantes traitent des Notifications Push :</span><span class="sxs-lookup"><span data-stu-id="0f9da-420">hello following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="0f9da-421">Inscription aux notifications Push</span><span class="sxs-lookup"><span data-stu-id="0f9da-421">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="0f9da-422">Obtention d’un SID de package Windows Store</span><span class="sxs-lookup"><span data-stu-id="0f9da-422">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="0f9da-423">Inscription avec des modèles inter-plateformes</span><span class="sxs-lookup"><span data-stu-id="0f9da-423">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="0f9da-424"><a name="register-for-push"></a>Procédure : inscription aux notifications Push</span><span class="sxs-lookup"><span data-stu-id="0f9da-424"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="0f9da-425">client des applications mobiles Hello vous permet de tooregister pour les notifications push avec Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="0f9da-425">hello Mobile Apps client enables you tooregister for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="0f9da-426">Lors de l’inscription, vous obtenez d’un handle que vous obtenez à partir de hello spécifique à la plateforme du Service de Notification Push (PNS).</span><span class="sxs-lookup"><span data-stu-id="0f9da-426">When registering, you obtain a handle that you obtain from hello platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="0f9da-427">Ensuite, vous fournissez cette valeur, ainsi que toutes les balises lorsque vous créez l’enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-427">You then provide this value along with any tags when you create hello registration.</span></span> <span data-ttu-id="0f9da-428">Hello de code suivant inscrit votre application Windows pour les notifications push avec hello Service de Notification de Windows (WNS) :</span><span class="sxs-lookup"><span data-stu-id="0f9da-428">hello following code registers your Windows app for push notifications with hello Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="0f9da-429">Si vous transmettez tooWNS, vous devez [obtenir un SID de package du Windows Store](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="0f9da-429">If you are pushing tooWNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="0f9da-430">Pour plus d’informations sur les applications Windows, y compris comment tooregister des enregistrements dans le modèle, consultez [ajouter push notifications tooyour application].</span><span class="sxs-lookup"><span data-stu-id="0f9da-430">For more information on Windows apps, including how tooregister for template registrations, see [Add push notifications tooyour app].</span></span>

<span data-ttu-id="0f9da-431">Demander des balises à partir de clients de hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0f9da-431">Requesting tags from hello client is not supported.</span></span>  <span data-ttu-id="0f9da-432">Les requêtes de balises sont supprimées de manière silencieuse à partir de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="0f9da-432">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="0f9da-433">Si vous le souhaitez tooregister votre appareil avec balises, créez une API personnalisée qui utilise l’enregistrement de hello API de concentrateurs de Notification tooperform hello en votre nom.</span><span class="sxs-lookup"><span data-stu-id="0f9da-433">If you wish tooregister your device with tags, create a Custom API that uses hello Notification Hubs API tooperform hello registration on your behalf.</span></span>  <span data-ttu-id="0f9da-434">[Appelez hello personnalisé API](#customapi) au lieu de hello `RegisterNativeAsync()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="0f9da-434">[Call hello Custom API](#customapi) instead of hello `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="0f9da-435"><a name="package-sid"></a>Obtention d'un SID de package Windows Store</span><span class="sxs-lookup"><span data-stu-id="0f9da-435"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="0f9da-436">Un SID de package est nécessaire pour l’activation des notifications Push dans les applications Windows Store.</span><span class="sxs-lookup"><span data-stu-id="0f9da-436">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="0f9da-437">tooreceive un package SID, inscrivez votre application avec hello du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="0f9da-437">tooreceive a package SID, register your application with hello Windows Store.</span></span>

<span data-ttu-id="0f9da-438">tooobtain cette valeur :</span><span class="sxs-lookup"><span data-stu-id="0f9da-438">tooobtain this value:</span></span>

1. <span data-ttu-id="0f9da-439">Dans l’Explorateur de solutions Visual Studio, projet d’application hello du Windows Store avec le bouton droit, cliquez sur **magasin** > **associer application hello Store...** .</span><span class="sxs-lookup"><span data-stu-id="0f9da-439">In Visual Studio Solution Explorer, right-click hello Windows Store app project, click **Store** > **Associate App with hello Store...**.</span></span>
2. <span data-ttu-id="0f9da-440">Dans l’Assistant de hello, cliquez sur **suivant**, connectez-vous avec votre compte Microsoft, tapez un nom pour votre application dans **réserver un nouveau nom de l’application**, puis cliquez sur **réserve**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-440">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="0f9da-441">Une fois l’inscription d’une application hello est le nom de l’application a été créé correctement, sélectionnez hello, cliquez sur **suivant**, puis cliquez sur **associer**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-441">After hello app registration is successfully created, select hello app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="0f9da-442">Connectez-vous à toohello [centre de développement Windows] à l’aide de votre Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0f9da-442">Log in toohello [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="0f9da-443">Sous **mes applications**, cliquez sur inscription d’une application hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="0f9da-443">Under **My apps**, click hello app registration you created.</span></span>
5. <span data-ttu-id="0f9da-444">Cliquez sur **gestion des applications** > **identité de l’application**, puis faites défiler vers le bas toofind votre **SID du Package**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-444">Click **App management** > **App identity**, and then scroll down toofind your **Package SID**.</span></span>

<span data-ttu-id="0f9da-445">Nombre d’utilisations de SID du package hello traitent comme un URI, auquel cas vous devez toouse *ms-app : / /* en tant que schéma de hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-445">Many uses of hello package SID treat it as a URI, in which case you need toouse *ms-app://* as hello scheme.</span></span> <span data-ttu-id="0f9da-446">Prenez note de la version de hello de votre package SID formé en concaténant cette valeur en tant que préfixe.</span><span class="sxs-lookup"><span data-stu-id="0f9da-446">Make note of hello version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="0f9da-447">Applications Xamarin nécessitent certains tooregister en mesure de code supplémentaire toobe une application en cours d’exécution sur les plateformes hello iOS ou Android.</span><span class="sxs-lookup"><span data-stu-id="0f9da-447">Xamarin apps require some additional code toobe able tooregister an app running on hello iOS or Android platforms.</span></span> <span data-ttu-id="0f9da-448">Pour plus d’informations, consultez la rubrique hello pour votre plateforme :</span><span class="sxs-lookup"><span data-stu-id="0f9da-448">For more information, see hello topic for your platform:</span></span>

* [<span data-ttu-id="0f9da-449">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="0f9da-449">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="0f9da-450">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="0f9da-450">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="0f9da-451"><a name="register-xplat"></a>Comment : notifications de Registre push modèles toosend inter-plateformes</span><span class="sxs-lookup"><span data-stu-id="0f9da-451"><a name="register-xplat"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="0f9da-452">modèles de tooregister, utilisez hello `RegisterAsync()` méthode avec des modèles de hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f9da-452">tooregister templates, use hello `RegisterAsync()` method with hello templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="0f9da-453">Vos modèles doivent être `JObject` types et peut contenir plusieurs modèles Bonjour suivant le format JSON :</span><span class="sxs-lookup"><span data-stu-id="0f9da-453">Your templates should be `JObject` types and can contain multiple templates in hello following JSON format:</span></span>

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

<span data-ttu-id="0f9da-454">Hello méthode **RegisterAsync()** accepte également des vignettes secondaire :</span><span class="sxs-lookup"><span data-stu-id="0f9da-454">hello method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="0f9da-455">Toutes les balises sont supprimées lors de l’inscription pour la sécurité.</span><span class="sxs-lookup"><span data-stu-id="0f9da-455">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="0f9da-456">tooadd balises tooinstallations ou modèles dans les installations, consultez [utiliser hello .NET back-end server SDK pour les applications mobiles Azure].</span><span class="sxs-lookup"><span data-stu-id="0f9da-456">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="0f9da-457">notifications toosend utilisant ces modèles enregistrés, consultez toohello [API de concentrateurs de Notification].</span><span class="sxs-lookup"><span data-stu-id="0f9da-457">toosend notifications utilizing these registered templates, refer toohello [Notification Hubs APIs].</span></span>

## <span data-ttu-id="0f9da-458"><a name="misc"></a>Rubriques diverses</span><span class="sxs-lookup"><span data-stu-id="0f9da-458"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="0f9da-459"><a name="errors"></a>Procédure : gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="0f9da-459"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="0f9da-460">Lorsqu’une erreur se produit dans le back-end hello, client de hello SDK déclenche un `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="0f9da-460">When an error occurs in hello backend, hello client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="0f9da-461">L’exemple suivant montre comment toohandle une exception qui est retournée par hello principal :</span><span class="sxs-lookup"><span data-stu-id="0f9da-461">The following example shows how toohandle an exception that is returned by hello backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
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

<span data-ttu-id="0f9da-462">Vous trouverez un autre exemple de traitement des conditions d’erreur Bonjour [Mobile Apps fichiers exemple].</span><span class="sxs-lookup"><span data-stu-id="0f9da-462">Another example of dealing with error conditions can be found in hello [Mobile Apps Files Sample].</span></span> <span data-ttu-id="0f9da-463">Le [LoggingHandler] exemple fournit un délégué de journalisation Gestionnaire toolog hello demandes toohello principal.</span><span class="sxs-lookup"><span data-stu-id="0f9da-463">The [LoggingHandler] example provides a logging delegate handler toolog hello requests being made toohello backend.</span></span>

### <span data-ttu-id="0f9da-464"><a name="headers"></a>Procédure de personnalisation des en-têtes de requête</span><span class="sxs-lookup"><span data-stu-id="0f9da-464"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="0f9da-465">toosupport votre scénario d’application spécifique, vous devrez peut-être toocustomize des communications avec le serveur principal de l’application Mobile hello.</span><span class="sxs-lookup"><span data-stu-id="0f9da-465">toosupport your specific app scenario, you might need toocustomize communication with hello Mobile App backend.</span></span> <span data-ttu-id="0f9da-466">Par exemple, vous pouvez souhaitez tooadd une demande sortante de tooevery en-tête personnalisé ou même modifier les codes d’état de réponse.</span><span class="sxs-lookup"><span data-stu-id="0f9da-466">For example, you may want tooadd a custom header tooevery outgoing request or even change responses status codes.</span></span> <span data-ttu-id="0f9da-467">Vous pouvez utiliser une personnalisée [DelegatingHandler], comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0f9da-467">You can use a custom [DelegatingHandler], as in hello following example:</span></span>

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
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
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

[ajouter l’authentification tooyour application]: app-service-mobile-windows-store-dotnet-get-started-users.md
[synchronisation des données hors connexion dans les applications mobiles Azure]: app-service-mobile-offline-data-sync.md
[ajouter push notifications tooyour application]: app-service-mobile-windows-store-dotnet-get-started-push.md
[inscrire votre application de toouse une connexion au compte Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md
[comment tooconfigure application de Service pour la connexion Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[crée un tableau typé de référence tooan]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[prendre]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[sélectionnez]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[ignorer]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[l'UserId]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[où]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[portail Azure]: https://portal.azure.com/
[portail Azure classic]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[centre de développement Windows]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[API de concentrateurs de Notification]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[Mobile Apps fichiers exemple]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 Documentation]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
