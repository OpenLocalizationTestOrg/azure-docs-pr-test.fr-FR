---
title: "aaaFailback les ordinateurs virtuels VMware à partir d’Azure site tooon | Documents Microsoft"
description: "En savoir plus sur l’échec des deux sites locaux toohello précédent après le basculement des ordinateurs virtuels VMware et tooAzure des serveurs physiques."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 5a47337f-89a9-43e8-8fdc-7da373c0fb0f
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: ruturajd
ms.openlocfilehash: 258f5a55252083135b2040e5a235fa1ffbf3b9d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site"></a>Échec des ordinateurs virtuels VMware arrière et des serveurs physiques toohello sur site local


Cet article décrit comment toofailback Azure machines virtuelles à partir du site local de toohello Azure. Suivez les instructions de hello ici quand vous êtes prêt toofail sauvegarder vos machines virtuelles VMware ou serveurs physiques Windows ou Linux après avoir protégé vos ordinateurs à l’aide de ce nouveau [référence](site-recovery-how-to-reprotect.md).

>[!NOTE]
>Si vous utilisez le portail Azure classic de hello, reportez-vous à tooinstructions mentionnées [ici](site-recovery-failback-azure-to-vmware-classic.md) pour l’architecture tooAzure VMware améliorée et [ici](site-recovery-failback-azure-to-vmware-classic-legacy.md) d’architecture hello hérité

## <a name="overview"></a>Vue d'ensemble
diagrammes Hello dans cette section montrent l’architecture de la restauration automatique hello pour ce scénario.

Lorsque hello serveur de processus est local et que vous utilisez une connexion Azure ExpressRoute, utilisez cette architecture :

