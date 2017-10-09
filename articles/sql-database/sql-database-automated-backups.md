---
title: "les sauvegardes de base de données SQL automatique, géo-redondant aaaAzure | Documents Microsoft"
description: "SQL Database crée automatiquement une sauvegarde de base de données locale toutes les cinq minutes et utilise le stockage géoredondant avec accès en lecture pour fournir la géoredondance."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 3ee3d49d-16fa-47cf-a3ab-7b22aa491a8d
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 8aff5356e8142707dd7cd2533a4aa5ea8fec866d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-automatic-sql-database-backups"></a>En savoir plus sur les sauvegardes automatiques SQL Database

Base de données SQL crée des sauvegardes de base de données automatiquement et utilise le stockage géo-redondant Azure avec accès en lecture (RA-GRS) tooprovide géo-redondance. Ces sauvegardes sont créées automatiquement et sans frais supplémentaires. Vous n’avez pas besoin toodo tout toomake que les se produisent. Les sauvegardes de base de données sont une partie essentielle de toute stratégie de continuité d’activité ou de récupération d’urgence, dans la mesure où elles protègent vos données des corruptions et des suppressions accidentelles. Si vous souhaitez que les sauvegardes tookeep dans votre propre conteneur de stockage, vous pouvez configurer une stratégie de rétention de sauvegarde à long terme. Pour plus d’informations, consultez [Rétention à long terme](sql-database-long-term-retention.md).

## <a name="what-is-a-sql-database-backup"></a>Qu’est-ce qu’une sauvegarde SQL Database ?

