---
title: "Didacticiel : Utilisation REST API toocreate un pipeline Azure Data Factory | Documents Microsoft"
description: "Dans ce didacticiel, vous utilisez des API REST toocreate un pipeline Azure Data Factory comportant des données toocopy d’activité de copie à partir d’un stockage d’objets blob Azure une base de données SQL Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="e832d-103">Didacticiel : Utilisation REST API toocreate un Azure Data Factory pipeline toocopy de données</span><span class="sxs-lookup"><span data-stu-id="e832d-103">Tutorial: Use REST API toocreate an Azure Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e832d-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="e832d-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="e832d-105">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="e832d-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="e832d-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e832d-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="e832d-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e832d-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="e832d-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e832d-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="e832d-109">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e832d-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="e832d-110">API REST</span><span class="sxs-lookup"><span data-stu-id="e832d-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="e832d-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="e832d-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="e832d-112">Dans cet article, vous découvrez comment toouse REST API toocreate une fabrique de données avec un pipeline qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-112">In this article, you learn how toouse REST API toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="e832d-113">Si vous êtes tooAzure nouvelle fabrique de données, lisez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article avant d’entamer ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e832d-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="e832d-114">Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie.</span><span class="sxs-lookup"><span data-stu-id="e832d-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="e832d-115">activité de copie Hello copie des données à partir d’un magasin de données de données pris en charge magasin tooa récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e832d-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="e832d-116">Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="e832d-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="e832d-117">activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="e832d-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="e832d-118">Pour plus d’informations sur l’activité de copie de hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e832d-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="e832d-119">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="e832d-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="e832d-120">De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="e832d-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="e832d-121">Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="e832d-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="e832d-122">Cet article ne couvre pas hello toutes les API REST de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="e832d-122">This article does not cover all hello Data Factory REST API.</span></span> <span data-ttu-id="e832d-123">Consultez les [informations de référence sur l’API REST Data Factory](/rest/api/datafactory/) pour obtenir une documentation complète sur les applets de commande Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e832d-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="e832d-124">le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa.</span><span class="sxs-lookup"><span data-stu-id="e832d-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="e832d-125">Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="e832d-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e832d-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e832d-126">Prerequisites</span></span>
* <span data-ttu-id="e832d-127">Passez en revue [vue d’ensemble du didacticiel](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) et hello complète **condition préalable** étapes.</span><span class="sxs-lookup"><span data-stu-id="e832d-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="e832d-128">Installez [Curl](https://curl.haxx.se/dlwiz/) sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e832d-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="e832d-129">Vous utilisez l’outil de Curl de hello avec d’autres commandes toocreate une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="e832d-129">You use hello Curl tool with REST commands toocreate a data factory.</span></span> 
* <span data-ttu-id="e832d-130">Suivez les instructions de [cet article](../azure-resource-manager/resource-group-create-service-principal-portal.md) pour effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e832d-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="e832d-131">Créez une application Web nommée **ADFCopyTutotiralApp** dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e832d-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="e832d-132">Obtenez un **ID client** et une **clé secrète**.</span><span class="sxs-lookup"><span data-stu-id="e832d-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="e832d-133">Obtenez l’ **ID de locataire**.</span><span class="sxs-lookup"><span data-stu-id="e832d-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="e832d-134">Affecter hello **ADFCopyTutorialApp** application toohello **collaborateur de fabrique de données** rôle.</span><span class="sxs-lookup"><span data-stu-id="e832d-134">Assign hello **ADFCopyTutorialApp** application toohello **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="e832d-135">Installez [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e832d-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="e832d-136">Lancez **PowerShell** et hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="e832d-136">Launch **PowerShell** and do hello following steps.</span></span> <span data-ttu-id="e832d-137">Laissez Azure PowerShell ouverte jusqu'à la fin de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e832d-137">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="e832d-138">Si vous fermez et rouvrez, vous devez à nouveau les commandes de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="e832d-138">If you close and reopen, you need toorun hello commands again.</span></span>
  
  1. <span data-ttu-id="e832d-139">Exécutez hello commande suivante, puis entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="e832d-139">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="e832d-140">Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte :</span><span class="sxs-lookup"><span data-stu-id="e832d-140">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="e832d-141">Tooselect hello abonnement toowork avec la commande suivante d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-141">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="e832d-142">Remplacez  **&lt;NameOfAzureSubscription** &gt; avec le nom de hello de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-142">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="e832d-143">Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello commande Bonjour PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="e832d-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="e832d-144">Si groupe de ressources hello existe déjà, vous spécifiez si tooupdate il (Y) ou conserver en tant que (N).</span><span class="sxs-lookup"><span data-stu-id="e832d-144">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="e832d-145">Certaines des étapes hello dans ce didacticiel supposent que vous utilisez le groupe de ressources hello nommé ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="e832d-145">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="e832d-146">Si vous utilisez un autre groupe de ressources, vous devez le nom de hello toouse de votre groupe de ressources à la place de ADFTutorialResourceGroup dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e832d-146">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="e832d-147">Créer des définitions JSON</span><span class="sxs-lookup"><span data-stu-id="e832d-147">Create JSON definitions</span></span>
<span data-ttu-id="e832d-148">Créer des fichiers JSON dans le dossier hello où se trouve curl.exe suivants.</span><span class="sxs-lookup"><span data-stu-id="e832d-148">Create following JSON files in hello folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="e832d-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="e832d-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e832d-150">Nom doit être globalement unique, vous pouvez donc tooprefix/suffixe ADFCopyTutorialDF toomake il un nom unique.</span><span class="sxs-lookup"><span data-stu-id="e832d-150">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="e832d-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="e832d-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e832d-152">Remplacez **accountname** et **accountkey** par le nom et la clé de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="e832d-153">toolearn comment tooget votre stockage accéder aux clés, voir [clés d’accès afficher, copier et régénérer stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="e832d-153">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

<span data-ttu-id="e832d-154">Pour plus d’informations sur les propriétés JSON, consultez [Service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="e832d-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="e832d-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="e832d-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e832d-156">Remplacez **nom_serveur**, **databasename**, **nom d’utilisateur**, et **mot de passe** avec le nom de votre serveur SQL Azure, le nom de base de données SQL, utilisateur compte et mot de passe pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for hello account.</span></span>  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="e832d-157">Pour plus d’informations sur les propriétés JSON, consultez [Service lié SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e832d-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="e832d-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="e832d-158">inputdataset.json</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "AzureStorageLinkedService",
    "typeProperties": {
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ","
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="e832d-159">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="e832d-159">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="e832d-160">Propriété</span><span class="sxs-lookup"><span data-stu-id="e832d-160">Property</span></span> | <span data-ttu-id="e832d-161">Description</span><span class="sxs-lookup"><span data-stu-id="e832d-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e832d-162">type</span><span class="sxs-lookup"><span data-stu-id="e832d-162">type</span></span> | <span data-ttu-id="e832d-163">propriété de type Hello est définie trop**AzureBlob** , car les données résident dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-163">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="e832d-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e832d-164">linkedServiceName</span></span> | <span data-ttu-id="e832d-165">Fait référence toohello **AzureStorageLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="e832d-165">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="e832d-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="e832d-166">folderPath</span></span> | <span data-ttu-id="e832d-167">Spécifie l’objet blob de hello **conteneur** et hello **dossier** qui contient des objets BLOB d’entrée.</span><span class="sxs-lookup"><span data-stu-id="e832d-167">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="e832d-168">Dans ce didacticiel, adftutorial est le conteneur d’objets blob hello et dossier est le dossier racine de hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-168">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
| <span data-ttu-id="e832d-169">fileName</span><span class="sxs-lookup"><span data-stu-id="e832d-169">fileName</span></span> | <span data-ttu-id="e832d-170">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="e832d-170">This property is optional.</span></span> <span data-ttu-id="e832d-171">Si vous omettez cette propriété, tous les fichiers à partir de hello folderPath sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="e832d-171">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="e832d-172">Dans ce didacticiel, **emp.txt** n’est spécifié pour hello nom de fichier, ainsi que pour ce fichier est récupéré pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="e832d-172">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="e832d-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="e832d-173">format -> type</span></span> |<span data-ttu-id="e832d-174">fichier d’entrée de Hello est au format de texte hello, nous utilisons **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="e832d-174">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="e832d-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="e832d-175">columnDelimiter</span></span> | <span data-ttu-id="e832d-176">colonnes Hello dans le fichier d’entrée de hello sont délimitées par **caractère virgule (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="e832d-176">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="e832d-177">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="e832d-177">frequency/interval</span></span> | <span data-ttu-id="e832d-178">fréquence de Hello est défini trop**heure** et de l’intervalle est défini trop**1**, ce qui signifie que hello entrée tranches sont disponibles **toutes les heures**.</span><span class="sxs-lookup"><span data-stu-id="e832d-178">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="e832d-179">En d’autres termes, hello service Data Factory recherche les données d’entrée toutes les heures dans le dossier racine de hello du conteneur d’objets blob (**adftutorial**) vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="e832d-179">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="e832d-180">Il recherche les données de salutation dans hello pipeline début et fin des heures, pas avant ou après ces moments précis.</span><span class="sxs-lookup"><span data-stu-id="e832d-180">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="e832d-181">external</span><span class="sxs-lookup"><span data-stu-id="e832d-181">external</span></span> | <span data-ttu-id="e832d-182">Cette propriété a la valeur trop**true** si les données de salutation ne sont pas générées par ce pipeline.</span><span class="sxs-lookup"><span data-stu-id="e832d-182">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="e832d-183">les données d’entrée de salutation dans ce didacticiel sont dans le fichier hello emp.txt, ce qui n’est pas généré par ce pipeline, et nous avons tootrue de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="e832d-183">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

<span data-ttu-id="e832d-184">Pour plus d’informations sur ces propriétés JSON, voir [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e832d-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="e832d-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="e832d-185">outputdataset.json</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "emp"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="e832d-186">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="e832d-186">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="e832d-187">Propriété</span><span class="sxs-lookup"><span data-stu-id="e832d-187">Property</span></span> | <span data-ttu-id="e832d-188">Description</span><span class="sxs-lookup"><span data-stu-id="e832d-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e832d-189">type</span><span class="sxs-lookup"><span data-stu-id="e832d-189">type</span></span> | <span data-ttu-id="e832d-190">propriété de type Hello est définie trop**AzureSqlTable** , car les données sont table tooa copiées dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-190">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
| <span data-ttu-id="e832d-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e832d-191">linkedServiceName</span></span> | <span data-ttu-id="e832d-192">Fait référence toohello **AzureSqlLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="e832d-192">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="e832d-193">TableName</span><span class="sxs-lookup"><span data-stu-id="e832d-193">tableName</span></span> | <span data-ttu-id="e832d-194">Hello spécifié **table** toowhich hello données sont copiées.</span><span class="sxs-lookup"><span data-stu-id="e832d-194">Specified hello **table** toowhich hello data is copied.</span></span> | 
| <span data-ttu-id="e832d-195">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="e832d-195">frequency/interval</span></span> | <span data-ttu-id="e832d-196">Hello fréquence est définie trop**heure** et l’intervalle est **1**, ce qui signifie que les tranches de sortie hello sont produits **toutes les heures** entre le début du pipeline hello et les heures, pas avant de fin ou après ces moments précis.</span><span class="sxs-lookup"><span data-stu-id="e832d-196">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="e832d-197">Il existe trois colonnes : **ID**, **FirstName**, et **LastName** : dans la table emp de hello dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-197">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="e832d-198">ID est une colonne d’identité, vous devez toospecify uniquement **FirstName** et **LastName** ici.</span><span class="sxs-lookup"><span data-stu-id="e832d-198">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="e832d-199">Pour plus d’informations sur ces propriétés JSON, consultez l’article [Connecteur SQL Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e832d-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="e832d-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="e832d-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

<span data-ttu-id="e832d-201">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="e832d-201">Note hello following points:</span></span>

- <span data-ttu-id="e832d-202">Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**copie**.</span><span class="sxs-lookup"><span data-stu-id="e832d-202">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="e832d-203">Pour plus d’informations sur l’activité de copie hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e832d-203">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="e832d-204">Dans les solutions Data Factory, vous pouvez également utiliser [Activités de transformation des données](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e832d-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="e832d-205">Entrée d’activité hello est définie trop**AzureBlobInput** et de sortie d’activité hello est définie trop**AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="e832d-205">Input for hello activity is set too**AzureBlobInput** and output for hello activity is set too**AzureSqlOutput**.</span></span> 
- <span data-ttu-id="e832d-206">Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-206">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="e832d-207">Pour obtenir une liste complète des magasins de données pris en charge par l’activité de copie hello en tant que sources et récepteurs, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="e832d-207">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="e832d-208">toolearn comment toouse données pris en charge spécifiques stocker en tant que source/récepteur, cliquez sur lien hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-208">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
 
<span data-ttu-id="e832d-209">Remplacez la valeur hello hello **Démarrer** propriété hello jour actuel et **fin** valeur avec hello jour suivant.</span><span class="sxs-lookup"><span data-stu-id="e832d-209">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="e832d-210">Vous pouvez spécifier qu’une partie date hello et ignorer la partie heure hello hello date heure.</span><span class="sxs-lookup"><span data-stu-id="e832d-210">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="e832d-211">Par exemple, « 2017-02-03 », qui est l’équivalent trop « 2017-02-03T00:00:00Z »</span><span class="sxs-lookup"><span data-stu-id="e832d-211">For example, "2017-02-03", which is equivalent too"2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="e832d-212">Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="e832d-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="e832d-213">Par exemple : 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="e832d-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="e832d-214">Hello **fin** temps est facultatif, mais nous l’utilisons dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e832d-214">hello **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="e832d-215">Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures**».</span><span class="sxs-lookup"><span data-stu-id="e832d-215">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="e832d-216">pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété.</span><span class="sxs-lookup"><span data-stu-id="e832d-216">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
 
<span data-ttu-id="e832d-217">Hello précédent exemple, sont des tranches de données 24 comme chaque tranche de données est généré toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="e832d-217">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="e832d-218">Pour obtenir une description des propriétés JSON dans une définition de pipeline, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="e832d-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e832d-219">Pour obtenir une description des propriétés JSON dans une définition d’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e832d-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="e832d-220">Pour obtenir une description des propriétés JSON prises en charge par BlobSource, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="e832d-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="e832d-221">Pour obtenir une description des propriétés JSON prises en charge par SqlSink, consultez l’article [Azure SQL Database connector](data-factory-azure-sql-connector.md) (Connecteur de base de données SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="e832d-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="e832d-222">Définir des variables globales</span><span class="sxs-lookup"><span data-stu-id="e832d-222">Set global variables</span></span>
<span data-ttu-id="e832d-223">Dans Azure PowerShell, exécutez hello suivant les commandes après le remplacement des valeurs de hello par les vôtres :</span><span class="sxs-lookup"><span data-stu-id="e832d-223">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e832d-224">Consultez la section [Configuration requise](#prerequisites) pour savoir comment obtenir un ID client, une clé secrète client, un ID de locataire et un ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="e832d-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="e832d-225">Exécutez hello commande suivante après la mise à jour nom hello hello fabrique de données que vous utilisez :</span><span class="sxs-lookup"><span data-stu-id="e832d-225">Run hello following command after updating hello name of hello data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="e832d-226">Authentifier avec AAD</span><span class="sxs-lookup"><span data-stu-id="e832d-226">Authenticate with AAD</span></span>
<span data-ttu-id="e832d-227">Exécutez hello suivant commande tooauthenticate avec Azure Active Directory (AAD) :</span><span class="sxs-lookup"><span data-stu-id="e832d-227">Run hello following command tooauthenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="e832d-228">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="e832d-228">Create data factory</span></span>
<span data-ttu-id="e832d-229">Dans cette étape, vous créez une fabrique de données Azure nommée **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="e832d-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="e832d-230">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="e832d-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="e832d-231">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="e832d-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="e832d-232">Par exemple, magasin de données toocopy l’activité de copie à partir de la source de données de destination tooa.</span><span class="sxs-lookup"><span data-stu-id="e832d-232">For example, a Copy Activity toocopy data from a source tooa destination data store.</span></span> <span data-ttu-id="e832d-233">Un toorun d’activité HDInsight Hive un tootransform de script Hive les données de sortie de tooproduct de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="e832d-233">A HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="e832d-234">Exécutez hello suivant la fabrique de données de commandes toocreate hello :</span><span class="sxs-lookup"><span data-stu-id="e832d-234">Run hello following commands toocreate hello data factory:</span></span> 

1. <span data-ttu-id="e832d-235">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="e832d-235">Assign hello command toovariable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="e832d-236">Confirmer ce nom hello hello fabrique de données vous spécifiez ici les correspondances (ADFCopyTutorialDF) hello nom spécifié dans hello **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="e832d-236">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="e832d-237">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="e832d-237">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="e832d-238">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-238">View hello results.</span></span> <span data-ttu-id="e832d-239">Si la fabrique de données hello a été créé avec succès, vous voyez hello JSON de fabrique de données hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="e832d-239">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="e832d-240">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="e832d-240">Note hello following points:</span></span>

* <span data-ttu-id="e832d-241">nom de Hello Hello Azure Data Factory doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="e832d-241">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="e832d-242">Si vous voyez l’erreur hello dans les résultats : **nom de fabrique de données « ADFCopyTutorialDF » n’est pas disponible**, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e832d-242">If you see hello error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do hello following steps:</span></span>  
  
  1. <span data-ttu-id="e832d-243">Modifier le nom hello (par exemple, yournameADFCopyTutorialDF) Bonjour **datafactory.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="e832d-243">Change hello name (for example, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span></span>
  2. <span data-ttu-id="e832d-244">Dans la première commande de hello où hello **$cmd** une valeur est assignée à la variable, remplacez ADFCopyTutorialDF avec le nouveau nom de hello et exécutez la commande hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-244">In hello first command where hello **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with hello new name and run hello command.</span></span> 
  3. <span data-ttu-id="e832d-245">Résultats de la série hello deux commandes tooinvoke hello API REST toocreate hello données fabrique et impression hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-245">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span> 
     
     <span data-ttu-id="e832d-246">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e832d-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="e832d-247">instances de fabrique de données toocreate, vous devez toobe un collaborateur/administrateur Hello abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="e832d-247">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="e832d-248">nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="e832d-248">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="e832d-249">Si vous recevez une erreur de hello : «**cet abonnement n’est pas un espace de noms inscrit toouse Microsoft.DataFactory**», effectuez l’une des manières suivantes les hello et essayez de publier à nouveau :</span><span class="sxs-lookup"><span data-stu-id="e832d-249">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="e832d-250">Dans Azure PowerShell, exécutez hello suivant le fournisseur de commandes tooregister hello fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="e832d-250">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="e832d-251">Vous pouvez exécuter hello suivant commande tooconfirm ce fournisseur est inscrit de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-251">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="e832d-252">Connexion à l’aide de hello abonnement Azure dans hello [portail Azure](https://portal.azure.com) et accédez Panneau de Data Factory tooa (ou) créer une fabrique de données Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-252">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="e832d-253">Cette action enregistre automatiquement le fournisseur hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="e832d-253">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="e832d-254">Avant de créer un pipeline, vous devez toocreate quelques entités de fabrique de données tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="e832d-254">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="e832d-255">Vous créez tout d’abord la source de toolink services liés et les données de destination stocke les données tooyour stocker.</span><span class="sxs-lookup"><span data-stu-id="e832d-255">You first create linked services toolink source and destination data stores tooyour data store.</span></span> <span data-ttu-id="e832d-256">Ensuite, définissez les jeux de données d’entrée et de sortie toorepresent données de magasins de données lié.</span><span class="sxs-lookup"><span data-stu-id="e832d-256">Then, define input and output datasets toorepresent data in linked data stores.</span></span> <span data-ttu-id="e832d-257">Enfin, créez le pipeline de hello avec une activité qui utilise ces jeux de données.</span><span class="sxs-lookup"><span data-stu-id="e832d-257">Finally, create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="e832d-258">Créez des services liés</span><span class="sxs-lookup"><span data-stu-id="e832d-258">Create linked services</span></span>
<span data-ttu-id="e832d-259">Vous créez des services liés dans un toolink de fabrique de données stocke de vos données et fabrique de données toohello de services de calcul.</span><span class="sxs-lookup"><span data-stu-id="e832d-259">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="e832d-260">Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e832d-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="e832d-261">Vous utilisez deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination).</span><span class="sxs-lookup"><span data-stu-id="e832d-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="e832d-262">Vous créez ainsi deux services liés nommés AzureStorageLinkedService et AzureSqlLinkedService de types : AzureStorage et AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="e832d-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="e832d-263">Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-263">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="e832d-264">Ce compte de stockage est hello une dans laquelle vous créé un conteneur et à télécharger des données de hello dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="e832d-264">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="e832d-265">AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-265">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="e832d-266">données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="e832d-266">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="e832d-267">Vous avez créé la table emp de hello dans cette base de données dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="e832d-267">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="e832d-268">Créer le service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="e832d-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="e832d-269">Dans cette étape, vous liez votre fabrique de données tooyour compte stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-269">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="e832d-270">Vous spécifiez le nom de hello et la clé de votre compte de stockage Azure dans cette section.</span><span class="sxs-lookup"><span data-stu-id="e832d-270">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="e832d-271">Consultez [service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour plus d’informations sur JSON propriétés utilisées toodefine un stockage Azure le service lié.</span><span class="sxs-lookup"><span data-stu-id="e832d-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="e832d-272">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="e832d-272">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="e832d-273">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="e832d-273">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="e832d-274">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-274">View hello results.</span></span> <span data-ttu-id="e832d-275">Si hello lié service a été créé avec succès, vous voyez hello JSON pour le service lié de hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="e832d-275">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="e832d-276">Créer un service lié Azure SQL</span><span class="sxs-lookup"><span data-stu-id="e832d-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="e832d-277">Dans cette étape, vous liez votre fabrique de données de tooyour de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-277">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="e832d-278">Vous spécifiez le nom du serveur SQL Azure hello, nom de la base de données, nom d’utilisateur et mot de passe utilisateur dans cette section.</span><span class="sxs-lookup"><span data-stu-id="e832d-278">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="e832d-279">Consultez [service lié Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) pour plus d’informations sur JSON propriétés utilisées toodefine service lié de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>

1. <span data-ttu-id="e832d-280">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="e832d-280">Assign hello command toovariable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="e832d-281">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="e832d-281">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="e832d-282">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-282">View hello results.</span></span> <span data-ttu-id="e832d-283">Si hello lié service a été créé avec succès, vous voyez hello JSON pour le service lié de hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="e832d-283">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="e832d-284">Créez les jeux de données</span><span class="sxs-lookup"><span data-stu-id="e832d-284">Create datasets</span></span>
<span data-ttu-id="e832d-285">Dans l’étape précédente de hello, vous avez créé toolink de services liés de votre compte de stockage Azure et de la fabrique de données de tooyour de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-285">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="e832d-286">Dans cette étape, vous définissez deux jeux de données nommées AzureBlobInput et AzureSqlOutput qui représentent une entrée et les données de sortie qui sont stockées dans des magasins de données hello visés par AzureStorageLinkedService et AzureSqlLinkedService, respectivement.</span><span class="sxs-lookup"><span data-stu-id="e832d-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="e832d-287">service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-287">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="e832d-288">Et, le jeu de données objet blob d’entrée hello (AzureBlobInput) spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-288">And, hello input blob dataset (AzureBlobInput) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="e832d-289">De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="e832d-289">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="e832d-290">Et, hello sortie de jeu de données de table SQL (OututDataset) spécifie la table de hello Bonjour de toowhich hello de base de données à partir du stockage d’objets blob hello, les données sont copiées.</span><span class="sxs-lookup"><span data-stu-id="e832d-290">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="e832d-291">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="e832d-291">Create input dataset</span></span>
<span data-ttu-id="e832d-292">Dans cette étape, vous créez un dataset nommé AzureBlobInput qui pointe le fichier d’objet blob tooa (emp.txt) dans le dossier racine de hello d’un conteneur d’objets blob (adftutorial) Bonjour Azure Storage est représenté par hello AzureStorageLinkedService lié service.</span><span class="sxs-lookup"><span data-stu-id="e832d-292">In this step, you create a dataset named AzureBlobInput that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="e832d-293">Si vous ne spécifiez une valeur pour le nom de fichier hello (ignorer), les données à partir de tous les objets BLOB dans le dossier d’entrée de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="e832d-293">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="e832d-294">Dans ce didacticiel, vous spécifiez une valeur pour le nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-294">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="e832d-295">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="e832d-295">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="e832d-296">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="e832d-296">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="e832d-297">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-297">View hello results.</span></span> <span data-ttu-id="e832d-298">Si hello dataset a été créé avec succès, vous voyez hello JSON pour le dataset hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="e832d-298">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="e832d-299">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="e832d-299">Create output dataset</span></span>
<span data-ttu-id="e832d-300">Hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="e832d-300">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="e832d-301">Hello SQL table dataset de sortie (OututDataset) vous créez dans cette étape spécifie table hello dans les données de hello toowhich hello de base de données à partir du stockage d’objets blob hello est copiée.</span><span class="sxs-lookup"><span data-stu-id="e832d-301">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="e832d-302">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="e832d-302">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="e832d-303">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="e832d-303">Run hello command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="e832d-304">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-304">View hello results.</span></span> <span data-ttu-id="e832d-305">Si hello dataset a été créé avec succès, vous voyez hello JSON pour le dataset hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="e832d-305">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="e832d-306">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="e832d-306">Create pipeline</span></span>
<span data-ttu-id="e832d-307">Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **AzureBlobInput** en entrée et **AzureSqlOutput** en sortie.</span><span class="sxs-lookup"><span data-stu-id="e832d-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="e832d-308">Actuellement, le dataset de sortie est les lecteurs hello planification.</span><span class="sxs-lookup"><span data-stu-id="e832d-308">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="e832d-309">Dans ce didacticiel, le dataset de sortie est tooproduce configuré une tranche une fois par heure.</span><span class="sxs-lookup"><span data-stu-id="e832d-309">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="e832d-310">pipeline de Hello a une heure de début et l’heure de fin sont un jour séparé, ce qui est de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="e832d-310">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="e832d-311">Par conséquent, 24 tranches du jeu de données de sortie produits par le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-311">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="e832d-312">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="e832d-312">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="e832d-313">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="e832d-313">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="e832d-314">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-314">View hello results.</span></span> <span data-ttu-id="e832d-315">Si hello dataset a été créé avec succès, vous voyez hello JSON pour le dataset hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="e832d-315">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="e832d-316">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="e832d-316">**Congratulations!**</span></span> <span data-ttu-id="e832d-317">Vous venez de créer une fabrique de données Azure, avec un pipeline qui copie les données à partir de la base de données SQL Azure Blob Storage tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e832d-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage tooAzure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="e832d-318">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="e832d-318">Monitor pipeline</span></span>
<span data-ttu-id="e832d-319">Dans cette étape, vous utilisez tranches de toomonitor API REST de fabrique données produits par le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-319">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="e832d-320">Assurez-vous que Démarrer de hello et heures spécifiées dans hello suivant de fin commande correspondance hello début et fin du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-320">Make sure that hello start and end times specified in hello following command match hello start and end times of hello pipeline.</span></span> 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

<span data-ttu-id="e832d-321">Exécutez hello Invoke-Command et hello suivant jusqu'à ce que vous voyiez un secteur dans **prêt** état ou **n’a pas pu** état.</span><span class="sxs-lookup"><span data-stu-id="e832d-321">Run hello Invoke-Command and hello next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="e832d-322">Lors de la tranche de hello est prêt, vérifiez hello **emp** table dans votre base de données SQL Azure pour les données de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-322">When hello slice is in Ready state, check hello **emp** table in your Azure SQL database for hello output data.</span></span> 

<span data-ttu-id="e832d-323">Pour chaque secteur, deux lignes de données à partir du fichier de source de hello sont table emp de toohello copiés dans la base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-323">For each slice, two rows of data from hello source file are copied toohello emp table in hello Azure SQL database.</span></span> <span data-ttu-id="e832d-324">Par conséquent, vous voyez 24 nouveaux enregistrements dans la table emp de hello lorsque toutes les tranches de hello sont traitées avec succès (dans l’état prêt).</span><span class="sxs-lookup"><span data-stu-id="e832d-324">Therefore, you see 24 new records in hello emp table when all hello slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="e832d-325">Résumé</span><span class="sxs-lookup"><span data-stu-id="e832d-325">Summary</span></span>
<span data-ttu-id="e832d-326">Dans ce didacticiel, vous avez utilisé les API REST toocreate un Azure fabrique toocopy de données à partir d’une base de données SQL Azure de tooan objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-326">In this tutorial, you used REST API toocreate an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="e832d-327">Voici les étapes principales hello que vous avez effectuées dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="e832d-327">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="e832d-328">Création d’une **fabrique de données**Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="e832d-329">Création de **services liés**:</span><span class="sxs-lookup"><span data-stu-id="e832d-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="e832d-330">Un stockage Azure lié à service toolink votre compte de stockage Azure qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="e832d-330">An Azure Storage linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="e832d-331">SQL Azure lié à service toolink votre base de données SQL Azure qui contient les données de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-331">An Azure SQL linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="e832d-332">Création des **jeux de données**qui décrivent les données d’entrée et de sortie des pipelines.</span><span class="sxs-lookup"><span data-stu-id="e832d-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="e832d-333">Création d’un **pipeline** avec une activité de copie avec BlobSource en tant que source et SqlSink en tant que récepteur.</span><span class="sxs-lookup"><span data-stu-id="e832d-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e832d-334">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e832d-334">Next steps</span></span>
<span data-ttu-id="e832d-335">Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie.</span><span class="sxs-lookup"><span data-stu-id="e832d-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="e832d-336">Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello :</span><span class="sxs-lookup"><span data-stu-id="e832d-336">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="e832d-337">toolearn sur la banque de données de toocopy vers/à partir de données, cliquez sur lien hello hello magasin de données dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-337">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
