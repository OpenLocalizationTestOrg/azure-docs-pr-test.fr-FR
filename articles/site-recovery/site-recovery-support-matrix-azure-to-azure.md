---
title: "matrice de prise en charge aaaAzure Site Recovery pour la réplication à partir d’Azure tooAzure | Documents Microsoft"
description: "Résume hello pris en charge les systèmes d’exploitation et configurations pour la réplication de machines virtuelles (VM) Azure Site Recovery à partir de tooanother d’une région pour les besoins de reprise après sinistre."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: 75b2451b4c2069ca4b11deb0efe1329d43879eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-azure-tooazure"></a>Matrice de prise en charge Azure Site Recovery pour la réplication à partir d’Azure tooAzure


>[!NOTE]
>
> La réplication Site Recovery pour les machines virtuelles Azure est actuellement en préversion.

Cet article résume les composants et configurations prises en charge pour Azure Site Recovery lors de la réplication et la récupération des machines virtuelles à partir de la région de tooanother d’une région.

## <a name="user-interface-options"></a>Options d’interface utilisateur

**Interface utilisateur** |  **Prise en charge / Non prise en charge**
--- | ---
**Portail Azure** | Pris en charge
**Portail Classic** | Non pris en charge
**PowerShell** | Non pris en charge pour le moment
**API REST** | Non prise en charge pour le moment
**INTERFACE DE LIGNE DE COMMANDE** | Non prise en charge pour le moment


## <a name="resource-move-support"></a>Prise en charge du déplacement de ressources

**Type de déplacement de ressources** | **Pris en charge / Non pris en charge** | **Notes**  
--- | --- | ---
**Déplacer le coffre entre plusieurs groupes de ressources** | Non pris en charge |Vous ne pouvez pas déplacer le coffre hello Recovery services plusieurs groupes de ressources.
**Déplacer le calcul, le stockage et le réseau entre plusieurs groupes de ressources** | Non pris en charge |Si vous déplacez un ordinateur virtuel (ou ses composants associés, tels que le réseau et stockage) après l’activation de la réplication, vous devez toodisable la réplication et activez la réplication pour la machine virtuelle de hello à nouveau.


## <a name="support-for-deployment-models"></a>Prise en charge des modèles de déploiement

**Modèle de déploiement** | **Pris en charge / Non pris en charge** | **Notes**  
--- | --- | ---
**Classique** | Pris en charge | Vous pouvez uniquement répliquer une machine virtuelle classique et la récupérer en tant que machine virtuelle classique. Vous ne pouvez pas la récupérer en tant que machine virtuelle Resource Manager. Si vous déployez un ordinateur classique virtuel sans un réseau virtuel et directement tooan région Azure, il n’est pas pris en charge.
**Gestionnaire de ressources** | Pris en charge |

## <a name="support-for-replicated-machine-os-versions"></a>Prise en charge des versions de système d’exploitation de machine répliquée

Hello ci-dessous prise en charge n’est applicable à toute charge de travail en cours d’exécution sur hello mentionné du système d’exploitation.

#### <a name="windows"></a>Windows

- Windows Server 2016 (Server Core et Server avec Expérience utilisateur)*
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 avec au moins SP1

