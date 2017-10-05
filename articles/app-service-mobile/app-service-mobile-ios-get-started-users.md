---
title: "Ajout de l’authentification sur iOS avec Azure Mobile Apps"
description: "Découvrez comment utiliser Azure Mobile Apps pour authentifier les utilisateurs de votre application iOS via divers fournisseurs d'identité, notamment AAD, Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: 21a2cc6c1eaf4b34cbe8c2d7c4dbb69c8730cf32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-ios-app"></a><span data-ttu-id="89e24-103">Ajout de l'authentification à votre application iOS</span><span class="sxs-lookup"><span data-stu-id="89e24-103">Add authentication to your iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="89e24-104">Dans ce didacticiel, vous allez ajouter l’authentification au projet de [Démarrage rapide iOS] en faisant appel à un fournisseur d’identité pris en charge.</span><span class="sxs-lookup"><span data-stu-id="89e24-104">In this tutorial, you add authentication to the [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="89e24-105">Ce didacticiel est basé sur le didacticiel [Démarrage rapide iOS] , que vous devez effectuer en premier.</span><span class="sxs-lookup"><span data-stu-id="89e24-105">This tutorial is based on the [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="89e24-106"><a name="register"></a>Inscription de votre application pour l’authentification et configuration d’App Service</span><span class="sxs-lookup"><span data-stu-id="89e24-106"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="89e24-107"><a name="redirecturl"></a>Ajouter votre application aux URL de redirection externes autorisées</span><span class="sxs-lookup"><span data-stu-id="89e24-107"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="89e24-108">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="89e24-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="89e24-109">Cela permet au système d’authentification de vous rediriger vers votre application une fois le processus d’authentification terminé.</span><span class="sxs-lookup"><span data-stu-id="89e24-109">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span>  <span data-ttu-id="89e24-110">Dans ce didacticiel, nous utilisons le schéma d’URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="89e24-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="89e24-111">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="89e24-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="89e24-112">Il doit être propre à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="89e24-112">It should be unique to your mobile application.</span></span>  <span data-ttu-id="89e24-113">Pour activer la redirection côté serveur :</span><span class="sxs-lookup"><span data-stu-id="89e24-113">To enable the redirection on th server side:</span></span>

1. <span data-ttu-id="89e24-114">Dans le[ portail Azure], sélectionnez votre App Service.</span><span class="sxs-lookup"><span data-stu-id="89e24-114">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="89e24-115">Cliquez sur l’option de menu **Authentication/Authorisation**.</span><span class="sxs-lookup"><span data-stu-id="89e24-115">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="89e24-116">Sous la section **Fournisseurs d’authentification**, cliquez sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89e24-116">Click **Azure Active Directory** under the **Authentication Providers** section.</span></span>

4. <span data-ttu-id="89e24-117">Définissez le **mode de gestion** sur **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="89e24-117">Set the **Management mode** to **Advanced**.</span></span>

5. <span data-ttu-id="89e24-118">Dans **URL de redirection externes autorisées**, saisissez `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="89e24-118">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="89e24-119">La chaîne _appname_ de cette chaîne est le schéma d’URL de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="89e24-119">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="89e24-120">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="89e24-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="89e24-121">Vous devez noter la chaîne que vous choisissez, dans la mesure où vous devez ajuster votre code d’application mobile avec le schéma d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="89e24-121">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

6. <span data-ttu-id="89e24-122">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89e24-122">Click **OK**.</span></span>

7. <span data-ttu-id="89e24-123">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="89e24-123">Click **Save**.</span></span>

## <span data-ttu-id="89e24-124"><a name="permissions"></a>Restriction des autorisations pour les utilisateurs authentifiés</span><span class="sxs-lookup"><span data-stu-id="89e24-124"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="89e24-125">Dans Xcode, appuyez sur **Exécuter** pour démarrer l’application.</span><span class="sxs-lookup"><span data-stu-id="89e24-125">In Xcode, press **Run** to start the app.</span></span> <span data-ttu-id="89e24-126">Une exception se déclenche, car l’application essaye d’accéder au serveur principal en tant qu’utilisateur non authentifié alors que la table *TodoItem* requiert désormais l’authentification.</span><span class="sxs-lookup"><span data-stu-id="89e24-126">An exception is raised because the app attempts to access the backend as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="89e24-127"><a name="add-authentication"></a>Ajout de l'authentification à l'application</span><span class="sxs-lookup"><span data-stu-id="89e24-127"><a name="add-authentication"></a>Add authentication to app</span></span>
<span data-ttu-id="89e24-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="89e24-128">**Objective-C**:</span></span>

1. <span data-ttu-id="89e24-129">Sur votre Mac, ouvrez *QSTodoListViewController.m* dans Xcode et ajoutez la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="89e24-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add the following method:</span></span>

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    <span data-ttu-id="89e24-130">Remplacez *google* par *microsoftaccount*, *twitter*, *facebook* ou *windowsazureactivedirectory* si vous n’utilisez pas Google comme fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="89e24-130">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="89e24-131">Si vous utilisez Facebook, vous devrez [autoriser les domaines Facebook][1] dans votre application.</span><span class="sxs-lookup"><span data-stu-id="89e24-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="89e24-132">Remplacez **urlScheme** par un nom unique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="89e24-132">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="89e24-133">La chaîne urlScheme doit être identique au protocole de schéma d’URL spécifié dans le champ **URL de redirection externes autorisés** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="89e24-133">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="89e24-134">La chaîne urlScheme est utilisée par le rappel d’authentification pour revenir à votre application une fois la demande d’authentification terminée.</span><span class="sxs-lookup"><span data-stu-id="89e24-134">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="89e24-135">Remplacez `[self refresh]` dans `viewDidLoad` dans *QSTodoListViewController.m* par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="89e24-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with the following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="89e24-136">Ouvrez le fichier`QSAppDelegate.h` et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="89e24-136">Open the `QSAppDelegate.h` file and add the following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="89e24-137">Ouvrez le fichier`QSAppDelegate.m` et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="89e24-137">Open the `QSAppDelegate.m` file and add the following code:</span></span>

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   <span data-ttu-id="89e24-138">Ajoutez ce code juste avant la lecture de la ligne `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="89e24-138">Add this code directly before the line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="89e24-139">Remplacez la chaîne _appname_ par la valeur de urlScheme utilisée à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="89e24-139">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="89e24-140">Ouvrez le fichier `AppName-Info.plist` (en remplaçant AppName par le nom de votre application) et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="89e24-140">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="89e24-141">Ce code doit être placé dans l’élément `<dict>`.</span><span class="sxs-lookup"><span data-stu-id="89e24-141">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="89e24-142">Remplacez la chaîne _appname_ (dans le tableau pour **CFBundleURLSchemes**) par le nom d’application choisi à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="89e24-142">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="89e24-143">Vous pouvez également effectuer ces modifications dans l’éditeur plist - cliquez sur le fichier `AppName-Info.plist` dans XCode pour ouvrir l’éditeur plist.</span><span class="sxs-lookup"><span data-stu-id="89e24-143">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="89e24-144">Remplacez la chaîne `com.microsoft.azure.zumo` pour **CFBundleURLName** par votre identifiant d’offre groupée Apple.</span><span class="sxs-lookup"><span data-stu-id="89e24-144">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="89e24-145">Appuyez sur *Exécuter* pour démarrer l’application, puis ouvrez une session.</span><span class="sxs-lookup"><span data-stu-id="89e24-145">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="89e24-146">Une fois connecté, vous devez être en mesure d’afficher la liste des tâches et d’effectuer des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="89e24-146">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="89e24-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="89e24-147">**Swift**:</span></span>

