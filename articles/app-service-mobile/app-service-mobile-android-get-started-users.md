---
title: authentification aaaAdd sur Android avec des applications mobiles | Documents Microsoft
description: "Découvrez comment toouse hello fonctionnalité des applications mobiles des utilisateurs de tooauthenticate Azure App Service de votre application Android via une variété de fournisseurs d’identité, y compris de Google, Facebook, Twitter et Microsoft."
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
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a><span data-ttu-id="a9ddb-103">Ajouter une application Android de l’authentification tooyour</span><span class="sxs-lookup"><span data-stu-id="a9ddb-103">Add authentication tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="a9ddb-104">Résumé</span><span class="sxs-lookup"><span data-stu-id="a9ddb-104">Summary</span></span>
<span data-ttu-id="a9ddb-105">Dans ce didacticiel, vous ajoutez le projet de démarrage rapide de l’authentification toohello todolist sur Android à l’aide d’un fournisseur d’identité pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-105">In this tutorial, you add authentication toohello todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="a9ddb-106">Ce didacticiel est basé sur hello [prise en main les applications mobiles] didacticiel, vous devez effectuer en premier.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="a9ddb-107"><a name="register"></a>Inscription de votre application pour l’authentification et configuration d’Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a9ddb-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="a9ddb-108"><a name="redirecturl"></a>Ajouter votre URL de redirection externe d’autorisé toohello application</span><span class="sxs-lookup"><span data-stu-id="a9ddb-108"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="a9ddb-109">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="a9ddb-110">Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-110">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="a9ddb-111">Dans ce didacticiel, nous utilisons le modèle d’URL hello _appname_ dans l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-111">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="a9ddb-112">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="a9ddb-113">Il doit être unique tooyour des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-113">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="a9ddb-114">redirection de hello tooenable côté serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="a9ddb-114">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="a9ddb-115">Bonjour [Azure portal], sélectionnez votre application de Service.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-115">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="a9ddb-116">Cliquez sur hello **l’authentification / autorisation** option de menu.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-116">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="a9ddb-117">Bonjour **autorisé des URL de redirection externe**, entrez `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-117">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="a9ddb-118">Hello _appname_ dans cette chaîne est hello le modèle d’URL pour votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-118">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="a9ddb-119">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="a9ddb-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="a9ddb-120">Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-120">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="a9ddb-121">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-121">Click **OK**.</span></span>

5. <span data-ttu-id="a9ddb-122">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-122">Click **Save**.</span></span>

## <span data-ttu-id="a9ddb-123"><a name="permissions"></a>Restreindre les autorisations des utilisateurs tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="a9ddb-123"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="a9ddb-124">Dans Android Studio, ouvrez le projet hello avec le didacticiel de hello [prise en main les applications mobiles].</span><span class="sxs-lookup"><span data-stu-id="a9ddb-124">In Android Studio, open hello project you completed with hello tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="a9ddb-125">À partir de hello **exécuter** menu, cliquez sur **exécuter application**et vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-125">From hello **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span>

     <span data-ttu-id="a9ddb-126">Cette exception se produit, car les tentatives d’application hello tooaccess hello retour comme un utilisateur non authentifié, mais hello *TodoItem* table requiert l’authentification.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-126">This exception happens because hello app attempts tooaccess hello back end as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="a9ddb-127">Ensuite, vous mettre à jour les utilisateurs de hello application tooauthenticate avant de demander des ressources à partir de hello de fin dans les applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-127">Next, you update hello app tooauthenticate users before requesting resources from hello Mobile Apps back end.</span></span> 

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="a9ddb-128">Ajouter une application de toohello d’authentification</span><span class="sxs-lookup"><span data-stu-id="a9ddb-128">Add authentication toohello app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="a9ddb-129"><a name="cache-tokens"></a>Mettre en cache des jetons d’authentification sur le client de hello</span><span class="sxs-lookup"><span data-stu-id="a9ddb-129"><a name="cache-tokens"></a>Cache authentication tokens on hello client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="a9ddb-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9ddb-130">Next steps</span></span>
<span data-ttu-id="a9ddb-131">Maintenant que vous terminé ce didacticiel de l’authentification de base, pensez à poursuivre sur tooone Hello suivant didacticiels :</span><span class="sxs-lookup"><span data-stu-id="a9ddb-131">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="a9ddb-132">[Ajouter une application Android de push notifications tooyour](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="a9ddb-132">[Add push notifications tooyour Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="a9ddb-133">Découvrez comment tooconfigure vos applications mobiles sauvegarder terminer les notifications push toosend toouse Azure notification hubs.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-133">Learn how tooconfigure your Mobile Apps back end toouse Azure notification hubs toosend push notifications.</span></span>
* <span data-ttu-id="a9ddb-134">[Activation de la synchronisation hors connexion pour votre application Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="a9ddb-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="a9ddb-135">Découvrez comment tooadd hors connexion prennent en charge tooyour application à l’aide d’un principal des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-135">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="a9ddb-136">La synchronisation hors connexion permet aux utilisateurs d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="a9ddb-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[prise en main les applications mobiles]: app-service-mobile-android-get-started.md
