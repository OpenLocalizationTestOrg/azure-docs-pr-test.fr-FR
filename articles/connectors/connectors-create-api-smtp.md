---
title: connecteur aaaSMTP dans Azure Logic Apps | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. Se connecter tooSMTP toosend e-mail."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a>Prise en main connecteur hello
Se connecter tooSMTP toosend e-mail.

toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique. Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosmtp"></a>Se connecter tooSMTP
Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service. Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service. Par exemple, tooconnect tooSMTP, vous devez d’abord un SMTP *connexion*. toocreate une connexion, entrez des informations d’identification de hello que vous utilisez normalement le service de hello tooaccess vous vous connectez à. Par conséquent, dans l’exemple de hello SMTP, entrez tooSMTP de la connexion utilisateur connexion informations toocreate hello, adresse du serveur SMTP et nom de connexion tooyour hello informations d’identification.  

### <a name="create-a-connection-toosmtp"></a>Créer un tooSMTP de connexion
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a>Utiliser un déclencheur SMTP
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique. [En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Dans cet exemple, étant donné que SMTP n’a pas un déclencheur qui lui sont propres, nous allons utiliser hello **Salesforce - lors de la création d’un objet** déclencheur. Ce déclencheur s’active lorsqu’un objet est créé dans Salesforce. Dans notre exemple, nous allons la définir telle sorte que chaque fois qu’un nouveau prospect est créé dans Salesforce, un *envoyer un courrier électronique* action se produit via le connecteur hello SMTP avec une notification de prospect hello en cours de création.

1. Entrez *salesforce* dans la zone de recherche de hello sur le Concepteur d’applications hello logique, puis sélectionnez hello **Salesforce - lors de la création d’un objet** déclencheur.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. Hello **lorsqu’un objet est créé** contrôle s’affiche.
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. Sélectionnez hello **Type d’objet** puis sélectionnez *entraîner* à partir de la liste de hello d’objets. Lors de cette étape, vous indiquez que vous créez un déclencheur qui informe votre application logique de la création d’un prospect dans Salesforce.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. déclencheur de Hello a été créé.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a>Utiliser une action SMTP
Une action est une opération effectuée par flux de travail hello défini dans une application logique. [En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Maintenant que hello déclencheur a été ajouté, suivez ces étapes tooadd un SMTP l’action qui se produit lorsqu’un nouveau prospect est créé dans Salesforce.

1. Sélectionnez **+ nouvelle étape** action de hello tooadd vous aimeriez tootake lors de la création d’un nouveau prospect.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. Sélectionnez **Ajouter une action**. Cette zone de recherche hello s’ouvre dans laquelle vous pouvez rechercher n’importe quelle action vous aimeriez tootake.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. Entrez *smtp* toosearch pour tooSMTP connexes d’actions.  
4. Sélectionnez **SMTP - envoyer un courrier électronique** comme hello action tootake lors de la création de prospect hello. bloc de contrôle d’action Hello s’ouvre. Vous devez tooestablish votre connexion smtp dans le bloc de concepteur hello si vous le n'avez pas fait précédemment.  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. Entrez vos informations de messagerie de votre choix dans hello **SMTP - envoyer un courrier électronique** bloc.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. Enregistrez votre travail dans l’ordre tooactivate votre flux de travail.  

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/smtpconnector/).

## <a name="more-connectors"></a>Autres connecteurs
Revenir en arrière toohello [liste des API](apis-list.md).
