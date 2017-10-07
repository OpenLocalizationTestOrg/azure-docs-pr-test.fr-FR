---
title: "application d’authentification aaaMicrosoft aide et support | Documents Microsoft"
description: "Fournit une liste de questions fréquemment posées et les réponses associées toohello Microsoft Authentication app et l’authentification multifacteur Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f04d5bce-e99e-4f75-82d1-ef6369be3402
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: afba9b59ccaac60d022e8516fcf573dcfbf68af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-authenticator-app-faq"></a>Forum aux questions sur l’application Microsoft Authenticator

Cet article répond aux questions courantes que nous recevons sur l’application de Microsoft Authenticator hello. Si vous ne voyez pas un tooyour répondre à la question, accédez à toohello [forum d’application Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp). Nous avons également un autre Forum aux questions concernant une fonctionnalité spécifique sur l’application hello, [connectez-vous avec votre téléphone FAQ](microsoft-authenticator-app-phone-signin-faq.md).

application de Microsoft Authenticator Hello remplacé application Azure Authenticator de hello et hello conseillons application lorsque vous utilisez l’authentification multifacteur Azure. application de Microsoft Authenticator Hello est disponible pour [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), et [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="frequently-asked-questions"></a>Forum Aux Questions

### <a name="what-are-hello-codes-in-hello-app-for-why-does-hello-number-keep-counting-down"></a>Quelles sont les codes hello dans application hello pour ? Pourquoi nombre de hello conserver rebours ?

Lorsque vous ouvrez hello Microsoft Authenticator application, vous voyez que vous avez ajouté des comptes hello et un numéro à six ou huit chiffres par chacun d’eux. Vous pouvez voir un minuteur de 30 secondes exécutant un compte à rebours.

Ces codes sont utilisés lors de la connexion tooyour compte. Après avoir entré votre nom d’utilisateur et un mot de passe, vous pouvez être invité à tooenter un code de vérification. Ouvrez hello Microsoft Authenticator application copie hello code et qui est actuellement affiché. Entrez ce code dans toofinish de page de connexion hello.

Bonjour raison que les codes hello modifier toutes les 30 secondes est afin que vous n’utilisez jamais hello même code à deux reprises. Il n’est pas comme un mot de passe que vous êtes censé tooremember. Hello est que seules les personnes avec un téléphone tooyour accès connaît votre code de vérification.

codes de Hello ne nécessitent pas internet ou des données, vous n’avez tooworry informant phone service toosign. Lorsque vous fermez application hello, il ne conserver en cours d’exécution en arrière-plan de hello et il ne videz votre batterie. Vous pouvez fermer l’application hello et ignorer jusqu'à ce que la prochaine fois que vous vous connectez de hello.  

### <a name="i-only-get-notifications-when-i-have-hello-app-open-if-hello-app-isnt-open-i-dont-get-any-notifications"></a>Obtenir uniquement des notifications lorsque j’ai application hello ouvrir. Si l’application hello n’est pas ouverte, je n’obtiens de notifications.

Si vous recevez des notifications, mais qu’elles ne bruit ou faire vibrer malgré votre sonnerie sur, vérifiez tout d’abord les paramètres de l’application hello. Activer le son de toouse application hello ou faire vibrer avec ses notifications.

Si vous n’obtenez de notifications, vérifiez hello suivant cas :

- Votre téléphone est-il en mode silencieux ou Ne pas déranger ? Ce mode peut empêcher l’envoi de notifications par les applications.
- Vous recevez des notifications d’autres applications ? Si ce n’est pas le cas, il peut y avoir un problème avec les connexions de réseau hello sur votre téléphone ou un canal de notifications hello à partir d’Android ou Apple. Vous pouvez traiter la première option à hello dans les paramètres de votre téléphone, mais vous devrez peut-être le fournisseur de services tootalk tooyour pour vous aider à la deuxième option de hello.
- Vous pouvez recevoir des notifications pour certains comptes de l’application hello, mais pas d’autres ? Si Oui, supprimer le compte problématiques de hello de votre application et l’ajouter à nouveau des notifications push de tooenable. 

Si vous avez tenté ces suggestions de dépannage mais que les problèmes persistent, envoyez-nous vos journaux pour que nous les vérifiions. Paramètres de l’application toohello, puis sélectionnez **aide et commentaires** et **envoyer les journaux de**. Ensuite, passez toohello [forum d’application Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) et faites-nous savoir ce que problème que vous voyez et indique les étapes que vous avez essayé de jusqu'à présent. 

### <a name="im-already-using-hello-microsoft-authenticator-application-for-verification-codes-how-do-i-switch-tooone-click-push-notifications"></a>J’utilise déjà hello application Authenticator de Microsoft pour les codes de vérification. Comment basculer les notifications push de clic tooone ?
L’approbation d’une connexion via notification push est disponible uniquement pour les comptes Microsoft personnels, professionnels ou scolaires. Les comptes tiers tels que Google ou Facebook ne bénéficient pas de cette fonctionnalité. Si vous disposez d’une entreprise ou école compte Microsoft, votre organisation peut choisir cette option toodisable.

Si vous utilisez un compte Microsoft pour votre compte personnel et que vous souhaitez tooswitch sur toopush notifications, vous devez tooadd votre compte à nouveau. Réinscrivez le périphérique hello avec votre compte et configurer des notifications push.  

Si vous utilisez Microsoft Authenticator pour votre compte professionnel ou scolaire, votre organisation décide si des notifications de tooallow en un clic.

### <a name="do-one-click-push-notifications-work-for-non-microsoft-accounts"></a>Les notifications push en un clic fonctionnent-elles pour les comptes non Microsoft ?
Non, les notifications push fonctionnent uniquement avec les comptes Microsoft et Azure Active Directory. Si votre entreprise ou école utilise des comptes Azure AD, vous pouvez désactiver cette fonctionnalité.  

### <a name="i-restored-my-device-from-a-backup-and-my-account-codes-are-missing-or-not-working-what-happened"></a>J’ai restauré mon appareil à partir d’une sauvegarde, et les codes de mon compte sont manquants ou ne fonctionnent pas. Que s’est-il passé ?
Pour des raisons de sécurité, nous ne restaurons pas les comptes à partir de sauvegardes d’application.  Après avoir restauré application hello, supprimez vos comptes et les ajouter à nouveau.

### <a name="i-got-a-new-device-how-do-i-remove-hello-microsoft-authenticator-app-from-my-old-device-and-move-toohello-new-one"></a>Je possède un nouvel appareil. Comment supprimer l’application de Microsoft Authenticator hello à partir de mon appareil ancien et déplacer toohello nouveau ?
Ajout hello Microsoft Authenticator tooa nouveau périphérique d’application ne supprime pas automatiquement qu’il de tous les autres périphériques. toomanage les périphériques sont configurés pour votre compte, visitez hello même site Web que vous utilisez la vérification en deux étapes de toomanage, choisissez tooremove anciennes applications.

Pour les comptes Microsoft personnels, ce site web correspond à votre page [sécurité du compte](https://account.microsoft.com/security). Pour les comptes Microsoft professionnels ou scolaires, ce site web peut être [MyApps](https://myapps.microsoft.com) ou un portail personnalisé que votre organisation a configuré.

### <a name="how-do-i-remove-an-account-from-hello-app"></a>Comment supprimer un compte à partir de l’application hello ?
* iOS : à partir de l’écran principal de hello, balayez vers la gauche sur une vignette de compte. Sélectionnez **Supprimer**.
* Windows Phone : À partir de l’écran principal de hello, sélectionnez bouton de menu hello, puis **modifier les comptes**. Appuyez sur hello **X** nom de compte suivant toohello.
* Android : À partir de l’écran principal de hello, sélectionnez bouton de menu hello, puis **modifier les comptes**. Appuyez sur hello **X** nom de compte suivant toohello.

Si vous avez un appareil qui est inscrit auprès de votre organisation, vous devrez peut-être toocomplete un tooremove étape supplémentaire de votre compte. Sur ces appareils, application de Microsoft Authenticator hello est automatiquement enregistrée en tant qu’administrateur d’un appareil. Si vous souhaitez toocompletely désinstallation hello application, vous devez toofirst annuler l’inscription d’application hello dans les paramètres de l’application hello.

### <a name="why-does-hello-app-request-so-many-permissions"></a>Pourquoi application hello ne demande pas les autorisations autant ?
Voici une liste complète des autorisations, que nous pouvons également demander et comment elles sont utilisées dans l’application hello. vous consultez des autorisations spécifiques Hello dépendent de type hello de téléphone que vous avez.

* **Appareil photo**: nous utilisons vos codes tooscan QR de caméra lorsque vous ajoutez un travail, l’école ou un compte non Microsoft.
* **Contacts et phone**: lorsque vous vous connectez avec votre compte Microsoft personnel, nous essayons de processus de hello toosimplify en recherchant des comptes existants que vous utilisez sur votre téléphone.
* **SMS**: lorsque vous vous connectez avec votre compte Microsoft personnel pour hello première fois, nous avons toomake sûr que vos correspondances de numéro de téléphone hello une sur l’enregistrement. Nous envoyons un téléphone toohello de message texte où vous avez téléchargé l’application hello. message de salutation contient un code de vérification de 6 à 8 chiffres. Au lieu de vous demander toofind ce code et entrez-le dans l’application hello, nous trouver dans le message de texte hello pour vous.
* **Dessiner sur d’autres applications**: lorsque vous recevez une notification tooverify votre identité, nous affichons cette notification via une autre application qui peut être en cours d’exécution.
* **Recevoir des données à partir de hello internet**: cette autorisation est requise pour envoyer des notifications.
* **Prevent phone from sleeping (Empêcher la mise en veille du téléphone)** : si vous enregistrez votre appareil auprès de votre organisation, elle peut modifier cette stratégie sur votre téléphone.
* **Contrôler les vibrations**: vous pouvez choisir si vous souhaitez qu’une vibration lorsque vous recevez une notification tooverify votre identité.
* **Use fingerprint hardware (Utiliser du matériel de détection de l’empreinte digitale** : certains comptes professionnels et scolaires demandent un code PIN supplémentaire chaque fois que vous vérifiez votre identité. toomake hello procédure plus facile, nous vous permettre de toouse votre empreinte digitale au lieu d’entrer hello code confidentiel.
* **Afficher les connexions réseau**: lorsque vous ajoutez un compte Microsoft, application hello requiert la connexion réseau/internet.
* **Lire le contenu de votre stockage hello**: cette autorisation est utilisée uniquement lorsque vous signalez un problème technique via les paramètres de l’application hello. Certaines informations de votre espace de stockage sont collectées problème de hello toodiagnose.
* **Les accès réseau complet**: cette autorisation est requise pour l’envoi de notifications tooverify votre identité.
* **Exécuter au démarrage**: Si vous redémarrez votre téléphone, cette autorisation permet de s’assurer que vous continuez de vous recevez des notifications tooverify votre identité.

### <a name="why-does-hello-microsoft-authenticator-app-allow-you-tooapprove-a-request-without-unlocking-hello-device"></a>Pourquoi hello application d’authentification Microsoft vous permet-elle de tooapprove une demande sans dispositif de déverrouillage hello ?

Vous n’avez pas toounlock que demande de vérification tooapprove de votre appareil, car il vous suffit de tooprove est que vous avez votre téléphone avec vous. La vérification en deux étapes fait appel à deux éléments : un que vous connaissez, et un autre que vous possédez. Hello que vous savez consiste votre mot de passe. chose Hello est votre téléphone (configuré avec l’application de Microsoft Authenticator hello et enregistrée comme une preuve de MFA). Par conséquent, avoir phone de hello et leur approbation demande hello répond aux hello critères pour hello second facteur d’authentification. 

### <a name="what-does-hello-lock-icon-in-hello-account-list-mean"></a>Icône de verrou hello dans la liste des comptes hello signification ?

icône de cadenas Hello indique que hello de l’appareil est inscrit dans Azure AD et enregistré toohello compte. L’inscription de l’appareil pour iOS a lieu lors de l’inscription de Microsoft Intune.

## <a name="next-steps"></a>Étapes suivantes

### <a name="contact-us"></a>Nous contacter
Si votre question n’a pas été ayant obtenu une réponse ici, nous souhaitons toohear de votre part. Accédez toohello [forum d’application Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) toopost votre question get à partir de la Communauté de hello et laisse un commentaire sur cette page.


### <a name="related-topics"></a>Rubriques connexes
* [À propos de la vérification en deux étapes](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) pour les comptes Microsoft
* Vous rencontrez des [difficultés avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md) pour votre compte professionnel ou scolaire ?
* [Utilisez toosign de Microsoft Authenticator hello dans à partir de votre téléphone](microsoft-authenticator-app-phone-signin-faq.md)

