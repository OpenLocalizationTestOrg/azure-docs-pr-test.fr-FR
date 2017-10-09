---
title: aaaAzure AD v2 iOS route - introduction | Documents Microsoft
description: "Cet article explique comment les applications iOS (Swift) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a><span data-ttu-id="df737-103">Appel hello Microsoft Graph API à partir d’une application iOS</span><span class="sxs-lookup"><span data-stu-id="df737-103">Call hello Microsoft Graph API from an iOS app</span></span>

<span data-ttu-id="df737-104">Ce guide montre comment une application iOS native (Swift) peut obtenir un jeton accès et appeler hello API Graph de Microsoft ou d’autres API qui nécessitent des jetons d’accès de point de terminaison Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="df737-104">This guide demonstrates how a native iOS application (Swift) can get an access token and call hello Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="df737-105">À la fin de hello de ce guide, votre application sera être en mesure de toocall API protégée à l’aide des comptes personnels (y compris les outlook.com, live.com et autres) ainsi que de travail et les comptes d’établissement d’une entreprise ou d’une organisation qui dispose d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df737-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>

> ### <a name="pre-requisites"></a><span data-ttu-id="df737-106">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="df737-106">Pre-requisites</span></span>
> - <span data-ttu-id="df737-107">XCode 8.x est nécessaire pour ce guide.</span><span class="sxs-lookup"><span data-stu-id="df737-107">XCode 8.x is required for this guide.</span></span> <span data-ttu-id="df737-108">Vous pouvez télécharger XCode [ici](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "URL de téléchargement de XCode").</span><span class="sxs-lookup"><span data-stu-id="df737-108">You can download XCode [from here](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode Download URL").</span></span>
> - <span data-ttu-id="df737-109">[Carthage](https://github.com/Carthage/Carthage) pour la gestion des packages</span><span class="sxs-lookup"><span data-stu-id="df737-109">[Carthage](https://github.com/Carthage/Carthage) for package management</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="df737-110">Fonctionnement de ce guide</span><span class="sxs-lookup"><span data-stu-id="df737-110">How this guide works</span></span>

![Fonctionnement de ce guide](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

<span data-ttu-id="df737-112">exemple d’application Hello créé par ce guide permet un hello de tooquery de l’application iOS Microsoft Graph API ou une API Web qui accepte les jetons à partir du point de terminaison Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="df737-112">hello sample application created by this guide enables an iOS application tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="df737-113">Pour ce scénario, un jeton est ajouté tooHTTP des demandes via l’en-tête d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="df737-113">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="df737-114">Renouvellement et acquisition de jeton est gérée par hello bibliothèque d’authentification Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="df737-114">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="df737-115">Gestion de l’acquisition de jetons pour accéder à des API web protégées</span><span class="sxs-lookup"><span data-stu-id="df737-115">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="df737-116">Une fois hello utilisateur s’authentifie, exemple d’application hello reçoit un jeton qui peut être utilisé tooquery hello Microsoft Graph API ou une API Web sécurisées par Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="df737-116">After hello user authenticates, hello sample application receives a token that can be used tooquery hello Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="df737-117">API telles que Microsoft Graph requièrent un tooallow jeton accès l’accès aux ressources spécifiques – tooread, par exemple, un profil utilisateur, accéder au calendrier de l’utilisateur ou envoyer un courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="df737-117">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="df737-118">Votre application peut demander un jeton d’accès à l’aide de la bibliothèque MSAL en spécifiant les étendues d’API.</span><span class="sxs-lookup"><span data-stu-id="df737-118">Your application can request an access token using MSAL by specifying API scopes.</span></span> <span data-ttu-id="df737-119">Ce jeton d’accès est ensuite ajouté toohello en-tête d’autorisation HTTP pour chaque appel effectué par rapport à hello une ressource protégée.</span><span class="sxs-lookup"><span data-stu-id="df737-119">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span>

<span data-ttu-id="df737-120">MSAL gère la mise en cache et l’actualisation des jetons d’accès pour vous, ce qui évite à votre application d’avoir à le faire.</span><span class="sxs-lookup"><span data-stu-id="df737-120">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="df737-121">Packages NuGet</span><span class="sxs-lookup"><span data-stu-id="df737-121">NuGet packages</span></span>

<span data-ttu-id="df737-122">Ce guide utilise hello suivant les packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="df737-122">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="df737-123">Bibliothèque</span><span class="sxs-lookup"><span data-stu-id="df737-123">Library</span></span>|<span data-ttu-id="df737-124">Description</span><span class="sxs-lookup"><span data-stu-id="df737-124">Description</span></span>|
|---|---|
|[<span data-ttu-id="df737-125">MSAL.framework</span><span class="sxs-lookup"><span data-stu-id="df737-125">MSAL.framework</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|<span data-ttu-id="df737-126">Préversion de la bibliothèque d’authentification Microsoft pour iOS</span><span class="sxs-lookup"><span data-stu-id="df737-126">Microsoft Authentication Library Preview for iOS</span></span>|

