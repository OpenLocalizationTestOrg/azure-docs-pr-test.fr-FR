---
title: "application d’authentification aaaMicrosoft pour les téléphones mobiles | Documents Microsoft"
description: "Découvrez comment tooupgrade toohello dernière version de Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>Prise en main hello Microsoft Authenticator application
application Microsoft Authenticator Hello fournit un niveau supplémentaire de sécurité de votre compte professionnel ou scolaire (par exemple, bsimon@contoso.com) ou votre compte Microsoft (par exemple, bsimon@outlook.com).

application Hello fonctionne dans un des deux façons :

* **Notification**. application Hello peut aider à empêcher tout accès non autorisé tooaccounts et arrêter les transactions frauduleuses en envoyant une notification tooyour smartphone ou une tablette. Afficher simplement la notification de hello et si elle est légitime, sélectionnez **Vérifiez**. Sinon, vous pouvez sélectionner **Refuser**. 
* **Code de vérification**. application Hello peut être utilisée comme un logiciel de jeton toogenerate un code de vérification OAuth. Après avoir entré votre nom d’utilisateur et un mot de passe, vous entrez le code hello fourni par l’application hello dans l’écran de connexion hello. code de vérification Hello fournit un deuxième formulaire d’authentification.

application de Microsoft Authenticator Hello remplace l’application Azure Authenticator de hello. application Azure Authenticator de Hello fonctionne toujours, mais si vous décidez d’application Microsoft Authenticator toomove toohello, cet article peut vous aider.  

## <a name="opt-in-for-two-step-verification"></a>Abonnement à la vérification en deux étapes

application de Microsoft Authenticator Hello ne fonctionne pas par lui-même. Configurer chacun de vos tooprompt de comptes d’une deuxième méthode de vérification après avoir connectez-vous avec votre nom d’utilisateur et un mot de passe. 

Pour un compte professionnel ou scolaire, vous ne généralement obtenir toochoose cette fonctionnalité pour vous-même. Au lieu de cela, un administrateur de sécurité a donné son consentement à votre place et vous avertit tooregister les méthodes de vérification de votre compte. Si ce scénario s’applique tooyou, pour en savoir plus [que signifie l’authentification multifacteur Azure pour me](multi-factor-authentication-end-user.md).

Pour un compte personnel, vous devez tooset la vérification en deux étapes pour vous-même. Si vous avez un compte Microsoft, ces étapes sont disponibles dans [À propos de la vérification en deux étapes](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification). 

Vous pouvez également utiliser hello Microsoft Authenticator avec les comptes non Microsoft. Ils peuvent faire appel fonctionnalité de hello chose qu’une vérification en deux étapes, mais vous devez être en mesure de toofind sous les paramètres de sécurité ou de connexion. 

