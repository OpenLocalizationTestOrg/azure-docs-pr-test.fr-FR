---
title: "aaaPlan mise en réseau pour Hyper-V réplication tooa site VMM secondaire avec Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit la planification d’un réseau lors de la réplication de site secondaire System Center VMM des ordinateurs virtuels Hyper-V tooa avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Étape 3 : Planifier la mise en réseau pour le site VMM secondaire de machine virtuelle Hyper-V réplication tooa

Après avoir examiné les conditions préalables au déploiement, lisez cette tooplan article lors de la réplication Hyper-V virtual machines virtuelles gérées dans des clouds de System Center Virtual Machine Manager (VMM), la mise en réseau à l’aide du site secondaire tooa [Azure Site Recovery](site-recovery-overview.md) Bonjour portail Azure. 

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-overview"></a>Vue d’ensemble du mappage réseau

Le mappage réseau est utilisé pour répliquer des machines virtuelles de Hyper-V (géré dans VMM) tooa centre de données secondaire. Le mappage réseau opère entre des réseaux de machines virtuelles sur un serveur VMM source et des réseaux de machines virtuelles sur un serveur VMM cible. Mappage hello suivant :

- **Connexion réseau**, réseaux de tooappropriate se connecte les machines virtuelles après le basculement. ordinateur virtuel de réplication Hello sera réseau connecté toohello cible qui est mappé toohello source réseau.
- **Placement optimal**: pas de façon optimale les endroits hello machines virtuelles de réplication sur les serveurs hôtes Hyper-V. Machines virtuelles de réplication sont placées sur des hôtes auxquels peuvent hello d’accès mappées réseaux d’ordinateurs virtuels.
- **Aucun mappage de réseau**: Si vous ne configurez pas le mappage réseau, machines virtuelles de réplica sera connecté tooany réseaux d’ordinateurs virtuels après le basculement.


### <a name="example"></a>Exemple

Voici un exemple tooillustrate ce mécanisme. Prenons l’exemple d’une entreprise ayant ouvert deux bureaux, l’un à New York et l’autre à Chicago.

**Emplacement** | **Serveur VMM** | **Réseaux de machines virtuelles** | **Mappés à**
---|---|---|---
New York | VMM-NewYork| VMNetwork1-NewYork | Mappé tooVMNetwork1-Chicago
 |  | VMNetwork2-NewYork | Non mappé
Chicago | VMM-Chicago| VMNetwork1-Chicago | TooVMNetwork1-NewYork mappé
 | | VMNetwork1-Chicago | Non mappé

Dans cet exemple :

- Lorsqu’un ordinateur virtuel est créé pour un ordinateur virtuel qui est connecté tooVMNetwork1-NewYork, il sera connecté tooVMNetwork1-Chicago.
- Lorsqu’un ordinateur virtuel est créé pour VMNetwork2-NewYork ou VMNetwork2-Chicago, il ne sera pas connectée tooany réseau.

Voici la façon dont les clouds VMM sont configurés dans notre exemple d’organisation et les réseaux logiques hello associées aux clouds de hello.

#### <a name="cloud-protection-settings"></a>Paramètres de protection des clouds

**Cloud protégé** | **Cloud de protection** | **Réseau logique (New York)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>N/D</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>
SilverCloud2 | <p>N/D</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>Paramètres des réseaux de machines virtuelles et des réseaux logiques

**Emplacement** | **Réseau logique** | **Réseau de machines virtuelles associé**
---|---|---
New York | LogicalNetwork1-NewYork | VMNetwork1-NewYork
Chicago | LogicalNetwork1-Chicago | VMNetwork1-Chicago
 | LogicalNetwork2Chicago | VMNetwork2-Chicago

#### <a name="target-network-settings"></a>Paramètres de réseau cible

Selon ces paramètres, lorsque vous sélectionnez le réseau d’ordinateurs virtuels hello cible, hello tableau suivant affiche les options de hello qui seront disponibles.

**Sélection** | **Cloud protégé** | **Cloud de protection** | **Réseau cible disponible**
---|---|---|---
VMNetwork1-Chicago | SilverCloud1 | SilverCloud2 | Disponible
 | GoldCloud1 | GoldCloud2 | Disponible
VMNetwork2-Chicago | SilverCloud1 | SilverCloud2 | Non disponible
 | GoldCloud1 | GoldCloud2 | Disponible


Si le réseau cible de hello a plusieurs sous-réseaux et de ces sous-réseaux a hello même nom comme hello sous-réseau sur quel hello ordinateur virtuel source se trouve, puis hello machine virtuelle de réplication sera connectée toothat cible sous-réseau après le basculement. S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.


#### <a name="failback-behavior"></a>Comportement de restauration automatique

toosee que se passe-t-il en cas de hello de la restauration automatique (réplication inverse), supposons que VMNetwork1-NewYork est mappé tooVMNetwork1-Chicago, avec hello suivant les paramètres.


**Machine virtuelle** | **Réseau de tooVM connecté**
---|---
MV1 | VMNetwork1-Network
VM2 (réplica de VM1) | VMNetwork1-Chicago

