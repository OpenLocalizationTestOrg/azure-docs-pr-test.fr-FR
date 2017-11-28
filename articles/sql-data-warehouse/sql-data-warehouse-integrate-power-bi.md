---
title: "aaaUse Power BI avec l’entrepôt de données SQL | Documents Microsoft"
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
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="f06bf-103">Utiliser Power BI avec SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f06bf-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="f06bf-104">Comme avec la base de données SQL Azure, entrepôt de données du SQL directe Connect permet utilisateur tooleverage puissante logique poussée vers le bas en même temps que les fonctions d’analyse hello de Power BI.</span><span class="sxs-lookup"><span data-stu-id="f06bf-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user tooleverage powerful logical pushdown alongside hello analytical capabilities of Power BI.</span></span>  <span data-ttu-id="f06bf-105">Avec la connexion directe, requêtes sont envoyées tooyour arrière Azure SQL Data Warehouse en temps réel que vous explorez les données hello.</span><span class="sxs-lookup"><span data-stu-id="f06bf-105">With Direct Connect, queries are sent back tooyour Azure SQL Data Warehouse in real time as you explore hello data.</span></span>  <span data-ttu-id="f06bf-106">Ceci, combiné avec échelle hello SQL Data Warehouse, permet aux utilisateurs des rapports dynamiques toocreate en minutes par rapport à plusieurs téraoctets de données.</span><span class="sxs-lookup"><span data-stu-id="f06bf-106">This, combined with hello scale of SQL Data Warehouse, enables users toocreate dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="f06bf-107">En outre, introduction hello Hello ouvrir du bouton Power BI permet aux utilisateurs toodirectly se connecter à Power BI tootheir SQL Data Warehouse sans recueillir des informations à partir d’autres parties de Azure.</span><span class="sxs-lookup"><span data-stu-id="f06bf-107">In addition, hello introduction of hello Open in Power BI button allows users toodirectly connect Power BI tootheir SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="f06bf-108">Lorsque vous utilisez la connexion directe, notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="f06bf-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="f06bf-109">Spécifiez le nom du serveur complet hello lors de la connexion (voir ci-dessous pour plus de détails)</span><span class="sxs-lookup"><span data-stu-id="f06bf-109">Specify hello fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="f06bf-110">Que les règles de pare-feu de base de données hello sont configurés trop « autorisent l’accès tooAzure services ».</span><span class="sxs-lookup"><span data-stu-id="f06bf-110">Ensure firewall rules for hello database are configured too"Allow access tooAzure services".</span></span>
* <span data-ttu-id="f06bf-111">Toutes les actions telles que la sélection d’une colonne ou l’ajout d’un filtre sont interroge directement l’entrepôt de données hello</span><span class="sxs-lookup"><span data-stu-id="f06bf-111">Every action such as selecting a column or adding a filter will  directly query hello data warehouse</span></span>
* <span data-ttu-id="f06bf-112">Les vignettes sont actualisées environ toutes les 15 minutes (actualisation n’est pas nécessaire toobe planifiée)</span><span class="sxs-lookup"><span data-stu-id="f06bf-112">Tiles are refreshed approximately every 15 minutes (refresh does not need toobe scheduled)</span></span>
* <span data-ttu-id="f06bf-113">Les Questions et réponses ne sont pas disponibles pour les jeux de données de connexion directe.</span><span class="sxs-lookup"><span data-stu-id="f06bf-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="f06bf-114">Les modifications de schéma ne sont pas récupérées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f06bf-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="f06bf-115">Toutes les requêtes de connexion directe expireront après 2 minutes.</span><span class="sxs-lookup"><span data-stu-id="f06bf-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="f06bf-116">Ces restrictions et les notes peuvent changer à mesure que nous tooimprove hello expériences.</span><span class="sxs-lookup"><span data-stu-id="f06bf-116">These restrictions and notes may change as we continue tooimprove hello experiences.</span></span> <span data-ttu-id="f06bf-117">Hello étapes tooconnect sont détaillées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f06bf-117">hello steps tooconnect are detailed below.</span></span>  

