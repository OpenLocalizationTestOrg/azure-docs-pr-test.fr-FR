---
title: "aaaHow tooconfigure Google l’authentification pour votre application de Services d’application"
description: "Découvrez comment l’authentification Google tooconfigure pour votre application de Services d’application."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="82339-103">Comment tooconfigure votre compte de connexion du Service d’applications application toouse Google</span><span class="sxs-lookup"><span data-stu-id="82339-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="82339-104">Cette rubrique vous montre comment tooconfigure Azure App Service toouse Google comme fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="82339-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="82339-105">procédure de hello toocomplete dans cette rubrique, vous devez disposer d’un compte Google qui possède une adresse de messagerie vérifié.</span><span class="sxs-lookup"><span data-stu-id="82339-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="82339-106">toocreate un nouveau compte Google, accédez trop[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="82339-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="82339-107"><a name="register"></a>Inscription de votre application avec Google</span><span class="sxs-lookup"><span data-stu-id="82339-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="82339-108">Ouvrez une session sur toohello [portail Azure]et accédez tooyour application.</span><span class="sxs-lookup"><span data-stu-id="82339-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="82339-109">Copiez votre **URL**, qui vous utilisez tooconfigure ultérieure de votre application de Google.</span><span class="sxs-lookup"><span data-stu-id="82339-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="82339-110">Accédez toohello [API Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) cliquez sur le site Web, connectez-vous avec vos informations d’identification du compte Google, **créer un projet de**, fournissez un **nom du projet**, puis cliquez sur  **Créer**.</span><span class="sxs-lookup"><span data-stu-id="82339-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="82339-111">Sous **API sociales**, cliquez sur **API Google+** puis **Activer**.</span><span class="sxs-lookup"><span data-stu-id="82339-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="82339-112">Bonjour, barre de navigation gauche **informations d’identification** > **écran de consentement OAuth**, puis sélectionnez votre **adresse de messagerie**, entrez un **nomduproduit**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="82339-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="82339-113">Bonjour **informations d’identification** , cliquez sur **créer les informations d’identification** > **ID de client OAuth**, puis sélectionnez **application Web**.</span><span class="sxs-lookup"><span data-stu-id="82339-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="82339-114">Coller hello du Service d’applications **URL** vous avez copiée précédemment dans **origines JavaScript**, puis collez votre redirection URI en **URI de redirection autorisés**.</span><span class="sxs-lookup"><span data-stu-id="82339-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="82339-115">Hello URI de redirection est hello les URL de votre application ajoutée avec le chemin d’accès de hello, */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="82339-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="82339-116">Par exemple, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="82339-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="82339-117">Assurez-vous que vous utilisez le schéma HTTPS de hello.</span><span class="sxs-lookup"><span data-stu-id="82339-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="82339-118">Cliquez ensuite sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="82339-118">Then click **Create**.</span></span>
7. <span data-ttu-id="82339-119">Sur l’écran suivant de hello, prenez note des valeurs hello du client de hello secret ID et le client.</span><span class="sxs-lookup"><span data-stu-id="82339-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="82339-120">question secrète du client Hello est une information d’identification de sécurité importantes.</span><span class="sxs-lookup"><span data-stu-id="82339-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="82339-121">Ne partagez cette clé secrète avec personne et ne la distribuez pas dans une application cliente.</span><span class="sxs-lookup"><span data-stu-id="82339-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="82339-122"><a name="secrets"></a>Tooyour d’application Google d’ajouter des informations</span><span class="sxs-lookup"><span data-stu-id="82339-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="82339-123">Dans hello [portail Azure], accédez tooyour application.</span><span class="sxs-lookup"><span data-stu-id="82339-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="82339-124">Cliquez sur **Paramètres**, puis sur **Authentification/Autorisation**.</span><span class="sxs-lookup"><span data-stu-id="82339-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="82339-125">Si l’authentification de hello / la fonctionnalité d’autorisation n’est pas activée, activer hello trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="82339-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="82339-126">Cliquez sur **Google**.</span><span class="sxs-lookup"><span data-stu-id="82339-126">Click **Google**.</span></span> <span data-ttu-id="82339-127">Coller dans les valeurs d’ID d’application et le Secret de l’application hello que vous avez obtenu précédemment et vous pouvez éventuellement activer des étendues de que votre application requiert.</span><span class="sxs-lookup"><span data-stu-id="82339-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="82339-128">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="82339-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="82339-129">Par défaut, le Service d’applications fournit l’authentification mais ne restreint pas les API et contenu de site tooyour autorisé à accéder.</span><span class="sxs-lookup"><span data-stu-id="82339-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="82339-130">Vous devez autoriser les utilisateurs dans votre code d'application.</span><span class="sxs-lookup"><span data-stu-id="82339-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="82339-131">(Facultatif) toorestrict accès tooyour site tooonly les utilisateurs authentifiés par Google, définissez **tootake Action lors de la demande n’est pas authentifiée** trop**Google**.</span><span class="sxs-lookup"><span data-stu-id="82339-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="82339-132">Cela requiert que toutes les demandes authentifiées, et toutes les demandes non authentifiées sont redirigée tooGoogle pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="82339-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="82339-133">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="82339-133">Click **Save**.</span></span>

<span data-ttu-id="82339-134">Vous êtes maintenant prêt toouse Google pour l’authentification dans votre application.</span><span class="sxs-lookup"><span data-stu-id="82339-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="82339-135"><a name="related-content"></a>Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="82339-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portail Azure]: https://portal.azure.com/

