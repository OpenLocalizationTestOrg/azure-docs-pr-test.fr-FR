## <span data-ttu-id="fd66c-101"><a name="create-client"></a>Créer une connexion cliente</span><span class="sxs-lookup"><span data-stu-id="fd66c-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="fd66c-102">Créez une connexion cliente en créant un objet `WindowsAzure.MobileServiceClient` .</span><span class="sxs-lookup"><span data-stu-id="fd66c-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="fd66c-103">Remplacez `appUrl` par l’URL de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="fd66c-103">Replace `appUrl` with the URL to your Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="fd66c-104"><a name="table-reference"></a>Utilisation des tables</span><span class="sxs-lookup"><span data-stu-id="fd66c-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="fd66c-105">Pour accéder aux données ou les mettre à jour, créez une référence à la table principale.</span><span class="sxs-lookup"><span data-stu-id="fd66c-105">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="fd66c-106">Remplacez `tableName` par le nom de votre table.</span><span class="sxs-lookup"><span data-stu-id="fd66c-106">Replace `tableName` with the name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="fd66c-107">Une fois que vous disposez d’une référence de table, vous pouvez continuer à utiliser votre table :</span><span class="sxs-lookup"><span data-stu-id="fd66c-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="fd66c-108">Interroger une table</span><span class="sxs-lookup"><span data-stu-id="fd66c-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="fd66c-109">Filtrage des données</span><span class="sxs-lookup"><span data-stu-id="fd66c-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="fd66c-110">Pagination des données</span><span class="sxs-lookup"><span data-stu-id="fd66c-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="fd66c-111">Tri des données</span><span class="sxs-lookup"><span data-stu-id="fd66c-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="fd66c-112">Insertion de données</span><span class="sxs-lookup"><span data-stu-id="fd66c-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="fd66c-113">Modification des données</span><span class="sxs-lookup"><span data-stu-id="fd66c-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="fd66c-114">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="fd66c-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="fd66c-115"><a name="querying"></a>Procédure : interrogation d’une référence de table</span><span class="sxs-lookup"><span data-stu-id="fd66c-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="fd66c-116">Une fois que vous disposez d’une référence de table, vous pouvez l’utiliser pour rechercher des données sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="fd66c-116">Once you have a table reference, you can use it to query for data on the server.</span></span>  <span data-ttu-id="fd66c-117">Les requêtes sont effectuées dans un langage de type LINQ.</span><span class="sxs-lookup"><span data-stu-id="fd66c-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="fd66c-118">Pour retourner toutes les données de la table, utilisez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="fd66c-118">To return all data from the table, use the following code:</span></span>

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="fd66c-119">La fonction success est appelée avec les résultats.</span><span class="sxs-lookup"><span data-stu-id="fd66c-119">The success function is called with the results.</span></span>  <span data-ttu-id="fd66c-120">Ne recourez pas à `for (var i in results)` dans la fonction success, car cette action entraîne une itération sur les informations contenues dans les résultats quand d’autres fonctions de requête (telles que `.includeTotalCount()`) sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="fd66c-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="fd66c-121">Pour plus d’informations sur la syntaxe de requête, consultez la [documentation de l’objet Query].</span><span class="sxs-lookup"><span data-stu-id="fd66c-121">For more information on the Query syntax, see the [Query object documentation].</span></span>

#### <span data-ttu-id="fd66c-122"><a name="table-filter"></a>Filtrage des données sur le serveur</span><span class="sxs-lookup"><span data-stu-id="fd66c-122"><a name="table-filter"></a>Filtering data on the server</span></span>
<span data-ttu-id="fd66c-123">Vous pouvez utiliser une clause `where` sur la référence de table :</span><span class="sxs-lookup"><span data-stu-id="fd66c-123">You can use a `where` clause on the table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="fd66c-124">Vous pouvez également utiliser une fonction qui filtre l’objet.</span><span class="sxs-lookup"><span data-stu-id="fd66c-124">You can also use a function that filters the object.</span></span>  <span data-ttu-id="fd66c-125">Dans ce cas, la variable `this` est affectée à l’objet en cours de filtrage.</span><span class="sxs-lookup"><span data-stu-id="fd66c-125">In this case, the `this` variable is assigned to the current object being filtered.</span></span>  <span data-ttu-id="fd66c-126">Le code suivant est équivalent à l’exemple précédent sur le plan fonctionnel :</span><span class="sxs-lookup"><span data-stu-id="fd66c-126">The following code is functionally equivalent to the prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="fd66c-127"><a name="table-paging"></a>Pagination des données</span><span class="sxs-lookup"><span data-stu-id="fd66c-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="fd66c-128">Utilisez les méthodes `take()` et `skip()`.</span><span class="sxs-lookup"><span data-stu-id="fd66c-128">Utilize the `take()` and `skip()` methods.</span></span>  <span data-ttu-id="fd66c-129">Par exemple, si vous souhaitez fractionner la table en enregistrements de 100 lignes :</span><span class="sxs-lookup"><span data-stu-id="fd66c-129">For example, if you wish to split the table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
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

