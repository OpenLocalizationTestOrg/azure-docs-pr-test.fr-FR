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
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a><span data-ttu-id="3c31c-103">Utilisez les fonctions Azure tooconnect tooan base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3c31c-103">Use Azure Functions tooconnect tooan Azure SQL Database</span></span>
<span data-ttu-id="3c31c-104">Cette rubrique vous montre comment toocreate des fonctions d’Azure toouse planifiée de la tâche qui nettoie les lignes d’une table dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3c31c-104">This topic shows you how toouse Azure Functions toocreate a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="3c31c-105">le nouveau Hello fonction c# est créée selon un modèle de déclenchement du minuteur prédéfinis Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3c31c-105">hello new C# function is created based on a pre-defined timer trigger template in hello Azure portal.</span></span> <span data-ttu-id="3c31c-106">toosupport ce scénario, vous devez également définir une chaîne de connexion de base de données en tant que paramètre dans une application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="3c31c-106">toosupport this scenario, you must also set a database connection string as a setting in hello function app.</span></span> <span data-ttu-id="3c31c-107">Ce scénario utilise une opération en bloc par rapport à la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="3c31c-107">This scenario uses a bulk operation against hello database.</span></span> <span data-ttu-id="3c31c-108">toohave votre fonction processus CRUD opérations individuelles dans une table d’applications mobiles, vous devez utiliser [liaisons des applications mobiles](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3c31c-108">toohave your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c31c-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3c31c-109">Prerequisites</span></span>

+ <span data-ttu-id="3c31c-110">Cette rubrique crée une fonction déclenchée par un minuteur.</span><span class="sxs-lookup"><span data-stu-id="3c31c-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="3c31c-111">Hello terminé les étapes dans la rubrique de hello [créer une fonction dans Azure qui est déclenchée par un minuteur](functions-create-scheduled-function.md) version toocreate c# de cette fonction.</span><span class="sxs-lookup"><span data-stu-id="3c31c-111">Complete hello steps in hello topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) toocreate a C# version of this function.</span></span>   

