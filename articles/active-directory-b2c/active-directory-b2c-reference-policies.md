---
title: "Azure Active Directory B2C : stratégies intégrées | Microsoft Docs"
description: "Une rubrique sur l’infrastructure de stratégie extensible hello d’Azure Active Directory B2C et sur la façon toocreate différents types de stratégie"
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
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="57a5d-103">Azure Active Directory B2C: stratégies intégrées</span><span class="sxs-lookup"><span data-stu-id="57a5d-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="57a5d-104">infrastructure de stratégie extensible Hello de B2C d’Azure Active Directory (Azure AD) est la force du noyau de hello du service de hello.</span><span class="sxs-lookup"><span data-stu-id="57a5d-104">hello extensible policy framework of Azure Active Directory (Azure AD) B2C is hello core strength of hello service.</span></span> <span data-ttu-id="57a5d-105">Les stratégies décrivent entièrement les expériences relatives à l’identité des consommateurs, telles que l’inscription, la connexion ou la modification de profil.</span><span class="sxs-lookup"><span data-stu-id="57a5d-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="57a5d-106">Par exemple, une stratégie d’inscription vous permet des comportements toocontrol en hello suivant les paramètres de configuration :</span><span class="sxs-lookup"><span data-stu-id="57a5d-106">For instance, a sign-up policy allows you toocontrol behaviors by configuring hello following settings:</span></span>

* <span data-ttu-id="57a5d-107">Types (comptes sociaux tels que Facebook) ou les comptes locaux, tels que les adresses de messagerie que les utilisateurs peuvent utiliser toosign pour une application hello de comptes</span><span class="sxs-lookup"><span data-stu-id="57a5d-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use toosign up for hello application</span></span>
* <span data-ttu-id="57a5d-108">Attributs (par exemple, prénom, code postal, pointure) toobe collectées à partir de consommateur de hello pendant l’inscription</span><span class="sxs-lookup"><span data-stu-id="57a5d-108">Attributes (for example, first name, postal code, and shoe size) toobe collected from hello consumer during sign-up</span></span>
* <span data-ttu-id="57a5d-109">utilisation d’Azure Multi-Factor Authentication ;</span><span class="sxs-lookup"><span data-stu-id="57a5d-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="57a5d-110">Hello apparence et la convivialité de toutes les pages d’inscription</span><span class="sxs-lookup"><span data-stu-id="57a5d-110">hello look and feel of all sign-up pages</span></span>
* <span data-ttu-id="57a5d-111">Reçoit des informations (qui se manifeste en tant que revendications dans un jeton) hello application issue de la stratégie hello exécuter</span><span class="sxs-lookup"><span data-stu-id="57a5d-111">Information (which manifests as claims in a token) that hello application receives when hello policy run finishes</span></span>

<span data-ttu-id="57a5d-112">Vous pouvez créer plusieurs stratégies de types différents dans votre client et les utiliser dans vos applications en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="57a5d-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="57a5d-113">Les stratégies peuvent être réutilisées entre les différentes applications.</span><span class="sxs-lookup"><span data-stu-id="57a5d-113">Policies can be reused across applications.</span></span> <span data-ttu-id="57a5d-114">Cette flexibilité permet aux développeurs toodefine et modifier des expériences d’identité consommateur avec peu ou aucun code tootheir de modifications.</span><span class="sxs-lookup"><span data-stu-id="57a5d-114">This flexibility enables developers toodefine and modify consumer identity experiences with minimal or no changes tootheir code.</span></span>

<span data-ttu-id="57a5d-115">Les stratégies sont disponibles à l'utilisation par le biais d'une interface développeur simple.</span><span class="sxs-lookup"><span data-stu-id="57a5d-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="57a5d-116">Votre application déclenche une stratégie à l’aide d’une demande d’authentification HTTP standard (en passant un paramètre de stratégie de demande de hello) et reçoit un jeton personnalisé en tant que réponse.</span><span class="sxs-lookup"><span data-stu-id="57a5d-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in hello request) and receives a customized token as response.</span></span> <span data-ttu-id="57a5d-117">Par exemple, hello seule différence entre les demandes qui font appel à une stratégie d’inscription et les demandes qui font appel à une stratégie d’authentification est nom de la stratégie hello qui est utilisé dans le paramètre de chaîne de requête hello « p » :</span><span class="sxs-lookup"><span data-stu-id="57a5d-117">For example, hello only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is hello policy name that's used in hello "p" query string parameter:</span></span>

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

