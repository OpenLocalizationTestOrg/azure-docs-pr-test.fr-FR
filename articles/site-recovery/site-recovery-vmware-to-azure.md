---
title: aaaReplicate les ordinateurs virtuels VMware tooAzure | Documents Microsoft
description: "Résume les étapes hello pour répliquer les charges de travail en cours d’exécution sur les ordinateurs virtuels VMware tooAzure stockage"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-overview
ms.openlocfilehash: f800e7d8a3b59a86809a995748eacf87630a1713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-tooazure-with-site-recovery"></a>Répliquer tooAzure de machines virtuelles VMware avec Site Recovery

> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-vmware-to-azure.md)
> * [Portail Azure Classic](site-recovery-vmware-to-azure-classic.md)


Cet article décrit comment tooreplicate local tooAzure d’ordinateurs virtuels VMware, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Si vous souhaitez que les ordinateurs virtuels VMware de toomigrate tooAzure (basculement uniquement), lecture [cet article](site-recovery-migrate-to-azure.md) toolearn plus.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="deployment-steps"></a>Étapes du déploiement

Voici ce que vous devez toodo :

1. Vérifiez les conditions préalables et les limitations.
2. Configurez des comptes de réseau et de stockage Azure.
3. Préparer l’ordinateur local, hello que vous souhaitez toodeploy en tant que serveur de configuration hello.
4. Préparez des comptes VMware toobe utilisé pour la découverte automatique des machines virtuelles et éventuellement pour l’installation push du service mobilité de hello.
4. Créez un coffre Recovery Services. coffre de Hello contient les paramètres de configuration et orchestre la réplication.
5. Spécifiez les paramètres de la source, de la cible et de réplication.
6. Déployer le service de mobilité hello sur des machines virtuelles, vous souhaitez tooreplicate.
7. Activer la réplication pour les machines virtuelles de hello.
7. Exécutez un toomake de basculement de test que tout fonctionne comme prévu.

## <a name="prerequisites"></a>Composants requis

**Configuration requise pour la prise en charge** | **Détails**
--- | ---
**Microsoft Azure** | En savoir plus sur la [configuration requise pour Azure](site-recovery-prereq.md#azure-requirements)
**Serveur de configuration local** | Vous devez disposer d’une machine virtuelle VMware Windows Server 2012 R2 ou une version ultérieure. Configurez ce serveur au cours du déploiement de Site Recovery.<br/><br/> Par le processus de hello par défaut serveur et le serveur cible maître sont également installés sur cet ordinateur virtuel. Lors de la montée en puissance, vous devrez peut-être un serveur de processus distinct, et il a hello mêmes exigences que le serveur de configuration hello.<br/><br/> Vous trouverez de plus amples informations sur ces composants [ici](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**Serveurs VMware locaux** | Un ou plusieurs serveurs VMware vSphere exécutant la version 6.0, 5.5, 5.1 avec les dernières mises à jour. Les serveurs doivent se trouver dans le même réseau que le serveur de configuration hello (ou un serveur de processus distinct) de hello.<br/><br/> Nous vous recommandons un vCenter server toomanage hôtes, exécutant 6.0 ou 5.5 avec les dernières mises à jour de hello. Seules les fonctionnalités disponibles dans la version 5.5 sont prises en charge lorsque du déploiement de la version 6.0.
**Machines virtuelles locales** | Machines virtuelles que vous souhaitez tooreplicate doit être en cours d’exécution un [prise en charge du système d’exploitation](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)et être conformes avec [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). La machine virtuelle doit exécuter des outils VMware.
**URLs** | serveur de configuration Hello doit accéder aux URL de toothese :<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.<br/></br> Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).<br/></br> Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).<br/><br/> Autoriser cette URL pour le téléchargement de MySQL hello : http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Service de mobilité** | Installé sur chaque machine virtuelle répliquée.




## <a name="limitations"></a>Limitations

**Limite** | **Détails**
--- | ---
**Microsoft Azure** | Les comptes de stockage et réseau doivent être Bonjour même région que le coffre de hello<br/><br/> Si vous utilisez un compte de stockage premium, vous devez également une norme de stocker les journaux de compte de réplication toostore<br/><br/> Vous ne peut pas répliquer toopremium des comptes dans le centre et de l’Inde du Sud.
**Serveur de configuration local** | Le type d’adaptateur de machine virtuelle VMware doit être VMXNET3. Dans le cas contraire, [installez cette mise à jour](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> vSphere PowerCLI 6.0 doit être installé.<br/><br> machine de Hello ne doivent pas être un contrôleur de domaine. machine de Hello doit avoir une adresse IP statique.<br/><br/> nom d’hôte Hello doit être de 15 caractères ou moins, et le système d’exploitation doit être en anglais.
**VMware** | Seules les fonctionnalités de la version 5.5 sont prises en charge dans vCenter 6.0. Site Recovery ne prend pas en charge les nouvelles fonctionnalités de vCenter et vSphere 6.0 telles que Cross vCenter vMotion, les volumes virtuels et le DRS de stockage.
**Machines virtuelles** | Vérifier les [limitations de la machine virtuelle Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> Vous ne pouvez pas répliquer de machines virtuelles comportant des disques chiffrés, ou des machines virtuelles avec le démarrage UEFI/EFI.<br/><br> Les clusters à disque partagé ne sont pas pris en charge. Si l’ordinateur virtuel source de hello a association de cartes réseau, il est converti tooa une seule carte réseau après le basculement.<br/><br/> Si les ordinateurs virtuels disposent d’un disque iSCSI, Site Recovery convertit fichier de disque dur virtuel tooa après le basculement. Si la cible iSCSI de hello peut être atteint par hello machine virtuelle Azure, il connecte tooit et voit il et hello disque dur virtuel. Si cela se produit, vous déconnecter de cible iSCSI hello.<br/><br/> Si vous souhaitez que la cohérence multimachine virtuelle tooenable, ce qui permet aux ordinateurs virtuels en cours d’exécution hello récupérée de la même charge de travail toobe tooa ensemble des données cohérentes point, ouvrir le port 20004 sur hello machine virtuelle.<br/><br/> Windows doit être installé sur le lecteur de hello C. disque de système d’exploitation Hello doit être de base et non dynamique. disque de données Hello peut être dynamique.<br/><br/> Les fichiers Linux/etc/hosts sur des machines virtuelles doivent contenir des entrées qui mappent des adresses de tooIP du nom d’hôte local hello associés à toutes les cartes réseau. Hello nom d’hôte, des points de montage, nom du périphérique, chemins d’accès système et noms de fichiers (/ etc. ; /usr) doit être en anglais uniquement.<br/><br/> Les types spécifiques de [stockage Linux](site-recovery-support-matrix-to-azure.md#support-for-storage) sont pris en charge.<br/><br/>Créer ou définir **disk.enableUUID=true** dans les paramètres de machine virtuelle hello. Cela fournit un toohello UUID cohérent VMDK, afin qu’il monte correctement et garantit que les modifications delta uniquement sont transférées local tooon arrière lors du retour arrière, sans réplication complète.

## <a name="set-up-azure"></a>Configurer Azure

1. [Configurez un réseau Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    - Les machines virtuelles Azure seront placées dans ce réseau une fois créées après le basculement.
    - Vous pouvez configurer un réseau dans [Resource Manager](../resource-manager-deployment-model.md), ou en mode classique.

2. Configurer un [compte de stockage Azure](../storage/storage-create-storage-account.md#create-a-storage-account) pour les données répliquées.
    - compte de Hello peut être standard ou [premium](../storage/storage-premium-storage.md).
    - Vous pouvez configurer un compte dans Resource Manager, ou en mode classique.

3. [Préparer un compte](#prepare-for-automatic-discovery-and-push-installation) sur le serveur vCenter hello ou vSphere hôtes, ainsi que la récupération Site peut détecter automatiquement les ordinateurs virtuels VMware.

## <a name="prepare-hello-configuration-server"></a>Préparer le serveur de configuration hello

1. Installez Windows Server 2012 R2 ou version ultérieure sur une machine virtuelle VMware.
2. Assurez-vous que hello machine virtuelle a répertorié dans les URL d’accès toohello [conditions préalables](#prerequisites).
3. Installez [VMware vSphere PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1).


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>Préparation pour l’installation Push et la découverte automatique

- **Préparer un compte pour la découverte automatique**: serveur de processus de récupération de Site hello découvre automatiquement les machines virtuelles. toodo, informations d’identification de besoins de récupération de Site qui peuvent accéder aux serveurs vCenter et des ordinateurs hôtes ESXi vSphere.

    1. toouse un compte dédié, créer un rôle (au niveau de vCenter Bonjour, grâce à ces [autorisations](#vmware-account-permissions). Donnez-lui un nom, tel que **Azure_Site_Recovery**.
    2. Ensuite, créez un utilisateur sur le serveur hôte/vCenter de vSphere hello et affecter hello rôle toohello utilisateur. Vous spécifiez ce compte d’utilisateur pendant le déploiement de Site Recovery.

- **Préparer un hello toopush de compte service de mobilité**: Si vous souhaitez toopush hello mobilité service tooVMs, vous avez besoin d’un compte qui peut être utilisé par hello processus serveur tooaccess hello machine virtuelle. Hello compte est uniquement utilisé pour l’installation push de hello. Vous pouvez utiliser un compte local ou de domaine :

    - Pour Windows, si vous n’utilisez pas un compte de domaine, vous devez toodisable contrôle des accès utilisateur à distance sur l’ordinateur local de hello. toodo, Bonjour Enregistrer sous **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, ajouter l’entrée DWORD de hello **LocalAccountTokenFilterPolicy**, avec la valeur 1.
    - Si vous souhaitez l’entrée de Registre tooadd hello pour Windows à partir d’une interface CLI, tapez :``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - Pour Linux, hello doit être racine sur le serveur de Linux hello source.

## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-hello-protection-goal"></a>Sélectionnez l’objectif de protection de hello

Sélectionnez les éléments tooreplicate, et où vous souhaitez que tooreplicate à.

1. Cliquez sur **Coffres Recovery Services** > coffre.
2. Bonjour ressource Menu, cliquez sur **Site Recovery** > **étape 1 : préparer l’Infrastructure** > **objectif de Protection**.

    ![Sélectionner des objectifs](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. Dans **objectif de Protection**, sélectionnez **tooAzure** > **Oui, avec l’hyperviseur VMware vSphere**.

    ![Sélectionner des objectifs](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

Configurer le serveur de configuration hello, enregistrez-le dans le coffre hello et découvrir des ordinateurs virtuels.

1. Cliquez sur **Site Recovery** > **Étape 1 : Préparer l’infrastructure** > **Source**.
2. Si vous n’avez pas de serveur de configuration, cliquez sur **+Serveur de configuration**.

    ![Configurer la source](./media/site-recovery-vmware-to-azure/set-source1.png)
3. Dans **Ajouter un serveur**, vérifiez que **Serveur de configuration** s’affiche dans **Type de serveur**.
4. Télécharger le fichier d’installation le programme d’installation de Site Recovery unifiée hello.
5. Télécharger la clé d’inscription du coffre hello. Vous en aurez besoin lors de l’exécution du programme d’installation unifiée. clé de Hello est valide pendant cinq jours après que l’avoir généré.

   ![Configurer la source](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Exécuter le programme d’installation unifiée Site Recovery

Suit hello avant de démarrer, puis exécuter le programme d’installation unifiée serveur de configuration tooinstall hello, serveur de processus hello et serveur cible maître de hello.
    - Visionnez une courte vidéo de présentation :

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Sur le serveur de configuration hello machine virtuelle, assurez-vous que l’horloge système hello est synchronisée avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Elles doivent correspondre. S’il y a 15 minutes d’avance ou de retard, le programme d’installation peut échouer.
    - Exécutez le programme d’installation en tant qu’administrateur Local sur le serveur de configuration hello machine virtuelle.
    - Vérifiez que TLS 1.0 est activé sur la machine virtuelle de hello.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> serveur de configuration Hello peut également être installé [à partir de la ligne de commande hello](http://aka.ms/installconfigsrv).



### <a name="add-hello-account-for-automatic-discovery"></a>Ajoutez le compte hello pour la découverte automatique

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-toovmware-servers"></a>Connecter les serveurs tooVMware

Se connecter toovSphere ESXi hôtes ou les serveurs vCenter toodiscover les ordinateurs virtuels VMware.

- Si vous ajoutez le serveur vCenter hello ou hôtes vSphere avec un compte sans privilèges d’administrateur sur le serveur de hello, compte de hello a besoin de ces privilèges activés :
    - Centre de données, magasin de données, dossier, hôte, réseau, ressource, machine virtuelle, vSphere Distributed Switch.
    - le serveur vCenter Hello a besoin d’autorisations de vues de stockage.
- Lorsque vous ajoutez des serveurs VMware, il peut prendre 15 minutes ou plus pour les tooappear dans le portail de hello.
tooallow Azure Site Recovery toodiscover machines virtuelles en cours d’exécution dans votre environnement local, vous devez tooconnect votre serveur VMware vCenter ou les ordinateurs hôtes ESXi vSphere avec Site Recovery.

Sélectionnez **+ vCenter** toostart connecter un serveur VMware vCenter ou un hôte VMware vSphere ESXi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

Récupération de site connecte tooVMware serveurs à l’aide de hello spécifié de paramètres et détecte les machines virtuelles.

## <a name="set-up-hello-target"></a>Configurer la cible de hello

Avant de configurer l’environnement cible de hello, vérifiez d’avoir un [compte de stockage et réseau](#set-up-azure)

1. Cliquez sur **Prepare infrastructure** > **cible**, et sélectionnez hello abonnement Azure que vous souhaitez toouse.
2. Spécifiez si votre modèle de déploiement cible est basé sur Resource Manager ou est de type classique.
3. Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.

   ![Cible](./media/site-recovery-vmware-to-azure/gs-target.png)
4. Si vous n’avez pas créé un compte de stockage ou un réseau, cliquez sur **+ compte de stockage** ou **+ réseau**, toocreate un gestionnaire de ressources du réseau ou le compte en ligne.

## <a name="set-up-replication-settings"></a>Configurer les paramètres de réplication

Visionnez une courte vidéo de présentation avant de commencer :
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate une stratégie de réplication, cliquez sur **infrastructure de Site Recovery** > **stratégies de réplication** > **+ la stratégie de réplication**.
2. Dans **Créer une stratégie de réplication**, indiquez le nom de la stratégie.
3. Dans **seuil RPO**, spécifiez la limite RPO hello. Cette valeur spécifie la fréquence à laquelle les points de récupération des données sont créés. Une alerte est générée lorsque la réplication continue dépasse cette limite.
4. Dans **rétention du point de récupération**, spécifiez la durée (en heures) est d’une fenêtre de rétention hello pour chaque point de récupération. Machines virtuelles répliquées peuvent être récupérées point tooany dans une fenêtre. Des too24 rétention d’heures est pris en charge pour les machines répliquées toopremium stockage et 72 heures pour le stockage standard.
5. Dans **Fréquence des captures instantanées de cohérence d’application**, spécifiez la fréquence de création des points de récupération contenant des captures instantanées cohérentes avec les applications (en minutes). Cliquez sur **OK** stratégie de hello toocreate.

    ![Stratégie de réplication](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. Lorsque vous créez une nouvelle stratégie, il est automatiquement associé serveur de configuration hello. Par défaut, une stratégie de correspondance est automatiquement créée pour la restauration automatique. Par exemple, si hello stratégie de réplication est **rep-policy** stratégie de restauration automatique hello sera **rep-stratégie de la restauration automatique**. Cette stratégie n’est utilisée qu’à partir du moment où vous initiez une restauration automatique à partir d’Azure.  



## <a name="plan-capacity"></a>Planifier la capacité

1. Votre infrastructure de base est désormais configurée. Vous pouvez donc réfléchir à la planification de la capacité et déterminer si des ressources supplémentaires sont nécessaires. [En savoir plus](site-recovery-plan-capacity-vmware.md).
2. Lorsque vous avez terminé la planification de la capacité, sélectionnez **Oui** dans **Avez-vous effectué une planification de la capacité ?**

   ![Planification de la capacité](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Préparer des machines virtuelles pour la réplication

Hello service mobilité doit être installé sur tous les ordinateurs virtuels VMware que vous souhaitez tooreplicate. Vous pouvez installer le service de mobilité hello dans de plusieurs façons :

1. Installer avec une installation poussée du hello du serveur de processus. Vous devez toouse de machines virtuelles tooprepare cette méthode.
2. Utilisez des outils de déploiement tels que System Center Configuration Manager ou Azure automation DSC.
3.  Procédez à une installation manuelle.

[En savoir plus](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>Activer la réplication

Avant de commencer :

- Votre compte d’utilisateur Azure doit toohave certaines [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’un nouveau tooAzure d’ordinateur virtuel.
- Lorsque vous ajoutez ou modifiez des machines virtuelles, il peut prendre too15 minutes ou plus pour effet de tootake de modifications et les tooappear dans le portail de hello.
- Vous pouvez vérifier l’heure de dernier découvert de hello pour les machines virtuelles dans **serveurs de Configuration** > **dernier Contact à**.
- tooadd machines virtuelles sans attendre la détection planifiée hello, serveur de configuration de mise en surbrillance hello (ne cliquez pas dessus), puis cliquez sur **Actualiser**.
- Si une machine virtuelle est préparée à l’installation push, serveur de processus hello installe automatiquement le service de mobilité hello lorsque vous activez la réplication.


### <a name="exclude-disks-from-replication"></a>Exclure les disques de la réplication

Par défaut, tous les disques d’une machine sont répliqués. Vous pouvez exclure des disques de la réplication. Par exemple, vous pouvez tooreplicate les disques avec les données temporaires ou des données a actualisé chaque fois qu’un ordinateur ou redémarrage de l’application (par exemple pagefile.sys ou tempdb de SQL Server).

### <a name="replicate-vms"></a>Répliquer des machines virtuelles

Avant de commencer, visionnez une courte vidéo de présentation :

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Cliquez sur **Étape 2 : Répliquer l’application** > **Source**.
2. Dans **Source**, sélectionnez le serveur de configuration hello.
3. Dans **Type de machine**, sélectionnez **Machines virtuelles**.
4. Dans **vCenter/vSphere hyperviseur**, sélectionnez le serveur vCenter hello qui gère l’ordinateur hôte de vSphere hello ou sélectionner l’ordinateur hôte hello.
5. Sélectionnez le serveur de processus hello. Si vous n’avez pas créé de tous les serveurs de processus supplémentaire ce sera le serveur de configuration hello. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. Dans **cible**hello du groupe de ressources dans lequel vous souhaitez hello toocreate a échoué sur des machines virtuelles et sélectionnez l’abonnement de hello. Choisir le modèle de déploiement hello que toouse dans Azure (classique ou ressource de gestion), hello basculé de machines virtuelles.


7. Sélectionnez le compte de stockage Azure hello que toouse souhaité pour répliquer les données. Si vous ne souhaitez pas toouse un compte que vous avez déjà configuré, vous pouvez créer un nouveau.

8. Sélectionnez hello toowhich réseau et le sous-réseau Azure machines virtuelles Azure se connecte lorsqu’elles sont créées après le basculement. Sélectionnez **configurer maintenant pour les machines sélectionnées**, tooapply hello réseau paramètre tooall machines que vous sélectionnez pour la protection. Sélectionnez **configurer ultérieurement** tooselect hello réseau Azure par ordinateur. Si vous ne souhaitez pas toouse un réseau existant, vous pouvez créer un.

    ![Activer la réplication](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. Dans **virtuels** > **sélectionner des machines virtuelles**, cliquez sur et sélectionnez chaque ordinateur que vous souhaitez tooreplicate. Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. Dans **propriétés** > **configurer les propriétés**, sélectionnez compte hello qui sera utilisé par hello processus serveur tooautomatically installer le service de mobilité hello sur l’ordinateur de hello.
11. Par défaut, tous les disques sont répliqués. Cliquez sur **tous les disques** et effacer tous les disques que vous ne souhaitez pas tooreplicate. Cliquez ensuite sur **OK**. Vous pouvez configurer des propriétés de machine virtuelle supplémentaires ultérieurement.

    ![Activer la réplication](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. Dans **les paramètres de réplication** > **configurer les paramètres de réplication**, vérifiez que hello correct de la stratégie de réplication est activée. Si vous modifiez une stratégie, les modifications seront appliquées tooreplicating machine et toonew machines.
12. Activer **la cohérence Multimachine virtuelle** si vous souhaitez toogather ordinateurs dans un groupe de réplication, spécifiez un nom pour le groupe de hello. Cliquez ensuite sur **OK**. Notez les points suivants :

    * Les machines des groupes de réplication sont répliquées ensemble et ont des points de récupération cohérents après incident et avec les applications lorsqu’elles basculent.
    * Nous vous recommandons de rassembler les machines virtuelles et les serveurs physiques afin qu’ils reflètent vos charges de travail. L’activation de la cohérence multimachine virtuelle peuvent affecter les performances de la charge de travail et doit être utilisé uniquement si les ordinateurs hello même charge de travail et que vous avez besoin de cohérence.

    ![Activer la réplication](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. Cliquez sur **Activer la réplication**. Vous pouvez suivre la progression de hello **activer la Protection** de la tâche dans **paramètres** > **travaux** > **tâches de récupération de Site**. Après avoir hello **finaliser la Protection** s’exécute la tâche machine de hello est prête pour le basculement.

### <a name="view-and-manage-vm-properties"></a>Afficher et gérer les propriétés des machines virtuelles

Nous vous recommandons de vérifier les propriétés d’ordinateurs virtuels hello apporter des modifications que vous deviez.

1. Cliquez sur **éléments répliqués** > et sélectionnez hello machine. Hello **Essentials** panneau affiche des informations sur les paramètres des ordinateurs et l’état.
2. Dans **propriétés**, vous pouvez afficher la réplication et les informations de basculement pour hello machine virtuelle.
3. Dans **de calcul et réseau** > **propriétés de calcul**, vous pouvez spécifier la taille de nom et la cible de la machine virtuelle Azure hello. Modifier toocomply de nom hello avec [conditions requises pour Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) si vous avez besoin.
4. Modifier les paramètres de réseau de cible de hello, sous-réseau et adresse IP qui sera assigné toohello machine virtuelle Azure :

   - Vous pouvez définir l’adresse IP de hello cible.

    - Si vous ne fournissez une adresse, hello a échoué sur l’ordinateur utilise DHCP.
    - Si vous définissez une adresse qui n’est pas disponible au moment du basculement, ce dernier échoue.
    - Hello même adresse IP peut servir pour le test de basculement, si l’adresse de hello est disponible dans le réseau de basculement de test hello.

   - nombre de Hello de cartes réseau est dicté par taille hello que vous spécifiez pour la machine virtuelle cible hello :

     - Si nombre hello de cartes réseau sur l’ordinateur source de hello est hello identique ou inférieur au nombre de hello de cartes autorisé pour la taille de la machine cible hello, cible de hello aura hello même nombre de cartes en tant que source de hello.
     - Si nombre hello de cartes pour l’ordinateur virtuel de source hello dépasse le nombre hello autorisé pour la taille cible de hello, taille maximale de la cible hello sera utilisée.
     - Par exemple, si un ordinateur source possède deux cartes réseau et la taille de la machine cible hello prend en charge quatre, l’ordinateur cible hello aura deux cartes. Si hello source ordinateur possède deux cartes, mais hello taille cible pris en charge uniquement en charge l’un de l’ordinateur cible hello aura qu’un seul adaptateur.     
   - Si l’ordinateur virtuel de hello possède plusieurs cartes réseau qu’ils seront connectent tous toohello même réseau.
   - Si l’ordinateur virtuel de hello possède plusieurs cartes réseau, hello celui affiché dans la liste de hello devient hello *par défaut* carte réseau Bonjour machine virtuelle Azure.
4. Dans **disques**, vous pouvez voir le système d’exploitation de l’ordinateur virtuel hello et les données de salutation disques qui seront répliquées.

#### <a name="managed-disks"></a>Disques gérés

Dans **de calcul et réseau** > **propriétés de calcul**, vous pouvez définir « Utilisation des disques gérés par » trop « Oui » pour hello machine virtuelle si vous voulez tooattach disques gérés tooyour machine sur tooAzure de basculement. Disques gérés par la gestion des comptes de stockage hello associées aux disques de machine virtuelle hello, ce qui simplifie la gestion de disque pour les machines virtuelles Azure IaaS. En savoir plus sur les [disques gérés](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)

   - Disques gérés sont un ordinateur virtuel de toohello créé et attaché uniquement sur un tooAzure de basculement. Sur l’activation de la protection, les données à partir d’ordinateurs locaux continuent tooreplicate toostorage comptes.  Disques gérés peuvent être créés uniquement pour les ordinateurs virtuels déployés à l’aide du modèle de déploiement du Gestionnaire de ressources hello.  

   - Lorsque vous définissez « Utilisation des disques gérés par » trop « Oui », uniquement à haute disponibilité dans le groupe de ressources hello avec « Utilisation des disques gérés par » le jeu trop « Oui » est alors disponible pour sélection. Il s’agit, car les machines virtuelles avec des disques gérés ne peut faire partie de la haute disponibilité avec un jeu de propriétés de « Disques utilisez géré » trop « Oui ». Assurez-vous que vous créez des groupes à haute disponibilité avec un jeu de propriétés de « Disques utilisez géré » en fonction de vos disques toouse intention géré lors du basculement.  De même, lorsque vous définissez « Utilisation des disques gérés par » trop « non », seuls groupes à haute disponibilité dans le groupe de ressources hello avec « Utilisation des disques gérés par » propriété trop « non » sont alors disponibles pour sélection. [En savoir plus sur les disques gérés et les groupes à haute disponibilité](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Si le compte de stockage hello utilisée pour la réplication a été chiffré avec un chiffrement de Service de stockage à n’importe quel point dans le temps, la création de disques gérés pendant le basculement échoue. Vous pouvez définir « Utilisation des disques gérés par » trop « non » et réessayez de basculement ou désactivez la protection pour la machine virtuelle de hello et protéger le compte de stockage tooa qui n’avait pas de chiffrement de service de stockage activé à n’importe quel point dans le temps.
  > [En savoir plus sur Storage Service Encryption et les disques gérés](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="run-a-test-failover"></a>Exécution d’un test de basculement


Une fois que vous avez configuré tous les éléments, exécutez un toomake de basculement de test que tout fonctionne comme prévu. Visionnez une courte vidéo de présentation avant de commencer :
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail sur un seul ordinateur, dans **paramètres** > **répliquées des éléments**, cliquez sur la machine virtuelle de hello > **+ Test de basculement** icône.

    ![Test de basculement](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. toofail sur la récupération d’un plan, en **paramètres** > **les Plans de récupération**, plan de hello avec le bouton droit > **Test de basculement**. toocreate un plan de récupération, [suivez ces instructions](site-recovery-create-recovery-plans.md).  

1. Dans **Test de basculement**, sélectionnez hello réseau Azure toowhich machines virtuelles Azure est connectée après le basculement se produit.

1. Cliquez sur **OK** toobegin hello basculement. Vous pouvez suivre la progression en cliquant sur hello VM tooopen ses propriétés, ou sur hello **Test de basculement** travail dans le nom du coffre > **paramètres** > **travaux**  >  **Les tâches de récupération de site**.

1. Une fois hello basculement terminé, vous devez également être en mesure de réplica de hello toosee machine Azure s’affichent dans hello portail Azure > **virtuels**. Assurez-vous que VM hello est hello approprié, qui sa connexion réseau approprié de toohello, et qu’il s’exécute.

1. Si vous [préparé pour les connexions après le basculement](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), vous devez être en mesure de tooconnect toohello machine virtuelle Azure.

1. Une fois que vous avez terminé, cliquez sur **basculement de test de nettoyage** sur le plan de récupération hello. Dans **Notes**, enregistrer et enregistrer toutes les observations associées au basculement de test hello. Cette opération supprimera les machines virtuelles hello qui ont été créés pendant le test de basculement.

Pour plus d’informations sur les tests de basculement, cliquez [ici](site-recovery-test-failover-to-azure.md).


## <a name="vmware-account-permissions"></a>Autorisations du compte VMware

Les besoins de récupération de site accès tooVMware hello processus serveur tooautomatically découvrir les machines virtuelles et pour le basculement et la restauration des machines virtuelles.

- **Migrer**: Si vous souhaitez uniquement toomigrate les ordinateurs virtuels VMware tooAzure, sans jamais les échoue de nouveau, vous pouvez utiliser un compte de VMware avec un rôle en lecture seule. Ce type de rôle peut exécuter le basculement mais ne peut pas arrêter les machines source protégées. Cela n’est pas nécessaire pour la migration.
- **Réplication/récupération**: Si vous souhaitez que le compte de hello toodeploy réplication complète (replicate, basculement, la restauration automatique) doit être toorun en mesure des opérations telles que la création et la suppression de disques, sous tension etc. de machines virtuelles.
- **Découverte automatique** : au moins un compte en lecture seule est nécessaire.


**Tâche** | **Nécessite un compte/rôle** | **Autorisations** | **Détails**
--- | --- | --- | ---
**Le serveur de processus découvre automatiquement les machines virtuelles VMware** | Vous devez disposer d’au moins un utilisateur en lecture seule | Objet de centre de données -> propager tooChild objet rôle = lecture seule | Utilisateur affecté au niveau du centre de données et a accès tooall hello objets dans le centre de données hello.<br/><br/> accès toorestrict, affecter hello **aucun accès** rôle avec hello **propager toochild** toohello des objets enfants (hôtes de vSphere, magasins de données, machines virtuelles et réseaux), l’objet.
**Type de basculement** | Vous devez disposer d’au moins un utilisateur en lecture seule | Objet de centre de données -> propager tooChild objet rôle = lecture seule | Utilisateur affecté au niveau du centre de données et a accès tooall hello objets dans le centre de données hello.<br/><br/> accès toorestrict, affecter hello **aucun accès** rôle avec hello **propager toochild** toohello (hôtes de vSphere, magasins de données, machines virtuelles et réseaux) des objets enfants de l’objet.<br/><br/> Utile à des fins de migration, mais pas pour la réplication complète, le basculement et la restauration automatique.
**Basculement et restauration automatique** | Nous vous suggérons de vous créez un rôle (Azure_Site_Recovery) avec les autorisations hello requis, puis affectez hello rôle tooa VMware utilisateur ou un groupe | Objet de centre de données -> propager tooChild objet rôle = Azure_Site_Recovery<br/><br/> Banque de données -> Allouer de l’espace, parcourir la banque de données, opérations de fichier de bas niveau, supprimer le fichier, mettre à jour les fichiers de machine virtuelle<br/><br/> Réseau -> Attribution de réseau<br/><br/> Ressource -> pool tooresource d’affecter un ordinateur virtuel, migrez la machine virtuelle hors tension, migrer sous tension sur la machine virtuelle<br/><br/> Tâches -> Créer une tâche, Mettre à jour une tâche<br/><br/> Machine virtuelle -> Configuration<br/><br/> Machine virtuelle -> Interagir -> répondre à la question, connexion d’appareil, configurer un support de CD, configurer une disquette, mettre hors tension, mettre sous tension, installation des outils VMware<br/><br/> Machine virtuelle -> Stock -> Créer, inscrire, désinscrire<br/><br/> Machine virtuelle -> Approvisionnement -> Autoriser le téléchargement de machines virtuelles, autoriser le chargement de fichiers de machine virtuelle<br/><br/> Machine virtuelle -> Instantanés -> Supprimer les instantanés | Utilisateur affecté au niveau du centre de données et a accès tooall hello objets dans le centre de données hello.<br/><br/> accès toorestrict, affecter hello **aucun accès** rôle avec hello **propager toochild** toohello des objets enfants (hôtes de vSphere, magasins de données, machines virtuelles et réseaux), l’objet.


## <a name="next-steps"></a>Étapes suivantes

Après avoir préparer la réplication et en cours d’exécution, lorsqu’une panne se produit vous procédez au basculement tooAzure et machines virtuelles Azure sont créés à partir des données de hello répliquée. Vous pouvez ensuite accéder des charges de travail et des applications dans Azure, jusqu'à ce que vous ne parvenez pas emplacement principal d’arrière tooyour lorsqu’elle retourne les opérations de toonormal.

- [En savoir plus](site-recovery-failover.md) sur différents types de basculement et comment toorun les.
- Si vous migrez des ordinateurs au lieu de procéder à une réplication et une restauration automatique, [lisez cet article pour en savoir plus](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [En savoir plus sur la restauration automatique](site-recovery-failback-azure-to-vmware.md), toofail et réplication de machines virtuelles Azure sauvegarder toohello principal sur-site local.

## <a name="third-party-software-notices-and-information"></a>Informations et remarques relatives aux logiciels tiers
Do Not Translate or Localize

logiciels de Hello et de microprogramme en cours d’exécution hello produit Microsoft ou service repose sur ou inclut, du contenu à partir de hello projets répertoriés ci-dessous (collectivement, « Code tiers »).  Microsoft est hello pas auteur de hello Code de tiers.  mention de copyright d’origine Hello et de licence, dans lesquelles Microsoft a reçu ce Code tiers, sont définies ci-dessous.

informations Hello dans la Section A concerne un Code de tiers des composants à partir de projets de hello répertoriées ci-dessous. Such licenses and information are provided for informational purposes only.  Ce Code de tiers est en cours tooyou relicensed par Microsoft hello produit ou service Microsoft termes du contrat de licence des logiciels de Microsoft.  

informations Hello dans la Section B concernant les composants de Code de tiers qui sont établies tooyou disponible par Microsoft sous les termes du contrat de licence d’origine hello.

fichier dans son intégralité Hello se trouve sur hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
