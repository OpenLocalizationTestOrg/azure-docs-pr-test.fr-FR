---
title: "Azure AD : inscription SSPR | Microsoft Docs"
description: "Inscrire les données d’authentification en vue de la réinitialisation de mot de passe en libre-service Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: dfcd0106616218c84d23920b124bed5b202cdd6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="register-for-self-service-password-reset"></a>S’inscrire à la réinitialisation de mot de passe en libre-service

> [!IMPORTANT]
> **Rencontrez-vous des problèmes de connexion ?** Dans ce cas, [voici comment vous pouvez modifier et réinitialiser votre mot de passe](active-directory-passwords-update-your-own-password.md).

En tant qu’un utilisateur final, vous pouvez réinitialiser votre mot de passe ou déverrouiller votre compte sans avoir personne de tooa toospeak à l’aide de la réinitialisation du mot de passe libre-service (SSPR). Avant de pouvoir utiliser cette fonctionnalité, vous disposez des méthodes d’authentification tooregister ou confirmez votre administrateur a renseigné les méthodes d’authentification hello prédéfinie.

## <a name="register-or-confirm-authentication-data-with-sspr"></a>Inscrire ou confirmer les données d’authentification avec SSPR

1. Navigateur hello ouvert sur votre toohello dispositif et accédez [inscription page de réinitialisation de mot de passe](http://aka.ms/ssprsetup)
2. Entrez le nom d’utilisateur et le mot de passe qui vous ont été fournis par votre administrateur.
3. Selon la manière dont votre personnel informatique avez configuré les choses, un ou plusieurs des éléments suivants de hello options sont disponibles pour vous tooconfigure et vérifient. Votre administrateur peut remplir certaines de ces vous s’ils ont vos informations d’autorisation toouse hello.
    * Téléphone de bureau est uniquement en mesure de toobe définie par votre administrateur
    * Téléphone d’authentification doit être défini de numéro de téléphone tooanother vous auriez accès toolike un téléphone portable qui peut recevoir un appel ou texte.
    * E-mail d’authentification doit être définie tooan autre adresse de messagerie que vous pouvez accéder sans mot de passe hello, vous devez tooreset.
    * Les Questions de sécurité vous donne la liste de questions que votre administrateur a approuvé pour vous tooanswer. Vous ne pouvez pas utiliser hello même question ou de répondre à plusieurs fois.
4. Fournir et vérifiez les informations de hello requises par votre administrateur. Si plusieurs options sont disponibles, nous vous suggérons de que vous inscrivez une grande souplesse de plusieurs méthodes tooprovide lorsqu’une autre méthode n’est pas disponible (exemple : tooaccess en déplacement et ne peut pas votre téléphone de bureau)

    ![Inscrire des méthodes d’authentification et cliquer sur Terminer][Register]

5. Quand vous avez terminé l’étape 4 Choisissez **Terminer** et vous serez en mesure de toouse mot de passe libre-service réinitialiser lorsque vous avez besoin tooin hello futures.

Si vous entrez des données dans hello téléphone d’authentification ou l’E-mail d’authentification, il n’est pas visible dans le répertoire global de hello. Hello seules les personnes qui peuvent voir ces données sont vous et vos administrateurs. Vous seul pouvez voir hello répond à des Questions de sécurité tooyour.

Les administrateurs peuvent nécessiter vous tooconfirm vos méthodes d’authentification après une période de toomake fois que vous disposez toujours les méthodes appropriées hello inscrit.

## <a name="common-problems-and-their-solutions"></a>Problèmes courants et leurs solutions

 Voici quelques cas d'erreur courants et leurs solutions :

| Cas d’erreur| Quelle erreur voyez-vous ?| Solution |
| --- | --- | --- |
| J’obtiens une page « Veuillez contacter votre administrateur » après avoir entré mon identifiant utilisateur. | Veuillez contacter votre administrateur. <br> <br> Nous avons détecté que votre mot de passe de compte d'utilisateur n'est pas géré par Microsoft. Par conséquent, nous ne pouvons pas tooautomatically réinitialiser votre mot de passe. <br> <br> Vous avez besoin de toocontact votre personnel informatique pour plus d’informations. | Vous voyez ce message, car votre personnel informatique gère votre mot de passe dans votre environnement local et ne vous autorise pas tooreset votre mot de passe à partir de la ne peut pas accéder au lien avec votre compte. <br> <br> tooreset votre mot de passe, contactez votre service informatique personnel directement pour aider à et leur permettre de savoir vous tooreset votre mot de passe afin qu’ils peuvent activer cette fonctionnalité pour vous.|
| J'obtiens une erreur « Votre compte n'est pas activé pour la réinitialisation de mot de passe » après avoir entré mon identifiant utilisateur. | Votre compte n’est pas activé pour la réinitialisation du mot de passe <br> <br> Nous sommes désolés, mais votre service informatique n’a pas configuré votre compte pour utiliser ce service. <br> <br> Si vous le souhaitez, nous pouvons contacter un administrateur dans votre organisation de tooreset votre mot de passe pour vous. | Vous voyez ce message, car votre service informatique n’a pas activé le mot de passe réinitialisé pour votre organisation à partir de la ne peut pas accéder au lien avec votre compte, ou n’a pas de licence fonctionnalité de hello toouse. <br> <br> tooreset votre mot de passe, cliquez sur le contact un toosend de lien administrateur une société tooyour de courrier électronique du personnel informatique et leur permettre de vous comptez tooreset votre mot de passe afin qu’ils peuvent activer cette fonctionnalité pour vous. |
| J'obtiens une erreur « Impossible de vérifier votre compte » après avoir entré mon identifiant utilisateur. | Impossible de vérifier votre compte <br> <br> Si vous le souhaitez, nous pouvons contacter un administrateur dans votre organisation de tooreset votre mot de passe pour vous. | Vous voyez ce message, car vous sont activées pour la réinitialisation du mot de passe, mais vous n’êtes pas inscrit de service de hello toouse. tooregister mot de passe réinitialisé, accédez toohttp://aka.ms/ssprsetup une fois que vous avez récupéré tooyour compte d’accès. <br> <br> tooreset votre mot de passe, cliquez sur le contact à un administrateur lien toosend une société tooyour de courrier électronique personnel informatique. |

## <a name="next-steps"></a>Étapes suivantes

* [Comment toochange réinitialiser votre mot de passe à l’aide du mot de passe libre-service](active-directory-passwords-update-your-own-password.md)
* [Page relative à l’inscription à la réinitialisation de mot de passe](http://aka.ms/ssprsetup)
* [Portail de réinitialisation de mot de passe](https://passwordreset.microsoftonline.com/)
* [Impossible de se connecter tooyour compte Microsoft](https://support.microsoft.com/help/12429/microsoft-account-sign-in-cant)

[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "Page relative à l’inscription à la réinitialisation de mot de passe, montrant les méthodes inscrites et le bouton Terminer"

