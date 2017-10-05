---
title: "Modèles de page dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment personnaliser le contenu des pages du portail des développeurs à l’aide d’un ensemble de modèles dans Gestion des API Azure."
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
ms.openlocfilehash: 7f9ef37a694bce786b6acaa428df83f0cb23c2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="c760b-103">Modèles de page dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="c760b-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="c760b-104">Gestion des API Azure vous offre la possibilité de personnaliser le contenu des pages du portail des développeurs à l’aide d’un ensemble de modèles qui configurent leur contenu.</span><span class="sxs-lookup"><span data-stu-id="c760b-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="c760b-105">En utilisant la syntaxe [DotLiquid](http://dotliquidmarkup.org/) et l’éditeur de votre choix, comme [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ainsi qu’un ensemble de [ressources de chaîne](api-management-template-resources.md#strings), de [ressources de glyphe](api-management-template-resources.md#glyphs) et de [contrôles de page](api-management-page-controls.md) localisés, vous disposez d’un large choix pour configurer le contenu des pages selon vos besoins à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="c760b-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="c760b-106">Les modèles de cette section vous permettent de personnaliser le contenu des pages de connexion, des pages d’authentification et des pages introuvables dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="c760b-106">The templates in this section allow you to customize the content of the sign in, sign up, and page not found pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="c760b-107">Connexion</span><span class="sxs-lookup"><span data-stu-id="c760b-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="c760b-108">Inscription</span><span class="sxs-lookup"><span data-stu-id="c760b-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="c760b-109">Page introuvable</span><span class="sxs-lookup"><span data-stu-id="c760b-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="c760b-110">Les exemples de modèles par défaut inclus dans la documentation suivante sont susceptibles d’être modifiés et améliorés de façon régulière.</span><span class="sxs-lookup"><span data-stu-id="c760b-110">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="c760b-111">Vous pouvez afficher les modèles dynamiques par défaut dans le portail des développeurs en accédant aux modèles individuels souhaités.</span><span class="sxs-lookup"><span data-stu-id="c760b-111">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="c760b-112">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="c760b-112">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="c760b-113"><a name="SignIn"></a> Connexion</span><span class="sxs-lookup"><span data-stu-id="c760b-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="c760b-114">Le modèle de **connexion** vous permet de personnaliser la page de connexion dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="c760b-114">The **sign in** template allows you to customize the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="c760b-115">![Page de connexion](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "Modèles du portail des développeurs de la page de connexion APIM")</span><span class="sxs-lookup"><span data-stu-id="c760b-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="c760b-116">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="c760b-116">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="c760b-117">Commandes</span><span class="sxs-lookup"><span data-stu-id="c760b-117">Controls</span></span>  
 <span data-ttu-id="c760b-118">Ce modèle peut utiliser les [contrôles de page](api-management-page-controls.md) suivants.</span><span class="sxs-lookup"><span data-stu-id="c760b-118">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="c760b-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="c760b-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="c760b-120">fournisseurs</span><span class="sxs-lookup"><span data-stu-id="c760b-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="c760b-121">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="c760b-121">Data model</span></span>  
 <span data-ttu-id="c760b-122">Entité [Connexion de l’utilisateur](api-management-template-data-model-reference.md#UseSignIn).</span><span class="sxs-lookup"><span data-stu-id="c760b-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="c760b-123">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="c760b-123">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="c760b-124"><a name="SignUp"></a> Inscription</span><span class="sxs-lookup"><span data-stu-id="c760b-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="c760b-125">Le modèle d’**inscription** vous permet de personnaliser la page d’inscription dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="c760b-125">The **sign up** template allows you to customize the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="c760b-126">![Page d’inscription](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "Modèles du portail des développeurs de la page d’inscription APIM")</span><span class="sxs-lookup"><span data-stu-id="c760b-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="c760b-127">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="c760b-127">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="c760b-128">Commandes</span><span class="sxs-lookup"><span data-stu-id="c760b-128">Controls</span></span>  
 <span data-ttu-id="c760b-129">Ce modèle peut utiliser les [contrôles de page](api-management-page-controls.md) suivants.</span><span class="sxs-lookup"><span data-stu-id="c760b-129">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="c760b-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="c760b-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="c760b-131">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="c760b-131">Data model</span></span>  
 <span data-ttu-id="c760b-132">Entité [Inscription de l’utilisateur](api-management-template-data-model-reference.md#UserSignUp).</span><span class="sxs-lookup"><span data-stu-id="c760b-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="c760b-133">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="c760b-133">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="c760b-134"><a name="PageNotFound"></a> Page introuvable</span><span class="sxs-lookup"><span data-stu-id="c760b-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="c760b-135">Le modèle **Page introuvable** vous permet de personnaliser la page « Page introuvable » dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="c760b-135">The **page not found** template allows you to customize the page not found page in the developer portal.</span></span>  
  
 <span data-ttu-id="c760b-136">![Page introuvable](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "Modèles du portail des développeurs de la page Page introuvable APIM")</span><span class="sxs-lookup"><span data-stu-id="c760b-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="c760b-137">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="c760b-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="c760b-138">Commandes</span><span class="sxs-lookup"><span data-stu-id="c760b-138">Controls</span></span>  
 <span data-ttu-id="c760b-139">Ce modèle ne peut pas utiliser de [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="c760b-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="c760b-140">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="c760b-140">Data model</span></span>  
  
|<span data-ttu-id="c760b-141">Propriété</span><span class="sxs-lookup"><span data-stu-id="c760b-141">Property</span></span>|<span data-ttu-id="c760b-142">Type</span><span class="sxs-lookup"><span data-stu-id="c760b-142">Type</span></span>|<span data-ttu-id="c760b-143">Description</span><span class="sxs-lookup"><span data-stu-id="c760b-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="c760b-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="c760b-144">referenceCode</span></span>|<span data-ttu-id="c760b-145">string</span><span class="sxs-lookup"><span data-stu-id="c760b-145">string</span></span>|<span data-ttu-id="c760b-146">Code généré si cette page s’est affichée à la suite d’une erreur interne.</span><span class="sxs-lookup"><span data-stu-id="c760b-146">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="c760b-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="c760b-147">errorCode</span></span>|<span data-ttu-id="c760b-148">string</span><span class="sxs-lookup"><span data-stu-id="c760b-148">string</span></span>|<span data-ttu-id="c760b-149">Code généré si cette page s’est affichée à la suite d’une erreur interne.</span><span class="sxs-lookup"><span data-stu-id="c760b-149">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="c760b-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="c760b-150">emailBody</span></span>|<span data-ttu-id="c760b-151">string</span><span class="sxs-lookup"><span data-stu-id="c760b-151">string</span></span>|<span data-ttu-id="c760b-152">Corps d’e-mail généré si cette page s’est affichée à la suite d’une erreur interne.</span><span class="sxs-lookup"><span data-stu-id="c760b-152">Email body generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="c760b-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="c760b-153">requestedUrl</span></span>|<span data-ttu-id="c760b-154">string</span><span class="sxs-lookup"><span data-stu-id="c760b-154">string</span></span>|<span data-ttu-id="c760b-155">URL demandée quand la page est introuvable.</span><span class="sxs-lookup"><span data-stu-id="c760b-155">The URL requested when the page was not found.</span></span>|  
|<span data-ttu-id="c760b-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="c760b-156">referrerUrl</span></span>|<span data-ttu-id="c760b-157">string</span><span class="sxs-lookup"><span data-stu-id="c760b-157">string</span></span>|<span data-ttu-id="c760b-158">URL de point d’accès pointant vers l’URL demandée.</span><span class="sxs-lookup"><span data-stu-id="c760b-158">The referrer URL to the requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="c760b-159">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="c760b-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="c760b-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c760b-160">Next steps</span></span>
<span data-ttu-id="c760b-161">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c760b-161">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>