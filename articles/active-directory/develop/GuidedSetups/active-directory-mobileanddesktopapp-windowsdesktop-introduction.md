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
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a>Appel hello Microsoft Graph API à partir d’une application de bureau Windows

Ce guide explique comment une application de bureau Windows .NET (XAML) native peut obtenir un jeton d’accès et appeler l’API Microsoft Graph ou d’autres API qui nécessitent des jetons d’accès provenant d’un point de terminaison Azure Active Directory v2.

À la fin de hello de ce guide, votre application sera être en mesure de toocall API protégée à l’aide des comptes personnels (y compris les outlook.com, live.com et autres) ainsi que de travail et les comptes d’établissement d’une entreprise ou d’une organisation qui dispose d’Azure Active Directory.  

> Ce guide requiert Visual Studio 2015 Update 3 ou Visual Studio 2017.  Ni l’un, ni l’autre ne sont installés sur votre ordinateur ? [Téléchargez gratuitement Visual Studio 2017](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a>Fonctionnement de ce guide

![Fonctionnement de ce guide](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

Hello exemple d’application créé par ce guide permet à une Application de bureau Windows de tooquery Microsoft Graph API ou une API Web qui accepte les jetons à partir du point de terminaison Azure Active Directory v2. Pour ce scénario, un jeton est ajouté tooHTTP des demandes via l’en-tête d’autorisation hello. Renouvellement et acquisition de jeton est gérée par hello bibliothèque d’authentification Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Gestion de l’acquisition de jetons pour accéder à des API web protégées

Une fois hello utilisateur s’authentifie, exemple d’application hello reçoit un jeton qui peut être utilisé tooquery Microsoft Graph API ou une API Web sécurisées par Microsoft Azure Active Directory v2.

API telles que Microsoft Graph requièrent un tooallow jeton accès l’accès aux ressources spécifiques – tooread, par exemple, un profil utilisateur, accéder au calendrier de l’utilisateur ou envoyer un courrier électronique. Votre application peut demander un jeton d’accès à l’aide de MSAL tooaccess ces ressources en spécifiant des étendues de l’API. Ce jeton d’accès est ensuite ajouté toohello en-tête d’autorisation HTTP pour chaque appel effectué par rapport à hello une ressource protégée. 

MSAL gère la mise en cache et l’actualisation des jetons d’accès pour vous, ce qui évite à votre application d’avoir à le faire.


### <a name="nuget-packages"></a>Packages NuGet

Ce guide utilise hello suivant les packages NuGet :

|Bibliothèque|Description|
|---|---|
|[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client)|Bibliothèque d’authentification Microsoft (MSAL)|

