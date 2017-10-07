---
title: "aaaRestore un volume à partir de la sauvegarde sur une série StorSimple 8000 | Documents Microsoft"
description: "Explique comment toouse hello toorestore de catalogue de sauvegarde de service de gestionnaire de périphériques StorSimple un volume StorSimple à partir d’un jeu de sauvegarde."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 0fe2e4c23a23c75ce4058a8531356c94c973c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Restauration d’un volume StorSimple à partir d’un jeu de sauvegarde

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel décrit l’opération de restauration hello effectuée sur un appareil de série StorSimple 8000 à l’aide d’un jeu de sauvegarde existant. Hello d’utilisation **catalogue de sauvegarde** panneau toorestore un volume à partir d’une variable locale ou sauvegarde sur le cloud. Hello **catalogue de sauvegarde** panneau affiche tous les jeux de sauvegarde hello qui sont créés lorsque des sauvegardes manuelles ou automatisées sont effectuées. opération de restauration de Hello à partir d’un jeu de sauvegarde met le volume hello en ligne immédiatement pendant le téléchargement de données en arrière-plan de hello.

Une autre méthode toostart la restauration est toogo trop**périphériques > [votre appareil] > Volumes**. Bonjour **Volumes** panneau, sélectionnez un volume, un menu contextuel hello tooinvoke, puis **restaurer**.

## <a name="before-you-restore"></a>Avant de procéder à la restauration

Avant de démarrer une restauration, passez en revue hello suivant mises en garde :

