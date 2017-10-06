---
title: "aaaAdd d’authentification sur iOS avec les applications mobiles Azure"
description: "Découvrez comment toouse Azure Mobile Apps tooauthenticate les utilisateurs de votre application iOS via une variété de fournisseurs d’identité, notamment AAD, Google, Facebook, Twitter et Microsoft."
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
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a><span data-ttu-id="ac895-103">Ajouter une application de l’authentification tooyour iOS</span><span class="sxs-lookup"><span data-stu-id="ac895-103">Add authentication tooyour iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="ac895-104">Dans ce didacticiel, vous ajoutez l’authentification toohello [iOS rapides Démarrer] de projet à l’aide d’un fournisseur d’identité pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ac895-104">In this tutorial, you add authentication toohello [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="ac895-105">Ce didacticiel est basé sur hello [iOS rapides Démarrer] didacticiel, vous devez effectuer en premier.</span><span class="sxs-lookup"><span data-stu-id="ac895-105">This tutorial is based on hello [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="ac895-106"><a name="register"></a>Inscrire votre application pour l’authentification et de configurer hello du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="ac895-106"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="ac895-107"><a name="redirecturl"></a>Ajouter votre URL de redirection externe d’autorisé toohello application</span><span class="sxs-lookup"><span data-stu-id="ac895-107"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="ac895-108">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ac895-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="ac895-109">Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="ac895-109">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span>  <span data-ttu-id="ac895-110">Dans ce didacticiel, nous utilisons le schéma d’URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="ac895-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="ac895-111">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="ac895-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="ac895-112">Il doit être unique tooyour des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="ac895-112">It should be unique tooyour mobile application.</span></span>  <span data-ttu-id="ac895-113">redirection de hello tooenable côté serveur de th :</span><span class="sxs-lookup"><span data-stu-id="ac895-113">tooenable hello redirection on th server side:</span></span>

1. <span data-ttu-id="ac895-114">Bonjour [portail Azure], sélectionnez votre application de Service.</span><span class="sxs-lookup"><span data-stu-id="ac895-114">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="ac895-115">Cliquez sur hello **l’authentification / autorisation** option de menu.</span><span class="sxs-lookup"><span data-stu-id="ac895-115">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="ac895-116">Cliquez sur **Azure Active Directory** sous hello **fournisseurs d’authentification** section.</span><span class="sxs-lookup"><span data-stu-id="ac895-116">Click **Azure Active Directory** under hello **Authentication Providers** section.</span></span>

4. <span data-ttu-id="ac895-117">Ensemble hello **mode de gestion** trop**avancé**.</span><span class="sxs-lookup"><span data-stu-id="ac895-117">Set hello **Management mode** too**Advanced**.</span></span>

5. <span data-ttu-id="ac895-118">Bonjour **autorisé des URL de redirection externe**, entrez `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="ac895-118">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="ac895-119">Hello _appname_ dans cette chaîne est hello le modèle d’URL pour votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="ac895-119">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="ac895-120">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="ac895-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="ac895-121">Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="ac895-121">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

6. <span data-ttu-id="ac895-122">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ac895-122">Click **OK**.</span></span>

7. <span data-ttu-id="ac895-123">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ac895-123">Click **Save**.</span></span>

## <span data-ttu-id="ac895-124"><a name="permissions"></a>Restreindre les autorisations des utilisateurs tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="ac895-124"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="ac895-125">Dans Xcode, appuyez sur **exécuter** toostart hello application.</span><span class="sxs-lookup"><span data-stu-id="ac895-125">In Xcode, press **Run** toostart hello app.</span></span> <span data-ttu-id="ac895-126">Une exception est levée, car l’application hello tente tooaccess le serveur principal en tant qu’un utilisateur non authentifié, mais hello *TodoItem* table requiert l’authentification.</span><span class="sxs-lookup"><span data-stu-id="ac895-126">An exception is raised because hello app attempts tooaccess the backend as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="ac895-127"><a name="add-authentication"></a>Ajouter l’authentification tooapp</span><span class="sxs-lookup"><span data-stu-id="ac895-127"><a name="add-authentication"></a>Add authentication tooapp</span></span>
<span data-ttu-id="ac895-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ac895-128">**Objective-C**:</span></span>

1. <span data-ttu-id="ac895-129">Sur votre Mac, ouvrez *QSTodoListViewController.m* dans Xcode et ajoutez hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="ac895-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="ac895-130">Modification *google* trop*microsoftaccount*, *twitter*, *facebook*, ou *windowsazureactivedirectory* si vous n’utilisez pas de Google comme fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="ac895-130">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="ac895-131">Si vous utilisez Facebook, vous devrez [autoriser les domaines Facebook][1] dans votre application.</span><span class="sxs-lookup"><span data-stu-id="ac895-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="ac895-132">Remplacez hello **urlScheme** avec un nom unique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ac895-132">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="ac895-133">Hello urlScheme doit être hello même comme hello protocole de modèle d’URL que vous avez spécifié dans hello **autorisé des URL de redirection externe** champ hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ac895-133">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="ac895-134">Hello urlScheme est utilisé par hello authentification rappel tooswitch tooyour arrière application une fois la demande d’authentification est terminée.</span><span class="sxs-lookup"><span data-stu-id="ac895-134">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="ac895-135">Remplacez `[self refresh]` dans `viewDidLoad` dans *QSTodoListViewController.m* avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="ac895-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with hello following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="ac895-136">Ouvrez hello `QSAppDelegate.h` et ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="ac895-136">Open hello `QSAppDelegate.h` file and add hello following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="ac895-137">Ouvrez hello `QSAppDelegate.m` et ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="ac895-137">Open hello `QSAppDelegate.m` file and add hello following code:</span></span>

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

   <span data-ttu-id="ac895-138">Ajoutez ce code juste avant la lecture de ligne hello `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="ac895-138">Add this code directly before hello line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="ac895-139">Remplacez le _appname_ permanence hello urlScheme valeur que vous avez utilisé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="ac895-139">Replace the _appname_ wih hello urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="ac895-140">Ouvrez hello `AppName-Info.plist` (en remplaçant AppName avec nom hello de votre application) et ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="ac895-140">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="ac895-141">Ce code doit être placé à l’intérieur de hello `<dict>` élément.</span><span class="sxs-lookup"><span data-stu-id="ac895-141">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="ac895-142">Remplacez hello _appname_ chaîne (dans le tableau pour **CFBundleURLSchemes**) avec le nom de l’application hello choisi à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="ac895-142">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="ac895-143">Vous pouvez également apporter ces modifications dans hello plist éditeur - cliquez sur hello `AppName-Info.plist` fichier dans XCode tooopen hello plist éditeur.</span><span class="sxs-lookup"><span data-stu-id="ac895-143">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="ac895-144">Remplacez hello `com.microsoft.azure.zumo` de chaîne pour **CFBundleURLName** avec votre Apple identificateur d’offres groupées.</span><span class="sxs-lookup"><span data-stu-id="ac895-144">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="ac895-145">Appuyez sur *exécuter* toostart hello app, puis connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="ac895-145">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="ac895-146">Lorsque vous êtes connecté, vous devez être en mesure de tooview hello Todo liste et effectuer des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="ac895-146">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="ac895-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ac895-147">**Swift**:</span></span>

