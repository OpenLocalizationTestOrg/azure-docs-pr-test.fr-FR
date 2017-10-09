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
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Hello d’appel d’une Application de Page unique (SPA) JavaScript de l’API Microsoft Graph

Ce guide montre comment une Application de Page unique (SPA) de JavaScript peut se connecter, personnelles et comptes d’établissement scolaire, obtenir un jeton d’accès et appeler hello API Graph de Microsoft ou d’autres API qui nécessitent des jetons d’accès de hello de point de terminaison Azure Active Directory v2.

### <a name="how-this-guide-works"></a>Fonctionnement de ce guide

![Fonctionne de l’application d’exemple hello générée par ce guide](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Informations complémentaires

exemple d’application Hello créé par ce guide permet un Bonjour de tooquery Microsoft Graph API JavaScript SPA ou une API Web qui accepte les jetons à partir du point de terminaison Azure Active Directory v2. Pour ce scénario, après qu’un utilisateur se connecte en, un jeton d’accès est demandé et ajouté tooHTTP des demandes via l’en-tête d’autorisation hello. Renouvellement et acquisition de jeton sont gérés par hello bibliothèque d’authentification Microsoft (MSAL).

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Bibliothèques

Ce guide utilise hello suivant bibliothèque :

|Bibliothèque|Description|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Bibliothèque d’authentification Microsoft pour JavaScript Preview|

> [!NOTE]
> *msal.js* hello de cibles *point de terminaison Azure Active Directory v2* -qui permet de toosign comptes personnels, l’école et professionnels dans et acquérir des jetons. Hello *point de terminaison Azure Active Directory v2* a [certaines limitations](..\active-directory-v2-limitations.md). Si vous êtes uniquement intéressé par les comptes de l’école et professionnelles, utilisez *adal.js* et hello *V1 de point de terminaison*. toounderstand les différences entre les points de terminaison hello v1 et v2 lire hello [v1-v2 comparaison](..\active-directory-v2-compare.md).

<!--end-collapse-->
