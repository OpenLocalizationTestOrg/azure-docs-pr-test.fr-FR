---
title: "Répliquer des applications (VMware tooAzure) | Documents Microsoft"
description: "Cet article décrit comment tooset la réplication de virtual machines en cours d’exécution sur VMware dans Azure."
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
ms.date: 06/05/2017
ms.author: asgang
ms.openlocfilehash: b07aabdacec521c7bd89e50f6a1427a774ff0287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-applications-running-on-vmware-vms-tooazure"></a>Répliquer des applications en cours d’exécution sur les ordinateurs virtuels VMware tooAzure



Cet article décrit comment tooset la réplication de virtual machines en cours d’exécution sur VMware dans Azure.
## <a name="prerequisites"></a>Composants requis

Hello article suppose que vous avez déjà

1.  [Configurer un environnement source local](site-recovery-set-up-vmware-to-azure.md)
2.  [Configurer un environnement cible dans Azure](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>Activer la réplication
#### <a name="before-you-start"></a>Avant de commencer
Lors de la réplication de machines virtuelles VMware, prenez note des points suivants :

* Votre compte d’utilisateur Azure doit toohave certaines [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’un nouveau tooAzure d’ordinateur virtuel.
* Les machines virtuelles VMware sont découvertes toutes les 15 minutes, Il peut prendre 15 minutes ou plus pour les tooappear dans portail hello après la découverte. De même, la découverte peut prendre 15 minutes ou plus lorsque vous ajoutez un serveur vCenter ou un hôte vSphere.
* Modifications de l’environnement sur l’ordinateur virtuel de hello (par exemple, l’installation des outils VMware) peuvent prendre 15 minutes ou plus toobe mis à jour dans le portail de hello.
* Vous pouvez vérifier hello découverts dernière heure pour les ordinateurs virtuels VMware Bonjour **dernier Contact à** champ hello vCenter serveur/hôte vSphere, sur hello **serveurs de Configuration** panneau.
* ordinateurs tooadd pour la réplication sans attendre la détection planifiée de hello, mettez en surbrillance le serveur de configuration hello (ne cliquez pas dessus), puis cliquez sur hello **Actualiser** bouton.
* Lorsque vous activez la réplication, si l’ordinateur de hello est préparée, serveur de processus hello installe automatiquement le service de mobilité hello sur celui-ci.


**À présent, activez la réplication comme suit**:

1. Cliquez sur **Étape 2 : Répliquer l’application** > **Source**. Une fois que vous avez activé la réplication pour hello première fois, cliquez sur **+ répliquer** dans la réplication de tooenable hello coffre pour des ordinateurs supplémentaires.
2. Bonjour **Source** panneau > **Source**, sélectionnez le serveur de configuration hello.
3. Dans la zone **Type de machine**, sélectionnez **Machines virtuelles** ou **Machines physiques**.
4. Dans **vCenter/vSphere hyperviseur**, sélectionnez le serveur vCenter hello qui gère l’ordinateur hôte de vSphere hello ou sélectionner l’ordinateur hôte hello. Ce paramètre n’est pas utile si vous répliquez des machines physiques.
5. Sélectionnez le serveur de processus hello. Si vous n’avez pas créé de tous les serveurs de processus supplémentaire ce sera le nom hello hello du serveur de configuration. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. Dans **cible** sélectionnez abonnement de hello et le groupe de ressources hello où vous souhaitez hello toocreate machines virtuelles ayant basculé. Choisir un modèle de déploiement hello souhaitées toouse dans Azure (classique ou une ressource de gestion) pour hello machines virtuelles ayant basculé.
7. Sélectionnez le compte de stockage Azure hello que toouse souhaité pour répliquer les données. Notez les points suivants :

   * Vous pouvez sélectionner un compte Standard Storage ou Premium Storage. Si vous sélectionnez un compte premium, vous devez toospecify un compte de stockage standard supplémentaire pour les journaux de réplication en cours. Comptes doivent être Bonjour Services de récupération de la même région que hello coffre.
   * Si vous voulez toouse un compte de stockage différentes que celles que vous avez, vous pouvez créer un*lien d’espace réservé pour la création de compte de stockage à l’aide de la ressource gestionnaire qui est abordé dans la mise en route*. toocreate un compte de stockage à l’aide du Gestionnaire de ressources, cliquez sur **nouvel**. Si vous voulez toocreate un compte de stockage à l’aide du modèle classique de hello, c’est [Bonjour Azure portal](../storage/common/storage-create-storage-account.md).

8. Sélectionnez hello toowhich réseau et le sous-réseau Azure machines virtuelles Azure se connecte lorsqu’ils êtes lancés après le basculement. réseau de Hello doit être Bonjour Services de récupération de la même région que hello coffre. Sélectionnez **configurer maintenant pour les machines sélectionnées**, tooapply hello réseau paramètre tooall machines que vous sélectionnez pour la protection. Sélectionnez **configurer ultérieurement** tooselect hello réseau Azure par ordinateur. Si vous n’avez pas un réseau, vous devez trop[créer un](#set-up-an-azure-network). toocreate un réseau à l’aide du Gestionnaire de ressources, cliquez sur **nouvel**. Si vous voulez toocreate un réseau en utilisant le modèle classique de hello, cela [Bonjour Azure portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Sélectionnez un sous-réseau, le cas échéant. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. Dans **virtuels** > **sélectionner des machines virtuelles**, cliquez sur et sélectionnez chaque ordinateur que vous souhaitez tooreplicate. Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. Dans **propriétés** > **configurer les propriétés**, sélectionnez compte hello qui sera utilisé par hello processus serveur tooautomatically installer le service de mobilité hello sur l’ordinateur de hello.  
11. Par défaut, tous les disques sont répliqués. disques tooexclude de la réplication, cliquez sur **tous les disques** et effacer tous les disques que vous ne souhaitez pas tooreplicate.  Cliquez ensuite sur **OK**. Vous pouvez opter pour une définition ultérieure des propriétés. [Apprenez-en davantage](site-recovery-exclude-disk.md) sur l’exclusion de disques.

    ![Activer la réplication](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. Dans **les paramètres de réplication** > **configurer les paramètres de réplication**, vérifiez que hello correct de la stratégie de réplication est activée. Vous pouvez modifier les paramètres de la stratégie de réplication dans **Paramètres** > **Stratégies de réplication** > Nom de la stratégie > **Modifier les paramètres**. Les modifications vous appliquez la stratégie de tooa seront appliqué tooreplicating et nouveaux ordinateurs.
13. Activer **la cohérence Multimachine virtuelle** si vous souhaitez toogather ordinateurs dans un groupe de réplication, spécifiez un nom pour le groupe de hello. Cliquez ensuite sur **OK**. Notez les points suivants :

    * Toutes les machines d’un groupe de réplication sont répliquées ensemble et elles ont des points de récupération cohérents après incident et avec les applications lorsqu’elles basculent.
    * Nous vous recommandons de rassembler les machines virtuelles et les serveurs physiques afin qu’ils reflètent vos charges de travail. L’activation de la cohérence multimachine virtuelle peuvent affecter les performances de la charge de travail et doit être utilisé uniquement si les ordinateurs hello même charge de travail et que vous avez besoin de cohérence.

    ![Activer la réplication](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Cliquez sur **Activer la réplication**. Vous pouvez suivre la progression de hello **activer la Protection** de la tâche dans **paramètres** > **travaux** > **tâches de récupération de Site**. Après avoir hello **finaliser la Protection** s’exécute la tâche machine de hello est prête pour le basculement.

> [!NOTE]
> Si l’ordinateur de hello est préparé pour hello d’installation push mobilité de composant de service sera installé à la protection est activée. Après avoir hello composant est installé sur échoue et l’ordinateur hello qu'une tâche de protection démarre. Après l’échec de hello, vous devez toomanually redémarrer chaque machine. Après la protection de hello hello redémarrage du travail commence à nouveau et la réplication initiale se produit.
>
>

## <a name="view-and-manage-vm-properties"></a>Afficher et gérer les propriétés des machines virtuelles

Nous vous conseillons de vérifier les propriétés de hello d’ordinateur de source de hello. N’oubliez pas de ce nom de machine virtuelle Azure hello doit respecter les [spécifications de la machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Cliquez sur **paramètres** > **éléments répliqués** > et sélectionnez hello machine. Hello **Essentials** panneau affiche des informations sur les paramètres des ordinateurs et l’état.
2. Dans **propriétés**, vous pouvez afficher la réplication et les informations de basculement pour hello machine virtuelle.
3. Dans **de calcul et réseau** > **propriétés de calcul**, vous pouvez spécifier la taille de nom et la cible de la machine virtuelle Azure hello. Modifiez toocomply de nom hello aux exigences d’Azure si vous avez besoin.
    ![Activer la réplication](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  Vous pouvez sélectionner un [groupe de ressources](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) dont l’ordinateur fera partie lors du post-basculement. Vous pouvez modifier ce paramètre avant le basculement. Après basculement, si vous migrez hello machine tooa autre groupe de ressources, puis les paramètres de protection d’un ordinateur seront arrête.
5. Vous pouvez sélectionner un [à haute disponibilité](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) basculer si votre ordinateur nécessaire toobe faire partie d’une publication. Lorsque vous sélectionnez le groupe à haute disponibilité, prenez note de ce qui suit :

    * Groupe de ressources est répertorié uniquement toohello appartenant spécifié à haute disponibilité  
    * Les ordinateurs avec différents réseaux virtuels ne peuvent pas faire partie du même groupe à haute disponibilité.
    * Seules les machines virtuelles de même taille peuvent faire partie du même groupe à haute disponibilité.
5. Vous pouvez également afficher et ajouter des informations sur le réseau cible de hello, du sous-réseau et adresse IP qui sera assigné toohello machine virtuelle Azure.
6. Dans **disques**, vous pouvez voir le système d’exploitation de hello et disques de données de hello des ordinateurs virtuels qui seront répliqués.

### <a name="network-adapters-and-ip-addressing"></a>Cartes réseau et adressage IP 

- Vous pouvez définir l’adresse IP de hello cible. Si vous ne fournissez une adresse, hello a échoué sur l’ordinateur utilise DHCP. Si vous définissez une adresse qui n’est pas disponible lors du basculement, hello basculement ne fonctionne pas. Hello même adresse IP peut servir pour le test de basculement si l’adresse de hello est disponible dans le réseau de basculement de test hello.
- nombre de Hello de cartes réseau est dicté par taille hello que vous spécifiez pour la machine virtuelle de cible hello, comme suit :
    - Si le nombre de hello de cartes réseau sur l’ordinateur source de hello est inférieur ou égal toohello le nombre de cartes autorisé pour la taille de la machine cible hello, puis cible de hello aura hello même nombre de cartes en tant que source de hello.
    - Si nombre hello de cartes pour l’ordinateur virtuel de hello source dépasse nombre hello autorisé pour la taille cible hello puis la taille maximale de la cible hello est utilisé.
    - Par exemple, si un ordinateur source possède deux cartes réseau et prend en charge la taille de la machine cible hello quatre, l’ordinateur cible hello aura deux cartes. Si hello source ordinateur possède deux cartes, mais hello taille cible pris en charge uniquement en charge l’un de l’ordinateur cible hello aura qu’un seul adaptateur.
    - Si l’ordinateur virtuel de hello possède plusieurs cartes réseau qu’ils seront connectent tous toohello même réseau.
    - Si l’ordinateur virtuel de hello possède plusieurs cartes réseau, hello celui affiché dans la liste de hello devient hello *par défaut* carte réseau Bonjour machine virtuelle Azure.
   



## <a name="common-issues"></a>Problèmes courants

* La taille de chaque disque doit être inférieure à 1 To.
* disque de Hello du système d’exploitation doit être un disque de base et les disques dynamiques pas
* Pour la génération 2/UEFI activé des machines virtuelles, famille de système d’exploitation hello doit être Windows et le disque de démarrage doit être inférieur à 300 Go

## <a name="next-steps"></a>Étapes suivantes

Une fois la protection de hello est terminée, vous pouvez essayer de [basculer](site-recovery-failover.md) toocheck si votre application s’affiche dans Azure ou non.

Au cas où vous souhaiteriez toodisable protection, vérifiez comment trop[nettoyer les paramètres d’inscription et de protection](site-recovery-manage-registration-and-protection.md)
