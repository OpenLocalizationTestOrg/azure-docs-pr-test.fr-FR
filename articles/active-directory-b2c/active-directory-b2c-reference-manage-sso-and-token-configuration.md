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
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="1442e-102">Azure Active Directory B2C : gestion de la personnalisation des configurations SSO et de jetons avec des stratégies personnalisées</span><span class="sxs-lookup"><span data-stu-id="1442e-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="1442e-103">Utilisation de stratégies personnalisées fournit que vous hello même contrôle votre jeton, la session et la seule configurations sign-on (SSO) par le biais des stratégies intégrées.</span><span class="sxs-lookup"><span data-stu-id="1442e-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="1442e-104">toolearn fait de la signification de chaque paramètre, consultez la documentation de hello [ici](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="1442e-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="1442e-105">Configuration des revendications et de la durée de vie des jetons</span><span class="sxs-lookup"><span data-stu-id="1442e-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="1442e-106">paramètres hello toochange votre durée de vie des jetons, vous devez tooadd un `<ClaimsProviders>` élément hello partie de confiance tiers fichier de stratégie de hello souhaité tooimpact.</span><span class="sxs-lookup"><span data-stu-id="1442e-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="1442e-107">Hello `<ClaimsProviders>` élément est un enfant de hello `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="1442e-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="1442e-108">Dans, vous aurez besoin des informations de hello tooput qui affecte votre durée de vie des jetons.</span><span class="sxs-lookup"><span data-stu-id="1442e-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="1442e-109">Hello XML ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="1442e-109">hello XML looks like this:</span></span>

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

<span data-ttu-id="1442e-110">**Durée de vie des jetons d’accès** hello accès durée de vie de jeton peut être modifiée en modifiant la valeur hello à l’intérieur de hello `<Item>` avec hello clé = « token_lifetime_secs » en secondes.</span><span class="sxs-lookup"><span data-stu-id="1442e-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1442e-111">valeur par défaut Hello intégré est 3 600 secondes (60 minutes).</span><span class="sxs-lookup"><span data-stu-id="1442e-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="1442e-112">**Durée de vie de jeton ID** durée de vie hello ID peut être modifiée en modifiant la valeur hello à l’intérieur de hello `<Item>` avec hello clé = « id_token_lifetime_secs » en secondes.</span><span class="sxs-lookup"><span data-stu-id="1442e-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1442e-113">valeur par défaut Hello intégré est 3 600 secondes (60 minutes).</span><span class="sxs-lookup"><span data-stu-id="1442e-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="1442e-114">**Durée de vie de jeton d’actualisation** durée de vie hello actualisation peut être modifiée en modifiant la valeur hello à l’intérieur de hello `<Item>` avec hello clé = « refresh_token_lifetime_secs » en secondes.</span><span class="sxs-lookup"><span data-stu-id="1442e-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1442e-115">valeur par défaut Hello intégré est 1209600 secondes (14 jours).</span><span class="sxs-lookup"><span data-stu-id="1442e-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="1442e-116">**Actualiser le jeton durée de vie de fenêtre glissante** si vous souhaitez que tooset un jeton d’actualisation de tooyour de durée de vie fenêtre glissante, modifiez la valeur hello à l’intérieur `<Item>` avec hello clé = « rolling_refresh_token_lifetime_secs » en secondes.</span><span class="sxs-lookup"><span data-stu-id="1442e-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1442e-117">valeur par défaut Hello intégré est 7776000 (90 jours).</span><span class="sxs-lookup"><span data-stu-id="1442e-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="1442e-118">Si vous ne souhaitez pas tooenfore un glissante de durée de vie de fenêtre, remplacez cette ligne en :</span><span class="sxs-lookup"><span data-stu-id="1442e-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="1442e-119">**Revendication de l’émetteur (iss)** si vous souhaitez la revendication de l’émetteur (iss) toochange hello, modifier la valeur hello à l’intérieur de hello `<Item>` avec hello clé = « IssuanceClaimPattern ».</span><span class="sxs-lookup"><span data-stu-id="1442e-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="1442e-120">les valeurs applicables Hello sont `AuthorityAndTenantGuid` et `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="1442e-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="1442e-121">**Paramètre représentant les ID de stratégie de revendication** options hello pour définir cette valeur sont TFP (stratégie d’infrastructure approbation) et ACR (référence de contexte d’authentification).</span><span class="sxs-lookup"><span data-stu-id="1442e-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="1442e-122">Nous vous recommandons de définir cette tooTFP, toodo cela, vérifiez hello `<Item>` avec hello clé = « AuthenticationContextReferenceClaimPattern » existe et que la valeur hello est `None`.</span><span class="sxs-lookup"><span data-stu-id="1442e-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="1442e-123">Dans votre élément `<OutputClaims>`, ajoutez cet élément :</span><span class="sxs-lookup"><span data-stu-id="1442e-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="1442e-124">À l’ACR, supprimez hello `<Item>` avec hello clé = « AuthenticationContextReferenceClaimPattern ».</span><span class="sxs-lookup"><span data-stu-id="1442e-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="1442e-125">**Revendication de sujet (sub)** cette option est définie par défaut tooObjectID, si vous souhaitez que tooswitch cela trop`Not Supported`, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="1442e-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="1442e-126">Remplacez cette ligne :</span><span class="sxs-lookup"><span data-stu-id="1442e-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="1442e-127">par cette ligne :</span><span class="sxs-lookup"><span data-stu-id="1442e-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="1442e-128">Comportement de la session et SSO</span><span class="sxs-lookup"><span data-stu-id="1442e-128">Session behavior and SSO</span></span>
<span data-ttu-id="1442e-129">toochange votre comportement de session et des configurations de l’authentification unique, vous devez tooadd une `<UserJourneyBehaviors>` élément hello `<RelyingParty>` élément.</span><span class="sxs-lookup"><span data-stu-id="1442e-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="1442e-130">Hello `<UserJourneyBehaviors>` élément doit suivre immédiatement hello `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="1442e-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="1442e-131">Bonjour à l’intérieur de votre `<UserJourneyBehavors>` élément doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1442e-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="1442e-132">**Configuration de l’authentification unique (SSO)** toochange hello seule configuration de l’authentification, vous devez valeur hello toomodify `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="1442e-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="1442e-133">les valeurs applicables Hello sont `Tenant`, `Application`, `Policy` et `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="1442e-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="1442e-134">**Durée de vie de session (minutes) l’application Web** toochange hello hello web application durée de vie de session, vous devez toomodify valeur hello `<SessionExpiryInSeconds>` élément.</span><span class="sxs-lookup"><span data-stu-id="1442e-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="1442e-135">valeur par défaut de Hello dans les stratégies intégrées est 86 400 secondes (1 440 minutes).</span><span class="sxs-lookup"><span data-stu-id="1442e-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="1442e-136">**Délai d’expiration de session Web application** toochange hello web application délai d’expiration, vous devez valeur hello toomodify `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="1442e-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="1442e-137">les valeurs applicables Hello sont `Absolute` et `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="1442e-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
