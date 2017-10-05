---
title: "Prise en main de l’authentification Azure AD à l’aide du portail Azure | Microsoft Docs"
description: "Découvrez comment utiliser le portail Azure pour accéder à l’authentification Azure Active Directory (Azure AD) en vue d’utiliser l’API Azure Media Services."
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
ms.openlocfilehash: 829e0759f8aeb8758f6b8895b88b60b66ffb22ed
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-the-azure-portal"></a><span data-ttu-id="d4f3f-103">Prise en main de l’authentification Azure AD à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d4f3f-103">Get started with Azure AD authentication by using the Azure portal</span></span>

<span data-ttu-id="d4f3f-104">Découvrez comment utiliser le portail Azure pour accéder à l’authentification Azure Active Directory (Azure AD) en vue d’accéder à l’API Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-104">Learn how to use the Azure portal to access Azure Active Directory (Azure AD) authentication to access the Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4f3f-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d4f3f-105">Prerequisites</span></span>

- <span data-ttu-id="d4f3f-106">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-106">An Azure account.</span></span> <span data-ttu-id="d4f3f-107">Si vous n’avez pas de compte, commencez avec un [essai gratuit Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="d4f3f-108">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-108">A Media Services account.</span></span> <span data-ttu-id="d4f3f-109">Pour plus d’informations, consultez [Création d’un compte Azure Media Services à l’aide du portail Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-109">For more information, see [Create an Azure Media Services account by using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="d4f3f-110">Assurez-vous de consulter [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md) (Vue d’ensemble de l’accès à l’API Azure Media Services avec l’authentification Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-110">Make sure you review the [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="d4f3f-111">Lorsque vous utilisez l’authentification Azure AD avec Azure Media Services, vous disposez de deux options d’authentification :</span><span class="sxs-lookup"><span data-stu-id="d4f3f-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="d4f3f-112">**Authentification utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-112">**User authentication**.</span></span> <span data-ttu-id="d4f3f-113">Authentifiez une personne qui utilise l’application pour interagir avec les ressources Media Services.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-113">Authenticate a person who is using the app to interact with Media Services resources.</span></span> <span data-ttu-id="d4f3f-114">L’application interactive invite tout d’abord l’utilisateur à entrer ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-114">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="d4f3f-115">Par exemple, une application de console de gestion peut être utilisée par les utilisateurs autorisés pour contrôler les travaux d’encodage ou de streaming en direct.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-115">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="d4f3f-116">**Authentification d’un principal de service**.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-116">**Service principal authentication**.</span></span> <span data-ttu-id="d4f3f-117">Authentifiez un service.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-117">Authenticate a service.</span></span> <span data-ttu-id="d4f3f-118">Les applications qui utilisent généralement cette méthode d’authentification sont des applications qui exécutent des services démon, des services de niveau intermédiaire ou des travaux planifiés : applications web, applications de fonction, applications logiques, API ou microservices.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4f3f-119">À l’heure actuelle, Media Services prend en charge le modèle d’authentification du service Azure Access Control.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-119">Currently, Media Services supports the Azure Access Control service authentication model.</span></span> <span data-ttu-id="d4f3f-120">Toutefois, l’autorisation Access Control sera déconseillée à compter du 1er juin 2018.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="d4f3f-121">Nous vous recommandons de migrer vers le modèle d’authentification Azure AD dès que possible.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-121">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span></span>

## <a name="select-the-authentication-method"></a><span data-ttu-id="d4f3f-122">Sélectionner la méthode d’authentification</span><span class="sxs-lookup"><span data-stu-id="d4f3f-122">Select the authentication method</span></span>

1. <span data-ttu-id="d4f3f-123">Dans le [portail Azure](https://portal.azure.com/), sélectionnez votre compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-123">In the [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="d4f3f-124">Choisissez comment vous connecter à l’API Media Services.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-124">Select how to connect to the Media Services API.</span></span>

    ![Sélectionner la page de méthode de connexion](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="d4f3f-126">Authentification utilisateur</span><span class="sxs-lookup"><span data-stu-id="d4f3f-126">User authentication</span></span>

<span data-ttu-id="d4f3f-127">Pour vous connecter à l’API Media Services à l’aide de l’option d’authentification utilisateur, l’application cliente doit demander un jeton Azure AD qui possède les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="d4f3f-127">To connect to the Media Services API by using the user authentication option, the client app needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="d4f3f-128">Point de terminaison de locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4f3f-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="d4f3f-129">URI de ressource Media Services</span><span class="sxs-lookup"><span data-stu-id="d4f3f-129">Media Services resource URI</span></span>
* <span data-ttu-id="d4f3f-130">ID client d’application Media Services (natif)</span><span class="sxs-lookup"><span data-stu-id="d4f3f-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="d4f3f-131">URI de redirection d’application Media Services (natif)</span><span class="sxs-lookup"><span data-stu-id="d4f3f-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="d4f3f-132">URI de ressource pour REST Media Services</span><span class="sxs-lookup"><span data-stu-id="d4f3f-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="d4f3f-133">Vous pouvez obtenir les valeurs de ces paramètres sur la page **Se connecter à l’API Media Services avec l’authentification utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-133">You can get the values for these parameters on the **Media Services API with user authentication** page.</span></span> 

![Se connecter à la page d’authentification utilisateur](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="d4f3f-135">Si vous vous connectez à l’API Media Services à l’aide du Kit de développement logiciel (SDK) Media Services Microsoft .NET, les valeurs requises sont disponibles dans le cadre du Kit de développement.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-135">If you connect to the Media Services API by using the Media Services Microsoft .NET SDK, the required values are available to you as part of the SDK.</span></span> <span data-ttu-id="d4f3f-136">Pour plus d’informations, consultez [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md) (Utiliser l’authentification Azure AD pour accéder à l’API Azure Media Services avec .NET).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-136">For more information, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="d4f3f-137">Si vous n’utilisez pas le Kit de développement logiciel (SDK) du client Media Services .NET, vous devez créer manuellement une demande de jeton Azure AD en utilisant les paramètres décrits précédemment.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-137">If you're not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using the parameters discussed earlier.</span></span> <span data-ttu-id="d4f3f-138">Pour plus d’informations, consultez [Bibliothèques d’authentification d’Azure Active Directory](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-138">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="d4f3f-139">Authentification d’un principal du service</span><span class="sxs-lookup"><span data-stu-id="d4f3f-139">Service principal authentication</span></span>

<span data-ttu-id="d4f3f-140">Pour vous connecter à l’API Media Services à l’aide de l’option de principal de service, votre application de niveau intermédiaire (API web ou application API) doit demander un jeton Azure AD qui possède les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="d4f3f-140">To connect to the Media Services API by using the service principal option, your middle-tier app (web API or web application) needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="d4f3f-141">Point de terminaison de locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4f3f-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="d4f3f-142">URI de ressource Media Services</span><span class="sxs-lookup"><span data-stu-id="d4f3f-142">Media Services resource URI</span></span> 
* <span data-ttu-id="d4f3f-143">URI de ressource pour REST Media Services</span><span class="sxs-lookup"><span data-stu-id="d4f3f-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="d4f3f-144">Valeurs de l’application Azure AD : **ID client** et **clé secrète client**</span><span class="sxs-lookup"><span data-stu-id="d4f3f-144">Azure AD application values: the **client ID** and **client secret**</span></span>

<span data-ttu-id="d4f3f-145">Vous pouvez obtenir les valeurs de ces paramètres sur la page **Se connecter à l’API Media Services avec le principal de service**.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-145">You can get the values for these parameters on the **Connect to Media Services API with service principal** page.</span></span> <span data-ttu-id="d4f3f-146">Utilisez cette page pour créer une application Azure AD ou sélectionnez-en une existante.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-146">Use this page to create a new Azure AD application or to select an existing one.</span></span> <span data-ttu-id="d4f3f-147">Après avoir sélectionné l’application Azure AD, vous pouvez obtenir l’ID client (ID d’application) et générer les valeurs de clé secrète client (clé).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-147">After you select the Azure AD app, you can get the client ID (Application ID) and generate the client secret (key) values.</span></span> 

![Se connecter à la page du principal de service](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="d4f3f-149">Lorsque le panneau **Principal de service** s’ouvre, la première application Azure AD qui répond aux critères suivants est sélectionnée :</span><span class="sxs-lookup"><span data-stu-id="d4f3f-149">When the **Service Principal** blade opens, the first Azure AD application that meets the following criteria is selected:</span></span>

- <span data-ttu-id="d4f3f-150">Il s’agit d’une application Azure AD inscrite.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="d4f3f-151">Elle dispose d’autorisations Access Control de type Collaborateur ou Propriétaire sur le compte.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-151">It has Contributor or Owner Role-Based Access Control permissions on the account.</span></span>

<span data-ttu-id="d4f3f-152">Une fois que vous avez créé ou sélectionné une application Azure AD, vous pouvez créer et copier une clé secrète client (clé) ainsi que l’ID client (ID d’application).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and the client ID (Application ID).</span></span> <span data-ttu-id="d4f3f-153">La clé secrète client et l’ID client sont requis pour l’obtention du jeton d’accès dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-153">The client secret and client ID are required to get the access token in this scenario.</span></span>

<span data-ttu-id="d4f3f-154">Si vous n’êtes pas autorisé à créer des applications Azure AD dans votre domaine, les contrôles d’application Azure AD du panneau ne sont pas affichés, et un message d’avertissement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-154">If you don't have permissions to create Azure AD apps in your domain, the Azure AD app controls of the blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="d4f3f-155">Si vous vous connectez à l’API Media Services à l’aide du Kit logiciel de développement (SDK) Media Services .NET, consultez [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md) (Utiliser l’authentification Azure AD pour accéder à l’API Azure Media Services avec .NET).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-155">If you connect to the Media Services API by using the Media Services .NET SDK, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="d4f3f-156">Si vous n’utilisez pas le Kit de développement logiciel (SDK) du client Media Services .NET, vous devez créer manuellement une demande de jeton Azure AD en utilisant les paramètres décrits précédemment.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-156">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request using the parameters discussed earlier.</span></span> <span data-ttu-id="d4f3f-157">Pour plus d’informations, consultez [Bibliothèques d’authentification d’Azure Active Directory](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-157">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-the-client-id-and-client-secret"></a><span data-ttu-id="d4f3f-158">Obtenir l’ID client et la clé secrète client</span><span class="sxs-lookup"><span data-stu-id="d4f3f-158">Get the client ID and client secret</span></span>

<span data-ttu-id="d4f3f-159">Après avoir sélectionné une application Azure AD existante ou choisi l’option permettant d’en créer une, les boutons suivants s’affichent :</span><span class="sxs-lookup"><span data-stu-id="d4f3f-159">After you select an existing Azure AD app or select the option to create a new one, the following buttons appear:</span></span>

![Bouton Gérer les autorisations et bouton Gérer l’application](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="d4f3f-161">Pour ouvrir le panneau de l’application Azure AD, cliquez sur **Gérer l’application**.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-161">To open the Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="d4f3f-162">Dans le panneau **Gérer l’application**, vous pouvez obtenir l’ID client de l’application (ID d’application).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-162">On the **Manage application** blade, you can get the app's client ID (Application ID).</span></span> <span data-ttu-id="d4f3f-163">Pour générer une clé secrète client (clé), sélectionnez **Clés**.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-163">To generate a client secret (key), select **Keys**.</span></span>

![Option Clés du panneau Gérer l’application](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-the-application"></a><span data-ttu-id="d4f3f-165">Gérer les autorisations et l’application</span><span class="sxs-lookup"><span data-stu-id="d4f3f-165">Manage permissions and the application</span></span>

<span data-ttu-id="d4f3f-166">Après avoir sélectionné l’application Azure AD, vous pouvez gérer l’application et les autorisations.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-166">After you select the Azure AD application, you can manage the application and permissions.</span></span> <span data-ttu-id="d4f3f-167">Pour configurer votre application Azure AD afin d’accéder à d’autres applications, cliquez sur **Gérer les autorisations**.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-167">To set up your Azure AD application to access other applications, click **Manage permissions**.</span></span> <span data-ttu-id="d4f3f-168">Pour les tâches de gestion, telles que la modification des clés et des URL de réponse, ou pour modifier le manifeste de l’application, cliquez sur **Gérer l’application**.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-168">For management tasks, such as changing keys and reply URLs, or to edit the application’s manifest, click **Manage application**.</span></span>

### <a name="edit-the-apps-settings-or-manifest"></a><span data-ttu-id="d4f3f-169">Modifier les paramètres ou le manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="d4f3f-169">Edit the app's settings or manifest</span></span>

<span data-ttu-id="d4f3f-170">Pour modifier les paramètres ou le manifeste de l’application, cliquez sur **Gérer l’application**.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-170">To edit the app's settings or manifest, click **Manage application**.</span></span>

![Page Gérer l’application](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="d4f3f-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4f3f-172">Next steps</span></span>

<span data-ttu-id="d4f3f-173">Commencez le [chargement de fichiers sur votre compte](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="d4f3f-173">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