![Diagramme d’architecture pour ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Lorsque hello serveur de processus est sur Azure et que vous avez un VPN ou une connexion ExpressRoute, utilisez cette architecture :

![Diagramme d’architecture pour VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Pour obtenir une liste complète des ports et diagramme d’architecture de la restauration automatique hello, consultez toohello suivant l’image :

![Liste des ports de basculement-restauration automatique](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Une fois que vous avez basculé tooAzure, vous ne parvenez pas tooyour arrière sur site local en trois étapes :

* **Étape 1**: Protégez-les de machines virtuelles de Azure hello pour qu’ils commencer la réplication des machines virtuelles VMware toohello précédent qui s’exécutent sur votre site local.
* **Étape 2**: une fois que vos machines virtuelles Azure sont répliquées tooyour un site local, vous exécutez un basculement toofail précédent à partir d’Azure.
* **Étape 3**: une fois que vos données a échoué en retour, vous protégez de nouveau hello sauvegarder des machines virtuelles locales que vous avez effectué, pour qu’ils commencer la réplication tooAzure.

### <a name="fail-back-toohello-original-location-or-an-alternate-location"></a>Emplacement d’origine du précédent toohello échouent ou un autre emplacement
Après avoir basculé une VM VMware, vous pouvez basculer toohello arrière même source de machine virtuelle si elle existe toujours sur site. Dans ce scénario, uniquement les deltas hello sont rétablies.

Si vous effectuez le basculement des serveurs physiques, la restauration automatique est toujours tooa nouveau VMware VM. Avant d’effectuer la restauration automatique d’un ordinateur physique, notez les points suivants :
* Un ordinateur physique protégé reviendra comme un ordinateur virtuel après un basculement à partir de tooVMware Azure. Une machine Windows Server 2008 R2 SP1, si elle est protégée et basculé tooAzure, ne peut pas être rétablie. Un ordinateur Windows Server 2008 R2 SP1 démarré, car un ordinateur virtuel local sera en mesure de toofail précédent.
* Assurez-vous que vous découvriez au moins un serveur cible maître avec hello pour les hôtes ESX/ESXi nécessaires que vous devez toofail revenir.

Si vous ne parvenez pas toohello précédent ordinateur virtuel d’origine, hello Voici requis :

* Si hello machine virtuelle est géré par un serveur vCenter, hello ESX hôte du serveur cible maître doit avoir accès toohello machines virtuelles banque de données.
* Si hello machine virtuelle se trouve sur un ordinateur hôte ESX, mais n’est pas géré par vCenter, disque dur de hello Hello machine virtuelle doit être dans une banque de données est accessible par l’hôte de hello de MT.
* Si votre machine virtuelle se trouve sur un ordinateur hôte ESX et n’utilise pas vCenter, détection de l’ordinateur hôte ESX hello Hello MT doit se terminer avant que vous protégez de nouveau. Cela s’applique également si vous restaurez automatiquement des serveurs physiques.
* Une autre option (si hello local machine virtuelle existe) est toodelete avant de procéder à une restauration automatique. La restauration automatique crée ensuite une nouvelle machine virtuelle sur hello le même hôte que l’ordinateur hôte ESX hello cible maître.

Lorsque vous ne parvenez pas tooan arrière autre emplacement, les données de salutation sont récupérée toohello même magasin de données et hello même ordinateur hôte ESX que celle utilisée par le serveur cible maître de local hello.

## <a name="prerequisites"></a>Composants requis
* toofail les ordinateurs virtuels VMware et serveurs physiques, vous avez besoin d’un environnement VMware. Échec en arrière tooa serveur physique n’est pas pris en charge.
* toofail précédent, vous devez avoir créé un réseau Azure lorsque vous définissez initialement la protection. La restauration automatique a besoin d’une connexion VPN ou ExpressRoute à partir de hello Azure réseau dans lequel hello machines virtuelles Azure sont toohello trouve un site local.
* Si hello machines virtuelles que vous souhaitez toofail sauvegarder tooare géré par un serveur vCenter, assurez-vous que vous disposez des autorisations hello requis pour la découverte d’ordinateurs virtuels sur les serveurs vCenter. Pour plus d’informations, consultez [les ordinateurs virtuels VMware de répliquer et tooAzure des serveurs physiques avec Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).
* Si des instantanés sont présents sur une machine virtuelle, la reprotection échouera. Vous pouvez supprimer les captures instantanées de hello ou des disques de hello.
* Avant de procéder à la restauration automatique, créez les composants suivants :
  * **Créez un serveur de processus dans Azure**. Il s’agit d’une machine virtuelle Azure que vous créez et maintenez en cours d’exécution pendant la restauration automatique. Vous pouvez supprimer hello machine virtuelle une fois la restauration automatique terminée.
  * **Créer un serveur cible maître**: serveur cible maître de hello envoie et reçoit des données de la restauration automatique. serveur d’administration Hello que vous avez créé sur site possède un serveur cible maître qui est installé par défaut. Toutefois, en fonction du volume hello du trafic de sauvegarde a échoué, vous devrez peut-être toocreate un serveur cible maître distinct pour la restauration automatique.
  * toocreate un serveur cible maître supplémentaires qui s’exécute sur Linux, configurez hello Linux VM avant d’installer le serveur cible maître de hello, comme décrit plus loin.
* Le serveur de configuration est requis en local lorsque vous effectuez une restauration automatique. Lors du retour arrière, machine virtuelle de hello doit exister dans la base de données de serveur de configuration hello. Si la base de données de serveur de configuration hello ne contient aucune machine virtuelle, la restauration automatique ne peut pas réussir. Vous devez donc veiller à planifier une sauvegarde régulière de votre serveur. En cas de sinistre, vous devez toorestore avec hello d’adresses IP même afin que la restauration automatique fonctionne.
* Définition des paramètres de disk.enableUUID=true hello pour **les paramètres de Configuration** du maître de hello cibler les ordinateurs virtuels dans les environnements VMware. Si cette ligne n’existe pas, ajoutez-la. Ce paramètre est requis tooprovide un fichier de disque (VMDK) d’ordinateur virtuel de toohello identificateur unique universel (UUID) cohérente afin qu’il est monté correctement.
* Tenez compte d’un « maître serveur cible ne peut pas être vMotioned de stockage « condition, ce qui peut entraîner des toofail de la restauration automatique hello. Hello machine virtuelle ne peut pas démarrer car les disques hello ne sont pas apportées tooit disponible.
* Ajouter un lecteur, appelé un lecteur de rétention sur le serveur cible maître de hello. Ajouter un disque et formater le lecteur hello.

## <a name="failback-policy"></a>Stratégie de restauration automatique
tooreplicate arrière tooon local, vous devez une stratégie de restauration automatique. stratégie de Hello est créé automatiquement lorsque vous créez une stratégie du haut vers le bas, et il est automatiquement associé au serveur de configuration hello. Elle n’est pas modifiable. stratégie de Hello a hello suivant les paramètres de réplication :

* Seuil d’objectif de point de récupération : 15 minutes
* Rétention de point de récupération : 24 heures
* Fréquence des instantanés de cohérence au niveau application : 60 minutes

 ![Paramètres de réplication de la stratégie de restauration automatique hello](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

## <a name="set-up-a-process-server-in-azure"></a>Configurer un serveur de processus dans Azure
Installer un serveur de traitement dans Azure afin que les machines virtuelles de Azure hello peut envoyer le serveur cible maître local hello données toohello précédent.

Si vous avez protégé vos machines virtuelles en tant que ressources classiques (autrement dit, hello machine virtuelle récupérée dans Azure est un ordinateur virtuel qui a été créé à l’aide du modèle de déploiement classique hello), vous avez besoin d’un serveur de traitement dans Azure. Si vous avez récupéré hello machines virtuelles Azure Resource Manager en tant que type de déploiement hello, hello processus serveur doit avoir le Gestionnaire de ressources en tant que type de déploiement hello. Hello type de déploiement est sélectionné par hello Azure réseau virtuel que vous déployez hello processus serveur.

1. Dans **coffre** > **paramètres** > **Infrastructure de la récupération de sites** (sous **gérer**) > **Serveurs de configuration** (sous **pour VMware et des Machines physiques**), sélectionnez le serveur de configuration hello.
2. Cliquez sur **Serveur de processus**.

  ![Bouton Serveur de processus](./media/site-recovery-failback-azure-to-vmware-classic/add-processserver.png)
3. Choisissez toodeploy hello du serveur de traitement en tant que **déployer une restauration automatique du serveur de traitement dans Azure**.
4. Sélectionnez l’abonnement hello que vous avez récupéré des machines virtuelles hello.
5. Sélectionnez hello réseau Azure que vous avez récupéré des machines virtuelles hello. Hello processus serveur doit toobe Bonjour que même réseau afin que hello récupéré des machines virtuelles et hello processus serveur peut communiquer.
6. Si vous avez sélectionné un *modèle de déploiement classique* réseau, créez une machine virtuelle via hello Azure Marketplace, puis installez hello serveur de processus qu’elle contient.

 ![fenêtre de « Serveur de processus ajouter » Hello](./media/site-recovery-failback-azure-to-vmware-classic/add-classic.png)

 Lorsque vous créez hello serveur de processus, de paie suivant de toohello attention :
 * le nom de l’image de hello Hello est *Microsoft Azure Site Recovery processus serveur V2*. Sélectionnez **classique** en tant que modèle de déploiement hello.

       ![Select "Classic" as hello Process Server deployment model](./media/site-recovery-failback-azure-to-vmware-classic/templatename.png)
 * Hello serveur de processus conséquente toohello les instructions d’installation dans [les ordinateurs virtuels VMware de répliquer et tooAzure des serveurs physiques avec Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).
7. Si vous sélectionnez hello *le Gestionnaire de ressources* Azure réseau, déployer hello serveur de processus en fournissant hello informations suivantes :

  * nom Hello hello du groupe de ressources que vous voulez toodeploy hello server
  * nom Hello du serveur de hello
  * Un nom d’utilisateur et un mot de passe pour établir la connexion toohello server
  * compte de stockage Hello que vous voulez toodeploy hello server
  * sous-réseau de Hello et interface de réseau hello que vous souhaitez tooconnect tooit
   >[!NOTE]
   >Vous devez créer votre propre [interface réseau](../virtual-network/virtual-networks-multiple-nics.md) (NIC) et sélectionnez alors que vous déployez hello serveur de processus.

    ![Entrez les informations dans la boîte de dialogue « Ajouter un processus serveur » hello](./media/site-recovery-failback-azure-to-vmware-classic/psinputsadd.png)

8. Cliquez sur **OK**. Cette action déclenche une tâche qui crée un ordinateur virtuel de gestionnaire de ressources du déploiement type pendant l’installation du serveur de processus hello. tooregister hello toohello configuration serveur, le programme d’installation de hello exécution à l’intérieur de hello machine virtuelle en suivant les instructions de hello dans [les ordinateurs virtuels VMware de répliquer et tooAzure des serveurs physiques avec Azure Site Recovery](site-recovery-vmware-to-azure-classic.md). Un Bonjour toodeploy de travail serveur de processus est également déclenché.

  Serveur de processus Hello est répertorié sur hello **serveurs de Configuration** > **serveurs associés** > **serveurs de processus** onglet.

    ![](./media/site-recovery-failback-azure-to-vmware-new/pslistingincs.png)

    > [!NOTE]
    > Hello serveur de processus n’est pas visible sous **propriétés de la machine virtuelle**. Il n’est visible uniquement sur hello **serveurs** onglet dans le serveur d’administration hello il est enregistré dans. Il peut prendre 10 minutes too15 tooappear du serveur de processus hello.


## <a name="set-up-hello-master-target-server-on-premises"></a>Configurer la cible maître hello/server sur site
serveur cible maître de Hello reçoit les données de la restauration automatique hello. Hello serveur est automatiquement installé sur le serveur d’administration local hello, mais si vous êtes échouent dans trop de données, vous devrez peut-être tooset d’un serveur cible maître supplémentaires. tooset une maître cibler le serveur local, hello suivant :

> [!NOTE]
> tooset d’un serveur cible maître sur Linux, ignorer la procédure suivante de toohello. Utilisez uniquement CentOS 6.6 système d’exploitation minimal comme hello cible maître du système d’exploitation.

1. Si vous installez le serveur cible maître de hello sur Windows, ouvrez la page de démarrage rapide de hello de hello machine virtuelle que vous installez un serveur cible maître de hello sur.
2. Télécharger le fichier d’installation hello pour l’Assistant d’installation de Unified Azure Site Recovery hello.
3. Exécutez le programme d’installation hello et, dans **avant de commencer**, sélectionnez **ajouter tooscale de serveurs de traitement supplémentaire déploiement**.
4. Assistant hello complète Bonjour même façon que lorsque vous [configurer le serveur d’administration hello](site-recovery-vmware-to-azure-classic.md). Sur hello **détails du serveur Configuration** page, spécifiez l’adresse IP de hello du serveur cible maître de hello et entrez un Bonjour tooaccess de phrase secrète machine virtuelle.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Configurer un VM Linux en tant que serveur cible maître de hello
tooset serveur de gestion hello exécutant le serveur cible maître de hello comme un VM Linux, installez hello CentOS 6.6 minimale du système d’exploitation. Ensuite, extraire des ID de SCSI hello pour chaque disque SCSI, installer des packages supplémentaires et appliquer des modifications personnalisées.

#### <a name="install-centos-66"></a>Installer CentOS 6.6

1. Installez hello CentOS 6.6 minimale du système d’exploitation sur le serveur d’administration hello machine virtuelle. Conserver hello ISO sur un lecteur de DVD et hello système de démarrage. Ignorer les tests de support hello. Sélectionnez **anglais (États-Unis)** en tant que langage de hello, sélectionnez **périphériques de stockage de base**, vérifiez que le disque dur de hello ne comporte aucune donnée importante, cliquez sur **Oui**et ignorer les données. Entrez le nom d’hôte hello hello du serveur d’administration et sélectionnez la carte réseau du serveur hello.  Bonjour **système de montage** boîte de dialogue, sélectionnez **me connecter automatiquement**, puis ajoutez les paramètres DNS, réseau et une adresse IP statique. Spécifiez un fuseau horaire. tooaccess hello serveur d’administration, entrez le mot de passe racine hello.
2. Lorsque vous êtes invité à quel type d’installation que vous souhaitez, sélectionnez **créer une disposition de personnalisée** en tant que partition de hello. Cliquez sur **Suivant**. Sélectionnez **Free** (Libre), puis cliquez sur **Créer**. Créez les partitions **/**,  **/var/crash** et **/home** avec **FS Type:** **ext4**. Créer la partition d’échange hello en tant que **FS Type : échange**.
3. Si des appareils préexistants sont trouvés, un message d’avertissement s’affiche. Cliquez sur **Format** lecteur de hello tooformat avec les paramètres de partition hello. Cliquez sur **écriture modifier toodisk** modifications de partition tooapply hello.
4. Sélectionnez **chargeur de démarrage d’installation** > **suivant** tooinstall chargeur de démarrage hello sur la partition racine hello.
5. Lors de l’installation de hello est terminée, cliquez sur **redémarrer**.

#### <a name="retrieve-hello-scsi-ids"></a>Récupérer des ID SCSI hello

1. Après l’installation de hello, récupérer des ID SCSI hello pour chaque disque SCSI Bonjour machine virtuelle. toodo arrêté, le serveur d’administration hello machine virtuelle. Dans les propriétés de machine virtuelle hello dans VMware, cliquez sur entrée de machine virtuelle hello > **modifier les paramètres** > **Options**.
2. Sélectionnez **Avancé** > **Général**, puis cliquez sur **Paramètres de configuration**. Cette option n’est pas disponible lors de la machine de hello est en cours d’exécution. Pour toobe d’option hello disponible, machine de hello doit être arrêté.
3. Effectuez une des manières suivantes les hello :
 * Si hello ligne **disque. EnableUUID** existe, vérifiez que hello a la valeur trop**True** (sensible à la casse). Si la valeur de hello est déjà défini tooTrue, vous pouvez annuler et tester la commande hello SCSI à l’intérieur d’un système d’exploitation invité après que qu’il est démarré.
 * Si hello ligne **disque. EnableUUID** n’existe pas, cliquez sur **ajouter une ligne**, puis ajoutez-le avec hello **True** valeur. N’utilisez pas de guillemets doubles.

#### <a name="install-additional-packages"></a>Installer des packages supplémentaires
Téléchargez et installez des packages supplémentaires.

1. Assurez-vous que le serveur cible maître de hello est connecté toohello Internet.
2. toodownload et les packages d’installation de 15 à partir du référentiel de CentOS hello, exécutez la commande suivante : `# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools`.
3. Si les ordinateurs source hello que vous protégez sont en cours d’exécution Linux avec un Reiser ou XFS système pour le périphérique de démarrage ou de la racine de hello de fichiers, téléchargez et installez les packages supplémentaires comme suit :

   * \# cd /usr/local
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * \# rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * \# wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * \# rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm
   * \#YUM installer MPIO de mappeur de périphérique (packages MPIO tooenable requis sur le serveur cible maître de hello)

#### <a name="apply-custom-changes"></a>Appliquer des modifications personnalisées
Après avoir terminé les étapes de post-installation hello et les packages installés hello, appliquer des modifications personnalisées de manière hello suivante :

1. Copiez hello RHEL 6-64 unifiée de l’Agent toohello binaire machine virtuelle. hello toountar binaire, exécutez la commande suivante : `tar –zxvf <file name>`.
2. autorisations de toogive, exécutez la commande suivante : `# chmod 755 ./ApplyCustomChanges.sh`.
3. Exécution hello suivants script : `# ./ApplyCustomChanges.sh`. Exécutez-le une seule fois. Une fois qu’il s’exécute correctement, redémarrez serveur de hello.

## <a name="run-hello-failback"></a>Exécuter la restauration automatique de hello
### <a name="reprotect-hello-azure-vms"></a>Rétablissez les machines virtuelles de Azure hello
1. Dans **coffre**, dans **éléments répliqués**, hello machine virtuelle qui a été basculé d’avec le bouton droit, puis sélectionnez **Reprotéger**.
2. Dans Panneau de hello, vous pouvez voir cette direction hello de protection **tooOn local Azure** est déjà sélectionné.
3. Dans **serveur cible maître** et **serveur de processus**hello du serveur de processus de machine virtuelle Azure et sélectionnez le serveur cible maître de local hello.
4. Sélectionnez hello le magasin de données que vous souhaitez les disques hello toorecover locale vers. Utilisez cette option lorsque hello local machine virtuelle est supprimée et que vous devez toocreate nouveaux disques. Ignorer l’option de hello si hello disques existent déjà, mais vous devez toospecify une valeur.
5. Utilisez une rétention lecteur toostop hello points où hello machine virtuelle est répliquée local tooon précédent. Vous trouverez ci-après quelques critères d’un lecteur de rétention. Sans ces critères, le lecteur de hello n’est pas répertorié pour le serveur cible maître de hello.

  * Le volume ne doit pas être utilisé à d’autres fins (cible de réplication, etc.).
  * Le volume ne doit pas être en mode de verrouillage.
  * Le volume ne doit pas être un volume de cache. (installation du serveur cible maître hello ne doit pas exister sur ce volume. Hello du serveur de traitement plus master volume d’installation personnalisée de cible n’est pas éligible pour le volume de rétention. Ici, hello installé le serveur de processus ainsi que le volume cible maître est le volume de cache hello du serveur cible maître hello.)
  * type de système de fichiers de volume Hello ne doivent pas être FAT et FAT32.
  * capacité du volume Hello doit être différente de zéro.
  * volume de rétention par défaut Hello pour Windows est un volume de R.
  * volume de rétention par défaut Hello pour Linux est /mnt/retention.

6. stratégie de restauration automatique Hello est sélectionné automatiquement.
7. Après avoir cliqué sur **OK** toobegin reprotection, un travail commence tooreplicate hello machine virtuelle à partir du site local de toohello Azure. Vous pouvez suivre la progression de hello sur hello **travaux** onglet.

Si vous souhaitez toorecover tooan autre emplacement, sélectionnez le lecteur de rétention hello et magasin de données qui sont configurés pour le serveur cible maître de hello. Lorsque vous ne parvenez pas toohello arrière sur site local, hello les ordinateurs virtuels VMware dans un plan de protection de la restauration automatique hello utiliser hello même magasin de données en tant que serveur cible maître de hello. Si vous souhaitez toorecover hello réplica Azure VM toohello même local machine virtuelle, hello local machine virtuelle doit déjà être dans hello même magasin de données en tant que serveur cible maître de hello. En l’absence de machine virtuelle locale, une nouvelle machine virtuelle de ce type est créée pendant la reprotection.

![Sélectionnez « Azure local tooon » dans le menu déroulant de hello](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

Vous pouvez également effectuer la reprotection au niveau du plan de récupération. Si vous avez un groupe de réplication, il peut être reprotégé uniquement à l’aide d’un plan de récupération. Lorsque vous protégez de nouveau à l’aide d’un plan de récupération, utilisez les valeurs précédentes hello pour chaque ordinateur protégé.

> [!NOTE]
> Groupes de réplication doivent être protégés avec hello même cible maître. Si ce n’est pas le cas, aucun point dans le temps commun ne pourra être défini pour ces groupes.

### <a name="run-a-failover-toohello-on-premises-site"></a>Exécuter un basculement toohello sur site local
Une fois que vous protégez de nouveau hello machine virtuelle, vous pouvez lancer un basculement à partir d’Azure tooon local.

1. Sur la page d’éléments répliqués hello, avec le bouton droit hello virtual machine, puis **basculement non planifié**.
2. Dans **confirmer le basculement**, vérifiez le sens du basculement hello (à partir de Azure), puis sélectionnez le point de récupération hello que vous souhaitez toouse pour le basculement hello (hello plus récentes ou hello dernier cohérents au niveau de l’application de point de récupération). Un point de récupération cohérents avec l’application se produit avant le point le plus récent hello dans le temps, et il entraîne une perte de données.
3. Pendant le basculement, récupération de Site arrête hello machines virtuelles Azure. Après avoir vérifié que la restauration a été effectuée comme prévu, vous pouvez vérifier tooensure hello Azure VM a été arrêté comme prévu.

### <a name="reprotect-hello-on-premises-site"></a>Protégez de nouveau site local de hello
Une fois la restauration automatique terminée, validation hello machine virtuelle tooensure qui hello récupérées dans Azure de machines virtuelles sont supprimés. toodo, élément de hello protégé d’avec le bouton droit, puis cliquez sur **valider**. Cette action déclenche une tâche qui supprime les ordinateurs virtuels récupérée ancien hello dans Azure.

Après la fin de la validation de hello, vos données doivent être sur site local de hello, mais il ne sera pas être protégé. là encore, tooAzure de réplication toostart hello suivant :

1. Dans **coffre**, dans **paramètre** > **éléments répliqués**, sélectionnez les ordinateurs virtuels hello qui ont échoué précédent, puis cliquez sur **Reprotéger**.
2. Affectez la valeur hello hello serveur de processus qui a besoin de toobe utilisé toosend données back tooAzure à.
3. Cliquez sur **OK**.

Une fois terminée la reprotection de hello, hello VM réplique tooAzure précédent et vous pouvez effectuer un basculement.

### <a name="resolve-common-failback-issues"></a>Résoudre les problèmes courants lors de la restauration automatique
* Si vous effectuez une découverte vCenter en mode lecture seule utilisateur et protégez des machines virtuelles, l’opération réussit et le basculement fonctionne. Lors de la reprotection, basculement échoue, car il est hello banques de données ne peut pas être découvert. Comme un symptôme, vous ne verrez pas les magasins de données hello répertorié au cours de la reprotection. tooresolve ce problème, vous pouvez mettre à jour des informations d’identification de vCenter hello avec un compte approprié qui dispose des autorisations et recommencez la tâche de hello. Pour plus d’informations, consultez [les ordinateurs virtuels VMware de répliquer et tooAzure des serveurs physiques avec Azure Site Recovery](site-recovery-vmware-to-azure-classic.md)
* Lorsque vous restaurez un VM Linux et l’exécuter localement, vous pouvez voir que ce package du Gestionnaire de réseau hello a été désinstallé de la machine de hello. Cette désinstallation se produit, car le package du Gestionnaire de réseau hello est supprimé lors de la récupération hello machine virtuelle dans Azure.
* Lorsqu’une machine virtuelle est configurée avec une adresse IP statique et est basculée tooAzure, adresse IP de hello est acquis via DHCP. Lorsque vous basculez tooon locale précédent, hello machine virtuelle continue à adresse IP de toouse DHCP tooacquire hello. Manuellement, connectez-vous à toohello ordinateur et affecter hello tooa arrière statique adresse si nécessaire.
* Si vous utilisez la version gratuite d’ESXi 5.5 ou de vSphere 6 Hypervisor, le basculement aboutira, mais pas la restauration automatique. restauration automatique tooenable, la licence d’évaluation du programme de mise à niveau tooeither.
* Si vous ne pouvez pas contacter le serveur de configuration de hello de hello serveur de processus, vérifiez le serveur de configuration de connectivité toohello en Telnet toohello configuration du serveur sur le port 443. Vous pouvez également essayer le serveur de configuration tooping hello à partir de l’ordinateur du serveur de processus hello. Un serveur de processus doit également avoir une pulsation lorsqu’il est le serveur de configuration toohello connecté.
* Si vous essayez de vCenter de remplacement toofail tooan arrière, assurez-vous que votre nouveau vCenter est détecté et que le serveur cible maître hello est également détecté. Courant est que les banques de données hello ne sont pas accessibles ou visibles Bonjour **Reprotéger** boîte de dialogue.
* Un ordinateur WS2008R2SP1 qui est protégé comme un ordinateur physique local ne peut pas être ayant échoué depuis Azure tooon local.

## <a name="fail-back-with-expressroute"></a>Effectuer une restauration automatique avec ExpressRoute
Vous pouvez effectuer une restauration automatique à l’aide d’une connexion VPN ou ExpressRoute. Si vous souhaitez toouse une connexion ExpressRoute, notez hello qui suit :

* Hello connexion ExpressRoute doit être configurée sur hello réseau virtuel Azure que les ordinateurs source hello basculent tooand où hello machines virtuelles Azure sont situés après le basculement hello.
* Les données sont répliquée tooan compte de stockage Azure sur un point de terminaison public. toouse une connexion ExpressRoute, configurer l’homologation publique dans ExpressRoute avec le centre de données cible hello pour la réplication de la récupération de Site.
