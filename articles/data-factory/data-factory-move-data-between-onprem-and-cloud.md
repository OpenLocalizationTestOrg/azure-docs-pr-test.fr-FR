---
title: "données aaaMove - passerelle de gestion des données | Documents Microsoft"
description: "Configurer une passerelle de données toomove des données entre locaux et hello cloud. Utiliser la passerelle de gestion des données dans Azure Data Factory toomove vos données."
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
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a><span data-ttu-id="dee1c-105">Déplacement des données entre des sources locales et cloud hello avec la passerelle de gestion des données</span><span class="sxs-lookup"><span data-stu-id="dee1c-105">Move data between on-premises sources and hello cloud with Data Management Gateway</span></span>
<span data-ttu-id="dee1c-106">Cet article présente l’intégration des données entre les magasins de données locaux et les magasins de données cloud à l’aide de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dee1c-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="dee1c-107">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article et autres articles de concepts de base données fabrique : [datasets](data-factory-create-datasets.md) et [pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="dee1c-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="dee1c-108">Passerelle de gestion de données</span><span class="sxs-lookup"><span data-stu-id="dee1c-108">Data Management Gateway</span></span>
<span data-ttu-id="dee1c-109">Vous devez installer la passerelle de gestion des données sur votre tooenable d’ordinateur local déplacement des données vers/à partir d’une banque de données locale.</span><span class="sxs-lookup"><span data-stu-id="dee1c-109">You must install Data Management Gateway on your on-premises machine tooenable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="dee1c-110">passerelle de Hello peut être installé sur le même ordinateur en tant que banque de données hello ou sur un autre ordinateur, tant que passerelle de hello peut se connecter de magasin de données toohello de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-110">hello gateway can be installed on hello same machine as hello data store or on a different machine as long as hello gateway can connect toohello data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dee1c-111">Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour obtenir des informations détaillées sur la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="dee1c-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="dee1c-112">Hello procédure pas à pas suivante vous montre comment toocreate une fabrique de données avec un pipeline qui déplace les données à partir d’un site local **SQL Server** stockage d’objets blob Azure tooan de base de données.</span><span class="sxs-lookup"><span data-stu-id="dee1c-112">hello following walkthrough shows you how toocreate a data factory with a pipeline that moves data from an on-premises **SQL Server** database tooan Azure blob storage.</span></span> <span data-ttu-id="dee1c-113">Dans le cadre de la procédure pas à pas hello, vous installez et configurez hello passerelle de gestion des données sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dee1c-113">As part of hello walkthrough, you install and configure hello Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-toocloud"></a><span data-ttu-id="dee1c-114">Procédure pas à pas : copier toocloud de données locale</span><span class="sxs-lookup"><span data-stu-id="dee1c-114">Walkthrough: copy on-premises data toocloud</span></span>
<span data-ttu-id="dee1c-115">Dans cette procédure pas à pas vous hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dee1c-115">In this walkthrough you do hello following steps:</span></span> 

1. <span data-ttu-id="dee1c-116">Créer une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="dee1c-116">Create a data factory.</span></span>
2. <span data-ttu-id="dee1c-117">Créer une passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="dee1c-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="dee1c-118">Créer des services liés pour les magasins de données des sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="dee1c-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="dee1c-119">Créer des groupes de données toorepresent d’entrée et les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="dee1c-119">Create datasets toorepresent input and output data.</span></span>
5. <span data-ttu-id="dee1c-120">Créer un pipeline comportant des données copie activité toomove hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-120">Create a pipeline with a copy activity toomove hello data.</span></span>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="dee1c-121">Configuration requise pour le didacticiel de hello</span><span class="sxs-lookup"><span data-stu-id="dee1c-121">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="dee1c-122">Avant de commencer cette procédure pas à pas, vous devez disposer de hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="dee1c-122">Before you begin this walkthrough, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="dee1c-123">**Abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-123">**Azure subscription**.</span></span>  <span data-ttu-id="dee1c-124">Si vous n'êtes pas abonné, vous pouvez créer un compte d'essai gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="dee1c-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="dee1c-125">Consultez hello [version d’évaluation gratuite](http://azure.microsoft.com/pricing/free-trial/) article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="dee1c-125">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="dee1c-126">**Compte Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-126">**Azure Storage Account**.</span></span> <span data-ttu-id="dee1c-127">Vous utilisez le stockage d’objets blob hello comme un **destination/récepteur** stocker des données dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="dee1c-127">You use hello blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="dee1c-128">Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) toocreate suit un article.</span><span class="sxs-lookup"><span data-stu-id="dee1c-128">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="dee1c-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-129">**SQL Server**.</span></span> <span data-ttu-id="dee1c-130">Dans le cadre de ce didacticiel, vous utilisez une base de données SQL Server locale comme magasin de données **source**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="dee1c-131">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="dee1c-131">Create data factory</span></span>
<span data-ttu-id="dee1c-132">Dans cette étape, vous utilisez hello Azure toocreate portail une instance d’Azure Data Factory nommée **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-132">In this step, you use hello Azure portal toocreate an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="dee1c-133">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dee1c-133">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dee1c-134">Cliquez sur **+ NOUVEAU**, **Intelligence + analyse**, puis **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Nouveau -> DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="dee1c-136">Bonjour **nouvelle fabrique de données** , entrez **ADFTutorialOnPremDF** pour hello nom.</span><span class="sxs-lookup"><span data-stu-id="dee1c-136">In hello **New data factory** page, enter **ADFTutorialOnPremDF** for hello Name.</span></span>

    ![Ajouter tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="dee1c-138">nom de Hello de fabrique de données Azure hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="dee1c-138">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="dee1c-139">Si vous recevez une erreur de hello : **nom de fabrique de données « ADFTutorialOnPremDF » n’est pas disponible**, de modifier le nom hello hello fabrique de données (par exemple, yournameADFTutorialOnPremDF) et essayez à nouveau de créer.</span><span class="sxs-lookup"><span data-stu-id="dee1c-139">If you receive hello error: **Data factory name “ADFTutorialOnPremDF” is not available**, change hello name of hello data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="dee1c-140">Utilisez ce nom à la place d'ADFTutorialOnPremDF quand vous effectuez les étapes restantes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="dee1c-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="dee1c-141">nom Hello hello fabrique de données peut être enregistré comme un **DNS** nom dans les futures hello et donc devenir visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="dee1c-141">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="dee1c-142">Sélectionnez hello **abonnement Azure** où vous souhaitez toobe de fabrique de données hello créé.</span><span class="sxs-lookup"><span data-stu-id="dee1c-142">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="dee1c-143">Sélectionnez un **groupe de ressources** existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="dee1c-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="dee1c-144">Didacticiel de hello, créer un groupe de ressources nommé : **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-144">For hello tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="dee1c-145">Cliquez sur **créer** sur hello **nouvelle fabrique de données** page.</span><span class="sxs-lookup"><span data-stu-id="dee1c-145">Click **Create** on hello **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="dee1c-146">instances de fabrique de données toocreate, vous devez être membre du hello [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rôle au niveau de groupe de ressource d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="dee1c-147">Une fois la création terminée, vous voyez hello **Data Factory** page comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="dee1c-147">After creation is complete, you see hello **Data Factory** page as shown in hello following image:</span></span>

   ![Page d’accueil Data Factory](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="dee1c-149">Créer une passerelle</span><span class="sxs-lookup"><span data-stu-id="dee1c-149">Create gateway</span></span>
1. <span data-ttu-id="dee1c-150">Bonjour **Data Factory** , cliquez sur **auteur et déployer** vignette toolaunch hello **éditeur** de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-150">In hello **Data Factory** page, click **Author and deploy** tile toolaunch hello **Editor** for hello data factory.</span></span>

    ![Vignette Créer et déployer](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="dee1c-152">Bonjour éditeur Data Factory, cliquez sur **... Plus** sur hello barre d’outils, puis cliquez sur **nouvelle passerelle de données**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-152">In hello Data Factory Editor, click **... More** on hello toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="dee1c-153">Vous pouvez également cliquer sur **passerelles de données** dans hello arborescence, puis cliquez sur **nouvelle passerelle de données**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-153">Alternatively, you can right-click **Data Gateways** in hello tree view, and click **New data gateway**.</span></span>

   ![Nouvelle passerelle de données sur la barre d’outils](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="dee1c-155">Bonjour **créer** , entrez **adftutorialgateway** pour hello **nom**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-155">In hello **Create** page, enter **adftutorialgateway** for hello **name**, and click **OK**.</span></span>     

    ![Page Créer une passerelle](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="dee1c-157">Dans cette procédure pas à pas, vous créez la passerelle de logique hello qu’un seul nœud (ordinateur local, Windows).</span><span class="sxs-lookup"><span data-stu-id="dee1c-157">In this walkthrough, you create hello logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="dee1c-158">Vous pouvez faire évoluer une passerelle de gestion des données en associant plusieurs machines locales de la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-158">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="dee1c-159">Vous pouvez monter en puissance une passerelle en augmentant le nombre de travaux de déplacement des données qui peuvent s’exécuter simultanément sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="dee1c-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="dee1c-160">Cette fonctionnalité est également disponible pour une passerelle logique à nœud unique.</span><span class="sxs-lookup"><span data-stu-id="dee1c-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="dee1c-161">Consultez l’article [Mise à l’échelle de la passerelle de gestion des données dans Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="dee1c-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="dee1c-162">Bonjour **configurer** , cliquez sur **installer directement sur cet ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-162">In hello **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="dee1c-163">Cette action télécharge le package d’installation hello pour la passerelle de hello, installe, configure et enregistre la passerelle hello sur l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-163">This action downloads hello installation package for hello gateway, installs, configures, and registers hello gateway on hello computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="dee1c-164">Utilisez Internet Explorer ou un navigateur web compatible Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="dee1c-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="dee1c-165">Si vous utilisez Chrome, accédez toohello [Boutique Chrome](https://chrome.google.com/webstore/), recherche avec « ClickOnce » (mot clé), choisissez une des extensions de ClickOnce hello et installez-le.</span><span class="sxs-lookup"><span data-stu-id="dee1c-165">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="dee1c-166">Hello même pour Firefox (complément installation).</span><span class="sxs-lookup"><span data-stu-id="dee1c-166">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="dee1c-167">Cliquez sur **ouvrir le Menu** bouton de barre d’outils hello (**trois lignes horizontales** dans l’angle supérieur droit de hello), cliquez sur **modules complémentaires**, recherche avec « ClickOnce » (mot clé), choisissez une des hello Extensions de ClickOnce et l’installer.</span><span class="sxs-lookup"><span data-stu-id="dee1c-167">Click **Open Menu** button on hello toolbar (**three horizontal lines** in hello top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Passerelle - Page Configurer](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="dee1c-169">De cette façon est toodownload (un seul clic) de façon plus simple de hello, installer, configurer et inscrire la passerelle de hello en une seule étape.</span><span class="sxs-lookup"><span data-stu-id="dee1c-169">This way is hello easiest way (one-click) toodownload, install, configure, and register hello gateway in one single step.</span></span> <span data-ttu-id="dee1c-170">Vous pouvez voir hello **Gestionnaire de Configuration de passerelle de gestion de données de Microsoft** application est installée sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dee1c-170">You can see hello **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="dee1c-171">Vous pouvez également trouver hello exécutable **ConfigManager.exe** dans le dossier de hello : **C:\Program Files\Microsoft données Gestion Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-171">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="dee1c-172">Vous pouvez également télécharger et installer manuellement de passerelle à l’aide de liens de hello dans cette page et inscrire à l’aide de la clé de hello Bonjour **nouvelle clé** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="dee1c-172">You can also download and install gateway manually by using hello links in this page and register it using hello key shown in hello **NEW KEY** text box.</span></span>

    <span data-ttu-id="dee1c-173">Consultez [passerelle de gestion des données](data-factory-data-management-gateway.md) de l’article pour tous les hello plus d’informations sur la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dee1c-174">Vous devez être administrateur sur tooinstall d’ordinateur local hello et configurer la passerelle de gestion des données de hello avec succès.</span><span class="sxs-lookup"><span data-stu-id="dee1c-174">You must be an administrator on hello local computer tooinstall and configure hello Data Management Gateway successfully.</span></span> <span data-ttu-id="dee1c-175">Vous pouvez ajouter des utilisateurs supplémentaires toohello **utilisateurs de gestion des données à l’aide de la passerelle** groupe Windows local.</span><span class="sxs-lookup"><span data-stu-id="dee1c-175">You can add additional users toohello **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="dee1c-176">membres de Hello de ce groupe peuvent utiliser passerelle de hello Gestionnaire de Configuration de passerelle de gestion de données outil tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-176">hello members of this group can use hello Data Management Gateway Configuration Manager tool tooconfigure hello gateway.</span></span>
   >
   >
5. <span data-ttu-id="dee1c-177">Attendez quelques minutes, ou patientez jusqu'à ce que vous voyiez hello suivant le message de notification :</span><span class="sxs-lookup"><span data-stu-id="dee1c-177">Wait for a couple of minutes or wait until you see hello following notification message:</span></span>

    ![Gateway installation successful (Installation réussie de la passerelle)](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="dee1c-179">Lancez l’application **Gestionnaire de configuration de passerelle de gestion des données** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dee1c-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="dee1c-180">Bonjour **recherche** fenêtre, tapez **passerelle de gestion des données** tooaccess cet utilitaire.</span><span class="sxs-lookup"><span data-stu-id="dee1c-180">In hello **Search** window, type **Data Management Gateway** tooaccess this utility.</span></span> <span data-ttu-id="dee1c-181">Vous pouvez également trouver hello exécutable **ConfigManager.exe** dans le dossier de hello : **C:\Program Files\Microsoft données Gestion Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="dee1c-181">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Gestionnaire de configuration de la passerelle](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="dee1c-183">Vérifiez que le message `adftutorialgateway is connected toohello cloud service` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="dee1c-183">Confirm that you see `adftutorialgateway is connected toohello cloud service` message.</span></span> <span data-ttu-id="dee1c-184">Hello hello bas affiche la barre d’état **toohello cloud service connecté** avec un **coche verte**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-184">hello status bar hello bottom displays **Connected toohello cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="dee1c-185">Sur hello **accueil** onglet, vous pouvez également effectuer hello fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="dee1c-185">On hello **Home** tab, you can also do hello following operations:</span></span>

   * <span data-ttu-id="dee1c-186">**Inscrire** une passerelle avec une clé à partir de hello portail Azure à l’aide du bouton de Registre hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-186">**Register** a gateway with a key from hello Azure portal by using hello Register button.</span></span>
   * <span data-ttu-id="dee1c-187">**Arrêter** hello Service Gestion des données passerelle hôte en cours d’exécution sur votre ordinateur de passerelle.</span><span class="sxs-lookup"><span data-stu-id="dee1c-187">**Stop** hello Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="dee1c-188">**Planifier les mises à jour** toobe installé à un moment donné de la journée de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-188">**Schedule updates** toobe installed at a specific time of hello day.</span></span>
   * <span data-ttu-id="dee1c-189">Afficher lors de la passerelle de hello **dernière mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-189">View when hello gateway was **last updated**.</span></span>
   * <span data-ttu-id="dee1c-190">Spécifiez l’heure à laquelle une passerelle toohello de mise à jour peut être installée.</span><span class="sxs-lookup"><span data-stu-id="dee1c-190">Specify time at which an update toohello gateway can be installed.</span></span>
8. <span data-ttu-id="dee1c-191">Commutateur toohello **paramètres** certificat de hello onglet spécifié dans hello **certificat** section est utilisé tooencrypt/déchiffrer les informations d’identification de banque de données locale hello que vous spécifiez sur le portail hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-191">Switch toohello **Settings** tab. hello certificate specified in hello **Certificate** section is used tooencrypt/decrypt credentials for hello on-premises data store that you specify on hello portal.</span></span> <span data-ttu-id="dee1c-192">(facultatif) Cliquez sur **modification** toouse votre propre certificat à la place.</span><span class="sxs-lookup"><span data-stu-id="dee1c-192">(optional) Click **Change** toouse your own certificate instead.</span></span> <span data-ttu-id="dee1c-193">Par défaut, la passerelle de hello utilise certificat hello qui est généré automatiquement par hello service Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dee1c-193">By default, hello gateway uses hello certificate that is auto-generated by hello Data Factory service.</span></span>

    ![Configuration de certificat de la passerelle](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="dee1c-195">Vous pouvez également effectuer hello actions suivantes sur hello **paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="dee1c-195">You can also do hello following actions on hello **Settings** tab:</span></span>

   * <span data-ttu-id="dee1c-196">Afficher ou exporter le certificat hello utilisé par la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-196">View or export hello certificate being used by hello gateway.</span></span>
   * <span data-ttu-id="dee1c-197">Modifier le point de terminaison HTTPS hello utilisé par la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-197">Change hello HTTPS endpoint used by hello gateway.</span></span>    
   * <span data-ttu-id="dee1c-198">Définir un toobe du proxy HTTP utilisé par la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-198">Set an HTTP proxy toobe used by hello gateway.</span></span>     
9. <span data-ttu-id="dee1c-199">(facultatif) Commutateur toohello **Diagnostics** onglet, vérifiez hello **activer la journalisation documentée** option si vous souhaitez tooenable détaillés de journalisation que vous pouvez utiliser tootroubleshoot des problèmes avec la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-199">(optional) Switch toohello **Diagnostics** tab, check hello **Enable verbose logging** option if you want tooenable verbose logging that you can use tootroubleshoot any issues with hello gateway.</span></span> <span data-ttu-id="dee1c-200">Hello des informations de journalisation peuvent être trouvées dans **Observateur d’événements** sous **journaux des Applications et Services** -> **passerelle de gestion des données** nœud.</span><span class="sxs-lookup"><span data-stu-id="dee1c-200">hello logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Onglet Diagnostic](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="dee1c-202">Vous pouvez également effectuer hello suivant actions Bonjour **Diagnostics** onglet :</span><span class="sxs-lookup"><span data-stu-id="dee1c-202">You can also perform hello following actions in hello **Diagnostics** tab:</span></span>

   * <span data-ttu-id="dee1c-203">Utilisez **tester la connexion** source de données locale tooan section à l’aide de la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-203">Use **Test Connection** section tooan on-premises data source using hello gateway.</span></span>
   * <span data-ttu-id="dee1c-204">Cliquez sur **afficher les journaux** toosee hello passerelle de gestion des données de session dans une fenêtre de l’Observateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="dee1c-204">Click **View Logs** toosee hello Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="dee1c-205">Cliquez sur **d’envoi de journaux** tooupload un fichier zip avec des journaux de dernière sept jours tooMicrosoft toofacilitate dépannage de vos problèmes.</span><span class="sxs-lookup"><span data-stu-id="dee1c-205">Click **Send Logs** tooupload a zip file with logs of last seven days tooMicrosoft toofacilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="dee1c-206">Sur hello **Diagnostics** onglet hello **tester la connexion** section, sélectionnez **SqlServer** de type hello de données de hello stocker, entrez le nom hello du serveur de base de données hello, nom du Hello de base de données, spécifiez le type d’authentification, entrez le nom d’utilisateur et mot de passe, puis cliquez sur **Test** tootest si la passerelle de hello peut se connecter toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="dee1c-206">On hello **Diagnostics** tab, in hello **Test Connection** section, select **SqlServer** for hello type of hello data store, enter hello name of hello database server, name of hello database, specify authentication type, enter user name, and password, and click **Test** tootest whether hello gateway can connect toohello database.</span></span>
11. <span data-ttu-id="dee1c-207">Navigateur web du commutateur toohello, hello et **portail Azure**, cliquez sur **OK** sur hello **configurer** page puis, dans hello **nouvelle passerelle de données** page.</span><span class="sxs-lookup"><span data-stu-id="dee1c-207">Switch toohello web browser, and in hello **Azure portal**, click **OK** on hello **Configure** page and then on hello **New data gateway** page.</span></span>
12. <span data-ttu-id="dee1c-208">Vous devez voir **adftutorialgateway** sous **passerelles de données** dans l’arborescence hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="dee1c-208">You should see **adftutorialgateway** under **Data Gateways** in hello tree view on hello left.</span></span>  <span data-ttu-id="dee1c-209">Si vous cliquez dessus, vous devez voir hello associés JSON.</span><span class="sxs-lookup"><span data-stu-id="dee1c-209">If you click it, you should see hello associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="dee1c-210">Créez des services liés</span><span class="sxs-lookup"><span data-stu-id="dee1c-210">Create linked services</span></span>
<span data-ttu-id="dee1c-211">Au cours de cette étape, vous créez deux services liés : **AzureStorageLinkedService** et **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="dee1c-212">Hello **SqlServerLinkedService** lie une base de données SQL Server sur site et le hello **AzureStorageLinkedService** service lié lie une fabrique de données objet blob Azure store toohello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-212">hello **SqlServerLinkedService** links an on-premises SQL Server database and hello **AzureStorageLinkedService** linked service links an Azure blob store toohello data factory.</span></span> <span data-ttu-id="dee1c-213">Créer un pipeline plus loin dans cette procédure pas à pas qui copie les données de magasin de hello local SQL Server de base de données toohello objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="dee1c-213">You create a pipeline later in this walkthrough that copies data from hello on-premises SQL Server database toohello Azure blob store.</span></span>

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a><span data-ttu-id="dee1c-214">Ajouter une base de données locale SQL Server de service lié tooan</span><span class="sxs-lookup"><span data-stu-id="dee1c-214">Add a linked service tooan on-premises SQL Server database</span></span>
1. <span data-ttu-id="dee1c-215">Bonjour **éditeur Data Factory**, cliquez sur **nouveau magasin de données** sur la barre d’outils hello et sélectionnez **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-215">In hello **Data Factory Editor**, click **New data store** on hello toolbar and select **SQL Server**.</span></span>

   ![Nouveau service lié SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="dee1c-217">Bonjour **éditeur JSON** sur hello droite, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dee1c-217">In hello **JSON editor** on hello right, do hello following steps:</span></span>

   1. <span data-ttu-id="dee1c-218">Pourquoi **gatewayName**, spécifiez **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-218">For hello **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="dee1c-219">Bonjour **connectionString**, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dee1c-219">In hello **connectionString**, do hello following steps:</span></span>    

      1. <span data-ttu-id="dee1c-220">Pour **nom_serveur**, entrez le nom hello du serveur hello qui héberge la base de données SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-220">For **servername**, enter hello name of hello server that hosts hello SQL Server database.</span></span>
      2. <span data-ttu-id="dee1c-221">Pour **databasename**, entrez le nom hello de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-221">For **databasename**, enter hello name of hello database.</span></span>
      3. <span data-ttu-id="dee1c-222">Cliquez sur **Encrypt** bouton de barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-222">Click **Encrypt** button on hello toolbar.</span></span> <span data-ttu-id="dee1c-223">Application du Gestionnaire d’informations d’identification hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="dee1c-223">You see hello Credentials Manager application.</span></span>

         ![Application Gestionnaire des informations d’identification](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="dee1c-225">Bonjour **informations d’identification du paramètre** boîte de dialogue, spécifiez le type d’authentification, nom d’utilisateur et mot de passe, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-225">In hello **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="dee1c-226">Si la connexion de hello est réussie, hello chiffrée sont stockées dans hello JSON et fermeture de la boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-226">If hello connection is successful, hello encrypted credentials are stored in hello JSON and hello dialog box closes.</span></span>
      5. <span data-ttu-id="dee1c-227">Fermer un onglet de navigateur vide hello lancer la boîte de dialogue hello s’il n’est pas fermé automatiquement et revenir à onglet toohello avec hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dee1c-227">Close hello empty browser tab that launched hello dialog box if it is not automatically closed and get back toohello tab with hello Azure portal.</span></span>

         <span data-ttu-id="dee1c-228">Sur l’ordinateur de passerelle hello, ces informations d’identification sont **chiffrées** à l’aide d’un certificat qui hello fabrique de données propriétaire de service.</span><span class="sxs-lookup"><span data-stu-id="dee1c-228">On hello gateway machine, these credentials are **encrypted** by using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="dee1c-229">Si vous souhaitez que le certificat hello toouse associé hello passerelle de gestion des données au lieu de cela, consultez [définir les informations d’identification en toute sécurité](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="dee1c-229">If you want toouse hello certificate that is associated with hello Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="dee1c-230">Cliquez sur **déployer** sur toodeploy hello service lié SQL Server de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-230">Click **Deploy** on hello command bar toodeploy hello SQL Server linked service.</span></span> <span data-ttu-id="dee1c-231">Vous devez voir service hello lié dans l’arborescence hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-231">You should see hello linked service in hello tree view.</span></span>

      ![Service lié SQL Server dans l’arborescence de hello](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="dee1c-233">Ajout d’un service lié pour un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="dee1c-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="dee1c-234">Bonjour **éditeur Data Factory**, cliquez sur **nouveau magasin de données** hello de barre de commandes et cliquez sur **le stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-234">In hello **Data Factory Editor**, click **New data store** on hello command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="dee1c-235">Entrez le nom hello de votre compte de stockage Azure pour hello **nom de compte**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-235">Enter hello name of your Azure storage account for hello **Account name**.</span></span>
3. <span data-ttu-id="dee1c-236">Entrez la clé hello pour votre compte de stockage Azure pour hello **clé de compte**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-236">Enter hello key for your Azure storage account for hello **Account key**.</span></span>
4. <span data-ttu-id="dee1c-237">Cliquez sur **déployer** toodeploy hello **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-237">Click **Deploy** toodeploy hello **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="dee1c-238">Créez les jeux de données</span><span class="sxs-lookup"><span data-stu-id="dee1c-238">Create datasets</span></span>
<span data-ttu-id="dee1c-239">Dans cette étape, vous créez une entrée et sortie datasets qui représentent les données d’entrée et de sortie pour l’opération de copie hello (base de données locale SQL Server = > stockage d’objets blob Azure).</span><span class="sxs-lookup"><span data-stu-id="dee1c-239">In this step, you create input and output datasets that represent input and output data for hello copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="dee1c-240">Avant de créer des jeux de données, procédez comme hello (les étapes détaillées suit la liste de hello) comme suit :</span><span class="sxs-lookup"><span data-stu-id="dee1c-240">Before creating datasets, do hello following steps (detailed steps follows hello list):</span></span>

* <span data-ttu-id="dee1c-241">Créer une table nommée **emp** hello de base de données SQL Server vous avez ajouté en tant qu’une fabrique de données de service lié toohello et insérer quelques exemples d’entrées dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-241">Create a table named **emp** in hello SQL Server Database you added as a linked service toohello data factory and insert a couple of sample entries into hello table.</span></span>
* <span data-ttu-id="dee1c-242">Créer un conteneur d’objets blob nommé **adftutorial** Bonjour Azure blob compte de stockage que vous avez ajouté en tant qu’une fabrique de données toohello service lié.</span><span class="sxs-lookup"><span data-stu-id="dee1c-242">Create a blob container named **adftutorial** in hello Azure blob storage account you added as a linked service toohello data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a><span data-ttu-id="dee1c-243">Préparer SQL Server sur site hello</span><span class="sxs-lookup"><span data-stu-id="dee1c-243">Prepare On-premises SQL Server for hello tutorial</span></span>
1. <span data-ttu-id="dee1c-244">Dans base de données hello spécifiée pour hello local SQL Server service lié (**SqlServerLinkedService**), utilisez hello suivant hello SQL script toocreate **emp** table hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="dee1c-244">In hello database you specified for hello on-premises SQL Server linked service (**SqlServerLinkedService**), use hello following SQL script toocreate hello **emp** table in hello database.</span></span>

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
2. <span data-ttu-id="dee1c-245">Insérer des exemples dans la table de hello :</span><span class="sxs-lookup"><span data-stu-id="dee1c-245">Insert some sample into hello table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="dee1c-246">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="dee1c-246">Create input dataset</span></span>

1. <span data-ttu-id="dee1c-247">Bonjour **éditeur Data Factory**, cliquez sur **... Plus**, cliquez sur **nouveau dataset** sur hello de barre de commandes, puis cliquez sur **table SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-247">In hello **Data Factory Editor**, click **... More**, click **New dataset** on hello command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="dee1c-248">Remplacez hello JSON dans le volet de droite hello hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="dee1c-248">Replace hello JSON in hello right pane with hello following text:</span></span>

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
   <span data-ttu-id="dee1c-249">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="dee1c-249">Note hello following points:</span></span>

   * <span data-ttu-id="dee1c-250">**type** est défini trop**SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-250">**type** is set too**SqlServerTable**.</span></span>
   * <span data-ttu-id="dee1c-251">**tableName** est défini trop**emp**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-251">**tableName** is set too**emp**.</span></span>
   * <span data-ttu-id="dee1c-252">**linkedServiceName** est défini trop**SqlServerLinkedService** (vous aviez créé ce service lié plus haut dans cette procédure pas à pas).</span><span class="sxs-lookup"><span data-stu-id="dee1c-252">**linkedServiceName** is set too**SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="dee1c-253">Pour un jeu de données d’entrée qui n’est pas généré par un autre pipeline Azure Data Factory, vous devez définir **externe** trop**true**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** too**true**.</span></span> <span data-ttu-id="dee1c-254">Cela signifie que les données d’entrée hello sont toohello externe produit service Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dee1c-254">It denotes hello input data is produced external toohello Azure Data Factory service.</span></span> <span data-ttu-id="dee1c-255">Vous pouvez éventuellement spécifier des stratégies de données externes à l’aide de hello **externalData** élément Bonjour **stratégie** section.</span><span class="sxs-lookup"><span data-stu-id="dee1c-255">You can optionally specify any external data policies using hello **externalData** element in hello **Policy** section.</span></span>    

   <span data-ttu-id="dee1c-256">Pour plus de détails sur les propriétés JSON, voir [Déplacer des données vers/à partir SQL Server](data-factory-sqlserver-connector.md).</span><span class="sxs-lookup"><span data-stu-id="dee1c-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="dee1c-257">Cliquez sur **déployer** sur toodeploy hello dataset de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-257">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="dee1c-258">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="dee1c-258">Create output dataset</span></span>

1. <span data-ttu-id="dee1c-259">Bonjour **éditeur Data Factory**, cliquez sur **nouveau dataset** sur hello de barre de commandes, puis cliquez sur **le stockage Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-259">In hello **Data Factory Editor**, click **New dataset** on hello command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="dee1c-260">Remplacez hello JSON dans le volet de droite hello hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="dee1c-260">Replace hello JSON in hello right pane with hello following text:</span></span>

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
   <span data-ttu-id="dee1c-261">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="dee1c-261">Note hello following points:</span></span>

   * <span data-ttu-id="dee1c-262">**type** est défini trop**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-262">**type** is set too**AzureBlob**.</span></span>
   * <span data-ttu-id="dee1c-263">**linkedServiceName** est défini trop**AzureStorageLinkedService** (vous aviez créé ce service lié à l’étape 2).</span><span class="sxs-lookup"><span data-stu-id="dee1c-263">**linkedServiceName** is set too**AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="dee1c-264">**folderPath** est défini trop**adftutorial/outfromonpremdf** où outfromonpremdf est le dossier hello dans le conteneur d’adftutorial hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-264">**folderPath** is set too**adftutorial/outfromonpremdf** where outfromonpremdf is hello folder in hello adftutorial container.</span></span> <span data-ttu-id="dee1c-265">Créer hello **adftutorial** conteneur s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="dee1c-265">Create hello **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="dee1c-266">Hello **disponibilité** est défini trop**toutes les heures** (**fréquence** défini trop**heure** et **intervalle** défini trop **1**).</span><span class="sxs-lookup"><span data-stu-id="dee1c-266">hello **availability** is set too**hourly** (**frequency** set too**hour** and **interval** set too**1**).</span></span>  <span data-ttu-id="dee1c-267">Hello service Data Factory génère une tranche de données de sortie de toutes les heures Bonjour **emp** table Bonjour base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dee1c-267">hello Data Factory service generates an output data slice every hour in hello **emp** table in hello Azure SQL Database.</span></span>

   <span data-ttu-id="dee1c-268">Si vous ne spécifiez pas un **nom de fichier** pour un **table de sortie**, fichiers hello généré Bonjour **folderPath** sont nommés Bonjour suivant le format : données.<Guid>. txt (par exemple : : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="dee1c-268">If you do not specify a **fileName** for an **output table**, hello generated files in hello **folderPath** are named in hello following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="dee1c-269">tooset **folderPath** et **nom de fichier** dynamiquement en fonction de hello **SliceStart** fois, utilisez la propriété de partitionedBy hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-269">tooset **folderPath** and **fileName** dynamically based on hello **SliceStart** time, use hello partitionedBy property.</span></span> <span data-ttu-id="dee1c-270">Dans l’exemple suivant de hello, folderPath utilise Year, Month et Day de hello SliceStart (heure de début de la tranche hello en cours de traitement) et nom de fichier utilise l’heure de hello SliceStart.</span><span class="sxs-lookup"><span data-stu-id="dee1c-270">In hello following example, folderPath uses Year, Month, and Day from hello SliceStart (start time of hello slice being processed) and fileName uses Hour from hello SliceStart.</span></span> <span data-ttu-id="dee1c-271">Par exemple, si une tranche est produite pour 2014-10-20T08:00:00, hello nom_dossier est défini toowikidatagateway/wikidatagateway/2014/10/20 et nom de fichier hello too08.csv.</span><span class="sxs-lookup"><span data-stu-id="dee1c-271">For example, if a slice is being produced for 2014-10-20T08:00:00, hello folderName is set toowikidatagateway/wikisampledataout/2014/10/20 and hello fileName is set too08.csv.</span></span>

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

    <span data-ttu-id="dee1c-272">Pour plus de détails sur les propriétés JSON, voir [Déplacer des données vers/à partir de Stockage Blob Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="dee1c-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="dee1c-273">Cliquez sur **déployer** sur toodeploy hello dataset de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-273">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span> <span data-ttu-id="dee1c-274">Vérifiez que vous voyez deux jeux de données dans l’arborescence hello hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-274">Confirm that you see both hello datasets in hello tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="dee1c-275">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="dee1c-275">Create pipeline</span></span>
<span data-ttu-id="dee1c-276">Dans cette étape, vous créez un **pipeline** avec une **activité Copier l’activité** qui utilise **EmpOnPremSQLTable** en tant qu’entrée et **OutputBlobTable** en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="dee1c-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="dee1c-277">Dans Data Factory Editor, cliquez sur **... Plus**, puis sur **Nouveau pipeline**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="dee1c-278">Remplacez hello JSON dans le volet de droite hello hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="dee1c-278">Replace hello JSON in hello right pane with hello following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
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
   > <span data-ttu-id="dee1c-279">Remplacez la valeur hello hello **Démarrer** propriété hello jour actuel et **fin** valeur avec hello jour suivant.</span><span class="sxs-lookup"><span data-stu-id="dee1c-279">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span>
   >
   >

   <span data-ttu-id="dee1c-280">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="dee1c-280">Note hello following points:</span></span>

   * <span data-ttu-id="dee1c-281">Dans la section d’activités hello, il est uniquement les activités dont **type** est défini trop**copie**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-281">In hello activities section, there is only activity whose **type** is set too**Copy**.</span></span>
   * <span data-ttu-id="dee1c-282">**Entrée** d’activité hello est définie trop**EmpOnPremSQLTable** et **sortie** d’activité hello est définie trop**OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-282">**Input** for hello activity is set too**EmpOnPremSQLTable** and **output** for hello activity is set too**OutputBlobTable**.</span></span>
   * <span data-ttu-id="dee1c-283">Bonjour **typeProperties** section, **SqlSource** est spécifié comme hello **type de source de** et ** BlobSink ** est spécifié comme hello **detypederécepteur**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-283">In hello **typeProperties** section, **SqlSource** is specified as hello **source type** and **BlobSink **is specified as hello **sink type**.</span></span>
   * <span data-ttu-id="dee1c-284">Requête SQL `select * from emp` est spécifié pour hello **sqlReaderQuery** propriété du **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-284">SQL query `select * from emp` is specified for hello **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="dee1c-285">Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="dee1c-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="dee1c-286">Par exemple : 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="dee1c-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="dee1c-287">Hello **fin** temps est facultatif, mais nous l’utilisons dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="dee1c-287">hello **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="dee1c-288">Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures**».</span><span class="sxs-lookup"><span data-stu-id="dee1c-288">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="dee1c-289">pipeline de hello toorun indéfiniment, spécifiez **9/9/9999** en tant que valeur hello pour hello **fin** propriété.</span><span class="sxs-lookup"><span data-stu-id="dee1c-289">toorun hello pipeline indefinitely, specify **9/9/9999** as hello value for hello **end** property.</span></span>

   <span data-ttu-id="dee1c-290">Vous définissez hello durée dans le hello tranches de données sont traités en fonction de hello **disponibilité** propriétés qui ont été définies pour chaque jeu de données Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dee1c-290">You are defining hello time duration in which hello data slices are processed based on hello **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="dee1c-291">Exemple de hello, sont des tranches de données 24 comme chaque tranche de données est généré toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="dee1c-291">In hello example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="dee1c-292">Cliquez sur **déployer** sur toodeploy hello dataset de la barre de commandes hello (table est un jeu de données rectangulaire).</span><span class="sxs-lookup"><span data-stu-id="dee1c-292">Click **Deploy** on hello command bar toodeploy hello dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="dee1c-293">Confirmer ce pipeline hello s’affiche dans l’arborescence hello sous **Pipelines** nœud.</span><span class="sxs-lookup"><span data-stu-id="dee1c-293">Confirm that hello pipeline shows up in hello tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="dee1c-294">Maintenant, cliquez sur **X** à deux reprises tooclose hello page tooget arrière toohello **Data Factory** page hello **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-294">Now, click **X** twice tooclose hello page tooget back toohello **Data Factory** page for hello **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="dee1c-295">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="dee1c-295">**Congratulations!**</span></span> <span data-ttu-id="dee1c-296">Vous venez de créer une fabrique de données Azure, services liés, jeux de données et un pipeline et le pipeline de hello planifiée.</span><span class="sxs-lookup"><span data-stu-id="dee1c-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled hello pipeline.</span></span>

#### <a name="view-hello-data-factory-in-a-diagram-view"></a><span data-ttu-id="dee1c-297">Fabrique de données hello vue dans une vue de diagramme</span><span class="sxs-lookup"><span data-stu-id="dee1c-297">View hello data factory in a Diagram View</span></span>
1. <span data-ttu-id="dee1c-298">Bonjour **portail Azure**, cliquez sur **diagramme** vignette sur la page d’accueil hello pour hello **ADFTutorialOnPremDF** fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="dee1c-298">In hello **Azure portal**, click **Diagram** tile on hello home page for hello **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="dee1c-299">:</span><span class="sxs-lookup"><span data-stu-id="dee1c-299">:</span></span>

    ![Lien Diagramme](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="dee1c-301">Vous devez voir toohello similaires du diagramme hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="dee1c-301">You should see hello diagram similar toohello following image:</span></span>

    ![Vue du diagramme](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="dee1c-303">Vous pouvez faire un zoom, effectuer un zoom arrière, zoom too100 %, toofit de zoom, automatiquement les pipelines de position et jeux de données et afficher les informations de lignage (surligne les éléments en amont et en aval des éléments sélectionnés).</span><span class="sxs-lookup"><span data-stu-id="dee1c-303">You can zoom in, zoom out, zoom too100%, zoom toofit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="dee1c-304">Vous pouvez double-cliquer sur les propriétés de toosee d’un objet (jeu de données d’entrée/sortie ou pipeline) pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="dee1c-304">You can double-click an object (input/output dataset or pipeline) toosee properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="dee1c-305">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="dee1c-305">Monitor pipeline</span></span>
<span data-ttu-id="dee1c-306">Dans cette étape, vous utilisez hello Azure toomonitor portail, ce qui se passe dans une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="dee1c-306">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="dee1c-307">Vous pouvez également utiliser des pipelines et les jeux de données toomonitor d’applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dee1c-307">You can also use PowerShell cmdlets toomonitor datasets and pipelines.</span></span> <span data-ttu-id="dee1c-308">Pour plus de détails sur la surveillance, consultez [Surveillance et gestion des pipelines](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="dee1c-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="dee1c-309">Dans le diagramme de hello, double-cliquez sur **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-309">In hello diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Tranches EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="dee1c-311">Notez que toutes les données hello tranches des se trouvent dans **prêt** durée de pipeline hello (heure de début heure tooend) étant Bonjour passées de l’état.</span><span class="sxs-lookup"><span data-stu-id="dee1c-311">Notice that all hello data slices up are in **Ready** state because hello pipeline duration (start time tooend time) is in hello past.</span></span> <span data-ttu-id="dee1c-312">Il est également, car vous avez inséré des données de hello dans la base de données SQL Server hello et il n’y figure tout temps hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-312">It is also because you have inserted hello data in hello SQL Server database and it is there all hello time.</span></span> <span data-ttu-id="dee1c-313">Vérifiez qu’aucune tranche n’apparaissent dans hello **tranches de problème** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-313">Confirm that no slices show up in hello **Problem slices** section at hello bottom.</span></span> <span data-ttu-id="dee1c-314">Cliquez sur tous les secteurs de hello, de tooview **consultez plus** bas hello liste hello des tranches.</span><span class="sxs-lookup"><span data-stu-id="dee1c-314">tooview all hello slices, click **See More** at hello bottom of hello list of slices.</span></span>
3. <span data-ttu-id="dee1c-315">Maintenant, dans hello **Datasets** , cliquez sur **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-315">Now, In hello **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Tranches OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="dee1c-317">Cliquez sur n’importe quel tranche de données à partir de la liste de hello et vous devez voir hello **tranche de données** page.</span><span class="sxs-lookup"><span data-stu-id="dee1c-317">Click any data slice from hello list and you should see hello **Data Slice** page.</span></span> <span data-ttu-id="dee1c-318">Vous voyez l’exécution de l’activité de la tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-318">You see activity runs for hello slice.</span></span> <span data-ttu-id="dee1c-319">Généralement, une seule activité exécutée s’affiche.</span><span class="sxs-lookup"><span data-stu-id="dee1c-319">You see only one activity run usually.</span></span>  

    ![Panneau Tranche de données](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="dee1c-321">Si la tranche de hello n’est pas hello **prêt** état, vous pouvez voir les tranches en amont hello qui ne sont pas prêtes et bloquent tranche à partir de l’exécution dans hello hello **tranches en amont qui ne sont pas prêtes** liste.</span><span class="sxs-lookup"><span data-stu-id="dee1c-321">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="dee1c-322">Cliquez sur hello **activité exécuter** à partir de la liste de hello en hello bas toosee **détails d’activité l'exécution**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-322">Click hello **activity run** from hello list at hello bottom toosee **activity run details**.</span></span>

   ![Page Détails de l’exécution d’activité](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="dee1c-324">Vous constatez des informations telles que le débit, la durée et passerelle de hello tootransfer les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="dee1c-324">You would see information such as throughput, duration, and hello gateway used tootransfer hello data.</span></span>
6. <span data-ttu-id="dee1c-325">Cliquez sur **X** tooclose tous hello pages jusqu'à ce que vous</span><span class="sxs-lookup"><span data-stu-id="dee1c-325">Click **X** tooclose all hello pages until you</span></span>
7. <span data-ttu-id="dee1c-326">revenir toohello page d’accueil pour hello **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="dee1c-326">get back toohello home page for hello **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="dee1c-327">(facultatif) Cliquez sur **Pipelines**, sur **ADFTutorialOnPremDF**, puis accédez aux tables d’entrée (**Consommé**) ou aux jeux de données de sortie (**Produit**).</span><span class="sxs-lookup"><span data-stu-id="dee1c-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="dee1c-328">Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) tooverify qu’un objet blob/fichier est créé pour chaque heure.</span><span class="sxs-lookup"><span data-stu-id="dee1c-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) tooverify that a blob/file is created for each hour.</span></span>

   ![Explorateur de stockage Azure](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="dee1c-330">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dee1c-330">Next steps</span></span>
* <span data-ttu-id="dee1c-331">Consultez [passerelle de gestion des données](data-factory-data-management-gateway.md) de l’article pour tous les hello plus d’informations sur la passerelle de gestion des données de hello.</span><span class="sxs-lookup"><span data-stu-id="dee1c-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello Data Management Gateway.</span></span>
* <span data-ttu-id="dee1c-332">Consultez [copier les données d’objets Blob Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn sur comment banque de données récepteur tooa du magasin de données de toomove de l’activité de copie de toouse d’une source de données.</span><span class="sxs-lookup"><span data-stu-id="dee1c-332">See [Copy data from Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn about how toouse Copy Activity toomove data from a source data store tooa sink data store.</span></span>
