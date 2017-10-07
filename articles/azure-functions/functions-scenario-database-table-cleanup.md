---
title: "aaaUse les fonctions Azure tooperform une base de données nettoyer tâche | Documents Microsoft"
description: "Utilisez les fonctions Azure tooschedule une tâche qui se connecte tooperiodically de base de données SQL tooAzure nettoyer les lignes."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a>Utilisez les fonctions Azure tooconnect tooan base de données SQL Azure
Cette rubrique vous montre comment toocreate des fonctions d’Azure toouse planifiée de la tâche qui nettoie les lignes d’une table dans une base de données SQL Azure. le nouveau Hello fonction c# est créée selon un modèle de déclenchement du minuteur prédéfinis Bonjour portail Azure. toosupport ce scénario, vous devez également définir une chaîne de connexion de base de données en tant que paramètre dans une application de fonction hello. Ce scénario utilise une opération en bloc par rapport à la base de données hello. toohave votre fonction processus CRUD opérations individuelles dans une table d’applications mobiles, vous devez utiliser [liaisons des applications mobiles](functions-bindings-mobile-apps.md).

## <a name="prerequisites"></a>Composants requis

+ Cette rubrique crée une fonction déclenchée par un minuteur. Hello terminé les étapes dans la rubrique de hello [créer une fonction dans Azure qui est déclenchée par un minuteur](functions-create-scheduled-function.md) version toocreate c# de cette fonction.   

+ Cette rubrique montre une commande Transact-SQL qui exécute une opération de nettoyage en bloc Bonjour **SalesOrderHeader** table dans la base de données AdventureWorksLT hello. toocreate hello AdventureWorksLT base de données exemple hello terminé les étapes dans la rubrique de hello [créer une base de données SQL Azure Bonjour Azure portal](../sql-database/sql-database-get-started-portal.md). 

## <a name="get-connection-information"></a>Obtenir des informations de connexion

Vous avez besoin d’une chaîne de connexion tooget hello pour vous avez créé lorsque vous avez effectué de la base de données hello [créer une base de données SQL Azure Bonjour Azure portal](../sql-database/sql-database-get-started-portal.md).

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
 
3. Sélectionnez **bases de données SQL** hello menu de gauche, sélectionnez votre base de données sur hello **bases de données SQL** page.

4. Sélectionnez **afficher les chaînes de connexion de base de données** et hello copie complète **ADO.NET** chaîne de connexion.

    ![Copiez la chaîne de connexion ADO.NET hello.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a>Définir la chaîne de connexion hello 

Une application de la fonction héberge l’exécution de hello de vos fonctions dans Azure. Il s’agit des chaînes de connexion une meilleure pratique toostore et autres secrets dans vos paramètres d’application de fonction. À l’aide des paramètres de l’application empêche la divulgation accidentelle de chaîne de connexion hello avec votre code. 

1. Accédez d’application de fonction tooyour vous avez créé [créer une fonction dans Azure qui est déclenchée par un minuteur](functions-create-scheduled-function.md).

2. Sélectionnez **Fonctionnalités de la plateforme** > **Paramètres de l’application**.
   
    ![Paramètres d’application pour l’application de fonction hello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. Faites défiler la liste trop**les chaînes de connexion** et ajouter une chaîne de connexion à l’aide des paramètres de hello comme spécifié dans la table de hello.
   
    ![Ajouter des paramètres d’application (fonction) de connexion à chaîne toohello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | Paramètre       | Valeur suggérée | Description             | 
    | ------------ | ------------------ | --------------------- | 
    | **Nom**  |  sqldb_connection  | Tooaccess utilisé hello stockées chaîne de connexion dans votre code de fonction.    |
    | **Valeur** | Chaîne copiée  | Après la chaîne de connexion hello que vous avez copié dans la section précédente de hello. |
    | **Type** | Base de données SQL | Utilisez la connexion de base de données SQL par défaut hello. |   

3. Cliquez sur **Enregistrer**.

Maintenant, vous pouvez ajouter hello fonction code c# qui se connecte tooyour base de données SQL.

## <a name="update-your-function-code"></a>Mettre à jour le code de votre fonction

1. Dans votre application de la fonction, sélectionnez la fonction a déclenché le minuteur de hello.
 
3. Ajoutez hello suit les références d’assembly haut hello hello existante du code de fonction :

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. Ajoutez hello suit `using` (fonction) toohello instructions :
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. Remplacer hello **exécuter** fonction avec hello suivant de code :
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    Cet exemple de commande met à jour hello **état** colonne basée sur la date d’expédition hello. Il doit mettre à jour 32 lignes de données.

5. Cliquez sur **enregistrer**, hello d’espion **journaux** windows pour hello ensuite l’exécution de la fonction, puis notez le nombre hello de lignes mises à jour Bonjour **SalesOrderHeader** table.

    ![Afficher les journaux de fonction hello.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a>Étapes suivantes

Ensuite, découvrez comment toouse fonctionne avec toointegrate Logic Apps avec d’autres services.

> [!div class="nextstepaction"] 
> [Créer une fonction qui s’intègre avec Logic Apps](functions-twitter-email.md)

Pour plus d’informations sur les fonctions, consultez hello rubriques suivantes :

* [Référence du développeur Azure Functions](functions-reference.md)  
  Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.
* [Test d’Azure Functions](functions-test-a-function.md)  
  décrit plusieurs outils et techniques permettant de tester vos fonctions.  
