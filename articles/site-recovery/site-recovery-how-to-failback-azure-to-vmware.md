---
title: toofail aaaHow de tooVMware Azure | Documents Microsoft
description: "Après le basculement des machines virtuelles tooAzure, vous pouvez lancer une restauration automatique toobring machines virtuelles arrière tooon local. Découvrez les étapes hello pour comment toofail sauvegarder."
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
ms.openlocfilehash: b82abf6b15db9dccab49edbd14298b121e9fdc6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-from-azure-tooan-on-premises-site"></a>Échec de tooan Azure site local

Cet article décrit comment toofail sauvegarder des ordinateurs virtuels à partir de Machines virtuelles Azure toohello sur site local. Suivez les instructions dans cette toofail article hello sauvegarder vos machines virtuelles VMware ou les serveurs physiques Windows/Linux après leur avez basculé de hello local site tooAzure à l’aide de hello [les ordinateurs virtuels VMware de répliquer et physique tooAzure de serveurs avec Azure Site Recovery](site-recovery-vmware-to-azure-classic.md) didacticiel.

> [!WARNING]
> Si vous avez [terminé la migration](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), les ressources, groupe ou supprimés de tooanother d’ordinateurs virtuels hello déplacé hello machine virtuelle Azure, vous ne pouvez pas la restauration automatique par la suite.

> [!NOTE]
> Si vous n’avez pas sur les ordinateurs virtuels VMware puis vous ne pouvez pas la restauration automatique tooa Hyper-v hôte.

## <a name="overview-of-failback"></a>Vue d’ensemble de la restauration automatique
Voici comment fonctionne la restauration automatique. Après avoir basculé tooAzure, vous ne parvenez pas tooyour arrière sur site local en quelques étapes :

1. [Protégez de nouveau](site-recovery-how-to-reprotect.md) hello des machines virtuelles sur Azure pour qu’ils commencer tooreplicate tooVMware virtuels dans votre site local. Dans le cadre de ce processus, vous devez également :
    1. Configurer un serveur cible maître local : Windows pour les machines virtuelles Windows et [Linux](site-recovery-how-to-install-linux-master-target.md) pour les machines virtuelles Linux.
    2. Configurer un [serveur de processus](site-recovery-vmware-setup-azure-ps-resource-manager.md).
    3. Lancer la [reprotection](site-recovery-how-to-reprotect.md). Cela désactiver ordinateur virtuel local, hello et synchroniser hello Azure des données de l’ordinateur virtuel avec hello disques sur site.
5. Une fois que vos machines virtuelles sur Azure répliquez tooyour sur site local, vous lancez un basculement sur depuis Azure toohello sur site local.

Une fois que vos données a échoué en retour, vous protégez de nouveau les machines virtuelles hello local que vous n’avez pas à, afin qu’ils démarrent tooreplicate tooAzure.

Pour obtenir une présentation rapide, regardez hello suivant vidéo sur comment toofail sur à partir d’Azure tooan site local.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-toohello-original-or-alternate-location"></a>Échec d’origine ou sur un autre emplacement du toohello précédent

Si vous avez effectué sur un ordinateur virtuel VMware, vous pouvez échouer arrière toohello même ordinateur virtuel local de source s’il est encore existe. Dans ce scénario, seules les modifications de hello sont répliquées en retour. Ce scénario est appelé restauration dans l’emplacement d’origine. Si l’ordinateur virtuel local, hello n’existe pas, le scénario de hello est une récupération à autre emplacement.

> [!NOTE]
> Vous pouvez uniquement vCenter de la restauration automatique toohello d’origine et le serveur de configuration. Vous ne pouvez pas déployer un nouveau serveur de configuration et procéder à une restauration automatique au moyen de celui-ci. En outre, Impossible d’ajouter un nouveau vCenter toohello sortie configuration serveur et la restauration automatique en vCenter de nouveau hello.

#### <a name="original-location-recovery"></a>Récupération à l’emplacement d’origine

