---
title: "matrice de prise en charge aaaAzure Site Recovery pour répliquer tooAzure | Documents Microsoft"
description: "Résume hello pris en charge les systèmes d’exploitation et composants pour Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajanaki
ms.openlocfilehash: eae1db2ff1392d272f6b2eb0e3410da19d09da7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-on-premises-tooazure"></a>Matrice de prise en charge Azure Site Recovery pour la réplication à partir de tooAzure sur site


Cet article résume les composants et configurations prises en charge pour Azure Site Recovery lors de la réplication et la récupération de tooAzure. Pour plus d’informations sur la configuration requise d’Azure Site Recovery, consultez hello [conditions préalables](site-recovery-prereq.md).


## <a name="support-for-deployment-options"></a>Prise en charge des options de déploiement

**Déploiement** | **Serveur VMware/physique** | **Hyper-V (avec / sans  Virtual Machine Manager)** |
--- | --- | ---
**Portail Azure** | Les ordinateurs virtuels VMware tooAzure stockage Azure Resource Manager ou stockage classiques et les réseaux sur site.<br/><br/> Basculement tooResource classiques ou basée sur le Gestionnaire de machines virtuelles. | Stockage de tooAzure des ordinateurs virtuels Hyper-V, avec le Gestionnaire de ressources ou de stockage classiques et les réseaux sur site.<br/><br/> Basculement tooResource classiques ou basée sur le Gestionnaire de machines virtuelles.
**Portail classique** | Mode Maintenance uniquement. Il est impossible de créer des coffres. | Mode Maintenance uniquement.
**PowerShell** | Non pris en charge pour le moment. | Pris en charge


## <a name="support-for-datacenter-management-servers"></a>Prise en charge des serveurs de gestion du centre de données

### <a name="virtualization-management-entities"></a>Entités de gestion de la virtualisation

**Déploiement** | **Support**
--- | ---
**Machine virtuelle VMware/serveur physique** | vCenter 6.5, 6.0 ou 5.5
**Hyper-V (avec VMM)** | System Center Virtual Machine Manager 2016 et System Center Virtual Machine Manager 2012 R2

  >[!Note]
  > Un cloud System Center Virtual Machine Manager 2016 qui combine des hôtes Windows Server 2016 et 2012 R2 n’est pas actuellement pris en charge.

### <a name="host-servers"></a>Serveurs hôtes

**Déploiement** | **Support**
--- | ---
**Machine virtuelle VMware/serveur physique** | vSphere 6.5, 6.0 ou 5.5
**Hyper-V (avec / sans Virtual Machine Manager)** | Windows Server 2016, Windows Server 2012 R2 avec les dernières mises à jour.<br></br>Si SCVMM est utilisé, les hôtes Windows Server 2016 doivent être gérés par SCVMM 2016.


  >[!Note]
  >Les sites Hyper-V qui combinent des hôtes Windows Server 2016 et 2012 R2 ne sont actuellement pas pris en charge. Récupération tooan autre emplacement pour les machines virtuelles sur un ordinateur hôte Windows Server 2016 n’est pas actuellement pris en charge.

## <a name="support-for-replicated-machine-os-versions"></a>Prise en charge des versions de système d’exploitation de machine répliquée

