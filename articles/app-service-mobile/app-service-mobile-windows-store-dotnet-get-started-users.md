---
title: "Ajout de authentification à votre plateforme Windows universelle (UWP) | Microsoft Docs"
description: "Découvrez comment utiliser Azure App Service Mobile Apps pour authentifier les utilisateurs de votre application de plateforme Windows universelle à l’aide de divers fournisseurs d'identité, notamment AAD, Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 47da343d4ec956ec2e669757f56e853675f887a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-windows-app"></a><span data-ttu-id="ca1ad-103">Ajout de l'authentification à votre application Windows</span><span class="sxs-lookup"><span data-stu-id="ca1ad-103">Add authentication to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="ca1ad-104">Cette rubrique indique comment ajouter l'authentification basée sur le cloud à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-104">This topic shows you how to add cloud-based authentication to your mobile app.</span></span> <span data-ttu-id="ca1ad-105">Dans ce didacticiel, vous ajoutez l'authentification au projet de démarrage rapide de plateforme Windows universelle pour Mobile Apps à l'aide d'un fournisseur d'identité pris en charge par Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="ca1ad-106">Une fois l'utilisateur authentifié et autorisé par votre backend d'application Mobile, la valeur de l'ID utilisateur s'affiche.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span></span>

<span data-ttu-id="ca1ad-107">Ce didacticiel est basé sur le démarrage rapide de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-107">This tutorial is based on the Mobile Apps quickstart.</span></span> <span data-ttu-id="ca1ad-108">Vous devez commencer par suivre le didacticiel [Prise en main de Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ca1ad-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="ca1ad-109"><a name="register"></a>Inscription de votre application pour l’authentification et configuration d’App Service</span><span class="sxs-lookup"><span data-stu-id="ca1ad-109"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="ca1ad-110"><a name="redirecturl"></a>Ajouter votre application aux URL de redirection externes autorisées</span><span class="sxs-lookup"><span data-stu-id="ca1ad-110"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="ca1ad-111">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="ca1ad-112">Cela permet au système d’authentification de vous rediriger vers votre application une fois le processus d’authentification terminé.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-112">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="ca1ad-113">Dans ce didacticiel, nous utilisons le schéma d’URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-113">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="ca1ad-114">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="ca1ad-115">Il doit être propre à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-115">It should be unique to your mobile application.</span></span> <span data-ttu-id="ca1ad-116">Pour activer la redirection côté serveur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ca1ad-116">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="ca1ad-117">Dans le [portail Azure], sélectionnez votre instance App Service.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-117">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="ca1ad-118">Cliquez sur l’option de menu **Authentication/Authorisation**.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-118">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="ca1ad-119">Dans **URL de redirection externes autorisées**, saisissez `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-119">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="ca1ad-120">La chaîne **url_scheme_of_your_app** de cette chaîne est le schéma d’URL de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-120">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="ca1ad-121">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="ca1ad-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="ca1ad-122">Vous devez noter la chaîne que vous choisissez, dans la mesure où vous devez ajuster votre code d’application mobile avec le schéma d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-122">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="ca1ad-123">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-123">Click **OK**.</span></span>

5. <span data-ttu-id="ca1ad-124">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-124">Click **Save**.</span></span>

