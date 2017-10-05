---
title: "Créer une API REST dans Azure avec ASP.NET et SQL DB | Microsoft Docs"
description: "Didacticiel expliquant comment déployer une application qui utilise l’API Web ASP.NET dans une application web Azure à l’aide de Visual Studio."
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
ms.openlocfilehash: 64c18f2cfabbb7af6ffd89b4c2a9095fca1cf799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="31deb-103">Créer un service REST à l’aide de l’API Web ASP.NET et de Base de données SQL dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="31deb-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="31deb-104">Ce didacticiel explique comment déployer une application Web ASP.NET dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) à l’aide de l’Assistant Publier le site Web de Visual Studio 2013 ou Visual Studio Community 2013.</span><span class="sxs-lookup"><span data-stu-id="31deb-104">This tutorial shows how to deploy an ASP.NET web app to an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using the Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="31deb-105">Vous pouvez ouvrir gratuitement un compte Azure. Si vous n’avez pas déjà Visual Studio 2013, le Kit de développement logiciel (SDK) installe automatiquement Visual Studio Express 2013 pour le Web.</span><span class="sxs-lookup"><span data-stu-id="31deb-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, the SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="31deb-106">Vous pouvez donc commencer vos développements Azure gratuitement.</span><span class="sxs-lookup"><span data-stu-id="31deb-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="31deb-107">Ce didacticiel part du principe que vous n'avez pas d'expérience en tant qu'utilisateur d'Azure.</span><span class="sxs-lookup"><span data-stu-id="31deb-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="31deb-108">À la fin de ce didacticiel, vous disposerez d’une application web simple et fonctionnelle dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="31deb-108">On completing this tutorial, you'll have a simple web app up and running in the cloud.</span></span>

<span data-ttu-id="31deb-109">Vous apprendrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="31deb-109">You'll learn:</span></span>

* <span data-ttu-id="31deb-110">configurer votre ordinateur pour le développement Azure en installant le Kit de développement logiciel (SDK) Azure ;</span><span class="sxs-lookup"><span data-stu-id="31deb-110">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="31deb-111">créer un projet Visual Studio ASP.NET MVC 5 et le publier dans une application Azure ;</span><span class="sxs-lookup"><span data-stu-id="31deb-111">How to create a Visual Studio ASP.NET MVC 5 project and publish it to an Azure app.</span></span>
* <span data-ttu-id="31deb-112">utiliser l'API Web ASP.NET pour activer les appels d'API Restful ;</span><span class="sxs-lookup"><span data-stu-id="31deb-112">How to use the ASP.NET Web API to enable Restful API calls.</span></span>
* <span data-ttu-id="31deb-113">utiliser une base de données SQL pour stocker des données dans Azure ;</span><span class="sxs-lookup"><span data-stu-id="31deb-113">How to use a SQL database to store data in Azure.</span></span>
* <span data-ttu-id="31deb-114">publier des mises à jour d'application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="31deb-114">How to publish application updates to Azure.</span></span>

<span data-ttu-id="31deb-115">Vous développerez une application Web de liste de contacts simple basée sur ASP.NET MVC 5 et utilisant Entity Framework ADO.NET pour accéder à la base de données.</span><span class="sxs-lookup"><span data-stu-id="31deb-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses the ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="31deb-116">L’illustration suivante présente l’application terminée :</span><span class="sxs-lookup"><span data-stu-id="31deb-116">The following illustration shows the completed application:</span></span>

