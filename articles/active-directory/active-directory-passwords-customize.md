---
title: "Personnalisation : réinitialisation de mot de passe en libre-service d’Azure AD | Microsoft Docs"
description: "Options de personnalisation pour la réinitialisation de mot de passe libre-service Azure AD"
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
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>Personnaliser les fonctionnalités d’Azure AD pour la réinitialisation de mot en passe libre-service

Recherche de réinitialisation de mot de passe libre-service toodeploy les professionnels de l’informatique peuvent personnaliser hello expérience toomatch leurs utilisateurs.

## <a name="customize-hello-contact-your-administrator-link"></a>Personnaliser les contacts hello votre lien administrateur

Même si les utilisateurs activés SSPR n’est pas toujours un lien « Contactez votre administrateur » sur le mot de passe hello portail de réinitialisation.  Ce lien, vos administrateurs demander de l’assistance à modifier le mot de passe de l’utilisateur hello courriers électroniques. Ce courrier électronique est envoyé à toohello suivant destinataires Bonjour suivant l’ordre :

1. Si hello **administrateur de mot de passe** rôle est attribué, les administrateurs disposant de ce rôle sont notifiés
2. Si aucun mot de passe les administrateurs ne sont affectés, puis les administrateurs avec hello **utilisateur administrateur** rôle sont avertis.
3. Si aucun des rôles précédents de hello assignés, puis **administrateurs globaux** notification

Dans tous les cas, un maximum de 100 destinataires sont informés.

toofind plus d’informations sur hello différents rôles d’administrateur et comment tooassign les voir hello document [attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>Désactiver les e-mails Contactez votre administrateur

Si votre organisation ne souhaite pas que les demandes de réinitialisation de notifier à propos de mot de passe des administrateurs, hello configuration suivante peut être activée

* Activez la réinitialisation du mot de passe en libre-service pour tous les utilisateurs finaux. Cette option se trouve sous **Réinitialisation de mot de passe > Propriétés**.
    * Si vous ne souhaitez pas les utilisateurs tooreset leurs mots de passe, vous pouvez définir l’étendue groupe vide d’accès tooan **nous ne recommandons pas cette option**.
* Personnaliser tooprovide de lien de support technique hello une URL web ou un mailto : adresse que les utilisateurs peuvent utiliser l’assistance de tooget. Cette option se trouve sous **Réinitialisation de mot de passe > Personnalisation > Adresse e-mail ou URL du support technique**.

## <a name="customize-adfs-sign-in-page-for-sspr"></a>Personnaliser la page de connexion AD FS pour SSPR

Les administrateurs des services AD FS peut ajouter une lien tootheir-page de connexion à l’aide des conseils de hello figurant dans l’article de hello [description de la page de connexion ajouter](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).

À l’aide de la commande hello qui suit sur votre serveur AD FS ajoute une page de connexion AD FS lien toohello directement en autorisant les utilisateurs tooenter hello du mot de passe libre-service réinitialisation du workflow.

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a>Personnaliser hello connectez-vous et accès panneau apparence

Lorsque des utilisateurs accèdent à la page de connexion hello, vous pouvez personnaliser le logo hello qui s’affiche avec toofit d’image hello-page de connexion de votre société.

Ces graphiques sont affichés dans hello suivant circonstances :

* Lorsqu’un utilisateur saisit son nom d’utilisateur
* Lorsque l’utilisateur accède à une URL personnalisée
    * Hello de passage de mot de passe « whr » paramètre toohello réinitialiser page, comme « https://login.microsoftonline.com/?whr=contoso.com »
    * En passant hello « nom_utilisateur » un mot de passe toohello paramètre page de réinitialisation, comme « https://login.microsoftonline.com/?username=admin@contoso.com»

### <a name="graphics-details"></a>Détails des éléments visuels

Hello paramètres suivants permettent de caractéristiques visuelles de hello toochange de hello-page de connexion et peut être trouvées sous **Azure Active Directory**, **de personnalisation de la société**, **modifier la société la marque**

* L’image de la page de connexion doit être un fichier PNG ou JPG de 1420 x 1200 pixels et ne dépassant pas 500 ko. Nous vous recommandons toobe environ 200 Ko pour de meilleurs résultats.
* Couleur d’arrière-plan de page de connexion est utilisé sur les connexions à latence élevée et doit être au format hexadécimal de hello RVB.
* L’image de la bannière doit être un fichier PNG ou JPG de 60 x 280 pixels ne dépassant pas 10 Ko.
* Le logo carré (thème normal et foncé) doit être un fichier PNG ou JPG de 240 x 240 (redimensionnable) ne dépassant pas 10 Ko.

### <a name="sign-in-text-options"></a>Options de texte de connexion

Hello suivant les paramètres vous permettre d’organisation tooyour pertinentes de tooadd texte toohello page de connexion. Ces paramètres se trouvent sous **Azure Active Directory**, **Personnalisation de la société**, **Modifier la personnalisation de la société**

* **Indicateur de nom d’utilisateur** remplace hello texte d’exemple de someone@example.com avec un nom plus approprié pour vos utilisateurs, recommandé par défaut de gauche toobe lors de la prise en charge des utilisateurs internes et externes
* Le **Texte de la page de connexion** fait un maximum de 256 caractères. Ce texte s’affiche n’importe où votre nom de connexion des utilisateurs en ligne et Bonjour Azure AD Join d’expérience sur Windows 10. Utilisez ce texte pour les conditions d’utilisation, les instructions et conseils pour vos utilisateurs. **N’importe qui peut voir votre page de connexion, aussi ne fournissez pas d’informations sensibles ici.**

### <a name="keep-me-signed-in-disabled"></a>Désactiver le maintien de la connexion

option de Hello « maintenir la connexion désactivée » permet de tooremain utilisateurs connecté lorsqu’ils fermez et rouvrez la fenêtre du navigateur. Cette option n’affecte pas la durée de vie de session. Ce paramètre se trouve sous **Azure Active Directory > Personnalisation de la société > Modifier la personnalisation de la société**.

Certaines fonctionnalités de SharePoint Online et Office 2010 ont une dépendance sur les utilisateurs vont toocheck en mesure de cette zone. Si vous masquez cette option, les utilisateurs peuvent obtenir des invites de connexion supplémentaires et inattendues.

### <a name="directory-name"></a>Nom de l’annuaire

Vous pouvez modifier les attributs de nom hello sous **Azure Active Directory > Propriétés** tooshow un nom d’organisation convivial apparaît dans le portail de hello et automatisée des communications. Cette option n’est plus visible sous forme de hello d’e-mails automatiques dans les formulaires hello qui suivent

* Nom convivial dans l’e-mail « Microsoft pour le compte de la démonstration CONTOSO »
* Ligne d’objet dans l’e-mail « Code de vérification d’e-mail pour le compte de démonstration CONTOSO »

## <a name="next-steps"></a>Étapes suivantes

Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD

* [**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD. 
* [**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.
* [**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe
* [**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici
* [**Stratégie**](active-directory-passwords-policy.md) : comprenez et définissez les stratégies de mot de passe d’Azure AD
* [**Écriture différée du mot de passe**](active-directory-passwords-writeback.md) : fonctionnement de l’écriture différée du mot de passe avec votre répertoire local.
* [**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service
* [**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement
* [**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ? Pourquoi ? Quoi ? Où ? Qui ? Quand ? -Réponses tooquestions vous souhaitiez toujours tooask
* [**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR

