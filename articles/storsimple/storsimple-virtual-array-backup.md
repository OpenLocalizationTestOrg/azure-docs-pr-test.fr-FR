---
title: didacticiel de sauvegarde Azure StorSimple Virtual Array aaaMicrosoft | Documents Microsoft
description: "Décrit comment tooback des StorSimple Virtual Array et les volumes."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a>Sauvegarde de partages ou de volumes sur votre StorSimple Virtual Array

## <a name="overview"></a>Vue d'ensemble

Hello StorSimple Virtual Array est un hybride cloud stockage local périphérique virtuel qui peut être configuré comme un serveur de fichiers ou un serveur iSCSI. unité de stockage virtuelle Hello permet hello utilisateur toocreate des sauvegardes planifiées et manuelles de tous les partages de hello ou volumes sur l’appareil de hello. Configuré comme serveur de fichiers, il permet également la récupération au niveau de l’élément. Ce didacticiel décrit comment toocreate planifiées et sauvegardes manuelles et effectuer la récupération au niveau élément toorestore un fichier supprimé sur votre tableau virtuel.

Ce didacticiel s’applique toohello StorSimple tableaux virtuels uniquement. Pour plus d’informations sur la 8000 série, accédez trop[créer une sauvegarde pour appareil de 8000 série](storsimple-manage-backup-policies-u2.md)

## <a name="back-up-shares-and-volumes"></a>Sauvegarder des partages et des volumes

Les sauvegardes fournissent une protection jusqu’à une date et une heure, et optimisent la récupération tout en réduisant les délais de restauration pour les partages et les sauvegardes. Vous pouvez sauvegarder un partage ou un volume sur votre appareil StorSimple de deux manières : **planifiée** ou **manuelle**. Chacune des méthodes de hello est expliqué dans les sections suivantes de hello.

## <a name="change-hello-backup-start-time"></a>Modifier l’heure de début de la sauvegarde hello

> [!NOTE]
> Dans cette version, les sauvegardes planifiées sont créés par une stratégie par défaut qui s’exécute tous les jours à une heure spécifiée et la sauvegarde de tous les partages de hello ou volumes sur l’appareil de hello. Il n’est pas possible de toocreate des stratégies personnalisées pour les sauvegardes planifiées pour l’instant.


Votre StorSimple Virtual Array a une stratégie de sauvegarde par défaut qui commence à une heure spécifiée (22:30) et sauvegarde toutes les hello partages ou volumes sur l’appareil de hello une fois par jour. Vous pouvez modifier le temps de hello auxquelles démarrage de la sauvegarde hello, mais les fréquences de hello et hello rétention (qui spécifie le nombre de hello de sauvegardes tooretain) ne peut pas être modifiée. Au cours de ces sauvegardes, un appareil virtuel entier hello est sauvegardé. Cela pourrait potentiellement hello les performances du périphérique de hello et affecter des charges de travail hello déployés sur le périphérique de hello. Par conséquent, nous vous recommandons de planifier ces sauvegardes pendant les heures creuses.

 heure de début de sauvegarde par défaut de hello toochange, effectuer hello Bonjour comme suit [portail Azure](https://portal.azure.com/).

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a>toochange hello heure de début de stratégie de sauvegarde par défaut hello

1. Accédez trop**périphériques**. liste de Hello des appareils inscrits auprès du service Gestionnaire de périphériques StorSimple s’affichera. 
   
    ![Accédez toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. Sélectionnez votre appareil, puis cliquez dessus. Hello **paramètres** panneau s’affiche. Accédez trop**gérer > stratégies de sauvegarde**.
   
    ![sélectionner votre appareil](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. Bonjour **stratégies de sauvegarde** panneau, heure de début hello par défaut est 22:30. Vous pouvez spécifier la nouvelle heure de début hello pour une planification quotidienne de hello dans le fuseau horaire.
   
    ![Accédez toobackup stratégies](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. Cliquez sur **Enregistrer**.

### <a name="take-a-manual-backup"></a>Exécuter une sauvegarde manuelle

En outre tooscheduled des sauvegardes, vous pouvez exécuter une sauvegarde de (à la demande) manuelle de données de l’appareil à tout moment.

#### <a name="toocreate-a-manual-backup"></a>toocreate une sauvegarde manuelle

1. Accédez trop**périphériques**. Sélectionnez votre appareil et avec le bouton droit **...**  à hello plus à droite de la ligne sélectionnée de hello. Dans le menu contextuel de hello, sélectionnez **sauvegarde**.
   
    ![Accédez tootake sauvegarde](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. Bonjour **sauvegarde** panneau, cliquez sur **sauvegarde**. Cette opération sauvegarde tous les partages de hello sur le serveur de fichiers hello ou tous les volumes hello sur votre serveur iSCSI. 
   
    ![démarrage de sauvegarde](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    Une sauvegarde à la demande démarre ; vous constatez qu’un travail de sauvegarde a démarré.
   
    ![démarrage de sauvegarde](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    Une fois le travail de hello terminé, vous êtes averti à nouveau. processus de sauvegarde Hello démarre ensuite.
   
    ![travail de sauvegarde créé](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. progression de hello tootrack de sauvegardes de hello et examinez les détails de la tâche hello, cliquez sur la notification de hello. Vous accéderez trop **détails de la tâche**.
   
     ![détails du travail de sauvegarde](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. Une fois hello sauvegarde est terminée, passez trop**Gestion > catalogue de sauvegarde**. Vous verrez un instantané cloud de tous les partages de hello (ou volumes) sur votre appareil.
   
    ![Sauvegarde terminée](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a>Afficher les sauvegardes existantes
tooview les sauvegardes existantes hello, effectuer hello Bonjour portail Azure comme suit.

#### <a name="tooview-existing-backups"></a>sauvegardes existantes tooview

1. Accédez trop**périphériques** panneau. Sélectionnez votre appareil, puis cliquez dessus. Bonjour **paramètres** panneau, accédez trop**Gestion > catalogue de sauvegarde**.
   
    ![Accédez toobackup catalogue](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. Spécifiez hello suivant toobe de critères utilisé pour le filtrage :
   
    - **Période** : peut être **Dernière heure**, **Dernières 24 heures**, **Derniers 7 jours**, **30 derniers jours**, **Année dernière** et **Date personnalisée**.
    
    - **Appareils** – permet de sélectionner à partir de la liste de hello des serveurs de fichiers ou des serveurs iSCSI inscrits auprès du service Gestionnaire de périphériques StorSimple.
   
    - **Initialisé** : peut être automatiquement **Planifié** (par une stratégie de sauvegarde) ou lancé **Manuellement** (par vous).
   
    ![Filtrer les sauvegardes](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. Cliquez sur **Apply**. liste filtrée des sauvegardes Hello s’affiche dans hello **catalogue de sauvegarde** panneau. Uniquement 100 éléments de sauvegarde peuvent s’afficher simultanément.
   
    ![Catalogue de sauvegarde mis à jour](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur la [gestion de votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

