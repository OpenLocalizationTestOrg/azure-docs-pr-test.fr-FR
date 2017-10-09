---
title: "Azure B2C Active Directory : Présentation des stratégies personnalisées de pack de démarrage hello | Documents Microsoft"
description: "Une rubrique sur les stratégies personnalisées Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a>Fonctionnement des stratégies personnalisées hello de pack de démarrage de stratégie personnalisée hello Azure AD B2C

Cette section répertorie tous les éléments de base hello de stratégie hello B2C_1A_base fourni avec hello **Starter Pack** et qui est utilisé pour la création de vos propres stratégies via l’héritage hello Hello *B2C_1A_base_ stratégie d’extensions*.

Par conséquent, il plus particulièrement axé sur hello déjà défini les types, les transformations de revendications, définitions de contenu, les fournisseurs de revendications avec leurs profils techniques de revendication et hello trajets d’utilisateur de base.

> [!IMPORTANT]
> Microsoft n’apporte aucune garantie, expresse ou implicite, avec les informations de toohello égard fournies ci-après. Des modifications peuvent être apportées à tout moment, avant, pendant ou après la mise à la disposition générale.

Vos propres stratégies et les hello B2C_1A_base_extensions stratégie peuvent remplacer ces définitions et étendre cette stratégie parent en fournissant de nouvelles en fonction des besoins.

Hello principaux éléments de hello *B2C_1A_base stratégie* sont des types de revendications, les transformations de revendications et des définitions de contenu. Ces éléments peuvent toobe susceptibles d’être référencé dans vos propres stratégies ainsi que dans hello *B2C_1A_base_extensions stratégie*.

## <a name="claims-schemas"></a>Schéma de revendications

Ce schéma de revendications comprend trois sections :

1.  Première section qui répertorie les revendications minimale hello qui sont requises pour hello utilisateur trajets toowork correctement.
2.  Une deuxième section que listes hello revendications requises pour les paramètres de chaîne de requête et autres toobe paramètres spéciaux passé tooother les fournisseurs de revendications, notamment login.microsoftonline.com pour l’authentification. **Ne modifiez pas ces revendications**.
3.  Et finit par une troisième section qui répertorie toutes les revendications supplémentaires, facultatifs qui peuvent être collectées à partir de l’utilisateur de hello, stocké dans le répertoire de hello et envoyés dans les jetons lors de l’authentification dans. Nouvelles revendications type toobe collectées à partir de l’utilisateur de hello et/ou envoyées dans le jeton de hello peuvent être ajoutées dans cette section.

> [!IMPORTANT]
> schéma de revendications Hello contient des restrictions sur certaines revendications telles que les noms d’utilisateur et mots de passe. Hello stratégie d’approbation d’infrastructure (TF) traite Azure AD comme tout autre fournisseur de revendications et tous ses restrictions sont modélisées dans la stratégie de premium hello. Une stratégie peut être modifiée tooadd plus de restrictions, ou utiliser un autre fournisseur de revendications pour le stockage d’informations d’identification qui disposera de ses propres restrictions.

types de revendications disponibles Hello sont répertoriées ci-dessous.

### <a name="claims-that-are-required-for-hello-user-journeys"></a>Revendications qui sont requises pour les déplacements des utilisateurs hello

Hello suivant les revendications est requise pour utilisateur trajets toowork correctement :

