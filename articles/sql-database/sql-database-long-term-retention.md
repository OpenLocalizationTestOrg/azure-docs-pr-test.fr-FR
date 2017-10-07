---
title: "aaaStore les sauvegardes de base de données SQL Azure pour les années de too10 | Documents Microsoft"
description: "Découvrez comment Azure SQL Database prend en charge le stockage des sauvegardes pour les années de too10."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a>Stocker les sauvegardes de base de données SQL Azure pour les années de too10
De nombreuses applications ont réglementaires, de conformité ou autres activités à des fins qui nécessitent que des sauvegardes de base de données tooretain au-delà de hello jours 7-35 fournies par la base de données SQL Azure [sauvegardes automatiques](sql-database-automated-backups.md). En utilisant la fonctionnalité de rétention de sauvegarde à long terme hello, vous pouvez stocker vos sauvegardes de base de données SQL dans un coffre Azure Recovery Services pour les années de too10. Vous pouvez de stocker jusqu'à too1, 000 bases de données par le coffre. Vous pouvez ensuite sélectionner n’importe quelle sauvegarde dans hello coffre toorestore sous la forme d’une base de données.

> [!IMPORTANT]
> Rétention de sauvegarde à long terme est actuellement en version préliminaire et disponible dans hello suivant régions : est de l’Australie, Sud-est de l’Australie, sud du Brésil, du centre des États-Unis, Asie orientale, est des États-Unis, est des États-Unis 2, Inde centrale, sud de l’Inde, est du Japon, ouest du Japon, Amérique du Nord, du Nord Europe du Sud-Centre des États-Unis, Asie du Sud-est, Europe de l’ouest et ouest des États-Unis.
>

> [!NOTE]
> Vous pouvez activer des bases de données too200 par coffre pendant une période de 24 heures. Nous vous recommandons d’utiliser un coffre distinct pour chaque impact sur le serveur toominimize hello de cette limite. 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a>Comment fonctionne la rétention de sauvegarde SQL Database à long terme

Avec la rétention à long terme des sauvegardes, vous pouvez associer un serveur de base de données SQL à un coffre Azure Recovery Services. 

* Vous devez créer le coffre de hello en hello même abonnement Azure créé hello SQL serveur et dans hello même groupe de ressources et de la région géographique. 
* Vous configurez ensuite une stratégie de rétention pour une base de données quelconque. Hello stratégie causes hello hebdomadaire de la base de données complète des sauvegardes toobe copié le coffre Recovery Services toohello et conservées pendant la période de rétention spécifiée hello (haut too10 ans). 
* Vous pouvez ensuite restaurer la base de données hello à partir d’un de ces sauvegardes tooa nouvelle base de données dans n’importe quel serveur dans l’abonnement de hello. Le stockage Azure crée une copie à partir de sauvegardes existants, et copie de hello n’a aucun impact sur les performances sur la base de données existante hello.

> [!TIP]
> Pour une procédure-tooguide, consultez [configurer et restauration à partir de la rétention de sauvegarde à long terme de base de données SQL Azure](sql-database-long-term-backup-retention-configure.md).

## <a name="enable-long-term-backup-retention"></a>Activer la rétention des sauvegardes à long terme

rétention de sauvegarde à long terme tooconfigure pour une base de données :

1. Créer un coffre Azure Recovery Services Bonjour même groupe de région, les abonnements et les ressources que votre serveur de base de données SQL. 
2. Inscrire un coffre-fort toohello hello.
3. Créez une stratégie de protection Azure Recovery Services.
4. Appliquer hello protection stratégie toohello bases de données qui nécessitent la rétention de sauvegarde à long terme.

tooconfigure, gérer et restaurer une base de données à partir de la rétention de sauvegarde à long terme des sauvegardes automatisées dans un coffre Azure Recovery Services, effectuez une des manières suivantes les hello :

