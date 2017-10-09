---
title: "aaaGet démarrer avec ASP.NET et les Services de cloud computing Azure | Documents Microsoft"
description: "Découvrez comment toocreate une application à plusieurs niveaux à l’aide d’ASP.NET MVC et Azure. application Hello s’exécute dans un service cloud, avec un rôle web et rôle de travail. Elle utilise Entity Framework, Base de données SQL et les files d'attente et objets blobs du stockage Azure."
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
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="30853-105">Prise en main des services cloud Azure et d'ASP.NET</span><span class="sxs-lookup"><span data-stu-id="30853-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="30853-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="30853-106">Overview</span></span>
<span data-ttu-id="30853-107">Ce didacticiel montre comment toocreate une application de .NET à plusieurs niveaux avec un frontal, ASP.NET MVC et déployez-le tooan [service cloud Azure](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="30853-107">This tutorial shows how toocreate a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it tooan [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="30853-108">Hello application utilise [base de données SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), hello [service d’objets Blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)et hello [service de file d’attente Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="30853-108">hello application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and hello [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="30853-109">Vous pouvez [télécharger le projet de Visual Studio hello](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) de hello MSDN Code Gallery.</span><span class="sxs-lookup"><span data-stu-id="30853-109">You can [download hello Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from hello MSDN Code Gallery.</span></span>

<span data-ttu-id="30853-110">didacticiel de Hello vous montre comment application hello toobuild et exécutez localement, comment toodeploy il tooAzure et hello exécution dans le cloud et comment toobuild à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="30853-110">hello tutorial shows you how toobuild and run hello application locally, how toodeploy it tooAzure and run in hello cloud, and how toobuild it from scratch.</span></span> <span data-ttu-id="30853-111">Vous pouvez commencer par la génération à partir de zéro et puis hello test et déployer ensuite les étapes si vous préférez.</span><span class="sxs-lookup"><span data-stu-id="30853-111">You can start by building from scratch and then do hello test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="30853-112">Application Contoso Ads</span><span class="sxs-lookup"><span data-stu-id="30853-112">Contoso Ads application</span></span>
<span data-ttu-id="30853-113">application Hello est un forum de publicité.</span><span class="sxs-lookup"><span data-stu-id="30853-113">hello application is an advertising bulletin board.</span></span> <span data-ttu-id="30853-114">Les utilisateurs créent une publicité en entrant du texte et en téléchargeant une image.</span><span class="sxs-lookup"><span data-stu-id="30853-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="30853-115">Ils peuvent voir une liste de publicités avec des images miniatures, et ils peuvent voir image en taille réelle de hello lorsqu’ils sélectionnent un ad toosee hello les détails.</span><span class="sxs-lookup"><span data-stu-id="30853-115">They can see a list of ads with thumbnail images, and they can see hello full-size image when they select an ad toosee hello details.</span></span>

![Ad list](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="30853-117">application Hello utilise hello [centré sur la file d’attente de travail modèle](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) travail hello sollicitant beaucoup le processeur de toooff en charge de la création de miniatures tooa au processus principal.</span><span class="sxs-lookup"><span data-stu-id="30853-117">hello application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="30853-118">Autre architecture : Sites Web et WebJobs</span><span class="sxs-lookup"><span data-stu-id="30853-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="30853-119">Ce didacticiel montre comment toorun frontaux et principaux dans Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="30853-119">This tutorial shows how toorun both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="30853-120">Une autre solution consiste à hello toorun frontal dans une [site Web Azure](/services/web-sites/) et utiliser hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) fonctionnalité (actuellement en version préliminaire) pour le serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="30853-120">An alternative is toorun hello front-end in an [Azure website](/services/web-sites/) and use hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for hello back-end.</span></span> <span data-ttu-id="30853-121">Pour obtenir un didacticiel qui utilise des tâches Web, consultez [prise en main hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="30853-121">For a tutorial that uses WebJobs, see [Get Started with hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="30853-122">Pour plus d’informations sur comment toochoose hello services mieux adapter à votre scénario, consultez [comparaison de sites Web Azure, Services de cloud computing et machines virtuelles](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="30853-122">For information about how toochoose hello services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="30853-123">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="30853-123">What you'll learn</span></span>
* <span data-ttu-id="30853-124">Comment tooenable votre ordinateur pour le développement Azure en installant hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="30853-124">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="30853-125">Projet de service avec un rôle web d’ASP.NET MVC et un rôle de travail cloud toocreate Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30853-125">How toocreate a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="30853-126">Comment tootest hello projet de service cloud localement, à l’aide d’émulateur de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="30853-126">How tootest hello cloud service project locally, using hello Azure storage emulator.</span></span>
* <span data-ttu-id="30853-127">Comment toopublish hello cloud projet tooan Azure cloud service et tester à l’aide d’un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="30853-127">How toopublish hello cloud project tooan Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="30853-128">Comment tooupload les fichiers et les stocker dans le service d’objets Blob Azure hello.</span><span class="sxs-lookup"><span data-stu-id="30853-128">How tooupload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="30853-129">Comment toouse hello service de file d’attente Azure pour la communication entre les couches.</span><span class="sxs-lookup"><span data-stu-id="30853-129">How toouse hello Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30853-130">Composants requis</span><span class="sxs-lookup"><span data-stu-id="30853-130">Prerequisites</span></span>
<span data-ttu-id="30853-131">Hello didacticiel suppose que vous comprenez [concepts de base sur Azure cloud services](cloud-services-choose-me.md) comme *rôle web* et *rôle de travail* terminologie.</span><span class="sxs-lookup"><span data-stu-id="30853-131">hello tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="30853-132">Il suppose également que vous savez comment toowork avec [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) ou [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projets dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30853-132">It also assumes that you know how toowork with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="30853-133">exemple d’application Hello utilise MVC, mais hello didacticiel s’applique également tooWeb Forms.</span><span class="sxs-lookup"><span data-stu-id="30853-133">hello sample application uses MVC, but most of hello tutorial also applies tooWeb Forms.</span></span>

<span data-ttu-id="30853-134">Vous pouvez exécuter des application hello localement sans un abonnement Azure, mais vous aurez besoin d’un cloud de toohello application hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="30853-134">You can run hello app locally without an Azure subscription, but you'll need one toodeploy hello application toohello cloud.</span></span> <span data-ttu-id="30853-135">Si vous n’avez pas de compte, vous pouvez [activer les avantages de votre abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) ou [demander une évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="30853-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="30853-136">instructions des didacticiels de Hello fonctionnent avec l’option de hello suite de produits :</span><span class="sxs-lookup"><span data-stu-id="30853-136">hello tutorial instructions work with either of hello following products:</span></span>

* <span data-ttu-id="30853-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="30853-137">Visual Studio 2013</span></span>
* <span data-ttu-id="30853-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="30853-138">Visual Studio 2015</span></span>
* <span data-ttu-id="30853-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="30853-139">Visual Studio 2017</span></span>

<span data-ttu-id="30853-140">Si vous n’avez pas un de ces, Visual Studio peuvent être installé automatiquement lorsque vous installez hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="30853-140">If you don't have one of these, Visual Studio may be installed automatically when you install hello Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="30853-141">Architecture de l'application</span><span class="sxs-lookup"><span data-stu-id="30853-141">Application architecture</span></span>
<span data-ttu-id="30853-142">application Hello stocke des publicités dans une base de données SQL, à l’aide des tables de hello toocreate Entity Framework Code First et accéder aux données de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-142">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="30853-143">Pour chaque annonce, hello de base de données stocke deux URL, une pour hello image plein écran et l’autre pour l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-143">For each ad, hello database stores two URLs, one for hello full-size image and one for hello thumbnail.</span></span>

![Ad table](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="30853-145">Lorsqu’un utilisateur télécharge une image, hello frontal en cours d’exécution dans un rôle web stocke image hello dans un [objets blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), et stocke des informations d’Active Directory hello dans base de données hello avec une URL qui pointe toohello blob.</span><span class="sxs-lookup"><span data-stu-id="30853-145">When a user uploads an image, hello front-end running in a web role stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="30853-146">AT hello même temps, il écrit un message de tooan file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="30853-146">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="30853-147">Un processus principal en cours d’exécution régulièrement dans un rôle de travail interroge la file d’attente hello pour les nouveaux messages.</span><span class="sxs-lookup"><span data-stu-id="30853-147">A back-end process running in a worker role periodically polls hello queue for new messages.</span></span> <span data-ttu-id="30853-148">Quand un nouveau message s’affiche, rôle de travail hello crée une miniature pour cette image et les mises à jour hello miniature champ de base de données d’URL pour qu’ad.</span><span class="sxs-lookup"><span data-stu-id="30853-148">When a new message appears, hello worker role creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="30853-149">Hello diagramme suivant montre comment hello de l’application hello interagissent.</span><span class="sxs-lookup"><span data-stu-id="30853-149">hello following diagram shows how hello parts of hello application interact.</span></span>

![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a><span data-ttu-id="30853-151">Téléchargez et exécutez la solution de hello terminée</span><span class="sxs-lookup"><span data-stu-id="30853-151">Download and run hello completed solution</span></span>
1. <span data-ttu-id="30853-152">Téléchargez et décompressez hello [complété solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="30853-152">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="30853-153">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30853-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="30853-154">À partir de hello **fichier** menu Choisissez **ouvrir un projet**, accédez toowhere que vous avez téléchargé les solutions hello et puis ouvrez le fichier de solution hello.</span><span class="sxs-lookup"><span data-stu-id="30853-154">From hello **File** menu choose **Open Project**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="30853-155">Appuyez sur solution de hello toobuild CTRL + MAJ + B.</span><span class="sxs-lookup"><span data-stu-id="30853-155">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="30853-156">Par défaut, Visual Studio restaure automatiquement le contenu du package NuGet hello, qui n’est pas compris dans hello *.zip* fichier.</span><span class="sxs-lookup"><span data-stu-id="30853-156">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="30853-157">Si les packages hello ne sont pas restaurées, installez-les manuellement en accédant de toohello **gérer les Packages NuGet pour la Solution** boîte de dialogue et en cliquant sur hello **restaurer** bouton à droite en haut hello.</span><span class="sxs-lookup"><span data-stu-id="30853-157">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog box and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="30853-158">Dans **l’Explorateur de solutions**, assurez-vous que **ContosoAdsCloudService** est sélectionné comme projet de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="30853-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as hello startup project.</span></span>
6. <span data-ttu-id="30853-159">Si vous utilisez Visual Studio 2015 ou version ultérieure, chaîne de connexion SQL Server hello dans l’application hello *Web.config* fichier de projet de ContosoAdsWeb hello et hello *ServiceConfiguration.Local.cscfg* le fichier de projet de ContosoAdsCloudService hello.</span><span class="sxs-lookup"><span data-stu-id="30853-159">If you're using Visual Studio 2015 or higher, change hello SQL Server connection string in hello application *Web.config* file of hello ContosoAdsWeb project and in hello *ServiceConfiguration.Local.cscfg* file of hello ContosoAdsCloudService project.</span></span> <span data-ttu-id="30853-160">Dans chaque cas, « (localdb) \v11.0 » également modifier « (localdb) \MSSQLLocalDB ».</span><span class="sxs-lookup"><span data-stu-id="30853-160">In each case, change "(localdb)\v11.0" too"(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="30853-161">Appuyez sur la touche application de hello toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="30853-161">Press CTRL+F5 toorun hello application.</span></span>

    <span data-ttu-id="30853-162">Lorsque vous exécutez un projet de service cloud localement, Visual Studio appelle automatiquement hello Azure *émulateur de calcul* et Azure *l’émulateur de stockage*.</span><span class="sxs-lookup"><span data-stu-id="30853-162">When you run a cloud service project locally, Visual Studio automatically invokes hello Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="30853-163">utilisations de l’émulateur de calcul Hello rôle web de votre ordinateur ressources toosimulate hello et les environnements de rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="30853-163">hello compute emulator uses your computer's resources toosimulate hello web role and worker role environments.</span></span> <span data-ttu-id="30853-164">l’émulateur de stockage Hello utilise un [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) toosimulate stockage du cloud Azure de base de données.</span><span class="sxs-lookup"><span data-stu-id="30853-164">hello storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database toosimulate Azure cloud storage.</span></span>

    <span data-ttu-id="30853-165">Hello première fois que vous exécutez un projet de service cloud, il prend environ une minute pour toostart d’émulateurs hello des.</span><span class="sxs-lookup"><span data-stu-id="30853-165">hello first time you run a cloud service project, it takes a minute or so for hello emulators toostart up.</span></span> <span data-ttu-id="30853-166">Lors du démarrage d’émulateur terminé, navigateur par défaut de hello ouvre la page d’accueil toohello application.</span><span class="sxs-lookup"><span data-stu-id="30853-166">When emulator startup is finished, hello default browser opens toohello application home page.</span></span>

    ![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="30853-168">Cliquez sur **Créer une publicité**.</span><span class="sxs-lookup"><span data-stu-id="30853-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="30853-169">Entrez des données de test et sélectionnez un *.jpg* tooupload de l’image, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="30853-169">Enter some test data and select a *.jpg* image tooupload, and then click **Create**.</span></span>

    ![Create page](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="30853-171">application Hello passe toohello page d’Index, mais elle n’affiche une miniature de publicité hello parce que ce traitement n’a pas encore s’est produite.</span><span class="sxs-lookup"><span data-stu-id="30853-171">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="30853-172">Patientez quelques instants, puis actualisez hello Index toosee hello vignette.</span><span class="sxs-lookup"><span data-stu-id="30853-172">Wait a moment and then refresh hello Index page toosee hello thumbnail.</span></span>

     ![Page d'index](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="30853-174">Cliquez sur **détails** pour votre image en taille réelle d’ad toosee hello.</span><span class="sxs-lookup"><span data-stu-id="30853-174">Click **Details** for your ad toosee hello full-size image.</span></span>

     ![Details page](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="30853-176">Vous avez déjà exécuté application hello entièrement sur votre ordinateur local, sans cloud toohello de connexion.</span><span class="sxs-lookup"><span data-stu-id="30853-176">You've been running hello application entirely on your local computer, with no connection toohello cloud.</span></span> <span data-ttu-id="30853-177">émulateur de stockage Hello stocke la file d’attente hello et les données blob dans une base de données SQL Server Express LocalDB et application hello stocke des données d’Active Directory de hello dans une autre base de données de base de données locale.</span><span class="sxs-lookup"><span data-stu-id="30853-177">hello storage emulator stores hello queue and blob data in a SQL Server Express LocalDB database, and hello application stores hello ad data in another LocalDB database.</span></span> <span data-ttu-id="30853-178">Entity Framework Code First hello créé automatiquement base de données ad hello première tooaccess a tenté de l’application web hello il.</span><span class="sxs-lookup"><span data-stu-id="30853-178">Entity Framework Code First automatically created hello ad database hello first time hello web app tried tooaccess it.</span></span>

<span data-ttu-id="30853-179">Bonjour, suivant la section vous allez configurer les ressources de cloud computing Azure toouse la solution hello pour les files d’attente, les objets BLOB et base de données application hello lorsqu’il s’exécute dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-179">In hello following section you'll configure hello solution toouse Azure cloud resources for queues, blobs, and hello application database when it runs in hello cloud.</span></span> <span data-ttu-id="30853-180">Si vous souhaitiez toorun toocontinue localement mais utilisez des ressources de base de données et de stockage cloud, vous pouvez le faire.</span><span class="sxs-lookup"><span data-stu-id="30853-180">If you wanted toocontinue toorun locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="30853-181">Il vous suffit de la définition de chaînes de connexion, vous verrez comment toodo.</span><span class="sxs-lookup"><span data-stu-id="30853-181">It's just a matter of setting connection strings, which you'll see how toodo.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="30853-182">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="30853-182">Deploy hello application tooAzure</span></span>
<span data-ttu-id="30853-183">Vous effectuerez hello après application de hello toorun étapes dans le cloud de hello :</span><span class="sxs-lookup"><span data-stu-id="30853-183">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="30853-184">Créez un service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="30853-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="30853-185">Créez une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="30853-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="30853-186">Créez un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="30853-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="30853-187">Configurer hello solution toouse votre base de données SQL Azure lorsqu’elle s’exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="30853-187">Configure hello solution toouse your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="30853-188">Configurer hello solution toouse votre compte de stockage Azure lorsqu’elle s’exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="30853-188">Configure hello solution toouse your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="30853-189">Déployer un service de cloud computing Azure hello projet tooyour.</span><span class="sxs-lookup"><span data-stu-id="30853-189">Deploy hello project tooyour Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="30853-190">Création d'un service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="30853-190">Create an Azure cloud service</span></span>
<span data-ttu-id="30853-191">Un service cloud Azure est hello environnement hello application s’exécutera dans.</span><span class="sxs-lookup"><span data-stu-id="30853-191">An Azure cloud service is hello environment hello application will run in.</span></span>

1. <span data-ttu-id="30853-192">Dans votre navigateur, ouvrez hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="30853-192">In your browser, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="30853-193">Cliquez sur **Nouveau > Compute > Service cloud**.</span><span class="sxs-lookup"><span data-stu-id="30853-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="30853-194">Dans la zone d’entrée du nom DNS hello, entrez un préfixe d’URL pour le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="30853-194">In hello DNS name input box, enter a URL prefix for hello cloud service.</span></span>

    <span data-ttu-id="30853-195">Cette URL a toobe unique.</span><span class="sxs-lookup"><span data-stu-id="30853-195">This URL has toobe unique.</span></span>  <span data-ttu-id="30853-196">Vous obtenez un message d’erreur si vous choisissez de préfixe de hello est déjà en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="30853-196">You'll get an error message if hello prefix you choose is already in use.</span></span>
4. <span data-ttu-id="30853-197">Spécifiez un groupe de ressources pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-197">Specify a new Resource group for hello  service.</span></span> <span data-ttu-id="30853-198">Cliquez sur **nouvel** puis tapez un nom dans hello ressource groupe zone d’entrée, tels que CS_contososadsRG.</span><span class="sxs-lookup"><span data-stu-id="30853-198">Click **Create new** and then type a name in hello Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="30853-199">Choisissez une région où vous souhaitez application hello de toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="30853-199">Choose hello region where you want toodeploy hello application.</span></span>

    <span data-ttu-id="30853-200">Ce champ indique le centre de données dans lequel votre service cloud sera hébergé.</span><span class="sxs-lookup"><span data-stu-id="30853-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="30853-201">Pour une application de production, vous choisissez les clients tooyour le plus proche hello région.</span><span class="sxs-lookup"><span data-stu-id="30853-201">For a production application, you'd choose hello region closest tooyour customers.</span></span> <span data-ttu-id="30853-202">Pour ce didacticiel, choisissez tooyou le plus proche de la région de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-202">For this tutorial, choose hello region closest tooyou.</span></span>
5. <span data-ttu-id="30853-203">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="30853-203">Click **Create**.</span></span>

    <span data-ttu-id="30853-204">Bonjour suivant l’image, un service cloud est créé par hello CSvccontosoads.cloudapp.net d’URL.</span><span class="sxs-lookup"><span data-stu-id="30853-204">In hello following image, a cloud service is created with hello URL CSvccontosoads.cloudapp.net.</span></span>

    ![New Cloud Service](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="30853-206">Création d’une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="30853-206">Create an Azure SQL database</span></span>
<span data-ttu-id="30853-207">Lorsque l’application hello s’exécute dans le cloud de hello, il utilise une base de données en nuage.</span><span class="sxs-lookup"><span data-stu-id="30853-207">When hello app runs in hello cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="30853-208">Bonjour [portail Azure](https://portal.azure.com), cliquez sur **Nouveau > bases de données > base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="30853-208">In hello [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="30853-209">Bonjour **nom de la base de données** , entrez *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="30853-209">In hello **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="30853-210">Bonjour **groupe de ressources**, cliquez sur **utiliser l’existante** et groupe de ressources hello sélectionnez utilisé pour le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="30853-210">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
4. <span data-ttu-id="30853-211">Bonjour suivant de l’image, cliquez sur **Server - configurer les paramètres requis** et **créer un nouveau serveur**.</span><span class="sxs-lookup"><span data-stu-id="30853-211">In hello following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Serveur toodatabase de tunnel](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="30853-213">Vous pouvez également, si votre abonnement possède déjà un serveur, vous pouvez sélectionner ce serveur à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-213">Alternatively, if your subscription already has a server, you can select that server from hello drop-down list.</span></span>
5. <span data-ttu-id="30853-214">Bonjour **nom du serveur** , entrez *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="30853-214">In hello **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="30853-215">Entrez un **Nom de connexion** et un **Mot de passe** d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="30853-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="30853-216">Si vous avez sélectionné **Créer un serveur**, vous ne devez pas entrer un nom et un mot de passe existants ici.</span><span class="sxs-lookup"><span data-stu-id="30853-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="30853-217">Vous entrez un nouveau nom et mot de passe que vous définissez maintenant toouse ultérieurement lorsque vous accédez à la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="30853-217">You're entering a new name and password that you're defining now toouse later when you access hello database.</span></span> <span data-ttu-id="30853-218">Si vous avez sélectionné un serveur que vous avez créé précédemment, vous êtes invité à entrer pour le compte d’utilisateur administratif hello mot de passe toohello vous avez déjà créé.</span><span class="sxs-lookup"><span data-stu-id="30853-218">If you selected a server that you created previously, you'll be prompted for hello password toohello administrative user account you already created.</span></span>
7. <span data-ttu-id="30853-219">Choisissez hello même **emplacement** que vous avez choisi pour le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="30853-219">Choose hello same **Location** that you chose for hello cloud service.</span></span>

    <span data-ttu-id="30853-220">Lorsque le service de cloud computing hello et la base de données sont dans différents centres de données (différentes régions), la latence augmentera, et vous serez facturé pour la bande passante en dehors du centre de données hello.</span><span class="sxs-lookup"><span data-stu-id="30853-220">When hello cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="30853-221">alors qu'elle est gratuite dans un centre de données.</span><span class="sxs-lookup"><span data-stu-id="30853-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="30853-222">Vérifiez **server d’Autoriser les services azure tooaccess**.</span><span class="sxs-lookup"><span data-stu-id="30853-222">Check **Allow azure services tooaccess server**.</span></span>
9. <span data-ttu-id="30853-223">Cliquez sur **sélectionnez** pour le nouveau serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-223">Click **Select** for hello new server.</span></span>

    ![Nouveau serveur SQL Database](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="30853-225">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="30853-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="30853-226">Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="30853-226">Create an Azure storage account</span></span>
<span data-ttu-id="30853-227">Un compte de stockage Azure fournit des ressources pour le stockage de la file d’attente et les données blob dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-227">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span>

<span data-ttu-id="30853-228">Dans une application réelle, on crée généralement des comptes distincts pour les données d'application et les données de journalisation, et des comptes distincts pour les données de test et les données de production.</span><span class="sxs-lookup"><span data-stu-id="30853-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="30853-229">Pour ce didacticiel, vous allez utiliser un seul compte.</span><span class="sxs-lookup"><span data-stu-id="30853-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="30853-230">Bonjour [portail Azure](https://portal.azure.com), cliquez sur **Nouveau > stockage > compte de stockage - objet blob, de fichier, de table, de file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="30853-230">In hello [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="30853-231">Bonjour **nom** , entrez un préfixe d’URL.</span><span class="sxs-lookup"><span data-stu-id="30853-231">In hello **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="30853-232">Ce texte de préfixe plus hello que sous la zone de hello sera le compte de stockage hello unique URL tooyour.</span><span class="sxs-lookup"><span data-stu-id="30853-232">This prefix plus hello text you see under hello box will be hello unique URL tooyour storage account.</span></span> <span data-ttu-id="30853-233">Si le préfixe hello que vous entrez a déjà été utilisé par quelqu'un d’autre, vous devrez toochoose un préfixe différent.</span><span class="sxs-lookup"><span data-stu-id="30853-233">If hello prefix you enter has already been used by someone else, you'll have toochoose a different prefix.</span></span>
3. <span data-ttu-id="30853-234">Ensemble hello **modèle de déploiement** trop*classique*.</span><span class="sxs-lookup"><span data-stu-id="30853-234">Set hello **Deployment model** too*Classic*.</span></span>

4. <span data-ttu-id="30853-235">Ensemble hello **réplication** déroulante liste trop**stockage localement redondant**.</span><span class="sxs-lookup"><span data-stu-id="30853-235">Set hello **Replication** drop-down list too**Locally redundant storage**.</span></span>

    <span data-ttu-id="30853-236">Lors de la géo-réplication est activée pour un compte de stockage, le contenu stockée hello est répliquées tooa centre de données secondaire tooenable basculement cas de sinistre majeur dans l’emplacement principal de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-236">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover if a major disaster occurs in hello primary location.</span></span> <span data-ttu-id="30853-237">La géo-réplication peut engendrer des coûts supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="30853-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="30853-238">Pour les comptes de test et de développement, généralement non désirés toopay pour la géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="30853-238">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="30853-239">Pour plus d’informations, consultez [Création, gestion ou suppression d’un compte de stockage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="30853-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="30853-240">Bonjour **groupe de ressources**, cliquez sur **utiliser l’existante** et groupe de ressources hello sélectionnez utilisé pour le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="30853-240">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
6. <span data-ttu-id="30853-241">Ensemble hello **emplacement** toohello de liste déroulante, même région que vous avez choisi pour le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="30853-241">Set hello **Location** drop-down list toohello same region you chose for hello cloud service.</span></span>

    <span data-ttu-id="30853-242">Lorsque le compte de service et le stockage cloud hello se trouvent dans différents centres de données (différentes régions), la latence augmentera, et vous serez facturé pour la bande passante en dehors du centre de données hello.</span><span class="sxs-lookup"><span data-stu-id="30853-242">When hello cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="30853-243">alors qu'elle est gratuite dans un centre de données.</span><span class="sxs-lookup"><span data-stu-id="30853-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="30853-244">Les groupes d’affinités Azure fournissent une mécanisme toominimize hello la distance entre les ressources dans un centre de données, ce qui peut réduire la latence.</span><span class="sxs-lookup"><span data-stu-id="30853-244">Azure affinity groups provide a mechanism toominimize hello distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="30853-245">Ce didacticiel n'utilise pas de groupes d'affinités.</span><span class="sxs-lookup"><span data-stu-id="30853-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="30853-246">Pour plus d’informations, consultez [comment tooCreate une affinité de groupe dans Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="30853-246">For more information, see [How tooCreate an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="30853-247">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="30853-247">Click **Create**.</span></span>

    ![New storage account](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="30853-249">Dans l’image de hello, un compte de stockage est créé avec l’URL de hello `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="30853-249">In hello image, a storage account is created with hello URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="30853-250">Configurer hello solution toouse votre base de données SQL Azure lorsqu’elle s’exécute dans Azure</span><span class="sxs-lookup"><span data-stu-id="30853-250">Configure hello solution toouse your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="30853-251">Hello projet web et chaque projet de rôle Collaborateur hello possède sa propre chaîne de connexion de base de données, et chacune a besoin d’une base de données SQL Azure toopoint toohello lors de l’application hello s’exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="30853-251">hello web project and hello worker role project each has its own database connection string, and each needs toopoint toohello Azure SQL database when hello app runs in Azure.</span></span>

<span data-ttu-id="30853-252">Vous allez utiliser un [transformation Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) pour un rôle web de hello et un paramètre d’environnement de service cloud pour le rôle de travail hello.</span><span class="sxs-lookup"><span data-stu-id="30853-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for hello web role and a cloud service environment setting for hello worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="30853-253">Dans cette section et la section suivante de hello, vous stockez les informations d’identification dans les fichiers projet.</span><span class="sxs-lookup"><span data-stu-id="30853-253">In this section and hello next section, you store credentials in project files.</span></span> <span data-ttu-id="30853-254">[Ne stockez pas d'informations confidentielles dans des référentiels de code source publics](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="30853-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="30853-255">Dans le projet de ContosoAdsWeb hello, ouvrez hello *Web.Release.config* fichier de transformation de l’application hello *Web.config* , supprimez le bloc de commentaires hello contenant un `<connectionStrings>` élément et coller Hello suivant du code à la place.</span><span class="sxs-lookup"><span data-stu-id="30853-255">In hello ContosoAdsWeb project, open hello *Web.Release.config* transform file for hello application *Web.config* file, delete hello comment block that contains a `<connectionStrings>` element, and paste hello following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="30853-256">Laissez le fichier de hello ouvert pour modification.</span><span class="sxs-lookup"><span data-stu-id="30853-256">Leave hello file open for editing.</span></span>
2. <span data-ttu-id="30853-257">Bonjour [portail Azure](https://portal.azure.com), cliquez sur **bases de données SQL** dans le volet gauche de hello, cliquez sur base de données hello vous avez créé pour ce didacticiel, puis cliquez sur **afficher les chaînes de connexion**.</span><span class="sxs-lookup"><span data-stu-id="30853-257">In hello [Azure portal](https://portal.azure.com), click **SQL Databases** in hello left pane, click hello database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Afficher les chaînes de connexion](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="30853-259">portail de Hello affiche les chaînes de connexion, avec un espace réservé pour le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="30853-259">hello portal displays connection strings, with a placeholder for hello password.</span></span>

    ![Chaînes de connexion](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="30853-261">Bonjour *Web.Release.config* de transformer le fichier, supprimez `{connectionstring}` et collez dans sa chaîne de connexion ADO.NET hello portail Azure de hello sur place.</span><span class="sxs-lookup"><span data-stu-id="30853-261">In hello *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place hello ADO.NET connection string from hello Azure portal.</span></span>
4. <span data-ttu-id="30853-262">Dans la chaîne de connexion hello que vous avez collé dans hello *Web.Release.config* de transformer le fichier, remplacez `{your_password_here}` avec le mot de passe hello créé pour la base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="30853-262">In hello connection string that you pasted into hello *Web.Release.config* transform file, replace `{your_password_here}` with hello password you created for hello new SQL database.</span></span>
5. <span data-ttu-id="30853-263">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-263">Save hello file.</span></span>  
6. <span data-ttu-id="30853-264">Sélectionnez et copiez la chaîne de connexion hello (sans hello entourant les guillemets) pour une utilisation dans hello comme suit pour configurer le projet de rôle de travail hello.</span><span class="sxs-lookup"><span data-stu-id="30853-264">Select and copy hello connection string (without hello surrounding quotation marks) for use in hello following steps for configuring hello worker role project.</span></span>
7. <span data-ttu-id="30853-265">Dans **l’Explorateur de solutions**, sous **rôles** dans le projet de service cloud hello, cliquez sur **ContosoAdsWorker** puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="30853-265">In **Solution Explorer**, under **Roles** in hello cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="30853-267">Cliquez sur hello **paramètres** onglet.</span><span class="sxs-lookup"><span data-stu-id="30853-267">Click hello **Settings** tab.</span></span>
9. <span data-ttu-id="30853-268">Modification **Configuration du Service** trop**Cloud**.</span><span class="sxs-lookup"><span data-stu-id="30853-268">Change **Service Configuration** too**Cloud**.</span></span>
10. <span data-ttu-id="30853-269">Sélectionnez hello **valeur** champ hello `ContosoAdsDbConnectionString` définition, puis collez la chaîne de connexion hello que vous avez copié à partir de la section précédente de hello du didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-269">Select hello **Value** field for hello `ContosoAdsDbConnectionString` setting, and then paste hello connection string that you copied from hello previous section of hello tutorial.</span></span>

     ![Database connection string for worker role](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="30853-271">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="30853-271">Save your changes.</span></span>  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="30853-272">Configurer hello solution toouse votre compte de stockage Azure lorsqu’elle s’exécute dans Azure</span><span class="sxs-lookup"><span data-stu-id="30853-272">Configure hello solution toouse your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="30853-273">Chaînes de connexion de compte de stockage Azure pour le projet de rôle web hello et projet de rôle de travail hello sont stockées dans les paramètres d’environnement dans le projet de service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="30853-273">Azure storage account connection strings for both hello web role project and hello worker role project are stored in environment settings in hello cloud service project.</span></span> <span data-ttu-id="30853-274">Pour chaque projet, il existe un ensemble distinct de toobe de paramètres utilisé lors de l’application hello s’exécute localement et lorsqu’elle est exécutée dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-274">For each project, there is a separate set of settings toobe used when hello application runs locally and when it runs in hello cloud.</span></span> <span data-ttu-id="30853-275">Vous allez mettre à jour les paramètres d’environnement cloud hello pour les projets de rôle web et de travail.</span><span class="sxs-lookup"><span data-stu-id="30853-275">You'll update hello cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="30853-276">Dans **l’Explorateur de solutions**, avec le bouton droit **ContosoAdsWeb** sous **rôles** Bonjour **ContosoAdsCloudService** de projet, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="30853-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in hello **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="30853-278">Cliquez sur hello **paramètres** onglet. Bonjour **Configuration du Service** liste déroulante, choisissez **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="30853-278">Click hello **Settings** tab. In hello **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Cloud configuration](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="30853-280">Sélectionnez hello **StorageConnectionString** entrée et vous verrez des points de suspension (**...** ) situé à droite de hello de ligne de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-280">Select hello **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at hello right end of hello line.</span></span> <span data-ttu-id="30853-281">Cliquez sur hello de tooopen de bouton de points de suspension hello **chaîne de connexion du compte de stockage créer** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="30853-281">Click hello ellipsis button tooopen hello **Create Storage Account Connection String** dialog box.</span></span>

    ![Open Connection String Create box](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="30853-283">Bonjour **créer une chaîne de connexion stockage** boîte de dialogue, cliquez sur **votre abonnement**, choisissez le compte de stockage hello que vous avez créé précédemment, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="30853-283">In hello **Create Storage Connection String** dialog box, click **Your subscription**, choose hello storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="30853-284">Si vous n'êtes pas déjà connecté, vous êtes invité à entrer vos informations d'identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="30853-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Create Storage Connection String](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="30853-286">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="30853-286">Save your changes.</span></span>
6. <span data-ttu-id="30853-287">Suivez hello même procédure que celle utilisée pour hello `StorageConnectionString` hello de tooset de chaîne de connexion `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="30853-287">Follow hello same procedure that you used for hello `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="30853-288">Cette chaîne de connexion est utilisée pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="30853-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="30853-289">Suivez hello même procédure que celle utilisée pour hello **ContosoAdsWeb** tooset de rôle les deux chaînes de connexion pour hello **ContosoAdsWorker** rôle.</span><span class="sxs-lookup"><span data-stu-id="30853-289">Follow hello same procedure that you used for hello **ContosoAdsWeb** role tooset both connection strings for hello **ContosoAdsWorker** role.</span></span> <span data-ttu-id="30853-290">N’oubliez pas tooset **Configuration du Service** trop**Cloud**.</span><span class="sxs-lookup"><span data-stu-id="30853-290">Don't forget tooset **Service Configuration** too**Cloud**.</span></span>

<span data-ttu-id="30853-291">paramètres d’environnement Hello rôle que vous avez configuré à l’aide de hello interface utilisateur Visual Studio sont stockés dans hello fichiers dans le projet de ContosoAdsCloudService hello suivants :</span><span class="sxs-lookup"><span data-stu-id="30853-291">hello role environment settings that you have configured using hello Visual Studio UI are stored in hello following files in hello ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="30853-292">*ServiceDefinition.csdef* -définit les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="30853-292">*ServiceDefinition.csdef* - Defines hello setting names.</span></span>
* <span data-ttu-id="30853-293">*ServiceConfiguration.Cloud.cscfg* -fournit des valeurs d’exécution dans le cloud de hello application hello.</span><span class="sxs-lookup"><span data-stu-id="30853-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when hello app runs in hello cloud.</span></span>
* <span data-ttu-id="30853-294">*ServiceConfiguration.Local.cscfg* -fournit des valeurs pour lorsque l’application hello exécute localement.</span><span class="sxs-lookup"><span data-stu-id="30853-294">*ServiceConfiguration.Local.cscfg* - Provides values for when hello app runs locally.</span></span>

<span data-ttu-id="30853-295">Par exemple, hello ServiceDefinition.csdef inclut hello suivant des définitions :</span><span class="sxs-lookup"><span data-stu-id="30853-295">For example, hello ServiceDefinition.csdef includes hello following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="30853-296">Et hello *ServiceConfiguration.Cloud.cscfg* fichier inclut les valeurs hello saisies pour ces paramètres dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30853-296">And hello *ServiceConfiguration.Cloud.cscfg* file includes hello values you entered for those settings in Visual Studio.</span></span>

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

<span data-ttu-id="30853-297">Hello `<Instances>` paramètre spécifie le nombre de hello de machines virtuelles Azure sur laquelle s’exécutera travailleur de hello code du rôle.</span><span class="sxs-lookup"><span data-stu-id="30853-297">hello `<Instances>` setting specifies hello number of virtual machines that Azure will run hello worker role code on.</span></span> <span data-ttu-id="30853-298">Hello [étapes](#next-steps) section inclut des informations de toomore de liens sur la montée en puissance parallèle d’un service cloud,</span><span class="sxs-lookup"><span data-stu-id="30853-298">hello [Next steps](#next-steps) section includes links toomore information about scaling out a cloud service,</span></span>

### <a name="deploy-hello-project-tooazure"></a><span data-ttu-id="30853-299">Déployer hello projet tooAzure</span><span class="sxs-lookup"><span data-stu-id="30853-299">Deploy hello project tooAzure</span></span>
1. <span data-ttu-id="30853-300">Dans **l’Explorateur de solutions**, avec le bouton hello **ContosoAdsCloudService** cloud du projet, puis sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="30853-300">In **Solution Explorer**, right-click hello **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Publish menu](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="30853-302">Bonjour **connectez-vous** étape Hello **publier l’Application Azure** Assistant, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="30853-302">In hello **Sign in** step of hello **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Sign in step](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="30853-304">Bonjour **paramètres** étape de l’Assistant de hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="30853-304">In hello **Settings** step of hello wizard, click **Next**.</span></span>

    ![Settings step](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="30853-306">Hello des paramètres par défaut dans hello **avancé** onglet conviennent pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="30853-306">hello default settings in hello **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="30853-307">Pour plus d’informations sur l’onglet Avancé de hello, consultez [Assistant Publication d’Application Azure](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="30853-307">For information about hello advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="30853-308">Bonjour **Résumé** étape, cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="30853-308">In hello **Summary** step, click **Publish**.</span></span>

    ![Summary step](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="30853-310">Hello **journal des activités Azure** fenêtre s’ouvre dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30853-310">hello **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="30853-311">Cliquez sur Détails du déploiement icône tooexpand hello hello flèche droite.</span><span class="sxs-lookup"><span data-stu-id="30853-311">Click hello right arrow icon tooexpand hello deployment details.</span></span>

    <span data-ttu-id="30853-312">déploiement de Hello peut prendre jusqu'à too5 minutes ou plus toocomplete.</span><span class="sxs-lookup"><span data-stu-id="30853-312">hello deployment can take up too5 minutes or more toocomplete.</span></span>

    ![Azure Activity Log window](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="30853-314">Lorsque l’état du déploiement hello est terminée, cliquez sur hello **URL de l’application Web** application hello de toostart.</span><span class="sxs-lookup"><span data-stu-id="30853-314">When hello deployment status is complete, click hello **Web app URL** toostart hello application.</span></span>
7. <span data-ttu-id="30853-315">Vous pouvez maintenant tester application hello par la création, affichage et modification des annonces, comme vous le faisiez lorsque vous avez exécuté localement application hello.</span><span class="sxs-lookup"><span data-stu-id="30853-315">You can now test hello app by creating, viewing, and editing some ads, as you did when you ran hello application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="30853-316">Lorsque vous avez terminé de tester, supprimer ou arrêter le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="30853-316">When you're finished testing, delete or stop hello cloud service.</span></span> <span data-ttu-id="30853-317">Même si vous n’utilisez pas le service de cloud computing hello, il accumule des frais, car les ressources d’ordinateur virtuel sont réservées.</span><span class="sxs-lookup"><span data-stu-id="30853-317">Even if you're not using hello cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="30853-318">Si vous le laissez s'exécuter, toute personne qui trouve votre URL peut créer et afficher des publicités.</span><span class="sxs-lookup"><span data-stu-id="30853-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="30853-319">Bonjour [portail Azure](https://portal.azure.com), accédez toohello **vue d’ensemble** onglet pour votre service cloud, puis cliquez sur hello **supprimer** bouton en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="30853-319">In hello [Azure portal](https://portal.azure.com), go toohello **Overview** tab for your cloud service, and then click hello **Delete** button at hello top of hello page.</span></span> <span data-ttu-id="30853-320">Si vous souhaitez simplement tootemporarily empêcher d’autres utilisateurs d’accéder au site de hello, cliquez sur **arrêter** à la place.</span><span class="sxs-lookup"><span data-stu-id="30853-320">If you just want tootemporarily prevent others from accessing hello site, click **Stop** instead.</span></span> <span data-ttu-id="30853-321">Dans ce cas, interrompt tooaccrue.</span><span class="sxs-lookup"><span data-stu-id="30853-321">In that case, charges will continue tooaccrue.</span></span> <span data-ttu-id="30853-322">Vous pouvez suivre un Bonjour de toodelete procédure comme compte de stockage et de la base de données SQL lorsque vous n’en avez plus besoin.</span><span class="sxs-lookup"><span data-stu-id="30853-322">You can follow a similar procedure toodelete hello SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-hello-application-from-scratch"></a><span data-ttu-id="30853-323">Créer l’application hello à partir de zéro</span><span class="sxs-lookup"><span data-stu-id="30853-323">Create hello application from scratch</span></span>
<span data-ttu-id="30853-324">Si vous n’avez pas encore téléchargé [application hello terminée](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), faites-le maintenant.</span><span class="sxs-lookup"><span data-stu-id="30853-324">If you haven't already downloaded [hello completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="30853-325">Vous allez copier les fichiers de hello téléchargé projet en projet hello.</span><span class="sxs-lookup"><span data-stu-id="30853-325">You'll copy files from hello downloaded project into hello new project.</span></span>

<span data-ttu-id="30853-326">Création d’application des annonces de Contoso hello implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="30853-326">Creating hello Contoso Ads application involves hello following steps:</span></span>

* <span data-ttu-id="30853-327">création d'une solution Visual Studio de service cloud ;</span><span class="sxs-lookup"><span data-stu-id="30853-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="30853-328">mise à jour et ajout de packages NuGet ;</span><span class="sxs-lookup"><span data-stu-id="30853-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="30853-329">définition des références d'un projet ;</span><span class="sxs-lookup"><span data-stu-id="30853-329">Set project references.</span></span>
* <span data-ttu-id="30853-330">configuration des chaînes de connexion ;</span><span class="sxs-lookup"><span data-stu-id="30853-330">Configure connection strings.</span></span>
* <span data-ttu-id="30853-331">ajout de fichiers de code.</span><span class="sxs-lookup"><span data-stu-id="30853-331">Add code files.</span></span>

<span data-ttu-id="30853-332">Après la création de la solution de hello, vous allez consulter le code hello toocloud unique les projets de service et objets BLOB Windows Azure et files d’attente.</span><span class="sxs-lookup"><span data-stu-id="30853-332">After hello solution is created, you'll review hello code that is unique toocloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="30853-333">Création d'une solution Visual Studio de service cloud</span><span class="sxs-lookup"><span data-stu-id="30853-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="30853-334">Dans Visual Studio, choisissez **nouveau projet** de hello **fichier** menu.</span><span class="sxs-lookup"><span data-stu-id="30853-334">In Visual Studio, choose **New Project** from hello **File** menu.</span></span>
2. <span data-ttu-id="30853-335">Dans le volet gauche de hello Hello **nouveau projet** boîte de dialogue, développez **Visual C#** et choisissez **Cloud** modèles, puis choisissez hello **Azure Cloud Service** modèle.</span><span class="sxs-lookup"><span data-stu-id="30853-335">In hello left pane of hello **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose hello **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="30853-336">Nommez le projet de hello et une solution ContosoAdsCloudService, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="30853-336">Name hello project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Nouveau projet](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="30853-338">Bonjour **nouveau Service Cloud Azure** boîte de dialogue zone, ajouter un rôle web et un rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="30853-338">In hello **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="30853-339">Nom de rôle web de hello ContosoAdsWeb et nommez le rôle de travail hello ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="30853-339">Name hello web role ContosoAdsWeb, and name hello worker role ContosoAdsWorker.</span></span> <span data-ttu-id="30853-340">(Utilisez l’icône de crayon hello dans hello volet droit toochange hello noms par défaut des rôles de hello).</span><span class="sxs-lookup"><span data-stu-id="30853-340">(Use hello pencil icon in hello right-hand pane toochange hello default names of hello roles.)</span></span>

    ![New Cloud Service Project](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="30853-342">Lorsque vous consultez hello **nouveau projet ASP.NET** boîte de dialogue rôle web de hello, choisissez le modèle MVC de hello, puis cliquez sur **modifier l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="30853-342">When you see hello **New ASP.NET Project** dialog box for hello web role, choose hello MVC template, and then click **Change Authentication**.</span></span>

    ![Modifier l'authentification](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="30853-344">Bonjour **modifier l’authentification** boîte de dialogue, choisissez **aucune authentification**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="30853-344">In hello **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![Aucune authentification](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="30853-346">Bonjour **nouveau projet ASP.NET** boîte de dialogue, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="30853-346">In hello **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="30853-347">Dans **l’Explorateur de solutions**, avec le bouton droit de solution hello (pas un des projets de hello), puis choisissez **Ajouter - nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="30853-347">In **Solution Explorer**, right-click hello solution (not one of hello projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="30853-348">Bonjour **ajouter un nouveau projet** boîte de dialogue, choisissez **Windows** sous **Visual C#** dans hello du volet gauche, puis cliquez sur hello **bibliothèque de classes** modèle.</span><span class="sxs-lookup"><span data-stu-id="30853-348">In hello **Add New Project** dialog box, choose **Windows** under **Visual C#** in hello left pane, and then click hello **Class Library** template.</span></span>  
10. <span data-ttu-id="30853-349">Projet de hello nom *ContosoAdsCommon*, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="30853-349">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="30853-350">Vous devez tooreference hello Entity Framework hello et contexte de modèle de données à partir de projets de rôle web et de travail.</span><span class="sxs-lookup"><span data-stu-id="30853-350">You need tooreference hello Entity Framework context and hello data model from both web and worker role projects.</span></span> <span data-ttu-id="30853-351">En guise d’alternative, vous pouvez définir des classes de lié à EF hello dans le projet de rôle web hello et faire référence à ce projet à partir du projet de rôle de travail hello.</span><span class="sxs-lookup"><span data-stu-id="30853-351">As an alternative, you could define hello EF-related classes in hello web role project and reference that project from hello worker role project.</span></span> <span data-ttu-id="30853-352">Mais dans une autre approche de hello, votre projet de rôle de travail aurait un assemblys tooweb de référence qui n’a pas besoin.</span><span class="sxs-lookup"><span data-stu-id="30853-352">But in hello alternative approach, your worker role project would have a reference tooweb assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="30853-353">Mise à jour et ajout de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="30853-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="30853-354">Ouvrez hello **gérer les Packages NuGet** boîte de dialogue pour la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-354">Open hello **Manage NuGet Packages** dialog box for hello solution.</span></span>
2. <span data-ttu-id="30853-355">Haut hello de fenêtre hello, sélectionnez **mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="30853-355">At hello top of hello window, select **Updates**.</span></span>
3. <span data-ttu-id="30853-356">Recherchez hello *WindowsAzure.Storage* du package et s’il est dans la liste de hello, sélectionnez-le et sélectionnez tooupdate de projets web et de travail hello dans, puis cliquez sur **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="30853-356">Look for hello *WindowsAzure.Storage* package, and if it's in hello list, select it and select hello web and worker projects tooupdate it in, and then click **Update**.</span></span>

    <span data-ttu-id="30853-357">bibliothèque cliente de stockage Hello est mis à jour plus fréquemment que les modèles de projet Visual Studio, vous trouverez souvent que la version hello dans un toobe de besoins nouvellement créé le projet mis à jour.</span><span class="sxs-lookup"><span data-stu-id="30853-357">hello storage client library is updated more frequently than Visual Studio project templates, so you'll often find that hello version in a newly-created project needs toobe updated.</span></span>
4. <span data-ttu-id="30853-358">Haut hello de fenêtre hello, sélectionnez **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="30853-358">At hello top of hello window, select **Browse**.</span></span>
5. <span data-ttu-id="30853-359">Recherche hello *EntityFramework* NuGet package et l’installer dans les trois projets.</span><span class="sxs-lookup"><span data-stu-id="30853-359">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="30853-360">Recherche hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package et l’installer dans le projet de rôle de travail hello.</span><span class="sxs-lookup"><span data-stu-id="30853-360">Find hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in hello worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="30853-361">Définition des références de projet</span><span class="sxs-lookup"><span data-stu-id="30853-361">Set project references</span></span>
1. <span data-ttu-id="30853-362">Dans le projet de ContosoAdsWeb hello, définissez une référence de projet de ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="30853-362">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="30853-363">Projet de ContosoAdsWeb hello d’avec le bouton droit, puis cliquez sur **références** - **ajouter des références**.</span><span class="sxs-lookup"><span data-stu-id="30853-363">Right-click hello ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="30853-364">Bonjour **Gestionnaire de références** boîte de dialogue, sélectionnez **Solution – projets** dans le volet gauche de hello, sélectionnez **ContosoAdsCommon**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="30853-364">In hello **Reference Manager** dialog box, select **Solution – Projects** in hello left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="30853-365">Dans le projet de ContosoAdsWorker hello, définissez une référence de projet de ContosAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="30853-365">In hello ContosoAdsWorker project, set a reference toohello ContosAdsCommon project.</span></span>

    <span data-ttu-id="30853-366">ContosoAdsCommon contiendra hello Entity Framework modèle et le contexte de classe de données, qui sera utilisée par les deux hello frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="30853-366">ContosoAdsCommon will contain hello Entity Framework data model and context class, which will be used by both hello front-end and back-end.</span></span>
3. <span data-ttu-id="30853-367">Dans le projet de ContosoAdsWorker hello, définissez une référence trop`System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="30853-367">In hello ContosoAdsWorker project, set a reference too`System.Drawing`.</span></span>

    <span data-ttu-id="30853-368">Cet assembly est utilisé par hello principal tooconvert images toothumbnails.</span><span class="sxs-lookup"><span data-stu-id="30853-368">This assembly is used by hello back-end tooconvert images toothumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="30853-369">Configuration des chaînes de connexion</span><span class="sxs-lookup"><span data-stu-id="30853-369">Configure connection strings</span></span>
<span data-ttu-id="30853-370">Dans cette section, vous allez configurer les chaînes de connexion Azure Storage et SQL pour un test local.</span><span class="sxs-lookup"><span data-stu-id="30853-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="30853-371">instructions de déploiement de Hello plus haut dans le didacticiel de hello expliquent comment tooset connexion de hello chaînes pour quand hello application s’exécute dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-371">hello deployment instructions earlier in hello tutorial explain how tooset up hello connection strings for when hello app runs in hello cloud.</span></span>

1. <span data-ttu-id="30853-372">Hello ContosoAdsWeb projet, fichier Web.config de l’application hello ouvert, et suivant de hello insert `connectionStrings` élément après hello `configSections` élément.</span><span class="sxs-lookup"><span data-stu-id="30853-372">In hello ContosoAdsWeb project, open hello application Web.config file, and insert hello following `connectionStrings` element after hello `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="30853-373">Si vous utilisez Visual Studio 2015 ou version ultérieure, remplacez « v11.0 » par « MSSQLLocalDB ».</span><span class="sxs-lookup"><span data-stu-id="30853-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="30853-374">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="30853-374">Save your changes.</span></span>
3. <span data-ttu-id="30853-375">Dans le projet de ContosoAdsCloudService hello, avec le bouton droit ContosoAdsWeb sous **rôles**, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="30853-375">In hello ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="30853-377">Bonjour **ContosAdsWeb [rôle]** fenêtre Propriétés, cliquez sur hello **paramètres** onglet, puis cliquez sur **ajouter un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="30853-377">In hello **ContosAdsWeb [Role]** properties window, click hello **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="30853-378">Laissez **Configuration du Service** défini trop**toutes les Configurations**.</span><span class="sxs-lookup"><span data-stu-id="30853-378">Leave **Service Configuration** set too**All Configurations**.</span></span>
5. <span data-ttu-id="30853-379">Ajoutez un paramètre nommé *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="30853-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="30853-380">Définissez **Type** trop*ConnectionString*et la valeur **valeur** trop*UseDevelopmentStorage = true*.</span><span class="sxs-lookup"><span data-stu-id="30853-380">Set **Type** too*ConnectionString*, and set **Value** too*UseDevelopmentStorage=true*.</span></span>

    ![New connection string](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="30853-382">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="30853-382">Save your changes.</span></span>
7. <span data-ttu-id="30853-383">Suivez hello même procédure tooadd une chaîne de connexion de stockage dans les propriétés du rôle ContosoAdsWorker hello.</span><span class="sxs-lookup"><span data-stu-id="30853-383">Follow hello same procedure tooadd a storage connection string in hello ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="30853-384">Toujours en hello **ContosoAdsWorker [rôle]** fenêtre Propriétés, ajoutez une autre chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="30853-384">Still in hello **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="30853-385">Nom : ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="30853-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="30853-386">Type : string</span><span class="sxs-lookup"><span data-stu-id="30853-386">Type: String</span></span>
   * <span data-ttu-id="30853-387">Valeur : Coller hello même chaîne de connexion que vous avez utilisé pour le projet de rôle web hello.</span><span class="sxs-lookup"><span data-stu-id="30853-387">Value: Paste hello same connection string you used for hello web role project.</span></span> <span data-ttu-id="30853-388">(hello l’exemple suivant est pour Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="30853-388">(hello following example is for Visual Studio 2013.</span></span> <span data-ttu-id="30853-389">N’oubliez pas toochange hello Source de données si vous copiez cet exemple et à l’aide de Visual Studio 2015 ou version ultérieure.)</span><span class="sxs-lookup"><span data-stu-id="30853-389">Don't forget toochange hello Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="30853-390">Ajout de fichiers de code</span><span class="sxs-lookup"><span data-stu-id="30853-390">Add code files</span></span>
<span data-ttu-id="30853-391">Dans cette section, vous copiez les fichiers de code à partir de la solution de hello téléchargé dans une nouvelle solution hello.</span><span class="sxs-lookup"><span data-stu-id="30853-391">In this section, you copy code files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="30853-392">Hello sections suivantes seront afficher et expliquer les éléments clés de ce code.</span><span class="sxs-lookup"><span data-stu-id="30853-392">hello following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="30853-393">tooa projet ou un dossier, projet de hello avec le bouton droit ou un dossier et cliquez sur les fichiers tooadd **ajouter** - **élément existant**.</span><span class="sxs-lookup"><span data-stu-id="30853-393">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="30853-394">Sélectionnez les fichiers hello puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="30853-394">Select hello files you want and then click **Add**.</span></span> <span data-ttu-id="30853-395">Si vous êtes invité tooreplace des fichiers existants, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="30853-395">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="30853-396">Dans le projet de ContosoAdsCommon hello, supprimez hello *Class1.cs* et ajoutez son Bonjour place *Ad.cs* et *ContosoAdscontext.cs* fichiers à partir de hello téléchargé le projet.</span><span class="sxs-lookup"><span data-stu-id="30853-396">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello *Ad.cs* and *ContosoAdscontext.cs* files from hello downloaded project.</span></span>
2. <span data-ttu-id="30853-397">Dans le projet de ContosoAdsWeb hello, ajoutez hello fichiers suivants à partir de projet de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="30853-397">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="30853-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="30853-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="30853-399">Bonjour *Views\Shared* dossier :  *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="30853-399">In hello *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="30853-400">Bonjour *Views\Home* dossier : *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="30853-400">In hello *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="30853-401">Bonjour *contrôleurs* dossier : *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="30853-401">In hello *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="30853-402">Bonjour *Views\Ad* dossier (créez d’abord le dossier de hello) : cinq *.cshtml* fichiers.</span><span class="sxs-lookup"><span data-stu-id="30853-402">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="30853-403">Dans le projet de ContosoAdsWorker hello, ajoutez *WorkerRole.cs* de hello téléchargé le projet.</span><span class="sxs-lookup"><span data-stu-id="30853-403">In hello ContosoAdsWorker project, add *WorkerRole.cs* from hello downloaded project.</span></span>

<span data-ttu-id="30853-404">Vous pouvez maintenant générer et exécuter l’application hello comme indiqué plus haut dans le didacticiel de hello, et l’application hello utilisera la base de données locale et les ressources d’émulateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="30853-404">You can now build and run hello application as instructed earlier in hello tutorial, and hello app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="30853-405">Hello sections suivantes expliquent les code hello tooworking connexe avec hello environnement Azure, objets BLOB et files d’attente.</span><span class="sxs-lookup"><span data-stu-id="30853-405">hello following sections explain hello code related tooworking with hello Azure environment, blobs, and queues.</span></span> <span data-ttu-id="30853-406">Ce didacticiel n’explique pas comment les contrôleurs MVC toocreate et vues à l’aide de la structure, comment toowrite code Entity Framework qui fonctionne avec les bases de données SQL Server ou les principes de base hello de la programmation asynchrone dans ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="30853-406">This tutorial does not explain how toocreate MVC controllers and views using scaffolding, how toowrite Entity Framework code that works with SQL Server databases, or hello basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="30853-407">Pour plus d’informations sur ces sujets, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="30853-407">For information about these topics, see hello following resources:</span></span>

* [<span data-ttu-id="30853-408">Prise en main de MVC 5</span><span class="sxs-lookup"><span data-stu-id="30853-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="30853-409">Prise en main d’EF 6 et de MVC 5</span><span class="sxs-lookup"><span data-stu-id="30853-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="30853-410">[Programmation de tooasynchronous introduction dans .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="30853-410">[Introduction tooasynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="30853-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="30853-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="30853-412">fichier de Ad.cs Hello définit un enum pour les catégories d’Active Directory et une classe d’entité POCO pour les informations Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30853-412">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="30853-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="30853-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="30853-414">Hello ContosoAdsContext classe spécifie que la classe de publicité de hello est utilisée dans une collection DbSet, Entity Framework seront stockés dans une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="30853-414">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

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

<span data-ttu-id="30853-415">classe Hello possède deux constructeurs.</span><span class="sxs-lookup"><span data-stu-id="30853-415">hello class has two constructors.</span></span> <span data-ttu-id="30853-416">Hello premier d'entre eux est utilisé par le projet web de hello et spécifie le nom de hello d’une chaîne de connexion qui est stockée dans le fichier Web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-416">hello first of them is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file.</span></span> <span data-ttu-id="30853-417">constructeur de deuxième Hello vous permet de toopass dans la chaîne de connexion de hello utilisé par le projet de rôle de travail hello, car celui-ci ne dispose d’un fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="30853-417">hello second constructor enables you toopass in hello actual connection string used by hello worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="30853-418">Vous savez où cette chaîne de connexion a été stockée, et vous verrez plus tard comment les code hello récupère la chaîne de connexion hello lorsqu’il instancie la classe DbContext de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-418">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="30853-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="30853-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="30853-420">Code qui est appelé à partir de hello `Application_Start` méthode crée un *images* conteneur d’objets blob et un *images* file d’attente si elles n’existent pas déjà.</span><span class="sxs-lookup"><span data-stu-id="30853-420">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="30853-421">Cela garantit que chaque fois que vous débutiez à l’aide d’un compte de stockage, ou sur un nouvel ordinateur à l’aide de l’émulateur de stockage hello, file d’attente et le conteneur d’objets blob obligatoires hello seront créés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="30853-421">This ensures that whenever you start using a new storage account, or start using hello storage emulator on a new computer, hello required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="30853-422">Hello compte de stockage toohello code obtient l’accès à l’aide de chaînes de connexion de stockage hello de hello *.cscfg* fichier.</span><span class="sxs-lookup"><span data-stu-id="30853-422">hello code gets access toohello storage account by using hello storage connection string from hello *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="30853-423">Ensuite, il obtient une référence toohello *images* conteneur d’objets blob, crée le conteneur de hello si elle n’existe pas déjà, et définit les autorisations sur le conteneur hello d’accès.</span><span class="sxs-lookup"><span data-stu-id="30853-423">Then it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="30853-424">Par défaut, des conteneurs autorisent uniquement les clients avec un compte de stockage BLOB de tooaccess d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="30853-424">By default, new containers only allow clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="30853-425">site Web de Hello doit hello BLOB toobe public afin qu’il peut afficher des images à l’aide de l’URL que BLOB d’image toohello de point de.</span><span class="sxs-lookup"><span data-stu-id="30853-425">hello website needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

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

<span data-ttu-id="30853-426">Un code similaire Obtient une référence toohello *images* file d’attente et crée une nouvelle file d’attente.</span><span class="sxs-lookup"><span data-stu-id="30853-426">Similar code gets a reference toohello *images* queue and creates a new queue.</span></span> <span data-ttu-id="30853-427">Dans ce cas, aucune modification des autorisations n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="30853-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="30853-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="30853-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="30853-429">Hello *_Layout.cshtml* fichier définit le nom de l’application hello dans l’en-tête de hello et de pied de page et crée une entrée de menu « Annonces ».</span><span class="sxs-lookup"><span data-stu-id="30853-429">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="30853-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="30853-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="30853-431">Hello *Views\Home\Index.cshtml* fichier affiche les liens de catégorie sur la page d’accueil hello.</span><span class="sxs-lookup"><span data-stu-id="30853-431">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="30853-432">les liens Hello passent entier hello hello `Category` enum dans une page d’Index de publicités toohello variable querystring.</span><span class="sxs-lookup"><span data-stu-id="30853-432">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="30853-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="30853-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="30853-434">Bonjour *AdController.cs* fichier, les appels de constructeur Bonjour Bonjour `InitializeStorage` méthode toocreate bibliothèque cliente de stockage Azure objets qui fournissent une API pour l’utilisation des objets BLOB et files d’attente.</span><span class="sxs-lookup"><span data-stu-id="30853-434">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="30853-435">Code de hello Obtient une référence toohello *images* conteneur d’objets blob comme vous l’avez vu précédemment dans *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="30853-435">Then hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="30853-436">Ce faisant, il définit une [stratégie de nouvelles tentatives](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) par défaut appropriée pour une application web.</span><span class="sxs-lookup"><span data-stu-id="30853-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="30853-437">stratégie de nouvelle tentative interruption exponentielle Hello par défaut se bloque hello web app pour plus d’une minute sur les tentatives répétées d’une erreur transitoire.</span><span class="sxs-lookup"><span data-stu-id="30853-437">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="30853-438">stratégie de nouvelle tentative Hello spécifié ici attend trois secondes après chacun pour des tentatives de toothree.</span><span class="sxs-lookup"><span data-stu-id="30853-438">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="30853-439">Un code similaire Obtient une référence toohello *images* file d’attente.</span><span class="sxs-lookup"><span data-stu-id="30853-439">Similar code gets a reference toohello *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="30853-440">La plupart du code du contrôleur hello est typique pour travailler avec un modèle de données Entity Framework à l’aide d’une classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="30853-440">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="30853-441">Une exception est hello HttpPost `Create` (méthode), qui télécharge un fichier et l’enregistre dans le stockage blob.</span><span class="sxs-lookup"><span data-stu-id="30853-441">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="30853-442">classeur de modèles Hello fournit un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello méthode de l’objet.</span><span class="sxs-lookup"><span data-stu-id="30853-442">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="30853-443">Si l’utilisateur hello sélectionné un tooupload de fichier, code de hello télécharge hello fichier enregistre dans un objet blob et met à jour d’enregistrement de base de données Ad hello avec une URL qui pointe toohello blob.</span><span class="sxs-lookup"><span data-stu-id="30853-443">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="30853-444">Hello code hello téléchargement est hello `UploadAndSaveBlobAsync` (méthode).</span><span class="sxs-lookup"><span data-stu-id="30853-444">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="30853-445">Il crée un nom GUID pour les objets blob de hello, téléchargements et enregistre le fichier hello et retourne un objet blob de référence toohello enregistré.</span><span class="sxs-lookup"><span data-stu-id="30853-445">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

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

<span data-ttu-id="30853-446">Après avoir hello HttpPost `Create` méthode télécharge un objet blob et les mises à jour hello de base de données, il crée un tooinform de message de file d’attente de ce processus principal qu’une image est prête pour la miniature tooa de conversion.</span><span class="sxs-lookup"><span data-stu-id="30853-446">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform that back-end process that an image is ready for conversion tooa thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="30853-447">Hello code hello HttpPost `Edit` méthode est similaire à ceci près que si l’utilisateur de hello sélectionne un nouveau fichier image tous les objets BLOB existants doivent être supprimés.</span><span class="sxs-lookup"><span data-stu-id="30853-447">hello code for hello HttpPost `Edit` method is similar except that if hello user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="30853-448">Hello l’exemple suivant montre le code hello qui supprime des objets BLOB lorsque vous supprimez une annonce.</span><span class="sxs-lookup"><span data-stu-id="30853-448">hello next example shows hello code that deletes blobs when you delete an ad.</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="30853-449">ContosoAdsWeb - Views\Ad\Index.cshtml et Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="30853-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="30853-450">Hello *Index.cshtml* fichier affiche les miniatures avec hello autres données Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30853-450">hello *Index.cshtml* file displays thumbnails with hello other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="30853-451">Hello *Details.cshtml* fichier affiche l’image en taille réelle de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-451">hello *Details.cshtml* file displays hello full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="30853-452">ContosoAdsWeb - Views\Ad\Create.cshtml et Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="30853-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="30853-453">Hello *Create.cshtml* et *Edit.cshtml* fichiers spécifient qu’Active hello hello tooget de contrôleur d’encodage de formulaire `HttpPostedFileBase` objet.</span><span class="sxs-lookup"><span data-stu-id="30853-453">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="30853-454">Un `<input>` élément indique hello navigateur tooprovide une boîte de dialogue de sélection de fichier.</span><span class="sxs-lookup"><span data-stu-id="30853-454">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="30853-455">ContosoAdsWorker - WorkerRole.cs - Méthode OnStart</span><span class="sxs-lookup"><span data-stu-id="30853-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="30853-456">environnement de rôle de travail Azure Hello appelle hello `OnStart` méthode Bonjour `WorkerRole` classe une fois le rôle de travail hello est mise en route, et il appelle hello `Run` méthode lorsque hello `OnStart` fin de la méthode.</span><span class="sxs-lookup"><span data-stu-id="30853-456">hello Azure worker role environment calls hello `OnStart` method in hello `WorkerRole` class when hello worker role is getting started, and it calls hello `Run` method when hello `OnStart` method finishes.</span></span>

<span data-ttu-id="30853-457">Hello `OnStart` méthode obtient la chaîne de connexion de base de données hello de hello *.cscfg* de fichiers et le passe toohello Entity Framework DbContext classe.</span><span class="sxs-lookup"><span data-stu-id="30853-457">hello `OnStart` method gets hello database connection string from hello *.cscfg* file and passes it toohello Entity Framework DbContext class.</span></span> <span data-ttu-id="30853-458">fournisseur SQLClient de Hello est utilisé par défaut, afin de fournisseur de hello n’a pas toobe spécifié.</span><span class="sxs-lookup"><span data-stu-id="30853-458">hello SQLClient provider is used by default, so hello provider does not have toobe specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="30853-459">Après cela, méthode hello Obtient un compte de stockage de toohello de référence et crée la file d’attente et le conteneur d’objets blob hello si elles n’existent pas.</span><span class="sxs-lookup"><span data-stu-id="30853-459">After that, hello method gets a reference toohello storage account and creates hello blob container and queue if they don't exist.</span></span> <span data-ttu-id="30853-460">code Hello qui est similaire toowhat vous nous avons déjà vu dans un rôle web de hello `Application_Start` (méthode).</span><span class="sxs-lookup"><span data-stu-id="30853-460">hello code for that is similar toowhat you already saw in hello web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="30853-461">ContosoAdsWorker - WorkerRole.cs - Méthode Run</span><span class="sxs-lookup"><span data-stu-id="30853-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="30853-462">Hello `Run` méthode est appelée lorsque hello `OnStart` méthode termine son travail de l’initialisation.</span><span class="sxs-lookup"><span data-stu-id="30853-462">hello `Run` method is called when hello `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="30853-463">méthode Hello exécute une boucle infinie qui surveille les nouveaux messages de file d’attente et les traite lorsqu’ils arrivent.</span><span class="sxs-lookup"><span data-stu-id="30853-463">hello method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

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

<span data-ttu-id="30853-464">Après chaque itération de boucle de hello, si aucun message de la file d’attente a été trouvé, programme de hello se met en veille pendant une seconde.</span><span class="sxs-lookup"><span data-stu-id="30853-464">After each iteration of hello loop, if no queue message was found, hello program sleeps for a second.</span></span> <span data-ttu-id="30853-465">Rôle de travail hello cela empêche de subir excessive du processeur durée et le stockage transaction des frais.</span><span class="sxs-lookup"><span data-stu-id="30853-465">This prevents hello worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="30853-466">Hello équipe de consultants clients Microsoft indique un récit à propos d’un développeur qui a oublié tooinclude, déployées tooproduction et pour les vacances.</span><span class="sxs-lookup"><span data-stu-id="30853-466">hello Microsoft Customer Advisory Team tells a story about a  developer who forgot tooinclude this, deployed tooproduction, and left for vacation.</span></span> <span data-ttu-id="30853-467">Lorsqu’il a obtenu sa supervision coûtent plus cher que les vacances hello.</span><span class="sxs-lookup"><span data-stu-id="30853-467">When he got back, his oversight cost more than hello vacation.</span></span>

<span data-ttu-id="30853-468">Parfois, le contenu d’un message de la file d’attente hello provoque une erreur lors du traitement.</span><span class="sxs-lookup"><span data-stu-id="30853-468">Sometimes hello content of a queue message causes an error in processing.</span></span> <span data-ttu-id="30853-469">Cela s’appelle un *message incohérent*, et si vous venez a consigné une erreur et redémarrer la boucle de hello, vous pouvez essayer indéfiniment qu’un message aux tooprocess.</span><span class="sxs-lookup"><span data-stu-id="30853-469">This is called a *poison message*, and if you just logged an error and restarted hello loop, you could endlessly try tooprocess that message.</span></span>  <span data-ttu-id="30853-470">Par conséquent bloc catch de hello inclut une instruction if qui vérifie toosee combien de fois application hello a essayé de tooprocess hello message actuel, et si elle a été plus de 5 fois, le message de type hello est supprimé à partir de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="30853-470">Therefore hello catch block includes an if statement that checks toosee how many times hello app has tried tooprocess hello current message, and if it has been more than 5 times, hello message is deleted from hello queue.</span></span>

<span data-ttu-id="30853-471">`ProcessQueueMessage` est appelé lorsqu'un message de file d'attente est trouvé.</span><span class="sxs-lookup"><span data-stu-id="30853-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

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

<span data-ttu-id="30853-472">Ce code lit l’URL de l’image de hello de base de données tooget hello convertit tooa vignette de l’image hello, enregistre la miniature de hello dans un objet blob, met à jour la base de données hello avec l’URL de blob miniature hello et supprime le message de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="30853-472">This code reads hello database tooget hello image URL, converts hello image tooa thumbnail, saves hello thumbnail in a blob, updates hello database with hello thumbnail blob URL, and deletes hello queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="30853-473">Hello code Bonjour `ConvertImageToThumbnailJPG` méthode utilise les classes dans l’espace de noms System.Drawing hello par souci de simplicité.</span><span class="sxs-lookup"><span data-stu-id="30853-473">hello code in hello `ConvertImageToThumbnailJPG` method uses classes in hello System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="30853-474">Toutefois, les classes de hello dans cet espace de noms ont été conçues pour une utilisation avec Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="30853-474">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="30853-475">Elles ne sont pas prises en charge dans un service Windows ou ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="30853-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="30853-476">Pour plus d’informations sur les options de traitement d’images, consultez [Génération d’images dynamiques](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) et [Redimensionnement d’images approfondi](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="30853-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="30853-477">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="30853-477">Troubleshooting</span></span>
<span data-ttu-id="30853-478">En cas de quelque chose ne fonctionne pas pendant que vous êtes suivant les instructions de hello dans ce didacticiel, voici quelques erreurs courantes et comment tooresolve les.</span><span class="sxs-lookup"><span data-stu-id="30853-478">In case something doesn't work while you're following hello instructions in this tutorial, here are some common errors and how tooresolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="30853-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="30853-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="30853-480">Hello `RoleEnvironment` objet est fourni par Azure lorsque vous exécutez une application dans Azure, ou lorsque vous exécutez localement à l’aide d’émulateur de calcul Azure hello.</span><span class="sxs-lookup"><span data-stu-id="30853-480">hello `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using hello Azure compute emulator.</span></span>  <span data-ttu-id="30853-481">Si vous obtenez cette erreur lorsque vous exécutez localement, assurez-vous que vous avez défini le projet de ContosoAdsCloudService hello en tant que projet de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="30853-481">If you get this error when you're running locally, make sure that you have set hello ContosoAdsCloudService project as hello startup project.</span></span> <span data-ttu-id="30853-482">Cela configure hello toorun de projet à l’aide d’émulateur de calcul Azure hello.</span><span class="sxs-lookup"><span data-stu-id="30853-482">This sets up hello project toorun using hello Azure compute emulator.</span></span>

<span data-ttu-id="30853-483">Une des choses hello hello application utilise hello RoleEnvironment Azure pour est tooget des valeurs de chaîne de connexion de hello qui sont stockés dans hello *.cscfg* des fichiers, par conséquent, une autre cause de cette exception est une chaîne de connexion manquant.</span><span class="sxs-lookup"><span data-stu-id="30853-483">One of hello things hello application uses hello Azure RoleEnvironment for is tooget hello connection string values that are stored in hello *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="30853-484">Assurez-vous que vous avez créé paramètre hello StorageConnectionString Cloud à la fois et les configurations locales dans le projet de ContosoAdsWeb hello et que vous avez créé les deux chaînes de connexion pour les deux configurations de projet de ContosoAdsWorker hello.</span><span class="sxs-lookup"><span data-stu-id="30853-484">Make sure that you created hello StorageConnectionString setting for both Cloud and Local configurations in hello ContosoAdsWeb project, and that you created both connection strings for both configurations in hello ContosoAdsWorker project.</span></span> <span data-ttu-id="30853-485">Si vous effectuez un **Rechercher tout** recherche pour StorageConnectionString dans l’ensemble de la solution hello, vous devez voir il 9 heures dans les 6 fichiers.</span><span class="sxs-lookup"><span data-stu-id="30853-485">If you do a **Find All** search for StorageConnectionString in hello entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="30853-486">Impossible de remplacer tooport xxx.</span><span class="sxs-lookup"><span data-stu-id="30853-486">Cannot override tooport xxx.</span></span> <span data-ttu-id="30853-487">La valeur du nouveau port est inférieure à la valeur minimale autorisée de 8080 pour le protocole http</span><span class="sxs-lookup"><span data-stu-id="30853-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="30853-488">Essayez de modifier le numéro de port de hello utilisé par le projet web de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-488">Try changing hello port number used by hello web project.</span></span> <span data-ttu-id="30853-489">Projet de ContosoAdsWeb hello d’avec le bouton droit, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="30853-489">Right-click hello ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="30853-490">Cliquez sur hello **Web** onglet et modifiez le numéro de port hello Bonjour **Url du projet** paramètre.</span><span class="sxs-lookup"><span data-stu-id="30853-490">Click hello **Web** tab, and then change hello port number in hello **Project Url** setting.</span></span>

<span data-ttu-id="30853-491">Pour une autre solution susceptibles de résoudre le problème de hello, consultez hello suivant la section.</span><span class="sxs-lookup"><span data-stu-id="30853-491">For another alternative that might resolve hello problem, see hello following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="30853-492">Autres erreurs lors de l'exécution locale</span><span class="sxs-lookup"><span data-stu-id="30853-492">Other errors when running locally</span></span>
<span data-ttu-id="30853-493">Par nouveau cloud de la valeur par défaut des projets de service utilisent Bonjour Azure compute emulator toosimulate express Bonjour environnement Azure.</span><span class="sxs-lookup"><span data-stu-id="30853-493">By default new cloud service projects use hello Azure compute emulator express toosimulate hello Azure environment.</span></span> <span data-ttu-id="30853-494">Il s’agit d’une version légère de l’émulateur de calcul complet de hello et fonctionne sous certaines hello conditions émulateur complet lors de la version express de hello n’est pas.</span><span class="sxs-lookup"><span data-stu-id="30853-494">This is a lightweight version of hello full compute emulator, and under some conditions hello full emulator will work when hello express version does not.</span></span>  

<span data-ttu-id="30853-495">toochange hello émulateur complet de projet toouse hello, cliquez sur le projet de ContosoAdsCloudService hello, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="30853-495">toochange hello project toouse hello full emulator, right-click hello ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="30853-496">Bonjour **propriétés** fenêtre, cliquez sur hello **Web** onglet, puis cliquez sur hello **utiliser l’émulateur complet** case d’option.</span><span class="sxs-lookup"><span data-stu-id="30853-496">In hello **Properties** window click hello **Web** tab, and then click hello **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="30853-497">Dans l’application de type hello toorun de commandes avec l’émulateur complet hello, vous avez tooopen Visual Studio avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="30853-497">In order toorun hello application with hello full emulator, you have tooopen Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30853-498">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30853-498">Next steps</span></span>
<span data-ttu-id="30853-499">Hello application d’annonces de Contoso a intentionnellement été conservée simple pour obtenir un didacticiel de mise en route.</span><span class="sxs-lookup"><span data-stu-id="30853-499">hello Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="30853-500">Par exemple, il n’implémente pas [injection de dépendance](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) ou hello [référentiel et une unité de travaillent des modèles](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), ce n’est pas [utiliser une interface pour la journalisation](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), il n’utilise pas [ Migrations EF Code First](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage données modifications sur le modèle ou [résilience des connexions EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage temporaire des erreurs réseau et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="30853-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors, and so forth.</span></span>

<span data-ttu-id="30853-501">Voici certaines applications service cloud qui illustrent les plus pratiques de codage réel, répertoriées de moins complexe toomore complexe :</span><span class="sxs-lookup"><span data-stu-id="30853-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex toomore complex:</span></span>

* <span data-ttu-id="30853-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="30853-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="30853-503">Un concept similaire tooContoso annonces mais implémente que davantage de fonctionnalités et les plus pratiques de codage réel.</span><span class="sxs-lookup"><span data-stu-id="30853-503">Similar in concept tooContoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="30853-504">[Application multiniveau Azure Cloud Service avec tables, files d'attente et objets blob](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="30853-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="30853-505">Présente les tables Azure Storage ainsi que des objets blob et des files d’attente.</span><span class="sxs-lookup"><span data-stu-id="30853-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="30853-506">Basé sur une version antérieure de hello Azure SDK pour .NET, requiert certains toowork modifications avec la version actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-506">Based on an older version of hello Azure SDK for .NET, will require some modifications toowork with hello current version.</span></span>
* <span data-ttu-id="30853-507">[Concepts de base des services cloud dans Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="30853-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="30853-508">Un exemple complet illustrant une large gamme de meilleures pratiques, produit par le groupe Microsoft Patterns and Practices de hello.</span><span class="sxs-lookup"><span data-stu-id="30853-508">A comprehensive sample demonstrating a wide range of best practices, produced by hello Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="30853-509">Pour obtenir des informations générales sur le développement pour le cloud de hello, consultez [génération d’applications Cloud réel avec Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="30853-509">For general information about developing for hello cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="30853-510">Pour un stockage de tooAzure vidéo de présentation des meilleures pratiques et les modèles, consultez [Microsoft Azure Storage – nouveautés, meilleures pratiques et modèles](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="30853-510">For a video introduction tooAzure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="30853-511">Pour plus d’informations, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="30853-511">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="30853-512">Azure Cloud Services Partie 1 : Présentation</span><span class="sxs-lookup"><span data-stu-id="30853-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="30853-513">Comment les Services de cloud computing toomanage</span><span class="sxs-lookup"><span data-stu-id="30853-513">How toomanage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="30853-514">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="30853-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="30853-515">Comment toochoose un cloud de fournisseur de services</span><span class="sxs-lookup"><span data-stu-id="30853-515">How toochoose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
