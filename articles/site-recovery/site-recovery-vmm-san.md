---
title: "aaaReplicate machines virtuelles de Hyper-V dans VMM avec le réseau SAN à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit comment virtuels tooreplicate Hyper-V entre deux sites avec Azure Site Recovery à l’aide de la réplication SAN."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: cee4ff519a8e9e7f29e17e923a9533fb339634b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-tooa-secondary-site-with-azure-site-recovery-by-using-san"></a>Répliquer les machines virtuelles de Hyper-V dans le site secondaire tooa clouds VMM avec Azure Site Recovery à l’aide de SAN


Utilisez cet article si vous souhaitez toodeploy [Azure Site Recovery](site-recovery-overview.md) toomanage la réplication de machines virtuelles de Hyper-V (managé dans des clouds System Center Virtual Machine Manager) tooa site VMM secondaire, à l’aide d’Azure Site Recovery dans le portail classique de hello. Ce scénario n’est pas disponible dans le nouveau portail de Azure hello.



Valider des commentaires à la fin de hello de cet article. Obtenir des réponses aux questions de tootechnical Bonjour [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="why-replicate-with-san-and-site-recovery"></a>Pourquoi effectuer une réplication avec SAN et Site Recovery ?

* Réseau SAN fournit une solution de réplication au niveau de l’entreprise, évolutif afin qu’un site principal contenant avec SAN Hyper-V peut répliquer le site secondaire de numéros d’unités logiques tooa avec SAN. Le stockage géré par VMM, et la réplication et le basculement sont orchestrés avec Site Recovery.
* Récupération de site a collaboré avec plusieurs [partenaires de stockage SAN](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx) tooprovide la réplication sur le stockage Fibre Channel et iSCSI.  
* Utilisez votre SAN infrastructure tooprotect critiques applications existantes déployées dans des clusters Hyper-V. Les machines virtuelles peuvent être répliquées en tant que groupe afin que les applications multiniveaux puissent être basculées régulièrement.
* La réplication SAN garantit la cohérence de la réplication entre les différentes couches d’une application avec réplication synchronisée pour un RTO et une RPO faibles, et une réplication asynchronisée pour une haute flexibilité, selon les capacités de votre groupe de stockage.  
* Vous pouvez gérer le stockage SAN dans hello ensemble fibre optique VMM et utiliser SMI-S dans un stockage existant toodiscover VMM.  

Notez les points suivants :
- Réplication de site à site avec SAN n’est pas disponible dans hello portail Azure. Il est uniquement disponible dans le portail classique de hello. Impossible de créer des coffres dans le portail classique de hello. Les coffres existants peuvent être conservés.
- La réplication SAN tooAzure n’est pas pris en charge.
- Vous ne pouvez pas répliquer des fichiers vhdx partagés, ou des unités logiques (LUN) qui sont directement connectés tooVMs via iSCSI ou Fibre Channel. Les clusters invités peuvent être répliqués.


## <a name="architecture"></a>Architecture

![Architecture SAN](./media/site-recovery-vmm-san/architecture.png)

- **Azure**: configurer un coffre Bonjour portail Azure Site Recovery.
- **Le stockage SAN**: stockage SAN est géré dans hello ensemble fibre optique VMM. Vous ajoutez le fournisseur de stockage hello, créez des classifications de stockage et configurez des pools de stockage.
- **VMM et Hyper-V** : nous recommandons un serveur VMM sur chaque site. Définissez des clouds privés VMM et placez des clusters Hyper-V dans ces clouds. Au cours du déploiement, hello fournisseur Azure Site Recovery est installé sur chaque serveur VMM et serveur de hello est inscrit dans le coffre hello. Hello fournisseur communique avec réplication toomanage hello du service de récupération de Site, le basculement et la restauration automatique.
- **Réplication**: après avoir configuré le stockage dans VMM et configurer la réplication de la récupération de Site, la réplication a lieu entre hello principaux et secondaire un stockage SAN. Aucune donnée de réplication n’est envoyée tooSite récupération.
- **Basculement**: activer le basculement dans le portail Site Recovery hello. Il n’y a aucune perte de données pendant le basculement, car la réplication est synchrone.
- **La restauration automatique**: toofail précédent, vous activez les modifications delta de la réplication inverse tootransfer de hello secondaire toohello site principal. Une fois la réplication inverse est terminée, vous exécutez un basculement planifié tooprimary secondaire. Ce basculement planifié arrête le réplica hello machines virtuelles sur le site secondaire de hello et les démarre sur le site principal de hello.


## <a name="before-you-start"></a>Avant de commencer


**Configuration requise** | **Détails**
--- | ---
**Microsoft Azure** |Vous avez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) . Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/). [En savoir plus](https://azure.microsoft.com/pricing/details/site-recovery/) sur la tarification Site Recovery. Créer un tooconfigure du coffre Azure Site Recovery et gérer la réplication et basculement.
**VMM** | Vous pouvez utiliser un seul serveur VMM et répliquer entre des clouds différents, mais nous vous recommandons d’un VMM site principal de hello et un site secondaire de hello. Un VMM peut être déployé comme serveur autonome physique ou virtuel, ou en tant que cluster. <br/><br/>serveur VMM de Hello doit exécuter System Center 2012 R2 ou version ultérieure avec hello dernières mises à jour cumulatives.<br/><br/> Vous avez besoin d’au moins un cloud configuré sur le serveur VMM principal hello souhaité tooprotect et un cloud configuré sur le serveur VMM secondaire de hello souhaité toouse pour le basculement.<br/><br/> cloud de Hello source doit contenir un ou plusieurs groupes d’hôtes VMM.<br/><br/> Tous les clouds VMM doivent avoir le profil de capacité de Hyper-V hello.<br/><br/> Pour plus d’informations sur la configuration des clouds VMM, consultez [Déployer un cloud de machine virtuelle privé](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview).
**Hyper-V** | Vous devez avoir un ou plusieurs clusters Hyper-V dans les clouds VMM principaux et secondaires.<br/><br/> cluster d’Hyper-V Hello source doit contenir un ou plusieurs ordinateurs virtuels.<br/><br/> groupes d’hôtes VMM Hello dans les sites principaux et secondaires hello doivent contenir au moins un des clusters Hyper-V de hello.<br/><br/>Hello hôte et cible les serveurs Hyper-V doivent exécuter Windows Server 2012 ou installé une version ultérieure avec Hyper-V de hello rôle et hello dernières mises à jour.<br/><br/> Si vous utilisez Hyper-V dans un cluster et avez un cluster basé sur des adresses IP statiques, le service Broker du cluster n’est pas créé automatiquement. Vous devez le configurer manuellement. Pour plus d’informations, consultez [Préparation des clusters hôtes pour un réplica Hyper-V](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters).
**Stockage SAN** | Vous pouvez répliquer des machines virtuelles en cluster invité avec un stockage iSCSI ou Fibre Channel, ou bien à l’aide de disques durs virtuels partagés (VHDX).<br/><br/> Vous avez besoin de deux groupes SAN : un dans le site principal de hello et un hello dans un site secondaire.<br/><br/> Une infrastructure réseau doit être configurée entre les tableaux hello. L'homologation et la réplication doivent être configurées. Les licences de réplication doivent être configurés conformément aux exigences de baie de stockage hello.<br/><br/>Configurer le réseau entre les serveurs hôtes de hello Hyper-V et la baie de stockage hello afin que les hôtes peuvent communiquer avec les numéros d’unités logiques de stockage à l’aide d’iSCSI ou Fibre Channel.<br/><br/> Consultez la liste des [groupes de stockage pris en charge](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx).<br/><br/> Les fournisseurs SMI-S provenant de fabricants de baie de stockage doivent être installés, et des groupes SAN hello doivent être gérées par le fournisseur de hello. Définir des instructions toomanufacturer conséquente hello fournisseur.<br/><br/>Assurez-vous que le fournisseur SMI-S de ce tableau hello est sur un serveur que VMM hello serveur peut accéder via le réseau hello avec une adresse IP ou le nom de domaine complet.<br/><br/> Chaque groupe SAN doit posséder un ou plusieurs pools de stockage disponibles.<br/><br/> serveur VMM principal que Hello doit gérer le groupe principal de hello et serveur VMM secondaire de hello doit gérer le groupe secondaire de hello.
**Mappage réseau** | Configurer le mappage réseau afin que les machines virtuelles répliquées sont placées de façon optimale sur des serveurs hôtes Hyper-V secondaire après le basculement, et pour qu’ils soient connectés tooappropriate réseaux d’ordinateurs virtuels. Si vous ne configurez pas le mappage réseau, machines virtuelles de réplica sera connecté tooany réseau après le basculement.<br/><br/> Assurez-vous que les réseaux VMM sont configurés correctement, afin de pouvoir configurer le mappage réseau lors du déploiement de Site Recovery. Dans VMM, hello machines virtuelles sur un ordinateur hôte Hyper-V hello source doit être connecté tooa réseau de VMM VM. Ce réseau doit être lié tooa réseau logique associé au cloud de hello.<br/><br/> cloud cible de Hello doit avoir un réseau d’ordinateurs virtuels correspondant et il doit à son tour être lié tooa réseau logique correspondant associé au cloud cible de hello.<br/><br/>.

## <a name="step-1-prepare-hello-vmm-infrastructure"></a>Étape 1 : Préparer l’infrastructure VMM hello
tooprepare votre infrastructure VMM, vous devez :

1. vérifier les clouds VMM ;
2. intégrer et classer le stockage SAN dans VMM ;
3. créer des LUN et allouer de l’espace de stockage ;
4. créer des groupes de réplication ;
5. configurer les réseaux de machines virtuelles.

### <a name="verify-vmm-clouds"></a>Vérifier les clouds VMM

Vérifiez que vos clouds VMM sont configurés correctement avant de commencer le déploiement de Site Recovery.

### <a name="integrate-and-classify-san-storage-in-hello-vmm-fabric"></a>Intégrez et Classifiez le stockage SAN dans hello ensemble fibre optique VMM

1. Dans la console VMM hello, accédez trop**l’ensemble fibre optique** > **stockage** > **ajouter des ressources** > **lesdispositifsdestockage**.
2. Bonjour **ajouter des périphériques de stockage** Assistant, sélectionnez **sélectionner un type de fournisseur de stockage** et sélectionnez **périphériques SAN et NAS détectés et gérés par un fournisseur SMI-S**.

    ![Type de fournisseur](./media/site-recovery-vmm-san/provider-type.png)

3. Sur hello **spécifier le protocole et l’adresse du fournisseur de stockage SMI-S de hello** page, sélectionnez **CIMXML SMI-S** et spécifiez les paramètres de hello pour connexion toohello fournisseur.
4. Dans **adresse IP du fournisseur ou le nom de domaine complet** et **port TCP/IP**, spécifiez les paramètres de hello pour connexion toohello fournisseur. Vous pouvez uniquement utiliser une connexion SSL pour CIMXML SMI-S.

    ![Connexion au fournisseur](./media/site-recovery-vmm-san/connect-settings.png)
5. Dans **compte d’identification**, spécifiez un compte d’identification VMM qui peut accéder au fournisseur de hello, ou créer un compte.
6. Sur hello **collecter des informations** page, VMM essaie automatiquement les informations de périphérique de stockage hello toodiscover et l’importation. détection de tooretry, cliquez sur **analyser le fournisseur**. Si le processus de découverte hello réussit, hello découvert de baies de stockage, pools de stockage, fabricant, modèle et la capacité sont répertoriés sur la page de hello.

    ![Détecter le stockage](./media/site-recovery-vmm-san/discover.png)
7. Dans **tooplace de pools de stockage sous administration de sélectionner et affecter une classification**, sélectionnez les pools de stockage hello que VMM gère et affectez-leur une classification. Numéro d’unité logique est importée à partir de pools de stockage hello. Créez des LUN basés sur les applications hello vous devez tooprotect, leurs besoins en capacité et vos besoins pour connaître la tooreplicate ensemble.

    ![Classifier le stockage](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a>Créer des LUN et allouer de l'espace de stockage

Créez des LUN basés sur les applications hello vous devez tooprotect, les besoins en capacité et vos besoins pour connaître la tooreplicate ensemble.

1. Une fois le stockage de hello s’affiche dans hello structure VMM, vous pouvez [configurer des numéros d’unités logiques](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm).

     > [!NOTE]
     > Ne pas ajouter des disques durs virtuels pour hello machine virtuelle qui sont activées pour la réplication tooLUNs. Si ces LUN ne font pas partie d’un groupe de réplication Site Recovery, elles ne seront pas détectées par Site Recovery.
     >

2. Allouez le cluster hôte Hyper-V stockage capacité toohello afin que VMM puisse déployer stockage toohello mis en service des données machine virtuelle :

   * Avant l’allocation de cluster toohello de stockage, vous devez tooallocate il toohello groupe d’hôtes VMM sur le hello cluster réside. Pour plus d’informations, consultez [comment tooa d’unités logiques de stockage tooallocate héberger le groupe dans VMM](https://technet.microsoft.com/library/gg610686.aspx) et [comment tooallocate stockage regroupe le groupe hôte de tooa dans VMM](https://technet.microsoft.com/library/gg610635.aspx).
   * Allocation de cluster de toohello de capacité de stockage comme décrit dans [comment de cluster de stockage tooconfigure sur un ordinateur hôte Hyper-V dans VMM](https://technet.microsoft.com/library/gg610692.aspx).

    ![Type de fournisseur](./media/site-recovery-vmm-san/provider-type.png)
3. Dans **spécifier le protocole et l’adresse du fournisseur de stockage SMI-S de hello**, sélectionnez **CIMXML SMI-S**. Spécifiez les paramètres de hello pour la connexion toohello fournisseur. Vous pouvez uniquement utiliser une connexion SSL pour CIMXML SMI-S.

    ![Connexion au fournisseur](./media/site-recovery-vmm-san/connect-settings.png)
4. Dans **compte d’identification**, spécifiez un compte d’identification VMM qui peut accéder au fournisseur de hello, ou créer un compte.
5. Dans **collecter des informations**, VMM essaie automatiquement les informations de périphérique de stockage hello toodiscover et l’importation. Si vous avez besoin de tooretry, cliquez sur **analyser le fournisseur**. Lorsque le processus de découverte hello réussit, les baies de stockage hello, capacité, fabricant, modèle et pools de stockage sont répertoriés sur la page de hello.

    ![Détecter le stockage](./media/site-recovery-vmm-san/discover.png)
7. Dans **tooplace de pools de stockage sous administration de sélectionner et affecter une classification**, sélectionnez les pools de stockage hello que VMM gère et affectez-leur une classification. Numéro d’unité logique est importée à partir de pools de stockage hello.

    ![Classifier le stockage](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a>Créer des groupes de réplication

Créer un groupe de réplication qui inclut toutes les unités logiques hello qui devront tooreplicate ensemble.

1. Dans la console VMM hello, ouvrez hello **groupes de réplication** onglet des propriétés du tableau de stockage hello, puis cliquez sur **nouveau**.
2. Créer un groupe de réplication hello.

    ![Groupe de réplication SAN](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a>Configurer des réseaux

Si vous souhaitez que le mappage réseau tooconfigure, hello suivant :

1. Consultez Mappage réseau de Site Recovery.
2. Préparez les réseaux de machines virtuelles dans VMM :

   * [Configurez les réseaux logiques](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks).
   * [Configurez les réseaux de machines virtuelles](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks).


## <a name="step-2-create-a-vault"></a>Étape 2 : Créer un coffre

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) d’un serveur VMM hello souhaité tooregister dans le coffre hello.
2. Développez **Data Services** > **Recovery Services**, puis cliquez sur **Coffre Site Recovery**.
3. Cliquez sur **Créer nouveau** > **Création rapide**.
4. Dans **nom**, entrez un coffre de hello tooidentify nom convivial.
5. Dans **région**, sélectionnez hello région géographique pour le coffre hello. les régions toocheck pris en charge, consultez [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Cliquez sur **Create vault**.

    ![Nouveau coffre](./media/site-recovery-vmm-san/create-vault.png)

Vérifiez tooconfirm de barre d’état hello qui hello coffre a été créé avec succès. Hello est répertorié en tant que **Active** sur hello principal **Services de récupération** page.

### <a name="register-hello-vmm-servers"></a>Inscrire les serveurs VMM de hello

1. Ouvrez hello **Quick Start** page à partir de hello **Services de récupération** page. Démarrage rapide peut également être ouvert à tout moment en sélectionnant l’icône de hello.

    ![Icône Quick Start](./media/site-recovery-vmm-san/quick-start-icon.png)
2. Dans la zone de liste déroulante hello, sélectionnez **entre Hyper-V local à l’aide de la réplication de site**.

    ![Clé d’enregistrement](./media/site-recovery-vmm-san/select-san.png)
3. Dans **serveurs VMM de préparer**, téléchargez la version la plus récente du fichier d’installation fournisseur Azure Site Recovery hello hello.
4. Exécuter ce fichier sur le serveur VMM de hello source. Si VMM est déployé dans un cluster et que vous installez hello fournisseur pour hello première fois, installez hello fournisseur sur un nœud actif et terminer hello installation tooregister hello serveur VMM dans le coffre hello. Installez hello fournisseur sur hello autres nœuds. Si vous mettez à niveau hello fournisseur, vous devez tooupgrade sur tous les nœuds afin qu’ils ont hello même version du fournisseur.
5. programme d’installation de l’Hello vérifie la configuration requise et les demandes autorisation toostop hello le programme d’installation VMM service toobegin fournisseur. service de Hello redémarre automatiquement lorsque le programme d’installation se termine. Sur un cluster VMM, vous pourrez le rôle de Cluster invité à toostop hello.
6. Dans **Microsoft Update**, vous pouvez la choisir des mises à jour et mises à jour du fournisseur seront installés en fonction de stratégie de tooyour Microsoft Update.

    ![Mises à jour Microsoft](./media/site-recovery-vmm-san/ms-update.png)

7. Par défaut, hello hello fournisseur est installé <SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin. Cliquez sur **installer** toobegin.

    ![Emplacement d’installation](./media/site-recovery-vmm-san/install-location.png)

8. Une fois hello fournisseur est installé, cliquez sur **inscrire** serveur VMM tooregister hello dans le coffre hello.

    ![Installation terminée](./media/site-recovery-vmm-san/install-complete.png)

9. Dans **connexion Internet**, indiquez comment hello fournisseur connecte toohello Internet. Sélectionnez **utiliser les paramètres du proxy système par défaut** si vous souhaitez que les paramètres de connexion Internet toouse hello par défaut sur le serveur de hello.

    ![Paramètres Internet](./media/site-recovery-vmm-san/proxy-details.png)

   * Si vous voulez toouse un proxy personnalisé, installez-le avant d’installer le fournisseur de hello. Lorsque vous configurez les paramètres de proxy personnalisés, un test s’exécute de connexion au proxy toocheck hello.
   * Si vous n’utilisez pas un proxy personnalisé, ou si votre proxy par défaut nécessite une authentification, vous devez entrer les détails du proxy hello, y compris le port et l’adresse de hello.
   * Hello requis Qu'url doivent être accessibles depuis le serveur VMM de hello.
   * Si vous utilisez un proxy personnalisé, un compte d’identification VMM (DRAProxyAccount) est automatiquement créé à l’aide de hello spécifié les informations d’identification de proxy. Configurer le serveur de proxy hello afin que ce compte peut authentifier. Vous pouvez modifier hello exécuter en tant que paramètres de compte dans la console VMM hello (**paramètres** > **sécurité** > **comptes d’identification**  >  **DRAProxyAccount**). Vous devez redémarrer le service VMM hello pour modifier un effet de tootake hello.
10. Dans **clé d’inscription**, sélectionnez clé hello que vous avez téléchargé depuis le serveur VMM de portail et copié toohello hello.
11. Dans **nom du coffre**, vérifier nom hello de coffre hello dans le hello serveur sera inscrit.

    ![Enregistrement du serveur](./media/site-recovery-vmm-san/vault-creds.png)
12. paramètre de chiffrement Hello est uniquement utilisé pour la réplication tooAzure VMM. Vous pouvez l’ignorer.

    ![Enregistrement du serveur](./media/site-recovery-vmm-san/encrypt.png)
13. Dans **nom du serveur**, spécifiez un serveur VMM à hello tooidentify nom convivial dans le coffre hello. Dans une configuration de cluster, spécifiez le nom de rôle de cluster VMM hello.
14. Dans **synchronisation initiale des métadonnées cloud**, sélectionnez si vous souhaitez toosynchronize métadonnées pour tous les clouds sur le serveur VMM de hello. Cette action ne doit toohappen qu’une seule fois sur chaque serveur. Si vous ne souhaitez pas toosynchronize tous les clouds, vous pouvez laisser ce paramètre désactivé et synchroniser chaque cloud individuellement dans les propriétés du cloud hello dans la console VMM hello.

    ![Enregistrement du serveur](./media/site-recovery-vmm-san/friendly-name.png)

15. Cliquez sur **suivant** processus de hello toocomplete. Après l’inscription, les métadonnées d’un serveur hello VMM sont récupérées par Azure Site Recovery. Hello serveur s’affiche dans **serveurs** > **serveurs VMM** dans le coffre hello.

### <a name="command-line-installation"></a>Installation avec une ligne de commande

Hello fournisseur Azure Site Recovery peut également être installé à l’aide de hello suivant la ligne de commande. Cette méthode peut être le fournisseur de hello tooinstall utilisés sur Server Core de Windows Server 2012 R2.

1. Téléchargez hello fournisseur de fichiers et d’enregistrement clé tooa dossier d’installation. par exemple, C:\ASR.
2. Arrêter le service VMM hello.
3. Extrayez le programme d’installation du fournisseur hello. En tant qu’administrateur, exécutez les commandes suivantes :

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Installez hello fournisseur :

        C:\ASR> setupdr.exe /i
5. Inscrire hello fournisseur :

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Paramètres :

* **/ Informations d’identification**: paramètre requis pour l’emplacement hello dans le hello se trouve le fichier de clé d’inscription.  
* **/ FriendlyName**: un paramètre obligatoire pour le nom hello du serveur hôte hello Hyper-V qui s’affiche dans le portail Azure Site Recovery hello.
* **/ EncryptionEnabled**: paramètre facultatif utilisé uniquement lors de la réplication à partir de VMM tooAzure.
* **/ProxyAddress**: paramètre facultatif qui spécifie l’adresse hello du serveur de proxy hello.
* **/ProxyPort**: paramètre optionnel qui spécifie le port du serveur proxy de hello hello.
* **/proxyUsername**: paramètre facultatif qui spécifie le nom d’utilisateur proxy hello (si le proxy de hello exige une authentification).
* **/proxyPassword**: paramètre facultatif qui spécifie le mot de passe hello pour l’authentification avec le serveur de proxy hello (si le proxy de hello exige une authentification).

## <a name="step-3-map-storage-arrays-and-pools"></a>Étape 3 : Mapper les groupes et pools de stockage

Mapper toospecify tableaux principaux et secondaires un pool de stockage secondaire qui reçoit les données de réplication à partir du pool principal de hello. Mapper le stockage avant de configurer la réplication, car les informations de mappage hello sont utilisées lorsque vous activez la protection des groupes de réplication.

Avant de commencer, vérifiez que les clouds VMM apparaissent dans le coffre hello. Clouds sont détectées lors de la synchronisation de tous les clouds lors de l’installation du fournisseur ou lorsque vous synchronisez un cloud spécifique dans la console VMM hello.

1. Cliquez sur **Ressources** > **Stockage serveur** > **Mapper les baies de stockage source et cible**.
    ![Inscription du serveur](./media/site-recovery-vmm-san/storage-map.png)

2. Sélectionnez les groupes de stockage hello sur le site principal de hello et mapper les baies toostorage sur le site secondaire de hello. Dans **Pools de stockage**, sélectionnez une source et cible toomap de pool de stockage.

    ![Enregistrement du serveur](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a>Étape 4 : Configurer les paramètres de réplication

Une fois les serveurs VMM inscrits, configurez les paramètres de protection de cloud.

1. Sur hello **Quick Start** , cliquez sur **configurer la protection pour les clouds VMM**.
2. Sur hello **éléments protégés** , sélectionnez le cloud de hello **Configuration**.
3. Dans **Cible**, sélectionnez **VMM**.
4. Dans **emplacement cible**, sélectionnez serveur hello VMM qui gère le cloud hello toouse souhaité pour la récupération.
5. Dans **cloud cible**, sélectionnez hello cible cloud toouse pour le basculement de la machine virtuelle.
   * Nous vous recommandons de sélectionner un cloud cible qui répond aux exigences de récupération pour les ordinateurs virtuels de hello que vous protégez.
   * Un cloud ne peut appartenir paire de cloud unique tooa--primaire ou un cloud cible.
6. Récupération de site vérifie que les clouds ont accès tooSAN stockage et que le stockage hello tableaux sont mappés.
7. Si la vérification aboutit, sélectionnez **SAN** dans **Type de réplication**.

Après avoir enregistré les paramètres de hello, un travail est créé qui peuvent être surveillés sur hello **travaux** onglet. Paramètres peuvent être modifiés sur hello **configurer** onglet. Si vous souhaitez l’emplacement cible de hello toomodify ou le cloud cible, vous devez supprimer la configuration du cloud hello et puis reconfigurez hello cloud.

## <a name="step-5-enable-network-mapping"></a>Étape 5 : Activer le mappage réseau

1. Sur hello **Quick Start** , cliquez sur **mapper les réseaux**.
2. Sélectionnez le serveur VMM de hello source, puis hello hello cible VMM server toowhich réseaux seront mappés. liste Hello des réseaux source et de leurs réseaux cibles associés sont affichés. Les réseaux non mappés n’affichent aucune valeur. Cliquez sur hello informations icône suivant toohello source et cible noms tooview hello sous-réseaux du réseau pour chaque réseau.
3. Sélectionnez un réseau dans **Réseau sur la source**, puis cliquez sur **Mapper**. service de Hello détecte les réseaux d’ordinateurs virtuels hello sur le serveur cible de hello et les affiche.

    ![Architecture SAN](./media/site-recovery-vmm-san/network-map1.png)
4. Sélectionnez un des réseaux d’ordinateurs virtuels hello à partir du serveur VMM de hello cible.

    ![Architecture SAN](./media/site-recovery-vmm-san/network-map2.png)

5. Lorsque vous sélectionnez un réseau cible, hello clouds protégés qui utilisent le réseau source de hello sont affichés. Les réseaux cibles disponibles sont également affichés. Nous vous recommandons de sélectionner un réseau cible disponible tooall des clouds hello que vous utilisez pour la réplication.
6. Cliquez sur le processus de mappage hello coche toocomplete hello. Une tâche de suivi de la progression commence. Vous pouvez l’afficher sur hello **travaux** onglet.

## <a name="step-6-enable-replication-for-replication-groups"></a>Étape 6 : activer la réplication des groupes de réplication

Vous pouvez activer la protection pour les ordinateurs virtuels, vous devez tooenable la réplication pour les groupes de réplication de stockage.

1. Sur hello **propriétés** page de hello le cloud principal dans le portail Site Recovery hello, ouvrez hello **virtuels** onglet et cliquez sur **ajouter un groupe de réplication**.
2. Sélectionnez un ou plusieurs VMM groupes de réplication qui sont associés au cloud de hello, vérifiez les tableaux source et cible hello et spécifiez la fréquence de réplication hello.

Récupération de site, VMM et les fournisseurs SMI-S de hello configurer des numéros d’unités logiques de stockage du site hello cible et activer la réplication de stockage. Si le groupe de réplication hello est déjà répliqué, Site Recovery réutilise la relation de réplication existante hello et mises à jour hello plus d’informations.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Étape 7 : Activation de la protection des machines virtuelles


Lorsqu’un groupe de stockage réplique, activez la protection des ordinateurs virtuels dans la console VMM hello avec l’une des méthodes suivantes de hello :

* **Machine virtuelle**: lorsque vous créez une machine virtuelle, activer la réplication et associer hello VM de groupe de réplication hello.
  Avec cette option, VMM utilise le stockage de machine virtuelle de la sélection élective intelligente toooptimally place hello sur LUN hello hello du groupe de réplication. Site Recovery orchestre la création d’une machine virtuelle sur le site secondaire de hello ombre hello et alloue de la capacité afin que les machines virtuelles de réplica peuvent être démarrés après le basculement.
* **Machine virtuelle existante**: si un ordinateur virtuel est déjà déployé dans VMM, vous pouvez activer la réplication et l’exécution d’un groupe de réplication de stockage migration tooa. Après la saisie semi-automatique, VMM et Site Recovery détecter hello du nouvel ordinateur virtuel et commencer à le gérer en mode de récupération de Site. Un cliché instantané de machine virtuelle est créée sur le site secondaire de hello et capacité allouée afin que le réplica hello machine virtuelle peut être démarré après le basculement.

![Activer la protection](./media/site-recovery-vmm-san/enable-protect.png)

Une fois les machines virtuelles activées pour la réplication, ils apparaissent dans la console de récupération de Site hello. Vous pouvez afficher les propriétés des machines virtuelles, suivre leur état et suivre le basculement des groupes de réplication contenant plusieurs machines virtuelles. Dans le cadre de la réplication SAN, toutes les machines virtuelles associées à un groupe de réplication doivent basculer ensemble. Il s’agit, car le basculement se produit au niveau de la couche de stockage hello en premier. Il est important toogroup votre réplication regroupe correctement et placez uniquement les machines virtuelles associées ensemble.

> [!NOTE]
> Une fois que vous avez activé la réplication pour une machine virtuelle, n’ajoutez pas son tooLUNs de disques durs virtuels, sauf si elles se trouvent dans un groupe de réplication de Site Recovery. Les disques durs virtuels seront détectés par Site Recovery uniquement s’ils font partie d’un groupe de réplication Site Recovery.
>
>

Vous pouvez suivre la progression, y compris la réplication initiale hello, sur hello **travaux** onglet. Après l’exécution du travail de finaliser la Protection hello, ordinateur virtuel de hello est prêt pour le basculement.

![Tâche de protection de la machine virtuelle](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-hello-deployment"></a>Étape 8 : Tester le déploiement de hello

Tester votre déploiement toomake assurer que les ordinateurs virtuels échouent plus comme prévu. toodo, créez un plan de récupération et exécuter un test de basculement.

1. Sur hello **les Plans de récupération** , cliquez sur **créer un Plan de récupération**.
2. Spécifiez un nom pour le plan de récupération hello, puis sélectionnez les serveurs VMM source et cible. serveur de source de Hello doit avoir des machines virtuelles qui sont activés pour le basculement et la récupération. Sélectionnez **SAN** tooview uniquement cloud est configuré pour la réplication SAN.

    ![Créer un plan de récupération](./media/site-recovery-vmm-san/r-plan.png)

3. Dans **Sélectionner la machine virtuelle**, sélectionnez les groupes de réplication. Toutes les machines virtuelles associées au groupe de hello sont ajoutés de plan de récupération toohello. Ces machines virtuelles sont ajoutés groupe par défaut plans de récupération toohello (groupe 1). Vous pouvez ajouter d’autres groupes si nécessaire. Après la réplication, les machines virtuelles sont numérotées selon l’ordre de toohello des groupes de plan de récupération hello.

    ![Sélectionner les machines virtuelles](./media/site-recovery-vmm-san/r-plan-vm.png)
4. Une fois le plan de récupération hello est créé, il apparaît dans la liste hello sur hello **les Plans de récupération** onglet. Sélectionnez le plan de hello et choisissez **Test de basculement**.
5. Sur hello **confirmer le Test de basculement** page, sélectionnez **aucun**. Avec cette option activée, hello basculé de machines virtuelles de réplica n’est pas connecté tooany réseau. Ce test qui hello machines virtuelles basculent comme prévu, mais il ne teste pas environnement hello du réseau. Pour plus d’informations sur les autres options de mise en réseau, consultez [Basculement Site Recovery](site-recovery-failover.md).

    ![Sélectionner le réseau de test](./media/site-recovery-vmm-san/test-fail1.png)

6. machine virtuelle de test Hello est créée sur hello en tant qu’hôte hello sur quel réplica hello machine virtuelle existe le même hôte. Il n’est pas ajouté cloud toohello dans quels hello ordinateur virtuel de réplication se trouve.
2. Après la réplication, ordinateur virtuel de réplication hello aura une autre adresse IP de l’ordinateur virtuel principal hello. Si vous émettez des adresses à partir de DHCP, la mise à jour s’effectue automatiquement. Si vous n’utilisez pas DHCP et que vous souhaitez hello, même les adresses, vous devez toorun des scripts.
3. Exécutez cette adresse IP de script tooretrieve hello :

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. Exécutez cette tooupdate de script d’exemple DNS. Spécifier l’adresse hello que vous avez récupéré.

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez exécuté un toocheck de basculement de test de votre environnement fonctionne comme prévu, consultez [Site Recovery basculement](site-recovery-failover.md) toolearn sur différents types de basculement.
