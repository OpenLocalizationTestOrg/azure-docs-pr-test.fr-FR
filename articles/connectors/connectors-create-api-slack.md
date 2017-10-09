---
title: aaaUse hello Slack connecteur dans vos applications Azure logique | Documents Microsoft
description: Se connecter tooSlack dans vos applications logiques
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a>Prise en main connecteur de marge hello
Slack est un outil de communication collaboratif qui centralise toutes les communications de votre équipe dans un seul emplacement que vous pouvez consulter instantanément, où que vous vous trouviez. 

Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tooslack"></a>Créer un tooSlack de connexion
connecteur de marge hello toouse, tout d’abord créer un **connexion** puis fournissez les informations de hello pour ces propriétés : 

| Propriété | Requis | Description |
| --- | --- | --- |
| Jeton |Oui |Fournir les informations d’identification de Slack |

Suivez ces étapes toosign en marge et la configuration de hello complète de hello Slack **connexion** dans votre application logique :

1. Sélectionnez **Périodicité**
2. Sélectionnez une **Fréquence** et entrez un **Intervalle**
3. Sélectionnez **Ajouter une action**  
   ![Configurer Slack][1]  
4. Entrez une marge dans la zone de recherche hello et hello recherche tooreturn attendre que toutes les entrées avec une marge de nom de hello
5. Sélectionnez **Slack - Publier un message**
6. Sélectionnez **connecter tooSlack**:  
   ![Configurer Slack][2]
7. Fournissez votre toosign les informations d’identification Slack dans l’application de hello tooauthorize    
   ![Configurer Slack][3]  
8. Vous serez page de connexion redirigé tooyour organisation. **Autoriser** marge toointeract avec votre application logique :      
   ![Configurer Slack][5] 
9. Une fois l’autorisation de hello terminée, vous serez redirigé tooyour logique application toocomplete il en configurant hello **marge - obtenir tous les messages** section. Ajouter les autres déclencheurs et actions dont vous avez besoin.  
   ![Configurer Slack][6]
10. Enregistrez votre travail en sélectionnant **enregistrer** sur la barre de menus hello ci-dessus.

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/slack/).

## <a name="more-connectors"></a>Autres connecteurs
Revenir en arrière toohello [liste des API](apis-list.md).

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
