---
title: "données aaaMove local HDFS | Documents Microsoft"
description: "Découvrez comment toomove des données à partir de local HDFS à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="30351-103">Transfert de données à partir d’un HDFS local à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="30351-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="30351-104">Cet article explique comment toouse hello activité de copie de données Azure Data Factory toomove un HDFS local.</span><span class="sxs-lookup"><span data-stu-id="30351-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises HDFS.</span></span> <span data-ttu-id="30351-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="30351-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="30351-106">Vous pouvez copier des données à partir du magasin de données du récepteur HDFS tooany pris en charge.</span><span class="sxs-lookup"><span data-stu-id="30351-106">You can copy data from HDFS tooany supported sink data store.</span></span> <span data-ttu-id="30351-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="30351-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="30351-108">Fabrique de données prend actuellement en charge le déplacement des données uniquement à partir d’un HDFS local tooother des magasins de données, mais ne pas pour le déplacement des données à partir d’autres données de magasins tooan local HDFS.</span><span class="sxs-lookup"><span data-stu-id="30351-108">Data factory currently supports only moving data from an on-premises HDFS tooother data stores, but not for moving data from other data stores tooan on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="30351-109">Activité de copie ne supprime pas le fichier de source de hello lorsqu’elle est correctement copié toohello destination.</span><span class="sxs-lookup"><span data-stu-id="30351-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="30351-110">Si vous avez besoin de fichier de source de hello toodelete après la copie a réussi, créer un fichier de hello toodelete activité personnalisée et utiliser l’activité hello dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="30351-111">Activation de la connectivité</span><span class="sxs-lookup"><span data-stu-id="30351-111">Enabling connectivity</span></span>
<span data-ttu-id="30351-112">Service de fabrique de données prend en charge la connexion HDFS tooon local à l’aide de la passerelle de gestion des données de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-112">Data Factory service supports connecting tooon-premises HDFS using hello Data Management Gateway.</span></span> <span data-ttu-id="30351-113">Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="30351-114">Utilisez hello passerelle tooconnect tooHDFS même s’il est hébergé dans une machine virtuelle IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="30351-114">Use hello gateway tooconnect tooHDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="30351-115">Vérifiez que hello est passerelle de gestion des données peuvent accéder à trop**tous les** hello [serveur de noms de nœud] : [nom de port du nœud] et [serveurs de nœud de données] : [port de nœud de données] du cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-115">Make sure hello Data Management Gateway can access too**ALL** hello [name node server]:[name node port] and [data node servers]:[data node port] of hello Hadoop cluster.</span></span> <span data-ttu-id="30351-116">Le [port du nœud de nom] par défaut est 50070 et le [port du nœud de données] par défaut est 50075.</span><span class="sxs-lookup"><span data-stu-id="30351-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="30351-117">Lorsque vous installez une passerelle sur hello même ordinateur ou local hello Azure VM comme hello HDFS, nous vous recommandons d’installer hello passerelle sur un ordinateur distinct/Azure IaaS machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30351-117">While you can install gateway on hello same on-premises machine or hello Azure VM as hello HDFS, we recommend that you install hello gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="30351-118">Disposer d’une passerelle sur un ordinateur distinct réduit les conflits de ressources et améliore les performances.</span><span class="sxs-lookup"><span data-stu-id="30351-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="30351-119">Lorsque vous installez la passerelle de hello sur un ordinateur distinct, machine de hello doit être machine hello tooaccess en mesure de hello HDFS.</span><span class="sxs-lookup"><span data-stu-id="30351-119">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="30351-120">Prise en main</span><span class="sxs-lookup"><span data-stu-id="30351-120">Getting started</span></span>
<span data-ttu-id="30351-121">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source HDFS à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="30351-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="30351-122">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="30351-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="30351-123">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="30351-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="30351-124">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="30351-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="30351-125">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="30351-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="30351-126">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="30351-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="30351-127">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="30351-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="30351-128">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="30351-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="30351-129">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="30351-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="30351-130">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="30351-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="30351-131">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="30351-132">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’un magasin de données HDFS, [exemple de JSON : copier des données locales HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="30351-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="30351-133">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifiques tooHDFS :</span><span class="sxs-lookup"><span data-stu-id="30351-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooHDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="30351-134">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="30351-134">Linked service properties</span></span>
<span data-ttu-id="30351-135">Un service lié lie une fabrique de données de tooa de magasin de données.</span><span class="sxs-lookup"><span data-stu-id="30351-135">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="30351-136">Vous créez un service lié de type **Hdfs** toolink une fabrique de données tooyour HDFS local.</span><span class="sxs-lookup"><span data-stu-id="30351-136">You create a linked service of type **Hdfs** toolink an on-premises HDFS tooyour data factory.</span></span> <span data-ttu-id="30351-137">Hello tableau suivant fournit la description du service de tooHDFS spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="30351-137">hello following table provides description for JSON elements specific tooHDFS linked service.</span></span>

| <span data-ttu-id="30351-138">Propriété</span><span class="sxs-lookup"><span data-stu-id="30351-138">Property</span></span> | <span data-ttu-id="30351-139">Description</span><span class="sxs-lookup"><span data-stu-id="30351-139">Description</span></span> | <span data-ttu-id="30351-140">Requis</span><span class="sxs-lookup"><span data-stu-id="30351-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="30351-141">type</span><span class="sxs-lookup"><span data-stu-id="30351-141">type</span></span> |<span data-ttu-id="30351-142">propriété de type Hello doit indiquer : **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="30351-142">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="30351-143">Oui</span><span class="sxs-lookup"><span data-stu-id="30351-143">Yes</span></span> |
| <span data-ttu-id="30351-144">Url</span><span class="sxs-lookup"><span data-stu-id="30351-144">Url</span></span> |<span data-ttu-id="30351-145">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="30351-145">URL toohello HDFS</span></span> |<span data-ttu-id="30351-146">Oui</span><span class="sxs-lookup"><span data-stu-id="30351-146">Yes</span></span> |
| <span data-ttu-id="30351-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="30351-147">authenticationType</span></span> |<span data-ttu-id="30351-148">Anonyme ou Windows.</span><span class="sxs-lookup"><span data-stu-id="30351-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="30351-149">toouse **l’authentification Kerberos** pour le connecteur HDFS, consultez trop[cette section](#use-kerberos-authentication-for-hdfs-connector) tooset votre environnement local en conséquence.</span><span class="sxs-lookup"><span data-stu-id="30351-149">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="30351-150">Oui</span><span class="sxs-lookup"><span data-stu-id="30351-150">Yes</span></span> |
| <span data-ttu-id="30351-151">userName</span><span class="sxs-lookup"><span data-stu-id="30351-151">userName</span></span> |<span data-ttu-id="30351-152">Nom d’utilisateur de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="30351-152">Username for Windows authentication.</span></span> |<span data-ttu-id="30351-153">Oui (pour l’authentification Windows)</span><span class="sxs-lookup"><span data-stu-id="30351-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="30351-154">password</span><span class="sxs-lookup"><span data-stu-id="30351-154">password</span></span> |<span data-ttu-id="30351-155">Mot de passe de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="30351-155">Password for Windows authentication.</span></span> |<span data-ttu-id="30351-156">Oui (pour l’authentification Windows)</span><span class="sxs-lookup"><span data-stu-id="30351-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="30351-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="30351-157">gatewayName</span></span> |<span data-ttu-id="30351-158">Nom de passerelle hello hello service Data Factory doit utiliser tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="30351-158">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="30351-159">Oui</span><span class="sxs-lookup"><span data-stu-id="30351-159">Yes</span></span> |
| <span data-ttu-id="30351-160">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="30351-160">encryptedCredential</span></span> |<span data-ttu-id="30351-161">[Nouveau-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) sortie des informations d’identification de l’accès hello.</span><span class="sxs-lookup"><span data-stu-id="30351-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="30351-162">Non</span><span class="sxs-lookup"><span data-stu-id="30351-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="30351-163">Utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="30351-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="30351-164">Utilisation de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="30351-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="30351-165">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="30351-165">Dataset properties</span></span>
<span data-ttu-id="30351-166">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="30351-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="30351-167">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="30351-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="30351-168">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="30351-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="30351-169">jeu de données de type Hello typeProperties section **le partage de fichiers** (qui inclut les dataset HDFS) a hello propriétés suivantes</span><span class="sxs-lookup"><span data-stu-id="30351-169">hello typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has hello following properties</span></span>

| <span data-ttu-id="30351-170">Propriété</span><span class="sxs-lookup"><span data-stu-id="30351-170">Property</span></span> | <span data-ttu-id="30351-171">Description</span><span class="sxs-lookup"><span data-stu-id="30351-171">Description</span></span> | <span data-ttu-id="30351-172">Requis</span><span class="sxs-lookup"><span data-stu-id="30351-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="30351-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="30351-173">folderPath</span></span> |<span data-ttu-id="30351-174">Dossier toohello de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="30351-174">Path toohello folder.</span></span> <span data-ttu-id="30351-175">Exemple : `myfolder`</span><span class="sxs-lookup"><span data-stu-id="30351-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="30351-176">Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-176">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="30351-177">Par exemple : pour dossier\sous-dossier, spécifiez dossier\\\\sous-dossier et pour d:\dossier d’exemple, spécifiez d:\\\\dossier d’exemple.</span><span class="sxs-lookup"><span data-stu-id="30351-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="30351-178">Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin.</span><span class="sxs-lookup"><span data-stu-id="30351-178">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="30351-179">Oui</span><span class="sxs-lookup"><span data-stu-id="30351-179">Yes</span></span> |
| <span data-ttu-id="30351-180">fileName</span><span class="sxs-lookup"><span data-stu-id="30351-180">fileName</span></span> |<span data-ttu-id="30351-181">Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-181">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="30351-182">Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-182">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="30351-183">Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format :</span><span class="sxs-lookup"><span data-stu-id="30351-183">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="30351-184">Data<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="30351-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="30351-185">Non</span><span class="sxs-lookup"><span data-stu-id="30351-185">No</span></span> |
| <span data-ttu-id="30351-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="30351-186">partitionedBy</span></span> |<span data-ttu-id="30351-187">partitionedBy peut être utilisé toospecify un folderPath dynamique, le nom de fichier de données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="30351-187">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="30351-188">Exemple : folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="30351-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="30351-189">Non</span><span class="sxs-lookup"><span data-stu-id="30351-189">No</span></span> |
| <span data-ttu-id="30351-190">format</span><span class="sxs-lookup"><span data-stu-id="30351-190">format</span></span> | <span data-ttu-id="30351-191">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="30351-191">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="30351-192">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="30351-192">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="30351-193">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="30351-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="30351-194">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="30351-194">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="30351-195">Non</span><span class="sxs-lookup"><span data-stu-id="30351-195">No</span></span> |
| <span data-ttu-id="30351-196">compression</span><span class="sxs-lookup"><span data-stu-id="30351-196">compression</span></span> | <span data-ttu-id="30351-197">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="30351-197">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="30351-198">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="30351-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="30351-199">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="30351-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="30351-200">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="30351-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="30351-201">Non</span><span class="sxs-lookup"><span data-stu-id="30351-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="30351-202">fileName et fileFilter ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="30351-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="30351-203">Utilisation de la propriété partitionedBy</span><span class="sxs-lookup"><span data-stu-id="30351-203">Using partionedBy property</span></span>
<span data-ttu-id="30351-204">Comme indiqué dans la section précédente de hello, vous pouvez spécifier un folderPath dynamique et le nom de fichier de données de série chronologique par hello **partitionedBy** propriété, [fonctions de la fabrique de données et les variables système hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="30351-204">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="30351-205">toolearn en savoir plus sur les jeux de données de série temps, en planifiant et secteurs, consultez [création de Datasets](data-factory-create-datasets.md), [de planification et l’exécution de](data-factory-scheduling-and-execution.md), et [création de Pipelines](data-factory-create-pipelines.md) articles.</span><span class="sxs-lookup"><span data-stu-id="30351-205">toolearn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="30351-206">Exemple 1 :</span><span class="sxs-lookup"><span data-stu-id="30351-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="30351-207">Dans cet exemple {Slice} est remplacé par la valeur hello de fabrique de données variable système SliceStart au format (AAAAMMJJHH) de la hello spécifiée.</span><span class="sxs-lookup"><span data-stu-id="30351-207">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="30351-208">Hello SliceStart fait référence à des temps de toostart de tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-208">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="30351-209">Hello folderPath est différent pour chaque secteur.</span><span class="sxs-lookup"><span data-stu-id="30351-209">hello folderPath is different for each slice.</span></span> <span data-ttu-id="30351-210">Par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="30351-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="30351-211">Exemple 2 :</span><span class="sxs-lookup"><span data-stu-id="30351-211">Sample 2:</span></span>

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
<span data-ttu-id="30351-212">Dans cet exemple, l'année, le mois, le jour et l'heure de SliceStart sont extraits dans des variables distinctes qui sont utilisées par les propriétés folderPath et fileName.</span><span class="sxs-lookup"><span data-stu-id="30351-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="30351-213">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="30351-213">Copy activity properties</span></span>
<span data-ttu-id="30351-214">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="30351-214">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="30351-215">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="30351-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="30351-216">Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="30351-216">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="30351-217">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="30351-217">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="30351-218">Pour l’activité de copie, lors de la source est de type **FileSystemSource** hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="30351-218">For Copy Activity, when source is of type **FileSystemSource** hello following properties are available in typeProperties section:</span></span>

<span data-ttu-id="30351-219">**FileSystemSource** prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="30351-219">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="30351-220">Propriété</span><span class="sxs-lookup"><span data-stu-id="30351-220">Property</span></span> | <span data-ttu-id="30351-221">Description</span><span class="sxs-lookup"><span data-stu-id="30351-221">Description</span></span> | <span data-ttu-id="30351-222">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="30351-222">Allowed values</span></span> | <span data-ttu-id="30351-223">Requis</span><span class="sxs-lookup"><span data-stu-id="30351-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="30351-224">recursive</span><span class="sxs-lookup"><span data-stu-id="30351-224">recursive</span></span> |<span data-ttu-id="30351-225">Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-225">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="30351-226">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="30351-226">True, False (default)</span></span> |<span data-ttu-id="30351-227">Non</span><span class="sxs-lookup"><span data-stu-id="30351-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="30351-228">Formats de fichier et de compression pris en charge</span><span class="sxs-lookup"><span data-stu-id="30351-228">Supported file and compression formats</span></span>
<span data-ttu-id="30351-229">Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="30351-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a><span data-ttu-id="30351-230">Exemple de JSON : copier des données locales HDFS tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="30351-230">JSON example: Copy data from on-premises HDFS tooAzure Blob</span></span>
<span data-ttu-id="30351-231">Cet exemple montre comment toocopy des données à partir d’un tooAzure HDFS local stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="30351-231">This sample shows how toocopy data from an on-premises HDFS tooAzure Blob Storage.</span></span> <span data-ttu-id="30351-232">Toutefois, les données peuvent être copiées **directement** tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="30351-232">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="30351-233">exemple Hello fournit les définitions de JSON pour hello suivant des entités de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="30351-233">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="30351-234">Vous pouvez utiliser ces définitions de toocreate un pipeline toocopy des données d’HDFS tooAzure stockage d’objets Blob à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="30351-234">You can use these definitions toocreate a pipeline toocopy data from HDFS tooAzure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="30351-235">Un service lié de type [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="30351-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="30351-236">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="30351-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="30351-237">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="30351-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="30351-238">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="30351-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="30351-239">Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="30351-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="30351-240">exemple Hello copie des données à partir d’un tooan HDFS local Azure blob toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="30351-240">hello sample copies data from an on-premises HDFS tooan Azure blob every hour.</span></span> <span data-ttu-id="30351-241">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-241">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="30351-242">Dans un premier temps, configurer la passerelle de gestion des données hello.</span><span class="sxs-lookup"><span data-stu-id="30351-242">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="30351-243">Hello instructions Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="30351-243">hello instructions in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="30351-244">**Service lié de HDFS :** cet exemple utilise hello l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="30351-244">**HDFS linked service:** This example uses hello Windows authentication.</span></span> <span data-ttu-id="30351-245">Consultez la section [Service lié HDFS](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="30351-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="30351-246">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="30351-246">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="30351-247">**HDFS d’entrée de jeu de données :** ce jeu de données fait référence le dossier HDFS toohello DataTransfer/UnitTest /.</span><span class="sxs-lookup"><span data-stu-id="30351-247">**HDFS input dataset:** This dataset refers toohello HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="30351-248">pipeline de Hello copie tous les fichiers de hello dans cette destination toohello de dossier.</span><span class="sxs-lookup"><span data-stu-id="30351-248">hello pipeline copies all hello files in this folder toohello destination.</span></span>

<span data-ttu-id="30351-249">Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="30351-249">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="30351-250">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="30351-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="30351-251">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="30351-251">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="30351-252">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="30351-252">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="30351-253">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="30351-253">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="30351-254">**Activité de copie dans un pipeline avec une source Système de fichiers et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="30351-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="30351-255">pipeline de Hello contient une activité de copie qui est configuré toouse ces jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="30351-255">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="30351-256">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**FileSystemSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="30351-256">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="30351-257">la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="30351-257">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="30351-258">Utilisation de l’authentification Kerberos pour le connecteur HDFS</span><span class="sxs-lookup"><span data-stu-id="30351-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="30351-259">Il existe deux tooset options d’environnement local de hello ainsi en toouse l’authentification Kerberos dans le connecteur HDFS.</span><span class="sxs-lookup"><span data-stu-id="30351-259">There are two options tooset up hello on-premises environment so as toouse Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="30351-260">Vous pouvez choisir de hello une correspond mieux à votre cas.</span><span class="sxs-lookup"><span data-stu-id="30351-260">You can choose hello one better fits your case.</span></span>
* <span data-ttu-id="30351-261">Option 1 : [Joindre l’ordinateur de la passerelle au domaine Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="30351-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="30351-262">Option 2 : [activer l’approbation mutuelle entre le domaine Windows et le domaine Kerberos](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="30351-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="30351-263"><a name="kerberos-join-realm"></a>Option 1 : Joindre l’ordinateur de la passerelle au domaine Kerberos</span><span class="sxs-lookup"><span data-stu-id="30351-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="30351-264">Condition :</span><span class="sxs-lookup"><span data-stu-id="30351-264">Requirement:</span></span>

* <span data-ttu-id="30351-265">ordinateur de passerelle Hello a besoin de domaine Kerberos de hello toojoin et ne peut pas joindre un domaine Windows.</span><span class="sxs-lookup"><span data-stu-id="30351-265">hello gateway machine needs toojoin hello Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="30351-266">Comment tooconfigure :</span><span class="sxs-lookup"><span data-stu-id="30351-266">How tooconfigure:</span></span>

<span data-ttu-id="30351-267">**Sur l’ordinateur de la passerelle :**</span><span class="sxs-lookup"><span data-stu-id="30351-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="30351-268">Exécutez hello **Ksetup** utilitaire tooconfigure hello serveur KDC Kerberos et le domaine.</span><span class="sxs-lookup"><span data-stu-id="30351-268">Run hello **Ksetup** utility tooconfigure hello Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="30351-269">machine de Hello doit être configuré en tant que membre d’un groupe de travail, car un domaine Kerberos est différent d’un domaine Windows.</span><span class="sxs-lookup"><span data-stu-id="30351-269">hello machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="30351-270">Cela est possible en définissant de Kerberos hello et en ajoutant un serveur de contrôleur de domaine Kerberos comme suit.</span><span class="sxs-lookup"><span data-stu-id="30351-270">This can be achieved by setting hello Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="30351-271">Remplacez *REALM.COM* par votre propre domaine respectif en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="30351-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="30351-272">**Redémarrez** machine hello après l’exécution de ces 2 commandes.</span><span class="sxs-lookup"><span data-stu-id="30351-272">**Restart** hello machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="30351-273">Vérifiez la configuration hello avec **Ksetup** commande.</span><span class="sxs-lookup"><span data-stu-id="30351-273">Verify hello configuration with **Ksetup** command.</span></span> <span data-ttu-id="30351-274">sortie de Hello doit être telles que :</span><span class="sxs-lookup"><span data-stu-id="30351-274">hello output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="30351-275">**Dans Azure Data Factory :**</span><span class="sxs-lookup"><span data-stu-id="30351-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="30351-276">Configurer l’utilisation du connecteur hello HDFS **l’authentification Windows** avec Kerberos principal nom et mot de passe tooconnect toohello HDFS source de données.</span><span class="sxs-lookup"><span data-stu-id="30351-276">Configure hello HDFS connector using **Windows authentication** together with your Kerberos principal name and password tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="30351-277">Vérifiez les détails de configuration dans la section sur les [propriétés du service lié HDFS](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="30351-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="30351-278"><a name="kerberos-mutual-trust"></a>Option 2 : activer l’approbation mutuelle entre le domaine Windows et le domaine Kerberos</span><span class="sxs-lookup"><span data-stu-id="30351-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="30351-279">Condition :</span><span class="sxs-lookup"><span data-stu-id="30351-279">Requirement:</span></span>
*   <span data-ttu-id="30351-280">ordinateur de passerelle Hello doit rejoindre un domaine Windows.</span><span class="sxs-lookup"><span data-stu-id="30351-280">hello gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="30351-281">Vous avez besoin des paramètres d’autorisation tooupdate hello du contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="30351-281">You need permission tooupdate hello domain controller's settings.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="30351-282">Comment tooconfigure :</span><span class="sxs-lookup"><span data-stu-id="30351-282">How tooconfigure:</span></span>

> [!NOTE]
> <span data-ttu-id="30351-283">Remplacez le domaine.com et AD.COM Bonjour suivant le didacticiel avec vos propres respectif domaine et contrôleur de domaine en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="30351-283">Replace REALM.COM and AD.COM in hello following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="30351-284">**Sur le serveur KDC :**</span><span class="sxs-lookup"><span data-stu-id="30351-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="30351-285">Modifier la configuration KDC hello **krb5.conf** fichier toolet KDC approbation de domaine Windows toohello suivant le modèle de configuration de référence.</span><span class="sxs-lookup"><span data-stu-id="30351-285">Edit hello KDC configuration in **krb5.conf** file toolet KDC trust Windows Domain referring toohello following configuration template.</span></span> <span data-ttu-id="30351-286">Par défaut, configuration de hello se trouve dans **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="30351-286">By default, hello configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="30351-287">**Redémarrez** hello service KDC après la configuration.</span><span class="sxs-lookup"><span data-stu-id="30351-287">**Restart** hello KDC service after configuration.</span></span>

2.  <span data-ttu-id="30351-288">Préparer un principal nommé  **krbtgt/REALM.COM@AD.COM**  dans serveur KDC avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="30351-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with hello following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="30351-289">Dans le fichier de configuration du service HDFS **hadoop.security.auth_to_local**, ajoutez `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="30351-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="30351-290">**Sur le contrôleur de domaine :**</span><span class="sxs-lookup"><span data-stu-id="30351-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="30351-291">Exécutez hello **Ksetup** commandes tooadd une entrée de domaine :</span><span class="sxs-lookup"><span data-stu-id="30351-291">Run hello following **Ksetup** commands tooadd a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="30351-292">Établir l’approbation de domaine Windows tooKerberos domaine.</span><span class="sxs-lookup"><span data-stu-id="30351-292">Establish trust from Windows Domain tooKerberos Realm.</span></span> <span data-ttu-id="30351-293">[] est hello mot de passe pour le principal de hello  **krbtgt/REALM.COM@AD.COM** .</span><span class="sxs-lookup"><span data-stu-id="30351-293">[password] is hello password for hello principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="30351-294">Sélectionnez l’algorithme de chiffrement utilisé dans Kerberos.</span><span class="sxs-lookup"><span data-stu-id="30351-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="30351-295">Accédez tooServer Manager > Gestion des stratégies de groupe > domaine > objets de stratégie de groupe > par défaut ou stratégie de domaine Active et modifier.</span><span class="sxs-lookup"><span data-stu-id="30351-295">Go tooServer Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="30351-296">Bonjour **éditeur de gestion de stratégie de groupe** fenêtre contextuelle, accédez tooComputer Configuration > stratégies > Paramètres Windows > Paramètres de sécurité > Stratégies locales > Options de sécurité et configurer **réseau sécurité : configurer les types de chiffrement autorisés pour Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="30351-296">In hello **Group Policy Management Editor** popup window, go tooComputer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="30351-297">Algorithme de chiffrement hello sélectionnez souhaité toouse lorsque connectez tooKDC.</span><span class="sxs-lookup"><span data-stu-id="30351-297">Select hello encryption algorithm you want toouse when connect tooKDC.</span></span> <span data-ttu-id="30351-298">En règle générale, vous pouvez simplement sélectionner toutes les options de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-298">Commonly, you can simply select all hello options.</span></span>

        ![Configuration des types de chiffrement pour Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="30351-300">Utilisez **Ksetup** algorithme de chiffrement du hello commande toospecify toobe utilisé sur hello domaine spécifique.</span><span class="sxs-lookup"><span data-stu-id="30351-300">Use **Ksetup** command toospecify hello encryption algorithm toobe used on hello specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="30351-301">Créer un mappage de hello entre le compte de domaine hello et Kerberos principal, dans l’ordre toouse principal Kerberos dans un domaine Windows.</span><span class="sxs-lookup"><span data-stu-id="30351-301">Create hello mapping between hello domain account and Kerberos principal, in order toouse Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="30351-302">Démarrer les outils d’administration hello > **Active Directory Users and Computers**.</span><span class="sxs-lookup"><span data-stu-id="30351-302">Start hello Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="30351-303">Pour configurer les fonctionnalités avancées, cliquez sur **Affichage** > **Fonctionnalités avancées**.</span><span class="sxs-lookup"><span data-stu-id="30351-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="30351-304">Recherchez hello compte toowhich vous souhaitez les mappages toocreate, avec le bouton droit tooview **mappages nom** > cliquez sur **noms Kerberos** onglet.</span><span class="sxs-lookup"><span data-stu-id="30351-304">Locate hello account toowhich you want toocreate mappings, and right-click tooview **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="30351-305">Ajouter un principal de domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="30351-305">Add a principal from hello realm.</span></span>

        ![Mappage des identités de sécurité](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="30351-307">**Sur l’ordinateur de la passerelle :**</span><span class="sxs-lookup"><span data-stu-id="30351-307">**On gateway machine:**</span></span>

* <span data-ttu-id="30351-308">Exécutez hello **Ksetup** commandes tooadd une entrée de domaine.</span><span class="sxs-lookup"><span data-stu-id="30351-308">Run hello following **Ksetup** commands tooadd a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="30351-309">**Dans Azure Data Factory :**</span><span class="sxs-lookup"><span data-stu-id="30351-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="30351-310">Configurer l’utilisation du connecteur hello HDFS **l’authentification Windows** avec votre compte de domaine ou une source de données Principal Kerberos tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="30351-310">Configure hello HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="30351-311">Vérifiez les détails de configuration dans la section sur les [propriétés du service lié HDFS](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="30351-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="30351-312">colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="30351-312">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="30351-313">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="30351-313">Performance and Tuning</span></span>
<span data-ttu-id="30351-314">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="30351-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
