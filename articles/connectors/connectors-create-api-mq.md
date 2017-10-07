---
title: aaaLearn comment toouse hello connecteur MQ dans Azure Logic Apps | Documents Microsoft
description: "Se connecter tooan sur site ou serveur Azure à partir de votre toobrowse de flux de travail d’application logique, recevoir et envoyer des messages tooWebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a>Se connecter tooan IBM MQ server à partir d’applications logique à l’aide du connecteur MQ hello 

Microsoft Connector pour MQ envoie et récupère les messages stockés dans un serveur MQ local ou dans Azure. Ce connecteur inclut un client Microsoft MQ qui communique avec un serveur IBM MQ distant sur un réseau TCP/IP. Ce document est un connecteur de starter guide toouse hello MQ. Nous vous recommandons de commencer en parcourant un seul message dans une file d’attente, et puis que vous essayez de hello autres actions.    

connecteur MQ Hello inclut hello suivant des actions. Il n’y a aucun déclencheur.

-   Parcourir un seul message sans supprimer le message de type hello hello IBM MQ Server
-   Parcourir un lot de messages sans supprimer les messages hello hello IBM MQ Server
-   Un seul message de réception et supprimer message de type hello hello IBM MQ Server
-   Réception d’un lot de messages et supprimer des messages de type hello hello IBM MQ Server
-   Envoyer un message unique de toohello IBM MQ Server 

## <a name="prerequisites"></a>Composants requis

* Si vous utilisez un serveur local, [installer la passerelle de données locale hello](../logic-apps/logic-apps-gateway-install.md) sur un serveur au sein de votre réseau. Si hello MQ Server est publiquement disponible ou disponible dans Azure, puis la passerelle de données hello est non utilisée ou requises.

    > [!NOTE]
    > serveur Hello où hello passerelle de données locale est installée doit être également installé .net Framework 4.6 est installé pour hello MQ connecteur toofunction.

* Créer hello des ressources Azure pour la passerelle de données locale hello - [configurer la connexion de passerelle de données hello](../logic-apps/logic-apps-gateway-connection.md).

* Versions d’IBM WebSphere MQ Officiellement prises en charge :
   * MQ 7.5
   * MQ 8.0

## <a name="create-a-logic-app"></a>Créer une application logique

1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**. 
2. Entrez hello **nom**, telles que MQTestApp, **abonnement**, **groupe de ressources**, et **emplacement** (utiliser un emplacement de hello où hello connexion à la passerelle de données locale est configurée). Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.  
![Créer une application logique](media/connectors-create-api-mq/Create_Logic_App.png)

## <a name="add-a-trigger"></a>Ajouter un déclencheur

> [!NOTE]
> Hello MQ connecteur n’a pas de déclencheurs. Par conséquent, utilisez un autre déclencheur toostart votre application logique, par exemple hello **périodicité** déclencheur. 

1. Hello **Concepteur d’applications logique** s’ouvre, sélectionnez **périodicité** dans la liste hello de déclencheurs courantes.
2. Sélectionnez **modifier** dans hello déclencheur de périodicité. 
3. Ensemble hello **fréquence** trop**jour**et ensemble hello **intervalle** trop**7**. 

## <a name="browse-a-single-message"></a>Parcourir un seul message
1. Sélectionnez **+Nouvelle étape**, puis **Ajouter une action**.
2. Dans la zone de recherche de hello, tapez `mq`, puis sélectionnez **MQ - Parcourir message**.  
![Parcourir un message](media/connectors-create-api-mq/Browse_message.png)

3. En l’absence d’une connexion MQ existante, puis créez des connexions de hello :  

    1. Sélectionnez **se connecter via la passerelle de données locale**et entrez les propriétés hello de votre serveur.  
    Pour **Server**, vous pouvez entrer le nom du serveur MQ hello ou entrez l’adresse hello suivie d’un signe deux-points et hello le numéro de port. 
    2. Hello **passerelle** liste déroulante répertorie toutes les connexions de passerelle existantes qui ont été configurées. Sélectionnez votre passerelle.
    3. Lorsque vous avez terminé, sélectionnez **Créer**. Votre connexion semble similaire toohello suivantes :   
    ![Propriétés de connexion](media/connectors-create-api-mq/Connection_Properties.png)

