---
title: "aaaRestore données tooa Windows Server ou Client Windows à partir d’Azure à l’aide hello modèle de déploiement classique | Documents Microsoft"
description: "Découvrez comment toorestore à partir de Windows Server ou Windows Client."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a>Restaurer des fichiers tooa Windows server ou la machine du client Windows à l’aide du modèle de déploiement classique de hello
> [!div class="op_single_selector"]
> * [Portail classique](backup-azure-restore-windows-server-classic.md)
> * [Portail Azure](backup-azure-restore-windows-server.md)
>
>

Cet article explique comment les données de toorecover à partir d’une sauvegarde de coffre et restaurer tooa serveur ou l’ordinateur. À partir de mars 2017, vous pouvez créer n’est plus des coffres de sauvegarde dans le portail classique de hello.

> [!IMPORTANT]
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> **Le 15 octobre 2017**, vous ne pourra plus être coffres de sauvegarde toocreate toouse en mesure de PowerShell. <br/> **À compter du 1er novembre 2017** :
>- Les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>

toorestore des données, vous utilisez hello récupérer les données Assistant agent de Microsoft Azure Recovery Services (MARS) hello. Lorsque vous restaurez des données, il est possible de :

* Restauration de données toohello est identique à l’ordinateur à partir de laquelle les sauvegardes hello ont été effectuées.
* Restaurer un ordinateur autre tooan de données.

En janvier 2017, Microsoft a publié un agent de MARS toohello aperçu mise à jour. Ainsi que des correctifs de bogues, cette mise à jour Active la restauration instantanée, ce qui vous permet de toomount un instantané de point de récupération accessible en écriture comme un volume de reprise. Vous pouvez ensuite Explorer hello récupération volume et copie les fichiers tooa ordinateur local ainsi sélectivement restauration de fichiers.

> [!NOTE]
> Hello [janvier 2017 mise à jour d’Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) est requis si vous voulez toouse restauration instantanée toorestore données. Les données de sauvegarde hello doivent également être protégées dans des coffres dans les paramètres régionaux répertoriés dans l’article du support technique hello. Consultez hello [janvier 2017 mise à jour d’Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) pour hello dernière liste des paramètres régionaux qui prennent en charge la restauration instantanée. La restauration instantanée n’est actuellement **pas** disponible dans tous les pays.
>

Restauration instantanée est disponible pour utilisation dans les Services de récupération des coffres Bonjour portail Azure et les coffres de sauvegarde dans le portail classique de hello. Si vous souhaitez toouse restauration instantanée, téléchargez la mise à jour de MARS hello et suivez les procédures de hello mentionnant restauration instantanée.


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
    > Si vous ne cliquez pas sur les démonter, hello récupération Volume restera monté pour six heures après hello lorsqu’elle a été montée. Aucune opération de sauvegarde ne s’exécuteront pendant que hello volume est monté. N’importe quel toorun de l’opération de sauvegarde planifiée pendant les temps de hello lorsque le volume de hello est monté, s’exécute une fois que le volume de récupération hello est déchargé.
    >


## <a name="recover-data-toohello-same-machine"></a>Récupérer des données toohello même ordinateur
Si vous avez supprimé accidentellement une toorestore de fichier et qui souhaitent il toohello étapes de la même machine (à partir de quels hello est la sauvegarde), hello suivant vous permettra de récupérer les données de salutation.

1. Ouvrez hello **Microsoft Azure Backup** snap dans.
2. Cliquez sur **récupérer les données** flux de travail tooinitiate hello.

    ![Récupérer des données](./media/backup-azure-restore-windows-server-classic/recover.png)
