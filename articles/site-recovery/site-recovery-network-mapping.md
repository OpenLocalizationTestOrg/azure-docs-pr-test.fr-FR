---
title: "aaaPlan le mappage réseau pour la réplication de machine virtuelle Hyper-V avec Site Recovery | Documents Microsoft"
description: "Configurez le mappage réseau pour la réplication d’ordinateur virtuel Hyper-V à partir d’un tooAzure de centre de données local, ou tooa un site secondaire."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a>Planifier un mappage réseau pour la réplication de machine virtuelle Hyper-V avec Site Recovery



Cet article vous aidera à toounderstand et plan pour le réseau pendant la réplication d’ordinateurs virtuels Hyper-V tooAzure ou site secondaire de tooa de mappage, à l’aide de hello [service Azure Site Recovery](site-recovery-overview.md).

Après l’avoir lu cet article valider les commentaires en bas de hello de cet article, ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-for-replication-tooazure"></a>Mappage réseau pour la réplication tooAzure

Le mappage réseau est utilisé pour répliquer des machines virtuelles de Hyper-V (géré dans VMM) tooAzure. Le mappage réseau opère entre des réseaux de machines virtuelles sur un serveur VMM source et des réseaux Azure cibles. Mappage hello suivant :

- **Connexion réseau**: garantit que les machines virtuelles répliquées de Azure sont réseau toohello connecté. Toutes les machines qui basculent sur hello même réseau peut se connecter tooeach autre, même si elles ont échoué sur les plans de récupération différent.
- **Passerelle de réseau**: si une passerelle de réseau est configurée sur le réseau Azure cible de hello, les machines virtuelles peuvent se connecter tooother locaux virtuels.

Notez les points suivants :

- Vous mappez une source de VMM VM réseau tooan réseau virtuel Azure.
- Après le basculement de machines virtuelles Azure Bonjour réseau source sera réseau virtuel de cible mappé toohello connecté.
- Nouvelles machines virtuelles ajoutées réseau d’ordinateurs virtuels toohello source sont connectés toohello mappé réseau Azure lors de la réplication a lieu.
- Si le réseau cible de hello possède plusieurs sous-réseaux, et un de ces sous-réseaux a hello le même nom que le sous-réseau sur lequel virtual machine de hello source se trouve, puis hello ordinateur virtuel se connecte le sous-réseau de toothat cible après le basculement.
- S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello se connecte toohello premier sous-réseau de réseau de hello.


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a>Mappage réseau pour la réplication tooa centre de données secondaire

Le mappage réseau est utilisé pour répliquer des machines virtuelles de Hyper-V (gérée dans System Center Virtual Machine Manager (VMM)) tooa centre de données secondaire. Le mappage réseau opère entre des réseaux de machines virtuelles sur un serveur VMM source et des réseaux de machines virtuelles sur un serveur VMM cible. Mappage hello suivant :

- **Connexion réseau**, réseaux de tooappropriate se connecte les machines virtuelles après le basculement. ordinateur virtuel de réplication Hello sera réseau connecté toohello cible qui est mappé toohello source réseau.
- **Placement optimal**: pas de façon optimale les endroits hello machines virtuelles de réplication sur les serveurs hôtes Hyper-V. Machines virtuelles de réplication sont placées sur des hôtes auxquels peuvent hello d’accès mappées réseaux d’ordinateurs virtuels.
- **Aucun mappage de réseau**: Si vous ne configurez pas le mappage réseau, machines virtuelles de réplica sera connecté tooany réseaux d’ordinateurs virtuels après le basculement.

Notez les points suivants :

- Le mappage réseau peut être configuré entre les réseaux VM sur deux serveurs VMM ou sur un seul serveur VMM si deux sites sont gérés par hello même serveur.
- Lorsque le mappage est correctement configuré la réplication est activée, une machine virtuelle à l’emplacement principal de hello sera connecté tooa réseau et son réplica dans l’emplacement cible de hello sera connecté tooits mappé réseau.
-
- Si les réseaux ont été configurées correctement dans VMM, lorsque vous sélectionnez un réseau de machines virtuelles cible lors du mappage réseau, les clouds sources hello VMM qui utilisent le réseau d’ordinateurs virtuels hello source seront affichera, ainsi que les réseaux d’ordinateurs virtuels hello cibles disponibles sur les clouds cibles hello qui sont utilisés pour protection.
- Si le réseau cible de hello a plusieurs sous-réseaux et de ces sous-réseaux a hello même nom comme hello sous-réseau sur quel hello ordinateur virtuel source se trouve, puis hello machine virtuelle de réplication sera connectée toothat cible sous-réseau après le basculement. S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.



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



## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur [planification d’infrastructure de réseau hello](site-recovery-network-design.md).
