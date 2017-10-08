---
title: "Azure Active Directory B2C : configuration du jeton, de la session et de l’authentification unique | Microsoft Docs"
description: "Configuration du jeton, de la session et de l’authentification unique dans Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a>Azure Active Directory B2C : configuration du jeton, de la session et de l’authentification unique
Cette fonctionnalité vous donne un contrôle précis, [par stratégie](active-directory-b2c-reference-policies.md), de ce qui suit :

1. Durées de vie des jetons de sécurité émis par Azure Active Directory (Azure AD) B2C.
2. Durées de vie des sessions d’applications web gérées par Azure AD B2C.
3. Formats de revendications importantes dans les jetons de sécurité hello émis par Azure AD B2C.
4. Comportement de l’authentification unique (SSO) entre plusieurs applications et stratégies dans votre client B2C.

Vous pouvez utiliser cette fonctionnalité dans votre client B2C comme suit :

1. Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
2. Cliquez sur **Stratégies d’authentification**. *Remarque : vous pouvez utiliser cette fonctionnalité avec n’importe quel type de stratégie, pas seulement les **stratégies de connexion***.
3. Ouvrez une stratégie en cliquant dessus. Par exemple, cliquez sur **B2C_1_SiIn**.
4. Cliquez sur **modifier** haut hello du Panneau de hello.
5. Cliquez sur **Configuration du jeton, de la session et de l’authentification unique**.
6. Apportez les modifications voulues. Apprenez-en plus sur les propriétés disponibles dans les sections suivantes.
7. Cliquez sur **OK**.
8. Cliquez sur **enregistrer** haut hello du Panneau de hello.

## <a name="token-lifetimes-configuration"></a>Configuration de la durée de vie des jetons
Prend en charge de Azure AD B2C hello [protocole d’autorisation OAuth 2.0](active-directory-b2c-reference-protocols.md) pour l’activation de sécuriser l’accès aux ressources de tooprotected. tooimplement cette prise en charge, Azure AD B2C émet divers [les jetons de sécurité](active-directory-b2c-reference-tokens.md). Voici les propriétés de hello que vous pouvez utiliser toomanage de durées de vie des jetons de sécurité émis par Azure AD B2C :

* **Durées de vie (minutes) du jeton accès & ID**: durée de vie hello de hello OAuth 2.0 support toogain utilisé jeton accès tooa une ressource protégée. À ce stade, Azure AD B2C émet uniquement des jetons d’ID. Cette valeur s’appliquera jetons tooaccess, lorsque nous ajoutons leur prise en charge.
  * Par défaut : 60 minutes.
  * Valeur minimale (inclusive) : 5 minutes.
  * Valeur maximale (inclusive) : 1 440 minutes.
* **Durée de vie de jeton d’actualisation (jours)**: hello durée maximale avant laquelle un jeton d’actualisation peut être utilisé tooacquire un nouvel accès ou le jeton d’ID (et éventuellement, un nouveau jeton d’actualisation, si votre application a été accordée hello `offline_access` étendue).
  * Par défaut : 14 jours.
  * Valeur minimale (inclusive) : 1 jour.
  * Valeur maximale (inclusive) : 90 jours.
* **Actualiser le jeton durée de vie de fenêtre glissante (jours)**: une fois cet période écoulée utilisateur hello toore forcé-authentifier, quel que soit la période de validité de hello du dernier jeton d’actualisation hello acquis par l’application hello. Il peut uniquement être fourni si la valeur du commutateur de hello est trop**Bounded**. Doit être toobe supérieur ou égal toohello **actualisation durée de vie (jours)** valeur. Si la valeur du commutateur de hello est trop**Unbounded**, vous ne pouvez pas fournir une valeur spécifique.
  * Par défaut : 90 jours.
  * Valeur minimale (inclusive) : 1 jour.
  * Valeur maximale (inclusive) : 365 jours.

Voici quelques cas d’usage que vous pouvez activer à l’aide de ces propriétés :

* Autoriser un toostay de l’utilisateur connecté à une application mobile indéfiniment, tant qu’il est actif en permanence dans l’application hello. Cela en définissant un hello **actualisation glissante fenêtre durée de vie (jours)** basculer trop**Unbounded** dans votre stratégie d’authentification.
* Répondre aux exigences de conformité et de sécurité de votre secteur en définissant la durée de vie des jetons d’hello accès appropriés.

    > [!NOTE]
    > Ces paramètres ne sont pas disponibles pour les stratégies de réinitialisation de mot de passe.
    > 
    > 

## <a name="token-compatibility-settings"></a>Paramètres de conformité de jeton
Nous avons simplifié la mise en forme revendications tooimportant de modifications dans les jetons de sécurité émis par Azure AD B2C. Cela a été fait tooimprove prise en charge du protocole standard et pour une meilleure interopérabilité avec les bibliothèques d’identité tiers. Toutefois, tooavoid les applications existantes avec rupture, nous avons créé hello suivant propriétés tooallow clients tooopt-en fonction des besoins :

