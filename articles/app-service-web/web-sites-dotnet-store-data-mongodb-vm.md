---
title: "Création d’une application Web Azure se connectant à MongoDB exécuté sur une machine virtuelle"
description: "Didacticiel qui explique comment utiliser Git pour déployer une application ASP.NET vers Azure App Service, connecté à MongoDB sur une machine virtuelle Azure."
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: a3f289ed9c764d0859573de4f834e042d0f103c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a>Création d’une application Web Azure se connectant à MongoDB exécuté sur une machine virtuelle
Git vous permet de déployer une application ASP.NET sur Azure App Service Web Apps. Ce didacticiel vous apprend à créer une simple application frontale de liste de tâches ASP.NET MVC se connectant à une base de données MongoDB exécutée sur une machine virtuelle dans Azure.  [MongoDB][MongoDB] est une base de données NoSQL open-source qui offre des performances élevées. Après avoir exécuté et testé l’application ASP.NET sur votre ordinateur de développement, vous téléchargerez l’application vers App Service Web Apps à l’aide de Git.

> [!NOTE]
> Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="background-knowledge"></a>Connaissances générales
Dans le cadre de ce didacticiel, la connaissance des éléments suivants est utile, mais pas obligatoire :

* Pilote C# pour MongoDB Pour plus d’informations sur le développement d’applications C# sur MongoDB, reportez-vous au [CSharp Language Center][MongoC#LangCenter] de MongoDB. 
* Infrastructure de développement d'applications Web ASP .NET Pour plus d’informations, consultez le [site web ASP.net][ASP.NET].
* Infrastructure de développement d'applications Web ASP .NET MVC Pour plus d’informations, consultez le [site web ASP.NET MVC][MVCWebSite].
* Azure. Pour commencer, lisez les informations relatives à [Azure][WindowsAzure].

