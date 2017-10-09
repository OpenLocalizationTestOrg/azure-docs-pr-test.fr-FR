---
title: aaaOverview de Azure sans serveur | Documents Microsoft
description: "Créer des solutions puissantes dans le cloud de hello sans avoir toothink sur l’infrastructure."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 7c9c09d96e472edd1631892982ac60aae97342a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-serverless-with-functions-and-logic-apps"></a>Vue d’ensemble d’une application sans serveur dans Azure avec Functions et Logic Apps

Les applications sans serveur offrent les avantages suivants : augmentation de la vitesse de développement, réduction de code requis et simplicité de mise à l’échelle.  Cet article sont stockées dans des attributs différents hello de solutions sans serveur et des offres sans serveur Azure.

## <a name="what-is-serverless"></a>Que sont les environnements sans serveur ?

Aucun serveur - il signifie simplement développeur de hello n’a pas tooworry sur les serveurs ne signifie pas sans serveur.  Une grande partie du développement d’applications traditionnelles est répondre aux questions concernant la mise à l’échelle, l’hébergement et la surveillance des solutions toomeet hello de l’application hello.  Avec sans serveur, ces questions sont pris en charge dans le cadre de la solution de hello.  En outre, les applications sans serveur sont facturées en fonction de la consommation.  Si l’application hello n’est jamais utilisée, frais n’est jamais générée.  Ces fonctionnalités permettent aux développeurs toofocus uniquement sur une logique métier hello de solution de hello.

les services de base Hello dans Azure autour sans serveur sont [Azure fonctions](https://azure.microsoft.com/services/functions/) et [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).  Ces deux solutions suivent les principes hello ci-dessus et permettent aux développeurs toobuild des applications de cloud fiable avec un minimum de code.

## <a name="what-are-azure-functions"></a>Qu’est-ce qu’Azure Functions ?

Les fonctions Azure est une solution pour exécuter facilement des petits éléments de code, ou « fonctions » dans le cloud de hello. Vous pouvez écrire du code de hello simplement que vous avez besoin pour hello problème, sans se préoccuper un ensemble toorun d’infrastructure application ou hello il. Grâce à Functions, le développement gagne en productivité et vous pouvez utiliser votre langage de développement préféré, tel que C#, F#, Node.js, Python ou PHP. Payez uniquement pour le moment hello que votre code s’exécute et Azure peut évoluer en fonction des besoins.

Si vous souhaitez toojump droite dans et prise en main des fonctions de Azure, commencez par [créer votre première fonction Azure](../azure-functions/functions-create-first-azure-function.md). Si vous recherchez des informations techniques supplémentaires sur les fonctions, consultez hello [référence du développeur](../azure-functions/functions-reference.md).

## <a name="what-are-azure-logic-apps"></a>Qu’est-ce qu’Azure Logic Apps ?

Azure Logic Apps fournit un moyen toosimplify et implémenter des intégrations évolutives et flux de travail dans le cloud de hello. Il fournit un toomodel concepteur visuel et automatiser votre processus comme une série d’étapes appelé un flux de travail.  Il n’y [de connecteurs](../connectors/apis-list.md) sur les services cloud et locales tooquickly se connecter à un tooother sans application API.  Une application logique commence par un déclencheur (par exemple, « quand un compte est ajouté tooDynamics CRM ») et après le déclenchement de l’événement peut commencer plusieurs actions de combinaisons, conversions et la logique de la condition.  Logique d’applications est un bon choix lors de l’orchestration de différentes fonctions d’Azure dans un processus - en particulier lorsque les processus hello requiert interagissent avec un système externe ou une API.

tooget en main de Logic Apps, commencez par [créer votre première application logique](logic-apps-create-a-logic-app.md).  Si vous recherchez des informations techniques supplémentaires sur Logic Apps, consultez hello [référence du développeur](logic-apps-workflow-actions-triggers.md).

## <a name="how-can-i-build-and-deploy-serverless-applications-in-azure"></a>Comment puis-je créer et déployer des applications sans serveur dans Azure ?

Azure fournit un ensemble complet d’outils pour le développement, le déploiement et la gestion des applications sans serveur.  Les applications peuvent être construites directement dans hello portail Azure, ou avec [pour les outils à partir de Visual Studio](logic-apps-serverless-get-started-vs.md).  Une fois qu’une application a été développée, elle peut être [déployée immédiatement](logic-apps-create-deploy-template.md).  Azure fournit également une surveillance pour les applications sans serveur.  Cette analyse est accessible à partir de la hello portail Azure, via les API hello ou les kits de développement logiciel, ou avec des outils intégrés tooOMS et Application Insights.

## <a name="next-steps"></a>Étapes suivantes

* [Prise en main de la création d’une application sans serveur dans Visual Studio](logic-apps-serverless-get-started-vs.md)
* [Création d’un tableau de bord des insights client sans serveur](logic-apps-scenario-social-serverless.md)
* [Création d’un modèle de déploiement pour une application logique](logic-apps-create-deploy-template.md)