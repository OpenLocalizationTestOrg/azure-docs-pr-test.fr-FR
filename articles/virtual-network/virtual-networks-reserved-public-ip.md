---
title: "aaaManage Azure réservée d’adresses IP (classiques) - PowerShell | Documents Microsoft"
description: "Comprendre les adresses IP réservées (classiques) et comment toomanage les à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a>Adresses IP réservées (Classic)

> [!div class="op_single_selector"]
> * [Portail Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interface de ligne de commande Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Modèle](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (classique)](virtual-networks-reserved-public-ip.md)

Il existe deux catégories d’adresses IP dans Azure, les réservées et les dynamiques. Les adresses IP publiques gérées par Azure sont dynamiques par défaut. Que signifie que hello adresse IP utilisée pour un service de cloud donné (VIP) ou un tooaccess une machine virtuelle ou instance de rôle directement (ILPIP) peut changer à partir de l’heure tootime, lorsque des ressources sont arrêter ou arrêtés (désallouées).

tooprevent les adresses IP à partir de la modification, vous pouvez réserver une adresse IP. Adresses IP réservées peuvent être utilisé uniquement comme une adresse IP virtuelle, vous être assuré de cette adresse IP de hello pour le service cloud hello reste hello identiques, même si les ressources sont arrêtés ou arrêtée (désallouée). En outre, vous pouvez convertir des adresses IP dynamiques existante utilisée comme adresse IP VIP tooa réservé.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment un statique publique IP adresse à l’aide de tooreserve hello [modèle de déploiement de gestionnaire de ressources](virtual-network-ip-addresses-overview-arm.md).

toolearn savoir plus sur IP adresses dans Azure, lisez hello [des adresses IP](virtual-network-ip-addresses-overview-classic.md) l’article.

## <a name="when-do-i-need-a-reserved-ip"></a>Quand ai-je besoin d’une adresse IP réservée ?
* **Vous souhaitez tooensure qui hello IP est réservée dans votre abonnement**. Si vous souhaitez tooreserve une adresse IP qui n’est pas libérée à partir de votre abonnement dans aucune circonstance, vous devez utiliser une adresse IP publique réservée.  
* **Vous souhaitez que votre toostay IP avec votre service cloud même à travers arrêté ou désalloué (machines virtuelles) d’état**. Si vous souhaitez que votre toobe service accessible à l’aide d’une adresse IP qui ne change pas, même lorsque le cloud de machines virtuelles dans hello service sont arrêtés ou l’arrêter (libéré).
* **Vous souhaitez que le trafic sortant d’Azure utilise une adresse IP prévisible de tooensure**. Vous avez peut-être votre local configuré le pare-feu tooallow uniquement le trafic d’adresses IP spécifiques. En réservant une adresse IP, vous connaissez l’adresse IP source hello d’adresses et n’avez pas besoin de tooupdate votre pare-feu règles en raison de la modification de tooan IP.

## <a name="faq"></a>Forum Aux Questions
1. Puis-je utiliser une adresse IP réservée pour tous les services Azure ? <br>
    Non. Les adresses IP réservées peuvent être utilisées uniquement pour les machines virtuelles et les rôles d'instance de service cloud exposés par une adresse IP virtuelle.
2. Combien d’adresses IP réservées puis-je avoir ? <br>
    Pour plus d’informations, consultez hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.
