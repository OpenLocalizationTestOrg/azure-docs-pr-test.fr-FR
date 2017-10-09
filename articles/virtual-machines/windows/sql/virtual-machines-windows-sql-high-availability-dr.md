---
title: "aaaHigh disponibilité et récupération d’urgence pour SQL Server | Documents Microsoft"
description: "En savoir plus sur hello différents types de stratégies HADR pour SQL Server s’exécutant sur des Machines virtuelles Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 53981f7e-8370-4979-b26a-93a5988d905f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: mikeray
ms.openlocfilehash: 2b62d8b30520952ba6b7da7177a2c2de95bea8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-and-disaster-recovery-for-sql-server-in-azure-virtual-machines"></a>Haute disponibilité et récupération d’urgence pour SQL Server dans Azure Virtual Machines

Microsoft Azure virtual machines virtuelles avec SQL Server peut aider à réduire le coût hello de solution de haute disponibilité et d’urgence (HADR) de récupération de base de données. La plupart des solutions HADR SQL Server sont prises en charge dans les machines virtuelles Azure, en tant que solutions Azure uniquement et solutions hybrides. Dans une solution Azure uniquement, le système HADR hello s’exécute dans Azure. Dans une configuration hybride, la partie de la solution de hello s’exécute dans Azure et hello autre partie est exécutée localement dans votre organisation. Hello souplesse de hello environnement Azure vous permet de toomove partiellement ou totalement budgétaire de hello tooAzure toosatisfy exigences HADR et de votre serveur SQL Server de base de données système.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="understanding-hello-need-for-an-hadr-solution"></a>Comprendre les besoins de hello pour une solution HADR
C’est tooyou tooensure que votre système de base de données possède des fonctions HADR hello qui hello contrat de niveau de service (SLA). Hello fait que Azure fournisse des mécanismes de haute disponibilité, telles que le service de réparation pour les services de cloud computing et la détection des ordinateurs virtuels, de la récupération de défaillance n’est pas garantie que vous permettent de respecter les SLA hello souhaité. Ces mécanismes protègent hello haute disponibilité des machines virtuelles de hello mais pas hello haute disponibilité de SQL Server est en cours d’exécution à l’intérieur de hello machines virtuelles. Il est possible pour hello SQL Server instance toofail tandis que hello machine virtuelle est en ligne et sain. En outre, les mécanismes de haute disponibilité de même hello fournies par Azure offrent des temps morts des machines virtuelles de hello échéance tooevents tels que la récupération de défaillances logicielles ou matérielles et des mises à niveau du système d’exploitation.

