---
title: "un volume StorSimple à partir de la sauvegarde d’aaaRestore | Documents Microsoft"
description: "Explique comment toouse hello StorSimple Manager service catalogue de sauvegarde page toorestore un volume StorSimple à partir d’un jeu de sauvegarde."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6f289c39-96c7-4d57-b68a-4bc2e99aef9d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/22/2017
ms.author: alkohli
ms.openlocfilehash: c2e38765e750749f5764b5cbf2167d3cd5edfe5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set-update-2"></a>Restauration d’un volume StorSimple à partir d’un jeu de sauvegarde (Mise à jour 2)
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Vue d'ensemble
Hello **catalogue de sauvegarde** page affiche tous les jeux de sauvegarde hello qui sont créés lorsque des sauvegardes manuelles ou automatisées sont effectuées. Utiliser toolist de cette page et gérer les sauvegardes, restaurez à partir d’un jeu de sauvegarde ou de cloner un volume.

 ![Page Catalogue de sauvegarde](./media/storsimple-restore-from-backup-set-u2/restore.png)

Ce didacticiel explique comment toouse hello **catalogue de sauvegarde** page toorestore votre appareil à partir d’un jeu de sauvegarde.

Vous pouvez restaurer un volume à partir d’une sauvegarde locale ou sur le cloud. Dans les deux cas, opération de restauration hello met le volume hello en ligne immédiatement pendant le téléchargement de données en arrière-plan de hello. 

## <a name="before-you-restore"></a>Avant de procéder à la restauration
Avant de lancer une opération de restauration, vous devez connaître de hello suivant mises en garde :