4. Dans les propriétés d’une action hello, vous pouvez :  

    * Hello d’utilisation **file d’attente** propriété tooaccess un nom de file d’attente différent que celui défini dans la connexion de hello
    * Hello d’utilisation **MessageId**, **CorrelationId**, **GroupId**et autres toobrowse propriétés d’un message en fonction des propriétés de message hello différents MQ
    * Définissez **IncludeInfo** trop**True** tooinclude informations supplémentaires dans la sortie de hello. Ou, définissez-le trop**False** toonot inclure des informations supplémentaires dans une sortie hello.
    * Entrez un **délai d’attente** valeur toodetermine toowait combien de temps pour un message tooarrive dans une file d’attente vide. Si aucune valeur n’est entrée, hello premier message de file d’attente hello est récupérée et il n’existe aucun temps d’attente pour un tooappear de message.  
    ![Parcourir les propriétés d’un message](media/connectors-create-api-mq/Browse_message_Props.png)

5. **Enregistrez** vos modifications, puis **exécutez** votre application logique :  
![Enregistrer et exécuter](media/connectors-create-api-mq/Save_Run.png)

6. Après quelques secondes, étapes hello Hello exécuter sont affichées et vous pouvez examiner la sortie de hello. Sélectionnez hello coche verte toosee détails de chaque étape. Sélectionnez **consultez sorties brutes** toosee des détails supplémentaires sur hello les données de sortie.  
![Parcourir une sortie de message](media/connectors-create-api-mq/Browse_message_output.png)  

    Sortie brute :  
    ![Parcourir une sortie brute de message](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. Hello lorsque **IncludeInfo** option a la valeur tootrue, hello suivant la sortie s’affiche :  
![Parcourir les informations include d’un message](media/connectors-create-api-mq/Browse_message_Include_Info.png)

## <a name="browse-multiple-messages"></a>Parcourir plusieurs messages
Hello **parcourir les messages** action inclut un **BatchSize** option tooindicate combien de messages doit être retourné à partir de la file d’attente hello.  Si l’option **BatchSize** ne comporte aucune entrée, tous les messages sont retournés. Hello retourné un tableau de messages.

1. Lors de l’ajout de hello **parcourir les messages** action, hello première connexion qui est configurée est sélectionnée par défaut. Sélectionnez **modifier la connexion** toocreate une nouvelle connexion, ou sélectionnez une autre connexion.

2. sortie Hello de parcourir les messages montre :  
![Parcourir la sortie des messages](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a>Recevoir un seul message
Hello **recevoir un message** action a hello des mêmes entrées et sorties en tant que hello **Parcourir message** action. Lorsque vous utilisez **recevoir un message**, message de type hello est supprimé de la file d’attente hello.

## <a name="receive-multiple-messages"></a>Recevoir plusieurs messages
Hello **recevoir des messages** action a hello des mêmes entrées et sorties en tant que hello **parcourir les messages** action. Lorsque vous utilisez **recevoir des messages**, messages hello sont supprimés de la file d’attente hello.

S’il n’existe aucun message dans la file d’attente hello lorsque vous effectuez une recherche ou une opération de réception, étape de hello échoue avec hello suivant de sortie :  
![Erreur MQ Aucun message](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a>Envoyer un message
1. Lors de l’ajout de hello **envoyer le message** action, hello première connexion qui est configurée est sélectionnée par défaut. Sélectionnez **modifier la connexion** toocreate une nouvelle connexion, ou sélectionnez une autre connexion. Hello valide **Types de messages** sont **datagramme**, **réponse**, ou **demande**.  
![Propriétés d’envoi des messages](media/connectors-create-api-mq/Send_Msg_Props.png)

2. Hello sortie d’envoyer le message ressemble à hello suivantes :  
![Sortie Envoyer un message](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/mq/).

## <a name="next-steps"></a>Étapes suivantes
[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).