Examinons ce qui se passe dans différents scénarios possibles avec ces paramètres.

**Scénario** | **Résultat**
---|---
Aucune modification dans les propriétés du réseau hello de VM-2 après le basculement. | VM-1 reste connecté toohello source réseau.
Les propriétés du réseau de la machine VM2 sont modifiées après le basculement ; la machine est déconnectée. | La machine VM1 est déconnectée.
Propriétés réseau de VM-2 sont modifiées après basculement et sont connecté tooVMNetwork2-Chicago. | Si le réseau VMNetwork2-Chicago n’est pas mappé, la machine VM1 est déconnectée.
Le mappage réseau de VMNetwork1-Chicago est modifié. | VM-1 sera connecté toohello réseau mappé tooVMNetwork1-Chicago.



## <a name="prepare-for-network-mapping"></a>Préparer le mappage réseau

1. Sur hello source et cible VMM des serveurs, vous devez disposer d’un réseau logique associé aux clouds source et cible de hello. 
2. Dans les serveurs source et cible de hello, vous devez disposer d’un réseau logique de machine virtuelle réseau toohello lié.
3. Machines virtuelles sur les hôtes Hyper-V dans un emplacement de source de hello doivent être le réseau d’ordinateurs virtuels lié toohello source. Si vous utilisez uniquement un seul serveur VMM, vous pouvez configurer le mappage entre les réseaux d’ordinateurs virtuels sur hello même serveur.

Voici ce qui se passe lorsque vous configurez le mappage réseau lors du déploiement de Site Recovery :

- Lorsque vous définissez le mappage réseau et que vous sélectionnez un réseau de machines virtuelles cible, les clouds sources hello VMM qui utilisent le réseau d’ordinateurs virtuels hello source seront affichera, ainsi que les réseaux d’ordinateurs virtuels hello cibles disponibles sur les clouds cibles hello.
- - Lorsque le mappage est correctement configuré la réplication est activée, un ordinateur virtuel source seront réseau d’ordinateurs virtuels connectés tooits source et son réplica dans l’emplacement cible de hello sera connecté tooits mappé réseau d’ordinateurs virtuels.
- Si le réseau cible de hello possède plusieurs sous-réseaux et un de ces sous-réseaux hello même nom comme hello sous-réseau sur quel hello ordinateur virtuel source se trouve, puis hello machine virtuelle de réplication sera connectée toothat cible sous-réseau après le basculement. S’il n’existe aucun sous-réseau cible avec un nom correspondant, hello machine virtuelle sera connectée toohello premier sous-réseau de réseau de hello.

## <a name="connect-toovms-after-failover"></a>Se connecter tooVMs après le basculement

Lorsque vous planifiez votre stratégie de basculement et de réplication, une des questions clés de hello est comment réplica de toohello tooconnect après le basculement. Vous disposez de deux options : 

- **Utiliser une autre adresse IP**: vous pouvez sélectionner toouse une adresse IP différente pour hello répliquées de machine virtuelle. Dans cette hello scénario VM Obtient une nouvelle adresse IP après un basculement, et une mise à jour DNS est requis.
- **Conserver hello la même adresse IP**: vous souhaiterez peut-être toouse hello la même adresse IP pour l’ordinateur virtuel de réplication hello. Hello conserver des adresses IP mêmes simplifie la récupération hello en réduisant les problèmes de réseau après le basculement. 

## <a name="retain-ip-addresses"></a>Conserver les adresses IP

Si vous souhaitez que les adresses IP de hello tooretain à partir du site principal de hello après le site secondaire de basculement toohello, vous pouvez effectuer un basculement de sous-réseau complet et mettre à jour des itinéraires tooindicate hello nouvel emplacement d’adresses IP de hello ou alternative déployer un sous-réseau étendu entre hello principal et hello sites de récupération.

### <a name="stretched-subnet"></a>Sous-réseau étiré

Dans un sous-réseau étendu hello sous-réseau est disponible simultanément dans les deux sites principaux et secondaires de hello. Si vous déplacez un serveur et son site secondaire de IP (couche 3) configuration toohello, réseau de hello acheminer nouvel emplacement hello trafic toohello automatiquement. 

En ce qui concerne la couche 2 (couche de liaison de données), vous devez disposer d’un équipement réseau qui peut gérer un VLAN étiré. En outre, par étirement hello VLAN, domaine d’erreur potentielles hello étend sites tooboth, essentiellement devient un point de défaillance unique. Bien que cela soit peu probable, il est possible qu’une tempête de diffusion commence sans pouvoir être isolée. 


### <a name="subnet-failover"></a>Basculement de sous-réseau

Vous pouvez exécuter un Bonjour de tooobtain de basculement de sous-réseau avantages du sous-réseau de hello étirée, sans réellement l’étirement. Dans cette solution, un sous-réseau sera disponible dans le site source ou cible de hello, mais pas les deux simultanément. toomaintain hello espace d’adressage IP dans les événements hello d’un basculement, vous pouvez organiser par programme des sous-réseaux de hello hello routeur infrastructure toomove à partir d’un site tooanother. Après basculement, déplacer des sous-réseaux avec hello associés des machines virtuelles. Hello principal inconvénient est que dans l’événement hello d’une défaillance, vous disposez de sous-réseau entier de toomove hello.

