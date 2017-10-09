---
title: "aaaAzure AD v2 JS SPA guidée par le programme d’installation - introduction | Documents Microsoft"
description: "Comment les applications JavaScript SPA peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="3cbdb-103">Hello d’appel d’une Application de Page unique (SPA) JavaScript de l’API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="3cbdb-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="3cbdb-104">Ce guide montre comment une Application de Page unique (SPA) de JavaScript peut se connecter, personnelles et comptes d’établissement scolaire, obtenir un jeton d’accès et appeler hello API Graph de Microsoft ou d’autres API qui nécessitent des jetons d’accès de hello de point de terminaison Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="3cbdb-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="3cbdb-105">Fonctionnement de ce guide</span><span class="sxs-lookup"><span data-stu-id="3cbdb-105">How this guide works</span></span>

![Fonctionne de l’application d’exemple hello générée par ce guide](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="3cbdb-107">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="3cbdb-107">More Information</span></span>

<span data-ttu-id="3cbdb-108">exemple d’application Hello créé par ce guide permet un Bonjour de tooquery Microsoft Graph API JavaScript SPA ou une API Web qui accepte les jetons à partir du point de terminaison Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="3cbdb-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="3cbdb-109">Pour ce scénario, après qu’un utilisateur se connecte en, un jeton d’accès est demandé et ajouté tooHTTP des demandes via l’en-tête d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="3cbdb-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="3cbdb-110">Renouvellement et acquisition de jeton sont gérés par hello bibliothèque d’authentification Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="3cbdb-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="3cbdb-111">Bibliothèques</span><span class="sxs-lookup"><span data-stu-id="3cbdb-111">Libraries</span></span>

<span data-ttu-id="3cbdb-112">Ce guide utilise hello suivant bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="3cbdb-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="3cbdb-113">Bibliothèque</span><span class="sxs-lookup"><span data-stu-id="3cbdb-113">Library</span></span>|<span data-ttu-id="3cbdb-114">Description</span><span class="sxs-lookup"><span data-stu-id="3cbdb-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="3cbdb-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="3cbdb-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="3cbdb-116">Bibliothèque d’authentification Microsoft pour JavaScript Preview</span><span class="sxs-lookup"><span data-stu-id="3cbdb-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="3cbdb-117">*msal.js* hello de cibles *point de terminaison Azure Active Directory v2* -qui permet de toosign comptes personnels, l’école et professionnels dans et acquérir des jetons.</span><span class="sxs-lookup"><span data-stu-id="3cbdb-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="3cbdb-118">Hello *point de terminaison Azure Active Directory v2* a [certaines limitations](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3cbdb-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="3cbdb-119">Si vous êtes uniquement intéressé par les comptes de l’école et professionnelles, utilisez *adal.js* et hello *V1 de point de terminaison*.</span><span class="sxs-lookup"><span data-stu-id="3cbdb-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="3cbdb-120">toounderstand les différences entre les points de terminaison hello v1 et v2 lire hello [v1-v2 comparaison](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="3cbdb-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
