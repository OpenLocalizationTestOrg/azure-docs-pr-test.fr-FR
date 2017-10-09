---
title: application de plateforme Windows universelle (UWP) aaaAdd authentication tooyour | Documents Microsoft
description: "Découvrez comment toouse Azure App Service Mobile Apps tooauthenticate les utilisateurs de votre application de plateforme Windows universelle (UWP) à l’aide de divers modules fournisseurs d’identité, y compris : AAD, Google, Facebook, Twitter et Microsoft."
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
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="95f5d-103">Ajouter l’application Windows authentification tooyour</span><span class="sxs-lookup"><span data-stu-id="95f5d-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="95f5d-104">Cette rubrique vous montre comment application mobile du tooyour tooadd l’authentification basée sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="95f5d-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="95f5d-105">Dans ce didacticiel, vous ajouter le projet de démarrage rapide de l’authentification toohello plateforme Windows universelle (UWP) pour les applications mobiles à l’aide d’un fournisseur d’identité qui est pris en charge par le Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="95f5d-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="95f5d-106">Après avoir en cours a été authentifié et autorisé par votre serveur principal de l’application Mobile, la valeur d’ID utilisateur hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="95f5d-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="95f5d-107">Ce didacticiel est basé sur le démarrage rapide pour des applications mobiles hello.</span><span class="sxs-lookup"><span data-stu-id="95f5d-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="95f5d-108">Vous devez d’abord terminer le didacticiel de hello [prise en main les applications mobiles](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="95f5d-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="95f5d-109"><a name="register"></a>Inscrire votre application pour l’authentification et de configurer hello du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="95f5d-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="95f5d-110"><a name="redirecturl"></a>Ajouter votre URL de redirection externe d’autorisé toohello application</span><span class="sxs-lookup"><span data-stu-id="95f5d-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="95f5d-111">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="95f5d-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="95f5d-112">Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="95f5d-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="95f5d-113">Dans ce didacticiel, nous utilisons le modèle d’URL hello _appname_ dans l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="95f5d-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="95f5d-114">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="95f5d-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="95f5d-115">Il doit être unique tooyour des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="95f5d-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="95f5d-116">redirection de hello tooenable côté serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="95f5d-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="95f5d-117">Bonjour [Azure portal], sélectionnez votre application de Service.</span><span class="sxs-lookup"><span data-stu-id="95f5d-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="95f5d-118">Cliquez sur hello **l’authentification / autorisation** option de menu.</span><span class="sxs-lookup"><span data-stu-id="95f5d-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="95f5d-119">Bonjour **autorisé des URL de redirection externe**, entrez `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="95f5d-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="95f5d-120">Hello **url_scheme_of_your_app** de cette chaîne est hello le modèle d’URL pour votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="95f5d-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="95f5d-121">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="95f5d-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="95f5d-122">Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="95f5d-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="95f5d-123">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95f5d-123">Click **OK**.</span></span>

5. <span data-ttu-id="95f5d-124">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="95f5d-124">Click **Save**.</span></span>

## <span data-ttu-id="95f5d-125"><a name="permissions"></a>Restreindre les autorisations des utilisateurs tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="95f5d-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="95f5d-126">Maintenant, vous pouvez vérifier que ce principal de tooyour l’accès anonyme a été désactivé.</span><span class="sxs-lookup"><span data-stu-id="95f5d-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="95f5d-127">Avec le projet d’application UWP hello définir comme projet de démarrage hello, déployer et exécuter l’application hello ; Vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="95f5d-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="95f5d-128">Cela se produit car l’application hello tente tooaccess le Code de votre application Mobile comme un utilisateur non authentifié, mais hello *TodoItem* table requiert l’authentification.</span><span class="sxs-lookup"><span data-stu-id="95f5d-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="95f5d-129">Ensuite, vous mettrez à jour les utilisateurs de hello application tooauthenticate avant de demander des ressources à partir de votre application de Service.</span><span class="sxs-lookup"><span data-stu-id="95f5d-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="95f5d-130"><a name="add-authentication"></a>Ajouter une application de toohello d’authentification</span><span class="sxs-lookup"><span data-stu-id="95f5d-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="95f5d-131">Dans le projet d’application UWP hello MainPage.xaml.cs et ajoutez hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="95f5d-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
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
   
    <span data-ttu-id="95f5d-132">Ce code s’authentifie l’utilisateur hello avec une connexion Facebook.</span><span class="sxs-lookup"><span data-stu-id="95f5d-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="95f5d-133">Si vous utilisez un fournisseur d’identité autre que Facebook, modifiez la valeur hello **MobileServiceAuthenticationProvider** au-dessus de valeur toohello pour votre fournisseur.</span><span class="sxs-lookup"><span data-stu-id="95f5d-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="95f5d-134">Remplacez hello **OnNavigatedTo()** méthode dans MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="95f5d-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="95f5d-135">Ensuite, vous allez ajouter un **connectez-vous** application toohello bouton qui déclenche l’authentification.</span><span class="sxs-lookup"><span data-stu-id="95f5d-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="95f5d-136">Ajoutez hello suivant extrait de code toohello MainPage.xaml.cs :</span><span class="sxs-lookup"><span data-stu-id="95f5d-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="95f5d-137">Ouvrir le fichier de projet hello MainPage.xaml, recherchez des élément hello qui définit hello **enregistrer** bouton et remplacez-le par hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="95f5d-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
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
5. <span data-ttu-id="95f5d-138">Ajoutez hello suivant extrait de code toohello App.xaml.cs :</span><span class="sxs-lookup"><span data-stu-id="95f5d-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

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
6. <span data-ttu-id="95f5d-139">Ouvrez le fichier Package.appxmanifest, accédez trop**déclarations**, dans **déclarations disponibles** liste déroulante, sélectionnez **protocole** et cliquez sur **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="95f5d-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="95f5d-140">À présent configurer hello **propriétés** Hello **protocole** déclaration.</span><span class="sxs-lookup"><span data-stu-id="95f5d-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="95f5d-141">Dans **nom d’affichage**, ajoutez le nom hello toousers toodisplay de votre application.</span><span class="sxs-lookup"><span data-stu-id="95f5d-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="95f5d-142">Dans **Nom**, ajoutez votre {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="95f5d-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="95f5d-143">Appuyez sur la touche application de hello hello F5 toorun clé, cliquez sur hello **connectez-vous** bouton et connectez-vous à application hello avec votre fournisseur d’identité choisi.</span><span class="sxs-lookup"><span data-stu-id="95f5d-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="95f5d-144">Une fois que votre connexion est réussie, application hello s’exécute sans erreur et sont en mesure de tooquery votre serveur principal et d’effectuer des mises à jour toodata.</span><span class="sxs-lookup"><span data-stu-id="95f5d-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="95f5d-145"><a name="tokens"></a>Jeton d’authentification hello banque d’informations sur le client de hello</span><span class="sxs-lookup"><span data-stu-id="95f5d-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="95f5d-146">Hello l’exemple précédent a montré une standard sign-in, ce qui nécessite hello client toocontact à la fois le fournisseur d’identité hello et hello App Service chaque fois que cette application hello démarre.</span><span class="sxs-lookup"><span data-stu-id="95f5d-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="95f5d-147">Est non seulement cette méthode inefficace, vous pouvez exécuter dans l’utilisation-se rapporte les problèmes de nombreux clients essayez toostart votre application à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="95f5d-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="95f5d-148">Une meilleure approche est le jeton d’autorisation toocache hello retournées par votre Service d’applications et essayez toouse cela tout d’abord avant d’utiliser un fournisseur connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="95f5d-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="95f5d-149">Vous pouvez mettre en cache jeton hello émis par les Services d’application, quelle que soit la que vous utilisez l’authentification de client géré ou par le service.</span><span class="sxs-lookup"><span data-stu-id="95f5d-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="95f5d-150">Ce didacticiel utilise cette dernière.</span><span class="sxs-lookup"><span data-stu-id="95f5d-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="95f5d-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95f5d-151">Next steps</span></span>
<span data-ttu-id="95f5d-152">Maintenant que vous terminé ce didacticiel de l’authentification de base, pensez à poursuivre sur tooone Hello suivant didacticiels :</span><span class="sxs-lookup"><span data-stu-id="95f5d-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="95f5d-153">Ajouter une application de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="95f5d-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="95f5d-154">Découvrez comment les notifications push tooadd prennent en charge tooyour application et configurer votre application Mobile back-end toouse Azure Notification Hubs toosend les notifications de transmission.</span><span class="sxs-lookup"><span data-stu-id="95f5d-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="95f5d-155">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="95f5d-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="95f5d-156">Découvrez comment tooadd hors connexion prennent en charge votre application à l’aide d’un serveur principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="95f5d-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="95f5d-157">Synchronisation hors connexion permet de toointeract les utilisateurs finaux avec une application mobile&mdash;affichage, l’ajout ou la modification des données&mdash;même quand il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="95f5d-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
