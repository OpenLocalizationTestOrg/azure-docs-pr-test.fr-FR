---
title: aaaHow toocreate un ticket de support pour SQL Data Warehouse | Documents Microsoft
description: Comment toocreate une prise en charge de ticket dans Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="912a5-103">Comment toocreate une prise en charge de ticket pour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="912a5-103">How toocreate a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="912a5-104">Si vous rencontrez des problèmes avec SQL Data Warehouse, créez un ticket de support pour que notre équipe d’ingénierie puisse vous aider.</span><span class="sxs-lookup"><span data-stu-id="912a5-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="912a5-105">À compter de 20/12/2016, intégrité de ressource hello Bonjour portail Azure n’est pas précise.</span><span class="sxs-lookup"><span data-stu-id="912a5-105">As of 12/20/2016, hello resource health check in hello Azure portal is not accurate.</span></span> <span data-ttu-id="912a5-106">Nous essayons de toofix ce problème.</span><span class="sxs-lookup"><span data-stu-id="912a5-106">We are actively working toofix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="912a5-107">Création d’un ticket de support</span><span class="sxs-lookup"><span data-stu-id="912a5-107">Create a support ticket</span></span>
1. <span data-ttu-id="912a5-108">Ouvrez hello [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="912a5-108">Open hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="912a5-109">Sur l’écran d’accueil hello, cliquez sur hello **aide + support** vignette.</span><span class="sxs-lookup"><span data-stu-id="912a5-109">On hello Home screen, click hello **Help + support** tile.</span></span>
   
    ![Aide + Support](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="912a5-111">Hello aide + Support panneau, cliquez sur **demande de prise en charge de création**.</span><span class="sxs-lookup"><span data-stu-id="912a5-111">On hello Help + Support blade, click **Create support request**.</span></span>
   
    ![Nouvelle demande de support](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="912a5-113">Sélectionnez hello **le Type de demande**.</span><span class="sxs-lookup"><span data-stu-id="912a5-113">Select hello **Request Type**.</span></span>
   
    ![Type de demande](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="912a5-115">Par défaut, le **Quota de DTU** de chaque serveur SQL (par exemple, myserver.database.windows.net) est de 45 000.</span><span class="sxs-lookup"><span data-stu-id="912a5-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="912a5-116">Ce quota constitue simplement une limite de sécurité.</span><span class="sxs-lookup"><span data-stu-id="912a5-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="912a5-117">Vous pouvez augmenter votre quota en créant un ticket de support en sélectionnant *Quota* en tant que type de demande hello.</span><span class="sxs-lookup"><span data-stu-id="912a5-117">You can increase your quota by creating a support ticket and selecting *Quota* as hello request type.</span></span> <span data-ttu-id="912a5-118">toocalculate votre DTU a besoin, multipliez hello 7.5 par hello total [DWU] [ DWU] si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="912a5-118">toocalculate your DTU needs, multiply hello 7.5 by hello total [DWU][DWU] needed.</span></span> <span data-ttu-id="912a5-119">Par exemple, vous aimeriez toohost deux DW6000s sur un serveur SQL server, puis vous devez demander un quota UDBD 90 000.</span><span class="sxs-lookup"><span data-stu-id="912a5-119">For example, you would like toohost two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="912a5-120">Vous pouvez afficher votre consommation DTU actuelle à partir du panneau hello SQL server dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="912a5-120">You can view your current DTU consumption from hello SQL server blade in hello portal.</span></span> <span data-ttu-id="912a5-121">Interruption et reprises des bases de données s’inscrivent du quota UDBD hello.</span><span class="sxs-lookup"><span data-stu-id="912a5-121">Both paused and un-paused databases count toward hello DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="912a5-122">Sélectionnez hello **abonnement** que les ordinateurs hôtes hello de base de données avec le problème hello vous signalez.</span><span class="sxs-lookup"><span data-stu-id="912a5-122">Select hello **Subscription** that hosts hello database with hello problem you are reporting.</span></span>
   
    ![Abonnement](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="912a5-124">Sélectionnez **SQL Data Warehouse** comme hello des ressources.</span><span class="sxs-lookup"><span data-stu-id="912a5-124">Select **SQL Data Warehouse** as hello Resource.</span></span>
   
    ![Ressource](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="912a5-126">Sélectionnez votre [plan de support Azure][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="912a5-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="912a5-127">**gestion de la facturation, des abonnements et des quotas** sont pris en charge à tous les niveaux de support.</span><span class="sxs-lookup"><span data-stu-id="912a5-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="912a5-128">Les problèmes **couverts par la garantie de réparation et d’assistance** sont pris en charge dans les plans de support suivants : [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] ou [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="912a5-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="912a5-129">Problèmes de réparation sont les problèmes rencontrés par les clients lors de l’utilisation d’Azure dans lequel il existe une attente raisonnable ce problème de hello Microsoft dû.</span><span class="sxs-lookup"><span data-stu-id="912a5-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused hello problem.</span></span>
   * <span data-ttu-id="912a5-130">**Développeur encadrement** et **les services de conseil** sont disponibles à hello [Direct Professionnel] [ Professional Direct] et [Premier] [ Premier] les niveaux de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="912a5-130">**Developer mentoring** and **advisory services** are available at hello [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="912a5-131">Si vous avez un Premier plan de prise en charge, vous pouvez également signaler SQL Data Warehouse problèmes sur hello [portail en ligne de Microsoft Premier][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="912a5-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on hello [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="912a5-132">Consultez [les plans de support Azure] [ Azure support plan] toolearn plus hello prend en charge les différents plans, notamment la portée, le temps de réponse, la tarification, etc..  Pour accéder aux questions fréquemment posées sur le support Azure, consultez la page [FAQ du support Azure][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="912a5-132">See [Azure support plans][Azure support plan] toolearn more about hello various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![Plan de support](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="912a5-134">Sélectionnez hello **Type de problème** et **catégorie**.</span><span class="sxs-lookup"><span data-stu-id="912a5-134">Select hello **Problem Type** and **Category**.</span></span> <span data-ttu-id="912a5-135">Dans cet exemple, nous avons choisi « Outils » en tant que type de problème de hello et « Outils de Client » comme catégorie de hello.</span><span class="sxs-lookup"><span data-stu-id="912a5-135">In this example, we have chosen "Tools" as hello Problem type and "Client tools" as hello category.</span></span> 
   
    ![Catégorie de type de problème](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="912a5-137">Décrire le problème de hello et choisissez niveau hello d’impact sur l’activité.</span><span class="sxs-lookup"><span data-stu-id="912a5-137">Describe hello problem and choose hello level of business impact.</span></span>
   
    ![Description du problème](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="912a5-139">Vos **informations de contact** pour ce ticket de support seront pré-remplies.</span><span class="sxs-lookup"><span data-stu-id="912a5-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="912a5-140">Mettez-les à jour si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="912a5-140">Update this if necessary.</span></span>
    
    ![Informations de contact](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="912a5-142">Cliquez sur **créer** toosubmit hello prise en charge de demande.</span><span class="sxs-lookup"><span data-stu-id="912a5-142">Click **Create** toosubmit hello support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="912a5-143">Surveiller un ticket de support</span><span class="sxs-lookup"><span data-stu-id="912a5-143">Monitor a support ticket</span></span>
<span data-ttu-id="912a5-144">Une fois que vous avez envoyé la demande de support hello, équipe de support Azure hello vous contacter.</span><span class="sxs-lookup"><span data-stu-id="912a5-144">After you have submitted hello support request, hello Azure support team will contact you.</span></span> <span data-ttu-id="912a5-145">toocheck votre état de la demande et les détails, cliquez sur **gérer les demandes de support** sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="912a5-145">toocheck your request status and details, click **Manage support requests** on hello dashboard.</span></span>

![Vérification du statut](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="912a5-147">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="912a5-147">Other Resources</span></span>
<span data-ttu-id="912a5-148">En outre, vous pouvez vous connecter avec hello Communauté de SQL Data Warehouse sur [Stack Overflow] [ Stack Overflow] ou sur hello [forum MSDN de l’entrepôt de données de SQL Azure] [ Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="912a5-148">Additionally, you can connect with hello SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on hello [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

