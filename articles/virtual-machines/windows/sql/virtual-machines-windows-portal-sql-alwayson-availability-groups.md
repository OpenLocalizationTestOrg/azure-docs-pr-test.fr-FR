---
title: "aaaSet la haute disponibilité pour les machines virtuelles du Gestionnaire de ressources Azure | Documents Microsoft"
description: "Ce didacticiel vous montre comment grouper des toocreate un groupe de disponibilité Always On avec des machines virtuelles Azure en mode Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 6f0a253d3502259a487e66fd62d92e41c379a6b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a>Configurer des groupes de disponibilité Always On dans des machines virtuelles Azure automatiquement : Resource Manager

Ce didacticiel vous montre comment toocreate une disponibilité de SQL Server de groupe qui utilise de machines virtuelles Azure Resource Manager. didacticiel de Hello utilise Azure panneaux tooconfigure un modèle. Vous pouvez passez en revue les paramètres par défaut de hello, tapez les paramètres requis et mettre à jour les panneaux hello dans le portail de hello dans ce didacticiel.

didacticiel complet de Hello crée un groupe de disponibilité de SQL Server sur Azure Virtual Machines qui incluent hello suivant d’éléments :

* un réseau virtuel avec plusieurs sous-réseaux, notamment un sous-réseau frontal et un sous-réseau principal ;
* deux contrôleurs de domaine avec un domaine Active Directory ;
* Deux ordinateurs virtuels qui exécutent SQL Server et qui sont toohello déployé principal sous-réseau et domaine Active Directory de toohello jointes
* Un cluster de basculement de trois nœuds avec le modèle de quorum nœud majoritaire hello
* un groupe de disponibilité avec deux réplicas avec validation synchrone d’une base de données de disponibilité.

Hello suivant illustration représente la solution complète de hello.

