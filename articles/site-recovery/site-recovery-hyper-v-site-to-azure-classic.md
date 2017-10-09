---
title: "tooAzure d’ordinateurs virtuels Hyper-V aaaReplicate dans le portail classique de hello | Documents Microsoft"
description: "Cet article décrit comment tooreplicate Hyper-V virtual machines tooAzure lorsque les ordinateurs ne sont pas gérées dans des clouds VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 3f4c4483-e3dd-495a-bd02-c16e9e28c88d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 12d08d950a79e956436cb03ffc87ab40e86c589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a>Réplication de machines virtuelles Hyper-V en local dans Azure (sans VMM) avec Azure Site Recovery
> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portail Classic](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

Cet article décrit comment tooreplicate local tooAzure d’ordinateurs virtuels Hyper-V, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure. Dans ce scénario, les serveurs Hyper-V ne sont pas gérés dans des clouds VMM.

Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="site-recovery-in-hello-azure-portal"></a>Récupération de site Bonjour portail Azure

Azure dispose de deux [modèles de déploiement](../resource-manager-deployment-model.md) différents pour créer et utiliser des ressources : le déploiement Azure Resource Manager et le déploiement classique. Azure a également deux portails : hello portail Azure classic et hello portail Azure.

Cet article décrit comment toodeploy dans le portail classique de hello. portail classique de Hello peut être utilisé toomaintain des archivages existants. Impossible de créer des coffres à l’aide du portail classique de hello.

## <a name="site-recovery-in-your-business"></a>Site Recovery dans votre entreprise

Les organisations besoin d’une stratégie BCDR qui détermine comment les applications et les données restent en cours d’exécution et disponibles pendant le temps d’arrêt planifiés et non planifiés et récupérer les conditions de travail toonormal dès que possible. Voici ce que Site Recovery peut faire :

* Protection hors site pour les applications professionnelles s’exécutant sur des machines virtuelles Hyper-V
* Un tooset emplacement unique, gérer et surveiller la réplication, le basculement et récupération.
* Basculement simple tooAzure et la restauration (restore) à partir des serveurs hôtes tooHyper-V Azure dans votre site local.
* Plans de récupération incluant plusieurs machines virtuelles et permettant ainsi le basculement simultané de charges de travail d’applications hiérarchisées

## <a name="azure-prerequisites"></a>Conditions préalables pour Azure
* Vous avez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) . Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Vous avez besoin d’un stockage Azure compte toostore répliquée de données. compte de Hello doit géo-réplication activée. Il doit être en hello même région que le coffre Azure Site Recovery hello et être associé hello même abonnement. [En savoir plus sur Azure Storage](../storage/common/storage-introduction.md). Notez que nous ne prend en charge le déplacement des comptes de stockage créés à l’aide de hello [nouveau portail Azure](../storage/common/storage-create-storage-account.md) plusieurs groupes de ressources.
* Vous devez un réseau virtuel Azure afin que les machines virtuelles Azure sera connecté tooa réseau lorsque vous basculez à partir de votre site principal.

