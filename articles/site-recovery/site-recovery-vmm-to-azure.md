---
title: aaaReplicate des ordinateurs virtuels Hyper-V dans VMM nuages tooAzure | Documents Microsoft
description: "Orchestrer le basculement, la réplication, et la récupération des ordinateurs virtuels Hyper-V gérés dans System Center VMM clouds tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: 84182fe4b63862ac7643208a22f236a7515a25a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Répliquer les machines virtuelles Hyper-V dans VMM tooAzure de nuages à l’aide de la récupération de Site Bonjour portail Azure
> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-vmm-to-azure.md)
> * [Portail Azure Classic](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell Classic](site-recovery-deploy-with-powershell.md)


Cet article décrit comment tooreplicate locaux virtuels Hyper-V gérés dans System Center VMM clouds tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Si vous souhaitez tooAzure de machines toomigrate (sans restauration), pour en savoir plus [cet article](site-recovery-migrate-to-azure.md).


## <a name="deployment-steps"></a>Étapes du déploiement

Procédez hello article toocomplete déploiement comme suit :


1. [En savoir plus](site-recovery-components.md) sur l’architecture hello pour ce déploiement. En outre, [découvrez](site-recovery-hyper-v-azure-architecture.md) le fonctionnement de la réplication Hyper-V dans Site Recovery.
2. Vérifiez les conditions préalables et les limitations.
3. Configurez des comptes de réseau et de stockage Azure.
4. Préparer le serveur VMM de local hello et hôtes Hyper-V.
5. Créez un coffre Recovery Services. coffre de Hello contient les paramètres de configuration et orchestre la réplication.
6. Spécifiez les paramètres de la source. Inscrire le serveur VMM de hello dans le coffre hello. Installez hello fournisseur Azure Site Recovery sur hello VMM server installation hello Microsoft Recovery Services agent sur les ordinateurs hôtes Hyper-V.
7. Configurez les paramètres de la cible et de réplication.
8. Activer la réplication pour les machines virtuelles de hello.
9. Exécutez un toomake de basculement de test que tout fonctionne comme prévu.



## <a name="prerequisites"></a>Composants requis


**Configuration requise pour la prise en charge** | **Détails**
--- | ---
**Microsoft Azure** | Découvrez la [configuration requise pour Azure](site-recovery-prereq.md#azure-requirements).
**Serveurs locaux** | [En savoir plus](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-in-vmm-clouds-to-azure) sur la configuration requise pour le serveur VMM de local hello et hôtes Hyper-V.
**Machines virtuelles Hyper-V en local** | Machines virtuelles que vous souhaitez tooreplicate doit être en cours d’exécution un [prise en charge du système d’exploitation](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)et être conformes avec [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL Azure** | serveur VMM de Hello doit accéder aux URL de toothese :<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.<br/></br> Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).<br/></br> Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).


## <a name="prepare-for-deployment"></a>Préparation du déploiement
tooprepare pour le déploiement, vous devez :

