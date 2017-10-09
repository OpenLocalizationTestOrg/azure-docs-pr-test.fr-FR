---
title: "aaaSet la vérification en deux étapes pour mon compte professionnel ou scolaire | Documents Microsoft"
description: "Lorsque votre société configure l’authentification multifacteur Azure, vous serez invité à toosign pour la vérification en deux étapes. Découvrez comment tooset, configurez-le. "
services: multi-factor-authentication
keywords: "Comment toouse azure directory, active directory dans le cloud hello, didacticiel d’active directory"
documentationcenter: 
author: kgremban
manager: femila
editor: pblachar
ms.assetid: 46f83a6a-dbdd-4375-8dc4-e7ea77c16357
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2d0348081eefa42c23de2047044688879dcb5966
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-my-account-for-two-step-verification"></a>Configurer mon compte pour la vérification en deux étapes
Vérification en deux étapes est une étape de sécurité supplémentaire qui permet de protéger votre compte, qui rendent plus difficile pour les autres toobreak personnes dans. Si vous lisez cet article, c’est que vous avez probablement reçu un e-mail de la part de l’administrateur de votre entreprise ou établissement scolaire concernant Multi-Factor Authentication. Ou peut-être vous a tenté de toosign dans un message vous demandant de tooset la vérification de sécurité supplémentaire. Si tel est le cas de hello, **vous ne pouvez pas vous connecter jusqu'à ce que vous avez terminé le processus d’inscription automatique hello**.

Cet article vous aide à configurer votre **compte professionnel ou scolaire**. Si vous souhaitez la vérification en deux étapes de tooenable pour votre propre compte Microsoft personnel, consultez [sur la vérification en deux étapes](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).

## <a name="set-up-your-account"></a>Configurer votre compte

Lorsque votre service informatique vous oblige toostart à l’aide de la vérification en deux étapes, un message de l’écran **votre administrateur exige que vous définissez ce compte pour la vérification de sécurité supplémentaire** s’affiche :

![Paramétrage](./media/multi-factor-authentication-end-user-first-time/first.png)

tooget démarré, sélectionnez **configurer maintenant.**

Si vous ne voyez pas un écran comme suit lors de la connexion, suivez les instructions de hello de [gérer vos paramètres de vérification en deux étapes](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page) où vous pouvez gérer vos options de vérification de page des paramètres toofind hello. 

## <a name="decide-how-you-want-tooverify-your-sign-ins"></a>Décidez comment tooverify vos connexions

première question de Hello dans le processus d’inscription de hello est la façon dont vous souhaitez que nous toocontact vous. Examinons les options hello dans la table de hello et utilisez les étapes d’installation de hello liens toogo toohello pour chaque méthode.

