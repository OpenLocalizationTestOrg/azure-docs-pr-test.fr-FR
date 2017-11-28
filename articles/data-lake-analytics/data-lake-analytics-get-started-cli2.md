---
title: "Prise en main d’Azure Data Lake Analytics à l’aide de l’interface de ligne de commande Azure 2.0 | Microsoft Docs"
description: "Découvrez comment utiliser l’interface de ligne de commande Azure 2.0 pour créer un compte Data Lake Analytics, créer un travail Data Lake Analytics avec U-SQL et le soumettre. "
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
ms.openlocfilehash: fe2b84aac718ff5eddd4d73b5dc2120362952c1e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="9bd80-103">Prise en main d’Azure Data Lake Analytics à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9bd80-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="9bd80-104">Dans ce didacticiel, vous développez un travail qui lit un fichier TSV (valeurs séparées par des tabulations) et le convertit en fichier CSV (valeurs séparées par des virgules).</span><span class="sxs-lookup"><span data-stu-id="9bd80-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="9bd80-105">Pour suivre ce didacticiel même à l’aide d’autres outils pris en charge, utilisez la liste déroulante en haut de cette section.</span><span class="sxs-lookup"><span data-stu-id="9bd80-105">To go through the same tutorial using other supported tools, use the dropdown list on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bd80-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9bd80-106">Prerequisites</span></span>
<span data-ttu-id="9bd80-107">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9bd80-107">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="9bd80-108">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bd80-108">**An Azure subscription**.</span></span> <span data-ttu-id="9bd80-109">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9bd80-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9bd80-110">**Azure CLI 2.0**.</span><span class="sxs-lookup"><span data-stu-id="9bd80-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="9bd80-111">Consultez [Installation et configuration de l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9bd80-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="9bd80-112">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="9bd80-112">Log in to Azure</span></span>

<span data-ttu-id="9bd80-113">Pour vous connecter à votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="9bd80-113">To log in to your Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="9bd80-114">Vous êtes invité à accéder à une URL, et à entrer un code d’authentification.</span><span class="sxs-lookup"><span data-stu-id="9bd80-114">You are requested to browse to a URL, and enter an authentication code.</span></span>  <span data-ttu-id="9bd80-115">Ensuite, suivez les instructions pour entrer vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="9bd80-115">And then follow the instructions to enter your credentials.</span></span>

<span data-ttu-id="9bd80-116">Une fois que vous êtes connecté, la commande de connexion répertorie vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="9bd80-116">Once you have logged in, the login command lists your subscriptions.</span></span>

<span data-ttu-id="9bd80-117">Pour utiliser un abonnement spécifique :</span><span class="sxs-lookup"><span data-stu-id="9bd80-117">To use a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="9bd80-118">Créer un compte Analytique Data Lake</span><span class="sxs-lookup"><span data-stu-id="9bd80-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="9bd80-119">Vous devez disposer d’un compte Data Lake Analytics avant de pouvoir exécuter des travaux quelconques.</span><span class="sxs-lookup"><span data-stu-id="9bd80-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="9bd80-120">Pour créer un compte Data Lake Analytics, vous devez spécifier les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9bd80-120">To create a Data Lake Analytics account, you must specify the following items:</span></span>

* <span data-ttu-id="9bd80-121">**Groupe de ressources Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bd80-121">**Azure Resource Group**.</span></span> <span data-ttu-id="9bd80-122">Un compte Data Lake Analytics doit être créé au sein d’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd80-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="9bd80-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) vous permet de manipuler les ressources de votre application sous la forme d’un groupe.</span><span class="sxs-lookup"><span data-stu-id="9bd80-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="9bd80-124">Vous pouvez déployer, mettre à jour ou supprimer toutes les ressources de votre application dans le cadre d’une opération unique et coordonnée.</span><span class="sxs-lookup"><span data-stu-id="9bd80-124">You can deploy, update, or delete all of the resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="9bd80-125">Pour répertorier les groupes de ressources existants dans votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="9bd80-125">To list the existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="9bd80-126">Pour créer un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="9bd80-126">To create a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="9bd80-127">**Nom du compte Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="9bd80-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="9bd80-128">Chaque compte Data Lake Analytics porte un nom.</span><span class="sxs-lookup"><span data-stu-id="9bd80-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="9bd80-129">**Emplacement**.</span><span class="sxs-lookup"><span data-stu-id="9bd80-129">**Location**.</span></span> <span data-ttu-id="9bd80-130">Utilisez l’un des centres de données Azure prenant en charge Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bd80-130">Use one of the Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="9bd80-131">**Compte Data Lake Store par défaut** : chaque compte Data Lake Analytics possède un compte Data Lake Store par défaut.</span><span class="sxs-lookup"><span data-stu-id="9bd80-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="9bd80-132">Pour répertorier le compte Data Lake Store existant :</span><span class="sxs-lookup"><span data-stu-id="9bd80-132">To list the existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="9bd80-133">Pour créer un compte Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="9bd80-133">To create a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="9bd80-134">Utilisez la syntaxe suivante pour créer un compte Data Lake Analytics :</span><span class="sxs-lookup"><span data-stu-id="9bd80-134">Use the following syntax to create a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="9bd80-135">Après avoir créé un compte, vous pouvez utiliser les commandes suivantes pour répertorier les comptes et afficher leurs détails :</span><span class="sxs-lookup"><span data-stu-id="9bd80-135">After creating an account, you can use the following commands to list the accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-to-data-lake-store"></a><span data-ttu-id="9bd80-136">Téléchargement de données vers Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9bd80-136">Upload data to Data Lake Store</span></span>
<span data-ttu-id="9bd80-137">Dans ce didacticiel, vous traitez des journaux de recherche.</span><span class="sxs-lookup"><span data-stu-id="9bd80-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="9bd80-138">Le journal de recherche peut être stocké dans Data Lake Store ou dans le stockage d’objets blobs Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd80-138">The search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="9bd80-139">Le portail Azure fournit une interface utilisateur pour la copie de fichiers de données d’exemple vers le compte Data Lake Store par défaut, y compris un fichier de journal de recherche.</span><span class="sxs-lookup"><span data-stu-id="9bd80-139">The Azure portal provides a user interface for copying some sample data files to the default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="9bd80-140">Voir [Préparer des données sources](data-lake-analytics-get-started-portal.md) pour charger les données dans le compte Data Lake Store par défaut.</span><span class="sxs-lookup"><span data-stu-id="9bd80-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) to upload the data to the default Data Lake Store account.</span></span>

