---
title: "Didacticiel ASP.NET MVC pour Azure Cosmos DB : développement d’applications Web | Microsoft Docs"
description: "Une application web MVC à l’aide de la base de données Azure Cosmos de toocreate didacticiel ASP.NET MVC. Vous allez stocker JSON et accéder aux données à partir d’une application todo hébergée sur des sites web Azure - Didacticiel étape par étape ASP NET MVC."
keywords: "didacticiel asp.net mvc, développement d’application web, application web mvc, didacticiel mvc asp net étape par étape"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395809351"></a>Didacticiel ASP.NET MVC : développement d’applications web avec Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

toohighlight comment vous pouvez efficacement tirer parti de base de données Azure Cosmos toostore et interroger des documents JSON, cet article fournit une procédure de bout en bout vous montrant comment toobuild une application de tâches à l’aide de la base de données Azure Cosmos. tâches de Hello sont stockés sous forme de documents JSON dans la base de données Azure Cosmos.

![Capture d’écran de liste de tâches hello application de web MVC créée par ce didacticiel - Didacticiel de ASP NET MVC étape par étape](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

Cette procédure pas à pas vous montre comment toouse hello Azure Cosmos DB service toostore et accéder aux données à partir d’une application de web ASP.NET MVC hébergée sur Azure. Si vous recherchez un didacticiel qui porte uniquement sur la base de données Azure Cosmos, et pas hello composants d’ASP.NET MVC, consultez [générer une application de console Azure Cosmos DB c#](documentdb-get-started.md).

> [!TIP]
> Ce didacticiel suppose que vous disposez d'une expérience préalable de l'utilisation d'ASP.NET MVC et d'Azure Websites. Si vous êtes tooASP.NET nouveau ou hello [outils requis](#_Toc395637760), nous vous recommandons de télécharger le projet exemple complet de hello à partir de [GitHub] [ GitHub] et en suivant les instructions de hello dans Cet exemple. Une fois que vous avez créé, vous pouvez consulter ces informations toogain de l’article sur le code hello dans le contexte de hello du projet de hello.
> 
> 

## <a name="_Toc395637760"></a>Conditions préalables à l’exécution de ce didacticiel de base de données
Avant de suivre les instructions de hello dans cet article, vous devez vous assurer que vous disposez des éléments suivants de hello :

* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 

    OU

    Une installation locale de hello [Azure Cosmos DB émulateur](local-emulator.md).
* [Visual Studio 2017](http://www.visualstudio.com/).  
* Microsoft Azure SDK pour .NET de Visual Studio 2017, disponible via le programme d’installation de Visual Studio de hello.

Toutes les captures d’écran hello dans cet article ont été effectuées à l’aide de Microsoft Visual Studio Community 2017. Si votre système est configuré avec une version différente, il est possible que vos écrans et les options ne correspondront pas entièrement, mais si vous répondez à hello au-dessus de conditions préalables cette solution doit fonctionner.

## <a name="_Toc395637761"></a>Étape 1 : création d’un compte de base de données Azure Cosmos DB
Commençons par créer un compte Azure Cosmos DB. Si vous déjà disposez d’un compte SQL (DocumentDB) pour la base de données Azure Cosmos ou si vous utilisez hello Azure Cosmos DB émulateur pour ce didacticiel, vous pouvez ignorer trop[créer une application ASP.NET MVC](#_Toc395637762).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
Nous étudierons maintenant comment toocreate une application ASP.NET MVC à partir de hello sol à distance. 

## <a name="_Toc395637762"></a>Étape 2 : création d'une application ASP.NET MVC

1. Dans Visual Studio, sur hello **fichier** menu, pointez trop**nouveau**, puis cliquez sur **projet**. Hello **nouveau projet** boîte de dialogue s’affiche.

2. Bonjour **types de projet** volet, développez **modèles**, **Visual C#**, **Web**, puis sélectionnez **Application Web ASP.NET** .

      ![Capture d’écran de boîte de dialogue Nouveau projet hello avec le type de projet d’Application Web ASP.NET hello mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. Bonjour **nom** zone, entrez un nom hello du projet de hello. Ce didacticiel utilise le nom hello « todo ». Si vous choisissez autre chose qu’il toouse, partout où ce didacticiel s’adresse à propos de l’espace de noms hello todo, vous devez tooadjust hello fourni code exemples toouse tout ce que vous avez nommé votre application. 
4. Cliquez sur **Parcourir** toonavigate toohello dossier où vous serez comme projet de hello toocreate, puis cliquez sur **OK**.
   
      Hello **nouvelle Application Web ASP.NET** boîte de dialogue s’affiche.
   
    ![Capture d’écran de la boîte de dialogue nouvelle Application Web ASP.NET hello avec le modèle d’application MVC hello mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. Dans le volet des modèles hello, sélectionnez **MVC**.

6. Cliquez sur **OK** et permettent d’effectuer son travail autour de modèle ASP.NET MVC vide de la structure hello Visual Studio. 

          
7. Une fois que Visual Studio a terminé la création d’application de MVC hello réutilisable, vous avez une application ASP.NET vide que vous pouvez exécuter localement.
   
    Nous ignorons le projet de hello en cours d’exécution localement, car je suis sûr que nous avons hello vu tous les « Hello World » d’ASP.NET application. Attardons-nous droites tooadding base de données Azure Cosmos toothis projet et la création de notre application.

## <a name="_Toc395637767"></a>Étape 3 : Ajouter le projet d’application web MVC Azure Cosmos DB tooyour
Maintenant que nous avons la plupart des mécanismes d’ASP.NET MVC hello dont nous avons besoin pour cette solution, nous allons obtenir toohello véritable but de ce didacticiel, l’ajout d’une application web de base de données Azure Cosmos tooour MVC.

1. Bonjour Azure Cosmos DB .NET SDK est packagée et distribuée comme package NuGet. tooget hello package NuGet dans Visual Studio, utilisez le Gestionnaire de package NuGet hello dans Visual Studio en cliquant sur le projet hello dans **l’Explorateur de solutions** , puis en cliquant sur **gérer les Packages NuGet**.
   
    ![Capture d’écran de hello cliquez sur options pour le projet d’application web hello dans l’Explorateur de solutions, gérer les Packages NuGet mis en surbrillance.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    Hello **gérer les Packages NuGet** boîte de dialogue s’affiche.
2. Bonjour NuGet **Parcourir** , tapez ***Azure DocumentDB***. (nom du package hello n’a été mis à jour tooAzure Cosmos DB.)
   
    À partir des résultats de hello, installez hello **Microsoft.Azure.DocumentDB par Microsoft** package. Il télécharge et installe le package de base de données Azure Cosmos hello, ainsi que toutes les dépendances, telles que Newtonsoft.Json. Cliquez sur **OK** Bonjour **aperçu** fenêtre, et **J’accepte** Bonjour **acceptation de licence** fenêtre toocomplete hello installation.
   
    ![Capture de l ' écran de la fenêtre Gérer les Packages NuGet hello, avec hello bibliothèque cliente Microsoft Azure DocumentDB mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      Vous pouvez également utiliser hello package de Console du Gestionnaire de Package tooinstall hello. toodo sur hello **outils** menu, cliquez sur **Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console**. À l’invite de hello, tapez hello qui suit.
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. Une fois le package de hello est installé, votre solution Visual Studio doit ressembler à suivant hello avec deux nouvelles références ajoutées, Microsoft.Azure.Documents.Client et Newtonsoft.Json.
   
    ![Capture de l ' écran de deux références de hello ajouté toohello projet des données JSON dans l’Explorateur de solutions](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>Étape 4 : Configurer hello application ASP.NET MVC
Maintenant nous allons ajouter application de MVC toothis modèles, vues et contrôleurs des hello :

* [Ajout d'un modèle](#_Toc395637764).
* [Ajout d'un contrôleur](#_Toc395637765).
* [Ajout de vues](#_Toc395637766).

### <a name="_Toc395637764"></a>Ajout d’un modèle de données JSON
Commençons par créer hello **M** dans MVC, hello modèle. 

1. Dans **l’Explorateur de solutions**, avec le bouton hello **modèles** dossier, cliquez sur **ajouter**, puis cliquez sur **classe**.
   
      Hello **ajouter un nouvel élément** boîte de dialogue s’affiche.
2. Nommez votre nouvelle classe **Item.cs**, puis cliquez sur **Ajouter**. 
3. Dans cette nouvelle **Item.cs** , ajoutez suivant hello après hello dernière *à l’aide d’instruction*.
   
        using Newtonsoft.Json;
4. Remplacez maintenant ce code 
   
        public class Item
        {
        }
   
    avec hello suivant de code.
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    Toutes les données dans la base de données Azure Cosmos est transmise sur le câble de hello et stockés au format JSON. moyen de hello toocontrol vos objets sont sérialisés/désérialisé par JSON.NET, vous pouvez utiliser hello **JsonProperty** attribut comme Bonjour **élément** classe que nous venons de créer. Vous n’avez pas **ont** toodo cela mais souhaitez tooensure que mes propriétés suivent camelCase JSON hello conventions d’affectation de noms. 
   
    Non seulement pourrez vous contrôler hello format du nom de la propriété hello lorsqu’il passe en JSON, mais vous pouvez entièrement renommer vos propriétés .NET comme je l’ai fait avec hello **Description** propriété. 

### <a name="_Toc395637765"></a>Ajout d'un contrôleur
Qui prend en charge hello **M**, maintenant nous allons créer hello **C** dans MVC, une classe de contrôleur.

1. Dans **l’Explorateur de solutions**, avec le bouton hello **contrôleurs** dossier, cliquez sur **ajouter**, puis cliquez sur **contrôleur**.
   
    Hello **ajouter une vue de structure** boîte de dialogue s’affiche.
2. Sélectionnez **Classe de contrôleur MVC 5 - Vide** puis cliquez sur **Ajouter**.
   
    ![Capture d’écran de la boîte de dialogue Ajouter une vue de structure hello hello contrôleur MVC 5 - option vide mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. Nommez votre contrôleur **ItemController**
   
    ![Capture d’écran de la boîte de dialogue Ajouter un contrôleur hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    Une fois que le fichier de hello est créé, votre solution Visual Studio doit se présenter comme suit de hello avec le nouveau fichier de ItemController.cs hello dans **l’Explorateur de solutions**. nouveau fichier Item.cs Hello, créé précédemment est également affiché.
   
    ![Capture d’écran de hello solution Visual Studio - Explorateur de solutions avec le nouveau fichier de ItemController.cs hello et fichier Item.cs mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    Vous pouvez fermer ItemController.cs, nous y reviendrons tooit plus tard. 

### <a name="_Toc395637766"></a>Ajout de vues
Maintenant, nous allons créer hello **V** dans MVC, hello vues :

* [Ajout d'une vue Index de l'élément](#AddItemIndexView).
* [Ajout d'une vue Nouvel élément](#AddNewIndexView).
* [Ajout d'une vue Modifier l'élément](#_Toc395888515).

#### <a name="AddItemIndexView"></a>Ajout d'une vue Index de l'élément
1. Dans **l’Explorateur de solutions**, développez hello **vues** dossier, hello avec le bouton vide **élément** dossier créé par Visual Studio pour vous lorsque vous avez ajouté hello  **ItemController** précédemment, cliquez sur **ajouter**, puis cliquez sur **vue**.
   
    ![Capture d’écran de l’Explorateur de solutions affichant le dossier d’éléments de hello créé par Visual Studio avec des commandes d’ajouter une vue hello mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. Bonjour **ajouter une vue** boîte de dialogue zone, hello suivant :
   
   * Bonjour **nom de la vue** , tapez ***Index***.
   * Bonjour **modèle** boîte, sélectionnez ***liste***.
   * Bonjour **classe de modèle** boîte, sélectionnez ***élément (todo. Modèles)***.
   * Dans la zone de page de disposition hello, tapez ***~/Views/Shared/_Layout.cshtml***.
     
   ![Boîte de dialogue Ajouter une vue de capture d’écran montrant hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. Une fois que vous avez défini toutes ces valeurs, cliquez sur **Ajouter** et laissez Visual Studio créer une vue de modèle. Une fois ceci effectué, il ouvre le fichier cshtml hello qui a été créé. Nous pouvons fermer ce fichier dans Visual Studio comme nous reviendra tooit plus tard.

#### <a name="AddNewIndexView"></a>Ajout d'une vue Nouvel élément
Toohow semblables, nous avons créé un **Index de l’élément** affichage, nous allons maintenant créer une nouvelle vue pour la création de nouveaux **éléments**.

1. Dans **l’Explorateur de solutions**, avec le bouton hello **élément** dossier, cliquez sur **ajouter**, puis cliquez sur **vue**.
2. Bonjour **ajouter une vue** boîte de dialogue zone, hello suivant :
   
   * Bonjour **nom de la vue** , tapez ***créer***.
   * Bonjour **modèle** boîte, sélectionnez ***créer***.
   * Bonjour **classe de modèle** boîte, sélectionnez ***élément (todo. Modèles)***.
   * Dans la zone de page de disposition hello, tapez ***~/Views/Shared/_Layout.cshtml***.
   * Cliquez sur **Add**.
   
#### <a name="_Toc395888515"></a>Ajout d'une vue Modifier l'élément
Enfin, ajoutez une dernière vue pour modifier un **élément** Bonjour même façon qu’avant.

1. Dans **l’Explorateur de solutions**, avec le bouton hello **élément** dossier, cliquez sur **ajouter**, puis cliquez sur **vue**.
2. Bonjour **ajouter une vue** boîte de dialogue zone, hello suivant :
   
   * Bonjour **nom de la vue** , tapez ***modifier***.
   * Bonjour **modèle** boîte, sélectionnez ***modifier***.
   * Bonjour **classe de modèle** boîte, sélectionnez ***élément (todo. Modèles)***.
   * Dans la zone de page de disposition hello, tapez ***~/Views/Shared/_Layout.cshtml***.
   * Cliquez sur **Add**.

Une fois cette opération est effectuée, fermez tous les documents de cshtml de hello dans Visual Studio comme nous retourneront les vues toothese plus tard.

## <a name="_Toc395637769"></a>Étape 5 : liaison d’Azure Cosmos DB
Maintenant que les sélections MVC standard hello sont pris en charge, nous allons activer le code de hello tooadding pour la base de données Azure Cosmos. 

Dans cette section, nous allons ajouter suivante de code toohandle hello :

* [Recensement des éléments non terminés.](#_Toc395637770)
* [Ajout d'éléments](#_Toc395637771).
* [Modification d'éléments](#_Toc395637772).

### <a name="_Toc395637770"></a>Établissement de la liste des éléments incomplets dans votre application web MVC
Hello premier toodo chose ici est d’ajouter une classe qui contient tous les hello logique tooconnect tooand utiliser Azure Cosmos. Pour ce didacticiel nous allons encapsulent toute cette logique dans la classe de référentiel tooa appelé DocumentDBRepository. 

1. Dans **l’Explorateur de solutions**, avec le bouton droit sur le projet de hello, cliquez sur **ajouter**, puis cliquez sur **classe**. Nommez la nouvelle classe de hello **DocumentDBRepository** et cliquez sur **ajouter**.
2. Bonjour nouvellement créé **DocumentDBRepository** et ajouter des éléments suivants de hello *à l’aide d’instructions* ci-dessus hello *espace de noms* déclaration
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    Remplacez maintenant ce code 
   
        public class DocumentDBRepository
        {
        }
   
    avec hello suivant de code.
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. Nous mettons lors de la lecture des valeurs de configuration, ouvrez hello **Web.config** fichier de votre application et ajoutez hello lignes sous hello suivantes `<AppSettings>` section.
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. À présent, mettez à jour de valeurs hello *point de terminaison* et *authKey* à l’aide du Panneau de clés hello Hello portail Azure. Utilisez hello **URI** à partir du Panneau de clés hello en tant que valeur hello du paramètre de point de terminaison hello et utilisez hello **clé primaire**, ou **clé secondaire** à partir du Panneau de clés hello en tant que valeur hello Hello paramètre d’authKey.

    Que se charge de mettre en place des référentiels de base de données Azure Cosmos hello, maintenant nous allons ajouter notre logique d’application.

1. Hello première chose que nous souhaitons toodo en mesure de toobe avec une application de liste todo est toodisplay des éléments incomplets hello.  Copiez et collez hello suivant extrait de code n’importe où dans hello **DocumentDBRepository** classe.
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. Ouvrez hello **ItemController** nous avons ajouté précédemment et ajoutez hello suivant *à l’aide d’instructions* au-dessus de déclaration d’espace de noms hello.
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    Si votre projet n’est pas nommé « todo », vous devez tooupdate à l’aide de « todo. Modèles » ; nom de hello tooreflect de votre projet.
   
    Remplacez maintenant ce code
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    avec hello suivant de code.
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. Ouvrez **Global.asax.cs** et ajoutez hello suivant ligne toohello **Application_Start** (méthode) 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

À ce stade, votre solution doit être en mesure de toobuild sans erreurs.

Si vous avez exécuté application hello maintenant, vous indiquerez toohello **HomeController** et hello **Index** vue de ce contrôleur. Il s’agit par défaut hello pour le projet de modèle MVC hello que nous avons choisi au démarrage de hello, mais nous ne voulons pas qui ! Nous allons modifier hello routage sur cette tooalter d’application MVC ce comportement.

Ouvrez ***application\_Start\RouteConfig.cs*** et recherchez la ligne hello commençant par « valeurs par défaut : » et modifiez-le hello tooresemble suivant.

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

Cela maintenant indique à ASP.NET MVC que si vous n’avez pas spécifié une valeur dans hello URL toocontrol hello le comportement de routage que, au lieu de **accueil**, utilisez **élément** en tant que contrôleur de hello et utilisateur **Index** comme vue de hello.

À présent si vous exécutez application hello, il appelle votre **ItemController** qui appeler dans la classe de référentiel toohello et utiliser hello GetItems méthode tooreturn tous les toohello d’éléments incomplet hello **vues** \\ **Élément**\\**Index** vue. 

Si vous créez et exécutez ce projet maintenant, vous devriez voir ce qui suit :    

![Capture d’écran de l’application web hello todo liste sont créée par ce didacticiel de base de données](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>Ajout d'éléments
Nous allons insérer des éléments dans notre base de données afin que nous quelque chose de plus qu’un toolook de grille vide à.

Vous allez ajouter du code trop Azure Cosmos DBRepository ItemController toopersist hello enregistrement de base de données Azure Cosmos.

1. Ajouter hello suivant de méthode tooyour **DocumentDBRepository** classe.
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   Cette méthode prend un objet passé tooit simplement et l’enregistre dans la base de données Azure Cosmos.
2. Ouvrir le fichier de ItemController.cs hello et ajouter hello suivant extrait de code au sein de la classe hello. Voici comment ASP.NET MVC sait quel toodo pour hello **créer** action. Dans ce cas rendu simplement hello associés vue Create.cshtml créé précédemment.
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    Nous devons maintenant du code plus dans ce contrôleur qui acceptera soumission hello de hello **créer** vue.
3. Ajoutez hello bloc suivant de code toohello classe ItemController.cs qui indique à ASP.NET MVC quel toodo avec une publication de formulaire pour ce contrôleur.
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    Ce code appelle dans toohello DocumentDBRepository et utilise hello CreateItemAsync méthode toopersist hello todo élément toohello base de données. 
   
    **Note de sécurité**: hello **ValidateAntiForgeryToken** attribut est utilisé ici toohelp protéger cette application contre les attaques de falsification de requête. Il est tooit plus que simplement en ajoutant cet attribut, vos vues doivent toowork par ce jeton anti-contrefaçon ainsi. Pour plus d’informations sur le sujet de hello et des exemples de procédure tooimplement cela correctement, consultez [empêcher Cross-Site Request Forgery][Preventing Cross-Site Request Forgery]. Hello de code source fourni sur [GitHub] [ GitHub] comporte une implémentation complète de hello en place.
   
    **Note de sécurité**: nous utilisons également hello **lier** attribut sur toohelp de paramètre de méthode hello protéger contre les attaques de validation excessive. Pour plus d’informations, consultez la rubrique [Opérations CRUD de base dans ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].

Ceci conclut hello code nécessaire tooadd éléments tooour base de données.

### <a name="_Toc395637772"></a>Modification d'éléments
Il existe une dernière chose pour nous toodo, et qui est tooadd hello capacité tooedit **éléments** dans la base de données hello et toomark en tant que terminer. Hello vue pour la modification a déjà été ajoutée toohello projet, donc vous devez simplement tooadd certains de code tooour contrôleur toohello **DocumentDBRepository** classe à nouveau.

1. Ajouter hello suivant toohello **DocumentDBRepository** classe.
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    Hello première de ces méthodes, **GetItem** extrait un élément à partir de la base de données Azure Cosmos passée arrière toohello **ItemController** et ensuite sur toohello **modifier** vue.
   
    Hello seconde des méthodes de hello nous venons d’ajouter remplace hello **Document** dans la base de données Azure Cosmos avec version hello Hello **Document** transmis depuis hello **ItemController**.
2. Ajouter hello suivant toohello **ItemController** classe.
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    Hello première méthode gère hello Http GET qui se produit lorsque hello utilisateur clique sur hello **modifier** lien à partir de hello **Index** vue. Cette méthode extrait un [ **Document** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) à partir de la base de données Azure Cosmos et lui passe toohello **modifier** vue.
   
    Hello **modifier** vue effectuez un toohello Http POST **IndexController**. 
   
    Hello seconde méthode nous avons ajouté des handles en passant hello mis à jour objet tooAzure Cosmos DB toobe rendues persistantes dans la base de données hello.

C’est tout, ce qui est tout ce dont nous avons besoin toorun notre application, la liste incomplète **éléments**, ajouter de nouveaux **éléments**et modifier **éléments**.

## <a name="_Toc395637773"></a>Étape 6 : Exécuter localement l’application hello
application de hello tootest sur votre ordinateur local, procédez comme hello suivant :

1. Dans l’application de hello toobuild Visual Studio en mode débogage, appuyez sur F5. Il doit générer l’application hello et lancer un navigateur avec la page de grille vide hello que nous avons vu avant :
   
    ![Capture d’écran de l’application web hello todo liste sont créée par ce didacticiel de base de données](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. Cliquez sur hello **créer un nouveau** lier et ajouter des valeurs toohello **nom** et **Description** champs. Laissez hello **terminé** case à cocher désactivée sinon hello nouvelle **élément** sera ajoutée dans un état terminé et n’apparaissent pas dans la liste initiale de hello.
   
    ![Capture d’écran de hello créer une vue](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. Cliquez sur **créer** et que vous êtes redirigé toohello arrière **Index** vue et votre **élément** s’affiche dans la liste de hello.
   
    ![Capture d’écran de hello vue d’Index](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    Pensez tooadd libre plus quelques **éléments** tooyour liste des tâches.
    
4. Cliquez sur **modifier** tooan suivant **élément** proviennent de la liste de hello et que vous toohello **modifier** vue dans laquelle vous pouvez mettre à jour n’importe quelle propriété de votre objet, y compris hello  **Terminé** indicateur. Si vous marquez hello **Complete** indicateur et cliquez sur **enregistrer**, hello **élément** est supprimé de la liste de hello des tâches incomplètes.
   
    ![Capture d’écran de hello vue Index avec case hello terminé à](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. Une fois que vous avez testé l’application hello, appuyez sur toostop Ctrl + F5 débogage application hello. Vous êtes prêt toodeploy !

## <a name="_Toc395637774"></a>Étape 7 : Déployer hello application tooAzure du Service d’applications 
Maintenant que vous avez application complète hello fonctionne correctement avec la base de données Azure Cosmos nous allons toodeploy cette tooAzure d’application web du Service d’applications.  

1. est de cette application tous les, vous devez toodo toopublish avec le bouton droit sur le projet hello dans **l’Explorateur de solutions** et cliquez sur **publier**.
   
    ![Capture d’écran de hello option Publier dans l’Explorateur de solutions](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. Bonjour **publier** boîte de dialogue, cliquez sur **Microsoft Azure App Service**, puis sélectionnez **créer un nouveau** toocreate un Service d’application de profil, ou cliquez sur **sélectionner Existant** toouse un profil existant.

    ![Publier une boîte de dialogue dans Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. Si vous possédez un profil Azure App Service existant, entrez votre nom d’abonnement. Hello d’utilisation **vue** filtrer toosort par type de ressource ou le groupe de ressources, puis sélectionnez votre Service d’applications Azure. 
   
    ![Boîte de dialogue App Service dans Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. toocreate un nouveau profil de Service d’applications Azure, cliquez sur **créer un nouveau** Bonjour **publier** boîte de dialogue. Bonjour **créer un Service application** boîte de dialogue, entrez votre nom de l’application Web et un abonnement approprié, un groupe de ressources et un plan App Service, puis cliquez sur **créer**.

    ![Créer une boîte de dialogue App Service dans Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

Dans quelques secondes, Visual Studio achèvera la publication de votre application web et lancera un navigateur dans lequel vous pourrez voir votre réalisation exécutée dans Azure !



## <a name="_Toc395637775"></a>Étapes suivantes
Félicitations ! Vous venez de créé votre premier ASP.NET MVC application web à l’aide de la base de données Azure Cosmos et publié tooAzure. Hello de code source pour l’application hello complète, y compris les détails de hello et supprimer des fonctionnalités qui n’étaient pas incluses dans ce didacticiel peut être téléchargé ou cloné à partir de [GitHub][GitHub]. Par conséquent, si vous souhaitez ajouter à cette application tooyour, saisissez le code de hello et l’ajouter toothis application.

application de tooyour tooadd des fonctionnalités supplémentaires, consultez hello API disponibles dans hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) apparence toocontribute libre toohello Azure Cosmos DB .NET Library sur [GitHub] [GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
