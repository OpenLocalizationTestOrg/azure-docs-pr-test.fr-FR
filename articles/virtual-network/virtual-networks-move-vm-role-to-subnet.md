---
title: "aaaMove une machine virtuelle (classique) ou Services de cloud computing rôle instance tooa autre sous-réseau - Azure PowerShell | Documents Microsoft"
description: "Découvrez comment toomove machines virtuelles (classiques) et les instances de rôle des Services de cloud computing tooa autre sous-réseau à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a>Déplacer une machine virtuelle (classique) ou les Services de cloud computing rôle instance tooa sous-réseau différent à l’aide de PowerShell
Vous pouvez utiliser PowerShell toomove vos machines virtuelles (classiques) à partir d’un sous-réseau tooanother Bonjour même réseau virtuel (VNet). Instances de rôle peuvent être déplacés en modifiant le fichier CSCFG de hello, plutôt qu’à l’aide de PowerShell.

> [!NOTE]
> Cet article explique comment les ordinateurs virtuels de toomove déployés via le modèle de déploiement classique hello uniquement.
> 
> 

Pourquoi déplacer des machines virtuelles tooanother sous-réseau ? Migration de sous-réseau est utile lorsque le sous-réseau plus ancien de hello est trop petite et ne peuvent pas être développée à l’échéance tooexisting machines virtuelles s’exécutant dans ce sous-réseau. Dans ce cas, vous pouvez créer un sous-réseau nouvelle et migrer de nouveau sous-réseau hello machines virtuelles toohello, puis une fois la migration terminée, vous pouvez supprimer le sous-réseau de vide ancien hello.

## <a name="how-toomove-a-vm-tooanother-subnet"></a>Comment toomove tooanother sous-réseau d’ordinateurs virtuels
toomove une machine virtuelle, exécutez hello Set-AzureSubnet applet de commande PowerShell à l’aide d’exemple hello ci-dessous comme modèle. Dans l’exemple hello ci-dessous, nous déplaçons TestVM de son sous-réseau actuel, tooSubnet-2. Être vraiment tooedit hello exemple tooreflect votre environnement. Notez que chaque fois que vous exécutez l’applet de commande Update-AzureVM hello dans le cadre d’une procédure, il redémarrera votre machine virtuelle dans le cadre du processus de mise à jour hello.

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

Si vous avez spécifié une adresse IP privée interne statique pour votre machine virtuelle, vous devrez tooclear ce paramètre avant de pouvoir déplacer hello VM tooa sous-réseau. Dans ce cas, utilisez qui suit hello :

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a>toomove un sous-réseau de tooanother instance rôle
toomove une instance de rôle, modifiez le fichier CSCFG de hello. Dans l’exemple hello ci-dessous, nous déplaçons « Role0 » dans le réseau virtuel *VNETName* de son sous-réseau actuel trop*Subnet-2*. Étant donné que l’instance de rôle hello a déjà été déployé, vous devez juste modifier le nom du sous-réseau hello = Subnet-2. Être vraiment tooedit hello exemple tooreflect votre environnement.

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
