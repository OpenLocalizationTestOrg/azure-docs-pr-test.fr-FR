---
title: "aaaGet main Analytique de LAC de données Azure à l’aide d’Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toouse hello une Interface de ligne de Azure 2.0 toocreate un compte Analytique lac de données, créez une tâche Analytique lac de données à l’aide de U-SQL et envoi de la tâche de hello. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="13ebb-103">Prise en main d’Azure Data Lake Analytics à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="13ebb-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="13ebb-104">Dans ce didacticiel, vous développez un travail qui lit un fichier TSV (valeurs séparées par des tabulations) et le convertit en fichier CSV (valeurs séparées par des virgules).</span><span class="sxs-lookup"><span data-stu-id="13ebb-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="13ebb-105">toogo hello même didacticiel d’autres prises en charge par le biais des outils, utiliser la liste déroulante hello haut hello de cette section.</span><span class="sxs-lookup"><span data-stu-id="13ebb-105">toogo through hello same tutorial using other supported tools, use hello dropdown list on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13ebb-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="13ebb-106">Prerequisites</span></span>
<span data-ttu-id="13ebb-107">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="13ebb-107">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="13ebb-108">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="13ebb-108">**An Azure subscription**.</span></span> <span data-ttu-id="13ebb-109">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13ebb-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="13ebb-110">**Azure CLI 2.0**.</span><span class="sxs-lookup"><span data-stu-id="13ebb-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="13ebb-111">Consultez [Installation et configuration de l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="13ebb-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="13ebb-112">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="13ebb-112">Log in tooAzure</span></span>

<span data-ttu-id="13ebb-113">toolog dans tooyour abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="13ebb-113">toolog in tooyour Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="13ebb-114">Vous êtes demandé toobrowse tooa URL et que vous entrez un code d’authentification.</span><span class="sxs-lookup"><span data-stu-id="13ebb-114">You are requested toobrowse tooa URL, and enter an authentication code.</span></span>  <span data-ttu-id="13ebb-115">Puis suivez hello instructions tooenter vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="13ebb-115">And then follow hello instructions tooenter your credentials.</span></span>

<span data-ttu-id="13ebb-116">Une fois que vous êtes connecté, la commande de connexion hello répertorie vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="13ebb-116">Once you have logged in, hello login command lists your subscriptions.</span></span>

<span data-ttu-id="13ebb-117">toouse un abonnement spécifique :</span><span class="sxs-lookup"><span data-stu-id="13ebb-117">toouse a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="13ebb-118">Créer un compte Analytique Data Lake</span><span class="sxs-lookup"><span data-stu-id="13ebb-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="13ebb-119">Vous devez disposer d’un compte Data Lake Analytics avant de pouvoir exécuter des travaux quelconques.</span><span class="sxs-lookup"><span data-stu-id="13ebb-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="13ebb-120">toocreate un compte Analytique lac de données, vous devez spécifier hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="13ebb-120">toocreate a Data Lake Analytics account, you must specify hello following items:</span></span>

* <span data-ttu-id="13ebb-121">**Groupe de ressources Azure**.</span><span class="sxs-lookup"><span data-stu-id="13ebb-121">**Azure Resource Group**.</span></span> <span data-ttu-id="13ebb-122">Un compte Data Lake Analytics doit être créé au sein d’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="13ebb-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="13ebb-123">[Le Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md) vous permet de toowork avec des ressources hello dans votre application en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="13ebb-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you toowork with hello resources in your application as a group.</span></span> <span data-ttu-id="13ebb-124">Vous pouvez déployer, mettre à jour ou supprimer toutes les ressources de hello pour votre application dans une opération unique et coordonnée.</span><span class="sxs-lookup"><span data-stu-id="13ebb-124">You can deploy, update, or delete all of hello resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="13ebb-125">toolist hello des groupes de ressource sous votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="13ebb-125">toolist hello existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="13ebb-126">toocreate un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="13ebb-126">toocreate a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="13ebb-127">**Nom du compte Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="13ebb-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="13ebb-128">Chaque compte Data Lake Analytics porte un nom.</span><span class="sxs-lookup"><span data-stu-id="13ebb-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="13ebb-129">**Emplacement**.</span><span class="sxs-lookup"><span data-stu-id="13ebb-129">**Location**.</span></span> <span data-ttu-id="13ebb-130">Utilisez une des centres de données Azure hello qui prend en charge les données de LAC Analytique.</span><span class="sxs-lookup"><span data-stu-id="13ebb-130">Use one of hello Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="13ebb-131">**Compte Data Lake Store par défaut** : chaque compte Data Lake Analytics possède un compte Data Lake Store par défaut.</span><span class="sxs-lookup"><span data-stu-id="13ebb-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="13ebb-132">toolist hello Data Lake Store compte existant :</span><span class="sxs-lookup"><span data-stu-id="13ebb-132">toolist hello existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="13ebb-133">toocreate un nouveau compte Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="13ebb-133">toocreate a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="13ebb-134">Utilisez hello suivant de syntaxe toocreate un compte Analytique lac de données :</span><span class="sxs-lookup"><span data-stu-id="13ebb-134">Use hello following syntax toocreate a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="13ebb-135">Après avoir créé un compte, vous pouvez utiliser les hello suivant des comptes de commandes toolist hello et afficher les détails du compte :</span><span class="sxs-lookup"><span data-stu-id="13ebb-135">After creating an account, you can use hello following commands toolist hello accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a><span data-ttu-id="13ebb-136">Télécharger des données tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="13ebb-136">Upload data tooData Lake Store</span></span>
<span data-ttu-id="13ebb-137">Dans ce didacticiel, vous traitez des journaux de recherche.</span><span class="sxs-lookup"><span data-stu-id="13ebb-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="13ebb-138">journal des recherches Hello peut être stockée dans le magasin de LAC de données ou le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="13ebb-138">hello search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="13ebb-139">Hello portail Azure fournit une interface utilisateur pour la copie de certains exemples données fichiers toohello par défaut compte Data Lake Store, qui incluent un fichier journal de recherche.</span><span class="sxs-lookup"><span data-stu-id="13ebb-139">hello Azure portal provides a user interface for copying some sample data files toohello default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="13ebb-140">Consultez [préparer les données sources](data-lake-analytics-get-started-portal.md) compte Data Lake Store de tooupload hello données toohello par défaut.</span><span class="sxs-lookup"><span data-stu-id="13ebb-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) tooupload hello data toohello default Data Lake Store account.</span></span>

