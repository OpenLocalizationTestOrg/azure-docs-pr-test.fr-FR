---
title: "sources de données aaaSupported dans Azure Data Catalog | Documents Microsoft"
description: "Cet article répertorie les spécifications hello actuellement pris en charge des sources de données."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: jstevens
editor: 
tags: 
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 4bfcabf31bf9fd781c939a5026abc42a5407df32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="fff47-103">Sources de données prises en charge dans Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="fff47-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="fff47-104">Vous pouvez publier des métadonnées à l’aide d’une API publique ou un clic-une fois outil d’inscription, ou en entrant manuellement les informations directement toohello Azure Data Catalog de portail web.</span><span class="sxs-lookup"><span data-stu-id="fff47-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly toohello Azure Data Catalog web portal.</span></span> <span data-ttu-id="fff47-105">Hello tableau suivant récapitule toutes les sources de données pris en charge par le catalogue de hello aujourd'hui et hello des fonctionnalités de publication pour chacun.</span><span class="sxs-lookup"><span data-stu-id="fff47-105">hello following table summarizes all data sources that are supported by hello catalog today, and hello publishing capabilities for each.</span></span> <span data-ttu-id="fff47-106">Est également répertoriées hello des outils de données externes que chaque source de données peut lancer à partir de notre expérience du portail « open in ».</span><span class="sxs-lookup"><span data-stu-id="fff47-106">Also listed are hello external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="fff47-107">Hello deuxième table contient une spécification plus technique de chaque propriété de connexion de source de données.</span><span class="sxs-lookup"><span data-stu-id="fff47-107">hello second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="fff47-108">Liste des sources de données prises en charge</span><span class="sxs-lookup"><span data-stu-id="fff47-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="fff47-109"><b>Objet de source de données</b></span><span class="sxs-lookup"><span data-stu-id="fff47-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="fff47-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="fff47-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="fff47-111"><b>Saisie manuelle</b></span><span class="sxs-lookup"><span data-stu-id="fff47-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="fff47-112"><b>Outil d’inscription</b></span><span class="sxs-lookup"><span data-stu-id="fff47-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="fff47-113"><b>Outils d’ouverture intégrés</b></span><span class="sxs-lookup"><span data-stu-id="fff47-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="fff47-114"><b>Remarques</b></span><span class="sxs-lookup"><span data-stu-id="fff47-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-115">Répertoire Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fff47-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="fff47-116">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-116">✓</span></span></td>
      <td><span data-ttu-id="fff47-117">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-117">✓</span></span></td>
      <td><span data-ttu-id="fff47-118">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-119">Fichier Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fff47-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="fff47-120">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-120">✓</span></span></td>
      <td><span data-ttu-id="fff47-121">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-121">✓</span></span></td>
      <td><span data-ttu-id="fff47-122">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-123">Stockage d'objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="fff47-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="fff47-124">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-124">✓</span></span></td>
      <td><span data-ttu-id="fff47-125">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-125">✓</span></span></td>
      <td><span data-ttu-id="fff47-126">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-126">✓</span></span></td>
      <td><span data-ttu-id="fff47-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-128">Répertoire de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="fff47-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="fff47-129">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-129">✓</span></span></td>
      <td><span data-ttu-id="fff47-130">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-130">✓</span></span></td>
      <td><span data-ttu-id="fff47-131">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-131">✓</span></span></td>
      <td><span data-ttu-id="fff47-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-133">Table de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="fff47-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="fff47-134">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-134">✓</span></span></td>
      <td><span data-ttu-id="fff47-135">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-135">✓</span></span></td>
      <td><span data-ttu-id="fff47-136">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-137">Répertoire HDFS</span><span class="sxs-lookup"><span data-stu-id="fff47-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="fff47-138">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-138">✓</span></span></td>
      <td><span data-ttu-id="fff47-139">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-139">✓</span></span></td>
      <td><span data-ttu-id="fff47-140">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-141">Fichier HDFS</span><span class="sxs-lookup"><span data-stu-id="fff47-141">HDFS file</span></span></td>
      <td><span data-ttu-id="fff47-142">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-142">✓</span></span></td>
      <td><span data-ttu-id="fff47-143">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-143">✓</span></span></td>
      <td><span data-ttu-id="fff47-144">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-145">Table hive</span><span class="sxs-lookup"><span data-stu-id="fff47-145">Hive table</span></span></td>
      <td><span data-ttu-id="fff47-146">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-146">✓</span></span></td>
      <td><span data-ttu-id="fff47-147">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-147">✓</span></span></td>
      <td><span data-ttu-id="fff47-148">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-148">✓</span></span></td>
      <td><span data-ttu-id="fff47-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="fff47-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-150">Affichage hive</span><span class="sxs-lookup"><span data-stu-id="fff47-150">Hive view</span></span></td>
      <td><span data-ttu-id="fff47-151">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-151">✓</span></span></td>
      <td><span data-ttu-id="fff47-152">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-152">✓</span></span></td>
      <td><span data-ttu-id="fff47-153">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-153">✓</span></span></td>
      <td><span data-ttu-id="fff47-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="fff47-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-155">Table MySQL</span><span class="sxs-lookup"><span data-stu-id="fff47-155">MySQL table</span></span></td>
      <td><span data-ttu-id="fff47-156">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-156">✓</span></span></td>
      <td><span data-ttu-id="fff47-157">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-157">✓</span></span></td>
      <td><span data-ttu-id="fff47-158">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-158">✓</span></span></td>
      <td><span data-ttu-id="fff47-159"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-160">Vue MySQL</span><span class="sxs-lookup"><span data-stu-id="fff47-160">MySQL view</span></span></td>
      <td><span data-ttu-id="fff47-161">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-161">✓</span></span></td>
      <td><span data-ttu-id="fff47-162">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-162">✓</span></span></td>
      <td><span data-ttu-id="fff47-163">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-163">✓</span></span></td>
      <td><span data-ttu-id="fff47-164"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-165">Table de base de données Oracle</span><span class="sxs-lookup"><span data-stu-id="fff47-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="fff47-166">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-166">✓</span></span></td>
      <td><span data-ttu-id="fff47-167">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-167">✓</span></span></td>
      <td><span data-ttu-id="fff47-168">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-168">✓</span></span></td>
      <td><span data-ttu-id="fff47-169"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-170">Vue de base de données Oracle</span><span class="sxs-lookup"><span data-stu-id="fff47-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="fff47-171">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-171">✓</span></span></td>
      <td><span data-ttu-id="fff47-172">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-172">✓</span></span></td>
      <td><span data-ttu-id="fff47-173">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-173">✓</span></span></td>
      <td><span data-ttu-id="fff47-174"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-175">Autre (ressource générique)</span><span class="sxs-lookup"><span data-stu-id="fff47-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="fff47-176">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-176">✓</span></span></td>
      <td><span data-ttu-id="fff47-177">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-178">Table Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fff47-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="fff47-179">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-179">✓</span></span></td>
      <td><span data-ttu-id="fff47-180">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-180">✓</span></span></td>
      <td><span data-ttu-id="fff47-181">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-181">✓</span></span></td>
      <td><span data-ttu-id="fff47-182"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="fff47-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-183">Vue SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fff47-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="fff47-184">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-184">✓</span></span></td>
      <td><span data-ttu-id="fff47-185">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-185">✓</span></span></td>
      <td><span data-ttu-id="fff47-186">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-186">✓</span></span></td>
      <td><span data-ttu-id="fff47-187"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="fff47-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-188">Dimension SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="fff47-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="fff47-189">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-189">✓</span></span></td>
      <td><span data-ttu-id="fff47-190">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-190">✓</span></span></td>
      <td><span data-ttu-id="fff47-191">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-191">✓</span></span></td>
      <td><span data-ttu-id="fff47-192"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-193">Indicateur de performance clé de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="fff47-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="fff47-194">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-194">✓</span></span></td>
      <td><span data-ttu-id="fff47-195">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-195">✓</span></span></td>
      <td><span data-ttu-id="fff47-196">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-196">✓</span></span></td>
      <td><span data-ttu-id="fff47-197"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-198">Mesure SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="fff47-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="fff47-199">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-199">✓</span></span></td>
      <td><span data-ttu-id="fff47-200">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-200">✓</span></span></td>
      <td><span data-ttu-id="fff47-201">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-201">✓</span></span></td>
      <td><span data-ttu-id="fff47-202"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-203">Table SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="fff47-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="fff47-204">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-204">✓</span></span></td>
      <td><span data-ttu-id="fff47-205">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-205">✓</span></span></td>
      <td><span data-ttu-id="fff47-206">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-206">✓</span></span></td>
      <td><span data-ttu-id="fff47-207"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-208">Rapport SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="fff47-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="fff47-209">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-209">✓</span></span></td>
      <td><span data-ttu-id="fff47-210">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-210">✓</span></span></td>
      <td><span data-ttu-id="fff47-211">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-211">✓</span></span></td>
      <td><span data-ttu-id="fff47-212"><font size=2>Browser</font></span><span class="sxs-lookup"><span data-stu-id="fff47-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="fff47-213"><font size=2>Serveurs en mode natif uniquement. Le mode SharePoint n’est pas pris en charge.</font></span><span class="sxs-lookup"><span data-stu-id="fff47-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-214">Table SQL Server</span><span class="sxs-lookup"><span data-stu-id="fff47-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="fff47-215">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-215">✓</span></span></td>
      <td><span data-ttu-id="fff47-216">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-216">✓</span></span></td>
      <td><span data-ttu-id="fff47-217">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-217">✓</span></span></td>
      <td><span data-ttu-id="fff47-218"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="fff47-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-219">Vue SQL Server</span><span class="sxs-lookup"><span data-stu-id="fff47-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="fff47-220">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-220">✓</span></span></td>
      <td><span data-ttu-id="fff47-221">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-221">✓</span></span></td>
      <td><span data-ttu-id="fff47-222">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-222">✓</span></span></td>
      <td><span data-ttu-id="fff47-223"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="fff47-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-224">Table Teradata</span><span class="sxs-lookup"><span data-stu-id="fff47-224">Teradata table</span></span></td>
      <td><span data-ttu-id="fff47-225">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-225">✓</span></span></td>
      <td><span data-ttu-id="fff47-226">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-226">✓</span></span></td>
      <td><span data-ttu-id="fff47-227">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-227">✓</span></span></td>
      <td><span data-ttu-id="fff47-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="fff47-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-229">Vue Teradata</span><span class="sxs-lookup"><span data-stu-id="fff47-229">Teradata view</span></span></td>
      <td><span data-ttu-id="fff47-230">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-230">✓</span></span></td>
      <td><span data-ttu-id="fff47-231">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-231">✓</span></span></td>
      <td><span data-ttu-id="fff47-232">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-232">✓</span></span></td>
      <td><span data-ttu-id="fff47-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="fff47-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-234">Vue SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fff47-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="fff47-235">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-235">✓</span></span></td>
      <td><span data-ttu-id="fff47-236">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-236">✓</span></span></td>
      <td><span data-ttu-id="fff47-237">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-237">✓</span></span></td>
      <td><span data-ttu-id="fff47-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="fff47-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-239">Table DB2</span><span class="sxs-lookup"><span data-stu-id="fff47-239">DB2 table</span></span></td>
      <td><span data-ttu-id="fff47-240">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-240">✓</span></span></td>
      <td><span data-ttu-id="fff47-241">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-241">✓</span></span></td>
      <td><span data-ttu-id="fff47-242">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-243">Vue DB2</span><span class="sxs-lookup"><span data-stu-id="fff47-243">DB2 view</span></span></td>
      <td><span data-ttu-id="fff47-244">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-244">✓</span></span></td>
      <td><span data-ttu-id="fff47-245">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-245">✓</span></span></td>
      <td><span data-ttu-id="fff47-246">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-247">Fichier de système de fichiers</span><span class="sxs-lookup"><span data-stu-id="fff47-247">File system file</span></span></td>
      <td><span data-ttu-id="fff47-248">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-249">Répertoire FTP</span><span class="sxs-lookup"><span data-stu-id="fff47-249">FTP directory</span></span></td>
      <td><span data-ttu-id="fff47-250">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-250">✓</span></span></td>
      <td><span data-ttu-id="fff47-251">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-251">✓</span></span></td>
      <td><span data-ttu-id="fff47-252">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-253">Fichier FTP</span><span class="sxs-lookup"><span data-stu-id="fff47-253">FTP file</span></span></td>
      <td><span data-ttu-id="fff47-254">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-254">✓</span></span></td>
      <td><span data-ttu-id="fff47-255">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-255">✓</span></span></td>
      <td><span data-ttu-id="fff47-256">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-257">Rapport HTTP</span><span class="sxs-lookup"><span data-stu-id="fff47-257">HTTP report</span></span></td>
      <td><span data-ttu-id="fff47-258">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-259">Point de terminaison HTTP</span><span class="sxs-lookup"><span data-stu-id="fff47-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="fff47-260">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-261">Fichier HTTP</span><span class="sxs-lookup"><span data-stu-id="fff47-261">HTTP file</span></span></td>
      <td><span data-ttu-id="fff47-262">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-263">Jeu d’entités OData</span><span class="sxs-lookup"><span data-stu-id="fff47-263">OData entity set</span></span></td>
      <td><span data-ttu-id="fff47-264">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-265">Fonction OData</span><span class="sxs-lookup"><span data-stu-id="fff47-265">OData function</span></span></td>
      <td><span data-ttu-id="fff47-266">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-267">Table PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="fff47-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="fff47-268">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-268">✓</span></span></td>
      <td><span data-ttu-id="fff47-269">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-269">✓</span></span></td>
      <td><span data-ttu-id="fff47-270">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-271">Vue PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="fff47-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="fff47-272">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-272">✓</span></span></td>
      <td><span data-ttu-id="fff47-273">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-273">✓</span></span></td>
      <td><span data-ttu-id="fff47-274">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-275">Vue SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fff47-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="fff47-276">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="fff47-277">Objet Salesforce</span><span class="sxs-lookup"><span data-stu-id="fff47-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="fff47-278">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-278">✓</span></span></td>
      <td><span data-ttu-id="fff47-279">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-279">✓</span></span></td>
      <td><span data-ttu-id="fff47-280">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-281">Liste SharePoint</span><span class="sxs-lookup"><span data-stu-id="fff47-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="fff47-282">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-283">Collection Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fff47-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="fff47-284">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-284">✓</span></span></td>
      <td><span data-ttu-id="fff47-285">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-285">✓</span></span></td>
      <td><span data-ttu-id="fff47-286">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-287">Table ODBC générique</span><span class="sxs-lookup"><span data-stu-id="fff47-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="fff47-288">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-288">✓</span></span></td>
      <td><span data-ttu-id="fff47-289">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-289">✓</span></span></td>
      <td><span data-ttu-id="fff47-290">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-291">Vue ODBC générique</span><span class="sxs-lookup"><span data-stu-id="fff47-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="fff47-292">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-292">✓</span></span></td>
      <td><span data-ttu-id="fff47-293">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-293">✓</span></span></td>
      <td><span data-ttu-id="fff47-294">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-295">Table Cassandra</span><span class="sxs-lookup"><span data-stu-id="fff47-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="fff47-296">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-296">✓</span></span></td>
      <td><span data-ttu-id="fff47-297">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-297">✓</span></span></td>
      <td><span data-ttu-id="fff47-298">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="fff47-299"><font size=2>Publier en tant que ressource ODBC générique</font></span><span class="sxs-lookup"><span data-stu-id="fff47-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-300">Vue Cassandra</span><span class="sxs-lookup"><span data-stu-id="fff47-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="fff47-301">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-301">✓</span></span></td>
      <td><span data-ttu-id="fff47-302">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-302">✓</span></span></td>
      <td><span data-ttu-id="fff47-303">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="fff47-304"><font size=2>Publier en tant que ressource ODBC générique</font></span><span class="sxs-lookup"><span data-stu-id="fff47-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-305">Table Sybase</span><span class="sxs-lookup"><span data-stu-id="fff47-305">Sybase table</span></span></td>
      <td><span data-ttu-id="fff47-306">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-306">✓</span></span></td>
      <td><span data-ttu-id="fff47-307">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-307">✓</span></span></td>
      <td><span data-ttu-id="fff47-308">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-309">Vue Sybase</span><span class="sxs-lookup"><span data-stu-id="fff47-309">Sybase view</span></span></td>
      <td><span data-ttu-id="fff47-310">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-310">✓</span></span></td>
      <td><span data-ttu-id="fff47-311">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-311">✓</span></span></td>
      <td><span data-ttu-id="fff47-312">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-313">Table MongoDB</span><span class="sxs-lookup"><span data-stu-id="fff47-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="fff47-314">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-314">✓</span></span></td>
      <td><span data-ttu-id="fff47-315">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-315">✓</span></span></td>
      <td><span data-ttu-id="fff47-316">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="fff47-317"><font size=2>Publier en tant que ressource ODBC générique</font></span><span class="sxs-lookup"><span data-stu-id="fff47-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-318">Vue MongoDB</span><span class="sxs-lookup"><span data-stu-id="fff47-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="fff47-319">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-319">✓</span></span></td>
      <td><span data-ttu-id="fff47-320">✓ </span><span class="sxs-lookup"><span data-stu-id="fff47-320">✓</span></span></td>
      <td><span data-ttu-id="fff47-321">✓</span><span class="sxs-lookup"><span data-stu-id="fff47-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="fff47-322"><font size=2>Publier en tant que ressource ODBC générique</font></span><span class="sxs-lookup"><span data-stu-id="fff47-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="fff47-323">Si vous devez prendre en charge des sources supplémentaires, envoyez un toohello de demande de fonctionnalité [forum Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="fff47-323">If you need support for additional sources, submit a feature request toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="fff47-324">Spécification de référence de la source de données</span><span class="sxs-lookup"><span data-stu-id="fff47-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="fff47-325">Hello **structure DSL** colonne Bonjour tableau suivant répertorie uniquement hello propriétés de connexion pour le jeu de propriétés « address » sont utilisées par Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="fff47-325">hello **DSL structure** column in hello following table lists only hello connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="fff47-326">Autrement dit, sac de propriétés « address » peut contenir d’autres propriétés de connexion de source de données hello persiste Azure Data Catalog, mais n’utilise pas.</span><span class="sxs-lookup"><span data-stu-id="fff47-326">That is, "address" property bag can contain other connection properties of hello data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="fff47-327"><b>Type de source</b></span><span class="sxs-lookup"><span data-stu-id="fff47-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="fff47-328"><b>Type de ressource</b></span><span class="sxs-lookup"><span data-stu-id="fff47-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="fff47-329"><b>Types d’objets</b></span><span class="sxs-lookup"><span data-stu-id="fff47-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="fff47-330"><b>Structure DSL<b></span><span class="sxs-lookup"><span data-stu-id="fff47-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-331">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fff47-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="fff47-332">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-332">Container</span></span></td>
      <td><span data-ttu-id="fff47-333">Data Lake</span><span class="sxs-lookup"><span data-stu-id="fff47-333">Data Lake</span></span></td>
      <td><span data-ttu-id="fff47-334">
        <font size=2> Protocole : webhdfs</span><span class="sxs-lookup"><span data-stu-id="fff47-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="fff47-335">Authentification : {de base, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="fff47-336">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-336">Address:</span></span> <br><span data-ttu-id="fff47-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-338">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fff47-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="fff47-339">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-339">Table</span></span></td>
      <td><span data-ttu-id="fff47-340">Répertoire, fichier</span><span class="sxs-lookup"><span data-stu-id="fff47-340">Directory, file</span></span></td>
      <td><span data-ttu-id="fff47-341">
        <font size=2> Protocole : webhdfs</span><span class="sxs-lookup"><span data-stu-id="fff47-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="fff47-342">Authentification : {de base, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="fff47-343">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-343">Address:</span></span> <br><span data-ttu-id="fff47-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-345">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fff47-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="fff47-346">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-346">Container</span></span></td>
      <td><span data-ttu-id="fff47-347">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-347">Container</span></span></td>
      <td><span data-ttu-id="fff47-348">
        <font size=2> Protocole : azure-blobs</span><span class="sxs-lookup"><span data-stu-id="fff47-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="fff47-349">Authentication : {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="fff47-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="fff47-350">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-350">Address:</span></span> <br><span data-ttu-id="fff47-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="fff47-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="fff47-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="fff47-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="fff47-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-354">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fff47-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="fff47-355">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-355">Table</span></span></td>
      <td><span data-ttu-id="fff47-356">Objet blob, répertoire</span><span class="sxs-lookup"><span data-stu-id="fff47-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="fff47-357">
        <font size=2> Protocole : azure-blobs</span><span class="sxs-lookup"><span data-stu-id="fff47-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="fff47-358">Authentication : {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="fff47-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="fff47-359">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-359">Address:</span></span> <br><span data-ttu-id="fff47-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="fff47-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="fff47-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="fff47-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="fff47-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="fff47-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-364">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fff47-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="fff47-365">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-365">Container</span></span></td>
      <td><span data-ttu-id="fff47-366">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-366">Container</span></span></td>
      <td><span data-ttu-id="fff47-367">
        <font size=2> Protocole : azure-tables</span><span class="sxs-lookup"><span data-stu-id="fff47-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="fff47-368">Authentication : {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="fff47-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="fff47-369">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-369">Address:</span></span> <br><span data-ttu-id="fff47-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="fff47-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="fff47-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-372">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fff47-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="fff47-373">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-373">Table</span></span></td>
      <td><span data-ttu-id="fff47-374">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-374">Table</span></span></td>
      <td><span data-ttu-id="fff47-375">
        <font size=2> Protocole : azure-tables</span><span class="sxs-lookup"><span data-stu-id="fff47-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="fff47-376">Authentication : {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="fff47-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="fff47-377">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-377">Address:</span></span> <br><span data-ttu-id="fff47-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="fff47-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="fff47-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="fff47-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="fff47-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="fff47-381">Cosmos</span></span></td>
      <td><span data-ttu-id="fff47-382">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-382">Container</span></span></td>
      <td><span data-ttu-id="fff47-383">Cluster virtuel</span><span class="sxs-lookup"><span data-stu-id="fff47-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="fff47-384">
        <font size=2> Protocole : cosmos</span><span class="sxs-lookup"><span data-stu-id="fff47-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="fff47-385">Authentification : {de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-386">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-386">Address:</span></span> <br><span data-ttu-id="fff47-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="fff47-388">Cosmos</span></span></td>
      <td><span data-ttu-id="fff47-389">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-389">Table</span></span></td>
      <td><span data-ttu-id="fff47-390">Flux, ensemble de flux, vue</span><span class="sxs-lookup"><span data-stu-id="fff47-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="fff47-391">
        <font size=2> Protocole : cosmos</span><span class="sxs-lookup"><span data-stu-id="fff47-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="fff47-392">Authentification : {de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-393">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-393">Address:</span></span> <br><span data-ttu-id="fff47-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="fff47-395">Datazen</span></span></td>
      <td><span data-ttu-id="fff47-396">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-396">Container</span></span></td>
      <td><span data-ttu-id="fff47-397">Site</span><span class="sxs-lookup"><span data-stu-id="fff47-397">Site</span></span></td>
      <td><span data-ttu-id="fff47-398">
        <font size=2> Protocole : http</span><span class="sxs-lookup"><span data-stu-id="fff47-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="fff47-399">Authentification : {aucune, de base, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="fff47-400">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-400">Address:</span></span> <br><span data-ttu-id="fff47-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="fff47-402">Datazen</span></span></td>
      <td><span data-ttu-id="fff47-403">Rapport</span><span class="sxs-lookup"><span data-stu-id="fff47-403">Report</span></span></td>
      <td><span data-ttu-id="fff47-404">Rapport, tableau de bord</span><span class="sxs-lookup"><span data-stu-id="fff47-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="fff47-405">
        <font size=2> Protocole : http</span><span class="sxs-lookup"><span data-stu-id="fff47-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="fff47-406">Authentification : {aucune, de base, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="fff47-407">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-407">Address:</span></span> <br><span data-ttu-id="fff47-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-409">DB2</span><span class="sxs-lookup"><span data-stu-id="fff47-409">DB2</span></span></td>
      <td><span data-ttu-id="fff47-410">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-410">Container</span></span></td>
      <td><span data-ttu-id="fff47-411">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-411">Database</span></span></td>
      <td><span data-ttu-id="fff47-412">
        <font size=2> Protocole : db2</span><span class="sxs-lookup"><span data-stu-id="fff47-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="fff47-413">Authentification : {de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-414">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-414">Address:</span></span> <br><span data-ttu-id="fff47-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-417">DB2</span><span class="sxs-lookup"><span data-stu-id="fff47-417">DB2</span></span></td>
      <td><span data-ttu-id="fff47-418">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-418">Table</span></span></td>
      <td><span data-ttu-id="fff47-419">Table, vue</span><span class="sxs-lookup"><span data-stu-id="fff47-419">Table, view</span></span></td>
      <td><span data-ttu-id="fff47-420">
        <font size=2> Protocole : db2</span><span class="sxs-lookup"><span data-stu-id="fff47-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="fff47-421">Authentification : {de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-422">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-422">Address:</span></span> <br><span data-ttu-id="fff47-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="fff47-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="fff47-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-427">Système de fichiers</span><span class="sxs-lookup"><span data-stu-id="fff47-427">File system</span></span></td>
      <td><span data-ttu-id="fff47-428">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-428">Table</span></span></td>
      <td><span data-ttu-id="fff47-429">Fichier</span><span class="sxs-lookup"><span data-stu-id="fff47-429">File</span></span></td>
      <td><span data-ttu-id="fff47-430">
        <font size=2> Protocole : file</span><span class="sxs-lookup"><span data-stu-id="fff47-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="fff47-431">Authentification : {aucune, de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="fff47-432">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-432">Address:</span></span> <br><span data-ttu-id="fff47-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-434">FTP</span><span class="sxs-lookup"><span data-stu-id="fff47-434">FTP</span></span></td>
      <td><span data-ttu-id="fff47-435">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-435">Table</span></span></td>
      <td><span data-ttu-id="fff47-436">Répertoire, fichier</span><span class="sxs-lookup"><span data-stu-id="fff47-436">Directory, file</span></span></td>
      <td><span data-ttu-id="fff47-437">
        <font size=2> Protocol : ftp</span><span class="sxs-lookup"><span data-stu-id="fff47-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="fff47-438">Authentification : {aucune, de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="fff47-439">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-439">Address:</span></span> <br><span data-ttu-id="fff47-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-441">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="fff47-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="fff47-442">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-442">Container</span></span></td>
      <td><span data-ttu-id="fff47-443">Cluster</span><span class="sxs-lookup"><span data-stu-id="fff47-443">Cluster</span></span></td>
      <td><span data-ttu-id="fff47-444">
        <font size=2> Protocole : webhdfs</span><span class="sxs-lookup"><span data-stu-id="fff47-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="fff47-445">Authentification : {de base, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="fff47-446">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-446">Address:</span></span> <br><span data-ttu-id="fff47-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-448">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="fff47-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="fff47-449">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-449">Table</span></span></td>
      <td><span data-ttu-id="fff47-450">Répertoire, fichier</span><span class="sxs-lookup"><span data-stu-id="fff47-450">Directory, file</span></span></td>
      <td><span data-ttu-id="fff47-451">
        <font size=2> Protocole : webhdfs</span><span class="sxs-lookup"><span data-stu-id="fff47-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="fff47-452">Authentification : {de base, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="fff47-453">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-453">Address:</span></span> <br><span data-ttu-id="fff47-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-455">Hive</span><span class="sxs-lookup"><span data-stu-id="fff47-455">Hive</span></span></td>
      <td><span data-ttu-id="fff47-456">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-456">Container</span></span></td>
      <td><span data-ttu-id="fff47-457">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-457">Database</span></span></td>
      <td><span data-ttu-id="fff47-458">
        <font size=2> Protocole : hive</span><span class="sxs-lookup"><span data-stu-id="fff47-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="fff47-459">Authentification : {hdinsight, de base, nom d’utilisateur, aucune}</span><span class="sxs-lookup"><span data-stu-id="fff47-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="fff47-460">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-460">Address:</span></span> <br><span data-ttu-id="fff47-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-463">connectionProperties :</span><span class="sxs-lookup"><span data-stu-id="fff47-463">connectionProperties:</span></span> <br><span data-ttu-id="fff47-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-465">Hive</span><span class="sxs-lookup"><span data-stu-id="fff47-465">Hive</span></span></td>
      <td><span data-ttu-id="fff47-466">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-466">Table</span></span></td>
      <td><span data-ttu-id="fff47-467">Table, vue</span><span class="sxs-lookup"><span data-stu-id="fff47-467">Table, view</span></span></td>
      <td><span data-ttu-id="fff47-468">
        <font size=2> Protocole : hive</span><span class="sxs-lookup"><span data-stu-id="fff47-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="fff47-469">Authentification : {hdinsight, de base, nom d’utilisateur, aucune}</span><span class="sxs-lookup"><span data-stu-id="fff47-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="fff47-470">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-470">Address:</span></span> <br><span data-ttu-id="fff47-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="fff47-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="fff47-474">connectionProperties :</span><span class="sxs-lookup"><span data-stu-id="fff47-474">connectionProperties:</span></span> <br><span data-ttu-id="fff47-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-476">HTTP</span><span class="sxs-lookup"><span data-stu-id="fff47-476">HTTP</span></span></td>
      <td><span data-ttu-id="fff47-477">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-477">Container</span></span></td>
      <td><span data-ttu-id="fff47-478">Site</span><span class="sxs-lookup"><span data-stu-id="fff47-478">Site</span></span></td>
      <td><span data-ttu-id="fff47-479">
        <font size=2> Protocole : http</span><span class="sxs-lookup"><span data-stu-id="fff47-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="fff47-480">Authentification : {aucune, de base, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="fff47-481">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-481">Address:</span></span> <br><span data-ttu-id="fff47-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-483">HTTP</span><span class="sxs-lookup"><span data-stu-id="fff47-483">HTTP</span></span></td>
      <td><span data-ttu-id="fff47-484">Rapport</span><span class="sxs-lookup"><span data-stu-id="fff47-484">Report</span></span></td>
      <td><span data-ttu-id="fff47-485">Rapport, tableau de bord</span><span class="sxs-lookup"><span data-stu-id="fff47-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="fff47-486">
        <font size=2> Protocole : http</span><span class="sxs-lookup"><span data-stu-id="fff47-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="fff47-487">Authentification : {aucune, de base, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="fff47-488">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-488">Address:</span></span> <br><span data-ttu-id="fff47-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-490">HTTP</span><span class="sxs-lookup"><span data-stu-id="fff47-490">HTTP</span></span></td>
      <td><span data-ttu-id="fff47-491">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-491">Table</span></span></td>
      <td><span data-ttu-id="fff47-492">Point de terminaison, fichier</span><span class="sxs-lookup"><span data-stu-id="fff47-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="fff47-493">
        <font size=2> Protocole : http</span><span class="sxs-lookup"><span data-stu-id="fff47-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="fff47-494">Authentification : {aucune, de base, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="fff47-495">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-495">Address:</span></span> <br><span data-ttu-id="fff47-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="fff47-497">MySQL</span></span></td>
      <td><span data-ttu-id="fff47-498">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-498">Container</span></span></td>
      <td><span data-ttu-id="fff47-499">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-499">Database</span></span></td>
      <td><span data-ttu-id="fff47-500">
        <font size=2> Protocole : mysql</span><span class="sxs-lookup"><span data-stu-id="fff47-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="fff47-501">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-502">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-502">Address:</span></span> <br><span data-ttu-id="fff47-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="fff47-505">MySQL</span></span></td>
      <td><span data-ttu-id="fff47-506">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-506">Table</span></span></td>
      <td><span data-ttu-id="fff47-507">Table, vue</span><span class="sxs-lookup"><span data-stu-id="fff47-507">Table, view</span></span></td>
      <td><span data-ttu-id="fff47-508">
        <font size=2> Protocole : mysql</span><span class="sxs-lookup"><span data-stu-id="fff47-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="fff47-509">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-510">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-510">Address:</span></span> <br><span data-ttu-id="fff47-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-514">OData</span><span class="sxs-lookup"><span data-stu-id="fff47-514">OData</span></span></td>
      <td><span data-ttu-id="fff47-515">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-515">Container</span></span></td>
      <td><span data-ttu-id="fff47-516">Conteneur d’entités</span><span class="sxs-lookup"><span data-stu-id="fff47-516">Entity container</span></span></td>
      <td><span data-ttu-id="fff47-517">
        <font size=2> Protocole : odata</span><span class="sxs-lookup"><span data-stu-id="fff47-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="fff47-518">Authentification : {aucune, de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="fff47-519">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-519">Address:</span></span> <br><span data-ttu-id="fff47-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-521">OData</span><span class="sxs-lookup"><span data-stu-id="fff47-521">OData</span></span></td>
      <td><span data-ttu-id="fff47-522">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-522">Table</span></span></td>
      <td><span data-ttu-id="fff47-523">Jeu d’entités, fonction</span><span class="sxs-lookup"><span data-stu-id="fff47-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="fff47-524">
        <font size=2> Protocole : odata</span><span class="sxs-lookup"><span data-stu-id="fff47-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="fff47-525">Authentification : {aucune, de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="fff47-526">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-526">Address:</span></span> <br><span data-ttu-id="fff47-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="fff47-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="fff47-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-529">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="fff47-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="fff47-530">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-530">Container</span></span></td>
      <td><span data-ttu-id="fff47-531">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-531">Database</span></span></td>
      <td><span data-ttu-id="fff47-532">
        <font size=2> Protocole : oracle</span><span class="sxs-lookup"><span data-stu-id="fff47-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="fff47-533">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-534">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-534">Address:</span></span> <br><span data-ttu-id="fff47-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-537">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="fff47-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="fff47-538">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-538">Table</span></span></td>
      <td><span data-ttu-id="fff47-539">Table, vue</span><span class="sxs-lookup"><span data-stu-id="fff47-539">Table, view</span></span></td>
      <td><span data-ttu-id="fff47-540">
        <font size=2> Protocole : oracle</span><span class="sxs-lookup"><span data-stu-id="fff47-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="fff47-541">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-542">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-542">Address:</span></span> <br><span data-ttu-id="fff47-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="fff47-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="fff47-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="fff47-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="fff47-548">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-548">Container</span></span></td>
      <td><span data-ttu-id="fff47-549">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-549">Database</span></span></td>
      <td><span data-ttu-id="fff47-550">
        <font size=2> Protocole : postgresql</span><span class="sxs-lookup"><span data-stu-id="fff47-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="fff47-551">Authentification : {de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-552">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-552">Address:</span></span> <br><span data-ttu-id="fff47-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="fff47-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="fff47-556">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-556">Table</span></span></td>
      <td><span data-ttu-id="fff47-557">Table, vue</span><span class="sxs-lookup"><span data-stu-id="fff47-557">Table, view</span></span></td>
      <td><span data-ttu-id="fff47-558">
        <font size=2> Protocole : postgresql</span><span class="sxs-lookup"><span data-stu-id="fff47-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="fff47-559">Authentification : {de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-560">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-560">Address:</span></span> <br><span data-ttu-id="fff47-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="fff47-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="fff47-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="fff47-565">Power BI</span></span></td>
      <td><span data-ttu-id="fff47-566">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-566">Container</span></span></td>
      <td><span data-ttu-id="fff47-567">Site</span><span class="sxs-lookup"><span data-stu-id="fff47-567">Site</span></span></td>
      <td><span data-ttu-id="fff47-568">
        <font size=2> Protocole : http</span><span class="sxs-lookup"><span data-stu-id="fff47-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="fff47-569">Authentification : {aucune, de base, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="fff47-570">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-570">Address:</span></span> <br><span data-ttu-id="fff47-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="fff47-572">Power BI</span></span></td>
      <td><span data-ttu-id="fff47-573">Rapport</span><span class="sxs-lookup"><span data-stu-id="fff47-573">Report</span></span></td>
      <td><span data-ttu-id="fff47-574">Rapport, tableau de bord</span><span class="sxs-lookup"><span data-stu-id="fff47-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="fff47-575">
        <font size=2> Protocole : http</span><span class="sxs-lookup"><span data-stu-id="fff47-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="fff47-576">Authentification : {aucune, de base, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="fff47-577">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-577">Address:</span></span> <br><span data-ttu-id="fff47-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="fff47-579">Power Query</span></span></td>
      <td><span data-ttu-id="fff47-580">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-580">Table</span></span></td>
      <td><span data-ttu-id="fff47-581">Application Web hybride</span><span class="sxs-lookup"><span data-stu-id="fff47-581">Data mashup</span></span></td>
      <td><span data-ttu-id="fff47-582">
        <font size=2> Protocole : power-query</span><span class="sxs-lookup"><span data-stu-id="fff47-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="fff47-583">Authentification : {oauth}</span><span class="sxs-lookup"><span data-stu-id="fff47-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="fff47-584">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-584">Address:</span></span> <br><span data-ttu-id="fff47-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="fff47-586">Salesforce</span></span></td>
      <td><span data-ttu-id="fff47-587">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-587">Table</span></span></td>
      <td><span data-ttu-id="fff47-588">Object</span><span class="sxs-lookup"><span data-stu-id="fff47-588">Object</span></span></td>
      <td><span data-ttu-id="fff47-589">
        <font size=2> Protocole : salesforce-com</span><span class="sxs-lookup"><span data-stu-id="fff47-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="fff47-590">Authentification : {de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-591">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-591">Address:</span></span> <br><span data-ttu-id="fff47-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="fff47-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="fff47-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span><span class="sxs-lookup"><span data-stu-id="fff47-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="fff47-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fff47-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="fff47-596">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-596">Container</span></span></td>
      <td><span data-ttu-id="fff47-597">Serveur</span><span class="sxs-lookup"><span data-stu-id="fff47-597">Server</span></span></td>
      <td><span data-ttu-id="fff47-598">
        <font size=2> Protocole : sap hana-sql</span><span class="sxs-lookup"><span data-stu-id="fff47-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="fff47-599">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-600">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-600">Address:</span></span> <br><span data-ttu-id="fff47-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fff47-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="fff47-603">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-603">Table</span></span></td>
      <td><span data-ttu-id="fff47-604">Affichage</span><span class="sxs-lookup"><span data-stu-id="fff47-604">View</span></span></td>
      <td><span data-ttu-id="fff47-605">
        <font size=2> Protocole : sap hana-sql</span><span class="sxs-lookup"><span data-stu-id="fff47-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="fff47-606">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-607">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-607">Address:</span></span> <br><span data-ttu-id="fff47-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="fff47-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="fff47-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="fff47-611">SharePoint</span></span></td>
      <td><span data-ttu-id="fff47-612">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-612">Table</span></span></td>
      <td><span data-ttu-id="fff47-613">Énumérer</span><span class="sxs-lookup"><span data-stu-id="fff47-613">List</span></span></td>
      <td><span data-ttu-id="fff47-614">
        <font size=2> Protocole : sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="fff47-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="fff47-615">Authentification : {de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-616">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-616">Address:</span></span> <br><span data-ttu-id="fff47-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-618">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fff47-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="fff47-619">Commande</span><span class="sxs-lookup"><span data-stu-id="fff47-619">Command</span></span></td>
      <td><span data-ttu-id="fff47-620">Procédure stockée</span><span class="sxs-lookup"><span data-stu-id="fff47-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="fff47-621">
        <font size=2> Protocole : tds</span><span class="sxs-lookup"><span data-stu-id="fff47-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="fff47-622">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-623">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-623">Address:</span></span> <br><span data-ttu-id="fff47-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="fff47-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="fff47-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-628">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fff47-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="fff47-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="fff47-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="fff47-630">Fonction table</span><span class="sxs-lookup"><span data-stu-id="fff47-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="fff47-631">
        <font size=2> Protocole : tds</span><span class="sxs-lookup"><span data-stu-id="fff47-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="fff47-632">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-633">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-633">Address:</span></span> <br><span data-ttu-id="fff47-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="fff47-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="fff47-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-638">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fff47-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="fff47-639">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-639">Container</span></span></td>
      <td><span data-ttu-id="fff47-640">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-640">Database</span></span></td>
      <td><span data-ttu-id="fff47-641">
        <font size=2> Protocole : tds</span><span class="sxs-lookup"><span data-stu-id="fff47-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="fff47-642">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-643">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-643">Address:</span></span> <br><span data-ttu-id="fff47-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-646">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fff47-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="fff47-647">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-647">Table</span></span></td>
      <td><span data-ttu-id="fff47-648">Table, vue</span><span class="sxs-lookup"><span data-stu-id="fff47-648">Table, view</span></span></td>
      <td><span data-ttu-id="fff47-649">
        <font size=2> Protocole : tds</span><span class="sxs-lookup"><span data-stu-id="fff47-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="fff47-650">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-651">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-651">Address:</span></span> <br><span data-ttu-id="fff47-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="fff47-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="fff47-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="fff47-656">SQL Server</span></span></td>
      <td><span data-ttu-id="fff47-657">Commande</span><span class="sxs-lookup"><span data-stu-id="fff47-657">Command</span></span></td>
      <td><span data-ttu-id="fff47-658">Procédure stockée</span><span class="sxs-lookup"><span data-stu-id="fff47-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="fff47-659">
        <font size=2> Protocole : tds</span><span class="sxs-lookup"><span data-stu-id="fff47-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="fff47-660">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-661">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-661">Address:</span></span> <br><span data-ttu-id="fff47-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="fff47-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="fff47-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="fff47-666">SQL Server</span></span></td>
      <td><span data-ttu-id="fff47-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="fff47-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="fff47-668">Fonction table</span><span class="sxs-lookup"><span data-stu-id="fff47-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="fff47-669">
        <font size=2> Protocole : tds</span><span class="sxs-lookup"><span data-stu-id="fff47-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="fff47-670">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-671">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-671">Address:</span></span> <br><span data-ttu-id="fff47-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="fff47-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="fff47-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="fff47-676">SQL Server</span></span></td>
      <td><span data-ttu-id="fff47-677">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-677">Container</span></span></td>
      <td><span data-ttu-id="fff47-678">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-678">Database</span></span></td>
      <td><span data-ttu-id="fff47-679">
        <font size=2> Protocole : tds</span><span class="sxs-lookup"><span data-stu-id="fff47-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="fff47-680">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-681">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-681">Address:</span></span> <br><span data-ttu-id="fff47-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="fff47-684">SQL Server</span></span></td>
      <td><span data-ttu-id="fff47-685">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-685">Table</span></span></td>
      <td><span data-ttu-id="fff47-686">Table, vue</span><span class="sxs-lookup"><span data-stu-id="fff47-686">Table, view</span></span></td>
      <td><span data-ttu-id="fff47-687">
        <font size=2> Protocole : tds</span><span class="sxs-lookup"><span data-stu-id="fff47-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="fff47-688">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-689">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-689">Address:</span></span> <br><span data-ttu-id="fff47-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="fff47-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="fff47-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-694">SQL Server Analysis Services multidimensionnel</span><span class="sxs-lookup"><span data-stu-id="fff47-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="fff47-695">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-695">Container</span></span></td>
      <td><span data-ttu-id="fff47-696">Modèle</span><span class="sxs-lookup"><span data-stu-id="fff47-696">Model</span></span></td>
      <td><span data-ttu-id="fff47-697">
        <font size=2> Protocole : analysis-services</span><span class="sxs-lookup"><span data-stu-id="fff47-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="fff47-698">Authentification : {windows, de base, anonyme, aucune}</span><span class="sxs-lookup"><span data-stu-id="fff47-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="fff47-699">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-699">Address:</span></span> <br><span data-ttu-id="fff47-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-703">SQL Server Analysis Services multidimensionnel</span><span class="sxs-lookup"><span data-stu-id="fff47-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="fff47-704">KPI</span><span class="sxs-lookup"><span data-stu-id="fff47-704">KPI</span></span></td>
      <td><span data-ttu-id="fff47-705">KPI</span><span class="sxs-lookup"><span data-stu-id="fff47-705">KPI</span></span></td>
      <td><span data-ttu-id="fff47-706">
        <font size=2> Protocole : analysis-services</span><span class="sxs-lookup"><span data-stu-id="fff47-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="fff47-707">Authentification : {windows, de base, anonyme, aucune}</span><span class="sxs-lookup"><span data-stu-id="fff47-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="fff47-708">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-708">Address:</span></span> <br><span data-ttu-id="fff47-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="fff47-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="fff47-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="fff47-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="fff47-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-714">SQL Server Analysis Services multidimensionnel</span><span class="sxs-lookup"><span data-stu-id="fff47-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="fff47-715">Measure</span><span class="sxs-lookup"><span data-stu-id="fff47-715">Measure</span></span></td>
      <td><span data-ttu-id="fff47-716">Measure</span><span class="sxs-lookup"><span data-stu-id="fff47-716">Measure</span></span></td>
      <td><span data-ttu-id="fff47-717">
        <font size=2> Protocole : analysis-services</span><span class="sxs-lookup"><span data-stu-id="fff47-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="fff47-718">Authentification : {windows, de base, anonyme, aucune}</span><span class="sxs-lookup"><span data-stu-id="fff47-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="fff47-719">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-719">Address:</span></span> <br><span data-ttu-id="fff47-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="fff47-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="fff47-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="fff47-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="fff47-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-725">SQL Server Analysis Services multidimensionnel</span><span class="sxs-lookup"><span data-stu-id="fff47-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="fff47-726">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-726">Table</span></span></td>
      <td><span data-ttu-id="fff47-727">Dimension</span><span class="sxs-lookup"><span data-stu-id="fff47-727">Dimension</span></span></td>
      <td><span data-ttu-id="fff47-728">
        <font size=2> Protocole : analysis-services</span><span class="sxs-lookup"><span data-stu-id="fff47-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="fff47-729">Authentification : {windows, de base, anonyme, aucune}</span><span class="sxs-lookup"><span data-stu-id="fff47-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="fff47-730">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-730">Address:</span></span> <br><span data-ttu-id="fff47-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="fff47-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="fff47-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="fff47-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="fff47-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-736">Table SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="fff47-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="fff47-737">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-737">Container</span></span></td>
      <td><span data-ttu-id="fff47-738">Modèle</span><span class="sxs-lookup"><span data-stu-id="fff47-738">Model</span></span></td>
      <td><span data-ttu-id="fff47-739">
        <font size=2> Protocole : analysis-services</span><span class="sxs-lookup"><span data-stu-id="fff47-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="fff47-740">Authentification : {windows, de base, anonyme, aucune}</span><span class="sxs-lookup"><span data-stu-id="fff47-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="fff47-741">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-741">Address:</span></span> <br><span data-ttu-id="fff47-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-745">Table SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="fff47-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="fff47-746">KPI</span><span class="sxs-lookup"><span data-stu-id="fff47-746">KPI</span></span></td>
      <td><span data-ttu-id="fff47-747">KPI</span><span class="sxs-lookup"><span data-stu-id="fff47-747">KPI</span></span></td>
      <td><span data-ttu-id="fff47-748">
        <font size=2> Protocole : analysis-services</span><span class="sxs-lookup"><span data-stu-id="fff47-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="fff47-749">Authentification : {windows, de base, anonyme, aucune}</span><span class="sxs-lookup"><span data-stu-id="fff47-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="fff47-750">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-750">Address:</span></span> <br><span data-ttu-id="fff47-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="fff47-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="fff47-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="fff47-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="fff47-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-756">Table SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="fff47-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="fff47-757">Measure</span><span class="sxs-lookup"><span data-stu-id="fff47-757">Measure</span></span></td>
      <td><span data-ttu-id="fff47-758">Measure</span><span class="sxs-lookup"><span data-stu-id="fff47-758">Measure</span></span></td>
      <td><span data-ttu-id="fff47-759">
        <font size=2> Protocole : analysis-services</span><span class="sxs-lookup"><span data-stu-id="fff47-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="fff47-760">Authentification : {windows, de base, anonyme, aucune}</span><span class="sxs-lookup"><span data-stu-id="fff47-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="fff47-761">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-761">Address:</span></span> <br><span data-ttu-id="fff47-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="fff47-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="fff47-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="fff47-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="fff47-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-767">Table SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="fff47-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="fff47-768">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-768">Table</span></span></td>
      <td><span data-ttu-id="fff47-769">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-769">Table</span></span></td>
      <td><span data-ttu-id="fff47-770">
        <font size=2> Protocole : analysis-services</span><span class="sxs-lookup"><span data-stu-id="fff47-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="fff47-771">Authentification : {windows, de base, anonyme, aucune}</span><span class="sxs-lookup"><span data-stu-id="fff47-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="fff47-772">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-772">Address:</span></span> <br><span data-ttu-id="fff47-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="fff47-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="fff47-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="fff47-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="fff47-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="fff47-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="fff47-779">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-779">Container</span></span></td>
      <td><span data-ttu-id="fff47-780">Serveur</span><span class="sxs-lookup"><span data-stu-id="fff47-780">Server</span></span></td>
      <td><span data-ttu-id="fff47-781">
        <font size=2> Protocole : reporting-services</span><span class="sxs-lookup"><span data-stu-id="fff47-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="fff47-782">Authentification : {windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-782">Authentication: {windows}</span></span> <br><span data-ttu-id="fff47-783">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-783">Address:</span></span> <br><span data-ttu-id="fff47-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="fff47-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="fff47-787">Rapport</span><span class="sxs-lookup"><span data-stu-id="fff47-787">Report</span></span></td>
      <td><span data-ttu-id="fff47-788">Rapport</span><span class="sxs-lookup"><span data-stu-id="fff47-788">Report</span></span></td>
      <td><span data-ttu-id="fff47-789">
        <font size=2> Protocole : reporting-services</span><span class="sxs-lookup"><span data-stu-id="fff47-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="fff47-790">Authentification : {windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-790">Authentication: {windows}</span></span> <br><span data-ttu-id="fff47-791">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-791">Address:</span></span> <br><span data-ttu-id="fff47-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span><span class="sxs-lookup"><span data-stu-id="fff47-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="fff47-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="fff47-795">Teradata</span></span></td>
      <td><span data-ttu-id="fff47-796">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-796">Container</span></span></td>
      <td><span data-ttu-id="fff47-797">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-797">Database</span></span></td>
      <td><span data-ttu-id="fff47-798">
        <font size=2> Protocole : teradata</span><span class="sxs-lookup"><span data-stu-id="fff47-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="fff47-799">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-800">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-800">Address:</span></span> <br><span data-ttu-id="fff47-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="fff47-803">Teradata</span></span></td>
      <td><span data-ttu-id="fff47-804">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-804">Table</span></span></td>
      <td><span data-ttu-id="fff47-805">Table, vue</span><span class="sxs-lookup"><span data-stu-id="fff47-805">Table, view</span></span></td>
      <td><span data-ttu-id="fff47-806">
        <font size=2> Protocole : teradata</span><span class="sxs-lookup"><span data-stu-id="fff47-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="fff47-807">Authentification : {protocole, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="fff47-808">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-808">Address:</span></span> <br><span data-ttu-id="fff47-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="fff47-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="fff47-813">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-813">Container</span></span></td>
      <td><span data-ttu-id="fff47-814">Modèle</span><span class="sxs-lookup"><span data-stu-id="fff47-814">Model</span></span></td>
      <td><span data-ttu-id="fff47-815">
        <font size="2"> Protocole : mssql-mds</span><span class="sxs-lookup"><span data-stu-id="fff47-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="fff47-816">Authentification : {windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-816">Authentication: {windows}</span></span> <br><span data-ttu-id="fff47-817">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-817">Address:</span></span> <br><span data-ttu-id="fff47-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="fff47-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="fff47-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="fff47-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="fff47-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="fff47-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="fff47-822">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-822">Table</span></span></td>
      <td><span data-ttu-id="fff47-823">Entité</span><span class="sxs-lookup"><span data-stu-id="fff47-823">Entity</span></span></td>
      <td><span data-ttu-id="fff47-824">
        <font size="2"> Protocole : mssql-mds</span><span class="sxs-lookup"><span data-stu-id="fff47-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="fff47-825">Authentification : {windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-825">Authentication: {windows}</span></span> <br><span data-ttu-id="fff47-826">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-826">Address:</span></span> <br><span data-ttu-id="fff47-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="fff47-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="fff47-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="fff47-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="fff47-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span><span class="sxs-lookup"><span data-stu-id="fff47-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="fff47-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fff47-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="fff47-832">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-832">Container</span></span></td>
      <td><span data-ttu-id="fff47-833">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-833">Database</span></span></td>
      <td><span data-ttu-id="fff47-834">
        <font size=2> Protocole : document-db</span><span class="sxs-lookup"><span data-stu-id="fff47-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="fff47-835">Authentication : {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="fff47-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="fff47-836">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-836">Address:</span></span> <br><span data-ttu-id="fff47-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="fff47-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="fff47-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fff47-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="fff47-840">Collection</span><span class="sxs-lookup"><span data-stu-id="fff47-840">Collection</span></span></td>
      <td><span data-ttu-id="fff47-841">Collection</span><span class="sxs-lookup"><span data-stu-id="fff47-841">Collection</span></span></td>
      <td><span data-ttu-id="fff47-842">
        <font size=2> Protocole : document-db</span><span class="sxs-lookup"><span data-stu-id="fff47-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="fff47-843">Authentication : {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="fff47-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="fff47-844">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-844">Address:</span></span> <br><span data-ttu-id="fff47-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="fff47-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="fff47-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-847">&nbsp;Collection &nbsp;&nbsp;&nbsp;&nbsp;</font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-848">ODBC générique</span><span class="sxs-lookup"><span data-stu-id="fff47-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="fff47-849">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-849">Container</span></span></td>
      <td><span data-ttu-id="fff47-850">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-850">Database</span></span></td>
      <td><span data-ttu-id="fff47-851">
        <font size=2> Protocole : odbc</span><span class="sxs-lookup"><span data-stu-id="fff47-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="fff47-852">Authentification : {de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-853">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-853">Address:</span></span> <br><span data-ttu-id="fff47-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span><span class="sxs-lookup"><span data-stu-id="fff47-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="fff47-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-856">ODBC générique</span><span class="sxs-lookup"><span data-stu-id="fff47-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="fff47-857">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-857">Table</span></span></td>
      <td><span data-ttu-id="fff47-858">Table, Vue</span><span class="sxs-lookup"><span data-stu-id="fff47-858">Table, View</span></span></td>
      <td><span data-ttu-id="fff47-859">
        <font size=2> Protocole : odbc</span><span class="sxs-lookup"><span data-stu-id="fff47-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="fff47-860">Authentification : {de base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-861">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-861">Address:</span></span> <br><span data-ttu-id="fff47-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span><span class="sxs-lookup"><span data-stu-id="fff47-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="fff47-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="fff47-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="fff47-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="fff47-866">Sybase</span></span></td>
      <td><span data-ttu-id="fff47-867">Conteneur</span><span class="sxs-lookup"><span data-stu-id="fff47-867">Container</span></span></td>
      <td><span data-ttu-id="fff47-868">Base de données</span><span class="sxs-lookup"><span data-stu-id="fff47-868">Database</span></span></td>
      <td><span data-ttu-id="fff47-869">
        <font size=2> Protocole : sybase</span><span class="sxs-lookup"><span data-stu-id="fff47-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="fff47-870">authentification : {base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-871">adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-871">address:</span></span> <br><span data-ttu-id="fff47-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="fff47-874">Sybase</span></span></td>
      <td><span data-ttu-id="fff47-875">Table</span><span class="sxs-lookup"><span data-stu-id="fff47-875">Table</span></span></td>
      <td><span data-ttu-id="fff47-876">Table, Vue</span><span class="sxs-lookup"><span data-stu-id="fff47-876">Table, View</span></span></td>
      <td><span data-ttu-id="fff47-877">
        <font size=2> Protocole : sybase</span><span class="sxs-lookup"><span data-stu-id="fff47-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="fff47-878">authentification : {base, windows}</span><span class="sxs-lookup"><span data-stu-id="fff47-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="fff47-879">adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-879">address:</span></span> <br><span data-ttu-id="fff47-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="fff47-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="fff47-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="fff47-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="fff47-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="fff47-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="fff47-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="fff47-884">Autre (aucun Hello ci-dessus)</span><span class="sxs-lookup"><span data-stu-id="fff47-884">Other (none of hello above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="fff47-885">
        <font size=2> Protocole : generic-asset</span><span class="sxs-lookup"><span data-stu-id="fff47-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="fff47-886">Adresse :</span><span class="sxs-lookup"><span data-stu-id="fff47-886">Address:</span></span> <br><span data-ttu-id="fff47-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="fff47-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
