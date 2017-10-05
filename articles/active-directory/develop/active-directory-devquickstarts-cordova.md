---
title: "Bien démarrer avec Azure Cordova | Microsoft Docs"
description: "Création d’une application Cordova qui s’intègre avec Azure AD pour la connexion et appelle les API protégées par Azure AD en utilisant OAuth."
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
ms.openlocfilehash: d9f53148787729d29a0a89cce1b8b2b83ba228f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="2e296-103">Intégration d’Azure AD avec une application Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="2e296-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="2e296-104">Apache Cordova permet de développer des applications HTML5/JavaScript exécutables sur des appareils mobiles en tant qu’applications natives à part entière.</span><span class="sxs-lookup"><span data-stu-id="2e296-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="2e296-105">Avec Azure Active Directory (Azure AD), vous pouvez ajouter des fonctionnalités d’authentification d’entreprise à vos applications Cordova.</span><span class="sxs-lookup"><span data-stu-id="2e296-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span></span>

<span data-ttu-id="2e296-106">Un plug-in Cordova encapsule des kits de développement logiciels (SDK) natifs Azure AD sur iOS, Android, Windows Store et Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="2e296-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="2e296-107">En utilisant ce plug-in, vous pouvez améliorer votre application pour qu’elle prenne en charge la connexion avec les comptes Windows Server Active Directory de vos utilisateurs, qu’elle puisse accéder aux API Office 365 et Azure, et même qu’elle contribue à protéger les appels à votre API web personnalisée.</span><span class="sxs-lookup"><span data-stu-id="2e296-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span></span>

<span data-ttu-id="2e296-108">Dans ce didacticiel, nous allons utiliser le plug-in Apache Cordova pour la bibliothèque d’authentification Active Directory (ADAL) afin d’améliorer une application simple en ajoutant les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="2e296-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span></span>

* <span data-ttu-id="2e296-109">Avec quelques lignes de code seulement, authentifier un utilisateur et obtenir un jeton.</span><span class="sxs-lookup"><span data-stu-id="2e296-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="2e296-110">Utiliser ce jeton pour appeler l’API Graph afin d’interroger ce répertoire et d’afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="2e296-110">Use that token to invoke the Graph API to query that directory and display the results.</span></span>  
* <span data-ttu-id="2e296-111">Utiliser le cache de jetons ADAL pour limiter les invites d’authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2e296-111">Use the ADAL token cache to minimize authentication prompts for the user.</span></span>

<span data-ttu-id="2e296-112">Pour apporter ces améliorations, vous devez :</span><span class="sxs-lookup"><span data-stu-id="2e296-112">To make those improvements, you need to:</span></span>

1. <span data-ttu-id="2e296-113">inscrivez une application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="2e296-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="2e296-114">ajouter du code pour que votre application demande des jetons ;</span><span class="sxs-lookup"><span data-stu-id="2e296-114">Add code to your app to request tokens.</span></span>
3. <span data-ttu-id="2e296-115">ajouter du code pour utiliser le jeton pour l’interrogation de l’API Graph et afficher les résultats ;</span><span class="sxs-lookup"><span data-stu-id="2e296-115">Add code to use the token for querying the Graph API and display results.</span></span>
4. <span data-ttu-id="2e296-116">créer le projet de déploiement Cordova avec toutes les plateformes à cibler, ajouter le plug-in Cordova ADAL, puis tester la solution dans des émulateurs.</span><span class="sxs-lookup"><span data-stu-id="2e296-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e296-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2e296-117">Prerequisites</span></span>
<span data-ttu-id="2e296-118">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2e296-118">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="2e296-119">Un client Azure AD où vous avez un compte disposant de droits de développement d’application.</span><span class="sxs-lookup"><span data-stu-id="2e296-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="2e296-120">Un environnement de développement configuré pour exécuter Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="2e296-120">A development environment that's configured to use Apache Cordova.</span></span>  

