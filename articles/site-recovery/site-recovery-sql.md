---
title: applications aaaReplicate avec SQL Server et Azure Site Recovery | Documents Microsoft
description: "Cet article décrit comment tooreplicate SQL Server à l’aide d’Azure Site Recovery pour les fonctions de reprise après sinistre de SQL Server."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 99755f2cd2f7e924071f1e230ac4a0bda88f0a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a>Protéger SQL Server à l’aide de la récupération d’urgence SQL Server et d’Azure Site Recovery

Cet article décrit comment tooprotect hello SQL Server back-end d’une application à l’aide d’une combinaison de continuité d’activité SQL Server et les technologies de récupération d’urgence, et [Azure Site Recovery](site-recovery-overview.md).

Avant de commencer, assurez-vous de bien comprendre les fonctionnalités de récupération d’urgence de SQL Server, notamment le clustering de basculement, les groupes de disponibilité AlwaysOn, la mise en miroir de bases de données et la copie des journaux de transaction.


## <a name="sql-server-deployments"></a>Déploiements SQL Server

Nombreuses charges de travail utilisent SQL Server comme base, et il peut être intégré aux applications telles que SAP, les services de données tooimplement, Dynamics et SharePoint.  SQL Server peut être déployé de plusieurs façons :

* **SQL Server autonome**: le serveur SQL et toutes les bases de données sont hébergés sur un seul ordinateur (physique ou une machine virtuelle). Quand le serveur est virtualisé, le cluster hôte est utilisé pour la haute disponibilité locale. La haute disponibilité pour le niveau invité n’est pas mise en œuvre.
* **Instances de clustering de basculement SQL Server (Always On FCI)** : au moins deux nœuds exécutant des instances SQL Server avec des disques partagés sont configurés dans un cluster de basculement Windows. Si un nœud est arrêté, hello cluster permettre basculer SQL Server tooanother instance. Cette configuration est généralement utilisé tooimplement haute disponibilité sur un site principal. Ce déploiement ne protège pas contre les pannes ou de panne dans la couche de stockage partagé hello. Un disque partagé peut être mis en œuvre avec iSCSI, Fibre Channel ou VHDx partagé.
* **Groupes de disponibilité SQL Always On** : au moins deux nœuds sont configurés dans un cluster sans partage avec des bases de données SQL Server configurées dans un groupe de disponibilité avec réplication synchrone et basculement automatique.

 Cet article s’appuie sur hello suivant natifs technologies de récupération d’urgence SQL pour la récupération de site distant tooa de bases de données :

* SQL groupes de disponibilité AlwaysOn, tooprovide pour la récupération d’urgence pour SQL Server 2012 ou 2014 Enterprise Edition.
* Mise en miroir de base de données SQL en mode haute sécurité pour SQL Server édition Standard (toute version) ou SQL Server 2008 R2.

## <a name="site-recovery-support"></a>Prise en charge de Site Recovery

### <a name="supported-scenarios"></a>Scénarios pris en charge
Récupération de site peut protéger SQL Server tel qu’indiqué dans la table de hello.

**Scénario** | **site secondaire de tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Oui | Oui
**VMware** | Oui | Oui
**Serveur physique** | Oui | Oui

### <a name="supported-sql-server-versions"></a>Versions de SQL Server prises en charge
Ces versions de SQL Server sont prises en charge pour les scénarios de hello pris en charge :

* SQL Server 2016 Entreprise et Standard
* SQL Server 2014 Entreprise et Standard
* SQL Server 2012 Entreprise et Standard
* SQL Server 2008 R2 Entreprise et Standard

### <a name="supported-sql-server-integration"></a>Intégration de SQL Server prise en charge

Récupération de site peut être intégrée à des technologies SQL Server BCDR natives résumées dans la table hello, tooprovide une solution de récupération d’urgence.

