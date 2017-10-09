---
title: "Azure App Service : Mise à l’échelle des applications d’App Service"
description: "Découvrez hello coulisses de mise à l’échelle d’Application dans le Service d’applications."
keywords: "app service, azure app service, mise à l'échelle, évolutif, plan app service, coût d'app service"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Azure App Service : Mise à l’échelle des applications d’App Service
Les applications hébergées dans Azure App Service peuvent [être mises à l’échelle massivement](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
Toutefois, la mise à l’échelle d’une application est un problème complexe pour lequel il n’existe pas de solution universelle. toocorrectly l’échelle votre application il existe 3 domaines clés qui contribueront réussite des applications tooyour :

1. Comprendre l’architecture de votre application et ses faiblesses.
   * Votre application est-elle avec état ? Sans état ?
   * Quels sont les composants hello de votre application ?
     * Où sont les goulots d’étranglement de hello dans l’application hello ?
   * Lorsque la charge est appliquée tooyour application, ce qui interrompt premier ?
2. Hello de présentation des attendu des exigences de performances et de charge.
   * Application hello doit-elle tooserve mille utilisateurs ? ou d’un million ?
   * Le trafic provient-il d’un seul emplacement géographique ou du monde entier ?
   * Existe-t-il des variations saisonnières ? Des pics de trafic ?
   * La vitesse à laquelle l’application hello doit répondre ? 1 seconde ? 1 milliseconde ?
3. Présentation et correctement tirer parti de la plateforme de hello qui héberge votre application.
   * Les fonctionnalités doivent exploiter tooachieve mes objectifs de mise à l’échelle ?

Cette section vous aidera à comprendre tous les facteurs de hello et aide vous concevoir une stratégie qui tire parti de hello nécessaires du Service d’applications fonctionnalités tooachieve vos objectifs d’évolutivité.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

