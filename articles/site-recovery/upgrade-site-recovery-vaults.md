---
title: "aaaUpgrade un coffre de Services de récupération Azure Site Recovery coffre tooan"
description: "Découvrez comment tooupgrade un coffre Azure Site Recovery Services de récupération tooa coffre"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a>Mise à niveau d’un coffre de Services de récupération basée sur le Gestionnaire de ressources Azure Site Recovery coffre tooan

Cet article décrit comment les coffres de coffres de Service de récupération basée sur le Gestionnaire de ressources tooAzure sans aucun impact sur la réplication en cours tooupgrade Azure Site Recovery. Pour plus d’informations sur les fonctionnalités et les avantages d’Azure Resource Manager, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="introduction"></a>Introduction
Un coffre Recovery Services est une ressource Azure Resource Manager pour la gestion de sauvegarde et récupération d’urgence en mode natif dans le cloud de hello. Il est un coffre unifié que vous pouvez utiliser dans le nouveau portail Azure hello et il remplace les sauvegarde classique hello et les coffres de récupération de Site.

Les coffres Recovery Services offrent tout un ensemble de fonctionnalités, notamment :

* Prise en charge d’Azure Resource Manager : vous pouvez protéger et basculer vos machines virtuelles et ordinateurs physiques dans une pile Azure Resource Manager.

* Exclure le disque : Si vous avez des fichiers temporaires ou des données d’évolution élevé que vous ne souhaitez pas toouse votre bande passante pour, vous pouvez exclure des volumes de réplication. Cette fonctionnalité a été activée actuellement en *VMware tooAzure* et *Hyper-V tooAzure* et est étendues scénarios tooother également.

* Prise en charge pour le stockage localement redondant et premium : vous pouvez désormais protéger des serveurs dans un stockage premium comptes qui permettent aux clients tooprotect des applications avec une version ultérieure d’entrée/sortient d’opérations par seconde (IOPS). Cette fonctionnalité est actuellement activée dans *VMware tooAzure*.

* Rationalisé expérience de mise en route : expérience de mise en route de hello améliorée a été conçu configuration de la récupération d’urgence toomake facile.

* Sauvegarde et gestion de récupération de Site à partir de hello même coffre : vous pouvez désormais protéger les serveurs de récupération d’urgence ou effectuer la sauvegarde à partir de hello même coffre, ce qui peut réduire votre charge considérablement.

Pour plus d’informations sur l’expérience de hello mis à niveau et de fonctionnalités, consultez hello [blog de stockage, la sauvegarde et récupération](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).

## <a name="salient-features"></a>Principales fonctionnalités

* Aucun impact sur la réplication en cours : les réplications en cours se poursuivent sans interruption pendant et après la mise à niveau.

* Aucun coût supplémentaire : à disposition, un ensemble complet de fonctionnalités mises à jour sans coût supplémentaire.

* Aucune perte de données : étant donné que ce processus est une mise à niveau et pas une migration, les paramètres et les points de récupération de réplication existants restent intacts pendant et après la mise à niveau hello.


## <a name="what-happens-during-hello-vault-upgrade"></a>Que se passe-t-il au cours de la mise à niveau du coffre hello ?

Au cours de la mise à niveau de hello, Impossible d’effectuer les opérations telles que l’inscription d’un nouveau serveur ou l’activation de la réplication pour un ordinateur virtuel (VM). Les opérations qui impliquent la lecture des données à partir d’ou de l’écriture de données toohello coffre, telles que la réplication en cours de l’archivage de toohello les éléments protégés, continuent sans interruption.

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a>Modifications tooautomation et outils après la mise à niveau hello
Comme le type d’archivage hello mise à niveau à partir du modèle de déploiement du modèle toohello Gestionnaire de ressources hello déploiement classique, mettre à jour automation existante de hello ou tooensure outils qu’il remplisse toujours toowork après mise à niveau hello.

### <a name="prepare-your-environment-for-hello-upgrade"></a>Préparer votre environnement pour la mise à niveau hello

