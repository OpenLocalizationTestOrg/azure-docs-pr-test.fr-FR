---
title: aaaAzure AD Cordova prise en main | Documents Microsoft
description: "Comment toobuild une application Cordova s’intègre à Azure AD pour la connexion et appelle les API de protégé par AD Azure à l’aide d’OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="61c00-103">Intégration d’Azure AD avec une application Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="61c00-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="61c00-104">Vous pouvez utiliser les applications Apache Cordova toodevelop HTML5/JavaScript pouvant s’exécuter sur des appareils mobiles en tant qu’applications natives à part entière.</span><span class="sxs-lookup"><span data-stu-id="61c00-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="61c00-105">Avec Azure Active Directory (Azure AD), vous pouvez ajouter les applications Cordova tooyour Professionnel authentification fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="61c00-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="61c00-106">Un plug-in Cordova encapsule des kits de développement logiciels (SDK) natifs Azure AD sur iOS, Android, Windows Store et Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="61c00-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="61c00-107">À l’aide de plug-in, vous pouvez améliorer votre application toosupport connectez-vous avec les comptes de vos utilisateurs Active Directory Windows Server, obtenir accès tooOffice 365 ainsi que des API Azure et même aider à protéger les appels tooyour propre personnalisé API web.</span><span class="sxs-lookup"><span data-stu-id="61c00-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="61c00-108">Dans ce didacticiel, nous allons utiliser hello Apache Cordova plug-in pour Active Directory Authentication Library (ADAL) tooimprove une application simple en ajoutant hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="61c00-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="61c00-109">Avec quelques lignes de code seulement, authentifier un utilisateur et obtenir un jeton.</span><span class="sxs-lookup"><span data-stu-id="61c00-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="61c00-110">Utilisez ce tooquery de l’API Graph hello jeton tooinvoke ce répertoire et afficher les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="61c00-111">Utiliser l’authentification toominimize cache de jeton ADAL hello demande utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="61c00-112">toomake ces améliorations, vous devez :</span><span class="sxs-lookup"><span data-stu-id="61c00-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="61c00-113">inscrivez une application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="61c00-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="61c00-114">Ajoutez des jetons de code tooyour application toorequest.</span><span class="sxs-lookup"><span data-stu-id="61c00-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="61c00-115">Ajouter un jeton hello toouse du code pour l’interrogation hello API Graph et afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="61c00-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="61c00-116">Créer un projet de déploiement Cordova hello avec toutes les plateformes hello vous souhaitez tootarget, ajouter hello plug-in Cordova ADAL et tester des solutions de hello dans les émulateurs.</span><span class="sxs-lookup"><span data-stu-id="61c00-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61c00-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="61c00-117">Prerequisites</span></span>
<span data-ttu-id="61c00-118">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="61c00-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="61c00-119">Un client Azure AD où vous avez un compte disposant de droits de développement d’application.</span><span class="sxs-lookup"><span data-stu-id="61c00-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="61c00-120">Un environnement de développement qui a configuré toouse Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="61c00-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="61c00-121">Si vous les avez déjà configuré, passez directement toostep 1.</span><span class="sxs-lookup"><span data-stu-id="61c00-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="61c00-122">Si vous n’avez pas un locataire Azure AD, utilisez hello [obtenir des instructions sur la façon de tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="61c00-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="61c00-123">Si vous n’avez pas Apache Cordova sur votre ordinateur, installez des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="61c00-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="61c00-124">Git</span><span class="sxs-lookup"><span data-stu-id="61c00-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="61c00-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="61c00-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="61c00-126">[Cordova CLI](https://cordova.apache.org/) (peut être installé facilement via le Gestionnaire de package NPM : `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="61c00-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="61c00-127">Hello précédentes installations doit fonctionner sur hello PC et sur hello Mac.</span><span class="sxs-lookup"><span data-stu-id="61c00-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="61c00-128">Chaque plateforme cible présente une configuration requise différente :</span><span class="sxs-lookup"><span data-stu-id="61c00-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="61c00-129">toobuild et exécuter une application pour Tablet PC/PC Windows ou Windows Phone :</span><span class="sxs-lookup"><span data-stu-id="61c00-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="61c00-130">Installez [Visual Studio 2013 pour Windows Update 2 ou version ultérieure](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express ou autre version) ou [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="61c00-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="61c00-131">toobuild et exécuter une application pour iOS :</span><span class="sxs-lookup"><span data-stu-id="61c00-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="61c00-132">Installez Xcode 6.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="61c00-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="61c00-133">Téléchargez-le à partir de hello [site Apple Developer](http://developer.apple.com/downloads) ou hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="61c00-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="61c00-134">Installez [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="61c00-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="61c00-135">Vous pouvez l’utiliser des applications iOS toostart dans iOS Simulator depuis la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="61c00-136">(Vous pouvez l’installer facilement via hello Terminal Server : `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="61c00-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="61c00-137">toobuild et exécuter une application pour Android :</span><span class="sxs-lookup"><span data-stu-id="61c00-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="61c00-138">Installez le [Kit de développement Java (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou ultérieur.</span><span class="sxs-lookup"><span data-stu-id="61c00-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="61c00-139">Assurez-vous que `JAVA_HOME` (variable d’environnement) est correctement définie selon le chemin d’installation de JDK toohello (par exemple, C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="61c00-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="61c00-140">Installer [du SDK Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) et ajoutez hello `<android-sdk-location>\tools` emplacement (par exemple, C:\tools\Android\android-sdk\tools) tooyour `PATH` variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="61c00-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="61c00-141">Ouvrez le Gestionnaire de SDK Android (via hello Terminal Server, par exemple : `android`) et l’installer :</span><span class="sxs-lookup"><span data-stu-id="61c00-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="61c00-142">*Android 5.0.1 (API 21)*</span><span class="sxs-lookup"><span data-stu-id="61c00-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="61c00-143">*Android SDK Build Tools* version 19.1.0 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="61c00-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="61c00-144">*Android Support Repository* (modules complémentaires)</span><span class="sxs-lookup"><span data-stu-id="61c00-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="61c00-145">Hello du SDK Android ne fournit pas une instance d’émulateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="61c00-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="61c00-146">En exécutant `android avd` de hello Terminal Server, puis en sélectionnant **créer**, si vous souhaitez toorun hello des applications Android sur un émulateur.</span><span class="sxs-lookup"><span data-stu-id="61c00-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="61c00-147">Nous recommandons un niveau d’API de 19 ou plus.</span><span class="sxs-lookup"><span data-stu-id="61c00-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="61c00-148">Pour plus d’informations sur les options de création et d’émulateur Android hello, consultez [Gestionnaire AVD](http://developer.android.com/tools/help/avd-manager.html) sur le site de Android hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="61c00-149">Étape 1 : Inscrire une application auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="61c00-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="61c00-150">Cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="61c00-150">This step is optional.</span></span> <span data-ttu-id="61c00-151">Ce didacticiel fournit des valeurs préconfigurés, que vous pouvez utiliser toosee hello exemple en action sans effectuer toute mise en service dans votre propre locataire.</span><span class="sxs-lookup"><span data-stu-id="61c00-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="61c00-152">Toutefois, nous vous recommandons de réaliser cette étape et vous familiariser avec les processus hello, car elle sera nécessaire lorsque vous créez vos propres applications.</span><span class="sxs-lookup"><span data-stu-id="61c00-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="61c00-153">Azure AD émet tooonly jetons connu des applications.</span><span class="sxs-lookup"><span data-stu-id="61c00-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="61c00-154">Avant de pouvoir utiliser Azure AD à partir de votre application, vous devez toocreate une entrée pour celle-ci dans votre client.</span><span class="sxs-lookup"><span data-stu-id="61c00-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="61c00-155">tooregister une nouvelle application dans votre client :</span><span class="sxs-lookup"><span data-stu-id="61c00-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="61c00-156">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61c00-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="61c00-157">Sur la barre supérieure de hello, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="61c00-157">On hello top bar, click your account.</span></span> <span data-ttu-id="61c00-158">Bonjour **répertoire** , choisissez locataire hello AD Azure où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="61c00-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="61c00-159">Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="61c00-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="61c00-160">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="61c00-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="61c00-161">Suivez les invites hello et créer un **Application cliente Native**.</span><span class="sxs-lookup"><span data-stu-id="61c00-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="61c00-162">(Bien que les applications Cordova soient basées sur le langage HTML, nous créons ici une application cliente native.</span><span class="sxs-lookup"><span data-stu-id="61c00-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="61c00-163">Hello **Application cliente Native** doit être activée ou l’application hello ne fonctionne pas.)</span><span class="sxs-lookup"><span data-stu-id="61c00-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="61c00-164">**Nom** décrit toousers de votre application.</span><span class="sxs-lookup"><span data-stu-id="61c00-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="61c00-165">**URI de redirection** est hello URI qui a utilisé tooreturn jetons tooyour application.</span><span class="sxs-lookup"><span data-stu-id="61c00-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="61c00-166">Entrez **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="61c00-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="61c00-167">Une fois que vous avez terminé l’inscription, Azure AD assigne une application de tooyour ID unique d’application.</span><span class="sxs-lookup"><span data-stu-id="61c00-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="61c00-168">Vous aurez besoin de cette valeur dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="61c00-169">Vous pouvez le trouver sur l’onglet de l’application hello Hello l’application nouvellement créée.</span><span class="sxs-lookup"><span data-stu-id="61c00-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="61c00-170">toorun `DirSearchClient Sample`, accorder hello nouvellement créé application autorisation tooquery hello Azure AD Graph API :</span><span class="sxs-lookup"><span data-stu-id="61c00-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="61c00-171">À partir de hello **paramètres** page, sélectionnez **autorisations requises**, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="61c00-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="61c00-172">Pour hello application Azure Active Directory, sélectionnez **Microsoft Graph** comme hello API et ajouter hello **répertoire de hello Access en tant qu’utilisateur connecté hello** autorisation sous **délégués Autorisations**.</span><span class="sxs-lookup"><span data-stu-id="61c00-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="61c00-173">Cela permet à votre hello de tooquery d’application API Graph pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="61c00-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="61c00-174">Étape 2 : Cloner le référentiel d’application exemple hello</span><span class="sxs-lookup"><span data-stu-id="61c00-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="61c00-175">À partir de votre environnement ou de la ligne de commande, tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="61c00-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="61c00-176">Étape 3 : Créer l’application de Cordova hello</span><span class="sxs-lookup"><span data-stu-id="61c00-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="61c00-177">Il existe plusieurs façons toocreate Cordova applications.</span><span class="sxs-lookup"><span data-stu-id="61c00-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="61c00-178">Dans ce didacticiel, nous allons utiliser l’interface de ligne de commande de Cordova hello (CLI).</span><span class="sxs-lookup"><span data-stu-id="61c00-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="61c00-179">À partir de votre environnement ou de la ligne de commande, tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="61c00-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="61c00-180">Cette commande crée la structure de dossiers hello et génération de modèles automatique pour le projet de Cordova hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="61c00-181">Déplacer le dossier DirSearchClient toohello :</span><span class="sxs-lookup"><span data-stu-id="61c00-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="61c00-182">Copier le contenu de hello du projet de démarrage hello dans le sous-dossier de www hello à l’aide d’un gestionnaire de fichiers ou le hello commande dans votre interpréteur de commandes suivante :</span><span class="sxs-lookup"><span data-stu-id="61c00-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="61c00-183">Windows : `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="61c00-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="61c00-184">Mac : `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="61c00-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="61c00-185">Ajouter un plug-in de la liste d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="61c00-186">Cela est nécessaire pour l’appel d’API Graph de hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="61c00-187">Ajoutez toutes les plateformes hello que vous souhaitez toosupport.</span><span class="sxs-lookup"><span data-stu-id="61c00-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="61c00-188">toohave un exemple fonctionnel, vous devez tooexecute au moins l’un de hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="61c00-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="61c00-189">Notez que vous ne seront pas être iOS en mesure de tooemulate sur Windows ou émuler Windows sur un Mac.</span><span class="sxs-lookup"><span data-stu-id="61c00-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="61c00-190">Ajoutez hello ADAL pour le projet de tooyour plug-in Cordova :</span><span class="sxs-lookup"><span data-stu-id="61c00-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="61c00-191">Étape 4 : Ajouter des utilisateurs tooauthenticate de code et obtenir des jetons d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="61c00-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="61c00-192">application Hello que vous développez dans ce didacticiel fournit une fonctionnalité de recherche de répertoire simple.</span><span class="sxs-lookup"><span data-stu-id="61c00-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="61c00-193">Hello utilisateur peut taper alias hello de n’importe quel utilisateur dans le répertoire de hello et visualiser certains attributs de base.</span><span class="sxs-lookup"><span data-stu-id="61c00-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="61c00-194">projet de démarrage Hello contient la définition hello d’interface utilisateur de base de hello de l’application hello (dans www/index.html) et la structure hello qui relie des événements d’application de base, les liaisons d’interface utilisateur, cycles et les résultats de logique d’affichage (dans www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="61c00-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="61c00-195">Hello seule tâche pour vous est tooadd hello logique qui implémente les tâches d’identité.</span><span class="sxs-lookup"><span data-stu-id="61c00-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="61c00-196">Hello première chose toodo dans votre code est de présenter les valeurs de protocole hello Azure AD utilise pour identifier votre application et hello ressources que vous ciblez.</span><span class="sxs-lookup"><span data-stu-id="61c00-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="61c00-197">Ces valeurs seront ultérieurement sur les demandes de jeton de hello tooconstruct utilisé.</span><span class="sxs-lookup"><span data-stu-id="61c00-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="61c00-198">Insérez hello suivant extrait haut hello du fichier de index.js hello :</span><span class="sxs-lookup"><span data-stu-id="61c00-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="61c00-199">Hello `redirectUri` et `clientId` valeurs doivent correspondre les valeurs hello qui décrivent votre application dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61c00-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="61c00-200">Vous pouvez trouver ceux de hello **configurer** onglet hello portail Azure, comme décrit à l’étape 1, plus haut dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="61c00-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="61c00-201">Si vous avez choisi pour ne pas l’inscription d’une nouvelle application dans votre propre client, vous pouvez coller simplement les valeurs hello préconfiguré en l’état.</span><span class="sxs-lookup"><span data-stu-id="61c00-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="61c00-202">Vous pouvez ensuite voir en cours d’exécution exemple hello, bien que vous devez toujours créer votre propre entrée pour vos applications sont destinées à la production.</span><span class="sxs-lookup"><span data-stu-id="61c00-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="61c00-203">Ensuite, ajoutez le code de demande de jeton hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-203">Next, add hello token request code.</span></span> <span data-ttu-id="61c00-204">Insérer hello suivant extrait entre hello `search` et `renderData` définitions :</span><span class="sxs-lookup"><span data-stu-id="61c00-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="61c00-205">Examinons cette fonction en la décomposant en deux parties principales.</span><span class="sxs-lookup"><span data-stu-id="61c00-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="61c00-206">Cet exemple est conçu toowork avec n’importe quel client, comme toobeing opposé liée tooa d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="61c00-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="61c00-207">Il utilise hello « / common » point de terminaison, qui permet de n’importe quel compte hello utilisateur tooenter au moment de l’authentification et dirige les client de toohello hello demande à laquelle il appartient.</span><span class="sxs-lookup"><span data-stu-id="61c00-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="61c00-208">La première partie de la méthode hello inspecte hello cache ADAL toosee si un jeton est déjà stocké.</span><span class="sxs-lookup"><span data-stu-id="61c00-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="61c00-209">Dans ce cas, méthode hello utilise les locataires hello d'où provenance le jeton de hello pour la réinitialisation de la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="61c00-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="61c00-210">Cela est nécessaire tooavoid invites supplémentaires, car hello utilisation de « / courantes » toujours demandant hello utilisateur tooenter un nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="61c00-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="61c00-211">Hello deuxième partie de méthode hello effectue la demande de jeton correcte hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="61c00-212">Hello `acquireTokenSilentAsync` méthode demande tooreturn ADAL un jeton hello spécifié ressource sans affichage de n’importe quel UX.</span><span class="sxs-lookup"><span data-stu-id="61c00-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="61c00-213">Cela peut se produire si le cache de hello a déjà un jeton d’accès stocké, ou si un jeton d’actualisation peut être utilisé tooget un nouveau jeton d’accès sans affichage d’une invite.</span><span class="sxs-lookup"><span data-stu-id="61c00-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="61c00-214">Si cette tentative échoue, nous revenir `acquireTokenAsync`--ce qui invite visiblement hello utilisateur tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="61c00-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="61c00-215">Maintenant que nous avons le jeton de hello, nous pouvons enfin appeler hello API Graph et d’effectuer la requête de recherche hello que nous voulons.</span><span class="sxs-lookup"><span data-stu-id="61c00-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="61c00-216">Insérer hello suivant extrait de code ci-dessous hello `authenticate` définition :</span><span class="sxs-lookup"><span data-stu-id="61c00-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="61c00-217">fichiers de point de départ Hello fourni une expérience utilisateur simple pour l’entrée d’un alias de l’utilisateur dans une zone de texte.</span><span class="sxs-lookup"><span data-stu-id="61c00-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="61c00-218">Cette méthode utilise la valeur tooconstruct une requête, combiner avec le jeton d’accès hello, envoyer tooMicrosoft graphique et analyser les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="61c00-219">Hello `renderData` (méthode), déjà présente dans le fichier de point de départ de hello, prend en charge de visualisation des résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="61c00-220">Étape 5 : Exécuter l’application hello</span><span class="sxs-lookup"><span data-stu-id="61c00-220">Step 5: Run hello app</span></span>
<span data-ttu-id="61c00-221">Votre application est maintenant prête toorun.</span><span class="sxs-lookup"><span data-stu-id="61c00-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="61c00-222">Il fonctionne est simple : au démarrage de l’application hello, entrez l’alias hello de hello utilisateur toolook des, puis cliquez sur le bouton de hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="61c00-223">Vous êtes invité à vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="61c00-223">You're prompted for authentication.</span></span> <span data-ttu-id="61c00-224">Lors de l’authentification réussie et la recherche réussit, les attributs hello de hello recherché utilisateur sont affichés.</span><span class="sxs-lookup"><span data-stu-id="61c00-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="61c00-225">Les exécutions suivantes effectuera hello recherche sans affichage d’une invite, grâce présence toohello Hello précédemment acquis jeton dans le cache.</span><span class="sxs-lookup"><span data-stu-id="61c00-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="61c00-226">étapes de concrète Hello pour exécuter l’application hello varient selon la plateforme.</span><span class="sxs-lookup"><span data-stu-id="61c00-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="61c00-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="61c00-227">Windows 10</span></span>
   <span data-ttu-id="61c00-228">Tablette/PC : `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="61c00-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="61c00-229">Mobile (nécessite un tooa de périphérique connecté PC Windows 10 Mobile) :`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="61c00-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="61c00-230">Au cours de hello exécutez d’abord, vous pouvez être invité toosign dans une licence de développeur.</span><span class="sxs-lookup"><span data-stu-id="61c00-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="61c00-231">Pour plus d’informations, consultez [Obtenir une licence de développeur](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="61c00-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="61c00-232">Tablette/PC Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="61c00-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="61c00-233">Au cours de hello exécutez d’abord, vous pouvez être invité toosign dans une licence de développeur.</span><span class="sxs-lookup"><span data-stu-id="61c00-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="61c00-234">Pour plus d’informations, consultez [Obtenir une licence de développeur](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="61c00-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="61c00-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="61c00-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="61c00-236">toorun sur un appareil connecté :`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="61c00-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="61c00-237">toorun sur l’émulateur par défaut de hello :`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="61c00-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="61c00-238">Utilisez `cordova run windows --list -- --phone` toosee toutes les cibles disponibles et `cordova run windows --target=<target_name> -- --phone` application hello de toorun sur un émulateur ou un périphérique spécifique (par exemple, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="61c00-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="61c00-239">Android</span><span class="sxs-lookup"><span data-stu-id="61c00-239">Android</span></span>
   <span data-ttu-id="61c00-240">toorun sur un appareil connecté :`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="61c00-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="61c00-241">toorun sur l’émulateur par défaut de hello :`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="61c00-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="61c00-242">Assurez-vous que vous avez créé une instance de l’émulateur à l’aide du gestionnaire AVD, comme décrit précédemment dans la section « Conditions préalables » de hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="61c00-243">Utilisez `cordova run android --list` toosee toutes les cibles disponibles et `cordova run android --target=<target_name>` application hello de toorun sur un émulateur ou un périphérique spécifique (par exemple, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="61c00-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="61c00-244">iOS</span><span class="sxs-lookup"><span data-stu-id="61c00-244">iOS</span></span>
   <span data-ttu-id="61c00-245">toorun sur un appareil connecté :`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="61c00-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="61c00-246">toorun sur l’émulateur par défaut de hello :`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="61c00-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="61c00-247">Assurez-vous que vous avez hello `ios-sim` toorun package installé sur l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="61c00-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="61c00-248">Pour plus d’informations, consultez hello « conditions préalables » section.</span><span class="sxs-lookup"><span data-stu-id="61c00-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="61c00-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61c00-249">Next steps</span></span>
<span data-ttu-id="61c00-250">Pour référence, l’exemple hello terminée (sans les valeurs de configuration) est disponible dans [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="61c00-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="61c00-251">Vous pouvez maintenant les scénarios de transfert sur toomore avancé (et plus intéressantes).</span><span class="sxs-lookup"><span data-stu-id="61c00-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="61c00-252">Vous souhaiterez peut-être tootry : [sécuriser une API Web de Node.js avec Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="61c00-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
