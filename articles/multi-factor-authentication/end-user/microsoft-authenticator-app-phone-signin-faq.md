---
title: aaaMicrosoft authentificateur phone connectez-vous - comptes Azure et Microsoft | Documents Microsoft
description: "Utilisez votre toosign phone tooyour compte Microsoft au lieu de taper votre mot de passe. Cet article répond aux questions fréquentes concernant cette fonctionnalité."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: a4911ff580b3ffa078299ad706d099330b75a2e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-with-your-phone-not-your-password"></a>Connectez-vous avec votre téléphone, et non votre mot de passe

application de Microsoft Authenticator Hello vous permet de sécuriser vos comptes en effectuant la vérification en deux étapes après avoir entré votre mot de passe. Mais vous ne connaissiez, il peut remplacer un mot de passe hello pour votre compte Microsoft personnel entièrement ? 

Cette fonctionnalité est disponible sur les appareils iOS et Android, et est compatible avec les comptes Microsoft personnels. 

## <a name="how-it-works"></a>Fonctionnement

Beaucoup d'entre vous utilisent hello Microsoft Authenticator application pour la vérification en deux étapes lors de la connexion tooyour compte Microsoft. Vous tapez votre mot de passe, puis toohello application tooeither approuver une notification ou obtenir un code de vérification. Dans téléphone, vous ignorez le mot de passe hello et effectuez toutes de la vérification de votre identité sur votre téléphone. Connectez-vous téléphone est un type de vérification en deux étapes, vous devez toujours tooprovide une chose que vous connaissez et une chose que vous avez tooverify votre identité. Hello phone est toujours chose hello et code confidentiel ou la clé biométrique de votre téléphone est chose hello que vous connaissez. 

## <a name="how-tooget-started"></a>Mode de démarrage tooget

toosign dans tooyour le compte Microsoft personnel avec votre téléphone, procédez comme suit : 

1. Activez la connexion par téléphone pour votre compte. 

  - Si vous n’avez hello Microsoft Authenticator application encore, installer et ajouter votre compte Microsoft personnel, en fonction de la procédure toohello hello [page de Microsoft Authenticator](microsoft-authenticator-app-how-to.md). Comptes nouvellement ajoutés sont automatiquement activées, vous êtes toogo bon.

  - Si vous utilisez déjà Microsoft Authenticator pour vérification en deux étapes, sélectionnez votre compte à partir de la page d’accueil application hello, puis **activer connectez-vous phone** à partir du menu déroulant de hello.

  >[!NOTE] 
  >tooprotect votre compte, nous avons besoin d’un code confidentiel ou un verrou biométrique sur votre appareil. Si vous conservez votre téléphone déverrouillé, application hello une demande vous tooset un verrou avant d’activer connectez-vous phone s’affiche. 

3. La plupart des pages où vous entrez habituellement le mot de passe de votre compte Microsoft comportent un lien indiquant **Utiliser une application à la place**. Sélectionnez cette toosign lien avec votre téléphone. 

4. Microsoft envoie un téléphone tooyour de notification. Approuver toosign de notification hello dans tooyour compte.   

## <a name="faq"></a>Forum Aux Questions 

### <a name="how-is-signing-in-with-my-phone-more-secure-than-typing-a-password"></a>En quoi la connexion par téléphone est-elle plus sécurisée que la saisie d’un mot de passe ?  

La plupart des gens connexion aujourd'hui tooweb sites ou applications à l’aide d’un nom d’utilisateur et un mot de passe.  Malheureusement, les mots de passe sont souvent perdus, volés ou devinés par des pirates. Lorsque vous configurez hello Microsoft Authenticator application toosign dans, nous générons une clé sur votre téléphone peut déverrouiller votre compte. Nous protéger cette clé avec un code confidentiel de hello ou biométriques que vous utilisez déjà sur votre téléphone.  Lorsque vous vous connectez avec votre téléphone, cette clé est utilisée tooprove votre identité en toute sécurité avec deux facteurs : hello phone lui-même et votre capacité toounlock il. 

clé Hello utilisée est similaire toohello clés utilisés dans Windows Hello et les spécifications de Rex Alliance UAF hello. Votre bio de données sont uniquement utilisé tooprotect hello clé localement et est jamais envoyée à ou stocké dans cloud de hello. 
 
### <a name="where-can-i-use-my-phone-tooreplace-my-password-and-where-would-i-still-need-hello-password"></a>Où puis-je utiliser mon tooreplace téléphone mon mot de passe, et où je déclenchera un mot de passe hello ?  

