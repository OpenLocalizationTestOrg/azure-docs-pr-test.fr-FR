---
title: "aaaAdd tooa de connexion dans l’application web Node.js pour Azure B2C | Documents Microsoft"
description: "Comment toobuild une application web de Node.js qui se connecte les utilisateurs à l’aide d’un locataire B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="a6a67-103">Azure AD B2C : Ajouter l’application web connectez-vous tooa Node.js</span><span class="sxs-lookup"><span data-stu-id="a6a67-103">Azure AD B2C: Add sign-in tooa Node.js web app</span></span>

<span data-ttu-id="a6a67-104">**Passport** est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="a6a67-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="a6a67-105">Extrêmement flexible et modulaire, Passport peut être installé discrètement dans n’importe quelle application web basée sur Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="a6a67-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="a6a67-106">Une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter,etc.</span><span class="sxs-lookup"><span data-stu-id="a6a67-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="a6a67-107">Nous avons développé une stratégie pour Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a6a67-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a6a67-108">Vous allez installer ce module et puis ajoutez hello Azure AD `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="a6a67-108">You will install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="a6a67-109">toodo, vous devez :</span><span class="sxs-lookup"><span data-stu-id="a6a67-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="a6a67-110">Inscrivez une application en utilisant Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6a67-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="a6a67-111">Configurer votre hello de toouse application `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="a6a67-111">Set up your app toouse hello `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="a6a67-112">Utilisez Passport tooissue connectez-vous et demandes de déconnexion tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="a6a67-112">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="a6a67-113">Imprimez les données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a6a67-113">Print user data.</span></span>

<span data-ttu-id="a6a67-114">Hello du code pour ce didacticiel [est conservée sur GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="a6a67-114">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="a6a67-115">toofollow le long, vous pouvez [télécharger la structure de l’application hello sous forme de fichier .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="a6a67-115">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="a6a67-116">Vous pouvez également dupliquer le squelette de hello :</span><span class="sxs-lookup"><span data-stu-id="a6a67-116">You can also clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="a6a67-117">application Hello terminée est fournie à la fin de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a6a67-117">hello completed application is provided at hello end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="a6a67-118">Obtention d'un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a6a67-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="a6a67-119">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="a6a67-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="a6a67-120">Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc.</span><span class="sxs-lookup"><span data-stu-id="a6a67-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="a6a67-121">Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant d’aller plus loin dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="a6a67-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="a6a67-122">Création d'une application</span><span class="sxs-lookup"><span data-stu-id="a6a67-122">Create an application</span></span>

<span data-ttu-id="a6a67-123">Ensuite, vous devez toocreate une application dans votre répertoire B2C.</span><span class="sxs-lookup"><span data-stu-id="a6a67-123">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="a6a67-124">Cela fournit des informations de Azure AD lui toocommunicate en toute sécurité avec votre application.</span><span class="sxs-lookup"><span data-stu-id="a6a67-124">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="a6a67-125">Les deux hello application cliente et l’API web est représenté par un seul **ID de l’Application**, car ils constituent une seule application logique.</span><span class="sxs-lookup"><span data-stu-id="a6a67-125">Both hello client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="a6a67-126">toocreate une application, procédez comme [ces instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a6a67-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="a6a67-127">Veillez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a6a67-127">Be sure to:</span></span>

- <span data-ttu-id="a6a67-128">Inclure un **application web**/**web API** dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-128">Include a **web app**/**web API** in hello application.</span></span>
- <span data-ttu-id="a6a67-129">Entrez `http://localhost:3000/auth/openid/return` comme **URL de réponse**.</span><span class="sxs-lookup"><span data-stu-id="a6a67-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="a6a67-130">Il s’agit d’URL par défaut de hello pour cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="a6a67-130">It is hello default URL for this code sample.</span></span>
- <span data-ttu-id="a6a67-131">Créez une **clé secrète d’application** pour votre application et copiez-la.</span><span class="sxs-lookup"><span data-stu-id="a6a67-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="a6a67-132">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="a6a67-132">You will need it later.</span></span> <span data-ttu-id="a6a67-133">Notez que cette valeur doit toobe [XML échappé](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) avant de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="a6a67-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="a6a67-134">Hello de copie **ID d’Application** qui est attribué tooyour application.</span><span class="sxs-lookup"><span data-stu-id="a6a67-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="a6a67-135">Vous allez également en avoir besoin par la suite.</span><span class="sxs-lookup"><span data-stu-id="a6a67-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="a6a67-136">Création de vos stratégies</span><span class="sxs-lookup"><span data-stu-id="a6a67-136">Create your policies</span></span>

