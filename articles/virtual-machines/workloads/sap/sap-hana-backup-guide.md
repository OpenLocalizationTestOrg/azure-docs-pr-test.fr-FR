---
title: "guide d’aaaBackup pour SAP HANA sur des Machines virtuelles Azure | Documents Microsoft"
description: "Le guide de sauvegarde pour SAP HANA couvre deux méthodes de sauvegarde clés pour SAP HANA sur machines virtuelles Azure"
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
ms.openlocfilehash: e651091bb5da2698ec8bf80cad405bfce5b192cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-guide-for-sap-hana-on-azure-virtual-machines"></a>Guide de sauvegarde pour SAP HANA sur Machines Virtuelles Azure

## <a name="getting-started"></a>Mise en route

guide de sauvegarde Hello pour SAP HANA en cours d’exécution sur des Machines virtuelles Azure décrit uniquement les rubriques spécifiques à Azure. Pour général SAP HANA sauvegarde les éléments associés, consultez la documentation de SAP HANA hello (consultez _documentation de SAP HANA sauvegarde_ plus loin dans cet article).

Hello de cet article porte sur deux possibilités sauvegarde majeures pour SAP HANA sur des machines virtuelles :

- Système de fichiers de sauvegarde toohello HANA dans une Machine virtuelle de Azure Linux (consultez [SAP HANA Azure Backup au niveau du fichier](sap-hana-backup-file-level.md))
- Sauvegarde HANA basée sur les instantanés de stockage à l’aide de fonctionnalité de capture instantanée hello stockage Azure blob manuellement ou le Service de sauvegarde Azure (consultez [sauvegarde de SAP HANA basée sur des instantanés de stockage](sap-hana-backup-storage-snapshots.md))

SAP HANA offre une API, ce qui permet de toointegrate les outils de sauvegarde tiers directement avec SAP HANA de sauvegarde. (Qui n’est pas étendue hello de ce guide.) Actuellement, il n’existe aucune intégration directe de SAP HANA au service Azure Backup basée sur cette API.

