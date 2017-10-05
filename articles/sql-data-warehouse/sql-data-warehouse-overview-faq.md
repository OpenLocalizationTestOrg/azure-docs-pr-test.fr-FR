---
title: Foire aux questions Azure SQL Data Warehouse | Microsoft Docs
description: "Cet article répertorie les questions fréquemment posées par les clients et les développeurs sur Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 4c00710ecc0c91f8407eca81b78176075fcbd6ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="4225e-103">Foire aux questions SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4225e-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="4225e-104">Généralités</span><span class="sxs-lookup"><span data-stu-id="4225e-104">General</span></span>

<span data-ttu-id="4225e-105">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-105">Q.</span></span> <span data-ttu-id="4225e-106">Quelles sont les solutions offertes par SQL DW en matière de sécurité des données ?</span><span class="sxs-lookup"><span data-stu-id="4225e-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="4225e-107">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-107">A.</span></span> <span data-ttu-id="4225e-108">SQL DW propose plusieurs solutions de protection des données, comme le chiffrement TDE et les audits.</span><span class="sxs-lookup"><span data-stu-id="4225e-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="4225e-109">Pour plus d’informations, consultez [Sécurité].</span><span class="sxs-lookup"><span data-stu-id="4225e-109">For more information, see [Security].</span></span>

<span data-ttu-id="4225e-110">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-110">Q.</span></span> <span data-ttu-id="4225e-111">Où puis-je trouver les normes juridiques et commerciales auxquelles SQL DW est conforme ?</span><span class="sxs-lookup"><span data-stu-id="4225e-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="4225e-112">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-112">A.</span></span> <span data-ttu-id="4225e-113">Consultez la page [Conformité Microsoft] pour connaître les différentes offres de conformité par produit, notamment SOC et ISO.</span><span class="sxs-lookup"><span data-stu-id="4225e-113">Visit the [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="4225e-114">Tout d’abord, sélectionnez le titre de conformité de votre choix, puis développez Azure dans la section des services cloud qui figurent dans le champ d’application de Microsoft, sur le côté droit de la page, pour voir quels sont les services Azure conformes.</span><span class="sxs-lookup"><span data-stu-id="4225e-114">First choose by Compliance title, then expand Azure in the Microsoft in-scope cloud services section on the right side of the page to see what services are Azure services are compliant.</span></span>

<span data-ttu-id="4225e-115">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-115">Q.</span></span> <span data-ttu-id="4225e-116">Puis-je connecter Power BI ?</span><span class="sxs-lookup"><span data-stu-id="4225e-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="4225e-117">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-117">A.</span></span> <span data-ttu-id="4225e-118">Oui.</span><span class="sxs-lookup"><span data-stu-id="4225e-118">Yes!</span></span> <span data-ttu-id="4225e-119">Bien que Power BI prenne en charge les requêtes directes avec SQL DW, il n’est pas destiné à traiter un grand nombre d’utilisateurs ou de données en temps réel.</span><span class="sxs-lookup"><span data-stu-id="4225e-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="4225e-120">Pour une utilisation en production de Power BI, nous recommandons d’utiliser Power BI en complément d’Azure Analysis Services ou d’Analysis Service IaaS.</span><span class="sxs-lookup"><span data-stu-id="4225e-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="4225e-121">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-121">Q.</span></span> <span data-ttu-id="4225e-122">Quelles sont les limites de capacité de SQL Data Warehouse ?</span><span class="sxs-lookup"><span data-stu-id="4225e-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="4225e-123">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-123">A.</span></span> <span data-ttu-id="4225e-124">Consultez notre page [Limites de capacité] actuelle.</span><span class="sxs-lookup"><span data-stu-id="4225e-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="4225e-125">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-125">Q.</span></span> <span data-ttu-id="4225e-126">Pourquoi ma Mise à l’échelle/Pause/Reprise est-elle si longue ?</span><span class="sxs-lookup"><span data-stu-id="4225e-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="4225e-127">R :</span><span class="sxs-lookup"><span data-stu-id="4225e-127">A.</span></span> <span data-ttu-id="4225e-128">Un certain nombre de facteurs peuvent influencer la durée des opérations de gestion du calcul.</span><span class="sxs-lookup"><span data-stu-id="4225e-128">A variety of factors can influence the time for compute management operations.</span></span> <span data-ttu-id="4225e-129">Une cause fréquente des opérations avec une durée d’exécution longue est l’annulation de transactions.</span><span class="sxs-lookup"><span data-stu-id="4225e-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="4225e-130">Quand une opération de mise à l’échelle ou de pause est lancée, toutes les sessions entrantes sont bloquées et les requêtes sont vidées.</span><span class="sxs-lookup"><span data-stu-id="4225e-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="4225e-131">Afin de laisser le système dans un état stable, les transactions doivent être annulées avant qu’une opération puisse commencer.</span><span class="sxs-lookup"><span data-stu-id="4225e-131">In order to leave the system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="4225e-132">Plus le nombre et la taille du journal des transactions sont importants, plus longtemps l’opération sera bloquée en attente de la restauration du système à un état stable.</span><span class="sxs-lookup"><span data-stu-id="4225e-132">The greater the number and larger the log size of transactions, the longer the operation will be stalled restoring the system to a stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="4225e-133">Service client</span><span class="sxs-lookup"><span data-stu-id="4225e-133">User support</span></span>