## <a name="using-hello-open-in-power-bi-button"></a><span data-ttu-id="f06bf-118">À l’aide du bouton « Ouvrir dans Power BI » de hello</span><span class="sxs-lookup"><span data-stu-id="f06bf-118">Using hello ‘Open in Power BI’ button</span></span>
<span data-ttu-id="f06bf-119">Hello toomove de façon plus simple entre votre entrepôt de données SQL et de Power BI est hello ouvrir du bouton Power BI.</span><span class="sxs-lookup"><span data-stu-id="f06bf-119">hello easiest way toomove between your SQL Data Warehouse and Power BI is with hello Open in Power BI button.</span></span> <span data-ttu-id="f06bf-120">Ce bouton vous permet de tooseamlessly commencer à créer de nouveaux tableaux de bord dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="f06bf-120">This button allows you tooseamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="f06bf-121">tooget démarré accédez l’instance de SQL Data Warehouse tooyour Bonjour portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="f06bf-121">tooget started navigate tooyour SQL Data Warehouse instance in hello Azure Classic Portal.</span></span>
2. <span data-ttu-id="f06bf-122">Cliquez sur le bouton « Ouvrir dans Power BI » de hello.</span><span class="sxs-lookup"><span data-stu-id="f06bf-122">Click hello 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="f06bf-123">Si nous ne sommes pas en mesure de toosign dans directement, ou si vous n’avez pas un compte Power BI, vous devez toosign dans.</span><span class="sxs-lookup"><span data-stu-id="f06bf-123">If we are not able toosign you in directly, or if you do not have a Power BI account, you will need toosign-in.</span></span>  
4. <span data-ttu-id="f06bf-124">Vous allez être redirigé toohello page de connexion de l’entrepôt de données SQL, avec les informations de hello de votre entrepôt de données SQL est préremplie.</span><span class="sxs-lookup"><span data-stu-id="f06bf-124">You will be directed toohello SQL Data Warehouse connection page, with hello information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="f06bf-125">Après avoir entré vos informations d’identification, vous serez totalement connecté tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f06bf-125">After entering your credentials you will be fully connected tooyour SQL Data Warehouse.</span></span>

## <a name="connecting-through-hello-power-bi-portal"></a><span data-ttu-id="f06bf-126">Connexion via le portail de Power BI hello</span><span class="sxs-lookup"><span data-stu-id="f06bf-126">Connecting through hello Power BI portal</span></span>
<span data-ttu-id="f06bf-127">Bonjour toousing plus ouvrir du bouton Power BI, les utilisateurs peuvent également connecter tootheir SQL Data Warehouse via hello portail Power BI.</span><span class="sxs-lookup"><span data-stu-id="f06bf-127">In addition toousing hello Open in Power BI button, users can also connect tootheir SQL Data Warehouse through hello Power BI Portal.</span></span>

1. <span data-ttu-id="f06bf-128">Cliquez sur « Obtenir les données » en bas de hello hello du volet de navigation.</span><span class="sxs-lookup"><span data-stu-id="f06bf-128">Click 'Get Data' at hello bottom of hello navigation pane.</span></span>
2. <span data-ttu-id="f06bf-129">Sélectionnez « Bases de données ».</span><span class="sxs-lookup"><span data-stu-id="f06bf-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="f06bf-130">Une fois sur la page de bases de données hello, sélectionnez Azure SQL Data Warehouse, puis sur « Se connecter ».</span><span class="sxs-lookup"><span data-stu-id="f06bf-130">Once on hello Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="f06bf-131">Entrez les informations de connexion nécessaires hello.</span><span class="sxs-lookup"><span data-stu-id="f06bf-131">Enter hello necessary connection information.</span></span>  <span data-ttu-id="f06bf-132">Votre nom de serveur et le nom de la base de données sont accessibles dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f06bf-132">Your server name and database name can be found in hello Azure Portal.</span></span>
5. <span data-ttu-id="f06bf-133">Vous serez dirigé précédent toohello la page principale de Power BI et une fois que votre connexion est établie à une nouvelle entrée sous « Jeux de données » s’affiche avec le nom hello de votre instance.</span><span class="sxs-lookup"><span data-stu-id="f06bf-133">You will be directed back toohello main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with hello name of your instance.</span></span>  
6. <span data-ttu-id="f06bf-134">Vous pouvez cliquer sur hello nouveau dataset tooexplore toutes les tables de hello et des vues dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="f06bf-134">You can click on hello new dataset tooexplore all of hello tables and views in your database.</span></span> <span data-ttu-id="f06bf-135">Sélection d’une colonne enverra une source toohello précédent de requête, créant ainsi dynamiquement votre élément visuel.</span><span class="sxs-lookup"><span data-stu-id="f06bf-135">Selecting a column will send a query back toohello source, dynamically creating your visual.</span></span> <span data-ttu-id="f06bf-136">Ces éléments visuels peuvent être enregistrés dans un nouveau rapport et épinglés dans tooyour le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f06bf-136">These visuals can be saved in a new report and pinned back tooyour dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