3. Sélectionnez hello  **ce serveur (*Nom_de_votre_ordinateur*) ** hello de toorestore option fichier sauvegardé sur hello même ordinateur.

    ![Même ordinateur](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. Choisissez trop**parcourir vos fichiers** ou **recherche des fichiers**.

    Laissez option par défaut de hello si vous envisagez de toorestore un ou plusieurs fichiers dont le chemin est connu. Si vous n’êtes pas sûr à propos de la structure de dossiers hello mais que vous aimeriez toosearch pour un fichier, choisissez hello **recherche des fichiers** option. Pour les besoins de hello de cette section, nous continuerons avec l’option par défaut de hello.

    ![Parcourir les fichiers](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. Sélectionnez un volume hello à partir de laquelle vous souhaitez fichier hello de toorestore.

    Vous pouvez restaurer le fichier à partir de n’importe quel point dans le temps. Les dates qui apparaissent dans **gras** dans le contrôle de calendrier hello indiquer la disponibilité de hello d’un point de restauration. Une fois qu’une date est sélectionnée, en fonction de votre planification de sauvegarde (et réussite hello d’une opération de sauvegarde), vous pouvez sélectionner un point dans le temps de hello **temps** liste déroulante.

    ![Volume et date](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. Sélectionnez hello éléments toorecover. Vous pouvez sélections plusieurs dossiers/fichiers toorestore.

    ![Sélectionner des fichiers](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. Spécifiez des paramètres de récupération hello.

    ![Options de récupération](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * Vous avez la possibilité de restaurer l’emplacement d’origine de toohello (les Bonjour fichier/dossier serait remplacé) ou tooanother Bonjour même ordinateur.
   * Si hello fichier/dossier que vous souhaitez toorestore existe dans l’emplacement cible de hello, vous pouvez créer des copies (deux versions de hello même fichier), remplacer les fichiers hello dans l’emplacement cible de hello ou ignorer des fichiers hello qui existe dans la cible de hello hello.
   * Il est fortement recommandé que vous laissez l’option par défaut hello restauration des ACL hello sur les fichiers hello qui sont en cours de récupération.
8. Une fois ces entrées fournies, cliquez sur **Suivant**. workflow de récupération Hello, qui restaure l’ordinateur de toothis fichiers hello, commencera.

## <a name="recover-tooan-alternate-machine"></a>Récupérer tooan un autre ordinateur
Si l’intégralité du serveur est perdu, vous pouvez toujours récupérer des données à partir d’ordinateurs différents du tooa Azure Backup. Hello suit illustre des flux de travail hello.  

terminologie Hello utilisée dans cette procédure inclut :

* *Ordinateur source* : ordinateur d’origine hello quelle sauvegarde hello a été effectuée et qui est actuellement indisponible.
* *Ordinateur cible* – hello machine toowhich hello données sont récupérées.
* *Archivage de l’exemple* – hello de toowhich de coffre de sauvegarde hello *machine Source* et *de l’ordinateur cible* sont enregistrés. <br/>

> [!NOTE]
> Les sauvegardes effectuées à partir d’un ordinateur ne peut pas être restaurées sur un ordinateur qui exécute une version antérieure du système d’exploitation de hello. Par exemple, si les sauvegardes sont effectuées à partir d’un ordinateur Windows 7, elles peuvent être restaurées sur un ordinateur Windows 8 ou supérieur. Toutefois, inversement hello n’est pas vraie.
>
>

1. Ouvrez hello **Microsoft Azure Backup** dans l’alignement sur hello *de l’ordinateur cible*.
2. Vérifiez que hello *de l’ordinateur cible* et hello *machine Source* sont inscrit toohello même archivage de sauvegarde.
3. Cliquez sur **récupérer les données** flux de travail tooinitiate hello.

    ![Récupérer des données](./media/backup-azure-restore-windows-server-classic/recover.png)
4. Sélectionnez **Un autre serveur**

    ![Un autre serveur](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. Fournissez le fichier d’informations d’identification de coffre hello correspondant toohello *coffre d’exemple*. Si le fichier d’informations d’identification de coffre hello est non valide (ou a expiré) Télécharger un nouveau fichier d’informations d’identification de coffre à partir de hello *coffre d’exemple* Bonjour portail Azure classic. Une fois que le fichier d’informations d’identification de coffre hello est fourni, le coffre de sauvegarde hello sur le fichier d’informations d’identification de coffre hello s’affiche.
6. Sélectionnez hello *machine Source* à partir de la liste hello des ordinateurs affichés.

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. Sélectionnez soit hello **recherche des fichiers** ou **parcourir vos fichiers** option. Pour les besoins de hello de cette section, nous allons utiliser hello **recherche des fichiers** option.

    ![Search](./media/backup-azure-restore-windows-server-classic/search.png)
8. Sélectionnez hello volume et la date dans l’écran suivant de hello. Recherche de nom de dossier ou fichier hello souhaité toorestore.

    ![Éléments de recherche](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. Sélectionnez emplacement hello où les fichiers de hello doivent toobe restaurée.

    ![Emplacement de restauration](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. Fournir hello phrase secrète de chiffrement qui a été fourni au cours de *l’ordinateur Source* inscription trop*coffre d’exemple*.

    ![Chiffrement](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. Une fois l’entrée hello est fournie, cliquez sur **récupérer**, les déclencheurs hello restauration Hello sauvegardé des fichiers toohello destination fournie.

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
    > Si vous ne cliquez pas sur les démonter, hello récupération Volume restera monté pour six heures après hello lorsqu’elle a été montée. Aucune opération de sauvegarde ne s’exécuteront pendant que hello volume est monté. N’importe quel toorun de l’opération de sauvegarde planifiée pendant les temps de hello lorsque le volume de hello est monté, s’exécute une fois que le volume de récupération hello est déchargé.
    >


## <a name="next-steps"></a>Étapes suivantes
* [Azure Backup - Forum Aux Questions](backup-azure-backup-faq.md)
* Visitez hello [Forum de sauvegarde Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).

## <a name="learn-more"></a>En savoir plus
* [Vue d’ensemble d’Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [Sauvegarde des machines virtuelles Azure](backup-azure-vms-introduction.md)
* [Sauvegarde des charges de travail Microsoft](backup-azure-dpm-introduction.md)
