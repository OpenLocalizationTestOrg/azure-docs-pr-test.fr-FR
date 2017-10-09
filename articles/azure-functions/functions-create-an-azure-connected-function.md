---
title: "aaaCreate une fonction qui se connecte à des services de tooAzure | Documents Microsoft"
description: Utilisez les fonctions Azure toocreate une application sans serveur qui se connecte tooother Azure services.
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>Utilisez les fonctions Azure toocreate une fonction qui se connecte tooother Azure services

Cette rubrique vous montre comment toocreate une fonction dans les fonctions Azure toomessages sur un hello de file d’attente et les copies de stockage Azure est à l’écoute les messages toorows dans une table de stockage Azure. Une fonction de minuteur déclenché est tooload utilisé des messages en file d’attente hello. Une deuxième fonction lit à partir de la file d’attente hello et écrit les messages toohello table. File d’attente hello et table de hello sont créés pour vous par les fonctions Azure basé sur des définitions de liaison hello. 

toomake les choses plus intéressants, une fonction est écrit en JavaScript et hello autres est écrit dans le script c#. Cela montre qu’une Function App peut avoir des fonctions dans différentes langues. 

Vous pouvez voir la démonstration de ce scénario dans une [vidéo sur Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).

## <a name="create-a-function-that-writes-toohello-queue"></a>Créez une fonction qui écrit la file d’attente toohello

