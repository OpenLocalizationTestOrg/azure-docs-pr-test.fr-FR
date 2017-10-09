---
title: "sauvegarde de HANA Azure aaaSAP basée sur des instantanés de stockage | Documents Microsoft"
description: "Il existe deux grandes méthodes permettant d’effectuer des sauvegardes SAP HANA sur des machines virtuelles Azure. Cet article aborde la sauvegarde SAP HANA à partir de captures instantanées de stockage"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a>Sauvegarde SAP HANA à partir de captures instantanées de stockage

## <a name="introduction"></a>Introduction

Ce document fait partie d’une série d’articles connexes en trois parties dédiés à la sauvegarde SAP HANA. [Guide de sauvegarde pour SAP HANA sur des Machines virtuelles Azure](sap-hana-backup-guide.md) fournit une vue d’ensemble et des informations sur la prise en main, et [SAP HANA Azure Backup au niveau du fichier](sap-hana-backup-file-level.md) couvre hello option basée sur le fichier de sauvegarde.

Lorsque vous utilisez une fonctionnalité de sauvegarde de machine virtuelle pour un système de démonstration de tout-en-un à instance unique, il doit considérer d’effectuer une sauvegarde de la machine virtuelle au lieu de la gestion des sauvegardes HANA à hello au niveau du système d’exploitation. Une alternative consiste à tootake objets blob Azure instantanés toocreate des copies de disques virtuels individuels qui sont tooa joint l’ordinateur virtuel et conserver les fichiers de données HANA hello. Mais un point critique est la cohérence d’application lors de la création d’un instantané de sauvegarde ou de disque de machine virtuelle alors que le système de hello et en cours d’exécution. Consultez _la cohérence des données SAP HANA lors de la prise d’instantanés de stockage_ dans l’article hello [guide de sauvegarde pour SAP HANA sur des Machines virtuelles Azure](sap-hana-backup-guide.md). SAP HANA dispose d’une fonction qui prend en charge ces types de captures instantanées de stockage.

## <a name="sap-hana-snapshots"></a>Captures instantanées de SAP HANA

Il existe dans SAP HANA une fonctionnalité qui prend en charge la création de captures instantanées de stockage. Toutefois, à compter de 2016 de décembre, il existe une restriction des systèmes de toosingle-container. Les configurations de conteneur multitenant ne gèrent pas ce type de capture instantanée de la base de données (voir [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) [Créer une capture instantanée de stockage (SAP HANA Studio)]).

Elle fonctionne de la manière suivante :

- Préparer un instantané du stockage en lançant l’instantané de SAP HANA hello
- Exécuter hello capture instantanée de stockage (Azure blob capture instantanée, par exemple)
- Confirmer l’instantané de SAP HANA hello

![Cette capture d’écran montre qu’une capture instantanée des données SAP HANA peut être créée via une instruction SQL](media/sap-hana-backup-storage-snapshots/image011.png)

Cette capture d’écran montre qu’une capture instantanée des données SAP HANA peut être créée via une instruction SQL.

![Hello d’instantané puis apparaît également dans le catalogue de sauvegarde hello dans SAP HANA Studio](media/sap-hana-backup-storage-snapshots/image012.png)

Hello d’instantané puis apparaît également dans le catalogue de sauvegarde hello dans SAP HANA Studio.

![Sur le disque, les instantanés hello s’affiche dans le répertoire de données SAP HANA hello](media/sap-hana-backup-storage-snapshots/image013.png)

Sur le disque, les instantanés hello s’affiche dans le répertoire de données SAP HANA hello.

L’un est tooensure fsck hello est également garantie avant d’exécuter la capture instantanée de stockage hello tandis que SAP HANA est en mode de préparation d’instantané hello. Consultez _la cohérence des données SAP HANA lors de la prise d’instantanés de stockage_ dans l’article hello [guide de sauvegarde pour SAP HANA sur des Machines virtuelles Azure](sap-hana-backup-guide.md).

