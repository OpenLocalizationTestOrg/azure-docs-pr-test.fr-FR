---
title: "Azure Active Directory B2C : Modifier l’inscription dans les stratégies personnalisées et configurer le fournisseur autodéclaré"
description: "Une procédure pas à pas sur l’ajout de revendications pour inscrire et configurer la saisie utilisateur"
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
ms.openlocfilehash: 64b9d904d7d070052e125b479f4719d208c9ff85
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-to-add-new-claims-and-configure-user-input"></a><span data-ttu-id="84e20-103">Azure Active Directory B2C : Modifier l’inscription pour ajouter de nouvelles recommandations et configurer la saisie utilisateur.</span><span class="sxs-lookup"><span data-stu-id="84e20-103">Azure Active Directory B2C: Modify sign up to add new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="84e20-104">Dans cet article, vous allez ajouter une nouvelle entrée fournie par l’utilisateur (une revendication) à votre parcours utilisateur d’inscription.</span><span class="sxs-lookup"><span data-stu-id="84e20-104">In this article, you will add a new user provided entry (a claim) to your signup user journey.</span></span>  <span data-ttu-id="84e20-105">Vous allez configurer l’entrée en tant que liste déroulante et définir si elle est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="84e20-105">You will configure the entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="84e20-106">Modifié par Sipi pour déclencher la remise de test.</span><span class="sxs-lookup"><span data-stu-id="84e20-106">Edited by Sipi to trigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84e20-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="84e20-107">Prerequisites</span></span>

