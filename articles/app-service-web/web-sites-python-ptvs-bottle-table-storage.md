---
title: "Bottle et stockage de tables Azure sur Azure avec Python Tools 2.2 pour Visual Studio"
description: "Découvrez comment utiliser Python Tools pour Visual Studio afin de créer une application Bottle qui stocke les données dans le stockage de tables Azure et déployer l’application web dans Azure App Service Web Apps."
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
ms.openlocfilehash: fb25f03607ac6e9af46b47f54e830e0283dd1b0a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="ec792-103">Bottle et stockage de tables Azure sur Azure avec Python Tools 2.2 pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ec792-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="ec792-104">Dans ce didacticiel, nous allons utiliser [Python Tools pour Visual Studio] afin de créer une application web de sondage simple, à l’aide de l’un des exemples de modèle PTVS.</span><span class="sxs-lookup"><span data-stu-id="ec792-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="ec792-105">Ce didacticiel est également disponible en [vidéo](https://www.youtube.com/watch?v=GJXDGaEPy94).</span><span class="sxs-lookup"><span data-stu-id="ec792-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="ec792-106">L’application web de sondage définit une abstraction pour son référentiel, ce qui vous permet de basculer facilement d’un type de référentiel à un autre (In-Memory, Azure Table Storage, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="ec792-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="ec792-107">Nous allons découvrir comment créer un compte Azure Storage, comment configurer l’application web pour utiliser le stockage de tables Azure et comment publier l’application web sur un [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ec792-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="ec792-108">Visitez le [Centre de développement Python] pour consulter d’autres articles sur le développement d’applications Azure App Service Web Apps avec PTVS à l’aide des infrastructures web Bottle, Flask et Django, ainsi que des services MongoDB, Azure Table Storage, MySQL et Base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="ec792-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="ec792-109">Cet article concerne App Service, mais les étapes sont similaires lorsque vous développez pour [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="ec792-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec792-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ec792-110">Prerequisites</span></span>
* <span data-ttu-id="ec792-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ec792-111">Visual Studio 2015</span></span>
* <span data-ttu-id="ec792-112">[Python Tools 2.2 pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="ec792-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="ec792-113">[Python Tools 2.2 pour Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="ec792-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="ec792-114">[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="ec792-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="ec792-115">[Python 2.7 32 bits] ou [Python 3.4 32 bits]</span><span class="sxs-lookup"><span data-stu-id="ec792-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="ec792-116">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="ec792-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ec792-117">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="ec792-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="ec792-118">Création du projet</span><span class="sxs-lookup"><span data-stu-id="ec792-118">Create the Project</span></span>
<span data-ttu-id="ec792-119">Dans cette section, nous allons créer un projet Visual Studio à l’aide d’un exemple de modèle.</span><span class="sxs-lookup"><span data-stu-id="ec792-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="ec792-120">Nous allons créer un environnement virtuel et installer les packages requis.</span><span class="sxs-lookup"><span data-stu-id="ec792-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="ec792-121">Ensuite, nous allons exécuter l’application localement à l’aide du référentiel In-Memory par défaut.</span><span class="sxs-lookup"><span data-stu-id="ec792-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="ec792-122">Dans Visual Studio, sélectionnez **Fichier**, **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="ec792-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="ec792-123">Les modèles de projet issus de [Python Tools 2.2 pour Visual Studio Samples VSIX] sont disponibles sous **Python**, **Exemples**.</span><span class="sxs-lookup"><span data-stu-id="ec792-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="ec792-124">Sélectionnez **Projet web de sondage Bottle** et cliquez sur OK pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="ec792-124">Select **Polls Bottle Web Project** and click OK to create the project.</span></span>
   
     ![Boîte de dialogue Nouveau projet](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="ec792-126">Vous allez être invité à installer des packages externes.</span><span class="sxs-lookup"><span data-stu-id="ec792-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="ec792-127">Sélectionnez **Installer dans un environnement virtuel**.</span><span class="sxs-lookup"><span data-stu-id="ec792-127">Select **Install into a virtual environment**.</span></span>
   
     ![Boîte de dialogue Packages externes](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="ec792-129">Sélectionnez **Python 2.7** ou **Python 3.4** comme interpréteur de base.</span><span class="sxs-lookup"><span data-stu-id="ec792-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![Boîte de dialogue Ajouter un environnement virtuel](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="ec792-131">Vérifiez que l’application fonctionne en appuyant sur `F5`.</span><span class="sxs-lookup"><span data-stu-id="ec792-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="ec792-132">Par défaut, l’application utilise un référentiel In-Memory qui ne requiert aucune configuration.</span><span class="sxs-lookup"><span data-stu-id="ec792-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="ec792-133">Toutes les données sont perdues à l’arrêt du serveur web.</span><span class="sxs-lookup"><span data-stu-id="ec792-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="ec792-134">Cliquez sur **Créer un exemple de sondage**, puis sur un sondage et un vote.</span><span class="sxs-lookup"><span data-stu-id="ec792-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Navigateur web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="ec792-136">Création d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="ec792-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="ec792-137">Pour utiliser les opérations de stockage, vous avez besoin d’un compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ec792-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="ec792-138">Pour en créer un, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec792-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="ec792-139">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ec792-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ec792-140">Cliquez sur l’icône **Nouveau** en haut à gauche du portail, puis cliquez sur **Données + stockage** > **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="ec792-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="ec792-141">Cliquez sur le bouton **Créer** , puis attribuez un nom unique au compte de stockage et créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="ec792-141">Click the **Create** button, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Création rapide](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="ec792-143">Une fois le compte de stockage créé, le bouton **Notifications** affiche la mention **RÉUSSITE** en vert clignotant et le panneau du compte de stockage s’ouvre pour indiquer qu’il appartient au groupe de ressources créé.</span><span class="sxs-lookup"><span data-stu-id="ec792-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="ec792-144">Cliquez sur la section **Clés d’accès** dans le panneau du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec792-144">Click the **Access keys** part in the storage account's blade.</span></span> <span data-ttu-id="ec792-145">Prenez note du nom du compte et de la clé1.</span><span class="sxs-lookup"><span data-stu-id="ec792-145">Take note of the account name and key1.</span></span>
   
      ![de clés symétriques](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="ec792-147">Nous aurons besoin de ces informations pour configurer votre projet dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="ec792-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="ec792-148">Configurer le projet</span><span class="sxs-lookup"><span data-stu-id="ec792-148">Configure the Project</span></span>
<span data-ttu-id="ec792-149">Dans cette section, nous allons configurer notre application pour utiliser le compte de stockage que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="ec792-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="ec792-150">Ensuite, nous allons exécuter l’application localement.</span><span class="sxs-lookup"><span data-stu-id="ec792-150">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="ec792-151">Dans Visual Studio, cliquez avec le bouton droit sur le nœud de votre projet dans l’Explorateur de solutions, puis sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="ec792-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="ec792-152">Cliquez sur l’onglet **Déboguer** .</span><span class="sxs-lookup"><span data-stu-id="ec792-152">Click on the **Debug** tab.</span></span>
   
     ![Paramètres de débogage du projet](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="ec792-154">Définissez les valeurs des variables d’environnement requises par l’application dans **Déboguer la commande de serveur**, **Environnement**.</span><span class="sxs-lookup"><span data-stu-id="ec792-154">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="ec792-155">Les variables d’environnement sont définies lorsque la commande **Démarrer le débogage**est exécutée.</span><span class="sxs-lookup"><span data-stu-id="ec792-155">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="ec792-156">Si vous voulez que les variables soient définies lorsque la commande **Démarrer sans débogage** est exécutée, indiquez les mêmes valeurs sous **Exécuter la commande de serveur**.</span><span class="sxs-lookup"><span data-stu-id="ec792-156">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="ec792-157">Vous pouvez aussi définir des variables d’environnement à l’aide du Panneau de configuration Windows.</span><span class="sxs-lookup"><span data-stu-id="ec792-157">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="ec792-158">Cette option est la plus appropriée pour éviter de stocker des informations d’identification dans le code source/fichier de projet.</span><span class="sxs-lookup"><span data-stu-id="ec792-158">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="ec792-159">Notez que vous devrez redémarrer Visual Studio pour que les nouvelles variables d’environnement soient disponibles pour l’application.</span><span class="sxs-lookup"><span data-stu-id="ec792-159">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="ec792-160">Le code qui implémente le référentiel du stockage de tables Azure se trouve dans **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="ec792-160">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="ec792-161">Consultez la [documentation] pour plus d’informations sur la manière d’utiliser le service de Table de Python.</span><span class="sxs-lookup"><span data-stu-id="ec792-161">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="ec792-162">Exécutez l’application avec `F5`.</span><span class="sxs-lookup"><span data-stu-id="ec792-162">Run the application with `F5`.</span></span> <span data-ttu-id="ec792-163">Les sondages créés à l’aide de la fonction **Créer un exemple de sondage** et les données soumises par vote sont sérialisés dans le stockage de tables Azure.</span><span class="sxs-lookup"><span data-stu-id="ec792-163">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ec792-164">L'environnement virtuel Python 2.7 peut provoquer un arrêt exceptionnel dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec792-164">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="ec792-165">Appuyez sur `F5` pour continuer à charger le projet web.</span><span class="sxs-lookup"><span data-stu-id="ec792-165">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="ec792-166">Accédez à la page **À propos** pour vérifier que l’application utilise le référentiel **Stockage de tables Azure**.</span><span class="sxs-lookup"><span data-stu-id="ec792-166">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Navigateur web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="ec792-168">Exploration du stockage de tables Azure</span><span class="sxs-lookup"><span data-stu-id="ec792-168">Explore the Azure Table Storage</span></span>
<span data-ttu-id="ec792-169">L’affichage et la modification des tables de stockage sont très faciles dans Visual Studio grâce à Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="ec792-169">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="ec792-170">Dans cette section, nous allons utiliser l’Explorateur de serveurs pour afficher le contenu des tables de l’application de sondage.</span><span class="sxs-lookup"><span data-stu-id="ec792-170">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="ec792-171">Pour cela, les outils Microsoft Azure doivent être installés. Ils sont disponibles dans le [Kit de développement logiciel (SDK) Azure pour .NET].</span><span class="sxs-lookup"><span data-stu-id="ec792-171">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="ec792-172">Ouvrez **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ec792-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="ec792-173">Développez **Comptes de stockage**, votre compte de stockage, puis **Tables**.</span><span class="sxs-lookup"><span data-stu-id="ec792-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="ec792-175">Double-cliquez sur la table **sondages** ou **choix** pour en afficher le contenu dans une fenêtre et ajouter/supprimer/modifier des entités.</span><span class="sxs-lookup"><span data-stu-id="ec792-175">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Résultats de la requête de table](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="ec792-177">Publication de l’application web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ec792-177">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="ec792-178">Le kit de développement logiciel (SDK) Azure .NET offre un moyen simple de déployer votre application web dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ec792-178">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="ec792-179">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le nœud du projet et sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="ec792-179">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![Boîte de dialogue Publier le site Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="ec792-181">Cliquez sur **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="ec792-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="ec792-182">Cliquez sur **Nouveau** pour créer une application web.</span><span class="sxs-lookup"><span data-stu-id="ec792-182">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="ec792-183">Renseignez les champs suivants et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ec792-183">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="ec792-184">**Nom de l’application web**</span><span class="sxs-lookup"><span data-stu-id="ec792-184">**Web App name**</span></span>
   * <span data-ttu-id="ec792-185">**Plan App Service**</span><span class="sxs-lookup"><span data-stu-id="ec792-185">**App Service plan**</span></span>
   * <span data-ttu-id="ec792-186">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="ec792-186">**Resource group**</span></span>
   * <span data-ttu-id="ec792-187">**Région**</span><span class="sxs-lookup"><span data-stu-id="ec792-187">**Region**</span></span>
   * <span data-ttu-id="ec792-188">Dans **Serveur de base de données**, conservez **Aucune base de données**</span><span class="sxs-lookup"><span data-stu-id="ec792-188">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="ec792-189">Acceptez toutes les valeurs par défaut et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="ec792-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="ec792-190">Votre navigateur web ouvre automatiquement l’application web publiée.</span><span class="sxs-lookup"><span data-stu-id="ec792-190">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="ec792-191">Si vous accédez à la page À propos, vous pouvez voir qu’elle utilise le référentiel **en mémoire** et non le référentiel **Stockage de tables Azure**.</span><span class="sxs-lookup"><span data-stu-id="ec792-191">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="ec792-192">En effet, comme les variables d’environnement ne sont pas définies dans l’instance Web Apps d’Azure App Service, l’application utilise les valeurs par défaut spécifiées dans **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="ec792-192">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="ec792-193">Configurer l'instance Web Apps</span><span class="sxs-lookup"><span data-stu-id="ec792-193">Configure the Web Apps instance</span></span>
<span data-ttu-id="ec792-194">Dans cette section, nous allons configurer les variables d’environnement de l’instance Web Apps.</span><span class="sxs-lookup"><span data-stu-id="ec792-194">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="ec792-195">Dans le [portail Azure], ouvrez le panneau de l'application web en cliquant sur **Parcourir** > **App Services** > le nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="ec792-195">In [Azure Portal], open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="ec792-196">Dans le volet de votre application web, cliquez sur **Tous les paramètres**, puis cliquez sur **Paramètres de l'application**.</span><span class="sxs-lookup"><span data-stu-id="ec792-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="ec792-197">Accédez à la section **Paramètres de l’application** et définissez les valeurs **REPOSITORY\_NAME**, **STORAGE\_NAME** et **STORAGE\_KEY** comme décrit dans la section **Configurer le projet** ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ec792-197">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![Paramètres de l’application](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="ec792-199">Cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="ec792-199">Click on **Save**.</span></span> <span data-ttu-id="ec792-200">Une fois que vous avez reçu les notifications confirmant que les modifications ont été appliquées, cliquez sur **Parcourir** à partir du panneau principal de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="ec792-200">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="ec792-201">L’application doit fonctionner comme prévu et utiliser le référentiel **Stockage de tables Azure** .</span><span class="sxs-lookup"><span data-stu-id="ec792-201">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="ec792-202">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="ec792-202">Congratulations!</span></span>
   
     ![Navigateur web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="ec792-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec792-204">Next steps</span></span>
<span data-ttu-id="ec792-205">Suivez ces liens pour en savoir plus sur Python Tools pour Visual Studio, Bottle et le stockage de tables Azure.</span><span class="sxs-lookup"><span data-stu-id="ec792-205">Follow these links to learn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="ec792-206">[Documentation relative à Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="ec792-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="ec792-207">[Projets web]</span><span class="sxs-lookup"><span data-stu-id="ec792-207">[Web Projects]</span></span>
  * <span data-ttu-id="ec792-208">[Projets de service cloud]</span><span class="sxs-lookup"><span data-stu-id="ec792-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="ec792-209">[Débogage à distance sur Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="ec792-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="ec792-210">[Documentation relative à Bottle]</span><span class="sxs-lookup"><span data-stu-id="ec792-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="ec792-211">[Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="ec792-211">[Azure Storage]</span></span>
* <span data-ttu-id="ec792-212">[Kit de développement logiciel (SDK) Azure pour Python]</span><span class="sxs-lookup"><span data-stu-id="ec792-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="ec792-213">[Utilisation du service de stockage de tables de Python]</span><span class="sxs-lookup"><span data-stu-id="ec792-213">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="ec792-214">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="ec792-214">What's changed</span></span>
* <span data-ttu-id="ec792-215">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ec792-215">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centre de développement Python]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[documentation]:../cosmos-db/table-storage-how-to-use-python.md
[Utilisation du service de stockage de tables de Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[portail Azure]: https://portal.azure.com
[Kit de développement logiciel (SDK) Azure pour .NET]: http://azure.microsoft.com/downloads/
[Python Tools pour Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Python Tools 2.2 pour Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
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