## <a name="prerequisites"></a>Composants requis
* [Visual Studio Express 2013 pour le web][VSEWeb] ou [Visual Studio 2013][VSUlt]
* [Kit de développement logiciel (SDK) Azure pour .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Un abonnement Microsoft Azure actif

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Création d’une machine virtuelle et installation de MongoDB
Ce didacticiel part du principe que vous avez créé une machine virtuelle dans Azure. Une fois la machine virtuelle créée, vous devez y installer MongoDB :

* Pour créer une machine virtuelle Windows et installer MongoDB, consultez la rubrique [Installation de MongoDB sur une machine virtuelle exécutant Windows Server dans Azure][InstallMongoOnWindowsVM].

Après avoir créé la machine virtuelle dans Azure et installé MongoDB, mémorisez le nom DNS de la machine virtuelle (« testlinuxvm.cloudapp.net », par exemple) ainsi que le port externe de MongoDB spécifié dans le point de terminaison.  Ces informations vous seront nécessaires plus loin dans ce didacticiel.

<a id="createapp"></a>

## <a name="create-the-application"></a>Création de l'application
Dans cette section, vous allez créer une application ASP.NET appelée « My Task List » à l’aide de Visual Studio et effectuer un déploiement initial vers Azure App Service Web Apps. Vous exécuterez cette application localement, mais elle se connectera à votre machine virtuelle sur Azure et utilisera l'instance MongoDB que vous y avez créée.

1. Dans Visual Studio, cliquez sur **Nouveau projet**.
   
    ![Page de démarrage Nouveau projet][StartPageNewProject]
2. Dans le volet gauche de la fenêtre **Nouveau projet**, sélectionnez **Visual C#**, puis **Web**. Dans le volet central, sélectionnez **Application Web ASP.NET**. En bas, nommez votre projet « MyTaskListApp », puis cliquez sur **OK**.
   
    ![Boîte de dialogue Nouveau projet][NewProjectMyTaskListApp]
3. Dans la boîte de dialogue **Nouveau projet ASP.NET**, sélectionnez **MVC**, puis cliquez sur **OK**.
   
    ![Sélection du modèle MVC][VS2013SelectMVCTemplate]
4. Si vous n’êtes pas déjà connecté à Microsoft Azure, vous serez invité à vous connecter. Suivez les instructions de l’invite pour vous connecter à Azure.
5. Une fois que vous êtes connecté, vous pouvez commencer à configurer votre application Web App Service. Indiquez le **nom de l’application web**, le **plan App Service**, le **groupe de ressources** et la **région**, puis cliquez sur **Créer**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Une fois le projet créé, attendez que l’application Web soit créée dans Azure App Service, comme indiqué dans la fenêtre **Activité Azure App Service** . Cliquez ensuite sur **Publier MyTaskListApp dans cette application Web**.
7. Cliquez sur **Publier**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Une fois que votre application ASP.NET par défaut est publiée sur Azure App Service Web Apps, elle est lancée dans le navigateur.

## <a name="install-the-mongodb-c-driver"></a>Installation du pilote MongoDB C#
MongoDB offre une prise en charge côté client des applications C# via un pilote à installer sur votre ordinateur de développement local. Le pilote C# est disponible via NuGet.

Pour installer le pilote MongoDB C# :

1. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet **MyTaskListApp**, puis sélectionnez **Gérer les packages NuGet**.
   
    ![Gérer les packages NuGet][VS2013ManageNuGetPackages]
2. Dans le volet gauche de la fenêtre **Gérer les packages NuGet**, cliquez sur **En ligne**. Dans la zone **Rechercher en ligne** de droite, tapez « mongodb.driver ».  Cliquez sur **Installer** pour installer le pilote.
   
    ![Recherche du pilote MongoDB C#][SearchforMongoDBCSharpDriver]
3. Cliquez sur **J'accepte** pour accepter les termes du contrat de licence 10gen, Inc.
4. Cliquez sur **Fermer** une fois le pilote installé.
    ![Pilote MongoDB C# installé][MongoDBCsharpDriverInstalled]

Le pilote MongoDB C# est maintenant installé.  Des références vers les bibliothèques **MongoDB.Bson**, **MongoDB.Driver** et **MongoDB.Driver.Core** ont été ajoutées au projet.

![Références du pilote MongoDB C#][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Ajout d'un modèle
Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le dossier *Modèles* et **ajoutez** une nouvelle **classe** que vous nommez *TaskModel.cs*.  Dans *TaskModel.cs*, remplacez le code existant par le code suivant :

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-the-data-access-layer"></a>Ajout de la couche d'accès aux données
Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet *MyTaskListApp* et **ajoutez** un **nouveau dossier** appelé *DAL*.  Cliquez avec le bouton droit sur le dossier *DAL* et **ajoutez** une nouvelle **classe**. Nommez le fichier de classe *Dal.cs*.  Dans *Dal.cs*, remplacez le code existant par le code suivant :

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  The database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from the MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }

            // Creates a Task and inserts it into the collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }

            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            # region IDisposable

            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a>Ajout d'un contrôleur
Ouvrez le fichier *Controllers\HomeController.cs* dans l’**Explorateur de solutions** et remplacez le code existant par ce qui suit :

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-the-styles"></a>Configuration des styles
Pour changer le titre en haut de la page, ouvrez le fichier *Views\Shared\\_Layout.cshtml* dans l’**Explorateur de solutions** et remplacez « Nom de l’application » dans le titre de la barre de navigation par « Application My Task List » afin d’afficher ce qui suit :

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

Pour configurer le menu Liste des tâches, ouvrez le fichier *\Views\Home\Index.cshtml* et remplacez le code existant par le code suivant :

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


Pour permettre la création d’une tâche, cliquez avec le bouton droit sur le dossier *Views\Home\\* et **ajoutez** une **vue**.  que vous nommez *Créer*. Remplacez le code par ce qui suit :

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

**Explorateur de solutions** doit se présenter comme suit :

![Explorateur de solutions][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a>Configuration de la chaîne de connexion MongoDB
Dans l' **Explorateur de solutions**, ouvrez le fichier *DAL/Dal.cs* . Recherchez la ligne de code suivante :

    private string connectionString = "mongodb://<vm-dns-name>";

Remplacez `<vm-dns-name>` par le nom DNS de la machine virtuelle exécutant MongoDB, que vous avez créée à l’étape [Création d’une machine virtuelle et installation de MongoDB][Create a virtual machine and install MongoDB] de ce didacticiel.  Pour rechercher le nom DNS de votre machine virtuelle, accédez au portail Azure, sélectionnez **Machines virtuelles** et recherchez **Nom DNS**.

Si le nom DNS de la machine virtuelle correspond à « testlinuxvm.cloudapp.net » et que MongoDB écoute sur le port par défaut 27017, la ligne de code de la chaîne de connexion se présente comme suit :

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Si le point de terminaison de la machine virtuelle spécifie un port externe différent pour MongoDB, vous pouvez indiquer ce port dans la chaîne de connexion :

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

Pour plus d’informations sur les chaînes de connexion MongoDB, consultez la rubrique [Connections][MongoConnectionStrings].

## <a name="test-the-local-deployment"></a>Test du déploiement local
Pour exécuter l’application sur votre ordinateur de développement, sélectionnez **Démarrer le débogage** dans le menu **Déboguer** ou appuyez sur **F5**. IIS Express démarre et un navigateur s'ouvre et lance la page d'accueil de l'application.  Vous pouvez ajouter une nouvelle tâche qui sera ajoutée à la base de données MongoDB exécutée sur votre machine virtuelle dans Azure.

![Application My Task List][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a>Publication sur Azure App Service Web Apps
Dans cette section, vous allez publier vos modifications apportées à Azure App Service Web Apps.

1. Dans l’Explorateur de solutions, cliquez une nouvelle fois avec le bouton droit sur **MyTaskListApp**, puis cliquez sur **Publier**.
2. Cliquez sur **Publier**.
   
    Votre application Web doit à présent s’exécuter dans Azure App Service et vous devez être en mesure d’accéder à la base de données MongoDB sur les machines virtuelles Azure.

## <a name="summary"></a>Résumé
Vous avez déployé votre application ASP.NET sur Azure App Service Web Apps. Pour afficher l’application Web :

1. Connectez-vous au portail Azure.
2. Cliquez sur **Applications Web**. 
3. Sélectionnez votre application Web dans la liste **Applications Web** .

Pour plus d’informations sur le développement d’applications C# sur MongoDB, reportez-vous à [CSharp Language Center][MongoC#LangCenter]. 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: ./media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: ./media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run the My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy the ASP.NET application to the web site using Git]: #deployapp
