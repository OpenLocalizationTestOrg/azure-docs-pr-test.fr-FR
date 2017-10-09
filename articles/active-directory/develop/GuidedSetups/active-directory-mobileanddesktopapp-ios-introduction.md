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
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a>Appel hello Microsoft Graph API à partir d’une application iOS

Ce guide montre comment une application iOS native (Swift) peut obtenir un jeton accès et appeler hello API Graph de Microsoft ou d’autres API qui nécessitent des jetons d’accès de point de terminaison Azure Active Directory v2.

À la fin de hello de ce guide, votre application sera être en mesure de toocall API protégée à l’aide des comptes personnels (y compris les outlook.com, live.com et autres) ainsi que de travail et les comptes d’établissement d’une entreprise ou d’une organisation qui dispose d’Azure Active Directory.

> ### <a name="pre-requisites"></a>Conditions préalables
> - XCode 8.x est nécessaire pour ce guide. Vous pouvez télécharger XCode [ici](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "URL de téléchargement de XCode").
> - [Carthage](https://github.com/Carthage/Carthage) pour la gestion des packages

### <a name="how-this-guide-works"></a>Fonctionnement de ce guide

![Fonctionnement de ce guide](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

exemple d’application Hello créé par ce guide permet un hello de tooquery de l’application iOS Microsoft Graph API ou une API Web qui accepte les jetons à partir du point de terminaison Azure Active Directory v2. Pour ce scénario, un jeton est ajouté tooHTTP des demandes via l’en-tête d’autorisation hello. Renouvellement et acquisition de jeton est gérée par hello bibliothèque d’authentification Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Gestion de l’acquisition de jetons pour accéder à des API web protégées

Une fois hello utilisateur s’authentifie, exemple d’application hello reçoit un jeton qui peut être utilisé tooquery hello Microsoft Graph API ou une API Web sécurisées par Microsoft Azure Active Directory v2.

API telles que Microsoft Graph requièrent un tooallow jeton accès l’accès aux ressources spécifiques – tooread, par exemple, un profil utilisateur, accéder au calendrier de l’utilisateur ou envoyer un courrier électronique. Votre application peut demander un jeton d’accès à l’aide de la bibliothèque MSAL en spécifiant les étendues d’API. Ce jeton d’accès est ensuite ajouté toohello en-tête d’autorisation HTTP pour chaque appel effectué par rapport à hello une ressource protégée.

MSAL gère la mise en cache et l’actualisation des jetons d’accès pour vous, ce qui évite à votre application d’avoir à le faire.


### <a name="nuget-packages"></a>Packages NuGet

Ce guide utilise hello suivant les packages NuGet :

|Bibliothèque|Description|
|---|---|
|[MSAL.framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|Préversion de la bibliothèque d’authentification Microsoft pour iOS|

