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
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a><span data-ttu-id="7d7b5-103">Création d’une application Web Azure se connectant à MongoDB exécuté sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7d7b5-103">Create a web app in Azure that connects to MongoDB running on a virtual machine</span></span>
<span data-ttu-id="7d7b5-104">Git vous permet de déployer une application ASP.NET sur Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-104">Using Git, you can deploy an ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="7d7b5-105">Ce didacticiel vous apprend à créer une simple application frontale de liste de tâches ASP.NET MVC se connectant à une base de données MongoDB exécutée sur une machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects to a MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="7d7b5-106">[MongoDB][MongoDB] est une base de données NoSQL open-source qui offre des performances élevées.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="7d7b5-107">Après avoir exécuté et testé l’application ASP.NET sur votre ordinateur de développement, vous téléchargerez l’application vers App Service Web Apps à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-107">After running and testing the ASP.NET application on your development computer, you will upload the application to App Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="7d7b5-108">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-108">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7d7b5-109">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="7d7b5-110">Connaissances générales</span><span class="sxs-lookup"><span data-stu-id="7d7b5-110">Background knowledge</span></span>
<span data-ttu-id="7d7b5-111">Dans le cadre de ce didacticiel, la connaissance des éléments suivants est utile, mais pas obligatoire :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-111">Knowledge of the following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="7d7b5-112">Pilote C# pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="7d7b5-112">The C# driver for MongoDB.</span></span> <span data-ttu-id="7d7b5-113">Pour plus d’informations sur le développement d’applications C# sur MongoDB, reportez-vous au [CSharp Language Center][MongoC#LangCenter] de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-113">For more information on developing C# applications against MongoDB, see the MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="7d7b5-114">Infrastructure de développement d'applications Web ASP .NET</span><span class="sxs-lookup"><span data-stu-id="7d7b5-114">The ASP .NET web application framework.</span></span> <span data-ttu-id="7d7b5-115">Pour plus d’informations, consultez le [site web ASP.net][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="7d7b5-115">You can learn all about it at the [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="7d7b5-116">Infrastructure de développement d'applications Web ASP .NET MVC</span><span class="sxs-lookup"><span data-stu-id="7d7b5-116">The ASP .NET MVC web application framework.</span></span> <span data-ttu-id="7d7b5-117">Pour plus d’informations, consultez le [site web ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="7d7b5-117">You can learn all about it at the [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="7d7b5-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-118">Azure.</span></span> <span data-ttu-id="7d7b5-119">Pour commencer, lisez les informations relatives à [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="7d7b5-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d7b5-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7d7b5-120">Prerequisites</span></span>
* <span data-ttu-id="7d7b5-121">[Visual Studio Express 2013 pour le web][VSEWeb] ou [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="7d7b5-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="7d7b5-122">Kit de développement logiciel (SDK) Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="7d7b5-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="7d7b5-123">Un abonnement Microsoft Azure actif</span><span class="sxs-lookup"><span data-stu-id="7d7b5-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="7d7b5-124">Création d’une machine virtuelle et installation de MongoDB</span><span class="sxs-lookup"><span data-stu-id="7d7b5-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="7d7b5-125">Ce didacticiel part du principe que vous avez créé une machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="7d7b5-126">Une fois la machine virtuelle créée, vous devez y installer MongoDB :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-126">After creating the virtual machine you need to install MongoDB on the virtual machine:</span></span>

* <span data-ttu-id="7d7b5-127">Pour créer une machine virtuelle Windows et installer MongoDB, consultez la rubrique [Installation de MongoDB sur une machine virtuelle exécutant Windows Server dans Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="7d7b5-127">To create a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="7d7b5-128">Après avoir créé la machine virtuelle dans Azure et installé MongoDB, mémorisez le nom DNS de la machine virtuelle (« testlinuxvm.cloudapp.net », par exemple) ainsi que le port externe de MongoDB spécifié dans le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-128">After you have created the virtual machine in Azure and installed MongoDB, be sure to remember the DNS name of the virtual machine ("testlinuxvm.cloudapp.net", for example) and the external port for MongoDB that you specified in the endpoint.</span></span>  <span data-ttu-id="7d7b5-129">Ces informations vous seront nécessaires plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-129">You will need this information later in the tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-the-application"></a><span data-ttu-id="7d7b5-130">Création de l'application</span><span class="sxs-lookup"><span data-stu-id="7d7b5-130">Create the application</span></span>
<span data-ttu-id="7d7b5-131">Dans cette section, vous allez créer une application ASP.NET appelée « My Task List » à l’aide de Visual Studio et effectuer un déploiement initial vers Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment to Azure App Service Web Apps.</span></span> <span data-ttu-id="7d7b5-132">Vous exécuterez cette application localement, mais elle se connectera à votre machine virtuelle sur Azure et utilisera l'instance MongoDB que vous y avez créée.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-132">You will run the application locally, but it will connect to your virtual machine on Azure and use the MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="7d7b5-133">Dans Visual Studio, cliquez sur **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Page de démarrage Nouveau projet][StartPageNewProject]
2. <span data-ttu-id="7d7b5-135">Dans le volet gauche de la fenêtre **Nouveau projet**, sélectionnez **Visual C#**, puis **Web**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-135">In the **New Project** window, in the left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="7d7b5-136">Dans le volet central, sélectionnez **Application Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-136">In the middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="7d7b5-137">En bas, nommez votre projet « MyTaskListApp », puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-137">At the bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Boîte de dialogue Nouveau projet][NewProjectMyTaskListApp]
3. <span data-ttu-id="7d7b5-139">Dans la boîte de dialogue **Nouveau projet ASP.NET**, sélectionnez **MVC**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-139">In the **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Sélection du modèle MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="7d7b5-141">Si vous n’êtes pas déjà connecté à Microsoft Azure, vous serez invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-141">If you aren't already signed into Microsoft Azure, you will be prompted to sign in.</span></span> <span data-ttu-id="7d7b5-142">Suivez les instructions de l’invite pour vous connecter à Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-142">Follow the prompts to sign into Azure.</span></span>
5. <span data-ttu-id="7d7b5-143">Une fois que vous êtes connecté, vous pouvez commencer à configurer votre application Web App Service.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="7d7b5-144">Indiquez le **nom de l’application web**, le **plan App Service**, le **groupe de ressources** et la **région**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-144">Specify the **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="7d7b5-145">Une fois le projet créé, attendez que l’application Web soit créée dans Azure App Service, comme indiqué dans la fenêtre **Activité Azure App Service** .</span><span class="sxs-lookup"><span data-stu-id="7d7b5-145">After the project creation completes, wait for the web app to be created in Azure App Service as indicated in the **Azure App Service Activity** window.</span></span> <span data-ttu-id="7d7b5-146">Cliquez ensuite sur **Publier MyTaskListApp dans cette application Web**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-146">Then, click **Publish MyTaskListApp to this Web App now**.</span></span>
7. <span data-ttu-id="7d7b5-147">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="7d7b5-148">Une fois que votre application ASP.NET par défaut est publiée sur Azure App Service Web Apps, elle est lancée dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-148">Once your default ASP.NET application is published to Azure App Service Web Apps, it will be launched in the browser.</span></span>

## <a name="install-the-mongodb-c-driver"></a><span data-ttu-id="7d7b5-149">Installation du pilote MongoDB C#</span><span class="sxs-lookup"><span data-stu-id="7d7b5-149">Install the MongoDB C# driver</span></span>
<span data-ttu-id="7d7b5-150">MongoDB offre une prise en charge côté client des applications C# via un pilote à installer sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-150">MongoDB offers client-side support for C# applications through a driver, which you need to install on your local development computer.</span></span> <span data-ttu-id="7d7b5-151">Le pilote C# est disponible via NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-151">The C# driver is available through NuGet.</span></span>

<span data-ttu-id="7d7b5-152">Pour installer le pilote MongoDB C# :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-152">To install the MongoDB C# driver:</span></span>

1. <span data-ttu-id="7d7b5-153">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet **MyTaskListApp**, puis sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-153">In **Solution Explorer**, right-click the **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Gérer les packages NuGet][VS2013ManageNuGetPackages]
2. <span data-ttu-id="7d7b5-155">Dans le volet gauche de la fenêtre **Gérer les packages NuGet**, cliquez sur **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-155">In the **Manage NuGet Packages** window, in the left pane, click **Online**.</span></span> <span data-ttu-id="7d7b5-156">Dans la zone **Rechercher en ligne** de droite, tapez « mongodb.driver ».</span><span class="sxs-lookup"><span data-stu-id="7d7b5-156">In the **Search Online** box on the right, type "mongodb.driver".</span></span>  <span data-ttu-id="7d7b5-157">Cliquez sur **Installer** pour installer le pilote.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-157">Click **Install** to install the driver.</span></span>
   
    ![Recherche du pilote MongoDB C#][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="7d7b5-159">Cliquez sur **J'accepte** pour accepter les termes du contrat de licence 10gen, Inc.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-159">Click **I Accept** to accept the 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="7d7b5-160">Cliquez sur **Fermer** une fois le pilote installé.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-160">Click **Close** after the driver has installed.</span></span>
    <span data-ttu-id="7d7b5-161">![Pilote MongoDB C# installé][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="7d7b5-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="7d7b5-162">Le pilote MongoDB C# est maintenant installé.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-162">The MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="7d7b5-163">Des références vers les bibliothèques **MongoDB.Bson**, **MongoDB.Driver** et **MongoDB.Driver.Core** ont été ajoutées au projet.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-163">References to the **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added to the project.</span></span>

![Références du pilote MongoDB C#][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="7d7b5-165">Ajout d'un modèle</span><span class="sxs-lookup"><span data-stu-id="7d7b5-165">Add a model</span></span>
<span data-ttu-id="7d7b5-166">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le dossier *Modèles* et **ajoutez** une nouvelle **classe** que vous nommez *TaskModel.cs*.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-166">In **Solution Explorer**, right-click the *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="7d7b5-167">Dans *TaskModel.cs*, remplacez le code existant par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-167">In *TaskModel.cs*, replace the existing code with the following code:</span></span>

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

## <a name="add-the-data-access-layer"></a><span data-ttu-id="7d7b5-168">Ajout de la couche d'accès aux données</span><span class="sxs-lookup"><span data-stu-id="7d7b5-168">Add the data access layer</span></span>
<span data-ttu-id="7d7b5-169">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet *MyTaskListApp* et **ajoutez** un **nouveau dossier** appelé *DAL*.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-169">In **Solution Explorer**, right-click the *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="7d7b5-170">Cliquez avec le bouton droit sur le dossier *DAL* et **ajoutez** une nouvelle **classe**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-170">Right-click the *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="7d7b5-171">Nommez le fichier de classe *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-171">Name the class file *Dal.cs*.</span></span>  <span data-ttu-id="7d7b5-172">Dans *Dal.cs*, remplacez le code existant par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-172">In *Dal.cs*, replace the existing code with the following code:</span></span>

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

## <a name="add-a-controller"></a><span data-ttu-id="7d7b5-173">Ajout d'un contrôleur</span><span class="sxs-lookup"><span data-stu-id="7d7b5-173">Add a controller</span></span>
<span data-ttu-id="7d7b5-174">Ouvrez le fichier *Controllers\HomeController.cs* dans l’**Explorateur de solutions** et remplacez le code existant par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-174">Open the *Controllers\HomeController.cs* file in **Solution Explorer** and replace the existing code with the following:</span></span>

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

## <a name="set-up-the-styles"></a><span data-ttu-id="7d7b5-175">Configuration des styles</span><span class="sxs-lookup"><span data-stu-id="7d7b5-175">Set up the styles</span></span>
<span data-ttu-id="7d7b5-176">Pour changer le titre en haut de la page, ouvrez le fichier *Views\Shared\\_Layout.cshtml* dans l’**Explorateur de solutions** et remplacez « Nom de l’application » dans le titre de la barre de navigation par « Application My Task List » afin d’afficher ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-176">To change the title at the top of the page, open the *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in the navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="7d7b5-177">Pour configurer le menu Liste des tâches, ouvrez le fichier *\Views\Home\Index.cshtml* et remplacez le code existant par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-177">In order to set up the Task List menu, open the *\Views\Home\Index.cshtml* file and replace the existing code with the following code:</span></span>

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


<span data-ttu-id="7d7b5-178">Pour permettre la création d’une tâche, cliquez avec le bouton droit sur le dossier *Views\Home\\* et **ajoutez** une **vue**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-178">To add the ability to create a new task, right-click the *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="7d7b5-179">que vous nommez *Créer*.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-179">Name the view *Create*.</span></span> <span data-ttu-id="7d7b5-180">Remplacez le code par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-180">Replace the code with the following:</span></span>

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

<span data-ttu-id="7d7b5-181">**Explorateur de solutions** doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-181">**Solution Explorer** should look like this:</span></span>

![Explorateur de solutions][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a><span data-ttu-id="7d7b5-183">Configuration de la chaîne de connexion MongoDB</span><span class="sxs-lookup"><span data-stu-id="7d7b5-183">Set the MongoDB connection string</span></span>
<span data-ttu-id="7d7b5-184">Dans l' **Explorateur de solutions**, ouvrez le fichier *DAL/Dal.cs* .</span><span class="sxs-lookup"><span data-stu-id="7d7b5-184">In **Solution Explorer**, open the *DAL/Dal.cs* file.</span></span> <span data-ttu-id="7d7b5-185">Recherchez la ligne de code suivante :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-185">Find the following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="7d7b5-186">Remplacez `<vm-dns-name>` par le nom DNS de la machine virtuelle exécutant MongoDB, que vous avez créée à l’étape [Création d’une machine virtuelle et installation de MongoDB][Create a virtual machine and install MongoDB] de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-186">Replace `<vm-dns-name>` with the DNS name of the virtual machine running MongoDB you created in the [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="7d7b5-187">Pour rechercher le nom DNS de votre machine virtuelle, accédez au portail Azure, sélectionnez **Machines virtuelles** et recherchez **Nom DNS**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-187">To find the DNS name of your virtual machine, go to the Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="7d7b5-188">Si le nom DNS de la machine virtuelle correspond à « testlinuxvm.cloudapp.net » et que MongoDB écoute sur le port par défaut 27017, la ligne de code de la chaîne de connexion se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-188">If the DNS name of the virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on the default port 27017, the connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="7d7b5-189">Si le point de terminaison de la machine virtuelle spécifie un port externe différent pour MongoDB, vous pouvez indiquer ce port dans la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-189">If the virtual machine endpoint specifies a different external port for MongoDB, you can specifiy the port in the connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="7d7b5-190">Pour plus d’informations sur les chaînes de connexion MongoDB, consultez la rubrique [Connections][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="7d7b5-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-the-local-deployment"></a><span data-ttu-id="7d7b5-191">Test du déploiement local</span><span class="sxs-lookup"><span data-stu-id="7d7b5-191">Test the local deployment</span></span>
<span data-ttu-id="7d7b5-192">Pour exécuter l’application sur votre ordinateur de développement, sélectionnez **Démarrer le débogage** dans le menu **Déboguer** ou appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-192">To run your application on your development computer, select **Start Debugging** from the **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="7d7b5-193">IIS Express démarre et un navigateur s'ouvre et lance la page d'accueil de l'application.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-193">IIS Express starts and a browser opens and launches the application's home page.</span></span>  <span data-ttu-id="7d7b5-194">Vous pouvez ajouter une nouvelle tâche qui sera ajoutée à la base de données MongoDB exécutée sur votre machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-194">You can add a new task, which will be added to the MongoDB database running on your virtual machine in Azure.</span></span>

![Application My Task List][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a><span data-ttu-id="7d7b5-196">Publication sur Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="7d7b5-196">Publish to Azure App Service Web Apps</span></span>
<span data-ttu-id="7d7b5-197">Dans cette section, vous allez publier vos modifications apportées à Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-197">In this section you will publish your changes to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="7d7b5-198">Dans l’Explorateur de solutions, cliquez une nouvelle fois avec le bouton droit sur **MyTaskListApp**, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="7d7b5-199">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="7d7b5-200">Votre application Web doit à présent s’exécuter dans Azure App Service et vous devez être en mesure d’accéder à la base de données MongoDB sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-200">You should now see your web app running in Azure App Service and accessing the MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="7d7b5-201">Résumé</span><span class="sxs-lookup"><span data-stu-id="7d7b5-201">Summary</span></span>
<span data-ttu-id="7d7b5-202">Vous avez déployé votre application ASP.NET sur Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-202">You have now successfully deployed your ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="7d7b5-203">Pour afficher l’application Web :</span><span class="sxs-lookup"><span data-stu-id="7d7b5-203">To view the web app:</span></span>

1. <span data-ttu-id="7d7b5-204">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-204">Log into the Azure Portal.</span></span>
2. <span data-ttu-id="7d7b5-205">Cliquez sur **Applications Web**.</span><span class="sxs-lookup"><span data-stu-id="7d7b5-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="7d7b5-206">Sélectionnez votre application Web dans la liste **Applications Web** .</span><span class="sxs-lookup"><span data-stu-id="7d7b5-206">Select your web app in the **Web Apps** list.</span></span>

<span data-ttu-id="7d7b5-207">Pour plus d’informations sur le développement d’applications C# sur MongoDB, reportez-vous à [CSharp Language Center][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="7d7b5-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