**Fonctionnalité** | **Détails** | **SQL Server** |
--- | --- | ---
**Groupe de disponibilité AlwaysOn** | Plusieurs instances autonomes de SQL Server s’exécutent chacune dans un cluster de basculement qui comporte plusieurs nœuds.<br/><br/>Les bases de données peuvent être regroupées dans des groupes de basculement qui peuvent être copiés (mis en miroir) sur des instances de SQL Server, pour éviter tout stockage partagé.<br/><br/>Cette fonction assure une récupération d'urgence entre un site primaire et un ou plusieurs sites secondaires. Il est possible de configurer deux nœuds dans un cluster sans partage avec les bases de données SQL Server configurées dans un groupe de disponibilité avec réplication synchrone et basculement automatique. | SQL Server 2014 et 2012 édition Enterprise
**Clustering de basculement (instance de cluster de basculement AlwaysOn)** | SQL Server tire parti de la fonction de cluster de basculement Windows pour assurer la haute disponibilité des charges de travail SQL Server locales.<br/><br/>Les nœuds qui exécutent des instances de SQL Server avec des disques partagés sont configurés dans un cluster de basculement. Si une instance est arrêtée hello basculement cluster toodifferent une.<br/><br/>cluster de Hello ne protège pas contre les pannes ou interruptions dans le stockage partagé. les disques partagés Hello peuvent être implémentée avec iSCSI, Fibre channel, ou partagé Vhdx. | Éditions SQL Server Enterprise<br/><br/>SQL Server Standard edition (nœuds tootwo limitée uniquement)
**Mise en miroir de base de données (mode haute sécurité)** | Protège une copie secondaire de la base de données unique tooa unique. Disponible dans les modes de réplication haute sécurité (synchrone) et hautes performances (asynchrone). Cluster de basculement non requis. | SQL Server 2008 R2<br/><br/>SQL Server Enterprise (toutes les éditions)
**Serveur SQL autonome** | Hello SQL Server et la base de données sont hébergées sur un serveur unique (physique ou virtuel). Cluster hôte est utilisé pour la haute disponibilité en cas hello serveur virtuel. Aucune haute disponibilité pour le niveau invité. | Édition Enterprise ou Standard

## <a name="deployment-recommendations"></a>Recommandations concernant le déploiement

Ce tableau récapitule nos recommandations pour intégrer les technologies BCDR de SQL Server à Site Recovery.

| **Version** | **Édition** | **Déploiement** | **Local tooon localement** | **Local tooAzure** |
| --- | --- | --- | --- | --- |
| SQL Server 2014 ou 2012 |Entreprise |Instance de cluster de basculement |Groupes de disponibilité AlwaysOn |Groupes de disponibilité AlwaysOn |
|| Entreprise |Groupes de disponibilité AlwaysOn pour la haute disponibilité |Groupes de disponibilité AlwaysOn |Groupes de disponibilité AlwaysOn | |
|| Standard |Instance de cluster de basculement (FCI) |Réplication Site Recovery avec miroir local |Réplication Site Recovery avec miroir local | |
|| Enterprise ou Standard |Standalone |Réplication de la récupération de sites |Réplication de la récupération de sites | |
| SQL Server 2008 R2 ou 2008 |Enterprise ou Standard |Instance de cluster de basculement (FCI) |Réplication Site Recovery avec miroir local |Réplication Site Recovery avec miroir local |
|| Enterprise ou Standard |Standalone |Réplication de la récupération de sites |Réplication de la récupération de sites | |
| SQL Server (toute version) |Enterprise ou Standard |Instance de cluster de basculement - application DTC |Réplication de la récupération de sites |Non pris en charge |

## <a name="deployment-prerequisites"></a>Conditions préalables au déploiement

