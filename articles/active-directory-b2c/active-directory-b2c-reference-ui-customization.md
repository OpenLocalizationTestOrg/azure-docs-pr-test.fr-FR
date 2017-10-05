---
title: "Personnalisation de l’interface utilisateur (IU) - Azure AD B2C | Documents Microsoft"
description: "Une rubrique sur les fonctionnalités de personnalisation de l’interface utilisateur (UI) dans Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 122fa997ea11b369aae3c59edf0043ab19d21aea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-customize-the-azure-ad-b2c-user-interface-ui"></a><span data-ttu-id="8cc3b-103">Azure Active Directory B2C : personnalisation de l’interface utilisateur Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="8cc3b-103">Azure Active Directory B2C: Customize the Azure AD B2C user interface (UI)</span></span>

<span data-ttu-id="8cc3b-104">L’expérience utilisateur est primordiale dans une application orientée client.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-104">User experience is paramount in a customer facing application.</span></span>  <span data-ttu-id="8cc3b-105">Développez votre base clients en créant des expériences utilisateur avec l’apparence de votre marque.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-105">Grow your customer base by crafting user experiences with the look and feel of your brand.</span></span> <span data-ttu-id="8cc3b-106">Azure Active Directory B2C (Azure AD B2C) vous permet de personnaliser les pages d’inscription, de connexion, de modification du profil et de réinitialisation du mot de passe avec le contrôle pixel-perfect.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-106">Azure Active Directory B2C (Azure AD B2C) lets you customize sign-up, sign-in, profile editing, and password reset pages with pixel-perfect control.</span></span>

> [!NOTE]
> <span data-ttu-id="8cc3b-107">La fonctionnalité de personnalisation de l’interface utilisateur de page décrite dans cet article ne s’applique pas à la stratégie d’authentification uniquement, à sa page de réinitialisation du mot de passe qui l’accompagne ni aux e-mails de vérification.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-107">The page UI customization feature described in this article does not apply to the sign-in only policy, its accompanying password reset page, and verification emails.</span></span>  <span data-ttu-id="8cc3b-108">Ces fonctionnalités utilisent la [fonctionnalité de marque de société](../active-directory/active-directory-add-company-branding.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-108">These features use the [company branding feature](../active-directory/active-directory-add-company-branding.md) instead.</span></span>
>

<span data-ttu-id="8cc3b-109">Cet article aborde les thèmes suivants :</span><span class="sxs-lookup"><span data-stu-id="8cc3b-109">This article covers the following topics:</span></span>

* <span data-ttu-id="8cc3b-110">la fonctionnalité de personnalisation de l’interface utilisateur de page.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-110">The page UI customization feature.</span></span>
* <span data-ttu-id="8cc3b-111">Un outil de téléchargement du contenu HTML pour Azure Blob Storage pour une utilisation avec la fonctionnalité de personnalisation de l’interface utilisateur de page.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-111">A tool for uploading HTML content to Azure Blob Storage for use with the page UI customization feature.</span></span>
* <span data-ttu-id="8cc3b-112">Les éléments de l’interface utilisateur utilisés par Azure AD B2C que vous pouvez personnaliser à l’aide des feuilles de Style en cascade (CSS).</span><span class="sxs-lookup"><span data-stu-id="8cc3b-112">The UI elements used by Azure AD B2C that you can customize using Cascading Style Sheets (CSS).</span></span>
* <span data-ttu-id="8cc3b-113">Meilleures pratiques lors de l’exercice de cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-113">Best practices when exercising this feature.</span></span>

## <a name="the-page-ui-customization-feature"></a><span data-ttu-id="8cc3b-114">La fonctionnalité de personnalisation de l’interface utilisateur de page</span><span class="sxs-lookup"><span data-stu-id="8cc3b-114">The page UI customization feature</span></span>

<span data-ttu-id="8cc3b-115">Vous pouvez personnaliser l’apparence des pages d’inscription, de connexion, de réinitialisation du mot de passe et de modification du profil (en configurant des [stratégies](active-directory-b2c-reference-policies.md)).</span><span class="sxs-lookup"><span data-stu-id="8cc3b-115">You can customize the look and feel of customer sign-up, sign-in, password reset, and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span></span> <span data-ttu-id="8cc3b-116">Vos clients bénéficieront d’une expérience transparente lors de la navigation entre votre application et les pages fournies par Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-116">Your customers get a seamless experience when navigating between your application and pages served by Azure AD B2C.</span></span>

<span data-ttu-id="8cc3b-117">Contrairement à d’autres services avec des options de l’interface utilisateur, Azure AD B2C utilise une approche simple et moderne à la personnalisation de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-117">Unlike other services where UI options, Azure AD B2C uses a simple and modern approach to UI customization.</span></span>

