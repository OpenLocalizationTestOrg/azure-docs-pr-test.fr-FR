---
title: "connectivité aaaCheck avec l’Observateur réseau de Azure - portail Azure | Documents Microsoft"
description: "Cette page explique comment vérifier des toouse connectivité avec l’Observateur réseau à l’aide de hello portail Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="736f5-103">Vérifiez la connectivité avec l’Observateur réseau de Azure à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="736f5-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="736f5-104">Portail</span><span class="sxs-lookup"><span data-stu-id="736f5-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="736f5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="736f5-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="736f5-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="736f5-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="736f5-107">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="736f5-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="736f5-108">Découvrez comment toouse connectivité tooverify si une connexion TCP directe à partir d’un tooa de machine virtuelle donné du point de terminaison peut être établie.</span><span class="sxs-lookup"><span data-stu-id="736f5-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="736f5-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="736f5-109">Before you begin</span></span>

<span data-ttu-id="736f5-110">Cet article suppose que vous avez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="736f5-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="736f5-111">Une instance de l’Observateur réseau dans la région de hello souhaité toocheck connectivité.</span><span class="sxs-lookup"><span data-stu-id="736f5-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="736f5-112">Machines virtuelles toocheck la connectivité avec.</span><span class="sxs-lookup"><span data-stu-id="736f5-112">Virtual machines toocheck connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="736f5-113">La vérification de la connectivité requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="736f5-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="736f5-114">Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="736f5-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="736f5-115">Vérifiez la connectivité tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="736f5-115">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="736f5-116">Cet exemple vérifie l’ordinateur virtuel de destination de tooa connectivité via le port 80.</span><span class="sxs-lookup"><span data-stu-id="736f5-116">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

<span data-ttu-id="736f5-117">Accédez tooyour Observateur réseau et cliquez sur **vérification de la connectivité (version préliminaire)**.</span><span class="sxs-lookup"><span data-stu-id="736f5-117">Navigate tooyour Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="736f5-118">Sélectionnez la connectivité de toocheck hello machine virtuelle à partir de.</span><span class="sxs-lookup"><span data-stu-id="736f5-118">Select hello virtual machine toocheck connectivity from.</span></span> <span data-ttu-id="736f5-119">Bonjour **Destination** section Choisissez **sélectionnez une machine virtuelle** et choisir la machine virtuelle appropriée de hello et tootest de port.</span><span class="sxs-lookup"><span data-stu-id="736f5-119">In hello **Destination** section choose **Select a virtual machine** and choose hello correct virtual machine and port tootest.</span></span>

<span data-ttu-id="736f5-120">Une fois que vous cliquez sur **vérifier**, connectivité hello entre les machines virtuelles de hello sur port hello spécifié sont vérifiées.</span><span class="sxs-lookup"><span data-stu-id="736f5-120">Once you click **Check**, hello connectivity between hello virtual machines on hello port specified are checked.</span></span> <span data-ttu-id="736f5-121">Dans l’exemple de hello, hello destination machine virtuelle est inaccessible, une liste de sauts sont affichés.</span><span class="sxs-lookup"><span data-stu-id="736f5-121">In hello example, hello destination VM is unreachable, a listing of hops are shown.</span></span>

![Consulter les résultats de la connectivité d’une machine virtuelle][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="736f5-123">Vérifier la connectivité du point de terminaison distant</span><span class="sxs-lookup"><span data-stu-id="736f5-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="736f5-124">connectivité de hello toocheck et le point de terminaison distant latence tooa, choisissez hello **spécifier manuellement** case Bonjour **Destination** , d’entrée hello url et le port de hello et cliquez sur **vérifier** .</span><span class="sxs-lookup"><span data-stu-id="736f5-124">toocheck hello connectivity and latency tooa remote endpoint, choose hello **Specify manually** radio button in hello **Destination** section, input hello url and hello port and click **Check**.</span></span>  <span data-ttu-id="736f5-125">Cette opération est utilisée pour les points de terminaison distants comme des sites web et des points de terminaison de stockage.</span><span class="sxs-lookup"><span data-stu-id="736f5-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Consulter les résultats de la connectivité d’un site web][2]

## <a name="next-steps"></a><span data-ttu-id="736f5-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="736f5-127">Next steps</span></span>

<span data-ttu-id="736f5-128">Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="736f5-128">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="736f5-129">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="736f5-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