1. <span data-ttu-id="ac895-148">Sur votre Mac, ouvrez *ToDoTableViewController.swift* dans Xcode et ajoutez hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="ac895-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="ac895-149">Modification *google* trop*microsoftaccount*, *twitter*, *facebook*, ou *windowsazureactivedirectory* si vous n’utilisez pas de Google comme fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="ac895-149">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="ac895-150">Si vous utilisez Facebook, vous devrez [autoriser les domaines Facebook][1] dans votre application.</span><span class="sxs-lookup"><span data-stu-id="ac895-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="ac895-151">Remplacez hello **urlScheme** avec un nom unique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ac895-151">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="ac895-152">Hello urlScheme doit être hello même comme hello protocole de modèle d’URL que vous avez spécifié dans hello **autorisé des URL de redirection externe** champ hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ac895-152">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="ac895-153">Hello urlScheme est utilisé par hello authentification rappel tooswitch tooyour arrière application une fois la demande d’authentification est terminée.</span><span class="sxs-lookup"><span data-stu-id="ac895-153">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="ac895-154">Supprimer les lignes hello `self.refreshControl?.beginRefreshing()` et `self.onRefresh(self.refreshControl)` à la fin de `viewDidLoad()` dans *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="ac895-154">Remove hello lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="ac895-155">Ajoutez un appel trop`loginAndGetData()` à leur place :</span><span class="sxs-lookup"><span data-stu-id="ac895-155">Add a call too`loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="ac895-156">Ouvrez hello `AppDelegate.swift` et ajoutez hello suivant ligne toohello `AppDelegate` classe :</span><span class="sxs-lookup"><span data-stu-id="ac895-156">Open hello `AppDelegate.swift` file and add hello following line toohello `AppDelegate` class:</span></span>

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

    <span data-ttu-id="ac895-157">Remplacez hello _appname_ permanence hello urlScheme valeur que vous avez utilisé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="ac895-157">Replace hello _appname_ wih hello urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="ac895-158">Ouvrez hello `AppName-Info.plist` (en remplaçant AppName avec nom hello de votre application) et ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="ac895-158">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="ac895-159">Ce code doit être placé à l’intérieur de hello `<dict>` élément.</span><span class="sxs-lookup"><span data-stu-id="ac895-159">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="ac895-160">Remplacez hello _appname_ chaîne (dans le tableau pour **CFBundleURLSchemes**) avec le nom de l’application hello choisi à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="ac895-160">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="ac895-161">Vous pouvez également apporter ces modifications dans hello plist éditeur - cliquez sur hello `AppName-Info.plist` fichier dans XCode tooopen hello plist éditeur.</span><span class="sxs-lookup"><span data-stu-id="ac895-161">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="ac895-162">Remplacez hello `com.microsoft.azure.zumo` de chaîne pour **CFBundleURLName** avec votre Apple identificateur d’offres groupées.</span><span class="sxs-lookup"><span data-stu-id="ac895-162">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="ac895-163">Appuyez sur *exécuter* toostart hello app, puis connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="ac895-163">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="ac895-164">Lorsque vous êtes connecté, vous devez être en mesure de tooview hello Todo liste et effectuer des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="ac895-164">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="ac895-165">L’authentification App Service utilise la communication inter-application d’Apple.</span><span class="sxs-lookup"><span data-stu-id="ac895-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="ac895-166">Pour plus d’informations sur ce sujet, consultez toohello [Documentation Apple][2]</span><span class="sxs-lookup"><span data-stu-id="ac895-166">For more details on this subject, refer toohello [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[portail Azure]: https://portal.azure.com

[iOS rapides Démarrer]: app-service-mobile-ios-get-started.md

