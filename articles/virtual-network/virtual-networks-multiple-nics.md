---
title: "aaaCreate une machine virtuelle (classique) avec plusieurs cartes réseau à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate et configurer des machines virtuelles avec plusieurs cartes réseau à l’aide de PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a>Créer une machine virtuelle (classique) avec plusieurs cartes réseau
Vous pouvez créer des machines virtuelles (VM) dans Azure et attacher plusieurs tooeach de cartes réseau de vos ordinateurs virtuels. Il s’agit d’une exigence pour de nombreuses appliances virtuelles réseau, comme les solutions de distribution d’applications et d’optimisation de réseau étendu (WAN). La présence de plusieurs cartes réseau assure aussi une isolation du trafic entre les cartes réseau.

![Fonctionnalité Multi-NIC pour machine virtuelle](./media/virtual-networks-multiple-nics/IC757773.png)

Hello figure illustre une machine virtuelle avec trois cartes réseau, chacun connecté tooa autre sous-réseau.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser Resource Manager.

* Adresse IP virtuelle sur Internet (déploiements classiques) est uniquement pris en charge sur hello, « default » NIC. Il est IP de toohello qu’une seule adresse IP virtuelle de NIC hello par défaut.
* Pour l’instant, les adresses IP publiques de niveau d’instance (LPIP) (déploiements classiques) ne sont pas prises en charge pour les machines virtuelles à plusieurs NIC.
* Hello ordre des NIC hello à l’intérieur de hello machine virtuelle est aléatoire et peut également changer entre les mises à jour de l’infrastructure Azure. Toutefois, hello des adresses IP et hello correspondant ethernet MAC adresses resteront identiques hello. Par exemple, supposons que **Eth1** a l’adresse IP 10.1.0.100 et une adresse MAC 00-0D-3A-B0-39-0D ; après une mise à jour de l’infrastructure Azure et un redémarrage, il peut être modifié trop**Eth2**, mais hello IP et MAC appariement va restent identiques hello. Lorsqu’un redémarrage est lancée par le client, hello ordre des NIC reste identique hello.
* Hello adresse pour chaque carte réseau sur chaque machine virtuelle doit se trouver dans un sous-réseau, plusieurs cartes réseau sur un seul ordinateur virtuel peut chacun avoir des adresses qui se trouvent dans hello même sous-réseau.
* Hello taille de machine virtuelle détermine le nombre de hello de cartes réseau que vous pouvez créer pour une machine virtuelle. Hello de référence [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) combien de cartes réseau prend en charge la taille de chaque machine virtuelle articles toodetermine des tailles de machine virtuelle. 

## <a name="network-security-groups-nsgs"></a>Groupes de sécurité réseau (NSG)
Dans un déploiement avec gestionnaire de ressources, les NIC d’une machine virtuelle peuvent être associées à un groupe de sécurité réseau (NSG), y compris les NIC d’une machine virtuelle sur laquelle la fonctionnalité Multi-NIC est activée. Si une adresse dans un sous-réseau dans lequel le sous-réseau de hello est associé à un groupe de sécurité réseau est assignée à une carte réseau, puis hello règles dans le groupe de sécurité réseau du sous-réseau hello s’appliquent également toothat carte Dans des sous-réseaux tooassociating addition avec des groupes de sécurité réseau, vous pouvez également associer une carte réseau avec un groupe de sécurité réseau.

Si un sous-réseau est associé à un groupe de sécurité réseau et une carte réseau au sein de ce sous-réseau est individuellement associé à un groupe de sécurité réseau, les règles de groupe de sécurité réseau hello associée sont appliquées dans **flux ordre** selon la direction de toohello du trafic de hello transmis vers ou depuis Hello carte réseau :

* **Le trafic entrant** sous-réseau hello, déclencher des règles de groupe de sécurité réseau du sous-réseau hello, avant de passer dans hello carte réseau, puis déclencher des règles de groupe de sécurité réseau hello carte d’interface réseau dont la destination est hello NIC en question parcourt tout d’abord.
* **Le trafic sortant** dont la source est hello NIC en question flux premier sorti de hello NIC, déclencher des règles de groupe de sécurité réseau hello carte d’interface réseau, avant de passer par le sous-réseau de hello, puis déclencher des règles de groupe de sécurité réseau du sous-réseau hello.

En savoir plus sur [groupes de sécurité réseau](virtual-networks-nsg.md) et comment elles sont appliquées selon les associations toosubnets, les machines virtuelles et les cartes réseau...

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a>Comment tooConfigure un plusieurs NIC VM dans un déploiement classique
instructions Hello ci-dessous vous aide à créer un multi VM NIC contenant 3 NIC : une carte réseau par défaut et deux cartes réseau supplémentaires. étapes de configuration Hello va créer une machine virtuelle qui est configurée en fonction de fragment de fichier de configuration d’un service de toohello ci-dessous :

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


Vous devez hello suivant des conditions préalables avant d’essayer de commandes PowerShell hello exemple toorun hello.

* Un abonnement Azure.
* Un réseau virtuel configuré. Pour plus d’informations sur les réseaux virtuels, voir l’article [Présentation du réseau virtuel](virtual-networks-overview.md) .
* version la plus récente d’Azure PowerShell Hello téléchargé et installé. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

toocreate une machine virtuelle avec plusieurs cartes réseau, hello complète à l’aide de chaque commande dans une session PowerShell unique comme suit :

