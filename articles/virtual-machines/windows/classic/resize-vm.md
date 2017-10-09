---
title: "aaaResize un ordinateur virtuel Windows Azure - modèle de déploiement classique hello | Documents Microsoft"
description: "Redimensionner une machine virtuelle de Windows créée dans le modèle de déploiement classique de hello, à l’aide d’Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a>Redimensionner une machine virtuelle de Windows créé dans le modèle de déploiement classique de hello
Cet article explique comment tooresize une machine virtuelle Windows, créé dans le modèle de déploiement classique de hello à l’aide d’Azure Powershell.

Lorsque vous envisagez hello capacité tooresize une machine virtuelle, il existe deux concepts qui contrôlent la plage hello de machine virtuelle de tailles disponibles tooresize hello. Hello premier concept est la région de hello dans lequel votre machine virtuelle est déployée. liste de Hello des tailles de machine virtuelle disponibles dans la région est sous l’onglet Services de hello de page web de régions Azure hello. concept de deuxième Hello est votre machine virtuelle qui héberge actuellement un matériel physique hello. les serveurs physiques Hello héberge des ordinateurs virtuels sont regroupés dans des clusters de matériel physique commun. méthode Hello de la modification d’une taille de machine virtuelle diffère en fonction de hello souhaitée nouvelle taille de machine virtuelle est prise en charge par cluster de matériel hello hello machine virtuelle qui héberge actuellement.

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Vous pouvez également [redimensionner une machine virtuelle créée dans le modèle de déploiement du Gestionnaire de ressources hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="add-your-account"></a>Ajouter votre compte
Vous devez configurer Azure PowerShell toowork avec des ressources Azure classiques. Suivez les étapes de hello ci-dessous Azure PowerShell tooconfigure toomanage les ressources classiques.

1. À l’invite de commandes PowerShell hello, tapez `Add-AzureAccount` et cliquez sur **entrée**. 
2. Tapez hello adresse de messagerie associée à votre abonnement Azure et cliquez sur **continuer**. 
3. Tapez hello de mot de passe pour votre compte. 
4. Cliquez sur **Se connecter**. 

## <a name="resize-in-hello-same-hardware-cluster"></a>Redimensionner dans hello même cluster de matériel
tooresize une taille de tooa de machine virtuelle disponible dans le cluster de matériel hello hébergement hello machine virtuelle, effectuez hello comme suit.

1. Exécutez hello suivant de commande PowerShell tailles de machine virtuelle toolist hello disponibles dans le cluster de matériel hello hébergeant un service cloud hello qui contienne hello machine virtuelle.
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. Exécutez hello suivant de commandes tooresize hello machine virtuelle.
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>Redimensionner sur un nouveau cluster matériel
tooresize une taille de tooa de machine virtuelle non disponible dans hello matériel cluster héberge hello VM, hello service cloud et tous les ordinateurs virtuels dans le service cloud hello doivent être recréés. Chaque service cloud est hébergé sur un cluster de matériel unique pour tous les ordinateurs virtuels dans le service cloud hello doivent avoir une taille qui est pris en charge sur un cluster de matériel. Hello étapes suivantes décrivent comment tooresize une machine virtuelle en supprimant et en recréant puis hello cloud service.

1. Exécutez hello suivant PowerShell commande toolist hello tailles de machine virtuelle disponibles dans la région de hello. 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. Prenez note de tous les paramètres de configuration pour chaque ordinateur virtuel dans le service cloud hello contenant toobe de machine virtuelle hello redimensionné. 
3. Supprimez tous les ordinateurs virtuels dans le service cloud hello en sélectionnant hello option tooretain hello des disques pour chaque machine virtuelle.
4. Recréez toobe de machine virtuelle hello redimensionné à l’aide de la taille de machine virtuelle hello souhaité.
5. Recréez toutes les autres machines virtuelles qui étaient dans le service de cloud à l’aide d’une taille de machine virtuelle disponible dans cluster de matériel hello héberge désormais le service de cloud computing hello hello.

Vous trouverez [ici](https://github.com/Azure/azure-vm-scripts) un exemple de script de suppression et de recréation d’un service cloud avec une nouvelle taille de machines virtuelles. 

## <a name="next-steps"></a>Étapes suivantes
* [Redimensionner une machine virtuelle créée dans le modèle de déploiement du Gestionnaire de ressources hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

