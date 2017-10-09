---
title: "aaaFail sauvegarder des ordinateurs virtuels VMware à partir d’Azure dans le portail classique de hello | Documents Microsoft"
description: "En savoir plus sur l’échec des deux sites locaux toohello précédent après le basculement des ordinateurs virtuels VMware et tooAzure des serveurs physiques."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 7ca86e21-7a5d-45ab-8f4b-e42da90f199a
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 80bc3ab2708a5df953c6532b353da19a4c44ac34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site-classic-portal"></a>Échec des ordinateurs virtuels VMware arrière et des serveurs physiques toohello sur site local (portail classique)
> [!div class="op_single_selector"]
> * [portail Azure](site-recovery-failback-azure-to-vmware.md)
> * [Portail Azure Classic](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portail Azure Classic (version héritée)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Cet article explique comment toofail sauvegarder des machines virtuelles à partir du site local de toohello Azure. Suivez les instructions dans cet article lorsque vous êtes prêt toofail hello sauvegarder vos machines virtuelles VMware ou les serveurs physiques Windows/Linux après avoir basculé de hello local site tooAzure à l’aide de ce [didacticiel](site-recovery-vmware-to-azure-classic.md).

## <a name="overview"></a>Vue d'ensemble
Ce diagramme illustre l’architecture de la restauration automatique hello pour ce scénario.

Utilisez cette architecture lorsque le serveur de processus hello est local et que vous utilisez un ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Utilisez cette architecture lorsque le serveur de processus hello est sur Azure et vous disposez d’un réseau privé virtuel ou une connexion ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

image toohello ci-dessous font référence le toosee hello la liste complète des ports et diagramme d’architecture du hello la restauration automatique

![](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Voici comment fonctionne la restauration automatique :

* Une fois que vous avez basculé tooAzure, vous ne parvenez pas tooyour arrière sur site local en quelques étapes :
  * **Étape 1**: Protégez-les de machines virtuelles de Azure hello pour qu’ils commencer la réplication des machines virtuelles de tooVMware arrière en cours d’exécution dans votre site local. L’activation de la reprotection, hello machine virtuelle déplace dans un groupe de protection de la restauration automatique a été créé automatiquement lorsque vous avez créé le groupe de protection de basculement hello. Si vous avez ajouté votre plan de récupération de basculement protection groupe tooa groupe de protection hello la restauration automatique a été ajouté automatiquement toohello plan.  Au cours de reprotection vous spécifiez comment tooplan toofail sauvegarder.
  * **Étape 2**: une fois que vos machines virtuelles Azure répliquez tooyour sur site local, vous exécutez un basculement sur toofail à partir d’Azure.
  * **Étape 3**: une fois que vos données a échoué en retour, vous protégez de nouveau hello sauvegarder des machines virtuelles locales que vous avez effectué, pour qu’ils commencer la réplication tooAzure.


  [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failback/player]

### <a name="failback-toohello-original-or-alternate-location"></a>Emplacement d’origine ou sur un autre du toohello la restauration automatique
Si vous avez basculé une VM VMware vous pouvez échouer toohello arrière même source de machine virtuelle si elle existe toujours sur site. Dans ce scénario, seules les modifications différentielles hello va échouer précédent. Notez les points suivants :

* Si vous effectuez le basculement des serveurs physiques, la restauration automatique est toujours tooa nouveau VMware VM.
  * Avant d’effectuer la restauration automatique d’un ordinateur physique, notez les points suivants :
  * Ordinateur physique protégé reviendra comme un ordinateur virtuel après un basculement depuis Azure tooVMware
  * Assurez-vous que vous découvriez au moins une cible maître serveur en même temps que nécessaire toowhich de hôtes ESX/ESXi hello vous devez toofailback.
* Si vous effectuez une restauration automatique toohello d’origine VM hello Voici requis :

  * Si la machine virtuelle hello est gérée par un serveur vCenter ordinateur hôte ESX hello principale cible doit avoir accès toohello machines virtuelles banque de données.
  * Si hello machine virtuelle se trouve sur un ordinateur hôte ESX, mais n’est pas géré par vCenter puis disque hello Hello machine virtuelle doit être dans un magasin de données accessible par l’hôte de hello de MT.
  * Si votre machine virtuelle se trouve sur un ordinateur hôte ESX et n’utilise pas vCenter vous devez effectuer la détection de l’ordinateur hôte ESX hello Hello MT avant que vous protégez de nouveau. Cela s’applique également si vous restaurez automatiquement des serveurs physiques.
  * Une autre option (si hello local machine virtuelle existe) est toodelete avant de procéder à une restauration automatique. Puis la restauration automatique crée ensuite une nouvelle machine virtuelle sur hello le même hôte que l’ordinateur hôte ESX hello cible maître.
* Lorsque la restauration automatique tooan autre emplacement hello données sera récupérée toohello même magasin de données et hello même ordinateur hôte ESX que celle utilisée par le serveur cible maître de local hello.

## <a name="prerequisites"></a>Composants requis
* Vous aurez besoin d’un environnement VMware dans l’ordre toofail les ordinateurs virtuels VMware et de serveurs physiques. Échec en arrière tooa serveur physique n’est pas pris en charge.
* Dans commande toofail précédent vous devez avoir créé un réseau Azure lorsque vous définissez initialement la protection. La restauration automatique a besoin d’une connexion VPN ou ExpressRoute à partir de hello Azure réseau dans lequel hello machines virtuelles Azure sont toohello trouve un site local.
* Machines virtuelles de hello souhaitée toofail arrière tooare est géré par un serveur vCenter, vous devez toomake que vous disposez des autorisations de hello requis pour la découverte d’ordinateurs virtuels sur les serveurs vCenter. [En savoir plus](site-recovery-vmware-to-azure-classic.md).
* Si des instantanés sont présents sur une machine virtuelle, la reprotection échoue. Vous pouvez supprimer les captures instantanées de hello ou des disques de hello.
* Avant que vous effectuez une restauration automatique, vous devez toocreate un certain nombre de composants :
  * **Créez un serveur de processus dans Azure**. Il s’agit d’une machine virtuelle Azure, vous devez toocreate et de s’exécuter pendant la restauration automatique. Vous pouvez supprimer la machine de hello après que la restauration est terminée.
  * **Créer un serveur cible maître**: serveur cible maître de hello envoie et reçoit des données de la restauration automatique. serveur d’administration Hello vous créée sur site possède un serveur cible maître installé par défaut. Toutefois, en fonction du volume hello du trafic précédent a échoué, vous devrez peut-être toocreate un serveur cible maître distinct pour la restauration automatique.
  * Si vous voulez toocreate un serveur cible maître supplémentaires en cours d’exécution sur Linux, vous devez tooset des hello Linux VM avant d’installer le serveur cible maître de hello, comme décrit ci-dessous.
* Le serveur de configuration est requis en local lorsque vous effectuez une restauration automatique. Lors du retour arrière, hello virtual machine doit exister dans hello Configuration serveur base de données échouent lesquelles la restauration ne soit correcte. Vous devez donc veiller à planifier une sauvegarde régulière de votre serveur. En cas de sinistre, vous devez toorestore avec hello même adresse IP afin que la restauration automatique fonctionne.

## <a name="set-up-hello-process-server-in-azure"></a>Configurer le serveur de processus hello dans Azure
Vous devez tooinstall un serveur de traitement dans Azure afin que machines virtuelles de Azure hello puisse envoyer le serveur cible maître de hello données tooon locale précédent.

1. Dans le portail Site Recovery hello > **serveurs de Configuration** sélectionnez tooadd un nouveau serveur de processus.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps1.png)
2. Spécifiez un nom de serveur de traitement, puis entrez un nom et un mot de passe vous utiliserez tooconnect toohello machine virtuelle Azure en tant qu’administrateur. Dans **serveur de Configuration** sélectionnez serveur d’administration local hello et spécifiez hello Azure réseau dans le hello serveur de processus doit être déployé. Il doit s’agir réseau hello dans lequel se trouvent les machines virtuelles de Azure hello. Spécifiez une adresse IP unique à partir du sous-réseau de select hello et commencer le déploiement.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps2.png)

   Un serveur de processus de travail toodeploy hello est déclenché.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps3.png)

   Après hello serveur de processus est déployé dans Azure, vous pouvez vous connecter sur celui-ci à l’aide des informations d’identification hello spécifié. Hello première fois que vous ouvrez une session dans la boîte de dialogue hello processus serveur s’exécute. Tapez Bonjour adresse IP du serveur d’administration local hello et son mot de passe. Laissez le paramètre de port 443 par défaut hello. Vous pouvez également laisser de hello port de 9443 par défaut pour la réplication de données, sauf si en particulier, vous avez modifié ce paramètre lorsque vous configurez le serveur d’administration local hello.

   > [!NOTE]
   > serveur de Hello n’est pas visible sous **propriétés de la machine virtuelle**. Il est uniquement visible sous hello **serveurs** onglet toowhich de serveur de gestion hello est inscrite. Il peut prendre environ 10-15 min pour tooappear de serveur de processus hello.
   >
   >

## <a name="set-up-hello-master-target-server-on-premises"></a>Configurer la cible maître hello/server sur site
serveur cible maître de Hello reçoit les données de la restauration automatique hello. Un serveur cible maître est automatiquement installé sur le serveur d’administration local hello, mais si vous êtes échoue une grande quantité de données, vous devrez peut-être tooset d’un serveur cible maître supplémentaires. Procédez comme suit :

> [!NOTE]
> Si vous voulez tooinstall un serveur cible maître sur Linux, suivez les instructions de hello dans la procédure suivante de hello.
>
>

1. Si vous installez sur Windows server du serveur cible maître hello, ouvrir la page de démarrage rapide de hello dans hello la machine virtuelle sur lequel vous installez serveur cible maître de hello et téléchargez le fichier d’installation hello pour l’Assistant d’installation de Unified Azure Site Recovery hello.
2. Exécutez le programme d’installation et dans **avant de commencer** sélectionnez **ajouter tooscale de serveurs de processus supplémentaire déploiement**.
3. Assistant hello complète Bonjour même façon que lorsque vous [configurer le serveur d’administration hello](site-recovery-vmware-to-azure-classic.md). Sur hello **détails du serveur de Configuration** , spécifiez l’adresse IP de hello de ce serveur cible maître et un Bonjour tooaccess de phrase secrète machine virtuelle.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Configurer un VM Linux en tant que serveur cible maître de hello
tooset serveur de gestion hello serveur cible maître de hello en cours d’exécution en tant qu’une machine virtuelle, vous devez tooinstall hello Cent Linux) S 6.6 système d’exploitation minimal, extraire des ID de SCSI hello pour chaque disque SCSI, installer des packages supplémentaires et appliquer des modifications personnalisées.

#### <a name="install-centos-66"></a>Installer CentOS 6.6
1. Installez hello CentOS 6.6 minimale du système d’exploitation sur le serveur d’administration hello machine virtuelle. Conserver hello ISO dans un système de hello de démarrage et le lecteur de DVD. Skip hello média est un test, sélectionnez anglais (États-Unis) au langage hello, sélectionnez **périphériques de stockage de base**, vérifiez que le disque dur de hello n’y a aucune donnée importante et cliquez sur **Oui**, ignorer les données. Entrez le nom d’hôte hello hello du serveur d’administration et sélectionnez la carte réseau du serveur hello.  Bonjour **système de montage** boîte de dialogue Sélectionnez ** se connecter automatiquement ** et ajouter une adresse IP statique, réseau et les paramètres DNS. Spécifiez un fuseau horaire et un serveur d’administration racine mot de passe tooaccess hello.
2. Lorsque vous devez confirmer la type hello d’installation vous sélectionnez **créer une disposition de personnalisée** en tant que partition de hello. Après avoir cliqué sur **Suivant** select **Libre** et cliquez sur Créer. Créez les partitions **/**,  **/var/crash** et **/home** avec **FS Type:** **ext4**. Créer la partition d’échange hello en tant que **FS Type : échange**.
3. Si des appareils préexistants sont trouvés, un message d’avertissement s’affiche. Cliquez sur **Format** lecteur de hello tooformat avec les paramètres de partition hello. Cliquez sur **écriture modifier toodisk** modifications de partition tooapply hello.
4. Sélectionnez **chargeur de démarrage d’installation** > **suivant** tooinstall chargeur de démarrage hello sur la partition racine hello.
5. Une fois l’installation terminée, cliquez sur **Redémarrer**.

#### <a name="retrieve-hello-scsi-ids"></a>Récupérer des ID SCSI hello
1. Après l’installation d’extraire des ID de SCSI hello pour chaque disque SCSI Bonjour machine virtuelle. toodo cette arrêter le serveur d’administration hello VM, Bonjour VM propriétés dans les environnements VMware avec le bouton droit entrée de machine virtuelle hello > **modifier les paramètres** > **Options**.
2. Sélectionnez **Avancé** > **Général**, puis cliquez sur **Paramètres de configuration**. Cette option sera de-active lors de la machine de hello est en cours d’exécution. toomake informatique machine de hello active doit être arrêté.
3. Si hello ligne **disque. EnableUUID** existe Assurez-vous hello a la valeur trop**True** (sensible à la casse). S’il s’agit déjà, vous pouvez annuler et tester la commande hello SCSI à l’intérieur d’un système d’exploitation invité après que qu’il est démarré.
4. Si les lignes hello n’est pas existant Cliquez **ajouter une ligne** – et ajoutez-le avec hello **True** valeur. N’utilisez pas de guillemets doubles.

#### <a name="install-additional-packages"></a>Installer des packages supplémentaires
Vous devez toodownload et installer des packages supplémentaires.

1. Assurez-vous que le serveur cible maître de hello est connecté toohello internet.
2. Exécuter toodownload de cette commande et installer des packages de 15 à partir du référentiel de CentOS hello : **# yum installer – y xfsprogs perl lsscsi ont wget kexec-tools**.
3. Si hello source que vous protégez les ordinateurs Linux wit Reiser XFS système pour la racine de hello de fichiers ou périphérique de démarrage, puis vous devez télécharger et installer des packages supplémentaires comme suit :

   * # <a name="cd-usrlocal"></a>cd /usr/local
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * # <a name="rpm-ivh-kmod-reiserfs-00-1el6elrepox8664rpm-reiserfs-utils-3621-1el6elrepox8664rpm"></a>rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * # <a name="wget-httpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpmhttpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpm"></a>wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * # <a name="rpm-ivh-xfsprogs-311-16el6x8664rpm"></a>rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm

#### <a name="apply-custom-changes"></a>Appliquer des modifications personnalisées
Effectuez hello suivant tooapply des modifications personnalisées une fois que vous avez des étapes de post-installation hello terminée et les packages installés hello :

1. Copiez hello RHEL 6-64 unifiée de l’Agent toohello binaire machine virtuelle. Exécutez cette commande hello toountar binaire : **tar – zxvf<file name>**
2. Exécutez cette autorisations toogive de commande : **# chmod 755./ApplyCustomChanges.sh**
3. Exécutez le script de hello : **#./ApplyCustomChanges.sh**. Vous devez uniquement exécuter les script hello qu’une seule fois. Redémarrez le serveur de hello après que hello script s’exécute correctement.

## <a name="run-hello-failback"></a>Exécuter la restauration automatique de hello
### <a name="reprotect-hello-azure-vms"></a>Rétablissez les machines virtuelles de Azure hello
1. Dans le portail Site Recovery hello > **Machines** onglet, sélectionnez hello machine virtuelle qui est basculé et cliquez sur **Reprotéger**.
2. Dans **serveur cible maître** et **serveur de processus** sélectionnez serveur cible maître de local hello et le serveur de processus de machine virtuelle Azure hello.
3. Sélectionnez le compte hello que vous avez configuré pour la connexion toohello machine virtuelle.
4. Sélectionnez la version de la restauration automatique hello hello du groupe de protection. Par exemple, si hello machine virtuelle est protégée dans PG1, vous devez tooselect PG1_Failback.
5. Si vous souhaitez toorecover tooan autre emplacement, sélectionnez le lecteur de rétention hello et magasin de données configuré pour le serveur cible maître de hello. Lorsque vous ne parvenez pas toohello arrière local site hello les ordinateurs virtuels VMware dans un plan de protection de la restauration automatique hello utilisera hello même magasin de données en tant que serveur cible maître de hello. Si vous souhaitez toorecover hello réplica Azure VM toohello même local machine virtuelle puis hello local machine virtuelle doit déjà être Bonjour même magasin de données en tant que hello principal serveur cible. En l’absence de machine virtuelle locale, une nouvelle machine virtuelle de ce type est créée pendant la reprotection.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback1.png)
6. Après avoir cliqué sur **OK** toobegin protéger un travail commence tooreplicate hello machine virtuelle à partir du site local de toohello Azure. Vous pouvez suivre la progression de hello sur hello **travaux** onglet.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback2.png)

