---
title: "aaaCreate une application web dans Azure qui se connecte tooMongoDB en cours d’exécution sur un ordinateur virtuel"
description: "Un didacticiel vous apprend comment toouse Git toodeploy un tooAzure d’application ASP.NET, du Service d’applications connectées tooMongoDB sur une Machine virtuelle de Azure."
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
ms.openlocfilehash: 1f5f42c28c3c294d92c9ebf1499374931d47c010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a>Créer une application web dans Azure qui se connecte tooMongoDB en cours d’exécution sur un ordinateur virtuel
À l’aide de Git, vous pouvez déployer un tooAzure d’application ASP.NET Application Service Web Apps. Dans ce didacticiel, vous allez générer un frontal ASP.NET MVC simple application de liste de tâches qui se connecte MongoDB tooa de base de données en cours d’exécution sur un ordinateur virtuel dans Azure.  [MongoDB][MongoDB] est une base de données NoSQL open-source qui offre des performances élevées. Après avoir en cours d’exécution et test d’application ASP.NET de hello sur votre ordinateur de développement, vous allez télécharger hello application tooApp applications de Service Web à l’aide de Git.

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="background-knowledge"></a>Connaissances générales
Connaissance des éléments suivants de hello est utile pour ce didacticiel, toutefois ne pas obligatoire :

* pilote Hello c# pour MongoDB. Pour plus d’informations sur le développement d’applications C# contre MongoDB, consultez hello MongoDB [centre de langage CSharp][MongoC#LangCenter]. 
* infrastructure d’application web ASP .NET de Hello. Vous trouverez tous les détails sur hello [site Web ASP.net][ASP.NET].
* infrastructure d’application web Hello ASP .NET MVC. Vous trouverez tous les détails sur hello [site Web ASP.NET MVC][MVCWebSite].
* Azure. Pour commencer, lisez les informations relatives à [Azure][WindowsAzure].

