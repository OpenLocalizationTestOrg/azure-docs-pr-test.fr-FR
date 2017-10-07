---
title: "requêtes d’utilisateur aaaMonitor dans Azure SQL Data Warehouse | Documents Microsoft"
description: "Vue d’ensemble des considérations de hello, les meilleures pratiques et les tâches de surveillance des requêtes utilisateur dans Azure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 1d0960db-5dcf-4a08-b1dc-6c5d3d5a616d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 67639e81b04635452e1ed844fe2d7245aa96a4fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="a5b4b-103">Surveillance des requêtes d’utilisateur dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a5b4b-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a5b4b-104">Vue d’ensemble des considérations de hello, les meilleures pratiques et les tâches de surveillance des requêtes de l’utilisateur dans l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="a5b4b-104">Overview of hello considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="a5b4b-105">Catégorie</span><span class="sxs-lookup"><span data-stu-id="a5b4b-105">Category</span></span> | <span data-ttu-id="a5b4b-106">Tâche ou considération</span><span class="sxs-lookup"><span data-stu-id="a5b4b-106">Task or consideration</span></span> | <span data-ttu-id="a5b4b-107">Description</span><span class="sxs-lookup"><span data-stu-id="a5b4b-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a5b4b-108">Performances lentes</span><span class="sxs-lookup"><span data-stu-id="a5b4b-108">Slow performance</span></span> |<span data-ttu-id="a5b4b-109">Rechercher une longue requête d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a5b4b-109">Find a long-running user query</span></span> |<span data-ttu-id="a5b4b-110">[Rechercher les requêtes à exécution longue][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="a5b4b-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="a5b4b-111">Accès concurrentiel</span><span class="sxs-lookup"><span data-stu-id="a5b4b-111">Concurrency</span></span> |<span data-ttu-id="a5b4b-112">Affecter des ressources simultanées toouser requêtes</span><span class="sxs-lookup"><span data-stu-id="a5b4b-112">Assign concurrent resources toouser queries</span></span> |<span data-ttu-id="a5b4b-113">[Gestion de la concurrence et des charges de travail][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="a5b4b-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a5b4b-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a5b4b-114">Next steps</span></span>
<span data-ttu-id="a5b4b-115">Pour plus d’informations de gestion, rendez-vous sur toohello [vue d’ensemble de la gestion][Management overview].</span><span class="sxs-lookup"><span data-stu-id="a5b4b-115">For more management tips, head over toohello [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
