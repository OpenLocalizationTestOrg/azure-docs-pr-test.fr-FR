---
title: "aaaHow tooconfigure Account Microsoft l’authentification pour votre application de Services d’application"
description: "Découvrez comment l’authentification de Microsoft Account tooconfigure pour votre application de Services d’application."
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
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="7faa2-103">Comment tooconfigure votre connexion au Service d’applications application toouse Account Microsoft</span><span class="sxs-lookup"><span data-stu-id="7faa2-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="7faa2-104">Cette rubrique vous montre comment tooconfigure Azure App Service toouse Account Microsoft comme fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="7faa2-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="7faa2-105"><a name="register-microsoft-account"></a>Inscription de votre application avec un compte Microsoft</span><span class="sxs-lookup"><span data-stu-id="7faa2-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="7faa2-106">Ouvrez une session sur toohello [portail Azure]et accédez tooyour application.</span><span class="sxs-lookup"><span data-stu-id="7faa2-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="7faa2-107">Copiez votre **URL**, qui vous utiliserez tooconfigure votre application avec Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7faa2-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="7faa2-108">Accédez toohello [Mes Applications] page hello Microsoft Account Developer Center et connectez-vous avec votre compte Microsoft, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7faa2-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="7faa2-109">Cliquez sur **Ajouter une application**, puis tapez le nom de l’application et cliquez sur **Créer une application**.</span><span class="sxs-lookup"><span data-stu-id="7faa2-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="7faa2-110">Prenez note de hello **ID de l’Application**, car vous en aurez besoin plus tard.</span><span class="sxs-lookup"><span data-stu-id="7faa2-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="7faa2-111">Sous « Plateformes », cliquez sur **Ajouter une plateforme** et sélectionnez « Web ».</span><span class="sxs-lookup"><span data-stu-id="7faa2-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="7faa2-112">Sous « URI de redirection » approvisionnement hello point de terminaison pour votre application, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7faa2-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7faa2-113">Votre URI de redirection est hello les URL de votre application ajoutée avec le chemin d’accès de hello, */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="7faa2-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="7faa2-114">Par exemple, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="7faa2-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="7faa2-115">Assurez-vous que vous utilisez le schéma HTTPS de hello.</span><span class="sxs-lookup"><span data-stu-id="7faa2-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="7faa2-116">Sous « Secrets de l’application », cliquez sur **Générer un nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7faa2-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="7faa2-117">Notez la valeur hello qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7faa2-117">Make note of hello value that appears.</span></span> <span data-ttu-id="7faa2-118">Une fois que vous quittez la page de hello, il ne sera pas affiché à nouveau.</span><span class="sxs-lookup"><span data-stu-id="7faa2-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7faa2-119">mot de passe Hello est une information d’identification de sécurité importantes.</span><span class="sxs-lookup"><span data-stu-id="7faa2-119">hello password is an important security credential.</span></span> <span data-ttu-id="7faa2-120">Ne partagez le mot de passe de hello avec d’autres personnes ou le distribuer dans une application cliente.</span><span class="sxs-lookup"><span data-stu-id="7faa2-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="7faa2-121"><a name="secrets"></a>Ajouter un compte Microsoft informations tooyour application de Service d’application</span><span class="sxs-lookup"><span data-stu-id="7faa2-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="7faa2-122">Dans hello [portail Azure], accédez tooyour application, cliquez sur **paramètres** > **l’authentification / autorisation**.</span><span class="sxs-lookup"><span data-stu-id="7faa2-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="7faa2-123">Si l’authentification de hello / la fonctionnalité d’autorisation n’est pas activée, connectez-le **sur**.</span><span class="sxs-lookup"><span data-stu-id="7faa2-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="7faa2-124">Cliquez sur **Compte Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="7faa2-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="7faa2-125">Coller dans les valeurs hello ID d’Application et le mot de passe que vous avez obtenu précédemment et vous pouvez éventuellement activer des étendues de que votre application requiert.</span><span class="sxs-lookup"><span data-stu-id="7faa2-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="7faa2-126">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7faa2-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="7faa2-127">Par défaut, le Service d’applications fournit l’authentification mais ne restreint pas les API et contenu de site tooyour autorisé à accéder.</span><span class="sxs-lookup"><span data-stu-id="7faa2-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="7faa2-128">Vous devez autoriser les utilisateurs dans votre code d'application.</span><span class="sxs-lookup"><span data-stu-id="7faa2-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="7faa2-129">(Facultatif) toorestrict tooyour site tooonly les utilisateurs d’accès authentifiés par un compte Microsoft, définissez **tootake Action lors de la demande n’est pas authentifiée** trop**Account Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="7faa2-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="7faa2-130">Cela requiert que toutes les demandes authentifiées, et toutes les demandes non authentifiées sont redirigées compte tooMicrosoft pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="7faa2-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="7faa2-131">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7faa2-131">Click **Save**.</span></span>

<span data-ttu-id="7faa2-132">Vous êtes maintenant prêt toouse Account Microsoft pour l’authentification dans votre application.</span><span class="sxs-lookup"><span data-stu-id="7faa2-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="7faa2-133"><a name="related-content"></a>Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="7faa2-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[Mes Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portail Azure]: https://portal.azure.com/
