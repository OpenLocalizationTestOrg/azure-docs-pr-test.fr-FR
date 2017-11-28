---
title: "Prise en main d’Azure AD Android | Microsoft Docs"
description: "Création d’une application Android qui s’intègre avec Azure AD pour la connexion et appelle des API protégées par Azure AD en utilisant OAuth."
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
ms.openlocfilehash: 746cad19093fd2a1ad23ddd9412394f8d9da331c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="a1601-103">Intégration d’Azure AD dans une application Android</span><span class="sxs-lookup"><span data-stu-id="a1601-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="a1601-104">Essayez la version préliminaire de notre nouveau [portail des développeurs](https://identity.microsoft.com/Docs/Android), qui vous permettra de devenir opérationnel avec Azure AD en quelques minutes seulement.</span><span class="sxs-lookup"><span data-stu-id="a1601-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="a1601-105">Le portail des développeurs vous guidera tout au long du processus d’inscription d’une application et d’intégration d’Azure AD dans votre code.</span><span class="sxs-lookup"><span data-stu-id="a1601-105">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="a1601-106">Une fois que vous aurez terminé, vous disposerez d’une application simple capable d’authentifier les utilisateurs dans votre client et d’un serveur principal qui peut accepter les jetons et effectuer la validation.</span><span class="sxs-lookup"><span data-stu-id="a1601-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="a1601-107">Si vous développez une application de bureau, Azure Active Directory (Azure AD) facilite l’authentification de vos utilisateurs en utilisant leurs comptes Active Directory locaux.</span><span class="sxs-lookup"><span data-stu-id="a1601-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="a1601-108">Il permet également à votre application d’utiliser en toute sécurité une API web protégée par Azure AD, telle que l’API Office 365 ou Azure.</span><span class="sxs-lookup"><span data-stu-id="a1601-108">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="a1601-109">Pour les clients Android qui doivent accéder à des ressources protégées, Azure AD fournit la bibliothèque d’authentification Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="a1601-109">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="a1601-110">Cette bibliothèque a pour seule fonction de simplifier l’obtention des jetons d’accès pour votre application.</span><span class="sxs-lookup"><span data-stu-id="a1601-110">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="a1601-111">Pour illustrer sa facilité d’utilisation, nous allons créer une application de liste de tâches Android qui effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="a1601-111">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="a1601-112">obtention de jetons d’accès pour appeler une API To-Do List à l’aide du [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx) ;</span><span class="sxs-lookup"><span data-stu-id="a1601-112">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="a1601-113">obtention de la liste des tâches d’un utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="a1601-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="a1601-114">déconnexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a1601-114">Signs out users.</span></span>

