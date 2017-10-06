---
title: "Azure Active Directory B2C : Ajout de Google+ en tant que fournisseur d’identités OAuth2 à l’aide de stratégies personnalisées"
description: "Exemple d’utilisation de Google+ en tant que fournisseur d’identité à l’aide du protocole OAuth2"
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
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a>Azure Active Directory B2C : Ajout de Google+ en tant que fournisseur d’identités OAuth2 à l’aide de stratégies personnalisées

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Ce guide vous explique comment tooenable connectez-vous pour les utilisateurs à partir de Google + compte via l’utilisation de hello de [des stratégies personnalisées](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Composants requis

Hello terminé les étapes Bonjour [mise en route avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md) l’article.

Ces étapes sont les suivantes :

1.  Création d’une application de compte Google+.
2.  Ajout de hello Google + compte application clé tooAzure AD B2C
3.  Ajout d’une stratégie de tooa de fournisseur de revendications
4.  L’inscription hello Google + compte revendications fournisseur tooa utilisateur voyage
5.  Téléchargement de stratégie de hello tooan Azure AD B2C de client et de le tester

## <a name="create-a-google-account-application"></a>Création d’une application de compte Google+
toouse + Google comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Google + et lui fournir les paramètres appropriés hello. Vous pouvez inscrire une application Google+ ici : [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)

1.  Accédez toohello [Console des développeurs Google](https://console.developers.google.com/) et connectez-vous avec vos informations d’identification compte Google +.
2.  Cliquez sur **Créer un projet**, saisissez un **nom de projet**, puis cliquez sur **Créer**.

3.  Cliquez sur hello **menu projets**.

    ![Compte Google+ - Sélectionner le projet](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  Cliquez sur hello  **+**  bouton.

    ![Compte Google+ - Créer un nouveau projet](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  Entrez un **Nom de projet**, puis cliquez sur **Créer**.

    ![Compte Google+ : Nouveau projet](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  Attendez que le projet de hello est prêt, cliquez sur hello **menu projets**.

    ![Compte Google + - en attente jusqu'à ce que le nouveau projet est prêt toouse](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  Cliquez sur le nom de votre projet.

    ![Compte Google + - projet hello Select](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  Cliquez sur **API Manager** puis cliquez sur **informations d’identification** Bonjour barre de navigation gauche.
9.  Cliquez sur hello **écran de consentement OAuth** onglet en haut de hello.

    ![Compte Google+ - Définition de l’écran de consentement OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  Sélectionnez ou spécifiez une valeur valide pour **Adresse de messagerie**, fournissez une valeur pour **Nom de produit**, puis cliquez sur **Enregistrer**.

    ![Google+ - Informations d’identification de l’application](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  Cliquez sur **Nouvelles informations d’identification**, puis sur **ID client OAuth**.

    ![Google+ - Créer de nouvelles informations d’identification d’application](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  Sous **Type d’application**, sélectionnez **Application web**.

    ![Google+ - Sélectionner un type d’application](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  Fournir un **nom** pour votre application, entrez `https://login.microsoftonline.com` Bonjour **autorisé de JavaScript origines** champ, et `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **autorisés rediriger URI**champ. Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com). Hello **{tenant}** valeur respecte la casse. Cliquez sur **Créer**.

    ![Google+ - Fournir les origines autorisées de JavaScript et les URI de redirection](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  Copier les valeurs hello de **Id Client** et **clé secrète Client**. Vous devez les deux tooconfigure Google + comme fournisseur d’identité dans votre client. **Client secret** est une information d’identification de sécurité importante.

    ![Google + - valeurs hello de copie de la clé secrète du Client et Id de client](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a>Ajouter hello Google + compte application clé tooAzure AD B2C
Fédération avec Google + comptes requiert une clé secrète client pour Google + compte tootrust Azure AD B2C au nom de l’application hello. Vous devez toostore votre secret d’application Google + dans Azure AD B2C client :  

1.  Accédez tooyour Azure AD B2C client, puis sélectionnez **B2C paramètres** > **infrastructure expérience d’identité**
2.  Sélectionnez **clés de stratégie** tooview hello disponibles dans votre client.
3.  Cliquez sur **+Ajouter**.
4.  Pour **Options**, utilisez **Manuel**.
5.  Pour **Nom**, utilisez `GoogleSecret`.  
    préfixe de Hello `B2C_1A_` peuvent être ajoutées automatiquement.
6.  Bonjour **Secret** , entrez votre clé secrète d’application Microsoft à partir de https://apps.dev.microsoft.com
7.  Pour **Utilisation de la clé**, utilisez **Signature**.
8.  Cliquez sur **Créer**
9.  Vérifiez que vous avez créé la clé de hello `B2C_1A_GoogleSecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Ajouter un fournisseur de revendications à une stratégie d’extension

Si vous souhaitez que les utilisateurs toosign à l’aide du compte Google +, vous devez toodefine Google + compte comme un fournisseur de revendications. En d’autres termes, vous devez toospecify un point de terminaison Azure AD B2C communique avec. point de terminaison Hello fournit un ensemble de revendications qui sont utilisées par Azure AD B2C tooverify authentifié un utilisateur spécifique.

Définissez le compte Google+ comme fournisseur de revendications, en ajoutant le nœud `<ClaimsProvider>` dans votre fichier de stratégie d’extension :

1.  Ouvrez le fichier de stratégie d’extension hello (TrustFrameworkExtensions.xml) à partir de votre répertoire de travail. Si vous avez besoin d’un éditeur XML, [essayez Visual Studio Code](https://code.visualstudio.com/download), un éditeur multiplateforme léger.
2.  Recherche hello `<ClaimsProviders>` section
3.  Ajouter hello suivant extrait de code XML sous hello `ClaimsProviders` élément et remplacer `client_id` valeur avec votre ID de client application compte Google + avant d’enregistrer le fichier de hello.  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Inscrire hello Google + compte revendications fournisseur tooSign des ou connectez-vous de parcours de l’utilisateur

fournisseur d’identité Hello a été configuré.  Toutefois, il n’est pas disponible dans les écrans de connexion-haut/connectez-vous hello. Ajouter hello Google + compte fournisseur tooyour utilisateur de l’identité `SignUpOrSignIn` parcours de l’utilisateur. toomake il est disponible, nous créons un doublon d’un déplacement de modèle à l’utilisateur existant.  Puis nous ajouter hello Google + fournisseur d’identité du compte :

>[!NOTE]
>
>Si vous avez copié hello `<UserJourneys>` élément à partir du fichier de base de votre fichier d’extension de stratégie toohello (TrustFrameworkExtensions.xml), vous pouvez ignorer toothis section.

1.  Ouvrez le fichier de base hello de votre stratégie (par exemple, TrustFrameworkBase.xml).
2.  Recherche hello `<UserJourneys>` élément et copie hello ensemble du contenu de `<UserJourneys>` nœud.
3.  Ouvrez le fichier d’extension hello (par exemple, TrustFrameworkExtensions.xml) et recherche hello `<UserJourneys>` élément. Si l’élément de hello n’existe pas, ajoutez-en un.
4.  Coller le contenu entier de hello de `<UserJournesy>` nœud que vous avez copié en tant qu’enfant de hello `<UserJourneys>` élément.

### <a name="display-hello-button"></a>Bouton d’affichage hello
Hello `<ClaimsProviderSelections>` élément définit la liste hello des options de sélection de fournisseur de revendications et leur ordre.  `<ClaimsProviderSelection>`élément est un bouton de fournisseur d’identité tooan analogue sur une connexion-haut/page de connexion. Si vous ajoutez un `<ClaimsProviderSelection>` élément compte Google +, un nouveau bouton apparaît lorsqu’un utilisateur arrive sur la page de hello. tooadd cet élément :

1.  Recherche hello `<UserJourney>` nœud incluant `Id="SignUpOrSignIn"` dans voyage utilisateur hello que vous avez copiée.
2.  Recherchez hello `<OrchestrationStep>` nœud qui inclut`Order="1"`
3.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Action de lien hello bouton tooan
Maintenant que vous avez un bouton en place, vous devez toolink il tooan action. action de Hello, dans ce cas, est de toocommunicate Azure AD B2C avec Google + compte tooreceive un jeton.

1.  Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.
2.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * Assurez-vous de hello `Id` a hello même valeur que celle de `TargetClaimsExchangeId` Bonjour précédant la section
> * Vérifiez `TechnicalProfileReferenceId` ID a la valeur toohello de profil technique vous avez créé plus haut (Google OAUTH).

## <a name="upload-hello-policy-tooyour-tenant"></a>Télécharger le client de tooyour stratégie hello
1.  Bonjour [portail Azure](https://portal.azure.com), basculez dans hello [contexte de votre locataire Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)et ouvrez hello **Azure AD B2C** panneau.
2.  Sélectionnez **Infrastructure d’expérience d’identité**.
3.  Ouvrez hello **toutes les stratégies** panneau.
4.  Sélectionnez **Charger la stratégie**.
5.  Vérifiez **remplacer la stratégie de hello si elle existe** boîte.
6.  **Télécharger** TrustFrameworkExtensions.xml et assurez-vous qu’il validation n’échoue pas hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Tester une stratégie personnalisée de hello à l’aide d’exécuter maintenant
1.  Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.

    >[!NOTE]
    >
    >    **Exécutez maintenant** requiert au moins une application toobe préinscrites sur le client de hello. 
    >    toolearn tooregister applications, voir hello Azure AD B2C [prise en main](active-directory-b2c-get-started.md) article ou hello [inscription d’Application](active-directory-b2c-app-registration.md) l’article.


2.  Ouvrez **B2C_1A_signup_signin**, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé. Sélectionnez **Exécuter maintenant**.
3.  Vous devez être en mesure de toosign à l’aide du compte Google +.

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a>[Facultatif] Inscrire hello Google + compte revendications fournisseur tooProfile-Modifier utilisateur voyage
Vous pouvez souhaiter tooadd hello Google + compte fournisseur d’identité également tooyour utilisateur `ProfileEdit` parcours de l’utilisateur. toomake disponibles, nous Répétez hello a deux étapes :

### <a name="display-hello-button"></a>Bouton d’affichage hello
1.  Ouvrez le fichier d’extension hello de votre stratégie (par exemple, TrustFrameworkExtensions.xml).
2.  Recherche hello `<UserJourney>` nœud incluant `Id="ProfileEdit"` dans voyage utilisateur hello que vous avez copiée.
3.  Recherchez hello `<OrchestrationStep>` nœud qui inclut`Order="1"`
4.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Action de lien hello bouton tooan
1.  Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.
2.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Tester une stratégie de profil de modification personnalisée hello à l’aide d’exécuter maintenant

1.  Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.
2.  Ouvrez **B2C_1A_ProfileEdit**, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé. Sélectionnez **Exécuter maintenant**.
3.  Vous devez être en mesure de toosign à l’aide du compte Google +.

## <a name="download-hello-complete-policy-files"></a>Télécharger les fichiers de stratégie complète hello
Facultatif : Nous vous recommandons de que générer votre scénario à l’aide de vos propres fichiers de stratégie personnalisée hello prise en main des stratégies personnalisées guident au lieu d’utiliser ces exemples de fichiers à la fin.  [Exemples de fichiers de stratégie de référence](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