* Un déploiement local de SQL Server exécutant une version prise en charge de SQL Server. En général, il est également nécessaire de configurer Active Directory pour votre serveur SQL.
* configuration requise de Hello pour hello scénario que vous souhaitez toodeploy. En savoir plus sur les exigences de prise en charge pour [tooAzure de réplication](site-recovery-support-matrix-to-azure.md) et [local](site-recovery-support-matrix.md), et [conditions préalables au déploiement](site-recovery-prereq.md).
* tooset la récupération dans Azure, exécution hello [Azure Virtual Machine Readiness Assessment](http://www.microsoft.com/download/details.aspx?id=40898) outil sur vos ordinateurs virtuels SQL Server, toomake assurer qu’ils sont compatibles avec Azure et de récupération de Site.

## <a name="set-up-active-directory"></a>Configurer Active Directory

Configurer Active Directory, dans le site de récupération secondaire hello, pour SQL Server toorun correctement.

* **Petite entreprise**, avec un petit nombre d’applications et de contrôleur de domaine unique pour le site local de hello, si vous souhaitez que toofail sur l’ensemble du site hello, nous vous recommandons d’utiliser Site Recovery réplication tooreplicate hello contrôleur de domaine Centre de données secondaire toohello ou tooAzure.
* **Toolarge moyenne entreprise**: Si vous avez un grand nombre d’applications, une forêt Active Directory, et que vous souhaitez toofail par les applications ou charges de travail, nous vous recommandons de configurer un contrôleur de domaine supplémentaire dans le centre de données secondaire hello ou dans Azure. Si vous utilisez Always On disponibilité groupes toorecover tooa site distant, nous vous recommandons de que vous configurez un autre contrôleur de domaine supplémentaire sur le site secondaire de hello ou dans Azure, toouse d’instance de SQL Server hello récupérée.

instructions Hello dans cet article suppose qu’un contrôleur de domaine est disponible dans l’emplacement secondaire de hello. [ici](site-recovery-active-directory.md) .


## <a name="integrate-with-sql-server-always-on-for-replication-tooazure"></a>Intégrer avec SQL Server Always On pour la réplication tooAzure

Voici ce que vous devez toodo :

1. Importez les scripts sur votre compte Azure Automation. Contient des scripts de hello toofailover groupe de disponibilité SQL dans un [machine virtuelle Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAG.ps1) et un [virtuels standard](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAGClassic.ps1).

    [![Déployer tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)


1. Ajoutez ASR-SQL-FailoverAG comme une action de versions antérieures du premier groupe de hello hello du plan de récupération.

1. Suivez les instructions de hello disponibles dans hello script toocreate un nom de hello tooprovide variable automation hello des groupes de disponibilité.

### <a name="steps-toodo-a-test-failover"></a>Étapes toodo un test de basculement

SQL AlwaysOn ne prend pas en charge le test de basculement de manière native. Par conséquent, nous vous recommandons de suivant de hello :

1. Configurer [Azure Backup](../backup/backup-azure-vms.md) sur l’ordinateur virtuel hello qui héberge le réplica de groupe de disponibilité hello dans Azure.

1. Avant de déclencher un test de basculement hello du plan de récupération, récupérez hello virtual machine à partir de la sauvegarde de hello effectuée à l’étape précédente de hello.

    ![Restauration à partir de Sauvegarde Azure ](./media/site-recovery-sql/restore-from-backup.png)

1. [Forcer un quorum](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum#PowerShellProcedure) dans la machine virtuelle de hello restauré à partir de la sauvegarde.

1. Mettre à jour d’adresse IP de hello écouteur tooan IP disponible dans le réseau de basculement de test hello.

    ![Mettre à jour l’adresse IP de l’écouteur](./media/site-recovery-sql/update-listener-ip.png)

1. Mettez l’écouteur en ligne.

    ![Mettre l’écouteur en ligne](./media/site-recovery-sql/bring-listener-online.png)

1. Créez un équilibreur de charge avec une adresse IP créée sous le serveur frontal IP pool correspondante tooeach écouteur et ajouté dans le pool principal d’hello un ordinateur virtuel SQL hello.

     ![Créer un équilibrage de charge – pool d’adresses IP frontal ](./media/site-recovery-sql/create-load-balancer1.png)

    ![Créer un équilibrage de charge – pool principal ](./media/site-recovery-sql/create-load-balancer2.png)

1. Effectuez un test de basculement hello du plan de récupération.

### <a name="steps-toodo-a-failover"></a>Étapes toodo un basculement

Une fois que vous avez ajouté le script de hello dans le plan de récupération hello et plan de récupération hello validé en effectuant un test de basculement, vous pouvez effectuer le basculement hello du plan de récupération.


## <a name="integrate-with-sql-server-always-on-for-replication-tooa-secondary-on-premises-site"></a>Intégration avec SQL Server Always On pour le site de réplication tooa sur site secondaire

Hello SQL Server est à l’aide de groupes de disponibilité pour une haute disponibilité (ou une instance FCI), nous vous recommandons à l’aide de groupes de disponibilité sur le site de récupération hello également. Notez que cela s’applique tooapps qui n’utilisent pas les transactions distribuées.

1. [Configurez les bases de données](https://msdn.microsoft.com/library/hh213078.aspx) dans des groupes de disponibilité.
1. Créer un réseau virtuel sur le site secondaire de hello.
1. Configurer une connexion VPN de site à site entre le réseau virtuel de hello et le site principal de hello.
1. Créer un ordinateur virtuel sur le site de récupération hello et installer SQL Server sur ce dernier.
1. Étendre hello existant Always On disponibilité groupes toohello nouvelle machine virtuelle de serveur SQL. Configurez cette instance SQL Server comme une copie de réplica asynchrone.
1. Créer un écouteur de groupe de disponibilité, ou mettre à jour de hello écouteur tooinclude hello réplica asynchrone ordinateur virtuel.
1. Assurez-vous que cette batterie de serveurs application hello est configuré à l’aide du port d’écoute hello. S’il est le programme d’installation à l’aide du nom du serveur de base de données hello, mettez-le à jour écouteur de hello toouse, vous n’avez pas besoin tooreconfigure après le basculement de hello.

Pour les applications qui utilisent des transactions distribuées, nous vous recommandons de déployer Site Recovery avec la [réplication de site à site avec serveur physique / VMware](site-recovery-vmware-to-vmware.md).

### <a name="recovery-plan-considerations"></a>Considérations concernant le plan de récupération
1. Ajoutez cette bibliothèque exemple script toohello VMM, sur les sites principaux et secondaires hello.

        Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force

1. Lorsque vous créez un plan de récupération pour une application hello, ajoutez une pre action tooGroup-1 sous forme de script étape, qui appelle hello script toofail sur les groupes de disponibilité.

## <a name="protect-a-standalone-sql-server"></a>Protéger un serveur SQL Server autonome

Dans ce scénario, nous vous recommandons d’utiliser l’ordinateur SQL Server Site Recovery réplication tooprotect hello. les étapes exactes Hello dépendra si SQL Server est un ordinateur virtuel ou un serveur physique et si vous souhaitez tooreplicate tooAzure ou une base de données secondaire site local. En savoir plus sur les [scénarios Site Recovery](site-recovery-overview.md).

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a>Protéger un cluster SQL Server (Standard Edition/Windows Server 2008 R2)

Pour un cluster SQL Server Standard edition ou SQL Server 2008 R2, nous vous recommandons de qu'utiliser la réplication de Site Recovery tooprotect SQL Server.

### <a name="on-premises-tooon-premises"></a>Tooon-site local

* Si l’application hello utilise des transactions distribuées nous vous recommandons de déployer [Site Recovery avec la réplication SAN](site-recovery-vmm-san.md) pour un environnement Hyper-V, ou [tooVMware du serveur VMware/physiques](site-recovery-vmware-to-vmware.md) d’un environnement VMware.
* Pour les applications non-DTC, utilisez hello au-dessus de cluster de hello toorecover approche comme serveur autonome, en tirant parti d’une mise en miroir de base de données locale haute sécurité.

### <a name="on-premises-tooazure"></a>Local tooAzure

Récupération de site ne fournit pas invité prise en charge de cluster lors de la réplication tooAzure. De même, SQL Server n’inclut aucune solution de récupération d'urgence à faible coût dans l’édition Standard. Dans ce scénario, nous vous recommandons de vous protégez hello local SQL Server cluster tooa autonome SQL Server et les restaurer dans Azure.

1. Configurer une instance de SQL Server autonome supplémentaires sur le site local de hello.
1. Configurer hello instance tooserve comme une mise en miroir de bases de données hello vous souhaitez tooprotect. Configurez la mise en miroir en mode haute sécurité.
1. Configurer la récupération de Site sur le site local de hello, pour ([Hyper-V](site-recovery-hyper-v-site-to-azure.md) ou [des serveurs VMware machines virtuelles/physiques)](site-recovery-vmware-to-azure-classic.md).
1. Utilisez le nouveau SQL Server instance tooAzure de récupération de Site réplication tooreplicate hello. S’agissant d’une copie miroir de haute sécurité, il sera synchronisé avec le cluster principal de hello, mais il sera répliqué tooAzure à l’aide de la réplication de la récupération de Site.


![Cluster standard](./media/site-recovery-sql/standalone-cluster-local.png)

### <a name="failback-considerations"></a>Considérations en matière de restauration automatique

Pour les clusters SQL Server Standard, la restauration automatique après un basculement non planifié nécessite une sauvegarde de SQL server et de restauration, de hello miroir instance toohello cluster d’origine, avec le rétablissement de la mise en miroir hello.

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus](site-recovery-components.md) sur l’architecture de Site Recovery.
