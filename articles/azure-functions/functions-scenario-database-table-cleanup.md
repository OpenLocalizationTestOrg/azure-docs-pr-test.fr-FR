---
title: "Utiliser Azure Functions pour effectuer une tâche de nettoyage de base de données | Microsoft Docs"
description: "Utilisez Azure Functions pour planifier une tâche qui se connecte à Azure SQL Database pour nettoyer des lignes périodiquement."
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
ms.openlocfilehash: 6fd0e32374827b249f5aba1cbfc39117c88c6272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="7c930-103">Utiliser Azure Functions pour se connecter à une base de données Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="7c930-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="7c930-104">Cette rubrique vous montre comment utiliser Azure Functions pour créer une tâche planifiée qui nettoie des lignes dans une table d’une base de données Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7c930-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="7c930-105">La nouvelle fonction C# est créée selon un modèle de déclencheur de minuteur prédéfini dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7c930-105">The new C# function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="7c930-106">Pour prendre en charge ce scénario, vous devez également définir une chaîne de connexion de base de données comme paramètre de l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="7c930-106">To support this scenario, you must also set a database connection string as a setting in the function app.</span></span> <span data-ttu-id="7c930-107">Ce scénario utilise une opération en bloc sur la base de données.</span><span class="sxs-lookup"><span data-stu-id="7c930-107">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="7c930-108">Pour que votre fonction traite des opérations CRUD individuelles dans une table Mobile Apps, utilisez à la place des [liaisons Mobile Apps](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="7c930-108">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c930-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7c930-109">Prerequisites</span></span>

+ <span data-ttu-id="7c930-110">Cette rubrique crée une fonction déclenchée par un minuteur.</span><span class="sxs-lookup"><span data-stu-id="7c930-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="7c930-111">Suivez les étapes de la rubrique [Créer une fonction dans Azure, qui est déclenchée par un minuteur](functions-create-scheduled-function.md) pour créer une version C# de cette fonction.</span><span class="sxs-lookup"><span data-stu-id="7c930-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="7c930-112">Cette rubrique montre une commande Transact-SQL qui exécute une opération de nettoyage en bloc dans la table nommée **SalesOrderHeader** de l’exemple de base de données AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="7c930-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="7c930-113">Pour créer l’exemple de base de données AdventureWorksLT, effectuez les étapes de la rubrique [Création d’une base de données SQL Azure dans le portail Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7c930-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="7c930-114">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="7c930-114">Get connection information</span></span>

