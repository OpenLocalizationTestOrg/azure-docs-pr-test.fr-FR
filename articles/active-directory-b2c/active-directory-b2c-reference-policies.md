---
title: "Azure Active Directory B2C : stratégies intégrées | Microsoft Docs"
description: "Une rubrique sur l'infrastructure de stratégie extensible d'Azure Active Directory B2C et la création de différents types de stratégies"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: daad3af089afdf76b930053728bb11a5cf4c2a92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="7c444-103">Azure Active Directory B2C: stratégies intégrées</span><span class="sxs-lookup"><span data-stu-id="7c444-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="7c444-104">L’infrastructure de stratégie extensible d’Azure Active Directory (Azure AD) B2C est le pilier central du service.</span><span class="sxs-lookup"><span data-stu-id="7c444-104">The extensible policy framework of Azure Active Directory (Azure AD) B2C is the core strength of the service.</span></span> <span data-ttu-id="7c444-105">Les stratégies décrivent entièrement les expériences relatives à l’identité des consommateurs, telles que l’inscription, la connexion ou la modification de profil.</span><span class="sxs-lookup"><span data-stu-id="7c444-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="7c444-106">Par exemple, une stratégie d'inscription vous permet de contrôler les comportements en configurant les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="7c444-106">For instance, a sign-up policy allows you to control behaviors by configuring the following settings:</span></span>

* <span data-ttu-id="7c444-107">types de compte (réseaux sociaux tels que Facebook et comptes locaux tels que des adresses de courrier) que les clients peuvent utiliser pour s’inscrire à l’application ;</span><span class="sxs-lookup"><span data-stu-id="7c444-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use to sign up for the application</span></span>
* <span data-ttu-id="7c444-108">attributs (par exemple, prénom, code postal et pointure) à recueillir auprès du client lors de l’inscription ;</span><span class="sxs-lookup"><span data-stu-id="7c444-108">Attributes (for example, first name, postal code, and shoe size) to be collected from the consumer during sign-up</span></span>
* <span data-ttu-id="7c444-109">utilisation d’Azure Multi-Factor Authentication ;</span><span class="sxs-lookup"><span data-stu-id="7c444-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="7c444-110">aspect de toutes les pages d'inscription ;</span><span class="sxs-lookup"><span data-stu-id="7c444-110">The look and feel of all sign-up pages</span></span>
* <span data-ttu-id="7c444-111">informations (qui apparaissent en tant que revendications dans un jeton) que l’application reçoit lorsque l’exécution de la stratégie est terminée.</span><span class="sxs-lookup"><span data-stu-id="7c444-111">Information (which manifests as claims in a token) that the application receives when the policy run finishes</span></span>

<span data-ttu-id="7c444-112">Vous pouvez créer plusieurs stratégies de types différents dans votre client et les utiliser dans vos applications en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="7c444-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="7c444-113">Les stratégies peuvent être réutilisées entre les différentes applications.</span><span class="sxs-lookup"><span data-stu-id="7c444-113">Policies can be reused across applications.</span></span> <span data-ttu-id="7c444-114">Cette flexibilité permet aux développeurs de définir et de modifier les expériences relatives à l’identité du client avec peu ou pas de modification du code.</span><span class="sxs-lookup"><span data-stu-id="7c444-114">This flexibility enables developers to define and modify consumer identity experiences with minimal or no changes to their code.</span></span>

<span data-ttu-id="7c444-115">Les stratégies sont disponibles à l'utilisation par le biais d'une interface développeur simple.</span><span class="sxs-lookup"><span data-stu-id="7c444-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="7c444-116">Votre application déclenche une stratégie avec une requête d'authentification HTTP standard (en transmettant un paramètre de stratégie dans la requête) et reçoit un jeton personnalisé en réponse.</span><span class="sxs-lookup"><span data-stu-id="7c444-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in the request) and receives a customized token as response.</span></span> <span data-ttu-id="7c444-117">Par exemple, la seule différence entre les requêtes invoquant une stratégie d’inscription et celles invoquant une stratégie de connexion réside dans le nom de stratégie utilisé dans le paramètre de chaîne de requête « p » :</span><span class="sxs-lookup"><span data-stu-id="7c444-117">For example, the only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is the policy name that's used in the "p" query string parameter:</span></span>

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

