---
title: "aaaToken-(HTTP/2) l’authentification pour APNS dans Azure Notification Hubs | Documents Microsoft"
description: Cette rubrique explique comment tooleverage hello nouvelle authentification de jeton pour APNS
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
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="57f09-103">Authentification basée sur un jeton (HTTP/2) pour APNS</span><span class="sxs-lookup"><span data-stu-id="57f09-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="57f09-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="57f09-104">Overview</span></span>
<span data-ttu-id="57f09-105">Cet article décrit en détail comment toouse hello nouveau APNS HTTP/2 protocole avec le jeton d’authentification basée sur les.</span><span class="sxs-lookup"><span data-stu-id="57f09-105">This article details how toouse hello new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="57f09-106">Hello des avantages clés de l’utilisation du nouveau protocole de hello :</span><span class="sxs-lookup"><span data-stu-id="57f09-106">hello key benefits of using hello new protocol include:</span></span>
-   <span data-ttu-id="57f09-107">Génération de jeton est relativement vous soucier libre (comparés toocertificates)</span><span class="sxs-lookup"><span data-stu-id="57f09-107">Token generation is relatively hassle free (compared toocertificates)</span></span>
-   <span data-ttu-id="57f09-108">Plus de date d’expiration : vous contrôlez vos jetons d’authentification et leur révocation</span><span class="sxs-lookup"><span data-stu-id="57f09-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="57f09-109">Charges utiles peuvent maintenant être des too4 Ko</span><span class="sxs-lookup"><span data-stu-id="57f09-109">Payloads can now be up too4 KB</span></span>
- <span data-ttu-id="57f09-110">Les commentaires sont synchrones</span><span class="sxs-lookup"><span data-stu-id="57f09-110">Synchronous feedback</span></span>
-   <span data-ttu-id="57f09-111">Vous êtes sur le protocole de dernière d’Apple – certificats utilisent toujours le protocole binaire hello, qui est marquée pour l’abandon</span><span class="sxs-lookup"><span data-stu-id="57f09-111">You’re on Apple’s latest protocol – certificates still use hello binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="57f09-112">L’utilisation de ce nouveau mécanisme peut être lancée en deux étapes et en quelques minutes :</span><span class="sxs-lookup"><span data-stu-id="57f09-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="57f09-113">Obtenir les informations nécessaires hello à partir du portail de compte de développeur Apple hello</span><span class="sxs-lookup"><span data-stu-id="57f09-113">Obtain hello necessary information from hello Apple Developer Account portal</span></span>
2.  <span data-ttu-id="57f09-114">Configurer votre concentrateur de notification avec les nouvelles informations de hello</span><span class="sxs-lookup"><span data-stu-id="57f09-114">Configure your notification hub with hello new information</span></span>

<span data-ttu-id="57f09-115">Concentrateurs de notification est désormais tous ensemble toouse hello nouveau système d’authentification avec APNS.</span><span class="sxs-lookup"><span data-stu-id="57f09-115">Notification Hubs is now all set toouse hello new authentication system with APNS.</span></span> 

