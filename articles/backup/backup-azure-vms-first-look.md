---
title: "Découverte : Sauvegarder des machines virtuelles Azure avec un coffre de sauvegarde | Microsoft Docs"
description: "Utilisez tooback portail classique de hello de coffre de sauvegarde tooa de machines virtuelles Azure. Ce didacticiel explique toutes les phases, y compris la création du coffre de sauvegarde hello, l’inscription d’ordinateurs virtuels de hello, création de stratégie de sauvegarde et en cours d’exécution du travail de sauvegarde initiale hello."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a>Découverte : sauvegarde des machines virtuelles Azure
> [!div class="op_single_selector"]
> * [Protéger les machines virtuelles avec un coffre Recovery Services](backup-azure-vms-first-look-arm.md)
> * [Protéger les machines virtuelles Azure avec un coffre de sauvegarde](backup-azure-vms-first-look.md)
>
>

Ce didacticiel vous guide tout au long des étapes de hello pour la sauvegarde d’un machine virtuelle Azure (VM) tooa coffre de sauvegarde Azure. Cet article décrit le modèle classique de hello ou modèle de déploiement de Service Manager, pour la sauvegarde des machines virtuelles. Hello étapes suivantes s’appliquent uniquement les coffres tooBackup créés dans le portail classique de hello. Microsoft recommande d’utiliser le modèle de gestionnaire de ressources hello pour les nouveaux déploiements.

Si vous êtes intéressé par sauvegarde un coffre de Services de récupération tooa machine virtuelle qui appartient tooa groupe de ressources, consultez [tout d’abord rechercher : protéger les machines virtuelles avec un coffre recovery services](backup-azure-vms-first-look-arm.md).

toosuccessfully effectuer des opérations suivantes de hello didacticiel, ces conditions doivent être réunies :

* Vous avez créé une machine virtuelle dans votre abonnement Azure.
* Hello machine virtuelle a des adresses IP publiques de connectivité tooAzure. Pour plus d’informations, consultez la rubrique [Connectivité réseau](backup-azure-vms-prepare.md#network-connectivity).


> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md). Ce didacticiel est pour une utilisation avec les ordinateurs virtuels créés dans le portail classique de hello.
>
>

## <a name="create-a-backup-vault"></a>Créer un coffre de sauvegarde
Un coffre de sauvegarde est une entité qui stocke toutes les sauvegardes de hello et les points de récupération qui ont été créées au fil du temps. coffre de sauvegarde Hello contient également des stratégies de sauvegarde hello sont appliqués toohello des ordinateurs virtuels en cours de sauvegarde.

> [!IMPORTANT]
> À partir de mars 2017, vous pouvez utiliser n’est plus les coffres de sauvegarde hello toocreate portail classique.
> Vous pouvez mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell. **D’ici au 1er novembre 2017** :
>- Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>

## <a name="discover-and-register-azure-virtual-machines"></a>Découverte et inscription des machines virtuelles Azure
Avant d’inscrire hello machine virtuelle dans un coffre, exécutez tooidentify de processus de découverte hello de nouvelles machines virtuelles. Cela retourne une liste d’ordinateurs virtuels dans l’abonnement hello, ainsi que des informations supplémentaires telles que le nom du service cloud hello et la région de hello.

