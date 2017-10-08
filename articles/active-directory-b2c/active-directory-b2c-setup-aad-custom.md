---
title: "Azure Active Directory B2C : Ajouter un fournisseur Azure AD à l’aide de stratégies personnalisées | Microsoft Docs"
description: "Découvrir les stratégies personnalisées Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a>Azure Active Directory B2C : se connecter à l’aide de comptes Azure AD

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Cet article vous explique comment tooenable connectez-vous pour les utilisateurs à partir d’une organisation Azure Active Directory (Azure AD) spécifique à l’aide de hello de [des stratégies personnalisées](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Composants requis

Hello terminé les étapes Bonjour [mise en route avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md) l’article.

Ces étapes sont les suivantes :

1. Création d’un locataire Azure Active Directory B2C (Azure AD B2C).
2. Création d’une application Azure AD B2C.
3. Inscription de deux applications de moteur de stratégie.
4. Configuration des clés.
5. Configuration d’un pack de démarrage hello.

## <a name="create-an-azure-ad-app"></a>Création d’une application Azure AD

tooenable connectez-vous pour les utilisateurs spécifiques à une organisation Azure AD, vous devez tooregister une application au sein de client de hello d’organisation Azure AD.

>[!NOTE]
> Nous utilisons « contoso.com » pour le locataire de hello d’organisation Azure AD et « fabrikamb2c.onmicrosoft.com » en tant que client hello Azure AD B2C Bonjour suivant les instructions.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
1. Dans la barre supérieure de hello, sélectionnez votre compte. À partir de hello **répertoire** , choisissez locataire hello d’organisation Azure AD où vous souhaitez tooregister votre application (contoso.com).
1. Sélectionnez **davantage de services** dans le volet gauche de hello et recherchez « Inscriptions d’application ».
1. Sélectionnez **Nouvelle inscription d’application**.
1. Entrez un nom pour votre application (par exemple, `Azure AD B2C App`).
1. Sélectionnez **application Web / API** hello pour type d’application.
1. Pour **URL de connexion**, entrez hello suivant URL, où `yourtenant` remplacé par le nom de votre client Azure AD B2C hello (`fabrikamb2c.onmicrosoft.com`) :

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. Enregistrer l’ID d’application hello.
1. Sélectionnez l’application hello nouvellement créé.
1. Sous hello **paramètres** panneau, sélectionnez **clés**.
1. Créez une clé et enregistrez-la. Vous allez l’utiliser dans les étapes de hello dans la section suivante de hello.

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a>Ajouter tooAzure de clé hello AD Azure AD B2C

Vous avez besoin de clé d’application toostore hello contoso.com dans votre locataire Azure AD B2C. toodo cela :
1. Accédez tooyour Azure AD B2C client, puis sélectionnez **B2C paramètres** > **infrastructure d’identité expérience** > **clés de stratégie**.
1. Sélectionnez **+Ajouter**.
1. Sélectionnez ou entrez les options suivantes :
   * Sélectionnez **Manuel**.
   * Pour **Nom**, choisissez un nom correspondant au nom de votre locataire Azure AD (par exemple, `ContosoAppSecret`).  préfixe de Hello `B2C_1A_` est ajouté automatiquement nom toohello de votre clé.
   * Collez votre clé d’application Bonjour **Secret** boîte.
   * Sélectionnez **Signature**.
1. Sélectionnez **Créer**.
1. Vérifiez que vous avez créé la clé de hello `B2C_1A_ContosoAppSecret`.


## <a name="add-a-claims-provider-in-your-base-policy"></a>Ajoutez un fournisseur de revendications dans votre stratégie de base

Si vous souhaitez que les utilisateurs toosign à l’aide d’Azure AD, vous devez toodefine Azure AD comme fournisseur de revendications. En d’autres termes, vous devez toospecify un point de terminaison communique avec Azure Active Directory B2C. point de terminaison Hello fournissent un ensemble de revendications qui sont utilisés par Azure AD B2C tooverify authentifié un utilisateur spécifique. 

Vous pouvez définir Azure AD comme fournisseur de revendications en ajoutant Azure AD toohello `<ClaimsProvider>` nœud dans le fichier d’extension hello de votre stratégie :

1. Ouvrez le fichier d’extension hello (TrustFrameworkExtensions.xml) à partir de votre répertoire de travail.
1. Recherche hello `<ClaimsProviders>` section. Si elle n’existe pas, l’ajouter sous le nœud racine de hello.
1. Ajoutez un nœud `<ClaimsProvider>` comme suit :

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
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

1. Sous hello `<ClaimsProvider>` nœud, la valeur hello de mise à jour pour `<Domain>` tooa valeur unique qui peut être utilisé toodistinguish à partir d’autres fournisseurs d’identité.
1. Sous hello `<ClaimsProvider>` nœud, la valeur hello de mise à jour pour `<DisplayName>` fournisseur de revendications de nom convivial tooa hello. Cette valeur n’est pas utilisée actuellement.

### <a name="update-hello-technical-profile"></a>Mettre à jour le profil de technique hello

tooget un jeton à partir du point de terminaison hello Azure AD, vous devez les protocoles de hello toodefine que Azure AD B2C doit utiliser toocommunicate avec Azure AD. Cette opération est effectuée à l’intérieur de hello `<TechnicalProfile>` élément de `<ClaimsProvider>`.
1. Mise à jour ID hello Hello `<TechnicalProfile>` nœud. Cet ID est utilisé toorefer toothis profil technique à partir d’autres parties de la stratégie de hello.
1. Mettre à jour la valeur hello pour `<DisplayName>`. Cette valeur s’affichera sur le bouton hello de connexion sur votre écran de connexion.
1. Mettre à jour la valeur hello pour `<Description>`.
1. Azure AD utilise le protocole OpenID Connect de hello, assurez-vous que valeur hello pour `<Protocol>` est `"OpenIdConnect"`.

Vous devez tooupdate hello `<Metadata>` section dans le fichier XML de hello référencé des paramètres de configuration tooearlier tooreflect hello pour spécifique à votre client Azure AD. Dans le fichier XML de hello, mettre à jour les valeurs de métadonnées hello comme suit :

1. Définissez `<Item Key="METADATA">` trop`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, où `yourAzureADtenant` est votre nom de client Azure AD (contoso.com).
1. Ouvrez votre toohello navigateur et allez `METADATA` URL que vous venez de mettre à jour.
1. Dans le navigateur de hello, recherche d’objet 'd’attribut issuer' hello et copiez sa valeur. Il doit ressembler à hello suivant : `https://sts.windows.net/{tenantId}/`.
1. Collez la valeur hello pour `<Item Key="ProviderName">` dans le fichier XML de hello.
1. Définissez `<Item Key="client_id">` toohello ID de l’application à partir de l’inscription d’une application hello.
1. Définissez `<Item Key="IdTokenAudience">` toohello ID de l’application à partir de l’inscription d’une application hello.
1. Vérifiez que `<Item Key="response_types">` est défini trop`id_token`.
1. Vérifiez que `<Item Key="UsePolicyInRedirectUri">` est défini trop`false`.

Vous devez également le code secret toolink hello Azure AD que vous avez enregistré dans votre toohello de locataire Azure AD B2C Azure AD `<ClaimsProvider>` informations :

* Bonjour `<CryptographicKeys>` section Bonjour précédant le fichier XML, mettre à jour la valeur hello pour `StorageReferenceId` toohello ID de référence de clé secrète hello que vous avez définie (par exemple, `ContosoAppSecret`).

### <a name="upload-hello-extension-file-for-verification"></a>Télécharger le fichier d’extension hello pour la vérification

À ce stade, vous avez configuré votre stratégie afin que Azure AD B2C sait comment toocommunicate avec votre annuaire Azure AD. Essayez de télécharger le fichier d’extension hello de votre tooconfirm simplement stratégie qu’il ne possède pas les problèmes de jusqu'à présent. toodo pour :

1. Ouvrez hello **toutes les stratégies** panneau dans votre locataire Azure AD B2C.
1. Vérifiez hello **remplacer la stratégie de hello si elle existe** boîte.
1. Télécharger le fichier d’extension hello (TrustFrameworkExtensions.xml) et assurez-vous qu’il validation n’échoue pas hello.

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a>Inscrire le parcours de hello Azure AD revendications fournisseur tooa utilisateur

Vous devez maintenant tooadd hello Azure AD identity fournisseur tooone de votre parcours de l’utilisateur. À ce stade, le fournisseur d’identité hello a été configuré, mais il n’est pas disponible dans les écrans de connexion-haut/connectez-vous hello. toomake il est disponible, nous crée un doublon d’un déplacement de modèle à l’utilisateur existant et modifiez-le afin qu’il puisse également le fournisseur d’identité hello Azure AD :

1. Ouvrez le fichier de base hello de votre stratégie (par exemple, TrustFrameworkBase.xml).
1. Recherche hello `<UserJourneys>` hello élément et copie entière `<UserJourney>` nœud inclut `Id="SignUpOrSignIn"`.
1. Ouvrez le fichier d’extension hello (par exemple, TrustFrameworkExtensions.xml) et recherche hello `<UserJourneys>` élément. Si l’élément de hello n’existe pas, ajoutez-en un.
1. Hello coller entière `<UserJourney>` nœud que vous avez copié en tant qu’enfant de hello `<UserJourneys>` élément.
1. Renommer des ID hello de parcours d’utilisateur nouveau hello (par exemple, renommer en tant que `SignUpOrSignUsingContoso`).

### <a name="display-hello-button"></a>Hello d’affichage « bouton »

Hello `<ClaimsProviderSelection>` élément est le bouton de fournisseur d’identité tooan analogue sur un connexion-haut/écran de connexion. Si vous ajoutez un `<ClaimsProviderSelection>` élément pour Azure AD, un nouveau bouton apparaît lorsqu’un utilisateur arrive sur la page de hello. tooadd cet élément :

1. Recherche hello `<OrchestrationStep>` nœud incluant `Order="1"` dans voyage utilisateur hello que vous venez de créer.
1. Ajoutez hello qui suit :

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. Définissez `TargetClaimsExchangeId` tooan les valeur appropriée. Nous vous recommandons de suivant hello même convention que d’autres :  *\[ClaimProviderName\]Exchange*.

### <a name="link-hello-button-tooan-action"></a>Action de lien hello bouton tooan

Maintenant que vous avez un bouton en place, vous devez toolink il tooan action. action de Hello, dans ce cas, est de toocommunicate Azure AD B2C avec Azure AD tooreceive un jeton. Action de tooan bouton lien hello en liant le profil de technique hello pour votre fournisseur de revendications d’Azure AD :

1. Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.
1. Ajoutez hello qui suit :

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. Mise à jour `Id` toohello même valeur que celle de `TargetClaimsExchangeId` Bonjour précédant la section.
1. Mise à jour `TechnicalProfileReferenceId` ID toohello Hello technique du profil que vous avez créé précédemment (ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Télécharger le fichier d’extension de mise à jour de hello

Vous avez terminé la modification d’extension hello. Enregistrez-le. Puis téléchargez le fichier de hello et assurez-vous que toutes les validations réussissent.

### <a name="update-hello-rp-file"></a>Fichier de mise à jour hello RP

Vous devez maintenant tooupdate hello partie de confiance (RP) de tiers fichier qui exécutera voyage utilisateur hello que vous venez de créer :

1. Faites une copie de SignUpOrSignIn.xml dans votre répertoire de travail et renommez-le (par exemple, renommer tooSignUpOrSignInWithAAD.xml).
1. Hello de fichier et de mise à jour de nouveau hello ouvrir `PolicyId` attribut `<TrustFrameworkPolicy>` avec une valeur unique (par exemple, SignUpOrSignInWithAAD). <br> Ce sera le nom hello de votre stratégie (par exemple, B2C\_1 a\_SignUpOrSignInWithAAD).
1. Modifier hello `ReferenceId` attribut `<DefaultUserJourney>` ID de hello toomatch nouveau voyage utilisateur hello, que vous avez créé (SignUpOrSignUsingContoso).
1. Enregistrer vos modifications et téléchargez le fichier de hello.

## <a name="troubleshooting"></a>Résolution des problèmes

Tester une stratégie personnalisée hello que vous venez de télécharger en cliquant sur son panneau **exécuter maintenant**. problèmes de toodiagnose, en savoir plus sur [dépannage](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Étapes suivantes

Fournir des commentaires trop[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
