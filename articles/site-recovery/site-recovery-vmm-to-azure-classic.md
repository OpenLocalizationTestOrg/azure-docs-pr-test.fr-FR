---
title: "machines virtuelles d’aaaReplicate Hyper-V dans VMM clouds tooAzure | Documents Microsoft"
description: "Cet article décrit comment virtuels tooreplicate Hyper-V sur des ordinateurs hôtes Hyper-V situé dans tooAzure des clouds System Center VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 9d526a1f-0d8e-46ec-83eb-7ea762271db5
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 136f68585534c17b615ecc4e82c0133bf813503f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure"></a>Réplication d’ordinateurs virtuels Hyper-V dans VMM clouds tooAzure
> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-vmm-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Portail classique](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Classique](site-recovery-deploy-with-powershell.md)
>
>

Hello service Azure Site Recovery contribue tooyour continuité des activités et la stratégie de récupération d’urgence en orchestrant ces opérations de réplication, le basculement et récupération des ordinateurs virtuels et des serveurs physiques. Machines peuvent être répliquée tooAzure ou centre de données secondaire locale tooa. Pour avoir un rapide aperçu, consultez la section [Qu’est-ce qu’Azure Site Recovery ?](site-recovery-overview.md)

## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment toodeploy Site Recovery tooreplicate Hyper-V virtuels sur Hyper-V hébergent les serveurs qui sont trouvent dans tooAzure des clouds privés VMM.

article de Hello inclut les conditions préalables requises pour le scénario de hello et affiche comment tooset d’un coffre Site Recovery, exploiter hello fournisseur Azure Site Recovery installé sur le serveur VMM source à hello, inscrire le serveur de hello dans le coffre de hello, ajouter un compte de stockage Azure, installez hello Azure agent Recovery Services sur les serveurs hôtes de Hyper-V, configurez les paramètres de protection pour les clouds VMM qui seront appliqués tooall protégé par les ordinateurs virtuels et puis réactivez la protection pour ces ordinateurs virtuels. Terminez en toomake de basculement de test hello que tout fonctionne comme prévu.

Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Architecture
![Architecture](./media/site-recovery-vmm-to-azure-classic/topology.png)

* Hello fournisseur Azure Site Recovery est installé sur hello VMM durant le déploiement de la récupération de Site et le serveur VMM de hello est enregistré dans le coffre Site Recovery hello. Hello fournisseur communique avec l’orchestration de la réplication toohandle Site Recovery.
* Hello Azure Recovery Services agent est installé sur les serveurs hôtes Hyper-V lors du déploiement de la récupération de Site. Il gère le stockage de tooAzure de réplication de données.

## <a name="azure-prerequisites"></a>Conditions préalables pour Azure
Voici ce dont vous aurez besoin dans Azure :

