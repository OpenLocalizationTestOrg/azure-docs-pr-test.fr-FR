---
title: authentification aaaAdd sur Apache Cordova avec les applications mobiles | Documents Microsoft
description: "Découvrez comment toouse applications mobiles dans les utilisateurs de tooauthenticate Azure App Service de votre application Apache Cordova via une variété de fournisseurs d’identité, y compris de Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a><span data-ttu-id="6126c-103">Ajouter une application de l’authentification tooyour Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="6126c-103">Add authentication tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="6126c-104">Résumé</span><span class="sxs-lookup"><span data-stu-id="6126c-104">Summary</span></span>
<span data-ttu-id="6126c-105">Dans ce didacticiel, vous ajoutez le projet de démarrage rapide de l’authentification toohello todolist sur Apache Cordova à l’aide d’un fournisseur d’identité pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6126c-105">In this tutorial, you add authentication toohello todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="6126c-106">Ce didacticiel est basé sur hello [prise en main les applications mobiles] didacticiel, vous devez effectuer en premier.</span><span class="sxs-lookup"><span data-stu-id="6126c-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="6126c-107"><a name="register"></a>Inscrire votre application pour l’authentification et de configurer hello du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="6126c-107"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="6126c-108">Regarder une vidéo montrant des étapes similaires</span><span class="sxs-lookup"><span data-stu-id="6126c-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="6126c-109"><a name="permissions"></a>Restreindre les autorisations des utilisateurs tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="6126c-109"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="6126c-110">Maintenant, vous pouvez vérifier que ce principal de tooyour l’accès anonyme a été désactivé.</span><span class="sxs-lookup"><span data-stu-id="6126c-110">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="6126c-111">Dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="6126c-111">In Visual Studio:</span></span>

* <span data-ttu-id="6126c-112">Projet ouvert hello que vous avez créé lorsque vous avez rempli le didacticiel de hello [prise en main les applications mobiles].</span><span class="sxs-lookup"><span data-stu-id="6126c-112">Open hello project that you created when you completed hello tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="6126c-113">Exécutez votre application dans hello **émulateur Android de Google**.</span><span class="sxs-lookup"><span data-stu-id="6126c-113">Run your application in hello **Google Android Emulator**.</span></span>
* <span data-ttu-id="6126c-114">Vérifiez qu’une défaillance inattendue de la connexion n’est affichée après le démarrage de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6126c-114">Verify that an Unexpected Connection Failure is shown after hello app starts.</span></span>

<span data-ttu-id="6126c-115">Ensuite, mettez à jour les utilisateurs de hello application tooauthenticate avant de demander des ressources à partir du serveur principal de l’application Mobile hello.</span><span class="sxs-lookup"><span data-stu-id="6126c-115">Next, update hello app tooauthenticate users before requesting resources from hello Mobile App backend.</span></span>

