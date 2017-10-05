---
title: "Création d'une tâche web .NET dans Azure App Service | Microsoft Docs"
description: "Créez une application multiniveau avec ASP.NET MVC et Azure. Le serveur frontal s’exécute dans une application web d’Azure App Service, tandis que le serveur principal s’exécute en tant que tâche web. L’application utilise Entity Framework, la base de données SQL, ainsi que les files d’attente et objets blobs du stockage Azure."
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
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="6eadc-105">Créer une tâche web .NET dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6eadc-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="6eadc-106">Ce didacticiel montre comment écrire du code pour une simple application ASP.NET MVC 5 à plusieurs niveaux utilisant le [kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="6eadc-106">This tutorial shows how to write code for a simple multi-tier ASP.NET MVC 5 application that uses the [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="6eadc-107">L’objectif du [kit de développement logiciel (SDK) WebJobs](websites-webjobs-resources.md) consiste à simplifier le code que vous écrivez pour les tâches web courantes, telles que le traitement d’image, le traitement de la file d’attente, l’agrégation RSS, la maintenance des fichiers et l’envoi des messages électroniques.</span><span class="sxs-lookup"><span data-stu-id="6eadc-107">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="6eadc-108">Le kit de développement logiciel (SDK) WebJobs dispose de fonctionnalités intégrées fonctionnant avec le stockage Azure et Service Bus et servant à planifier des tâches, à gérer des erreurs et à nombreux autres scénarios courants.</span><span class="sxs-lookup"><span data-stu-id="6eadc-108">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="6eadc-109">En outre, il est évolutif et il existe un [référentiel open source contenant les extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="6eadc-109">In addition, it's designed to be extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="6eadc-110">L'exemple d'application concerne un panneau d'affichage publicitaire.</span><span class="sxs-lookup"><span data-stu-id="6eadc-110">The sample application is an advertising bulletin board.</span></span> <span data-ttu-id="6eadc-111">Les utilisateurs peuvent télécharger des images pour les annonces ; un processus principal convertit les images en miniatures.</span><span class="sxs-lookup"><span data-stu-id="6eadc-111">Users can upload images for ads, and a backend process converts the images to thumbnails.</span></span> <span data-ttu-id="6eadc-112">La page de liste des annonces affiche des miniatures et la page de détails des annonces affiche les images en taille réelle.</span><span class="sxs-lookup"><span data-stu-id="6eadc-112">The ad list page shows the thumbnails, and the ad details page shows the full-size image.</span></span> <span data-ttu-id="6eadc-113">Voici une capture d'écran :</span><span class="sxs-lookup"><span data-stu-id="6eadc-113">Here's a screenshot:</span></span>

![Ad list](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="6eadc-115">Cet exemple d’application fonctionne avec des [files d’attente Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) et [objets blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="6eadc-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="6eadc-116">Ce didacticiel montre comment déployer l’application sur [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) et sur la [base de données SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="6eadc-116">The tutorial shows how to deploy the application to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="6eadc-117"><a id="prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="6eadc-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="6eadc-118">Ce didacticiel suppose que vous savez utiliser les projets [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6eadc-118">The tutorial assumes that you know how to work with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="6eadc-119">Ce didacticiel a été rédigé à l’origine pour Visual Studio 2013, mais peut être utilisé avec des versions ultérieures de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6eadc-119">The tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="6eadc-120">Si vous utilisez Visual Studio 2015 ou 2017, notez qu’avant d’exécuter l’application localement, vous devez modifier la partie `Data Source` de la chaîne de connexion SQL Server LocalDB dans les fichiers Web.config et App.config de `Data Source=(localdb)\v11.0` à `Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="6eadc-120">If you are using Visual Studio 2015 or 2017, make note that before you run the application locally, you must change the `Data Source` part of the SQL Server LocalDB connection string in the Web.config and App.config files from `Data Source=(localdb)\v11.0` to `Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="6eadc-121"><a name="note"></a>Pour suivre ce didacticiel, vous avez besoin d’un compte Azure :</span><span class="sxs-lookup"><span data-stu-id="6eadc-121"><a name="note"></a>You must have an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="6eadc-122">Vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) : vous obtenez alors des crédits dont vous pouvez vous servir pour tester les services Azure payants et, même lorsqu’ils sont épuisés, vous pouvez conserver le compte et utiliser les services Azure gratuits, notamment Sites Web.</span><span class="sxs-lookup"><span data-stu-id="6eadc-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use to try out paid Azure services, and even after they're used up, you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="6eadc-123">Votre carte de crédit ne sera pas débitée tant que vous n'aurez pas explicitement modifié vos paramètres pour demander à l'être.</span><span class="sxs-lookup"><span data-stu-id="6eadc-123">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
> * <span data-ttu-id="6eadc-124">Vous pouvez [activer le crédit Azure mensuel pour Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) : votre abonnement vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.</span><span class="sxs-lookup"><span data-stu-id="6eadc-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="6eadc-125">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="6eadc-125">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6eadc-126">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="6eadc-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="6eadc-127"><a id="learn"></a>Contenu</span><span class="sxs-lookup"><span data-stu-id="6eadc-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="6eadc-128">Ce didacticiel explique comment effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="6eadc-128">The tutorial shows how to do the following tasks:</span></span>

* <span data-ttu-id="6eadc-129">Activer votre ordinateur pour le développement Azure en installant le Kit de développement logiciel (SDK) Azure (uniquement pour les utilisateurs de Visual Studio 2013 et 2015).</span><span class="sxs-lookup"><span data-stu-id="6eadc-129">Enable your machine for Azure development by installing the Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="6eadc-130">création du projet d'application console qui se déploie automatiquement comme une tâche web Azure lorsque vous déployez le projet web associé ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy the associated web project.</span></span>
* <span data-ttu-id="6eadc-131">test d'un serveur principal de Kit de développement logiciel (SDK) WebJobs localement sur l'ordinateur de développement ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-131">Test a WebJobs SDK backend locally on the development computer.</span></span>
* <span data-ttu-id="6eadc-132">publication d’une application avec un serveur principal de tâches web dans une application web d’App Service ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-132">Publish an application with a WebJobs backend to a web app in App Service.</span></span>
* <span data-ttu-id="6eadc-133">téléchargement et enregistrement de fichiers dans le service Blob Azure ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-133">Upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="6eadc-134">utilisation du Kit de développement logiciel (SDK) Azure WebJobs avec des files d'attente et des objets blob Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-134">Use the Azure WebJobs SDK to work with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="6eadc-135"><a id="contosoads"></a>Architecture de l’application</span><span class="sxs-lookup"><span data-stu-id="6eadc-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="6eadc-136">L'exemple d'application utilise le [modèle de travail centré sur les files d'attente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) pour décharger le travail de création de vignettes exigeant en ressources vers un processus principal.</span><span class="sxs-lookup"><span data-stu-id="6eadc-136">The sample application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a backend process.</span></span>

<span data-ttu-id="6eadc-137">L'application stocke les publicités dans une base de données SQL et utilise Entity Framework Code First pour créer les tables et accéder aux données.</span><span class="sxs-lookup"><span data-stu-id="6eadc-137">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="6eadc-138">Pour chaque publicité, la base de données stocke deux URL, une pour l’image à taille réelle et l’autre pour la miniature.</span><span class="sxs-lookup"><span data-stu-id="6eadc-138">For each ad, the database stores two URLs: one for the full-size image and one for the thumbnail.</span></span>

![Ad table](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="6eadc-140">Lorsqu’un utilisateur charge une image, l’application web la stocke dans un [objet blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)et stocke les informations publicitaires dans la base de données avec une URL pointant vers l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6eadc-140">When a user uploads an image, the web app stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="6eadc-141">En même temps, il écrit un message dans une file d'attente Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-141">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="6eadc-142">Dans un processus principal s’exécutant en tant qu’Azure WebJob, le Kit de développement logiciel (SDK) WebJobs interroge la file d’attente sur la présence de nouveaux messages.</span><span class="sxs-lookup"><span data-stu-id="6eadc-142">In a backend process running as an Azure WebJob, the WebJobs SDK polls the queue for new messages.</span></span> <span data-ttu-id="6eadc-143">Lorsqu'un nouveau message arrive, la tâche web crée une vignette pour cette image et met à jour le champ de la base de données des URL des vignettes pour cette publicité.</span><span class="sxs-lookup"><span data-stu-id="6eadc-143">When a new message appears, the WebJob creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="6eadc-144">Le schéma suivant montre l'interaction des parties de l'application :</span><span class="sxs-lookup"><span data-stu-id="6eadc-144">Here's a diagram that shows how the parts of the application interact:</span></span>

![Contoso Ads architecture](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="6eadc-146">Les instructions du didacticiel s’appliquent au Kit de développement logiciel (SDK) Azure pour .NET 2.7.1 ou pour une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-146">The tutorial instructions apply to Azure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="6eadc-147"><a id="storage"></a>Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="6eadc-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="6eadc-148">Un compte de stockage Azure fournit des ressources pour stocker les données de file d'attente et d'objet blob dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="6eadc-148">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span> <span data-ttu-id="6eadc-149">Le Kit de développement logiciel (SDK) WebJobs l'utilise également pour enregistrer les données de journalisation du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="6eadc-149">It's also used by the WebJobs SDK to store logging data for the dashboard.</span></span>

<span data-ttu-id="6eadc-150">Dans une application réelle, vous créez généralement des comptes distincts pour les données d’application et de journalisation, et des comptes distincts pour les données de test et de production.</span><span class="sxs-lookup"><span data-stu-id="6eadc-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="6eadc-151">Pour ce didacticiel, vous allez utiliser un seul compte.</span><span class="sxs-lookup"><span data-stu-id="6eadc-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="6eadc-152">Ouvrez la fenêtre **Explorateur de serveurs** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6eadc-152">Open the **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="6eadc-153">Cliquez avec le bouton droit sur le nœud **Azure**, puis cliquez sur **Se connecter à un abonnement Microsoft Azure...**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-153">Right-click the **Azure** node, and then click **Connect to Microsoft Azure Subscription...**.</span></span>
   
   ![Connexion à Azure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="6eadc-155">Connectez-vous à l'aide de vos informations d'identification Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="6eadc-156">Cliquez avec le bouton droit sur **Stockage** sous le nœud Azure, puis cliquez sur **Créer un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-156">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Créer un compte de stockage](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="6eadc-158">Dans la boîte de dialogue **Créer un compte de stockage** , entrez un nom correspondant au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-158">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="6eadc-159">Le nom doit être unique (aucun autre compte de stockage Azure ne doit avoir le même nom).</span><span class="sxs-lookup"><span data-stu-id="6eadc-159">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="6eadc-160">Si le nom que vous entrez est déjà utilisé, vous aurez la possibilité de le modifier.</span><span class="sxs-lookup"><span data-stu-id="6eadc-160">If the name you enter is already in use, you'll get a chance to change it.</span></span>

    <span data-ttu-id="6eadc-161">L’URL permettant d’accéder à votre compte de stockage est *{nom}*.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="6eadc-161">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="6eadc-162">Choisissez la région la proche de vous dans la liste déroulante **Région ou groupe d’affinités** .</span><span class="sxs-lookup"><span data-stu-id="6eadc-162">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="6eadc-163">Ce paramètre spécifie le centre de données Azure qui hébergera votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="6eadc-164">Pour ce didacticiel, votre choix ne fera pas une grande différence.</span><span class="sxs-lookup"><span data-stu-id="6eadc-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="6eadc-165">Toutefois, dans le cas d’une application web de production, vous souhaitez que votre serveur web et votre compte de stockage soient situés dans la même région afin de minimiser la latence et les frais d’acheminement des données.</span><span class="sxs-lookup"><span data-stu-id="6eadc-165">However, for a production web app, you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="6eadc-166">Le centre de données de l’application web (que vous créerez par la suite) doit être aussi proche que possible des navigateurs qui accèdent à l’application afin de réduire la latence.</span><span class="sxs-lookup"><span data-stu-id="6eadc-166">The web app (which you'll create later) datacenter should be as close as possible to the browsers accessing the web app in order to minimize latency.</span></span>
7. <span data-ttu-id="6eadc-167">Dans la liste déroulante **Réplication**, sélectionnez **Redondant en local**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-167">Set the **Replication** drop-down list to **Locally redundant**.</span></span>

    <span data-ttu-id="6eadc-168">Lorsque la géo-réplication est activée pour un compte de stockage, le contenu stocké est répliqué dans un centre de données secondaire pour activer le basculement vers cet emplacement en cas de sinistre majeur à l'emplacement principal.</span><span class="sxs-lookup"><span data-stu-id="6eadc-168">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="6eadc-169">La géo-réplication peut engendrer des coûts supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6eadc-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="6eadc-170">Dans le cas des comptes test et de développement, vous êtes en général peu enclin à payer pour la géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="6eadc-170">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="6eadc-171">Pour plus d’informations, consultez [Création, gestion ou suppression d’un compte de stockage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6eadc-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="6eadc-172">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-172">Click **Create**.</span></span>

    ![New storage account](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="6eadc-174"><a id="download"></a>Télécharger l’application</span><span class="sxs-lookup"><span data-stu-id="6eadc-174"><a id="download"></a>Download the application</span></span>
1. <span data-ttu-id="6eadc-175">Téléchargez et décompressez la [solution terminée](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="6eadc-175">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="6eadc-176">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6eadc-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="6eadc-177">Dans le menu **Fichier**, sélectionnez **Ouvrir > Projet/Solution**, accédez à l’emplacement où vous avez téléchargé la solution, puis ouvrez le fichier de la solution.</span><span class="sxs-lookup"><span data-stu-id="6eadc-177">From the **File** menu choose **Open > Project/Solution**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="6eadc-178">Appuyez sur Ctrl+Maj+B pour générer la solution.</span><span class="sxs-lookup"><span data-stu-id="6eadc-178">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="6eadc-179">Par défaut, Visual Studio restaure automatiquement le contenu du package NuGet, qui n'était pas inclus dans le fichier *.zip* .</span><span class="sxs-lookup"><span data-stu-id="6eadc-179">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="6eadc-180">Si les packages ne sont pas restaurés, installez-les manuellement en ouvrant la boîte de dialogue **Gérer les packages NuGet pour la solution** et en cliquant sur le bouton **Restaurer** en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="6eadc-180">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="6eadc-181">Dans l'**Explorateur de solutions**, vérifiez que **ContosoAdsWeb** est sélectionné comme projet de démarrage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as the startup project.</span></span>

## <span data-ttu-id="6eadc-182"><a id="configurestorage"></a>Configurer l’application pour utiliser votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="6eadc-182"><a id="configurestorage"></a>Configure the application to use your storage account</span></span>
1. <span data-ttu-id="6eadc-183">Ouvrez le fichier d'application *Web.config* dans le projet ContosoAdsWeb.</span><span class="sxs-lookup"><span data-stu-id="6eadc-183">Open the application *Web.config* file in the ContosoAdsWeb project.</span></span>

    <span data-ttu-id="6eadc-184">Ce fichier contient des chaînes de connexion SQL et de stockage Azure pour utiliser des objets blob et des files d'attente.</span><span class="sxs-lookup"><span data-stu-id="6eadc-184">The file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="6eadc-185">La chaîne de connexion SQL pointe vers une base de données [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6eadc-185">The SQL connection string points to a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="6eadc-186">La chaîne de connexion de stockage est un exemple qui comporte des espaces réservés pour la clé d’accès et le nom du compte stockage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-186">The storage connection string is an example that has placeholders for the storage account name and access key.</span></span> <span data-ttu-id="6eadc-187">Vous allez le remplacer par une chaîne de connexion qui a le nom et la clé de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-187">You'll replace this with a connection string that has the name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="6eadc-188">La chaîne de connexion de stockage est nommée AzureWebJobsStorage, car il s'agit du nom que le Kit de développement logiciel (SDK) WebJobs utilise par défaut.</span><span class="sxs-lookup"><span data-stu-id="6eadc-188">The storage connection string is named AzureWebJobsStorage because that's the name the WebJobs SDK uses by default.</span></span> <span data-ttu-id="6eadc-189">Nous utilisons ce nom ici pour qu’il ne vous reste plus qu’à définir une seule valeur de chaîne de connexion dans l’environnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-189">The same name is used here so you have to set only one connection string value in the Azure environment.</span></span>
2. <span data-ttu-id="6eadc-190">Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur votre compte de stockage sous le nœud **Stockage**, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-190">In **Server Explorer**, right-click your storage account under the **Storage** node, and then click **Properties**.</span></span>

    ![Click Storage Account Properties](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="6eadc-192">Dans la fenêtre **Propriétés**, cliquez sur **Clés de compte de stockage**, puis cliquez sur le bouton de sélection.</span><span class="sxs-lookup"><span data-stu-id="6eadc-192">In the **Properties** window, click **Storage Account Keys**, and then click the ellipsis.</span></span>

    ![Clés de compte de stockage](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="6eadc-194">Copiez la **chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-194">Copy the **Connection String**.</span></span>

    ![Storage Account Keys dialog](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="6eadc-196">Remplacez la chaîne de connexion de stockage dans le fichier *Web.config* par celle que vous venez de copier.</span><span class="sxs-lookup"><span data-stu-id="6eadc-196">Replace the storage connection string in the *Web.config* file with the connection string you just copied.</span></span> <span data-ttu-id="6eadc-197">Veillez à sélectionner tout ce qui se trouve entre les guillemets, mais sans inclure les guillemets, avant le collage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-197">Make sure you select everything inside the quotation marks but not including the quotation marks before pasting.</span></span>
6. <span data-ttu-id="6eadc-198">Ouvrez le fichier *App.config* dans le projet ContosoAdsWebJob.</span><span class="sxs-lookup"><span data-stu-id="6eadc-198">Open the *App.config* file in the ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="6eadc-199">Ce fichier comporte deux chaînes de connexion : une pour les données de l'application et une pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="6eadc-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="6eadc-200">Vous pouvez utiliser des comptes de stockage distincts pour les données et la journalisation de l’application, ainsi qu’utiliser [plusieurs comptes de stockage pour les données](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="6eadc-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="6eadc-201">Pour ce didacticiel, vous allez utiliser un seul compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="6eadc-202">Les chaînes de connexion comportent des espaces réservés pour les clés de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-202">The connection strings have placeholders for the storage account keys.</span></span>

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

    <span data-ttu-id="6eadc-203">Par défaut, le Kit de développement logiciel (SDK) WebJobs recherche les chaînes de connexion AzureWebJobsStorage et AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="6eadc-203">By default, the WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="6eadc-204">Vous pouvez également [stocker la chaîne de connexion comme vous le souhaitez et la transmettre explicitement à l’objet `JobHost`](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="6eadc-204">As an alternative, you can [store the connection string however you want and pass it in explicitly to the `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="6eadc-205">Remplacez les chaînes de connexion de stockage par la chaîne de connexion que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="6eadc-205">Replace both storage connection strings with the connection string you copied earlier.</span></span>
8. <span data-ttu-id="6eadc-206">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="6eadc-206">Save your changes.</span></span>

## <span data-ttu-id="6eadc-207"><a id="run"></a>Exécuter l’application localement</span><span class="sxs-lookup"><span data-stu-id="6eadc-207"><a id="run"></a>Run the application locally</span></span>
1. <span data-ttu-id="6eadc-208">Pour démarrer le programme web frontal de l'application, appuyez sur Ctrl+F5.</span><span class="sxs-lookup"><span data-stu-id="6eadc-208">To start the web frontend of the application, press CTRL+F5.</span></span>

    <span data-ttu-id="6eadc-209">Le navigateur par défaut ouvre la page d'accueil.</span><span class="sxs-lookup"><span data-stu-id="6eadc-209">The default browser opens to the home page.</span></span> <span data-ttu-id="6eadc-210">Le projet web s'exécute, car vous l'avez défini comme projet de démarrage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-210">(The web project runs because you've made it the startup project.)</span></span>

    ![Contoso Ads home page](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="6eadc-212">Pour démarrer la tâche web principale de l'application, cliquez avec le bouton droit sur le projet ContosoAdsWebJob dans l'**Explorateur de solutions**, puis sur **Débogage** > **Démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-212">To start the WebJob backend of the application, right-click the ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="6eadc-213">Une fenêtre d'application console s'ouvre et affiche des messages de journalisation indiquant que l'objet JobHost du Kit de développement logiciel (SDK) WebJobs a commencé à s'exécuter.</span><span class="sxs-lookup"><span data-stu-id="6eadc-213">A console application window opens and displays logging messages indicating the WebJobs SDK JobHost object has started to run.</span></span>

    ![Console application window showing that the backend is running](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="6eadc-215">Dans votre navigateur, cliquez sur **Créer une publicité**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="6eadc-216">Entrez des données de test, sélectionnez une image à télécharger, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-216">Enter some test data, select an image to upload, and then click **Create**.</span></span>

    ![Create page](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="6eadc-218">L'application ouvre la page Index, mais n'affiche pas de vignette pour la nouvelle publicité, car le processus n'a pas encore eu lieu.</span><span class="sxs-lookup"><span data-stu-id="6eadc-218">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="6eadc-219">Entre-temps, après une brève attente, un message dans la fenêtre d'application console indique qu'un message en file d'attente a été reçu et traité.</span><span class="sxs-lookup"><span data-stu-id="6eadc-219">Meanwhile, after a short wait a logging message in the console application window shows that a queue message was received and has been processed.</span></span>

    ![Console application window showing that a queue message has been processed](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="6eadc-221">Lorsque ces messages s'affichent dans la fenêtre d'application console, actualisez la page Index pour afficher la vignette.</span><span class="sxs-lookup"><span data-stu-id="6eadc-221">After you see the logging messages in the console application window, refresh the Index page to see the thumbnail.</span></span>

    ![Page d'index](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="6eadc-223">Cliquez sur l'option **Détails** de votre publicité pour afficher l'image intégrale.</span><span class="sxs-lookup"><span data-stu-id="6eadc-223">Click **Details** for your ad to see the full-size image.</span></span>

    ![Details page](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="6eadc-225">Vous avez exécuté l'application sur votre ordinateur local. Elle utilise une base de données SQL Server sur votre ordinateur, mais travaille sur des files d'attente et des objets blob dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="6eadc-225">You've been running the application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in the cloud.</span></span> <span data-ttu-id="6eadc-226">Dans la section suivante, vous allez exécuter l'application dans le cloud en utilisant une base de données du cloud ainsi que des objets blob et des files d'attente du cloud.</span><span class="sxs-lookup"><span data-stu-id="6eadc-226">In the following section you'll run the application in the cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="6eadc-227"><a id="runincloud"></a>Exécuter l’application dans le cloud</span><span class="sxs-lookup"><span data-stu-id="6eadc-227"><a id="runincloud"></a>Run the application in the cloud</span></span>
<span data-ttu-id="6eadc-228">Pour exécuter l'application dans le cloud, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6eadc-228">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="6eadc-229">Procédez au déploiement dans Web Apps.</span><span class="sxs-lookup"><span data-stu-id="6eadc-229">Deploy to Web Apps.</span></span> <span data-ttu-id="6eadc-230">Visual Studio crée automatiquement une application web dans App Service et une instance Base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="6eadc-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="6eadc-231">Configurez l’application pour l’utilisation de votre base de données SQL et de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-231">Configure the web app to use your Azure SQL database and storage account.</span></span>

<span data-ttu-id="6eadc-232">Après avoir créé quelques publicités dans le cloud, vous afficherez le tableau de bord du Kit de développement logiciel (SDK) WebJobs pour voir les fonctions de surveillance enrichies qu'il offre.</span><span class="sxs-lookup"><span data-stu-id="6eadc-232">After you've created some ads while running in the cloud, you'll view the WebJobs SDK dashboard to see the rich monitoring features it has to offer.</span></span>

### <a name="deploy-to-web-apps"></a><span data-ttu-id="6eadc-233">Déployer dans Web Apps</span><span class="sxs-lookup"><span data-stu-id="6eadc-233">Deploy to Web Apps</span></span>

1. <span data-ttu-id="6eadc-234">Fermez le navigateur et la fenêtre d'application console.</span><span class="sxs-lookup"><span data-stu-id="6eadc-234">Close the browser and the console application window.</span></span>
2. <span data-ttu-id="6eadc-235">Suivez les étapes de la section [Publier sur Azure avec SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="6eadc-235">Follow the steps in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="6eadc-236">Une fois les étapes de déploiement accomplies, effectuez les tâches restantes décrites dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6eadc-236">After you complete the steps for deploying, continue with the remaining tasks in this article.</span></span>

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="6eadc-237">Configurer l’application pour l’utilisation de votre base de données SQL et de votre compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="6eadc-237">Configure the web app to use your Azure SQL database and storage account</span></span>
<span data-ttu-id="6eadc-238">Par sécurité, il est conseillé [d'éviter de placer des informations sensibles (par exemple, des chaînes de connexion) dans des fichiers stockés dans des référentiels de code source](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="6eadc-238">It's a security best practice to [avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="6eadc-239">Vous pouvez définir une chaîne de connexion et d’autres paramètres dans l’environnement Azure. Les API de configuration ASP.NET sélectionnent automatiquement ces valeurs quand l’application s’exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-239">Azure provides a way to do that: you can set connection string and other setting values in the Azure environment, and ASP.NET configuration APIs automatically pick up these values when the app runs in Azure.</span></span> <span data-ttu-id="6eadc-240">Vous pouvez définir ces valeurs dans Azure à l’aide de l’**Explorateur de serveurs**, du portail Azure, de Windows PowerShell ou de l’interface de ligne de commande interplateforme.</span><span class="sxs-lookup"><span data-stu-id="6eadc-240">You can set these values in Azure by using **Server Explorer**, the Azure Portal, Windows PowerShell, or the cross-platform command-line interface.</span></span> <span data-ttu-id="6eadc-241">Pour plus d’informations, consultez [Fonctionnement des chaînes d’application et des chaînes de connexion](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="6eadc-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="6eadc-242">Dans cette section, vous utilisez l’ **Explorateur de serveurs** pour définir des valeurs de chaînes de connexion dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-242">In this section, you use **Server Explorer** to set connection string values in Azure.</span></span>

1. <span data-ttu-id="6eadc-243">Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur votre application web sous **Azure > App Service {votre groupe de ressources}**, puis cliquez sur **Afficher les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="6eadc-244">La fenêtre **Application web Azure** s’ouvre dans l’onglet **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-244">The **Azure Web App** window opens on the **Configuration** tab.</span></span>
2. <span data-ttu-id="6eadc-245">Modifiez le nom de la chaîne de connexion par défaut en le remplaçant par le nom que vous avez choisi lors de la configuration de la base de données SQL dans le cadre de l’article [Publier sur Azure avec SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="6eadc-245">Change the name of the DefaultConnection connection string to the name you chose when you configured the SQL database in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="6eadc-246">Azure a automatiquement créé cette chaîne de connexion lorsque vous avez créé l’application web avec une base de données associée ; il présente donc déjà la valeur de chaîne de connexion adéquate.</span><span class="sxs-lookup"><span data-stu-id="6eadc-246">Azure automatically created this connection string when you created the web app with an associated database, so it already has the right connection string value.</span></span> <span data-ttu-id="6eadc-247">Vous remplacez simplement le nom par celui que votre code recherche.</span><span class="sxs-lookup"><span data-stu-id="6eadc-247">You're changing just the name to what your code is looking for.</span></span>
3. <span data-ttu-id="6eadc-248">Ajoutez deux chaînes de connexion nommées AzureWebJobsStorage et AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="6eadc-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="6eadc-249">Définissez le type de base de données sur **Personnalisé** et définissez la valeur de la chaîne de connexion sur la valeur que vous avez utilisée auparavant pour les fichiers *Web.config* et *App.config*.</span><span class="sxs-lookup"><span data-stu-id="6eadc-249">Set the database type to **Custom**, and set the connection string value to the same value that you used earlier for the *Web.config* and *App.config* files.</span></span> <span data-ttu-id="6eadc-250">Veillez à inclure la chaîne de connexion complète, pas uniquement la clé d’accès, ainsi qu’à ne pas inclure les guillemets.</span><span class="sxs-lookup"><span data-stu-id="6eadc-250">(Be sure you include the entire connection string, not just the access key, and don't include the quotation marks.)</span></span>

    <span data-ttu-id="6eadc-251">Le Kit de développement logiciel (SDK) WebJobs utilise ces chaînes de connexion : une pour les données de l'application et une pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="6eadc-251">These connection strings are used by the WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="6eadc-252">Comme nous l’avons vu précédemment, le code du programme web frontal utilise aussi la chaîne pour les données de l’application.</span><span class="sxs-lookup"><span data-stu-id="6eadc-252">As you saw earlier, the one for application data is also used by the web front-end code.</span></span>
4. <span data-ttu-id="6eadc-253">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-253">Click **Save**.</span></span>

    ![Chaînes de connexion dans le portail Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="6eadc-255">Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur l’application web, puis cliquez sur **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-255">In **Server Explorer**, right-click the web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="6eadc-256">Une fois l’application web arrêtée, cliquez de nouveau sur cette dernière avec le bouton droit, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-256">After the web app stops, right-click the web app again, and then click **Start**.</span></span>

   <span data-ttu-id="6eadc-257">La tâche web démarre automatiquement lorsque vous publiez, mais elle s'arrête lorsque vous modifiez la configuration.</span><span class="sxs-lookup"><span data-stu-id="6eadc-257">The WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="6eadc-258">Pour la redémarrer, vous pouvez soit redémarrer l’application web, soit redémarrer la tâche web dans le [portail Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="6eadc-258">To restart it, you can either restart the web app or restart the WebJob in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="6eadc-259">Il est généralement recommandé de redémarrer l’application web après une modification de la configuration.</span><span class="sxs-lookup"><span data-stu-id="6eadc-259">It's generally recommended to restart the web app after a configuration change.</span></span>
7. <span data-ttu-id="6eadc-260">Actualisez la fenêtre du navigateur contenant l’URL de l’application web dans sa barre d’adresse.</span><span class="sxs-lookup"><span data-stu-id="6eadc-260">Refresh the browser window that has the web app URL in its address bar.</span></span>

    <span data-ttu-id="6eadc-261">La page d'accueil s'affiche.</span><span class="sxs-lookup"><span data-stu-id="6eadc-261">The home page appears.</span></span>
8. <span data-ttu-id="6eadc-262">Créez une publicité comme vous l’avez fait lorsque vous avez [exécuté l’application localement](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="6eadc-262">Create an ad, as you did when you [ran the application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="6eadc-263">La page Index s'affiche d'abord sans vignette.</span><span class="sxs-lookup"><span data-stu-id="6eadc-263">The Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="6eadc-264">Actualisez la page après quelques secondes. La miniature s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6eadc-264">Refresh the page after a few seconds and the thumbnail appears.</span></span>

   <span data-ttu-id="6eadc-265">Si elle n’apparaît pas, il se peut que vous deviez patienter environ une minute pour que la tâche web redémarre.</span><span class="sxs-lookup"><span data-stu-id="6eadc-265">If the thumbnail doesn't appear, you might have to wait a minute or so for the WebJob to restart.</span></span> <span data-ttu-id="6eadc-266">Si, après un certain temps, vous ne voyez toujours pas la miniature lorsque vous actualisez la page, il se peut que la tâche web n’ait pas démarré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="6eadc-266">If after a while, you still don't see the thumbnail when you refresh the page, the WebJob might not have started automatically.</span></span> <span data-ttu-id="6eadc-267">Dans ce cas, accédez au panneau **App Services** dans le [portail Azure](https://portal.azure.com/), localisez votre application web, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-267">In that case, go to the **App Services** blade in the [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-the-webjobs-sdk-dashboard"></a><span data-ttu-id="6eadc-268">Affichage du tableau de bord du Kit de développement logiciel (SDK) WebJobs</span><span class="sxs-lookup"><span data-stu-id="6eadc-268">View the WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="6eadc-269">Dans le [portail Azure](https://portal.azure.com/), sélectionnez le panneau **App Services**, localisez votre application web, puis sélectionnez **Tâches web**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-269">In the [Azure portal](https://portal.azure.com/), select the **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="6eadc-270">Sélectionnez l’onglet **Journaux**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-270">Select the **Logs** tab.</span></span>

    ![Onglet journaux](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="6eadc-272">Un nouvel onglet ouvre le tableau de bord du Kit de développement logiciel (SDK) WebJobs dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="6eadc-272">A new browser tab opens to the WebJobs SDK dashboard.</span></span> <span data-ttu-id="6eadc-273">Le tableau de bord indique que la tâche web est en cours d'exécution et affiche la liste des fonctions de votre code que le SDK a déclenchées.</span><span class="sxs-lookup"><span data-stu-id="6eadc-273">The dashboard shows that the WebJob is running and shows a list of functions in your code that the WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="6eadc-274">Cliquez sur une des fonctions pour afficher des informations sur son exécution.</span><span class="sxs-lookup"><span data-stu-id="6eadc-274">Click one of the functions to see details about its execution.</span></span>

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="6eadc-277">Le bouton **Rappeler la fonction** de cette page commande à l'infrastructure du SDK de rappeler la fonction et vous permet de modifier les données déjà transmises à la fonction.</span><span class="sxs-lookup"><span data-stu-id="6eadc-277">The **Replay Function** button on this page causes the WebJobs SDK framework to call the function again, and it gives you a chance to change the data passed to the function first.</span></span>

> [!NOTE]
> <span data-ttu-id="6eadc-278">Lorsque vous avez fini de tester, songez à supprimer l’application web, le compte de stockage et votre instance SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6eadc-278">When you're finished testing, consider deleting the web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="6eadc-279">L’application web est gratuite, mais le compte de stockage et l’instance de base de données SQL augmentent les frais (quoique minimaux du fait de la petite taille).</span><span class="sxs-lookup"><span data-stu-id="6eadc-279">The web app is free, but the SQL storage account and database instance accrue charges (albeit, minimal due to the small size).</span></span> <span data-ttu-id="6eadc-280">De même, si vous laissez l’application web s’exécuter, toute personne trouvant votre URL peut créer et afficher des publicités.</span><span class="sxs-lookup"><span data-stu-id="6eadc-280">Also, if you leave the web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="6eadc-281">Supprimer votre application web</span><span class="sxs-lookup"><span data-stu-id="6eadc-281">Delete your web app</span></span>
<span data-ttu-id="6eadc-282">Dans le portail, accédez au panneau **App Services**, recherchez et sélectionnez votre application web, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-282">In the portal, go to the **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="6eadc-283">Si vous souhaitez empêcher temporairement l’accès à l’application web, cliquez plutôt sur **Arrêter** .</span><span class="sxs-lookup"><span data-stu-id="6eadc-283">If you just want to temporarily prevent others from accessing the web app, click **Stop** instead.</span></span> <span data-ttu-id="6eadc-284">Dans ce cas, les frais continuent à s'accumuler pour la base de données SQL et le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-284">In that case, charges will continue to accrue for the SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="6eadc-285">Supprimer votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="6eadc-285">Delete your storage account</span></span>
<span data-ttu-id="6eadc-286">Pour supprimer votre compte de stockage, voir [Supprimer un compte de stockage](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="6eadc-286">To delete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="6eadc-287">Supprimer de votre base de données</span><span class="sxs-lookup"><span data-stu-id="6eadc-287">Delete your database</span></span>
<span data-ttu-id="6eadc-288">Pour supprimer votre base de données SQL, voir la documentation de l’[API REST Azure SQL Database](https://docs.microsoft.com/rest/api/sql/).</span><span class="sxs-lookup"><span data-stu-id="6eadc-288">To delete your SQL database, see the [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="6eadc-289"><a id="create"></a>Créer l’application intégralement</span><span class="sxs-lookup"><span data-stu-id="6eadc-289"><a id="create"></a>Create the application from scratch</span></span>
<span data-ttu-id="6eadc-290">Dans cette section, vous effectuerez les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="6eadc-290">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="6eadc-291">création d'une solution Visual Studio avec un projet web ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="6eadc-292">ajout d’un projet de bibliothèque de classes pour la couche d’accès aux données partagée par le programme frontal et le programme principal ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-292">Add a class library project for the data access layer that is shared between the front end and back end.</span></span>
* <span data-ttu-id="6eadc-293">ajout d'un projet d'application console pour le programme principal, le déploiement de tâches web étant activé ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-293">Add a Console Application project for the backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="6eadc-294">ajout de packages NuGet ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-294">Add NuGet packages.</span></span>
* <span data-ttu-id="6eadc-295">définition des références d'un projet ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-295">Set project references.</span></span>
* <span data-ttu-id="6eadc-296">copie des fichiers de code et de configuration de l'application téléchargée que vous avez utilisée dans la section précédente de ce didacticiel ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-296">Copy application code and configuration files from the downloaded application that you worked with in the previous section of the tutorial.</span></span>
* <span data-ttu-id="6eadc-297">examen des parties du code qui fonctionnent avec les objets blob, les files d'attente et le Kit de développement logiciel (SDK) WebJobs Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-297">Review the parts of the code that work with Azure blobs and queues and the WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="6eadc-298">Création d'une solution Visual Studio avec un projet web et un projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="6eadc-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="6eadc-299">Dans Visual Studio, choisissez **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="6eadc-300">Dans la boîte de dialogue **Nouveau projet**, choisissez **Visual C#** > **Web** > **Application web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-300">In the **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="6eadc-301">Nommez le projet ContosoAdsWeb, la solution ContosoAdsWebJobsSDK (modifiez le nom de la solution si vous la placez dans le même dossier que la solution téléchargée) et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-301">Name the project ContosoAdsWeb, name the solution ContosoAdsWebJobsSDK (change the solution name if you're putting it in the same folder as the downloaded solution), and then click **OK**.</span></span>

    ![Nouveau projet](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="6eadc-303">Dans la boîte de dialogue **Nouvelle application web ASP.NET**, choisissez le modèle MVC, puis sélectionnez **Modifier l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-303">In the **New ASP.NET Web Application** dialog, choose the MVC template, and select **Change Authentication**.</span></span>

    ![Modifier l'authentification](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="6eadc-305">Dans la boîte de dialogue **Modifier l'authentification**, choisissez **Aucune authentification** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-305">In the **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Aucune authentification](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="6eadc-307">Dans la boîte de dialogue **Nouvelle application web ASP.NET**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-307">In the **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="6eadc-308">Visual Studio crée la solution et le projet web.</span><span class="sxs-lookup"><span data-stu-id="6eadc-308">Visual Studio creates the solution and the web project.</span></span>
7. <span data-ttu-id="6eadc-309">Dans l'**Explorateur de solutions**, cliquez avec le bouton droit sur la solution (et non sur le projet) et choisissez **Ajouter** > **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-309">In **Solution Explorer**, right-click the solution (not the project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="6eadc-310">Dans la boîte de dialogue **Ajouter un nouveau projet**, choisissez le modèle **Visual C#** > **Bureau classique Windows** > **Bibliothèque de classes (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-310">In the **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="6eadc-311">Nommez le projet *ContosoAdsCommon*, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-311">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="6eadc-312">Ce projet contient le contexte Entity Framework et le modèle de données que le programme frontal et le programme principal vont utiliser.</span><span class="sxs-lookup"><span data-stu-id="6eadc-312">This project will contain the Entity Framework context and the data model which both the front end and back end will use.</span></span> <span data-ttu-id="6eadc-313">Vous pouvez également définir les classes associées à Entity Framework dans le projet web et faire référence à ce projet de tâche web.</span><span class="sxs-lookup"><span data-stu-id="6eadc-313">As an alternative, you could define the EF-related classes in the web project and reference that project from the WebJob project.</span></span> <span data-ttu-id="6eadc-314">Mais dans ce cas, ce dernier aura une référence inutile aux assemblys web.</span><span class="sxs-lookup"><span data-stu-id="6eadc-314">But, then your WebJob project would have a reference to web assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="6eadc-315">Ajout d'un projet d'application console dont le déploiement de tâches web est activé</span><span class="sxs-lookup"><span data-stu-id="6eadc-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="6eadc-316">Cliquez avec le bouton droit sur le projet web (et non sur la solution ou le projet de bibliothèque de classes), puis cliquez sur **Ajouter** > **Nouveau projet de tâche web Azure**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-316">Right-click the web project (not the solution or the class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![New Azure WebJob Project menu selection](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="6eadc-318">Dans la boîte de dialogue **Ajouter une tâche web Azure**, entrez ContosoAdsWebJob pour le **Nom du projet** et le **Nom de la tâche web**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-318">In the **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both the **Project name** and the **WebJob name**.</span></span> <span data-ttu-id="6eadc-319">Laissez **Mode d'exécution de la tâche web** sur **Exécuter en continu**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-319">Leave **WebJob run mode** set to **Run Continuously**.</span></span>
3. <span data-ttu-id="6eadc-320">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-320">Click **OK**.</span></span>

   <span data-ttu-id="6eadc-321">Visual Studio crée une application console configurée pour se déployer comme une tâche web lorsque vous déployez le projet web.</span><span class="sxs-lookup"><span data-stu-id="6eadc-321">Visual Studio creates a Console application that is configured to deploy as a WebJob whenever you deploy the web project.</span></span> <span data-ttu-id="6eadc-322">Pour cela, il a effectué les tâches suivantes après la création du projet :</span><span class="sxs-lookup"><span data-stu-id="6eadc-322">To do that, it performed the following tasks after creating the project:</span></span>

   * <span data-ttu-id="6eadc-323">ajout d'un fichier *webjob-publish-settings.json* dans le dossier des propriétés du projet de tâche web ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-323">Added a *webjob-publish-settings.json* file in the WebJob project Properties folder.</span></span>
   * <span data-ttu-id="6eadc-324">ajout d'un fichier *webjobs-list.json* dans le dossier des propriétés du projet web ;</span><span class="sxs-lookup"><span data-stu-id="6eadc-324">Added a *webjobs-list.json* file in the web project Properties folder.</span></span>
   * <span data-ttu-id="6eadc-325">installation du package NuGet Microsoft.Web.WebJobs.Publish dans le projet de tâche web.</span><span class="sxs-lookup"><span data-stu-id="6eadc-325">Installed the Microsoft.Web.WebJobs.Publish NuGet package in the WebJob project.</span></span>

   <span data-ttu-id="6eadc-326">Pour plus d’informations sur ces modifications, consultez la rubrique [Déployer des tâches web à l’aide de Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="6eadc-326">For more information about these changes, see [How to deploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="6eadc-327">Ajout de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="6eadc-327">Add NuGet packages</span></span>
<span data-ttu-id="6eadc-328">Le nouveau modèle de projet pour un projet de tâche web installe automatiquement le package NuGet [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) du Kit de développement logiciel (SDK) WebJobs et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="6eadc-328">The new-project template for a WebJob project automatically installs the WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="6eadc-329">L’une des dépendances du Kit de développement logiciel WebJobs installée automatiquement dans le projet WebJob est la bibliothèque cliente de stockage Azure (SCL, Storage Client Library).</span><span class="sxs-lookup"><span data-stu-id="6eadc-329">One of the WebJobs SDK dependencies that is installed automatically in the WebJob project is the Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="6eadc-330">Toutefois, vous devez l’ajouter au projet web pour qu’elle fonctionne avec les objets blob et les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="6eadc-330">However, you need to add it to the web project to work with blobs and queues.</span></span>

1. <span data-ttu-id="6eadc-331">Ouvrez la boîte de dialogue **Gérer les packages NuGet** pour la solution.</span><span class="sxs-lookup"><span data-stu-id="6eadc-331">Open the **Manage NuGet Packages** dialog for the solution.</span></span>
2. <span data-ttu-id="6eadc-332">Dans le volet de gauche, sélectionnez **Packages installés**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-332">In the left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="6eadc-333">Recherchez le package *Azure Storage* et cliquez sur **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-333">Find the *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="6eadc-334">Dans la boîte de dialogue **Sélectionner les projets**, activez la case à cocher **ContosoAdsWeb**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-334">In the **Select Projects** box, select the **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="6eadc-335">Ces trois projets ont recours à Entity Framework pour utiliser les données de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="6eadc-335">All three projects use the Entity Framework to work with data in SQL Database.</span></span>
5. <span data-ttu-id="6eadc-336">Dans le volet gauche, sélectionnez **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-336">In the left pane, select **Online**.</span></span>
6. <span data-ttu-id="6eadc-337">Recherchez le package NuGet *EntityFramework* et installez-le dans les trois projets.</span><span class="sxs-lookup"><span data-stu-id="6eadc-337">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="6eadc-338">Définition des références de projet</span><span class="sxs-lookup"><span data-stu-id="6eadc-338">Set project references</span></span>
<span data-ttu-id="6eadc-339">Les projets web et de tâches web utilisent la base de données SQL ; les deux nécessitent une référence au projet ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="6eadc-339">Both web and WebJob projects work with the SQL database, so both need a reference to the ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="6eadc-340">Dans le projet ContosoAdsWeb, définissez une référence au projet ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="6eadc-340">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="6eadc-341">Cliquez avec le bouton droit sur le projet ContosoAdsWeb, puis cliquez sur **Ajouter** > **Référence**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-341">(Right-click the ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="6eadc-342">Dans la boîte de dialogue **Gestionnaire de références**, sélectionnez **Projets** > **Solution** > **ContosoAdsCommon**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-342">In the **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="6eadc-343">Le projet web nécessite des références pour utiliser des images et accéder aux chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="6eadc-343">The WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="6eadc-344">Dans le projet ContosoAdsWebJob, définissez une référence à `System.Drawing` et `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="6eadc-344">In the ContosoAdsWebJob project, set a reference to `System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="6eadc-345">Ajout de fichiers de code et de configuration</span><span class="sxs-lookup"><span data-stu-id="6eadc-345">Add code and configuration files</span></span>
<span data-ttu-id="6eadc-346">Ce didacticiel n'explique pas comment [créer des contrôleurs et des vues MVC à l'aide de la structure](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), comment [écrire du code Entity Framework qui fonctionne avec les bases de données SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), [ni les bases de la programmation asynchrone dans ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="6eadc-346">This tutorial does not show how to [create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how to [write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [the basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="6eadc-347">Il ne reste donc qu’à copier les fichiers de code et de configuration de la solution téléchargée dans la nouvelle solution.</span><span class="sxs-lookup"><span data-stu-id="6eadc-347">So, all that remains to do is copy code and configuration files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="6eadc-348">Ensuite, les sections suivantes montrent et expliquent les éléments essentiels de ce code.</span><span class="sxs-lookup"><span data-stu-id="6eadc-348">After you do that, the following sections show and explain key parts of the code.</span></span>

<span data-ttu-id="6eadc-349">Pour ajouter des fichiers à un projet ou à un dossier, cliquez avec le bouton droit sur le projet ou le dossier, puis cliquez sur **Ajouter** > **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-349">To add files to a project or a folder, right-click the project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="6eadc-350">Sélectionnez les fichiers et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-350">Select the files you want and click **Add**.</span></span> <span data-ttu-id="6eadc-351">Si un message vous demande si vous souhaitez remplacer les fichiers existants, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="6eadc-351">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="6eadc-352">Dans le projet ContosoAdsCommon, supprimez le fichier *Class1.cs* et ajoutez à la place les fichiers suivants du projet téléchargé.</span><span class="sxs-lookup"><span data-stu-id="6eadc-352">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the following files from the downloaded project.</span></span>

   * <span data-ttu-id="6eadc-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="6eadc-353">*Ad.cs*</span></span>
   * <span data-ttu-id="6eadc-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="6eadc-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="6eadc-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="6eadc-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="6eadc-356">Dans le projet ContosoAdsWeb, ajoutez les fichiers suivants du projet téléchargé.</span><span class="sxs-lookup"><span data-stu-id="6eadc-356">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="6eadc-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="6eadc-357">*Web.config*</span></span>
   * <span data-ttu-id="6eadc-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="6eadc-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="6eadc-359">Dans le dossier *Controllers* : *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="6eadc-359">In the *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="6eadc-360">Dans le dossier *Views\Shared* : fichier *_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="6eadc-360">In the *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="6eadc-361">Dans le dossier *Views\Home* : *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="6eadc-361">In the *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="6eadc-362">Dans le dossier *Views\Ad* (à créer) : cinq fichiers *.cshtml*</span><span class="sxs-lookup"><span data-stu-id="6eadc-362">In the *Views\Ad* folder (create the folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="6eadc-363">Dans le projet ContosoAdsWebJob, ajoutez les fichiers suivants du projet téléchargé.</span><span class="sxs-lookup"><span data-stu-id="6eadc-363">In the ContosoAdsWebJob project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="6eadc-364">*App.config* (indiquez le type de fichier **Tous les fichiers**)</span><span class="sxs-lookup"><span data-stu-id="6eadc-364">*App.config* (change the file type filter to **All Files**)</span></span>
   * <span data-ttu-id="6eadc-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="6eadc-365">*Program.cs*</span></span>
   * <span data-ttu-id="6eadc-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="6eadc-366">*Functions.cs*</span></span>

<span data-ttu-id="6eadc-367">Vous pouvez maintenant générer, exécuter et déployer l'application en suivant les instructions fournies précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6eadc-367">You can now build, run, and deploy the application as instructed earlier in the tutorial.</span></span> <span data-ttu-id="6eadc-368">Toutefois, avant cela, arrêtez la tâche web toujours en cours d’exécution dans la première application web dans laquelle vous l’avez déployée.</span><span class="sxs-lookup"><span data-stu-id="6eadc-368">Before you do that, however, stop the WebJob that is still running in the first web app you deployed to.</span></span> <span data-ttu-id="6eadc-369">Dans le cas contraire, cette tâche web traite les messages de file d’attente créés localement ou par l’application en cours d’exécution dans une nouvelle application web, car ils utilisent tous le même compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-369">Otherwise, that WebJob will process queue messages created locally or by the app running in a new web app, since all are using the same storage account.</span></span>

## <span data-ttu-id="6eadc-370"><a id="code"></a>Vérifier le code de l’application</span><span class="sxs-lookup"><span data-stu-id="6eadc-370"><a id="code"></a>Review the application code</span></span>
<span data-ttu-id="6eadc-371">Les sections suivantes présentent le code utilisé avec le Kit de développement logiciel (SDK) WebJobs et des objets blob et des files d'attente Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-371">The following sections explain the code related to working with the WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="6eadc-372">Pour le code spécifique au kit de développement logiciel (SDK) WebJobs, accédez aux sections [Program.cs et Functions.cs](#programcs) .</span><span class="sxs-lookup"><span data-stu-id="6eadc-372">For the code specific to the WebJobs SDK, go to the [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="6eadc-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="6eadc-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="6eadc-374">Le fichier Ad.cs définit une énumération des catégories de publicité et une classe d'entité POCO pour les informations de publicité.</span><span class="sxs-lookup"><span data-stu-id="6eadc-374">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="6eadc-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="6eadc-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="6eadc-376">La classe ContosoAdsContext spécifie que la classe Ad est utilisée dans une collection DbSet, qui est stockée par Entity Framework dans une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="6eadc-376">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="6eadc-377">La classe a deux constructeurs.</span><span class="sxs-lookup"><span data-stu-id="6eadc-377">The class has two constructors.</span></span> <span data-ttu-id="6eadc-378">Le premier est utilisé par le projet web et spécifie le nom d'une chaîne de connexion stockée dans le fichier Web.config de l'environnement d'exécution Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-378">The first is used by the web project, and specifies the name of a connection string that is stored in the Web.config file or the Azure runtime environment.</span></span> <span data-ttu-id="6eadc-379">Le second vous permet de passer la chaîne de connexion existante.</span><span class="sxs-lookup"><span data-stu-id="6eadc-379">The second constructor enables you to pass in the actual connection string.</span></span> <span data-ttu-id="6eadc-380">Le projet de rôle de travail, qui ne comporte pas de fichier Web.config. nécessite cette opération.</span><span class="sxs-lookup"><span data-stu-id="6eadc-380">That is needed by the WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="6eadc-381">Vous avez vu précédemment où est stockée cette chaîne de connexion, et vous allez voir comme le code la récupère quand il instancie la classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="6eadc-381">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="6eadc-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="6eadc-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="6eadc-383">La classe `BlobInformation` permet de stocker les informations d’un objet blob d’image dans un message de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="6eadc-383">The `BlobInformation` class is used to store information about an image blob in a queue message.</span></span>

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


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="6eadc-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="6eadc-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="6eadc-385">Le code appelé par la méthode `Application_Start` crée un conteneur d’objets blob *images* et une file d’attente *images*, s’ils n’existent pas déjà.</span><span class="sxs-lookup"><span data-stu-id="6eadc-385">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="6eadc-386">Cela garantit que, lorsque vous commencez à utiliser un nouveau compte de stockage, le conteneur d'objets blob et la file d'attente nécessaires sont créés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="6eadc-386">This ensures that whenever you start using a new storage account, the required blob container and queue are created automatically.</span></span>

<span data-ttu-id="6eadc-387">Le code a accès au compte de stockage en utilisant la chaîne de connexion du fichier *Web.config* ou l'environnement d'exécution Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-387">The code gets access to the storage account by using the storage connection string from the *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="6eadc-388">Il obtient ensuite une référence au conteneur d’objets blob *images*, crée le conteneur s’il n’existe pas, et définit les autorisations d’accès au nouveau conteneur.</span><span class="sxs-lookup"><span data-stu-id="6eadc-388">Then, it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="6eadc-389">Par défaut, les nouveaux conteneurs ne donnent accès aux objets blob qu’aux clients disposant d’informations d’identification de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6eadc-389">By default, new containers allow only clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="6eadc-390">L’application web a besoin que les objets blob soient publics pour afficher des images en utilisant des URL qui pointent vers les objets blob de ces images.</span><span class="sxs-lookup"><span data-stu-id="6eadc-390">The web app needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

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

<span data-ttu-id="6eadc-391">Du code similaire obtient une référence à la file d’attente *thumbnailrequest* et crée une nouvelle file d’attente.</span><span class="sxs-lookup"><span data-stu-id="6eadc-391">Similar code gets a reference to the *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="6eadc-392">Dans ce cas, aucune modification des autorisations n'est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6eadc-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="6eadc-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="6eadc-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="6eadc-394">Le fichier *_Layout.cshtml* définit le nom de l’application dans l’en-tête et le pied de page, puis crée une entrée de menu « Ads ».</span><span class="sxs-lookup"><span data-stu-id="6eadc-394">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="6eadc-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="6eadc-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="6eadc-396">Le fichier *Views\Home\Index.cshtml* affiche les liens de catégorie sur la page d'accueil.</span><span class="sxs-lookup"><span data-stu-id="6eadc-396">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="6eadc-397">Les liens transmettent la valeur entière de l’énumération `Category` d’une variable querystring à la page Ads Index.</span><span class="sxs-lookup"><span data-stu-id="6eadc-397">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="6eadc-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="6eadc-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="6eadc-399">Dans le fichier *AdController.cs*, le constructeur appelle la méthode `InitializeStorage` pour créer les objets de la bibliothèque cliente Azure Storage, qui fournissent une API pour les objets blob et les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="6eadc-399">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="6eadc-400">Le code obtient ensuite une référence au conteneur d’objets blob *images* comme vu précédemment dans *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="6eadc-400">Then, the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="6eadc-401">Ce faisant, il définit une [stratégie de nouvelles tentatives](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) par défaut appropriée pour une application web.</span><span class="sxs-lookup"><span data-stu-id="6eadc-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="6eadc-402">La stratégie de nouvelles tentatives d'interruption exponentielle par défaut peut suspendre l'application web pendant plus d'une minute en cas de tentatives répétées pour une erreur temporaire.</span><span class="sxs-lookup"><span data-stu-id="6eadc-402">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="6eadc-403">La stratégie de nouvelle tentative spécifiée ici laisse trois secondes après chaque nouvelle tentative, jusqu’à trois.</span><span class="sxs-lookup"><span data-stu-id="6eadc-403">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="6eadc-404">Un code similaire obtient une référence à la file d'attente *images* .</span><span class="sxs-lookup"><span data-stu-id="6eadc-404">Similar code gets a reference to the *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="6eadc-405">La plupart du code du contrôleur permet généralement d'utiliser un modèle de données Entity Framework en utilisant une classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="6eadc-405">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="6eadc-406">La méthode HttpPost `Create` est une exception, car elle télécharge un fichier et l’enregistre dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="6eadc-406">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="6eadc-407">Le classeur de modèles fournit un objet [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) à la méthode.</span><span class="sxs-lookup"><span data-stu-id="6eadc-407">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="6eadc-408">Si l'utilisateur a sélectionné un fichier à télécharger, le code met à jour le fichier, l'enregistre dans un objet blob et met à jour l'enregistrement de base de données AD avec une URL qui pointe vers l'objet blob.</span><span class="sxs-lookup"><span data-stu-id="6eadc-408">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="6eadc-409">Le code qui procède au téléchargement se trouve dans la méthode `UploadAndSaveBlobAsync` .</span><span class="sxs-lookup"><span data-stu-id="6eadc-409">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="6eadc-410">Il crée un nom GUID pour l'objet blob, télécharge et enregistre le fichier, et renvoie une référence vers l'objet blob enregistré.</span><span class="sxs-lookup"><span data-stu-id="6eadc-410">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="6eadc-411">Une fois que la méthode HttpPost `Create` a téléchargé un objet blob et mis à jour la base de données, elle crée un message de file d’attente pour informer ce processus d’arrière-plan qu’une image est prête à être convertie en vignette.</span><span class="sxs-lookup"><span data-stu-id="6eadc-411">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform the back-end process that an image is ready for conversion to a thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="6eadc-412">Le code de la méthode HttpPost `Edit` est similaire, mais si l’utilisateur sélectionne un nouveau fichier image, les objets blob qui existent pour cette publicité doivent être supprimés.</span><span class="sxs-lookup"><span data-stu-id="6eadc-412">The code for the HttpPost `Edit` method is similar, except that if the user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="6eadc-413">Voici le code qui supprime les objets blob lorsque vous supprimez une publicité :</span><span class="sxs-lookup"><span data-stu-id="6eadc-413">Here is the code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="6eadc-414">ContosoAdsWeb - Views\Ad\Index.cshtml et Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="6eadc-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="6eadc-415">Le fichier *Index.cshtml* affiche des vignettes avec les autres données de publicité :</span><span class="sxs-lookup"><span data-stu-id="6eadc-415">The *Index.cshtml* file displays thumbnails with the other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="6eadc-416">Le fichier *Details.cshtml* affiche l'image intégrale :</span><span class="sxs-lookup"><span data-stu-id="6eadc-416">The *Details.cshtml* file displays the full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="6eadc-417">ContosoAdsWeb - Views\Ad\Create.cshtml et Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="6eadc-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="6eadc-418">Les fichiers *Create.cshtml* et *Edit.cshtml* spécifient l’encodage de formulaire qui permet au contrôleur d’obtenir l’objet `HttpPostedFileBase`.</span><span class="sxs-lookup"><span data-stu-id="6eadc-418">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="6eadc-419">Un élément `<input>` indique au navigateur de fournir une boîte de dialogue de sélection de fichier.</span><span class="sxs-lookup"><span data-stu-id="6eadc-419">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="6eadc-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="6eadc-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="6eadc-421">Lorsque la tâche web démarre, la méthode `Main` appelle la méthode `JobHost.RunAndBlock` du Kit de développement logiciel (SDK) WebJobs pour commencer l’exécution des fonctions déclenchées sur le thread actuel.</span><span class="sxs-lookup"><span data-stu-id="6eadc-421">When the WebJob starts, the `Main` method calls the WebJobs SDK `JobHost.RunAndBlock` method to begin execution of triggered functions on the current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="6eadc-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - Méthode GenerateThumbnail</span><span class="sxs-lookup"><span data-stu-id="6eadc-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="6eadc-423">Le Kit de développement logiciel (SDK) WebJobs appelle cette méthode lorsqu'un message de file d'attente est reçu.</span><span class="sxs-lookup"><span data-stu-id="6eadc-423">The WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="6eadc-424">Cette méthode crée une vignette et place son URL dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="6eadc-424">The method creates a thumbnail and puts the thumbnail URL in the database.</span></span>

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
            // be instantiated and disposed within the function.
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

* <span data-ttu-id="6eadc-425">L’attribut `QueueTrigger` demande au Kit de développement logiciel (SDK) WebJobs d’appeler cette méthode lorsqu’un nouveau message est reçu dans la file d’attente thumbnailrequest.</span><span class="sxs-lookup"><span data-stu-id="6eadc-425">The `QueueTrigger` attribute directs the WebJobs SDK to call this method when a new message is received on the thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="6eadc-426">L’objet `BlobInformation` dans le message de file d’attente est automatiquement désérialisé dans le paramètre `blobInfo`.</span><span class="sxs-lookup"><span data-stu-id="6eadc-426">The `BlobInformation` object in the queue message is automatically deserialized into the `blobInfo` parameter.</span></span> <span data-ttu-id="6eadc-427">Lorsque la méthode est terminée, le message de file d'attente est supprimé.</span><span class="sxs-lookup"><span data-stu-id="6eadc-427">When the method completes, the queue message is deleted.</span></span> <span data-ttu-id="6eadc-428">Si la méthode échoue avant de se terminer, le message de file d'attente n'est pas supprimé ; après un bail de 10 minutes, il est libéré pour être à nouveau sélectionné et traité.</span><span class="sxs-lookup"><span data-stu-id="6eadc-428">If the method fails before completing, the queue message is not deleted; after a 10-minute lease expires, the message is released to be picked up again and processed.</span></span> <span data-ttu-id="6eadc-429">Cette séquence ne se répète pas indéfiniment si un message provoque toujours une exception.</span><span class="sxs-lookup"><span data-stu-id="6eadc-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="6eadc-430">Après 5 tentatives ayant échoué de traitement d'un message, celui-ci est déplacé dans la file d'attente nommée {queuename}-poison.</span><span class="sxs-lookup"><span data-stu-id="6eadc-430">After 5 unsuccessful attempts to process a message, the message is moved to a queue named {queuename}-poison.</span></span> <span data-ttu-id="6eadc-431">Vous pouvez configurer le nombre maximal de tentatives.</span><span class="sxs-lookup"><span data-stu-id="6eadc-431">The maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="6eadc-432">Les deux attributs `Blob` fournissent des objets qui sont liés aux objets blob : un pour l’objet blob d’image existant et un pour le nouvel objet blob miniature créé par la méthode.</span><span class="sxs-lookup"><span data-stu-id="6eadc-432">The two `Blob` attributes provide objects that are bound to blobs: one to the existing image blob and one to a new thumbnail blob that the method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="6eadc-433">Les noms des objets blob proviennent des propriétés de l’objet `BlobInformation` reçu dans le message de file d’attente ((`BlobName` et `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="6eadc-433">Blob names come from properties of the `BlobInformation` object received in the queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="6eadc-434">Pour profiter de toutes les fonctionnalités de la bibliothèque cliente de stockage, vous pouvez utiliser des objets blob à l’aide de la classe `CloudBlockBlob`.</span><span class="sxs-lookup"><span data-stu-id="6eadc-434">To get the full functionality of the Storage Client Library, you can use the `CloudBlockBlob` class to work with blobs.</span></span> <span data-ttu-id="6eadc-435">Si vous voulez réutiliser du code écrit pour des objets `Stream`, optez pour la classe `Stream`.</span><span class="sxs-lookup"><span data-stu-id="6eadc-435">If you want to reuse code that was written to work with `Stream` objects, you can use the `Stream` class.</span></span>

<span data-ttu-id="6eadc-436">Pour plus d’informations sur l’écriture de fonctions utilisant des attributs du Kit de développement logiciel (SDK) WebJobs, voir les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="6eadc-436">For more information about how to write functions that use  WebJobs SDK attributes, see the following resources:</span></span>

* [<span data-ttu-id="6eadc-437">Utilisation du stockage de file d’attente Microsoft Azure avec le Kit de développement logiciel (SDK) WebJobs</span><span class="sxs-lookup"><span data-stu-id="6eadc-437">How to use Azure queue storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="6eadc-438">Utilisation du stockage d’objets blob Azure avec le Kit de développement logiciel (SDK) WebJobs</span><span class="sxs-lookup"><span data-stu-id="6eadc-438">How to use Azure blob storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="6eadc-439">Utilisation du stockage de tables Microsoft Azure avec le Kit de développement logiciel (SDK) WebJobs</span><span class="sxs-lookup"><span data-stu-id="6eadc-439">How to use Azure table storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="6eadc-440">Utilisation de Microsoft Azure Service Bus avec le Kit de développement logiciel (SDK) WebJobs</span><span class="sxs-lookup"><span data-stu-id="6eadc-440">How to use Azure Service Bus with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="6eadc-441">Si votre application web s'exécute sur plusieurs machines virtuelles, plusieurs WebJobs seront exécutés simultanément et, dans certains cas, cela peut entraîner le traitement multiple des mêmes données.</span><span class="sxs-lookup"><span data-stu-id="6eadc-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in the same data getting processed multiple times.</span></span> <span data-ttu-id="6eadc-442">Cela n'est pas un problème si vous utilisez la file d'attente, le blob et les déclencheurs Service Bus intégrés.</span><span class="sxs-lookup"><span data-stu-id="6eadc-442">This is not a problem if you use the built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="6eadc-443">Le Kit de développement logiciel (SDK) garantit que vos fonctions ne seront traitées qu'une seule fois pour chaque message ou objet blob.</span><span class="sxs-lookup"><span data-stu-id="6eadc-443">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="6eadc-444">Pour plus d’informations sur la façon d’implémenter l’arrêt approprié, consultez la rubrique [Arrêt approprié](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="6eadc-444">For information about how to implement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="6eadc-445">Le code de la méthode `ConvertImageToThumbnailJPG` (non représenté) utilise des classes dans l’espace de noms `System.Drawing` pour plus de simplicité.</span><span class="sxs-lookup"><span data-stu-id="6eadc-445">The code in the `ConvertImageToThumbnailJPG` method (not shown) uses classes in the `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="6eadc-446">Cependant, les classes de cet espace de noms ont été conçues pour être utilisées avec Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="6eadc-446">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="6eadc-447">Elles ne sont pas prises en charge dans un service Windows ou ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6eadc-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="6eadc-448">Pour plus d’informations sur les options de traitement d’images, consultez les rubriques [Génération d’images dynamiques](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) et [Redimensionnement d’images approfondi](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="6eadc-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6eadc-449">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6eadc-449">Next steps</span></span>
<span data-ttu-id="6eadc-450">Dans ce didacticiel, nous avons vu une simple application multiniveau qui utilise le Kit de développement logiciel (SDK) WebJobs pour le traitement principal.</span><span class="sxs-lookup"><span data-stu-id="6eadc-450">In this tutorial, you've seen a simple multi-tier application that uses the WebJobs SDK for backend processing.</span></span> <span data-ttu-id="6eadc-451">Cette section propose des suggestions pour en savoir plus sur les applications à plusieurs niveaux ASP.NET et WebJobs.</span><span class="sxs-lookup"><span data-stu-id="6eadc-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="6eadc-452">Fonctionnalités manquantes</span><span class="sxs-lookup"><span data-stu-id="6eadc-452">Missing features</span></span>
<span data-ttu-id="6eadc-453">L'application est intentionnellement simple pour un didacticiel de prise en main.</span><span class="sxs-lookup"><span data-stu-id="6eadc-453">The application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="6eadc-454">Dans une application réelle, vous implémenteriez l’[injection de dépendances](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) et les [modèles de référentiel et d’élément de travail](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), et vous utiliseriez [une interface pour la connexion](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), les [migrations Code First EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) pour gérer les changements de modèles de données et la [résilience des connexions EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) pour gérer les erreurs réseau temporaires.</span><span class="sxs-lookup"><span data-stu-id="6eadc-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="6eadc-455">Mise à l’échelle de WebJobs</span><span class="sxs-lookup"><span data-stu-id="6eadc-455">Scaling WebJobs</span></span>
<span data-ttu-id="6eadc-456">Les tâches web s’exécutent dans le contexte d’une application web et ne sont pas évolutives séparément.</span><span class="sxs-lookup"><span data-stu-id="6eadc-456">WebJobs run in the context of a web app and are not scalable separately.</span></span> <span data-ttu-id="6eadc-457">Par exemple, si vous disposez d’une instance d’application web Standard, vous n’avez qu’une seule instance en cours d’exécution du processus en arrière-plan. Cette dernière utilise certaines ressources du serveur (unité centrale, mémoire, etc.) qui seraient autrement disponibles pour distribuer du contenu web.</span><span class="sxs-lookup"><span data-stu-id="6eadc-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of the server resources (CPU, memory, etc.) that otherwise would be available to serve web content.</span></span>

<span data-ttu-id="6eadc-458">Si le trafic varie au cours de la journée ou de la semaine et si le traitement principal dont vous avez besoin peut attendre, vous pouvez planifier l'exécution de vos tâches web aux heures de faible trafic.</span><span class="sxs-lookup"><span data-stu-id="6eadc-458">If traffic varies by time of day or day of week, and if the backend processing you need to do can wait, you could schedule your WebJobs to run at low-traffic times.</span></span> <span data-ttu-id="6eadc-459">Si la charge est encore trop élevée pour cette solution, vous pouvez exécuter le serveur principal comme un WebJob dans une application web distincte dédiée à cet effet.</span><span class="sxs-lookup"><span data-stu-id="6eadc-459">If the load is still too high for that solution, you can run the backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="6eadc-460">Vous pouvez ensuite faire évoluer votre application web principale indépendamment de votre application web frontale.</span><span class="sxs-lookup"><span data-stu-id="6eadc-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="6eadc-461">Pour plus d’informations, consultez [Mise à l’échelle WebJobs](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="6eadc-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="6eadc-462">Éviter les arrêts dus à l’expiration des applications web</span><span class="sxs-lookup"><span data-stu-id="6eadc-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="6eadc-463">Pour vous assurer que vos WebJobs sont toujours en cours d’exécution sur toutes les instances de votre application web, vous devez activer la fonctionnalité [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6eadc-463">To make sure your WebJobs are always running, and running on all instances of your web app, you have to enable the [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="6eadc-464">Utilisation du Kit de développement logiciel (SDK) WebJobs en dehors de WebJobs</span><span class="sxs-lookup"><span data-stu-id="6eadc-464">Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="6eadc-465">Un programme qui utilise le Kit SDK WebJobs ne doit pas obligatoirement s’exécuter dans Azure dans une tâche web.</span><span class="sxs-lookup"><span data-stu-id="6eadc-465">A program that uses the WebJobs SDK doesn't have to run in Azure in a WebJob.</span></span> <span data-ttu-id="6eadc-466">Il peut s'exécuter localement, ou dans d'autres environnements tels qu'un rôle de travail de service cloud ou un service Windows.</span><span class="sxs-lookup"><span data-stu-id="6eadc-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="6eadc-467">Toutefois, vous ne pouvez accéder au tableau de bord du Kit de développement logiciel (SDK) WebJobs que par le biais d’une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="6eadc-467">However, you can only access the WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="6eadc-468">Pour utiliser le tableau de bord, vous devez connecter l’application web au compte de stockage que vous utilisez en définissant la chaîne de connexion AzureWebJobsDashboard sous l’onglet **Configurer** du portail Classic.</span><span class="sxs-lookup"><span data-stu-id="6eadc-468">To use the dashboard you have to connect the web app to the storage account you're using by setting the AzureWebJobsDashboard connection string on the **Configure** tab of the classic portal.</span></span> <span data-ttu-id="6eadc-469">Vous pouvez ensuite accéder au tableau de bord à l’aide de l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="6eadc-469">Then, you can get to the Dashboard by using the following URL:</span></span>

<span data-ttu-id="6eadc-470">https://{nom_d’application_web}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="6eadc-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="6eadc-471">Pour plus d'informations, consultez le billet de blog [Récupération d'un tableau de bord pour un développement local avec le Kit de développement logiciel (SDK) WebJobs](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx)(notez cependant qu'il affiche un ancien nom de chaîne de connexion).</span><span class="sxs-lookup"><span data-stu-id="6eadc-471">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="6eadc-472">Plus de documentation relative à WebJobs</span><span class="sxs-lookup"><span data-stu-id="6eadc-472">More WebJobs documentation</span></span>
<span data-ttu-id="6eadc-473">Pour plus d’informations, consultez [Ressources de documentation relatives à Azure WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="6eadc-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