* **Vous devez déconnecter volume de hello** : prendre un volume hello hors connexion sur les deux hôtes hello et hello périphérique avant de vous lancer l’opération de restauration hello. Bien que l’opération de restauration de hello met automatiquement le volume hello en ligne sur l’appareil de hello, vous devez manuellement mettre appareil hello en ligne sur l’ordinateur hôte de hello. Vous pouvez donner le volume hello en ligne sur l’ordinateur hôte de hello dès que le volume de hello est en ligne sur l’appareil de hello. (Il est inutile toowait jusqu'à la fin d’opération de restauration hello.) Pour les procédures, passez trop[mettre un volume hors connexion](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).

* **Type de volume après restauration** : Deleted volumes sont restaurés en fonction de type hello dans l’instantané d’hello ; autrement dit, les volumes qui ont été attachés localement sont restaurés en tant que volumes attachés localement et les volumes qui ont été assemblés sont restaurés en tant que volumes hiérarchisés.

    Pour les volumes existants, hello en cours d’utilisation type de volume de hello substitue type hello est stocké dans l’instantané d’hello. Par exemple, si vous restaurez un volume à partir d’un instantané qui a été effectuée lors du type de volume hello a été à plusieurs niveaux et que le type de volume est désormais localement épinglé (en raison d’opération de conversion tooa qui a été exécutée), volume de hello restaurée en tant qu’un volume attaché localement. De même, si un volume attaché localement a été développé et restauré par la suite à partir d’un instantané plus ancien est effectuée lorsque le volume de hello était plus petit, hello volume restauré conservera taille développée de hello en cours.

    Vous ne peut pas convertir un volume à partir d’un volume de tooa attaché localement volume hiérarchisé ou à partir d’un tooa volume attaché localement à plusieurs niveaux volume alors que le volume de hello est en cours de restauration. Attendez la fin de l’opération de restauration hello, puis vous pouvez convertir le type de tooanother volume hello. Pour plus d’informations sur la conversion d’un volume, accédez trop[modifier le type de volume hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type). 

* **taille du volume Hello est répercutée dans le volume de hello restauré** – il s’agit d’un aspect important si vous restaurez un volume attaché localement a été supprimé (car les volumes attachés localement sont totalement configurées). Assurez-vous que vous disposez de suffisamment d’espace avant de tenter de toorestore un volume attaché localement qui a été supprimé précédemment.

* **Vous ne pouvez pas développer un volume pendant qu’il est en cours de restauration** : attendez que l’opération de restauration hello est terminée avant de tenter de volume de hello tooexpand. Pour plus d’informations sur le développement d’un volume, accédez trop[modifier un volume](storsimple-8000-manage-volumes-u2.md#modify-a-volume).

* **Vous pouvez effectuer une sauvegarde lorsque vous restaurez un volume local** : pour les procédures accédez trop[utiliser des stratégies de sauvegarde hello le Gestionnaire de périphériques StorSimple service toomanage](storsimple-8000-manage-backup-policies-u2.md).

* **Vous pouvez annuler une opération de restauration** : Si vous annulez le travail de restauration hello, puis le volume de hello sera restaurée toohello état où il se trouvait avant que vous avez lancé l’opération de restauration hello. Pour les procédures, passez trop[annuler un travail](storsimple-8000-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Fonctionnement du processus de restauration

Pour les appareils exécutant Update 4 ou version ultérieure, une restauration basée sur une carte thermique est implémentée. Hello hôte demande des données tooaccess parviennent appareil de hello, ces demandes sont suivies et un heatmap est créé. Taux élevé d’entraîne des segments de données avec chaleur supérieure tandis que les taux inférieur traduit toochunks avec chaleur inférieur. Vous devez accéder à hello données au moins deux fois la mention toobe _à chaud_. Un fichier modifié est également marqué comme _chaud_. Une fois que vous avez lancé la restauration de hello, HYDRATATION proactive des données se produit en fonction de hello heatmap. Pour les versions antérieures à la mise à jour 4, les données de salutation sont téléchargées au cours de restauration basée sur l’accès uniquement.

Hello suivant mises en garde s’appliquent les restaurations à partir de tooheatmap :

* Le suivi de carte thermique est activé uniquement pour les volumes hiérarchisés (les volumes épinglés localement ne sont pas pris en charge).

* Restauration Heatmap n’est pas prise en charge durant le clonage d’un périphérique tooanother de volume. 

* S’il existe une restauration sur place et un instantané local pour hello toobe de volume restauré existe sur le périphérique de hello, nous ne pas réalimenter (comme les données sont déjà disponibles localement). 

* Par défaut, lorsque vous restaurez, hello réalimentation travaux sont lancés qui réalimenter proactive des données en fonction de hello heatmap. 

Dans la mise à jour 4, applets de commande Windows PowerShell peut être utilisé tooquery en cours d’exécution des travaux de la réactivation, annuler un travail de la réactivation et obtenir l’état de hello du travail de la réactivation hello.

* `Get-HcsRehydrationJob`-Cette applet de commande Obtient l’état hello du travail de la réactivation hello. Un seul travail de rafraîchissement est déclenché pour un volume.

* `Set-HcsRehydrationJob`-Cette applet de commande vous permet de toopause, arrêter, reprendre le travail de la réactivation hello, lors de la réactivation de hello est en cours d’exécution.

Pour plus d’informations sur les applets de commande de la réactivation, consultez trop[référence d’applet de commande Windows PowerShell pour StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

En général, avec le rafraîchissement automatique, des performances de lecture temporaires plus élevées sont attendues. magniutde réel de Hello d’améliorations dépend de divers facteurs tels que le modèle d’accès, évolution des données et le type de données. 

toocancel un travail de la réactivation, vous pouvez utiliser l’applet de commande PowerShell hello. Si vous le souhaitez travaux de réalimentation toopermanently désactiver pour tous les hello futures restaurations, [contactez le Support Microsoft](storsimple-8000-contact-microsoft-support.md).

## <a name="how-toouse-hello-backup-catalog"></a>Comment toouse hello catalogue de sauvegarde

Hello **catalogue de sauvegarde** panneau fournit une requête qui vous permet de toonarrow votre sélection du jeu de sauvegarde. Vous pouvez filtrer hello jeux de sauvegarde qui est récupérés en fonction de hello paramètres suivants :

* **Intervalle de temps** – hello plage de date et heure de création de jeu de sauvegarde hello.
* **APPAREIL** – périphérique hello sur quel hello jeu de sauvegarde a été créé.
* **Stratégie de sauvegarde** ou **Volume** – hello stratégie de sauvegarde ou volume associé à ce jeu de sauvegarde.

Hello jeux de sauvegarde filtrés sont ensuite sous forme de tableau en fonction de hello suivant des attributs :

* **Nom** hello – nom de la stratégie de sauvegarde hello ou volume associé au jeu de sauvegarde hello.
* **Type** : les jeux de sauvegarde peuvent être des instantanés locaux ou des instantanés cloud. Un instantané local est une sauvegarde de toutes vos données de volume stockées localement sur le périphérique de hello, tandis qu’un instantané cloud fait référence sauvegarde toohello des données de volume résidant dans le cloud de hello. Les instantanés locaux offrent un accès plus rapide, alors que les instantanés cloud sont choisis pour la résilience des données.
* **Taille** – hello taille réelle du jeu de sauvegarde hello.
* **Créé sur** : date de hello et l’heure de création des sauvegardes de hello. 
* **Volumes** -hello du nombre de volumes associé au jeu de sauvegarde hello.
* **Initiée par** : les sauvegardes hello peuvent être lancées automatiquement en fonction de tooa planification ou manuellement par un utilisateur. (Vous pouvez utiliser les sauvegardes tooschedule stratégie de sauvegarde. Vous pouvez également utiliser hello **sauvegarde** option tootake une sauvegarde interactive ou à la demande.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Comment toorestore votre volume StorSimple à partir d’une sauvegarde

Vous pouvez utiliser hello **catalogue de sauvegarde** panneau toorestore votre volume StorSimple à partir d’une sauvegarde spécifique. N’oubliez pas, toutefois, que la restauration d’un volume reprendra l’état toohello hello volume où qu'elle était lors de la sauvegarde de hello a été effectuée. Toutes les données qui a été ajoutées après l’opération de sauvegarde hello seront perdues.

> [!WARNING]
> Restauration à partir d’une sauvegarde remplace les volumes existants hello à partir de la sauvegarde de hello. Cela peut entraîner une perte de hello de toutes les données écrites après que hello sauvegarde a été effectuée.


### <a name="toorestore-your-volume"></a>toorestore votre volume.
1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, puis cliquez sur **catalogue de sauvegarde**.

2. Sélectionnez un jeu de sauvegarde comme suit :
   
   1. Spécifiez la plage de temps hello.
   2. Sélectionnez le périphérique approprié de hello.
   3. Dans la liste déroulante hello, choisissez que vous souhaitez tooselect la stratégie de sauvegarde ou volume hello pour la sauvegarde de hello.
   4. Cliquez sur **appliquer** tooexecute cette requête.

    Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.
   
    ![Liste des jeux de sauvegarde](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. Développez hello jeu de sauvegarde tooview hello associée des volumes. Ces volumes doivent être mis hors connexion sur l’hôte de hello et de périphérique avant de les restaurer. Accès aux volumes hello sur hello **Volumes** Panneau de votre appareil, puis hello de suivre les étapes [mettre un volume hors connexion](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake hors connexion.
   
   > [!IMPORTANT]
   > Assurez-vous que vous avez effectué des volumes hello hors connexion sur l’ordinateur hôte de hello tout d’abord, avant de mettre hors connexion les volumes hello sur le périphérique de hello. Si vous ne prenez pas les volumes hello hors connexion sur l’ordinateur hôte de hello, il pourrait endommager toodata corruption.
   
4. Accédez arrière toohello **catalogue de sauvegarde** onglet et sélectionnez un jeu de sauvegarde. Avec le bouton droit et, dans le menu contextuel de hello, sélectionnez **restaurer**.

    ![Liste des jeux de sauvegarde](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. Vous êtes invité à confirmer l’opération. Révision Bonjour restaurer les informations et puis sélectionnez la case à cocher de confirmation hello.
   
    ![Page Confirmation](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  Cliquez sur **Restaurer**. Cette commande lance un travail de restauration que vous pouvez afficher en accédant à hello **travaux** page.

    ![Page Confirmation](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. Une fois la restauration de hello est terminée, vérifiez que le contenu hello de vos volumes est remplacés par les volumes de sauvegarde de hello.


## <a name="if-hello-restore-fails"></a>Si la restauration de hello échoue

Vous recevrez une alerte si hello opération de restauration échoue pour une raison quelconque. Si cela se produit, actualisation hello liste de sauvegarde tooverify qui hello sauvegarde est toujours valide. Si la sauvegarde de hello est valide et que vous restaurez à partir du cloud de hello, puis des problèmes de connectivité peuvent être cause hello.

toocomplete hello l’opération de restauration, prendre du volume hello hors connexion sur l’ordinateur hôte de hello et recommencez l’opération de restauration hello. Notez que toutes les données de volume de toohello de modifications qui ont été effectuées au cours de hello des processus de restauration seront perdue.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[StorSimple de gérer les volumes](storsimple-8000-manage-volumes-u2.md).
* Découvrez comment trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

