---
title: "Possibilité de prise en charge de l’ajout de machines virtuelles Azure à un groupe à haute disponibilité | Microsoft Docs"
description: "Possibilité de prise en charge de l’ajout de machines virtuelles Azure à un groupe à haute disponibilité."
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
ms.openlocfilehash: 3ce9b8a79108cb9e57df14bcb3354cc637193233
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="supportability-of-adding-azure-vms-to-an-existing-availability-set"></a><span data-ttu-id="8782c-103">Possibilité de prise en charge de l’ajout de machines virtuelles Azure à un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="8782c-103">Supportability of adding Azure VMs to an existing availability set</span></span>

<span data-ttu-id="8782c-104">Vous pouvez parfois rencontrer des limitations lorsque vous ajoutez des machines virtuelles à un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8782c-104">You may occasionally encounter limitations when you add new virtual machines (VMs) to an existing availability set.</span></span> <span data-ttu-id="8782c-105">Le tableau suivant détaille les séries de machines virtuelles que vous pouvez combiner dans le même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8782c-105">The following chart details which VM series you can mix in the same availability set.</span></span>

<span data-ttu-id="8782c-106">Voici la matrice de possibilité de prise en charge pour combiner différents types de machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="8782c-106">Here is the supportability matrix to mix different types of VMs:</span></span>

<span data-ttu-id="8782c-107">Série et groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="8782c-107">Series & Availability Set</span></span>|<span data-ttu-id="8782c-108">Deuxième machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8782c-108">Second VM</span></span>|<span data-ttu-id="8782c-109">A</span><span class="sxs-lookup"><span data-stu-id="8782c-109">A</span></span>|<span data-ttu-id="8782c-110">Av2</span><span class="sxs-lookup"><span data-stu-id="8782c-110">Av2</span></span>|<span data-ttu-id="8782c-111">D</span><span class="sxs-lookup"><span data-stu-id="8782c-111">D</span></span>|<span data-ttu-id="8782c-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="8782c-112">Dv2</span></span>|<span data-ttu-id="8782c-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="8782c-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="8782c-114">Première machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8782c-114">First VM</span></span>|||||||
|<span data-ttu-id="8782c-115">A</span><span class="sxs-lookup"><span data-stu-id="8782c-115">A</span></span>||<span data-ttu-id="8782c-116">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-116">OK</span></span>|<span data-ttu-id="8782c-117">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-117">OK</span></span>|<span data-ttu-id="8782c-118">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-118">OK</span></span>|<span data-ttu-id="8782c-119">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-119">OK</span></span>|<span data-ttu-id="8782c-120">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-120">OK</span></span>|
|<span data-ttu-id="8782c-121">Av2</span><span class="sxs-lookup"><span data-stu-id="8782c-121">Av2</span></span>||<span data-ttu-id="8782c-122">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-122">OK</span></span>|<span data-ttu-id="8782c-123">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-123">OK</span></span>|<span data-ttu-id="8782c-124">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-124">OK</span></span>|<span data-ttu-id="8782c-125">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-125">OK</span></span>|<span data-ttu-id="8782c-126">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-126">OK</span></span>|
|<span data-ttu-id="8782c-127">D</span><span class="sxs-lookup"><span data-stu-id="8782c-127">D</span></span>||<span data-ttu-id="8782c-128">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-128">OK</span></span>|<span data-ttu-id="8782c-129">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-129">OK</span></span>|<span data-ttu-id="8782c-130">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-130">OK</span></span>|<span data-ttu-id="8782c-131">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-131">OK</span></span>|<span data-ttu-id="8782c-132">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-132">OK</span></span>|
|<span data-ttu-id="8782c-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="8782c-133">Dv2</span></span>||<span data-ttu-id="8782c-134">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-134">OK</span></span>|<span data-ttu-id="8782c-135">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-135">OK</span></span>|<span data-ttu-id="8782c-136">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-136">OK</span></span>|<span data-ttu-id="8782c-137">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-137">OK</span></span>|<span data-ttu-id="8782c-138">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-138">OK</span></span>|
|<span data-ttu-id="8782c-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="8782c-139">Dv3</span></span>||<span data-ttu-id="8782c-140">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-140">OK</span></span>|<span data-ttu-id="8782c-141">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-141">OK</span></span>|<span data-ttu-id="8782c-142">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-142">OK</span></span>|<span data-ttu-id="8782c-143">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-143">OK</span></span>|<span data-ttu-id="8782c-144">OK</span><span class="sxs-lookup"><span data-stu-id="8782c-144">OK</span></span>|

<span data-ttu-id="8782c-145">Les autres séries ne pourraient pas être dans le même groupe à haute disponibilité, car elles nécessitent un matériel spécifique.</span><span class="sxs-lookup"><span data-stu-id="8782c-145">All other series could not be in the same availability set because they require a specific hardware.</span></span>