<span data-ttu-id="a6a67-137">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a6a67-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="a6a67-138">Cette application contient trois expériences liées à l’identité : l’inscription, la connexion et la connexion avec Facebook.</span><span class="sxs-lookup"><span data-stu-id="a6a67-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="a6a67-139">Vous devez toocreate cette stratégie de chaque type, comme décrit dans la [article de référence de stratégie](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="a6a67-139">You need toocreate this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="a6a67-140">Lors de la création de vos 3 stratégies, assurez-vous de :</span><span class="sxs-lookup"><span data-stu-id="a6a67-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="a6a67-141">Choisissez hello **nom d’affichage** et d’autres attributs d’inscription de votre stratégie d’inscription.</span><span class="sxs-lookup"><span data-stu-id="a6a67-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="a6a67-142">Choisissez hello **nom d’affichage** et **ID d’objet** revendications de l’application dans chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="a6a67-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="a6a67-143">Vous pouvez aussi choisir d'autres revendications.</span><span class="sxs-lookup"><span data-stu-id="a6a67-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="a6a67-144">Hello de copie **nom** de chaque stratégie après l’avoir créée.</span><span class="sxs-lookup"><span data-stu-id="a6a67-144">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="a6a67-145">Il doit avoir le préfixe de hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="a6a67-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="a6a67-146">Vous aurez besoin des noms de ces stratégies ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="a6a67-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="a6a67-147">Après avoir créé votre trois stratégies, vous êtes prêt toobuild votre application.</span><span class="sxs-lookup"><span data-stu-id="a6a67-147">After you create your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="a6a67-148">Notez que cet article ne couvre pas la façon dont les stratégies hello toouse vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="a6a67-148">Note that this article does not cover how toouse hello policies you just created.</span></span> <span data-ttu-id="a6a67-149">toolearn sur le fonctionnement des stratégies dans Azure AD B2C, commencer par hello [.NET web application mise en route didacticiel](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a6a67-149">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-tooyour-directory"></a><span data-ttu-id="a6a67-150">Ajouter un répertoire tooyour de conditions préalables</span><span class="sxs-lookup"><span data-stu-id="a6a67-150">Add prerequisites tooyour directory</span></span>

<span data-ttu-id="a6a67-151">À partir de la ligne de commande hello, modifiez le dossier racine du tooyour de répertoires, si vous n’êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="a6a67-151">From hello command line, change directories tooyour root folder, if you're not already there.</span></span> <span data-ttu-id="a6a67-152">Exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="a6a67-152">Run hello following commands:</span></span>

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