>[!NOTE]
>
> \* Windows Server 2016 Nano Server n’est pas pris en charge.

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 6.7, 6.8, 7.0, 7.1, 7.2, 7.3
- CentOS 6.5, 6.6, 6.7, 6.8, 7.0, 7.1, 7.2, 7.3
- Serveur LTS Ubuntu 14.04 [ (versions du noyau prises en charge)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Serveur LTS Ubuntu 16.04 [ (versions du noyau prises en charge)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Oracle Enterprise Linux 6.4, 6.5 exécutant noyau compatible de Red Hat hello ou insécable Enterprise noyau version 3 (UEK3)
- SUSE Linux Enterprise Server 11 SP3

>[!NOTE]
>
> Serveurs Ubuntu à l’aide du mot de passe authentification et connexion et à l’aide de machines virtuelles de hello cloud-init package tooconfigure cloud, peut avoir un mot de passe connexion désactivée lors du basculement (selon la configuration de cloudinit hello.) Compte de connexion en fonction de mot de passe peut être réactivée sur l’ordinateur virtuel de hello en réinitialisant le mot de passe hello dans menu des paramètres de hello (sous hello prise en charge + dépannage) de hello a échoué sur l’ordinateur virtuel sur hello portail Azure.

### <a name="supported-ubuntu-kernel-versions-for-azure-virtual-machines"></a>Versions du noyau Ubuntu prises en charge pour les machines virtuelles Azure

**Version release** | **Version du service Mobilité** | **Version du noyau** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0-117-générique<br/>3.16.0-25-Generic too3.16.0-77-générique<br/>3.19.0-18-Generic too3.19.0-80-générique<br/>4.2.0-18-Generic too4.2.0-42-générique<br/>4.4.0-21-Generic too4.4.0 75-générique |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0 121-générique,<br/>3.16.0-25-Generic too3.16.0-77-générique<br/>3.19.0-18-Generic too3.19.0-80-générique<br/>4.2.0-18-Generic too4.2.0-42-générique<br/>4.4.0-21-Generic too4.4.0 81-générique |
LTS 16.04 | 9.10 | 4.4.0-21-Generic too4.4.0-81-générique<br/>4.8.0-34-Generic too4.8.0-56-générique<br/>4.10.0-14-Generic too4.10.0-24-générique |

## <a name="supported-file-systems-and-guest-storage-configurations-on-azure-virtual-machines-running-linux-os"></a>Systèmes de fichiers et configurations de stockage invité pris en charge sur les machines virtuelles Azure exécutant le système d’exploitation Linux

* Systèmes de fichiers : ext3, ext4, ReiserFS (Suse Linux Enterprise Server uniquement), XFS
* Gestionnaire de volume : LVM2
* Logiciel multichemin : Device Mapper

## <a name="region-support"></a>Prise en charge de la région

Vous pouvez répliquer et récupérer des ordinateurs virtuels entre les deux régions dans hello même cluster géographique.

**Cluster géographique** | **Régions Azure**
-- | --
Amérique | Canada de l’Est, Canada du Centre, Sud du Centre des États-Unis, Ouest du Centre des États-Unis, États-Unis de l’Est, États-Unis de l’Est 2, États-Unis de l’Ouest, États-Unis de l’Ouest 2, États-Unis du Centre, Nord du Centre des États-Unis
Europe | Ouest du Royaume-Uni, Sud du Royaume-Uni, Europe du Nord, Europe de l’Ouest
Asie | Inde du Sud, Centre de l’Inde, Asie du Sud-Est, Asie de l’Est, Japon de l’Est, Japon de l’Ouest, Centre de la Corée, Corée du Sud
Australie   | Est de l’Australie, Sud-Est de l’Australie

>[!NOTE]
>
> Pour la région Sud du Brésil, vous pouvez répliquer uniquement et tooone de basculement de l’Amérique du Sud, ouest des États-Unis, est des États-Unis, est des États-Unis 2, ouest des États-Unis, ouest des États-Unis 2 et régions Amérique du Nord et échouent sauvegarder.


## <a name="support-for-compute-configuration"></a>Prise en charge de la configuration de calcul

**Configuration** | **Prise en charge/Non prise en charge** | **Notes**
--- | --- | ---
Taille | N’importe quelle taille de machine virtuelle Azure avec au moins deux cœurs d’UC et 1 Go de RAM | Consultez trop[tailles de machine virtuelle Azure](../virtual-machines/windows/sizes.md)
Groupes à haute disponibilité | Pris en charge | Si vous utilisez l’option par défaut de hello pendant l’activation de la réplication dans le portail, hello à haute disponibilité est automatiquement créé en fonction de la configuration de la zone source. Vous pouvez modifier la disponibilité de cible hello définie dans ' répliqué élément > Paramètres > calcul et réseau > haute disponibilité ' tout moment.
Machines virtuelles HUB (Hybrid Use Benefit) | Pris en charge | Si machine virtuelle de la source hello a licence HUB activé, hello Test de basculement ou Failover VM utilise également les licences de concentrateur hello.
Groupes identiques de machines virtuelles  | Non pris en charge |
Images de la galerie Azure publiées par Microsoft | Pris en charge | Prise en charge tant que hello machine virtuelle s’exécute sur un système d’exploitation pris en charge par la récupération de Site
Images de la galerie Azure publiées par un tiers | Pris en charge | Cette prise en charge tant que hello machine virtuelle s’exécute sur un système d’exploitation pris en charge par la récupération de Site.
Images personnalisées publiées par un tiers | Pris en charge | Cette prise en charge tant que hello machine virtuelle s’exécute sur un système d’exploitation pris en charge par la récupération de Site.
Machines virtuelles migrées à l’aide de Site Recovery | Pris en charge | Si elle est un ordinateur VMware/physiques migrés tooAzure à l’aide de la récupération de Site, vous devez toouninstall hello ancienne version du service mobilité et redémarrez l’ordinateur de hello avant de les répliquer tooanother région Azure.

## <a name="support-for-storage-configuration"></a>Prise en charge de la configuration de stockage

**Configuration** | **Prise en charge/Non prise en charge** | **Notes**
--- | --- | ---
Taille maximale du disque du système d’exploitation | 1 023 Go | Consultez trop[disques utilisés par les ordinateurs virtuels.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Taille maximale de disque de données | 1 023 Go | Consultez trop[disques utilisés par les ordinateurs virtuels.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Nombre de disques de données | Jusqu’à 64, tel que pris en charge par une taille spécifique de machine virtuelle Azure | Consultez trop[tailles de machine virtuelle Azure](../virtual-machines/windows/sizes.md)
Disque temporaire | Toujours exclus de la réplication | Le disque temporaire est exclu de la réplication. Dans les recommandations Azure, il est stipulé que vous ne devez pas placer de données persistantes sur un disque temporaire. Consultez trop[disque temporaire sur des machines virtuelles Azure](../virtual-machines/windows/about-disks-and-vhds.md#temporary-disk) pour plus d’informations.
Taux de disque de hello de modification des données | Au plus 6 Mbits/s par disque | Si le taux de modification de données moyen de hello sur disque de hello est au-delà de 6 Mbits/s en continu, la réplication n’intercepte pas. Toutefois, si il s’agit d’une rafale de données occasionnelles et taux de modification des données hello est supérieure à 6 Mbits/s pendant un certain temps et qu’il est fourni vers le bas, la réplication sera rattraper. Dans ce cas, certains points de récupération pourront être légèrement différés.
Disques sur des comptes de stockage Standard | Pris en charge |
Disques sur des comptes de stockage Premium | Pris en charge | Si un ordinateur virtuel possède des disques réparties sur premium et les comptes de stockage standard, vous pouvez sélectionner un compte de stockage cible différent pour chaque disque de tooensure vous avez hello même configuration de stockage dans la région cible
Disques gérés Standard | Non pris en charge |  
Disques gérés Premium | Non pris en charge |
Espaces de stockage | Pris en charge |         
Chiffrement au repos (SSE) | Pris en charge | Pour les comptes de stockage du cache et cible, vous pouvez sélectionner un compte de stockage compatible SSE.     
Azure Disk Encryption (ADE) | Non pris en charge |
Ajout/suppression de disque à chaud | Non pris en charge | Si vous ajoutez ou supprimez le disque de données sur la machine virtuelle de hello, vous devez toodisable la réplication et activez la réplication pour hello machine virtuelle.
Exclure le disque | Non pris en charge|   Le disque temporaire est exclu par défaut.
LRS | Pris en charge |
GRS | Pris en charge |
RA-GRS | Pris en charge |
ZRS | Non pris en charge |  
Stockage à froid et à chaud | Non pris en charge | Les disques de machine virtuelle ne sont pas pris en charge sur le stockage à froid et à chaud.

>[!IMPORTANT]
> Vérifiez que vous suivez hello [conseils de stockage](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) pour votre source Azure virtual machines tooavoid les problèmes de performances. Si vous suivez les paramètres par défaut de hello, Site Recovery crée des comptes de stockage hello requis en fonction de la configuration de la source hello. Si vous personnalisez et sélectionnez vos paramètres, assurez-vous de suivre hello (.. / storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) comme source de machines virtuelles.

## <a name="support-for-network-configuration"></a>Prise en charge de la configuration réseau
**Configuration** | **Prise en charge/Non prise en charge** | **Notes**
--- | --- | ---
Interfaces réseau | Jusqu’à la quantité maximale de cartes réseau prises en charge par une taille spécifique de machine virtuelle Azure | Cartes réseau est créés lorsque hello machine virtuelle est créée en tant que partie du Test de basculement ou l’opération de basculement. Bonjour le nombre de cartes réseau sur le basculement hello que machine virtuelle varie selon le nombre hello de cartes réseau source de hello qu'est l’ordinateur virtuel au moment de l’activation de la réplication de hello. Si vous ajouter/supprimer des cartes réseau après l’activation de la réplication, il n’affecte pas de nombre de cartes réseau sur hello bascule la machine virtuelle.
Équilibreur de charge Internet | Pris en charge | Vous devez tooassociate hello préconfiguré équilibrage de charge à l’aide d’un script d’automatisation azure dans un plan de récupération.
Équilibreur de charge interne | Pris en charge | Vous devez tooassociate hello préconfiguré équilibrage de charge à l’aide d’un script d’automatisation azure dans un plan de récupération.
Adresse IP publique| Pris en charge | Vous devez tooassociate une toohello IP publique existante NIC ou en créer un et associez toohello carte réseau à l’aide d’un script d’automatisation azure dans un plan de récupération.
Groupe de sécurité réseau sur la carte réseau (Resource Manager)| Pris en charge | Vous devez tooassociate hello NSG toohello carte réseau à l’aide d’un script d’automatisation azure dans un plan de récupération.  
Groupe de sécurité réseau sur le sous-réseau (Resource Manager et Classique)| Pris en charge | Vous devez tooassociate hello NSG toohello carte réseau à l’aide d’un script d’automatisation azure dans un plan de récupération.
Groupe de sécurité réseau sur la machine virtuelle (Classique)| Pris en charge | Vous devez tooassociate hello NSG toohello carte réseau à l’aide d’un script d’automatisation azure dans un plan de récupération.
Adresse IP réservée (adresse IP statique) / Conserver l’adresse IP source | Pris en charge | Si hello carte réseau sur l’ordinateur virtuel source de hello possède une configuration IP statique et le sous-réseau de cible hello a hello même adresse IP disponible, il est attribué toohello bascule la machine virtuelle. Sous-réseau de hello cible n’a pas de hello même adresse IP disponible, un des hello des adresses IP disponible dans les sous-réseaux hello sont réservée pour cet ordinateur virtuel. Vous pouvez spécifier l’adresse IP fixe de votre choix dans « Élément répliqué > Paramètres > Calcul et réseau > Interfaces réseau ». Vous pouvez sélectionner hello NIC et spécifiez le sous-réseau de hello et l’adresse IP de votre choix.
Adresse IP dynamique| Pris en charge | Si hello carte réseau sur l’ordinateur virtuel source de hello possède la configuration IP dynamique, hello NIC lors du basculement de hello machine virtuelle est également dynamique par défaut. Vous pouvez spécifier l’adresse IP fixe de votre choix dans « Élément répliqué > Paramètres > Calcul et réseau > Interfaces réseau ». Vous pouvez sélectionner hello NIC et spécifiez le sous-réseau de hello et l’adresse IP de votre choix.
Intégration de Traffic Manager | Pris en charge | Vous pouvez préconfigurer votre traffic manager de sorte que le trafic de hello est routé toohello le point de terminaison dans la région de la source sur une réguliers base toohello point de terminaison et dans la région cible en cas de basculement.
Système DNS géré par Azure | Pris en charge |
Système DNS personnalisé  | Pris en charge |    
Proxy non authentifié | Pris en charge | Consultez trop[document du Guide de mise en réseau.](site-recovery-azure-to-azure-networking-guidance.md)    
Proxy authentifié | Non pris en charge | Si hello machine virtuelle utilise un proxy authentifié pour la connexion sortante, il ne peut pas être répliquée à l’aide d’Azure Site Recovery.  
Site tooSite VPN locale (avec ou sans ExpressRoute)| Pris en charge | Vérifiez que hello UDRs et les groupes de sécurité réseau sont configurés de sorte que le trafic de récupération de Site hello n’est pas routé tooon local. Consultez trop[document du Guide de mise en réseau.](site-recovery-azure-to-azure-networking-guidance.md)  
Connexion tooVNET de réseau virtuel | Pris en charge | Consultez trop[document du Guide de mise en réseau.](site-recovery-azure-to-azure-networking-guidance.md)  


## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur la [mise en réseau pour la réplication des machines virtuelles Azure](site-recovery-azure-to-azure-networking-guidance.md).
- Commencez à protéger vos charges de travail en [répliquant des machines virtuelles Azure](site-recovery-azure-to-azure.md).
