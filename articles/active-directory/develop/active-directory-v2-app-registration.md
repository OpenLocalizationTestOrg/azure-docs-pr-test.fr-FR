---
title: "aaaRegister une application avec un point de terminaison v2.0 hello Azure AD à l’aide du portail de hello | Documents Microsoft"
description: "Comment tooregister une application avec Microsoft pour l’activation de l’authentification et l’accès à Microsoft services à l’aide du point de terminaison hello v2.0"
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
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a><span data-ttu-id="0a073-103">Comment tooregister une application avec un point de terminaison hello v2.0</span><span class="sxs-lookup"><span data-stu-id="0a073-103">How tooregister an app with hello v2.0 endpoint</span></span>
<span data-ttu-id="0a073-104">toobuild une application qui accepte le compte de service administré et Azure AD, sign-in, vous devez tout d’abord tooregister une application avec Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0a073-104">toobuild an app that accepts both MSA & Azure AD sign-in, you'll first need tooregister an app with Microsoft.</span></span>  <span data-ttu-id="0a073-105">À ce stade, vous ne serez pas être en mesure de toouse toutes les applications existantes, vous auriez conclus avec Azure AD ou MSA - vous devez toocreate une marque de nouveau.</span><span class="sxs-lookup"><span data-stu-id="0a073-105">At this time, you won't be able toouse any existing apps you may have with Azure AD or MSA - you'll need toocreate a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="0a073-106">Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="0a073-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="0a073-107">toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="0a073-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a><span data-ttu-id="0a073-108">Visitez le portail d’inscription application hello Microsoft</span><span class="sxs-lookup"><span data-stu-id="0a073-108">Visit hello Microsoft app registration portal</span></span>
<span data-ttu-id="0a073-109">Avant tout - accédez d’abord trop[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="0a073-109">First things first - navigate too[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="0a073-110">Il s’agit d’un nouveau portail d’inscription des applications où vous pouvez gérer vos applications Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0a073-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="0a073-111">Connectez-vous à l’aide d’un compte Microsoft personnel, professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="0a073-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="0a073-112">Si vous en êtes dépourvu, inscrivez-vous pour obtenir un nouveau compte personnel.</span><span class="sxs-lookup"><span data-stu-id="0a073-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="0a073-113">Cela ne sera pas long. Nous patientons ici.</span><span class="sxs-lookup"><span data-stu-id="0a073-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="0a073-114">Vous avez terminé ?</span><span class="sxs-lookup"><span data-stu-id="0a073-114">Done?</span></span> <span data-ttu-id="0a073-115">À présent, consultez votre liste d’applications Microsoft, qui est probablement vide.</span><span class="sxs-lookup"><span data-stu-id="0a073-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="0a073-116">Nous allons y remédier.</span><span class="sxs-lookup"><span data-stu-id="0a073-116">Let's change that.</span></span>

<span data-ttu-id="0a073-117">Cliquez sur **Ajouter une application**, et attribuez-lui un nom.</span><span class="sxs-lookup"><span data-stu-id="0a073-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="0a073-118">portail de Hello affectera votre application un Id global unique d’Application que vous utiliserez ultérieurement dans votre code.</span><span class="sxs-lookup"><span data-stu-id="0a073-118">hello portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="0a073-119">Si votre application inclut un composant côté serveur qui a besoin de jetons d’accès pour appeler des API (pensez : Office, Azure ou votre propre API web), vous souhaiterez toocreate un **Secret d’Application** ici.</span><span class="sxs-lookup"><span data-stu-id="0a073-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want toocreate an **Application Secret** here as well.</span></span>

<span data-ttu-id="0a073-120">Ensuite, ajoutez hello plateformes que votre application utilisera.</span><span class="sxs-lookup"><span data-stu-id="0a073-120">Next, add hello Platforms that your app will use.</span></span>

* <span data-ttu-id="0a073-121">Pour les applications basées sur le Web, fournissez une **URI de redirection** où les messages de connexion peuvent être envoyés.</span><span class="sxs-lookup"><span data-stu-id="0a073-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="0a073-122">Pour les applications mobiles, copiez la valeur par défaut hello créé automatiquement pour vous des uri de redirection.</span><span class="sxs-lookup"><span data-stu-id="0a073-122">For mobile apps, copy down hello default redirect uri automatically created for you.</span></span>

<span data-ttu-id="0a073-123">Si vous le souhaitez, vous pouvez personnaliser hello apparence de votre page de connexion Bonjour profil.</span><span class="sxs-lookup"><span data-stu-id="0a073-123">Optionally, you can customize hello look and feel of your sign-in page in hello Profile section.</span></span>  <span data-ttu-id="0a073-124">Assurez-vous que tooclick **enregistrer** avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="0a073-124">Make sure tooclick **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="0a073-125">Lorsque vous créez une application en utilisant [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), application hello est enregistrée dans le locataire d’accueil hello hello de compte de que vous utilisez toosign portail de hello.</span><span class="sxs-lookup"><span data-stu-id="0a073-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello application will be registered in hello home tenant of hello account that you use toosign into hello portal.</span></span>  <span data-ttu-id="0a073-126">Cela signifie que vous ne pouvez pas inscrire une application dans votre client Azure AD à l’aide d’un compte Microsoft personnel.</span><span class="sxs-lookup"><span data-stu-id="0a073-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="0a073-127">Si vous explicitement souhaitez tooregister une application dans un locataire particulier, connectez-vous avec un compte créé à l’origine de ce client.</span><span class="sxs-lookup"><span data-stu-id="0a073-127">If you explicitly wish tooregister an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="0a073-128">Générer une application de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="0a073-128">Build a quick start app</span></span>
<span data-ttu-id="0a073-129">Maintenant que vous disposez d’une application Microsoft, vous pouvez suivre l’un de nos didacticiels de démarrage rapide de v2.0.</span><span class="sxs-lookup"><span data-stu-id="0a073-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="0a073-130">Voici quelques recommandations :</span><span class="sxs-lookup"><span data-stu-id="0a073-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

