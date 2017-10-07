---
title: connecteur aaaDropbox dans Azure Logic Apps | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. Se connecter tooDropbox toomanage vos fichiers. Vous pouvez exécuter différentes actions, comme charger, mettre à jour, obtenir et supprimer des fichiers dans Dropbox."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a>Prise en main connecteur d’échange hello
Se connecter tooDropbox toomanage vos fichiers. Vous pouvez exécuter différentes actions, comme charger, mettre à jour, obtenir et supprimer des fichiers dans Dropbox.

toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique. Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toodropbox"></a>Se connecter tooDropbox
Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service. Une connexion permet d’assurer la connectivité entre une application logique et un autre service. Par exemple, dans l’ordre tooconnect tooDropbox, vous devez un échange *connexion*. toocreate une connexion, vous aurez besoin des informations d’identification de hello tooprovide que vous utilisez normalement le service de hello tooaccess à que vous souhaitez tooconnect. Par conséquent, dans l’exemple d’échange hello, vous devez tooyour des informations d’identification hello compte Dropbox dans l’ordre toocreate hello connexion tooDropbox. [Apprenez-en davantage sur les connexions]().

### <a name="create-a-connection-toodropbox"></a>Créer un tooDropbox de connexion
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a>Utiliser un déclencheur Dropbox
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique. [En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Dans cet exemple, nous allons utiliser hello **lorsqu’un fichier est créé** déclencheur. Lorsque ce déclencheur se produit, nous appellerons hello **obtenir le contenu du fichier à l’aide du chemin d’accès** action d’échange. 

1. Entrez *dropbox* dans la zone de recherche hello sur le concepteur hello Logic Apps, puis sélectionnez hello **Dropbox - lors de la création d’un fichier** déclencheur.      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. Sélectionnez hello le dossier dans lequel la création du fichier tootrack. Sélectionnez... (identifiées dans la zone de hello rouge) et parcourir toohello dossier tooselect pour déclencheur de hello d’entrée.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a>Utiliser une action Dropbox
Une action est une opération effectuée par flux de travail hello défini dans une application logique. [En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Maintenant que hello déclencheur a été ajouté, suivez ces étapes de tooadd une action qui obtiennent le contenu hello du nouveau fichier.

1. Sélectionnez **+ nouvelle étape** action de hello tooadd vous aimeriez tootake lorsqu’un nouveau fichier est créé.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. Sélectionnez **Ajouter une action**. Cette zone de recherche hello s’ouvre dans laquelle vous pouvez rechercher n’importe quelle action vous aimeriez tootake.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. Entrez *dropbox* toosearch pour tooDropbox connexes d’actions.  
4. Sélectionnez **Dropbox - le contenu du fichier Get à l’aide du chemin d’accès** comme hello action tootake lorsqu’un nouveau fichier est créé dans hello sélectionné de dossier Dropbox. bloc de contrôle d’action Hello s’ouvre. Vous est demandée tooauthorize votre tooaccess d’application logique votre Dropbox compte si vous le n'avez pas fait précédemment.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. Sélectionnez... (situé à droite de hello Hello **chemin d’accès du fichier** contrôle) et de parcourir le chemin d’accès du fichier toohello toouse voulue. Ou, utilisez hello **chemin d’accès du fichier** toospeed de jeton de votre création d’une logique d’application.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. Enregistrez votre travail et créer un nouveau fichier dans Dropbox tooactivate votre flux de travail.  

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/dropbox/).

## <a name="more-connectors"></a>Autres connecteurs
Revenir en arrière toohello [liste des API](apis-list.md).