* <span data-ttu-id="84e20-108">Suivez les étapes de l’article [Azure Active Directory B2C : bien démarrer avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="84e20-108">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="84e20-109">Testez le parcours utilisateur d’inscription/de connexion pour inscrire un nouveau compte local avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="84e20-109">Test the signup/signin user journey to signup a new local account before proceeding.</span></span>


<span data-ttu-id="84e20-110">La collecte des données initiales de vos utilisateurs est obtenue via l’inscription/la connexion.</span><span class="sxs-lookup"><span data-stu-id="84e20-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="84e20-111">Des revendications supplémentaires peuvent être collectées ultérieurement via des parcours utilisateur de modification de profil.</span><span class="sxs-lookup"><span data-stu-id="84e20-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="84e20-112">Chaque fois qu’Azure AD B2C rassemble des informations directement à partir de l’utilisateur de manière interactive, l’infrastructure d’expérience d’identité utilise son `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="84e20-112">Anytime Azure AD B2C gathers information directly from the user interactively, the Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="84e20-113">Les étapes ci-dessous s’appliquent à chaque fois que ce fournisseur est utilisé.</span><span class="sxs-lookup"><span data-stu-id="84e20-113">The steps below apply anytime this provider is used.</span></span>


## <a name="define-the-claim-its-display-name-and-the-user-input-type"></a><span data-ttu-id="84e20-114">Définir la revendication, son nom d’affichage et le type de saisie utilisateur</span><span class="sxs-lookup"><span data-stu-id="84e20-114">Define the claim, its display name and the user input type</span></span>
<span data-ttu-id="84e20-115">Demandons à l’utilisateur la ville où il vit.</span><span class="sxs-lookup"><span data-stu-id="84e20-115">Lets ask the user for their city.</span></span>  <span data-ttu-id="84e20-116">Ajoutez l’élément suivant à l’élément `<ClaimsSchema>` dans le fichier de stratégie TrustFrameWorkExtensions :</span><span class="sxs-lookup"><span data-stu-id="84e20-116">Add the following element to the `<ClaimsSchema>` element in the TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="84e20-117">Vous pouvez sélectionner d’autres choix pour personnaliser la revendication.</span><span class="sxs-lookup"><span data-stu-id="84e20-117">There are additional choices you can make here to customize the claim.</span></span>  <span data-ttu-id="84e20-118">Pour un schéma complet, reportez-vous au **guide de référence technique sur l’infrastructure d’expérience d’identité**.</span><span class="sxs-lookup"><span data-stu-id="84e20-118">For a full schema, refer to the **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="84e20-119">Ce guide sera bientôt publié dans la section de référence.</span><span class="sxs-lookup"><span data-stu-id="84e20-119">This guide will be published soon in the reference section.</span></span>

* <span data-ttu-id="84e20-120">`<DisplayName>` est une chaîne qui définit *l’étiquette* orientée utilisateur.</span><span class="sxs-lookup"><span data-stu-id="84e20-120">`<DisplayName>` is a string that defines the user-facing *label*</span></span>

* <span data-ttu-id="84e20-121">`<UserHelpText>` permet à l’utilisateur de comprendre ce qui est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="84e20-121">`<UserHelpText>` helps the user understand what is required</span></span>

* <span data-ttu-id="84e20-122">`<UserInputType>` comprend les quatre options suivantes mises en surbrillance ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="84e20-122">`<UserInputType>` has the following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="84e20-123">`RadioSingleSelectduration` - Applique une seule sélection.</span><span class="sxs-lookup"><span data-stu-id="84e20-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="84e20-124">`DropdownSingleSelect` - Permet la sélection d’une valeur valide uniquement.</span><span class="sxs-lookup"><span data-stu-id="84e20-124">`DropdownSingleSelect` - Allows the selection of only valid value.</span></span>

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


* <span data-ttu-id="84e20-126">`CheckboxMultiSelect` Permet la sélection d’une ou de plusieurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="84e20-126">`CheckboxMultiSelect` Allows for the selection of one or more values.</span></span>

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

## <a name="add-the-claim-to-the-sign-upsign-in-user-journey"></a><span data-ttu-id="84e20-128">Ajouter la revendication pour le parcours utilisateur d’inscription/de connexion</span><span class="sxs-lookup"><span data-stu-id="84e20-128">Add the claim to the sign up/sign in user journey</span></span>

1. <span data-ttu-id="84e20-129">Ajoutez la revendication en tant que `<OutputClaim ClaimTypeReferenceId="city"/>` à `LocalAccountSignUpWithLogonEmail` de TechnicalProfile (trouvé dans le fichier de stratégie TrustFrameworkBase).</span><span class="sxs-lookup"><span data-stu-id="84e20-129">Add the claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` to the TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in the TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="84e20-130">Notez que ce TechnicalProfile utilise le SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="84e20-130">Note this TechnicalProfile uses the SelfAssertedAttributeProvider.</span></span>

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
      <!-- Optional claims, to be collected from the user -->
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

2. <span data-ttu-id="84e20-131">Ajoutez la revendication à l’AAD-UserWriteUsingLogonEmail en tant que `<PersistedClaim ClaimTypeReferenceId="city" />` pour écrire la revendication dans le répertoire AAD après sa collecte auprès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="84e20-131">Add the claim to the AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` to write the claim to the AAD directory after collecting it from the user.</span></span> <span data-ttu-id="84e20-132">Vous pouvez ignorer cette étape si vous préférez ne pas conserver la revendication dans le répertoire pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="84e20-132">You may skip this step if you prefer not to persist the claim in the directory for future use.</span></span>

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

3. <span data-ttu-id="84e20-133">Ajouter la revendication au TechnicalProfile qui lit à partir du répertoire lorsqu’un utilisateur se connecte en tant que `<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="84e20-133">Add the claim to the TechnicalProfile that reads from the directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for the provided user ID.</Item>
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

4. <span data-ttu-id="84e20-134">Ajoutez `<OutputClaim ClaimTypeReferenceId="city" />` au fichier de stratégie de partie de confiance SignUporSignIn.xml pour que cette revendication soit envoyée à l’application dans le jeton après un parcours utilisateur réussi.</span><span class="sxs-lookup"><span data-stu-id="84e20-134">Add the `<OutputClaim ClaimTypeReferenceId="city" />` to the RP policy file SignUporSignIn.xml so this claim is sent to the application in the token after a successful user journey.</span></span>

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

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="84e20-135">Tester la stratégie personnalisée avec « Exécuter maintenant »</span><span class="sxs-lookup"><span data-stu-id="84e20-135">Test the custom policy using "Run Now"</span></span>

1. <span data-ttu-id="84e20-136">Ouvrez le **panneau Azure AD B2C** et accédez à **Infrastructure d’expérience d’identité > Stratégies personnalisées**.</span><span class="sxs-lookup"><span data-stu-id="84e20-136">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="84e20-137">Sélectionnez la stratégie personnalisée que vous avez téléchargée, puis cliquez sur le bouton **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="84e20-137">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="84e20-138">Vous devriez pouvoir vous inscrire à l’aide d’une adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="84e20-138">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="84e20-139">L’écran d’inscription en mode test doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="84e20-139">The signup screen in test mode should look similar to this:</span></span>

![Capture d’écran de l’option d’inscription modifiée](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="84e20-141">Le jeton qui est renvoyé à vote application inclut désormais la revendication `city` comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="84e20-141">The token back to your application will now include the `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="84e20-142">Facultatif : Supprimer la vérification de l’adresse e-mail du parcours d’inscription</span><span class="sxs-lookup"><span data-stu-id="84e20-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="84e20-143">Pour ignorer la vérification de l’adresse e-mail, l’auteur de la stratégie peut choisir de supprimer `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="84e20-143">To skip email verification, the policy author can choose to remove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="84e20-144">L’adresse e-mail sera requise mais pas vérifiée, sauf si « Requis » = true est supprimé.</span><span class="sxs-lookup"><span data-stu-id="84e20-144">The email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="84e20-145">Réfléchissez bien pour savoir si cette option peut vous être utile !</span><span class="sxs-lookup"><span data-stu-id="84e20-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="84e20-146">La vérification de l’adresse e-mail est activée par défaut dans `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">`, dans le fichier de stratégie TrustFrameworkBase du pack de démarrage :</span><span class="sxs-lookup"><span data-stu-id="84e20-146">Verified email is enabled by default in the `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in the TrustFrameworkBase policy file in the starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="84e20-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84e20-147">Next steps</span></span>

<span data-ttu-id="84e20-148">Ajoutez la nouvelle revendication aux flux des connexions aux comptes sociaux en modifiant les éléments TechnicalProfiles répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="84e20-148">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed below.</span></span> <span data-ttu-id="84e20-149">Ces derniers sont utilisés par les connexions aux comptes sociaux/fédérés pour écrire et lire les données utilisateur avec alternativeSecurityId en tant que localisateur.</span><span class="sxs-lookup"><span data-stu-id="84e20-149">These are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
