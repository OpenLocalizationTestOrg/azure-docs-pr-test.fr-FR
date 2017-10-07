---
title: "aaaMove des données à partir de DB2 à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Découvrez comment toomove des données à partir d’un DB2 sur site de base de données à l’aide d’activité de copie de fabrique de données Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="afe36-103">Déplacer des données depuis DB2 à l’aide de l’activité de copie dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="afe36-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="afe36-104">Cet article décrit comment vous pouvez utiliser l’activité de copie de données de toocopy Azure Data Factory à partir d’une banque de données de tooa de base de données locale DB2.</span><span class="sxs-lookup"><span data-stu-id="afe36-104">This article describes how you can use Copy Activity in Azure Data Factory toocopy data from an on-premises DB2 database tooa data store.</span></span> <span data-ttu-id="afe36-105">Vous pouvez copier le magasin de tooany de données qui est répertorié comme un récepteur pris en charge dans hello [activités de déplacement de données de Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) l’article.</span><span class="sxs-lookup"><span data-stu-id="afe36-105">You can copy data tooany store that is listed as a supported sink in hello [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="afe36-106">Cette rubrique s’appuie sur l’article Data Factory hello, qui présente une vue d’ensemble du déplacement des données à l’aide de l’activité de copie et répertorie les combinaisons de magasin de données hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="afe36-106">This topic builds on hello Data Factory article, which presents an overview of data movement by using Copy Activity and lists hello supported data store combinations.</span></span> 

<span data-ttu-id="afe36-107">Fabrique de données prend actuellement en charge le déplacement des données uniquement à partir d’un tooa de la base de données DB2 [magasin de données pris en charge de récepteur](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="afe36-107">Data Factory currently supports only moving data from a DB2 database tooa [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="afe36-108">Déplacement des données à partir d’autres données stocke tooa DB2 de base de données n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="afe36-108">Moving data from other data stores tooa DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afe36-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="afe36-109">Prerequisites</span></span>
<span data-ttu-id="afe36-110">Fabrique de données prend en charge la connexion de base de données DB2 de local tooan à l’aide de hello [passerelle de gestion des données](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="afe36-110">Data Factory supports connecting tooan on-premises DB2 database by using hello [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="afe36-111">Pour tooset des instructions pas à pas les données de passerelle hello pipeline toomove vos données, consultez hello [déplacer des données locales toocloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="afe36-111">For step-by-step instructions tooset up hello gateway data pipeline toomove your data, see hello [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="afe36-112">Une passerelle est requise même si DB2 hello est hébergé sur la machine virtuelle de Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="afe36-112">A gateway is required even if hello DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="afe36-113">Vous pouvez installer la passerelle de hello sur hello même VM IaaS comme magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-113">You can install hello gateway on hello same IaaS VM as hello data store.</span></span> <span data-ttu-id="afe36-114">Si la passerelle de hello peut se connecter toohello de base de données, vous pouvez installer la passerelle de hello sur une machine virtuelle différente.</span><span class="sxs-lookup"><span data-stu-id="afe36-114">If hello gateway can connect toohello database, you can install hello gateway on a different VM.</span></span>

<span data-ttu-id="afe36-115">passerelle de gestion des données Hello fournit un pilote DB2 intégré, donc vous ne devez toomanually installer les une pilote toocopy données à partir de DB2.</span><span class="sxs-lookup"><span data-stu-id="afe36-115">hello data management gateway provides a built-in DB2 driver, so you don't need toomanually install a driver toocopy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="afe36-116">Pour obtenir des conseils sur la résolution des problèmes de connexion et les problèmes de passerelle, consultez hello [résoudre les problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) l’article.</span><span class="sxs-lookup"><span data-stu-id="afe36-116">For tips on troubleshooting connection and gateway issues, see hello [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="afe36-117">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="afe36-117">Supported versions</span></span>
<span data-ttu-id="afe36-118">connecteur de Hello DB2 de fabrique de données prend en charge hello suivant plateformes IBM DB2 et les versions avec le Gestionnaire d’accès de base de données Architecture DRDA (Distributed Relational) SQL versions 9, 10 et 11 :</span><span class="sxs-lookup"><span data-stu-id="afe36-118">hello Data Factory DB2 connector supports hello following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="afe36-119">IBM DB2 pour z/OS version 11.1</span><span class="sxs-lookup"><span data-stu-id="afe36-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="afe36-120">IBM DB2 pour z/OS version 10.1</span><span class="sxs-lookup"><span data-stu-id="afe36-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="afe36-121">IBM DB2 pour i (AS400) version 7.2</span><span class="sxs-lookup"><span data-stu-id="afe36-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="afe36-122">IBM DB2 pour i (AS400) version 7.1</span><span class="sxs-lookup"><span data-stu-id="afe36-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="afe36-123">IBM DB2 pour Linux, UNIX et Windows (LUW) version 11</span><span class="sxs-lookup"><span data-stu-id="afe36-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="afe36-124">IBM DB2 pour LUW version 10.5</span><span class="sxs-lookup"><span data-stu-id="afe36-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="afe36-125">IBM DB2 pour LUW version 10.1</span><span class="sxs-lookup"><span data-stu-id="afe36-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="afe36-126">Si vous recevez message d’erreur hello « demande hello package correspondant tooan SQL instruction d’exécution introuvable.</span><span class="sxs-lookup"><span data-stu-id="afe36-126">If you receive hello error message "hello package corresponding tooan SQL statement execution request was not found.</span></span> <span data-ttu-id="afe36-127">SQLSTATE = 51002 SQLCODE =-805, « hello fait un package nécessaire n’est pas créé pour un utilisateur normal de hello sur hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="afe36-127">SQLSTATE=51002 SQLCODE=-805," hello reason is a necessary package is not created for hello normal user on hello OS.</span></span> <span data-ttu-id="afe36-128">tooresolve ce problème, suivez ces instructions pour le type de votre serveur DB2 :</span><span class="sxs-lookup"><span data-stu-id="afe36-128">tooresolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="afe36-129">DB2 pour i (AS400) : permettent à un utilisateur avec pouvoir de créer la collection hello pour un utilisateur normal de hello avant d’exécuter l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="afe36-129">DB2 for i (AS400): Let a power user create hello collection for hello normal user before running Copy Activity.</span></span> <span data-ttu-id="afe36-130">collection de hello toocreate, utilisez hello commande :`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="afe36-130">toocreate hello collection, use hello command: `create collection <username>`</span></span>
> - <span data-ttu-id="afe36-131">DB2 pour z/OS ou LUW : utilisez un compte doté de privilèges élevés, un utilisateur avec pouvoir ou un administrateur qui a des autorités de package et de liaison, BINDADD, ACCORDEZ les autorisations de tooPUBLIC EXECUTE--copie de hello toorun qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="afe36-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE tooPUBLIC permissions--toorun hello copy once.</span></span> <span data-ttu-id="afe36-132">package nécessaire de Hello est créé automatiquement pendant la copie de hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-132">hello necessary package is automatically created during hello copy.</span></span> <span data-ttu-id="afe36-133">Par la suite, vous pouvez basculer utilisateur normal de toohello arrière pour vos séries de copie suivantes.</span><span class="sxs-lookup"><span data-stu-id="afe36-133">Afterward, you can switch back toohello normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="afe36-134">Prise en main</span><span class="sxs-lookup"><span data-stu-id="afe36-134">Getting started</span></span>
<span data-ttu-id="afe36-135">Vous pouvez créer un pipeline comportant des données d’activité toomove copie à partir d’une banque de données DB2 locale à l’aide de différents outils et API :</span><span class="sxs-lookup"><span data-stu-id="afe36-135">You can create a pipeline with a copy activity toomove data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="afe36-136">toocreate de façon plus simple Hello un pipeline est toouse hello Assistant de copie de fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="afe36-136">hello easiest way toocreate a pipeline is toouse hello Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="afe36-137">Pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant copie de hello, consultez hello [didacticiel : créer un pipeline à l’aide de hello Assistant copie de](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="afe36-137">For a quick walkthrough on creating a pipeline by using hello Copy Wizard, see hello [Tutorial: Create a pipeline by using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="afe36-138">Vous pouvez également utiliser les outils toocreate un pipeline, y compris hello portail Azure, Visual Studio, Azure PowerShell, un modèle Azure Resource Manager, hello API .NET et hello API REST.</span><span class="sxs-lookup"><span data-stu-id="afe36-138">You can also use tools toocreate a pipeline, including hello Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, hello .NET API, and hello REST API.</span></span> <span data-ttu-id="afe36-139">Pour obtenir des instructions toocreate un pipeline avec une activité de copie, consultez hello [didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="afe36-139">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="afe36-140">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="afe36-140">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="afe36-141">Créer fabrique de données tooyour de magasins de services liés toolink des données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="afe36-141">Create linked services toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="afe36-142">Créer des groupes de données toorepresent d’entrée et sortie des données pour l’opération de copie hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-142">Create datasets toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="afe36-143">Création d’un pipeline avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="afe36-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="afe36-144">Lorsque vous utilisez hello Assistant copie de définitions de JSON pour les services de fabrique de données lié hello, jeux de données et des entités de pipeline sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="afe36-144">When you use hello Copy Wizard, JSON definitions for hello Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="afe36-145">Lorsque vous utilisez des API ou des outils (à l’exception de hello API .NET), vous définissez des entités de fabrique de données hello à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-145">When you use tools or APIs (except hello .NET API), you define hello Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="afe36-146">Hello [exemple de JSON : copier des données à partir de DB2 tooAzure stockage d’objets Blob](#json-example-copy-data-from-db2-to-azure-blob) montre définitions JSON hello hello des entités de fabrique de données qui sont des données toocopy utilisé à partir d’une banque de données DB2 locale.</span><span class="sxs-lookup"><span data-stu-id="afe36-146">hello [JSON example: Copy data from DB2 tooAzure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows hello JSON definitions for hello Data Factory entities that are used toocopy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="afe36-147">Hello les sections suivantes fournit des détails sur hello propriétés JSON qui sont des entités de fabrique de données hello toodefine utilisés qui sont le magasin de données spécifique tooa DB2.</span><span class="sxs-lookup"><span data-stu-id="afe36-147">hello following sections provide details about hello JSON properties that are used toodefine hello Data Factory entities that are specific tooa DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="afe36-148">Propriétés du service lié DB2</span><span class="sxs-lookup"><span data-stu-id="afe36-148">DB2 linked service properties</span></span>
<span data-ttu-id="afe36-149">Hello tableau suivant répertorie les propriétés JSON de hello tooa spécifique au service lié DB2.</span><span class="sxs-lookup"><span data-stu-id="afe36-149">hello following table lists hello JSON properties that are specific tooa DB2 linked service.</span></span>

| <span data-ttu-id="afe36-150">Propriété</span><span class="sxs-lookup"><span data-stu-id="afe36-150">Property</span></span> | <span data-ttu-id="afe36-151">Description</span><span class="sxs-lookup"><span data-stu-id="afe36-151">Description</span></span> | <span data-ttu-id="afe36-152">Requis</span><span class="sxs-lookup"><span data-stu-id="afe36-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="afe36-153">**type**</span><span class="sxs-lookup"><span data-stu-id="afe36-153">**type**</span></span> |<span data-ttu-id="afe36-154">Cette propriété doit être définie trop**OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="afe36-154">This property must be set too**OnPremisesDB2**.</span></span> |<span data-ttu-id="afe36-155">Oui</span><span class="sxs-lookup"><span data-stu-id="afe36-155">Yes</span></span> |
| <span data-ttu-id="afe36-156">**server**</span><span class="sxs-lookup"><span data-stu-id="afe36-156">**server**</span></span> |<span data-ttu-id="afe36-157">nom de Hello du serveur de hello DB2.</span><span class="sxs-lookup"><span data-stu-id="afe36-157">hello name of hello DB2 server.</span></span> |<span data-ttu-id="afe36-158">Oui</span><span class="sxs-lookup"><span data-stu-id="afe36-158">Yes</span></span> |
| <span data-ttu-id="afe36-159">**database**</span><span class="sxs-lookup"><span data-stu-id="afe36-159">**database**</span></span> |<span data-ttu-id="afe36-160">nom Hello de base de données hello DB2.</span><span class="sxs-lookup"><span data-stu-id="afe36-160">hello name of hello DB2 database.</span></span> |<span data-ttu-id="afe36-161">Oui</span><span class="sxs-lookup"><span data-stu-id="afe36-161">Yes</span></span> |
| <span data-ttu-id="afe36-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="afe36-162">**schema**</span></span> |<span data-ttu-id="afe36-163">nom de Hello du schéma hello hello DB2 de base de données.</span><span class="sxs-lookup"><span data-stu-id="afe36-163">hello name of hello schema in hello DB2 database.</span></span> <span data-ttu-id="afe36-164">Cette propriété est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="afe36-164">This property is case-sensitive.</span></span> |<span data-ttu-id="afe36-165">Non</span><span class="sxs-lookup"><span data-stu-id="afe36-165">No</span></span> |
| <span data-ttu-id="afe36-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="afe36-166">**authenticationType**</span></span> |<span data-ttu-id="afe36-167">type de Hello d’authentification qui est la base de données utilisé tooconnect toohello DB2.</span><span class="sxs-lookup"><span data-stu-id="afe36-167">hello type of authentication that is used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="afe36-168">Hello les valeurs possibles sont : anonyme, Basic et Windows.</span><span class="sxs-lookup"><span data-stu-id="afe36-168">hello possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="afe36-169">Oui</span><span class="sxs-lookup"><span data-stu-id="afe36-169">Yes</span></span> |
| <span data-ttu-id="afe36-170">**nom d’utilisateur**</span><span class="sxs-lookup"><span data-stu-id="afe36-170">**username**</span></span> |<span data-ttu-id="afe36-171">Hello nom hello compte d’utilisateur si vous utilisez l’authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="afe36-171">hello name for hello user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="afe36-172">Non</span><span class="sxs-lookup"><span data-stu-id="afe36-172">No</span></span> |
| <span data-ttu-id="afe36-173">**mot de passe**</span><span class="sxs-lookup"><span data-stu-id="afe36-173">**password**</span></span> |<span data-ttu-id="afe36-174">mot de passe Hello hello compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afe36-174">hello password for hello user account.</span></span> |<span data-ttu-id="afe36-175">Non</span><span class="sxs-lookup"><span data-stu-id="afe36-175">No</span></span> |
| <span data-ttu-id="afe36-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="afe36-176">**gatewayName**</span></span> |<span data-ttu-id="afe36-177">nom Hello de passerelle hello hello service Data Factory doit utiliser la base de données DB2 tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="afe36-177">hello name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="afe36-178">Oui</span><span class="sxs-lookup"><span data-stu-id="afe36-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="afe36-179">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="afe36-179">Dataset properties</span></span>
<span data-ttu-id="afe36-180">Pour obtenir la liste des sections de hello et des propriétés qui sont disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="afe36-180">For a list of hello sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="afe36-181">Sections, tel que **structure**, **disponibilité**et hello **stratégie** pour un jeu de données JSON, sont similaires pour tous les types de jeu de données (SQL Azure, le stockage Blob Azure, Azure Table stockage et ainsi de suite).</span><span class="sxs-lookup"><span data-stu-id="afe36-181">Sections, such as **structure**, **availability**, and hello **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="afe36-182">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-182">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="afe36-183">Hello **typeProperties** section pour un jeu de données de type **RelationalTable**, qui inclut le jeu de données hello DB2, a hello suivant la propriété :</span><span class="sxs-lookup"><span data-stu-id="afe36-183">hello **typeProperties** section for a dataset of type **RelationalTable**, which includes hello DB2 dataset, has hello following property:</span></span>

| <span data-ttu-id="afe36-184">Propriété</span><span class="sxs-lookup"><span data-stu-id="afe36-184">Property</span></span> | <span data-ttu-id="afe36-185">Description</span><span class="sxs-lookup"><span data-stu-id="afe36-185">Description</span></span> | <span data-ttu-id="afe36-186">Requis</span><span class="sxs-lookup"><span data-stu-id="afe36-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="afe36-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="afe36-187">**tableName**</span></span> |<span data-ttu-id="afe36-188">nom de Hello de table hello d’instance de base de données DB2 de hello hello service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="afe36-188">hello name of hello table in hello DB2 database instance that hello linked service refers to.</span></span> <span data-ttu-id="afe36-189">Cette propriété est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="afe36-189">This property is case-sensitive.</span></span> |<span data-ttu-id="afe36-190">Non (si hello **requête** propriété d’une activité de copie de type **RelationalSource** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="afe36-190">No (if hello **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="afe36-191">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="afe36-191">Copy Activity properties</span></span>
<span data-ttu-id="afe36-192">Pour obtenir la liste des sections de hello et des propriétés qui sont disponibles pour la définition d’activités de copie, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="afe36-192">For a list of hello sections and properties that are available for defining copy activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="afe36-193">Les propriétés d’activité de copie comme le **nom**, la **description**, la table d’**entrée**, la table de **sortie** et la **stratégie** sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="afe36-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="afe36-194">Hello des propriétés qui sont disponibles dans hello **typeProperties** section d’activité hello pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="afe36-194">hello properties that are available in hello **typeProperties** section of hello activity for each activity type.</span></span> <span data-ttu-id="afe36-195">Pour l’activité de copie, les propriétés de hello varient en fonction des types hello de sources de données et les récepteurs.</span><span class="sxs-lookup"><span data-stu-id="afe36-195">For Copy Activity, hello properties vary depending on hello types of data sources and sinks.</span></span>

<span data-ttu-id="afe36-196">Pour l’activité de copie, lors de la source de hello est de type **RelationalSource** (qui inclut DB2), hello propriétés suivantes est disponible dans hello **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="afe36-196">For Copy Activity, when hello source is of type **RelationalSource** (which includes DB2), hello following properties are available in hello **typeProperties** section:</span></span>

| <span data-ttu-id="afe36-197">Propriété</span><span class="sxs-lookup"><span data-stu-id="afe36-197">Property</span></span> | <span data-ttu-id="afe36-198">Description</span><span class="sxs-lookup"><span data-stu-id="afe36-198">Description</span></span> | <span data-ttu-id="afe36-199">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="afe36-199">Allowed values</span></span> | <span data-ttu-id="afe36-200">Requis</span><span class="sxs-lookup"><span data-stu-id="afe36-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="afe36-201">**query**</span><span class="sxs-lookup"><span data-stu-id="afe36-201">**query**</span></span> |<span data-ttu-id="afe36-202">Utiliser des données de hello tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="afe36-202">Use hello custom query tooread hello data.</span></span> |<span data-ttu-id="afe36-203">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="afe36-203">SQL query string.</span></span> <span data-ttu-id="afe36-204">Par exemple : `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="afe36-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="afe36-205">Non (si hello **tableName** propriété d’un jeu de données est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="afe36-205">No (if hello **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="afe36-206">Les noms de schéma et de table respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="afe36-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="afe36-207">Dans l’instruction de requête hello, placez les noms de propriétés à l’aide de « » (guillemets doubles).</span><span class="sxs-lookup"><span data-stu-id="afe36-207">In hello query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="afe36-208">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="afe36-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a><span data-ttu-id="afe36-209">Exemple de JSON : copier des données à partir de DB2 tooAzure stockage d’objets Blob</span><span class="sxs-lookup"><span data-stu-id="afe36-209">JSON example: Copy data from DB2 tooAzure Blob storage</span></span>
<span data-ttu-id="afe36-210">Cet exemple fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de hello [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="afe36-210">This example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="afe36-211">Hello montre tooBlob stockage base de données toocopy à partir de DB2.</span><span class="sxs-lookup"><span data-stu-id="afe36-211">hello example shows you how toocopy data from a DB2 database tooBlob storage.</span></span> <span data-ttu-id="afe36-212">Toutefois, les données peuvent être copiées trop[toutes les données prises en charge stocker le type de récepteur](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide d’activité de copie de fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="afe36-212">However, data can be copied too[any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="afe36-213">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="afe36-213">hello sample has hello following Data Factory entities:</span></span>

- <span data-ttu-id="afe36-214">Un service lié DB2 de type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="afe36-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="afe36-215">Un service lié de stockage Azure Blob de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="afe36-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="afe36-216">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="afe36-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="afe36-217">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="afe36-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="afe36-218">A [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) propriétés</span><span class="sxs-lookup"><span data-stu-id="afe36-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="afe36-219">exemple Hello copie toutes les heures des données à partir d’un résultat de requête dans un tooan de base de données DB2 blob Azure.</span><span class="sxs-lookup"><span data-stu-id="afe36-219">hello sample copies data from a query result in a DB2 database tooan Azure blob hourly.</span></span> <span data-ttu-id="afe36-220">les propriétés JSON Hello qui sont utilisées dans l’exemple hello sont décrites dans les sections hello qui suivent les définitions d’entité hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-220">hello JSON properties that are used in hello sample are described in hello sections that follow hello entity definitions.</span></span>

<span data-ttu-id="afe36-221">Pour commencer, installez et configurez une passerelle de données.</span><span class="sxs-lookup"><span data-stu-id="afe36-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="afe36-222">Instructions sont fournies dans hello [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="afe36-222">Instructions are in hello [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="afe36-223">**Service lié DB2**</span><span class="sxs-lookup"><span data-stu-id="afe36-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="afe36-224">**Service lié Azure Blob Storage**</span><span class="sxs-lookup"><span data-stu-id="afe36-224">**Azure Blob storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="afe36-225">**Jeu de données d’entrée DB2**</span><span class="sxs-lookup"><span data-stu-id="afe36-225">**DB2 input dataset**</span></span>

<span data-ttu-id="afe36-226">exemple Hello part du principe que vous avez créé une table dans DB2 nommé « MyTable » qui comporte une colonne intitulée « timestamp » pour les données de série chronologique hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-226">hello sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for hello time series data.</span></span>

<span data-ttu-id="afe36-227">Hello **externe** propriété a la valeur trop « true ».</span><span class="sxs-lookup"><span data-stu-id="afe36-227">hello **external** property is set too"true."</span></span> <span data-ttu-id="afe36-228">Ce paramètre informe le service de fabrique de données hello que ce jeu de données est la fabrique de données externe toohello et qu’il n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-228">This setting informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="afe36-229">Notez que hello **type** propriété a la valeur trop**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="afe36-229">Notice that hello **type** property is set too**RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="afe36-230">**Jeu de données de sortie d’objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="afe36-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="afe36-231">Les données sont écrites tooa nouvel objet blob toutes les heures en définissant un hello **fréquence** propriété trop « Heure » et hello **intervalle** too1 de propriété.</span><span class="sxs-lookup"><span data-stu-id="afe36-231">Data is written tooa new blob every hour by setting hello **frequency** property too"Hour" and hello **interval** property too1.</span></span> <span data-ttu-id="afe36-232">Hello **folderPath** propriété pour les blob hello est dynamiquement évaluée selon l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="afe36-232">hello **folderPath** property for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="afe36-233">chemin d’accès du dossier Hello utilise hello des parties d’année, mois, jour et heure de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-233">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="afe36-234">**Pipeline pour l’activité de copie hello**</span><span class="sxs-lookup"><span data-stu-id="afe36-234">**Pipeline for hello copy activity**</span></span>

<span data-ttu-id="afe36-235">pipeline de Hello contient une activité de copie qui est configurée toouse spécifié des jeux de données d’entrée et de sortie et qui est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="afe36-235">hello pipeline contains a copy activity that is configured toouse specified input and output datasets and which is scheduled toorun every hour.</span></span> <span data-ttu-id="afe36-236">Bonjour définition JSON pour le pipeline de hello, hello **source** type est défini trop**RelationalSource** et hello **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="afe36-236">In hello JSON definition for hello pipeline, hello **source** type is set too**RelationalSource** and hello **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="afe36-237">la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne les données de salutation à partir de la table « Orders » de hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-237">hello SQL query specified for hello **query** property selects hello data from hello "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="afe36-238">Mappage de type pour DB2</span><span class="sxs-lookup"><span data-stu-id="afe36-238">Type mapping for DB2</span></span>
<span data-ttu-id="afe36-239">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue des conversions de type automatique à partir de la source de type type toosink à l’aide de hello suivant l’approche en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="afe36-239">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type toosink type by using hello following two-step approach:</span></span>

1. <span data-ttu-id="afe36-240">Convertir un type de source native type tooa .NET</span><span class="sxs-lookup"><span data-stu-id="afe36-240">Convert from a native source type tooa .NET type</span></span>
2. <span data-ttu-id="afe36-241">Convertir un type de récepteur natif .NET type tooa</span><span class="sxs-lookup"><span data-stu-id="afe36-241">Convert from a .NET type tooa native sink type</span></span>

<span data-ttu-id="afe36-242">mappages suivants Hello sont utilisées lorsque l’activité de copie convertit les données de salutation à partir d’un type .NET de DB2 type tooa :</span><span class="sxs-lookup"><span data-stu-id="afe36-242">hello following mappings are used when Copy Activity converts hello data from a DB2 type tooa .NET type:</span></span>

| <span data-ttu-id="afe36-243">Type de base de données DB2</span><span class="sxs-lookup"><span data-stu-id="afe36-243">DB2 database type</span></span> | <span data-ttu-id="afe36-244">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="afe36-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="afe36-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="afe36-245">SmallInt</span></span> |<span data-ttu-id="afe36-246">Int16</span><span class="sxs-lookup"><span data-stu-id="afe36-246">Int16</span></span> |
| <span data-ttu-id="afe36-247">Integer</span><span class="sxs-lookup"><span data-stu-id="afe36-247">Integer</span></span> |<span data-ttu-id="afe36-248">Int32</span><span class="sxs-lookup"><span data-stu-id="afe36-248">Int32</span></span> |
| <span data-ttu-id="afe36-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="afe36-249">BigInt</span></span> |<span data-ttu-id="afe36-250">Int64</span><span class="sxs-lookup"><span data-stu-id="afe36-250">Int64</span></span> |
| <span data-ttu-id="afe36-251">Real</span><span class="sxs-lookup"><span data-stu-id="afe36-251">Real</span></span> |<span data-ttu-id="afe36-252">Single</span><span class="sxs-lookup"><span data-stu-id="afe36-252">Single</span></span> |
| <span data-ttu-id="afe36-253">Double</span><span class="sxs-lookup"><span data-stu-id="afe36-253">Double</span></span> |<span data-ttu-id="afe36-254">Double</span><span class="sxs-lookup"><span data-stu-id="afe36-254">Double</span></span> |
| <span data-ttu-id="afe36-255">Float</span><span class="sxs-lookup"><span data-stu-id="afe36-255">Float</span></span> |<span data-ttu-id="afe36-256">Double</span><span class="sxs-lookup"><span data-stu-id="afe36-256">Double</span></span> |
| <span data-ttu-id="afe36-257">Décimal</span><span class="sxs-lookup"><span data-stu-id="afe36-257">Decimal</span></span> |<span data-ttu-id="afe36-258">Décimal</span><span class="sxs-lookup"><span data-stu-id="afe36-258">Decimal</span></span> |
| <span data-ttu-id="afe36-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="afe36-259">DecimalFloat</span></span> |<span data-ttu-id="afe36-260">Décimal</span><span class="sxs-lookup"><span data-stu-id="afe36-260">Decimal</span></span> |
| <span data-ttu-id="afe36-261">Chiffre</span><span class="sxs-lookup"><span data-stu-id="afe36-261">Numeric</span></span> |<span data-ttu-id="afe36-262">Décimal</span><span class="sxs-lookup"><span data-stu-id="afe36-262">Decimal</span></span> |
| <span data-ttu-id="afe36-263">Date</span><span class="sxs-lookup"><span data-stu-id="afe36-263">Date</span></span> |<span data-ttu-id="afe36-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="afe36-264">DateTime</span></span> |
| <span data-ttu-id="afe36-265">Time</span><span class="sxs-lookup"><span data-stu-id="afe36-265">Time</span></span> |<span data-ttu-id="afe36-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="afe36-266">TimeSpan</span></span> |
| <span data-ttu-id="afe36-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="afe36-267">Timestamp</span></span> |<span data-ttu-id="afe36-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="afe36-268">DateTime</span></span> |
| <span data-ttu-id="afe36-269">xml</span><span class="sxs-lookup"><span data-stu-id="afe36-269">Xml</span></span> |<span data-ttu-id="afe36-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="afe36-270">Byte[]</span></span> |
| <span data-ttu-id="afe36-271">Char</span><span class="sxs-lookup"><span data-stu-id="afe36-271">Char</span></span> |<span data-ttu-id="afe36-272">String</span><span class="sxs-lookup"><span data-stu-id="afe36-272">String</span></span> |
| <span data-ttu-id="afe36-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="afe36-273">VarChar</span></span> |<span data-ttu-id="afe36-274">String</span><span class="sxs-lookup"><span data-stu-id="afe36-274">String</span></span> |
| <span data-ttu-id="afe36-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="afe36-275">LongVarChar</span></span> |<span data-ttu-id="afe36-276">String</span><span class="sxs-lookup"><span data-stu-id="afe36-276">String</span></span> |
| <span data-ttu-id="afe36-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="afe36-277">DB2DynArray</span></span> |<span data-ttu-id="afe36-278">String</span><span class="sxs-lookup"><span data-stu-id="afe36-278">String</span></span> |
| <span data-ttu-id="afe36-279">Fichier binaire</span><span class="sxs-lookup"><span data-stu-id="afe36-279">Binary</span></span> |<span data-ttu-id="afe36-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="afe36-280">Byte[]</span></span> |
| <span data-ttu-id="afe36-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="afe36-281">VarBinary</span></span> |<span data-ttu-id="afe36-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="afe36-282">Byte[]</span></span> |
| <span data-ttu-id="afe36-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="afe36-283">LongVarBinary</span></span> |<span data-ttu-id="afe36-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="afe36-284">Byte[]</span></span> |
| <span data-ttu-id="afe36-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="afe36-285">Graphic</span></span> |<span data-ttu-id="afe36-286">String</span><span class="sxs-lookup"><span data-stu-id="afe36-286">String</span></span> |
| <span data-ttu-id="afe36-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="afe36-287">VarGraphic</span></span> |<span data-ttu-id="afe36-288">String</span><span class="sxs-lookup"><span data-stu-id="afe36-288">String</span></span> |
| <span data-ttu-id="afe36-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="afe36-289">LongVarGraphic</span></span> |<span data-ttu-id="afe36-290">String</span><span class="sxs-lookup"><span data-stu-id="afe36-290">String</span></span> |
| <span data-ttu-id="afe36-291">Clob</span><span class="sxs-lookup"><span data-stu-id="afe36-291">Clob</span></span> |<span data-ttu-id="afe36-292">String</span><span class="sxs-lookup"><span data-stu-id="afe36-292">String</span></span> |
| <span data-ttu-id="afe36-293">Blob</span><span class="sxs-lookup"><span data-stu-id="afe36-293">Blob</span></span> |<span data-ttu-id="afe36-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="afe36-294">Byte[]</span></span> |
| <span data-ttu-id="afe36-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="afe36-295">DbClob</span></span> |<span data-ttu-id="afe36-296">String</span><span class="sxs-lookup"><span data-stu-id="afe36-296">String</span></span> |
| <span data-ttu-id="afe36-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="afe36-297">SmallInt</span></span> |<span data-ttu-id="afe36-298">Int16</span><span class="sxs-lookup"><span data-stu-id="afe36-298">Int16</span></span> |
| <span data-ttu-id="afe36-299">Integer</span><span class="sxs-lookup"><span data-stu-id="afe36-299">Integer</span></span> |<span data-ttu-id="afe36-300">Int32</span><span class="sxs-lookup"><span data-stu-id="afe36-300">Int32</span></span> |
| <span data-ttu-id="afe36-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="afe36-301">BigInt</span></span> |<span data-ttu-id="afe36-302">Int64</span><span class="sxs-lookup"><span data-stu-id="afe36-302">Int64</span></span> |
| <span data-ttu-id="afe36-303">Real</span><span class="sxs-lookup"><span data-stu-id="afe36-303">Real</span></span> |<span data-ttu-id="afe36-304">Single</span><span class="sxs-lookup"><span data-stu-id="afe36-304">Single</span></span> |
| <span data-ttu-id="afe36-305">Double</span><span class="sxs-lookup"><span data-stu-id="afe36-305">Double</span></span> |<span data-ttu-id="afe36-306">Double</span><span class="sxs-lookup"><span data-stu-id="afe36-306">Double</span></span> |
| <span data-ttu-id="afe36-307">Float</span><span class="sxs-lookup"><span data-stu-id="afe36-307">Float</span></span> |<span data-ttu-id="afe36-308">Double</span><span class="sxs-lookup"><span data-stu-id="afe36-308">Double</span></span> |
| <span data-ttu-id="afe36-309">Décimal</span><span class="sxs-lookup"><span data-stu-id="afe36-309">Decimal</span></span> |<span data-ttu-id="afe36-310">Décimal</span><span class="sxs-lookup"><span data-stu-id="afe36-310">Decimal</span></span> |
| <span data-ttu-id="afe36-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="afe36-311">DecimalFloat</span></span> |<span data-ttu-id="afe36-312">Décimal</span><span class="sxs-lookup"><span data-stu-id="afe36-312">Decimal</span></span> |
| <span data-ttu-id="afe36-313">Chiffre</span><span class="sxs-lookup"><span data-stu-id="afe36-313">Numeric</span></span> |<span data-ttu-id="afe36-314">Décimal</span><span class="sxs-lookup"><span data-stu-id="afe36-314">Decimal</span></span> |
| <span data-ttu-id="afe36-315">Date</span><span class="sxs-lookup"><span data-stu-id="afe36-315">Date</span></span> |<span data-ttu-id="afe36-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="afe36-316">DateTime</span></span> |
| <span data-ttu-id="afe36-317">Time</span><span class="sxs-lookup"><span data-stu-id="afe36-317">Time</span></span> |<span data-ttu-id="afe36-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="afe36-318">TimeSpan</span></span> |
| <span data-ttu-id="afe36-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="afe36-319">Timestamp</span></span> |<span data-ttu-id="afe36-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="afe36-320">DateTime</span></span> |
| <span data-ttu-id="afe36-321">xml</span><span class="sxs-lookup"><span data-stu-id="afe36-321">Xml</span></span> |<span data-ttu-id="afe36-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="afe36-322">Byte[]</span></span> |
| <span data-ttu-id="afe36-323">Char</span><span class="sxs-lookup"><span data-stu-id="afe36-323">Char</span></span> |<span data-ttu-id="afe36-324">String</span><span class="sxs-lookup"><span data-stu-id="afe36-324">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="afe36-325">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="afe36-325">Map source toosink columns</span></span>
<span data-ttu-id="afe36-326">toolearn colonnes toomap hello toocolumns de jeu de données source dans le jeu de données récepteur hello, voir [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="afe36-326">toolearn how toomap columns in hello source dataset toocolumns in hello sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="afe36-327">Lectures renouvelées de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="afe36-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="afe36-328">Lorsque vous copiez des données à partir d’un magasin de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="afe36-328">When you copy data from a relational data store, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="afe36-329">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="afe36-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="afe36-330">Vous pouvez également configurer les nouvelles tentatives de hello **stratégie** propriété pour un toorerun de jeu de données un secteur lorsqu’une défaillance se produit.</span><span class="sxs-lookup"><span data-stu-id="afe36-330">You can also configure hello retry **policy** property for a dataset toorerun a slice when a failure occurs.</span></span> <span data-ttu-id="afe36-331">Vérifiez que hello les mêmes données ne sont en lecture aucune question comment tranche de hello autant de fois est exécuter à nouveau et indépendamment de la façon dont vous réexécutez tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="afe36-331">Make sure that hello same data is read no matter how many times hello slice is rerun, and regardless of how you rerun hello slice.</span></span> <span data-ttu-id="afe36-332">Pour plus d’informations, consultez [Lectures renouvelées de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="afe36-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="afe36-333">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="afe36-333">Performance and tuning</span></span>
<span data-ttu-id="afe36-334">En savoir plus sur les principaux facteurs qui affectent les performances hello de l’activité de copie et de méthodes toooptimize Bonjour [copie activité Guide des performances et paramétrage](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="afe36-334">Learn about key factors that affect hello performance of Copy Activity and ways toooptimize performance in hello [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
