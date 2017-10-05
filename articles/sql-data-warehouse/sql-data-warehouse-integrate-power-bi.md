---
title: "Utiliser Power BI avec SQL Data Warehouse | Microsoft Docs"
description: "Conseils relatifs à l’utilisation de Power BI avec Azure SQL Data Warehouse pour le développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 4b7609fc5d6ce7bf0e3bd3ebf6d8f52e93a40a75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="50a73-103">Utiliser Power BI avec SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="50a73-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="50a73-104">À l’instar de la Base de données SQL Azure, la fonction de connexion directe de SQL Data Warehouse permet à l’utilisateur de tirer parti d’une capacité de transfert logique performante, ainsi que des fonctionnalités d’analyse de Power BI.</span><span class="sxs-lookup"><span data-stu-id="50a73-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user to leverage powerful logical pushdown alongside the analytical capabilities of Power BI.</span></span>  <span data-ttu-id="50a73-105">Grâce à la connexion directe, les requêtes sont renvoyées vers votre solution Azure SQL Data Warehouse en temps réel lorsque vous explorez les données.</span><span class="sxs-lookup"><span data-stu-id="50a73-105">With Direct Connect, queries are sent back to your Azure SQL Data Warehouse in real time as you explore the data.</span></span>  <span data-ttu-id="50a73-106">Combinée à la puissance de SQL Data Warehouse, cette fonction permet aux utilisateurs de créer des rapports dynamiques en quelques minutes pour plusieurs téraoctets de données.</span><span class="sxs-lookup"><span data-stu-id="50a73-106">This, combined with the scale of SQL Data Warehouse, enables users to create dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="50a73-107">En outre, l’introduction du bouton Open in Power BI permet aux utilisateurs de connecter directement Power BI à leur solution SQL Data Warehouse sans collecter d’informations à partir d’autres sections d’Azure.</span><span class="sxs-lookup"><span data-stu-id="50a73-107">In addition, the introduction of the Open in Power BI button allows users to directly connect Power BI to their SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="50a73-108">Lorsque vous utilisez la connexion directe, notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="50a73-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="50a73-109">Spécifiez le nom de serveur complet lors de la connexion (voir ci-dessous pour plus de détails).</span><span class="sxs-lookup"><span data-stu-id="50a73-109">Specify the fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="50a73-110">Vérifiez que les règles de pare-feu relatives à la base de données sont configurées sur « Autoriser l’accès aux services Azure ».</span><span class="sxs-lookup"><span data-stu-id="50a73-110">Ensure firewall rules for the database are configured to "Allow access to Azure services".</span></span>
* <span data-ttu-id="50a73-111">Chaque action, telle que la sélection d’une colonne ou l’ajout d’un filtre, interroge directement l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="50a73-111">Every action such as selecting a column or adding a filter will  directly query the data warehouse</span></span>
* <span data-ttu-id="50a73-112">Les vignettes sont actualisées environ toutes les 15 minutes (il n’est donc pas nécessaire de planifier l’actualisation).</span><span class="sxs-lookup"><span data-stu-id="50a73-112">Tiles are refreshed approximately every 15 minutes (refresh does not need to be scheduled)</span></span>
* <span data-ttu-id="50a73-113">Les Questions et réponses ne sont pas disponibles pour les jeux de données de connexion directe.</span><span class="sxs-lookup"><span data-stu-id="50a73-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="50a73-114">Les modifications de schéma ne sont pas récupérées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="50a73-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="50a73-115">Toutes les requêtes de connexion directe expireront après 2 minutes.</span><span class="sxs-lookup"><span data-stu-id="50a73-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="50a73-116">Ces restrictions et remarques sont susceptibles de changer, car nous améliorons continuellement les expériences.</span><span class="sxs-lookup"><span data-stu-id="50a73-116">These restrictions and notes may change as we continue to improve the experiences.</span></span> <span data-ttu-id="50a73-117">Les étapes de connexion sont détaillées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="50a73-117">The steps to connect are detailed below.</span></span>  