Machines virtuelles qui sont protégées doivent répondre aux [conditions requises pour Azure](#failed-over-azure-vm-requirements) lors de la réplication tooAzure.
Hello tableau suivant résume la prise en charge du système d’exploitation répliquées dans différents scénarios de déploiement lors de l’utilisation d’Azure Site Recovery. Cette prise en charge n’est applicable à toute charge de travail en cours d’exécution sur hello mentionné du système d’exploitation.

 **Serveur VMware/physique** | **Hyper-V (avec ou sans VMM)** |
--- | --- |
Windows Server 2012 R2 64 bits, Windows Server 2012, Windows Server 2008 R2 avec au moins SP1<br/>*Windows Server 2016* n’est actuellement pas pris en charge sur les machines virtuelles VMware et les serveurs physiques. <br/><br/> Red Hat Enterprise Linux : too5.11 5.2, 6.1 too6.8, too7.3 7.0 <br/><br/>Centos : too5.11 5.2, 6.1 too6.8, too7.3 7.0 <br/><br/>Serveur LTS Ubuntu 14.04[ (versions du noyau prises en charge)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Serveur LTS Ubuntu 16.04 [ (versions du noyau prises en charge)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Oracle Enterprise Linux 6.4, 6.5 exécutant noyau compatible de Red Hat hello ou insécable Enterprise noyau version 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 SP3 <br/><br/> SUSE Linux Enterprise Server 11 SP4 <br/>(Mise à niveau de la réplication des machines SLES 11 SP3 tooSLES 11 SP4 n’est pas pris en charge. Si un ordinateur répliqué a été mis à niveau à partir de SLES 11SP3 tooSLES 11 SP4, vous devez toodisable réplication et protéger les ordinateur hello à nouveau de post mise à niveau hello.) | N’importe quel système d’exploitation invité [pris en charge par Azure](https://technet.microsoft.com/library/cc794868.aspx)


>[!IMPORTANT]
>(Applicable tooVMware/des serveurs physiques tooAzure de réplication)
>
> Sur Red Hat Enterprise Linux Server 7 + et les serveurs de CentOS 7 +, 3.10.0-514 de version du noyau est pris en charge à partir de la version 9.8 Hello service Azure Site Recovery mobilité.<br/><br/>
> Les clients sur le noyau de 3.10.0-514 hello avec une version de hello service mobilité inférieure à la version 9.8 sont requis toodisable réplication, mise à jour de version hello de hello mobilité service tooversion 9.8 et activer à nouveau la réplication.


### <a name="supported-ubuntu-kernel-versions-for-vmwarephysical-servers"></a>Versions du noyau Ubuntu prises en charge pour les serveurs VMware/physiques

**Version release** | **Version du service Mobilité** | **Version du noyau** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0-117-générique<br/>3.16.0-25-Generic too3.16.0-77-générique<br/>3.19.0-18-Generic too3.19.0-80-générique<br/>4.2.0-18-Generic too4.2.0-42-générique<br/>4.4.0-21-Generic too4.4.0 75-générique |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0 121-générique,<br/>3.16.0-25-Generic too3.16.0-77-générique<br/>3.19.0-18-Generic too3.19.0-80-générique<br/>4.2.0-18-Generic too4.2.0-42-générique<br/>4.4.0-21-Generic too4.4.0 81-générique |
LTS 16.04 | 9.10 | 4.4.0-21-Generic too4.4.0-81-générique<br/>4.8.0-34-Generic too4.8.0-56-générique<br/>4.10.0-14-Generic too4.10.0-24-générique |


## <a name="supported-file-systems-and-guest-storage-configurations-on-linux-vmwarephysical-servers"></a>Systèmes de fichiers pris en charge et configurations de stockage invité sous Linux (serveurs physiques / VMware)

suivant de Hello systèmes de fichiers et stockage logiciel de configuration est prise en charge sur des serveurs Linux s’exécutant sur des serveurs VMware ou physique :
* Systèmes de fichiers : ext3, ext4, ReiserFS (Suse Linux Enterprise Server uniquement), XFS
* Gestionnaire de volume : LVM2
* Logiciel multichemin : Device Mapper

Les périphériques de stockage Paravirtualized (exportés par les pilotes paravirtualized) ne sont pas pris en charge.<br/>
Les unités de bloc d’entrée et de sortie en file d’attente ne sont pas prises en charge.<br/>
Les serveurs physiques avec un contrôleur de stockage HP CCISS hello ne sont pas pris en charge.<br/>

>[!Note]
> Sur Linux hello de serveurs suivant des répertoires (si configuré en tant que partitions/fichier-systèmes distincts) doit être sur hello même disque (disque hello du système d’exploitation) sur le serveur de source de hello : / (racine), /boot, / usr, / usr/local, /var, etc<br/><br/>
> Fonctionnalités XFSv5 sur les systèmes de fichiers XFS telles que des métadonnées de somme de contrôle sont pris en charge à partir de la version 9.10 Hello service mobilité. Si vous utilisez les fonctionnalités XFSv5, assurez-vous d’exécuter la version 9.10 ou ultérieure du service Mobilité. Vous pouvez utiliser superbloc XFS de hello xfs_info utilitaire toocheck hello pour la partition de hello. Si a la valeur too1 ftype, puis XFSv5 fonctionnalités sont utilisées.
>


## <a name="support-for-network-configuration"></a>Prise en charge de la configuration réseau
Hello les tableaux suivants résument la prise en charge de la configuration réseau dans différents scénarios de déploiement qui utilisent Azure Site Recovery tooreplicate tooAzure.

### <a name="host-network-configuration"></a>Configuration du réseau hôte

**Configuration** | **Serveur VMware/physique** | **Hyper-V (avec / sans Virtual Machine Manager)**
--- | --- | ---
Association de cartes réseau | Oui<br/><br/>Non pris en charge lorsque les machines physiques sont répliquées| Oui
VLAN | Oui | Oui
IPv4 | Oui | Oui
IPv6 | Non | Non

### <a name="guest-vm-network-configuration"></a>Configuration du réseau de machines virtuelles invitées

**Configuration** | **Serveur VMware/physique** | **Hyper-V (avec / sans Virtual Machine Manager)**
--- | --- | ---
Association de cartes réseau | Non | Non
IPv4 | Oui | Oui
IPv6 | Non | Non
Adresse IP statique (Windows) | Oui | Oui
Adresse IP statique (Linux) | Oui <br/><br/>Machines virtuelles est configuré toouse DHCP sur la restauration automatique  | Non
Plusieurs cartes réseau | Oui | Oui

### <a name="failed-over-azure-vm-network-configuration"></a>Configuration de réseau des machines virtuelles Azure basculées

**Mise en réseau Azure** | **Serveur VMware/physique** | **Hyper-V (avec / sans Virtual Machine Manager)**
--- | --- | ---
ExpressRoute | Oui | Oui
ILB | Oui | Oui
ELB | Oui | Oui
Traffic Manager | Oui | Oui
Plusieurs cartes réseau | Oui | Oui
Adresse IP réservée | Oui | Oui
IPv4 | Oui | Oui
Conserver l’adresse IP source | Oui | Oui


## <a name="support-for-storage"></a>Prise en charge du stockage
Hello les tableaux suivants résument la configuration du stockage prise en charge dans différents scénarios de déploiement qui utilisent Azure Site Recovery tooreplicate tooAzure.

### <a name="host-storage-configuration"></a>Configuration du stockage hôte

**Configuration** | **Serveur VMware/physique** | **Hyper-V (avec / sans Virtual Machine Manager)**
--- | --- | --- | ---
NFS | Oui pour VMware<br/><br/> Non pour les serveurs physiques | N/A
SMB 3.0 | N/A | Oui
SAN (ISCSI) | Oui | Oui
Chemins d’accès multiples (MPIO)<br></br>Testé avec : Microsoft DSM, EMC PowerPath 5.7 SP4, EMC PowerPath DSM pour CLARiiON | Oui | Oui

### <a name="guest-or-physical-server-storage-configuration"></a>Configuration du stockage sur serveur physique ou invité

**Configuration** | **Serveur VMware/physique** | **Hyper-V (avec / sans Virtual Machine Manager)**
--- | --- | ---
VMDK | Oui | N/A
VHD/VHDX | N/A | Oui
Machine virtuelle de 2e génération | N/A | Oui
EFI/UEFI| Non | Oui
Disque de cluster partagé | Non | Non
Disque chiffré | Non | Non
NFS | Non | N/A
SMB 3.0 | Non | Non
RDM | Oui<br/><br/> N/A pour les serveurs physiques | N/A
Disque > 1 To | Oui<br/><br/>Jusqu’à 4095 Go | Oui<br/><br/>Jusqu’à 4095 Go
Disque avec une taille de secteur de 4K | Oui | Oui, les machines virtuelles de génération 1 sont prises en charge<br/><br/>Les machines virtuelles de génération 2 ne sont pas prises en charge.
Volume avec disque à bandes > 1 To<br/><br/> Gestion des volumes logiques | Oui | Oui
Espaces de stockage | Non | Oui
Ajout/suppression de disque à chaud | Non | Non
Exclure le disque | Oui | Oui
Chemins d’accès multiples (MPIO) | N/A | Oui

**Stockage Azure** | **Serveur VMware/physique** | **Hyper-V (avec / sans Virtual Machine Manager)**
--- | --- | ---
LRS | Oui | Oui
GRS | Oui | Oui
RA-GRS | Oui | Oui
Stockage froid | Non | Non
Stockage chaud| Non | Non
Chiffrement au repos (SSE)| Oui | Oui
Stockage Premium | Oui | Oui
Service Import/Export | Non | Non


## <a name="support-for-azure-compute-configuration"></a>Prise en charge de la configuration de calcul Azure

**Fonctionnalité de calcul** | **Serveur VMware/physique** | **Hyper-V (avec / sans Virtual Machine Manager)**
--- | --- | --- 
Groupes à haute disponibilité | Oui | Oui
HUB | Oui | Oui  
Disques gérés | Oui | Oui<br/><br/>La restauration automatique tooon local à partir de la machine virtuelle Azure avec des disques gérés n’est pas pris en charge actuellement.

## <a name="failed-over-azure-vm-requirements"></a>Configuration requise des machines virtuelles Azure basculées

Vous pouvez déployer des machines virtuelles de tooreplicate Site Recovery et des serveurs physiques exécutant n’importe quel système d’exploitation pris en charge par Azure. La plupart des versions de Windows et Linux sont concernées. Machines virtuelles que vous souhaitez tooreplicate doivent être conformes à hello suivant les exigences Azure lors de la réplication tooAzure sur site.

**Entité** | **Configuration requise** | **Détails**
--- | --- | ---
**Système d’exploitation invité** | La réplication Hyper-V tooAzure : récupération de Site prend en charge tous les systèmes d’exploitation [pris en charge par Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx). <br/><br/> Pour la réplication de serveur physique et de VMware : Vérifiez hello Windows et Linux [conditions préalables](site-recovery-vmware-to-azure-classic.md) | La vérification de la configuration requise est mise en échec en cas de défaut de prise en charge.
**Architecture du système d’exploitation invité** | 64 bits | La vérification de la configuration requise est mise en échec en cas de défaut de prise en charge.
**Taille du disque du système d’exploitation** | Jusqu'à too2048 Go si vous répliquez **les ordinateurs virtuels VMware ou serveurs physiques tooAzure**.<br/><br/>Jusqu’à 2048 Go pour les machines virtuelles **Hyper-V Génération 1**.<br/><br/>Jusqu’à 300 Go pour les **machines virtuelles Hyper-V Génération 2**.  | La vérification de la configuration requise est mise en échec en cas de défaut de prise en charge.
**Nombre de disques du système d’exploitation** | 1 | La vérification de la configuration requise est mise en échec en cas de défaut de prise en charge.
**Nombre de disques de données** | inférieur ou égal à 64 si vous répliquez **les ordinateurs virtuels VMware tooAzure**; 16 ou moins si vous répliquez **tooAzure d’ordinateurs virtuels Hyper-V** | La vérification de la configuration requise est mise en échec en cas de défaut de prise en charge.
**Taille du disque dur virtuel de données** | Des too4095 Go | La vérification de la configuration requise est mise en échec en cas de défaut de prise en charge.
**Adaptateurs réseau** | Prise en charge de plusieurs adaptateurs réseau. |
**Disque dur virtuel partagé** | Non pris en charge | La vérification de la configuration requise est mise en échec en cas de défaut de prise en charge.
**Disque FC** | Non pris en charge | La vérification de la configuration requise est mise en échec en cas de défaut de prise en charge.
**Format de disque dur** | Disque dur virtuel (VHD)  <br/><br/> VHDX | VHDX n’est pas actuellement pris en charge dans Azure, Site Recovery convertit automatiquement VHDX tooVHD lorsque vous basculez tooAzure. Lorsque vous effectuez une restauration automatique tooon local hello virtuels continuer format VHDX de hello toouse.
**BitLocker** | Non pris en charge | Bitlocker doit être désactivé préalablement à la protection d’une machine virtuelle.
**Nom de la machine virtuelle** | Entre 1 et 63 caractères. Tooletters restreint, des chiffres et des traits d’union. nom d’ordinateur virtuel Hello doit commencer et se terminer par une lettre ou un chiffre. | Mettre à jour la valeur hello dans les propriétés d’ordinateur virtuel hello en mode de récupération de Site.
**Type de machine virtuelle** | Génération 1<br/><br/> Génération 2 -- Windows | Les machines virtuelles de 2e génération avec un type de disque de système d’exploitation de base, qui inclut un ou deux volumes de données au format VHDX et un espace disque inférieur à 300 Go sont prises en charge.<br></br>Les machines virtuelles Linux de 2e génération ne sont pas prises en charge. [En savoir plus](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## <a name="support-for-recovery-services-vault-actions"></a>Prise en charge des actions de coffre Recovery Services

**Action** | **Serveur VMware/physique** | **Hyper-V (sans VMM)** | **Hyper-V (avec VMM)**
--- | --- | --- | ---
Déplacer le coffre entre plusieurs groupes de ressources<br/><br/> Au sein et entre des abonnements | Non | Non | Non
Déplacer le stockage, les réseaux, les machines virtuelles Azure entre des groupes de ressources<br/><br/> Au sein et entre des abonnements | Non | Non | Non


## <a name="support-for-provider-and-agent"></a>Prise en charge du fournisseur et de l’agent

**Nom** | **Description** | **Version la plus récente** | **Détails**
--- | --- | --- | --- | ---
**Fournisseur Azure Site Recovery** | Coordonne les communications entre les serveurs locaux et Azure <br/><br/> Installé sur les serveurs VMM locaux ou sur des serveurs Hyper-V s’il n’existe aucun serveur VMM | 5.1.19 ([disponible sur le portail](http://aka.ms/downloaddra)) | [Fonctionnalités et correctifs récents](https://support.microsoft.com/kb/3155002)
**Azure Site Recovery unifiée le programme d’installation (tooAzure VMware)** | Coordonne les communications entre les serveurs VMware locaux et Azure  <br/><br/> Installé sur des serveurs VMware locaux | 9.3.4246.1 (disponible sur le portail) | [Fonctionnalités et correctifs récents](https://support.microsoft.com/kb/3155002)
**Service de mobilité** | Coordonne la réplication entre les serveurs VMware/serveurs physiques et Azure/site secondaire<br/><br/> Installé sur des serveurs physiques ou de VMware VM souhaité tooreplicate  | N/A (disponible sur le portail) | N/A
**Agent Microsoft Azure Recovery Services (MARS)** | Coordonne la réplication entre les machines virtuelles Hyper-V et Azure<br/><br/> Installé sur des serveurs Hyper-V locaux (avec ou sans serveur VMM) | Dernier agent ([disponible sur le portail](http://aka.ms/latestmarsagent)) |






## <a name="next-steps"></a>Étapes suivantes
[Vérifiez les composants requis](site-recovery-prereq.md)
