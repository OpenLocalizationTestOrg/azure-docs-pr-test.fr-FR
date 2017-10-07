---
title: "mot de passe de l’administrateur d’appareil aaaChange StorSimple Virtual Array | Documents Microsoft"
description: "Décrit comment toouse hello soit portail Azure ou StorSimple Virtual Array web UI toochange hello appareil mot de passe administrateur."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a>Modifier le mot de passe hello StorSimple Virtual Array appareil administrateur via le Gestionnaire de périphériques StorSimple

## <a name="overview"></a>Vue d'ensemble

Lorsque vous utilisez hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, vous êtes tooenter requis un mot de passe administrateur. Lorsque l’appareil StorSimple hello est tout d’abord configuré et démarré, le mot de passe par défaut hello est *Password1*. Pour une sécurité hello de vos données, un mot de passe par défaut hello expire hello première fois que vous vous connectez et vous est requis toochange ce mot de passe.

Vous pouvez également utiliser soit hello web local UI ou hello toochange portail Azure hello appareil administrateur mot de passe à tout moment une fois l’appareil de hello est déployé dans votre environnement de production. Chacune de ces procédures est décrite dans cet article.

 ![Panneau Appareils](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a>Mot de passe hello hello toochange portail Azure

Effectuer hello suivant les étapes toochange hello appareil mot de passe administrateur via hello portail Azure.

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a>mot de passe administrateur toochange pour hello appareil via hello portail Azure

1. Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur service hello nom, puis dans hello **gestion** , cliquez sur **périphériques**. Cette opération ouvre hello **périphériques** panneau qui répertorie tous vos appareils StorSimple Virtual Array.

2. Bonjour **périphériques** panneau, double-cliquez sur le périphérique hello qui nécessite un changement de mot de passe.

3. Bonjour **paramètres** panneau pour votre appareil, cliquez sur **sécurité**.

4. Bonjour **paramètres de sécurité** panneau, hello suivant :
   
   1. Faites défiler vers le bas toohello **mot de passe administrateur de l’appareil** section. Fournir un mot de passe administrateur contenant entre 8 caractères too15.
   2. Confirmer le mot de passe hello.
   3. Cliquez sur **enregistrer** haut hello du Panneau de hello.

mise à jour de mot de passe administrateur de périphérique Hello. Vous pouvez utiliser ce périphérique de hello tooaccess mot de passe modifié localement.

![Panneau Paramètres de sécurité](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a>Utilisez hello web local UI toochange hello mot de passe

Effectuer hello suivant les étapes toochange hello appareil mot de passe administrateur via l’interface utilisateur de web locale hello.

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a>mot de passe administrateur toochange pour hello appareil via l’interface utilisateur de web locale hello

1. Dans l’interface utilisateur de web locale hello, cliquez sur **Maintenance** > **modification de mot de passe** pour votre appareil.
   
    ![change password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. Entrez hello **mot de passe actuel**.
3. Fournissez un **nouveau mot de passe**. mot de passe Hello doit être au moins 8 caractères. Il doit contenir 3 des 4 suivants de hello : caractères majuscules, minuscules, numériques et spéciaux.
   
    Notez que votre mot de passe ne peut pas être hello identique hello derniers 24 mots de passe.
4. Entrez à nouveau tooconfirm de mot de passe hello il.
   
    ![change password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. Au bas de hello de page de hello, cliquez sur **appliquer**. nouveau mot de passe Hello est maintenant appliquée. Si la modification de mot de passe hello ne réussit pas, vous consultez hello l’erreur suivante :
   
    ![password error](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    Une fois le mot de passe hello est correctement mise à jour, vous êtes averti. Vous pouvez ensuite utiliser ce périphérique de hello tooaccess mot de passe modifié localement.


## <a name="next-steps"></a>Étapes suivantes
Découvrez comment trop[administrer votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