## <a name="using-the-open-in-power-bi-button"></a><span data-ttu-id="50a73-118">Utilisation du bouton « Open in Power BI »</span><span class="sxs-lookup"><span data-stu-id="50a73-118">Using the ‘Open in Power BI’ button</span></span>
<span data-ttu-id="50a73-119">La méthode la plus simple pour basculer entre SQL Data Warehouse et Power BI consiste à utiliser le bouton Open in Power BI.</span><span class="sxs-lookup"><span data-stu-id="50a73-119">The easiest way to move between your SQL Data Warehouse and Power BI is with the Open in Power BI button.</span></span> <span data-ttu-id="50a73-120">Ce bouton vous permet de commencer à créer des tableaux de bord en toute transparence dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="50a73-120">This button allows you to seamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="50a73-121">Pour démarrer, accédez à votre instance SQL Data Warehouse dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="50a73-121">To get started navigate to your SQL Data Warehouse instance in the Azure Classic Portal.</span></span>
2. <span data-ttu-id="50a73-122">Cliquez sur le bouton Open in Power BI.</span><span class="sxs-lookup"><span data-stu-id="50a73-122">Click the 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="50a73-123">Si nous ne sommes pas en mesure de vous connecter directement, ou que vous ne disposez pas d’un compte Power BI, vous devrez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="50a73-123">If we are not able to sign you in directly, or if you do not have a Power BI account, you will need to sign-in.</span></span>  
4. <span data-ttu-id="50a73-124">Vous serez alors dirigé vers la page de connexion SQL Data Warehouse, préremplie avec les informations de votre instance SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="50a73-124">You will be directed to the SQL Data Warehouse connection page, with the information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="50a73-125">Après avoir entré vos informations d’identification, vous serez complètement connecté à votre instance SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="50a73-125">After entering your credentials you will be fully connected to your SQL Data Warehouse.</span></span>

## <a name="connecting-through-the-power-bi-portal"></a><span data-ttu-id="50a73-126">Connexion par le biais du portail Power BI</span><span class="sxs-lookup"><span data-stu-id="50a73-126">Connecting through the Power BI portal</span></span>
<span data-ttu-id="50a73-127">Outre l’utilisation du bouton Open in Power BI, les utilisateurs peuvent se connecter à leur instance SQL Data Warehouse au moyen du portail Power BI.</span><span class="sxs-lookup"><span data-stu-id="50a73-127">In addition to using the Open in Power BI button, users can also connect to their SQL Data Warehouse through the Power BI Portal.</span></span>

1. <span data-ttu-id="50a73-128">En bas du volet de navigation, cliquez sur « Obtenir des données ».</span><span class="sxs-lookup"><span data-stu-id="50a73-128">Click 'Get Data' at the bottom of the navigation pane.</span></span>
2. <span data-ttu-id="50a73-129">Sélectionnez « Bases de données ».</span><span class="sxs-lookup"><span data-stu-id="50a73-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="50a73-130">Une fois sur la page des bases de données, sélectionnez « Entrepôt de données SQL Azure », puis cliquez sur « Se connecter ».</span><span class="sxs-lookup"><span data-stu-id="50a73-130">Once on the Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="50a73-131">Entrez les informations de connexion nécessaires.</span><span class="sxs-lookup"><span data-stu-id="50a73-131">Enter the necessary connection information.</span></span>  <span data-ttu-id="50a73-132">Le nom de serveur et le nom de base de données sont spécifiés dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="50a73-132">Your server name and database name can be found in the Azure Portal.</span></span>
5. <span data-ttu-id="50a73-133">Vous serez redirigé vers la page d’accueil de Power BI et, une fois que vous serez connecté, une nouvelle entrée sous « Jeu de données » s’affichera avec le nom de votre instance.</span><span class="sxs-lookup"><span data-stu-id="50a73-133">You will be directed back to the main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with the name of your instance.</span></span>  
6. <span data-ttu-id="50a73-134">Vous pouvez cliquer sur le nouveau jeu de données pour explorer toutes les tables et les affichages dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="50a73-134">You can click on the new dataset to explore all of the tables and views in your database.</span></span> <span data-ttu-id="50a73-135">La sélection d’une colonne renverra une requête à la source, ce qui entraînera la création dynamique de votre élément visuel.</span><span class="sxs-lookup"><span data-stu-id="50a73-135">Selecting a column will send a query back to the source, dynamically creating your visual.</span></span> <span data-ttu-id="50a73-136">Ces éléments visuels peuvent être enregistrés dans un nouveau rapport, puis ré-épinglés dans votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="50a73-136">These visuals can be saved in a new report and pinned back to your dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
