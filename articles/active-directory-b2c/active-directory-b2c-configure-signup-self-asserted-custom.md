---
title: "Azure Active Directory B2C : Modifier l’inscription dans les stratégies personnalisées et configurer le fournisseur autodéclaré"
description: "Une procédure pas à pas sur l’ajout de revendications toosign des et configurer l’entrée d’utilisateur hello"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: tbd
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/29/2017
ms.author: joroja
ms.openlocfilehash: c31d737263fef3e771bdf451b809b0ca522c8fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a><span data-ttu-id="748d3-103">Azure B2C Active Directory : Modifier tooadd nouvelles demandes d’inscription et configurer l’entrée d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="748d3-103">Azure Active Directory B2C: Modify sign up tooadd new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="748d3-104">Dans cet article, vous allez ajouter un nouveau fournies par l’utilisateur entrée (une revendication) utilisateur tooyour inscription voyage.</span><span class="sxs-lookup"><span data-stu-id="748d3-104">In this article, you will add a new user provided entry (a claim) tooyour signup user journey.</span></span>  <span data-ttu-id="748d3-105">Vous configurerez l’entrée de hello comme une liste déroulante et définir s’il est requis.</span><span class="sxs-lookup"><span data-stu-id="748d3-105">You will configure hello entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="748d3-106">Modifié par Sipi tootrigger test remise.</span><span class="sxs-lookup"><span data-stu-id="748d3-106">Edited by Sipi tootrigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="748d3-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="748d3-107">Prerequisites</span></span>

