---
title: "aaaReprotect à partir du site local de Azure tooan | Documents Microsoft"
description: "Après le basculement des machines virtuelles tooAzure, vous pouvez lancer une toobring de la restauration automatique différé tooon-local de machines virtuelles. Découvrez comment tooreprotect avant une restauration automatique."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 94c86e79cba4cd3f0c5821fdd5509cca1d0e7820
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-azure-tooan-on-premises-site"></a>Protégez de nouveau à partir du site local de Azure tooan



## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment tooreprotect Azure machines virtuelles à partir du site local de tooan Azure. Suivez les instructions dans cet article lorsque vous êtes prêt toofail hello sauvegarder vos machines virtuelles VMware ou les serveurs physiques Windows/Linux après avoir basculé de hello local site tooAzure (comme décrit dans [virtuel VMware répliquer ordinateurs et tooAzure des serveurs physiques avec Azure Site Recovery](site-recovery-failover.md)).

> [!WARNING]
> Vous ne pouvez pas restauré après vous [terminer la migration](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), déplacer un groupe de ressources d’ordinateur virtuel tooanother ou supprimer une machine virtuelle Azure.


Une fois la reprotection est terminée et hello machines virtuelles protégées sont répliqués, vous pouvez lancer une restauration automatique sur hello machines virtuelles toobring les toohello sur site local.

Valider des commentaires ou des questions à fin hello de cet article ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Pour obtenir une présentation rapide, regardez hello suivant vidéo sur comment toofail sur à partir d’Azure tooan site local.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="prerequisites"></a>Composants requis
Lorsque vous préparez les ordinateurs virtuels tooreprotect, prendre ou envisagez de hello suit les actions préalables requises :

* Si un serveur vCenter gère hello ordinateurs virtuels que vous souhaitez toofail sur, assurez-vous que vous avez hello [autorisations requises](site-recovery-vmware-to-azure-classic.md) pour la découverte des ordinateurs virtuels sur les serveurs vCenter.

  > [!WARNING]
  > Si les instantanés sont présents sur hello local maître hello ou cible de la machine virtuelle, la reprotection échoue. Vous pouvez supprimer les captures instantanées de hello sur le serveur cible maître hello avant de continuer tooreprotect. instantanés Hello sur l’ordinateur virtuel de hello sont fusionnées automatiquement lors d’un travail de reprotection.

* Avant de procéder à une restauration automatique, créez deux autres composants :

  * **Serveur de processus**: hello [serveur de processus](site-recovery-vmware-setup-azure-ps-resource-manager.md) reçoit des données à partir de la machine virtuelle de hello protégée dans Azure et envoie des données toohello sur site local. Un réseau à latence faible est requis entre le serveur de processus hello et hello protégé virtual machine. Par conséquent, vous pouvez avoir un serveur de processus local si vous utilisez une connexion Azure ExpressRoute ou un serveur de processus basé sur Azure et un VPN.
  
  * **Serveur cible maître**: serveur cible maître de hello reçoit les données de la restauration automatique. serveur d’administration Hello local que vous avez créé a un serveur cible maître installé par défaut. Toutefois, en fonction du volume hello du trafic de sauvegarde a échoué, vous devrez peut-être toocreate un serveur cible maître distinct pour la restauration automatique.
    * [Si vous avez une machine virtuelle Linux, vous avez besoin d’un serveur cible maître Linux](site-recovery-how-to-install-linux-master-target.md).
    * Si vous avez une machine virtuelle Windows, vous avez besoin d’un serveur cible maître Windows. Vous pouvez réutiliser hello local processus serveur et maître d’ordinateurs cibles.

    serveur cible maître Hello a d’autres conditions requises répertoriées dans [toocheck d’opérations courantes sur un serveur cible maître avant de reprotection](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server).

* Un serveur de configuration est requis en local lorsque vous effectuez une restauration automatique. Lors du retour arrière, machine virtuelle de hello doit exister dans la base de données de serveur de configuration hello. Sinon, la restauration automatique échoue. 

> [!IMPORTANT]
> Veillez à effectuer des sauvegardes régulières de votre serveur de configuration. S’il existe un reprise après sinistre, restaurez serveur hello avec hello d’adresses IP même afin que la restauration automatique fonctionne.

* Ensemble hello `disk.EnableUUID=true` définissant dans les paramètres de configuration hello de hello cible maître virtual machine dans VMware. Si cette ligne n’existe pas, ajoutez-la. Ce paramètre est requis tooprovide un disque de machine virtuelle toohello UUID cohérent (VMDK) afin qu’il monte correctement.