<span data-ttu-id="2e296-121">Si vous disposez déjà de ces éléments, passez directement à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="2e296-121">If you have both already set up, proceed directly to step 1.</span></span>

<span data-ttu-id="2e296-122">Si vous n’avez pas de client Azure AD, suivez la [procédure permettant d’en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="2e296-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="2e296-123">Si Apache Cordova n’est pas configuré sur votre ordinateur, installez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2e296-123">If you don't have Apache Cordova set up on your machine, install the following:</span></span>

* [<span data-ttu-id="2e296-124">Git</span><span class="sxs-lookup"><span data-stu-id="2e296-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="2e296-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2e296-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="2e296-126">[Cordova CLI](https://cordova.apache.org/) (peut être installé facilement via le Gestionnaire de package NPM : `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="2e296-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="2e296-127">Les installations précédentes doivent en principe fonctionner aussi bien sur PC que sur Mac.</span><span class="sxs-lookup"><span data-stu-id="2e296-127">The preceding installations should work both on the PC and on the Mac.</span></span>

<span data-ttu-id="2e296-128">Chaque plateforme cible présente une configuration requise différente :</span><span class="sxs-lookup"><span data-stu-id="2e296-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="2e296-129">Pour générer et exécuter une application pour une tablette/un PC Windows ou Windows Phone :</span><span class="sxs-lookup"><span data-stu-id="2e296-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="2e296-130">Installez [Visual Studio 2013 pour Windows Update 2 ou version ultérieure](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express ou autre version) ou [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="2e296-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="2e296-131">Pour générer et exécuter une application pour iOS :</span><span class="sxs-lookup"><span data-stu-id="2e296-131">To build and run an app for iOS:</span></span>

  * <span data-ttu-id="2e296-132">Installez Xcode 6.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2e296-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="2e296-133">Téléchargez-le à partir du [site Apple Developer](http://developer.apple.com/downloads) ou du [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="2e296-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="2e296-134">Installez [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="2e296-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="2e296-135">Vous pouvez l’utiliser pour démarrer des applications iOS dans iOS Simulator à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="2e296-135">You can use it to start iOS apps in iOS Simulator from the command line.</span></span> <span data-ttu-id="2e296-136">(Vous pouvez l’installer facilement via le terminal : `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="2e296-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="2e296-137">Pour générer et exécuter une application pour Android :</span><span class="sxs-lookup"><span data-stu-id="2e296-137">To build and run an app for Android:</span></span>

  * <span data-ttu-id="2e296-138">Installez le [Kit de développement Java (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou ultérieur.</span><span class="sxs-lookup"><span data-stu-id="2e296-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="2e296-139">Assurez-vous que la variable d’environnement `JAVA_HOME` est correctement définie en fonction du chemin d’installation du JDK (par exemple, C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="2e296-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="2e296-140">Installez le [Kit de développement logiciel (SDK) Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) et ajoutez l’emplacement `<android-sdk-location>\tools` (par exemple, C:\tools\Android\android-sdk\tools) pour votre variable d’environnement `PATH`.</span><span class="sxs-lookup"><span data-stu-id="2e296-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span></span>
  * <span data-ttu-id="2e296-141">Ouvrez Android SDK Manager (par exemple, via le terminal : `android`) et installez :</span><span class="sxs-lookup"><span data-stu-id="2e296-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span></span>
    * <span data-ttu-id="2e296-142">*Android 5.0.1 (API 21)* </span><span class="sxs-lookup"><span data-stu-id="2e296-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="2e296-143">*Android SDK Build Tools* version 19.1.0 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="2e296-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="2e296-144">*Android Support Repository* (modules complémentaires)</span><span class="sxs-lookup"><span data-stu-id="2e296-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="2e296-145">Le Kit de développement logiciel (SDK) Android ne fournit pas d’instance d’émulateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="2e296-145">The Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="2e296-146">Si vous souhaitez exécuter l’application Android sur un émulateur, créez une instance en exécutant `android avd` à partir du terminal, puis en sélectionnant **Create** (Créer).</span><span class="sxs-lookup"><span data-stu-id="2e296-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span></span> <span data-ttu-id="2e296-147">Nous recommandons un niveau d’API de 19 ou plus.</span><span class="sxs-lookup"><span data-stu-id="2e296-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="2e296-148">Pour plus d’informations sur les options de création et l’émulateur Android, consultez [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) sur le site Android.</span><span class="sxs-lookup"><span data-stu-id="2e296-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="2e296-149">Étape 1 : Inscrire une application auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e296-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="2e296-150">Cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="2e296-150">This step is optional.</span></span> <span data-ttu-id="2e296-151">Ce didacticiel fournit des valeurs préconfigurées que vous pouvez utiliser pour voir l’exemple à l’œuvre sans effectuer d’approvisionnement dans votre propre client.</span><span class="sxs-lookup"><span data-stu-id="2e296-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="2e296-152">Toutefois, nous vous recommandons d’effectuer cette étape et de vous familiariser avec le processus, car vous devrez y faire appel lorsque vous créerez vos propres applications.</span><span class="sxs-lookup"><span data-stu-id="2e296-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="2e296-153">Azure AD émet uniquement des jetons pour les applications connues.</span><span class="sxs-lookup"><span data-stu-id="2e296-153">Azure AD issues tokens to only known applications.</span></span> <span data-ttu-id="2e296-154">Avant de pouvoir utiliser Azure AD à partir de votre application, vous devez créer une entrée pour elle dans votre client.</span><span class="sxs-lookup"><span data-stu-id="2e296-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span></span> <span data-ttu-id="2e296-155">Pour inscrire une nouvelle application dans votre client :</span><span class="sxs-lookup"><span data-stu-id="2e296-155">To register a new application in your tenant:</span></span>

1. <span data-ttu-id="2e296-156">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2e296-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2e296-157">Dans la barre supérieure, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="2e296-157">On the top bar, click your account.</span></span> <span data-ttu-id="2e296-158">Dans la liste **Répertoire**, choisissez le locataire Azure AD auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="2e296-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="2e296-159">Dans le volet gauche, cliquez sur **Plus de services**, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e296-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="2e296-160">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2e296-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="2e296-161">Suivez les invites à l’écran et créez une **application cliente native**.</span><span class="sxs-lookup"><span data-stu-id="2e296-161">Follow the prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="2e296-162">(Bien que les applications Cordova soient basées sur le langage HTML, nous créons ici une application cliente native.</span><span class="sxs-lookup"><span data-stu-id="2e296-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="2e296-163">L’option **Application cliente native** doit être sélectionnée, sinon l’application ne fonctionnera pas.)</span><span class="sxs-lookup"><span data-stu-id="2e296-163">The **Native Client Application** option must be selected, or the application won't work.)</span></span>
  * <span data-ttu-id="2e296-164">**Nom** décrit votre application pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2e296-164">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="2e296-165">**URI de redirection** correspond à l’URI utilisé pour renvoyer les jetons à votre application.</span><span class="sxs-lookup"><span data-stu-id="2e296-165">**Redirect URI** is the URI that's used to return tokens to your app.</span></span> <span data-ttu-id="2e296-166">Entrez **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="2e296-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="2e296-167">Une fois l’inscription terminée, Azure AD affecte un ID d’application unique à votre application.</span><span class="sxs-lookup"><span data-stu-id="2e296-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="2e296-168">Vous aurez besoin de cette valeur dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="2e296-168">You’ll need this value in the next sections.</span></span> <span data-ttu-id="2e296-169">Vous le trouverez dans l’onglet Application de la nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="2e296-169">You can find it on the application tab of the newly created app.</span></span>

<span data-ttu-id="2e296-170">Pour exécuter `DirSearchClient Sample`, autorisez la nouvelle application à interroger l’API Azure AD Graph :</span><span class="sxs-lookup"><span data-stu-id="2e296-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span></span>

1. <span data-ttu-id="2e296-171">Dans la page **Paramètres**, sélectionnez **Autorisations requises**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2e296-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="2e296-172">Pour l’application Azure Active Directory, sélectionnez l’API **Microsoft Graph**, puis ajoutez l’autorisation **Access the directory as the signed-in user** (Accéder au répertoire en tant qu’utilisateur connecté) sous **Autorisations déléguées**.</span><span class="sxs-lookup"><span data-stu-id="2e296-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="2e296-173">Cela permet à votre application d’interroger l’API Graph concernant les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2e296-173">This enables your application to query the Graph API for users.</span></span>

## <a name="step-2-clone-the-sample-app-repository"></a><span data-ttu-id="2e296-174">Étape 2 : Cloner l’exemple de référentiel d’application</span><span class="sxs-lookup"><span data-stu-id="2e296-174">Step 2: Clone the sample app repository</span></span>
<span data-ttu-id="2e296-175">À partir de votre environnement ou de la ligne de commande, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2e296-175">From your shell or command line, type the following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-the-cordova-app"></a><span data-ttu-id="2e296-176">Étape 3 : Créer l’application Cordova</span><span class="sxs-lookup"><span data-stu-id="2e296-176">Step 3: Create the Cordova app</span></span>
<span data-ttu-id="2e296-177">Il existe plusieurs moyens de créer des applications Cordova.</span><span class="sxs-lookup"><span data-stu-id="2e296-177">There are multiple ways to create Cordova applications.</span></span> <span data-ttu-id="2e296-178">Dans ce didacticiel, nous allons utiliser l’interface de ligne de commande (CLI) Cordova.</span><span class="sxs-lookup"><span data-stu-id="2e296-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="2e296-179">À partir de votre environnement ou de la ligne de commande, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2e296-179">From your shell or command line, type the following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="2e296-180">Cette commande permet de créer la structure de dossiers et la structure du projet Cordova.</span><span class="sxs-lookup"><span data-stu-id="2e296-180">That command creates the folder structure and scaffolding for the Cordova project.</span></span>

2. <span data-ttu-id="2e296-181">Accédez au nouveau dossier DirSearchClient :</span><span class="sxs-lookup"><span data-stu-id="2e296-181">Move to the new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="2e296-182">Copiez le contenu du projet de démarrage dans le sous-dossier www en utilisant un gestionnaire de fichiers ou la commande suivante dans votre interpréteur de commandes :</span><span class="sxs-lookup"><span data-stu-id="2e296-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span></span>

  * <span data-ttu-id="2e296-183">Windows : `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="2e296-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="2e296-184">Mac : `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="2e296-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="2e296-185">Ajoutez le plug-in d’autorisation (whitelist).</span><span class="sxs-lookup"><span data-stu-id="2e296-185">Add the whitelist plug-in.</span></span> <span data-ttu-id="2e296-186">Celui-ci est nécessaire pour appeler l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="2e296-186">This is necessary for invoking the Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="2e296-187">Ajoutez toutes les plateformes que vous souhaitez prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="2e296-187">Add all the platforms that you want to support.</span></span> <span data-ttu-id="2e296-188">Pour avoir un exemple fonctionnel, vous devez exécuter au moins une des commandes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2e296-188">To have a working sample, you need to execute at least one of the following commands.</span></span> <span data-ttu-id="2e296-189">Notez que vous ne pouvez pas émuler iOS sur Windows ou Windows sur un Mac.</span><span class="sxs-lookup"><span data-stu-id="2e296-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="2e296-190">Ajoutez la bibliothèque ADAL pour le plug-in Cordova dans votre projet :</span><span class="sxs-lookup"><span data-stu-id="2e296-190">Add the ADAL for Cordova plug-in to your project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-to-authenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="2e296-191">Étape 4 : Ajouter le code pour authentifier les utilisateurs et obtenir des jetons d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e296-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="2e296-192">L’application que vous développez dans ce didacticiel fournira une fonctionnalité simple de recherche dans l’annuaire.</span><span class="sxs-lookup"><span data-stu-id="2e296-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="2e296-193">L’utilisateur pourra taper l’alias de n’importe quel utilisateur de l’annuaire pour visualiser certains attributs de base.</span><span class="sxs-lookup"><span data-stu-id="2e296-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span></span> <span data-ttu-id="2e296-194">Le projet de démarrage contient la définition de l’interface utilisateur de base de l’application (dans www/index.html) et la génération de modèles automatique qui associe les cycles d’événements des applications, les liaisons d’interface utilisateur et la logique d’affichage des résultats (dans www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="2e296-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="2e296-195">Vous n’avez plus qu’à ajouter la logique d’implémentation des tâches d’identité.</span><span class="sxs-lookup"><span data-stu-id="2e296-195">The only task left for you is to add the logic that implements identity tasks.</span></span>

<span data-ttu-id="2e296-196">La première chose à faire dans votre code est d’introduire les valeurs de protocole utilisées par Azure AD pour identifier votre application et les ressources que vous ciblez.</span><span class="sxs-lookup"><span data-stu-id="2e296-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span></span> <span data-ttu-id="2e296-197">Ces valeurs sont ensuite utilisées pour créer les demandes de jeton.</span><span class="sxs-lookup"><span data-stu-id="2e296-197">Those values will be used to construct the token requests later on.</span></span> <span data-ttu-id="2e296-198">Insérez l’extrait de code suivant en haut du fichier index.js :</span><span class="sxs-lookup"><span data-stu-id="2e296-198">Insert the following snippet at the top of the index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="2e296-199">Les valeurs `redirectUri` et `clientId` doivent correspondre à celles décrivant votre application dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e296-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span></span> <span data-ttu-id="2e296-200">Vous pouvez les trouver dans l’onglet **Configurer** du portail Azure, comme décrit à l’étape 1 plus haut dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2e296-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="2e296-201">Si vous avez choisi de ne pas inscrire une nouvelle application dans votre propre client, vous pouvez simplement coller les valeurs préconfigurées sans les modifier.</span><span class="sxs-lookup"><span data-stu-id="2e296-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span></span> <span data-ttu-id="2e296-202">Vous pourrez alors voir l’exemple exécuté. Cependant, notez que vous devez toujours créer votre propre entrée pour vos applications de production.</span><span class="sxs-lookup"><span data-stu-id="2e296-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="2e296-203">Ensuite, ajoutez le code de demande de jeton.</span><span class="sxs-lookup"><span data-stu-id="2e296-203">Next, add the token request code.</span></span> <span data-ttu-id="2e296-204">Insérez l’extrait de code suivant entre les définitions `search` et `renderData` :</span><span class="sxs-lookup"><span data-stu-id="2e296-204">Insert the following snippet between the `search` and `renderData` definitions:</span></span>

```javascript
    // Shows the user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="2e296-205">Examinons cette fonction en la décomposant en deux parties principales.</span><span class="sxs-lookup"><span data-stu-id="2e296-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="2e296-206">Cet exemple est conçu pour fonctionner avec n’importe quel client.</span><span class="sxs-lookup"><span data-stu-id="2e296-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span></span> <span data-ttu-id="2e296-207">Il utilise le point de terminaison « /common », ce qui permet à l’utilisateur d’entrer n’importe quel compte au moment de l’authentification et de rediriger la demande au client auquel elle appartient.</span><span class="sxs-lookup"><span data-stu-id="2e296-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span></span>

<span data-ttu-id="2e296-208">La première partie de la méthode inspecte le cache de la bibliothèque ADAL pour voir si un jeton y est déjà stocké.</span><span class="sxs-lookup"><span data-stu-id="2e296-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span></span> <span data-ttu-id="2e296-209">Si c’est le cas, elle utilise les clients d’où le jeton provient pour réinitialiser la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="2e296-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span></span> <span data-ttu-id="2e296-210">Cela est nécessaire pour éviter les invites supplémentaires, car l’utilisation de « /common » génère toujours une invite demandant à l’utilisateur d’entrer un nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="2e296-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="2e296-211">La deuxième partie de la méthode effectue la demande de jeton appropriée.</span><span class="sxs-lookup"><span data-stu-id="2e296-211">The second part of the method performs the proper token request.</span></span> <span data-ttu-id="2e296-212">La méthode `acquireTokenSilentAsync` demande à la bibliothèque ADAL de renvoyer un jeton pour la ressource spécifiée sans afficher d’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2e296-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span></span> <span data-ttu-id="2e296-213">Cela peut se produire si le cache a déjà un jeton d’accès stocké approprié ou si un jeton d’actualisation peut être utilisé pour obtenir un nouveau jeton d’accès sans afficher d’invite.</span><span class="sxs-lookup"><span data-stu-id="2e296-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span></span> <span data-ttu-id="2e296-214">Si cette tentative échoue, nous revenons à `acquireTokenAsync`, qui affichera une invite pour demander à l’utilisateur de s’authentifier.</span><span class="sxs-lookup"><span data-stu-id="2e296-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span></span>

```javascript
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
```
<span data-ttu-id="2e296-215">Maintenant que nous avons le jeton, nous pouvons enfin appeler l’API Graph et effectuer la requête de recherche souhaitée.</span><span class="sxs-lookup"><span data-stu-id="2e296-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span></span> <span data-ttu-id="2e296-216">Insérez l’extrait de code suivant en dessous de la définition `authenticate` :</span><span class="sxs-lookup"><span data-stu-id="2e296-216">Insert the following snippet below the `authenticate` definition:</span></span>

```javascript
// Makes an API call to receive the user list
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
<span data-ttu-id="2e296-217">Les fichiers de départ fournissaient une expérience utilisateur simple pour la saisie de l’alias d’un utilisateur dans une zone de texte.</span><span class="sxs-lookup"><span data-stu-id="2e296-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="2e296-218">Cette méthode utilise cette valeur pour construire une requête, l’associer au jeton d’accès, l’envoyer à Microsoft Graph et analyser les résultats.</span><span class="sxs-lookup"><span data-stu-id="2e296-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span></span> <span data-ttu-id="2e296-219">La méthode `renderData`, déjà présente dans le fichier de départ, s’occupe de visualiser les résultats.</span><span class="sxs-lookup"><span data-stu-id="2e296-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span></span>

## <a name="step-5-run-the-app"></a><span data-ttu-id="2e296-220">Étape 5 : Exécuter l’application</span><span class="sxs-lookup"><span data-stu-id="2e296-220">Step 5: Run the app</span></span>
<span data-ttu-id="2e296-221">Votre application est maintenant prête à être exécutée.</span><span class="sxs-lookup"><span data-stu-id="2e296-221">Your app is finally ready to run.</span></span> <span data-ttu-id="2e296-222">Son fonctionnement est simple : lorsque l’application démarre, entrez l’alias de l’utilisateur que vous souhaitez rechercher, puis cliquez sur le bouton.</span><span class="sxs-lookup"><span data-stu-id="2e296-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span></span> <span data-ttu-id="2e296-223">Vous êtes invité à vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="2e296-223">You're prompted for authentication.</span></span> <span data-ttu-id="2e296-224">Une fois l’authentification et la recherche réussies, les attributs de l’utilisateur recherché s’affichent.</span><span class="sxs-lookup"><span data-stu-id="2e296-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span></span>

<span data-ttu-id="2e296-225">Les exécutions suivantes effectuent la recherche sans afficher d’invite, grâce à la présence dans le cache du jeton obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="2e296-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span></span>

<span data-ttu-id="2e296-226">Les étapes concrètes pour l’exécution de l’application varient selon la plateforme.</span><span class="sxs-lookup"><span data-stu-id="2e296-226">The concrete steps for running the app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="2e296-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="2e296-227">Windows 10</span></span>
   <span data-ttu-id="2e296-228">Tablette/PC : `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="2e296-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="2e296-229">Mobile (nécessite un appareil Windows 10 Mobile connecté à un PC) : `cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="2e296-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="2e296-230">Lors de la première exécution, vous pouvez être invité à vous connecter pour obtenir une licence de développeur.</span><span class="sxs-lookup"><span data-stu-id="2e296-230">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="2e296-231">Pour plus d’informations, consultez [Obtenir une licence de développeur](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e296-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="2e296-232">Tablette/PC Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="2e296-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="2e296-233">Lors de la première exécution, vous pouvez être invité à vous connecter pour obtenir une licence de développeur.</span><span class="sxs-lookup"><span data-stu-id="2e296-233">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="2e296-234">Pour plus d’informations, consultez [Obtenir une licence de développeur](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e296-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="2e296-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="2e296-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="2e296-236">Pour une exécution sur un appareil connecté : `cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="2e296-236">To run on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="2e296-237">Pour une exécution sur l’émulateur par défaut : `cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="2e296-237">To run on the default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="2e296-238">Utilisez `cordova run windows --list -- --phone` pour voir toutes les cibles disponibles et `cordova run windows --target=<target_name> -- --phone` pour exécuter l’application sur un appareil ou un émulateur spécifique (par exemple, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="2e296-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="2e296-239">Android</span><span class="sxs-lookup"><span data-stu-id="2e296-239">Android</span></span>
   <span data-ttu-id="2e296-240">Pour une exécution sur un appareil connecté : `cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="2e296-240">To run on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="2e296-241">Pour une exécution sur l’émulateur par défaut : `cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="2e296-241">To run on the default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="2e296-242">Assurez-vous que vous avez créé une instance d’émulateur à l’aide d’AVD Manager, comme expliqué plus haut dans la section Composants requis.</span><span class="sxs-lookup"><span data-stu-id="2e296-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span></span>

   <span data-ttu-id="2e296-243">Utilisez `cordova run android --list` pour voir toutes les cibles disponibles et `cordova run android --target=<target_name>` pour exécuter l’application sur un appareil ou un émulateur spécifique (par exemple, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="2e296-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="2e296-244">iOS</span><span class="sxs-lookup"><span data-stu-id="2e296-244">iOS</span></span>
   <span data-ttu-id="2e296-245">Pour une exécution sur un appareil connecté : `cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="2e296-245">To run on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="2e296-246">Pour une exécution sur l’émulateur par défaut : `cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="2e296-246">To run on the default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="2e296-247">Pour une exécution sur l’émulateur, assurez-vous que vous avez installé le package `ios-sim`.</span><span class="sxs-lookup"><span data-stu-id="2e296-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span></span> <span data-ttu-id="2e296-248">Pour plus d’informations, consultez la section Composants requis.</span><span class="sxs-lookup"><span data-stu-id="2e296-248">For more information, see the "Prerequisites" section.</span></span>

    Use `cordova run ios --list` to see all available targets and `cordova run ios --target=<target_name>` to run the application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` to see additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="2e296-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e296-249">Next steps</span></span>
<span data-ttu-id="2e296-250">Pour référence, l’exemple terminé (sans vos valeurs de configuration) est disponible dans [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="2e296-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="2e296-251">Vous pouvez maintenant passer à des scénarios plus avancés (et plus intéressants).</span><span class="sxs-lookup"><span data-stu-id="2e296-251">You can now move on to more advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="2e296-252">Par exemple : [Sécurisation d’une API web Node.js avec Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2e296-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
