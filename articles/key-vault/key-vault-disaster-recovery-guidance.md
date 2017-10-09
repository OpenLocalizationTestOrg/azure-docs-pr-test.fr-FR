---
title: "toodo aaaWhat dans les cas de hello d’une interruption de service Azure qui affecte le coffre de clés Azure | Documents Microsoft"
description: "Découvrez quels toodo dans les cas de hello d’une interruption de service Azure qui affecte le coffre de clés Azure."
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
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="f5b3b-103">Disponibilité et redondance d’Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f5b3b-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="f5b3b-104">Coffre de clés Azure propose plusieurs couches de toomake redondance sûr que vos clés et les clés secrètes restent disponibles tooyour application hello des composants de service échouent.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-104">Azure Key Vault features multiple layers of redundancy toomake sure that your keys and secrets remain available tooyour application even if individual components of hello service fail.</span></span>

<span data-ttu-id="f5b3b-105">Hello contenu de votre coffre de clés est répliquées dans la région de hello et la région secondaire tooa au moins 150 miles immédiatement, mais dans hello même geography.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-105">hello contents of your key vault are replicated within hello region and tooa secondary region at least 150 miles away but within hello same geography.</span></span> <span data-ttu-id="f5b3b-106">Cela maintient une durabilité élevée de vos clés et secrets.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="f5b3b-107">Consultez hello [Azure associés régions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document pour plus d’informations sur les paires de région spécifique.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-107">See hello [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="f5b3b-108">Si des composants individuels dans le service de coffre de clés hello échouent, des composants de substitution dans une région de hello étape tooserve votre toomake demande qu’il n’existe aucune dégradation des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-108">If individual components within hello key vault service fail, alternate components within hello region step in tooserve your request toomake sure that there is no degradation of functionality.</span></span> <span data-ttu-id="f5b3b-109">Vous n’avez pas besoin tootake tout tootrigger action cela.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-109">You do not need tootake any action tootrigger this.</span></span> <span data-ttu-id="f5b3b-110">Il se produit automatiquement et sera tooyou transparent.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-110">It happens automatically and will be transparent tooyou.</span></span>

<span data-ttu-id="f5b3b-111">Dans l’événement rare de hello qu’un ensemble de la région Azure n’est pas disponible, hello que vous apportez d’Azure Key Vault dans cette région sont automatiquement routées (*basculé*) tooa la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-111">In hello rare event that an entire Azure region is unavailable, hello requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) tooa secondary region.</span></span> <span data-ttu-id="f5b3b-112">Lors de la région principale de hello est à nouveau disponible, les demandes sont routées précédent (*échec précédent*) toohello la région principale.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-112">When hello primary region is available again, requests are routed back (*failed back*) toohello primary region.</span></span> <span data-ttu-id="f5b3b-113">Là encore, il est inutile tootake n’importe quelle action, car cela se produit automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-113">Again, you do not need tootake any action because this happens automatically.</span></span>

<span data-ttu-id="f5b3b-114">Il existe quelques avertissements toobe prenant en charge de :</span><span class="sxs-lookup"><span data-stu-id="f5b3b-114">There are a few caveats toobe aware of:</span></span>

* <span data-ttu-id="f5b3b-115">Dans l’événement hello d’un basculement de la région, il peut prendre quelques minutes pour hello service toofail.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-115">In hello event of a region failover, it may take a few minutes for hello service toofail over.</span></span> <span data-ttu-id="f5b3b-116">Les demandes qui sont effectuées pendant ce temps risque d’échouer jusqu'à ce que le basculement de hello est terminé.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-116">Requests that are made during this time may fail until hello failover completes.</span></span>
* <span data-ttu-id="f5b3b-117">Après basculement, votre Key Vault est en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="f5b3b-118">Les demandes prises en charge dans ce mode sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5b3b-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="f5b3b-119">List key vaults (Afficher la liste des Key Vaults)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-119">List key vaults</span></span>
  * <span data-ttu-id="f5b3b-120">Get properties of key vaults (Obtenir les propriétés des Key Vaults)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="f5b3b-121">List secrets (Afficher la liste des secrets)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-121">List secrets</span></span>
  * <span data-ttu-id="f5b3b-122">Get secrets (Obtenir les secrets)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-122">Get secrets</span></span>
  * <span data-ttu-id="f5b3b-123">List keys (Afficher la liste des clés)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-123">List keys</span></span>
  * <span data-ttu-id="f5b3b-124">Get (properties of) keys (Obtenir les propriétés des clés)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="f5b3b-125">Encrypt (Chiffrer)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-125">Encrypt</span></span>
  * <span data-ttu-id="f5b3b-126">Decrypt (Déchiffrer)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-126">Decrypt</span></span>
  * <span data-ttu-id="f5b3b-127">Wrap (Encapsuler)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-127">Wrap</span></span>
  * <span data-ttu-id="f5b3b-128">Unwrap (Désencapsuler)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-128">Unwrap</span></span>
  * <span data-ttu-id="f5b3b-129">Verify (Vérifier)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-129">Verify</span></span>
  * <span data-ttu-id="f5b3b-130">Sign (Signer)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-130">Sign</span></span>
  * <span data-ttu-id="f5b3b-131">Backup (Sauvegarder)</span><span class="sxs-lookup"><span data-stu-id="f5b3b-131">Backup</span></span>
* <span data-ttu-id="f5b3b-132">Une fois le basculement restauré, tous les types de demandes (y compris de lecture -read- *et* d’écriture write-) sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="f5b3b-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