1. Sélectionnez une image de machine virtuelle dans la galerie d’images de machine virtuelle Azure. Notez que les images changent fréquemment et sont disponibles par région. Hello image spécifiée dans l’exemple hello ci-dessous peut modifier ou peut pas se trouver dans votre région, veillez donc à image de hello toospecify vous avez besoin.

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. Créez une configuration de machine virtuelle.

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. Créer la connexion de l’administrateur par défaut hello.

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. Ajouter la configuration de machine virtuelle toohello cartes réseau supplémentaires.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. Spécifiez le sous-réseau de hello et l’adresse IP pour NIC hello par défaut.

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. Créez hello machine virtuelle dans votre réseau virtuel.

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > Hello réseau virtuel que vous spécifiez ici doit déjà exister (comme indiqué dans les conditions préalables de hello). exemple Hello ci-dessous spécifie un réseau virtuel nommé **MultiNIC-VNet**.
    >

## <a name="limitations"></a>Limites
Hello limites suivantes s’appliquent lors de l’utilisation de plusieurs cartes réseau :

* Les machines virtuelles à plusieurs cartes réseau doivent être créées dans des réseaux virtuels Azure. Les machines virtuelles n’appartenant pas à un réseau virtuel ne peuvent pas être configurées avec plusieurs cartes réseau.
* Tous les ordinateurs virtuels d’un groupe défini besoin toouse plusieurs cartes réseau ou une carte réseau. unique La cohabitation entre des machines virtuelles à plusieurs cartes réseau et des machines virtuelles à une seule carte réseau n’est pas possible au sein d’un groupe à haute disponibilité. Les mêmes règles s’appliquent pour les machines virtuelles dans un service cloud. Pour plusieurs machines virtuelles de carte réseau, ils ne sont pas indispensables toohave hello même nombre de cartes réseau, tant qu’ils ont chacun au moins deux.
* Une machine virtuelle à une seule carte réseau ne peut pas être configurée avec plusieurs cartes réseau (et inversement) une fois qu’elle est déployée. Il faut la supprimer et la recréer.

## <a name="secondary-nics-access-tooother-subnets"></a>Cartes d’interface réseau secondaire accéder aux sous-réseaux de tooother
Par défaut de cartes d’interface réseau secondaire ne seront pas configurés avec une passerelle par défaut, en raison de flux de trafic toowhich hello sur hello NIC secondaire sera limité toobe dans hello même sous-réseau. Si les utilisateurs de hello souhaitent tooenable tootalk de cartes d’interface réseau secondaire à l’extérieur de leur propre sous-réseau, ils devront tooadd une entrée dans hello table tooconfigure hello passerelle de routage comme décrit ci-dessous.

> [!NOTE]
> Les machines virtuelles créées avant juillet 2015 peuvent avoir une passerelle par défaut configurée pour toutes les cartes réseau. passerelle par défaut de Hello pour les cartes réseau secondaire n’est pas supprimé jusqu'à ce que ces machines virtuelles sont redémarrés. Dans les systèmes d’exploitation qui utilisent le modèle de routage d’hôte faible hello, tels que Linux, une connectivité Internet peut cesser de fonctionner si le trafic entrant et sortant hello utilise différentes cartes réseau.
> 

### <a name="configure-windows-vms"></a>Configurer les machines virtuelles Windows
Supposons que vous disposiez d’une machine virtuelle Windows avec deux cartes réseau, comme suit :

* Adresse IP de la carte réseau principale : 192.168.1.4
* Adresse IP de la carte réseau secondaire : 192.168.2.5

table de routage IPv4 Hello pour cet ordinateur virtuel ressemble à ceci :

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

Notez que cet itinéraire par défaut de hello (0.0.0.0) est uniquement une carte principal toohello disponibles Vous ne serez pas tooaccess en mesure des ressources à l’extérieur du sous-réseau hello pour hello secondaire carte réseau, comme indiqué ci-dessous :

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

tooadd un itinéraire par défaut sur hello NIC secondaire, hello suivez les étapes ci-dessous :

1. À partir d’une invite de commandes, exécuter la commande hello ci-dessous le numéro d’index tooidentify hello pour hello NIC secondaire :
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. Notez la deuxième entrée de hello dans la table hello, avec un index de 27 (dans cet exemple).
3. À partir de l’invite de commandes hello, exécutez hello **itinéraire ajouter** commande comme indiqué ci-dessous. Dans cet exemple, vous spécifiez 192.168.2.1 en tant que passerelle par défaut de hello pour hello NIC secondaire :
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. tootest connectivité, invite de commandes toohello revenir en arrière et essayez tooping un sous-réseau différent de celui hello NIC secondaire en tant qu’int indiqué eh exemple ci-dessous :
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. Vous pouvez également vérifier votre hello toocheck de table itinéraire récemment ajouté itinéraire, comme indiqué ci-dessous :
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a>Configurer des machines virtuelles Linux
Pour les machines virtuelles Linux, par défaut hello utilise hôte faible routage, il est recommandé que hello NIC secondaire sont des flux tootraffic restreint uniquement dans hello même sous-réseau. Toutefois si certains scénarios exigent de connectivité en dehors du sous-réseau de hello, les utilisateurs doivent activer tooensure de routage basée sur la stratégie qui hello en entrée et sortie trafic utilise hello même carte réseau.

## <a name="next-steps"></a>Étapes suivantes
* Déploiement de [machines virtuelles MultiNIC dans un scénario d’application à 2 niveaux pour un déploiement Resource Manager](virtual-network-deploy-multinic-arm-template.md).
* Déploiement de [machines virtuelles MultiNIC dans un scénario d’application à 2 niveaux pour un déploiement classique](virtual-network-deploy-multinic-classic-ps.md).