| Méthode de contact | Description |
| --- | --- |
| [Application mobile](#use-a-mobile-app-as-the-contact-method) |- **Recevoir des notifications pour la vérification.** Cette option exécute un push d’une application d’authentification toohello notification sur votre tablette ou le smartphone. Afficher la notification de hello et, si elle est légitime, sélectionnez **authentifier** dans l’application hello. Votre entreprise ou établissement scolaire peut vous demander d’entrer un code confidentiel avant de vous authentifier.<br>- **Utiliser le code de vérification.** Dans ce mode, application d’authentification hello génère un code de vérification qui met à jour toutes les 30 secondes. Entrez le code de vérification hello plus récente dans l’interface de connexion hello.<br>application de Microsoft Authenticator Hello est disponible pour [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), et [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| [Appel ou SMS sur téléphone mobile](#use-your-mobile-phone-as-the-contact-method) |- **Appel téléphonique** place un numéro de téléphone de toohello d’appel vocal automatisé vous fournissez. Répondre à un appel de hello et appuyez sur # dans hello phone pavé tooauthenticate.<br>- **SMS** envoie un SMS contenant un code de vérification. Après l’invite hello dans le texte hello, soit de répondre au message de texte toohello ou entrez le code de vérification hello fourni dans l’interface de connexion hello. |
| [Appel téléphonique au bureau](#use-your-office-phone-as-the-contact-method) |Place un numéro de téléphone de toohello d’appel vocal automatisé que vous fournissez. Hello de réponse appel et appuie sur # dans hello phone pavé tooauthenticate. |

## <a name="use-a-mobile-app-as-hello-contact-method"></a>Utiliser une application mobile comme méthode de contact hello
Cette méthode nécessite l’installation d’une application d’authentification sur votre téléphone ou tablette. étapes de cet article Hello sont basés sur l’application Microsoft Authenticator hello, qui est disponible pour [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), et [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

1. Sélectionnez **application Mobile** à partir de la liste déroulante de hello.
2. Sélectionnez **Recevoir des notifications pour la vérification** ou **Utiliser le code de vérification**, puis sélectionnez **Configurer**.

   ![Écran de vérification de sécurité supplémentaire](./media/multi-factor-authentication-end-user-first-time/mobileapp.png)

3. Sur votre téléphone ou votre tablette, ouvrez l’application hello et sélectionnez  **+**  tooadd un compte. (Sur les appareils Android, sélectionnez hello trois points, puis **Ajouter compte**.)
4. Spécifier que vous souhaitez tooadd un compte professionnel ou scolaire. scanner de code QR Hello sur votre téléphone s’ouvre. Si votre appareil photo ne fonctionne pas correctement, vous pouvez sélectionner tooenter informations de votre société manuellement. Pour plus d’informations, consultez [Ajouter manuellement un compte](#add-an-account-manually).  
5. Numérisez image code QR hello est apparu avec écran hello pour la configuration d’application mobile hello.  Sélectionnez **fait** écran de code hello QR tooclose.  

   ![Écran de code QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)

6. Lorsque l’activation se termine sur le téléphone de hello, sélectionnez **Contact me**.  Cette étape envoie une notification ou un téléphone de tooyour de code de vérification. Sélectionnez **Vérifier**.  
7. Si votre entreprise requiert un code confidentiel pour approuver la vérification de l’identification, entrez-le.

   ![Zone permettant d’entrer un code confidentiel](./media/multi-factor-authentication-end-user-first-time/scan3.png)

8. Une fois le code confidentiel entré, sélectionnez **Fermer**. À ce stade, la vérification doit réussir.
9. Nous vous recommandons d’entrer votre numéro de téléphone mobile en cas de perte d’application mobile de tooyour accès. Spécifiez votre pays dans la liste déroulante de hello et entrez votre numéro de téléphone mobile dans le nom de pays hello boîte suivant toohello. Sélectionnez **Suivant**.
10. À ce stade, vous êtes invité à tooset des mots de passe d’application pour les applications non-Web comme Outlook 2010 ou antérieure ou une application de messagerie native hello sur des périphériques Apple. Cette action s’explique par le fait que certaines applications ne prennent pas en charge la vérification en deux étapes. Si vous n’utilisez pas ces applications, cliquez sur **fait** et ignorez les étapes restantes hello.
11. Si vous utilisez ces applications, mot de passe copie hello fourni et collez-le dans votre application au lieu de votre mot de passe standard. Vous pouvez utiliser hello même mot de passe pour plusieurs applications. Pour plus d’informations, [aide sur les mots de passe d’application].
12. Cliquez sur **Done**.

### <a name="add-an-account-manually"></a>Ajouter manuellement un compte
Si vous souhaitez tooadd une application mobile toohello de compte au lieu d’utiliser le lecteur de hello QR manuellement, procédez comme suit.

1. Sélectionnez hello **entrer manuellement les compte** bouton.  
2. Entrez les code hello et l’URL de hello qui sont fournis sur hello même page qui vous montre hello code-barres. Ces informations s’intègre dans hello **Code** et **URL** zones sur les applications mobiles hello.

    ![Paramétrage](./media/multi-factor-authentication-end-user-first-time/barcode2.png)
3. L’activation de hello terminée, sélectionnez **Contact me**. Cette étape envoie une notification ou un téléphone de tooyour de code de vérification. Sélectionnez **Vérifier**.

## <a name="use-your-mobile-phone-as-hello-contact-method"></a>Utiliser votre téléphone mobile comme méthode de contact hello
1. Sélectionnez **téléphone d’authentification** à partir de la liste déroulante de hello.  

    ![Paramétrage](./media/multi-factor-authentication-end-user-first-time/phone.png)  
2. Choisissez votre pays à partir de la liste déroulante de hello et entrez votre numéro de téléphone mobile.
3. Sélectionnez la méthode hello vous préférez toouse avec votre téléphone mobile - SMS ou appel.
4. Sélectionnez **Contact me** tooverify votre numéro de téléphone. Selon le mode hello sélectionné, nous vous envoyer un SMS ou appel que vous avez. Suivez les instructions de hello fournies dans l’écran hello, puis sélectionnez **Vérifiez**.
5. À ce stade, vous êtes invité à tooset des mots de passe d’application pour les applications non-Web comme Outlook 2010 ou antérieure ou une application de messagerie native hello sur des périphériques Apple. Cette action s’explique par le fait que certaines applications ne prennent pas en charge la vérification en deux étapes. Si vous n’utilisez pas ces applications, cliquez sur **fait** et ignorer les autres étapes de hello hello.
6. Si vous utilisez ces applications, mot de passe copie hello fourni et collez-le dans votre application au lieu de votre mot de passe standard. Vous pouvez utiliser hello même mot de passe pour plusieurs applications. Pour plus d’informations, [aide sur les mots de passe d’application].
7. Cliquez sur **Done**.

## <a name="use-your-office-phone-as-hello-contact-method"></a>Utiliser votre téléphone de bureau comme méthode de contact hello
1. Sélectionnez **téléphone** dans hello de liste déroulante  

    ![Paramétrage](./media/multi-factor-authentication-end-user-first-time/office.png)  
2. zone de numéro de téléphone Hello est automatiquement renseigné avec les informations de contact de votre société. Si le nombre de hello est erroné ou manquant, demandez à votre administrateur toomake modifications.
3. Sélectionnez **Contact me** tooverify votre numéro de téléphone et nous appellera votre numéro. Suivez les instructions de hello fournies dans l’écran hello, puis sélectionnez **Vérifiez**.
4. À ce stade, vous êtes invité à tooset des mots de passe d’application pour les applications non-Web comme Outlook 2010 ou antérieure ou une application de messagerie native hello sur des périphériques Apple. Cette action s’explique par le fait que certaines applications ne prennent pas en charge la vérification en deux étapes. Si vous n’utilisez pas ces applications, cliquez sur **fait** et ignorer les autres étapes de hello hello.
5. Si vous utilisez ces applications, mot de passe copie hello fourni et collez-le dans votre application au lieu de votre mot de passe standard. Vous pouvez utiliser hello même mot de passe pour plusieurs applications. Pour plus d’informations, consultez [Définition des mots de passe d’application](multi-factor-authentication-end-user-app-passwords.md).
6. Cliquez sur **Done**.

## <a name="next-steps"></a>Étapes suivantes
* Modifier les options préférées et [gérer les paramètres de la vérification en deux étapes](multi-factor-authentication-end-user-manage-settings.md)
* Configurer des [mots de passe d’application](multi-factor-authentication-end-user-app-passwords.md) pour les applications natives sur des appareils qui ne prennent pas en charge la vérification en deux étapes
* Extraire hello [application Authenticator de Microsoft](microsoft-authenticator-app-how-to.md) d’accélérée, sécuriser l’authentification, même si vous n’avez pas service de la cellule.

