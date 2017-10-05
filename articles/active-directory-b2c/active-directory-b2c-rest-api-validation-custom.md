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
ms.openlocfilehash: eb44a0d2234c9ee3801d8b3a1655d877aa2f4fef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="360a3-103">Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure Active Directory B2C comme validation d’une entrée de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="360a3-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="360a3-104">L’infrastructure d’expérience d’identité sur laquelle repose Azure Active Directory B2C (Azure AD B2C) permet au développeur d’identité d’intégrer une interaction avec une API RESTful dans un parcours utilisateur.</span><span class="sxs-lookup"><span data-stu-id="360a3-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="360a3-105">À la fin de cette procédure pas à pas, vous pourrez créer un parcours utilisateur Azure AD B2C qui interagit avec les services RESTful.</span><span class="sxs-lookup"><span data-stu-id="360a3-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="360a3-106">L’IEF envoie des données dans des revendications et reçoit en retour des données via des revendications.</span><span class="sxs-lookup"><span data-stu-id="360a3-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="360a3-107">L’interaction avec l’API :</span><span class="sxs-lookup"><span data-stu-id="360a3-107">The interaction with the API:</span></span>

- <span data-ttu-id="360a3-108">Peut être conçue comme un échange de revendications de l’API REST ou comme un profil de validation, qui s’effectue dans une étape d’orchestration.</span><span class="sxs-lookup"><span data-stu-id="360a3-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="360a3-109">Valide en général une entrée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="360a3-109">Typically validates input from the user.</span></span> <span data-ttu-id="360a3-110">Si la valeur de l’utilisateur est rejetée, il peut essayer à nouveau d’entrer une valeur valide, avec la possibilité de retourner un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="360a3-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="360a3-111">Vous pouvez aussi concevoir l’interaction comme une étape d’orchestration.</span><span class="sxs-lookup"><span data-stu-id="360a3-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="360a3-112">Pour plus d’informations, consultez [Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure Active Directory B2C comme étape d’orchestration](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="360a3-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="360a3-113">Pour l’exemple de profil de validation, nous allons utiliser le parcours utilisateur de modification de profil dans le fichier ProfileEdit.xml du pack de démarrage.</span><span class="sxs-lookup"><span data-stu-id="360a3-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="360a3-114">Nous pouvons vérifier que le nom fourni par l’utilisateur dans la modification de profil ne figure sur aucune liste d’exclusions.</span><span class="sxs-lookup"><span data-stu-id="360a3-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="360a3-115">Prérequis</span><span class="sxs-lookup"><span data-stu-id="360a3-115">Prerequisites</span></span>