<span data-ttu-id="a6a67-153">En outre, nous avons utilisé `passport-azure-ad` pour notre version préliminaire dans squelette hello Hello démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="a6a67-153">In addition, we used `passport-azure-ad` for our preview in hello skeleton of hello Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="a6a67-154">Il installe les bibliothèques hello qui `passport-azure-ad` dépend.</span><span class="sxs-lookup"><span data-stu-id="a6a67-154">This will install hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a><span data-ttu-id="a6a67-155">Configurer votre hello de toouse application Node.js de Passport stratégie</span><span class="sxs-lookup"><span data-stu-id="a6a67-155">Set up your app toouse hello Passport-Node.js strategy</span></span>
<span data-ttu-id="a6a67-156">Configurer un intergiciel (middleware) d’Express Bonjour Bonjour toouse protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a6a67-156">Configure hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="a6a67-157">Passport est utilisé tooissue les demandes de connexion et déconnexion, gérer les sessions utilisateur et obtenir des informations sur les utilisateurs, entre autres.</span><span class="sxs-lookup"><span data-stu-id="a6a67-157">Passport will be used tooissue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="a6a67-158">Ouvrez hello `config.js` fichier racine hello du projet de hello et entrez les valeurs de configuration de votre application Bonjour `exports.creds` section.</span><span class="sxs-lookup"><span data-stu-id="a6a67-158">Open hello `config.js` file in hello root of hello project and enter your app's configuration values in hello `exports.creds` section.</span></span>
- <span data-ttu-id="a6a67-159">`clientID`: hello **ID d’Application** affecté application tooyour dans le portail de l’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-159">`clientID`: hello **Application ID** assigned tooyour app in hello registration portal.</span></span>
- <span data-ttu-id="a6a67-160">`returnURL`: hello **URI de redirection** vous avez entré dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-160">`returnURL`: hello **Redirect URI** you entered in hello portal.</span></span>
- <span data-ttu-id="a6a67-161">`tenantName`: nom du client de votre application, par exemple, hello **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="a6a67-161">`tenantName`: hello tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="a6a67-162">Ouvrez hello `app.js` dans fichier hello la racine du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-162">Open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="a6a67-163">Ajouter hello après appel tooinvoke hello `OIDCStrategy` stratégie qui est fourni avec `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="a6a67-163">Add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="a6a67-164">Utilisez stratégie hello vous référencé uniquement les demandes de connexion toohandle.</span><span class="sxs-lookup"><span data-stu-id="a6a67-164">Use hello strategy you just referenced toohandle sign-in requests.</span></span>

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
    process.nextTick(function () {
      findByEmail(profile.email, function(err, user) {
        if (err) {
          return done(err);
        }
        if (!user) {
          // "Auto-registration"
          users.push(profile);
          return done(null, profile);
        }
        return done(null, user);
      });
    });
  }
));
```
<span data-ttu-id="a6a67-165">Passport utilise un modèle similaire pour l’ensemble de ses stratégies (y compris Twitter et Facebook).</span><span class="sxs-lookup"><span data-stu-id="a6a67-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="a6a67-166">Tous les enregistreurs de stratégie respectent toothis modèle.</span><span class="sxs-lookup"><span data-stu-id="a6a67-166">All strategy writers adhere toothis pattern.</span></span> <span data-ttu-id="a6a67-167">Lorsque vous examinez la stratégie de hello, vous pouvez voir que vous lui passez un `function()` qui a un jeton et un `done` en tant que paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-167">When you look at hello strategy, you can see that you pass it a `function()` that has a token and a `done` as hello parameters.</span></span> <span data-ttu-id="a6a67-168">stratégie de Hello revient tooyou après que qu’il a terminé tout son travail.</span><span class="sxs-lookup"><span data-stu-id="a6a67-168">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="a6a67-169">Stocker les utilisateur hello et dissimuler les jeton hello afin que vous n’avez pas besoin tooask pour celle-ci à nouveau.</span><span class="sxs-lookup"><span data-stu-id="a6a67-169">Store hello user and stash hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="a6a67-170">Hello code précédent prend tous les utilisateurs auxquels hello serveur authentifie.</span><span class="sxs-lookup"><span data-stu-id="a6a67-170">hello preceding code takes all users whom hello server authenticates.</span></span> <span data-ttu-id="a6a67-171">C’est ce que l’on appelle l’enregistrement automatique.</span><span class="sxs-lookup"><span data-stu-id="a6a67-171">This is autoregistration.</span></span> <span data-ttu-id="a6a67-172">Lorsque vous utilisez des serveurs de production, vous ne souhaitez pas toolet dans les utilisateurs, sauf si elles sont passées par un processus d’inscription que vous avez définis.</span><span class="sxs-lookup"><span data-stu-id="a6a67-172">When you use production servers, you don’t want toolet in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="a6a67-173">C’est le modèle souvent utilisé dans les applications grand public.</span><span class="sxs-lookup"><span data-stu-id="a6a67-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="a6a67-174">Qui vous permettent de tooregister à l’aide de Facebook, mais, ils invite toofill des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a6a67-174">These allow you tooregister by using Facebook, but then they ask you toofill out additional information.</span></span> <span data-ttu-id="a6a67-175">Si notre application n’était pas un exemple, nous avons extraire une adresse de messagerie à partir de l’objet du jeton hello qui est retournée et puis demandez à toofill d’utilisateur hello des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a6a67-175">If our application wasn’t a sample, we could extract an email address from hello token object that is returned, and then ask hello user toofill out additional information.</span></span> <span data-ttu-id="a6a67-176">Comme il s’agit d’un serveur de test, nous suffit d’ajouter les utilisateurs toohello base de données.</span><span class="sxs-lookup"><span data-stu-id="a6a67-176">Because this is a test server, we simply add users toohello in-memory database.</span></span>

<span data-ttu-id="a6a67-177">Ajouter des méthodes hello qui permettent de suivre tookeep d’utilisateurs qui se sont connectés, comme requis par Passport.</span><span class="sxs-lookup"><span data-stu-id="a6a67-177">Add hello methods that allow you tookeep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="a6a67-178">Cela inclut la sérialisation et la désérialisation des informations des utilisateurs :</span><span class="sxs-lookup"><span data-stu-id="a6a67-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
var users = [];

var findByEmail = function(email, fn) {
  for (var i = 0, len = users.length; i < len; i++) {
    var user = users[i];
    log.info('we are using user: ', user);
    if (user.email === email) {
      return fn(null, user);
    }
  }
  return fn(null, null);
};

```