Base de données SQL utilise SQL Server technologie toocreate [complète](https://msdn.microsoft.com/library/ms186289.aspx), [différentielle](https://msdn.microsoft.com/library/ms175526.aspx), et [journal des transactions](https://msdn.microsoft.com/library/ms191429.aspx) sauvegardes. sauvegardes de journaux de transactions Hello lieu généralement toutes les 5 à 10 minutes, avec une fréquence hello basée sur le niveau de performance hello et la quantité d’activité de la base de données. Autorisent les sauvegardes de journal des transactions, les sauvegardes complètes et différentielles, vous toorestore un serveur de base de données tooa spécifique toohello point-à-temps même serveur qui héberge la base de données hello. Lorsque vous restaurez une base de données, hello cherche de service qui complète, différentielle et sauvegardes de journal de transaction doivent toobe restaurée.


Vous pouvez utiliser ces sauvegardes aux fins suivantes :

* Restaurer un base de données tooa point-à-temps dans la période de rétention hello. Cette opération va créer une base de données Bonjour même serveur que la base de données d’origine hello.
* Restaurer une heure toohello de base de données supprimée qu’il a été supprimé ou à tout moment au sein de la période de rétention hello. base de données Hello supprimé ne peut être restaurée hello même serveur où la base de données d’origine hello a été créé.
* Restaurer une région géographique tooanother de base de données. Ainsi, vous toorecover d’urgence géographique lorsque vous ne pouvez pas accéder à votre serveur et la base de données. Il crée une nouvelle base de données dans n’importe quel serveur existant n’importe où dans Bonjour. 
* Restaurer une base de données à partir d’une sauvegarde spécifique stockée dans le coffre Azure Recovery Services. Cela vous permet de toorestore une ancienne version de la base de données de hello toosatisfy une demande de conformité ou toorun une ancienne version de l’application hello. Consultez [Rétention à long terme](sql-database-long-term-retention.md).
* tooperform une restauration, consultez [restaurer la base de données à partir de sauvegardes](sql-database-recovery-using-backups.md).

> [!NOTE]
> Dans le stockage Azure, terme de hello *réplication* fait référence toocopying fichiers à partir d’un emplacement tooanother. SQL *réplication de base de données* fait référence tookeeping toomultiple bases de données secondaires synchronisées avec une base de données primaire. 
> 

## <a name="how-much-backup-storage-is-included-at-no-cost"></a>Quelle est la quantité de stockage de sauvegarde incluse sans frais ?
Base de données SQL fournit un % too200 de votre stockage de base de données maximal configuré en tant que stockage de sauvegarde sans frais supplémentaires. Par exemple, si vous avez une instance de base de données Standard configurée à une taille de 250 Go, vous bénéficiez de 500 Go d’espace de stockage de sauvegarde sans coût supplémentaire. Si votre base de données dépasse hello fourni le stockage de sauvegarde, vous pouvez choisir la période de rétention tooreduce hello en contactant le Support technique Azure. Une autre option consiste à toopay pour le stockage de sauvegarde supplémentaire qui est facturée au taux de Read-Access Geographically Redundant Storage (RA-GRS) standard hello. 

## <a name="how-often-do-backups-happen"></a>À quelle fréquence les sauvegardes se produisent-elles ?
Les sauvegardes complètes de base de données sont effectuées chaque semaine, les sauvegardes différentielles de base de données sont, en général, effectuées à quelques heures d’intervalle et les sauvegardes du journal des transactions sont effectuées toutes les 5 à 10 minutes. Hello première sauvegarde est planifiée immédiatement après la création d’une base de données. Il se termine généralement dans les 30 minutes, mais il peut prendre plus de temps lors de la base de données hello est de taille importante. Par exemple, sauvegarde initiale de hello peut prendre plus de temps sur une base de données restaurée ou une copie de la base de données. Après la première sauvegarde complète hello, tous les autres sauvegardes soient planifiées automatiquement et gérés en mode silencieux en arrière-plan de hello. minutage exact de Hello de toutes les sauvegardes de base de données est déterminée par hello service de base de données SQL lorsqu’il équilibre hello globale la charge du système. 

géo-réplication de stockage de sauvegarde Hello se produit en fonction de la planification de réplication de stockage Azure hello.

## <a name="how-long-do-you-keep-my-backups"></a>Combien de temps conservez-vous mes sauvegardes ?
Chaque sauvegarde de base de données SQL a une période de rétention qui est basée sur hello [niveau de service](sql-database-service-tiers.md) de base de données hello. période de rétention de Hello pour une base de données dans le :


* Niveau de service De base : 7 jours.
* Niveau de service Standard : 35 jours.
* Niveau de service Premium : 35 jours.

Si vous passer de votre base de données de type hello Standard ou tooBasic de niveaux de service Premium, hello sauvegardes pendant sept jours. Toutes les sauvegardes existantes d’une ancienneté supérieure à sept jours ne sont plus disponibles. 

Si vous mettez à niveau votre base de données tooStandard de niveau de service de base hello ou Premium, base de données SQL conserve les sauvegardes existantes jusqu'à ce qu’ils soient 35 jours. Il conserve les nouvelles sauvegardes pendant 35 jours.

Si vous supprimez une base de données, base de données SQL conserve les sauvegardes hello Bonjour comme une base de données en ligne. Par exemple, supposons que vous supprimez une base de données qui a une période de rétention de sept jours. Une sauvegarde dont l’ancienneté est de quatre jours est conservée trois jours de plus.

> [!IMPORTANT]
> Si vous supprimez hello Azure SQL server qui héberge les bases de données SQL, toutes les bases de données qui appartiennent toohello serveur sont également supprimées et ne peuvent pas être récupérées. Vous ne pouvez pas restaurer un serveur supprimé.
> 

## <a name="how-tooextend-hello-backup-retention-period"></a>Comment tooextend hello une période de rétention de sauvegarde ?
Si votre application nécessite que les sauvegardes de hello sont disponibles pour une période plus longue, vous pouvez étendre la période de rétention intégrés hello en configurant la stratégie de rétention de sauvegarde à long terme hello pour les bases de données individuelles (stratégie LTR). Cela vous permet de période de rétention de l’informatique intégrée de hello de tooextend des années de 35 jours tooup too10. Pour plus d’informations, consultez [Rétention à long terme](sql-database-long-term-retention.md).

Lorsque vous ajoutez hello LTR stratégie tooa base de données à l’aide du portail Azure ou API, des sauvegardes complètes hebdomadaires hello sera tooyour copié automatiquement possède le Service Azure Backup Vault. Si votre base de données est chiffrée avec les sauvegardes de hello chiffrement transparent des données sont automatiquement chiffrées au repos.  Hello coffre Services supprimera automatiquement vos sauvegardes ayant expirés, en fonction de leur horodatage et le hello stratégie LTR.  Afin de vous ne devez le planification de sauvegarde toomanage hello ou nettoyage hello de vous soucier hello anciens fichiers. prend en charge l’API Hello restauration de sauvegardes stockées dans hello coffre tant que le coffre hello est dans hello même abonnement que votre base de données SQL. Vous pouvez utiliser hello portail Azure ou PowerShell tooaccess ces sauvegardes.

> [!TIP]
> Pour une procédure-tooguide, consultez [configurer et restauration à partir de la rétention de sauvegarde à long terme de base de données SQL Azure](sql-database-long-term-backup-retention-configure.md)
>

## <a name="are-backups-encrypted"></a>Les sauvegardes sont-elles chiffrées ?

Lorsque le TDE est activé pour une base de données SQL Azure, les sauvegardes sont également chiffrées. Le TDE est configuré par défaut sur l’ensemble des nouvelles bases de données SQL Azure. Pour en savoir plus sur le TDE, consultez la page [Chiffrement transparent des données avec Azure SQL Database](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database).

## <a name="next-steps"></a>Étapes suivantes

- Les sauvegardes de base de données sont une partie essentielle de toute stratégie de continuité d’activité ou de récupération d’urgence, dans la mesure où elles protègent vos données des corruptions et des suppressions accidentelles. toolearn sur hello d’autres solutions de continuité d’activité base de données SQL Azure, consultez [vue d’ensemble de la continuité des activités métier](sql-database-business-continuity.md).
- point de tooa toorestore dans le temps à l’aide de hello portail Azure, consultez [restauration de base de données tooa point dans le temps à l’aide de hello portail Azure](sql-database-recovery-using-backups.md).
- point de tooa toorestore dans le temps à l’aide de PowerShell, consultez [restaurer la base de données tooa point dans le temps à l’aide de PowerShell](scripts/sql-database-restore-database-powershell.md).
- tooconfigure, gérer et restaurer à partir de la rétention à long terme des sauvegardes automatisées dans un coffre Azure Recovery Services à l’aide de hello Azure portail, consultez [gérer à long terme rétention de sauvegarde à l’aide de hello Azure portal](sql-database-long-term-backup-retention-configure.md).
- tooconfigure, gérer et les restaurer à partir de la rétention à long terme des sauvegardes automatisées dans un coffre Azure Recovery Services à l’aide de PowerShell, consultez [gérer la rétention de sauvegarde à long terme à l’aide de PowerShell](sql-database-long-term-backup-retention-configure.md).
