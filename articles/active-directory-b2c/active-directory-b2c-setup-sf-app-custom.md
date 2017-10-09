---
title: "Azure Active Directory B2C : ajout d’un fournisseur SAML Salesforce à l’aide de stratégies personnalisées | Microsoft Docs"
description: "En savoir plus sur la façon de toocreate et gérer des stratégies personnalisées Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a>Azure Active Directory B2C : connexion à l’aide de comptes Salesforce via SAML

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Cet article vous montre comment toouse [des stratégies personnalisées](active-directory-b2c-overview-custom.md) tooset des connectez-vous pour les utilisateurs à partir d’une organisation de force de vente spécifique.

## <a name="prerequisites"></a>Composants requis

### <a name="azure-ad-b2c-setup"></a>Configuration d’Azure AD B2C

Vérifiez que vous avez effectué toutes les étapes de hello qui vous montrent comment trop[prise en main des stratégies personnalisées](active-directory-b2c-get-started-custom.md) dans Azure Active Directory B2C (B2C Active Directory de Azure).

Vous avez notamment vu les points suivants :

* Créer un locataire Azure AD B2C
* Créer une application Azure AD B2C
* Inscrire deux applications de moteur de stratégie
* Configurer des clés
* Configurer le pack de démarrage hello.

### <a name="salesforce-setup"></a>Configuration Salesforce

Dans cet article, nous supposons que vous avez déjà effectué les suivant hello :

