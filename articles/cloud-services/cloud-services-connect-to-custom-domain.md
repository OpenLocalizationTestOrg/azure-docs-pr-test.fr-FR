---
title: "aaaConnect un tooa de Service Cloud contrôleur de domaine personnalisé | Documents Microsoft"
description: "Découvrez comment tooconnect votre personnalisé de tooa de rôles web/de travail domaine Active Directory à l’aide de PowerShell et l’Extension de domaine Active Directory"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a>Connexion personnalisée tooa de rôles des Services Azure Cloud hébergé par le contrôleur de domaine Active Directory dans Azure
Nous allons tout d’abord définir un réseau virtuel (VNet) dans Azure. Nous allons ensuite ajouter un contrôleur de domaine Active Directory (hébergé sur une Machine virtuelle de Azure) de toohello réseau virtuel. Ensuite, nous Ajouter existant toohello de rôles de service cloud créé au préalable réseau virtuel, puis connectez-les toohello contrôleur de domaine.

Avant de commencer, deux de tookeep choses à l’esprit :

1. Ce didacticiel utilise PowerShell, par conséquent, assurez-vous que vous disposez d’Azure PowerShell est installé et prêt toogo. tooget de l’aide sur la configuration d’Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
2. Les instances de votre contrôleur de domaine Active Directory et les rôles Web/de travail doivent toobe Bonjour réseau virtuel.

Suivez ce guide pas à pas et si vous rencontrez des problèmes, nous laisser un commentaire à la fin de hello de l’article de hello. Une personne retrouvez tooyou (Oui, nous lisons commentaires).

réseau Hello qui est référencé par le service de cloud computing hello doit être un **réseau virtuel classique**.

## <a name="create-a-virtual-network"></a>Création d'un réseau virtuel
Vous pouvez créer un réseau virtuel dans Azure à l’aide de hello portail Azure ou PowerShell. Pour ce didacticiel, nous utiliserons Powershell. un réseau virtuel à l’aide de toocreate hello Azure portail, consultez [créer un réseau virtuel](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle
Une fois que vous avez terminé la configuration de réseau virtuel de hello, vous devez toocreate un contrôleur de domaine Active Directory. Pour ce didacticiel, nous configurerons un contrôleur de domaine Active Directory sur une machine virtuelle Azure.

toodo, créez une machine virtuelle via PowerShell à l’aide de hello suivant de commandes :

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a>Promouvoir votre tooa d’ordinateur virtuel contrôleur de domaine
tooconfigure hello Machine virtuelle tant que contrôleur de domaine Active Directory, vous devez toolog dans toohello machine virtuelle et configurez-le.

toolog dans toohello machine virtuelle, vous pouvez obtenir le fichier RDP de hello via PowerShell, hello utilisation suivant de commandes :

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

Une fois que vous êtes connecté toohello VM, configuré votre Machine virtuelle comme un contrôleur de domaine Active Directory en suivant guide pas à pas de hello dans [comment tooset votre contrôleur de domaine Active Directory du client](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).

## <a name="add-your-cloud-service-toohello-virtual-network"></a>Ajoutez votre réseau virtuel de toohello Service Cloud
Ensuite, vous devez tooadd votre toohello de déploiement de service cloud nouveau réseau virtuel. toodo, modifier votre service cloud cscfg en ajoutant hello sections pertinentes tooyour cscfg à l’aide de Visual Studio ou de bienvenue de l’éditeur de votre choix.

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

Ensuite, générez votre projet de services cloud et déployez-le tooAzure. aide tooget avec le déploiement de votre tooAzure de package de services cloud, consultez [comment tooCreate et déployer un Service Cloud](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)

## <a name="connect-your-webworker-roles-toohello-domain"></a>Se connecter à votre domaine toohello de rôles web/de travail
Une fois votre projet de service cloud est déployé sur Azure, connectez-vous à votre domaine toohello AD personnalisé d’instances de rôle hello Extension de domaine Active Directory à l’aide de. tooadd hello déploiement des services cloud existant Extension de domaine Active Directory tooyour et joindre le domaine personnalisé hello, exécutez hello suivant les commandes dans PowerShell :

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

Et c’est terminé !

Vos services de cloud doivent être le contrôleur de domaine personnalisé tooyour jointes. Si vous souhaitez que toolearn plus hello différentes options disponibles pour la tooconfigure Extension de domaine Active Directory, utilisez hello PowerShell aide. Voici quelques exemples :

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
