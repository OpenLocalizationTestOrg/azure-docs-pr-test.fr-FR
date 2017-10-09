---
title: "aaaSingle authentification tooapps avec Proxy d’Application Azure AD | Documents Microsoft"
description: "Activer l’authentification unique pour vos applications publiées sur site avec le Proxy d’Application Azure AD Bonjour portail Azure."
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
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="bd3bc-103">Authentification unique avec mise au coffre des mots de passe par le biais du proxy d’application</span><span class="sxs-lookup"><span data-stu-id="bd3bc-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="bd3bc-104">Le service Proxy d’application Azure Active Directory vous aide à améliorer la productivité en publiant des applications locales afin que les employés travaillant à distance puissent également y accéder.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="bd3bc-105">Bonjour portail Azure, vous pouvez également configurer unique (SSO) toothese applications avec authentification.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-105">In hello Azure portal, you can also set up single sign-on (SSO) toothese apps.</span></span> <span data-ttu-id="bd3bc-106">Vos utilisateurs doivent uniquement tooauthenticate avec Azure AD, et ils peuvent accéder à votre application d’entreprise sans avoir à nouveau les toosign.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-106">Your users only need tooauthenticate with Azure AD, and they can access your enterprise application without having toosign in again.</span></span>

<span data-ttu-id="bd3bc-107">Le proxy d’application prend en charge plusieurs [modes d’authentification unique](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd3bc-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="bd3bc-108">L’authentification par mot de passe est destinée aux applications qui utilisent une combinaison nom d’utilisateur/mot de passe pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="bd3bc-109">Lorsque vous configurez le mot de passe de session pour votre application, vos utilisateurs ont toosign dans l’application locale de toohello une seule fois.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-109">When you configure password-based sign-on for your application, your users have toosign in toohello on-premises application once.</span></span> <span data-ttu-id="bd3bc-110">Après cela, Azure Active Directory stocke les informations de connexion hello et fournit automatiquement il toohello application lorsque vos utilisateurs l’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-110">After that, Azure Active Directory stores hello sign-in information and automatically provides it toohello application when your users access it remotely.</span></span> 

<span data-ttu-id="bd3bc-111">Vous devez avoir déjà publié et testé votre application avec le proxy d’application.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="bd3bc-112">Dans le cas contraire, suivez les étapes de hello dans [publier des applications à l’aide du Proxy d’Application Azure AD](application-proxy-publish-azure-portal.md) puis revenez ici.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-112">If not, follow hello steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="bd3bc-113">Configurer le stockage de mots de passe pour votre application</span><span class="sxs-lookup"><span data-stu-id="bd3bc-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="bd3bc-114">Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-114">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="bd3bc-115">Sélectionnez **Azure Active Directory** > **Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="bd3bc-116">À partir de la liste de hello, sélectionnez application hello que vous souhaitez tooset les avec l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-116">From hello list, select hello app that you want tooset up with SSO.</span></span>  
4. <span data-ttu-id="bd3bc-117">Sélectionnez **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-117">Select **Single sign-on**.</span></span>

   ![Sélectionner l’authentification unique](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="bd3bc-119">Pour le mode d’authentification unique de hello, choisissez **mot de passe de session**.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-119">For hello SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="bd3bc-120">Pour l’URL de connexion hello, entrez hello URL pour la page de hello où les utilisateurs entrent leur toosign nom d’utilisateur et mot de passe dans l’application tooyour en dehors du réseau d’entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-120">For hello Sign-on URL, enter hello URL for hello page where users enter their username and password toosign in tooyour app outside of hello corporate network.</span></span> <span data-ttu-id="bd3bc-121">Cela peut être hello URL externe que vous avez créé lorsque vous avez publié l’application hello via le Proxy d’Application.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-121">This may be hello External URL that you created when you published hello app through Application Proxy.</span></span> 

   ![Choisissez Authentification par mot de passe et entrez votre URL.](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="bd3bc-123">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-123">Select **Save**.</span></span>

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="bd3bc-124">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="bd3bc-124">Test your app</span></span>

<span data-ttu-id="bd3bc-125">Accédez tooexternal URL que vous avez configuré pour l’application de tooyour d’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-125">Go tooexternal URL that you configured for remote access tooyour application.</span></span> <span data-ttu-id="bd3bc-126">Connectez-vous avec vos informations d’identification pour cette application (ou hello pour un compte de test que vous avez configurée avec un accès).</span><span class="sxs-lookup"><span data-stu-id="bd3bc-126">Sign in with your credentials for that app (or hello credentials for a test account that you set up with access).</span></span> <span data-ttu-id="bd3bc-127">Une fois que vous êtes connecté avec succès, vous devez être en mesure de tooleave hello application et revenez sans entrer de nouveau vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="bd3bc-127">Once you sign in successfully, you should be able tooleave hello app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bd3bc-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd3bc-128">Next steps</span></span>

- <span data-ttu-id="bd3bc-129">En savoir plus sur d’autres façons tooimplement [Single sign-on avec le Proxy d’Application](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bd3bc-129">Read about other ways tooimplement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="bd3bc-130">En savoir plus sur les [considérations de sécurité pour l’accès aux applications à distance avec le proxy d’application Azure AD](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="bd3bc-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>