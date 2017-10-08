---
title: "Azure Active Directory B2C : échanges de revendications de l’API REST en tant que validation | Microsoft Docs"
description: "Une rubrique sur les stratégies personnalisées Azure Active Directory B2C"
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
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure Active Directory B2C comme validation d’une entrée de l’utilisateur

Hello identité expérience Framework (IEF) qui se trouve sous Azure Active Directory B2C (B2C Active Directory de Azure) permet de hello identité développeur toointegrate une interaction avec une API RESTful dans un parcours de l’utilisateur.  

À la fin de hello de cette procédure pas à pas, vous serez en mesure de toocreate un voyage utilisateur Azure AD B2C qui interagit avec les services RESTful.

Hello IEF envoie des données dans les demandes et reçoit des données dans les revendications. interaction Hello avec hello API :

- Peut être conçue comme un échange de revendications de l’API REST ou comme un profil de validation, qui s’effectue dans une étape d’orchestration.
- En général, valide l’entrée d’utilisateur de hello. Si la valeur hello à partir de l’utilisateur de hello est rejetée, utilisateur de hello peut essayer de nouveau tooenter une valeur valide avec hello opportunité tooreturn un message d’erreur.

Vous pouvez également concevoir interaction hello en guise d’étape d’orchestration. Pour plus d’informations, consultez [Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure Active Directory B2C comme étape d’orchestration](active-directory-b2c-rest-api-step-custom.md).

Par exemple de profil de validation hello, nous allons utiliser voyage de hello profil Modifier utilisateur dans le fichier de pack de démarrage hello ProfileEdit.xml.

Nous pouvons vérifier ce nom hello fournie par l’utilisateur hello dans le profil de hello Edition n’est pas partie d’une liste d’exclusion.

## <a name="prerequisites"></a>Composants requis

- Un toocomplete de client configuré un compte de connexion-haut/connectez-vous, comme décrit dans Azure AD B2C [mise en route](active-directory-b2c-get-started-custom.md).
- Un toointeract de point de terminaison API REST avec. Pour cette procédure pas à pas, nous avons configuré un site de démonstration appelé [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) avec un service de l’API REST.

## <a name="step-1-prepare-hello-rest-api-function"></a>Étape 1 : Préparer la fonction d’API REST hello

> [!NOTE]
> Le programme d’installation de fonctions de l’API REST est en dehors de la portée de hello de cet article. [Les fonctions Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fournit un excellente toolkit toocreate des services RESTful dans le cloud de hello.

Nous avons créé une fonction Azure qui reçoit une revendication qu’elle attend en tant que `playerTag`. fonction Hello valide qui indique si cette revendication. Vous pouvez accéder à code de fonction Azure complète hello dans [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

Hello IEF attend hello `userMessage` cette fonction Azure hello retourne de la revendication. Cette demande s’affiche en tant qu’un utilisateur toohello de chaîne si la validation de hello échoue, par exemple quand il est retourné un état de 409 conflit Bonjour précédent exemple.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>Étape 2 : Configurer exchange de revendications d’API RESTful hello comme profil technique dans votre fichier TrustFrameworkExtensions.xml

Un profil de technique est la configuration complète de hello d’exchange hello souhaitée avec hello service RESTful. Ouvrir le fichier de TrustFrameworkExtensions.xml hello et ajouter hello suivant extrait XML à l’intérieur de hello `<ClaimsProviders>` élément.

> [!NOTE]
> Bonjour, XML, fournisseur RESTful suivant `Version=1.0.0.0` est décrite en tant que protocole de hello. Le considérer comme fonction hello qui interagit avec un service externe de hello. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Hello `InputClaims` élément définit les revendications hello qui seront envoyées à partir de hello service REST de toohello IEF. Dans cet exemple, hello le contenu de la revendication de hello `givenName` sera envoyé service REST de toohello comme `playerTag`. Dans cet exemple, hello QU'IEF n’attend pas de revendications précédent. Au lieu de cela, il attend une réponse de service REST de hello et agit selon les codes d’état hello qu’il reçoit.

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>Étape 3 : Inclure hello service RESTful revendications exchange dans automatique déclarée profil technique où vous souhaitez toovalidate hello l’entrée d’utilisateur

utilisation la plus courante de l’étape de validation hello Hello est dans une interaction de hello avec un utilisateur. Toutes les interactions où les utilisateurs hello sont tooprovide attendu d’entrée sont *automatique déclarée profils techniques*. Pour cet exemple, nous allons ajouter profil technique du libre-service Asserted-ProfileUpdate toohello validation hello. Il s’agit profil technique hello hello du fichier de stratégie de confiance partie de confiance `Profile Edit` utilise.

tooadd hello revendications exchange toohello automatique déclarée profil technique :

1. Ouvrez le fichier TrustFrameworkBase.xml de hello et recherchez `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.
2. Passez en revue la configuration hello de ce profil technique. Observez comment exchange hello avec l’utilisateur de hello est défini en tant que revendications qui seront demandées de l’utilisateur hello (revendications d’entrée) et qui sera attendu de fournisseur de hello automatique déclarée (revendications de sortie).
3. Recherchez `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`. Notez que ce profil est appelé au titre de l’étape d’orchestration 6 de `<UserJourney Id="ProfileEdit">`.

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>Étape 4 : Télécharger et d’un fichier de stratégie de hello profil modifier RP test

1. Téléchargez hello une nouvelle version du fichier de TrustFrameworkExtensions.xml hello.
2. Utilisez **exécuter maintenant** profil de hello tootest modifier le fichier de stratégie RP.
3. Test de validation de hello en fournissant un des noms de hello existant (par exemple, mcvinny) Bonjour **prénom** champ. Si tout est configuré correctement, vous devez recevoir un message qui avertit les utilisateurs hello que hello lecteur balise est déjà utilisée.

## <a name="next-steps"></a>Étapes suivantes

[Modifier hello profil utilisateur et modifier l’inscription toogather des informations supplémentaires à partir de vos utilisateurs](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure AD B2C comme étape d’orchestration](active-directory-b2c-rest-api-step-custom.md)
