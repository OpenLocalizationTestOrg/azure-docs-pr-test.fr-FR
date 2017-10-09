---
title: "aaaStatic interne classique IP - Azure VM - privée"
description: "Présentation des adresses IP internes statique (adresses IP dynamiques) et la manière dont toomanage les"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>Comment tooset une adresse IP privée interne statique d’adresses à l’aide de PowerShell (classique)
Dans la plupart des cas, vous ne devez toospecify une adresse IP interne statique pour votre machine virtuelle. Les machines virtuelles dans un réseau virtuel recevront automatiquement une adresse IP interne à partir d'une plage que vous spécifiez. Toutefois, dans certains cas, il peut être bon de spécifier une adresse IP statique pour une machine virtuelle en particulier. Par exemple, si votre machine virtuelle est continu toorun DNS ou être un contrôleur de domaine. Une adresse IP interne statique reste associée aux hello machine virtuelle, même par le biais d’un état d’arrêt/mise hors service. 

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande à la plupart des nouveaux déploiements hello [modèle de déploiement de gestionnaire de ressources](virtual-networks-static-private-ip-arm-ps.md).
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>Comment tooverify si une adresse IP spécifique est disponible
tooverify si hello adresse IP *10.0.0.7* est disponible dans un réseau virtuel nommé *TestVnet*, exécutez hello suivant de commande PowerShell et vérifiez la valeur hello pour *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> Si vous souhaitez que la commande de hello tootest ci-dessus dans un environnement sécurisé instructions hello dans [créer un réseau virtuel (classiques)](virtual-networks-create-vnet-classic-pportal.md) toocreate un réseau virtuel nommé *TestVnet* et assurez-vous qu’il utilise hello  *10.0.0.0/8* l’espace d’adressage.
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>Comment toospecify une adresse IP interne statique lors de la création d’une machine virtuelle
Hello script PowerShell ci-dessous crée un nouveau service cloud nommé *TestService*, puis récupère une image à partir d’Azure, puis crée un ordinateur virtuel nommé *TestVM* dans le nouveau service cloud hello, à l’aide de l’image hello récupérée, jeux de hello toobe de machine virtuelle dans un sous-réseau nommé *Subnet-1*et définit *10.0.0.7* en tant qu’une adresse IP interne statique pour hello machine virtuelle :

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>Comment tooretrieve internes informations IP statique pour une machine virtuelle
tooview hello statique internes informations IP pour hello machine virtuelle créée avec le script hello ci-dessus, exécutez hello suivant de commande PowerShell et observer les valeurs hello pour *IpAddress*:

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>Comment tooremove une adresse IP interne statique d’une machine virtuelle
adresse IP interne statique de tooremove hello ajouté toohello machine virtuelle dans le script hello ci-dessus, exécutez hello suivant de commande PowerShell :

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>Comment tooadd un tooan d’IP interne statique machine virtuelle existante
tooadd un toohello IP interne statique machine virtuelle créée à l’aide de script hello ci-dessus, exécutez commande suivante :

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>Étapes suivantes
[Adresse IP réservée](virtual-networks-reserved-public-ip.md)

[Adresses IP publiques de niveau d’instance (ILPIP)](virtual-networks-instance-level-public-ip.md)

[API REST d’adresse IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx)