| Type de revendication | Description |
|-------------|-------------|
| *UserId* | Nom d’utilisateur |
| *signInName* | Nom de connexion |
| *tenantId* | Identificateur de client (ID) d’objet utilisateur hello Premium d’Azure AD B2C |
| *objectId* | Identificateur d’objet (ID) de l’objet utilisateur hello Premium d’Azure AD B2C |
| *mot de passe* | Mot de passe |
| *newPassword* | |
| *reenterPassword* | |
| *passwordPolicies* | Stratégies de mot de passe utilisés par la longueur de mot de passe toodetermine Premium d’Azure AD B2C, expiration, etc.. |
| *sub* | |
| *alternativeSecurityId* | |
| *identityProvider* | |
| *displayName* | |
| *strongAuthenticationPhoneNumber* | Numéro de téléphone de l’utilisateur |
| *Verified.strongAuthenticationPhoneNumber* | |
| *email* | Adresse de messagerie qui peut être utilisé toocontact hello utilisateur |
| *signInNamesInfo.emailAddress* | Adresse de messagerie hello utilisateur peut utiliser toosign dans |
| *otherMails* | Adresses de messagerie qui peuvent être utilisé toocontact hello utilisateur |
| *userPrincipalName* | Nom d’utilisateur, tel que stocké dans hello Premium d’Azure AD B2C |
| *upnUserName* | Nom d’utilisateur utilisé pour créer le nom d’utilisateur principal |
| *mailNickName* | Nom d’utilisateur messagerie nick stocké dans hello Premium d’Azure AD B2C |
| *newUser* | |
| *executed-SelfAsserted-Input* | Revendication qui spécifie si les attributs ont été collectées à partir de l’utilisateur de hello |
| *executed-PhoneFactor-Input* | Revendication qui spécifie si un nouveau numéro de téléphone a été collecté à partir de l’utilisateur de hello |
| *authenticationSource* | Spécifie si l’utilisateur de hello a été authentifié au fournisseur d’identité sociaux, login.microsoftonline.com ou compte local |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a>Revendications requises pour les paramètres de chaîne de requête et d’autres paramètres spéciaux

Hello revendications suivantes sont requises toopass sur les fournisseurs de revendications tooother paramètres spéciaux (y compris certains paramètres de chaîne de requête) :

| Type de revendication | Description |
|-------------|-------------|
| *nux* | Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local |
| *nca* | Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local |
| *prompt* | Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local |
| *mkt* | Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local |
| *lc* | Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local |
| *grant_type* | Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local |
| *scope* | Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local |
| *client_id* | Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local |
| *objectIdFromSession* | Paramètre fourni par hello par défaut session gestion fournisseur tooindicate qui hello id d’objet a été récupéré à partir d’une session de l’authentification unique |
| *isActiveMFASession* | Paramètre fourni par tooindicate de gestion de session de l’authentification Multifacteur hello que cet utilisateur hello a une session active de l’authentification Multifacteur |

### <a name="additional-optional-claims-that-can-be-collected"></a>Revendications supplémentaires (facultatives) qui peuvent être collectées

suivant de Hello revendications sont des revendications supplémentaires qui peuvent être collectées auprès des utilisateurs de hello, stocké dans le répertoire de hello et envoyé dans le jeton de hello. Comme avant, des revendications supplémentaires peuvent être ajoutées toothis liste.

| Type de revendication | Description |
|-------------|-------------|
| *givenName* | Prénom de l’utilisateur |
| *surname* | Nom de famille de l’utilisateur |
| *Extension_picture* | Image de l’utilisateur obtenue via les réseaux sociaux |

## <a name="claim-transformations"></a>Transformations de revendication

transformations de revendications disponibles Hello sont répertoriées ci-dessous.

| Transformation de revendication | Description |
|----------------------|-------------|
| *CreateOtherMailsFromEmail* | |
| *CreateRandomUPNUserName* | |
| *CreateUserPrincipalName* | |
| *CreateSubjectClaimFromObjectID* | |
| *CreateSubjectClaimFromAlternativeSecurityId* | |
| *CreateAlternativeSecurityId* | |

## <a name="content-definitions"></a>Définitions de contenu

Cette section décrit les définitions de contenu hello déjà déclarées dans hello *B2C_1A_base* stratégie. Ces définitions de contenu sont susceptibles d’être toobe référencé, substitution et/ou étendue autant que nécessaire dans vos propres stratégies ainsi que dans hello *B2C_1A_base_extensions* stratégie.

| Fournisseur de revendications | Description |
|-----------------|-------------|
| *Facebook* | |
| *Local Account SignIn* | |
| *PhoneFactor* | |
| *Azure Active Directory* | |
| *Self Asserted* | |
| *Local Account* | |
| *Gestion des sessions* | |
| *Trustframework Policy Engine* | |
| *TechnicalProfiles* | |
| *Token Issuer* | |

## <a name="technical-profiles"></a>Profils techniques

