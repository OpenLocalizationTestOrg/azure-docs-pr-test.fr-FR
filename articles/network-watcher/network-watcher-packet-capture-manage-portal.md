---
title: "captures de paquets d’aaaManage d’observateur de réseau Azure - portail Azure | Documents Microsoft"
description: "Cette page explique comment toomanage hello la fonctionnalité de capture de paquet de l’Observateur réseau à l’aide du portail Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="2f8f4-103">Gérer des captures de paquets avec l’Observateur réseau de Azure à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="2f8f4-103">Manage packet captures with Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2f8f4-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="2f8f4-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="2f8f4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f8f4-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="2f8f4-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2f8f4-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="2f8f4-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2f8f4-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="2f8f4-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="2f8f4-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="2f8f4-109">Capture de paquets de l’Observateur réseau vous permet de toocreate capture sessions tootrack trafic tooand à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="2f8f4-110">Les filtres sont fournies pour tooensure de session de capture hello que vous capturer le trafic hello seulement que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="2f8f4-111">Capture des paquets permet des anomalies de réseau toodiagnose proactive et réactive.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="2f8f4-112">Autres utilisations incluent la collecte des statistiques de réseau, obtenir des informations sur les intrusions, toodebug client-serveur de communications et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="2f8f4-113">En étant en mesure de tooremotely déclencheur paquet captures, cette fonctionnalité facilite hello de l’exécution d’une capture de paquets sur l’ordinateur souhaité hello, qui permet d’économiser un temps précieux et manuellement.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="2f8f4-114">Cet article passe en revue hello différentes tâches de gestion qui sont actuellement disponibles pour la capture des paquets.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="2f8f4-115">**Démarrer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="2f8f4-116">**Arrêter une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="2f8f4-117">**Supprimer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="2f8f4-118">**Télécharger une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="2f8f4-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="2f8f4-119">Before you begin</span></span>

<span data-ttu-id="2f8f4-120">Cet article suppose que vous avez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-120">This article assumes that you have hello following resources:</span></span>

- <span data-ttu-id="2f8f4-121">Une instance de l’Observateur réseau dans la région de hello souhaité toocreate une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="2f8f4-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="2f8f4-122">Une machine virtuelle avec les paquets hello capturer extension activée.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f8f4-123">La capture de paquets requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="2f8f4-124">Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="2f8f4-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-hello-portal"></a><span data-ttu-id="2f8f4-125">Extension de l’agent de Capture de paquets via le portail de hello</span><span class="sxs-lookup"><span data-stu-id="2f8f4-125">Packet Capture agent extension through hello portal</span></span>

<span data-ttu-id="2f8f4-126">capture des paquets hello tooinstall agent de machine virtuelle via le portail de hello, accédez tooyour virtual machine, cliquez sur **Extensions** > **ajouter** et recherchez **Agent de l’Observateur réseau pour Windows**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-126">tooinstall hello packet capture VM agent through hello portal, navigate tooyour virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![vue de l’agent][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="2f8f4-128">Vue d’ensemble des captures de paquets</span><span class="sxs-lookup"><span data-stu-id="2f8f4-128">Packet Capture overview</span></span>

