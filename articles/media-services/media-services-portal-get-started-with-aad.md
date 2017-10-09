---
title: "aaaGet démarrée avec l’authentification Azure AD à l’aide de hello portail Azure | Documents Microsoft"
description: "Découvrez comment toouse hello tooaccess portail Azure tooconsume d’authentification Azure Active Directory (Azure AD) hello API Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a><span data-ttu-id="5b4fb-103">Prise en main d’authentification Azure AD à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5b4fb-103">Get started with Azure AD authentication by using hello Azure portal</span></span>

<span data-ttu-id="5b4fb-104">Découvrez comment toouse hello Azure tooaccess portail Azure Active Directory (Azure AD) d’authentification tooaccess hello API Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-104">Learn how toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) authentication tooaccess hello Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b4fb-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5b4fb-105">Prerequisites</span></span>

- <span data-ttu-id="5b4fb-106">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-106">An Azure account.</span></span> <span data-ttu-id="5b4fb-107">Si vous n’avez pas de compte, commencez avec un [essai gratuit Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b4fb-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="5b4fb-108">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-108">A Media Services account.</span></span> <span data-ttu-id="5b4fb-109">Pour plus d’informations, consultez [créer un compte Azure Media Services à l’aide de hello Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="5b4fb-109">For more information, see [Create an Azure Media Services account by using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="5b4fb-110">Assurez-vous que vous passez en revue hello [l’accès à des API Azure Media Services avec une vue d’ensemble de l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="5b4fb-110">Make sure you review hello [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="5b4fb-111">Lorsque vous utilisez l’authentification Azure AD avec Azure Media Services, vous disposez de deux options d’authentification :</span><span class="sxs-lookup"><span data-stu-id="5b4fb-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="5b4fb-112">**Authentification utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-112">**User authentication**.</span></span> <span data-ttu-id="5b4fb-113">Authentifier un utilisateur de hello application toointeract avec les ressources de Media Services.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-113">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="5b4fb-114">les applications interactives Hello doivent tout d’abord utilisateur hello pour les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-114">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="5b4fb-115">Un exemple est une application de console de gestion utilisée par les tâches d’encodage toomonitor des utilisateurs autorisés ou la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-115">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="5b4fb-116">**Authentification d’un principal de service**.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-116">**Service principal authentication**.</span></span> <span data-ttu-id="5b4fb-117">Authentifiez un service.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-117">Authenticate a service.</span></span> <span data-ttu-id="5b4fb-118">Les applications qui utilisent généralement cette méthode d’authentification sont des applications qui exécutent des services démon, des services de niveau intermédiaire ou des travaux planifiés : applications web, applications de fonction, applications logiques, API ou microservices.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b4fb-119">Actuellement, Media Services prend en charge le modèle d’authentification hello Azure Access Control service.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-119">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="5b4fb-120">Toutefois, l’autorisation Access Control sera déconseillée à compter du 1er juin 2018.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="5b4fb-121">Nous vous recommandons de migrer modèle d’authentification Azure AD de toohello dès que possible.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-121">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

## <a name="select-hello-authentication-method"></a><span data-ttu-id="5b4fb-122">Sélectionnez la méthode d’authentification hello</span><span class="sxs-lookup"><span data-stu-id="5b4fb-122">Select hello authentication method</span></span>

1. <span data-ttu-id="5b4fb-123">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-123">In hello [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="5b4fb-124">Sélectionnez la façon dont tooconnect toohello API Media Services.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-124">Select how tooconnect toohello Media Services API.</span></span>

    ![Sélectionner la page de méthode de connexion](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="5b4fb-126">Authentification utilisateur</span><span class="sxs-lookup"><span data-stu-id="5b4fb-126">User authentication</span></span>

<span data-ttu-id="5b4fb-127">tooconnect toohello API Media Services à l’aide de hello option d’authentification utilisateur, hello client application doit toorequest un jeton d’Azure AD a hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="5b4fb-127">tooconnect toohello Media Services API by using hello user authentication option, hello client app needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="5b4fb-128">Point de terminaison de locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b4fb-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="5b4fb-129">URI de ressource Media Services</span><span class="sxs-lookup"><span data-stu-id="5b4fb-129">Media Services resource URI</span></span>
* <span data-ttu-id="5b4fb-130">ID client d’application Media Services (natif)</span><span class="sxs-lookup"><span data-stu-id="5b4fb-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="5b4fb-131">URI de redirection d’application Media Services (natif)</span><span class="sxs-lookup"><span data-stu-id="5b4fb-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="5b4fb-132">URI de ressource pour REST Media Services</span><span class="sxs-lookup"><span data-stu-id="5b4fb-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="5b4fb-133">Vous pouvez obtenir les valeurs hello pour ces paramètres sur hello **API Media Services avec l’authentification utilisateur** page.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-133">You can get hello values for these parameters on hello **Media Services API with user authentication** page.</span></span> 

![Se connecter à la page d’authentification utilisateur](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="5b4fb-135">Si vous vous connectez toohello API Media Services à l’aide de hello Media Services Microsoft .NET SDK, hello requis valeurs tooyou disponible en tant que partie du Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-135">If you connect toohello Media Services API by using hello Media Services Microsoft .NET SDK, hello required values are available tooyou as part of hello SDK.</span></span> <span data-ttu-id="5b4fb-136">Pour plus d’informations, consultez [utilisent Azure AD authentication tooaccess hello API Azure Media Services avec .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="5b4fb-136">For more information, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="5b4fb-137">Si vous n’utilisez pas le client de Media Services .NET hello SDK, vous devez créer manuellement une demande de jeton Azure AD à l’aide de paramètres hello abordées précédemment.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-137">If you're not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using hello parameters discussed earlier.</span></span> <span data-ttu-id="5b4fb-138">Pour plus d’informations, consultez [comment toouse hello Azure AD Authentication Library tooget hello jeton Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="5b4fb-138">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="5b4fb-139">Authentification d’un principal du service</span><span class="sxs-lookup"><span data-stu-id="5b4fb-139">Service principal authentication</span></span>

<span data-ttu-id="5b4fb-140">tooconnect toohello API Media Services à l’aide de hello option principal de service, votre application de couche intermédiaire (API web ou une application web) doit toorequest un jeton d’Azure AD a hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="5b4fb-140">tooconnect toohello Media Services API by using hello service principal option, your middle-tier app (web API or web application) needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="5b4fb-141">Point de terminaison de locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b4fb-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="5b4fb-142">URI de ressource Media Services</span><span class="sxs-lookup"><span data-stu-id="5b4fb-142">Media Services resource URI</span></span> 
* <span data-ttu-id="5b4fb-143">URI de ressource pour REST Media Services</span><span class="sxs-lookup"><span data-stu-id="5b4fb-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="5b4fb-144">Valeurs de l’application Azure AD : hello **ID client** et **question secrète du client**</span><span class="sxs-lookup"><span data-stu-id="5b4fb-144">Azure AD application values: hello **client ID** and **client secret**</span></span>

<span data-ttu-id="5b4fb-145">Vous pouvez obtenir les valeurs hello pour ces paramètres sur hello **Rejoignez tooMedia API des Services de principal du service** page.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-145">You can get hello values for these parameters on hello **Connect tooMedia Services API with service principal** page.</span></span> <span data-ttu-id="5b4fb-146">Utilisez cette page de toocreate un nouvel Azure application AD ou tooselect un existant.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-146">Use this page toocreate a new Azure AD application or tooselect an existing one.</span></span> <span data-ttu-id="5b4fb-147">Après avoir sélectionné des application Azure AD de hello, vous pouvez obtenir l’ID de client hello (ID d’Application) et générer des valeurs de clé secrète (clé) de client hello.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-147">After you select hello Azure AD app, you can get hello client ID (Application ID) and generate hello client secret (key) values.</span></span> 

![Se connecter à la page du principal de service](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="5b4fb-149">Hello lorsque **Principal du Service** panneau s’ouvre, l’application Azure AD première hello répondant hello suivant des critères est activée :</span><span class="sxs-lookup"><span data-stu-id="5b4fb-149">When hello **Service Principal** blade opens, hello first Azure AD application that meets hello following criteria is selected:</span></span>

- <span data-ttu-id="5b4fb-150">Il s’agit d’une application Azure AD inscrite.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="5b4fb-151">Il dispose d’autorisations de collaborateur ou Owner Role-Based le contrôle d’accès sur le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-151">It has Contributor or Owner Role-Based Access Control permissions on hello account.</span></span>

<span data-ttu-id="5b4fb-152">Une fois que vous créez ou sélectionnez une application Azure AD, vous pouvez créer et copier une question secrète du client (clé) et hello client ID (ID d’Application).</span><span class="sxs-lookup"><span data-stu-id="5b4fb-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and hello client ID (Application ID).</span></span> <span data-ttu-id="5b4fb-153">l’ID de client et de la clé secrète du client Hello sont un jeton d’accès hello tooget requis dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-153">hello client secret and client ID are required tooget hello access token in this scenario.</span></span>

<span data-ttu-id="5b4fb-154">Si vous n’avez pas applications Azure AD de toocreate autorisations dans votre domaine, les contrôles d’application Azure AD hello du Panneau de hello ne sont pas affichés, et un message d’avertissement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-154">If you don't have permissions toocreate Azure AD apps in your domain, hello Azure AD app controls of hello blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="5b4fb-155">Si vous vous connectez toohello API Media Services à l’aide de hello Media Services .NET SDK, consultez [utilisent Azure AD authentication tooaccess hello API Azure Media Services avec .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="5b4fb-155">If you connect toohello Media Services API by using hello Media Services .NET SDK, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="5b4fb-156">Si vous n’utilisez pas de client de Media Services .NET hello SDK, vous devez créer manuellement une demande de jeton Azure AD à l’aide de paramètres hello abordées précédemment.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-156">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request using hello parameters discussed earlier.</span></span> <span data-ttu-id="5b4fb-157">Pour plus d’informations, consultez [comment toouse hello Azure AD Authentication Library tooget hello jeton Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="5b4fb-157">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-hello-client-id-and-client-secret"></a><span data-ttu-id="5b4fb-158">Obtenir les client hello client et le code secret</span><span class="sxs-lookup"><span data-stu-id="5b4fb-158">Get hello client ID and client secret</span></span>

<span data-ttu-id="5b4fb-159">Après avoir sélectionné une application Azure AD existante hello sélectionnez option toocreate un nouveau, hello suivant boutons s’affichent :</span><span class="sxs-lookup"><span data-stu-id="5b4fb-159">After you select an existing Azure AD app or select hello option toocreate a new one, hello following buttons appear:</span></span>

![Bouton Gérer les autorisations et bouton Gérer l’application](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="5b4fb-161">tooopen hello panneau des applications Azure AD, cliquez sur **gérer application**.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-161">tooopen hello Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="5b4fb-162">Sur hello **gérer application** panneau, vous pouvez obtenir un ID de client de l’application hello (ID d’Application).</span><span class="sxs-lookup"><span data-stu-id="5b4fb-162">On hello **Manage application** blade, you can get hello app's client ID (Application ID).</span></span> <span data-ttu-id="5b4fb-163">toogenerate une clé secrète client (clé), sélectionnez **clés**.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-163">toogenerate a client secret (key), select **Keys**.</span></span>

![Option Clés du panneau Gérer l’application](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a><span data-ttu-id="5b4fb-165">Gérer les autorisations et l’application hello</span><span class="sxs-lookup"><span data-stu-id="5b4fb-165">Manage permissions and hello application</span></span>

<span data-ttu-id="5b4fb-166">Après avoir sélectionné des application Azure AD de hello, vous pouvez gérer les autorisations et l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-166">After you select hello Azure AD application, you can manage hello application and permissions.</span></span> <span data-ttu-id="5b4fb-167">tooset votre tooaccess d’application Azure AD d’autres applications, cliquez sur **gérer les autorisations**.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-167">tooset up your Azure AD application tooaccess other applications, click **Manage permissions**.</span></span> <span data-ttu-id="5b4fb-168">Pour les tâches de gestion, telles que la modification des clés et les URL de réponse ou tooedit hello du manifeste d’application, cliquez sur **gérer application**.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-168">For management tasks, such as changing keys and reply URLs, or tooedit hello application’s manifest, click **Manage application**.</span></span>

### <a name="edit-hello-apps-settings-or-manifest"></a><span data-ttu-id="5b4fb-169">Modifier les paramètres de l’application hello ou le manifeste.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-169">Edit hello app's settings or manifest</span></span>

<span data-ttu-id="5b4fb-170">paramètres d’application tooedit hello ou de manifeste, cliquez sur **gérer application**.</span><span class="sxs-lookup"><span data-stu-id="5b4fb-170">tooedit hello app's settings or manifest, click **Manage application**.</span></span>

![Page Gérer l’application](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="5b4fb-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b4fb-172">Next steps</span></span>

<span data-ttu-id="5b4fb-173">Prise en main [téléchargement de fichiers tooyour compte](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="5b4fb-173">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