Aujourd'hui, hello phone sign-fonctionnalité fonctionne uniquement avec les applications web et les services qui sont alimentées par des comptes personnels Microsoft, iOS ou Android aux applications qui utilisent un compte Microsoft personnel et sur Windows 10, les applications qui utilisent un compte Microsoft personnel. Lorsque vous vous connectez dans tooone de ces sites ou applications web, sur la page hello généralement où que vous entrez votre mot de passe est un lien indiquant que **utiliser une application à la place**. 

Connectez-vous téléphone ne peut pas être toounlock utilisé un PC Windows, XBOX ou n’importe quel bureau les versions des applications Microsoft tels que les applications Office pour l’instant. 
 
### <a name="does-this-replace-two-step-verification-should-i-turn-it-off"></a>Cette fonctionnalité remplace-t-elle la vérification en deux étapes ? Dois-je désactiver cette dernière ?   

Parfois. Nous travaillons sur l’expansion de portée hello de la connexion au téléphone, mais pour l’instant il existe encore des emplacements dans l’écosystème de Microsoft hello qui ne prennent en charge. Lorsqu’elle n’est pas disponible, nous utilisons toujours la vérification en deux étapes pour sécuriser la connexion. C’est pourquoi vous ne devez pas désactiver la vérification en deux étapes pour votre compte. 
 
### <a name="okay-if-i-keep-two-step-verification-turned-on-for-my-account-do-i-have-tooapprove-two-notifications"></a>OK, si la vérification en deux étapes est activée pour mon compte conserver, dois-je tooapprove deux notifications ?

Non. L’ouverture de session tooyour compte Microsoft avec votre téléphone est considérée comme la vérification en deux étapes. Au lieu de taper votre mot de passe, puis l’approbation d’une notification de prouver votre identité par le fait de savoir comment toounlock votre téléphone et ensuite approuver une notification. Nous ne vous enverrons un deuxième tooapprove de notification.

### <a name="what-if-i-lose-my-phone-or-dont-have-it-with-me-how-can-i-access-my-account"></a>Et si je perds mon téléphone ou je ne l’ai pas sur moi, comment puis-je accéder à mon compte ?  

Vous pouvez toujours cliquer sur **utilisez un mot de passe à la place** sur tooswitch de page de connexion hello sauvegarder toousing votre mot de passe. Gardez à l’esprit que si vous utilisez la vérification en deux étapes, vous devez une deuxième tooverify de méthode vous connecter à. C’est pourquoi nous vous encourageons vivement toomake assurer que vous disposez des informations de sécurité supplémentaire et à jour sur votre compte. Vous pouvez gérer vos informations de sécurité à l’adresse https://account.live.com/proofs/manage. 
 
### <a name="how-do-i-stop-using-this-feature-and-go-back-tooentering-my-password"></a>Comment arrêter d’utiliser cette fonctionnalité et revenir en arrière tooentering mon mot de passe ?

Cliquez sur **Utiliser votre mot de passe à la place** sur la page de connexion. Nous n’oubliez pas de votre choix plus récente et qui offrent par hello de valeur par défaut prochaine fois que vous vous connectez. Si vous souhaitez jamais toosigning de retour toogo avec votre téléphone, cliquez sur **utiliser une application à la place**. 
 
### <a name="can-i-use-hello-app-toosign-in-tooall-my-accounts-with-microsoft"></a>Puis-je utiliser toosign d’application hello dans tooall mes comptes avec Microsoft ?   
Pour le moment, cette fonctionnalité est uniquement disponible pour les comptes Microsoft personnels. 
 
### <a name="can-i-sign-into-my-pc-with-my-phone"></a>Puis-je me connecter à mon PC avec mon téléphone ?  
Pour votre PC, nous vous recommandons de vous connecter à Windows Hello sur Windows 10 à l’aide de la reconnaissance des empreintes digitales ou faciale, ou d’un code PIN.   
 
### <a name="can-i-sign-in-with-my-windows-phone"></a>Puis-je me connecter avec mon Windows Phone ?  
À ce stade, nous développons pas cette fonctionnalité pour hello Microsoft Authenticator sur Windows Phone. 

## <a name="next-steps"></a>Étapes suivantes
Si vous n’avez pas encore téléchargé hello Microsoft Authenticator application, l’extraire. application Hello est disponible pour [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), et connectez-vous phone est disponible sur l’application de Microsoft Authenticator hello pour [Android](http://go.microsoft.com/fwlink/?Linkid=825072) et [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

Si vous avez des questions concernant l’application hello en général, examinons hello [Microsoft authentificateur FAQ](microsoft-authenticator-app-faq.md)
