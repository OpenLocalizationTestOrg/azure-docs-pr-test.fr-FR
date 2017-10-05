---
title: "Prise en main des services cloud Azure et d’ASP.NET | Microsoft Docs"
description: "Découvrez comment créer une application multiniveau avec ASP.NET MVC et Azure. L'application s'exécute dans un service cloud, avec un rôle web et un rôle de travail. Elle utilise Entity Framework, Base de données SQL et les files d'attente et objets blobs du stockage Azure."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: d2c197db73477d06d86d1c4faa8c4a2f58c7b391
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="7b7de-105">Prise en main des services cloud Azure et d'ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7b7de-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="7b7de-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7b7de-106">Overview</span></span>
<span data-ttu-id="7b7de-107">Ce didacticiel explique comment créer une application .NET multiniveau avec un composant frontal ASP.NET MVC et comment la déployer sur un [service cloud Azure](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="7b7de-107">This tutorial shows how to create a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it to an [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="7b7de-108">L’application utilise la [Base de données SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), le [service Blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage) et le [service de File d'attente Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="7b7de-108">The application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), the [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and the [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="7b7de-109">Vous pouvez [télécharger le projet Visual Studio](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) dans la galerie de code MSDN.</span><span class="sxs-lookup"><span data-stu-id="7b7de-109">You can [download the Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from the MSDN Code Gallery.</span></span>

<span data-ttu-id="7b7de-110">Le didacticiel vous apprend à générer et à exécuter l’application localement, à la déployer dans Azure, à l’exécuter dans le cloud et à la générer intégralement.</span><span class="sxs-lookup"><span data-stu-id="7b7de-110">The tutorial shows you how to build and run the application locally, how to deploy it to Azure and run in the cloud, and how to build it from scratch.</span></span> <span data-ttu-id="7b7de-111">Vous pouvez également démarrer à partir de zéro, puis effectuer les tests et le déploiement par la suite.</span><span class="sxs-lookup"><span data-stu-id="7b7de-111">You can start by building from scratch and then do the test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="7b7de-112">Application Contoso Ads</span><span class="sxs-lookup"><span data-stu-id="7b7de-112">Contoso Ads application</span></span>
<span data-ttu-id="7b7de-113">L'application est un panneau d'affichage publicitaire.</span><span class="sxs-lookup"><span data-stu-id="7b7de-113">The application is an advertising bulletin board.</span></span> <span data-ttu-id="7b7de-114">Les utilisateurs créent une publicité en entrant du texte et en téléchargeant une image.</span><span class="sxs-lookup"><span data-stu-id="7b7de-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="7b7de-115">Ils peuvent voir une liste de publicités avec des images en miniature qu’ils peuvent agrandir en sélectionnant la publicité de leur choix.</span><span class="sxs-lookup"><span data-stu-id="7b7de-115">They can see a list of ads with thumbnail images, and they can see the full-size image when they select an ad to see the details.</span></span>

![Ad list](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="7b7de-117">L'application utilise le [modèle de travail centré sur les files d'attente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) pour décharger le travail de création de vignettes exigeant en ressources vers un processus principal.</span><span class="sxs-lookup"><span data-stu-id="7b7de-117">The application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="7b7de-118">Autre architecture : Sites Web et WebJobs</span><span class="sxs-lookup"><span data-stu-id="7b7de-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="7b7de-119">Ce didacticiel indique comment exécuter le composant frontal et le composant principal dans un service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-119">This tutorial shows how to run both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="7b7de-120">Une alternative consiste à exécuter le composant frontal dans un [site web Azure](/services/web-sites/) et à utiliser la fonctionnalité [Tâches web](http://go.microsoft.com/fwlink/?LinkId=390226) (actuellement en version préliminaire) pour le composant principal.</span><span class="sxs-lookup"><span data-stu-id="7b7de-120">An alternative is to run the front-end in an [Azure website](/services/web-sites/) and use the [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for the back-end.</span></span> <span data-ttu-id="7b7de-121">Pour un didacticiel qui utilise Tâches web, reportez-vous à la section [Prise en main du Kit de développement logiciel (SDK) Azure Tâches web](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7b7de-121">For a tutorial that uses WebJobs, see [Get Started with the Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="7b7de-122">Pour plus d'informations sur le choix des meilleurs services pour votre scénario, reportez-vous à la rubrique [Comparaison entre Sites Web Azure, Azure Cloud Services et Azure Virtual Machines](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="7b7de-122">For information about how to choose the services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="7b7de-123">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="7b7de-123">What you'll learn</span></span>
* <span data-ttu-id="7b7de-124">configurer votre ordinateur pour le développement Azure en installant le Kit de développement logiciel (SDK) Azure ;</span><span class="sxs-lookup"><span data-stu-id="7b7de-124">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="7b7de-125">créer un service de projet cloud Visual Studio avec un rôle web et un rôle de travail ASP.NET MVC ;</span><span class="sxs-lookup"><span data-stu-id="7b7de-125">How to create a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="7b7de-126">tester localement le projet de service cloud en utilisant l'émulateur de stockage Azure ;</span><span class="sxs-lookup"><span data-stu-id="7b7de-126">How to test the cloud service project locally, using the Azure storage emulator.</span></span>
* <span data-ttu-id="7b7de-127">publier le projet cloud dans un service cloud Azure et le tester avec un compte de stockage Azure ;</span><span class="sxs-lookup"><span data-stu-id="7b7de-127">How to publish the cloud project to an Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="7b7de-128">télécharger des fichiers et les stocker dans le service Blob Azure ;</span><span class="sxs-lookup"><span data-stu-id="7b7de-128">How to upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="7b7de-129">utiliser le service de File d'attente Azure pour la communication entre tiers.</span><span class="sxs-lookup"><span data-stu-id="7b7de-129">How to use the Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b7de-130">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7b7de-130">Prerequisites</span></span>
<span data-ttu-id="7b7de-131">Pour utiliser ce didacticiel, vous devez maîtriser les [concepts de base des services cloud Azure](cloud-services-choose-me.md) et la terminologie afférente, par exemple les *rôles web* et *rôles de travail*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-131">The tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="7b7de-132">Vous devez également savoir utiliser les projets [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) ou [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b7de-132">It also assumes that you know how to work with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="7b7de-133">L’exemple d’application utilise MVC, mais une grande part du didacticiel concerne également Web Forms.</span><span class="sxs-lookup"><span data-stu-id="7b7de-133">The sample application uses MVC, but most of the tutorial also applies to Web Forms.</span></span>

<span data-ttu-id="7b7de-134">Vous pouvez exécuter l’application localement sans abonnement Azure, mais il vous en faut un pour déployer l’application dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-134">You can run the app locally without an Azure subscription, but you'll need one to deploy the application to the cloud.</span></span> <span data-ttu-id="7b7de-135">Si vous n’avez pas de compte, vous pouvez [activer les avantages de votre abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) ou [demander une évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="7b7de-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="7b7de-136">Les instructions du didacticiel sont valables pour les produits suivants :</span><span class="sxs-lookup"><span data-stu-id="7b7de-136">The tutorial instructions work with either of the following products:</span></span>

* <span data-ttu-id="7b7de-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7b7de-137">Visual Studio 2013</span></span>
* <span data-ttu-id="7b7de-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7b7de-138">Visual Studio 2015</span></span>
* <span data-ttu-id="7b7de-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7b7de-139">Visual Studio 2017</span></span>

<span data-ttu-id="7b7de-140">En l’absence d’un de ces produits, Visual Studio sera automatiquement installé à l’occasion de l’installation du kit de développement logiciel Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-140">If you don't have one of these, Visual Studio may be installed automatically when you install the Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="7b7de-141">Architecture de l'application</span><span class="sxs-lookup"><span data-stu-id="7b7de-141">Application architecture</span></span>
<span data-ttu-id="7b7de-142">L'application stocke les publicités dans une base de données SQL et utilise Entity Framework Code First pour créer les tables et accéder aux données.</span><span class="sxs-lookup"><span data-stu-id="7b7de-142">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="7b7de-143">Pour chaque publicité, la base de données stocke deux URL, une pour l’image à taille réelle et l’autre pour la miniature.</span><span class="sxs-lookup"><span data-stu-id="7b7de-143">For each ad, the database stores two URLs, one for the full-size image and one for the thumbnail.</span></span>

![Ad table](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="7b7de-145">Lorsqu'un utilisateur télécharge une image, l'application frontale qui s'exécute dans un rôle web la stocke dans un [objet blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), et stocke les informations de la publicité dans la base de données avec une URL qui pointe vers l'objet blob.</span><span class="sxs-lookup"><span data-stu-id="7b7de-145">When a user uploads an image, the front-end running in a web role stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="7b7de-146">En même temps, il écrit un message dans une file d'attente Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-146">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="7b7de-147">Un processus principal qui s'exécute dans un rôle de travail interroge périodiquement la file d'attente pour connaître les nouveaux messages.</span><span class="sxs-lookup"><span data-stu-id="7b7de-147">A back-end process running in a worker role periodically polls the queue for new messages.</span></span> <span data-ttu-id="7b7de-148">Lorsqu'un nouveau message arrive, le rôle de travail crée une vignette pour cette image et met à jour le champ de la base de données des URL des vignettes pour cette publicité.</span><span class="sxs-lookup"><span data-stu-id="7b7de-148">When a new message appears, the worker role creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="7b7de-149">Le diagramme suivant montre l'interaction des parties de l'application.</span><span class="sxs-lookup"><span data-stu-id="7b7de-149">The following diagram shows how the parts of the application interact.</span></span>

![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-the-completed-solution"></a><span data-ttu-id="7b7de-151">Téléchargement et exécution de la solution terminée</span><span class="sxs-lookup"><span data-stu-id="7b7de-151">Download and run the completed solution</span></span>
1. <span data-ttu-id="7b7de-152">Téléchargez et décompressez la [solution terminée](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="7b7de-152">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="7b7de-153">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b7de-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="7b7de-154">Dans le menu **Fichier**, choisissez **Ouvrir un projet**, accédez à l’emplacement où vous avez téléchargé la solution, puis ouvrez le fichier de solution.</span><span class="sxs-lookup"><span data-stu-id="7b7de-154">From the **File** menu choose **Open Project**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="7b7de-155">Appuyez sur Ctrl+Maj+B pour générer la solution.</span><span class="sxs-lookup"><span data-stu-id="7b7de-155">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="7b7de-156">Par défaut, Visual Studio restaure automatiquement le contenu du package NuGet, qui n'était pas inclus dans le fichier *.zip* .</span><span class="sxs-lookup"><span data-stu-id="7b7de-156">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="7b7de-157">Si les packages ne sont pas restaurés, installez-les manuellement en ouvrant la boîte de dialogue **Gérer les packages NuGet pour la solution** et en cliquant sur le bouton **Restaurer** en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="7b7de-157">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog box and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="7b7de-158">Dans **l’Explorateur de solutions**, assurez-vous que **ContosoAdsCloudService** est sélectionné comme projet de démarrage.</span><span class="sxs-lookup"><span data-stu-id="7b7de-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as the startup project.</span></span>
6. <span data-ttu-id="7b7de-159">Si vous utilisez Visual Studio 2015 ou version ultérieure, modifiez la chaîne de connexion SQL Server dans le fichier d’application *Web.config* du projet ContosoAdsWeb et dans le fichier *ServiceConfiguration.Local.cscfg* du projet ContosoAdsCloudService.</span><span class="sxs-lookup"><span data-stu-id="7b7de-159">If you're using Visual Studio 2015 or higher, change the SQL Server connection string in the application *Web.config* file of the ContosoAdsWeb project and in the *ServiceConfiguration.Local.cscfg* file of the ContosoAdsCloudService project.</span></span> <span data-ttu-id="7b7de-160">Dans tous les cas, changez « (localdb) \v11.0 » en « (localdb) \MSSQLLocalDB ».</span><span class="sxs-lookup"><span data-stu-id="7b7de-160">In each case, change "(localdb)\v11.0" to "(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="7b7de-161">Appuyez sur Ctrl+F5 pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="7b7de-161">Press CTRL+F5 to run the application.</span></span>

    <span data-ttu-id="7b7de-162">Lorsque vous exécutez un projet de service cloud localement, Visual Studio appelle automatiquement *l’émulateur de calcul* Azure et *l’émulateur de stockage* Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-162">When you run a cloud service project locally, Visual Studio automatically invokes the Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="7b7de-163">L'émulateur de calcul utilise les ressources de votre ordinateur pour simuler les environnements de rôle Web et de rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="7b7de-163">The compute emulator uses your computer's resources to simulate the web role and worker role environments.</span></span> <span data-ttu-id="7b7de-164">L'émulateur de stockage utilise une base de données [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) pour simuler le stockage sur le cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-164">The storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database to simulate Azure cloud storage.</span></span>

    <span data-ttu-id="7b7de-165">À la première exécution d'un projet de service cloud, le démarrage des émulateurs prend une ou deux minutes.</span><span class="sxs-lookup"><span data-stu-id="7b7de-165">The first time you run a cloud service project, it takes a minute or so for the emulators to start up.</span></span> <span data-ttu-id="7b7de-166">Après le démarrage de l'émulateur, le navigateur par défaut s'ouvre sur la page d'accueil de l'application.</span><span class="sxs-lookup"><span data-stu-id="7b7de-166">When emulator startup is finished, the default browser opens to the application home page.</span></span>

    ![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="7b7de-168">Cliquez sur **Créer une publicité**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="7b7de-169">Entrez des données de test et sélectionnez une image *.jpg* à télécharger, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-169">Enter some test data and select a *.jpg* image to upload, and then click **Create**.</span></span>

    ![Create page](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="7b7de-171">L’application ouvre la page Index, mais n’affiche pas de miniature pour la nouvelle publicité, car le processus n’a pas encore eu lieu.</span><span class="sxs-lookup"><span data-stu-id="7b7de-171">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="7b7de-172">Attendez un instant, puis actualisez la page Index pour afficher la vignette.</span><span class="sxs-lookup"><span data-stu-id="7b7de-172">Wait a moment and then refresh the Index page to see the thumbnail.</span></span>

     ![Page d'index](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="7b7de-174">Cliquez sur l'option **Détails** de votre publicité pour afficher l'image intégrale.</span><span class="sxs-lookup"><span data-stu-id="7b7de-174">Click **Details** for your ad to see the full-size image.</span></span>

     ![Details page](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="7b7de-176">Vous avez exécuté l'application intégralement sur l'ordinateur local, sans connexion au cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-176">You've been running the application entirely on your local computer, with no connection to the cloud.</span></span> <span data-ttu-id="7b7de-177">L'émulateur de stockage stocke la file d'attente et les données blob dans une base de données SQL Server Express LocalDB, et l'application stocke les données de la publicité dans une autre base de données LocalDB.</span><span class="sxs-lookup"><span data-stu-id="7b7de-177">The storage emulator stores the queue and blob data in a SQL Server Express LocalDB database, and the application stores the ad data in another LocalDB database.</span></span> <span data-ttu-id="7b7de-178">Entity Framework Code First crée automatiquement la base de données de publicités lorsque l'application web essaie pour la première fois d'y accéder.</span><span class="sxs-lookup"><span data-stu-id="7b7de-178">Entity Framework Code First automatically created the ad database the first time the web app tried to access it.</span></span>

<span data-ttu-id="7b7de-179">Dans la section suivante, vous allez configurer la solution pour utiliser les ressources de cloud Azure pour les files d'attente, les objets blob et la base de données d'application lorsqu'elle est exécutée dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-179">In the following section you'll configure the solution to use Azure cloud resources for queues, blobs, and the application database when it runs in the cloud.</span></span> <span data-ttu-id="7b7de-180">Si vous souhaitiez continuer à l’exécuter localement, mais utiliser des ressources de stockage cloud et de base de données, vous pourriez le faire.</span><span class="sxs-lookup"><span data-stu-id="7b7de-180">If you wanted to continue to run locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="7b7de-181">Il suffit de définir des chaînes de connexion, ce que nous allez apprendre à faire.</span><span class="sxs-lookup"><span data-stu-id="7b7de-181">It's just a matter of setting connection strings, which you'll see how to do.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="7b7de-182">Déploiement de l'application dans Azure</span><span class="sxs-lookup"><span data-stu-id="7b7de-182">Deploy the application to Azure</span></span>
<span data-ttu-id="7b7de-183">Pour exécuter l'application dans le cloud, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7b7de-183">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="7b7de-184">Créez un service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="7b7de-185">Créez une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="7b7de-186">Créez un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="7b7de-187">Configurez la solution pour utiliser votre base de données SQL Azure lorsqu'elle est exécutée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-187">Configure the solution to use your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="7b7de-188">Configurez la solution pour utiliser votre compte de stockage Azure lorsqu'il est exécuté dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-188">Configure the solution to use your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="7b7de-189">Déployez le projet dans votre service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-189">Deploy the project to your Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="7b7de-190">Création d'un service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="7b7de-190">Create an Azure cloud service</span></span>
<span data-ttu-id="7b7de-191">Un service cloud Azure est l'environnement dans lequel l'application s'exécute.</span><span class="sxs-lookup"><span data-stu-id="7b7de-191">An Azure cloud service is the environment the application will run in.</span></span>

1. <span data-ttu-id="7b7de-192">Dans votre navigateur, ouvrez le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b7de-192">In your browser, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7b7de-193">Cliquez sur **Nouveau > Compute > Service cloud**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="7b7de-194">Dans la zone de saisie du nom DNS, entrez un préfixe d’URL pour le service cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-194">In the DNS name input box, enter a URL prefix for the cloud service.</span></span>

    <span data-ttu-id="7b7de-195">Cette URL doit être unique.</span><span class="sxs-lookup"><span data-stu-id="7b7de-195">This URL has to be unique.</span></span>  <span data-ttu-id="7b7de-196">Un message d’erreur s’affiche si le préfixe que vous choisissez est déjà utilisé.</span><span class="sxs-lookup"><span data-stu-id="7b7de-196">You'll get an error message if the prefix you choose is already in use.</span></span>
4. <span data-ttu-id="7b7de-197">Spécifiez un nouveau groupe de ressources ou le service.</span><span class="sxs-lookup"><span data-stu-id="7b7de-197">Specify a new Resource group for the  service.</span></span> <span data-ttu-id="7b7de-198">Cliquez sur **Créer** puis tapez un nom dans la zone de saisie du groupe de ressources, CS_contososadsRG par exemple.</span><span class="sxs-lookup"><span data-stu-id="7b7de-198">Click **Create new** and then type a name in the Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="7b7de-199">Choisissez la région dans laquelle vous souhaitez déployer l'application.</span><span class="sxs-lookup"><span data-stu-id="7b7de-199">Choose the region where you want to deploy the application.</span></span>

    <span data-ttu-id="7b7de-200">Ce champ indique le centre de données dans lequel votre service cloud sera hébergé.</span><span class="sxs-lookup"><span data-stu-id="7b7de-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="7b7de-201">Pour une application de production, vous devriez choisir la région la plus proche de vos clients.</span><span class="sxs-lookup"><span data-stu-id="7b7de-201">For a production application, you'd choose the region closest to your customers.</span></span> <span data-ttu-id="7b7de-202">Pour ce didacticiel, choisissez la région la plus proche de vous.</span><span class="sxs-lookup"><span data-stu-id="7b7de-202">For this tutorial, choose the region closest to you.</span></span>
5. <span data-ttu-id="7b7de-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-203">Click **Create**.</span></span>

    <span data-ttu-id="7b7de-204">Dans l’image suivante, un service cloud est créé avec l’URL CSvccontosoads.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="7b7de-204">In the following image, a cloud service is created with the URL CSvccontosoads.cloudapp.net.</span></span>

    ![New Cloud Service](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="7b7de-206">Création d’une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7b7de-206">Create an Azure SQL database</span></span>
<span data-ttu-id="7b7de-207">Lorsque l'application s'exécute dans le cloud, elle utilise une base de données basée sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-207">When the app runs in the cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="7b7de-208">Dans le [portail Azure](https://portal.azure.com), cliquez sur **Nouveau > Bases de données > SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-208">In the [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="7b7de-209">Dans la zone **Nom de la base de données** , entrez *contosoads*</span><span class="sxs-lookup"><span data-stu-id="7b7de-209">In the **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="7b7de-210">Dans le **Groupe de ressources**, cliquez sur **Use existing** (Utiliser existant) et sélectionnez le groupe de ressources utilisé pour le service cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-210">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
4. <span data-ttu-id="7b7de-211">Dans l’image suivante, cliquez sur **Serveur - Configurer les paramètres requis** et sur **Créer un serveur**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-211">In the following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Tunnel vers un serveur de base de données](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="7b7de-213">Si votre abonnement a déjà un serveur, vous pouvez le sélectionner dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="7b7de-213">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span></span>
5. <span data-ttu-id="7b7de-214">Dans la zone **Nom du serveur**, entrez *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-214">In the **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="7b7de-215">Entrez un **Nom de connexion** et un **Mot de passe** d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7b7de-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="7b7de-216">Si vous avez sélectionné **Créer un serveur**, vous ne devez pas entrer un nom et un mot de passe existants ici.</span><span class="sxs-lookup"><span data-stu-id="7b7de-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="7b7de-217">Vous entrez de nouveaux nom et mot de passe que vous définissez maintenant pour les utiliser ultérieurement lorsque vous accédez à la base de données.</span><span class="sxs-lookup"><span data-stu-id="7b7de-217">You're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="7b7de-218">Si vous avez sélectionné un serveur créé auparavant, vous devez entrer le mot de passe du compte d’utilisateur administratif déjà créé.</span><span class="sxs-lookup"><span data-stu-id="7b7de-218">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span></span>
7. <span data-ttu-id="7b7de-219">Choisissez le même **Emplacement** que celui choisi pour le service cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-219">Choose the same **Location** that you chose for the cloud service.</span></span>

    <span data-ttu-id="7b7de-220">Lorsque le service cloud et la base de données se trouvent dans des centres de données différents (différentes régions), la latence augmente et la bande passante en dehors du centre de données vous est facturée,</span><span class="sxs-lookup"><span data-stu-id="7b7de-220">When the cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="7b7de-221">alors qu'elle est gratuite dans un centre de données.</span><span class="sxs-lookup"><span data-stu-id="7b7de-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="7b7de-222">Cochez **Autoriser les services Azure à accéder au serveur**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-222">Check **Allow azure services to access server**.</span></span>
9. <span data-ttu-id="7b7de-223">Cliquez sur **Sélectionner** pour le nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="7b7de-223">Click **Select** for the new server.</span></span>

    ![Nouveau serveur SQL Database](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="7b7de-225">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="7b7de-226">Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="7b7de-226">Create an Azure storage account</span></span>
<span data-ttu-id="7b7de-227">Un compte de stockage Azure fournit des ressources pour stocker les données de file d'attente et d'objet blob dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-227">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span>

<span data-ttu-id="7b7de-228">Dans une application réelle, on crée généralement des comptes distincts pour les données d'application et les données de journalisation, et des comptes distincts pour les données de test et les données de production.</span><span class="sxs-lookup"><span data-stu-id="7b7de-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="7b7de-229">Pour ce didacticiel, vous allez utiliser un seul compte.</span><span class="sxs-lookup"><span data-stu-id="7b7de-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="7b7de-230">Dans le [portail Azure](https://portal.azure.com), cliquez sur **Nouveau > Stockage > Compte de stockage - blob, fichier, table, file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-230">In the [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="7b7de-231">Dans la zone **Nom** , entrez un préfixe d’URL.</span><span class="sxs-lookup"><span data-stu-id="7b7de-231">In the **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="7b7de-232">Ce préfixe, associé au texte visible sous la zone, sera l'URL unique de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7b7de-232">This prefix plus the text you see under the box will be the unique URL to your storage account.</span></span> <span data-ttu-id="7b7de-233">Si le préfixe que vous entrez est déjà utilisé, vous devez en choisir un autre.</span><span class="sxs-lookup"><span data-stu-id="7b7de-233">If the prefix you enter has already been used by someone else, you'll have to choose a different prefix.</span></span>
3. <span data-ttu-id="7b7de-234">Définissez le **Modèle de déploiement** sur *Classique*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-234">Set the **Deployment model** to *Classic*.</span></span>

4. <span data-ttu-id="7b7de-235">Dans la liste déroulante **Réplication**, sélectionnez **Stockage localement redondant**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-235">Set the **Replication** drop-down list to **Locally redundant storage**.</span></span>

    <span data-ttu-id="7b7de-236">Lorsque la géoréplication est activée pour un compte de stockage, le contenu stocké est répliqué dans un centre de données secondaire pour activer le basculement si un sinistre majeur se produit à l'emplacement principal.</span><span class="sxs-lookup"><span data-stu-id="7b7de-236">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover if a major disaster occurs in the primary location.</span></span> <span data-ttu-id="7b7de-237">La géo-réplication peut engendrer des coûts supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="7b7de-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="7b7de-238">Dans le cas des comptes test et de développement, vous êtes en général peu enclin à payer pour la géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="7b7de-238">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="7b7de-239">Pour plus d’informations, consultez [Création, gestion ou suppression d’un compte de stockage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="7b7de-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="7b7de-240">Dans le **Groupe de ressources**, cliquez sur **Use existing** (Utiliser existant) et sélectionnez le groupe de ressources utilisé pour le service cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-240">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
6. <span data-ttu-id="7b7de-241">Dans la liste déroulante **Emplacement**, sélectionnez la région choisie pour le service cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-241">Set the **Location** drop-down list to the same region you chose for the cloud service.</span></span>

    <span data-ttu-id="7b7de-242">Lorsque le service cloud et le compte de stockage se trouvent dans des centres de données différents (différentes régions), la latence augmente et la bande passante en dehors du centre de données vous est facturée,</span><span class="sxs-lookup"><span data-stu-id="7b7de-242">When the cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="7b7de-243">alors qu'elle est gratuite dans un centre de données.</span><span class="sxs-lookup"><span data-stu-id="7b7de-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="7b7de-244">Les groupes d'affinités Azure fournissent un mécanisme pour minimiser la distance entre les ressources dans un centre de données, ce qui peut réduire la latence.</span><span class="sxs-lookup"><span data-stu-id="7b7de-244">Azure affinity groups provide a mechanism to minimize the distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="7b7de-245">Ce didacticiel n'utilise pas de groupes d'affinités.</span><span class="sxs-lookup"><span data-stu-id="7b7de-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="7b7de-246">Pour plus d'informations, consultez la page [Création d'un groupe d'affinités dans Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b7de-246">For more information, see [How to Create an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="7b7de-247">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-247">Click **Create**.</span></span>

    ![New storage account](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="7b7de-249">Dans l’image, un compte de stockage est créé avec l’URL `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="7b7de-249">In the image, a storage account is created with the URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-the-solution-to-use-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="7b7de-250">Configuration de la solution pour utiliser votre base de données SQL Azure lorsqu’elle est exécutée dans Azure</span><span class="sxs-lookup"><span data-stu-id="7b7de-250">Configure the solution to use your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="7b7de-251">Le projet web et le projet de rôle de travail ont chacun leur chaîne de connexion à la base de données et doivent tous deux pointer vers la base de données SQL Azure lorsque l'application s'exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-251">The web project and the worker role project each has its own database connection string, and each needs to point to the Azure SQL database when the app runs in Azure.</span></span>

<span data-ttu-id="7b7de-252">Utilisez une [transformation Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) pour le rôle web et un paramètre d'environnement de service cloud pour le rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="7b7de-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for the web role and a cloud service environment setting for the worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="7b7de-253">Dans cette section et la suivante, vous allez stocker des informations d’identification dans des fichiers projet.</span><span class="sxs-lookup"><span data-stu-id="7b7de-253">In this section and the next section, you store credentials in project files.</span></span> <span data-ttu-id="7b7de-254">[Ne stockez pas d'informations confidentielles dans des référentiels de code source publics](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="7b7de-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="7b7de-255">Dans le projet ContosoAdsWeb, ouvrez le fichier de transformation *Web.Release.config* pour le fichier d’application *Web.config*, supprimez le bloc de commentaires qui contient un élément `<connectionStrings>`, puis collez le code suivant à la place.</span><span class="sxs-lookup"><span data-stu-id="7b7de-255">In the ContosoAdsWeb project, open the *Web.Release.config* transform file for the application *Web.config* file, delete the comment block that contains a `<connectionStrings>` element, and paste the following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="7b7de-256">Laissez le fichier ouvert pour le modifier.</span><span class="sxs-lookup"><span data-stu-id="7b7de-256">Leave the file open for editing.</span></span>
2. <span data-ttu-id="7b7de-257">Dans le [portail Azure](https://portal.azure.com), cliquez successivement sur **Bases de données SQL** dans le volet de gauche, sur la base de données que vous avez créée pour ce didacticiel, puis sur **Afficher les chaînes de connexion**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-257">In the [Azure portal](https://portal.azure.com), click **SQL Databases** in the left pane, click the database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Afficher les chaînes de connexion](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="7b7de-259">Le portail affiche les chaînes de connexion, avec un espace réservé pour le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7b7de-259">The portal displays connection strings, with a placeholder for the password.</span></span>

    ![Chaînes de connexion](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="7b7de-261">Dans le fichier de transformation *Web.Release.config*, supprimez `{connectionstring}` et collez à la place la chaîne de connexion ADO.NET du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-261">In the *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place the ADO.NET connection string from the Azure portal.</span></span>
4. <span data-ttu-id="7b7de-262">Dans la chaîne de connexion que vous avez collée dans le fichier de transformation *Web.Release.config*, remplacez `{your_password_here}` par le mot de passe que vous avez créé pour la nouvelle base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="7b7de-262">In the connection string that you pasted into the *Web.Release.config* transform file, replace `{your_password_here}` with the password you created for the new SQL database.</span></span>
5. <span data-ttu-id="7b7de-263">Enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="7b7de-263">Save the file.</span></span>  
6. <span data-ttu-id="7b7de-264">Sélectionnez et copiez la chaîne de connexion (sans les guillemets) pour l'utiliser dans les étapes suivantes de configuration du projet de rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="7b7de-264">Select and copy the connection string (without the surrounding quotation marks) for use in the following steps for configuring the worker role project.</span></span>
7. <span data-ttu-id="7b7de-265">Dans **l’Explorateur de solutions**, sous **Rôles** dans le projet de service cloud, cliquez avec le bouton droit sur **ContosoAdsWorker**, puis sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-265">In **Solution Explorer**, under **Roles** in the cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="7b7de-267">Cliquez sur l'onglet **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="7b7de-267">Click the **Settings** tab.</span></span>
9. <span data-ttu-id="7b7de-268">Changez **Configuration du service** en **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-268">Change **Service Configuration** to **Cloud**.</span></span>
10. <span data-ttu-id="7b7de-269">Sélectionnez le champ **Valeur** du paramètre `ContosoAdsDbConnectionString`, puis collez la chaîne de connexion que vous avez copiée à partir de la section précédente du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7b7de-269">Select the **Value** field for the `ContosoAdsDbConnectionString` setting, and then paste the connection string that you copied from the previous section of the tutorial.</span></span>

     ![Database connection string for worker role](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="7b7de-271">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="7b7de-271">Save your changes.</span></span>  

### <a name="configure-the-solution-to-use-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="7b7de-272">Configuration de la solution pour utiliser votre compte de stockage Azure lorsqu'elle est exécutée dans Azure</span><span class="sxs-lookup"><span data-stu-id="7b7de-272">Configure the solution to use your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="7b7de-273">Les chaînes de connexion au compte de stockage Azure pour le projet de rôle web et le projet de rôle de travail sont stockées dans les paramètres d’environnement du projet de service cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-273">Azure storage account connection strings for both the web role project and the worker role project are stored in environment settings in the cloud service project.</span></span> <span data-ttu-id="7b7de-274">Pour chaque projet, un ensemble distinct de paramètres doit être utilisé lorsque l’application s’exécute localement et dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-274">For each project, there is a separate set of settings to be used when the application runs locally and when it runs in the cloud.</span></span> <span data-ttu-id="7b7de-275">Vous allez mettre à jour les paramètres d'environnement de cloud pour les projets de rôle web et de travail.</span><span class="sxs-lookup"><span data-stu-id="7b7de-275">You'll update the cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="7b7de-276">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **ContosoAdsWeb** sous **Rôles** dans le projet **ContosoAdsCloudService**, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in the **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="7b7de-278">Cliquez sur l'onglet **Paramètres** . Dans la liste déroulante **Configuration du service**, sélectionnez **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-278">Click the **Settings** tab. In the **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Cloud configuration](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="7b7de-280">Sélectionnez l’entrée **StorageConnectionString**. Un bouton représentant des points de suspension (**...**) apparaît à l’extrémité droite de la ligne.</span><span class="sxs-lookup"><span data-stu-id="7b7de-280">Select the **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at the right end of the line.</span></span> <span data-ttu-id="7b7de-281">Cliquez dessus pour ouvrir la boîte de dialogue **Créer une chaîne de connexion de compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-281">Click the ellipsis button to open the **Create Storage Account Connection String** dialog box.</span></span>

    ![Open Connection String Create box](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="7b7de-283">Dans la boîte de dialogue **Créer une chaîne de connexion de compte de stockage**, cliquez sur **Votre abonnement**, choisissez le compte de stockage que vous avez créé précédemment, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-283">In the **Create Storage Connection String** dialog box, click **Your subscription**, choose the storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="7b7de-284">Si vous n'êtes pas déjà connecté, vous êtes invité à entrer vos informations d'identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Create Storage Connection String](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="7b7de-286">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="7b7de-286">Save your changes.</span></span>
6. <span data-ttu-id="7b7de-287">Suivez la même procédure que celle que vous avez utilisée pour la chaîne de connexion `StorageConnectionString` pour définir la chaîne de connexion `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="7b7de-287">Follow the same procedure that you used for the `StorageConnectionString` connection string to set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="7b7de-288">Cette chaîne de connexion est utilisée pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="7b7de-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="7b7de-289">Suivez la procédure utilisée pour le rôle **ContosoAdsWeb** pour définir les deux chaînes de connexion pour le rôle **ContosoAdsWorker**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-289">Follow the same procedure that you used for the **ContosoAdsWeb** role to set both connection strings for the **ContosoAdsWorker** role.</span></span> <span data-ttu-id="7b7de-290">Pensez à définir **Configuration du service** sur **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-290">Don't forget to set **Service Configuration** to **Cloud**.</span></span>

<span data-ttu-id="7b7de-291">Les paramètres d'environnement de rôle configurés à l'aide de l'interface utilisateur de Visual Studio sont stockés dans les fichiers suivants du projet ContosoAdsCloudService :</span><span class="sxs-lookup"><span data-stu-id="7b7de-291">The role environment settings that you have configured using the Visual Studio UI are stored in the following files in the ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="7b7de-292">*ServiceDefinition.csdef* : définit les noms des paramètres.</span><span class="sxs-lookup"><span data-stu-id="7b7de-292">*ServiceDefinition.csdef* - Defines the setting names.</span></span>
* <span data-ttu-id="7b7de-293">*ServiceConfiguration.Cloud.cscfg* : fournit des valeurs utilisées lorsque l'application s'exécute dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when the app runs in the cloud.</span></span>
* <span data-ttu-id="7b7de-294">*ServiceConfiguration.Local.cscfg* : fournit des valeurs utilisées lorsque l'application s'exécute localement.</span><span class="sxs-lookup"><span data-stu-id="7b7de-294">*ServiceConfiguration.Local.cscfg* - Provides values for when the app runs locally.</span></span>

<span data-ttu-id="7b7de-295">Par exemple, le fichier ServiceDefinition.csdef inclut les définitions suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b7de-295">For example, the ServiceDefinition.csdef includes the following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="7b7de-296">Et le fichier *ServiceConfiguration.Cloud.cscfg* inclut les valeurs entrées pour ces paramètres dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b7de-296">And the *ServiceConfiguration.Cloud.cscfg* file includes the values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="7b7de-297">Le paramètre `<Instances>` spécifie le nombre de machines virtuelles sur lesquelles Azure va exécuter le code du rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="7b7de-297">The `<Instances>` setting specifies the number of virtual machines that Azure will run the worker role code on.</span></span> <span data-ttu-id="7b7de-298">La section [Étapes suivantes](#next-steps) inclut des liens vers d'autres informations sur la montée en charge d'un service cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-298">The [Next steps](#next-steps) section includes links to more information about scaling out a cloud service,</span></span>

### <a name="deploy-the-project-to-azure"></a><span data-ttu-id="7b7de-299">Déployer le projet dans Azure</span><span class="sxs-lookup"><span data-stu-id="7b7de-299">Deploy the project to Azure</span></span>
1. <span data-ttu-id="7b7de-300">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet cloud **ContosoAdsCloudService** et sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-300">In **Solution Explorer**, right-click the **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Publish menu](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="7b7de-302">À l’étape **Se connecter** de l’Assistant **Publier l’application Azure**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-302">In the **Sign in** step of the **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Sign in step](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="7b7de-304">À l’étape **Paramètres** de l’Assistant, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-304">In the **Settings** step of the wizard, click **Next**.</span></span>

    ![Settings step](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="7b7de-306">Les paramètres par défaut sous l'onglet **Advanced** conviennent pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7b7de-306">The default settings in the **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="7b7de-307">Pour plus d'informations sur l'onglet avancé, consultez la rubrique [Assistant Publication d'application Azure](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b7de-307">For information about the advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="7b7de-308">À l’étape **Résumé**, cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-308">In the **Summary** step, click **Publish**.</span></span>

    ![Summary step](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="7b7de-310">La fenêtre **Journal des activités Azure** s'ouvre dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b7de-310">The **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="7b7de-311">Cliquez sur l'icône représentant une flèche vers la droite pour développer les détails du déploiement.</span><span class="sxs-lookup"><span data-stu-id="7b7de-311">Click the right arrow icon to expand the deployment details.</span></span>

    <span data-ttu-id="7b7de-312">Le déploiement peut durer environ 5 minutes, voire plus.</span><span class="sxs-lookup"><span data-stu-id="7b7de-312">The deployment can take up to 5 minutes or more to complete.</span></span>

    ![Azure Activity Log window](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="7b7de-314">Une fois le déploiement terminé, cliquez sur l’ **URL d’application web** pour lancer l’application.</span><span class="sxs-lookup"><span data-stu-id="7b7de-314">When the deployment status is complete, click the **Web app URL** to start the application.</span></span>
7. <span data-ttu-id="7b7de-315">À ce stade, vous pouvez tester l'application en créant, affichant et modifiant des publicités, comme lorsque vous avez exécuté l'application localement.</span><span class="sxs-lookup"><span data-stu-id="7b7de-315">You can now test the app by creating, viewing, and editing some ads, as you did when you ran the application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="7b7de-316">À l'issue du test, supprimez ou arrêtez le service cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-316">When you're finished testing, delete or stop the cloud service.</span></span> <span data-ttu-id="7b7de-317">Même si vous n'utilisez pas le service cloud, il accumule des frais, car les ressources de la machine virtuelle lui sont réservées.</span><span class="sxs-lookup"><span data-stu-id="7b7de-317">Even if you're not using the cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="7b7de-318">Si vous le laissez s'exécuter, toute personne qui trouve votre URL peut créer et afficher des publicités.</span><span class="sxs-lookup"><span data-stu-id="7b7de-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="7b7de-319">Dans le [portail Azure](https://portal.azure.com), ouvrez l’onglet **Vue d’ensemble** de votre service cloud, puis cliquez sur le bouton **Supprimer** en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="7b7de-319">In the [Azure portal](https://portal.azure.com), go to the **Overview** tab for your cloud service, and then click the **Delete** button at the top of the page.</span></span> <span data-ttu-id="7b7de-320">Si vous voulez juste empêcher temporairement l'accès au site, cliquez sur **Arrêter** .</span><span class="sxs-lookup"><span data-stu-id="7b7de-320">If you just want to temporarily prevent others from accessing the site, click **Stop** instead.</span></span> <span data-ttu-id="7b7de-321">Dans ce cas, les frais continuent de s'accumuler.</span><span class="sxs-lookup"><span data-stu-id="7b7de-321">In that case, charges will continue to accrue.</span></span> <span data-ttu-id="7b7de-322">Vous pouvez suivre une procédure similaire pour supprimer la base de données SQL et le compte de stockage lorsque vous n'en avez plus besoin.</span><span class="sxs-lookup"><span data-stu-id="7b7de-322">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-the-application-from-scratch"></a><span data-ttu-id="7b7de-323">Créer l’application à partir de zéro</span><span class="sxs-lookup"><span data-stu-id="7b7de-323">Create the application from scratch</span></span>
<span data-ttu-id="7b7de-324">Si vous n'avez pas encore téléchargé [l'application terminée](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), faites-le maintenant.</span><span class="sxs-lookup"><span data-stu-id="7b7de-324">If you haven't already downloaded [the completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="7b7de-325">Vous allez copier les fichiers du projet téléchargé dans le nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="7b7de-325">You'll copy files from the downloaded project into the new project.</span></span>

<span data-ttu-id="7b7de-326">La création de l'application Contoso Ads implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b7de-326">Creating the Contoso Ads application involves the following steps:</span></span>

* <span data-ttu-id="7b7de-327">création d'une solution Visual Studio de service cloud ;</span><span class="sxs-lookup"><span data-stu-id="7b7de-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="7b7de-328">mise à jour et ajout de packages NuGet ;</span><span class="sxs-lookup"><span data-stu-id="7b7de-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="7b7de-329">définition des références d'un projet ;</span><span class="sxs-lookup"><span data-stu-id="7b7de-329">Set project references.</span></span>
* <span data-ttu-id="7b7de-330">configuration des chaînes de connexion ;</span><span class="sxs-lookup"><span data-stu-id="7b7de-330">Configure connection strings.</span></span>
* <span data-ttu-id="7b7de-331">ajout de fichiers de code.</span><span class="sxs-lookup"><span data-stu-id="7b7de-331">Add code files.</span></span>

<span data-ttu-id="7b7de-332">Une fois la solution créée, vérifiez le code qui est propre aux projets de service cloud et aux objets blob et files d'attente Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-332">After the solution is created, you'll review the code that is unique to cloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="7b7de-333">Création d'une solution Visual Studio de service cloud</span><span class="sxs-lookup"><span data-stu-id="7b7de-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="7b7de-334">Dans Visual Studio, dans le menu **Nouveau projet** from the **Nouveau projet** .</span><span class="sxs-lookup"><span data-stu-id="7b7de-334">In Visual Studio, choose **New Project** from the **File** menu.</span></span>
2. <span data-ttu-id="7b7de-335">Dans le volet gauche de la boîte de dialogue **Nouveau projet**, développez **Visual C#** et choisissez les modèles **Cloud**, puis le modèle **Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-335">In the left pane of the **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose the **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="7b7de-336">Nommez le projet et la solution ContosoAdsCloudService, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-336">Name the project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Nouveau projet](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="7b7de-338">Dans la boîte de dialogue **Nouveau service cloud Azure**, ajoutez un rôle web et un rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="7b7de-338">In the **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="7b7de-339">Nommez le rôle web ContosoAdsWeb, et le rôle de travail ContosoAdsWorker</span><span class="sxs-lookup"><span data-stu-id="7b7de-339">Name the web role ContosoAdsWeb, and name the worker role ContosoAdsWorker.</span></span> <span data-ttu-id="7b7de-340">(pour modifier le nom par défaut des rôles, utilisez l'icône en forme de crayon dans le volet de droite).</span><span class="sxs-lookup"><span data-stu-id="7b7de-340">(Use the pencil icon in the right-hand pane to change the default names of the roles.)</span></span>

    ![New Cloud Service Project](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="7b7de-342">Lorsque la boîte de dialogue **Nouveau projet ASP.NET** est affichée pour le rôle web, choisissez le modèle MVC et cliquez sur **Modifier l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-342">When you see the **New ASP.NET Project** dialog box for the web role, choose the MVC template, and then click **Change Authentication**.</span></span>

    ![Modifier l'authentification](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="7b7de-344">Dans la boîte de dialogue **Modifier l’authentification**, choisissez **Aucune authentification** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-344">In the **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![Aucune authentification](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="7b7de-346">Dans la boîte de dialogue **Nouveau projet ASP.NET**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-346">In the **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="7b7de-347">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur la solution (pas sur l’un des projets) et choisissez **Ajouter - Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-347">In **Solution Explorer**, right-click the solution (not one of the projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="7b7de-348">Dans la boîte de dialogue **Ajouter un nouveau projet**, choisissez **Windows** sous **Visual C#** dans le volet gauche, puis cliquez sur le modèle **Bibliothèque de classes**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-348">In the **Add New Project** dialog box, choose **Windows** under **Visual C#** in the left pane, and then click the **Class Library** template.</span></span>  
10. <span data-ttu-id="7b7de-349">Nommez le projet *ContosoAdsCommon*, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-349">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="7b7de-350">Vous devez indiquer le contexte Entity Framework et le modèle de données des projets des rôles web et de travail.</span><span class="sxs-lookup"><span data-stu-id="7b7de-350">You need to reference the Entity Framework context and the data model from both web and worker role projects.</span></span> <span data-ttu-id="7b7de-351">Vous pouvez également définir les classes associées à Entity Framework dans le projet de rôle web et faire référence à ce projet dans le projet de rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="7b7de-351">As an alternative, you could define the EF-related classes in the web role project and reference that project from the worker role project.</span></span> <span data-ttu-id="7b7de-352">Mais dans l’approche alternative, votre projet de rôle de travail aura une référence inutile aux assemblys web.</span><span class="sxs-lookup"><span data-stu-id="7b7de-352">But in the alternative approach, your worker role project would have a reference to web assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="7b7de-353">Mise à jour et ajout de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="7b7de-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="7b7de-354">Ouvrez la boîte de dialogue **Gérer les packages NuGet** pour la solution.</span><span class="sxs-lookup"><span data-stu-id="7b7de-354">Open the **Manage NuGet Packages** dialog box for the solution.</span></span>
2. <span data-ttu-id="7b7de-355">En haut de la fenêtre, sélectionnez **Mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-355">At the top of the window, select **Updates**.</span></span>
3. <span data-ttu-id="7b7de-356">Recherchez le package *WindowsAzure.Storage* et, s’il se trouve dans la liste, sélectionnez-le, puis sélectionnez les projets web et de travail concernés par la mise à jour, puis cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-356">Look for the *WindowsAzure.Storage* package, and if it's in the list, select it and select the web and worker projects to update it in, and then click **Update**.</span></span>

    <span data-ttu-id="7b7de-357">La bibliothèque cliente de stockage est mise à jour plus souvent que les modèles de projet Visual Studio, ce qui explique pourquoi il faut effectuer la mise à jour dans un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="7b7de-357">The storage client library is updated more frequently than Visual Studio project templates, so you'll often find that the version in a newly-created project needs to be updated.</span></span>
4. <span data-ttu-id="7b7de-358">En haut de la fenêtre, sélectionnez **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-358">At the top of the window, select **Browse**.</span></span>
5. <span data-ttu-id="7b7de-359">Recherchez le package NuGet *EntityFramework* et installez-le dans les trois projets.</span><span class="sxs-lookup"><span data-stu-id="7b7de-359">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="7b7de-360">Recherchez le package NuGet *Microsoft.WindowsAzure.ConfigurationManager* et installez-le dans le projet de rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="7b7de-360">Find the *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in the worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="7b7de-361">Définition des références de projet</span><span class="sxs-lookup"><span data-stu-id="7b7de-361">Set project references</span></span>
1. <span data-ttu-id="7b7de-362">Dans le projet ContosoAdsWeb, définissez une référence au projet ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="7b7de-362">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="7b7de-363">Cliquez avec le bouton droit sur le projet ContosoAdsWeb, puis cliquez sur **Références** - **Ajouter des références**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-363">Right-click the ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="7b7de-364">Dans la boîte de dialogue **Gestionnaire de références**, dans le volet gauche, sélectionnez **Solution – Projets**, puis sélectionnez **ContosoAdsCommon** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-364">In the **Reference Manager** dialog box, select **Solution – Projects** in the left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="7b7de-365">Dans le projet ContosoAdsWorker, définissez une référence au projet ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="7b7de-365">In the ContosoAdsWorker project, set a reference to the ContosAdsCommon project.</span></span>

    <span data-ttu-id="7b7de-366">ContosoAdsCommon contient le modèle de données et la classe de contexte Entity Framework, qui seront utilisés par les applications frontale et principale.</span><span class="sxs-lookup"><span data-stu-id="7b7de-366">ContosoAdsCommon will contain the Entity Framework data model and context class, which will be used by both the front-end and back-end.</span></span>
3. <span data-ttu-id="7b7de-367">Dans le projet ContosoAdsWorker, définissez une référence à `System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="7b7de-367">In the ContosoAdsWorker project, set a reference to `System.Drawing`.</span></span>

    <span data-ttu-id="7b7de-368">Cet assembly est utilisé par l'application principale pour convertir les images en vignettes.</span><span class="sxs-lookup"><span data-stu-id="7b7de-368">This assembly is used by the back-end to convert images to thumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="7b7de-369">Configuration des chaînes de connexion</span><span class="sxs-lookup"><span data-stu-id="7b7de-369">Configure connection strings</span></span>
<span data-ttu-id="7b7de-370">Dans cette section, vous allez configurer les chaînes de connexion Azure Storage et SQL pour un test local.</span><span class="sxs-lookup"><span data-stu-id="7b7de-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="7b7de-371">Les instructions de déploiement données précédemment dans le didacticiel expliquent comment paramétrer les chaînes de connexion lorsque l'application s'exécute dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="7b7de-371">The deployment instructions earlier in the tutorial explain how to set up the connection strings for when the app runs in the cloud.</span></span>

1. <span data-ttu-id="7b7de-372">Dans le projet ContosoAdsWeb, ouvrez le fichier Web.config de l'application et insérez l'élément `connectionStrings` suivant après l'élément `configSections`.</span><span class="sxs-lookup"><span data-stu-id="7b7de-372">In the ContosoAdsWeb project, open the application Web.config file, and insert the following `connectionStrings` element after the `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="7b7de-373">Si vous utilisez Visual Studio 2015 ou version ultérieure, remplacez « v11.0 » par « MSSQLLocalDB ».</span><span class="sxs-lookup"><span data-stu-id="7b7de-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="7b7de-374">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="7b7de-374">Save your changes.</span></span>
3. <span data-ttu-id="7b7de-375">Dans le projet ContosoAdsCloudService, cliquez avec le bouton droit sur ContosoAdsWeb sous **Rôles**, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-375">In the ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="7b7de-377">Dans la fenêtre des propriétés **ContosAdsWeb [Rôle]**, cliquez sur l’onglet **Paramètres**, puis sur **Ajouter un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-377">In the **ContosAdsWeb [Role]** properties window, click the **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="7b7de-378">Laissez **Configuration du service** sur **Toutes les configurations**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-378">Leave **Service Configuration** set to **All Configurations**.</span></span>
5. <span data-ttu-id="7b7de-379">Ajoutez un paramètre nommé *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="7b7de-380">Définissez **Type** sur *ConnectionString* et **Value** sur *UseDevelopmentStorage=true*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-380">Set **Type** to *ConnectionString*, and set **Value** to *UseDevelopmentStorage=true*.</span></span>

    ![New connection string](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="7b7de-382">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="7b7de-382">Save your changes.</span></span>
7. <span data-ttu-id="7b7de-383">Suivez la procédure utilisée pour ajouter une chaîne de connexion de stockage dans les propriétés du rôle ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="7b7de-383">Follow the same procedure to add a storage connection string in the ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="7b7de-384">Toujours dans la fenêtre des propriétés **ContosoAdsWorker [Rôle]** , ajoutez une chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="7b7de-384">Still in the **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="7b7de-385">Nom : ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="7b7de-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="7b7de-386">Type : string</span><span class="sxs-lookup"><span data-stu-id="7b7de-386">Type: String</span></span>
   * <span data-ttu-id="7b7de-387">Valeur : collez la même chaîne de connexion que celle utilisée pour le projet de rôle web.</span><span class="sxs-lookup"><span data-stu-id="7b7de-387">Value: Paste the same connection string you used for the web role project.</span></span> <span data-ttu-id="7b7de-388">(L’exemple suivant concerne Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7b7de-388">(The following example is for Visual Studio 2013.</span></span> <span data-ttu-id="7b7de-389">N’oubliez pas de modifier la source de données si vous copiez cet exemple et utilisez Visual Studio 2015 ou version ultérieure.)</span><span class="sxs-lookup"><span data-stu-id="7b7de-389">Don't forget to change the Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="7b7de-390">Ajout de fichiers de code</span><span class="sxs-lookup"><span data-stu-id="7b7de-390">Add code files</span></span>
<span data-ttu-id="7b7de-391">Dans cette section, vous allez copier les fichiers de code de la solution téléchargée dans la nouvelle solution.</span><span class="sxs-lookup"><span data-stu-id="7b7de-391">In this section, you copy code files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="7b7de-392">Les sections suivantes montrent et expliquent les éléments essentiels de ce code.</span><span class="sxs-lookup"><span data-stu-id="7b7de-392">The following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="7b7de-393">Pour ajouter des fichiers à un projet ou à un dossier, cliquez avec le bouton droit sur le projet ou le dossier, puis cliquez sur **Ajouter** - **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-393">To add files to a project or a folder, right-click the project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="7b7de-394">Sélectionnez les fichiers et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-394">Select the files you want and then click **Add**.</span></span> <span data-ttu-id="7b7de-395">Si un message vous demande si vous souhaitez remplacer les fichiers existants, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-395">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="7b7de-396">Dans le projet ContosoAdsCommon, supprimez le fichier *Class1.cs* et ajoutez à la place les fichiers *Ad.cs* et *ContosoAdscontext.cs* du projet téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7b7de-396">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the *Ad.cs* and *ContosoAdscontext.cs* files from the downloaded project.</span></span>
2. <span data-ttu-id="7b7de-397">Dans le projet ContosoAdsWeb, ajoutez les fichiers suivants du projet téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7b7de-397">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="7b7de-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="7b7de-399">Dans le dossier *Views\Shared* : *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-399">In the *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="7b7de-400">Dans le dossier *Views\Home* : *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-400">In the *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="7b7de-401">Dans le dossier *Controllers* : *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-401">In the *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="7b7de-402">Dans le dossier *Views\Ad* (à créer) : cinq fichiers *.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-402">In the *Views\Ad* folder (create the folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="7b7de-403">Dans le projet ContosoAdsWorker, ajoutez le fichier *WorkerRole.cs* du projet téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7b7de-403">In the ContosoAdsWorker project, add *WorkerRole.cs* from the downloaded project.</span></span>

<span data-ttu-id="7b7de-404">À ce stade, vous pouvez générer et exécuter l'application comme indiqué précédemment dans le didacticiel. L'application utilisera la base de données locale et les ressources de l'émulateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="7b7de-404">You can now build and run the application as instructed earlier in the tutorial, and the app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="7b7de-405">Les sections suivantes présentent le code utilisé dans l'environnement, les objets blob et les files d'attente Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-405">The following sections explain the code related to working with the Azure environment, blobs, and queues.</span></span> <span data-ttu-id="7b7de-406">Ce didacticiel ne montre pas comment créer des contrôleurs et des vues MVC à l'aide de la structure, comment écrire du code Entity Framework qui fonctionne avec les bases de données SQL Server, ni les bases de la programmation asynchrone dans ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="7b7de-406">This tutorial does not explain how to create MVC controllers and views using scaffolding, how to write Entity Framework code that works with SQL Server databases, or the basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="7b7de-407">Pour plus d'informations sur ces sujets, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b7de-407">For information about these topics, see the following resources:</span></span>

* [<span data-ttu-id="7b7de-408">Prise en main de MVC 5</span><span class="sxs-lookup"><span data-stu-id="7b7de-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="7b7de-409">Prise en main d’EF 6 et de MVC 5</span><span class="sxs-lookup"><span data-stu-id="7b7de-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="7b7de-410">[Introduction à la programmation asynchrone dans .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="7b7de-410">[Introduction to asynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="7b7de-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="7b7de-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="7b7de-412">Le fichier Ad.cs définit une énumération des catégories de publicité et une classe d'entité POCO pour les informations de publicité.</span><span class="sxs-lookup"><span data-stu-id="7b7de-412">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
public enum Category
{
    Cars,
    [Display(Name="Real Estate")]
    RealEstate,
    [Display(Name = "Free Stuff")]
    FreeStuff
}

public class Ad
{
    public int AdId { get; set; }

    [StringLength(100)]
    public string Title { get; set; }

    public int Price { get; set; }

    [StringLength(1000)]
    [DataType(DataType.MultilineText)]
    public string Description { get; set; }

    [StringLength(1000)]
    [DisplayName("Full-size Image")]
    public string ImageURL { get; set; }

    [StringLength(1000)]
    [DisplayName("Thumbnail")]
    public string ThumbnailURL { get; set; }

    [DataType(DataType.Date)]
    [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
    public DateTime PostedDate { get; set; }

    public Category? Category { get; set; }
    [StringLength(12)]
    public string Phone { get; set; }
}
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="7b7de-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="7b7de-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="7b7de-414">La classe ContosoAdsContext spécifie que la classe Ad est utilisée dans une collection DbSet, qui est stockée par Entity Framework dans une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="7b7de-414">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
public class ContosoAdsContext : DbContext
{
    public ContosoAdsContext() : base("name=ContosoAdsContext")
    {
    }
    public ContosoAdsContext(string connString)
        : base(connString)
    {
    }
    public System.Data.Entity.DbSet<Ad> Ads { get; set; }
}
```

<span data-ttu-id="7b7de-415">La classe a deux constructeurs.</span><span class="sxs-lookup"><span data-stu-id="7b7de-415">The class has two constructors.</span></span> <span data-ttu-id="7b7de-416">Le premier est utilisé par le projet web et spécifie le nom d'une chaîne de connexion stockée dans le fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="7b7de-416">The first of them is used by the web project, and specifies the name of a connection string that is stored in the Web.config file.</span></span> <span data-ttu-id="7b7de-417">Le second vous permet de passer la chaîne de connexion réelle utilisée par le projet de rôle de travail, car il n’a pas un fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="7b7de-417">The second constructor enables you to pass in the actual connection string used by the worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="7b7de-418">Vous avez vu précédemment où est stockée cette chaîne de connexion, et vous allez voir comme le code la récupère quand il instancie la classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="7b7de-418">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="7b7de-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="7b7de-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="7b7de-420">Le code appelé par la méthode `Application_Start` crée un conteneur d’objets blob *images* et une file d’attente *images*, s’ils n’existent pas déjà.</span><span class="sxs-lookup"><span data-stu-id="7b7de-420">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="7b7de-421">Ainsi, à chaque fois que vous utilisez un nouveau compte de stockage ou l'émulateur de stockage sur un nouvel ordinateur, le conteneur d'objets blob et la file d'attente nécessaires sont créés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="7b7de-421">This ensures that whenever you start using a new storage account, or start using the storage emulator on a new computer, the required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="7b7de-422">Le code a accès au compte de stockage en utilisant la chaîne de connexion du fichier *.cscfg* .</span><span class="sxs-lookup"><span data-stu-id="7b7de-422">The code gets access to the storage account by using the storage connection string from the *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="7b7de-423">Il obtient ensuite une référence au conteneur d'objets blob *images* , crée le conteneur s'il n'existe pas déjà et définit les autorisations d'accès au nouveau conteneur.</span><span class="sxs-lookup"><span data-stu-id="7b7de-423">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="7b7de-424">Par défaut, les nouveaux conteneurs donnent accès aux objets blob uniquement aux clients possédant des informations d'identification de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7b7de-424">By default, new containers only allow clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="7b7de-425">Pour le site web, les objets blob doivent être publics pour afficher des images en utilisant des URL qui pointent vers les objets blob des images.</span><span class="sxs-lookup"><span data-stu-id="7b7de-425">The website needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="7b7de-426">Du code similaire obtient une référence à la file d'attente *images* et crée une nouvelle file d'attente.</span><span class="sxs-lookup"><span data-stu-id="7b7de-426">Similar code gets a reference to the *images* queue and creates a new queue.</span></span> <span data-ttu-id="7b7de-427">Dans ce cas, aucune modification des autorisations n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7b7de-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="7b7de-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="7b7de-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="7b7de-429">Le fichier *_Layout.cshtml* définit le nom de l’application dans l’en-tête et le pied de page, puis crée une entrée de menu « Ads ».</span><span class="sxs-lookup"><span data-stu-id="7b7de-429">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="7b7de-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="7b7de-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="7b7de-431">Le fichier *Views\Home\Index.cshtml* affiche les liens de catégorie sur la page d'accueil.</span><span class="sxs-lookup"><span data-stu-id="7b7de-431">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="7b7de-432">Les liens transmettent la valeur entière de l’énumération `Category` d’une variable querystring à la page Ads Index.</span><span class="sxs-lookup"><span data-stu-id="7b7de-432">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="7b7de-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="7b7de-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="7b7de-434">Dans le fichier *AdController.cs*, le constructeur appelle la méthode `InitializeStorage` pour créer les objets de la bibliothèque cliente Azure Storage, qui fournissent une API pour les objets blob et les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="7b7de-434">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="7b7de-435">Le code obtient ensuite une référence au conteneur d'objets blob *images* comme vu précédemment dans *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="7b7de-435">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="7b7de-436">Ce faisant, il définit une [stratégie de nouvelles tentatives](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) par défaut appropriée pour une application web.</span><span class="sxs-lookup"><span data-stu-id="7b7de-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="7b7de-437">La stratégie de nouvelles tentatives d'interruption exponentielle par défaut peut suspendre l'application web pendant plus d'une minute en cas de tentatives répétées pour une erreur temporaire.</span><span class="sxs-lookup"><span data-stu-id="7b7de-437">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="7b7de-438">La stratégie de nouvelle tentative spécifiée ici laisse trois secondes après chaque nouvelle tentative, jusqu’à trois.</span><span class="sxs-lookup"><span data-stu-id="7b7de-438">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="7b7de-439">Un code similaire obtient une référence à la file d'attente *images* .</span><span class="sxs-lookup"><span data-stu-id="7b7de-439">Similar code gets a reference to the *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="7b7de-440">La plupart du code du contrôleur permet généralement d'utiliser un modèle de données Entity Framework en utilisant une classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="7b7de-440">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="7b7de-441">La méthode HttpPost `Create` est une exception, car elle télécharge un fichier et l’enregistre dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="7b7de-441">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="7b7de-442">Le classeur de modèles fournit un objet [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) à la méthode.</span><span class="sxs-lookup"><span data-stu-id="7b7de-442">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="7b7de-443">Si l'utilisateur a sélectionné un fichier à télécharger, le code met à jour le fichier, l'enregistre dans un objet blob et met à jour l'enregistrement de base de données AD avec une URL qui pointe vers l'objet blob.</span><span class="sxs-lookup"><span data-stu-id="7b7de-443">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="7b7de-444">Le code qui procède au téléchargement se trouve dans la méthode `UploadAndSaveBlobAsync` .</span><span class="sxs-lookup"><span data-stu-id="7b7de-444">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="7b7de-445">Il crée un nom GUID pour l’objet blob, télécharge et enregistre le fichier, et renvoie une référence vers l’objet blob enregistré.</span><span class="sxs-lookup"><span data-stu-id="7b7de-445">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

```csharp
private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
{
    string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
    CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
    using (var fileStream = imageFile.InputStream)
    {
        await imageBlob.UploadFromStreamAsync(fileStream);
    }
    return imageBlob;
}
```

<span data-ttu-id="7b7de-446">Dès que la méthode `Create` HttpPost charge un objet blob et met à jour la base de données, elle crée un message de file d’attente pour informer ce processus de backend qu’une image est prête à être convertie en vignette.</span><span class="sxs-lookup"><span data-stu-id="7b7de-446">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform that back-end process that an image is ready for conversion to a thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="7b7de-447">Le code de la méthode `Edit` HttpPost est similaire, mais si l’utilisateur sélectionne un nouveau fichier image, les objets blob existants doivent être supprimés.</span><span class="sxs-lookup"><span data-stu-id="7b7de-447">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="7b7de-448">L'exemple suivant illustre le code qui supprime les objets blob lorsque vous supprimez une publicité.</span><span class="sxs-lookup"><span data-stu-id="7b7de-448">The next example shows the code that deletes blobs when you delete an ad.</span></span>

```csharp
private async Task DeleteAdBlobsAsync(Ad ad)
{
    if (!string.IsNullOrWhiteSpace(ad.ImageURL))
    {
        Uri blobUri = new Uri(ad.ImageURL);
        await DeleteAdBlobAsync(blobUri);
    }
    if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
    {
        Uri blobUri = new Uri(ad.ThumbnailURL);
        await DeleteAdBlobAsync(blobUri);
    }
}
private static async Task DeleteAdBlobAsync(Uri blobUri)
{
    string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
    CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
    await blobToDelete.DeleteAsync();
}
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="7b7de-449">ContosoAdsWeb - Views\Ad\Index.cshtml et Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="7b7de-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="7b7de-450">Le fichier *Index.cshtml* affiche des vignettes avec les autres données de publicité.</span><span class="sxs-lookup"><span data-stu-id="7b7de-450">The *Index.cshtml* file displays thumbnails with the other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="7b7de-451">Le fichier *Details.cshtml* affiche l'image intégrale.</span><span class="sxs-lookup"><span data-stu-id="7b7de-451">The *Details.cshtml* file displays the full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="7b7de-452">ContosoAdsWeb - Views\Ad\Create.cshtml et Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="7b7de-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="7b7de-453">Les fichiers *Create.cshtml* et *Edit.cshtml* spécifient l’encodage de formulaire qui permet au contrôleur d’obtenir l’objet `HttpPostedFileBase`.</span><span class="sxs-lookup"><span data-stu-id="7b7de-453">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="7b7de-454">Un élément `<input>` indique au navigateur de fournir une boîte de dialogue de sélection de fichier.</span><span class="sxs-lookup"><span data-stu-id="7b7de-454">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="7b7de-455">ContosoAdsWorker - WorkerRole.cs - Méthode OnStart</span><span class="sxs-lookup"><span data-stu-id="7b7de-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="7b7de-456">L’environnement du rôle de travail Azure appelle la méthode `OnStart` de la classe `WorkerRole` lorsque le rôle de travail est démarré, puis appelle la méthode `Run` à la fin de la méthode `OnStart`.</span><span class="sxs-lookup"><span data-stu-id="7b7de-456">The Azure worker role environment calls the `OnStart` method in the `WorkerRole` class when the worker role is getting started, and it calls the `Run` method when the `OnStart` method finishes.</span></span>

<span data-ttu-id="7b7de-457">La méthode `OnStart` obtient la chaîne de connexion à la base de données à partir du fichier *.cscfg* et la transmet à la classe DbContext d’Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="7b7de-457">The `OnStart` method gets the database connection string from the *.cscfg* file and passes it to the Entity Framework DbContext class.</span></span> <span data-ttu-id="7b7de-458">Le fournisseur SQLClient est utilisé par défaut et n'a donc pas besoin d'être spécifié.</span><span class="sxs-lookup"><span data-stu-id="7b7de-458">The SQLClient provider is used by default, so the provider does not have to be specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="7b7de-459">La méthode obtient ensuite une référence au compte de stockage et crée le conteneur d’objets blob et la file d’attente s’ils n’existent pas déjà.</span><span class="sxs-lookup"><span data-stu-id="7b7de-459">After that, the method gets a reference to the storage account and creates the blob container and queue if they don't exist.</span></span> <span data-ttu-id="7b7de-460">Le code correspondant est celui que vous avez déjà vu dans la méthode `Application_Start` du rôle Web.</span><span class="sxs-lookup"><span data-stu-id="7b7de-460">The code for that is similar to what you already saw in the web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="7b7de-461">ContosoAdsWorker - WorkerRole.cs - Méthode Run</span><span class="sxs-lookup"><span data-stu-id="7b7de-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="7b7de-462">La méthode `Run` est appelée lorsque la méthode `OnStart` a terminé son travail d’initialisation.</span><span class="sxs-lookup"><span data-stu-id="7b7de-462">The `Run` method is called when the `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="7b7de-463">La méthode exécute une boucle infinie qui recherche des messages de file d'attente et les traite lorsqu'ils arrivent.</span><span class="sxs-lookup"><span data-stu-id="7b7de-463">The method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="7b7de-464">Après chaque itération de la boucle, si aucun message de file d'attente n'a été trouvé, le programme se met en veille pendant une seconde.</span><span class="sxs-lookup"><span data-stu-id="7b7de-464">After each iteration of the loop, if no queue message was found, the program sleeps for a second.</span></span> <span data-ttu-id="7b7de-465">Cela évite au rôle de travail un temps processeur et des coûts de transaction de stockage trop élevés.</span><span class="sxs-lookup"><span data-stu-id="7b7de-465">This prevents the worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="7b7de-466">L’équipe de conseil clientèle Microsoft raconte une anecdote sur un développeur qui, avant de partir en vacances, avait oublié d’inclure ce point et avait procédé au déploiement en production.</span><span class="sxs-lookup"><span data-stu-id="7b7de-466">The Microsoft Customer Advisory Team tells a story about a  developer who forgot to include this, deployed to production, and left for vacation.</span></span> <span data-ttu-id="7b7de-467">À son retour, les coûts de surveillance étaient plus élevés que le coût de ses vacances.</span><span class="sxs-lookup"><span data-stu-id="7b7de-467">When he got back, his oversight cost more than the vacation.</span></span>

<span data-ttu-id="7b7de-468">Il arrive que le contenu d'un message de file d'attente provoque une erreur de traitement.</span><span class="sxs-lookup"><span data-stu-id="7b7de-468">Sometimes the content of a queue message causes an error in processing.</span></span> <span data-ttu-id="7b7de-469">On parle alors de *message empoisonné*, et si vous relancez la boucle après avoir consigné une erreur, vous risquez d'essayer sans fin de traiter ce message.</span><span class="sxs-lookup"><span data-stu-id="7b7de-469">This is called a *poison message*, and if you just logged an error and restarted the loop, you could endlessly try to process that message.</span></span>  <span data-ttu-id="7b7de-470">Le bloc catch inclut donc une instruction If qui vérifie combien de fois l'application a tenté de traiter le message actuel, et si le nombre de tentatives est supérieur à 5, le message est supprimé de la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="7b7de-470">Therefore the catch block includes an if statement that checks to see how many times the app has tried to process the current message, and if it has been more than 5 times, the message is deleted from the queue.</span></span>

<span data-ttu-id="7b7de-471">`ProcessQueueMessage` est appelé lorsqu'un message de file d'attente est trouvé.</span><span class="sxs-lookup"><span data-stu-id="7b7de-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="7b7de-472">Ce code lit la base de données pour obtenir l'URL de l'image, convertit l'image en vignette, enregistre la vignette dans un objet blob, met à jour la base de données avec l'URL de l'objet blob de la vignette et supprime le message de la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="7b7de-472">This code reads the database to get the image URL, converts the image to a thumbnail, saves the thumbnail in a blob, updates the database with the thumbnail blob URL, and deletes the queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="7b7de-473">Pour plus de simplicité, le code de la méthode `ConvertImageToThumbnailJPG` utilise des classes dans l’espace de noms System.Drawing.</span><span class="sxs-lookup"><span data-stu-id="7b7de-473">The code in the `ConvertImageToThumbnailJPG` method uses classes in the System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="7b7de-474">Cependant, les classes de cet espace de noms ont été conçues pour être utilisées avec Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="7b7de-474">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="7b7de-475">Elles ne sont pas prises en charge dans un service Windows ou ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7b7de-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="7b7de-476">Pour plus d’informations sur les options de traitement d’images, consultez [Génération d’images dynamiques](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) et [Redimensionnement d’images approfondi](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="7b7de-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="7b7de-477">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="7b7de-477">Troubleshooting</span></span>
<span data-ttu-id="7b7de-478">Voici quelques erreurs courantes et leur solution en cas de problème lorsque vous suivez les instructions de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7b7de-478">In case something doesn't work while you're following the instructions in this tutorial, here are some common errors and how to resolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="7b7de-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="7b7de-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="7b7de-480">L’objet `RoleEnvironment` est fourni par Azure lorsque vous exécutez une application dans Azure ou lorsque vous l’exécutez localement à l’aide de l’émulateur de calcul Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-480">The `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using the Azure compute emulator.</span></span>  <span data-ttu-id="7b7de-481">Si vous obtenez cette erreur lors de l'exécution en local, vérifiez si le projet ContosoAdsCloudService est défini comme projet de démarrage.</span><span class="sxs-lookup"><span data-stu-id="7b7de-481">If you get this error when you're running locally, make sure that you have set the ContosoAdsCloudService project as the startup project.</span></span> <span data-ttu-id="7b7de-482">Cela permet au projet de s'exécuter avec l'émulateur de calcul Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-482">This sets up the project to run using the Azure compute emulator.</span></span>

<span data-ttu-id="7b7de-483">L'application utilise notamment la classe RoleEnvironment Azure pour obtenir les valeurs de chaîne de connexion qui sont stockées dans les fichiers *.cscfg* , et l'absence de chaîne de connexion est une autre cause de cette exception.</span><span class="sxs-lookup"><span data-stu-id="7b7de-483">One of the things the application uses the Azure RoleEnvironment for is to get the connection string values that are stored in the *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="7b7de-484">Veillez à créer le paramètre StorageConnectionString pour les configurations cloud et locale dans le projet ContosoAdsWeb et créez les deux chaînes de connexion pour les deux configurations dans le projet ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="7b7de-484">Make sure that you created the StorageConnectionString setting for both Cloud and Local configurations in the ContosoAdsWeb project, and that you created both connection strings for both configurations in the ContosoAdsWorker project.</span></span> <span data-ttu-id="7b7de-485">Si vous effectuez une recherche de type **Rechercher tout** pour StorageConnectionString dans toute la solution, vous devez la voir 9 fois dans 6 fichiers.</span><span class="sxs-lookup"><span data-stu-id="7b7de-485">If you do a **Find All** search for StorageConnectionString in the entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-to-port-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="7b7de-486">Impossible de remplacer par le port xxx.</span><span class="sxs-lookup"><span data-stu-id="7b7de-486">Cannot override to port xxx.</span></span> <span data-ttu-id="7b7de-487">La valeur du nouveau port est inférieure à la valeur minimale autorisée de 8080 pour le protocole http</span><span class="sxs-lookup"><span data-stu-id="7b7de-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="7b7de-488">Changez le numéro du port utilisé par le projet web.</span><span class="sxs-lookup"><span data-stu-id="7b7de-488">Try changing the port number used by the web project.</span></span> <span data-ttu-id="7b7de-489">Cliquez avec le bouton droit sur le projet ContosoAdsWeb, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-489">Right-click the ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="7b7de-490">Cliquez sur l’onglet **Web** et changez le numéro du port dans le paramètre **URL du projet**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-490">Click the **Web** tab, and then change the port number in the **Project Url** setting.</span></span>

<span data-ttu-id="7b7de-491">Vous trouverez une autre solution au problème dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="7b7de-491">For another alternative that might resolve the problem, see the following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="7b7de-492">Autres erreurs lors de l'exécution locale</span><span class="sxs-lookup"><span data-stu-id="7b7de-492">Other errors when running locally</span></span>
<span data-ttu-id="7b7de-493">Par défaut, les nouveaux projets de service cloud utilisent l'émulateur de calcul Azure express pour simuler l'environnement Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7de-493">By default new cloud service projects use the Azure compute emulator express to simulate the Azure environment.</span></span> <span data-ttu-id="7b7de-494">Il s'agit d'une version légère de l'émulateur de calcul, mais il peut arriver que la version express ne fonctionne pas là où l'émulateur complet fonctionne.</span><span class="sxs-lookup"><span data-stu-id="7b7de-494">This is a lightweight version of the full compute emulator, and under some conditions the full emulator will work when the express version does not.</span></span>  

<span data-ttu-id="7b7de-495">Pour que le projet utilise la version complète de l'émulateur, cliquez avec le bouton droit sur le projet ContosoAdsCloudService, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-495">To change the project to use the full emulator, right-click the ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="7b7de-496">Dans la fenêtre **Propriétés**, cliquez sur l’onglet **Web**, puis sur la case d’option **Utiliser l’émulateur complet**.</span><span class="sxs-lookup"><span data-stu-id="7b7de-496">In the **Properties** window click the **Web** tab, and then click the **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="7b7de-497">Pour exécuter l'application avec l'émulateur complet, vous devez ouvrir Visual Studio avec les privilèges d'administrateur.</span><span class="sxs-lookup"><span data-stu-id="7b7de-497">In order to run the application with the full emulator, you have to open Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b7de-498">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7b7de-498">Next steps</span></span>
<span data-ttu-id="7b7de-499">L'application Contoso Ads est intentionnellement simple pour un didacticiel de prise en main.</span><span class="sxs-lookup"><span data-stu-id="7b7de-499">The Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="7b7de-500">Par exemple, elle n’implémente pas [l’injection de dépendances](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) ni les [modèles de référentiel et d’élément de travail](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), elle [n’utilise pas d’interface pour la connexion](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), ni les [migrations Code First EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) pour gérer les changements de modèles de données ou la [résilience des connexions EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) pour gérer les erreurs réseau temporaires, etc.</span><span class="sxs-lookup"><span data-stu-id="7b7de-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors, and so forth.</span></span>

<span data-ttu-id="7b7de-501">Voici quelques exemples d'applications de service cloud qui montrent des pratiques d'encodage réelles, de la plus simple à la plus complexe :</span><span class="sxs-lookup"><span data-stu-id="7b7de-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex to more complex:</span></span>

* <span data-ttu-id="7b7de-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="7b7de-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="7b7de-503">De conception identique à Contoso Ads, mais implémente plus de fonctionnalités et plus de pratiques d'encodage réelles.</span><span class="sxs-lookup"><span data-stu-id="7b7de-503">Similar in concept to Contoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="7b7de-504">[Application multiniveau Azure Cloud Service avec tables, files d'attente et objets blob](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="7b7de-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="7b7de-505">Présente les tables Azure Storage ainsi que des objets blob et des files d’attente.</span><span class="sxs-lookup"><span data-stu-id="7b7de-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="7b7de-506">Si l’on se base sur une version plus ancienne du kit de développement logiciel Azure pour .NET, certaines modifications sont nécessaires pour travailler avec la version actuelle.</span><span class="sxs-lookup"><span data-stu-id="7b7de-506">Based on an older version of the Azure SDK for .NET, will require some modifications to work with the current version.</span></span>
* <span data-ttu-id="7b7de-507">[Concepts de base des services cloud dans Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="7b7de-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="7b7de-508">Cet exemple complet présente une grande variété de meilleures pratiques, produites par le groupe Microsoft Patterns and Practices.</span><span class="sxs-lookup"><span data-stu-id="7b7de-508">A comprehensive sample demonstrating a wide range of best practices, produced by the Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="7b7de-509">Pour obtenir des informations générales sur le développement pour le cloud, consultez la rubrique [Création d’applications cloud réalistes avec Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="7b7de-509">For general information about developing for the cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="7b7de-510">Pour voir une vidéo de présentation des meilleures pratiques et des modèles Azure Storage, consultez la rubrique [Microsoft Azure Storage – Nouveautés, meilleures pratiques et modèles](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="7b7de-510">For a video introduction to Azure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="7b7de-511">Pour plus d’informations, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b7de-511">For more information, see the following resources:</span></span>

* [<span data-ttu-id="7b7de-512">Azure Cloud Services Partie 1 : Présentation</span><span class="sxs-lookup"><span data-stu-id="7b7de-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="7b7de-513">Gestion des services cloud</span><span class="sxs-lookup"><span data-stu-id="7b7de-513">How to manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="7b7de-514">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7b7de-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="7b7de-515">Choix d’un fournisseur de services cloud</span><span class="sxs-lookup"><span data-stu-id="7b7de-515">How to choose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
