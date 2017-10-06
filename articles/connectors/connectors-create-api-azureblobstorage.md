---
title: "aaaAdd hello stockage d’objets blob Azure dans vos applications de la logique d’un connecteur | Documents Microsoft"
description: "Prise en main et de configurer le connecteur de stockage d’objets blob Azure hello dans une application de logique"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a>Utiliser le connecteur de stockage d’objets blob Azure hello dans une application de logique
Tooupload de connecteur utilisez hello Azure Blob storage, mettre à jour, obtenir et supprimer des objets BLOB dans votre compte de stockage, toutes les tâches dans une application logique.  

Avec Azure Blob Storage, vous pouvez effectuer les opérations suivantes :

* Créez votre workflow en téléchargeant les nouveaux projets ou en extrayant les fichiers récemment mis à jour.
* Utilisez les métadonnées du fichier actions tooget, supprimer un fichier, copier les fichiers et bien plus encore. Par exemple, lorsqu’un outil est mis à jour dans un site web Azure (déclencheur), vous pouvez mettre à jour un fichier dans le stockage blob (action). 

Cette rubrique vous montre comment toouse hello blob connecteur dans une application de la logique de stockage.

toolearn en savoir plus sur les applications de la logique, consultez [quelles sont les applications logique](../logic-apps/logic-apps-what-are-logic-apps.md) et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

toolearn en savoir plus sur les applications de la logique, consultez [quelles sont les applications logique](../logic-apps/logic-apps-what-are-logic-apps.md) et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-blob-storage"></a>Connecter le stockage d’objets blob tooAzure
Avant que votre application logique peut accéder à n’importe quel service, vous créez tout d’abord un *connexion* toohello service. Une connexion permet d’assurer la connectivité entre une application logique et un autre service. Par exemple, le compte de stockage tooconnect tooa vous tout d’abord créez un stockage d’objets blob *connexion*. toocreate une connexion, entrez des informations d’identification de hello que vous utilisez normalement le service de hello tooaccess vous êtes connecté. Par conséquent, avec le stockage Azure, entrez connexion hello de hello informations d’identification tooyour stockage compte toocreate. 

#### <a name="create-hello-connection"></a>Créer la connexion de hello
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a>Utilisation d’un déclencheur
Ce connecteur ne possède aucun déclencheur. Utilisez l’autre application logique de déclencheurs toostart hello, comme un déclencheur de périodicité, un déclencheur HTTP Webhook, déclencheurs disponibles avec tous les autres connecteurs et bien plus encore. [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md) vous fournit un exemple.

## <a name="use-an-action"></a>Utilisation d’une action
Une action est une opération effectuée par flux de travail hello défini dans une application logique.

1. Sélectionnez le signe plus hello. Vous voyez plusieurs choix : **ajouter une action**, **ajouter une condition**, ou l’un des hello **plus** options.
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. Choisissez **Ajouter une action**.
3. Dans la zone de texte hello, tapez « blob » tooget une liste de toutes les actions disponibles hello.
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. Dans notre exemple, choisissez **AzureBlob - Obtenir les métadonnées d’un fichier à l’aide du chemin**. Si une connexion existe déjà, puis sélectionnez hello **...** Tooselect de bouton (Afficher sélecteur) un fichier.
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    Si vous êtes invité hello informations de connexion, puis entrez connexion de hello toocreate hello détails. [Créer la connexion de hello](connectors-create-api-azureblobstorage.md#create-the-connection) dans cette rubrique décrit ces propriétés. 
   
   > [!NOTE]
   > Dans cet exemple, nous obtenons hello les métadonnées d’un fichier. toosee hello des métadonnées, ajoutez une autre action qui crée un nouveau fichier à l’aide d’un autre connecteur. Par exemple, ajouter une action OneDrive qui crée un nouveau fichier de « test » en fonction de métadonnées de hello. 


5. **Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello). Votre application logique est enregistrée et peut être activée automatiquement.

> [!TIP]
> [Explorateur de stockage](http://storageexplorer.com/) est un excellent outil gérer trop de plusieurs comptes de stockage.

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/azureblobconnector/). 

## <a name="next-steps"></a>Étapes suivantes
[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).