Si l’échec de l’ordinateur virtuel d’origine de toohello arrière, hello conditions suivantes est requise :
* Si l’ordinateur virtuel de hello est géré par un serveur vCenter, puis hello ESX hôte du serveur cible maître doit avoir banque de données de la machine virtuelle accès toohello.
* Si hello virtuel se trouve sur un ordinateur hôte ESX, mais il n’est pas géré par vCenter, puis hello le disque de machine virtuelle de hello doit être dans un magasin de données hôte de cette cible maître hello peut accéder.
* Si votre machine virtuelle se trouve sur un ordinateur hôte ESX et n’utilise pas vCenter, vous devez effectuer la détection de l’ordinateur hôte ESX hello du serveur cible maître hello avant que vous protégez de nouveau. Cela s’applique si vous restaurez automatiquement les serveurs physiques.
* Vous ne parvenez pas tooa arrière réseau virtuel (vSAN) ou un disque en fonction de RDM (RDM) si les disques hello existent déjà et locale de toohello connecté l’ordinateur virtuel.

#### <a name="alternate-location-recovery"></a>Récupération à un autre emplacement
Si hello locaux virtuels n’existe pas avant la reprotection de machine virtuelle de hello, hello scénario corresponde à une récupération à autre emplacement. flux de travail de reprotection Hello crée de nouveau hello locaux virtuels. Cela entraîne également le téléchargement complet de données.

* Lorsque vous ne parvenez pas tooan arrière autre emplacement, hello virtuels sera récupérée toohello même ordinateur hôte ESX sur le hello serveur cible maître est déployé. Hello banque de données qui a utilisé des disques de hello toocreate sera hello même magasin de données qui a été sélectionnée lors de la reprotection de machine virtuelle de hello.
* Vous pouvez échouer seulement tooa machine virtuelle fichier système (VMFS) banque de données. Si vous utilisez un disque vSAN ou RDM, la reprotection et la restauration automatique ne fonctionneront pas.
* Reprotection implique un transfert de grande taille initiale des données qui est suivi par les modifications hello. Ce processus existe, car la machine virtuelle de hello n’existe pas sur le site. les données complètes Hello doivent toobe répliquée précédent. Cette reprotection prendra également plus de temps que la récupération sur l’emplacement d’origine.
* Vous ne peuvent pas basculer précédent toovSAN ou RDM basés sur des disques. Seuls les nouveaux disques de machine virtuelle (VMDK) peuvent être créés sur un magasin de données VMFS.

Échec de l’un ordinateur physique, lorsque basculé tooAzure, sauvegarder uniquement en tant que machine virtuelle VMware (également désignée tooas P2A2V). Ce flux relève de la récupération à autre emplacement hello.

* Un serveur physique Windows Server 2008 R2 SP1, si protégé et basculé tooAzure, ne peut pas être rétablie.
* Assurez-vous que vous découvriez au moins un serveur cible maître serveur et hello nécessaire ESX/ESXi hôtes toowhich vous devez toofail précédent.

## <a name="have-you-completed-reprotection"></a>Vous avez terminé la reprotection ?
Avant de continuer, hello complète Protégez-les étapes afin que les machines virtuelles de hello sont dans un état répliqué, et vous pouvez lancer un site local de tooan précédent basculement. Pour plus d’informations, consultez [comment tooreprotect à partir d’Azure site tooon](site-recovery-how-to-reprotect.md).

## <a name="prerequisites"></a>Composants requis

* Un serveur de configuration est requis localement, lorsque vous effectuez une restauration automatique. Lors du retour arrière, ordinateur virtuel de hello doit exister dans la base de données de serveur de configuration hello ou la restauration automatique ne réussisse. Veillez donc à effectuer des sauvegardes régulières de votre serveur. En cas de sinistre, vous devez serveur hello toorestore hello même adresse IP pour la restauration automatique toowork.
* serveur cible maître de Hello ne devez pas les captures instantanées avant de déclencher la restauration automatique.

## <a name="steps-toofail-back"></a>Toofail étapes précédent

> [!IMPORTANT]
> Avant de lancer la restauration automatique, vérifiez que vous avez terminé de machines virtuelles de hello protéger. machines virtuelles de Hello doit être dans un état de protection et leur intégrité doit être **OK**. machines virtuelles tooreprotect hello lire [comment tooreprotect](site-recovery-how-to-reprotect.md).

1. Bonjour éléments répliqués page, sélectionnez l’ordinateur virtuel de hello et faites un clic droit tooselect **basculement non planifié**.
2. Dans **confirmer le basculement**, vérifiez le sens du basculement hello (à partir de Azure) et sélectionnez hello point de récupération (la plus récente ou dernière application hello cohérente) que vous souhaitez toouse pour le basculement hello. état cohérent application Hello est derrière les plus récentes hello dans le temps et entraîne une perte de données.
3. Pendant le basculement, récupération de Site arrête de machines virtuelles de hello sur Azure. Après avoir vérifié que la restauration est terminé comme prévu, vous pouvez vérifier que les ordinateurs virtuels de hello sur Azure a été arrêtés.

