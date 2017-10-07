---
title: "données aaaRestore dans Azure tooa Windows Server ou ordinateur Windows | Documents Microsoft"
description: "Découvrez comment les données de toorestore stockées dans Azure tooa Windows Server ou de l’ordinateur Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a>Restaurer des fichiers tooa Windows server ou la machine du client Windows à l’aide du modèle de déploiement de gestionnaire de ressources
> [!div class="op_single_selector"]
> * [Portail Azure](backup-azure-restore-windows-server.md)
> * [Portail classique](backup-azure-restore-windows-server-classic.md)
>
>

Cet article explique comment toorestore des données à partir d’un coffre de sauvegarde. toorestore des données, vous utilisez hello récupérer les données Assistant agent de Microsoft Azure Recovery Services (MARS) hello. Lorsque vous restaurez des données, il est possible de :

* Restauration de données toohello est identique à l’ordinateur à partir de laquelle les sauvegardes hello ont été effectuées.
* Restaurer un ordinateur autre tooan de données.

En janvier 2017, Microsoft a publié un agent de MARS toohello aperçu mise à jour. Ainsi que des correctifs de bogues, cette mise à jour Active la restauration instantanée, ce qui vous permet de toomount un instantané de point de récupération accessible en écriture comme un volume de reprise. Vous pouvez ensuite Explorer hello récupération volume et copie les fichiers tooa ordinateur local ainsi sélectivement restauration de fichiers.

> [!NOTE]
> Hello [janvier 2017 mise à jour d’Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) est requis si vous voulez toouse restauration instantanée toorestore données. Les données de sauvegarde hello doivent également être protégées dans des coffres dans les paramètres régionaux répertoriés dans l’article du support technique hello. Consultez hello [janvier 2017 mise à jour d’Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) pour hello dernière liste des paramètres régionaux qui prennent en charge la restauration instantanée. La restauration instantanée n’est actuellement **pas** disponible dans tous les pays.
>

Restauration instantanée est disponible pour utilisation dans les Services de récupération des coffres Bonjour portail Azure et les coffres de sauvegarde dans le portail classique de hello. Si vous souhaitez toouse restauration instantanée, téléchargez la mise à jour de MARS hello et suivez les procédures de hello mentionnant restauration instantanée.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a>Utiliser la restauration instantanée toohello de données toorecover même ordinateur

Si vous avez supprimé accidentellement une toorestore de fichier et qui souhaitent il toohello étapes de la même machine (à partir de quels hello est la sauvegarde), hello suivant vous permettra de récupérer les données de salutation.

1. Ouvrez hello **Microsoft Azure Backup** snap dans. Si vous ne savez pas où le composant logiciel enfichable hello a été installé, recherchez hello ordinateur ou un serveur pour **Microsoft Azure Backup**.

    application de bureau Hello doit apparaître dans les résultats de la recherche hello.

2. Cliquez sur **récupérer les données** Assistant de hello toostart.

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

