---
title: "Forum aux questions de la base de données SQL d’aaaAzure | Documents Microsoft"
description: "Clients de questions réponses toocommon posent sur les bases de données cloud et base de données SQL Azure, du système de gestion de Microsoft de la base de données relationnelle (SGBDR) et de base de données en tant que service dans le cloud de hello."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 1da12abc-0646-43ba-b564-e3b049a6487f
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 02/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 04c02f96e6e91cf314221134ee0ef6d24217ef45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-faq"></a>Forum Aux Questions de base de données SQL

## <a name="what-is-hello-current-version-of-sql-database"></a>Qu’est la version actuelle de hello de base de données SQL ?
Hello version actuelle de la base de données SQL est V12. La version 11 a été retirée.

## <a name="what-is-hello-sla-for-sql-database"></a>Quel est le contrat SLA de hello pour la base de données SQL ?
Nous garantissons au moins 99,99 % des clients hello aura la connectivité entre leurs Basic unique ou élastique, Standard ou Premium Microsoft Azure SQL Database et notre passerelle Internet. Pour plus d’informations, consultez [Contrat de niveau de service](http://azure.microsoft.com/support/legal/sla/).

## <a name="how-do-i-reset-hello-password-for-hello-server-admin"></a>Mode de réinitialisation de mot de passe hello pour l’administration de serveur hello
Bonjour [portail Azure](https://portal.azure.com) cliquez sur **serveurs SQL**, sélectionnez-en hello dans hello liste, puis cliquez sur **réinitialiser le mot de passe**.

## <a name="how-do-i-manage-databases-and-logins"></a>Comment gérer les bases de données et les connexions ?
Consultez [Gestion des bases de données et des connexions](sql-database-manage-logins.md).

## <a name="how-do-i-make-sure-only-authorized-ip-addresses-are-allowed-tooaccess-a-server"></a>Comment faire en sorte que seules les adresses IP autorisées sont autorisés à tooaccess un serveur ?
Voir [Configuration des paramètres de pare-feu sur une base de données SQL](sql-database-configure-firewall-settings.md).

## <a name="how-does-hello-usage-of-sql-database-show-up-on-my-bill"></a>Comment l’utilisation de hello de base de données SQL s’afficheront pas sur ma facture ?
Opérations de base de données SQL sur un taux horaire prévisible basé sur le niveau de service hello + performances au niveau de bases de données uniques ou Edtu par pool élastique. L’utilisation réelle est calculée au pro-rata horaire, et il se peut que votre facture affiche des fractions d’heure. Par exemple, si une base de données existe pendant 12 heures au cours d’un mois, votre facture affiche une demi-journée d’utilisation. En outre, les niveaux de service + de niveau de performance et d’Edtu de pool est interrompues out dans hello bill toomake de nombre hello toosee plus facile de jours de base de données vous avez utilisé pour chacune d’elles dans un même mois.

## <a name="what-if-a-single-database-is-active-for-less-than-an-hour-or-uses-a-higher-service-tier-for-less-than-an-hour"></a>Que se passe-t-il si une base de données est active pendant moins d’une heure ou utilise un niveau de service plus élevé pendant moins d’une heure ?
Vous êtes facturé pour chaque heure de de qu'une base de données existe à l’aide hello plus haut niveau de service + performances niveau appliqué pendant cette heure, quel que soit l’utilisation ou de la base de données hello était active pour moins d’une heure. Par exemple, si vous avez créé une base de données unique et que vous l’avez supprimée cinq minutes après, votre facture mentionne le coût d’une heure de base de données. 

Exemples

* Si vous créez une base de données, puis immédiatement mettre à niveau tooStandard S1, vous êtes facturé au taux Standard S1 hello hello première heure.
* Si vous mettez à niveau une base de données à partir de la base tooPremium à 10:00. et que la mise à niveau se termine à 01 h 35 sur hello suivant jour, vous êtes facturé au tarif Premium de hello en commençant à 01:00. 
* Si vous rétrogradez une base de données Premium tooBasic à 11 h 00 Il se termine à 2 h 15, puis base de données hello est facturée au taux de Premium hello à 3 h, après laquelle il est facturée au taux de base hello.

## <a name="how-does-elastic-pool-usage-show-up-on-my-bill-and-what-happens-when-i-change-edtus-per-pool"></a>Comment l’utilisation du pool élastique s’affiche-il sur ma facture et que se passe-t-il lorsque je change le nombre d’eDTU par pool ?
Pool élastique frais afficher sur votre facture en tant que dtu élastiques (Edtu) par incréments de hello figurant sous Edtu par pool sur [hello page de tarification](https://azure.microsoft.com/pricing/details/sql-database/). Il n’existe pas de facturation par base de données pour les pools élastiques. Vous êtes facturé pour chaque heure qu'un pool existe à hello eDTU la plus élevée, quel que soit l’utilisation ou le pool de hello était active pour moins d’une heure. 

Exemples

* Si vous créez un pool élastique Standard avec 200 Edtu à 11:18 h 00, ajout de pool de toohello cinq bases de données, vous êtes facturé pour 200 Edtu une heure ensemble hello commençant à 11 h 00 via reste hello du jour de hello.
* Sur le jour 2, 5 h 05, 1 de la base de données commence à consommer de 50 Edtu et reste stable au jour de hello. Les bases de données 2-5 fluctuent entre 0 et 80 eDTU. Au jour de hello, vous ajoutez cinq autres bases de données qui utilisent des variables Edtu journée hello. Le jour 2 est un jour complet facturé à 200 eDTU. 
* Le troisième jour, à 5 h 00, vous ajoutez 15 autres bases de données. Utilisation de la base de données augmente dans l’ensemble de point de toohello hello jour où vous décidez d’Edtu tooincrease pour le pool hello de 200 too400 à 20 h 05. Des frais au niveau des eDTU hello 200 en vigueur jusqu'à 8 heures et augmente les Edtu too400 pour hello restant de quatre heures. 

## <a name="elastic-pool-billing-and-pricing-information"></a>Informations sur la tarification et la facturation du pool élastique
Pools élastiques sont facturées par hello suivant caractéristiques :

* Un pool élastique est facturé lors de sa création, même s’il n’existe aucune base de données dans le pool de hello.
* Il est facturé toutes les heures. Cela est hello même contrôle la fréquence que pour les niveaux de performance des bases de données uniques.
* Si un pool élastique est redimensionné tooa nouveau nombre d’Edtu de pool de hello puis n’est pas facturé selon toohello nouvelle durée Edtu jusqu'à la fin de hello opération de redimensionnement. Cela suit hello même modèle en tant que la modification du niveau de performance hello des bases de données uniques.
* prix de Hello d’un pool élastique est basé sur nombre hello d’Edtu de pool de hello. prix Hello d’un pool élastique est indépendante du nombre de hello et de l’utilisation des bases de données élastique hello qu’il contient.
* Le prix est calculé comme suit : le nombre d’eDTUs d’un pool x le prix unitaire par eDTU.

eDTU UnitPrice de Hello pour un pool élastique est supérieur au prix DTU unité hello pour une base de données Bonjour même niveau de service. Pour en savoir plus, voir [Tarification de la base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/). 

compte tenu des niveaux d’Edtu et service hello toounderstand, consultez [les options de base de données SQL et les performances](sql-database-service-tiers.md).

## <a name="how-does-hello-use-of-active-geo-replication-in-an-elastic-pool-show-up-on-my-bill"></a>Comment hello n’utilise pas de géo-réplication active dans un pool élastique qui s’affichent sur ma facture ?
Contrairement aux bases de données uniques, l’utilisation de la [géoréplication active](sql-database-geo-replication-overview.md) avec des bases de données élastiques n’a pas d’incidence directe sur la facturation.  Vous êtes uniquement facturé pour Edtu hello mis en service pour chacun des pools hello (pool principal et secondaire pool)

## <a name="how-does-hello-use-of-hello-auditing-feature-impact-my-bill"></a>Comment hello utilise-t-il Hello impact sur les fonctionnalités d’audit ma facture ?
L’audit est généré dans hello service de base de données SQL sans supplémentaire de coût et est disponible tooBasic, Standard, Premium et Premium RS bases de données. Toutefois, toostore hello les journaux d’audit, hello audit utilise un compte de stockage Azure et de taux pour les tables et les files d’attente dans le stockage Azure s’appliquent selon la taille de hello de votre journal d’audit.

## <a name="how-do-i-find-hello-right-service-tier-and-performance-level-for-single-databases-and-elastic-pools"></a>Comment trouver hello bon niveau et les performances niveau de service pour les bases de données uniques et les pools élastiques ?
Il existe quelques tooyou d’outils disponibles. 

* Pour les bases de données locales, utilisez hello [Assistant de dimensionnement de DTU](http://dtucalculator.azurewebsites.net/) toorecommend hello des bases de données et les dtu requis et évaluer plusieurs bases de données pour les pools élastiques.
* Si une base de données unique tire avantage d’être au sein d’un pool, le moteur intelligent d’Azure recommande un pool élastique s’il détecte un schéma d’utilisation historique qui le justifie. Consultez [analyse et de gérer un pool élastique hello Azure portal](sql-database-elastic-pool-manage-portal.md). Pour plus d’informations sur la façon dont toodo hello mathématiques vous-même, consultez [considérations de prix et de performances pour un pool élastique](sql-database-elastic-pool.md)
* toosee si vous avez besoin de toodial une base de données vers le haut ou vers le bas, voir [Guide des performances pour les bases de données uniques](sql-database-performance-guidance.md).

## <a name="how-often-can-i-change-hello-service-tier-or-performance-level-of-a-single-database"></a>La fréquence à laquelle modifier le niveau de performance ou de niveau de service d’une base de données hello ?
Vous pouvez modifier le niveau de service hello (entre Basic, Standard, Premium et Premium RS) ou hello le niveau de performance au sein d’un niveau de service (par exemple, S1 tooS2) aussi souvent que vous le souhaitez. Pour les anciennes bases de données, vous pouvez modifier hello service niveau ou performances un total de quatre fois dans une période de 24 heures.

## <a name="how-often-can-i-adjust-hello-edtus-per-pool"></a>La fréquence à laquelle ajuster Edtu hello par pool ?
Aussi souvent que vous le souhaitez.

## <a name="how-long-does-it-take-toochange-hello-service-tier-or-performance-level-of-a-single-database-or-move-a-database-in-and-out-of-an-elastic-pool"></a>La durée pendant laquelle il prendre toochange hello service niveau niveau de performance ou d’une base de données ou déplacer une base de données vers et depuis un pool élastique ?
La modification du niveau de service hello d’une base de données et le déplacement et l’extraction d’un pool requièrent hello toobe de base de données copié sur la plateforme hello en tant qu’une opération d’arrière-plan. Niveau de service hello modification peut prendre de quelques minutes tooseveral heures selon la taille de hello des bases de données hello. Dans les deux cas, les bases de données hello restent en ligne et disponibles pendant le déplacement de hello. Pour plus d’informations sur la modification des bases de données uniques, consultez [niveau de service hello de modification d’une base de données](sql-database-service-tiers.md). 

## <a name="when-should-i-use-a-single-database-vs-elastic-databases"></a>Quand dois-je choisir une base de données unique plutôt que des bases de données élastiques ?
En général, les pools élastiques sont conçus pour un [modèle d’application logiciel en tant que service (SaaS)](sql-database-design-patterns-multi-tenancy-saas-applications.md) standard, où il existe une base de données par client ou par locataire. Achats de bases de données individuelles et variable de hello toomeet un surapprovisionnement et une utilisation maximale la demande pour chaque base de données est souvent pas réaliser des économies. Avec les pools, gérer les performances de collectif hello du pool de hello et bases de données hello évoluer automatiquement. Le moteur intelligent d’Azure recommande un pool pour les bases de données quand un modèle d’utilisation l’exige. Pour plus d’informations, consultez [Conseils pour les pools élastiques](sql-database-elastic-pool.md).

## <a name="what-does-it-mean-toohave-up-too200-of-your-maximum-provisioned-database-storage-for-backup-storage"></a>Que signifie toohave % too200 de votre stockage de base de données maximal configuré pour le stockage de sauvegarde ?
Stockage de sauvegarde est le stockage hello par vos sauvegardes automatisées de la base de données qui sont utilisés pour [Point-de-temps restauration](sql-database-recovery-using-backups.md#point-in-time-restore) et [géo-restauration](sql-database-recovery-using-backups.md#geo-restore). Base de données SQL Microsoft Azure fournit un % too200 de votre stockage de base de données maximal configuré de stockage de sauvegarde sans frais supplémentaires. Par exemple, si vous avez une instance de base de données Standard configurée à une taille de 250 Go, vous bénéficiez de 500 Go d’espace de stockage de sauvegarde sans coût supplémentaire. Si votre base de données dépasse hello fourni le stockage de sauvegarde, vous pouvez choisir la période de rétention tooreduce hello en contactant le Support technique Azure ou payer pour le stockage de sauvegarde supplémentaire hello facturé au taux Read-Access Geographically Redundant Storage (RA-GRS) standard. Pour plus d’informations sur la facturation RA-GRS, consultez la page Détails de tarification de stockage.

## <a name="im-moving-from-webbusiness-toohello-new-service-tiers-what-do-i-need-tooknow"></a>Je passe à partir du Web/Business toohello nouveaux niveaux de service, comment dois-je tooknow ?
Les bases de données Web et Business SQL Azure sont désormais supprimées. les niveaux de base, Standard, Premium, Premium RS et élastiques Hello remplacent hello mise hors service des bases de données Web et Business. 

## <a name="what-is-an-expected-replication-lag-when-geo-replicating-a-database-between-two-regions-within-hello-same-azure-geography"></a>Qu’est un décalage de réplication attendu lors de la réplication géo-réplication une base de données entre les deux régions dans hello même geography Azure ?
Nous sommes actuellement en charge un RPO de cinq secondes et décalage de réplication hello et a été inférieure à celle lorsque hello secondaires géo-réplication est hébergé dans hello Qu'azure recommandé région associée au hello même niveau de service.

## <a name="what-is-an-expected-replication-lag-when-geo-secondary-is-created-in-hello-same-region-as-hello-primary-database"></a>Qu’est un décalage de réplication attendu lors de la géo-secondaire est créée dans hello même région que la base de données primaire hello ?
Des données empiriques, il n’est pas trop de différence entre intra-région et le décalage de réplication de la région entre lorsque hello Qu'azure recommandé région associée est utilisée. 

## <a name="if-there-is-a-network-failure-between-two-regions-how-does-hello-retry-logic-work-when-geo-replication-is-set-up"></a>S’il existe une défaillance du réseau entre deux régions, logique de nouvelle tentative hello fonctionnement lorsque la géo-réplication est configurée
S’il existe une déconnexion, nous réessayer chaque toore de 10 secondes-établir des connexions.

## <a name="what-can-i-do-tooguarantee-that-a-critical-change-on-hello-primary-database-is-replicated"></a>Que puis-je faire tooguarantee qu’une modification critique sur la base de données primaire hello est répliquée ?
géo-réplication secondaire Hello est un réplica async et nous n’essayez pas de tookeep dans la synchronisation complète avec hello principal. Mais nous fournissent une méthode tooforce synchronisation tooensure hello la réplication des modifications critiques (par exemple, les mises à jour du mot de passe). Synchronisation forcée affecte les performances, car il bloque le thread appelant de hello jusqu'à ce que toutes les transactions validées sont répliquées. Pour plus d’informations, consultez [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx). 

## <a name="what-tools-are-available-toomonitor-hello-replication-lag-between-hello-primary-database-and-geo-secondary"></a>Quels sont les outils disponibles toomonitor décalage de réplication hello hello bases primaire et secondaire de géo-réplication ?
Nous présentons le décalage de réplication en temps réel de hello hello bases primaire et secondaires géo-réplication via une vue de gestion dynamique. Pour plus d’informations, consultez [sys.dm_geo_replication_link_status](https://msdn.microsoft.com/library/mt575504.aspx).

## <a name="toomove-a-database-tooa-different-server-in-hello-same-subscription"></a>toomove un base de données tooa autre serveur hello même abonnement
* Bonjour [portail Azure](https://portal.azure.com), cliquez sur **bases de données SQL**, sélectionnez une base de données à partir de la liste de hello, puis cliquez sur **copie**. Pour plus d’informations, consultez [Copier une base de données SQL Azure](sql-database-copy.md) .

## <a name="toomove-a-database-between-subscriptions"></a>toomove une base de données entre des abonnements
* Bonjour [portail Azure](https://portal.azure.com), cliquez sur **serveurs SQL** puis hello serveur qui héberge votre base de données à partir de la liste de hello. Cliquez sur **déplacer**, puis sélectionner hello ressources toomove et toomove d’abonnement hello pour.