### <a name="toowhat-recovery-point-can-i-fail-back-hello-virtual-machines"></a>point de récupération toowhat puis-je basculer la fonctionnalité machines virtuelles que hello précédent ?

Lors de la restauration automatique, vous avez deux options toofail arrière hello/récupération d’ordinateur virtuel plan.

Si vous sélectionnez point de hello dernière traité dans le temps, toutes les machines virtuelles basculeront tootheir dernière version disponible point dans le temps. Au cas où un groupe de réplication dans le plan de récupération hello, chaque ordinateur virtuel hello du groupe de réplication échoue sur tooits indépendants dernier point dans le temps.

Vous ne pouvez pas restaurer une machine virtuelle, tant qu’elle n’a pas un point de récupération. Vous ne pouvez pas restaurer automatiquement un plan de récupération, tant que toutes ses machines virtuelles n’ont pas au moins un point de récupération.

> [!NOTE]
> Le point de récupération le plus récent est un point de récupération cohérent en cas d’incident.

Si vous sélectionnez le point de récupération cohérent d’application hello, une restauration automatique d’une seule machine virtuelle récupérera tooits dernier point de récupération cohérents avec les applications disponibles. Dans le cas de hello d’un plan de récupération avec un groupe de réplication, chaque groupe de réplication permet de récupérer tooits commun point de récupération disponible.
Notez que les points de récupération cohérents d’application peuvent se trouver dans le passé et qu’une perte de données est susceptible de se produire.

### <a name="what-happens-toovmware-tools-post-failback"></a>Que se passe-t-il tooVMware outils valider la restauration automatique ?

Pendant le basculement tooAzure, les outils VMware hello ne peut pas s’exécuter sur hello machine virtuelle Azure. En cas d’une machine virtuelle Windows, ASR désactive les outils VMware hello pendant le basculement. En cas de l’ordinateur virtuel Linux, ASR désinstalle les outils VMware hello pendant le basculement.

Pendant la restauration automatique de l’ordinateur virtuel Windows hello, les outils VMware hello sont réactivés lors de la restauration automatique. De même, pour une machine virtuelle linux, les outils VMware hello sont réinstallés sur l’ordinateur de hello lors de la restauration automatique.

## <a name="next-steps"></a>Étapes suivantes

Une fois la restauration terminée, vous devez toocommit tooensure de machine virtuelle hello récupération des machines virtuelles dans Azure sont supprimés.

### <a name="commit"></a>Validation
La validation est hello tooremove requis a échoué sur l’ordinateur virtuel à partir d’Azure.
Élément de hello protégé d’avec le bouton droit, puis cliquez sur **valider**. Un travail supprime hello basculé de machines virtuelles dans Azure.

### <a name="reprotect-from-on-premises-tooazure"></a>Protégez de nouveau à partir de local tooAzure

Une fois la validation terminée, votre machine virtuelle est à nouveau hello sur site local, mais il ne sera pas être protégé. là encore, toostart tooreplicate tooAzure hello suivant :

1. Dans **coffre** > **paramètre** > **éléments répliqués**, sélectionnez hello des ordinateurs virtuels qui ont échoué précédent, puis cliquez sur  **Protégez de nouveau**.
2. Donner une valeur hello hello du serveur de processus nécessitant tooAzure arrière des données toosend toobe utilisé.
3. Cliquez sur **OK** travaux de reprotection toobegin hello.

> [!NOTE]
> Après le démarrage d’une machine virtuelle de local, il prend un certain temps pour l’agent de hello serveur de configuration tooregister toohello arrière (vers le haut too15 minutes). Pendant ce temps, restaurez la protection échoue et retourne un message d’erreur indiquant que l’agent hello n’est pas installé. Patientez quelques minutes et essayez de relancer la reprotection.

Après hello Protégez-les fin du travail de machine virtuelle de hello réplique tooAzure précédent et vous pouvez effectuer un basculement.

## <a name="common-issues"></a>Problèmes courants
Assurez-vous que vCenter hello est dans un état connecté avant d’effectuer une restauration automatique. Dans le cas contraire, déconnexion des disques et les joindre toohello précédent l’ordinateur virtuel échoue.
