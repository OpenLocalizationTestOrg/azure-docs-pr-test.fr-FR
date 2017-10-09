---
title: aaaAzure AD v2 ASP.NET Web Server mise en route - introduction | Documents Microsoft
description: "Implémentation de la connexion Microsoft dans une solution ASP.NET avec une application basée sur un navigateur web traditionnel utilisant le standard OpenID Connect"
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="1af1b-103">Ajouter la connexion à l’aide de l’application web ASP.NET tooan Microsoft</span><span class="sxs-lookup"><span data-stu-id="1af1b-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="1af1b-104">Ce guide montre comment tooimplement connectez-vous avec Microsoft à l’aide d’une solution ASP.NET MVC avec une application web classique basée sur navigateur, à l’aide de OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="1af1b-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="1af1b-105">À la fin de hello de ce guide, votre application sera ins du personnel des comptes (y compris les outlook.com, live.com et autres) ainsi que comment utiliser l’authentification en mesure de tooaccept comptes professionnels et scolaires à partir de toute entreprise ou d’une organisation qui a intégré à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1af1b-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="1af1b-106">Ce guide requiert Visual Studio 2015 Update 3 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1af1b-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="1af1b-107">Ni l’un, ni l’autre ne sont installés sur votre ordinateur ?</span><span class="sxs-lookup"><span data-stu-id="1af1b-107">Don’t have it?</span></span>  [<span data-ttu-id="1af1b-108">Téléchargez gratuitement Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1af1b-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="1af1b-109">Fonctionnement de ce guide</span><span class="sxs-lookup"><span data-stu-id="1af1b-109">How this guide works</span></span>

![Fonctionnement de ce guide](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="1af1b-111">Ce guide se base sur le scénario hello où un navigateur accède à un site web ASP.NET, demande un tooauthenticate utilisateur via un bouton de connexion.</span><span class="sxs-lookup"><span data-stu-id="1af1b-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="1af1b-112">Dans ce scénario, la majeure partie de la page web de hello travail toorender hello se produit côté serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="1af1b-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="1af1b-113">Bibliothèques</span><span class="sxs-lookup"><span data-stu-id="1af1b-113">Libraries</span></span>

<span data-ttu-id="1af1b-114">Ce guide utilise hello suivant bibliothèques :</span><span class="sxs-lookup"><span data-stu-id="1af1b-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="1af1b-115">Bibliothèque</span><span class="sxs-lookup"><span data-stu-id="1af1b-115">Library</span></span>|<span data-ttu-id="1af1b-116">Description</span><span class="sxs-lookup"><span data-stu-id="1af1b-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="1af1b-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="1af1b-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="1af1b-118">Intergiciel (middleware) qui permet à une application de toouse OpenIdConnect pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="1af1b-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="1af1b-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="1af1b-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="1af1b-120">Intergiciel (middleware) qui permet à une session d’utilisateur toomaintain application à l’aide de cookies</span><span class="sxs-lookup"><span data-stu-id="1af1b-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="1af1b-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="1af1b-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="1af1b-122">Permet de toorun des applications OWIN sur IIS à l’aide du pipeline de demande ASP.NET hello</span><span class="sxs-lookup"><span data-stu-id="1af1b-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|