3. L’obtention d’adresses IP réservées est-elle payante ? <br>
    Parfois. Pour plus d’informations de tarification, consultez hello [détails de tarification de l’adresse IP réservée](http://go.microsoft.com/fwlink/?LinkID=398482) page.
4. Comment réserver une adresse IP ? <br>
    Vous pouvez utiliser PowerShell, hello [API REST de gestion Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), ou hello [portail Azure](https://portal.azure.com) tooreserve une adresse IP dans une région Azure. Une adresse IP réservée est associée tooyour abonnement.
5. Puis-je utiliser une adresse IP réservée avec des réseaux virtuels basés sur un groupe d'affinités ? <br>
    Non. Les adresses IP réservées sont uniquement prises en charge dans les réseaux virtuels régionaux. Les adresses IP réservées ne sont pas prises en charge dans les réseaux virtuels associés à des groupes d’affinités. Pour plus d’informations sur l’association d’un réseau virtuel avec une région ou un groupe d’affinités, consultez hello [sur des réseaux virtuels régionaux et des groupes d’affinités](virtual-networks-migrate-to-regional-vnet.md) l’article.

## <a name="manage-reserved-vips"></a>Gérer les adresses IP virtuelles réservées

Assurez-vous d’avoir installé et configuré PowerShell en effectuant les étapes hello Bonjour [installer et configurer PowerShell](/powershell/azure/overview) l’article. 

Avant de pouvoir utiliser des adresses IP réservées, vous devez l’ajouter tooyour abonnement. toocreate une adresse IP réservée à partir du pool hello de l’adresse IP publique adresses disponibles dans hello *du centre des États-Unis* emplacement, exécutez hello de commande suivante :

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

Toutefois, veuillez noter que vous ne pouvez pas spécifier quelle adresse IP vous souhaitez réserver. tooview quelles sont les adresses IP sont réservées dans votre abonnement, exécutez hello suivant de commande PowerShell et notez les valeurs hello pour *ReservedIPName* et *adresse*:

```powershell
Get-AzureReservedIP
```

Sortie attendue :

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
>Lorsque vous créez une adresse IP réservée avec PowerShell, vous ne pouvez pas spécifier une groupe ressource toocreate adresse IP hello réservé dans. Azure place automatiquement cette adresse dans un groupe de ressources nommé *Default-Networking*. Si vous créez IP hello réservé à l’aide de hello [portail Azure](http://portal.azure.com), vous pouvez spécifier n’importe quel groupe de ressources que vous choisissez. Si vous créez hello réservée IP dans un groupe de ressources autre que *réseau par défaut* Toutefois, chaque fois que vous référencez hello IP réservée avec les commandes telles que `Get-AzureReservedIP` et `Remove-AzureReservedIP`, vous devez référencer le nom hello *-Nom d’ip réservée nom du groupe de ressources du groupe*.  Par exemple, si vous créez une adresse IP réservée nommée *myReservedIP* dans un groupe de ressources nommé *myResourceGroup*, vous devez référencer le nom hello de l’adresse IP hello réservé en tant que *myResourceGroup de groupe myReservedIP*.   

Une fois qu’une adresse IP est réservée, il reste associé tooyour abonnement jusqu'à ce que vous la supprimiez. toodelete une adresse IP réservée, hello exécution suivant de commande PowerShell :

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a>Réserver l’adresse IP de hello d’un service cloud existant
Vous pouvez réserver l’adresse IP de hello d’un service cloud existant en ajoutant hello `-ServiceName` paramètre. adresse tooreserve hello d’un service cloud *TestService* Bonjour *du centre des États-Unis* emplacement, exécutez hello suivant de commande PowerShell :

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a>Associer un réservée IP tooa nouveau service cloud
Hello script suivant crée une adresse IP réservée de nouveau, puis il associe le nouveau service de cloud tooa nommé *TestService*.

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> Lorsque vous créez un toouse IP réservée avec un service cloud, vous consultez toujours toohello machine virtuelle à l’aide de *VIP :&lt;numéro de port >* pour les communications entrantes. Réserver une adresse IP ne signifie pas que vous pouvez connecter directement toohello machine virtuelle. Hello IP réservée est affectée toohello cloud service ce hello machine virtuelle a été déployée. Si vous souhaitez tooconnect tooa VM par IP directement, vous avez tooconfigure une adresse IP publique de niveau de l’instance. Une adresse IP publique de niveau de l’instance est un type d’adresse IP publique (appelé un ILPIP) qui est directement affectée tooyour machine virtuelle. Elle ne peut pas être réservée. Pour plus d’informations, consultez hello [IP publique de niveau de l’Instance (ILPIP)](virtual-networks-instance-level-public-ip.md) l’article.
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a>Supprimer une adresse IP réservée d’un déploiement en cours d’exécution
tooremove une adresse IP réservée ajouté un nouveau service de cloud tooa, exécutez hello suivant de commande PowerShell :

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> Suppression d’une adresse IP réservée à partir d’un déploiement en cours d’exécution ne supprime pas de réservation de hello à partir de votre abonnement. Elle libère simplement hello IP toobe est utilisé par une autre ressource dans votre abonnement.
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a>Associer un tooa IP réservée déploiement en cours d’exécution
Hello commandes suivantes créent un service cloud nommé *TestService2* avec un nouvel ordinateur virtuel nommé *TestVM2*. Hello existant réservée IP nommé *MyReservedIP* est ensuite le service de cloud computing toohello associé.

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a>Associer un service de cloud tooa IP réservé à l’aide d’un fichier de configuration de service
Vous pouvez également associer un service de cloud tooa IP réservé à l’aide d’un fichier de configuration (CSCFG) du service. Hello exemple de code xml suivant montre comment tooconfigure un toouse de service cloud une adresse IP virtuelle réservée nommée *MyReservedIP*:

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a>Étapes suivantes
* Comprendre comment [l’adressage IP](virtual-network-ip-addresses-overview-classic.md) fonctionne dans le modèle de déploiement classique hello.
* En savoir plus sur [les adresses IP privées réservées](virtual-networks-reserved-private-ip.md).
* En savoir plus sur [les adresses IP publiques de niveau d’instance (ILPIP)](virtual-networks-instance-level-public-ip.md).

