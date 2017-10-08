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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="f19e5-103">Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure Active Directory B2C comme validation d’une entrée de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f19e5-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="f19e5-104">Hello identité expérience Framework (IEF) qui se trouve sous Azure Active Directory B2C (B2C Active Directory de Azure) permet de hello identité développeur toointegrate une interaction avec une API RESTful dans un parcours de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f19e5-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="f19e5-105">À la fin de hello de cette procédure pas à pas, vous serez en mesure de toocreate un voyage utilisateur Azure AD B2C qui interagit avec les services RESTful.</span><span class="sxs-lookup"><span data-stu-id="f19e5-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="f19e5-106">Hello IEF envoie des données dans les demandes et reçoit des données dans les revendications.</span><span class="sxs-lookup"><span data-stu-id="f19e5-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="f19e5-107">interaction Hello avec hello API :</span><span class="sxs-lookup"><span data-stu-id="f19e5-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="f19e5-108">Peut être conçue comme un échange de revendications de l’API REST ou comme un profil de validation, qui s’effectue dans une étape d’orchestration.</span><span class="sxs-lookup"><span data-stu-id="f19e5-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="f19e5-109">En général, valide l’entrée d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="f19e5-109">Typically validates input from hello user.</span></span> <span data-ttu-id="f19e5-110">Si la valeur hello à partir de l’utilisateur de hello est rejetée, utilisateur de hello peut essayer de nouveau tooenter une valeur valide avec hello opportunité tooreturn un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="f19e5-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="f19e5-111">Vous pouvez également concevoir interaction hello en guise d’étape d’orchestration.</span><span class="sxs-lookup"><span data-stu-id="f19e5-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="f19e5-112">Pour plus d’informations, consultez [Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure Active Directory B2C comme étape d’orchestration](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="f19e5-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="f19e5-113">Par exemple de profil de validation hello, nous allons utiliser voyage de hello profil Modifier utilisateur dans le fichier de pack de démarrage hello ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="f19e5-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="f19e5-114">Nous pouvons vérifier ce nom hello fournie par l’utilisateur hello dans le profil de hello Edition n’est pas partie d’une liste d’exclusion.</span><span class="sxs-lookup"><span data-stu-id="f19e5-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f19e5-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f19e5-115">Prerequisites</span></span>

- <span data-ttu-id="f19e5-116">Un toocomplete de client configuré un compte de connexion-haut/connectez-vous, comme décrit dans Azure AD B2C [mise en route](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="f19e5-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="f19e5-117">Un toointeract de point de terminaison API REST avec.</span><span class="sxs-lookup"><span data-stu-id="f19e5-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="f19e5-118">Pour cette procédure pas à pas, nous avons configuré un site de démonstration appelé [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) avec un service de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="f19e5-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="f19e5-119">Étape 1 : Préparer la fonction d’API REST hello</span><span class="sxs-lookup"><span data-stu-id="f19e5-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="f19e5-120">Le programme d’installation de fonctions de l’API REST est en dehors de la portée de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="f19e5-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="f19e5-121">[Les fonctions Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fournit un excellente toolkit toocreate des services RESTful dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="f19e5-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="f19e5-122">Nous avons créé une fonction Azure qui reçoit une revendication qu’elle attend en tant que `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="f19e5-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="f19e5-123">fonction Hello valide qui indique si cette revendication.</span><span class="sxs-lookup"><span data-stu-id="f19e5-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="f19e5-124">Vous pouvez accéder à code de fonction Azure complète hello dans [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="f19e5-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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

<span data-ttu-id="f19e5-125">Hello IEF attend hello `userMessage` cette fonction Azure hello retourne de la revendication.</span><span class="sxs-lookup"><span data-stu-id="f19e5-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="f19e5-126">Cette demande s’affiche en tant qu’un utilisateur toohello de chaîne si la validation de hello échoue, par exemple quand il est retourné un état de 409 conflit Bonjour précédent exemple.</span><span class="sxs-lookup"><span data-stu-id="f19e5-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="f19e5-127">Étape 2 : Configurer exchange de revendications d’API RESTful hello comme profil technique dans votre fichier TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="f19e5-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="f19e5-128">Un profil de technique est la configuration complète de hello d’exchange hello souhaitée avec hello service RESTful.</span><span class="sxs-lookup"><span data-stu-id="f19e5-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="f19e5-129">Ouvrir le fichier de TrustFrameworkExtensions.xml hello et ajouter hello suivant extrait XML à l’intérieur de hello `<ClaimsProviders>` élément.</span><span class="sxs-lookup"><span data-stu-id="f19e5-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="f19e5-130">Bonjour, XML, fournisseur RESTful suivant `Version=1.0.0.0` est décrite en tant que protocole de hello.</span><span class="sxs-lookup"><span data-stu-id="f19e5-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="f19e5-131">Le considérer comme fonction hello qui interagit avec un service externe de hello.</span><span class="sxs-lookup"><span data-stu-id="f19e5-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="f19e5-132">Hello `InputClaims` élément définit les revendications hello qui seront envoyées à partir de hello service REST de toohello IEF.</span><span class="sxs-lookup"><span data-stu-id="f19e5-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="f19e5-133">Dans cet exemple, hello le contenu de la revendication de hello `givenName` sera envoyé service REST de toohello comme `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="f19e5-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="f19e5-134">Dans cet exemple, hello QU'IEF n’attend pas de revendications précédent.</span><span class="sxs-lookup"><span data-stu-id="f19e5-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="f19e5-135">Au lieu de cela, il attend une réponse de service REST de hello et agit selon les codes d’état hello qu’il reçoit.</span><span class="sxs-lookup"><span data-stu-id="f19e5-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="f19e5-136">Étape 3 : Inclure hello service RESTful revendications exchange dans automatique déclarée profil technique où vous souhaitez toovalidate hello l’entrée d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f19e5-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="f19e5-137">utilisation la plus courante de l’étape de validation hello Hello est dans une interaction de hello avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f19e5-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="f19e5-138">Toutes les interactions où les utilisateurs hello sont tooprovide attendu d’entrée sont *automatique déclarée profils techniques*.</span><span class="sxs-lookup"><span data-stu-id="f19e5-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="f19e5-139">Pour cet exemple, nous allons ajouter profil technique du libre-service Asserted-ProfileUpdate toohello validation hello.</span><span class="sxs-lookup"><span data-stu-id="f19e5-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="f19e5-140">Il s’agit profil technique hello hello du fichier de stratégie de confiance partie de confiance `Profile Edit` utilise.</span><span class="sxs-lookup"><span data-stu-id="f19e5-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="f19e5-141">tooadd hello revendications exchange toohello automatique déclarée profil technique :</span><span class="sxs-lookup"><span data-stu-id="f19e5-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="f19e5-142">Ouvrez le fichier TrustFrameworkBase.xml de hello et recherchez `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="f19e5-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="f19e5-143">Passez en revue la configuration hello de ce profil technique.</span><span class="sxs-lookup"><span data-stu-id="f19e5-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="f19e5-144">Observez comment exchange hello avec l’utilisateur de hello est défini en tant que revendications qui seront demandées de l’utilisateur hello (revendications d’entrée) et qui sera attendu de fournisseur de hello automatique déclarée (revendications de sortie).</span><span class="sxs-lookup"><span data-stu-id="f19e5-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="f19e5-145">Recherchez `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`. Notez que ce profil est appelé au titre de l’étape d’orchestration 6 de `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="f19e5-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="f19e5-146">Étape 4 : Télécharger et d’un fichier de stratégie de hello profil modifier RP test</span><span class="sxs-lookup"><span data-stu-id="f19e5-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="f19e5-147">Téléchargez hello une nouvelle version du fichier de TrustFrameworkExtensions.xml hello.</span><span class="sxs-lookup"><span data-stu-id="f19e5-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="f19e5-148">Utilisez **exécuter maintenant** profil de hello tootest modifier le fichier de stratégie RP.</span><span class="sxs-lookup"><span data-stu-id="f19e5-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="f19e5-149">Test de validation de hello en fournissant un des noms de hello existant (par exemple, mcvinny) Bonjour **prénom** champ.</span><span class="sxs-lookup"><span data-stu-id="f19e5-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="f19e5-150">Si tout est configuré correctement, vous devez recevoir un message qui avertit les utilisateurs hello que hello lecteur balise est déjà utilisée.</span><span class="sxs-lookup"><span data-stu-id="f19e5-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f19e5-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f19e5-151">Next steps</span></span>

[<span data-ttu-id="f19e5-152">Modifier hello profil utilisateur et modifier l’inscription toogather des informations supplémentaires à partir de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="f19e5-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="f19e5-153">Procédure pas à pas : intégration des échanges de revendications de l’API REST dans votre parcours utilisateur Azure AD B2C comme étape d’orchestration</span><span class="sxs-lookup"><span data-stu-id="f19e5-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