| **Configuration requise** | **Détails** |
| --- | --- |
| **Compte Azure** |Vous aurez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) . Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/). [En savoir plus](https://azure.microsoft.com/pricing/details/site-recovery/) sur la tarification Site Recovery. |
| **Stockage Azure** |Vous aurez besoin d’un stockage Azure compte toostore répliquée de données. Les données répliquées sont stockées dans le stockage Azure et les machines virtuelles Azure sont lancées au moment du basculement. <br/><br/>Vous avez besoin d’un [compte de stockage géoredondant standard](../storage/common/storage-redundancy.md#geo-redundant-storage). Hello compte doit être en hello même région que le service de récupération de Site hello et être associé à hello même abonnement. Notez que les comptes de stockage toopremium de réplication n’est pas pris en charge actuellement et ne doivent pas être utilisées.<br/><br/>[Découvrez plus d’informations](../storage/common/storage-introduction.md) sur Azure Storage. |
| **Réseau Azure** |Vous aurez besoin d’un réseau virtuel Azure qui se connectera machines virtuelles Azure toowhen basculement se produit. réseau virtuel Azure Hello doit être Bonjour même région que le coffre Site Recovery hello. |

## <a name="on-premises-prerequisites"></a>Conditions préalables locales
Voici ce dont vous aurez besoin en local :

| **Configuration requise** | **Détails** |
| --- | --- |
| **VMM** |Vous devez disposer d’au moins un serveur VMM déployé comme serveur autonome physique ou virtuel, ou comme cluster virtuel. <br/><br/>serveur VMM de Hello doit exécuter System Center 2012 R2 hello dernières mises à jour cumulatives.<br/><br/>Vous devez au moins un cloud configuré sur le serveur VMM de hello.<br/><br/>cloud de source de Hello que vous souhaitez tooprotect doit contenir un ou plusieurs groupes d’hôtes VMM.<br/><br/>Pour en savoir plus sur la configuration des clouds VMM, consultez la rubrique [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx) (Procédure pas à pas : création de clouds privés avec System Center 2012 SP1 VMM) dans le blog de Keith Mayer. |
| **Hyper-V** |Vous aurez besoin d’un ou plusieurs serveurs hôtes Hyper-V ou des clusters dans hello cloud VMM. serveur hôte de Hello doit avoir et un ou plusieurs ordinateurs virtuels. <br/><br/>serveur de Hello Hyper-V doit s’exécuter sur au moins **Windows Server 2012 R2** avec le rôle de hello Hyper-V ou **Microsoft Hyper-V Server 2012 R2** et avez hello les dernières mises à jour installées.<br/><br/>N’importe quel serveur Hyper-V contenant des machines virtuelles que vous souhaitiez tooprotect doit se trouver dans un cloud VMM.<br/><br/>Si vous utilisez Hyper-V dans un cluster, notez que le service Broker du cluster n'est pas créé automatiquement si vous avez un cluster basé sur des adresses IP statiques. Vous devez manuellement service broker de cluster tooconfigure hello. [En savoir plus](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) sur l’entrée de blog d’Aidan Finn. |
| **Machines protégées** | Machines virtuelles doivent satisfaire tooprotect [conditions requises pour Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). |

## <a name="network-mapping-prerequisites"></a>Conditions préalables liées au mappage réseau
Lorsque vous protégez des ordinateurs virtuels dans le mappage réseau Azure mappe entre les réseaux d’ordinateurs virtuels sur le serveur VMM de source hello et suivant de hello de tooenable de réseaux Azure cible :

* Toutes les machines qui basculent sur hello même réseau peut se connecter tooeach autre, quel que soit le plan de récupération auquel elles sont dans.
* Si une passerelle de réseau est configurée sur le réseau Azure cible de hello, les machines virtuelles peuvent se connecter tooother locaux virtuels.
* Si vous ne configurez pas de réseau mappage seuls les ordinateurs virtuels qui basculent Bonjour même plan de récupération sera en mesure de tooconnect tooeach autres après basculement tooAzure.

Si vous souhaitez que le mappage réseau toodeploy, vous devez suivant de hello :

* Hello machines virtuelles tooprotect sur le serveur VMM de hello source doit être connecté tooa réseau d’ordinateurs virtuels. Ce réseau doit être lié tooa réseau logique associé au cloud de hello.
* Un réseau de Azure toowhich répliquée d’ordinateurs virtuels peuvent se connecter après le basculement. Vous devez sélectionner ce réseau au moment du basculement de hello. réseau de Hello doivent se trouver dans hello même région que votre abonnement Azure Site Recovery.


Préparez les réseaux dans VMM :

   * [Configurez les réseaux logiques](https://technet.microsoft.com/library/jj721568.aspx).
   * [Configurez les réseaux de machines virtuelles](https://technet.microsoft.com/library/jj721575.aspx).


## <a name="step-1-create-a-site-recovery-vault"></a>Étape 1 : Création d’un coffre Site Recovery
1. Connectez-vous à toohello [portail de gestion](https://portal.azure.com) d’un serveur VMM hello souhaité tooregister.
2. Développez **Services de données** > **Services de récupération** > , puis cliquez sur **Coffre Site Recovery**.
3. Cliquez sur **Créer nouveau** > **Création rapide**.
4. Dans **nom**, entrez un coffre de hello tooidentify nom convivial.
5. Dans **région**, sélectionnez hello région géographique pour le coffre hello. les régions toocheck pris en charge consultez disponibilité géographique dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Cliquez sur **Create vault**.

    ![Nouveau coffre](./media/site-recovery-vmm-to-azure-classic/create-vault.png)

Vérifiez tooconfirm de barre d’état hello qui hello coffre a été créé avec succès. Hello est répertorié en tant que **Active** sur la page Services de récupération de la principale hello.

## <a name="step-2-generate-a-vault-registration-key"></a>Étape 2 : Génération d’une clé d'inscription du coffre
Générer une clé d’inscription dans le coffre hello. Une fois que vous téléchargez hello fournisseur Azure Site Recovery et l’installer sur le serveur VMM de hello, vous allez utiliser ce serveur VMM de hello tooregister clé dans le coffre hello.

1. Bonjour **Services de récupération** , cliquez sur la page de démarrage rapide de hello coffre tooopen hello. Démarrage rapide peut également être ouvert à tout moment à l’aide d’icône de hello.

    ![Icône Quick Start](./media/site-recovery-vmm-to-azure-classic/qs-icon.png)
2. Dans la liste déroulante de hello, sélectionnez **entre un site VMM local et le Microsoft Azure**.
3. Dans **Prepare VMM Servers**, cliquez sur le fichier **Generate registration key**. fichier de clé Hello est généré automatiquement et n’est valide pendant 5 jours après sa génération. Si vous n’accédez pas à hello portail Azure à partir du serveur VMM de hello vous devez toocopy ce serveur toohello de fichiers.

    ![Clé d’enregistrement](./media/site-recovery-vmm-to-azure-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Étape 3 : Installer hello fournisseur Azure Site Recovery
1. Dans **Quick Start** > **serveurs VMM de préparer**, cliquez sur **télécharger le fournisseur Microsoft Azure Site Recovery pour installation sur les serveurs VMM** tooobtain hello dernière version du fichier d’installation hello.
2. Exécuter ce fichier sur le serveur VMM de hello source.

   > [!NOTE]
   > Si VMM est déployé dans un cluster et que vous installez hello fournisseur pour hello première installez-la sur un nœud actif et terminer hello installation tooregister hello serveur VMM dans le coffre hello. Installez hello fournisseur sur hello autres nœuds. Notez que si vous mettez à niveau hello fournisseur, vous devez tooupgrade sur tous les nœuds, car elles doivent toutes être en cours d’exécution hello même version du fournisseur.
   >
   >
3. Hello programme d’installation effectue une vérification des conditions préalables et demande l’autorisation toostop hello VMM service toobegin fournisseur le programme d’installation. Hello Service VMM va redémarrer automatiquement lorsque le programme d’installation se termine. Si vous installez sur un cluster VMM que vous serez invité toostop le rôle de Cluster hello.
4. Dans **Microsoft Update** , vous pouvez opter pour l’installation de mises à jour. Avec ce paramètre activés les mises à jour fournisseur seront installés selon la stratégie de Microsoft Update tooyour.

    ![Mises à jour Microsoft](./media/site-recovery-vmm-to-azure-classic/updates.png)
5. emplacement d’installation pour hello fournisseur est défini trop de Hello**<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Cliquez sur **Installer**.

   ![Emplacement de l’installation](./media/site-recovery-vmm-to-azure-classic/install-location.png)
6. Après avoir hello fournisseur est installé, cliquez sur **inscrire** serveur hello de tooregister dans le coffre hello.

    ![Installation terminée](./media/site-recovery-vmm-to-azure-classic/install-complete.png)
7. Dans **nom du coffre**, vérifier nom hello de coffre hello dans le hello serveur sera inscrit. Cliquez sur *Suivant*.

    ![Enregistrement du serveur](./media/site-recovery-vmm-to-azure-classic/vaultcred.PNG)
8. Dans **connexion Internet** spécifier comment hello fournisseur qui s’exécute sur hello VMM server connecte toohello Internet. Sélectionnez **se connecter avec des paramètres proxy existants** paramètres de la connexion d’Internet toouse hello par défaut configurés sur le serveur de hello.

    ![Paramètres Internet](./media/site-recovery-vmm-to-azure-classic/proxydetails.PNG)

   * Si vous voulez toouse un proxy personnalisé vous devez installez-le avant d’installer le fournisseur de hello. Lorsque vous configurez les paramètres de proxy personnalisés un test s’exécutera de connexion au proxy toocheck hello.
   * Si vous utilisez un proxy personnalisé, ou votre proxy par défaut nécessite une authentification, vous devez tooenter hello proxy plus d’informations, y compris le port et l’adresse de proxy hello.
   * URL suivantes doit être accessible à partir de hello serveur VMM et des ordinateurs hôtes Hyper-v de hello
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Autoriser les adresses IP de hello décrites dans [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653) et le protocole HTTPS (443). Vous devriez toowhite-liste des plages IP de hello région Azure que vous envisagez de toouse et celle de l’ouest des États-Unis.
   * Si vous utilisez un proxy personnalisé un compte RunAs VMM (DRAProxyAccount) est créé automatiquement à l’aide de hello spécifié les informations d’identification de proxy. Configurer le serveur de proxy hello afin que ce compte peut s’authentifier avec succès. paramètres du compte RunAs VMM Hello peuvent être modifiés dans la console VMM hello. toodo, ouvrez hello **paramètres** espace de travail, développez **sécurité**, cliquez sur **comptes d’identification**, puis modifiez le mot de passe hello de DRAProxyAccount. Vous devez le service VMM toorestart hello afin que ce paramètre prenne effet.
9. Dans **clé d’inscription**, sélectionnez clé hello téléchargés à partir d’Azure Site Recovery et copiée serveur VMM de toohello.
10. paramètre de chiffrement Hello est uniquement utilisé lorsque vous répliquez des ordinateurs virtuels Hyper-V dans VMM clouds tooAzure. Si vous effectuez une réplication site secondaire de tooa n’est pas utilisé.
11. Dans **nom du serveur**, spécifiez un serveur VMM à hello tooidentify nom convivial dans le coffre hello. Dans une configuration de cluster spécifier le nom de rôle de cluster VMM hello.
12. Dans **synchroniser les métadonnées du cloud** Indiquez si vous souhaitez toosynchronize métadonnées pour tous les clouds sur le serveur VMM de hello avec le coffre de hello. Cette action ne doit toohappen qu’une seule fois sur chaque serveur. Si vous ne souhaitez pas toosynchronize tous les clouds, vous pouvez laisser ce paramètre désactivé et synchroniser chaque cloud individuellement dans les propriétés du cloud hello dans la console VMM hello.
13. Cliquez sur **suivant** processus de hello toocomplete. Après l’inscription, les métadonnées d’un serveur hello VMM sont récupérées par Azure Site Recovery. serveur de Hello est affiché sur hello **serveurs VMM** onglet hello **serveurs** page dans le coffre hello.

    ![Dernière page](./media/site-recovery-vmm-to-azure-classic/provider13.PNG)

Après l’inscription, les métadonnées d’un serveur hello VMM sont récupérées par Azure Site Recovery. serveur de Hello est affiché sur hello **serveurs VMM** , onglet hello **serveurs** page dans le coffre hello.

### <a name="command-line-installation"></a>Installer à partir de la ligne de commande
Hello fournisseur Azure Site Recovery peut également être installé à l’aide de hello suivant la ligne de commande. Cette méthode peut être le fournisseur de hello tooinstall utilisé sur un serveur de base pour Windows Server 2012 R2.

1. Téléchargez hello fournisseur de fichiers et d’enregistrement clé tooa dossier d’installation. par exemple : C:\ASR.
2. Arrêter le service System Center Virtual Machine Manager de hello
3. À partir d’une invite de commandes avec élévation de privilèges, extrayez le programme d’installation du fournisseur hello avec ces commandes :

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Installez le fournisseur de hello comme suit :

        C:\ASR> setupdr.exe /i
5. Enregistrer hello fournisseur comme suit :

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Où les paramètres sont les suivants :

* **/ Informations d’identification** : un paramètre obligatoire qui spécifie l’emplacement de hello dans le hello se trouve le fichier de clé d’inscription  
* **/ FriendlyName** : paramètre obligatoire pour nom hello du serveur hôte hello Hyper-V qui s’affiche dans le portail Azure Site Recovery hello.
* **/ EncryptionEnabled** : paramètre facultatif toospecify si vous souhaitez tooencryption vos machines virtuelles dans Azure (au niveau de chiffrement de rest). nom de fichier Hello doit avoir un **.pfx** extension.
* **/ProxyAddress** : paramètre facultatif qui spécifie l’adresse hello du serveur de proxy hello.
* **/ProxyPort** : paramètre optionnel qui spécifie le port du serveur proxy de hello hello.
* **/proxyUsername** : paramètre facultatif qui spécifie le nom d’utilisateur proxy hello.
* **/proxyPassword** : paramètre facultatif qui spécifie le mot de passe proxy hello.  

## <a name="step-4-create-an-azure-storage-account"></a>Étape 4 : Création d’un compte de stockage Azure
1. Si vous n’avez pas de compte de stockage Azure cliquez sur **ajouter un compte Azure Storage** toocreate un compte.
2. La géo-réplication doit être activée dans le compte que vous créez. Il doit en hello même région que hello service Azure Site Recovery et être associé à hello même abonnement.

    ![Compte de stockage](./media/site-recovery-vmm-to-azure-classic/storage.png)

> [!NOTE]
> [Migration de comptes de stockage](../azure-resource-manager/resource-group-move-resources.md) entre les ressources groupes dans hello même abonnement ou entre abonnements n’est pas prise en charge pour les comptes de stockage utilisés pour le déploiement de Site Recovery.
>
>

## <a name="step-5-install-hello-azure-recovery-services-agent"></a>Étape 5 : Installation Bonjour Azure Recovery Services Agent
Installez l’agent Azure Recovery Services de hello sur chaque serveur hôte Hyper-V hello cloud VMM.

1. Cliquez sur **Quick Start** > **télécharger Azure Site Recovery Services Agent et installer sur les hôtes** tooobtain hello dernière version du fichier d’installation de l’agent de hello.

    ![Install Recovery Services Agent](./media/site-recovery-vmm-to-azure-classic/install-agent.png)
2. Exécutez le fichier d’installation hello sur chaque serveur hôte Hyper-V.
3. Sur hello **vérification** page, cliquez sur **suivant**. Tous les éléments manquants de la configuration requise sont automatiquement installés.

    ![Prerequisites Recovery Services Agent](./media/site-recovery-vmm-to-azure-classic/agent-prereqs.png)
4. Sur hello **les paramètres d’Installation** , spécifiez où vous souhaitez l’agent de tooinstall hello et l’emplacement de cache hello select dans laquelle les métadonnées de sauvegarde seront installée. Cliquez ensuite sur **Installer**.
5. Une fois l’installation terminée, cliquez sur **fermer** Assistant de hello toocomplete.

    ![Inscrire l’Agent MARS](./media/site-recovery-vmm-to-azure-classic/agent-register.png)

### <a name="command-line-installation"></a>Installer à partir de la ligne de commande
Vous pouvez également installer hello Microsoft Azure Recovery Services Agent à partir de la ligne de commande hello à l’aide de cette commande :

    marsagentinstaller.exe /q /nu

## <a name="step-6-configure-cloud-protection-settings"></a>Étape 6 : Configuration des paramètres de protection de cloud
Une fois que le serveur VMM de hello est inscrit, vous pouvez configurer les paramètres de protection de cloud. Vous avez activé l’option de hello **synchroniser les données de cloud avec le coffre de hello** hello fournisseur lorsque vous avez installé, tous les clouds sur le serveur VMM de hello seront affiche sous hello <b>éléments protégés</b> onglet dans le coffre hello.

![Cloud publié](./media/site-recovery-vmm-to-azure-classic/clouds-list.png)

1. Dans la page de démarrage rapide de hello, cliquez sur **configurer la protection pour les clouds VMM**.
2. Sur hello **éléments protégés** onglet, cliquez sur le cloud de hello vous le souhaitez tooconfigure et accédez toohello **Configuration** onglet.
3. Dans **Cible** select **Azure**
4. Dans **compte de stockage** sélectionnez le compte de stockage Azure hello vous utilisez pour la réplication.
5. Définissez **chiffrer les données stockées** trop**hors**. Ce paramètre spécifie que les données doivent être chiffrées pendant la réplication entre deux sites locaux hello et Azure.
6. Dans **fréquence de copie** laissez le paramètre par défaut de hello. Cette valeur indique la fréquence de synchronisation des données entre les emplacements source et cible.
7. Dans **conserver les points de récupération pour**, laissez le paramètre par défaut de hello. Avec une valeur par défaut de zéro, seul hello dernier point de récupération pour un ordinateur virtuel principal est stocké sur un serveur hôte de réplica.
8. Dans **fréquence des instantanés cohérents au niveau applicatif**, laissez le paramètre par défaut de hello. Cette valeur spécifie la fréquence à laquelle les instantanés toocreate. Instantanés utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello.  Si vous ne définissez pas de valeur, assurez-vous qu’il est inférieur au nombre de hello de points de récupération supplémentaires que vous configurez.
9. Dans **heure de début de la réplication**, spécifiez quand la réplication initiale des données tooAzure doit démarrer. fuseau horaire de Hello sur le serveur hôte de Hyper-V hello sera utilisé. Nous vous recommandons de planifier la réplication initiale hello pendant les heures creuses.

    ![Cloud replication settings](./media/site-recovery-vmm-to-azure-classic/cloud-settings.png)

Après avoir enregistré les paramètres hello un travail est créé et peuvent être surveillé sur hello **travaux** onglet. Tous les serveurs hôtes de Hyper-V dans hello cloud source VMM seront configurés pour la réplication.

Après l’enregistrement, les paramètres de cloud peuvent être modifiés sur hello **configurer** onglet toomodify hello emplacement cible ou le compte de stockage cible vous aurez besoin de configuration du cloud tooremove hello, puis reconfigurez hello cloud. Notez que si vous modifiez la modification hello du compte de stockage hello s’appliquent uniquement aux ordinateurs virtuels qui sont activés pour la protection une fois le compte de stockage hello a été modifié. Les ordinateurs virtuels existants ne sont pas migrés toohello nouveau compte de stockage.

## <a name="step-7-configure-network-mapping"></a>Étape 7 : Configuration du mappage réseau
Avant de commencer le mappage réseau Vérifiez que les ordinateurs virtuels sur le serveur VMM de hello source sont connectés tooa réseau d’ordinateurs virtuels. En outre, vous devez créer un ou plusieurs réseaux virtuels Azure. Notez que plusieurs réseaux d’ordinateurs virtuels peuvent être mappés tooa réseau Azure unique.

1. Dans la page de démarrage rapide de hello, cliquez sur **mapper les réseaux**.
2. Sur hello **réseaux** sous l’onglet **emplacement Source**, sélectionnez serveur VMM de hello source. Dans **Emplacement cible** , sélectionnez Azure.
3. Dans **Source** réseaux serveur VMM de hello associée à une liste de réseaux d’ordinateurs virtuels sont affichés. Dans **cible** réseaux hello Azure réseaux associés hello abonnement sont affichés.
4. Sélectionnez le réseau d’ordinateurs virtuels source hello et cliquez sur **carte**.
5. Sur hello **sélectionner un réseau cible** page cible de hello sélectionnez Azure réseau toouse.
6. Cliquez sur le processus de mappage hello coche toocomplete hello.

    ![Cloud replication settings](./media/site-recovery-vmm-to-azure-classic/map-networks.png)

Après avoir enregistré les paramètres hello un travail démarre la progression du mappage tootrack hello et il peut être surveillé sur l’onglet tâches de hello. Les ordinateurs virtuels réplica existants qui correspondent le réseau d’ordinateurs virtuels toohello source sera connecté toohello réseaux Azure cibles. Nouveaux ordinateurs virtuels qui sont le réseau d’ordinateurs virtuels connectés toohello source sera connecté toohello de réseau Azure mappé après la réplication. Si vous modifiez un mappage existant avec un nouveau réseau, les machines virtuelles de réplication sera connectées à l’aide de nouveaux paramètres de hello.

Notez que si le réseau cible de hello possède plusieurs sous-réseaux et d’un de ces sous-réseaux a hello trouve du même nom que le sous-réseau sur lequel hello source virtual machine, puis hello ordinateur virtuel sera connecté toothat cible sous-réseau après le basculement. S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.

> [!NOTE]
> [Migration des réseaux](../azure-resource-manager/resource-group-move-resources.md) entre les ressources groupes dans hello même abonnement ou entre abonnements n’est pas prise en charge pour les réseaux utilisés pour le déploiement de Site Recovery.
>
>

## <a name="step-8-enable-protection-for-virtual-machines"></a>Étape 8 : Activation de la protection des machines virtuelles
Une fois les serveurs, les clouds et les réseaux configurés, vous pouvez activer la protection des machines virtuelles dans le cloud de hello. Notez hello suivantes :

* Les machines virtuelles doivent respecter la [configuration requise pour Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
* système d’exploitation de tooenable protection hello et les propriétés de disque de système d’exploitation doivent être définies pour la machine virtuelle de hello. Lorsque vous créez un ordinateur virtuel dans VMM à l’aide d’un modèle d’ordinateur virtuel, vous pouvez définir la propriété de hello. Vous pouvez également définir ces propriétés pour les ordinateurs virtuels existants sur hello **général** et **Configuration matérielle** onglets des propriétés d’ordinateur virtuel hello. Si vous ne définissez pas ces propriétés dans VMM, vous serez en mesure de tooconfigure dans le portail Azure Site Recovery hello.

    ![Create virtual machine](./media/site-recovery-vmm-to-azure-classic/enable-new.png)

    ![Modify virtual machine properties](./media/site-recovery-vmm-to-azure-classic/enable-existing.png)

1. protection tooenable, hello **virtuels** dans le cloud hello dans le hello ordinateur virtuel se trouve sous l’onglet **activer la protection** > **ajouter des ordinateurs virtuels**.
2. À partir de la liste de hello d’ordinateurs virtuels dans le cloud de hello, sélectionnez hello une souhaité tooprotect.

    ![Activer la protection pour les machines virtuelles](./media/site-recovery-vmm-to-azure-classic/select-vm.png)

    Suivre la progression de hello **activer la Protection** action Bonjour **travaux** onglet, y compris la réplication initiale hello. Après avoir hello **finaliser la Protection** s’exécute la tâche hello virtual machine est prête pour le basculement. Une fois la protection est activée et machines virtuelles répliquées, vous serez en mesure de tooview dans Azure.

    ![Tâche de protection de la machine virtuelle](./media/site-recovery-vmm-to-azure-classic/vm-jobs.png)

1. Vérifiez les propriétés de machine virtuelle hello et modifiez-le si nécessaire.

    ![Verify virtual machines](./media/site-recovery-vmm-to-azure-classic/vm-properties.png)
2. Sur hello **configurer** onglet des propriétés d’ordinateur virtuel hello réseau propriétés suivantes peut être modifié.

* **Nombre de cartes réseau sur la machine virtuelle cible hello** -nombre hello de cartes réseau est dicté par taille hello que vous spécifiez pour la machine virtuelle cible hello. Vérifiez [spécifications de taille de machine virtuelle](../virtual-machines/linux/sizes.md) pour nombre de hello de cartes pris en charge par la taille de machine virtuelle hello. Lorsque vous modifiez taille hello pour un ordinateur virtuel et enregistrez les paramètres de hello, nombre hello de cartes réseau change hello prochaine ouverture hello **configurer** page. nombre Hello de cartes réseau de machines virtuelles cible est le nombre minimal de hello de cartes réseau sur la source de machines virtuelles et hello nombre maximal de cartes réseau prises en charge par la taille de hello de machine virtuelle de hello choisi, comme suit :

  * Si le nombre de hello de cartes réseau sur l’ordinateur source de hello est inférieur ou égal toohello le nombre de cartes autorisé pour la taille de la machine cible hello, puis cible de hello aura hello même nombre de cartes en tant que source de hello.
  * Si nombre hello de cartes pour l’ordinateur virtuel de hello source dépasse nombre hello autorisé pour la taille cible hello puis la taille maximale de la cible hello est utilisé.
  * Par exemple, si un ordinateur source possède deux cartes réseau et la taille de la machine cible hello prend en charge quatre, l’ordinateur cible hello aura deux cartes. Si hello source ordinateur possède deux cartes, mais hello taille cible pris en charge uniquement en charge l’un de l’ordinateur cible hello aura qu’un seul adaptateur.     
* **Réseau de la machine virtuelle cible hello** -machine virtuelle de hello réseau toowhich hello se connecte toois déterminé par le mappage réseau du réseau hello de l’ordinateur virtuel source. Si l’ordinateur virtuel de hello source a plusieurs réseaux source et de la carte de réseau sont réseaux toodifferent mappé sur la cible, vous devrez alors toochoose entre un des réseaux de cible hello.
* **Sous-réseau de chaque carte réseau** - pour chaque carte réseau que vous pouvez sélectionner hello de toowhich hello sous-réseau a échoué sur l’ordinateur virtuel se connecte à.
* **Adresse IP de cibler** - si la carte réseau de hello de machine virtuelle source est toouse configuré une adresse IP statique d’adresses vous pouvez fournir l’adresse IP de hello pour la machine virtuelle cible hello. Utilisez cette fonctionnalité conserver l’adresse IP de hello d’une machine virtuelle source après un basculement. Si aucune adresse IP n’est fournie n’importe quelle adresse IP disponible reçoit l’adaptateur réseau toohello au moment du basculement de hello. Si l’adresse IP de hello cible est spécifié mais qu’il est déjà utilisé par une autre machine virtuelle s’exécutant dans Azure, basculement échoue.  

    ![Modifier les propriétés du réseau](./media/site-recovery-vmm-to-azure-classic/multi-nic.png)

> [!NOTE]
> Les machines virtuelles Linux avec adresse IP statique ne sont pas prises en charge.
>
>

## <a name="test-hello-deployment"></a>Déploiement de test hello
planification de votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération composé de plusieurs machines virtuelles et exécuter un test de basculement pour hello tootest.  

Il simule votre mécanisme de basculement et de récupération dans un réseau isolé. Notez les points suivants :

* Si vous souhaitez tooconnect toohello machine virtuelle Azure à l’aide du Bureau à distance après le basculement de hello, activer la connexion Bureau à distance sur l’ordinateur virtuel de hello avant d’exécuter le test de basculement hello.
* Après le basculement, vous utilisez un toohello de tooconnect adresse IP publique Azure VM à l’aide du Bureau à distance. Si vous voulez toodo, assurez-vous que vous n’avez pas les stratégies de domaine qui vous empêchent de connexion tooa machine virtuelle une adresse publique.

> [!NOTE]
> tooget hello meilleures performances lorsque vous basculez tooAzure, assurez-vous que vous avez installé hello agent Azure sur hello machine virtuelle. Cela permet d’accélérer le démarrage et facilite la résolution des problèmes. Télécharger hello [agent Linux](https://github.com/Azure/WALinuxAgent), ou hello [agent Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="create-a-recovery-plan"></a>Créer un plan de récupération
1. Sur hello **les Plans de récupération** onglet, ajoutez un nouveau plan. Spécifiez un nom, **VMM** dans **type de Source de**et serveur VMM source hello dans **Source**. cible de Hello sera Azure.

    ![Créer un plan de récupération](./media/site-recovery-vmm-to-azure-classic/recovery-plan1.png)
2. Bonjour **sélectionner des Machines virtuelles** page, le plan de récupération des machines virtuelles sélectionnez tooadd toohello. Ces machines virtuelles sont ajoutés de groupe par défaut de plans de récupération toohello : groupe 1. Un maximum de 100 machines virtuelles dans un même plan de récupération ont été testées.

* Si vous souhaitez que les propriétés d’une machine virtuelle tooverify hello avant de les ajouter toohello plan, cliquez sur machine virtuelle de hello sur hello page de propriétés hello cloud dans lequel elle se trouve. Vous pouvez également configurer les propriétés d’une machine virtuelle hello dans la console VMM hello.
* Tous les ordinateurs virtuels hello affichées ont été activées pour la protection. liste de Hello inclut les deux ordinateurs virtuels qui sont activés pour la protection et la réplication initiale est terminée, et ceux qui sont activés pour la protection avec réplication initiale en attente. Seules les machines virtuelles avec réplication initiale terminée peuvent basculer dans le cadre d'un plan de récupération.

    ![Créer un plan de récupération](./media/site-recovery-vmm-to-azure-classic/select-rp.png)

Une fois un plan de récupération a été créé, il apparaît dans hello **les Plans de récupération** onglet. Vous pouvez également ajouter [runbooks Azure automation](site-recovery-runbook-automation.md) actions de tooautomate de plan de récupération toohello pendant le basculement.

### <a name="run-a-test-failover"></a>Exécution d’un test de basculement
Il existe deux façons toorun un tooAzure de basculement de test.

* **Test de basculement sans réseau Azure**: ce type de test de basculement vérifie que l’ordinateur virtuel hello s’affiche correctement dans Azure. ordinateur virtuel de Hello n’est pas connecté tooany réseau Azure après le basculement.
* **Test de basculement avec un réseau Azure**: ce type de basculement vérifie que hello l’environnement de réplication se présente comme prévu et qui ont échoué sur les ordinateurs virtuels de hello sera connecté toohello réseau Azure cible de spécifié. Pour la gestion des sous-réseaux, pour le test de basculement sous-réseau hello d’ordinateur virtuel de test hello sera déterminé en basée sur le sous-réseau hello de machine virtuelle de réplication hello. Il s’agit de la réplication tooregular différents lorsque sous-réseau hello d’une machine virtuelle de réplication est basée sur le sous-réseau hello de machine virtuelle de hello source.

Si vous souhaitez toorun un test de basculement pour un ordinateur virtuel activé pour la protection tooAzure sans spécifier un réseau cible Azure vous n’avez pas besoin tooprepare quoi que ce soit. toorun un test de basculement avec une réseau Azure, vous devez toocreate un réseau Azure isolé de votre réseau de production Azure (comportement par défaut lorsque vous créez un nouveau réseau dans Azure) de la cible. Examiner le trop[exécuter un test de basculement](site-recovery-failover.md) pour plus d’informations.

Vous devez également tooset infrastructure de hello pour toowork de machine virtuelle hello répliquée comme prévu. Par exemple, un ordinateur virtuel avec le contrôleur de domaine et DNS peut être répliquée tooAzure à l’aide d’Azure Site Recovery et peuvent être créé dans le réseau de test hello à l’aide de Test de basculement. Consultez la rubrique [Considérations relatives au test de basculement](site-recovery-active-directory.md#test-failover-considerations) pour plus de détails.

toorun un test de basculement hello suivant :

1. Sur hello **les Plans de récupération** , sélectionnez le plan de hello et cliquez sur **Test de basculement**.
2. Sur hello **confirmer le Test de basculement** page Sélectionnez **aucun** ou un réseau Azure spécifique.  Notez que si vous sélectionnez aucun test de basculement hello sera Vérifiez que hello machine virtuelle répliquée correctement tooAzure mais ne vérifie pas votre configuration réseau de réplication.

    ![Pas de réseau](./media/site-recovery-vmm-to-azure-classic/test-no-network.png)
3. Si le chiffrement des données est activé pour le cloud de hello, dans **clé de chiffrement** certificat hello select qui a été émis lors de l’installation de hello fournisseur sur le serveur VMM de hello, quand vous avez activé hello option tooenable cryptage des données pour un cloud .
4. Sur hello **travaux** onglet, vous pouvez suivre la progression du basculement. Vous devez également être toosee en mesure de test de réplica d’un ordinateur virtuel d’hello Bonjour portail Azure. Si vous êtes configuré tooaccess ordinateurs virtuels à partir de votre réseau local, vous pouvez lancer une machine virtuelle de bureau à distance connexion toohello.
5. Lorsque le basculement de hello atteint hello **test complet** de phase, cliquez sur **effectuer le Test** toofinish il. Vous pouvez descendre toohello **travail** onglet progression du basculement tootrack et état et tooperform toutes les actions qui sont nécessaires.
6. Après le basculement, vous pouvez voir le réplica de test de machine virtuelle hello Bonjour portail Azure. Si vous êtes configuré tooaccess ordinateurs virtuels à partir de votre réseau local, vous pouvez lancer une machine virtuelle de bureau à distance connexion toohello. Hello suivant :

   1. Vérifiez que les ordinateurs virtuels hello démarrer correctement.
   2. Si vous souhaitez tooconnect toohello machine virtuelle Azure à l’aide du Bureau à distance après le basculement de hello, activer la connexion Bureau à distance sur l’ordinateur virtuel de hello avant d’exécuter le test de basculement hello. Vous devez également tooadd un point de terminaison RDP sur l’ordinateur virtuel de hello. Vous pouvez exploiter une [Runbooks d’automatisation Azure](site-recovery-runbook-automation.md) toodo qui.
   3. Après un basculement, si vous utilisez un ordinateur virtuel toohello de publique IP adresse tooconnect dans Azure à l’aide du Bureau à distance, assurez-vous de qu'avoir ne toutes les stratégies de domaine qui empêchent la connexion de la machine virtuelle de tooa à l’aide d’une adresse publique.
7. Effectuez l’issue du test de hello hello suivant :

   * Cliquez sur **hello test de basculement est terminé**. Nettoyage hello power de tooautomatically d’environnement de test désactiver et supprimer des machines virtuelles de test hello.
   * Cliquez sur **Notes** toorecord enregistrer toutes les observations associées au basculement de test hello.


## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur la [configuration des plans de récupération](site-recovery-create-recovery-plans.md) et sur le [basculement](site-recovery-failover.md).