<span data-ttu-id="a6a67-179">Ajoutez le moteur Express hello hello code tooload.</span><span class="sxs-lookup"><span data-stu-id="a6a67-179">Add hello code tooload hello Express engine.</span></span> <span data-ttu-id="a6a67-180">Dans les éléments suivants de hello, vous pouvez voir que nous utilisons par défaut de hello `/views` et `/routes` modèle Express fournit.</span><span class="sxs-lookup"><span data-stu-id="a6a67-180">In hello following, you can see that we use hello default `/views` and `/routes` pattern that Express provides.</span></span>

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="a6a67-181">Ajouter hello `POST` itinéraires remettre hello toohello de demandes de connexion réel `passport-azure-ad` moteur :</span><span class="sxs-lookup"><span data-stu-id="a6a67-181">Add hello `POST` routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="a6a67-182">Utilisez Passport tooissue connectez-vous et demandes de déconnexion tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="a6a67-182">Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>

<span data-ttu-id="a6a67-183">Votre application est maintenant toocommunicate correctement configurée avec un point de terminaison hello v2.0 à l’aide du protocole d’authentification OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-183">Your app is now properly configured toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="a6a67-184">`passport-azure-ad`a prise en charge des détails de hello d’élaborer des messages d’authentification, la validation des jetons d’Azure AD et la gestion de session utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a6a67-184">`passport-azure-ad` has taken care of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="a6a67-185">Tout ce qui reste est toogive vos utilisateurs un toosign moyen dans et les signer hors et toogather plus d’informations sur les utilisateurs qui sont connectés.</span><span class="sxs-lookup"><span data-stu-id="a6a67-185">All that remains is toogive your users a way toosign in and sign out, and toogather additional information on users who have signed in.</span></span>