* *Vous ne pouvez pas utiliser Storage vMotion sur le serveur cible maître de hello*. Cela peut entraîner des toofail de la restauration automatique hello. machine virtuelle de Hello ne peut pas démarrer, car les disques hello ne sont pas tooit disponible. tooprevent ce problème, excluez hello cible maître serveurs dans votre liste de vMotion.

* Ajouter un nouveau serveur cible maître de toohello lecteur : un lecteur de rétention. Ajouter un nouveau lecteur hello disque et le format.


### <a name="frequently-asked-questions"></a>Forum Aux Questions

#### <a name="why-do-i-need-a-s2s-vpn-or-an-expressroute-connection-tooreplicate-data-back-toohello-on-premises-site"></a>Pourquoi ai-je besoin d’un VPN S2S ou un site local de ExpressRoute connexion tooreplicate données toohello précédent ?
Alors que la réplication à partir de local tooAzure peut se produire sur hello Internet ou une connexion qui a l’homologation publique ExpressRoute, protéger et restauration requièrent un site à site (S2S) données tooreplicate VPN. Fournir les réseau hello afin que les machines virtuelles Azure hello basculé peut atteindre le serveur de configuration local (ping) hello. Vous pouvez également déployer un serveur de processus Bonjour Azure réseau d’ordinateur virtuel de basculé hello. Ce serveur de processus doit également être en mesure de toocommunicate avec le serveur de configuration local hello.

#### <a name="when-should-i-install-a-process-server-in-azure"></a>Quand convient-il d’installer un serveur de processus dans Azure ?


machines virtuelles Azure que vous souhaitez tooreprotect Hello envoyer un serveur de processus de réplication données tooa. Configurer votre réseau afin que les machines virtuelles de hello sur Azure peut atteindre le serveur de processus hello.

Vous pouvez déployer un serveur de traitement dans Azure ou utilisez hello existante serveur de processus que vous avez utilisé pendant le basculement. tooconsider point important de Hello est hello toosend hello données de latence de machines virtuelles de hello sur le serveur de processus toohello Azure.

Si vous avez une connexion ExpressRoute, vous pouvez utiliser des processus serveur toosend données locales, car la latence entre la machine virtuelle de hello et serveur de processus hello hello est faible.

 ![Diagramme d’architecture pour ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)



Toutefois, si vous avez uniquement un VPN S2S, nous vous recommandons de déployer le serveur de processus hello dans Azure.

 ![Diagramme d’architecture pour VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)


N’oubliez pas que la réplication se produit uniquement sur hello S2S VPN ou hello privé d’homologation de votre réseau ExpressRoute. Assurez-vous de disposer de suffisamment de bande passante sur ce réseau.

Pour plus d’informations sur l’installation d’un serveur de processus basé sur Azure, consultez [Gérer un serveur de processus en cours d’exécution dans Azure (Resource Manager)](site-recovery-vmware-setup-azure-ps-resource-manager.md).

> [!TIP]
> Nous vous recommandons d’utiliser un serveur de processus basé sur Azure lors de la restauration automatique. performances de la réplication Hello sont plus élevée si le serveur de processus hello est proche toohello réplication de l’ordinateur virtuel (ordinateur hello basculé dans Azure). Toutefois, pendant la phase de preuve de concept (POC) ou de démonstration, vous pouvez utiliser serveur de traitement local hello avec ExpressRoute avec privés d’homologation toocomplete hello preuve de concept plus rapide.



#### <a name="what-ports-should-i-open-on-different-components-so-that-reprotection-can-work"></a>Quels ports dois-je ouvrir sur les différents composants pour que la reprotection fonctionne ?

