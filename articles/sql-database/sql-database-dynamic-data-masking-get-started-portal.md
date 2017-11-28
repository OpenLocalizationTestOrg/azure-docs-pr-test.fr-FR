---
title: "Portail Azure : masquage de données dynamiques de base de données SQL | Microsoft Docs"
description: "Comment tooget démarrer avec la base de données SQL masquage dynamique des données Bonjour portail Azure"
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
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a><span data-ttu-id="e335d-103">Prise en main de la base de données SQL masquage dynamique des données avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e335d-103">Get started with SQL Database dynamic data masking with hello Azure Portal</span></span>

<span data-ttu-id="e335d-104">Cette rubrique vous montre comment tooimplement [masquage dynamique des données](sql-database-dynamic-data-masking-get-started.md) avec hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e335d-104">This topic shows you how tooimplement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with hello Azure portal.</span></span> <span data-ttu-id="e335d-105">Vous pouvez également implémenter à l’aide du masquage dynamique des données [applets de commande de base de données SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="e335d-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a><span data-ttu-id="e335d-106">Configurer le masquage dynamique des données pour votre base de données à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e335d-106">Set up dynamic data masking for your database using hello Azure Portal</span></span>
1. <span data-ttu-id="e335d-107">Lancement hello portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e335d-107">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e335d-108">Accédez à panneau des paramètres de base de données hello qui inclut des données sensibles hello souhaité toomask toohello.</span><span class="sxs-lookup"><span data-stu-id="e335d-108">Navigate toohello settings blade of hello database that includes hello sensitive data you want toomask.</span></span>
3. <span data-ttu-id="e335d-109">Cliquez sur hello **masquage dynamique des données** vignette qui lance hello **masquage dynamique des données** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="e335d-109">Click hello **Dynamic Data Masking** tile which launches hello **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="e335d-110">Ou bien, vous pouvez faire défiler toohello **Operations** et cliquez sur **masquage dynamique des données**.</span><span class="sxs-lookup"><span data-stu-id="e335d-110">Alternatively, you can scroll down toohello **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="e335d-112">Bonjour **masquage dynamique des données** Panneau de configuration que vous pouvez voir certaines colonnes de la base de données, ce moteur de recommandations hello a signalé de masquage.</span><span class="sxs-lookup"><span data-stu-id="e335d-112">In hello **Dynamic Data Masking** configuration blade you may see some database columns that hello recommendations engine has flagged for masking.</span></span> <span data-ttu-id="e335d-113">Dans commande tooaccept recommandations de hello, cliquez simplement sur **ajouter un masque** pour une ou plusieurs colonnes et un masque seront créés selon le type de valeur par défaut hello pour cette colonne.</span><span class="sxs-lookup"><span data-stu-id="e335d-113">In order tooaccept hello recommendations, just click **Add Mask** for one or more columns and a mask will be created based on hello default type for this column.</span></span> <span data-ttu-id="e335d-114">Vous pouvez modifier la fonction de masquage en cliquant sur la règle de masquage hello et en modifiant les hello champ format tooa autre format de votre choix de masquage de hello.</span><span class="sxs-lookup"><span data-stu-id="e335d-114">You can change hello masking function by clicking on hello masking rule and editing hello masking field format tooa different format of your choice.</span></span> <span data-ttu-id="e335d-115">Être vraiment tooclick **enregistrer** toosave vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="e335d-115">Be sure tooclick **Save** toosave your settings.</span></span>
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="e335d-117">tooadd un masque pour n’importe quelle colonne dans votre base de données, en haut de hello Hello **masquage dynamique des données** cliquez sur Panneau de configuration **ajouter un masque** tooopen hello **ajouter une règle de masquage** Panneau de configuration</span><span class="sxs-lookup"><span data-stu-id="e335d-117">tooadd a mask for any column in your database, at hello top of hello **Dynamic Data Masking** configuration blade click **Add Mask** tooopen hello **Add Masking Rule** configuration blade</span></span>
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="e335d-119">Sélectionnez hello **schéma**, **Table** et **colonne** hello toodefine désigné du champ qui sera masqué.</span><span class="sxs-lookup"><span data-stu-id="e335d-119">Select hello **Schema**, **Table** and **Column** toodefine hello designated field that will be masked.</span></span>
7. <span data-ttu-id="e335d-120">Choisissez un **de masquage de Format de champ** à partir de la liste de hello des catégories de masquage des données sensibles.</span><span class="sxs-lookup"><span data-stu-id="e335d-120">Choose a **Masking Field Format** from hello list of sensitive data masking categories.</span></span>
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="e335d-122">Cliquez sur **enregistrer** dans les données de salutation règle panneau tooupdate hello ensemble de règles dans hello masquage dynamique des données stratégie de masquage de masques.</span><span class="sxs-lookup"><span data-stu-id="e335d-122">Click **Save** in hello data masking rule blade tooupdate hello set of masking rules in hello dynamic data masking policy.</span></span>
9. <span data-ttu-id="e335d-123">Les utilisateurs SQL de type hello ou identités AAD qui doivent être exclues du masquage et ont accès aux données sensibles de toohello non masquée.</span><span class="sxs-lookup"><span data-stu-id="e335d-123">Type hello SQL users or AAD identities that should be excluded from masking, and have access toohello unmasked sensitive data.</span></span> <span data-ttu-id="e335d-124">La liste d'utilisateurs doit être délimitée par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="e335d-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="e335d-125">Notez que les utilisateurs disposant des privilèges d’administrateur ont toujours toohello accéder aux données non masquées d’origine.</span><span class="sxs-lookup"><span data-stu-id="e335d-125">Note that users with administrator privileges always have access toohello original unmasked data.</span></span>
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="e335d-127">toomake il hello par conséquent, la couche d’application peut afficher des données sensibles pour les utilisateurs de l’application privilégiée, hello utilisateur SQL ou l’application de hello identité AAD utilise la base de données tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="e335d-127">toomake it so hello application layer can display sensitive data for application privileged users, add hello SQL user or AAD identity hello application uses tooquery hello database.</span></span> <span data-ttu-id="e335d-128">Il est vivement recommandé que cette liste contient un nombre minimal de l’exposition aux utilisateurs privilégiés toominimize des données sensibles hello.</span><span class="sxs-lookup"><span data-stu-id="e335d-128">It is highly recommended that this list contain a minimal number of privileged users toominimize exposure of hello sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="e335d-129">Cliquez sur **enregistrer** dans la stratégie de masquage de nouveau ou mis à jour de configuration panneau toosave hello de masquage des données hello.</span><span class="sxs-lookup"><span data-stu-id="e335d-129">Click **Save** in hello data masking configuration blade toosave hello new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e335d-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e335d-130">Next steps</span></span>

* <span data-ttu-id="e335d-131">Pour une vue d’ensemble du masquage des données dynamiques, consultez [Masquage des données dynamiques](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e335d-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="e335d-132">Vous pouvez également implémenter à l’aide du masquage dynamique des données [applets de commande de base de données SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="e335d-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>