<span data-ttu-id="57a5d-118">Pour plus d’informations sur l’infrastructure de stratégie hello, consultez [ce billet de blog sur B2C d’Active Directory de Azure sur hello mobilité d’entreprise et le Blog de sécurité](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="57a5d-118">For more information about hello policy framework, see [this blog post about Azure AD B2C on hello Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="57a5d-119">Création d’une stratégie d’inscription ou de connexion</span><span class="sxs-lookup"><span data-stu-id="57a5d-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="57a5d-120">Cette stratégie gère les expériences d’inscription et de connexion des utilisateurs avec une configuration unique.</span><span class="sxs-lookup"><span data-stu-id="57a5d-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="57a5d-121">Les consommateurs sont dirigées vers le bas hello chemin d’accès correct (inscription ou connectez-vous) selon le contexte de hello.</span><span class="sxs-lookup"><span data-stu-id="57a5d-121">Consumers are led down hello right path (sign-up or sign-in) depending on hello context.</span></span> <span data-ttu-id="57a5d-122">Elle décrit également le contenu hello de jetons qui reçoit les inscriptions réussies ou connexions application hello.  Un exemple de code pour la stratégie d’inscription ou connectez-vous hello est [disponible ici](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="57a5d-122">It also describes hello contents of tokens that hello application will receive upon successful sign-ups or sign-ins.  A code sample for hello sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="57a5d-123">Il est recommandé d’utiliser cette stratégie plutôt qu’une stratégie d’inscription et de connexion.</span><span class="sxs-lookup"><span data-stu-id="57a5d-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="57a5d-124">Création d’une stratégie d’inscription</span><span class="sxs-lookup"><span data-stu-id="57a5d-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="57a5d-125">Création d’une stratégie de connexion</span><span class="sxs-lookup"><span data-stu-id="57a5d-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="57a5d-126">Création d’une stratégie de modification de profil</span><span class="sxs-lookup"><span data-stu-id="57a5d-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="57a5d-127">Création d’une stratégie de réinitialisation du mot de passe</span><span class="sxs-lookup"><span data-stu-id="57a5d-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="57a5d-128">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="57a5d-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="57a5d-129">Comment lier une stratégie d’inscription ou de connexion à une stratégie de réinitialisation de mot de passe ?</span><span class="sxs-lookup"><span data-stu-id="57a5d-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="57a5d-130">Lorsque vous créez une stratégie d’inscription ou de la connexion (avec des comptes locaux), vous voyez un **mot de passe oublié ?** lien sur la première page de hello d’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="57a5d-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on hello first page of hello experience.</span></span> <span data-ttu-id="57a5d-131">Cliquer sur ce lien ne déclenche pas automatiquement une stratégie de réinitialisation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="57a5d-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="57a5d-132">Au lieu de cela, hello code d’erreur  **`AADB2C90118`**  est retourné tooyour application.</span><span class="sxs-lookup"><span data-stu-id="57a5d-132">Instead, hello error code **`AADB2C90118`** is returned tooyour app.</span></span> <span data-ttu-id="57a5d-133">Votre application doit toohandle ce code d’erreur en appelant une stratégie de réinitialisation de mot de passe spécifiques.</span><span class="sxs-lookup"><span data-stu-id="57a5d-133">Your app needs toohandle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="57a5d-134">Pour plus d’informations, consultez un [exemple qui illustre l’approche hello de liaison des stratégies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="57a5d-134">For more information, see a [sample that demonstrates hello approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="57a5d-135">Dois-je utiliser une stratégie d’inscription ou de connexion ou une stratégie d’inscription et une stratégie de connexion ?</span><span class="sxs-lookup"><span data-stu-id="57a5d-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="57a5d-136">Nous vous recommandons d’utiliser une stratégie d’inscription ou de connexion plutôt qu’une stratégie d’inscription et une stratégie de connexion.</span><span class="sxs-lookup"><span data-stu-id="57a5d-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="57a5d-137">stratégie d’inscription ou connectez-vous Hello a plus de capacités que la stratégie d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="57a5d-137">hello sign-up or sign-in policy has more capabilities than hello sign-in policy.</span></span> <span data-ttu-id="57a5d-138">Aussi, il vous permet de personnalisation de l’interface utilisateur de page toouse et une meilleure prise en charge pour la localisation.</span><span class="sxs-lookup"><span data-stu-id="57a5d-138">It also enables you toouse page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="57a5d-139">stratégie d’authentification Hello est recommandé si vous n’avez pas besoin toolocalize vos stratégies, uniquement besoin des fonctionnalités de personnalisation secondaire pour la personnalisation et de mot de passe réinitialisation intégrée.</span><span class="sxs-lookup"><span data-stu-id="57a5d-139">hello sign-in policy is recommended if you don't need toolocalize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57a5d-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57a5d-140">Next steps</span></span>
* [<span data-ttu-id="57a5d-141">Configuration du jeton, de la session et de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="57a5d-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="57a5d-142">Désactiver la vérification par courrier électronique lors de l’inscription du consommateur</span><span class="sxs-lookup"><span data-stu-id="57a5d-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

