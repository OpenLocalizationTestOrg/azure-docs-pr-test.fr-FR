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
# <a name="get-started-with-hello-azure-sql-database-connector"></a><span data-ttu-id="148f2-103">Prise en main connecteur de base de données SQL Azure hello</span><span class="sxs-lookup"><span data-stu-id="148f2-103">Get started with hello Azure SQL Database connector</span></span>
<span data-ttu-id="148f2-104">À l’aide du connecteur de base de données SQL Azure hello, créer des flux de travail pour votre organisation qui gèrent les données de vos tables.</span><span class="sxs-lookup"><span data-stu-id="148f2-104">Using hello Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="148f2-105">Avec Base de données SQL, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="148f2-105">With SQL Database, you:</span></span>

* <span data-ttu-id="148f2-106">Créer votre flux de travail en ajoutant une nouvelle base de données client tooa clients ou une commande dans une base de données des commandes de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="148f2-106">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="148f2-107">Utilisez les actions tooget une ligne de données, insérer une nouvelle ligne, ou les supprimer.</span><span class="sxs-lookup"><span data-stu-id="148f2-107">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="148f2-108">Par exemple, quand un enregistrement est créé dans Dynamics CRM Online (déclencheur), insérez une ligne dans une base de données SQL Azure (action).</span><span class="sxs-lookup"><span data-stu-id="148f2-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="148f2-109">Cette rubrique vous montre comment toouse hello connecteur de base de données SQL dans une application logique, et également les listes hello actions.</span><span class="sxs-lookup"><span data-stu-id="148f2-109">This topic shows you how toouse hello SQL Database connector in a logic app, and also lists hello actions.</span></span>

<span data-ttu-id="148f2-110">toolearn en savoir plus sur les applications de la logique, consultez [quelles sont les applications logique](../logic-apps/logic-apps-what-are-logic-apps.md) et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="148f2-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-sql-database"></a><span data-ttu-id="148f2-111">Se connecter tooAzure base de données SQL</span><span class="sxs-lookup"><span data-stu-id="148f2-111">Connect tooAzure SQL Database</span></span>
<span data-ttu-id="148f2-112">Avant que votre application logique peut accéder à n’importe quel service, vous créez tout d’abord un *connexion* toohello service.</span><span class="sxs-lookup"><span data-stu-id="148f2-112">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="148f2-113">Une connexion permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="148f2-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="148f2-114">Par exemple, tooconnect tooSQL base de données, vous tout d’abord créez une base de données SQL *connexion*.</span><span class="sxs-lookup"><span data-stu-id="148f2-114">For example, tooconnect tooSQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="148f2-115">toocreate une connexion, vous entrez les informations d’identification hello que vous utilisez normalement le service de hello tooaccess à que vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="148f2-115">toocreate a connection, you enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="148f2-116">Par conséquent, dans la base de données SQL, entrez votre connexion de base de données SQL informations d’identification toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="148f2-116">So, in SQL Database, enter your SQL Database credentials toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="148f2-117">Créer la connexion de hello</span><span class="sxs-lookup"><span data-stu-id="148f2-117">Create hello connection</span></span>
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="148f2-118">Utilisation d’un déclencheur</span><span class="sxs-lookup"><span data-stu-id="148f2-118">Use a trigger</span></span>
<span data-ttu-id="148f2-119">Ce connecteur ne possède aucun déclencheur.</span><span class="sxs-lookup"><span data-stu-id="148f2-119">This connector does not have any triggers.</span></span> <span data-ttu-id="148f2-120">Utilisez l’autre application logique de déclencheurs toostart hello, comme un déclencheur de périodicité, un déclencheur HTTP Webhook, déclencheurs disponibles avec tous les autres connecteurs et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="148f2-120">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="148f2-121">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md) vous fournit un exemple.</span><span class="sxs-lookup"><span data-stu-id="148f2-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="148f2-122">Utilisation d’une action</span><span class="sxs-lookup"><span data-stu-id="148f2-122">Use an action</span></span>
<span data-ttu-id="148f2-123">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="148f2-123">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="148f2-124">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="148f2-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="148f2-125">Sélectionnez le signe plus hello.</span><span class="sxs-lookup"><span data-stu-id="148f2-125">Select hello plus sign.</span></span> <span data-ttu-id="148f2-126">Vous voyez plusieurs choix : **ajouter une action**, **ajouter une condition**, ou l’un des hello **plus** options.</span><span class="sxs-lookup"><span data-stu-id="148f2-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="148f2-127">Choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="148f2-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="148f2-128">Dans la zone de texte hello, tapez « sql » tooget une liste de toutes les actions disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="148f2-128">In hello text box, type “sql” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="148f2-129">Dans notre exemple, choisissez **SQL Server - Obtenir une ligne**.</span><span class="sxs-lookup"><span data-stu-id="148f2-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="148f2-130">Si une connexion existe déjà, puis sélectionnez hello **nom de la Table** dans hello de liste déroulante de liste, puis entrez les hello **ID de ligne** vous souhaitez tooreturn.</span><span class="sxs-lookup"><span data-stu-id="148f2-130">If a connection already exists, then select hello **Table name** from hello drop-down list, and enter hello **Row ID** you want tooreturn.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="148f2-131">Si vous êtes invité hello informations de connexion, puis entrez connexion de hello toocreate hello détails.</span><span class="sxs-lookup"><span data-stu-id="148f2-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="148f2-132">[Créer la connexion de hello](connectors-create-api-sqlazure.md#create-the-connection) dans cette rubrique décrit ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="148f2-132">[Create hello connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="148f2-133">Dans cet exemple, nous obtiendrons une ligne d’une table.</span><span class="sxs-lookup"><span data-stu-id="148f2-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="148f2-134">données de hello toosee dans cette ligne, ajoutez une autre action qui crée un fichier à l’aide des champs hello à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="148f2-134">toosee hello data in this row, add another action that creates a file using hello fields from hello table.</span></span> <span data-ttu-id="148f2-135">Par exemple, ajouter une action de OneDrive qui utilise hello FirstName et LastName champs toocreate un nouveau fichier dans le compte de stockage cloud hello.</span><span class="sxs-lookup"><span data-stu-id="148f2-135">For example, add a OneDrive action that uses hello FirstName and LastName fields toocreate a new file in hello cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="148f2-136">**Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello).</span><span class="sxs-lookup"><span data-stu-id="148f2-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="148f2-137">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="148f2-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="148f2-138">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="148f2-138">Connector-specific details</span></span>

<span data-ttu-id="148f2-139">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="148f2-139">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="148f2-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="148f2-140">Next steps</span></span>
<span data-ttu-id="148f2-141">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="148f2-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="148f2-142">Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="148f2-142">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

