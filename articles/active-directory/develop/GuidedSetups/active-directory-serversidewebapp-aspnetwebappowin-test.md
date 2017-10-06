---
title: aaaAzure AD v2 ASP.NET Web Server mise en route - Test | Documents Microsoft
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
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="22b8b-103">Test de votre code</span><span class="sxs-lookup"><span data-stu-id="22b8b-103">Test your code</span></span>

<span data-ttu-id="22b8b-104">Appuyez sur `F5` toorun votre projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22b8b-104">Press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="22b8b-105">Hello navigateur s’ouvre et vous diriger trop*http://localhost : {port}* où vous verrez hello *connectez-vous avec Microsoft* bouton.</span><span class="sxs-lookup"><span data-stu-id="22b8b-105">hello browser will open and direct you too*http://localhost:{port}* where you’ll see hello *Sign in with Microsoft* button.</span></span> <span data-ttu-id="22b8b-106">Continuez et cliquez dessus toosign dans.</span><span class="sxs-lookup"><span data-stu-id="22b8b-106">Go ahead and click it toosign in.</span></span>

<span data-ttu-id="22b8b-107">Lorsque vous êtes prêt tootest, utilisez toosign dans le compte professionnel ou scolaire (Azure Active Directory) ou personnelle (live.com, outlook.com).</span><span class="sxs-lookup"><span data-stu-id="22b8b-107">When you're ready tootest, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account toosign in.</span></span> 