![Ports pour le basculement et la restauration automatique](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

#### <a name="which-master-target-server-should-i-use-for-reprotection"></a>Quel serveur cible maître dois-je utiliser pour la reprotection ?
Un serveur de la cible maître local est données tooreceive requis hello du serveur de processus, puis écrivez VMDK l’ordinateur virtuel toohello local. Si vous protégez des machines virtuelles Windows, vous avez besoin d’un serveur cible maître Windows. Vous pouvez réutiliser le serveur de traitement local hello et la cible maître<!-- !todo component -->. Pour les ordinateurs virtuels Linux, vous devez tooset une cible maître Linux de locales supplémentaires.


Pour plus d’informations sur l’installation d’un serveur cible maître, consultez :

* [Comment tooinstall Windows maître serveur cible](site-recovery-vmware-to-azure.md)
* [Comment tooinstall Linux maître serveur cible](site-recovery-how-to-install-linux-master-target.md)


#### <a name="what-datastore-types-are-supported-on-hello-on-premises-esxi-host-during-failback"></a>Les types de banque de données sont pris en charge sur l’ordinateur hôte de ESXi hello local lors de la restauration automatique ?

Actuellement, prend en charge d’Azure Site Recovery échouent sauvegarde le système de fichiers de machine virtuelle tooa (VMFS) ou de banque de données vSAN. Les banques de données NFS ne sont pas prises en charge. En raison de la limitation de toothis, hello banque de données d’entrée de sélection sur hello reprotection écran est vide dans le cas de hello de magasins de données NFS, ou il affiche la banque de données vSAN hello mais échoue lors de la tâche de hello. Si vous envisagez de toofail précédent, vous pouvez créer une banque de données VMFS localement et échouer tooit précédent. Cette restauration provoque un téléchargement complet du hello VMDK.

### <a name="common-things-toocheck-after-completing-installation-of-hello-master-target-server"></a>Toocheck de choses commun après avoir terminé l’installation du serveur cible maître de hello

* Si hello ordinateur virtuel est présent sur le site sur Bonjour serveur vCenter, hello serveur cible maître a besoin d’accéder à VMDK l’ordinateur virtuel toohello local. L’accès est nécessaire toowrite hello répliquée données toohello de disques de machine virtuelle. Vérifiez le que magasin de données du que hello virtual machine locale est monté sur l’hôte de la cible maître hello avec accès en lecture/écriture.

* Si la machine virtuelle de hello n’est pas présent localement sur le serveur vCenter hello, hello service Site Recovery doit toocreate un nouvel ordinateur virtuel pendant la reprotection. Cet ordinateur virtuel est créé sur l’ordinateur hôte ESX hello sur lequel vous créez le serveur cible maître hello. Choisissez avec soin, ordinateur hôte ESX hello afin que l’ordinateur virtuel de la restauration automatique hello est créé sur l’ordinateur hôte hello que vous souhaitez.

* *Vous ne pouvez pas utiliser Storage vMotion pour le serveur cible maître de hello*. Cela peut entraîner des toofail de la restauration automatique hello. machine virtuelle de Hello ne peut pas démarrer, car les disques hello ne sont pas tooit disponible.

  > [!WARNING]
  > Si un serveur cible maître subit une tâche de vMotion de stockage après la reprotection, les disques virtuels hello protégé attaché toohello serveur cible maître migrent cible toohello de tâche de vMotion hello. Si vous essayez toofail après cela, le détachement du disque de hello échoue, car les disques hello sont introuvables. Il devient alors les disques dur toofind hello dans vos comptes de stockage. Vous devez toofind les manuellement et les joindre la machine virtuelle de toohello. Après cela, hello locaux virtuels pouvant être démarré.

* Ajouter un serveur cible maître de Windows existant de rétention lecteur tooyour. Ajouter un nouveau lecteur hello disque et le format. lecteur de rétention Hello est utilisé toostop hello points dans le temps lorsque hello virtual machine réplique toohello arrière sur site local. Vous trouverez ci-après quelques critères d’un lecteur de rétention. Sans ces critères, lecteur de hello ne sera pas répertorié pour le serveur cible maître de hello.

   * volume de Hello n’est pas utilisé à d’autres fins, par exemple une cible de réplication.

   * volume de Hello n’est pas en mode verrouillage.

   * volume de Hello n’est pas un volume de cache. installation du serveur cible maître Hello ne doit pas exister sur ce volume. le volume d’installation personnalisée Hello pour hello processus serveur et principale cible n’est pas éligible pour un volume de rétention. Lorsque le serveur de processus hello et cible maître sont installés sur un volume, volume de hello est un volume de cache du serveur cible maître hello.

   * type de système de fichiers Hello du volume de hello n’est pas FAT ou FAT32.

   * capacité du volume Hello est différente de zéro.

   * volume de rétention par défaut Hello pour Windows est un volume de hello R.

   * volume de rétention par défaut Hello pour Linux est /mnt/retention.

  > [!IMPORTANT]
  > Vous devez tooadd un nouveau lecteur si vous utilisez un ordinateur de serveur de configuration du serveur/processus existant ou une échelle ou un ordinateur de serveur de processus serveur/principale cible. nouveau lecteur de Hello doit répondre à hello précédant la configuration requise. Si le lecteur de rétention hello n’est pas présent, il n’apparaît pas dans la liste de déroulante Sélection hello sur le portail hello. Après avoir ajouté un lecteur toohello local serveur cible maître, elle occupe minutes too15 tooappear de lecteur hello de sélection hello sur le portail hello. Vous pouvez également actualiser le serveur de configuration hello si le lecteur de hello n’apparaît pas après 15 minutes.

* Une machine virtuelle Linux basculée requiert un serveur cible maître Linux. Si vous avez une machine virtuelle Windows basculée, vous avez besoin d’un serveur cible maître Windows.

* Installer les outils VMware sur le serveur cible maître de hello. Sans les outils VMware hello, hello des magasins de données sur l’ordinateur hôte de la cible maître hello ESXi ne peut pas être détecté.

* Activer hello `disk.EnableUUID=true` paramètre sur l’ordinateur de virtuel hello cible maître à l’aide des propriétés de vCenter hello. <!-- !todo Needs link. -->

* serveur cible maître Hello doit avoir au moins une banque de données VMFS attaché. S’il en existe aucun, hello **banque de données** entrée sur la page de reprotection hello est vide, et vous ne pouvez pas continuer.

* serveur cible maître de Hello ne peut pas avoir des captures instantanées sur des disques hello. S’il existe des captures instantanées, l’opération de reprotection et de restauration automatique échoue.

* serveur cible maître Hello ne peut pas avoir un contrôleur Paravirtual SCSI. contrôleur de Hello peut être uniquement un contrôleur LSI Logic. Sans contrôleur LSI Logic, la reprotection échoue.

<!--
### Failback policy
tooreplicate back tooon-premises, you will need a failback policy. This policy get automatically created when you create a forward direction policy. Note that

1. This policy gets auto associated with hello configuration server during creation.
2. This policy is not editable.
3. hello set values of hello policy are (RPO Threshold = 15 Mins, Recovery Point Retention = 24 Hours, App Consistency Snapshot Frequency = 60 Mins)
   ![](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

-->

## <a name="steps-tooreprotect"></a>Étapes tooreprotect

> [!NOTE]
> Une fois un ordinateur virtuel démarre dans Azure, il prend un certain temps pour l’agent de hello serveur de configuration tooregister toohello arrière (vers le haut too15 minutes). Pendant ce temps, la reprotection échoue et un message d’erreur indique que l’agent hello n’est pas installé. Patientez quelques minutes et essayez de relancer la reprotection.



1. Dans **coffre** > **éléments répliqués**, avec le bouton droit de machine virtuelle hello été basculée, puis sélectionnez **Reprotéger**. Vous pouvez également cliquer sur hello machine et sélectionnez **Reprotéger** hello boutons de commande.
2. Dans le panneau de hello, notez cette direction hello de protection, **Azure local tooOn**, est déjà sélectionné.
3. Dans **serveur cible maître** et **serveur de processus**hello du serveur de processus et sélectionnez le serveur cible maître de local hello.
4. Pour **banque de données**, sélectionnez hello toowhich de banque de données vous souhaitez toorecover hello disques locaux. Cette option est utilisée lors de la machine virtuelle de local hello est supprimée, et vous devez toocreate nouveaux disques. Cette option est ignorée si les disques hello existent déjà, mais vous devez toospecify une valeur.
5. Choisissez un lecteur de rétention hello.
6. stratégie de restauration automatique Hello est sélectionné automatiquement.
7. Cliquez sur **OK** toobegin reprotection. Un travail commence tooreplicate hello virtual machine à partir du site local de toohello Azure. Vous pouvez suivre la progression de hello sur hello **travaux** onglet.

Si vous souhaitez toorecover tooan autre emplacement (lorsque l’ordinateur virtuel local, hello est supprimé), sélectionnez le lecteur de rétention hello et magasin de données qui sont configurés pour le serveur cible maître de hello. Lorsque vous ne parvenez pas toohello arrière sur site local, hello VMware des ordinateurs virtuels en cours d’utilisation de plan de protection de la restauration automatique hello hello même magasin de données en tant que hello principal serveur cible. Une nouvelle machine virtuelle est créée dans vCenter.

Si vous souhaitez toorecover hello virtual machine tooan Azure existant local machine virtuelle, hello de montage local banques de données de l’ordinateur virtuel avec un accès en lecture/écriture sur l’hôte de ESXi du serveur cible maître de hello.
    ![Boîte de dialogue Reprotéger](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

Vous pouvez également protéger de nouveau au niveau de hello d’un plan de récupération. Un groupe de réplication peut uniquement être reprotégé via un plan de récupération. Lorsque vous protégez de nouveau à l’aide d’un plan de récupération, vous avez besoin de valeurs de hello tooprovide pour chaque ordinateur protégé.

> [!NOTE]
> Utilisez hello tooreprotect de serveur cible maître même un groupe de réplication. Si vous utilisez un tooreprotect du serveur cible maître différents un groupe de réplication, serveur de hello ne peut pas fournir un point commun dans le temps.

> [!NOTE]
> ordinateur virtuel local, Hello est mis hors tension pendant la reprotection. Cela permet de garantir la cohérence des données pendant la réplication. N’activez pas sur l’ordinateur virtuel de hello une fois la reprotection terminée.

Une fois la reprotection de hello réussit, hello virtuels sera entrer dans un état protégé.

## <a name="next-steps"></a>Étapes suivantes

Une fois la machine virtuelle de hello a entré un état protégé, vous pouvez [lancer une restauration automatique](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back). 

la restauration automatique Hello s’arrête à la machine virtuelle de hello dans Azure et démarrer l’ordinateur virtuel local hello. Prévoyez un temps d’arrêt pour l’application hello. Choisissez une heure pour la restauration automatique lors de l’application hello peut tolérer un temps mort.

## <a name="common-problems"></a>Problèmes courants

* Si vous avez utilisé un modèle toocreate vos machines virtuelles, assurez-vous que chaque machine virtuelle possède son propre UUID pour les disques de hello. Si hello local conflits UUID de la machine virtuelle avec celle du serveur cible maître hello, car les deux ont été créés à partir de hello même la reprotection de modèle, échoue. Déployer un autre serveur cible maître qui n’a été créée à partir de hello même modèle.

* Si vous effectuez une découverte utilisateur vCenter en mode lecture seule et protégez des machines virtuelles, la protection réussit et le basculement fonctionne. Lors de la reprotection, basculement échoue, car il est hello banques de données ne peut pas être découvert. Un problème est que hello banques de données ne sont pas répertoriés lors de la reprotection. tooresolve ce problème, vous pouvez mettre à jour d’informations d’identification de hello vCenter avec un compte approprié qui possède les autorisations et recommencez la tâche de hello. Pour plus d’informations, consultez [les ordinateurs virtuels VMware de répliquer et tooAzure des serveurs physiques avec Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).

* Lorsque vous restaurez automatiquement à une machine virtuelle Linux et l’exécuter localement, vous pouvez voir que ce package du Gestionnaire de réseau hello a été désinstallé de la machine de hello. Cette désinstallation se produit, car le package du Gestionnaire de réseau hello est supprimé lors de la récupération de la machine virtuelle de hello dans Azure.

* Lorsqu’une machine virtuelle Linux est configurée avec une adresse IP statique et est basculée tooAzure, adresse IP de hello est acquis à partir de DHCP. Lorsque vous basculez tooon local, ordinateur virtuel de hello continue adresse IP de toouse DHCP tooacquire hello. Manuellement connectez-vous toohello machine et définir les hello tooa arrière statique adresse si nécessaire. Une machine virtuelle Windows peut récupérer son adresse IP fixe.

* Si vous utilisez la version gratuite d’ESXi 5.5 ou de vSphere 6 Hypervisor, le basculement aboutit, mais la restauration automatique ne fonctionnera pas. restauration automatique tooenable, la licence d’évaluation du programme de mise à niveau tooeither.

* Si vous ne pouvez pas contacter le serveur de configuration de hello hello du serveur de processus, utilisez le serveur de configuration toohello Telnet toocheck connectivité sur le port 443. Vous pouvez également essayer le serveur de configuration tooping hello hello du serveur de processus. Un serveur de processus doit également avoir une pulsation lorsqu’il est le serveur de configuration toohello connecté.

* Si vous essayez de vCenter de remplacement toofail tooan arrière, assurez-vous que votre nouveau vCenter et le serveur cible maître de hello sont détectés. Courant est que les banques de données hello ne sont pas accessibles ou visibles Bonjour **Reprotéger** boîte de dialogue.

* Un serveur Windows Server 2008 R2 SP1 qui est protégé comme un physique serveur local n’est possible de site local de tooan Azure.