## <a name="prerequisites"></a>Composants requis
* [Visual Studio Express 2013 pour le web][VSEWeb] ou [Visual Studio 2013][VSUlt]
* [Kit de développement logiciel (SDK) Azure pour .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Un abonnement Microsoft Azure actif

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Création d’une machine virtuelle et installation de MongoDB
Ce didacticiel part du principe que vous avez créé une machine virtuelle dans Azure. Après avoir créé l’ordinateur virtuel de hello, vous devez tooinstall MongoDB sur l’ordinateur virtuel de hello :

* toocreate une machine virtuelle Windows et installez MongoDB, consultez [installer de MongoDB sur une machine virtuelle exécutant Windows Server dans Azure][InstallMongoOnWindowsVM].

Après avoir créé l’ordinateur virtuel de hello dans Azure et installé MongoDB, être assuré que nom DNS hello tooremember de machine virtuelle de hello (« testlinuxvm.cloudapp.net », par exemple) et le port externe hello pour MongoDB que vous avez spécifié dans le point de terminaison hello.  Vous devez ces informations plus loin dans le didacticiel de hello.

<a id="createapp"></a>

## <a name="create-hello-application"></a>Créer l’application hello
Dans cette section, vous créez une application ASP.NET appelée « Ma liste de tâches » à l’aide de Visual Studio et effectuer un déploiement initial de tooAzure App Service Web Apps. Vous allez exécuter application hello localement, mais elle se connecter à une machine virtuelle tooyour sur Azure et y utiliser instance MongoDB hello que vous avez créé.

1. Dans Visual Studio, cliquez sur **Nouveau projet**.
   
    ![Page de démarrage Nouveau projet][StartPageNewProject]
2. Bonjour **nouveau projet** fenêtre, dans le volet gauche de hello, sélectionnez **Visual C#**, puis sélectionnez **Web**. Dans le volet du milieu hello, sélectionnez **Application Web ASP.NET**. Au bas de hello, nommez votre projet « MyTaskListApp », puis cliquez sur **OK**.
   
    ![Boîte de dialogue Nouveau projet][NewProjectMyTaskListApp]
3. Bonjour **nouveau projet ASP.NET** boîte de dialogue, sélectionnez **MVC**, puis cliquez sur **OK**.
   
    ![Sélection du modèle MVC][VS2013SelectMVCTemplate]
4. Si vous n’êtes pas déjà connecté à Microsoft Azure, vous serez invité à toosign dans. Suivez hello invites toosign dans Azure.
5. Une fois que vous êtes connecté, vous pouvez commencer à configurer votre application Web App Service. Spécifiez hello **nom de l’application Web**, **plan App Service**, **groupe de ressources**, et **région**, puis cliquez sur **créer**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Après la création du projet hello, attendez hello web application toobe créé dans Azure App Service, comme indiqué dans hello **Azure App Service activité** fenêtre. Ensuite, cliquez sur **toothis MyTaskListApp de publier l’application Web maintenant**.
7. Cliquez sur **Publier**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Une fois que votre application ASP.NET de valeur par défaut est publiée tooAzure App Service Web Apps, elle sera lancée dans le navigateur de hello.

## <a name="install-hello-mongodb-c-driver"></a>Installer hello pilote MongoDB c#
MongoDB offre la prise en charge côté client pour les applications c# via un pilote, vous devez tooinstall sur votre ordinateur de développement local. Hello c# pilote est disponible via NuGet.

hello tooinstall pilote MongoDB c# :

1. Dans **l’Explorateur de solutions**, avec le bouton hello **MyTaskListApp** de projet et sélectionnez **NuGetPackages de gérer**.
   
    ![Gérer les packages NuGet][VS2013ManageNuGetPackages]
2. Bonjour **gérer les Packages NuGet** , dans le volet gauche de hello, cliquez sur **Online**. Bonjour **recherche en ligne** sur hello droite, tapez « mongodb.driver ».  Cliquez sur **installer** pilote de hello tooinstall.
   
    ![Recherche du pilote MongoDB C#][SearchforMongoDBCSharpDriver]
3. Cliquez sur **J’accepte** tooaccept hello 10gen, Inc. les termes du contrat de licence.
4. Cliquez sur **fermer** après hello pilote a installé.
    ![Pilote MongoDB C# installé][MongoDBCsharpDriverInstalled]

Hello pilote MongoDB c# est maintenant installé.  Références toohello **MongoDB.Bson**, **MongoDB.Driver**, et **MongoDB.Driver.Core** bibliothèques ont été ajoutées toohello projet.

![Références du pilote MongoDB C#][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Ajout d'un modèle
Dans **l’Explorateur de solutions**, avec le bouton hello *modèles* dossier et **ajouter** un nouveau **classe** et nommez-le *TaskModel.cs* .  Dans *TaskModel.cs*, remplacez le code hello avec hello suivant de code :

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

## <a name="add-hello-data-access-layer"></a>Ajouter la couche d’accès aux données hello
Dans **l’Explorateur de solutions**, avec le bouton hello *MyTaskListApp* projet et **ajouter** un **nouveau dossier** nommé *DAL*.  Avec le bouton hello *DAL* dossier et **ajouter** un nouveau **classe**. Fichier de classe nom hello *Dal.cs*.  Dans *Dal.cs*, remplacez le code hello avec hello suivant de code :

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

            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from hello MongoDB server.        
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

            // Creates a Task and inserts it into hello collection in MongoDB.
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
Ouvrez hello *Controllers\HomeController.cs* de fichiers dans **l’Explorateur de solutions** et remplacez le code existant de hello par qui suit hello :

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

## <a name="set-up-hello-styles"></a>Définir des styles de hello
titre de hello toochange en hello haut hello, ouvrez hello *Views\Shared\\_Layout.cshtml* fichier **l’Explorateur de solutions** et remplacez « Mes tâches de « Nom de l’Application » dans l’en-tête de barre de navigation hello Liste des applications » afin qu’il ressemble à ceci :

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

Dans tooset de commande de menu de liste des tâches hello, ouvrez hello *\Views\Home\Index.cshtml* de fichier et remplacez le code hello avec hello suivant de code :

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


tooadd hello capacité toocreate une nouvelle tâche, avec le bouton droit hello *Views\Home\\*  dossier et **ajouter** un **vue**.  Nom d’affichage de hello *créer*. Remplacez le code de hello par hello qui suit :

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

## <a name="set-hello-mongodb-connection-string"></a>Définir la chaîne de connexion hello MongoDB
Dans **l’Explorateur de solutions**, ouvrez hello *DAL/Dal.cs* fichier. Recherche hello ligne de code suivante :

    private string connectionString = "mongodb://<vm-dns-name>";

Remplacez `<vm-dns-name>` portant le nom DNS de hello de machine virtuelle de hello en cours d’exécution MongoDB que vous avez créé dans hello [créer un ordinateur virtuel et installez MongoDB] [ Create a virtual machine and install MongoDB] étape de ce didacticiel.  nom DNS toofind hello de votre machine virtuelle, accédez toohello portail Azure, sélectionnez **virtuels**et recherchez **nom DNS**.

Si le nom DNS de hello de machine virtuelle de hello est « testlinuxvm.cloudapp.net » et est à l’écoute sur le port par défaut de hello 27017 MongoDB, ligne de chaîne de connexion hello du code doit ressembler à :

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Si le point de terminaison de machine virtuelle hello spécifie un autre port externe pour MongoDB, vous pouvez spécifier des ports de hello dans la chaîne de connexion hello :

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

Pour plus d’informations sur les chaînes de connexion MongoDB, consultez la rubrique [Connections][MongoConnectionStrings].

## <a name="test-hello-local-deployment"></a>Tester le déploiement local de hello
sélectionner de votre application sur votre ordinateur de développement, toorun **démarrer le débogage** de hello **déboguer** menu ou appuyez sur **F5**. Démarrage d’IIS Express et un navigateur s’ouvre et lance la page d’accueil de l’application hello.  Vous pouvez ajouter une nouvelle tâche, qui sera ajoutée MongoDB toohello de base de données en cours d’exécution sur votre machine virtuelle dans Azure.

![Application My Task List][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a>Publier des applications Web de tooAzure App Service
Dans cette section, vous allez publier votre application de Service Web Apps de tooAzure modifications.

1. Dans l’Explorateur de solutions, cliquez une nouvelle fois avec le bouton droit sur **MyTaskListApp**, puis cliquez sur **Publier**.
2. Cliquez sur **Publier**.
   
    Vous devez maintenant voir votre application web en cours d’exécution dans Azure App Service et l’accès à la base de données MongoDB hello dans les Machines virtuelles Azure.

## <a name="summary"></a>Résumé
Vous avez déployé avec succès votre tooAzure d’application ASP.NET Application Service Web Apps. application web tooview hello :

1. Connectez-vous à hello portail Azure.
2. Cliquez sur **Applications Web**. 
3. Sélectionnez votre application web Bonjour **Web Apps** liste.

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
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp
