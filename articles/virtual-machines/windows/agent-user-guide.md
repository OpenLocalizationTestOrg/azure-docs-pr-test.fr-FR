---
title: "Vue d’ensemble d’agent de machine virtuelle Azure | Microsoft Docs"
description: "Vue d’ensemble d’agent de machine virtuelle Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: nepeters
ms.openlocfilehash: 24ad2c2d2872f844e32d3fae559683c3d992bd00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="26e2e-103">Vue d’ensemble d’agent de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="26e2e-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="26e2e-104">L’agent de machine virtuelle Microsoft Azure (AM Agent) est un processus léger sécurisé qui gère l’interaction des machines virtuelles avec le contrôleur de structure Azure.</span><span class="sxs-lookup"><span data-stu-id="26e2e-104">The Microsoft Azure Virtual Machine Agent (AM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="26e2e-105">L’agent de machine virtuelle a un rôle essentiel dans l’activation et l’exécution des extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="26e2e-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="26e2e-106">Extensions de machine virtuelle permettant la configuration post-déploiement de machines virtuelles, comme l’installation et la configuration de logiciels.</span><span class="sxs-lookup"><span data-stu-id="26e2e-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="26e2e-107">Les extensions de machine virtuelle permettent également d’utiliser des fonctionnalités de récupération, telles que la réinitialisation du mot de passe d’administration d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="26e2e-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="26e2e-108">Sans l’agent de machine virtuelle Azure, les extensions de machine virtuelle ne peuvent pas être exécutées.</span><span class="sxs-lookup"><span data-stu-id="26e2e-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="26e2e-109">Ce document détaille l’installation, la détection et la suppression de l’agent de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="26e2e-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="26e2e-110">Installer l'agent de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="26e2e-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="26e2e-111">Image de la galerie Azure</span><span class="sxs-lookup"><span data-stu-id="26e2e-111">Azure gallery image</span></span>

<span data-ttu-id="26e2e-112">L’agent de machine virtuelle Azure est installé par défaut sur les machines virtuelles Windows déployées à partir d’une image de la galerie Azure.</span><span class="sxs-lookup"><span data-stu-id="26e2e-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="26e2e-113">Lorsque vous déployez une image de la galerie Azure à partir du portail, de PowerShell, de l’interface de ligne de commande ou d’un modèle Azure Resource Manager, l’agent de machine virtuelle Azure est également installé.</span><span class="sxs-lookup"><span data-stu-id="26e2e-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="26e2e-114">Installation manuelle</span><span class="sxs-lookup"><span data-stu-id="26e2e-114">Manual installation</span></span>

<span data-ttu-id="26e2e-115">L’agent de machine virtuelle Windows peut être installé manuellement à l’aide d’un package Windows installer.</span><span class="sxs-lookup"><span data-stu-id="26e2e-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="26e2e-116">Une installation manuelle peut être nécessaire lors de la création d’une image de machine virtuelle qui sera déployée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="26e2e-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="26e2e-117">Pour installer manuellement l’agent de machine virtuelle Windows, téléchargez le programme d’installation de l’agent de machine virtuelle à partir de cet emplacement : [Téléchargement de l’agent de machine virtuelle Windows Azure](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="26e2e-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="26e2e-118">L’agent de machine virtuelle peut être installé en double-cliquant sur le fichier Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="26e2e-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="26e2e-119">Pour une installation automatisée ou sans assistance de l’agent de machine virtuelle, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="26e2e-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="26e2e-120">Détecter l’agent de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="26e2e-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="26e2e-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26e2e-121">PowerShell</span></span>

<span data-ttu-id="26e2e-122">Le module PowerShell Azure Resource Manager peut être utilisé pour récupérer des informations sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="26e2e-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="26e2e-123">L’exécution de `Get-AzureRmVM` renvoie de nombreuses informations, dont l’état d’approvisionnement de l’agent de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="26e2e-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="26e2e-124">Ce qui suit n’est qu’un extrait de la sortie `Get-AzureRmVM`.</span><span class="sxs-lookup"><span data-stu-id="26e2e-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="26e2e-125">Notez la propriété `ProvisionVMAgent` imbriquée dans `OSProfile`. Cette propriété peut être utilisée pour déterminer si l’agent de machine virtuelle a été déployé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="26e2e-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="26e2e-126">Le script suivant peut être utilisé pour renvoyer une liste concise des noms des machines virtuelles et l’état de l’agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="26e2e-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="26e2e-127">Détection manuelle</span><span class="sxs-lookup"><span data-stu-id="26e2e-127">Manual Detection</span></span>

<span data-ttu-id="26e2e-128">Lorsque vous vous connectez à une machine virtuelle Windows Azure, le gestionnaire des tâches peut servir à examiner les processus en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="26e2e-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="26e2e-129">Pour vérifier l’agent de machine virtuelle Azure, ouvrez le Gestionnaire des tâches > cliquez sur l’onglet Détails et recherchez le nom de processus `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="26e2e-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="26e2e-130">La présence de ce processus indique que l’agent de machine virtuelle est installé.</span><span class="sxs-lookup"><span data-stu-id="26e2e-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="26e2e-131">Mettre à niveau l’agent de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="26e2e-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="26e2e-132">L’agent de machine virtuelle Azure est automatiquement mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="26e2e-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="26e2e-133">Lorsque de nouvelles machines virtuelles sont déployées sur Azure, elles reçoivent le dernier agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="26e2e-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="26e2e-134">Les images de machine virtuelle personnalisées doivent être manuellement mises à jour pour inclure le nouvel agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="26e2e-134">Custom VM images should be manually updated to include the new VM agent.</span></span>