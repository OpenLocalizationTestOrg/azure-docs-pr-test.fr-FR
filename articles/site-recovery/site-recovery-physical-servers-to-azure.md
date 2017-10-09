---
title: aaaReplicate serveurs physiques tooAzure | Documents Microsoft
description: "Décrit comment la réplication tooorchestrate toodeploy Azure Site Recovery, le basculement et récupération de local tooAzure des serveurs physiques Windows/Linux à l’aide de hello portail Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a>Répliquer des machines physiques tooAzure à l’aide de récupération de Site


Cet article décrit comment tooreplicate local tooAzure de machines physiques à l’aide du service d’Azure Site Recovery hello Bonjour portail Azure.

Si vous souhaitez toomigrate machines physiques tooAzure (basculement uniquement), lecture [migrer tooAzure avec Site Recovery](site-recovery-migrate-to-azure.md) toolearn plus.

Ajouter des commentaires et questions bas hello de cet article ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Composants requis

**Configuration requise pour la prise en charge** | **Détails**
--- | ---
**Microsoft Azure** | Découvrez la [configuration requise pour Azure](site-recovery-prereq.md#azure-requirements).
**Serveur de configuration local** | Machine locale (machine physique ou machine virtuelle VMware) exécutant Windows Server 2012 R2 ou version ultérieure. Pour configurer le serveur de configuration hello lors du déploiement de Site Recovery.<br/><br/> Par défaut, serveur de processus hello et serveur cible maître sont également installés sur cet ordinateur. Lors de la montée en puissance, vous devrez peut-être un serveur de processus distinct, et il a hello mêmes exigences que le serveur de configuration hello.<br/><br/> En savoir plus sur ces composants dans [configurer l’environnement source hello](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**Machines virtuelles locales** | Ordinateurs que vous souhaitez tooreplicate doit être en cours d’exécution un [prise en charge du système d’exploitation](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) et être conformes avec [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs** | serveur de configuration Hello doit accéder aux URL de toothese :<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent la communication tooAzure.<br/></br> Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653) et hello port HTTPS (443).<br/></br> Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion de contrôle et l’identité de l’accès).<br/><br/> Autoriser cette URL pour le téléchargement de MySQL hello : http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Service de mobilité** | Ce service est installé sur chaque ordinateur, vous souhaitez tooreplicate.

## <a name="limitations"></a>Limites

**Limite** | **Détails**
--- | ---
**Microsoft Azure** | Les comptes de stockage et réseau doivent être Bonjour même région que le coffre hello.<br/><br/> Si vous utilisez un compte de stockage premium, vous devez également une norme de stocker les journaux de compte de réplication toostore.<br/><br/> Vous ne peut pas répliquer toopremium des comptes dans le centre et de l’Inde du Sud.
**Serveur de configuration local** | Si vous installez le serveur de configuration hello sur un VM VMware, hello type d’adaptateur de machine virtuelle doit être VMXNET3. Dans le cas contraire, [installez cette mise à jour](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Si vous utilisez une machine virtuelle VMware, vSphere PowerCLI 6.0 doit être installé dessus.<br/><br> machine de Hello ne doivent pas être un contrôleur de domaine.<br/><br/> machine de Hello doit avoir une adresse IP statique.<br/><br/> nom d’hôte Hello doit être de 15 caractères ou moins, et le système d’exploitation de hello doit être en anglais.
**Machines répliquées** | Vérifiez les [limitations de la machine virtuelle Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Si vous souhaitez que la cohérence multimachine virtuelle tooenable, ce qui permet aux ordinateurs exécutant hello récupérée de la même charge de travail toobe tooa ensemble des données cohérentes point, ouvrez le port 20004 sur l’ordinateur de hello.<br/><br/> Les types spécifiques de [stockage Linux](site-recovery-support-matrix-to-azure.md#support-for-storage) sont pris en charge.
**Restauration automatique** | Vous ne pouvez pas échouer à partir de l’ordinateur physique tooa Azure. Si vous souhaitez toobe toofail en mesure de retour tooon local après un basculement, un environnement VMware est nécessaire afin que vous pouvez échouent tooa arrière VMware VM.


## <a name="set-up-azure"></a>Configurer Azure

1. [Configurez un réseau Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. Les machines virtuelles Azure sont placées dans ce réseau une fois créées après le basculement.

      b. Vous pouvez configurer un réseau dans [Azure Resource Manager](../resource-manager-deployment-model.md) ou en mode classique.

2. Configurer un [compte de stockage Azure](../storage/storage-create-storage-account.md#create-a-storage-account) pour les données répliquées.

    a. compte de Hello peut être standard ou [premium](../storage/storage-premium-storage.md).

    b. Vous pouvez configurer un compte dans Resource Manager ou en mode classique.

## <a name="prepare-hello-configuration-server"></a>Préparer le serveur de configuration hello

1. Installez Windows Server 2012 R2 ou version ultérieure sur un serveur physique local ou une machine virtuelle VMware.

2. Assurez-vous qu’ordinateur de hello a répertorié dans les URL d’accès toohello [conditions préalables](#prerequisites).

## <a name="prepare-for-mobility-service-installation"></a>Préparer l’installation du service Mobilité

Si vous souhaitez machine physique tooa du service mobilité toopush hello, vous avez besoin d’un compte peut être utilisé par les ordinateurs hello tooaccess hello processus serveur. compte de Hello est utilisé uniquement pour l’installation push de hello. Vous pouvez utiliser un compte local ou de domaine :

  - Pour Windows, si vous n’utilisez pas un compte de domaine, vous devez toodisable contrôle des accès utilisateur à distance sur l’ordinateur local de hello. toodo cela, dans le Registre hello sous **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, ajouter l’entrée DWORD de hello **LocalAccountTokenFilterPolicy**, avec la valeur 1. Entrée de Registre tooadd hello pour Windows à partir d’une interface de ligne de commande, tapez :

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Pour Linux, le compte de hello doit être un utilisateur racine sur le serveur de Linux hello source.


## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a>Sélectionnez l’objectif de protection de hello

Sélectionnez ce que vous souhaitez tooreplicate, et où tooreplicate à.

1. Cliquez sur **Coffres Recovery Services** > **coffre**.
2. Sur hello **ressource** menu, cliquez sur **Site Recovery** > **préparer l’Infrastructure** > **l’objectif de Protection**.

    ![Sélectionner des objectifs](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. Dans **objectif de Protection**, sélectionnez **tooAzure** > **non virtualisé,**.


## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

Configurer le serveur de configuration hello, enregistrez-le dans le coffre hello et découvrir des ordinateurs virtuels.

1. Cliquez sur **Site Recovery** > **Préparer l’infrastructure** > **Source**.
2. Si vous n’avez pas de serveur de configuration, cliquez sur **+Serveur de configuration**.

    ![Configurer la source](./media/site-recovery-vmware-to-azure/set-source1.png)

3. Dans **Ajouter un serveur**, vérifiez que **Serveur de configuration** s’affiche dans **Type de serveur**.
4. Télécharger hello **le programme d’installation de Site Recovery unifiée** fichier d’installation.
5. Télécharger hello **clé d’inscription du coffre**. Vous aurez besoin de cette clé lors de l’exécution du programme d’installation unifiée. clé de Hello est valide pendant cinq jours après que l’avoir généré.

   ![Configurer la source](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Exécuter le programme d’installation unifiée Site Recovery

Avant de commencer, procédez comme hello suivant :

- Regardez une courte vidéo de présentation (hello vidéo explique comment traite les tooreplicate les ordinateurs virtuels VMware, mais hello est similaire pour la réplication de l’ordinateur physique.)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- Sur l’ordinateur du serveur de configuration de hello, assurez-vous que l’horloge système hello est synchronisée avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). S’il y a 15 minutes d’avance ou de retard, l’installation peut échouer.
- Exécutez le programme d’installation en tant qu’administrateur local sur l’ordinateur de serveur de configuration hello.
- Vérifiez que TLS 1.0 est activé sur l’ordinateur de hello.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> serveur de configuration Hello peut également être installé [à partir de la ligne de commande hello](http://aka.ms/installconfigsrv).


## <a name="set-up-hello-target-environment"></a>Configuration d’environnement cible de hello

Avant de configurer l’environnement cible de hello, vérifiez toomake que vous avez un [compte de stockage et réseau](#set-up-azure).

1. Cliquez sur **préparer l’Infrastructure** > **cible**, et sélectionnez hello abonnement Azure que vous souhaitez toouse.
2. Spécifiez si votre modèle de déploiement cible est Resource Manager ou est de type classique.
3. Récupération de site vérifie toomake assurer que vous disposez d’un ou plusieurs comptes de stockage Azure compatible et des réseaux.

   ![Cible](./media/site-recovery-vmware-to-azure/gs-target.png)

4. Si vous n’avez pas créé un compte de stockage ou un réseau, cliquez sur **+ compte de stockage** ou **+ réseau** toocreate un gestionnaire de ressources du réseau ou le compte en ligne.

## <a name="set-up-replication-settings"></a>Configurer les paramètres de réplication

Avant de commencer, regardez une courte vidéo de présentation (hello vidéo explique comment traite les tooreplicate les ordinateurs virtuels VMware, mais hello est similaire pour la réplication de l’ordinateur physique.)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate une stratégie de réplication, cliquez sur **infrastructure de Site Recovery** > **stratégies de réplication** > **+ la stratégie de réplication**.
2. Dans **Créer une stratégie de réplication**, indiquez le nom de la stratégie.
3. Dans **seuil RPO**, spécifiez la limite RPO hello. Cette valeur spécifie la fréquence à laquelle les points de récupération des données sont créés. Une alerte est générée lorsque la réplication continue dépasse cette limite.
4. Dans **rétention du point de récupération**, spécifiez la durée (en heures) est d’une fenêtre de rétention hello pour chaque point de récupération. Machines virtuelles répliquées peuvent être récupérées point tooany dans une fenêtre. Jusqu'à too24 rétention d’heures est pris en charge pour le stockage de machines toopremium répliquées. Jusqu'à too72 rétention d’heures est pris en charge pour le stockage de machines toostandard répliquées.
5. Dans **Fréquence des captures instantanées cohérentes au niveau de l’application**, spécifiez la fréquence de création des points de récupération qui contiennent des captures instantanées cohérentes au niveau de l’application (en minutes). Cliquez sur **OK** stratégie de hello toocreate.

    ![Stratégie de réplication](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. Lorsque vous créez une nouvelle stratégie, il est automatiquement associé serveur de configuration hello. Par défaut, une stratégie de correspondance est automatiquement créée pour la restauration automatique. Par exemple, si hello stratégie de réplication est **rep-policy**, puis de la stratégie de restauration automatique hello est **rep-stratégie de la restauration automatique**. Cette stratégie n’est utilisée qu’à partir du moment où vous initiez une restauration automatique à partir d’Azure.  


## <a name="plan-capacity"></a>Planifier la capacité

1. Votre infrastructure de base est désormais configurée. Vous pouvez donc réfléchir à la planification de la capacité et déterminer si des ressources supplémentaires sont nécessaires. [En savoir plus](site-recovery-plan-capacity-vmware.md).
2. Lorsque vous avez terminé la planification de la capacité, sélectionnez **Oui** dans **Avez-vous effectué une planification de la capacité ?**

   ![Planification de la capacité](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Préparer des machines virtuelles pour la réplication

Tous les ordinateurs que vous souhaitez tooreplicate doivent avoir le service mobilité hello est installé. Vous pouvez installer le service de mobilité hello dans de plusieurs façons :

- Installer le service de hello avec une installation poussée du hello du serveur de processus. Vous avez besoin de machines tooprepare dans avance toouse cette méthode.
- Installer le service de hello à l’aide des outils de déploiement tels que System Center Configuration Manager ou Configuration d’état souhaité Azure Automation.
- Installer le service de hello manuellement.

[En savoir plus](site-recovery-vmware-to-azure-install-mob-svc.md).


## <a name="enable-replication"></a>Activer la réplication

Avant de commencer :

- Votre compte d’utilisateur Azure doit toohave certaines [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’un nouveau tooAzure d’ordinateur virtuel.
- Lorsque vous ajoutez ou modifiez des machines virtuelles, il peut prendre too15 minutes ou plus pour effet de tootake de modifications et les tooappear dans le portail de hello.
- Vous pouvez vérifier l’heure de dernier découvert de hello pour les machines virtuelles dans **serveurs de Configuration** > **dernier Contact à**.
- tooadd machines virtuelles sans attendre la détection planifiée hello, serveur de configuration de mise en surbrillance hello (ne cliquez pas dessus), puis cliquez sur **Actualiser**.
- Si une machine virtuelle est préparée à l’installation push, serveur de processus hello installe automatiquement le service de mobilité hello lorsque vous activez la réplication.
- Regardez une courte vidéo de présentation (hello vidéo explique comment traite les tooreplicate les ordinateurs virtuels VMware, mais hello est similaire pour la réplication de l’ordinateur physique.)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>Exclure les disques de la réplication

Par défaut, tous les disques d’une machine sont répliqués. Vous pouvez exclure des disques de la réplication. Par exemple, vous pouvez tooreplicate les disques avec les données temporaires ou les données qui ont été actualisées chaque fois un redémarrage de l’ordinateur ou de l’application (par exemple, pagefile.sys ou tempdb de SQL Server).

### <a name="replicate-vms"></a>Répliquer des machines virtuelles

1. Cliquez sur **Répliquer l’application** > **Source**.
2. Dans **Source**, sélectionnez **Locale**.
3. Dans **emplacement Source**, sélectionnez nom de serveur de configuration hello.
4. Dans **Type de machine**, sélectionnez **Machines physiques**.
5. Dans **serveur de processus**, choisissez le serveur de processus hello. Si vous n’avez pas créé de tous les serveurs de processus supplémentaire, ce serveur est le serveur de configuration hello. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/site-recovery-physical-to-azure/chooseVM.png)

6. Dans **cible**, sélectionnez hello **abonnement** et hello **groupe de ressources** dans lequel vous souhaitez toocreate hello machines virtuelles Azure après le basculement. Choisissez le déploiement hello modèle que vous souhaitez toouse dans Azure (classique ou le Gestionnaire de ressources) pour hello basculé machines virtuelles.

7. Sélectionnez le compte de stockage Azure hello que toouse souhaité pour répliquer les données. Si vous ne souhaitez pas toouse un compte que vous avez déjà configuré, vous pouvez créer un nouveau.

8. Sélectionnez hello **réseau Azure** et **sous-réseau** toowhich machines virtuelles Azure se connecter après le basculement. Sélectionnez **configurer maintenant pour les machines sélectionnées** tooapply hello réseau paramètre tooall machines que vous sélectionnez pour la protection. Sélectionnez **configurer ultérieurement** tooselect hello réseau Azure par ordinateur. Si vous ne souhaitez pas toouse un réseau existant, vous pouvez créer un.

    ![Activer la réplication](./media/site-recovery-physical-to-azure/targetsettings.png)

9. Dans **machines physiques**, cliquez sur **+ machine physique** et entrez hello **nom** et **adresse IP**. Choisissez un système d’exploitation hello de l’ordinateur de hello souhaité tooreplicate. Il prend quelques minutes jusqu'à ce que les ordinateurs sont découverts et affichés dans la liste de hello.

    ![Activer la réplication](./media/site-recovery-physical-to-azure/machineselect.png)

10. Dans **propriétés** > **configurer les propriétés**, sélectionnez compte hello toobe utilisé par hello processus serveur tooautomatically installer le service de mobilité hello sur l’ordinateur de hello.
11. Par défaut, tous les disques sont répliqués. Cliquez sur **tous les disques**et désactivez les disques que vous ne souhaitez pas tooreplicate. Cliquez ensuite sur **OK**. Vous pouvez configurer des propriétés de machine virtuelle supplémentaires ultérieurement.

    ![Activer la réplication](./media/site-recovery-physical-to-azure/configprop.png)

12. Dans **les paramètres de réplication** > **configurer les paramètres de réplication**, vérifiez que hello correct de la stratégie de réplication est activée. Si vous modifiez une stratégie, les modifications sont appliquée toohello réplication d’ordinateur et les ordinateurs toonew.
13. Activer **la cohérence Multimachine virtuelle** si vous souhaitez toogather ordinateurs dans un groupe de réplication, spécifiez un nom pour le groupe de hello. Cliquez ensuite sur **OK**. Notez les points suivants :

    a. Les machines des groupes de réplication sont répliquées ensemble et ont des points de récupération cohérents après incident et avec les applications lorsqu’elles basculent.

    b. Nous vous recommandons de rassembler les machines virtuelles et les serveurs physiques afin qu’ils reflètent vos charges de travail. L’activation de la cohérence multimachine virtuelle peut affecter les performances de la charge de travail. Elle doit être utilisée uniquement si les ordinateurs sont en cours d’exécution hello la même charge de travail et que vous avez besoin de cohérence.

    ![Activer la réplication](./media/site-recovery-physical-to-azure/policy.png)

14. Cliquez sur **Activer la réplication**. Vous pouvez suivre la progression de hello **activer la Protection** de la tâche dans **paramètres** > **travaux** > **tâches de récupération de Site**. Après avoir hello **finaliser la Protection** travail s’exécute, l’ordinateur de hello est prêt pour le basculement.

Après avoir activé la réplication, hello service mobilité est installé si vous configurez l’installation push. Une fois hello service mobilité par émission de données installée sur un ordinateur, une tâche de protection démarre et échoue. Après l’échec de hello, vous devez toomanually redémarrer chaque machine. Tâche de protection hello commence ensuite à nouveau, et la réplication initiale se produit.


### <a name="view-and-manage-azure-vm-properties"></a>Afficher et gérer les propriétés des machines virtuelles Azure

Nous recommandons que vous vérifiez les propriétés de machine virtuelle hello et apportez les modifications que vous avez besoin.

1. Cliquez sur **éléments répliqués**et sélectionnez hello machine. Hello **Essentials** panneau affiche des informations sur les paramètres des ordinateurs et l’état.
2. Dans **propriétés**, vous pouvez afficher la réplication et les informations de basculement pour hello machine virtuelle.
3. Dans **de calcul et réseau** > **propriétés de calcul**, vous pouvez spécifier la taille de nom et la cible de la machine virtuelle Azure hello. Modifier toocomply de nom hello avec [conditions requises pour Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) si vous avez besoin.
4. Modifier les paramètres d’adresse IP, sous-réseau et réseau de cible hello assignés toohello machine virtuelle Azure :

    a. Vous pouvez définir l’adresse IP de hello cible.

    b.  Si vous ne fournissez pas une adresse, hello basculé utilise DHCP.

    c. Si vous définissez une adresse qui n’est pas disponible au moment du basculement, ce dernier échoue.

    d. Hello même adresse IP peut servir pour le test de basculement si l’adresse de hello est disponible dans le réseau de basculement de test hello.

    e. nombre de Hello de cartes réseau est dicté par taille hello que vous spécifiez pour la machine virtuelle cible hello :

     - Si nombre hello de cartes réseau sur l’ordinateur source de hello est hello identique ou inférieur au nombre de hello de cartes autorisé pour la taille de la machine cible hello, cible de hello a hello même nombre de cartes en tant que source de hello.
     - Si le nombre de cartes pour l’ordinateur virtuel de source hello hello dépasse nombre de hello autorisé pour la taille cible hello, puis taille maximale de la cible hello est utilisé.
     - Par exemple, si un ordinateur source possède deux cartes réseau et la taille de la machine cible hello prend en charge quatre, l’ordinateur cible hello possède deux cartes. Si ordinateur source de hello possède deux cartes, mais prend en charge la taille de la cible hello pris en charge qu’un seul, de l’ordinateur cible hello n'a qu’une seule carte.     
   - Si l’ordinateur virtuel de hello possède plusieurs cartes réseau, ils connectent toohello même réseau.
   - Si machine virtuelle de hello possède plusieurs cartes réseau, puis hello celui affiché dans la liste de hello devient hello *par défaut* carte réseau Bonjour Azure VM.
5. Dans **disques**, vous pouvez voir le système d’exploitation de l’ordinateur virtuel hello et des disques de données hello qui sont répliqués.

## <a name="run-a-test-failover"></a>Exécution d’un test de basculement

Une fois que vous avez configuré tous les éléments, exécutez un toomake de basculement de test que tout fonctionne comme prévu. Visionnez une courte vidéo de présentation avant de commencer.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail sur un seul ordinateur, dans **paramètres** > **répliquées des éléments**, cliquez sur **Test de basculement**.

    ![Test de basculement](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. toofail sur la récupération d’un plan, en **paramètres** > **les Plans de récupération**, plan de hello avec le bouton droit > **Test de basculement**. toocreate un plan de récupération, [suivez ces instructions](site-recovery-create-recovery-plans.md).  
3. Dans **Test de basculement**, sélectionnez hello réseau Azure toowhich machines virtuelles Azure sont connectés après le basculement se produit.
4. Cliquez sur **OK** toobegin hello basculement. Vous pouvez suivre la progression en cliquant sur hello VM tooopen ses propriétés ou en cliquant sur hello **Test de basculement** travail dans le nom du coffre > **paramètres** > **travaux**  >  **Les tâches de récupération de site**.
5. Une fois hello basculement terminé, vous devez également être en mesure de réplica de hello toosee machine Azure s’affichent dans hello portail Azure > **virtuels**. Assurez-vous que cette machine virtuelle hello est la taille appropriée de hello, que sa connexion réseau approprié de toohello, et qu’il s’exécute.
6. Si vous [préparé pour les connexions après le basculement](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), vous devez être en mesure de tooconnect toohello machine virtuelle Azure.
7. Une fois que vous avez terminé, cliquez sur **basculement de test de nettoyage** sur le plan de récupération hello. Dans **Notes**, enregistrer et enregistrer toutes les observations associées au basculement de test hello. Cette étape supprime hello virtuels qui ont été créés pendant le test de basculement.

Pour plus d’informations, consultez hello [tooAzure de basculement de Test](site-recovery-test-failover-to-azure.md) document.

## <a name="next-steps"></a>Étapes suivantes

Après avoir préparer la réplication et en cours d’exécution, lorsqu’une panne se produit vous procédez au basculement tooAzure et machines virtuelles Azure sont créés à partir des données de hello répliquée. Vous pouvez ensuite accéder des charges de travail et des applications dans Azure, jusqu'à ce que vous ne parvenez pas emplacement principal d’arrière tooyour lorsqu’elle retourne les opérations de toonormal.

- [En savoir plus](site-recovery-failover.md) sur différents types de basculement et la manière dont toorun les.
- Si vous migrez des ordinateurs au lieu de procéder à une réplication et une restauration automatique, [lisez cet article pour en savoir plus](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- Lors de la réplication des machines physiques, vous pouvez uniquement à la restauration automatique tooa VMware environnement. [En savoir plus sur la restauration automatique](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>Informations et remarques relatives aux logiciels tiers
Do Not Translate or Localize

logiciels de Hello et de microprogramme en cours d’exécution hello produit Microsoft ou service repose sur ou inclut, du contenu à partir de hello projets répertoriés ci-dessous (collectivement, « Code tiers »). Microsoft n’est pas hello auteur d’origine hello Code tiers. mention de copyright d’origine Hello et de licence, dans lesquelles Microsoft a reçu ce Code tiers, sont définies ci-dessous.

informations Hello dans la Section A sont concernant le Code de tiers des composants à partir de projets de hello répertoriées ci-dessous. Such licenses and information are provided for informational purposes only. Ce Code de tiers est en cours tooyou relicensed par Microsoft hello produit ou service Microsoft termes du contrat de licence des logiciels de Microsoft.  

informations Hello dans la Section B concernant les composants de Code de tiers qui sont établies tooyou disponible par Microsoft sous les termes du contrat de licence d’origine hello.

fichier dans son intégralité Hello se trouvent sur hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel, or otherwise.
