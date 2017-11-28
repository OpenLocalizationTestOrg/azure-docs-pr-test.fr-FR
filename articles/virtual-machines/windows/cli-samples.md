---
title: aaaAzure CLI exemples Windows | Documents Microsoft
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
ms.openlocfilehash: 1eef61a24d14897dd0a88a3f467854cc21b1938d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="8d025-103">Exemples d’interface de ligne de commande Azure pour machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="8d025-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="8d025-104">Hello tableau suivant inclut des liens toobash des scripts créés à l’aide de hello CLI d’Azure à déployer des machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="8d025-104">hello following table includes links toobash scripts built using hello Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="8d025-105">**Créer des machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="8d025-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="8d025-106">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8d025-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8d025-107">Crée une machine virtuelle Windows avec une configuration minimale.</span><span class="sxs-lookup"><span data-stu-id="8d025-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="8d025-108">Créer une machine virtuelle entièrement configurée</span><span class="sxs-lookup"><span data-stu-id="8d025-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8d025-109">Crée un groupe de ressources, une machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="8d025-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="8d025-110">Créer des machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="8d025-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8d025-111">Crée plusieurs machines virtuelles dans une configuration haute disponibilité avec équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="8d025-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="8d025-112">Créer une machine virtuelle et exécuter le script de configuration</span><span class="sxs-lookup"><span data-stu-id="8d025-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8d025-113">Crée une machine virtuelle et utilise l’extension tooinstall IIS de hello Azure un Script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="8d025-113">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="8d025-114">Créer une machine virtuelle et exécuter la configuration DSC</span><span class="sxs-lookup"><span data-stu-id="8d025-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8d025-115">Crée une machine virtuelle et utilise tooinstall extension de Configuration d’état souhaité (DSC) Azure hello IIS.</span><span class="sxs-lookup"><span data-stu-id="8d025-115">Creates a virtual machine and uses hello Azure Desired State Configuration (DSC) extension tooinstall IIS.</span></span> |
|<span data-ttu-id="8d025-116">**Mettre en réseau des machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="8d025-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="8d025-117">Sécuriser le trafic réseau entre les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="8d025-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8d025-118">Crée deux machines virtuelles, toutes les ressources associées, ainsi qu’un groupe de sécurité réseau interne et un groupe de sécurité réseau externe.</span><span class="sxs-lookup"><span data-stu-id="8d025-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="8d025-119">**Sécuriser les machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="8d025-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="8d025-120">Chiffrer une machine virtuelle et des disques de données</span><span class="sxs-lookup"><span data-stu-id="8d025-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8d025-121">Crée une solution Key Vault, une clé de chiffrement et le principal de service, puis chiffre une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8d025-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="8d025-122">**Surveiller les machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="8d025-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="8d025-123">Surveiller une machine virtuelle avec Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="8d025-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8d025-124">Crée un ordinateur virtuel, installe l’agent de Operations Management Suite hello et inscrit hello machine virtuelle dans un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="8d025-124">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |
