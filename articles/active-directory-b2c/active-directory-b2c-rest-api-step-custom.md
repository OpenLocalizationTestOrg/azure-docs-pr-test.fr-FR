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
ms.openlocfilehash: dc319c97e64e55861b84cc3943667418077a05d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="9eade-103">Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure AD B2C comme étape d’orchestration</span><span class="sxs-lookup"><span data-stu-id="9eade-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="9eade-104">L’infrastructure d’expérience d’identité sur laquelle repose Azure Active Directory B2C (Azure AD B2C) permet au développeur d’identité d’intégrer une interaction avec une API RESTful dans un parcours utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9eade-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="9eade-105">À la fin de cette procédure pas à pas, vous pourrez créer un parcours utilisateur Azure AD B2C qui interagit avec les services RESTful.</span><span class="sxs-lookup"><span data-stu-id="9eade-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="9eade-106">L’IEF envoie des données dans des revendications et reçoit en retour des données via des revendications.</span><span class="sxs-lookup"><span data-stu-id="9eade-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="9eade-107">L’échange de revendications de l’API REST :</span><span class="sxs-lookup"><span data-stu-id="9eade-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="9eade-108">Peut être conçue comme une étape d’orchestration.</span><span class="sxs-lookup"><span data-stu-id="9eade-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="9eade-109">Peut déclencher une action externe.</span><span class="sxs-lookup"><span data-stu-id="9eade-109">Can trigger an external action.</span></span> <span data-ttu-id="9eade-110">Par exemple, elle peut enregistrer un événement dans une base de données externe.</span><span class="sxs-lookup"><span data-stu-id="9eade-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="9eade-111">Peut être utilisée pour extraire une valeur puis la stocker dans la base de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9eade-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="9eade-112">Vous pouvez utiliser ultérieurement les revendications reçues pour modifier le flux d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9eade-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="9eade-113">Vous pouvez aussi concevoir l’interaction comme un profil de validation.</span><span class="sxs-lookup"><span data-stu-id="9eade-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="9eade-114">Pour plus d’informations, consultez [Intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure Active Directory B2C comme validation d’une entrée de l’utilisateur](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="9eade-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="9eade-115">Le scénario est le suivant : quand un utilisateur effectue une modification du profil, nous voulons :</span><span class="sxs-lookup"><span data-stu-id="9eade-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="9eade-116">Rechercher l’utilisateur dans un système externe.</span><span class="sxs-lookup"><span data-stu-id="9eade-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="9eade-117">Obtenir la ville dans laquelle cet utilisateur est inscrit.</span><span class="sxs-lookup"><span data-stu-id="9eade-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="9eade-118">Retourner cet attribut à l’application sous forme de revendication.</span><span class="sxs-lookup"><span data-stu-id="9eade-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9eade-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9eade-119">Prerequisites</span></span>