## <a name="install-hello-app"></a>Installer l’application hello
application de Microsoft Authenticator Hello est disponible pour [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), et [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="add-accounts-toohello-app"></a>Ajouter des comptes toohello application
Pour chaque compte que vous souhaitez tooadd toohello Microsoft Authenticator application, utilisez une des hello procédures suivantes :

### <a name="add-a-personal-microsoft-account-toohello-app"></a>Ajouter une application de toohello de compte Microsoft personnelle

Pour un compte Microsoft personnel (une que vous utilisez toosign dans tooOutlook.com, Xbox, Skype, etc.), tout ce que vous avez toodo est compte tooyour dans l’application de Microsoft Authenticator hello de connexion.

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>Ajouter un travail ou d’établissement scolaire application toohello de compte à l’aide du scanner de code hello QR
1. Passez l’écran de paramètres de vérification de sécurité toohello.  Pour plus d’informations sur l’écran de toothis tooget, consultez [modification des paramètres de sécurité](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).
2. Case à cocher hello ensuite trop**application Authenticator** puis sélectionnez **configurer**.

    ![bouton de configurer Hello sur l’écran de paramètres de vérification de sécurité hello](./media/authenticator-app-how-to/azureauthe.png)

    Cela fait apparaître un écran avec un code QR dessus.

    ![Écran qui fournit du code de hello QR](./media/authenticator-app-how-to/barcode2.png)
3. Application Microsoft Authenticator hello ouvert. Sur hello **comptes** écran, sélectionnez  **+** , puis indiquez que vous souhaitez tooadd un compte professionnel ou scolaire.
4. Utilisez hello caméra tooscan hello QR code et sélectionnez **fait** écran de code hello QR tooclose.

    Si votre appareil photo ne fonctionne pas correctement, vous pouvez [entrer manuellement les hello QR code et l’URL](#add-an-account-to-the-app-manually).

5. Lors de l’application hello affiche le nom de votre compte avec un code à six chiffres situés sous celui-ci, vous avez terminé. 

    ![Écran de comptes](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>Ajouter une application de toohello compte manuellement
1. Passez l’écran de paramètres de vérification de sécurité toohello.  Pour plus d’informations sur l’écran de toothis tooget, consultez [modification des paramètres de sécurité](multi-factor-authentication-end-user-manage-settings.md).
2. Sélectionnez **Configurer**.

    ![bouton de configurer Hello sur l’écran de paramètres de vérification de sécurité hello](./media/authenticator-app-how-to/azureauthe.png)

    Cela fait apparaître un écran avec un code QR dessus.  Code de note de hello et l’URL.

    ![Écran qui fournit le code de hello QR et l’URL](./media/authenticator-app-how-to/barcode2.png)
3. Application Microsoft Authenticator hello ouvert. Sur hello **comptes** écran, sélectionnez  **+** , puis indiquez que vous souhaitez tooadd un compte professionnel ou scolaire.

4. Dans l’Analyseur de hello, sélectionnez **Entrez du code manuellement**.

    ![Écran pour scanner un code QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Entrez le code de hello et l’URL de hello dans les zones appropriées de hello dans l’application hello, puis sélectionnez **Terminer**.

    ![Écran pour saisir le code et de l’URL](./media/authenticator-app-how-to/manual.png)

6. Lors de l’application hello affiche le nom de votre compte avec un code à six chiffres situés sous celui-ci, vous avez terminé.

    ![Écran de comptes](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>Ajouter une application toohello de compte à l’aide de Touch ID
application de Microsoft Authenticator Hello sur iOS prend en charge un ID tactile.  Azure multi-Factor Authentication permet aux organisations toorequire un code confidentiel pour les appareils. Avec Touch ID, les utilisateurs iOS n’avez pas besoin tooenter un code confidentiel. Au lieu de cela, ils peuvent analyser leur empreinte digitale et sélectionner **Approuver**.

La configuration de Touch ID avec Microsoft Authenticator est simple. Vous effectuez une vérification normale avec un code confidentiel. Si votre appareil prend en charge Touch ID, Microsoft Authenticator le configure automatiquement pour ce compte.

![Vérification de la configuration de Touch ID](./media/authenticator-app-how-to/touchid1.png)

À partir de ce point vers l’avant, quand vous êtes requis tooverify vous connecter à, vous sélectionnez de notifications push hello reçu et analyser votre empreinte digitale au lieu d’entrer votre PIN.

![Notification Push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>Utiliser l’application hello lors de la connexion

Une fois que votre compte est ajouté toohello application, vous pouvez être demandées par invite toodo un toomake de vérification de test que tout a été correctement configuré. Après cela, vous avez terminé ! Vous n’avez pas besoin toodo chose jusqu'à ce que hello prochaine fois que vous vous connectez.

Si vous choisissez des codes de vérification toouse dans l’application hello, vous démarrez toosee à la page d’accueil hello. Ils changent toutes les 30 secondes, de sorte que vous ayez toujours un nouveau code lorsque vous en avez besoin. Mais vous n’avez pas besoin toodo rien avec eux jusqu'à ce que vous vous connecter et sont invités à tooenter un code de vérification.  