Par ailleurs, le stockage géo-redondant dans Azure (implémenté via la fonctionnalité de géo-réplication) peut ne pas être une solution de récupération d’urgence adaptée pour vos bases de données. Étant donné que la géo-réplication envoie les données de façon asynchrone, mises à jour récentes peuvent être perdus en cas de hello de sinistre. Plus d’informations concernant les limitations de géo-réplication sont traités dans hello [géo-réplication non pris en charge pour les données et fichiers journaux sur des disques distincts](#geo-replication-support) section.

## <a name="hadr-deployment-architectures"></a>Architectures de déploiement HADR
Les technologies HADR SQL Server prises en charge dans Azure incluent :

* [Groupes de disponibilité AlwaysOn](https://technet.microsoft.com/library/hh510230.aspx)
* [Instances de cluster de basculement AlwaysOn](https://technet.microsoft.com/library/ms189134.aspx)
* [Copie des journaux de transaction](https://technet.microsoft.com/library/ms187103.aspx)
* [Sauvegarde et restauration SQL Server avec le service de stockage d’objets blob Azure](https://msdn.microsoft.com/library/jj919148.aspx)
* [Mise en miroir de base de données](https://technet.microsoft.com/library/ms189852.aspx) - Déconseillée dans SQL Server 2016

Il est possible de toocombine hello technologies ensemble tooimplement une solution SQL Server qui a une haute disponibilité et les fonctionnalités de récupération d’urgence. En fonction de la technologie hello que vous utilisez, un déploiement hybride peut nécessiter un tunnel VPN avec hello réseau virtuel Azure. Hello sections ci-dessous illustrent certaines des architectures de déploiement exemple hello.

## <a name="azure-only-high-availability-solutions"></a>Azure uniquement : solutions de haute disponibilité

Vous disposez d’une solution de haute disponibilité pour SQL Server au niveau de la base de données avec des groupes de disponibilité AlwaysOn (groupes de disponibilité). Vous pouvez également créer une solution de haute disponibilité au niveau de l’instance avec des instances de cluster de basculement AlwaysOn (instances de cluster de basculement). Pour une redondance accrue, vous pouvez créer une redondance aux deux niveaux en créant des groupes de disponibilité sur les instances de cluster de basculement. 

| Technology | Exemples d’architecture |
| --- | --- |
| **Groupes de disponibilité** |Réplicas de disponibilité en cours d’exécution des machines virtuelles dans Azure hello même région de fournir une haute disponibilité. Vous devez tooconfigure un machine virtuelle, du contrôleur de domaine, car le clustering de basculement Windows requiert un domaine Active Directory.<br/> ![Groupes de disponibilité](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_ha_always_on.gif)<br/>Pour plus d’informations, consultez la section [Configurer des groupes de disponibilité dans Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md). |
| **Instances de cluster de basculement** |Les instances de cluster de basculement (FCI) qui nécessitent un stockage partagé, peuvent être créées de 3 manières.<br/><br/>1. Un cluster de basculement à deux nœuds en cours d’exécution dans des machines virtuelles Azure à l’aide du stockage en attachement [espaces de stockage Windows Server 2016 Direct \(S2D\) ](virtual-machines-windows-portal-sql-create-failover-cluster.md) tooprovide un réseau SAN virtuel basé sur le logiciel.<br/><br/>2. Un cluster de basculement à deux nœuds exécuté sur des machines virtuelles Azure avec le stockage pris en charge par une solution de clustering tierce. Pour un exemple spécifique utilisant SIOS DataKeeper, consultez la section [Haute disponibilité pour un partage de fichiers à l’aide du clustering de basculement et du logiciel tiers SIOS Datakeeper](https://azure.microsoft.com/blog/high-availability-for-a-file-share-using-wsfc-ilb-and-3rd-party-software-sios-datakeeper/).<br/><br/>3. Un cluster de basculement à deux nœuds exécuté sur des machines virtuelles Azure, avec le stockage de bloc partagé cible iSCSI distant via ExpressRoute. Par exemple, stockage privé de NetApp (NPS) expose une cible iSCSI via ExpressRoute avec Equinix tooAzure machines virtuelles.<br/><br/>Pour un stockage partagé tiers et les solutions de réplication de données, vous devez contacter le fournisseur hello des données connexes tooaccessing des problèmes lors du basculement.<br/><br/>Notez que l’utilisation des instances de cluster de basculement dans [Azure File Storage](https://azure.microsoft.com/services/storage/files/) n’est pas encore prise en charge, car cette solution n’utilise pas Premium Storage. Nous travaillons toosupport ce bientôt. |

## <a name="azure-only-disaster-recovery-solutions"></a>Azure uniquement : solutions de récupération d’urgence
Vous pouvez disposer d’une solution de récupération d’urgence pour vos bases de données SQL Server dans Azure en utilisant des groupes de disponibilité, la mise en miroir de bases de données ou la sauvegarde et la restauration à l’aide d’objets blob de stockage.

| Technology | Exemples d’architecture |
| --- | --- |
| **Groupes de disponibilité** |Réplicas de disponibilité exécutés dans plusieurs centres de données sur les machines virtuelles Azure pour la récupération d’urgence. Cette solution inter-régions empêche l’indisponibilité totale du site. <br/> ![Groupes de disponibilité](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_alwayson.png)<br/>Dans une région, tous les réplicas doivent être dans hello même service cloud et hello même réseau virtuel. Étant donné que chaque région aura un réseau virtuel distinct, ces solutions nécessitent une connectivité tooVNet de réseau virtuel. Pour plus d’informations, consultez [configurer un réseau pour une connexion à l’aide de hello Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md). Pour obtenir des instructions détaillées, consultez la section [Configurer un groupe de disponibilité SQL Server sur des machines virtuelles Azure dans différentes régions](virtual-machines-windows-portal-sql-availability-group-dr.md).|
| **Mise en miroir de bases de données** |Serveurs principal et miroir s’exécutant dans des centres de données différents pour la récupération d’urgence. Vous devez déployer à l’aide de certificats de serveur, car un domaine Active Directory ne peut pas couvrir plusieurs centres de données.<br/>![Mise en miroir de bases de données](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_dbmirroring.gif) |
| **Sauvegarde et restauration avec le service de stockage d’objets blob Azure** |Bases de données de production sauvegardées directement tooblob stockage dans un autre centre de données pour la récupération d’urgence.<br/>![Sauvegarde et restauration](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_backup_restore.gif)<br/>Pour plus d’informations, voir [Sauvegarde et restauration de SQL Server dans les machines virtuelles Azure](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="hybrid-it-disaster-recovery-solutions"></a>Informatique hybride : solutions de récupération d’urgence
Vous pouvez disposer d’une solution de récupération d’urgence pour vos bases de données SQL Server dans un environnement informatique hybride, en utilisant des groupes de disponibilité, la mise en miroir de bases de données, la copie des journaux de transaction, ainsi que la sauvegarde et la restauration avec le stockage d’objets blob Azure.

| Technology | Exemples d’architecture |
| --- | --- |
| **Groupes de disponibilité** |Certains réplicas de disponibilité s’exécutant dans les machines virtuelles Azure et d’autres réplicas s’exécutant sur site pour la récupération d’urgence entre sites. Hello site de production peut être soit local ou dans un centre de données Azure.<br/>![Groupes de disponibilité](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_alwayson.gif)<br/>Étant donné que tous les réplicas de disponibilité doivent être dans hello même cluster de basculement, hello cluster doit couvrir les deux réseaux (un cluster de basculement de sous-réseaux multiples). Cette configuration nécessite une connexion VPN entre Azure et hello sur réseau local.<br/><br/>Pour la récupération d’urgence réussie de vos bases de données, vous devez également installer un contrôleur de domaine répliqué sur le site de récupération d’urgence hello.<br/><br/>Il est possible de toouse hello Assistant Ajouter un réplica dans SSMS tooadd un tooan un réplica Windows Azure toujours sur le groupe de disponibilité existant. Pour plus d’informations, consultez Didacticiel : étendre votre tooAzure de groupe de disponibilité AlwaysOn. |
| **Mise en miroir de bases de données** |Un serveur partenaire exécuté dans une machine virtuelle Azure et de hello autres exécutés sur site pour la récupération d’urgence entre site à l’aide de certificats de serveur. Les partenaires n’est pas nécessaire de toobe dans hello du même domaine Active Directory, et aucune connexion VPN n’est nécessaire.<br/>![Mise en miroir de bases de données](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_dbmirroring.gif)<br/>Un autre scénario de mise en miroir de base de données implique un serveur partenaire exécuté dans une machine virtuelle Azure et hello autres en cours d’exécution en local dans hello même domaine Active Directory pour la récupération d’urgence entre site. A [connexion VPN entre le réseau de hello Azure virtual network et hello locaux](../../../vpn-gateway/vpn-gateway-site-to-site-create.md) est requis.<br/><br/>Pour la récupération d’urgence réussie de vos bases de données, vous devez également installer un contrôleur de domaine répliqué sur le site de récupération d’urgence hello. |
| **Copie des journaux de transaction** |Un serveur en cours d’exécution dans une machine virtuelle Azure et de hello autres exécutés sur site pour la récupération d’urgence entre site. Envoi de journaux dépend le partage de fichiers Windows, une connexion VPN entre le réseau virtuel Azure de hello et hello sur site réseau est requis.<br/>![Copie des journaux de transaction](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_log_shipping.gif)<br/>Pour la récupération d’urgence réussie de vos bases de données, vous devez également installer un contrôleur de domaine répliqué sur le site de récupération d’urgence hello. |
| **Sauvegarde et restauration avec le service de stockage d’objets blob Azure** |Bases de données de production sauvegardées directement tooAzure stockage d’objets blob pour la récupération d’urgence sur site.<br/>![Sauvegarde et restauration](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_backup_restore.gif)<br/>Pour plus d’informations, voir [Sauvegarde et restauration de SQL Server dans les machines virtuelles Azure](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="important-considerations-for-sql-server-hadr-in-azure"></a>Considérations importantes pour HADR SQL Server dans Azure
Les machines virtuelles Azure, le stockage et le réseau ont des caractéristiques opérationnelles différentes par rapport à celles d’une infrastructure informatique non virtualisée sur site. Une implémentation réussie d’une solution HADR SQL Server dans Azure nécessite que vous devez comprendre ces différences et concevez votre solution tooaccommodate les.

### <a name="high-availability-nodes-in-an-availability-set"></a>Nœuds haute disponibilité d’un groupe à haute disponibilité
Haute disponibilité dans Azure permettre de nœuds de haute disponibilité hello tooplace par des domaines d’erreur (groupes) et des domaines de mise à jour (domaines d’erreur) distinctes. Pour les machines virtuelles Azure toobe placé dans hello même groupe à haute disponibilité, vous devez les déployer dans hello même service cloud. Seuls les nœuds Bonjour même service cloud peut participer hello même groupe à haute disponibilité. Pour plus d’informations, consultez [gérer hello disponibilité des Machines virtuelles](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="failover-cluster-behavior-in-azure-networking"></a>Comportement d’un cluster de basculement sur le réseau Azure
du service DHCP non compatible RFC Hello dans Azure peut entraîner la création de hello de certain toofail de configurations de cluster de basculement, en raison de nom réseau du cluster toohello assignée une adresse IP dupliquée, par exemple hello d’adresses IP même en tant qu’un des nœuds de cluster hello. Il s’agit d’un problème lorsque vous implémentez des groupes de disponibilité, qui varie selon la fonctionnalité de cluster de basculement Windows hello.

Envisagez le scénario de hello lorsqu’un cluster à deux nœuds est créé et mis en ligne :

1. Hello cluster est en ligne, puis NODE1 demande une adresse IP affectée dynamiquement pour le nom réseau du cluster hello.
2. Aucune adresse IP autre que l’adresse de NODE1 propres IP n’est fournie par hello service DHCP, étant donné que hello service DHCP reconnaît cette demande hello provient de NODE1 lui-même.
3. Windows détecte qu’une adresse en double est affectée à la fois tooNODE1 et toohello nom du réseau de cluster de basculement et groupe de clusters par défaut hello échoue toocome en ligne.
4. groupe de clusters par défaut Hello déplace tooNODE2, qui traite l’IP adresse NODE1 comme adresse IP de cluster hello et met en ligne le groupe de cluster par défaut hello.
5. Lorsque NODE2 tente de connexion tooestablish avec NODE1, les paquets dirigés vers NODE1 ne quittent jamais NODE2 car il est résolu tooitself d’adresse IP de NODE1. Impossible d’établir une connexion avec NODE1 Node2, puis perd le quorum et arrête hello cluster.
6. Bonjour pendant ce temps, NODE1 peut envoyer des paquets tooNODE2, mais NODE2 ne peut pas répondre. Node1 perd le quorum et arrête hello cluster.

Ce scénario peut être évité en affectant une adresse IP statique inutilisée, par exemple une adresse IP de lien local comme 169.254.1.1, le nom réseau du cluster toohello dans l’ordre toobring hello nom réseau du cluster en ligne. toosimplify ce processus, consultez [le cluster de basculement de Windows de configuration dans Azure pour les groupes de disponibilité](http://social.technet.microsoft.com/wiki/contents/articles/14776.configuring-windows-failover-cluster-in-windows-azure-for-alwayson-availability-groups.aspx).

Pour plus d’informations, consultez la section [Configurer des groupes de disponibilité dans Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md).

### <a name="availability-group-listener-support"></a>Prise en charge de l’écouteur du groupe de disponibilité
Les écouteurs de groupe de disponibilité sont pris en charge sur les machines virtuelles Azure exécutant Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 et Windows Server 2016. Cette prise en charge est rendue possible à l’aide de hello de points de terminaison avec équilibrage de charge, activée sur des machines virtuelles Azure hello qui sont des nœuds de groupe de disponibilité. Vous devez suivre les étapes de configuration spéciales pour toowork des écouteurs hello pour les applications clientes qui s’exécutent dans Azure, ainsi que celles qui s’exécutent localement.

Il existe deux options principales de configuration de votre écouteur : externe (public) ou interne. Hello externes (publics) récepteur utilise une connecté à internet, l’équilibrage de charge et est associé à un public IP virtuelle (VIP) qui est accessible via hello internet. Un écouteur interne utilise un équilibrage de charge interne et prend en charge uniquement des clients dans hello même réseau virtuel. Quel que soit le type d’équilibrage de charge, vous devez activer le retour direct du serveur. 

Si hello groupe de disponibilité s’étend sur plusieurs sous-réseaux Azure (par exemple, un déploiement qui traverse les régions Azure), la chaîne de connexion du client hello doit inclure «**MultisubnetFailover = True**». Cela entraîne des réplicas de toohello de tentatives de connexion parallèle dans des sous-réseaux différents hello. Pour obtenir des instructions sur la configuration d'un port d'écoute, consultez

* [Configurer un écouteur ILB pour des groupes de disponibilité dans Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md).
* [Configurer un écouteur externe pour des groupes de disponibilité dans Azure](../classic/ps-sql-ext-listener.md).

Vous pouvez toujours vous connecter réplica de disponibilité tooeach séparément en vous connectant directement toohello l’instance de service. En outre, étant donné que les groupes de disponibilité sont à compatibilité descendante avec les clients de mise en miroir de base de données, vous pouvez vous connecter toohello les réplicas de disponibilité comme partenaires de mise en miroir tant que hello réplicas sont configurés de la base de données de mise en miroir toodatabase similaire :

* Un réplica principal et un réplica secondaire
* Hello réplica secondaire est configuré comme non lisible (**secondaire accessible en lecture** option définie trop**non**)

Un exemple de chaîne de connexion client qui correspond la configuration de type de mise en miroir de base de données toothis à l’aide d’ADO.NET ou SQL Server Native Client est ci-dessous :

    Data Source=ReplicaServer1;Failover Partner=ReplicaServer2;Initial Catalog=AvailabilityDatabase;

Pour plus d’informations sur la connectivité client, consultez :

* [Utilisation de mots clés de chaîne de connexion avec SQL Server Native Client](https://msdn.microsoft.com/library/ms130822.aspx)
* [Connecter des Clients tooa Session de mise en miroir de base de données (SQL Server)](https://technet.microsoft.com/library/ms175484.aspx)
* [Connexion tooAvailability écouteur de groupe dans l’informatique hybride](http://blogs.msdn.com/b/sqlalwayson/archive/2013/02/14/connecting-to-availability-group-listener-in-hybrid-it.aspx)
* [Écouteurs de groupe de disponibilité, connectivité client et basculement d’application (SQL Server)](https://technet.microsoft.com/library/hh213417.aspx)
* [Utilisation de chaînes de connexion de mise en miroir de bases de données avec des groupes de disponibilité](https://technet.microsoft.com/library/hh213417.aspx)

### <a name="network-latency-in-hybrid-it"></a>Latence du réseau dans un environnement hybride
Vous devez déployer votre solution HADR principe hello qu’il peut y avoir des périodes de latence réseau élevée entre votre réseau local et de Azure. Lorsque vous déployez des réplicas tooAzure, vous devez utiliser la validation asynchrone au lieu de validation synchrone pour le mode de synchronisation hello. Lorsque le déploiement de serveurs de mise en miroir de base de données à la fois localement et dans Azure, utilisez le mode hautes performances hello plutôt qu’en mode haute sécurité de hello.

### <a name="geo-replication-support"></a>Prise en charge de la géo-réplication
Géo-réplication dans les disques Azure ne prend pas en charge le fichier de données hello et fichier journal de hello même toobe de base de données stockée sur des disques distincts. GRS réplique les modifications sur chaque disque indépendamment et de manière asynchrone. Ce mécanisme garantit l’ordre d’écriture hello dans un seul disque sur la copie de géo-répliquée hello, mais pas entre les copies géo-répliquées de plusieurs disques. Si vous configurez un toostore de la base de données de fichier de données et son fichier journal sur des disques distincts, hello récupérée disques après que sinistre peuvent contenir une copie plus à jour hello du fichier de données que le fichier journal de hello, qui marque une interruption hello journal à écriture anticipée dans SQL Server et hello ACID propriétés des transactions. Si vous n’avez pas hello option toodisable géo-réplication hello compte de stockage, vous devez conserver toutes les données et les fichiers journaux pour une base de données sur hello même disque. Si vous devez utiliser plusieurs disques en raison de la taille toohello hello de base de données, vous devez toodeploy une des solutions de récupération d’urgence hello répertoriée ci-dessus tooensure la redondance des données.

## <a name="next-steps"></a>Étapes suivantes
Si vous devez toocreate une machine virtuelle Azure avec SQL Server, consultez [approvisionnement d’une Machine virtuelle de SQL Server sur Azure](virtual-machines-windows-portal-sql-server-provision.md).

tooget hello meilleures performances à partir de SQL Server s’exécutant sur une machine virtuelle Azure, consultez les conseils de hello dans [performances les meilleures pratiques pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

Pour les autres rubriques connexes toorunning SQL Server dans des machines virtuelles Azure, consultez [SQL Server sur des Machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

### <a name="other-resources"></a>Autres ressources
* [Installation d’une nouvelle forêt Active Directory dans Azure](../../../active-directory/active-directory-new-forest-virtual-machine.md)
* [Créer un cluster de basculement pour les groupes de disponibilité dans une machine virtuelle Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)

