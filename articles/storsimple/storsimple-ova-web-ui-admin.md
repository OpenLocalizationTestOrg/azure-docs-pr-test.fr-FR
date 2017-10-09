---
title: "web de tableau virtuel aaaStorSimple administration de l’interface utilisateur | Documents Microsoft"
description: "Décrit comment tâches d’administration de base des périphériques de tooperform via l’interface utilisateur web de StorSimple Virtual Array hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a>Utilisez tooadminister de l’interface utilisateur Web hello votre tableau virtuel StorSimple
![flux du processus d'installation](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a>Vue d'ensemble
didacticiels Hello dans cet article s’appliquent toohello Microsoft Azure StorSimple Virtual Array (également appelé hello local périphérique virtuel StorSimple) en cours d’exécution mars 2016 (GA) version en disponibilité générale. Cet article décrit certains des flux de travail complexes hello et tâches de gestion qui peuvent être effectuées sur hello StorSimple Virtual Array. Vous pouvez gérer hello StorSimple Virtual Array à l’aide du service StorSimple Manager de hello UI (tooas référencé hello interface utilisateur du portail) et hello d’interface utilisateur web locale pour appareil de hello. Cet article se concentre sur les tâches hello que vous pouvez effectuer à l’aide de l’interface utilisateur web de hello.

Cet article inclut hello suivant didacticiels :

* Obtenir la clé de chiffrement de données de service hello
* Résoudre les erreurs d'installation de l'interface utilisateur web
* Générer un package de journaux
* Arrêter ou redémarrer votre appareil

## <a name="get-hello-service-data-encryption-key"></a>Obtenir la clé de chiffrement de données de service hello
Une clé de chiffrement de données de service est générée lorsque vous enregistrez votre premier appareil auprès hello service StorSimple Manager. Cette clé est alors requise avec hello service d’inscription tooregister clé des unités supplémentaires dans hello service StorSimple Manager.

Si vous avez égaré votre clé de chiffrement de données de service et que vous avez besoin de tooretrieve, hello suivants comme suit dans hello local interface utilisateur web de périphérique de hello inscrits auprès du service.

#### <a name="tooget-hello-service-data-encryption-key"></a>clé de chiffrement de données tooget hello service
1. Se connecter toohello interface utilisateur web de locale. Accédez trop**Configuration** > **paramètres Cloud**.
2. Au bas de hello de page de hello, cliquez sur **clé de chiffrement de données de service Get**. Une clé s'affiche. Copiez et enregistrez cette clé.
   
    ![obtenir la clé de chiffrement des données du service 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a>Résoudre les erreurs d'installation de l'interface utilisateur web
Dans certains cas lorsque vous configurez le périphérique hello via web locale de hello l’interface utilisateur, vous pouvez exécuter des erreurs. toodiagnose et résoudre de telles erreurs, vous pouvez exécuter des tests de diagnostic hello.

#### <a name="toorun-hello-diagnostic-tests"></a>tests de diagnostic de hello toorun
1. Dans l’interface utilisateur de web locale hello, accédez trop**dépannage** > **tests de Diagnostic**.
   
    ![exécuter les diagnostics 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. Au bas de hello de page de hello, cliquez sur **exécuter les Tests de Diagnostic**. Ceci lancera tests toodiagnose les éventuels problèmes de votre réseau, un périphérique, un proxy web, une heure ou un paramètres de cloud. Vous serez averti que cet appareil hello est en cours d’exécution des tests.
3. Une fois les tests hello terminées, les résultats hello seront affichera. Hello suivant montre les résultats de hello de tests de diagnostic. Notez que les paramètres de proxy web hello non configurés sur ce périphérique, et par conséquent, test de proxy web hello n’a pas été exécutée. Tous les hello autres tests pour les paramètres de réseau, serveur DNS, et les paramètres de temps ont réussi.
   
    ![exécuter les diagnostics 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a>Générer un package de journaux
Un package de journaux est composé de tous les journaux appropriés hello qui peuvent aider le Support technique de Microsoft à résoudre les problèmes de votre appareil. Dans cette version, un package de journaux peut être généré via l’interface utilisateur de web locale hello.

#### <a name="toogenerate-hello-log-package"></a>package de journaux hello toogenerate
1. Dans l’interface utilisateur de web locale hello, accédez trop**dépannage** > **journaux système**.
   
    ![générer un package de journaux 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. Au bas de hello de page de hello, cliquez sur **créer un package journal**. Un package de journaux du système hello va être créé. Cette opération prend quelques minutes.
   
    ![générer un package de journaux 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    Vous serez averti une fois hello package a été créé et hello page sera actualisée temps de hello tooindicate et date de création de package de hello.
   
    ![générer un package de journaux 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. Cliquez sur **Télécharger le package de journaux**. Un package zippé sera téléchargé sur votre système.
   
    ![générer un package de journaux 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. Vous pouvez décompresser le package de journaux téléchargé de hello et afficher les fichiers journaux du système hello.

## <a name="shut-down-and-restart-your-device"></a>Arrêter et redémarrer votre appareil
Vous pouvez arrêter ou redémarrer votre appareil virtuel à l’aide de l’interface utilisateur de web local hello. Nous recommandons que, avant de redémarrer, prendre des volumes de hello ou partages en mode hors connexion sur l’ordinateur hôte de hello et puis hello appareil. Vous réduisez ainsi toute possibilité d’altération des données. 

#### <a name="tooshut-down-your-virtual-device"></a>tooshut vers le bas de votre appareil virtuel
1. Dans l’interface utilisateur de web locale hello, accédez trop**Maintenance** > **paramètres d’alimentation**.
2. Au bas de hello de page de hello, cliquez sur **arrêt**.
   
    ![arrêter l'appareil 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. Un avertissement s’affiche indiquant qu’un arrêt de l’appareil de hello interrompra d’e/s à qui étaient en cours d’exécution, ce qui entraîne un temps d’arrêt. Cliquez sur une icône de coche hello ![icône en forme de coche](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![avertissement d'arrêt de l'appareil](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Vous serez averti qu’un arrêt hello a été lancé.
   
    ![arrêt de l'appareil initié](./media/storsimple-ova-web-ui-admin/image38.png)
   
    Appareil de Hello va s’arrêter. Si vous souhaitez toostart votre appareil, vous devez toodo qui, par le biais hello Gestionnaire Hyper-V.

#### <a name="toorestart-your-virtual-device"></a>toorestart votre appareil virtuel
1. Dans l’interface utilisateur de web locale hello, accédez trop**Maintenance** > **paramètres d’alimentation**.
2. Au bas de hello de page de hello, cliquez sur **redémarrer**.
   
    ![redémarrer l'appareil](./media/storsimple-ova-web-ui-admin/image36.png)
3. Un avertissement s’affiche indiquant que cet appareil hello redémarrage interrompra tout IOs qui étaient en cours d’exécution, ce qui entraîne un temps d’arrêt. Cliquez sur une icône de coche hello ![icône en forme de coche](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![avertissement de redémarrage](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Vous serez averti que le redémarrage hello a été lancé.
   
    ![redémarrage initié](./media/storsimple-ova-web-ui-admin/image39.png)
   
    Pendant le redémarrage de hello est en cours d’exécution, vous perdrez hello connexion toohello l’interface utilisateur. Vous pouvez surveiller hello redémarrage en actualisant hello UI régulièrement. Vous pouvez aussi surveiller état de redémarrage du périphérique hello via hello Gestionnaire Hyper-V.

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment trop[utilisez hello toomanage du service StorSimple Manager de votre appareil](storsimple-virtual-array-manager-service-administration.md).

