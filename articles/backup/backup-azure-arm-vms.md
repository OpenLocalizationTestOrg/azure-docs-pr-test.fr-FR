---
title: aaaBack des machines virtuelles Azure | Documents Microsoft
description: "Permet de découvrir, d’enregistrer et de sauvegarder des machines virtuelles tooa coffre recovery services."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sauvegarde de machine virtuelle ; sauvegarder la machine virtuelle ; sauvegarde et récupération d’urgence ; sauvegarde de machine virtuelle arm"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a>Sauvegarder les machines virtuelles de coffre de Services de récupération tooa
> [!div class="op_single_selector"]
> * [Sauvegarder le coffre de Services tooRecovery de machines virtuelles](backup-azure-arm-vms.md)
> * [Sauvegarder des machines virtuelles tooBackup coffre](backup-azure-vms.md)
>
>

Cet article décrit en détail comment tooback des machines virtuelles de Azure (déployées par le Gestionnaire de ressources et déployés classique) tooa Services de récupération de coffre. La plupart du travail hello pour la sauvegarde d’ordinateurs virtuels est préparation de hello. Avant de pouvoir sauvegarder ou protéger un ordinateur virtuel, vous devez effectuer hello [conditions préalables](backup-azure-arm-vms-prepare.md) tooprepare votre environnement de protection de vos machines virtuelles. Une fois que vous avez terminé la configuration requise de hello, vous pouvez lancer hello opération de sauvegarde tootake des instantanés de votre machine virtuelle.


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

Pour plus d’informations, consultez les articles hello sur [planification de votre infrastructure de sauvegarde de machine virtuelle dans Azure](backup-azure-vms-introduction.md) et [machines virtuelles](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="triggering-hello-backup-job"></a>Déclenchement hello tâche de sauvegarde
stratégie de sauvegarde Hello associé hello que coffre des Services de récupération définit la fréquence et à quel moment la sauvegarde hello s’exécute. Par défaut, hello première planifiée est hello initiale sauvegarde. Jusqu'à ce que la sauvegarde initiale de hello se produit, hello état de la dernière sauvegarde sur hello **les travaux de sauvegarde** panneau affiche sous la forme **avertissement (sauvegarde initiale en attente)**.

![Sauvegarde en attente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

Sauf si votre sauvegarde initiale est due toobegin bientôt, il est recommandé d’exécuter **sauvegarder maintenant**. Hello procédure suivante commence à partir du tableau de bord coffre hello. Cette procédure remplit pour l’exécution du travail de sauvegarde initiale hello après avoir terminé toutes les conditions préalables. Si la tâche de sauvegarde initiale hello a déjà été exécutée, cette procédure n’est pas disponible. Hello stratégie de sauvegarde associée détermine prochaine tâche de sauvegarde hello.  

toorun hello initiale travail de sauvegarde :

1. Tableau de bord du coffre hello, cliquez sur nombre hello sous **des éléments de sauvegarde**, ou cliquez sur hello **des éléments de sauvegarde** vignette. <br/>
  ![Icône Paramètres](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Hello **des éléments de sauvegarde** panneau s’ouvre.

  ![Éléments de sauvegarde](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. Sur hello **des éléments de sauvegarde** les lames, les éléments select hello.

  ![Icône Paramètres](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Hello **des éléments de sauvegarde** liste s’ouvre. <br/>

  ![Travail de sauvegarde déclenché](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Sur hello **des éléments de sauvegarde** , cliquez sur le bouton de sélection hello **...**  menu de contexte tooopen hello.

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu.png)

  menu contextuel de Hello s’affiche.

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Dans le menu contextuel de hello, cliquez sur **sauvegarder maintenant**.

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  panneau Hello sauvegarder maintenant s’ouvre.

  ![Affiche le panneau hello sauvegarder maintenant](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Dans Panneau de sauvegarder maintenant du hello, cliquez l’icône de calendrier hello, utilisez Bonjour calendrier contrôle tooselect Bonjour dernier jour de ce point de récupération est conservé, puis cliquez sur **sauvegarde**.

  ![définir hello dernier jour hello sauvegarder maintenant point de récupération est conservé.](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Notifications de déploiement vous permettent de connaître la tâche de sauvegarde hello a été déclenchée, et que vous pouvez surveiller la progression hello de hello de page de travaux de sauvegarde hello. Selon la taille de hello de votre machine virtuelle, la création de sauvegarde initiale de hello peut prendre un certain temps.

6. état de hello tooview ou le suivi de la sauvegarde initiale hello, tableau de bord du coffre hello, sur hello **les travaux de sauvegarde** cliquez sur la vignette **en cours d’exécution**.

  ![Vignette Travaux de sauvegarde](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  Panneau de travaux de sauvegarde Hello s’ouvre.

  ![Vignette Travaux de sauvegarde](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  Bonjour **travaux de sauvegarde** panneau, vous pouvez voir État hello de tous les travaux. Vérifiez si le travail de sauvegarde hello pour votre machine virtuelle est toujours en cours ou s’il s’est terminé. Une opération de sauvegarde est terminée, le statut de hello est *terminé*.

  > [!NOTE]
  > Dans le cadre de l’opération de sauvegarde hello, hello Azure Backup service émet une extension de sauvegarde commande toohello dans chaque tooflush de machine virtuelle, toutes les écritures et prendre un instantané cohérent.
  >
  >

## <a name="troubleshooting-errors"></a>Résolution des erreurs
Si vous rencontrez des problèmes pendant la sauvegarde de votre machine virtuelle, consultez hello [article de résolution des problèmes de machine virtuelle](backup-azure-vms-troubleshoot.md) de l’aide.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez protégé votre machine virtuelle, consultez hello suivant toolearn des articles sur les tâches de gestion de machine virtuelle et comment toorestore machines virtuelles.

* [Gestion et surveillance de vos machines virtuelles](backup-azure-manage-vms.md)
* [Restauration des machines virtuelles](backup-azure-arm-restore-vms.md)