<span data-ttu-id="7c930-115">Vous devez obtenir la chaîne de connexion pour la base de données que vous avez créée quand vous avez effectué les étapes de [Création d’une base de données SQL Azure dans le portail Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7c930-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="7c930-116">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7c930-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="7c930-117">Sélectionnez **Bases de données SQL** dans le menu de gauche, puis sélectionnez votre base de données dans la page **Bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="7c930-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="7c930-118">Sélectionnez **Afficher les chaînes de connexion de la base de données** et copiez la chaîne de connexion **ADO.NET** complète.</span><span class="sxs-lookup"><span data-stu-id="7c930-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span>

    ![Copiez la chaîne de connexion ADO.NET.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="7c930-120">Définir la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="7c930-120">Set the connection string</span></span> 

<span data-ttu-id="7c930-121">Une application de fonction héberge l’exécution de vos fonctions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7c930-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="7c930-122">Il est recommandé de stocker les chaînes de connexion et autres secrets dans vos paramètres de conteneur de fonctions.</span><span class="sxs-lookup"><span data-stu-id="7c930-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="7c930-123">L’utilisation de paramètres d’application empêche la divulgation accidentelle de la chaîne de connexion avec votre code.</span><span class="sxs-lookup"><span data-stu-id="7c930-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="7c930-124">Accédez à l’application de fonction que vous avez créée dans [Créer une fonction dans Azure, qui est déclenchée par un minuteur](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="7c930-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="7c930-125">Sélectionnez **Fonctionnalités de la plateforme** > **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="7c930-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Paramètres de l’application pour l’application de fonction.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="7c930-127">Faites défiler jusqu’à **Chaînes de connexion** et ajoutez une chaîne de connexion en utilisant les paramètres spécifiés dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="7c930-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![Ajoutez une chaîne de connexion aux paramètres de l’application de fonction.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="7c930-129">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7c930-129">Setting</span></span>       | <span data-ttu-id="7c930-130">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="7c930-130">Suggested value</span></span> | <span data-ttu-id="7c930-131">Description</span><span class="sxs-lookup"><span data-stu-id="7c930-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="7c930-132">**Nom**</span><span class="sxs-lookup"><span data-stu-id="7c930-132">**Name**</span></span>  |  <span data-ttu-id="7c930-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="7c930-133">sqldb_connection</span></span>  | <span data-ttu-id="7c930-134">Utilisé pour accéder à la chaîne de connexion stockée dans le code de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="7c930-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="7c930-135">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="7c930-135">**Value**</span></span> | <span data-ttu-id="7c930-136">Chaîne copiée</span><span class="sxs-lookup"><span data-stu-id="7c930-136">Copied string</span></span>  | <span data-ttu-id="7c930-137">Collez la chaîne de connexion que vous avez copiée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="7c930-137">Past the connection string you copied in the previous section.</span></span> |
    | <span data-ttu-id="7c930-138">**Type**</span><span class="sxs-lookup"><span data-stu-id="7c930-138">**Type**</span></span> | <span data-ttu-id="7c930-139">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="7c930-139">SQL Database</span></span> | <span data-ttu-id="7c930-140">Utilisez la connexion SQL Database par défaut.</span><span class="sxs-lookup"><span data-stu-id="7c930-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="7c930-141">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="7c930-141">Click **Save**.</span></span>

<span data-ttu-id="7c930-142">À présent, vous pouvez ajouter le code de fonction C# qui se connecte à votre base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="7c930-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="7c930-143">Mettre à jour le code de votre fonction</span><span class="sxs-lookup"><span data-stu-id="7c930-143">Update your function code</span></span>

1. <span data-ttu-id="7c930-144">Dans votre application de fonction, sélectionnez la fonction déclenchée par un minuteur.</span><span class="sxs-lookup"><span data-stu-id="7c930-144">In your function app, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="7c930-145">Ajoutez les références d’assembly suivantes en haut du code de la fonction existante :</span><span class="sxs-lookup"><span data-stu-id="7c930-145">Add the following assembly references at the top of the existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="7c930-146">Ajoutez les instructions `using` suivantes à la fonction :</span><span class="sxs-lookup"><span data-stu-id="7c930-146">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="7c930-147">Remplacez la fonction **Run** existante par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="7c930-147">Replace the existing **Run** function with the following code:</span></span>
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
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="7c930-148">Cet exemple de commande met à jour la colonne **Status** en fonction de la date d’envoi.</span><span class="sxs-lookup"><span data-stu-id="7c930-148">This sample command updates the **Status** column based on the ship date.</span></span> <span data-ttu-id="7c930-149">Il doit mettre à jour 32 lignes de données.</span><span class="sxs-lookup"><span data-stu-id="7c930-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="7c930-150">Cliquez sur **Enregistrer**, surveillez l’exécution suivante de la fonction dans les fenêtres **Journaux**, puis notez le nombre de lignes mises à jour dans la table **SalesOrderHeader**.</span><span class="sxs-lookup"><span data-stu-id="7c930-150">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![Consultez les journaux des fonctions.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="7c930-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c930-152">Next steps</span></span>

<span data-ttu-id="7c930-153">Découvrez ensuite comment utiliser des fonctions avec Logic Apps pour s’intégrer à d’autres services.</span><span class="sxs-lookup"><span data-stu-id="7c930-153">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="7c930-154">Créer une fonction qui s’intègre avec Logic Apps</span><span class="sxs-lookup"><span data-stu-id="7c930-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="7c930-155">Pour plus d’informations sur Functions, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c930-155">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="7c930-156">Informations de référence pour les développeurs sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7c930-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="7c930-157">Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.</span><span class="sxs-lookup"><span data-stu-id="7c930-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="7c930-158">Test d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7c930-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="7c930-159">décrit plusieurs outils et techniques permettant de tester vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="7c930-159">Describes various tools and techniques for testing your functions.</span></span>  