<span data-ttu-id="4225e-134">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-134">Q.</span></span> <span data-ttu-id="4225e-135">J’ai une suggestion de fonctionnalité, où dois-je l’envoyer ?</span><span class="sxs-lookup"><span data-stu-id="4225e-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="4225e-136">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-136">A.</span></span> <span data-ttu-id="4225e-137">Si vous souhaitez faire une demande de fonctionnalité, envoyez-la sur notre page [UserVoice].</span><span class="sxs-lookup"><span data-stu-id="4225e-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="4225e-138">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-138">Q.</span></span> <span data-ttu-id="4225e-139">Comment faire x ?</span><span class="sxs-lookup"><span data-stu-id="4225e-139">How can I do x?</span></span>

<span data-ttu-id="4225e-140">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-140">A.</span></span> <span data-ttu-id="4225e-141">Pour obtenir de l’aide concernant le développement avec SQL Data Warehouse, vous pouvez poser des questions sur notre page [Stack Overflow].</span><span class="sxs-lookup"><span data-stu-id="4225e-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="4225e-142">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-142">Q.</span></span> <span data-ttu-id="4225e-143">Comment envoyer un ticket de support ?</span><span class="sxs-lookup"><span data-stu-id="4225e-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="4225e-144">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-144">A.</span></span> <span data-ttu-id="4225e-145">Les [tickets de support] peuvent être déposés sur le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4225e-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="4225e-146">Prise en charge de fonctionnalités / langages SQL</span><span class="sxs-lookup"><span data-stu-id="4225e-146">SQL language/feature support</span></span> 

<span data-ttu-id="4225e-147">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-147">Q.</span></span> <span data-ttu-id="4225e-148">Quels sont les types de données pris en charge par SQL Data Warehouse ?</span><span class="sxs-lookup"><span data-stu-id="4225e-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="4225e-149">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-149">A.</span></span> <span data-ttu-id="4225e-150">Consultez la page [Types de données] SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4225e-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="4225e-151">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-151">Q.</span></span> <span data-ttu-id="4225e-152">Quelles fonctionnalités de table prenez-vous en charge ?</span><span class="sxs-lookup"><span data-stu-id="4225e-152">What table features do you support?</span></span>

