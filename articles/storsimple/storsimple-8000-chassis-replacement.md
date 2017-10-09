---
title: "châssis aaaReplace sur l’appareil de série StorSimple 8000 | Documents Microsoft"
description: "Décrit comment tooremove et remplacer hello châssis pour votre boîtier principal de StorSimple ou d’un boîtier EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 94bbd3d354a9b8866ece036238927e67ec5ce2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="a1467-103">Remplacez le châssis hello sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="a1467-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="a1467-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a1467-104">Overview</span></span>
<span data-ttu-id="a1467-105">Ce didacticiel explique comment tooremove et remplacer un châssis dans un appareil de série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="a1467-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="a1467-106">modèle de Hello StorSimple 8100 est un appareil à boîtier unique (un seul châssis), tandis que hello 8600 possède un double boîtier (deux châssis).</span><span class="sxs-lookup"><span data-stu-id="a1467-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="a1467-107">Pour un modèle 8600, il existe potentiellement deux châssis qui risque d’échouer dans le dispositif de hello : hello châssis du boîtier principal hello ou châssis hello pour hello boîtiers.</span><span class="sxs-lookup"><span data-stu-id="a1467-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="a1467-108">Dans les deux cas, le châssis de remplacement hello fourni par Microsoft est vide.</span><span class="sxs-lookup"><span data-stu-id="a1467-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="a1467-109">Aucun module d’alimentation et de refroidissement (PCM), module de contrôleur, disque SSD, lecteur de disque dur (HDD) ni module EBOD ne seront inclus.</span><span class="sxs-lookup"><span data-stu-id="a1467-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1467-110">Avant de retrait et le remplacement du châssis hello, passez en revue les informations de sécurité hello dans [remplacement de composant matériel StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="a1467-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-chassis"></a><span data-ttu-id="a1467-111">Retirer hello châssis</span><span class="sxs-lookup"><span data-stu-id="a1467-111">Remove hello chassis</span></span>
<span data-ttu-id="a1467-112">Effectuer hello suivant châssis de hello tooremove étapes sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a1467-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="a1467-113">tooremove un châssis</span><span class="sxs-lookup"><span data-stu-id="a1467-113">tooremove a chassis</span></span>
1. <span data-ttu-id="a1467-114">Assurez-vous que l’appareil StorSimple hello est arrêté et déconnecté de toutes les sources d’alimentation hello.</span><span class="sxs-lookup"><span data-stu-id="a1467-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="a1467-115">Supprimez tous les hello câbles réseau et SAS, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="a1467-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="a1467-116">Sortez hello de rack de hello.</span><span class="sxs-lookup"><span data-stu-id="a1467-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="a1467-117">Supprimer tous les lecteurs hello et notez les emplacements de hello à partir duquel ils sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="a1467-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="a1467-118">Pour plus d’informations, consultez [supprimer le lecteur de disque hello](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="a1467-118">For more information, see [Remove hello disk drive](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="a1467-119">Sur hello boîtier EBOD (s’il s’agit de châssis hello qui a échoué), supprimez les modules de contrôleur EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="a1467-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="a1467-120">Pour plus d’informations, consultez [Retrait d’un contrôleur EBOD](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="a1467-120">For more information, see [Remove an EBOD controller](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span>
   
    <span data-ttu-id="a1467-121">Sur hello boîtier principal (s’il s’agit de châssis hello qui a échoué), supprimez les contrôleurs de hello et notez les emplacements de hello à partir duquel ils sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="a1467-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="a1467-122">Pour plus d’informations, consultez [Retrait d’un contrôleur](storsimple-8000-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="a1467-122">For more information, see [Remove a controller](storsimple-8000-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="a1467-123">Installer hello châssis</span><span class="sxs-lookup"><span data-stu-id="a1467-123">Install hello chassis</span></span>
<span data-ttu-id="a1467-124">Effectuer hello suivant châssis de hello tooinstall étapes sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a1467-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="a1467-125">tooinstall un châssis</span><span class="sxs-lookup"><span data-stu-id="a1467-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="a1467-126">Montez le châssis hello dans un rack de hello.</span><span class="sxs-lookup"><span data-stu-id="a1467-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="a1467-127">Pour en savoir plus, consultez la rubrique [Montage en rack de votre appareil StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) ou [Montage en rack de votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="a1467-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="a1467-128">Une fois le châssis de hello est monté en rack de hello, installez les modules de contrôleur de hello Bonjour dans que même positionne qu’elles ont été précédemment installées.</span><span class="sxs-lookup"><span data-stu-id="a1467-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="a1467-129">Installation hello lecteurs Bonjour positions et emplacements qu’elles ont été précédemment installées dans.</span><span class="sxs-lookup"><span data-stu-id="a1467-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1467-130">Nous vous recommandons de disques SSD de hello dans les emplacements de hello d’abord installer puis installez hello HDD.</span><span class="sxs-lookup"><span data-stu-id="a1467-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
  
4. <span data-ttu-id="a1467-131">Avec hello appareil monté en rack de hello et hello components, connecter vos sources d’alimentation appropriées toohello appareil et activer sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="a1467-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="a1467-132">Pour en savoir plus, consultez la rubrique [Branchement des câbles de votre appareil StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [Branchement des câbles de votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="a1467-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1467-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1467-133">Next steps</span></span>
<span data-ttu-id="a1467-134">En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="a1467-134">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