1. Connectez-vous à toohello [portail Azure Classic](http://manage.windowsazure.com/)
2. Bonjour portail Azure classic, cliquez sur **Services de récupération** liste de hello tooopen des archivages de Recovery Services.
    ![Sélectionner la charge de travail](./media/backup-azure-vms-first-look/recovery-services-icon.png)
3. À partir de la liste de hello des coffres, sélectionnez tooback de coffre hello d’un ordinateur virtuel.

    Lorsque vous sélectionnez votre archivage, il s’ouvre dans hello **Quick Start** page
4. Dans le menu de coffre hello, cliquez sur **éléments inscrits**.

    ![Sélectionner la charge de travail](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. À partir de hello **Type** menu, sélectionnez **Machine virtuelle Azure**.

    ![Sélectionner la charge de travail](./media/backup-azure-vms/discovery-select-workload.png)
6. Cliquez sur **DISCOVER** bas hello de page de hello.
    ![Bouton découverte](./media/backup-azure-vms/discover-button-only.png)

    processus de découverte Hello peut prendre quelques minutes hello virtuels sont en cours sous forme de tableau. Il existe une notification bas hello écran hello qui vous permet de savoir que hello est en cours.

    ![Détection des machines virtuelles](./media/backup-azure-vms/discovering-vms.png)

    modifications de la notification Hello lorsque hello est terminée.

    ![Détection exécutée](./media/backup-azure-vms-first-look/discovery-complete.png)
7. Cliquez sur **inscrire** bas hello de page de hello.
    ![Bouton Inscription](./media/backup-azure-vms-first-look/register-icon.png)
8. Bonjour **enregistrer les éléments** menu contextuel, sélectionnez hello ordinateurs virtuels que vous souhaitez tooregister.

   > [!TIP]
   > Plusieurs machines virtuelles peuvent être inscrites en même temps.
   >
   >

    Un travail est créé pour chaque machine virtuelle sélectionnée.
9. Cliquez sur **afficher le travail** dans hello notification toogo toohello **travaux** page.

    ![Inscrire du travail](./media/backup-azure-vms/register-create-job.png)

    machine virtuelle de Hello apparaît également dans la liste hello des éléments inscrits, ainsi que de l’état hello de l’opération d’inscription de hello.

    ![État de l’inscription 1](./media/backup-azure-vms/register-status01.png)

    Lors de la fin de l’opération de hello, hello devient tooreflect hello *inscrit* état.

    ![État de l’inscription 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Installer hello Agent de machine virtuelle sur l’ordinateur virtuel de hello
Hello Agent de machine virtuelle Azure doit être installé sur la machine virtuelle Azure à hello sauvegarde extension toowork de hello. Si votre machine virtuelle a été créé à partir de la galerie Azure de hello, hello Agent de machine virtuelle est déjà présent sur hello machine virtuelle ; Vous pouvez ignorer trop[protéger vos machines virtuelles](backup-azure-vms-first-look.md#create-the-backup-policy).

Si votre machine virtuelle migré à partir d’un centre de données local, hello VM probablement n’a pas hello installé d’Agent de machine virtuelle. Vous devez installer hello Agent de machine virtuelle sur l’ordinateur virtuel de hello avant hello de tooprotect continuer machine virtuelle. Pour obtenir des instructions détaillées sur l’installation de hello Agent de machine virtuelle, consultez hello [section Agent de machine virtuelle de l’article de machines virtuelles de sauvegarde hello](backup-azure-vms-prepare.md#vm-agent).

## <a name="create-hello-backup-policy"></a>Créer une stratégie de sauvegarde hello
Avant de déclencher de travail de sauvegarde initiale hello, planifier hello quand les instantanés de sauvegarde sont créés. Hello planifier des instantanés de sauvegarde sont effectuées et hello durée ces instantanés sont conservés, est la stratégie de sauvegarde hello. informations de rétention Hello sont basées sur le jeu de sauvegarde rotation grand-père-father-son.

1. Accédez de coffre de sauvegarde toohello sous **Services de récupération** dans hello portail Azure Classic, puis cliquez sur **éléments inscrits**.
2. Sélectionnez **Machine virtuelle Azure** à partir du menu déroulant de hello.

    ![Sélectionner la charge de travail dans le portail](./media/backup-azure-vms/select-workload.png)
3. Cliquez sur **protéger** bas hello de page de hello.
    ![Cliquer sur Protéger](./media/backup-azure-vms-first-look/protect-icon.png)

    Hello **Assistant protéger** apparaît et répertorie *uniquement* les ordinateurs virtuels qui sont enregistrés et non protégés.

    ![Configurer les paramètres de protection pendant la mise à jour](./media/backup-azure-vms/protect-at-scale.png)
4. Sélectionnez hello ordinateurs virtuels que vous souhaitez tooprotect.

    S’il existe deux ou plusieurs machines virtuelles avec hello même nom, utilisez hello toodistinguish Service Cloud entre des machines virtuelles de hello.
5. Sur hello **configurer la protection** menu, sélectionnez une stratégie existante ou créer une nouvelle tooprotect de stratégie hello virtuels que vous avez identifié.

    Des coffres de sauvegarde ont une stratégie par défaut associée au coffre de hello. Cette stratégie est un plan quotidien chaque soir d’instantané et instantané quotidien de hello est conservé pendant 30 jours. Vous pouvez associer plusieurs machines virtuelles à chaque stratégie de sauvegarde. Toutefois, hello virtual machine ne peut être associé à une stratégie à une heure.

    ![Protéger grâce à la nouvelle stratégie](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Une stratégie de sauvegarde inclut un jeu de rétention pour les sauvegardes planifiée de hello. Si vous sélectionnez une stratégie de sauvegarde existante, vous serez options de rétention hello toomodify impossible à l’étape suivante de hello.
   >
   >
6. Sur **de rétention** définir hello quotidienne, hebdomadaire, mensuelle et annuelle étendue pour les points de sauvegarde spécifique hello.

    ![La machine virtuelle est sauvegardée avec un point de récupération](./media/backup-azure-vms/long-term-retention.png)

    Stratégie de rétention spécifie la durée hello pour stocker une sauvegarde. Vous pouvez spécifier des stratégies de rétention différentes basées sur lors de la sauvegarde de hello est effectuée.
7. Cliquez sur **travaux** liste de hello tooview de **configurer la Protection** travaux.

    ![Configurer le travail de protection](./media/backup-azure-vms/protect-configureprotection.png)

    Maintenant que vous avez créé la stratégie de hello, passez l’étape suivante de toohello et exécuter la sauvegarde initiale de hello.

## <a name="initial-backup"></a>Sauvegarde initiale
Une fois qu’un ordinateur virtuel a été protégé par une stratégie, vous pouvez afficher cette relation à hello **éléments protégés** onglet. Jusqu'à ce que la sauvegarde initiale de hello se produit, hello **état de la Protection** affiche sous la forme **Protected - (en attente de sauvegarde initiale)**. Par défaut, première sauvegarde planifiée du hello est hello *sauvegarde initiale*.

![Sauvegarde en attente](./media/backup-azure-vms-first-look/protection-pending-border.png)

toostart hello sauvegarde initiale maintenant :

1. Sur hello **éléments protégés** , cliquez sur **sauvegarde maintenant** bas hello de page de hello.
    ![Icône Sauvegarder maintenant](./media/backup-azure-vms-first-look/backup-now-icon.png)

    Hello service Azure Backup crée une tâche de sauvegarde pour l’opération de sauvegarde initiale hello.
2. Cliquez sur hello **travaux** liste de hello onglet tooview des tâches.

    ![Sauvegarde en cours](./media/backup-azure-vms-first-look/protect-inprogress.png)

    Lorsque la sauvegarde initiale est terminée, le statut de hello de machine virtuelle de hello Bonjour **éléments protégés** onglet est *protégé*.

    ![La machine virtuelle est sauvegardée avec un point de récupération](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > La sauvegarde des machines virtuelles est un processus local. Vous ne pouvez pas sauvegarder des ordinateurs virtuels à partir d’un coffre de sauvegarde de tooa région dans une autre région. Par conséquent, pour chaque région Azure qui a des machines virtuelles qui doivent toobe sauvegardé, au moins un coffre de sauvegarde doit être créé dans cette région.
   >
   >

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous êtes parvenu à sauvegarder une machine virtuelle, d’autres étapes peuvent vous intéresser. Hello plus logique consiste toofamiliarize vous-même avec la restauration de données tooa machine virtuelle. Toutefois, il existe des tâches de gestion qui vous aideront à comprendre comment tookeep sécurité de vos données et réduire les coûts.

* [Gestion et surveillance de vos machines virtuelles](backup-azure-manage-vms.md)
* [Restauration des machines virtuelles](backup-azure-restore-vms.md)
* [Instructions pour la résolution des problèmes](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a>Des questions ?
Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).
