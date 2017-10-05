---
title: "Déplacer des données – Passerelle de gestion des données | Microsoft Docs"
description: "Mettez en place une passerelle de données pour déplacer vos données entre un emplacement local et le cloud. Utilisez la passerelle de gestion des données dans Azure Data Factory pour déplacer vos données."
keywords: "passerelle de données, intégration de données, déplacer des données, informations d’identification de passerelle"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 565091e24a8c0009793e2e2365fb95013cad5028
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-between-on-premises-sources-and-the-cloud-with-data-management-gateway"></a><span data-ttu-id="8ccf7-105">Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données</span><span class="sxs-lookup"><span data-stu-id="8ccf7-105">Move data between on-premises sources and the cloud with Data Management Gateway</span></span>
<span data-ttu-id="8ccf7-106">Cet article présente l’intégration des données entre les magasins de données locaux et les magasins de données cloud à l’aide de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="8ccf7-107">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md) et d’autres articles sur les principaux concepts Data Factory : les [jeux de données](data-factory-create-datasets.md) et les [pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="8ccf7-108">Passerelle de gestion de données</span><span class="sxs-lookup"><span data-stu-id="8ccf7-108">Data Management Gateway</span></span>
<span data-ttu-id="8ccf7-109">Vous devez installer la passerelle de gestion des données sur votre ordinateur local pour activer le déplacement des données vers/depuis un magasin de données local.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-109">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="8ccf7-110">La passerelle peut être installée sur le même ordinateur que le magasin de données ou sur un autre ordinateur, pourvu qu’elle puisse se connecter au magasin de données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-110">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ccf7-111">Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour obtenir des informations détaillées sur la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="8ccf7-112">La procédure pas à pas suivante explique comment créer une fabrique de données avec un pipeline qui déplace les données d’une base de données **SQL Server** locale vers un Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-112">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span></span> <span data-ttu-id="8ccf7-113">Dans le cadre de la procédure pas à pas, vous installez et configurez la passerelle de gestion des données sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-113">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-to-cloud"></a><span data-ttu-id="8ccf7-114">Procédure pas à pas : copier des données locales vers le cloud</span><span class="sxs-lookup"><span data-stu-id="8ccf7-114">Walkthrough: copy on-premises data to cloud</span></span>
<span data-ttu-id="8ccf7-115">Dans cette procédure pas à pas, vous effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-115">In this walkthrough you do the following steps:</span></span> 

1. <span data-ttu-id="8ccf7-116">Créer une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-116">Create a data factory.</span></span>
2. <span data-ttu-id="8ccf7-117">Créer une passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="8ccf7-118">Créer des services liés pour les magasins de données des sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="8ccf7-119">Créer des jeux de données pour représenter les données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-119">Create datasets to represent input and output data.</span></span>
5. <span data-ttu-id="8ccf7-120">Créer un pipeline avec une activité de copie pour déplacer les données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-120">Create a pipeline with a copy activity to move the data.</span></span>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="8ccf7-121">Configuration requise pour le didacticiel</span><span class="sxs-lookup"><span data-stu-id="8ccf7-121">Prerequisites for the tutorial</span></span>
<span data-ttu-id="8ccf7-122">Avant de commencer ce guide, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-122">Before you begin this walkthrough, you must have the following prerequisites:</span></span>

* <span data-ttu-id="8ccf7-123">**Abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-123">**Azure subscription**.</span></span>  <span data-ttu-id="8ccf7-124">Si vous n'êtes pas abonné, vous pouvez créer un compte d'essai gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8ccf7-125">Consultez l'article [Essai gratuit](http://azure.microsoft.com/pricing/free-trial/) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-125">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="8ccf7-126">**Compte Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-126">**Azure Storage Account**.</span></span> <span data-ttu-id="8ccf7-127">Dans le cadre de ce didacticiel, le stockage d’objets blob est utilisé comme magasin de données **destination/réception**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-127">You use the blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="8ccf7-128">Si vous n’avez pas de compte de stockage Azure, consultez l’article [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) pour découvrir comment en créer un.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-128">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="8ccf7-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-129">**SQL Server**.</span></span> <span data-ttu-id="8ccf7-130">Dans le cadre de ce didacticiel, vous utilisez une base de données SQL Server locale comme magasin de données **source**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="8ccf7-131">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="8ccf7-131">Create data factory</span></span>
<span data-ttu-id="8ccf7-132">Dans cette étape, vous allez utiliser le portail Azure pour créer une instance Azure Data Factory nommée **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-132">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="8ccf7-133">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-133">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8ccf7-134">Cliquez sur **+ NOUVEAU**, **Intelligence + analyse**, puis **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Nouveau -> DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="8ccf7-136">Dans la page **Nouvelle fabrique de données**, dans le champ Nom, entrez **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-136">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span></span>

    ![Ajouter au Tableau d'accueil](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="8ccf7-138">Le nom de la fabrique de données Azure doit être un nom global unique.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-138">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="8ccf7-139">Si l'erreur suivante s'affiche : **Le nom de la fabrique de données « ADFTutorialOnPremDF » n'est pas disponible**, changez le nom de la fabrique de données (par exemple, votrenomADFTutorialOnPremDF), puis essayez de la recréer.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-139">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="8ccf7-140">Utilisez ce nom à la place d'ADFTutorialOnPremDF quand vous effectuez les étapes restantes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="8ccf7-141">Le nom de la fabrique de données pourra être enregistré en tant que nom **DNS** et devenir ainsi visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-141">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="8ccf7-142">Sélectionnez l’ **abonnement Azure** où vous voulez que la fabrique de données soit créée.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-142">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="8ccf7-143">Sélectionnez un **groupe de ressources** existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="8ccf7-144">Pour les besoins de ce didacticiel, créez un groupe de ressources nommé **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-144">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="8ccf7-145">Cliquez sur **Créer** dans la page **Nouvelle fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-145">Click **Create** on the **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="8ccf7-146">Pour créer des instances Data Factory, vous devez avoir un rôle de [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) au niveau de l’abonnement/du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="8ccf7-147">Une fois la création terminée, la page **Data Factory** s’affiche comme sur l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-147">After creation is complete, you see the **Data Factory** page as shown in the following image:</span></span>

   ![Page d’accueil Data Factory](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="8ccf7-149">Créer une passerelle</span><span class="sxs-lookup"><span data-stu-id="8ccf7-149">Create gateway</span></span>
1. <span data-ttu-id="8ccf7-150">Dans la page **Data Factory**, cliquez sur la vignette **Créer et déployer** pour lancer l’**éditeur** de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-150">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>

    ![Vignette Créer et déployer](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="8ccf7-152">Dans Data Factory Editor, dans la barre d’outils, cliquez sur **... Plus**, puis cliquez sur **Nouvelle passerelle de données**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-152">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="8ccf7-153">Vous pouvez également cliquer avec le bouton droit sur **Passerelles de données** dans l’arborescence, puis cliquer sur **Nouvelle passerelle de données**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-153">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span></span>

   ![Nouvelle passerelle de données sur la barre d’outils](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="8ccf7-155">Dans la page **Créer**, entrez **adftutorialgateway** dans le champ **Nom**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-155">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span></span>     

    ![Page Créer une passerelle](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="8ccf7-157">Dans cette procédure pas à pas, vous créez la passerelle logique avec un seul nœud (ordinateur Windows local).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-157">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="8ccf7-158">Vous pouvez augmenter le nombre des instances d’une passerelle de gestion des données en associant plusieurs machines locales avec la passerelle.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-158">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="8ccf7-159">Vous pouvez monter en puissance une passerelle en augmentant le nombre de travaux de déplacement des données qui peuvent s’exécuter simultanément sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="8ccf7-160">Cette fonctionnalité est également disponible pour une passerelle logique à nœud unique.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="8ccf7-161">Consultez l’article [Mise à l’échelle de la passerelle de gestion des données dans Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="8ccf7-162">Dans la page **Configurer**, cliquez sur **Installer directement sur cet ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-162">In the **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="8ccf7-163">Cette action télécharge le package d’installation de la passerelle, installe, configure et inscrit la passerelle sur l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-163">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="8ccf7-164">Utilisez Internet Explorer ou un navigateur web compatible Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="8ccf7-165">Si vous utilisez Chrome, accédez au [Chrome Web Store](https://chrome.google.com/webstore/), faites une recherche sur le mot-clé « ClickOnce », choisissez l’une des extensions ClickOnce, puis installez-la.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-165">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="8ccf7-166">Faites de même pour Firefox (installez un complément).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-166">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="8ccf7-167">Cliquez sur le bouton **Ouvrir le menu** dans la barre d’outils (**trois lignes horizontales** en haut à droite), cliquez sur **Modules complémentaires**, effectuez une recherche avec le mot-clé « ClickOnce », choisissez l’une des extensions de ClickOnce et installez le programme.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-167">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Passerelle - Page Configurer](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="8ccf7-169">Il s’agit de la méthode la plus simple (un clic) pour télécharger, installer, configurer et inscrire la passerelle en une seule étape.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-169">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span></span> <span data-ttu-id="8ccf7-170">Vous pouvez voir que l’application **Gestionnaire de configuration de la passerelle de gestion de données Microsoft** est installée sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-170">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="8ccf7-171">Vous pouvez également trouver l’exécutable **ConfigManager.exe** dans le dossier suivant : **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-171">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="8ccf7-172">Vous pouvez également télécharger et installer manuellement la passerelle en utilisant les liens de cette page et l’inscrire à l’aide de la clé indiquée dans la zone de texte **NOUVELLE CLÉ**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-172">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span></span>

    <span data-ttu-id="8ccf7-173">Consultez l’article [Data Management Gateway](data-factory-data-management-gateway.md) (Passerelle de gestion des données) pour obtenir des informations détaillées sur la passerelle.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8ccf7-174">Vous devez être administrateur sur l’ordinateur local pour pouvoir installer et configurer la passerelle de gestion des données avec succès.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-174">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span></span> <span data-ttu-id="8ccf7-175">Vous pouvez ajouter des utilisateurs supplémentaires au groupe Windows local **Utilisateurs de la passerelle de gestion des données** .</span><span class="sxs-lookup"><span data-stu-id="8ccf7-175">You can add additional users to the **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="8ccf7-176">Les membres de ce groupe peuvent utiliser l’outil Gestionnaire de configuration de la passerelle de gestion des données pour configurer la passerelle.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-176">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span></span>
   >
   >
5. <span data-ttu-id="8ccf7-177">Attendez quelques minutes, ou patientez jusqu’à ce que le message de notification suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-177">Wait for a couple of minutes or wait until you see the following notification message:</span></span>

    ![Gateway installation successful (Installation réussie de la passerelle)](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="8ccf7-179">Lancez l’application **Gestionnaire de configuration de passerelle de gestion des données** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="8ccf7-180">Dans la fenêtre **Rechercher**, saisissez **passerelle de gestion de données** pour accéder à cet utilitaire.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-180">In the **Search** window, type **Data Management Gateway** to access this utility.</span></span> <span data-ttu-id="8ccf7-181">Vous pouvez également trouver l’exécutable **ConfigManager.exe** dans le dossier suivant : **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="8ccf7-181">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Gestionnaire de configuration de la passerelle](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="8ccf7-183">Vérifiez que le message `adftutorialgateway is connected to the cloud service` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-183">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span></span> <span data-ttu-id="8ccf7-184">La barre d’état située au bas de l’écran affiche le message **Connecté au service de cloud** accompagné d’une **coche verte**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-184">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="8ccf7-185">Sous l’onglet **Accueil**, vous pouvez également effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-185">On the **Home** tab, you can also do the following operations:</span></span>

   * <span data-ttu-id="8ccf7-186">**Inscrire** une passerelle avec une clé obtenue à partir du portail Azure en utilisant le bouton Inscrire.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-186">**Register** a gateway with a key from the Azure portal by using the Register button.</span></span>
   * <span data-ttu-id="8ccf7-187">**Arrêter** le service hôte de la passerelle de gestion des données en cours d’exécution sur la machine passerelle.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-187">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="8ccf7-188">**Planifier des mises à jour** à installer à une heure spécifique de la journée.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-188">**Schedule updates** to be installed at a specific time of the day.</span></span>
   * <span data-ttu-id="8ccf7-189">Voir l’heure de **dernière mise à jour** de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-189">View when the gateway was **last updated**.</span></span>
   * <span data-ttu-id="8ccf7-190">Spécifier l’heure à laquelle une mise à jour de la passerelle peut être installée.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-190">Specify time at which an update to the gateway can be installed.</span></span>
8. <span data-ttu-id="8ccf7-191">Basculez vers l’onglet **Paramètres** . Le certificat spécifié dans la section **Certificat** est utilisé pour chiffrer/déchiffrer les informations d’identification du magasin de données local que vous fournissez dans le portail (facultatif).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-191">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span></span> <span data-ttu-id="8ccf7-192">Cliquez sur **Modifier** pour utiliser votre propre certificat à la place.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-192">(optional) Click **Change** to use your own certificate instead.</span></span> <span data-ttu-id="8ccf7-193">Par défaut, la passerelle utilise le certificat généré automatiquement par le service Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-193">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span></span>

    ![Configuration de certificat de la passerelle](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="8ccf7-195">Vous pouvez également effectuer les actions suivantes sous l’onglet **Paramètres**:</span><span class="sxs-lookup"><span data-stu-id="8ccf7-195">You can also do the following actions on the **Settings** tab:</span></span>

   * <span data-ttu-id="8ccf7-196">Afficher ou exporter le certificat utilisé par la passerelle.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-196">View or export the certificate being used by the gateway.</span></span>
   * <span data-ttu-id="8ccf7-197">Modifier le point de terminaison HTTPS utilisé par la passerelle.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-197">Change the HTTPS endpoint used by the gateway.</span></span>    
   * <span data-ttu-id="8ccf7-198">Définir un proxy HTTP que la passerelle peut utiliser.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-198">Set an HTTP proxy to be used by the gateway.</span></span>     
9. <span data-ttu-id="8ccf7-199">(facultatif) Basculez sur l’onglet **Diagnostics**, et cochez l’option **Activer la journalisation détaillée** si vous souhaitez activer la journalisation détaillée à utiliser pour résoudre les problèmes de passerelle.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-199">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span></span> <span data-ttu-id="8ccf7-200">Vous trouverez les informations de journalisation dans **l’Observateur d’événements** sous le nœud **Journaux des applications et des services** -> **Passerelle de gestion des données**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-200">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Onglet Diagnostic](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="8ccf7-202">Vous pouvez également effectuer les actions suivantes dans l’onglet **Diagnostics** :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-202">You can also perform the following actions in the **Diagnostics** tab:</span></span>

   * <span data-ttu-id="8ccf7-203">Utilisez la section **Tester la connexion** à une source de données locale à l’aide de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-203">Use **Test Connection** section to an on-premises data source using the gateway.</span></span>
   * <span data-ttu-id="8ccf7-204">Cliquez sur **Afficher les journaux** pour consulter le journal de la passerelle de gestion des données dans une fenêtre de l’Observateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-204">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="8ccf7-205">Cliquez sur **Envoyer des journaux** pour charger un fichier zip contenant les journaux des sept derniers jours et l’envoyer à Microsoft pour faciliter le dépannage en cas de problèmes.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-205">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="8ccf7-206">Sous l’onglet **Diagnostics**, dans la section **Tester la connexion**, sélectionnez **SqlServer** pour le type de magasin de données, entrez le nom du serveur de base de données et le nom de la base de données, spécifiez le type d’authentification, entrez un nom d’utilisateur et un mot de passe, puis cliquez sur **Tester** pour tester si la passerelle peut se connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-206">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span></span>
11. <span data-ttu-id="8ccf7-207">Basculez vers le navigateur web, puis, dans le **portail Azure**, cliquez sur **OK** dans la page **Configurer**, puis dans la page **Nouvelle passerelle de données**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-207">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span></span>
12. <span data-ttu-id="8ccf7-208">Vous devez voir **adftutorialgateway** sous **Passerelles de données** dans l’arborescence de gauche.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-208">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span></span>  <span data-ttu-id="8ccf7-209">Si vous cliquez dessus, vous devez voir le code JSON associé.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-209">If you click it, you should see the associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="8ccf7-210">Créez des services liés</span><span class="sxs-lookup"><span data-stu-id="8ccf7-210">Create linked services</span></span>
<span data-ttu-id="8ccf7-211">Au cours de cette étape, vous créez deux services liés : **AzureStorageLinkedService** et **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="8ccf7-212">Le service lié **SqlServerLinkedService** associe une base de données SQL Server locale, et le service lié **AzureStorageLinkedService** associe un magasin d’objets blob Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-212">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span></span> <span data-ttu-id="8ccf7-213">Plus loin dans cette procédure pas à pas, vous allez créer un pipeline qui copie les données de la base de données SQL Server locale vers le magasin d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-213">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span></span>

#### <a name="add-a-linked-service-to-an-on-premises-sql-server-database"></a><span data-ttu-id="8ccf7-214">Ajout d’un service lié à une base de données SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="8ccf7-214">Add a linked service to an on-premises SQL Server database</span></span>
1. <span data-ttu-id="8ccf7-215">Dans **Data Factory Editor**, cliquez sur **Nouvelle banque de données** sur la barre d’outils, puis sélectionnez **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-215">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span></span>

   ![Nouveau service lié SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="8ccf7-217">Dans l’**éditeur JSON** à droite, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-217">In the **JSON editor** on the right, do the following steps:</span></span>

   1. <span data-ttu-id="8ccf7-218">Pour **gatewayName**, spécifiez **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-218">For the **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="8ccf7-219">Dans **connectionString**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-219">In the **connectionString**, do the following steps:</span></span>    

      1. <span data-ttu-id="8ccf7-220">Pour **servername**, entrez le nom du serveur qui héberge la base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-220">For **servername**, enter the name of the server that hosts the SQL Server database.</span></span>
      2. <span data-ttu-id="8ccf7-221">Pour **databasename**, entrez le nom de la base de données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-221">For **databasename**, enter the name of the database.</span></span>
      3. <span data-ttu-id="8ccf7-222">Cliquez sur le bouton **Chiffrer** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-222">Click **Encrypt** button on the toolbar.</span></span> <span data-ttu-id="8ccf7-223">L’application Gestionnaire des informations d’identification apparaît.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-223">You see the Credentials Manager application.</span></span>

         ![Application Gestionnaire des informations d’identification](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="8ccf7-225">Dans la boîte de dialogue **Définition des informations d’identification**, spécifiez le type d’authentification, le nom d’utilisateur et le mot de passe, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-225">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="8ccf7-226">Si la connexion est réussie, les informations d’identification chiffrées sont stockées dans le JSON, et la boîte de dialogue se ferme.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-226">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span></span>
      5. <span data-ttu-id="8ccf7-227">Fermez l’onglet de navigateur vide qui a lancé la boîte de dialogue s’il ne se ferme pas automatiquement, puis revenez à l’onglet du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-227">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span></span>

         <span data-ttu-id="8ccf7-228">Sur la machine passerelle, ces informations d’identification sont **chiffrées** à l’aide d’un certificat appartenant au service Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-228">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="8ccf7-229">Si vous préférez utiliser le certificat qui est associé à la passerelle de gestion des données, consultez [Set credentials securely](#set-credentials-and-security)(Configuration des informations d’identification de manière sécurisée).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-229">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="8ccf7-230">Cliquez sur l’option **Déployer** de la barre de commandes pour déployer le service lié SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-230">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span></span> <span data-ttu-id="8ccf7-231">Vous devez voir le service lié dans l’arborescence.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-231">You should see the linked service in the tree view.</span></span>

      ![Service lié SQL Server dans l’arborescence](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="8ccf7-233">Ajout d’un service lié pour un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8ccf7-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="8ccf7-234">Dans **Data Factory Editor**, dans la barre de commandes, cliquez sur **Nouvelle banque de données**, puis sur **Stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-234">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="8ccf7-235">Entrez le nom de votre compte de stockage Azure dans le champ **Nom du compte**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-235">Enter the name of your Azure storage account for the **Account name**.</span></span>
3. <span data-ttu-id="8ccf7-236">Entrez la clé de votre compte de stockage Azure dans le champ **Clé du compte**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-236">Enter the key for your Azure storage account for the **Account key**.</span></span>
4. <span data-ttu-id="8ccf7-237">Cliquez sur **Déployer** pour déployer le service lié **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-237">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="8ccf7-238">Créez les jeux de données</span><span class="sxs-lookup"><span data-stu-id="8ccf7-238">Create datasets</span></span>
<span data-ttu-id="8ccf7-239">Dans cette étape, vous allez créer des jeux de données d’entrée et de sortie qui représentent les données d’entrée et de sortie pour l’opération de copie (base de données SQL Server locale = > stockage d’objets blob Azure).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-239">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="8ccf7-240">Avant de créer des jeux de données, procédez comme suit (des étapes détaillées suivent la liste) :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-240">Before creating datasets, do the following steps (detailed steps follows the list):</span></span>

* <span data-ttu-id="8ccf7-241">Créez une table nommée **emp** dans la base de données SQL Server que vous avez ajoutée en tant que service lié à la fabrique de données, puis insérez quelques exemples d’entrées dans la table.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-241">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span></span>
* <span data-ttu-id="8ccf7-242">Créez un conteneur d’objets blobs nommé **adftutorial** dans le compte de stockage d’objets blobs Azure que vous avez ajouté en tant que service associé à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-242">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-the-tutorial"></a><span data-ttu-id="8ccf7-243">Préparation du serveur SQL Server local pour le didacticiel</span><span class="sxs-lookup"><span data-stu-id="8ccf7-243">Prepare On-premises SQL Server for the tutorial</span></span>
1. <span data-ttu-id="8ccf7-244">Dans la base de données que vous avez spécifiée pour le service lié SQL Server local (**SqlServerLinkedService**), utilisez le script SQL suivant pour créer la table **emp** dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-244">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="8ccf7-245">Insérer des exemples dans la table :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-245">Insert some sample into the table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="8ccf7-246">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="8ccf7-246">Create input dataset</span></span>

1. <span data-ttu-id="8ccf7-247">Dans **Data Factory Editor**, cliquez sur **... Plus**, dans la barre de commande, cliquez sur **Nouveau jeu de données**, puis sur **Table SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-247">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="8ccf7-248">Remplacez le code JSON du volet droit par le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-248">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="8ccf7-249">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-249">Note the following points:</span></span>

   * <span data-ttu-id="8ccf7-250">Le **type** est défini sur **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-250">**type** is set to **SqlServerTable**.</span></span>
   * <span data-ttu-id="8ccf7-251">**tableName** est défini sur **emp**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-251">**tableName** is set to **emp**.</span></span>
   * <span data-ttu-id="8ccf7-252">Le paramètre **linkedServiceName** est défini sur **SqlServerLinkedService** (vous avez créé ce service lié précédemment dans le cadre de la procédure pas à pas).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-252">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="8ccf7-253">Pour un jeu de données d’entrée non généré par un autre pipeline dans Azure Data Factory, vous devez définir **external** sur **true**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span></span> <span data-ttu-id="8ccf7-254">Cela signifie que les données d’entrée sont produites à l’extérieur du service Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-254">It denotes the input data is produced external to the Azure Data Factory service.</span></span> <span data-ttu-id="8ccf7-255">Vous pouvez éventuellement spécifier des stratégies de données externes à l’aide de l’élément **externalData** dans la section **Policy**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-255">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span></span>    

   <span data-ttu-id="8ccf7-256">Pour plus de détails sur les propriétés JSON, voir [Déplacer des données vers/à partir SQL Server](data-factory-sqlserver-connector.md).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="8ccf7-257">Cliquez sur **Déployer** dans la barre de commandes pour déployer le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-257">Click **Deploy** on the command bar to deploy the dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="8ccf7-258">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="8ccf7-258">Create output dataset</span></span>

1. <span data-ttu-id="8ccf7-259">Dans **Data Factory Editor**, cliquez sur **Nouveau jeu de données** dans la barre de commandes, puis sur **Stockage Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-259">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="8ccf7-260">Remplacez le code JSON du volet droit par le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-260">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="8ccf7-261">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-261">Note the following points:</span></span>

   * <span data-ttu-id="8ccf7-262">**type** est défini sur **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-262">**type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="8ccf7-263">Le paramètre **linkedServiceName** est défini sur **AzureStorageLinkedService** (que vous avez créé à l’étape 2).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-263">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="8ccf7-264">Le paramètre **folderPath** est défini sur **adftutorial/outfromonpremdf**, où « outfromonpremdf » est le dossier dans le conteneur adftutorial.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-264">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span></span> <span data-ttu-id="8ccf7-265">S’il n’existe pas déjà, créez le conteneur **adftutorial** .</span><span class="sxs-lookup"><span data-stu-id="8ccf7-265">Create the **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="8ccf7-266">**availability** est défini sur **hourly** (**frequency** a la valeur **hour** et **interval** est défini sur **1**).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-266">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="8ccf7-267">Le service Data Factory génère une tranche de données de sortie toutes les heures dans la table **emp** de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-267">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span></span>

   <span data-ttu-id="8ccf7-268">Si vous ne spécifiez pas de **fileName** pour une **table de sortie**, les fichiers générés dans le **folderPath** sont nommés selon le format suivant : Data<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-268">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="8ccf7-269">Pour affecter une valeur à **folderPath** et **fileName** de manière dynamique en fonction de l’heure de **SliceStart**, utilisez la propriété partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-269">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span></span> <span data-ttu-id="8ccf7-270">Dans l’exemple suivant, folderPath utilise les valeurs Year, Month et Day à partir de SliceStart (heure de début de la partie en cours de traitement), alors que fileName utilise la valeur Hour à partir de SliceStart.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-270">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="8ccf7-271">Par exemple, si une partie est produite pour 2014-10-20T08:00:00, la valeur folderName est wikidatagateway/wikisampledataout/2014/10/20, alors que la valeur de fileName est 08.csv.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-271">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="8ccf7-272">Pour plus de détails sur les propriétés JSON, voir [Déplacer des données vers/à partir de Stockage Blob Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="8ccf7-273">Cliquez sur **Déployer** dans la barre de commandes pour déployer le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-273">Click **Deploy** on the command bar to deploy the dataset.</span></span> <span data-ttu-id="8ccf7-274">Vérifiez que les jeux de données s’affichent dans l’arborescence.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-274">Confirm that you see both the datasets in the tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="8ccf7-275">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="8ccf7-275">Create pipeline</span></span>
<span data-ttu-id="8ccf7-276">Dans cette étape, vous créez un **pipeline** avec une **activité Copier l’activité** qui utilise **EmpOnPremSQLTable** en tant qu’entrée et **OutputBlobTable** en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="8ccf7-277">Dans Data Factory Editor, cliquez sur **... Plus**, puis sur **Nouveau pipeline**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="8ccf7-278">Remplacez le code JSON du volet droit par le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-278">Replace the JSON in the right pane with the following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL to Azure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server to blob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="8ccf7-279">Remplacez la valeur de la propriété **start** par le jour actuel et la valeur **end** par le jour suivant.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-279">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span>
   >
   >

   <span data-ttu-id="8ccf7-280">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-280">Note the following points:</span></span>

   * <span data-ttu-id="8ccf7-281">Dans la section des activités, toutes les activités ont le **type** **Copy**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-281">In the activities section, there is only activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="8ccf7-282">**L’entrée** de l’activité est définie sur **EmpOnPremSQLTable** et la **sortie** de l’activité, sur **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-282">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span></span>
   * <span data-ttu-id="8ccf7-283">Dans la section **typeProperties**, **SqlSource** est spécifié en tant que **Type de source** et **BlobSink **, en tant que **Type de récepteur**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-283">In the **typeProperties** section, **SqlSource** is specified as the **source type** and **BlobSink **is specified as the **sink type**.</span></span>
   * <span data-ttu-id="8ccf7-284">La requête SQL `select * from emp` est spécifiée pour la propriété **sqlReaderQuery** de **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-284">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="8ccf7-285">Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="8ccf7-286">Par exemple : 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="8ccf7-287">L’heure de fin ( **end** ) est facultative, mais nous allons l’utiliser dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-287">The **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="8ccf7-288">Si vous ne spécifiez aucune valeur pour la propriété **end**, cette dernière est calculée comme suit : « **start + 48 heures** ».</span><span class="sxs-lookup"><span data-stu-id="8ccf7-288">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="8ccf7-289">Pour exécuter le pipeline indéfiniment, spécifiez **9/9/9999** comme valeur pour la propriété **end**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-289">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="8ccf7-290">Vous définissez la durée pendant laquelle les tranches de données seront traitées en fonction des propriétés de **Disponibilité** définies pour chaque jeu de données Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-290">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="8ccf7-291">Dans l’exemple ci-dessus, il existe 24 tranches de données, car une tranche est générée par heure.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-291">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="8ccf7-292">Cliquez sur l’option **Déployer** de la barre de commandes pour déployer le jeu de données (la table est un jeu de données rectangulaire).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-292">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="8ccf7-293">Vérifiez que le pipeline s’affiche dans l’arborescence sous le nœud **Pipelines**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-293">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="8ccf7-294">Maintenant, cliquez sur **X** à deux reprises pour fermer la page et revenir à la page **Data Factory** pour **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-294">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="8ccf7-295">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="8ccf7-295">**Congratulations!**</span></span> <span data-ttu-id="8ccf7-296">Vous avez correctement créé une fabrique de données Azure, des services liés, des jeux de données et un pipeline, et planifié le pipeline.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span></span>

#### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="8ccf7-297">Afficher une vue schématique d'une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="8ccf7-297">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="8ccf7-298">Dans le **portail Azure**, cliquez sur la vignette **Diagramme** sur la page d’accueil de la fabrique de données **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-298">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="8ccf7-299">:</span><span class="sxs-lookup"><span data-stu-id="8ccf7-299">:</span></span>

    ![Lien Diagramme](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="8ccf7-301">Le diagramme devrait ressembler à l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="8ccf7-301">You should see the diagram similar to the following image:</span></span>

    ![Vue du diagramme](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="8ccf7-303">Vous pouvez faire un zoom avant, un zoom arrière, un zoom à 100 %, un zoom pour ajuster, positionner automatiquement les pipelines et les jeux de données, et afficher les informations de lignage (mise en surbrillance des éléments en amont et en aval des éléments sélectionnés).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-303">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="8ccf7-304">Vous pouvez double-cliquer sur un objet (jeu de données d’entrée/de sortie) pour afficher ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-304">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="8ccf7-305">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="8ccf7-305">Monitor pipeline</span></span>
<span data-ttu-id="8ccf7-306">Dans cette étape, vous utilisez le portail Azure pour surveiller ce qui se passe dans une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-306">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="8ccf7-307">Vous pouvez également utiliser les applets de commande PowerShell pour surveiller les jeux de données et les pipelines.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-307">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span></span> <span data-ttu-id="8ccf7-308">Pour plus de détails sur la surveillance, consultez [Surveillance et gestion des pipelines](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="8ccf7-309">Dans le diagramme, double-cliquez sur **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-309">In the diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Tranches EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="8ccf7-311">Notez que toutes les tranches de données sont dans l’état **Prêt** parce que la durée du pipeline (de l’heure de début à l’heure de fin) s’inscrit dans le passé.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-311">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span></span> <span data-ttu-id="8ccf7-312">Cela est dû au fait que vous avez inséré les données dans la base de données SQL Server et qu’elles y sont tout le temps.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-312">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span></span> <span data-ttu-id="8ccf7-313">Vérifiez qu’aucune tranche n’apparaît dans la section **Tranches problématiques** , sur la partie inférieure de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-313">Confirm that no slices show up in the **Problem slices** section at the bottom.</span></span> <span data-ttu-id="8ccf7-314">Pour afficher toutes les tranches, cliquez sur **Afficher plus** en bas de la liste des tranches.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-314">To view all the slices, click **See More** at the bottom of the list of slices.</span></span>
3. <span data-ttu-id="8ccf7-315">À présent, dans la page **Jeux de données**, cliquez sur **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-315">Now, In the **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Tranches OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="8ccf7-317">Cliquez sur une tranche de données dans la liste pour afficher la page **Tranche de données**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-317">Click any data slice from the list and you should see the **Data Slice** page.</span></span> <span data-ttu-id="8ccf7-318">Les activités exécutées pour cette tranche s’affichent.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-318">You see activity runs for the slice.</span></span> <span data-ttu-id="8ccf7-319">Généralement, une seule activité exécutée s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-319">You see only one activity run usually.</span></span>  

    ![Panneau Tranche de données](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="8ccf7-321">Si la tranche n’a pas l’état **Prêt**, vous pouvez voir les tranches en amont qui ne sont pas prêtes et qui empêchent l’exécution de la tranche actuelle dans la liste **Tranches en amont qui ne sont pas prêtes**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-321">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="8ccf7-322">Cliquez sur **l’exécution d’activité** dans la liste de la partie inférieure de la fenêtre pour afficher les **détails sur l’exécution d’activité**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-322">Click the **activity run** from the list at the bottom to see **activity run details**.</span></span>

   ![Page Détails de l’exécution d’activité](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="8ccf7-324">Vous devriez voir des informations telles que le débit, la durée et la passerelle utilisée pour transférer les données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-324">You would see information such as throughput, duration, and the gateway used to transfer the data.</span></span>
6. <span data-ttu-id="8ccf7-325">Cliquez sur **X** pour fermer toutes les pages jusqu’à ce que vous</span><span class="sxs-lookup"><span data-stu-id="8ccf7-325">Click **X** to close all the pages until you</span></span>
7. <span data-ttu-id="8ccf7-326">reveniez à la page d’accueil de l’élément **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-326">get back to the home page for the **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="8ccf7-327">(facultatif) Cliquez sur **Pipelines**, sur **ADFTutorialOnPremDF**, puis accédez aux tables d’entrée (**Consommé**) ou aux jeux de données de sortie (**Produit**).</span><span class="sxs-lookup"><span data-stu-id="8ccf7-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="8ccf7-328">Utilisez des outils tels que [Microsoft Storage Explorer](http://storageexplorer.com/) pour vérifier qu’un objet blob/fichier est créé pour chaque heure.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span></span>

   ![Explorateur de stockage Azure](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="8ccf7-330">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ccf7-330">Next steps</span></span>
* <span data-ttu-id="8ccf7-331">Consultez l’article [Data Management Gateway](data-factory-data-management-gateway.md) (Passerelle de gestion des données) pour obtenir des informations détaillées sur la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span></span>
* <span data-ttu-id="8ccf7-332">Consultez l’article [Copie de données d’un objet blob vers Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour en savoir plus sur l’utilisation de l’activité de copie pour déplacer des données d’une banque de données source vers une banque de données récepteur.</span><span class="sxs-lookup"><span data-stu-id="8ccf7-332">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span></span>