* **Revendication de l’émetteur (iss)**: identifie locataire hello Azure AD B2C qui a émis le jeton de hello.
  * `https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: Il s’agit de valeur par défaut de hello.
  * `https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: Cette valeur inclut l’ID de client de hello B2C et stratégie hello utilisé dans la demande de jeton hello. Si votre application ou une bibliothèque doit Azure AD B2C toobe conforme hello [OpenID Connect 1.0 de découverte spec](http://openid.net/specs/openid-connect-discovery-1_0.html), utilisez cette valeur.
* **Revendication de sujet (sub)**: identifie entité hello, par exemple, les utilisateurs de hello, pour quels hello jeton déclare les informations.
  * **ObjectID**: il s’agit par défaut hello. Il remplit hello ID d’objet de l’utilisateur hello dans le répertoire de hello en hello `sub` de revendication dans le jeton de hello.
  * **Non pris en charge**: il n’est disponible que pour assurer la compatibilité descendante, et nous vous recommandons de passer trop**ObjectID** dès que vous êtes en mesure de.
* **Représentant l’ID de stratégie de revendication**: identifie le type de revendication hello dans le hello ID de stratégie utilisé dans la demande de jeton hello est remplie.
  * **TFP**: il s’agit par défaut hello.
  * **ACR**: il n’est disponible que pour assurer la compatibilité descendante, et nous vous recommandons de passer trop`tfp` dès que vous êtes en mesure de.

## <a name="session-behavior"></a>Comportement de la session
Prend en charge de Azure AD B2C hello [protocole d’authentification OpenID Connect](active-directory-b2c-reference-oidc.md) permet aux applications de tooweb de connexion sécurisée. Voici les propriétés de hello que vous pouvez utiliser des sessions de l’application web toomanage :

* **Durée de vie de session (minutes) l’application Web**: durée de vie de hello du cookie de session du B2C Azure AD stocké sur le navigateur de l’utilisateur hello après une authentification réussie.
  * Par défaut : 1 440 minutes.
  * Valeur minimale (inclusive) : 15 minutes.
  * Valeur maximale (inclusive) : 1 440 minutes.
* **Délai d’expiration de session Web application**: Si ce commutateur est défini trop**absolu**, l’utilisateur hello est forcé toore-authentifier après hello laps de temps spécifié par **Web app, durée de vie de session (minutes)** s’écoule. Si ce commutateur est défini trop**propagées** (hello paramètre par défaut), utilisateur de hello reste connecté tant qu’utilisateur de hello est active en permanence dans votre application web.

Voici quelques cas d’usage que vous pouvez activer à l’aide de ces propriétés :

* Répondre aux exigences de conformité et de sécurité de votre secteur en définissant la session d’application web appropriés hello durées de vie.
* Forcez la réauthentification après une période donnée pendant une interaction utilisateur avec une partie haute sécurité de votre application web. 

    > [!NOTE]
    > Ces paramètres ne sont pas disponibles pour les stratégies de réinitialisation de mot de passe.
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a>Configuration de l’authentification unique
Si vous avez plusieurs applications et les stratégies de votre client B2C, vous pouvez gérer des interactions utilisateur entre eux à l’aide de hello **configuration de l’authentification unique** propriété. Vous pouvez définir tooone de propriété hello Hello suivant les paramètres :

* **Client**: c’est le paramètre par défaut de hello. À l’aide de ce paramètre permet à plusieurs applications et des stratégies de votre client B2C tooshare hello même session de l’utilisateur. Par exemple, lorsqu’un utilisateur se connecte à une application, Contoso Shopping, il peut également se connecter de façon transparente à une autre application, Contoso Pharmacy, lorsqu’il y accède.
* **Application**: ainsi, vous toomaintain une session utilisateur exclusivement pour une application, indépendamment des autres applications. Par exemple, si vous souhaitez toosign d’utilisateur hello dans tooContoso pharmacie (hello avec les mêmes informations d’identification), même si elle est déjà connecté à Contoso d’achat, une autre application hello même locataire B2C. 
* **Stratégie**: ainsi, vous toomaintain une session utilisateur exclusivement pour une stratégie, indépendamment des applications hello à l’utiliser. Par exemple, si hello utilisateur a déjà connecté et terminé une étape de l’authentification Multifacteur facteur multiples, il ou elle peut être attribuée l’accès des parties de toohigher à la sécurité de plusieurs applications tant que stratégie de toohello hello session liée n’expire jamais.
* **Désactivé**: cette opération force toorun d’utilisateur hello via le voyage d’ensemble des utilisateurs hello à chaque exécution de la stratégie de hello. Par exemple, ainsi, plusieurs utilisateurs toosign, application tooyour (dans un scénario bureau partagé), même pendant un seul utilisateur reste connecté au moment de toute hello.

    > [!NOTE]
    > Ces paramètres ne sont pas disponibles pour les stratégies de réinitialisation de mot de passe.
    > 
    > 

