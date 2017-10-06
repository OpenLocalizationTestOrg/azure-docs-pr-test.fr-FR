---
title: "aaaBack de coffre de sauvegarde de machines virtuelles déployées classique tooa | Documents Microsoft"
description: "Découvrez, inscrivez et sauvegardez vos machines virtuelles avec ces procédures pour la sauvegarde de la machine virtuelle Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sauvegarde de machine virtuelle ; sauvegarder la machine virtuelle ; sauvegarde et récupération d’urgence ; sauvegarde de machine virtuelle"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>Sauvegarde des machines virtuelles Azure (portail classique)
> [!div class="op_single_selector"]
> * [Sauvegarder le coffre de Services tooRecovery de machines virtuelles](backup-azure-arm-vms.md)
> * [Sauvegarder des machines virtuelles tooBackup coffre](backup-azure-vms.md)
>
>

Cet article fournit des procédures hello pour la sauvegarde d’un coffre de sauvegarde tooa déployés classique Azure virtual machine (VM). Il existe quelques tâches que vous devez tootake charge avant que vous puissiez sauvegarder une machine virtuelle Azure. Si vous n’avez pas déjà fait hello donc, complète [conditions préalables](backup-azure-vms-prepare.md) tooprepare votre environnement pour sauvegarder vos machines virtuelles.

Pour plus d’informations, reportez-vous aux articles de hello [planification de votre infrastructure de sauvegarde de machine virtuelle dans Azure](backup-azure-vms-introduction.md) et [machines virtuelles](https://azure.microsoft.com/documentation/services/virtual-machines/).

> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md). Un coffre de sauvegarde peut uniquement protéger les machines virtuelles déployées à l’aide du modèle Classic. Vous ne pouvez pas utiliser un coffre de sauvegarde pour protéger les machines virtuelles déployées par le biais de Resource Manager. Consultez [sauvegarder les machines virtuelles tooRecovery Services coffre](backup-azure-arm-vms.md) pour plus d’informations sur l’utilisation des Services de récupération des coffres-forts.
>
>

Les trois principales étapes de la sauvegarde des machines virtuelles sont les suivantes :

