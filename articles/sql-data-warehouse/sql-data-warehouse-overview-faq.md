---
title: "aaaAzure SQL données entrepôt Forum aux Questions | Documents Microsoft"
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
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="c8ae1-103">Foire aux questions SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c8ae1-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="c8ae1-104">Généralités</span><span class="sxs-lookup"><span data-stu-id="c8ae1-104">General</span></span>

<span data-ttu-id="c8ae1-105">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-105">Q.</span></span> <span data-ttu-id="c8ae1-106">Quelles sont les solutions offertes par SQL DW en matière de sécurité des données ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="c8ae1-107">R.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-107">A.</span></span> <span data-ttu-id="c8ae1-108">SQL DW propose plusieurs solutions de protection des données, comme le chiffrement TDE et les audits.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="c8ae1-109">Pour plus d’informations, consultez [Sécurité].</span><span class="sxs-lookup"><span data-stu-id="c8ae1-109">For more information, see [Security].</span></span>

<span data-ttu-id="c8ae1-110">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-110">Q.</span></span> <span data-ttu-id="c8ae1-111">Où puis-je trouver les normes juridiques et commerciales auxquelles SQL DW est conforme ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="c8ae1-112">R :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-112">A.</span></span> <span data-ttu-id="c8ae1-113">Visitez hello [Microsoft Compliance] page pour différentes offres de conformité par produit par exemple, le SOC et ISO.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="c8ae1-114">Tout d’abord choisir par titre de la conformité, puis développez Azure hello dans l’étendue Microsoft nuage section services sur le côté droit de hello de hello page toosee quels services sont des services Azure est conformes.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="c8ae1-115">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-115">Q.</span></span> <span data-ttu-id="c8ae1-116">Puis-je connecter Power BI ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="c8ae1-117">R.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-117">A.</span></span> <span data-ttu-id="c8ae1-118">Oui.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-118">Yes!</span></span> <span data-ttu-id="c8ae1-119">Bien que Power BI prenne en charge les requêtes directes avec SQL DW, il n’est pas destiné à traiter un grand nombre d’utilisateurs ou de données en temps réel.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="c8ae1-120">Pour une utilisation en production de Power BI, nous recommandons d’utiliser Power BI en complément d’Azure Analysis Services ou d’Analysis Service IaaS.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="c8ae1-121">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-121">Q.</span></span> <span data-ttu-id="c8ae1-122">Quelles sont les limites de capacité de SQL Data Warehouse ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="c8ae1-123">R.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-123">A.</span></span> <span data-ttu-id="c8ae1-124">Consultez notre page [Limites de capacité] actuelle.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="c8ae1-125">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-125">Q.</span></span> <span data-ttu-id="c8ae1-126">Pourquoi ma Mise à l’échelle/Pause/Reprise est-elle si longue ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="c8ae1-127">R :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-127">A.</span></span> <span data-ttu-id="c8ae1-128">Un certain nombre de facteurs peut influencer la durée hello pour les opérations de gestion de calcul.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="c8ae1-129">Une cause fréquente des opérations avec une durée d’exécution longue est l’annulation de transactions.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="c8ae1-130">Quand une opération de mise à l’échelle ou de pause est lancée, toutes les sessions entrantes sont bloquées et les requêtes sont vidées.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="c8ae1-131">Dans le système de type hello tooleave de commande dans un état stable, les transactions doivent être restaurées avant une opération puisse commencer.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="c8ae1-132">Hello plus grand nombre de hello et la plus grande taille de journal hello des transactions, opération hello plue de hello est bloquée hello système tooa stable état de restauration.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="c8ae1-133">Service client</span><span class="sxs-lookup"><span data-stu-id="c8ae1-133">User support</span></span>

<span data-ttu-id="c8ae1-134">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-134">Q.</span></span> <span data-ttu-id="c8ae1-135">J’ai une suggestion de fonctionnalité, où dois-je l’envoyer ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="c8ae1-136">R.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-136">A.</span></span> <span data-ttu-id="c8ae1-137">Si vous souhaitez faire une demande de fonctionnalité, envoyez-la sur notre page [UserVoice].</span><span class="sxs-lookup"><span data-stu-id="c8ae1-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="c8ae1-138">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-138">Q.</span></span> <span data-ttu-id="c8ae1-139">Comment faire x ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-139">How can I do x?</span></span>

<span data-ttu-id="c8ae1-140">R.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-140">A.</span></span> <span data-ttu-id="c8ae1-141">Pour obtenir de l’aide concernant le développement avec SQL Data Warehouse, vous pouvez poser des questions sur notre page [Stack Overflow].</span><span class="sxs-lookup"><span data-stu-id="c8ae1-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="c8ae1-142">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-142">Q.</span></span> <span data-ttu-id="c8ae1-143">Comment envoyer un ticket de support ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="c8ae1-144">R.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-144">A.</span></span> <span data-ttu-id="c8ae1-145">Les [tickets de support] peuvent être déposés sur le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="c8ae1-146">Prise en charge de fonctionnalités / langages SQL</span><span class="sxs-lookup"><span data-stu-id="c8ae1-146">SQL language/feature support</span></span> 

