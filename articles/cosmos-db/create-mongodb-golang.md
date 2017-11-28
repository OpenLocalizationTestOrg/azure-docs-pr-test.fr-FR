---
<span data-ttu-id="43fb1-101">titre : aaa « base de données Azure Cosmos : générer une application de console d’API de MongoDB avec Golang et hello portail Azure | Description de Microsoft Docs » : présente un exemple de code Golang que vous pouvez utiliser tooconnect tooand interroger les services Azure Cosmos DB : cosmos-db auteur : Gestionnaire de Durgaprasad-Budhwani : jhubbard éditeur : mimig1</span><span class="sxs-lookup"><span data-stu-id="43fb1-101">title: aaa"Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal | Microsoft Docs" description: Presents a Golang code sample you can use tooconnect tooand query Azure Cosmos DB services: cosmos-db author: Durgaprasad-Budhwani manager: jhubbard editor: mimig1</span></span>

<span data-ttu-id="43fb1-102">MS.service : cosmos-db ms.topic : article héros ms.date : 21/07/2017 ms.author : mimig</span><span class="sxs-lookup"><span data-stu-id="43fb1-102">ms.service: cosmos-db ms.topic: hero-article ms.date: 07/21/2017 ms.author: mimig</span></span>
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a><span data-ttu-id="43fb1-103">Base de données Cosmos Azure : Générer une application de console d’API de MongoDB avec Golang et hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="43fb1-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal</span></span>

