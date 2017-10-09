## <span data-ttu-id="e72ea-101"><a name="create-client"></a>Créer une connexion cliente</span><span class="sxs-lookup"><span data-stu-id="e72ea-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="e72ea-102">Créez une connexion cliente en créant un objet `WindowsAzure.MobileServiceClient` .</span><span class="sxs-lookup"><span data-stu-id="e72ea-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="e72ea-103">Remplacez `appUrl` avec la tooyour URL de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="e72ea-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="e72ea-104"><a name="table-reference"></a>Utilisation des tables</span><span class="sxs-lookup"><span data-stu-id="e72ea-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="e72ea-105">tooaccess ou mise à jour des données, créez une table de serveur principal de référence toohello.</span><span class="sxs-lookup"><span data-stu-id="e72ea-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="e72ea-106">Remplacez `tableName` par nom de hello de votre table</span><span class="sxs-lookup"><span data-stu-id="e72ea-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="e72ea-107">Une fois que vous disposez d’une référence de table, vous pouvez continuer à utiliser votre table :</span><span class="sxs-lookup"><span data-stu-id="e72ea-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="e72ea-108">Interroger une table</span><span class="sxs-lookup"><span data-stu-id="e72ea-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="e72ea-109">Filtrage des données</span><span class="sxs-lookup"><span data-stu-id="e72ea-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="e72ea-110">Pagination des données</span><span class="sxs-lookup"><span data-stu-id="e72ea-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="e72ea-111">Tri des données</span><span class="sxs-lookup"><span data-stu-id="e72ea-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="e72ea-112">Insertion de données</span><span class="sxs-lookup"><span data-stu-id="e72ea-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="e72ea-113">Modification des données</span><span class="sxs-lookup"><span data-stu-id="e72ea-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="e72ea-114">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="e72ea-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="e72ea-115"><a name="querying"></a>Procédure : interrogation d’une référence de table</span><span class="sxs-lookup"><span data-stu-id="e72ea-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="e72ea-116">Une fois que vous avez une référence de table, vous pouvez l’utiliser tooquery des données sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="e72ea-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="e72ea-117">Les requêtes sont effectuées dans un langage de type LINQ.</span><span class="sxs-lookup"><span data-stu-id="e72ea-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="e72ea-118">tooreturn de code de toutes les données à partir de la table hello, hello utilisation suivant :</span><span class="sxs-lookup"><span data-stu-id="e72ea-118">tooreturn all data from hello table, use hello following code:</span></span>

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="e72ea-119">fonction de réussite Hello est appelée avec les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e72ea-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="e72ea-120">N’utilisez pas `for (var i in results)` en cas de réussite hello de fonction qui effectue une itération sur les informations qui sont incluses dans les résultats de hello lorsque autres fonctions de requête (tel que `.includeTotalCount()`) sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="e72ea-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="e72ea-121">Pour plus d’informations sur la syntaxe de requête de hello, consultez hello [documentation de l’objet de requête].</span><span class="sxs-lookup"><span data-stu-id="e72ea-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="e72ea-122"><a name="table-filter"></a>Le filtrage des données sur le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="e72ea-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="e72ea-123">Vous pouvez utiliser un `where` clause sur la référence de table hello :</span><span class="sxs-lookup"><span data-stu-id="e72ea-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="e72ea-124">Vous pouvez également utiliser une fonction qui permet de filtrer l’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="e72ea-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="e72ea-125">Dans ce cas, hello `this` est affectée à la variable objet en cours de toothe filtrée.</span><span class="sxs-lookup"><span data-stu-id="e72ea-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="e72ea-126">Hello suivant de code est un exemple de préalable de toohello équivalentes :</span><span class="sxs-lookup"><span data-stu-id="e72ea-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="e72ea-127"><a name="table-paging"></a>Pagination des données</span><span class="sxs-lookup"><span data-stu-id="e72ea-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="e72ea-128">Utiliser hello `take()` et `skip()` méthodes.</span><span class="sxs-lookup"><span data-stu-id="e72ea-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="e72ea-129">Par exemple, si vous le souhaitez table de hello toosplit en ligne de 100 enregistrements :</span><span class="sxs-lookup"><span data-stu-id="e72ea-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

