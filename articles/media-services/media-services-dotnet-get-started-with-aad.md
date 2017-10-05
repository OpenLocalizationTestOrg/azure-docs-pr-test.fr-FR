---
title: "Utiliser l’authentification Azure AD pour accéder à l’API Azure Media Services avec .NET | Microsoft Docs"
description: "Cette rubrique aborde l’utilisation de l’authentification Azure Active Directory (Azure AD) en vue d’accéder à l’API Azure Media Services (AMS) avec .NET."
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
ms.openlocfilehash: a9355200a05a3aa1b494b76977d38ddc42bfe179
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-ad-authentication-to-access-azure-media-services-api-with-net"></a><span data-ttu-id="c12c4-103">Utiliser l’authentification Azure AD pour accéder à l’API Azure Media Services avec .NET</span><span class="sxs-lookup"><span data-stu-id="c12c4-103">Use Azure AD authentication to access Azure Media Services API with .NET</span></span>

<span data-ttu-id="c12c4-104">À partir de windowsazure.mediaservices 4.0.0.4, Azure Media Services prend en charge l’authentification basée sur Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c12c4-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c12c4-105">Cette rubrique aborde l’utilisation de l’authentification Azure AD en vue d’accéder à l’API Azure Media Services avec Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="c12c4-105">This topic shows you how to use Azure AD  authentication to access Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c12c4-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c12c4-106">Prerequisites</span></span>