* **Mettre hors connexion de volume de hello** : prendre un volume hello hors connexion sur les deux hôtes hello et hello périphérique avant de vous lancer l’opération de restauration hello. Bien que l’opération de restauration de hello met automatiquement le volume hello en ligne sur l’appareil de hello, vous devez manuellement mettre appareil hello en ligne sur l’ordinateur hôte de hello. Vous pouvez mettre le volume hello en ligne sur l’ordinateur hôte de hello lorsque le volume de hello est en ligne sur l’appareil de hello. (Il est inutile toowait jusqu'à la fin d’opération de restauration hello.) Pour les procédures, passez trop[mettre un volume hors connexion](storsimple-manage-volumes-u2.md#take-a-volume-offline).
* **Type de volume après restauration** – Deleted volumes sont restaurés en fonction de type hello dans l’instantané d’hello. Les volumes qui ont été épinglés localement sont restaurés en tant que volumes épinglés localement, et les volumes qui étaient hiérarchisés sont restaurés en tant que volumes hiérarchisés.
  
    Pour les volumes existants, hello en cours d’utilisation type de volume de hello substitue type hello est stocké dans l’instantané d’hello. Par exemple, si vous restaurez un volume à partir d’un instantané qui a été effectuée lors du type de volume hello a été à plusieurs niveaux et que le type de volume est désormais localement épinglé (en raison d’opération de conversion tooa), puis le volume de hello est restauré en tant qu’un volume attaché localement. De même, si un volume attaché localement est développé et restauré par la suite à partir d’un instantané plus ancien est effectuée lorsque le volume de hello était plus petit, hello volume restauré conserve taille développée de hello en cours.
  
    Impossible de convertir un volume à partir d’un volume de tooa attaché localement volume hiérarchisé ou _inversement_ alors que le volume de hello est en cours de restauration. Attendez la fin de l’opération de restauration hello, puis vous pouvez convertir le type de tooanother volume hello. Pour plus d’informations sur la conversion d’un volume, accédez trop[modifier le type de volume hello](storsimple-manage-volumes-u2.md#change-the-volume-type). 
* **taille du volume Hello est répercutée dans le volume de hello restauré** – il s’agit d’un aspect important si vous restaurez un volume attaché localement a été supprimé (car les volumes attachés localement sont totalement configurées). Assurez-vous que vous disposez de suffisamment d’espace avant de tenter de toorestore un volume attaché localement qui a été supprimé précédemment. 
* **Vous ne pouvez pas développer un volume pendant qu’il est en cours de restauration** : attendez que l’opération de restauration hello est terminée avant de tenter de volume de hello tooexpand. Pour plus d’informations sur le développement d’un volume, accédez trop[modifier un volume](storsimple-manage-volumes-u2.md#modify-a-volume).
* **Vous pouvez effectuer une sauvegarde lorsque vous restaurez un volume local** : pour les procédures accédez trop[utiliser des stratégies de sauvegarde hello StorSimple Manager service toomanage](storsimple-manage-backup-policies.md).
* **Vous pouvez annuler une opération de restauration** : Si vous annulez le travail de restauration hello, puis le volume de hello est restaurée toohello état où il se trouvait avant le lancement de la restauration de hello. Pour les procédures, passez trop[annuler un travail](storsimple-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Fonctionnement du processus de restauration
Pour les appareils exécutant Update 4 ou version ultérieure, une restauration basée sur une carte thermique est implémentée. Hello hôte demande des données tooaccess parviennent appareil de hello, ces demandes sont suivies et un heatmap est créé. Taux élevé d’entraîne des segments de données avec chaleur supérieure tandis que les taux inférieur traduit toochunks avec chaleur inférieur. Vous devez accéder à hello données au moins deux fois la mention toobe _à chaud_. Un fichier modifié est également marqué comme _chaud_. Une fois que vous avez lancé la restauration de hello, HYDRATATION proactive des données se produit en fonction de hello heatmap. Pour les versions antérieures à la mise à jour 4, les données de salutation a été téléchargées au cours de restauration basée sur l’accès uniquement. 

Le suivi basé sur la carte thermique est activé uniquement pour les volumes hiérarchisés (les volumes épinglés localement ne sont pas pris en charge). Restauration Heatmap est également pas pris en charge le clonage d’un périphérique tooanother de volume. S’il existe une restauration sur place et un instantané local pour hello toobe de volume restauré existe sur le périphérique de hello, nous ne pas réalimenter (comme les données sont déjà disponibles localement). Par défaut, lorsque vous restaurez, hello réalimentation travaux sont lancés qui réalimenter proactive des données en fonction de hello heatmap. Dans la mise à jour 4, applets de commande Windows PowerShell peut être utilisé tooquery en cours d’exécution des travaux de la réactivation, annuler un travail de la réactivation et obtenir l’état de hello du travail de la réactivation hello.

* `Get-HcsRehydrationJob`-Cette applet de commande Obtient l’état hello du travail de la réactivation hello. Un seul travail de rafraîchissement est déclenché pour un volume.
* `Set-HcsRehydrationJob`-Cette applet de commande vous permet de toopause, arrêter, reprendre le travail de la réactivation hello, lors de la réactivation de hello est en cours d’exécution. 

Pour plus d’informations sur les applets de commande de la réactivation, consultez trop[référence d’applet de commande Windows PowerShell pour StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

En général, avec le rafraîchissement automatique, des performances de lecture temporaires plus élevées sont attendues. magniutde réel de Hello d’améliorations dépend de divers facteurs tels que le modèle d’accès, évolution des données et le type de données. toocancel un travail de la réactivation, vous pouvez utiliser l’applet de commande PowerShell hello. Si vous souhaitez les travaux de réalimentation toopermanently désactiver pour toutes les restaurations futures hello, contactez le Support Microsoft.

## <a name="how-toouse-hello-backup-catalog"></a>Comment toouse hello catalogue de sauvegarde
Hello **catalogue de sauvegarde** page fournit une requête qui vous permet de toonarrow votre sélection du jeu de sauvegarde. Vous pouvez filtrer hello jeux de sauvegarde qui est récupérés en fonction de hello paramètres suivants :

* **APPAREIL** – périphérique hello sur quel hello jeu de sauvegarde a été créé.
* **Stratégie de sauvegarde** ou **volume** – hello stratégie de sauvegarde ou volume associé à ce jeu de sauvegarde.
* **À partir de** et **à** : hello plage de date et heure de création de jeu de sauvegarde hello.

Hello jeux de sauvegarde filtrés sont ensuite sous forme de tableau en fonction de hello suivant des attributs :

* **Nom** hello – nom de la stratégie de sauvegarde hello ou volume associé au jeu de sauvegarde hello.
* **Taille** – hello taille réelle du jeu de sauvegarde hello.
* **Créé sur** : date de hello et l’heure de création des sauvegardes de hello. 
* **Type** : les jeux de sauvegarde peuvent être des instantanés locaux ou des instantanés cloud. Un instantané local est une sauvegarde de toutes vos données de volume stockées localement sur le périphérique de hello. Un instantané cloud fait référence sauvegarde toohello des données de volume résidant dans le cloud de hello. Les instantanés locaux offrent un accès plus rapide, alors que les instantanés cloud sont choisis pour la résilience des données.
* **Initié par** : les sauvegardes hello peuvent être lancées automatiquement en fonction de tooa planification ou manuellement par vous-même. (Vous pouvez utiliser les sauvegardes tooschedule stratégie de sauvegarde. Vous pouvez également utiliser hello **sauvegarde** option tootake une sauvegarde interactive.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Comment toorestore votre volume StorSimple à partir d’une sauvegarde
Vous pouvez utiliser hello **catalogue de sauvegarde** page toorestore votre volume StorSimple à partir d’une sauvegarde spécifique. N’oubliez pas, toutefois, que la restauration d’un volume rétablit l’état toohello hello volume où qu'elle était lors de la sauvegarde de hello a été effectuée. Les données qui a été ajoutées après l’opération de sauvegarde hello sont perdues.

> [!WARNING]
> Restauration à partir d’une sauvegarde remplace les volumes existants de hello à partir de la sauvegarde de hello. Cela peut entraîner une perte de hello de toutes les données écrites après que hello sauvegarde a été effectuée.
> 
> 

### <a name="toorestore-your-volume"></a>toorestore votre volume.
1. Sur la page du service StorSimple Manager hello, cliquez sur hello **catalogue de sauvegarde** onglet.
   
    ![Catalogue de sauvegarde](./media/storsimple-restore-from-backup-set-u2/restore.png)
2. Sélectionnez un jeu de sauvegarde comme suit :
   
   1. Sélectionnez le périphérique approprié de hello.
   2. Dans la liste déroulante hello, choisissez que vous souhaitez tooselect la stratégie de sauvegarde ou volume hello pour la sauvegarde de hello.
   3. Spécifiez la plage de temps hello.
   4. Cliquez sur une icône de coche hello ![icône en forme de coche](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png) tooexecute cette requête.
      
      Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.
3. Développez hello jeu de sauvegarde tooview hello associée des volumes. Ces volumes doivent être mis hors connexion sur l’hôte de hello et de périphérique avant de les restaurer. Accès aux volumes hello sur hello **conteneurs de volumes** page, puis suivez les étapes de hello dans [mettre un volume hors connexion](storsimple-manage-volumes-u2.md#take-a-volume-offline) tootake hors connexion.
   
   > [!IMPORTANT]
   > Assurez-vous que vous avez effectué des volumes hello hors connexion sur l’ordinateur hôte de hello tout d’abord, avant de mettre hors connexion les volumes hello sur le périphérique de hello. Si vous ne prenez pas les volumes hello hors connexion sur l’ordinateur hôte de hello, il pourrait endommager toodata corruption.
   > 
   > 
4. Accédez arrière toohello **catalogue de sauvegarde** onglet et sélectionnez un jeu de sauvegarde.
5. Cliquez sur **restaurer** bas hello de page de hello.
6. Vous êtes invité à confirmer l’opération. Révision Bonjour restaurer les informations et puis sélectionnez la case à cocher de confirmation hello.
   
    ![Page Confirmation](./media/storsimple-restore-from-backup-set-u2/ConfirmRestore.png)
7. Cliquez sur une icône de coche hello ![icône de coche](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png). Un travail de restauration commence. Vous pouvez afficher le travail de hello en accédant à hello **travaux** page. 
8. Une fois la restauration de hello est terminée, vous pouvez vérifier que le contenu hello de vos volumes est remplacés par les volumes de sauvegarde de hello.

![Vidéo disponible](./media/storsimple-restore-from-backup-set-u2/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment vous pouvez utiliser hello clone et restaurer les fonctionnalités dans les fichiers de StorSimple toorecover supprimé, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="if-hello-restore-fails"></a>Si la restauration de hello échoue
Vous recevez une alerte si hello opération de restauration échoue pour une raison quelconque. Si cela se produit, actualisation hello liste de sauvegarde tooverify qui hello sauvegarde est toujours valide. Si la sauvegarde de hello est valide et que vous restaurez à partir du cloud de hello, puis des problèmes de connectivité peuvent être cause hello. 

toocomplete hello l’opération de restauration, prendre du volume hello hors connexion sur l’ordinateur hôte de hello et recommencez l’opération de restauration hello. Toutes les données de volume de toohello de modifications qui ont été effectuées au cours du processus de restauration hello sont perdues.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[StorSimple de gérer les volumes](storsimple-manage-volumes-u2.md).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