### <a name="example"></a>Exemple

Voici un exemple de basculement de sous-réseau complet. site principal de Hello possède des applications en cours d’exécution dans le sous-réseau 192.168.1.0/24. Lors du basculement, hello toutes les machines virtuelles dans ce sous-réseau ont échoué sur le site secondaire de toohello et conservent leurs adresses IP. Itinéraires besoin toobe modifié fait de hello tooreflect que tous les ordinateurs virtuels VM hello appartenant toosubnet 192.168.1.0/24 ont été déplacés de site secondaire de toohello.

Hello graphiques suivants illustrent les sous-réseaux hello avant et après le basculement :

- Avant le basculement, sous-réseau 192.168.0.1/24 est actif sur le site source de hello, devient active sur le site secondaire de hello après le basculement.
- Hello achemine entre le site principal et le site de récupération, site tiers et site principal et site tiers et le site de récupération aura toobe modifiée en conséquence.

**Avant le basculement**

![Avant le basculement](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**Après le basculement**

![Après le basculement](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

Voici ce qui se passe après le basculement :

- Récupération de site alloue une adresse IP pour chaque interface réseau sur hello machine virtuelle, à partir de hello pool d’adresses IP de réseau appropriées hello, pour chaque instance VMM.
- Si le pool d’adresses IP hello dans le site secondaire de hello est hello alloue de la même que celle sur le site source de hello, Site Recovery hello même IP adresse (de la machine virtuelle de la source hello) toohello ordinateur virtuel de réplication. adresse IP de Hello est réservé dans VMM, mais il n’est pas défini comme adresse IP de basculement hello sur l’ordinateur hôte Hyper-V de hello. adresse IP de basculement Hello sur un ordinateur hôte Hyper-v est définie juste avant le basculement de hello.
- Hello même adresse IP n’est pas disponible, Site Recovery alloue une autre adresse IP disponible à partir du pool de hello.
- Si les machines virtuelles utilisent DHCP, Site Recovery ne gère pas les adresses IP hello. Vous devez toocheck qui hello DHCP server sur le site secondaire de hello peut allouer une adresse à partir de la même plage comme site source de hello de hello.

### <a name="validate-hello-ip-address"></a>Valider l’adresse IP de hello

Une fois que vous activez la protection d’un ordinateur virtuel, vous pouvez utiliser suivants exemple script tooverify hello adresse affectée toohello machine virtuelle. Hello même adresse IP est définie en tant qu’adresse IP de basculement hello et affecté toohello machine virtuelle au moment de hello de basculement :

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>Modifier les adresses IP

Dans ce scénario, les adresses IP de hello de machines virtuelles qui basculent sont modifiés. Hello inconvénient de cette solution est maintenance hello requis. En règle générale, DNS sera mis à jour après le démarrage des machines virtuelles de réplica. Les entrées DNS deviez toobe modifiée ou fluster dans réseau fonctionnant et les entrées mises en cache mis à jour. Cela peut entraîner un temps d’arrêt. Le temps d’arrêt peut être atténué comme suit :

- Utilisez des valeurs TTL faibles pour les applications intranet.
- Utiliser le script suivant dans un plan de récupération de Site Recovery, tooupdate hello DNS server tooensure une mise à jour en temps voulu de hello. Vous n’avez pas besoin script de hello si vous utilisez l’inscription DNS dynamique.

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a>Exemple 

Examinons un scénario dans lequel vous avez l’intention toouse différentes adresses IP entre hello principal et les sites de récupération hello. Dans cet exemple, nous avons différentes adresses IP entre les sites principaux et secondaires, et il ; s une troisième les applications hébergées sur le site principal ou de récupération de hello est accessible.

- Avant le basculement, les applications sont 192.168.1.0/24 sous-réseau hébergé sur le site principal de hello et sont configuré toobe dans 172.16.1.0/24 sous-réseau sur le site secondaire de hello après un basculement.
- Les itinéraires du réseau/des connexions VPN ont été correctement configurés pour que les trois sites puissent accéder l’un à l'autre.
- Après le basculement, les applications seront restaurées dans un sous-réseau de récupération hello. Dans ce cas il n’y a aucune toofail besoin sur sous-réseau en entier hello et aucune modification n’est nécessaire tooreconfigure les itinéraires VPN ou réseau. basculement de Hello et certaines mises à jour DNS, assurent que les applications restent accessibles.
- Si DNS est configuré tooallow les mises à jour dynamiques, les machines virtuelles hello seront inscrivent eux-mêmes à l’aide de la nouvelle adresse d’IP hello, quand ils démarrent après le basculement.

**Avant le basculement**

![Autre adresse IP - avant le basculement](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**Après le basculement**

![Autre adresse IP - après le basculement](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 4 : préparer le VMM et Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).


