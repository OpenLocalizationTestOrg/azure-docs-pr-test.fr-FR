---
title: "matrice aaaSupport pour le site secondaire de réplication tooa avec Azure Site Recovery | Documents Microsoft"
description: "Résume hello pris en charge les systèmes d’exploitation et composants pour Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 0b2bbc86aff52308d5a90a56d7a3ff4286877740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="support-matrix-for-replication-tooa-secondary-site-with-azure-site-recovery"></a>Matrice de prise en charge pour le site secondaire de réplication tooa avec Azure Site Recovery

Cet article résume ce qui est pris en charge lorsque vous utilisez Azure Site Recovery tooreplicate tooa secondaire sur-site local.

## <a name="deployment-options"></a>Options de déploiement

**Déploiement** | **Serveur VMware/physique** | **Hyper-V (avec ou sans SCVMM)**
--- | --- | --- | ---
**Portail Azure** | Les ordinateurs virtuels VMware toosecondary VMware site local.<br/><br/> Télécharger hello [guide de l’utilisateur InMage Scout](http://download.microsoft.com/download/E/0/8/E08B3BCE-3631-4CED-8E65-E3E7D252D06D/InMage_Scout_Standard_User_Guide_8.0.1.pdf) (non disponible dans hello portail Azure). | Machines virtuelles de Hyper-V dans le cloud VMM secondaire VMM clouds tooa sur site.<br></br> Non pris en charge sans VMM  <br/><br/> Réplication Hyper-V standard uniquement. SAN non pris en charge.
**Portail classique** | Mode Maintenance uniquement. Il est impossible de créer des coffres. | Mode Maintenance uniquement<br></br> Non pris en charge sans SCVMM
**PowerShell** | Non pris en charge | Pris en charge<br></br> Non pris en charge sans SCVMM

## <a name="on-premises-servers"></a>Serveurs locaux

### <a name="virtualization-servers"></a>Serveurs de virtualisation

**Déploiement** | **Support**
--- | ---
**Machine virtuelle VMware/serveur physique** | vSphere 6.0, 5.5 ou 5.1 avec les dernières mises à jour
**Hyper-V (avec VMM)** | VMM 2016 et VMM 2012 R2

  >[!Note]
  > Les clouds VMM 2016 qui combinent des hôtes Windows Server 2016 et 2012 R2 ne sont actuellement pas pris en charge.

### <a name="host-servers"></a>Serveurs hôtes

**Déploiement** | **Support**
--- | ---
**Machine virtuelle VMware/serveur physique** | vCenter 5.5 ou 6.0 (prise en charge des fonctionnalités 5.5 uniquement) 
**Hyper-V (sans VMM)** | Pas une configuration prise en charge pour la réplication de site secondaire de tooa
**Hyper-V avec VMM** | Windows Server 2016 et Windows Server 2012 R2 avec les dernières mises à jour de hello.<br/><br/> Les hôtes Windows Server 2016 doivent être gérés par VMM 2016.

## <a name="support-for-replicated-machine-os-versions"></a>Prise en charge des versions de système d’exploitation de machine répliquée
Hello tableau suivant résume la prise en charge du système d’exploitation dans différents scénarios de déploiement lors de l’utilisation d’Azure Site Recovery. Cette prise en charge n’est applicable à toute charge de travail en cours d’exécution sur hello mentionné du système d’exploitation.

**Serveur VMware/physique** | **Hyper-V (avec VMM)**
--- | --- | ---
Windows Server 2012 R2 64 bits, Windows Server 2012, Windows Server 2008 R2 avec au moins SP1<br/><br/> Red Hat Enterprise Linux 6.7, 7.1, 7.2 <br/><br/> Centos 6.5, 6.6, 6.7, 7.0, 7.1, 7.2 <br/><br/> Oracle Enterprise Linux version 6.4 ou 6.5 noyau compatible de Red Hat hello ou insécable Enterprise noyau version 3 (UEK3) en cours d’exécution <br/><br/> SUSE Linux Enterprise Server 11 SP3 | Tout système d’exploitation invité [pris en charge par Hyper-V](https://technet.microsoft.com/library/mt126277.aspx)

>[!Note]
>Seuls les ordinateurs Linux avec hello suivant de stockage peuvent être répliquées : fichiers système (EXT3, ETX4, ReiserFS, XFS) ; Mappeur de chemins d’accès multiples de périphérique de logiciel ; Gestionnaire de volume (LVM2).
>Les serveurs physiques avec stockage de contrôleur HP CCISS ne sont pas pris en charge.
>système de fichiers ReiserFS Hello est pris en charge uniquement sur SUSE Linux Enterprise Server 11 SP3.

## <a name="network-configuration"></a>Configuration réseau

### <a name="hosts"></a>Hôtes

**Configuration** | **Serveur VMware/physique** | **Hyper-V (avec VMM)**
--- | --- | ---
Association de cartes réseau | Oui | Oui
VLAN | Oui | Oui
IPv4 | Oui | Oui
IPv6 | Non | Non

### <a name="guest-vms"></a>MV invitées

**Configuration** | **Serveur VMware/physique** | **Hyper-V (avec VMM)**
--- | --- | ---
Association de cartes réseau | Non | Non
IPv4 | Oui | Oui
IPv6 | Non | Non
Adresse IP statique (Windows) | Oui | Oui
Adresse IP statique (Linux) | Oui | Oui
Plusieurs cartes réseau | Oui | Oui


## <a name="storage"></a>Storage

### <a name="host-storage"></a>Stockage hôte

**Stockage (hôte)** | **Serveur VMware/physique** | **Hyper-V (avec VMM)**
--- | --- | ---
NFS | Oui | N/A
SMB 3.0 | N/A | Oui
SAN (ISCSI) | Oui | Oui
Chemins d’accès multiples (MPIO) | Oui | Oui

### <a name="guest-or-physical-server-storage"></a>Stockage sur serveur physique ou invité

**Configuration** | **Serveur VMware/physique** | **Hyper-V (avec VMM)**
--- | --- | ---
VMDK | Oui | N/A
VHD/VHDX | N/A | Oui (haut too16 disques)
Machine virtuelle de 2e génération | N/A | Oui
Disque de cluster partagé | Oui  | Non
Disque chiffré | Non | Non
UEFI| Non | N/A
NFS | Non | Non
SMB 3.0 | Non | Non
RDM | Oui | N/A
Disque > 1 To | Non | Oui
Volume avec disque à bandes > 1 To<br/><br/> LVM | Oui | Oui
Espaces de stockage | Non | Oui
Ajout/suppression de disque à chaud | Non | Non
Exclure le disque | Non | Oui
Chemins d’accès multiples (MPIO) | N/A | Oui

## <a name="vaults"></a>Coffres

**Action** | **Serveur VMware/physique** | **Hyper-V (avec VMM)**
--- | --- | ---
Déplacer les coffres entre plusieurs groupes de ressources (dans ou entre les différents abonnements) | Non | Non
Déplacer le stockage, les réseaux, les machines virtuelles Azure entre des groupes de ressources (dans ou entre les différents abonnements) | Non | Non

## <a name="provider-and-agent"></a>Fournisseur et agent

**Nom** | **Description** | **Version la plus récente** | **Détails**
--- | --- | --- | --- | ---
**Fournisseur Azure Site Recovery** | Coordonne les communications entre les serveurs locaux et Azure <br/><br/> Installé sur des serveurs VMM locaux ou des serveurs Hyper-V, si aucun serveur VMM n’existe | 5.1.19 ([disponible sur le portail](http://aka.ms/downloaddra)) | [Fonctionnalités et correctifs récents](https://support.microsoft.com/kb/3155002)
**Service de mobilité** | La réplication entre des serveurs VMware locaux ou de serveurs physiques et de site secondaire de hello<br/><br/> Installé sur les VM VMware ou serveurs physiques que vous souhaitez tooreplicate  | N/A (disponible sur le portail) | N/A


## <a name="next-steps"></a>Étapes suivantes

- [Répliquer les machines virtuelles de Hyper-V dans le site secondaire du tooa clouds VMM](site-recovery-vmm-to-vmm.md)
- [Répliquer des ordinateurs virtuels VMware et des serveurs physiques tooa un site secondaire](site-recovery-vmware-to-vmware.md)
