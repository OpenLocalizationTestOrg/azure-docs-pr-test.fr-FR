---
title: "Gestion d’Azure Data Lake Analytics à l’aide de l’interface de ligne de commande Azure | Microsoft Docs"
description: "Apprenez à gérer des comptes Data Lake Analytics, des sources de données, des utilisateurs et des travaux à l'aide de l’interface de ligne de commande Azure."
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f90bada3572c0ed40b07d76ec02c1b499bbd1428
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="8089b-103">Gestion de Azure Data Lake Analytics à l’aide de l’interface de ligne de commande Azure (CLI)</span><span class="sxs-lookup"><span data-stu-id="8089b-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="8089b-104">Découvrez comment gérer des comptes Azure Data Lake Analytics, des sources de données, des utilisateurs et des travaux à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="8089b-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI.</span></span> <span data-ttu-id="8089b-105">Pour afficher les rubriques de gestion à l’aide d’autres outils, cliquez sur l’onglet de sélection ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8089b-105">To see management topics using other tools, click the tab select above.</span></span>


<span data-ttu-id="8089b-106">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="8089b-106">**Prerequisites**</span></span>

<span data-ttu-id="8089b-107">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8089b-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="8089b-108">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="8089b-108">**An Azure subscription**.</span></span> <span data-ttu-id="8089b-109">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8089b-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8089b-110">**Interface de ligne de commande Azure**.</span><span class="sxs-lookup"><span data-stu-id="8089b-110">**Azure CLI**.</span></span> <span data-ttu-id="8089b-111">Consultez [Installation et configuration de l’interface de ligne de commande Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8089b-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="8089b-112">Téléchargez et installez les **outils d’interface de ligne de commande Azure** [version préliminaire](https://github.com/MicrosoftBigData/AzureDataLake/releases) pour effectuer cette démonstration.</span><span class="sxs-lookup"><span data-stu-id="8089b-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>
* <span data-ttu-id="8089b-113">**Authentication**, en utilisant la commande  suivante :</span><span class="sxs-lookup"><span data-stu-id="8089b-113">**Authentication**, using the following command:</span></span>
  
        azure login
    <span data-ttu-id="8089b-114">Pour plus d’informations sur l’authentification à l’aide d’un compte professionnel ou scolaire, consultez la section [Se connecter à un abonnement Azure à partir de l’interface de ligne de commande Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8089b-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="8089b-115">**Passez en mode Azure Resource Manager**en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8089b-115">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="8089b-116">**Pour répertorier les commandes Data Lake Store et Data Lake Analytics :**</span><span class="sxs-lookup"><span data-stu-id="8089b-116">**To list the Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="8089b-117">Gérer les comptes</span><span class="sxs-lookup"><span data-stu-id="8089b-117">Manage accounts</span></span>
<span data-ttu-id="8089b-118">Avant d'exécuter des travaux Data Lake Analytics, vous devez avoir un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8089b-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="8089b-119">Contrairement à Azure HDInsight, vous ne payez pas pour un compte Analytics lorsque celui-ci n'exécute aucun travail.</span><span class="sxs-lookup"><span data-stu-id="8089b-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="8089b-120">Vous payez uniquement lorsqu'il exécute un travail.</span><span class="sxs-lookup"><span data-stu-id="8089b-120">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="8089b-121">Pour plus d'informations, consultez [Présentation d'Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8089b-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="8089b-122">Création de comptes</span><span class="sxs-lookup"><span data-stu-id="8089b-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="8089b-123">Mise à jour de comptes</span><span class="sxs-lookup"><span data-stu-id="8089b-123">Update accounts</span></span>
<span data-ttu-id="8089b-124">La commande suivante met à jour les propriétés d'un compte Data Lake Analytics existant</span><span class="sxs-lookup"><span data-stu-id="8089b-124">The following command updates the properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="8089b-125">Énumérer les comptes</span><span class="sxs-lookup"><span data-stu-id="8089b-125">List accounts</span></span>
<span data-ttu-id="8089b-126">Énumérer les comptes Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8089b-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="8089b-127">Répertorier les comptes Data Lake Analytics dans un groupe de ressources spécifique</span><span class="sxs-lookup"><span data-stu-id="8089b-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="8089b-128">Obtenir des détails sur un compte Data Lake Analytics spécifique</span><span class="sxs-lookup"><span data-stu-id="8089b-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="8089b-129">Supprimer les comptes Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8089b-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="8089b-130">Gestion des sources de données du compte</span><span class="sxs-lookup"><span data-stu-id="8089b-130">Manage account data sources</span></span>
<span data-ttu-id="8089b-131">Data Lake Analytics prend actuellement en charge les sources de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="8089b-131">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="8089b-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8089b-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="8089b-133">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8089b-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="8089b-134">Lorsque vous créez un compte Analytics, vous devez désigner un compte Azure Data Lake Storage comme compte de stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="8089b-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="8089b-135">Le compte de stockage ADL par défaut est utilisé pour stocker les métadonnées du travail et les journaux d'audit du travail.</span><span class="sxs-lookup"><span data-stu-id="8089b-135">The default ADL storage account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="8089b-136">Après la création d'un compte Analytics, vous pouvez ajouter des comptes Data Lake Storage et/ou des comptes Azure Storage supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8089b-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-adl-storage-account"></a><span data-ttu-id="8089b-137">Recherchez le compte de stockage ADL par défaut</span><span class="sxs-lookup"><span data-stu-id="8089b-137">Find the default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="8089b-138">La valeur est répertoriée sous properties:datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="8089b-138">The value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="8089b-139">Ajouter des comptes de stockage d'objets Blob Azure supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8089b-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="8089b-140">Seuls les noms courts Blob Storage sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="8089b-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="8089b-141">N'utilisez pas de nom de domaine complet, comme « myblob.blob.core.windows.net ».</span><span class="sxs-lookup"><span data-stu-id="8089b-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="8089b-142">Ajouter des comptes Data Lake Store supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8089b-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="8089b-143">[-d] est un commutateur facultatif pour indiquer si le Data Lake ajouté est le compte Data Lake par défaut.</span><span class="sxs-lookup"><span data-stu-id="8089b-143">[-d] is an optional switch to indicate whether the Data Lake being added is the default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="8089b-144">Mettre à jour la source de données existante</span><span class="sxs-lookup"><span data-stu-id="8089b-144">Update existing data source</span></span>
<span data-ttu-id="8089b-145">Pour faire d’un compte existant de magasin Data Lake un compte par défaut :</span><span class="sxs-lookup"><span data-stu-id="8089b-145">To set an existing Data Lake Store account to be the default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="8089b-146">Pour mettre à jour une clé de compte Blob Storage existante :</span><span class="sxs-lookup"><span data-stu-id="8089b-146">To update an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="8089b-147">Répertorier les sources de données :</span><span class="sxs-lookup"><span data-stu-id="8089b-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics : énumérer les sources de données](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="8089b-149">Supprimer des sources de données :</span><span class="sxs-lookup"><span data-stu-id="8089b-149">Delete data sources:</span></span>
<span data-ttu-id="8089b-150">Pour supprimer un compte de magasin Data Lake :</span><span class="sxs-lookup"><span data-stu-id="8089b-150">To delete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="8089b-151">Pour supprimer un compte de stockage Blob :</span><span class="sxs-lookup"><span data-stu-id="8089b-151">To delete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="8089b-152">Gestion des travaux</span><span class="sxs-lookup"><span data-stu-id="8089b-152">Manage jobs</span></span>
<span data-ttu-id="8089b-153">Vous devez disposer d'un compte Data Lake Analytics avant de pouvoir créer un travail.</span><span class="sxs-lookup"><span data-stu-id="8089b-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="8089b-154">Pour plus d'informations, consultez [Gestion des comptes Data Lake Analytics](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="8089b-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="8089b-155">Répertorier les travaux</span><span class="sxs-lookup"><span data-stu-id="8089b-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics : énumérer les sources de données](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="8089b-157">Obtenir les détails du travail</span><span class="sxs-lookup"><span data-stu-id="8089b-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="8089b-158">Soumettre les travaux</span><span class="sxs-lookup"><span data-stu-id="8089b-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="8089b-159">La priorité par défaut d'un travail est 1 000 et le degré de parallélisme par défaut d'un travail est 1.</span><span class="sxs-lookup"><span data-stu-id="8089b-159">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="8089b-160">Annuler les travaux</span><span class="sxs-lookup"><span data-stu-id="8089b-160">Cancel jobs</span></span>
<span data-ttu-id="8089b-161">Utilisez la commande list pour trouver l'id de travail, puis utilisez la fonction d’annulation pour annuler le travail.</span><span class="sxs-lookup"><span data-stu-id="8089b-161">Use the list command to find the job id, and then use cancel to cancel the job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="8089b-162">Gestion du catalogue</span><span class="sxs-lookup"><span data-stu-id="8089b-162">Manage catalog</span></span>
<span data-ttu-id="8089b-163">Le catalogue U-SQL est utilisé pour structurer les données et le code afin que les scripts U-SQL puissent les partager.</span><span class="sxs-lookup"><span data-stu-id="8089b-163">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="8089b-164">Le catalogue permet les meilleures performances possibles avec les données comprises dans Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8089b-164">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="8089b-165">Pour plus d'informations, consultez [Utilisation du catalogue U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="8089b-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="8089b-166">Répertorier les éléments du catalogue</span><span class="sxs-lookup"><span data-stu-id="8089b-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="8089b-167">Les types incluent : database, schema, assembly, external data source, table, table valued function ou table statistics.</span><span class="sxs-lookup"><span data-stu-id="8089b-167">The types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="8089b-168">Utilisez des groupes ARM</span><span class="sxs-lookup"><span data-stu-id="8089b-168">Use ARM groups</span></span>
<span data-ttu-id="8089b-169">Les applications sont généralement constituées de nombreux composants, par exemple une application web, base de données, serveur de base de données, stockage et services tiers.</span><span class="sxs-lookup"><span data-stu-id="8089b-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="8089b-170">Azure Resource Manager (ARM) vous permet de manipuler les ressources de votre application sous la forme d’un groupe, nommé groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8089b-170">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="8089b-171">Vous pouvez déployer, mettre à jour, surveiller ou supprimer toutes les ressources de votre application dans le cadre d’une opération unique et coordonnée.</span><span class="sxs-lookup"><span data-stu-id="8089b-171">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="8089b-172">Vous utilisez un modèle de déploiement pouvant fonctionner avec différents environnements (environnements de test, intermédiaire et de production).</span><span class="sxs-lookup"><span data-stu-id="8089b-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="8089b-173">Vous pouvez clarifier la facturation pour votre organisation en visualisant les coûts cumulés pour l’ensemble du groupe.</span><span class="sxs-lookup"><span data-stu-id="8089b-173">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="8089b-174">Pour plus d'informations, consultez [Présentation d'Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8089b-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="8089b-175">Un service Data Lake Analytics peut inclure les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="8089b-175">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="8089b-176">Compte Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8089b-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="8089b-177">Compte Azure Data Lake Storage par défaut requis</span><span class="sxs-lookup"><span data-stu-id="8089b-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="8089b-178">Comptes Azure Data Lake Storage supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8089b-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="8089b-179">Comptes Azure Storage supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8089b-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="8089b-180">Vous pouvez créer tous ces composants dans un groupe ARM pour les rendre plus facile à gérer.</span><span class="sxs-lookup"><span data-stu-id="8089b-180">You can create all these components under one ARM group to make them easier to manage.</span></span>

![Compte et stockage Azure Data Lake Analytics](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="8089b-182">Un compte Data Lake Analytics et les compte de stockage dépendants doivent se trouver dans le même centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="8089b-182">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="8089b-183">Le groupe ARM peut cependant se trouver dans un autre centre de données.</span><span class="sxs-lookup"><span data-stu-id="8089b-183">The ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="8089b-184">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8089b-184">See also</span></span>
* [<span data-ttu-id="8089b-185">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8089b-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="8089b-186">Prise en main des analyses Data Lake à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="8089b-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="8089b-187">Gérer les analyses Azure Data Lake à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="8089b-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="8089b-188">Surveiller et résoudre les problèmes des tâches d’analyse Azure Data Lake à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="8089b-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

