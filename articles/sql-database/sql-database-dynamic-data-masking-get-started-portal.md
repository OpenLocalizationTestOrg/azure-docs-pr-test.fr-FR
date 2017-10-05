---
title: "Portail Azure : masquage de données dynamiques de base de données SQL | Microsoft Docs"
description: "Guide de prise en main du masquage des données dynamiques de base de données SQL dans le portail Azure"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 15184e14d4e1e23b56126bbf9f972c1619dcba80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-the-azure-portal"></a><span data-ttu-id="78c9d-103">Prise en main du masquage des données dynamiques de base de données SQL dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="78c9d-103">Get started with SQL Database dynamic data masking with the Azure Portal</span></span>

<span data-ttu-id="78c9d-104">Cette rubrique vous montre comment implémenter [le masquage des données dynamiques](sql-database-dynamic-data-masking-get-started.md) avec le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="78c9d-104">This topic shows you how to implement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with the Azure portal.</span></span> <span data-ttu-id="78c9d-105">Vous pouvez également implémenter le masquage de données dynamique avec les [applets de commande de base de données Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou [l’API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="78c9d-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-the-azure-portal"></a><span data-ttu-id="78c9d-106">Configuration du masquage des données dynamiques pour votre base de données à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="78c9d-106">Set up dynamic data masking for your database using the Azure Portal</span></span>
1. <span data-ttu-id="78c9d-107">Accédez à l’adresse [https://portal.azure.com](https://portal.azure.com)et exécutez le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="78c9d-107">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="78c9d-108">Accédez au volet des paramètres de la base de données comprenant les données sensibles que vous souhaitez masquer.</span><span class="sxs-lookup"><span data-stu-id="78c9d-108">Navigate to the settings blade of the database that includes the sensitive data you want to mask.</span></span>
3. <span data-ttu-id="78c9d-109">Cliquez sur la vignette **Dynamic Data Masking** qui lance le panneau de configuration **Dynamic Data Masking**.</span><span class="sxs-lookup"><span data-stu-id="78c9d-109">Click the **Dynamic Data Masking** tile which launches the **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="78c9d-110">Vous pouvez également faire défiler vers le bas vers la section **Opérations** et cliquer sur **Dynamic Data Masking**.</span><span class="sxs-lookup"><span data-stu-id="78c9d-110">Alternatively, you can scroll down to the **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="78c9d-112">Dans le volet de configuration **Masquage des données dynamiques** , certaines colonnes de base de données ont été indiquées par le moteur de recommandations pour le masquage.</span><span class="sxs-lookup"><span data-stu-id="78c9d-112">In the **Dynamic Data Masking** configuration blade you may see some database columns that the recommendations engine has flagged for masking.</span></span> <span data-ttu-id="78c9d-113">Pour accepter les recommandations, cliquez simplement sur **Ajouter un masque** pour une ou plusieurs colonnes et un masque sera créé en fonction du type par défaut pour cette colonne.</span><span class="sxs-lookup"><span data-stu-id="78c9d-113">In order to accept the recommendations, just click **Add Mask** for one or more columns and a mask will be created based on the default type for this column.</span></span> <span data-ttu-id="78c9d-114">Vous pouvez modifier la fonction de masquage en cliquant sur la règle de masquage et en modifiant le format du champ de masquage pour un format différent de votre choix.</span><span class="sxs-lookup"><span data-stu-id="78c9d-114">You can change the masking function by clicking on the masking rule and editing the masking field format to a different format of your choice.</span></span> <span data-ttu-id="78c9d-115">N'oubliez pas de cliquer sur **Enregistrer** pour enregistrer vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="78c9d-115">Be sure to click **Save** to save your settings.</span></span>
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="78c9d-117">Pour ajouter un masque pour une colonne de votre base de données, au sommet du panneau de configuration **Dynamic Data Masking**, cliquez sur **Ajouter un masque** pour ouvrir le panneau de configuration **Ajouter une règle de masquage**.</span><span class="sxs-lookup"><span data-stu-id="78c9d-117">To add a mask for any column in your database, at the top of the **Dynamic Data Masking** configuration blade click **Add Mask** to open the **Add Masking Rule** configuration blade</span></span>
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="78c9d-119">Sélectionnez le **Schéma**, la **Table** et la **Colonne** pour définir les champs désignés qui seront masqués.</span><span class="sxs-lookup"><span data-stu-id="78c9d-119">Select the **Schema**, **Table** and **Column** to define the designated field that will be masked.</span></span>
7. <span data-ttu-id="78c9d-120">Choisissez un **Format de champ de masquage** dans la liste des catégories de masquage des données sensibles.</span><span class="sxs-lookup"><span data-stu-id="78c9d-120">Choose a **Masking Field Format** from the list of sensitive data masking categories.</span></span>
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="78c9d-122">Cliquez sur **Enregistrer** dans le panneau des règles de masquage pour mettre à jour l'ensemble des règles de la stratégie de masquage des données dynamiques.</span><span class="sxs-lookup"><span data-stu-id="78c9d-122">Click **Save** in the data masking rule blade to update the set of masking rules in the dynamic data masking policy.</span></span>
9. <span data-ttu-id="78c9d-123">Tapez les utilisateurs SQL ou les identités AAD à exclure du masquage et qui doivent avoir accès aux données sensibles non masquées.</span><span class="sxs-lookup"><span data-stu-id="78c9d-123">Type the SQL users or AAD identities that should be excluded from masking, and have access to the unmasked sensitive data.</span></span> <span data-ttu-id="78c9d-124">La liste d'utilisateurs doit être délimitée par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="78c9d-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="78c9d-125">Les utilisateurs disposant de privilèges administrateur ont toujours accès aux données d'origine non masquées.</span><span class="sxs-lookup"><span data-stu-id="78c9d-125">Note that users with administrator privileges always have access to the original unmasked data.</span></span>
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="78c9d-127">Pour que la couche d'application puisse afficher des données sensibles aux utilisateurs d'application privilégiés, ajoutez l'utilisateur SQL ou l'identité AAD qu'utilise l'application pour interroger la base de données.</span><span class="sxs-lookup"><span data-stu-id="78c9d-127">To make it so the application layer can display sensitive data for application privileged users, add the SQL user or AAD identity the application uses to query the database.</span></span> <span data-ttu-id="78c9d-128">Il est vivement recommandé de limiter le nombre d'utilisateurs privilégiés dans cette liste afin de limiter l'exposition des données sensibles.</span><span class="sxs-lookup"><span data-stu-id="78c9d-128">It is highly recommended that this list contain a minimal number of privileged users to minimize exposure of the sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="78c9d-129">Cliquez sur **Enregistrer** dans le panneau de configuration du masquage des données afin d'enregistrer la stratégie de masquage, nouvelle ou mise à jour.</span><span class="sxs-lookup"><span data-stu-id="78c9d-129">Click **Save** in the data masking configuration blade to save the new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="78c9d-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="78c9d-130">Next steps</span></span>

* <span data-ttu-id="78c9d-131">Pour une vue d’ensemble du masquage des données dynamiques, consultez [Masquage des données dynamiques](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="78c9d-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="78c9d-132">Vous pouvez également implémenter le masquage de données dynamique avec les [applets de commande de base de données Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou [l’API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="78c9d-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>