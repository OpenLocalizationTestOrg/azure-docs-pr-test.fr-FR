---
title: "Ajout de l’authentification à Android à l’aide de Mobile Apps | Microsoft Docs"
description: "Découvrez comment utiliser la fonctionnalité Mobile Apps d’Azure App Service pour authentifier les utilisateurs de votre application Android via divers fournisseurs d’identité, notamment Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 81331142aa6110d4e29e6fb30a90ce6e3a853439
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-android-app"></a><span data-ttu-id="950da-103">Ajout de l’authentification à votre application Android</span><span class="sxs-lookup"><span data-stu-id="950da-103">Add authentication to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="950da-104">Résumé</span><span class="sxs-lookup"><span data-stu-id="950da-104">Summary</span></span>
<span data-ttu-id="950da-105">Dans ce didacticiel, vous allez ajouter l’authentification au projet de démarrage rapide todolist sur Android en faisant appel à un fournisseur d’identité pris en charge.</span><span class="sxs-lookup"><span data-stu-id="950da-105">In this tutorial, you add authentication to the todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="950da-106">Ce didacticiel est basé sur le didacticiel [Prise en main de Mobile Apps] , que vous devez effectuer en premier.</span><span class="sxs-lookup"><span data-stu-id="950da-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="950da-107"><a name="register"></a>Inscription de votre application pour l’authentification et configuration d’Azure App Service</span><span class="sxs-lookup"><span data-stu-id="950da-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="950da-108"><a name="redirecturl"></a>Ajouter votre application aux URL de redirection externes autorisées</span><span class="sxs-lookup"><span data-stu-id="950da-108"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="950da-109">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="950da-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="950da-110">Cela permet au système d’authentification de vous rediriger vers votre application une fois le processus d’authentification terminé.</span><span class="sxs-lookup"><span data-stu-id="950da-110">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="950da-111">Dans ce didacticiel, nous utilisons le schéma d’URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="950da-111">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="950da-112">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="950da-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="950da-113">Il doit être propre à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="950da-113">It should be unique to your mobile application.</span></span> <span data-ttu-id="950da-114">Pour activer la redirection côté serveur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="950da-114">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="950da-115">Dans le [portail Azure], sélectionnez votre instance App Service.</span><span class="sxs-lookup"><span data-stu-id="950da-115">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="950da-116">Cliquez sur l’option de menu **Authentication/Authorisation**.</span><span class="sxs-lookup"><span data-stu-id="950da-116">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="950da-117">Dans **URL de redirection externes autorisées**, saisissez `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="950da-117">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="950da-118">La chaîne _appname_ de cette chaîne est le schéma d’URL de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="950da-118">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="950da-119">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="950da-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="950da-120">Vous devez noter la chaîne que vous choisissez, dans la mesure où vous devez ajuster votre code d’application mobile avec le schéma d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="950da-120">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="950da-121">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="950da-121">Click **OK**.</span></span>

5. <span data-ttu-id="950da-122">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="950da-122">Click **Save**.</span></span>

## <span data-ttu-id="950da-123"><a name="permissions"></a>Restriction des autorisations pour les utilisateurs authentifiés</span><span class="sxs-lookup"><span data-stu-id="950da-123"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="950da-124">Dans Android Studio, ouvrez le projet que vous avez terminé avec le didacticiel [Prise en main de Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="950da-124">In Android Studio, open the project you completed with the tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="950da-125">Dans le menu **Exécuter**, cliquez sur **Exécuter l’application** et vérifiez qu’une exception non prise en charge avec le code d’état 401 (Non autorisé) est générée après le démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="950da-125">From the **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span>

     <span data-ttu-id="950da-126">Cela se produit car l’application essaie d’accéder au serveur principal en tant qu’utilisateur non authentifié, mais la table *TodoItem* requiert désormais l’authentification.</span><span class="sxs-lookup"><span data-stu-id="950da-126">This exception happens because the app attempts to access the back end as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="950da-127">Ensuite, mettez à jour l’application pour authentifier les utilisateurs avant de demander des ressources à partir du serveur principal Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="950da-127">Next, you update the app to authenticate users before requesting resources from the Mobile Apps back end.</span></span> 

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="950da-128">Ajout de l'authentification à l'application</span><span class="sxs-lookup"><span data-stu-id="950da-128">Add authentication to the app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="950da-129"><a name="cache-tokens"></a>Mise en cache de jetons d'authentification sur le client</span><span class="sxs-lookup"><span data-stu-id="950da-129"><a name="cache-tokens"></a>Cache authentication tokens on the client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="950da-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="950da-130">Next steps</span></span>
<span data-ttu-id="950da-131">Maintenant que vous avez terminé ce didacticiel sur l'authentification de base, vous pouvez passer à l'un des didacticiels suivants :</span><span class="sxs-lookup"><span data-stu-id="950da-131">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="950da-132">[Ajout de notifications Push à votre application Android](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="950da-132">[Add push notifications to your Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="950da-133">Découvrez comment configurer votre serveur principal Mobile Apps pour utiliser Azure Notification Hubs afin d’envoyer des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="950da-133">Learn how to configure your Mobile Apps back end to use Azure notification hubs to send push notifications.</span></span>
* <span data-ttu-id="950da-134">[Activation de la synchronisation hors connexion pour votre application Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="950da-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="950da-135">Découvrez comment ajouter une prise en charge hors connexion à votre application à l’aide d’un serveur principal Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="950da-135">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="950da-136">La synchronisation hors connexion permet aux utilisateurs d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="950da-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions to authenticated users]: #permissions
[Add authentication to the app]: #add-authentication
[Store authentication tokens on the client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
<span data-ttu-id="950da-137">[Prise en main de Mobile Apps]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="950da-137">[Get started with Mobile Apps]: app-service-mobile-android-get-started.md</span></span>
