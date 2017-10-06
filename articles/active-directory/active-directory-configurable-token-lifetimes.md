---
title: "durées de vie jeton aaaConfigurable dans Azure Active Directory | Documents Microsoft"
description: "Découvrez comment tooset des durées de vie des jetons émis par Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: 0d4c8545981c5463cc7c95f669167bbc38230123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a>Durées de vie des jetons configurables dans Azure Active Directory (version préliminaire publique)
Vous pouvez spécifier la durée de vie hello d’un jeton émis par Azure Active Directory (Azure AD). Vous pouvez définir les durées de vie des jetons pour toutes les applications de votre organisation, pour une application mutualisée (plusieurs organisations) ou pour un principal de service spécifique de votre organisation.

> [!NOTE]
> Pour le moment, cette fonctionnalité est disponible dans la version préliminaire publique. Préparez-vous à toorevert ou supprimer toutes les modifications. Hello fonctionnalité est disponible dans n’importe quel abonnement Azure Active Directory au cours de la version préliminaire publique. Toutefois, lorsque la fonctionnalité de hello devient disponible de manière générale, certains aspects de la fonctionnalité de hello peuvent nécessiter un [Azure Active Directory Premium](active-directory-get-started-premium.md) abonnement.
>
>

Dans Azure AD, un objet de stratégie représente un ensemble de règles appliquées sur des applications individuelles ou sur toutes les applications d’une organisation. Chaque type de stratégie a une structure unique, avec un ensemble de propriétés qui sont toowhich tooobjects appliqués qu’ils sont attribués.

Vous pouvez désigner une stratégie comme stratégie par défaut de hello pour votre organisation. stratégie de Hello est application tooany appliqués dans l’organisation de hello, tant qu’il n’est pas remplacé par une stratégie avec une priorité plus élevée. Vous pouvez également affecter un toospecific stratégie applications. ordre de priorité de Hello varie selon le type de stratégie.


## <a name="token-types"></a>Types de jetons

Vous pouvez définir les stratégies de durée de vie des jetons pour les jetons d’actualisation, les jetons d’accès, les jetons de session et les jetons d’ID.

### <a name="access-tokens"></a>Jetons d’accès
Utiliser les clients l’accès des jetons tooaccess une ressource protégée. Un jeton d’accès peut uniquement être utilisé pour une combinaison spécifique d’utilisateur, de client et de ressource. Les jetons d’accès ne peuvent pas être révoqués et sont valides jusqu’à leur expiration. Un acteur malveillant qui a obtenu un jeton d’accès peut l’utiliser pour prolonger sa durée de vie. Ajustement de durée de vie hello jeton d’accès est un compromis entre l’amélioration des performances du système et croissante hello durée hello client conserve l’accès après que hello du compte utilisateur est désactivé. Améliorer les performances système sont obtenue en réduisant le nombre hello de fois où qu'un client doit tooacquire un jeton d’accès de nouveau.

### <a name="refresh-tokens"></a>Jetons d’actualisation
Lorsqu’un client acquiert un tooaccess de jeton d’accès une ressource protégée, le client de hello reçoit un jeton d’actualisation et un jeton d’accès. jeton d’actualisation Hello est nouvelles paires de jeton accès/actualisation tooobtain utilisé lors de l’expiration du jeton d’accès actuel hello. Un jeton d’actualisation est la combinaison de tooa dépendant de l’utilisateur et le client. Un jeton d’actualisation peut être révoqué et les validité du jeton hello sont vérifiée à chaque fois que le jeton de hello est utilisé.

