---
title: Que faire si une interruption de service Azure affecte Azure Key Vault | Microsoft Docs
description: "Découvrez que faire si une interruption de service Azure affecte Azure Key Vault."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 6419d54c54e7d19103419262b79e7a5268b2268c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="3f3e4-103">Disponibilité et redondance d’Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3f3e4-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="3f3e4-104">Azure Key Vault dispose de plusieurs couches de redondance pour garantir que vos clés et secrets restent disponibles pour votre application même en cas d’échec de composants individuels du service.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span></span>

<span data-ttu-id="3f3e4-105">Le contenu de votre Key Vault est répliqué dans la région ainsi que dans une région secondaire éloignée d’au moins 241 kilomètres, mais située au sein de la même zone géographique.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span></span> <span data-ttu-id="3f3e4-106">Cela maintient une durabilité élevée de vos clés et secrets.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="3f3e4-107">Consultez le document [Régions jumelées d’Azure](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) pour plus d’informations sur les paires de régions spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="3f3e4-108">En cas d’échec de composants du service Key Vault, d’autres composants de la même région interviennent pour traiter votre demande afin de garantir l’intégrité des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span></span> <span data-ttu-id="3f3e4-109">Il est inutile d’intervenir pour déclencher cette action.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-109">You do not need to take any action to trigger this.</span></span> <span data-ttu-id="3f3e4-110">Cela se produit automatiquement, sans que vous le perceviez.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-110">It happens automatically and will be transparent to you.</span></span>

<span data-ttu-id="3f3e4-111">Dans les rares cas d’indisponibilité d’une région Azure entière, les demandes d’Azure Key Vault effectuées dans cette région sont automatiquement acheminées (*basculées*) vers une région secondaire.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span></span> <span data-ttu-id="3f3e4-112">Lorsque la région principale est de nouveau disponible, les demandes sont réacheminées (*basculées*) vers la région principale.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span></span> <span data-ttu-id="3f3e4-113">Vous n’avez pas besoin d’agir dans la mesure où tout se passe automatiquement.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-113">Again, you do not need to take any action because this happens automatically.</span></span>

<span data-ttu-id="3f3e4-114">Il convient toutefois de prendre quelques précautions :</span><span class="sxs-lookup"><span data-stu-id="3f3e4-114">There are a few caveats to be aware of:</span></span>

* <span data-ttu-id="3f3e4-115">En cas de basculement vers une autre région, quelques minutes peuvent être nécessaires pour que le service soit de nouveau opérationnel.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span></span> <span data-ttu-id="3f3e4-116">Il se peut que les demandes effectuées pendant cette période échouent jusqu’à ce que le basculement soit terminé.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-116">Requests that are made during this time may fail until the failover completes.</span></span>
* <span data-ttu-id="3f3e4-117">Après basculement, votre Key Vault est en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="3f3e4-118">Les demandes prises en charge dans ce mode sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3f3e4-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="3f3e4-119">List key vaults (Afficher la liste des Key Vaults)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-119">List key vaults</span></span>
  * <span data-ttu-id="3f3e4-120">Get properties of key vaults (Obtenir les propriétés des Key Vaults)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="3f3e4-121">List secrets (Afficher la liste des secrets)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-121">List secrets</span></span>
  * <span data-ttu-id="3f3e4-122">Get secrets (Obtenir les secrets)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-122">Get secrets</span></span>
  * <span data-ttu-id="3f3e4-123">List keys (Afficher la liste des clés)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-123">List keys</span></span>
  * <span data-ttu-id="3f3e4-124">Get (properties of) keys (Obtenir les propriétés des clés)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="3f3e4-125">Encrypt (Chiffrer)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-125">Encrypt</span></span>
  * <span data-ttu-id="3f3e4-126">Decrypt (Déchiffrer)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-126">Decrypt</span></span>
  * <span data-ttu-id="3f3e4-127">Wrap (Encapsuler)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-127">Wrap</span></span>
  * <span data-ttu-id="3f3e4-128">Unwrap (Désencapsuler)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-128">Unwrap</span></span>
  * <span data-ttu-id="3f3e4-129">Verify (Vérifier)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-129">Verify</span></span>
  * <span data-ttu-id="3f3e4-130">Sign (Signer)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-130">Sign</span></span>
  * <span data-ttu-id="3f3e4-131">Backup (Sauvegarder)</span><span class="sxs-lookup"><span data-stu-id="3f3e4-131">Backup</span></span>
* <span data-ttu-id="3f3e4-132">Une fois le basculement restauré, tous les types de demandes (y compris de lecture -read- *et* d’écriture write-) sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="3f3e4-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