## <span data-ttu-id="ca1ad-125"><a name="permissions"></a>Restriction des autorisations pour les utilisateurs authentifiés</span><span class="sxs-lookup"><span data-stu-id="ca1ad-125"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="ca1ad-126">À présent, vous pouvez vérifier que l’accès anonyme à votre serveur principal a été désactivé.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-126">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="ca1ad-127">Avec le projet d’application Windows défini en tant que projet de démarrage, déployez et exécutez l'application, et vérifiez qu'une exception non prise en charge avec le code d'état 401 (Non autorisé) est déclenchée après le démarrage de l'application.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-127">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="ca1ad-128">Cette exception se produit, car l’application tente d’accéder à votre code Mobile App en tant qu’utilisateur non authentifié, alors que la table *TodoItem* requiert désormais une authentification.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-128">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="ca1ad-129">Ensuite, vous allez mettre à jour l'application pour authentifier les utilisateurs avant de demander des ressources à partir de votre service App Service.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-129">Next, you will update the app to authenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="ca1ad-130"><a name="add-authentication"></a>Ajout de l’authentification à l’application</span><span class="sxs-lookup"><span data-stu-id="ca1ad-130"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="ca1ad-131">Dans le fichier de projet d’application UWP MainPage.xaml.cs, ajoutez l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="ca1ad-131">In the UWP app project file MainPage.xaml.cs and add the following code snippet:</span></span>
   
        // Define a member variable for storing the signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs the authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' to the name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    <span data-ttu-id="ca1ad-132">Ce code authentifie l’utilisateur à l’aide d’une connexion Facebook.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-132">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="ca1ad-133">Si vous utilisez un fournisseur d'identité différent de Facebook, remplacez la valeur de **MobileServiceAuthenticationProvider** ci-dessus par la valeur de votre fournisseur.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-133">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="ca1ad-134">Remplacez la méthode **OnNavigatedTo()** dans MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-134">Replace the **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="ca1ad-135">Ensuite, vous allez ajouter à l’application un bouton **Connexion** qui déclenche l’authentification.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-135">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="ca1ad-136">Ajoutez l’extrait de code suivant dans MainPage.xaml.cs :</span><span class="sxs-lookup"><span data-stu-id="ca1ad-136">Add the following code snippet to the MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login the user and then load data from the mobile app.
            if (await AuthenticateAsync())
            {
                // Switch the buttons and load items from the mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="ca1ad-137">Ouvrez le fichier de projet MainPage.xaml, recherchez l’élément qui définit le bouton **Enregistrer** et remplacez-le par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="ca1ad-137">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span></span>
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. <span data-ttu-id="ca1ad-138">Ajoutez l’extrait de code suivant dans App.xaml.cs :</span><span class="sxs-lookup"><span data-stu-id="ca1ad-138">Add the following code snippet to the App.xaml.cs:</span></span>

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. <span data-ttu-id="ca1ad-139">Ouvrez le fichier Package.appxmanifest, accédez à **Déclarations**, dans la liste déroulante **Déclarations disponibles**, sélectionnez **Protocole** et cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-139">Open Package.appxmanifest file, navigate to **Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="ca1ad-140">À présent, configurez les **propriétés** de la déclaration **Protocole**.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-140">Now configure the **Properties** of the **Protocol** declaration.</span></span> <span data-ttu-id="ca1ad-141">Dans **Nom d’affichage**, ajoutez le nom que vous souhaitez montrer aux utilisateurs de votre application.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-141">In **Display name**, add the name you wish to display to users of your application.</span></span> <span data-ttu-id="ca1ad-142">Dans **Nom**, ajoutez votre {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="ca1ad-143">Appuyez sur la touche F5 pour exécuter l'application, puis cliquez sur le bouton **Se connecter** pour vous connecter à l'application avec le fournisseur d'identité choisi.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-143">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> <span data-ttu-id="ca1ad-144">Lorsque vous êtes connecté, l'application s'exécute sans erreur, et vous pouvez exécuter des requêtes sur votre backend et mettre à jour les données.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-144">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span></span>

## <span data-ttu-id="ca1ad-145"><a name="tokens"></a>Stockage du jeton d’authentification sur le client</span><span class="sxs-lookup"><span data-stu-id="ca1ad-145"><a name="tokens"></a>Store the authentication token on the client</span></span>
<span data-ttu-id="ca1ad-146">L’exemple précédent montrait une connexion standard, qui nécessite que le client contacte le fournisseur d’identité et le service d’application à chaque démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-146">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span></span> <span data-ttu-id="ca1ad-147">Cette méthode est non seulement inefficace, mais vous pouvez rencontrer des problèmes d'utilisation si de nombreux clients tentent de lancer votre application en même temps.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span></span> <span data-ttu-id="ca1ad-148">Une meilleure approche consiste à mettre en cache le jeton d’autorisation renvoyé par votre service d’application et à l’utiliser en premier avant de faire appel à la connexion via un fournisseur.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-148">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="ca1ad-149">Vous pouvez mettre en cache le jeton émis par App Services, que vous utilisiez l’authentification gérée par un client ou gérée par un service.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-149">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="ca1ad-150">Ce didacticiel utilise cette dernière.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="ca1ad-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ca1ad-151">Next steps</span></span>
<span data-ttu-id="ca1ad-152">Maintenant que vous avez terminé ce didacticiel sur l'authentification de base, vous pouvez passer à l'un des didacticiels suivants :</span><span class="sxs-lookup"><span data-stu-id="ca1ad-152">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="ca1ad-153">Ajouter des notifications Push à votre application Android</span><span class="sxs-lookup"><span data-stu-id="ca1ad-153">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="ca1ad-154">Apprenez à ajouter la prise en charge des notifications Push à votre application et à configurer le serveur principal d’applications mobiles pour utiliser Azure Notification Hubs afin d’envoyer des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-154">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="ca1ad-155">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="ca1ad-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="ca1ad-156">Apprenez à ajouter une prise en charge hors connexion à votre application à l’aide d’un backend Mobile App.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-156">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="ca1ad-157">La synchronisation hors connexion permet aux utilisateurs finaux d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="ca1ad-157">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