![Architecture de laboratoire de test pour les groupes de disponibilité dans Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

Toutes les ressources dans cette solution appartiennent tooa seul groupe de ressources.

Avant de commencer ce didacticiel, confirmez suivant de hello :

* Vous disposez déjà d’un compte Azure. Si vous n’en avez pas, [inscrivez-vous pour obtenir un compte d’évaluation](http://azure.microsoft.com/pricing/free-trial/).
* Vous savez déjà comment toouse hello tooprovision de l’interface graphique utilisateur, un ordinateur virtuel de SQL Server à partir de la galerie de machine virtuelle hello. Pour plus d'informations, consultez [Approvisionnement d’une machine virtuelle SQL Server dans le portail Azure](virtual-machines-windows-portal-sql-server-provision.md).
* Vous disposez déjà d’une connaissance approfondie des groupes de disponibilité. Pour plus d’informations, voir [Groupes de disponibilité AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Si l’utilisation des groupes de disponibilité avec SharePoint vous intéresse, consultez également [Configurer des groupes de disponibilité AlwaysOn SQL Server 2012 pour SharePoint 2013](http://technet.microsoft.com/library/jj715261.aspx).
>
>

Dans ce didacticiel, utilisez hello Azure portail pour :

* Choisissez hello Always On modèle à partir du portail de hello.
* Passez en revue les paramètres du modèle hello et mettre à jour de certains paramètres de configuration pour votre environnement.
* Azure moniteur tel qu’il crée un ensemble de l’environnement hello.
* Connecter le contrôleur de domaine tooa, puis tooa serveur qui exécute SQL Server.

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-hello-cluster-from-hello-gallery"></a>Cluster hello de disposition à partir de la galerie de hello
Azure fournit une image de la galerie pour l’ensemble de la solution hello. modèle de hello toolocate :

1. Se connecter toohello portail Azure en utilisant votre compte.
2. Bonjour portail Azure, cliquez sur **+ nouveau** tooopen hello **nouveau** panneau.
3. Sur hello **nouveau** panneau, recherchez **AlwaysOn**.
   ![Rechercher le modèle AlwaysOn](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)
4. Dans les résultats de recherche de hello, recherchez **Cluster de SQL Server AlwaysOn**.
   ![Modèle AlwaysOn](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)
5. Dans **Sélectionner un modèle de déploiement**, choisissez **Resource Manager**.

### <a name="basics"></a>Concepts de base
Cliquez sur **notions de base** et hello suivant les paramètres de configuration :

* **Nom d’utilisateur administrateur** est un compte d’utilisateur qui dispose des autorisations d’administrateur de domaine et est membre du rôle de serveur fixe sysadmin hello SQL Server sur les deux instances de SQL Server. Pour ce didacticiel, utilisez **DomainAdmin**.
* **Mot de passe** hello de mot de passe de compte d’administrateur de domaine de hello. Utilisez un mot de passe complexe. Confirmer le mot de passe hello.
* **Abonnement** abonnement hello que Azure facture toorun tous déployé des ressources pour le groupe de disponibilité hello. Vous pouvez spécifier un autre abonnement si votre compte en dispose de plusieurs.
* **Groupe de ressources** est le nom hello pour toowhich de groupe hello toutes les ressources Azure qui sont créés par ce modèle appartiennent. Pour ce didacticiel, utilisez **SQL-HA-RG**. Pour plus d’informations, consultez [Présentation d’Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md#resource-groups).
* **Emplacement** est hello région Azure où le didacticiel de hello crée les ressources hello. Sélectionnez une région Azure.

Bonjour capture d’écran suivante est une opération **notions de base** panneau :

![Concepts de base](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

Cliquez sur **OK**.

### <a name="domain-and-network-settings"></a>Paramètres de domaine et réseau
Ce modèle de galerie Azure crée un domaine et des contrôleurs de domaine. Il crée également un réseau et deux sous-réseaux. modèle de Hello ne peut pas créer des serveurs dans un domaine existant ou d’un réseau virtuel. étape suivante de Hello configure les paramètres de réseau et de domaine hello.

Sur hello **les paramètres réseau et de domaine** panneau, révision hello prédéfinie des valeurs pour les paramètres réseau et de domaine hello :

* **Nom de domaine racine de forêt** est le nom de domaine hello pour le domaine Active Directory de hello ce cluster des hôtes de hello. Didacticiel de hello, utilisez **contoso.com**.
* **Nom de réseau virtuel** est le nom de réseau hello pour hello réseau virtuel Azure. Didacticiel de hello, utilisez **autohaVNET**.
* **Nom de sous-réseau de contrôleur de domaine** désigne hello d’une partie du réseau virtuel de hello ce contrôleur de domaine héberge hello. Utilisez **subnet-1**. Ce sous-réseau utilise le préfixe d’adresse **10.0.0.0/24**.
* **SQL Server nom de sous-réseau** hello désigne une partie du réseau virtuel de hello témoin de partage de serveurs hello hôtes qui exécutent SQL Server et le fichier de hello. Utilisez **subnet-2**. Ce sous-réseau utilise le préfixe d’adresse **10.0.1.0/26**.

toolearn en savoir plus sur les réseaux virtuels dans Azure, consultez [vue d’ensemble du réseau virtuel](../../../virtual-network/virtual-networks-overview.md).  

Hello **les paramètres réseau et de domaine** doit ressemble hello suivant capture d’écran :

![Paramètres de domaine et réseau](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

Si nécessaire, vous pouvez modifier ces valeurs. Pour ce didacticiel, utilisez hello des valeurs prédéfinies.

Passez en revue les paramètres de hello, puis cliquez sur **OK**.

### <a name="availability-group-settings"></a>Paramètres de groupe de disponibilité
Sur **les paramètres de groupe de disponibilité**, révision hello prédéfinir des valeurs pour le groupe de disponibilité hello et hello écouteur.

* **Nom du groupe de disponibilité** est le nom de ressource en cluster hello pour le groupe de disponibilité hello. Pour ce didacticiel, utilisez **Contoso-ag**.
* **Nom d’écouteur de groupe de disponibilité** est utilisé par le cluster de hello et équilibrage de charge interne hello. Les clients qui se connectent tooSQL Server peuvent utiliser ce réplica nom tooconnect toohello appropriée de la base de données hello. Pour ce didacticiel, utilisez **Contoso-listener**.
* **Port d’écoute de groupe de disponibilité** Spécifie le port TCP de l’écouteur de SQL Server hello hello. Pour ce didacticiel, utilisez le port par défaut de hello, **1433**.

Si nécessaire, vous pouvez modifier ces valeurs. Pour ce didacticiel, utilisez hello des valeurs prédéfinies.  

![paramètres de groupe de disponibilité](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

Cliquez sur **OK**.

### <a name="virtual-machine-size-storage-settings"></a>Taille de la machine virtuelle, paramètres de stockage
Sur **taille de machine virtuelle, les paramètres de stockage**, choisissez une taille de machine virtuelle SQL Server, révision hello autres paramètres.

* **Taille de machine virtuelle SQL Server** hello une taille pour les deux ordinateurs virtuels qui exécutent SQL Server. Choisissez une taille de machine virtuelle appropriée à votre charge de travail. Si vous générez cet environnement pour le didacticiel de hello, utilisez **DS2**. Pour les charges de production, choisissez une taille de machine virtuelle qui peut prendre en charge les charges de travail hello. Dans le cas d’importants volumes de charges de travail de production, **DS4** ou plus est nécessaire. modèle de Hello génère deux machines virtuelles de cette taille et installe SQL Server sur chacun d’eux. Pour plus d’informations, consultez [Tailles des machines virtuelles](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Bonjour Azure installe SQL Server, Enterprise Edition. Hello coût dépend de l’édition de hello et taille de machine virtuelle hello. Pour plus d’informations sur les coûts actuels, consultez la [tarification des machines virtuelles](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql).
>
>

* **Taille de machine virtuelle de contrôleur de domaine** est de taille de machine virtuelle hello hello pour les contrôleurs de domaine. Pour ce didacticiel, utilisez **D2**.
* **Taille de machine virtuelle le témoin de partage de fichiers** est la taille de machine virtuelle hello pour hello témoin de partage de fichiers. Pour ce didacticiel, utilisez **A1**.
* **Compte de stockage de SQL** est le nom hello hello du compte de stockage qui contient les données de SQL Server de hello et des disques de système d’exploitation. Pour ce didacticiel, utilisez **alwaysonsql01**.
* **Compte de stockage du contrôleur de domaine** désigne hello hello du compte de stockage pour hello contrôleurs de domaine. Pour ce didacticiel, utilisez **alwaysondc01**.
* **Taille du disque de données SQL Server** to est taille hello du disque de données SQL Server hello en to. Spécifiez un nombre compris entre 1 et 4 Pour ce didacticiel, utilisez **1**.
* **Optimisation du stockage** définit les paramètres de configuration de stockage spécifique pour les ordinateurs virtuels de hello SQL Server selon le type de charge de travail hello. Toutes les machines virtuelles de SQL Server dans ce scénario utiliser un stockage premium avec le cache d’hôte disque Azure tooread seule. En outre, vous pouvez optimiser les paramètres SQL Server pour la charge de travail hello en choisissant une de ces trois paramètres :

  * **Charge de travail générale** ne définit aucun paramètre de configuration spécifique.
  * **Traitement transactionnel** définit les indicateurs de suivi 1117 et 1118.
  * **Data warehousing** définit les indicateurs de suivi 1117 et 610.

Pour ce didacticiel, utilisez le paramètre **Charge de travail générale**.

![Taille de la machine virtuelle, paramètres de stockage](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

Passez en revue les paramètres de hello, puis cliquez sur **OK**.

#### <a name="a-note-about-storage"></a>Remarque sur le stockage
D’autres optimisations dépendant de la taille de hello hello SQL Server de disques de données. Pour chaque téraoctet de disque de données, Azure ajoute un stockage Premium de 1 To supplémentaire. Lorsqu’un serveur requiert au moins 2 To, modèle de hello crée un pool de stockage sur chaque ordinateur virtuel de SQL Server. Un pool de stockage est une forme de virtualisation du stockage où plusieurs disques sont tooprovide configuré une capacité supérieure, de résilience et de performances.  modèle de Hello crée un espace de stockage sur le pool de stockage hello et présente un système d’exploitation toohello de données. modèle de Hello désigne ce disque comme disque de données hello pour SQL Server. modèle de Hello ajuste le pool de stockage hello pour SQL Server à l’aide de hello suivant les paramètres :

* Taille de répartition est hello un entrelacement de paramètre pour le disque virtuel de hello. Les charges de travail transactionnelles utilisent 64 Ko. Les charges de travail d’entreposage de données utilisent 256 Ko.
* La résilience est simple (aucune résilience).

> [!NOTE]
> Stockage Azure premium est localement redondant et conserve trois copies des données de hello dans une région unique, afin de la résilience supplémentaire au pool de stockage hello n’est pas obligatoire.
>
>

* Nombre de colonnes est égal à nombre hello des disques de pool de stockage hello.

Pour plus d’informations sur l’espace de stockage et les pools de stockage, consultez :

* [Vue d’ensemble des espaces de stockage](http://technet.microsoft.com/library/hh831739.aspx)
* [Sauvegarde et pools de stockage Windows Server](http://technet.microsoft.com/library/dn390929.aspx)

Pour plus d’informations sur les meilleures pratiques de configuration SQL Server, consultez [Meilleures pratiques relatives aux performances de SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

### <a name="sql-server-settings"></a>Paramètres de SQL Server
Sur **paramètres SQL Server**, passez en revue et modifier le préfixe du nom d’ordinateur virtuel SQL Server hello, version de SQL Server, compte de service SQL Server et un mot de passe et hello planification de maintenance de la mise à jour corrective automatique SQL.

* **Préfixe du nom de serveur SQL** est toocreate utilisé un nom pour chaque machine virtuelle de SQL Server. Pour ce didacticiel, utilisez **sqlserver**. Hello modèle noms hello machines virtuelles SQL Server *sqlserver-0* et *sqlserver-1*.
* **Version de SQL Server** est la version de hello de SQL Server. Pour ce didacticiel, utilisez **SQL Server 2014**. Vous pouvez également choisir **SQL Server 2012** ou **SQL Server 2016**.
* **Nom utilisateur de compte de service SQL Server** est le nom de compte de domaine hello pour hello service SQL Server. Pour ce didacticiel, utilisez **sqlservice**.
* **Mot de passe** hello de mot de passe pour hello compte de service SQL Server.  Utilisez un mot de passe complexe. Confirmer le mot de passe hello.
* **Planification de maintenance SQL corrective** identifie jour hello de semaine hello que Azure corrige automatiquement les serveurs SQL hello. Pour ce didacticiel, tapez **Sunday** (Dimanche).
* **Heure de début de maintenance de mise à jour corrective d’automatique SQL** est heure hello pour hello région Azure lors de la mise à jour corrective automatique commence.

> [!NOTE]
> Hello mise à jour corrective de fenêtre pour chaque ordinateur virtuel est appliqué progressivement d’une heure. Qu’un seul ordinateur virtuel est appliqué à une interruption de tooprevent de temps de services.
>
>

![Paramètres de SQL Server](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

Passez en revue les paramètres de hello, puis cliquez sur **OK**.

### <a name="summary"></a>Résumé
Sur la page de résumé hello, Azure valide les paramètres hello. Vous pouvez également télécharger le modèle de hello. Hello de révision résumé. Cliquez sur **OK**.

### <a name="buy"></a>Acheter
Ce panneau final contient les **conditions d’utilisation** et la **politique de confidentialité**. Prenez connaissance de ces informations. Lorsque vous êtes prêt pour les ordinateurs virtuels de Azure toostart toocreate hello et tous les hello autres ressources requises pour le groupe de disponibilité hello, cliquez sur **créer**.

Hello portail Azure crée le groupe de ressources hello et toutes les ressources hello.

## <a name="monitor-deployment"></a>Surveiller le déploiement
Surveiller la progression du déploiement hello de hello portail Azure. Une icône qui représente le déploiement de hello est automatiquement épinglée toohello tableau de bord de portail Azure.

![Tableau de bord Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-toosql-server"></a>Se connecter tooSQL Server
Hello nouvelles instances de SQL Server sont exécutent sur les ordinateurs virtuels qui ont des adresses IP connecté à internet. Vous pouvez à distance (RDP) directement tooeach SQL Server machine virtuelle.

tooRDP tooa SQL Server, procédez comme suit :

1. À partir de hello tableau de bord de portail Azure, vérifiez que le déploiement de hello a réussi.
2. Cliquez sur **Ressources**.
3. Bonjour **ressources** panneau, cliquez sur **sqlserver-0**, qui est le nom de l’ordinateur de l’un des ordinateurs virtuels hello qui exécute SQL Server hello.
4. Panneau hello pour **sqlserver-0**, cliquez sur **connexion**. Votre navigateur vous demande si vous souhaitez tooopen ou d’enregistrer l’objet de connexion à distance hello. Cliquez sur **Ouvrir**.
5. **Connexion Bureau à distance** peut vous avertir que hello serveur de publication de cette connexion à distance ne peut pas être identifié. Cliquez sur **Connecter**.
6. Sécurité de Windows vous invite à entrer vous tooenter votre adresse IP d’informations d’identification tooconnect toohello hello principal du contrôleur de domaine. Cliquez sur **Utiliser un autre compte**. Pour **Nom d’utilisateur**, tapez **contoso\DomainAdmin**. Vous avez configuré ce compte lorsque vous définissez le nom d’utilisateur administrateur hello dans le modèle de hello. Utilisez le mot de passe complexe hello que vous avez choisi lors de la configuration de modèle de hello.
7. **Bureau à distance** peut vous avertir que l’ordinateur distant hello ne peut pas être authentifié échéance tooproblems avec son certificat de sécurité. Il vous montre nom hello du certificat de sécurité. Si vous avez suivi le didacticiel de hello, nom de hello est **sqlserver-0.contoso.com**. Cliquez sur **Oui**.

Vous êtes maintenant connecté à la machine virtuelle RDP toohello SQL Server. Vous pouvez ouvrir SQL Server Management Studio, connecter l’instance par défaut de toohello de SQL Server et vérifiez que le groupe de disponibilité hello est configuré.
