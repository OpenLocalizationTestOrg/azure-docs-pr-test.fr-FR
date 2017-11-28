---
title: "les applications prenant en charge les aaaClaims - Proxy d’application Azure AD | Documents Microsoft"
description: "Comment toopublish localement les applications ASP.NET qui accepte les revendications AD FS pour l’accès à distance sécurisé par vos utilisateurs."
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
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="71db6-103">Utilisation d’applications prenant en charge les revendications dans le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="71db6-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="71db6-104">[Les applications prenant en charge les revendications](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) effectuer une redirection de toohello Service de jeton de sécurité (STS).</span><span class="sxs-lookup"><span data-stu-id="71db6-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection toohello Security Token Service (STS).</span></span> <span data-ttu-id="71db6-105">Hello STS demande des informations d’identification d’utilisateur hello en échange d’un jeton et redirige ensuite l’application hello utilisateur toohello.</span><span class="sxs-lookup"><span data-stu-id="71db6-105">hello STS requests credentials from hello user in exchange for a token and then redirects hello user toohello application.</span></span> <span data-ttu-id="71db6-106">Il existe quelques toowork de Proxy d’Application tooenable manières avec ces redirections.</span><span class="sxs-lookup"><span data-stu-id="71db6-106">There are a few ways tooenable Application Proxy toowork with these redirects.</span></span> <span data-ttu-id="71db6-107">Utilisez cette tooconfigure article votre déploiement pour les applications prenant en charge les revendications.</span><span class="sxs-lookup"><span data-stu-id="71db6-107">Use this article tooconfigure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="71db6-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="71db6-108">Prerequisites</span></span>
<span data-ttu-id="71db6-109">Assurez-vous que ce STS hello qui hello application prenant en charge les revendications redirige toois disponible en dehors de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="71db6-109">Make sure that hello STS that hello claims-aware app redirects toois available outside of your on-premises network.</span></span> <span data-ttu-id="71db6-110">Vous pouvez rendre hello STS disponible en exposant via un proxy ou en autorisant les connexions à l’extérieur.</span><span class="sxs-lookup"><span data-stu-id="71db6-110">You can make hello STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="71db6-111">Publication de votre application</span><span class="sxs-lookup"><span data-stu-id="71db6-111">Publish your application</span></span>

1. <span data-ttu-id="71db6-112">Publier votre application en fonction des instructions toohello décrites dans [publier des applications avec Proxy d’Application](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="71db6-112">Publish your application according toohello instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="71db6-113">Parcourir la page d’application toohello Bonjour portail et sélectionnez **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="71db6-113">Navigate toohello application page in hello portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="71db6-114">Si vous choisissez **Azure Active Directory** comme **méthode de préauthentification**, sélectionnez **Authentification unique Azure AD désactivée** comme **méthode d’authentification interne**.</span><span class="sxs-lookup"><span data-stu-id="71db6-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="71db6-115">Si vous avez choisi **Passthrough** en tant que votre **méthode de pré-authentification**, vous n’avez pas besoin toochange n’est pas défini.</span><span class="sxs-lookup"><span data-stu-id="71db6-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need toochange anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="71db6-116">Configurer AD FS</span><span class="sxs-lookup"><span data-stu-id="71db6-116">Configure ADFS</span></span>

<span data-ttu-id="71db6-117">Vous pouvez configurer AD FS pour les applications prenant en charge les revendications de deux façons.</span><span class="sxs-lookup"><span data-stu-id="71db6-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="71db6-118">Hello est tout d’abord à l’aide de domaines personnalisés.</span><span class="sxs-lookup"><span data-stu-id="71db6-118">hello first is by using custom domains.</span></span> <span data-ttu-id="71db6-119">Hello est ensuite avec WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="71db6-119">hello second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="71db6-120">Option 1 : domaines personnalisés</span><span class="sxs-lookup"><span data-stu-id="71db6-120">Option 1: Custom domains</span></span>

<span data-ttu-id="71db6-121">Si tous hello URL internes pour vos applications sont pleinement qualifiées (FQDN) des noms de domaine, vous pouvez ensuite configurer [des domaines personnalisés](active-directory-application-proxy-custom-domains.md) pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="71db6-121">If all hello internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="71db6-122">Utilisez hello domaines personnalisés toocreate URL externes qui sont hello identique hello URL internes.</span><span class="sxs-lookup"><span data-stu-id="71db6-122">Use hello custom domains toocreate external URLs that are hello same as hello internal URLs.</span></span> <span data-ttu-id="71db6-123">Lorsque votre URL externes correspondent à votre URL internes, les redirections de STS hello fonctionnent si vos utilisateurs sont en local ou à distance.</span><span class="sxs-lookup"><span data-stu-id="71db6-123">When your external URLs match your internal URLs, then hello STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="71db6-124">Option 2 : WS-Federation</span><span class="sxs-lookup"><span data-stu-id="71db6-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="71db6-125">Ouvrez Gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="71db6-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="71db6-126">Accédez trop**confiance**, avec le bouton droit sur l’application hello publication avec le Proxy d’Application, puis choisissez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="71db6-126">Go too**Relying Party Trusts**, right-click on hello app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Approbations de partie de confiance, clic droit sur le nom de l’application - capture d’écran](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="71db6-128">Sur hello **points de terminaison** sous l’onglet sous **type de point de terminaison**, sélectionnez **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="71db6-128">On hello **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="71db6-129">Sous **URL de confiance**, entrez les URL hello saisis dans hello Proxy d’Application sous **URL externe** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="71db6-129">Under **Trusted URL**, enter hello URL you entered in hello Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Ajouter un point de terminaison, définition de la valeur de l’URL approuvée – capture d’écran](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="71db6-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71db6-131">Next steps</span></span>
* <span data-ttu-id="71db6-132">[Activer l’authentification unique](application-proxy-sso-overview.md) pour les applications qui ne prennent pas en charge les revendications</span><span class="sxs-lookup"><span data-stu-id="71db6-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="71db6-133">Activer toointeract d’applications client natif avec les applications du proxy</span><span class="sxs-lookup"><span data-stu-id="71db6-133">Enable native client apps toointeract with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