* [Installer PowerShell ou de mettre à niveau tooversion 5 ou version ultérieure](https://www.microsoft.com/download/details.aspx?id=50395)
* [Installer la version la plus récente d’Azure PowerShell MSI hello](https://github.com/Azure/azure-powershell/releases)
* [Télécharger le script mis à niveau du coffre Recovery Services hello](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a>Composants requis
tooAzure basée sur le Gestionnaire de ressources de Service de récupération coffres les coffres de tooupgrade à partir de la récupération de Site, vous devez disposer des hello suivant les exigences :

* Version minimale de l’agent : hello la version du fournisseur Azure Site Recovery installé sur votre serveur doit être 5.1.1700.0 ou version ultérieure.

* Configuration prise en charge : vous ne pouvez pas configurer votre coffre avec le réseau de zone de stockage (SAN) ou des groupes de disponibilité AlwaysOn SQL Server. Toutes les autres configurations sont prises en charge.

    >[!NOTE]
    >Après la mise à niveau de hello, vous pouvez gérer le mappage de stockage uniquement via PowerShell.

* Scénario de déploiement pris en charge : votre coffre ne doivent pas être hello *VMware tooAzure* modèle de déploiement hérité. Avant de continuer, commencez par déplacer modèle améliorée du déploiement de toohello.

* Aucune tâche active initiée par l’utilisateur qui impliquent management ne plan operations :, car le plan de gestion des accès toohello est limitée au cours de la mise à niveau, effectuez toutes les actions votre plan de gestion avant de déclencher la mise à niveau de hello. Ce processus n’inclut pas la réplication en cours.

## <a name="frequently-asked-questions"></a>Forum Aux Questions

**Cette mise à niveau affecte-t-elle la réplication en cours ?**

Non. La réplication en cours se poursuit sans interruption pendant et après la mise à niveau hello.

**Que passe-t-il toonetwork des paramètres tels que les paramètres IP et VPN de site à site ?**

mise à niveau Hello n’affecte pas les paramètres de réseau hello. Toutes les connexions depuis Azure vers un emplacement local demeurent intactes.

**Que passe-t-il toomy coffres si vous ne prévoyez pas tooupgrade Bonjour futur proche ?**

Prise en charge pour le coffre Site Recovery dans l’ancien portail de Azure hello sera déconseillée à partir de septembre 2017. Nous vous recommandons vivement que vous utilisez des hello mise à niveau de fonctionnalité toomove toohello nouveau portail.

**Quelles sont les implications de ce plan de migration pour mes outils existants ?**  

Mise à jour de votre modèle de déploiement du Gestionnaire de ressources de toohello outils est une des modifications les plus importantes hello que vous devez prendre en compte pour dans vos plans de mise à niveau. archivages de Recovery Services Hello sont basés sur le modèle de déploiement du Gestionnaire de ressources hello. 

**La durée pendant laquelle dernière hello temps mort du plan de gestion ?**

mise à niveau Hello prend généralement environ 15 minutes de too30, et il peut s’écouler jusqu'à tooa maximale d’une heure.

**Puis-je restaurer après la mise à niveau ?**

Non. La restauration n’est pas prise en charge une fois que les ressources hello ont été mis à niveau avec succès.

**Puis-je valider des mon abonnement ou les ressources toosee si elles peuvent être mis à niveau ?**

Oui. Dans hello plateforme prise en charge option mise à niveau, hello première étape de mise à niveau hello est toovalidate que les ressources hello compatibles avec une mise à niveau. Si hello validation échoue, vous recevez des messages d’erreur appropriés ou des avertissements.

**Comment signaler un problème avec la mise à niveau hello ?**

Si vous rencontrez les échecs au cours de la mise à niveau hello, notez les ID d’opération hello est répertorié dans l’erreur de hello. Support technique de Microsoft proactive fonctionne sur la résolution de problème de hello. Vous pouvez également contacter l’équipe de Support hello avec votre ID d’abonnement, le nom de l’archivage et l’ID d’opération. Prise en charge fonctionnera problème de hello tooresolve aussi rapidement que possible. Ne pas réessayer les opération hello sauf si vous êtes toodo explicitement demandé c’est le cas par Microsoft.

## <a name="run-hello-script"></a>Exécutez le script de hello

Dans PowerShell, exécutez hello de commande suivante :

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* SubscriptionID : ID d’abonnement hello qui est associé à l’archivage hello que vous mettez à niveau.

* Nom du coffre : nom de hello de coffre hello que vous mettez à niveau.

* Emplacement : emplacement de hello de coffre hello que vous mettez à niveau.

* ResourceType : HyperVRecoveryManagerVault pour les coffres Site Recovery.

* TargetResourceGroupName : mise à niveau de groupe de ressources hello dans lequel vous souhaitez hello toobe coffre placé. TargetResourceGroupName peut être un groupe de ressources existant dans Azure Resource Manager ou un nouveau groupe. Si hello TargetResourceGroupName fourni n’existe pas, il est créé dans le cadre de la mise à niveau hello Bonjour même emplacement que le coffre de hello. Pour plus d’informations, voir section « Groupes de ressources » hello [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).

    >[!NOTE]
    >Nom de groupe de ressources est contraintes toocertain de sujet. tooprevent coffre mise à niveau de défaillance, être vraiment tooobserve hello convention d’affectation de noms avec soin.
    >
    >Par exemple :
    >
    >.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc

Vous pouvez également exécuter hello script suivant. Entrez les valeurs de hello pour les paramètres hello requis.

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. Hello script PowerShell vous invite à entrer vous tooenter vos informations d’identification. Entrez-les à deux reprises, une fois pour le compte de modèle de déploiement classique de hello et une fois pour hello compte de gestionnaire de ressources Azure.

2. Une fois que vous avez entré vos informations d’identification, script de hello exécute un toodetermine à cocher si votre hello répond à du programme d’installation infrastructure mentionné précédemment configuration requise.

3. Une fois les conditions préalables de hello ont été vérifiés et confirmés, vous êtes tooproceed demandée avec mise à niveau du coffre hello. processus de mise à niveau Hello démarre la mise à niveau votre archivage. mise à niveau entière de Hello peut prendre 15 toocomplete de minutes too30.

4. Une fois la mise à niveau hello est terminée avec succès, vous pouvez accéder à hello de coffre mis à niveau dans le nouveau portail de Azure hello.

## <a name="post-upgrade-vault-management"></a>Gestion du coffre après la mise à niveau

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a>Répliquer à l’aide d’Azure Site Recovery Bonjour de coffre Recovery Services

* Vous pouvez désormais protéger vos machines virtuelles Azure à partir d’une région tooanother. Pour plus d’informations, consultez [Répliquer des machines virtuelles Azure entre des régions avec Azure Site Recovery](site-recovery-azure-to-azure.md).

* Pour plus d’informations sur la réplication des ordinateurs virtuels VMware tooAzure, consultez [tooAzure de répliquer des machines virtuelles VMware avec Site Recovery](vmware-walkthrough-overview.md).

* Pour plus d’informations sur la réplication des ordinateurs virtuels Hyper-V (sans VMM) tooAzure, consultez [Hyper-V répliquer les machines virtuelles (sans VMM) tooAzure](hyper-v-site-walkthrough-overview.md).

* Pour plus d’informations sur la réplication des ordinateurs virtuels Hyper-V (avec VMM) tooAzure, consultez [machines virtuelles de réplication Hyper-V dans VMM tooAzure de nuages à l’aide de la récupération de Site dans hello Azure portal](vmm-to-azure-walkthrough-overview.md).

* Pour plus d’informations sur la réplication de site secondaire de tooa Hyper-VMs (avec VMM), consultez [machines virtuelles de réplication Hyper-V dans VMM clouds tooa secondaire VMM site à l’aide de hello Azure portal](site-recovery-vmm-to-vmm.md).

* Pour plus d’informations sur la réplication de site secondaire de tooa les ordinateurs virtuels VMware, consultez [Replicate locaux des ordinateurs virtuels VMware ou serveurs physiques tooa secondaire dans le portail Azure classic de hello](site-recovery-vmware-to-vmware.md).

### <a name="view-your-replicated-items"></a>Afficher vos éléments répliqués

Hello image suivante montre hello Recovery Services page coffre du tableau de bord qui affiche les entités clés pour le coffre hello. tooview une liste des entités protégées dans le coffre de hello, sélectionnez **Site Recovery** > **éléments répliqués**.


![Éléments répliqués](./media/upgrade-site-recovery-vaults/replicateditems.png)

Hello image suivante présente hello de flux de travail pour afficher les éléments répliqués hello **basculement** commande pour initialiser un basculement.

![Éléments répliqués](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a>Afficher vos paramètres de réplication

Dans le coffre Site Recovery hello, chaque groupe de protection est configuré avec une fréquence de copie, délai de rétention de point de récupération, fréquence des instantanés cohérents d’application et autres paramètres de réplication. Dans le coffre Recovery Services hello, ces paramètres sont configurés en tant qu’une stratégie de réplication. nom Hello de stratégie de hello est nom hello du groupe de protection hello ou hello *primarycloud_Policy*.

Pour plus d’informations sur la stratégie de réplication, consultez [gérer la stratégie de réplication pour VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).