<span data-ttu-id="7c444-118">Pour plus d’informations sur l’infrastructure de stratégie, consultez [ce billet de blog concernant Azure AD B2C sur le blog consacré à la mobilité et à la sécurité d’entreprise](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c444-118">For more information about the policy framework, see [this blog post about Azure AD B2C on the Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="7c444-119">Création d’une stratégie d’inscription ou de connexion</span><span class="sxs-lookup"><span data-stu-id="7c444-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="7c444-120">Cette stratégie gère les expériences d’inscription et de connexion des utilisateurs avec une configuration unique.</span><span class="sxs-lookup"><span data-stu-id="7c444-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="7c444-121">Les utilisateurs sont dirigés vers le chemin d’accès correct (inscription ou connexion) en fonction du contexte.</span><span class="sxs-lookup"><span data-stu-id="7c444-121">Consumers are led down the right path (sign-up or sign-in) depending on the context.</span></span> <span data-ttu-id="7c444-122">Cet article décrit également le contenu des jetons que l’application recevra en cas d’inscription ou de connexion réussie.  Un exemple de code pour la stratégie d’inscription ou de connexion est [disponible ici](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="7c444-122">It also describes the contents of tokens that the application will receive upon successful sign-ups or sign-ins.  A code sample for the sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="7c444-123">Il est recommandé d’utiliser cette stratégie plutôt qu’une stratégie d’inscription et de connexion.</span><span class="sxs-lookup"><span data-stu-id="7c444-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="7c444-124">Création d’une stratégie d’inscription</span><span class="sxs-lookup"><span data-stu-id="7c444-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="7c444-125">Création d’une stratégie de connexion</span><span class="sxs-lookup"><span data-stu-id="7c444-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="7c444-126">Création d’une stratégie de modification de profil</span><span class="sxs-lookup"><span data-stu-id="7c444-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="7c444-127">Création d’une stratégie de réinitialisation du mot de passe</span><span class="sxs-lookup"><span data-stu-id="7c444-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="7c444-128">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="7c444-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="7c444-129">Comment lier une stratégie d’inscription ou de connexion à une stratégie de réinitialisation de mot de passe ?</span><span class="sxs-lookup"><span data-stu-id="7c444-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="7c444-130">Lorsque vous créez une stratégie d’inscription ou de connexion (avec des comptes locaux), vous voyez un lien **Mot de passe oublié ?** sur la première page.</span><span class="sxs-lookup"><span data-stu-id="7c444-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on the first page of the experience.</span></span> <span data-ttu-id="7c444-131">Cliquer sur ce lien ne déclenche pas automatiquement une stratégie de réinitialisation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7c444-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="7c444-132">Au lieu de cela, le code d’erreur **`AADB2C90118`** est retourné à votre application.</span><span class="sxs-lookup"><span data-stu-id="7c444-132">Instead, the error code **`AADB2C90118`** is returned to your app.</span></span> <span data-ttu-id="7c444-133">Votre application a besoin de gérer ce code d’erreur en appelant une stratégie de réinitialisation de mot de passe spécifique.</span><span class="sxs-lookup"><span data-stu-id="7c444-133">Your app needs to handle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="7c444-134">Pour plus d’informations, consultez un [exemple qui illustre l’approche de la liaison de stratégies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="7c444-134">For more information, see a [sample that demonstrates the approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="7c444-135">Dois-je utiliser une stratégie d’inscription ou de connexion ou une stratégie d’inscription et une stratégie de connexion ?</span><span class="sxs-lookup"><span data-stu-id="7c444-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="7c444-136">Nous vous recommandons d’utiliser une stratégie d’inscription ou de connexion plutôt qu’une stratégie d’inscription et une stratégie de connexion.</span><span class="sxs-lookup"><span data-stu-id="7c444-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="7c444-137">La stratégie d’inscription ou de connexion offre plus de possibilités que la stratégie de connexion.</span><span class="sxs-lookup"><span data-stu-id="7c444-137">The sign-up or sign-in policy has more capabilities than the sign-in policy.</span></span> <span data-ttu-id="7c444-138">Elle vous permet également d’utiliser une personnalisation de l’interface utilisateur de la page et offre une meilleure prise en charge de la localisation.</span><span class="sxs-lookup"><span data-stu-id="7c444-138">It also enables you to use page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="7c444-139">La stratégie de connexion est recommandée si vous n’avez pas besoin de localiser vos stratégies mais que vous avez besoin uniquement de fonctionnalités de personnalisation mineures, et souhaitez que la réinitialisation de mot de passe y soit intégrée.</span><span class="sxs-lookup"><span data-stu-id="7c444-139">The sign-in policy is recommended if you don't need to localize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c444-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c444-140">Next steps</span></span>
* [<span data-ttu-id="7c444-141">Configuration du jeton, de la session et de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7c444-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="7c444-142">Désactiver la vérification par courrier électronique lors de l’inscription du consommateur</span><span class="sxs-lookup"><span data-stu-id="7c444-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