<span data-ttu-id="a1601-115">Pour commencer, vous avez besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="a1601-115">To get started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="a1601-116">Si vous ne disposez pas encore d’un client, [découvrez comment en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="a1601-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="a1601-117">Étape 1 : Téléchargement et exécution de l’exemple de serveur TODO d’API REST Node.js</span><span class="sxs-lookup"><span data-stu-id="a1601-117">Step 1: Download and run the Node.js REST API TODO sample server</span></span>
<span data-ttu-id="a1601-118">L’exemple TODO d’API REST Node.js est écrit spécifiquement pour fonctionner avec notre exemple existant pour la création d’une API REST To-Do à client unique pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1601-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="a1601-119">Il s’agit d’un composant requis pour le démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="a1601-119">This is a prerequisite for the Quick Start.</span></span>

<span data-ttu-id="a1601-120">Pour plus d’informations sur la configuration associée, consultez nos exemples existants dans [Exemple de service d’API REST Microsoft Azure Active Directory pour Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a1601-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="a1601-121">Étape 2 : Inscription de votre API web auprès de votre client Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1601-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="a1601-122">Active Directory prend en charge l’ajout de deux types d’application :</span><span class="sxs-lookup"><span data-stu-id="a1601-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="a1601-123">les API web qui offrent des services aux utilisateurs ;</span><span class="sxs-lookup"><span data-stu-id="a1601-123">Web APIs that offer services to users</span></span>
- <span data-ttu-id="a1601-124">les applications (exécutées sur le web ou sur un appareil) qui accèdent à ces API web</span><span class="sxs-lookup"><span data-stu-id="a1601-124">Applications (running either on the web or on a device) that access those web APIs</span></span>

<span data-ttu-id="a1601-125">Au cours de cette étape, vous allez inscrire l’API web que vous exécutez localement pour tester cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a1601-125">In this step, you're registering the web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="a1601-126">Normalement, cette API web est un service REST qui offre les fonctionnalités auxquelles vous souhaitez qu’une application ait accès.</span><span class="sxs-lookup"><span data-stu-id="a1601-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span></span> <span data-ttu-id="a1601-127">Azure AD peut contribuer à protéger n’importe quel point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="a1601-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="a1601-128">Nous partons du principe que vous inscrivez l’API REST TODO mentionnée précédemment.</span><span class="sxs-lookup"><span data-stu-id="a1601-128">We're assuming that you're registering the TODO REST API referenced earlier.</span></span> <span data-ttu-id="a1601-129">Cependant, cela fonctionne pour toute API web que vous voulez protéger à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a1601-129">But this works for any web API that you want Azure Active Directory to help protect.</span></span>

1. <span data-ttu-id="a1601-130">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a1601-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a1601-131">Dans la barre supérieure, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="a1601-131">On the top bar, click your account.</span></span> <span data-ttu-id="a1601-132">Dans la liste **Répertoire**, choisissez le locataire Azure AD auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="a1601-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="a1601-133">Dans le volet gauche, cliquez sur **Plus de services**, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1601-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="a1601-134">Cliquez sur **Inscriptions d’applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a1601-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="a1601-135">Entrez un nom convivial pour l’application (par exemple, **TodoListService**), sélectionnez **Application Web et/ou API Web**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a1601-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="a1601-136">Pour l’URL d’authentification, entrez l’URL de base pour l’exemple</span><span class="sxs-lookup"><span data-stu-id="a1601-136">For the sign-on URL, enter the base URL for the sample.</span></span> <span data-ttu-id="a1601-137">(`https://localhost:8080` par défaut).</span><span class="sxs-lookup"><span data-stu-id="a1601-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="a1601-138">Cliquez sur **OK** pour terminer l’inscription.</span><span class="sxs-lookup"><span data-stu-id="a1601-138">Click **OK** to complete the registration.</span></span>
8. <span data-ttu-id="a1601-139">Toujours dans le portail Azure, accédez à la page de votre application, recherchez la valeur de l’ID d’application et copiez-la.</span><span class="sxs-lookup"><span data-stu-id="a1601-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span></span> <span data-ttu-id="a1601-140">Vous en aurez besoin plus tard lors de la configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="a1601-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="a1601-141">À partir de la page **Paramètres** -> **Propriétés**, mettez à jour l’URI ID d’application : entrez `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="a1601-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="a1601-142">Remplacez `<your_tenant_name>` par le nom de votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1601-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span></span>

## <a name="step-3-register-the-sample-android-native-client-application"></a><span data-ttu-id="a1601-143">Étape 3 : Inscription de l’exemple d’application cliente native Android</span><span class="sxs-lookup"><span data-stu-id="a1601-143">Step 3: Register the sample Android Native Client application</span></span>
<span data-ttu-id="a1601-144">Vous devez inscrire votre application web dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a1601-144">You must register your web application in this sample.</span></span> <span data-ttu-id="a1601-145">Cela permet à votre application de communiquer avec l’API web qui vient d’être inscrite.</span><span class="sxs-lookup"><span data-stu-id="a1601-145">This allows your application to communicate with the just-registered web API.</span></span> <span data-ttu-id="a1601-146">Azure AD n’autorisera même pas votre application à demander une connexion si elle n’est pas inscrite.</span><span class="sxs-lookup"><span data-stu-id="a1601-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span></span> <span data-ttu-id="a1601-147">Cela fait partie de la sécurité du modèle.</span><span class="sxs-lookup"><span data-stu-id="a1601-147">That's part of the security of the model.</span></span>

<span data-ttu-id="a1601-148">Nous partons du principe que vous inscrivez l’exemple d’application mentionné précédemment.</span><span class="sxs-lookup"><span data-stu-id="a1601-148">We're assuming that you're registering the sample application referenced earlier.</span></span> <span data-ttu-id="a1601-149">Cependant, cette procédure fonctionne pour n’importe quelle application que vous développez.</span><span class="sxs-lookup"><span data-stu-id="a1601-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="a1601-150">Vous vous demandez peut-être pourquoi nous incorporons à la fois une application et une API web dans un seul client.</span><span class="sxs-lookup"><span data-stu-id="a1601-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="a1601-151">Comme vous l’avez peut-être deviné, vous pouvez générer une application qui accède à une API externe inscrite dans Azure AD à partir d’un autre client.</span><span class="sxs-lookup"><span data-stu-id="a1601-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="a1601-152">Si vous procédez ainsi, vos clients sont invités à donner leur autorisation pour l’utilisation de l’API dans l’application.</span><span class="sxs-lookup"><span data-stu-id="a1601-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span></span> <span data-ttu-id="a1601-153">La bibliothèque d’authentification Active Directory pour iOS s’occupe de cette autorisation pour vous.</span><span class="sxs-lookup"><span data-stu-id="a1601-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="a1601-154">À mesure que nous explorerons des fonctionnalités plus avancées, vous verrez qu’il s’agit d’une partie importante du travail nécessaire pour accéder à la suite d’API Microsoft Azure et Office, ainsi qu’à tout autre fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="a1601-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="a1601-155">Pour l’instant, comme vous avez inscrit votre API web et l’application sous le même client, vous ne voyez aucune invite de consentement.</span><span class="sxs-lookup"><span data-stu-id="a1601-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="a1601-156">Cela est généralement le cas si vous développez une application destinée uniquement à votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="a1601-156">This is usually the case if you're developing an application just for your own company to use.</span></span>

1. <span data-ttu-id="a1601-157">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a1601-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a1601-158">Dans la barre supérieure, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="a1601-158">On the top bar, click your account.</span></span> <span data-ttu-id="a1601-159">Dans la liste **Répertoire**, choisissez le locataire Azure AD auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="a1601-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="a1601-160">Dans le volet gauche, cliquez sur **Plus de services**, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1601-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="a1601-161">Cliquez sur **Inscriptions d’applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a1601-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="a1601-162">Entrez un nom convivial pour l’application (par exemple **TodoListClient-Android**), sélectionnez **Application cliente native**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a1601-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="a1601-163">Pour l’URI de redirection, entrez `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="a1601-163">For the redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="a1601-164">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="a1601-164">Click **Finish**.</span></span>
7. <span data-ttu-id="a1601-165">Dans la page de l’application, recherchez la valeur de l’ID d’application et copiez-la.</span><span class="sxs-lookup"><span data-stu-id="a1601-165">From the application page, find the application ID value and copy it.</span></span> <span data-ttu-id="a1601-166">Vous en aurez besoin plus tard lors de la configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="a1601-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="a1601-167">Dans la page **Paramètres**, sélectionnez **Autorisations requises**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a1601-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="a1601-168">Recherchez et sélectionnez TodoListService, ajoutez l’autorisation d’**accès à TodoListService** sous **Autorisations déléguées**, puis cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="a1601-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="a1601-169">Pour générer l’application avec Maven, vous pouvez utiliser pom.xml au niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="a1601-169">To build with Maven, you can use pom.xml at the top level:</span></span>

1. <span data-ttu-id="a1601-170">Clonez ce référentiel dans le répertoire de votre choix :</span><span class="sxs-lookup"><span data-stu-id="a1601-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="a1601-171">Suivez les étapes de la [section sur la configuration requise pour configurer votre environnement Maven pour Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="a1601-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="a1601-172">Installez l’émulateur avec le Kit de développement logiciel (SDK) 19.</span><span class="sxs-lookup"><span data-stu-id="a1601-172">Set up the emulator with SDK 19.</span></span>
4. <span data-ttu-id="a1601-173">Accédez au dossier racine où vous avez cloné le référentiel.</span><span class="sxs-lookup"><span data-stu-id="a1601-173">Go to the root folder where you cloned the repo.</span></span>
5. <span data-ttu-id="a1601-174">Exécutez cette commande : `mvn clean install`.</span><span class="sxs-lookup"><span data-stu-id="a1601-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="a1601-175">Remplacez le répertoire par celui de l’exemple de démarrage rapide : `cd samples\hello`.</span><span class="sxs-lookup"><span data-stu-id="a1601-175">Change the directory to the Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="a1601-176">Exécutez cette commande : `mvn android:deploy android:run`.</span><span class="sxs-lookup"><span data-stu-id="a1601-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="a1601-177">L’application doit normalement démarrer.</span><span class="sxs-lookup"><span data-stu-id="a1601-177">You should see the app starting.</span></span>
8. <span data-ttu-id="a1601-178">Entrez des informations d’identification utilisateur de test pour faire un essai.</span><span class="sxs-lookup"><span data-stu-id="a1601-178">Enter test user credentials to try.</span></span>

<span data-ttu-id="a1601-179">Des packages JAR sont envoyés en plus du package AAR.</span><span class="sxs-lookup"><span data-stu-id="a1601-179">JAR packages will be submitted beside the AAR package.</span></span>

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a><span data-ttu-id="a1601-180">Étape 4 : Téléchargement de la bibliothèque ADAL Android et ajout de cette dernière à votre espace de travail Eclipse</span><span class="sxs-lookup"><span data-stu-id="a1601-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span></span>
<span data-ttu-id="a1601-181">Nous avons fait en sorte que vous puissiez facilement disposer de plusieurs options pour utiliser la bibliothèque ADAL dans votre projet Android :</span><span class="sxs-lookup"><span data-stu-id="a1601-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span></span>

* <span data-ttu-id="a1601-182">Vous pouvez utiliser le code source pour importer cette bibliothèque dans Eclipse et la lier à votre application.</span><span class="sxs-lookup"><span data-stu-id="a1601-182">You can use the source code to import this library into Eclipse and link to your application.</span></span>
* <span data-ttu-id="a1601-183">Si vous utilisez Android Studio, vous pouvez utiliser le format de package AAR et référencer les fichiers binaires.</span><span class="sxs-lookup"><span data-stu-id="a1601-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="a1601-184">Option 1 : code source dans un fichier ZIP</span><span class="sxs-lookup"><span data-stu-id="a1601-184">Option 1: Source Zip</span></span>
<span data-ttu-id="a1601-185">Pour télécharger une copie du code source, cliquez sur **Télécharger ZIP** sur le côté droit de la page.</span><span class="sxs-lookup"><span data-stu-id="a1601-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span></span> <span data-ttu-id="a1601-186">Vous pouvez également [effectuer le téléchargement à partir de GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="a1601-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="a1601-187">Option 2:  code Source via Git</span><span class="sxs-lookup"><span data-stu-id="a1601-187">Option 2: Source via Git</span></span>
<span data-ttu-id="a1601-188">Pour obtenir le code source du Kit SDK via Git, tapez :</span><span class="sxs-lookup"><span data-stu-id="a1601-188">To get the source code of the SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="a1601-189">Option 3: fichiers binaires via Gradle</span><span class="sxs-lookup"><span data-stu-id="a1601-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="a1601-190">Vous pouvez obtenir les fichiers binaires à partir du référentiel central Maven.</span><span class="sxs-lookup"><span data-stu-id="a1601-190">You can get the binaries from the Maven central repo.</span></span> <span data-ttu-id="a1601-191">Le package AAR peut être inclus dans votre projet dans Android Studio comme suit :</span><span class="sxs-lookup"><span data-stu-id="a1601-191">The AAR package can be included as follows in your project in Android Studio:</span></span>

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

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="a1601-192">Option 4: AAR via Maven</span><span class="sxs-lookup"><span data-stu-id="a1601-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="a1601-193">Si vous utilisez le plug-in M2Eclipse, vous pouvez spécifier la dépendance dans votre fichier pom.xml :</span><span class="sxs-lookup"><span data-stu-id="a1601-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a><span data-ttu-id="a1601-194">Option 5 : package JAR à l’intérieur du dossier de bibliothèques</span><span class="sxs-lookup"><span data-stu-id="a1601-194">Option 5: JAR package inside the libs folder</span></span>
<span data-ttu-id="a1601-195">Vous pouvez obtenir le fichier JAR à partir du référentiel Maven et le déposer dans le dossier **libs** de votre projet.</span><span class="sxs-lookup"><span data-stu-id="a1601-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span></span> <span data-ttu-id="a1601-196">Vous devez également copier les ressources nécessaires à votre projet, car les packages JAR ne les incluent pas.</span><span class="sxs-lookup"><span data-stu-id="a1601-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span></span>

## <a name="step-5-add-references-to-android-adal-to-your-project"></a><span data-ttu-id="a1601-197">Étape 5 : ajout des références à la bibliothèque ADAL Android dans votre projet</span><span class="sxs-lookup"><span data-stu-id="a1601-197">Step 5: Add references to Android ADAL to your project</span></span>
1. <span data-ttu-id="a1601-198">Ajoutez une référence à votre projet et spécifiez qu’il s’agit d’une bibliothèque Android.</span><span class="sxs-lookup"><span data-stu-id="a1601-198">Add a reference to your project and specify it as an Android library.</span></span> <span data-ttu-id="a1601-199">Si vous n’êtes pas sûr de la procédure à suivre, vous trouverez plus d’informations sur le [site Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="a1601-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="a1601-200">Ajoutez la dépendance de projet pour le débogage dans vos paramètres de projet.</span><span class="sxs-lookup"><span data-stu-id="a1601-200">Add the project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="a1601-201">Mettez à jour le fichier AndroidManifest.xml du projet pour y inclure le code suivant :</span><span class="sxs-lookup"><span data-stu-id="a1601-201">Update your project's AndroidManifest.xml file to include:</span></span>

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

4. <span data-ttu-id="a1601-202">Créez une instance d’AuthenticationContext pour votre activité principale.</span><span class="sxs-lookup"><span data-stu-id="a1601-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="a1601-203">Les détails de cet appel dépassent la cadre de cette rubrique, mais pour commencer, vous pouvez examiner l’[exemple de client natif Android](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="a1601-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="a1601-204">Dans l’exemple suivant, SharedPreferences est le cache par défaut et l’autorité prend la forme `https://login.microsoftonline.com/yourtenant.onmicrosoft.com` :</span><span class="sxs-lookup"><span data-stu-id="a1601-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="a1601-205">Copiez ce bloc de code pour gérer la fin d’AuthenticationActivity une fois que l’utilisateur a entré les informations d’identification et reçu le code d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="a1601-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="a1601-206">Pour demander un jeton, définissez un rappel :</span><span class="sxs-lookup"><span data-stu-id="a1601-206">To ask for a token, define a callback:</span></span>

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

7. <span data-ttu-id="a1601-207">Enfin, demandez un jeton à l’aide de ce rappel :</span><span class="sxs-lookup"><span data-stu-id="a1601-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="a1601-208">Voici une explication des paramètres :</span><span class="sxs-lookup"><span data-stu-id="a1601-208">Here's an explanation of the parameters:</span></span>

* <span data-ttu-id="a1601-209">*resource* est obligatoire et désigne la ressource à laquelle vous tentez d’accéder.</span><span class="sxs-lookup"><span data-stu-id="a1601-209">*resource* is required and is the resource you're trying to access.</span></span>
* <span data-ttu-id="a1601-210">*clientid* est obligatoire et provient d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1601-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="a1601-211">*RedirectUri* n’est pas obligatoire pour l’appel à acquireToken.</span><span class="sxs-lookup"><span data-stu-id="a1601-211">*RedirectUri* is not required to be provided for the acquireToken call.</span></span> <span data-ttu-id="a1601-212">Vous pouvez définir ce paramètre sur le nom de votre package.</span><span class="sxs-lookup"><span data-stu-id="a1601-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="a1601-213">*PromptBehavior* permet de demander des informations d’identification pour ignorer le cache et le cookie.</span><span class="sxs-lookup"><span data-stu-id="a1601-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span></span>
* <span data-ttu-id="a1601-214">*callback* est appelé une fois que le code d’autorisation a été échangé contre un jeton.</span><span class="sxs-lookup"><span data-stu-id="a1601-214">*callback* is called after the authorization code is exchanged for a token.</span></span> <span data-ttu-id="a1601-215">Ce paramètre présente un objet AuthenticationResult avec jeton d’accès, date d’expiration et informations de jeton d’ID.</span><span class="sxs-lookup"><span data-stu-id="a1601-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="a1601-216">*acquireTokenSilent* est facultatif.</span><span class="sxs-lookup"><span data-stu-id="a1601-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="a1601-217">Vous pouvez appeler ce paramètre pour gérer la mise en cache et l’actualisation du jeton.</span><span class="sxs-lookup"><span data-stu-id="a1601-217">You can call it to handle caching and token refresh.</span></span> <span data-ttu-id="a1601-218">Il fournit également la version de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="a1601-218">It also provides the sync version.</span></span> <span data-ttu-id="a1601-219">Il accepte *userId* comme paramètre.</span><span class="sxs-lookup"><span data-stu-id="a1601-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="a1601-220">Cette procédure pas à pas devrait vous permettre d’effectuer correctement l’intégration avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a1601-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="a1601-221">Pour d’autres exemples, consultez le référentiel AzureADSamples/ sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a1601-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="a1601-222">Informations importantes</span><span class="sxs-lookup"><span data-stu-id="a1601-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="a1601-223">Personnalisation</span><span class="sxs-lookup"><span data-stu-id="a1601-223">Customization</span></span>
<span data-ttu-id="a1601-224">Les ressources de votre application peuvent remplacer celles du projet de bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="a1601-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="a1601-225">Cela se produit lors de la création de votre application.</span><span class="sxs-lookup"><span data-stu-id="a1601-225">This happens when your app is being built.</span></span> <span data-ttu-id="a1601-226">C’est pourquoi vous pouvez personnaliser la mise en page de l’activité d’authentification comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="a1601-226">For this reason, you can customize authentication activity layout the way you want.</span></span> <span data-ttu-id="a1601-227">Veillez à conserver l’ID des contrôles utilisés par ADAL (WebView).</span><span class="sxs-lookup"><span data-stu-id="a1601-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="a1601-228">Broker</span><span class="sxs-lookup"><span data-stu-id="a1601-228">Broker</span></span>
<span data-ttu-id="a1601-229">L’application Portail d’entreprise Microsoft Intune fournit le composant de service Broker.</span><span class="sxs-lookup"><span data-stu-id="a1601-229">The Microsoft Intune Company Portal app provides the broker component.</span></span> <span data-ttu-id="a1601-230">Le compte est créé dans AccountManager.</span><span class="sxs-lookup"><span data-stu-id="a1601-230">The account is created in AccountManager.</span></span> <span data-ttu-id="a1601-231">Le type de compte est « com.microsoft.workaccount ».</span><span class="sxs-lookup"><span data-stu-id="a1601-231">The account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="a1601-232">AccountManager autorise un seul compte d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a1601-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="a1601-233">Il crée un cookie d’authentification unique pour cet utilisateur après avoir terminé la demande d’appareil pour l’une des applications.</span><span class="sxs-lookup"><span data-stu-id="a1601-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span></span>

<span data-ttu-id="a1601-234">La bibliothèque ADAL utilise le compte de service Broker si un compte d’utilisateur a été créé pour cet authentificateur et que vous choisissez de ne pas l’ignorer.</span><span class="sxs-lookup"><span data-stu-id="a1601-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span></span> <span data-ttu-id="a1601-235">Vous pouvez ignorer l’utilisateur du service Broker avec :</span><span class="sxs-lookup"><span data-stu-id="a1601-235">You can skip the broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="a1601-236">Vous devez inscrire un redirectUri spécial pour l’utilisation du service Broker.</span><span class="sxs-lookup"><span data-stu-id="a1601-236">You need to register a special RedirectUri for broker usage.</span></span> <span data-ttu-id="a1601-237">RedirectUri est au format `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="a1601-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="a1601-238">Vous pouvez obtenir votre RedirectUri pour votre application en utilisant le script brokerRedirectPrint.ps1 ou l’appel d’API mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="a1601-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="a1601-239">La signature est liée à vos certificats de signature.</span><span class="sxs-lookup"><span data-stu-id="a1601-239">The signature is related to your signing certificates.</span></span>

<span data-ttu-id="a1601-240">Le modèle actuel de service Broker est limité à un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a1601-240">The current broker model is for one user.</span></span> <span data-ttu-id="a1601-241">AuthenticationContext fournit une méthode API pour obtenir l’utilisateur du service Broker.</span><span class="sxs-lookup"><span data-stu-id="a1601-241">AuthenticationContext provides the API method to get the broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="a1601-242">Le manifeste de votre application doit présenter les autorisations suivantes pour utiliser des comptes AccountManager.</span><span class="sxs-lookup"><span data-stu-id="a1601-242">Your app manifest should have the following permissions to use AccountManager accounts.</span></span> <span data-ttu-id="a1601-243">Pour plus d’informations, consultez les [informations concernant AccountManager sur le site Android](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="a1601-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="a1601-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="a1601-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="a1601-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="a1601-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="a1601-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="a1601-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="a1601-247">AD FS et URL de l’autorité</span><span class="sxs-lookup"><span data-stu-id="a1601-247">Authority URL and AD FS</span></span>
<span data-ttu-id="a1601-248">Les services de fédération Active Directory ne sont pas reconnus comme des services d’émission de jeton de sécurité (STS) de production ; vous devez donc activer la découverte de l’instance et transmettre la valeur false au constructeur AuthenticationContext.</span><span class="sxs-lookup"><span data-stu-id="a1601-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span></span>

<span data-ttu-id="a1601-249">L’URL de l’autorité a besoin d’une instance STS et d’un [nom de client](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="a1601-249">The authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="a1601-250">Interrogation des éléments de cache</span><span class="sxs-lookup"><span data-stu-id="a1601-250">Querying cache items</span></span>
<span data-ttu-id="a1601-251">ADAL fournit un cache par défaut dans SharedPreferences avec quelques fonctions simples de requête de cache.</span><span class="sxs-lookup"><span data-stu-id="a1601-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="a1601-252">Vous pouvez récupérer le cache actuel d’AuthenticationContext avec :</span><span class="sxs-lookup"><span data-stu-id="a1601-252">You can get the current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="a1601-253">Vous pouvez également fournir votre implémentation de cache, si vous souhaitez le personnaliser.</span><span class="sxs-lookup"><span data-stu-id="a1601-253">You can also provide your cache implementation, if you want to customize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="a1601-254">Comportement d’invite</span><span class="sxs-lookup"><span data-stu-id="a1601-254">Prompt behavior</span></span>
<span data-ttu-id="a1601-255">ADAL fournit une option permettant de spécifier le comportement d’invite.</span><span class="sxs-lookup"><span data-stu-id="a1601-255">ADAL provides an option to specify prompt behavior.</span></span> <span data-ttu-id="a1601-256">PromptBehavior.Auto affiche l’interface utilisateur si le jeton d’actualisation n’est pas valide et les informations d’identification utilisateur sont requises.</span><span class="sxs-lookup"><span data-stu-id="a1601-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="a1601-257">PromptBehavior.Always ignore l’utilisation du cache et affiche toujours l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a1601-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="a1601-258">Demande de jeton en mode silencieux à partir du cache et actualisation</span><span class="sxs-lookup"><span data-stu-id="a1601-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="a1601-259">Une demande de jeton en mode silencieux n’utilise pas l’affichage de l’interface utilisateur et ne nécessite pas d’activité.</span><span class="sxs-lookup"><span data-stu-id="a1601-259">A silent token request does not use the UI pop-up and does not require an activity.</span></span> <span data-ttu-id="a1601-260">Elle renvoie un jeton à partir du cache s’il est disponible.</span><span class="sxs-lookup"><span data-stu-id="a1601-260">It returns a token from the cache if available.</span></span> <span data-ttu-id="a1601-261">Si le jeton est arrivé à expiration, cette méthode tente de l’actualiser.</span><span class="sxs-lookup"><span data-stu-id="a1601-261">If the token is expired, this method tries to refresh it.</span></span> <span data-ttu-id="a1601-262">Si le jeton d’actualisation est arrivé à expiration ou a échoué, elle renvoie AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="a1601-262">If the refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="a1601-263">Vous pouvez également effectuer un appel de synchronisation à l’aide de cette méthode.</span><span class="sxs-lookup"><span data-stu-id="a1601-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="a1601-264">Vous pouvez définir la valeur null pour un rappel ou utiliser acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="a1601-264">You can set null to callback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="a1601-265">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="a1601-265">Diagnostics</span></span>
<span data-ttu-id="a1601-266">Voici les principales sources d’informations pour diagnostiquer les problèmes :</span><span class="sxs-lookup"><span data-stu-id="a1601-266">These are the primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="a1601-267">Exceptions</span><span class="sxs-lookup"><span data-stu-id="a1601-267">Exceptions</span></span>
* <span data-ttu-id="a1601-268">Journaux</span><span class="sxs-lookup"><span data-stu-id="a1601-268">Logs</span></span>
* <span data-ttu-id="a1601-269">Suivis réseau</span><span class="sxs-lookup"><span data-stu-id="a1601-269">Network traces</span></span>

<span data-ttu-id="a1601-270">Notez que les ID de corrélation sont un élément central des diagnostics dans la bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="a1601-270">Note that correlation IDs are central to the diagnostics in the library.</span></span> <span data-ttu-id="a1601-271">Vous pouvez définir vos ID de corrélation en fonction de chaque demande si vous souhaitez mettre en corrélation une demande de la bibliothèque d’authentification Azure AD (ADAL) avec d’autres opérations dans votre code.</span><span class="sxs-lookup"><span data-stu-id="a1601-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="a1601-272">Si vous ne définissez aucun ID de corrélation, la bibliothèque ADAL génère un ID aléatoire.</span><span class="sxs-lookup"><span data-stu-id="a1601-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="a1601-273">Tous les messages de journal et les appels réseau sont alors marqués avec l’ID de corrélation.</span><span class="sxs-lookup"><span data-stu-id="a1601-273">All log messages and network calls will then be stamped with the correlation ID.</span></span> <span data-ttu-id="a1601-274">L’ID généré automatiquement change à chaque demande.</span><span class="sxs-lookup"><span data-stu-id="a1601-274">The self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="a1601-275">Exceptions</span><span class="sxs-lookup"><span data-stu-id="a1601-275">Exceptions</span></span>
<span data-ttu-id="a1601-276">Les exceptions sont le premier diagnostic.</span><span class="sxs-lookup"><span data-stu-id="a1601-276">Exceptions are the first diagnostic.</span></span> <span data-ttu-id="a1601-277">Nous essayons de fournir des messages d’erreur utiles.</span><span class="sxs-lookup"><span data-stu-id="a1601-277">We try to provide helpful error messages.</span></span> <span data-ttu-id="a1601-278">Si vous en trouvez un qui n’est pas utile, faites-le-nous savoir en signalant un problème.</span><span class="sxs-lookup"><span data-stu-id="a1601-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="a1601-279">Incluez des informations sur l’appareil, notamment le modèle et le numéro du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="a1601-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="a1601-280">Journaux</span><span class="sxs-lookup"><span data-stu-id="a1601-280">Logs</span></span>
<span data-ttu-id="a1601-281">Vous pouvez configurer la bibliothèque pour générer des messages de journal que vous pouvez utiliser pour diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="a1601-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span></span> <span data-ttu-id="a1601-282">Pour configurer la journalisation, effectuez l’appel suivant afin de configurer un rappel qui sera utilisé par ADAL pour transmettre chaque message de journal lorsqu’il sera généré.</span><span class="sxs-lookup"><span data-stu-id="a1601-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="a1601-283">Les messages peuvent être écrits dans un fichier journal personnalisé, comme illustré dans le code suivant.</span><span class="sxs-lookup"><span data-stu-id="a1601-283">Messages can be written to a custom log file, as shown in the following code.</span></span> <span data-ttu-id="a1601-284">Malheureusement, il n’existe aucun moyen standard d’obtenir les journaux d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="a1601-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="a1601-285">Il existe des services qui peuvent vous y aider.</span><span class="sxs-lookup"><span data-stu-id="a1601-285">There are some services that can help you with this.</span></span> <span data-ttu-id="a1601-286">Vous pouvez également inventer votre propre méthode, telle que l’envoi du fichier à un serveur.</span><span class="sxs-lookup"><span data-stu-id="a1601-286">You can also invent your own, such as sending the file to a server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="a1601-287">Voici les différents niveaux de journalisation :</span><span class="sxs-lookup"><span data-stu-id="a1601-287">These are the logging levels:</span></span>
* <span data-ttu-id="a1601-288">Error (exceptions)</span><span class="sxs-lookup"><span data-stu-id="a1601-288">Error (exceptions)</span></span>
* <span data-ttu-id="a1601-289">Warn (avertissement)</span><span class="sxs-lookup"><span data-stu-id="a1601-289">Warn (warning)</span></span>
* <span data-ttu-id="a1601-290">Info (informations)</span><span class="sxs-lookup"><span data-stu-id="a1601-290">Info (information purposes)</span></span>
* <span data-ttu-id="a1601-291">Verbose (détails supplémentaires)</span><span class="sxs-lookup"><span data-stu-id="a1601-291">Verbose (more details)</span></span>

<span data-ttu-id="a1601-292">Vous définissez le niveau de journal comme suit :</span><span class="sxs-lookup"><span data-stu-id="a1601-292">You set the log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="a1601-293">Tous les messages de journal sont envoyés à logcat en plus des éventuels rappels de journal personnalisé.</span><span class="sxs-lookup"><span data-stu-id="a1601-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span></span>
<span data-ttu-id="a1601-294">Vous pouvez envoyer un journal dans un fichier à partir de logcat comme suit :</span><span class="sxs-lookup"><span data-stu-id="a1601-294">You can get a log to a file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="a1601-295">Pour plus d’informations sur les commandes adb, consultez les [informations concernant logcat sur le site Android](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="a1601-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="a1601-296">Suivis réseau</span><span class="sxs-lookup"><span data-stu-id="a1601-296">Network traces</span></span>
<span data-ttu-id="a1601-297">Vous pouvez utiliser différents outils pour capturer le trafic HTTP généré par la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="a1601-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="a1601-298">Cela est particulièrement utile si vous êtes familiarisé avec le protocole OAuth ou si vous avez besoin de fournir des informations de diagnostic à Microsoft ou à d’autres canaux de support.</span><span class="sxs-lookup"><span data-stu-id="a1601-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span></span>

<span data-ttu-id="a1601-299">Fiddler est l'outil de suivi HTTP le plus simple.</span><span class="sxs-lookup"><span data-stu-id="a1601-299">Fiddler is the easiest HTTP tracing tool.</span></span> <span data-ttu-id="a1601-300">Utilisez les liens suivants pour le configurer de manière à enregistrer correctement le trafic réseau ADAL.</span><span class="sxs-lookup"><span data-stu-id="a1601-300">Use the following links to set it up to correctly record ADAL network traffic.</span></span> <span data-ttu-id="a1601-301">Pour qu’un outil de suivi comme Fiddler ou Charles soit utile, vous devez le configurer de manière à enregistrer le trafic SSL non chiffré.</span><span class="sxs-lookup"><span data-stu-id="a1601-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="a1601-302">Les suivis générés de cette manière peuvent contenir des informations hautement privilégiées (jetons d’accès, noms d’utilisateur, mots de passe, etc.).</span><span class="sxs-lookup"><span data-stu-id="a1601-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="a1601-303">Si vous utilisez des comptes de production, ne partagez pas ces suivis avec des tiers.</span><span class="sxs-lookup"><span data-stu-id="a1601-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="a1601-304">Si vous avez besoin de fournir un suivi à quelqu’un pour obtenir un support technique, reproduisez le problème à l’aide d’un compte temporaire, avec des noms d’utilisateur et des mots de passe que vous êtes prêt à partager.</span><span class="sxs-lookup"><span data-stu-id="a1601-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="a1601-305">À partir du site web de Telerik : [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid) (Configuration de Fiddler pour Android)</span><span class="sxs-lookup"><span data-stu-id="a1601-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="a1601-306">À partir de GitHub : [Configuration des règles de Fiddler pour la bibliothèque ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="a1601-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="a1601-307">Mode de la boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="a1601-307">Dialog mode</span></span>
<span data-ttu-id="a1601-308">La méthode acquireToken sans activité prend en charge une invite de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a1601-308">The acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="a1601-309">Chiffrement</span><span class="sxs-lookup"><span data-stu-id="a1601-309">Encryption</span></span>
<span data-ttu-id="a1601-310">ADAL chiffre les jetons et les stocke dans SharedPreferences par défaut.</span><span class="sxs-lookup"><span data-stu-id="a1601-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="a1601-311">Vous pouvez consulter la classe StorageHelper pour afficher les détails.</span><span class="sxs-lookup"><span data-stu-id="a1601-311">You can look at the StorageHelper class to see the details.</span></span> <span data-ttu-id="a1601-312">Android a introduit Android Keydtore pour le stockage sécurisé des clés privées de la version 4.3 (API 18).</span><span class="sxs-lookup"><span data-stu-id="a1601-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="a1601-313">La bibliothèque ADAL utilise ces informations pour l’API 18 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="a1601-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="a1601-314">Si vous souhaitez utiliser la bibliothèque ADAL pour les versions antérieures du Kit de développement logiciel (SDK), vous devez fournir une clé secrète à AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="a1601-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="a1601-315">Demande de support OAuth2</span><span class="sxs-lookup"><span data-stu-id="a1601-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="a1601-316">La classe AuthenticationParameters fournit les fonctionnalités requises pour obtenir authorization_uri à partir de la demande de support OAuth2.</span><span class="sxs-lookup"><span data-stu-id="a1601-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="a1601-317">Cookies de session dans WebView</span><span class="sxs-lookup"><span data-stu-id="a1601-317">Session cookies in WebView</span></span>
<span data-ttu-id="a1601-318">Android WebView n’efface pas les cookies de session après la fermeture de l’application.</span><span class="sxs-lookup"><span data-stu-id="a1601-318">Android WebView does not clear session cookies after the app is closed.</span></span> <span data-ttu-id="a1601-319">Vous pouvez gérer cela à l’aide de l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="a1601-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="a1601-320">Pour plus d’informations sur les cookies, consultez les [informations concernant CookieSyncManager sur le site Android](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="a1601-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="a1601-321">Remplacements de ressources</span><span class="sxs-lookup"><span data-stu-id="a1601-321">Resource overrides</span></span>
<span data-ttu-id="a1601-322">La bibliothèque ADAL inclut les chaînes en anglais pour les messages ProgressDialog.</span><span class="sxs-lookup"><span data-stu-id="a1601-322">The ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="a1601-323">Votre application doit les remplacer si vous voulez des chaînes localisées.</span><span class="sxs-lookup"><span data-stu-id="a1601-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="a1601-324">Boîte de dialogue NTLM</span><span class="sxs-lookup"><span data-stu-id="a1601-324">NTLM dialog box</span></span>
<span data-ttu-id="a1601-325">ADAL version 1.1.0 prend en charge une boîte de dialogue NTLM qui est traitée via l’événement onReceivedHttpAuthRequest de WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="a1601-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="a1601-326">Vous pouvez personnaliser la disposition et les chaînes de cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a1601-326">You can customize the layout and strings for the dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="a1601-327">Authentification unique entre applications</span><span class="sxs-lookup"><span data-stu-id="a1601-327">Cross-app SSO</span></span>
<span data-ttu-id="a1601-328">Découvrez [comment activer l’authentification unique entre applications sur Android à l’aide de la bibliothèque ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="a1601-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