Avant de pouvoir vous connecter de la file d’attente de stockage tooa, vous devez toocreate une fonction qui charge la file d’attente de messages hello. Cette fonction JavaScript utilise un déclencheur du minuteur qui écrit une file d’attente de message toohello toutes les 10 secondes. Si vous n’avez pas encore un compte Azure, consultez hello [essayer les fonctions Azure](https://functions.azure.com/try) expérience, ou [créer gratuitement un compte Azure](https://azure.microsoft.com/free/).

1. Accédez toohello portail Azure et recherchez votre application de la fonction.

2. Cliquez sur **Nouvelle fonction** > **TimerTrigger-JavaScript**. 

3. Nom de fonction hello **FunctionsBindingsDemo1**, entrez une valeur d’expression cron `0/10 * * * * *` pour **planification**, puis cliquez sur **créer**.
   
    ![Ajouter une fonction de minuteur déclencheur](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    Vous venez de créer une fonction de minuteur déclencheur qui s’exécute toutes les 10 secondes.

5. Sur hello **développer** , cliquez sur **journaux** et afficher les activités de hello dans le journal de hello. Les entrées de journal que vous consultez ont été écrites toutes les 10 secondes.
   
    ![Fonctionnement de la fonction vue hello journal tooverify hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>Ajouter une liaison de sortie de file d’attente de messages

1. Sur hello **intégrer** , onglet choisir **nouvelle sortie** > **stockage de file d’attente Azure** > **sélectionnez**.

    ![Ajouter une fonction de minuteur déclencheur](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. Entrez `myQueueItem` pour **nom de paramètre de Message** et `functions-bindings` pour **nom de la file d’attente**, sélectionnez un existant **connexion au compte de stockage** ou cliquez sur **nouvelle** toocreate un stockage compte de connexion, puis cliquez sur **enregistrer**.  

    ![Créer la file d’attente de liaison toohello stockage hello sortie](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. Dans hello **développer** onglet, ajouter hello suivant code toohello fonction :
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. Recherchez hello *si* instruction environ 9 de la fonction hello et de code suivant de hello d’insertion après cette instruction.
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    Ce code crée un **myQueueItem** et définit ses **temps** horodateur actuel toohello de propriété. Il ajoute ensuite hello nouvelle file d’attente élément toohello du contexte **myQueueItem** liaison.

3. Cliquez sur **Enregistrer et exécuter**.

## <a name="view-storage-updates-by-using-storage-explorer"></a>Afficher les mises à jour du stockage à l’aide de l’Explorateur de stockage
Vous pouvez vérifier que votre fonction fonctionne en consultant les messages dans la file d’attente hello que vous avez créé.  Vous pouvez connecter la file d’attente de stockage tooyour à l’aide de l’Explorateur de Cloud dans Visual Studio. Toutefois, portail de hello rend compte de stockage tooyour tooconnect facile à l’aide de l’Explorateur de stockage Microsoft Azure.

1. Bonjour **intégrer** , cliquez sur votre file d’attente de liaison de sortie > **Documentation**, afficher hello chaîne de connexion pour votre compte de stockage, puis copiez la valeur de hello. Vous utilisez ce compte de stockage de valeur tooconnect tooyour.

    ![Télécharger l’Explorateur de stockage Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. Si ce n’est déjà fait, téléchargez et installez [l’Explorateur de stockage Microsoft Azure](http://storageexplorer.com). 
 
3. Dans l’Explorateur de stockage, cliquez sur hello tooAzure stockage icône de connexion, collez la chaîne de connexion hello dans le champ de hello et terminer l’Assistant de hello.

    ![Explorateur de stockage - Ajout d’une connexion](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. Sous **Local et attachées**, développez **comptes de stockage** > votre compte de stockage > **les files d’attente** > **deliaisonsdefonctions**et vérifiez que les messages sont écrits de file d’attente toohello.

    ![Affichage des messages dans la file d’attente hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    Si la file d’attente hello n’existe pas ou est vide, il s’agit probablement d’un problème avec votre code ou de liaison de fonction.

## <a name="create-a-function-that-reads-from-hello-queue"></a>Créez une fonction qui lit à partir de la file d’attente hello

Maintenant que vous avez ajoutés la file d’attente de toohello de messages, vous pouvez créer une autre fonction qui lit à partir de la file d’attente hello et écritures hello messages définitivement table de stockage Azure tooan.

1. Cliquez sur **Nouvelle fonction** > **QueueTrigger-CSharp**. 
 
2. Nom de fonction hello `FunctionsBindingsDemo2`, entrez **liaisons de fonctions** Bonjour **nom de la file d’attente** champ, sélectionnez un compte de stockage existant ou créez-en un, puis cliquez sur **créer**.

    ![Ajouter une fonction de minuteur de file d’attente de sortie](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. (Facultatif) Vous pouvez vérifier que la nouvelle fonction de hello fonctionne en consultant la nouvelle file d’attente de hello dans l’Explorateur de stockage comme avant. Vous pouvez également utiliser Cloud Explorer dans Visual Studio.  

4. (Facultatif) Actualiser hello **liaisons de fonctions** file d’attente et notez que les éléments ont été supprimés de la file d’attente hello. Hello suppression se produit, car la fonction hello est lié toohello **liaisons de fonctions** comme une fonction d’entrée de déclencheur et hello lit la file d’attente hello en file d’attente. 
 
## <a name="add-a-table-output-binding"></a>Ajouter une liaison de sortie de table

1. Dans FunctionsBindingsDemo2, cliquez sur **Intégrer** > **Nouvelle sortie** > **Table de stockage Azure** > **Sélectionner**.

    ![Ajouter une table de stockage Azure tooan liaison](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. Entrez `functionbindings` pour **Nom de la table** et `myTable` pour **Nom du paramètre de table**, choisissez une **Connexion du compte de stockage** ou créez-en une, puis cliquez sur **Enregistrer**.

    ![Configurer la liaison de table de stockage hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. Bonjour **développer** onglet, remplacez le code existant de la fonction hello par qui suit hello :
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    Hello **TableItem** classe représente une ligne dans la table de stockage hello, et vous ajoutez hello élément toohello `myTable` collection de **TableItem** objets. Vous devez définir hello **PartitionKey** et **RowKey** tooinsert en mesure de propriétés toobe dans la table de hello.

4. Cliquez sur **Enregistrer**.  Enfin, vous pouvez vérifier le fonctionnement de la fonction hello en consultant la table de hello dans l’Explorateur de stockage ou de Visual Studio Cloud Explorer.

5. (Facultatif) Dans votre compte de stockage dans l’Explorateur de stockage, développez **Tables** > **functionsbindings** et vérifiez que les lignes sont ajoutées toohello table. Vous pouvez effectuer même hello dans Cloud Explorer dans Visual Studio.

    ![Affichage des lignes de table de hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    Si la table de hello n’existe pas ou est vide, il s’agit probablement d’un problème avec votre code ou de liaison de fonction. 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les fonctions d’Azure, consultez hello rubriques suivantes :

* [Référence du développeur Azure Functions](functions-reference.md)  
  Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.
* [Test d’Azure Functions](functions-test-a-function.md)  
  décrit plusieurs outils et techniques permettant de tester vos fonctions.
* [Comment tooscale les fonctions Azure](functions-scale.md)  
  Décrit des plans de service disponibles avec les fonctions d’Azure, y compris le plan d’hébergement hello consommation, et comment toochoose hello adaptée. 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

