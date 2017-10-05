---
title: "Déplacer des données depuis DB2 à l’aide d’Azure Data Factory | Microsoft Docs"
description: "Découvrez comment déplacer des données depuis une base de données DB2 locale à l’aide de l’activité de copie dans Azure Data Factory"
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
ms.openlocfilehash: 6a89cc44724dbb5b46a9e89d6da24d9b35ddbbef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="f3b83-103">Déplacer des données depuis DB2 à l’aide de l’activité de copie dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f3b83-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="f3b83-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour copier des données d’une base de données DB2 locale dans un autre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="f3b83-104">This article describes how you can use Copy Activity in Azure Data Factory to copy data from an on-premises DB2 database to a data store.</span></span> <span data-ttu-id="f3b83-105">Vous pouvez copier des données dans n’importe quel magasin figurant dans la liste des récepteurs pris en charge que vous trouverez dans l’article sur les [activités de déplacement de données dans Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f3b83-105">You can copy data to any store that is listed as a supported sink in the [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="f3b83-106">Cette rubrique s’appuie sur l’article concernant Data Factory, qui présente une vue d’ensemble du déplacement de données à l’aide de l’activité de copie et fournit une liste des combinaisons de magasins de données prises en charge.</span><span class="sxs-lookup"><span data-stu-id="f3b83-106">This topic builds on the Data Factory article, which presents an overview of data movement by using Copy Activity and lists the supported data store combinations.</span></span> 

<span data-ttu-id="f3b83-107">Actuellement, Data Factory prend uniquement en charge le déplacement de données depuis une base de données DB2 vers un [magasin de données récepteur pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats),</span><span class="sxs-lookup"><span data-stu-id="f3b83-107">Data Factory currently supports only moving data from a DB2 database to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f3b83-108">et non le déplacement de données depuis d’autres magasins de données vers une base de données DB2.</span><span class="sxs-lookup"><span data-stu-id="f3b83-108">Moving data from other data stores to a DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3b83-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f3b83-109">Prerequisites</span></span>
<span data-ttu-id="f3b83-110">Data Factory prend en charge la connexion à une base de données DB2 locale à l’aide de la [passerelle de gestion des données](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="f3b83-110">Data Factory supports connecting to an on-premises DB2 database by using the [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="f3b83-111">Pour obtenir des instructions détaillées sur la configuration du pipeline de données de la passerelle pour déplacer des données, consultez l’article [Déplacement de données entre des sources locales et le cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="f3b83-111">For step-by-step instructions to set up the gateway data pipeline to move your data, see the [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f3b83-112">Une passerelle est requise même si la base de données DB2 est hébergée sur une machine virtuelle Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="f3b83-112">A gateway is required even if the DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="f3b83-113">Vous pouvez installer la passerelle sur la même machine virtuelle IaaS que le magasin de données,</span><span class="sxs-lookup"><span data-stu-id="f3b83-113">You can install the gateway on the same IaaS VM as the data store.</span></span> <span data-ttu-id="f3b83-114">ou sur une autre machine virtuelle pourvu que la passerelle puisse se connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="f3b83-114">If the gateway can connect to the database, you can install the gateway on a different VM.</span></span>

<span data-ttu-id="f3b83-115">La passerelle de gestion des données fournit un pilote DB2 intégré. Par conséquent, vous n’avez pas besoin d’installer manuellement de pilote lors de la copie de données depuis DB2.</span><span class="sxs-lookup"><span data-stu-id="f3b83-115">The data management gateway provides a built-in DB2 driver, so you don't need to manually install a driver to copy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="f3b83-116">Pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle, consultez l’article [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="f3b83-116">For tips on troubleshooting connection and gateway issues, see the [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="f3b83-117">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="f3b83-117">Supported versions</span></span>
<span data-ttu-id="f3b83-118">Le connecteur DB2 Data Factory prend en charge les plateformes et versions IBM DB2 suivantes avec les versions 9, 10 et 11 de SQL Access Manager Distributed Relational Database Architecture (DRDA) :</span><span class="sxs-lookup"><span data-stu-id="f3b83-118">The Data Factory DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="f3b83-119">IBM DB2 pour z/OS version 11.1</span><span class="sxs-lookup"><span data-stu-id="f3b83-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="f3b83-120">IBM DB2 pour z/OS version 10.1</span><span class="sxs-lookup"><span data-stu-id="f3b83-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="f3b83-121">IBM DB2 pour i (AS400) version 7.2</span><span class="sxs-lookup"><span data-stu-id="f3b83-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="f3b83-122">IBM DB2 pour i (AS400) version 7.1</span><span class="sxs-lookup"><span data-stu-id="f3b83-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="f3b83-123">IBM DB2 pour Linux, UNIX et Windows (LUW) version 11</span><span class="sxs-lookup"><span data-stu-id="f3b83-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="f3b83-124">IBM DB2 pour LUW version 10.5</span><span class="sxs-lookup"><span data-stu-id="f3b83-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="f3b83-125">IBM DB2 pour LUW version 10.1</span><span class="sxs-lookup"><span data-stu-id="f3b83-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="f3b83-126">Si vous recevez le message d’erreur « Le package correspondant à une requête d’exécution d’instruction SQL est introuvable.</span><span class="sxs-lookup"><span data-stu-id="f3b83-126">If you receive the error message "The package corresponding to an SQL statement execution request was not found.</span></span> <span data-ttu-id="f3b83-127">SQLSTATE = 51002 SQLCODE =-805 », la raison en est qu’un package nécessaire n’est pas créé pour l’utilisateur normal sur le système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f3b83-127">SQLSTATE=51002 SQLCODE=-805," the reason is a necessary package is not created for the normal user on the OS.</span></span> <span data-ttu-id="f3b83-128">Pour résoudre le problème, suivez ces instructions en fonction de votre type de serveur DB2 :</span><span class="sxs-lookup"><span data-stu-id="f3b83-128">To resolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="f3b83-129">DB2 pour i (AS400) : demandez à un utilisateur chevronné de créer la collection pour l’utilisateur normal avant d’exécuter l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="f3b83-129">DB2 for i (AS400): Let a power user create the collection for the normal user before running Copy Activity.</span></span> <span data-ttu-id="f3b83-130">Pour créer la collection, utilisez la commande : `create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="f3b83-130">To create the collection, use the command: `create collection <username>`</span></span>
> - <span data-ttu-id="f3b83-131">DB2 pour z/OS ou LUW : utilisez un compte doté de privilèges élevés (utilisateur chevronné ou administrateur disposant d’autorités de package et d’autorisations BIND, BINDADD, GRANT EXECUTE TO PUBLIC) pour exécuter une fois l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="f3b83-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE TO PUBLIC permissions--to run the copy once.</span></span> <span data-ttu-id="f3b83-132">Le package nécessaire est automatiquement créé au cours de la copie.</span><span class="sxs-lookup"><span data-stu-id="f3b83-132">The necessary package is automatically created during the copy.</span></span> <span data-ttu-id="f3b83-133">Vous pouvez ensuite revenir au mode utilisateur normal pour vos copies suivantes.</span><span class="sxs-lookup"><span data-stu-id="f3b83-133">Afterward, you can switch back to the normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f3b83-134">Prise en main</span><span class="sxs-lookup"><span data-stu-id="f3b83-134">Getting started</span></span>
<span data-ttu-id="f3b83-135">Vous pouvez créer un pipeline avec une activité de copie pour déplacer des données d’un magasin de données DB2 local à l’aide de différents outils et API :</span><span class="sxs-lookup"><span data-stu-id="f3b83-135">You can create a pipeline with a copy activity to move data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="f3b83-136">Le moyen le plus simple de créer un pipeline consiste à utiliser l’Assistant de copie Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f3b83-136">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="f3b83-137">Pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant de copie, consultez la page [Didacticiel : Créer un pipeline à l’aide de l’Assistant de copie](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="f3b83-137">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="f3b83-138">Vous pouvez également utiliser des outils pour créer un pipeline, notamment le portail Azure, Visual Studio, Azure PowerShell, un modèle Azure Resource Manager, l’API .NET et l’API REST.</span><span class="sxs-lookup"><span data-stu-id="f3b83-138">You can also use tools to create a pipeline, including the Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, the .NET API, and the REST API.</span></span> <span data-ttu-id="f3b83-139">Pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie, consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f3b83-139">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="f3b83-140">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f3b83-140">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="f3b83-141">Création de services liés pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="f3b83-141">Create linked services to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="f3b83-142">Création de jeux de données pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="f3b83-142">Create datasets to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="f3b83-143">Création d’un pipeline avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="f3b83-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f3b83-144">Lorsque vous utilisez l’Assistant de copie, les définitions JSON des entités de services liés, jeux de données et pipeline Data Factory sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="f3b83-144">When you use the Copy Wizard, JSON definitions for the Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="f3b83-145">Lorsque vous utilisez des outils ou API (à l’exception de l’API .NET), vous devez définir les entités Data Factory à l’aide du format JSON.</span><span class="sxs-lookup"><span data-stu-id="f3b83-145">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="f3b83-146">L’[exemple JSON : copier des données depuis DB2 vers le stockage Azure Blob](#json-example-copy-data-from-db2-to-azure-blob) montre des définitions JSON pour les entités Data Factory utilisées pour copier des données depuis un magasin de données DB2 local.</span><span class="sxs-lookup"><span data-stu-id="f3b83-146">The [JSON example: Copy data from DB2 to Azure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="f3b83-147">Les sections suivantes contiennent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à un magasin de données DB2.</span><span class="sxs-lookup"><span data-stu-id="f3b83-147">The following sections provide details about the JSON properties that are used to define the Data Factory entities that are specific to a DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="f3b83-148">Propriétés du service lié DB2</span><span class="sxs-lookup"><span data-stu-id="f3b83-148">DB2 linked service properties</span></span>
<span data-ttu-id="f3b83-149">Le tableau suivant répertorie les propriétés JSON spécifiques d’un service lié DB2.</span><span class="sxs-lookup"><span data-stu-id="f3b83-149">The following table lists the JSON properties that are specific to a DB2 linked service.</span></span>

| <span data-ttu-id="f3b83-150">Propriété</span><span class="sxs-lookup"><span data-stu-id="f3b83-150">Property</span></span> | <span data-ttu-id="f3b83-151">Description</span><span class="sxs-lookup"><span data-stu-id="f3b83-151">Description</span></span> | <span data-ttu-id="f3b83-152">Requis</span><span class="sxs-lookup"><span data-stu-id="f3b83-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f3b83-153">**type**</span><span class="sxs-lookup"><span data-stu-id="f3b83-153">**type**</span></span> |<span data-ttu-id="f3b83-154">La propriété doit être définie sur **OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="f3b83-154">This property must be set to **OnPremisesDB2**.</span></span> |<span data-ttu-id="f3b83-155">Oui</span><span class="sxs-lookup"><span data-stu-id="f3b83-155">Yes</span></span> |
| <span data-ttu-id="f3b83-156">**server**</span><span class="sxs-lookup"><span data-stu-id="f3b83-156">**server**</span></span> |<span data-ttu-id="f3b83-157">Nom du serveur DB2.</span><span class="sxs-lookup"><span data-stu-id="f3b83-157">The name of the DB2 server.</span></span> |<span data-ttu-id="f3b83-158">Oui</span><span class="sxs-lookup"><span data-stu-id="f3b83-158">Yes</span></span> |
| <span data-ttu-id="f3b83-159">**database**</span><span class="sxs-lookup"><span data-stu-id="f3b83-159">**database**</span></span> |<span data-ttu-id="f3b83-160">Nom de la base de données DB2.</span><span class="sxs-lookup"><span data-stu-id="f3b83-160">The name of the DB2 database.</span></span> |<span data-ttu-id="f3b83-161">Oui</span><span class="sxs-lookup"><span data-stu-id="f3b83-161">Yes</span></span> |
| <span data-ttu-id="f3b83-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="f3b83-162">**schema**</span></span> |<span data-ttu-id="f3b83-163">Nom du schéma dans la base de données DB2.</span><span class="sxs-lookup"><span data-stu-id="f3b83-163">The name of the schema in the DB2 database.</span></span> <span data-ttu-id="f3b83-164">Cette propriété est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="f3b83-164">This property is case-sensitive.</span></span> |<span data-ttu-id="f3b83-165">Non</span><span class="sxs-lookup"><span data-stu-id="f3b83-165">No</span></span> |
| <span data-ttu-id="f3b83-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="f3b83-166">**authenticationType**</span></span> |<span data-ttu-id="f3b83-167">Type d'authentification utilisé pour se connecter à la base de données DB2.</span><span class="sxs-lookup"><span data-stu-id="f3b83-167">The type of authentication that is used to connect to the DB2 database.</span></span> <span data-ttu-id="f3b83-168">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="f3b83-168">The possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="f3b83-169">Oui</span><span class="sxs-lookup"><span data-stu-id="f3b83-169">Yes</span></span> |
| <span data-ttu-id="f3b83-170">**nom d’utilisateur**</span><span class="sxs-lookup"><span data-stu-id="f3b83-170">**username**</span></span> |<span data-ttu-id="f3b83-171">Nom du compte d’utilisateur si vous utilisez l’authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="f3b83-171">The name for the user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="f3b83-172">Non</span><span class="sxs-lookup"><span data-stu-id="f3b83-172">No</span></span> |
| <span data-ttu-id="f3b83-173">**mot de passe**</span><span class="sxs-lookup"><span data-stu-id="f3b83-173">**password**</span></span> |<span data-ttu-id="f3b83-174">Mot de passe du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f3b83-174">The password for the user account.</span></span> |<span data-ttu-id="f3b83-175">Non</span><span class="sxs-lookup"><span data-stu-id="f3b83-175">No</span></span> |
| <span data-ttu-id="f3b83-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="f3b83-176">**gatewayName**</span></span> |<span data-ttu-id="f3b83-177">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données DB2 locale.</span><span class="sxs-lookup"><span data-stu-id="f3b83-177">The name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="f3b83-178">Oui</span><span class="sxs-lookup"><span data-stu-id="f3b83-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="f3b83-179">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="f3b83-179">Dataset properties</span></span>
<span data-ttu-id="f3b83-180">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="f3b83-180">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f3b83-181">Les sections comme la **structure**, la **disponibilité** et la **stratégie** d’un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, stockage Azure Blob, stockage Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="f3b83-181">Sections, such as **structure**, **availability**, and the **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="f3b83-182">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="f3b83-182">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f3b83-183">La section **typeProperties** pour un jeu de données de type **RelationalTable** (qui inclut le jeu de données DB2) a la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="f3b83-183">The **typeProperties** section for a dataset of type **RelationalTable**, which includes the DB2 dataset, has the following property:</span></span>

| <span data-ttu-id="f3b83-184">Propriété</span><span class="sxs-lookup"><span data-stu-id="f3b83-184">Property</span></span> | <span data-ttu-id="f3b83-185">Description</span><span class="sxs-lookup"><span data-stu-id="f3b83-185">Description</span></span> | <span data-ttu-id="f3b83-186">Requis</span><span class="sxs-lookup"><span data-stu-id="f3b83-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f3b83-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="f3b83-187">**tableName**</span></span> |<span data-ttu-id="f3b83-188">Nom de la table dans l'instance de base de données DB2 à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="f3b83-188">The name of the table in the DB2 database instance that the linked service refers to.</span></span> <span data-ttu-id="f3b83-189">Cette propriété est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="f3b83-189">This property is case-sensitive.</span></span> |<span data-ttu-id="f3b83-190">Non (si la propriété **query** d’une activité de copie de type **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="f3b83-190">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f3b83-191">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="f3b83-191">Copy Activity properties</span></span>
<span data-ttu-id="f3b83-192">Pour obtenir la liste des sections et des propriétés disponibles pour la définition des activités de copie, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f3b83-192">For a list of the sections and properties that are available for defining copy activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f3b83-193">Les propriétés d’activité de copie comme le **nom**, la **description**, la table d’**entrée**, la table de **sortie** et la **stratégie** sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="f3b83-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="f3b83-194">Les propriétés disponibles dans la section **typeProperties** de l’activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="f3b83-194">The properties that are available in the **typeProperties** section of the activity for each activity type.</span></span> <span data-ttu-id="f3b83-195">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="f3b83-195">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span></span>

<span data-ttu-id="f3b83-196">Pour l’activité de copie, lorsque la source est de type **RelationalSource** (qui inclut DB2), les propriétés suivantes sont disponibles dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="f3b83-196">For Copy Activity, when the source is of type **RelationalSource** (which includes DB2), the following properties are available in the **typeProperties** section:</span></span>

| <span data-ttu-id="f3b83-197">Propriété</span><span class="sxs-lookup"><span data-stu-id="f3b83-197">Property</span></span> | <span data-ttu-id="f3b83-198">Description</span><span class="sxs-lookup"><span data-stu-id="f3b83-198">Description</span></span> | <span data-ttu-id="f3b83-199">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="f3b83-199">Allowed values</span></span> | <span data-ttu-id="f3b83-200">Requis</span><span class="sxs-lookup"><span data-stu-id="f3b83-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f3b83-201">**query**</span><span class="sxs-lookup"><span data-stu-id="f3b83-201">**query**</span></span> |<span data-ttu-id="f3b83-202">Utilise la requête personnalisée pour lire les données.</span><span class="sxs-lookup"><span data-stu-id="f3b83-202">Use the custom query to read the data.</span></span> |<span data-ttu-id="f3b83-203">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="f3b83-203">SQL query string.</span></span> <span data-ttu-id="f3b83-204">Par exemple : `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="f3b83-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="f3b83-205">Non (si la propriété **tableName** d’un jeu de données est spécifié)</span><span class="sxs-lookup"><span data-stu-id="f3b83-205">No (if the **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="f3b83-206">Les noms de schéma et de table respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="f3b83-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="f3b83-207">Dans l’instruction de requête, mettez les noms de propriétés entre "" (guillemets doubles).</span><span class="sxs-lookup"><span data-stu-id="f3b83-207">In the query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="f3b83-208">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f3b83-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-to-azure-blob-storage"></a><span data-ttu-id="f3b83-209">Exemple JSON : copie de données de DB2 vers le stockage Azure Blob</span><span class="sxs-lookup"><span data-stu-id="f3b83-209">JSON example: Copy data from DB2 to Azure Blob storage</span></span>
<span data-ttu-id="f3b83-210">Cet exemple présente des exemples de définition JSON, que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou d’[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f3b83-210">This example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f3b83-211">L’exemple montre comment copier des données depuis une base de données DB2 dans le stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="f3b83-211">The example shows you how to copy data from a DB2 database to Blob storage.</span></span> <span data-ttu-id="f3b83-212">Les données peuvent toutefois être copiées dans [tout magasin de données récepteur pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de l’activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f3b83-212">However, data can be copied to [any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="f3b83-213">L’exemple contient les entités Data Factory suivantes :</span><span class="sxs-lookup"><span data-stu-id="f3b83-213">The sample has the following Data Factory entities:</span></span>

- <span data-ttu-id="f3b83-214">Un service lié DB2 de type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="f3b83-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="f3b83-215">Un service lié de stockage Azure Blob de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="f3b83-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="f3b83-216">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="f3b83-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="f3b83-217">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="f3b83-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="f3b83-218">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise les propriétés [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="f3b83-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="f3b83-219">L'exemple copie toutes les heures les données de résultat d’une requête de base de données DB2 vers un objet Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b83-219">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span></span> <span data-ttu-id="f3b83-220">Les propriétés JSON utilisées dans l’exemple sont décrites dans les sections suivant les définitions des entités.</span><span class="sxs-lookup"><span data-stu-id="f3b83-220">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span></span>

<span data-ttu-id="f3b83-221">Pour commencer, installez et configurez une passerelle de données.</span><span class="sxs-lookup"><span data-stu-id="f3b83-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="f3b83-222">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="f3b83-222">Instructions are in the [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f3b83-223">**Service lié DB2**</span><span class="sxs-lookup"><span data-stu-id="f3b83-223">**DB2 linked service**</span></span>

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

<span data-ttu-id="f3b83-224">**Service lié Azure Blob Storage**</span><span class="sxs-lookup"><span data-stu-id="f3b83-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="f3b83-225">**Jeu de données d’entrée DB2**</span><span class="sxs-lookup"><span data-stu-id="f3b83-225">**DB2 input dataset**</span></span>

<span data-ttu-id="f3b83-226">L'exemple suppose que vous avez créé une table nommée « MyTable » dans DB2 qui contient une colonne appelée « timestamp » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="f3b83-226">The sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for the time series data.</span></span>

<span data-ttu-id="f3b83-227">La propriété **external** est définie sur « true ».</span><span class="sxs-lookup"><span data-stu-id="f3b83-227">The **external** property is set to "true."</span></span> <span data-ttu-id="f3b83-228">Ce paramètre informe le service Data Factory que ce jeu de données est externe à la fabrique de données et non produit par une activité dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="f3b83-228">This setting informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="f3b83-229">Notez que la propriété **type** est définie sur **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="f3b83-229">Notice that the **type** property is set to **RelationalTable**.</span></span>


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

<span data-ttu-id="f3b83-230">**Jeu de données de sortie Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="f3b83-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="f3b83-231">Les données sont écrites dans un nouvel objet blob toutes les heures en configurant la propriété **frequency** sur « Hour » et la propriété **interval** sur 1.</span><span class="sxs-lookup"><span data-stu-id="f3b83-231">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span></span> <span data-ttu-id="f3b83-232">La propriété **folderPath** de l’objet blob est évaluée dynamiquement en fonction de l’heure de début de la section en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="f3b83-232">The **folderPath** property for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f3b83-233">Le chemin d’accès du dossier utilise l’année, le mois, le jour et l’heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="f3b83-233">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

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

<span data-ttu-id="f3b83-234">**Pipeline pour l'activité de copie**</span><span class="sxs-lookup"><span data-stu-id="f3b83-234">**Pipeline for the copy activity**</span></span>

<span data-ttu-id="f3b83-235">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie spécifiées, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="f3b83-235">The pipeline contains a copy activity that is configured to use specified input and output datasets and which is scheduled to run every hour.</span></span> <span data-ttu-id="f3b83-236">Dans la définition JSON du pipeline, le type **source** est défini sur **RelationalSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f3b83-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="f3b83-237">La requête SQL spécifiée pour la propriété **query** sélectionne les données de la table « Orders ».</span><span class="sxs-lookup"><span data-stu-id="f3b83-237">The SQL query specified for the **query** property selects the data from the "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for the copy activity",
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

## <a name="type-mapping-for-db2"></a><span data-ttu-id="f3b83-238">Mappage de type pour DB2</span><span class="sxs-lookup"><span data-stu-id="f3b83-238">Type mapping for DB2</span></span>
<span data-ttu-id="f3b83-239">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md), l’activité de copie convertit automatiquement un type source en type récepteur à l’aide de l’approche en deux étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="f3b83-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type by using the following two-step approach:</span></span>

1. <span data-ttu-id="f3b83-240">Conversion d’un type natif source en type .NET</span><span class="sxs-lookup"><span data-stu-id="f3b83-240">Convert from a native source type to a .NET type</span></span>
2. <span data-ttu-id="f3b83-241">Conversion d’un type .NET en type récepteur natif</span><span class="sxs-lookup"><span data-stu-id="f3b83-241">Convert from a .NET type to a native sink type</span></span>

<span data-ttu-id="f3b83-242">Les mappages suivants sont utilisés lorsque l’activité de copie convertit les données de type DB2 en type .NET :</span><span class="sxs-lookup"><span data-stu-id="f3b83-242">The following mappings are used when Copy Activity converts the data from a DB2 type to a .NET type:</span></span>

| <span data-ttu-id="f3b83-243">Type de base de données DB2</span><span class="sxs-lookup"><span data-stu-id="f3b83-243">DB2 database type</span></span> | <span data-ttu-id="f3b83-244">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f3b83-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="f3b83-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="f3b83-245">SmallInt</span></span> |<span data-ttu-id="f3b83-246">Int16</span><span class="sxs-lookup"><span data-stu-id="f3b83-246">Int16</span></span> |
| <span data-ttu-id="f3b83-247">Integer</span><span class="sxs-lookup"><span data-stu-id="f3b83-247">Integer</span></span> |<span data-ttu-id="f3b83-248">Int32</span><span class="sxs-lookup"><span data-stu-id="f3b83-248">Int32</span></span> |
| <span data-ttu-id="f3b83-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="f3b83-249">BigInt</span></span> |<span data-ttu-id="f3b83-250">Int64</span><span class="sxs-lookup"><span data-stu-id="f3b83-250">Int64</span></span> |
| <span data-ttu-id="f3b83-251">Real</span><span class="sxs-lookup"><span data-stu-id="f3b83-251">Real</span></span> |<span data-ttu-id="f3b83-252">Single</span><span class="sxs-lookup"><span data-stu-id="f3b83-252">Single</span></span> |
| <span data-ttu-id="f3b83-253">Double</span><span class="sxs-lookup"><span data-stu-id="f3b83-253">Double</span></span> |<span data-ttu-id="f3b83-254">Double</span><span class="sxs-lookup"><span data-stu-id="f3b83-254">Double</span></span> |
| <span data-ttu-id="f3b83-255">Float</span><span class="sxs-lookup"><span data-stu-id="f3b83-255">Float</span></span> |<span data-ttu-id="f3b83-256">Double</span><span class="sxs-lookup"><span data-stu-id="f3b83-256">Double</span></span> |
| <span data-ttu-id="f3b83-257">Décimal</span><span class="sxs-lookup"><span data-stu-id="f3b83-257">Decimal</span></span> |<span data-ttu-id="f3b83-258">Décimal</span><span class="sxs-lookup"><span data-stu-id="f3b83-258">Decimal</span></span> |
| <span data-ttu-id="f3b83-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="f3b83-259">DecimalFloat</span></span> |<span data-ttu-id="f3b83-260">Décimal</span><span class="sxs-lookup"><span data-stu-id="f3b83-260">Decimal</span></span> |
| <span data-ttu-id="f3b83-261">Chiffre</span><span class="sxs-lookup"><span data-stu-id="f3b83-261">Numeric</span></span> |<span data-ttu-id="f3b83-262">Décimal</span><span class="sxs-lookup"><span data-stu-id="f3b83-262">Decimal</span></span> |
| <span data-ttu-id="f3b83-263">Date</span><span class="sxs-lookup"><span data-stu-id="f3b83-263">Date</span></span> |<span data-ttu-id="f3b83-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="f3b83-264">DateTime</span></span> |
| <span data-ttu-id="f3b83-265">Time</span><span class="sxs-lookup"><span data-stu-id="f3b83-265">Time</span></span> |<span data-ttu-id="f3b83-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f3b83-266">TimeSpan</span></span> |
| <span data-ttu-id="f3b83-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="f3b83-267">Timestamp</span></span> |<span data-ttu-id="f3b83-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="f3b83-268">DateTime</span></span> |
| <span data-ttu-id="f3b83-269">xml</span><span class="sxs-lookup"><span data-stu-id="f3b83-269">Xml</span></span> |<span data-ttu-id="f3b83-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3b83-270">Byte[]</span></span> |
| <span data-ttu-id="f3b83-271">Char</span><span class="sxs-lookup"><span data-stu-id="f3b83-271">Char</span></span> |<span data-ttu-id="f3b83-272">String</span><span class="sxs-lookup"><span data-stu-id="f3b83-272">String</span></span> |
| <span data-ttu-id="f3b83-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="f3b83-273">VarChar</span></span> |<span data-ttu-id="f3b83-274">String</span><span class="sxs-lookup"><span data-stu-id="f3b83-274">String</span></span> |
| <span data-ttu-id="f3b83-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="f3b83-275">LongVarChar</span></span> |<span data-ttu-id="f3b83-276">String</span><span class="sxs-lookup"><span data-stu-id="f3b83-276">String</span></span> |
| <span data-ttu-id="f3b83-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="f3b83-277">DB2DynArray</span></span> |<span data-ttu-id="f3b83-278">String</span><span class="sxs-lookup"><span data-stu-id="f3b83-278">String</span></span> |
| <span data-ttu-id="f3b83-279">Fichier binaire</span><span class="sxs-lookup"><span data-stu-id="f3b83-279">Binary</span></span> |<span data-ttu-id="f3b83-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3b83-280">Byte[]</span></span> |
| <span data-ttu-id="f3b83-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="f3b83-281">VarBinary</span></span> |<span data-ttu-id="f3b83-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3b83-282">Byte[]</span></span> |
| <span data-ttu-id="f3b83-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="f3b83-283">LongVarBinary</span></span> |<span data-ttu-id="f3b83-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3b83-284">Byte[]</span></span> |
| <span data-ttu-id="f3b83-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="f3b83-285">Graphic</span></span> |<span data-ttu-id="f3b83-286">String</span><span class="sxs-lookup"><span data-stu-id="f3b83-286">String</span></span> |
| <span data-ttu-id="f3b83-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="f3b83-287">VarGraphic</span></span> |<span data-ttu-id="f3b83-288">String</span><span class="sxs-lookup"><span data-stu-id="f3b83-288">String</span></span> |
| <span data-ttu-id="f3b83-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="f3b83-289">LongVarGraphic</span></span> |<span data-ttu-id="f3b83-290">String</span><span class="sxs-lookup"><span data-stu-id="f3b83-290">String</span></span> |
| <span data-ttu-id="f3b83-291">Clob</span><span class="sxs-lookup"><span data-stu-id="f3b83-291">Clob</span></span> |<span data-ttu-id="f3b83-292">String</span><span class="sxs-lookup"><span data-stu-id="f3b83-292">String</span></span> |
| <span data-ttu-id="f3b83-293">Blob</span><span class="sxs-lookup"><span data-stu-id="f3b83-293">Blob</span></span> |<span data-ttu-id="f3b83-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3b83-294">Byte[]</span></span> |
| <span data-ttu-id="f3b83-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="f3b83-295">DbClob</span></span> |<span data-ttu-id="f3b83-296">String</span><span class="sxs-lookup"><span data-stu-id="f3b83-296">String</span></span> |
| <span data-ttu-id="f3b83-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="f3b83-297">SmallInt</span></span> |<span data-ttu-id="f3b83-298">Int16</span><span class="sxs-lookup"><span data-stu-id="f3b83-298">Int16</span></span> |
| <span data-ttu-id="f3b83-299">Integer</span><span class="sxs-lookup"><span data-stu-id="f3b83-299">Integer</span></span> |<span data-ttu-id="f3b83-300">Int32</span><span class="sxs-lookup"><span data-stu-id="f3b83-300">Int32</span></span> |
| <span data-ttu-id="f3b83-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="f3b83-301">BigInt</span></span> |<span data-ttu-id="f3b83-302">Int64</span><span class="sxs-lookup"><span data-stu-id="f3b83-302">Int64</span></span> |
| <span data-ttu-id="f3b83-303">Real</span><span class="sxs-lookup"><span data-stu-id="f3b83-303">Real</span></span> |<span data-ttu-id="f3b83-304">Single</span><span class="sxs-lookup"><span data-stu-id="f3b83-304">Single</span></span> |
| <span data-ttu-id="f3b83-305">Double</span><span class="sxs-lookup"><span data-stu-id="f3b83-305">Double</span></span> |<span data-ttu-id="f3b83-306">Double</span><span class="sxs-lookup"><span data-stu-id="f3b83-306">Double</span></span> |
| <span data-ttu-id="f3b83-307">Float</span><span class="sxs-lookup"><span data-stu-id="f3b83-307">Float</span></span> |<span data-ttu-id="f3b83-308">Double</span><span class="sxs-lookup"><span data-stu-id="f3b83-308">Double</span></span> |
| <span data-ttu-id="f3b83-309">Décimal</span><span class="sxs-lookup"><span data-stu-id="f3b83-309">Decimal</span></span> |<span data-ttu-id="f3b83-310">Décimal</span><span class="sxs-lookup"><span data-stu-id="f3b83-310">Decimal</span></span> |
| <span data-ttu-id="f3b83-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="f3b83-311">DecimalFloat</span></span> |<span data-ttu-id="f3b83-312">Décimal</span><span class="sxs-lookup"><span data-stu-id="f3b83-312">Decimal</span></span> |
| <span data-ttu-id="f3b83-313">Chiffre</span><span class="sxs-lookup"><span data-stu-id="f3b83-313">Numeric</span></span> |<span data-ttu-id="f3b83-314">Décimal</span><span class="sxs-lookup"><span data-stu-id="f3b83-314">Decimal</span></span> |
| <span data-ttu-id="f3b83-315">Date</span><span class="sxs-lookup"><span data-stu-id="f3b83-315">Date</span></span> |<span data-ttu-id="f3b83-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="f3b83-316">DateTime</span></span> |
| <span data-ttu-id="f3b83-317">Time</span><span class="sxs-lookup"><span data-stu-id="f3b83-317">Time</span></span> |<span data-ttu-id="f3b83-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f3b83-318">TimeSpan</span></span> |
| <span data-ttu-id="f3b83-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="f3b83-319">Timestamp</span></span> |<span data-ttu-id="f3b83-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="f3b83-320">DateTime</span></span> |
| <span data-ttu-id="f3b83-321">xml</span><span class="sxs-lookup"><span data-stu-id="f3b83-321">Xml</span></span> |<span data-ttu-id="f3b83-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3b83-322">Byte[]</span></span> |
| <span data-ttu-id="f3b83-323">Char</span><span class="sxs-lookup"><span data-stu-id="f3b83-323">Char</span></span> |<span data-ttu-id="f3b83-324">String</span><span class="sxs-lookup"><span data-stu-id="f3b83-324">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="f3b83-325">Mapper les colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="f3b83-325">Map source to sink columns</span></span>
<span data-ttu-id="f3b83-326">Pour savoir comment mapper des colonnes du jeu de données source à des colonnes du jeu de données récepteur, consultez [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f3b83-326">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="f3b83-327">Lectures renouvelées de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="f3b83-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="f3b83-328">Lorsque vous copiez des données à partir d’un magasin de données relationnel, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="f3b83-328">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="f3b83-329">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="f3b83-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f3b83-330">Vous pouvez également configurer la propriété de **stratégie** de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="f3b83-330">You can also configure the retry **policy** property for a dataset to rerun a slice when a failure occurs.</span></span> <span data-ttu-id="f3b83-331">Assurez-vous que les mêmes données sont lues, quel que soit le nombre d’exécutions de la tranche et quelle que soit la manière dont vous la réexécutez.</span><span class="sxs-lookup"><span data-stu-id="f3b83-331">Make sure that the same data is read no matter how many times the slice is rerun, and regardless of how you rerun the slice.</span></span> <span data-ttu-id="f3b83-332">Pour plus d’informations, consultez [Lectures renouvelées de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="f3b83-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f3b83-333">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="f3b83-333">Performance and tuning</span></span>
<span data-ttu-id="f3b83-334">Pour en savoir plus sur les facteurs clés affectant les performances de l’activité de copie et les différentes manières de les optimiser, consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="f3b83-334">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>