- <span data-ttu-id="9eade-120">Un locataire Azure AD B2C configuré pour effectuer une inscription/connexion à un compte local, comme décrit dans [Bien démarrer](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="9eade-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="9eade-121">Un point de terminaison API REST avec lequel vous allez interargir.</span><span class="sxs-lookup"><span data-stu-id="9eade-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="9eade-122">Cette procédure pas à pas utilise comme exemple un webhook d’application de fonction Azure simple.</span><span class="sxs-lookup"><span data-stu-id="9eade-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="9eade-123">*Recommandé* : suivez la procédure pas à pas d’échange de revendications de l’[API REST comme une étape de validation](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="9eade-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="9eade-124">Étape 1 : préparation de la fonction de l’API REST</span><span class="sxs-lookup"><span data-stu-id="9eade-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="9eade-125">Cet article ne traite pas de la configuration des fonctions de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="9eade-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="9eade-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) fournit un excellent kit de ressources pour la création de services RESTful dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="9eade-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="9eade-127">Nous avons configuré une fonction Azure qui reçoit une revendication appelée `email` puis qui retourne simplement la revendication `city` avec la valeur affectée `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="9eade-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="9eade-128">L’exemple de fonction Azure se trouve sur [Github](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="9eade-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="9eade-129">La revendication `userMessage` retournée par la fonction Azure est facultative dans ce contexte et elle sera ignorée par l’infrastructure d’expérience d’identité.</span><span class="sxs-lookup"><span data-stu-id="9eade-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="9eade-130">Vous pouvez éventuellement l’utiliser comme message passé à l’application et présenté ultérieurement à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9eade-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

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

<span data-ttu-id="9eade-131">Une application de fonction Azure facilite l’obtention de l’URL de la fonction, qui inclut l’identificateur de la fonction spécifique.</span><span class="sxs-lookup"><span data-stu-id="9eade-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="9eade-132">Dans ce cas, l’URL est : https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="9eade-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="9eade-133">Vous pouvez l’utiliser pour les tests.</span><span class="sxs-lookup"><span data-stu-id="9eade-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="9eade-134">Étape 2 : configuration de l’échange de revendications de l’API RESTful comme profil technique dans votre fichier TrustFrameworExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="9eade-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="9eade-135">Le profil technique est la configuration complète de l’échange souhaité avec le service RESTful.</span><span class="sxs-lookup"><span data-stu-id="9eade-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="9eade-136">Ouvrez le fichier TrustFrameworkExtensions.xml et ajoutez l’extrait de code XML suivant à l’intérieur de l’élément `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="9eade-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="9eade-137">Dans le code XML suivant, le fournisseur RESTful `Version=1.0.0.0` est décrit comme étant le protocole.</span><span class="sxs-lookup"><span data-stu-id="9eade-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="9eade-138">Considérez-le comme étant la fonction qui interagit avec le service externe.</span><span class="sxs-lookup"><span data-stu-id="9eade-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="9eade-139">L’élément `<InputClaims>` définit les revendications qui seront envoyées depuis l’IEF vers le service REST.</span><span class="sxs-lookup"><span data-stu-id="9eade-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="9eade-140">Dans cet exemple, le contenu de la revendication `givenName` sera envoyé au service REST en tant que revendication `email`.</span><span class="sxs-lookup"><span data-stu-id="9eade-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="9eade-141">L’élément `<OutputClaims>` définit les revendications que l’IEF doit recevoir du service REST.</span><span class="sxs-lookup"><span data-stu-id="9eade-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="9eade-142">Quel que soit le nombre de revendications reçues, l’infrastructure d’expérience d’identité utilisera seulement celles qui sont identifiées ici.</span><span class="sxs-lookup"><span data-stu-id="9eade-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="9eade-143">Dans cet exemple, une revendication reçue en tant que `city` sera mappée à une revendication de l’infrastructure d’expérience d’identité appelée `city`.</span><span class="sxs-lookup"><span data-stu-id="9eade-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="9eade-144">Étape 3 : ajout d’une nouvelle revendication `city` au schéma de votre fichier TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="9eade-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="9eade-145">La revendication `city` n’est définie pour l’instant nulle part dans notre schéma.</span><span class="sxs-lookup"><span data-stu-id="9eade-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="9eade-146">Ajoutez donc une définition à l’intérieur de l’élément `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="9eade-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="9eade-147">Vous pouvez trouver cet élément au début du fichier TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="9eade-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
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

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="9eade-148">Étape 4 : inclusion de l’échange de revendications du service REST en tant qu’étape d’orchestration dans votre parcours utilisateur de modification de profil dans votre fichier TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="9eade-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="9eade-149">Ajoutez une étape au parcours utilisateur de modification de profil, une fois que l’utilisateur a été authentifié (étapes d’orchestration 1 à 4 du fichier XML suivant) et qu’il a fourni les informations de profil mises à jour (étape 5).</span><span class="sxs-lookup"><span data-stu-id="9eade-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="9eade-150">Vous pouvez utiliser l’appel de l’API REST comme étape d’orchestration dans de nombreux cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="9eade-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="9eade-151">Il peut par exemple être utilisé comme mise à jour pour un système externe une fois qu’un utilisateur a terminé une tâche, comme sa première inscription ou une mise à jour de son profil, afin de synchroniser les informations.</span><span class="sxs-lookup"><span data-stu-id="9eade-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="9eade-152">Dans ce cas, il est utilisé pour transférer les informations fournies à l’application après la modification du profil.</span><span class="sxs-lookup"><span data-stu-id="9eade-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="9eade-153">Copiez le code XML du parcours utilisateur de modification du profil du fichier TrustFrameworkBase.xml vers votre fichier TrustFrameworkExtensions.xml, à l’intérieur de l’élément `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="9eade-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="9eade-154">Effectuez la modification de l’étape 6.</span><span class="sxs-lookup"><span data-stu-id="9eade-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="9eade-155">Si l’ordre ne correspond pas à votre version, veillez à insérer le code comme étape avant le type `ClaimsExchange` `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="9eade-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="9eade-156">Le code XML final pour le parcours utilisateur doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="9eade-156">The final XML for the user journey should look like this:</span></span>

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
        <!-- Add a step 6 to the user journey before the JWT token is created-->
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

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="9eade-157">Étape 5 : ajout de la revendication `city` à votre fichier de stratégie de partie de confiance pour que la revendication soit envoyée à votre application</span><span class="sxs-lookup"><span data-stu-id="9eade-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="9eade-158">Ouvrez votre fichier de partie de confiance ProfileEdit.xml et modifiez l’élément `<TechnicalProfile Id="PolicyProfile">` en y ajoutant ceci : `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="9eade-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="9eade-159">Une fois que vous avez ajouté la nouvelle revendication, le profil technique ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="9eade-159">After you add the new claim, the technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="9eade-160">Étape 6 : téléchargement et test de vos modifications</span><span class="sxs-lookup"><span data-stu-id="9eade-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="9eade-161">Remplacez les versions existantes de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="9eade-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="9eade-162">(Facultatif :) Enregistrez la version existante de votre fichier d’extensions (en la téléchargeant) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="9eade-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="9eade-163">Nous vous recommandons de ne pas télécharger plusieurs versions du fichier d’extensions afin de ne pas compliquer l’opération.</span><span class="sxs-lookup"><span data-stu-id="9eade-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="9eade-164">(Facultatif :) Renommez la nouvelle version de l’ID de stratégie pour le fichier de modification de stratégie en changeant `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="9eade-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="9eade-165">Chargez le fichier d’extensions.</span><span class="sxs-lookup"><span data-stu-id="9eade-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="9eade-166">Chargez le fichier de partie de confiance de modification de stratégie.</span><span class="sxs-lookup"><span data-stu-id="9eade-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="9eade-167">Utilisez **Exécuter maintenant** pour tester la stratégie.</span><span class="sxs-lookup"><span data-stu-id="9eade-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="9eade-168">Examinez le jeton retourné par l’infrastructure d’expérience d’identité à l’application.</span><span class="sxs-lookup"><span data-stu-id="9eade-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="9eade-169">Si tout est bien configuré, le jeton inclut la nouvelle revendication `city`, avec la valeur `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="9eade-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9eade-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9eade-170">Next steps</span></span>

<span data-ttu-id="9eade-171">[Use a REST API as a validation step](active-directory-b2c-rest-api-validation-custom.md) (Utilisation d’une API REST comme une étape de validation)</span><span class="sxs-lookup"><span data-stu-id="9eade-171">[Use a REST API as a validation step](active-directory-b2c-rest-api-validation-custom.md)</span></span>

[<span data-ttu-id="9eade-172">Changer la modification de profil pour rassembler des informations supplémentaires de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="9eade-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
