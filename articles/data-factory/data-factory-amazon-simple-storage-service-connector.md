---
title: "données aaaMove Amazon Simple Service de stockage à l’aide de Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir du Service de stockage Simple Amazon (S3) à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="0b662-103">Déplacement de données à partir d’Amazon Simple Storage Service à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0b662-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="0b662-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir du Service de stockage Simple Amazon (S3).</span><span class="sxs-lookup"><span data-stu-id="0b662-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="0b662-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="0b662-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="0b662-106">Vous pouvez copier des données à partir de la banque de données récepteur Amazon S3 tooany pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0b662-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="0b662-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="0b662-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="0b662-108">Fabrique de données prend actuellement en charge le déplacement des données uniquement à partir des magasins de données Amazon S3 tooother, mais ne pas déplacer les données à partir d’autres données stocke tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="0b662-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="0b662-109">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="0b662-109">Required permissions</span></span>
<span data-ttu-id="0b662-110">données toocopy de Amazon S3, assurez-vous que vous avez été accordées hello les autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b662-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="0b662-111">`s3:GetObject` et `s3:GetObjectVersion` pour les opérations d’objet Amazon S3 ;</span><span class="sxs-lookup"><span data-stu-id="0b662-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="0b662-112">`s3:ListBucket` pour les opérations de compartiment Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="0b662-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="0b662-113">Si vous utilisez hello Assistant Copier les données de fabrique, `s3:ListAllMyBuckets` est également requis.</span><span class="sxs-lookup"><span data-stu-id="0b662-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="0b662-114">Pour plus d’informations sur la liste complète des autorisations d’Amazon S3 hello, consultez [spécifier les autorisations dans une stratégie](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="0b662-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="0b662-115">Prise en main</span><span class="sxs-lookup"><span data-stu-id="0b662-115">Getting started</span></span>
<span data-ttu-id="0b662-116">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source Amazon S3 à l’aide de différents outils ou API.</span><span class="sxs-lookup"><span data-stu-id="0b662-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="0b662-117">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="0b662-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="0b662-118">Pour obtenir une description rapide, consultez [Didacticiel : créer un pipeline à l’aide de l’Assistant Copie](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0b662-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="0b662-119">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="0b662-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0b662-120">Pour obtenir des instructions toocreate un pipeline avec une activité de copie, consultez hello [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0b662-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="0b662-121">Si vous utilisez des outils ou des API, vous allez exécuter hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données sources :</span><span class="sxs-lookup"><span data-stu-id="0b662-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="0b662-122">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="0b662-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="0b662-123">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="0b662-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="0b662-124">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="0b662-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="0b662-125">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="0b662-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="0b662-126">Lorsque vous utilisez des outils ou des API (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="0b662-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="0b662-127">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données Amazon S3, hello [exemple de JSON : copier des données d’Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="0b662-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="0b662-128">Pour plus d’informations sur les formats de fichier et de compression pris en charge pour une activité de copie, consultez [Formats de fichier et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="0b662-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="0b662-129">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="0b662-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0b662-130">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="0b662-130">Linked service properties</span></span>
<span data-ttu-id="0b662-131">Un service lié lie une fabrique de données de tooa de magasin de données.</span><span class="sxs-lookup"><span data-stu-id="0b662-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="0b662-132">Vous créez un service lié de type **AwsAccessKey** toolink vos données Amazon S3 stocker la fabrique de données tooyour.</span><span class="sxs-lookup"><span data-stu-id="0b662-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="0b662-133">Hello tableau suivant fournit un service de description pour JSON éléments tooAmazon spécifique S3 (AwsAccessKey) liée.</span><span class="sxs-lookup"><span data-stu-id="0b662-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="0b662-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="0b662-134">Property</span></span> | <span data-ttu-id="0b662-135">Description</span><span class="sxs-lookup"><span data-stu-id="0b662-135">Description</span></span> | <span data-ttu-id="0b662-136">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0b662-136">Allowed values</span></span> | <span data-ttu-id="0b662-137">Requis</span><span class="sxs-lookup"><span data-stu-id="0b662-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0b662-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="0b662-138">accessKeyID</span></span> |<span data-ttu-id="0b662-139">ID de clé d’accès de clé secrète hello.</span><span class="sxs-lookup"><span data-stu-id="0b662-139">ID of hello secret access key.</span></span> |<span data-ttu-id="0b662-140">string</span><span class="sxs-lookup"><span data-stu-id="0b662-140">string</span></span> |<span data-ttu-id="0b662-141">Oui</span><span class="sxs-lookup"><span data-stu-id="0b662-141">Yes</span></span> |
| <span data-ttu-id="0b662-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="0b662-142">secretAccessKey</span></span> |<span data-ttu-id="0b662-143">clé d’accès de clé secrète Hello elle-même.</span><span class="sxs-lookup"><span data-stu-id="0b662-143">hello secret access key itself.</span></span> |<span data-ttu-id="0b662-144">Chaîne secrète chiffrée</span><span class="sxs-lookup"><span data-stu-id="0b662-144">Encrypted secret string</span></span> |<span data-ttu-id="0b662-145">Oui</span><span class="sxs-lookup"><span data-stu-id="0b662-145">Yes</span></span> |

<span data-ttu-id="0b662-146">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="0b662-146">Here is an example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="0b662-147">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="0b662-147">Dataset properties</span></span>
<span data-ttu-id="0b662-148">toospecify un toorepresent de jeu de données d’entrée les données dans le stockage d’objets Blob Azure, propriété de type hello ensemble du jeu de données hello**AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="0b662-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="0b662-149">Ensemble hello **linkedServiceName** service lié de propriété du nom de toohello hello dataset Hello Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="0b662-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="0b662-150">Pour obtenir la liste complète des sections et propriétés disponibles pour la définition de jeux de données, voir [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="0b662-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="0b662-151">Les sections comme la structure, la disponibilité et la stratégie sont similaires pour tous les types de jeux de données (par exemple, SQL Database, Azure Blob et Azure Table).</span><span class="sxs-lookup"><span data-stu-id="0b662-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="0b662-152">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="0b662-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="0b662-153">Hello **typeProperties** section pour un jeu de données de type **AmazonS3** (qui inclut les dataset hello Amazon S3) a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b662-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="0b662-154">Propriété</span><span class="sxs-lookup"><span data-stu-id="0b662-154">Property</span></span> | <span data-ttu-id="0b662-155">Description</span><span class="sxs-lookup"><span data-stu-id="0b662-155">Description</span></span> | <span data-ttu-id="0b662-156">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0b662-156">Allowed values</span></span> | <span data-ttu-id="0b662-157">Requis</span><span class="sxs-lookup"><span data-stu-id="0b662-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0b662-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="0b662-158">bucketName</span></span> |<span data-ttu-id="0b662-159">nom du compartiment Hello S3.</span><span class="sxs-lookup"><span data-stu-id="0b662-159">hello S3 bucket name.</span></span> |<span data-ttu-id="0b662-160">String</span><span class="sxs-lookup"><span data-stu-id="0b662-160">String</span></span> |<span data-ttu-id="0b662-161">Oui</span><span class="sxs-lookup"><span data-stu-id="0b662-161">Yes</span></span> |
| <span data-ttu-id="0b662-162">key</span><span class="sxs-lookup"><span data-stu-id="0b662-162">key</span></span> |<span data-ttu-id="0b662-163">clé d’objet Hello S3.</span><span class="sxs-lookup"><span data-stu-id="0b662-163">hello S3 object key.</span></span> |<span data-ttu-id="0b662-164">String</span><span class="sxs-lookup"><span data-stu-id="0b662-164">String</span></span> |<span data-ttu-id="0b662-165">Non</span><span class="sxs-lookup"><span data-stu-id="0b662-165">No</span></span> |
| <span data-ttu-id="0b662-166">prefix</span><span class="sxs-lookup"><span data-stu-id="0b662-166">prefix</span></span> |<span data-ttu-id="0b662-167">Préfixe de la clé d’objet hello S3.</span><span class="sxs-lookup"><span data-stu-id="0b662-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="0b662-168">Les objets dont les clés commencent par ce préfixe sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="0b662-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="0b662-169">S’applique uniquement lorsque la clé est vide.</span><span class="sxs-lookup"><span data-stu-id="0b662-169">Applies only when key is empty.</span></span> |<span data-ttu-id="0b662-170">string</span><span class="sxs-lookup"><span data-stu-id="0b662-170">String</span></span> |<span data-ttu-id="0b662-171">Non</span><span class="sxs-lookup"><span data-stu-id="0b662-171">No</span></span> |
| <span data-ttu-id="0b662-172">version</span><span class="sxs-lookup"><span data-stu-id="0b662-172">version</span></span> |<span data-ttu-id="0b662-173">version Hello d’objet hello S3, si le contrôle de version S3 est activé.</span><span class="sxs-lookup"><span data-stu-id="0b662-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="0b662-174">String</span><span class="sxs-lookup"><span data-stu-id="0b662-174">String</span></span> |<span data-ttu-id="0b662-175">Non</span><span class="sxs-lookup"><span data-stu-id="0b662-175">No</span></span> |
| <span data-ttu-id="0b662-176">format</span><span class="sxs-lookup"><span data-stu-id="0b662-176">format</span></span> | <span data-ttu-id="0b662-177">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0b662-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0b662-178">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0b662-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="0b662-179">Pour plus d’informations, consultez hello [au format texte](data-factory-supported-file-and-compression-formats.md#text-format), [format JSON](data-factory-supported-file-and-compression-formats.md#json-format), [le format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), et [format de Parquet ](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="0b662-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="0b662-180">Si vous souhaitez que les fichiers toocopy en tant que-entre le fichier magasins (copie binaire), ignorer hello format section dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="0b662-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="0b662-181">Non</span><span class="sxs-lookup"><span data-stu-id="0b662-181">No</span></span> | |
| <span data-ttu-id="0b662-182">compression</span><span class="sxs-lookup"><span data-stu-id="0b662-182">compression</span></span> | <span data-ttu-id="0b662-183">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0b662-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="0b662-184">les types Hello pris en charge sont : **GZip**, **Deflate**, **BZip2**, et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="0b662-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="0b662-185">les niveaux de Hello pris en charge sont : **Optimal** et **plus rapide**.</span><span class="sxs-lookup"><span data-stu-id="0b662-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0b662-186">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="0b662-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0b662-187">Non</span><span class="sxs-lookup"><span data-stu-id="0b662-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="0b662-188">**bucketName + touche** Spécifie l’emplacement de hello d’objet hello S3, où compartiment est le conteneur racine hello S3 objets et la clé est hello chemin d’accès complet toohello S3 objet.</span><span class="sxs-lookup"><span data-stu-id="0b662-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="0b662-189">Exemple de jeu de données avec le préfixe</span><span class="sxs-lookup"><span data-stu-id="0b662-189">Sample dataset with prefix</span></span>

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
### <a name="sample-dataset-with-version"></a><span data-ttu-id="0b662-190">Exemple de jeu de données (avec la version)</span><span class="sxs-lookup"><span data-stu-id="0b662-190">Sample dataset (with version)</span></span>

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

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="0b662-191">Chemins d’accès dynamiques pour S3</span><span class="sxs-lookup"><span data-stu-id="0b662-191">Dynamic paths for S3</span></span>
<span data-ttu-id="0b662-192">Hello précédent exemple utilise des valeurs fixes pour hello **clé** et **bucketName** propriétés dans le jeu de données hello Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="0b662-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="0b662-193">Vous pouvez demander à Data Factory de calculer ces propriétés dynamiquement au moment de l’exécution à l’aide de variables système telles que SliceStart.</span><span class="sxs-lookup"><span data-stu-id="0b662-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="0b662-194">Vous pouvez effectuer même hello pour hello **préfixe** propriété d’un jeu de données Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="0b662-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="0b662-195">Pour obtenir la liste des fonctions et variables prises en charge, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="0b662-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="0b662-196">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0b662-196">Copy activity properties</span></span>
<span data-ttu-id="0b662-197">Pour obtenir la liste complète des sections et propriétés disponibles pour la définition des activités, voir [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0b662-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="0b662-198">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="0b662-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="0b662-199">Propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="0b662-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="0b662-200">Pour l’activité de copie hello, les propriétés varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="0b662-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="0b662-201">Lorsqu’une source de l’activité de copie hello est de type **FileSystemSource** (qui inclut Amazon S3), hello suivant la propriété est disponible dans **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0b662-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="0b662-202">Propriété</span><span class="sxs-lookup"><span data-stu-id="0b662-202">Property</span></span> | <span data-ttu-id="0b662-203">Description</span><span class="sxs-lookup"><span data-stu-id="0b662-203">Description</span></span> | <span data-ttu-id="0b662-204">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0b662-204">Allowed values</span></span> | <span data-ttu-id="0b662-205">Requis</span><span class="sxs-lookup"><span data-stu-id="0b662-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0b662-206">recursive</span><span class="sxs-lookup"><span data-stu-id="0b662-206">recursive</span></span> |<span data-ttu-id="0b662-207">Spécifie si la liste de toorecursively S3 objets sous le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="0b662-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="0b662-208">true/false</span><span class="sxs-lookup"><span data-stu-id="0b662-208">true/false</span></span> |<span data-ttu-id="0b662-209">Non</span><span class="sxs-lookup"><span data-stu-id="0b662-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="0b662-210">Exemple de JSON : copier des données d’Amazon S3 tooAzure stockage d’objets Blob</span><span class="sxs-lookup"><span data-stu-id="0b662-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="0b662-211">Cet exemple montre comment toocopy des données à partir d’Amazon S3 tooan stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0b662-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="0b662-212">Toutefois, les données peuvent être copiées directement trop[des récepteurs hello qui sont pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de l’activité de copie hello dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0b662-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="0b662-213">exemple Hello fournit les définitions de JSON pour hello suivant des entités de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0b662-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="0b662-214">Vous pouvez utiliser ces définitions de toocreate un pipeline toocopy des données d’Amazon S3 tooBlob stockage, à l’aide de hello [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0b662-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="0b662-215">Un service lié de type [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0b662-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="0b662-216">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0b662-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="0b662-217">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0b662-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="0b662-218">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0b662-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="0b662-219">Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0b662-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0b662-220">exemple Hello copie des données d’Amazon S3 tooan objets blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="0b662-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="0b662-221">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="0b662-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="0b662-222">Service lié Amazon S3</span><span class="sxs-lookup"><span data-stu-id="0b662-222">Amazon S3 linked service</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="0b662-223">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0b662-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="0b662-224">Jeu de données d’entrée Amazon S3</span><span class="sxs-lookup"><span data-stu-id="0b662-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="0b662-225">Paramètre **« external » : true** informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello.</span><span class="sxs-lookup"><span data-stu-id="0b662-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="0b662-226">Définir tootrue de cette propriété sur un jeu de données d’entrée qui n’est pas généré par une activité dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="0b662-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

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


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="0b662-227">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="0b662-227">Azure Blob output dataset</span></span>

<span data-ttu-id="0b662-228">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="0b662-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0b662-229">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="0b662-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="0b662-230">chemin d’accès du dossier Hello utilise hello des parties d’année, mois, jours et heures de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="0b662-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="0b662-231">Activité de copie dans un pipeline avec une source Amazon S3 et un récepteur blob</span><span class="sxs-lookup"><span data-stu-id="0b662-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="0b662-232">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie, et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="0b662-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="0b662-233">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**FileSystemSource**, et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0b662-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

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
> <span data-ttu-id="0b662-234">toomap des colonnes à partir d’un toocolumns de jeu de données source à partir d’un jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="0b662-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="0b662-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b662-235">Next steps</span></span>
<span data-ttu-id="0b662-236">Consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="0b662-236">See hello following articles:</span></span>

* <span data-ttu-id="0b662-237">impact sur les performances de déplacement des données (activité de copie) dans la fabrique de données et différentes façons toooptimize des facteurs toolearn sur la clé, consultez hello [copier activité guide des performances et paramétrage](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="0b662-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="0b662-238">Pour obtenir des instructions pour la création d’un pipeline avec une activité de copie, consultez hello [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0b662-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
