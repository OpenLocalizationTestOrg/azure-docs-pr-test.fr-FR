---
title: "les mots de passe aaaChange via le Gestionnaire de périphériques StorSimple | Documents Microsoft"
description: "Décrit comment toouse hello toochange du service StorSimple Manager vos mots de passe d’administrateur de gestionnaire d’instantanés StorSimple et de périphérique."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a>Utilisez hello StorSimple Manager service toochange vos mots de passe StorSimple
## <a name="overview"></a>Vue d'ensemble
Hello portail Azure classic **configurer** page contient tous les paramètres de périphérique hello que vous pouvez reconfigurer sur un appareil StorSimple qui est géré par un service StorSimple Manager. Ce didacticiel explique comment vous pouvez utiliser hello **configurer** page toochange votre administrateur de l’appareil ou le mot de passe de gestionnaire d’instantanés StorSimple.

## <a name="change-hello-device-administrator-password"></a>Mot de passe de l’administrateur d’appareil modification hello
Lorsque vous utilisez Windows PowerShell interface tooaccess hello StorSimple, vous êtes tooenter requis un mot de passe administrateur. Lorsque l’appareil StorSimple première hello est inscrit auprès d’un service, un mot de passe par défaut hello pour cette interface est *Password1*. Sécurité hello de vos données, vous êtes toochange requis ce mot de passe à fin hello du processus d’inscription de hello. Vous ne pouvez pas quitter processus d’inscription de hello sans modifier ce mot de passe. Pour plus d’informations, consultez [étape 3 : configurer et inscrire l’appareil hello via Windows PowerShell pour StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

mot de passe Hello tout d’abord défini via l’interface Windows PowerShell de hello lors de l’inscription peut ensuite être modifié via hello portail Azure classic. Effectuer hello suivant les étapes toochange hello administrateur mot de passe.

#### <a name="toochange-hello-device-administrator-password"></a>mot de passe de l’administrateur d’appareil toochange hello
1. Dans le portail classique hello, cliquez sur **périphériques** > **configurer** pour votre appareil.
2. Faites défiler vers le bas toohello **mot de passe administrateur de l’appareil** section. Fournir un mot de passe administrateur contenant entre 8 caractères too15. mot de passe Hello doit être une combinaison d’au moins 3 caractères majuscules, minuscules, numériques et spéciaux.
3. Confirmer le mot de passe hello.
4. Cliquez sur **enregistrer** bas hello de page de hello.

mot de passe administrateur Hello périphérique doit maintenant être mis à jour. Vous pouvez utiliser cette interface Windows PowerShell de mot de passe modifié tooaccess hello.

## <a name="change-hello-storsimple-snapshot-manager-password"></a>Modifier le mot de passe de gestionnaire d’instantanés StorSimple hello
Gestionnaire d’instantanés StorSimple logiciel réside sur l’hôte Windows et permet aux administrateurs toomanage les sauvegardes de votre appareil StorSimple dans l’écran hello locaux et les instantanés cloud.

Lorsque vous configurez un appareil de gestionnaire d’instantanés StorSimple, vous serez invité tooprovide hello IP adresse et le mot de passe tooauthenticate d’appareil de votre périphérique de stockage. Ce mot de passe est d’abord configuré via l’interface Windows PowerShell de hello. Pour plus d’informations, consultez [étape 3 : configurer et inscrire l’appareil hello via Windows PowerShell pour StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

mot de passe Hello tout d’abord défini via l’interface Windows PowerShell de hello lors de l’inscription peut ensuite être modifié via le portail classique de hello. Effectuer hello suivant de mot de passe du Gestionnaire d’instantanés StorSimple étapes toochange hello.

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a>mot de passe toochange hello Gestionnaire d’instantanés StorSimple
1. Dans le portail classique hello, cliquez sur **périphériques** > **configurer** pour votre appareil.
2. Faites défiler vers le bas toohello **StorSimple Snapshot Manager** section. Entrez un mot de passe 14 ou 15 caractères. Assurez-vous que ce mot de passe hello contienne une combinaison d’au moins 3 caractères majuscules, minuscules, numériques et spéciaux.
3. Confirmer le mot de passe hello.
4. Cliquez sur **enregistrer** bas hello de page de hello.

mot de passe de gestionnaire d’instantanés StorSimple Hello doit maintenant être mis à jour.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [sécurité StorSimple](storsimple-security.md).
* En savoir plus sur la [modification de la configuration de votre appareil](storsimple-modify-device-config.md).
* En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).

