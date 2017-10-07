---
title: "aaaBackup et récupération d’urgence pour les disques Azure IaaS | Documents Microsoft"
description: "Dans cet article, nous expliquerons comment tooplan pour la sauvegarde et récupération d’urgence (DR) de IaaS machines () et les disques dans Azure. Ce document couvre les disques managés et non managés."
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: luywang
ms.openlocfilehash: 17c697bc411fb47c4b7483b59829af1c40732ac1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Sauvegarde et récupération d’urgence pour les disques IaaS Azure

Dans cet article, nous expliquerons comment tooplan pour la sauvegarde et récupération d’urgence (DR) de IaaS machines () et les disques dans Azure. Ce document couvre les disques managés et non managés.

Nous parlerons tout d’abord hello intégrées des fonctionnalités de tolérance Bonjour plateforme Azure qui vous protéger contre les défaillances locales. Nous discuterons des scénarios de reprise après sinistre hello pas entièrement couverts par les fonctionnalités intégrées de hello, qui est le sujet principal de hello traité par ce document. Nous montrons également plusieurs exemples de charges de travail où différentes considérations en matière de sauvegarde et de récupération d’urgence peuvent s’appliquer. Nous voyons ensuite les solutions possibles pour la récupération d’urgence des disques IaaS. 

## <a name="introduction"></a>Introduction

Hello plateforme Azure utilise plusieurs méthodes pour assurer la redondance et protéger les clients contre les défaillances matérielles localisées qui peuvent se produire toohelp de tolérance de panne. Échecs locaux peuvent inclure des problèmes avec un ordinateur de serveur de stockage Azure qui stocke une partie des données hello pour un disque virtuel ou échecs d’un disque SSD ou un disque dur sur le serveur. Ces défaillances de composant matériel isolé peuvent se produire pendant les opérations normales et plate-forme de hello est conçue toobe toothese résilient échecs. Des sinistres majeurs peuvent entraîner des défaillances ou l’inaccessibilité d’un grand nombre de serveurs de stockage ou d’un centre de données entier. Alors que vos machines virtuelles et les disques sont normalement protégés contre les défaillances localisés, des étapes supplémentaires sont nécessaire tooprotect votre charge de travail à partir de la région d’erreurs irrécupérables (par exemple, une catastrophe majeure) qui peuvent affecter votre machine virtuelle et les disques.

En outre possibilité toohello d’échecs de la plateforme, des problèmes avec les données ou application de client hello peuvent se produire. Par exemple, une nouvelle version de votre application peut par inadvertance modifiez importantes toohello données. Dans ce cas, vous souhaiterez peut-être application hello de toorevert et hello données tooa version antérieure contenant hello dernier état correct connu. Cela nécessite la gestion de sauvegardes régulières.

Reprise après sinistre régional, vous devez sauvegarder votre IaaS VM disques tooa autre région. 

Avant d’examiner les options de sauvegarde et de récupération d’urgence, récapitulons quelques méthodes disponibles pour gérer les défaillances localisées.

### <a name="azure-iaas-resiliency"></a>Résilience Azure IaaS

*Résilience* fait référence toohello tolérance des échecs normales qui se produisent dans les composants matériels. Résilience est toorecover de capacité hello contre les pannes et continuer toofunction. Il n’est pas sur ce qui évite les échecs, mais répond toofailures d’une manière qui évite les temps d’arrêt ou perte de données. Hello résilience vise tooreturn hello tooa pleinement fonctionnel état de l’application après un échec. Machines virtuelles et les disques sont les défaillances matérielles conçue toobe toocommon résilient. Examinons la plateforme Azure IaaS de hello fournit cette résilience.

Un ordinateur virtuel se compose principalement de deux parties : un (1) de calcul serveur et les disques persistants hello (2). Les deux affectent hello une tolérance de panne d’un ordinateur virtuel.

Si le serveur hôte de calcul Azure hello qui héberge votre machine virtuelle rencontre une défaillance matérielle (ce qui est rare), Azure est conçue tooautomatically restauration hello machine virtuelle sur un autre serveur. Dans ce cas, vous rencontrerez un redémarrage et hello machine virtuelle sera après un certain temps. Azure détecte ces défaillances matérielles automatiquement et exécute des récupérations toohelp vous assurer que le client de hello machine virtuelle seront disponible dès que possible.

