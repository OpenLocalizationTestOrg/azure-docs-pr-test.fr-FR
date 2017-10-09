---
title: aaaAzure AD v2 Android prise en main - introduction | Documents Microsoft
description: "Cet article explique comment une application Android peut obtenir un jeton d’accès et appeler une ou plusieurs API Microsoft Graph qui nécessitent des jetons d’accès à partir du point de terminaison Azure Active Directory v2"
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
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="8c911-103">Appel hello Microsoft Graph API à partir d’une application Android</span><span class="sxs-lookup"><span data-stu-id="8c911-103">Call hello Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="8c911-104">Ce guide explique comment une application Android native peut obtenir un jeton d’accès et appeler l’API Microsoft Graph ou d’autres API qui nécessitent des jetons d’accès provenant d’un point de terminaison Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="8c911-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="8c911-105">À la fin de hello de ce guide, votre application sera être en mesure de toocall API protégée à l’aide des comptes personnels (y compris les outlook.com, live.com et autres) ainsi que de travail et les comptes d’établissement d’une entreprise ou d’une organisation qui dispose d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c911-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="8c911-106">Fonctionnement de cet exemple</span><span class="sxs-lookup"><span data-stu-id="8c911-106">How this sample works</span></span>
![Fonctionnement de cet exemple](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="8c911-108">exemple Hello créé par ce guide est basé sur un scénario où une application Android est tooquery utilisé une API Web qui accepte les jetons à partir d’Azure Active Directory v2 endpoint – dans ce cas, l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="8c911-108">hello sample created by this guide is based on a scenario where an Android application is used tooquery a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="8c911-109">Pour ce scénario, un jeton est ajouté tooHTTP des demandes via l’en-tête d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="8c911-109">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="8c911-110">Renouvellement et acquisition de jeton est gérée par hello bibliothèque d’authentification Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="8c911-110">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="8c911-111">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="8c911-111">Pre-requisites</span></span>
* <span data-ttu-id="8c911-112">Cette installation guidée se concentre sur Android Studio, mais n’importe quel autre environnement de développement d’application Android peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="8c911-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="8c911-113">Le Kit de développement logiciel (SDK) Android 21 ou version ultérieure est requis (Kit de développement logiciel (SDK) 25 recommandé).</span><span class="sxs-lookup"><span data-stu-id="8c911-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="8c911-114">Google Chrome ou un navigateur web utilisant les onglets personnalisés est requis pour cette version de Microsoft Authentication Library (MSAL) pour Android.</span><span class="sxs-lookup"><span data-stu-id="8c911-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="8c911-115">Remarque : Google Chrome n’est pas inclus dans l’émulateur Visual Studio pour Android.</span><span class="sxs-lookup"><span data-stu-id="8c911-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="8c911-116">Nous vous recommandons de vous tootest ce code sur un émulateur avec une API 25 ou une image avec les API 21 ou plus récente qui a installé avec Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="8c911-116">We recommend you tootest this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a><span data-ttu-id="8c911-117">Comment toohandle jeton acquisition tooaccess une API Web protégé</span><span class="sxs-lookup"><span data-stu-id="8c911-117">How toohandle token acquisition tooaccess a protected Web API</span></span>

<span data-ttu-id="8c911-118">Une fois hello utilisateur s’authentifie, exemple d’application hello reçoit un jeton qui peut être utilisé tooquery Microsoft Graph API ou une API Web sécurisées par Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="8c911-118">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="8c911-119">API telles que Microsoft Graph requièrent un tooallow jeton accès l’accès aux ressources spécifiques – tooread, par exemple, un profil utilisateur, accéder au calendrier de l’utilisateur ou envoyer un courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="8c911-119">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="8c911-120">Votre application peut demander un jeton d’accès à l’aide de MSAL tooaccess ces ressources en spécifiant des étendues de l’API.</span><span class="sxs-lookup"><span data-stu-id="8c911-120">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="8c911-121">Ce jeton d’accès est ensuite ajouté toohello en-tête d’autorisation HTTP pour chaque appel effectué par rapport à hello une ressource protégée.</span><span class="sxs-lookup"><span data-stu-id="8c911-121">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="8c911-122">MSAL gère la mise en cache et l’actualisation des jetons d’accès pour vous, ce qui évite à votre application d’avoir à le faire.</span><span class="sxs-lookup"><span data-stu-id="8c911-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="8c911-123">Bibliothèques</span><span class="sxs-lookup"><span data-stu-id="8c911-123">Libraries</span></span>

<span data-ttu-id="8c911-124">Ce guide utilise hello suivant bibliothèques :</span><span class="sxs-lookup"><span data-stu-id="8c911-124">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="8c911-125">Bibliothèque</span><span class="sxs-lookup"><span data-stu-id="8c911-125">Library</span></span>|<span data-ttu-id="8c911-126">Description</span><span class="sxs-lookup"><span data-stu-id="8c911-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="8c911-127">com.microsoft.identity.client</span><span class="sxs-lookup"><span data-stu-id="8c911-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="8c911-128">Bibliothèque d’authentification Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="8c911-128">Microsoft Authentication Library (MSAL)</span></span>|
