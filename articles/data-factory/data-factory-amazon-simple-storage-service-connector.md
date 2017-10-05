---
title: "Déplacement de données à partir d’Amazon Simple Storage Service à l’aide de Data Factory | Microsoft Docs"
description: "Découvrez comment déplacer des données à partir d’Amazon Simple Storage Service (S3) à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 3e21f7dfccc3b235071344a28c7d94f65e6bf9ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="80276-103">Déplacement de données à partir d’Amazon Simple Storage Service à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="80276-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="80276-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’un système Amazon Simple Storage Service (S3).</span><span class="sxs-lookup"><span data-stu-id="80276-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="80276-105">Il s’appuie sur l’article relatif aux [activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement des données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="80276-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="80276-106">Vous pouvez copier les données d’Amazon S3 dans tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="80276-106">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="80276-107">Consultez le tableau [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="80276-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="80276-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données d’Amazon S3 vers d’autres magasins de données, mais pas l’inverse.</span><span class="sxs-lookup"><span data-stu-id="80276-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="80276-109">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="80276-109">Required permissions</span></span>
<span data-ttu-id="80276-110">Pour copier des données à partir d’Amazon S3, assurez-vous que vous disposez des autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="80276-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="80276-111">`s3:GetObject` et `s3:GetObjectVersion` pour les opérations d’objet Amazon S3 ;</span><span class="sxs-lookup"><span data-stu-id="80276-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="80276-112">`s3:ListBucket` pour les opérations de compartiment Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="80276-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="80276-113">Si vous utilisez l’Assistant de copie de Data Factory, l’élément `s3:ListAllMyBuckets` est également requis.</span><span class="sxs-lookup"><span data-stu-id="80276-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="80276-114">Pour obtenir la liste complète des autorisations Amazon S3, consultez l’article [Spécification des autorisations d’une stratégie](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="80276-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="80276-115">Prise en main</span><span class="sxs-lookup"><span data-stu-id="80276-115">Getting started</span></span>
<span data-ttu-id="80276-116">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source Amazon S3 à l’aide de différents outils ou API.</span><span class="sxs-lookup"><span data-stu-id="80276-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="80276-117">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="80276-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="80276-118">Pour obtenir une description rapide, consultez [Didacticiel : créer un pipeline à l’aide de l’Assistant Copie](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="80276-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="80276-119">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="80276-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="80276-120">Pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie, consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="80276-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="80276-121">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="80276-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="80276-122">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="80276-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="80276-123">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="80276-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="80276-124">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="80276-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="80276-125">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="80276-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="80276-126">Lorsque vous utilisez les outils ou API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory à l’aide du format JSON.</span><span class="sxs-lookup"><span data-stu-id="80276-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="80276-127">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données Amazon S3, consultez la section [Exemple JSON : copier des données depuis un système Amazon S3 vers Blob Azure](#json-example-copy-data-from-amazon-s3-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="80276-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="80276-128">Pour plus d’informations sur les formats de fichier et de compression pris en charge pour une activité de copie, consultez [Formats de fichier et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="80276-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="80276-129">Les sections suivantes fournissent des informations sur les propriétés JSON utilisées pour définir les entités Data Factory spécifiques à Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="80276-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="80276-130">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="80276-130">Linked service properties</span></span>
<span data-ttu-id="80276-131">Un service lié lie un magasin de données à une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="80276-131">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="80276-132">Pour lier votre magasin de données Amazon S3 à votre fabrique de données, vous devez créer un service lié de type **AwsAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="80276-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="80276-133">La table suivante fournit la description des éléments JSON spécifiques au service lié Amazon S3 (AwsAccessKey).</span><span class="sxs-lookup"><span data-stu-id="80276-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="80276-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="80276-134">Property</span></span> | <span data-ttu-id="80276-135">Description</span><span class="sxs-lookup"><span data-stu-id="80276-135">Description</span></span> | <span data-ttu-id="80276-136">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="80276-136">Allowed values</span></span> | <span data-ttu-id="80276-137">Requis</span><span class="sxs-lookup"><span data-stu-id="80276-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="80276-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="80276-138">accessKeyID</span></span> |<span data-ttu-id="80276-139">ID de la clé d’accès secrète.</span><span class="sxs-lookup"><span data-stu-id="80276-139">ID of the secret access key.</span></span> |<span data-ttu-id="80276-140">string</span><span class="sxs-lookup"><span data-stu-id="80276-140">string</span></span> |<span data-ttu-id="80276-141">Oui</span><span class="sxs-lookup"><span data-stu-id="80276-141">Yes</span></span> |
| <span data-ttu-id="80276-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="80276-142">secretAccessKey</span></span> |<span data-ttu-id="80276-143">La clé d’accès secrète elle-même.</span><span class="sxs-lookup"><span data-stu-id="80276-143">The secret access key itself.</span></span> |<span data-ttu-id="80276-144">Chaîne secrète chiffrée</span><span class="sxs-lookup"><span data-stu-id="80276-144">Encrypted secret string</span></span> |<span data-ttu-id="80276-145">Oui</span><span class="sxs-lookup"><span data-stu-id="80276-145">Yes</span></span> |

<span data-ttu-id="80276-146">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="80276-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="80276-147">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="80276-147">Dataset properties</span></span>
<span data-ttu-id="80276-148">Pour spécifier un jeu de données afin de représenter les données d’entrée dans un Stockage Blob Azure, définissez la propriété de type du jeu de données sur **AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="80276-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="80276-149">Définissez la propriété **linkedServiceName** du jeu de données sur le nom du service lié Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="80276-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="80276-150">Pour obtenir la liste complète des sections et propriétés disponibles pour la définition de jeux de données, voir [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="80276-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="80276-151">Les sections comme la structure, la disponibilité et la stratégie sont similaires pour tous les types de jeux de données (par exemple, SQL Database, Azure Blob et Azure Table).</span><span class="sxs-lookup"><span data-stu-id="80276-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="80276-152">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l'emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="80276-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="80276-153">La section **typeProperties** du jeu de données de type **AmazonS3** (comprenant le jeu de données Amazon S3) présente les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="80276-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="80276-154">Propriété</span><span class="sxs-lookup"><span data-stu-id="80276-154">Property</span></span> | <span data-ttu-id="80276-155">Description</span><span class="sxs-lookup"><span data-stu-id="80276-155">Description</span></span> | <span data-ttu-id="80276-156">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="80276-156">Allowed values</span></span> | <span data-ttu-id="80276-157">Requis</span><span class="sxs-lookup"><span data-stu-id="80276-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="80276-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="80276-158">bucketName</span></span> |<span data-ttu-id="80276-159">Le nom de compartiment S3.</span><span class="sxs-lookup"><span data-stu-id="80276-159">The S3 bucket name.</span></span> |<span data-ttu-id="80276-160">string</span><span class="sxs-lookup"><span data-stu-id="80276-160">String</span></span> |<span data-ttu-id="80276-161">Oui</span><span class="sxs-lookup"><span data-stu-id="80276-161">Yes</span></span> |
| <span data-ttu-id="80276-162">key</span><span class="sxs-lookup"><span data-stu-id="80276-162">key</span></span> |<span data-ttu-id="80276-163">La clé d’objet S3.</span><span class="sxs-lookup"><span data-stu-id="80276-163">The S3 object key.</span></span> |<span data-ttu-id="80276-164">string</span><span class="sxs-lookup"><span data-stu-id="80276-164">String</span></span> |<span data-ttu-id="80276-165">Non</span><span class="sxs-lookup"><span data-stu-id="80276-165">No</span></span> |
| <span data-ttu-id="80276-166">prefix</span><span class="sxs-lookup"><span data-stu-id="80276-166">prefix</span></span> |<span data-ttu-id="80276-167">Préfixe de la clé d’objet S3.</span><span class="sxs-lookup"><span data-stu-id="80276-167">Prefix for the S3 object key.</span></span> <span data-ttu-id="80276-168">Les objets dont les clés commencent par ce préfixe sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="80276-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="80276-169">S’applique uniquement lorsque la clé est vide.</span><span class="sxs-lookup"><span data-stu-id="80276-169">Applies only when key is empty.</span></span> |<span data-ttu-id="80276-170">string</span><span class="sxs-lookup"><span data-stu-id="80276-170">String</span></span> |<span data-ttu-id="80276-171">Non</span><span class="sxs-lookup"><span data-stu-id="80276-171">No</span></span> |
| <span data-ttu-id="80276-172">version</span><span class="sxs-lookup"><span data-stu-id="80276-172">version</span></span> |<span data-ttu-id="80276-173">La version de l’objet S3 si le contrôle de version S3 est activé.</span><span class="sxs-lookup"><span data-stu-id="80276-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="80276-174">String</span><span class="sxs-lookup"><span data-stu-id="80276-174">String</span></span> |<span data-ttu-id="80276-175">Non</span><span class="sxs-lookup"><span data-stu-id="80276-175">No</span></span> |
| <span data-ttu-id="80276-176">format</span><span class="sxs-lookup"><span data-stu-id="80276-176">format</span></span> | <span data-ttu-id="80276-177">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="80276-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="80276-178">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="80276-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="80276-179">Pour en savoir plus, voir les sections [Format Text](data-factory-supported-file-and-compression-formats.md#text-format), [Format JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [Format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="80276-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="80276-180">Si vous souhaitez copier des fichiers en l’état entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="80276-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="80276-181">Non</span><span class="sxs-lookup"><span data-stu-id="80276-181">No</span></span> | |
| <span data-ttu-id="80276-182">compression</span><span class="sxs-lookup"><span data-stu-id="80276-182">compression</span></span> | <span data-ttu-id="80276-183">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="80276-183">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="80276-184">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="80276-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="80276-185">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="80276-185">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="80276-186">Pour en savoir plus, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="80276-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="80276-187">Non</span><span class="sxs-lookup"><span data-stu-id="80276-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="80276-188">**bucketName + key** spécifient l’emplacement de l’objet S3 où le compartiment est le conteneur racine pour les objets S3 et la clé est le chemin d’accès complet à l’objet S3.</span><span class="sxs-lookup"><span data-stu-id="80276-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="80276-189">Exemple de jeu de données avec le préfixe</span><span class="sxs-lookup"><span data-stu-id="80276-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="80276-190">Exemple de jeu de données (avec la version)</span><span class="sxs-lookup"><span data-stu-id="80276-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="80276-191">Chemins d’accès dynamiques pour S3</span><span class="sxs-lookup"><span data-stu-id="80276-191">Dynamic paths for S3</span></span>
<span data-ttu-id="80276-192">L’exemple précédent utilise des valeurs fixes pour les propriétés **key** et **bucketName** dans le jeu de données Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="80276-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="80276-193">Vous pouvez demander à Data Factory de calculer ces propriétés dynamiquement au moment de l’exécution à l’aide de variables système telles que SliceStart.</span><span class="sxs-lookup"><span data-stu-id="80276-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="80276-194">Vous pouvez faire de même pour la propriété **prefix** d’un jeu de données Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="80276-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="80276-195">Pour obtenir la liste des fonctions et variables prises en charge, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="80276-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="80276-196">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="80276-196">Copy activity properties</span></span>
<span data-ttu-id="80276-197">Pour obtenir la liste complète des sections et propriétés disponibles pour la définition des activités, voir [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="80276-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="80276-198">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="80276-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="80276-199">Les propriétés disponibles dans la section **typeProperties** de l’activité varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="80276-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="80276-200">Pour l’activité de copie, les propriétés dépendent des types de sources et de récepteurs.</span><span class="sxs-lookup"><span data-stu-id="80276-200">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="80276-201">Lorsque la source de l’activité de copie est de type **FileSystemSource** (qui inclut Amazon S3), la propriété suivante est disponible dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="80276-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="80276-202">Propriété</span><span class="sxs-lookup"><span data-stu-id="80276-202">Property</span></span> | <span data-ttu-id="80276-203">Description</span><span class="sxs-lookup"><span data-stu-id="80276-203">Description</span></span> | <span data-ttu-id="80276-204">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="80276-204">Allowed values</span></span> | <span data-ttu-id="80276-205">Requis</span><span class="sxs-lookup"><span data-stu-id="80276-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="80276-206">recursive</span><span class="sxs-lookup"><span data-stu-id="80276-206">recursive</span></span> |<span data-ttu-id="80276-207">Spécifie s’il faut répertorier de manière récursive les objets S3 sous le répertoire.</span><span class="sxs-lookup"><span data-stu-id="80276-207">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="80276-208">true/false</span><span class="sxs-lookup"><span data-stu-id="80276-208">true/false</span></span> |<span data-ttu-id="80276-209">Non</span><span class="sxs-lookup"><span data-stu-id="80276-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="80276-210">Exemple JSON : copier des données depuis un système Amazon S3 vers le stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="80276-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="80276-211">Cet exemple indique comment copier des données à partir d’Amazon S3 vers un stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="80276-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="80276-212">Toutefois, les données peuvent être copiées directement vers [l’un des récepteurs pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats), via l’activité de copie de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="80276-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="80276-213">Cet exemple fournit des définitions JSON pour les entités Data Factory suivantes.</span><span class="sxs-lookup"><span data-stu-id="80276-213">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="80276-214">Vous pouvez utiliser ces définitions pour créer un pipeline afin de copier des données depuis Amazon S3 vers un Stockage Blob Azure à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [de PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="80276-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="80276-215">Un service lié de type [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="80276-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="80276-216">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="80276-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="80276-217">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="80276-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="80276-218">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="80276-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="80276-219">Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="80276-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="80276-220">L’exemple copie des données à partir d’Amazon S3 vers un objet blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="80276-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="80276-221">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="80276-221">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="80276-222">Service lié Amazon S3</span><span class="sxs-lookup"><span data-stu-id="80276-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="80276-223">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="80276-223">Azure Storage linked service</span></span>

```json
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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="80276-224">Jeu de données d’entrée Amazon S3</span><span class="sxs-lookup"><span data-stu-id="80276-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="80276-225">La définition de **"external": true** informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à Data Factory.</span><span class="sxs-lookup"><span data-stu-id="80276-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="80276-226">Définissez cette propriété sur true sur un jeu de données d’entrée qui n’est pas produit par une activité dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="80276-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="80276-227">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="80276-227">Azure Blob output dataset</span></span>

<span data-ttu-id="80276-228">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="80276-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="80276-229">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="80276-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="80276-230">Le chemin d’accès du dossier utilise l’année, le mois, le jour et la partie heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="80276-230">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="80276-231">Activité de copie dans un pipeline avec une source Amazon S3 et un récepteur blob</span><span class="sxs-lookup"><span data-stu-id="80276-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="80276-232">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d’entrée et de sortie, et qui est planifiée pour s’exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="80276-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="80276-233">Dans la définition du pipeline JSON, le type **source** est défini sur **FileSystemSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="80276-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="80276-234">Pour savoir comment mapper des colonnes d’un jeu de données source à des colonnes d’un jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="80276-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="80276-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80276-235">Next steps</span></span>
<span data-ttu-id="80276-236">Consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="80276-236">See the following articles:</span></span>

* <span data-ttu-id="80276-237">Pour découvrir les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser, voir [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="80276-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="80276-238">Pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie, voir [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="80276-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
