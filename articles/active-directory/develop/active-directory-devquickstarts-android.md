---
title: aaaAzure AD Android prise en main | Documents Microsoft
description: "Comment toobuild une application Android qui s’intègre à Azure AD pour se connecter et d’appels Azure AD protégé API à l’aide d’OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="fd377-103">Intégration d’Azure AD dans une application Android</span><span class="sxs-lookup"><span data-stu-id="fd377-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="fd377-104">Un aperçu de hello de notre nouveau [portail des développeurs](https://identity.microsoft.com/Docs/Android), ce qui vous aidera à obtenir en cours d’exécution auprès d’Azure AD en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="fd377-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="fd377-105">portail des développeurs Hello vous guidera tout au long des processus hello l’inscription d’une application et l’intégration d’Azure AD dans votre code.</span><span class="sxs-lookup"><span data-stu-id="fd377-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="fd377-106">Une fois que vous aurez terminé, vous disposerez d’une application simple capable d’authentifier les utilisateurs dans votre client et d’un serveur principal qui peut accepter les jetons et effectuer la validation.</span><span class="sxs-lookup"><span data-stu-id="fd377-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="fd377-107">Si vous développez une application de bureau, Azure Active Directory (Azure AD) rend très simple pour vous tooauthenticate vos utilisateurs à l’aide de leurs comptes d’Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="fd377-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="fd377-108">Il permet également de votre application toosecurely consommer n’importe quel web API protégée par Azure AD, comme la hello API Office 365 ou hello API Azure.</span><span class="sxs-lookup"><span data-stu-id="fd377-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="fd377-109">Pour les clients Android qui ont besoin de ressources de tooaccess protégé, Azure AD fournit hello Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="fd377-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="fd377-110">Hello seul but de la bibliothèque ADAL est toomake plus facile pour les jetons d’accès tooget votre application.</span><span class="sxs-lookup"><span data-stu-id="fd377-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="fd377-111">toodemonstrate facilement il s’agit, nous allons créer une application Android liste de tâches :</span><span class="sxs-lookup"><span data-stu-id="fd377-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="fd377-112">Obtient les jetons pour l’appel d’une API de la liste des tâches à l’aide de hello d’accès [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd377-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="fd377-113">obtention de la liste des tâches d’un utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="fd377-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="fd377-114">déconnexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fd377-114">Signs out users.</span></span>

<span data-ttu-id="fd377-115">tooget démarré, vous devez un locataire Azure AD, dans laquelle vous pouvez créer des utilisateurs et inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="fd377-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="fd377-116">Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="fd377-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="fd377-117">Étape 1 : Télécharger et exécuter l’exemple de serveur hello Node.js REST API TODO</span><span class="sxs-lookup"><span data-stu-id="fd377-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="fd377-118">exemple de Node.js REST API TODO Hello est écrit spécifiquement toowork par rapport à notre exemple existant pour la création d’un locataire unique action REST API pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd377-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="fd377-119">Il s’agit d’une condition préalable pour hello démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="fd377-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="fd377-120">Pour plus d’informations sur comment tooset cette installation, consultez nos exemples existants dans [Service Microsoft Azure Active Directory exemple REST API pour Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="fd377-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="fd377-121">Étape 2 : Inscription de votre API web auprès de votre client Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd377-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="fd377-122">Active Directory prend en charge l’ajout de deux types d’application :</span><span class="sxs-lookup"><span data-stu-id="fd377-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="fd377-123">API qui offrent des toousers de services Web</span><span class="sxs-lookup"><span data-stu-id="fd377-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="fd377-124">Applications (en cours d’exécution sur le web de hello ou sur un appareil) qui accèdent à ceux des API web</span><span class="sxs-lookup"><span data-stu-id="fd377-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="fd377-125">Dans cette étape, vous êtes enregistré hello web API que vous exécutez localement pour tester cet exemple.</span><span class="sxs-lookup"><span data-stu-id="fd377-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="fd377-126">Normalement, cette API web est un service REST offre les fonctionnalités que vous souhaitez une tooaccess de l’application.</span><span class="sxs-lookup"><span data-stu-id="fd377-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="fd377-127">Azure AD peut contribuer à protéger n’importe quel point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="fd377-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="fd377-128">Nous supposons que vous êtes inscrit hello API REST de tâches mentionnée précédemment.</span><span class="sxs-lookup"><span data-stu-id="fd377-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="fd377-129">Mais cela fonctionne pour n’importe quel site web API Azure Active Directory toohelp protéger.</span><span class="sxs-lookup"><span data-stu-id="fd377-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="fd377-130">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd377-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fd377-131">Sur la barre supérieure de hello, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="fd377-131">On hello top bar, click your account.</span></span> <span data-ttu-id="fd377-132">Bonjour **répertoire** , choisissez locataire hello AD Azure où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="fd377-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="fd377-133">Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd377-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="fd377-134">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fd377-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="fd377-135">Entrez un nom convivial pour l’application hello (par exemple, **TodoListService**), sélectionnez **Application Web et/ou API Web**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="fd377-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="fd377-136">Pour l’URL de connexion hello, entrez les URL de base de hello pour exemple hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="fd377-137">(`https://localhost:8080` par défaut).</span><span class="sxs-lookup"><span data-stu-id="fd377-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="fd377-138">Cliquez sur **OK** l’inscription de toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="fd377-139">Dans hello portail Azure, atteindre la page d’application tooyour, recherchez la valeur d’ID application hello et copiez-le.</span><span class="sxs-lookup"><span data-stu-id="fd377-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="fd377-140">Vous en aurez besoin plus tard lors de la configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="fd377-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="fd377-141">À partir de hello **paramètres** -> **propriétés** page, mettre à jour d’URI ID d’application hello - entrez `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="fd377-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="fd377-142">Remplacez `<your_tenant_name>` par nom de hello de votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd377-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="fd377-143">Étape 3 : Inscrire hello exemple Android Native d’application cliente</span><span class="sxs-lookup"><span data-stu-id="fd377-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="fd377-144">Vous devez inscrire votre application web dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="fd377-144">You must register your web application in this sample.</span></span> <span data-ttu-id="fd377-145">Cela permet de toocommunicate de votre application avec hello inscrit juste API web.</span><span class="sxs-lookup"><span data-stu-id="fd377-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="fd377-146">Azure AD refusera tooeven autoriser tooask de votre application pour la connexion, sauf si elle est inscrite.</span><span class="sxs-lookup"><span data-stu-id="fd377-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="fd377-147">Qui est la partie de la sécurité hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="fd377-148">Nous supposons que vous êtes l’inscription d’application d’exemple hello mentionnée précédemment.</span><span class="sxs-lookup"><span data-stu-id="fd377-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="fd377-149">Cependant, cette procédure fonctionne pour n’importe quelle application que vous développez.</span><span class="sxs-lookup"><span data-stu-id="fd377-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="fd377-150">Vous vous demandez peut-être pourquoi nous incorporons à la fois une application et une API web dans un seul client.</span><span class="sxs-lookup"><span data-stu-id="fd377-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="fd377-151">Comme vous l’avez peut-être deviné, vous pouvez générer une application qui accède à une API externe inscrite dans Azure AD à partir d’un autre client.</span><span class="sxs-lookup"><span data-stu-id="fd377-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="fd377-152">Si vous procédez ainsi, vos clients seront vous y êtes invité à utiliser toohello tooconsent hello API dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="fd377-153">La bibliothèque d’authentification Active Directory pour iOS s’occupe de cette autorisation pour vous.</span><span class="sxs-lookup"><span data-stu-id="fd377-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="fd377-154">Lors de l’exploration des fonctionnalités plus avancées, vous verrez qu’il s’agit d’une partie importante de la suite de hello hello travail tooaccess nécessaires de Microsoft APIs d’Azure et Office, ainsi que tout autre fournisseur de service.</span><span class="sxs-lookup"><span data-stu-id="fd377-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="fd377-155">Pour l’instant, car vous avez inscrit votre API web et votre application sous hello même locataire, vous ne voyez pas les invites de consentement.</span><span class="sxs-lookup"><span data-stu-id="fd377-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="fd377-156">C’est généralement hello cas si vous développez une application simplement pour votre propre toouse d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="fd377-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="fd377-157">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd377-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fd377-158">Sur la barre supérieure de hello, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="fd377-158">On hello top bar, click your account.</span></span> <span data-ttu-id="fd377-159">Bonjour **répertoire** , choisissez locataire hello AD Azure où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="fd377-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="fd377-160">Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd377-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="fd377-161">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fd377-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="fd377-162">Entrez un nom convivial pour l’application hello (par exemple, **TodoListClient-Android**), sélectionnez **Application cliente Native**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="fd377-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="fd377-163">Pourquoi les URI de redirection, entrez `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="fd377-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="fd377-164">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="fd377-164">Click **Finish**.</span></span>
7. <span data-ttu-id="fd377-165">À partir de la page d’application hello, recherchez la valeur d’ID application hello et copiez-la.</span><span class="sxs-lookup"><span data-stu-id="fd377-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="fd377-166">Vous en aurez besoin plus tard lors de la configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="fd377-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="fd377-167">À partir de hello **paramètres** page, sélectionnez **autorisations requises** et sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fd377-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="fd377-168">Recherchez et sélectionnez TodoListService, ajouter hello **accès TodoListService** autorisation sous **autorisations déléguées**, puis cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="fd377-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="fd377-169">toobuild avec Maven, vous pouvez utiliser pom.xml hello premier niveau :</span><span class="sxs-lookup"><span data-stu-id="fd377-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="fd377-170">Clonez ce référentiel dans le répertoire de votre choix :</span><span class="sxs-lookup"><span data-stu-id="fd377-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="fd377-171">Suivez les étapes de hello Bonjour [tooset des conditions préalables de votre environnement de Maven pour Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="fd377-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="fd377-172">Configurer l’émulateur hello avec le Kit de développement logiciel 19.</span><span class="sxs-lookup"><span data-stu-id="fd377-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="fd377-173">Atteindre le dossier racine de toohello où vous avez cloné le dépôt de hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="fd377-174">Exécutez cette commande : `mvn clean install`.</span><span class="sxs-lookup"><span data-stu-id="fd377-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="fd377-175">Modifier l’exemple de démarrage rapide de toohello hello active :`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="fd377-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="fd377-176">Exécutez cette commande : `mvn android:deploy android:run`.</span><span class="sxs-lookup"><span data-stu-id="fd377-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="fd377-177">Vous devez voir le démarrage d’application hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="fd377-178">Entrez tootry d’informations d’identification utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="fd377-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="fd377-179">Les packages JAR seront soumis à côté de package de AAR hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="fd377-180">Étape 4 : Télécharger hello Android ADAL et ajoutez-le tooyour espace de travail Eclipse</span><span class="sxs-lookup"><span data-stu-id="fd377-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="fd377-181">Nous avons simplifié pour vous toohave plusieurs options toouse ADAL dans votre projet Android :</span><span class="sxs-lookup"><span data-stu-id="fd377-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="fd377-182">Vous pouvez utiliser tooimport de code source hello cette bibliothèque dans des application tooyour Eclipse et lien.</span><span class="sxs-lookup"><span data-stu-id="fd377-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="fd377-183">Si vous utilisez Android Studio, vous pouvez utiliser hello AAR package format référence hello binaires et.</span><span class="sxs-lookup"><span data-stu-id="fd377-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="fd377-184">Option 1 : code source dans un fichier ZIP</span><span class="sxs-lookup"><span data-stu-id="fd377-184">Option 1: Source Zip</span></span>
<span data-ttu-id="fd377-185">toodownload une copie du code source de hello, cliquez sur **ZIP de téléchargement** sur le côté droit de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="fd377-186">Vous pouvez également [effectuer le téléchargement à partir de GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="fd377-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="fd377-187">Option 2:  code Source via Git</span><span class="sxs-lookup"><span data-stu-id="fd377-187">Option 2: Source via Git</span></span>
<span data-ttu-id="fd377-188">code de source tooget hello Hello SDK via Git, tapez :</span><span class="sxs-lookup"><span data-stu-id="fd377-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="fd377-189">Option 3: fichiers binaires via Gradle</span><span class="sxs-lookup"><span data-stu-id="fd377-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="fd377-190">Vous pouvez obtenir les fichiers binaires de hello référentiel central de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="fd377-191">package de AAR Hello peut être inclus comme suit dans votre projet dans Android Studio :</span><span class="sxs-lookup"><span data-stu-id="fd377-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="fd377-192">Option 4: AAR via Maven</span><span class="sxs-lookup"><span data-stu-id="fd377-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="fd377-193">Si vous utilisez hello M2Eclipse plug-in, vous pouvez spécifier la dépendance de hello dans votre fichier pom.xml :</span><span class="sxs-lookup"><span data-stu-id="fd377-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="fd377-194">Option 5 : Package du fichier JAR à l’intérieur du dossier de bibliothèques hello</span><span class="sxs-lookup"><span data-stu-id="fd377-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="fd377-195">Vous pouvez obtenir le fichier JAR hello à partir du référentiel de Maven hello et déposez-le dans hello **libs** dossier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="fd377-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="fd377-196">Vous devez toocopy hello ressources requises tooyour projet ainsi, car les packages JAR hello ne les incluent pas.</span><span class="sxs-lookup"><span data-stu-id="fd377-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="fd377-197">Étape 5 : Ajouter le projet de références tooAndroid tooyour ADAL</span><span class="sxs-lookup"><span data-stu-id="fd377-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="fd377-198">Ajouter une référence de projet tooyour et spécifiez-le sous la forme d’une bibliothèque Android.</span><span class="sxs-lookup"><span data-stu-id="fd377-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="fd377-199">Si vous n’êtes pas sûr comment toodo cela, vous pouvez obtenir plus d’informations sur hello [site Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="fd377-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="fd377-200">Ajouter une dépendance de projet hello pour le débogage dans les paramètres de votre projet.</span><span class="sxs-lookup"><span data-stu-id="fd377-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="fd377-201">Mettre à jour tooinclude de fichier AndroidManifest.xml de votre projet :</span><span class="sxs-lookup"><span data-stu-id="fd377-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="fd377-202">Créez une instance d’AuthenticationContext pour votre activité principale.</span><span class="sxs-lookup"><span data-stu-id="fd377-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="fd377-203">Détails de Hello de cet appel sont traitées par cette rubrique hello, mais vous pouvez obtenir un bon début en examinant hello [exemple d’Android Native Client](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="fd377-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="fd377-204">Bonjour l’exemple suivant, SharedPreferences est cache par défaut de hello et autorité est de forme hello `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="fd377-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="fd377-205">Copiez le code bloc toohandle hello parvenir de AuthenticationActivity une fois que l’utilisateur de hello entre des informations d’identification et qu’il reçoit un code d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="fd377-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="fd377-206">tooask pour un jeton, définissez un rappel :</span><span class="sxs-lookup"><span data-stu-id="fd377-206">tooask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="fd377-207">Enfin, demandez un jeton à l’aide de ce rappel :</span><span class="sxs-lookup"><span data-stu-id="fd377-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="fd377-208">Voici une explication des paramètres de hello :</span><span class="sxs-lookup"><span data-stu-id="fd377-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="fd377-209">*ressource* est requise et que vous essayez de tooaccess de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="fd377-210">*clientid* est obligatoire et provient d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd377-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="fd377-211">*RedirectUri* n’est pas requis toobe fourni pour l’appel d’acquireToken hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="fd377-212">Vous pouvez définir ce paramètre sur le nom de votre package.</span><span class="sxs-lookup"><span data-stu-id="fd377-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="fd377-213">*PromptBehavior* vous aide à tooask pour la mémoire cache tooskip hello et un cookie.</span><span class="sxs-lookup"><span data-stu-id="fd377-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="fd377-214">*rappel* est appelé après que le code d’autorisation de hello est échangé pour un jeton.</span><span class="sxs-lookup"><span data-stu-id="fd377-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="fd377-215">Ce paramètre présente un objet AuthenticationResult avec jeton d’accès, date d’expiration et informations de jeton d’ID.</span><span class="sxs-lookup"><span data-stu-id="fd377-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="fd377-216">*acquireTokenSilent* est facultatif.</span><span class="sxs-lookup"><span data-stu-id="fd377-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="fd377-217">Vous pouvez l’appeler toohandle mise en cache et l’actualisation de jeton.</span><span class="sxs-lookup"><span data-stu-id="fd377-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="fd377-218">Il fournit également la version de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-218">It also provides hello sync version.</span></span> <span data-ttu-id="fd377-219">Il accepte *userId* comme paramètre.</span><span class="sxs-lookup"><span data-stu-id="fd377-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="fd377-220">À l’aide de cette procédure pas à pas, vous devez disposer de ce que vous devez intégrer toosuccessfully avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd377-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="fd377-221">Pour plus d’exemples de ce travail, visitez hello AzureADSamples / référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="fd377-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="fd377-222">Informations importantes</span><span class="sxs-lookup"><span data-stu-id="fd377-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="fd377-223">Personnalisation</span><span class="sxs-lookup"><span data-stu-id="fd377-223">Customization</span></span>
<span data-ttu-id="fd377-224">Les ressources de votre application peuvent remplacer celles du projet de bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="fd377-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="fd377-225">Cela se produit lors de la création de votre application.</span><span class="sxs-lookup"><span data-stu-id="fd377-225">This happens when your app is being built.</span></span> <span data-ttu-id="fd377-226">Pour cette raison, vous pouvez personnaliser l’authentification activité disposition hello librement.</span><span class="sxs-lookup"><span data-stu-id="fd377-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="fd377-227">Code de hello tookeep que des contrôles de hello que la bibliothèque ADAL utilise (WebView).</span><span class="sxs-lookup"><span data-stu-id="fd377-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="fd377-228">Service Broker</span><span class="sxs-lookup"><span data-stu-id="fd377-228">Broker</span></span>
<span data-ttu-id="fd377-229">application de portail d’entreprise Microsoft Intune Hello fournit un composant de service broker hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="fd377-230">compte de Hello est créé dans AccountManager.</span><span class="sxs-lookup"><span data-stu-id="fd377-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="fd377-231">type de compte Hello est « com.microsoft.workaccount ».</span><span class="sxs-lookup"><span data-stu-id="fd377-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="fd377-232">AccountManager autorise un seul compte d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fd377-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="fd377-233">Il crée un cookie d’authentification unique pour l’utilisateur de hello après avoir effectué la demande de périphérique hello pour l’une des applications de hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="fd377-234">La bibliothèque ADAL utilise le compte de service broker hello si un compte d’utilisateur est créé à cet authentificateur et que vous choisissez tooskip pas il.</span><span class="sxs-lookup"><span data-stu-id="fd377-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="fd377-235">Vous pouvez ignorer l’utilisateur du service broker hello avec :</span><span class="sxs-lookup"><span data-stu-id="fd377-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="fd377-236">Vous devez tooregister une RedirectUri spécial pour l’utilisation de service broker.</span><span class="sxs-lookup"><span data-stu-id="fd377-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="fd377-237">RedirectUri est au format hello de `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="fd377-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="fd377-238">Vous pouvez obtenir votre RedirectUri pour votre application à l’aide de hello script brokerRedirectPrint.ps1 ou hello API appel mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="fd377-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="fd377-239">signature de Hello est connexe tooyour certificats de signature.</span><span class="sxs-lookup"><span data-stu-id="fd377-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="fd377-240">modèle de service broker actif Hello est pour un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd377-240">hello current broker model is for one user.</span></span> <span data-ttu-id="fd377-241">AuthenticationContext fournit un utilisateur de service broker hello API méthode tooget hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="fd377-242">Votre manifeste d’application doit avoir hello suivant autorisations toouse AccountManager des comptes.</span><span class="sxs-lookup"><span data-stu-id="fd377-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="fd377-243">Pour plus d’informations, consultez hello [AccountManager plus d’informations sur le site de Android hello](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="fd377-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="fd377-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="fd377-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="fd377-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="fd377-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="fd377-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="fd377-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="fd377-247">AD FS et URL de l’autorité</span><span class="sxs-lookup"><span data-stu-id="fd377-247">Authority URL and AD FS</span></span>
<span data-ttu-id="fd377-248">Services de fédération Active Directory (AD FS) n’est pas reconnu en tant que STS, de production, afin que vous avez besoin tooturn de découverte d’instance et passez la valeur false au constructeur de classe AuthenticationContext hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="fd377-249">URL d’autorité Hello a besoin d’une instance de STS et une [nom_client](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="fd377-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="fd377-250">Interrogation des éléments de cache</span><span class="sxs-lookup"><span data-stu-id="fd377-250">Querying cache items</span></span>
<span data-ttu-id="fd377-251">ADAL fournit un cache par défaut dans SharedPreferences avec quelques fonctions simples de requête de cache.</span><span class="sxs-lookup"><span data-stu-id="fd377-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="fd377-252">Vous pouvez obtenir de cache actuelle hello de AuthenticationContext à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="fd377-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="fd377-253">Vous pouvez également fournir votre implémentation de cache, si vous souhaitez toocustomize il.</span><span class="sxs-lookup"><span data-stu-id="fd377-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="fd377-254">Comportement d’invite</span><span class="sxs-lookup"><span data-stu-id="fd377-254">Prompt behavior</span></span>
<span data-ttu-id="fd377-255">ADAL fournit un comportement de toospecify l’option invite.</span><span class="sxs-lookup"><span data-stu-id="fd377-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="fd377-256">PromptBehavior.Auto affiche hello l’interface utilisateur si le jeton d’actualisation hello n’est pas valide et les informations d’identification utilisateur sont requises.</span><span class="sxs-lookup"><span data-stu-id="fd377-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="fd377-257">PromptBehavior.Always ignore l’utilisation du cache de hello et toujours afficher hello l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd377-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="fd377-258">Demande de jeton en mode silencieux à partir du cache et actualisation</span><span class="sxs-lookup"><span data-stu-id="fd377-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="fd377-259">Une demande de jeton en mode silencieux n’utilise pas de hello indépendante de l’interface utilisateur et ne nécessite pas une activité.</span><span class="sxs-lookup"><span data-stu-id="fd377-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="fd377-260">Il retourne un jeton à partir du cache de hello s’il est disponible.</span><span class="sxs-lookup"><span data-stu-id="fd377-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="fd377-261">Si le jeton de hello a expiré, cette méthode essaie de toorefresh il.</span><span class="sxs-lookup"><span data-stu-id="fd377-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="fd377-262">Si le jeton d’actualisation hello est expiré ou a échoué, elle retourne AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="fd377-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="fd377-263">Vous pouvez également effectuer un appel de synchronisation à l’aide de cette méthode.</span><span class="sxs-lookup"><span data-stu-id="fd377-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="fd377-264">Vous pouvez définir toocallback null ou utiliser acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="fd377-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="fd377-265">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="fd377-265">Diagnostics</span></span>
<span data-ttu-id="fd377-266">Il s’agit de hello principales sources d’informations pour diagnostiquer les problèmes :</span><span class="sxs-lookup"><span data-stu-id="fd377-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="fd377-267">Exceptions</span><span class="sxs-lookup"><span data-stu-id="fd377-267">Exceptions</span></span>
* <span data-ttu-id="fd377-268">Journaux</span><span class="sxs-lookup"><span data-stu-id="fd377-268">Logs</span></span>
* <span data-ttu-id="fd377-269">Suivis réseau</span><span class="sxs-lookup"><span data-stu-id="fd377-269">Network traces</span></span>

<span data-ttu-id="fd377-270">Notez que les ID de corrélation sont diagnostics toohello central dans la bibliothèque de hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="fd377-271">Si vous voulez toocorrelate une ADAL demander avec d’autres opérations dans votre code, vous pouvez définir votre ID de corrélation sur la base de chaque demande.</span><span class="sxs-lookup"><span data-stu-id="fd377-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="fd377-272">Si vous ne définissez aucun ID de corrélation, la bibliothèque ADAL génère un ID aléatoire.</span><span class="sxs-lookup"><span data-stu-id="fd377-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="fd377-273">Tous les messages du journal et les appels réseau seront ensuite marqués avec l’ID de corrélation hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="fd377-274">modifications Hello générées automatiquement ID à chaque demande.</span><span class="sxs-lookup"><span data-stu-id="fd377-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="fd377-275">Exceptions</span><span class="sxs-lookup"><span data-stu-id="fd377-275">Exceptions</span></span>
<span data-ttu-id="fd377-276">Les exceptions sont tout d’abord hello diagnostic.</span><span class="sxs-lookup"><span data-stu-id="fd377-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="fd377-277">Nous essayons de messages d’erreur utiles tooprovide.</span><span class="sxs-lookup"><span data-stu-id="fd377-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="fd377-278">Si vous en trouvez un qui n’est pas utile, faites-le-nous savoir en signalant un problème.</span><span class="sxs-lookup"><span data-stu-id="fd377-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="fd377-279">Incluez des informations sur l’appareil, notamment le modèle et le numéro du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="fd377-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="fd377-280">Journaux</span><span class="sxs-lookup"><span data-stu-id="fd377-280">Logs</span></span>
<span data-ttu-id="fd377-281">Vous pouvez configurer hello bibliothèque toogenerate des messages de journal que vous pouvez utiliser toohelp diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="fd377-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="fd377-282">Vous configurez la journalisation en rendant hello suivant appeler tooconfigure un rappel que la bibliothèque ADAL utilisera toohand chaque message du journal car il est généré.</span><span class="sxs-lookup"><span data-stu-id="fd377-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="fd377-283">Les messages peuvent être écrits tooa fichier de journal personnalisé, comme indiqué dans hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="fd377-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="fd377-284">Malheureusement, il n’existe aucun moyen standard d’obtenir les journaux d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="fd377-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="fd377-285">Il existe des services qui peuvent vous y aider.</span><span class="sxs-lookup"><span data-stu-id="fd377-285">There are some services that can help you with this.</span></span> <span data-ttu-id="fd377-286">Vous pouvez également inventer votre propre, tels que serveur de tooa fichier hello émetteur.</span><span class="sxs-lookup"><span data-stu-id="fd377-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="fd377-287">Il s’agit des niveaux de journalisation hello :</span><span class="sxs-lookup"><span data-stu-id="fd377-287">These are hello logging levels:</span></span>
* <span data-ttu-id="fd377-288">Error (exceptions)</span><span class="sxs-lookup"><span data-stu-id="fd377-288">Error (exceptions)</span></span>
* <span data-ttu-id="fd377-289">Warn (avertissement)</span><span class="sxs-lookup"><span data-stu-id="fd377-289">Warn (warning)</span></span>
* <span data-ttu-id="fd377-290">Info (informations)</span><span class="sxs-lookup"><span data-stu-id="fd377-290">Info (information purposes)</span></span>
* <span data-ttu-id="fd377-291">Verbose (détails supplémentaires)</span><span class="sxs-lookup"><span data-stu-id="fd377-291">Verbose (more details)</span></span>

<span data-ttu-id="fd377-292">Vous définissez le niveau de journal hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd377-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="fd377-293">Tous les messages de journal sont envoyés toologcat, dans les rappels de journal personnalisé tooany Ajout.</span><span class="sxs-lookup"><span data-stu-id="fd377-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="fd377-294">Vous pouvez obtenir un fichier journal de tooa de logcat comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd377-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="fd377-295">Pour plus d’informations sur les commandes d’adb, consultez hello [logcat plus d’informations sur le site de Android hello](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="fd377-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="fd377-296">Suivis réseau</span><span class="sxs-lookup"><span data-stu-id="fd377-296">Network traces</span></span>
<span data-ttu-id="fd377-297">Vous pouvez utiliser divers outils toocapture hello le trafic HTTP qui génère de la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="fd377-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="fd377-298">Cela est particulièrement utile si vous êtes familiarisé avec hello protocole OAuth ou si vous devez tooprovide des informations de diagnostic tooMicrosoft ou autres canaux de support.</span><span class="sxs-lookup"><span data-stu-id="fd377-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="fd377-299">Fiddler est un outil de suivi HTTP hello plus simple.</span><span class="sxs-lookup"><span data-stu-id="fd377-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="fd377-300">Tooset des liens de suivants de hello d’utilisation de l’enregistrement toocorrectly ADAL trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="fd377-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="fd377-301">Pour un outil de suivi comme toobe Fiddler ou Charles utile, vous devez le configurer le trafic SSL toorecord non chiffré.</span><span class="sxs-lookup"><span data-stu-id="fd377-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="fd377-302">Les suivis générés de cette manière peuvent contenir des informations hautement privilégiées (jetons d’accès, noms d’utilisateur, mots de passe, etc.).</span><span class="sxs-lookup"><span data-stu-id="fd377-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="fd377-303">Si vous utilisez des comptes de production, ne partagez pas ces suivis avec des tiers.</span><span class="sxs-lookup"><span data-stu-id="fd377-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="fd377-304">Si vous avez besoin de toosupply un toosomeone de trace dans la prise en charge de commande tooget, reproduisez le problème d’hello à l’aide d’un compte temporaire avec les noms d’utilisateur et mots de passe que vous êtes prêt à partager.</span><span class="sxs-lookup"><span data-stu-id="fd377-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="fd377-305">À partir du site Web de Telerik hello : [paramètre de Fiddler pour Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="fd377-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="fd377-306">À partir de GitHub : [Configuration des règles de Fiddler pour la bibliothèque ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="fd377-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="fd377-307">Mode de la boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="fd377-307">Dialog mode</span></span>
<span data-ttu-id="fd377-308">méthode d’acquireToken Hello sans activité prend en charge une invite de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fd377-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="fd377-309">Chiffrement</span><span class="sxs-lookup"><span data-stu-id="fd377-309">Encryption</span></span>
<span data-ttu-id="fd377-310">La bibliothèque ADAL chiffre les jetons hello et magasin dans SharedPreferences par défaut.</span><span class="sxs-lookup"><span data-stu-id="fd377-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="fd377-311">Vous pouvez examiner les détails de hello StorageHelper classe toosee hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="fd377-312">Android a introduit Android Keydtore pour le stockage sécurisé des clés privées de la version 4.3 (API 18).</span><span class="sxs-lookup"><span data-stu-id="fd377-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="fd377-313">La bibliothèque ADAL utilise ces informations pour l’API 18 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="fd377-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="fd377-314">Si vous souhaitez toouse ADAL pour les versions inférieures de kit de développement logiciel, vous devez tooprovide une clé secrète à AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="fd377-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="fd377-315">Demande de support OAuth2</span><span class="sxs-lookup"><span data-stu-id="fd377-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="fd377-316">Hello AuthenticationParameters classe fournit authorization_uri tooget de fonctionnalités à partir de hello défi de support OAuth2.</span><span class="sxs-lookup"><span data-stu-id="fd377-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="fd377-317">Cookies de session dans WebView</span><span class="sxs-lookup"><span data-stu-id="fd377-317">Session cookies in WebView</span></span>
<span data-ttu-id="fd377-318">Android WebView n’efface pas les cookies de session une fois l’application hello est fermée.</span><span class="sxs-lookup"><span data-stu-id="fd377-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="fd377-319">Vous pouvez gérer cela à l’aide de l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="fd377-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="fd377-320">Pour plus d’informations sur les cookies, consultez hello [CookieSyncManager plus d’informations sur le site de Android hello](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="fd377-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="fd377-321">Remplacements de ressources</span><span class="sxs-lookup"><span data-stu-id="fd377-321">Resource overrides</span></span>
<span data-ttu-id="fd377-322">bibliothèque ADAL de Hello inclut des chaînes en anglais pour les messages ProgressDialog.</span><span class="sxs-lookup"><span data-stu-id="fd377-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="fd377-323">Votre application doit les remplacer si vous voulez des chaînes localisées.</span><span class="sxs-lookup"><span data-stu-id="fd377-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="fd377-324">Boîte de dialogue NTLM</span><span class="sxs-lookup"><span data-stu-id="fd377-324">NTLM dialog box</span></span>
<span data-ttu-id="fd377-325">ADAL version 1.1.0 prend en charge une boîte de dialogue NTLM qui est traitée via un événement onReceivedHttpAuthRequest hello WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="fd377-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="fd377-326">Vous pouvez personnaliser la disposition de hello et les chaînes de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="fd377-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="fd377-327">Authentification unique entre applications</span><span class="sxs-lookup"><span data-stu-id="fd377-327">Cross-app SSO</span></span>
<span data-ttu-id="fd377-328">En savoir plus [comment tooenable SSO inter-applications sur Android à l’aide de la bibliothèque ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="fd377-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