3. Sur hello **mise en route** volet, toorestore hello données toohello même serveur ou ordinateur, sélectionnez **ce serveur (`<server name>`)** et cliquez sur **suivant**.

    ![Choisissez cette toohello de données de serveur option toorestore hello même ordinateur](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. Sur hello **sélectionner le Mode de récupération** volet, choisissez **fichiers et dossiers individuels** puis cliquez sur **suivant**.

    ![Parcourir les fichiers](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. Sur hello **sélectionner le Volume et la Date** volet, volume hello select qui contient les fichiers hello et/ou les dossiers que vous souhaitez toorestore.

    Dans le calendrier de hello, sélectionnez un point de récupération. Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps. Les dates dans **gras** indiquer la disponibilité de hello d’au moins un point de récupération. Une fois que vous sélectionnez une date, si plusieurs points de récupération sont disponibles, choisissez le point de récupération spécifique hello dans hello **temps** menu déroulant.

    ![Volume et date](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. Une fois que vous avez choisi toorestore de point de récupération hello, cliquez sur **monter**.

    Sauvegarde Azure monte le point de récupération locaux hello et l’utilise comme un volume de reprise.

7. Sur hello **Parcourir et restaurer des fichiers** volet, cliquez sur **Parcourir** tooopen l’Explorateur Windows et hello rechercher des fichiers et dossiers que vous souhaitez.

    ![Options de récupération](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. Dans l’Explorateur Windows, hello copier les fichiers et/ou dossiers souhaité toorestore et les coller tooany emplacement local toohello serveur ou l’ordinateur. Vous pouvez ouvrir ou diffuser des fichiers hello directement à partir de volume de récupération hello et vérifiez hello correct versions sont récupérées.

    ![Copiez et collez les fichiers et dossiers à partir de l’emplacement du volume monté toolocal](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. Quand vous avez terminé de restauration des fichiers de hello et/ou des dossiers, sur hello **Parcourir et les fichiers de récupération** volet, cliquez sur **démontage**. Puis cliquez sur **Oui** tooconfirm que vous souhaitez le volume de hello toounmount.

    ![Démontez le volume de hello et confirmer](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > Si vous ne cliquez pas sur les démonter, hello récupération Volume restera monté pendant 6 heures à partir de l’heure hello lorsqu’elle a été montée. Toutefois, le temps de montage hello est étendue jusqu'à un maximum de 24 heures en cas d’une copie de fichier en cours. Aucune opération de sauvegarde ne s’exécuteront pendant que hello volume est monté. N’importe quel toorun de l’opération de sauvegarde planifiée pendant les temps de hello lorsque le volume de hello est monté, s’exécute une fois que le volume de récupération hello est déchargé.
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a>Utiliser la restauration instantanée toorestore données tooan autre ordinateur
Si l’intégralité du serveur est perdu, vous pouvez toujours récupérer des données à partir d’ordinateurs différents du tooa Azure Backup. Hello suit illustre des flux de travail hello.


terminologie Hello utilisée dans cette procédure inclut :

* *Ordinateur source* : ordinateur d’origine hello quelle sauvegarde hello a été effectuée et qui est actuellement indisponible.
* *Ordinateur cible* – hello machine toowhich hello données sont récupérées.
* *Archivage de l’exemple* – Bonjour Recovery Services coffre toowhich Bonjour *machine Source* et *de l’ordinateur cible* sont enregistrés. <br/>

> [!NOTE]
> Les sauvegardes ne peut pas être restaurée tooa machine de cible exécute une version antérieure du système d’exploitation de hello. Par exemple, une sauvegarde effectuée à partir d’un ordinateur Windows 7 ne peut pas être restaurée sur un ordinateur sous Windows 8 ou une version ultérieure. Une sauvegarde effectuée à partir d’un ordinateur Windows 8 ne peut pas être restaurée tooa Windows 7 ordinateur.
>
>

1. Ouvrez hello **Microsoft Azure Backup** dans l’alignement sur hello *de l’ordinateur cible*.

2. Assurez-vous de hello *de l’ordinateur cible* et hello *machine Source* sont toohello des Services de récupération même coffre.

3. Cliquez sur **récupérer les données** tooopen hello **Assistant de récupération des données**.

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

4. Sur hello **mise en route** volet, sélectionnez **un autre serveur**

    ![Un autre serveur](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. Fournissez le fichier d’informations d’identification de coffre hello correspondant toohello *coffre d’exemple*, puis cliquez sur **suivant**.

    Si le fichier d’informations d’identification de coffre hello est non valide (ou a expiré), téléchargez un nouveau fichier d’informations d’identification de coffre à partir de hello *coffre d’exemple* Bonjour portail Azure. Une fois que vous fournissez une information d’identification de coffre valide, le nom hello Hello correspondant du coffre de sauvegarde s’affiche.


6. Sur hello **sélectionner le serveur de sauvegarde** volet, sélectionnez hello *machine Source* à partir de la liste hello d’ordinateurs affichés et fournir le mot de passe hello. Cliquez ensuite sur **Suivant**.

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. Sur hello **sélectionner le Mode de récupération** volet, sélectionnez **fichiers et dossiers individuels** et cliquez sur **suivant**.

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. Sur hello **sélectionner le Volume et la Date** volet, volume hello select qui contient les fichiers hello et/ou les dossiers que vous souhaitez toorestore.

    Dans le calendrier de hello, sélectionnez un point de récupération. Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps. Les dates dans **gras** indiquer la disponibilité de hello d’au moins un point de récupération. Une fois que vous sélectionnez une date, si plusieurs points de récupération sont disponibles, choisissez le point de récupération spécifique hello dans hello **temps** menu déroulant.

    ![Éléments de recherche](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. Cliquez sur **de montage** point de récupération toolocally montage hello comme un volume de récupération sur votre *de l’ordinateur cible*.

10. Sur hello **Parcourir et restaurer des fichiers** volet, cliquez sur **Parcourir** tooopen l’Explorateur Windows et hello rechercher des fichiers et dossiers que vous souhaitez.

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. Dans l’Explorateur Windows, copiez hello fichiers et/ou dossiers à partir du volume de reprise hello et collez-les tooyour *de l’ordinateur cible* emplacement. Vous pouvez ouvrir ou diffuser des fichiers hello directement à partir de volume de récupération hello et vérifiez hello correct versions sont récupérées.

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. Quand vous avez terminé de restauration des fichiers de hello et/ou des dossiers, sur hello **Parcourir et les fichiers de récupération** volet, cliquez sur **démontage**. Puis cliquez sur **Oui** tooconfirm que vous souhaitez le volume de hello toounmount.

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > Si vous ne cliquez pas sur les démonter, hello récupération Volume restera monté pendant 6 heures à partir de l’heure hello lorsqu’elle a été montée. Toutefois, le temps de montage hello est étendue jusqu'à un maximum de 24 heures en cas d’une copie de fichier en cours. Aucune opération de sauvegarde ne s’exécuteront pendant que hello volume est monté. N’importe quel toorun de l’opération de sauvegarde planifiée pendant les temps de hello lorsque le volume de hello est monté, s’exécute une fois que le volume de récupération hello est déchargé.
    >

## <a name="troubleshooting"></a>Résolution des problèmes
Si Azure Backup n’est pas monté correctement reconstitution hello même après plusieurs minutes, d’un clic sur **de montage** ou le volume de reprise toomount hello échoue avec une ou plusieurs erreurs, suivez les étapes de hello ci-dessous toobegin récupération normalement.

1.  Annuler le processus de montage en cours de hello au cas où il a été exécuté pendant plusieurs minutes.

2.  Vérifiez que vous êtes sur la version la plus récente de l’agent de sauvegarde Azure hello hello. toofind des informations de version hello d’Azure Backup agent, cliquez sur **sur Microsoft Azure Recovery Services Agent** sur hello **Actions** volet de Microsoft Azure Backup de la console et vérifiez que hello  **Version** nombre est égal tooor ultérieure à la version de hello mentionnée dans [cet article](https://go.microsoft.com/fwlink/?linkid=229525). Vous pouvez télécharger la version la plus récente à partir de hello [ici](https://go.microsoft.com/fwLink/?LinkID=288905)

3.  Accédez trop**le Gestionnaire de périphériques** -> **contrôleurs de stockage** et assurez-vous que vous pouvez localiser **initiateur Microsoft iSCSI**. Si vous pouvez le localiser, accéder directement toostep 7 ci-dessous. 

4.  Si vous ne trouvez pas le service Microsoft iSCSI Initiator comme indiqué à l’étape 3, vérifiez toosee si vous pouvez trouver une entrée sous **le Gestionnaire de périphériques** -> **contrôleurs de stockage** appelée  **APPAREIL inconnu** avec l’ID de matériel **ROOT\ISCSIPRT**.

5.  Cliquez avec le bouton droit sur l’entrée **Appareil inconnu** et sélectionnez **Mettre à jour le pilote**.

6.  Pilote hello de mise à jour par l’option hello trop **rechercher automatiquement un pilote mis à jour**. Fin de la mise à jour hello doit modifier **périphérique inconnu** trop**initiateur Microsoft iSCSI** comme indiqué ci-dessous. 

    ![Chiffrement](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  Accédez trop**le Gestionnaire des tâches** -> **Services (Local)** -> **Service initiateur Microsoft iSCSI**. 

    ![Chiffrement](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  Redémarrez le service de Microsoft iSCSI Initiator hello en cliquant sur service hello, en cliquant sur **arrêter** et à nouveau le bouton droit et en cliquant sur **Démarrer**.

9.  Recommencez la récupération à l’aide de la restauration instantanée. 

Si la récupération de hello échoue encore, redémarrez votre serveur/client. Si un redémarrage n’est pas souhaitable ou récupération de hello persiste même après le redémarrage du serveur de hello, essayez de récupérer à partir d’un autre ordinateur et contactez le Support de Azure en accédant trop[portail Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) et soumettre une demande de support.

## <a name="next-steps"></a>Étapes suivantes
* Maintenant que vous avez restauré vos fichiers et vos dossiers, vous pouvez [gérer vos sauvegardes](backup-azure-manage-windows-server.md).
