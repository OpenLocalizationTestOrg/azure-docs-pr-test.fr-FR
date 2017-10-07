---
title: "Azure Active Directory B2C : ajouter un compte Microsoft (MSA) comme fournisseur d’identité à l’aide de stratégies personnalisées"
description: "Exemple utilisant Microsoft comme fournisseur d’identité à l’aide du protocole OpenID Connect (OIDC)"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a>Azure Active Directory B2C : ajouter un compte Microsoft (MSA) comme fournisseur d’identité à l’aide de stratégies personnalisées

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Cet article vous explique comment tooenable connectez-vous pour les utilisateurs de compte Microsoft (MSA) via l’utilisation de hello de [des stratégies personnalisées](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Composants requis
Hello terminé les étapes Bonjour [mise en route avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md) l’article.

Ces étapes sont les suivantes :

1.  créer une application de compte Microsoft ;
2.  Ajout de hello Microsoft compte application clé tooAzure AD B2C
3.  Ajout d’une stratégie de tooa de fournisseur de revendications
4.  L’inscription de voyage de hello Account Microsoft revendications fournisseur tooa utilisateur
5.  Téléchargement de stratégie de hello tooan Azure AD B2C de client et de le tester

## <a name="create-a-microsoft-account-application"></a>Créer une application de compte Microsoft
toouse de compte Microsoft en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application de compte Microsoft et lui fournir les paramètres appropriés hello. Il vous faut un compte Microsoft. Si vous n’en avez pas, rendez-vous sur [https://www.live.com/](https://www.live.com/).

1.  Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) et connectez-vous avec vos informations d’identification du compte Microsoft.
2.  Cliquez sur **Ajouter une application**.

    ![Compte Microsoft : ajouter une application](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  Donnez un **Nom** à votre application, indiquez une **adresse e-mail de contact**, décochez la case **Aidez-moi à commencer** et cliquez sur **Créer**.

    ![Compte Microsoft : inscrire une application](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  Copiez la valeur hello **Id de l’Application**. Vous en avez besoin tooconfigure compte Microsoft en tant que fournisseur d’identité dans votre client.

    ![Compte Microsoft - copier la valeur d’Id de l’Application hello](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  Cliquez sur **Ajouter une plateforme**.

    ![Compte Microsoft - Ajouter une plateforme](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  Dans la liste des plateformes hello, choisissez **Web**.

    ![Compte Microsoft, à partir de la liste des plateformes hello choisissez Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **URI de redirection** champ. Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com).

    ![Compte Microsoft : définir des URL de redirection](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  Cliquez sur **générer un nouveau mot de passe** sous hello **Application Secrets** section. Copiez le nouveau mot de passe hello affiché sur l’écran. Vous en avez besoin tooconfigure compte Microsoft en tant que fournisseur d’identité dans votre client. Ce mot de passe est une information d’identification de sécurité importante.

    ![Compte Microsoft - générer un nouveau mot de passe](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Compte Microsoft - copie hello nouveau mot de passe](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  Case à cocher hello indiquant **prise en charge du Kit de développement logiciel Live** sous hello **Options avancées** section. Cliquez sur **Enregistrer**.

    ![Compte Microsoft - Support du Kit SDK Live](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a>Ajouter hello Microsoft compte application clé tooAzure AD B2C
Fédération avec des comptes Microsoft requiert une clé secrète client pour tootrust de compte Microsoft Azure AD B2C au nom de l’application hello. Vous devez toostore votre secert d’application de compte Microsoft Azure AD B2C locataire :   

1.  Accédez tooyour Azure AD B2C client, puis sélectionnez **B2C paramètres** > **infrastructure expérience d’identité**
2.  Sélectionnez **clés de stratégie** tooview hello disponibles dans votre client.
3.  Cliquez sur **+Ajouter**.
4.  Pour **Options**, utilisez **Manuel**.
5.  Pour **Nom**, utilisez `MSASecret`.  
    préfixe de Hello `B2C_1A_` peuvent être ajoutées automatiquement.
6.  Bonjour **Secret** , entrez votre clé secrète d’application Microsoft à partir de https://apps.dev.microsoft.com
7.  Pour **Utilisation de la clé**, utilisez **Signature**.
8.  Cliquez sur **Créer**
9.  Vérifiez que vous avez créé la clé de hello `B2C_1A_MSASecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Ajouter un fournisseur de revendications à une stratégie d’extension
Si vous souhaitez que les utilisateurs toosign à l’aide de Microsoft Account, vous devez toodefine Account Microsoft en tant que fournisseur de revendications. En d’autres termes, vous devez toospecify un point de terminaison Azure AD B2C communique avec. point de terminaison Hello fournit un ensemble de revendications qui sont utilisées par Azure AD B2C tooverify authentifié un utilisateur spécifique.

Définissez le compte Microsoft comme fournisseur de revendications, en ajoutant le nœud `<ClaimsProvider>` à votre fichier de stratégie d’extension :

1.  Ouvrez le fichier de stratégie d’extension hello (TrustFrameworkExtensions.xml) à partir de votre répertoire de travail. Si vous avez besoin d’un éditeur XML, [essayez Visual Studio Code](https://code.visualstudio.com/download), un éditeur multiplateforme léger.
2.  Recherche hello `<ClaimsProviders>` section
3.  Ajoutez suivant extrait de code XML sous hello `ClaimsProviders` élément :

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  Remplacez la valeur `client_id` par votre ID client d’application de compte Microsoft.

5.  Enregistrez le fichier de hello.

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Inscrire tooSign de fournisseur de revendications de Account Microsoft hello haut ou connectez-vous le voyage d’utilisateur

À ce stade, le fournisseur d’identité hello a été configuré, mais il n’est pas disponible dans les écrans de connexion-haut/connectez-vous hello. Maintenant vous devez tooyour utilisateur du fournisseur tooadd hello Account Microsoft identité `SignUpOrSignIn` parcours de l’utilisateur. toomake il est disponible, nous créons un doublon d’un déplacement de modèle à l’utilisateur existant.  Puis nous ajouter le fournisseur d’identité hello Account Microsoft :

> [!NOTE]
>
>Si vous avez copiés précédemment hello `<UserJourneys>` élément à partir du fichier de base de votre fichier d’extension de stratégie toohello `TrustFrameworkExtensions.xml`, vous pouvez ignorer la section de toothis.

1.  Ouvrez le fichier de base hello de votre stratégie (par exemple, TrustFrameworkBase.xml).
2.  Recherche hello `<UserJourneys>` élément et copie hello ensemble du contenu de `<UserJourneys>` nœud.
3.  Ouvrez le fichier d’extension hello (par exemple, TrustFrameworkExtensions.xml) et recherche hello `<UserJourneys>` élément. Si l’élément de hello n’existe pas, ajoutez-en un.
4.  Coller le contenu entier de hello de `<UserJournesy>` nœud que vous avez copié en tant qu’enfant de hello `<UserJourneys>` élément.

### <a name="display-hello-button"></a>Bouton d’affichage hello
Hello `<ClaimsProviderSelections>` élément définit la liste hello des options de sélection de fournisseur de revendications et leur ordre.  `<ClaimsProviderSelection>`élément est un bouton de fournisseur d’identité tooan analogue sur une connexion-haut/page de connexion. Si vous ajoutez un `<ClaimsProviderSelection>` élément pour le compte Microsoft, un nouveau bouton apparaît lorsqu’un utilisateur arrive sur la page de hello. tooadd cet élément :

1.  Recherche hello `<UserJourney>` nœud incluant `Id="SignUpOrSignIn"` dans voyage utilisateur hello que vous avez copiée.
2.  Recherchez hello `<OrchestrationStep>` nœud qui inclut`Order="1"`
3.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Action de lien hello bouton tooan
Maintenant que vous avez un bouton en place, vous devez toolink il tooan action. action de Hello, dans ce cas, est de toocommunicate Azure AD B2C avec Microsoft Account tooreceive un jeton. Lier action tooan du bouton hello en liant le profil de technique hello pour votre fournisseur de revendications Account Microsoft :

1.  Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.
2.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * Assurez-vous de hello `Id` a hello même valeur que celle de `TargetClaimsExchangeId` Bonjour précédant la section
>   * Vérifiez `TechnicalProfileReferenceId` ID a la valeur toohello de profil technique vous avez créé plus haut (MSA OIDC).

## <a name="upload-hello-policy-tooyour-tenant"></a>Télécharger le client de tooyour stratégie hello
1.  Bonjour [portail Azure](https://portal.azure.com), basculez dans hello [contexte de votre locataire Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)et ouvrez hello **Azure AD B2C** panneau.
2.  Sélectionnez **Infrastructure d’expérience d’identité**.
3.  Ouvrez hello **toutes les stratégies** panneau.
4.  Sélectionnez **Charger la stratégie**.
5.  Vérifiez **remplacer la stratégie de hello si elle existe** boîte.
6.  **Télécharger** TrustFrameworkExtensions.xml et assurez-vous qu’il validation n’échoue pas hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Tester une stratégie personnalisée de hello à l’aide d’exécuter maintenant

1.  Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.
> [!NOTE]
>
>**Exécutez maintenant** requiert au moins une application toobe préinscrites sur le client de hello. toolearn tooregister applications, voir hello Azure AD B2C [prise en main](active-directory-b2c-get-started.md) article ou hello [inscription d’Application](active-directory-b2c-app-registration.md) l’article.
2.  Ouvrez **B2C_1A_signup_signin**, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé. Sélectionnez **Exécuter maintenant**.
3.  Vous devez être en mesure de toosign à l’aide du compte Microsoft.

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a>[Facultatif] Inscrire le parcours de hello Account Microsoft revendications fournisseur tooProfile-Modifier utilisateur
Vous pouvez souhaiter fournisseur d’identité Microsoft Account tooadd hello également tooyour utilisateur `ProfileEdit` parcours de l’utilisateur. toomake disponibles, nous Répétez hello a deux étapes :

### <a name="display-hello-button"></a>Bouton d’affichage hello
1.  Ouvrez le fichier d’extension hello de votre stratégie (par exemple, TrustFrameworkExtensions.xml).
2.  Recherche hello `<UserJourney>` nœud incluant `Id="ProfileEdit"` dans voyage utilisateur hello que vous avez copiée.
3.  Recherchez hello `<OrchestrationStep>` nœud qui inclut`Order="1"`
4.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Action de lien hello bouton tooan
1.  Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.
2.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Tester une stratégie de profil de modification personnalisée hello à l’aide d’exécuter maintenant
1.  Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.
2.  Ouvrez **B2C_1A_ProfileEdit**, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé. Sélectionnez **Exécuter maintenant**.
3.  Vous devez être en mesure de toosign à l’aide du compte Microsoft.

## <a name="download-hello-complete-policy-files"></a>Télécharger les fichiers de stratégie complète hello
Facultatif : Nous vous recommandons de que générer votre scénario à l’aide de vos propres fichiers de stratégie personnalisée hello prise en main des stratégies personnalisées guident au lieu d’utiliser ces exemples de fichiers à la fin.  [Exemples de fichiers de stratégie de référence](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
