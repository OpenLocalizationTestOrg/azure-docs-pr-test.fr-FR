---
title: "aaaUse tooaccess d’authentification Azure AD API Azure Media Services avec .NET | Documents Microsoft"
description: "Cette rubrique montre comment toouse tooaccess d’authentification Azure Active Directory (Azure AD) Azure Media Services (AMS) des API avec .NET."
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
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a><span data-ttu-id="1f675-103">Utiliser Azure AD authentication tooaccess API Azure Media Services avec .NET</span><span class="sxs-lookup"><span data-stu-id="1f675-103">Use Azure AD authentication tooaccess Azure Media Services API with .NET</span></span>

<span data-ttu-id="1f675-104">À partir de windowsazure.mediaservices 4.0.0.4, Azure Media Services prend en charge l’authentification basée sur Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f675-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="1f675-105">Cette rubrique vous montre comment toouse tooaccess d’authentification Azure AD API Azure Media Services avec Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="1f675-105">This topic shows you how toouse Azure AD  authentication tooaccess Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f675-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1f675-106">Prerequisites</span></span>

- <span data-ttu-id="1f675-107">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1f675-107">An Azure account.</span></span> <span data-ttu-id="1f675-108">Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f675-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="1f675-109">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="1f675-109">A Media Services account.</span></span> <span data-ttu-id="1f675-110">Pour plus d’informations, consultez [créer un compte Azure Media Services à l’aide de hello Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="1f675-110">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="1f675-111">Hello dernières [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span><span class="sxs-lookup"><span data-stu-id="1f675-111">hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="1f675-112">Connaissance de la rubrique de hello [l’accès à des API Azure Media Services avec une vue d’ensemble de l’authentification AAD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="1f675-112">Familiarity with hello topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="1f675-113">Lorsque vous utilisez l’authentification Azure AD avec Azure Media Services, vous pouvez vous authentifier de deux manières :</span><span class="sxs-lookup"><span data-stu-id="1f675-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="1f675-114">**Authentification utilisateur** authentifie un utilisateur de hello application toointeract avec des ressources Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="1f675-114">**User authentication** authenticates a person who is using hello app toointeract with Azure Media Services resources.</span></span> <span data-ttu-id="1f675-115">les applications interactives Hello doivent tout d’abord utilisateur hello pour les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="1f675-115">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="1f675-116">Un exemple est une application de console de gestion qui est utilisée par toomonitor les utilisateurs autorisés travaux d’encodage ou de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="1f675-116">An example is a management console app that's used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="1f675-117">L’**authentification de principal de service** authentifie un service.</span><span class="sxs-lookup"><span data-stu-id="1f675-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="1f675-118">Les applications qui utilisent généralement cette méthode d’authentification sont des applications qui exécutent des services démon, des services de niveau intermédiaire ou des travaux planifiés (par exemple, applications web, applications de fonction, applications logiques, API ou microservices).</span><span class="sxs-lookup"><span data-stu-id="1f675-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="1f675-119">Azure Media Services prend actuellement en charge un modèle d’authentification Azure Access Control Service.</span><span class="sxs-lookup"><span data-stu-id="1f675-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="1f675-120">Toutefois, l’autorisation de contrôle d’accès est en cours toobe déconseillée sur le 1 juin 2018.</span><span class="sxs-lookup"><span data-stu-id="1f675-120">However, Access Control authorization is going toobe deprecated on June 1, 2018.</span></span> <span data-ttu-id="1f675-121">Nous vous recommandons de migrer modèle d’authentification Azure Active Directory tooan dès que possible.</span><span class="sxs-lookup"><span data-stu-id="1f675-121">We recommend that you migrate tooan Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="1f675-122">Obtenir un jeton d’accès Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f675-122">Get an Azure AD access token</span></span>