1. <span data-ttu-id="89e24-148">Sur votre Mac, ouvrez *ToDoTableViewController.swift* dans Xcode et ajoutez la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="89e24-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add the following method:</span></span>

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    <span data-ttu-id="89e24-149">Remplacez *google* par *microsoftaccount*, *twitter*, *facebook* ou *windowsazureactivedirectory* si vous n’utilisez pas Google comme fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="89e24-149">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="89e24-150">Si vous utilisez Facebook, vous devrez [autoriser les domaines Facebook][1] dans votre application.</span><span class="sxs-lookup"><span data-stu-id="89e24-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="89e24-151">Remplacez **urlScheme** par un nom unique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="89e24-151">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="89e24-152">La chaîne urlScheme doit être identique au protocole de schéma d’URL spécifié dans le champ **URL de redirection externes autorisés** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="89e24-152">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="89e24-153">La chaîne urlScheme est utilisée par le rappel d’authentification pour revenir à votre application une fois la demande d’authentification terminée.</span><span class="sxs-lookup"><span data-stu-id="89e24-153">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="89e24-154">Supprimez les lignes `self.refreshControl?.beginRefreshing()` et `self.onRefresh(self.refreshControl)` à la fin de `viewDidLoad()` dans *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="89e24-154">Remove the lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="89e24-155">Ajoutez un appel à `loginAndGetData()` à leur place :</span><span class="sxs-lookup"><span data-stu-id="89e24-155">Add a call to `loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="89e24-156">Ouvrez le fichier `AppDelegate.swift` et ajoutez la ligne de suivante à la classe `AppDelegate` :</span><span class="sxs-lookup"><span data-stu-id="89e24-156">Open the `AppDelegate.swift` file and add the following line to the `AppDelegate` class:</span></span>

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    <span data-ttu-id="89e24-157">Remplacez la chaîne _appname_ par la valeur de urlScheme utilisée à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="89e24-157">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="89e24-158">Ouvrez le fichier `AppName-Info.plist` (en remplaçant AppName par le nom de votre application) et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="89e24-158">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="89e24-159">Ce code doit être placé dans l’élément `<dict>`.</span><span class="sxs-lookup"><span data-stu-id="89e24-159">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="89e24-160">Remplacez la chaîne _appname_ (dans le tableau pour **CFBundleURLSchemes**) par le nom d’application choisi à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="89e24-160">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="89e24-161">Vous pouvez également effectuer ces modifications dans l’éditeur plist - cliquez sur le fichier `AppName-Info.plist` dans XCode pour ouvrir l’éditeur plist.</span><span class="sxs-lookup"><span data-stu-id="89e24-161">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="89e24-162">Remplacez la chaîne `com.microsoft.azure.zumo` pour **CFBundleURLName** par votre identifiant d’offre groupée Apple.</span><span class="sxs-lookup"><span data-stu-id="89e24-162">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="89e24-163">Appuyez sur *Exécuter* pour démarrer l’application, puis ouvrez une session.</span><span class="sxs-lookup"><span data-stu-id="89e24-163">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="89e24-164">Une fois connecté, vous devez être en mesure d’afficher la liste des tâches et d’effectuer des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="89e24-164">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="89e24-165">L’authentification App Service utilise la communication inter-application d’Apple.</span><span class="sxs-lookup"><span data-stu-id="89e24-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="89e24-166">Pour plus d’informations sur ce sujet, reportez-vous à la [Documentation Apple][2]</span><span class="sxs-lookup"><span data-stu-id="89e24-166">For more details on this subject, refer to the [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
<span data-ttu-id="89e24-167">[ portail Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="89e24-167">[Azure portal]: https://portal.azure.com</span></span>

<span data-ttu-id="89e24-168">[Démarrage rapide iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="89e24-168">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>

