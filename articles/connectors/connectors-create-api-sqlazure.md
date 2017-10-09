---
title: "connecteur de base de données SQL Azure hello aaaAdd dans vos applications logiques | Documents Microsoft"
description: "Vue d’ensemble du connecteur de base de données SQL Azure avec les paramètres de l’API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a>Prise en main connecteur de base de données SQL Azure hello
À l’aide du connecteur de base de données SQL Azure hello, créer des flux de travail pour votre organisation qui gèrent les données de vos tables. 

Avec Base de données SQL, vous pouvez effectuer les opérations suivantes :

* Créer votre flux de travail en ajoutant une nouvelle base de données client tooa clients ou une commande dans une base de données des commandes de mise à jour.
* Utilisez les actions tooget une ligne de données, insérer une nouvelle ligne, ou les supprimer. Par exemple, quand un enregistrement est créé dans Dynamics CRM Online (déclencheur), insérez une ligne dans une base de données SQL Azure (action). 

Cette rubrique vous montre comment toouse hello connecteur de base de données SQL dans une application logique, et également les listes hello actions.

toolearn en savoir plus sur les applications de la logique, consultez [quelles sont les applications logique](../logic-apps/logic-apps-what-are-logic-apps.md) et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-sql-database"></a>Se connecter tooAzure base de données SQL
Avant que votre application logique peut accéder à n’importe quel service, vous créez tout d’abord un *connexion* toohello service. Une connexion permet d’assurer la connectivité entre une application logique et un autre service. Par exemple, tooconnect tooSQL base de données, vous tout d’abord créez une base de données SQL *connexion*. toocreate une connexion, vous entrez les informations d’identification hello que vous utilisez normalement le service de hello tooaccess à que vous vous connectez. Par conséquent, dans la base de données SQL, entrez votre connexion de base de données SQL informations d’identification toocreate hello. 

#### <a name="create-hello-connection"></a>Créer la connexion de hello
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>Utilisation d’un déclencheur
Ce connecteur ne possède aucun déclencheur. Utilisez l’autre application logique de déclencheurs toostart hello, comme un déclencheur de périodicité, un déclencheur HTTP Webhook, déclencheurs disponibles avec tous les autres connecteurs et bien plus encore. [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md) vous fournit un exemple.

## <a name="use-an-action"></a>Utilisation d’une action
Une action est une opération effectuée par flux de travail hello défini dans une application logique. [En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Sélectionnez le signe plus hello. Vous voyez plusieurs choix : **ajouter une action**, **ajouter une condition**, ou l’un des hello **plus** options.
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. Choisissez **Ajouter une action**.
3. Dans la zone de texte hello, tapez « sql » tooget une liste de toutes les actions disponibles hello.
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. Dans notre exemple, choisissez **SQL Server - Obtenir une ligne**. Si une connexion existe déjà, puis sélectionnez hello **nom de la Table** dans hello de liste déroulante de liste, puis entrez les hello **ID de ligne** vous souhaitez tooreturn.
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    Si vous êtes invité hello informations de connexion, puis entrez connexion de hello toocreate hello détails. [Créer la connexion de hello](connectors-create-api-sqlazure.md#create-the-connection) dans cette rubrique décrit ces propriétés. 
   
   > [!NOTE]
   > Dans cet exemple, nous obtiendrons une ligne d’une table. données de hello toosee dans cette ligne, ajoutez une autre action qui crée un fichier à l’aide des champs hello à partir de la table de hello. Par exemple, ajouter une action de OneDrive qui utilise hello FirstName et LastName champs toocreate un nouveau fichier dans le compte de stockage cloud hello. 
   > 
   > 
5. **Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello). Votre application logique est enregistrée et peut être activée automatiquement.

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/sql/). 

## <a name="next-steps"></a>Étapes suivantes
[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).

