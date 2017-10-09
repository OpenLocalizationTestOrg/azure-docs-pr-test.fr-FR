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
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a>Azure B2C Active Directory : Modifier tooadd nouvelles demandes d’inscription et configurer l’entrée d’utilisateur.

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Dans cet article, vous allez ajouter un nouveau fournies par l’utilisateur entrée (une revendication) utilisateur tooyour inscription voyage.  Vous configurerez l’entrée de hello comme une liste déroulante et définir s’il est requis.

Modifié par Sipi tootrigger test remise.

## <a name="prerequisites"></a>Composants requis

* Hello terminé les étapes dans l’article de hello [prise en main des stratégies personnalisées](active-directory-b2c-get-started-custom.md).  Test hello / l’inscription de l’inscription utilisateur voyage toosignup un nouveau compte local avant de continuer.


La collecte des données initiales de vos utilisateurs est obtenue via l’inscription/la connexion.  Des revendications supplémentaires peuvent être collectées ultérieurement via des parcours utilisateur de modification de profil. Chaque fois qu’Azure AD B2C rassemble des informations directement à partir de l’utilisateur de hello de manière interactive, hello identité expérience Framework utilise son `selfasserted provider`. étapes de Hello ci-dessous s’appliquent à chaque fois que ce fournisseur est utilisé.


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a>Définir hello revendication, son nom complet et le type d’entrée d’utilisateur de hello
Permet de demander à l’utilisateur de hello pour leur ville.  Ajouter hello suivant élément toohello `<ClaimsSchema>` élément dans le fichier de stratégie TrustFrameWorkExtensions hello :

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
Voici les autres options à que votre disposition ici toocustomize hello de revendication.  Pour un schéma complet, consultez toohello **le Guide de référence technique identité expérience Framework**.  Ce guide sera bientôt publié dans la section de référence hello.

* `<DisplayName>`est une chaîne qui définit hello orientés utilisateur *étiquette*

* `<UserHelpText>`permet à utilisateur de hello de comprendre ce qui est obligatoire

* `<UserInputType>`a hello quatre options suivantes en surbrillance ci-dessous :
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * `RadioSingleSelectduration` - Applique une seule sélection.
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

    * `DropdownSingleSelect`-Permet de sélectionner hello uniquement une valeur valide.

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


* `CheckboxMultiSelect`Permet la sélection d’une ou plusieurs valeurs hello.

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

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a>Ajouter hello revendication toohello connexion à distance et à la connexion dans le parcours de l’utilisateur

1. Ajouter des revendications hello comme un `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (trouvée dans le fichier de stratégie TrustFrameworkBase hello).  Notez que cette TechnicalProfile utilise hello SelfAssertedAttributeProvider.

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

2. Ajouter hello revendication toohello AAD-UserWriteUsingLogonEmail comme un `<PersistedClaim ClaimTypeReferenceId="city" />` annuaire toowrite hello revendication toohello AAD après sa collecte à partir de l’utilisateur de hello. Vous pouvez ignorer cette étape si vous ne préférez pas toopersist hello revendication dans le répertoire de hello pour un usage ultérieur.

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

3. Ajouter hello revendication toohello TechnicalProfile qui lit à partir du répertoire de hello lorsqu’un utilisateur se connecte en tant qu’un`<OutputClaim ClaimTypeReferenceId="city" />`

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

4. Ajouter hello `<OutputClaim ClaimTypeReferenceId="city" />` du fichier de stratégie toohello RP SignUporSignIn.xml pour que cette revendication est envoyée toohello application dans le jeton de hello après un voyage réussie de l’utilisateur.

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

## <a name="test-hello-custom-policy-using-run-now"></a>Tester une stratégie personnalisée de hello à l’aide de « Exécuter maintenant »

1. Ouvrez hello **Azure AD B2C panneau** et accédez trop**identité expérience Framework > stratégies personnalisées**.
2. Stratégie personnalisée hello que vous avez téléchargé, puis cliquez sur hello **exécuter maintenant** bouton.
3. Vous devez être en mesure de toosign à l’aide d’une adresse de messagerie.

écran d’inscription Hello en mode test doit ressembler toothis similaire :

![Capture d’écran de l’option d’inscription modifiée](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  Hello tooyour précédent jeton application incluront désormais hello `city` revendication comme indiqué ci-dessous
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

## <a name="optional-remove-email-verification-from-signup-journey"></a>Facultatif : Supprimer la vérification de l’adresse e-mail du parcours d’inscription

vérification du courrier électronique tooskip, auteur de stratégie de hello peut choisir tooremove `PartnerClaimType="Verified.Email"`. Hello adresse de messagerie est requis mais pas vérifiée, sauf si « Requis » = true est supprimée.  Réfléchissez bien pour savoir si cette option peut vous être utile !

Vérifié par courrier électronique est activé par défaut dans hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` dans fichier de stratégie TrustFrameworkBase hello dans le pack de démarrage hello :
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a>Étapes suivantes

Ajouter hello nouvelle revendication toohello des flux pour les connexions de réseaux sociaux compte en modifiant hello TechnicalProfiles répertoriées ci-dessous. Ces sont utilisées par compte sociale/fédéré connexions toowrite et lire les données d’utilisateur hello à l’aide de hello alternativeSecurityId comme hello localisateur.
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