<span data-ttu-id="e72ea-130">Hello `.includeTotalCount()` méthode est utilisée tooadd un objet de résultats totalCount champ toohello.</span><span class="sxs-lookup"><span data-stu-id="e72ea-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="e72ea-131">Le champ totalCount est rempli avec le nombre total de hello d’enregistrements qui serait retournée si aucune pagination n’est utilisée.</span><span class="sxs-lookup"><span data-stu-id="e72ea-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="e72ea-132">Vous pouvez ensuite utiliser la variable de pages hello et certains tooprovide de boutons de l’interface utilisateur une liste de la page ; Utilisez `loadPage()` pour charger les nouveaux enregistrements de hello pour chaque page.</span><span class="sxs-lookup"><span data-stu-id="e72ea-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="e72ea-133">Implémenter la mise en cache toorecords accès toospeed qui ont déjà été chargés.</span><span class="sxs-lookup"><span data-stu-id="e72ea-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="e72ea-134"><a name="sorting-data"></a>Procédure : renvoi de données triées</span><span class="sxs-lookup"><span data-stu-id="e72ea-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="e72ea-135">Hello d’utilisation `.orderBy()` ou `.orderByDescending()` méthodes de requête :</span><span class="sxs-lookup"><span data-stu-id="e72ea-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="e72ea-136">Pour plus d’informations sur l’objet de requête hello, consultez hello [documentation de l’objet de requête].</span><span class="sxs-lookup"><span data-stu-id="e72ea-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="e72ea-137"><a name="inserting"></a>Procédure : insertion de données</span><span class="sxs-lookup"><span data-stu-id="e72ea-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="e72ea-138">Créer un objet JavaScript avec date appropriée de hello et appelez `table.insert()` asynchrone :</span><span class="sxs-lookup"><span data-stu-id="e72ea-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

<span data-ttu-id="e72ea-139">Sur la réussite de l’insertion, hello inséré élément est renvoyé hello autres champs qui sont requis pour les opérations de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="e72ea-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="e72ea-140">Mettez à jour votre propre cache avec ces informations en vue des mises à jour ultérieures.</span><span class="sxs-lookup"><span data-stu-id="e72ea-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="e72ea-141">Bonjour Azure Mobile Apps Node.js serveur SDK prend en charge le schéma dynamique à des fins de développement.</span><span class="sxs-lookup"><span data-stu-id="e72ea-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="e72ea-142">Le schéma dynamique vous permet de table de toohello tooadd colonnes en les spécifiant dans une opération insert ou update.</span><span class="sxs-lookup"><span data-stu-id="e72ea-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="e72ea-143">Nous vous recommandons de désactiver le schéma dynamique avant le déplacement de tooproduction de votre application.</span><span class="sxs-lookup"><span data-stu-id="e72ea-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="e72ea-144"><a name="modifying"></a>Procédure : modification des données</span><span class="sxs-lookup"><span data-stu-id="e72ea-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="e72ea-145">Similaire toohello `.insert()` (méthode), vous devez créer un objet de la mise à jour et appelez ensuite `.update()`.</span><span class="sxs-lookup"><span data-stu-id="e72ea-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="e72ea-146">Hello objet mise à jour doit contenir des ID de hello de hello enregistrement toobe est mis à jour - hello ID est obtenu lors de la lecture de l’enregistrement de hello ou lors de l’appel `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="e72ea-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <span data-ttu-id="e72ea-147"><a name="deleting"></a>Procédure : suppression de données</span><span class="sxs-lookup"><span data-stu-id="e72ea-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="e72ea-148">toodelete un enregistrement, appel hello `.del()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="e72ea-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="e72ea-149">Transmettez hello ID dans une référence d’objet :</span><span class="sxs-lookup"><span data-stu-id="e72ea-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
