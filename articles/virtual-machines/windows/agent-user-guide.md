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
# <a name="azure-virtual-machine-agent-overview"></a>Vue d’ensemble d’agent de machine virtuelle Azure

Hello Microsoft Azure Virtual Machine Agent (AM Agent) est un processus léger et sécurisé qui gère l’interaction avec hello contrôleur de structure Azure VM. Hello Agent de machine virtuelle a un rôle essentiel dans l’activation et l’exécution des extensions de machine virtuelle Azure. Extensions de machine virtuelle permettant la configuration post-déploiement de machines virtuelles, comme l’installation et la configuration de logiciels. Extensions de machine virtuelle également activer des fonctionnalités de récupération telles que la réinitialisation de mot de passe d’administration hello d’un ordinateur virtuel. Sans hello Agent de machine virtuelle Azure, les extensions de machine virtuelle ne peut pas être exécutées.

Ce document détaille l’installation, la détection et la suppression de l’Agent de Machine virtuelle Azure de hello.

## <a name="install-hello-vm-agent"></a>Installer l’Agent de machine virtuelle de hello

### <a name="azure-gallery-image"></a>Image de la galerie Azure

Hello Agent de machine virtuelle Azure est installé par défaut sur un ordinateur virtuel de Windows déployé à partir d’une image de la galerie Azure. Lorsque vous déployez une image de la galerie Azure à partir de hello Portal, PowerShell, Interface de ligne de commande ou un modèle Azure Resource Manager, hello Qu'agent de machine virtuelle Azure est également être installé. 

### <a name="manual-installation"></a>Installation manuelle

l’agent de machine virtuelle Windows Hello peut être installé manuellement à l’aide d’un package Windows installer. Une installation manuelle peut être nécessaire lors de la création d’une image de machine virtuelle qui sera déployée dans Azure. toomanually installation hello Agent de machine virtuelle Windows, téléchargez le programme d’installation de hello Agent de machine virtuelle à partir de cet emplacement [téléchargement de l’Agent Windows Azure VM](http://go.microsoft.com/fwlink/?LinkID=394789). 

Hello Agent de machine virtuelle peut être installé en double-cliquant sur le fichier de programme d’installation de windows hello. Pour une installation automatisée ou sans assistance de l’agent de machine virtuelle hello, exécutez hello commande suivante.

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>Détecter hello Agent de machine virtuelle

### <a name="powershell"></a>PowerShell

module d’Azure Resource Manager PowerShell Hello peut être utilisé tooretrieve plus d’informations sur les Machines virtuelles Azure. En cours d’exécution `Get-AzureRmVM` retourne reste un peu d’informations, y compris hello état pourquoi l’Agent de machine virtuelle Azure de configuration.

```PowerShell
Get-AzureRmVM
```

Bonjour suivant est uniquement un sous-ensemble de hello `Get-AzureRmVM` sortie. Hello d’avis `ProvisionVMAgent` propriété imbriquée dans `OSProfile`, cette propriété peut être utilisé toodetermine si l’agent de machine virtuelle hello a été déployé toohello virtual machine.

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

Hello script suivant peut être utilisé tooreturn une liste concise des noms des ordinateurs virtuels et l’état de hello Hello Agent de machine virtuelle.

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>Détection manuelle

Lorsque connecté tooa machine virtuelle Windows Azure, le Gestionnaire des tâches peut être utilisé tooexamine processus en cours d’exécution. toocheck pour hello Agent de machine virtuelle Azure, ouvrez le Gestionnaire des tâches > cliquez sur hello détails de l’onglet et recherchez un nom de processus `WindowsAzureGuestAgent.exe`. présence de Hello de ce processus indique que l’agent de machine virtuelle hello est installé.

## <a name="upgrade-hello-vm-agent"></a>Mise à niveau hello Agent de machine virtuelle

Bonjour Azure VM pour Windows de l’Agent est automatiquement mis à niveau. Comme de nouveaux ordinateurs virtuels sont déployé tooAzure, ils reçoivent agent de machine virtuelle hello plus récent. Les images de machine virtuelle personnalisées doivent être l’agent de machine virtuelle nouvelles mises à jour manuellement tooinclude hello.