<span data-ttu-id="13ebb-141">fichiers tooupload à l’aide de la version 2.0 CLI, utilisez hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="13ebb-141">tooupload files using CLI 2.0, use hello following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="13ebb-142">Analytique Data Lake peut également accéder au stockage d’objets blobs Azure.</span><span class="sxs-lookup"><span data-stu-id="13ebb-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="13ebb-143">Pour télécharger le stockage d’objets Blob de données tooAzure, consultez [Using hello CLI d’Azure avec le stockage Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="13ebb-143">For uploading data tooAzure Blob storage, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="13ebb-144">Envoyer des travaux Analytique Data Lake</span><span class="sxs-lookup"><span data-stu-id="13ebb-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="13ebb-145">travaux de Hello Analytique lac de données est écrites dans hello langage U-SQL.</span><span class="sxs-lookup"><span data-stu-id="13ebb-145">hello Data Lake Analytics jobs are written in hello U-SQL language.</span></span> <span data-ttu-id="13ebb-146">toolearn en savoir plus sur U-SQL, consultez [prise en main langage U-SQL](data-lake-analytics-u-sql-get-started.md) et [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="13ebb-146">toolearn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="13ebb-147">**toocreate un script de travail Analytique lac de données**</span><span class="sxs-lookup"><span data-stu-id="13ebb-147">**toocreate a Data Lake Analytics job script**</span></span>

<span data-ttu-id="13ebb-148">Créez un fichier texte avec le script U-SQL suivant, enregistrez la station de travail hello texte fichier tooyour :</span><span class="sxs-lookup"><span data-stu-id="13ebb-148">Create a text file with following U-SQL script, and save hello text file tooyour workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="13ebb-149">Ce script U-SQL lit le fichier de données source hello via **Extractors.Tsv()**, puis crée un fichier csv en utilisant **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="13ebb-149">This U-SQL script reads hello source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="13ebb-150">Ne modifiez pas deux chemins d’accès de hello, sauf si vous copiez le fichier de source de hello dans un autre emplacement.</span><span class="sxs-lookup"><span data-stu-id="13ebb-150">Don't modify hello two paths unless you copy hello source file into a different location.</span></span>  <span data-ttu-id="13ebb-151">Analytique de LAC de données crée le dossier de sortie hello si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="13ebb-151">Data Lake Analytics creates hello output folder if it doesn't exist.</span></span>

<span data-ttu-id="13ebb-152">Il est plus simples toouse chemins d’accès relatifs pour les fichiers stockés sur les comptes Data Lake Store par défaut.</span><span class="sxs-lookup"><span data-stu-id="13ebb-152">It is simpler toouse relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="13ebb-153">Vous pouvez également utiliser des chemins d’accès absolus.</span><span class="sxs-lookup"><span data-stu-id="13ebb-153">You can also use absolute paths.</span></span>  <span data-ttu-id="13ebb-154">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="13ebb-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="13ebb-155">Vous devez utiliser des chemins d’accès absolus des fichiers de tooaccess dans les comptes de stockage liés.</span><span class="sxs-lookup"><span data-stu-id="13ebb-155">You must use absolute paths tooaccess files in linked Storage accounts.</span></span>  <span data-ttu-id="13ebb-156">syntaxe de Hello pour les fichiers stockés dans le compte de stockage Azure associé est la suivante :</span><span class="sxs-lookup"><span data-stu-id="13ebb-156">hello syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="13ebb-157">Conteneur d’objets Blob Azure avec des objets Blob publics ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="13ebb-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="13ebb-158">Le conteneur d’objets Blob Azure avec des conteneurs publics n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="13ebb-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="13ebb-159">**travaux de toosubmit**</span><span class="sxs-lookup"><span data-stu-id="13ebb-159">**toosubmit jobs**</span></span>

<span data-ttu-id="13ebb-160">Utilisez hello suivant de syntaxe toosubmit un travail.</span><span class="sxs-lookup"><span data-stu-id="13ebb-160">Use hello following syntax toosubmit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="13ebb-161">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="13ebb-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="13ebb-162">**travaux de toolist et afficher les détails de travail**</span><span class="sxs-lookup"><span data-stu-id="13ebb-162">**toolist jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="13ebb-163">**travaux de toocancel**</span><span class="sxs-lookup"><span data-stu-id="13ebb-163">**toocancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="13ebb-164">Récupérer les résultats de travaux</span><span class="sxs-lookup"><span data-stu-id="13ebb-164">Retrieve job results</span></span>

<span data-ttu-id="13ebb-165">Lorsqu’un travail est terminé, vous pouvez utiliser hello suivant des fichiers de sortie de commandes toolist hello et télécharger les fichiers de hello :</span><span class="sxs-lookup"><span data-stu-id="13ebb-165">After a job is completed, you can use hello following commands toolist hello output files, and download hello files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="13ebb-166">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="13ebb-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="13ebb-167">Pipelines et récurrences</span><span class="sxs-lookup"><span data-stu-id="13ebb-167">Pipelines and recurrences</span></span>

<span data-ttu-id="13ebb-168">**Obtenir des informations sur les pipelines et les récurrences**</span><span class="sxs-lookup"><span data-stu-id="13ebb-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="13ebb-169">Hello d’utilisation `az dla job pipeline` commandes informations de pipeline toosee hello envoyés précédemment des travaux.</span><span class="sxs-lookup"><span data-stu-id="13ebb-169">Use hello `az dla job pipeline` commands toosee hello pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="13ebb-170">Hello d’utilisation `az dla job recurrence` commandes d’informations sur la périodicité toosee hello pour les travaux soumis précédemment.</span><span class="sxs-lookup"><span data-stu-id="13ebb-170">Use hello `az dla job recurrence` commands toosee hello recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="13ebb-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13ebb-171">Next steps</span></span>

* <span data-ttu-id="13ebb-172">toosee hello Data Lake Analytique CLI 2.0 de document de référence, consultez [Analytique lac de données](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="13ebb-172">toosee hello Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="13ebb-173">toosee hello Data Lake Store CLI 2.0 de document de référence, consultez [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="13ebb-173">toosee hello Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="13ebb-174">toosee une requête plus complexe, consultez [site Web d’analyse se connecte à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="13ebb-174">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
