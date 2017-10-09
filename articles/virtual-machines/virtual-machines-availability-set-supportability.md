---
title: "aaaSupportability d’ajout de machines virtuelles Azure tooan à haute disponibilité existant | Documents Microsoft"
description: "Prise en charge de l’ajout de machines virtuelles Azure tooan à haute disponibilité existant."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="1622d-103">Prise en charge de l’ajout de machines virtuelles Azure tooan à haute disponibilité existant</span><span class="sxs-lookup"><span data-stu-id="1622d-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="1622d-104">Vous pouvez parfois rencontrer des limitations lorsque vous ajoutez de nouvelles machines virtuelles (VM) tooan à haute disponibilité existant.</span><span class="sxs-lookup"><span data-stu-id="1622d-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="1622d-105">Hello suivant détaille graphique les séries de machines virtuelles que vous pouvez combiner dans hello même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="1622d-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="1622d-106">Voici hello prise en charge matrice toomix différents types d’ordinateurs virtuels :</span><span class="sxs-lookup"><span data-stu-id="1622d-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="1622d-107">Série et groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="1622d-107">Series & Availability Set</span></span>|<span data-ttu-id="1622d-108">Deuxième machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1622d-108">Second VM</span></span>|<span data-ttu-id="1622d-109">A</span><span class="sxs-lookup"><span data-stu-id="1622d-109">A</span></span>|<span data-ttu-id="1622d-110">Av2</span><span class="sxs-lookup"><span data-stu-id="1622d-110">Av2</span></span>|<span data-ttu-id="1622d-111">D</span><span class="sxs-lookup"><span data-stu-id="1622d-111">D</span></span>|<span data-ttu-id="1622d-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="1622d-112">Dv2</span></span>|<span data-ttu-id="1622d-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="1622d-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="1622d-114">Première machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1622d-114">First VM</span></span>|||||||
|<span data-ttu-id="1622d-115">A</span><span class="sxs-lookup"><span data-stu-id="1622d-115">A</span></span>||<span data-ttu-id="1622d-116">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-116">OK</span></span>|<span data-ttu-id="1622d-117">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-117">OK</span></span>|<span data-ttu-id="1622d-118">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-118">OK</span></span>|<span data-ttu-id="1622d-119">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-119">OK</span></span>|<span data-ttu-id="1622d-120">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-120">OK</span></span>|
|<span data-ttu-id="1622d-121">Av2</span><span class="sxs-lookup"><span data-stu-id="1622d-121">Av2</span></span>||<span data-ttu-id="1622d-122">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-122">OK</span></span>|<span data-ttu-id="1622d-123">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-123">OK</span></span>|<span data-ttu-id="1622d-124">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-124">OK</span></span>|<span data-ttu-id="1622d-125">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-125">OK</span></span>|<span data-ttu-id="1622d-126">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-126">OK</span></span>|
|<span data-ttu-id="1622d-127">D</span><span class="sxs-lookup"><span data-stu-id="1622d-127">D</span></span>||<span data-ttu-id="1622d-128">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-128">OK</span></span>|<span data-ttu-id="1622d-129">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-129">OK</span></span>|<span data-ttu-id="1622d-130">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-130">OK</span></span>|<span data-ttu-id="1622d-131">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-131">OK</span></span>|<span data-ttu-id="1622d-132">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-132">OK</span></span>|
|<span data-ttu-id="1622d-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="1622d-133">Dv2</span></span>||<span data-ttu-id="1622d-134">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-134">OK</span></span>|<span data-ttu-id="1622d-135">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-135">OK</span></span>|<span data-ttu-id="1622d-136">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-136">OK</span></span>|<span data-ttu-id="1622d-137">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-137">OK</span></span>|<span data-ttu-id="1622d-138">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-138">OK</span></span>|
|<span data-ttu-id="1622d-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="1622d-139">Dv3</span></span>||<span data-ttu-id="1622d-140">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-140">OK</span></span>|<span data-ttu-id="1622d-141">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-141">OK</span></span>|<span data-ttu-id="1622d-142">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-142">OK</span></span>|<span data-ttu-id="1622d-143">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-143">OK</span></span>|<span data-ttu-id="1622d-144">OK</span><span class="sxs-lookup"><span data-stu-id="1622d-144">OK</span></span>|

<span data-ttu-id="1622d-145">Toutes les autres séries n’a pas pu être Bonjour groupe à haute disponibilité de même, car elles nécessitent un matériel spécifique.</span><span class="sxs-lookup"><span data-stu-id="1622d-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
