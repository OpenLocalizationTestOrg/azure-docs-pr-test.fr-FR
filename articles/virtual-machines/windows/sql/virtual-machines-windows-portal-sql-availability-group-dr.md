---
title: "aaaSQL groupes de disponibilité de serveur - des Machines virtuelles Azure - la récupération d’urgence | Documents Microsoft"
description: "Cet article explique comment regrouper des tooconfigure une disponibilité de SQL Server sur des machines virtuelles Azure avec un réplica dans une autre région."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a>Configurer un groupe de disponibilité AlwaysOn sur des machines virtuelles Azure dans des emplacements différents

Cet article explique comment tooconfigure une disponibilité de SQL Server Always On groupe réplica sur des machines virtuelles dans un emplacement Azure distant. Utilisez la récupération d’urgence toosupport de cette configuration.

Cet article s’applique tooAzure Machines virtuelles en mode de gestionnaire de ressources.

Hello image suivante montre un déploiement classique d’un groupe de disponibilité sur des machines virtuelles :

   ![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

Dans ce déploiement, toutes les machines virtuelles sont dans une région Azure. réplicas de groupe de disponibilité Hello peuvent avoir une validation synchrone avec basculement automatique sur SQL-1 et 2 de SQL. toobuild cette architecture, consultez [modèle de groupe de disponibilité ou didacticiel](virtual-machines-windows-portal-sql-availability-group-overview.md).

Cette architecture est vulnérable toodowntime si hello région Azure devient inaccessible. tooovercome cette vulnérabilité, ajouter un réplica dans une région différente. Hello diagramme suivant montre comment la nouvelle architecture de hello ressemble :

   ![Récupération d’urgence du groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

Hello diagramme précédent illustre un nouvel ordinateur virtuel appelé SQL-3. SQL-3 se trouve dans une autre région Azure. SQL-3 est ajouté toohello Cluster de basculement Windows Server. SQL-3 peut héberger un réplica de groupe de disponibilité. Enfin, notez que hello région Azure pour SQL-3 a un nouvel équilibrage de charge Azure.

>[!NOTE]
> Haute disponibilité Azure est requise lorsque plus d’une machine virtuelle est en hello même région. Si seul un ordinateur virtuel est dans une région de hello, hello à haute disponibilité n’est pas requis. Vous ne pouvez placer une machine virtuelle dans un groupe à haute disponibilité que lors de la création. Si hello machine virtuelle est déjà dans un ensemble de disponibilité, vous pouvez ajouter un ordinateur virtuel pour un réplica supplémentaire ultérieurement.

Dans cette architecture, hello réplica dans la région de hello distant est normalement configuré avec le mode de disponibilité avec validation asynchrone et le mode de basculement manuel.

Lorsque les réplicas du groupe de disponibilité se trouvent sur des machines virtuelles Azure dans différentes régions Azure, chaque région requiert :

* Une passerelle de réseau virtuel
* Une connexion à la passerelle de réseau virtuel

Hello diagramme suivant montre comment les réseaux hello communiquent entre les centres de données.

   ![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
>Cette architecture facture les données sortantes des données répliquées entre des régions Azure. Consultez [Détails de la tarification de la bande passante](http://azure.microsoft.com/pricing/details/bandwidth/).  

## <a name="create-remote-replica"></a>Créer un réplica distant

toocreate un réplica dans un centre de données à distance, procédez comme hello comme suit :

1. [Créer un réseau virtuel dans la nouvelle région de hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

1. [Configurer une connexion au réseau à l’aide de hello Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).

   >[!NOTE]
   >Dans certains cas, vous avez peut-être connexion au réseau de toouse PowerShell toocreate hello. Par exemple, si vous utilisez des comptes Azure différents vous ne pouvez pas configurer la connexion de hello dans le portail de hello. Dans ce cas le voir, [configurer un réseau pour une connexion à l’aide de hello Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

1. [Créer un contrôleur de domaine dans la nouvelle région de hello](../../../active-directory/active-directory-new-forest-virtual-machine.md).

   Ce contrôleur de domaine fournit l’authentification si le contrôleur de domaine hello dans le site principal de hello n’est pas disponible.

1. [Créer une machine virtuelle SQL Server dans la nouvelle région de hello](virtual-machines-windows-portal-sql-server-provision.md).

1. [Créer un équilibrage de charge Azure réseau hello sur la nouvelle région de hello](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

   Cet équilibrage de charge doit :

   - Dans hello même réseau et le sous-réseau comme hello du nouvel ordinateur virtuel.
   - Avoir une adresse IP statique pour l’écouteur du groupe de disponibilité hello.
   - Inclure un pool principal constitué uniquement d’ordinateurs virtuels hello hello même région que hello d’équilibrage de charge.
   - Utilisez une adresse IP spécifique toohello de sonde de port TCP.
   - Une charge de l’équilibrage de la règle spécifique toohello SQL Server Bonjour même région.  

1. [Ajouter le Clustering de basculement des toohello fonctionnalité nouvelle de SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

1. [Joindre hello nouveau SQL Server toohello domaine](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

1. [Définissez toouse de compte de service hello nouveau SQL Server à un compte de domaine](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).

1. [Ajouter hello nouveau SQL Server toohello Cluster de basculement Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).

1. Créer une ressource d’adresse IP sur le cluster de hello.

   Vous pouvez créer la ressource adresse IP hello Gestionnaire du Cluster de basculement. Sur le rôle du groupe de disponibilité hello, cliquez **ajouter une ressource**, **plus de ressources**, puis cliquez sur **adresse IP**.

   ![Création d’une adresse IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   Configurez cette adresse IP comme suit :

   - Utiliser le réseau hello à partir du centre de données distant hello.
   - Attribuer l’adresse IP de hello à partir d’un équilibrage de charge Azure hello. 

1. Sur hello nouveau SQL Server dans le Gestionnaire de Configuration SQL Server, [activer les groupes de disponibilité AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx).

1. [Ports de pare-feu ouvert hello nouveau SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

   Vous devez tooopen les numéros de port Hello dépendent de votre environnement. Ouvrir les ports pour hello Azure et point de terminaison de mise en miroir de charger sonde d’équilibrage de contrôle d’intégrité.

1. [Ajouter un groupe de disponibilité de réplica toohello sur hello nouveau SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).

   Pour un réplica dans une région Azure distante, configurez-le pour une réplication asynchrone avec basculement manuel.  

1. Ajoutez la ressource d’adresse IP hello en tant que dépendance pour hello écouteur client access point (nom réseau) le cluster.

   Hello capture d’écran suivante montre une ressource de cluster d’adresse IP configurée correctement :

   ![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   >groupe de ressources de cluster Hello inclut les deux adresses IP. Les deux adresses IP sont des dépendances pour le point d’accès client hello écouteur. Hello d’utilisation **ou** opérateur dans la configuration de dépendance hello cluster.

1. [Définir les paramètres de cluster hello dans PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).

Exécuter le script PowerShell de hello avec le nom réseau du cluster hello, adresse IP et port de la sonde que vous avez configurés sur l’équilibrage de charge hello dans la nouvelle région de hello.

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a>Configurer la connexion à plusieurs sous-réseaux

la réplication Hello dans le centre de données distant hello fait partie du groupe de disponibilité hello, mais il est dans un sous-réseau différent. Si ce réplica devienne le réplica principal de hello, les délais de connexion d’application peuvent se produire. Ce comportement est hello identique à un groupe de disponibilité local dans un déploiement de sous-réseaux multiples. tooallow des connexions à partir d’applications clientes, mettre à jour de la connexion du client hello ou configurer la résolution de nom sur la ressource de nom de réseau de clusters hello la mise en cache.

De préférence, mettre à jour tooset de chaînes de connexion de client hello `MultiSubnetFailover=Yes`. Consultez [Connexion à MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).

Si vous ne pouvez pas modifier les chaînes de connexion hello, vous pouvez configurer la mise en cache de résolution de nom. Consultez [Connection Timeouts in Multi-subnet Availability Group (Délais d’expiration de la connexion dans le groupe de disponibilité de plusieurs sous-réseaux)](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).

## <a name="fail-over-tooremote-region"></a>Basculer la région tooremote

tootest écouteur connectivité toohello distant région, vous pouvez basculer région de hello réplica toohello à distance. Alors que le réplica de hello est asynchrone, le basculement est vulnérable toopotential une perte de données. toofail sur sans perte de données, modifiez toosynchronous de mode de disponibilité hello puis tooautomatic de mode de basculement hello. Utilisez hello comme suit :

1. Dans **l’Explorateur d’objets**, connectez-vous instance toohello de SQL Server qui héberge le réplica principal de hello.
1. Sous **Groupes de disponibilité AlwaysOn**, **Groupes de disponibilité**, cliquez avec le bouton droit sur votre groupe de disponibilité, puis cliquez sur **Propriétés**.
1. Sur hello **général** sous **réplicas de disponibilité**, jeu de réplica de secondaire hello dans toouse de site de récupération d’urgence de hello **validation synchrone** mode de disponibilité et **Automatique** le mode de basculement.
1. Si vous avez un réplica secondaire dans le même site que votre réplica principal pour la haute disponibilité, définissez ce réplica trop**validation asynchrone** et **manuel**.
1. Cliquez sur OK.
1. Dans **l’Explorateur d’objets**, cliquez sur le groupe de disponibilité hello, puis cliquez sur **afficher le tableau de bord**.
1. Tableau de bord de hello, vérifiez que hello réplica sur le site de récupération d’urgence de hello est synchronisé.
1. Dans **l’Explorateur d’objets**, cliquez sur le groupe de disponibilité hello, puis cliquez sur **basculement...** . SQL Server Management Studio s’ouvre un Assistant toofail sur SQL Server.  
1. Cliquez sur **suivant**et l’instance de SQL Server hello select dans le site de récupération d’urgence de hello. Cliquez à nouveau sur **Suivant** .
1. Connecter l’instance de SQL Server toohello dans le site de récupération d’urgence de hello et cliquez sur **suivant**.
1. Sur hello **Résumé** page, vérifiez les paramètres de hello et cliquez sur **Terminer**.

Après le test de connectivité, déplacez hello réplica principal précédent tooyour principal Datacenter et définir hello disponibilité mode retour tootheir des paramètres de fonctionnement normales. Hello tableau suivant montre les paramètres opérationnels normal hello pour architecture hello décrites dans ce document :

| Lieu | Instance de serveur | Rôle | Mode de disponibilité | Mode de basculement
| ----- | ----- | ----- | ----- | -----
| Centre de données principal | SQL-1 | Primaire | Synchrone | Automatique
| Centre de données principal | SQL-2 | Secondaire | Synchrone | Automatique
| Centre de données secondaire ou distant | SQL-3 | Secondaire | Asynchrone | Manuel


### <a name="more-information-about-planned-and-forced-manual-failover"></a>Plus d’informations sur le basculement manuel forcé et planifié

Pour plus d’informations, consultez hello rubriques suivantes :

- [Effectuer un basculement manuel planifié d'un groupe de disponibilité (SQL Server)](http://msdn.microsoft.com/library/hh231018.aspx)
- [Effectuer un basculement manuel forcé d'un groupe de disponibilité (SQL Server)](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a>Liens supplémentaires

* [Groupes de disponibilité AlwaysOn](http://msdn.microsoft.com/library/hh510230.aspx)
* [Azure Virtual Machines](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [Équilibrages de charge Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [Groupes à haute disponibilité Azure](../manage-availability.md)