<span data-ttu-id="c8ae1-147">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-147">Q.</span></span> <span data-ttu-id="c8ae1-148">Quels sont les types de données pris en charge par SQL Data Warehouse ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="c8ae1-149">R.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-149">A.</span></span> <span data-ttu-id="c8ae1-150">Consultez la page [Types de données] SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="c8ae1-151">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-151">Q.</span></span> <span data-ttu-id="c8ae1-152">Quelles fonctionnalités de table prenez-vous en charge ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-152">What table features do you support?</span></span>

<span data-ttu-id="c8ae1-153">R.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-153">A.</span></span> <span data-ttu-id="c8ae1-154">SQL Data Warehouse prend en charge de nombreuses fonctionnalités, mais pas toutes ; celles qui ne sont pas prises en charge sont documentées dans [Fonctionnalités de table non prises en charge].</span><span class="sxs-lookup"><span data-stu-id="c8ae1-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="c8ae1-155">Outils et administration</span><span class="sxs-lookup"><span data-stu-id="c8ae1-155">Tooling and administration</span></span>

<span data-ttu-id="c8ae1-156">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-156">Q.</span></span> <span data-ttu-id="c8ae1-157">Prenez-vous en charge les projets de base de données dans Visual Studio ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="c8ae1-158">R.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-158">A.</span></span> <span data-ttu-id="c8ae1-159">À l’heure actuelle, nous ne prenons pas en charge les projets de base de données dans Visual Studio pour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="c8ae1-160">Si vous souhaitez que toocast un tooget vote cette fonctionnalité, visitez notre User Voice [demande des fonctionnalités des projets de base de données].</span><span class="sxs-lookup"><span data-stu-id="c8ae1-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="c8ae1-161">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-161">Q.</span></span> <span data-ttu-id="c8ae1-162">SQL Data Warehouse prend-il en charge les API REST ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="c8ae1-163">R.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-163">A.</span></span> <span data-ttu-id="c8ae1-164">Oui.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-164">Yes.</span></span> <span data-ttu-id="c8ae1-165">La plupart des fonctionnalités REST utilisables avec SQL Database sont également disponibles avec SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="c8ae1-166">Vous trouverez des informations sur les API sur les pages de documentation REST ou sur [MSDN].</span><span class="sxs-lookup"><span data-stu-id="c8ae1-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="c8ae1-167">Chargement</span><span class="sxs-lookup"><span data-stu-id="c8ae1-167">Loading</span></span>

<span data-ttu-id="c8ae1-168">Q :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-168">Q.</span></span> <span data-ttu-id="c8ae1-169">Quels pilotes clients prenez-vous en charge ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-169">What client drivers do you support?</span></span>

<span data-ttu-id="c8ae1-170">R :</span><span class="sxs-lookup"><span data-stu-id="c8ae1-170">A.</span></span> <span data-ttu-id="c8ae1-171">Prise en charge de pilote pour l’entrepôt de données se trouvent sur hello [les chaînes de connexion] page</span><span class="sxs-lookup"><span data-stu-id="c8ae1-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="c8ae1-172">Q : Quels sont les formats de fichier pris en charge par PolyBase avec SQL Data Warehouse ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="c8ae1-173">R : Orc, RC, Parquet et le texte plat délimité</span><span class="sxs-lookup"><span data-stu-id="c8ae1-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="c8ae1-174">Q : que se connecter à l’aide de PolyBase de toofrom SQL DW ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="c8ae1-175">R : [Azure Data Lake Store] et [Azure Storage Blobs].</span><span class="sxs-lookup"><span data-stu-id="c8ae1-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="c8ae1-176">Q : est poussée vers le bas de calcul possible lors de la connexion tooAzure d’objets BLOB de stockage ou ADLS ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="c8ae1-177">R : non, SQL Data Warehouse PolyBase interagit uniquement les composants de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="c8ae1-178">Q : puis-je connecter tooHDI ?</span><span class="sxs-lookup"><span data-stu-id="c8ae1-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="c8ae1-179">R : HDI pouvez utiliser ADLS ou WASB comme couche HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="c8ae1-180">Si vous avez l’un des deux comme couche HDFS, vous pouvez charger ces données dans SQL DW.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="c8ae1-181">Toutefois, vous ne pouvez pas générer instance HDI de poussée vers le bas calcul toohello.</span><span class="sxs-lookup"><span data-stu-id="c8ae1-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c8ae1-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c8ae1-182">Next steps</span></span>
<span data-ttu-id="c8ae1-183">Pour plus d’informations sur SQL Data Warehouse dans son ensemble, consultez notre page [Vue d’ensemble].</span><span class="sxs-lookup"><span data-stu-id="c8ae1-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[les chaînes de connexion]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[tickets de support]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Sécurité]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[Limites de capacité]: ./sql-data-warehouse-service-capacity-limits.md
[Types de données]: ./sql-data-warehouse-tables-data-types.md
[Fonctionnalités de table non prises en charge]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[demande des fonctionnalités des projets de base de données]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[Vue d’ensemble]: ./sql-data-warehouse-overview-faq.md