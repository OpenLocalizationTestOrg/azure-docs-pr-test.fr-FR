---
title: "Stockage Azure Stack : différences et points à prendre en compte"
description: "Découvrez les différences entre le stockage Azure Stack et le stockage Azure, ainsi que les points à prendre en compte quand vous déployez Azure Stack."
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: 381950321ac3a5ea8a43b76f3fba868da4be4682
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="azure-stack-storage-differences-and-considerations"></a><span data-ttu-id="8a701-103">Stockage Azure Stack : différences et points à prendre en compte</span><span class="sxs-lookup"><span data-stu-id="8a701-103">Azure Stack Storage: Differences and considerations</span></span>

<span data-ttu-id="8a701-104">*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="8a701-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="8a701-105">Le stockage Azure Stack est l’ensemble des services cloud de stockage fournis dans Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8a701-105">Azure Stack Storage is the set of storage cloud services in Microsoft Azure Stack.</span></span> <span data-ttu-id="8a701-106">Le stockage Azure Stack fournit des fonctionnalités de gestion des objets blob, des tables, des files d’attente et des comptes avec une sémantique Azure cohérente.</span><span class="sxs-lookup"><span data-stu-id="8a701-106">Azure Stack Storage provides blob, table, queue, and account management functionality with Azure-consistent semantics.</span></span>