* À l’aide de hello portail Azure : cliquez sur **rétention de sauvegarde à long terme**, sélectionnez une base de données, puis cliquez sur **configurer**. 

   ![Sélectionner une base de données pour la rétention des sauvegardes à long terme](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* À l’aide de PowerShell : Accédez trop[configurer et restauration à partir de la rétention de sauvegarde à long terme de base de données SQL Azure](sql-database-long-term-backup-retention-configure.md).

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a>Restaurer une base de données qui est stockée avec la fonctionnalité de rétention de sauvegarde à long terme hello

toorecover à partir d’une sauvegarde à long terme de la rétention de sauvegarde :

1. Coffre de hello liste où la sauvegarde de hello est stocké.
2. Conteneur de hello de liste qui est mappé tooyour logique.
3. Source de données liste hello dans le coffre hello qui est mappé tooyour de base de données.
4. Liste hello points de récupération sont toorestore disponible.
5. Restaurer la base de données de hello à partir de serveur de cible de toohello de point de récupération hello dans votre abonnement.

tooconfigure, gérer et restaurer une base de données à partir de la rétention de sauvegarde à long terme des sauvegardes automatisées dans un coffre Azure Recovery Services, effectuez une des manières suivantes les hello :

* À l’aide de hello portail Azure : accédez trop[gérer à long terme rétention de sauvegarde à l’aide de hello Azure portal](sql-database-long-term-backup-retention-configure.md). 

* À l’aide de PowerShell : Accédez trop[gérer la rétention de sauvegarde à long terme à l’aide de PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="get-pricing-for-long-term-backup-retention"></a>Obtenir les prix de la rétention des sauvegardes à long terme

Rétention à long terme des sauvegardes de base de données SQL est facturée en fonction de toohello [service sauvegarde Azure tarification taux](https://azure.microsoft.com/pricing/details/backup/).

Une fois le serveur de base de données SQL hello toohello inscrits coffre, vous êtes facturé pour le stockage total hello qui est utilisé par les sauvegardes hebdomadaires hello stockées dans le coffre hello.

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a>Afficher les sauvegardes disponibles qui sont stockées avec rétention à long terme

tooconfigure, gérer et restaurer une base de données à partir de la rétention de sauvegarde à long terme des sauvegardes automatisées dans un coffre Azure Recovery Services à l’aide de hello portail Azure, effectuez une des manières suivantes les hello :

* À l’aide de hello portail Azure : accédez trop[gérer à long terme rétention de sauvegarde à l’aide de hello Azure portal](sql-database-long-term-backup-retention-configure.md). 

* À l’aide de PowerShell : Accédez trop[gérer la rétention de sauvegarde à long terme à l’aide de PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="disable-long-term-retention"></a>Désactiver la rétention à long terme

le service de récupération Hello gère automatiquement le nettoyage hello de hello fourni la stratégie de rétention des sauvegardes. 

les sauvegardes hello envoi toostop pour un coffre toohello de la base de données spécifique, supprimer la stratégie de rétention de hello pour cette base de données.
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> les sauvegardes Hello qui se trouvent déjà dans le coffre hello ne sont pas affectés. Ils sont automatiquement supprimés par le service de récupération hello lorsque leur période de rétention expire.

## <a name="long-term-backup-retention-faq"></a>Questions fréquentes (FAQ) sur la rétention des sauvegardes à long terme

**Puis-je supprimer manuellement des sauvegardes spécifiques dans le coffre hello ?**

Pas actuellement. coffre de Hello nettoie automatiquement les sauvegardes lors de la période de rétention hello a expiré.

**Puis-je enregistrer mon toomore de sauvegardes toostore serveur à un coffre-fort ?**

Non, vous pouvez stocker actuellement un coffre-fort de sauvegardes tooonly à la fois.

**Puis-je avoir un serveur et un coffre dans différents abonnements ?**

Non, actuellement le coffre hello et le serveur doivent être Bonjour même groupe d’abonnement et de ressources.

**Puis-je utiliser un coffre que j’ai créé dans une région qui est différente de celle de mon serveur ?**

Non, le coffre hello et le serveur doivent être Bonjour même région toominimize copier du temps et éviter les frais liés au trafic.

**Combien de bases de données puis-je stocker dans un coffre ?**

Actuellement, nous prenons en charge des too1, 000 bases de données par le coffre. 

**Combien de coffres puis-je créer par abonnement ?**

Vous pouvez créer des coffres too25 par abonnement.

**Combien de bases de données puis-je configurer par jour par coffre ?**

Vous pouvez configurer jusqu’à 200 bases de données par jour par coffre.

**La rétention de sauvegarde à long terme fonctionne-t-elle avec des pools élastiques ?**

Oui. Une base de données dans le pool de hello peut être configuré avec la stratégie de rétention hello.

**Puis-je choisir temps hello création de sauvegarde de hello ?**

Non, la base de données SQL contrôle hello planification de sauvegarde toominimize hello impact sur les performances de vos bases de données.

**Transparent Data Encryption est activé pour ma base de données. Puis-je utiliser avec le coffre de hello ?** 

Oui, Transparent Data Encryption est pris en charge. Vous pouvez restaurer la base de données hello du coffre de hello même si la base de données d’origine hello n’existe plus.

**Que se passe-t-il avec des sauvegardes dans le coffre hello hello si mon abonnement est suspendu ?** 

Si votre abonnement est suspendu, nous conserver les sauvegardes et les bases de données existantes hello. Nouvelles sauvegardes ne sont pas copiés toohello coffre. Après la réactivation d’abonnement de hello, service de hello reprend coffre toohello de sauvegardes de copie. Votre archivage devenue accessible toohello les opérations de restauration à l’aide de sauvegardes hello qui ont été copiés il avant hello abonnement a été suspendu. 

**Puis-je accéder aux fichiers de sauvegarde de base de données SQL toohello donc je peux télécharger ou les restaurer toohello SQL server ?**

Non, pas actuellement.

**Il est possible de toohave plusieurs planifications (quotidienne, hebdomadaire, mensuelle, annuelle) au sein d’une stratégie de rétention SQL.**

Non. Les planifications multiples sont prises en charge uniquement pour les sauvegardes de machines virtuelles.

**Que se passe-t-il si nous configurons la rétention à long terme de la sauvegarde sur une base de données qui est une base de données de géoréplication active secondaire ?**

Comme nous ne prenons pas en charge les sauvegardes sur des réplicas, il n’existe aucune option de rétention de sauvegarde à long terme sur les bases de données secondaires. Toutefois, il est important pour les utilisateurs des tooset de rétention de sauvegarde à long terme sur une base de données secondaires géo-réplication active pour ces raisons :
* Lorsqu’un basculement a lieu et base de données hello devient une base de données primaire, nous effectuer une sauvegarde complète, qui est téléchargé toovault.
* Il n’existe pas d’autres clients de toohello de coût pour configurer la rétention des sauvegardes à long terme sur une base de données secondaire.

## <a name="next-steps"></a>Étapes suivantes
Dans la mesure où les sauvegardes de base de données protègent les données des corruptions et des suppressions accidentelles, elles sont une partie essentielle de toute stratégie de continuité d’activité ou de récupération d’urgence. toolearn sur hello d’autres solutions de continuité d’activité de base de données SQL, consultez [vue d’ensemble de la continuité des activités métier](sql-database-business-continuity.md).
