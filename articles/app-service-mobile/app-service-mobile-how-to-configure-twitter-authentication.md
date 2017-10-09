---
title: "aaaHow tooconfigure Twitter l’authentification pour votre application de Services d’application"
description: "Découvrez comment l’authentification Twitter tooconfigure pour votre application de Services d’application."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a><span data-ttu-id="702d7-103">Comment tooconfigure votre connexion de Service d’applications application toouse Twitter</span><span class="sxs-lookup"><span data-stu-id="702d7-103">How tooconfigure your App Service application toouse Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="702d7-104">Cette rubrique vous montre comment tooconfigure Azure App Service toouse Twitter comme fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="702d7-104">This topic shows you how tooconfigure Azure App Service toouse Twitter as an authentication provider.</span></span>

<span data-ttu-id="702d7-105">procédure de hello toocomplete dans cette rubrique, vous devez disposer d’un compte Twitter qui a un messagerie vérifié adresse et numéro de téléphone.</span><span class="sxs-lookup"><span data-stu-id="702d7-105">toocomplete hello procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="702d7-106">toocreate un nouveau compte Twitter, accédez trop<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="702d7-106">toocreate a new Twitter account, go too<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="702d7-107"><a name="register"></a>Inscription de votre application avec Twitter</span><span class="sxs-lookup"><span data-stu-id="702d7-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="702d7-108">Ouvrez une session sur toohello [portail Azure]et accédez tooyour application.</span><span class="sxs-lookup"><span data-stu-id="702d7-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="702d7-109">Copiez votre **URL**.</span><span class="sxs-lookup"><span data-stu-id="702d7-109">Copy your **URL**.</span></span> <span data-ttu-id="702d7-110">Vous utiliserez cette tooconfigure votre application Twitter.</span><span class="sxs-lookup"><span data-stu-id="702d7-110">You will use this tooconfigure your Twitter app.</span></span>
2. <span data-ttu-id="702d7-111">Accédez toohello [aux développeurs de Twitter] site Web, connectez-vous avec vos informations d’identification du compte Twitter, puis cliquez sur **créer une application**.</span><span class="sxs-lookup"><span data-stu-id="702d7-111">Navigate toohello [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="702d7-112">Type Bonjour **nom** et un **Description** pour votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="702d7-112">Type in hello **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="702d7-113">Coller dans votre application **URL** pour hello **site Web** valeur.</span><span class="sxs-lookup"><span data-stu-id="702d7-113">Paste in your application's **URL** for hello **Website** value.</span></span> <span data-ttu-id="702d7-114">Ensuite, pour hello **URL de rappel**, collez hello **URL de rappel** vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="702d7-114">Then, for hello **Callback URL**, paste hello **Callback URL** you copied earlier.</span></span> <span data-ttu-id="702d7-115">Voici la passerelle d’application Mobile ajoutée au chemin d’accès de hello, */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="702d7-115">This is your Mobile App gateway appended with hello path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="702d7-116">Par exemple, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="702d7-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="702d7-117">Assurez-vous que vous utilisez le schéma HTTPS de hello.</span><span class="sxs-lookup"><span data-stu-id="702d7-117">Make sure that you are using hello HTTPS scheme.</span></span>
4. <span data-ttu-id="702d7-118">Dans la page de hello hello bas, lisez et acceptez les termes du contrat de hello.</span><span class="sxs-lookup"><span data-stu-id="702d7-118">At hello bottom hello page, read and accept hello terms.</span></span> <span data-ttu-id="702d7-119">Ensuite, cliquez sur **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="702d7-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="702d7-120">Cette application hello de registres affiche les détails de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="702d7-120">This registers hello app displays hello application details.</span></span>
5. <span data-ttu-id="702d7-121">Cliquez sur hello **paramètres** onglet, vérifiez **autoriser cette toosign de toobe utilisé application connecter avec Twitter**, puis cliquez sur **les paramètres de mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="702d7-121">Click hello **Settings** tab, check **Allow this application toobe used toosign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="702d7-122">Sélectionnez hello **clés et les jetons d’accès** onglet. Prenez note des valeurs hello de **Consumer Key (clé d’API)** et **question secrète du client (clé secrète API)**.</span><span class="sxs-lookup"><span data-stu-id="702d7-122">Select hello **Keys and Access Tokens** tab. Make a note of hello values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="702d7-123">secret de consommateur Hello est une information d’identification de sécurité importantes.</span><span class="sxs-lookup"><span data-stu-id="702d7-123">hello consumer secret is an important security credential.</span></span> <span data-ttu-id="702d7-124">Ne partagez pas cette clé secrète avec quiconque et ne la distribuez pas avec votre application.</span><span class="sxs-lookup"><span data-stu-id="702d7-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="702d7-125"><a name="secrets"></a>Ajouter Twitter d’application des informations tooyour</span><span class="sxs-lookup"><span data-stu-id="702d7-125"><a name="secrets"> </a>Add Twitter information tooyour application</span></span>
1. <span data-ttu-id="702d7-126">Dans hello [portail Azure], accédez tooyour application.</span><span class="sxs-lookup"><span data-stu-id="702d7-126">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="702d7-127">Cliquez sur **Paramètres**, puis sur **Authentification/Autorisation**.</span><span class="sxs-lookup"><span data-stu-id="702d7-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="702d7-128">Si l’authentification de hello / la fonctionnalité d’autorisation n’est pas activée, activer hello trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="702d7-128">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="702d7-129">Cliquez sur **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="702d7-129">Click **Twitter**.</span></span> <span data-ttu-id="702d7-130">Collez hello ID d’application et Secret d’application les valeurs que vous avez obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="702d7-130">Paste in hello App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="702d7-131">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="702d7-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="702d7-132">Par défaut, le Service d’applications fournit l’authentification mais ne restreint pas les API et contenu de site tooyour autorisé à accéder.</span><span class="sxs-lookup"><span data-stu-id="702d7-132">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="702d7-133">Vous devez autoriser les utilisateurs dans votre code d'application.</span><span class="sxs-lookup"><span data-stu-id="702d7-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="702d7-134">(Facultatif) toorestrict accès tooyour site tooonly les utilisateurs authentifiés par Twitter, définissez **tootake Action lors de la demande n’est pas authentifiée** trop**Twitter**.</span><span class="sxs-lookup"><span data-stu-id="702d7-134">(Optional) toorestrict access tooyour site tooonly users authenticated by Twitter, set **Action tootake when request is not authenticated** too**Twitter**.</span></span> <span data-ttu-id="702d7-135">Cela requiert que toutes les demandes authentifiées, et toutes les demandes non authentifiées sont redirigée tooTwitter pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="702d7-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooTwitter for authentication.</span></span>
5. <span data-ttu-id="702d7-136">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="702d7-136">Click **Save**.</span></span>

<span data-ttu-id="702d7-137">Vous êtes maintenant prêt toouse Twitter pour l’authentification dans votre application.</span><span class="sxs-lookup"><span data-stu-id="702d7-137">You are now ready toouse Twitter for authentication in your app.</span></span>

## <span data-ttu-id="702d7-138"><a name="related-content"></a>Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="702d7-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[aux développeurs de Twitter]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portail Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