Il est important toomake une distinction entre les clients confidentiels et public. Pour plus d’informations sur les différents types de client, consultez [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a>Durées de vie des jetons avec des jetons d’actualisation de client confidentiel
Les clients confidentiels sont des applications qui peuvent stocker un mot de passe client (secret). Ils peuvent s’avérer provenant des demandes à partir de l’application cliente de hello et non à partir d’un acteur malveillant. Par exemple, une application web est un client confidentiel, car il peut stocker une clé secrète client sur le serveur web de hello. Elle n’est pas exposée. Étant donné que ces flux est plus sécurisées, hello durées de vie par défaut des jetons d’actualisation émis toothese flux est `until-revoked`, ne peut pas être modifié à l’aide de stratégie et ne seront pas révoquées sur les réinitialisations de mot de passe facultatif.

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a>Durées de vie des jetons avec des jetons d’actualisation de client public

Les clients publics ne peuvent pas stocker en toute sécurité un mot de passe client (secret). Par exemple, une application iOS/Android ne peut pas appliquer une clé secrète à partir de propriétaire de la ressource hello, afin qu’il est considéré comme un client public. Vous pouvez définir des stratégies sur les ressources tooprevent des jetons d’actualisation à partir des clients publics antérieures à une période spécifiée à partir de l’obtention d’une nouvelle paire de jeton d’accès/actualisation. (toodo, hello utilisez propriété de jeton maximale inactif heure d’actualisation.) Vous pouvez également utiliser tooset stratégies une période au-delà des jetons d’actualisation hello qui ne sont plus valides. (toodo, hello utilisez propriété actualiser un jeton Age de Max.) Vous pouvez ajuster la durée de vie de hello d’un toocontrol jeton actualisation quand et à quelle fréquence hello utilisateur est requis tooreenter informations d’identification, au lieu d’être authentifiés en mode silencieux, lors de l’utilisation d’une application cliente publique.

### <a name="id-tokens"></a>Jetons d’ID
Toowebsites et clients natifs, les jetons d’ID sont passés. Les jetons d’ID contiennent des informations de profil sur un utilisateur. Un jeton d’ID est la combinaison spécifique de tooa dépendant de l’utilisateur et le client. Les jetons d’ID sont considérés comme valides jusqu’à leur expiration. En règle générale, une application web correspond à un utilisateur de durée de vie de session dans hello application toohello durée de vie du jeton d’ID hello émis pour l’utilisateur de hello. Vous pouvez ajuster la durée de vie de hello d’un ID jeton toocontrol la fréquence à laquelle application web de hello expiration de session de l’application hello et la fréquence à laquelle il nécessite toobe d’utilisateur hello authentifié auprès d’Azure AD (en mode silencieux ou interactive).

### <a name="single-sign-on-session-tokens"></a>Jetons de session d’authentification unique
Lorsqu’un utilisateur s’authentifie auprès d’Azure AD et sélectionne hello **maintenir la connexion** case à cocher, une authentification session unique (SSO) est établie avec le navigateur de l’utilisateur hello et Azure AD. jeton d’authentification unique Hello, sous forme de hello d’un cookie, représente cette session. Notez que ce jeton de session hello SSO n’est pas application de ressource/client spécifique tooa liée. Les jetons de session SSO peuvent être révoqués, et leur validité est vérifiée à chaque fois qu’ils sont utilisés.

Azure AD utilise deux types de jetons de session SSO : persistant et non persistant. Les jetons de session persistante sont stockés en tant que les cookies persistants par le navigateur de hello. Les jetons de session non persistants sont stockés en tant que cookies de session. (Les cookies de session sont détruits lors de la fermeture du navigateur hello).

Les jetons de session non persistants ont une durée de vie de 24 heures. Les jetons persistants ont une durée de vie de 180 jours. N’importe quel moment qu'un jeton de session de l’authentification unique est utilisé au sein de sa période de validité, la période de validité hello est étendue une autre de 24 heures ou de 180 jours, selon le type de jeton hello. Si un jeton de session SSO n’est pas utilisé au cours de sa période de validité, il est considéré comme arrivé à expiration et n’est plus accepté.

Vous pouvez utiliser une stratégie tooset hello fois premier jeton de session hello a été émis le hello au-delà de jeton de session n’est plus accepté. (toodo, hello utilisez propriété Max Age jeton de Session.) Vous pouvez ajuster la durée de vie de hello d’un toocontrol de jeton de session quand et la fréquence à laquelle un utilisateur est requis tooreenter informations d’identification, au lieu de l’authentification en mode silencieux, lors de l’utilisation d’une application web.

### <a name="token-lifetime-policy-properties"></a>Propriétés des stratégies de durée de vie des jetons
Une stratégie de durée de vie des jetons est un type d’objet de stratégie qui contient des règles de durée de vie des jetons. Utilisation des propriétés de hello stratégie toocontrol hello spécifié des durées de vie de jeton. Si aucune stratégie n’est définie, système de hello applique la valeur de durée de vie par défaut hello.

### <a name="configurable-token-lifetime-properties"></a>Propriétés des durées de vie des jetons configurables
| Propriété | Chaîne de propriété de stratégie | Éléments affectés | Default | Minimale | Maximale |
| --- | --- | --- | --- | --- | --- |
| Durée de vie de jeton d’accès |AccessTokenLifetime |Jetons d’accès, jetons d’ID, jetons SAML2 |1 heure |10 minutes |1 jour |
| Délai d’inactivité maximale de jeton d’actualisation |MaxInactiveTime |Jetons d’actualisation |14 jours |10 minutes |90 jours |
| Âge maximal de jeton d’actualisation à facteur unique |MaxAgeSingleFactor |Jetons d’actualisation (pour tous les utilisateurs) |Jusqu’à révocation |10 minutes |Jusqu’à révocation<sup>1</sup> |
| Âge maximal de jeton d’actualisation multifacteur |MaxAgeMultiFactor |Jetons d’actualisation (pour tous les utilisateurs) |Jusqu’à révocation |10 minutes |Jusqu’à révocation<sup>1</sup> |
| Âge maximal de jeton de session à facteur unique |MaxAgeSessionSingleFactor<sup>2</sup> |Jetons de session (persistants et non persistants) |Jusqu’à révocation |10 minutes |Jusqu’à révocation<sup>1</sup> |
| Âge maximal de jeton de session multifacteur |MaxAgeSessionMultiFactor<sup>3</sup> |Jetons de session (persistants et non persistants) |Jusqu’à révocation |10 minutes |Jusqu’à révocation<sup>1</sup> |

* <sup>1</sup>365 jours est hello explicite longueur maximale qui peut être définie pour ces attributs.
* <sup>2</sup>si **MaxAgeSessionSingleFactor** n’est pas définie, cette valeur est hello **MaxAgeSingleFactor** valeur. Si aucun de ces paramètres est définie, propriété de hello prend par défaut hello (jusqu'à ce que révoqués).
* <sup>3</sup>si **MaxAgeSessionMultiFactor** n’est pas définie, cette valeur est hello **MaxAgeMultiFactor** valeur. Si aucun de ces paramètres est définie, propriété de hello prend par défaut hello (jusqu'à ce que révoqués).

### <a name="exceptions"></a>Exceptions
| Propriété | Éléments affectés | Default |
| --- | --- | --- |
| Âge maximal de jeton d’actualisation (émis pour les utilisateurs fédérés disposant d’informations de révocation insuffisantes<sup>1</sup>) |Jetons d’actualisation (émis pour les utilisateurs fédérés disposant d’informations de révocation insuffisantes<sup>1</sup>) |12 heures |
| Délai d’inactivité maximale de jeton d’actualisation (émis pour les clients confidentiels) |Jetons d’actualisation (émis pour les clients confidentiels) |90 jours |
| Âge maximal de jeton d’actualisation (émis pour les clients confidentiels) |Jetons d’actualisation (émis pour les clients confidentiels) |Jusqu’à révocation |

* <sup>1</sup>les utilisateurs fédérés qui dispose des informations de révocation insuffisantes incluent tous les utilisateurs qui n’ont pas hello attribut « LastPasswordChangeTimestamp » synchronisé. Ces utilisateurs figurent l’âge maximum ce court étant AAD tooverify impossible quand toorevoke des jetons qui sont liées tooan ancien des informations d’identification (par exemple, un mot de passe a été modifié) et qu’il doit vérifier dans tooensure plus fréquemment que l’utilisateur hello et les jetons associés sont toujours dans la règle. tooimprove cette expérience, les administrateurs doivent s’assurer qu’ils sont à la synchronisation de client hello attribut « LastPasswordChangeTimestamp » (Cela peut être défini sur l’objet d’utilisateur hello à l’aide de Powershell ou via AADSync).

### <a name="policy-evaluation-and-prioritization"></a>Définition des priorités et évaluation de la stratégie
Vous pouvez créer et ensuite affecter une application spécifique de durée de vie de jeton stratégie tooa tooyour organisation et tooservice principaux. Plusieurs stratégies peuvent s’appliquer tooa des applications spécifiques. stratégie de durée de vie de jeton Hello qui entre en vigueur suit ces règles :

* Si une stratégie est explicitement affectée toohello principal du service, il est appliqué.
* Si aucune stratégie n’est explicitement affectée toohello principal du service, une stratégie attribuée explicitement organisation parente de toohello de principal du service hello est appliquée.
* Si aucune stratégie n’est explicitement affectée principal du service toohello ou toohello organisation, stratégie toohello application hello est appliquée.
* Si aucune stratégie n’a été affectée toohello service principal, organisation de hello ou un objet d’application hello, hello par défaut est appliquée. (Voir tableau hello dans [propriétés de la durée de vie de jeton Configurable](#configurable-token-lifetime-properties).)

Pour plus d’informations sur la relation hello entre objets principal du service et application, consultez [Application et les objets principal du service dans Azure Active Directory](active-directory-application-objects.md).

Validité d’un jeton est évaluée au moment de hello hello jeton est utilisé. stratégie Hello avec la priorité la plus élevée de hello dans l’application hello qui est accessible en vigueur.

> [!NOTE]
> Voici un scénario d’exemple.
>
> Un utilisateur souhaite tooaccess deux des applications web : l’Application Web A et b d’Application Web
> 
> Facteurs :
> * Les deux applications web sont Bonjour même parent d’organisation.
> * Jeton de durée de vie Policy 1 avec un jeton Session Max Age de huit heures est définie comme valeur par défaut de l’organisation hello parent.
> * L’Application Web A est une application web d’utilisation normale et n’est pas lié tooany stratégies.
> * L’application web B est utilisée pour les processus très sensibles. Son principal de service est lié tooToken 2 de stratégie de durée de vie, qui a un jeton Session Max Age de 30 minutes.
>
> À 12 h 00, utilisateur de hello démarre une nouvelle session de navigateur et les tentatives tooaccess A. Application de Web hello utilisateur est redirigé tooAzure AD et qu’il est invité à toosign dans. Cette opération crée un cookie qui a un jeton de session dans le navigateur de hello. l’utilisateur Hello est tooWeb arrière redirigé A de l’Application avec un jeton d’ID qui permet de hello utilisateur tooaccess application hello.
>
> À 12:15 PM, hello utilisateur tente de tooaccess tooAzure de redirections de navigateur Web, Application B. hello AD, qui détecte le cookie de session hello. Principal du service Web Application B est lié tooToken 2 de stratégie de durée de vie, mais il fait également partie de l’organisation parente hello, la valeur par défaut 1 de stratégie de durée de vie de jeton. Jeton 2 de stratégie de durée de vie en vigueur, car les stratégies liées tooservice principaux ont une priorité plus élevée que les stratégies d’organisation par défaut. jeton de session Hello avait été initialement émis dans hello 30 dernières minutes, donc il est considéré comme valide. l’utilisateur Hello est tooWeb arrière redirigé Application B avec un jeton d’ID qui accorde l’accès.
>
> À 13 h 00, hello tentatives tooaccess A. Application de Web hello utilisateur est redirigé tooAzure AD. Web Application un n’est pas lié tooany stratégies, mais, car il s’agit d’une organisation avec jeton 1 de stratégie de durée de vie par défaut, cette stratégie est appliquée. cookie de session Hello qui avait été initialement émise dans hello huit dernières heures est détecté. l’utilisateur Hello est tooWeb arrière en mode silencieux redirigé A de l’Application avec un nouveau jeton d’ID. utilisateur de Hello n’est pas tooauthenticate requis.
>
> Immédiatement après coup, utilisateur de hello tente de l’utilisateur de hello tooaccess B. Application de Web est redirigé tooAzure AD. Comme avant, la stratégie 2 de durée de vie des jetons est appliquée. Étant donné que le jeton de hello a été émis il y a plus de 30 minutes, utilisateur de hello est demandée tooreenter leurs informations d’identification d’ouverture de session. Un nouveau jeton de session et un jeton d’ID sont émis. Hello utilisateur peut alors accéder Web Application B.
>
>

## <a name="configurable-policy-property-details"></a>Présentation des propriétés de stratégie configurables
### <a name="access-token-lifetime"></a>Durée de vie de jeton d’accès
**Chaîne :** AccessTokenLifetime

**Éléments affectés :** jetons d’accès, jetons d’ID

**Résumé :** cette stratégie détermine la durée pendant laquelle les jetons d’accès et d’ID sont considérés comme valides. Ce qui réduit la propriété de durée de vie accès hello d’atténue le risque de hello d’un jeton d’accès ou le jeton d’ID utilisé par un acteur malveillant pour une période prolongée. (Ces jetons ne peuvent pas être révoqués.) Hello inconvénient est que les performances sont affectées, parce que les jetons hello ont toobe remplacé le plus souvent.

### <a name="refresh-token-max-inactive-time"></a>Délai d’inactivité maximale de jeton d’actualisation
**Chaîne :** MaxInactiveTime

**Éléments affectés :** jetons d’actualisation

**Résumé :** cette stratégie contrôle l’ancienneté un jeton d’actualisation peut être avant un client peut ne plus l’utiliser tooretrieve une nouvelle paire de jeton d’accès/actualisation lors de la tentative de tooaccess cette ressource. Car un nouveau jeton d’actualisation est généralement retourné lorsqu’un jeton d’actualisation est utilisé, cette stratégie empêche l’accès si hello tentatives tooaccess n’importe quelle ressource à l’aide du jeton d’actualisation actuel hello pendant hello spécifié laps de temps.

Cette stratégie force les utilisateurs qui n’ont pas été actifs sur leur tooretrieve de tooreauthenticate client un nouveau jeton d’actualisation.

Hello, propriété de jeton maximale inactif heure d’actualisation doit être définie tooa une valeur inférieure à hello l’âge maximum jeton facteur unique et les propriétés de multi-Factor actualiser jeton l’âge maximum hello.

### <a name="single-factor-refresh-token-max-age"></a>Âge maximal de jeton d’actualisation à facteur unique
**Chaîne :** MaxAgeSingleFactor

**Éléments affectés :** jetons d’actualisation

**Résumé :** cette stratégie contrôle comment long, un utilisateur peut utiliser un tooget de jeton d’actualisation un nouvel accès/actualisation paire de jetons après leur dernière authentifié avec succès en utilisant uniquement un facteur unique. Une fois un utilisateur s’authentifie et reçoit un jeton d’actualisation, utilisateur de hello peut utiliser le flux de jeton de l’actualisation hello pour hello spécifié période de temps. (Cela est vrai tant que jeton d’actualisation actuel hello n’est pas révoqué, et il ne reste pas inutilisé pendant plus de temps d’inactivité hello.) À ce stade, les utilisateurs hello sont forcé tooreauthenticate tooreceive un nouveau jeton d’actualisation.

Réduire l’âge maximal de hello force le plus souvent tooauthenticate d’utilisateurs. Étant donné que l’authentification du seul facteur est considéré comme moins sécurisée que l’authentification multifacteur, nous vous recommandons de définir cette valeur de la propriété tooa qui est égale tooor d’antérieure à hello propriété Age multifacteur actualiser jeton Max.

### <a name="multi-factor-refresh-token-max-age"></a>Âge maximal de jeton d’actualisation multifacteur
**Chaîne :** MaxAgeMultiFactor

**Éléments affectés :** jetons d’actualisation

**Résumé :** cette stratégie contrôle comment long, un utilisateur peut utiliser un tooget de jeton d’actualisation un nouvel accès/actualisation paire de jetons après leur dernière authentifié avec succès à l’aide de plusieurs facteurs. Une fois un utilisateur s’authentifie et reçoit un jeton d’actualisation, utilisateur de hello peut utiliser le flux de jeton de l’actualisation hello pour hello spécifié période de temps. (Cela est vrai tant que jeton d’actualisation actuel hello n’est pas révoqué, et il n’est pas inutilisé pendant plus de temps d’inactivité hello.) À ce stade, les utilisateurs sont obligés de tooreauthenticate tooreceive un nouveau jeton d’actualisation.

Réduire l’âge maximal de hello force le plus souvent tooauthenticate d’utilisateurs. Car l’authentification de facteur unique est considérée comme moins sûre que l’authentification multifacteur, nous vous recommandons de définir cette valeur tooa de propriété qui est égale tooor supérieure hello seul facteur actualiser jeton l’âge maximum propriété.

### <a name="single-factor-session-token-max-age"></a>Âge maximal de jeton de session à facteur unique
**Chaîne :** MaxAgeSessionSingleFactor

**Éléments affectés :** jetons de session (persistants et non persistants)

**Résumé :** ce de stratégie contrôle la durée pendant laquelle un utilisateur peut utiliser un tooget de jeton de session nouvel identificateur de session du jeton après leur dernière authentifié avec succès en utilisant uniquement un facteur unique. Une fois un utilisateur s’authentifie et reçoit un jeton de la nouvelle session, utilisateur de hello peut utiliser le flux de jeton de session hello pour hello spécifié période de temps. (Cela vaut aussi longtemps que le jeton de session actuel hello n’est pas révoqué et n’a pas expiré.) Après que hello spécifié laps de temps, l’utilisateur hello est forcé tooreauthenticate tooreceive un jeton de la nouvelle session.

Réduire l’âge maximal de hello force le plus souvent tooauthenticate d’utilisateurs. Car l’authentification de facteur unique est considérée comme moins sûre que l’authentification multifacteur, nous vous recommandons de définir cette valeur tooa propriété propriété de l’âge maximum jeton multifacteur Session tooor inférieur à hello égale.

### <a name="multi-factor-session-token-max-age"></a>Âge maximal de jeton de session multifacteur
**Chaîne :** MaxAgeSessionMultiFactor

**Éléments affectés :** jetons de session (persistants et non persistants)

**Résumé :** ce de stratégie contrôle la durée pendant laquelle un utilisateur peut utiliser un tooget de jeton de session nouvel identificateur de session du jeton après hello dernière fois authentifiés avec succès à l’aide de plusieurs facteurs. Une fois un utilisateur s’authentifie et reçoit un jeton de la nouvelle session, utilisateur de hello peut utiliser le flux de jeton de session hello pour hello spécifié période de temps. (Cela vaut aussi longtemps que le jeton de session actuel hello n’est pas révoqué et n’a pas expiré.) Après que hello spécifié laps de temps, l’utilisateur hello est forcé tooreauthenticate tooreceive un jeton de la nouvelle session.

Réduire l’âge maximal de hello force le plus souvent tooauthenticate d’utilisateurs. Étant donné que l’authentification du seul facteur est considéré comme moins sécurisée que l’authentification multifacteur, nous vous recommandons de définir cette valeur de tooa de propriété est égale tooor supérieure hello facteur unique Session l’âge maximum jeton propriété.

## <a name="example-token-lifetime-policies"></a>Exemples de stratégie de durée de vie des jetons
De nombreux scénarios sont possibles dans Azure AD lorsque vous créez et gérez les durées de vie des jetons pour les applications, les principaux du service et votre organisation globale. Dans cette section, nous allons vous guider dans quelques scénarios courants de stratégie qui peuvent vous aider à imposer de nouvelles règles pour les éléments suivants :

* Durée de vie du jeton
* Délai d’inactivité maximale des jetons
* Âge maximal des jetons

Dans les exemples hello, vous pouvez apprendre comment :

* Gérer la stratégie par défaut d’une organisation
* Créer une stratégie de connexion web
* Créer une stratégie pour une application native qui appelle une API web
* Gérer une stratégie avancée

### <a name="prerequisites"></a>Composants requis
Bonjour exemple suivant, vous créez, mettre à jour, liez et supprimez des stratégies pour les applications, les principaux de service et votre organisation générale. Si vous êtes de nouveau tooAzure AD, nous vous recommandons d’en savoir plus sur [comment tooget une annonce Azure locataire](active-directory-howto-tenant.md) avant de procéder à ces exemples.  

tooget démarré, hello comme suit :

1. Télécharger le dernier hello [Azure AD PowerShell Module version](https://www.powershellgallery.com/packages/AzureADPreview).
2. Exécutez hello `Connect` toosign de commande dans tooyour compte d’administrateur Azure AD. Exécutez cette commande chaque fois que vous démarrez une nouvelle session.

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. toosee toutes les stratégies qui ont été créés dans votre organisation, hello exécution suivant la commande. Exécutez cette commande après la plupart des opérations dans les scénarios suivants de hello. En cours d’exécution commande hello également vous aide à obtenir de hello ** ** de vos stratégies.

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a>Exemple : Gérer la stratégie par défaut d’une organisation
Dans cet exemple, vous allez créer une stratégie qui permet à vos utilisateurs de se connecter moins fréquemment dans votre organisation entière. toodo, créer une stratégie d’émission de jeton de durée de vie pour les jetons d’Actualiser facteur unique, qui est appliquée dans votre organisation. stratégie de Hello est application tooevery appliquées dans votre organisation et le principal du service tooeach qui n’a pas encore une stratégie définie.

1. Créez une stratégie de durée de vie des jetons.

    1.  Hello ensemble seul facteur jeton d’actualisation trop » jusqu'à ce que révoqués. » jeton de Hello n’expire jamais jusqu'à ce que l’accès est révoqué. Créer hello après la définition de la stratégie :

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  stratégie de hello toocreate, exécutez hello de commande suivante :

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  toosee votre nouvelle stratégie, puis de la stratégie tooget hello **ObjectId**, exécutez hello commande suivante :

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Mettre à jour la stratégie de hello.

    Vous pouvez décider que hello première stratégie que vous définissez dans cet exemple n’est pas aussi stricte que votre service requiert. l’exécution de votre jeton d’actualisation facteur unique tooexpire dans les deux derniers jours, tooset hello la commande suivante :

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a>Exemple : Créer une stratégie de connexion web

Dans cet exemple, vous créez une stratégie qui impose aux utilisateurs des tooauthenticate plus fréquemment dans votre application web. Cette stratégie définit la durée de vie hello de jetons d’accès/ID hello et l’âge maximal de hello d’un principal de service de jeton toohello multifacteur session de votre application web.

1. Créez une stratégie de durée de vie des jetons.

    Cette stratégie, pour le web connectez-vous, définit la durée de vie hello/ID d’accès et heures de tootwo hello max facteur unique session âge jeton.

    1.  stratégie de hello toocreate, exécutez la commande suivante :

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee votre nouvelle stratégie et la stratégie de hello tooget **ObjectId**, exécutez hello commande suivante :

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  Affecter le principal du service tooyour hello stratégie. Vous devez également tooget hello **ObjectId** de votre principal de service. 

    1.  toosee principaux de service d’ensemble de l’entreprise, vous pouvez interroger [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). Ou, [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), connectez-vous à tooyour compte Azure AD.

    2.  Lorsque vous avez hello **ObjectId** votre principal de service, exécutez hello de commande suivante :

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a>Exemple : Créer une stratégie pour une application native qui appelle une API web
Dans cet exemple, vous créez une stratégie qui impose aux utilisateurs tooauthenticate moins fréquemment. stratégie de Hello augmente également la durée hello de qu'un utilisateur peut être inactif avant de l’utilisateur de hello doit authentifier. stratégie de Hello est appliqué toohello web API. Lors de l’application native hello demande API web de hello en tant que ressource, cette stratégie est appliquée.

1. Créez une stratégie de durée de vie des jetons.

    1.  toocreate règles strictes pour une API web, exécutez hello de commande suivante :

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee votre nouvelle stratégie et la stratégie de hello tooget **ObjectId**, exécutez hello commande suivante :

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Affecter hello stratégie tooyour web API. Vous devez également tooget hello **ObjectId** de votre application. Hello meilleure manière toofind de votre application **ObjectId** est toouse hello [portail Azure](https://portal.azure.com/).

   Lorsque vous avez hello **ObjectId** de votre application, exécutez hello de commande suivante :

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of hello Application> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a>Exemple : Gérer une stratégie avancée
Dans cet exemple, vous créez quelques stratégies, toolearn fonctionnement du système de priorité hello. Vous pouvez également apprendre comment toomanage plusieurs stratégies sont appliquées tooseveral des objets.

1. Créez une stratégie de durée de vie des jetons.

    1.  toocreate une stratégie par défaut qui définit les jours hello jeton d’actualisation seul facteur too30 de durée de vie, exécutez hello de commande suivante :

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  toosee votre nouvelle stratégie, puis de la stratégie tooget hello **ObjectId**, exécutez hello commande suivante :

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Affecter le principal du service tooa hello stratégie.

    Maintenant, vous disposez d’une stratégie qui s’applique toohello toute organisation. Vous pouvez toopreserve cette stratégie de 30 jours pour un principal de service spécifique, mais modifiez hello organisation par défaut stratégie toohello limite supérieure de « jusqu'à révoqués. »

    1.  toosee principaux de service d’ensemble de l’entreprise, vous pouvez interroger [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). Ou, dans [l’explorateur Azure AD Graph](https://graphexplorer.cloudapp.net/), connectez-vous à l’aide de votre compte Azure AD.

    2.  Lorsque vous avez hello **ObjectId** votre principal de service, exécutez hello de commande suivante :

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
            ```
        
3. Ensemble hello `IsOrganizationDefault` indicateur toofalse :

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. Créez une stratégie par défaut d’organisation :

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    Vous disposez maintenant de principal du service lié tooyour hello d’origine stratégie et une nouvelle stratégie hello est définie en tant que votre stratégie de valeur par défaut. Il est important tooremember que les stratégies appliquées tooservice principaux est prioritaires sur les stratégies d’organisation par défaut.

## <a name="cmdlet-reference"></a>Référence sur les applets de commande

### <a name="manage-policies"></a>Gérer les stratégies

Vous pouvez utiliser hello suivant des stratégies de toomanage d’applets de commande.

#### <a name="new-azureadpolicy"></a>New-AzureADPolicy

Permet de créer une stratégie.

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| Paramètres | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Definition</code> |Tableau de stringified JSON qui contient des règles de la stratégie du hello. | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |Chaîne de nom de la stratégie hello. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |Si la valeur est true, définit la stratégie de hello comme stratégie par défaut de l’organisation hello. Si la valeur est false, rien ne se produit. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |Type de stratégie. Pour les durées de vie des jetons, utilisez toujours « TokenLifetimePolicy ». | `-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code> [Facultatif] |Définit un autre ID pour la stratégie de hello. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a>Get-AzureADPolicy
Permet d’obtenir toutes les stratégies d’Azure AD ou une stratégie spécifiée.

```PowerShell
Get-AzureADPolicy
```

| parameters | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Id</code> [Facultatif] |**ObjectId (Id)** de stratégie hello. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a>Get-AzureADPolicyAppliedObject
Obtient toutes les applications et principaux de service qui est liés tooa stratégie.

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| Paramètres | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de stratégie hello. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a>Set-AzureADPolicy
Met à jour une stratégie existante.

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| parameters | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de stratégie hello. |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |Chaîne de nom de la stratégie hello. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;Definition</code> [Facultatif] |Tableau de stringified JSON qui contient des règles de la stratégie du hello. |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;IsOrganizationDefault</code> [Facultatif] |Si la valeur est true, définit la stratégie de hello comme stratégie par défaut de l’organisation hello. Si la valeur est false, rien ne se produit. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> [Facultatif] |Type de stratégie. Pour les durées de vie des jetons, utilisez toujours « TokenLifetimePolicy ». |`-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code> [Facultatif] |Définit un autre ID pour la stratégie de hello. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a>Remove-AzureADPolicy
Suppressions hello spécifié de stratégie.

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| Paramètres | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de stratégie hello. | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a>Stratégies d’application
Vous pouvez utiliser hello suivant d’applets de commande pour les stratégies d’application.</br></br>

#### <a name="add-azureadapplicationpolicy"></a>Add-AzureADApplicationPolicy
Hello de liens spécifiée tooan l’application de stratégie.

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| Paramètres | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de l’application hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId** de stratégie de hello. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a>Get-AzureADApplicationPolicy
Obtient la stratégie hello tooan application attribuée.

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| Paramètres | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de l’application hello. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a>Remove-AzureADApplicationPolicy
Supprime une stratégie d’une application.

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| parameters | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de l’application hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId** de stratégie de hello. | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a>Stratégies de principal du service
Vous pouvez utiliser hello suivant d’applets de commande pour les stratégies de principal de service.

#### <a name="add-azureadserviceprincipalpolicy"></a>Add-AzureADServicePrincipalPolicy
Liens hello principal du service tooa stratégie spécifiée.

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| Paramètres | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de l’application hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId** de stratégie de hello. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a>Get-AzureADServicePrincipalPolicy
Obtient un principal de service spécifié de stratégie toohello lié.

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| Paramètres | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de l’application hello. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a>Remove-AzureADServicePrincipalPolicy
Supprime la stratégie de hello de principal du service spécifié hello.

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| Paramètres | Description | Exemple |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de l’application hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId** de stratégie de hello. | `-PolicyId <ObjectId of Policy>` |
