---
title: "aaaCreate une API REST dans Azure avec ASP.NET et la base de données SQL | Documents Microsoft"
description: "Un didacticiel qui vous apprend de comment toodeploy une application qui utilise hello tooan de l’API Web ASP.NET application web Azure à l’aide de Visual Studio."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="67862-103">Créer un service REST à l’aide de l’API Web ASP.NET et de Base de données SQL dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="67862-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="67862-104">Ce didacticiel montre comment toodeploy ASP.NET web application tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en utilisant l’Assistant de publication Web hello dans Visual Studio 2013 ou Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="67862-104">This tutorial shows how toodeploy an ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using hello Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="67862-105">Vous pouvez ouvrir un compte Azure gratuit, et si vous ne disposez pas de Visual Studio 2013, hello SDK installe automatiquement Visual Studio 2013 pour Web Express.</span><span class="sxs-lookup"><span data-stu-id="67862-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, hello SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="67862-106">Vous pouvez donc commencer vos développements Azure gratuitement.</span><span class="sxs-lookup"><span data-stu-id="67862-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="67862-107">Ce didacticiel part du principe que vous n'avez pas d'expérience en tant qu'utilisateur d'Azure.</span><span class="sxs-lookup"><span data-stu-id="67862-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="67862-108">Une fois ce didacticiel, vous avez une application web simple haut et en cours d’exécution dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="67862-108">On completing this tutorial, you'll have a simple web app up and running in hello cloud.</span></span>

<span data-ttu-id="67862-109">Vous apprendrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="67862-109">You'll learn:</span></span>

* <span data-ttu-id="67862-110">Comment tooenable votre ordinateur pour le développement Azure en installant hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="67862-110">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="67862-111">Comment toocreate un Visual Studio ASP.NET MVC 5 du projet et publiez-le tooan application Azure.</span><span class="sxs-lookup"><span data-stu-id="67862-111">How toocreate a Visual Studio ASP.NET MVC 5 project and publish it tooan Azure app.</span></span>
* <span data-ttu-id="67862-112">Appels d’API Restful comment toouse hello tooenable de l’API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="67862-112">How toouse hello ASP.NET Web API tooenable Restful API calls.</span></span>
* <span data-ttu-id="67862-113">Toouse SQL base de données toostore dans Azure.</span><span class="sxs-lookup"><span data-stu-id="67862-113">How toouse a SQL database toostore data in Azure.</span></span>
* <span data-ttu-id="67862-114">Comment toopublish application met à jour tooAzure.</span><span class="sxs-lookup"><span data-stu-id="67862-114">How toopublish application updates tooAzure.</span></span>

<span data-ttu-id="67862-115">Vous allez générer une application web de liste de contacts simple qui repose sur ASP.NET MVC 5 et utilise hello ADO.NET Entity Framework pour l’accès de la base de données.</span><span class="sxs-lookup"><span data-stu-id="67862-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses hello ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="67862-116">Hello suivant illustration montre hello terminé l’application :</span><span class="sxs-lookup"><span data-stu-id="67862-116">hello following illustration shows hello completed application:</span></span>

![capture d’écran du site Web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a><span data-ttu-id="67862-118">Créer le projet de hello</span><span class="sxs-lookup"><span data-stu-id="67862-118">Create hello project</span></span>
1. <span data-ttu-id="67862-119">Démarrez Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="67862-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="67862-120">À partir de hello **fichier** menu, cliquez sur **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="67862-120">From hello **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="67862-121">Bonjour **nouveau projet** boîte de dialogue, développez **Visual C#** et sélectionnez **Web** , puis sélectionnez **Application Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="67862-121">In hello **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="67862-122">Nommez l’application hello **ContactManager** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="67862-122">Name hello application **ContactManager** and click **OK**.</span></span>
   
    ![Boîte de dialogue Nouveau projet](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="67862-124">Bonjour **nouveau projet ASP.NET** boîte de dialogue, sélectionnez hello **MVC** modèle, cocher **API Web** puis cliquez sur **modifier l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="67862-124">In hello **New ASP.NET Project** dialog box, select hello **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="67862-125">Bonjour **modifier l’authentification** boîte de dialogue, cliquez sur **aucune authentification**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="67862-125">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Aucune authentification](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="67862-127">exemple d’application Hello que vous créez ne sont pas ont des fonctionnalités qui nécessitent des toolog d’utilisateurs dans.</span><span class="sxs-lookup"><span data-stu-id="67862-127">hello sample application you're creating won't have features that require users toolog in.</span></span> <span data-ttu-id="67862-128">Pour plus d’informations sur la façon tooimplement des fonctionnalités d’authentification et d’autorisation, consultez hello [étapes](#nextsteps) section à fin hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="67862-128">For information about how tooimplement authentication and authorization features, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
6. <span data-ttu-id="67862-129">Bonjour **nouveau projet ASP.NET** boîte de dialogue, vérifiez les hello que **hôte Bonjour Cloud** est activée et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="67862-129">In hello **New ASP.NET Project** dialog box, make sure hello **Host in hello Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="67862-130">Si vous n’êtes pas déjà inscrit dans tooAzure, vous serez invité à toosign dans.</span><span class="sxs-lookup"><span data-stu-id="67862-130">If you have not previously signed in tooAzure, you will be prompted toosign in.</span></span>

1. <span data-ttu-id="67862-131">Assistant de configuration Hello suggère un nom unique basé sur *ContactManager* (voir l’image hello ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="67862-131">hello configuration wizard will suggest a unique name based on *ContactManager* (see hello image below).</span></span> <span data-ttu-id="67862-132">Sélectionnez une région proche de chez vous.</span><span class="sxs-lookup"><span data-stu-id="67862-132">Select a region near you.</span></span> <span data-ttu-id="67862-133">Vous pouvez utiliser [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") centre de données de latence la plus faible toofind hello.</span><span class="sxs-lookup"><span data-stu-id="67862-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello lowest latency data center.</span></span> 
2. <span data-ttu-id="67862-134">Si vous n’avez pas créé de serveur de base de données, sélectionnez **Créer un serveur**, entrez un nom d’utilisateur et un mot de passe de base de données.</span><span class="sxs-lookup"><span data-stu-id="67862-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Configuration du site Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="67862-136">Si vous avez un serveur de base de données, utilisez ce toocreate une base de données.</span><span class="sxs-lookup"><span data-stu-id="67862-136">If you have a database server, use that toocreate a new database.</span></span> <span data-ttu-id="67862-137">Les serveurs de base de données sont une ressource précieuse, et que vous souhaitez généralement toocreate plusieurs bases de données sur hello même serveur de test et développement au lieu de créer un serveur de base de données par base de données.</span><span class="sxs-lookup"><span data-stu-id="67862-137">Database servers are a precious resource, and you generally want toocreate multiple databases on hello same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="67862-138">Assurez-vous que votre site web et la base de données sont Bonjour même région.</span><span class="sxs-lookup"><span data-stu-id="67862-138">Make sure your web site and database are in hello same region.</span></span>

![Configuration du site Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a><span data-ttu-id="67862-140">Page hello en-tête et pied de page</span><span class="sxs-lookup"><span data-stu-id="67862-140">Set hello page header and footer</span></span>
1. <span data-ttu-id="67862-141">Dans **l’Explorateur de solutions**, développez hello *Views\Shared* dossier et ouvrez hello *_Layout.cshtml* fichier.</span><span class="sxs-lookup"><span data-stu-id="67862-141">In **Solution Explorer**, expand hello *Views\Shared* folder and open hello *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml dans l'Explorateur de solutions][newapp004]
2. <span data-ttu-id="67862-143">Remplacez le contenu hello Hello *Views\Shared_Layout.cshtml* fichier avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="67862-143">Replace hello contents of hello *Views\Shared_Layout.cshtml* file with hello following code:</span></span>

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="67862-144">balisage de Hello au-dessus de nom de l’application hello modifications à partir de « My ASP.NET App » trop « Contact Manager » et il supprime les liens hello trop**accueil**, **sur** et **Contact**.</span><span class="sxs-lookup"><span data-stu-id="67862-144">hello markup above changes hello app name from "My ASP.NET App" too"Contact Manager", and it removes hello links too**Home**, **About** and **Contact**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="67862-145">Exécutez hello application localement</span><span class="sxs-lookup"><span data-stu-id="67862-145">Run hello application locally</span></span>
1. <span data-ttu-id="67862-146">Appuyez sur la touche application de hello toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="67862-146">Press CTRL+F5 toorun hello application.</span></span>
   <span data-ttu-id="67862-147">page d’accueil application Hello s’affiche dans le navigateur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="67862-147">hello application home page appears in hello default browser.</span></span>
    <span data-ttu-id="67862-148">![page d’accueil liste tooDo](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="67862-148">![tooDo List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="67862-149">Cela est que nécessaire pour l’application de hello toocreate maintenant que vous allez déployer tooAzure toodo.</span><span class="sxs-lookup"><span data-stu-id="67862-149">This is all you need toodo for now toocreate hello application that you'll deploy tooAzure.</span></span> <span data-ttu-id="67862-150">Après cela, vous allez ajouter les fonctionnalités de base de données.</span><span class="sxs-lookup"><span data-stu-id="67862-150">Later you'll add database functionality.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="67862-151">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="67862-151">Deploy hello application tooAzure</span></span>
1. <span data-ttu-id="67862-152">Dans Visual Studio, cliquez sur projet hello dans **l’Explorateur de solutions** et sélectionnez **publier** à partir du menu contextuel de hello.</span><span class="sxs-lookup"><span data-stu-id="67862-152">In Visual Studio, right-click hello project in **Solution Explorer** and select **Publish** from hello context menu.</span></span>
   
    ![Publier dans le menu contextuel du projet][PublishVSSolution]
   
    <span data-ttu-id="67862-154">Hello **publier le site Web** Assistant s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="67862-154">hello **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="67862-155">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="67862-155">Click **Publish**.</span></span>

![Onglet Paramètres](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="67862-157">Visual Studio commence le processus hello hello fichiers toohello serveur Azure à copier.</span><span class="sxs-lookup"><span data-stu-id="67862-157">Visual Studio begins hello process of copying hello files toohello Azure server.</span></span> <span data-ttu-id="67862-158">Hello **sortie** fenêtre affiche les actions de déploiement ont été effectuées et signale la réussite du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="67862-158">hello **Output** window shows what deployment actions were taken and reports successful completion of hello deployment.</span></span>

1. <span data-ttu-id="67862-159">navigateur par défaut de Hello ouvre automatiquement toohello les URL du site de hello déployé.</span><span class="sxs-lookup"><span data-stu-id="67862-159">hello default browser automatically opens toohello URL of hello deployed site.</span></span>
   
   <span data-ttu-id="67862-160">application Hello que vous avez créé est en cours d’exécution dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="67862-160">hello application you created is now running in hello cloud.</span></span>
   
   ![page d’accueil liste tooDo s’exécutant dans Azure][rxz2]

## <a name="add-a-database-toohello-application"></a><span data-ttu-id="67862-162">Ajouter une application toohello de base de données</span><span class="sxs-lookup"><span data-stu-id="67862-162">Add a database toohello application</span></span>
<span data-ttu-id="67862-163">Ensuite, vous allez mettre à jour hello MVC application tooadd hello capacité toodisplay et mettre à jour contacts stocker les données de hello dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="67862-163">Next, you'll update hello MVC application tooadd hello ability toodisplay and update contacts and store hello data in a database.</span></span> <span data-ttu-id="67862-164">application Hello utilise tooread et la base de données hello Entity Framework toocreate hello et mettre à jour des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="67862-164">hello application will use hello Entity Framework toocreate hello database and tooread and update data in hello database.</span></span>

### <a name="add-data-model-classes-for-hello-contacts"></a><span data-ttu-id="67862-165">Ajouter des classes de modèle de données pour les contacts de hello</span><span class="sxs-lookup"><span data-stu-id="67862-165">Add data model classes for hello contacts</span></span>
<span data-ttu-id="67862-166">Commencez par créer un modèle de données simple dans le code.</span><span class="sxs-lookup"><span data-stu-id="67862-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="67862-167">Dans **l’Explorateur de solutions**, cliquez sur le dossier de modèles hello, cliquez sur **ajouter**, puis **classe**.</span><span class="sxs-lookup"><span data-stu-id="67862-167">In **Solution Explorer**, right-click hello Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Menu contextuel Ajouter une classe aux modèles][adddb001]
2. <span data-ttu-id="67862-169">Bonjour **ajouter un nouvel élément** boîte de dialogue, le fichier de classe nom hello *Contact.cs*, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="67862-169">In hello **Add New Item** dialog box, name hello new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Boîte de dialogue Ajouter un nouvel élément][adddb002]
3. <span data-ttu-id="67862-171">Remplacez contenu hello du fichier de Contacts.cs hello hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="67862-171">Replace hello contents of hello Contacts.cs file with hello following code.</span></span>
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

<span data-ttu-id="67862-172">Hello **contactez** classe définit les données de hello que vous souhaitez stocker pour chaque contact, plus une clé primaire, ContactID, qui est requise par la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="67862-172">hello **Contact** class defines hello data that you will store for each contact, plus a primary key, ContactID, that is needed by hello database.</span></span> <span data-ttu-id="67862-173">Vous pouvez obtenir plus d’informations sur les modèles de données Bonjour [étapes](#nextsteps) section à fin hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="67862-173">You can get more information about data models in hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a><span data-ttu-id="67862-174">Créer des pages web qui permettent de toowork d’utilisateurs d’application avec des contacts de hello</span><span class="sxs-lookup"><span data-stu-id="67862-174">Create web pages that enable app users toowork with hello contacts</span></span>
<span data-ttu-id="67862-175">Hello fonctionnalité de génération de modèles automatique ASP.NET MVC hello peut générer automatiquement le code qui effectue créer, lire, mettre à jour et supprimer des actions (CRUD).</span><span class="sxs-lookup"><span data-stu-id="67862-175">hello ASP.NET MVC hello scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-hello-data"></a><span data-ttu-id="67862-176">Ajouter un contrôleur et une vue de données de salutation</span><span class="sxs-lookup"><span data-stu-id="67862-176">Add a Controller and a view for hello data</span></span>
1. <span data-ttu-id="67862-177">Dans **l’Explorateur de solutions**, développez le dossier de contrôleurs hello.</span><span class="sxs-lookup"><span data-stu-id="67862-177">In **Solution Explorer**, expand hello Controllers folder.</span></span>
2. <span data-ttu-id="67862-178">Générez le projet de hello **(Ctrl + Maj + B)**.</span><span class="sxs-lookup"><span data-stu-id="67862-178">Build hello project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="67862-179">(Vous devez générer le projet de hello avant d’utiliser le mécanisme de génération de modèles automatique.)</span><span class="sxs-lookup"><span data-stu-id="67862-179">(You must build hello project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="67862-180">Cliquez sur le dossier de contrôleurs hello, sur **ajouter**, puis cliquez sur **contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="67862-180">Right-click hello Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Ajouter un contrôleur dans le menu contextuel du dossier Contrôleurs][addcode001]
4. <span data-ttu-id="67862-182">Bonjour **ajouter une vue de structure** boîte de dialogue, sélectionnez **contrôleur MVC avec vues, utilisant Entity Framework** et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="67862-182">In hello **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Ajouter un contrôleur](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="67862-184">Définir le nom du contrôleur hello trop**HomeController**.</span><span class="sxs-lookup"><span data-stu-id="67862-184">Set hello controller name too**HomeController**.</span></span> <span data-ttu-id="67862-185">Sélectionnez **Contact** comme classe de modèle.</span><span class="sxs-lookup"><span data-stu-id="67862-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="67862-186">Cliquez sur hello **nouveau contexte de données** bouton et acceptez la valeur par défaut de hello « ContactManager.Models.ContactManagerContext » pour hello **nouveau type de contexte de données**.</span><span class="sxs-lookup"><span data-stu-id="67862-186">Click hello **New data context** button and accept hello default "ContactManager.Models.ContactManagerContext" for hello **New data context type**.</span></span> <span data-ttu-id="67862-187">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="67862-187">Click **Add**.</span></span>

    <span data-ttu-id="67862-188">Une boîte de dialogue vous invite à vous : « un fichier portant le nom de hello HomeController existe déjà.</span><span class="sxs-lookup"><span data-stu-id="67862-188">A dialog box will prompt you: "A file with hello name HomeController already exits.</span></span> <span data-ttu-id="67862-189">Voulez-vous vraiment tooreplace il ? ».</span><span class="sxs-lookup"><span data-stu-id="67862-189">Do you want tooreplace it?".</span></span> <span data-ttu-id="67862-190">Cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="67862-190">Click **Yes**.</span></span> <span data-ttu-id="67862-191">Nous sommes remplacement hello contrôleur Home qui a été créé avec un nouveau projet de hello.</span><span class="sxs-lookup"><span data-stu-id="67862-191">We are overwriting hello Home Controller that was created with hello new project.</span></span> <span data-ttu-id="67862-192">Nous allons utiliser hello nouvelle accueil contrôleur pour notre liste de contacts.</span><span class="sxs-lookup"><span data-stu-id="67862-192">We will use hello new Home Controller for our contact list.</span></span>

    <span data-ttu-id="67862-193">Visual Studio crée des méthodes de contrôleur et des vues pour les opérations de base de données CRUD des objets **Contact** .</span><span class="sxs-lookup"><span data-stu-id="67862-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="67862-194">Activer les Migrations, créer la base de données hello, ajouter un initialiseur de données et des exemples de données</span><span class="sxs-lookup"><span data-stu-id="67862-194">Enable Migrations, create hello database, add sample data and a data initializer</span></span>
<span data-ttu-id="67862-195">la tâche suivante Hello est tooenable hello [Migrations Code First](http://curah.microsoft.com/55220) fonctionnalité dans la base de données de commandes toocreate hello en fonction de modèle de données hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="67862-195">hello next task is tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) feature in order toocreate hello database based on hello data model you created.</span></span>

1. <span data-ttu-id="67862-196">Bonjour **outils** menu, sélectionnez **Gestionnaire de Package de bibliothèque** , puis **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="67862-196">In hello **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Console du Gestionnaire de package dans le menu Outils][addcode008]
2. <span data-ttu-id="67862-198">Bonjour **Package Manager Console** fenêtre, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="67862-198">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="67862-199">Hello **enable-migrations** commande crée un *Migrations* dossier et qu’il place dans ce dossier un *Configuration.cs* fichier que vous pouvez modifier les Migrations tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="67862-199">hello **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit tooconfigure Migrations.</span></span> 
3. <span data-ttu-id="67862-200">Bonjour **Package Manager Console** fenêtre, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="67862-200">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="67862-201">Hello **Initial de la migration ajouter** commande génère une classe nommée  **&lt;date_stamp&gt;initiale** qui crée la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="67862-201">hello **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates hello database.</span></span> <span data-ttu-id="67862-202">Hello du premier paramètre ( *initiale* ) nom de hello toocreate arbitraire et utilisé du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="67862-202">hello first parameter ( *Initial* ) is arbitrary and used toocreate hello name of hello file.</span></span> <span data-ttu-id="67862-203">Vous pouvez voir les nouveaux fichiers de classe hello dans **l’Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="67862-203">You can see hello new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="67862-204">Bonjour **initiale** classe hello **des** méthode crée la table Contacts de hello et hello **vers le bas** dépose (méthode) (utilisé lorsque vous souhaitez que l’état précédent de tooreturn toohello).</span><span class="sxs-lookup"><span data-stu-id="67862-204">In hello **Initial** class, hello **Up** method creates hello Contacts table, and hello **Down** method (used when you want tooreturn toohello previous state) drops it.</span></span>
4. <span data-ttu-id="67862-205">Ouvrez hello *Migrations\Configuration.cs* fichier.</span><span class="sxs-lookup"><span data-stu-id="67862-205">Open hello *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="67862-206">Ajoutez hello suivant des espaces de noms.</span><span class="sxs-lookup"><span data-stu-id="67862-206">Add hello following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="67862-207">Remplacez hello *Seed* méthode avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="67862-207">Replace hello *Seed* method with hello following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    <span data-ttu-id="67862-208">Ce code ci-dessus initialisera la base de données de hello avec les informations de contact hello.</span><span class="sxs-lookup"><span data-stu-id="67862-208">This code above will initialize hello database with hello contact information.</span></span> <span data-ttu-id="67862-209">Pour plus d’informations sur la base de données hello l’amorçage, consultez [les bases de données Entity Framework (EF) débogage](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="67862-209">For more information on seeding hello database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="67862-210">Bonjour **Package Manager Console** Entrez la commande hello :</span><span class="sxs-lookup"><span data-stu-id="67862-210">In hello **Package Manager Console** enter hello command:</span></span>
   
        update-database
   
    ![Commandes de la Console du Gestionnaire de package][addcode009]
   
    <span data-ttu-id="67862-212">Hello **mise à jour de la base de données** séries hello première migration qui crée la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="67862-212">hello **update-database** runs hello first migration which creates hello database.</span></span> <span data-ttu-id="67862-213">Par défaut, la base de données de hello est créée en tant qu’une base de données SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="67862-213">By default, hello database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="67862-214">Appuyez sur la touche application de hello toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="67862-214">Press CTRL+F5 toorun hello application.</span></span> 

<span data-ttu-id="67862-215">application Hello affiche les données de valeur initiale hello et fournit les modifier, détails et les liens de suppression.</span><span class="sxs-lookup"><span data-stu-id="67862-215">hello application shows hello seed data and provides edit, details and delete links.</span></span>

![Affichage MVC des données][rxz3]

## <a name="edit-hello-view"></a><span data-ttu-id="67862-217">Modifier hello vue</span><span class="sxs-lookup"><span data-stu-id="67862-217">Edit hello View</span></span>
1. <span data-ttu-id="67862-218">Ouvrez hello *Views\Home\Index.cshtml* fichier.</span><span class="sxs-lookup"><span data-stu-id="67862-218">Open hello *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="67862-219">Dans l’étape suivante de hello, nous remplaçons balisage de hello généré par le code qui utilise [jQuery](http://jquery.com/) et [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="67862-219">In hello next step, we will replace hello generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="67862-220">Ce nouveau code récupère la liste des contacts hello d’à l’aide des API web et JSON, puis lie hello contactez données toohello l’interface utilisateur à l’aide de knockout.js.</span><span class="sxs-lookup"><span data-stu-id="67862-220">This new code retrieves hello list of contacts from using web API and JSON and then binds hello contact data toohello UI using knockout.js.</span></span> <span data-ttu-id="67862-221">Pour plus d’informations, consultez hello [étapes](#nextsteps) section à fin hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="67862-221">For more information, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
2. <span data-ttu-id="67862-222">Remplacez contenu hello du fichier de hello hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="67862-222">Replace hello contents of hello file with hello following code.</span></span>
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. <span data-ttu-id="67862-223">Cliquez sur le dossier de contenu hello, sur **ajouter**, puis cliquez sur **un nouvel élément...** .</span><span class="sxs-lookup"><span data-stu-id="67862-223">Right-click hello Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Ajouter une feuille de style dans le menu contextuel du dossier Contenu][addcode005]
4. <span data-ttu-id="67862-225">Bonjour **ajouter un nouvel élément** boîte de dialogue, entrez **Style** dans hello de zone de recherche du volet supérieur droit, puis sélectionnez **feuille de Style**.</span><span class="sxs-lookup"><span data-stu-id="67862-225">In hello **Add New Item** dialog box, enter **Style** in hello upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="67862-226">![Boîte de dialogue Ajouter un nouvel élément][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="67862-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="67862-227">Nom de fichier hello *Contacts.css* et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="67862-227">Name hello file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="67862-228">Remplacez contenu hello du fichier de hello hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="67862-228">Replace hello contents of hello file with hello following code.</span></span>
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    <span data-ttu-id="67862-229">Nous allons utiliser cette feuille de style pour la mise en page hello, couleurs et styles utilisés dans l’application du Gestionnaire de contacts hello.</span><span class="sxs-lookup"><span data-stu-id="67862-229">We will use this style sheet for hello layout, colors and styles used in hello contact manager app.</span></span>
6. <span data-ttu-id="67862-230">Ouvrez hello *App_Start\BundleConfig.cs* fichier.</span><span class="sxs-lookup"><span data-stu-id="67862-230">Open hello *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="67862-231">Ajouter hello suivant hello tooregister de code [Knockout](http://knockoutjs.com/index.html "KO") plug-in.</span><span class="sxs-lookup"><span data-stu-id="67862-231">Add hello following code tooregister hello [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="67862-232">Cet exemple à l’aide de knockout toosimplify dynamique du code JavaScript qui gère les modèles d’écran hello.</span><span class="sxs-lookup"><span data-stu-id="67862-232">This sample using knockout toosimplify dynamic JavaScript code that handles hello screen templates.</span></span>
8. <span data-ttu-id="67862-233">Modifier hello de hello contenu/css entrée tooregister *contacts.css* feuille de style.</span><span class="sxs-lookup"><span data-stu-id="67862-233">Modify hello contents/css entry tooregister hello *contacts.css* style sheet.</span></span> <span data-ttu-id="67862-234">Modifier hello ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="67862-234">Change hello following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="67862-235">Par :</span><span class="sxs-lookup"><span data-stu-id="67862-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="67862-236">Dans la Console du Gestionnaire de Package de hello, exécutez hello suivant commande tooinstall Knockout.</span><span class="sxs-lookup"><span data-stu-id="67862-236">In hello Package Manager Console, run hello following command tooinstall Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a><span data-ttu-id="67862-237">Ajouter un contrôleur pour l’interface Web API Restful de hello</span><span class="sxs-lookup"><span data-stu-id="67862-237">Add a controller for hello Web API Restful interface</span></span>
1. <span data-ttu-id="67862-238">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur Contrôleurs, cliquez sur **Ajouter**, puis sur **Contrôleur...**</span><span class="sxs-lookup"><span data-stu-id="67862-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="67862-239">Bonjour **ajouter une vue de structure** boîte de dialogue, entrez **Web API 2 contrôleur avec actions, utilisant Entity Framework** puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="67862-239">In hello **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Ajouter un contrôleur API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="67862-241">Bonjour **ajouter un contrôleur** boîte de dialogue, entrez « ContactsController » comme nom de votre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="67862-241">In hello **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="67862-242">Sélectionnez « Contact (ContactManager.Models) » pour hello **classe de modèle**.</span><span class="sxs-lookup"><span data-stu-id="67862-242">Select "Contact (ContactManager.Models)" for hello **Model class**.</span></span>  <span data-ttu-id="67862-243">Conserver la valeur par défaut de hello pour hello **classe de contexte de données**.</span><span class="sxs-lookup"><span data-stu-id="67862-243">Keep hello default value for hello **Data context class**.</span></span> 
4. <span data-ttu-id="67862-244">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="67862-244">Click **Add**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="67862-245">Exécutez hello application localement</span><span class="sxs-lookup"><span data-stu-id="67862-245">Run hello application locally</span></span>
1. <span data-ttu-id="67862-246">Appuyez sur la touche application de hello toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="67862-246">Press CTRL+F5 toorun hello application.</span></span>
   
    ![Page d'index][intro001]
2. <span data-ttu-id="67862-248">Entrez un contact, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="67862-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="67862-249">application Hello retourne la page d’accueil toohello et affiche le contact hello que vous avez entré.</span><span class="sxs-lookup"><span data-stu-id="67862-249">hello app returns toohello home page and displays hello contact you entered.</span></span>
   
    ![Page d'index avec éléments de liste des tâches][addwebapi004]
3. <span data-ttu-id="67862-251">Dans le navigateur de hello, ajoutez **/api/contacts** toohello URL.</span><span class="sxs-lookup"><span data-stu-id="67862-251">In hello browser, append **/api/contacts** toohello URL.</span></span>
   
    <span data-ttu-id="67862-252">les URL qui en résulte Hello ressemblera http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="67862-252">hello resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="67862-253">web RESTful de Hello API que vous avez ajouté retourne les contacts stockée hello.</span><span class="sxs-lookup"><span data-stu-id="67862-253">hello RESTful web API you added returns hello stored contacts.</span></span> <span data-ttu-id="67862-254">Firefox et Chrome affiche les données de salutation au format XML.</span><span class="sxs-lookup"><span data-stu-id="67862-254">Firefox and Chrome will display hello data in XML format.</span></span>
   
    ![Page d'index avec éléments de liste des tâches][rxFFchrome]

    <span data-ttu-id="67862-256">Internet Explorer est vous invite tooopen ou enregistrer les contacts de hello.</span><span class="sxs-lookup"><span data-stu-id="67862-256">IE will prompt you tooopen or save hello contacts.</span></span>

    ![Boîte de dialogue Enregistrer de l'API Web][addwebapi006]


    <span data-ttu-id="67862-258">Vous pouvez ouvrir hello retourné de contacts dans le bloc-notes ou un navigateur.</span><span class="sxs-lookup"><span data-stu-id="67862-258">You can open hello returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="67862-259">Ce résultat peut être utilisé par une autre application, comme une page Web ou une application mobile.</span><span class="sxs-lookup"><span data-stu-id="67862-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Boîte de dialogue Enregistrer de l'API Web][addwebapi007]

    <span data-ttu-id="67862-261">**Avertissement de sécurité**: À ce stade, votre application est non sécurisé et vulnérable tooCSRF attaque.</span><span class="sxs-lookup"><span data-stu-id="67862-261">**Security Warning**: At this point, your application is insecure and vulnerable tooCSRF attack.</span></span> <span data-ttu-id="67862-262">Plus loin dans le didacticiel de hello, nous allons supprimer cette vulnérabilité.</span><span class="sxs-lookup"><span data-stu-id="67862-262">Later in hello tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="67862-263">Pour plus d’informations, consultez la page [Prévention des falsifications de requête intersites][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="67862-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="67862-264">Ajouter une protection XSRF</span><span class="sxs-lookup"><span data-stu-id="67862-264">Add XSRF Protection</span></span>
<span data-ttu-id="67862-265">Falsification de requête (également appelé XSRF ou CSRF) est une attaque contre les applications hébergées par le web dans laquelle un site Web malveillant peut influencer interaction hello entre un navigateur client et un site Web approuvé par ce navigateur.</span><span class="sxs-lookup"><span data-stu-id="67862-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence hello interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="67862-266">Ces attaques sont possible parce que les navigateurs web envoie des jetons d’authentification automatiquement avec tous les sites Web tooa demande.</span><span class="sxs-lookup"><span data-stu-id="67862-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request tooa website.</span></span> <span data-ttu-id="67862-267">exemple Hello est un cookie d’authentification, tels que ASP. Ticket d’authentification par formulaire de NET.</span><span class="sxs-lookup"><span data-stu-id="67862-267">hello canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="67862-268">Cependant, les sites Web utilisant un mécanisme d'authentification persistant (comme l'authentification Windows, Basic, etc.) peuvent être visés par ces attaques.</span><span class="sxs-lookup"><span data-stu-id="67862-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="67862-269">Une attaque XSRF est différente d'une attaque par hameçonnage (ou « phishing »).</span><span class="sxs-lookup"><span data-stu-id="67862-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="67862-270">Des attaques d’hameçonnage requièrent une interaction à partir de la victime de hello.</span><span class="sxs-lookup"><span data-stu-id="67862-270">Phishing attacks require interaction from hello victim.</span></span> <span data-ttu-id="67862-271">Dans une attaque par hameçonnage, un site Web malveillant reflétera le site Web cible de hello et victime de hello est croyez fournissant les intrus de toohello des informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="67862-271">In a phishing attack, a malicious website will mimic hello target website, and hello victim is fooled into providing sensitive information toohello attacker.</span></span> <span data-ttu-id="67862-272">Dans une attaque XSRF, aucune interaction n’est souvent nécessaire de victime de hello.</span><span class="sxs-lookup"><span data-stu-id="67862-272">In an XSRF attack, there is often no interaction necessary from hello victim.</span></span> <span data-ttu-id="67862-273">Au lieu de cela, les intrus hello repose sur navigateur hello envoyer automatiquement le site Web de destination toohello tous les cookies pertinentes.</span><span class="sxs-lookup"><span data-stu-id="67862-273">Rather, hello attacker is relying on hello browser automatically sending all relevant cookies toohello destination website.</span></span>

<span data-ttu-id="67862-274">Pour plus d’informations, consultez hello [ouvrir un projet Web Application sécurité](https://www.owasp.org/index.php/Main_Page) (OWASP avoir) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="67862-274">For more information, see hello [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="67862-275">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet **ContactManager**, cliquez sur **Ajouter**, puis sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="67862-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="67862-276">Nom de fichier hello *ValidateHttpAntiForgeryTokenAttribute.cs* et ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="67862-276">Name hello file *ValidateHttpAntiForgeryTokenAttribute.cs* and add hello following code:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. <span data-ttu-id="67862-277">Ajoutez hello suivant *à l’aide de* toohello d’instruction contrats contrôleur afin que vous ayez accès toohello **[ValidateHttpAntiForgeryToken]** attribut.</span><span class="sxs-lookup"><span data-stu-id="67862-277">Add hello following *using* statement toohello contracts controller so you have access toohello **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="67862-278">Ajouter hello **[ValidateHttpAntiForgeryToken]** toohello des méthodes de publication de hello d’attribut **ContactsController** tooprotect à partir de menaces XSRF.</span><span class="sxs-lookup"><span data-stu-id="67862-278">Add hello **[ValidateHttpAntiForgeryToken]** attribute toohello Post methods of hello **ContactsController** tooprotect it from XSRF threats.</span></span> <span data-ttu-id="67862-279">Vous allez l’ajouter toohello « PutContact », « PostContact » et **DeleteContact** méthodes d’action.</span><span class="sxs-lookup"><span data-stu-id="67862-279">You will add it toohello "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="67862-280">Hello de mise à jour *Scripts* section Hello *Views\Home\Index.cshtml* les jetons XSRF hello tooinclude code tooget de fichiers.</span><span class="sxs-lookup"><span data-stu-id="67862-280">Update hello *Scripts* section of hello *Views\Home\Index.cshtml* file tooinclude code tooget hello XSRF tokens.</span></span>
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a><span data-ttu-id="67862-281">Publier tooAzure de mise à jour d’application hello et la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="67862-281">Publish hello application update tooAzure and SQL Database</span></span>
<span data-ttu-id="67862-282">application de hello toopublish, vous répétez procédure hello que vous avez suivi le plus haut.</span><span class="sxs-lookup"><span data-stu-id="67862-282">toopublish hello application, you repeat hello procedure you followed earlier.</span></span>

1. <span data-ttu-id="67862-283">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet hello et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="67862-283">In **Solution Explorer**, right click hello project and select **Publish**.</span></span>
   
    ![Publier][rxP]
2. <span data-ttu-id="67862-285">Cliquez sur hello **paramètres** onglet.</span><span class="sxs-lookup"><span data-stu-id="67862-285">Click hello **Settings** tab.</span></span>
3. <span data-ttu-id="67862-286">Sous **ContactsManagerContext(ContactsManagerContext)**, cliquez sur hello **v** icône toochange *chaîne de connexion à distance* toohello chaîne de connexion pour le contact de hello base de données.</span><span class="sxs-lookup"><span data-stu-id="67862-286">Under **ContactsManagerContext(ContactsManagerContext)**, click hello **v** icon toochange *Remote connection string* toohello connection string for hello contact database.</span></span> <span data-ttu-id="67862-287">Cliquez sur **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="67862-287">Click **ContactDB**.</span></span>
   
    ![Paramètres](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="67862-289">Case de hello pour **exécuter fonctionnalité Migrations Code First (s’exécute sur le démarrage de l’application)**.</span><span class="sxs-lookup"><span data-stu-id="67862-289">Check hello box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="67862-290">Cliquez sur **Suivant**, puis sur **Aperçu**.</span><span class="sxs-lookup"><span data-stu-id="67862-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="67862-291">Visual Studio affiche une liste de fichiers hello qui seront ajoutés ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="67862-291">Visual Studio displays a list of hello files that will be added or updated.</span></span>
6. <span data-ttu-id="67862-292">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="67862-292">Click **Publish**.</span></span>
   <span data-ttu-id="67862-293">Après déploiement de hello, navigateur de hello ouvre toohello page d’accueil de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="67862-293">After hello deployment completes, hello browser opens toohello home page of hello application.</span></span>
   
    ![Page d'index sans contacts][intro001]
   
    <span data-ttu-id="67862-295">Hello Visual Studio publier la chaîne de connexion de processus configuré automatiquement hello Bonjour déployé *Web.config* base de données de fichier toopoint toohello SQL.</span><span class="sxs-lookup"><span data-stu-id="67862-295">hello Visual Studio publish process automatically configured hello connection string in hello deployed *Web.config* file toopoint toohello SQL database.</span></span> <span data-ttu-id="67862-296">Elle également configurée Migrations Code First tooautomatically hello mise à niveau de base de données toohello version la plus récente hello première heure hello application accède à des base de données hello après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="67862-296">It also configured Code First Migrations tooautomatically upgrade hello database toohello latest version hello first time hello application accesses hello database after deployment.</span></span>
   
    <span data-ttu-id="67862-297">À la suite de cette configuration, Code First créé hello base de données en exécutant du code de hello Bonjour **initiale** classe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="67862-297">As a result of this configuration, Code First created hello database by running hello code in hello **Initial** class that you created earlier.</span></span> <span data-ttu-id="67862-298">Après le déploiement, il a cette hello première hello application a tenté de tooaccess hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="67862-298">It did this hello first time hello application tried tooaccess hello database after deployment.</span></span>
7. <span data-ttu-id="67862-299">Entrez un contact comme vous l’avez fait lors de l’exécution d’application hello localement, tooverify le déploiement de la base de données a réussi.</span><span class="sxs-lookup"><span data-stu-id="67862-299">Enter a contact as you did when you ran hello app locally, tooverify that database deployment succeeded.</span></span>

<span data-ttu-id="67862-300">Lorsque vous voyez cet élément hello que vous entrez est enregistré et s’affiche sur la page du Gestionnaire de contacts hello, vous savez qu’elle a été stockée dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="67862-300">When you see that hello item you enter is saved and appears on hello contact manager page, you know that it has been stored in hello database.</span></span>

![Page d'index avec contacts][addwebapi004]

<span data-ttu-id="67862-302">application Hello est en cours d’exécution dans le cloud de hello, à l’aide de la base de données SQL toostore ses données.</span><span class="sxs-lookup"><span data-stu-id="67862-302">hello application is now running in hello cloud, using SQL Database toostore its data.</span></span> <span data-ttu-id="67862-303">Une fois que vous avez terminé de tester l’application hello dans Azure, supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="67862-303">After you finish testing hello application in Azure, delete it.</span></span> <span data-ttu-id="67862-304">application Hello est publique et n’a pas un mécanisme toolimit.</span><span class="sxs-lookup"><span data-stu-id="67862-304">hello application is public and doesn't have a mechanism toolimit access.</span></span>

> [!NOTE]
> <span data-ttu-id="67862-305">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="67862-305">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="67862-306">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="67862-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="67862-307">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="67862-307">Next Steps</span></span>
<span data-ttu-id="67862-308">Une autre façon dont les données toostore dans une application Windows Azure sont toouse le stockage Azure, qui permettent de stocker des données non relationnelles sous forme de hello d’objets BLOB et tables.</span><span class="sxs-lookup"><span data-stu-id="67862-308">Another way toostore data in an Azure application is toouse Azure storage, which provide non-relational data storage in hello form of blobs and tables.</span></span> <span data-ttu-id="67862-309">Hello suivant liens fournit plus d’informations sur les API Web, ASP.NET MVC et Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="67862-309">hello following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="67862-310">[Mise en route d’Entity Framework avec MVC (en anglais)][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="67862-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="67862-311">Introduction tooASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="67862-311">Intro tooASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="67862-312">Votre première API Web ASP.NET (en anglais)</span><span class="sxs-lookup"><span data-stu-id="67862-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="67862-313">Débogage de WAWS</span><span class="sxs-lookup"><span data-stu-id="67862-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="67862-314">Cet exemple d’application didacticiel et hello a été écrit par [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) avec l’assistance de Tom Dykstra et Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="67862-314">This tutorial and hello sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="67862-315">Veuillez laisser des commentaires sur ce que vous avez aimé ou ce que vous voulez toosee améliorée, non seulement sur didacticiel hello lui-même, mais également sur les produits de hello il montre.</span><span class="sxs-lookup"><span data-stu-id="67862-315">Please leave feedback on what you liked or what you would like toosee improved, not only about hello tutorial itself but also about hello products that it demonstrates.</span></span> <span data-ttu-id="67862-316">Vos commentaires nous aideront à orienter nos améliorations.</span><span class="sxs-lookup"><span data-stu-id="67862-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="67862-317">Nous intéressent particulièrement savoir combien intérêt il est en plus d’automation pour les processus hello de configuration et de déploiement de base de données d’appartenance hello.</span><span class="sxs-lookup"><span data-stu-id="67862-317">We are especially interested in finding out how much interest there is in more automation for hello process of configuring and deploying hello membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="67862-318">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="67862-318">What's changed</span></span>
* <span data-ttu-id="67862-319">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="67862-319">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

