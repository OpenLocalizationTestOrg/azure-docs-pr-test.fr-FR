---
title: "Azure Active Directory B2C : échanges de revendications de l’API REST en tant qu’étape d’orchestration | Microsoft Docs"
description: "Une rubrique sur les stratégies personnalisées d’Azure Active Directory B2C qui s’intègrent à une API"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure AD B2C comme étape d’orchestration

Hello identité expérience Framework (IEF) qui se trouve sous Azure Active Directory B2C (B2C Active Directory de Azure) permet de hello identité développeur toointegrate une interaction avec une API RESTful dans un parcours de l’utilisateur.  

À la fin de hello de cette procédure pas à pas, vous serez en mesure de toocreate un voyage utilisateur Azure AD B2C qui interagit avec les services RESTful.

Hello IEF envoie des données dans les demandes et reçoit des données dans les revendications. Hello exchange de revendications d’API REST :

- Peut être conçue comme une étape d’orchestration.
- Peut déclencher une action externe. Par exemple, elle peut enregistrer un événement dans une base de données externe.
- Peut être utilisé toofetch une valeur et puis le stocker dans la base de données utilisateur hello.

Vous pouvez utiliser les revendications hello a reçu des flux de hello toochange ultérieure d’exécution.

Vous pouvez également concevoir interaction hello tant que profil de validation. Pour plus d’informations, consultez [Intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure Active Directory B2C comme validation d’une entrée de l’utilisateur](active-directory-b2c-rest-api-validation-custom.md).

scénario de Hello est que lorsqu’un utilisateur effectue une modification de profil, nous voulons :

1. Rechercher hello utilisateur dans un système externe.
2. Obtenir la ville hello dans laquelle cet utilisateur est enregistré.
3. Retourner l’application toohello attribut comme une revendication.

## <a name="prerequisites"></a>Composants requis

- Un toocomplete de client configuré un compte de connexion-haut/connectez-vous, comme décrit dans Azure AD B2C [mise en route](active-directory-b2c-get-started-custom.md).
- Un toointeract de point de terminaison API REST avec. Cette procédure pas à pas utilise comme exemple un webhook d’application de fonction Azure simple.
- *Recommandé*: hello complète [API REST de procédure pas à pas d’exchange en tant qu’une étape de validation des revendications](active-directory-b2c-rest-api-validation-custom.md).

## <a name="step-1-prepare-hello-rest-api-function"></a>Étape 1 : Préparer la fonction d’API REST hello