<span data-ttu-id="4225e-153">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-153">A.</span></span> <span data-ttu-id="4225e-154">SQL Data Warehouse prend en charge de nombreuses fonctionnalités, mais pas toutes ; celles qui ne sont pas prises en charge sont documentées dans [Fonctionnalités de table non prises en charge].</span><span class="sxs-lookup"><span data-stu-id="4225e-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="4225e-155">Outils et administration</span><span class="sxs-lookup"><span data-stu-id="4225e-155">Tooling and administration</span></span>

<span data-ttu-id="4225e-156">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-156">Q.</span></span> <span data-ttu-id="4225e-157">Prenez-vous en charge les projets de base de données dans Visual Studio ?</span><span class="sxs-lookup"><span data-stu-id="4225e-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="4225e-158">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-158">A.</span></span> <span data-ttu-id="4225e-159">À l’heure actuelle, nous ne prenons pas en charge les projets de base de données dans Visual Studio pour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4225e-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="4225e-160">Si vous souhaitez voter pour obtenir cette fonctionnalité, visitez notre UserVoice [Demande de fonctionnalités pour les projets de base de données].</span><span class="sxs-lookup"><span data-stu-id="4225e-160">If you'd like to cast a vote to get this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="4225e-161">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-161">Q.</span></span> <span data-ttu-id="4225e-162">SQL Data Warehouse prend-il en charge les API REST ?</span><span class="sxs-lookup"><span data-stu-id="4225e-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="4225e-163">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-163">A.</span></span> <span data-ttu-id="4225e-164">Oui.</span><span class="sxs-lookup"><span data-stu-id="4225e-164">Yes.</span></span> <span data-ttu-id="4225e-165">La plupart des fonctionnalités REST utilisables avec SQL Database sont également disponibles avec SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4225e-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="4225e-166">Vous trouverez des informations sur les API sur les pages de documentation REST ou sur [MSDN].</span><span class="sxs-lookup"><span data-stu-id="4225e-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="4225e-167">Chargement</span><span class="sxs-lookup"><span data-stu-id="4225e-167">Loading</span></span>

<span data-ttu-id="4225e-168">Q :</span><span class="sxs-lookup"><span data-stu-id="4225e-168">Q.</span></span> <span data-ttu-id="4225e-169">Quels pilotes clients prenez-vous en charge ?</span><span class="sxs-lookup"><span data-stu-id="4225e-169">What client drivers do you support?</span></span>

<span data-ttu-id="4225e-170">R.</span><span class="sxs-lookup"><span data-stu-id="4225e-170">A.</span></span> <span data-ttu-id="4225e-171">La prise en charge des pilotes pour DW est détaillée sur la page [Chaînes de connexion].</span><span class="sxs-lookup"><span data-stu-id="4225e-171">Driver support for DW can be found on the [Connection Strings] page</span></span>

<span data-ttu-id="4225e-172">Q : Quels sont les formats de fichier pris en charge par PolyBase avec SQL Data Warehouse ?</span><span class="sxs-lookup"><span data-stu-id="4225e-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="4225e-173">R : Orc, RC, Parquet et le texte plat délimité</span><span class="sxs-lookup"><span data-stu-id="4225e-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="4225e-174">Q : À quoi puis-je me connecter à partir de SQL DW à l’aide de PolyBase ?</span><span class="sxs-lookup"><span data-stu-id="4225e-174">Q: What can I connect to from SQL DW using PolyBase?</span></span> 

<span data-ttu-id="4225e-175">R : [Azure Data Lake Store] et [Azure Storage Blobs].</span><span class="sxs-lookup"><span data-stu-id="4225e-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="4225e-176">Q : Les automates à pile sont-ils possibles lors de la connexion à Azure Storage Blobs ou à  ADLS ?</span><span class="sxs-lookup"><span data-stu-id="4225e-176">Q: Is computation pushdown possible  when connecting to Azure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="4225e-177">R : Non, SQL DW PolyBase interagit uniquement avec les composants de stockage.</span><span class="sxs-lookup"><span data-stu-id="4225e-177">A: No, SQL DW PolyBase only interacts the storage components.</span></span> 