<span data-ttu-id="a6a67-186">Ajoutez d’abord par défaut de hello, connectez-vous, compte et méthodes déconnexion tooyour `app.js` fichier :</span><span class="sxs-lookup"><span data-stu-id="a6a67-186">First, add hello default, sign-in, account, and sign-out methods tooyour `app.js` file:</span></span>

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in hello Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="a6a67-187">tooreview ces méthodes en détail :</span><span class="sxs-lookup"><span data-stu-id="a6a67-187">tooreview these methods in detail:</span></span>
- <span data-ttu-id="a6a67-188">Hello `/` itinéraire redirige toohello `index.ejs` vue en passant l’utilisateur de hello dans la demande hello (s’il existe).</span><span class="sxs-lookup"><span data-stu-id="a6a67-188">hello `/` route redirects toohello `index.ejs` view by passing hello user in hello request (if it exists).</span></span>
- <span data-ttu-id="a6a67-189">Hello `/account` itinéraire vérifie d’abord que vous êtes authentifié (hello mise en œuvre pour cette figure ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="a6a67-189">hello `/account` route first verifies that you are authenticated (hello implementation for this is below).</span></span> <span data-ttu-id="a6a67-190">Il passe ensuite les utilisateur hello dans la demande hello qui vous pouvez d’obtenir des informations supplémentaires sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-190">It then passes hello user in hello request so that you can get additional information about hello user.</span></span>
- <span data-ttu-id="a6a67-191">Hello `/login` itinéraire appels hello `azuread-openidconnect` authentificateur de `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="a6a67-191">hello `/login` route calls hello `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="a6a67-192">S’il ne réussit pas, les itinéraires hello redirige l’utilisateur hello trop`/login`.</span><span class="sxs-lookup"><span data-stu-id="a6a67-192">If it doesn't succeed, hello route redirects hello user back too`/login`.</span></span>
- <span data-ttu-id="a6a67-193">`/logout` appelle simplement `logout.ejs` (et son itinéraire).</span><span class="sxs-lookup"><span data-stu-id="a6a67-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="a6a67-194">Cela efface les cookies et puis retourne hello utilisateur trop`index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="a6a67-194">This clears cookies and then returns hello user back too`index.ejs`.</span></span>


<span data-ttu-id="a6a67-195">Pour la dernière partie de hello de `app.js`, ajouter hello `EnsureAuthenticated` méthode qui est utilisée dans hello `/account` itinéraire.</span><span class="sxs-lookup"><span data-stu-id="a6a67-195">For hello last part of `app.js`, add hello `EnsureAuthenticated` method that is used in hello `/account` route.</span></span>

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="a6a67-196">Enfin, créez le serveur hello lui-même dans `app.js`.</span><span class="sxs-lookup"><span data-stu-id="a6a67-196">Finally, create hello server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a><span data-ttu-id="a6a67-197">Créer des vues hello et achemine dans Express toocall vos stratégies</span><span class="sxs-lookup"><span data-stu-id="a6a67-197">Create hello views and routes in Express toocall your policies</span></span>

<span data-ttu-id="a6a67-198">La création du fichier `app.js` est maintenant terminée.</span><span class="sxs-lookup"><span data-stu-id="a6a67-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="a6a67-199">Vous devez simplement les itinéraires de hello tooadd et vues que vous autorisent des stratégies d’ouverture de session et d’inscription toocall hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-199">You just need tooadd hello routes and views that allow you toocall hello sign-in and sign-up policies.</span></span> <span data-ttu-id="a6a67-200">Ils gèrent également hello `/logout` et `/login` itinéraires que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="a6a67-200">These also handle hello `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="a6a67-201">Créer hello `/routes/index.js` itinéraire sous le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-201">Create hello `/routes/index.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="a6a67-202">Créer hello `/routes/user.js` itinéraire sous le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-202">Create hello `/routes/user.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="a6a67-203">Vues de demandes tooyour transmettez ces itinéraires simples.</span><span class="sxs-lookup"><span data-stu-id="a6a67-203">These simple routes pass along requests tooyour views.</span></span> <span data-ttu-id="a6a67-204">Ils comprennent les utilisateur hello, s’il en existe.</span><span class="sxs-lookup"><span data-stu-id="a6a67-204">They include hello user, if one is present.</span></span>

<span data-ttu-id="a6a67-205">Créer hello `/views/index.ejs` sous le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-205">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="a6a67-206">Il s’agit d’une page simple qui appelle des stratégies de connexion et de déconnexion. Vous pouvez également l’utiliser toograb les informations de compte.</span><span class="sxs-lookup"><span data-stu-id="a6a67-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it toograb account information.</span></span> <span data-ttu-id="a6a67-207">Notez que vous pouvez utiliser hello conditionnel `if (!user)` comme utilisateur de hello est passé par le biais de demande hello tooprovide preuve que l’utilisateur hello est connecté.</span><span class="sxs-lookup"><span data-stu-id="a6a67-207">Note that you can use hello conditional `if (!user)` as hello user is passed through in hello request tooprovide evidence that hello user is signed in.</span></span>

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

<span data-ttu-id="a6a67-208">Créer hello `/views/account.ejs` afficher sous le répertoire racine de hello afin que vous pouvez afficher des informations supplémentaires qui `passport-azure-ad` placé dans la demande de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="a6a67-208">Create hello `/views/account.ejs` view under hello root directory so that you can view additional information that `passport-azure-ad` put in hello user request.</span></span>

```Javascript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login">Sign in</a>
<% } else { %>
<p>displayName: <%= user.displayName %></p>
<p>givenName: <%= user.name.givenName %></p>
<p>familyName: <%= user.name.familyName %></p>
<p>UPN: <%= user._json.upn %></p>
<p>Profile ID: <%= user.id %></p>
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

<span data-ttu-id="a6a67-209">Vous pouvez maintenant créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="a6a67-209">You can now build and run your app.</span></span>

<span data-ttu-id="a6a67-210">Exécutez `node app.js` et accédez trop`http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="a6a67-210">Run `node app.js` and navigate too`http://localhost:3000`</span></span>


<span data-ttu-id="a6a67-211">S’inscrire ou se connecter à l’aide de messages électroniques ou Facebook toohello application.</span><span class="sxs-lookup"><span data-stu-id="a6a67-211">Sign up or sign in toohello app by using email or Facebook.</span></span> <span data-ttu-id="a6a67-212">Déconnectez-vous, puis reconnectez-vous comme si vous étiez un autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a6a67-212">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="a6a67-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a6a67-213">Next steps</span></span>

<span data-ttu-id="a6a67-214">Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie comme un fichier .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a6a67-214">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="a6a67-215">Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="a6a67-215">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="a6a67-216">Vous pouvez maintenant passer toomore rubriques avancées.</span><span class="sxs-lookup"><span data-stu-id="a6a67-216">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="a6a67-217">Vous pouvez essayer :</span><span class="sxs-lookup"><span data-stu-id="a6a67-217">You might try:</span></span>

[<span data-ttu-id="a6a67-218">Sécuriser une API web à l’aide du modèle de hello B2C dans Node.js</span><span class="sxs-lookup"><span data-stu-id="a6a67-218">Secure a web API by using hello B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
