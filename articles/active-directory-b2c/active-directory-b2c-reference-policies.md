---
title: "Azure Active Directory B2C : stratégies intégrées | Microsoft Docs"
description: "Une rubrique sur l’infrastructure de stratégie extensible hello d’Azure Active Directory B2C et sur la façon toocreate différents types de stratégie"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a>Azure Active Directory B2C: stratégies intégrées


infrastructure de stratégie extensible Hello de B2C d’Azure Active Directory (Azure AD) est la force du noyau de hello du service de hello. Les stratégies décrivent entièrement les expériences relatives à l’identité des consommateurs, telles que l’inscription, la connexion ou la modification de profil. Par exemple, une stratégie d’inscription vous permet des comportements toocontrol en hello suivant les paramètres de configuration :

* Types (comptes sociaux tels que Facebook) ou les comptes locaux, tels que les adresses de messagerie que les utilisateurs peuvent utiliser toosign pour une application hello de comptes
* Attributs (par exemple, prénom, code postal, pointure) toobe collectées à partir de consommateur de hello pendant l’inscription
* utilisation d’Azure Multi-Factor Authentication ;
* Hello apparence et la convivialité de toutes les pages d’inscription
* Reçoit des informations (qui se manifeste en tant que revendications dans un jeton) hello application issue de la stratégie hello exécuter

Vous pouvez créer plusieurs stratégies de types différents dans votre client et les utiliser dans vos applications en fonction des besoins. Les stratégies peuvent être réutilisées entre les différentes applications. Cette flexibilité permet aux développeurs toodefine et modifier des expériences d’identité consommateur avec peu ou aucun code tootheir de modifications.

Les stratégies sont disponibles à l'utilisation par le biais d'une interface développeur simple. Votre application déclenche une stratégie à l’aide d’une demande d’authentification HTTP standard (en passant un paramètre de stratégie de demande de hello) et reçoit un jeton personnalisé en tant que réponse. Par exemple, hello seule différence entre les demandes qui font appel à une stratégie d’inscription et les demandes qui font appel à une stratégie d’authentification est nom de la stratégie hello qui est utilisé dans le paramètre de chaîne de requête hello « p » :

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

Pour plus d’informations sur l’infrastructure de stratégie hello, consultez [ce billet de blog sur B2C d’Active Directory de Azure sur hello mobilité d’entreprise et le Blog de sécurité](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).

## <a name="create-a-sign-up-or-sign-in-policy"></a>Création d’une stratégie d’inscription ou de connexion

Cette stratégie gère les expériences d’inscription et de connexion des utilisateurs avec une configuration unique. Les consommateurs sont dirigées vers le bas hello chemin d’accès correct (inscription ou connectez-vous) selon le contexte de hello. Elle décrit également le contenu hello de jetons qui reçoit les inscriptions réussies ou connexions application hello.  Un exemple de code pour la stratégie d’inscription ou connectez-vous hello est [disponible ici](active-directory-b2c-devquickstarts-web-dotnet-susi.md).  Il est recommandé d’utiliser cette stratégie plutôt qu’une stratégie d’inscription et de connexion.  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a>Création d’une stratégie d’inscription

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a>Création d’une stratégie de connexion

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a>Création d’une stratégie de modification de profil

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a>Création d’une stratégie de réinitialisation du mot de passe

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a>Forum Aux Questions

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a>Comment lier une stratégie d’inscription ou de connexion à une stratégie de réinitialisation de mot de passe ?
Lorsque vous créez une stratégie d’inscription ou de la connexion (avec des comptes locaux), vous voyez un **mot de passe oublié ?** lien sur la première page de hello d’expérience de hello. Cliquer sur ce lien ne déclenche pas automatiquement une stratégie de réinitialisation de mot de passe. 

Au lieu de cela, hello code d’erreur  **`AADB2C90118`**  est retourné tooyour application. Votre application doit toohandle ce code d’erreur en appelant une stratégie de réinitialisation de mot de passe spécifiques. Pour plus d’informations, consultez un [exemple qui illustre l’approche hello de liaison des stratégies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a>Dois-je utiliser une stratégie d’inscription ou de connexion ou une stratégie d’inscription et une stratégie de connexion ?
Nous vous recommandons d’utiliser une stratégie d’inscription ou de connexion plutôt qu’une stratégie d’inscription et une stratégie de connexion.  

stratégie d’inscription ou connectez-vous Hello a plus de capacités que la stratégie d’authentification hello. Aussi, il vous permet de personnalisation de l’interface utilisateur de page toouse et une meilleure prise en charge pour la localisation. 

stratégie d’authentification Hello est recommandé si vous n’avez pas besoin toolocalize vos stratégies, uniquement besoin des fonctionnalités de personnalisation secondaire pour la personnalisation et de mot de passe réinitialisation intégrée.

## <a name="next-steps"></a>Étapes suivantes
* [Configuration du jeton, de la session et de l’authentification unique](active-directory-b2c-token-session-sso.md)
* [Désactiver la vérification par courrier électronique lors de l’inscription du consommateur](active-directory-b2c-reference-disable-ev.md)

