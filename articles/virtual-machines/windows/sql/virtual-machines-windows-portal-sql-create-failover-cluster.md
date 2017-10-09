---
title: aaaSQL ICF Server - Machines virtuelles Azure | Documents Microsoft
description: "Cet article explique comment toocreate sur des Machines virtuelles Azure de l’Instance Cluster de basculement SQL Server."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>Configurer une instance de cluster de basculement SQL Server sur des machines virtuelles Azure

Cet article explique comment toocreate un basculement SQL Server Cluster Instance (ICF) sur les machines virtuelles dans le modèle de gestionnaire de ressources. Cette solution utilise [Windows Server 2016 Datacenter edition espaces de stockage Direct \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) comme un logiciel réseau SAN virtuel qui synchronise le stockage hello (disques de données) entre les nœuds hello (machines virtuelles Azure) dans un Cluster Windows. La technologie Espaces de stockage direct (S2D) est une nouveauté dans Windows Server 2016.

Hello diagramme suivant montre les solution complète hello sur des machines virtuelles :

![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

Hello précédant le diagramme montre :

- Deux machines virtuelles Azure dans un cluster de basculement Windows. Lorsqu’une machine virtuelle se trouve dans un cluster de basculement, elle est également désignée comme *nœud* ou *nœuds* de cluster.
- Chaque machine virtuelle possède au moins deux disques de données.
- S2D synchronise les données de hello sur disque de données hello et présente le stockage hello synchronisé en tant qu’un pool de stockage.
- pool de stockage Hello présente un cluster de basculement de cluster (CSV) de volume partagé toohello.
- rôle de cluster SQL Server FCI Hello utilise hello CSV hello lecteurs de données.
- Une charge Azure équilibrage toohold hello adresse IP pour hello ICF de SQL Server.
- Haute disponibilité Azure conserve toutes les ressources hello.

   >[!NOTE]
   >Toutes les ressources Azure sont dans le diagramme de hello sont Bonjour même groupe de ressources.

Pour plus d’informations sur la technologie S2D, consultez [l’édition Espaces de stockage direct \(S2D\) de Windows Server 2016 Datacenter](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

La technologie S2D prend en charge deux types d’architectures : convergée et hyper-convergée. architecture de Hello dans ce document est Hyper-convergée. Un stockage de hello emplacements Hyper-convergée l’infrastructure sur hello serveurs mêmes application hello cluster hôte. Dans cette architecture, le stockage de hello est sur chaque nœud de l’instance de cluster de SQL Server.

### <a name="example-azure-template"></a>Exemple de modèle Azure

Vous pouvez créer l’ensemble de la solution hello dans Azure à partir d’un modèle. Un exemple d’un modèle est disponible dans hello GitHub [modèles de démarrage rapide Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad). Cet exemple n’est pas conçu ni testé pour une charge de travail spécifique. Vous pouvez exécuter hello modèle toocreate une instance de cluster SQL Server avec le domaine S2D tooyour connecté. Vous pouvez évaluer le modèle de hello et modifier en fonction de vos besoins.

## <a name="before-you-begin"></a>Avant de commencer

Il existe plusieurs choses tooknow et remplit les fonctions dont vous avez besoin en place avant de continuer.

### <a name="what-tooknow"></a>Quel tooknow
Vous devez avoir une compréhension opérationnelle de hello suivant technologies :

- [Technologies de cluster Windows](http://technet.microsoft.com/library/hh831579.aspx)
-  [Instances de cluster de basculement SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).

En outre, doit avoir une compréhension générale de hello suivant technologies :

- [Solution hyper-convergée utilisant les Espaces de stockage direct dans Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [Groupes de ressources Azure](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a>Quel toohave

Avant de suivre les instructions de hello dans cet article, vous devez déjà avoir :

- Un abonnement Microsoft Azure.
- Un domaine Windows sur des machines virtuelles Azure.
- Un compte avec des objets d’autorisation toocreate hello machine virtuelle Azure.
- Un réseau virtuel Azure et un sous-réseau avec un espace d’adressage IP pour hello suivant des composants :
   - Les deux machines virtuelles.
   - adresse IP de cluster Hello basculement.
   - Une adresse IP pour chaque instance de cluster de basculement.
- DNS configuré sur le réseau Azure, pointant vers les contrôleurs de domaine toohello de hello.

Une fois ces conditions préalables en place, vous pouvez passer à la création de votre cluster de basculement. première étape de Hello est toocreate hello virtual machines.

## <a name="step-1-create-virtual-machines"></a>Étape 1 : Créer les machines virtuelles

1. Connectez-vous à toohello [portail Azure](http://portal.azure.com) avec votre abonnement.

1. [Créez un groupe à haute disponibilité Azure](../tutorial-availability-sets.md).

   disponibilité de Hello définis regroupe des machines virtuelles entre les domaines d’erreur et domaines de mise à jour. Bonjour à haute disponibilité permet de s’assurer que votre application n’est pas affectée par des points uniques de panne, comme le commutateur de réseau hello ou unité d’alimentation de hello d’un rack de serveurs.

   Si vous n'avez pas créé le groupe de ressources hello pour vos machines virtuelles, le faire lorsque vous créez un groupe à haute disponibilité Azure. Si vous utilisez un ensemble de disponibilité hello hello toocreate portail Azure, procédez comme hello comme suit :

   - Bonjour portail Azure, cliquez sur  **+**  tooopen hello Azure Marketplace. Recherchez **Groupe à haute disponibilité**.
   - Cliquez sur **Groupe à haute disponibilité**.
   - Cliquez sur **Créer**.
   - Sur hello **créer le groupe à haute disponibilité** panneau, hello du jeu de valeurs suivantes :
      - **Nom**: un nom pour le groupe à haute disponibilité hello.
      - **Abonnement** : votre abonnement Azure.
      - **Groupe de ressources**: Si vous souhaitez toouse un groupe existant, cliquez sur **utiliser l’existante** et groupe hello select à partir de la liste déroulante de hello. Sinon choisissez **créer un nouveau** et tapez un nom pour le groupe de hello.
      - **Emplacement**: définir l’emplacement de hello où vous prévoyez de toocreate vos machines virtuelles.
      - **Domaines d’erreur**: hello par défaut (3).
      - **Mettre à jour des domaines**: hello par défaut (5).
   - Cliquez sur **créer** toocreate hello à haute disponibilité.

1. Créer des machines virtuelles de hello dans hello à haute disponibilité.

   Configurez deux ordinateurs virtuels SQL Server à haute disponibilité Azure hello. Pour obtenir des instructions, consultez [configurer un ordinateur virtuel de SQL Server Bonjour Azure portal](virtual-machines-windows-portal-sql-server-provision.md).

   Placez les deux machines virtuelles :

   - Bonjour le même groupe de ressources Azure votre groupe à haute disponibilité est dans.
   - Sur le même réseau que votre contrôleur de domaine de hello.
   - Sur un sous-réseau avec un espace d’adressage IP suffisant pour les deux machines virtuelles et toutes les instances de cluster de basculement que vous pourriez utiliser sur ce cluster.
   - Dans le groupe à haute disponibilité Azure hello.   

      >[!IMPORTANT]
      >Vous ne pouvez pas définir ni modifier un groupe à haute disponibilité après la création d’une machine virtuelle.

   Choisir une image de hello Azure Marketplace. Vous pouvez utiliser un Marketplace image avec qui inclut Windows Server et SQL Server ou simplement hello Windows Server. Pour plus d’informations, consultez [Présentation de SQL Server sur les machines virtuelles Azure](../../virtual-machines-windows-sql-server-iaas-overview.md)

   les images SQL Server officiels Hello Bonjour galerie Azure incluent une instance installée de SQL Server, ainsi que le logiciel d’installation de SQL Server de hello et la clé de requis de hello.

   Choisissez l’image de droite hello selon toohow que vous souhaitez toopay de licence de SQL Server hello :

   - **Payer par le Gestionnaire de licences d’utilisation**: coût par minute de hello de ces images inclut hello licences de SQL Server :
      - **SQL Server 2016 Enterprise sur Windows Server Datacenter 2016**
      - **SQL Server 2016 Standard sur Windows Server Datacenter 2016**
      - **SQL Server 2016 Developer sur Windows Server Datacenter 2016**

   - **BYOL (apportez votre propre licence)**

      - **{BYOL} SQL Server 2016 Enterprise sur Windows Server Datacenter 2016**
      - **{BYOL} SQL Server 2016 Standard sur Windows Server Datacenter 2016**

   >[!IMPORTANT]
   >Après avoir créé la machine virtuelle de hello, supprimer l’instance de SQL Server autonome préinstallées hello. Vous allez utiliser hello préinstallées SQL Server Support toocreate hello ICF de SQL Server après avoir configuré le cluster de basculement hello et S2D.

   Ou bien, vous pouvez utiliser images Azure Marketplace avec uniquement les systèmes d’exploitation hello. Choisissez un **Windows Server 2016 Datacenter** de l’image et installer hello ICF de SQL Server après avoir configuré le cluster de basculement hello et S2D. Cette image ne contient aucun support d’installation SQL Server. Placez le support d’installation hello dans un emplacement où vous pouvez exécuter l’installation de SQL Server hello pour chaque serveur.

1. Une fois Azure crée vos machines virtuelles, connectez tooeach virtual machine à RDP.

   Lorsque vous vous connectez premier ordinateur virtuel de tooa avec RDP, ordinateur de hello vous demande si vous tooallow cette toobe PC détectable sur le réseau de hello. Cliquez sur **Oui**.

1. Si vous utilisez une des images de machine virtuelle SQL Server hello, supprimez l’instance de SQL Server hello.

   - Dans **Programmes et fonctionnalités**, cliquez avec le bouton droit sur **Microsoft SQL Server 2016 (64 bits)** et sur **Désinstaller/modifier**.
   - Cliquez sur **Supprimer**.
   - Sélectionnez l’instance par défaut de hello.
   - Supprimer toutes les fonctionnalités sous **Services Moteur de base de données**. Ne supprimez pas les **Fonctionnalités partagées**. Consultez hello illustration suivante :

      ![Supprimer des fonctionnalités](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - Cliquez sur **Suivant**, puis sur **Supprimer**.

1. <a name="ports"></a>Ouvrir les ports du pare-feu hello.

   Sur chaque ordinateur virtuel, ouvrez hello suivant des ports de hello le pare-feu Windows.

   | Objectif | Port TCP | Remarques
   | ------ | ------ | ------
   | SQL Server | 1433 | Port normal pour les instances par défaut de SQL Server. Si vous avez utilisé une image à partir de la galerie de hello, ce port est ouvert automatiquement.
   | Sonde d’intégrité | 59999 | Tout port TCP ouvert. Dans une étape ultérieure, configurer l’équilibrage de charge hello [sonde d’intégrité](#probe) et hello cluster toouse ce port.  

1. Ajouter la machine virtuelle de toohello stockage. Pour plus d’informations, consultez [Ajouter du stockage](../../../storage/common/storage-premium-storage.md).

   Les deux machines virtuelles ont besoin d’au moins deux disques de données.

   Attachez des disques bruts, et non des disques au format NTFS.
      >[!NOTE]
      >Si vous attachez des disques au format NTFS, vous pouvez uniquement activer la technologie S2D sans vérification d’éligibilité de disque.  

   Attacher un minimum de deux Premium stockage (disques SSD) tooeach machine virtuelle. Nous vous recommandons d’utiliser au minimum des disques P30 (1 To).

   Hôte de jeu de mise en cache trop**en lecture seule**.

   capacité de stockage Hello dans des environnements de production dépend de votre charge de travail. les valeurs Hello décrites dans cet article sont de démonstration et de test.

1. [Ajouter un domaine existant de hello machines virtuelles tooyour](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

Une fois hello virtuels sont créés et configurés, vous pouvez configurer le cluster de basculement hello.

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>Étape 2 : Configurer hello Cluster de basculement Windows avec S2D

étape suivante de Hello est un cluster de basculement tooconfigure hello avec S2D. Dans cette étape, vous ferez hello en suivant les étapes :

1. Ajouter la fonctionnalité Windows de Clustering de basculement
1. Validez le cluster de hello
1. Créer le cluster de basculement hello
1. Créer le témoin de cloud hello
1. Ajouter du stockage

### <a name="add-windows-failover-clustering-feature"></a>Ajouter la fonctionnalité Windows de Clustering de basculement

1. toobegin, connecter la première machine virtuelle de toohello avec RDP à l’aide d’un compte de domaine qui est membre du groupe Administrateurs locaux et possède des objets de toocreate autorisations dans Active Directory. Utilisez ce compte pour rest hello de configuration de hello.

1. [Ajouter le Clustering de basculement d’ordinateur virtuel tooeach fonctionnalité](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

   fonctionnalité de Clustering de basculement tooinstall à partir de l’interface utilisateur, de hello hello comme suit sur les deux ordinateurs virtuels.
   - Dans le **Gestionnaire de serveur**, cliquez sur **Gérer**, puis sur **Ajouter des rôles et fonctionnalités**.
   - Dans **Assistant Ajouter des rôles et fonctionnalités**, cliquez sur **suivant** jusqu'à ce que vous atteigniez trop**sélectionner des fonctionnalités**.
   - Dans **Sélectionner les fonctionnalités**, cliquez sur **Clustering de basculement**. Inclure toutes les fonctionnalités requises et les outils de gestion hello. Cliquez sur **Ajouter des fonctionnalités**.
   - Cliquez sur **suivant** puis cliquez sur **Terminer** fonctionnalités de hello tooinstall.

   tooinstall hello fonctionnalité Clustering avec basculement avec PowerShell, exécutez hello suivant de script à partir d’une session PowerShell d’administrateur sur l’un des ordinateurs virtuels hello.

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

Pour référence, les étapes suivantes hello suivent les instructions de hello sous l’étape 3 de [solution Hyper convergé à l’aide des espaces de stockage Direct dans Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).

### <a name="validate-hello-cluster"></a>Validez le cluster de hello

Ce guide fait référence tooinstructions sous [validez le cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).

Valider le cluster hello dans l’interface utilisateur de hello ou PowerShell.

cluster de hello toovalidate avec hello l’interface utilisateur, procédez comme hello suivant les étapes de l’une des machines virtuelles de hello.

1. Dans le **Gestionnaire de serveur**, cliquez sur **Outils**, puis cliquez sur **Gestionnaire du cluster de basculement**.
1. Dans le **Gestionnaire du cluster de basculement**, cliquez sur **Action**, puis cliquez sur **Valider la configuration...**.
1. Cliquez sur **Suivant**.
1. Sur **sélectionner des serveurs ou un Cluster**, nom du type hello de deux machines virtuelles.
1. Sous **Options de test**, choisissez **Exécuter uniquement les tests que je sélectionne**. Cliquez sur **Suivant**.
1. Sous **Sélection du test**, incluez tous les tests sauf **Stockage**. Consultez hello illustration suivante :

   ![Valider les tests](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. Cliquez sur **Suivant**.
1. Sous **Confirmation**, cliquez sur **Suivant**.

Hello **Assistant Validation d’une Configuration** séries hello des tests de validation.

cluster de hello toovalidate avec PowerShell, exécutez hello suivant de script à partir d’une session PowerShell d’administrateur sur l’un des ordinateurs virtuels hello.

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

Une fois que vous validez le cluster de hello, créez le cluster de basculement de hello.

### <a name="create-hello-failover-cluster"></a>Créer le cluster de basculement hello

Ce guide fait référence trop[créer un cluster de basculement hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).

cluster de basculement toocreate hello, vous devez :
- les noms d’ordinateurs virtuels hello deviennent Hello hello des nœuds de cluster.
- Un nom pour le cluster de basculement hello
- Une adresse IP de cluster de basculement hello. Vous pouvez utiliser une adresse IP qui n’est pas utilisée sur hello même réseau virtuel Azure et sous-réseau hello des nœuds de cluster.

Hello suivant PowerShell crée un cluster de basculement. Mettre à jour le script hello avec des noms de nœuds de hello (noms d’ordinateur virtuel hello) hello et une adresse IP disponible à partir de hello réseau virtuel Azure :

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>Créer un témoin cloud

Un témoin cloud est un nouveau type de témoin de quorum de cluster stocké dans un Azure Storage Blob. Cela supprime la nécessité de hello d’un ordinateur de virtuel distinct qui héberge un témoin de partage.

1. [Créer un témoin de cloud pour le cluster de basculement hello](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).

1. Créez un conteneur d’objets blob.

1. Enregistrer les clés d’accès hello et URL du conteneur hello.

1. Configurer le témoin de quorum de cluster hello basculement cluster. Consultez [configurer le témoin de quorum hello dans l’interface utilisateur hello]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) dans l’interface utilisateur de hello.

### <a name="add-storage"></a>Ajouter du stockage

les disques de Hello pour S2D doivent toobe vide et sans partitions ou d’autres données. suivent des disques de tooclean [hello les étapes de ce guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).

1. [Activez les Espaces de stockage direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).

   Hello suivant PowerShell permet d’espaces de stockage directs.  

   ```PowerShell
   Enable-ClusterS2D
   ```

   Dans **Gestionnaire du Cluster de basculement**, vous pouvez maintenant voir le pool de stockage hello.

1. [Créez un volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).

   Une des fonctionnalités de hello de S2D est qu’il crée automatiquement un pool de stockage lorsque vous l’activez. Vous êtes maintenant prêt toocreate un volume. applet de commande PowerShell de Hello `New-Volume` automatise le processus de création de volume hello, y compris la mise en forme, l’ajout de toohello cluster et la création d’un volume partagé de cluster (CSV). Bonjour à l’exemple suivant crée un 800 Go CSV.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   Une fois cette commande terminée, un volume de 800 Go est monté en tant que ressource du cluster. volume de Hello est à `C:\ClusterStorage\Volume1\`.

   Hello suivant schéma montre un volume partagé de cluster avec S2D :

   ![VolumePartagéCluster](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>Étape 3 : Tester le basculement du cluster de basculement

Dans le Gestionnaire de Cluster de basculement, vérifiez que vous pouvez déplacer toohello de ressource de stockage hello autre nœud de cluster. Si vous pouvez vous connecter toohello basculement de cluster avec **Gestionnaire du Cluster de basculement** et déplacer le stockage hello d’un nœud toohello autres, vous êtes prêt tooconfigure hello FCI.

## <a name="step-4-create-sql-server-fci"></a>Étape 4 : Créer l’instance de cluster de basculement SQL Server

Une fois que vous avez configuré le cluster de basculement hello et tous les composants de cluster, y compris le stockage, vous pouvez créer hello ICF de SQL Server.

1. Connectez la première machine virtuelle de toohello à RDP.

1. Dans **Gestionnaire du Cluster de basculement**, assurez-vous que toutes les ressources principales du cluster se trouvent sur le premier ordinateur virtuel de hello. Si nécessaire, déplacez l’ordinateur virtuel de toothis toutes les ressources.

1. Recherchez le support d’installation hello. Si la machine virtuelle de hello utilise l’une des images d’Azure Marketplace hello, support de hello est situé à `C:\SQLServer_<version number>_Full`. Cliquez sur **Setup**.

1. Bonjour **centre d’Installation SQL Server**, cliquez sur **Installation**.

1. Cliquez sur **Installation d’un nouveau cluster de basculement SQL Server**. Suivez les instructions de hello Bonjour de tooinstall Assistant hello ICF de SQL Server.

   répertoires de données Hello FCI doivent toobe sur le stockage en cluster. Avec S2D, il n’est pas un disque partagé, mais un volume tooa de point de montage sur chaque serveur. S2D synchronise volume hello entre les deux nœuds. volume de Hello est présentée toohello cluster comme un volume partagé de cluster. Utilisez le point de montage de volume partagé de cluster hello pour les répertoires de données hello.

   ![RépertoiresDonnées](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. Au terme de l’Assistant de hello, installe une instance de cluster SQL Server sur le premier nœud de hello.

1. Une fois que le programme d’installation installe correctement hello ICF sur le premier nœud de hello, connectez toohello second nœud à RDP.

1. Ouvrez hello **centre d’Installation SQL Server**. Cliquez sur **Installation**.

1. Cliquez sur **cluster de basculement SQL Server ajouter nœud tooa**. Suivez les instructions de hello de hello Assistant tooinstall SQL server, puis ajouter cette toohello serveur FCI.

   >[!NOTE]
   >Si vous avez utilisé une image de la galerie Azure Marketplace avec SQL Server, outils de SQL Server ont été inclus avec l’image de hello. Si vous n’utilisez pas cette image, installez les outils de SQL Server hello séparément. Consultez [Télécharger SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="step-5-create-azure-load-balancer"></a>Étape 5 : Créer un équilibrage de charge Azure

Sur les machines virtuelles Azure, les clusters utilisent un toohold d’équilibrage de charge une adresse IP qui doit toobe sur un nœud de cluster à la fois. Dans cette solution, équilibrage de charge hello conserve adresse IP hello hello ICF de SQL Server.

[Créez et configurez un équilibrage de charge Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>Créer un équilibreur de charge hello Bonjour portail Azure

équilibrage de charge toocreate hello :

1. Bonjour portail Azure, accédez à toohello groupe de ressources avec des machines virtuelles de hello.

1. Cliquez sur **+ Ajouter**. Hello de recherche Marketplace pour **équilibrage de charge**. Cliquez sur **Équilibrage de charge**.

1. Cliquez sur **Créer**.

1. Configurer l’équilibrage de charge hello avec :

   - **Nom**: un nom qui identifie l’équilibrage de charge hello.
   - **Type**: équilibrage de charge hello peut être public ou privé. Est accessible à partir d’un équilibreur de charge privé hello même réseau virtuel. La plupart des applications Azure peut utiliser un équilibrage de charge privé. Si votre application requiert un accès tooSQL Server directement via hello Internet, utilisez un équilibreur de charge public.
   - **Réseau virtuel**: hello même réseau que les machines virtuelles de hello.
   - **Sous-réseau**: hello même sous-réseau que les ordinateurs virtuels de hello.
   - **Adresse IP privée**: hello la même adresse IP que vous avez affecté toohello SQL Server FCI réseau du cluster.
   - **Abonnement** : votre abonnement Azure.
   - **Groupe de ressources**: utilisez hello même groupe de ressources que vos machines virtuelles.
   - **Emplacement**: utilisez hello même emplacement que celui de vos machines virtuelles.
   Consultez hello illustration suivante :

   ![CréerÉquilibrageCharge](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Configurer le pool principal d’équilibrage de charge hello

1. Retourner toohello groupe de ressources Azure avec des machines virtuelles de hello et localiser un équilibrage de charge hello. Vous pouvez avoir toorefresh hello vue sur hello groupe de ressources. Cliquez sur le programme d’équilibrage de charge hello.

1. Dans le panneau de programme d’équilibrage de charge hello, cliquez sur **pools principaux**.

1. Cliquez sur **+ ajouter** tooadd un pool principal.

1. Tapez un nom pour le pool principal d’hello.

1. Cliquez sur **Ajouter une machine virtuelle**.

1. Sur hello **choisir les machines virtuelles** panneau, cliquez sur **choisir un ensemble de disponibilité**.

1. Choisissez que vous avez placé virtuels hello SQL Server dans un ensemble de disponibilité de hello.

1. Sur hello **choisir les machines virtuelles** panneau, cliquez sur **choisissez hello virtuels**.

   Votre portail Azure doit ressembler à hello illustration suivante :

   ![CréerPoolPrincipalÉquilibrageCharge](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. Cliquez sur **sélectionnez** sur hello **choisir les machines virtuelles** panneau.

1. Cliquez sur **OK** deux fois.

### <a name="configure-a-load-balancer-health-probe"></a>Configurer une sonde d’intégrité d’équilibrage de charge

1. Dans le panneau de programme d’équilibrage de charge hello, cliquez sur **sondes d’intégrité**.

1. Cliquez sur **+ Ajouter**.

1. Sur hello **sonde d’intégrité ajouter** panneau, <a name="probe"> </a>définir les paramètres de sonde d’intégrité hello :

   - **Nom**: un nom pour la sonde d’intégrité hello.
   - **Protocole** : TCP.
   - **Port**: définissez tooan port TCP disponible. Ce port nécessite un port de pare-feu ouvert. Hello d’utilisation [même port](#ports) vous définissez pour la sonde d’intégrité hello au pare-feu de hello.
   - **Intervalle** : 5 secondes.
   - **Seuil de défaillance** : 2 défaillances consécutives.

1. Cliquez sur OK.

### <a name="set-load-balancing-rules"></a>Définir les règles d’équilibrage de charge

1. Dans le panneau de programme d’équilibrage de charge hello, cliquez sur **règles d’équilibrage de charge**.

1. Cliquez sur **+ Ajouter**.

1. Définir des paramètres de règles équilibrage hello charge :

   - **Nom**: un nom pour les règles d’équilibrage de charge hello.
   - **Adresse IP de Frontend**: utiliser d’adresse IP de hello pour hello ressource réseau de clusters SQL Server FCI.
   - **Port**: définie pour hello port TCP d’instance de cluster de SQL Server. port d’instance Hello par défaut est 1433.
   - **Port principal**: cette valeur utilise hello même port que hello **Port** valeur lorsque vous activez **IP flottante (retour direct du serveur)**.
   - **Pool principal**: nom du pool utilisez hello principal que vous avez configuré précédemment.
   - **Sonde d’intégrité**: sonde d’intégrité de hello utilisation que vous avez configuré précédemment.
   - **Persistance de session** : aucune.
   - **Délai d’inactivité (minutes)** : 4.
   - **Adresse IP flottante (retour serveur direct)** : activée

1. Cliquez sur **OK**.

## <a name="step-6-configure-cluster-for-probe"></a>Étape 6 : Configurer le cluster pour la sonde

Définissez le paramètre de port de sonde de cluster hello dans PowerShell.

tooset hello du paramètre de port de sonde de cluster, mettre à jour des variables dans le script suivant à partir de votre environnement de hello.

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>Étape 7 : Test du basculement FCI

Testez le basculement de hello la fonctionnalité cluster toovalidate FCI. Hello comme suit :

1. Se connecter tooone des nœuds de cluster de SQL Server FCI hello à RDP.

1. Ouvrez le **Gestionnaire du cluster de basculement**. Cliquez sur **Rôles**. Notez le nœud qui possède le rôle de SQL Server FCI hello.

1. Cliquez sur le rôle de SQL Server FCI hello.

1. Cliquez sur **Déplacer** et sur **Meilleur nœud possible**.

**Gestionnaire du Cluster de basculement** affiche hello rôle et ses ressources hors ligne. Hello ressources ensuite déplacer et en ligne sur hello autre nœud.

### <a name="test-connectivity"></a>Tester la connectivité

connectivité tootest, journal de la machine virtuelle tooanother hello même réseau virtuel. Ouvrez **SQL Server Management Studio** et nom d’instance de cluster de SQL Server toohello connect.

>[!NOTE]
>Si nécessaire, vous pouvez [télécharger SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="limitations"></a>Limites
Sur les machines virtuelles Azure, Microsoft Distributed Transaction Coordinator (DTC) n'est pas prise en charge sur les instances fci car hello port RPC n’est pas pris en charge par l’équilibrage de charge hello.

## <a name="see-also"></a>Voir aussi

[Configurer S2D avec le Bureau à distance (Azure)](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

[Solution hyper-convergée avec Espaces de stockage direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).

[Vue d’ensemble de l’espace de stockage direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[Prise en charge de SQL Server pour S2D](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
