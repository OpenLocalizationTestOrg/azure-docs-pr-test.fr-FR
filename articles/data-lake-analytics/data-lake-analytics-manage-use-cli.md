---
title: "aaaManage Analytique de LAC de données Azure à l’aide d’une Interface de ligne Azure | Documents Microsoft"
description: "Découvrez comment les comptes toomanage Analytique lac de données, sources de données, des travaux et des utilisateurs à l’aide de CLI d’Azure"
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
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="48b01-103">Gestion de Azure Data Lake Analytics à l’aide de l’interface de ligne de commande Azure (CLI)</span><span class="sxs-lookup"><span data-stu-id="48b01-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="48b01-104">Découvrez comment des comptes toomanage Analytique de LAC de données Azure, des sources de données, des utilisateurs et des travaux à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="48b01-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure CLI.</span></span> <span data-ttu-id="48b01-105">les rubriques de gestion toosee à l’aide d’autres outils, cliquez sur l’onglet hello ci-dessus, sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="48b01-105">toosee management topics using other tools, click hello tab select above.</span></span>


<span data-ttu-id="48b01-106">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="48b01-106">**Prerequisites**</span></span>

<span data-ttu-id="48b01-107">Avant de commencer ce didacticiel, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="48b01-107">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="48b01-108">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="48b01-108">**An Azure subscription**.</span></span> <span data-ttu-id="48b01-109">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48b01-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="48b01-110">**Interface de ligne de commande Azure**.</span><span class="sxs-lookup"><span data-stu-id="48b01-110">**Azure CLI**.</span></span> <span data-ttu-id="48b01-111">Consultez [Installation et configuration de l’interface de ligne de commande Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="48b01-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="48b01-112">Téléchargez et installez hello **préliminaires** [outils CLI d’Azure](https://github.com/MicrosoftBigData/AzureDataLake/releases) commander toocomplete cette démonstration.</span><span class="sxs-lookup"><span data-stu-id="48b01-112">Download and install hello **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order toocomplete this demo.</span></span>
* <span data-ttu-id="48b01-113">**Authentification**, à l’aide hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="48b01-113">**Authentication**, using hello following command:</span></span>
  
        azure login
    <span data-ttu-id="48b01-114">Pour plus d’informations sur l’authentification à l’aide d’un compte professionnel ou scolaire, consultez [connecter tooan abonnement Azure à partir de hello CLI d’Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="48b01-114">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="48b01-115">**Passez en mode Azure Resource Manager de toohello**, à l’aide hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="48b01-115">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="48b01-116">**toolist hello Data Lake Store et Analytique lac de données de commandes :**</span><span class="sxs-lookup"><span data-stu-id="48b01-116">**toolist hello Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="48b01-117">Gérer les comptes</span><span class="sxs-lookup"><span data-stu-id="48b01-117">Manage accounts</span></span>
<span data-ttu-id="48b01-118">Avant d'exécuter des travaux Data Lake Analytics, vous devez avoir un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="48b01-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="48b01-119">Contrairement à Azure HDInsight, vous ne payez pas pour un compte Analytics lorsque celui-ci n'exécute aucun travail.</span><span class="sxs-lookup"><span data-stu-id="48b01-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="48b01-120">Vous payez uniquement pour fois hello lorsqu’il exécute un travail.</span><span class="sxs-lookup"><span data-stu-id="48b01-120">You only pay for hello time when it is running a job.</span></span>  <span data-ttu-id="48b01-121">Pour plus d'informations, consultez [Présentation d'Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48b01-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="48b01-122">Création de comptes</span><span class="sxs-lookup"><span data-stu-id="48b01-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="48b01-123">Mise à jour de comptes</span><span class="sxs-lookup"><span data-stu-id="48b01-123">Update accounts</span></span>
<span data-ttu-id="48b01-124">Hello commande suivante met à jour les propriétés de hello d’un compte d’Analytique Data Lake existant</span><span class="sxs-lookup"><span data-stu-id="48b01-124">hello following command updates hello properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="48b01-125">Énumérer les comptes</span><span class="sxs-lookup"><span data-stu-id="48b01-125">List accounts</span></span>
<span data-ttu-id="48b01-126">Énumérer les comptes Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="48b01-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="48b01-127">Répertorier les comptes Data Lake Analytics dans un groupe de ressources spécifique</span><span class="sxs-lookup"><span data-stu-id="48b01-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="48b01-128">Obtenir des détails sur un compte Data Lake Analytics spécifique</span><span class="sxs-lookup"><span data-stu-id="48b01-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="48b01-129">Supprimer les comptes Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="48b01-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="48b01-130">Gestion des sources de données du compte</span><span class="sxs-lookup"><span data-stu-id="48b01-130">Manage account data sources</span></span>
<span data-ttu-id="48b01-131">Analytique lac de données prend en charge actuellement les hello les sources de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="48b01-131">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="48b01-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="48b01-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="48b01-133">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="48b01-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="48b01-134">Lorsque vous créez un compte Analytique, vous devez désigner un compte de stockage par défaut de stockage de LAC de données Azure compte toobe hello.</span><span class="sxs-lookup"><span data-stu-id="48b01-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account toobe hello default storage account.</span></span> <span data-ttu-id="48b01-135">Hello compte de stockage par défaut ADL sert toostore métadonnée de la tâche et le travail de journaux d’audit.</span><span class="sxs-lookup"><span data-stu-id="48b01-135">hello default ADL storage account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="48b01-136">Après la création d'un compte Analytics, vous pouvez ajouter des comptes Data Lake Storage et/ou des comptes Azure Storage supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="48b01-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-hello-default-adl-storage-account"></a><span data-ttu-id="48b01-137">Recherchez le compte de stockage ADL hello par défaut</span><span class="sxs-lookup"><span data-stu-id="48b01-137">Find hello default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="48b01-138">valeur de Hello est répertorié sous propriétés : datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="48b01-138">hello value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="48b01-139">Ajouter des comptes de stockage d'objets Blob Azure supplémentaires</span><span class="sxs-lookup"><span data-stu-id="48b01-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="48b01-140">Seuls les noms courts Blob Storage sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="48b01-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="48b01-141">N'utilisez pas de nom de domaine complet, comme « myblob.blob.core.windows.net ».</span><span class="sxs-lookup"><span data-stu-id="48b01-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="48b01-142">Ajouter des comptes Data Lake Store supplémentaires</span><span class="sxs-lookup"><span data-stu-id="48b01-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="48b01-143">[-d] est un tooindicate commutateur facultatif si hello lac de données ajouté est le compte Data Lake n’hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="48b01-143">[-d] is an optional switch tooindicate whether hello Data Lake being added is hello default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="48b01-144">Mettre à jour la source de données existante</span><span class="sxs-lookup"><span data-stu-id="48b01-144">Update existing data source</span></span>
<span data-ttu-id="48b01-145">tooset une valeur par défaut de hello toobe existante Data Lake Store compte :</span><span class="sxs-lookup"><span data-stu-id="48b01-145">tooset an existing Data Lake Store account toobe hello default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="48b01-146">tooupdate une clé de compte de stockage Blob :</span><span class="sxs-lookup"><span data-stu-id="48b01-146">tooupdate an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="48b01-147">Répertorier les sources de données :</span><span class="sxs-lookup"><span data-stu-id="48b01-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics : énumérer les sources de données](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="48b01-149">Supprimer des sources de données :</span><span class="sxs-lookup"><span data-stu-id="48b01-149">Delete data sources:</span></span>
<span data-ttu-id="48b01-150">toodelete un compte Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="48b01-150">toodelete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="48b01-151">toodelete un compte de stockage d’objets Blob :</span><span class="sxs-lookup"><span data-stu-id="48b01-151">toodelete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="48b01-152">Gestion des travaux</span><span class="sxs-lookup"><span data-stu-id="48b01-152">Manage jobs</span></span>
<span data-ttu-id="48b01-153">Vous devez disposer d'un compte Data Lake Analytics avant de pouvoir créer un travail.</span><span class="sxs-lookup"><span data-stu-id="48b01-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="48b01-154">Pour plus d'informations, consultez [Gestion des comptes Data Lake Analytics](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="48b01-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="48b01-155">Répertorier les travaux</span><span class="sxs-lookup"><span data-stu-id="48b01-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics : énumérer les sources de données](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="48b01-157">Obtenir les détails du travail</span><span class="sxs-lookup"><span data-stu-id="48b01-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="48b01-158">Soumettre les travaux</span><span class="sxs-lookup"><span data-stu-id="48b01-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="48b01-159">priorité par défaut de Hello d’une tâche est comprise entre 1000 et hello par défaut de parallélisme pour un travail est 1.</span><span class="sxs-lookup"><span data-stu-id="48b01-159">hello default priority of a job is 1000, and hello default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="48b01-160">Annuler les travaux</span><span class="sxs-lookup"><span data-stu-id="48b01-160">Cancel jobs</span></span>
<span data-ttu-id="48b01-161">Utilisez l’id de tâche hello liste commande toofind hello et utilisez annulation du travail toocancel hello.</span><span class="sxs-lookup"><span data-stu-id="48b01-161">Use hello list command toofind hello job id, and then use cancel toocancel hello job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="48b01-162">Gestion du catalogue</span><span class="sxs-lookup"><span data-stu-id="48b01-162">Manage catalog</span></span>
<span data-ttu-id="48b01-163">catalogue de Hello U-SQL est utilisé toostructure données et le code afin qu’ils peuvent être partagés par les scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="48b01-163">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="48b01-164">catalogue de Hello permet hello performances maximales des données dans Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="48b01-164">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="48b01-165">Pour plus d'informations, consultez [Utilisation du catalogue U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="48b01-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="48b01-166">Répertorier les éléments du catalogue</span><span class="sxs-lookup"><span data-stu-id="48b01-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="48b01-167">les types de Hello incluent la base de données, schéma, assembly, source de données externe, table, fonction table ou des statistiques de table.</span><span class="sxs-lookup"><span data-stu-id="48b01-167">hello types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="48b01-168">Utilisez des groupes ARM</span><span class="sxs-lookup"><span data-stu-id="48b01-168">Use ARM groups</span></span>
<span data-ttu-id="48b01-169">Les applications sont généralement constituées de nombreux composants, par exemple une application web, base de données, serveur de base de données, stockage et services tiers.</span><span class="sxs-lookup"><span data-stu-id="48b01-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="48b01-170">Azure Resource Manager (ARM) vous permet de toowork avec des ressources dans votre application comme une tooas de groupe, ou un groupe de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="48b01-170">Azure Resource Manager (ARM) enables you toowork with hello resources in your application as a group, referred tooas an Azure Resource Group.</span></span> <span data-ttu-id="48b01-171">Vous pouvez déployer, mettre à jour, analyser ou supprimer toutes les ressources de hello pour votre application dans une opération unique et coordonnée.</span><span class="sxs-lookup"><span data-stu-id="48b01-171">You can deploy, update, monitor or delete all of hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="48b01-172">Vous utilisez un modèle de déploiement pouvant fonctionner avec différents environnements (environnements de test, intermédiaire et de production).</span><span class="sxs-lookup"><span data-stu-id="48b01-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="48b01-173">Vous pouvez de clarifier la facturation pour votre organisation en consultant les coûts de hello reportées pour l’ensemble du groupe hello.</span><span class="sxs-lookup"><span data-stu-id="48b01-173">You can clarify billing for your organization by viewing hello rolled-up costs for hello entire group.</span></span> <span data-ttu-id="48b01-174">Pour plus d'informations, consultez [Présentation d'Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48b01-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="48b01-175">Un service de données Lake Analytique peut inclure hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="48b01-175">A Data Lake Analytics service can include hello following components:</span></span>

* <span data-ttu-id="48b01-176">Compte Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="48b01-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="48b01-177">Compte Azure Data Lake Storage par défaut requis</span><span class="sxs-lookup"><span data-stu-id="48b01-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="48b01-178">Comptes Azure Data Lake Storage supplémentaires</span><span class="sxs-lookup"><span data-stu-id="48b01-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="48b01-179">Comptes Azure Storage supplémentaires</span><span class="sxs-lookup"><span data-stu-id="48b01-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="48b01-180">Vous pouvez créer tous ces composants sous un toomake de groupe ARM les toomanage plus facile.</span><span class="sxs-lookup"><span data-stu-id="48b01-180">You can create all these components under one ARM group toomake them easier toomanage.</span></span>

![Compte et stockage Azure Data Lake Analytics](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="48b01-182">Un compte Analytique lac de données et les comptes de stockage dépendant de hello doivent être placés dans hello même centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="48b01-182">A Data Lake Analytics account and hello dependent storage accounts must be placed in hello same Azure data center.</span></span>
<span data-ttu-id="48b01-183">groupe de Hello ARM peut cependant se trouver dans un autre centre de données.</span><span class="sxs-lookup"><span data-stu-id="48b01-183">hello ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="48b01-184">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="48b01-184">See also</span></span>
* [<span data-ttu-id="48b01-185">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="48b01-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="48b01-186">Prise en main des analyses Data Lake à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="48b01-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="48b01-187">Gérer les analyses Azure Data Lake à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="48b01-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="48b01-188">Surveiller et résoudre les problèmes des tâches d’analyse Azure Data Lake à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="48b01-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