<span data-ttu-id="9bd80-141">Pour charger des fichiers à l’aide de l’interface de CLI 2.0, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9bd80-141">To upload files using CLI 2.0, use the following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="9bd80-142">Analytique Data Lake peut également accéder au stockage d’objets blobs Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd80-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="9bd80-143">Pour télécharger des données dans le Blob Storage Azure, consultez [Utilisation de la CLI Microsoft Azure avec Microsoft Azure Storage](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9bd80-143">For uploading data to Azure Blob storage, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="9bd80-144">Envoyer des travaux Analytique Data Lake</span><span class="sxs-lookup"><span data-stu-id="9bd80-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="9bd80-145">Les travaux Data Lake Analytics sont écrits en langage U-SQL.</span><span class="sxs-lookup"><span data-stu-id="9bd80-145">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="9bd80-146">Pour en savoir plus sur U-SQL, consultez [Prise en main du langage U-SQL](data-lake-analytics-u-sql-get-started.md) et [Référence du langage U-SQL](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="9bd80-146">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="9bd80-147">**Pour créer un script de travail Analytique Data Lake**</span><span class="sxs-lookup"><span data-stu-id="9bd80-147">**To create a Data Lake Analytics job script**</span></span>

<span data-ttu-id="9bd80-148">Créez un fichier texte avec le script U-SQL suivant, puis enregistrez le fichier texte sur votre station de travail :</span><span class="sxs-lookup"><span data-stu-id="9bd80-148">Create a text file with following U-SQL script, and save the text file to your workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="9bd80-149">Ce script U-SQL lit le fichier de données source avec **Extractors.Tsv()**, puis crée un fichier csv à l’aide d’**Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="9bd80-149">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="9bd80-150">Ne modifiez pas les deux chemins d’accès, sauf si vous copiez le fichier source dans un autre emplacement.</span><span class="sxs-lookup"><span data-stu-id="9bd80-150">Don't modify the two paths unless you copy the source file into a different location.</span></span>  <span data-ttu-id="9bd80-151">Data Lake Analytics crée le dossier de sortie s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="9bd80-151">Data Lake Analytics creates the output folder if it doesn't exist.</span></span>

