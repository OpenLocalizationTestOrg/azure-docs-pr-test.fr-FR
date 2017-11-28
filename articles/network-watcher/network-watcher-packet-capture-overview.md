---
title: "Présentation de la capture de paquets dans Azure Network Watcher | Microsoft Docs"
description: "Cette page fournit une vue d’ensemble de la fonctionnalité de capture de paquets de Network Watcher."
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
ms.openlocfilehash: 4fdd007c2cfad7b42f26ab2cacfba06d95c8dad3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-variable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="85be8-103">Présentation de la capture de paquets variable dans Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="85be8-103">Introduction to variable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="85be8-104">La fonctionnalité de capture de paquets variable de Network Watcher vous permet de créer des sessions de capture de paquets afin d’effectuer le suivi du trafic en direction et en provenance d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="85be8-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="85be8-105">La capture de paquets aide à diagnostiquer les anomalies réseau de manière proactive et réactive.</span><span class="sxs-lookup"><span data-stu-id="85be8-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="85be8-106">Elle permet aussi de collecter des statistiques réseau, d’obtenir des informations sur les intrusions, de déboguer des communications client-serveur, etc.</span><span class="sxs-lookup"><span data-stu-id="85be8-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="85be8-107">La capture de paquets est une extension de machine virtuelle qui est démarrée à distance par le biais de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="85be8-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="85be8-108">Cette fonctionnalité allège la tâche d’exécution manuelle d’une capture de paquets sur la machine virtuelle souhaitée et permet ainsi d’économiser un temps précieux.</span><span class="sxs-lookup"><span data-stu-id="85be8-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="85be8-109">La capture de paquets peut être déclenchée par l’intermédiaire du portail, de PowerShell, de l’interface de ligne de commande ou de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="85be8-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="85be8-110">Les alertes de machine virtuelle constituent un exemple de mode de déclenchement de la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="85be8-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="85be8-111">Des filtres sont fournis pour la session de capture afin de vous permettre de capturer uniquement le trafic que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="85be8-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span></span> <span data-ttu-id="85be8-112">Ces filtres reposent sur des informations à 5 tuples (protocole, adresse IP locale, adresse IP distante, port local et port distant).</span><span class="sxs-lookup"><span data-stu-id="85be8-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="85be8-113">Les données capturées sont stockées dans le disque local ou dans un objet blob de stockage.</span><span class="sxs-lookup"><span data-stu-id="85be8-113">The captured data is stored in the local disk or a storage blob.</span></span> <span data-ttu-id="85be8-114">Il existe une limite de 10 sessions de capture de paquets par région par abonnement.</span><span class="sxs-lookup"><span data-stu-id="85be8-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="85be8-115">Cette limite s’applique uniquement aux sessions, mais pas aux fichiers de capture de paquets enregistrés localement sur la machine virtuelle ou dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="85be8-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85be8-116">La capture de paquets requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="85be8-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="85be8-117">Pour installer l’extension sur une machine virtuelle Windows, consultez la page [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) (Extension de machine virtuelle Azure Network Watcher Agent pour Windows). Pour une machine virtuelle Linux, consultez la page [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md) (Extension de machine virtuelle Azure Network Watcher Agent pour Linux).</span><span class="sxs-lookup"><span data-stu-id="85be8-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="85be8-118">Pour capturer uniquement les informations qui vous intéressent, vous disposez des options ci-après dans le cadre d’une session de capture de paquets :</span><span class="sxs-lookup"><span data-stu-id="85be8-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span></span>

<span data-ttu-id="85be8-119">**Configuration de la capture**</span><span class="sxs-lookup"><span data-stu-id="85be8-119">**Capture configuration**</span></span>