<span data-ttu-id="fd66c-130">La méthode `.includeTotalCount()` est utilisée pour ajouter un champ totalCount à l’objet results.</span><span class="sxs-lookup"><span data-stu-id="fd66c-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span></span>  <span data-ttu-id="fd66c-131">Le champ totalCount est rempli avec le nombre total d’enregistrements qui est retourné si aucune pagination n’est utilisée.</span><span class="sxs-lookup"><span data-stu-id="fd66c-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="fd66c-132">Vous pouvez ensuite utiliser la variable pages et des boutons d’interface utilisateur pour fournir une liste de pages ; utilisez `loadPage()` pour charger les nouveaux enregistrements pour chaque page.</span><span class="sxs-lookup"><span data-stu-id="fd66c-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span></span>  <span data-ttu-id="fd66c-133">Implémentez la mise en cache pour accélérer l’accès aux enregistrements qui ont déjà été chargés.</span><span class="sxs-lookup"><span data-stu-id="fd66c-133">Implement caching to speed access to records that have already been loaded.</span></span>

#### <span data-ttu-id="fd66c-134"><a name="sorting-data"></a>Procédure : renvoi de données triées</span><span class="sxs-lookup"><span data-stu-id="fd66c-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="fd66c-135">Utilisez les méthodes de requête `.orderBy()` ou `.orderByDescending()` :</span><span class="sxs-lookup"><span data-stu-id="fd66c-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="fd66c-136">Pour plus d’informations sur l’objet Query, consultez la [documentation de l’objet Query].</span><span class="sxs-lookup"><span data-stu-id="fd66c-136">For more information on the Query object, see the [Query object documentation].</span></span>

### <span data-ttu-id="fd66c-137"><a name="inserting"></a>Procédure : insertion de données</span><span class="sxs-lookup"><span data-stu-id="fd66c-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="fd66c-138">Créez un objet JavaScript avec la date appropriée et appelez `table.insert()` de façon asynchrone :</span><span class="sxs-lookup"><span data-stu-id="fd66c-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="fd66c-139">Une fois l’insertion correctement effectuée, l’élément inséré est retourné avec les champs supplémentaires qui sont nécessaires pour les opérations de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="fd66c-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span></span>  <span data-ttu-id="fd66c-140">Mettez à jour votre propre cache avec ces informations en vue des mises à jour ultérieures.</span><span class="sxs-lookup"><span data-stu-id="fd66c-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="fd66c-141">Le Kit de développement logiciel (SDK) de serveur Node.js Azure Mobile Apps prend en charge le schéma dynamique à des fins de développement.</span><span class="sxs-lookup"><span data-stu-id="fd66c-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="fd66c-142">Le schéma dynamique vous permet d’ajouter des colonnes à la table en les spécifiant dans une opération d’insertion ou de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="fd66c-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="fd66c-143">Nous vous recommandons de désactiver le schéma dynamique avant de déplacer votre application vers un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="fd66c-143">We recommend that you turn off dynamic schema before moving your application to production.</span></span>

### <span data-ttu-id="fd66c-144"><a name="modifying"></a>Procédure : modification des données</span><span class="sxs-lookup"><span data-stu-id="fd66c-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="fd66c-145">Comme dans le cas de la méthode `.insert()`, vous devez créer un objet de mise à jour, puis appeler `.update()`.</span><span class="sxs-lookup"><span data-stu-id="fd66c-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="fd66c-146">L’objet de mise à jour doit contenir l’ID de l’enregistrement à mettre à jour, obtenu au moment de la lecture de l’enregistrement ou de l’appel de `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="fd66c-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="fd66c-147"><a name="deleting"></a>Procédure : suppression de données</span><span class="sxs-lookup"><span data-stu-id="fd66c-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="fd66c-148">Pour supprimer un enregistrement, appelez la méthode `.del()`.</span><span class="sxs-lookup"><span data-stu-id="fd66c-148">To delete a record, call the `.del()` method.</span></span>  <span data-ttu-id="fd66c-149">Transmettez l’ID d’une référence d’objet :</span><span class="sxs-lookup"><span data-stu-id="fd66c-149">Pass the ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
