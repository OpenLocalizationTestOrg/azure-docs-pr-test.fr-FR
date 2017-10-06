---
title: "Azure Active Directory B2C : gestion de la personnalisation des configurations SSO et de jetons avec des stratégies personnalisées | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Azure Active Directory B2C : gestion de la personnalisation des configurations SSO et de jetons avec des stratégies personnalisées
Utilisation de stratégies personnalisées fournit que vous hello même contrôle votre jeton, la session et la seule configurations sign-on (SSO) par le biais des stratégies intégrées.  toolearn fait de la signification de chaque paramètre, consultez la documentation de hello [ici](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Configuration des revendications et de la durée de vie des jetons
paramètres hello toochange votre durée de vie des jetons, vous devez tooadd un `<ClaimsProviders>` élément hello partie de confiance tiers fichier de stratégie de hello souhaité tooimpact.  Hello `<ClaimsProviders>` élément est un enfant de hello `<TrustFrameworkPolicy>`.  Dans, vous aurez besoin des informations de hello tooput qui affecte votre durée de vie des jetons.  Hello XML ressemble à ceci :

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

**Durée de vie des jetons d’accès** hello accès durée de vie de jeton peut être modifiée en modifiant la valeur hello à l’intérieur de hello `<Item>` avec hello clé = « token_lifetime_secs » en secondes.  valeur par défaut Hello intégré est 3 600 secondes (60 minutes).

**Durée de vie de jeton ID** durée de vie hello ID peut être modifiée en modifiant la valeur hello à l’intérieur de hello `<Item>` avec hello clé = « id_token_lifetime_secs » en secondes.  valeur par défaut Hello intégré est 3 600 secondes (60 minutes).

**Durée de vie de jeton d’actualisation** durée de vie hello actualisation peut être modifiée en modifiant la valeur hello à l’intérieur de hello `<Item>` avec hello clé = « refresh_token_lifetime_secs » en secondes.  valeur par défaut Hello intégré est 1209600 secondes (14 jours).

**Actualiser le jeton durée de vie de fenêtre glissante** si vous souhaitez que tooset un jeton d’actualisation de tooyour de durée de vie fenêtre glissante, modifiez la valeur hello à l’intérieur `<Item>` avec hello clé = « rolling_refresh_token_lifetime_secs » en secondes.  valeur par défaut Hello intégré est 7776000 (90 jours).  Si vous ne souhaitez pas tooenfore un glissante de durée de vie de fenêtre, remplacez cette ligne en :
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**Revendication de l’émetteur (iss)** si vous souhaitez la revendication de l’émetteur (iss) toochange hello, modifier la valeur hello à l’intérieur de hello `<Item>` avec hello clé = « IssuanceClaimPattern ».  les valeurs applicables Hello sont `AuthorityAndTenantGuid` et `AuthorityWithTfp`.

**Paramètre représentant les ID de stratégie de revendication** options hello pour définir cette valeur sont TFP (stratégie d’infrastructure approbation) et ACR (référence de contexte d’authentification).  
Nous vous recommandons de définir cette tooTFP, toodo cela, vérifiez hello `<Item>` avec hello clé = « AuthenticationContextReferenceClaimPattern » existe et que la valeur hello est `None`.
Dans votre élément `<OutputClaims>`, ajoutez cet élément :
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
À l’ACR, supprimez hello `<Item>` avec hello clé = « AuthenticationContextReferenceClaimPattern ».

**Revendication de sujet (sub)** cette option est définie par défaut tooObjectID, si vous souhaitez que tooswitch cela trop`Not Supported`, hello suivant :

Remplacez cette ligne : 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
par cette ligne :
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Comportement de la session et SSO
toochange votre comportement de session et des configurations de l’authentification unique, vous devez tooadd une `<UserJourneyBehaviors>` élément hello `<RelyingParty>` élément.  Hello `<UserJourneyBehaviors>` élément doit suivre immédiatement hello `<DefaultUserJourney>`.  Bonjour à l’intérieur de votre `<UserJourneyBehavors>` élément doit ressembler à ceci :

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Configuration de l’authentification unique (SSO)** toochange hello seule configuration de l’authentification, vous devez valeur hello toomodify `<SingleSignOn>`.  les valeurs applicables Hello sont `Tenant`, `Application`, `Policy` et `Disabled`. 

**Durée de vie de session (minutes) l’application Web** toochange hello hello web application durée de vie de session, vous devez toomodify valeur hello `<SessionExpiryInSeconds>` élément.  valeur par défaut de Hello dans les stratégies intégrées est 86 400 secondes (1 440 minutes).

**Délai d’expiration de session Web application** toochange hello web application délai d’expiration, vous devez valeur hello toomodify `<SessionExpiryType>`.  les valeurs applicables Hello sont `Absolute` et `Rolling`.
