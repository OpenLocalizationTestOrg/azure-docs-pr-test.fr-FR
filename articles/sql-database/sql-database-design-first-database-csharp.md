---
title: "aaaDesign votre première Azure SQL database : C# | Documents Microsoft"
description: "En savoir plus toodesign votre première base de données SQL Azure et se connecter tooit avec un programme c# à l’aide d’ADO.NET."
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="609fd-103">Concevoir une base de données SQL Azure et se connecter avec C&#x23; et ADO.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="609fd-104">Base de données SQL Azure est un relationnel de base de données comme un service (DBaaS) Bonjour Microsoft Cloud (« Azure »).</span><span class="sxs-lookup"><span data-stu-id="609fd-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="609fd-105">Dans ce didacticiel, vous découvrez comment toouse hello portail Azure et ADO.NET avec Visual Studio pour :</span><span class="sxs-lookup"><span data-stu-id="609fd-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="609fd-106">Créer une base de données Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="609fd-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="609fd-107">Définir une règle de pare-feu de niveau serveur Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="609fd-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="609fd-108">Se connecter toohello de base de données avec ADO.NET et de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="609fd-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="609fd-109">Créer des tables avec ADO.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="609fd-110">Insérer, mettre à jour et supprimer des données avec ADO.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="609fd-111">Interroger les données avec ADO.NET</span><span class="sxs-lookup"><span data-stu-id="609fd-111">Query data ADO.NET</span></span>

<span data-ttu-id="609fd-112">Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="609fd-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="609fd-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="609fd-113">Prerequisites</span></span>

<span data-ttu-id="609fd-114">Une installation de [Visual Studio Community 2017, Visual Studio Professional 2017 ou Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="609fd-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="609fd-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="609fd-115">Next steps</span></span>

<span data-ttu-id="609fd-116">Dans ce didacticiel, vous avez appris les tâches de base de données telles que la création une base de données et les tables, charger et interroger des données et restaurer le point précédent du tooa hello de base de données dans le temps.</span><span class="sxs-lookup"><span data-stu-id="609fd-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="609fd-117">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="609fd-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="609fd-118">Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="609fd-118">Create a database</span></span>
> * <span data-ttu-id="609fd-119">Configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="609fd-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="609fd-120">Se connecter à base de données toohello avec [Visual Studio et Visual c#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="609fd-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="609fd-121">créez des tables</span><span class="sxs-lookup"><span data-stu-id="609fd-121">Create tables</span></span>
> * <span data-ttu-id="609fd-122">Insérer, mettre à jour et supprimer des données</span><span class="sxs-lookup"><span data-stu-id="609fd-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="609fd-123">Données de requête</span><span class="sxs-lookup"><span data-stu-id="609fd-123">Query data</span></span>

<span data-ttu-id="609fd-124">Avance toohello toolearn de didacticiel suivant sur la migration de vos données.</span><span class="sxs-lookup"><span data-stu-id="609fd-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="609fd-125">Migrer votre tooAzure de base de données SQL Server de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="609fd-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

