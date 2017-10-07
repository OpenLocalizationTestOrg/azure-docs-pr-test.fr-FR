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
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a>Comment toouse hello gérées client pour les applications mobiles Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide vous explique comment tooperform des scénarios courants utilisant hello gérées bibliothèque cliente pour les applications Azure App Service Mobile applications pour Windows et Xamarin. Si vous êtes tooMobile de nouvelles applications, vous devez envisager la première hello fin [démarrage rapide des applications mobiles Azure] [ 1] didacticiel. Dans ce guide, nous nous concentrer sur hello côté client géré SDK. toolearn savoir plus sur hello des kits de développement logiciel côté serveur pour les applications mobiles, consultez la documentation de hello pour hello [le Kit de développement .NET Server] [ 2] ou [Node.js serveur SDK] [ 3].

## <a name="reference-documentation"></a>Documentation de référence
Hello documentation de référence pour le client hello SDK se trouve ici : [référence de client Azure Mobile Apps .NET][4].
Vous pouvez également trouver des exemples de plusieurs clients Bonjour [référentiel GitHub d’exemples de Azure][5].

## <a name="supported-platforms"></a>Plateformes prises en charge
Hello plateforme .NET prend en charge hello suivant plates-formes :

* Versions Xamarin Android pour API 19 à 24 (KitKat jusqu’à Nougat)
* Versions Xamarin iOS pour iOS 8.0 et versions ultérieures
* Plateforme Windows universelle
* Windows Phone 8.1
* Windows Phone 8.0, à l’exception des applications Silverlight

l’authentification de « flux de serveur » Hello utilise un WebView hello affiche l’interface utilisateur.  Si l’appareil de hello n’est pas en mesure de toopresent un UI WebView, autres méthodes d’authentification sont nécessaires.  Ce SDK ne convient donc pas au type Watch ou d’autres appareils restreints similaires.

## <a name="setup"></a>Configuration et conditions préalables
Nous supposons que vous avez déjà créé et publié votre projet de backend Mobile Apps et qu'il comprend au moins une table.  Dans le code hello utilisé dans cette rubrique, table de hello est nommée `TodoItem` et qu’il a hello suivant colonnes : `Id`, `Text`, et `Complete`. Cette table est hello même table créé lorsque vous complétez le [démarrage rapide des applications mobiles Azure][1].

Hello typé côté client type correspondant dans c# est hello suivant classe :

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

Hello [JsonPropertyAttribute] [ 6] est utilisé toodefine hello *PropertyName* le mappage entre les champs de client hello et hello table.

toolearn comment toocreate les tables de votre serveur principal Mobile Apps, consultez hello [rubrique du serveur de développement .NET SDK] [ 7] ou hello [rubrique du SDK du serveur Node.js] [ 8] . Si vous avez créé votre serveur principal de l’application Mobile Bonjour Azure à l’aide de portail hello démarrage rapide, vous pouvez également utiliser hello **tables facile** paramètre Bonjour [portail Azure].

### <a name="how-to-install-hello-managed-client-sdk-package"></a>Comment : installer hello managed package SDK de client
Utilisez une des hello suivant hello tooinstall de méthodes managées package SDK de client pour les applications mobiles à partir de [NuGet][9]:

* **Visual Studio** avec le bouton droit de votre projet, cliquez sur **gérer les Packages NuGet**, recherchez hello `Microsoft.Azure.Mobile.Client` du package, puis cliquez sur **installer**.
* **Xamarin Studio** avec le bouton droit de votre projet, cliquez sur **ajouter** > **ajouter des Packages NuGet**, recherchez hello `Microsoft.Azure.Mobile.Client `du package, puis cliquez sur **ajouter Package**.

Dans votre fichier de l’activité principale, n’oubliez pas de suivant de hello tooadd **à l’aide de** instruction :

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a>Instructions : Utilisation des symboles de débogage dans Visual Studio
symboles Hello pour l’espace de noms hello Microsoft.Azure.Mobile sont disponibles sur [SymbolSource][10].  Consultez toothe [SymbolSource instructions] [ 11] toointegrate SymbolSource avec Visual Studio.

## <a name="create-client"></a>Créer le client des applications mobiles hello
Hello de code suivant crée hello [MobileServiceClient] [ 12] objet tooaccess utilisé votre serveur principal de l’application Mobile.

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

Bonjour précédant le code, remplacez `MOBILE_APP_URL` avec hello l’URL du serveur principal de l’application Mobile hello, qui se trouve dans le panneau pour le service principal de votre application Mobile Bonjour [portail Azure]. MobileServiceClient (objet) Hello doit être un singleton.

## <a name="work-with-tables"></a>Utilisation des tables
Hello suivant section détaille comment toosearch et récupérer les enregistrements et modifier des données de hello dans la table de hello.  Hello rubriques suivantes est traitée :

