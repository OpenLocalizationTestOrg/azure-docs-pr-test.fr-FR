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
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>Ajouter la connexion à l’aide de l’application web ASP.NET tooan Microsoft

Ce guide montre comment tooimplement connectez-vous avec Microsoft à l’aide d’une solution ASP.NET MVC avec une application web classique basée sur navigateur, à l’aide de OpenID Connect. 

À la fin de hello de ce guide, votre application sera ins du personnel des comptes (y compris les outlook.com, live.com et autres) ainsi que comment utiliser l’authentification en mesure de tooaccept comptes professionnels et scolaires à partir de toute entreprise ou d’une organisation qui a intégré à Azure Active Directory. 

> Ce guide requiert Visual Studio 2015 Update 3 ou Visual Studio 2017.  Ni l’un, ni l’autre ne sont installés sur votre ordinateur ?  [Téléchargez gratuitement Visual Studio 2017](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>Fonctionnement de ce guide

![Fonctionnement de ce guide](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

Ce guide se base sur le scénario hello où un navigateur accède à un site web ASP.NET, demande un tooauthenticate utilisateur via un bouton de connexion. Dans ce scénario, la majeure partie de la page web de hello travail toorender hello se produit côté serveur de hello.

## <a name="libraries"></a>Bibliothèques

Ce guide utilise hello suivant bibliothèques :

|Bibliothèque|Description|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|Intergiciel (middleware) qui permet à une application de toouse OpenIdConnect pour l’authentification|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|Intergiciel (middleware) qui permet à une session d’utilisateur toomaintain application à l’aide de cookies|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|Permet de toorun des applications OWIN sur IIS à l’aide du pipeline de demande ASP.NET hello|

