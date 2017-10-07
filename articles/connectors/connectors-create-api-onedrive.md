---
title: connecteur de OneDrive aaaAdd hello dans vos applications logiques | Documents Microsoft
description: "Vue d’ensemble du connecteur de OneDrive hello avec des paramètres de l’API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a>Prise en main connecteur de OneDrive hello
Se connecter tooOneDrive toomanage vos fichiers, y compris le téléchargement, get, supprimez des fichiers et bien plus encore. 

Avec OneDrive, vous pouvez effectuer les opérations suivantes : 

* Créer votre flux de travail en stockant des fichiers dans OneDrive, ou mettre à jour des fichiers existants dans OneDrive. 
* Utilisez des déclencheurs toostart votre flux de travail lorsqu’un fichier est créé ou mis à jour au sein de votre OneDrive.
* Utiliser des actions toocreate un fichier, supprimer un fichier et bien plus encore. Par exemple, lorsqu’un nouveau courrier électronique Office 365 est reçu avec une pièce jointe (déclencheur), créer un nouveau fichier dans OneDrive (action).

Cette rubrique vous montre comment toouse hello dans une application de la logique d’un connecteur OneDrive, et également les listes hello déclencheurs et actions.

toolearn en savoir plus sur les applications de la logique, consultez [quelles sont les applications logique](../logic-apps/logic-apps-what-are-logic-apps.md) et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooonedrive"></a>Se connecter tooOneDrive
Avant que votre application logique peut accéder à n’importe quel service, vous créez tout d’abord un *connexion* toohello service. Une connexion permet d’assurer la connectivité entre une application logique et un autre service. Par exemple, tooconnect tooOneDrive, vous devez d’abord un OneDrive *connexion*. toocreate une connexion, entrez des informations d’identification de hello que vous utilisez normalement le service de hello tooaccess tooconnect pour vous le souhaitez. Par conséquent, avec OneDrive, entrez hello authentification tooyour OneDrive compte toocreate hello à la connexion.

### <a name="create-hello-connection"></a>Créer la connexion de hello
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a>Utilisation d’un déclencheur
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique. Déclencheurs « interrogent « service de hello à un intervalle et la fréquence à laquelle vous souhaitez. [En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Dans l’application de la logique de hello, tapez « onedrive » tooget une liste des déclencheurs de hello :  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. Sélectionnez **Quand un fichier est modifié**. Si une connexion existe déjà, puis sélectionnez le bouton tooselect un dossier de hello afficher le sélecteur.
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    Si vous êtes invité à toosign dans, puis entrez le signe de hello dans Détails toocreate hello de connexion. [Créer la connexion de hello](connectors-create-api-onedrive.md#create-the-connection) dans cette rubrique répertorie les étapes de hello. 
   
   > [!NOTE]
   > Dans cet exemple, application logique de hello, s’exécute lorsqu’un fichier dans le dossier hello que vous choisissez est mis à jour. résultats de hello toosee de ce déclencheur, ajouter une autre action qui vous envoie un message électronique. Par exemple, ajouter hello Outlook Office 365 *envoyer un courrier électronique* action qui envoie par courrier électronique vous lorsqu’un fichier est mis à jour. 

3. Sélectionnez hello **modifier** bouton et définissez hello **fréquence** et **intervalle** valeurs. Par exemple, si vous souhaitez hello déclencheur toopoll toutes les 15 minutes, puis définissez hello **fréquence** trop**Minute**et ensemble hello **intervalle** trop**15**. 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. **Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello). Votre application logique est enregistrée et peut être activée automatiquement.

## <a name="use-an-action"></a>Utilisation d’une action
Une action est une opération effectuée par flux de travail hello défini dans une application logique. [En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Sélectionnez le signe plus hello. Vous voyez plusieurs choix : **ajouter une action**, **ajouter une condition**, ou l’un des hello **plus** options.
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. Choisissez **Ajouter une action**.
3. Dans la zone de texte hello, tapez « onedrive » tooget une liste de toutes les actions disponibles hello.
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. Dans notre exemple, choisissez **OneDrive - Créer un fichier**. Si une connexion existe déjà, puis sélectionnez hello **chemin d’accès du dossier** tooput hello de fichier, entrez hello **nom de fichier**, puis choisissez hello **contenu du fichier** souhaité :  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    Si vous êtes invité hello informations de connexion, puis entrez connexion de hello toocreate hello détails. [Créer la connexion de hello](connectors-create-api-onedrive.md#create-the-connection) dans cette rubrique décrit ces propriétés. 
   
   > [!NOTE]
   > Dans cet exemple, nous allons créer un nouveau fichier dans un dossier OneDrive. Vous pouvez utiliser la sortie à partir d’un autre fichier OneDrive de déclencheur toocreate hello. Par exemple, ajouter hello Outlook Office 365 *lorsqu’un nouvel e-mail arrive* déclencheur. Ajoutez ensuite hello OneDrive *créer un fichier* action qui utilise une hello des pièces jointes et les champs de Type de contenu dans un fichier ForEach toocreate hello nouveau dans OneDrive. 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. **Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello). Votre application logique est enregistrée et peut être activée automatiquement.


## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/onedriveconnector/).

## <a name="more-connectors"></a>Autres connecteurs
Revenir en arrière toohello [liste des API](apis-list.md).
