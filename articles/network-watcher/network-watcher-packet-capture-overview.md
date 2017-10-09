---
title: "capture de tooPacket aaaIntroduction dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de la fonctionnalité de capture de paquets hello Observateur réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="46af6-103">Introduction toovariable capture des paquets dans l’Observateur réseau de Azure</span><span class="sxs-lookup"><span data-stu-id="46af6-103">Introduction toovariable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="46af6-104">Capture de paquet variable de l’Observateur réseau vous permet de toocreate paquet capture sessions tootrack trafic tooand à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="46af6-104">Network Watcher variable packet capture allows you toocreate packet capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="46af6-105">Capture des paquets permet les anomalies de réseau toodiagnose réactive et proactivity.</span><span class="sxs-lookup"><span data-stu-id="46af6-105">Packet capture helps toodiagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="46af6-106">Autres utilisations incluent la collecte des statistiques de réseau, obtenir des informations sur les intrusions, toodebug client-serveur de communications et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="46af6-106">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span>

<span data-ttu-id="46af6-107">La capture de paquets est une extension de machine virtuelle qui est démarrée à distance par le biais de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="46af6-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="46af6-108">Cette fonctionnalité facilite la charge hello de l’exécution d’une capture de paquets manuellement sur l’ordinateur virtuel hello souhaité, ce qui permet de gagner du temps.</span><span class="sxs-lookup"><span data-stu-id="46af6-108">This capability eases hello burden of running a packet capture manually on hello desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="46af6-109">Capture de paquets peut être déclenchée via le portail de hello, PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="46af6-109">Packet capture can be triggered through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="46af6-110">Les alertes de machine virtuelle constituent un exemple de mode de déclenchement de la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="46af6-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="46af6-111">Les filtres sont fournies pour tooensure de session de capture hello vous capturez le trafic que vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="46af6-111">Filters are provided for hello capture session tooensure you capture traffic you want toomonitor.</span></span> <span data-ttu-id="46af6-112">Ces filtres reposent sur des informations à 5 tuples (protocole, adresse IP locale, adresse IP distante, port local et port distant).</span><span class="sxs-lookup"><span data-stu-id="46af6-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="46af6-113">les données de Hello capturée sont stockées dans le disque local de hello ou un objet blob de stockage.</span><span class="sxs-lookup"><span data-stu-id="46af6-113">hello captured data is stored in hello local disk or a storage blob.</span></span> <span data-ttu-id="46af6-114">Il existe une limite de 10 sessions de capture de paquets par région par abonnement.</span><span class="sxs-lookup"><span data-stu-id="46af6-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="46af6-115">Cette limite s’applique uniquement les sessions toohello et ne s’applique pas toohello enregistré les fichiers de capture de paquet localement sur hello machine virtuelle ou dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="46af6-115">This limit applies only toohello sessions and does not apply toohello saved packet capture files either locally on hello VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46af6-116">La capture de paquets requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="46af6-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="46af6-117">Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="46af6-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="46af6-118">informations de hello tooreduce vous capturez des informations de hello tooonly souhaité, hello options suivantes sont disponibles pour une session de capture de paquet :</span><span class="sxs-lookup"><span data-stu-id="46af6-118">tooreduce hello information you capture tooonly hello information you want, hello following options are available for a packet capture session:</span></span>

<span data-ttu-id="46af6-119">**Configuration de la capture**</span><span class="sxs-lookup"><span data-stu-id="46af6-119">**Capture configuration**</span></span>

