---
title: aaaClone une sauvegarde StorSimple Virtual Array | Documents Microsoft
description: "Découvrez comment tooclone une sauvegarde et récupérer un fichier à partir de votre tableau virtuel StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a>Cloner à partir d’une sauvegarde de votre instance StorSimple Virtual Array

## <a name="overview"></a>Vue d'ensemble

Cet article explique étape par étape comment tooclone une jeu de sauvegarde de vos partages ou des volumes sur votre tableau de virtuel StorSimple Microsoft Azure. cloné Hello est toorecover utilisé un fichier supprimé ou perdu. Hello inclut également tooperform obtenir des instructions détaillées qu'une récupération au niveau élément sur votre tableau virtuel StorSimple configurée comme un serveur de fichiers.

## <a name="clone-shares-from-a-backup-set"></a>Cloner des partages à partir d’un jeu de sauvegarde

**Avant d’essayer des partages tooclone, assurez-vous d’avoir suffisamment d’espace sur hello appareil toocomplete cette opération.** tooclone à partir d’une sauvegarde, Bonjour [portail Azure](https://portal.azure.com/), effectuer hello comme suit.

#### <a name="tooclone-a-share"></a>tooclone un partage

1. Parcourir trop**périphériques** panneau. Sélectionnez et cliquez sur votre appareil, puis cliquez sur **Partages**. Sélectionnez le partage hello que vous souhaitez tooclone, hello partage tooinvoke hello menu contextuel. Sélectionnez **Cloner**.
   
   ![Cloner une sauvegarde](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. Bonjour **Clone** panneau, cliquez sur **sauvegarde > sélectionnez** et puis hello suivant : 
   
   a.    Filtrer une sauvegarde sur ce périphérique en fonction de la plage de temps hello. Vous pouvez choisir **7 derniers jours**, **30 derniers jours** ou **Dernière année**.
   
   b.    Dans liste de hello de sauvegardes filtrés affichés, sélectionnez une sauvegarde tooclone à partir de.
   
   c.    Cliquez sur **OK**.
   
   ![Cloner une sauvegarde](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. Bonjour **Clone** panneau, cliquez sur **cibler les paramètres** et puis hello suivant :
   
   a.    Nommez le partage. nom de partage Hello doit contenir 3 et 127 caractères.
   
   b.    Indiquez éventuellement une description pour le partage de cloné hello.
   
   c.    Vous ne pouvez pas modifier le type hello du partage hello que vous effectuez la restauration. Un partage à plusieurs niveaux est cloné comme un partage à plusieurs niveaux, et un partage épinglé localement comme un partage épinglé localement.
   
   d.    capacité de Hello est définie en tant que taille égale toohello du partage hello que vous effectuez un clonage à partir de.
   
   e.    Affecter des administrateurs hello pour ce partage. Vous serez en mesure de toomodify propriétés de partage hello via l’Explorateur de fichiers après que le clonage de hello est terminée.
   
   f.    Cliquez sur **OK**.
   
   ![Cloner une sauvegarde](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. Cliquez sur **Clone** toostart un travail de clonage. Une fois le travail de hello terminée, opération de clonage hello démarre et vous en êtes informé. progression de hello toomonitor de clone, accédez toohello **travaux** panneau, cliquez sur hello tooview travail Détails de la tâche.
5. Une fois hello clone est correctement créé, accédez à toohello arrière **partages** panneau sur votre appareil.
6. Vous pouvez maintenant afficher nouveau partage de hello cloné dans la liste hello des partages sur votre appareil. Un partage à plusieurs niveaux est cloné comme un partage à plusieurs niveaux, et un partage épinglé localement comme un partage épinglé localement.
   
   ![Cloner une sauvegarde](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a>Cloner des volumes à partir d’un jeu de sauvegarde

tooclone à partir d’une sauvegarde, Bonjour portail Azure, vous avez tooperform étapes toohello similaire ceux durant le clonage d’un partage. opération de clonage Hello clone hello tooa sauvegarde nouveau volume sur hello même périphérique virtuel ; Impossible de cloner tooa autre appareil.

#### <a name="tooclone-a-volume"></a>tooclone un volume

1. Parcourir trop**périphériques** panneau. Sélectionnez et cliquez sur votre appareil, puis cliquez sur **Volumes**. Sélectionner le volume hello que vous souhaitez tooclone, hello volume tooinvoke hello menu contextuel. Sélectionnez **Cloner**.
   
   ![Clonage d’un volume](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. Bonjour **Clone** panneau, cliquez sur **sauvegarde** et puis hello suivant : 
   
   a.    Filtrer une sauvegarde sur ce périphérique en fonction de la plage de temps hello. Vous pouvez choisir **7 derniers jours**, **30 derniers jours** ou **Dernière année**. 
   
   b.    Dans liste de hello de sauvegardes filtrés affichés, sélectionnez une sauvegarde tooclone à partir de.
   
   c.    Cliquez sur **OK**.
   
   ![Cloner une sauvegarde](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. Bonjour **Clone** panneau, cliquez sur **cibler les paramètres de volume** et puis hello suivant ::
   
   a. nom de l’appareil Hello est remplie automatiquement.
   
   b. Fournissez un nom de volume pour hello **cloner le volume**. nom de volume Hello doit contenir 3 caractères too127.
   
   c. type de volume Hello est défini automatiquement le volume d’origine de toohello. Un volume à plusieurs niveaux est cloné comme un partage à plusieurs niveaux, et un volume épinglé localement comme un volume épinglé localement.
   
   d. Pourquoi **connecté des ordinateurs hôtes**, cliquez sur **sélectionnez**.
   
   ![Cloner une sauvegarde](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. Bonjour **connecté des ordinateurs hôtes** panneau, sélectionnez à partir d’un ACR existant ou ajouter un nouvel ACR. tooadd un nouvel ACR, vous devez tooprovide un nom d’ACR et l’hôte hello IQN. Cliquez sur **Sélectionner**.
   
   ![Cloner une sauvegarde](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. Cliquez sur **Clone** toolaunch un travail de clonage.
   
   ![Cloner une sauvegarde](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. Une fois le travail de clonage hello est créé, le clonage démarre. Une fois le clone de hello est créé, il est affiché sur le panneau de Volumes hello sur votre appareil. Remarque : un volume à plusieurs niveaux est cloné comme un volume à plusieurs niveaux, et un volume épinglé localement comme un volume épinglé localement.
   
   ![Cloner une sauvegarde](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. Une fois que le volume de hello s’affiche en ligne sur liste hello des volumes, volume de hello est disponible pour utilisation. Sur l’hôte initiateur iSCSI hello actualiser la liste hello de cibles dans la fenêtre de propriétés d’initiateur iSCSI. Une nouvelle cible qui contient le nom de volume cloné hello doit apparaître comme « inactive » sous la colonne d’état hello.
8. Sélectionnez la cible de hello et cliquez sur **connexion**. Une fois l’initiateur de hello toohello connecté cible, état de hello doit également modifier**connecté**.
9. Bonjour **gestion des disques** fenêtre hello volumes montés s’affichent comme illustré hello après l’illustration. Cliquez sur hello découverts volume (cliquez sur le nom du disque hello), puis cliquez sur **Online**.

> [!IMPORTANT]
> Lorsque la tentative de tooclone un volume ou un partage à partir d’un jeu de sauvegarde, si le travail de clonage hello échoue, un volume cible ou un partage peut toujours être créé dans le portail de hello. Il est important que vous supprimez ce volume cible ou partagez dans toominimize de portail hello des problèmes futurs découlant de cet élément.
> 
> 

## <a name="item-level-recovery-ilr"></a>Récupération au niveau de l'élément (ILR)

Cette version introduit de récupération hello au niveau élément (ILR) sur un tableau virtuel StorSimple configuré comme un serveur de fichiers. fonctionnalité de Hello vous permet de toodo de récupération granulaire de fichiers et dossiers à partir d’une sauvegarde sur le cloud de tous les partages de hello sur l’appareil StorSimple hello. Grâce à un modèle en libre-service, vous pouvez récupérer des fichiers supprimés à partir de sauvegardes récentes.

Chaque partage possède un *.backups* dossier qui contient les sauvegardes les plus récentes hello. Vous pouvez naviguer de sauvegarde de votre choix toohello, copiez les fichiers appropriés et les dossiers à partir de la sauvegarde de hello et les restaurer. Cette fonctionnalité élimine tooadministrators d’appels de restauration de fichiers à partir de sauvegardes.

1. Lorsque vous effectuez hello au niveau élément, vous pouvez afficher les sauvegardes hello via l’Explorateur de fichiers. Cliquez sur Partage spécifique hello toolook lors de la sauvegarde hello pour souhaitées. Vous verrez un *.backups* dossier créé sous le partage hello qui stocke toutes les sauvegardes hello. Développez hello *.backups* sauvegardes de dossier tooview hello. dossier de Hello montre la vue éclatée hello de hiérarchie de la sauvegarde entière hello. Cette vue est créée à la demande et ne prend que quelques secondes toocreate.
   
   sauvegardes de cinq derniers Hello sont affichés de cette façon et peuvent être utilisé tooperform un niveau de l’élément de récupération. Hello cinq sauvegardes récentes comprennent hello planifiée par défaut et hello sauvegardes manuelles.
   
   * **Sauvegardes planifiées** nommées &lt;Nom de l’appareil&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC.
   * **Sauvegardes manuelles** nommées Ad-hoc-YYYYMMDD-HHMMSS-UTC.
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. Identifier la sauvegarde de hello contenant la version la plus récente du fichier de hello supprimé hello. Bien que le nom du dossier hello contient un horodatage UTC dans chacune des hello précédant le cas, les temps de hello à quels hello dossier a été créé est temps de périphérique réel de hello lorsque hello sauvegarde a démarré. Utilisez hello dossier timestamp toolocate et identifiez les sauvegardes hello.

3. Recherchez le dossier de hello ou hello fichier toorestore dans sauvegarde hello que vous avez identifié à l’étape précédente de hello. Notez que vous pouvez afficher uniquement les fichiers de hello ou dossiers que vous disposez d’autorisations. Si vous ne pouvez pas accéder à certains fichiers ou dossiers, contactez un administrateur de partage. administrateur de Hello peut utiliser des autorisations de partage de l’Explorateur de fichiers tooedit hello et vous donnent accès toohello fichier ou dossier spécifique. Il est recommandé que hello partage administrateur est un groupe d’utilisateurs au lieu d’un seul utilisateur.

4. Copiez les fichiers hello ou partage approprié toohello dossier hello sur votre serveur de fichiers StorSimple.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur la façon trop[administrer votre tableau virtuel StorSimple à l’aide de l’interface utilisateur de web local hello](storsimple-ova-web-ui-admin.md).