SAP HANA est officiellement pris en charge sur le type de machine virtuelle Azure GS5 en tant qu’instance unique avec un charges de travail tooOLAP restriction supplémentaire (consultez [trouver les plateformes IaaS certifié](https://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) sur le site Web SAP hello). Cet article sera mis à jour lors de la mise à disposition de nouvelles offres pour SAP HANA sur Azure.

Une solution SAP HANA hybride est également disponible sur Azure. Dans le cadre de cette solution, SAP HANA s’exécute de façon non virtualisée sur des serveurs physiques. Toutefois, ce guide de sauvegarde SAP HANA pour Azure couvre un environnement Azure pur où SAP HANA s’exécute dans une machine virtuelle Azure et non sur de &quot;grandes instances&quot;. Consultez l’article [Vue d’ensemble et architecture de SAP HANA (grandes instances) sur Azure](hana-overview-architecture.md) pour plus d’informations sur cette solution de sauvegarde sur de &quot;grandes instances&quot;, basée sur des captures instantanées de stockage.

Vous trouverez des informations générales sur les produits SAP pris en charge par Azure dans la [note SAP 1928533](https://launchpad.support.sap.com/#/notes/1928533).

Hello trois figures suivantes donnent une vue d’ensemble de hello les options de sauvegarde SAP HANA à l’aide des fonctionnalités natives de Azure actuellement et indiquent également les trois scénarios de sauvegarde futures potentielles. articles connexes de Hello [SAP HANA Azure Backup au niveau du fichier de](sap-hana-backup-file-level.md) et [sauvegarde de SAP HANA basée sur des instantanés de stockage](sap-hana-backup-storage-snapshots.md) décrivent ces options plus en détail, y compris les considérations relatives à la taille et de performances pour SAP Sauvegardes HANA multi-téraoctets.

![Cette illustration montre deux possibilités pour enregistrer l’état des ordinateurs virtuels en cours hello](media/sap-hana-backup-guide/image001.png)

Cette illustration montre la possibilité de hello de l’enregistrement de hello VM état actuel, soit via le service de sauvegarde Azure ou d’un instantané manuel de disques de machine virtuelle. Avec cette approche, un n &#39; t disposer de sauvegardes de SAP HANA toomanage. défi Hello du scénario de capture instantanée de disque hello est la cohérence des fichiers système et un état de disque cohérents avec les applications. rubrique de la cohérence Hello est décrite dans la section de hello _la cohérence des données SAP HANA lors de la prise d’instantanés de stockage_ plus loin dans cet article. Fonctionnalités et restrictions de Azure Backup service liées à des sauvegardes HANA tooSAP sont également décrites plus loin dans cet article.

![Cette illustration montre la sauvegarde à l’intérieur de machine virtuelle de hello du fichier options pour effectuer une SAP HANA](media/sap-hana-backup-guide/image002.png)

Cette figure illustre les options pour une sauvegarde de fichier SAP HANA à l’intérieur de hello machine virtuelle et puis le stockage des fichiers de sauvegarde HANA quelque part à l’aide de différents outils. Une sauvegarde HANA nécessite plus de temps qu’une solution de sauvegarde basée sur des captures instantanées. Cependant, elle présente certains avantages en termes d’intégrité et de cohérence. Vous trouverez des informations plus détaillées à ce sujet plus loin dans cet article.

![Ce schéma illustre un scénario de sauvegarde SAP HANA futur potentiel.](media/sap-hana-backup-guide/image003.png)

Ce schéma illustre un scénario de sauvegarde SAP HANA futur potentiel. Si SAP HANA autorisait à effectuer des sauvegardes à partir d’une réplication secondaire, cela offrirait des possibilités supplémentaires en matière de stratégies de sauvegarde. Actuellement il n’est pas possible en fonction de post tooa Bonjour SAP HANA Wiki :

_&quot;Il est possible tootake les sauvegardes sur site secondaire de hello ?_

_Non, actuellement vous pouvez uniquement des données et sauvegardes de journaux côté primaire de hello. Si la sauvegarde de l’ouverture de session automatique est activée, après toohello prise de contrôle de site secondaire, les sauvegardes de journal hello seront automatiquement écrit il.&quot;_

## <a name="sap-resources-for-hana-backup"></a>Ressources SAP pour la sauvegarde HANA

### <a name="sap-hana-backup-documentation"></a>Documentation sur la sauvegarde SAP HANA

- [Introduction tooSAP HANA Administration](https://help.sap.com/viewer/6b94445c94ae495c83a19646e7c3fd56/2.0.00/en-US)
- [Planning Your Backup and Recovery Strategy](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm) (Planification de votre stratégie de sauvegarde et de récupération)
- [Schedule HANA Backup using ABAP DBACOCKPIT](http://www.hanatutorials.com/p/schedule-hana-backup-using-abap.html) (Planifier la sauvegarde HANA avec ABAP DBACOCKPIT)
- [Schedule Data Backups (SAP HANA Cockpit)](http://help.sap.com/saphelp_hanaplatform/helpdata/en/6d/385fa14ef64a6bab2c97a3d3e40292/frameset.htm) (Planifier des sauvegardes de données (cockpit SAP HANA))
- FAQ sur la sauvegarde SAP HANA dans la [note SAP 1642148](https://launchpad.support.sap.com/#/notes/1642148)
- FAQ sur les captures instantanées de base de données et de stockage SAP HANA dans la [note SAP 2039883](https://launchpad.support.sap.com/#/notes/2039883)
- Systèmes de fichiers en réseau inappropriés pour la sauvegarde et la récupération dans la [note SAP 1820529](https://launchpad.support.sap.com/#/notes/1820529)

### <a name="why-sap-hana-backup"></a>Pourquoi utiliser la sauvegarde SAP HANA ?

Le stockage Azure offre la disponibilité et la fiabilité en dehors de la zone de hello (consultez [Introduction tooMicrosoft Azure Storage](../../../storage/common/storage-introduction.md) pour plus d’informations sur le stockage Azure).

Hello minimale pour &quot;sauvegarde&quot; est toorely sur hello SLA Azure, conservation hello SAP HANA données et fichiers journaux sur la machine virtuelle du serveur SAP HANA disques durs virtuels d’Azure attaché toohello. Cette approche couvre les échecs de la machine virtuelle, mais pas potentiels dommages toohello SAP HANA données et fichiers journaux ou les erreurs logiques tels que la suppression des fichiers de données ou par accident. Les sauvegardes sont également requises pour des raisons juridiques ou de conformité. En bref, il est toujours nécessaire d’effectuer des sauvegardes SAP HANA.

### <a name="how-tooverify-correctness-of-sap-hana-backup"></a>Comment exactitude tooverify de sauvegarde de SAP HANA
Lorsque vous utilisez des captures instantanées de stockage, il est recommandé d’effectuer un test de restauration sur un autre système. Cette approche offre un moyen tooensure qu’une sauvegarde est corrects et internes des processus pour le travail de sauvegarde et de restauration, comme prévu. Bien que cela soit un obstacle sur site, il est beaucoup plus facile tooaccomplish dans le cloud de hello en fournissant temporairement les ressources nécessaires à cet effet.

Gardez à l’esprit qu’il ne suffit pas d’effectuer une simple restauration et de vérifier si HANA est opérationnel et en cours d’exécution. Dans l’idéal, un doit s’exécuter une table cohérence cocher toobe que cette base de données restaurée de hello est correct. SAP HANA offre plusieurs types de vérifications de cohérence. Ceux-ci sont décrits dans la [note SAP 1977584](https://launchpad.support.sap.com/#/notes/1977584).

Plus d’informations sur la vérification de cohérence hello table vous trouverez également sur le site Web SAP hello, consultez [Table et le catalogue des vérifications de cohérence](http://help.sap.com/saphelp_hanaplatform/helpdata/en/25/84ec2e324d44529edc8221956359ea/content.htm#loio9357bf52c7324bee9567dca417ad9f8b).

Pour les sauvegardes de fichiers standard, il n’est pas nécessaire d’effectuer un test de restauration. Il existe deux outils SAP HANA qui aident à toocheck quelle sauvegarde peut être utilisé pour la restauration : hdbbackupdiag et hdbbackupcheck. Consultez la page [Manually Checking Whether a Recovery is Possible](https://help.sap.com/saphelp_hanaplatform/helpdata/en/77/522ef1e3cb4d799bab33e0aeb9c93b/content.htm) (Vérifier manuellement si une récupération est possible) pour plus d’informations sur ces outils.

### <a name="pros-and-cons-of-hana-backup-versus-storage-snapshot"></a>Avantages et inconvénients de la sauvegarde HANA par rapport à la capture instantanée de stockage

SAP n & #39 t permettent de préférence tooeither HANA sauvegarde ; et les instantanés de stockage. Il répertorie leurs avantages et inconvénients, afin qu’un puisse déterminer quels toouse selon la situation de hello et la technologie de stockage disponible (voir [planification de votre stratégie de sauvegarde et récupération](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)).

Sur Azure, tenez compte des faits hello qui hello Azure blob instantané fonctionnalité n &#39; t garantir la cohérence de système de fichier (voir [instantanés d’objet blob à l’aide avec PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/)). Hello la section suivante, _la cohérence des données SAP HANA lors de la prise d’instantanés de stockage_, présente certaines considérations relatives à cette fonctionnalité.

En outre, un a toounderstand hello conséquences de facturation lorsque vous utilisez fréquemment des instantanés d’objet blob comme décrit dans cet article : [comprendre comment les instantanés engendrent une augmentation des coûts](/rest/api/storageservices/understanding-how-snapshots-accrue-charges): il n’est pas &#39; t comme évident que l’utilisation de Azure disques virtuels.

### <a name="sap-hana-data-consistency-when-taking-storage-snapshots"></a>Cohérence des données SAP HANA lors de la création de captures instantanées de stockage

Dans le cadre de la création de captures instantanées de stockage, la cohérence du système de fichiers et des applications représente un problème complexe. des problèmes tooavoid de façon plus simple Hello est tooshut vers le bas SAP HANA, ou peut-être même machine virtuelle entière de hello. Un arrêt pourrait être effectué avec une démonstration ou un prototype, voire avec un système de développement. Cependant, ce procédé n’est pas envisageable avec un système de production.

Sur Azure, l’un est tookeep à l’esprit que hello Azure blob instantané fonctionnalité n &#39; t garantir la cohérence de système de fichiers. Il fonctionne toutefois à l’aide de hello SAP HANA instantané fonctionnalité, tant qu’il existe un seul disque virtuel impliqués. Mais même avec un disque unique, d’autres éléments toobe activée. La [note SAP 2039883](https://launchpad.support.sap.com/#/notes/2039883) fournit des informations importantes sur les sauvegardes SAP HANA effectuées avec des captures instantanées de stockage. Par exemple, il mentionne, avec le système de fichiers XFS hello, il est nécessaire toorun **xfs\_Figer** avant à partir d’un stockage d’instantané tooguarantee cohérence (consultez [xfs\_freeze(8) - man de Linux page](https://linux.die.net/man/8/xfs_freeze) pour plus d’informations sur **xfs\_Figer**).

rubrique Hello de cohérence complique encore plus dans un cas où un système de fichiers s’étend sur plusieurs disques/volumes. par exemple, lors de l’utilisation de mdadm ou de LVM et de l’entrelacement. Hello la Note SAP mentionnés ci-dessus états :

_&quot;Mais n’oubliez pas que le système de stockage hello possède la cohérence de tooguarantee d’e/s lors de la création d’un instantané du stockage par volume de données SAP HANA, autrement dit, la prise d’un instantané d’un volume de données spécifiques au service de SAP HANA doit être une opération atomique.&quot;_

En supposant qu’il existe un système de fichiers XFS fractionnement quatre disques virtuels Azure, hello étapes suivantes fournissent un instantané cohérent qui représente la zone de données hello HANA :

- Préparer la capture instantanée HANA
- Figer le système de fichiers hello (par exemple, utilisez **xfs\_Figer**)
- Créer toutes les captures instantanées d’objets blob nécessaires sur Azure
- Libérer le système de fichiers hello
- Confirmer la capture instantanée de hello HANA

Recommandation est la procédure de hello toouse ci-dessus dans tous les cas toobe, côté hello-safe, quel que soit le système de fichiers. S’il s’agit d’un seul disque ou d’un entrelacement, il convient d’utiliser mdadm ou LVM sur plusieurs disques.

Il s’agit de capture instantanée de tooconfirm important hello HANA. Échéance toohello &quot;copie sur écriture&quot; SAP HANA ne nécessitent pas d’espace disque supplémentaire dans ce mode de préparation d’instantané. &#39; s également n’est pas possible de toostart nouvelles sauvegardes jusqu'à ce que l’instantané de SAP HANA hello est confirmée.

Le service Azure Backup utilise tootake d’extensions de machine virtuelle Azure administration fsck hello. Ces extensions de machine virtuelle ne sont pas disponibles pour une utilisation autonome. Un a toujours la cohérence de toomanage SAP HANA. Consultez l’article hello [SAP HANA Azure Backup au niveau du fichier](sap-hana-backup-file-level.md) pour plus d’informations.

### <a name="sap-hana-backup-scheduling-strategy"></a>Stratégie de planification de sauvegarde SAP HANA

article de SAP HANA Hello [planification de votre stratégie de sauvegarde et récupération](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm) États a basic planifier des sauvegardes de toodo :

- Capture instantanée de stockage (quotidienne)
- Sauvegarde de données complète dans un fichier ou au format bacint (hebdomadaire)
- Sauvegardes de fichiers journaux automatiques

Si vous le souhaitez, vous pouvez procéder sans captures instantanées de stockage. Celles-ci peuvent être remplacées par des sauvegardes HANA différentielles ou incrémentielles (voir [Delta Backups](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm) (Sauvegardes différentielles) pour plus d’informations).

guide d’Administration de HANA Hello fournit un exemple de liste. Il suggère qu’il possible de récupérer point spécifique de SAP HANA tooa dans le temps à l’aide de hello suivant la séquence des sauvegardes :

1. Sauvegarde de données complète
2. Sauvegarde différentielle
3. Sauvegarde incrémentielle 1
4. Sauvegarde incrémentielle 2
5. Sauvegardes de fichiers journaux

En ce qui concerne une planification exacte comme toowhen et la fréquence à laquelle un type de sauvegarde spécifique doit se produire, il n’est pas possible toogive règle générale, il est trop spécifiques au client et varie selon le nombre de modifications de données se produire dans le système de hello. Une recommandation de base à partir du côté SAP, ce qui peut être considérée comme des indications générales, est toomake une sauvegarde HANA complète une fois par semaine.
Relatives aux sauvegardes de journaux, consultez la documentation de SAP HANA hello [sauvegardes du journal](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm).

SAP recommande un peu de ménage de hello catalogue de sauvegarde tookeep à partir de la culture à l’infini (consultez [pour le catalogue de sauvegarde et de stockage de sauvegarde de ménage](http://help.sap.com/saphelp_hanaplatform/helpdata/en/ca/c903c28b0e4301b39814ef41dbf568/content.htm)).

### <a name="sap-hana-configuration-files"></a>Fichiers de configuration SAP HANA

Comme indiqué dans la FAQ hello dans [SAP Remarque 1642148](https://launchpad.support.sap.com/#/notes/1642148), fichiers de configuration SAP HANA hello ne font pas partie d’une sauvegarde HANA standard. Ils ne sont pas essentiel toorestore un système. configuration de HANA Hello pourrait être modifiée manuellement après la restauration de hello. En cas de souhaité tooget hello même configuration personnalisée pendant le processus de restauration hello, il est nécessaire tooback les fichiers de configuration hello HANA séparément.

Si des sauvegardes standard HANA apprêtez tooa dédié de système de fichier de sauvegarde HANA, un peut également copier toohello de fichiers de configuration hello même système de fichiers de sauvegarde et copiez tout comme de la destination de stockage final toohello ensemble refroidir le stockage d’objets blob.

### <a name="sap-hana-cockpit"></a>Cockpit SAP HANA

Cockpit SAP HANA offre la possibilité de hello d’analyse et la gestion de SAP HANA via un navigateur. Il permet également la gestion des sauvegardes de SAP HANA et par conséquent peut être utilisé en tant qu’autre tooSAP HANA Studio et ABAP DBACOCKPIT (consultez [Cockpit SAP HANA](https://help.sap.com/saphelp_hanaplatform/helpdata/en/73/c37822444344f3973e0e976b77958e/content.htm) pour plus d’informations).

![Cette figure illustre le hello écran d’Administration de base de données SAP HANA Cockpit](media/sap-hana-backup-guide/image004.png)

Cette figure montre hello écran d’Administration de base de données SAP HANA Cockpit et vignette sauvegarde hello hello gauche. Vignette de sauvegarde Voir hello nécessite des autorisations utilisateur appropriées pour le compte de connexion.

![Les sauvegardes peuvent être surveillées dans le cockpit SAP HANA lors de leur réalisation.](media/sap-hana-backup-guide/image005.png)

Les sauvegardes peuvent être surveillés dans Cockpit SAP HANA pendant qu’ils sont en cours, une fois terminée, tous les détails de sauvegarde hello sont disponibles.

![Exemple utilisant Firefox sur une machine virtuelle Azure SLES 12 avec le bureau Gnome](media/sap-hana-backup-guide/image006.png)

Hello des captures d’écran précédentes ont été effectuées à partir d’une machine virtuelle de Windows Azure. Celle-ci illustre l’utilisation de Firefox sur une machine virtuelle Azure SLES 12 avec le bureau Gnome. Il affiche les planifications de sauvegarde hello option toodefine SAP HANA dans Cockpit SAP HANA. Comme l’également, il suggère de date/heure en tant que préfixe pour les fichiers de sauvegarde hello. Dans SAP HANA Studio, le préfixe par défaut de hello est &quot;COMPLETE\_données\_sauvegarde&quot; lorsque vous effectuez une sauvegarde complète. L’utilisation d’un préfixe unique est recommandée.

### <a name="sap-hana-backup-encryption"></a>Chiffrement de sauvegarde SAP HANA

SAP HANA assure le chiffrement des données et du journal. Si les journaux et données de SAP HANA ne sont pas chiffrés, puis les sauvegardes de hello sont également pas chiffrés. C’est toohello client toouse une forme de solution tierce tooencrypt hello SAP HANA des sauvegardes. Consultez [données et le chiffrement de Volume de journal](https://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/01f36fbb5710148b668201a6e95cf2/content.htm) toofind plus d’informations sur le chiffrement de SAP HANA.

Sur Microsoft Azure, un client peut utiliser hello tooencrypt de fonctionnalité de chiffrement IaaS VM. Par exemple, un peut utiliser dédiée aux données des disques toohello attaché machine virtuelle, qui sont des sauvegardes de SAP HANA toostore utilisé, puis effectuer des copies de ces disques.

Le service Azure Backup peut gérer des machines virtuelles/disques chiffrés (voir [mode tooback configuration et restauration de chiffrement de machines virtuelles dans Azure Backup](../../../backup/backup-azure-vms-encryption.md)).

Une autre option serait être toomaintain hello SAP HANA virtuelle et ses disques sans chiffrement et stocker des fichiers de sauvegarde de SAP HANA hello dans un compte de stockage pour lequel le chiffrement a été activé (voir [chiffrement de Service de stockage Azure pour les données au repos](../../../storage/common/storage-service-encryption.md)) .

## <a name="test-setup"></a>Configuration des tests

### <a name="test-virtual-machine-on-azure"></a>Machine virtuelle de test sur Azure

Une installation SAP HANA dans une machine virtuelle de Azure GS5 a été utilisée pour hello suite de tests de la sauvegarde/restauration.

![Cette illustration montre une partie de hello, vue d’ensemble du portail Azure pour la machine virtuelle de test hello HANA](media/sap-hana-backup-guide/image007.png)

Cette illustration montre une partie de hello, vue d’ensemble du portail Azure pour la machine virtuelle de test HANA hello.

### <a name="test-backup-size"></a>Taille de la sauvegarde de test

![Cette figure a été effectuée à partir de la console de sauvegarde hello dans HANA Studio et affiche la taille du fichier de sauvegarde hello Go 229 hello HANA serveur d’index](media/sap-hana-backup-guide/image008.png)

Une table fictive a été remplie avec les données tooget une taille totale des données de sauvegarde de plus de 200 Go de données de performances réalistes tooderive. la figure Hello a été effectuée à partir de la console de sauvegarde hello dans HANA Studio et affiche la taille du fichier de sauvegarde hello Go 229 hello HANA serveur d’index. Pour les tests de hello, le préfixe de sauvegarde hello par défaut « COMPLETE_DATA_BACKUP » dans SAP HANA Studio a été utilisé. Dans des systèmes de production réels, un préfixe plus utile doit être défini. Le cockpit SAP HANA suggère la date et l’heure.

### <a name="test-tool-toocopy-files-directly-tooazure-storage"></a>Fichiers de test outil toocopy directement tooAzure stockage

fichiers de sauvegarde de SAP HANA tootransfer directement tooAzure stockage d’objets blob ou les partages de fichiers Azure hello blobxfer tool a été utilisé, car il prend en charge les cibles et il peuvent être facilement intégrés à des scripts d’automatisation en raison de l’interface de ligne de commande de tooits. Hello blobxfer outil est disponible sur [GitHub](https://github.com/Azure/blobxfer).

### <a name="test-backup-size-estimation"></a>Estimation de la taille de la sauvegarde de test

Il est important de tooestimate hello taille de la sauvegarde de SAP HANA. Cette estimation permet de performances de tooimprove en définissant la taille du fichier de sauvegarde max hello pour un nombre de fichiers de sauvegarde, échéance tooparallelism lors d’une copie du fichier. (Ces aspects particuliers sont expliqués plus loin dans cet article.) Vous devez également choisir si toodo un jeu de sauvegarde ou un delta de sauvegarde (différentielle ou incrémentielle).

Heureusement, il existe une simple instruction SQL permettant d’estimer la taille de hello hello des fichiers de sauvegarde : **sélectionnez \* de M\_sauvegarde\_taille\_ESTIMATIONS** (consultez [ Hello d’estimation espace nécessaire dans hello système de fichiers pour une sauvegarde de données](https://help.sap.com/saphelp_hanaplatform/helpdata/en/7d/46337b7a9c4c708d965b65bc0f343c/content.htm)).

![sortie de Hello de cette instruction SQL correspond à quasiment hello taille réelle de la sauvegarde complète des données de hello sur le disque](media/sap-hana-backup-guide/image009.png)

Pour le système de test hello, sortie hello de cette instruction SQL correspond à quasiment hello taille réelle de la sauvegarde complète des données de hello sur le disque.

### <a name="test-hana-backup-file-size"></a>Taille du fichier de la sauvegarde de test HANA

![console de sauvegarde Hello HANA Studio permet une taille de fichier maximale hello toorestrict HANA des fichiers de sauvegarde](media/sap-hana-backup-guide/image010.png)

console de sauvegarde Hello HANA Studio permet une taille de fichier maximale hello toorestrict HANA des fichiers de sauvegarde. Dans l’environnement d’exemple hello, cette fonctionnalité rend possible tooget les fichiers de sauvegarde plus petit multiples au lieu d’un fichier de sauvegarde 230 Go. Taille de fichier a un impact significatif sur les performances (voir l’article connexe hello [SAP HANA Azure Backup au niveau du fichier](sap-hana-backup-file-level.md)).

## <a name="summary"></a>Résumé

Selon les résultats de test hello hello les tableaux suivants montrent les avantages et inconvénients des tooback solutions une base de données SAP HANA en cours d’exécution sur des machines virtuelles.

**Sauvegarde de copie et de système de fichiers SAP HANA toohello les fichiers de sauvegarde par la suite destination de sauvegarde finale toohello**

|Solution                                           |Avantages                                 |Inconvénients                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Conservation des sauvegardes HANA sur des disques de machine virtuelle                      |Aucun effort de gestion supplémentaire     |Occupation d’espace sur le disque de machine virtuelle local           |
|Stockage de tooblob Blobxfer outil toocopy les fichiers de sauvegarde |Parallélisme toocopy plusieurs fichiers, stockage d’objets blob froid de toouse de choix | Maintenance de l’outil supplémentaire et scripts personnalisés | 
|Copie d’objets blob avec Powershell ou l’interface CLI                    |Aucun outil supplémentaire nécessaire ; possibilité d’utiliser Azure Powershell ou l’interface CLI |processus manuel, le client a tootake administration scripts et la gestion d’objets BLOB de copié pour la restauration|
|Partage de tooNFS                                  |Après le traitement de fichiers de sauvegarde sur un autre ordinateur virtuel sans impact sur le serveur HANA hello|Lenteur du processus de copie|
|Blobxfer copie tooAzure Service de fichiers                |Pas d’occupation d’espace sur les disques de machine virtuelle locaux|Pas de prise en charge de l’écriture directe par la sauvegarde HANA ; restriction de la taille du partage de fichiers (actuellement 5 To)|
|Agent Azure Backup                                 | Serait la solution privilégiée         | Actuellement non disponible sur Linux    |



**Sauvegarde de SAP HANA à partir de captures instantanées de stockage**

|Solution                                           |Avantages                                 |Inconvénients                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Service Azure Backup                               | Possibilité d’effectuer une sauvegarde de machine virtuelle à partir de captures instantanées d’objets blob | Lorsque vous n’utilisez ne pas de restauration au niveau fichier, il requiert la création de hello d’une machine virtuelle pour le processus de restauration hello, ce qui implique de puis besoin hello d’une nouvelle clé de licence SAP HANA|
|Captures instantanées d’objets blob manuelles                              | Flexibilité toocreate et la restauration des disques de machine virtuelle sans modifier hello unique ID de machine virtuelle|Toutes les manipulations ayant toobe effectuée par le client de hello|

## <a name="next-steps"></a>Étapes suivantes
* [SAP HANA Azure Backup au niveau du fichier](sap-hana-backup-file-level.md) décrit l’option de sauvegarde basée sur le fichier hello.
* [Sauvegarde de SAP HANA basée sur des instantanés de stockage](sap-hana-backup-storage-snapshots.md) décrit l’option sauvegarde basée sur un instantané stockage hello.
* toolearn comment tooestablish haute disponibilité et le plan de récupération d’urgence de SAP HANA sur Azure (instances de grande taille), consultez [SAP HANA (instances de grande taille) haute disponibilité et récupération d’urgence sur Azure](hana-overview-high-availability-disaster-recovery.md).
