---
title: "Présentation de l’Agent de Machine virtuelle d’aaaAzure | Documents Microsoft"
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
ms.openlocfilehash: b03542b9a9c711000fab18ed82e9b17ee5510bbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="e0cf8-103">Vue d’ensemble d’agent de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="e0cf8-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="e0cf8-104">Hello Microsoft Azure Virtual Machine Agent (AM Agent) est un processus léger et sécurisé qui gère l’interaction avec hello contrôleur de structure Azure VM.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-104">hello Microsoft Azure Virtual Machine Agent (AM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="e0cf8-105">Hello Agent de machine virtuelle a un rôle essentiel dans l’activation et l’exécution des extensions de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="e0cf8-106">Extensions de machine virtuelle permettant la configuration post-déploiement de machines virtuelles, comme l’installation et la configuration de logiciels.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="e0cf8-107">Extensions de machine virtuelle également activer des fonctionnalités de récupération telles que la réinitialisation de mot de passe d’administration hello d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="e0cf8-108">Sans hello Agent de machine virtuelle Azure, les extensions de machine virtuelle ne peut pas être exécutées.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="e0cf8-109">Ce document détaille l’installation, la détection et la suppression de l’Agent de Machine virtuelle Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="e0cf8-110">Installer l’Agent de machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="e0cf8-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="e0cf8-111">Image de la galerie Azure</span><span class="sxs-lookup"><span data-stu-id="e0cf8-111">Azure gallery image</span></span>

<span data-ttu-id="e0cf8-112">Hello Agent de machine virtuelle Azure est installé par défaut sur un ordinateur virtuel de Windows déployé à partir d’une image de la galerie Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="e0cf8-113">Lorsque vous déployez une image de la galerie Azure à partir de hello Portal, PowerShell, Interface de ligne de commande ou un modèle Azure Resource Manager, hello Qu'agent de machine virtuelle Azure est également être installé.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="e0cf8-114">Installation manuelle</span><span class="sxs-lookup"><span data-stu-id="e0cf8-114">Manual installation</span></span>

<span data-ttu-id="e0cf8-115">l’agent de machine virtuelle Windows Hello peut être installé manuellement à l’aide d’un package Windows installer.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="e0cf8-116">Une installation manuelle peut être nécessaire lors de la création d’une image de machine virtuelle qui sera déployée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="e0cf8-117">toomanually installation hello Agent de machine virtuelle Windows, téléchargez le programme d’installation de hello Agent de machine virtuelle à partir de cet emplacement [téléchargement de l’Agent Windows Azure VM](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="e0cf8-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="e0cf8-118">Hello Agent de machine virtuelle peut être installé en double-cliquant sur le fichier de programme d’installation de windows hello.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="e0cf8-119">Pour une installation automatisée ou sans assistance de l’agent de machine virtuelle hello, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="e0cf8-120">Détecter hello Agent de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e0cf8-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="e0cf8-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0cf8-121">PowerShell</span></span>

<span data-ttu-id="e0cf8-122">module d’Azure Resource Manager PowerShell Hello peut être utilisé tooretrieve plus d’informations sur les Machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="e0cf8-123">En cours d’exécution `Get-AzureRmVM` retourne reste un peu d’informations, y compris hello état pourquoi l’Agent de machine virtuelle Azure de configuration.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="e0cf8-124">Bonjour suivant est uniquement un sous-ensemble de hello `Get-AzureRmVM` sortie.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="e0cf8-125">Hello d’avis `ProvisionVMAgent` propriété imbriquée dans `OSProfile`, cette propriété peut être utilisé toodetermine si l’agent de machine virtuelle hello a été déployé toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="e0cf8-126">Hello script suivant peut être utilisé tooreturn une liste concise des noms des ordinateurs virtuels et l’état de hello Hello Agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="e0cf8-127">Détection manuelle</span><span class="sxs-lookup"><span data-stu-id="e0cf8-127">Manual Detection</span></span>

<span data-ttu-id="e0cf8-128">Lorsque connecté tooa machine virtuelle Windows Azure, le Gestionnaire des tâches peut être utilisé tooexamine processus en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="e0cf8-129">toocheck pour hello Agent de machine virtuelle Azure, ouvrez le Gestionnaire des tâches > cliquez sur hello détails de l’onglet et recherchez un nom de processus `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="e0cf8-130">présence de Hello de ce processus indique que l’agent de machine virtuelle hello est installé.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="e0cf8-131">Mise à niveau hello Agent de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e0cf8-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="e0cf8-132">Bonjour Azure VM pour Windows de l’Agent est automatiquement mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="e0cf8-133">Comme de nouveaux ordinateurs virtuels sont déployé tooAzure, ils reçoivent agent de machine virtuelle hello plus récent.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="e0cf8-134">Les images de machine virtuelle personnalisées doivent être l’agent de machine virtuelle nouvelles mises à jour manuellement tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="e0cf8-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