![capture d’écran du site Web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a><span data-ttu-id="31deb-118">Création du projet</span><span class="sxs-lookup"><span data-stu-id="31deb-118">Create the project</span></span>
1. <span data-ttu-id="31deb-119">Démarrez Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="31deb-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="31deb-120">Dans le menu **Fichier**, cliquez sur **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="31deb-120">From the **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="31deb-121">Dans la boîte de dialogue **Nouveau projet**, développez **Visual C#** et sélectionnez **Web**, puis **Application Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="31deb-121">In the **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="31deb-122">Nommez l'application **ContactManager** , puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="31deb-122">Name the application **ContactManager** and click **OK**.</span></span>
   
    ![Boîte de dialogue Nouveau projet](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="31deb-124">Dans la boîte de dialogue **Nouveau projet ASP.NET**, sélectionnez le modèle **MVC**, activez la case à cocher **API Web**, puis cliquez sur **Modifier l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="31deb-124">In the **New ASP.NET Project** dialog box, select the **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="31deb-125">Dans la boîte de dialogue **Modifier l’authentification**, cliquez sur **Aucune authentification**, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="31deb-125">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Aucune authentification](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="31deb-127">L’exemple d’application que vous créez ne sera pas doté de fonctionnalités nécessitant la connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="31deb-127">The sample application you're creating won't have features that require users to log in.</span></span> <span data-ttu-id="31deb-128">Pour plus d’informations sur l’implémentation de fonctionnalités d’authentification et d’autorisation, consultez la section [Étapes suivantes](#nextsteps) à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="31deb-128">For information about how to implement authentication and authorization features, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
6. <span data-ttu-id="31deb-129">Dans la boîte de dialogue **Nouveau projet ASP.NET**, vérifiez que la case **Hôte dans le Cloud** est cochée, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="31deb-129">In the **New ASP.NET Project** dialog box, make sure the **Host in the Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="31deb-130">Si vous n’êtes pas déjà connecté à Azure, vous serez invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="31deb-130">If you have not previously signed in to Azure, you will be prompted to sign in.</span></span>

1. <span data-ttu-id="31deb-131">L’Assistant Configuration suggère un nom unique basé sur *ContactManager* (voir l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="31deb-131">The configuration wizard will suggest a unique name based on *ContactManager* (see the image below).</span></span> <span data-ttu-id="31deb-132">Sélectionnez une région proche de chez vous.</span><span class="sxs-lookup"><span data-stu-id="31deb-132">Select a region near you.</span></span> <span data-ttu-id="31deb-133">Vous pouvez utiliser [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") pour trouver le centre de données affichant la plus faible latence.</span><span class="sxs-lookup"><span data-stu-id="31deb-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") to find the lowest latency data center.</span></span> 
2. <span data-ttu-id="31deb-134">Si vous n’avez pas créé de serveur de base de données, sélectionnez **Créer un serveur**, entrez un nom d’utilisateur et un mot de passe de base de données.</span><span class="sxs-lookup"><span data-stu-id="31deb-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Configuration du site Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="31deb-136">Si vous avez un serveur de bases de données, utilisez-le pour créer une base de données.</span><span class="sxs-lookup"><span data-stu-id="31deb-136">If you have a database server, use that to create a new database.</span></span> <span data-ttu-id="31deb-137">Les serveurs de base de données sont une ressource essentielle, et vous souhaitez généralement créer plusieurs bases de données sur le même serveur à des fins de test et développement au lieu de créer un serveur de base de données par base de données.</span><span class="sxs-lookup"><span data-stu-id="31deb-137">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="31deb-138">Assurez-vous que votre site web et la base de données sont dans la même région.</span><span class="sxs-lookup"><span data-stu-id="31deb-138">Make sure your web site and database are in the same region.</span></span>

![Configuration du site Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a><span data-ttu-id="31deb-140">Définition de l'en-tête et du pied de page de la page</span><span class="sxs-lookup"><span data-stu-id="31deb-140">Set the page header and footer</span></span>
1. <span data-ttu-id="31deb-141">Dans l’**Explorateur de solutions**, développez le dossier *Views\Shared* et ouvrez le fichier *_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="31deb-141">In **Solution Explorer**, expand the *Views\Shared* folder and open the *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml dans l'Explorateur de solutions][newapp004]
2. <span data-ttu-id="31deb-143">Remplacez le contenu du fichier *Views\Shared_Layout.cshtml* par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="31deb-143">Replace the contents of the *Views\Shared_Layout.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="31deb-144">Le balisage ci-dessus remplace le nom de l’application « My ASP.NET App » par « Gestionnaire de contacts » et supprime les liens vers les pages **Accueil**, **À propos de** et **Contact**.</span><span class="sxs-lookup"><span data-stu-id="31deb-144">The markup above changes the app name from "My ASP.NET App" to "Contact Manager", and it removes the links to **Home**, **About** and **Contact**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="31deb-145">Exécution locale de l'application</span><span class="sxs-lookup"><span data-stu-id="31deb-145">Run the application locally</span></span>
1. <span data-ttu-id="31deb-146">Appuyez sur Ctrl+F5 pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="31deb-146">Press CTRL+F5 to run the application.</span></span>
   <span data-ttu-id="31deb-147">La page d’accueil de l’application apparaît dans le navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="31deb-147">The application home page appears in the default browser.</span></span>
    <span data-ttu-id="31deb-148">![Page d’accueil Liste des tâches](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="31deb-148">![To Do List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="31deb-149">Voilà, vous avez fait tout ce qu'il fallait pour créer l'application que vous allez déployer dans Azure.</span><span class="sxs-lookup"><span data-stu-id="31deb-149">This is all you need to do for now to create the application that you'll deploy to Azure.</span></span> <span data-ttu-id="31deb-150">Après cela, vous allez ajouter les fonctionnalités de base de données.</span><span class="sxs-lookup"><span data-stu-id="31deb-150">Later you'll add database functionality.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="31deb-151">Déploiement de l'application dans Azure</span><span class="sxs-lookup"><span data-stu-id="31deb-151">Deploy the application to Azure</span></span>
1. <span data-ttu-id="31deb-152">Dans **l’Explorateur de solutions** de Visual Studio, cliquez avec le bouton droit sur le projet, puis dans le menu contextuel, sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="31deb-152">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    ![Publier dans le menu contextuel du projet][PublishVSSolution]
   
    <span data-ttu-id="31deb-154">L'Assistant **Publier le site Web** s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="31deb-154">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="31deb-155">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="31deb-155">Click **Publish**.</span></span>

![Onglet Paramètres](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="31deb-157">Visual Studio démarre le processus de copie des fichiers vers le serveur Azure.</span><span class="sxs-lookup"><span data-stu-id="31deb-157">Visual Studio begins the process of copying the files to the Azure server.</span></span> <span data-ttu-id="31deb-158">La fenêtre **Output** indique les actions de déploiement entreprises et signale la réussite du déploiement.</span><span class="sxs-lookup"><span data-stu-id="31deb-158">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>

1. <span data-ttu-id="31deb-159">Le navigateur par défaut ouvre automatiquement l'URL du site déployé.</span><span class="sxs-lookup"><span data-stu-id="31deb-159">The default browser automatically opens to the URL of the deployed site.</span></span>
   
   <span data-ttu-id="31deb-160">L'application créée est maintenant exécutée dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="31deb-160">The application you created is now running in the cloud.</span></span>
   
   ![Page d'accueil Liste des tâches exécutée dans Azure][rxz2]

## <a name="add-a-database-to-the-application"></a><span data-ttu-id="31deb-162">Ajout d'une base de données à l'application</span><span class="sxs-lookup"><span data-stu-id="31deb-162">Add a database to the application</span></span>
<span data-ttu-id="31deb-163">À présent, vous allez mettre à jour l'application MVC pour y ajouter la capacité d'afficher et de mettre à jour les contacts, puis stocker les données dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="31deb-163">Next, you'll update the MVC application to add the ability to display and update contacts and store the data in a database.</span></span> <span data-ttu-id="31deb-164">L'application va utiliser Entity Framework pour créer la base de données, ainsi que lire et mettre à jour les données associées.</span><span class="sxs-lookup"><span data-stu-id="31deb-164">The application will use the Entity Framework to create the database and to read and update data in the database.</span></span>

### <a name="add-data-model-classes-for-the-contacts"></a><span data-ttu-id="31deb-165">Ajout de classes de modèle de données pour les contacts</span><span class="sxs-lookup"><span data-stu-id="31deb-165">Add data model classes for the contacts</span></span>
<span data-ttu-id="31deb-166">Commencez par créer un modèle de données simple dans le code.</span><span class="sxs-lookup"><span data-stu-id="31deb-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="31deb-167">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le dossier Modèles, cliquez sur **Ajouter**, puis sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="31deb-167">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Menu contextuel Ajouter une classe aux modèles][adddb001]
2. <span data-ttu-id="31deb-169">Dans la boîte de dialogue **Ajouter un nouvel élément**, nommez le nouveau fichier de classe *Contact.cs*, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31deb-169">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Boîte de dialogue Ajouter un nouvel élément][adddb002]
3. <span data-ttu-id="31deb-171">Remplacez le contenu du fichier Contacts.cs par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31deb-171">Replace the contents of the Contacts.cs file with the following code.</span></span>
   
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

<span data-ttu-id="31deb-172">La classe **Contact** définit les données que vous allez stocker pour chaque contact, ainsi que la clé primaire ContactID dont la base de données a besoin.</span><span class="sxs-lookup"><span data-stu-id="31deb-172">The **Contact** class defines the data that you will store for each contact, plus a primary key, ContactID, that is needed by the database.</span></span> <span data-ttu-id="31deb-173">Pour plus d'informations sur les modèles de données, consultez la section [Étapes suivantes](#nextsteps) à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="31deb-173">You can get more information about data models in the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a><span data-ttu-id="31deb-174">Création de pages Web permettant aux utilisateurs de l'application d'utiliser des contacts</span><span class="sxs-lookup"><span data-stu-id="31deb-174">Create web pages that enable app users to work with the contacts</span></span>
<span data-ttu-id="31deb-175">La fonctionnalité de génération de modèle automatique ASP.NET MVC peut générer automatiquement un code qui effectue les actions CRUD (Create, Read, Update et Delete, ou Créer, Lire, Mettre à jour et Supprimer).</span><span class="sxs-lookup"><span data-stu-id="31deb-175">The ASP.NET MVC the scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-the-data"></a><span data-ttu-id="31deb-176">Ajout d'un contrôleur et affichage des données</span><span class="sxs-lookup"><span data-stu-id="31deb-176">Add a Controller and a view for the data</span></span>
1. <span data-ttu-id="31deb-177">Dans l' **Explorateur de solutions**, développez le dossier Contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="31deb-177">In **Solution Explorer**, expand the Controllers folder.</span></span>
2. <span data-ttu-id="31deb-178">Développez le projet **(Ctrl+Maj+B)**.</span><span class="sxs-lookup"><span data-stu-id="31deb-178">Build the project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="31deb-179">(vous devez développer le projet avant d'utiliser le mécanisme de génération de modèle automatique).</span><span class="sxs-lookup"><span data-stu-id="31deb-179">(You must build the project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="31deb-180">Cliquez avec le bouton droit sur le dossier Contrôleurs, cliquez sur **Ajouter**, puis sur **Contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="31deb-180">Right-click the Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Ajouter un contrôleur dans le menu contextuel du dossier Contrôleurs][addcode001]
4. <span data-ttu-id="31deb-182">Dans la boîte de dialogue **Ajouter une vue de structure**, sélectionnez **Contrôleur MVC avec vues, avec Entity Framework**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31deb-182">In the **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Ajouter un contrôleur](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="31deb-184">Définissez le nom du contrôleur sur **HomeController**.</span><span class="sxs-lookup"><span data-stu-id="31deb-184">Set the controller name to **HomeController**.</span></span> <span data-ttu-id="31deb-185">Sélectionnez **Contact** comme classe de modèle.</span><span class="sxs-lookup"><span data-stu-id="31deb-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="31deb-186">Cliquez sur le bouton **Nouveau contexte de données** et acceptez la valeur par défaut ContactManager.Models.ContactManagerContext pour le champ **Type du nouveau contexte de données**.</span><span class="sxs-lookup"><span data-stu-id="31deb-186">Click the **New data context** button and accept the default "ContactManager.Models.ContactManagerContext" for the **New data context type**.</span></span> <span data-ttu-id="31deb-187">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31deb-187">Click **Add**.</span></span>

    <span data-ttu-id="31deb-188">Une boîte de dialogue affiche le message suivant : « Un fichier ayant le nom HomeController existe déjà.</span><span class="sxs-lookup"><span data-stu-id="31deb-188">A dialog box will prompt you: "A file with the name HomeController already exits.</span></span> <span data-ttu-id="31deb-189">Voulez-vous le remplacer ? ».</span><span class="sxs-lookup"><span data-stu-id="31deb-189">Do you want to replace it?".</span></span> <span data-ttu-id="31deb-190">Cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="31deb-190">Click **Yes**.</span></span> <span data-ttu-id="31deb-191">Nous allons remplacer le contrôleur d'accueil créé avec le nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="31deb-191">We are overwriting the Home Controller that was created with the new project.</span></span> <span data-ttu-id="31deb-192">Nous allons utiliser le nouveau contrôleur d'accueil pour notre liste de contacts.</span><span class="sxs-lookup"><span data-stu-id="31deb-192">We will use the new Home Controller for our contact list.</span></span>

    <span data-ttu-id="31deb-193">Visual Studio crée des méthodes de contrôleur et des vues pour les opérations de base de données CRUD des objets **Contact** .</span><span class="sxs-lookup"><span data-stu-id="31deb-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="31deb-194">Activation des migrations, création de la base de données, ajout d'exemples de données et d'un initialiseur de données</span><span class="sxs-lookup"><span data-stu-id="31deb-194">Enable Migrations, create the database, add sample data and a data initializer</span></span>
<span data-ttu-id="31deb-195">L'étape suivante consiste à activer la fonctionnalité [Migrations Code First](http://curah.microsoft.com/55220) pour créer la base de données en fonction du modèle de données que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="31deb-195">The next task is to enable the [Code First Migrations](http://curah.microsoft.com/55220) feature in order to create the database based on the data model you created.</span></span>

1. <span data-ttu-id="31deb-196">Dans le menu **Outils**, sélectionnez **Gestionnaire de package de bibliothèques**, puis **Console du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="31deb-196">In the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Console du Gestionnaire de package dans le menu Outils][addcode008]
2. <span data-ttu-id="31deb-198">Dans la fenêtre **Console du Gestionnaire de package** , entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="31deb-198">In the **Package Manager Console** window, enter the following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="31deb-199">La commande **enable-migrations** crée un dossier *Migrations* dans lequel elle place un fichier *Configuration.cs* que vous pouvez modifier pour configurer les migrations.</span><span class="sxs-lookup"><span data-stu-id="31deb-199">The **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span></span> 
3. <span data-ttu-id="31deb-200">Dans la fenêtre **Console du Gestionnaire de package** , entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="31deb-200">In the **Package Manager Console** window, enter the following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="31deb-201">La commande **add-migration Initial** génère une classe nommée **&lt;date_stamp&gt;Initial** qui crée la base de données.</span><span class="sxs-lookup"><span data-stu-id="31deb-201">The **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates the database.</span></span> <span data-ttu-id="31deb-202">Le premier paramètre ( *Initial* ) est arbitraire et permet de créer le nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="31deb-202">The first parameter ( *Initial* ) is arbitrary and used to create the name of the file.</span></span> <span data-ttu-id="31deb-203">Les nouveaux fichiers de classe sont affichés dans l' **Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="31deb-203">You can see the new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="31deb-204">Dans la classe **Initial**, la méthode **Up** crée la table des contacts et la méthode **Down** (utilisée lorsque vous voulez revenir à l’état précédent) annule cette table.</span><span class="sxs-lookup"><span data-stu-id="31deb-204">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span></span>
4. <span data-ttu-id="31deb-205">Ouvrez le fichier *Migrations\Configuration.cs*.</span><span class="sxs-lookup"><span data-stu-id="31deb-205">Open the *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="31deb-206">Ajoutez les espaces de noms suivants.</span><span class="sxs-lookup"><span data-stu-id="31deb-206">Add the following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="31deb-207">Remplacez la méthode *Seed* par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="31deb-207">Replace the *Seed* method with the following code:</span></span>
   
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
   
    <span data-ttu-id="31deb-208">Le code ci-dessus initialise la base de données avec les informations de contact.</span><span class="sxs-lookup"><span data-stu-id="31deb-208">This code above will initialize the database with the contact information.</span></span> <span data-ttu-id="31deb-209">Pour plus d'informations sur l'amorçage de la base de données, consultez la page [Débogage des bases de données Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="31deb-209">For more information on seeding the database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="31deb-210">Dans la **Console du Gestionnaire de package** , entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="31deb-210">In the **Package Manager Console** enter the command:</span></span>
   
        update-database
   
    ![Commandes de la Console du Gestionnaire de package][addcode009]
   
    <span data-ttu-id="31deb-212">La commande **update-database** exécute la première migration qui entraîne la création de la base de données.</span><span class="sxs-lookup"><span data-stu-id="31deb-212">The **update-database** runs the first migration which creates the database.</span></span> <span data-ttu-id="31deb-213">Par défaut, la base de données est créée en tant que base de données SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="31deb-213">By default, the database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="31deb-214">Appuyez sur Ctrl+F5 pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="31deb-214">Press CTRL+F5 to run the application.</span></span> 

<span data-ttu-id="31deb-215">L'application affiche les données amorcées, ainsi que des liens pour les modifier, les supprimer ou obtenir des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="31deb-215">The application shows the seed data and provides edit, details and delete links.</span></span>

![Affichage MVC des données][rxz3]

## <a name="edit-the-view"></a><span data-ttu-id="31deb-217">Modifier la vue</span><span class="sxs-lookup"><span data-stu-id="31deb-217">Edit the View</span></span>
1. <span data-ttu-id="31deb-218">Ouvrez le fichier *Views\Home\Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="31deb-218">Open the *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="31deb-219">Dans l’étape suivante, nous allons remplacer le balisage généré par un code utilisant [jQuery](http://jquery.com/) et [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="31deb-219">In the next step, we will replace the generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="31deb-220">Ce nouveau code récupère la liste des contacts à l’aide de l’API web et de JSON, puis relie les données de contact à l’interface utilisateur à l’aide de knockout.js.</span><span class="sxs-lookup"><span data-stu-id="31deb-220">This new code retrieves the list of contacts from using web API and JSON and then binds the contact data to the UI using knockout.js.</span></span> <span data-ttu-id="31deb-221">Pour plus d’informations, consultez la section [Étapes suivantes](#nextsteps) à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="31deb-221">For more information, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
2. <span data-ttu-id="31deb-222">Remplacez le contenu du fichier par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31deb-222">Replace the contents of the file with the following code.</span></span>
   
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
3. <span data-ttu-id="31deb-223">Cliquez avec le bouton droit sur le dossier Contenu, puis cliquez sur **Ajouter** et sur **Nouvel élément...**.</span><span class="sxs-lookup"><span data-stu-id="31deb-223">Right-click the Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Ajouter une feuille de style dans le menu contextuel du dossier Contenu][addcode005]
4. <span data-ttu-id="31deb-225">Dans la boîte de dialogue **Ajouter un nouvel élément**, entrez **Style** dans la zone de recherche située en haut à droite, puis sélectionnez **Feuille de style**.</span><span class="sxs-lookup"><span data-stu-id="31deb-225">In the **Add New Item** dialog box, enter **Style** in the upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="31deb-226">![Boîte de dialogue Ajouter un nouvel élément][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="31deb-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="31deb-227">Nommez le fichier *Contacts.css* , puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31deb-227">Name the file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="31deb-228">Remplacez le contenu du fichier par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31deb-228">Replace the contents of the file with the following code.</span></span>
   
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
   
    <span data-ttu-id="31deb-229">Nous allons utiliser cette feuille de style pour la disposition, les couleurs et les styles de l'application Gestionnaire de contacts.</span><span class="sxs-lookup"><span data-stu-id="31deb-229">We will use this style sheet for the layout, colors and styles used in the contact manager app.</span></span>
6. <span data-ttu-id="31deb-230">Ouvrez le fichier *App_Start\BundleConfig.cs*.</span><span class="sxs-lookup"><span data-stu-id="31deb-230">Open the *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="31deb-231">Ajoutez le code suivant pour inscrire le plug-in [Knockout](http://knockoutjs.com/index.html "KO") .</span><span class="sxs-lookup"><span data-stu-id="31deb-231">Add the following code to register the [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="31deb-232">Cet exemple utilise Knockout pour simplifier le code JavaScript dynamique gérant les modèles d'écran.</span><span class="sxs-lookup"><span data-stu-id="31deb-232">This sample using knockout to simplify dynamic JavaScript code that handles the screen templates.</span></span>
8. <span data-ttu-id="31deb-233">Modifiez l'entrée contents/css pour inscrire la feuille de style *contacts.css* .</span><span class="sxs-lookup"><span data-stu-id="31deb-233">Modify the contents/css entry to register the *contacts.css* style sheet.</span></span> <span data-ttu-id="31deb-234">Remplacez la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="31deb-234">Change the following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="31deb-235">Par :</span><span class="sxs-lookup"><span data-stu-id="31deb-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="31deb-236">Dans la console du Gestionnaire de package, exécutez la commande suivante pour installer Knockout.</span><span class="sxs-lookup"><span data-stu-id="31deb-236">In the Package Manager Console, run the following command to install Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a><span data-ttu-id="31deb-237">Ajouter un contrôleur pour l’interface d’API Web Restful</span><span class="sxs-lookup"><span data-stu-id="31deb-237">Add a controller for the Web API Restful interface</span></span>
1. <span data-ttu-id="31deb-238">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur Contrôleurs, cliquez sur **Ajouter**, puis sur **Contrôleur...**</span><span class="sxs-lookup"><span data-stu-id="31deb-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="31deb-239">Dans la boîte de dialogue **Ajouter une vue de structure**, entrez **Contrôleur API web 2 avec actions, à l’aide d’Entity Framework**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31deb-239">In the **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Ajouter un contrôleur API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="31deb-241">Dans la boîte de dialogue **Ajouter un contrôleur** , nommez votre contrôleur « ContactsController ».</span><span class="sxs-lookup"><span data-stu-id="31deb-241">In the **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="31deb-242">Sélectionnez « Contact (ContactManager.Models) » en tant que **Classe de modèle**.</span><span class="sxs-lookup"><span data-stu-id="31deb-242">Select "Contact (ContactManager.Models)" for the **Model class**.</span></span>  <span data-ttu-id="31deb-243">Conservez la valeur par défaut pour la **classe du contexte des données**.</span><span class="sxs-lookup"><span data-stu-id="31deb-243">Keep the default value for the **Data context class**.</span></span> 
4. <span data-ttu-id="31deb-244">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31deb-244">Click **Add**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="31deb-245">Exécution locale de l'application</span><span class="sxs-lookup"><span data-stu-id="31deb-245">Run the application locally</span></span>
1. <span data-ttu-id="31deb-246">Appuyez sur Ctrl+F5 pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="31deb-246">Press CTRL+F5 to run the application.</span></span>
   
    ![Page d'index][intro001]
2. <span data-ttu-id="31deb-248">Entrez un contact, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31deb-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="31deb-249">L'application revient à la page d'accueil et affiche le contact que vous venez d'entrer.</span><span class="sxs-lookup"><span data-stu-id="31deb-249">The app returns to the home page and displays the contact you entered.</span></span>
   
    ![Page d'index avec éléments de liste des tâches][addwebapi004]
3. <span data-ttu-id="31deb-251">Dans le navigateur, ajoutez **/api/contacts** à l'URL.</span><span class="sxs-lookup"><span data-stu-id="31deb-251">In the browser, append **/api/contacts** to the URL.</span></span>
   
    <span data-ttu-id="31deb-252">L'URL ressemblera alors à http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="31deb-252">The resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="31deb-253">L'API Web RESTful ajoutée revient aux contacts stockés.</span><span class="sxs-lookup"><span data-stu-id="31deb-253">The RESTful web API you added returns the stored contacts.</span></span> <span data-ttu-id="31deb-254">Firefox et Chrome affichent les données au format XML.</span><span class="sxs-lookup"><span data-stu-id="31deb-254">Firefox and Chrome will display the data in XML format.</span></span>
   
    ![Page d'index avec éléments de liste des tâches][rxFFchrome]

    <span data-ttu-id="31deb-256">IE vous invite à ouvrir ou enregistrer les contacts.</span><span class="sxs-lookup"><span data-stu-id="31deb-256">IE will prompt you to open or save the contacts.</span></span>

    ![Boîte de dialogue Enregistrer de l'API Web][addwebapi006]


    <span data-ttu-id="31deb-258">Vous pouvez ouvrir les contacts renvoyés dans le Bloc-notes ou un navigateur.</span><span class="sxs-lookup"><span data-stu-id="31deb-258">You can open the returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="31deb-259">Ce résultat peut être utilisé par une autre application, comme une page Web ou une application mobile.</span><span class="sxs-lookup"><span data-stu-id="31deb-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Boîte de dialogue Enregistrer de l'API Web][addwebapi007]

    <span data-ttu-id="31deb-261">**Avertissement de sécurité**: pour l’instant, votre application n’est pas sécurisée et elle est vulnérable aux falsifications de requête intersites.</span><span class="sxs-lookup"><span data-stu-id="31deb-261">**Security Warning**: At this point, your application is insecure and vulnerable to CSRF attack.</span></span> <span data-ttu-id="31deb-262">Nous résoudrons ce problème plus tard dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="31deb-262">Later in the tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="31deb-263">Pour plus d’informations, consultez la page [Prévention des falsifications de requête intersites][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="31deb-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="31deb-264">Ajouter une protection XSRF</span><span class="sxs-lookup"><span data-stu-id="31deb-264">Add XSRF Protection</span></span>
<span data-ttu-id="31deb-265">Une falsification de requête intersites (également connue sous le nom de XSRF ou CSRF) est une attaque contre des applications hébergées sur le Web durant lesquelles un site Web malveillant peut influencer l'interaction entre un navigateur client et un site Web approuvé par ce navigateur.</span><span class="sxs-lookup"><span data-stu-id="31deb-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence the interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="31deb-266">Ces attaques sont rendues possibles par le fait que les navigateurs Web envoient automatiquement des jetons d'authentification avec chaque requête vers un site Web.</span><span class="sxs-lookup"><span data-stu-id="31deb-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="31deb-267">L'exemple classique est le cookie d'authentification, comme le ticket d'authentification d'ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="31deb-267">The canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="31deb-268">Cependant, les sites Web utilisant un mécanisme d'authentification persistant (comme l'authentification Windows, Basic, etc.) peuvent être visés par ces attaques.</span><span class="sxs-lookup"><span data-stu-id="31deb-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="31deb-269">Une attaque XSRF est différente d'une attaque par hameçonnage (ou « phishing »).</span><span class="sxs-lookup"><span data-stu-id="31deb-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="31deb-270">Les attaques par hameçonnage requièrent une interaction avec la victime.</span><span class="sxs-lookup"><span data-stu-id="31deb-270">Phishing attacks require interaction from the victim.</span></span> <span data-ttu-id="31deb-271">Dans ce genre d'attaque, un site Web malveillant va imiter un site Web cible et la victime est dupée pour fournir des informations sensibles à l'attaquant.</span><span class="sxs-lookup"><span data-stu-id="31deb-271">In a phishing attack, a malicious website will mimic the target website, and the victim is fooled into providing sensitive information to the attacker.</span></span> <span data-ttu-id="31deb-272">Dans une attaque XSRF, il n'y a généralement pas d'interaction avec la victime.</span><span class="sxs-lookup"><span data-stu-id="31deb-272">In an XSRF attack, there is often no interaction necessary from the victim.</span></span> <span data-ttu-id="31deb-273">L’attaquant se repose plutôt sur le fait que le navigateur envoie automatiquement tous les cookies utiles au site Web de destination.</span><span class="sxs-lookup"><span data-stu-id="31deb-273">Rather, the attacker is relying on the browser automatically sending all relevant cookies to the destination website.</span></span>

<span data-ttu-id="31deb-274">Pour plus d’informations, consultez la page [Projet de sécurité d’application web ouvert](https://www.owasp.org/index.php/Main_Page) (ou OWASP pour « Open Web Application Security Project ») (en anglais) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="31deb-274">For more information, see the [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="31deb-275">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet **ContactManager**, cliquez sur **Ajouter**, puis sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="31deb-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="31deb-276">Nommez le fichier *ValidateHttpAntiForgeryTokenAttribute.cs* et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="31deb-276">Name the file *ValidateHttpAntiForgeryTokenAttribute.cs* and add the following code:</span></span>
   
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
3. <span data-ttu-id="31deb-277">Ajoutez l'instruction *using* suivante au contrôleur de contacts pour accéder à l'attribut **[ValidateHttpAntiForgeryToken]** .</span><span class="sxs-lookup"><span data-stu-id="31deb-277">Add the following *using* statement to the contracts controller so you have access to the **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="31deb-278">Ajoutez l’attribut **[ValidateHttpAntiForgeryToken]** aux méthodes Post du **ContactsController** pour le protéger des menaces XSRF.</span><span class="sxs-lookup"><span data-stu-id="31deb-278">Add the **[ValidateHttpAntiForgeryToken]** attribute to the Post methods of the **ContactsController** to protect it from XSRF threats.</span></span> <span data-ttu-id="31deb-279">Vous l’ajouterez aux méthodes d’action « PutContact », « PostContact » et **DeleteContact**.</span><span class="sxs-lookup"><span data-stu-id="31deb-279">You will add it to the "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="31deb-280">Mettez à jour la section *Scripts* du fichier *Views\Home\Index.cshtml* pour inclure le code d’obtention des jetons XSRF.</span><span class="sxs-lookup"><span data-stu-id="31deb-280">Update the *Scripts* section of the *Views\Home\Index.cshtml* file to include code to get the XSRF tokens.</span></span>
   
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

## <a name="publish-the-application-update-to-azure-and-sql-database"></a><span data-ttu-id="31deb-281">Publier la mise à jour de l’application dans Azure et Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="31deb-281">Publish the application update to Azure and SQL Database</span></span>
<span data-ttu-id="31deb-282">Pour publier l'application, répétez la procédure suivie précédemment.</span><span class="sxs-lookup"><span data-stu-id="31deb-282">To publish the application, you repeat the procedure you followed earlier.</span></span>

1. <span data-ttu-id="31deb-283">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet, puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="31deb-283">In **Solution Explorer**, right click the project and select **Publish**.</span></span>
   
    ![Publier][rxP]
2. <span data-ttu-id="31deb-285">Cliquez sur l'onglet **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="31deb-285">Click the **Settings** tab.</span></span>
3. <span data-ttu-id="31deb-286">Sous **ContactsManagerContext(ContactsManagerContext)**, cliquez sur l’icône **v** pour remplacer *Remote connection string* par la chaîne de connexion pour la base de données de contacts.</span><span class="sxs-lookup"><span data-stu-id="31deb-286">Under **ContactsManagerContext(ContactsManagerContext)**, click the **v** icon to change *Remote connection string* to the connection string for the contact database.</span></span> <span data-ttu-id="31deb-287">Cliquez sur **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="31deb-287">Click **ContactDB**.</span></span>
   
    ![Paramètres](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="31deb-289">Activez la case à cocher pour **Execute Code First Migrations (runs on application start)**.</span><span class="sxs-lookup"><span data-stu-id="31deb-289">Check the box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="31deb-290">Cliquez sur **Suivant**, puis sur **Aperçu**.</span><span class="sxs-lookup"><span data-stu-id="31deb-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="31deb-291">Visual Studio affiche une liste des fichiers ajoutés ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="31deb-291">Visual Studio displays a list of the files that will be added or updated.</span></span>
6. <span data-ttu-id="31deb-292">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="31deb-292">Click **Publish**.</span></span>
   <span data-ttu-id="31deb-293">Une fois le déploiement terminé, le navigateur ouvre la page d'accueil de l'application.</span><span class="sxs-lookup"><span data-stu-id="31deb-293">After the deployment completes, the browser opens to the home page of the application.</span></span>
   
    ![Page d'index sans contacts][intro001]
   
    <span data-ttu-id="31deb-295">Le processus de publication Visual Studio a configuré automatiquement la chaîne de connexion du fichier *Web.config* déployé pour qu'elle pointe vers la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="31deb-295">The Visual Studio publish process automatically configured the connection string in the deployed *Web.config* file to point to the SQL database.</span></span> <span data-ttu-id="31deb-296">Il a également configuré les migrations Code First pour mettre automatiquement à niveau la base de données vers la dernière version, dès le premier accès de l'application à la base de données après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="31deb-296">It also configured Code First Migrations to automatically upgrade the database to the latest version the first time the application accesses the database after deployment.</span></span>
   
    <span data-ttu-id="31deb-297">Ainsi, Code First a créé la base de données en exécutant le code de la classe **Initial** que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="31deb-297">As a result of this configuration, Code First created the database by running the code in the **Initial** class that you created earlier.</span></span> <span data-ttu-id="31deb-298">Cela s'est produit lors du premier accès de l'application à la base de données après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="31deb-298">It did this the first time the application tried to access the database after deployment.</span></span>
7. <span data-ttu-id="31deb-299">Entrez un contact comme vous l'avez fait lorsque vous avez exécuté l'application en local, pour vérifier que le déploiement de la base de données est correct.</span><span class="sxs-lookup"><span data-stu-id="31deb-299">Enter a contact as you did when you ran the app locally, to verify that database deployment succeeded.</span></span>

<span data-ttu-id="31deb-300">Lorsque vous constatez que l'élément que vous entrez est enregistré et s'affiche sur la page du Gestionnaire de contacts, vous savez qu'il a été stocké dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="31deb-300">When you see that the item you enter is saved and appears on the contact manager page, you know that it has been stored in the database.</span></span>

![Page d'index avec contacts][addwebapi004]

<span data-ttu-id="31deb-302">L'application est à présent exécutée dans le cloud et utilise la base de données SQL Database pour stocker ses données.</span><span class="sxs-lookup"><span data-stu-id="31deb-302">The application is now running in the cloud, using SQL Database to store its data.</span></span> <span data-ttu-id="31deb-303">Lorsque vous avez fini de tester l'application dans Azure, supprimez-la.</span><span class="sxs-lookup"><span data-stu-id="31deb-303">After you finish testing the application in Azure, delete it.</span></span> <span data-ttu-id="31deb-304">L'application est publique et ne dispose pas de mécanismes permettant d'en limiter l'accès.</span><span class="sxs-lookup"><span data-stu-id="31deb-304">The application is public and doesn't have a mechanism to limit access.</span></span>

> [!NOTE]
> <span data-ttu-id="31deb-305">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="31deb-305">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="31deb-306">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="31deb-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="31deb-307">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31deb-307">Next Steps</span></span>
<span data-ttu-id="31deb-308">Une autre méthode pour stocker des données dans une application Azure consiste à utiliser le stockage Azure, qui permet de stocker des données non relationnelles sous la forme d'objets blob et de tables.</span><span class="sxs-lookup"><span data-stu-id="31deb-308">Another way to store data in an Azure application is to use Azure storage, which provide non-relational data storage in the form of blobs and tables.</span></span> <span data-ttu-id="31deb-309">Pour plus d'informations sur les API Web, ASP.NET MVC et Microsoft Azure, consultez les liens suivants.</span><span class="sxs-lookup"><span data-stu-id="31deb-309">The following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="31deb-310">[Mise en route d’Entity Framework avec MVC (en anglais)][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="31deb-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="31deb-311">Introduction à ASP.NET MVC 5 (en anglais)</span><span class="sxs-lookup"><span data-stu-id="31deb-311">Intro to ASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="31deb-312">Votre première API Web ASP.NET (en anglais)</span><span class="sxs-lookup"><span data-stu-id="31deb-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="31deb-313">Débogage de WAWS</span><span class="sxs-lookup"><span data-stu-id="31deb-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="31deb-314">Ce didacticiel et son exemple d’application ont été écrits par [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) avec l’aide de Tom Dykstra et Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="31deb-314">This tutorial and the sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="31deb-315">N'hésitez pas à nous transmettre vos commentaires sur ce qui vous a plu et ce qui pourrait être amélioré... pas seulement à propos de ce didacticiel, mais aussi en ce qui concerne les produits présentés ici.</span><span class="sxs-lookup"><span data-stu-id="31deb-315">Please leave feedback on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span></span> <span data-ttu-id="31deb-316">Vos commentaires nous aideront à orienter nos améliorations.</span><span class="sxs-lookup"><span data-stu-id="31deb-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="31deb-317">Nous aimerions particulièrement savoir si l'automatisation du processus de configuration et de déploiement de la base de données d'appartenance vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="31deb-317">We are especially interested in finding out how much interest there is in more automation for the process of configuring and deploying the membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="31deb-318">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="31deb-318">What's changed</span></span>
* <span data-ttu-id="31deb-319">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="31deb-319">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles to the Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2
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

