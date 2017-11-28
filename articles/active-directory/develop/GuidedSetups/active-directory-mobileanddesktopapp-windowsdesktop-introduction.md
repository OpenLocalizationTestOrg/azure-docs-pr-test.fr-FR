---
title: "Prise en main d’Azure AD v2 avec les applications de bureau Windows - Introduction | Documents Microsoft"
description: "Cet article explique comment les applications de bureau Windows .NET (XAML) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 4a695c00fce4deb02261ba58ec95469746bb1486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="call-the-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="c3e80-103">Appeler l’API Microsoft Graph à partir d’une application de bureau Windows</span><span class="sxs-lookup"><span data-stu-id="c3e80-103">Call the Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="c3e80-104">Ce guide explique comment une application de bureau Windows .NET (XAML) native peut obtenir un jeton d’accès et appeler l’API Microsoft Graph ou d’autres API qui nécessitent des jetons d’accès provenant d’un point de terminaison Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="c3e80-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="c3e80-105">À la fin de ce guide, votre application pourra appeler une API protégée à l’aide de comptes personnels (y compris outlook.com et live.com), ainsi que de comptes professionnels et scolaires de n’importe quelle société ou organisation qui possède Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3e80-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="c3e80-106">Ce guide requiert Visual Studio 2015 Update 3 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c3e80-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="c3e80-107">Ni l’un, ni l’autre ne sont installés sur votre ordinateur ?</span><span class="sxs-lookup"><span data-stu-id="c3e80-107">Don’t have it?</span></span> [<span data-ttu-id="c3e80-108">Téléchargez gratuitement Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c3e80-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="c3e80-109">Fonctionnement de ce guide</span><span class="sxs-lookup"><span data-stu-id="c3e80-109">How this guide works</span></span>

![Fonctionnement de ce guide](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="c3e80-111">L’exemple d’application créé dans le cadre de ce guide permet à une application de bureau Windows d’interroger l’API Microsoft Graph ou une API web qui accepte les jetons à partir d’un point de terminaison Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="c3e80-111">The sample application created by this guide enables a Windows Desktop Application to query Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="c3e80-112">Pour ce scénario, un jeton est ajouté aux requêtes HTTP via l’en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="c3e80-112">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="c3e80-113">L’acquisition et le renouvellement de jetons sont gérés par la bibliothèque d’authentification Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="c3e80-113">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="c3e80-114">Gestion de l’acquisition de jetons pour accéder à des API web protégées</span><span class="sxs-lookup"><span data-stu-id="c3e80-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="c3e80-115">Une fois l’utilisateur authentifié, l’exemple d’application reçoit un jeton qui peut être utilisé pour interroger l’API Microsoft Graph ou une API web sécurisée par Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="c3e80-115">After the user authenticates, the sample application receives a token that can be used to query Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="c3e80-116">Les API telles que Microsoft Graph requièrent un jeton d’accès pour autoriser l’accès à des ressources spécifiques, par exemple pour lire le profil d’un utilisateur, accéder au calendrier de l’utilisateur ou envoyer un courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="c3e80-116">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="c3e80-117">Votre application peut demander un jeton d’accès à l’aide de MSAL pour accéder à ces ressources en spécifiant les étendues d’API.</span><span class="sxs-lookup"><span data-stu-id="c3e80-117">Your application can request an access token using MSAL to access these resources by specifying API scopes.</span></span> <span data-ttu-id="c3e80-118">Ce jeton d’accès est ensuite ajouté à l’en-tête d’autorisation HTTP pour chaque appel effectué sur la ressource protégée.</span><span class="sxs-lookup"><span data-stu-id="c3e80-118">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span> 

<span data-ttu-id="c3e80-119">MSAL gère la mise en cache et l’actualisation des jetons d’accès pour vous, ce qui évite à votre application d’avoir à le faire.</span><span class="sxs-lookup"><span data-stu-id="c3e80-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="c3e80-120">Packages NuGet</span><span class="sxs-lookup"><span data-stu-id="c3e80-120">NuGet Packages</span></span>

<span data-ttu-id="c3e80-121">Ce guide utilise les packages NuGet suivants :</span><span class="sxs-lookup"><span data-stu-id="c3e80-121">This guide uses the following NuGet packages:</span></span>

|<span data-ttu-id="c3e80-122">Bibliothèque</span><span class="sxs-lookup"><span data-stu-id="c3e80-122">Library</span></span>|<span data-ttu-id="c3e80-123">Description</span><span class="sxs-lookup"><span data-stu-id="c3e80-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="c3e80-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="c3e80-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="c3e80-125">Bibliothèque d’authentification Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="c3e80-125">Microsoft Authentication Library (MSAL)</span></span>|

