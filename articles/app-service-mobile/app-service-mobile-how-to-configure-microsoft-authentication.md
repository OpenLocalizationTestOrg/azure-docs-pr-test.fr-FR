---
title: Comment configurer l'authentification par compte Microsoft pour votre application App Services
description: "Découvrez comment configurer l'authentification par compte Microsoft pour votre application App Services."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 67386b03ae4cc683fe00e11e8dad19d1442eff09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-microsoft-account-login"></a><span data-ttu-id="93b71-103">Comment configurer votre application App Service pour utiliser une connexion par compte Microsoft</span><span class="sxs-lookup"><span data-stu-id="93b71-103">How to configure your App Service application to use Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="93b71-104">Cette rubrique montre comment configurer Azure App Service pour utiliser un compte Microsoft comme fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="93b71-104">This topic shows you how to configure Azure App Service to use Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="93b71-105"><a name="register-microsoft-account"> </a>Inscription de votre application avec un compte Microsoft</span><span class="sxs-lookup"><span data-stu-id="93b71-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="93b71-106">Connectez-vous au [portail Azure]et accédez à votre application.</span><span class="sxs-lookup"><span data-stu-id="93b71-106">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="93b71-107">Copiez votre **URL**, que vous utiliserez ultérieurement pour configurer votre application avec votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93b71-107">Copy your **URL**, which later you use to configure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="93b71-108">Accédez à la page [Mes applications] dans le Centre des développeurs de compte Microsoft, puis connectez-vous avec votre compte Microsoft si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="93b71-108">Navigate to the [My Applications] page in the Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="93b71-109">Cliquez sur **Ajouter une application**, puis tapez le nom de l’application et cliquez sur **Créer une application**.</span><span class="sxs-lookup"><span data-stu-id="93b71-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="93b71-110">Prenez note de l’ **ID d’application**, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="93b71-110">Make a note of the **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="93b71-111">Sous « Plateformes », cliquez sur **Ajouter une plateforme** et sélectionnez « Web ».</span><span class="sxs-lookup"><span data-stu-id="93b71-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="93b71-112">Sous « URI de redirection », entrez le point de terminaison de votre application, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="93b71-112">Under "Redirect URIs" supply the endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="93b71-113">Votre URI de redirection correspond à l’URL de votre application suivie du chemin d’accès, */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="93b71-113">Your redirect URI is the URL of your application appended with the path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="93b71-114">Par exemple, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="93b71-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="93b71-115">Assurez-vous d'utiliser le schéma HTTPS.</span><span class="sxs-lookup"><span data-stu-id="93b71-115">Make sure that you are using the HTTPS scheme.</span></span>
   
7. <span data-ttu-id="93b71-116">Sous « Secrets de l’application », cliquez sur **Générer un nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="93b71-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="93b71-117">Prenez note de la valeur qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="93b71-117">Make note of the value that appears.</span></span> <span data-ttu-id="93b71-118">Une fois que vous quittez cette page, le mot de passe ne s’affiche plus.</span><span class="sxs-lookup"><span data-stu-id="93b71-118">Once you leave the page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="93b71-119">Le mot de passe est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="93b71-119">The password is an important security credential.</span></span> <span data-ttu-id="93b71-120">Ne partagez le mot de passe avec personne et ne le distribuez pas dans une application cliente.</span><span class="sxs-lookup"><span data-stu-id="93b71-120">Do not share the password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="93b71-121"><a name="secrets"> </a>Ajout des informations de compte Microsoft à votre application App Service</span><span class="sxs-lookup"><span data-stu-id="93b71-121"><a name="secrets"> </a>Add Microsoft Account information to your App Service application</span></span>
1. <span data-ttu-id="93b71-122">Dans le [portail Azure], accédez à votre application et cliquez sur **Paramètres** > **Authentification / Autorisation**.</span><span class="sxs-lookup"><span data-stu-id="93b71-122">Back in the [Azure portal], navigate to your application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="93b71-123">Si la fonctionnalité Authentification / Autorisation n’est pas activée, définissez-la sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="93b71-123">If the Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="93b71-124">Cliquez sur **Compte Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="93b71-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="93b71-125">Collez les valeurs d’ID et de mot de passe de l’application que vous avez obtenues précédemment et activez éventuellement les étendues que votre application requiert.</span><span class="sxs-lookup"><span data-stu-id="93b71-125">Paste in the Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="93b71-126">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="93b71-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="93b71-127">Par défaut, App Service fournit une authentification, mais ne restreint pas l'accès autorisé à votre contenu et aux API de votre site.</span><span class="sxs-lookup"><span data-stu-id="93b71-127">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="93b71-128">Vous devez autoriser les utilisateurs dans votre code d'application.</span><span class="sxs-lookup"><span data-stu-id="93b71-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="93b71-129">(Facultatif) Pour restreindre l’accès à votre site aux seuls utilisateurs authentifiés par votre compte Microsoft, définissez **Action à exécuter quand une demande n’est pas authentifiée** sur **Compte Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="93b71-129">(Optional) To restrict access to your site to only users authenticated by Microsoft account, set **Action to take when request is not authenticated** to **Microsoft Account**.</span></span> <span data-ttu-id="93b71-130">Cela implique que toutes les demandes soient authentifiées. Toutes les demandes non authentifiées sont redirigées vers le compte Micrososft pour être authentifiées.</span><span class="sxs-lookup"><span data-stu-id="93b71-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Microsoft account for authentication.</span></span>
5. <span data-ttu-id="93b71-131">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="93b71-131">Click **Save**.</span></span>

<span data-ttu-id="93b71-132">Vous êtes maintenant prêt à utiliser un compte Microsoft pour l’authentification dans votre application.</span><span class="sxs-lookup"><span data-stu-id="93b71-132">You are now ready to use Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="93b71-133"><a name="related-content"> </a>Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="93b71-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[Mes applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portail Azure]: https://portal.azure.com/
