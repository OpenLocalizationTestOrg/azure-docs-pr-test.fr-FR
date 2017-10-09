---
title: aaaReplicate machines virtuelles de Hyper-V dans VMM tooa site secondaire (Azure classic) | Documents Microsoft
description: "Cet article décrit comment des clouds de site VMM secondaire de tooa avec Azure Site Recovery tooreplicate des ordinateurs virtuels Hyper-V dans VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: fe551e1f741579044f540ea0e50a6e36d48133ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Réplication d’ordinateurs virtuels Hyper-V dans le site VMM secondaire VMM clouds tooa
> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-vmm-to-vmm.md)
> * [Portail classique](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Hello service Azure Site Recovery contribue tooyour continuité des activités et la stratégie de récupération d’urgence en orchestrant ces opérations de réplication, le basculement et récupération des ordinateurs virtuels et des serveurs physiques. Machines peuvent être répliquée tooAzure ou centre de données secondaire locale tooa. Pour avoir un rapide aperçu, consultez la section [Qu’est-ce qu’Azure Site Recovery ?](site-recovery-overview.md)

## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment virtuels tooreplicate Hyper-V sur Hyper-V hébergent les serveurs qui sont gérés dans VMM clouds toosecondary de site VMM à l’aide d’Azure Site Recovery.

article de Hello inclut les conditions préalables, vous montre comment installer le tooset d’un coffre Site Recovery, hello fournisseur Azure Site Recovery sur la source et les serveurs VMM ciblez, inscrire les serveurs de hello dans le coffre de hello, configurer les paramètres de protection pour les clouds VMM, puis activer protection des ordinateurs virtuels Hyper-V. Terminez en toomake de basculement de test hello que tout fonctionne comme prévu.

Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Architecture
image Hello ci-dessous montre les canaux de communication différentes hello et les ports utilisés par Azure Site Recovery pour l’orchestration et la réplication

![Topologie E2E](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Avant de commencer
Assurez-vous que les conditions préalables sont remplies :

| **Configuration requise** | **Détails** |
| --- | --- |
| **Microsoft Azure** |Vous avez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) . Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/). [En savoir plus](https://azure.microsoft.com/pricing/details/site-recovery/) sur la tarification Site Recovery. |
| **VMM** |Vous avez besoin d’au moins un serveur VMM.<br/><br/>serveur VMM de Hello doit exécuter au moins System Center 2012 SP1 hello dernières mises à jour cumulatives.<br/><br/>Si vous souhaitez tooset la protection avec un seul serveur VMM, vous devez au moins deux clouds configurés sur le serveur de hello.<br/><br/>Si vous souhaitez que la protection toodeploy avec deux serveurs VMM, chaque serveur doit avoir au moins un cloud configuré sur le serveur VMM principal hello vous voulez tooprotect et un cloud configuré sur le serveur VMM secondaire de hello souhaité toouse pour la protection et de récupération<br/><br/>Tous les clouds VMM doivent être profil de capacité hello Hyper-V.<br/><br/>cloud de source de Hello que vous souhaitez tooprotect doit contenir un ou plusieurs groupes d’hôtes VMM. |
| **Hyper-V** |Vous avez besoin d’un ou plusieurs serveurs hôtes Hyper-V dans des groupes de hôtes VMM principaux et secondaires des hello et un ou plusieurs ordinateurs virtuels sur chaque serveur hôte Hyper-V.<br/><br/>Hello des serveurs Hyper-V hôte et la cible doivent exécuter au moins Windows Server 2012 avec un rôle de hello Hyper-V et avez hello les dernières mises à jour installées.<br/><br/>N’importe quel serveur Hyper-V contenant des machines virtuelles que vous souhaitiez tooprotect doit se trouver dans un cloud VMM.<br/><br/>Si vous exécutez Hyper-V dans un cluster, notez que le service Broker de cluster n’est pas créé automatiquement si le cluster est basé sur des adresses IP statiques. Vous devez manuellement service broker de cluster tooconfigure hello. [En savoir plus](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) sur l’entrée de blog d’Aidan Finn. |
| **Mappage réseau** |Vous pouvez configurer toomake de mappage réseau assurer que les machines virtuelles répliquées sont placées de façon optimale sur des serveurs hôtes Hyper-V secondaire après le basculement, et qu’ils peuvent connecter des réseaux d’ordinateurs virtuels tooappropriate. Si vous ne configurez pas le mappage réseau, machines virtuelles de réplica sera connecté tooany réseau après le basculement.<br/><br/>tooset le mappage réseau pendant le déploiement, vous assurer que virtuels hello sur le serveur hôte de Hyper-V source hello sont connecté tooa réseau de VMM VM. Ce réseau doit être lié tooa réseau logique associé hello cloud. < br /<br/>cloud cible Hello hello serveur VMM secondaire que vous utilisez pour la récupération doit avoir un réseau de machines virtuelles correspondant configuré, et il à son tour doit être lié tooa correspondant du réseau logique associé au cloud cible de hello. |
| **Mappage de stockage** |Par défaut lorsque vous répliquez une machine virtuelle sur une source Hyper-V server tooa cible Hyper-V hôte serveur hôte, les données répliquées sont stockées dans l’emplacement par défaut hello qui est indiqué pour l’ordinateur hôte Hyper-V de cible hello dans le Gestionnaire Hyper-V. Pour disposer d’un meilleur contrôle sur l’emplacement de stockage des données répliquées, vous pouvez configurer un mappage de stockage.<br/><br/> stockage de tooconfigure un mappage, vous devez tooset des classifications de stockage sur la source de hello et serveurs VMM cible avant de commencer le déploiement. |

## <a name="step-1-create-a-site-recovery-vault"></a>Étape 1 : Création d’un coffre Site Recovery
1. Connectez-vous à toohello [portail de gestion](https://portal.azure.com) d’un serveur VMM hello souhaité tooregister.
2. Développez **Data Services** > **Recovery Services**, puis cliquez sur **Coffre Site Recovery**.
3. Cliquez sur **Créer nouveau** > **Création rapide**.
4. Dans **nom**, entrez un coffre de hello tooidentify nom convivial.
5. Dans **région** sélectionnez hello région géographique pour le coffre hello. les régions toocheck pris en charge consultez disponibilité géographique dans [détails de la tarification de Azure Site Recovery](http://go.microsoft.com/fwlink/?LinkId=389880).
6. Cliquez sur **Create vault**.

    ![Create vault](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Vérification de ce coffre hello de la barre d’état hello a été créée. Hello est répertorié en tant que **Active** sur la page Services de récupération de la principale hello.

## <a name="step-2-generate-a-vault-registration-key"></a>Étape 2 : Génération d’une clé d'inscription du coffre
Générer une clé d’inscription dans le coffre hello. Une fois que vous téléchargez hello fournisseur Azure Site Recovery et l’installer sur le serveur VMM de hello, vous allez utiliser ce serveur VMM de hello tooregister clé dans le coffre hello.

1. Bonjour **Services de récupération** , cliquez sur la page de démarrage rapide de hello coffre tooopen hello. Démarrage rapide peut également être ouvert à tout moment à l’aide d’icône de hello.

    ![Icône Quick Start](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Dans la liste déroulante de hello, sélectionnez **entre deux sites VMM de local**.
3. Dans **Préparer les serveurs VMM**, cliquez sur **Générer le fichier de clé d’inscription**. fichier de clé Hello est généré automatiquement et n’est valide pendant 5 jours après sa génération. Si vous n’accédez pas à hello portail Azure à partir du serveur VMM de hello, vous devez toocopy ce serveur toohello de fichiers.

    ![Clé d’enregistrement](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Étape 3 : Installer hello fournisseur Azure Site Recovery
1. Sur hello **Quick Start** page **serveurs VMM de préparer**, cliquez sur **télécharger le fournisseur Microsoft Azure Site Recovery pour installation sur les serveurs VMM** hello tooobtain dernière version du fichier d’installation hello.
2. Exécuter ce fichier sur le serveur VMM de hello source.

   > [!NOTE]
   > Si VMM est déployé dans un cluster et que vous installez hello fournisseur pour hello première installez-la sur un nœud actif et terminer hello installation tooregister hello serveur VMM dans le coffre hello. Installez hello fournisseur sur hello autres nœuds. Notez que si vous mettez à niveau hello fournisseur, vous devez tooupgrade sur tous les nœuds, car elles doivent toutes être en cours d’exécution hello même version du fournisseur.
   >
   >
3. programme d’installation de Hello réalise un certain nombre **vérification des conditions préalables** et demandes hello de toostop autorisation VMM toobegin l’installation du fournisseur de service. Hello Service VMM va redémarrer automatiquement lorsque le programme d’installation se termine. Si vous installez sur un cluster VMM que vous serez invité toostop le rôle de Cluster hello.
4. Dans **Microsoft Update** , vous pouvez opter pour l’installation de mises à jour. Avec ce paramètre activés les mises à jour fournisseur seront installés selon la stratégie de Microsoft Update tooyour.

    ![Mises à jour Microsoft](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. emplacement d’installation Hello est défini trop**<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Cliquez sur hello toostart de bouton installer installation hello fournisseur.

    ![Emplacement de l’installation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Après avoir hello fournisseur est installé, cliquez sur **inscrire** serveur hello de tooregister dans le coffre hello.

    ![Installation terminée](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. Dans **nom du coffre**, vérifier nom hello de coffre hello dans le hello serveur sera inscrit. Cliquez sur *Suivant*.

    ![Enregistrement du serveur](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. Dans **connexion Internet** spécifier comment hello fournisseur qui s’exécute sur hello VMM server connecte toohello Internet. Sélectionnez **se connecter avec des paramètres proxy existants** paramètres de la connexion d’Internet toouse hello par défaut configurés sur le serveur de hello.

    ![Paramètres Internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

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
13. Cliquez sur **suivant** processus de hello toocomplete. Après l’inscription, les métadonnées d’un serveur hello VMM sont récupérées par Azure Site Recovery. Hello serveur s’affiche dans **serveurs VMM** > **serveurs** dans le coffre hello.

    ![Serveurs](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Installer à partir de la ligne de commande
Hello fournisseur Azure Site Recovery peut également être installé à partir de la ligne de commande hello. Cette méthode peut être le fournisseur de hello tooinstall utilisé sur un serveur de base pour Windows Server 2012 R2.

1. Téléchargez hello fournisseur de fichiers et d’enregistrement clé tooa dossier d’installation. par exemple C:\ASR.
2. Arrêter le Service System Center Virtual Machine Manager de hello
3. Extraire le programme d’installation du fournisseur de hello en exécutant ces commandes à partir d’une invite de commandes avec **administrateur** privilèges :

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Installez le fournisseur de hello en exécutant :

        C:\ASR> setupdr.exe /i
5. Inscription du fournisseur de hello en exécutant :

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>     

Où les paramètres de hello sont :

* **/ Informations d’identification**: un paramètre obligatoire qui spécifie l’emplacement de hello dans le hello se trouve le fichier de clé d’inscription  
* **/ FriendlyName**: paramètre obligatoire pour nom hello du serveur hôte hello Hyper-V qui s’affiche dans le portail Azure Site Recovery hello.
* **/ EncryptionEnabled**: paramètre facultatif que vous avez besoin de toouse uniquement dans hello VMM tooAzure scénario si vous avez besoin de chiffrement de vos machines virtuelles au repos dans Azure. Vérifiez que le nom hello du fichier de hello vous fournir a un **.pfx** extension.
* **/ProxyAddress**: paramètre facultatif qui spécifie l’adresse hello du serveur de proxy hello.
* **/ProxyPort**: paramètre optionnel qui spécifie le port du serveur proxy de hello hello.
* **/proxyUsername**: paramètre facultatif qui spécifie le nom d’utilisateur Proxy hello (si le proxy requiert une authentification).
* **/proxyPassword**: paramètre facultatif qui spécifie hello mot de passe pour l’authentification avec le serveur de proxy hello (si le proxy requiert une authentification).  

## <a name="step-4-configure-cloud-protection-settings"></a>Étape 4 : Configuration des paramètres de protection de cloud
Une fois les serveurs VMM inscrits, vous pouvez configurer les paramètres de protection de cloud. Si vous avez activé l’option de hello **synchroniser les données de cloud avec le coffre de hello** hello fournisseur lorsque vous avez installé, tous les clouds sur le serveur VMM de hello seront affiche sous hello **éléments protégés** onglet dans le coffre hello. Si vous n’avez pas encore synchroniser un cloud spécifique avec Azure Site Recovery hello **général** onglet de page de propriétés de cloud hello dans la console VMM hello.

![Cloud publié](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Dans la page de démarrage rapide de hello, cliquez sur **configurer la protection pour les clouds VMM**.
2. Sur hello **Clouds VMM** , sélectionnez le cloud hello que vous souhaitez tooconfigure et que vous allez toohello **Configuration** onglet.
3. Dans **Cible**, sélectionnez **VMM**.
4. Dans **emplacement cible**, sélectionnez hello serveur VMM local qui gère le cloud hello toouse souhaité pour la récupération.
5. Dans **cloud cible**, sélectionnez hello cible cloud toouse pour le basculement des machines virtuelles dans le cloud de source de hello. Notez les points suivants :

   * Nous vous recommandons de sélectionner un cloud cible qui répond aux exigences de récupération pour les ordinateurs virtuels de hello que vous permettent de protéger.
   * Paire de cloud unique tooa ne peut appartenir qu’un cloud, en tant que principal ou un cloud cible.
6. Dans **Fréquence de copie**, spécifiez la fréquence de synchronisation des données entre les emplacements source et cible. Notez que ce paramètre est pertinente uniquement lorsque l’ordinateur hôte Hyper-V de hello est en cours d’exécution Windows Server 2012 R2. Les autres serveurs utilisent un paramétrage par défaut de cinq minutes.
7. Dans **des points de récupération**, spécifiez si vous souhaitez toocreate des points supplémentaires. Hello zéro par défaut indique que seuls hello dernier point de récupération pour un ordinateur virtuel principal est stocké sur un serveur hôte de réplica. Notez que l’activation de plusieurs points de récupération nécessite un stockage supplémentaire pour les instantanés hello qui sont stockés sur chaque point de récupération. Par défaut, des points de récupération sont créés toutes les heures, pour que chacun contienne une heure de données. valeur de point de récupération Hello que vous attribuez à la machine virtuelle de hello dans la console VMM hello ne doit pas être inférieure à celle hello que vous affectez dans la console Azure Site Recovery hello.
8. Dans **fréquence des instantanés cohérents au niveau applicatif**, spécifiez la fréquence à laquelle toocreate des instantanés cohérents au niveau de l’application. Hyper-V utilise deux types de captures instantanées, un instantané standard qui fournit un instantané incrémentiel de la machine virtuelle hello et un instantané cohérent de l’application qui prend un instantané de point-à-temps hello des données d’application à l’intérieur de machine virtuelle de hello. Instantanés cohérents au niveau de l’application utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello. Notez que si vous activez les instantanés cohérents au niveau de l’application, il affecte les performances de hello des applications s’exécutant sur des machines virtuelles sources. Assurez-vous que la valeur hello que vous définissez est inférieur au nombre de hello de points de récupération supplémentaires que vous configurez.

    ![Configurer les paramètres de protection](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. Dans **Compression du transfert de données**, indiquez si les données répliquées transférées doivent être compressées.
10. Dans **authentification**, spécifiez comment le trafic est authentifié entre hello principal et les serveurs hôtes Hyper-V de récupération. Sélectionnez HTTPS, sauf si vous avez configuré un environnement Kerberos opérationnel. Azure Site Recovery configurera automatiquement des certificats pour l'authentification HTTPS. Aucune configuration manuelle n'est nécessaire. Si vous sélectionnez Kerberos, un ticket Kerberos sera utilisé pour l’authentification mutuelle des serveurs hôtes de hello. Par défaut, les ports 8083 et 8084 (pour les certificats) seront ouverts dans hello le pare-feu Windows sur les serveurs hôtes de Hyper-V hello. Notez que ce paramètre n'est utile que pour les serveurs hôtes Hyper-V s'exécutant sur Windows Server 2012 R2.
11. Dans **Port**, modifiez hello numéro du port sur lequel la source hello et de cibler les ordinateurs d’hôte écoute le trafic de réplication. Par exemple, vous pouvez modifier le paramètre de hello si vous souhaitez tooapply qualité de Service (QoS) réseau limitation de bande passante pour le trafic de réplication. Vérifiez que le port de hello n’est pas utilisé par une autre application et qu’il est ouvert dans les paramètres de pare-feu hello.
12. Dans **la méthode de réplication**, spécifiez comment la réplication initiale des données à partir d’emplacements de tootarget source hello sera gérée, avant le démarrage de la réplication normale :

    * **Réseau**: copie de données sur le réseau de hello peut être longue et gourmande en ressources. Nous vous recommandons d’utiliser cette option si le cloud de hello contient des machines virtuelles avec des disques durs virtuels relativement petits, et si le site principal de hello est un site secondaire de toohello connecté via une connexion haut débit. Vous pouvez spécifier que copie de hello doit démarrer immédiatement, ou sélectionnez une heure. Si vous utilisez la réplication réseau, nous vous recommandons de la planifier sur des heures creuses.
    * **En mode hors connexion**, cette méthode indique que la réplication initiale hello sera effectuée à l’aide d’un support externe. Il est utile si vous souhaitez tooavoid la dégradation des performances du réseau, ou pour les emplacements géographiquement distants. toouse cette méthode, vous spécifiez l’emplacement d’exportation hello sur hello source cloud et emplacement d’importation hello sur le cloud cible de hello. Lorsque vous activez la protection pour un ordinateur virtuel, un disque dur virtuel hello est copié toohello spécifié emplacement d’exportation. Vous l’envoyez site cible de toohello et copiez toohello emplacement d’importation. Hello système copies hello importés des machines virtuelles de réplication de toohello plus d’informations.
13. Sélectionnez **Machine virtuelle de réplication supprimer** toospecify qui hello d’ordinateur virtuel de réplication doit être supprimé si vous arrêtez la protection de machine virtuelle de hello en sélectionnant hello **supprimer la protection pour la machine virtuelle de hello**  option sur l’onglet de Machines virtuelles hello des propriétés de cloud hello. Avec ce paramètre activé, quand vous désactivez la protection hello virtual machine est supprimée d’Azure Site Recovery hello des paramètres de récupération de Site pour la machine virtuelle de hello sont supprimés dans la console VMM hello et hello réplica est supprimé.

    ![Configurer les paramètres de protection](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Après avoir enregistré les paramètres hello un travail est créé et peuvent être surveillé sur hello **travaux** onglet. Tous les serveurs hôtes de Hyper-V dans hello cloud source VMM seront configurés pour la réplication. Paramètres de cloud peuvent être modifiés sur hello **configurer** onglet. Si vous souhaitez toomodify hello cible emplacement cible cloud ou vous devez supprimer la configuration du cloud hello et puis reconfigurez hello cloud.

### <a name="prepare-for-offline-initial-replication"></a>Préparer la réplication initiale hors connexion
Vous devez hello toodo suivant tooprepare d’actions pour la réplication initiale hors connexion :

* Sur le serveur de source de hello, vous allez spécifier un emplacement de chemin d’accès à partir de quels hello exportation de données aura lieu. Affecter un contrôle total pour les autorisations de partage et NTFS toohello le service VMM sur le chemin d’exportation de hello. Sur le serveur cible de hello, vous allez spécifier un emplacement de chemin d’accès à partir de laquelle importent les données de salutation se produira. Affecter des mêmes autorisations sur ce chemin d’accès d’importation hello.
* Si hello importer ou chemin d’exportation est partagé, attribuer l’appartenance au groupe administrateur, utilisateur avec pouvoir, opérateurs d’impression ou opérateur de serveur pour le compte de service VMM hello sur l’ordinateur distant de hello sur quel hello partagé se trouve.
* Si vous utilisez des hôtes exécuter en tant que comptes tooadd, sur hello importer et exporter les chemins d’accès, affecter en lecture et écriture toohello comptes d’identification dans VMM.
* Hello importer et exporter les partages ne doivent pas être situés sur tout ordinateur utilisé comme un serveur hôte Hyper-V, car la configuration de boucle n’est pas pris en charge par Hyper-V.
* Dans Active Directory, sur chaque serveur hôte Hyper-V qui contient les ordinateurs virtuels que vous souhaitez tooprotect, activez et configurez des ordinateurs distants la délégation contrainte tootrust hello exportation et importation de hello chemins d’accès sont situés, comme suit :
  1. Sur le contrôleur de domaine hello, ouvrez **Active Directory Users and Computers**.
  2. Dans l’arborescence de la console hello cliquez sur **DomainName** > **ordinateurs**.
  3. Nom de serveur hôte hello Hyper-V avec le bouton droit > **propriétés**.
  4. Sur hello **délégation** T cliquez sur l’onglet**rouille cet ordinateur pour les services uniquement de délégation toospecified**.
  5. Cliquez sur **Utiliser tout protocole d’authentification**.
  6. Cliquez sur **Ajouter** > **Utilisateurs et ordinateurs**.
  7. Nom du type hello d’ordinateur hello qui héberge le chemin d’exportation de hello > **OK**. À partir de la liste hello des services disponibles, maintenez la touche CTRL de hello et cliquez sur **cifs** > **OK**. Répétez pour nom hello d’ordinateur de hello ce chemin d’importation de hello hôtes. Répétez cette procédure pour les serveurs hôtes Hyper-V supplémentaires.

## <a name="step-5-configure-network-mapping"></a>Étape 5 : Configuration du mappage réseau
1. Dans la page de démarrage rapide de hello, cliquez sur **mapper les réseaux**.
2. Sélectionnez hello source VMM serveur à partir de laquelle vous souhaitez que les réseaux toomap, puis hello cible VMM toowhich messages hello du serveur réseaux seront mappés. liste Hello des réseaux source et de leurs réseaux cibles associés sont affichés. Une valeur vide est indiquée pour les réseaux qui ne sont pas mappés.
3. Sélectionnez un réseau dans **Réseau sur la source** > **Mapper**. service de Hello détecte les réseaux d’ordinateurs virtuels hello sur le serveur cible de hello et les affiche. Cliquez sur hello informations icône suivant toohello source et cible noms tooview hello sous-réseaux du réseau pour chaque réseau.

    ![Configurer le mappage réseau](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. Dans la boîte de dialogue hello sélectionnez un des réseaux d’ordinateurs virtuels hello à partir du serveur VMM de hello cible.

    ![Sélectionner un réseau cible](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Lorsque vous sélectionnez un réseau cible, hello clouds protégés qui utilisent le réseau source de hello sont affichés. Les réseaux cibles disponibles qui sont associés aux clouds hello utilisés pour la protection sont également affichés. Nous vous recommandons de sélectionner un réseau cible disponible tooall hello clouds utilisés pour la protection. Ou vous pouvez également toohello serveur VMM et modifier hello cloud propriétés tooadd hello réseau logique correspondant toohello réseau d’ordinateurs virtuels que vous souhaitez toochoose.
6. Cliquez sur le processus de mappage hello coche toocomplete hello. Un travail démarre la progression du mappage tootrack hello. Vous pouvez l’afficher sur hello **travaux** onglet.

## <a name="step-6-configure-storage-mapping"></a>Étape 6 : Configuration du mappage de stockage
Par défaut lorsque vous répliquez une machine virtuelle sur une source Hyper-V server tooa cible Hyper-V hôte serveur hôte, les données répliquées sont stockées dans l’emplacement par défaut hello qui est indiqué pour l’ordinateur hôte Hyper-V de cible hello dans le Gestionnaire Hyper-V. Si vous souhaitez mieux contrôler l'emplacement de stockage des données de réplication, vous pouvez configurer des mappages de stockage comme suit :

1. Définir des classifications de stockage sur les deux sources hello et serveurs VMM cible. [En savoir plus](https://technet.microsoft.com/library/gg610685.aspx). Classifications doivent être des serveurs d’hôtes Hyper-V toohello disponibles dans les clouds source et cible. Les classifications n’avez pas besoin toohave hello même type de stockage. Par exemple, vous pouvez mapper une classification source contenant la classification SMB partages tooa cible qui contient des volumes partagés de cluster.
2. Une fois les classifications en place, vous pouvez créer des mappages. toodo cette, hello **Quick Start** page > **mapper le stockage**.
3. Cliquez sur hello **stockage** onglet > **mapper les classifications de stockage**.
4. Sur hello **mapper les classifications de stockage** , sélectionnez les classifications sur la source de hello et serveurs VMM cible. Enregistrez vos paramètres.

    ![Sélectionner un réseau cible](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>Étape 7 : Activation de la protection des machines virtuelles
Une fois les serveurs, les clouds et les réseaux configurés, vous pouvez activer la protection des machines virtuelles dans le cloud de hello.

1. Sur hello **virtuels** dans le cloud hello dans le hello ordinateur virtuel se trouve sous l’onglet **activer la protection** > **ajouter des machines virtuelles**.
2. À partir de la liste de hello d’ordinateurs virtuels dans le cloud de hello, sélectionnez hello une souhaité tooprotect.

    ![Activer la protection pour les machines virtuelles](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Suivre la progression de hello action Activer la Protection Bonjour **travaux** onglet, y compris la réplication initiale hello. Après le travail finaliser la Protection de hello machine virtuelle de hello s’exécute est prêt pour le basculement. Une fois la protection est activée et machines virtuelles répliquées, vous serez en mesure de tooview dans Azure.

    ![Tâche de protection de la machine virtuelle](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> Vous pouvez également activer la protection des machines virtuelles dans la console VMM hello. Cliquez sur **activer la Protection** sur la barre d’outils hello Bonjour **Azure Site Recovery** onglet dans les propriétés d’ordinateur virtuel hello.
>
>

### <a name="on-board-existing-virtual-machines"></a>Intégrer des machines virtuelles existantes
Si vous avez des machines virtuelles existantes dans VMM qui sont répliqués avec réplica Hyper-V, vous devez tooonboard pour la protection Azure Site Recovery comme suit :

1. Vérifiez que vous avez un cloud principal et un cloud secondaire. Vérifiez que serveur hello Hyper-V qui héberge la machine virtuelle existante de hello se trouve dans un cloud principal hello et que ce serveur d’Hyper-V hello hébergement hello ordinateur virtuel se trouve dans le cloud secondaire de hello. Assurez-vous que vous avez configuré les paramètres de protection pour les clouds hello. paramètres de Hello doivent correspondre à ceux actuellement configurés pour réplica Hyper-V. Sinon, la réplication de machine virtuelle risque de ne pas fonctionner comme prévu.
2. Puis activez la protection pour l’ordinateur virtuel principal hello. Azure Site Recovery et VMM garantit que hello même hôte de réplica et de la machine virtuelle est détectée, et Azure Site Recovery réutilise et rétablit la réplication à l’aide des paramètres de hello configurés lors de la configuration du cloud.

## <a name="test-your-deployment"></a>Tester votre déploiement
planification de votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération composé de plusieurs ordinateurs virtuels et exécuter un test de basculement pour hello tootest.  Il simule votre mécanisme de basculement et de récupération dans un réseau isolé.

### <a name="create-a-recovery-plan"></a>Créer un plan de récupération
1. Sur hello **les Plans de récupération** , cliquez sur **créer un Plan de récupération**.
2. Spécifiez un nom pour le plan de récupération hello et les serveurs VMM source et cible. serveur de source de Hello doit avoir des machines virtuelles qui sont activés pour le basculement et la récupération. Sélectionnez **Hyper-V** tooview uniquement cloud est configuré pour la réplication Hyper-V.

    ![Créer un plan de récupération](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. Dans **Sélectionner la machine virtuelle**, sélectionnez les groupes de réplication. Toutes les machines virtuelles associées au groupe de réplication hello est sélectionnés et ajouté le plan de récupération toohello. Ces machines virtuelles sont ajoutés de groupe par défaut de plans de récupération toohello : groupe 1. Vous pouvez ajouter d'autres groupes si nécessaire. Notez qu’une fois que les machines virtuelles de réplication démarre en fonction de la commande hello de groupes de plan de récupération hello.

    ![Ajouter des machines virtuelles](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Après avoir créé un plan de récupération, il apparaît dans la liste hello sur hello **les Plans de récupération** onglet.

### <a name="run-a-test-failover"></a>Exécution d’un test de basculement
1. Sur hello **les Plans de récupération** , sélectionnez le plan de hello et cliquez sur **Test de basculement**.
2. Sur hello **confirmer le Test de basculement** page, sélectionnez **aucun**. Notez que cette option activée hello basculé de machines virtuelles de réplication n’est pas connecté tooany réseau. Cette opération teste qui hello échoue de machine virtuelle plus comme prévu, mais ne teste pas votre environnement réseau de réplication. Examiner le trop[exécuter un test de basculement](site-recovery-failover.md) pour plus d’informations sur la façon toouse différentes options de mise en réseau.
3. machine virtuelle de test Hello va être créé sur hello en tant qu’hôte hello sur quel hello machine virtuelle de réplication existe le même hôte. Il est ajouté toohello cloud même dans le hello machine virtuelle de réplication se trouve.

### <a name="run-a-recovery-plan"></a>Exécuter un plan de récupération
Une fois la réplication hello ordinateur virtuel n’est peut-être pas une adresse IP qui est hello identique à l’adresse IP hello hello ordinateur virtuel principal. Machines virtuelles met à jour de serveur DNS hello qu’ils utilisent après leur démarrage. Vous pouvez également ajouter un tooensure de serveur DNS hello script tooupdate une mise à jour en temps voulu.

#### <a name="script-tooretrieve-hello-ip-address"></a>Adresse IP de script tooretrieve hello
Exécutez cette adresse IP d’exemple script tooretrieve hello.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-tooupdate-dns"></a>Script tooupdate DNS
Exécutez cette tooupdate de script d’exemple DNS, en spécifiant l’adresse IP de hello vous récupérées à l’aide de hello précédent exemple de script.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Informations de confidentialité pour Azure Site Recovery
Cette section fournit des informations de confidentialité supplémentaire pour hello le service Microsoft Azure Site Recovery (« Service »). déclaration de confidentialité tooview hello pour les services Microsoft Azure, consultez le [déclaration de confidentialité de Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=324899)

**Fonctionnalité : Inscription**

* **Résultat**: inscrit le serveur auprès du service pour que les machines virtuelles puissent être protégées.
* **Les informations collectées**: après l’inscription hello Service collecte, traite et transmet les informations de certificat de gestion de serveur VMM hello désigné à l’aide du nom du Service hello du serveur VMM de hello, la récupération d’urgence tooprovide et le nom de hello de clouds de machines virtuelles sur votre serveur VMM.
* **Utilisation des informations**:

  * Certificat de gestion, il est utilisé toohelp identifier et d’authentifier le serveur VMM de hello inscrit pour l’accès toohello Service. Hello Service utilise hello partie de clé publique hello toosecure de certificat enregistré d’un jeton uniquement hello serveur VMM peut accéder. serveur de Hello doit toouse ce jeton toogain accès toohello Service les fonctions.
  * Nom du serveur VMM de hello : nom du serveur VMM hello est tooidentify requis et communiquer avec le serveur VMM approprié hello sur quel hello clouds sont situés.
  * Les noms de serveur VMM de hello en nuage : nom du cloud hello est requis lors de l’utilisation du cloud de Service hello appariement/annulation d’une fonctionnalité est décrite ci-dessous. Lorsque vous décidez toopair votre cloud à partir d’un centre de données principal avec un autre cloud dans le centre de données de récupération hello, les noms de tous les clouds hello à partir du centre de données de récupération hello hello sont présentés.
* **Choix**: ces informations est un élément essentiel de hello processus d’inscription de Service car elle permet de vous et hello du serveur VMM du Service tooidentify hello pour lequel vous souhaitez tooprovide une protection Azure Site Recovery, ainsi que tooidentify hello serveur VMM enregistré approprié. Si vous ne souhaitez pas toosend cette toohello informations Service, n’utilisez pas ce Service. Si vous enregistrez votre serveur, puis décidez toounregister, vous pouvez le faire en supprimant les informations sur le serveur VMM hello de portail hello (qui est hello portail Azure).

**Fonctionnalité : Activer la protection Azure Site Recovery**

* **Ce qu’il fait**: hello fournisseur Azure Site Recovery installé sur le serveur VMM de hello est conduit hello pour communiquer avec hello Service. Hello fournisseur est une bibliothèque de liens dynamiques (DLL) hébergée dans le processus de VMM hello. Après hello que fournisseur est installé, la fonctionnalité de « Récupération de centre de données » hello obtient activée dans la console Administrateur VMM hello. Toutes les machines virtuelles nouvelles ou existantes dans un cloud peut permettre à une propriété appelée « Récupération de centre de données » toohelp protéger un ordinateur virtuel hello. Une fois que cette propriété est définie, hello fournisseur envoie le nom de hello et l’ID de machine virtuelle de hello toohello Service. protection de virtuelle Hello est activée par la technologie de réplication Windows Server 2012 ou Windows Server 2012 R2 Hyper-V. données de machine virtuelle Hello répliquées à partir d’un tooanother d’ordinateur hôte Hyper-V (généralement situé dans un centre de données différent de « récupération »).
* **Les informations collectées**: hello Service collecte, traite et transmet les métadonnées de l’ordinateur virtuel hello, qui inclut le nom de hello, ID, réseau virtuel et le nom de hello du cloud de hello à laquelle elle appartient.
* **Utilisation des informations**: hello Service utilise hello au-dessus des informations de machine virtuelle toopopulate hello sur votre portail Service.
* **Choix**: Ceci est une partie essentielle du service de hello et ne peut pas être désactivé. Si vous ne souhaitez pas envoyer toohello Service ces informations, ne pas activer la protection d’Azure Site Recovery pour les machines virtuelles. Notez que toutes les données envoyées par le fournisseur de hello toohello Service est envoyé via HTTPS.

**Fonctionnalité : Plan de récupération**

* **Ce qu’il fait**: cette fonctionnalité vous permet de toobuild un plan d’orchestration pour le centre de données de « récupération » hello. Vous pouvez définir l’ordre hello dans le hello des machines virtuelles ou un groupe d’ordinateurs virtuels doit être démarré sur site de récupération hello. Vous pouvez également spécifier n’importe quel toobe des scripts automatisés exécuter ou n’importe quel toobe action manuelle effectuée au moment de hello de récupération pour chaque ordinateur virtuel. Le basculement (décrit dans la section suivante de hello) est généralement déclenché au hello au niveau du Plan de récupération pour la récupération coordonnée.
* **Les informations collectées**: hello Service collecte, traite et transmet les métadonnées de plan de récupération hello, y compris les métadonnées de l’ordinateur virtuel et les métadonnées des scripts d’automatisation et notes de l’action manuelle.
* **Utilisation des informations**: métadonnées hello décrites ci-dessus sont le plan de récupération hello toobuild utilisés dans votre portail du Service.
* **Choix**: Ceci est une partie essentielle du service de hello et ne peut pas être désactivé. Si vous ne souhaitez pas envoyer toohello Service ces informations, ne créez pas de Plans de récupération dans ce Service.

**Fonctionnalité : Mappage réseau**

* **Ce qu’il fait**: cette fonctionnalité vous permet d’informations sur le réseau à partir de centre de données de récupération hello données primaires center toohello toomap. Lors de la récupération des machines virtuelles de hello sur site de récupération hello, ce mappage permet l’établissement de la connectivité réseau pour eux.
* **Les informations collectées**: dans le cadre de la fonctionnalité de mappage réseau hello, hello Service collecte, traite et transmet les métadonnées hello de réseaux logiques de hello pour chaque site (principal et centre de données).
* **Utilisation des informations**: hello Service utilise hello métadonnées toopopulate votre portail Service où vous pouvez mapper les informations sur le réseau hello.
* **Choix**: Ceci est un élément essentiel de hello Service et ne peut pas être désactivé. Si vous ne souhaitez pas envoyer toohello Service ces informations, n’utilisez pas de fonctionnalité de mappage réseau hello.

**Fonctionnalité : Basculement - planifié, non planifié et test**

* **Ce qu’il fait**: cette fonctionnalité permet le basculement d’un ordinateur virtuel à partir d’un centre de données gérées par VMM tooanother centre données gérées par VMM. action de basculement Hello est déclenchée par l’utilisateur de hello sur leur portail de Service. Les raisons possibles pour un basculement sont un événement non planifié (par exemple dans les cas de hello d’un disaster0 naturelle ; un événement planifié (par exemple centre de données d’équilibrage de charge) ; un test de basculement (par exemple une répétition de plan de récupération).

Hello fournisseur sur le serveur VMM de hello est averti de l’événement hello hello Service et exécute une action de basculement sur l’ordinateur hôte Hyper-V de hello via les interfaces VMM. Le basculement réel de l’ordinateur virtuel de hello à partir d’un tooanother d’ordinateur hôte Hyper-V (généralement en cours d’exécution dans un centre de données différent de « récupération ») est géré par la technologie de réplication Windows Server 2012 ou Windows Server 2012 R2 Hyper-V hello. Une fois le basculement de hello terminée, hello fournisseur installé sur le serveur VMM de hello hello « récupération » du centre de données envoie hello réussite informations toohello Service.

* **Les informations collectées**: hello Service utilise hello au-dessus de l’état de hello informations toopopulate des informations sur l’action de basculement hello sur votre portail Service.
* **Utilisation des informations**: hello Service utilise hello au-dessus des informations comme suit :

  * Certificat de gestion, il est utilisé toohelp identifier et d’authentifier le serveur VMM de hello inscrit pour l’accès toohello Service. Hello Service utilise hello partie de clé publique hello toosecure de certificat enregistré d’un jeton uniquement hello serveur VMM peut accéder. serveur de Hello doit toouse ce jeton toogain accès toohello Service les fonctions.
  * Nom du serveur VMM de hello : nom du serveur VMM hello est tooidentify requis et communiquer avec le serveur VMM approprié hello sur quel hello clouds sont situés.
  * Les noms de serveur VMM de hello en nuage : nom du cloud hello est requis lors de l’utilisation du cloud de Service hello appariement/annulation d’une fonctionnalité est décrite ci-dessous. Lorsque vous décidez toopair votre cloud à partir d’un centre de données principal avec un autre cloud dans le centre de données de récupération hello, les noms de tous les clouds hello à partir du centre de données de récupération hello hello sont présentés.
* **Choix**: Ceci est une partie essentielle du service de hello et ne peut pas être désactivé. Si vous ne souhaitez pas envoyer toohello Service ces informations, n’utilisez pas ce Service.

## <a name="next-steps"></a>Étapes suivantes
Après avoir exécuté un toocheck de basculement de test de votre environnement fonctionne comme prévu, [en savoir plus sur](site-recovery-failover.md) différents types de basculement.