|<span data-ttu-id="46af6-120">Propriété</span><span class="sxs-lookup"><span data-stu-id="46af6-120">Property</span></span>|<span data-ttu-id="46af6-121">Description</span><span class="sxs-lookup"><span data-stu-id="46af6-121">Description</span></span>|
|---|---|
|<span data-ttu-id="46af6-122">**Nombre maximal d’octets par paquet (octets)**</span><span class="sxs-lookup"><span data-stu-id="46af6-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="46af6-123">Hello du nombre d’octets à partir de chaque paquet sont capturées, tous les octets sont capturées, si ce champ est vide.</span><span class="sxs-lookup"><span data-stu-id="46af6-123">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="46af6-124">Hello du nombre d’octets à partir de chaque paquet sont capturées, tous les octets sont capturées, si ce champ est vide.</span><span class="sxs-lookup"><span data-stu-id="46af6-124">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="46af6-125">Si vous avez besoin d’en-tête IPv4 uniquement hello indiquer 34 ici</span><span class="sxs-lookup"><span data-stu-id="46af6-125">If you need only hello IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="46af6-126">**Nombre maximal d’octets par session (octets)**</span><span class="sxs-lookup"><span data-stu-id="46af6-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="46af6-127">Nombre total d’octets qui est capturée, une fois la valeur de hello atteinte hello session se termine.</span><span class="sxs-lookup"><span data-stu-id="46af6-127">Total number of bytes in that are captured, once hello value is reached hello session ends.</span></span>|
|<span data-ttu-id="46af6-128">**Délai imparti (secondes)**</span><span class="sxs-lookup"><span data-stu-id="46af6-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="46af6-129">Définit une contrainte de temps sur les paquets hello capturer la session.</span><span class="sxs-lookup"><span data-stu-id="46af6-129">Sets a time constraint on hello packet capture session.</span></span> <span data-ttu-id="46af6-130">valeur par défaut de Hello est 18000 secondes ou 5 heures.</span><span class="sxs-lookup"><span data-stu-id="46af6-130">hello default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="46af6-131">**Filtrage (facultatif)**</span><span class="sxs-lookup"><span data-stu-id="46af6-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="46af6-132">Propriété</span><span class="sxs-lookup"><span data-stu-id="46af6-132">Property</span></span>|<span data-ttu-id="46af6-133">Description</span><span class="sxs-lookup"><span data-stu-id="46af6-133">Description</span></span>|
|---|---|
|<span data-ttu-id="46af6-134">**Protocole**</span><span class="sxs-lookup"><span data-stu-id="46af6-134">**Protocol**</span></span> | <span data-ttu-id="46af6-135">toofilter de protocole Hello pour les paquets hello capturer.</span><span class="sxs-lookup"><span data-stu-id="46af6-135">hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="46af6-136">les valeurs disponibles Hello sont TCP, UDP et toutes.</span><span class="sxs-lookup"><span data-stu-id="46af6-136">hello available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="46af6-137">**Adresse IP locale**</span><span class="sxs-lookup"><span data-stu-id="46af6-137">**Local IP address**</span></span> | <span data-ttu-id="46af6-138">Cette valeur filtre toopackets de capture de paquets hello où l’adresse IP locale hello correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="46af6-138">This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>|
|<span data-ttu-id="46af6-139">**Port local**</span><span class="sxs-lookup"><span data-stu-id="46af6-139">**Local port**</span></span> | <span data-ttu-id="46af6-140">Cette valeur filtres hello paquet capture toopackets où port local de hello correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="46af6-140">This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>|
|<span data-ttu-id="46af6-141">**Adresse IP distante**</span><span class="sxs-lookup"><span data-stu-id="46af6-141">**Remote IP address**</span></span> | <span data-ttu-id="46af6-142">Cette valeur filtres hello paquet capture toopackets où adresse IP distante de hello correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="46af6-142">This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>|
|<span data-ttu-id="46af6-143">**Port distant**</span><span class="sxs-lookup"><span data-stu-id="46af6-143">**Remote port**</span></span> | <span data-ttu-id="46af6-144">Cette valeur filtres hello paquet capture toopackets où port distant de hello correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="46af6-144">This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="46af6-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="46af6-145">Next steps</span></span>

<span data-ttu-id="46af6-146">Découvrez comment vous pouvez gérer des captures de paquets via le portail de hello en vous rendant sur [gérer la capture des paquets Bonjour Azure portal](network-watcher-packet-capture-manage-portal.md) ou avec PowerShell en vous rendant sur [gérer la Capture de paquet avec PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="46af6-146">Learn how you can manage packet captures through hello portal by visiting [Manage packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="46af6-147">Découvrez comment les captures de paquets de proactive toocreate basés sur des alertes de l’ordinateur virtuel en vous rendant sur [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="46af6-147">Learn how toocreate proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