* <span data-ttu-id="748d3-108">Hello terminé les étapes dans l’article de hello [prise en main des stratégies personnalisées](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="748d3-108">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="748d3-109">Test hello / l’inscription de l’inscription utilisateur voyage toosignup un nouveau compte local avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="748d3-109">Test hello signup/signin user journey toosignup a new local account before proceeding.</span></span>


<span data-ttu-id="748d3-110">La collecte des données initiales de vos utilisateurs est obtenue via l’inscription/la connexion.</span><span class="sxs-lookup"><span data-stu-id="748d3-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="748d3-111">Des revendications supplémentaires peuvent être collectées ultérieurement via des parcours utilisateur de modification de profil.</span><span class="sxs-lookup"><span data-stu-id="748d3-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="748d3-112">Chaque fois qu’Azure AD B2C rassemble des informations directement à partir de l’utilisateur de hello de manière interactive, hello identité expérience Framework utilise son `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="748d3-112">Anytime Azure AD B2C gathers information directly from hello user interactively, hello Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="748d3-113">étapes de Hello ci-dessous s’appliquent à chaque fois que ce fournisseur est utilisé.</span><span class="sxs-lookup"><span data-stu-id="748d3-113">hello steps below apply anytime this provider is used.</span></span>


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a><span data-ttu-id="748d3-114">Définir hello revendication, son nom complet et le type d’entrée d’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="748d3-114">Define hello claim, its display name and hello user input type</span></span>
<span data-ttu-id="748d3-115">Permet de demander à l’utilisateur de hello pour leur ville.</span><span class="sxs-lookup"><span data-stu-id="748d3-115">Lets ask hello user for their city.</span></span>  <span data-ttu-id="748d3-116">Ajouter hello suivant élément toohello `<ClaimsSchema>` élément dans le fichier de stratégie TrustFrameWorkExtensions hello :</span><span class="sxs-lookup"><span data-stu-id="748d3-116">Add hello following element toohello `<ClaimsSchema>` element in hello TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="748d3-117">Voici les autres options à que votre disposition ici toocustomize hello de revendication.</span><span class="sxs-lookup"><span data-stu-id="748d3-117">There are additional choices you can make here toocustomize hello claim.</span></span>  <span data-ttu-id="748d3-118">Pour un schéma complet, consultez toohello **le Guide de référence technique identité expérience Framework**.</span><span class="sxs-lookup"><span data-stu-id="748d3-118">For a full schema, refer toohello **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="748d3-119">Ce guide sera bientôt publié dans la section de référence hello.</span><span class="sxs-lookup"><span data-stu-id="748d3-119">This guide will be published soon in hello reference section.</span></span>

* <span data-ttu-id="748d3-120">`<DisplayName>`est une chaîne qui définit hello orientés utilisateur *étiquette*</span><span class="sxs-lookup"><span data-stu-id="748d3-120">`<DisplayName>` is a string that defines hello user-facing *label*</span></span>

* <span data-ttu-id="748d3-121">`<UserHelpText>`permet à utilisateur de hello de comprendre ce qui est obligatoire</span><span class="sxs-lookup"><span data-stu-id="748d3-121">`<UserHelpText>` helps hello user understand what is required</span></span>

* <span data-ttu-id="748d3-122">`<UserInputType>`a hello quatre options suivantes en surbrillance ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="748d3-122">`<UserInputType>` has hello following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="748d3-123">`RadioSingleSelectduration` - Applique une seule sélection.</span><span class="sxs-lookup"><span data-stu-id="748d3-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * <span data-ttu-id="748d3-124">`DropdownSingleSelect`-Permet de sélectionner hello uniquement une valeur valide.</span><span class="sxs-lookup"><span data-stu-id="748d3-124">`DropdownSingleSelect` - Allows hello selection of only valid value.</span></span>

![Capture d’écran de l’option de liste déroulante](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* <span data-ttu-id="748d3-126">`CheckboxMultiSelect`Permet la sélection d’une ou plusieurs valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="748d3-126">`CheckboxMultiSelect` Allows for hello selection of one or more values.</span></span>

![Capture d’écran de l’option de sélection multiple](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a><span data-ttu-id="748d3-128">Ajouter hello revendication toohello connexion à distance et à la connexion dans le parcours de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="748d3-128">Add hello claim toohello sign up/sign in user journey</span></span>

1. <span data-ttu-id="748d3-129">Ajouter des revendications hello comme un `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (trouvée dans le fichier de stratégie TrustFrameworkBase hello).</span><span class="sxs-lookup"><span data-stu-id="748d3-129">Add hello claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in hello TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="748d3-130">Notez que cette TechnicalProfile utilise hello SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="748d3-130">Note this TechnicalProfile uses hello SelfAssertedAttributeProvider.</span></span>

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
    </CryptographicKeys>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
      <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" />
      <OutputClaim ClaimTypeReferenceId="newUser" />
      <!-- Optional claims, toobe collected from hello user -->
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. <span data-ttu-id="748d3-131">Ajouter hello revendication toohello AAD-UserWriteUsingLogonEmail comme un `<PersistedClaim ClaimTypeReferenceId="city" />` annuaire toowrite hello revendication toohello AAD après sa collecte à partir de l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="748d3-131">Add hello claim toohello AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello claim toohello AAD directory after collecting it from hello user.</span></span> <span data-ttu-id="748d3-132">Vous pouvez ignorer cette étape si vous ne préférez pas toopersist hello revendication dans le répertoire de hello pour un usage ultérieur.</span><span class="sxs-lookup"><span data-stu-id="748d3-132">You may skip this step if you prefer not toopersist hello claim in hello directory for future use.</span></span>

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. <span data-ttu-id="748d3-133">Ajouter hello revendication toohello TechnicalProfile qui lit à partir du répertoire de hello lorsqu’un utilisateur se connecte en tant qu’un`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="748d3-133">Add hello claim toohello TechnicalProfile that reads from hello directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for hello provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. <span data-ttu-id="748d3-134">Ajouter hello `<OutputClaim ClaimTypeReferenceId="city" />` du fichier de stratégie toohello RP SignUporSignIn.xml pour que cette revendication est envoyée toohello application dans le jeton de hello après un voyage réussie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="748d3-134">Add hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP policy file SignUporSignIn.xml so this claim is sent toohello application in hello token after a successful user journey.</span></span>

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="748d3-135">Tester une stratégie personnalisée de hello à l’aide de « Exécuter maintenant »</span><span class="sxs-lookup"><span data-stu-id="748d3-135">Test hello custom policy using "Run Now"</span></span>

1. <span data-ttu-id="748d3-136">Ouvrez hello **Azure AD B2C panneau** et accédez trop**identité expérience Framework > stratégies personnalisées**.</span><span class="sxs-lookup"><span data-stu-id="748d3-136">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="748d3-137">Stratégie personnalisée hello que vous avez téléchargé, puis cliquez sur hello **exécuter maintenant** bouton.</span><span class="sxs-lookup"><span data-stu-id="748d3-137">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="748d3-138">Vous devez être en mesure de toosign à l’aide d’une adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="748d3-138">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="748d3-139">écran d’inscription Hello en mode test doit ressembler toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="748d3-139">hello signup screen in test mode should look similar toothis:</span></span>

![Capture d’écran de l’option d’inscription modifiée](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="748d3-141">Hello tooyour précédent jeton application incluront désormais hello `city` revendication comme indiqué ci-dessous</span><span class="sxs-lookup"><span data-stu-id="748d3-141">hello token back tooyour application will now include hello `city` claim as shown below</span></span>
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="748d3-142">Facultatif : Supprimer la vérification de l’adresse e-mail du parcours d’inscription</span><span class="sxs-lookup"><span data-stu-id="748d3-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="748d3-143">vérification du courrier électronique tooskip, auteur de stratégie de hello peut choisir tooremove `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="748d3-143">tooskip email verification, hello policy author can choose tooremove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="748d3-144">Hello adresse de messagerie est requis mais pas vérifiée, sauf si « Requis » = true est supprimée.</span><span class="sxs-lookup"><span data-stu-id="748d3-144">hello email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="748d3-145">Réfléchissez bien pour savoir si cette option peut vous être utile !</span><span class="sxs-lookup"><span data-stu-id="748d3-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="748d3-146">Vérifié par courrier électronique est activé par défaut dans hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` dans fichier de stratégie TrustFrameworkBase hello dans le pack de démarrage hello :</span><span class="sxs-lookup"><span data-stu-id="748d3-146">Verified email is enabled by default in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in hello TrustFrameworkBase policy file in hello starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="748d3-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="748d3-147">Next steps</span></span>

<span data-ttu-id="748d3-148">Ajouter hello nouvelle revendication toohello des flux pour les connexions de réseaux sociaux compte en modifiant hello TechnicalProfiles répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="748d3-148">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed below.</span></span> <span data-ttu-id="748d3-149">Ces sont utilisées par compte sociale/fédéré connexions toowrite et lire les données d’utilisateur hello à l’aide de hello alternativeSecurityId comme hello localisateur.</span><span class="sxs-lookup"><span data-stu-id="748d3-149">These are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
