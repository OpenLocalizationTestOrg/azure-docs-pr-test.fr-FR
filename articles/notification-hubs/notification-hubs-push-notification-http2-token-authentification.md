---
title: "Authentification basée sur un jeton (HTTP/2) pour APNS dans Azure Notification Hubs | Microsoft Docs"
description: Cette rubrique explique comment tirer parti de la nouvelle authentification de jeton pour APNS
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 5a21bcd9f12fc3f96b17a556ba15526c35ababe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="c7820-103">Authentification basée sur un jeton (HTTP/2) pour APNS</span><span class="sxs-lookup"><span data-stu-id="c7820-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="c7820-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c7820-104">Overview</span></span>
<span data-ttu-id="c7820-105">Cet article explique comment utiliser le nouveau protocole APNS HTTP/2 avec une authentification basée sur un jeton.</span><span class="sxs-lookup"><span data-stu-id="c7820-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="c7820-106">Les principaux avantages de l’utilisation du nouveau protocole sont notamment :</span><span class="sxs-lookup"><span data-stu-id="c7820-106">The key benefits of using the new protocol include:</span></span>
-   <span data-ttu-id="c7820-107">La génération de jetons est relativement simple (par rapport aux certificats)</span><span class="sxs-lookup"><span data-stu-id="c7820-107">Token generation is relatively hassle free (compared to certificates)</span></span>
-   <span data-ttu-id="c7820-108">Plus de date d’expiration : vous contrôlez vos jetons d’authentification et leur révocation</span><span class="sxs-lookup"><span data-stu-id="c7820-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="c7820-109">Les charges utiles peuvent maintenant atteindre 4 Ko</span><span class="sxs-lookup"><span data-stu-id="c7820-109">Payloads can now be up to 4 KB</span></span>
- <span data-ttu-id="c7820-110">Les commentaires sont synchrones</span><span class="sxs-lookup"><span data-stu-id="c7820-110">Synchronous feedback</span></span>
-   <span data-ttu-id="c7820-111">Vous utilisez le dernier protocole d’Apple : les certificats utilisent toujours le protocole binaire, qui est marqué pour dépréciation</span><span class="sxs-lookup"><span data-stu-id="c7820-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="c7820-112">L’utilisation de ce nouveau mécanisme peut être lancée en deux étapes et en quelques minutes :</span><span class="sxs-lookup"><span data-stu-id="c7820-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="c7820-113">Obtenez les informations nécessaires auprès du portail du compte de développeur Apple</span><span class="sxs-lookup"><span data-stu-id="c7820-113">Obtain the necessary information from the Apple Developer Account portal</span></span>
2.  <span data-ttu-id="c7820-114">Configurez votre hub de notification avec les nouvelles informations</span><span class="sxs-lookup"><span data-stu-id="c7820-114">Configure your notification hub with the new information</span></span>

<span data-ttu-id="c7820-115">Notification Hubs est maintenant entièrement configuré pour utiliser le nouveau système d’authentification avec APNS.</span><span class="sxs-lookup"><span data-stu-id="c7820-115">Notification Hubs is now all set to use the new authentication system with APNS.</span></span> 

