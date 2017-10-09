---
title: les applications aaaReplicate (tooAzure Azure) | Documents Microsoft
description: "Cet article décrit comment tooset la réplication de virtual machines en cours d’exécution dans une région Azure trop d’une autre région dans Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a>Répliquer les machines virtuelles tooanother région Azure



>[!NOTE]
>
> La réplication Site Recovery pour les machines virtuelles Azure est actuellement en préversion.

Cet article décrit comment tooset la réplication de virtual machines en cours d’exécution dans une région Azure tooanother région Azure.

## <a name="prerequisites"></a>Composants requis

* article de Hello part du principe que vous connaissez déjà sur la récupération de Site et de coffre Recovery Services. Vous devez toohave une pre 'Coffre Recovery services' créé.

    >[!NOTE]
    >
    > Il est recommandé que vous créez hello 'Coffre Recovery services' dans hello emplacement où votre tooreplicate de machines virtuelles. Par exemple, si votre emplacement cible est la région « États-Unis du Centre », créez le coffre dans « États-Unis du Centre ».

* Si vous utilisez des règles de groupes de sécurité réseau (NSG) ou de la connectivité internet de pare-feu proxy toocontrol accès toooutbound sur hello machines virtuelles Azure, vérifiez que hello liste blanche vous requis URL ou les adresses IP. Consultez trop[document du Guide de mise en réseau](./site-recovery-azure-to-azure-networking-guidance.md) pour plus d’informations.

