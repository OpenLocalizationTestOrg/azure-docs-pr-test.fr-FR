---
title: "Inscription d’une application avec le point de terminaison Azure AD v2.0 à l’aide du portail | Microsoft Docs"
description: "Inscription d’une application avec Microsoft pour l’activation de l’authentification et l’accès aux services Microsoft à l’aide du point de terminaison v2.0"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: e6202aa8665c906382666fe08a561421e50e0a8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="8e2c6-103">Inscription d’une application avec le point de terminaison v2.0</span><span class="sxs-lookup"><span data-stu-id="8e2c6-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="8e2c6-104">Pour générer une application prenant en charge à la fois les connexions à MSA et Azure AD, vous devez d’abord l’inscrire auprès de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="8e2c6-105">Pour le moment, vous ne pouvez pas utiliser les applications existantes avec Azure AD ou MSA. Vous devez en créer une.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="8e2c6-106">Les scénarios et les fonctionnalités Azure Active Directory ne sont pas tous pris en charge par le point de terminaison v2.0.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="8e2c6-107">Pour déterminer si vous devez utiliser le point de terminaison v2.0, consultez les [limites de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="8e2c6-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="8e2c6-108">Visiter le portail d’inscription des applications Microsoft</span><span class="sxs-lookup"><span data-stu-id="8e2c6-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="8e2c6-109">Commencez tout d’abord par accéder à [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="8e2c6-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="8e2c6-110">Il s’agit d’un nouveau portail d’inscription des applications où vous pouvez gérer vos applications Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="8e2c6-111">Connectez-vous à l’aide d’un compte Microsoft personnel, professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="8e2c6-112">Si vous en êtes dépourvu, inscrivez-vous pour obtenir un nouveau compte personnel.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="8e2c6-113">Cela ne sera pas long. Nous patientons ici.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="8e2c6-114">Vous avez terminé ?</span><span class="sxs-lookup"><span data-stu-id="8e2c6-114">Done?</span></span> <span data-ttu-id="8e2c6-115">À présent, consultez votre liste d’applications Microsoft, qui est probablement vide.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="8e2c6-116">Nous allons y remédier.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-116">Let's change that.</span></span>

<span data-ttu-id="8e2c6-117">Cliquez sur **Ajouter une application**, et attribuez-lui un nom.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="8e2c6-118">Le portail attribue à votre application un ID d’application global unique que vous utiliserez ultérieurement dans votre code.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="8e2c6-119">Si votre application inclut un composant côté serveur, qui nécessite des jetons d’accès pour appeler des API (à savoir Office, Azure ou votre propre API Web), créez également ici un **secret d’application** .</span><span class="sxs-lookup"><span data-stu-id="8e2c6-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="8e2c6-120">Ensuite, ajoutez les plateformes que votre application utilisera.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="8e2c6-121">Pour les applications basées sur le Web, fournissez une **URI de redirection** où les messages de connexion peuvent être envoyés.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="8e2c6-122">Pour les applications mobiles, copiez la valeur par défaut de l’URI de redirection créée automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="8e2c6-123">Si vous le souhaitez, vous pouvez personnaliser l’apparence de votre page de connexion dans la section Profil.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="8e2c6-124">Avant de continuer, veillez à cliquer sur **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8e2c6-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="8e2c6-125">Lorsque vous créez une application à l'aide de [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), l’application est enregistrée dans le client de base du compte que vous utilisez pour vous connecter au portail.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="8e2c6-126">Cela signifie que vous ne pouvez pas inscrire une application dans votre client Azure AD à l’aide d’un compte Microsoft personnel.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="8e2c6-127">Si vous souhaitez réellement inscrire une application dans un client particulier, connectez-vous avec un compte créé à l’origine dans ce client.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="8e2c6-128">Générer une application de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="8e2c6-128">Build a quick start app</span></span>
<span data-ttu-id="8e2c6-129">Maintenant que vous disposez d’une application Microsoft, vous pouvez suivre l’un de nos didacticiels de démarrage rapide de v2.0.</span><span class="sxs-lookup"><span data-stu-id="8e2c6-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="8e2c6-130">Voici quelques recommandations :</span><span class="sxs-lookup"><span data-stu-id="8e2c6-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