Relatives aux disques de IaaS, la durabilité des données est essentielle pour la plateforme de stockage persistant hello. Les clients Azure ont des applications métier importants sur IaaS, et ils dépendent de persistance hello de données de hello. Azure conçoit la protection de ces disques IaaS avec trois copies redondantes des données stockées localement, fournissant ainsi une durabilité élevée contre les défaillances locales. Si un des composants matériels hello qui contient le disque échoue, votre machine virtuelle n’est pas affecté, car il existe deux copies supplémentaires toosupport disque demandes. Elle fonctionne même si les deux différents composants matériels prenant en charge d’un disque d’échouer au hello identiques (ce qui est très rare). toohelp Assurez-vous que nous conservent toujours les trois réplicas, le service de stockage Azure hello génère automatiquement une nouvelle copie de données en arrière-plan de hello si un des trois copies de hello n’est plus disponible. Par conséquent, il ne doit pas être nécessaire toouse RAID avec des disques Azure pour la tolérance de panne. Un simple RAID de niveau 0 configuration doit être suffisante pour la répartition des disques hello si les volumes de grande capacité toocreate nécessaire.

Cette architecture a permis à **Azure de fournir de façon cohérente une durabilité de classe Entreprise pour les disques IaaS, avec un [taux de défaillance annuel](https://en.wikipedia.org/wiki/Annualized_failure_rate) inégalé dans le secteur de zéro %.**

Les défaillances matérielles localisées sur hello calcul héberger ou dans le stockage hello plateforme peut quelquefois provoquer une indisponibilité temporaire pour hello machine virtuelle qui n’est couverte par hello [contrat SLA Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) pour la disponibilité de la machine virtuelle. Azure fournit également un contrat SLA de pointe pour les instances de machine virtuelle uniques qui utilisent des disques Stockage Premium.

toosafeguard des charges de travail à partir du temps mort en raison d’une indisponibilité temporaire de toohello d’un disque ou d’une machine virtuelle, les clients peuvent exploiter [haute disponibilité](../virtual-machines/windows/manage-availability.md). Deux ou plusieurs machines virtuelles dans un ensemble de disponibilité apporte la redondance pour l’application hello. Azure crée ensuite ces machines virtuelles et disques dans des domaines d’erreur distincts avec différents composants d’alimentation, réseau et serveur. Par conséquent, les défaillances matérielles localisées généralement n’affectent pas plusieurs machines virtuelles dans hello définie au hello même temps, en fournissant une haute disponibilité pour votre application. Il est considéré comme une disponibilité toouse de bonnes pratiques définit lors de la haute disponibilité n’est requise. Pour plus d’informations, consultez les aspects de la récupération d’urgence hello détaillées ci-dessous.

### <a name="backup-and-disaster-recovery"></a>Sauvegarde et récupération d’urgence

La récupération d’urgence (DR) est toorecover de capacité hello d’incidents rares mais principales : les défaillances non transitoires et à grande échelle, tels que des interruptions de service qui affecte une région entière. La récupération d’urgence inclut la sauvegarde et l’archivage des données. Elle peut également inclure une intervention manuelle, comme la restauration d’une base de données à partir de la sauvegarde.

Hello une protection intégrée contre les défaillances localisées de plateforme Azure ne peut pas protéger entièrement hello machines virtuelles/disques dans le cas de hello de sinistres majeurs qui peut provoquer des interruptions à grande échelle. Cela inclut les événements catastrophiques, par exemple un centre de données atteint par un ouragan, un tremblement de terre, un incendie ou des pannes d’unités matérielles à grande échelle. En outre, vous pouvez rencontrer des échecs en raison de problèmes de tooapplication ou de données.

toohelp protection de vos charges de travail IaaS contre les pannes, vous devez planifier pour la récupération de tooenable de redondance et de sauvegardes. Récupération d’urgence, vous devez prévoir de redondance et de sauvegarde dans un emplacement géographique différent en dehors du site principal de hello. Cela permet de garantir la sauvegarde n’est pas affectée par hello même événement à l’origine des conséquences sur hello machine virtuelle ou les disques. Pour plus d’informations, consultez [Récupération d’urgence pour les applications développées sur Azure](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications).

Votre considérations relatives à la récupération d’urgence peuvent inclure hello suivant aspects :

1. Haute disponibilité (HA) est la capacité hello hello application toocontinue est en cours d’exécution dans un état sain, sans temps mort significatif. Par « sain », nous entendons application hello ne répond, les utilisateurs peuvent se connecter toohello application et interagir avec lui. Certaines bases de données et les applications critiques peuvent être requis toobe disponible toujours, même lorsque sont en panne dans la plateforme de hello. Pour ces charges de travail, vous devrez peut-être redondance tooplan pour l’application hello, ainsi que les données de salutation.

2. Durabilité des données : Dans certains cas, les considération principale hello sont de vous assurer les données hello sont conservées dans le cas de hello d’un incident. Par conséquent, vous aurez peut-être besoin d’une sauvegarde de vos données dans un autre site. Pour ces charges de travail, vous ne devrez pas peut-être une redondance complète pour l’application hello, mais une sauvegarde régulière des disques de hello.

## <a name="backup-and-dr-scenarios"></a>Scénarios de sauvegarde et de récupération d’urgence

Examinons quelques exemples de scénarios de charge de travail d’application et les considérations de hello pour la planification de la récupération d’urgence.

### <a name="scenario-1-major-database-solutions"></a>Scénario 1 : solutions de base de données majeures

Prenons l’exemple d’un serveur de base de données de production tel que SQL Server ou Oracle prenant en charge la haute disponibilité. Les utilisateurs et les applications de production critiques dépendent de cette base de données. plan de récupération d’urgence Hello pour ce système peut être nécessaire de hello toosupport suivant les exigences :

1. Les données doivent être protégées et récupérables.
2.  Le serveur doit être disponible pour utilisation.

Cette opération peut nécessiter la gestion d’un réplica de base de données hello dans une région différente de sauvegarde. Selon les spécifications de hello pour la récupération des données et de la disponibilité du serveur, les solutions hello peut consister à partir d’un actif-actif ou actif-passif réplica site tooperiodic sauvegardes hors connexion de données de salutation. Les bases de données relationnelles telles que SQL Server et Oracle fournissent diverses options pour la réplication. Pour SQL Server, les [groupes de disponibilité SQL Server Always On](https://msdn.microsoft.com/library/hh510230.aspx) peuvent être utilisés pour la haute disponibilité.

Les bases de données NoSQL comme MongoDB prennent également en charge les [réplicas](https://docs.mongodb.com/manual/replication/) pour assurer la redondance. réplicas Hello pour la haute disponibilité peuvent être utilisés.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Scénario 2 : un cluster de machines virtuelles redondantes

Prenons l’exemple d’une charge de travail gérée par un cluster de machines virtuelles qui fournit la redondance et l’équilibrage de charge. Il peut s’agir d’un cluster Cassandra déployé dans une région. Ce type d’architecture fournit déjà un niveau élevé de redondance dans cette région. Toutefois, vous tooprotect hello la charge de travail à partir d’une défaillance au niveau régionale, vous devez envisager propagation du cluster de hello entre deux régions ou de création de la région tooanother des sauvegardes périodiques.

### <a name="scenario-3-iaas-application-workload"></a>Scénario 3 : charge de travail d’application IaaS

Il peut s’agir d’une charge de travail de production standard exécutée sur une machine virtuelle Azure. Par exemple, il peut être un serveur web ou un serveur de fichiers contenant le contenu de hello et d’autres ressources d’un site. Il peut également être une application métier personnalisée en cours d’exécution sur un ordinateur virtuel stocké de ses données, les ressources et état de l’application sur les disques de machine virtuelle hello. Dans ce cas, il est important toomake que vous effectuez des sauvegardes régulièrement. Fréquence de sauvegarde doit reposer sur la nature hello de charge de travail de machine virtuelle hello. Par exemple, si l’application hello s’exécute chaque jour et modifie des données, puis hello sauvegarde doit être effectuée toutes les heures.

Voici un autre exemple : un serveur de rapports qui extrait des données provenant d’autres sources et génère des rapports agrégés. Perte de cette machine virtuelle ou de disques entraîne une perte de toohello des rapports de hello. Toutefois, il peut être hello toorerun possible de processus et sortie de régénérer hello reporting. Dans ce cas, vous n’avez vraiment la perte de données même si le serveur de rapports hello est atteint avec un sinistre, donc vous pouvez avoir un niveau plus élevé de tolérance de perte de données hello sur le serveur de rapports de hello. Dans ce cas, les sauvegardes moins fréquentes est un coût de hello tooreduce option.

### <a name="scenario-4-iaas-application-data-issues"></a>Scénario 4 : problèmes liés aux données d’une application IaaS

Vous avez une application qui calcule, tient à jour et gère des données commerciales critiques telles que des informations de tarification. Une nouvelle version de votre application avait un bogue logiciel incorrectement calculée hello tarification et endommagé des données commerce existantes hello pris en charge par la plateforme de hello. Ici, hello meilleure marche à suivre serait toorevert toohello une version antérieure de l’application hello et les données de salutation premier. tooenable cette option, prenez des sauvegardes périodiques de votre système.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Solution de récupération d’urgence : service Sauvegarde Azure

Le [service Sauvegarde Azure](https://azure.microsoft.com/services/backup/) peut être utilisé pour la sauvegarde et la récupération d’urgence et il fonctionne aussi bien avec les [disques managés](storage-managed-disks-overview.md) que les [disques non managés](storage-about-disks-and-vhds-windows.md#unmanaged-disks). Vous pouvez créer un travail de sauvegarde avec des sauvegardes périodiques, une restauration facile des machines virtuelles et des stratégies de rétention de sauvegarde. 

Si vous utilisez [disques de stockage Premium](storage-premium-storage.md), [disques gérés](storage-managed-disks-overview.md), ou d’autres types de disque avec hello [stockage localement redondant (LRS)](storage-redundancy.md#locally-redundant-storage) option, il est particulièrement important tooleverage des sauvegardes de récupération d’urgence. Sauvegarde Azure stocke les données de hello dans votre coffre Recovery Services pour une rétention à long terme. Choisissez hello [stockage géo-redondant (GRS)](storage-redundancy.md#geo-redundant-storage) option pour les Services de récupération de sauvegarde hello coffre. Cela permettra de garantir les sauvegardes sont répliquées tooa autre région Azure pour la protection contre les sinistres distants.

Pour [disques non managé](storage-about-disks-and-vhds-windows.md#unmanaged-disks), vous pouvez utiliser le type de stockage LRS hello pour les disques IaaS, mais assurez-vous que Azure Backup est activé par hello option GRS pour hello coffre Recovery Services.

**Si vous utilisez hello [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) option pour vos disques non managé, vous avez besoin de captures instantanées cohérentes avec pour la sauvegarde et récupération d’urgence.** Vous devez utiliser le [service Sauvegarde Azure](https://azure.microsoft.com/services/backup/) ou des [captures instantanées cohérentes](#alternative-solution-consistent-snapshots).

Hello Voici un résumé des solutions de récupération d’urgence.

| Scénario | Réplication automatique | Solution de récupération d’urgence |
| --- | --- | --- |
| *Disques stockage Premium* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Disques gérés* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Disques LRS non managés* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Disques GRS non managés* | Inter-région ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Captures instantanées cohérentes](#alternative-solution-consistent-snapshots) |
| *Disques RA-GRS non managés* | Inter-région ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Captures instantanées cohérentes](#alternative-solution-consistent-snapshots) |

Haute disponibilité peut par répond le mieux à l’aide de hello de disques gérés dans un groupe à haute disponibilité avec Azure Backup. Si vous utilisez des disques non managés, vous pouvez toujours utiliser Sauvegarde Azure pour la récupération d’urgence. Si vous êtes toouse Impossible d’Azure Backup, puis en [instantanés cohérents avec](#alternative-solution-consistent-snapshots) comme décrit dans une section ultérieure est une autre solution de sauvegarde et de récupération d’urgence.

Vos choix pour la haute disponibilité, la sauvegarde et la récupération d’urgence aux niveaux Application et Infrastructure peuvent être représentés comme suit :

| *Niveau* | Haute disponibilité   | Sauvegarde/récupération d’urgence |
| --- | --- | --- |
| *Application* | SQL Always On | Azure Backup |
| *Infrastructure*  | Groupe à haute disponibilité  | GRS avec captures instantanées cohérentes |

### <a name="using-hello-azure-backup-service"></a>À l’aide de hello Service de sauvegarde Azure

[Sauvegarde Azure](../backup/backup-azure-vms-introduction.md) peut sauvegarder vos machines virtuelles Windows ou Linux toohello coffre Azure Recovery Services en cours d’exécution. Sauvegarde et restauration des données critiques est compliqué par le fait de hello données critiques doivent être sauvegardées lors des applications hello qui produisent des données sont en cours d’exécution de hello. tooaddress, Azure Backup offre des sauvegardes cohérentes avec les applications pour les charges de travail Microsoft à l’aide de hello tooensure de Service de cliché instantané de Volume (VSS) que les données écrites correctement toostorage. Pour les machines virtuelles Linux, seules les sauvegardes avec cohérence de fichiers sont possibles, Linux n’ayant pas tooVSS équivalent de fonctionnalité.

![][1]

Lors de la sauvegarde Azure initie une opération de sauvegarde au moment de hello planifiée, il déclenche hello sauvegarde d’extension sont installées dans hello VM tootake un instantané de point-à-temps. Un instantané est réalisé en coordination avec VSS tooget un instantané cohérent des disques virtuels hello hello sans avoir tooshut il vers le bas. extension de sauvegarde Hello Bonjour VM vide toutes les écritures avant d’effectuer des instantanés cohérent de hello de tous les disques hello. Après la réalisation de l’instantané d’hello, les données de salutation sont transférées par le coffre de sauvegarde Azure Backup toohello. toomake hello processus de sauvegarde plus efficace, service de hello identifie et transfère uniquement les blocs de hello de données qui ont été modifiées depuis la dernière sauvegarde de hello.


toorestore, vous pouvez afficher les sauvegardes disponibles hello via Azure Backup et puis lancez une restauration. Vous pouvez créer et restaurer des sauvegardes Azure via hello [portail Azure](https://portal.azure.com/), [à l’aide de PowerShell](../backup/backup-azure-vms-automation.md ), ou à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/azure/xplat-cli-install). Pour plus d’informations, consultez la page relative à Sauvegarde Azure.

### <a name="steps-tooenable-backup"></a>Étapes tooEnable sauvegarde

Hello étapes suivantes sont généralement utilisées tooenable des sauvegardes de vos machines virtuelles à l’aide de hello [Azure Portal](https://portal.azure.com/). Cela peut varier légèrement en fonction de votre scénario. Consultez toohello [Azure Backup](../backup/backup-azure-vms-introduction.md) documentation pour plus de détails. Sauvegarde Azure [prend également en charge les machines virtuelles avec des disques managés](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Créez un coffre recovery services pour une machine virtuelle à l’aide de hello comme suit :

    a.  À l’aide de hello [portail Azure](https://portal.azure.com/), parcourir toutes les ressources, puis recherchez « Coffres des Services de récupération ».

    b.  Sur hello les Services de récupération des coffres de menu, cliquez sur Ajouter et suivez hello étapes toocreate un nouvel archivage Bonjour même région que hello machine virtuelle. Par exemple, si votre machine virtuelle est dans la région ouest des États-Unis, vous pouvez choisir ouest des États-Unis pour l’archivage de hello.

2.  Vérifiez la réplication du stockage hello pour hello nouvellement créé le coffre. toodo, accès hello coffre-fort à partir de hello Recovery Services coffres lame et passer toohello paramètres/sauvegarde Configuration. Vérifiez hello option de GRS est sélectionné par défaut. Cela garantit que votre coffre est le centre de données secondaire tooa automatiquement répliquées. Par exemple, votre coffre de l’ouest des États-Unis seront automatiquement répliquée tooEast des États-Unis.

3.  Configurer la stratégie de sauvegarde hello et sélectionnez hello machine virtuelle à partir de hello même interface utilisateur.

4.  Vérifiez que hello que Backup Agent est installé sur hello machine virtuelle. Si votre machine virtuelle est créée à l’aide d’une image de la galerie Azure, cela signifie que l’agent de sauvegarde hello est déjà installé. Sinon (autrement dit, si vous utilisez une image personnalisée), utilisez les instructions trop[hello Install Agent de machine virtuelle sur l’ordinateur virtuel de hello](../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  Assurez-vous que cette machine virtuelle hello permet la connectivité réseau pour toofunction du service de sauvegarde hello. Suivez ces instructions relatives à la [connectivité réseau](../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Une fois terminés hello étapes ci-dessus, une sauvegarde hello sera exécutée à intervalles réguliers, comme spécifié dans la stratégie de sauvegarde hello. Si nécessaire, vous pouvez déclencher la première sauvegarde de hello manuellement à partir du tableau de bord coffre hello sur hello portail Azure.

Pour automatiser la sauvegarde Azure à l’aide de scripts, consultez trop[applets de commande PowerShell pour la sauvegarde de la machine virtuelle](../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Étapes de récupération

Si vous avez besoin de toorepair ou reconstruisez une machine virtuelle, vous pouvez restaurer hello machine virtuelle à partir d’un des points de récupération d’une sauvegarde hello dans le coffre hello. Il existe deux options différentes pour la récupération de hello :

1.  Vous pouvez créer une machine virtuelle en tant que représentation jusqu’à une date et une heure de votre machine virtuelle sauvegardée.

2.  Vous pouvez restaurer les disques hello et ensuite utiliser le modèle de hello pour toocustomize de machine virtuelle hello et reconstruction hello restauré la machine virtuelle. 

Consultez les instructions[utilisez Azure portail toorestore virtuels](../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). document de Hello explique également les étapes spécifiques de hello pour la restauration du centre de données associés sauvegardé machines virtuelles toohello à l’aide de votre coffre de sauvegarde géo-redondant dans les cas de hello d’un incident au centre de données principal hello. Dans ce cas, Azure Backup utilise le service de calcul hello de la machine virtuelle de hello région secondaire toocreate hello restaurée.

Vous pouvez également utiliser PowerShell pour [restaurer une machine virtuelle](../backup/backup-azure-vms-automation.md#restore-an-azure-vm) ou [créer une machine virtuelle à partir de disques restaurés](../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Solution alternative : captures instantanées cohérentes

Si vous êtes toouse Impossible hello Service Azure Backup, vous pouvez implémenter votre propre mécanisme de sauvegarde à l’aide de captures instantanées. Il est compliqué toocreate captures instantanées cohérentes pour tous les disques utilisés par un ordinateur virtuel et puis de répliquer ces région tooanother de captures instantanées. Pour cette raison, Azure considère que le Service de sauvegarde de hello en tirant parti une meilleure option que la création d’une solution personnalisée. Si vous utilisez le stockage de RA-GRS/GRS pour les disques, les instantanés sont automatiquement répliquées tooa les centre de données secondaire. Si vous utilisez le stockage LRS pour les disques, vous devez les données de salutation tooreplicate vous-même. Pour plus d’informations, consultez [Sauvegarder les disques de machines virtuelles Azure non gérés avec des captures instantanées incrémentielles](storage-incremental-snapshots.md).

Une capture instantanée est une représentation sous la forme d’un objet à un point spécifique dans le temps. Un instantané entraîne la facturation pour la taille de hello incrémentielle des données de hello contient. Pour plus d’informations, consultez [Création d’un instantané d’objet blob](storage-blob-snapshots.md).

### <a name="creating-snapshots-while-hello-vm-is-running"></a>Création d’instantanés hello lors de la machine virtuelle est en cours d’exécution

Pendant que vous pouvez prendre un instantané à tout moment, si hello machine virtuelle est en cours d’exécution, est toujours en cours de diffusion toohello disques de données, et les instantanés hello peuvent contenir des opérations partielles qui étaient en cours. En outre, si plusieurs disques sont impliqués, instantanés hello des différents disques peuvent être survenu à des moments différents, ce qui signifie que ces instantanés ne peuvent pas être coordonnés. Cela est particulièrement problématique pour les volumes agrégés par bandes dont les fichiers peuvent être endommagés si des modifications sont apportées pendant la sauvegarde.

tooavoid cette situation, le processus de sauvegarde hello doit implémenter hello comme suit :

1.  Figer tous les disques hello

2.  Vider hello toutes les écritures en attente

3.  Ensuite, [créer un instantané d’objet blob](storage-blob-snapshots.md) pour tous les hello disques

Certaines applications de Windows telles que SQL Server fournissent un mécanisme de sauvegarde coordonné via des sauvegardes cohérentes avec les applications toocreate VSS. Sur Linux, vous pouvez utiliser un outil tel que fsfreeze pour la coordination des disques hello, qui fourniront des sauvegardes cohérentes de fichier, mais pas application instantanés cohérents au niveau. Ce processus étant compliqué, envisagez d’utiliser le service [Sauvegarde Azure](../backup/backup-azure-vms-introduction.md) ou une solution de sauvegarde tierce qui implémente déjà cela.

Hello ci-dessus processus entraîne une collection d’instantanés coordonnés pour tous les disques de machine virtuelle hello, représentant une vue spécifique de point-à-temps de hello machine virtuelle. Il s’agit d’un point de restauration de sauvegarde pour hello machine virtuelle. Vous pouvez répéter le processus de hello lors des sauvegardes périodiques des intervalles planifiés toocreate. Voir ci-dessous pour connaître les étapes hello trop[région de copie hello sauvegardes tooanother](#copy-the-snapshots-to-another-region) pour la récupération d’urgence.

### <a name="creating-snapshots-while-hello-vm-is-offline"></a>Création d’instantanés hello lors de la machine virtuelle est en mode hors connexion

Des sauvegardes cohérentes une autre option toocreate en cours d’arrêt hello machine virtuelle et d’objet blob de prendre des instantanés de chaque disque. Cette opération est plus facile que de coordonner les captures instantanées d’une machine virtuelle en cours d’exécution, mais elle nécessite un temps d’arrêt de quelques minutes. Pour ce processus, procédez comme suit :

1. Arrêtez hello machine virtuelle.

2. Créez une capture instantanée de chaque blob de disque dur virtuel. Cette opération ne prend que quelques secondes.

    toocreate un instantané, vous pouvez utiliser [PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), hello [API Rest de stockage Azure](https://msdn.microsoft.com/library/azure/ee691971.aspx), [CLI d’Azure](https://docs.microsoft.com/azure/xplat-cli-install), ou l’une des bibliothèques du Client du stockage Azure hello comme [ bibliothèque cliente de stockage Hello pour .NET](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Démarrez hello machine virtuelle, ce qui se termine par des temps d’arrêt hello. En général, processus hello se termine dans quelques minutes.

Ce processus génère une collection de captures instantanées cohérentes pour tous les disques de hello, qui fournit un point de restauration de sauvegarde pour hello machine virtuelle. Voir ci-dessous pour hello étapes toocopy hello instantanés tooanother la région pour la récupération d’urgence.

### <a name="copy-hello-snapshots-tooanother-region"></a>Copier la région de hello instantanés tooanother

Création d’instantanés hello seuls peut ne pas suffire pour la récupération d’urgence. Vous devez également répliquer la région de tooanother de sauvegardes de capture instantanée hello.

Si vous utilisez GRS ou RA-GRS pour vos disques, puis hello les instantanés sont répliqués toohello la région secondaire automatiquement. Il peut y avoir quelques minutes de retard avant la réplication hello et si le centre de données principal hello tombe en panne avant de terminer la réplication des instantanés de hello, vous ne serez pas en mesure de tooaccess des instantanés de hello à partir du centre de données secondaire hello. probabilité Hello de ce est faible.

> [!Note] 
> Ayant uniquement des disques de hello dans un compte GRS ou RA-GRS ne protège pas hello machine virtuelle à un incident. Vous devez également créer des captures instantanées coordonnées ou utiliser Sauvegarde Azure. Il s’agit de toorecover requis un état cohérent tooa de machine virtuelle.

Si vous utilisez LRS, vous devez copier hello instantanés tooa autre compte de stockage immédiatement après la création de capture instantanée de hello. la cible de copie Hello peut être un compte de stockage LRS dans une autre région, entraîne la copie de hello en cours d’une région à distance. Vous pouvez également copier le compte de stockage hello instantané tooan RA-GRS Bonjour même région. Dans ce cas, les instantanés hello sera toohello tardivement répliquées de région secondaire distant. La sauvegarde est protégée contre les sinistres au site principal de hello une fois hello copie et la réplication terminée.

toocopy vos instantanés incrémentiels pour la récupération d’urgence efficace, passez en revue les instructions hello dans [sauvegarde des disques de machine virtuelle non managées Azure avec des instantanés incrémentiels](storage-incremental-snapshots.md).

![][2]

### <a name="recovery-from-snapshots"></a>Récupération à partir de captures instantanées

tooretrieve un instantané, copiez-le toomake un nouvel objet blob. Si vous copiez à partir du compte de principal hello instantané d’hello, vous pouvez copier hello instantané sur l’objet blob de base toohello d’instantané hello, donc rétablissement hello toohello snapshot de disque ; Il s’agit en tant que la promotion de capture instantanée de hello. Si vous copiez la sauvegarde d’instantanés hello à partir d’un compte secondaire (en cas de hello de RA-GRS), il doit être copié tooa le compte principal. Vous pouvez copier un instantané [à l’aide de PowerShell](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) ou à l’aide d’utilitaire AzCopy de hello. Pour plus d’informations, consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).

Dans le cas de hello de machines virtuelles avec plusieurs disques, vous devez copier tous les instantanés de hello qui font partie des mêmes coordonnées de hello point de restauration. Une fois que vous copiez des objets BLOB de hello instantanés toowritable disque dur virtuel, vous pouvez utiliser toorecreate d’objets BLOB hello votre machine virtuelle à l’aide du modèle de hello pour hello machine virtuelle.

## <a name="other-options"></a>Autres options

### <a name="sql-server"></a>SQL Server

SQL Server s’exécutant dans une machine virtuelle a ses propres fonctionnalités intégrées de toobackup votre tooAzure de base de données SQL Server stockage d’objets Blob ou un partage de fichiers. Si le compte de stockage hello est GRS ou RA-GRS, vous pouvez accéder à ces sauvegardes dans le centre de données secondaire du compte de stockage hello dans l’événement hello de sinistre, avec hello soumis aux mêmes restrictions, comme indiqué précédemment. Pour plus d’informations, voir [Sauvegarde et restauration de SQL Server dans les machines virtuelles Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). Dans toobackup d’addition et de restauration, [SQL Server groupes de disponibilité AlwaysOn](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) peut mettre à jour les réplicas secondaires de bases de données toogreatly réduisent les temps de récupération d’urgence hello.

## <a name="other-considerations"></a>Autres points à considérer

Cet article a examiné comment toobackup ou prendre des instantanés de vos machines virtuelles et de récupération d’urgence toosupport leurs disques et comment toouse ces toorecover. Avec le modèle de gestionnaire de ressources Azure hello, de nombreuses personnes utilisent les modèles toocreate leurs ordinateurs virtuels et autres infrastructures dans Azure. Vous pouvez utiliser un modèle de toocreate un ordinateur virtuel qui a hello configuration même chaque fois. Si vous utilisez des images personnalisées pour la création de vos machines virtuelles, vous devez également vous assurer que vos images sont protégés à l’aide d’un toostore de compte RA-GRS les.

Par conséquent, votre processus de sauvegarde peut être une combinaison de deux éléments :

1. Données de sauvegarde hello (disques)
2. Configuration de sauvegarde hello (modèles, des images personnalisées)

Selon l’option de sauvegarde hello que vous choisissez, vous n’avez peut-être toohandle hello sauvegarder à la fois hello données et configuration de hello ou service de sauvegarde hello peut gérer tout cela pour vous.

## <a name="appendix---understanding-hello-impact-of-lrs-grs-and-ra-grs"></a>Annexe - comprendre impact hello de LRS, GRS et RA-GRS

Pour les comptes de stockage dans Azure, il existe trois types de redondance de données que vous devez prendre en compte lors d’une récupération d’urgence : le stockage localement redondant (LRS), le stockage géoredondant (GRS) ou le stockage géoredondant avec accès en lecture (RA-GRS). 

Localement le stockage redondant (LRS) conserve trois copies de données hello Bonjour même centre de données. Lors de l’écriture des données de hello, tous les trois copies sont mises à jour avant de réussite est renvoyée toohello appelant, afin de savoir qu’ils sont identiques. Votre disque est protégé contre les pannes locales, car il est très peu probable que toutes les trois copies est affectés au hello même temps. Dans les cas de hello de LRS, il n’étant aucune géo-redondance, disque de hello n’est pas protégée contre les défaillances graves que peuvent avoir un impact sur une unité de stockage ou de centre de données.

GRS et RA-GRS, trois copies de vos données sont conservées dans la région principale de hello (que vous avez choisie), et plus de trois copies de vos données sont conservées dans une région secondaire correspondante (définie par Azure). Par exemple, si vous stockez des données dans l’ouest des États-Unis, les données de salutation seront répliquée tooEast des États-Unis. Cette opération est effectuée en mode asynchrone, et il existe un bref délai entre les mises à jour toohello principaux et secondaire. Réplicas de disques hello sur le site secondaire de hello sont cohérentes sur une base par disque (avec un délai hello), mais les réplicas de plusieurs disques actives ne peuvent pas être synchronisés **entre eux**. toohave des réplicas cohérents sur plusieurs disques, les captures instantanées cohérentes sont nécessaires.

Hello principale différence entre GRS et RA-GRS est qu’avec RA-GRS, vous pouvez lire la copie secondaire de hello à tout moment. S’il existe un problème qui rend les données hello dans la région principale de hello inaccessible, hello équipe Azure rend tous les accès toorestore effort. Alors que hello principal est en panne, si vous avez RA-GRS est activé, vous pouvez accéder à des données hello dans le centre de données secondaire hello. Par conséquent, si vous envisagez tooread à partir du réplica de hello tandis que hello principal n’est pas accessible, puis RA-GRS doit être envisagé.

S’il s’avère toobe une interruption importante, hello équipe Azure peut déclencher un basculement géographique et modifier toopoint toosecondary stockage hello principal DNS entrées. À ce stade, si vous avez deux GRS ou RA-GRS est activé, vous pouvez accéder données hello dans une région hello utilisé hello toobe secondaire. En d’autres termes, si votre compte de stockage est GRS, et il existe un problème, vous pouvez accéder au stockage de secondaire de hello uniquement s’il existe un basculement géographique.

Pour plus d’informations, consultez [le toodo en cas de panne de stockage Azure](storage-disaster-recovery-guidance.md). 

Notez que Microsoft contrôle si un basculement se produit. Le basculement n’est pas contrôlé par le compte de stockage. Par conséquent, il n’est pas décidé par les clients individuels. tooimplement la récupération d’urgence pour les comptes de stockage spécifique ou de disques de machine virtuelle, vous devez utiliser hello techniques décrites précédemment dans cet article.



[1]: ./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png
[2]: ./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png