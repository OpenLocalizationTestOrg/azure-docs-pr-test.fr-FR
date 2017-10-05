---
title: "Prise en main d’Azure AD v2 avec les applications de serveur web ASP.NET - Test | Microsoft Docs"
description: "Implémentation de la connexion Microsoft dans une solution ASP.NET avec une application basée sur un navigateur web traditionnel utilisant le standard OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 00cb963e85111274c36c3a84489894811ad2dabd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="19357-103">Test de votre code</span><span class="sxs-lookup"><span data-stu-id="19357-103">Test your code</span></span>

<span data-ttu-id="19357-104">Appuyez sur `F5` pour exécuter votre projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19357-104">Press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="19357-105">Le navigateur s’ouvre et vous redirige vers *http://localhost:{port}* où vous pouvez voir le bouton *Se connecter avec Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="19357-105">The browser will open and direct you to *http://localhost:{port}* where you’ll see the *Sign in with Microsoft* button.</span></span> <span data-ttu-id="19357-106">Continuez et cliquez dessus pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="19357-106">Go ahead and click it to sign in.</span></span>

<span data-ttu-id="19357-107">Lorsque vous êtes prêt à procéder au test, utilisez un compte professionnel ou scolaire (Azure Active Directory) ou un compte personnel (live.com, outlook.com) pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="19357-107">When you're ready to test, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account to sign in.</span></span> 