- <span data-ttu-id="360a3-116">Un locataire Azure AD B2C configuré pour effectuer une inscription/connexion à un compte local, comme décrit dans [Bien démarrer](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="360a3-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="360a3-117">Un point de terminaison API REST avec lequel vous allez interargir.</span><span class="sxs-lookup"><span data-stu-id="360a3-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="360a3-118">Pour cette procédure pas à pas, nous avons configuré un site de démonstration appelé [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) avec un service de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="360a3-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="360a3-119">Étape 1 : préparation de la fonction de l’API REST</span><span class="sxs-lookup"><span data-stu-id="360a3-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="360a3-120">Cet article ne traite pas de la configuration des fonctions de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="360a3-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="360a3-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) fournit un excellent kit de ressources pour la création de services RESTful dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="360a3-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="360a3-122">Nous avons créé une fonction Azure qui reçoit une revendication qu’elle attend en tant que `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="360a3-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="360a3-123">La fonction vérifie si cette revendication existe.</span><span class="sxs-lookup"><span data-stu-id="360a3-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="360a3-124">Vous pouvez accéder au code complet de la fonction Azure dans [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="360a3-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="360a3-125">L’infrastructure d’expérience d’identité attend la revendication `userMessage` retournée par la fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="360a3-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="360a3-126">Cette revendication est présentée sous forme de chaîne à l’utilisateur si la validation échoue, comme quand un état de conflit 409 est retourné dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="360a3-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="360a3-127">Étape 2 : configuration de l’échange de revendications de l’API RESTful comme profil technique dans votre fichier TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="360a3-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="360a3-128">Le profil technique est la configuration complète de l’échange souhaité avec le service RESTful.</span><span class="sxs-lookup"><span data-stu-id="360a3-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="360a3-129">Ouvrez le fichier TrustFrameworkExtensions.xml et ajoutez l’extrait de code XML suivant à l’intérieur de l’élément `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="360a3-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="360a3-130">Dans le code XML suivant, le fournisseur RESTful `Version=1.0.0.0` est décrit comme étant le protocole.</span><span class="sxs-lookup"><span data-stu-id="360a3-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="360a3-131">Considérez-le comme étant la fonction qui interagit avec le service externe.</span><span class="sxs-lookup"><span data-stu-id="360a3-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="360a3-132">L’élément `InputClaims` définit les revendications qui seront envoyées depuis l’IEF vers le service REST.</span><span class="sxs-lookup"><span data-stu-id="360a3-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="360a3-133">Dans cet exemple, le contenu de la revendication `givenName` sera envoyé au service REST en tant que `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="360a3-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="360a3-134">Dans cet exemple, l’infrastructure d’expérience d’identité n’attend pas de revendications en retour.</span><span class="sxs-lookup"><span data-stu-id="360a3-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="360a3-135">Au lieu de cela, elle attend une réponse du service REST et agit en fonction des codes d’état qu’elle reçoit.</span><span class="sxs-lookup"><span data-stu-id="360a3-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="360a3-136">Étape 3 : intégration de l’échange de revendications du service RESTful dans le profil technique autodéclaré où vous voulez valider la saisie de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="360a3-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="360a3-137">L’étape de validation est le plus souvent utilisée dans le cadre d’une interaction avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="360a3-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="360a3-138">Toutes les interactions où une saisie de l’utilisateur est attendue sont des *profils techniques autodéclarés*.</span><span class="sxs-lookup"><span data-stu-id="360a3-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="360a3-139">Pour cet exemple, nous ajoutons la validation au profil technique Self-Asserted-ProfileUpdate.</span><span class="sxs-lookup"><span data-stu-id="360a3-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="360a3-140">Il s’agit du profil technique utilisé par le fichier de stratégie de la partie de confiance `Profile Edit`.</span><span class="sxs-lookup"><span data-stu-id="360a3-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="360a3-141">Pour ajouter l’échange de revendications au profil technique autodéclaré :</span><span class="sxs-lookup"><span data-stu-id="360a3-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="360a3-142">Ouvrez le fichier TrustFrameworkBase.xml et recherchez `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="360a3-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="360a3-143">Passez en revue la configuration de ce profil technique.</span><span class="sxs-lookup"><span data-stu-id="360a3-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="360a3-144">Notez comment l’échange avec l’utilisateur est défini sous la forme de revendications demandées à l’utilisateur (revendications d’entrée) et de revendications attendues en retour par le fournisseur autodéclaré (revendications de sortie).</span><span class="sxs-lookup"><span data-stu-id="360a3-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="360a3-145">Recherchez `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`. Notez que ce profil est appelé au titre de l’étape d’orchestration 6 de `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="360a3-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="360a3-146">Étape 4 : téléchargement et test du fichier de stratégie de partie de confiance de modification de profil</span><span class="sxs-lookup"><span data-stu-id="360a3-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="360a3-147">Chargez la nouvelle version du fichier TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="360a3-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="360a3-148">Sélectionnez **Exécuter maintenant** pour tester le fichier de stratégie de partie de confiance Modification de profil.</span><span class="sxs-lookup"><span data-stu-id="360a3-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="360a3-149">Testez la validation en fournissant un des noms existants (par exemple mcvinny) dans le champ **Prénom**.</span><span class="sxs-lookup"><span data-stu-id="360a3-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="360a3-150">Si tout est correctement configuré, vous devez normalement recevoir un message indiquant à l’utilisateur que l’étiquette player est déjà utilisée.</span><span class="sxs-lookup"><span data-stu-id="360a3-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="360a3-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="360a3-151">Next steps</span></span>

[<span data-ttu-id="360a3-152">Changer la modification de profil et l’inscription des utilisateurs pour collecter des informations supplémentaires auprès de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="360a3-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="360a3-153">Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure AD B2C comme étape d’orchestration</span><span class="sxs-lookup"><span data-stu-id="360a3-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