- <span data-ttu-id="c12c4-107">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="c12c4-107">An Azure account.</span></span> <span data-ttu-id="c12c4-108">Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c12c4-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="c12c4-109">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="c12c4-109">A Media Services account.</span></span> <span data-ttu-id="c12c4-110">Pour plus d’informations, voir [Création d’un compte Azure Media Services à l’aide du portail Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="c12c4-110">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="c12c4-111">La dernière version du package [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices).</span><span class="sxs-lookup"><span data-stu-id="c12c4-111">The latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="c12c4-112">Veillez à consulter [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md) (Vue d’ensemble de l’accès à l’API Azure Media Services avec l’authentification Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c12c4-112">Familiarity with the topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="c12c4-113">Lorsque vous utilisez l’authentification Azure AD avec Azure Media Services, vous pouvez vous authentifier de deux manières :</span><span class="sxs-lookup"><span data-stu-id="c12c4-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="c12c4-114">L’**authentification utilisateur** authentifie une personne qui utilise l’application pour interagir avec les ressources Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="c12c4-114">**User authentication** authenticates a person who is using the app to interact with Azure Media Services resources.</span></span> <span data-ttu-id="c12c4-115">L’application interactive invite tout d’abord l’utilisateur à entrer ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="c12c4-115">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="c12c4-116">Par exemple, une application de console de gestion peut être utilisée par les utilisateurs autorisés pour contrôler les travaux d’encodage ou de streaming en direct.</span><span class="sxs-lookup"><span data-stu-id="c12c4-116">An example is a management console app that's used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="c12c4-117">L’**authentification de principal de service** authentifie un service.</span><span class="sxs-lookup"><span data-stu-id="c12c4-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="c12c4-118">Les applications qui utilisent généralement cette méthode d’authentification sont des applications qui exécutent des services démon, des services de niveau intermédiaire ou des travaux planifiés (par exemple, applications web, applications de fonction, applications logiques, API ou microservices).</span><span class="sxs-lookup"><span data-stu-id="c12c4-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c12c4-119">Azure Media Services prend actuellement en charge un modèle d’authentification Azure Access Control Service.</span><span class="sxs-lookup"><span data-stu-id="c12c4-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="c12c4-120">Toutefois, l’autorisation Access Control sera déconseillée à compter du 1er juin 2018.</span><span class="sxs-lookup"><span data-stu-id="c12c4-120">However, Access Control authorization is going to be deprecated on June 1, 2018.</span></span> <span data-ttu-id="c12c4-121">Nous vous recommandons de migrer vers un modèle d’authentification Azure Active Directory dès que possible.</span><span class="sxs-lookup"><span data-stu-id="c12c4-121">We recommend that you migrate to an Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="c12c4-122">Obtenir un jeton d’accès Azure AD</span><span class="sxs-lookup"><span data-stu-id="c12c4-122">Get an Azure AD access token</span></span>

<span data-ttu-id="c12c4-123">Pour que vous puissiez vous connecter à l’API Azure Media Services avec l’authentification Azure AD, l’application cliente doit demander un jeton d’accès Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c12c4-123">To connect to the Azure Media Services API with Azure AD authentication, the client app needs to request an Azure AD access token.</span></span> <span data-ttu-id="c12c4-124">Lorsque vous utilisez le kit de développement logiciel (SDK) client Media Services pour .NET, beaucoup de détails sur la façon d’acquérir un jeton d’accès Azure AD sont encapsulées et simplifiés dans les classes [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) et [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs).</span><span class="sxs-lookup"><span data-stu-id="c12c4-124">When you use the Media Services .NET client SDK, many of the details about how to acquire an Azure AD access token are wrapped and simplified for you in the [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="c12c4-125">Par exemple, vous n’avez pas besoin d’indiquer l’autorité Azure AD, l’URI de ressource Media Services, ni les détails de l’application Azure AD native.</span><span class="sxs-lookup"><span data-stu-id="c12c4-125">For example, you don't need to provide the Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="c12c4-126">Il s’agit de valeurs connues qui sont déjà configurées par la classe de fournisseur de jetons d’accès Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c12c4-126">These are well-known values that are already configured by the Azure AD access token provider class.</span></span> 

<span data-ttu-id="c12c4-127">Si vous n’utilisez pas le kit de développement logiciel (SDK) Azure Media Services pour .NET, nous vous recommandons d’utiliser la [bibliothèque d’authentification Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="c12c4-127">If you are not using Azure Media Service .NET SDK, we recommend that you use the [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="c12c4-128">Pour obtenir les valeurs des paramètres à utiliser avec la bibliothèque d’authentification Azure AD, voir [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md) (Utiliser le portail Azure pour accéder aux paramètres d’authentification Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c12c4-128">To get values for the parameters that you need to use with Azure AD Authentication Library, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="c12c4-129">Vous avez également la possibilité de remplacer l’implémentation par défaut de **AzureAdTokenProvider** par votre propre implémentation.</span><span class="sxs-lookup"><span data-stu-id="c12c4-129">You also have the option of replacing the default implementation of the **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="c12c4-130">Installer et configurer le kit de développement logiciel (SDK) Azure Media Services pour .NET</span><span class="sxs-lookup"><span data-stu-id="c12c4-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="c12c4-131">Pour utiliser l’authentification Azure AD avec le kit de développement logiciel (SDK) Media Services pour .NET, vous devez disposer de la dernière version du package [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices).</span><span class="sxs-lookup"><span data-stu-id="c12c4-131">To use Azure AD authentication with the Media Services .NET SDK, you need to have the latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="c12c4-132">En outre, ajoutez une référence à l’assembly **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="c12c4-132">Also, add a reference to the **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="c12c4-133">Si vous utilisez une application existante, incluez l’assembly **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll**.</span><span class="sxs-lookup"><span data-stu-id="c12c4-133">If you are using an existing app, include the **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="c12c4-134">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c12c4-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="c12c4-135">Utilisez le package NuGet [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) pour installer le **kit de développement logiciel (SDK) Azure Media Services pour .NET**.</span><span class="sxs-lookup"><span data-stu-id="c12c4-135">Use the [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package to install **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="c12c4-136">Pour ajouter des références à l’aide de NuGet, procédez comme suit : dans l’**Explorateur de solutions**, cliquez avec le bouton droit de la souris sur le nom du projet, puis sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c12c4-136">To add references by using NuGet, take the following steps: in **Solution Explorer**, right-click the project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="c12c4-137">Ensuite, recherchez **windowsazure.mediaservices** et cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="c12c4-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="c12c4-138">-ou-</span><span class="sxs-lookup"><span data-stu-id="c12c4-138">-or-</span></span>

    <span data-ttu-id="c12c4-139">Dans la **Console du Gestionnaire de package** de Visual Studio, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="c12c4-139">Run the following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="c12c4-140">Ajoutez **using** à votre code source.</span><span class="sxs-lookup"><span data-stu-id="c12c4-140">Add **using** to your source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="c12c4-141">Utiliser une authentification utilisateur</span><span class="sxs-lookup"><span data-stu-id="c12c4-141">Use user authentication</span></span>

<span data-ttu-id="c12c4-142">Pour vous connecter à l’API Azure Media Services avec l’option d’authentification utilisateur, l’application cliente doit demander un jeton Azure AD à l’aide des paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="c12c4-142">To connect to the Azure Media Service API with the user authentication option, the client app needs to request an Azure AD token by using the following parameters:</span></span>  

- <span data-ttu-id="c12c4-143">Point de terminaison de locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c12c4-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="c12c4-144">Les informations relatives au locataire peuvent être récupérées à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c12c4-144">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="c12c4-145">Pointez sur l’utilisateur connecté dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="c12c4-145">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="c12c4-146">URI de ressource Media Services.</span><span class="sxs-lookup"><span data-stu-id="c12c4-146">Media Services resource URI.</span></span>
- <span data-ttu-id="c12c4-147">ID client d’application Media Services (natif).</span><span class="sxs-lookup"><span data-stu-id="c12c4-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="c12c4-148">URI de redirection d’application Media Services (natif).</span><span class="sxs-lookup"><span data-stu-id="c12c4-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="c12c4-149">Les valeurs de ces paramètres sont accessibles dans **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="c12c4-149">The values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="c12c4-150">La constante **AzureEnvironments.AzureCloudEnvironment** est une application auxiliaire du kit de développement logiciel (SDK) pour .NET qui permet d’obtenir les paramètres de variable d’environnement corrects pour un centre de données Azure public.</span><span class="sxs-lookup"><span data-stu-id="c12c4-150">The **AzureEnvironments.AzureCloudEnvironment** constant is a helper in the .NET SDK to get the right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="c12c4-151">Elle contient des paramètres d’environnement prédéfinis pour accéder à Media Services dans les centres de données publics uniquement.</span><span class="sxs-lookup"><span data-stu-id="c12c4-151">It contains pre-defined environment settings for accessing Media Services in the public data centers only.</span></span> <span data-ttu-id="c12c4-152">Pour les régions de cloud souverain ou gouvernemental, vous pouvez utiliser **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** ou **AzureGermanCloudEnvironment** respectivement.</span><span class="sxs-lookup"><span data-stu-id="c12c4-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="c12c4-153">L’exemple de code suivant permet de créer un jeton :</span><span class="sxs-lookup"><span data-stu-id="c12c4-153">The following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="c12c4-154">Pour commencer à programmer sur Media Services, vous devez créer une instance **CloudMediaContext** qui représente le contexte du serveur.</span><span class="sxs-lookup"><span data-stu-id="c12c4-154">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="c12c4-155">**CloudMediaContext** comprend des références à des collections importantes comme les travaux, les éléments multimédias, les fichiers, les stratégies d'accès et les localisateurs.</span><span class="sxs-lookup"><span data-stu-id="c12c4-155">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="c12c4-156">Vous devez également transmettre l’**URI de ressource des services REST Media** au constructeur **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="c12c4-156">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="c12c4-157">Pour obtenir l’URI de ressource des services REST Media, connectez-vous au portail Azure, indiquez votre compte Azure Media Services, sélectionnez **Accès API**, puis choisissez l’option **Se connecter à l'API Azure Media Services avec l'authentification utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c12c4-157">To get the resource URI for Media REST Services, sign in to the Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect to Azure Media Services with user authentication**.</span></span> 

<span data-ttu-id="c12c4-158">L’exemple de code suivant permet de créer une instance **CloudMediaContext** :</span><span class="sxs-lookup"><span data-stu-id="c12c4-158">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="c12c4-159">L’exemple suivant montre comment créer le jeton Azure AD et le contexte :</span><span class="sxs-lookup"><span data-stu-id="c12c4-159">The following example shows how to create the Azure AD token and the context:</span></span>

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
><span data-ttu-id="c12c4-160">Si vous obtenez une exception indiquant que le serveur distant a renvoyé une erreur 401 « Non autorisé », consultez la section sur le [contrôle d’accès](media-services-use-aad-auth-to-access-ams-api.md#access-control) dans la vue d’ensemble de l’accès à l’API Azure Media Services avec l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c12c4-160">If you get an exception that says "The remote server returned an error: (401) Unauthorized," see the [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="c12c4-161">Utiliser une authentification de principal de service</span><span class="sxs-lookup"><span data-stu-id="c12c4-161">Use service principal authentication</span></span>
    
<span data-ttu-id="c12c4-162">Pour vous connecter à l’API Azure Media Services à l’aide de l’option de principal de service, votre application de niveau intermédiaire (API web ou application web) doit demander un jeton Azure AD avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="c12c4-162">To connect to the Azure Media Services API with the service principal option, your middle-tier app (web API or web application) needs to requests an Azure AD token with the following parameters:</span></span>  

- <span data-ttu-id="c12c4-163">Point de terminaison de locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c12c4-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="c12c4-164">Les informations relatives au locataire peuvent être récupérées à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c12c4-164">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="c12c4-165">Pointez sur l’utilisateur connecté dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="c12c4-165">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="c12c4-166">URI de ressource Media Services.</span><span class="sxs-lookup"><span data-stu-id="c12c4-166">Media Services resource URI.</span></span>
- <span data-ttu-id="c12c4-167">Valeurs de l’application Azure AD : **ID client** et **clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="c12c4-167">Azure AD application values: the **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="c12c4-168">Les valeurs pour les paramètres d’**ID client** et de **clé secrète client** se trouvent dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c12c4-168">The values for the **Client ID** and **Client secret** parameters can be found in the Azure portal.</span></span> <span data-ttu-id="c12c4-169">Pour plus d’informations, voir [Prise en main de l’authentification Azure AD à l’aide du portail Azure](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="c12c4-169">For more information, see [Getting started with Azure AD authentication using the Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="c12c4-170">L’exemple de code suivant permet de créer un jeton à l’aide du constructeur **AzureAdTokenCredentials**, qui accepte **AzureAdClientSymmetricKey** en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="c12c4-170">The following code example creates a token by using the **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="c12c4-171">Vous pouvez également spécifier le constructeur **AzureAdTokenCredentials**, qui accepte **AzureAdClientCertificate** en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="c12c4-171">You can also specify the **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="c12c4-172">Pour obtenir des instructions sur la création et la configuration d’un certificat dans un formulaire qui peut être utilisé par Azure AD, consultez les étapes de configuration manuelle dans [Authenticating to Azure AD in daemon apps with certificates](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md) (Authentification auprès d’Azure AD dans des applications démons avec des certificats).</span><span class="sxs-lookup"><span data-stu-id="c12c4-172">For instructions about how to create and configure a certificate in a form that can be used by Azure AD, see [Authenticating to Azure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="c12c4-173">Pour commencer à programmer sur Media Services, vous devez créer une instance **CloudMediaContext** qui représente le contexte du serveur.</span><span class="sxs-lookup"><span data-stu-id="c12c4-173">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="c12c4-174">Vous devez également transmettre l’**URI de ressource des services REST Media** au constructeur **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="c12c4-174">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="c12c4-175">Vous pouvez également obtenir la valeur de l’**URI de ressource des services REST Media** à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c12c4-175">You can get the **resource URI for Media REST Services** value from the Azure portal as well.</span></span>

<span data-ttu-id="c12c4-176">L’exemple de code suivant permet de créer une instance **CloudMediaContext** :</span><span class="sxs-lookup"><span data-stu-id="c12c4-176">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="c12c4-177">L’exemple suivant montre comment créer le jeton Azure AD et le contexte :</span><span class="sxs-lookup"><span data-stu-id="c12c4-177">The following example shows how to create the Azure AD token and the context:</span></span>

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a><span data-ttu-id="c12c4-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c12c4-178">Next steps</span></span>

<span data-ttu-id="c12c4-179">Commencez le [chargement de fichiers sur votre compte](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="c12c4-179">Get started with [uploading files to your account](media-services-dotnet-upload-files.md).</span></span>
