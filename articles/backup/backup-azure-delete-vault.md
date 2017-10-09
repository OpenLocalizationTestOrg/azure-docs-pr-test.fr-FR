---
title: " Supprimer un coffre Recovery Services dans Azure | Microsoft Docs "
description: "Comment toodelete une sauvegarde Azure et Services de récupération de coffre. Un coffre de sauvegarde peut être appelé un coffre cloud Azure ou un coffre de récupération Azure. Résolution des problèmes lorsque vous ne pouvez pas supprimer un coffre de sauvegarde dans le portail classique de hello ou le portail Azure."
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a>Supprimer un coffre Recovery Services
Hello service Azure Backup a deux types de coffres - coffre de sauvegarde hello et le coffre Recovery Services hello. coffre de sauvegarde Hello surviennent en premier. Puis hello de coffre Recovery Services arrivée de déploiements de gestionnaire de ressources toosupport hello développé. En raison de hello capacités étendues et les dépendances informations hello qui doivent être stockés dans le coffre hello, supprimer un coffre de sauvegarde ou de Services de récupération peuvent prêter à confus. Cet article explique comment les coffres de toodelete hello dans le portail classique de hello et hello portail Azure.  

| **Type de déploiement** | **Portail** | **Nom du coffre** |
| --- | --- | --- |
| Classique |Classique |Archivage de sauvegarde |
| Gestionnaire de ressources |Microsoft Azure |Coffre Recovery Services |

> [!NOTE]
> Les coffres de sauvegarde ne peuvent pas protéger les solutions déployées par le biais de Resource Manager. Toutefois, vous pouvez utiliser un coffre Recovery Services tooprotect déployé généralement des serveurs et les machines virtuelles.  
>

> [!IMPORTANT]
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> **Le 15 octobre 2017**, vous ne pourra plus être coffres de sauvegarde toocreate toouse en mesure de PowerShell. <br/> **À compter du 1er novembre 2017** :
>- Les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>

Dans cet article, nous utilisons le terme de hello, archivage, toorefer toohello de formulaire générique de coffre de sauvegarde hello ou un coffre de Services de récupération. Nous utilisons le nom formel de hello, coffre de sauvegarde ou coffre Recovery Services, lorsqu’il est nécessaire toodistinguish entre les coffres hello.

## <a name="deleting-a-recovery-services-vault"></a>Supprimer un coffre Recovery Services
Supprimer un coffre Recovery Services est un processus en une étape - *fourni le coffre hello ne contient pas toutes les ressources*. Avant de pouvoir supprimer un coffre Recovery Services, vous devez supprimer ou supprimer toutes les ressources dans le coffre hello. Si vous essayez de toodelete un coffre qui contient des ressources, vous obtenez une erreur comme hello suivant image :

