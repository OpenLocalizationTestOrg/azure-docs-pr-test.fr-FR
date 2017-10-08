---
title: "Azure AD B2C : sécuriser une API web à l’aide de Node.js | Microsoft Docs"
description: "Comment toobuild un Node.js web API qui accepte les jetons provenant d’un locataire B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="4faf7-103">Azure AD B2C : sécuriser une API web à l’aide de Node.js</span><span class="sxs-lookup"><span data-stu-id="4faf7-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="4faf7-104">Avec Azure Active Directory (Azure AD) B2C, vous pouvez sécuriser une API web à l’aide de jetons d’accès OAuth 2.0,</span><span class="sxs-lookup"><span data-stu-id="4faf7-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="4faf7-105">Ces jetons permettent à vos applications clientes qui utilisent Azure AD B2C tooauthenticate toohello API.</span><span class="sxs-lookup"><span data-stu-id="4faf7-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="4faf7-106">Cet article vous explique comment toocreate une API de la « liste des tâches » qui permet aux utilisateurs tooadd et liste des tâches.</span><span class="sxs-lookup"><span data-stu-id="4faf7-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="4faf7-107">Hello web API est sécurisé à l’aide d’Azure AD B2C et autorise uniquement les utilisateurs authentifiés toomanage leur liste de tâches.</span><span class="sxs-lookup"><span data-stu-id="4faf7-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="4faf7-108">Cet exemple a été écrit à l’aide de tooby toobe connecté notre [iOS B2C exemple d’application](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="4faf7-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="4faf7-109">Hello en cours de la procédure tout d’abord, puis suivez avec cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4faf7-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="4faf7-110">**Passport** est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="4faf7-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="4faf7-111">Flexible et modulaire, Passport peut être installé discrètement dans toute application web basée sur Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="4faf7-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="4faf7-112">Une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter,etc.</span><span class="sxs-lookup"><span data-stu-id="4faf7-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="4faf7-113">Nous avons développé une stratégie pour Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4faf7-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="4faf7-114">Vous installez ce module et que vous ajoutez ensuite hello Azure AD `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="4faf7-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="4faf7-115">toodo cet exemple, vous devez :</span><span class="sxs-lookup"><span data-stu-id="4faf7-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="4faf7-116">inscrivez une application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="4faf7-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="4faf7-117">Configurer votre application toouse Passport `azure-ad-passport` plug-in.</span><span class="sxs-lookup"><span data-stu-id="4faf7-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="4faf7-118">Configurer une client application toocall hello « liste de tâches » API web.</span><span class="sxs-lookup"><span data-stu-id="4faf7-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="4faf7-119">Obtention d'un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="4faf7-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="4faf7-120">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="4faf7-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="4faf7-121">Un répertoire est un conteneur destiné à recevoir tous les utilisateurs, applications, groupes et autres.</span><span class="sxs-lookup"><span data-stu-id="4faf7-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="4faf7-122">Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="4faf7-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="4faf7-123">Création d'une application</span><span class="sxs-lookup"><span data-stu-id="4faf7-123">Create an application</span></span>
<span data-ttu-id="4faf7-124">Ensuite, vous devez toocreate une application dans votre répertoire B2C qui donne à Azure AD des informations qu’il doit toosecurely communiquer avec votre application.</span><span class="sxs-lookup"><span data-stu-id="4faf7-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="4faf7-125">Dans ce cas, application de client hello et API web sont représentés par un seul **ID de l’Application**, car ils constituent une seule application logique.</span><span class="sxs-lookup"><span data-stu-id="4faf7-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="4faf7-126">toocreate une application, procédez comme [ces instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="4faf7-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="4faf7-127">Veillez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4faf7-127">Be sure to:</span></span>

* <span data-ttu-id="4faf7-128">Inclure un **web web/de l’application api** dans l’application hello</span><span class="sxs-lookup"><span data-stu-id="4faf7-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="4faf7-129">Entrez `http://localhost/TodoListService` comme **URL de réponse**.</span><span class="sxs-lookup"><span data-stu-id="4faf7-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="4faf7-130">Il s’agit d’URL par défaut de hello pour cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="4faf7-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="4faf7-131">Créez une **clé secrète d’application** pour votre application et copiez-la.</span><span class="sxs-lookup"><span data-stu-id="4faf7-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="4faf7-132">Vous aurez besoin de cette donnée ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="4faf7-132">You need this data later.</span></span> <span data-ttu-id="4faf7-133">Notez que cette valeur doit toobe [XML échappé](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) avant de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="4faf7-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="4faf7-134">Hello de copie **ID d’Application** qui est attribué tooyour application.</span><span class="sxs-lookup"><span data-stu-id="4faf7-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="4faf7-135">Vous aurez besoin de cette donnée ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="4faf7-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="4faf7-136">Création de vos stratégies</span><span class="sxs-lookup"><span data-stu-id="4faf7-136">Create your policies</span></span>
<span data-ttu-id="4faf7-137">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4faf7-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4faf7-138">Cette application contient deux expériences d’identité : l’inscription et la connexion.</span><span class="sxs-lookup"><span data-stu-id="4faf7-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="4faf7-139">Vous devez toocreate une stratégie de chaque type, comme décrit dans la [article de référence de stratégie](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="4faf7-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="4faf7-140">Lors de la création de vos 3 stratégies, assurez-vous de :</span><span class="sxs-lookup"><span data-stu-id="4faf7-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="4faf7-141">Choisissez hello **nom d’affichage** et d’autres attributs d’inscription de votre stratégie d’inscription.</span><span class="sxs-lookup"><span data-stu-id="4faf7-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="4faf7-142">Choisissez hello **nom d’affichage** et **ID d’objet** revendications de l’application dans chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="4faf7-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="4faf7-143">Vous pouvez aussi choisir d'autres revendications.</span><span class="sxs-lookup"><span data-stu-id="4faf7-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="4faf7-144">Copie vers le bas hello **nom** de chaque stratégie après l’avoir créée.</span><span class="sxs-lookup"><span data-stu-id="4faf7-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="4faf7-145">Il doit avoir le préfixe de hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="4faf7-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="4faf7-146">Vous aurez besoin des noms de ces stratégies ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="4faf7-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="4faf7-147">Après avoir créé votre trois stratégies, vous êtes prêt toobuild votre application.</span><span class="sxs-lookup"><span data-stu-id="4faf7-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="4faf7-148">toolearn sur le fonctionnement des stratégies dans Azure AD B2C, commencer par hello [.NET web application mise en route didacticiel](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4faf7-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="4faf7-149">Télécharger le code de hello</span><span class="sxs-lookup"><span data-stu-id="4faf7-149">Download hello code</span></span>
<span data-ttu-id="4faf7-150">Hello du code pour ce didacticiel [est conservée sur GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="4faf7-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="4faf7-151">exemple de hello toobuild en tant que vous accédez, vous pouvez [télécharger un projet sous forme de fichier .zip de squelette](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="4faf7-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="4faf7-152">Vous pouvez également dupliquer le squelette de hello :</span><span class="sxs-lookup"><span data-stu-id="4faf7-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="4faf7-153">application Hello terminée est également [disponible sous forme de fichier .zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) ou sur hello `complete` branche Hello même référentiel.</span><span class="sxs-lookup"><span data-stu-id="4faf7-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="4faf7-154">Télécharger Node.js pour votre plateforme</span><span class="sxs-lookup"><span data-stu-id="4faf7-154">Download Node.js for your platform</span></span>
<span data-ttu-id="4faf7-155">toosuccessfully utiliser cet exemple, vous avez besoin d’une installation active de Node.js.</span><span class="sxs-lookup"><span data-stu-id="4faf7-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="4faf7-156">Installez Node.js à partir de [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="4faf7-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="4faf7-157">Installer MongoDB pour votre plateforme</span><span class="sxs-lookup"><span data-stu-id="4faf7-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="4faf7-158">toosuccessfully utiliser cet exemple, vous avez besoin d’une installation active de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4faf7-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="4faf7-159">Nous utilisons MongoDB toomake de votre API REST persistant entre les instances de serveur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="4faf7-160">Installez MongoDB à partir de [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="4faf7-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="4faf7-161">Cette procédure pas à pas suppose que vous utilisez des points de terminaison hello par défaut installation et le serveur pour MongoDB, c'est-à-dire lors de cette écriture hello `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="4faf7-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="4faf7-162">Installer des modules de Restify hello dans votre API web</span><span class="sxs-lookup"><span data-stu-id="4faf7-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="4faf7-163">Nous utilisons Restify toobuild votre API REST.</span><span class="sxs-lookup"><span data-stu-id="4faf7-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="4faf7-164">Restify est une infrastructure d’application Node.js minimale et flexible dérivée d’Express.</span><span class="sxs-lookup"><span data-stu-id="4faf7-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="4faf7-165">Elle inclut un ensemble complet de fonctionnalités de création API REST sur Connect.</span><span class="sxs-lookup"><span data-stu-id="4faf7-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="4faf7-166">Installation de Restify</span><span class="sxs-lookup"><span data-stu-id="4faf7-166">Install Restify</span></span>
<span data-ttu-id="4faf7-167">À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`.</span><span class="sxs-lookup"><span data-stu-id="4faf7-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="4faf7-168">Si hello `azuread` répertoire n’existe pas, créez-le.</span><span class="sxs-lookup"><span data-stu-id="4faf7-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="4faf7-169">`cd azuread` ou `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="4faf7-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="4faf7-170">Entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4faf7-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="4faf7-171">Cette commande permet d’installer Restify.</span><span class="sxs-lookup"><span data-stu-id="4faf7-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="4faf7-172">Une erreur est-elle survenue ?</span><span class="sxs-lookup"><span data-stu-id="4faf7-172">Did you get an error?</span></span>
<span data-ttu-id="4faf7-173">Dans certains systèmes d’exploitation, lorsque vous utilisez `npm`, vous pouvez recevoir hello erreur `Error: EPERM, chmod '/usr/local/bin/..'` et une demande que vous exécutez un compte de hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="4faf7-174">Si ce problème se produit, utilisez hello `sudo` commande toorun `npm` à un niveau de privilège supérieur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="4faf7-175">Avez-vous reçu une erreur DTrace ?</span><span class="sxs-lookup"><span data-stu-id="4faf7-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="4faf7-176">Lors de l’installation de Restify, un texte semblable au suivant peut s’afficher :</span><span class="sxs-lookup"><span data-stu-id="4faf7-176">You may see something like this text when you install Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="4faf7-177">Restify fournit un mécanisme puissant pour suivre les appels REST à l’aide de DTrace.</span><span class="sxs-lookup"><span data-stu-id="4faf7-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="4faf7-178">Toutefois, de nombreux systèmes d’exploitation ne disposent pas de DTrace.</span><span class="sxs-lookup"><span data-stu-id="4faf7-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="4faf7-179">Vous pouvez ignorer ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="4faf7-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="4faf7-180">Hello une sortie de la commande hello doit apparaître le texte toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="4faf7-180">hello output of hello command should appear similar toothis text:</span></span>

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="4faf7-181">Installer Passport.dans votre API web</span><span class="sxs-lookup"><span data-stu-id="4faf7-181">Install Passport in your web API</span></span>
<span data-ttu-id="4faf7-182">À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà.</span><span class="sxs-lookup"><span data-stu-id="4faf7-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="4faf7-183">Installez Passport à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4faf7-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="4faf7-184">sortie de Hello de commande hello doit être texte toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="4faf7-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="4faf7-185">Ajouter l’organisation de passport tooyour web API</span><span class="sxs-lookup"><span data-stu-id="4faf7-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="4faf7-186">Ajoutez ensuite la stratégie d’OAuth hello à l’aide de `passport-azuread`, un ensemble de stratégies qui se connectent Azure AD à Passport.</span><span class="sxs-lookup"><span data-stu-id="4faf7-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="4faf7-187">Utilisez cette stratégie pour les jetons de support dans l’exemple d’API REST hello.</span><span class="sxs-lookup"><span data-stu-id="4faf7-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="4faf7-188">Bien qu’OAuth2 fournisse une infrastructure dans laquelle tout type de jeton connu peut être émis, seuls certains types de jeton sont utilisés de manière généralisée.</span><span class="sxs-lookup"><span data-stu-id="4faf7-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="4faf7-189">les jetons de Hello pour protéger les points de terminaison sont des jetons de support.</span><span class="sxs-lookup"><span data-stu-id="4faf7-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="4faf7-190">Ces types de jetons sont hello plus largement émis dans OAuth2.</span><span class="sxs-lookup"><span data-stu-id="4faf7-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="4faf7-191">De nombreuses implémentations supposent que les jetons de porteur hello seul type de jeton émis.</span><span class="sxs-lookup"><span data-stu-id="4faf7-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="4faf7-192">À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà.</span><span class="sxs-lookup"><span data-stu-id="4faf7-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="4faf7-193">Installer hello Passport `passport-azure-ad` module à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4faf7-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="4faf7-194">sortie de Hello de commande hello doit être texte toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="4faf7-194">hello output of hello command should be similar toothis text:</span></span>

``
passport-azure-ad@1.0.0 node_modules/passport-azure-ad
├── xtend@4.0.0
├── xmldom@0.1.19
├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
├── underscore@1.8.3
├── async@1.3.0
├── jsonwebtoken@5.0.2
├── xml-crypto@0.5.27 (xpath.js@1.0.6)
├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
└── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
``

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="4faf7-195">Ajout de MongoDB modules tooyour web API</span><span class="sxs-lookup"><span data-stu-id="4faf7-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="4faf7-196">Cet exemple utilise MongoDB comme magasin de données.</span><span class="sxs-lookup"><span data-stu-id="4faf7-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="4faf7-197">Pour ce dernier, installez Mongoose, un plug-in largement utilisé pour la gestion des modèles et des schémas.</span><span class="sxs-lookup"><span data-stu-id="4faf7-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="4faf7-198">Installation de modules supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4faf7-198">Install additional modules</span></span>
<span data-ttu-id="4faf7-199">Ensuite, installez hello restant modules requis.</span><span class="sxs-lookup"><span data-stu-id="4faf7-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="4faf7-200">À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :</span><span class="sxs-lookup"><span data-stu-id="4faf7-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="4faf7-201">Installer les modules hello dans votre `node_modules` active :</span><span class="sxs-lookup"><span data-stu-id="4faf7-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="4faf7-202">Créer un fichier server.js avec vos dépendances</span><span class="sxs-lookup"><span data-stu-id="4faf7-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="4faf7-203">Hello `server.js` fichier fournit la majorité de hello des fonctionnalités de hello pour votre serveur d’API Web.</span><span class="sxs-lookup"><span data-stu-id="4faf7-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="4faf7-204">À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :</span><span class="sxs-lookup"><span data-stu-id="4faf7-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="4faf7-205">Créez un fichier `server.js` dans un éditeur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="4faf7-206">Ajoutez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4faf7-206">Add hello following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="4faf7-207">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="4faf7-207">Save hello file.</span></span> <span data-ttu-id="4faf7-208">Vous revenez plus tard tooit.</span><span class="sxs-lookup"><span data-stu-id="4faf7-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="4faf7-209">Créer un toostore de fichier config.js vos paramètres Azure AD</span><span class="sxs-lookup"><span data-stu-id="4faf7-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="4faf7-210">Ce fichier de code transmet les paramètres de configuration hello à partir de votre portail Azure AD de toohello `Passport.js` fichier.</span><span class="sxs-lookup"><span data-stu-id="4faf7-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="4faf7-211">Vous avez créé ces valeurs de configuration lorsque vous avez ajouté le portail de hello web API toohello dans hello première partie de procédure pas à pas hello.</span><span class="sxs-lookup"><span data-stu-id="4faf7-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="4faf7-212">Nous vous expliquons quels tooput dans les valeurs hello de ces paramètres après avoir copié les code hello.</span><span class="sxs-lookup"><span data-stu-id="4faf7-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="4faf7-213">À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :</span><span class="sxs-lookup"><span data-stu-id="4faf7-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="4faf7-214">Créez un fichier `config.js` dans un éditeur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="4faf7-215">Ajoutez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4faf7-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="4faf7-216">Valeurs requises</span><span class="sxs-lookup"><span data-stu-id="4faf7-216">Required values</span></span>
<span data-ttu-id="4faf7-217">`clientID`: hello ID client de votre application d’API Web.</span><span class="sxs-lookup"><span data-stu-id="4faf7-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="4faf7-218">`IdentityMetadata`: Cette propriété est si `passport-azure-ad` recherche de vos données de configuration pour le fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="4faf7-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="4faf7-219">Il recherche également des jetons web hello clés toovalidate hello JSON.</span><span class="sxs-lookup"><span data-stu-id="4faf7-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="4faf7-220">`audience`: hello URI (URI) à partir du portail hello qui identifie votre application appelante.</span><span class="sxs-lookup"><span data-stu-id="4faf7-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="4faf7-221">`tenantName`: nom de votre locataire (par exemple, **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="4faf7-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="4faf7-222">`policyName`: hello stratégie que vous souhaitez les jetons de hello toovalidate dans tooyour server à venir.</span><span class="sxs-lookup"><span data-stu-id="4faf7-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="4faf7-223">Cette stratégie doit être hello même stratégie que vous utilisez dans l’application hello client pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="4faf7-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="4faf7-224">Pour l’instant, utilisez hello même stratégies sur le programme d’installation de client et le serveur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="4faf7-225">Si vous avez déjà effectué une procédure pas à pas et créé ces stratégies, vous n’avez pas besoin toodo encore une fois.</span><span class="sxs-lookup"><span data-stu-id="4faf7-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="4faf7-226">Étant donné que vous effectué la procédure pas à pas hello, vous ne doivent pas devez tooset des nouvelles stratégies pour les procédures détaillées de client sur le site de hello.</span><span class="sxs-lookup"><span data-stu-id="4faf7-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="4faf7-227">Ajouter le fichier de configuration tooyour server.js</span><span class="sxs-lookup"><span data-stu-id="4faf7-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="4faf7-228">valeurs hello tooread hello `config.js` que vous avez créé, ajoutez hello `.config` comme une ressource requise dans votre application, puis, définissez hello variables globales toothose Bonjour `config.js` document.</span><span class="sxs-lookup"><span data-stu-id="4faf7-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="4faf7-229">À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :</span><span class="sxs-lookup"><span data-stu-id="4faf7-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="4faf7-230">Ouvrez hello `server.js` fichier dans un éditeur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="4faf7-231">Ajoutez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4faf7-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="4faf7-232">Ajouter une nouvelle section trop`server.js` incluant hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="4faf7-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="4faf7-233">Ensuite, vous allez ajouter des espaces réservés pour les utilisateurs de hello nous recevons de nos applications appelante.</span><span class="sxs-lookup"><span data-stu-id="4faf7-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="4faf7-234">Nous allons également créer notre enregistreur d’événements.</span><span class="sxs-lookup"><span data-stu-id="4faf7-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="4faf7-235">Ajouter des informations de modèle et schéma de MongoDB hello à l’aide de Mongoose</span><span class="sxs-lookup"><span data-stu-id="4faf7-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="4faf7-236">Hello préparation antérieure bénéfiques Bring de ces trois fichiers dans un service de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="4faf7-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="4faf7-237">Pour cette procédure pas à pas, utiliser des MongoDB toostore vos tâches, comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="4faf7-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="4faf7-238">Bonjour `config.js` fichier, vous avez appelé votre base de données **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="4faf7-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="4faf7-239">Ce nom a été également ce que vous mettez à fin hello Hello `mongoose_auth_local` URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="4faf7-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="4faf7-240">Vous n’avez pas besoin toocreate cette base de données au préalable dans MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4faf7-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="4faf7-241">Il crée de la base de données hello de hello première exécution de votre application serveur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="4faf7-242">Une fois que vous indiquez à quel toouse de base de données MongoDB server de hello, vous devez toowrite certains modèles de code supplémentaire toocreate hello et un schéma pour vos tâches de serveur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="4faf7-243">Développez le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="4faf7-243">Expand hello model</span></span>
<span data-ttu-id="4faf7-244">Ce modèle de schéma est simple.</span><span class="sxs-lookup"><span data-stu-id="4faf7-244">This schema model is simple.</span></span> <span data-ttu-id="4faf7-245">Vous pouvez le développer en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="4faf7-245">You can expand it as required.</span></span>

<span data-ttu-id="4faf7-246">`owner`: Qui est assigné toohello tâche.</span><span class="sxs-lookup"><span data-stu-id="4faf7-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="4faf7-247">Cet objet est une **chaîne**.</span><span class="sxs-lookup"><span data-stu-id="4faf7-247">This object is a **string**.</span></span>  

<span data-ttu-id="4faf7-248">`Text`: tâche hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="4faf7-248">`Text`: hello task itself.</span></span> <span data-ttu-id="4faf7-249">Cet objet est une **chaîne**.</span><span class="sxs-lookup"><span data-stu-id="4faf7-249">This object is a **string**.</span></span>

<span data-ttu-id="4faf7-250">`date`: date de hello que la tâche hello est plein.</span><span class="sxs-lookup"><span data-stu-id="4faf7-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="4faf7-251">Cet objet est une **dateHeure**.</span><span class="sxs-lookup"><span data-stu-id="4faf7-251">This object is a **datetime**.</span></span>

<span data-ttu-id="4faf7-252">`completed`: Si la tâche hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="4faf7-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="4faf7-253">Cet objet est un **booléen**.</span><span class="sxs-lookup"><span data-stu-id="4faf7-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="4faf7-254">Créer un schéma de hello dans le code hello</span><span class="sxs-lookup"><span data-stu-id="4faf7-254">Create hello schema in hello code</span></span>
<span data-ttu-id="4faf7-255">À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :</span><span class="sxs-lookup"><span data-stu-id="4faf7-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="4faf7-256">Ouvrez hello `server.js` fichier dans un éditeur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="4faf7-257">Ajoutez hello informations sous l’entrée de configuration hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="4faf7-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="4faf7-258">Vous créez tout d’abord le schéma de hello, puis vous créez un objet de modèle que vous utilisez toostore vos données dans l’ensemble de hello code lorsque vous définissez votre **itinéraires**.</span><span class="sxs-lookup"><span data-stu-id="4faf7-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="4faf7-259">Ajouter des itinéraires pour votre serveur de la tâche API REST</span><span class="sxs-lookup"><span data-stu-id="4faf7-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="4faf7-260">Maintenant que vous avez un toowork de modèle de base de données avec, ajoutez des itinéraires hello que vous utilisez pour votre serveur d’API REST.</span><span class="sxs-lookup"><span data-stu-id="4faf7-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="4faf7-261">À propos des itinéraires dans Restify</span><span class="sxs-lookup"><span data-stu-id="4faf7-261">About routes in Restify</span></span>
<span data-ttu-id="4faf7-262">Fonctionnement des gammes Restify Bonjour même façon qu’ils utilisent lorsqu’ils utilisent la pile de Express hello.</span><span class="sxs-lookup"><span data-stu-id="4faf7-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="4faf7-263">Vous définissez des itinéraires à l’aide de hello URI que vous attendez hello client applications toocall.</span><span class="sxs-lookup"><span data-stu-id="4faf7-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="4faf7-264">Voici un exemple de modèle d’un itinéraire Restify :</span><span class="sxs-lookup"><span data-stu-id="4faf7-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="4faf7-265">Restify et Express fournissent des fonctionnalités bien plus approfondies, comme la définition de types d’application et la création d’un routage complexe entre différents points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4faf7-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="4faf7-266">Pour des raisons de hello de ce didacticiel, nous conserver ces itinéraires simple.</span><span class="sxs-lookup"><span data-stu-id="4faf7-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="4faf7-267">Ajouter le serveur de tooyour d’itinéraires par défaut</span><span class="sxs-lookup"><span data-stu-id="4faf7-267">Add default routes tooyour server</span></span>
<span data-ttu-id="4faf7-268">Vous ajoutez maintenant les itinéraires CRUD base hello de **créer** et **liste** pour notre API REST.</span><span class="sxs-lookup"><span data-stu-id="4faf7-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="4faf7-269">Vous trouverez les autres itinéraires Bonjour `complete` branche de l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="4faf7-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="4faf7-270">À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :</span><span class="sxs-lookup"><span data-stu-id="4faf7-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="4faf7-271">Ouvrez hello `server.js` fichier dans un éditeur.</span><span class="sxs-lookup"><span data-stu-id="4faf7-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="4faf7-272">Sous les entrées de base de données hello apportées ci-dessus ajouter hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4faf7-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err)
            return next(err);

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Add one!");
        }

        if (!owner) {
            log.warn(err, "You did not pass an owner when listing tasks.");
        } else {

            res.json(data);

        }
    });

    return next();
}
```


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="4faf7-273">Ajouter la gestion des erreurs pour les itinéraires hello</span><span class="sxs-lookup"><span data-stu-id="4faf7-273">Add error handling for hello routes</span></span>
<span data-ttu-id="4faf7-274">Ajoutez une gestion des erreurs afin que vous pouvez communiquer les problèmes de client toohello précédent de manière à ce qu’il puisse comprendre.</span><span class="sxs-lookup"><span data-stu-id="4faf7-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="4faf7-275">Ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="4faf7-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="create-your-server"></a><span data-ttu-id="4faf7-276">Créer votre serveur</span><span class="sxs-lookup"><span data-stu-id="4faf7-276">Create your server</span></span>
<span data-ttu-id="4faf7-277">Vous avez maintenant défini votre base de données et mis vos itinéraires en place.</span><span class="sxs-lookup"><span data-stu-id="4faf7-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="4faf7-278">dernière chose de Hello pour vous toodo est tooadd hello server instance qui gère vos appels.</span><span class="sxs-lookup"><span data-stu-id="4faf7-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="4faf7-279">Restify et Express fournissent une forte personnalisation pour un serveur d’API REST, mais nous utilisons le programme d’installation plus simple de hello ici.</span><span class="sxs-lookup"><span data-stu-id="4faf7-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="4faf7-280">Ajouter hello itinéraires toohello serveur (sans authentification)</span><span class="sxs-lookup"><span data-stu-id="4faf7-280">Add hello routes toohello server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="4faf7-281">Ajouter le serveur d’authentification tooyour API REST</span><span class="sxs-lookup"><span data-stu-id="4faf7-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="4faf7-282">Maintenant que vous disposez d’un serveur API REST en cours d’exécution, vous pouvez l’utiliser dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4faf7-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="4faf7-283">À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :</span><span class="sxs-lookup"><span data-stu-id="4faf7-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="4faf7-284">Utilisez hello OIDCBearerStrategy qui est inclus avec passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="4faf7-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="4faf7-285">Lorsque vous écrivez API, vous devez lier toujours hello toosomething de données unique à partir du jeton hello qui hello utilisateur ne peut pas usurper l’identité.</span><span class="sxs-lookup"><span data-stu-id="4faf7-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="4faf7-286">Lorsque le serveur de hello stocke des éléments de tâche, il est par conséquent, en fonction de hello **oid** d’utilisateur hello dans le jeton hello (appelé via token.oid), qui s’intègre dans le champ hello « propriétaire ».</span><span class="sxs-lookup"><span data-stu-id="4faf7-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="4faf7-287">Cette valeur permet de s’assurer que seul cet utilisateur peut accéder à ses propres tâches.</span><span class="sxs-lookup"><span data-stu-id="4faf7-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="4faf7-288">Il n’aucune exposition Bonjour API de « propriétaire », un utilisateur externe peut demander que d’autres éléments de tâche même s’ils sont authentifiés.</span><span class="sxs-lookup"><span data-stu-id="4faf7-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="4faf7-289">Ensuite, utilisez la stratégie de support hello fourni avec `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="4faf7-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="4faf7-290">Passport utilise hello même modèle pour toutes les stratégies de son.</span><span class="sxs-lookup"><span data-stu-id="4faf7-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="4faf7-291">Vous lui transmettez une `function()` qui dispose des paramètres `token` et `done`.</span><span class="sxs-lookup"><span data-stu-id="4faf7-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="4faf7-292">stratégie de Hello revient tooyou après que qu’il a terminé tout son travail.</span><span class="sxs-lookup"><span data-stu-id="4faf7-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="4faf7-293">Vous devez ensuite stocker utilisateur de hello et enregistrer le jeton de hello afin que vous n’avez pas besoin tooask pour celle-ci à nouveau.</span><span class="sxs-lookup"><span data-stu-id="4faf7-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4faf7-294">code Hello ci-dessus prend tout utilisateur qui se produit tooauthenticate tooyour server.</span><span class="sxs-lookup"><span data-stu-id="4faf7-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="4faf7-295">Ce processus est appelé enregistrement automatique.</span><span class="sxs-lookup"><span data-stu-id="4faf7-295">This process is known as autoregistration.</span></span> <span data-ttu-id="4faf7-296">Dans les serveurs de production, ne laissez pas dans les API hello d’accès aux utilisateurs sans avoir d’abord les passent par un processus d’inscription.</span><span class="sxs-lookup"><span data-stu-id="4faf7-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="4faf7-297">Ce processus est généralement hello modèle que s’affiche dans les applications consommateur qui vous permettent tooregister à l’aide de Facebook, mais vous demander de toofill des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4faf7-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="4faf7-298">Si ce programme n’est pas un programme de ligne de commande, nous avons extrait par courrier électronique hello à partir de l’objet du jeton hello qui est retourné et demandé toofill aux utilisateurs des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4faf7-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="4faf7-299">Comme il s’agit d’un exemple, nous les ajoutons tooan base de données.</span><span class="sxs-lookup"><span data-stu-id="4faf7-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="4faf7-300">Exécutez votre tooverify d’application serveur qu’il rejette vous</span><span class="sxs-lookup"><span data-stu-id="4faf7-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="4faf7-301">Vous pouvez utiliser `curl` toosee si vous avez maintenant OAuth2 protection par rapport à vos points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4faf7-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="4faf7-302">Hello en-têtes retournés doivent être suffisamment tootell que vous êtes sur le chemin d’accès correct de hello.</span><span class="sxs-lookup"><span data-stu-id="4faf7-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="4faf7-303">Vérifiez que votre instance MongoDB est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="4faf7-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="4faf7-304">Modifier toohello active et le serveur d’exécution hello :</span><span class="sxs-lookup"><span data-stu-id="4faf7-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="4faf7-305">Dans une nouvelle fenêtre de terminal, exécutez `curl`</span><span class="sxs-lookup"><span data-stu-id="4faf7-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="4faf7-306">Essayez une commande basique, comme POST :</span><span class="sxs-lookup"><span data-stu-id="4faf7-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="4faf7-307">Une erreur 401 est réponse hello souhaitée.</span><span class="sxs-lookup"><span data-stu-id="4faf7-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="4faf7-308">Il indique que cette couche de Passport hello essaie tooredirect toohello de point de terminaison authorize.</span><span class="sxs-lookup"><span data-stu-id="4faf7-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="4faf7-309">Vous disposez maintenant d’un service API REST qui utilise OAuth2.</span><span class="sxs-lookup"><span data-stu-id="4faf7-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="4faf7-310">Vous avez implémenté une API REST à l’aide de Restify et d’OAuth.</span><span class="sxs-lookup"><span data-stu-id="4faf7-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="4faf7-311">Vous avez maintenant suffisamment code afin que vous pouvez continuer toodevelop votre service et générer cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4faf7-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="4faf7-312">Vous êtes allé aussi loin que possible avec ce serveur sans utiliser un client compatible OAuth2.</span><span class="sxs-lookup"><span data-stu-id="4faf7-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="4faf7-313">Pour cette étape suivante, utilisez une procédure pas à pas supplémentaires comme notre [connecter tooa web API à l’aide d’iOS avec B2C](active-directory-b2c-devquickstarts-ios.md) procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="4faf7-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4faf7-314">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4faf7-314">Next steps</span></span>
<span data-ttu-id="4faf7-315">Vous pouvez maintenant déplacer des rubriques toomore avancée, telles que :</span><span class="sxs-lookup"><span data-stu-id="4faf7-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="4faf7-316">Se connecter tooa web API à l’aide d’iOS avec B2C</span><span class="sxs-lookup"><span data-stu-id="4faf7-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