![Connexion à l’aide de la fenêtre de navigateur Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Connexion à l’aide de la fenêtre de navigateur Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="22b8b-110">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="22b8b-110">Expected results</span></span>
<span data-ttu-id="22b8b-111">Après la connexion, utilisateur de hello est redirigé toohello page d’accueil de votre site web qui est hello URL HTTPS spécifié dans votre application d’enregistrement de hello portail de l’enregistrement des applications Microsoft.</span><span class="sxs-lookup"><span data-stu-id="22b8b-111">After sign-in, hello user is redirected toohello home page of your web site which is hello HTTPS URL specified in your application registration information in hello Microsoft Application Registration Portal.</span></span> <span data-ttu-id="22b8b-112">Cette page affiche maintenant *Hello {User}* et une lien toosign montée et revendications de lien toosee hello d’un utilisateur : qui est un contrôleur de Authorize toohello lien créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="22b8b-112">This page now shows *Hello {User}* and a link toosign-out, and a link toosee hello user’s claims – which is a link toohello Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="22b8b-113">Afficher les revendications de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="22b8b-113">See user's claims</span></span>
<span data-ttu-id="22b8b-114">Sélectionnez l’utilisateur hello hello hyperlink toosee.</span><span class="sxs-lookup"><span data-stu-id="22b8b-114">Select hello hyperlink toosee hello user's claims.</span></span> <span data-ttu-id="22b8b-115">Cela nous mène toohello contrôleur et la vue qui est uniquement disponible toousers qui sont authentifiés.</span><span class="sxs-lookup"><span data-stu-id="22b8b-115">This leads you toohello controller and view that is only available toousers that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="22b8b-116">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="22b8b-116">Expected results</span></span>
 <span data-ttu-id="22b8b-117">Vous devez voir une table qui contient les propriétés de base hello d’utilisateur de hello connecté :</span><span class="sxs-lookup"><span data-stu-id="22b8b-117">You should see a table containing hello basic properties of hello logged user:</span></span>

| <span data-ttu-id="22b8b-118">Propriété</span><span class="sxs-lookup"><span data-stu-id="22b8b-118">Property</span></span> | <span data-ttu-id="22b8b-119">Valeur</span><span class="sxs-lookup"><span data-stu-id="22b8b-119">Value</span></span> | <span data-ttu-id="22b8b-120">Description</span><span class="sxs-lookup"><span data-stu-id="22b8b-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="22b8b-121">Nom</span><span class="sxs-lookup"><span data-stu-id="22b8b-121">Name</span></span> | <span data-ttu-id="22b8b-122">{Nom complet de l’utilisateur}</span><span class="sxs-lookup"><span data-stu-id="22b8b-122">{User Full Name}</span></span> | <span data-ttu-id="22b8b-123">utilisateur de Hello prénom et nom</span><span class="sxs-lookup"><span data-stu-id="22b8b-123">hello user’s first and last name</span></span>
|<span data-ttu-id="22b8b-124">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="22b8b-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="22b8b-125">nom d’utilisateur Hello utilisé utilisateur hello connecté de tooidentify</span><span class="sxs-lookup"><span data-stu-id="22b8b-125">hello username used tooidentify hello logged user</span></span>
| <span data-ttu-id="22b8b-126">Objet</span><span class="sxs-lookup"><span data-stu-id="22b8b-126">Subject</span></span>| <span data-ttu-id="22b8b-127">{Objet}</span><span class="sxs-lookup"><span data-stu-id="22b8b-127">{Subject}</span></span>|<span data-ttu-id="22b8b-128">Une chaîne de toouniquely identifier d’ouverture de session utilisateur hello sur le web de hello</span><span class="sxs-lookup"><span data-stu-id="22b8b-128">A string toouniquely identify hello user logon across hello web</span></span>|
| <span data-ttu-id="22b8b-129">ID client</span><span class="sxs-lookup"><span data-stu-id="22b8b-129">Tenant ID</span></span>| <span data-ttu-id="22b8b-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="22b8b-130">{Guid}</span></span>| <span data-ttu-id="22b8b-131">A *guid* toouniquely représentent l’organisation Azure Active Directory de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="22b8b-131">A *guid* toouniquely represent hello user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="22b8b-132">En outre, vous verrez une table contenant toutes les revendications de l’utilisateur incluses dans la demande d’authentification.</span><span class="sxs-lookup"><span data-stu-id="22b8b-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="22b8b-133">Pour obtenir la liste des revendications dans un jeton d’ID et des informations complémentaires, consultez l’[article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Liste des revendications dans un jeton d’ID").</span><span class="sxs-lookup"><span data-stu-id="22b8b-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="22b8b-134">Test de l’accès à une méthode disposant d’un attribut *[Authorize]* (facultatif)</span><span class="sxs-lookup"><span data-stu-id="22b8b-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="22b8b-135">Dans cette étape, vous allez tester l’accès au contrôleur d’authentifié hello en tant qu’utilisateur anonyme :</span><span class="sxs-lookup"><span data-stu-id="22b8b-135">In this step, you will test accessing hello Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="22b8b-136">Sélectionnez hello lier toosign montée hello un utilisateur et les processus de déconnexion hello terminée.</span><span class="sxs-lookup"><span data-stu-id="22b8b-136">Select hello link toosign-out hello user and complete hello sign-out process.</span></span><br/>
<span data-ttu-id="22b8b-137">Désormais, dans votre navigateur, tapez http://localhost : {port} / authentifié tooaccess votre contrôleur qui est protégé par hello `[Authorize]` attribut</span><span class="sxs-lookup"><span data-stu-id="22b8b-137">Now in your browser, type http://localhost:{port}/authenticated tooaccess your controller that is protected with hello `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="22b8b-138">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="22b8b-138">Expected results</span></span>
<span data-ttu-id="22b8b-139">Vous devez recevoir le message hello vous demandant de vue de hello tooauthenticate toosee.</span><span class="sxs-lookup"><span data-stu-id="22b8b-139">You should receive hello prompt requiring you tooauthenticate toosee hello view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="22b8b-140">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="22b8b-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="22b8b-141">Protéger l’ensemble de votre site web</span><span class="sxs-lookup"><span data-stu-id="22b8b-141">Protect your entire web site</span></span>
<span data-ttu-id="22b8b-142">tooprotect votre site web, ajoutez hello `AuthorizeAttribute` trop`GlobalFilters` dans `Global.asax` `Application_Start` méthode :</span><span class="sxs-lookup"><span data-stu-id="22b8b-142">tooprotect your entire web site, add hello `AuthorizeAttribute` too`GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="22b8b-143">**Comment toorestrict les utilisateurs à partir de toosign qu’une organisation dans l’application de tooyour**</span><span class="sxs-lookup"><span data-stu-id="22b8b-143">**How toorestrict users from only one organization toosign in tooyour application**</span></span>

> <span data-ttu-id="22b8b-144">Par défaut, des comptes personnels (y compris outlook.com, live.com et autres), ainsi que des comptes professionnels et scolaires à partir de toute entreprise ou d’une organisation qui a intégré à Azure Active Directory peuvent se connecter au tooyour application.</span><span class="sxs-lookup"><span data-stu-id="22b8b-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in tooyour application.</span></span> 

> <span data-ttu-id="22b8b-145">Si vous souhaitez que votre application tooaccept connexions à partir d’une seule organisation Azure Active Directory, remplacez hello `Tenant` paramètre dans *web.config* de `Common` toohello nom du client de l’organisation de hello – exemple, *contoso.onmicrosoft.com*. Après cela, modifiez hello `ValidateIssuer` argument dans votre *classe de démarrage OWIN* trop`true`.</span><span class="sxs-lookup"><span data-stu-id="22b8b-145">If you want your application tooaccept sign-ins from only one Azure Active Directory organization, replace hello `Tenant` parameter in *web.config* from `Common` toohello tenant name of hello organization – example, *contoso.onmicrosoft.com*. After that, change hello `ValidateIssuer` argument in your *OWIN Startup class* too`true`.</span></span>

> <span data-ttu-id="22b8b-146">tooallow des utilisateurs à partir d’une liste d’organisations spécifiques, définissez `ValidateIssuer` tootrue et utilisation hello `ValidIssuers` paramètre toospecify une liste des organisations.</span><span class="sxs-lookup"><span data-stu-id="22b8b-146">tooallow users from only a list of specific organizations, set `ValidateIssuer` tootrue and use hello `ValidIssuers` parameter toospecify a list of organizations.</span></span>

> <span data-ttu-id="22b8b-147">Une autre option est une méthode personnalisée de tooimplement émetteurs de hello toovalidate à l’aide du paramètre de IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="22b8b-147">Another option is tooimplement a custom method toovalidate hello issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="22b8b-148">Pour en savoir plus sur `TokenValidationParameters`, consultez [l’](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "article MSDN sur la propriété TokenValidationParameters").</span><span class="sxs-lookup"><span data-stu-id="22b8b-148">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

