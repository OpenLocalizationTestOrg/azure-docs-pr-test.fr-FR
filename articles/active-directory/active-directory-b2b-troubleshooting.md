---
title: aaaTroubleshooting Azure Active Directory B2B collaboration | Documents Microsoft
description: "Solutions pour les problèmes courants liés à Azure Active Directory B2B Collaboration"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>Résolution des problèmes d’Azure Active Directory B2B Collaboration

Voici des solutions pour les problèmes courants liés à Azure Active Directory (Azure AD) B2B Collaboration.


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a>Vous avez ajouté un utilisateur externe mais ne sont pas visibles dans le carnet d’adresses Global ou dans le sélecteur de personnes hello

Dans les cas où les utilisateurs externes ne sont pas renseignés dans la liste de hello, objet de hello peut prendre quelques minutes tooreplicate.

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>Un utilisateur invité B2B ne s’affiche pas dans le sélecteur de personnes SharePoint Online/OneDrive 
 
toosearch de capacité Hello pour les utilisateurs invités dans le sélecteur de personnes hello SharePoint Online (OFS) est désactivé par défaut hérités toomatch.

Vous pouvez activer cette fonctionnalité à l’aide de hello la définition 'ShowPeoplePickerSuggestionsForGuestUsers' à la collection de site et de client hello niveau. Vous pouvez définir la fonction hello hello Set-SPOTenant et SPOSite de jeu d’applets de commande, qui permettent aux membres toosearch tous les utilisateurs invités existants dans le répertoire de hello. Modifications dans l’étendue de locataire hello n’affectent pas les sites simulé déjà configurés.

## <a name="invitations-have-been-disabled-for-directory"></a>Des invitations ont été désactivées pour le répertoire

Si vous êtes informé que vous n’avez pas les autorisations accordées aux utilisateurs de tooinvite, vérifiez que votre compte d’utilisateur est autorisé tooinvite des utilisateurs externes sous Paramètres utilisateur :

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

Si vous avez récemment modifié ces paramètres ou hello invité le rôle tooa utilisateur attribué, il peut y avoir un délai de 15 à 60 minutes que hello modifications prennent effet.

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a>utilisateur Hello qui vous a invité reçoit une erreur au cours de l’échange

Les erreurs courantes sont les suivantes :

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>L’administrateur de l’invité n’autorise pas la création d’utilisateurs EmailVerified dans leur client

Lorsque invitant les utilisateurs dont l’organisation utilise Azure Active Directory, mais où hello compte d’utilisateur spécifique n’existe pas (par exemple, hello utilisateur n’existe pas dans Azure AD contoso.com). administrateur Hello contoso.com qui peut exister une stratégie empêchant les utilisateurs d’en cours de création. utilisateur de Hello doit vérifier avec leur toodetermine administrateur si des utilisateurs externes sont autorisés. Hello administrateur de l’utilisateur externe peut-être tooallow vérifié par courrier électronique des utilisateurs dans leur domaine (consultez ce [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) sur permettant aux utilisateurs de vérifié par courrier électronique).

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>L'utilisateur externe n’existe pas déjà dans un domaine fédéré

Si vous utilisez l’authentification de la fédération et l’utilisateur de hello n’existe pas déjà dans Azure Active Directory, utilisateur de hello ne peut pas être invité.

tooresolve ce problème, hello administrateur de l’utilisateur externe doit synchroniser tooAzure de compte d’utilisateur hello Active Directory.

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>Comment synchroniser « \# », qui n’est normalement pas un caractère valide, avec Azure AD ?

«\#» est un caractère réservé dans les noms d’utilisateurs principaux pour Azure AD B2B collaboration ou externes, parce que hello invité compte user@contoso.com devient user_contoso.com#EXT@fabrikam.onmicrosoft.com. Par conséquent, \# dans UPN provenant du site ne sont pas autorisés toosign dans toohello portail Azure. 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a>Je reçois une erreur lors de l’ajout d’utilisateurs externes tooa synchronisé de groupe

Les utilisateurs externes peuvent être ajoutés uniquement trop « affecté » ou les groupes « Sécurité » et pas les toogroups sont contrôlées sur site.

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a>Mon utilisateur externe n’a pas reçu un tooredeem par courrier électronique

l’invité de Hello devez vérifier auprès de leur fournisseur de services Internet ou tooensure de filtre de courrier indésirable hello l’adresse suivante est autorisée :Invites@microsoft.com

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>Je remarque que message personnalisé hello n’obtient pas inclus dans les messages d’invitation à des moments

toocomply avec les lois sur la confidentialité, nos API n’inclure pas les messages personnalisés dans le message d’invitation hello lorsque :

- émetteur de l’invitation Hello n’a pas une adresse de messagerie dans hello inviter les clients
- Lorsqu’un principal de service d’applications envoie d’invitation hello

Si ce scénario est tooyou important, vous pouvez supprimer l’e-mail d’invitation de nos API et l’envoyer via le mécanisme de messagerie hello de votre choix. Consultez toomake de conseiller juridique de votre organisation que tout message électronique envoyer de cette façon est également conforme à la législation.

## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-admin-add-users.md)
* [Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-iw-add-users.md)
* [éléments Hello Hello e-mail d’invitation B2B collaboration](active-directory-b2b-invitation-email.md)
* [Utilisation d’une invitation B2B Collaboration](active-directory-b2b-redemption-experience.md)
* [Attribution de licences Azure AD B2B Collaboration](active-directory-b2b-licensing.md)
* [Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration](active-directory-b2b-faq.md)
* [API et personnalisation d’Azure Active Directory B2B Collaboration](active-directory-b2b-api.md)
* [Authentification multifacteur pour les utilisateurs B2B Collaboration](active-directory-b2b-mfa-instructions.md)
* [Ajouter des utilisateurs B2B Collaboration sans invitation](active-directory-b2b-add-user-without-invite.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