Cette section décrit les profils techniques hello déjà déclarés par le fournisseur de revendications Bonjour *B2C_1A_base* stratégie. Ces profils techniques sont susceptibles d’être toobe plus référencée, substitution et/ou étendue autant que nécessaire dans vos propres stratégies ainsi que dans hello *B2C_1A_base_extensions* stratégie.

### <a name="technical-profiles-for-facebook"></a>Profils techniques pour Facebook

| Profil technique | Description |
|-------------------|-------------|
| *Facebook-OAUTH* | |

### <a name="technical-profiles-for-local-account-signin"></a>Profils techniques pour Local Account Signin

| Profil technique | Description |
|-------------------|-------------|
| *Login-NonInteractive* | |

### <a name="technical-profiles-for-phone-factor"></a>Profils techniques pour PhoneFactor

| Profil technique | Description |
|-------------------|-------------|
| *PhoneFactor-Input* | |
| *PhoneFactor-InputOrVerify* | |
| *PhoneFactor-Verify* | |

### <a name="technical-profiles-for-azure-active-directory"></a>Profils techniques pour Azure Active Directory

| Profil technique | Description |
|-------------------|-------------|
| *AAD-Common* | Profil technique inclus par hello autres profils techniques AAD-xxx |
| *AAD-UserWriteUsingAlternativeSecurityId* | Profil technique pour les connexions via les réseaux sociaux |
| *AAD-UserReadUsingAlternativeSecurityId* | Profil technique pour les connexions via les réseaux sociaux |
| *AAD-UserReadUsingAlternativeSecurityId-NoError* | Profil technique pour les connexions via les réseaux sociaux |
| *AAD-UserWritePasswordUsingLogonEmail* | Profils techniques pour les comptes locaux |
| *AAD-UserReadUsingEmailAddress* | Profils techniques pour les comptes locaux |
| *AAD-UserWriteProfileUsingObjectId* | Profil technique pour la mise à jour de l’enregistrement utilisateur à l’aide de l’ID d’objet |
| *AAD-UserWritePhoneNumberUsingObjectId* | Profil technique pour la mise à jour de l’enregistrement utilisateur à l’aide de l’ID d’objet |
| *AAD-UserWritePasswordUsingObjectId* | Profil technique pour la mise à jour de l’enregistrement utilisateur à l’aide de l’ID d’objet |
| *AAD-UserReadUsingObjectId* | Profil technique donnée tooread utilisée une fois que l’utilisateur s’authentifie |

### <a name="technical-profiles-for-self-asserted"></a>Profils techniques pour Self Asserted

| Profil technique | Description |
|-------------------|-------------|
| *SelfAsserted-Social* | |
| *SelfAsserted-ProfileUpdate* | |

### <a name="technical-profiles-for-local-account"></a>Profils techniques pour Local Account

| Profil technique | Description |
|-------------------|-------------|
| *LocalAccountSignUpWithLogonEmail* | |

### <a name="technical-profiles-for-session-management"></a>Profils techniques pour Session Management

| Profil technique | Description |
|-------------------|-------------|
| *SM-Noop* | |
| *SM-AAD* | |
| *SM-SocialSignup* | Nom du profil est en cours de la session d’AAD toodisambiguate utilisé entre le signe des et se connecter |
| *SM-SocialLogin* | |
| *SM-MFA* | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a>Profils techniques pour Trustframework Policy Engine TechnicalProfiles

Actuellement, aucun profil technique n’est définis pour hello **Trustframework stratégie moteur TechnicalProfiles** fournisseur de revendications.

### <a name="technical-profiles-for-token-issuer"></a>Profils techniques pour Token Issuer

| Profil technique | Description |
|-------------------|-------------|
| *JwtIssuer* | |

## <a name="user-journeys"></a>Parcours utilisateur

Cette section décrit le parcours d’utilisateur hello déjà déclarés dans hello *B2C_1A_base* stratégie. Ces parcours de l’utilisateur sont susceptibles d’être toobe plus référencée, substitution et/ou étendue autant que nécessaire dans vos propres stratégies ainsi que dans hello *B2C_1A_base_extensions* stratégie.

| Parcours utilisateur | Description |
|--------------|-------------|
| *SignUp* | |
| *SignIn* | |
| *SignUpOrSignIn* | |
| *EditProfile* | |
| *PasswordReset* | |