* Si vous avez un ExpressRoute ou une connexion VPN entre locaux et hello source d’emplacement dans Azure, suivez [considérations de récupération de Site pour local tooon Azure ExpressRoute / configuration VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.

* Votre compte d’utilisateur Azure doit toohave certaines [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’une machine virtuelle Azure.

* Votre abonnement Azure doit être activé toocreate VM dans l’emplacement cible de hello souhaité toouse comme région de récupération d’urgence. Vous pouvez contacter le support tooenable hello requis quota.

## <a name="enable-replication-from-azure-site-recovery-vault"></a>Activer la réplication à partir du coffre Azure Site Recovery
Dans cette illustration, nous va répliquer les machines virtuelles en cours d’exécution dans hello 'Asie orientale' emplacement Azure toohello ' Asie du Sud-est ' emplacement. étapes de Hello sont les suivantes :

 Cliquez sur **+ répliquer** dans la réplication de tooenable coffre hello pour les ordinateurs virtuels de hello.

1. **Source :** il fait référence à toohello point d’origine de machines de hello qui dans ce cas est **Azure**.

2. **Emplacement source :** il est hello région Azure où vous souhaitez tooprotect vos machines virtuelles. Dans cette illustration, emplacement de source de hello sera « East Asia »

3. **Modèle de déploiement :** il fait référence le modèle de déploiement Azure toohello de machines de sources hello. Vous pouvez sélectionner soit classique ou le Gestionnaire de ressources et les machines appartenant toohello particuliers du modèle sont répertoriés pour la protection à l’étape suivante de hello.

      >[!NOTE]
      >
      > Vous pouvez uniquement répliquer une machine virtuelle classique et la récupérer en tant que machine virtuelle classique. Vous ne pouvez pas la récupérer en tant que machine virtuelle Resource Manager.

4. **Groupe de ressources :** de toowhich de groupe de ressources hello vos machines virtuelles source appartient. Hello tous les ordinateurs virtuels sous le groupe de ressources sélectionné hello apparaît pour la protection à l’étape suivante de hello.

    ![Activer la réplication](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

Dans **virtuels > Sélectionner les machines virtuelles**, cliquez sur et sélectionnez chaque ordinateur que vous souhaitez tooreplicate. Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée. Puis cliquez sur OK.
    ![Activer la réplication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)


Dans la section Paramètres, vous pouvez configurer les propriétés du site cible.

1. **Emplacement cible :** emplacement hello où vos données d’ordinateur virtuel source seront répliquées. En fonction de votre emplacement d’ordinateurs sélectionnés, Site Recovery fournira que Hello de la liste des régions de la cible appropriée.

    > [!TIP]
    > Il est recommandé d’emplacement cible de tookeep même à compter de la récupération du coffre de services.

2. **Groupe de ressources cible :** il est toowhich de groupe de ressources hello toutes vos machines virtuelles répliquées appartiendra. Par défaut ASR créera un nouveau groupe de ressources dans la région de hello cible avec le nom de suffixe de « asr ». En cas de groupe de ressources créé par la fonctionnalité déjà existe, elle est réutilisée. Vous pouvez également choisir toocustomize comme indiqué dans la section hello ci-dessous.    
3. **Réseau virtuel de cible :** par défaut, la fonctionnalité créera un nouveau réseau virtuel dans la région de hello cible avec le nom de suffixe de « asr ». Cela sera mappé tooyour source réseau et sera utilisé pour toute protection futures.

    > [!NOTE]
    > [Consultez les détails de mise en réseau](site-recovery-network-mapping-azure-to-azure.md) tooknow plus sur le mappage réseau.

4. **Cibler des comptes de stockage :** par défaut, la fonctionnalité créera hello nouveau compte de stockage cible avec votre configuration de stockage d’ordinateur virtuel source. Dans le cas où le compte de stockage créé par ASR existe déjà, il est réutilisé.

5. **Comptes de stockage de cache :** ASR a besoin de compte de stockage supplémentaire appelée stockage du cache dans la région de la source hello. Tous les hello les modifications effectuées sur hello machines virtuelles source sont suivies et envoyés le compte de stockage toocache avant de répliquer ces emplacement cible de toohello.

6. **Haute disponibilité :** par défaut, la fonctionnalité créera un nouveau groupe à haute disponibilité dans la région de hello cible avec le nom de suffixe de « asr ». Dans le cas où le groupe à haute disponibilité créé par ASR existe déjà, il est réutilisé.

7.  **La stratégie de réplication :** il définit des paramètres pour la récupération point rétention l’historique et application instantané cohérent fréquence hello. Par défaut, ASR crée une stratégie de réplication avec des paramètres par défaut de « 24 heures » pour la rétention des points de récupération et « 60 minutes » pour la fréquence des captures instantanées de cohérence des applications.

    ![Activer la réplication](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a>Personnaliser les ressources cibles

Au cas où vous souhaiteriez toochange hello valeurs par défaut utilisées par la récupération automatique du système, vous pouvez modifier les paramètres de hello selon vos besoins.

1. **Personnaliser :** dessus toochange hello par défaut utilisées par la récupération automatique du système.

2. **Groupe de ressources cible :** vous pouvez sélectionner le groupe de ressources hello dans liste hello de tous les groupes de ressources hello existant dans l’emplacement cible de hello au sein de l’abonnement de hello.

3. **Réseau virtuel de cible :** vous trouverez la liste hello de tous les réseaux hello dans l’emplacement cible de hello.

4. **Haute disponibilité :** vous pouvez uniquement ajouter disponibilité jeux de paramètres toohello machines virtuelles qui font partie de la disponibilité dans la zone source.

5. **Comptes de stockage cibles :**

![Activer la réplication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Cliquez sur **Créer la ressource cible** et Activer la réplication.


Une fois que les ordinateurs virtuels sont protégés, vous pouvez vérifier état hello d’intégrité des machines virtuelles sous **éléments répliqués**

>[!NOTE]
>Au cours de hello moment de la réplication initiale il pourrait possible qu’état prend toorefresh de temps et que vous ne voyez pas progression pendant un certain temps. Vous pouvez cliquer le bouton d’actualisation hello haut hello d’état le plus récent hello panneau tooget hello.
>

![Activer la réplication](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a>Étapes suivantes
- [En savoir plus](site-recovery-test-failover-to-azure.md) sur l’exécution d’un test de basculement.
- [En savoir plus](site-recovery-failover.md) sur différents types de basculement et comment toorun les.
- En savoir plus sur [à l’aide de plans de récupération](site-recovery-create-recovery-plans.md) tooreduce RTO.
- En savoir plus sur la [reprotection des machines virtuelles Azure](site-recovery-how-to-reprotect.md) après le basculement.