Une fois l’instantané du stockage hello est terminé, il est instantané de SAP HANA hello tooconfirm critiques. Il existe un toorun d’instruction SQL correspondante : fermer instantané des données de sauvegarde (voir [sauvegarde données instantané clôturer (sauvegarde et récupération)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).

> [!IMPORTANT]
> Confirmer la capture instantanée HANA hello. Échéance trop&quot;copie sur écriture&quot; SAP HANA peuvent nécessiter espace disque supplémentaire à instantané en mode de préparation, et il n’est pas possible de toostart nouvelles sauvegardes jusqu'à ce que l’instantané de SAP HANA hello est confirmée.

## <a name="hana-vm-backup-via-azure-backup-service"></a>Sauvegarde de machines virtuelles HANA via le service Azure Backup

À compter de 2016 de décembre, l’agent de sauvegarde hello Hello service Azure Backup n’est pas disponible pour les machines virtuelles Linux. utilisation de toomake de sauvegarde Azure au niveau fichier/répertoire hello, un serait copier les fichiers de sauvegarde de SAP HANA tooa machine virtuelle Windows et ensuite utiliser l’agent de sauvegarde hello. Dans le cas contraire, seule une sauvegarde complète de Linux VM est possible via le service de sauvegarde Azure hello. Consultez [fonctionnalités de la vue d’ensemble de hello dans Azure Backup](../../../backup/backup-introduction-to-azure-backup.md) toofind plus d’informations.

Hello service Azure Backup offre une option tooback jusqu'à et de restauration d’une machine virtuelle. Vous trouverez plus d’informations sur ce service et comment il fonctionne dans l’article de hello [planifier votre infrastructure de sauvegarde de machine virtuelle dans Azure](../../../backup/backup-azure-vms-introduction.md).

Il existe deux considérations importantes en fonction de l’article de toothat :

_&quot;Pour les ordinateurs virtuels Linux, uniquement des sauvegardes cohérentes de fichier sont possibles, car Linux n’a pas un tooVSS plate-forme équivalente.&quot;_

_&quot;Les applications doivent tooimplement leurs propres &quot;correction&quot; mécanisme sur hello restauré les données.&quot;_

Par conséquent, l’un est toomake que SAP HANA se trouve dans un état cohérent sur le disque lors du démarrage hello sauvegarde. Consultez _instantanés de SAP HANA_ décrit plus haut dans le document de hello. Mais le fait que SAP HANA reste dans ce mode de préparation de captures instantanées soulève un problème potentiel. Pour plus d’informations, consultez la page [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) [Créer une capture instantanée de stockage (SAP HANA Studio]).

Cet article indique :

_&quot;Il est fortement recommandé de tooconfirm ou abandonner une capture instantanée de stockage dès que possible après que qu’elle a été créée. Lors de la capture instantanée de stockage hello est en cours de préparation ou créé, hello données pertinentes de l’instantané sont figées. Alors que les données pertinentes de l’instantané hello restent figées, peut toujours être apportées dans la base de données hello. Ces modifications n’entraîne pas hello figée toobe pertinentes de l’instantané de données modifiée. Au lieu de cela, les modifications de hello sont écrites toopositions zone de données hello distinctes à partir de l’instantané du stockage hello. Modifications concernent également toohello journal. Toutefois, hello hello relatifs à la capture instantanée des données sont conservées figées, hello hello plus volume de données peut augmenter.&quot;_

Sauvegarde Azure s’occupe de la cohérence de système de fichier hello via les extensions de machine virtuelle Azure. Ces extensions ne sont pas disponibles sous une forme autonome et fonctionnent uniquement en association avec le service  Sauvegarde Azure. Cependant, il est toujours un toomanage exigence une cohérence d’application SAP HANA instantané tooguarantee.

Le service Sauvegarde Azure se décompose en deux grandes phases :

- Création d’une capture instantanée
- Transfert de données toovault

Ainsi, confirmer l’instantané de SAP HANA hello issue de la phase de service de sauvegarde Azure hello d’une capture instantanée. Cela peut prendre plusieurs minutes toosee hello portail Azure.

![Cette illustration montre une partie de la liste de sauvegarde hello d’un service Azure Backup](media/sap-hana-backup-storage-snapshots/image014.png)

Cette illustration montre une partie de liste de tâche de sauvegarde hello d’un service Azure Backup, qui était utilisé tooback de machine virtuelle de test HANA hello.

![Détails de la tâche tooshow hello, cliquez sur le travail de sauvegarde hello Bonjour portail Azure](media/sap-hana-backup-storage-snapshots/image015.png)

Détails de la tâche hello tooshow, cliquez sur la tâche de sauvegarde de hello Bonjour portail Azure. Ici, un peut voir hello deux phases. Il peut prendre quelques minutes jusqu'à ce qu’il indique la phase de capture instantanée hello comme terminée. La plupart du temps de hello est consacré à la phase de transfert de données hello.

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a>Automatisation des sauvegardes de machines virtuelles HANA via le service Azure Backup

Un confirmer manuellement instantané de SAP HANA hello une fois la phase de capture instantanée de sauvegarde Azure hello est terminée, comme décrit précédemment, mais il est utile de tooconsider automation, car un administrateur peut ne pas analyser la liste de sauvegarde hello Bonjour portail Azure.

Voici comment effectuer cette automatisation via des applets de commande Azure PowerShell.

![Un service Azure Backup a été créé avec hello nom hana--coffre de sauvegarde](media/sap-hana-backup-storage-snapshots/image016.png)

Un service Azure Backup a été créé avec le nom de hello &quot;hana-sauvegarde-coffre.&quot; hello commande PS **AzureRmRecoveryServicesVault de Get-nom du coffre de sauvegarde hana** récupère hello objet correspondant. Cet objet est ensuite utilisé tooset hello contexte sauvegarde, comme l’illustre la figure suivante hello.

![Consultez pour la tâche de sauvegarde hello actuellement en cours](media/sap-hana-backup-storage-snapshots/image017.png)

Après le paramètre hello contexte un qui peut vérifier pour la tâche de sauvegarde hello est en cours et puis rechercher les détails de la tâche. liste des tâches subordonnées Hello montre si hello instantané phase de hello du travail de sauvegarde Azure est déjà terminée :

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![Valeur de hello d’interrogation dans une boucle jusqu'à ce qu’il s’avère tooCompleted](media/sap-hana-backup-storage-snapshots/image018.png)

Une fois que les détails d’une tâche hello sont stockés dans une variable, il est simplement PS syntaxe tooget toohello première entrée de tableau et récupérer la valeur d’état hello. script d’automatisation toocomplete hello, valeur hello de sondage dans une boucle jusqu'à ce qu’il devient trop&quot;terminé.&quot;

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a>Clé de licence HANA et restauration de machine virtuelle via le service Sauvegarde Azure

Hello service Azure Backup est conçue toocreate un nouvel ordinateur virtuel pendant la restauration. Il n’existe aucun plan pour le moment toodo un &quot;in situ&quot; restauration d’une machine virtuelle Azure existante.

![Cette figure illustre l’option de restauration hello Hello service Azure Bonjour portail Azure](media/sap-hana-backup-storage-snapshots/image019.png)

Cette illustration montre l’option de restauration hello Hello service Azure Bonjour portail Azure. Une peut choisir entre la création d’un ordinateur virtuel pendant la restauration ou la restauration des disques de hello. Après la restauration des disques hello, il est encore nécessaire toocreate par-dessus une machine virtuelle. Chaque fois qu’un nouvel ordinateur virtuel est créé sur les modifications d’ID de machine virtuelle uniques Azure hello (consultez [accès et l’ID Unique de la machine virtuelle Azure à l’aide de](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).

![Cette figure illustre l’ID unique de machine virtuelle Azure hello avant et après la restauration de hello via le service de sauvegarde Azure](media/sap-hana-backup-storage-snapshots/image020.png)

Cette illustration montre l’ID unique de machine virtuelle Azure hello avant et après la restauration de hello via le service de sauvegarde Azure. clé matérielle Hello SAP, qui est utilisé pour le Gestionnaire de licences de SAP, à l’aide de cet ID de machine virtuelle unique. Par conséquent, une nouvelle licence SAP a toobe installé après une restauration de la machine virtuelle.

Une nouvelle fonctionnalité Azure Backup a été présentée en mode aperçu lors de la création de hello de ce guide de sauvegarde. Il permet une restauration au niveau du fichier en fonction de l’instantané d’ordinateur virtuel hello qui a été effectuée pour hello VM sauvegarde. Cela évite de hello besoin toodeploy un nouvel ordinateur virtuel et par conséquent reste d’ID de machine virtuelle unique hello hello même et aucune nouvelle clé de licence SAP HANA n’est requis. Vous trouverez plus d’informations sur cette fonctionnalité une fois qu’elle sera entièrement testée.

Sauvegarde Azure sera finalement autoriser la sauvegarde de différents disques virtuels Azure, ainsi que les fichiers et répertoires à partir à l’intérieur de machine virtuelle hello. Un avantage majeur d’Azure Backup est sa gestion de toutes les sauvegardes de hello, l’enregistrement de client de hello de ne pas avoir de toodo il. Si une restauration s’avère nécessaire, Azure Backup sélectionne hello toouse de sauvegarde correcte.

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a>Sauvegarde de machine virtuelle SAP HANA via une capture instantanée manuelle du disque

Au lieu d’utiliser le service de sauvegarde Azure hello, un pu configurer une solution de sauvegarde individuelle en créant des instantanés d’objet blob de disques durs virtuels de Azure manuellement via PowerShell. Consultez [instantanés d’objet blob à l’aide avec PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) pour obtenir une description des étapes de hello.

Elle offre plus de souplesse, mais ne résout pas les problèmes de hello expliqués plus haut dans ce document :

- Il faut toujours veiller à ce que SAP HANA reste à l’état cohérent
- Impossible de remplacer le disque du système d’exploitation Hello même si hello que machine virtuelle est libérée en raison d’une erreur indiquant qu’un bail existant. Il fonctionne uniquement après la suppression de hello machine virtuelle, ce qui signifierait tooa nouveau unique ID de machine virtuelle et hello besoin tooinstall une nouvelle licence SAP.

![Il est possible toorestore uniquement des disques de données hello d’une machine virtuelle Azure](media/sap-hana-backup-storage-snapshots/image021.png)

Il est possible toorestore uniquement les disques de données hello d’une machine virtuelle Azure, en évitant hello tout problème d’obtention d’un nouvel ID de machine virtuelle unique et invalidé par conséquent, des licences SAP hello :

- Pour le test de hello, deux disques de données Azure ont été attachée tooa machine virtuelle et les volumes RAID logiciels a été défini sur les 
- La fonction de capture instantanée SAP HANA a permis de confirmer l’état cohérent de SAP HANA
- Système de fichiers Figer (consultez _la cohérence des données SAP HANA lors de la prise d’instantanés de stockage_ dans l’article hello [guide de sauvegarde pour SAP HANA sur des Machines virtuelles Azure](sap-hana-backup-guide.md))
- Des captures instantanées d’objets blob ont été créées à partir des deux disques de données
- Déblocage du système de fichiers
- Confirmation de la capture instantanée SAP HANA
- les deux disques de détacher et de disques de données toorestore hello, hello machine virtuelle a été arrêté
- Après le détachement des disques hello, ils ont été remplacés par des captures instantanées du blob ancien hello
- Puis hello restauré les disques virtuels ont été attachés à nouveau toohello machine virtuelle
- Une fois que l’heure de début hello machine virtuelle, tous les éléments logiciels de hello RAID fonctionnait correctement et a été redéfini toohello blob capture instantanée
- HANA a été redéfini instantané HANA toohello

S’il est possible tooshut vers le bas SAP HANA avant les instantanés d’objet blob hello, procédure de hello serait moins complexe. Dans ce cas, un peut ignorer la capture instantanée HANA hello et, si rien d’autre ne se passe dans le système de hello, également ignorer blocage hello du système de fichiers. Complexité ajouté est fourni dans l’image de hello lorsqu’il est nécessaire de toodo instantanés si tout est en ligne. Consultez _la cohérence des données SAP HANA lors de la prise d’instantanés de stockage_ dans l’article hello [guide de sauvegarde pour SAP HANA sur des Machines virtuelles Azure](sap-hana-backup-guide.md).

## <a name="next-steps"></a>Étapes suivantes
* L’article [Guide de sauvegarde pour SAP HANA sur les machines virtuelles Azure](sap-hana-backup-guide.md) fournit une vue d’ensemble et des informations sur la mise en route.
* [Sauvegarde de SAP HANA en fonction de niveau fichier](sap-hana-backup-file-level.md) couvre hello option basée sur le fichier de sauvegarde.
* toolearn comment tooestablish haute disponibilité et le plan de récupération d’urgence de SAP HANA sur Azure (instances de grande taille), consultez [SAP HANA (instances de grande taille) haute disponibilité et récupération d’urgence sur Azure](hana-overview-high-availability-disaster-recovery.md).