## <span data-ttu-id="6126c-116"><a name="add-authentication"></a>Ajouter une application de toohello d’authentification</span><span class="sxs-lookup"><span data-stu-id="6126c-116"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="6126c-117">Ouvrez votre projet dans **Visual Studio**, puis ouvrez hello `www/index.html` fichier pour le modifier.</span><span class="sxs-lookup"><span data-stu-id="6126c-117">Open your project in **Visual Studio**, then open hello `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="6126c-118">Recherchez hello `Content-Security-Policy` balise meta de section d’en-tête hello.</span><span class="sxs-lookup"><span data-stu-id="6126c-118">Locate hello `Content-Security-Policy` meta tag in hello head section.</span></span>  <span data-ttu-id="6126c-119">Ajoutez hello OAuth hôte toohello liste de sources autorisées.</span><span class="sxs-lookup"><span data-stu-id="6126c-119">Add hello OAuth host toohello list of allowed sources.</span></span>

   | <span data-ttu-id="6126c-120">Fournisseur</span><span class="sxs-lookup"><span data-stu-id="6126c-120">Provider</span></span> | <span data-ttu-id="6126c-121">Nom du fournisseur du Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="6126c-121">SDK Provider Name</span></span> | <span data-ttu-id="6126c-122">Hôte OAuth</span><span class="sxs-lookup"><span data-stu-id="6126c-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="6126c-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6126c-123">Azure Active Directory</span></span> | <span data-ttu-id="6126c-124">aad</span><span class="sxs-lookup"><span data-stu-id="6126c-124">aad</span></span> | <span data-ttu-id="6126c-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6126c-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="6126c-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="6126c-126">Facebook</span></span> | <span data-ttu-id="6126c-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="6126c-127">facebook</span></span> | <span data-ttu-id="6126c-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="6126c-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="6126c-129">Google</span><span class="sxs-lookup"><span data-stu-id="6126c-129">Google</span></span> | <span data-ttu-id="6126c-130">Google</span><span class="sxs-lookup"><span data-stu-id="6126c-130">google</span></span> | <span data-ttu-id="6126c-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="6126c-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="6126c-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="6126c-132">Microsoft</span></span> | <span data-ttu-id="6126c-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="6126c-133">microsoftaccount</span></span> | <span data-ttu-id="6126c-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="6126c-134">https://login.live.com</span></span> |
   | <span data-ttu-id="6126c-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="6126c-135">Twitter</span></span> | <span data-ttu-id="6126c-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="6126c-136">twitter</span></span> | <span data-ttu-id="6126c-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="6126c-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="6126c-138">Voici un exemple Content-Security-Policy (implémenté pour Azure Active Directory) :</span><span class="sxs-lookup"><span data-stu-id="6126c-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="6126c-139">Remplacez `https://login.microsoftonline.com` avec hôte OAuth hello hello tableau précédent.</span><span class="sxs-lookup"><span data-stu-id="6126c-139">Replace `https://login.microsoftonline.com` with hello OAuth host from hello preceding table.</span></span>  <span data-ttu-id="6126c-140">Pour plus d’informations sur la balise meta de stratégie de sécurité de contenu hello, consultez hello [documentation de la stratégie de sécurité de contenu].</span><span class="sxs-lookup"><span data-stu-id="6126c-140">For more information about hello content-security-policy meta tag, see hello [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="6126c-141">Certains fournisseurs d’authentification ne requièrent aucune modification Content-Security-Policy avec des appareils mobiles appropriés.</span><span class="sxs-lookup"><span data-stu-id="6126c-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="6126c-142">Par exemple, aucune modification de l’approche Content-Security-Policy n’est nécessaire lorsque vous recourez à l’authentification Google sur un appareil Android.</span><span class="sxs-lookup"><span data-stu-id="6126c-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="6126c-143">Ouvrez hello `www/js/index.js` pour la modification du fichier, recherchez hello `onDeviceReady()` (méthode), et en cours de création de client hello code ajouter hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="6126c-143">Open hello `www/js/index.js` file for editing, locate hello `onDeviceReady()` method, and under hello client  creation code add hello following code:</span></span>

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="6126c-144">Ce code remplace le code d’existant hello qui crée la référence de table hello et actualise hello l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6126c-144">This code replaces hello existing code that creates hello table reference and refreshes hello UI.</span></span>

    <span data-ttu-id="6126c-145">méthode de login() Hello démarre l’authentification avec le fournisseur de hello.</span><span class="sxs-lookup"><span data-stu-id="6126c-145">hello login() method starts authentication with hello provider.</span></span> <span data-ttu-id="6126c-146">méthode de login() Hello est une fonction async qui retourne une promesse de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6126c-146">hello login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="6126c-147">rest Hello de l’initialisation de hello est placé dans la réponse de promesse hello afin qu’il n’est pas exécuté tant que hello login() méthode se termine.</span><span class="sxs-lookup"><span data-stu-id="6126c-147">hello rest of hello initialization is placed inside hello promise response so that it is not executed until hello login() method completes.</span></span>

4. <span data-ttu-id="6126c-148">Dans le code hello que vous venez d’ajouter, remplacer `SDK_Provider_Name` par nom de hello de votre fournisseur de connexion.</span><span class="sxs-lookup"><span data-stu-id="6126c-148">In hello code that you just added, replace `SDK_Provider_Name` with hello name of your login provider.</span></span> <span data-ttu-id="6126c-149">Par exemple, pour Azure Active Directory, utilisez `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="6126c-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="6126c-150">Exécutez votre projet.</span><span class="sxs-lookup"><span data-stu-id="6126c-150">Run your project.</span></span>  <span data-ttu-id="6126c-151">Lorsque le projet de hello a terminé l’initialisation, votre application montre la page de connexion OAuth hello pour hello choisi le fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="6126c-151">When hello project has finished initializing, your application shows hello OAuth login page for hello chosen authentication provider.</span></span>

## <span data-ttu-id="6126c-152"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6126c-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="6126c-153">En savoir plus [À propos de l’authentification] avec Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6126c-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="6126c-154">Continuer le didacticiel de hello en ajoutant [des Notifications Push] tooyour Apache Cordova application.</span><span class="sxs-lookup"><span data-stu-id="6126c-154">Continue hello tutorial by adding [Push Notifications] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="6126c-155">Découvrez comment toouse hello kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="6126c-155">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="6126c-156">[Kit de développement logiciel (SDK) Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="6126c-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="6126c-157">[Kit de développement logiciel du serveur ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="6126c-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="6126c-158">[Kit de développement logiciel du serveur Node.js]</span><span class="sxs-lookup"><span data-stu-id="6126c-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
[prise en main les applications mobiles]: app-service-mobile-cordova-get-started.md
[documentation de la stratégie de sécurité de contenu]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[des Notifications Push]: app-service-mobile-cordova-get-started-push.md
[À propos de l’authentification]: app-service-mobile-auth.md
[Kit de développement logiciel (SDK) Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[Kit de développement logiciel du serveur ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Kit de développement logiciel du serveur Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
