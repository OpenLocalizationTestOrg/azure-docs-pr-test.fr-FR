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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="ef633-103">Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure AD B2C comme étape d’orchestration</span><span class="sxs-lookup"><span data-stu-id="ef633-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="ef633-104">Hello identité expérience Framework (IEF) qui se trouve sous Azure Active Directory B2C (B2C Active Directory de Azure) permet de hello identité développeur toointegrate une interaction avec une API RESTful dans un parcours de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ef633-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="ef633-105">À la fin de hello de cette procédure pas à pas, vous serez en mesure de toocreate un voyage utilisateur Azure AD B2C qui interagit avec les services RESTful.</span><span class="sxs-lookup"><span data-stu-id="ef633-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="ef633-106">Hello IEF envoie des données dans les demandes et reçoit des données dans les revendications.</span><span class="sxs-lookup"><span data-stu-id="ef633-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="ef633-107">Hello exchange de revendications d’API REST :</span><span class="sxs-lookup"><span data-stu-id="ef633-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="ef633-108">Peut être conçue comme une étape d’orchestration.</span><span class="sxs-lookup"><span data-stu-id="ef633-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="ef633-109">Peut déclencher une action externe.</span><span class="sxs-lookup"><span data-stu-id="ef633-109">Can trigger an external action.</span></span> <span data-ttu-id="ef633-110">Par exemple, elle peut enregistrer un événement dans une base de données externe.</span><span class="sxs-lookup"><span data-stu-id="ef633-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="ef633-111">Peut être utilisé toofetch une valeur et puis le stocker dans la base de données utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="ef633-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="ef633-112">Vous pouvez utiliser les revendications hello a reçu des flux de hello toochange ultérieure d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ef633-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="ef633-113">Vous pouvez également concevoir interaction hello tant que profil de validation.</span><span class="sxs-lookup"><span data-stu-id="ef633-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="ef633-114">Pour plus d’informations, consultez [Intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure Active Directory B2C comme validation d’une entrée de l’utilisateur](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ef633-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="ef633-115">scénario de Hello est que lorsqu’un utilisateur effectue une modification de profil, nous voulons :</span><span class="sxs-lookup"><span data-stu-id="ef633-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="ef633-116">Rechercher hello utilisateur dans un système externe.</span><span class="sxs-lookup"><span data-stu-id="ef633-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="ef633-117">Obtenir la ville hello dans laquelle cet utilisateur est enregistré.</span><span class="sxs-lookup"><span data-stu-id="ef633-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="ef633-118">Retourner l’application toohello attribut comme une revendication.</span><span class="sxs-lookup"><span data-stu-id="ef633-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef633-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ef633-119">Prerequisites</span></span>

- <span data-ttu-id="ef633-120">Un toocomplete de client configuré un compte de connexion-haut/connectez-vous, comme décrit dans Azure AD B2C [mise en route](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ef633-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="ef633-121">Un toointeract de point de terminaison API REST avec.</span><span class="sxs-lookup"><span data-stu-id="ef633-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="ef633-122">Cette procédure pas à pas utilise comme exemple un webhook d’application de fonction Azure simple.</span><span class="sxs-lookup"><span data-stu-id="ef633-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="ef633-123">*Recommandé*: hello complète [API REST de procédure pas à pas d’exchange en tant qu’une étape de validation des revendications](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ef633-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="ef633-124">Étape 1 : Préparer la fonction d’API REST hello</span><span class="sxs-lookup"><span data-stu-id="ef633-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="ef633-125">Le programme d’installation de fonctions de l’API REST est en dehors de la portée de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="ef633-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="ef633-126">[Les fonctions Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fournit un excellente toolkit toocreate des services RESTful dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="ef633-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="ef633-127">Nous avons mis en place une fonction Azure qui reçoit une demande de remboursement appelé `email`, et puis retourne hello revendication `city` avec la valeur hello affecté `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="ef633-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="ef633-128">l’exemple Hello fonction Azure se trouve sur [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="ef633-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="ef633-129">Hello `userMessage` revendication hello retours de fonction Azure est facultative dans ce contexte et hello IEF il sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="ef633-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="ef633-130">Vous pouvez éventuellement l’utiliser comme un message transmis toohello application et présentées toohello utilisateur plus tard.</span><span class="sxs-lookup"><span data-stu-id="ef633-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

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

<span data-ttu-id="ef633-131">Une application Azure fonction rend tooget facile hello fonction URL, ce qui peut inclure un identificateur de fonction spécifique de hello hello.</span><span class="sxs-lookup"><span data-stu-id="ef633-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="ef633-132">Dans ce cas, les URL de hello est : https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="ef633-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="ef633-133">Vous pouvez l’utiliser pour les tests.</span><span class="sxs-lookup"><span data-stu-id="ef633-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="ef633-134">Étape 2 : Configurer exchange de revendications d’API RESTful hello comme profil technique dans votre fichier TrustFrameworExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="ef633-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="ef633-135">Un profil de technique est la configuration complète de hello d’exchange hello souhaitée avec hello service RESTful.</span><span class="sxs-lookup"><span data-stu-id="ef633-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="ef633-136">Ouvrir le fichier de TrustFrameworkExtensions.xml hello et ajouter hello suivant extrait XML à l’intérieur de hello `<ClaimsProvider>` élément.</span><span class="sxs-lookup"><span data-stu-id="ef633-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="ef633-137">Bonjour, XML, fournisseur RESTful suivant `Version=1.0.0.0` est décrite en tant que protocole de hello.</span><span class="sxs-lookup"><span data-stu-id="ef633-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="ef633-138">Le considérer comme fonction hello qui interagit avec un service externe de hello.</span><span class="sxs-lookup"><span data-stu-id="ef633-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="ef633-139">Hello `<InputClaims>` élément définit les revendications hello qui seront envoyées à partir de hello service REST de toohello IEF.</span><span class="sxs-lookup"><span data-stu-id="ef633-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="ef633-140">Dans cet exemple, hello le contenu de la revendication de hello `givenName` service REST de toohello sera envoyé en tant que revendication de hello `email`.</span><span class="sxs-lookup"><span data-stu-id="ef633-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="ef633-141">Hello `<OutputClaims>` élément définit les revendications hello que hello IEF s’attend à partir du service REST hello.</span><span class="sxs-lookup"><span data-stu-id="ef633-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="ef633-142">Quel que soit le nombre de hello de revendications qui sont reçus, hello IEF utilisera uniquement les identifié ici.</span><span class="sxs-lookup"><span data-stu-id="ef633-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="ef633-143">Dans cet exemple, une revendication reçue en tant que `city` sera mappé tooan IEF revendication appelée `city`.</span><span class="sxs-lookup"><span data-stu-id="ef633-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="ef633-144">Étape 3 : Ajouter la nouvelle revendication d’hello `city` schéma toohello de votre fichier TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="ef633-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="ef633-145">revendication de Hello `city` n’est pas encore défini n’importe où dans notre schéma.</span><span class="sxs-lookup"><span data-stu-id="ef633-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="ef633-146">Par conséquent, ajoutez une définition dans un élément hello `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="ef633-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="ef633-147">Vous pouvez trouver cet élément au début de hello du fichier de TrustFrameworkExtensions.xml hello.</span><span class="sxs-lookup"><span data-stu-id="ef633-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

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

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="ef633-148">Étape 4 : Inclure hello REST service revendications exchange en tant qu’orchestration étape dans votre profil Modifier utilisateur du voyage dans TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="ef633-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="ef633-149">Ajoutez une étape voyage utilisateur modifier toohello profil, une fois hello utilisateur a été authentifié (étapes d’orchestration 1-4 Bonjour XML suivant) et l’utilisateur de hello a fourni les informations de profil hello mis à jour (étape 5).</span><span class="sxs-lookup"><span data-stu-id="ef633-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="ef633-150">Il existe plusieurs cas d’usage où hello appel d’API REST peut être utilisé en tant qu’orchestration étape.</span><span class="sxs-lookup"><span data-stu-id="ef633-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="ef633-151">En guise d’étape d’orchestration, il peut servir un système externe tooan de mise à jour après qu’un utilisateur a terminé une tâche comme première inscription ou tant que profil de mettre à jour les informations tookeep synchronisées.</span><span class="sxs-lookup"><span data-stu-id="ef633-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="ef633-152">Dans ce cas, il est utilisé tooaugment hello informations toohello application une fois le profil de hello modifier.</span><span class="sxs-lookup"><span data-stu-id="ef633-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="ef633-153">Copier le profil hello Modifier code XML utilisateur voyage hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml fichier à l’intérieur de hello `<UserJourneys>` élément.</span><span class="sxs-lookup"><span data-stu-id="ef633-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="ef633-154">Apportez la modification de hello sous l’étape 6.</span><span class="sxs-lookup"><span data-stu-id="ef633-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="ef633-155">Si l’ordre de hello ne correspond pas à votre version, assurez-vous que vous insérez le code de hello en tant qu’étape hello avant hello `ClaimsExchange` type `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="ef633-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="ef633-156">Hello XML final pour le voyage d’utilisateur hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="ef633-156">hello final XML for hello user journey should look like this:</span></span>

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

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="ef633-157">Étape 5 : Ajouter des revendications de hello `city` stratégie tiers de la partie de confiance tooyour fichier afin de la revendication de hello est envoyée à tooyour application</span><span class="sxs-lookup"><span data-stu-id="ef633-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="ef633-158">Modifiez votre fichier tiers (RP) de la partie de confiance ProfileEdit.xml et hello `<TechnicalProfile Id="PolicyProfile">` suivant de hello élément tooadd : `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="ef633-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="ef633-159">Après avoir ajouté la nouvelle revendication de hello, profil de technique hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="ef633-159">After you add hello new claim, hello technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="ef633-160">Étape 6 : téléchargement et test de vos modifications</span><span class="sxs-lookup"><span data-stu-id="ef633-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="ef633-161">Remplacer les versions existantes de hello de stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="ef633-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="ef633-162">(Facultatif :) Enregistrez version existante de hello (en le téléchargeant) de votre fichier extensions avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="ef633-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="ef633-163">tookeep hello initiale complexité faible, nous recommandons que vous ne téléchargez pas plusieurs versions du fichier des extensions hello.</span><span class="sxs-lookup"><span data-stu-id="ef633-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="ef633-164">(Facultatif :) Renommer la nouvelle version de hello d’ID de stratégie hello pour modifier le fichier de stratégie hello en modifiant `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="ef633-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="ef633-165">Téléchargez le fichier des extensions hello.</span><span class="sxs-lookup"><span data-stu-id="ef633-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="ef633-166">Téléchargez hello stratégie modifier RP le fichier.</span><span class="sxs-lookup"><span data-stu-id="ef633-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="ef633-167">Utilisez **exécuter maintenant** stratégie de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="ef633-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="ef633-168">Jeton hello révision hello IEF retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="ef633-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="ef633-169">Si tout est configuré correctement, le jeton de hello inclura la nouvelle revendication d’hello `city`, avec la valeur de hello `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="ef633-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ef633-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef633-170">Next steps</span></span>

<span data-ttu-id="ef633-171">[Use a REST API as a validation step](active-directory-b2c-rest-api-validation-custom.md) (Utilisation d’une API REST comme une étape de validation)</span><span class="sxs-lookup"><span data-stu-id="ef633-171">[Use a REST API as a validation step](active-directory-b2c-rest-api-validation-custom.md)</span></span>

[<span data-ttu-id="ef633-172">Modifier hello profil modifier toogather des informations supplémentaires à partir de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ef633-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
