---
title: "débit de réseau de machine virtuelle aaaOptimize | Documents Microsoft"
description: "Découvrez comment toooptimize machine virtuelle Azure débit du réseau."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="aed3d-103">Optimiser le débit du réseau des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="aed3d-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="aed3d-104">Les machines virtuelles Azure disposent de paramètres réseau par défaut qui peuvent être davantage optimisés pour le débit du réseau.</span><span class="sxs-lookup"><span data-stu-id="aed3d-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="aed3d-105">Cet article décrit comment toooptimize débit du réseau pour Windows Azure de Microsoft et les machines virtuelles Linux, y compris les distributions majeures telles que Ubuntu, CentOS et Red Hat.</span><span class="sxs-lookup"><span data-stu-id="aed3d-105">This article describes how toooptimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="aed3d-106">Machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="aed3d-106">Windows VM</span></span>

<span data-ttu-id="aed3d-107">Si votre machine virtuelle Windows est prise en charge avec [Accelerated réseau](virtual-network-create-vm-accelerated-networking.md), l’activation de cette fonctionnalité serait la configuration optimale de hello pour le débit.</span><span class="sxs-lookup"><span data-stu-id="aed3d-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be hello optimal configuration for throughput.</span></span> <span data-ttu-id="aed3d-108">Pour toutes les autres machines virtuelles Windows, l’utilisation de la mise à l’échelle côté réception (RSS) peut permettre d’atteindre un débit maximal supérieur à celui d’une machine virtuelle sans RSS.</span><span class="sxs-lookup"><span data-stu-id="aed3d-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="aed3d-109">La mise à l’échelle côté réception (RSS) peut être désactivée par défaut sur une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="aed3d-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="aed3d-110">Terminer hello suivant les étapes toodetermine si RSS est activé et tooenable si elle est désactivée.</span><span class="sxs-lookup"><span data-stu-id="aed3d-110">Complete hello following steps toodetermine whether RSS is enabled and tooenable it if it's disabled.</span></span>

1. <span data-ttu-id="aed3d-111">Entrez hello `Get-NetAdapterRss` toosee de commande PowerShell si RSS est activé pour une carte réseau.</span><span class="sxs-lookup"><span data-stu-id="aed3d-111">Enter hello `Get-NetAdapterRss` PowerShell command toosee if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="aed3d-112">Bonjour suivant l’exemple de sortie retourné par hello `Get-NetAdapterRss`, RSS n’est pas activé.</span><span class="sxs-lookup"><span data-stu-id="aed3d-112">In hello following example output returned from hello `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="aed3d-113">Entrez hello suivant commande tooenable RSS :</span><span class="sxs-lookup"><span data-stu-id="aed3d-113">Enter hello following command tooenable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="aed3d-114">commande précédente Hello n’a pas une sortie.</span><span class="sxs-lookup"><span data-stu-id="aed3d-114">hello previous command does not have an output.</span></span> <span data-ttu-id="aed3d-115">commande Hello modifié des paramètres de carte réseau, à l’origine de la perte de connectivité temporaire d’une minute environ.</span><span class="sxs-lookup"><span data-stu-id="aed3d-115">hello command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="aed3d-116">Une boîte de dialogue Nouvelle connexion en cours s’affiche lors de la perte de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="aed3d-116">A Reconnecting dialog box appears during hello connectivity loss.</span></span> <span data-ttu-id="aed3d-117">En général la connectivité est rétablie après une tentative de tiers hello.</span><span class="sxs-lookup"><span data-stu-id="aed3d-117">Connectivity is typically restored after hello third attempt.</span></span>
3. <span data-ttu-id="aed3d-118">Vérifiez que RSS est activé dans la machine virtuelle de hello en entrant hello `Get-NetAdapterRss` réexécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="aed3d-118">Confirm that RSS is enabled in hello VM by entering hello `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="aed3d-119">En cas de réussite, hello suivant l’exemple de sortie est retournée :</span><span class="sxs-lookup"><span data-stu-id="aed3d-119">If successful, hello following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="aed3d-120">Machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="aed3d-120">Linux VM</span></span>

<span data-ttu-id="aed3d-121">La mise à l’échelle côté réception (RSS) est toujours activée par défaut sur une machine virtuelle Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="aed3d-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="aed3d-122">Noyaux Linux publiées depuis janvier 2017 incluent de nouvelles options d’optimisation de réseau qui permettent un débit plus élevé du réseau tooachieve Linux VM.</span><span class="sxs-lookup"><span data-stu-id="aed3d-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM tooachieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="aed3d-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="aed3d-123">Ubuntu</span></span>