![Connexion à l’aide de la fenêtre de navigateur Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Connexion à l’aide de la fenêtre de navigateur Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="19357-110">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="19357-110">Expected results</span></span>
<span data-ttu-id="19357-111">Après la connexion, l’utilisateur est redirigé vers la page d’accueil de votre site web qui est l’URL HTTPS spécifiée dans les informations d’inscription de votre application sur le portail d’inscription des applications de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19357-111">After sign-in, the user is redirected to the home page of your web site which is the HTTPS URL specified in your application registration information in the Microsoft Application Registration Portal.</span></span> <span data-ttu-id="19357-112">Cette page affiche désormais *Bonjour {utilisateur}*, ainsi qu’un lien de déconnexion et un lien pour afficher les revendications de l’utilisateur, qui est un lien vers le contrôleur d’autorisation créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="19357-112">This page now shows *Hello {User}* and a link to sign-out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="19357-113">Afficher les revendications de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="19357-113">See user's claims</span></span>
<span data-ttu-id="19357-114">Sélectionnez le lien hypertexte pour afficher les revendications de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="19357-114">Select the hyperlink to see the user's claims.</span></span> <span data-ttu-id="19357-115">Cela vous permet d’accéder au contrôleur et à la vue qui est uniquement disponible pour les utilisateurs authentifiés.</span><span class="sxs-lookup"><span data-stu-id="19357-115">This leads you to the controller and view that is only available to users that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="19357-116">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="19357-116">Expected results</span></span>
 <span data-ttu-id="19357-117">Vous devez voir une table contenant les propriétés de base de l’utilisateur connecté :</span><span class="sxs-lookup"><span data-stu-id="19357-117">You should see a table containing the basic properties of the logged user:</span></span>

| <span data-ttu-id="19357-118">Propriété</span><span class="sxs-lookup"><span data-stu-id="19357-118">Property</span></span> | <span data-ttu-id="19357-119">Valeur</span><span class="sxs-lookup"><span data-stu-id="19357-119">Value</span></span> | <span data-ttu-id="19357-120">Description</span><span class="sxs-lookup"><span data-stu-id="19357-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="19357-121">Nom</span><span class="sxs-lookup"><span data-stu-id="19357-121">Name</span></span> | <span data-ttu-id="19357-122">{Nom complet de l’utilisateur}</span><span class="sxs-lookup"><span data-stu-id="19357-122">{User Full Name}</span></span> | <span data-ttu-id="19357-123">Prénom et nom de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="19357-123">The user’s first and last name</span></span>
|<span data-ttu-id="19357-124">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="19357-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="19357-125">Nom d’utilisateur employé pour identifier l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="19357-125">The username used to identify the logged user</span></span>
| <span data-ttu-id="19357-126">Objet</span><span class="sxs-lookup"><span data-stu-id="19357-126">Subject</span></span>| <span data-ttu-id="19357-127">{Objet}</span><span class="sxs-lookup"><span data-stu-id="19357-127">{Subject}</span></span>|<span data-ttu-id="19357-128">Une chaîne pour identifier de façon unique l’ouverture de session utilisateur sur le web.</span><span class="sxs-lookup"><span data-stu-id="19357-128">A string to uniquely identify the user logon across the web</span></span>|
| <span data-ttu-id="19357-129">ID client</span><span class="sxs-lookup"><span data-stu-id="19357-129">Tenant ID</span></span>| <span data-ttu-id="19357-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="19357-130">{Guid}</span></span>| <span data-ttu-id="19357-131">Un *GUID* qui identifie l’organisation Azure Active Directory de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="19357-131">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="19357-132">En outre, vous verrez une table contenant toutes les revendications de l’utilisateur incluses dans la demande d’authentification.</span><span class="sxs-lookup"><span data-stu-id="19357-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="19357-133">Pour obtenir la liste des revendications dans un jeton d’ID et des informations complémentaires, consultez l’[article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Liste des revendications dans un jeton d’ID").</span><span class="sxs-lookup"><span data-stu-id="19357-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="19357-134">Test de l’accès à une méthode disposant d’un attribut *[Authorize]* (facultatif)</span><span class="sxs-lookup"><span data-stu-id="19357-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="19357-135">Dans cette étape, vous allez tester l’accès au contrôleur authentifié en tant qu’utilisateur anonyme :</span><span class="sxs-lookup"><span data-stu-id="19357-135">In this step, you will test accessing the Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="19357-136">Sélectionnez le lien de déconnexion de l’utilisateur et terminez le processus de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="19357-136">Select the link to sign-out the user and complete the sign-out process.</span></span><br/>
<span data-ttu-id="19357-137">À présent, dans votre navigateur, saisissez http://localhost:{port}/authenticated pour accéder à votre contrôleur qui est protégé par l’attribut `[Authorize]`.</span><span class="sxs-lookup"><span data-stu-id="19357-137">Now in your browser, type http://localhost:{port}/authenticated to access your controller that is protected with the `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="19357-138">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="19357-138">Expected results</span></span>
<span data-ttu-id="19357-139">Vous devriez recevoir l’invite vous demandant de vous authentifier pour afficher la vue.</span><span class="sxs-lookup"><span data-stu-id="19357-139">You should receive the prompt requiring you to authenticate to see the view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="19357-140">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="19357-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="19357-141">Protéger l’ensemble de votre site web</span><span class="sxs-lookup"><span data-stu-id="19357-141">Protect your entire web site</span></span>
<span data-ttu-id="19357-142">Pour protéger l’ensemble de votre site web, ajoutez `AuthorizeAttribute` à `GlobalFilters` dans la méthode `Global.asax` `Application_Start` :</span><span class="sxs-lookup"><span data-stu-id="19357-142">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="19357-143">**Autoriser uniquement les utilisateurs d’une seule organisation à se connecter à votre application**</span><span class="sxs-lookup"><span data-stu-id="19357-143">**How to restrict users from only one organization to sign in to your application**</span></span>

> <span data-ttu-id="19357-144">Votre application accepte par défaut des connexions de comptes personnels (y compris outlook.com, live.com et autres), ainsi que des comptes professionnels et scolaires de n’importe quelle société ou organisation ayant intégré Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="19357-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in to your application.</span></span> 

> <span data-ttu-id="19357-145">Si vous souhaitez que votre application accepte uniquement les connexions à partir d’une seule organisation Azure Active Directory, remplacez le paramètre `Tenant` dans *web.config* défini sur `Common` par le nom du client de l’organisation, par exemple *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="19357-145">If you want your application to accept sign-ins from only one Azure Active Directory organization, replace the `Tenant` parameter in *web.config* from `Common` to the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span></span> <span data-ttu-id="19357-146">Ensuite, définissez l’argument `ValidateIssuer` dans votre *classe de démarrage OWIN* sur `true`.</span><span class="sxs-lookup"><span data-stu-id="19357-146">After that, change the `ValidateIssuer` argument in your *OWIN Startup class* to `true`.</span></span>

> <span data-ttu-id="19357-147">Pour autoriser uniquement les utilisateurs de certaines organisations à se connecter, définissez `ValidateIssuer` sur true et utilisez le paramètre `ValidIssuers` pour créer une liste d’organisations.</span><span class="sxs-lookup"><span data-stu-id="19357-147">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span></span>

> <span data-ttu-id="19357-148">Une autre option consiste à implémenter une méthode personnalisée pour valider les émetteurs à l’aide du paramètre IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="19357-148">Another option is to implement a custom method to validate the issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="19357-149">Pour en savoir plus sur `TokenValidationParameters`, consultez [l’](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "article MSDN sur la propriété TokenValidationParameters").</span><span class="sxs-lookup"><span data-stu-id="19357-149">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

