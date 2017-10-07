---
title: "aaaRecover des données à partir d’un serveur de sauvegarde Azure | Documents Microsoft"
description: "Récupérer des données hello que vous avez protégé des Services de récupération tooa coffre dans n’importe quel coffre toothat inscrit de Azure Backup Server."
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 74847880e646c3c4f198afe318f1db30363d137a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-data-from-azure-backup-server"></a>Récupérer des données depuis Azure Backup Server
Vous pouvez utiliser les données de salutation toorecover Azure Backup Server que vous avez sauvegardé tooa de coffre Recovery Services. processus Hello pour cette opération donc est intégré dans la console de gestion de serveur de sauvegarde Azure hello et est le workflow de récupération toohello similaire pour d’autres composants Azure Backup.

> [!NOTE]
> Cet article s’applique pour [System Center Data Protection Manager 2012 R2 UR7 ou version ultérieure] (https://support.microsoft.com/en-us/kb/3065246), combinée avec hello [dernier agent Azure Backup](http://aka.ms/azurebackup_agent).
>
>

toorecover des données à partir d’un serveur de sauvegarde Azure :

1. À partir de hello **récupération** onglet Hello console de gestion de serveur de sauvegarde Azure, cliquez sur **'Ajouter un DPM externe'** (à hello haut à gauche de l’écran hello).   
    ![Ajouter un serveur DPM externe](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)
2. Téléchargement de nouvelles **informations d’identification de coffre** du coffre hello associé hello **Azure Backup Server** où les données de salutation sont en cours de récupération, choisissez hello Azure Backup Server à partir de la liste de hello de serveurs de sauvegarde Azure enregistré avec le coffre Recovery Services hello et fournir hello **phrase secrète de chiffrement** associé avec le serveur hello dont les données en cours de récupération.

    ![Informations d'identification d’un serveur DPM externe](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > Serveurs de sauvegarde Azure associé même hello coffre d’inscription peut récupérer des données de l’autre.
   >
   >

    Une fois que hello externes Azure Backup Server est correctement ajouté, vous pouvez parcourir les données de hello du serveur externe de hello et hello Azure Backup Server local à partir de hello **récupération** onglet.
3. Parcourir hello liste protégés par les serveurs de production hello externes Azure Backup Server et sélectionnez la source de données appropriée hello.

    ![Parcourir un serveur DPM externe](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. Sélectionnez **hello mois et année** de hello **points de récupération** liste déroulante, sélectionnez hello requis **la date de récupération** pour lorsque point de récupération hello a été créé, puis sélectionnez hello **Temps de récupération**.

    Une liste des fichiers et dossiers s’affiche dans le volet inférieur de hello, qui peut être exploré et récupérée tooany emplacement.

    ![Points de récupération d’un serveur DPM externe](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. Avec le bouton droit sur l’élément approprié de hello puis cliquez sur **récupérer**.

    ![Récupération d’un serveur DPM externe](./media/backup-azure-alternate-dpm-server/recover.png)
6. Hello de révision **récupérer une sélection**. Vérifiez les données de salutation et de temps de copie de sauvegarde hello en cours de récupération, ainsi que de source de hello à partir duquel la copie de sauvegarde hello a été créé. Si la sélection de hello est incorrecte, cliquez sur **Annuler** point de récupération approprié tooselect toonavigate toorecovery arrière de l’onglet. Si la sélection de hello est correcte, cliquez sur **suivant**.

    ![Résumé de la récupération d’un serveur DPM externe](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. Sélectionnez **tooan autre emplacement de récupération**. **Parcourir** toohello bon emplacement pour la récupération de hello.

    ![Emplacement de remplacement de la récupération d’un serveur DPM externe](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. Choisissez l’option hello liée trop**créer une copie**, **ignorer**, ou **remplacer**.

   * **Créer une copie** -crée une copie du fichier de hello s’il existe un conflit de noms.
   * **Ignorer** - s’il existe un conflit de noms, ne récupère pas de fichier hello qui laisse le fichier d’origine de hello.
   * **Remplacer** - s’il existe un conflit de noms, remplace la copie du fichier de hello hello.

     Choisissez option appropriée de hello trop**restaurer la sécurité**. Vous pouvez appliquer des paramètres de sécurité de hello hello ordinateur de destination où les données de salutation sont en cours de récupération ou les paramètres de sécurité hello qui étaient tooproduct applicable au moment de hello point de récupération hello a été créé.

     Identifier si un **Notification** est envoyée, une fois la récupération de hello terminée avec succès.

     ![Notifications de la récupération d’un serveur DPM externe](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. Hello **Résumé** écran répertorie les options de hello choisies jusqu'à présent. Une fois que vous cliquez sur **'Récupérer'**, les données de salutation sont récupérée toohello local approprié emplacement.

    ![Résumé des options de la récupération d’un serveur DPM externe](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > tâche de récupération Hello peut être surveillée dans hello **analyse** onglet Hello Azure Backup Server.
   >
   >

    ![Surveillance de la récupération](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. Vous pouvez cliquer sur **clair DPM externe** sur hello **récupération** onglet Hello vue hello tooremove du serveur DPM du serveur DPM externe de hello.

    ![Effacer un serveur DPM externe](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a>Dépannage des messages d'erreur
| Non. | Message d’erreur | Étapes de dépannage |
|:---:|:--- |:--- |
| 1. |Ce serveur n’est pas toohello inscrit le coffre spécifié par les informations d’identification de coffre hello. |**Cause :** cette erreur s’affiche lorsque le fichier d’informations d’identification de coffre hello sélectionné n’appartient pas toohello de coffre Recovery Services associé à Azure Backup Server sur le hello de la tentative de récupération. <br> **Résolution :** fichier d’informations d’identification téléchargement hello coffre à partir de hello de toowhich hello Recovery Services coffre Azure Backup Server est inscrit. |
| 2. |Soit les données récupérables hello ne seront pas disponibles ou le serveur sélectionné de hello n’est pas un serveur DPM. |**Cause :** il n’y aucun autres serveurs de sauvegarde Azure toohello inscrits coffre Recovery Services, ou les serveurs hello n’ont pas encore téléchargé les métadonnées hello serveur sélectionné de hello n’est pas un serveur de sauvegarde Azure (également appelé Windows Server ou Windows Client). <br> **Résolution :** s’il existe des autres coffre Recovery Services de toohello des serveurs de sauvegarde Azure, assurez-vous que l’agent Azure Backup de hello plus récente est installé. <br>S’il existe des autres coffre Recovery Services de toohello des serveurs de sauvegarde Azure, attendez un jour après le processus de récupération d’installation toostart hello. la tâche nocturne Hello téléchargera hello des métadonnées pour tous les toocloud de sauvegardes hello protégé. les données de salutation sera disponibles pour la récupération. |
| 3. |Aucun autre serveur DPM n’est inscrit toothis coffre. |**Cause :** aucun autre serveur de sauvegarde de Azure sont coffre toohello inscrits à partir de quels hello récupération est en cours.<br>**Résolution :** s’il existe des autres coffre Recovery Services de toohello des serveurs de sauvegarde Azure, assurez-vous que l’agent Azure Backup de hello plus récente est installé.<br>S’il existe des autres coffre Recovery Services de toohello des serveurs de sauvegarde Azure, attendez un jour après le processus de récupération d’installation toostart hello. la tâche nocturne Hello télécharge les métadonnées hello pour toutes les sauvegardes protégé toocloud. les données de salutation sera disponibles pour la récupération. |
| 4. |phrase secrète de chiffrement Hello ne correspond pas au mot de passe associé hello suivant du serveur :**<server name>** |**Cause :** hello phrase secrète de chiffrement utilisé dans les processus hello de chiffrement des données hello à partir des données du serveur de sauvegarde Azure hello sont en cours de récupération ne correspond pas à la phrase secrète de chiffrement hello. l’agent de Hello donnée toodecrypt Impossible hello. Par conséquent, la récupération de hello échoue.<br>**Résolution :** fournissez hello exacte même phrase secrète de chiffrement associée hello Azure Backup Server dont les données en cours de récupération. |

## <a name="frequently-asked-questions"></a>Forum Aux Questions

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a>Pourquoi ne puis-je pas ajouter un serveur DPM externe après avoir installé UR7 et le dernier agent Azure Backup ?

Hello serveurs DPM avec les sources de données qui sont protégés par toohello cloud (en utilisant une mise à jour cumulative antérieure à mettre à jour le correctif cumulatif 7), vous devez attendre au moins un jour après l’installation hello UR7 et agent Azure Backup plus récent, toostart **serveur d’ajouter un DPM externe** . Hello un jour période est tooupload nécessaires des métadonnées de hello de tooAzure de groupes de protection de DPM hello. Les métadonnées de groupe de protection sont téléchargées hello la première fois une tâche nocturne.

### <a name="what-is-hello-minimum-version-of-hello-microsoft-azure-recovery-services-agent-needed"></a>Qu’est la version minimale de hello de l’agent de Microsoft Azure Recovery Services hello nécessité ?

version minimale de Hello de hello Microsoft Azure Recovery Services agent ou l’agent Azure Backup, requis tooenable cette fonctionnalité est 2.0.8719.0.  version de l’agent tooview hello : ouvrez le panneau de configuration  **>**  tous les éléments  **>**  programmes et fonctionnalités  **>**  Microsoft Azure Recovery Services Agent. Version de hello est inférieur à 2.0.8719.0, téléchargez et installez hello [dernier agent Azure Backup](https://go.microsoft.com/fwLink/?LinkID=288905).

![Effacer un serveur DPM externe](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a>Étapes suivantes :
•    [Sauvegarde Azure - FAQ](backup-azure-backup-faq.md)
