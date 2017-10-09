---
title: tooAzure des ordinateurs virtuels Hyper-V aaaReplicate | Documents Microsoft
description: "Décrit comment la réplication tooorchestrate, le basculement et récupération de local Hyper-V VM tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a>Répliquer tooAzure de machines virtuelles (sans VMM) d’Hyper-V à l’aide d’Azure Site Recovery avec hello portail Azure

> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-hyper-v-site-to-azure.md)
> * [Portail Azure Classic](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Cet article décrit comment tooreplicate local tooAzure d’ordinateurs virtuels Hyper-V, à l’aide de [Azure Site Recovery](site-recovery-overview.md) Bonjour portail Azure. Dans ce déploiement, les machines virtuelles Hyper-V ne sont pas gérées par System Center Virtual Machine Manager (VMM).

Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Si vous souhaitez tooAzure de machines toomigrate (sans restauration), pour en savoir plus [cet article](site-recovery-migrate-to-azure.md).



## <a name="deployment-steps"></a>Étapes du déploiement

Procédez hello article toocomplete déploiement comme suit :

1. [En savoir plus](site-recovery-components.md#hyper-v-to-azure) sur l’architecture hello pour ce déploiement. En outre, [découvrez](site-recovery-hyper-v-azure-architecture.md) le fonctionnement de la réplication Hyper-V dans Site Recovery.
2. Vérifiez les conditions préalables et les limitations.
3. Configurez des comptes de réseau et de stockage Azure.
4. Préparez les hôtes Hyper-V.
5. Créez un coffre Recovery Services. coffre de Hello contient les paramètres de configuration et orchestre la réplication.
6. Spécifiez les paramètres de la source. Créer un site Hyper-V qui contient les ordinateurs hôtes Hyper-V de hello et inscrire le site de hello dans le coffre hello. Installer hello fournisseur Azure Site Recovery et hello Microsoft Recovery Services agent sur les hôtes Hyper-V de hello.
7. Configurez les paramètres de la cible et de réplication.
8. Activer la réplication pour les machines virtuelles de hello.
9. Exécutez un toomake de basculement de test que tout fonctionne comme prévu.



## <a name="prerequisites"></a>Composants requis


**Prérequis** | **Détails** |
--- | --- |
**Microsoft Azure** | Découvrez la [configuration requise pour Azure](site-recovery-prereq.md#azure-requirements).
**Serveurs locaux** | [En savoir plus](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) sur la configuration requise pour les ordinateurs hôtes Hyper-V de hello localement.
**Machines virtuelles Hyper-V en local** | Machines virtuelles que vous souhaitez tooreplicate doit être en cours d’exécution un [prise en charge du système d’exploitation](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)et être conformes avec [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL Azure** | Hôtes Hyper-V doivent accéder aux URL de toothese :<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.<br/></br> Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).<br/></br> Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).



## <a name="prepare-for-deployment"></a>Préparation du déploiement

tooprepare pour le déploiement, que vous devez :

1. [configurer un réseau Azure](#set-up-an-azure-network) dans lequel les machines virtuelles Azure sont placées lorsqu’elles sont créées après un basculement.
2. [Configurer un compte de stockage Azure](#set-up-an-azure-storage-account) pour les données répliquées.
3. [Préparer les ordinateurs hôtes Hyper-V de hello](#prepare-the-hyper-v-hosts) tooensure, ils peuvent accéder aux hello requis URL.

### <a name="set-up-an-azure-network"></a>Configurer un réseau Azure

Configurez un réseau Azure Vous en aurez besoin afin que les machines virtuelles de Azure hello sont créés après basculement tooa connecté réseau.

* réseau de Hello doivent se trouver dans hello Services de récupération de la même région que hello coffre.
* Selon le modèle de ressource hello souhaitées toouse de basculement des machines virtuelles Azure, vous devez définir hello réseau Azure [mode Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), ou [en mode classique](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* Nous vous recommandons de configurer un réseau avant de commencer. Si vous ne le faites pas, vous devez toodo il durant le déploiement de la récupération de Site.
- Les comptes de stockage utilisés par la récupération de Site ne peut pas être [déplacé](../azure-resource-manager/resource-group-move-resources.md) dans hello identique, ou entre des abonnements différents,.


### <a name="set-up-an-azure-storage-account"></a>Configurer un compte de stockage Azure

- Vous avez besoin d’un compte de stockage Azure toohold répliquées tooAzure standard/premium. [Stockage premium](../storage/storage-premium-storage.md) est généralement utilisé pour les ordinateurs virtuels qui nécessitent un manière cohérente hautes performances d’e/s et à faible latence toohost e/s intensives les charges de travail.
- Si vous voulez toouse un toostore de compte premium des données répliquées, vous devez également un journaux de réplication de compte de stockage standard toostore que capture en cours devient tooon locale, les données.
- Selon le modèle de ressource hello souhaitées toouse de basculement des machines virtuelles Azure, vous devez définir un compte dans [mode Resource Manager](../storage/storage-create-storage-account.md), ou [en mode classique](../storage/storage-create-storage-account-classic-portal.md).
- Nous vous recommandons de configurer un compte de stockage avant de commencer. Si vous ne vous devez toodo il durant le déploiement de la récupération de Site. Hello doivent être dans hello Services de récupération de la même région que hello coffre.
- Vous ne pouvez pas déplacer des comptes de stockage utilisé par la récupération de Site entre les groupes de ressources de hello même abonnement, ou entre différents abonnements.


### <a name="prepare-hello-hyper-v-hosts"></a>Préparer les ordinateurs hôtes Hyper-V de hello

* Assurez-vous que les hôtes Hyper-V de hello respectent hello [conditions préalables](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).
- Assurez-vous que les hôtes de hello peuvent accéder à des URL de hello requis.


## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Nouveau** > **Surveillance + gestion** > **Sauvegarde et Site Recovery (OMS)**.  

    ![Nouveau coffre](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. Dans **nom**, spécifiez un coffre de hello tooidentify nom convivial. Si vous avez plusieurs abonnements, sélectionnez-en un.

4. [Créez un groupe de ressources](../azure-resource-manager/resource-group-template-deploy-portal.md) ou sélectionnez un groupe existant et spécifiez une région Azure. Ordinateurs doivent être répliquées toothis région. les régions toocheck pris en charge, consultez disponibilité géographique dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).

5. Si vous souhaitez tooquickly accès hello coffre à partir de hello du tableau de bord, cliquez sur **code confidentiel toodashboard**, puis cliquez sur **créer**.

    ![Nouveau coffre](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

coffre Hello s’affiche dans hello **tableau de bord** > **toutes les ressources** liste et sur hello principal **les coffres de Services de récupération** panneau.



## <a name="select-hello-protection-goal"></a>Sélectionnez l’objectif de protection de hello

Sélectionnez les éléments tooreplicate, et où vous souhaitez que tooreplicate à.

1. Bonjour **les coffres de Services de récupération**, sélectionnez le coffre hello.
2. Dans **Prise en main**, cliquez sur **Site Recovery** > **Préparer l’infrastructure** > **Objectif de protection**.

    ![Sélectionner des objectifs](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. Dans **objectif de Protection**, sélectionnez **tooAzure**, puis sélectionnez **Oui, avec Hyper-V**. Sélectionnez **non** tooconfirm vous n’utilisez pas de VMM. Cliquez ensuite sur **OK**.

    ![Sélectionner des objectifs](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

Configurer le site de hello Hyper-V, installer hello fournisseur Azure Site Recovery et hello Azure Recovery Services agent sur les ordinateurs hôtes Hyper-V et inscrire le site de hello dans le coffre hello.

1. Dans **Préparer l’infrastructure**, cliquez sur **Source**. tooadd un nouveau site Hyper-V en tant que conteneur pour vos ordinateurs hôtes Hyper-V ou des clusters, cliquez sur **+ Site Hyper-V**.

    ![Configurer la source](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. Dans **site Hyper-V créer**, spécifiez un nom pour le site de hello. Cliquez ensuite sur **OK**. À présent, sélectionnez site hello vous créé, puis cliquez sur **+ Hyper-V Server** tooadd un site toohello du serveur.

    ![Configurer la source](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. Dans **Ajouter un serveur** > **Type de serveur**, vérifiez que **Serveur Hyper-V** est affiché.

    - Assurez-vous que server hello Hyper-V que vous souhaitez tooadd est conforme à hello [conditions préalables](#on-premises-prerequisites), et est en mesure de tooaccess hello URL spécifiées.
    - Téléchargez le fichier d’installation hello fournisseur Azure Site Recovery. Vous exécutez cette hello tooinstall de fichier fournisseur et hello agent Recovery Services sur chaque ordinateur hôte Hyper-V.

    ![Configurer la source](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Installer hello fournisseur et l’agent

1. Exécutez le fichier de configuration de fournisseur hello sur chaque ordinateur hôte ajouté toohello Hyper-V site. Si vous effectuez l’installation sur un cluster Hyper-V, exécutez le programme d’installation sur chaque nœud du cluster. L’installation et l’inscription de chaque nœud de cluster Hyper-V permettent de s’assurer que les machines virtuelles sont protégées, même si elles migrent entre les nœuds.
2. Dans **Microsoft Update**, vous pouvez choisir des mises à jour, pour que celles du fournisseur soient installées conformément à votre stratégie Microsoft Update.
3. Dans **Installation**, acceptez ou modifiez l’emplacement d’installation fournisseur hello par défaut et cliquez sur **installer**.
4. Dans **paramètres du coffre**, cliquez sur **Parcourir** tooselect hello coffre fichier de clé que vous avez téléchargé. Spécifier l’abonnement Azure Site Recovery de hello, nom du coffre hello, et hello Hyper-V site toowhich hello Hyper-V serveur appartient.

    ![Enregistrement du serveur](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. Dans **paramètres Proxy**, spécifiez comment hello fournisseur en cours d’exécution sur les ordinateurs hôtes Hyper-V connecte tooAzure Site Recovery via hello internet.

    * Si vous souhaitez sélectionner directement que hello fournisseur tooconnect **vous connecter directement tooAzure Site Recovery sans proxy**.
    * Si votre proxy existant nécessite une authentification, ou que vous souhaitez toouse un proxy personnalisé pour la connexion du fournisseur hello, sélectionnez **tooAzure Site Recovery à l’aide d’un serveur proxy de connexion**.
    * Si vous utilisez un proxy :
        - Spécifiez les informations d’identification, le port et adresse de hello
        - Vérifiez que hello URL décrites dans hello [conditions préalables](#prerequisites) sont autorisées via le proxy hello.

    ![Internet](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. Une fois l’installation terminée, cliquez sur **inscrire** serveur hello de tooregister dans le coffre hello.

    ![Emplacement d’installation](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. Une fois l’inscription terminée, les métadonnées à partir du serveur de hello Hyper-V sont récupérées par Azure Site Recovery et hello serveur s’affiche dans **Infrastructure Site Recovery** > **hôtes Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Configuration d’environnement cible de hello

Spécifiez le compte de stockage Azure hello pour la réplication et hello réseau Azure toowhich machines virtuelles Azure se connectera après le basculement.

1. Cliquez sur **Préparer l’infrastructure** > **Cible**.
2. Sélectionnez l’abonnement de hello et groupe de ressources hello dans lequel vous souhaitez toocreate hello machines virtuelles Azure après le basculement. Choisissez le déploiement hello modèle que vous souhaitez toouse dans Azure (classique ou une ressource de gestion) pour les machines virtuelles de hello.

3. Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.

    - Si vous n’avez pas un compte de stockage, cliquez sur **+ stockage** toocreate un inline compte basé sur le Gestionnaire de ressources. Consultez les [conditions requises pour le stockage](site-recovery-prereq.md#azure-requirements).
    - Si vous n’avez pas un réseau Azure, cliquez sur **+ réseau** toocreate un inline réseau basé sur le Gestionnaire de ressources.

    ![Storage](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a>Configurer les paramètres de réplication

1. toocreate une stratégie de réplication, cliquez sur **Prepare infrastructure** > **les paramètres de réplication** > **+ créer et associer**.

    ![Réseau](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. Dans **Créer et associer une stratégie**, indiquez le nom de la stratégie.
3. Dans **fréquence de copie**, spécifiez la fréquence à laquelle vous souhaitez tooreplicate d’éventuelles données delta après la réplication initiale de hello (toutes les 30 secondes, 5 ou 15 minutes).

    > [!NOTE]
    > Une fréquence de deuxième 30 n’est pas pris en charge lors de la réplication de stockage de toopremium. limitation de Hello est déterminée par le nombre de hello d’instantanés par l’objet blob (100) pris en charge par le stockage premium. [En savoir plus](../storage/storage-premium-storage.md#snapshots-and-copy-blob).

4. Dans **rétention du point de récupération**, spécifiez combien d’heures de conservation hello est pour chaque point de récupération. Machines virtuelles peuvent être récupérée point tooany dans une fenêtre.
5. Dans **Fréquence des captures instantanées cohérentes de l’application**, spécifiez la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications (entre 1 et 12 heures).

    - Hyper-V utilise deux types de captures instantanées, un instantané standard qui fournit un instantané incrémentiel de la machine virtuelle hello et un instantané cohérent de l’application qui prend un instantané de point-à-temps hello des données d’application à l’intérieur de machine virtuelle de hello.
    - Instantanés cohérents au niveau de l’application utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello.
    - Si vous activez les instantanés cohérents au niveau de l’application, il affecte les performances de hello des applications exécutées sur des machines virtuelles sources. Assurez-vous que la valeur hello que vous définissez est inférieur au nombre de hello de points de récupération supplémentaires que vous configurez.

6. Dans **heure de début de la réplication initiale**, spécifiez quand toostart hello la réplication initiale. la réplication Hello se produit sur votre bande passante internet, vous pouvez donc tooschedule il en dehors des heures occupés. Cliquez ensuite sur **OK**.

    ![Stratégie de réplication](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

Lorsque vous créez une nouvelle stratégie, il est automatiquement associé site Hyper-V de hello. Vous pouvez associer un site Hyper-V (et hello machines virtuelles qu’il contient) à plusieurs stratégies de réplication dans **réplication** > nom de la stratégie > **associer le Site Hyper-V**.

## <a name="capacity-planning"></a>Planification de la capacité

Votre infrastructure de base est désormais configurée. Vous pouvez donc réfléchir à la planification de la capacité et déterminer si des ressources supplémentaires sont nécessaires.

Récupération de site fournit un toohelp de planification de capacité vous allouez des ressources hello pour le calcul, de mise en réseau et de stockage. Vous pouvez exécuter le Planificateur de hello en mode rapide pour les estimations basées sur un nombre moyen de machines virtuelles, les disques et stockage, ou en mode détaillé avec numéros personnalisés au niveau de la charge de travail hello. Avant de commencer, vous devez :

* collecter les informations relatives à votre environnement de réplication, notamment les machines virtuelles, le nombre de disques par machine virtuelle et le stockage par disque ;
* Estimation hello quotidienne (évolution) taux de modification des données répliquées. Vous pouvez utiliser hello [Capacity Planner pour réplica Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) toohelp ce faire.

1. Cliquez sur **télécharger** toodownload hello outil, puis exécutez-le. [Lire l’article de hello](site-recovery-capacity-planner.md) qui accompagne l’outil de hello.
2. Lorsque vous avez terminé, sélectionnez **Oui** dans **vous avez exécuté hello Capacity Planner**?

   ![Planification de la capacité](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

En savoir plus sur le [contrôle de la bande passante réseau](#network-bandwidth-considerations)



## <a name="enable-replication"></a>Activer la réplication

Avant de commencer, assurez-vous que votre compte d’utilisateur Azure a hello requis [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’un nouveau tooAzure d’ordinateur virtuel.

Activez la réplication des machines virtuelles comme suit :          

1. Cliquez sur **Répliquer l’application** > **Source**. Après avoir configuré la réplication pour hello la première fois, vous pouvez cliquer sur **+ répliquer** tooenable la réplication pour des ordinateurs supplémentaires.

    ![Activer la réplication](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. Dans **Source**, sélectionnez les sites hello Hyper-V. Cliquez ensuite sur **OK**.
3. Dans **cible**, sélectionnez l’abonnement de coffre hello et hello basculement modèle toouse dans Azure (classique ou ressource management) après le basculement.
4. Sélectionnez le compte de stockage hello souhaité toouse. Si vous n’avez pas un compte que vous souhaitez toouse, vous pouvez [créer un](#set-up-an-azure-storage-account). Cliquez ensuite sur **OK**.
5. Sélectionnez hello toowhich réseau et le sous-réseau Azure machines virtuelles Azure se connecte lorsqu’elles sont créées avec basculement.

    - tooapply hello paramètres tooall ordinateurs du réseau vous activez pour la réplication, sélectionnez **configurer maintenant pour les ordinateurs sélectionnés**.
    - Sélectionnez **configurer ultérieurement** tooselect hello réseau Azure par ordinateur.
    - Si vous n’avez pas un réseau de toouse, vous pouvez [créer un](#set-up-an-azure-network). Sélectionnez un sous-réseau, le cas échéant. Cliquez ensuite sur **OK**.

   ![Activer la réplication](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. Dans **virtuels** > **sélectionner des machines virtuelles**, cliquez sur et sélectionnez chaque ordinateur que vous souhaitez tooreplicate. Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. Dans **propriétés** > **configurer les propriétés**, sélectionnez le système d’exploitation de hello pour les machines virtuelles hello sélectionné et hello disque de système d’exploitation.
8. Vérifiez que ce nom de machine virtuelle Azure hello (nom de la cible) est conforme à [spécifications de la machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Par défaut, tous les disques hello Hello machine virtuelle sont sélectionnés pour la réplication, mais vous pouvez désactiver les disques tooexclude les.
    - Vous souhaiterez peut-être la bande passante de tooexclude disques tooreduce la réplication. Par exemple, vous pouvez tooreplicate les disques avec les données temporaires, ou les données qui a actualisé chaque fois qu’un ordinateur ou applications redémarre (comme pagefile.sys ou Microsoft SQL Server tempdb). Vous pouvez exclure les disque hello de la réplication en désélectionnant disque de hello.
    - Vous ne pouvez exclure que des disques de base. Vous ne pouvez pas exclure de disques de système d’exploitation.
    - Nous vous recommandons de ne pas exclure de disques dynamiques. Site Recovery ne peut pas déterminer si un disque dur virtuel à l’intérieur d’une machine virtuelle invitée est un disque de base ou dynamique. Si tous les disques de volume dynamique dépendants ne sont pas exclus, disque protégé hello apparaît comme un disque en panne lorsque hello machine virtuelle bascule et données hello sur ce disque ne seront pas accessibles.
        - Une fois la réplication activée, vous ne pouvez pas ajouter ni supprimer de disques pour la réplication. Si vous souhaitez tooadd ou excluez un disque, votre besoin d’une protection de toodisable pour hello machine virtuelle, puis réactivez-la.
        - Les disques que vous créez manuellement dans Azure ne sont pas restaurés automatiquement. Par exemple, si vous échouer trois disques et créez deux directement dans la machine virtuelle Azure, uniquement hello trois disques qui ont été basculés va échouer à partir tooHyper-V Azure. Vous ne pouvez inclure les disques créés manuellement dans la restauration automatique, ou dans la réplication inverse depuis tooAzure d’Hyper-V.
        - Si vous excluez un disque que nécessaire pour un toooperate de l’application, vous devez après basculement tooAzure toocreate manuellement dans Azure, ainsi que hello répliquées application peut s’exécuter. Vous pouvez également intégrer Azure automation dans un plan de récupération, disque de hello toocreate pendant le basculement de l’ordinateur de hello.

10. Cliquez sur **OK** toosave modifications. Vous pouvez opter pour une définition ultérieure des propriétés.

    ![Activer la réplication](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. Dans **les paramètres de réplication** > **configurer les paramètres de réplication**, sélectionnez hello réplication stratégie tooapply pour hello protégé des machines virtuelles. Cliquez ensuite sur **OK**. Vous pouvez modifier la stratégie de réplication hello dans **stratégies de réplication** > nom de la stratégie > **modifier les paramètres**. Les modifications que vous appliquez seront utilisées pour les nouvelles machines et les machines dont la réplication est déjà en cours.


   ![Activer la réplication](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

Vous pouvez suivre la progression de hello **activer la Protection** de la tâche dans **travaux** > **les tâches de récupération de Site**. Après avoir hello **finaliser la Protection** s’exécute la tâche machine de hello est prête pour le basculement.

### <a name="view-and-manage-vm-properties"></a>Afficher et gérer les propriétés des machines virtuelles

Nous vous conseillons de vérifier les propriétés de hello d’ordinateur de source de hello.

1. Dans **éléments protégés**, cliquez sur **répliquées des éléments**et sélectionnez hello machine.

    ![Activer la réplication](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. Dans **propriétés**, vous pouvez afficher la réplication et les informations de basculement pour hello machine virtuelle.

    ![Activer la réplication](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. Dans **de calcul et réseau** > **propriétés de calcul**, vous pouvez spécifier la taille de nom et la cible de la machine virtuelle Azure hello. Modifiez toocomply de nom hello aux exigences d’Azure si vous avez besoin. Vous pouvez également afficher et modifier les informations sur le réseau cible de hello, du sous-réseau et adresse IP qui sera assigné toohello machine virtuelle Azure. Notez hello suivantes :

   * Vous pouvez définir l’adresse IP de hello cible. Si vous ne fournissez une adresse, hello a échoué sur l’ordinateur utilise DHCP. Si vous définissez une adresse qui n’est pas disponible lors du basculement, hello basculement échouera. Hello même adresse IP peut servir pour le test de basculement si l’adresse de hello est disponible dans le réseau de basculement de test hello.
   * nombre de Hello de cartes réseau est dicté par taille hello que vous spécifiez pour la machine virtuelle de cible hello, comme suit :

     * Si le nombre de hello de cartes réseau sur l’ordinateur source de hello est inférieur ou égal toohello le nombre de cartes autorisé pour la taille de la machine cible hello, puis cible de hello aura hello même nombre de cartes en tant que source de hello.
     * Si nombre hello de cartes pour l’ordinateur virtuel de hello source dépasse nombre hello autorisé pour la taille cible hello puis la taille maximale de la cible hello est utilisé.
     * Par exemple, si un ordinateur source possède deux cartes réseau et prend en charge la taille de la machine cible hello quatre, l’ordinateur cible hello aura deux cartes. Si hello source ordinateur possède deux cartes, mais hello taille cible pris en charge uniquement en charge l’un de l’ordinateur cible hello aura qu’un seul adaptateur.     
     * Si la machine virtuelle de hello possède plusieurs cartes réseau qu’ils seront connectent tous toohello même réseau.
     * Si l’ordinateur virtuel de hello possède plusieurs cartes réseau, hello celui affiché dans la liste de hello devient hello *par défaut* carte réseau Bonjour machine virtuelle Azure.

     ![Activer la réplication](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. Dans **disques**, vous pouvez voir le système d’exploitation de hello et disques de données de hello des ordinateurs virtuels qui seront répliqués.

#### <a name="managed-disks"></a>Disques gérés

Dans **de calcul et réseau** > **propriétés de calcul**, vous pouvez définir « Utilisation des disques gérés par » trop « Oui » pour hello machine virtuelle si vous voulez tooattach disques gérés tooyour machine sur tooAzure de migration. Disques gérés par la gestion des comptes de stockage hello associées aux disques de machine virtuelle hello, ce qui simplifie la gestion de disque pour les machines virtuelles Azure IaaS. [En savoir plus sur les disques managés](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Disques gérés sont un ordinateur virtuel de toohello créé et attaché uniquement sur un tooAzure de basculement. Sur l’activation de la protection, les données à partir d’ordinateurs locaux continuent tooreplicate toostorage comptes.
   Disques gérés peuvent être créés uniquement pour les ordinateurs virtuels déployés à l’aide du modèle de déploiement du Gestionnaire de ressources hello.

  > [!NOTE]
  > La restauration à partir de l’environnement de Hyper-V Azure tooon local n’est pas prise en charge pour les ordinateurs avec des disques gérés. Définissez « Utilisation des disques gérés par » trop « Oui » uniquement si vous envisagez de toomigrate tooAzure de cet ordinateur.

   - Lorsque vous définissez « Utilisation des disques gérés par » trop « Oui », uniquement à haute disponibilité dans le groupe de ressources hello avec « Utilisation des disques gérés par » le jeu trop « Oui » est alors disponible pour sélection. Il s’agit, car les machines virtuelles avec des disques gérés ne peut faire partie de la haute disponibilité avec un jeu de propriétés de « Disques utilisez géré » trop « Oui ». Assurez-vous que vous créez des groupes à haute disponibilité avec un jeu de propriétés de « Disques utilisez géré » en fonction de vos disques toouse intention géré lors du basculement. De même, lorsque vous définissez « Utilisation des disques gérés par » trop « non », seuls groupes à haute disponibilité dans le groupe de ressources hello avec « Utilisation des disques gérés par » propriété trop « non » sont alors disponibles pour sélection. [En savoir plus sur les disques gérés et les groupes à haute disponibilité](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Si le compte de stockage hello utilisée pour la réplication a été chiffré avec un chiffrement de Service de stockage à n’importe quel point dans le temps, la création de disques gérés pendant le basculement échoue. Vous pouvez définir « Utilisation des disques gérés par » trop « non » et réessayez de basculement ou désactivez la protection pour la machine virtuelle de hello et protéger le compte de stockage tooa qui n’avait pas de chiffrement de service de stockage activé à n’importe quel point dans le temps.
  > [En savoir plus sur Storage Service Encryption et les disques gérés](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Déploiement de test hello

déploiement de hello tootest vous pouvez exécuter un test de basculement pour un seul ordinateur virtuel ou d’un plan de récupération qui contient un ou plusieurs ordinateurs virtuels.

### <a name="before-you-start"></a>Avant de commencer

 - Si vous souhaitez tooconnect tooAzure machines virtuelles à l’aide du protocole RDP après le basculement, en savoir plus sur [préparation tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test de toofully vous avez besoin de toocopy d’Active Directory et DNS dans votre environnement de test. [En savoir plus](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Exécution d’un test de basculement

1. toofail sur un seul ordinateur, dans **répliquées des éléments**, cliquez sur la machine virtuelle de hello > **+ Test de basculement** icône.
2. toofail sur la récupération d’un plan, en **les Plans de récupération**, plan de hello avec le bouton droit > **Test de basculement**. toocreate un plan de récupération, [suivez ces instructions](site-recovery-create-recovery-plans.md).
3. Dans **Test de basculement**, sélectionnez hello réseau Azure toowhich machines virtuelles Azure est connectée après le basculement se produit.
4. Cliquez sur **OK** toobegin hello basculement. Vous pouvez suivre la progression en cliquant sur hello VM tooopen ses propriétés, ou sur hello **Test de basculement** travail dans le nom du coffre > **travaux** > **les tâches de récupération de Site**.
5. Une fois hello basculement terminé, vous devez également être en mesure de réplica de hello toosee machine Azure s’affichent dans hello portail Azure > **virtuels**. Assurez-vous que VM hello est hello approprié, qui sa connexion réseau approprié de toohello, et qu’il s’exécute.
6. Si vous préparé pour les connexions après le basculement, vous devez être en mesure de tooconnect toohello machine virtuelle Azure.
7. Une fois que vous avez terminé, cliquez sur **basculement de test de nettoyage** sur le plan de récupération hello. Dans **Notes** enregistrer toutes les observations associées au test de basculement hello. Cette opération supprimera les machines virtuelles hello qui ont été créés pendant le test de basculement.

Pour plus d’informations, lisez hello [tooAzure de basculement de Test](site-recovery-test-failover-to-azure.md) l’article.



## <a name="monitor-hello-deployment"></a>Moniteur hello déploiement

Surveiller les paramètres de configuration hello, l’état et l’intégrité de votre déploiement de Site Recovery :

1. Cliquez sur Bonjour coffre nom tooaccess Bonjour **Essentials** tableau de bord. Dans ce tableau de bord, vous pouvez suivre les événements, les plans de récupération, l’état de la récupération et les travaux de Site Recovery.  

    ![Essentials](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. Bonjour **intégrité** vignette, vous pouvez surveiller les serveurs de site qui rencontrent un problème et hello les événements déclenchés par la récupération de Site Bonjour des dernières 24 heures. Vous pouvez personnaliser les vignettes de hello tooshow Essentials et des dispositions qui sont plus utiles tooyou, y compris l’état hello autres récupération de Site et les coffres de sauvegarde.
3. Vous pouvez gérer et surveiller la réplication dans hello **répliquées des éléments**, **les Plans de récupération**, et **les tâches de récupération de Site** vignettes. Vous pouvez accéder au détail des travaux dans **Travaux** > **Travaux Site Recovery**.

## <a name="command-line-provider-and-agent-installation"></a>Installation de l’agent et du fournisseur en ligne de commande

Hello fournisseur Azure Site Recovery et l’agent peuvent également être installés à l’aide de hello suivant la ligne de commande. Cette méthode peut être le fournisseur de hello tooinstall utilisé sur un serveur de base pour Windows Server 2012 R2.

1. Téléchargez hello fournisseur de fichiers et d’enregistrement clé tooa dossier d’installation. par exemple C:\ASR.
2. À partir d’une invite de commandes avec élévation de privilèges, exécutez ces programme d’installation de commandes tooextract hello fournisseur :

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Exécuter des composants de hello tooinstall de cette commande :

            C:\ASR> setupdr.exe /i
4. Ensuite, exécutez ces serveurs de hello tooregister commandes dans le coffre hello :

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
Où :

* **/ Informations d’identification**: un paramètre obligatoire qui spécifie l’emplacement de hello dans le hello se trouve le fichier de clé d’inscription  
* **/ FriendlyName**: paramètre obligatoire pour nom hello du serveur hôte hello Hyper-V qui s’affiche dans le portail Azure Site Recovery hello.
* **/ProxyAddress**: paramètre facultatif qui spécifie l’adresse hello du serveur de proxy hello.
* **/ProxyPort** : paramètre optionnel qui spécifie le port du serveur proxy de hello hello.
* **/proxyUsername**: paramètre facultatif qui spécifie le nom d’utilisateur Proxy hello (si le proxy requiert une authentification).
* **/proxyPassword**: paramètre facultatif qui spécifie hello mot de passe pour l’authentification avec le serveur de proxy hello (si le proxy requiert une authentification).


## <a name="network-bandwidth-considerations"></a>Remarques relatives à la bande passante réseau
Vous pouvez utiliser hello [outil Hyper-V capacity planner](site-recovery-capacity-planner.md) toocalculate la bande passante de hello nécessaire pour la réplication (la réplication initiale, puis delta). quantité de hello toocontrol d’utilisation de la bande passante pour la réplication, vous avez plusieurs options :

* **Limiter la bande passante**: le trafic de Hyper-V qui réplique tooAzure passe par un hôte Hyper-V spécifique. Vous pouvez limiter la bande passante sur le serveur hôte de hello.
* **Optimiser la bande passante**: vous pouvez influer sur la bande passante hello utilisée pour la réplication à l’aide de deux clés de Registre.

### <a name="throttle-bandwidth"></a>Limiter la bande passante
1. Ouvrez le composant logiciel enfichable MMC Microsoft Azure Backup hello sur le serveur hôte de Hyper-V hello. Par défaut, un raccourci pour Microsoft Azure Backup est disponible sur le bureau de hello ou dans C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Dans le composant logiciel enfichable hello, cliquez sur **modifier les propriétés**.
3. Sur hello **limitation** onglet sélectionnez **activer l’utilisation de la bande passante internet pour les opérations de sauvegarde de limitation**et définir des limites de hello pour le travail et non liés au travail heures. Les plages valides sont de Mbits/s des too102 de 512 Kbits/s par seconde.

    ![Limiter la bande passante](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

Vous pouvez également utiliser hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) de limitation tooset applet de commande. Voici un exemple :

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indique qu’aucune limitation n’est requise.

### <a name="influence-network-bandwidth"></a>Influer sur la bande passante réseau
1. Dans le Registre de hello accédez trop**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * le trafic de la bande passante de hello tooinfluence sur un disque de réplication, modifiez hello de valeur hello **UploadThreadsPerVM**, ou créez la clé de hello si elle n’existe pas.
   * la bande passante de hello tooinfluence pour le trafic de la restauration automatique d’Azure, modifier la valeur de hello **DownloadThreadsPerVM**.
2. Hello par défaut est 4. Dans un réseau « surapprovisionnée », ces clés de Registre doivent être modifiées à partir des valeurs par défaut de hello. Hello maximal est 32. Surveiller le trafic toooptimize hello valeur.

## <a name="next-steps"></a>Étapes suivantes

Après la réplication initiale est terminée et que vous avez testé le déploiement de hello, vous pouvez appeler les basculements comme hello besoin. [En savoir plus](site-recovery-failover.md) sur différents types de basculement et la manière dont toorun les.