1. [Configurer un réseau Azure](#set-up-an-azure-network) dans lequel les machines virtuelles Azure sont placées après un basculement.
2. [Configurer un compte de stockage Azure](#set-up-an-azure-storage-account) pour les données répliquées.
3. [Préparer le serveur VMM de hello](#prepare-the-vmm-server) pour le déploiement de la récupération de Site.
4. Préparez le mappage réseau. configurer des réseaux de sorte à pouvoir définir le mappage réseau lors du déploiement de Site Recovery.

### <a name="set-up-an-azure-network"></a>Configurer un réseau Azure
Vous avez besoin d’un toowhich réseau Azure VM Azure créés après que le basculement se connectera.

* réseau de Hello doivent se trouver dans hello Services de récupération de la même région que hello coffre.
* Selon le modèle de ressource hello souhaitées toouse de basculement des machines virtuelles Azure, vous devez définir hello réseau Azure [mode Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ou [en mode classique](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* Nous vous recommandons de configurer un réseau avant de commencer. Si vous ne le faites pas, vous devez toodo il durant le déploiement de la récupération de Site.
Les réseaux Azure utilisés par la récupération de Site ne peut pas être [déplacé](../azure-resource-manager/resource-group-move-resources.md) dans hello identique, ou entre des abonnements différents,.

### <a name="set-up-an-azure-storage-account"></a>Configurer un compte de stockage Azure
* Vous avez besoin d’un compte de stockage Azure toohold répliquées tooAzure standard/premium. [Stockage premium](../storage/common/storage-premium-storage.md) est utilisé pour les ordinateurs virtuels qui nécessitent un manière cohérente hautes performances d’e/s et à faible latence toohost e/s intensives les charges de travail. Si vous voulez toouse un toostore de compte premium des données répliquées, vous devez également un journaux de réplication de compte de stockage standard toostore que capture en cours devient tooon locale, les données. compte de Hello doit être Bonjour Services de récupération de la même région que hello coffre.
* Selon le modèle de ressource hello souhaitées toouse de basculement des machines virtuelles Azure, vous devez définir un compte dans [mode Resource Manager](../storage/common/storage-create-storage-account.md) ou [en mode classique](../storage/common/storage-create-storage-account.md).
* Nous vous recommandons de configurer un compte avant de commencer. Si vous ne le faites pas, vous devez toodo il durant le déploiement de la récupération de Site.
- Notez que les comptes de stockage utilisés par la récupération de Site ne peut pas être [déplacé](../azure-resource-manager/resource-group-move-resources.md) dans hello identique, ou entre des abonnements différents,.

### <a name="prepare-hello-vmm-server"></a>Préparer le serveur VMM de hello
* Assurez-vous que le serveur VMM hello est conforme à hello [conditions préalables](#prerequisites).
* Pendant le déploiement de la récupération de Site, vous pouvez spécifier que tous les clouds sur un serveur VMM doivent être disponibles dans hello portail Azure. Si vous souhaitez uniquement tooappear clouds spécifiques dans le portail de hello, vous pouvez activer ce paramètre sur le cloud hello dans la console Administrateur VMM hello.

### <a name="prepare-for-network-mapping"></a>Préparer le mappage réseau
Vous devez configurer le mappage réseau lors du déploiement de Site Recovery. Réseau effectue un mappage entre les réseaux VMM VM la source et cible de réseaux Azure, hello tooenable suivant :

* Machines qui basculent sur hello même réseau peuvent se connecter tooeach autres, même s’ils ne sont pas basculés dans hello même façon ou Bonjour même plan de récupération.
* Si une passerelle de réseau est configurée sur le réseau Azure cible de hello, les machines virtuelles peuvent se connecter tooon locaux virtuels.
* tooset le mappage réseau, voici ce que vous devez :

  * Assurez-vous que les ordinateurs virtuels sur la source de hello serveur hôte Hyper-V sont connecté tooa réseau de VMM VM. Ce réseau doit être lié tooa réseau logique associé au cloud de hello.
  * Un réseau Azure, comme décrit [ci-dessus](#set-up-an-azure-network)

## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Nouveau** > **Surveillance + gestion** > **Sauvegarde et Site Recovery (OMS)**.

    ![Nouveau coffre](./media/site-recovery-vmm-to-azure/new-vault3.png)
3. Dans **nom**, spécifiez un coffre de hello tooidentify nom convivial. Si vous avez plusieurs abonnements, sélectionnez-en un.
4. [Créez un groupe de ressources](../azure-resource-manager/resource-group-template-deploy-portal.md)ou sélectionnez-en un. Spécifiez une région Azure. Ordinateurs doivent être répliquées toothis région. les régions toocheck pris en charge consultez disponibilité géographique dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Si vous souhaitez tooquickly accès hello coffre à partir de hello du tableau de bord, cliquez sur **code confidentiel toodashboard** > **créer un archivage**.

    ![Nouveau coffre](./media/site-recovery-vmm-to-azure/new-vault.png)

coffre Hello apparaît sur hello **tableau de bord** > **toutes les ressources**et sur hello principal **les coffres de Services de récupération** panneau.


## <a name="select-hello-protection-goal"></a>Sélectionnez l’objectif de protection de hello

Sélectionnez les éléments tooreplicate, et où vous souhaitez que tooreplicate à.

1. Dans **les coffres de Services de récupération**, sélectionnez le coffre hello.
2. Dans **Prise en main**, cliquez sur **Site Recovery** > **Préparer l’infrastructure** > **Objectif de protection**.

    ![Sélectionner des objectifs](./media/site-recovery-vmm-to-azure/choose-goals.png)
3. Dans **objectif de Protection** sélectionnez **tooAzure**, puis sélectionnez **Oui, avec Hyper-V**. Sélectionnez **Oui** tooconfirm que vous utilisez des hôtes VMM toomanage Hyper-V et le site de récupération hello. Cliquez ensuite sur **OK**.

## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

Installez hello fournisseur Azure Site Recovery sur le serveur VMM de hello et inscrire le serveur de hello dans le coffre hello. Installer l’agent Azure Recovery Services de hello sur les ordinateurs hôtes Hyper-V.

1. Cliquez sur **Préparer l’infrastructure** > **Source**.

    ![Configurer la source](./media/site-recovery-vmm-to-azure/set-source1.png)

2. Dans **Prepare source**, cliquez sur **+ VMM** tooadd un serveur VMM.

    ![Configurer la source](./media/site-recovery-vmm-to-azure/set-source2.png)

3. Dans **ajouter un serveur**, vérifiez que **serveur System Center VMM** s’affiche dans **type de serveur** et le serveur VMM hello satisfont à hello [conditions préalables et les URL configuration requise](#prerequisites).
4. Téléchargez le fichier d’installation hello fournisseur Azure Site Recovery.
5. Téléchargez la clé d’inscription de hello. Vous en aurez besoin lorsque vous exécuterez le programme d’installation. clé de Hello est valide pendant cinq jours après que l’avoir généré.

    ![Configurer la source](./media/site-recovery-vmm-to-azure/set-source3.png)


## <a name="install-hello-provider-on-hello-vmm-server"></a>Installer hello fournisseur sur le serveur VMM de hello

1. Exécutez le fichier de configuration de fournisseur hello sur le serveur VMM de hello.
2. Dans **Microsoft Update**, vous pouvez choisir des mises à jour, pour que celles du fournisseur soient installées conformément à votre stratégie Microsoft Update.
3. Dans **Installation**, acceptez ou modifiez l’emplacement d’installation fournisseur hello par défaut et cliquez sur **installer**.

    ![Emplacement d’installation](./media/site-recovery-vmm-to-azure/provider2.png)
4. Lors de l’installation terminée, cliquez sur **inscrire** serveur VMM tooregister hello dans le coffre hello.
5. Bonjour **paramètres du coffre** , cliquez sur **Parcourir** fichier de clé de coffre tooselect hello. Spécifier l’abonnement Azure Site Recovery de hello et de coffre hello.

    ![Enregistrement du serveur](./media/site-recovery-vmm-to-azure/provider10.PNG)
6. Dans **connexion Internet**, spécifiez comment hello fournisseur qui s’exécute sur le serveur VMM de hello se connectera tooSite récupération sur hello internet.

   * Si vous souhaitez hello fournisseur tooconnect directement, sélectionnez **vous connecter directement tooAzure Site Recovery sans proxy**.
   * Si votre proxy existant nécessite une authentification ou si vous souhaitez toouse un proxy personnalisé, sélectionnez **tooAzure Site Recovery à l’aide d’un serveur proxy de connexion**.
   * Si vous utilisez un proxy personnalisé, spécifiez les informations d’identification, le port et adresse de hello.
   * Si vous utilisez un proxy, vous devez avoir déjà hello URL autorisées décrites dans [conditions préalables](#on-premises-prerequisites).
   * Si vous utilisez un proxy personnalisé, un compte RunAs VMM (DRAProxyAccount) est créé automatiquement à l’aide de hello spécifié les informations d’identification de proxy. Configurer le serveur de proxy hello afin que ce compte peut s’authentifier avec succès. paramètres du compte RunAs VMM Hello peuvent être modifiés dans la console VMM hello. Dans **paramètres**, développez **sécurité** > **comptes d’identification**, puis modifiez le mot de passe hello de DRAProxyAccount. Vous devez le service VMM toorestart hello afin que ce paramètre prenne effet.

     ![Internet](./media/site-recovery-vmm-to-azure/provider13.PNG)
7. Acceptez ou modifiez l’emplacement de hello d’un certificat SSL qui est généré automatiquement pour le chiffrement de données. Ce certificat est utilisé si vous activez le chiffrement des données pour un cloud protégé par Azure dans le portail Azure Site Recovery hello. Conservez ce certificat en sécurité. Lorsque vous exécutez un basculement tooAzure vous en aurez besoin toodecrypt, si le chiffrement des données est activé.

    > [!NOTE]
    > Il est recommandé de fonctionnalité de chiffrement hello toouse fournie par Azure pour chiffrer les données au repos, au lieu d’utiliser l’option de chiffrement de données hello fournie par Azure Site Recovery. fonctionnalité de chiffrement de Hello fournie par Azure peut être activée pour un stockage > compte et permet d’obtenir de meilleures performances que le chiffrement/déchiffrement de hello est géré par le stockage Azure.
    > [En savoir plus sur le chiffrement du service de stockage depuis Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
8. Dans **nom du serveur**, spécifiez un serveur VMM à hello tooidentify nom convivial dans le coffre hello. Dans une configuration de cluster, spécifiez le nom de rôle de cluster VMM hello.
9. Activer **synchroniser les métadonnées de cloud**si vous voulez que les métadonnées toosynchronize pour tous les clouds sur le serveur VMM de hello avec le coffre de hello. Cette action ne doit toohappen qu’une seule fois sur chaque serveur. Si vous ne souhaitez pas toosynchronize tous les clouds, vous pouvez laisser ce paramètre désactivé et synchroniser chaque cloud individuellement dans les propriétés du cloud hello dans la console VMM hello. Cliquez sur **inscrire** processus de hello toocomplete.

    ![Enregistrement du serveur](./media/site-recovery-vmm-to-azure/provider16.PNG)
10. L’inscription débute. Une fois l’inscription terminée, le serveur de hello s’affiche dans **Infrastructure Site Recovery** > **serveurs VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Installer l’agent Azure Recovery Services de hello sur les ordinateurs hôtes Hyper-V

1. Une fois que vous avez configuré hello fournisseur, vous devez les fichier d’installation toodownload hello pour hello Azure Recovery Services agent. Exécutez le programme d’installation sur chaque serveur Hyper-V dans hello cloud VMM.

    ![Sites Hyper-V](./media/site-recovery-vmm-to-azure/hyperv-agent1.png)
2. Sous **Vérification de la configuration requise**, cliquez sur **Suivant**. Tous les éléments manquants de la configuration requise sont automatiquement installés.

    ![Prerequisites Recovery Services Agent](./media/site-recovery-vmm-to-azure/hyperv-agent2.png)
3. Dans **les paramètres d’Installation**, acceptez ou modifiez l’emplacement d’installation Bonjour et l’emplacement de cache hello. Vous pouvez configurer le cache de hello sur un lecteur qui dispose d’au moins 5 Go de stockage disponible, mais nous vous recommandons d’un lecteur de cache avec 600 Go ou plus d’espace libre. Cliquez ensuite sur **Installer**.
4. Une fois l’installation terminée, cliquez sur **fermer** toofinish.

    ![Inscrire l’Agent MARS](./media/site-recovery-vmm-to-azure/hyperv-agent3.png)

### <a name="command-line-installation"></a>Installer à partir de la ligne de commande
Vous pouvez installer hello Microsoft Azure Recovery Services Agent à partir de la ligne de commande à l’aide de hello commande suivante :

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Configurer internet proxy accès tooSite la récupération à partir d’ordinateurs hôtes Hyper-V

Hello Recovery Services agent en cours d’exécution sur les ordinateurs hôtes Hyper-V doit tooAzure d’accès internet pour la réplication de la machine virtuelle. Si vous accédez à hello internet via un proxy, définissez-le comme suit :

1. Ouvrez le composant logiciel enfichable MMC Microsoft Azure Backup hello sur l’ordinateur hôte Hyper-V de hello. Par défaut, un raccourci pour Microsoft Azure Backup est disponible sur le bureau de hello ou dans C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Dans le composant logiciel enfichable hello, cliquez sur **modifier les propriétés**.
3. Sur hello **Configuration Proxy** onglet, spécifiez les informations du serveur proxy.

    ![Inscrire l’Agent MARS](./media/site-recovery-vmm-to-azure/mars-proxy.png)
4. Vérifiez que l’agent hello peut atteindre l’URL de hello décrites dans hello [conditions préalables](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Configuration d’environnement cible de hello
Spécifiez toobe de compte de stockage Azure hello utilisée pour la réplication et hello réseau Azure toowhich machines virtuelles Azure se connectera après le basculement.

1. Cliquez sur **Prepare infrastructure** > **cible**, sélectionnez l’abonnement de hello et hello du groupe de ressources où vous souhaitez hello toocreate machines virtuelles ayant basculé. Choisir un modèle de déploiement hello souhaitées toouse dans Azure (classique ou une ressource de gestion) pour hello machines virtuelles ayant basculé.

    ![Storage](./media/site-recovery-vmm-to-azure/enablerep3.png)

2. Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.

    ![Storage](./media/site-recovery-vmm-to-azure/compatible-storage.png)

3. Si vous n’avez pas créé un compte de stockage et que vous souhaitez toocreate un à l’aide du Gestionnaire de ressources, cliquez sur **+ compte de stockage** toodo qu’inline.  Sur hello **créer le compte de stockage** panneau spécifier un nom de compte, un type, un abonnement et un emplacement. compte de Hello doit être Bonjour même emplacement que hello de coffre Recovery Services.

   ![Storage](./media/site-recovery-vmm-to-azure/gs-createstorage.png)


   * Si vous voulez toocreate un compte de stockage à l’aide du modèle classique de hello, faire Bonjour portail Azure. [En savoir plus](../storage/common/storage-create-storage-account.md)
   * Si vous utilisez un compte de stockage premium pour les données répliquées, configurez un compte de stockage standard supplémentaire, les journaux de réplication toostore qui capturent des données de site tooon les changements en cours.
5. Si vous n’avez pas créé un réseau Azure et que vous souhaitez toocreate un à l’aide du Gestionnaire de ressources, cliquez sur **+ réseau** toodo qu’inline. Sur hello **créer un réseau virtuel** panneau spécifier un nom de réseau, plage d’adresses, les informations de sous-réseau, abonnement et l’emplacement. réseau de Hello doivent se trouver dans hello même emplacement que hello de coffre Recovery Services.

   ![Réseau](./media/site-recovery-vmm-to-azure/gs-createnetwork.png)

   Si vous voulez toocreate un réseau en utilisant le modèle classique de hello, faire Bonjour portail Azure. [En savoir plus](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

### <a name="configure-network-mapping"></a>Configurer le mappage réseau

* [Lisez](#prepare-for-network-mapping) une présentation rapide du mappage réseau.
* Vérifiez que les ordinateurs virtuels sur le serveur VMM de hello sont connectés tooa réseau d’ordinateurs virtuels et que vous avez créé au moins un réseau virtuel Azure. Plusieurs réseaux d’ordinateurs virtuels peuvent être mappés tooa réseau Azure unique.

Configurez le mappage comme suit :

1. Dans **Infrastructure Site Recovery** > **réseau mappages** > **mappage réseau**, cliquez sur hello **+ mappage réseau**  icône.

    ![Mappage réseau](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. Dans **ajouter le mappage réseau**, sélectionnez serveur VMM source à hello, et **Azure** comme cible de hello.
3. Vérifiez l’abonnement de hello et le modèle de déploiement hello après le basculement.
4. Dans **réseau Source**, sélectionnez le réseau d’ordinateurs virtuels de hello source locale que vous souhaitez toomap à partir de la liste hello associé avec le serveur VMM de hello.
5. Dans **réseau cible**, sélectionnez hello réseau Azure dans le réplica de machines virtuelles Azure se trouve lorsqu’elles sont créées. Cliquez ensuite sur **OK**.

    ![Mappage réseau](./media/site-recovery-vmm-to-azure/network-mapping2.png)

Voici le processus exécuté lorsque le mappage réseau démarre :

* Machines virtuelles existantes sur le réseau d’ordinateurs virtuels hello source sont réseau cible de toohello connecté au commencement de mappage. Réseau d’ordinateurs virtuels source nouvelles machines virtuelles connectés toohello connectés toohello mappé réseau Azure lors de la réplication a lieu.
* Si vous modifiez un mappage réseau existant, les machines virtuelles de réplication se connecter à l’aide de nouveaux paramètres de hello.
* Si le réseau cible de hello possède plusieurs sous-réseaux, et un de ces sous-réseaux a hello le même nom que le sous-réseau sur lequel virtual machine de hello source se trouve, puis hello ordinateur virtuel se connecte le sous-réseau de toothat cible après le basculement.
* S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello se connecte toohello premier sous-réseau de réseau de hello.

## <a name="configure-replication-settings"></a>Configurer les paramètres de réplication
1. toocreate une stratégie de réplication, cliquez sur **Prepare infrastructure** > **les paramètres de réplication** > **+ créer et associer**.

    ![Réseau](./media/site-recovery-vmm-to-azure/gs-replication.png)
2. Dans **Créer et associer une stratégie**, indiquez le nom de la stratégie.
3. Dans **fréquence de copie**, spécifiez la fréquence à laquelle vous souhaitez tooreplicate d’éventuelles données delta après la réplication initiale de hello (toutes les 30 secondes, 5 ou 15 minutes).

    > [!NOTE]
    >  Une fréquence de deuxième 30 n’est pas pris en charge lors de la réplication de stockage de toopremium. limitation de Hello est déterminée par le nombre de hello d’instantanés par l’objet blob (100) pris en charge par le stockage premium. [En savoir plus](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. Dans **rétention du point de récupération**, spécifiez, en heures, la durée de conservation hello sera être pour chaque point de récupération. Les ordinateurs protégés peuvent être récupérées point tooany dans une fenêtre.
5. Dans **Fréquence des captures instantanées cohérentes de l’application**, spécifiez la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications (entre 1 et 12 heures). Hyper-V utilise deux types de captures instantanées, un instantané standard qui fournit un instantané incrémentiel de la machine virtuelle hello et un instantané cohérent de l’application qui prend un instantané de point-à-temps hello des données d’application à l’intérieur de machine virtuelle de hello. Instantanés cohérents au niveau de l’application utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello. Notez que si vous activez les instantanés cohérents au niveau de l’application, il affecte les performances de hello des applications s’exécutant sur des machines virtuelles sources. Assurez-vous que la valeur hello que vous définissez est inférieur au nombre de hello de points de récupération supplémentaires que vous configurez.
6. Dans **heure de début de la réplication initiale**, indiquer quand toostart hello la réplication initiale. la réplication Hello se produit sur votre bande passante internet, vous pouvez donc tooschedule il en dehors des heures occupés.
7. Dans **chiffrer les données stockées sur Azure**, spécifiez si tooencrypt données reste dans le stockage Azure. Cliquez ensuite sur **OK**.

    ![Stratégie de réplication](./media/site-recovery-vmm-to-azure/gs-replication2.png)
8. Lorsque vous créez une nouvelle stratégie, il est automatiquement associé hello cloud VMM. Cliquez sur **OK**. Vous pouvez associer clouds VMM supplémentaires (et hello machines virtuelles dans les) cette stratégie de réplication dans **réplication** > nom de la stratégie > **associer le Cloud VMM**.

    ![Stratégie de réplication](./media/site-recovery-vmm-to-azure/policy-associate.png)

## <a name="capacity-planning"></a>Planification de la capacité

Votre infrastructure de base est désormais configurée. Vous pouvez donc réfléchir à la planification de la capacité et déterminer si des ressources supplémentaires sont nécessaires.

Récupération de site fournit un toohelp de planification de capacité vous allouez des ressources hello pour votre environnement source, de composants de Site Recovery, réseau et stockage. Vous pouvez exécuter le Planificateur de hello en mode rapide pour les estimations basées sur un nombre moyen de machines virtuelles, des disques et de stockage, ou en mode détaillé dans lequel vous entrez les chiffres au niveau de la charge de travail hello. Avant de commencer :

* collecter les informations relatives à votre environnement de réplication, notamment les machines virtuelles, le nombre de disques par machine virtuelle et le stockage par disque ;
* Taux de modification (évolution) estimation hello quotidien, vous aurez pour les données répliquées. Vous pouvez utiliser hello [Capacity planner pour réplica Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) toohelp ce faire.

1. Cliquez sur **télécharger**, toodownload hello outil, puis exécutez-le. [Lire l’article de hello](site-recovery-capacity-planner.md) qui accompagne l’outil de hello.
2. Lorsque vous avez terminé, sélectionnez **Oui** dans **vous avez exécuté hello Capacity Planner**?

   ![Planification de la capacité](./media/site-recovery-vmm-to-azure/gs-capacity-planning.png)

   En savoir plus sur le [contrôle de la bande passante réseau](#network-bandwidth-considerations)




## <a name="enable-replication"></a>Activer la réplication

Avant de commencer, assurez-vous que votre compte d’utilisateur Azure a hello requis [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’un nouveau tooAzure d’ordinateur virtuel.

À présent, activez la réplication comme suit :

1. Cliquez sur **Étape 2 : Répliquer l’application** > **Source**. Une fois que vous avez activé la réplication pour hello première fois, cliquez sur **+ répliquer** dans la réplication de tooenable hello coffre pour des ordinateurs supplémentaires.

    ![Activer la réplication](./media/site-recovery-vmm-to-azure/enable-replication1.png)
2. Bonjour **Source** panneau serveur VMM de select hello et nuage de hello dans quel hello Hyper-V se trouvent les hôtes. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/site-recovery-vmm-to-azure/enable-replication-source.png)
3. Dans **cible**hello compte de stockage que vous utilisez pour les données répliquées et sélectionnez l’abonnement hello, modèle de déploiement après le basculement.

    ![Activer la réplication](./media/site-recovery-vmm-to-azure/enable-replication-target.png)
4. Sélectionnez le compte de stockage hello souhaité toouse. Si vous souhaitez toouse un compte de stockage différentes que celles que vous avez, vous pouvez [créer un](#set-up-an-azure-storage-account). Si vous utilisez un compte de stockage premium pour les données répliquées, vous devez tooselect une journaux de réplication de stockage standard supplémentaire compte toostore qui capturent les changements en cours tooon local data.toocreate un compte de stockage à l’aide du modèle de gestionnaire de ressources hello Cliquez sur **nouvel**. Si vous voulez toocreate un compte de stockage à l’aide du modèle classique de hello, cela [Bonjour Azure portal](../storage/common/storage-create-storage-account.md). Cliquez ensuite sur **OK**.
5. Sélectionnez hello toowhich réseau et le sous-réseau Azure machines virtuelles Azure se connecte lorsqu’elles sont créées après le basculement. Sélectionnez **configurer maintenant pour les machines sélectionnées**, tooapply hello réseau paramètre tooall machines que vous sélectionnez pour la protection. Sélectionnez **configurer ultérieurement**, tooselect hello réseau Azure par ordinateur. Si vous souhaitez toouse un réseau différents de ceux, vous pouvez [créer un](#set-up-an-azure-network). un réseau à l’aide de toocreate hello modèle, cliquez sur le Gestionnaire de ressources **nouvel**. Si vous voulez toocreate un réseau en utilisant le modèle classique de hello, cela [Bonjour Azure portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Sélectionnez un sous-réseau, le cas échéant. Cliquez ensuite sur **OK**.
6. Dans **virtuels** > **sélectionner des machines virtuelles**, cliquez sur et sélectionnez chaque ordinateur que vous souhaitez tooreplicate. Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/site-recovery-vmm-to-azure/enable-replication5.png)

7. Dans **propriétés** > **configurer les propriétés**, sélectionnez le système d’exploitation de hello pour les machines virtuelles hello sélectionné et hello disque de système d’exploitation.

    - Vérifiez que ce nom de machine virtuelle Azure hello (nom de la cible) est conforme à [spécifications de la machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Par défaut, tous les disques hello Hello machine virtuelle sont sélectionnés pour la réplication, mais vous pouvez désactiver les disques tooexclude les.

        - Vous souhaiterez peut-être la bande passante de tooexclude disques tooreduce la réplication. Par exemple, vous pouvez tooreplicate les disques avec les données temporaires, ou les données qui a actualisé chaque fois qu’un ordinateur ou applications redémarre (comme pagefile.sys ou Microsoft SQL Server tempdb). Vous pouvez exclure les disque hello de la réplication en désélectionnant disque de hello.
        - Vous ne pouvez exclure que des disques de base. Vous ne pouvez pas exclure de disques de système d’exploitation.
        - Nous vous recommandons de ne pas exclure de disques dynamiques. Site Recovery ne peut pas déterminer si un disque dur virtuel à l’intérieur d’une machine virtuelle invitée est un disque de base ou dynamique. Si tous les disques de volume dynamique dépendants ne sont pas exclus, disque protégé hello apparaît comme un disque en panne lorsque hello machine virtuelle bascule et données hello sur ce disque ne seront pas accessibles.
        - Une fois la réplication activée, vous ne pouvez pas ajouter ni supprimer de disques pour la réplication. Si vous souhaitez tooadd ou excluez un disque, votre besoin d’une protection de toodisable pour hello machine virtuelle, puis réactivez-la.
        - Les disques que vous créez manuellement dans Azure ne sont pas restaurés automatiquement. Par exemple, si vous échouer trois disques et créez deux directement dans la machine virtuelle Azure, uniquement hello trois disques qui ont été basculés va échouer à partir tooHyper-V Azure. Vous ne pouvez inclure les disques créés manuellement dans la restauration automatique, ou dans la réplication inverse depuis tooAzure d’Hyper-V.
        - Si vous excluez un disque que nécessaire pour un toooperate de l’application, vous devez après basculement tooAzure toocreate manuellement dans Azure, ainsi que hello répliquées application peut s’exécuter. Vous pouvez également intégrer Azure automation dans un plan de récupération, disque de hello toocreate pendant le basculement de l’ordinateur de hello.

    Cliquez sur **OK** toosave modifications. Vous pouvez opter pour une définition ultérieure des propriétés.

    ![Activer la réplication](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

8. Dans **les paramètres de réplication** > **configurer les paramètres de réplication**, sélectionnez hello réplication stratégie tooapply pour hello protégé des machines virtuelles. Cliquez ensuite sur **OK**. Vous pouvez modifier la stratégie de réplication hello dans **stratégies de réplication** > nom de la stratégie > **modifier les paramètres**. Les modifications appliquées sont utilisées pour les nouvelles machines et celles dont la réplication est en cours.

   ![Activer la réplication](./media/site-recovery-vmm-to-azure/enable-replication7.png)

Vous pouvez suivre la progression de hello **activer la Protection** de la tâche dans **travaux** > **les tâches de récupération de Site**. Après avoir hello **finaliser la Protection** travail s’exécute, l’ordinateur de hello est prêt pour le basculement.

### <a name="view-and-manage-vm-properties"></a>Afficher et gérer les propriétés des machines virtuelles

Nous vous conseillons de vérifier les propriétés de hello d’ordinateur de source de hello. N’oubliez pas de ce nom de machine virtuelle Azure hello doit respecter les [spécifications de la machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Dans **éléments protégés**, cliquez sur **répliquées des éléments**, et sélectionnez hello machine toosee ses détails.

    ![Activer la réplication](./media/site-recovery-vmm-to-azure/vm-essentials.png)
2. Dans **propriétés**, vous pouvez afficher la réplication et les informations de basculement pour hello machine virtuelle.

    ![Activer la réplication](./media/site-recovery-vmm-to-azure/test-failover2.png)
3. Dans **de calcul et réseau** > **propriétés de calcul**, vous pouvez spécifier la taille de nom et la cible de la machine virtuelle Azure hello. Modifier toocomply de nom hello avec [conditions requises pour Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) si vous avez besoin. Vous pouvez également afficher et modifier les informations sur le réseau cible de hello, du sous-réseau et adresse IP hello affectée toohello machine virtuelle Azure.
Notez les points suivants :

   * Vous pouvez définir l’adresse IP de hello cible. Si vous ne fournissez une adresse, hello a échoué sur l’ordinateur utilise DHCP. Si vous définissez une adresse qui n’est pas disponible lors du basculement, hello basculement échouera. Hello même adresse IP peut servir pour le test de basculement si l’adresse de hello est disponible dans le réseau de basculement de test hello.
   * nombre de Hello de cartes réseau est dicté par taille hello que vous spécifiez pour la machine virtuelle de cible hello, comme suit :

     * Si le nombre de hello de cartes réseau sur l’ordinateur source de hello est inférieur ou égal toohello le nombre de cartes autorisé pour la taille de la machine cible hello, puis cible de hello aura hello même nombre de cartes en tant que source de hello.
     * Si le nombre de cartes pour l’ordinateur virtuel de source hello hello dépasse nombre de hello autorisé pour la taille cible hello, puis taille maximale de la cible hello est utilisé.
     * Par exemple, si un ordinateur source possède deux cartes réseau et prend en charge la taille de la machine cible hello quatre, l’ordinateur cible hello aura deux cartes. Si ordinateur source de hello possède deux cartes mais hello taille cible pris en charge uniquement en charge l’un, de l’ordinateur cible hello aura qu’une seule carte.     
     * Si la machine virtuelle de hello possède plusieurs cartes réseau, ils se connectent tous toohello même réseau.

     ![Activer la réplication](./media/site-recovery-vmm-to-azure/test-failover4.png)

4. Dans **disques** vous pouvez voir les disques de données et du système d’exploitation de hello sur hello virtuelle sera répliquée.

#### <a name="managed-disks"></a>Disques gérés

Dans **de calcul et réseau** > **propriétés de calcul**, vous pouvez définir « Utilisation des disques gérés par » trop « Oui » pour hello machine virtuelle si vous voulez tooattach disques gérés tooyour machine sur tooAzure de migration. Disques gérés par la gestion des comptes de stockage hello associées aux disques de machine virtuelle hello, ce qui simplifie la gestion de disque pour les machines virtuelles Azure IaaS. [En savoir plus sur les disques managés](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Disques gérés sont un ordinateur virtuel de toohello créé et attaché uniquement sur un tooAzure de basculement. Sur l’activation de la protection, les données à partir d’ordinateurs locaux continuent tooreplicate toostorage comptes.
   Disques gérés peuvent être créés uniquement pour les ordinateurs virtuels déployés à l’aide du modèle de déploiement du Gestionnaire de ressources hello.  

  > [!NOTE]
  > La restauration à partir de l’environnement de Hyper-V Azure tooon local n’est pas prise en charge pour les ordinateurs avec des disques gérés. Définissez « Utilisation des disques gérés par » trop « Oui » uniquement si vous envisagez de toomigrate cet ordinateur vers Azure.

   - Lorsque vous définissez « Utilisation des disques gérés par » trop « Oui », uniquement à haute disponibilité dans le groupe de ressources hello avec « Utilisation des disques gérés par » le jeu trop « Oui » est alors disponible pour sélection. Il s’agit, car les machines virtuelles avec des disques gérés ne peut faire partie de la haute disponibilité avec un jeu de propriétés de « Disques utilisez géré » trop « Oui ». Assurez-vous que vous créez des groupes à haute disponibilité avec un jeu de propriétés de « Disques utilisez géré » en fonction de vos disques toouse intention géré lors du basculement.  De même, lorsque vous définissez « Utilisation des disques gérés par » trop « non », seuls groupes à haute disponibilité dans le groupe de ressources hello avec « Utilisation des disques gérés par » propriété trop « non » sont alors disponibles pour sélection. [En savoir plus sur les disques gérés et les groupes à haute disponibilité](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Si le compte de stockage hello utilisée pour la réplication a été chiffré avec un chiffrement de Service de stockage à n’importe quel point dans le temps, la création de disques gérés pendant le basculement échoue. Vous pouvez définir « Utilisation des disques gérés par » trop « non » et réessayez de basculement ou désactivez la protection pour la machine virtuelle de hello et protéger le compte de stockage tooa qui n’avait pas de chiffrement de service de stockage activé à n’importe quel point dans le temps.
  > [En savoir plus sur Storage Service Encryption et les disques gérés](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Déploiement de test hello

déploiement de hello tootest vous pouvez exécuter un test de basculement pour un seul ordinateur virtuel ou d’un plan de récupération qui contient un ou plusieurs ordinateurs virtuels.

### <a name="before-you-start"></a>Avant de commencer

 - Si vous souhaitez tooconnect tooAzure machines virtuelles à l’aide du protocole RDP après le basculement, en savoir plus sur [préparation tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test de toofully vous avez besoin de toocopy d’Active Directory et DNS dans votre environnement de test. [En savoir plus](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Exécution d’un test de basculement

1. toofail sur une seule machine virtuelle, dans **répliquées des éléments**, cliquez sur la machine virtuelle de hello > **+ Test de basculement**.
2. toofail sur la récupération d’un plan, en **les Plans de récupération**, plan de hello avec le bouton droit > **Test de basculement**. toocreate un plan de récupération, [suivez ces instructions](site-recovery-create-recovery-plans.md).
3. Dans **Test de basculement**, sélectionnez hello réseau Azure toowhich machines virtuelles Azure se connecter après le basculement se produit.
4. Cliquez sur **OK** toobegin hello basculement. Vous pouvez suivre la progression en cliquant sur hello VM tooopen ses propriétés, ou sur hello **Test de basculement** de la tâche dans **les tâches de récupération de Site**.
5. Une fois hello basculement terminé, vous devez également être en mesure de réplica de hello toosee machine Azure s’affichent dans hello portail Azure > **virtuels**. Il se peut que vous devez vous assurer que hello machine virtuelle est de taille hello appropriée, qu’il s’est connecté toohello de réseau appropriées et est en cours d’exécution.
6. Si vous préparé pour les connexions après le basculement, vous devez être en mesure de tooconnect toohello machine virtuelle Azure.
7. Une fois que vous avez terminé, cliquez sur **basculement de test de nettoyage** sur le plan de récupération hello. Dans **Notes** enregistrer toutes les observations associées au test de basculement hello. Cette opération supprimera les machines virtuelles hello qui ont été créés pendant le test de basculement.

Pour plus d’informations, lisez hello [tooAzure de basculement de Test](site-recovery-test-failover-to-azure.md) l’article.

## <a name="monitor-hello-deployment"></a>Moniteur hello déploiement

Voici comment vous pouvez surveiller les paramètres de configuration, l’état et l’intégrité pour hello déploiement de la récupération de Site :

1. Cliquez sur Bonjour coffre nom tooaccess Bonjour **Essentials** tableau de bord. Ce tableau affiche l’état de la réplication, les tâches, les plans de récupération, l’intégrité du serveur et les événements Site Recovery.  Vous pouvez personnaliser **Essentials** tooshow hello des vignettes et des dispositions qui sont plus utiles tooyou, y compris l’état hello d’autres coffres de sauvegarde et récupération de Site.

    ![Essentials](./media/site-recovery-vmm-to-azure/essentials.png)
2. Dans **intégrité**, vous pouvez analyser les problèmes sur des serveurs locaux (serveurs VMM ou de configuration) et hello les événements déclenchés par la récupération de Site Bonjour des dernières 24 heures.
3. Bonjour **répliquées des éléments**, **les Plans de récupération**, et **les tâches de récupération de Site** vignettes, vous pouvez gérer et surveiller la réplication. Vous pouvez accéder au détail des travaux dans **Travaux** > **Travaux Site Recovery**.

## <a name="command-line-installation-for-hello-azure-site-recovery-provider"></a>Installation de ligne de commande pour hello fournisseur Azure Site Recovery

Hello fournisseur Azure Site Recovery peut être installé à partir de hello de ligne de commande. Cette méthode peut être utilisé tooinstall hello fournisseur sur Server Core de Windows Server 2012 R2.

1. Téléchargez hello fournisseur de fichiers et d’enregistrement clé tooa dossier d’installation. par exemple, C:\ASR.
2. À partir d’une invite de commandes avec élévation de privilèges, exécutez ces programme d’installation de commandes tooextract hello fournisseur :

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Exécuter des composants de hello tooinstall de cette commande :

            C:\ASR> setupdr.exe /i
4. Ensuite, exécutez ces commandes, le serveur de hello tooregister dans le coffre hello :

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Où :

* **/ Informations d’identification**: un paramètre obligatoire qui spécifie où se trouve le fichier de clé d’inscription hello.  
* **/ FriendlyName**: paramètre obligatoire pour nom hello du serveur hôte hello Hyper-V qui s’affiche dans le portail Azure Site Recovery hello.
* * **/ EncryptionEnabled**: tooAzure des clouds de paramètre optionnel lorsque vous effectuez une réplication des ordinateurs virtuels Hyper-V dans VMM. Spécifier si vous souhaitez tooencrypt machines virtuelles Azure (au niveau de chiffrement de rest). Vérifiez que hello nom du fichier de hello a un **.pfx** extension. Par défaut, le chiffrement est désactivé

    > [!NOTE]
    > Il est recommandé de fonctionnalité de chiffrement hello toouse fournie par Azure pour chiffrer les données au repos, au lieu d’utiliser l’option de chiffrement hello (option EncryptionEnabled) fournie par Azure Site Recovery. fonctionnalité de chiffrement de Hello fournie par Azure peut être activée pour un compte de stockage et vous aide à obtenir de meilleures performances que hello chiffrement/déchiffrement est effectué par Azure  
    > Azure.
    > [En savoir plus sur le chiffrement du service de stockage dans Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
* **/ProxyAddress**: paramètre facultatif qui spécifie l’adresse hello du serveur de proxy hello.
* **/ProxyPort**: paramètre optionnel qui spécifie le port du serveur proxy de hello hello.
* **/proxyUsername**: paramètre facultatif qui spécifie le nom d’utilisateur proxy hello (si le proxy requiert une authentification).
* **/proxyPassword**: paramètre facultatif qui spécifie les tooauthenticate de mot de passe hello avec le serveur proxy (si le proxy de hello exige une authentification).


### <a name="network-bandwidth-considerations"></a>Remarques relatives à la bande passante réseau
Vous pouvez utiliser hello capacité planner outil toocalculate hello la bande passante que nécessaire pour la réplication (la réplication initiale, puis delta). toocontrol hello quantité utilisation de la bande passante pour la réplication, vous disposez de plusieurs options :

* **Limiter la bande passante**: le trafic de Hyper-V qui réplique le site secondaire de tooa passe par un hôte Hyper-V spécifique. Vous pouvez limiter la bande passante sur le serveur hôte de hello.
* **Optimiser la bande passante**: vous pouvez influer sur la bande passante hello utilisée pour la réplication à l’aide de deux clés de Registre.

#### <a name="throttle-bandwidth"></a>Limiter la bande passante
1. Ouvrez le composant logiciel enfichable MMC Microsoft Azure Backup hello sur le serveur hôte de Hyper-V hello. Par défaut, un raccourci pour Microsoft Azure Backup est disponible sur le bureau de hello ou dans C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Dans le composant logiciel enfichable hello, cliquez sur **modifier les propriétés**.
3. Sur hello **limitation** onglet, sélectionnez **activer l’utilisation de la bande passante internet pour les opérations de sauvegarde de limitation**et définir des limites de hello pour le travail et non liés au travail heures. Les plages valides sont de Mbits/s des too102 de 512 Kbits/s par seconde.

    ![Limiter la bande passante](./media/site-recovery-vmm-to-azure/throttle2.png)

Vous pouvez également utiliser hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) de limitation tooset applet de commande. Voici un exemple :

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indique qu’aucune limitation n’est requise.

#### <a name="influence-network-bandwidth"></a>Influer sur la bande passante réseau
Hello **UploadThreadsPerVM** valeur de Registre contrôle hello le nombre de threads qui sont utilisés pour le transfert de données (la réplication initiale ou delta) d’un disque. Une valeur plus élevée augmente la bande passante du réseau hello utilisée pour la réplication. Hello **DownloadThreadsPerVM** valeur de Registre spécifie le nombre de hello de threads utilisés pour le transfert de données pendant la restauration automatique.

1. Dans le Registre de hello, accédez trop**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.

   * Modifier la valeur de hello **UploadThreadsPerVM** (ou créer la clé de hello si elle n’existe pas) les threads toocontrol utilisées pour la réplication de disque.
   * Modifier la valeur de hello **DownloadThreadsPerVM** (ou créer la clé de hello si elle n’existe pas) les threads toocontrol utilisés pour le trafic de la restauration automatique d’Azure.
2. Hello par défaut est 4. Dans un réseau « surapprovisionnée », ces clés de Registre doivent être modifiées à partir des valeurs par défaut de hello. Hello maximal est 32. Surveiller le trafic toooptimize hello valeur.

## <a name="next-steps"></a>Étapes suivantes

Après la réplication initiale est terminée et que vous avez testé le déploiement de hello, vous pouvez appeler les basculements comme hello besoin. [En savoir plus](site-recovery-failover.md) sur différents types de basculement et la manière dont toorun les.
