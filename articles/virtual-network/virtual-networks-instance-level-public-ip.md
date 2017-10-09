---
title: des adresses IP publiques (classiques) aaaAzure niveau Instance | Documents Microsoft
description: "Comprendre les adresses IP (ILPIP) publique au niveau instance et comment toomanage les à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a>Vue d’ensemble des adresses IP publiques de niveau d’instance (classique)
Une instance IP publique au niveau (ILPIP) est une adresse IP publique que vous pouvez attribuer directement instance de rôle de machine virtuelle ou les Services de cloud computing tooa, plutôt que service cloud toohello résidant dans votre machine virtuelle ou instance de rôle. Un ILPIP n’a pas lieu hello hello adresse IP virtuelle (VIP) qui est affectée à tooyour le service cloud. Au lieu de cela, il est une adresse IP supplémentaire que vous pouvez utiliser tooconnect directement tooyour machine virtuelle ou instance de rôle.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft vous recommande de créer des machines virtuelles via Resource Manager. Assurez-vous que vous comprenez le fonctionnement des [adresses IP](virtual-network-ip-addresses-overview-classic.md) dans Azure.

![Différences entre les adresses IP publiques de niveau d’instance (ILPIP) et les adresses IP virtuelles (VIP)](./media/virtual-networks-instance-level-public-ip/Figure1.png)

Comme indiqué dans la Figure 1, le service cloud hello est accessible à l’aide d’une adresse IP virtuelle, lors de hello des ordinateurs virtuels individuels sont normalement accessibles à l’aide d’adresses IP virtuelles :&lt;numéro de port&gt;. En assignant un tooa ILPIP un ordinateur virtuel spécifique, qui peuvent être des ordinateurs virtuels accessibles directement à l’aide de cette adresse IP.

Lorsque vous créez un service cloud dans Azure, les enregistrements A DNS correspondants sont créés automatiquement service de toohello tooallow accès via un nom de domaine complet (FQDN), au lieu d’utiliser l’adresse IP virtuelle réel de hello. Hello même processus se produit pour un ILPIP, ce qui permet l’accès toohello machine virtuelle ou instance de rôle par le nom de domaine complet au lieu de hello ILPIP. Par exemple, si vous créez un service cloud nommé *contosoadservice*, et que vous configurez un rôle web nommé *contosoweb* avec deux instances, hello registres Azure suivant A des enregistrements pour les instances de hello :

* contosoweb\_IN_0.contosoadservice.cloudapp.net
* contosoweb\_IN_1.contosoadservice.cloudapp.net 

> [!NOTE]
> Vous ne pouvez affecter qu’une seule adresse ILPIP par machine virtuelle ou instance de rôle. Vous pouvez utiliser des ILPIPs too5 par abonnement. Les adresses ILPIP ne sont pas prises en charge pour les machines virtuelles à plusieurs cartes réseau.
> 
> 

## <a name="why-would-i-request-an-ilpip"></a>Pourquoi demander une adresse ILPIP ?
Si vous souhaitez toobe tooyour de tooconnect en mesure de machine virtuelle ou instance de rôle via une adresse IP affectée directement tooit, au lieu d’utiliser le cloud de hello service VIP :&lt;numéro de port&gt;, demander une ILPIP pour votre machine virtuelle ou instance de rôle.

* **FTP actif** -en affectant une tooa ILPIP machine virtuelle, il peut recevoir le trafic sur n’importe quel port. Points de terminaison ne sont pas requises pour hello le trafic tooreceive de machine virtuelle.  Pour plus d’informations sur le protocole de hello FTP, consultez (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [vue d’ensemble du protocole FTP].
* **IP sortante** - le trafic sortant en provenance de hello machine virtuelle est mappé toohello ILPIP en tant que source de hello et hello ILPIP identifie de façon unique les entités tooexternal hello machine virtuelle.

> [!NOTE]
> Bonjour précédentes, une adresse ILPIP a été référencé tooas une adresse IP (PIP) publique.
> 

## <a name="manage-an-ilpip-for-a-vm"></a>Gérer une adresse ILPIP pour une machine virtuelle
Bonjour tâches suivantes permettre de toocreate, affecter et supprimer ILPIPs à partir d’ordinateurs virtuels :

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a>Comment toorequest un ILPIP lors de la création d’ordinateurs virtuels à l’aide de PowerShell
Hello PowerShell script suivant crée un service cloud nommé *FTPService*, récupère une image à partir d’Azure, crée un ordinateur virtuel nommé *FTPInstance* à l’aide de l’image hello récupérée, définit hello VM toouse un ILPIP, et ajoute le nouveau service hello VM toohello :

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a>Comment tooretrieve les informations de ILPIP pour une machine virtuelle
tooview hello ILPIP concernant hello machine virtuelle créée avec le script précédent de hello, exécutez hello suivant de commande PowerShell et observer les valeurs hello pour *PublicIPAddress* et *PublicIPName*:

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

Sortie attendue :
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a>Comment tooremove un ILPIP à partir d’une machine virtuelle
tooremove hello ILPIP ajouté toohello machine virtuelle dans le script précédent hello, exécutez hello suivant de commande PowerShell :

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a>Comment tooadd un tooan ILPIP machine virtuelle existante
tooadd un toohello ILPIP machine virtuelle créée à l’aide du script hello précédente, exécutez hello de commande suivante :

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a>Gérer une adresse ILPIP pour une instance de rôle de services cloud

tooadd une instance de rôle Services de cloud computing de tooa ILPIP, hello complète comme suit :

1. Téléchargez le fichier .cscfg de hello pour service de cloud hello en effectuant hello étapes Bonjour [comment les Services de cloud computing tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) l’article.
2. Fichier .cscfg hello en ajoutant hello `InstanceAddress` élément. Hello exemple suivant ajoute une ILPIP nommé *MyPublicIP* tooa instance de rôle nommé *WebRole1*: 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. Télécharger le fichier .cscfg de hello pour service de cloud hello en effectuant hello étapes Bonjour [comment les Services de cloud computing tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) l’article.

## <a name="next-steps"></a>Étapes suivantes
* Comprendre comment [l’adressage IP](virtual-network-ip-addresses-overview-classic.md) fonctionne dans le modèle de déploiement classique hello.
* En savoir plus sur les [adresses IP réservées](virtual-networks-reserved-public-ip.md).
