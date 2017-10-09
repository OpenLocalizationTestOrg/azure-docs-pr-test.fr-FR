---
title: "aaaManage bases de données SQL Azure à l’aide d’Azure Automation | Documents Microsoft"
description: "Découvrez comment hello service Azure Automation peut être utilisés toomanage bases de données SQL Azure à l’échelle."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="b4a01-103">Gestion des bases de données SQL Azure à l'aide d'Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b4a01-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="b4a01-104">Ce guide vous oblige à service d’Azure Automation toohello et comment il peut être gestion toosimplify utilisés de vos bases de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b4a01-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b4a01-105">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="b4a01-105">What is Azure Automation?</span></span>
<span data-ttu-id="b4a01-106">[Azure Automation](https://azure.microsoft.com/services/automation/) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="b4a01-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="b4a01-107">Les tâches longues, manuelles, sujette aux erreurs et répétitives à l’aide d’Azure Automation, peuvent être automatisée tooincrease fiabilité, l’efficacité et toovalue de temps pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b4a01-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="b4a01-108">Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet vos besoins que votre organisation se développe.</span><span class="sxs-lookup"><span data-stu-id="b4a01-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="b4a01-109">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="b4a01-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b4a01-110">Réduire la surcharge opérationnelle et de libérer de l’informatique / toofocus du personnel DevOps sur le travail qui ajoute la valeur de l’entreprise en déplaçant votre toobe de tâches de gestion de cloud exécutés automatiquement par Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="b4a01-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="b4a01-111">Comment Azure Automation peut-il aider à gérer des bases de données SQL Azure ?</span><span class="sxs-lookup"><span data-stu-id="b4a01-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="b4a01-112">Base de données SQL Azure peuvent être géré dans Azure Automation à l’aide de hello [applets de commande PowerShell de base de données SQL Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) qui sont disponibles dans hello [outils Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4a01-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="b4a01-113">Azure Automation dispose de ces applets de commande PowerShell de base de données SQL Azure disponibles en dehors de la zone de hello, afin que vous pouvez effectuer toutes vos tâches de gestion de base de données SQL dans le service de hello.</span><span class="sxs-lookup"><span data-stu-id="b4a01-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="b4a01-114">Vous pouvez également de paires de ces applets de commande dans Azure Automation avec les applets de commande hello pour les autres services Azure, les tooautomate des tâches complexes entre des services Azure et les systèmes tiers 3e.</span><span class="sxs-lookup"><span data-stu-id="b4a01-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="b4a01-115">Azure Automation dispose également toocommunicate de capacité hello avec les serveurs SQL directement, en émettant des commandes SQL à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b4a01-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="b4a01-116">Hello [galerie de runbooks Azure Automation](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contient une série de produit Communauté et l’équipe runbooks tooget démarré l’automatisation de la gestion de bases de données SQL Azure, les autres services Azure et 3e systèmes tiers.</span><span class="sxs-lookup"><span data-stu-id="b4a01-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="b4a01-117">La galerie de Runbooks inclut :</span><span class="sxs-lookup"><span data-stu-id="b4a01-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="b4a01-118">Exécuter des requêtes SQL avec une base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="b4a01-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="b4a01-119">Mise à l’échelle verticale (haut ou bas) d’une base de données SQL Azure selon un programme planifié</span><span class="sxs-lookup"><span data-stu-id="b4a01-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="b4a01-120">Tronquer une table SQL si la base de données est proche de la taille maximale</span><span class="sxs-lookup"><span data-stu-id="b4a01-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="b4a01-121">Indexer les tables dans une base de données SQL Azure si elles sont très fragmentées</span><span class="sxs-lookup"><span data-stu-id="b4a01-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="b4a01-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b4a01-122">Next steps</span></span>
<span data-ttu-id="b4a01-123">Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être des bases de données SQL Azure toomanage utilisé, suivez ces liens de toolearn plus sur Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="b4a01-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="b4a01-124">Vue d’ensemble de Microsoft Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b4a01-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="b4a01-125">Mon premier Runbook</span><span class="sxs-lookup"><span data-stu-id="b4a01-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="b4a01-126">Plan d’apprentissage pour Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b4a01-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="b4a01-127">Azure Automation : Votre Agent SQL Bonjour Cloud</span><span class="sxs-lookup"><span data-stu-id="b4a01-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

