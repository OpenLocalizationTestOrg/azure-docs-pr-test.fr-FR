---
title: "Authentification unique auprès des applications avec le proxy d’application Azure AD | Microsoft Docs"
description: "Activez l’authentification unique pour vos applications locales publiées avec le proxy d’application Azure AD dans le portail Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9ddc0c1bd5f2cbb24f6761cfd041b820ee6464b8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="311c8-103">Authentification unique avec mise au coffre des mots de passe par le biais du proxy d’application</span><span class="sxs-lookup"><span data-stu-id="311c8-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="311c8-104">Le service Proxy d’application Azure Active Directory vous aide à améliorer la productivité en publiant des applications locales afin que les employés travaillant à distance puissent également y accéder.</span><span class="sxs-lookup"><span data-stu-id="311c8-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="311c8-105">Dans le portail Azure, vous pouvez également configurer l’authentification unique auprès de ces applications.</span><span class="sxs-lookup"><span data-stu-id="311c8-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span></span> <span data-ttu-id="311c8-106">Vos utilisateurs n’ont qu’à s’authentifier auprès d’Azure AD pour accéder à votre application d’entreprise sans se reconnecter.</span><span class="sxs-lookup"><span data-stu-id="311c8-106">Your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span></span>

<span data-ttu-id="311c8-107">Le proxy d’application prend en charge plusieurs [modes d’authentification unique](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="311c8-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="311c8-108">L’authentification par mot de passe est destinée aux applications qui utilisent une combinaison nom d’utilisateur/mot de passe pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="311c8-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="311c8-109">Lorsque vous configurez l’authentification par mot de passe pour votre application, vos utilisateurs ne doivent se connecter à l’application locale qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="311c8-109">When you configure password-based sign-on for your application, your users have to sign in to the on-premises application once.</span></span> <span data-ttu-id="311c8-110">Azure Active Directory stocke ensuite les informations de connexion et les fournit automatiquement à l’application lorsque vos utilisateurs y accèdent à distance.</span><span class="sxs-lookup"><span data-stu-id="311c8-110">After that, Azure Active Directory stores the sign-in information and automatically provides it to the application when your users access it remotely.</span></span> 

<span data-ttu-id="311c8-111">Vous devez avoir déjà publié et testé votre application avec le proxy d’application.</span><span class="sxs-lookup"><span data-stu-id="311c8-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="311c8-112">Sinon, suivez les étapes de la rubrique [Publier des applications avec le Proxy d’application Azure AD](application-proxy-publish-azure-portal.md) avant de revenir ici.</span><span class="sxs-lookup"><span data-stu-id="311c8-112">If not, follow the steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="311c8-113">Configurer le stockage de mots de passe pour votre application</span><span class="sxs-lookup"><span data-stu-id="311c8-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="311c8-114">Connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="311c8-114">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="311c8-115">Sélectionnez **Azure Active Directory** > **Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="311c8-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="311c8-116">Dans la liste, sélectionnez l’application pour laquelle vous voulez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="311c8-116">From the list, select the app that you want to set up with SSO.</span></span>  
4. <span data-ttu-id="311c8-117">Sélectionner **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="311c8-117">Select **Single sign-on**.</span></span>

   ![Sélectionner l’authentification unique](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="311c8-119">Pour le mode d’authentification unique, choisissez **Authentification par mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="311c8-119">For the SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="311c8-120">Pour l’URL de connexion, entrez l’URL de la page où les utilisateurs entrent leur nom d’utilisateur et leur mot de passe pour se connecter à votre application en dehors du réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="311c8-120">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network.</span></span> <span data-ttu-id="311c8-121">Il peut s’agir de l’URL externe que vous avez créée quand vous avez publié l’application par le biais du proxy d’application.</span><span class="sxs-lookup"><span data-stu-id="311c8-121">This may be the External URL that you created when you published the app through Application Proxy.</span></span> 

   ![Choisissez Authentification par mot de passe et entrez votre URL.](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="311c8-123">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="311c8-123">Select **Save**.</span></span>

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="311c8-124">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="311c8-124">Test your app</span></span>

<span data-ttu-id="311c8-125">Accédez à l’URL externe que vous avez configurée pour l’accès à distance à votre application.</span><span class="sxs-lookup"><span data-stu-id="311c8-125">Go to external URL that you configured for remote access to your application.</span></span> <span data-ttu-id="311c8-126">Connectez-vous avec vos informations d’identification associées à cette application (ou celles d’un compte de test pour lequel vous avez configuré un accès).</span><span class="sxs-lookup"><span data-stu-id="311c8-126">Sign in with your credentials for that app (or the credentials for a test account that you set up with access).</span></span> <span data-ttu-id="311c8-127">Une fois que vous êtes connecté, vous devez pouvoir quitter l’application et revenir sans entrer à nouveau vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="311c8-127">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="311c8-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="311c8-128">Next steps</span></span>

- <span data-ttu-id="311c8-129">En savoir plus sur les autres façons d’implémenter l’[authentification unique avec le proxy d’application](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="311c8-129">Read about other ways to implement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="311c8-130">En savoir plus sur les [considérations de sécurité pour l’accès aux applications à distance avec le proxy d’application Azure AD](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="311c8-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>