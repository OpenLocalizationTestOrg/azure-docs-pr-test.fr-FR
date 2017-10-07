---
title: "aaaAzure MFA connectez-vous avec vérification en deux étapes | Documents Microsoft"
description: "Cette page vous fournira des conseils sur où toogo toosee hello différentes méthodes de connexion disponibles avec l’authentification Multifacteur Azure."
keywords: "authentification de l'utilisateur, expérience de connexion, connexion avec un téléphone mobile, connexion avec le téléphone de bureau"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>expérience Hello de connexion avec l’authentification multifacteur Azure
> [!NOTE]
> Hello cet article vise toowalk via une expérience d’authentification classique. Pour plus d’informations la signature ou des problèmes de tootroubleshoot, consultez [rencontre des problèmes avec l’authentification multifacteur Azure](multi-factor-authentication-end-user-troubleshoot.md).

## <a name="what-will-your-sign-in-experience-be"></a>Quelle sera votre expérience de connexion ?
Votre expérience de connexion diffère selon que vous choisissez toouse comme votre second facteur : un appel téléphonique, d’une application d’authentification ou de textes. Choisissez l’option hello qui décrit le mieux ce que vous faites :

| Comment vous connectez-vous ? | 
| --- |
| [Avec un téléphone mobile ou bureau de toomy appel téléphonique](#signing-in-with-a-phone-call) |
| [Avec un texte toomy un téléphone mobile](#signing-in-with-a-text-message)
| [Des notifications à partir de l’application de Microsoft Authenticator hello](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [Avec les codes de vérification à partir de l’application de Microsoft Authenticator hello](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [Avec une autre méthode, car je ne peux pas utiliser ma méthode préférée à l’heure actuelle](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>Connexion avec un appel téléphonique
Hello informations suivantes décrit l’expérience de vérification en deux étapes hello avec un appareil mobile tooyour d’appel ou de téléphone de bureau.

1. Se connecter tooan application ou service tel qu’Office 365 à l’aide de votre nom d’utilisateur et un mot de passe.  
2. Microsoft vous appelle.  
3. Répondre hello téléphone et appuyez sur touche # de hello.  

## <a name="signing-in-with-a-text-message"></a>Connexion avec un message texte
Hello informations suivantes décrit l’expérience de vérification en deux étapes hello avec un message texte tooyour un téléphone mobile :

1. Se connecter tooan application ou service tel qu’Office 365 à l’aide de votre nom d’utilisateur et un mot de passe. 
2. Microsoft vous envoie un message texte qui contient un code à chiffres. 
3. Entrez les code hello dans zone hello fournie sur la page de connexion hello. 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>Connecter à l’application de Microsoft Authenticator hello 
Hello ci-après décrit le hello expérience de l’utilisation d’application de Microsoft Authenticator hello pour les vérifications en deux étapes. Il existe deux façons différentes toouse hello application. Vous pouvez recevoir des notifications push sur votre appareil, ou vous pouvez ouvrir hello application tooget un code de vérification.

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>toosign avec une notification à partir de l’application de Microsoft Authenticator hello
1. Se connecter tooan application ou service tel qu’Office 365 à l’aide de votre nom d’utilisateur et un mot de passe.
2. Microsoft envoie une application de Microsoft Authenticator toohello notification sur votre appareil.

  ![Microsoft envoie une notification](./media/multi-factor-authentication-end-user-signin/notify.png)

3. Notification hello ouvert sur votre téléphone et les sélectionner hello **Vérifiez** clé. Si votre entreprise requiert un code confidentiel, vous pouvez l’entrer ici.
4. Vous devez maintenant être connecté.

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>toosign à l’aide d’un code de vérification avec application de Microsoft Authenticator hello

Si vous utilisez des codes de vérification hello tooget de l’application Microsoft Authenticator, lorsque vous ouvrez l’application hello, vous consultez un nombre sous le nom de votre compte. Ce nombre change toutes les 30 secondes afin que vous n’utilisez pas hello même nombre à deux reprises. Lorsque vous êtes invité à entrer un code de vérification, ouvrez l’application hello et utiliser le nombre est actuellement affiché. 

1. Se connecter tooan application ou service tel qu’Office 365 à l’aide de votre nom d’utilisateur et un mot de passe.
2. Microsoft vous demande un code de vérification.

  ![Entrer le code de vérification](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. Ouvrez l’application de Microsoft Authenticator hello sur votre téléphone et entrez les code de hello dans zone hello où vous vous connectez.

## <a name="signing-in-with-an-alternate-method"></a>Connexion avec une autre méthode
Parfois, vous n’avez hello téléphone ou un périphérique que vous avez configurée comme méthode de vérification préférée. C’est la raison pour laquelle nous vous recommandons de définir des méthodes de sauvegarde pour votre compte. Hello section suivante vous montre comment toosign avec une autre méthode de votre méthode principale n’est peut-être pas disponible.

1. Se connecter tooan application ou service tel qu’Office 365 à l’aide de votre nom d’utilisateur et un mot de passe.
2. Sélectionnez **Utiliser une autre option de vérification**. Vous voyez autant d’options de vérification que vous en avez configurées.
3. Choisissez une autre méthode et connectez-vous.

  ![Utiliser une autre méthode](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>Étapes suivantes

Si vous rencontrez des problèmes de connexion avec la vérification en deux étapes, obtenez plus d’informations sur la page [Difficultés avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md).

Découvrez comment trop[gérer vos paramètres de vérification en deux étapes](multi-factor-authentication-end-user-manage-settings.md).

Découvrez comment trop[prise en main hello Microsoft Authenticator application](microsoft-authenticator-app-how-to.md) afin que vous puissiez utiliser les notifications toosign, au lieu de textes et les appels téléphoniques. 
