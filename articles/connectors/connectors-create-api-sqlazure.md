---
title: "Ajouter le connecteur de base de données SQL Azure à vos applications logiques | Microsoft Docs"
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
ms.openlocfilehash: a3d5cb909dbfcb00f3fbfa0165bb6cd58eb18688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-sql-database-connector"></a><span data-ttu-id="34f47-103">Prise en main du connecteur de base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="34f47-103">Get started with the Azure SQL Database connector</span></span>
<span data-ttu-id="34f47-104">Créez des flux de travail pour votre organisation destinés à gérer les données dans vos tables à l’aide du connecteur de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="34f47-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="34f47-105">Avec Base de données SQL, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="34f47-105">With SQL Database, you:</span></span>

* <span data-ttu-id="34f47-106">Créez votre flux de travail en ajoutant un nouveau client à une base de données clients ou en mettant à jour une commande dans une base de données de commandes.</span><span class="sxs-lookup"><span data-stu-id="34f47-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="34f47-107">Utilisez des actions pour obtenir une ligne de données, insérer une nouvelle ligne ou en supprimer.</span><span class="sxs-lookup"><span data-stu-id="34f47-107">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="34f47-108">Par exemple, quand un enregistrement est créé dans Dynamics CRM Online (déclencheur), insérez une ligne dans une base de données SQL Azure (action).</span><span class="sxs-lookup"><span data-stu-id="34f47-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="34f47-109">Cette rubrique explique comment utiliser le connecteur SQL Database dans une application logique, et répertorie les actions.</span><span class="sxs-lookup"><span data-stu-id="34f47-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span></span>

<span data-ttu-id="34f47-110">Pour plus d’informations sur Logic Apps, voir [Qu’est-ce qu’une application logique ?](../logic-apps/logic-apps-what-are-logic-apps.md) et [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="34f47-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-sql-database"></a><span data-ttu-id="34f47-111">Connexion à la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="34f47-111">Connect to Azure SQL Database</span></span>
<span data-ttu-id="34f47-112">Pour que votre application logique puisse accéder à un service, vous devez d’abord créer une *connexion* à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="34f47-112">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="34f47-113">Une connexion permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="34f47-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="34f47-114">Par exemple, pour vous connecter à SQL Database, vous devez commencer par créer une *connexion* SQL Database.</span><span class="sxs-lookup"><span data-stu-id="34f47-114">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="34f47-115">Pour créer une connexion, entrez les informations d’identification que vous utilisez généralement pour accéder au service auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="34f47-115">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="34f47-116">Ensuite, dans la base de données SQL, entrez vos informations d’identification de base de données SQL pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="34f47-116">So, in SQL Database, enter your SQL Database credentials to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="34f47-117">Créer la connexion</span><span class="sxs-lookup"><span data-stu-id="34f47-117">Create the connection</span></span>
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="34f47-118">Utilisation d’un déclencheur</span><span class="sxs-lookup"><span data-stu-id="34f47-118">Use a trigger</span></span>
<span data-ttu-id="34f47-119">Ce connecteur ne possède aucun déclencheur.</span><span class="sxs-lookup"><span data-stu-id="34f47-119">This connector does not have any triggers.</span></span> <span data-ttu-id="34f47-120">Utilisez d’autres déclencheurs pour démarrer l’application logique, notamment un déclencheur de périodicité, un déclencheur Webhook HTTP, des déclencheurs disponibles avec d’autres connecteurs, etc.</span><span class="sxs-lookup"><span data-stu-id="34f47-120">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="34f47-121">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md) vous fournit un exemple.</span><span class="sxs-lookup"><span data-stu-id="34f47-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="34f47-122">Utilisation d’une action</span><span class="sxs-lookup"><span data-stu-id="34f47-122">Use an action</span></span>
<span data-ttu-id="34f47-123">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="34f47-123">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="34f47-124">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="34f47-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="34f47-125">Sélectionnez le signe plus.</span><span class="sxs-lookup"><span data-stu-id="34f47-125">Select the plus sign.</span></span> <span data-ttu-id="34f47-126">Vous disposez de plusieurs options : **Ajouter une action**, **Ajouter une condition** ou l’une des options **Plus**.</span><span class="sxs-lookup"><span data-stu-id="34f47-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="34f47-127">Choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="34f47-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="34f47-128">Dans la zone de texte, saisissez « sql » pour obtenir la liste de toutes les actions disponibles.</span><span class="sxs-lookup"><span data-stu-id="34f47-128">In the text box, type “sql” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="34f47-129">Dans notre exemple, choisissez **SQL Server - Obtenir une ligne**.</span><span class="sxs-lookup"><span data-stu-id="34f47-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="34f47-130">S’il existe déjà une connexion, sélectionnez le **nom de la table** dans la liste déroulante, puis entrez l’**ID de ligne** à retourner.</span><span class="sxs-lookup"><span data-stu-id="34f47-130">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="34f47-131">Si vous êtes invité à saisir les informations de connexion, entrez les informations requises pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="34f47-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="34f47-132">La section [Créer la connexion](connectors-create-api-sqlazure.md#create-the-connection) dans cette rubrique décrit ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="34f47-132">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="34f47-133">Dans cet exemple, nous obtiendrons une ligne d’une table.</span><span class="sxs-lookup"><span data-stu-id="34f47-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="34f47-134">Pour consulter les données de cette ligne, ajoutez une autre action qui crée un fichier en utilisant les champs de la table.</span><span class="sxs-lookup"><span data-stu-id="34f47-134">To see the data in this row, add another action that creates a file using the fields from the table.</span></span> <span data-ttu-id="34f47-135">Par exemple, ajoutez une action OneDrive qui utilise les champs FirstName et LastName pour créer un nouveau fichier dans le compte de stockage cloud.</span><span class="sxs-lookup"><span data-stu-id="34f47-135">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="34f47-136">**Enregistrez** vos modifications (dans le coin supérieur gauche de la barre d’outils).</span><span class="sxs-lookup"><span data-stu-id="34f47-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="34f47-137">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="34f47-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="34f47-138">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="34f47-138">Connector-specific details</span></span>

<span data-ttu-id="34f47-139">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="34f47-139">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="34f47-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="34f47-140">Next steps</span></span>
<span data-ttu-id="34f47-141">[Créez une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="34f47-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="34f47-142">Explorez les autres connecteurs disponibles dans les applications logiques en consultant notre [liste d’API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="34f47-142">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

