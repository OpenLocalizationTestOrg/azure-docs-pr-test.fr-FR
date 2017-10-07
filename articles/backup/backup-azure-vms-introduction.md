---
title: aaaPlanning votre infrastructure de sauvegarde de machine virtuelle dans Azure | Documents Microsoft
description: "Considérations importantes lors de la planification tooback des machines virtuelles dans Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: sauvegarde de machines virtuelles
ms.assetid: 19d2cf82-1f60-43e1-b089-9238042887a9
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: d11982431610000293038ee6aa7df8e7bc2d8b70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-your-vm-backup-infrastructure-in-azure"></a>Planification de votre infrastructure de sauvegarde de machines virtuelles dans Azure
Cet article fournit des performances et la ressource toohelp de suggestions vous planifiez votre infrastructure de sauvegarde de machine virtuelle. Il définit également les principaux aspects hello du service de sauvegarde ; Ces aspects peuvent être essentiels dans la définition de votre architecture, la planification des capacités et la planification. Si vous avez [préparé votre environnement](backup-azure-vms-prepare.md), la planification est l’étape suivante de hello avant de commencer [tooback des machines virtuelles](backup-azure-vms.md). Si vous avez besoin de plus d’informations sur les machines virtuelles, consultez hello [documentation de Machines virtuelles](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="how-does-azure-back-up-virtual-machines"></a>Comment Azure sauvegarde-t-il des machines virtuelles Azure ?
Hello service Azure Backup lorsqu’un travail de sauvegarde au moment de hello planifiée, il déclenche hello extension de sauvegarde tootake un instantané de point-à-temps. Hello service Azure Backup utilise hello _VMSnapshot_ extension dans Windows et hello _VMSnapshotLinux_ extension dans Linux. extension de Hello est installée au cours de la première sauvegarde de machine virtuelle hello. extension de hello tooinstall, hello machine virtuelle doit s’exécuter. Si hello machine virtuelle ne fonctionne pas, hello service de sauvegarde prend un instantané de hello stockage sous-jacent (dans la mesure où aucune écriture de l’application se produire lors de la machine virtuelle est arrêtée de hello).

Lorsque vous prenez un instantané de machines virtuelles Windows, service de sauvegarde hello coordonne hello Volume Shadow Copy Service (VSS) tooget un instantané cohérent des disques de l’ordinateur virtuel de hello. Si vous sauvegardez les machines virtuelles Linux, vous pouvez écrire votre propre cohérence tooensure de scripts personnalisés lorsque vous prenez un instantané de la machine virtuelle. Des détails relatifs à l’appel de ces scripts sont fournis plus loin dans cet article.

Une fois que hello service Azure Backup prend un instantané de hello, données de hello sont transférées toohello coffre. l’efficacité toomaximize, hello service identifie et transfère uniquement les blocs de hello de données qui ont été modifiés depuis la sauvegarde précédente de hello.

![Architecture de la sauvegarde des machines virtuelles Azure](./media/backup-azure-vms-introduction/vmbackup-architecture.png)

Lorsque le transfert de données hello est terminé, les instantanés hello sont supprimé et un point de récupération est créé.

> [!NOTE]
> 1. Au cours du processus de sauvegarde hello, Azure Backup n’inclut pas hello disque temporaire attaché toohello virtual machine. Pour plus d’informations, voir le blog de hello sur [stockage temporaire](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/).
> 2. Étant donné que Azure Backup prend un instantané au niveau du stockage et les transferts toovault de capture instantanée, ne modifiez pas les clés de compte de stockage hello jusqu'à ce que la fin du travail de sauvegarde hello.
> 3. Pour les machines virtuelles premium, nous copions compte toostorage de capture instantanée hello. Il s’agit de toomake assurer que service Azure Backup IOPS suffisant pour le transfert de données toovault. Cette copie supplémentaire de stockage est facturée conformément à hello machine virtuelle de la taille allouée. 
>

### <a name="data-consistency"></a>Cohérence des données
Sauvegarde et restauration des données critiques sont compliqué par le fait de hello données critiques doivent être sauvegardées lors des applications hello qui produisent des données sont en cours d’exécution de hello. tooaddress, Azure Backup prend en charge les sauvegardes cohérentes avec les applications pour Windows et les machines virtuelles Linux
#### <a name="windows-vm"></a>Machine virtuelle Windows
Azure Backup effectue la sauvegarde complète VSS sur les machines virtuelles Windows (en savoir plus sur la [sauvegarde complète VSS](http://blogs.technet.com/b/filecab/archive/2008/05/21/what-is-the-difference-between-vss-full-backup-and-vss-copy-backup-in-windows-server-2008.aspx)). sauvegardes de copie VSS tooenable, hello suivant les besoins de la clé de Registre toobe définie sur hello machine virtuelle.

```
[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
"USEVSSCOPYBACKUP"="TRUE"
```

#### <a name="linux-vms"></a>Machines virtuelles Linux
Le service Sauvegarde Azure fournit une infrastructure de script. tooensure la cohérence des applications lors de la sauvegarde d’ordinateurs virtuels Linux, créer des scripts personnalisés avant et post-scripts qui contrôlent le flux de travail sauvegarde hello et l’environnement. Sauvegarde Azure appelle le script avant de hello avant d’effectuer l’instantané d’ordinateur virtuel hello et appelle postérieurs aux scripts hello une fois le travail de capture instantanée d’ordinateur virtuel hello se termine. Pour plus d’informations, voir [Sauvegarde cohérente des applications des machines virtuelles Linux à l’aide de pré-scripts et de post-scripts](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).
> [!NOTE]
> Sauvegarde Azure appelle uniquement hello écrits par le client avant et après des scripts. Si post-scripts et script avant de hello s’exécutent correctement, Azure Backup marque point de récupération hello en tant qu’application cohérente. Toutefois, les clients hello sont responsable de la cohérence des applications hello lors de l’utilisation des scripts personnalisés.
>


Ce tableau décrit les types de hello des conditions de la cohérence et hello qu’ils se produisent sous lors de la sauvegarde de la machine virtuelle Azure et procédures de restauration.

| Cohérence | En fonction du service VSS | Explication et détails |
| --- | --- | --- |
| Cohérence des applications |Oui pour Windows|La cohérence des applications est idéale pour les charges de travail, car elle apporte les garanties suivantes :<ol><li> Hello VM *démarre*. <li>Les données *ne sont pas endommagées*. <li>Il n’y a *aucune perte de données*.<li> les données de salutation sont toohello cohérente qui utilise des données hello en impliquant l’application hello au moment de hello de sauvegarde, à l’aide du script de pré/post ou de VSS.</ol> <li>*Machines virtuelles Windows*-charges de travail plus Microsoft ont les enregistreurs VSS qui effectuent des actions spécifiques à la charge de travail connexes toodata cohérence. Par exemple, Microsoft SQL Server a un enregistreur VSS qui permet de s’assurer que le fichier journal des transactions hello écritures toohello et la base de données hello effectuées correctement. Pour les sauvegardes de la machine virtuelle de Windows Azure, toocreate un point de récupération cohérents avec les applications, extension de sauvegarde hello doit appeler hello VSS workflow et la terminer avant de prendre l’instantané d’ordinateur virtuel hello. Pour toobe de capture instantanée Azure VM hello précis, les enregistreurs VSS de hello de toutes les applications de machine virtuelle Azure doivent exécuter ainsi. (En savoir hello [notions de base de VSS](http://blogs.technet.com/b/josebda/archive/2007/10/10/the-basics-of-the-volume-shadow-copy-service-vss.aspx) et examiner en détail les détails hello de [son fonctionnement](https://technet.microsoft.com/library/cc785914%28v=ws.10%29.aspx)). </li> <li> *Les machines virtuelles Linux*-les clients peuvent exécuter [tooensure personnalisé de script préalable et le script postérieur à la cohérence des applications](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). </li> |
| Cohérence du système de fichiers |Oui : pour les ordinateurs Windows |Il existe deux scénarios où le point de récupération hello peut être *système de fichiers cohérent*:<ul><li>Sauvegardes de machines virtuelles Linux dans Azure, sans pré/post-script ou si le pré/post-script a échoué. <li>Échec de VSS lors de la sauvegarde de machines virtuelles Windows dans Azure.</li></ul> Dans ces deux cas, hello meilleures qui peut être effectué est tooensure qui : <ol><li> Hello VM *démarre*. <li>Les données *ne sont pas endommagées*.<li>Il n’y a *aucune perte de données*.</ol> Les applications doivent mécanisme tooimplement leur propre « fix-up » sur les données de salutation restaurée. |
| Cohérence en cas d’incident |Non |Cette situation est la machine virtuelle de tooa équivalent rencontre un « incident » (via une réinitialisation matérielle ou logicielle). Cohérence d’incident se produit généralement lorsque hello machine virtuelle Azure est arrêté au moment de hello de sauvegarde. Un point de récupération cohérent après sinistre ne fournit aucune garantie autour de la cohérence de hello des données de hello sur support de stockage hello--à partir du point de vue hello hello système d’exploitation ou application hello. Seules les données hello qui existe déjà sur le disque de hello au moment de la sauvegarde de hello sont capturées et sauvegardées. <br/> <br/> Lorsqu’il n’y a aucune garantie, généralement, hello démarrages du système d’exploitation, suivies de la vérification de disque procédure, comme chkdsk, toofix les erreurs d’endommagement. Toutes les données en mémoire ou des écritures qui n’ont pas été transférés toohello disque sont perdues. application Hello suit généralement avec son propre mécanisme de vérification au cas où la restauration de données doit toobe terminé. <br><br>Par exemple, si le journal des transactions hello possède des entrées qui ne sont pas présentes dans la base de données hello, logiciel de base de données hello effectue ensuite une restauration jusqu'à ce que les données de salutation soient cohérentes. Lorsque les données sont réparties sur plusieurs disques virtuels (par exemple, les volumes fractionnés), un point de récupération cohérent après sinistre ne fournit aucune garantie d’exactitude hello de données de hello. |

## <a name="performance-and-resource-utilization"></a>Performance et utilisation des ressources
Au même titre qu’un logiciel de sauvegarde déployé sur site, il est recommandé de planifier les besoins en capacité et en consommation de ressources lors d’une sauvegarde de machines virtuelles dans Azure. Hello [limite de stockage Azure](../azure-subscription-service-limits.md#storage-limits) définir l’impact de toostructure VM déploiements tooget optimiser les performances avec au minimum sur les charges de travail toorunning.

Payer toohello attention que suivants de stockage Azure limite lors de la planification des performances de sauvegarde :

* Nombre maximal de sorties par compte de stockage
* Taux de requête total par compte de stockage

### <a name="storage-account-limits"></a>Limites de compte de stockage
Sauvegarder des données copiées à partir d’un compte de stockage, ajoute toohello d’opérations d’entrée/sortie par seconde (IOPS) et des métriques de sortie (ou un débit) hello du compte de stockage. AT hello même consomment également des machines virtuelles, en temps IOPS et le débit. Hello vise tooensure sauvegarde et le trafic d’ordinateur virtuel ne pas dépasser les limites de votre compte de stockage.

### <a name="number-of-disks"></a>Nombre de disques
processus de sauvegarde Hello tente toocomplete un travail de sauvegarde aussi rapidement que possible. Autrement dit, il consomme un maximum de ressources. Toutefois, toutes les opérations d’e/s sont limitées par hello *débit cible pour l’objet Blob unique*, qui a une limite de 60 Mo par seconde. Dans un toomaximize tentative de sa vitesse, les processus de sauvegarde hello tente tooback chacun des disques de l’ordinateur virtuel hello *en parallèle*. Si une machine virtuelle a quatre disques, hello tooback de tentatives de service de toutes les quatre disques en parallèle. Hello **nombre de disques** en cours de sauvegarde, est hello plus facteur déterminant le trafic sauvegarde de compte de stockage.

### <a name="backup-schedule"></a>Planification de sauvegarde
Un facteur supplémentaire qui affecte les performances est hello **planification de sauvegarde**. Si vous configurez des stratégies de hello pour toutes les machines virtuelles sont sauvegardés à hello même temps, vous avez planifié un bourrage de trafic. processus de sauvegarde Hello tentatives tooback tous les disques en parallèle. tooreduce hello le trafic de sauvegarde à partir d’un compte de stockage, sauvegardez les différentes machines virtuelles à différents heure hello, sans chevauchement.

## <a name="capacity-planning"></a>Planification de la capacité
Assembler les facteurs précédents hello, vous devez tooplan pour les besoins de l’utilisation de compte de stockage hello. Télécharger hello [capacité de sauvegarde de machine virtuelle planification de la feuille de calcul Excel](https://gallery.technet.microsoft.com/Azure-Backup-Storage-a46d7e33) impact de hello toosee de votre disque et de choix de la planification de sauvegarde.

### <a name="backup-throughput"></a>Débit de sauvegarde
Pour chaque disque en cours de sauvegarde, Azure Backup lit des blocs hello sur le disque de hello et magasins hello uniquement les données modifiées (sauvegarde incrémentielle). Hello tableau suivant montre les valeurs hello moyenne sauvegarde service débit. À l’aide de données suivantes de hello, vous pouvez estimer la durée hello nécessaire tooback d’un disque d’une taille donnée.

| Opération de sauvegarde | Meilleur débit |
| --- | --- |
| Sauvegarde initiale |160 Mbits/s |
| Sauvegarde incrémentielle (DR) |640 Mbits/s  <br><br> Chute considérablement si hello modifié des données (qui doivent toobe sauvegardé) sont réparties sur les disques hello.|

## <a name="total-vm-backup-time"></a>Durée de sauvegarde de machine virtuelle totale
Alors que la plupart du temps de sauvegarde hello est passé à la lecture et la copie des données, autres opérations contribuent tooback de temps total nécessaire toohello d’un ordinateur virtuel :

* Temps nécessaire trop[installer ou mettre à jour d’extension de sauvegarde hello](backup-azure-vms.md).
* Heure de l’instantané, qui est hello durée tootrigger un instantané. Les instantanés sont déclenchées toohello fermer planifiée les temps de sauvegarde.
* Délai d’attente de file d’attente. Étant donné que le service de sauvegarde hello le traitement de sauvegardes à partir de plusieurs clients, copie des données de sauvegarde à partir de la sauvegarde d’instantanés toohello ou les Services de récupération coffre peut ne pas démarre immédiatement. Dans les heures de pointe, hello attente permet d’étendre les heures tooeight en raison du nombre de toohello de sauvegardes en cours de traitement. Toutefois, hello total VM heure de la sauvegarde est inférieure à 24 heures pour les stratégies de sauvegarde quotidiennes.
* Temps de transfert de données, temps nécessaire pour la sauvegarde toocompute hello des modifications incrémentielles à partir d’une sauvegarde précédente du service et transférer ces stockage toovault de modifications.

### <a name="why-am-i-observing-longer12-hours-backup-time"></a>Pourquoi les temps de sauvegarde semblent-ils plus longs (>12 heures) ?
Sauvegarde se compose de deux phases : prise d’instantanés et le transfert hello instantanés toohello coffre. Hello service sauvegarde optimise les demandes de stockage. Lors du transfert de hello instantané données tooa coffre, service de hello transfère uniquement les modifications incrémentielles à partir de l’instantané précédent de hello.  toodetermine les modifications incrémentielles hello, service de hello calcule la somme de contrôle hello de blocs de hello. Si un bloc est modifié, les blocs hello sont identifié comme un toobe bloc envoyé toohello coffre. Extrait vers le service hello supplémentaire dans chacun des hello identifiés blocs, recherchez des opportunités toominimize hello données tootransfer. Après avoir évalué tous les blocs modifiés, service de hello fusionne les modifications hello et les envoie toohello coffre. Dans certaines applications héritées, les écritures de petite taille et fragmentées ne sont pas optimales pour le stockage. Si l’instantané d’hello contient de nombreuses écritures de petite taille, fragmentés, service de hello consacre plus de temps du traitement des données hello écrites par les applications hello. Hello recommandé de bloc écriture d’applications à partir d’Azure, pour les applications en cours d’exécution à l’intérieur de hello machine virtuelle, est un minimum de 8 Ko. Si votre application utilise un bloc de moins de 8 Ko, les performances de sauvegarde sont affectées. Pour plus d’informations de réglage des performances de sauvegarde tooimprove application, consultez [paramétrage des applications pour des performances optimales avec le stockage Azure](../storage/common/storage-premium-storage-performance.md). Bien que l’article hello sur les performances de sauvegarde utilise des exemples de stockage Premium, des conseils de hello sont applicable pour les disques de stockage Standard.

## <a name="total-restore-time"></a>Temps de restauration total
Une opération de restauration se compose de deux tâches principales sub : copie de données de compte de stockage client hello coffre toohello choisi et la création de machine virtuelle de hello. Copie de données à partir de coffre de hello dépend où les sauvegardes hello sont stockées en interne dans Azure, et où se trouve le compte de stockage client hello. Dépend de la durée des données de toocopy :
* File d’attente délai - étant donné que le processus de service hello les travaux de restauration à partir de plusieurs clients hello même temps, les demandes de restauration sont placés dans une file d’attente.
* Copie de données time - données sont copiées de hello coffre toohello compte de stockage. Restaurer temps dépend des e/s et obtient de débit service Azure Backup sur le compte de stockage client hello sélectionné. tooreduce hello copie moment pendant le processus de restauration hello, sélectionnez un compte de stockage ne pas chargé avec d’autres écritures de l’application et les lectures.

## <a name="best-practices"></a>Meilleures pratiques
Nous vous suggérons de suivre les meilleures pratiques ci-dessous lors de la configuration de sauvegardes de machines virtuelles :

* Ne pas planifier plus de 10 ordinateurs virtuels classiques hello même de cloud service tooback à hello même temps. Si vous souhaitez tooback plusieurs ordinateurs virtuels à partir du même service cloud, échelonner les heures de début de la sauvegarde de hello, d’une heure.
* Ne planifiez pas plus de 40 tooback de machines virtuelles à hello même temps.
* Planifiez les sauvegardes de machines virtuelles pendant les heures creuses. Ce service de sauvegarde de hello moyen utilise IOPS pour transférer des données à partir du coffre de toohello hello client stockage compte.
* Veillez à appliquer une stratégie aux machines virtuelles réparties entre les différents comptes de stockage. Nous vous suggérons de pas plus de 20 disques à partir d’un seul compte de stockage protégé par hello même planning de sauvegarde. Si vous avez supérieure à 20 disques dans un compte de stockage se propager ces machines virtuelles entre plusieurs stratégies tooget hello IOPS requises pendant la phase de transfert hello hello du processus de sauvegarde.
* Ne restaurez pas une machine virtuelle en cours d’exécution sur le compte de stockage toosame stockage Premium. Si le processus de restauration hello coïncide avec l’opération de sauvegarde hello, il réduit hello IOPS disponibles pour la sauvegarde.
* Pour la sauvegarde de machine virtuelle Premium, assurez-vous que le compte de stockage qui héberge les disques Premium dispose d’au moins 50 % d’espace libre pour créer des captures instantanées intermédiaires pour une sauvegarde réussie. 
* Assurez-vous que la version Python sur les machines virtuelles Linux activées pour la sauvegarde est 2.7

## <a name="data-encryption"></a>Chiffrement des données
Azure Backup ne chiffre pas les données dans le cadre du processus de sauvegarde hello. Toutefois, vous pouvez chiffrer les données au sein de hello VM et hello de sauvegarder les données protégées en toute transparence (en savoir plus sur [sauvegarde des données chiffrées](backup-azure-vms-encryption.md)).

## <a name="calculating-hello-cost-of-protected-instances"></a>Calcul du coût hello d’instances protégées
Machines virtuelles qui sont sauvegardés via Azure Backup sont soumises trop[tarification d’Azure Backup](https://azure.microsoft.com/pricing/details/backup/). Hello calcul des Instances de protégé est basée sur hello *réel* taille de machine virtuelle hello, qui est la somme de hello de toutes les données hello dans la machine virtuelle hello en excluant hello « disque de ressources ».

Prix de sauvegarde d’ordinateurs virtuels est *pas* en fonction de taille hello maximale prise en charge pour chaque ordinateur virtuel de données disque toohello attaché. Tarification est basée sur des données réelles de hello stockées dans le disque de données hello. De même, facture de stockage de sauvegarde hello est basée sur quantité hello de données qui sont stockées dans Azure Backup, qui est la somme de hello des données réelles de hello dans chaque point de récupération.

Prenons l’exemple d’une machine virtuelle de taille standard A2 avec deux disques de données supplémentaires d’une taille maximale de 1 To. Hello tableau suivant donne des données hello stockées sur chacun de ces disques :

| Type de disque | Taille maximale | Données réelles présentes |
| --- | --- | --- |
| Disque de système d’exploitation |1 023 Go |17 Go |
| Disque local/Disque de ressources |135 Go |5 Go (non inclus pour la sauvegarde) |
| Disque de données 1 |1 023 Go |30 Go |
| Disque de données 2 |1 023 Go |0 Go |

Hello *réel* taille de machine virtuelle de hello est dans ce cas 17 Go + 30 Go + 0 = 47 go. Cette taille instances protégées (47 Go) devient la base hello mensuel hello. En tant que hello quantité de données dans la machine virtuelle de hello augmente, taille des instances de protégé hello utilisé pour les modifications de facturation en conséquence.

Facturation ne démarre pas tant que sauvegarde première hello se termine. À ce stade, la facturation hello pour le stockage et protégé par les Instances commence. Facturation continue tant qu’il est *les données stockées dans un coffre de sauvegarde* pour la machine virtuelle de hello. Si vous arrêtez la protection sur l’ordinateur virtuel de hello, mais les données de sauvegarde d’ordinateur virtuel existent dans un coffre, la facturation continue.

Facturation pour un ordinateur virtuel spécifié s’arrête uniquement en cas d’arrêt de la protection de hello *et* toutes les données de sauvegarde est supprimé. Lorsque la protection s’arrête et n’a aucune tâche de sauvegarde active, taille hello de la dernière sauvegarde VM réussie hello devient la taille des instances de protégé hello utilisé pour la facture mensuelle de hello.

## <a name="questions"></a>Des questions ?
Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Étapes suivantes
* [Sauvegarde de machines virtuelles](backup-azure-vms.md)
* [Gestion de la sauvegarde de machine virtuelle](backup-azure-manage-vms.md)
* [Restauration des machines virtuelles](backup-azure-restore-vms.md)
* [Résoudre les problèmes de sauvegarde de machines virtuelles](backup-azure-vms-troubleshoot.md)