<span data-ttu-id="aed3d-124">Dans l’optimisation de l’ordre tooget hello, tout d’abord mettre à jour version toohello dernières pris en charge, à compter de juin 2017, qui est :</span><span class="sxs-lookup"><span data-stu-id="aed3d-124">In order tooget hello optimization, first update toohello latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="aed3d-125">Une fois la mise à jour hello est terminée, entrez hello suivant du noyau de commandes tooget hello plus récent :</span><span class="sxs-lookup"><span data-stu-id="aed3d-125">After hello update is complete, enter hello following commands tooget hello latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="aed3d-126">Commande facultative :</span><span class="sxs-lookup"><span data-stu-id="aed3d-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="aed3d-127">Noyau de la préversion Ubuntu Azure</span><span class="sxs-lookup"><span data-stu-id="aed3d-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="aed3d-128">Cette version d’évaluation Azure Linux noyau ne peut pas avoir hello même niveau de disponibilité et la fiabilité en tant qu’images de Marketplace et noyaux qui sont en général version en disponibilité.</span><span class="sxs-lookup"><span data-stu-id="aed3d-128">This Azure Linux Preview kernel may not have hello same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="aed3d-129">fonctionnalité de Hello n’est pas pris en charge peut-être avoir limitées des fonctionnalités et ne peut pas être aussi fiable que le noyau de hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="aed3d-129">hello feature is not supported, may have constrained capabilities, and may not be as reliable as hello default kernel.</span></span> <span data-ttu-id="aed3d-130">N’utilisez pas ce noyau pour les charges de travail de production.</span><span class="sxs-lookup"><span data-stu-id="aed3d-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="aed3d-131">Performances de débit significative possible en installant hello proposé noyau Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="aed3d-131">Significant throughput performance can be achieved by installing hello proposed Azure Linux kernel.</span></span> <span data-ttu-id="aed3d-132">tootry ce noyau, ajoutez cette ligne de too/etc/apt/sources.list</span><span class="sxs-lookup"><span data-stu-id="aed3d-132">tootry this kernel, add this line too/etc/apt/sources.list</span></span>

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="aed3d-133">Exécutez ensuite ces commandes en tant qu’utilisateur racine.</span><span class="sxs-lookup"><span data-stu-id="aed3d-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="aed3d-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="aed3d-134">CentOS</span></span>

<span data-ttu-id="aed3d-135">Dans l’optimisation de l’ordre tooget hello, tout d’abord mettre à jour version toohello dernières pris en charge, à compter de juillet 2017, qui est :</span><span class="sxs-lookup"><span data-stu-id="aed3d-135">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="aed3d-136">Une fois la mise à jour hello est terminée, installation Bonjour derniers Services d’intégration Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="aed3d-136">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="aed3d-137">optimisation de débit Hello est LIS, en commençant à partir de 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="aed3d-137">hello throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="aed3d-138">Entrez hello suivant de commandes tooinstall LIS :</span><span class="sxs-lookup"><span data-stu-id="aed3d-138">Enter hello following commands tooinstall LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="aed3d-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="aed3d-139">Red Hat</span></span>

<span data-ttu-id="aed3d-140">Dans l’optimisation de l’ordre tooget hello, tout d’abord mettre à jour version toohello dernières pris en charge, à compter de juillet 2017, qui est :</span><span class="sxs-lookup"><span data-stu-id="aed3d-140">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="aed3d-141">Une fois la mise à jour hello est terminée, installation Bonjour derniers Services d’intégration Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="aed3d-141">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="aed3d-142">optimisation de débit Hello est LIS, en commençant à partir de 4.2.</span><span class="sxs-lookup"><span data-stu-id="aed3d-142">hello throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="aed3d-143">Entrez hello suivant toodownload de commandes et installer LIS :</span><span class="sxs-lookup"><span data-stu-id="aed3d-143">Enter hello following commands toodownload and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="aed3d-144">En savoir plus sur Linux Integration Services Version 4.2 pour Hyper-V en consultant hello [page de téléchargement](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="aed3d-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing hello [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aed3d-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aed3d-145">Next steps</span></span>
* <span data-ttu-id="aed3d-146">Maintenant que hello machine virtuelle est optimisée, consultez résultat hello avec [la bande passante ou de débit test Azure VM](virtual-network-bandwidth-testing.md) pour votre scénario.</span><span class="sxs-lookup"><span data-stu-id="aed3d-146">Now that hello VM is optimized, see hello result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="aed3d-147">En savoir plus avec le [FAQ sur les réseaux virtuels Azure](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="aed3d-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