|<span data-ttu-id="85be8-120">Propriété</span><span class="sxs-lookup"><span data-stu-id="85be8-120">Property</span></span>|<span data-ttu-id="85be8-121">Description</span><span class="sxs-lookup"><span data-stu-id="85be8-121">Description</span></span>|
|---|---|
|<span data-ttu-id="85be8-122">**Nombre maximal d’octets par paquet (octets)**</span><span class="sxs-lookup"><span data-stu-id="85be8-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="85be8-123">Nombre d’octets capturés dans chaque paquet. Si ce champ est vide, tous les octets sont capturés.</span><span class="sxs-lookup"><span data-stu-id="85be8-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="85be8-124">Nombre d’octets capturés dans chaque paquet. Si ce champ est vide, tous les octets sont capturés.</span><span class="sxs-lookup"><span data-stu-id="85be8-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="85be8-125">Si seul l’en-tête IPv4 vous intéresse, indiquez 34 dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="85be8-125">If you need only the IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="85be8-126">**Nombre maximal d’octets par session (octets)**</span><span class="sxs-lookup"><span data-stu-id="85be8-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="85be8-127">Nombre total d’octets capturés. Une fois que cette valeur est atteinte, la session prend fin.</span><span class="sxs-lookup"><span data-stu-id="85be8-127">Total number of bytes in that are captured, once the value is reached the session ends.</span></span>|
|<span data-ttu-id="85be8-128">**Délai imparti (secondes)**</span><span class="sxs-lookup"><span data-stu-id="85be8-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="85be8-129">Contrainte de temps définie pour la session de capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="85be8-129">Sets a time constraint on the packet capture session.</span></span> <span data-ttu-id="85be8-130">La valeur par défaut est de 18 000 secondes (5 heures).</span><span class="sxs-lookup"><span data-stu-id="85be8-130">The default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="85be8-131">**Filtrage (facultatif)**</span><span class="sxs-lookup"><span data-stu-id="85be8-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="85be8-132">Propriété</span><span class="sxs-lookup"><span data-stu-id="85be8-132">Property</span></span>|<span data-ttu-id="85be8-133">Description</span><span class="sxs-lookup"><span data-stu-id="85be8-133">Description</span></span>|
|---|---|
|<span data-ttu-id="85be8-134">**Protocole**</span><span class="sxs-lookup"><span data-stu-id="85be8-134">**Protocol**</span></span> | <span data-ttu-id="85be8-135">Protocole permettant de filtrer la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="85be8-135">The protocol to filter for the packet capture.</span></span> <span data-ttu-id="85be8-136">Valeurs possibles : TCP, UDP et Tous.</span><span class="sxs-lookup"><span data-stu-id="85be8-136">The available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="85be8-137">**Adresse IP locale**</span><span class="sxs-lookup"><span data-stu-id="85be8-137">**Local IP address**</span></span> | <span data-ttu-id="85be8-138">Cette valeur filtre la capture de paquets sur ceux dont l’adresse IP locale correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="85be8-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>|
|<span data-ttu-id="85be8-139">**Port local**</span><span class="sxs-lookup"><span data-stu-id="85be8-139">**Local port**</span></span> | <span data-ttu-id="85be8-140">Cette valeur filtre la capture de paquets sur ceux dont le port local correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="85be8-140">This value filters the packet capture to packets where the local port matches this filter value.</span></span>|
|<span data-ttu-id="85be8-141">**Adresse IP distante**</span><span class="sxs-lookup"><span data-stu-id="85be8-141">**Remote IP address**</span></span> | <span data-ttu-id="85be8-142">Cette valeur filtre la capture de paquets sur ceux dont l’adresse IP distante correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="85be8-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>|
|<span data-ttu-id="85be8-143">**Port distant**</span><span class="sxs-lookup"><span data-stu-id="85be8-143">**Remote port**</span></span> | <span data-ttu-id="85be8-144">Cette valeur filtre la capture de paquets sur ceux dont le port distant correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="85be8-144">This value filters the packet capture to packets where the remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="85be8-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="85be8-145">Next steps</span></span>

<span data-ttu-id="85be8-146">Découvrez comment gérer les captures de paquets par le biais du portail en consultant l’article [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) (Gérer les captures de paquets dans le Portail Azure), ou par l’intermédiaire de PowerShell en consultant l’article [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md) (Gérer les captures de paquets à l’aide de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="85be8-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="85be8-147">Apprenez à créer des captures de paquets proactives reposant sur des alertes de machine virtuelle en consultant l’article [Create an alert triggered packet capture (Créer une capture de paquets déclenchée par alerte)](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="85be8-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