<span data-ttu-id="1f675-123">tooconnect toohello API Azure Media Services avec l’authentification Azure AD, application de client hello doit toorequest un jeton d’accès Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f675-123">tooconnect toohello Azure Media Services API with Azure AD authentication, hello client app needs toorequest an Azure AD access token.</span></span> <span data-ttu-id="1f675-124">Lorsque vous utilisez le SDK, nombreux hello plus d’informations sur comment tooacquire un jeton d’accès Azure AD sont encapsulées et simplifiée pour vous dans hello du client de Media Services .NET hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) et [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span><span class="sxs-lookup"><span data-stu-id="1f675-124">When you use hello Media Services .NET client SDK, many of hello details about how tooacquire an Azure AD access token are wrapped and simplified for you in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="1f675-125">Par exemple, vous n’avez pas besoin tooprovide hello Azure AD autorité, URI de ressource de Media Services ou natif détails de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f675-125">For example, you don't need tooprovide hello Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="1f675-126">Il s’agit des valeurs connues qui sont déjà configurés par hello classe de fournisseur de jetons d’accès Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f675-126">These are well-known values that are already configured by hello Azure AD access token provider class.</span></span> 

<span data-ttu-id="1f675-127">Si vous n’utilisez pas d’Azure Media Services .NET SDK, nous vous recommandons d’utiliser hello [bibliothèque d’authentification Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="1f675-127">If you are not using Azure Media Service .NET SDK, we recommend that you use hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="1f675-128">les valeurs de tooget des paramètres de hello que vous avez besoin de toouse avec la bibliothèque d’authentification Azure AD, consultez [utiliser les paramètres d’authentification tooaccess portail Azure AD Azure hello](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="1f675-128">tooget values for hello parameters that you need toouse with Azure AD Authentication Library, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="1f675-129">Vous avez également option hello de remplacer l’implémentation par défaut de hello Hello **AzureAdTokenProvider** avec votre propre implémentation.</span><span class="sxs-lookup"><span data-stu-id="1f675-129">You also have hello option of replacing hello default implementation of hello **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="1f675-130">Installer et configurer le kit de développement logiciel (SDK) Azure Media Services pour .NET</span><span class="sxs-lookup"><span data-stu-id="1f675-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="1f675-131">authentification toouse Azure AD avec hello Media Services .NET SDK, vous devez toohave hello dernières [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span><span class="sxs-lookup"><span data-stu-id="1f675-131">toouse Azure AD authentication with hello Media Services .NET SDK, you need toohave hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="1f675-132">En outre, ajoutez une référence toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span><span class="sxs-lookup"><span data-stu-id="1f675-132">Also, add a reference toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="1f675-133">Si vous utilisez une application existante, inclure hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span><span class="sxs-lookup"><span data-stu-id="1f675-133">If you are using an existing app, include hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="1f675-134">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1f675-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="1f675-135">Hello d’utilisation [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall de package NuGet **Azure Media Services .NET SDK**.</span><span class="sxs-lookup"><span data-stu-id="1f675-135">Use hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package tooinstall **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="1f675-136">tooadd des références à l’aide de NuGet, prendre hello comme suit : dans **l’Explorateur de solutions**, cliquez sur le nom de projet hello, puis sélectionnez **gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1f675-136">tooadd references by using NuGet, take hello following steps: in **Solution Explorer**, right-click hello project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="1f675-137">Ensuite, recherchez **windowsazure.mediaservices** et cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="1f675-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="1f675-138">-ou-</span><span class="sxs-lookup"><span data-stu-id="1f675-138">-or-</span></span>

    <span data-ttu-id="1f675-139">Exécution hello après une commande dans **Package Manager Console** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1f675-139">Run hello following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="1f675-140">Ajouter **à l’aide de** code source de tooyour.</span><span class="sxs-lookup"><span data-stu-id="1f675-140">Add **using** tooyour source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="1f675-141">Utiliser une authentification utilisateur</span><span class="sxs-lookup"><span data-stu-id="1f675-141">Use user authentication</span></span>

<span data-ttu-id="1f675-142">tooconnect toohello API de Service de média Azure avec l’option d’authentification utilisateur hello, hello client application doit toorequest hello d’un jeton d’Azure AD à l’aide de paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="1f675-142">tooconnect toohello Azure Media Service API with hello user authentication option, hello client app needs toorequest an Azure AD token by using hello following parameters:</span></span>  

- <span data-ttu-id="1f675-143">Point de terminaison de locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f675-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="1f675-144">les informations du locataire Hello peuvent être récupérées de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1f675-144">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="1f675-145">Pointez sur hello utilisateur connecté dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="1f675-145">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="1f675-146">URI de ressource Media Services.</span><span class="sxs-lookup"><span data-stu-id="1f675-146">Media Services resource URI.</span></span>
- <span data-ttu-id="1f675-147">ID client d’application Media Services (natif).</span><span class="sxs-lookup"><span data-stu-id="1f675-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="1f675-148">URI de redirection d’application Media Services (natif).</span><span class="sxs-lookup"><span data-stu-id="1f675-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="1f675-149">les valeurs Hello pour ces paramètres sont accessibles dans **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="1f675-149">hello values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="1f675-150">Hello **AzureEnvironments.AzureCloudEnvironment** constante est une application d’assistance dans hello .NET SDK tooget hello droit variable paramètres d’environnement pour un centre de données Azure publique.</span><span class="sxs-lookup"><span data-stu-id="1f675-150">hello **AzureEnvironments.AzureCloudEnvironment** constant is a helper in hello .NET SDK tooget hello right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="1f675-151">Il contient des paramètres d’environnement prédéfinis pour accéder aux Services de support dans des centres de données publics hello uniquement.</span><span class="sxs-lookup"><span data-stu-id="1f675-151">It contains pre-defined environment settings for accessing Media Services in hello public data centers only.</span></span> <span data-ttu-id="1f675-152">Pour les régions de cloud souverain ou gouvernemental, vous pouvez utiliser **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** ou **AzureGermanCloudEnvironment** respectivement.</span><span class="sxs-lookup"><span data-stu-id="1f675-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="1f675-153">Hello, exemple de code suivant crée un jeton :</span><span class="sxs-lookup"><span data-stu-id="1f675-153">hello following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="1f675-154">toostart programmation de Media Services, vous devez toocreate une **CloudMediaContext** instance qui représente le contexte de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="1f675-154">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="1f675-155">Hello **CloudMediaContext** contient des collections de tooimportant de références, y compris les travaux actifs, fichiers, les stratégies d’accès et les localisateurs.</span><span class="sxs-lookup"><span data-stu-id="1f675-155">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="1f675-156">Vous devez également toopass hello **ressource URI des Services REST de Media** toohello **CloudMediaContext** constructeur.</span><span class="sxs-lookup"><span data-stu-id="1f675-156">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="1f675-157">URI de la ressource tooget hello pour les Services REST de Media, connectez-vous toohello portail Azure, sélectionnez votre compte Azure Media Services, sélectionnez **l’accès aux API**, puis sélectionnez **connecter tooAzure Media Services avec l’utilisateur authentification**.</span><span class="sxs-lookup"><span data-stu-id="1f675-157">tooget hello resource URI for Media REST Services, sign in toohello Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect tooAzure Media Services with user authentication**.</span></span> 

<span data-ttu-id="1f675-158">Hello exemple de code suivant crée un **CloudMediaContext** instance :</span><span class="sxs-lookup"><span data-stu-id="1f675-158">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="1f675-159">Bonjour à l’exemple suivant montre comment toocreate hello contexte de jeton et hello Azure AD :</span><span class="sxs-lookup"><span data-stu-id="1f675-159">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

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
><span data-ttu-id="1f675-160">Si vous obtenez une exception indiquant que « serveur hello a renvoyé une erreur : non autorisé de (401), « voir hello [le contrôle d’accès](media-services-use-aad-auth-to-access-ams-api.md#access-control) section de l’accès à des API Azure Media Services, vue d’ensemble de l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f675-160">If you get an exception that says "hello remote server returned an error: (401) Unauthorized," see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="1f675-161">Utiliser une authentification de principal de service</span><span class="sxs-lookup"><span data-stu-id="1f675-161">Use service principal authentication</span></span>
    
<span data-ttu-id="1f675-162">tooconnect toohello API Azure Media Services avec l’option principal du service hello, votre application de couche intermédiaire (API web ou une application web) doit toorequests un jeton Azure AD avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="1f675-162">tooconnect toohello Azure Media Services API with hello service principal option, your middle-tier app (web API or web application) needs toorequests an Azure AD token with hello following parameters:</span></span>  

- <span data-ttu-id="1f675-163">Point de terminaison de locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f675-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="1f675-164">les informations du locataire Hello peuvent être récupérées de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1f675-164">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="1f675-165">Pointez sur hello utilisateur connecté dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="1f675-165">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="1f675-166">URI de ressource Media Services.</span><span class="sxs-lookup"><span data-stu-id="1f675-166">Media Services resource URI.</span></span>
- <span data-ttu-id="1f675-167">Valeurs de l’application Azure AD : hello **ID Client** et **clé secrète Client**.</span><span class="sxs-lookup"><span data-stu-id="1f675-167">Azure AD application values: hello **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="1f675-168">Hello des valeurs pour hello **ID Client** et **clé secrète Client** paramètres peuvent être trouvés dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1f675-168">hello values for hello **Client ID** and **Client secret** parameters can be found in hello Azure portal.</span></span> <span data-ttu-id="1f675-169">Pour plus d’informations, consultez [prise en main d’Azure AD à l’aide de l’authentification hello Azure portal](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="1f675-169">For more information, see [Getting started with Azure AD authentication using hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="1f675-170">Hello exemple de code suivant crée un jeton à l’aide de hello **AzureAdTokenCredentials** constructeur qui accepte **AzureAdClientSymmetricKey** en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="1f675-170">hello following code example creates a token by using hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="1f675-171">Vous pouvez également spécifier hello **AzureAdTokenCredentials** constructeur qui accepte **AzureAdClientCertificate** en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="1f675-171">You can also specify hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="1f675-172">Pour obtenir des instructions sur la façon toocreate et configurer un certificat dans un formulaire qui peut être utilisé par Azure AD, consultez [authentification tooAzure AD dans les applications avec des certificats - étapes de configuration manuelles démon](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span><span class="sxs-lookup"><span data-stu-id="1f675-172">For instructions about how toocreate and configure a certificate in a form that can be used by Azure AD, see [Authenticating tooAzure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="1f675-173">toostart programmation de Media Services, vous devez toocreate une **CloudMediaContext** instance qui représente le contexte de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="1f675-173">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="1f675-174">Vous devez également toopass hello **ressource URI des Services REST de Media** toohello **CloudMediaContext** constructeur.</span><span class="sxs-lookup"><span data-stu-id="1f675-174">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="1f675-175">Vous pouvez obtenir hello **ressource URI des Services REST de Media** comprise hello également le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1f675-175">You can get hello **resource URI for Media REST Services** value from hello Azure portal as well.</span></span>

<span data-ttu-id="1f675-176">Hello exemple de code suivant crée un **CloudMediaContext** instance :</span><span class="sxs-lookup"><span data-stu-id="1f675-176">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="1f675-177">Bonjour à l’exemple suivant montre comment toocreate hello contexte de jeton et hello Azure AD :</span><span class="sxs-lookup"><span data-stu-id="1f675-177">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1f675-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f675-178">Next steps</span></span>

<span data-ttu-id="1f675-179">Prise en main [téléchargement de fichiers tooyour compte](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="1f675-179">Get started with [uploading files tooyour account](media-services-dotnet-upload-files.md).</span></span>
