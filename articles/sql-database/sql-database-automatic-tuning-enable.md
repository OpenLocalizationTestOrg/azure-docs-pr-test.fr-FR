---
title: "aaaEnable automatique de paramétrage de base de données SQL Azure | Documents Microsoft"
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
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="68a30-103">Activer le réglage automatique</span><span class="sxs-lookup"><span data-stu-id="68a30-103">Enable automatic tuning</span></span>

<span data-ttu-id="68a30-104">Base de données SQL Azure est un service de données managées automatiquement constamment surveille vos requêtes et identifie l’action hello que vous puissiez effectuer tooimprove les performances de votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="68a30-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies hello action that you can perform tooimprove performance of your workload.</span></span> <span data-ttu-id="68a30-105">Vous pouvez consulter les recommandations et les appliquer manuellement ou laisser Azure SQL Database appliquer automatiquement des actions correctives : il s’agit du **mode de réglage automatique**.</span><span class="sxs-lookup"><span data-stu-id="68a30-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="68a30-106">Le paramétrage automatique peut être activé au niveau de base de données de hello ou de serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="68a30-106">Automatic tuning can be enabled at hello server or hello database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="68a30-107">Activer le réglage automatique sur le serveur</span><span class="sxs-lookup"><span data-stu-id="68a30-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="68a30-108">tooenable automatique de paramétrage sur le serveur de base de données SQL Azure, accédez à serveur toohello dans Azure portail, puis sélectionnez **le paramétrage automatique** dans le menu de hello.</span><span class="sxs-lookup"><span data-stu-id="68a30-108">tooenable automatic tuning on Azure SQL Database server, navigate toohello server in Azure portal and then select **Automatic tuning** in hello menu.</span></span> <span data-ttu-id="68a30-109">Sélectionnez hello des options de paramétrage automatique souhaitée tooenable **appliquer**:</span><span class="sxs-lookup"><span data-stu-id="68a30-109">Select hello automatic tuning options you want tooenable and select **Apply**:</span></span>

![Serveur](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="68a30-111">Options de serveur de réglage automatiques sont tooall appliqué des bases de données sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="68a30-111">Automatic tuning options on server are applied tooall databases on hello server.</span></span> <span data-ttu-id="68a30-112">Par défaut, toutes les bases de données héritent la configuration de hello depuis le serveur de leur parent, mais cela peut être substituée et être spécifiée individuellement pour chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="68a30-112">By default, all databases inherit hello configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="68a30-113">Configurer le réglage automatique sur la base de données</span><span class="sxs-lookup"><span data-stu-id="68a30-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="68a30-114">Bonjour Azure permet de portail tooindividually vous spécifiez la configuration de réglage automatique hello sur chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="68a30-114">hello Azure portal enables you tooindividually specify hello automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="68a30-115">recommandation générale de Hello est toomanage hello paramétrage configuration automatique au niveau serveur hello dans ce même paramètres de configuration peuvent être appliquées automatiquement sur chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="68a30-115">hello general recommendation is toomanage hello automatic tuning configuration at server level so hello same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="68a30-116">Configurez le paramétrage automatique sur une base de données si la base de données hello est autre que d’autres membres de hello même serveur.</span><span class="sxs-lookup"><span data-stu-id="68a30-116">Configure automatic tuning on an individual database if hello database is different that others on hello same server.</span></span>
>

<span data-ttu-id="68a30-117">tooenable automatique de paramétrage sur une base de données, accédez à base de données toohello Bonjour portail Azure et puis sélectionnez **le paramétrage automatique**.</span><span class="sxs-lookup"><span data-stu-id="68a30-117">tooenable automatic tuning on a single database, navigate toohello database in hello Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="68a30-118">Vous pouvez configurer une seule base de données tooinherit hello les paramètres de base de données hello en sélectionnant la case à cocher hello ou vous pouvez spécifier individuellement configuration hello pour une base de données.</span><span class="sxs-lookup"><span data-stu-id="68a30-118">You can configure a single database tooinherit hello settings from hello database by selecting hello checkbox or you can specify hello configuration for a database individually.</span></span>

![Base de données](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="68a30-120">Une fois que vous avez sélectionné la configuration appropriée, cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="68a30-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68a30-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68a30-121">Next steps</span></span>
* <span data-ttu-id="68a30-122">Hello de lecture [article Paramétrage automatique](sql-database-automatic-tuning.md) toolearn plus d’informations sur le paramétrage automatique et comment il peut vous aider à améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="68a30-122">Read hello [Automatic tuning article](sql-database-automatic-tuning.md) toolearn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="68a30-123">Consultez [Recommandations en matière de performances](sql-database-advisor.md) pour obtenir une vue d’ensemble des recommandations relatives aux performances Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="68a30-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="68a30-124">Consultez [analyse des performances des requêtes](sql-database-query-performance.md) toolearn sur l’affichage des performances hello de vos requêtes principales.</span><span class="sxs-lookup"><span data-stu-id="68a30-124">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>
