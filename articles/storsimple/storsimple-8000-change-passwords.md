---
title: aaaChange vos mots de passe StorSimple | Documents Microsoft
description: "Décrit comment toouse hello toochange du service Gestionnaire de périphériques StorSimple vos mots de passe d’administrateur de gestionnaire d’instantanés StorSimple et de périphérique."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a>Utilisez hello le Gestionnaire de périphériques StorSimple service toochange vos mots de passe StorSimple

## <a name="overview"></a>Vue d'ensemble
Bonjour Azure portal **paramètres de périphérique** option contienne tous les paramètres de périphérique hello que vous pouvez reconfigurer sur un appareil StorSimple qui est géré par un service Gestionnaire de périphériques StorSimple. Ce didacticiel explique comment vous pouvez utiliser hello **sécurité** sous **paramètres de périphérique** toochange votre administrateur de l’appareil ou le mot de passe de gestionnaire d’instantanés StorSimple.

## <a name="change-hello-device-administrator-password"></a>Mot de passe de l’administrateur d’appareil modification hello
Lorsque vous utilisez Windows PowerShell interface tooaccess hello StorSimple, vous êtes tooenter requis un mot de passe administrateur. Lorsque l’appareil StorSimple première hello est inscrit auprès d’un service, un mot de passe par défaut hello pour cette interface est *Password1*. Sécurité hello de vos données, vous êtes toochange requis ce mot de passe à fin hello du processus d’inscription de hello. Vous ne pouvez pas quitter processus d’inscription de hello sans modifier ce mot de passe. Pour plus d’informations, consultez [étape 3 : configurer et inscrire l’appareil hello via Windows PowerShell pour StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

mot de passe Hello tout d’abord défini via l’interface Windows PowerShell de hello lors de l’inscription peut être modifié ultérieurement via hello portail Azure. Effectuer hello suivant les étapes toochange hello administrateur mot de passe.

#### <a name="toochange-hello-device-administrator-password"></a>mot de passe de l’administrateur d’appareil toochange hello
1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**.

2. À partir de hello tabulaire la liste des périphériques, sélectionnez et cliquez sur périphérique de hello dont un mot de passe vous avez l’intention de toochange.

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. Bonjour **paramètres** panneau, accédez trop**paramètres du périphérique > sécurité**.

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. Bonjour **paramètres de sécurité** panneau, cliquez sur **mot de passe** mot de passe de l’administrateur d’appareil toochange hello.

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. Bonjour **mot de passe** panneau, fournir un mot de passe administrateur contenant entre 8 caractères too15. mot de passe Hello doit être une combinaison d’au moins 3 caractères majuscules, minuscules, numériques et spéciaux.

6. Confirmer le mot de passe hello.

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. Cliquez sur **Enregistrer** puis, lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui**.

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

mot de passe administrateur Hello périphérique doit maintenant être mis à jour. Vous pouvez utiliser cette interface Windows PowerShell de mot de passe modifié tooaccess hello.

## <a name="set-hello-storsimple-snapshot-manager-password"></a>Mot de passe de gestionnaire d’instantanés StorSimple hello
Gestionnaire d’instantanés StorSimple logiciel réside sur l’hôte Windows et permet aux administrateurs toomanage les sauvegardes de votre appareil StorSimple dans l’écran hello locaux et les instantanés cloud.

Lorsque vous configurez un appareil de gestionnaire d’instantanés StorSimple, vous serez invité tooprovide hello IP adresse et le mot de passe tooauthenticate d’appareil de votre périphérique de stockage.

Vous pouvez définir ou modifier un mot de passe hello Gestionnaire d’instantanés StorSimple via hello portail Azure. Effectuer hello suivant les étapes tooset ou modifier le mot de passe de gestionnaire d’instantanés StorSimple hello.

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a>mot de passe tooset hello Gestionnaire d’instantanés StorSimple
1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**.

2. À partir de hello tabulaire la liste des périphériques, sélectionnez et cliquez sur le périphérique de hello dont mot de passe de gestionnaire d’instantanés StorSimple vous avez l’intention tooset ou modifiez.

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. Bonjour **paramètres** panneau, accédez trop**paramètres du périphérique > sécurité**.

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. Bonjour **paramètres de sécurité** panneau, cliquez sur **mot de passe** tooset ou modification de mot de passe de gestionnaire d’instantanés StorSimple de hello.

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. Bonjour **mot de passe** panneau, entrez un mot de passe de 14 ou 15 caractères. Assurez-vous que ce mot de passe hello contienne une combinaison d’au moins 3 caractères majuscules, minuscules, numériques et spéciaux.

6. Confirmer le mot de passe hello.

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. Cliquez sur **Enregistrer** puis, lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui**.

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

mot de passe de gestionnaire d’instantanés StorSimple Hello doit maintenant être mis à jour.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [sécurité StorSimple](storsimple-8000-security.md).
* En savoir plus sur la [modification de la configuration de votre appareil](storsimple-8000-modify-device-config.md).
* En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