<span data-ttu-id="43fb1-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="43fb1-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="43fb1-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="43fb1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="43fb1-106">Ce démarrage rapide montre comment toouse existant [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) application écrite en [Golang](https://golang.org/) et le connecter à base de données de base de données Azure Cosmos tooyour, qui prend en charge les connexions clientes MongoDB.</span><span class="sxs-lookup"><span data-stu-id="43fb1-106">This quick-start demonstrates how toouse an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="43fb1-107">En d’autres termes, votre application Golang sait uniquement qu’il se connecte à l’aide de MongoDB APIs de la base de données tooa.</span><span class="sxs-lookup"><span data-stu-id="43fb1-107">In other words, your Golang application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="43fb1-108">Il est transparent toohello application hello les données est stockée dans la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="43fb1-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43fb1-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="43fb1-109">Prerequisites</span></span>

- <span data-ttu-id="43fb1-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="43fb1-110">An Azure subscription.</span></span> <span data-ttu-id="43fb1-111">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="43fb1-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="43fb1-112">[Accédez](https://golang.org/dl/) et une connaissance élémentaire de hello [accédez](https://golang.org/) language.</span><span class="sxs-lookup"><span data-stu-id="43fb1-112">[Go](https://golang.org/dl/) and a basic knowledge of hello [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="43fb1-113">Un IDE — [Gogland](https://www.jetbrains.com/go/) par Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) par Microsoft, ou [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="43fb1-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="43fb1-114">Dans ce didacticiel, j’utilise Goglang.</span><span class="sxs-lookup"><span data-stu-id="43fb1-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="43fb1-115">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="43fb1-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="43fb1-116">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="43fb1-116">Clone hello sample application</span></span>

<span data-ttu-id="43fb1-117">Cloner l’exemple d’application hello et installer des packages hello requis.</span><span class="sxs-lookup"><span data-stu-id="43fb1-117">Clone hello sample application and install hello required packages.</span></span>

1. <span data-ttu-id="43fb1-118">Créez un dossier nommé CosmosDBSample à l’intérieur du dossier de GOROOT\src hello, qui est C:\Go\ par défaut.</span><span class="sxs-lookup"><span data-stu-id="43fb1-118">Create a folder named CosmosDBSample inside hello GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="43fb1-119">Exécutez hello suivant de commande à l’aide d’une fenêtre de terminal git comme référentiel de git bash tooclone hello exemple dans le dossier de CosmosDBSample hello.</span><span class="sxs-lookup"><span data-stu-id="43fb1-119">Run hello following command using a git terminal window such as git bash tooclone hello sample repository into hello CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="43fb1-120">Exécutez hello suivant package mgo à commande tooget hello.</span><span class="sxs-lookup"><span data-stu-id="43fb1-120">Run hello following command tooget hello mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="43fb1-121">Hello [mgo](http://labix.org/mgo) pilote (prononcé comme *mango*) est un [MongoDB](http://www.mongodb.org/) pilote pour hello [accédez langage](http://golang.org/) qui implémente une riche et des tests sélection de fonctionnalités sous une API simple suivant des idiomes Go standards.</span><span class="sxs-lookup"><span data-stu-id="43fb1-121">hello [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for hello [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="43fb1-122">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="43fb1-122">Update your connection string</span></span>

<span data-ttu-id="43fb1-123">Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="43fb1-123">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="43fb1-124">Cliquez sur **démarrage rapide** dans hello du menu de navigation gauche, puis cliquez sur **autres** informations de chaîne de connexion tooview hello requises par hello Go application.</span><span class="sxs-lookup"><span data-stu-id="43fb1-124">Click **Quick start** in hello left navigation menu, and then click **Other** tooview hello connection string information required by hello Go application.</span></span>

2. <span data-ttu-id="43fb1-125">Dans Goglang, ouvrir le fichier de main.go hello dans le répertoire de GOROOT\CosmosDBSample hello et mettre à jour de hello lignes de code à l’aide des informations de chaîne de connexion de hello de hello portail Azure comme indiqué dans hello suivant capture d’écran suivantes.</span><span class="sxs-lookup"><span data-stu-id="43fb1-125">In Goglang, open hello main.go file in hello GOROOT\CosmosDBSample directory and update hello following lines of code using hello connection string information from hello Azure portal as shown in hello following screenshot.</span></span> 

    <span data-ttu-id="43fb1-126">nom de base de données Hello est le préfixe hello hello **hôte** valeur dans le volet de chaîne de connexion avec le portail Azure hello.</span><span class="sxs-lookup"><span data-stu-id="43fb1-126">hello Database name is hello prefix of hello **Host** value in hello Azure portal connection string pane.</span></span> <span data-ttu-id="43fb1-127">Compte hello illustré hello ci-dessous, le nom de base de données hello est golang-surveiller.</span><span class="sxs-lookup"><span data-stu-id="43fb1-127">For hello account shown in hello image below, hello Database name is golang-coach.</span></span>

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![Démarrage rapide de volet, onglet autre dans les informations de chaîne de connexion hello montrant portail Azure hello](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="43fb1-129">Enregistrez le fichier de main.go hello.</span><span class="sxs-lookup"><span data-stu-id="43fb1-129">Save hello main.go file.</span></span>

## <a name="review-hello-code"></a><span data-ttu-id="43fb1-130">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="43fb1-130">Review hello code</span></span>

<span data-ttu-id="43fb1-131">Nous allons effectuer une révision rapide de ce qui se passe dans le fichier de main.go hello.</span><span class="sxs-lookup"><span data-stu-id="43fb1-131">Let's make a quick review of what's happening in hello main.go file.</span></span> 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a><span data-ttu-id="43fb1-132">Connexion hello Go application tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="43fb1-132">Connecting hello Go app tooAzure Cosmos DB</span></span>

<span data-ttu-id="43fb1-133">Base de données Azure Cosmos prend en charge hello MongoDB de SSL activé.</span><span class="sxs-lookup"><span data-stu-id="43fb1-133">Azure Cosmos DB supports hello SSL-enabled MongoDB.</span></span> <span data-ttu-id="43fb1-134">tooconnect tooan MongoDB de SSL activé, vous devez toodefine hello **DialServer** fonctionner dans [mgo. DialInfo](http://gopkg.in/mgo.v2#DialInfo)et utiliser de hello [tls. *Accès à distance* ](http://golang.org/pkg/crypto/tls#Dial) connexion de hello tooperform de fonction.</span><span class="sxs-lookup"><span data-stu-id="43fb1-134">tooconnect tooan SSL-enabled MongoDB, you need toodefine hello **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of hello [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function tooperform hello connection.</span></span>

<span data-ttu-id="43fb1-135">Hello suivant extrait de code Golang connecte hello Go application avec Azure Cosmos DB MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="43fb1-135">hello following Golang code snippet connects hello Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="43fb1-136">Hello *DialInfo* classe contient des options pour établir une session avec un cluster de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="43fb1-136">hello *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// tooour Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect toomongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes hello session safety mode.
// If hello safe parameter is nil, hello session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. hello unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="43fb1-137">Hello **mgo. Dial()** méthode est utilisée lorsque aucune connexion SSL.</span><span class="sxs-lookup"><span data-stu-id="43fb1-137">hello **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="43fb1-138">Pour une connexion SSL, hello **mgo. DialWithInfo()** méthode est requise.</span><span class="sxs-lookup"><span data-stu-id="43fb1-138">For an SSL connection, hello **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="43fb1-139">Une instance de hello **{} de DialWIthInfo** objet est l’objet de session utilisé toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="43fb1-139">An instance of hello **DialWIthInfo{}** object is used toocreate hello session object.</span></span> <span data-ttu-id="43fb1-140">Une fois la session de hello est établie, vous pouvez accéder collection de hello à l’aide de hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="43fb1-140">Once hello session is established, you can access hello collection by using hello following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="43fb1-141">Créer un document</span><span class="sxs-lookup"><span data-stu-id="43fb1-141">Create a document</span></span>

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a><span data-ttu-id="43fb1-142">Interroger ou lire un document</span><span class="sxs-lookup"><span data-stu-id="43fb1-142">Query or read a document</span></span>

<span data-ttu-id="43fb1-143">Azure Cosmos DB prend en charge les requêtes enrichies sur les documents JSON stockés dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="43fb1-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="43fb1-144">Hello exemple de code suivant montre une requête que vous pouvez exécuter par rapport aux documents de hello dans votre collection.</span><span class="sxs-lookup"><span data-stu-id="43fb1-144">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

```go
// Get a Document from hello collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="43fb1-145">Mettre à jour un document</span><span class="sxs-lookup"><span data-stu-id="43fb1-145">Update a document</span></span>

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a><span data-ttu-id="43fb1-146">Supprimer un document</span><span class="sxs-lookup"><span data-stu-id="43fb1-146">Delete a document</span></span>

<span data-ttu-id="43fb1-147">Azure Cosmos DB prend en charge la suppression des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="43fb1-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a><span data-ttu-id="43fb1-148">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="43fb1-148">Run hello app</span></span>

1. <span data-ttu-id="43fb1-149">Dans Goglang, vérifiez que votre GOPATH (disponible sous **fichier**, **paramètres**, **accédez**, **GOPATH**) incluent l’emplacement de hello dans le hello gopkg a été installé, ce qui est USERPROFILE\go par défaut.</span><span class="sxs-lookup"><span data-stu-id="43fb1-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include hello location in which hello gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="43fb1-150">Commentez les lignes hello supprimer document hello, lignes 91 à 96, afin que vous pouvez voir le document de hello après application de hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="43fb1-150">Comment out hello lines that delete hello document, lines 91-96, so that you can see hello document after running hello app.</span></span>
3. <span data-ttu-id="43fb1-151">Dans Goglang, cliquez sur **Exécuter**, puis cliquez sur **Exécuter "Générer Main.go et exécuter"**.</span><span class="sxs-lookup"><span data-stu-id="43fb1-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="43fb1-152">application Hello se termine et affiche la description de hello du document hello créé dans [créer un document](#create-document).</span><span class="sxs-lookup"><span data-stu-id="43fb1-152">hello app finishes and displays hello description of hello document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Goglang affichant la sortie hello de l’application hello](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="43fb1-154">Réviser votre document dans l’Explorateur de données</span><span class="sxs-lookup"><span data-stu-id="43fb1-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="43fb1-155">Revenir en arrière toohello toosee portail Azure votre document dans l’Explorateur de données.</span><span class="sxs-lookup"><span data-stu-id="43fb1-155">Go back toohello Azure portal toosee your document in Data Explorer.</span></span>

1. <span data-ttu-id="43fb1-156">Cliquez sur **Explorateur de données (version préliminaire)** dans le menu de navigation gauche hello, développez **golang-surveillance**, **package**, puis cliquez sur **Documents**.</span><span class="sxs-lookup"><span data-stu-id="43fb1-156">Click **Data Explorer (Preview)** in hello left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="43fb1-157">Bonjour **Documents** , cliquez sur hello \_document de hello toodisplay id dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="43fb1-157">In hello **Documents** tab, click hello \_id toodisplay hello document in hello right pane.</span></span> 

    ![Document de données Explorer affichant hello qui vient d’être créé](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="43fb1-159">Vous pouvez ensuite manipuler hello document inline et cliquez sur **mise à jour** toosave il.</span><span class="sxs-lookup"><span data-stu-id="43fb1-159">You can then work with hello document inline and click **Update** toosave it.</span></span> <span data-ttu-id="43fb1-160">Vous pouvez également supprimer le document de hello, ou créer de nouveaux documents ou des requêtes.</span><span class="sxs-lookup"><span data-stu-id="43fb1-160">You can also delete hello document, or create new documents or queries.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="43fb1-161">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="43fb1-161">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="43fb1-162">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="43fb1-162">Clean up resources</span></span>

<span data-ttu-id="43fb1-163">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="43fb1-163">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="43fb1-164">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="43fb1-164">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="43fb1-165">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="43fb1-165">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43fb1-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43fb1-166">Next steps</span></span>

<span data-ttu-id="43fb1-167">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos et exécuter une application de Golang à l’aide de hello API pour MongoDB.</span><span class="sxs-lookup"><span data-stu-id="43fb1-167">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a Golang app using hello API for MongoDB.</span></span> <span data-ttu-id="43fb1-168">Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="43fb1-168">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="43fb1-169">Importer des données dans la base de données Azure Cosmos pour hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="43fb1-169">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)