<span data-ttu-id="8cc3b-118">Voici comment cela fonctionne : Azure AD B2C exécute le code dans le navigateur client et utilise une approche moderne appelée [partage des ressources cross-origin (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="8cc3b-118">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span>  <span data-ttu-id="8cc3b-119">Au moment de l’exécution, le contenu est chargé depuis une URL que vous spécifiez dans une stratégie.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-119">At run-time, content is loaded from a URL that you specify in a policy.</span></span> <span data-ttu-id="8cc3b-120">Vous pouvez spécifier des URL différentes pour différentes pages.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-120">You can specify different URLs for different pages.</span></span> <span data-ttu-id="8cc3b-121">Une fois le contenu chargé à partir de votre URL est fusionné à un fragment HTML inséré depuis Azure AD B2C, la page s’affiche pour votre client.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-121">After content loaded from your URL is merged with an HTML fragment inserted from Azure AD B2C, the page is displayed to your customer.</span></span> <span data-ttu-id="8cc3b-122">Procédure à suivre :</span><span class="sxs-lookup"><span data-stu-id="8cc3b-122">All you need to do is:</span></span>

1. <span data-ttu-id="8cc3b-123">Créez un contenu HTML5 correct avec un élément `<div id="api"></div>` vide situé quelque part dans le `<body>`.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-123">Create well-formed HTML5 content with an empty `<div id="api"></div>` element located somewhere in the `<body>`.</span></span> <span data-ttu-id="8cc3b-124">Cet élément marque l’endroit où le contenu Azure AD B2C est inséré.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-124">This element marks where the Azure AD B2C content is inserted.</span></span>
1. <span data-ttu-id="8cc3b-125">Héberger votre contenu sur un point de terminaison HTTPS (avec CORS activé).</span><span class="sxs-lookup"><span data-stu-id="8cc3b-125">Host your content on an HTTPS endpoint (with CORS allowed).</span></span> <span data-ttu-id="8cc3b-126">Notez que vous devez activer à la fois les méthodes de demande GET et OPTIONS lors de la configuration de CORS.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-126">Note both GET and OPTIONS request methods must be enabled when configuring CORS.</span></span>
1. <span data-ttu-id="8cc3b-127">Utilisez les feuilles de style en cascade pour donner du style aux éléments d’interface utilisateur dans lesquels est inséré Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-127">Use CSS to style the UI elements that Azure AD B2C inserts.</span></span>

### <a name="a-basic-example-of-customized-html"></a><span data-ttu-id="8cc3b-128">Un exemple de base de code HTML personnalisé</span><span class="sxs-lookup"><span data-stu-id="8cc3b-128">A basic example of customized HTML</span></span>

<span data-ttu-id="8cc3b-129">L’exemple suivant présente le contenu HTML élémentaire que vous pouvez utiliser pour tester cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-129">The following example is the most basic HTML content that you can use to test this capability.</span></span> <span data-ttu-id="8cc3b-130">Utilisez [l’outil d’assistance](active-directory-b2c-reference-ui-customization-helper-tool.md) pour télécharger et configurer ce contenu sur votre stockage Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-130">Use the [helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) to upload and configure this content on your Azure Blob storage.</span></span> <span data-ttu-id="8cc3b-131">Vous pouvez ensuite vérifier l’affichage et le fonctionnement des boutons et champs de formulaire de base (non stylisés) sur chaque page.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-131">You can then verify that the basic, non-stylized buttons & form fields on each page are displayed and functional.</span></span>

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-the-ui-customization-feature"></a><span data-ttu-id="8cc3b-132">Tester la fonctionnalité de personnalisation de l’interface</span><span class="sxs-lookup"><span data-stu-id="8cc3b-132">Test out the UI customization feature</span></span>

<span data-ttu-id="8cc3b-133">Vous souhaitez tester la fonctionnalité de personnalisation de l’interface utilisateur à l’aide de notre exemple de code HTML et de contenu CSS ?</span><span class="sxs-lookup"><span data-stu-id="8cc3b-133">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span>  <span data-ttu-id="8cc3b-134">Nous vous avons fourni [un outil d’assistance](active-directory-b2c-reference-ui-customization-helper-tool.md) qui télécharge et configure notre exemple de contenu sur votre stockage Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-134">We've provided you [a helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="8cc3b-135">Vous pouvez héberger le contenu de votre interface utilisateur sur tous types d’emplacements : serveurs web, CDN, AWS S3, systèmes de partage de fichiers, etc. Tout est possible à condition que le contenu soit hébergé sur un point de terminaison HTTPS disponible publiquement, avec CORS activé.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-135">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as the content is hosted on a publicly available HTTPS endpoint with CORS enabled, you are good to go.</span></span> <span data-ttu-id="8cc3b-136">Nous utilisons Azure Blob Storage à titre indicatif uniquement.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-136">We are using Azure Blob storage for illustrative purposes only.</span></span>
>

## <a name="the-ui-fragments-embedded-by-azure-ad-b2c"></a><span data-ttu-id="8cc3b-137">Les fragments de l’interface utilisateur incorporés par Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="8cc3b-137">The UI fragments embedded by Azure AD B2C</span></span>

<span data-ttu-id="8cc3b-138">Les sections suivantes répertorient les fragments HTML5 qu’Azure AD B2C fusionne dans l’élément `<div id="api"></div>` situé dans votre contenu.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-138">The following sections list the HTML5 fragments that Azure AD B2C merges into the `<div id="api"></div>` element located in your content.</span></span> <span data-ttu-id="8cc3b-139">**N’insérez pas ces fragments dans votre contenu HTML5.**</span><span class="sxs-lookup"><span data-stu-id="8cc3b-139">**Do not insert these fragments in your HTML 5 content.**</span></span> <span data-ttu-id="8cc3b-140">Le service Azure AD B2C les insère au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-140">The Azure AD B2C service inserts them in at run-time.</span></span> <span data-ttu-id="8cc3b-141">Utilisez ces fragments en tant que référence lors de la conception de vos propres feuilles de Style en cascade (CSS).</span><span class="sxs-lookup"><span data-stu-id="8cc3b-141">Use these fragments as a reference when designing your own Cascading Style Sheets (CSS).</span></span>

### <a name="fragment-inserted-into-the-identity-provider-selection-page"></a><span data-ttu-id="8cc3b-142">Fragment inséré dans la « page Sélection du fournisseur d’identité »</span><span class="sxs-lookup"><span data-stu-id="8cc3b-142">Fragment inserted into the "Identity provider selection page"</span></span>

<span data-ttu-id="8cc3b-143">Cette page contient une liste de fournisseurs d’identité parmi lesquels l’utilisateur peut faire son choix à l’inscription ou à la connexion.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-143">This page contains a list of identity providers that the user can choose from during sign-up or sign-in.</span></span> <span data-ttu-id="8cc3b-144">Ces boutons incluent des fournisseurs d’identité sociale tels que Facebook et Google+ ou de comptes locaux (basés sur une adresse e-mail ou un nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="8cc3b-144">These buttons include social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span>

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-the-local-account-sign-up-page"></a><span data-ttu-id="8cc3b-145">Fragment inséré dans la « page Inscription à un compte local »</span><span class="sxs-lookup"><span data-stu-id="8cc3b-145">Fragment inserted into the "Local account sign-up page"</span></span>

<span data-ttu-id="8cc3b-146">Cette page contient un formulaire d’inscription du compte local basée sur une adresse e-mail ou un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-146">This page contains a form for local account sign-up based on an email address or a user name.</span></span> <span data-ttu-id="8cc3b-147">Le formulaire peut contenir différentes commandes de saisie telles que la zone de saisie de texte, celle du mot de passe, le bouton radio, les cases du menu déroulant à sélection unique et la sélection de plusieurs cases à cocher.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-147">The form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span>

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing the following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">The password entry fields do not match. Please enter the same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent to your inbox. Please copy it to the input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need to send new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used to contact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('The postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-the-social-account-sign-up-page"></a><span data-ttu-id="8cc3b-148">Fragment inséré dans la « page Inscription à un compte social »</span><span class="sxs-lookup"><span data-stu-id="8cc3b-148">Fragment inserted into the ""Social account sign-up page"</span></span>

<span data-ttu-id="8cc3b-149">Cette page peut s’afficher lors de l’inscription à l’aide d’un compte existant depuis un fournisseur d’identité sociale tel que Facebook ou Google+.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-149">This page may appear when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span>  <span data-ttu-id="8cc3b-150">Cette page est utilisée lorsque des informations supplémentaires doivent être collectées depuis un utilisateur final à l’aide du formulaire d’inscription.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-150">It is used when additional information must be collected from the end user using a sign-up form.</span></span> <span data-ttu-id="8cc3b-151">Cette page est similaire à la page d’inscription à un compte local (affiché dans la section précédente) à l’exception des champs de saisie de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-151">This page is similar to the local account sign-up page (shown in the previous section) with the exception of the password entry fields.</span></span>

### <a name="fragment-inserted-into-the-unified-sign-up-or-sign-in-page"></a><span data-ttu-id="8cc3b-152">Fragment inséré dans la « page Inscription ou connexion unifiées »</span><span class="sxs-lookup"><span data-stu-id="8cc3b-152">Fragment inserted into the "Unified sign-up or sign-in page"</span></span>

<span data-ttu-id="8cc3b-153">Cette page gère l’inscription et la connexion des utilisateurs, qui peuvent utiliser les fournisseurs d’identité des réseaux sociaux, tels que Facebook ou Google+, ou des comptes locaux.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-153">This page handles both sign-up & sign-in of customers, who can use social identity providers such as Facebook or Google+, or local accounts.</span></span>

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-the-multi-factor-authentication-page"></a><span data-ttu-id="8cc3b-154">Fragment inséré dans la « page Authentification multifacteur »</span><span class="sxs-lookup"><span data-stu-id="8cc3b-154">Fragment inserted into the "Multi-factor authentication page"</span></span>

<span data-ttu-id="8cc3b-155">Cette page permet aux utilisateurs de vérifier leurs numéros de téléphone (par voie textuelle ou vocale) au cours de l’inscription ou de la connexion.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-155">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span>

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone to authenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-the-error-page"></a><span data-ttu-id="8cc3b-156">Fragment inséré dans la « page Erreur »</span><span class="sxs-lookup"><span data-stu-id="8cc3b-156">Fragment inserted into the ""Error page"</span></span>

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if the problem persists feel free to contact us. In the meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting the remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a><span data-ttu-id="8cc3b-157">Localisation de votre contenu HTML</span><span class="sxs-lookup"><span data-stu-id="8cc3b-157">Localizing your HTML content</span></span>

<span data-ttu-id="8cc3b-158">Vous pouvez localiser votre contenu HTML en activant [« Personnalisation de la langue »](active-directory-b2c-reference-language-customization.md).</span><span class="sxs-lookup"><span data-stu-id="8cc3b-158">You can localize your HTML content by turning on ['Language customization'](active-directory-b2c-reference-language-customization.md).</span></span>  <span data-ttu-id="8cc3b-159">L’activation de cette fonctionnalité permet à Azure AD B2C de transmettre le paramètre Open ID Connect, `ui-locales`, à votre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-159">Enabling this feature allows Azure AD B2C to forward the Open ID Connect parameter, `ui-locales`, to your endpoint.</span></span>  <span data-ttu-id="8cc3b-160">Votre serveur de contenu peut utiliser ce paramètre pour fournir des pages HTML personnalisées qui sont spécifiques à la langue.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-160">Your content server can use this parameter to provide customized HTML pages that are language-specific.</span></span>

## <a name="things-to-remember-when-building-your-own-content"></a><span data-ttu-id="8cc3b-161">Points à retenir lors de la création de votre propre contenu</span><span class="sxs-lookup"><span data-stu-id="8cc3b-161">Things to remember when building your own content</span></span>

<span data-ttu-id="8cc3b-162">Si vous envisagez d’utiliser la fonctionnalité de personnalisation d’interface utilisateur de page, veuillez consulter les meilleures pratiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="8cc3b-162">If you are planning to use the page UI customization feature, review the following best practices:</span></span>

* <span data-ttu-id="8cc3b-163">Ne copiez pas le contenu par défaut Azure AD B2C et n’essayez pas de le modifier.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-163">Don't copy the Azure AD B2C's default content and attempt to modify it.</span></span> <span data-ttu-id="8cc3b-164">Il est préférable de créer votre contenu HTML5 à partir de zéro et d’utiliser le contenu par défaut comme référence.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-164">It is best to build your HTML5 content from scratch and to use default content as reference.</span></span>
* <span data-ttu-id="8cc3b-165">Pour des raisons de sécurité, nous ne vous permettons pas d’inclure du langage JavaScript dans votre contenu.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-165">For security reasons, we don't allow you to include any JavaScript in your content.</span></span> <span data-ttu-id="8cc3b-166">La plupart des éléments dont vous avez besoin sont disponibles et prêts à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-166">Most of what you need should be available out of the box.</span></span> <span data-ttu-id="8cc3b-167">Dans le cas contraire, utilisez [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) pour demander de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-167">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) to request new functionality.</span></span>
* <span data-ttu-id="8cc3b-168">Versions de navigateur prises en charge :</span><span class="sxs-lookup"><span data-stu-id="8cc3b-168">Supported browser versions:</span></span>
  * <span data-ttu-id="8cc3b-169">Internet Explorer 11, 10, Edge</span><span class="sxs-lookup"><span data-stu-id="8cc3b-169">Internet Explorer 11, 10, Edge</span></span>
  * <span data-ttu-id="8cc3b-170">Prise en charge limitée pour Internet Explorer 9, 8</span><span class="sxs-lookup"><span data-stu-id="8cc3b-170">Limited support for Internet Explorer 9, 8</span></span>
  * <span data-ttu-id="8cc3b-171">Google Chrome 42.0 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="8cc3b-171">Google Chrome 42.0 and above</span></span>
  * <span data-ttu-id="8cc3b-172">Mozilla Firefox 38.0 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="8cc3b-172">Mozilla Firefox 38.0 and above</span></span>
