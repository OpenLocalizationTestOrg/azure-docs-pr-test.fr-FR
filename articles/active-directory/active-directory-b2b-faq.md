---
title: aaaAzure Active Directory B2B collaboration FAQ | Documents Microsoft
description: "Obtenir elles sonttrop des réponses aux questions sur Azure Active Directory B2B collaboration."
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
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>FAQ sur Azure Active Directory B2B Collaboration

Cette Foire aux questions (FAQ) sur la collaboration d’entreprise-entreprise (B2B) Azure Active Directory (Azure AD) sont mises à jour périodiquement tooinclude nouvelles rubriques.

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>Azure AD B2B collaboration n’est disponible dans le portail Azure classic de hello ?
Non. Fonctionnalités de Azure AD B2B collaboration sont uniquement disponibles dans hello [portail Azure](https://portal.azure.com) et Bonjour [volet d’accès](https://myapps.microsoft.com/). 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>Peut-on personnaliser sa page de connexion afin qu’elle soit plus intuitive pour les utilisateurs invités B2B Collaboration ?
Absolument ! Consultez notre [billet de blog sur cette fonctionnalité](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/). Pour plus d’informations sur comment toocustomize votre organisation de l’ouverture de session des pages, consultez [ajouter marque toosign dans et les pages du volet d’accès de l’entreprise](active-directory-add-company-branding.md).

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>Les utilisateurs de B2B Collaboration peuvent-ils accéder à SharePoint Online et OneDrive ?
Oui. Toutefois, toosearch de capacité hello pour les utilisateurs invités existant dans SharePoint Online à l’aide du sélecteur de personnes hello est **hors** par défaut. tooturn sur toosearch d’option hello pour les utilisateurs invités, définissez **ShowPeoplePickerSuggestionsForGuestUsers** trop**sur**. Vous pouvez activer ce paramètre au niveau du client hello ou au niveau de collection de sites hello. Vous pouvez modifier ce paramètre à l’aide des applets de commande Set-SPOTenant et Set-SPOSite hello. Ces applets de commande, membres peuvent rechercher tous les utilisateurs invités existants dans le répertoire de hello. Modifications dans l’étendue de locataire hello n’affectent pas les sites SharePoint Online qui ont déjà été configurés.

### <a name="is-hello-csv-upload-feature-still-supported"></a>Est hello toujours prise en charge de fonctionnalité de téléchargement de volume partagé de cluster ?
Oui. Pour plus d’informations sur l’utilisation de fonctionnalité de téléchargement de fichier .csv hello, consultez [cet exemple PowerShell](active-directory-b2b-code-samples.md).

### <a name="how-can-i-customize-my-invitation-emails"></a>Comment puis-je personnaliser mes e-mails d’invitation ?
Vous pouvez personnaliser presque tout ce qui concerne le processus d’inviter hello à l’aide de hello [B2B invitation API](active-directory-b2b-api.md).

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>Un utilisateur externe invité permettre laisser des organisation hello après à inviter ?
administrateur de l’organisation invitant Hello peut supprimer un utilisateur invité de collaboration B2B à partir de leur annuaire, mais l’utilisateur invité de hello ne peut pas quitter hello invitation d’annuaire de l’organisation par eux-mêmes. 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>Les utilisateurs invités peuvent-ils réinitialiser leur méthode d’authentification multifacteur ?
Oui. Les utilisateurs invités peuvent réinitialiser leur hello de méthode de l’authentification multifacteur que même façon que les utilisateurs standard.

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>Quelle est l’organisation responsable des licences de l’authentification multifacteur ?
organisation d’invitation Hello effectue l’authentification multifacteur. Hello inviter organisation devez vous assurer que les organisation hello détient de suffisamment de licences pour leurs utilisateurs B2B qui utilisent l’authentification multifacteur.

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>Que se passe-t-il si une organisation partenaire a déjà configuré l’authentification multifacteur ? Pouvons-nous faire confiance à son authentification multifacteur et ne pas utiliser notre propre authentification multifacteur ?
Cette fonctionnalité est prévue pour une version ultérieure, afin que vous pouvez ensuite sélectionner tooexclude de partenaires spécifiques à partir de l’authentification multifacteur (hello inviter de votre organisation).

### <a name="how-can-i-use-delayed-invitations"></a>Comment utiliser les invitations différées ?
Une organisation peut que les utilisateurs de tooadd B2B collaboration, configurez-les tooapplications en fonction des besoins et ensuite envoyer des invitations. Vous pouvez utiliser hello B2B collaboration invitation API toocustomize hello d’intégration du flux de travail.

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>Peut-on faire d’un utilisateur invité un administrateur limité ?
Absolument. Pour plus d’informations, consultez [rôle de tooa utilisateurs ajout invité](active-directory-users-assign-role-azure-portal.md).

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>Azure AD B2B collaboration autorise-t-elle B2B utilisateurs tooaccess hello portail Azure ?
Sauf si un utilisateur est affecté le rôle hello limité administrateur ou administrateur général, les utilisateurs de collaboration B2B ne nécessitent pas accès toohello portail Azure. Toutefois, B2B collaboration accessibles aux utilisateurs ayant le rôle administrateur limité ou administrateur général hello portal de hello. En outre, si un utilisateur invité qui n’est pas affecté un de ces rôles d’administrateur accède au portail de hello, hello utilisateur devra peut-être en mesure de tooaccess certaines parties de hello expérience. rôle d’utilisateur invité Hello a des autorisations dans le répertoire de hello.

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>Puis-je bloquer l’accès toohello portail Azure pour les utilisateurs invités ?
Oui. Lorsque vous configurez cette stratégie, être prudent tooavoid bloquer par accident toomembers d’accès et les administrateurs.
tooblock un utilisateur invité accéder toohello [portail Azure](https://portal.azure.com), utilisez une stratégie d’accès conditionnel dans hello API de modèle de déploiement classique de Windows Azure :
1. Modifier hello **tous les utilisateurs** pour qu’il contienne uniquement les membres de groupe.
  ![modifier la capture d’écran de groupe hello](media/active-directory-b2b-faq/modify-all-users-group.png)
2. Créez un groupe dynamique contenant des utilisateurs invités.
  ![capture d’écran - créer un groupe](media/active-directory-b2b-faq/group-with-guest-users.png)
3. Vous pouvez configurer un utilisateur invité de l’accès conditionnel stratégie tooblock d’accéder au portail de hello, comme indiqué dans les éléments suivants de hello vidéo :
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>Azure AD B2B Collaboration prend-il en charge l’authentification multifacteur et les comptes de messagerie grand public ?
Oui. Les comptes de messagerie grand public et l’authentification multifacteur sont tous deux pris en charge par Azure AD B2B Collaboration.

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>Prévoyez-vous de toosupport de mot de passe réinitialisé pour les utilisateurs Azure AD B2B collaboration ?
Oui. Obtenir des informations importantes hello pour la réinitialisation du mot de passe libre-service (SSPR) pour un utilisateur est invité à partir d’une organisation partenaire B2B sont :
 
* SSPR se produit uniquement dans le locataire d’identité hello d’utilisateur de B2B hello.
* Si le client d’identité hello est un compte Microsoft, le compte Microsoft mécanisme SSPR de hello est utilisé.
* Si le client d’identité hello est un juste-à-temps (JIT) ou de client « viral », un message électronique de réinitialisation du mot de passe est envoyé.
* Pour les autres clients, les processus SSPR standard hello sont suivi pour les utilisateurs de B2B. Comme membre SSPR pour les utilisateurs de B2B, dans le contexte de hello de ressource de hello, l’architecture mutualisée est bloquée. 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>La réinitialisation du mot de passe est-elle disponible pour les utilisateurs invités dans un locataire « viral » ou juste-à-temps (JIT) et qui ont accepté des invitations par le biais d’une adresse e-mail scolaire ou professionnelle, mais qui n’avaient pas de compte Azure AD préexistant ?
Oui. Un message de réinitialisation de mot de passe peut être envoyé qui permet une tooreset utilisateur son mot de passe dans l’architecture mutualisée de hello JIT.

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>Microsoft Dynamics CRM fournit-il un support en ligne pour Azure AD B2B Collaboration ?
Actuellement, Microsoft Dynamics CRM ne fournit pas de support en ligne pour Azure AD B2B Collaboration. Toutefois, nous prévoyons de toosupport cela Bonjour futures.

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>Quelle est la durée de vie de hello d’un mot de passe initial pour un utilisateur de collaboration B2B nouvellement créé ?
Azure AD a un ensemble fixe de type caractère, force de mot de passe et les exigences de verrouillage du compte qui s’appliquent également les comptes d’utilisateur cloud tooall Azure AD. Les comptes d’utilisateur cloud sont des comptes qui ne sont pas fédérés avec un autre fournisseur d’identité, comme 
* Compte Microsoft
* Facebook
* Services de fédération Active Directory (AD FS)
* Un autre locataire cloud (pour B2B Collaboration)

Pour les comptes fédérés, stratégie de mot de passe dépend de stratégie hello appliquée dans les paramètres de compte Microsoft hello local location et hello l’utilisateur.

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>Une organisation pourriez toohave différentes expériences dans leurs applications pour les utilisateurs de client et les utilisateurs invités. Une assistance standard est-elle disponible pour cela ? Est la présence de hello de hello identité fournisseur revendication hello modèle correct toouse ?
 Un utilisateur invité peut utiliser n’importe quel tooauthenticate de fournisseur d’identité. Pour plus d’informations, consultez la page [Propriétés d’un utilisateur B2B Collaboration](active-directory-b2b-user-properties.md). Hello d’utilisation **UserType** toodetermine de l’expérience utilisateur de propriété. Hello **UserType** revendication n’est pas actuellement pas incluse dans le jeton de hello. Applications doivent utiliser le répertoire de hello tooquery hello API Graph pour l’utilisateur de hello et tooget hello UserType.

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>Où puis-je trouver un tooshare de communauté B2B collaboration solutions et des idées de toosubmit ?
Nous tenons constamment des commentaires tooyour, tooimprove B2B collaboration. Nous vous invitons à vous tooshare votre utilisateur scénarios, les meilleures pratiques et ce qui vous plaît dans Azure AD B2B collaboration. Participez à hello discussion Bonjour [communauté technique de Microsoft](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).
 
Nous vous invitons également vous toosubmit vos idées et le vote pour des fonctionnalités futures au [B2B Collaboration idées](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas).

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>Quelle adresse pouvons-nous envoyer une invitation qui est échangé automatiquement, afin que hello utilisateur est simplement « prêt toogo » ? Ou hello toujours a-t-il tooclick via une URL de remboursement toohello ?
Envoyé par un utilisateur dans hello invitation d’entreprise, qui est également un membre de l’organisation partenaire de hello ne nécessite pas d’échange est requis par l’utilisateur de B2B hello.

Il est recommandé que vous invitez un utilisateur à partir de hello de toojoin hello partenaire organisation invitation d’organisation. [Ajouter ce rôle d’émetteur de l’invitation toohello utilisateur invité dans l’organisation de ressource hello](active-directory-b2b-add-guest-to-role.md). Cet utilisateur peut inviter d’autres utilisateurs dans l’organisation partenaire de hello en utilisant l’authentification hello dans l’interface utilisateur, des scripts PowerShell, ou des API. Ensuite, les utilisateurs de collaboration B2B à partir de cette organisation ne sont pas requis tooredeem leur invitation.

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>Comment B2B collaboration fonctionne lorsque les partenaires hello invité utilise fédération tooadd leur propre authentification locale ?
Si le partenaire de hello possède un locataire Azure AD fédéré toohello infrastructure de l’authentification locale, localement l’authentification unique (SSO) s’effectue automatiquement. Si le partenaire de hello n’a pas un locataire Azure AD, un compte Azure AD est créé pour les nouveaux utilisateurs. 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>Je pensais qu’Azure AD B2B n’acceptait pas les adresses de messagerie gmail.com et outlook.com, et que B2C était utilisé pour ces types de comptes ?
Nous allons supprimer les différences hello B2B et de collaboration de (B2C) d’entreprise à l’autre les identités sont pris en charge. identité Hello utilisée n’est pas un toochoose une bonne raison entre B2B et l’utilisation de B2C. Pour plus d’informations sur le choix de l’option de collaboration, consultez la page [Comparer B2C et B2B Collaboration dans Azure Active Directory](active-directory-b2b-compare-b2c.md).

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>Quelles applications et services prennent en charge les utilisateurs invités Azure B2B ?
Toutes les applications intégrées à Azure AD prennent en charge les utilisateurs invités Azure B2B. 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>Pouvons-nous forcer l’authentification multifacteur pour les utilisateurs invités B2B si nos partenaires n’ont pas l’authentification multifacteur ?
Oui. Pour plus d’informations, consultez la page [Accès conditionnel pour les utilisateurs B2B Collaboration](active-directory-b2b-mfa-instructions.md).

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>Dans SharePoint, il est possible de définir une liste « allow (autoriser) » ou « deny (refuser) » pour les utilisateurs externes. Peut-on faire cela dans Azure ?
Oui. Azure AD B2B Collaboration prend en charge les listes autorisées et refusées. 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>Que faire licences nous devons toouse Azure AD B2B ?
Pour plus d’informations sur les licences de votre organisation doit toouse Azure AD B2B, consultez [collaboration Azure Active Directory B2B Gestionnaire de licences des conseils](active-directory-b2b-licensing.md).

### <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Comment les administrateurs Azure AD ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-admin-add-users.md)
* [Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-iw-add-users.md)
* [éléments Hello Hello e-mail d’invitation B2B collaboration](active-directory-b2b-invitation-email.md)
* [Utilisation d’une invitation B2B Collaboration](active-directory-b2b-redemption-experience.md)
* [Attribution de licences Azure AD B2B Collaboration](active-directory-b2b-licensing.md)
* [Résolution des problèmes d’Azure AD B2B Collaboration](active-directory-b2b-troubleshooting.md)
* [API et personnalisation d’Azure AD B2B Collaboration](active-directory-b2b-api.md)
* [Authentification multifacteur pour les utilisateurs B2B Collaboration](active-directory-b2b-mfa-instructions.md)
* [Ajouter des utilisateurs B2B Collaboration sans invitation](active-directory-b2b-add-user-without-invite.md)
* [Index d’articles pour la gestion des applications dans Azure AD](active-directory-apps-index.md)