> [!NOTE]
> Le programme d’installation de fonctions de l’API REST est en dehors de la portée de hello de cet article. [Les fonctions Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fournit un excellente toolkit toocreate des services RESTful dans le cloud de hello.

Nous avons mis en place une fonction Azure qui reçoit une demande de remboursement appelé `email`, et puis retourne hello revendication `city` avec la valeur hello affecté `Redmond`. l’exemple Hello fonction Azure se trouve sur [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

Hello `userMessage` revendication hello retours de fonction Azure est facultative dans ce contexte et hello IEF il sera ignoré. Vous pouvez éventuellement l’utiliser comme un message transmis toohello application et présentées toohello utilisateur plus tard.

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

Une application Azure fonction rend tooget facile hello fonction URL, ce qui peut inclure un identificateur de fonction spécifique de hello hello. Dans ce cas, les URL de hello est : https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==. Vous pouvez l’utiliser pour les tests.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>Étape 2 : Configurer exchange de revendications d’API RESTful hello comme profil technique dans votre fichier TrustFrameworExtensions.xml

Un profil de technique est la configuration complète de hello d’exchange hello souhaitée avec hello service RESTful. Ouvrir le fichier de TrustFrameworkExtensions.xml hello et ajouter hello suivant extrait XML à l’intérieur de hello `<ClaimsProvider>` élément.

> [!NOTE]
> Bonjour, XML, fournisseur RESTful suivant `Version=1.0.0.0` est décrite en tant que protocole de hello. Le considérer comme fonction hello qui interagit avec un service externe de hello. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Hello `<InputClaims>` élément définit les revendications hello qui seront envoyées à partir de hello service REST de toohello IEF. Dans cet exemple, hello le contenu de la revendication de hello `givenName` service REST de toohello sera envoyé en tant que revendication de hello `email`.  

Hello `<OutputClaims>` élément définit les revendications hello que hello IEF s’attend à partir du service REST hello. Quel que soit le nombre de hello de revendications qui sont reçus, hello IEF utilisera uniquement les identifié ici. Dans cet exemple, une revendication reçue en tant que `city` sera mappé tooan IEF revendication appelée `city`.

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>Étape 3 : Ajouter la nouvelle revendication d’hello `city` schéma toohello de votre fichier TrustFrameworkExtensions.xml

revendication de Hello `city` n’est pas encore défini n’importe où dans notre schéma. Par conséquent, ajoutez une définition dans un élément hello `<BuildingBlocks>`. Vous pouvez trouver cet élément au début de hello du fichier de TrustFrameworkExtensions.xml hello.

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>Étape 4 : Inclure hello REST service revendications exchange en tant qu’orchestration étape dans votre profil Modifier utilisateur du voyage dans TrustFrameworkExtensions.xml

Ajoutez une étape voyage utilisateur modifier toohello profil, une fois hello utilisateur a été authentifié (étapes d’orchestration 1-4 Bonjour XML suivant) et l’utilisateur de hello a fourni les informations de profil hello mis à jour (étape 5).

> [!NOTE]
> Il existe plusieurs cas d’usage où hello appel d’API REST peut être utilisé en tant qu’orchestration étape. En guise d’étape d’orchestration, il peut servir un système externe tooan de mise à jour après qu’un utilisateur a terminé une tâche comme première inscription ou tant que profil de mettre à jour les informations tookeep synchronisées. Dans ce cas, il est utilisé tooaugment hello informations toohello application une fois le profil de hello modifier.

Copier le profil hello Modifier code XML utilisateur voyage hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml fichier à l’intérieur de hello `<UserJourneys>` élément. Apportez la modification de hello sous l’étape 6.

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> Si l’ordre de hello ne correspond pas à votre version, assurez-vous que vous insérez le code de hello en tant qu’étape hello avant hello `ClaimsExchange` type `SendClaims`.

Hello XML final pour le voyage d’utilisateur hello doit ressembler à ceci :

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>Étape 5 : Ajouter des revendications de hello `city` stratégie tiers de la partie de confiance tooyour fichier afin de la revendication de hello est envoyée à tooyour application

Modifiez votre fichier tiers (RP) de la partie de confiance ProfileEdit.xml et hello `<TechnicalProfile Id="PolicyProfile">` suivant de hello élément tooadd : `<OutputClaim ClaimTypeReferenceId="city" />`.

Après avoir ajouté la nouvelle revendication de hello, profil de technique hello ressemble à ceci :

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a>Étape 6 : téléchargement et test de vos modifications

Remplacer les versions existantes de hello de stratégie de hello.

1.  (Facultatif :) Enregistrez version existante de hello (en le téléchargeant) de votre fichier extensions avant de continuer. tookeep hello initiale complexité faible, nous recommandons que vous ne téléchargez pas plusieurs versions du fichier des extensions hello.
2.  (Facultatif :) Renommer la nouvelle version de hello d’ID de stratégie hello pour modifier le fichier de stratégie hello en modifiant `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.
3.  Téléchargez le fichier des extensions hello.
4.  Téléchargez hello stratégie modifier RP le fichier.
5.  Utilisez **exécuter maintenant** stratégie de hello tootest. Jeton hello révision hello IEF retourne toohello application.

Si tout est configuré correctement, le jeton de hello inclura la nouvelle revendication d’hello `city`, avec la valeur de hello `Redmond`.

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Étapes suivantes

[Use a REST API as a validation step](active-directory-b2c-rest-api-validation-custom.md) (Utilisation d’une API REST comme une étape de validation)

[Modifier hello profil modifier toogather des informations supplémentaires à partir de vos utilisateurs](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
