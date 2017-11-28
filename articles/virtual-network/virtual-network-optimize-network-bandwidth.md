---
title: "Optimiser le débit du réseau des machines virtuelles | Microsoft Docs"
description: "Découvrez comment optimiser le débit du réseau des machines virtuelles Azure."
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
ms.openlocfilehash: 914747983d4d974810836be66d6c6af343f58b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="8287a-103">Optimiser le débit du réseau des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="8287a-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="8287a-104">Les machines virtuelles Azure disposent de paramètres réseau par défaut qui peuvent être davantage optimisés pour le débit du réseau.</span><span class="sxs-lookup"><span data-stu-id="8287a-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="8287a-105">Cet article décrit comment optimiser le débit du réseau pour les machines virtuelles Microsoft Azure Windows et Linux, notamment les distributions majeures telles que Ubuntu, CentOS et Red Hat.</span><span class="sxs-lookup"><span data-stu-id="8287a-105">This article describes how to optimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="8287a-106">Machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="8287a-106">Windows VM</span></span>

<span data-ttu-id="8287a-107">Si votre machine virtuelle Windows est compatible avec la [mise en réseau accélérée](virtual-network-create-vm-accelerated-networking.md), l’activation de cette fonctionnalité constitue la configuration optimale pour le débit.</span><span class="sxs-lookup"><span data-stu-id="8287a-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be the optimal configuration for throughput.</span></span> <span data-ttu-id="8287a-108">Pour toutes les autres machines virtuelles Windows, l’utilisation de la mise à l’échelle côté réception (RSS) peut permettre d’atteindre un débit maximal supérieur à celui d’une machine virtuelle sans RSS.</span><span class="sxs-lookup"><span data-stu-id="8287a-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="8287a-109">La mise à l’échelle côté réception (RSS) peut être désactivée par défaut sur une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="8287a-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="8287a-110">Effectuez les étapes suivantes pour déterminer si la mise à l’échelle côté réception (RSS) est activée et, si nécessaire, pour l’activer.</span><span class="sxs-lookup"><span data-stu-id="8287a-110">Complete the following steps to determine whether RSS is enabled and to enable it if it's disabled.</span></span>

1. <span data-ttu-id="8287a-111">Entrez la commande PowerShell `Get-NetAdapterRss` pour savoir si la mise à l’échelle côté réception (RSS) est activée sur une carte réseau.</span><span class="sxs-lookup"><span data-stu-id="8287a-111">Enter the `Get-NetAdapterRss` PowerShell command to see if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="8287a-112">Dans l’exemple de sortie suivant retourné par `Get-NetAdapterRss`, la mise à l’échelle côté réception (RSS) n’est pas activée.</span><span class="sxs-lookup"><span data-stu-id="8287a-112">In the following example output returned from the `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="8287a-113">Entrez la commande suivante pour activer la mise à l’échelle côté réception (RSS) :</span><span class="sxs-lookup"><span data-stu-id="8287a-113">Enter the following command to enable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="8287a-114">La commande précédente n’a pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="8287a-114">The previous command does not have an output.</span></span> <span data-ttu-id="8287a-115">La commande a modifié les paramètres de la carte réseau, entraînant une perte temporaire de la connectivité pendant environ une minute.</span><span class="sxs-lookup"><span data-stu-id="8287a-115">The command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="8287a-116">Une boîte de dialogue de reconnexion s’affiche lors de la perte de connectivité.</span><span class="sxs-lookup"><span data-stu-id="8287a-116">A Reconnecting dialog box appears during the connectivity loss.</span></span> <span data-ttu-id="8287a-117">En général, la connectivité est rétablie après la troisième tentative.</span><span class="sxs-lookup"><span data-stu-id="8287a-117">Connectivity is typically restored after the third attempt.</span></span>
3. <span data-ttu-id="8287a-118">Vérifiez que la mise à l’échelle côté réception (RSS) est activée sur la machine virtuelle en entrant de nouveau la commande `Get-NetAdapterRss`.</span><span class="sxs-lookup"><span data-stu-id="8287a-118">Confirm that RSS is enabled in the VM by entering the `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="8287a-119">Si l’opération réussit, l’exemple de sortie suivant est retourné :</span><span class="sxs-lookup"><span data-stu-id="8287a-119">If successful, the following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="8287a-120">Machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="8287a-120">Linux VM</span></span>

<span data-ttu-id="8287a-121">La mise à l’échelle côté réception (RSS) est toujours activée par défaut sur une machine virtuelle Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="8287a-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="8287a-122">Les noyaux Linux publiés depuis janvier 2017 incluent de nouvelles options d’optimisation du réseau qui permettent à une machine virtuelle Linux d’obtenir un débit réseau plus élevé.</span><span class="sxs-lookup"><span data-stu-id="8287a-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM to achieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="8287a-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8287a-123">Ubuntu</span></span>

<span data-ttu-id="8287a-124">Pour bénéficier de l’optimisation, mettez tout d’abord à jour vers la version la plus récente, à compter de juin 2017, qui est :</span><span class="sxs-lookup"><span data-stu-id="8287a-124">In order to get the optimization, first update to the latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="8287a-125">Une fois la mise à jour terminée, entrez les commandes suivantes pour obtenir le noyau le plus récent :</span><span class="sxs-lookup"><span data-stu-id="8287a-125">After the update is complete, enter the following commands to get the latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="8287a-126">Commande facultative :</span><span class="sxs-lookup"><span data-stu-id="8287a-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="8287a-127">Noyau de la préversion Ubuntu Azure</span><span class="sxs-lookup"><span data-stu-id="8287a-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="8287a-128">Ce noyau de la préversion Azure Linux peut ne pas offrir les mêmes niveaux de disponibilité et de fiabilité que les noyaux et images de la Place de marché qui se trouvent dans la version mise à la disposition générale.</span><span class="sxs-lookup"><span data-stu-id="8287a-128">This Azure Linux Preview kernel may not have the same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="8287a-129">La fonctionnalité n’est pas prise en charge, est susceptible de disposer de possibilités limitées et peut ne pas être aussi fiable que le noyau par défaut.</span><span class="sxs-lookup"><span data-stu-id="8287a-129">The feature is not supported, may have constrained capabilities, and may not be as reliable as the default kernel.</span></span> <span data-ttu-id="8287a-130">N’utilisez pas ce noyau pour les charges de travail de production.</span><span class="sxs-lookup"><span data-stu-id="8287a-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="8287a-131">Des performances significatives en termes de débit peuvent être atteintes en installant le noyau Azure Linux proposé.</span><span class="sxs-lookup"><span data-stu-id="8287a-131">Significant throughput performance can be achieved by installing the proposed Azure Linux kernel.</span></span> <span data-ttu-id="8287a-132">Pour tester ce noyau, ajoutez cette ligne à /etc/apt/sources.list.</span><span class="sxs-lookup"><span data-stu-id="8287a-132">To try this kernel, add this line to /etc/apt/sources.list</span></span>

```bash
#add this to the end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="8287a-133">Exécutez ensuite ces commandes en tant qu’utilisateur racine.</span><span class="sxs-lookup"><span data-stu-id="8287a-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="8287a-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="8287a-134">CentOS</span></span>

<span data-ttu-id="8287a-135">Pour bénéficier de l’optimisation, mettez tout d’abord à jour vers la version la plus récente, à compter de juillet 2017, qui est :</span><span class="sxs-lookup"><span data-stu-id="8287a-135">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="8287a-136">Une fois la mise à jour terminée, installez les Services d’intégration Linux (LIS) les plus récents.</span><span class="sxs-lookup"><span data-stu-id="8287a-136">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="8287a-137">L’optimisation du débit est incluse dans les LIS, à partir de la version 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="8287a-137">The throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="8287a-138">Entrez les commandes suivantes pour installer LIS :</span><span class="sxs-lookup"><span data-stu-id="8287a-138">Enter the following commands to install LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="8287a-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="8287a-139">Red Hat</span></span>

<span data-ttu-id="8287a-140">Pour bénéficier de l’optimisation, mettez tout d’abord à jour vers la version la plus récente, à compter de juillet 2017, qui est :</span><span class="sxs-lookup"><span data-stu-id="8287a-140">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="8287a-141">Une fois la mise à jour terminée, installez les Services d’intégration Linux (LIS) les plus récents.</span><span class="sxs-lookup"><span data-stu-id="8287a-141">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="8287a-142">L’optimisation du débit est incluse dans les LIS, à partir de la version 4.2.</span><span class="sxs-lookup"><span data-stu-id="8287a-142">The throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="8287a-143">Entrez les commandes suivantes pour télécharger et installer les LIS :</span><span class="sxs-lookup"><span data-stu-id="8287a-143">Enter the following commands to download and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="8287a-144">Apprenez-en plus sur les Services d’intégration Linux version 4.2 pour Hyper-V en consultant la [page de téléchargement](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="8287a-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing the [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8287a-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8287a-145">Next steps</span></span>
* <span data-ttu-id="8287a-146">À présent que la machine virtuelle est optimisée, voyez le résultat avec le [Test de bande passante/débit de machine virtuelle](virtual-network-bandwidth-testing.md) pour votre scénario.</span><span class="sxs-lookup"><span data-stu-id="8287a-146">Now that the VM is optimized, see the result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="8287a-147">En savoir plus avec le [FAQ sur les réseaux virtuels Azure](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="8287a-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
