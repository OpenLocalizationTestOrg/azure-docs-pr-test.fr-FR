---
title: aaaBottle et stockage de Table Azure sur Windows Azure avec 2.2 des outils Python pour Visual Studio
description: "Découvrez comment toouse hello outils Python pour Visual Studio toocreate, une application d’eau qui stocke les données dans le stockage Table Azure et déployer hello web application tooAzure App Service Web Apps."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="86bad-103">Bottle et stockage de tables Azure sur Azure avec Python Tools 2.2 pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86bad-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="86bad-104">Dans ce didacticiel, nous allons utiliser [outils Python pour Visual Studio] toocreate simple interroge l’application web à l’aide d’un des exemples de modèles de PTVS hello.</span><span class="sxs-lookup"><span data-stu-id="86bad-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="86bad-105">Ce didacticiel est également disponible en [vidéo](https://www.youtube.com/watch?v=GJXDGaEPy94).</span><span class="sxs-lookup"><span data-stu-id="86bad-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="86bad-106">application web de sondages Hello définit une abstraction pour son espace de stockage, afin que vous pouvez facilement basculer entre les différents types de référentiels (en mémoire, stockage de tables Azure, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="86bad-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="86bad-107">Vous allez apprendre comment toocreate un stockage Azure de compte, comment tooconfigure hello web application toouse stockage de tables Azure et toopublish hello web application trop[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="86bad-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="86bad-108">Consultez hello [centre de développement Python] autres articles qui couvrent le développement de Azure App Service Web Apps avec PTVS à l’aide d’eau, ballon Django web et infrastructures, avec les services MongoDB, stockage de tables Azure, MySQL et base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="86bad-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="86bad-109">Alors que cet article se concentre sur le Service d’applications, les étapes de hello sont similaires lors du développement [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="86bad-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86bad-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="86bad-110">Prerequisites</span></span>
* <span data-ttu-id="86bad-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="86bad-111">Visual Studio 2015</span></span>
* <span data-ttu-id="86bad-112">[Python Tools 2.2 pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="86bad-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="86bad-113">[2.2 des outils Python pour Visual Studio exemples VSIX]</span><span class="sxs-lookup"><span data-stu-id="86bad-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="86bad-114">[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="86bad-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="86bad-115">[Python 2.7 32 bits] ou [Python 3.4 32 bits]</span><span class="sxs-lookup"><span data-stu-id="86bad-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="86bad-116">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="86bad-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="86bad-117">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="86bad-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="86bad-118">Créer hello projet</span><span class="sxs-lookup"><span data-stu-id="86bad-118">Create hello Project</span></span>
<span data-ttu-id="86bad-119">Dans cette section, nous allons créer un projet Visual Studio à l’aide d’un exemple de modèle.</span><span class="sxs-lookup"><span data-stu-id="86bad-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="86bad-120">Nous allons créer un environnement virtuel et installer les packages requis.</span><span class="sxs-lookup"><span data-stu-id="86bad-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="86bad-121">Puis nous exécuterons application hello localement à l’aide de référentiel de hello par défaut en mémoire.</span><span class="sxs-lookup"><span data-stu-id="86bad-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="86bad-122">Dans Visual Studio, sélectionnez **Fichier**, **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="86bad-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="86bad-123">Hello des modèles de projet à partir de hello [2.2 des outils Python pour Visual Studio exemples VSIX] sont disponibles sous **Python**, **exemples**.</span><span class="sxs-lookup"><span data-stu-id="86bad-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="86bad-124">Sélectionnez **interroge Bottle Web projet** et cliquez sur OK toocreate hello projet.</span><span class="sxs-lookup"><span data-stu-id="86bad-124">Select **Polls Bottle Web Project** and click OK toocreate hello project.</span></span>
   
     ![Boîte de dialogue Nouveau projet](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="86bad-126">Vous serez invité à tooinstall les packages externes.</span><span class="sxs-lookup"><span data-stu-id="86bad-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="86bad-127">Sélectionnez **Installer dans un environnement virtuel**.</span><span class="sxs-lookup"><span data-stu-id="86bad-127">Select **Install into a virtual environment**.</span></span>
   
     ![Boîte de dialogue Packages externes](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="86bad-129">Sélectionnez **Python 2.7** ou **Python 3.4** comme interpréteur de base hello.</span><span class="sxs-lookup"><span data-stu-id="86bad-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Boîte de dialogue Ajouter un environnement virtuel](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="86bad-131">Vérifier que l’application hello fonctionne en appuyant sur `F5`.</span><span class="sxs-lookup"><span data-stu-id="86bad-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="86bad-132">Par défaut, application hello utilise un référentiel en mémoire qui ne nécessite aucune configuration.</span><span class="sxs-lookup"><span data-stu-id="86bad-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="86bad-133">Toutes les données sont perdues lorsque hello web server est arrêté.</span><span class="sxs-lookup"><span data-stu-id="86bad-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="86bad-134">Cliquez sur **Créer un exemple de sondage**, puis sur un sondage et un vote.</span><span class="sxs-lookup"><span data-stu-id="86bad-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Navigateur web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="86bad-136">Création d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="86bad-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="86bad-137">toouse des opérations de stockage, vous devez un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="86bad-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="86bad-138">Pour en créer un, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="86bad-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="86bad-139">Ouvrez une session sur hello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="86bad-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="86bad-140">Cliquez sur hello **nouveau** icône en haut de hello à gauche de hello Portal, puis cliquez sur **données + stockage** > **compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="86bad-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="86bad-141">Cliquez sur hello **créer** bouton, puis donnez un nom unique à compte de stockage hello et créer un nouveau [groupe de ressources](../azure-resource-manager/resource-group-overview.md) pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="86bad-141">Click hello **Create** button, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Création rapide](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="86bad-143">Lorsque le compte de stockage hello a été créé, hello **Notifications** un vert clignote en bouton **réussite** et panneau du compte de stockage hello est ouvert tooshow qu’il appartient toohello nouvelle ressource groupe que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="86bad-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="86bad-144">Cliquez sur hello **clés d’accès** partie dans le panneau du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="86bad-144">Click hello **Access keys** part in hello storage account's blade.</span></span> <span data-ttu-id="86bad-145">Prenez note du nom du compte hello et key1.</span><span class="sxs-lookup"><span data-stu-id="86bad-145">Take note of hello account name and key1.</span></span>
   
      ![Clés](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="86bad-147">Nous devons cette tooconfigure informations votre projet dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="86bad-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="86bad-148">Configurer hello projet</span><span class="sxs-lookup"><span data-stu-id="86bad-148">Configure hello Project</span></span>
<span data-ttu-id="86bad-149">Dans cette section, nous allons configurer notre compte de stockage application toouse hello que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="86bad-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="86bad-150">Ensuite, nous allons exécuter application hello localement.</span><span class="sxs-lookup"><span data-stu-id="86bad-150">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="86bad-151">Dans Visual Studio, cliquez avec le bouton droit sur le nœud de votre projet dans l’Explorateur de solutions, puis sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="86bad-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="86bad-152">Cliquez sur hello **déboguer** onglet.</span><span class="sxs-lookup"><span data-stu-id="86bad-152">Click on hello **Debug** tab.</span></span>
   
     ![Paramètres de débogage du projet](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="86bad-154">Définir les valeurs des variables d’environnement requises par l’application hello dans hello **déboguer la commande de serveur**, **environnement**.</span><span class="sxs-lookup"><span data-stu-id="86bad-154">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="86bad-155">Ceci permettra de définir les variables d’environnement hello lorsque vous **démarrer le débogage**.</span><span class="sxs-lookup"><span data-stu-id="86bad-155">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="86bad-156">Si vous souhaitez hello variables toobe définie lorsque vous **démarrer sans débogage**, hello ensemble sous les mêmes valeurs **exécuter une commande de serveur** également.</span><span class="sxs-lookup"><span data-stu-id="86bad-156">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="86bad-157">Vous pouvez également définir des variables d’environnement à l’aide de hello le panneau de configuration Windows.</span><span class="sxs-lookup"><span data-stu-id="86bad-157">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="86bad-158">Il s’agit d’une meilleure option si vous souhaitez tooavoid stocke des informations d’identification dans le code source / fichier de projet.</span><span class="sxs-lookup"><span data-stu-id="86bad-158">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="86bad-159">Notez que vous devez toorestart Visual Studio pour l’application de hello nouvel environnement valeurs toobe toohello disponible.</span><span class="sxs-lookup"><span data-stu-id="86bad-159">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="86bad-160">code Hello qui implémente le référentiel de stockage de Table Azure hello se trouve dans **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="86bad-160">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="86bad-161">Consultez hello [documentation] pour plus d’informations sur la façon de toouse Service de Table à partir de Python.</span><span class="sxs-lookup"><span data-stu-id="86bad-161">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="86bad-162">Exécutez l’application hello avec `F5`.</span><span class="sxs-lookup"><span data-stu-id="86bad-162">Run hello application with `F5`.</span></span> <span data-ttu-id="86bad-163">Les interrogations sont créées avec **créer des sondages exemple** et données hello soumises par le vote seront sérialisées dans le stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="86bad-163">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="86bad-164">Hello environnement virtuel de Python 2.7 peut provoquer un arrêt de l’exception dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="86bad-164">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="86bad-165">Appuyez sur `F5` toocontinue chargement hello web projet.</span><span class="sxs-lookup"><span data-stu-id="86bad-165">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="86bad-166">Parcourir toohello **sur** tooverify page qui hello d’application à l’aide de hello **Azure Table Storage** référentiel.</span><span class="sxs-lookup"><span data-stu-id="86bad-166">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Navigateur web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="86bad-168">Explorer hello stockage de Table Azure</span><span class="sxs-lookup"><span data-stu-id="86bad-168">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="86bad-169">Il est facile tooview et modifier des tables de stockage à l’aide de l’Explorateur de Cloud dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="86bad-169">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="86bad-170">Dans cette section, nous allons utiliser contenu de hello tooview de l’Explorateur de serveurs de tables d’application interroge hello.</span><span class="sxs-lookup"><span data-stu-id="86bad-170">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="86bad-171">Cela nécessite toobe Microsoft Azure Tools installé, qui sont disponible dans le cadre de hello [Azure SDK pour .NET].</span><span class="sxs-lookup"><span data-stu-id="86bad-171">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="86bad-172">Ouvrez **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="86bad-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="86bad-173">Développez **Comptes de stockage**, votre compte de stockage, puis **Tables**.</span><span class="sxs-lookup"><span data-stu-id="86bad-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="86bad-175">Double-cliquez sur hello **interroge** ou **choix** contenu de hello tooview de table hello dans une fenêtre de document, ainsi que d’ajouter/supprimer/modifier des entités de table.</span><span class="sxs-lookup"><span data-stu-id="86bad-175">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Résultats de la requête de table](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="86bad-177">Publier hello web application tooAzure du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="86bad-177">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="86bad-178">Hello Kit de développement .NET Azure fournit un moyen simple de toodeploy votre tooAzure d’application web du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="86bad-178">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="86bad-179">Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="86bad-179">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Boîte de dialogue Publier le site Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="86bad-181">Cliquez sur **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="86bad-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="86bad-182">Cliquez sur **nouveau** toocreate une application web.</span><span class="sxs-lookup"><span data-stu-id="86bad-182">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="86bad-183">Renseignez hello suivant des champs, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="86bad-183">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="86bad-184">**Nom de l’application web**</span><span class="sxs-lookup"><span data-stu-id="86bad-184">**Web App name**</span></span>
   * <span data-ttu-id="86bad-185">**Plan App Service**</span><span class="sxs-lookup"><span data-stu-id="86bad-185">**App Service plan**</span></span>
   * <span data-ttu-id="86bad-186">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="86bad-186">**Resource group**</span></span>
   * <span data-ttu-id="86bad-187">**Région**</span><span class="sxs-lookup"><span data-stu-id="86bad-187">**Region**</span></span>
   * <span data-ttu-id="86bad-188">Laissez **serveur de base de données** défini trop**aucune base de données**</span><span class="sxs-lookup"><span data-stu-id="86bad-188">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="86bad-189">Acceptez toutes les valeurs par défaut et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="86bad-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="86bad-190">Votre navigateur web s’ouvre automatiquement toohello publié web app.</span><span class="sxs-lookup"><span data-stu-id="86bad-190">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="86bad-191">Si vous y accédez toohello sur la page, vous verrez qu’il utilise hello **In-Memory** référentiel, pas hello **Azure Table Storage** référentiel.</span><span class="sxs-lookup"><span data-stu-id="86bad-191">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="86bad-192">C’est parce que les variables d’environnement hello ne sont pas définies sur l’instance d’applications Web hello dans Azure App Service, afin d’utiliser les valeurs par défaut hello spécifiés dans **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="86bad-192">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="86bad-193">Configurer l’instance d’applications Web hello</span><span class="sxs-lookup"><span data-stu-id="86bad-193">Configure hello Web Apps instance</span></span>
<span data-ttu-id="86bad-194">Dans cette section, nous allons configurer les variables d’environnement pour l’instance d’applications Web hello.</span><span class="sxs-lookup"><span data-stu-id="86bad-194">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="86bad-195">Dans [Azure Portal], ouvrez le panneau de l’application hello web en cliquant sur **Parcourir** > **des Services d’application** > nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="86bad-195">In [Azure Portal], open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="86bad-196">Dans le volet de votre application web, cliquez sur **Tous les paramètres**, puis cliquez sur **Paramètres de l'application**.</span><span class="sxs-lookup"><span data-stu-id="86bad-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="86bad-197">Faites défiler vers le bas toohello **paramètres de l’application** section et définir des valeurs hello pour **référentiel\_nom**, **stockage\_nom** et  **STOCKAGE\_clé** comme décrit dans hello **projet hello de configurer** section ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="86bad-197">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Paramètres de l'application](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="86bad-199">Cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="86bad-199">Click on **Save**.</span></span> <span data-ttu-id="86bad-200">Une fois que vous avez reçu des notifications de hello que les modifications de hello ont été appliquées, cliquez sur **Parcourir** à partir du panneau principal de l’application hello Web.</span><span class="sxs-lookup"><span data-stu-id="86bad-200">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="86bad-201">Vous devez voir le travail d’application hello web comme prévu, à l’aide de hello **Azure Table Storage** référentiel.</span><span class="sxs-lookup"><span data-stu-id="86bad-201">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="86bad-202">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="86bad-202">Congratulations!</span></span>
   
     ![Navigateur web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="86bad-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="86bad-204">Next steps</span></span>
<span data-ttu-id="86bad-205">Suivez ces liens de toolearn plus d’informations sur les outils Python pour Visual Studio, d’eau et le stockage Table.</span><span class="sxs-lookup"><span data-stu-id="86bad-205">Follow these links toolearn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="86bad-206">[Documentation relative à Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="86bad-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="86bad-207">[Projets web]</span><span class="sxs-lookup"><span data-stu-id="86bad-207">[Web Projects]</span></span>
  * <span data-ttu-id="86bad-208">[Projets de service cloud]</span><span class="sxs-lookup"><span data-stu-id="86bad-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="86bad-209">[Débogage à distance sur Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="86bad-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="86bad-210">[Documentation relative à Bottle]</span><span class="sxs-lookup"><span data-stu-id="86bad-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="86bad-211">[Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="86bad-211">[Azure Storage]</span></span>
* <span data-ttu-id="86bad-212">[Kit de développement logiciel (SDK) Azure pour Python]</span><span class="sxs-lookup"><span data-stu-id="86bad-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="86bad-213">[Comment tooUse hello Service de stockage de Table à partir de Python]</span><span class="sxs-lookup"><span data-stu-id="86bad-213">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="86bad-214">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="86bad-214">What's changed</span></span>
* <span data-ttu-id="86bad-215">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="86bad-215">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[centre de développement Python]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[documentation]:../cosmos-db/table-storage-how-to-use-python.md
[Comment tooUse hello Service de stockage de Table à partir de Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK pour .NET]: http://azure.microsoft.com/downloads/
[outils Python pour Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[2.2 des outils Python pour Visual Studio exemples VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentation relative à Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Documentation relative à Bottle]: http://bottlepy.org/docs/dev/index.html
[Débogage à distance sur Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projets web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projets de service cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Storage]: http://azure.microsoft.com/documentation/services/storage/
[Kit de développement logiciel (SDK) Azure pour Python]: https://github.com/Azure/azure-sdk-for-python