<span data-ttu-id="57f09-116">Notez que, si vous n’utilisez plus les informations d’identification de certificat pour APNS :</span><span class="sxs-lookup"><span data-stu-id="57f09-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="57f09-117">Propriétés du jeton Hello remplacement votre certificat dans notre système.</span><span class="sxs-lookup"><span data-stu-id="57f09-117">hello token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="57f09-118">mais votre application continue tooreceive notifications en toute transparence.</span><span class="sxs-lookup"><span data-stu-id="57f09-118">but your application continues tooreceive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="57f09-119">Obtention d’informations d’authentification auprès d’Apple</span><span class="sxs-lookup"><span data-stu-id="57f09-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="57f09-120">l’authentification basée sur les jetons tooenable, vous devez hello propriétés suivantes à partir de votre compte de développeur Apple :</span><span class="sxs-lookup"><span data-stu-id="57f09-120">tooenable token-based authentication, you need hello following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="57f09-121">Identificateur de clé</span><span class="sxs-lookup"><span data-stu-id="57f09-121">Key Identifier</span></span>
<span data-ttu-id="57f09-122">identificateur de clé Hello peut être obtenu à partir de la page « Clés » de hello dans votre compte de développeur Apple</span><span class="sxs-lookup"><span data-stu-id="57f09-122">hello key identifier can be obtained from hello "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="57f09-123">Identificateur de l’application et nom de l’application</span><span class="sxs-lookup"><span data-stu-id="57f09-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="57f09-124">nom de l’application Hello est disponible via la page de codes de l’application hello Bonjour compte de développeur.</span><span class="sxs-lookup"><span data-stu-id="57f09-124">hello application name is available via hello App IDs page in hello Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="57f09-125">identificateur de l’application Hello est disponible via la page de détails d’appartenance hello hello compte de développeur.</span><span class="sxs-lookup"><span data-stu-id="57f09-125">hello application identifier is available via hello membership details page in hello Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="57f09-126">Jeton d’authentification</span><span class="sxs-lookup"><span data-stu-id="57f09-126">Authentication token</span></span>
<span data-ttu-id="57f09-127">jeton d’authentification Hello peut être téléchargé après avoir généré un jeton pour votre application.</span><span class="sxs-lookup"><span data-stu-id="57f09-127">hello authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="57f09-128">Pour plus d’informations sur comment toogenerate ce jeton, consultez trop[documentation pour développeurs d’Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="57f09-128">For details on how toogenerate this token, refer too[Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a><span data-ttu-id="57f09-129">Configuration de l’authentification basée sur les jetons de notification hub toouse</span><span class="sxs-lookup"><span data-stu-id="57f09-129">Configuring your notification hub toouse token-based authentication</span></span>
### <a name="configure-via-hello-azure-portal"></a><span data-ttu-id="57f09-130">Configurer via hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="57f09-130">Configure via hello Azure portal</span></span>
<span data-ttu-id="57f09-131">jeton de tooenable en fonction de l’authentification dans le portail hello, ouvrez une session toohello portail Azure et accédez tooyour Hub de Notification > Services de Notification > Panneau de configuration APNS.</span><span class="sxs-lookup"><span data-stu-id="57f09-131">tooenable token based authentication in hello portal, log in toohello Azure portal and go tooyour Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="57f09-132">Il existe une nouvelle propriété : *Mode d’authentification*.</span><span class="sxs-lookup"><span data-stu-id="57f09-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="57f09-133">En sélectionnant le jeton vous permet de tooupdate votre concentrateur avec toutes les propriétés pertinentes hello du jeton.</span><span class="sxs-lookup"><span data-stu-id="57f09-133">Selecting Token allows you tooupdate your hub with all hello relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="57f09-134">Entrez les propriétés hello récupérés à partir de votre compte de développeur Apple,</span><span class="sxs-lookup"><span data-stu-id="57f09-134">Enter hello properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="57f09-135">choisissez votre mode d’application : Production ou Bac à sable (sandbox),</span><span class="sxs-lookup"><span data-stu-id="57f09-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="57f09-136">Cliquez sur Enregistrer tooupdate vos informations d’identification APNS.</span><span class="sxs-lookup"><span data-stu-id="57f09-136">click Save tooupdate your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="57f09-137">Configurer via l’API de gestion (REST)</span><span class="sxs-lookup"><span data-stu-id="57f09-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="57f09-138">Vous pouvez utiliser notre [API de gestion](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate votre notification hub toouse token d’authentification.</span><span class="sxs-lookup"><span data-stu-id="57f09-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate your notification hub toouse token-based authentication.</span></span>
<span data-ttu-id="57f09-139">Selon qu’application hello que vous configurez est une application de Production ou de bac à sable (spécifiée dans votre compte de développeur Apple), utilisez un des points de terminaison hello correspondants :</span><span class="sxs-lookup"><span data-stu-id="57f09-139">Depending on whether hello application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of hello corresponding endpoints:</span></span>

- <span data-ttu-id="57f09-140">Point de terminaison sandbox : [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="57f09-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="57f09-141">Point de terminaison de production : [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="57f09-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57f09-142">L’authentification basée sur un jeton nécessite la version d’API **2017-04 ou ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="57f09-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="57f09-143">Voici un exemple d’un tooupdate de demande PUT un concentrateur avec l’authentification basée sur un jeton :</span><span class="sxs-lookup"><span data-stu-id="57f09-143">Here’s an example of a PUT request tooupdate a hub with token-based authentication:</span></span>


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
        

### <a name="configure-via-hello-net-sdk"></a><span data-ttu-id="57f09-144">Configurer via hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="57f09-144">Configure via hello .NET SDK</span></span>
<span data-ttu-id="57f09-145">Vous pouvez configurer votre concentrateur toouse authentification par jeton notre [dernière version du Kit de développement logiciel client](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="57f09-145">You can configure your hub toouse token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="57f09-146">Voici un exemple de code illustrant l’utilisation correcte de hello :</span><span class="sxs-lookup"><span data-stu-id="57f09-146">Here’s a code sample illustrating hello correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a><span data-ttu-id="57f09-147">Authentification basée sur certificat rétablissement toousing</span><span class="sxs-lookup"><span data-stu-id="57f09-147">Reverting toousing certificate-based authentication</span></span>
<span data-ttu-id="57f09-148">Vous pouvez revenir à n’importe quel moment toousing authentification par certificat à l’aide de n’importe quel certificat précédent de hello méthode et en passant au lieu des propriétés de jeton hello.</span><span class="sxs-lookup"><span data-stu-id="57f09-148">You can revert at any time toousing certificate-based authentication by using any preceding method and passing hello certificate instead of hello token properties.</span></span> <span data-ttu-id="57f09-149">Qu’action remplace hello précédemment stockées les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="57f09-149">That action overwrites hello previously stored credentials.</span></span>