<span data-ttu-id="8a701-107">Cet article récapitule les différences connues entre le stockage Azure Stack et le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8a701-107">This article summarizes the known Azure Stack Storage differences from Azure Storage.</span></span> <span data-ttu-id="8a701-108">Il expose également les principaux points à prendre en compte quand vous déployez Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8a701-108">It also summarizes other considerations to keep in mind when you deploy Azure Stack.</span></span> <span data-ttu-id="8a701-109">Pour connaître les différences majeures entre Azure Stack et Azure, consultez la rubrique [Principales considérations](azure-stack-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="8a701-109">To learn about high-level differences between Azure Stack and Azure, see the [Key considerations](azure-stack-considerations.md) topic.</span></span>

## <a name="cheat-sheet-storage-differences"></a><span data-ttu-id="8a701-110">Aide-mémoire : différences entre les stockages</span><span class="sxs-lookup"><span data-stu-id="8a701-110">Cheat sheet: Storage differences</span></span>

| <span data-ttu-id="8a701-111">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="8a701-111">Feature</span></span> | <span data-ttu-id="8a701-112">Azure (global)</span><span class="sxs-lookup"><span data-stu-id="8a701-112">Azure (global)</span></span> | <span data-ttu-id="8a701-113">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8a701-113">Azure Stack</span></span> |
| --- | --- | --- |
|<span data-ttu-id="8a701-114">Stockage Fichier</span><span class="sxs-lookup"><span data-stu-id="8a701-114">File storage</span></span>|<span data-ttu-id="8a701-115">Partages de fichiers SMB sur le cloud pris en charge</span><span class="sxs-lookup"><span data-stu-id="8a701-115">Cloud-based SMB file shares supported</span></span>|<span data-ttu-id="8a701-116">Pas encore pris en charge</span><span class="sxs-lookup"><span data-stu-id="8a701-116">Not yet supported</span></span>
|<span data-ttu-id="8a701-117">Chiffrement des données au repos</span><span class="sxs-lookup"><span data-stu-id="8a701-117">Data at rest encryption</span></span>|<span data-ttu-id="8a701-118">Chiffrement AES 256 bits</span><span class="sxs-lookup"><span data-stu-id="8a701-118">256-bit AES encryption</span></span>|<span data-ttu-id="8a701-119">Pas encore pris en charge</span><span class="sxs-lookup"><span data-stu-id="8a701-119">Not yet supported</span></span>
|<span data-ttu-id="8a701-120">Type de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="8a701-120">Storage account type</span></span>|<span data-ttu-id="8a701-121">Comptes de stockage à usage général et comptes de stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="8a701-121">General-purpose and Azure Blob storage accounts</span></span>|<span data-ttu-id="8a701-122">À usage général uniquement</span><span class="sxs-lookup"><span data-stu-id="8a701-122">General-purpose only</span></span>
|<span data-ttu-id="8a701-123">Options de réplication</span><span class="sxs-lookup"><span data-stu-id="8a701-123">Replication options</span></span>|<span data-ttu-id="8a701-124">Stockage localement redondant, stockage géoredondant, stockage géoredondant avec accès en lecture et stockage redondant dans une zone</span><span class="sxs-lookup"><span data-stu-id="8a701-124">Locally redundant storage, geo-redundant storage, read-access geo-redundant storage, and zone-redundant storage</span></span>|<span data-ttu-id="8a701-125">Stockage localement redondant</span><span class="sxs-lookup"><span data-stu-id="8a701-125">Locally redundant storage</span></span>
|<span data-ttu-id="8a701-126">Stockage Premium</span><span class="sxs-lookup"><span data-stu-id="8a701-126">Premium storage</span></span>|<span data-ttu-id="8a701-127">Entièrement pris en charge</span><span class="sxs-lookup"><span data-stu-id="8a701-127">Fully supported</span></span>|<span data-ttu-id="8a701-128">Peut être approvisionné, mais sans limite ni garantie de performances</span><span class="sxs-lookup"><span data-stu-id="8a701-128">Can be provisioned, but no performance limit or guarantee</span></span>
|<span data-ttu-id="8a701-129">Disques gérés</span><span class="sxs-lookup"><span data-stu-id="8a701-129">Managed disks</span></span>|<span data-ttu-id="8a701-130">Premium et standard pris en charge</span><span class="sxs-lookup"><span data-stu-id="8a701-130">Premium and standard supported</span></span>|<span data-ttu-id="8a701-131">Pas encore pris en charge</span><span class="sxs-lookup"><span data-stu-id="8a701-131">Not yet supported</span></span>
|<span data-ttu-id="8a701-132">Nom de l’objet blob</span><span class="sxs-lookup"><span data-stu-id="8a701-132">Blob name</span></span>|<span data-ttu-id="8a701-133">1 024 caractères (2 048 octets)</span><span class="sxs-lookup"><span data-stu-id="8a701-133">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="8a701-134">880 caractères (1 760 octets)</span><span class="sxs-lookup"><span data-stu-id="8a701-134">880 characters (1,760 bytes)</span></span>
|<span data-ttu-id="8a701-135">Taille maximale d’un objet blob de blocs</span><span class="sxs-lookup"><span data-stu-id="8a701-135">Block blob max size</span></span>|<span data-ttu-id="8a701-136">4,75 To (100 Mo X 50 000 blocs)</span><span class="sxs-lookup"><span data-stu-id="8a701-136">4.75 TB (100 MB X 50,000 blocks)</span></span>|<span data-ttu-id="8a701-137">50 000 X 4 Mo (195 Go environ)</span><span class="sxs-lookup"><span data-stu-id="8a701-137">50,000 X 4 MB (approx. 195 GB)</span></span>
|<span data-ttu-id="8a701-138">Copie d’instantané incrémentiel d’objet blob de pages</span><span class="sxs-lookup"><span data-stu-id="8a701-138">Page blob incremental snapshot copy</span></span>|<span data-ttu-id="8a701-139">Objets blob de pages Azure Premium et standard pris en charge</span><span class="sxs-lookup"><span data-stu-id="8a701-139">Premium and standard Azure page blobs supported</span></span>|<span data-ttu-id="8a701-140">Pas encore pris en charge</span><span class="sxs-lookup"><span data-stu-id="8a701-140">Not yet supported</span></span>
|<span data-ttu-id="8a701-141">Taille maximale d’un objet blob de pages</span><span class="sxs-lookup"><span data-stu-id="8a701-141">Page blob max size</span></span>|<span data-ttu-id="8a701-142">8 To</span><span class="sxs-lookup"><span data-stu-id="8a701-142">8 TB</span></span>|<span data-ttu-id="8a701-143">1 To</span><span class="sxs-lookup"><span data-stu-id="8a701-143">1 TB</span></span>
|<span data-ttu-id="8a701-144">Taille de page d’un objet blob de pages</span><span class="sxs-lookup"><span data-stu-id="8a701-144">Page blob page size</span></span>|<span data-ttu-id="8a701-145">512 octets</span><span class="sxs-lookup"><span data-stu-id="8a701-145">512 bytes</span></span>|<span data-ttu-id="8a701-146">4 Ko</span><span class="sxs-lookup"><span data-stu-id="8a701-146">4 KB</span></span>
|<span data-ttu-id="8a701-147">Taille de la clé de ligne et de la clé de partition de table</span><span class="sxs-lookup"><span data-stu-id="8a701-147">Table partition key and row key size</span></span>|<span data-ttu-id="8a701-148">1 024 caractères (2 048 octets)</span><span class="sxs-lookup"><span data-stu-id="8a701-148">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="8a701-149">400 caractères (800 octets)</span><span class="sxs-lookup"><span data-stu-id="8a701-149">400 characters (800 bytes)</span></span>

### <a name="metrics"></a><span data-ttu-id="8a701-150">Mesures</span><span class="sxs-lookup"><span data-stu-id="8a701-150">Metrics</span></span>
<span data-ttu-id="8a701-151">Il existe également des différences sur le plan des métriques de stockage :</span><span class="sxs-lookup"><span data-stu-id="8a701-151">There are also some differences with storage metrics:</span></span>
* <span data-ttu-id="8a701-152">Les données de transaction dans les métriques de stockage ne font pas la distinction entre la bande passante réseau interne et externe.</span><span class="sxs-lookup"><span data-stu-id="8a701-152">The transaction data in storage metrics does not differentiate internal or external network bandwidth.</span></span>
* <span data-ttu-id="8a701-153">Les données de transaction dans les métriques de stockage ne prennent pas en compte l’accès des machines virtuelles aux disques montés.</span><span class="sxs-lookup"><span data-stu-id="8a701-153">The transaction data in storage metrics does not include virtual machine access to the mounted disks.</span></span>

## <a name="api-version"></a><span data-ttu-id="8a701-154">Version de l'API</span><span class="sxs-lookup"><span data-stu-id="8a701-154">API version</span></span>
<span data-ttu-id="8a701-155">Les versions suivantes sont prises en charge avec le stockage Azure Stack :</span><span class="sxs-lookup"><span data-stu-id="8a701-155">The following versions are supported with Azure Stack Storage:</span></span>

* <span data-ttu-id="8a701-156">Services de données du stockage Azure : [version du 05-04-2015 de l’API REST](https://docs.microsoft.com/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="8a701-156">Azure Storage data services: [2015-04-05 REST API version](https://docs.microsoft.com/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span></span>
* <span data-ttu-id="8a701-157">Services de gestion du stockage Azure : [préversion du 01-05-2015, version du 15-06-2015 et version du 01-01-2016](https://docs.microsoft.com/rest/api/storagerp/?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="8a701-157">Azure Storage management services: [2015-05-01-preview, 2015-06-15, and 2016-01-01](https://docs.microsoft.com/rest/api/storagerp/?redirectedfrom=MSDN)</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8a701-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8a701-158">Next steps</span></span>

* [<span data-ttu-id="8a701-159">Bien démarrer avec les outils de développement du stockage Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8a701-159">Get started with Azure Stack Storage development tools</span></span>](azure-stack-storage-dev.md)
* [<span data-ttu-id="8a701-160">Présentation du stockage Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8a701-160">Introduction to Azure Stack Storage</span></span>](azure-stack-storage-overview.md)