<span data-ttu-id="9bd80-152">Il est plus simple d’utiliser des chemins d’accès relatifs pour les fichiers stockés dans les comptes Data Lake Store par défaut.</span><span class="sxs-lookup"><span data-stu-id="9bd80-152">It is simpler to use relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="9bd80-153">Vous pouvez également utiliser des chemins d’accès absolus.</span><span class="sxs-lookup"><span data-stu-id="9bd80-153">You can also use absolute paths.</span></span>  <span data-ttu-id="9bd80-154">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9bd80-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="9bd80-155">Vous devez utiliser des chemins d’accès absolus pour accéder aux fichiers dans les comptes de stockage liés.</span><span class="sxs-lookup"><span data-stu-id="9bd80-155">You must use absolute paths to access files in linked Storage accounts.</span></span>  <span data-ttu-id="9bd80-156">La syntaxe des fichiers stockés dans le compte de stockage Azure lié est la suivante :</span><span class="sxs-lookup"><span data-stu-id="9bd80-156">The syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="9bd80-157">Conteneur d’objets Blob Azure avec des objets Blob publics ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9bd80-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="9bd80-158">Le conteneur d’objets Blob Azure avec des conteneurs publics n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9bd80-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="9bd80-159">**Pour soumettre les travaux**</span><span class="sxs-lookup"><span data-stu-id="9bd80-159">**To submit jobs**</span></span>

<span data-ttu-id="9bd80-160">Pour soumettre un travail, utilisez la syntaxe suivante.</span><span class="sxs-lookup"><span data-stu-id="9bd80-160">Use the following syntax to submit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="9bd80-161">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9bd80-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="9bd80-162">**Pour répertorier les travaux et afficher leurs détails**</span><span class="sxs-lookup"><span data-stu-id="9bd80-162">**To list jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="9bd80-163">**Pour annuler les travaux**</span><span class="sxs-lookup"><span data-stu-id="9bd80-163">**To cancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="9bd80-164">Récupérer les résultats de travaux</span><span class="sxs-lookup"><span data-stu-id="9bd80-164">Retrieve job results</span></span>

<span data-ttu-id="9bd80-165">Une fois qu’un travail est terminé, vous pouvez utiliser les commandes suivantes pour répertorier les fichiers sortants et télécharger les fichiers :</span><span class="sxs-lookup"><span data-stu-id="9bd80-165">After a job is completed, you can use the following commands to list the output files, and download the files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="9bd80-166">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9bd80-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="9bd80-167">Pipelines et récurrences</span><span class="sxs-lookup"><span data-stu-id="9bd80-167">Pipelines and recurrences</span></span>

<span data-ttu-id="9bd80-168">**Obtenir des informations sur les pipelines et les récurrences**</span><span class="sxs-lookup"><span data-stu-id="9bd80-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="9bd80-169">Utilisez les commandes `az dla job pipeline` pour afficher les tâches déjà soumises sur les informations de pipeline.</span><span class="sxs-lookup"><span data-stu-id="9bd80-169">Use the `az dla job pipeline` commands to see the pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="9bd80-170">Utilisez les commandes `az dla job recurrence` pour afficher les tâches déjà soumises sur les informations de récurrences.</span><span class="sxs-lookup"><span data-stu-id="9bd80-170">Use the `az dla job recurrence` commands to see the recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="9bd80-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9bd80-171">Next steps</span></span>

* <span data-ttu-id="9bd80-172">Pour afficher le document de référence Data Lake Analytics CLI 2.0, consultez [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="9bd80-172">To see the Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="9bd80-173">Pour afficher le document de référence Data Lake Store CLI 2.0, consultez [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="9bd80-173">To see the Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="9bd80-174">Pour voir une requête plus complexe, consultez [Analyse de journaux des sites web à l'aide d'Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="9bd80-174">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