<span data-ttu-id="c7820-116">Notez que, si vous n’utilisez plus les informations d’identification de certificat pour APNS :</span><span class="sxs-lookup"><span data-stu-id="c7820-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="c7820-117">les propriétés de jeton remplacent votre certificat dans notre système,</span><span class="sxs-lookup"><span data-stu-id="c7820-117">the token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="c7820-118">mais votre application continue de recevoir des notifications sans interruption.</span><span class="sxs-lookup"><span data-stu-id="c7820-118">but your application continues to receive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="c7820-119">Obtention d’informations d’authentification auprès d’Apple</span><span class="sxs-lookup"><span data-stu-id="c7820-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="c7820-120">Pour activer l’authentification basée sur un jeton, vous devez obtenir les propriétés suivantes auprès de votre compte de développeur Apple :</span><span class="sxs-lookup"><span data-stu-id="c7820-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="c7820-121">Identificateur de clé</span><span class="sxs-lookup"><span data-stu-id="c7820-121">Key Identifier</span></span>
<span data-ttu-id="c7820-122">L’identificateur de clé peut être obtenu à partir de la page « Clés » dans le compte de développeur Apple</span><span class="sxs-lookup"><span data-stu-id="c7820-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="c7820-123">Identificateur de l’application et nom de l’application</span><span class="sxs-lookup"><span data-stu-id="c7820-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="c7820-124">Le nom de l’application est disponible via la page des ID d’application dans le compte de développeur.</span><span class="sxs-lookup"><span data-stu-id="c7820-124">The application name is available via the App IDs page in the Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="c7820-125">L’identificateur de l’application est disponible via la page des détails de l’adhésion dans le compte de développeur.</span><span class="sxs-lookup"><span data-stu-id="c7820-125">The application identifier is available via the membership details page in the Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="c7820-126">Jeton d’authentification</span><span class="sxs-lookup"><span data-stu-id="c7820-126">Authentication token</span></span>
<span data-ttu-id="c7820-127">Le jeton d’authentification peut être téléchargé après avoir généré un jeton pour votre application.</span><span class="sxs-lookup"><span data-stu-id="c7820-127">The authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="c7820-128">Pour plus d’informations sur la façon de générer ce jeton, reportez-vous à la [documentation du développeur Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="c7820-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-to-use-token-based-authentication"></a><span data-ttu-id="c7820-129">Configuration de votre hub de notification pour utiliser l’authentification basée sur un jeton</span><span class="sxs-lookup"><span data-stu-id="c7820-129">Configuring your notification hub to use token-based authentication</span></span>
### <a name="configure-via-the-azure-portal"></a><span data-ttu-id="c7820-130">Configurer via le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c7820-130">Configure via the Azure portal</span></span>
<span data-ttu-id="c7820-131">Pour activer l’authentification basée sur un jeton dans le portail, connectez-vous au portail Azure et accédez au panneau Hub de notification > Services de notification > APNS.</span><span class="sxs-lookup"><span data-stu-id="c7820-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="c7820-132">Il existe une nouvelle propriété : *Mode d’authentification*.</span><span class="sxs-lookup"><span data-stu-id="c7820-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="c7820-133">La sélection de Jeton vous permet de mettre à jour votre hub avec toutes les propriétés de jeton appropriées.</span><span class="sxs-lookup"><span data-stu-id="c7820-133">Selecting Token allows you to update your hub with all the relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="c7820-134">Entrez les propriétés que vous avez récupérées à partir de votre compte de développeur Apple,</span><span class="sxs-lookup"><span data-stu-id="c7820-134">Enter the properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="c7820-135">choisissez votre mode d’application : Production ou Bac à sable (sandbox),</span><span class="sxs-lookup"><span data-stu-id="c7820-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="c7820-136">cliquez sur Enregistrer pour mettre à jour vos informations d’identification APNS.</span><span class="sxs-lookup"><span data-stu-id="c7820-136">click Save to update your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="c7820-137">Configurer via l’API de gestion (REST)</span><span class="sxs-lookup"><span data-stu-id="c7820-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="c7820-138">Vous pouvez utiliser nos [API de gestion](https://msdn.microsoft.com/library/azure/dn495827.aspx) afin de mettre à jour votre hub de notification pour utiliser l’authentification basée sur un jeton.</span><span class="sxs-lookup"><span data-stu-id="c7820-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span></span>
<span data-ttu-id="c7820-139">Selon que l’application que vous configurez est une application de production ou Bac à sable (sandbox), ce qui est indiqué dans votre compte de développeur Apple, utilisez l’un des points de terminaison correspondants :</span><span class="sxs-lookup"><span data-stu-id="c7820-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span></span>

- <span data-ttu-id="c7820-140">Point de terminaison sandbox : [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="c7820-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="c7820-141">Point de terminaison de production : [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="c7820-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7820-142">L’authentification basée sur un jeton nécessite la version d’API **2017-04 ou ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="c7820-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="c7820-143">Voici un exemple d’une demande PUT pour mettre à jour un hub avec l’authentification basée sur un jeton :</span><span class="sxs-lookup"><span data-stu-id="c7820-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span></span>


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-the-net-sdk"></a><span data-ttu-id="c7820-144">Configurer via le Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="c7820-144">Configure via the .NET SDK</span></span>
<span data-ttu-id="c7820-145">Vous pouvez configurer votre hub pour utiliser l’authentification basée sur un jeton à l’aide de notre [dernier Kit SDK client](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="c7820-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="c7820-146">Voici un exemple de code illustrant l’utilisation correcte :</span><span class="sxs-lookup"><span data-stu-id="c7820-146">Here’s a code sample illustrating the correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH TO YOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-to-using-certificate-based-authentication"></a><span data-ttu-id="c7820-147">Rétablissement de l’utilisation de l’authentification basée sur les certificats</span><span class="sxs-lookup"><span data-stu-id="c7820-147">Reverting to using certificate-based authentication</span></span>
<span data-ttu-id="c7820-148">Vous pouvez rétablir à tout moment l’utilisation de l’authentification basée sur les certificats en utilisant l’une des méthodes précédentes et en passant le certificat au lieu des propriétés de jeton.</span><span class="sxs-lookup"><span data-stu-id="c7820-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span></span> <span data-ttu-id="c7820-149">Cette action remplace les informations d’identification précédemment stockées.</span><span class="sxs-lookup"><span data-stu-id="c7820-149">That action overwrites the previously stored credentials.</span></span>
