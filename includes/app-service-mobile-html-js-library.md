## <a name="create-client"></a>Créer une connexion cliente
Créez une connexion cliente en créant un objet `WindowsAzure.MobileServiceClient` .  Remplacez `appUrl` avec la tooyour URL de l’application Mobile.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>Utilisation des tables
tooaccess ou mise à jour des données, créez une table de serveur principal de référence toohello. Remplacez `tableName` par nom de hello de votre table

```
var table = client.getTable(tableName);
```

Une fois que vous disposez d’une référence de table, vous pouvez continuer à utiliser votre table :

* [Interroger une table](#querying)
  * [Filtrage des données](#table-filter)
  * [Pagination des données](#table-paging)
  * [Tri des données](#sorting-data)
* [Insertion de données](#inserting)
* [Modification des données](#modifying)
* [Suppression de données](#deleting)

### <a name="querying"></a>Procédure : interrogation d’une référence de table
Une fois que vous avez une référence de table, vous pouvez l’utiliser tooquery des données sur le serveur de hello.  Les requêtes sont effectuées dans un langage de type LINQ.
tooreturn de code de toutes les données à partir de la table hello, hello utilisation suivant :

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

fonction de réussite Hello est appelée avec les résultats hello.  N’utilisez pas `for (var i in results)` en cas de réussite hello de fonction qui effectue une itération sur les informations qui sont incluses dans les résultats de hello lorsque autres fonctions de requête (tel que `.includeTotalCount()`) sont utilisés.

Pour plus d’informations sur la syntaxe de requête de hello, consultez hello [documentation de l’objet de requête].

#### <a name="table-filter"></a>Le filtrage des données sur le serveur de hello
Vous pouvez utiliser un `where` clause sur la référence de table hello :

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

Vous pouvez également utiliser une fonction qui permet de filtrer l’objet de hello.  Dans ce cas, hello `this` est affectée à la variable objet en cours de toothe filtrée.  Hello suivant de code est un exemple de préalable de toohello équivalentes :

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>Pagination des données
Utiliser hello `take()` et `skip()` méthodes.  Par exemple, si vous le souhaitez table de hello toosplit en ligne de 100 enregistrements :

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

Hello `.includeTotalCount()` méthode est utilisée tooadd un objet de résultats totalCount champ toohello.  Le champ totalCount est rempli avec le nombre total de hello d’enregistrements qui serait retournée si aucune pagination n’est utilisée.

Vous pouvez ensuite utiliser la variable de pages hello et certains tooprovide de boutons de l’interface utilisateur une liste de la page ; Utilisez `loadPage()` pour charger les nouveaux enregistrements de hello pour chaque page.  Implémenter la mise en cache toorecords accès toospeed qui ont déjà été chargés.

#### <a name="sorting-data"></a>Procédure : renvoi de données triées
Hello d’utilisation `.orderBy()` ou `.orderByDescending()` méthodes de requête :

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Pour plus d’informations sur l’objet de requête hello, consultez hello [documentation de l’objet de requête].

### <a name="inserting"></a>Procédure : insertion de données
Créer un objet JavaScript avec date appropriée de hello et appelez `table.insert()` asynchrone :

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

Sur la réussite de l’insertion, hello inséré élément est renvoyé hello autres champs qui sont requis pour les opérations de synchronisation.  Mettez à jour votre propre cache avec ces informations en vue des mises à jour ultérieures.

Bonjour Azure Mobile Apps Node.js serveur SDK prend en charge le schéma dynamique à des fins de développement.  Le schéma dynamique vous permet de table de toohello tooadd colonnes en les spécifiant dans une opération insert ou update.  Nous vous recommandons de désactiver le schéma dynamique avant le déplacement de tooproduction de votre application.

### <a name="modifying"></a>Procédure : modification des données
Similaire toohello `.insert()` (méthode), vous devez créer un objet de la mise à jour et appelez ensuite `.update()`.  Hello objet mise à jour doit contenir des ID de hello de hello enregistrement toobe est mis à jour - hello ID est obtenu lors de la lecture de l’enregistrement de hello ou lors de l’appel `.insert()`.

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

### <a name="deleting"></a>Procédure : suppression de données
toodelete un enregistrement, appel hello `.del()` (méthode).  Transmettez hello ID dans une référence d’objet :

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
