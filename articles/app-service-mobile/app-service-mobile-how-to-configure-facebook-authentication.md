---
title: "authentification Facebook aaaHow tooconfigure pour votre application de Services d’application"
description: "Découvrez comment tooconfigure l’authentification Facebook pour votre application de Services d’application."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a><span data-ttu-id="330fd-103">Comment tooconfigure la connexion de Facebook toouse de votre application du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="330fd-103">How tooconfigure your App Service application toouse Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="330fd-104">Cette rubrique vous montre comment tooconfigure Azure App Service toouse Facebook comme fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="330fd-104">This topic shows you how tooconfigure Azure App Service toouse Facebook as an authentication provider.</span></span>

<span data-ttu-id="330fd-105">procédure de hello toocomplete dans cette rubrique, vous devez disposer d’un compte Facebook qui a une adresse de messagerie vérifié et un numéro de téléphone mobile.</span><span class="sxs-lookup"><span data-stu-id="330fd-105">toocomplete hello procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="330fd-106">toocreate un nouveau compte Facebook, accédez trop[facebook.com].</span><span class="sxs-lookup"><span data-stu-id="330fd-106">toocreate a new Facebook account, go too[facebook.com].</span></span>

## <span data-ttu-id="330fd-107"><a name="register"></a>Inscription de votre application sur Facebook</span><span class="sxs-lookup"><span data-stu-id="330fd-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="330fd-108">Ouvrez une session sur toohello [portail Azure]et accédez tooyour application.</span><span class="sxs-lookup"><span data-stu-id="330fd-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="330fd-109">Copiez votre **URL**.</span><span class="sxs-lookup"><span data-stu-id="330fd-109">Copy your **URL**.</span></span> <span data-ttu-id="330fd-110">Vous utiliserez cette tooconfigure votre application Facebook.</span><span class="sxs-lookup"><span data-stu-id="330fd-110">You will use this tooconfigure your Facebook app.</span></span>
2. <span data-ttu-id="330fd-111">Dans une autre fenêtre de navigateur, accédez à toohello [aux développeurs de Facebook] site Web et connectez-vous avec votre Facebook des informations d’identification de compte.</span><span class="sxs-lookup"><span data-stu-id="330fd-111">In another browser window, navigate toohello [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="330fd-112">(Facultatif) Si vous n’êtes pas déjà inscrit, cliquez sur **applications** > **enregistrer en tant que développeur**, acceptez la politique de hello, puis suivez les étapes d’inscription de hello.</span><span class="sxs-lookup"><span data-stu-id="330fd-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept hello policy and follow hello registration steps.</span></span>
4. <span data-ttu-id="330fd-113">Cliquez sur **Mes applications** > **Ajouter une nouvelle application** > **Site Web** > **Ignorer et créer un ID d’application**.</span><span class="sxs-lookup"><span data-stu-id="330fd-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="330fd-114">Dans **nom d’affichage**, tapez un nom unique pour votre application, le type de votre **messagerie du Contact**, choisissez un **catégorie** pour votre application, puis cliquez sur **créer des ID d’application**et terminer la vérification de sécurité hello.</span><span class="sxs-lookup"><span data-stu-id="330fd-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete hello security check.</span></span> <span data-ttu-id="330fd-115">Vous passez le tableau de bord du développeur de toohello pour votre nouvelle application Facebook.</span><span class="sxs-lookup"><span data-stu-id="330fd-115">This takes you toohello developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="330fd-116">Sous « Facebook Login » (Connexion Facebook), cliquez sur **Get Started**(Prise en main).</span><span class="sxs-lookup"><span data-stu-id="330fd-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="330fd-117">Ajout de votre application **URI de redirection** trop**URI de redirection OAuth valide**, puis cliquez sur **enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="330fd-117">Add your application's **Redirect URI** too**Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="330fd-118">Votre URI de redirection est hello les URL de votre application ajoutée avec le chemin d’accès de hello, */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="330fd-118">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="330fd-119">Par exemple, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="330fd-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="330fd-120">Assurez-vous que vous utilisez le schéma HTTPS de hello.</span><span class="sxs-lookup"><span data-stu-id="330fd-120">Make sure that you are using hello HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="330fd-121">Dans hello navigation gauche, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="330fd-121">In hello left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="330fd-122">Sur hello **Secret d’application** , cliquez sur **afficher**, fournir votre mot de passe si demandé, puis prenez note des valeurs hello de **ID d’application** et **Secret d’application**.</span><span class="sxs-lookup"><span data-stu-id="330fd-122">On hello **App Secret** field, click **Show**, provide your password if requested, then make a note of hello values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="330fd-123">Vous utilisez ces tooconfigure ultérieure de votre application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="330fd-123">You use these later tooconfigure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="330fd-124">secret d’application Hello est une information d’identification de sécurité importantes.</span><span class="sxs-lookup"><span data-stu-id="330fd-124">hello app secret is an important security credential.</span></span> <span data-ttu-id="330fd-125">Ne partagez cette clé secrète avec personne et ne la distribuez pas dans une application cliente.</span><span class="sxs-lookup"><span data-stu-id="330fd-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="330fd-126">Hello compte Facebook qui a été utilisé tooregister hello application est un administrateur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="330fd-126">hello Facebook account which was used tooregister hello application is an administrator of hello app.</span></span> <span data-ttu-id="330fd-127">À ce stade, seuls les administrateurs peuvent se connecter à cette application.</span><span class="sxs-lookup"><span data-stu-id="330fd-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="330fd-128">tooauthenticate autres comptes Facebook, cliquez sur **révision d’application** et activer **rendent < votre-app-name > publics** tooenable accès public général à l’aide de l’authentification Facebook.</span><span class="sxs-lookup"><span data-stu-id="330fd-128">tooauthenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** tooenable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="330fd-129"><a name="secrets"></a>Tooyour d’application Facebook d’ajouter des informations</span><span class="sxs-lookup"><span data-stu-id="330fd-129"><a name="secrets"> </a>Add Facebook information tooyour application</span></span>
1. <span data-ttu-id="330fd-130">Dans hello [portail Azure], accédez tooyour application.</span><span class="sxs-lookup"><span data-stu-id="330fd-130">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="330fd-131">Cliquez sur **Paramètres** > **Authentification / Autorisation**, et vérifiez que **l’authentification App Service** est activée, sur **On**.</span><span class="sxs-lookup"><span data-stu-id="330fd-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="330fd-132">Cliquez sur **Facebook**, collez dans les valeurs d’ID d’application et le Secret de l’application hello que vous avez obtenu précédemment, si vous le souhaitez activer toutes les étendues requises par votre application, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="330fd-132">Click **Facebook**, paste in hello App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="330fd-133">Par défaut, le Service d’applications fournit l’authentification mais ne restreint pas les API et contenu de site tooyour autorisé à accéder.</span><span class="sxs-lookup"><span data-stu-id="330fd-133">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="330fd-134">Vous devez autoriser les utilisateurs dans votre code d'application.</span><span class="sxs-lookup"><span data-stu-id="330fd-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="330fd-135">(Facultatif) toorestrict accès tooyour site tooonly les utilisateurs authentifiés par Facebook, définissez **tootake Action lors de la demande n’est pas authentifiée** trop**Facebook**.</span><span class="sxs-lookup"><span data-stu-id="330fd-135">(Optional) toorestrict access tooyour site tooonly users authenticated by Facebook, set **Action tootake when request is not authenticated** too**Facebook**.</span></span> <span data-ttu-id="330fd-136">Cela requiert que toutes les demandes authentifiées, et toutes les demandes non authentifiées sont redirigée tooFacebook pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="330fd-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooFacebook for authentication.</span></span>
4. <span data-ttu-id="330fd-137">Lorsque vous avez terminé de configurer l’authentification, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="330fd-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="330fd-138">Vous êtes maintenant prêt toouse Facebook pour l’authentification dans votre application.</span><span class="sxs-lookup"><span data-stu-id="330fd-138">You are now ready toouse Facebook for authentication in your app.</span></span>

## <span data-ttu-id="330fd-139"><a name="related-content"></a>Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="330fd-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[aux développeurs de Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[portail Azure]: https://portal.azure.com/
