---
title: "aaaCreate une tâche Web de .NET dans Azure App Service | Documents Microsoft"
description: "Créez une application multiniveau avec ASP.NET MVC et Azure. Hello frontal s’exécute dans une application web dans Azure App Service et hello précédent s’exécute en tant qu’une tâche Web. application Hello utilise Entity Framework, base de données SQL, les files d’attente de stockage Azure et des objets BLOB."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="8e49c-105">Créer une tâche web .NET dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8e49c-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="8e49c-106">Ce didacticiel montre comment le code pour une application ASP.NET MVC 5 à plusieurs niveaux simple qui utilise hello toowrite [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="8e49c-106">This tutorial shows how toowrite code for a simple multi-tier ASP.NET MVC 5 application that uses hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="8e49c-107">Hello d’objectif de hello [WebJobs SDK](websites-webjobs-resources.md) est toosimplify hello code que vous écrivez pour les tâches courantes qu’une tâche Web peut effectuer, telles que le traitement d’image, traitement de la file d’attente, agrégation RSS, maintenance des fichiers et de l’envoi des messages électroniques.</span><span class="sxs-lookup"><span data-stu-id="8e49c-107">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="8e49c-108">Hello WebJobs SDK inclut des fonctionnalités intégrées pour de nombreux autres scénarios courants pour travailler avec le stockage Azure et Service Bus et pour la planification des tâches et la gestion des erreurs.</span><span class="sxs-lookup"><span data-stu-id="8e49c-108">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="8e49c-109">En outre, il a conçu toobe extensible et il existe un [référentiel open source pour les extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="8e49c-109">In addition, it's designed toobe extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="8e49c-110">exemple d’application Hello est un forum de publicité.</span><span class="sxs-lookup"><span data-stu-id="8e49c-110">hello sample application is an advertising bulletin board.</span></span> <span data-ttu-id="8e49c-111">Les utilisateurs peuvent télécharger des images pour les annonces, et un processus principal convertit hello images toothumbnails.</span><span class="sxs-lookup"><span data-stu-id="8e49c-111">Users can upload images for ads, and a backend process converts hello images toothumbnails.</span></span> <span data-ttu-id="8e49c-112">page de liste ad Hello affiche des miniatures de hello et hello ad page des détails affiche les image plein écran hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-112">hello ad list page shows hello thumbnails, and hello ad details page shows hello full-size image.</span></span> <span data-ttu-id="8e49c-113">Voici une capture d'écran :</span><span class="sxs-lookup"><span data-stu-id="8e49c-113">Here's a screenshot:</span></span>

![Ad list](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="8e49c-115">Cet exemple d’application fonctionne avec des [files d’attente Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) et [objets blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="8e49c-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="8e49c-116">Hello didacticiel montre comment toodeploy hello application trop[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) et [base de données SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="8e49c-116">hello tutorial shows how toodeploy hello application too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="8e49c-117"><a id="prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="8e49c-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="8e49c-118">Hello didacticiel suppose que vous savez comment toowork avec [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projets dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e49c-118">hello tutorial assumes that you know how toowork with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="8e49c-119">didacticiel de Hello a été écrit à l’origine pour Visual Studio 2013, mais il peut être utilisé avec les versions ultérieures de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e49c-119">hello tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="8e49c-120">Si vous utilisez Visual Studio 2015 ou 2017, notez qu’avant d’exécuter application hello localement, vous devez modifier hello `Data Source` dans le cadre de la chaîne de connexion de base de données SQL Server locale hello dans les fichiers Web.config et App.config de hello de `Data Source=(localdb)\v11.0` trop`Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="8e49c-120">If you are using Visual Studio 2015 or 2017, make note that before you run hello application locally, you must change hello `Data Source` part of hello SQL Server LocalDB connection string in hello Web.config and App.config files from `Data Source=(localdb)\v11.0` too`Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="8e49c-121"><a name="note"></a>Ce didacticiel, vous devez avoir un toocomplete compte Azure :</span><span class="sxs-lookup"><span data-stu-id="8e49c-121"><a name="note"></a>You must have an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="8e49c-122">Vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): vous obtenez des crédits que vous pouvez utiliser tootry à payer des services Azure, et même une fois qu’ils sont utilisés, vous pouvez conserver le compte de hello et utiliser des services Azure gratuits, comme les sites Web.</span><span class="sxs-lookup"><span data-stu-id="8e49c-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use tootry out paid Azure services, and even after they're used up, you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="8e49c-123">Votre carte de crédit ne sera jamais facturé, sauf si vous explicitement modifiez vos paramètres et demandez toobe facturé.</span><span class="sxs-lookup"><span data-stu-id="8e49c-123">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
> * <span data-ttu-id="8e49c-124">Vous pouvez [activer le crédit Azure mensuel pour Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) : votre abonnement vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.</span><span class="sxs-lookup"><span data-stu-id="8e49c-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="8e49c-125">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="8e49c-125">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8e49c-126">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="8e49c-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="8e49c-127"><a id="learn"></a>Contenu</span><span class="sxs-lookup"><span data-stu-id="8e49c-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="8e49c-128">didacticiel de Hello illustre des tâches de hello toodo suivant :</span><span class="sxs-lookup"><span data-stu-id="8e49c-128">hello tutorial shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="8e49c-129">Activer votre ordinateur pour le développement Azure en installant hello Azure SDK (uniquement pour Visual Studio 2013 et 2015 utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="8e49c-129">Enable your machine for Azure development by installing hello Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="8e49c-130">Créez un projet d’Application Console qui déploie automatiquement comme une tâche Web Azure lorsque vous déployez le projet web associé de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy hello associated web project.</span></span>
* <span data-ttu-id="8e49c-131">Tester un service principal de WebJobs SDK localement sur l’ordinateur de développement hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-131">Test a WebJobs SDK backend locally on hello development computer.</span></span>
* <span data-ttu-id="8e49c-132">Publier une application avec une application web de tâches Web principal tooa dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="8e49c-132">Publish an application with a WebJobs backend tooa web app in App Service.</span></span>
* <span data-ttu-id="8e49c-133">Télécharger des fichiers et stockez-les dans hello service Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-133">Upload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="8e49c-134">Utilisez toowork du Kit de développement logiciel Azure WebJobs hello avec les objets BLOB et files d’attente de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-134">Use hello Azure WebJobs SDK toowork with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="8e49c-135"><a id="contosoads"></a>Architecture de l’application</span><span class="sxs-lookup"><span data-stu-id="8e49c-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="8e49c-136">exemple d’application Hello utilise hello [centré sur la file d’attente de travail modèle](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) travail hello gourmande en ressources processeur de toooff en charge de la création du processus de miniatures tooa principal.</span><span class="sxs-lookup"><span data-stu-id="8e49c-136">hello sample application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa backend process.</span></span>

<span data-ttu-id="8e49c-137">application Hello stocke des publicités dans une base de données SQL, à l’aide des tables de hello toocreate Entity Framework Code First et accéder aux données de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-137">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="8e49c-138">Pour chaque publicité, base de données hello stocke deux URL : un pour les image plein écran hello et un pour l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-138">For each ad, hello database stores two URLs: one for hello full-size image and one for hello thumbnail.</span></span>

![Ad table](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="8e49c-140">Lorsqu’un utilisateur télécharge une image, une application web de hello stocke image hello dans un [objets blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), et stocke des informations d’Active Directory hello dans base de données hello avec une URL qui pointe toohello blob.</span><span class="sxs-lookup"><span data-stu-id="8e49c-140">When a user uploads an image, hello web app stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="8e49c-141">AT hello même temps, il écrit un message de tooan file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-141">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="8e49c-142">Dans un processus principal en cours d’exécution en tant qu’une tâche Web Azure, hello WebJobs SDK interroge la file d’attente hello pour les nouveaux messages.</span><span class="sxs-lookup"><span data-stu-id="8e49c-142">In a backend process running as an Azure WebJob, hello WebJobs SDK polls hello queue for new messages.</span></span> <span data-ttu-id="8e49c-143">Quand un nouveau message s’affiche, hello la tâche Web crée une miniature pour cette image et les mises à jour hello miniature champ de base de données d’URL pour qu’ad.</span><span class="sxs-lookup"><span data-stu-id="8e49c-143">When a new message appears, hello WebJob creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="8e49c-144">Voici un diagramme qui illustre l’interagissent entre les parties hello de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="8e49c-144">Here's a diagram that shows how hello parts of hello application interact:</span></span>

![Contoso Ads architecture](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="8e49c-146">instructions des didacticiels de Hello appliquent tooAzure SDK pour .NET 2.7.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-146">hello tutorial instructions apply tooAzure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="8e49c-147"><a id="storage"></a>Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8e49c-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="8e49c-148">Un compte de stockage Azure fournit des ressources pour le stockage de la file d’attente et les données blob dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-148">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span> <span data-ttu-id="8e49c-149">Il est également utilisé par hello WebJobs SDK toostore enregistrement des données de tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-149">It's also used by hello WebJobs SDK toostore logging data for hello dashboard.</span></span>

<span data-ttu-id="8e49c-150">Dans une application réelle, vous créez généralement des comptes distincts pour les données d’application et de journalisation, et des comptes distincts pour les données de test et de production.</span><span class="sxs-lookup"><span data-stu-id="8e49c-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="8e49c-151">Pour ce didacticiel, vous allez utiliser un seul compte.</span><span class="sxs-lookup"><span data-stu-id="8e49c-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="8e49c-152">Ouvrez hello **l’Explorateur de serveurs** fenêtre dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e49c-152">Open hello **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="8e49c-153">Avec le bouton hello **Azure** nœud, puis cliquez sur **connecter tooMicrosoft abonnement Azure...** .</span><span class="sxs-lookup"><span data-stu-id="8e49c-153">Right-click hello **Azure** node, and then click **Connect tooMicrosoft Azure Subscription...**.</span></span>
   
   ![Se connecter tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="8e49c-155">Connectez-vous à l'aide de vos informations d'identification Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="8e49c-156">Avec le bouton droit **stockage** sous hello nœud Azure, puis cliquez sur **créer un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-156">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Créer un compte de stockage](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="8e49c-158">Bonjour **créer un compte de stockage** boîte de dialogue, entrez un nom pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-158">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="8e49c-159">nom de Hello doit être unique (aucun autre compte de stockage Azure ne peut avoir hello même nom).</span><span class="sxs-lookup"><span data-stu-id="8e49c-159">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="8e49c-160">Si le nom hello que vous entrez est déjà en cours d’utilisation, vous obtiendrez une chance toochange il.</span><span class="sxs-lookup"><span data-stu-id="8e49c-160">If hello name you enter is already in use, you'll get a chance toochange it.</span></span>

    <span data-ttu-id="8e49c-161">Hello tooaccess URL votre compte de stockage sera *{nom}*. core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="8e49c-161">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="8e49c-162">Ensemble hello **région ou groupe d’affinités** tooyou le plus proche de liste déroulante toohello région.</span><span class="sxs-lookup"><span data-stu-id="8e49c-162">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="8e49c-163">Ce paramètre spécifie le centre de données Azure qui hébergera votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e49c-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="8e49c-164">Pour ce didacticiel, votre choix ne fera pas une grande différence.</span><span class="sxs-lookup"><span data-stu-id="8e49c-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="8e49c-165">Toutefois, pour une application web de production, vous souhaitez que votre serveur web et votre toobe de compte de stockage Bonjour même latence toominimize de région et les données des frais de sortie.</span><span class="sxs-lookup"><span data-stu-id="8e49c-165">However, for a production web app, you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="8e49c-166">Hello web application (vous allez créer ultérieurement) centre de données doit être aussi proche que possible des navigateurs toohello l’accès à hello web application latence toominimize de commande.</span><span class="sxs-lookup"><span data-stu-id="8e49c-166">hello web app (which you'll create later) datacenter should be as close as possible toohello browsers accessing hello web app in order toominimize latency.</span></span>
7. <span data-ttu-id="8e49c-167">Ensemble hello **réplication** déroulante liste trop**localement redondant**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-167">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>

    <span data-ttu-id="8e49c-168">Lors de la géo-réplication est activée pour un compte de stockage, contenu de hello stocké est répliqué tooa centre de données secondaire tooenable basculement toothat emplacement en cas de sinistre majeur dans l’emplacement principal de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-168">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="8e49c-169">La géo-réplication peut engendrer des coûts supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8e49c-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="8e49c-170">Pour les comptes de test et de développement, généralement non désirés toopay pour la géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="8e49c-170">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="8e49c-171">Pour plus d’informations, consultez [Création, gestion ou suppression d’un compte de stockage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8e49c-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="8e49c-172">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-172">Click **Create**.</span></span>

    ![New storage account](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="8e49c-174"><a id="download"></a>Télécharger l’application hello</span><span class="sxs-lookup"><span data-stu-id="8e49c-174"><a id="download"></a>Download hello application</span></span>
1. <span data-ttu-id="8e49c-175">Téléchargez et décompressez hello [complété solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="8e49c-175">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="8e49c-176">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e49c-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="8e49c-177">À partir de hello **fichier** menu Choisissez **Ouvrir > Projet/Solution**, accédez toowhere que vous avez téléchargé les solutions hello et puis ouvrez le fichier de solution hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-177">From hello **File** menu choose **Open > Project/Solution**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="8e49c-178">Appuyez sur solution de hello toobuild CTRL + MAJ + B.</span><span class="sxs-lookup"><span data-stu-id="8e49c-178">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="8e49c-179">Par défaut, Visual Studio restaure automatiquement le contenu du package NuGet hello, qui n’est pas compris dans hello *.zip* fichier.</span><span class="sxs-lookup"><span data-stu-id="8e49c-179">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="8e49c-180">Si les packages hello ne sont pas restaurées, installez-les manuellement en accédant de toohello **gérer les Packages NuGet pour la Solution** boîte de dialogue et en cliquant sur hello **restaurer** bouton à droite en haut hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-180">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="8e49c-181">Dans **l’Explorateur de solutions**, assurez-vous que **ContosoAdsWeb** est sélectionné comme projet de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as hello startup project.</span></span>

## <span data-ttu-id="8e49c-182"><a id="configurestorage"></a>Configurer hello application toouse votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="8e49c-182"><a id="configurestorage"></a>Configure hello application toouse your storage account</span></span>
1. <span data-ttu-id="8e49c-183">Ouvrez l’application hello *Web.config* fichier hello ContosoAdsWeb projet.</span><span class="sxs-lookup"><span data-stu-id="8e49c-183">Open hello application *Web.config* file in hello ContosoAdsWeb project.</span></span>

    <span data-ttu-id="8e49c-184">Hello contient une chaîne de connexion SQL et une chaîne de connexion de stockage Azure pour l’utilisation des objets BLOB et files d’attente.</span><span class="sxs-lookup"><span data-stu-id="8e49c-184">hello file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="8e49c-185">Hello chaîne de connexion SQL pointe tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) base de données.</span><span class="sxs-lookup"><span data-stu-id="8e49c-185">hello SQL connection string points tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="8e49c-186">chaîne de connexion de stockage Hello est un exemple qui a des espaces réservés pour hello clé compte de stockage accès et le nom.</span><span class="sxs-lookup"><span data-stu-id="8e49c-186">hello storage connection string is an example that has placeholders for hello storage account name and access key.</span></span> <span data-ttu-id="8e49c-187">Vous devez le remplacer par une chaîne de connexion qui a le nom de hello et la clé de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e49c-187">You'll replace this with a connection string that has hello name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="8e49c-188">chaîne de connexion de stockage Hello AzureWebJobsStorage car il s’agit de hello de nom hello que webjobs SDK utilise par défaut est appelé.</span><span class="sxs-lookup"><span data-stu-id="8e49c-188">hello storage connection string is named AzureWebJobsStorage because that's hello name hello WebJobs SDK uses by default.</span></span> <span data-ttu-id="8e49c-189">Hello même nom est utilisé ici pour avoir une valeur de chaîne de connexion qu’un seul tooset Bonjour environnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-189">hello same name is used here so you have tooset only one connection string value in hello Azure environment.</span></span>
2. <span data-ttu-id="8e49c-190">Dans **l’Explorateur de serveurs**, avec le bouton droit de votre compte de stockage sous hello **stockage** nœud, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-190">In **Server Explorer**, right-click your storage account under hello **Storage** node, and then click **Properties**.</span></span>

    ![Click Storage Account Properties](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="8e49c-192">Bonjour **propriétés** fenêtre, cliquez sur **clés de compte de stockage**, puis cliquez sur les points de suspension hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-192">In hello **Properties** window, click **Storage Account Keys**, and then click hello ellipsis.</span></span>

    ![Clés de compte de stockage](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="8e49c-194">Hello de copie **chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-194">Copy hello **Connection String**.</span></span>

    ![Storage Account Keys dialog](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="8e49c-196">Remplacez la chaîne de connexion de stockage hello Bonjour *Web.config* fichier avec la chaîne de connexion hello vous venez de copier.</span><span class="sxs-lookup"><span data-stu-id="8e49c-196">Replace hello storage connection string in hello *Web.config* file with hello connection string you just copied.</span></span> <span data-ttu-id="8e49c-197">Veillez à que sélectionner tous les éléments à l’intérieur des guillemets hello mais sans inclure les guillemets hello avant le collage.</span><span class="sxs-lookup"><span data-stu-id="8e49c-197">Make sure you select everything inside hello quotation marks but not including hello quotation marks before pasting.</span></span>
6. <span data-ttu-id="8e49c-198">Ouvrez hello *App.config* fichier hello ContosoAdsWebJob projet.</span><span class="sxs-lookup"><span data-stu-id="8e49c-198">Open hello *App.config* file in hello ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="8e49c-199">Ce fichier comporte deux chaînes de connexion : une pour les données de l'application et une pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="8e49c-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="8e49c-200">Vous pouvez utiliser des comptes de stockage distincts pour les données et la journalisation de l’application, ainsi qu’utiliser [plusieurs comptes de stockage pour les données](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="8e49c-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="8e49c-201">Pour ce didacticiel, vous allez utiliser un seul compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e49c-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="8e49c-202">chaînes de connexion Hello possèdent des espaces réservés pour les clés de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-202">hello connection strings have placeholders for hello storage account keys.</span></span>

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    <span data-ttu-id="8e49c-203">Par défaut, hello WebJobs SDK recherche les chaînes de connexion nommées AzureWebJobsStorage et AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="8e49c-203">By default, hello WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="8e49c-204">En guise d’alternative, vous pouvez [stocker la chaîne de connexion hello toutefois vous souhaitez et le passez dans explicitement toohello `JobHost` objet](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="8e49c-204">As an alternative, you can [store hello connection string however you want and pass it in explicitly toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="8e49c-205">Remplacez les deux chaînes de connexion de stockage avec la chaîne de connexion hello que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="8e49c-205">Replace both storage connection strings with hello connection string you copied earlier.</span></span>
8. <span data-ttu-id="8e49c-206">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="8e49c-206">Save your changes.</span></span>

## <span data-ttu-id="8e49c-207"><a id="run"></a>Exécutez hello application localement</span><span class="sxs-lookup"><span data-stu-id="8e49c-207"><a id="run"></a>Run hello application locally</span></span>
1. <span data-ttu-id="8e49c-208">toostart hello web frontal de l’application hello, appuyez sur CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="8e49c-208">toostart hello web frontend of hello application, press CTRL+F5.</span></span>

    <span data-ttu-id="8e49c-209">navigateur par défaut de Hello ouvre la page d’accueil toohello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-209">hello default browser opens toohello home page.</span></span> <span data-ttu-id="8e49c-210">(projet de hello web s’exécute, car vous l’avez apportées projet de démarrage hello.)</span><span class="sxs-lookup"><span data-stu-id="8e49c-210">(hello web project runs because you've made it hello startup project.)</span></span>

    ![Contoso Ads home page](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="8e49c-212">toostart hello la tâche Web principal de l’application hello, avec le bouton droit de projet hello ContosoAdsWebJob **l’Explorateur de solutions**, puis cliquez sur **déboguer** > **démarrer une nouvelle instance** .</span><span class="sxs-lookup"><span data-stu-id="8e49c-212">toostart hello WebJob backend of hello application, right-click hello ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="8e49c-213">Une fenêtre d’application console s’ouvre et affiche des messages de journalisation indiquant l’objet de tâche Web SDK JobHost hello a démarré toorun.</span><span class="sxs-lookup"><span data-stu-id="8e49c-213">A console application window opens and displays logging messages indicating hello WebJobs SDK JobHost object has started toorun.</span></span>

    ![Fenêtre de l’application console montrant ce principal hello est en cours d’exécution.](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="8e49c-215">Dans votre navigateur, cliquez sur **Créer une publicité**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="8e49c-216">Entrez des données de test, sélectionnez une tooupload d’image, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-216">Enter some test data, select an image tooupload, and then click **Create**.</span></span>

    ![Create page](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="8e49c-218">application Hello passe toohello page d’Index, mais elle n’affiche une miniature de publicité hello parce que ce traitement n’a pas encore s’est produite.</span><span class="sxs-lookup"><span data-stu-id="8e49c-218">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="8e49c-219">Pendant ce temps, après un court délai d’attente un message de journalisation dans la fenêtre de l’application console hello indique qu’un message de la file d’attente a été reçu et qu’il a été traité.</span><span class="sxs-lookup"><span data-stu-id="8e49c-219">Meanwhile, after a short wait a logging message in hello console application window shows that a queue message was received and has been processed.</span></span>

    ![Console application window showing that a queue message has been processed](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="8e49c-221">Une fois que vous voyez hello consignant les messages dans la fenêtre de l’application console hello, actualiser hello Index toosee hello vignette.</span><span class="sxs-lookup"><span data-stu-id="8e49c-221">After you see hello logging messages in hello console application window, refresh hello Index page toosee hello thumbnail.</span></span>

    ![Page d'index](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="8e49c-223">Cliquez sur **détails** pour votre image en taille réelle d’ad toosee hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-223">Click **Details** for your ad toosee hello full-size image.</span></span>

    ![Details page](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="8e49c-225">Vous avez déjà exécuté application hello sur votre ordinateur local, et qu’il utilise un serveur SQL de base de données située sur votre ordinateur, mais il fonctionne avec les files d’attente et des objets BLOB dans hello cloud.</span><span class="sxs-lookup"><span data-stu-id="8e49c-225">You've been running hello application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in hello cloud.</span></span> <span data-ttu-id="8e49c-226">Bonjour, suivant la section vous allez exécuter application hello dans le cloud de hello, à l’aide d’une base de données de cloud ainsi que les objets BLOB du cloud et les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="8e49c-226">In hello following section you'll run hello application in hello cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="8e49c-227"><a id="runincloud"></a>Exécutez l’application hello dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="8e49c-227"><a id="runincloud"></a>Run hello application in hello cloud</span></span>
<span data-ttu-id="8e49c-228">Vous effectuerez hello après application de hello toorun étapes dans le cloud de hello :</span><span class="sxs-lookup"><span data-stu-id="8e49c-228">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="8e49c-229">Déployer des applications tooWeb.</span><span class="sxs-lookup"><span data-stu-id="8e49c-229">Deploy tooWeb Apps.</span></span> <span data-ttu-id="8e49c-230">Visual Studio crée automatiquement une application web dans App Service et une instance Base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="8e49c-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="8e49c-231">Configurer hello web application toouse votre compte de stockage et de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-231">Configure hello web app toouse your Azure SQL database and storage account.</span></span>

<span data-ttu-id="8e49c-232">Une fois que vous avez créé des publicités lors de l’exécution dans le cloud de hello, vous allez afficher hello hello de toosee du tableau de bord WebJobs SDK enrichi de fonctionnalités qu’il a toooffer d’analyse.</span><span class="sxs-lookup"><span data-stu-id="8e49c-232">After you've created some ads while running in hello cloud, you'll view hello WebJobs SDK dashboard toosee hello rich monitoring features it has toooffer.</span></span>

### <a name="deploy-tooweb-apps"></a><span data-ttu-id="8e49c-233">Déployer des applications de tooWeb</span><span class="sxs-lookup"><span data-stu-id="8e49c-233">Deploy tooWeb Apps</span></span>

1. <span data-ttu-id="8e49c-234">Fermez le navigateur de hello et la fenêtre de l’application console hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-234">Close hello browser and hello console application window.</span></span>
2. <span data-ttu-id="8e49c-235">Suivez les étapes de hello Bonjour [tooAzure avec la base de données de publication](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span><span class="sxs-lookup"><span data-stu-id="8e49c-235">Follow hello steps in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="8e49c-236">Après avoir terminé les étapes de hello pour le déploiement, continuer hello tâches restantes décrites dans cet article.</span><span class="sxs-lookup"><span data-stu-id="8e49c-236">After you complete hello steps for deploying, continue with hello remaining tasks in this article.</span></span>

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="8e49c-237">Configurer hello web application toouse votre compte de stockage et de la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8e49c-237">Configure hello web app toouse your Azure SQL database and storage account</span></span>
<span data-ttu-id="8e49c-238">Il est une meilleure pratique de sécurité trop[Évitez de placer des informations sensibles telles que des chaînes de connexion dans des fichiers qui sont stockés dans des référentiels de code source](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="8e49c-238">It's a security best practice too[avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="8e49c-239">Azure fournit un moyen toodo que : vous pouvez définir la chaîne de connexion et d’autres valeurs de paramètre Bonjour environnement Azure, et les API de configuration ASP.NET récupère automatiquement ces valeurs lors de l’application hello s’exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-239">Azure provides a way toodo that: you can set connection string and other setting values in hello Azure environment, and ASP.NET configuration APIs automatically pick up these values when hello app runs in Azure.</span></span> <span data-ttu-id="8e49c-240">Vous pouvez définir ces valeurs dans Azure à l’aide de **l’Explorateur de serveurs**, hello portail Azure, Windows PowerShell, ou hello interface de ligne de commande multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="8e49c-240">You can set these values in Azure by using **Server Explorer**, hello Azure Portal, Windows PowerShell, or hello cross-platform command-line interface.</span></span> <span data-ttu-id="8e49c-241">Pour plus d’informations, consultez [Fonctionnement des chaînes d’application et des chaînes de connexion](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="8e49c-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="8e49c-242">Dans cette section, vous utilisez **l’Explorateur de serveurs** tooset les valeurs de chaîne de connexion dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-242">In this section, you use **Server Explorer** tooset connection string values in Azure.</span></span>

1. <span data-ttu-id="8e49c-243">Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur votre application web sous **Azure > App Service {votre groupe de ressources}**, puis cliquez sur **Afficher les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="8e49c-244">Hello **application Web Azure** s’ouvre sur hello **Configuration** onglet.</span><span class="sxs-lookup"><span data-stu-id="8e49c-244">hello **Azure Web App** window opens on hello **Configuration** tab.</span></span>
2. <span data-ttu-id="8e49c-245">Modifier le nom de nom toohello de chaîne de connexion hello DefaultConnection hello choisis lors de la configuration de base de données SQL de hello Bonjour [tooAzure avec la base de données de publication](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) l’article.</span><span class="sxs-lookup"><span data-stu-id="8e49c-245">Change hello name of hello DefaultConnection connection string toohello name you chose when you configured hello SQL database in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="8e49c-246">Azure créé automatiquement cette chaîne de connexion lorsque vous avez créé l’application hello web avec une base de données associé, afin qu’il a déjà la valeur de chaîne de connexion adéquate hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-246">Azure automatically created this connection string when you created hello web app with an associated database, so it already has hello right connection string value.</span></span> <span data-ttu-id="8e49c-247">Vous modifiez simplement hello nom toowhat que recherche de votre code.</span><span class="sxs-lookup"><span data-stu-id="8e49c-247">You're changing just hello name toowhat your code is looking for.</span></span>
3. <span data-ttu-id="8e49c-248">Ajoutez deux chaînes de connexion nommées AzureWebJobsStorage et AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="8e49c-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="8e49c-249">Définir le type de base de données hello trop**personnalisé**et la même valeur que vous avez utilisé précédemment pour hello ensemble hello connexion chaîne valeur toohello *Web.config* et *App.config* fichiers.</span><span class="sxs-lookup"><span data-stu-id="8e49c-249">Set hello database type too**Custom**, and set hello connection string value toohello same value that you used earlier for hello *Web.config* and *App.config* files.</span></span> <span data-ttu-id="8e49c-250">(Veillez incluent la chaîne de connexion entière hello, pas seulement hello touche d’accès rapide et de ne pas inclure les guillemets hello.)</span><span class="sxs-lookup"><span data-stu-id="8e49c-250">(Be sure you include hello entire connection string, not just hello access key, and don't include hello quotation marks.)</span></span>

    <span data-ttu-id="8e49c-251">Ces chaînes de connexion sont utilisées par hello WebJobs SDK, l’autre pour les données d’application et un pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="8e49c-251">These connection strings are used by hello WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="8e49c-252">Comme vous l’avez vu précédemment, une hello pour les données d’application est également utilisé par le code hello web frontal.</span><span class="sxs-lookup"><span data-stu-id="8e49c-252">As you saw earlier, hello one for application data is also used by hello web front-end code.</span></span>
4. <span data-ttu-id="8e49c-253">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-253">Click **Save**.</span></span>

    ![Chaînes de connexion dans le portail Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="8e49c-255">Dans **l’Explorateur de serveurs**, avec le bouton droit de l’application hello web, puis cliquez sur **arrêter**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-255">In **Server Explorer**, right-click hello web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="8e49c-256">Après l’arrêt de l’application hello web, l’application hello web avec le bouton droit à nouveau, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-256">After hello web app stops, right-click hello web app again, and then click **Start**.</span></span>

   <span data-ttu-id="8e49c-257">Hello la tâche Web démarre automatiquement lorsque vous publiez, mais il s’arrête lorsque vous modifiez la configuration.</span><span class="sxs-lookup"><span data-stu-id="8e49c-257">hello WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="8e49c-258">toorestart, vous pouvez redémarrer l’application web hello ou redémarrez hello la tâche Web Bonjour [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="8e49c-258">toorestart it, you can either restart hello web app or restart hello WebJob in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="8e49c-259">Il est généralement recommandée toorestart hello web application après une modification de configuration.</span><span class="sxs-lookup"><span data-stu-id="8e49c-259">It's generally recommended toorestart hello web app after a configuration change.</span></span>
7. <span data-ttu-id="8e49c-260">Actualisez la fenêtre de navigateur hello qui a des URL de l’application hello web dans la barre d’adresse.</span><span class="sxs-lookup"><span data-stu-id="8e49c-260">Refresh hello browser window that has hello web app URL in its address bar.</span></span>

    <span data-ttu-id="8e49c-261">page d’accueil Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8e49c-261">hello home page appears.</span></span>
8. <span data-ttu-id="8e49c-262">Créer une annonce, comme vous le faisiez quand vous [s’exécutait localement des application hello](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="8e49c-262">Create an ad, as you did when you [ran hello application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="8e49c-263">page d’Index Hello affiche sans une vignette dans un premier temps.</span><span class="sxs-lookup"><span data-stu-id="8e49c-263">hello Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="8e49c-264">Actualiser la page de hello après quelques secondes et hello miniature s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8e49c-264">Refresh hello page after a few seconds and hello thumbnail appears.</span></span>

   <span data-ttu-id="8e49c-265">Si la miniature de hello n’apparaît pas, vous peut-être toowait environ une minute pour toorestart de la tâche Web hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-265">If hello thumbnail doesn't appear, you might have toowait a minute or so for hello WebJob toorestart.</span></span> <span data-ttu-id="8e49c-266">Si, après un certain temps, vous ne voyez toujours miniature hello lorsque vous actualisez la page hello, hello la tâche Web a ne peut-être pas démarré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="8e49c-266">If after a while, you still don't see hello thumbnail when you refresh hello page, hello WebJob might not have started automatically.</span></span> <span data-ttu-id="8e49c-267">Dans ce cas, accédez toohello **des Services d’application** panneau Bonjour [portail Azure](https://portal.azure.com/), localisez votre application web, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-267">In that case, go toohello **App Services** blade in hello [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-hello-webjobs-sdk-dashboard"></a><span data-ttu-id="8e49c-268">Hello d’affichage du tableau de bord WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="8e49c-268">View hello WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="8e49c-269">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez hello **panneau des Services d’application**, localisez votre application web, puis sélectionnez **WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-269">In hello [Azure portal](https://portal.azure.com/), select hello **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="8e49c-270">Sélectionnez hello **journaux** onglet.</span><span class="sxs-lookup"><span data-stu-id="8e49c-270">Select hello **Logs** tab.</span></span>

    ![Onglet journaux](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="8e49c-272">Un nouvel onglet de navigateur s’ouvre toohello du tableau de bord WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="8e49c-272">A new browser tab opens toohello WebJobs SDK dashboard.</span></span> <span data-ttu-id="8e49c-273">tableau de bord Hello montre que hello la tâche Web est en cours d’exécution et affiche la liste des fonctions dans votre code que hello que webjobs SDK est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="8e49c-273">hello dashboard shows that hello WebJob is running and shows a list of functions in your code that hello WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="8e49c-274">Cliquez sur un des détails de toosee fonctions hello concernant son exécution.</span><span class="sxs-lookup"><span data-stu-id="8e49c-274">Click one of hello functions toosee details about its execution.</span></span>

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="8e49c-277">Hello **relecture fonction** bouton sur cette page provoque la hello WebJobs SDK framework toocall hello fonction à nouveau, et elle vous offre une fonction de probabilité toochange hello données passées toohello tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="8e49c-277">hello **Replay Function** button on this page causes hello WebJobs SDK framework toocall hello function again, and it gives you a chance toochange hello data passed toohello function first.</span></span>

> [!NOTE]
> <span data-ttu-id="8e49c-278">Lorsque vous avez terminé de test, envisagez de supprimer hello web app, le compte de stockage et votre instance de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="8e49c-278">When you're finished testing, consider deleting hello web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="8e49c-279">l’application web Hello est libre, mais hello compte de stockage SQL et instance de base de données accumulent les coûts (et ce, minimal dû toohello de petite taille).</span><span class="sxs-lookup"><span data-stu-id="8e49c-279">hello web app is free, but hello SQL storage account and database instance accrue charges (albeit, minimal due toohello small size).</span></span> <span data-ttu-id="8e49c-280">En outre, si vous laissez hello web application est en cours d’exécution, toute personne qui recherche l’URL peut créer et d’afficher des publicités.</span><span class="sxs-lookup"><span data-stu-id="8e49c-280">Also, if you leave hello web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="8e49c-281">Supprimer votre application web</span><span class="sxs-lookup"><span data-stu-id="8e49c-281">Delete your web app</span></span>
<span data-ttu-id="8e49c-282">Dans le portail de hello, accédez toohello **des Services d’application** panneau, recherchez et sélectionnez votre application web, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-282">In hello portal, go toohello **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="8e49c-283">Si vous souhaitez simplement tootemporarily empêcher d’autres utilisateurs d’accéder à l’application hello web, cliquez sur **arrêter** à la place.</span><span class="sxs-lookup"><span data-stu-id="8e49c-283">If you just want tootemporarily prevent others from accessing hello web app, click **Stop** instead.</span></span> <span data-ttu-id="8e49c-284">Dans ce cas, interrompt tooaccrue pour hello compte de stockage et de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="8e49c-284">In that case, charges will continue tooaccrue for hello SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="8e49c-285">Supprimer votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="8e49c-285">Delete your storage account</span></span>
<span data-ttu-id="8e49c-286">toodelete votre compte de stockage, consultez [supprimer un compte de stockage](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="8e49c-286">toodelete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="8e49c-287">Supprimer de votre base de données</span><span class="sxs-lookup"><span data-stu-id="8e49c-287">Delete your database</span></span>
<span data-ttu-id="8e49c-288">toodelete SQL de base de données, consultez hello [API REST de Azure SQL Database](https://docs.microsoft.com/rest/api/sql/) documentation.</span><span class="sxs-lookup"><span data-stu-id="8e49c-288">toodelete your SQL database, see hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="8e49c-289"><a id="create"></a>Créer l’application hello à partir de zéro</span><span class="sxs-lookup"><span data-stu-id="8e49c-289"><a id="create"></a>Create hello application from scratch</span></span>
<span data-ttu-id="8e49c-290">Dans cette section, vous effectuerez hello tâche suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e49c-290">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="8e49c-291">création d'une solution Visual Studio avec un projet web ;</span><span class="sxs-lookup"><span data-stu-id="8e49c-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="8e49c-292">Ajouter un projet de bibliothèque de classes pour les données de salutation couche d’accès qui est partagée entre le serveur frontal hello et back end.</span><span class="sxs-lookup"><span data-stu-id="8e49c-292">Add a class library project for hello data access layer that is shared between hello front end and back end.</span></span>
* <span data-ttu-id="8e49c-293">Ajouter un projet d’Application Console pour hello principal, avec les tâches Web déploiement est activé.</span><span class="sxs-lookup"><span data-stu-id="8e49c-293">Add a Console Application project for hello backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="8e49c-294">ajout de packages NuGet ;</span><span class="sxs-lookup"><span data-stu-id="8e49c-294">Add NuGet packages.</span></span>
* <span data-ttu-id="8e49c-295">définition des références d'un projet ;</span><span class="sxs-lookup"><span data-stu-id="8e49c-295">Set project references.</span></span>
* <span data-ttu-id="8e49c-296">Copiez les fichiers de configuration et le code d’application à partir de l’application hello téléchargé que vous avez travaillé avec dans la section précédente de hello du didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-296">Copy application code and configuration files from hello downloaded application that you worked with in hello previous section of hello tutorial.</span></span>
* <span data-ttu-id="8e49c-297">Passez en revue les parties hello du code de hello qui fonctionnent avec les objets BLOB Windows Azure et files d’attente et hello WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="8e49c-297">Review hello parts of hello code that work with Azure blobs and queues and hello WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="8e49c-298">Création d'une solution Visual Studio avec un projet web et un projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="8e49c-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="8e49c-299">Dans Visual Studio, choisissez **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="8e49c-300">Bonjour **nouveau projet** boîte de dialogue, choisissez **Visual C#** > **Web** > **ASP.NET Web Application(.NETFramework)**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-300">In hello **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="8e49c-301">Nommez le projet hello ContosoAdsWeb, nommez hello solution ContosoAdsWebJobsSDK (modifier le nom de la solution hello si placez Bonjour même dossier que hello téléchargé solution), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-301">Name hello project ContosoAdsWeb, name hello solution ContosoAdsWebJobsSDK (change hello solution name if you're putting it in hello same folder as hello downloaded solution), and then click **OK**.</span></span>

    ![Nouveau projet](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="8e49c-303">Bonjour **nouvelle Application Web ASP.NET** boîte de dialogue, choisissez le modèle MVC de hello, puis sélectionnez **modifier l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-303">In hello **New ASP.NET Web Application** dialog, choose hello MVC template, and select **Change Authentication**.</span></span>

    ![Modifier l'authentification](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="8e49c-305">Bonjour **modifier l’authentification** boîte de dialogue, choisissez **aucune authentification**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-305">In hello **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Aucune authentification](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="8e49c-307">Bonjour **nouvelle Application Web ASP.NET** boîte de dialogue, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-307">In hello **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="8e49c-308">Visual Studio crée la solution de hello et de projet web de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-308">Visual Studio creates hello solution and hello web project.</span></span>
7. <span data-ttu-id="8e49c-309">Dans **l’Explorateur de solutions**, avec le bouton droit de la solution de hello (pas le projet hello), puis choisissez **ajouter** > **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-309">In **Solution Explorer**, right-click hello solution (not hello project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="8e49c-310">Bonjour **ajouter un nouveau projet** boîte de dialogue, choisissez **Visual C#** > **de bureau Windows classique** > **bibliothèque de classes (.NET Infrastructure)** modèle.</span><span class="sxs-lookup"><span data-stu-id="8e49c-310">In hello **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="8e49c-311">Projet de hello nom *ContosoAdsCommon*, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-311">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="8e49c-312">Ce projet contiendra au contexte d’Entity Framework hello hello modèle de données et qui les deux hello front-end et back-end utilisera.</span><span class="sxs-lookup"><span data-stu-id="8e49c-312">This project will contain hello Entity Framework context and hello data model which both hello front end and back end will use.</span></span> <span data-ttu-id="8e49c-313">En guise d’alternative, vous pouvez définir des classes liées EF de hello dans le projet web de hello et faire référence à ce projet à partir du projet de tâche Web hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-313">As an alternative, you could define hello EF-related classes in hello web project and reference that project from hello WebJob project.</span></span> <span data-ttu-id="8e49c-314">Toutefois, puis votre projet de tâche Web aurait un assemblys de tooweb de référence, elle n’a pas besoin.</span><span class="sxs-lookup"><span data-stu-id="8e49c-314">But, then your WebJob project would have a reference tooweb assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="8e49c-315">Ajout d'un projet d'application console dont le déploiement de tâches web est activé</span><span class="sxs-lookup"><span data-stu-id="8e49c-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="8e49c-316">Projet de web hello (et non hello solution ou projet de bibliothèque de classes hello) d’avec le bouton droit, puis cliquez sur **ajouter** > **nouveau projet de la tâche Web Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-316">Right-click hello web project (not hello solution or hello class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![New Azure WebJob Project menu selection](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="8e49c-318">Bonjour **ajouter de la tâche Web Azure** boîte de dialogue, entrez les deux hello ContosoAdsWebJob **nom du projet** et hello **nom de la tâche Web**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-318">In hello **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both hello **Project name** and hello **WebJob name**.</span></span> <span data-ttu-id="8e49c-319">Laissez **mode d’exécution de tâche Web** défini trop**exécuter en permanence**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-319">Leave **WebJob run mode** set too**Run Continuously**.</span></span>
3. <span data-ttu-id="8e49c-320">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-320">Click **OK**.</span></span>

   <span data-ttu-id="8e49c-321">Visual Studio crée une application Console qui est toodeploy configuré comme une tâche Web chaque fois que vous déployez le projet web de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-321">Visual Studio creates a Console application that is configured toodeploy as a WebJob whenever you deploy hello web project.</span></span> <span data-ttu-id="8e49c-322">toodo, elle effectuée hello tâches suivantes après avoir créé le projet de hello :</span><span class="sxs-lookup"><span data-stu-id="8e49c-322">toodo that, it performed hello following tasks after creating hello project:</span></span>

   * <span data-ttu-id="8e49c-323">Ajouter un *settings.json publier la tâche Web* fichier dans le dossier de propriétés de projet de la tâche Web hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-323">Added a *webjob-publish-settings.json* file in hello WebJob project Properties folder.</span></span>
   * <span data-ttu-id="8e49c-324">Ajouter un *webjobs-list.json* fichier dans le dossier de propriétés du projet web hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-324">Added a *webjobs-list.json* file in hello web project Properties folder.</span></span>
   * <span data-ttu-id="8e49c-325">Installé hello package NuGet de Microsoft.Web.WebJobs.Publish dans le projet de tâche Web hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-325">Installed hello Microsoft.Web.WebJobs.Publish NuGet package in hello WebJob project.</span></span>

   <span data-ttu-id="8e49c-326">Pour plus d’informations sur ces modifications, consultez [comment toodeploy tâches Web à l’aide de Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="8e49c-326">For more information about these changes, see [How toodeploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="8e49c-327">Ajout de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="8e49c-327">Add NuGet packages</span></span>
<span data-ttu-id="8e49c-328">modèle de nouveau projet Hello pour un projet de la tâche Web installe automatiquement le package WebJobs NuGet de kit de développement logiciel de hello [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="8e49c-328">hello new-project template for a WebJob project automatically installs hello WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="8e49c-329">Un des hello dépendances de WebJobs SDK est installé automatiquement dans le projet de tâche Web hello est Bonjour Azure Storage Client Library (SCL).</span><span class="sxs-lookup"><span data-stu-id="8e49c-329">One of hello WebJobs SDK dependencies that is installed automatically in hello WebJob project is hello Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="8e49c-330">Toutefois, vous devez tooadd il toohello toowork de projet web avec les objets BLOB et files d’attente.</span><span class="sxs-lookup"><span data-stu-id="8e49c-330">However, you need tooadd it toohello web project toowork with blobs and queues.</span></span>

1. <span data-ttu-id="8e49c-331">Ouvrez hello **gérer les Packages NuGet** boîte de dialogue pour les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-331">Open hello **Manage NuGet Packages** dialog for hello solution.</span></span>
2. <span data-ttu-id="8e49c-332">Dans le volet gauche de hello, sélectionnez **les packages installés**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-332">In hello left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="8e49c-333">Recherche hello *Azure Storage* du package, puis cliquez sur **gérer**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-333">Find hello *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="8e49c-334">Bonjour **sélectionner les projets** boîte, sélectionnez hello **ContosoAdsWeb** case à cocher, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-334">In hello **Select Projects** box, select hello **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="8e49c-335">Les trois projets utilisent hello Entity Framework toowork avec des données dans la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="8e49c-335">All three projects use hello Entity Framework toowork with data in SQL Database.</span></span>
5. <span data-ttu-id="8e49c-336">Dans le volet gauche de hello, sélectionnez **Online**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-336">In hello left pane, select **Online**.</span></span>
6. <span data-ttu-id="8e49c-337">Recherche hello *EntityFramework* NuGet package et l’installer dans les trois projets.</span><span class="sxs-lookup"><span data-stu-id="8e49c-337">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="8e49c-338">Définition des références de projet</span><span class="sxs-lookup"><span data-stu-id="8e49c-338">Set project references</span></span>
<span data-ttu-id="8e49c-339">Web et projets de la tâche Web fonctionnent avec la base de données SQL hello, donc les deux doivent être une référence de projet de ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-339">Both web and WebJob projects work with hello SQL database, so both need a reference toohello ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="8e49c-340">Dans le projet de ContosoAdsWeb hello, définissez une référence de projet de ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-340">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="8e49c-341">(Projet de ContosoAdsWeb hello d’avec le bouton droit, puis cliquez sur **ajouter** > **référence**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-341">(Right-click hello ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="8e49c-342">Bonjour **Gestionnaire de références** boîte de dialogue, sélectionnez **projets** > **Solution** > **ContosoAdsCommon**, puis cliquez sur **OK**.)</span><span class="sxs-lookup"><span data-stu-id="8e49c-342">In hello **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="8e49c-343">projet de tâche Web Hello nécessite des références pour utiliser des images et pour accéder aux chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="8e49c-343">hello WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="8e49c-344">Dans le projet de ContosoAdsWebJob hello, définissez une référence trop`System.Drawing` et `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="8e49c-344">In hello ContosoAdsWebJob project, set a reference too`System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="8e49c-345">Ajout de fichiers de code et de configuration</span><span class="sxs-lookup"><span data-stu-id="8e49c-345">Add code and configuration files</span></span>
<span data-ttu-id="8e49c-346">Ce didacticiel n’illustre pas comment trop[créer des vues à l’aide de la structure et les contrôleurs MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), comment trop[écrire du code d’Entity Framework qui fonctionne avec les bases de données SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), ou [hello notions de base de programmation asynchrone dans ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="8e49c-346">This tutorial does not show how too[create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how too[write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [hello basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="8e49c-347">Par conséquent, tout ce qui reste toodo est la copie des fichiers de code et la configuration de solution hello téléchargé dans une nouvelle solution hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-347">So, all that remains toodo is copy code and configuration files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="8e49c-348">Après quoi, hello sections suivantes montrent et expliquent les éléments clés du code de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-348">After you do that, hello following sections show and explain key parts of hello code.</span></span>

<span data-ttu-id="8e49c-349">tooa projet ou un dossier, projet de hello avec le bouton droit ou un dossier et cliquez sur les fichiers tooadd **ajouter** > **élément existant**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-349">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="8e49c-350">Sélectionnez hello fichiers que vous cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-350">Select hello files you want and click **Add**.</span></span> <span data-ttu-id="8e49c-351">Si vous êtes invité tooreplace des fichiers existants, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="8e49c-351">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="8e49c-352">Dans le projet de ContosoAdsCommon hello, supprimez hello *Class1.cs* et ajoutez son Bonjour place fichiers suivants à partir de projet de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="8e49c-352">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="8e49c-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="8e49c-353">*Ad.cs*</span></span>
   * <span data-ttu-id="8e49c-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="8e49c-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="8e49c-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="8e49c-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="8e49c-356">Dans le projet de ContosoAdsWeb hello, ajoutez hello fichiers suivants à partir de projet de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="8e49c-356">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="8e49c-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="8e49c-357">*Web.config*</span></span>
   * <span data-ttu-id="8e49c-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="8e49c-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="8e49c-359">Bonjour *contrôleurs* dossier : *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="8e49c-359">In hello *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="8e49c-360">Bonjour *Views\Shared* dossier : *_Layout.cshtml* fichier</span><span class="sxs-lookup"><span data-stu-id="8e49c-360">In hello *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="8e49c-361">Bonjour *Views\Home* dossier : *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="8e49c-361">In hello *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="8e49c-362">Bonjour *Views\Ad* dossier (créez d’abord le dossier de hello) : cinq *.cshtml* fichiers</span><span class="sxs-lookup"><span data-stu-id="8e49c-362">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="8e49c-363">Dans le projet de ContosoAdsWebJob hello, ajoutez hello fichiers suivants à partir de projet de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="8e49c-363">In hello ContosoAdsWebJob project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="8e49c-364">*App.config* (modifier le filtre de type de fichier hello trop**tous les fichiers**)</span><span class="sxs-lookup"><span data-stu-id="8e49c-364">*App.config* (change hello file type filter too**All Files**)</span></span>
   * <span data-ttu-id="8e49c-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="8e49c-365">*Program.cs*</span></span>
   * <span data-ttu-id="8e49c-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="8e49c-366">*Functions.cs*</span></span>

<span data-ttu-id="8e49c-367">Vous pouvez maintenant générer, exécuter et déployer l’application hello comme indiqué plus haut dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-367">You can now build, run, and deploy hello application as instructed earlier in hello tutorial.</span></span> <span data-ttu-id="8e49c-368">Avant cela, toutefois, l’arrêter hello la tâche Web qui s’exécute toujours dans la première application web hello, sur que vous avez déployé.</span><span class="sxs-lookup"><span data-stu-id="8e49c-368">Before you do that, however, stop hello WebJob that is still running in hello first web app you deployed to.</span></span> <span data-ttu-id="8e49c-369">Sinon, cette tâche Web sera traiter les messages de file d’attente créées localement ou par application hello en cours d’exécution dans une application web, étant donné que tous les utilisez hello même compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e49c-369">Otherwise, that WebJob will process queue messages created locally or by hello app running in a new web app, since all are using hello same storage account.</span></span>

## <span data-ttu-id="8e49c-370"><a id="code"></a>Passez en revue le code de l’application hello</span><span class="sxs-lookup"><span data-stu-id="8e49c-370"><a id="code"></a>Review hello application code</span></span>
<span data-ttu-id="8e49c-371">Hello sections suivantes expliquent les code hello liées tooworking avec hello WebJobs SDK et les objets BLOB de stockage Azure et files d’attente.</span><span class="sxs-lookup"><span data-stu-id="8e49c-371">hello following sections explain hello code related tooworking with hello WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="8e49c-372">Pour toohello spécifique hello code WebJobs SDK, consultez toohello [Program.cs et Functions.cs](#programcs) sections.</span><span class="sxs-lookup"><span data-stu-id="8e49c-372">For hello code specific toohello WebJobs SDK, go toohello [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="8e49c-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="8e49c-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="8e49c-374">fichier de Ad.cs Hello définit un enum pour les catégories d’Active Directory et une classe d’entité POCO pour les informations Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e49c-374">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="8e49c-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="8e49c-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="8e49c-376">Hello ContosoAdsContext classe spécifie que la classe de publicité de hello est utilisée dans une collection DbSet, Entity Framework stocke dans une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="8e49c-376">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="8e49c-377">classe Hello possède deux constructeurs.</span><span class="sxs-lookup"><span data-stu-id="8e49c-377">hello class has two constructors.</span></span> <span data-ttu-id="8e49c-378">tout d’abord Hello est utilisé par le projet de hello web et spécifie le nom de hello d’une chaîne de connexion qui est stockée dans le fichier Web.config de hello ou un environnement d’exécution Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-378">hello first is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file or hello Azure runtime environment.</span></span> <span data-ttu-id="8e49c-379">constructeur de deuxième Hello vous permet de toopass dans la chaîne de connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-379">hello second constructor enables you toopass in hello actual connection string.</span></span> <span data-ttu-id="8e49c-380">Qui est requis par le projet de tâche Web hello car celui-ci ne dispose d’un fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="8e49c-380">That is needed by hello WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="8e49c-381">Vous savez où cette chaîne de connexion a été stockée, et vous verrez plus tard comment les code hello récupère la chaîne de connexion hello lorsqu’il instancie la classe DbContext de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-381">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="8e49c-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="8e49c-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="8e49c-383">Hello `BlobInformation` classe est utilisée toostore d’informations sur un objet blob d’image dans un message de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8e49c-383">hello `BlobInformation` class is used toostore information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="8e49c-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="8e49c-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="8e49c-385">Code qui est appelé à partir de hello `Application_Start` méthode crée un *images* conteneur d’objets blob et un *images* file d’attente si elles n’existent pas déjà.</span><span class="sxs-lookup"><span data-stu-id="8e49c-385">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="8e49c-386">Cela garantit que chaque fois que vous démarrez à l’aide d’un compte de stockage, hello requis file d’attente et le conteneur d’objets blob sont créés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="8e49c-386">This ensures that whenever you start using a new storage account, hello required blob container and queue are created automatically.</span></span>

<span data-ttu-id="8e49c-387">Hello compte de stockage toohello code obtient l’accès à l’aide de chaînes de connexion de stockage hello de hello *Web.config* fichier ou un environnement d’exécution Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-387">hello code gets access toohello storage account by using hello storage connection string from hello *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="8e49c-388">Ensuite, il obtient une référence toohello *images* conteneur d’objets blob, crée le conteneur de hello si elle n’existe pas déjà, et définit les autorisations sur le conteneur hello d’accès.</span><span class="sxs-lookup"><span data-stu-id="8e49c-388">Then, it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="8e49c-389">Par défaut, les nouveaux conteneurs autorisent uniquement les clients avec des objets BLOB de stockage compte informations d’identification tooaccess.</span><span class="sxs-lookup"><span data-stu-id="8e49c-389">By default, new containers allow only clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="8e49c-390">l’application web Hello doit hello BLOB toobe public afin qu’il peut afficher des images à l’aide de l’URL que BLOB d’image toohello de point de.</span><span class="sxs-lookup"><span data-stu-id="8e49c-390">hello web app needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="8e49c-391">Un code similaire Obtient une référence toohello *thumbnailrequest* de file d’attente et crée une nouvelle file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8e49c-391">Similar code gets a reference toohello *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="8e49c-392">Dans ce cas, aucune modification des autorisations n'est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8e49c-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="8e49c-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="8e49c-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="8e49c-394">Hello *_Layout.cshtml* fichier définit le nom de l’application hello dans l’en-tête de hello et de pied de page et crée une entrée de menu « Annonces ».</span><span class="sxs-lookup"><span data-stu-id="8e49c-394">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="8e49c-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="8e49c-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="8e49c-396">Hello *Views\Home\Index.cshtml* fichier affiche les liens de catégorie sur la page d’accueil hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-396">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="8e49c-397">les liens Hello passent entier hello hello `Category` enum dans une page d’Index de publicités toohello variable querystring.</span><span class="sxs-lookup"><span data-stu-id="8e49c-397">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="8e49c-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="8e49c-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="8e49c-399">Bonjour *AdController.cs* fichier, les appels de constructeur Bonjour Bonjour `InitializeStorage` méthode toocreate bibliothèque cliente de stockage Azure objets qui fournissent une API pour l’utilisation des objets BLOB et files d’attente.</span><span class="sxs-lookup"><span data-stu-id="8e49c-399">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="8e49c-400">Code de hello extrait ensuite une référence toohello *images* conteneur d’objets blob comme vous l’avez vu précédemment dans *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="8e49c-400">Then, hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="8e49c-401">Ce faisant, il définit une [stratégie de nouvelles tentatives](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) par défaut appropriée pour une application web.</span><span class="sxs-lookup"><span data-stu-id="8e49c-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="8e49c-402">stratégie de nouvelle tentative interruption exponentielle Hello par défaut se bloque hello web app pour plus d’une minute sur les tentatives répétées d’une erreur transitoire.</span><span class="sxs-lookup"><span data-stu-id="8e49c-402">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="8e49c-403">stratégie de nouvelle tentative Hello spécifié ici attend trois secondes après chacun pour des tentatives de toothree.</span><span class="sxs-lookup"><span data-stu-id="8e49c-403">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="8e49c-404">Un code similaire Obtient une référence toohello *images* file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8e49c-404">Similar code gets a reference toohello *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="8e49c-405">La plupart du code du contrôleur hello est typique pour travailler avec un modèle de données Entity Framework à l’aide d’une classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="8e49c-405">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="8e49c-406">Une exception est hello HttpPost `Create` (méthode), qui télécharge un fichier et l’enregistre dans le stockage blob.</span><span class="sxs-lookup"><span data-stu-id="8e49c-406">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="8e49c-407">classeur de modèles Hello fournit un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello méthode de l’objet.</span><span class="sxs-lookup"><span data-stu-id="8e49c-407">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="8e49c-408">Si l’utilisateur hello sélectionné un tooupload de fichier, code de hello télécharge hello fichier enregistre dans un objet blob et met à jour d’enregistrement de base de données Ad hello avec une URL qui pointe toohello blob.</span><span class="sxs-lookup"><span data-stu-id="8e49c-408">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="8e49c-409">Hello code hello téléchargement est hello `UploadAndSaveBlobAsync` (méthode).</span><span class="sxs-lookup"><span data-stu-id="8e49c-409">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="8e49c-410">Il crée un nom GUID pour les objets blob de hello, téléchargements et enregistre le fichier hello et retourne un objet blob de référence toohello enregistré.</span><span class="sxs-lookup"><span data-stu-id="8e49c-410">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

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

<span data-ttu-id="8e49c-411">Après avoir hello HttpPost `Create` méthode télécharge un objet blob et les mises à jour hello de base de données, il crée un file d’attente message tooinform hello au processus principal qu’une image est prête pour la miniature tooa de conversion.</span><span class="sxs-lookup"><span data-stu-id="8e49c-411">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform hello back-end process that an image is ready for conversion tooa thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="8e49c-412">Hello code hello HttpPost `Edit` méthode est similaire, mais si l’utilisateur de hello sélectionne un fichier image, tous les objets BLOB qui existent déjà pour cette ad doivent être supprimés.</span><span class="sxs-lookup"><span data-stu-id="8e49c-412">hello code for hello HttpPost `Edit` method is similar, except that if hello user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="8e49c-413">Voici le code hello qui supprime des objets BLOB lorsque vous supprimez une annonce :</span><span class="sxs-lookup"><span data-stu-id="8e49c-413">Here is hello code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="8e49c-414">ContosoAdsWeb - Views\Ad\Index.cshtml et Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="8e49c-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="8e49c-415">Hello *Index.cshtml* fichier affiche les miniatures avec hello autres données d’Active Directory :</span><span class="sxs-lookup"><span data-stu-id="8e49c-415">hello *Index.cshtml* file displays thumbnails with hello other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="8e49c-416">Hello *Details.cshtml* fichier image en taille réelle de hello s’affiche :</span><span class="sxs-lookup"><span data-stu-id="8e49c-416">hello *Details.cshtml* file displays hello full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="8e49c-417">ContosoAdsWeb - Views\Ad\Create.cshtml et Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="8e49c-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="8e49c-418">Hello *Create.cshtml* et *Edit.cshtml* fichiers spécifient qu’Active hello hello tooget de contrôleur d’encodage de formulaire `HttpPostedFileBase` objet.</span><span class="sxs-lookup"><span data-stu-id="8e49c-418">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="8e49c-419">Un `<input>` élément indique hello navigateur tooprovide une boîte de dialogue de sélection de fichier.</span><span class="sxs-lookup"><span data-stu-id="8e49c-419">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="8e49c-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="8e49c-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="8e49c-421">Lorsque hello démarre la tâche Web hello `Main` les appels de méthode hello WebJobs SDK `JobHost.RunAndBlock` toobegin exécution de la méthode de fonctions déclenchées sur le thread en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-421">When hello WebJob starts, hello `Main` method calls hello WebJobs SDK `JobHost.RunAndBlock` method toobegin execution of triggered functions on hello current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="8e49c-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - Méthode GenerateThumbnail</span><span class="sxs-lookup"><span data-stu-id="8e49c-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="8e49c-423">Hello WebJobs SDK appelle cette méthode lorsqu’un message de la file d’attente est reçu.</span><span class="sxs-lookup"><span data-stu-id="8e49c-423">hello WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="8e49c-424">méthode Hello crée une miniature et met hello miniature URL dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-424">hello method creates a thumbnail and puts hello thumbnail URL in hello database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="8e49c-425">Hello `QueueTrigger` attribut dirige hello WebJobs SDK toocall cette méthode lorsqu’un nouveau message est reçu dans la file d’attente de thumbnailrequest hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-425">hello `QueueTrigger` attribute directs hello WebJobs SDK toocall this method when a new message is received on hello thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="8e49c-426">Hello `BlobInformation` objet dans le message de file d’attente hello est automatiquement désérialisée en hello `blobInfo` paramètre.</span><span class="sxs-lookup"><span data-stu-id="8e49c-426">hello `BlobInformation` object in hello queue message is automatically deserialized into hello `blobInfo` parameter.</span></span> <span data-ttu-id="8e49c-427">Lors de la fin de la méthode hello, message de file d’attente hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="8e49c-427">When hello method completes, hello queue message is deleted.</span></span> <span data-ttu-id="8e49c-428">Si la méthode hello échoue avant la fin, le message de file d’attente hello n’est pas supprimé ; après l’expiration d’un bail de 10 minutes, message de type hello est lancé toobe nouveau récupéré et traité.</span><span class="sxs-lookup"><span data-stu-id="8e49c-428">If hello method fails before completing, hello queue message is not deleted; after a 10-minute lease expires, hello message is released toobe picked up again and processed.</span></span> <span data-ttu-id="8e49c-429">Cette séquence ne se répète pas indéfiniment si un message provoque toujours une exception.</span><span class="sxs-lookup"><span data-stu-id="8e49c-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="8e49c-430">Après échec de 5 tentatives tooprocess un message, message de type hello est déplacé tooa file d’attente nommée {nom}-incohérents.</span><span class="sxs-lookup"><span data-stu-id="8e49c-430">After 5 unsuccessful attempts tooprocess a message, hello message is moved tooa queue named {queuename}-poison.</span></span> <span data-ttu-id="8e49c-431">Hello le nombre maximal de tentatives est configurable.</span><span class="sxs-lookup"><span data-stu-id="8e49c-431">hello maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="8e49c-432">deux Hello `Blob` attributs fournissent des objets qui sont liées tooblobs : un toohello existant objet blob d’image et un tooa nouvelle miniature blob qui crée de la méthode hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-432">hello two `Blob` attributes provide objects that are bound tooblobs: one toohello existing image blob and one tooa new thumbnail blob that hello method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="8e49c-433">Noms d’objets BLOB proviennent des propriétés de hello `BlobInformation` objet reçu dans le message de file d’attente hello (`BlobName` et `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="8e49c-433">Blob names come from properties of hello `BlobInformation` object received in hello queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="8e49c-434">tooget hello toutes les fonctionnalités de hello bibliothèque cliente de stockage, vous pouvez utiliser hello `CloudBlockBlob` toowork de classe avec des objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="8e49c-434">tooget hello full functionality of hello Storage Client Library, you can use hello `CloudBlockBlob` class toowork with blobs.</span></span> <span data-ttu-id="8e49c-435">Si vous souhaitez tooreuse le code qui a été écrite toowork avec `Stream` des objets, vous pouvez utiliser hello `Stream` classe.</span><span class="sxs-lookup"><span data-stu-id="8e49c-435">If you want tooreuse code that was written toowork with `Stream` objects, you can use hello `Stream` class.</span></span>

<span data-ttu-id="8e49c-436">Pour plus d’informations sur le mode de fonctionnement toowrite qui utilisent des attributs WebJobs SDK, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="8e49c-436">For more information about how toowrite functions that use  WebJobs SDK attributes, see hello following resources:</span></span>

* [<span data-ttu-id="8e49c-437">Comment toouse Azure file d’attente de stockage avec hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="8e49c-437">How toouse Azure queue storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="8e49c-438">Comment toouse Azure stockage d’objets blob par hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="8e49c-438">How toouse Azure blob storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="8e49c-439">Comment toouse Azure table storage avec hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="8e49c-439">How toouse Azure table storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="8e49c-440">Comment toouse Azure Service Bus avec hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="8e49c-440">How toouse Azure Service Bus with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="8e49c-441">Si votre application web s’exécute sur plusieurs machines virtuelles, plusieurs tâches Web s’exécuteront simultanément et dans certains scénarios, cela peut entraîner de hello même les données traitées plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="8e49c-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in hello same data getting processed multiple times.</span></span> <span data-ttu-id="8e49c-442">Cela n’est pas un problème si vous utilisez la file d’attente intégrées de hello, blob et les déclencheurs de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8e49c-442">This is not a problem if you use hello built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="8e49c-443">Hello SDK garantit que vos fonctions seront traitées qu’une seule fois pour chaque message ou d’un objet blob.</span><span class="sxs-lookup"><span data-stu-id="8e49c-443">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="8e49c-444">Pour plus d’informations sur l’arrêt correct de tooimplement, consultez [l’arrêt approprié](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="8e49c-444">For information about how tooimplement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="8e49c-445">Hello code Bonjour `ConvertImageToThumbnailJPG` (méthode) (non affiché) utilise des classes hello `System.Drawing` espace de noms par souci de simplicité.</span><span class="sxs-lookup"><span data-stu-id="8e49c-445">hello code in hello `ConvertImageToThumbnailJPG` method (not shown) uses classes in hello `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="8e49c-446">Toutefois, les classes de hello dans cet espace de noms ont été conçues pour une utilisation avec Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="8e49c-446">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="8e49c-447">Elles ne sont pas prises en charge dans un service Windows ou ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8e49c-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="8e49c-448">Pour plus d’informations sur les options de traitement d’images, consultez les rubriques [Génération d’images dynamiques](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) et [Redimensionnement d’images approfondi](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="8e49c-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="8e49c-449">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e49c-449">Next steps</span></span>
<span data-ttu-id="8e49c-450">Dans ce didacticiel, vous avez vu d’une application à plusieurs niveaux simple qui utilise hello WebJobs SDK pour le traitement du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="8e49c-450">In this tutorial, you've seen a simple multi-tier application that uses hello WebJobs SDK for backend processing.</span></span> <span data-ttu-id="8e49c-451">Cette section propose des suggestions pour en savoir plus sur les applications à plusieurs niveaux ASP.NET et WebJobs.</span><span class="sxs-lookup"><span data-stu-id="8e49c-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="8e49c-452">Fonctionnalités manquantes</span><span class="sxs-lookup"><span data-stu-id="8e49c-452">Missing features</span></span>
<span data-ttu-id="8e49c-453">application Hello a été conservée simple pour obtenir un didacticiel de mise en route.</span><span class="sxs-lookup"><span data-stu-id="8e49c-453">hello application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="8e49c-454">Dans une application réelle, vous pouvez implémenter [injection de dépendance](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) et hello [référentiel et une unité de travaillent des modèles](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), utilisez [une interface pour la journalisation](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), utilisez [ Migrations EF Code First](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage données modifications sur le modèle et utiliser [résilience des connexions EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage les erreurs temporaires du réseau.</span><span class="sxs-lookup"><span data-stu-id="8e49c-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="8e49c-455">Mise à l’échelle de WebJobs</span><span class="sxs-lookup"><span data-stu-id="8e49c-455">Scaling WebJobs</span></span>
<span data-ttu-id="8e49c-456">Les tâches Web s’exécutent dans le contexte de hello d’une application web, ne sont pas évolutifs séparément.</span><span class="sxs-lookup"><span data-stu-id="8e49c-456">WebJobs run in hello context of a web app and are not scalable separately.</span></span> <span data-ttu-id="8e49c-457">Par exemple, si vous avez une instance d’application web Standard, vous n'avez qu’une seule instance du processus d’arrière-plan en cours d’exécution et qu’il utilise certaines hello des ressources du serveur (processeur, mémoire, etc.) qui seraient sinon le contenu web tooserve disponibles.</span><span class="sxs-lookup"><span data-stu-id="8e49c-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of hello server resources (CPU, memory, etc.) that otherwise would be available tooserve web content.</span></span>

<span data-ttu-id="8e49c-458">Si le trafic varie selon le temps ou le jour de la semaine, et si principal hello traitement vous devez toodo peut attendre, vous pouvez planifier votre toorun tâches Web à des moments de faible trafic.</span><span class="sxs-lookup"><span data-stu-id="8e49c-458">If traffic varies by time of day or day of week, and if hello backend processing you need toodo can wait, you could schedule your WebJobs toorun at low-traffic times.</span></span> <span data-ttu-id="8e49c-459">Si la charge de hello est toujours trop élevé pour cette solution, vous pouvez exécuter hello principal en tant qu’une tâche Web dans une application web distinct dédiée à cet effet.</span><span class="sxs-lookup"><span data-stu-id="8e49c-459">If hello load is still too high for that solution, you can run hello backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="8e49c-460">Vous pouvez ensuite faire évoluer votre application web principale indépendamment de votre application web frontale.</span><span class="sxs-lookup"><span data-stu-id="8e49c-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="8e49c-461">Pour plus d’informations, consultez [Mise à l’échelle WebJobs](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="8e49c-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="8e49c-462">Éviter les arrêts dus à l’expiration des applications web</span><span class="sxs-lookup"><span data-stu-id="8e49c-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="8e49c-463">toomake que vos tâches Web sont toujours en cours d’exécution et en cours d’exécution sur toutes les instances de votre application web, vous avez tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8e49c-463">toomake sure your WebJobs are always running, and running on all instances of your web app, you have tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="8e49c-464">À l’aide de hello SDK WebJobs en dehors des tâches Web</span><span class="sxs-lookup"><span data-stu-id="8e49c-464">Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="8e49c-465">Un programme qui utilise hello WebJobs SDK ne toorun dans Azure dans une tâche Web.</span><span class="sxs-lookup"><span data-stu-id="8e49c-465">A program that uses hello WebJobs SDK doesn't have toorun in Azure in a WebJob.</span></span> <span data-ttu-id="8e49c-466">Il peut s'exécuter localement, ou dans d'autres environnements tels qu'un rôle de travail de service cloud ou un service Windows.</span><span class="sxs-lookup"><span data-stu-id="8e49c-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="8e49c-467">Toutefois, vous pouvez uniquement accéder hello du tableau de bord WebJobs SDK via une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49c-467">However, you can only access hello WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="8e49c-468">tableau de bord hello toouse vous avez tooconnect hello web application toohello compte de stockage que vous utilisez des en définissant la chaîne de connexion AzureWebJobsDashboard hello sur hello **configurer** onglet du portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="8e49c-468">toouse hello dashboard you have tooconnect hello web app toohello storage account you're using by setting hello AzureWebJobsDashboard connection string on hello **Configure** tab of hello classic portal.</span></span> <span data-ttu-id="8e49c-469">Ensuite, vous pouvez obtenir toohello du tableau de bord à l’aide de hello suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="8e49c-469">Then, you can get toohello Dashboard by using hello following URL:</span></span>

<span data-ttu-id="8e49c-470">https://{nom_d’application_web}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="8e49c-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="8e49c-471">Pour plus d’informations, consultez [mise en route d’un tableau de bord pour un développement local avec hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), mais notez qu’elle affiche un ancien nom de chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="8e49c-471">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="8e49c-472">Plus de documentation relative à WebJobs</span><span class="sxs-lookup"><span data-stu-id="8e49c-472">More WebJobs documentation</span></span>
<span data-ttu-id="8e49c-473">Pour plus d’informations, consultez [Ressources de documentation relatives à Azure WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="8e49c-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