### <a name="run-a-failover-toohello-on-premises-site"></a>Exécuter un basculement toohello sur site local
Après hello de protéger la machine virtuelle est la version de la restauration automatique toohello déplacé de son groupe de protection et est automatiquement ajouté le plan de récupération toohello que vous avez utilisé pour hello basculement tooAzure si elle existe.

1. Bonjour **les Plans de récupération** plan de récupération hello sélectionnez page contenant le groupe de la restauration automatique hello puis cliquez sur **basculement** > **basculement non planifié**.
2. Dans **confirmer le basculement** Vérifiez le sens du basculement hello (tooAzure) et sélectionnez hello point de récupération toouse pour le basculement hello (dernière version). Si vous avez activé **Multimachine virtuelle** lorsque vous avez configuré les propriétés de réplication, vous pouvez récupérer toohello dernière application ou point de récupération cohérent de l’incident. Cliquez sur le basculement de hello toostart hello case à cocher.
3. Pendant le basculement Site Recovery arrêtera hello machines virtuelles Azure. Après avoir vérifié que la restauration est terminée normalement vous pouvez vous pouvez vérifier que hello que machines virtuelles Azure a été arrêtés comme prévu.

### <a name="reprotect-hello--on-premises-site"></a>Protégez de nouveau site local de hello
Une fois la restauration automatique terminée vos données seront sur site local de hello, mais ne pas être protégées. tooAzure de réplication toostart à nouveau hello suivant :

1. Dans le portail Site Recovery hello > **Machines** onglet machines virtuelles hello select qui ont échoué en arrière et cliquez sur **Reprotéger**.
2. Après avoir vérifié que tooAzure de réplication fonctionne comme prévu, vous pouvez supprimer dans Azure hello machines virtuelles Azure (actuellement ne pas en cours d’exécution) qui ont été rétablies.

### <a name="common-issues-in-failback"></a>Problèmes courants lors de la restauration automatique
1. Si vous effectuez une découverte vCenter en mode lecture seule utilisateur et protégez des machines virtuelles, l’opération réussit et le basculement fonctionne. Au moment de hello de Reprotection, il échouera car hello banques de données ne peut pas être découvert. Comme un symptôme, vous ne verrez pas les magasins de données hello répertoriés, tout en ré protégeant les. tooresolve, vous pouvez mettre à jour les informations d’identification de vCenter hello avec le compte approprié qui dispose des autorisations et recommencez la tâche de hello. [En savoir plus](site-recovery-vmware-to-azure-classic.md)
2. Lors de la restauration automatique un VM Linux et l’exécuter localement, vous verrez que ce package du Gestionnaire de réseau hello est désinstallé de la machine de hello. Il s’agit, car après la récupération de hello machine virtuelle dans Azure, le package du Gestionnaire de réseau hello est supprimée.
3. Lorsqu’une machine virtuelle est configurée avec une adresse IP statique et est basculée tooAzure, adresse IP de hello est acquis via DHCP. Lorsque vous procédez au basculement local tooOn arrière, hello machine virtuelle continue à adresse IP de toouse DHCP tooacquire hello. Vous devez toomanually connexion dans l’ordinateur de hello et définir l’adresse IP hello sauvegarder tooStatic adresse si nécessaire.
4. Si vous utilisez la version gratuite d’ESXi 5.5 ou de vSphere 6 Hypervisor, le basculement devrait aboutir, mais la restauration automatique ne fonctionnera pas. Vous allez ned tooupgrade tooeither licence d’évaluation tooenable la restauration automatique.

## <a name="failing-back-with-expressroute"></a>Restauration automatique avec ExpressRoute
Vous pouvez effectuer une restauration automatique via une connexion VPN ou via Azure ExpressRoute. Si vous souhaitez suivant de hello toouse ExpressRoute Remarque :

* ExpressRoute doit être configurée sur hello réseau virtuel Azure toowhich source machines échouent sur, et dans lequel machines virtuelles Azure sont situés après le basculement hello.
* Les données sont répliquée tooan compte de stockage Azure sur un point de terminaison public. Vous devez configurer l’homologation publique dans ExpressRoute avec le centre de données cible hello toouse de réplication de Site Recovery ExpressRoute.