+ <span data-ttu-id="3c31c-112">Cette rubrique montre une commande Transact-SQL qui exécute une opération de nettoyage en bloc Bonjour **SalesOrderHeader** table dans la base de données AdventureWorksLT hello.</span><span class="sxs-lookup"><span data-stu-id="3c31c-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in hello **SalesOrderHeader** table in hello AdventureWorksLT sample database.</span></span> <span data-ttu-id="3c31c-113">toocreate hello AdventureWorksLT base de données exemple hello terminé les étapes dans la rubrique de hello [créer une base de données SQL Azure Bonjour Azure portal](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3c31c-113">toocreate hello AdventureWorksLT sample database, complete hello steps in hello topic [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="3c31c-114">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="3c31c-114">Get connection information</span></span>

<span data-ttu-id="3c31c-115">Vous avez besoin d’une chaîne de connexion tooget hello pour vous avez créé lorsque vous avez effectué de la base de données hello [créer une base de données SQL Azure Bonjour Azure portal](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3c31c-115">You need tooget hello connection string for hello database you created when you completed [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="3c31c-116">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3c31c-116">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="3c31c-117">Sélectionnez **bases de données SQL** hello menu de gauche, sélectionnez votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="3c31c-117">Select **SQL Databases** from hello left-hand menu, and select your database on hello **SQL databases** page.</span></span>

4. <span data-ttu-id="3c31c-118">Sélectionnez **afficher les chaînes de connexion de base de données** et hello copie complète **ADO.NET** chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="3c31c-118">Select **Show database connection strings** and copy hello complete **ADO.NET** connection string.</span></span>

    ![Copiez la chaîne de connexion ADO.NET hello.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a><span data-ttu-id="3c31c-120">Définir la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="3c31c-120">Set hello connection string</span></span> 

<span data-ttu-id="3c31c-121">Une application de la fonction héberge l’exécution de hello de vos fonctions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3c31c-121">A function app hosts hello execution of your functions in Azure.</span></span> <span data-ttu-id="3c31c-122">Il s’agit des chaînes de connexion une meilleure pratique toostore et autres secrets dans vos paramètres d’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="3c31c-122">It is a best practice toostore connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="3c31c-123">À l’aide des paramètres de l’application empêche la divulgation accidentelle de chaîne de connexion hello avec votre code.</span><span class="sxs-lookup"><span data-stu-id="3c31c-123">Using application settings prevents accidental disclosure of hello connection string with your code.</span></span> 

1. <span data-ttu-id="3c31c-124">Accédez d’application de fonction tooyour vous avez créé [créer une fonction dans Azure qui est déclenchée par un minuteur](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="3c31c-124">Navigate tooyour function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="3c31c-125">Sélectionnez **Fonctionnalités de la plateforme** > **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="3c31c-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Paramètres d’application pour l’application de fonction hello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="3c31c-127">Faites défiler la liste trop**les chaînes de connexion** et ajouter une chaîne de connexion à l’aide des paramètres de hello comme spécifié dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="3c31c-127">Scroll down too**Connection strings** and add a connection string using hello settings as specified in hello table.</span></span>
   
    ![Ajouter des paramètres d’application (fonction) de connexion à chaîne toohello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="3c31c-129">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3c31c-129">Setting</span></span>       | <span data-ttu-id="3c31c-130">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="3c31c-130">Suggested value</span></span> | <span data-ttu-id="3c31c-131">Description</span><span class="sxs-lookup"><span data-stu-id="3c31c-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="3c31c-132">**Nom**</span><span class="sxs-lookup"><span data-stu-id="3c31c-132">**Name**</span></span>  |  <span data-ttu-id="3c31c-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="3c31c-133">sqldb_connection</span></span>  | <span data-ttu-id="3c31c-134">Tooaccess utilisé hello stockées chaîne de connexion dans votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="3c31c-134">Used tooaccess hello stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="3c31c-135">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="3c31c-135">**Value**</span></span> | <span data-ttu-id="3c31c-136">Chaîne copiée</span><span class="sxs-lookup"><span data-stu-id="3c31c-136">Copied string</span></span>  | <span data-ttu-id="3c31c-137">Après la chaîne de connexion hello que vous avez copié dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="3c31c-137">Past hello connection string you copied in hello previous section.</span></span> |
    | <span data-ttu-id="3c31c-138">**Type**</span><span class="sxs-lookup"><span data-stu-id="3c31c-138">**Type**</span></span> | <span data-ttu-id="3c31c-139">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="3c31c-139">SQL Database</span></span> | <span data-ttu-id="3c31c-140">Utilisez la connexion de base de données SQL par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="3c31c-140">Use hello default SQL Database connection.</span></span> |   

3. <span data-ttu-id="3c31c-141">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3c31c-141">Click **Save**.</span></span>

<span data-ttu-id="3c31c-142">Maintenant, vous pouvez ajouter hello fonction code c# qui se connecte tooyour base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="3c31c-142">Now, you can add hello C# function code that connects tooyour SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="3c31c-143">Mettre à jour le code de votre fonction</span><span class="sxs-lookup"><span data-stu-id="3c31c-143">Update your function code</span></span>

1. <span data-ttu-id="3c31c-144">Dans votre application de la fonction, sélectionnez la fonction a déclenché le minuteur de hello.</span><span class="sxs-lookup"><span data-stu-id="3c31c-144">In your function app, select hello timer-triggered function.</span></span>
 
3. <span data-ttu-id="3c31c-145">Ajoutez hello suit les références d’assembly haut hello hello existante du code de fonction :</span><span class="sxs-lookup"><span data-stu-id="3c31c-145">Add hello following assembly references at hello top of hello existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="3c31c-146">Ajoutez hello suit `using` (fonction) toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="3c31c-146">Add hello following `using` statements toohello function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="3c31c-147">Remplacer hello **exécuter** fonction avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="3c31c-147">Replace hello existing **Run** function with hello following code:</span></span>
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

    <span data-ttu-id="3c31c-148">Cet exemple de commande met à jour hello **état** colonne basée sur la date d’expédition hello.</span><span class="sxs-lookup"><span data-stu-id="3c31c-148">This sample command updates hello **Status** column based on hello ship date.</span></span> <span data-ttu-id="3c31c-149">Il doit mettre à jour 32 lignes de données.</span><span class="sxs-lookup"><span data-stu-id="3c31c-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="3c31c-150">Cliquez sur **enregistrer**, hello d’espion **journaux** windows pour hello ensuite l’exécution de la fonction, puis notez le nombre hello de lignes mises à jour Bonjour **SalesOrderHeader** table.</span><span class="sxs-lookup"><span data-stu-id="3c31c-150">Click **Save**, watch hello **Logs** windows for hello next function execution, then note hello number of rows updated in hello **SalesOrderHeader** table.</span></span>

    ![Afficher les journaux de fonction hello.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="3c31c-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3c31c-152">Next steps</span></span>

<span data-ttu-id="3c31c-153">Ensuite, découvrez comment toouse fonctionne avec toointegrate Logic Apps avec d’autres services.</span><span class="sxs-lookup"><span data-stu-id="3c31c-153">Next, learn how toouse Functions with Logic Apps toointegrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="3c31c-154">Créer une fonction qui s’intègre avec Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3c31c-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="3c31c-155">Pour plus d’informations sur les fonctions, consultez hello rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="3c31c-155">For more information about Functions, see hello following topics:</span></span>

* [<span data-ttu-id="3c31c-156">Référence du développeur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3c31c-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="3c31c-157">Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.</span><span class="sxs-lookup"><span data-stu-id="3c31c-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="3c31c-158">Test d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3c31c-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="3c31c-159">décrit plusieurs outils et techniques permettant de tester vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="3c31c-159">Describes various tools and techniques for testing your functions.</span></span>  