<span data-ttu-id="4225e-178">Q : Puis-je me connecter à HDI ?</span><span class="sxs-lookup"><span data-stu-id="4225e-178">Q: Can I connect to HDI?</span></span>

<span data-ttu-id="4225e-179">R : HDI peut utiliser ADLS ou WASB comme couche HDFS.</span><span class="sxs-lookup"><span data-stu-id="4225e-179">A: HDI can use either ADLS or WASB as the HDFS layer.</span></span> <span data-ttu-id="4225e-180">Si vous avez l’un des deux comme couche HDFS, vous pouvez charger ces données dans SQL DW.</span><span class="sxs-lookup"><span data-stu-id="4225e-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="4225e-181">Toutefois, vous ne peut pas générer d’automate à pile vers l’instance HDI.</span><span class="sxs-lookup"><span data-stu-id="4225e-181">However, you cannot generate pushdown computation to the HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4225e-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4225e-182">Next steps</span></span>
<span data-ttu-id="4225e-183">Pour plus d’informations sur SQL Data Warehouse dans son ensemble, consultez notre page [Vue d’ensemble].</span><span class="sxs-lookup"><span data-stu-id="4225e-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
<span data-ttu-id="4225e-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="4225e-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span></span>
<span data-ttu-id="4225e-185">[Chaînes de connexion]: ./sql-data-warehouse-connection-strings.md</span><span class="sxs-lookup"><span data-stu-id="4225e-185">[Connection Strings]: ./sql-data-warehouse-connection-strings.md</span></span>
<span data-ttu-id="4225e-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span><span class="sxs-lookup"><span data-stu-id="4225e-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span></span>
<span data-ttu-id="4225e-187">[tickets de support]: ./sql-data-warehouse-get-started-create-support-ticket.md</span><span class="sxs-lookup"><span data-stu-id="4225e-187">[Support Tickets]: ./sql-data-warehouse-get-started-create-support-ticket.md</span></span>
<span data-ttu-id="4225e-188">[Sécurité]: ./sql-data-warehouse-overview-manage-security.md</span><span class="sxs-lookup"><span data-stu-id="4225e-188">[Security]: ./sql-data-warehouse-overview-manage-security.md</span></span>
<span data-ttu-id="4225e-189">[Conformité Microsoft]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span><span class="sxs-lookup"><span data-stu-id="4225e-189">[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span></span>
<span data-ttu-id="4225e-190">[Limites de capacité]: ./sql-data-warehouse-service-capacity-limits.md</span><span class="sxs-lookup"><span data-stu-id="4225e-190">[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md</span></span>
<span data-ttu-id="4225e-191">[Types de données]: ./sql-data-warehouse-tables-data-types.md</span><span class="sxs-lookup"><span data-stu-id="4225e-191">[data types]: ./sql-data-warehouse-tables-data-types.md</span></span>
<span data-ttu-id="4225e-192">[Fonctionnalités de table non prises en charge]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span><span class="sxs-lookup"><span data-stu-id="4225e-192">[Unsupported Table Features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span></span>
<span data-ttu-id="4225e-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span><span class="sxs-lookup"><span data-stu-id="4225e-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span></span>
<span data-ttu-id="4225e-194">[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span><span class="sxs-lookup"><span data-stu-id="4225e-194">[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span></span>
<span data-ttu-id="4225e-195">[Demande de fonctionnalités pour les projets de base de données]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span><span class="sxs-lookup"><span data-stu-id="4225e-195">[Database projects feature request]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span></span>
<span data-ttu-id="4225e-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span><span class="sxs-lookup"><span data-stu-id="4225e-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span></span>
<span data-ttu-id="4225e-197">[Vue d’ensemble]: ./sql-data-warehouse-overview-faq.md</span><span class="sxs-lookup"><span data-stu-id="4225e-197">[Overview]: ./sql-data-warehouse-overview-faq.md</span></span>