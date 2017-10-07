---
title: "aaaFail sauvegarder des ordinateurs virtuels VMware à partir de Azure dans portail hérité classique de hello | Documents Microsoft"
description: "Cet article décrit comment toofail arrière un ordinateur virtuel VMware qui a été répliquée tooAzure avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a>Échec des ordinateurs virtuels VMware arrière et des serveurs physiques à partir de tooVMware Azure avec Azure Site Recovery (hérité)
> [!div class="op_single_selector"]
> * [portail Azure](site-recovery-failback-azure-to-vmware.md)
> * [Portail Azure Classic](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portail Azure Classic (version héritée)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Cet article décrit comment toofail les ordinateurs virtuels VMware précédent et serveurs physiques Windows/Linux à partir d’Azure tooyour sur site local une fois que vous avez répliquées à partir de votre site de site à l’aide de tooAzure [Azure Site Recovery ?](site-recovery-overview.md).

N’utilisez pas cet article pour de nouveaux coffres, car il décrit une configuration ancienne.

## <a name="architecture"></a>Architecture
Ce schéma représente un scénario de basculement et de restauration hello. les lignes Hello bleu sont hello connexions utilisées pendant le basculement. les lignes Hello rouge sont hello connexions utilisées lors de la restauration automatique. lignes Hello avec des flèches dépasser hello internet.

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a>Avant de commencer
* Vous devez avoir basculé vos machines virtuelles VMware ou serveurs physiques, et ils doivent être en cours d’exécution dans Azure.
* Notez que vous pouvez échouer uniquement les ordinateurs virtuels VMware arrière et des serveurs physiques Windows/Linux à partir d’ordinateurs virtuels de Azure tooVMware dans un site principal local de hello.  Si vous êtes échouent dans un ordinateur physique, basculement tooAzure convertira tooan machine virtuelle Azure, et la restauration automatique tooVMware convertira tooa VMware VM.

Voici comment configurer la restauration :

1. **Configurer les composants de la restauration automatique**: vous devez tooset d’un serveur v-continuum localement et faites-le pointer le serveur de configuration toohello machine virtuelle dans Azure. Vous allez également configurer un serveur de processus en tant qu’un serveur cible maître de machine virtuelle Azure toosend données toohello arrière local. Vous inscrivez un serveur de processus hello avec serveur de configuration hello gérée hello basculement. Vous installez un serveur cible maître local. Si vous avez besoin d’un serveur cible maître Windows, il est configuré automatiquement lorsque vous installez vContinuum. Si vous avez besoin de Linux, vous devez tooset, configurez-le manuellement sur un serveur distinct.
2. **Activer la protection et la restauration automatique**: une fois que vous avez configuré les composants hello, dans la v-continuum vous devez tooenable protection a échoué sur des machines virtuelles Azure. Vous allez exécuter une vérification de la disponibilité sur des machines virtuelles de hello et exécuter un basculement à partir d’Azure tooyour sur site local. Une fois la restauration automatique terminée vous protégez de nouveau machines locales pour qu’ils commencer la réplication tooAzure.

## <a name="step-1-install-vcontinuum-on-premises"></a>Étape 1 : Installer le serveur vContinuum en local
Vous devez tooinstall un serveur local v-continuum et pointer le serveur de configuration toohello.

1. [Téléchargez vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).
2. Puis téléchargez hello [mise à jour v-continuum](http://go.microsoft.com/fwlink/?LinkID=533813) version.
3. Installez la version la plus récente de v-continuum hello. Sur hello **Bienvenue** page, cliquez sur **suivant**.
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. Sur hello première page de l’Assistant de hello spécifier l’adresse IP de serveur CX hello et port du serveur hello CX. Sélectionnez **Utiliser HTTPS**.

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. Adresse IP de serveur de configuration hello trouver sur hello **tableau de bord** onglet hello du serveur de configuration machine virtuelle dans Azure.
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. Rechercher le serveur de configuration hello HTTPS port public hello **points de terminaison** onglet hello du serveur de configuration machine virtuelle dans Azure.

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. Sur hello **détails de phrase secrète CS** page spécifier hello une phrase secrète que vous avez notée vers le bas lorsque vous avez inscrit le serveur de configuration hello. Si vous avez oublié il archivez-le **C:\\Program Files (x86)\\InMage systèmes\\privé\\connection.passphrase** sur la machine virtuelle du serveur de configuration hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. Bonjour **sélectionner l’emplacement de Destination** page spécifier où vous souhaitez que tooinstall hello v-continuum serveur et cliquez sur **installer**.

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. Une fois l’installation terminée, vous pouvez lancer vContinuum.
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a>Étape 2 : Installer un serveur de processus dans Azure
Vous devez tooinstall un serveur de traitement dans Azure afin que les machines virtuelles de hello dans Azure peuvent envoyer le serveur cible maître local hello données tooan précédent.

1. Sur hello **serveurs de Configuration** page dans Azure, sélectionnez tooadd un nouveau serveur de processus.

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. Spécifiez un nom de serveur de processus et un nom et mot de passe tooconnect toohello des ordinateurs virtuels en tant qu’administrateur. Sélectionnez hello configuration serveur toowhich tooregister hello processus serveur. Il doit s’agir hello même serveur que vous utilisez tooprotect et basculez vos machines virtuelles.
3. Spécifiez hello Azure réseau dans le hello serveur de processus doit être déployé. Il doit être le même hello réseau en tant que serveur de configuration hello. Indiquez une adresse IP unique dans le sous-réseau sélectionné et commencez le déploiement.

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. Un travail est un serveur de processus hello toodeploy déclenchées.

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. Vous pouvez vous connecter serveur hello à l’aide des informations d’identification hello que vous avez spécifié une fois que le serveur de processus hello est déployé dans Azure. Inscrire le serveur de processus hello Bonjour même façon que vous avez inscrit hello processus serveur local.

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> serveurs Hello enregistrés lors de la restauration automatique ne seront pas visibles sous les propriétés de machine virtuelle en cours de récupération de Site. Elles ne sont visibles sous hello **serveurs** onglet de hello configuration serveur toowhich lequel ils sont enregistrés. Il peut prendre environ 10-15 minutes jusqu'à ce qu’ils hello processus serveur s’affiche dans l’onglet de hello.
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a>Étape 3 : Installer un serveur cible maître local
Selon votre système d’exploitation de machines virtuelles source, vous devez tooinstall une Linux, ou un serveur cible maître de Windows local.

### <a name="deploy-a-windows-master-target-server"></a>Déployer un serveur cible maître Windows
Un serveur cible maître Windows est d’ores et déjà fourni avec la configuration du serveur vContinuum. Lorsque vous installez v-continuum hello, un serveur maître est également déployé sur hello même ordinateur et le serveur de configuration toohello inscrits.

1. déploiement de toobegin, créer vide de l’ordinateur local sur l’ordinateur hôte ESX hello sur lequel vous souhaitez toorecover hello machines virtuelles à partir d’Azure.
2. Assurez-vous qu’il existe au moins deux disques attachés toohello machine virtuelle : un est utilisé pour le système d’exploitation de hello et hello autres est utilisé pour le lecteur de rétention hello.
3. Installer le système d’exploitation de hello.
4. Installez v-continuum hello sur le serveur de hello. Installation du serveur cible maître de hello est également terminée.

### <a name="deploy-a-linux-master-target-server"></a>Déployer un serveur cible maître Linux
1. déploiement de toobegin, créer vide de l’ordinateur local sur l’ordinateur hôte ESX hello sur lequel vous souhaitez toorecover hello machines virtuelles à partir d’Azure.
2. Assurez-vous qu’il existe au moins deux disques attachés toohello machine virtuelle : un est utilisé pour le système d’exploitation de hello et hello autres est utilisé pour le lecteur de rétention hello.
3. Installer le système d’exploitation de Linux hello. Hello système du serveur cible maître Linux ne doit pas utiliser de gestionnaire de volume logique racine ou rétention des espaces de stockage. Une serveur cible maître de Linux configuré découverte de partitions/disques tooavoid Gestionnaire de volume logique par défaut.
4. Partitions que vous pouvez créer :

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. Effectuer avant de commencer l’installation du serveur cible maître hello hello ci-dessous les étapes d’installation post.

#### <a name="post-os-installation-steps"></a>Procédure de post-installation du système d’exploitation
tooget hello les ID SCSI pour chaque disque SCSI dans une machine virtuelle Linux, activez le paramètre hello « disque. EnableUUID = TRUE » comme suit :

1. Arrêtez votre machine virtuelle.
2. Droit d’entrée de machine virtuelle hello dans le panneau de gauche hello > **modifier les paramètres**.
3. Cliquez sur hello **Options** onglet. Sélectionnez **Avancé\>Général** > **Paramètres de configuration**. Hello **les paramètres de Configuration** option est disponible uniquement lorsque l’ordinateur de hello est arrêté.

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. Vérifiez si une ligne comportant **disk.EnableUUID** existe. Si Oui et est défini trop**False** puis définissez-la trop**True** (non sensible à la casse). Si existe et est tootrue, cliquez sur **Annuler** et tester la commande hello SCSI à l’intérieur du système d’exploitation de hello invité après qu’il est démarré. Si elle n’existe pas, cliquez sur **Ajouter une ligne**.
5. Ajouter le disque. EnableUUID Bonjour **nom** colonne. Définissez la valeur sur TRUE. N’ajoutez pas hello au-dessus des valeurs, ainsi que des guillemets doubles.

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a>Télécharger et installer des packages supplémentaires hello
Remarque : Assurez-vous que le système de hello possède une connexion internet avant de télécharger et installer des packages supplémentaires hello.

\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools

Cette commande permet de télécharger ces 15 packages à partir du référentiel CentOS 6.6 et de les installer :

bc-1.06.95-1.el6.x86\_64.rpm

busybox-1.15.1-20.el6.x86\_64.rpm

elfutils-libs-0.158-3.2.el6.x86\_64.rpm

kexec-tools-2.0.0-280.el6.x86\_64.rpm

lsscsi-0.23-2.el6.x86\_64.rpm

lzo-2.03-3.1.el6\_5.1.x86\_64.rpm

perl-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm

perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm

perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm

perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-version-0.77-136.el6\_6.1.x86\_64.rpm

rsync-3.0.6-12.el6.x86\_64.rpm

snappy-1.1.0-1.el6.x86\_64.rpm

wget-1.12-5.el6\_6.1.x86\_64.rpm

Si hello source utilise Reiser ou XFS de système de fichiers pour le périphérique de démarrage ou de la racine de hello, packages suivants doivent être téléchargés et installés sur tooprotection préalable du serveur cible maître Linux.

\# cd /usr/local

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm

\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm

#### <a name="apply-custom-configuration-changes"></a>Appliquer des modifications de configuration personnalisées
Avant d’appliquer ces modifications. Vérifiez que vous avez terminé de section précédente de hello, puis procédez comme suit :

1. Copiez toohello binaire de hello RHEL 6-64 unifiée de l’Agent nouvellement créée du système d’exploitation.
2. Exécutez cette commande hello toountar binaire : **tar - zxvf \<nom de fichier\>**
3. Exécutez cette autorisations toogive de commande : \# **chmod 755./ApplyCustomChanges.sh**
4. Exécutez le script de hello :  **\# ./ApplyCustomChanges.sh**. Exécuter le script hello qu’une seule fois sur le serveur de hello. Redémarrez le serveur de hello après exécution du script hello.

### <a name="install-hello-linux-server"></a>Installer le serveur de Linux hello
1. [Télécharger](http://go.microsoft.com/fwlink/?LinkID=529757) fichier d’installation hello.
2. Copiez hello fichier toohello virtuels cible maître Linux à l’aide d’un utilitaire de client sftp de votre choix. Ou bien vous pouvez ouvrir une session sur une machine virtuelle cible maître Linux hello et utiliser le package d’installation wget toodownload hello à partir du lien fourni
3. Connectez-vous à la machine virtuelle au serveur hello Linux cible maître en utilisant un ssh client de votre choix.
4. Si vous êtes connecté toohello Azure réseau sur lequel vous déployé votre serveur de la cible maître Linux via une connexion VPN, puis utilisez l’adresse IP interne pour le serveur hello que vous pouvez trouver dans la machine virtuelle **tableau de bord** onglet et le port 22 tooconnect toohello Linux master cibler un serveur à l’aide de Secure Shell.
5. Si vous vous connectez le serveur de cible maître Linux toohello via une connexion internet publique utiliser adresse IP virtuelle publique du serveur cible maître hello Linux (à partir d’ordinateurs virtuels hello **tableau de bord** onglet) et hello du point de terminaison public créé pour ssh toologin toohello Linux servder.
6. Extraire les fichiers hello archive tar programme d’installation de la cible maître Linux hello gzippé serveur en exécutant : *« tar – xvzf Microsoft ASR\_UA\_8.2.0.0\_-64 RHEL6 «* à partir du répertoire de hello qui contient le fichier du programme d’installation hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. Si vous hello extraits installer tooa autre répertoire des fichiers de modifier le contenu hello toowhich du répertoire toohello d’archive tar de hello ont été extraits. À partir de ce répertoire, exécutez « sudo ./install.sh ».

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. Lorsque toochoose invité à un rôle principal Sélectionnez **2 (principale cible)**. Laissez des autres options d’installation interactif hello avec leurs valeurs par défaut.
9. Attendez qu’installation toocontinue et hello tooappear de Config Interface de l’hôte. Hello utilitaire de Configuration de l’hôte de hello Linux cible maître Server est un utilitaire de ligne de commande. Ne pas redimensionner hello ssh fenêtre de l’utilitaire client. Utilisez Bonjour flèche clés tooselect Bonjour **Global** option appuyez sur entrée de votre clavier.

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. Dans le champ de hello **IP** Entrez l’adresse IP interne de hello hello du serveur de configuration (vous pouvez le trouver dans hello **tableau de bord** onglet hello du serveur de configuration VM) et appuyez sur ENTRÉE. Dans le champ **Port**, entrez la valeur **22**, puis appuyez sur ENTRÉE.
11. Laissez le champ **Use HTTPS** (Utiliser HTTPS) défini sur **Yes** (Oui), puis appuyez sur ENTRÉE.
12. Entrez hello phrase secrète qui a été généré sur le serveur de configuration hello. Si vous utilisez un client PUTTY à partir d’une machine virtuelle de Windows machine toossh toohello Linux, vous pouvez utiliser MAJ + INSER contenu de hello toopaste du Presse-papiers de hello. Copiez hello phrase secrète toohello local du Presse-papiers à l’aide de Ctrl + C, puis utilisez MAJ + INSER toopaste il. Appuyez sur ENTRÉE.
13. Utilisez hello flèche droite toonavigate clé tooquit et appuyez sur ENTRÉE. Attendez que toocomplete de l’installation.

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

Si pour une raison quelconque, vous avez effectué tooregister votre serveur de configuration toohello serveur Linux cible maître faire encore une fois en exécutant des utilitaire de configuration de l’ordinateur hôte à partir de /usr/local/ASR/Vx/bin/hostconfigcli (vous devez tooset accès autorisations toothis répertoire par chmod en cours d’exécution en tant que super utilisateur).

#### <a name="validate-master-target-registration"></a>Valider l’inscription du serveur cible maître
Vous pouvez valider ce hello serveur cible maître a été inscrit correctement le serveur de configuration toohello dans le coffre Azure Site Recovery > **serveur de Configuration** > **détails du serveur**.

> [!NOTE]
> Après l’inscription de serveur cible maître de hello, si vous recevez des erreurs de configuration qui hello d’ordinateur virtuel a peut-être été supprimé à partir de Azure ou que les points de terminaison ne sont pas configurés correctement, il s’agit, car bien que hello configuration du serveur cible maître est détectée. par hello dndpoints Azure lorsque le serveur cible maître hello est déployé dans Azure, cela n’est pas vrai pour un local cible maître serveur local. Cela n’affecte pas la restauration automatique, et vous pouvez ignorer ces erreurs.
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a>Étape 4 : Protéger hello machines virtuelles toohello sur site local
Vous devez tooprotect machines virtuelles toohello sur site local avant d’effectuer le retour.

### <a name="before-you-begin"></a>Avant de commencer
Lorsqu’un ordinateur virtuel est basculé tooAzure, il ajoute un disque temporaire supplémentaire pour le fichier d’échange. Il s’agit d’un lecteur supplémentaire qui n’est généralement pas requis par votre machine virtuelle basculée, dans la mesure où bien souvent, elle présente déjà un lecteur dédié au fichier de page. Avant de commencer la protection inverse des machines virtuelles de hello, vous devez vous assurer que ce lecteur est mis hors connexion afin que ne pas être protégé. Procédez comme suit :

1. Ouvrez Gestion de l’ordinateur, puis sélectionnez gestion du stockage pour qu’il répertorie la machine de hello disques toohello en ligne et attaché.
2. Sélectionnez la machine joint toohello hello disque temporaire et choisissez toobring hors connexion.

### <a name="protect-hello-vms"></a>Protéger les machines virtuelles de hello
1. Bonjour portail Azure, vérifiez États hello tooensure de machine virtuelle de hello qu’ils sont basculés.

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. Lancez vContinuum sur votre machine.

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. Cliquez sur **nouveau groupe de Protection** et sélectionnez le type de système d’opération hello, le
4. Dans hello nouvelle fenêtre qui s’ouvrent hello sélectionnez **type de système d’exploitation** > **obtenir les détails** hello machines virtuelles vous voulez toofail précédent. Dans **détails du serveur principal**, identifier et sélectionnez hello machines virtuelles que vous souhaitez tooprotect. Machines virtuelles sont répertoriés sous le nom d’hôte de vCenter hello qu’ils étaient avant le basculement.
5. Lorsque vous sélectionnez un ordinateur virtuel de tooprotect (et il a déjà basculé tooAzure) une fenêtre contextuelle fournit deux entrées pour la machine virtuelle de hello. Il s’agit, car le serveur de configuration hello détecte deux instances de tooit d’ordinateurs virtuels enregistrés hello. Vous avez besoin d’entrée de hello tooremove pour hello locaux VM afin que vous puissiez protéger hello machine virtuelle appropriée. tooidentify hello Azure VM correction ici, vous pouvez vous connecter à hello machine virtuelle Azure et accédez tooC:\Program fichiers (x86) \Microsoft Azure Site Recovery\Application Data\etc. Dans hello fichier drscout.conf, identifier les ID d’hôte hello. Dans la boîte de dialogue v-continuum hello, conserver hello entrée pour laquelle vous hello ID de l’hôte sur la machine virtuelle de hello. Supprimez toutes les autres entrées. tooselect hello corriger la machine virtuelle que vous pouvez faire référence à adresse IP de tooits. Hello IP adresse plage locale sera être hello local VM.

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. Sur le serveur vCenter hello arrêter la machine virtuelle de hello. Vous pouvez également supprimer hello machines virtuelles locales.
7. Spécifiez ensuite hello local MT server toowhich vous souhaitez tooprotect hello machines virtuelles. toodo, connecter toohello vCenter server toowhich vous souhaitez toofail précédent.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. Serveur cible maître de hello Select basée sur hello hôte toowhich vous souhaitez toorecover hello machine virtuelle.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. Fournir l’option de réplication hello pour chacun des ordinateurs virtuels hello. toodo cela vous devez tooselect hello récupération côté banque de données toowhich hello machines virtuelles seront récupérées. Hello tableau hello différentes options vous avez besoin de tooprovide pour chaque machine virtuelle.

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | **Option** | **Valeur recommandée d’option** |
   | --- | --- |
   |  Adresse IP du serveur de processus |Sélectionnez le serveur de processus hello déployé dans Azure |
   |  Retention size in MB | |
   |  Retention value |1 |
   |  Days/Hours |Jours |
   |  Intervalle de cohérence |1 |
   |  Sélectionner une banque de données cible |Hello banque de données disponible sur le site de récupération hello. magasin de données Hello doit disposer de suffisamment d’espace et d’hôte ESX toohello disponible sur lequel vous souhaitez toorestore hello virtual machine. |
10. Configurer hello propriétés hello d’ordinateur virtuel obtiendra après le site de basculement tooon local. propriétés de Hello sont résumées dans hello tableau suivant.

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | **Propriété** | **Détails** |
    | --- | --- |
    | Configuration réseau |Pour chaque carte réseau est détecté, sélectionnez-la et cliquez sur **modification** adresse d’IP tooconfigure hello la restauration automatique pour la machine virtuelle de hello. |
    | Hardware Configuration |Spécifiez hello UC et mémoire hello pour hello machine virtuelle. Paramètres peuvent être appliqués tooall hello machines virtuelles que vous essayez de tooprotect. tooidentify hello des valeurs correctes pour hello du processeur et mémoire, vous pouvez consultez taille de rôle des machines virtuelles IAAS toohello et nombre de hello de cœurs et de la mémoire affectée. |
    | Nom complet |Après la restauration automatique tooon local, vous pouvez renommer hello virtuels tels qu’ils apparaîtront dans l’inventaire de vCenter hello. Hello nom par défaut est hello machine virtuelle ordinateur hôte. nom de machine virtuelle tooidentify hello, liste de machine virtuelle toohello dans le groupe de Protection hello peut faire référence. |
    | NAT Configuration |Cette propriété est abordée en détail ci-dessous. |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a>Configurer des paramètres NAT
1. protection tooenable d’ordinateurs virtuels hello, deux canaux de communication doivent toobe établie. premier canal de Hello est entre la machine virtuelle de hello et serveur de processus hello. Ce canal collecte les données de hello de hello machine virtuelle et l’envoie toohello serveur de processus qui envoie ensuite hello serveur cible maître de toohello de données. Si le serveur de processus hello et hello toobe de machine virtuelle protégée sont sur hello même réseau virtuel Azure, vous n’avez pas besoin des paramètres NAT toouse. Dans le cas contraire, spécifiez les paramètres NAT. Afficher les adresse IP publique hello hello du serveur de traitement dans Azure.

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. deuxième canal de Hello est entre le serveur de processus hello et le serveur cible maître de hello. Hello option toouse NAT ou non dépend d’à l’aide d’une connexion VPN en fonction ou de la communication sur hello internet. Ne sélectionnez pas NAT si vous utilisez un réseau VPN, mais uniquement si vous utilisez une connexion Internet.

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. Si vous n’avez pas supprimé virtuels hello local tel que spécifié et que si hello le magasin de données que vous êtes toostill arrière du basculement contient hello ancien VMDK, vous devez alors tooensure que la restauration hello machine virtuelle est créée dans un nouvel emplacement. toodo cette sélection hello **avancé** paramètres et spécifiez un autre tooin de toorestore dossier **paramètres du nom de dossier**. Laissez hello autres options avec leurs paramètres par défaut. Appliquer hello dossier nom paramètres tooall hello serveurs.

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. Exécuter une vérification de la disponibilité tooensure que les machines virtuelles de hello sont prêt toobe protégé tooon locale précédent.

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. Attendez qu’elle toocomplete. S’il est correctement sur tous les ordinateurs virtuels, vous pouvez spécifier un nom pour le plan de protection hello. Puis cliquez sur **protéger** toobegin.

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. Vous pouvez surveiller la progression dans vContinuum.

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. Après l’étape de hello **activation d’un Plan de Protection** terminée, vous pouvez surveiller la protection des machines virtuelles dans le portail Site Recovery hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. Vous pouvez voir l’état exact de hello en cliquant sur la machine virtuelle de hello et la surveillance de sa progression.

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a>Préparer le plan de restauration automatique de hello
Vous pouvez préparer un plan de restauration automatique à l’aide de la v-continuum afin que l’application hello peut être toohello précédent a échoué sur site local à tout moment. Ces plans de récupération sont les plans de récupération toohello très similaire dans la récupération de Site.

1. Lancez vContinuum et sélectionnez **Gérer des plans** > **Récupérer.** Vous pouvez voir de la liste de tous les plans de hello qui ont été toofail utilisé sur les machines virtuelles. Vous pouvez utiliser hello même plans toorecover.

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. Sélectionnez plan de protection hello et tous hello machines virtuelles que vous souhaitez toorecover qu’il contient. Lorsque vous sélectionnez chaque ordinateur virtuel, vous pouvez voir plus d’informations, y compris VMware ESX hello cible et le disque de machine virtuelle source hello. Cliquez sur **suivant** toobegin hello Assistant Récupération et sélectionnez hello machines virtuelles toorecover.

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. Vous pouvez récupérer en fonction de plusieurs options, mais nous vous recommandons d’utiliser **dernière balise** et sélectionnez **appliquer pour toutes les machines virtuelles** tooensure qui hello les données les plus récentes de la machine virtuelle de hello sera utilisé.
4. Exécutez hello **vérification de la disponibilité.** Il vérifie si les paramètres appropriés hello sont tooenable configuré de récupération de machine virtuelle. Cliquez sur **suivant** si toutes les vérifications de hello réussissent. Si ce n’est pas hello journal et résoudre les erreurs de hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. Dans **Configuration d’ordinateur virtuel** vous assurer que les paramètres de récupération hello sont correctement définies. Vous pouvez modifier les paramètres de machine virtuelle hello si vous avez besoin.

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. Passez en revue la liste hello d’ordinateurs virtuels qui seront récupérés et spécifier un ordre de récupération. Notez que les machines virtuelles sont répertoriés à l’aide du nom d’hôte hello. Il peut être difficile de toomap hello ordinateur nom toohello machine virtuelle.
   noms de hello toomap, accédez toohello virtuels **tableau de bord** dans Azure et vérification de nom d’hôte de machine virtuelle hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. Spécifiez un nom de plan et sélectionnez **Récupérer plus tard**. Nous vous recommandons de toorecover, car la protection initiale de hello ne soient pas complet.
8. Cliquez sur **récupérer** toosave hello plan ou un déclencheur hello récupération si vous avez sélectionné toorecover maintenant et au plus tard. Vous pouvez vérifier hello récupération état toosee si le plan de hello été enregistré.

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a>Récupérer les machines virtuelles
Une fois le plan de hello créé, vous pouvez récupérer des machines virtuelles de hello. Avant que vous l’activez que hello virtual machines ont terminé la synchronisation. Si l’état de réplication indique OK ensuite la protection de hello est terminée et seuil RPO hello a été remplie. Vous pouvez vérifier l’intégrité de propriétés de machine virtuelle hello.

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

Désactiver hello machines virtuelles avant de vous lancez la récupération de hello. Ainsi, il n’existe aucun fractionnement et que les utilisateurs accéderont uniquement une copie de l’application hello.

1. Démarrez hello enregistré du plan. Dans la v-continuum sélectionnez **moniteur** hello plans. Celle-ci répertorie tous les plans de hello qui ont été exécutées.

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. Plan de sélection hello dans **récupération** et cliquez sur **Démarrer**. Vous pouvez surveiller la récupération. Une fois que les machines virtuelles ont été désactivées dans, vous pouvez vous connecter toothem dans le serveur vCenter.

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a>Protéger le tooAzure à nouveau après la restauration automatique
Une fois la restauration automatique terminée vous souhaiterez probablement tooprotect hello virtual machines à nouveau. Procédez comme suit :

1. Vérifiez que hello machines virtuelles locales fonctionnent et que les applications sont accessibles.
2. Dans le portail Azure Site Recovery hello, sélectionner des machines virtuelles hello et les supprimer. Sélectionnez toodisable hello la protection d’ordinateurs virtuels hello. Cela garantit que les machines virtuelles de hello ne sont pas plus protégés.
3. Dans Azure supprimer hello basculé de machines virtuelles
4. Supprimer les machine virtuelle ancien hello sur vSpehere. Il s’agit d’ordinateurs virtuels hello que vous avez basculé précédemment tooAzure.
5. Dans le portail Site Recovery hello protéger hello machines virtuelles ayant récemment basculé. Une fois qu’ils sont protégés vous pouvez les ajouter plan de récupération tooa.

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur](site-recovery-vmware-to-azure-classic.md) réplication des machines virtuelles VMware et tooAzure des serveurs physiques à l’aide du déploiement de hello améliorée.
