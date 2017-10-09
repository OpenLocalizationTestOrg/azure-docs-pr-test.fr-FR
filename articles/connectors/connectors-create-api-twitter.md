---
title: "aaaLearn comment toouse hello dans les applications de la logique d’un connecteur Twitter | Documents Microsoft"
description: "Vue d’ensemble du connecteur Twitter avec les paramètres d’API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a>Prise en main connecteur de Twitter hello
Avec le connecteur de Twitter hello, vous pouvez :

* publier et recevoir des tweets ;
* accéder à des fils d’actualités, des amis et des abonnés ;
* Effectuez l’une des hello autres actions et les déclencheurs décrites ci-dessous  

toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique. Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).  

## <a name="connect-tootwitter"></a>Se connecter tooTwitter
Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service. Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.  

### <a name="create-a-connection-tootwitter"></a>Créer un tooTwitter de connexion
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a>Utiliser un déclencheur Twitter
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique. [En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Dans cet exemple, je vous indiquent comment toouse hello **lors de la validation d’un tweet nouvelle** déclencher toosearch pour #Seattle et, si #Seattle est trouvée, mettre à jour un fichier dans l’échange avec texte hello tweet de hello. Dans un exemple d’entreprise, vous pourriez Rechercher nom hello de votre société et mettre à jour une base de données SQL avec texte hello tweet de hello.

1. Entrez *twitter* dans la zone de recherche de hello sur le Concepteur d’applications hello logique, puis sélectionnez hello **Twitter - lors de la validation d’un tweet nouvelle** déclencheur   
   ![Image de déclencheur Twitter 1](./media/connectors-create-api-twitter/trigger-1.png)  
2. Entrez *#Seattle* Bonjour **rechercher du texte** contrôle  
   ![Image de déclencheur Twitter 2](./media/connectors-create-api-twitter/trigger-2.png) 

À ce stade, votre application logique a été configurée avec un déclencheur qui commence une série de hello autres déclencheurs et les actions dans le flux de travail hello. 

> [!NOTE]
> Pour un toobe application logique fonctionnelle, il doit contenir au moins un déclencheur et une action. Suivez les étapes de hello de hello suivant section tooadd une action.  
> 
> 

## <a name="add-a-condition"></a>Ajouter une condition
Étant donné que nous intéresse uniquement tweet d’utilisateurs avec plus de 50 utilisateurs, une condition qui confirme que le nombre de hello imposait doit d’abord être ajoutée toohello logique application.  

1. Sélectionnez **+ nouvelle étape** action de hello tooadd vous aimeriez tootake quand #Seattle se trouve dans un tweet nouveau  
   ![Image d’action Twitter 1](../../includes/media/connectors-create-api-twitter/action-1.png)  
2. Sélectionnez hello **ajouter une condition** lien.  
   ![Image de condition Twitter 1](../../includes/media/connectors-create-api-twitter/condition-1.png)   
   Cette opération ouvre hello **Condition** contrôle où vous pouvez vérifier des conditions telles que *est égal à*, *est inférieur à*, *est supérieur à*, *contient*, etc..  
   ![Image de condition Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)   
3. Sélectionnez hello **choisir une valeur** contrôle.  
   Dans ce contrôle, vous pouvez sélectionner une ou plusieurs des propriétés de hello à partir des actions précédentes ou les déclencheurs en tant que valeur hello dont la condition sera évaluée tootrue ou false.
   ![Image de condition Twitter 3](../../includes/media/connectors-create-api-twitter/condition-3.png)   
4. Sélectionnez hello **...**  liste de hello tooexpand de propriétés afin de voir toutes les propriétés de hello qui sont disponibles.        
   ![Image de condition Twitter 4](../../includes/media/connectors-create-api-twitter/condition-4.png)   
5. Sélectionnez hello **nombre de suivis** propriété.    
   ![Image de condition Twitter 5](../../includes/media/connectors-create-api-twitter/condition-5.png)   
6. Notez que les suivis hello propriété count est présent dans le contrôle de valeurs hello.    
   ![Image de condition Twitter 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. Sélectionnez **est supérieur à** à partir de la liste des opérateurs hello.    
   ![Image de condition Twitter 7](../../includes/media/connectors-create-api-twitter/condition-7.png)   
8. Entrez 50 comme hello opérande pour hello *est supérieur à* opérateur.  
   Hello condition est maintenant ajoutée. Enregistrez votre travail à l’aide de hello **enregistrer** lien dans le menu hello ci-dessus.    
   ![Image de condition Twitter 8](../../includes/media/connectors-create-api-twitter/condition-8.png)   

## <a name="use-a-twitter-action"></a>Utiliser une action Twitter
Une action est une opération effectuée par flux de travail hello défini dans une application logique. [En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Maintenant que vous avez ajouté un déclencheur, suivez ces étapes de tooadd une action qui publie un tweet nouveau contenu hello de tweet hello trouvés par le déclencheur de hello. Pour les besoins de hello de cette procédure pas à pas uniquement des tweets d’utilisateurs avec plus de 50 suivis seront publiées.  

Dans l’étape suivante de hello, vous allez ajouter une action Twitter qui publie un tweet à l’aide de certaines des propriétés de hello de chaque tweet qui a été validé par un utilisateur qui a plus de 50 suivis.  

1. Sélectionnez **Ajouter une action**. Contrôle de recherche hello dans laquelle vous pouvez rechercher d’autres actions et les déclencheurs s’ouvre.  
   ![Image de condition Twitter 9](../../includes/media/connectors-create-api-twitter/condition-9.png)   
2. Entrez *twitter* dans la zone de recherche hello, puis sélectionnez hello **Twitter - valider un tweet** action. Cette opération ouvre hello **valider un tweet** contrôler où vous devrez entrer tous les détails pour tweet hello en cours de publication.      
   ![Image d’action Twitter 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)   
3. Sélectionnez hello **tweetez-texte** contrôle. Toutes les sorties à partir des actions précédentes et des déclencheurs dans l’application logique de hello sont désormais visibles. Vous pouvez sélectionner une de ces et les utiliser en tant que partie du texte de tweet hello de tweet de nouveau hello.     
   ![Image d’action Twitter 2](../../includes/media/connectors-create-api-twitter/action-2.png)   
4. Sélectionnez **Nom d’utilisateur**.   
5. Entrez *indique :* dans le contrôle de texte tweet hello. Effectuez cette opération immédiatement après avoir sélectionné le nom d’utilisateur.  
6. Sélectionnez *Tweet text* (Texte du tweet).       
   ![Image d’action Twitter 3](../../includes/media/connectors-create-api-twitter/action-3.png)   
7. Enregistrez votre travail et envoyer un tweet avec hello #Seattle #sqlhelp tooactivate votre flux de travail.  


## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/twitterconnector/). 

## <a name="next-steps"></a>Étapes suivantes
[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md)

