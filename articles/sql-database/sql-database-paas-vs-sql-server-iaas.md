---
title: "vs de base de données aaaSQL (PaaS). SQL Server dans le cloud hello sur des machines virtuelles (IaaS) | Documents Microsoft"
description: "En savoir quelle option de SQL Server cloud adaptée à votre application : base de données SQL de Azure (PaaS) ou SQL Server dans le cloud hello sur des Machines virtuelles Azure."
services: sql-database, virtual-machines
keywords: "Cloud de SQL Server, SQL Server dans le cloud hello, PaaS de base de données, SQL Server, DBaaS de cloud"
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cjgronlund
ms.assetid: 7467f422-b77d-4b60-9cb5-0f1ec17ec565
ms.service: sql-database
ms.custom: DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: carlrab
ms.openlocfilehash: 1b462a9a822d04dc5deb8422ed505a5d09279253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-cloud-sql-server-option-azure-sql-paas-database-or-sql-server-on-azure-vms-iaas"></a>Choisir une option de SQL Server cloud : Base de données SQL Azure (PaaS) ou SQL Server sur des machines virtuelles Azure (IaaS)
Azure propose deux options pour héberger des charges de travail SQL Server dans Microsoft Azure :

* [Base de données SQL Azure](https://azure.microsoft.com/services/sql-database/): cloud de toohello natif SQL d’une base de données, également appelé une plateforme en tant qu’une base de données de service (PaaS) ou une base de données en tant que service (DBaaS) qui est optimisé pour le développement d’applications software-as-a-service (SaaS). Elle est compatible avec la plupart des fonctionnalités de SQL Server. Pour plus d’informations sur le PaaS, consultez la page [Qu’est-ce que le PaaS](https://azure.microsoft.com/overview/what-is-paas/).
* [SQL Server sur des Machines virtuelles Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/): SQL Server installé et hébergé dans le cloud de hello sur Windows Server des Machines virtuelles (VM) s’exécutant sur Azure, également appelé une infrastructure en tant que service (IaaS).
  SQL Server sur les machines virtuelles Azure est optimisé pour la migration d’applications SQL Server existantes. Tous les hello versions et éditions de SQL Server sont disponibles. Il offre une compatibilité de 100 % avec SQL Server, toohost vous permettant ainsi qu’un grand nombre de bases de données en tant que les transactions entre bases de données nécessaires et en cours d’exécution. Il apporte un contrôle total sur SQL Server et Windows.

Découvrez comment chaque option s’adapte à la plate-forme de données Microsoft hello et obtenir l’aide correspondante hello option droite tooyour besoins de l’entreprise. Si vous hiérarchiser les économies ou une administration minimale avant tout le reste, cet article peut vous aider à décider quelle approche offre par rapport aux exigences d’entreprise hello que vous intéressent le plus.

## <a name="microsofts-data-platform"></a>Plateforme de données de Microsoft
Un des hello première choses toounderstand dans toute discussion de Azure par rapport aux bases de données locale SQL Server est que vous pouvez utiliser toutes les. La plateforme de données de Microsoft utilise la technologie SQL Server et la rend disponible sur les machines physiques locales, les environnements de cloud privé, les environnements de cloud privé hébergé par un tiers et le cloud public. SQL Server sur des machines virtuelles vous permet de toomeet unique et divers besoins par une combinaison des locaux et les déploiements basés sur le cloud, tandis qu’à l’aide de hello même ensemble de produits serveur, les outils de développement et le savoir-faire ces environnements.

   ![Options de SQL Server en nuage : la base de données SQL server sur IaaS ou SaaS SQL dans le cloud de hello.](./media/sql-database-paas-vs-sql-server-iaas/SQLIAAS_SQL_Server_Cloud_Continuum.png)

Comme indiqué dans le diagramme de hello, chaque offre peut être caractérisé par niveau hello d’administration sur l’infrastructure hello (sur l’axe des X de hello) et par le degré de hello de rentabilité résultant de la consolidation de niveau base de données et d’automatisation (sur l’axe des Y de hello).

Lorsque vous concevez une application, les quatre options de base sont disponibles pour l’hébergement de partie de SQL Server hello de l’application hello :

* SQL Server sur des machines physiques non virtualisées
* SQL Server sur des machines virtualisées locales (cloud privé)
* SQL Server sur Azure Virtual Machines (cloud public Microsoft)
* Base de données SQL Azure (cloud public Microsoft)

Bonjour les sections suivantes, vous en savoir plus sur SQL Server Bonjour cloud public Microsoft : base de données SQL Azure et SQL Server sur des machines virtuelles Azure. Vous allez également explorer les motivations commerciales courantes permettant de déterminer l’option qui convient le mieux à votre application.

## <a name="a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms"></a>Étude détaillée d’Azure SQL Database et de SQL Server sur les machines virtuelles Azure
**Base de données SQL Azure** est un relationnel de base de données-as-a-service (DBaaS) hébergé dans hello cloud Azure qui se situe en catégories d’industrie hello de *Software-as-a-Service (SaaS)* et *Platform-as-a-Service (PaaS)* . [Base de données SQL](sql-database-technical-overview.md) repose sur du matériel et des logiciels standardisés, qui sont détenus, hébergés et gérés par Microsoft. Avec la base de données SQL, vous pouvez développer directement sur le service hello à l’aide de fonctionnalités intégrées. Lors de l’utilisation de base de données SQL, vous le paiement à l’utilisation avec les options tooscale façon horizontale ou verticale de puissance sans interruption.

**SQL Server sur Azure des Machines virtuelles (VM)** se situe dans la catégorie d’industrie hello *Infrastructure-as-a-Service (IaaS)* et vous permet de toorun SQL Server à l’intérieur d’une machine virtuelle dans le cloud de hello. TooSQL comme base de données, il est construit sur du matériel standardisé détenu, hébergé et géré par Microsoft. Quand vous utilisez SQL Server sur une machine virtuelle, vous pouvez payer à l’utilisation pour une licence SQL Server déjà incluse dans une image SQL Server ou utiliser simplement une licence existante. Vous pouvez également facilement échelle-haut/bas et pause/reprise hello machine virtuelle en fonction des besoins.

En général, ces deux options SQL sont optimisées à différentes fins :

* **Base de données SQL Azure** est optimisé tooreduce les coûts globaux toohello minimale pour l’approvisionnement et la gestion de plusieurs bases de données. Il réduit les coûts d’administration en cours, car vous n’avez pas toomanage d’ordinateurs virtuels, le système d’exploitation ou le logiciel de base de données. Vous n’avez pas de mises à niveau de toomanage, haute disponibilité, ou [sauvegardes](sql-database-automated-backups.md). En général, la base de données SQL Azure peuvent améliorer considérablement nombre hello de bases de données gérées par un seul service informatique ou les ressources de développement.
* **SQL Server s’exécutant sur des machines virtuelles Azure** est optimisée pour migration d’existant tooAzure d’applications ou d’extension de cloud de toohello d’applications dans les déploiements hybrides locales existantes. En outre, vous pouvez utiliser SQL Server dans un toodevelop de l’ordinateur virtuel et tester les applications traditionnelles de SQL Server. Avec SQL Server sur des machines virtuelles Azure, vous disposez des droits d’administration complets de hello sur une instance dédiée de SQL Server et une machine virtuelle basée sur le cloud. Il est le choix idéal lorsqu’une organisation possède déjà les ordinateurs virtuels hello informatique ressources toomaintain disponibles. Ces fonctionnalités vous permettent de toobuild un tooaddress système hautement personnalisée performances spécifiques et des exigences de disponibilité de votre application.

Hello tableau suivant résume les principales caractéristiques de hello de base de données SQL et SQL Server sur des machines virtuelles Azure :

| **Idéal pour :** | **Base de données SQL Azure** | **SQL Server sur une machine virtuelle Azure** |
| --- | --- | --- |
|  |Nouvelles applications conçues pour le cloud qui ont des contraintes de temps de développement et de marketing. |Applications existantes qui nécessitent le cloud de toohello migration rapide avec des modifications minimes. Développement et test situations rapide lorsque vous ne souhaitez pas de matériel de SQL Server hors production toobuy sur site. |
|  | Équipes qui ont besoin d’une haute disponibilité intégrée, la récupération d’urgence et mise à niveau de base de données hello. |Équipes qui peuvent configurer et gérer une haute disponibilité, une récupération d’urgence et une mise à jour corrective pour SQL Server. Certaines fonctionnalités automatisées simplifient considérablement cette procédure. | |
|  | Équipes que vous ne souhaitez pas que les paramètres de configuration et de système d’exploitation sous-jacent de toomanage hello. |Vous avez besoin d’un environnement personnalisé avec des droits d’administration complets. | |
|  | Bases de données de configuration too4 to ou des bases de données volumineuses qui peuvent être [horizontalement ou verticalement partitionnée](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling) à l’aide d’un modèle de montée en puissance parallèle. |Instances de SQL Server avec jusqu'à too64 to de stockage. instance de Hello peut prendre en charge qu’un grand nombre de bases de données en fonction des besoins. | |
|  | [Création d’applications SaaS (logiciel en tant que service)](sql-database-design-patterns-multi-tenancy-saas-applications.md). |Migration et création d’applications d’entreprise et hybrides. | |
|  | | |
| **Ressources :** |Vous ne souhaitez pas tooemploy informatique ressources pour la configuration et la gestion de hello sous-jacent d’infrastructure, mais que voulez toofocus sur la couche d’application hello. |Vous disposez de ressources informatiques pour la configuration et la gestion. Certaines fonctionnalités automatisées simplifient considérablement cette procédure. |
| **Coût total de possession :** |Élimine les coûts matériels et réduit les coûts d’administration. |Élimine les coûts matériels. |
| **Continuité des activités :** |En outre toobuilt dans des infrastructures fonctionnalités de tolérance, base de données SQL Azure fournit des fonctionnalités, telles que [sauvegardes automatisées](sql-database-automated-backups.md), [Point-à-temps restauration](sql-database-recovery-using-backups.md#point-in-time-restore), [géo-restauration](sql-database-recovery-using-backups.md#geo-restore), et [géo-réplication active](sql-database-geo-replication-overview.md) tooincrease continuité d’activité. Pour plus d’informations, voir [Vue d’ensemble de la continuité des activités de la base de données SQL Azure](sql-database-business-continuity.md). |L’option SQL Server sur les machines virtuelles Azure vous permet de configurer une solution de haute disponibilité et de récupération d’urgence pour les besoins spécifiques de votre base de données. Vous pouvez donc disposer d'un système hautement optimisé pour votre application. Vous pouvez tester et exécuter des basculements par vous-même si nécessaire. Pour plus d’informations, voir [Haute disponibilité et récupération d’urgence pour SQL Server dans Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md). |
| **Cloud hybride :** |Votre application locale peut accéder aux données d’Azure SQL Database. |Avec SQL Server sur des machines virtuelles Azure, vous pouvez avoir des applications qui s’exécutent en partie dans le cloud de hello et en partie localement. Par exemple, vous pouvez étendre votre réseau local et le cloud de toohello de domaine Active Directory via [réseau virtuel Azure](../virtual-network/virtual-networks-overview.md). En outre, vous pouvez stocker des fichiers de données locaux dans Azure Storage en utilisant les [fichiers de données SQL Server dans Azure](http://msdn.microsoft.com/library/dn385720.aspx). Pour plus d’informations, consultez [Introduction tooSQL Cloud hybride de Server 2014](http://msdn.microsoft.com/library/dn606154.aspx). |
|  | Prend en charge [la réplication transactionnelle SQL Server](https://msdn.microsoft.com/library/mt589530.aspx) tooreplicate données abonné. |Prend entièrement en charge [la réplication transactionnelle SQL Server](https://msdn.microsoft.com/library/mt589530.aspx), [groupes de disponibilité AlwaysOn](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md), Integration Services et les journaux de transaction des données tooreplicate. En outre, les sauvegardes traditionnelles SQL Server sont entièrement prises en charge | |
|  | | |

## <a name="business-motivations-for-choosing-azure-sql-database-or-sql-server-on-azure-vms"></a>Critères pour choisir entre Azure SQL Database et SQL Server sur les machines virtuelles Azure
### <a name="cost"></a>Coût
Si vous êtes un démarrage est fixé pour trésorerie, ou une équipe dans une société établie qui fonctionne avec les contraintes de budget serré, limitées financement est souvent pilote principal de hello lorsque vous décidez comment toohost vos bases de données. Dans cette section, vous en savoir plus sur la facturation hello et Gestionnaire de licences principes fondamentaux dans Azure avec ce qui concerne les deux options de base de données relationnelle toothese : base de données SQL et SQL Server sur des machines virtuelles Azure. Vous découvrirez également sur le calcul du coût d’application total hello.

#### <a name="billing-and-licensing-basics"></a>Notions de base sur la facturation et les licences
**Base de données SQL** vendu toocustomers en tant que service, pas avec une licence.  [SQL Server sur les machines virtuelles Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md) est vendu avec une licence incluse que vous payez à la minute. Si vous disposez déjà d’une licence, vous pouvez également l’utiliser.  

Actuellement, **base de données SQL** est disponible dans plusieurs niveaux de service, qui sont facturées par heure à un taux fixe en fonction de hello service niveau et les performances du niveau choisis. Par ailleurs, vous êtes facturé pour le trafic internet sortant aux [tarifs de transfert de données](https://azure.microsoft.com/pricing/details/data-transfers/)standard. Hello Basic, Standard, Premium, et Premium service Reporting Services sont des niveaux conçu toodeliver des performances prévisibles avec plusieurs toomatch de niveaux de performances pointe exigences de votre application. Vous pouvez modifier entre les niveaux de service et toomatch de niveaux de performances qu'a besoin d’un débit variées de votre application. Si votre base de données a haute toosupport transactionnelle de volume et les besoins de nombreux utilisateurs simultanés, nous vous recommandons de niveau de service Premium hello. Hello dernières informations sur les niveaux de service en cours de hello pris en charge, consultez [niveaux de Service de base de données SQL Azure](sql-database-service-tiers.md). Vous pouvez également créer [pools élastiques](sql-database-elastic-pool.md) tooshare de ressources de performances entre les instances de base de données.

Avec **base de données SQL**, logiciel de base de données hello est automatiquement configuré, corrigé et mis à niveau par Microsoft, ce qui réduit les coûts d’administration. En outre, ses fonctionnalités de [sauvegarde intégrée](sql-database-automated-backups.md) vous permettent de réaliser d’importantes économies, notamment si vous avez un grand nombre de bases de données.

Avec **SQL Server sur des machines virtuelles Azure**, vous pouvez utiliser une des hello fournie par la plateforme images SQL Server (qui inclut une licence) ou mettre votre licence de SQL Server. Prise en charge de hello toutes les versions de SQL Server (2008 R2, 2012, 2014, 2016) et éditions (Developer, Express, Web, Standard, entreprise) sont disponibles. En outre, les versions Bring-Your-propre-licence (BYOL) des images de hello sont disponibles. Lorsque vous utilisez hello Qu'azure les images fournies, les coûts de fonctionnement hello dépend de taille de machine virtuelle hello et l’édition de hello de SQL Server, vous choisissez. Quelle que soit la taille de machine virtuelle ou l’édition de SQL Server, vous payez par minute coût de la licence de SQL Server et Windows Server, ainsi que de hello coût de stockage Azure pour les disques de machine virtuelle hello. option de facturation par minute Hello permet toouse SQL Server aussi longtemps que nécessaire sans acheter plus de licences de SQL Server. Si vous ajoutez vos propres tooAzure de licence de SQL Server, vous êtes facturé pour Windows Server et les coûts de stockage uniquement. Pour plus d’informations sur l’utilisation de votre propre licence, consultez [License Mobility via Software Assurance sur Azure](https://azure.microsoft.com/pricing/license-mobility/).

#### <a name="calculating-hello-total-application-cost"></a>Calcul du coût d’application total hello
Lorsque vous démarrez à l’aide d’une plateforme cloud, coût hello de l’exécution de votre application inclut développement de hello et les coûts d’administration, ainsi que les coûts du service de plate-forme hello cloud public.

Voici hello du calcul du coût détaillées pour votre application en cours d’exécution dans la base de données SQL et SQL Server sur des machines virtuelles Azure :

**Avec Azure SQL Database :**

*Coût total de l’application = coûts d’administration très réduits + coûts de développement logiciel + coûts du service SQL Database*

**Avec SQL Server sur les machines virtuelles Azure :**

*Coût total de l’application = coûts considérablement réduits de développement logiciel + coûts d’administration + coûts des licences SQL Server et Windows Server + coûts de stockage Azure*

Pour plus d’informations sur la tarification, consultez hello suivant des ressources :

* [Tarification des bases de données SQL](https://azure.microsoft.com/pricing/details/sql-database/)
* [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/) pour [SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#sql) et [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#windows)
* [Calcul des coûts Azure](https://azure.microsoft.com/pricing/calculator/)

> [!NOTE]
> Dans SQL Serveur, quelques fonctionnalités ne sont pas applicables ou disponibles avec SQL Database. Pour plus d’informations, consultez [Fonctionnalités de SQL Database](sql-database-features.md) et [Informations sur les instructions Transact-SQL de SQL Database](sql-database-transact-sql-information.md). Si vous déplacez un cloud toohello de solution SQL Server existant, consultez [un tooAzure de base de données SQL Server de la base de données SQL de la migration](sql-database-cloud-migrate.md). Lorsque vous migrez un tooSQL application de SQL Server existante sur site de base de données, envisagez de mise à jour de parti de tootake application hello des capacités de hello qui offre des services de cloud computing. Par exemple, vous pouvez envisager d’utiliser [du Service d’applications Web Azure](https://azure.microsoft.com/services/app-service/web/) ou [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services/) toohost avantages de coût de votre tooincrease de couche application.
> 
> 

### <a name="administration"></a>Administration
Pour de nombreuses entreprises, le service cloud tooa hello décision tootransition est ainsi que beaucoup sur le déchargement de la complexité d’administration qu’elle coût. Avec **base de données SQL**, Microsoft administre hello matériel sous-jacent. Microsoft automatiquement réplique toutes les données tooprovide élevé de disponibilité, configure et met à niveau le logiciel de base de données hello, gère l’équilibrage de charge et est le basculement transparent s’il existe une défaillance du serveur. Vous pouvez continuer à tooadminister votre base de données, mais vous n’avez plus besoin du moteur de base de données toomanage hello, de système d’exploitation serveur ou de matériel.  Exemples d’éléments que vous pouvez continuer de tooadminister incluent les bases de données et connexions, index et paramétrage des requêtes et l’audit et sécurité.

Avec **SQL Server sur des machines virtuelles Azure**, vous avez un contrôle total sur le système d’exploitation de hello et configuration de l’instance SQL Server. Avec une machine virtuelle, c’est tooyou toodecide lors de la mise à niveau de tooupdate/hello logiciel de base de données et du système d’exploitation et tooinstall des logiciels supplémentaires tels que les antivirus. Certaines fonctionnalités automatisées sont fournies toodramatically simplifier la gestion des correctifs, la sauvegarde et la haute disponibilité. En outre, vous pouvez contrôler la taille hello Hello VM, hello nombre de disques et leurs configurations de stockage. Azure vous permet de taille de hello toochange d’une machine virtuelle en fonction des besoins. Pour plus d’informations, consultez [Tailles de machines virtuelles et de services cloud pour Azure](../virtual-machines/windows/sizes.md). 

### <a name="service-level-agreement-sla"></a>Contrat de Niveau de Service (SLA)
Pour bon nombre de services informatiques, répondre aux obligations de temps d’exécution d’un contrat de niveau de service (SLA) est la priorité absolue. Dans cette section, nous examinons ce qui applique les SLA option d’hébergement de la base de données tooeach.

Pour **SQL Database**, avec les niveaux de service De base, Standard, Premium et Premium RS, Microsoft fournit un contrat SLA dont la disponibilité est de 99,99 %. Pour plus d’informations hello plus récente, consultez [contrat de niveau de Service](https://azure.microsoft.com/support/legal/sla/sql-database/). Hello dernières informations sur les niveaux de service de base de données SQL et les plans de continuité des activités hello pris en charge, consultez [niveaux de Service](sql-database-service-tiers.md).

Pour **SQL Server s’exécutant sur des machines virtuelles Azure**, Microsoft fournit un contrat SLA de 99,95 % de disponibilité que couvre hello simplement l’ordinateur virtuel. Ce contrat SLA ne couvre pas les processus hello (par exemple, SQL Server) en cours d’exécution sur la machine virtuelle de hello et requiert que vous hébergez d’au moins deux instances de machine virtuelle dans un ensemble de disponibilité. Pour plus d’informations plus récentes hello, consultez hello [SLA de la machine virtuelle](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Pour la base de données haute disponibilité (HA) dans des ordinateurs virtuels, vous devez configurer une des options de haute disponibilité hello pris en charge dans SQL Server, tels que [groupes de disponibilité AlwaysOn](http://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx). À l’aide d’une option de prise en charge de haute disponibilité ne fournit pas un contrat SLA supplémentaire, mais vous permet de tooachieve > disponibilité de base de données de 99,99 %.

### <a name="market"></a>Heure toomarket
**Base de données SQL** est hello de bonne solution pour les applications de cloud conçue lors de la productivité des développeurs et les temps de commercialisation rapide sont critiques. Avec les fonctionnalités de programmation comme le DBA, il est parfait pour cloud architectes et développeurs comme il réduit la nécessité de hello pour la gestion de la base de données et du système d’exploitation sous-jacent de hello. Par exemple, vous pouvez utiliser hello [API REST](http://msdn.microsoft.com/library/azure/dn505719.aspx) et [PowerShell Cmdlets](http://msdn.microsoft.com/library/mt740629.aspx) tooautomate et de gérer les opérations d’administration pour des milliers de bases de données. Fonctionnalités, telles que [pools élastiques](sql-database-elastic-pool.md) vous toofocus sur la couche d’application hello et fournir votre marché toohello de solution plus rapidement.

**SQL Server s’exécutant sur des machines virtuelles Azure** est parfait, si vos applications existantes ou nouvelles requièrent des bases de données volumineuses, les bases de données reliées entre elles, ou accéder aux fonctionnalités de tooall dans SQL Server ou Windows. Il est également adapté lorsque vous souhaitez toomigrate existant sur le site tooAzure de bases de données et applications en tant que-est. Étant donné que vous n’avez pas besoin de présentation de hello toochange, application et les couches de données, vous économisez du temps et budget sur remaniement de votre solution existante. Au lieu de cela, vous pouvez vous concentrer sur la migration de tous les tooAzure de vos solutions et en faisant certaines optimisations de performances qui peuvent être requis par hello plateforme Azure. Pour plus d’informations, consultez [Meilleures pratiques relatives aux performances de SQL Server dans les machines virtuelles Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md).

## <a name="summary"></a>Résumé
Cet article a décrit les options SQL Database et SQL Server sur les machines virtuelles Azure, ainsi que les critères les plus courants susceptibles d’influencer votre décision. Hello Voici un résumé des suggestions pour vous tooconsider :

Choisissez **Azure SQL Database** dans les cas suivants :

* Vous êtes construction nouvelle les applications cloud parti tootake d’optimisation de performances et d’économies de coût hello qui services de cloud computing fournissent. Cette approche offre les avantages de hello d’un service cloud entièrement géré, vous aide à inférieur initial temps sur le marché et permet d’optimiser les coûts à long terme.
* Vous souhaitez toohave Microsoft effectuer les opérations courantes de gestion de vos bases de données et nécessitent des contrats SLA de disponibilité plus élevée pour les bases de données.

Choisissez **SQL Server sur les machines virtuelles Azure** dans les cas suivants :

* Vous avez des applications existantes sur site que vous souhaitez toomigrate ou étendez toohello cloud, ou si vous souhaitez que les applications d’entreprise toobuild supérieure à 4 To. Cette approche offre l’avantage hello de compatibilité SQL 100 %, capacité de la base de données volumineuse, un contrôle total sur SQL Server et Windows et sécurisé de tunneling tooon en local. Cette approche réduit les coûts de développement et de modification des applications existantes.
* Vous disposez de ressources informatiques et vous pouvez bénéficier en fin de compte des correctifs, des sauvegardes et de la haute disponibilité de la base de données. Certaines fonctionnalités automatisées simplifient considérablement ces opérations. 

## <a name="next-steps"></a>Étapes suivantes
* Consultez [votre première base de données SQL Azure](sql-database-get-started-portal.md) tooget main de la base de données SQL.
* Voir [Tarification de Base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/).
* Consultez [configurer un ordinateur virtuel de SQL Server dans Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md) tooget en main de SQL Server sur des machines virtuelles Azure.

