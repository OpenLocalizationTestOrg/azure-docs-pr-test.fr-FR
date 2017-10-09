---
title: "tooReprotect aaaHow de basculé tooprimary arrière de machines virtuelles région Azure | Documents Microsoft"
description: "Après le basculement des machines virtuelles à partir d’une région Azure tooanother, vous pouvez utiliser des ordinateurs de hello tooprotect Azure Site Recovery dans le sens inverse. Découvrez comment les étapes à hello toodo une reprotection avant un basculement à nouveau."
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
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a>Reprotection de basculé région tooprimary arrière de région Azure



>[!NOTE]
>
> La réplication Site Recovery pour les machines virtuelles Azure est actuellement en préversion.


## <a name="overview"></a>Vue d'ensemble
Lorsque vous [basculement](site-recovery-failover.md) hello les machines virtuelles à partir d’une région Azure tooanother, hello virtuels sont dans un état non protégé. Si vous souhaitez toobring les toohello la région principale, vous devez toofirst protéger à nouveau des machines virtuelles de hello et de basculement. La façon d’opérer le basculement ne change pas, quelle que soit la direction du basculement. De même, validez activer la protection des machines virtuelles de hello, il n’existe aucune différence entre hello reprotection après basculement, ou la restauration automatique de la publication.
flux de travail tooexplain hello de reprotection et tooavoid confusion, nous allons utiliser hello site principal des ordinateurs de hello protégé en tant que la région Asie et site de récupération hello des machines de hello en tant que la région Asie du Sud-est. Pendant le basculement, vous allez la région Asie du Sud-est toohello basculement hello machines virtuelles. Avant la restauration, vous devez tooreprotect hello virtual machines à partir de l’Asie du Sud-est, tooEast arrière en Asie. Cet article décrit les étapes de hello sur la façon de tooreprotect.

> [!WARNING]
> Si vous avez [terminé la migration](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), les ressources, groupe ou supprimés de tooanother d’ordinateurs virtuels hello déplacé hello machine virtuelle Azure, vous ne pouvez pas la restauration automatique par la suite.

Une fois que reprotection se termine et réplication des machines virtuelles de hello protégé, vous pouvez lancer un basculement sur toobring de machines virtuelles hello les sauvegarder tooEast la région Asie.

Valider des commentaires ou des questions à fin hello de cet article ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Composants requis
1. machines virtuelles de Hello doit ont été validées.
2. site cible de Hello - dans ce cas la région Asie orientale Azure hello doit être disponible et de doit être en mesure de tooaccess/créer de nouvelles ressources dans cette région.

## <a name="steps-tooreprotect"></a>Étapes tooreprotect

Suivantes sont hello étapes tooreprotect un ordinateur virtuel à l’aide des valeurs par défaut hello.

1. Dans **coffre** > **éléments répliqués**, avec le bouton droit de machine virtuelle hello été basculée, puis sélectionnez **Reprotéger**. Vous pouvez également cliquer sur hello machine et sélectionnez **Reprotéger** hello boutons de commande.

