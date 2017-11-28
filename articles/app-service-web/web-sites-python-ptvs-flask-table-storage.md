---
title: "Flask et stockage des tables Azure sur Azure avec Python Tools 2.2 pour Visual Studio"
description: "Découvrez comment utiliser Python Tools pour Visual Studio afin de créer une application Flask qui stocke les données dans le stockage de tables Azure et déployer l’application web dans Azure App Service Web Apps."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 2e1bc8eebd0b67b965cc70ac4b5dfe03c4720ddf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="3d7ab-103">Flask et stockage des tables Azure sur Azure avec Python Tools 2.2 pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3d7ab-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="3d7ab-104">Dans ce didacticiel, nous allons utiliser [Python Tools pour Visual Studio] afin de créer une application web de sondage simple, à l’aide de l’un des exemples de modèle PTVS.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="3d7ab-105">Ce didacticiel est également disponible en [vidéo](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span><span class="sxs-lookup"><span data-stu-id="3d7ab-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="3d7ab-106">L’application web de sondage définit une abstraction pour son référentiel, ce qui vous permet de basculer facilement d’un type de référentiel à un autre (In-Memory, Azure Table Storage, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="3d7ab-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="3d7ab-107">Nous allons découvrir comment créer un compte Azure Storage, comment configurer l’application web pour utiliser le stockage de tables Azure et comment publier l’application web sur un [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="3d7ab-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="3d7ab-108">Visitez le [Centre de développement Python] pour consulter d’autres articles sur le développement d’applications Azure App Service Web Apps avec PTVS à l’aide des infrastructures web Bottle, Flask et Django, ainsi que des services MongoDB, Azure Table Storage, MySQL et Base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="3d7ab-109">Cet article concerne App Service, mais les étapes sont similaires lorsque vous développez pour [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="3d7ab-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d7ab-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3d7ab-110">Prerequisites</span></span>
* <span data-ttu-id="3d7ab-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="3d7ab-111">Visual Studio 2015</span></span>
* <span data-ttu-id="3d7ab-112">[Python Tools 2.2 pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="3d7ab-113">[Python Tools 2.2 pour Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="3d7ab-114">[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="3d7ab-115">[Python 2.7 32 bits] ou [Python 3.4 32 bits]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="3d7ab-116">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3d7ab-117">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="3d7ab-118">Création du projet</span><span class="sxs-lookup"><span data-stu-id="3d7ab-118">Create the Project</span></span>
<span data-ttu-id="3d7ab-119">Dans cette section, nous allons créer un projet Visual Studio à l’aide d’un exemple de modèle.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="3d7ab-120">Nous allons créer un environnement virtuel et installer les packages requis.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="3d7ab-121">Ensuite, nous allons exécuter l’application localement à l’aide du référentiel In-Memory par défaut.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="3d7ab-122">Dans Visual Studio, sélectionnez **Fichier**, **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="3d7ab-123">Les modèles de projet issus de [Python Tools 2.2 pour Visual Studio Samples VSIX] sont disponibles sous **Python**, **Exemples**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="3d7ab-124">Sélectionnez **Projet web de sondage Flask** et cliquez sur OK pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-124">Select **Polls Flask Web Project** and click OK to create the project.</span></span>
   
     ![Boîte de dialogue Nouveau projet](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="3d7ab-126">Vous allez être invité à installer des packages externes.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="3d7ab-127">Sélectionnez **Installer dans un environnement virtuel**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-127">Select **Install into a virtual environment**.</span></span>
   
     ![Boîte de dialogue Packages externes](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="3d7ab-129">Sélectionnez **Python 2.7** ou **Python 3.4** comme interpréteur de base.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![Boîte de dialogue Ajouter un environnement virtuel](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="3d7ab-131">Vérifiez que l’application fonctionne en appuyant sur `F5`.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="3d7ab-132">Par défaut, l’application utilise un référentiel In-Memory qui ne requiert aucune configuration.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="3d7ab-133">Toutes les données sont perdues à l’arrêt du serveur web.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="3d7ab-134">Cliquez sur **Créer un exemple de sondage**, puis sur un sondage et un vote.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Navigateur web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="3d7ab-136">Création d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="3d7ab-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="3d7ab-137">Pour utiliser les opérations de stockage, vous avez besoin d’un compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="3d7ab-138">Pour en créer un, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3d7ab-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="3d7ab-139">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3d7ab-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3d7ab-140">Cliquez sur l’icône **Nouveau** en haut à gauche du portail, puis cliquez sur **Données + stockage** > **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="3d7ab-141">Cliquez sur **Créer**, puis attribuez un nom unique au compte de stockage et créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d7ab-141">Click on **Create**, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Création rapide](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="3d7ab-143">Une fois le compte de stockage créé, le bouton **Notifications** affiche la mention **RÉUSSITE** en vert clignotant et le panneau du compte de stockage s’ouvre pour indiquer qu’il appartient au groupe de ressources créé.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="3d7ab-144">Cliquez sur la section **Clés d’accès** dans le panneau du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-144">Click the **Access Keys** part in the storage account's blade.</span></span> <span data-ttu-id="3d7ab-145">Prenez note du nom du compte et de la clé1.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-145">Take note of the account name and the key1.</span></span>
   
      ![de clés symétriques](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="3d7ab-147">Nous aurons besoin de ces informations pour configurer votre projet dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="3d7ab-148">Configurer le projet</span><span class="sxs-lookup"><span data-stu-id="3d7ab-148">Configure the Project</span></span>
<span data-ttu-id="3d7ab-149">Dans cette section, nous allons configurer notre application pour utiliser le compte de stockage que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="3d7ab-150">Nous allons découvrir comment obtenir des paramètres de connexion à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-150">We'll see how to obtain connection settings from the Azure Portal.</span></span> <span data-ttu-id="3d7ab-151">Ensuite, nous allons exécuter l’application localement.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-151">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="3d7ab-152">Dans Visual Studio, cliquez avec le bouton droit sur le nœud de votre projet dans l’Explorateur de solutions, puis sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="3d7ab-153">Cliquez sur l’onglet **Déboguer** .</span><span class="sxs-lookup"><span data-stu-id="3d7ab-153">Click on the **Debug** tab.</span></span>
   
     ![Paramètres de débogage du projet](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="3d7ab-155">Définissez les valeurs des variables d’environnement requises par l’application dans **Déboguer la commande de serveur**, **Environnement**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-155">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="3d7ab-156">Les variables d’environnement sont définies lorsque la commande **Démarrer le débogage**est exécutée.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-156">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="3d7ab-157">Si vous voulez que les variables soient définies lorsque la commande **Démarrer sans débogage** est exécutée, indiquez les mêmes valeurs sous **Exécuter la commande de serveur**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-157">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="3d7ab-158">Vous pouvez aussi définir des variables d’environnement à l’aide du Panneau de configuration Windows.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-158">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="3d7ab-159">Cette option est la plus appropriée pour éviter de stocker des informations d’identification dans le code source/fichier de projet.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-159">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="3d7ab-160">Notez que vous devrez redémarrer Visual Studio pour que les nouvelles variables d’environnement soient disponibles pour l’application.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-160">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="3d7ab-161">Le code qui implémente le référentiel du stockage de tables Azure se trouve dans **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-161">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="3d7ab-162">Consultez la [documentation] pour plus d’informations sur la manière d’utiliser le service de Table de Python.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-162">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="3d7ab-163">Exécutez l’application avec `F5`.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-163">Run the application with `F5`.</span></span> <span data-ttu-id="3d7ab-164">Les sondages créés à l’aide de la fonction **Créer un exemple de sondage** et les données soumises par vote sont sérialisés dans le stockage de tables Azure.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-164">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3d7ab-165">L'environnement virtuel Python 2.7 peut provoquer un arrêt exceptionnel dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-165">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="3d7ab-166">Appuyez sur `F5` pour continuer à charger le projet web.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-166">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="3d7ab-167">Accédez à la page **À propos** pour vérifier que l’application utilise le référentiel **Stockage de tables Azure**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-167">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Navigateur web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="3d7ab-169">Exploration du stockage de tables Azure</span><span class="sxs-lookup"><span data-stu-id="3d7ab-169">Explore the Azure Table Storage</span></span>
<span data-ttu-id="3d7ab-170">L’affichage et la modification des tables de stockage sont très faciles dans Visual Studio grâce à Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-170">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="3d7ab-171">Dans cette section, nous allons utiliser l’Explorateur de serveurs pour afficher le contenu des tables de l’application de sondage.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-171">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="3d7ab-172">Pour cela, les outils Microsoft Azure doivent être installés. Ils sont disponibles dans le [Kit de développement logiciel (SDK) Azure pour .NET].</span><span class="sxs-lookup"><span data-stu-id="3d7ab-172">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="3d7ab-173">Ouvrez **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="3d7ab-174">Développez **Comptes de stockage**, votre compte de stockage, puis **Tables**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="3d7ab-176">Double-cliquez sur la table **sondages** ou **choix** pour en afficher le contenu dans une fenêtre et ajouter/supprimer/modifier des entités.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-176">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Résultats de la requête de table](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="3d7ab-178">Publication de l’application web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3d7ab-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="3d7ab-179">Le kit de développement logiciel (SDK) Azure .NET offre un moyen simple de déployer votre application web dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-179">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="3d7ab-180">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le nœud du projet et sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![Boîte de dialogue Publier le site Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="3d7ab-182">Cliquez sur **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="3d7ab-183">Cliquez sur **Nouveau** pour créer une application web.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="3d7ab-184">Renseignez les champs suivants et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-184">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="3d7ab-185">**Nom de l’application web**</span><span class="sxs-lookup"><span data-stu-id="3d7ab-185">**Web App name**</span></span>
   * <span data-ttu-id="3d7ab-186">**Plan App Service**</span><span class="sxs-lookup"><span data-stu-id="3d7ab-186">**App Service plan**</span></span>
   * <span data-ttu-id="3d7ab-187">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="3d7ab-187">**Resource group**</span></span>
   * <span data-ttu-id="3d7ab-188">**Région**</span><span class="sxs-lookup"><span data-stu-id="3d7ab-188">**Region**</span></span>
   * <span data-ttu-id="3d7ab-189">Dans **Serveur de base de données**, conservez **Aucune base de données**</span><span class="sxs-lookup"><span data-stu-id="3d7ab-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="3d7ab-190">Acceptez toutes les valeurs par défaut et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="3d7ab-191">Votre navigateur web ouvre automatiquement l’application web publiée.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="3d7ab-192">Si vous accédez à la page À propos, vous pouvez voir qu’elle utilise le référentiel **en mémoire** et non le référentiel **Stockage de tables Azure**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-192">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="3d7ab-193">En effet, comme les variables d’environnement ne sont pas définies dans l’instance Web Apps d’Azure App Service, l’application utilise les valeurs par défaut spécifiées dans **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-193">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="3d7ab-194">Configurer l'instance Web Apps</span><span class="sxs-lookup"><span data-stu-id="3d7ab-194">Configure the Web Apps instance</span></span>
<span data-ttu-id="3d7ab-195">Dans cette section, nous allons configurer les variables d’environnement de l’instance Web Apps.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-195">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="3d7ab-196">Dans le [portail Azure](https://portal.azure.com), ouvrez le panneau de l'application web en cliquant sur **Parcourir** > **App Services** > le nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-196">In [Azure Portal](https://portal.azure.com), open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="3d7ab-197">Dans le volet de votre application web, cliquez sur **Tous les paramètres**, puis cliquez sur **Paramètres de l'application**.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="3d7ab-198">Accédez à la section **Paramètres de l’application** et définissez les valeurs **REPOSITORY\_NAME**, **STORAGE\_NAME** et **STORAGE\_KEY** comme décrit dans la section **Configurer le projet** ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-198">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![Paramètres de l’application](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="3d7ab-200">Cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="3d7ab-200">Click on **Save**.</span></span> <span data-ttu-id="3d7ab-201">Une fois que vous avez reçu les notifications confirmant que les modifications ont été appliquées, cliquez sur **Parcourir** à partir du panneau principal de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-201">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="3d7ab-202">L’application doit fonctionner comme prévu et utiliser le référentiel **Stockage de tables Azure** .</span><span class="sxs-lookup"><span data-stu-id="3d7ab-202">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="3d7ab-203">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="3d7ab-203">Congratulations!</span></span>
   
     ![Navigateur web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="3d7ab-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3d7ab-205">Next steps</span></span>
<span data-ttu-id="3d7ab-206">Suivez ces liens pour en savoir plus sur Python Tools for Visual Studio, Flask et le stockage de tables Azure.</span><span class="sxs-lookup"><span data-stu-id="3d7ab-206">Follow these links to learn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="3d7ab-207">[Documentation relative à Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="3d7ab-208">[Projets web]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-208">[Web Projects]</span></span>
  * <span data-ttu-id="3d7ab-209">[Projets de service cloud]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="3d7ab-210">[Débogage à distance sur Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="3d7ab-211">[Documentation relative à Flask]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-211">[Flask Documentation]</span></span>
* <span data-ttu-id="3d7ab-212">[Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-212">[Azure Storage]</span></span>
* <span data-ttu-id="3d7ab-213">[Kit de développement logiciel (SDK) Azure pour Python]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="3d7ab-214">[Utilisation du service de stockage de tables de Python]</span><span class="sxs-lookup"><span data-stu-id="3d7ab-214">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="3d7ab-215">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="3d7ab-215">What's changed</span></span>
* <span data-ttu-id="3d7ab-216">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="3d7ab-216">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centre de développement Python]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[documentation]:../cosmos-db/table-storage-how-to-use-python.md
[Utilisation du service de stockage de tables de Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Kit de développement logiciel (SDK) Azure pour .NET]: http://azure.microsoft.com/downloads/
[Python Tools pour Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 pour Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentation relative à Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Documentation relative à Flask]: http://flask.pocoo.org/
[Débogage à distance sur Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projets web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projets de service cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Storage]: http://azure.microsoft.com/documentation/services/storage/
[Kit de développement logiciel (SDK) Azure pour Python]: https://github.com/Azure/azure-sdk-for-python
