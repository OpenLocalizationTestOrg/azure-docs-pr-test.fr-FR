---
title: "modèles d’aaaPage dans Gestion des API Azure | Documents Microsoft"
description: "Découvrez comment toocustomize hello le contenu des pages de portail de développement à l’aide d’un ensemble de modèles dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: e57df269-1019-4b74-b74d-53155b809d59
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 84bd971ad4bcacfdd36c2ebbe05b16063f2a547b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="16fe0-103">Modèles de page dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="16fe0-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="16fe0-104">Gestion des API Azure fournit que Hello de contenu de hello toocustomize possibilité de pages du portail développeur à l’aide d’un ensemble de modèles que configurer leur contenu.</span><span class="sxs-lookup"><span data-stu-id="16fe0-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="16fe0-105">À l’aide de [DotLiquid](http://dotliquidmarkup.org/) syntaxe et hello l’éditeur de votre choix, tel que [DotLiquid pour les concepteurs](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), et un ensemble fourni de localisée [ressources de type chaîne](api-management-template-resources.md#strings), [ Ressources de glyphe](api-management-template-resources.md#glyphs), et [Page les contrôles](api-management-page-controls.md), vous avez une grande souplesse tooconfigure hello contenu hello pages comme vous le souhaitez à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="16fe0-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="16fe0-106">modèles de Hello dans cette section permettent de contenu de hello toocustomize de hello connexion, l’authentification des et page pages introuvable dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="16fe0-106">hello templates in this section allow you toocustomize hello content of hello sign in, sign up, and page not found pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="16fe0-107">Connexion</span><span class="sxs-lookup"><span data-stu-id="16fe0-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="16fe0-108">Inscription</span><span class="sxs-lookup"><span data-stu-id="16fe0-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="16fe0-109">Page introuvable</span><span class="sxs-lookup"><span data-stu-id="16fe0-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="16fe0-110">Exemples de modèles par défaut sont inclus dans hello suivant la documentation, mais sont toochange sujet en raison des améliorations de toocontinuous.</span><span class="sxs-lookup"><span data-stu-id="16fe0-110">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="16fe0-111">Vous pouvez afficher les modèles par défaut dynamique hello dans le portail des développeurs hello en naviguant toohello souhaitée des modèles individuels.</span><span class="sxs-lookup"><span data-stu-id="16fe0-111">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="16fe0-112">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="16fe0-112">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="16fe0-113"><a name="SignIn"></a> Connexion</span><span class="sxs-lookup"><span data-stu-id="16fe0-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="16fe0-114">Hello **connectez-vous** modèle vous permet de toocustomize hello signe dans la page dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="16fe0-114">hello **sign in** template allows you toocustomize hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="16fe0-115">![Page de connexion](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "Modèles du portail des développeurs de la page de connexion APIM")</span><span class="sxs-lookup"><span data-stu-id="16fe0-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="16fe0-116">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="16fe0-116">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SigninStrings|WebAuthenticationSigninTitle" %}</h2>  
{% if registrationEnabled == true %}  
<p class="text-center">{% localized "SigninStrings|WebAuthenticationNotAMember" %}</p>  
{% endif %}  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    {% if registrationEnabled == true %}  
        <p>{% localized "SigninStrings|WebAuthenticationSigininWithPassword" %}</p>  
    <basic-SignIn></basic-SignIn>  
    {% endif %}  
  </div>  
  
    {% if registrationEnabled != true and providers.size == 0 %}  
        {% localized "ProviderInfoStrings|TextboxExternalIdentitiesDisabled" %}  
  {% else %}  
        {% if providers.size > 0 %}  
      <div class="col-md-6">  
            <div class="providers-list">  
                <p class="text-left">  
                {% if registrationEnabled == true %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitation" %}  
                {% else %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitationPrimary" %}  
                {% endif %}  
                </p>  
        <providers></providers>  
            </div>  
    </div>  
        {% endif %}  
    {% endif %}  
  
  {% if userRegistrationTermsEnabled == true %}  
    <div class="col-md-6">  
        <div id="terms" class="modal" role="dialog" tabindex="-1">  
            <div class="modal-dialog">  
                <div class="modal-content">  
                    <div class="modal-header">  
                        <h4 class="modal-title">{% localized "SigninResources|DialogHeadingTermsOfUse" %}</h4>  
                    </div>  
                    <div class="modal-body break-all">{{userRegistrationTerms}}</div>  
                    <div class="modal-footer">  
                        <button type="button" class="btn btn-default" data-dismiss="modal">{% localized "CommonStrings|ButtonLabelClose" %}</button>  
                    </div>  
                </div>  
            </div>  
        </div>  
        <p>{% localized "SigninResources|TextblockUserRegistrationTermsProvided" %}</p>  
    </div>  
    {% endif %}  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="16fe0-117">Commandes</span><span class="sxs-lookup"><span data-stu-id="16fe0-117">Controls</span></span>  
 <span data-ttu-id="16fe0-118">Ce modèle peut utiliser des éléments suivants de hello [page les contrôles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="16fe0-118">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="16fe0-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="16fe0-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="16fe0-120">fournisseurs</span><span class="sxs-lookup"><span data-stu-id="16fe0-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="16fe0-121">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="16fe0-121">Data model</span></span>  
 <span data-ttu-id="16fe0-122">Entité [Connexion de l’utilisateur](api-management-template-data-model-reference.md#UseSignIn).</span><span class="sxs-lookup"><span data-stu-id="16fe0-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="16fe0-123">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="16fe0-123">Sample template data</span></span>  
  
```json  
{  
    "Email": null,  
    "Password": null,  
    "ReturnUrl": null,  
    "RememberMe": false,  
    "RegistrationEnabled": true,  
    "DelegationEnabled": false,  
    "DelegationUrl": null,  
    "SsoSignUpUrl": null,  
    "AuxServiceUrl": "https://manage.windowsazure.com/#Workspaces/ApiManagementExtension/service/contoso5/dashboard",  
    "Providers": [  
        {  
            "Properties": {  
                "AuthenticationType": "Aad",  
                "Caption": "Azure Active Directory"  
            },  
            "AuthenticationType": "Aad",  
            "Caption": "Azure Active Directory"  
        }  
    ],  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsEnabled": false  
}  
```  
  
##  <span data-ttu-id="16fe0-124"><a name="SignUp"></a> Inscription</span><span class="sxs-lookup"><span data-stu-id="16fe0-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="16fe0-125">Hello **inscrire** modèle vous permet de page d’inscription hello toocustomize dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="16fe0-125">hello **sign up** template allows you toocustomize hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="16fe0-126">![Page d’inscription](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "Modèles du portail des développeurs de la page d’inscription APIM")</span><span class="sxs-lookup"><span data-stu-id="16fe0-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="16fe0-127">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="16fe0-127">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SignupStrings|PageTitleSignup" %}</h2>  
<p class="text-center">  
  {% localized "SignupStrings|WebAuthenticationAlreadyAMember" %} <a href="/signin">{% localized "SignupStrings|WebAuthenticationSigninNow" %}</a>  
</p>  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    <p>{% localized "SignupStrings|WebAuthenticationCreateNewAccount" %}</p>  
    <sign-up></sign-up>  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="16fe0-128">Commandes</span><span class="sxs-lookup"><span data-stu-id="16fe0-128">Controls</span></span>  
 <span data-ttu-id="16fe0-129">Ce modèle peut utiliser des éléments suivants de hello [page les contrôles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="16fe0-129">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="16fe0-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="16fe0-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="16fe0-131">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="16fe0-131">Data model</span></span>  
 <span data-ttu-id="16fe0-132">Entité [Inscription de l’utilisateur](api-management-template-data-model-reference.md#UserSignUp).</span><span class="sxs-lookup"><span data-stu-id="16fe0-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="16fe0-133">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="16fe0-133">Sample template data</span></span>  
  
```json  
{  
    "PasswordConfirm": null,  
    "Password": null,  
    "PasswordVerdictLevel": 0,  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsOptions": 0,  
    "ConsentAccepted": false,  
    "Email": null,  
    "FirstName": null,  
    "LastName": null,  
    "UserData": null,  
    "NameIdentifier": null,  
    "ProviderName": null  
}  
```  
  
##  <span data-ttu-id="16fe0-134"><a name="PageNotFound"></a> Page introuvable</span><span class="sxs-lookup"><span data-stu-id="16fe0-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="16fe0-135">Hello **page non trouvée** modèle permet de vous toocustomize hello page non trouvée page dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="16fe0-135">hello **page not found** template allows you toocustomize hello page not found page in hello developer portal.</span></span>  
  
 <span data-ttu-id="16fe0-136">![Page introuvable](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "Modèles du portail des développeurs de la page Page introuvable APIM")</span><span class="sxs-lookup"><span data-stu-id="16fe0-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="16fe0-137">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="16fe0-137">Default template</span></span>  
  
```xml  
<h2>{% localized "NotFoundStrings|PageTitleNotFound" %}</h2>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialCause" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseOldLink" %}</li>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseMisspelledUrl" %}</li>  
</ul>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialSolution" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialSolutionRetype" %}</li>  
  <li>  
    {% capture textPotentialSolutionStartOver %}{% localized "NotFoundStrings|TextblockPotentialSolutionStartOver" %}{% endcapture %}  
    {% capture homeLink %}<a href="/">{% localized "NotFoundStrings|LinkLabelHomePage" %}</a>{% endcapture %}  
    {% assign replaceString = '{0}' %}  
  
    {{ textPotentialSolutionStartOver | replace : replaceString, homeLink }}  
  </li>  
</ul>  
  
<p>  
  {% capture textReportProblem %}{% localized "NotFoundStrings|TextReportProblem" %}{% endcapture %}  
  {% capture emailLink %}<a href="mailto:apimgmt@microsoft.com" target="_self" title="API Management Support">{% localized "NotFoundStrings|LinkLabelSendUsEmail" %}</a>{% endcapture %}  
  {% assign replaceString = '{0}' %}  
  
  {{ textReportProblem | replace : replaceString, emailLink }}  
</p>  
```  
  
### <a name="controls"></a><span data-ttu-id="16fe0-138">Commandes</span><span class="sxs-lookup"><span data-stu-id="16fe0-138">Controls</span></span>  
 <span data-ttu-id="16fe0-139">Ce modèle ne peut pas utiliser de [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="16fe0-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="16fe0-140">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="16fe0-140">Data model</span></span>  
  
|<span data-ttu-id="16fe0-141">Propriété</span><span class="sxs-lookup"><span data-stu-id="16fe0-141">Property</span></span>|<span data-ttu-id="16fe0-142">Type</span><span class="sxs-lookup"><span data-stu-id="16fe0-142">Type</span></span>|<span data-ttu-id="16fe0-143">Description</span><span class="sxs-lookup"><span data-stu-id="16fe0-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="16fe0-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="16fe0-144">referenceCode</span></span>|<span data-ttu-id="16fe0-145">string</span><span class="sxs-lookup"><span data-stu-id="16fe0-145">string</span></span>|<span data-ttu-id="16fe0-146">Code généré si cette page s’est affichée en tant que résultat de hello d’une erreur interne.</span><span class="sxs-lookup"><span data-stu-id="16fe0-146">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="16fe0-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="16fe0-147">errorCode</span></span>|<span data-ttu-id="16fe0-148">string</span><span class="sxs-lookup"><span data-stu-id="16fe0-148">string</span></span>|<span data-ttu-id="16fe0-149">Code généré si cette page s’est affichée en tant que résultat de hello d’une erreur interne.</span><span class="sxs-lookup"><span data-stu-id="16fe0-149">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="16fe0-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="16fe0-150">emailBody</span></span>|<span data-ttu-id="16fe0-151">string</span><span class="sxs-lookup"><span data-stu-id="16fe0-151">string</span></span>|<span data-ttu-id="16fe0-152">Envoyer par courrier électronique corps généré si cette page s’est affichée en tant que résultat de hello d’une erreur interne.</span><span class="sxs-lookup"><span data-stu-id="16fe0-152">Email body generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="16fe0-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="16fe0-153">requestedUrl</span></span>|<span data-ttu-id="16fe0-154">string</span><span class="sxs-lookup"><span data-stu-id="16fe0-154">string</span></span>|<span data-ttu-id="16fe0-155">URL de Hello demandé lors de la page de hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="16fe0-155">hello URL requested when hello page was not found.</span></span>|  
|<span data-ttu-id="16fe0-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="16fe0-156">referrerUrl</span></span>|<span data-ttu-id="16fe0-157">string</span><span class="sxs-lookup"><span data-stu-id="16fe0-157">string</span></span>|<span data-ttu-id="16fe0-158">Hello référent URL toohello des URL demandée.</span><span class="sxs-lookup"><span data-stu-id="16fe0-158">hello referrer URL toohello requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="16fe0-159">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="16fe0-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="16fe0-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="16fe0-160">Next steps</span></span>
<span data-ttu-id="16fe0-161">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="16fe0-161">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