![Erreur de suppression du coffre](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

Jusqu'à ce que vous avez effacé les ressources hello du coffre de hello, en cliquant sur **réessayer** produit hello même message d’erreur. Si vous êtes bloqué sur ce message d’erreur, cliquez sur **Annuler** et toodelete des ressources de hello dans le coffre hello les étapes suivantes de hello d’utilisation.

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a>Suppression d’éléments hello dans un coffre de protéger un ordinateur virtuel
Si vous avez déjà des Services de récupération hello coffre ouvrir, ignorer toohello deuxième étape.

1. Ouvrez hello portail Azure et à partir du tableau de bord de hello ouvrez coffre hello toodelete.

   Si vous n’avez pas hello de coffre Recovery Services épinglées toohello tableau de bord, dans le menu du Hub hello, cliquez sur **plus Services** et, dans la liste hello des ressources, tapez **Recovery Services**. Comme vous commencez à taper, hello filtres de la liste en fonction de votre entrée. Cliquez sur **Coffres Recovery Services**.

   ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   liste de Hello des coffres des Services de récupération s’affiche. Dans la liste hello, sélectionnez coffre hello toodelete.

   ![choisir le coffre à partir de la liste](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. Bonjour coffre vue, regardez à hello **Essentials** volet. toodelete un coffre, il ne peut pas être tous les éléments protégés. Si vous voyez un nombre différent de zéro, sous **des éléments de sauvegarde** ou **sauvegarde des serveurs d’administration**, vous devez supprimer ces éléments avant de pouvoir supprimer le coffre hello.

    ![Examiner le volet Essentials pour identifier les éléments protégés](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    Machines virtuelles et les fichiers/dossiers sont considérés comme des éléments de sauvegarde et sont répertoriées dans hello **des éléments de sauvegarde** zone du volet d’Essentials hello. Un serveur DPM est répertorié dans hello **sauvegarde du serveur de gestion** zone du volet d’Essentials hello. **Éléments répliqués** se rapportent toohello service Azure Site Recovery.
3. toobegin hello de suppression des éléments protégés à partir du coffre hello, rechercher des éléments dans le coffre hello hello. Dans le tableau de bord coffre hello cliquez sur **paramètres**, puis cliquez sur **des éléments de sauvegarde** tooopen ce panneau.

    ![choisir le coffre à partir de la liste](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    Hello **des éléments de sauvegarde** panneau a des listes distinctes selon hello Type d’élément : Machines virtuelles Azure ou les fichiers-dossiers (voir l’image). liste du Type d’élément par défaut Hello indiqué est Machines virtuelles Azure. liste de hello tooview d’éléments de dossiers de fichiers dans le coffre hello, sélectionnez **dossiers de fichiers** à partir du menu déroulant de hello.
4. Avant de pouvoir supprimer un élément à partir du coffre hello protéger un ordinateur virtuel, vous devez arrêter le travail de sauvegarde de l’élément hello et supprimer les données de point de récupération hello. Pour chaque élément dans le coffre de hello, procédez comme suit :

    a. Sur hello **des éléments de sauvegarde** panneau, avec le bouton hello élément à partir du menu contextuel de hello, sélectionnez **arrêter la sauvegarde**.

    ![arrêter le travail de sauvegarde hello](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    panneau d’arrêter la sauvegarde Hello s’ouvre.

    b. Sur hello **arrêter la sauvegarde** panneau, à partir de hello **choisir une option** menu, sélectionnez **supprimer les données de sauvegarde** > nom hello du type d’élément de hello > et cliquez sur **arrêter sauvegarde**.

    Nom hello du type d’élément de hello, tooverify vous souhaitez toodelete il. Hello **arrêter la sauvegarde** bouton est activé après avoir vérifié les élément hello. Si vous ne voyez pas le nom hello boîte de dialogue zone tootype hello de sauvegarder l’élément hello, vous avez choisi hello **conserver les données de sauvegarde** option.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    Si vous le souhaitez, vous pouvez fournir une raison pourquoi vous supprimez des données de hello et ajoutez des commentaires. Après avoir cliqué sur **arrêter la sauvegarde**, autoriser hello delete travail toocomplete avant de tenter de coffre de hello toodelete. tooverify qui hello tâche est terminée, vérifiez les Messages d’Azure hello ![supprimer les données de sauvegarde](./media/backup-azure-delete-vault/messages.png). <br/>
    Une fois le travail de hello est terminée, vous recevez un message indiquant que le processus de sauvegarde hello a été arrêtée et les données de sauvegarde hello, pour cet élément a été supprimées.

    c. Après la suppression d’un élément de liste hello, sur hello **des éléments de sauvegarde** menu, cliquez sur **Actualiser** hello toosee autres articles dans le coffre hello.

      ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/empty-items-list.png)

      Lorsqu’il n’y a aucun élément dans la liste de hello, faites défiler toohello **Essentials** volet dans le panneau de coffre de sauvegarde hello. Il ne doit pas contenir **d’Éléments de sauvegarde**, de **Serveurs de gestion des sauvegardes** ou **d’Éléments répliqués** répertoriés. Si les éléments apparaissent toujours dans le coffre de hello, retourner toostep trois et choisir une liste de type d’élément différent.  
5. Lorsqu’il n’y a aucun élément dans la barre d’outils du coffre hello, cliquez sur **supprimer**.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/delete-vault.png)
6. tooverify que vous souhaitez le coffre hello toodelete, cliquez sur **Oui**.

    coffre de Hello est supprimé et le portail de hello retourne toohello **nouveau** menu de service.

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a>Que se passe-t-il si j’ai arrêté le processus de sauvegarde hello mais la conservation des données hello ?
Si vous avez arrêté mais accidentellement des processus de sauvegarde hello *conservées* les données de salutation, vous devez supprimer les données de sauvegarde hello avant de pouvoir supprimer le coffre hello. données de sauvegarde hello toodelete :

1. Sur hello **des éléments de sauvegarde** avec le bouton hello panneau, élément et dans le menu contextuel de hello cliquez sur **supprimer les données de sauvegarde**.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    Hello **supprimer les données de sauvegarde** panneau s’ouvre.
2. Sur hello **supprimer les données de sauvegarde** panneau, nom hello du type d’élément de hello, puis cliquez sur **supprimer**.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/delete-retained-vault.png)

    Une fois que vous avez supprimé des données de hello, retourner toostep 4c et poursuivre le processus de hello.

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a>Supprimer un tooprotect coffre utilisé un serveur DPM
Avant de pouvoir supprimer un tooprotect coffre utilisé un serveur DPM, vous devez effacer les points de récupération qui ont été créés et puis annuler l’inscription de serveur hello du coffre de hello.

données de salutation toodelete associées à un groupe de protection :

1. Bonjour la Console Administrateur DPM, cliquez sur **Protection** > sélectionnez un groupe de protection > sélectionnez hello membre du groupe de Protection > dans la barre d’outils hello, cliquez sur **supprimer**.

  Hello de hello sélectionnez membre du groupe de Protection tooactivate **supprimer** bouton dans la barre d’outils hello. Dans l’exemple de hello, est membre de hello **dummyvm9**. tooselect plusieurs membres de groupe de protection hello, maintenez la touche Ctrl de hello tout en cliquant sur les membres hello.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    Hello **arrêter la Protection** boîte de dialogue s’ouvre.
2. Bonjour **arrêter la Protection** boîte de dialogue, sélectionnez **supprimer les données protégées**, puis cliquez sur **arrêter la Protection**.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    toodelete un coffre, vous devez effacer ou supprimer, archivage hello des données protégées. En fonction du nombre de hello de points de récupération et les données dans le groupe de protection hello, il peut prendre de quelques secondes tooseveral minutes toodelete les données de salutation. Hello **arrêter la Protection** boîte de dialogue affiche l’état de hello lorsque hello est terminée.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. Continuez ce processus pour tous les membres de tous les groupes de protection.

    Supprimez toutes les données protégées et tous les groupes de protection.
4. Après la suppression de tous les membres du groupe de protection hello, basculez toohello portail Azure. Ouvrir le tableau de bord coffre hello et assurez-vous qu’aucun **des éléments de sauvegarde**, **sauvegarde des serveurs d’administration**, ou **éléments répliqués**. Dans la barre d’outils du coffre hello, cliquez sur **supprimer**.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/delete-vault.png)

    S’il existe des serveurs inscrits de gestion de sauvegarde toohello vault, vous ne pouvez pas supprimer l’archivage de hello même s’il n’existe aucune donnée dans le coffre de hello. Si vous avez supprimé des serveurs d’administration de sauvegarde hello associés au coffre de hello, mais il existe des serveurs répertoriés dans hello **Essentials** volet, consultez [recherche hello sauvegarde gestion serveurs inscrits toohello vault](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault) .
5. tooverify que vous souhaitez le coffre hello toodelete, cliquez sur **Oui**.

    coffre de Hello est supprimé et le portail de hello retourne toohello **nouveau** menu de service.

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a>Supprimer un tooprotect coffre utilisé un serveur de Production
Avant de pouvoir supprimer un tooprotect coffre utilisé un serveur de Production, vous devez supprimer ou annuler l’inscription de serveur hello du coffre de hello.

serveur de Production hello toodelete associée hello coffre :

1. Bonjour portail Azure, ouvrez le tableau de bord coffre hello et cliquez sur **paramètres** > **sauvegarde Infrastructure** > **les serveurs de Production**.

    ![ouvrir le panneau serveurs de production](./media/backup-azure-delete-vault/delete-production-server.png)

    Hello **les serveurs de Production** panneau s’ouvre et répertorie tous les serveurs de Production dans le coffre hello.

    ![liste des serveurs de production](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. Sur hello **les serveurs de Production** panneau, avec le bouton droit sur le serveur de hello, puis cliquez sur **supprimer**.

    ![supprimer le serveur de production ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    Hello **supprimer** panneau s’ouvre.

    ![supprimer le serveur de production ](./media/backup-azure-delete-vault/delete-blade.png)
3. Sur hello **supprimer** panneau, vérifiez le nom du serveur hello, puis cliquez sur **supprimer**. Vous devez nommer correctement serveur hello, tooactivate hello **supprimer** bouton.

    Une fois que le coffre hello est supprimé, vous recevez un message indiquant que le coffre hello a été supprimé. Après la suppression de tous les serveurs dans le coffre de hello, faites défiler le volet d’Essentials toohello précédent dans le tableau de bord coffre hello.
4. Dans le tableau de bord du coffre hello, assurez-vous qu’aucun **des éléments de sauvegarde**, **sauvegarde des serveurs d’administration**, ou **éléments répliqués**. Dans la barre d’outils du coffre hello, cliquez sur **supprimer**.
5. tooverify que vous souhaitez le coffre hello toodelete, cliquez sur **Oui**.

    coffre de Hello est supprimé et le portail de hello retourne toohello **nouveau** menu de service.

## <a name="delete-a-backup-vault-in-classic-portal"></a>Supprimer un coffre de sauvegarde dans le portail Classic
Hello instructions ci-après permettent de supprimer un coffre de sauvegarde dans le portail classique de hello. Avant de pouvoir supprimer le coffre de sauvegarde hello, vous devez supprimer les points de récupération hello, ou sauvegardé les éléments et supprimez des serveurs hello inscrit. Hello serveurs inscrits sont hello Windows Server, station de travail ou les ordinateurs virtuels qui ont été inscrits toohello coffre.

1. Ouvrez hello [portal de classique](https://manage.windowsazure.com).

2. À partir de la liste de hello des coffres de sauvegarde, sélectionnez le coffre hello toodelete.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    tableau de bord coffre Hello s’ouvre. Regardez nombre hello de serveurs Windows et/ou Azure ordinateurs virtuels avec le coffre hello. Observez également le stockage total de hello consommé dans Azure. Arrêtez tous les travaux de sauvegarde et supprimer toutes les données avant de supprimer le coffre hello.

3. Cliquez sur hello **éléments protégés** onglet, puis cliquez sur **arrêter la Protection**

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    Hello **arrêter la protection de 'votre coffre'** boîte de dialogue s’affiche.
4. Bonjour **arrêter la protection de 'votre coffre'** boîte de dialogue, vérifiez **supprimer les données de sauvegarde associées** et cliquez sur ![coche](./media/backup-azure-delete-vault/checkmark.png). <br/>
    Si vous le souhaitez, vous pouvez indiquer une raison pour l’arrêt de la protection et fournir des commentaires.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    Après la suppression des éléments dans le coffre hello hello, le coffre hello sera vide.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. Dans la liste de hello des onglets, cliquez sur **éléments inscrits**. Hello **Type** menu déroulant, Active hello de toochoose vous tapez de l’archivage toohello de serveur inscrit. type de Hello peut être Windows Server ou la Machine virtuelle Azure. Dans l’exemple suivant de hello, sélectionnez hello ordinateur virtuel enregistré toohello coffre, puis cliquez sur **Unregister**.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  Si vous souhaitez l’inscription de toodelete hello pour un serveur Windows, à partir de hello **Type** menu déroulant, sélectionnez **Windows Server**, cliquez sur ![coche](./media/backup-azure-delete-vault/checkmark.png) écran hello toorefresh puis cliquez sur **supprimer**. <br/>

  ![Sélectionnez Windows Server](./media/backup-azure-delete-vault/select-windows-server.png)

6. Dans la liste de hello des onglets, cliquez sur **tableau de bord** tooopen onglet. Vérifier aucun des serveurs inscrits ou les machines virtuelles protégées dans le cloud de hello. Vérifiez également qu’il n’y a aucune donnée dans le stockage. Cliquez sur **supprimer** toodelete le coffre hello.

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    écran de confirmation de coffre de sauvegarde de supprimer Hello s’ouvre. Sélectionnez une option pourquoi vous supprimez le coffre de hello, puis cliquez sur ![coche](./media/backup-azure-delete-vault/checkmark.png). <br/>

    ![Supprimer les données de sauvegarde](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    coffre de Hello est supprimé, et que vous retournez toohello de tableau de bord portail classique.

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a>Rechercher le coffre de toohello inscrit de serveurs de gestion de sauvegarde hello
Si vous avez plusieurs coffre tooa de serveurs inscrits, il peut être difficile tooremember les. serveurs de hello toosee inscrit toohello coffre et les supprimer :

1. Tableau de bord du coffre hello ouvert.
2. Bonjour **Essentials** volet, cliquez sur **paramètres** tooopen ce panneau.

    ![ouvrir le panneau paramètres](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. Sur hello **panneau paramètres**, cliquez sur **Infrastructure de sauvegarde**.
4. Sur hello **sauvegarde Infrastructure** panneau, cliquez sur **serveurs d’administration de sauvegarde**. Panneau de serveurs d’administration de sauvegarde Hello s’ouvre.

    ![liste des serveurs de gestion des sauvegardes](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. toodelete un serveur à partir de la liste de hello, cliquez sur le nom hello du serveur de hello, puis cliquez sur **supprimer**.
    Hello **supprimer** panneau s’ouvre.
6. Sur hello **supprimer** panneau, fournissez le nom hello du serveur de hello. S’il est un nom long, vous pouvez copier et coller à partir de la liste de hello sauvegarde des serveurs d’administration. Ensuite, cliquez sur **Supprimer**.  