![Cliquez avec le bouton droit sur tooreprotect](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. Dans le panneau de hello, notez cette direction hello de protection, **Asie du Sud-est tooEast**, est déjà sélectionné.

![Panneau Reprotéger](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. Hello de révision **ressource, réseau, stockage et la disponibilité de groupes** informations et cliquez sur OK. S’il existe des ressources marqués (nouveau), ils sont créés comme partie de hello Protégez de nouveau.

Cela sera un travail de déclencheur Protégez de nouveau travail qui sera tout d’abord amorcer le site cible de hello (SEA dans ce cas) avec les données les plus récentes hello et une fois que qui se termine, répliquez deltas hello avant le basculement vous sauvegarder tooSoutheast Asie.

### <a name="reprotect-customization"></a>Personnalisation de la reprotection
Si vous souhaitez toochoose Protégez-les hello extrait stockage compte ou hello réseau pendant, vous pouvez faire à l’aide de hello personnaliser option fournie sur le panneau de reprotection hello.

![Option Personnaliser](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

Vous pouvez personnaliser hello suivante des propriétés de la machine virtuelle il cible au cours de reprotection.

![Panneau Personnaliser](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|Propriété |Remarques  |
|---------|---------|
|Groupe de ressources cible     | Vous pouvez choisir le groupe de ressources toochange hello cible dans lequel th virtuels sera créé. Cadre hello de reprotection, la machine virtuelle cible hello vont être supprimée, par conséquent, vous pouvez choisir un nouveau groupe de ressources sous lequel vous pouvez créer hello machines virtuelles après basculement         |
|Réseau virtuel cible     | Réseau ne peut pas être modifié pendant la reprotection de hello. toochange hello réseau, le mappage réseau hello de restauration par progression.         |
|Stockage cible     | Vous pouvez modifier le compte de stockage hello toowhich hello virtuels sera créé après basculement.         |
|Stockage du cache     | Vous pouvez spécifier un compte de stockage de cache à utiliser lors de la réplication. Si vous accédez avec les valeurs par défaut hello, un nouveau compte de stockage de cache est créé, s’il n’existe pas.         |
|Groupe à haute disponibilité     |Si l’ordinateur virtuel de hello en Asie orientale fait partie d’un ensemble de disponibilité, vous pouvez choisir une ensemble de disponibilité pour la machine virtuelle cible hello Asie du Sud-est. Valeurs par défaut recherche à haute disponibilité SEA existant hello et essayez toouse il. Au cours de personnalisation, vous pouvez spécifier un nouveau groupe à haute disponibilité.         |


### <a name="what-happens-during-reprotect"></a>Que se passe-t-il durant la reprotection ?

Simplement comme après hello tout d’abord activer la protection, voici les artefacts hello qui sont créés si vous utilisez les valeurs par défaut hello.
1. Un compte de stockage de cache est créé dans la région Asie orientale hello.
2. Si le compte de stockage cible hello (hello d’origine compte de stockage de hello Asie du Sud-est VM) n’existe pas, un nouveau est créé. nom de Hello est un compte de stockage de l’ordinateur virtuel hello Asie orientale suivis du suffixe « asr ».
3. Si le jeu de cibles AV de hello n’existe pas, et détectent les valeurs par défaut hello qu’elle a besoin de toocreate une nouvelle AV définie, elle sera créée dans le cadre de hello Protégez de nouveau travail. Si vous avez personnalisé hello Protégez de nouveau, puis hello sélectionné AV jeu est utilisé.
4.

Hello Voici une liste de hello des étapes qui se produisent lorsque vous déclenchez un travail de reprotection. Il s’agit dans côté cible de hello hello cas ordinateur virtuel existe.

1. Hello requis artefacts sont créés dans le cadre de reprotection. S’ils existent déjà, ils sont réutilisés.
2. machine virtuelle de Hello cible côté (Asie du Sud-est) est tout d’abord mises hors tension, si elle est en cours d’exécution.
3. disque de machine virtuelle Hello cible côté est copié par Azure Site Recovery dans un conteneur comme un objet blob de valeur initiale.
4. la machine virtuelle côté Hello cible est supprimée.
5. objet blob de valeur initiale Hello est utilisé par tooreplicate de machine virtuelle hello actuel source côté (Asie orientale). Cela garantit que seuls les deltas sont répliqués.
6. Hello des modifications majeures entre le disque source hello et d’objet blob de valeur initiale de hello sont synchronisées. Cette opération peut prendre quelques toocomplete de temps.
7. Une fois hello Protégez de nouveau travail se termine, la réplication delta hello commence qui crée un point de récupération conformément à la stratégie de hello.

> [!NOTE]
> Vous ne pouvez pas protéger à un niveau plan de récupération. Vous pouvez uniquement reprotéger à un niveau par machine virtuelle.

Une fois hello Protégez-les réussisse, hello virtual machine entrent un état protégé.

## <a name="next-steps"></a>Étapes suivantes

Une fois la machine virtuelle de hello a entré un état protégé, vous pouvez lancer un basculement. Hello basculement sera arrêter la machine virtuelle de hello dans la région Asie orientale Azure et créer et démarrer hello Asie du Sud-est région virtual machine. Il est donc un bref temps d’arrêt pour l’application hello. Par conséquent, choisissez heure hello pour le basculement lorsque votre application peut tolérer un temps d’arrêt. Il est recommandé de commencer par tester basculement hello machine virtuelle toomake qu’il prochaine correctement, avant d’initier un basculement.

-   [Étapes tooinitiate test de basculement de la machine virtuelle de hello](site-recovery-test-failover-to-azure.md)

-   [Basculement de tooinitiate étapes de la machine virtuelle de hello](site-recovery-failover.md)
