---
title: "Activer le réglage automatique pour Azure SQL Database | Microsoft Docs"
description: "Vous pouvez facilement activer le réglage automatique sur Azure SQL Database."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: b391b1f7aa37c5a06fc320ce892534187deb4959
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="49ef5-103">Activer le réglage automatique</span><span class="sxs-lookup"><span data-stu-id="49ef5-103">Enable automatic tuning</span></span>

<span data-ttu-id="49ef5-104">Azure SQL Database est un service de données géré automatiquement qui surveille vos requêtes en permanence et identifie les actions que vous pouvez effectuer pour améliorer les performances de votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="49ef5-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies the action that you can perform to improve performance of your workload.</span></span> <span data-ttu-id="49ef5-105">Vous pouvez consulter les recommandations et les appliquer manuellement ou laisser Azure SQL Database appliquer automatiquement des actions correctives : il s’agit du **mode de réglage automatique**.</span><span class="sxs-lookup"><span data-stu-id="49ef5-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="49ef5-106">Le réglage automatique peut être activé au niveau du serveur ou de la base de données.</span><span class="sxs-lookup"><span data-stu-id="49ef5-106">Automatic tuning can be enabled at the server or the database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="49ef5-107">Activer le réglage automatique sur le serveur</span><span class="sxs-lookup"><span data-stu-id="49ef5-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="49ef5-108">Pour activer le réglage automatique sur le serveur Azure SQL Database, accédez au serveur dans le portail Azure, puis sélectionnez **Réglage automatique** dans le menu.</span><span class="sxs-lookup"><span data-stu-id="49ef5-108">To enable automatic tuning on Azure SQL Database server, navigate to the server in Azure portal and then select **Automatic tuning** in the menu.</span></span> <span data-ttu-id="49ef5-109">Sélectionnez les options de réglage automatique que vous souhaitez activer et sélectionnez **Appliquer** :</span><span class="sxs-lookup"><span data-stu-id="49ef5-109">Select the automatic tuning options you want to enable and select **Apply**:</span></span>

![Serveur](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="49ef5-111">Les options de réglage automatique sur le serveur sont appliquées à toutes les bases de données du serveur.</span><span class="sxs-lookup"><span data-stu-id="49ef5-111">Automatic tuning options on server are applied to all databases on the server.</span></span> <span data-ttu-id="49ef5-112">Par défaut, toutes les bases de données héritent de la configuration de leur serveur parent, mais celle-ci peut être remplacée et spécifiée individuellement pour chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="49ef5-112">By default, all databases inherit the configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="49ef5-113">Configurer le réglage automatique sur la base de données</span><span class="sxs-lookup"><span data-stu-id="49ef5-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="49ef5-114">Le portail Azure vous permet de spécifier individuellement la configuration de réglage automatique de chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="49ef5-114">The Azure portal enables you to individually specify the automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="49ef5-115">Il est généralement recommandé de gérer la configuration du réglage automatique au niveau du serveur, afin que les mêmes paramètres de configuration soient appliqués automatiquement à chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="49ef5-115">The general recommendation is to manage the automatic tuning configuration at server level so the same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="49ef5-116">Configurez le réglage automatique au niveau d’une base de données si celle-ci est différente des autres sur le même serveur.</span><span class="sxs-lookup"><span data-stu-id="49ef5-116">Configure automatic tuning on an individual database if the database is different that others on the same server.</span></span>
>

<span data-ttu-id="49ef5-117">Pour activer le réglage automatique sur une seule base de données, accédez à la base de données dans le portail Azure, puis sélectionnez **Réglage automatique**.</span><span class="sxs-lookup"><span data-stu-id="49ef5-117">To enable automatic tuning on a single database, navigate to the database in the Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="49ef5-118">Vous pouvez configurer une seule base de données de façon à ce qu’elle hérite des paramètres de la base de données en cochant la case, ou vous pouvez spécifier individuellement la configuration d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="49ef5-118">You can configure a single database to inherit the settings from the database by selecting the checkbox or you can specify the configuration for a database individually.</span></span>

![Base de données](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="49ef5-120">Une fois que vous avez sélectionné la configuration appropriée, cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="49ef5-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49ef5-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="49ef5-121">Next steps</span></span>
* <span data-ttu-id="49ef5-122">Lisez l’[article Réglage automatique](sql-database-automatic-tuning.md) pour en savoir plus sur le réglage automatique et sur la manière dont il peut vous aider à améliorer vos performances.</span><span class="sxs-lookup"><span data-stu-id="49ef5-122">Read the [Automatic tuning article](sql-database-automatic-tuning.md) to learn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="49ef5-123">Consultez [Recommandations en matière de performances](sql-database-advisor.md) pour obtenir une vue d’ensemble des recommandations relatives aux performances Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="49ef5-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="49ef5-124">Pour connaître l’impact de vos principales requêtes sur les performances, consultez [Query Performance Insights](sql-database-query-performance.md).</span><span class="sxs-lookup"><span data-stu-id="49ef5-124">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>
