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
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>Appel hello Microsoft Graph API à partir d’une application Android

Ce guide explique comment une application Android native peut obtenir un jeton d’accès et appeler l’API Microsoft Graph ou d’autres API qui nécessitent des jetons d’accès provenant d’un point de terminaison Azure Active Directory v2.

À la fin de hello de ce guide, votre application sera être en mesure de toocall API protégée à l’aide des comptes personnels (y compris les outlook.com, live.com et autres) ainsi que de travail et les comptes d’établissement d’une entreprise ou d’une organisation qui dispose d’Azure Active Directory.  

### <a name="how-this-sample-works"></a>Fonctionnement de cet exemple
![Fonctionnement de cet exemple](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

exemple Hello créé par ce guide est basé sur un scénario où une application Android est tooquery utilisé une API Web qui accepte les jetons à partir d’Azure Active Directory v2 endpoint – dans ce cas, l’API Graph. Pour ce scénario, un jeton est ajouté tooHTTP des demandes via l’en-tête d’autorisation hello. Renouvellement et acquisition de jeton est gérée par hello bibliothèque d’authentification Microsoft (MSAL).

### <a name="pre-requisites"></a>Conditions préalables
* Cette installation guidée se concentre sur Android Studio, mais n’importe quel autre environnement de développement d’application Android peut être utilisé. 
* Le Kit de développement logiciel (SDK) Android 21 ou version ultérieure est requis (Kit de développement logiciel (SDK) 25 recommandé).
* Google Chrome ou un navigateur web utilisant les onglets personnalisés est requis pour cette version de Microsoft Authentication Library (MSAL) pour Android.

> Remarque : Google Chrome n’est pas inclus dans l’émulateur Visual Studio pour Android. Nous vous recommandons de vous tootest ce code sur un émulateur avec une API 25 ou une image avec les API 21 ou plus récente qui a installé avec Google Chrome.


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>Comment toohandle jeton acquisition tooaccess une API Web protégé

Une fois hello utilisateur s’authentifie, exemple d’application hello reçoit un jeton qui peut être utilisé tooquery Microsoft Graph API ou une API Web sécurisées par Microsoft Azure Active Directory v2.

API telles que Microsoft Graph requièrent un tooallow jeton accès l’accès aux ressources spécifiques – tooread, par exemple, un profil utilisateur, accéder au calendrier de l’utilisateur ou envoyer un courrier électronique. Votre application peut demander un jeton d’accès à l’aide de MSAL tooaccess ces ressources en spécifiant des étendues de l’API. Ce jeton d’accès est ensuite ajouté toohello en-tête d’autorisation HTTP pour chaque appel effectué par rapport à hello une ressource protégée. 

MSAL gère la mise en cache et l’actualisation des jetons d’accès pour vous, ce qui évite à votre application d’avoir à le faire.

### <a name="libraries"></a>Bibliothèques

Ce guide utilise hello suivant bibliothèques :

|Bibliothèque|Description|
|---|---|
|[com.microsoft.identity.client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Bibliothèque d’authentification Microsoft (MSAL)|
