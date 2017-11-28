---
title: Prise en main du serveur web ASP.NET Azure AD v2 - Intro | Microsoft Docs
description: "Implémentation de la connexion Microsoft sur une solution ASP.NET avec une application basée sur un navigateur web traditionnel avec une norme OpenID Connect"
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
ms.openlocfilehash: 8062923b6270ec6253dc231a3db4333cf4666b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a><span data-ttu-id="6259d-103">Ajouter la connexion avec Microsoft à une application ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6259d-103">Add sign-in with Microsoft to an ASP.NET web app</span></span>

<span data-ttu-id="6259d-104">Ce guide explique comment implémenter la connexion avec Microsoft à l’aide d’une solution ASP.NET MVC avec une application basée sur un navigateur web traditionnel avec une norme OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="6259d-104">This guide demonstrates how to implement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="6259d-105">À la fin de ce guide, votre application pourra accepter des connexions de comptes personnels (y compris outlook.com, live.com et autres), ainsi que des comptes professionnels et scolaires de n’importe quelle société ou organisation ayant intégré Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6259d-105">At the end of this guide, your application will be able to accept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="6259d-106">Ce guide requiert Visual Studio 2015 Update 3 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6259d-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="6259d-107">Ni l’un, ni l’autre ne sont installés sur votre ordinateur ?</span><span class="sxs-lookup"><span data-stu-id="6259d-107">Don’t have it?</span></span>  [<span data-ttu-id="6259d-108">Téléchargez gratuitement Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6259d-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="6259d-109">Fonctionnement de ce guide</span><span class="sxs-lookup"><span data-stu-id="6259d-109">How this guide works</span></span>

![Comment fonctionne ce guide](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="6259d-111">Ce guide est basé sur des scénarios dans lesquels un navigateur accède à un site web ASP.NET, invitant un utilisateur à s’authentifier via un bouton de connexion.</span><span class="sxs-lookup"><span data-stu-id="6259d-111">This guide is based on the scenario where a browser accesses an ASP.NET web site, requesting a user to authenticate via a sign-in button.</span></span> <span data-ttu-id="6259d-112">Dans ce scénario, la majorité du travail pour afficher la page web se passe côté serveur.</span><span class="sxs-lookup"><span data-stu-id="6259d-112">In this scenario, most of the work to render the web page occurs on the server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="6259d-113">Bibliothèques</span><span class="sxs-lookup"><span data-stu-id="6259d-113">Libraries</span></span>

<span data-ttu-id="6259d-114">Ce guide utilise les bibliothèques suivantes :</span><span class="sxs-lookup"><span data-stu-id="6259d-114">This guide uses the following libraries:</span></span>

|<span data-ttu-id="6259d-115">Bibliothèque</span><span class="sxs-lookup"><span data-stu-id="6259d-115">Library</span></span>|<span data-ttu-id="6259d-116">Description</span><span class="sxs-lookup"><span data-stu-id="6259d-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="6259d-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="6259d-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="6259d-118">Intergiciel qui permet à une application d’utiliser OpenIDConnect pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="6259d-118">Middleware that enables an application to use OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="6259d-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="6259d-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="6259d-120">Intergiciel qui permet à une application de maintenir la session utilisateur à l’aide de cookies.</span><span class="sxs-lookup"><span data-stu-id="6259d-120">Middleware that enables an application to maintain user session using cookies</span></span>|
|[<span data-ttu-id="6259d-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="6259d-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="6259d-122">Permet aux applications basées sur OWIN de s’exécuter sur IIS à l’aide du pipeline de requête ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6259d-122">Enables OWIN-based applications to run on IIS using the ASP.NET request pipeline</span></span>|

