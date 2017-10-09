---
title: aaaAzure AD v2 Windows Desktop mise en route - introduction | Documents Microsoft
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="d5740-103">Appel hello Microsoft Graph API à partir d’une application de bureau Windows</span><span class="sxs-lookup"><span data-stu-id="d5740-103">Call hello Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="d5740-104">Ce guide explique comment une application de bureau Windows .NET (XAML) native peut obtenir un jeton d’accès et appeler l’API Microsoft Graph ou d’autres API qui nécessitent des jetons d’accès provenant d’un point de terminaison Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="d5740-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="d5740-105">À la fin de hello de ce guide, votre application sera être en mesure de toocall API protégée à l’aide des comptes personnels (y compris les outlook.com, live.com et autres) ainsi que de travail et les comptes d’établissement d’une entreprise ou d’une organisation qui dispose d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5740-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="d5740-106">Ce guide requiert Visual Studio 2015 Update 3 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d5740-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="d5740-107">Ni l’un, ni l’autre ne sont installés sur votre ordinateur ?</span><span class="sxs-lookup"><span data-stu-id="d5740-107">Don’t have it?</span></span> [<span data-ttu-id="d5740-108">Téléchargez gratuitement Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d5740-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="d5740-109">Fonctionnement de ce guide</span><span class="sxs-lookup"><span data-stu-id="d5740-109">How this guide works</span></span>

![Fonctionnement de ce guide](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="d5740-111">Hello exemple d’application créé par ce guide permet à une Application de bureau Windows de tooquery Microsoft Graph API ou une API Web qui accepte les jetons à partir du point de terminaison Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="d5740-111">hello sample application created by this guide enables a Windows Desktop Application tooquery Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="d5740-112">Pour ce scénario, un jeton est ajouté tooHTTP des demandes via l’en-tête d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="d5740-112">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="d5740-113">Renouvellement et acquisition de jeton est gérée par hello bibliothèque d’authentification Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="d5740-113">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="d5740-114">Gestion de l’acquisition de jetons pour accéder à des API web protégées</span><span class="sxs-lookup"><span data-stu-id="d5740-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="d5740-115">Une fois hello utilisateur s’authentifie, exemple d’application hello reçoit un jeton qui peut être utilisé tooquery Microsoft Graph API ou une API Web sécurisées par Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="d5740-115">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="d5740-116">API telles que Microsoft Graph requièrent un tooallow jeton accès l’accès aux ressources spécifiques – tooread, par exemple, un profil utilisateur, accéder au calendrier de l’utilisateur ou envoyer un courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="d5740-116">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="d5740-117">Votre application peut demander un jeton d’accès à l’aide de MSAL tooaccess ces ressources en spécifiant des étendues de l’API.</span><span class="sxs-lookup"><span data-stu-id="d5740-117">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="d5740-118">Ce jeton d’accès est ensuite ajouté toohello en-tête d’autorisation HTTP pour chaque appel effectué par rapport à hello une ressource protégée.</span><span class="sxs-lookup"><span data-stu-id="d5740-118">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="d5740-119">MSAL gère la mise en cache et l’actualisation des jetons d’accès pour vous, ce qui évite à votre application d’avoir à le faire.</span><span class="sxs-lookup"><span data-stu-id="d5740-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="d5740-120">Packages NuGet</span><span class="sxs-lookup"><span data-stu-id="d5740-120">NuGet Packages</span></span>

<span data-ttu-id="d5740-121">Ce guide utilise hello suivant les packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="d5740-121">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="d5740-122">Bibliothèque</span><span class="sxs-lookup"><span data-stu-id="d5740-122">Library</span></span>|<span data-ttu-id="d5740-123">Description</span><span class="sxs-lookup"><span data-stu-id="d5740-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="d5740-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="d5740-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="d5740-125">Bibliothèque d’authentification Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="d5740-125">Microsoft Authentication Library (MSAL)</span></span>|

