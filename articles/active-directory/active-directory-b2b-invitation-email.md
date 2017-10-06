---
title: "éléments aaaThe d’e-mail d’invitation hello Azure Active Directory B2B collaboration | Documents Microsoft"
description: "Modèle d’e-mail d’invitation de collaboration d’Azure Active Directory B2B"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>éléments Hello Hello e-mail d’invitation B2B collaboration

Des e-mails d’invitation participent un composant essentiel toobring à bord en tant qu’utilisateurs de collaboration B2B dans Azure AD. Vous pouvez les utiliser une confiance tooincrease hello destinataire. Vous pouvez ajouter des légitimité et par courrier électronique toohello preuve sociaux, destinataire de hello que toomake estimez avec sélection hello **prise en main** bouton tooaccept d’invitation hello. Cette approbation est qu'une clé signifie tooreduce friction de partage. Et que vous souhaitez également toomake hello messagerie aspect excellent !

![E-mail d’invitation Azure AD B2b](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>Expliquant par courrier électronique hello
Penchons-nous sur quelques éléments de messagerie de hello afin que vous sachiez comment mieux toouse leurs fonctionnalités.

### <a name="subject"></a>Objet
objet du courrier électronique de hello Hello suit hello suivant le modèle : vous êtes invité toohello &lt;tenantname&gt; organisation

### <a name="from-address"></a>Adresse de l’expéditeur
Nous utilisons un modèle semblable à LinkedIn pour hello à partir de l’adresse.  Vous devez être clair inviter de hello et à partir duquel l’entreprise et également préciser que messagerie hello provient d’une adresse de messagerie de Microsoft. format de Hello est : &lt;nom complet de l’émetteur de l’invitation&gt; de &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>Adresse de réponse
réponse Hello-tooemail est définie par courrier électronique d’inviter toohello lorsqu’il est disponible, afin que vous répondez par courrier électronique toohello envoie un émetteur de toohello précédent l’invitation par courrier électronique.

### <a name="branding"></a>Personnalisation
invitation Hello des messages électroniques à partir de votre client utilisent entreprise hello marque qui vous pouvez avoir configuré pour votre client. Si vous souhaitez parti tootake cette fonctionnalité, [ici](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) hello des détails sur la façon de tooconfigure il. logo de bannière Hello s’affiche dans l’e-mail de hello. Suivez la taille de l’image hello et des instructions de qualité [ici](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) pour de meilleurs résultats. En outre, nom de la société hello apparaît également dans hello appel tooaction.

### <a name="call-tooaction"></a>Appel tooaction
Hello appel tooaction se compose de deux parties : expliquant pourquoi hello destinataire n’a reçu les messages hello et toodo lui a été demandé à ce que destinataire hello.
- Hello la section « Pourquoi » peut être adressée à l’aide de hello modèle : vous avez été applications tooaccess invités Bonjour &lt;tenantname&gt; organisation

- Et hello « qu’il vous est demandé toodo » une section est indiquée par la présence de hello Hello **prise en main** bouton. Lorsque les destinataire hello a été ajouté sans avoir besoin de hello pour les invitations, ce bouton n’apparaît pas.

### <a name="inviters-information"></a>Informations de l’inviteur
nom d’affichage d’inviter Hello est inclus dans le courrier électronique de hello. Et, en outre, si vous avez configuré une image de profil pour votre compte Azure AD, hello invitation par courrier électronique inclut également cette image. Les deux est tooincrease prévue de confiance de votre destinataire par courrier électronique hello.

Si vous n’avez pas encore configuré votre photo de profil, une icône initiales d’inviter hello à la place d’image de hello est indiquée :

  ![afficher les initiales d’inviter hello](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>Corps
corps de Hello contient le message de type hello qu’inviter hello compose ou est passé par le biais d’invitation hello API. Il s’agit d’une simple zone de texte qui ne traite pas les balises HTML pour des raisons de sécurité.

### <a name="footer-section"></a>Section Pied de page
pied de page Hello contient la marque de société Microsoft hello et informe le destinataire de hello si hello a été envoyé depuis un alias non contrôlé. Cas particuliers :

- émetteur de l’invitation Hello n’a pas une adresse de messagerie dans hello invitant l’architecture mutualisée

  ![image de l’émetteur de l’invitation n’a pas une adresse de messagerie dans hello invitant l’architecture mutualisée](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- destinataire de Hello n’a pas besoin d’invitation hello tooredeem

  ![Lorsque destinataire n’a pas besoin d’invitation tooredeem](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-admin-add-users.md)
* [Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-iw-add-users.md)
* [Utilisation d’une invitation B2B Collaboration](active-directory-b2b-redemption-experience.md)
* [Attribution de licences Azure AD B2B Collaboration](active-directory-b2b-licensing.md)
* [Résolution des problèmes d’Azure Active Directory B2B Collaboration](active-directory-b2b-troubleshooting.md)
* [Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration](active-directory-b2b-faq.md)
* [API et personnalisation d’Azure Active Directory B2B Collaboration](active-directory-b2b-api.md)
* [Authentification multifacteur pour les utilisateurs B2B Collaboration](active-directory-b2b-mfa-instructions.md)
* [Ajouter des utilisateurs B2B Collaboration sans invitation](active-directory-b2b-add-user-without-invite.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
