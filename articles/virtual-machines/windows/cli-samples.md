---
title: "Exemples d’interface de ligne de commande Azure sur Windows | Microsoft Docs"
description: "Exemples d’interface de ligne de commande Azure sur Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f4b2e8a5583855df7472af3fbef01ac641caf6bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="00edd-103">Exemples d’interface de ligne de commande Azure pour machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="00edd-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="00edd-104">Le tableau suivant contient des liens vers des scripts Bash créés à l’aide de l’interface de ligne de commande Azure pour déployer des machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="00edd-104">The following table includes links to bash scripts built using the Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="00edd-105">**Créer des machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="00edd-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="00edd-106">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="00edd-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="00edd-107">Crée une machine virtuelle Windows avec une configuration minimale.</span><span class="sxs-lookup"><span data-stu-id="00edd-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="00edd-108">Créer une machine virtuelle entièrement configurée</span><span class="sxs-lookup"><span data-stu-id="00edd-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="00edd-109">Crée un groupe de ressources, une machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="00edd-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="00edd-110">Créer des machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="00edd-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="00edd-111">Crée plusieurs machines virtuelles dans une configuration haute disponibilité avec équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="00edd-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="00edd-112">Créer une machine virtuelle et exécuter le script de configuration</span><span class="sxs-lookup"><span data-stu-id="00edd-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="00edd-113">Crée une machine virtuelle et utilise l’extension de script personnalisé Azure pour installer IIS.</span><span class="sxs-lookup"><span data-stu-id="00edd-113">Creates a virtual machine and uses the Azure Custom Script extension to install IIS.</span></span> |
| [<span data-ttu-id="00edd-114">Créer une machine virtuelle et exécuter la configuration DSC</span><span class="sxs-lookup"><span data-stu-id="00edd-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="00edd-115">Crée une machine virtuelle et utilise l’extension DSC Azure pour installer IIS.</span><span class="sxs-lookup"><span data-stu-id="00edd-115">Creates a virtual machine and uses the Azure Desired State Configuration (DSC) extension to install IIS.</span></span> |
|<span data-ttu-id="00edd-116">**Mettre en réseau des machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="00edd-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="00edd-117">Sécuriser le trafic réseau entre les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="00edd-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="00edd-118">Crée deux machines virtuelles, toutes les ressources associées, ainsi qu’un groupe de sécurité réseau interne et un groupe de sécurité réseau externe.</span><span class="sxs-lookup"><span data-stu-id="00edd-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="00edd-119">**Sécuriser les machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="00edd-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="00edd-120">Chiffrer une machine virtuelle et des disques de données</span><span class="sxs-lookup"><span data-stu-id="00edd-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="00edd-121">Crée une solution Key Vault, une clé de chiffrement et le principal de service, puis chiffre une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="00edd-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="00edd-122">**Surveiller les machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="00edd-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="00edd-123">Surveiller une machine virtuelle avec Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="00edd-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="00edd-124">Crée une machine virtuelle, installe l’agent Operations Management Suite et inscrit la machine virtuelle dans un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="00edd-124">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span></span>  |
| | |