## <a name="hyper-v-prerequisites"></a>Conditions préalables liées à Hyper-V
* Dans le site de hello source locale, vous devez un ou plusieurs serveurs en cours d’exécution **Windows Server 2012 R2** rôle hello Hyper-V est installé ou **Microsoft Hyper-V Server 2012 R2**. Ce serveur doit :
* contenir une ou plusieurs machines virtuelles ;
* Être connecté toohello Internet, directement ou via un proxy.
* Exécuter les correctifs hello décrites dans l’article [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977").

## <a name="virtual-machine-prerequisites"></a>Configuration requise pour les machines virtuelles
Machines virtuelles tooprotect doivent respecter les [spécifications de la machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="provider-and-agent-prerequisites"></a>Conditions préalables requises par les fournisseurs et les agents
Dans le cadre du déploiement d’Azure Site Recovery, vous allez installer hello fournisseur Azure Site Recovery et hello Azure Recovery Services Agent sur chaque serveur Hyper-V. Notez les points suivants :

* Nous vous recommandons toujours exécuté l’agent et les versions les plus récentes de hello fournisseur hello. Ils sont disponibles dans le portail Site Recovery hello.
* Tous les serveurs Hyper-V dans un coffre doit avoir hello même les versions de hello fournisseur et l’agent.
* Fournisseur qui s’exécute sur le serveur de hello Hello connecte tooSite récupération sur hello internet. Vous pouvez effectuer cela sans un proxy, les paramètres de proxy hello actuellement configurées sur le serveur d’Hyper-V hello ou avec les paramètres de proxy personnalisés que vous configurez pendant l’installation du fournisseur. Vous devez toomake que vous souhaitez toouse au serveur proxy hello peut accéder à ces URL hello pour la connexion tooAzure :

  * *.accesscontrol.windows.net
  * *.backup.windowsazure.com
  * *.hypervrecoverymanager.windowsazure.com
  * *.store.core.windows.net      
  * *.blob.core.windows.net
  - https://www.msftncsi.com/ncsi.txt
  - time.windows.com
  - time.nist.gov
* De plus autoriser les adresses IP de hello décrites dans [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/details.aspx?id=41653) et le protocole HTTPS (443). Vous avez des plages d’IP tooallow hello Hello région Azure que vous envisagez de toouse et celle de l’ouest des États-Unis.

Ce graphique montre les canaux de communication différentes hello et les ports utilisés par la récupération de Site pour l’orchestration et la réplication

![Topologie B2A](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a>Étape 1 : Créer un coffre
1. Connectez-vous à toohello [portail de gestion](https://portal.azure.com).
2. Développez **Data Services** > **Recovery Services**, puis cliquez sur **Coffre Site Recovery**.
3. Cliquez sur **Créer nouveau** > **Création rapide**.
4. Dans **nom**, entrez un coffre de hello tooidentify nom convivial.
5. Dans **région**, sélectionnez hello région géographique pour le coffre hello. les régions toocheck pris en charge consultez disponibilité géographique dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Cliquez sur **Create vault**.

    ![Nouveau coffre](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

Vérifiez tooconfirm de barre d’état hello qui hello coffre a été créé avec succès. Hello est répertorié en tant que **Active** sur la page Services de récupération de la principale hello.

## <a name="step-2-create-a-hyper-v-site"></a>Étape 2 : Créer un site Hyper-V
1. Dans la page des Services de récupération hello, cliquez sur page de démarrage rapide de hello coffre tooopen hello. Démarrage rapide peut également être ouvert à tout moment à l’aide d’icône de hello.

    ![Démarrage rapide](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. Dans la liste déroulante de hello, sélectionnez **entre un site de Hyper-V local et Azure**.

    ![Scénario de site Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. Sur la page **Créer un site Hyper-V**, cliquez sur **Créer un site Hyper-V**. Spécifiez un nom de site et enregistrez-le.

    ![Site Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-hello-provider-and-agent"></a>Étape 3 : Installer hello fournisseur et l’agent
Installez hello fournisseur et l’agent sur chaque serveur Hyper-V dont les machines virtuelles que vous souhaitez tooprotect.

Si vous installez sur un cluster Hyper-V, effectue les étapes 5 à 11 sur chaque nœud de cluster de basculement hello. Une fois que tous les nœuds sont enregistrés et la protection est activée, les machines virtuelles seront protégés même s’ils sont migrés sur les nœuds de cluster de hello.

1. Dans **Préparer les serveurs Hyper-V**, cliquez sur **Télécharger une clé d’inscription**.
2. Sur hello **télécharger la clé d’inscription** , cliquez sur **télécharger** site toohello suivant. Télécharger un emplacement sûr hello tooa clé qui est facilement accessible par le serveur de hello Hyper-V. clé de Hello est valide pendant 5 jours après sa génération.

    ![Clé d’enregistrement](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. Cliquez sur **téléchargement hello fournisseur** version la plus récente tooobtain hello.
4. Exécutez le fichier hello sur chaque serveur Hyper-V que vous souhaitez tooregister dans le coffre hello. fichier de Hello installe deux composants :
   * **Le fournisseur Azure Site Recovery**: gère la communication et l’orchestration entre le serveur de hello Hyper-V et le portail Azure Site Recovery hello.
   * **Azure Recovery Services Agent**: gère le transport de données entre des ordinateurs virtuels en cours d’exécution sur le serveur d’Hyper-V source hello et le stockage Azure.
5. Dans **Microsoft Update** , vous pouvez opter pour l’installation de mises à jour. Avec ce paramètre est activé, les mises à jour de fournisseur et l’Agent seront installés selon la stratégie de Microsoft Update tooyour.

    ![Mises à jour Microsoft](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. Dans **Installation** spécifier où vous souhaitez tooinstall hello fournisseur et l’Agent sur hello serveur Hyper-V.

    ![Emplacement d’installation](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. Une fois l’installation terminée continuer server de hello tooregister le programme d’installation dans le coffre hello.
8. Sur hello **paramètres du coffre** , cliquez sur **Parcourir** fichier de clé tooselect hello. Spécifier l’abonnement Azure Site Recovery de hello, nom du coffre hello, et hello Hyper-V site toowhich hello Hyper-V serveur appartient.

    ![Enregistrement du serveur](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. Sur hello **connexion Internet** page que vous spécifiez comment hello fournisseur connecte tooAzure Site Recovery. Sélectionnez **utiliser les paramètres du proxy système par défaut** paramètres de la connexion d’Internet toouse hello par défaut configurés sur le serveur de hello. Si vous ne spécifiez pas une valeur par défaut de hello valeur paramètres seront utilisés.

   ![Paramètres Internet](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. L’enregistrement démarre serveur hello de tooregister dans le coffre hello.

    ![Enregistrement du serveur](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. Une fois l’inscription terminée métadonnées hello Hyper-V server est extraites par Azure Site Recovery et serveur de hello est affiché sur hello **Sites Hyper-V** onglet hello **serveurs** page dans le coffre hello.

### <a name="install-hello-provider-from-hello-command-line"></a>Installer hello fournisseur à partir de la ligne de commande hello
En guise d’alternative, vous pouvez installer hello fournisseur Azure Site Recovery à partir de la ligne de commande hello. Vous devez utiliser cette méthode si vous souhaitez tooinstall hello fournisseur sur un ordinateur exécutant Windows Server Core 2012 R2. Exécutez à partir de la ligne de commande hello comme suit :

1. Téléchargez hello fournisseur de fichiers et d’enregistrement clé tooa dossier d’installation. par exemple C:\ASR.
2. Ouvrez une invite de commandes en tant qu’administrateur et saisissez la commande suivante :

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Installez ensuite hello fournisseur en exécutant :

        C:\ASR> setupdr.exe /i
4. Exécutez hello suivant toocomplete inscription :

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Les paramètres sont les suivants :

* **/ Informations d’identification**: spécifiez l’emplacement hello de clé d’inscription de hello vous avez téléchargé.
* **/ FriendlyName**: spécifiez un serveur hôte de nom tooidentify hello Hyper-V. Ce nom apparaîtra dans le portail de hello
* **/EncryptionEnabled**: facultatif. Spécifier si vous souhaitez tooencrypt réplica machines virtuelles Azure (au niveau de chiffrement de rest).
* **/proxyAddress** ; **/proxyport** ; **/proxyUsername** ; **/proxyPassword** : facultatifs. Spécifiez des paramètres de proxy si vous souhaitez toouse un proxy personnalisé, ou votre proxy existant nécessite une authentification.

## <a name="step-4-create-an-azure-storage-account"></a>Étape 4 : Création d’un compte de stockage Azure
* Dans **préparer les ressources** sélectionnez **créer un compte de stockage** toocreate si vous n’en avez un compte de stockage Azure. compte de Hello doit avoir la géo-réplication activée. Il doit être en hello même région que le coffre Azure Site Recovery hello et être associé hello même abonnement.

    ![Créer un compte de stockage](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. Nous ne prennent pas en charge déplacement hello de comptes de stockage créé à l’aide de hello [nouveau portail Azure](../storage/common/storage-create-storage-account.md) plusieurs groupes de ressources.
> 2. [Migration de comptes de stockage](../azure-resource-manager/resource-group-move-resources.md) entre les ressources groupes dans hello même abonnement ou entre abonnements n’est pas prise en charge pour les comptes de stockage utilisés pour le déploiement de Site Recovery.
>

## <a name="step-5-create-and-configure-protection-groups"></a>Étape 5 : Créer et configurer des groupes de protection
Groupes de protection sont des groupements logiques d’ordinateurs virtuels que vous souhaitez à l’aide de tooprotect hello mêmes paramètres de protection. Vous appliquez le groupe de protection de tooa de paramètres de protection, et ces paramètres sont appliqués tooall ordinateurs virtuels que vous ajoutez toohello groupe.

1. Dans **Créer et configurer des groupes de protection**, cliquez sur **Créer un nouveau groupe de protection**. Si la configuration requise n’est pas respectée, un message s’affiche. Vous pouvez cliquer sur **Afficher les détails** pour obtenir plus d’informations.
2. Bonjour **groupes de Protection** sous l’onglet Ajouter un groupe de protection. Spécifiez un nom, le site de Hyper-V source hello, la cible de hello **Azure**, votre nom de l’abonnement Azure Site Recovery et hello compte de stockage Azure.

    ![Groupe de protection](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. Dans **les paramètres de réplication** ensemble hello **fréquence de copie** toospecify la fréquence à laquelle delta de données hello doit être synchronisée entre hello source et cible. Vous pouvez définir too30 secondes, 5 minutes ou 15 minutes.
4. Dans la zone **Conserver les points de récupération** , indiquez le nombre d’heures de stockage de l’historique de récupération.
5. Dans **fréquence des instantanés cohérents au niveau applicatif** vous pouvez spécifier si les instantanés tootake qui utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello. Par défaut, aucun instantané n’est créé. Vérifiez que cette valeur est accessible sans que nombre hello de points de récupération supplémentaires que vous configurez. Cela est uniquement pris en charge si l’ordinateur virtuel de hello exécute un système d’exploitation de Windows.
6. Dans **heure de début de la réplication initiale** spécifiez quand la réplication initiale des machines virtuelles dans le groupe de protection hello doit être envoyée tooAzure.

    ![Groupe de protection](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a>Étape 6 : Activer la protection des machines virtuelles
Ajouter la protection tooenable du groupe de protection tooa machines virtuelles pour eux.

> [!NOTE]
> La protection des machines virtuelles exécutant Linux avec une adresse IP statique n’est pas prise en charge.
>
>

1. Sur hello **Machines** onglet hello groupe de protection, cliquez sur ** Ajouter les ordinateurs virtuels tooprotection groupes de protection de tooenable **.
2. Sur hello **activer la Protection des machines virtuelles** page Sélectionnez hello machines virtuelles tooprotect.

    ![Activer la protection pour les machines virtuelles](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    travaux d’activer la Protection Hello commence. Vous pouvez suivre la progression sur hello **travaux** onglet. Après le travail finaliser la Protection de hello machine virtuelle de hello s’exécute est prêt pour le basculement.
3. Une fois la protection activée, vous pouvez effectuer les opérations suivantes :

   * Afficher les ordinateurs virtuels dans **éléments protégés** > **groupes de Protection** > *protectiongroup_name*  >  **Virtuels** vous pouvez descendre détails toomachine Bonjour **propriétés** onglet...
   * Configurer les propriétés de basculement hello pour une machine virtuelle dans **éléments protégés** > **groupes de Protection** > *protectiongroup_name*  >  **Virtuels** *virtual_machine_name* > **configurer**. Vous pouvez configurer les éléments suivants :

     * **Nom**: nom hello de machine virtuelle de hello dans Azure.
     * **Taille**: hello taille cible de l’ordinateur virtuel hello qui bascule.

       ![Configurer les propriétés des machines virtuelles](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * Configurez les paramètres supplémentaires des machines virtuelles dans le champ *Éléments protégés** > **Groupes de protection** > *nom_groupeprotection* > **Machines virtuelles** *nom_machine_virtuelle* > **Configurer**, notamment :

     * **Cartes réseau**: nombre de hello de cartes réseau est dicté par taille hello que vous spécifiez pour la machine virtuelle cible hello. Vérifiez [spécifications de taille de machine virtuelle](../virtual-machines/linux/sizes.md) nombre hello de cartes réseau prises en charge par la taille de machine virtuelle hello.

       Lorsque vous modifiez taille hello pour un ordinateur virtuel et enregistrez les paramètres de hello, numéro hello de carte réseau change lorsque vous ouvrez **configurer** hello de page prochaine. nombre de Hello de cartes réseau de machines virtuelles cible est minimal de nombre hello de cartes réseau sur l’ordinateur virtuel source et le nombre maximal de cartes réseau prises en charge par la taille de hello de machine virtuelle de hello choisie. Vous trouverez l'explication ci-dessous :

       * Si le nombre de hello de cartes réseau sur l’ordinateur source de hello est inférieur ou égal toohello le nombre de cartes autorisé pour la taille de la machine cible hello, puis cible de hello aura hello même nombre de cartes en tant que source de hello.
       * Si nombre hello de cartes pour l’ordinateur virtuel de hello source dépasse nombre hello autorisé pour la taille cible hello puis la taille maximale de la cible hello est utilisé.
       * Par exemple, si un ordinateur source possède deux cartes réseau et prend en charge la taille de la machine cible hello quatre, l’ordinateur cible hello aura deux cartes. Si hello source ordinateur possède deux cartes, mais hello taille cible pris en charge uniquement en charge l’un de l’ordinateur cible hello aura qu’un seul adaptateur.

     * **Réseau Azure**: spécifiez la machine virtuelle de hello réseau toowhich hello doivent basculer. Si l’ordinateur virtuel de hello possède plusieurs cartes réseau de tous les adaptateurs doivent toohello connecté même réseau Azure.
     * **Sous-réseau** pour chaque carte réseau sur l’ordinateur virtuel de hello, sous-réseau hello select dans la machine de hello toowhich hello réseau Azure doit se connecter après le basculement.
     * **Adresse IP de cibler**: une adresse IP si l’adaptateur réseau de l’ordinateur virtuel source hello est configuré toouse statique d’adresses vous pouvez ensuite spécifier adresse hello pour tooensure de machine virtuelle cible hello qui hello machine a hello même adresse IP après un basculement .  Si vous ne spécifiez pas une adresse IP puis n’importe quelle adresse disponible sera affecté au moment du basculement de hello. Si vous spécifiez une adresse en cours d’utilisation, le basculement échoue.

     > [!NOTE]
     > [Migration des réseaux](../azure-resource-manager/resource-group-move-resources.md) entre les ressources groupes dans hello même abonnement ou entre abonnements n’est pas prise en charge pour les réseaux utilisés pour le déploiement de Site Recovery.
     >

     ![Configurer les propriétés des machines virtuelles](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a>Étape 7 : créer un plan de récupération
Dans le déploiement de hello tootest de commande, vous pouvez exécuter un test de basculement pour un seul ordinateur virtuel ou d’un plan de récupération qui contient un ou plusieurs ordinateurs virtuels. [En savoir plus](site-recovery-create-recovery-plans.md) sur la création d’un plan de récupération.

## <a name="step-8-test-hello-deployment"></a>Étape 8 : Tester le déploiement de hello
Il existe deux façons toorun un tooAzure de basculement de test.

* **Test de basculement sans réseau Azure**: ce type de test de basculement vérifie que l’ordinateur virtuel hello s’affiche correctement dans Azure. ordinateur virtuel de Hello n’est pas connecté tooany réseau Azure après le basculement.
* **Test de basculement avec un réseau Azure**: ce type de basculement vérifie que hello l’environnement de réplication se présente comme prévu et qui ont échoué sur les ordinateurs virtuels de hello connecte toohello réseau Azure cible de spécifié. Notez que pour le test de basculement sous-réseau hello d’ordinateur virtuel de test hello sera déterminé en basée sur le sous-réseau hello de machine virtuelle de réplication hello. Il s’agit de la réplication tooregular différents lorsque sous-réseau hello d’une machine virtuelle de réplication est basée sur le sous-réseau hello de machine virtuelle de hello source.

Si vous souhaitez toorun un test de basculement sans spécifier un réseau Azure vous n’avez pas besoin tooprepare quoi que ce soit.

toorun un test de basculement avec une réseau Azure, vous devez toocreate un réseau Azure isolé de votre réseau de production Azure (comportement par défaut lorsque vous créez un nouveau réseau dans Azure) de la cible. Lisez l’article [Basculement via Microsoft Azure Site Recovery](site-recovery-failover.md) pour plus de détails.

toofully tester votre déploiement de réplication et de réseau, vous devez tooset infrastructure de hello ainsi que hello répliquées toowork de machine virtuelle comme prévu. Une façon de faire ce tootooset une machine virtuelle comme contrôleur de domaine avec DNS et de les répliquer tooAzure à l’aide de toocreate de récupération de Site dans le test de hello réseau en exécutant un test de basculement.  [Lisez cet article](site-recovery-active-directory.md#test-failover-considerations) pour passer en revue les considérations relatives au test de basculement pour Active Directory.

Exécutez le test de basculement hello comme suit :

> [!NOTE]
> tooget hello meilleures performances lorsque vous effectuez un basculement tooAzure, assurez-vous que vous avez installé hello Agent Azure dans l’ordinateur de hello protégé. Cela permet de démarrer plus rapidement et de réaliser un diagnostic en cas de problème. L’agent Linux est disponible [ici](https://github.com/Azure/WALinuxAgent) et l’agent Windows est disponible [ici](http://go.microsoft.com/fwlink/?LinkID=394789)
>
>

1. Sur hello **les Plans de récupération** , sélectionnez le plan de hello et cliquez sur **Test de basculement**.
2. Sur hello **confirmer le Test de basculement** page Sélectionnez **aucun** ou un réseau Azure spécifique.  Notez que si vous sélectionnez **aucun** hello test de basculement vérifie que l’ordinateur virtuel hello répliquée correctement tooAzure mais ne vérifie pas votre configuration réseau de réplication.

    ![Test de basculement](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. Sur hello **travaux** onglet, vous pouvez suivre la progression du basculement. Vous devez également être toosee en mesure de test de réplica d’un ordinateur virtuel d’hello Bonjour portail Azure. Si vous êtes configuré tooaccess ordinateurs virtuels à partir de votre réseau local, vous pouvez lancer une machine virtuelle de bureau à distance connexion toohello.
4. Lorsque le basculement de hello atteint hello **test complet** de phase, cliquez sur **terminer le Test** toofinish hello test de basculement. Vous pouvez descendre toohello **travail** onglet progression du basculement tootrack et état et tooperform toutes les actions qui sont nécessaires.
5. Après le basculement, vous serez toosee en mesure de test de réplica d’un ordinateur virtuel d’hello Bonjour portail Azure. Si vous êtes configuré tooaccess ordinateurs virtuels à partir de votre réseau local, vous pouvez lancer une machine virtuelle de bureau à distance connexion toohello.

   1. Vérifiez que les ordinateurs virtuels hello démarrer correctement.
   2. Si vous souhaitez tooconnect toohello machine virtuelle Azure à l’aide du Bureau à distance après le basculement de hello, activer la connexion Bureau à distance sur l’ordinateur virtuel de hello avant d’exécuter le test de basculement hello. Vous devez également tooadd un point de terminaison RDP sur l’ordinateur virtuel de hello. Vous pouvez exploiter une [runbook Azure automation](site-recovery-runbook-automation.md) toodo qui.
   3. Une fois le basculement si vous utilisez un ordinateur virtuel toohello de publique IP adresse tooconnect dans Azure à l’aide du Bureau à distance, vérifiez que vous n’avez toutes les stratégies de domaine qui empêchent la connexion de la machine virtuelle de tooa à l’aide d’une adresse publique.
6. Effectuez l’issue du test de hello hello suivant :

   * Cliquez sur **hello test de basculement est terminé**. Nettoyage hello power de tooautomatically d’environnement de test désactiver et supprimer des machines virtuelles de test hello.
   * Cliquez sur **Notes** toorecord enregistrer toutes les observations associées au basculement de test hello.
7. Lorsque le basculement de hello atteint hello **test complet** terminer la phase de vérification de hello comme suit :
   1. Permet d’afficher l’ordinateur virtuel de réplication d’hello Bonjour portail Azure. Vérifiez que l’ordinateur virtuel hello démarre correctement.
   2. Si vous êtes configuré tooaccess ordinateurs virtuels à partir de votre réseau local, vous pouvez lancer une machine virtuelle de bureau à distance connexion toohello.
   3. Cliquez sur **test de hello complète** toofinish il.
   4. Cliquez sur **Notes** toorecord enregistrer toutes les observations associées au basculement de test hello.
   5. Cliquez sur **hello test de basculement est terminé**. Nettoyage hello power de tooautomatically d’environnement de test désactiver et supprimer l’ordinateur virtuel de test hello.

## <a name="next-steps"></a>Étapes suivantes
Une fois votre déploiement configuré et en cours d'exécution, découvrez [plus d'informations](site-recovery-failover.md) sur le basculement.
