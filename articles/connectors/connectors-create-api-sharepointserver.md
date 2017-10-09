---
title: aaaUse hello connecteur du serveur SharePoint dans vos applications logiques | Documents Microsoft
description: Prise en main Bonjour Bonjour SharePoint Server Connector dans vos applications logiques
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a>Prise en main connecteur de SharePoint hello
Hello connecteur SharePoint fournit un toowork de façon avec les listes sur SharePoint.

Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-toosharepoint"></a>Créer un tooSharePoint de connexion
toouse hello connecteur de SharePoint, vous commencez par créer un **connexion** puis fournissez les informations de hello pour ces propriétés : 

| Propriété | Requis | Description |
| --- | --- | --- |
| Jeton |Oui |Fournir les informations d’identification SharePoint |

tooconnect trop**SharePoint**, entrez votre tooSharePoint d’identité (nom d’utilisateur et mot de passe, informations d’identification de carte à puce, etc.). Une fois que vous avez été authentifié, vous pouvez passer le connecteur de SharePoint toouse hello dans votre application logique. 

Tandis que sur le Concepteur de hello de votre application logique, suivez ces toosign étapes dans une connexion SharePoint toocreate hello **connexion** pour une utilisation dans votre application logique :

1. Entrez SharePoint dans la zone de recherche hello et attendre que toutes les entrées avec SharePoint dans le nom de hello hello recherche tooreturn :   
   ![Configurer SharePoint][1]  
2. Sélectionner **SharePoint - Quand un fichier est créé**   
3. Sélectionnez **connecter tooSharePoint**:   
   ![Configurer SharePoint][2]    
4. Fournissez votre toosign d’informations d’identification SharePoint dans tooauthenticate avec SharePoint   
   ![Configurer SharePoint][3]     
5. Une fois l’authentification de hello est terminée, vous serez redirigé tooyour logique application toocomplete par la configuration de SharePoint **lorsqu’un fichier est créé** boîte de dialogue.          
   ![Configurer SharePoint][4]  
6. Vous pouvez ensuite ajouter d’autres déclencheurs et les actions que vous devez toocomplete votre application logique.   
7. Enregistrez votre travail en sélectionnant **enregistrer** sur la barre de menus hello ci-dessus.  

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/sharepoint/).

## <a name="more-connectors"></a>Autres connecteurs
Revenir en arrière toohello [liste des API](apis-list.md).

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
