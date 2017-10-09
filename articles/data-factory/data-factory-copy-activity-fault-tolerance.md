---
title: "la tolérance de panne aaaAdd dans l’activité de copie de fabrique de données Azure en ignorant les lignes incompatible | Documents Microsoft"
description: "Découvrez comment tooadd la tolérance de pannes dans l’activité de copie de fabrique de données Azure en ignorant les lignes incompatible pendant la copie"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="8920b-103">Ajouter une tolérance de panne de l’activité de copie en ignorant les lignes incompatibles</span><span class="sxs-lookup"><span data-stu-id="8920b-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="8920b-104">Azure Data Factory [l’activité de copie](data-factory-data-movement-activities.md) offre des lignes de deux façons toohandle incompatibles lors de la copie des données entre les magasins de données source et le récepteur :</span><span class="sxs-lookup"><span data-stu-id="8920b-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="8920b-105">Vous pouvez abandonner et Échec de copie de hello activité lorsque des données incompatibles sont rencontré (comportement par défaut).</span><span class="sxs-lookup"><span data-stu-id="8920b-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="8920b-106">Vous pouvez continuer toocopy toutes les données hello en ajoutant une tolérance de panne et de lignes de données incompatibles ont été ignorées.</span><span class="sxs-lookup"><span data-stu-id="8920b-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="8920b-107">En outre, vous pouvez consigner les lignes incompatible hello dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="8920b-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="8920b-108">Vous pouvez examiner hello journal toolearn hello cause de l’échec de hello, corriger les données de salutation sur la source de données hello, puis recommencez l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="8920b-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="8920b-109">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="8920b-109">Supported scenarios</span></span>
<span data-ttu-id="8920b-110">L’activité de copie offre la possibilité de détecter, d’ignorer et de journaliser les incompatibilités de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="8920b-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="8920b-111">**Incompatibilité entre le type de données source hello et un type natif hello récepteur**</span><span class="sxs-lookup"><span data-stu-id="8920b-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="8920b-112">Par exemple : copier des données à partir d’un fichier CSV dans tooa de stockage d’objets Blob SQL de base de données avec une définition de schéma qui contient trois **INT** colonnes de type.</span><span class="sxs-lookup"><span data-stu-id="8920b-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="8920b-113">Hello des lignes de fichier CSV qui contiennent des données numériques, tels que `123,456,789` sont copiés correctement magasin de récepteur toohello.</span><span class="sxs-lookup"><span data-stu-id="8920b-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="8920b-114">Hello, toutefois, les lignes qui contiennent des valeurs non numériques, tels que `123,456,abc` sont détectés comme étant incompatibles et sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="8920b-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="8920b-115">**Incohérence entre le nombre de hello des colonnes de la source de hello et récepteur de hello**</span><span class="sxs-lookup"><span data-stu-id="8920b-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="8920b-116">Par exemple : copier des données à partir d’un fichier CSV dans tooa de stockage d’objets Blob SQL de base de données avec une définition de schéma qui contient les six colonnes.</span><span class="sxs-lookup"><span data-stu-id="8920b-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="8920b-117">Hello fichier CSV sont des lignes qui contiennent les six colonnes copiées magasin de récepteur toohello.</span><span class="sxs-lookup"><span data-stu-id="8920b-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="8920b-118">lignes de fichier CSV Hello qui contiennent plus ou moins de six colonnes sont détectés comme étant incompatible et sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="8920b-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="8920b-119">**Violation de clé primaire lors de l’écriture de base de données relationnelle tooa**</span><span class="sxs-lookup"><span data-stu-id="8920b-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="8920b-120">Par exemple : copier des données d’une base de données SQL server tooa SQL.</span><span class="sxs-lookup"><span data-stu-id="8920b-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="8920b-121">Une clé primaire est définie dans la base de données SQL de récepteur hello, mais aucun ce type de clé primaire n’est définie dans SQL server de la source hello.</span><span class="sxs-lookup"><span data-stu-id="8920b-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="8920b-122">lignes Hello dupliqué existent dans la source de hello ne peut pas être copié toohello récepteur.</span><span class="sxs-lookup"><span data-stu-id="8920b-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="8920b-123">Activité de copie copie uniquement hello première ligne de source de données hello dans récepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="8920b-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="8920b-124">Hello source suivantes les lignes qui contiennent la valeur de clé primaire dupliquée de hello sont détectés comme étant incompatible et sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="8920b-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="8920b-125">Configuration</span><span class="sxs-lookup"><span data-stu-id="8920b-125">Configuration</span></span>
<span data-ttu-id="8920b-126">Hello exemple suivant fournit une tooconfigure de définition JSON hello des lignes incompatible dans l’activité de copie ont été ignorées :</span><span class="sxs-lookup"><span data-stu-id="8920b-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="8920b-127">Propriété</span><span class="sxs-lookup"><span data-stu-id="8920b-127">Property</span></span> | <span data-ttu-id="8920b-128">Description</span><span class="sxs-lookup"><span data-stu-id="8920b-128">Description</span></span> | <span data-ttu-id="8920b-129">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="8920b-129">Allowed values</span></span> | <span data-ttu-id="8920b-130">Requis</span><span class="sxs-lookup"><span data-stu-id="8920b-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8920b-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="8920b-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="8920b-132">Activer ou non l’option d’ignorer les lignes incompatibles.</span><span class="sxs-lookup"><span data-stu-id="8920b-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="8920b-133">true</span><span class="sxs-lookup"><span data-stu-id="8920b-133">True</span></span><br/><span data-ttu-id="8920b-134">False (valeur par défaut)</span><span class="sxs-lookup"><span data-stu-id="8920b-134">False (default)</span></span> | <span data-ttu-id="8920b-135">Non</span><span class="sxs-lookup"><span data-stu-id="8920b-135">No</span></span> |
| <span data-ttu-id="8920b-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="8920b-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="8920b-137">Un groupe de propriétés qui peuvent être spécifiées lorsque vous souhaitez que les lignes de toolog hello incompatible.</span><span class="sxs-lookup"><span data-stu-id="8920b-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="8920b-138">Non</span><span class="sxs-lookup"><span data-stu-id="8920b-138">No</span></span> |
| <span data-ttu-id="8920b-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="8920b-139">**linkedServiceName**</span></span> | <span data-ttu-id="8920b-140">service Hello lié de stockage Azure toostore hello journal contenant les lignes hello ignorée.</span><span class="sxs-lookup"><span data-stu-id="8920b-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="8920b-141">nom Hello d’un [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) service, qui fait référence toohello instance de stockage que vous souhaitez le fichier journal de toouse toostore hello lié.</span><span class="sxs-lookup"><span data-stu-id="8920b-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="8920b-142">Non</span><span class="sxs-lookup"><span data-stu-id="8920b-142">No</span></span> |
| <span data-ttu-id="8920b-143">**path**</span><span class="sxs-lookup"><span data-stu-id="8920b-143">**path**</span></span> | <span data-ttu-id="8920b-144">chemin d’accès de Hello du fichier journal hello contenant hello ignorée lignes.</span><span class="sxs-lookup"><span data-stu-id="8920b-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="8920b-145">Spécifier le chemin de stockage d’objets Blob hello toouse toolog hello des données incompatibles.</span><span class="sxs-lookup"><span data-stu-id="8920b-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="8920b-146">Si vous ne fournissez pas un chemin d’accès, le service de hello crée un conteneur pour vous.</span><span class="sxs-lookup"><span data-stu-id="8920b-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="8920b-147">Non</span><span class="sxs-lookup"><span data-stu-id="8920b-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="8920b-148">Surveillance</span><span class="sxs-lookup"><span data-stu-id="8920b-148">Monitoring</span></span>
<span data-ttu-id="8920b-149">Après la fin de l’activité de copie de hello exécuter, vous pouvez voir le nombre hello des lignes ignorées Bonjour section analyse :</span><span class="sxs-lookup"><span data-stu-id="8920b-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![Le système de surveillance a ignoré les lignes incompatibles](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="8920b-151">Si vous configurez des lignes de toolog hello incompatibles, vous pouvez trouver le fichier de journal de hello à ce chemin d’accès : `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` dans le fichier journal de hello, vous pouvez voir hello les lignes qui ont été ignorés et hello l’origine du problème d’incompatibilité de hello.</span><span class="sxs-lookup"><span data-stu-id="8920b-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="8920b-152">Les données d’origine hello et erreur correspondante de hello sont enregistrés dans le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="8920b-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="8920b-153">Un exemple de contenu du fichier journal hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="8920b-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="8920b-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8920b-154">Next steps</span></span>
<span data-ttu-id="8920b-155">toolearn en savoir plus sur l’activité de copie de fabrique de données de Azure, consultez [déplacer des données à l’aide de l’activité de copie](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8920b-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