* Vous êtes déjà inscrit à un compte Salesforce. Vous pouvez vous inscrire pour bénéficier d’un [compte Édition Développeur gratuit](https://developer.salesforce.com/signup).
* Vous avez déjà [configuré un domaine My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) pour votre organisation Salesforce.

## <a name="set-up-salesforce-so-users-can-federate"></a>Configurer Salesforce pour que les utilisateurs puissent fédérer

toohelp Azure AD B2C communiquer avec Salesforce, vous avez besoin d’URL de métadonnées tooget hello Salesforce.

### <a name="set-up-salesforce-as-an-identity-provider"></a>Configurer Salesforce en tant que fournisseur d’identité

> [!NOTE]
> Dans cet article, nous supposons que vous utilisez [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).

1. [Connectez-vous à tooSalesforce](https://login.salesforce.com/). 
2. Dans hello gauche menu, sous **paramètres**, développez **identité**, puis cliquez sur **fournisseur d’identité**.
3. Cliquez sur **Enable Identity Provider (Activer le fournisseur d’identité)**.
4. Sous **certificat de hello sélectionnez**, sélectionnez certificat hello toocommunicate toouse de Salesforce avec Azure Active Directory B2C. (Vous pouvez utiliser de certificat par défaut de hello). Cliquez sur **Enregistrer**. 

### <a name="create-a-connected-app-in-salesforce"></a>Créer une application connectée dans Salesforce

1. Sur hello **fournisseur d’identité** page, aller trop**fournisseurs de services**.
2. Cliquez sur **Service Providers are now created via Connected Apps (Les fournisseurs de services sont maintenant créés via des applications connectées). Cliquez ici.**
3. Sous **des informations de base**, entrez les valeurs hello requis pour votre application connectée.
4. Sous **paramètres de l’application Web**, sélectionnez hello **SAML d’activer** case à cocher.
5. Bonjour **ID d’entité** , saisissez hello suivant l’URL. Veillez à remplacer la valeur hello pour `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. Bonjour **URL ACS** , saisissez hello suivant l’URL. Veillez à remplacer la valeur hello pour `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. Laissez les valeurs par défaut de hello pour tous les autres paramètres.
8. Faites défiler bas toohello de liste de hello, puis cliquez sur **enregistrer**.

### <a name="get-hello-metadata-url"></a>Obtenir l’URL des métadonnées de hello

1. Sur la page de vue d’ensemble de hello de votre application connectée, cliquez sur **gérer**.
2. Copiez la valeur hello pour **point de terminaison de métadonnées de découverte**, puis enregistrez-le. Vous l’utiliserez plus loin dans cet article.

### <a name="set-up-salesforce-users-toofederate"></a>Configurer la force de vente utilisateurs toofederate

1. Sur hello **gérer** page de votre application connectée, accédez trop**profils**.
2. Cliquez sur **Manage Profiles (Gérer les profils)**.
3. Sélectionnez les profils hello (ou groupes d’utilisateurs) que vous souhaitez toofederate avec Azure Active Directory B2C. En tant qu’un administrateur système, sélectionnez hello **administrateur système** case, afin que vous pouvez fédérer à l’aide de votre compte Salesforce.

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a>Générer un certificat de signature pour Azure AD B2C

Les demandes envoyées tooSalesforce besoin toobe est signé par Azure AD B2C. toogenerate un certificat de signature, ouvrez Azure PowerShell et exécutez hello suivant les commandes.

> [!NOTE]
> Assurez-vous que vous mettez à jour nom hello du client et le mot de passe dans les premières lignes de deux hello.

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a>Ajouter tooAzure de certificat signature hello SAML AD B2C

Télécharger hello client tooyour Azure AD B2C de certificat de signature : 

1. Accédez tooyour Azure AD B2C locataire. Cliquez sur **Paramètres** > **Infrastructure d’expérience d’identité** > **Clés de stratégie**.
2. Cliquez sur **+Ajouter**, puis :
    1. Cliquez sur **Options** > **Charger**.
    2. Entrez un **Nom** (par exemple, SAMLSigningCert). préfixe de Hello *B2C_1A_* est automatiquement ajouté nom toohello de votre clé.
    3. tooselect votre certificat, sélectionnez **contrôle du fichier de téléchargement**. 
    4. Entrez le mot de passe du certificat hello que vous définissez dans le script PowerShell de hello.
3. Cliquez sur **Créer**.
4. Vérifiez que vous avez créé une clé (par exemple, B2C_1A_SAMLSigningCert). Prenez note du nom complet de hello (y compris *B2C_1A_*). Vous ferez référence clé toothis plus loin dans la stratégie de hello.

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a>Créer hello fournisseur de revendications Salesforce SAML dans votre stratégie de base

Vous devez toodefine Salesforce comme fournisseur de revendications pour les utilisateurs peuvent se connecter à l’aide de Salesforce. En d’autres termes, vous devez toospecify hello point de terminaison qui communiquent avec Azure AD B2C. point de terminaison Hello sera *fournir* un ensemble de *revendications* que Azure AD B2C utilise tooverify authentifié un utilisateur spécifique. toodo, ajoutez un `<ClaimsProvider>` pour Salesforce dans le fichier d’extension hello de votre stratégie :

1. Dans votre répertoire de travail, ouvrez le fichier d’extension hello (TrustFrameworkExtensions.xml).
2. Recherche hello `<ClaimsProviders>` section. Si elle n’existe pas, créez-le sous le nœud racine de hello.
3. Ajoutez un `<ClaimsProvider>` :

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
          </OutputClaims>
          <OutputClaimsTransformations>
            <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
            <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
            <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
            <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
          </OutputClaimsTransformations>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

Sous hello `<ClaimsProvider>` nœud :

1. Modifier la valeur hello pour `<Domain>` tooa valeur unique qui distingue `<ClaimsProvider>` à partir d’autres fournisseurs d’identité.
2. Mettre à jour la valeur hello pour `<DisplayName>` fournisseur de revendications de nom d’affichage tooa pour hello. Cette valeur n’est pas utilisée actuellement.

### <a name="update-hello-technical-profile"></a>Mettre à jour le profil de technique hello

tooget un jeton SAML de Salesforce, définir des protocoles hello que Azure AD B2C utilisera toocommunicate avec Azure Active Directory (Azure AD). Cela Bonjour `<TechnicalProfile>` élément de `<ClaimsProvider>`:

1. Mise à jour ID hello Hello `<TechnicalProfile>` nœud. Cet ID est utilisé toorefer toothis profil technique à partir d’autres parties de la stratégie de hello.
2. Mettre à jour la valeur hello pour `<DisplayName>`. Cette valeur est affichée sur le bouton hello de connexion dans votre page de connexion.
3. Mettre à jour la valeur hello pour `<Description>`.
4. Force de vente utilise le protocole de hello SAML 2.0. Que cette valeur hello `<Protocol>` est **SAML2**.

Hello de mise à jour `<Metadata>` section Bonjour précédant les paramètres XML tooreflect hello pour votre compte Salesforce. Bonjour XML, mettez à jour les valeurs de métadonnées hello :

1. Mettre à jour la valeur hello `<Item Key="PartnerEntity">` avec l’URL de métadonnées hello Salesforce vous avez copiée précédemment. Il a hello suivant le format : 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. Bonjour `<CryptographicKeys>` section, la valeur hello de mise à jour pour les deux instances de `StorageReferenceId` nom toohello de clé hello de votre certificat de signature (par exemple, B2C_1A_SAMLSigningCert).

### <a name="upload-hello-extension-file-for-verification"></a>Télécharger le fichier d’extension hello pour la vérification

Votre stratégie est désormais configurée pour que Azure AD B2C sait comment toocommunicate auprès de Salesforce. Essayez de télécharger le fichier d’extension hello de votre stratégie, tooverify qu’il ne sont pas tous les problèmes jusqu'à présent. fichier d’extension tooupload hello de votre stratégie :

1. Dans votre locataire Azure AD B2C, accédez à toohello **toutes les stratégies** panneau.
2. Sélectionnez hello **remplacer la stratégie de hello si elle existe** case à cocher.
3. Téléchargez le fichier d’extension hello (TrustFrameworkExtensions.xml). Vérifiez que sa validation n’échoue pas.

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a>Inscrire hello voyage de Salesforce SAML revendications fournisseur tooa utilisateur

Ensuite, ajoutez hello tooone de fournisseur d’identité Salesforce SAML de votre parcours de l’utilisateur. À ce stade, le fournisseur d’identité hello a été configuré, mais il n’est pas disponible sur les pages d’inscription ou de la connexion du utilisateur hello. tooadd hello identité fournisseur tooa-page de connexion, commencez par créer un doublon d’un déplacement de modèle à l’utilisateur existant. Ensuite, modifiez le modèle de hello afin qu’il puisse également le fournisseur d’identité Azure AD hello.

1. Ouvrez le fichier de base hello de votre stratégie (par exemple, TrustFrameworkBase.xml).
2. Recherche hello `<UserJourneys>` élément, puis hello copie entière `<UserJourney>` valeur, Id = « SignUpOrSignIn ».
3. Ouvrez le fichier d’extension hello (par exemple, TrustFrameworkExtensions.xml). Recherche hello `<UserJourneys>` élément. Si l’élément de hello n’existe pas, créez-le.
4. Hello coller ensemble copié `<UserJourney>` en tant qu’enfant de hello `<UserJourneys>` élément.
5. Renommer des ID hello Hello nouvelle `<UserJourney>` (par exemple, SignUpOrSignUsingContoso).

### <a name="display-hello-identity-provider-button"></a>Bouton d’affichage hello identité fournisseur

Hello `<ClaimsProviderSelection>` élément est le bouton de fournisseur d’identité tooan analogue sur une page d’inscription ou de connexion. En ajoutant un `<ClaimsProviderSelection>` élément pour Salesforce, un nouveau bouton s’affiche lorsqu’un utilisateur est toothis page. bouton de fournisseur toodisplay hello identité :

1. Bonjour `<UserJourney>` que vous avez créé, recherche hello `<OrchestrationStep>` avec `Order="1"`.
2. Ajoutez hello XML suivant :

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. Définissez `TargetClaimsExchangeId` tooa les valeur logique. Nous vous recommandons de suivant hello même convention que d’autres (par exemple,  *\[ClaimProviderName\]Exchange*).

### <a name="link-hello-identity-provider-button-tooan-action"></a>Action du lien hello identité fournisseur bouton tooan

Maintenant que vous avez un bouton de fournisseur d’identité en place, liez-le tooan action. Dans ce cas, l’action de hello est pour toocommunicate Azure AD B2C avec Salesforce tooreceive un jeton SAML. Faire cela en liant le profil de technique hello pour votre SAML Salesforce fournisseur de revendications :

1. Bonjour `<UserJourney>` nœud, rechercher hello `<OrchestrationStep>` avec `Order="2"`.
2. Ajoutez hello XML suivant :

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. Mise à jour `Id` toohello même valeur que vous avez utilisé précédemment pour `TargetClaimsExchangeId`.
4. Mise à jour `TechnicalProfileReferenceId` toohello `Id` Hello technique du profil que vous avez créé précédemment (par exemple, ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Télécharger le fichier d’extension de mise à jour de hello

Vous avez terminé la modification d’extension hello. Enregistrez et chargez ce fichier. Faites en sorte que toutes les validations réussissent.

### <a name="update-hello-relying-party-file"></a>Mettre à jour le fichier de partie de confiance hello

Ensuite, mettre à jour les hello fichier partie de confiance du tiers (RP) qui lance le voyage utilisateur hello que vous avez créé :

1. Faites une copie de SignUpOrSignIn.xml dans votre répertoire de travail. Ensuite, renommez-le (par exemple, SignUpOrSignInWithAAD.xml).
2. Hello de fichier et de mise à jour de nouveau hello ouvrir `PolicyId` attribut `<TrustFrameworkPolicy>` avec une valeur unique. Il s’agit de nom hello de votre stratégie (par exemple, SignUpOrSignInWithAAD).
3. Modifier hello `ReferenceId` attribut `<DefaultUserJourney>` toomatch hello `Id` de hello nouvel utilisateur voyage que vous avez créé (par exemple, SignUpOrSignUsingContoso).
4. Enregistrer vos modifications et télécharger les fichiers hello.

## <a name="test-and-troubleshoot"></a>Tester et résoudre les problèmes

stratégie personnalisée tootest hello que vous venez de télécharger, Bonjour portail Azure, accédez toohello Panneau de la stratégie, puis cliquez sur **exécuter maintenant**. En cas d’échec, consultez [Résoudre les problèmes des stratégies personnalisées](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Étapes suivantes

Fournir des commentaires trop[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
