---
title: "Applications prenant en charge les revendications - Proxy d’application Azure AD | Microsoft Docs"
description: "Comment publier des applications ASP.NET locales qui acceptent les revendications ADFS pour un accès à distance sécurisé par vos utilisateurs."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 5784222608b01509fc4ff84b1a8792cbcfea89e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="4978d-103">Utilisation d’applications prenant en charge les revendications dans le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="4978d-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="4978d-104">[Les applications prenant en charge les revendications](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) effectuent une redirection vers le service d’émission de jeton de sécurité (STS).</span><span class="sxs-lookup"><span data-stu-id="4978d-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span></span> <span data-ttu-id="4978d-105">Le service d’émission de jeton de sécurité demande des informations d’identification à l’utilisateur en échange d’un jeton, puis redirige l’utilisateur vers l’application.</span><span class="sxs-lookup"><span data-stu-id="4978d-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span></span> <span data-ttu-id="4978d-106">Il existe plusieurs façons d’activer le proxy d’application pour utiliser ces redirections.</span><span class="sxs-lookup"><span data-stu-id="4978d-106">There are a few ways to enable Application Proxy to work with these redirects.</span></span> <span data-ttu-id="4978d-107">Utilisez cet article pour configurer votre déploiement pour les applications prenant en charge les revendications.</span><span class="sxs-lookup"><span data-stu-id="4978d-107">Use this article to configure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4978d-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4978d-108">Prerequisites</span></span>
<span data-ttu-id="4978d-109">Vérifiez que le service d’émission de jeton de sécurité vers lequel l’application prenant en charge les revendications effectue la redirection est disponible en dehors de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="4978d-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span></span> <span data-ttu-id="4978d-110">Vous pouvez rendre le service d’émission de jeton de sécurité disponible en l’exposant par le biais d’un proxy ou en autorisant les connexions externes.</span><span class="sxs-lookup"><span data-stu-id="4978d-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="4978d-111">Publication de votre application</span><span class="sxs-lookup"><span data-stu-id="4978d-111">Publish your application</span></span>

1. <span data-ttu-id="4978d-112">Publiez votre application en suivant les instructions décrites dans [Publier des applications avec le proxy d’application](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4978d-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="4978d-113">Accédez à la page de l’application dans le portail et sélectionnez **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4978d-113">Navigate to the application page in the portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="4978d-114">Si vous choisissez **Azure Active Directory** comme **méthode de préauthentification**, sélectionnez **Authentification unique Azure AD désactivée** comme **méthode d’authentification interne**.</span><span class="sxs-lookup"><span data-stu-id="4978d-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="4978d-115">Si vous avez choisi **Directe** comme **méthode de préauthentification**, vous n’avez rien à modifier.</span><span class="sxs-lookup"><span data-stu-id="4978d-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="4978d-116">Configurer AD FS</span><span class="sxs-lookup"><span data-stu-id="4978d-116">Configure ADFS</span></span>

<span data-ttu-id="4978d-117">Vous pouvez configurer AD FS pour les applications prenant en charge les revendications de deux façons.</span><span class="sxs-lookup"><span data-stu-id="4978d-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="4978d-118">La première consiste à utiliser des domaines personnalisés.</span><span class="sxs-lookup"><span data-stu-id="4978d-118">The first is by using custom domains.</span></span> <span data-ttu-id="4978d-119">La seconde consiste à utiliser WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="4978d-119">The second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="4978d-120">Option 1 : domaines personnalisés</span><span class="sxs-lookup"><span data-stu-id="4978d-120">Option 1: Custom domains</span></span>

<span data-ttu-id="4978d-121">Si toutes les URL internes de vos applications sont des noms de domaines complets (FQDN), alors vous pouvez configurer des [domaines personnalisés](active-directory-application-proxy-custom-domains.md) pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="4978d-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="4978d-122">Utilisez ces domaines personnalisés pour créer des URL externes identiques aux URL internes.</span><span class="sxs-lookup"><span data-stu-id="4978d-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span></span> <span data-ttu-id="4978d-123">Lorsque vos URL externes correspondent à vos URL internes, les redirections STS fonctionnent que vos utilisateurs soient locaux ou à distance.</span><span class="sxs-lookup"><span data-stu-id="4978d-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="4978d-124">Option 2 : WS-Federation</span><span class="sxs-lookup"><span data-stu-id="4978d-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="4978d-125">Ouvrez Gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="4978d-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="4978d-126">Accédez à **Approbations de la partie de confiance**, cliquez avec le bouton droit sur l’application que vous publiez avec le proxy d’application, puis choisissez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="4978d-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Approbations de partie de confiance, clic droit sur le nom de l’application - capture d’écran](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="4978d-128">Sous l’onglet **Points de terminaison**, sous **Type de point de terminaison**, sélectionnez **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="4978d-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="4978d-129">Sous **URL approuvée**, entrez l’URL que vous avez entrée dans le proxy d’application sous **URL externe**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4978d-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Ajouter un point de terminaison, définition de la valeur de l’URL approuvée – capture d’écran](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="4978d-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4978d-131">Next steps</span></span>
* <span data-ttu-id="4978d-132">[Activer l’authentification unique](application-proxy-sso-overview.md) pour les applications qui ne prennent pas en charge les revendications</span><span class="sxs-lookup"><span data-stu-id="4978d-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="4978d-133">Activation d’applications clientes natives de manière à ce qu’elles interagissent avec des applications proxy</span><span class="sxs-lookup"><span data-stu-id="4978d-133">Enable native client apps to interact with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