<span data-ttu-id="2f8f4-129">Accédez toohello [portail Azure](https://portal.azure.com) et cliquez sur **réseau** > **Observateur réseau** > **de Capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-129">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="2f8f4-130">page Vue d’ensemble de Hello affiche qu'une liste de tous les paquets capture qui existent, quel que soit l’état de hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-130">hello overview page shows a list of all packet captures that exist no matter hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="2f8f4-131">Capture des paquets nécessite un compte de stockage toohello de connectivité sur le port 443.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-131">Packet capture requires connectivity toohello storage account over port 443.</span></span>

![Écran Vue d’ensemble des captures de paquets][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="2f8f4-133">Démarrer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="2f8f4-133">Start a packet capture</span></span>

<span data-ttu-id="2f8f4-134">Cliquez sur **ajouter** toocreate une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-134">Click **Add** toocreate a packet capture.</span></span>

<span data-ttu-id="2f8f4-135">propriétés de Hello qui peuvent être définies sur une capture de paquets sont :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-135">hello properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="2f8f4-136">**Paramètres principaux**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-136">**Main settings**</span></span>

- <span data-ttu-id="2f8f4-137">**Abonnement** -cette valeur est abonnement hello qui est utilisé, une instance de l’Observateur réseau est nécessaire dans chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-137">**Subscription** - This value is hello subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="2f8f4-138">**Groupe de ressources** -groupe de ressources hello de machine virtuelle hello ciblé.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-138">**Resource group** - hello resource group of hello virtual machine that is being targeted.</span></span>
- <span data-ttu-id="2f8f4-139">**Cibler la machine virtuelle** -machine virtuelle hello qui capture des paquets hello est en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="2f8f4-139">**Target virtual machine** - hello virtual machine that is running hello packet capture</span></span>
- <span data-ttu-id="2f8f4-140">**Nom de capture de paquet** -cette valeur est le nom de hello de capture de paquets hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-140">**Packet capture name** - This value is hello name of hello packet capture.</span></span>

<span data-ttu-id="2f8f4-141">**Configuration de la capture**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-141">**Capture configuration**</span></span>

- <span data-ttu-id="2f8f4-142">**Compte de stockage** : détermine si la capture de paquets est enregistrée dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="2f8f4-143">**Fichier** -détermine si une capture de paquets est enregistrée localement sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-143">**File** - Determines if a packet capture is saved locally on hello virtual machine.</span></span>
- <span data-ttu-id="2f8f4-144">**Comptes de stockage** -hello sélectionnée de capture de paquets hello stockage compte toosave dans.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-144">**Storage Accounts** - hello selected storage account toosave hello packet capture in.</span></span> <span data-ttu-id="2f8f4-145">Emplacement par défaut : https://{nom du compte de stockage}.blob.core.windows.net/network-watcher-logs/subscriptions/{ID d’abonnement}/resourcegroups/{nom du groupe de ressources}/providers/microsoft.compute/virtualmachines/{nom de la machine virtuelle}/{AA}/{MM}/{JJ}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="2f8f4-146">(Activé uniquement si **Stockage** est sélectionné.)</span><span class="sxs-lookup"><span data-stu-id="2f8f4-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="2f8f4-147">**Chemin d’accès local** -chemin d’accès local de hello sur une capture de paquets hello toosave machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-147">**Local file path** - hello local path on a virtual machine toosave hello packet capture.</span></span> <span data-ttu-id="2f8f4-148">(Activé uniquement si **Fichier** est sélectionné.)</span><span class="sxs-lookup"><span data-stu-id="2f8f4-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="2f8f4-149">Un chemin d’accès valide doit être fourni.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="2f8f4-150">**Nombre maximal d’octets par paquet** -hello du nombre d’octets à partir de chaque paquet sont capturées, tous les octets sont capturées, si ce champ est vide.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-150">**Maximum bytes per packet** - hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="2f8f4-151">**Nombre maximal d’octets par session** - Total nombre d’octets qui sont capturées, une fois la valeur de hello atteinte cesse de capture de paquets hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-151">**Maximum bytes per session** - Total number of bytes that are captured, once hello value is reached hello packet capture stops.</span></span>
- <span data-ttu-id="2f8f4-152">**Délai (secondes)** -définit une limite de temps pour toostop de capture de paquets hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-152">**Time limit (seconds)** - Sets a time limit for hello packet capture toostop.</span></span> <span data-ttu-id="2f8f4-153">La valeur par défaut est de 18 000 secondes.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="2f8f4-154">Les comptes de stockage Premium ne sont actuellement pas pris en charge pour le stockage des captures de paquets.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="2f8f4-155">**Filtrage (facultatif)**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="2f8f4-156">**Protocole** -hello toofilter de protocole pour la capture des paquets hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-156">**Protocol** - hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="2f8f4-157">les valeurs disponibles Hello sont TCP, UDP et toutes.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-157">hello available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="2f8f4-158">**Adresse IP locale** -cette valeur filtres toopackets de capture de paquets hello où l’adresse IP locale hello correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-158">**Local IP address** - This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>
- <span data-ttu-id="2f8f4-159">**Port local** -cette valeur filtres toopackets de capture de paquets hello où port local de hello correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-159">**Local port** - This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>
- <span data-ttu-id="2f8f4-160">**Adresse IP distante** -cette valeur filtres toopackets de capture de paquets hello où adresse IP distante de hello correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-160">**Remote IP address** - This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>
- <span data-ttu-id="2f8f4-161">**Port distant** -cette valeur filtres toopackets de capture de paquets hello où port distant de hello correspond à cette valeur de filtre.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-161">**Remote port** - This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="2f8f4-162">Les valeurs d’adresse IP et de port peuvent être une valeur unique, une plage de valeurs ou un ensemble</span><span class="sxs-lookup"><span data-stu-id="2f8f4-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="2f8f4-163">(c’est-à-dire, 80-1024 pour le port). Vous pouvez définir autant de filtres que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="2f8f4-164">Une fois que les valeurs hello sont remplis, cliquez sur **OK** toocreate capture des paquets hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-164">Once hello values are filled out, click **OK** toocreate hello packet capture.</span></span>

![créer une capture de paquets][2]

<span data-ttu-id="2f8f4-166">Après que hello délai défini sur capture des paquets hello a expiré, la capture des paquets hello s’arrête et peut être vérifiée.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-166">After hello time limit set on hello packet capture has expired, hello packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="2f8f4-167">Vous pouvez également arrêter manuellement des sessions de captures de paquets hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-167">You can also manually stop hello packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="2f8f4-168">Supprimer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="2f8f4-168">Delete a packet capture</span></span>

<span data-ttu-id="2f8f4-169">Dans les paquets hello capturer vue, cliquez sur hello **menu contextuel** (...) ou avec le bouton droit, puis cliquez sur **supprimer** capture des paquets hello toostop</span><span class="sxs-lookup"><span data-stu-id="2f8f4-169">In hello packet capture view, click hello **context menu** (...) or right click, and click **delete** toostop hello packet capture</span></span>

![supprimer une capture de paquets][3]

> [!NOTE]
> <span data-ttu-id="2f8f4-171">Suppression d’une capture de paquets ne supprime pas le fichier hello hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-171">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

<span data-ttu-id="2f8f4-172">Vous êtes invité tooconfirm vous souhaitez que la capture des paquets hello toodelete, cliquez sur **Oui**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-172">You are asked tooconfirm you want toodelete hello packet capture, click **Yes**</span></span>

![confirmation][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="2f8f4-174">Arrêter une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="2f8f4-174">Stop a packet capture</span></span>

<span data-ttu-id="2f8f4-175">Dans les paquets hello capturer vue, cliquez sur hello **menu contextuel** (...) ou avec le bouton droit, puis cliquez sur **arrêter** capture des paquets hello toostop</span><span class="sxs-lookup"><span data-stu-id="2f8f4-175">In hello packet capture view, click hello **context menu** (...) or right click, and click **Stop** toostop hello packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="2f8f4-176">Télécharger une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="2f8f4-176">Download a packet capture</span></span>

<span data-ttu-id="2f8f4-177">Une fois terminé, votre session de capture de paquets hello capture fichier est téléchargé tooblob tooa ou stockage local sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-177">Once your packet capture session has completed, hello capture file is uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="2f8f4-178">emplacement de stockage Hello de capture de paquets hello est définie lors de la création de la session de hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-178">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="2f8f4-179">Un outil pratique de tooaccess ces fichiers de capture de compte de stockage tooa enregistré est Microsoft Azure Storage Explorer, qui peut être téléchargée ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="2f8f4-179">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="2f8f4-180">Si un compte de stockage est spécifié, les fichiers de capture de paquet sont enregistrés compte de stockage tooa hello l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-180">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="2f8f4-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f8f4-181">Next steps</span></span>

<span data-ttu-id="2f8f4-182">Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="2f8f4-182">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="2f8f4-183">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2f8f4-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