* [Création d'une référence de table](#instantiating)
* [Données de requête](#querying)
* [Filtrer les données renvoyées](#filtering)
* [Trier les données renvoyées](#sorting)
* [Renvoyer les données de pages](#paging)
* [Sélectionner des colonnes spécifiques](#selecting)
* [Rechercher un enregistrement par ID](#lookingup)
* [Traitement des requêtes non typées](#untypedqueries)
* [Insertion de données](#inserting)
* [Mise à jour des données](#updating)
* [Suppression de données](#deleting)
* [Résolution des conflits et accès concurrentiel optimiste](#optimisticconcurrency)
* [Liaison tooa Interface utilisateur Windows](#binding)
* [Hello, taille de la Page de modification](#pagesize)

### <a name="instantiating"></a>Procédure : création d'une référence de table
Tout code hello qui accède ou modifie des données dans une table principale appelle des fonctions sur hello `MobileServiceTable` objet. Obtenir une table de toohello de référence en appelant hello [GetTable] méthode, comme suit :

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

Hello retourné d’objet utilise le modèle de sérialisation typé hello. Les modèles de sérialisation non typés sont également pris en charge. L’exemple suivant [crée un tableau typé de référence tooan]:

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

Dans les requêtes non typés, vous devez spécifier hello sous-jacent de chaîne de requête OData.

### <a name="querying"></a>Interrogation des données à partir de votre application mobile
Cette section décrit comment tooissue interroge le principal de l’application Mobile toohello, qui inclut hello suivant de fonctionnalités :

* [Filtrer les données renvoyées](#filtering)
* [Trier les données renvoyées](#sorting)
* [Renvoyer les données de pages](#paging)
* [Sélectionner des colonnes spécifiques](#selecting)
* [Rechercher des données par ID](#lookingup)

> [!NOTE]
> Une taille de page d’orientée serveur est appliquée tooprevent toutes les lignes soit retourné.  La pagination conserve les requêtes par défaut pour les grands jeux de données à partir d’un effet négatif sur les service hello.  tooreturn plus de 50 lignes, utilisez hello `Skip` et `Take` (méthode), comme décrit dans [retourner des données dans les pages](#paging).

### <a name="filtering"></a>Procédure : filtrage des données renvoyées
Hello de code suivant illustre comment les données toofilter en incluant un `Where` clause dans une requête. Il retourne tous les éléments de `todoTable` dont `Complete` propriété équivaut trop`false`. Hello [où] fonction applique une prédicat de requête de hello sur la table de hello de filtrage de ligne.

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

Vous pouvez afficher hello URI du back-end du toohello hello demande envoyée à l’aide du logiciel de contrôle du message, telles que les outils de développement de navigateur ou [Fiddler]. Si vous examinez l’URI de la demande hello, notez que la chaîne de requête hello est modifié :

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

Cette requête OData est traduite par une requête SQL par hello SDK du serveur :

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

Hello fonction passée toohello `Where` méthode peut avoir un nombre arbitraire de conditions.

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

Cet exemple se traduirait en une requête SQL par hello SDK du serveur :

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

Cette requête peut également être fractionnée en plusieurs clauses :

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

Bonjour, deux méthodes sont équivalentes et peuvent être utilisés indifféremment.  Hello première option&mdash;de la concaténation de plusieurs prédicats dans une requête&mdash;est plus compact et recommandé.

Hello `Where` clause prend en charge les opérations d’être traduit en un sous-ensemble d’OData hello. Les opérations incluent :

* les opérateurs relationnels (==, !=, <, <=, >, >=),
* les opérateurs arithmétiques (+, -, /, *, %),
* la précision des nombres (Math.Floor, Math.Ceiling),
* les fonctions de chaîne (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),
* les propriétés de date (Year, Month, Day, Hour, Minute, Second),
* les propriétés d’accès d’un objet, ainsi que
* les expressions qui combinent toutes ces opérations.

Lorsque le compte tenu que hello serveur SDK prend en charge, vous pouvez envisager hello [OData v3 Documentation].

### <a name="sorting"></a>Procédure : tri des données renvoyées
Hello de code suivant illustre comment les données toosort en incluant un [OrderBy] ou [OrderByDescending] fonction de requête de hello. Elle renvoie les éléments de `todoTable` triée par ordre croissant par hello `Text` champ.

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

### <a name="paging"></a>Procédure : renvoi des données de pages
Par défaut, hello principal retourne hello uniquement les 50 premières lignes. Vous pouvez augmenter le nombre hello de lignes retournées par l’appelant hello [prendre] (méthode). Utilisez `Take` avec hello [ignorer] méthode toorequest une spécifique « page » du jeu de données total hello retournée par la requête de hello. Hello requête suivante, lors de l’exécution, retourne hello trois premiers éléments de tableau de hello.

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

ignore la requête modifiée suivante Hello hello trois premiers résultats et retourne hello trois résultats. Cette requête produit hello deuxième « page » de données, où la taille de la page hello est trois éléments :

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Hello [IncludeTotalCount] méthode demande hello nombre total de *tous les* hello enregistrements qui auraient été retournés, en ignorant toute clause de pagination/limitation spécifiée :

```
query = query.IncludeTotalCount();
```

Dans une application réelle, vous pouvez utiliser toohello similaire de requêtes précédent exemple avec un contrôle pager ou d’une interface utilisateur comparable à naviguer entre les pages.

> [!NOTE]
> limite de 50 lignes toooverride hello dans un service principal de l’application Mobile, vous devez également appliquer hello [EnableQueryAttribute] toohello public GET (méthode) et spécifier le comportement de pagination hello. Lorsque toohello appliqué méthode, hello suivant définit le nombre maximal de lignes retourné too1000 :
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a>Procédure : sélection de colonnes spécifiques
Vous pouvez indiquer quel jeu de propriétés des tooinclude Bonjour génère en ajoutant un [sélectionnez] requête tooyour de clause. Par exemple, hello suivant de code montre comment tooselect à un seul champ et également comment tooselect et mettre en forme plusieurs champs :

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

Tous les hello fonctions décrites jusqu'à présent sont additives, donc nous pouvons conserver liant. Chaque appel chaînée affecte plus de requête de hello. Un exemple supplémentaire :

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a>Procédure : recherche de données par ID
Hello [LookupAsync] fonction peut être utilisé toolook des objets de base de données hello avec un ID particulier.

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a>Exécution de requêtes non typées
Lorsque vous exécutez une requête à l’aide d’un objet de table non typé, vous devez spécifier explicitement de chaîne de requête OData hello en appelant [ReadAsync], comme dans hello l’exemple suivant :

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

Vous obtenez en retour des valeurs JSON que vous pouvez utiliser comme conteneur de propriétés. Pour plus d’informations sur JToken et Newtonsoft Json.NET, consultez hello [Json.NET] site.

### <a name="inserting"></a>Insertion de données dans un backend Mobile Apps
Tous les types clients doivent contenir un membre nommé **Id**, par défaut une chaîne. Cela **Id** est requis pour effectuer des opérations CRUD et de synchronisation hors connexion. Pourquoi suivant de code illustre comment toouse hello [InsertAsync] méthode tooinsert nouvelles lignes dans une table. paramètre Hello contient hello toobe de données insérée en tant qu’objet .NET.

```
await todoTable.InsertAsync(todoItem);
```

Si une valeur d’ID unique personnalisée n’est pas incluse dans hello `todoItem` lors d’une insertion, un GUID est généré par le serveur de hello.
Vous pouvez récupérer hello des Id généré en examinant l’objet de hello après le retour de l’appel de hello.

tooinsert non typées de données, vous pouvez tirer parti de Json.NET :

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

Voici un exemple utilisant une adresse de messagerie comme ID de chaîne unique :

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a>Utilisation de valeurs d'ID
Applications mobiles prend en charge les valeurs de chaîne personnalisé unique pour la table hello **id** colonne. Valeur de chaîne permet aux applications toouse des valeurs personnalisées telles que les adresses de messagerie ou les noms d’utilisateur pour l’ID de hello.  ID de chaîne fournissent hello avantages suivants :

* Un ID est généré sans passer d’une base de données toohello aller-retour.
* Les enregistrements sont toomerge plus facile à partir de différentes tables ou bases de données.
* Les valeurs d’ID peuvent mieux s’intégrer à la logique d’une application.

Lorsqu’une valeur d’ID de chaîne n’est pas définie sur un enregistrement inséré, le principal de l’application Mobile hello génère une valeur unique pour le code. Vous pouvez utiliser hello [Guid.NewGuid] toogenerate méthode votre propre ID de valeurs, soit sur le client de hello hello principal.

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a>Modification de données dans un backend Mobile Apps
Hello de code suivant illustre comment toouse hello [UpdateAsync] méthode tooupdate un enregistrement existant avec hello même ID avec de nouvelles informations. paramètre Hello contient hello toobe de données mis à jour en tant qu’objet .NET.

```
await todoTable.UpdateAsync(todoItem);
```

tooupdate non typées de données, vous pouvez tirer parti de [Json.NET] comme suit :

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

Vous devez spécifier un champ `id` si vous effectuez une mise à jour. Hello principal utilise hello `id` tooidentify de champ qui tooupdate de ligne. Hello `id` champ peut être obtenu à partir du résultat de hello Hello `InsertAsync` appeler. Un `ArgumentException` est générée si vous essayez de tooupdate un élément sans fournir de hello `id` valeur.

### <a name="deleting"></a>Suppression de données dans un backend Mobile Apps
Hello de code suivant illustre comment toouse hello [DeleteAsync] méthode toodelete une instance existante. instance de Hello est identifiée par hello `id` champ ensemble sur hello `todoItem`.

```
await todoTable.DeleteAsync(todoItem);
```

toodelete non typées de données, vous pouvez tirer parti de Json.NET comme suit :

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

Vous devez spécifier un ID lorsque vous effectuez une requête de suppression. Autres propriétés ne sont pas transmises toohello service ou sont ignorées au niveau de service de hello. Hello du résultat d’une `DeleteAsync` appel est généralement `null`. toopass de code Hello dans peut être obtenu à partir du résultat de hello Hello `InsertAsync` appeler. A `MobileServiceInvalidOperationException` est levée lorsque vous essayez de toodelete un élément sans spécifier hello `id` champ.

### <a name="optimisticconcurrency"></a>Procédure : Utilisation de l’accès concurrentiel optimiste pour résoudre les conflits
Deux ou plusieurs clients peuvent écrire les modifications toohello même élément à hello même temps. Sans la détection de conflit, dernière écriture de hello remplace toutes les mises à jour précédentes. **contrôle d'accès concurrentiel optimiste** considère que chaque transaction peut être validée et, qu’à ce titre, elle ne fait appel à aucun verrouillage de ressources.  Avant de valider une transaction, contrôle d’accès concurrentiel optimiste vérifie qu’aucune autre transaction n’a modifié les données de salutation. Si les données de salutation a été modifiées, hello validation de la transaction est restaurée.

Applications mobiles prend en charge le contrôle d’accès concurrentiel optimiste en effectuant le suivi d’élément de tooeach de modifications à l’aide de hello `version` colonne de propriété système qui est défini pour chaque table dans votre service principal de l’application Mobile. Chaque fois un enregistrement est mis à jour, les applications mobiles définit hello `version` propriété pour cet enregistrement tooa nouvelle valeur. Lors de chaque demande de mise à jour, hello `version` propriété d’enregistrement hello inclus avec la demande de hello est toohello comparé même propriété pour l’enregistrement hello sur le serveur de hello. Si la version passée avec la demande de hello ne correspond pas à hello principal, puis déclenche de la bibliothèque cliente de hello un `MobileServicePreconditionFailedException<T>` exception. type Hello inclus avec l’exception de hello est enregistrement hello de hello principal contenant hello serveurs version de l’enregistrement de hello. Hello application peut ensuite utiliser cette toodecide informations si demande de mise à jour tooexecute hello avec hello correct `version` valeur à partir de modifications toocommit hello.

Définir une colonne sur la classe de table hello pour hello `version` système propriété tooenable l’accès concurrentiel optimiste. Par exemple :

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

Applications à l’aide de tables non typés activer l’accès concurrentiel optimiste en définissant un hello `Version` indicateur sur le `SystemProperties` de hello table comme suit.

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

En outre tooenabling d’accès concurrentiel optimiste, vous devez également intercepter hello `MobileServicePreconditionFailedException<T>` exception dans votre code lors de l’appel [UpdateAsync].  Résoudre le conflit de hello en appliquant hello correct `version` toothe mis à jour l’enregistrement et l’appel [UpdateAsync] avec hello résolu l’enregistrement. Hello suivant de code montre comment tooresolve un conflit d’écriture une fois détectée :

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

Pour plus d’informations, consultez hello [synchronisation des données hors connexion dans les applications mobiles Azure] rubrique.

### <a name="binding"></a>Comment : interface utilisateur de liaison Mobile Apps données tooa Windows
Cette section montre comment toodisplay retourné des objets de données à l’aide des éléments d’interface utilisateur dans une application Windows.  L’exemple de code suivant lie la source toohello de liste hello avec une requête pour des éléments incomplets. [MobileServiceCollection] permet de créer une collection de liaisons prenant en charge Mobile Apps.

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

Certains contrôles Bonjour gérés prise en charge du runtime une interface appelée [ISupportIncrementalLoading]. Cette interface permet à des contrôles toorequest des données supplémentaires lorsque hello utilisateur fait défiler. Il existe une prise en charge intégrée pour cette interface pour les applications Windows universelles via [MobileServiceIncrementalLoadingCollection], qui gère automatiquement les appels à partir de contrôles de hello. Utilisez `MobileServiceIncrementalLoadingCollection` dans les applications Windows, comme suit :

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

toouse hello nouveau regroupement sur les applications Windows Phone 8 et « Silverlight », utilisez hello `ToCollection` méthodes d’extension sur `IMobileServiceTableQuery<T>` et `IMobileServiceTable<T>`. les données tooload, appelez `LoadMoreItemsAsync()`.

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

Lorsque vous utilisez collection hello créée en appelant `ToCollectionAsync` ou `ToCollection`, vous obtenez une collection qui peut être liée tooUI contrôles.  Cette collection prend en charge la pagination.  Étant donné que la collection de hello est chargement des données à partir du réseau, le chargement parfois échoue. toohandle ces défaillances, substituez hello `OnException` méthode sur `MobileServiceIncrementalLoadingCollection` toohandle les exceptions résultant des appels trop`LoadMoreItemsAsync`.

Prendre en compte si votre table comporte plusieurs champs, mais que vous voulez uniquement toodisplay certaines d'entre elles dans votre contrôle. Vous pouvez utiliser les conseils hello Bonjour précédant la section «[sélectionner des colonnes spécifiques](#selecting)« toodisplay de colonnes spécifiques tooselect Bonjour l’interface utilisateur.

### <a name="pagesize"></a>Hello de modifier la taille de Page
Par défaut, Azure Mobile Apps retourne au maximum 50 éléments par demande.  Vous pouvez modifier la taille de la pagination hello en augmentant la taille de page maximale hello sur hello client et le serveur.  tooincrease hello la taille de la page demandée, spécifiez `PullOptions` lors de l’utilisation `PullAsync()`:

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

Si vous avez apporté hello `PageSize` tooor égal supérieure à 100 au sein du serveur de hello, une demande renvoie jusqu'à 100 éléments.

## <a name="#offlinesync"></a>Utilisation de tables hors connexion
Des tables hors connexion utilisent un toostore de magasin local SQLite données pour une utilisation en mode hors connexion.  Tableau de toutes les opérations sont effectuées par rapport à hello local SQLite stocker au lieu de la banque du serveur distant hello.  toocreate une table en mode hors connexion, d’abord préparer votre projet :

1. Dans Visual Studio, cliquez sur la solution de hello > **gérer les Packages NuGet pour la Solution...** , puis recherchez et installez le **Microsoft.Azure.Mobile.Client.SQLiteStore** package NuGet pour tous les projets dans la solution de hello.
2. Toosupport (facultatif) les appareils Windows, installez un de hello suivant SQLite runtime packages :

   * **Windows 8.1 Runtime :** installez [SQLite pour Windows 8.1][3].
   * **Windows Phone 8.1 :** installez [SQLite pour Windows Phone 8.1][4].
   * **Plateforme Windows universelle** installer [SQLite pour hello Windows universelles][5].
3. (Facultatif). Pour les appareils Windows, cliquez sur **références** > **ajouter une référence...** , développez hello **Windows** dossier > **Extensions**, puis activer hello approprié **SQLite pour Windows** SDK avec hello  **Visual C++ 2013 Runtime pour Windows** Kit de développement logiciel.
    Hello SQLite SDK noms varient légèrement avec chaque plate-forme Windows.

Avant de pouvoir créer une référence de table, le magasin local de hello doit être préparée :

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

L’initialisation du magasin est normalement effectuée immédiatement après que hello client est créé.  Hello **OfflineDbPath** doit être un nom de fichier pouvant être utilisée sur toutes les plateformes prises en charge.  Si le chemin d’accès hello est un chemin d’accès qualifié complet (autrement dit, il commence par une barre oblique), ce chemin d’accès est utilisé.  Si le chemin d’accès hello n’est pas pleinement qualifié, fichier de hello est placé dans un emplacement spécifique à la plateforme.

* Pour les appareils iOS et Android, chemin d’accès par défaut de hello est hello « personnel » temporaires.
* Pour les appareils Windows, le chemin d’accès de hello par défaut est dossier de « AppData » hello spécifiques à l’application.

Une référence de table peut être obtenue à l’aide de hello `GetSyncTable<>` méthode :

```
var table = client.GetSyncTable<TodoItem>();
```

Vous n’avez pas besoin de tooauthenticate toouse une table en mode hors connexion.  Vous ne devez tooauthenticate lorsque vous communiquez avec le service principal de hello.

### <a name="syncoffline"></a>Synchronisation d’une table hors connexion
Les tables en mode hors connexion ne sont pas synchronisées avec le serveur principal hello par défaut.  La synchronisation est divisée en deux parties.  Vous pouvez transmettre des modifications en dehors du processus de téléchargement de nouveaux éléments.  Voici une méthode de synchronisation typique :

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

Si hello premier argument trop`PullAsync` a la valeur null, puis la synchronisation incrémentielle n’est pas utilisée.  Chaque opération de synchronisation récupère tous les enregistrements.

Hello SDK effectue implicite `PushAsync()` avant l’extraction des enregistrements.

La gestion des conflits s’effectue par le biais d’une méthode `PullAsync()`.  Vous pouvez traiter les conflits Bonjour même manière que les tables en ligne.  conflit de Hello est généré lorsque `PullAsync()` est appelé à la place de lors de hello insert, update ou delete. Si plusieurs conflits se produisent, les opérations sont regroupées dans une seule MobileServicePushFailedException.  Gérez chaque défaillance séparément.

## <a name="#customapi"></a>Utilisation d’une API personnalisée
Une API personnalisée vous permet de toodefine points de terminaison personnalisés qui exposent les fonctionnalités de serveur qui ne pas mapper tooan insérer, mettre à jour, supprimer ou opération de lecture. En utilisant une API personnalisée, vous pouvez exercer davantage de contrôle sur la messagerie, notamment lire et définir des en-têtes de message HTTP et définir un format de corps de message autre que JSON.

Vous appelez une API personnalisée en appelant une de hello [InvokeApiAsync] méthodes sur le client de hello. Par exemple, hello ligne de code suivante envoie un toohello de la demande POST **completeAll** API sur hello principal :

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

Ce formulaire est un appel de méthode typée et requiert que hello **MarkAllResult** retourner le type est défini. Les méthodes typées et non typées sont toutes deux prises en charge.

Hello InvokeApiAsync() méthode ajoute/api/API toohello que vous le souhaitez toocall, sauf si hello API commence par un « / ».
Par exemple :

* `InvokeApiAsync("completeAll",...)`appelle /api/completeAll sur hello principal
* `InvokeApiAsync("/.auth/me",...)`appelle /.auth/me sur hello principal

Vous pouvez utiliser InvokeApiAsync toocall tout WebAPI, y compris les WebAPIs qui ne sont pas définis avec les applications mobiles Azure.  Lorsque vous utilisez InvokeApiAsync(), en-têtes appropriés hello, y compris les en-têtes d’authentification sont envoyés avec la demande de hello.

## <a name="authentication"></a>Authentification des utilisateurs
Mobile Apps prend en charge l’authentification et l’autorisation des utilisateurs d’applications via divers fournisseurs d’identité externes : Facebook, Google, Microsoft Account, Twitter et Azure Active Directory. Vous pouvez définir des autorisations sur l’accès aux toorestrict de tables pour des opérations spécifiques aux utilisateurs de tooonly authentifié. Vous pouvez également utiliser l’identité hello des règles d’autorisation de tooimplement utilisateurs authentifiés dans les scripts de serveur. Pour plus d’informations, consultez le didacticiel de hello [ajouter l’authentification tooyour application].

Deux flux d’authentification sont pris en charge : le flux *géré par le client* et le flux *géré par le serveur*. Hello géré par le serveur fournit expérience d’authentification la plus simple hello, car il repose sur l’interface d’authentification web du fournisseur hello. flux de Hello client géré permet une intégration plus étroite avec des fonctionnalités spécifiques à l’appareil comme il s’appuie sur les kits de développement logiciel spécifique au fournisseur spécifique à l’appareil.

> [!NOTE]
> Nous vous recommandons d’utiliser un flux géré par le client dans vos applications de production.

tooset l’authentification, vous devez inscrire votre application avec un ou plusieurs fournisseurs d’identité.  fournisseur d’identité Hello génère un ID client et une clé secrète du client pour votre application.  Ces valeurs sont ensuite définies dans votre tooenable de principal du Service d’applications Azure d’authentification ou d’autorisation.  Pour plus d’informations, suivez hello des instructions détaillées dans le didacticiel [ajouter l’authentification tooyour application].

Hello rubriques suivantes est traitée dans cette section :

* [Authentification gérée par le client](#clientflow)
* [Authentification gérée par le serveur](#serverflow)
* [Jeton d’authentification hello mise en cache](#caching)

### <a name="clientflow"></a>Authentification gérée par le client
Votre application peut indépendamment contactez le fournisseur d’identité hello et fournissez jeton retourné de hello lors de la connexion avec votre serveur principal. Ce flux du client vous permet de tooprovide une expérience d’authentification unique pour les utilisateurs ou les données d’utilisateur supplémentaires tooretrieve hello fournisseur d’identité. L’authentification du client flux est préféré toousing un flux de serveur comme fournisseur d’identité hello SDK fournit un aspect d’expérience utilisateur plus natif et permet la personnalisation supplémentaire.

Exemples sont fournis pour hello suivant des modèles de flux du client d’authentification :

* [Bibliothèque d’authentification Active Directory](#adal)
* [Facebook ou Google](#client-facebook)
* [Kit de développement logiciel (SDK) Live](#client-livesdk)

#### <a name="adal"></a>Authentifier les utilisateurs avec hello bibliothèque d’authentification Active Directory
Vous pouvez utiliser l’authentification utilisateur tooinitiate du hello Active Directory Authentication Library (ADAL) à partir du client de hello à l’aide de l’authentification Azure Active Directory.

1. Configurer le service principal de votre application mobile pour l’authentification AAD par hello suivant [comment tooconfigure application de Service pour la connexion Active Directory] didacticiel. Assurez-vous qu’étape facultative toocomplete hello d’inscription d’une application cliente native.
2. Dans Visual Studio ou Xamarin Studio, ouvrez votre projet et ajouter une référence toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` package NuGet. Au cours de la recherche, incluez les versions préliminaires.
3. Ajoutez hello après application de code tooyour, selon la plateforme toohello que vous utilisez. Dans chacune, apportez hello suivant remplacements :

   * Remplacez **INSERT-autorité-ici** avec nom hello du client hello dans lequel vous avez configuré votre application. Le format doit être https://login.microsoftonline.com/contoso.onmicrosoft.com. Cette valeur peut être copiée à partir de l’onglet du domaine hello dans Azure Active Directory Bonjour [portail Azure classic].
   * Remplacez **INSERT-RESOURCE-ID-ici** avec l’ID de client hello pour le service principal de votre application mobile. Vous pouvez obtenir l’ID de client hello de hello **avancé** onglet sous **paramètres Azure Active Directory** dans le portail de hello.
   * Remplacez **INSERT-CLIENT-ID-ici** avec l’ID de client hello copié à partir de l’application cliente native de hello.
   * Remplacez **INSERT-REDIRECT-URI-ici** avec de votre site */.auth/login/done* point de terminaison, à l’aide du schéma HTTPS de hello. Cette valeur doit être similaire trop*https://contoso.azurewebsites.net/.auth/login/done*.

     code Hello nécessaire pour chaque plateforme suivante :

     **Windows :**

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

     **Xamarin.iOS**

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

     **Xamarin.Android**

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

#### <a name="client-facebook"></a>Authentification unique à l’aide d’un jeton Facebook ou Google
Vous pouvez utiliser des flux hello du client comme indiqué dans cet extrait de code pour Facebook ou Google.

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

#### <a name="client-livesdk"></a>L’authentification unique à l’aide de Microsoft Account hello Live SDK
les utilisateurs tooauthenticate, vous devez inscrire votre application à hello le compte Microsoft Centre de développement. Configurez les détails de l’inscription sur votre backend Mobile App. toocreate Microsoft d’enregistrement de compte et le connecter principal de l’application Mobile tooyour, hello terminé les étapes [inscrire votre application de toouse une connexion au compte Microsoft]. Si vous avez Windows Store et Windows Phone 8/Silverlight les versions de votre application, inscrire tout d’abord version du magasin de Windows hello.

Hello code suivant authentifie à l’aide du Kit de développement logiciel Live et utilise hello retourné toosign jeton dans le service principal de l’application Mobile tooyour.

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

Pour plus d’informations, consultez hello [Windows Live SDK] documentation.

### <a name="serverflow"></a>Authentification gérée par le serveur
Une fois que vous avez enregistré votre fournisseur d’identité, appelez hello [LoginAsync] méthode sur hello [MobileServiceClient] avec hello [MobileServiceAuthenticationProvider] la valeur de votre fournisseur. Par exemple, hello de code suivant initialise un flux de connexion de serveur à l’aide de Facebook.

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

Si vous utilisez un fournisseur d’identité autre que Facebook, modifiez la valeur hello [MobileServiceAuthenticationProvider] valeur toohello pour votre fournisseur.

Dans un flux de serveur, du Service d’applications Azure gère les flux d’authentification OAuth hello en affichant hello-page de connexion du fournisseur sélectionné de hello.  Une fois retourne de fournisseur hello identité, Azure App Service génère un jeton d’authentification du Service d’applications. Hello [LoginAsync] méthode retourne un [MobileServiceUser], qui fournit les deux hello [UserId] Hello authentifié l’utilisateur et hello [ MobileServiceAuthenticationToken], comme jeton web JSON (JWT). Ce jeton peut être mis en cache et réutilisé jusqu'à ce qu'il arrive à expiration. Pour plus d’informations, consultez [jeton d’authentification mise en cache hello](#caching).

### <a name="caching"></a>Jeton d’authentification hello mise en cache
Dans certains cas, méthode de connexion toohello hello appel peut être évitée après une authentification réussie première hello en stockant le jeton d’authentification hello du fournisseur de hello.  Les applications du Windows Store et UWP peuvent utiliser [PasswordVault] toocache l’authentification en cours de jeton après une réussite sign-in, comme suit :

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

Hello identificateur de l’utilisateur est stocké comme hello nom d’utilisateur des informations d’identification hello et jeton de hello est stockée en tant que mot de passe de hello hello. Sous naissantes suivantes, vous pouvez vérifier hello **PasswordVault** pour des informations d’identification mises en cache. Hello exemple suivant utilise les informations d’identification mises en cache lorsqu’ils sont trouvés et sinon tente tooauthenticate à nouveau avec le serveur principal hello :

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

Lorsque vous vous déconnectez un utilisateur, vous devez également supprimer des informations d’identification de hello stockée, comme suit :

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

Applications Xamarin utilisent hello [Xamarin.Auth] informations d’identification du magasin API toosecurely dans un **compte** objet. Pour obtenir un exemple d’utilisation de ces API, consultez hello [AuthStore.cs] fichier de code dans hello [photo ContosoMoments partage exemple](https://github.com/azure-appservice-samples/ContosoMoments).

Lorsque vous utilisez l’authentification de client géré, vous pouvez également mettre en cache jeton d’accès hello obtenu à partir de votre fournisseur tel que Facebook ou Twitter. Ce jeton peut être fourni toorequest un nouveau jeton d’authentification de serveur principal hello, comme suit :

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a>Notifications Push
Hello rubriques suivantes traitent des Notifications Push :

* [Inscription aux notifications Push](#register-for-push)
* [Obtention d’un SID de package Windows Store](#package-sid)
* [Inscription avec des modèles inter-plateformes](#register-xplat)

### <a name="register-for-push"></a>Procédure : inscription aux notifications Push
client des applications mobiles Hello vous permet de tooregister pour les notifications push avec Azure Notification Hubs. Lors de l’inscription, vous obtenez d’un handle que vous obtenez à partir de hello spécifique à la plateforme du Service de Notification Push (PNS). Ensuite, vous fournissez cette valeur, ainsi que toutes les balises lorsque vous créez l’enregistrement de hello. Hello de code suivant inscrit votre application Windows pour les notifications push avec hello Service de Notification de Windows (WNS) :

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

Si vous transmettez tooWNS, vous devez [obtenir un SID de package du Windows Store](#package-sid).  Pour plus d’informations sur les applications Windows, y compris comment tooregister des enregistrements dans le modèle, consultez [ajouter push notifications tooyour application].

Demander des balises à partir de clients de hello n’est pas pris en charge.  Les requêtes de balises sont supprimées de manière silencieuse à partir de l’inscription.
Si vous le souhaitez tooregister votre appareil avec balises, créez une API personnalisée qui utilise l’enregistrement de hello API de concentrateurs de Notification tooperform hello en votre nom.  [Appelez hello personnalisé API](#customapi) au lieu de hello `RegisterNativeAsync()` (méthode).

### <a name="package-sid"></a>Obtention d'un SID de package Windows Store
Un SID de package est nécessaire pour l’activation des notifications Push dans les applications Windows Store.  tooreceive un package SID, inscrivez votre application avec hello du Windows Store.

tooobtain cette valeur :

1. Dans l’Explorateur de solutions Visual Studio, projet d’application hello du Windows Store avec le bouton droit, cliquez sur **magasin** > **associer application hello Store...** .
2. Dans l’Assistant de hello, cliquez sur **suivant**, connectez-vous avec votre compte Microsoft, tapez un nom pour votre application dans **réserver un nouveau nom de l’application**, puis cliquez sur **réserve**.
3. Une fois l’inscription d’une application hello est le nom de l’application a été créé correctement, sélectionnez hello, cliquez sur **suivant**, puis cliquez sur **associer**.
4. Connectez-vous à toohello [centre de développement Windows] à l’aide de votre Account Microsoft. Sous **mes applications**, cliquez sur inscription d’une application hello vous avez créé.
5. Cliquez sur **gestion des applications** > **identité de l’application**, puis faites défiler vers le bas toofind votre **SID du Package**.

Nombre d’utilisations de SID du package hello traitent comme un URI, auquel cas vous devez toouse *ms-app : / /* en tant que schéma de hello. Prenez note de la version de hello de votre package SID formé en concaténant cette valeur en tant que préfixe.

Applications Xamarin nécessitent certains tooregister en mesure de code supplémentaire toobe une application en cours d’exécution sur les plateformes hello iOS ou Android. Pour plus d’informations, consultez la rubrique hello pour votre plateforme :

* [Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [Xamarin.iOS](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a>Comment : notifications de Registre push modèles toosend inter-plateformes
modèles de tooregister, utilisez hello `RegisterAsync()` méthode avec des modèles de hello, comme suit :

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

Vos modèles doivent être `JObject` types et peut contenir plusieurs modèles Bonjour suivant le format JSON :

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

Hello méthode **RegisterAsync()** accepte également des vignettes secondaire :

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

Toutes les balises sont supprimées lors de l’inscription pour la sécurité. tooadd balises tooinstallations ou modèles dans les installations, consultez [utiliser hello .NET back-end server SDK pour les applications mobiles Azure].

notifications toosend utilisant ces modèles enregistrés, consultez toohello [API de concentrateurs de Notification].

## <a name="misc"></a>Rubriques diverses
### <a name="errors"></a>Procédure : gestion des erreurs
Lorsqu’une erreur se produit dans le back-end hello, client de hello SDK déclenche un `MobileServiceInvalidOperationException`.  L’exemple suivant montre comment toohandle une exception qui est retournée par hello principal :

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

Vous trouverez un autre exemple de traitement des conditions d’erreur Bonjour [Mobile Apps fichiers exemple]. Le [LoggingHandler] exemple fournit un délégué de journalisation Gestionnaire toolog hello demandes toohello principal.

### <a name="headers"></a>Procédure de personnalisation des en-têtes de requête
toosupport votre scénario d’application spécifique, vous devrez peut-être toocustomize des communications avec le serveur principal de l’application Mobile hello. Par exemple, vous pouvez souhaitez tooadd une demande sortante de tooevery en-tête personnalisé ou même modifier les codes d’état de réponse. Vous pouvez utiliser une personnalisée [DelegatingHandler], comme dans hello l’exemple suivant :

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