![Tooback trois étapes d’une machine virtuelle IaaS de Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> La sauvegarde des machines virtuelles est un processus local. Vous ne pouvez pas sauvegarder les machines virtuelles dans un coffre de sauvegarde de tooa région dans une autre région. Par conséquent, vous devez créer un archivage de sauvegarde dans chaque région Azure dans laquelle des machines virtuelles seront sauvegardées.
>
> [!IMPORTANT]
> À partir de mars 2017, vous pouvez utiliser n’est plus les coffres de sauvegarde hello toocreate portail classique.
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell. **D’ici au 1er novembre 2017** :
>- Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>

## <a name="step-1---discover-azure-virtual-machines"></a>Étape 1 - Découverte des machines virtuelles Azure
tooensure n’importe quel abonnement toohello ajouté de nouvelles machines virtuelles (VM) sont identifiés avant d’inscrire, exécuter le processus de découverte hello. Hello traiter les requêtes Azure pour la liste des ordinateurs virtuels dans l’abonnement hello, ainsi que les informations hello comme nom du service cloud hello et région de hello.

1. Connectez-vous à toohello [portal de classique](http://manage.windowsazure.com/)
2. Dans la liste de hello des services Azure, cliquez sur **Services de récupération** liste de hello tooopen de coffres de sauvegarde et de récupération de Site.
    ![Ouvrir la liste d’archivage](./media/backup-azure-vms/choose-vault-list.png)
3. Dans la liste hello de coffres de sauvegarde, sélectionnez tooback de coffre hello d’un ordinateur virtuel.

    S’il s’agit d’un nouveau portail de hello coffre ouvre toohello **Quick Start** page.

    ![Ouvrir le menu Éléments inscrits](./media/backup-azure-vms/vault-quick-start.png)

    Si le coffre hello a été configuré précédemment, le portail de hello ouvre toohello utilisé le plus récemment menu.
4. À partir du menu de coffre hello (en hello haut hello), cliquez sur **éléments inscrits**.

    ![Ouvrir le menu Éléments inscrits](./media/backup-azure-vms/vault-menu.png)
5. À partir de hello **Type** menu, sélectionnez **Machine virtuelle Azure**.

    ![Sélectionner la charge de travail](./media/backup-azure-vms/discovery-select-workload.png)
6. Cliquez sur **DISCOVER** bas hello de page de hello.
    ![Bouton découverte](./media/backup-azure-vms/discover-button-only.png)

    processus de découverte Hello peut prendre quelques minutes hello virtuels sont en cours sous forme de tableau. Il existe une notification bas hello écran hello qui vous permet de savoir que hello est en cours.

    ![Détection des machines virtuelles](./media/backup-azure-vms/discovering-vms.png)

    modifications de la notification Hello lorsque hello est terminée. Si le processus de découverte hello n’a pas trouvé les ordinateurs virtuels de hello, vérifiez d’abord que Hello VMs existent. Si les ordinateurs virtuels de hello existent, vérifiez hello machines virtuelles sont dans hello même région que le coffre de sauvegarde hello. Si les machines virtuelles de hello existent et sont hello la même région, vérifiez que Hello VM n’est pas déjà inscrit tooa coffre de sauvegarde. Si une machine virtuelle est le coffre de sauvegarde attribué tooa il n’est pas coffres de sauvegarde tooother toobe disponible attribué.

    ![Détection exécutée](./media/backup-azure-vms/discovery-complete.png)

    Une fois que vous avez découvert de nouveaux éléments de hello, accédez tooStep 2 et enregistrer vos machines virtuelles.

## <a name="step-2---register-azure-virtual-machines"></a>Étape 2 - Inscription des machines virtuelles Azure
Vous inscrivez une tooassociate de machine virtuelle Azure avec hello service Azure Backup. L’inscription est généralement une activité unique.

1. Accédez de coffre de sauvegarde toohello sous **Services de récupération** dans hello portail Azure, puis cliquez sur **éléments inscrits**.
2. Sélectionnez **Machine virtuelle Azure** à partir du menu déroulant de hello.

    ![Sélectionner la charge de travail](./media/backup-azure-vms/discovery-select-workload.png)
3. Cliquez sur **inscrire** bas hello de page de hello.
    ![Bouton Inscription](./media/backup-azure-vms/register-button-only.png)
4. Bonjour **enregistrer les éléments** menu contextuel, sélectionnez hello ordinateurs virtuels que vous souhaitez tooregister. S’il existe deux ou plusieurs machines virtuelles avec hello même nom, utilisez hello cloud service toodistinguish entre eux.

   > [!TIP]
   > Plusieurs machines virtuelles peuvent être inscrites en même temps.
   >
   >

    Un travail est créé pour chaque machine virtuelle sélectionnée.
5. Cliquez sur **afficher le travail** dans hello notification toogo toohello **travaux** page.

    ![Inscrire du travail](./media/backup-azure-vms/register-create-job.png)

    machine virtuelle de Hello apparaît également dans la liste hello des éléments inscrits, ainsi que de l’état hello de l’opération d’inscription de hello.

    ![État de l’inscription 1](./media/backup-azure-vms/register-status01.png)

    Lors de la fin de l’opération de hello, hello devient tooreflect hello *inscrit* état.

    ![État de l’inscription 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>Étape 3 - Protection des machines virtuelles Azure
Vous pouvez désormais configurer une stratégie de sauvegarde et de rétention pour la machine virtuelle de hello. Plusieurs machines virtuelles peuvent être protégées par la même action de protection.

Les coffres de sauvegarde Azure créés après mai 2015 fournis avec une stratégie par défaut intégrées dans le coffre hello. Cette stratégie par défaut est fournie avec une durée de conservation par défaut de 30 jours et une fréquence de sauvegarde quotidienne d’une fois par jour.

1. Accédez de coffre de sauvegarde toohello sous **Services de récupération** dans hello portail Azure, puis cliquez sur **éléments inscrits**.
2. Sélectionnez **Machine virtuelle Azure** à partir du menu déroulant de hello.

    ![Sélectionner la charge de travail dans le portail](./media/backup-azure-vms/select-workload.png)
3. Cliquez sur **protéger** bas hello de page de hello.

    Hello **Assistant protéger** s’affiche. Assistant de Hello répertorie uniquement les ordinateurs virtuels qui sont enregistrés et non protégés. Sélectionnez hello ordinateurs virtuels que vous souhaitez tooprotect.

    S’il existe deux ou plusieurs machines virtuelles avec hello même nom, utilisez hello cloud service toodistinguish entre les machines virtuelles de hello.

   > [!TIP]
   > Vous pouvez protéger plusieurs machines virtuelles en même temps.
   >
   >

    ![Configurer les paramètres de protection pendant la mise à jour](./media/backup-azure-vms/protect-at-scale.png)

4. Choisissez un **planification de sauvegarde** tooback les machines virtuelles hello que vous avez sélectionné. Vous pouvez sélectionner un ensemble de stratégies existant ou en définir un nouveau.

    Vous pouvez associer plusieurs machines virtuelles à chaque stratégie de sauvegarde. Toutefois, hello virtual machine peut uniquement être associé avec une stratégie à un moment donné dans le temps.

    ![Protéger grâce à la nouvelle stratégie](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Une stratégie de sauvegarde inclut un jeu de rétention pour les sauvegardes planifiée de hello. Si vous sélectionnez une stratégie de sauvegarde existante, vous ne pouvez pas modifier les options de rétention hello dans l’étape suivante de hello.
   >
   >

5. Choisissez un **de rétention** tooassociate avec des sauvegardes hello.

    ![Protéger avec la rétention flexible](./media/backup-azure-vms/policy-retention.png)

    Stratégie de rétention spécifie la durée hello pour stocker une sauvegarde. Vous pouvez spécifier des stratégies de rétention différentes basées sur lors de la sauvegarde de hello est effectuée. Par exemple, un point de sauvegarde effectué quotidiennement (qui sert de point de récupération opérationnel) peut être conservé pendant 90 jours. En comparaison, un point de sauvegarde effectuée à la fin de hello de chaque trimestre (à des fins d’audit) peut-être toobe conservée pendant des mois ou années.

    ![La machine virtuelle est sauvegardée avec un point de récupération](./media/backup-azure-vms/long-term-retention.png)

    Dans cet exemple :

   * **Stratégie de rétention quotidienne**: les sauvegardes effectuées quotidiennement sont stockées pendant 30 jours.
   * **Stratégie de rétention hebdomadaire**: les sauvegardes effectuées tous les dimanches sont conservées pendant 104 semaines.
   * **Stratégie de rétention mensuelle**: les sauvegardes effectuées sur hello dernier dimanche de chaque mois sont conservées pendant 120 mois.
   * **Stratégie de rétention annuelle**: les sauvegardes effectuées sur hello premier dimanche de chaque mois de janvier sont conservés pour de 99 ans.

     Un travail est créé de stratégie de protection tooconfigure hello et associer hello machines virtuelles toothat stratégie pour chaque ordinateur virtuel que vous avez sélectionné.
6. liste de hello tooview de **configurer la Protection** travaux, à partir du menu de coffres hello, cliquez sur **travaux** et sélectionnez **configurer la Protection** de hello **opération**  filtre.

    ![Configurer le travail de protection](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>Sauvegarde initiale
Une fois que l’ordinateur virtuel de hello est protégé par une stratégie, elle s’affiche sous hello **éléments protégés** onglet dont l’état hello *Protected - (en attente de sauvegarde initiale)*. Par défaut, première sauvegarde planifiée du hello est hello *sauvegarde initiale*.

sauvegarde initiale du hello tootrigger immédiatement après la configuration de la protection :

1. En bas de hello Hello **éléments protégés** , cliquez sur **sauvegarde maintenant**.

    Hello service Azure Backup crée une tâche de sauvegarde pour l’opération de sauvegarde initiale hello.
2. Cliquez sur hello **travaux** liste de hello onglet tooview des tâches.

    ![Sauvegarde en cours](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> Au cours de l’opération de sauvegarde hello, hello Azure Backup service émet une extension de sauvegarde commande toohello dans chaque tooflush de machine virtuelle, tous les travaux d’écriture et prenant un instantané cohérent.
>
>

Lorsque les sauvegarde initiale hello se termine, état hello de machine virtuelle de hello Bonjour **éléments protégés** onglet est *protégé*.

![La machine virtuelle est sauvegardée avec un point de récupération](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>Affichage des détails et de l’état de sauvegarde
Une fois que protégé, nombre d’ordinateurs virtuels hello augmente également Bonjour **tableau de bord** page Résumé. Hello **tableau de bord** page affiche également le nombre de hello de travaux à partir de hello des dernières 24 heures qui ont été *réussie*, ont *échec*et sont *en cours d’exécution*. Sur hello **travaux** page, utilisez hello **état**, **opération**, ou **de** et **à** toofilter de menus travaux de Hello.

![État de la sauvegarde sur la page Tableau de bord](./media/backup-azure-vms/dashboard-protectedvms.png)

Les valeurs dans le tableau de bord hello sont actualisés toutes les 24 heures.

## <a name="troubleshooting-errors"></a>Résolution des erreurs
Si vous rencontrez des problèmes pendant la sauvegarde de votre machine virtuelle, consultez hello [article de résolution des problèmes de machine virtuelle](backup-azure-vms-troubleshoot.md) de l’aide.

## <a name="next-steps"></a>Étapes suivantes
* [Gestion et surveillance de vos machines virtuelles](backup-azure-manage-vms.md)
* [Restauration des machines virtuelles](backup-azure-restore-vms.md)
