---
title: Connecteur GitHub dans Azure Logic Apps | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. GitHub est un servie d’hébergement de dépôt Git sur le web. Il offre toutes les fonctionnalités distribuées de contrôle de révision et de gestion du code source (SCM) de Git, ainsi que ses propres fonctionnalités."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a>Prise en main du connecteur GitHub
GitHub est un servie d’hébergement de dépôt Git sur le web. Il offre toutes les fonctionnalités distribuées de contrôle de révision et de gestion du code source (SCM) de Git, ainsi que ses propres fonctionnalités.

Vous pouvez commencer par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-to-github"></a>Créer une connexion à GitHub
Pour créer des applications logiques avec GitHub, vous devez d’abord créer une **connexion**, puis fournir les détails pour les propriétés suivantes : 

| Propriété | Requis | Description |
| --- | --- | --- |
| Jeton |Oui |Fournir des informations d’identification GitHub |

Après avoir créé la connexion, vous pouvez l’utiliser pour exécuter les actions et écouter les déclencheurs décrits dans cet article. 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a>Détails spécifiques aux connecteurs

Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/github/).

## <a name="more-connectors"></a>Autres connecteurs
Revenir à la [liste des API](apis-list.md).