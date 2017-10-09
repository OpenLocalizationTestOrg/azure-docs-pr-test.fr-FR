---
title: "la réplication pour les serveurs physiques réplication tooAzure avec Azure Site Recovery aaaEnable | Documents Microsoft"
description: "Résume les étapes hello vous devez tooenable réplication tooAzure pour les serveurs physiques, à l’aide du service d’Azure Site Recovery hello"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: dde4b1463023d2ccefa498f72bb51e57d60ac0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-physical-servers-tooazure"></a>Étape 10 : Activer la réplication pour les serveurs physiques tooAzure


Cet article décrit comment la réplication tooenable pour local Windows/Linux tooAzure serveurs physiques, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Avant de commencer

- Les serveurs doivent avoir hello [composant du service mobilité installé](physical-walkthrough-install-mobility.md).
- Si une machine virtuelle est préparée à l’installation push, serveur de processus hello installe automatiquement le service de mobilité hello lorsque vous activez la réplication.
- Lorsque vous activez un ordinateur pour la réplication, votre compte d’utilisateur Azure a besoin spécifique [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooensure vous êtes en mesure de toouse stockage Azure et créer des machines virtuelles Azure.
- Lorsque vous ajoutez ou modifiez les adresses IP des serveurs, il peut prendre too15 minutes ou plus pour effet de tootake de modifications et les tooappear dans le portail de hello.


## <a name="exclude-disks-from-replication"></a>Exclure les disques de la réplication

Par défaut, tous les disques d’une machine sont répliqués. Vous pouvez exclure des disques de la réplication. Par exemple, vous pouvez tooreplicate les disques avec les données temporaires ou des données a actualisé chaque fois qu’un ordinateur ou redémarrage de l’application (par exemple pagefile.sys ou tempdb de SQL Server). [En savoir plus](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a>Réplication des serveurs

1. Cliquez sur **Étape 2 : Répliquer l’application** > **Source**.
2. Dans **Source**, sélectionnez le serveur de configuration hello.
3. Dans **Type de machine**, sélectionnez **Machines physiques**.
4. Sélectionnez le serveur de processus hello. Si vous n’avez pas créé de tous les serveurs de processus supplémentaire ce sera le serveur de configuration hello. Cliquez ensuite sur **OK**.
5. Dans **cible**hello du groupe de ressources dans lequel vous souhaitez hello toocreate a échoué sur des machines virtuelles et sélectionnez l’abonnement de hello. Choisir le modèle de déploiement hello que toouse dans Azure (classique ou ressource de gestion), hello basculé de machines virtuelles.
6. Sélectionnez le compte de stockage Azure hello que toouse souhaité pour répliquer les données. Si vous ne souhaitez pas toouse un compte que vous avez déjà configuré, vous pouvez créer un nouveau.
7. Sélectionnez hello **réseau Azure** et **sous-réseau** toowhich machines virtuelles Azure se connecter après le basculement. Sélectionnez **configurer maintenant pour les machines sélectionnées** tooapply hello réseau paramètre tooall machines que vous sélectionnez pour la protection. Sélectionnez **configurer ultérieurement** tooselect hello réseau Azure par ordinateur. Si vous ne souhaitez pas toouse un réseau existant, vous pouvez créer un.

    ![Activer la réplication](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. Dans **machines physiques**, cliquez sur **+ machine physique** et entrez hello **nom** et **adresse IP**. Choisissez un système d’exploitation hello de l’ordinateur de hello souhaité tooreplicate. Il prend quelques minutes jusqu'à ce que les ordinateurs sont découverts et affichés dans la liste de hello.
9. Dans **propriétés** > **configurer les propriétés**, sélectionnez compte hello qui sera utilisé par hello processus serveur tooautomatically installer le service de mobilité hello sur l’ordinateur de hello.
10. Par défaut, tous les disques sont répliqués. Cliquez sur **tous les disques** et effacer tous les disques que vous ne souhaitez pas tooreplicate. Cliquez ensuite sur **OK**. Vous pouvez configurer des propriétés de machine virtuelle supplémentaires ultérieurement.

    ![Activer la réplication](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. Dans **les paramètres de réplication** > **configurer les paramètres de réplication**, vérifiez que hello correct de la stratégie de réplication est activée. Si vous modifiez une stratégie, les modifications seront appliquées tooreplicating machine et toonew machines.
12. Activer **la cohérence Multimachine virtuelle** si vous souhaitez toogather ordinateurs dans un groupe de réplication, spécifiez un nom pour le groupe de hello. Cliquez ensuite sur **OK**. Notez les points suivants :

    * Les machines des groupes de réplication sont répliquées ensemble et ont des points de récupération cohérents après incident et avec les applications lorsqu’elles basculent.
    * Nous vous recommandons de rassembler les serveurs physiques afin qu’ils reflètent vos charges de travail. L’activation de la cohérence multimachine virtuelle peuvent affecter les performances de la charge de travail et doit être utilisé uniquement si les ordinateurs hello même charge de travail et que vous avez besoin de cohérence.

13. Cliquez sur **Activer la réplication**. Vous pouvez suivre la progression de hello **activer la Protection** de la tâche dans **paramètres** > **travaux** > **tâches de récupération de Site**. Après avoir hello **finaliser la Protection** s’exécute la tâche machine de hello est prête pour le basculement.

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 11 : exécuter un test de basculement](physical-walkthrough-test-failover.md)
