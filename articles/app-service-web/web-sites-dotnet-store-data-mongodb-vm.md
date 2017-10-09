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
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a><span data-ttu-id="34cf9-103">Créer une application web dans Azure qui se connecte tooMongoDB en cours d’exécution sur un ordinateur virtuel</span><span class="sxs-lookup"><span data-stu-id="34cf9-103">Create a web app in Azure that connects tooMongoDB running on a virtual machine</span></span>
<span data-ttu-id="34cf9-104">À l’aide de Git, vous pouvez déployer un tooAzure d’application ASP.NET Application Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="34cf9-104">Using Git, you can deploy an ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="34cf9-105">Dans ce didacticiel, vous allez générer un frontal ASP.NET MVC simple application de liste de tâches qui se connecte MongoDB tooa de base de données en cours d’exécution sur un ordinateur virtuel dans Azure.</span><span class="sxs-lookup"><span data-stu-id="34cf9-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects tooa MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="34cf9-106">[MongoDB][MongoDB] est une base de données NoSQL open-source qui offre des performances élevées.</span><span class="sxs-lookup"><span data-stu-id="34cf9-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="34cf9-107">Après avoir en cours d’exécution et test d’application ASP.NET de hello sur votre ordinateur de développement, vous allez télécharger hello application tooApp applications de Service Web à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="34cf9-107">After running and testing hello ASP.NET application on your development computer, you will upload hello application tooApp Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="34cf9-108">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="34cf9-108">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="34cf9-109">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="34cf9-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="34cf9-110">Connaissances générales</span><span class="sxs-lookup"><span data-stu-id="34cf9-110">Background knowledge</span></span>
<span data-ttu-id="34cf9-111">Connaissance des éléments suivants de hello est utile pour ce didacticiel, toutefois ne pas obligatoire :</span><span class="sxs-lookup"><span data-stu-id="34cf9-111">Knowledge of hello following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="34cf9-112">pilote Hello c# pour MongoDB.</span><span class="sxs-lookup"><span data-stu-id="34cf9-112">hello C# driver for MongoDB.</span></span> <span data-ttu-id="34cf9-113">Pour plus d’informations sur le développement d’applications C# contre MongoDB, consultez hello MongoDB [centre de langage CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="34cf9-113">For more information on developing C# applications against MongoDB, see hello MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="34cf9-114">infrastructure d’application web ASP .NET de Hello.</span><span class="sxs-lookup"><span data-stu-id="34cf9-114">hello ASP .NET web application framework.</span></span> <span data-ttu-id="34cf9-115">Vous trouverez tous les détails sur hello [site Web ASP.net][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="34cf9-115">You can learn all about it at hello [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="34cf9-116">infrastructure d’application web Hello ASP .NET MVC.</span><span class="sxs-lookup"><span data-stu-id="34cf9-116">hello ASP .NET MVC web application framework.</span></span> <span data-ttu-id="34cf9-117">Vous trouverez tous les détails sur hello [site Web ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="34cf9-117">You can learn all about it at hello [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="34cf9-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="34cf9-118">Azure.</span></span> <span data-ttu-id="34cf9-119">Pour commencer, lisez les informations relatives à [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="34cf9-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34cf9-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="34cf9-120">Prerequisites</span></span>
* <span data-ttu-id="34cf9-121">[Visual Studio Express 2013 pour le web][VSEWeb] ou [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="34cf9-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="34cf9-122">Kit de développement logiciel (SDK) Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="34cf9-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="34cf9-123">Un abonnement Microsoft Azure actif</span><span class="sxs-lookup"><span data-stu-id="34cf9-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="34cf9-124">Création d’une machine virtuelle et installation de MongoDB</span><span class="sxs-lookup"><span data-stu-id="34cf9-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="34cf9-125">Ce didacticiel part du principe que vous avez créé une machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="34cf9-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="34cf9-126">Après avoir créé l’ordinateur virtuel de hello, vous devez tooinstall MongoDB sur l’ordinateur virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="34cf9-126">After creating hello virtual machine you need tooinstall MongoDB on hello virtual machine:</span></span>

* <span data-ttu-id="34cf9-127">toocreate une machine virtuelle Windows et installez MongoDB, consultez [installer de MongoDB sur une machine virtuelle exécutant Windows Server dans Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="34cf9-127">toocreate a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="34cf9-128">Après avoir créé l’ordinateur virtuel de hello dans Azure et installé MongoDB, être assuré que nom DNS hello tooremember de machine virtuelle de hello (« testlinuxvm.cloudapp.net », par exemple) et le port externe hello pour MongoDB que vous avez spécifié dans le point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="34cf9-128">After you have created hello virtual machine in Azure and installed MongoDB, be sure tooremember hello DNS name of hello virtual machine ("testlinuxvm.cloudapp.net", for example) and hello external port for MongoDB that you specified in hello endpoint.</span></span>  <span data-ttu-id="34cf9-129">Vous devez ces informations plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="34cf9-129">You will need this information later in hello tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-hello-application"></a><span data-ttu-id="34cf9-130">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="34cf9-130">Create hello application</span></span>
<span data-ttu-id="34cf9-131">Dans cette section, vous créez une application ASP.NET appelée « Ma liste de tâches » à l’aide de Visual Studio et effectuer un déploiement initial de tooAzure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="34cf9-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment tooAzure App Service Web Apps.</span></span> <span data-ttu-id="34cf9-132">Vous allez exécuter application hello localement, mais elle se connecter à une machine virtuelle tooyour sur Azure et y utiliser instance MongoDB hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="34cf9-132">You will run hello application locally, but it will connect tooyour virtual machine on Azure and use hello MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="34cf9-133">Dans Visual Studio, cliquez sur **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Page de démarrage Nouveau projet][StartPageNewProject]
2. <span data-ttu-id="34cf9-135">Bonjour **nouveau projet** fenêtre, dans le volet gauche de hello, sélectionnez **Visual C#**, puis sélectionnez **Web**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-135">In hello **New Project** window, in hello left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="34cf9-136">Dans le volet du milieu hello, sélectionnez **Application Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-136">In hello middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="34cf9-137">Au bas de hello, nommez votre projet « MyTaskListApp », puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-137">At hello bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Boîte de dialogue Nouveau projet][NewProjectMyTaskListApp]
3. <span data-ttu-id="34cf9-139">Bonjour **nouveau projet ASP.NET** boîte de dialogue, sélectionnez **MVC**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-139">In hello **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Sélection du modèle MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="34cf9-141">Si vous n’êtes pas déjà connecté à Microsoft Azure, vous serez invité à toosign dans.</span><span class="sxs-lookup"><span data-stu-id="34cf9-141">If you aren't already signed into Microsoft Azure, you will be prompted toosign in.</span></span> <span data-ttu-id="34cf9-142">Suivez hello invites toosign dans Azure.</span><span class="sxs-lookup"><span data-stu-id="34cf9-142">Follow hello prompts toosign into Azure.</span></span>
5. <span data-ttu-id="34cf9-143">Une fois que vous êtes connecté, vous pouvez commencer à configurer votre application Web App Service.</span><span class="sxs-lookup"><span data-stu-id="34cf9-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="34cf9-144">Spécifiez hello **nom de l’application Web**, **plan App Service**, **groupe de ressources**, et **région**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-144">Specify hello **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="34cf9-145">Après la création du projet hello, attendez hello web application toobe créé dans Azure App Service, comme indiqué dans hello **Azure App Service activité** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="34cf9-145">After hello project creation completes, wait for hello web app toobe created in Azure App Service as indicated in hello **Azure App Service Activity** window.</span></span> <span data-ttu-id="34cf9-146">Ensuite, cliquez sur **toothis MyTaskListApp de publier l’application Web maintenant**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-146">Then, click **Publish MyTaskListApp toothis Web App now**.</span></span>
7. <span data-ttu-id="34cf9-147">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="34cf9-148">Une fois que votre application ASP.NET de valeur par défaut est publiée tooAzure App Service Web Apps, elle sera lancée dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="34cf9-148">Once your default ASP.NET application is published tooAzure App Service Web Apps, it will be launched in hello browser.</span></span>

## <a name="install-hello-mongodb-c-driver"></a><span data-ttu-id="34cf9-149">Installer hello pilote MongoDB c#</span><span class="sxs-lookup"><span data-stu-id="34cf9-149">Install hello MongoDB C# driver</span></span>
<span data-ttu-id="34cf9-150">MongoDB offre la prise en charge côté client pour les applications c# via un pilote, vous devez tooinstall sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="34cf9-150">MongoDB offers client-side support for C# applications through a driver, which you need tooinstall on your local development computer.</span></span> <span data-ttu-id="34cf9-151">Hello c# pilote est disponible via NuGet.</span><span class="sxs-lookup"><span data-stu-id="34cf9-151">hello C# driver is available through NuGet.</span></span>

<span data-ttu-id="34cf9-152">hello tooinstall pilote MongoDB c# :</span><span class="sxs-lookup"><span data-stu-id="34cf9-152">tooinstall hello MongoDB C# driver:</span></span>

1. <span data-ttu-id="34cf9-153">Dans **l’Explorateur de solutions**, avec le bouton hello **MyTaskListApp** de projet et sélectionnez **NuGetPackages de gérer**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-153">In **Solution Explorer**, right-click hello **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Gérer les packages NuGet][VS2013ManageNuGetPackages]
2. <span data-ttu-id="34cf9-155">Bonjour **gérer les Packages NuGet** , dans le volet gauche de hello, cliquez sur **Online**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-155">In hello **Manage NuGet Packages** window, in hello left pane, click **Online**.</span></span> <span data-ttu-id="34cf9-156">Bonjour **recherche en ligne** sur hello droite, tapez « mongodb.driver ».</span><span class="sxs-lookup"><span data-stu-id="34cf9-156">In hello **Search Online** box on hello right, type "mongodb.driver".</span></span>  <span data-ttu-id="34cf9-157">Cliquez sur **installer** pilote de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="34cf9-157">Click **Install** tooinstall hello driver.</span></span>
   
    ![Recherche du pilote MongoDB C#][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="34cf9-159">Cliquez sur **J’accepte** tooaccept hello 10gen, Inc. les termes du contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="34cf9-159">Click **I Accept** tooaccept hello 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="34cf9-160">Cliquez sur **fermer** après hello pilote a installé.</span><span class="sxs-lookup"><span data-stu-id="34cf9-160">Click **Close** after hello driver has installed.</span></span>
    <span data-ttu-id="34cf9-161">![Pilote MongoDB C# installé][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="34cf9-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="34cf9-162">Hello pilote MongoDB c# est maintenant installé.</span><span class="sxs-lookup"><span data-stu-id="34cf9-162">hello MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="34cf9-163">Références toohello **MongoDB.Bson**, **MongoDB.Driver**, et **MongoDB.Driver.Core** bibliothèques ont été ajoutées toohello projet.</span><span class="sxs-lookup"><span data-stu-id="34cf9-163">References toohello **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added toohello project.</span></span>

![Références du pilote MongoDB C#][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="34cf9-165">Ajout d'un modèle</span><span class="sxs-lookup"><span data-stu-id="34cf9-165">Add a model</span></span>
<span data-ttu-id="34cf9-166">Dans **l’Explorateur de solutions**, avec le bouton hello *modèles* dossier et **ajouter** un nouveau **classe** et nommez-le *TaskModel.cs* .</span><span class="sxs-lookup"><span data-stu-id="34cf9-166">In **Solution Explorer**, right-click hello *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="34cf9-167">Dans *TaskModel.cs*, remplacez le code hello avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="34cf9-167">In *TaskModel.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-hello-data-access-layer"></a><span data-ttu-id="34cf9-168">Ajouter la couche d’accès aux données hello</span><span class="sxs-lookup"><span data-stu-id="34cf9-168">Add hello data access layer</span></span>
<span data-ttu-id="34cf9-169">Dans **l’Explorateur de solutions**, avec le bouton hello *MyTaskListApp* projet et **ajouter** un **nouveau dossier** nommé *DAL*.</span><span class="sxs-lookup"><span data-stu-id="34cf9-169">In **Solution Explorer**, right-click hello *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="34cf9-170">Avec le bouton hello *DAL* dossier et **ajouter** un nouveau **classe**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-170">Right-click hello *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="34cf9-171">Fichier de classe nom hello *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="34cf9-171">Name hello class file *Dal.cs*.</span></span>  <span data-ttu-id="34cf9-172">Dans *Dal.cs*, remplacez le code hello avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="34cf9-172">In *Dal.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-a-controller"></a><span data-ttu-id="34cf9-173">Ajout d'un contrôleur</span><span class="sxs-lookup"><span data-stu-id="34cf9-173">Add a controller</span></span>
<span data-ttu-id="34cf9-174">Ouvrez hello *Controllers\HomeController.cs* de fichiers dans **l’Explorateur de solutions** et remplacez le code existant de hello par qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="34cf9-174">Open hello *Controllers\HomeController.cs* file in **Solution Explorer** and replace hello existing code with hello following:</span></span>

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

## <a name="set-up-hello-styles"></a><span data-ttu-id="34cf9-175">Définir des styles de hello</span><span class="sxs-lookup"><span data-stu-id="34cf9-175">Set up hello styles</span></span>
<span data-ttu-id="34cf9-176">titre de hello toochange en hello haut hello, ouvrez hello *Views\Shared\\_Layout.cshtml* fichier **l’Explorateur de solutions** et remplacez « Mes tâches de « Nom de l’Application » dans l’en-tête de barre de navigation hello Liste des applications » afin qu’il ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="34cf9-176">toochange hello title at hello top of hello page, open hello *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in hello navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="34cf9-177">Dans tooset de commande de menu de liste des tâches hello, ouvrez hello *\Views\Home\Index.cshtml* de fichier et remplacez le code hello avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="34cf9-177">In order tooset up hello Task List menu, open hello *\Views\Home\Index.cshtml* file and replace hello existing code with hello following code:</span></span>

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


<span data-ttu-id="34cf9-178">tooadd hello capacité toocreate une nouvelle tâche, avec le bouton droit hello *Views\Home\\*  dossier et **ajouter** un **vue**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-178">tooadd hello ability toocreate a new task, right-click hello *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="34cf9-179">Nom d’affichage de hello *créer*.</span><span class="sxs-lookup"><span data-stu-id="34cf9-179">Name hello view *Create*.</span></span> <span data-ttu-id="34cf9-180">Remplacez le code de hello par hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="34cf9-180">Replace hello code with hello following:</span></span>

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

<span data-ttu-id="34cf9-181">**Explorateur de solutions** doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="34cf9-181">**Solution Explorer** should look like this:</span></span>

![Explorateur de solutions][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a><span data-ttu-id="34cf9-183">Définir la chaîne de connexion hello MongoDB</span><span class="sxs-lookup"><span data-stu-id="34cf9-183">Set hello MongoDB connection string</span></span>
<span data-ttu-id="34cf9-184">Dans **l’Explorateur de solutions**, ouvrez hello *DAL/Dal.cs* fichier.</span><span class="sxs-lookup"><span data-stu-id="34cf9-184">In **Solution Explorer**, open hello *DAL/Dal.cs* file.</span></span> <span data-ttu-id="34cf9-185">Recherche hello ligne de code suivante :</span><span class="sxs-lookup"><span data-stu-id="34cf9-185">Find hello following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="34cf9-186">Remplacez `<vm-dns-name>` portant le nom DNS de hello de machine virtuelle de hello en cours d’exécution MongoDB que vous avez créé dans hello [créer un ordinateur virtuel et installez MongoDB] [ Create a virtual machine and install MongoDB] étape de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="34cf9-186">Replace `<vm-dns-name>` with hello DNS name of hello virtual machine running MongoDB you created in hello [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="34cf9-187">nom DNS toofind hello de votre machine virtuelle, accédez toohello portail Azure, sélectionnez **virtuels**et recherchez **nom DNS**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-187">toofind hello DNS name of your virtual machine, go toohello Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="34cf9-188">Si le nom DNS de hello de machine virtuelle de hello est « testlinuxvm.cloudapp.net » et est à l’écoute sur le port par défaut de hello 27017 MongoDB, ligne de chaîne de connexion hello du code doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="34cf9-188">If hello DNS name of hello virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on hello default port 27017, hello connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="34cf9-189">Si le point de terminaison de machine virtuelle hello spécifie un autre port externe pour MongoDB, vous pouvez spécifier des ports de hello dans la chaîne de connexion hello :</span><span class="sxs-lookup"><span data-stu-id="34cf9-189">If hello virtual machine endpoint specifies a different external port for MongoDB, you can specifiy hello port in hello connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="34cf9-190">Pour plus d’informations sur les chaînes de connexion MongoDB, consultez la rubrique [Connections][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="34cf9-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-hello-local-deployment"></a><span data-ttu-id="34cf9-191">Tester le déploiement local de hello</span><span class="sxs-lookup"><span data-stu-id="34cf9-191">Test hello local deployment</span></span>
<span data-ttu-id="34cf9-192">sélectionner de votre application sur votre ordinateur de développement, toorun **démarrer le débogage** de hello **déboguer** menu ou appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-192">toorun your application on your development computer, select **Start Debugging** from hello **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="34cf9-193">Démarrage d’IIS Express et un navigateur s’ouvre et lance la page d’accueil de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="34cf9-193">IIS Express starts and a browser opens and launches hello application's home page.</span></span>  <span data-ttu-id="34cf9-194">Vous pouvez ajouter une nouvelle tâche, qui sera ajoutée MongoDB toohello de base de données en cours d’exécution sur votre machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="34cf9-194">You can add a new task, which will be added toohello MongoDB database running on your virtual machine in Azure.</span></span>

![Application My Task List][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a><span data-ttu-id="34cf9-196">Publier des applications Web de tooAzure App Service</span><span class="sxs-lookup"><span data-stu-id="34cf9-196">Publish tooAzure App Service Web Apps</span></span>
<span data-ttu-id="34cf9-197">Dans cette section, vous allez publier votre application de Service Web Apps de tooAzure modifications.</span><span class="sxs-lookup"><span data-stu-id="34cf9-197">In this section you will publish your changes tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="34cf9-198">Dans l’Explorateur de solutions, cliquez une nouvelle fois avec le bouton droit sur **MyTaskListApp**, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="34cf9-199">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="34cf9-200">Vous devez maintenant voir votre application web en cours d’exécution dans Azure App Service et l’accès à la base de données MongoDB hello dans les Machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="34cf9-200">You should now see your web app running in Azure App Service and accessing hello MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="34cf9-201">Résumé</span><span class="sxs-lookup"><span data-stu-id="34cf9-201">Summary</span></span>
<span data-ttu-id="34cf9-202">Vous avez déployé avec succès votre tooAzure d’application ASP.NET Application Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="34cf9-202">You have now successfully deployed your ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="34cf9-203">application web tooview hello :</span><span class="sxs-lookup"><span data-stu-id="34cf9-203">tooview hello web app:</span></span>

1. <span data-ttu-id="34cf9-204">Connectez-vous à hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="34cf9-204">Log into hello Azure Portal.</span></span>
2. <span data-ttu-id="34cf9-205">Cliquez sur **Applications Web**.</span><span class="sxs-lookup"><span data-stu-id="34cf9-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="34cf9-206">Sélectionnez votre application web Bonjour **Web Apps** liste.</span><span class="sxs-lookup"><span data-stu-id="34cf9-206">Select your web app in hello **Web Apps** list.</span></span>

<span data-ttu-id="34cf9-207">Pour plus d’informations sur le développement d’applications C# sur MongoDB, reportez-vous à [CSharp Language Center][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="34cf9-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
