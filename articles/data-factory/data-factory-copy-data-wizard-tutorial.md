---
title: "Didacticiel : Créer un pipeline à l’aide de l’Assistant de copie | Microsoft Docs"
description: "Dans ce didacticiel, vous allez créer un pipeline Azure Data Factory avec une activité de copie, à l’aide de l’Assistant de copie et de Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5922c050cc09236ba5fdec885a70d11da20135cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="6894a-103">Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy</span><span class="sxs-lookup"><span data-stu-id="6894a-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6894a-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="6894a-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="6894a-105">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="6894a-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="6894a-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="6894a-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="6894a-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6894a-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="6894a-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6894a-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="6894a-109">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6894a-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="6894a-110">API REST</span><span class="sxs-lookup"><span data-stu-id="6894a-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="6894a-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="6894a-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="6894a-112">Ce didacticiel vous montre comment utiliser **l’Assistant de copie** pour copier des données à partir d’un stockage Blob Azure dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6894a-112">This tutorial shows you how to use the **Copy Wizard** to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

<span data-ttu-id="6894a-113">**L’Assistant de copie** Azure Data Factory vous permet de créer rapidement un pipeline de données qui copie les données d’un magasin de données source pris en charge dans un magasin de données de destination pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6894a-113">The Azure Data Factory **Copy Wizard** allows you to quickly create a data pipeline that copies data from a supported source data store to a supported destination data store.</span></span> <span data-ttu-id="6894a-114">Par conséquent, nous vous recommandons d’utiliser l’Assistant en vue de créer un exemple de pipeline pour votre scénario de déplacement de données.</span><span class="sxs-lookup"><span data-stu-id="6894a-114">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="6894a-115">Pour obtenir la liste des magasins de données pris en charge en tant que sources et destinations, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) .</span><span class="sxs-lookup"><span data-stu-id="6894a-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="6894a-116">Ce didacticiel vous montre comment créer une fabrique de données Azure, lancer l’Assistant Copie et suivre une série d’étapes pour fournir des informations sur votre scénario d’ingestion/déplacement de données.</span><span class="sxs-lookup"><span data-stu-id="6894a-116">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="6894a-117">Une fois les étapes de l’Assistant terminées, celui-ci crée automatiquement un pipeline avec une activité de copie pour copier des données d’un stockage d’objets blob Azure à une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6894a-117">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="6894a-118">Pour plus d’informations sur l’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6894a-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6894a-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6894a-119">Prerequisites</span></span>
<span data-ttu-id="6894a-120">Assurez-vous que vous respectez la configuration requise décrite dans l’article [Vue d’ensemble du didacticiel](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) avant de suivre ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6894a-120">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="6894a-121">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="6894a-121">Create data factory</span></span>
<span data-ttu-id="6894a-122">Dans cette étape, vous allez utiliser le portail Azure pour créer une fabrique de données Azure nommée **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="6894a-122">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="6894a-123">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6894a-123">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6894a-124">Cliquez sur **+ NOUVEAU** en haut à gauche, sur **Données et analyse**, puis sur **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="6894a-124">Click **+ NEW** from the top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Nouveau -> DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="6894a-126">Dans le panneau **Nouvelle fabrique de données** :</span><span class="sxs-lookup"><span data-stu-id="6894a-126">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="6894a-127">Entrez **ADFTutorialDataFactory** comme **nom**.</span><span class="sxs-lookup"><span data-stu-id="6894a-127">Enter **ADFTutorialDataFactory** for the **name**.</span></span>
       <span data-ttu-id="6894a-128">Le nom de la fabrique de données Azure doit être un nom global unique.</span><span class="sxs-lookup"><span data-stu-id="6894a-128">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="6894a-129">Si l’erreur `Data factory name “ADFTutorialDataFactory” is not available` s’affiche, changez le nom de la fabrique de données (par exemple, votrenomADFTutorialDataFactoryAAAAMMJJ), puis tentez de la recréer.</span><span class="sxs-lookup"><span data-stu-id="6894a-129">If you receive the error: `Data factory name “ADFTutorialDataFactory” is not available`, change the name of the data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="6894a-130">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6894a-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Nom de la fabrique de données indisponible](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="6894a-132">Sélectionnez votre **abonnement**Azure.</span><span class="sxs-lookup"><span data-stu-id="6894a-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="6894a-133">Pour Groupe de ressources, effectuez l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6894a-133">For Resource Group, do one of the following steps:</span></span> 
      
      - <span data-ttu-id="6894a-134">Sélectionnez **Utiliser l’existant** pour sélectionner un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="6894a-134">Select **Use existing** to select an existing resource group.</span></span>
      - <span data-ttu-id="6894a-135">Sélectionnez **Créer un nouveau** pour entrer un nom pour un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6894a-135">Select **Create new** to enter a name for a resource group.</span></span>
          
        <span data-ttu-id="6894a-136">Certaines étapes de ce didacticiel supposent que vous utilisez le groupe de ressources nommé **ADFTutorialResourceGroup** .</span><span class="sxs-lookup"><span data-stu-id="6894a-136">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="6894a-137">Pour plus d'informations sur les groupes de ressources, consultez [Utilisation des groupes de ressources pour gérer vos ressources Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6894a-137">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="6894a-138">Sélectionnez un **emplacement** pour la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="6894a-138">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="6894a-139">Sélectionnez la case à cocher **Épingler au tableau de bord** en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="6894a-139">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="6894a-140">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6894a-140">Click **Create**.</span></span>
      
       ![Panneau Nouvelle fabrique de données](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="6894a-142">Une fois la création terminée, le panneau **Data Factory** s’affiche comme sur l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="6894a-142">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>
   
   ![Page d'accueil Data Factory](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="6894a-144">Lancer l’Assistant Copie</span><span class="sxs-lookup"><span data-stu-id="6894a-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="6894a-145">Dans le panneau Fabrique de données, cliquez sur **Copier les données [VERSION PRÉLIMINAIRE]** pour lancer **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="6894a-145">On the Data Factory blade, click **Copy data [PREVIEW]** to launch the **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="6894a-146">Si vous voyez que le navigateur web est bloqué au niveau « Autorisation... », désactivez/décochez l’option **Block third party cookies and site data** (Bloquer les cookies et les données de site tiers) dans les paramètres du navigateur (ou) laissez cette option activée et créez une exception pour **login.microsoftonline.com**, puis essayez de relancer l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="6894a-146">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in the browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="6894a-147">Dans la page **Propriétés** :</span><span class="sxs-lookup"><span data-stu-id="6894a-147">In the **Properties** page:</span></span>
   
   1. <span data-ttu-id="6894a-148">Saisissez **CopyFromBlobToAzureSql** dans **Nom de la tâche**.</span><span class="sxs-lookup"><span data-stu-id="6894a-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="6894a-149">Saisissez une **Description** (facultative).</span><span class="sxs-lookup"><span data-stu-id="6894a-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="6894a-150">Modifiez les champs **Date et heure de début** et **Date et heure de fin** de manière à définir la date de fin sur la date du jour et la date de début cinq jours plus tôt.</span><span class="sxs-lookup"><span data-stu-id="6894a-150">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days earlier.</span></span>  
   4. <span data-ttu-id="6894a-151">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6894a-151">Click **Next**.</span></span>  
      
      ![Outil de copie - page Propriétés](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="6894a-153">Dans la page **Source data store** (Magasin de données source), cliquez sur la vignette **Stockage d’objets blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="6894a-153">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="6894a-154">Cette page sert à spécifier le magasin de données source pour la tâche de copie.</span><span class="sxs-lookup"><span data-stu-id="6894a-154">You use this page to specify the source data store for the copy task.</span></span> 
   
    ![Outil de copie - page Source data store (Magasin de données source)](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="6894a-156">Dans la page **Specify the Azure Blob storage account** (Spécifier le compte de stockage d’objets blob Azure) :</span><span class="sxs-lookup"><span data-stu-id="6894a-156">On the **Specify the Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="6894a-157">Saisissez **AzureStorageLinkedService** dans **Nom du service lié**.</span><span class="sxs-lookup"><span data-stu-id="6894a-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="6894a-158">Vérifiez que l’option **À partir des abonnements** est sélectionnée pour **Account selection method** (Méthode de sélection du compte).</span><span class="sxs-lookup"><span data-stu-id="6894a-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="6894a-159">Sélectionnez votre **abonnement**Azure.</span><span class="sxs-lookup"><span data-stu-id="6894a-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="6894a-160">Sélectionnez un **compte de stockage Azure** dans la liste des comptes de stockage Azure disponibles dans l’abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6894a-160">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="6894a-161">Vous pouvez également choisir de saisir manuellement les paramètres du compte de stockage en sélectionnant l’option **Saisir manuellement** dans **Account selection method** (Méthode de sélection de compte). Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6894a-161">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span></span> 
      
      ![Outil de copie - spécifiez le compte de stockage d’objets blob Azure](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="6894a-163">Dans la page **Choose the input file or folder** (Choisir le fichier ou le dossier d’entrée) :</span><span class="sxs-lookup"><span data-stu-id="6894a-163">On **Choose the input file or folder** page:</span></span>
   
   1. <span data-ttu-id="6894a-164">Double-cliquez sur **adftutorial** (dossier).</span><span class="sxs-lookup"><span data-stu-id="6894a-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="6894a-165">Sélectionnez **emp.txt**, puis cliquez sur **Choisir**.</span><span class="sxs-lookup"><span data-stu-id="6894a-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Outil de copie - choisissez le fichier ou le dossier d’entrée](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="6894a-167">Sur la page **Choose the input file or folder (Choisir le fichier ou le dossier d’entrée)**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6894a-167">On the **Choose the input file or folder** page, click **Next**.</span></span> <span data-ttu-id="6894a-168">Ne sélectionnez pas **copie binaire**.</span><span class="sxs-lookup"><span data-stu-id="6894a-168">Do not select **Binary copy**.</span></span> 
   
    ![Outil de copie - choisissez le fichier ou le dossier d’entrée](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="6894a-170">Dans la page **File format settings** (Paramètres de format de fichier), vous pouvez voir les délimiteurs et le schéma qui sont détectés automatiquement par l’Assistant en analysant le fichier.</span><span class="sxs-lookup"><span data-stu-id="6894a-170">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> <span data-ttu-id="6894a-171">Vous pouvez également entrer les délimiteurs manuellement pour que l’Assistant copie arrête leur détection automatique ou pour remplacer les délimiteurs détectés.</span><span class="sxs-lookup"><span data-stu-id="6894a-171">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span></span> <span data-ttu-id="6894a-172">Une fois que vous avez vérifié les délimiteurs et afficher un aperçu des données, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6894a-172">Click **Next** after you review the delimiters and preview data.</span></span> 
   
    ![Outil de copie - Paramètres de format de fichier](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="6894a-174">Dans la page de la banque de données de destination, cliquez sur la vignette **Azure SQL Database**, puis sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6894a-174">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Outil de copie - Choisir une banque de destination](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="6894a-176">Dans la page **Specify the Azure SQL database** (Spécifier la base de données Azure SQL Database) :</span><span class="sxs-lookup"><span data-stu-id="6894a-176">On **Specify the Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="6894a-177">Saisissez **AzureSqlLinkedService** dans le champ **Nom de la connexion**.</span><span class="sxs-lookup"><span data-stu-id="6894a-177">Enter **AzureSqlLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="6894a-178">Vérifiez que l’option **À partir des abonnements** est sélectionnée pour **Server / database selection method** (Méthode de sélection du serveur/de la base de données).</span><span class="sxs-lookup"><span data-stu-id="6894a-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="6894a-179">Sélectionnez votre **abonnement**Azure.</span><span class="sxs-lookup"><span data-stu-id="6894a-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="6894a-180">Sélectionnez le **Nom du serveur** et la **Base de données**.</span><span class="sxs-lookup"><span data-stu-id="6894a-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="6894a-181">Saisissez le **Nom d’utilisateur** et le **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6894a-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="6894a-182">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6894a-182">Click **Next**.</span></span>  
      
      ![Outil de copie - Spécifier la base de données SQL Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="6894a-184">Dans la page **Mappage de table**, sélectionnez **emp** dans la liste déroulante du champ **Destination**, puis cliquez sur **Flèche vers le bas** (facultatif) pour afficher le schéma et un aperçu des données.</span><span class="sxs-lookup"><span data-stu-id="6894a-184">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span></span>
    
     ![Outil de copie - Mappage de Table](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="6894a-186">Dans la page **Mappage de schéma** cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6894a-186">On the **Schema mapping** page, click **Next**.</span></span>
    
    ![Outil de copie - Mappage de schéma](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="6894a-188">Dans la page **Paramètres de performances** cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6894a-188">On the **Performance settings** page, click **Next**.</span></span> 
    
    ![Outil de copie - Paramètres de performances](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="6894a-190">Passez en revue les informations contenues dans la page **Résumé**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="6894a-190">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="6894a-191">L’Assistant crée deux services liés, deux jeux de données (entrée et sortie) et un pipeline dans la fabrique de données (d’où vous avez lancé l’Assistant Copie).</span><span class="sxs-lookup"><span data-stu-id="6894a-191">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span> 
    
    ![Outil de copie - Paramètres de performances](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="6894a-193">Lancer l’application Surveiller et gérer</span><span class="sxs-lookup"><span data-stu-id="6894a-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="6894a-194">Dans la page **Déploiement**, cliquez sur le lien : `Click here to monitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="6894a-194">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span></span>
   
   ![Outil de copie - Déploiement réussi](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="6894a-196">L’application d’analyse est lancée dans un onglet distinct de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="6894a-196">The monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![Application de surveillance](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="6894a-198">Pour afficher le dernier état des tranches horaires, cliquez sur le bouton **Actualiser** dans la liste **FENÊTRES D’ACTIVITÉ** en bas.</span><span class="sxs-lookup"><span data-stu-id="6894a-198">To see the latest status of hourly slices, click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom.</span></span> <span data-ttu-id="6894a-199">Cette opération affiche cinq fenêtres d’activité pour cinq jours entre les heures de début et de fin du pipeline.</span><span class="sxs-lookup"><span data-stu-id="6894a-199">You see five activity windows for five days between start and end times for the pipeline.</span></span> <span data-ttu-id="6894a-200">Comme la liste n’est pas actualisée automatiquement, vous devrez peut-être cliquer sur Actualiser plusieurs fois avant que toutes les fenêtres d’activité soient à l’état Prêt.</span><span class="sxs-lookup"><span data-stu-id="6894a-200">The list is not automatically refreshed, so you may need to click Refresh a couple of times before you see all the activity windows in the Ready state.</span></span> 
4. <span data-ttu-id="6894a-201">Sélectionnez une fenêtre d’activité dans la liste.</span><span class="sxs-lookup"><span data-stu-id="6894a-201">Select an activity window in the list.</span></span> <span data-ttu-id="6894a-202">Affichez les informations la concernant dans **l’Explorateur de fenêtres d’activité** à droite.</span><span class="sxs-lookup"><span data-stu-id="6894a-202">See the details about it in the **Activity Window Explorer** on the right.</span></span>

    ![Détails de la fenêtre d’activité](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="6894a-204">Notez que les dates, 11, 12, 13, 14 et 15 sont en vert, ce qui signifie que les tranches de sortie quotidiennes de ces dates ont déjà été produites.</span><span class="sxs-lookup"><span data-stu-id="6894a-204">Notice that the dates 11, 12, 13, 14, and 15 are in green color, which means that the daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="6894a-205">Ce codage couleur apparaît également sur le pipeline et dans le jeu de données de sortie de la vue du diagramme.</span><span class="sxs-lookup"><span data-stu-id="6894a-205">You also see this color coding on the pipeline and the output dataset in the diagram view.</span></span> <span data-ttu-id="6894a-206">À l’étape précédente, notez que deux tranches ont déjà été produites et une tranche est en cours de traitement. Les deux autres sont en attente de traitement (comme l’indique le codage couleur).</span><span class="sxs-lookup"><span data-stu-id="6894a-206">In the previous step, notice that two slices have already been produced, one slice is currently being processed, and the other two are waiting to be processed (based on the color coding).</span></span> 

    <span data-ttu-id="6894a-207">Pour plus d’informations sur l’utilisation de cette application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et de gestion](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="6894a-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6894a-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6894a-208">Next steps</span></span>
<span data-ttu-id="6894a-209">Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie.</span><span class="sxs-lookup"><span data-stu-id="6894a-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="6894a-210">Le tableau ci-dessous contient la liste des magasins de données pris en charge en tant que sources et destinations par l’activité de copie :</span><span class="sxs-lookup"><span data-stu-id="6894a-210">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="6894a-211">Pour plus d’informations sur les champs/propriétés affichés dans l’Assistant de copie d’un magasin de données, cliquez sur le lien du magasin de données dans la table.</span><span class="sxs-lookup"><span data-stu-id="6894a-211">For details about fields/properties that you see in the copy wizard for a data store, click the link for the data store in the table.</span></span> 