---
title: "aaaTransactions dans l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils relatifs à l’implémentation de transactions dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="2e57a-103">Transactions dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2e57a-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="2e57a-104">Comme pour tout, l’entrepôt de données SQL prend en charge les transactions dans le cadre de la charge de travail entrepôt de données hello.</span><span class="sxs-lookup"><span data-stu-id="2e57a-104">As you would expect, SQL Data Warehouse supports transactions as part of hello data warehouse workload.</span></span> <span data-ttu-id="2e57a-105">Cependant, performances de hello tooensure d’entrepôt de données SQL sont conservées à l’échelle de que certaines fonctionnalités sont limitées quand comparé tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e57a-105">However, tooensure hello performance of SQL Data Warehouse is maintained at scale some features are limited when compared tooSQL Server.</span></span> <span data-ttu-id="2e57a-106">Cet article met en évidence les différences de hello et listes hello d’autres.</span><span class="sxs-lookup"><span data-stu-id="2e57a-106">This article highlights hello differences and lists hello others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="2e57a-107">Niveaux d’isolation des transactions</span><span class="sxs-lookup"><span data-stu-id="2e57a-107">Transaction isolation levels</span></span>
<span data-ttu-id="2e57a-108">SQL Data Warehouse implémente les transactions ACID.</span><span class="sxs-lookup"><span data-stu-id="2e57a-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="2e57a-109">Toutefois, hello d’Isolation de la prise en charge transactionnelle de hello est limité trop`READ UNCOMMITTED` et il ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="2e57a-109">However, hello Isolation of hello transactional support is limited too`READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="2e57a-110">Vous pouvez implémenter un nombre de méthodes de codage tooprevent dirty lit des données s’il s’agit d’un critère important pour vous.</span><span class="sxs-lookup"><span data-stu-id="2e57a-110">You can implement a number of coding methods tooprevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="2e57a-111">Hello méthodes les plus populaires exploitent SACT et le basculement de partition table (souvent appelé modèle de fenêtre glissante de hello) tooprevent les utilisateurs à partir de l’interrogation des données qui sont toujours en cours de préparation.</span><span class="sxs-lookup"><span data-stu-id="2e57a-111">hello most popular methods leverage both CTAS and table partition switching (often known as hello sliding window pattern) tooprevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="2e57a-112">Affichages que les données de filtre préliminaire hello sont également une approche courante.</span><span class="sxs-lookup"><span data-stu-id="2e57a-112">Views that pre-filter hello data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="2e57a-113">Taille de la transaction</span><span class="sxs-lookup"><span data-stu-id="2e57a-113">Transaction size</span></span>
<span data-ttu-id="2e57a-114">Une transaction de modification de données unique est limitée en taille.</span><span class="sxs-lookup"><span data-stu-id="2e57a-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="2e57a-115">limite de Hello aujourd'hui est appliqué « par distribution ».</span><span class="sxs-lookup"><span data-stu-id="2e57a-115">hello limit today is applied "per distribution".</span></span> <span data-ttu-id="2e57a-116">Par conséquent, l’allocation totale hello peut être calculée en multipliant la limite de hello par nombre de distribution hello.</span><span class="sxs-lookup"><span data-stu-id="2e57a-116">Therefore, hello total allocation can be calculated by multiplying hello limit by hello distribution count.</span></span> <span data-ttu-id="2e57a-117">tooapproximate hello nombre de lignes dans une transaction de hello division cap de distribution hello par taille totale de hello de chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="2e57a-117">tooapproximate hello maximum number of rows in hello transaction divide hello distribution cap by hello total size of each row.</span></span> <span data-ttu-id="2e57a-118">Pour les colonnes de longueur variable envisagez prendre une longueur de colonne moyenne au lieu d’utiliser la taille maximale de hello.</span><span class="sxs-lookup"><span data-stu-id="2e57a-118">For variable length columns consider taking an average column length rather than using hello maximum size.</span></span>

<span data-ttu-id="2e57a-119">Dans la table hello ci-dessous hello les hypothèses suivantes ont été apportées :</span><span class="sxs-lookup"><span data-stu-id="2e57a-119">In hello table below hello following assumptions have been made:</span></span>

* <span data-ttu-id="2e57a-120">Une distribution égale des données s’est produite</span><span class="sxs-lookup"><span data-stu-id="2e57a-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="2e57a-121">longueur de ligne moyenne Hello est 250 octets</span><span class="sxs-lookup"><span data-stu-id="2e57a-121">hello average row length is 250 bytes</span></span>

| <span data-ttu-id="2e57a-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="2e57a-122">[DWU][DWU]</span></span> | <span data-ttu-id="2e57a-123">Limite par distribution (Go)</span><span class="sxs-lookup"><span data-stu-id="2e57a-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="2e57a-124">Nombre de distributions</span><span class="sxs-lookup"><span data-stu-id="2e57a-124">Number of Distributions</span></span> | <span data-ttu-id="2e57a-125">Taille de transaction MAX (Go)</span><span class="sxs-lookup"><span data-stu-id="2e57a-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="2e57a-126"># Lignes par distribution</span><span class="sxs-lookup"><span data-stu-id="2e57a-126"># Rows per distribution</span></span> | <span data-ttu-id="2e57a-127">Nombre de lignes max par transaction</span><span class="sxs-lookup"><span data-stu-id="2e57a-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2e57a-128">DW100</span><span class="sxs-lookup"><span data-stu-id="2e57a-128">DW100</span></span> |<span data-ttu-id="2e57a-129">1</span><span class="sxs-lookup"><span data-stu-id="2e57a-129">1</span></span> |<span data-ttu-id="2e57a-130">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-130">60</span></span> |<span data-ttu-id="2e57a-131">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-131">60</span></span> |<span data-ttu-id="2e57a-132">4 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-132">4,000,000</span></span> |<span data-ttu-id="2e57a-133">240 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-133">240,000,000</span></span> |
| <span data-ttu-id="2e57a-134">DW200</span><span class="sxs-lookup"><span data-stu-id="2e57a-134">DW200</span></span> |<span data-ttu-id="2e57a-135">1.5</span><span class="sxs-lookup"><span data-stu-id="2e57a-135">1.5</span></span> |<span data-ttu-id="2e57a-136">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-136">60</span></span> |<span data-ttu-id="2e57a-137">90</span><span class="sxs-lookup"><span data-stu-id="2e57a-137">90</span></span> |<span data-ttu-id="2e57a-138">6 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-138">6,000,000</span></span> |<span data-ttu-id="2e57a-139">360 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-139">360,000,000</span></span> |
| <span data-ttu-id="2e57a-140">DW300</span><span class="sxs-lookup"><span data-stu-id="2e57a-140">DW300</span></span> |<span data-ttu-id="2e57a-141">2.25</span><span class="sxs-lookup"><span data-stu-id="2e57a-141">2.25</span></span> |<span data-ttu-id="2e57a-142">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-142">60</span></span> |<span data-ttu-id="2e57a-143">135</span><span class="sxs-lookup"><span data-stu-id="2e57a-143">135</span></span> |<span data-ttu-id="2e57a-144">9 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-144">9,000,000</span></span> |<span data-ttu-id="2e57a-145">540 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-145">540,000,000</span></span> |
| <span data-ttu-id="2e57a-146">DW400</span><span class="sxs-lookup"><span data-stu-id="2e57a-146">DW400</span></span> |<span data-ttu-id="2e57a-147">3</span><span class="sxs-lookup"><span data-stu-id="2e57a-147">3</span></span> |<span data-ttu-id="2e57a-148">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-148">60</span></span> |<span data-ttu-id="2e57a-149">180</span><span class="sxs-lookup"><span data-stu-id="2e57a-149">180</span></span> |<span data-ttu-id="2e57a-150">12 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-150">12,000,000</span></span> |<span data-ttu-id="2e57a-151">720 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-151">720,000,000</span></span> |
| <span data-ttu-id="2e57a-152">DW500</span><span class="sxs-lookup"><span data-stu-id="2e57a-152">DW500</span></span> |<span data-ttu-id="2e57a-153">3,75</span><span class="sxs-lookup"><span data-stu-id="2e57a-153">3.75</span></span> |<span data-ttu-id="2e57a-154">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-154">60</span></span> |<span data-ttu-id="2e57a-155">225</span><span class="sxs-lookup"><span data-stu-id="2e57a-155">225</span></span> |<span data-ttu-id="2e57a-156">15 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-156">15,000,000</span></span> |<span data-ttu-id="2e57a-157">900 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-157">900,000,000</span></span> |
| <span data-ttu-id="2e57a-158">DW600</span><span class="sxs-lookup"><span data-stu-id="2e57a-158">DW600</span></span> |<span data-ttu-id="2e57a-159">4.5</span><span class="sxs-lookup"><span data-stu-id="2e57a-159">4.5</span></span> |<span data-ttu-id="2e57a-160">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-160">60</span></span> |<span data-ttu-id="2e57a-161">270</span><span class="sxs-lookup"><span data-stu-id="2e57a-161">270</span></span> |<span data-ttu-id="2e57a-162">18 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-162">18,000,000</span></span> |<span data-ttu-id="2e57a-163">1 080 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-163">1,080,000,000</span></span> |
| <span data-ttu-id="2e57a-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="2e57a-164">DW1000</span></span> |<span data-ttu-id="2e57a-165">7.5</span><span class="sxs-lookup"><span data-stu-id="2e57a-165">7.5</span></span> |<span data-ttu-id="2e57a-166">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-166">60</span></span> |<span data-ttu-id="2e57a-167">450</span><span class="sxs-lookup"><span data-stu-id="2e57a-167">450</span></span> |<span data-ttu-id="2e57a-168">30 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-168">30,000,000</span></span> |<span data-ttu-id="2e57a-169">1 800 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-169">1,800,000,000</span></span> |
| <span data-ttu-id="2e57a-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="2e57a-170">DW1200</span></span> |<span data-ttu-id="2e57a-171">9</span><span class="sxs-lookup"><span data-stu-id="2e57a-171">9</span></span> |<span data-ttu-id="2e57a-172">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-172">60</span></span> |<span data-ttu-id="2e57a-173">540</span><span class="sxs-lookup"><span data-stu-id="2e57a-173">540</span></span> |<span data-ttu-id="2e57a-174">36 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-174">36,000,000</span></span> |<span data-ttu-id="2e57a-175">2 160 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-175">2,160,000,000</span></span> |
| <span data-ttu-id="2e57a-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="2e57a-176">DW1500</span></span> |<span data-ttu-id="2e57a-177">11,25</span><span class="sxs-lookup"><span data-stu-id="2e57a-177">11.25</span></span> |<span data-ttu-id="2e57a-178">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-178">60</span></span> |<span data-ttu-id="2e57a-179">675</span><span class="sxs-lookup"><span data-stu-id="2e57a-179">675</span></span> |<span data-ttu-id="2e57a-180">45 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-180">45,000,000</span></span> |<span data-ttu-id="2e57a-181">2 700 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-181">2,700,000,000</span></span> |
| <span data-ttu-id="2e57a-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="2e57a-182">DW2000</span></span> |<span data-ttu-id="2e57a-183">15</span><span class="sxs-lookup"><span data-stu-id="2e57a-183">15</span></span> |<span data-ttu-id="2e57a-184">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-184">60</span></span> |<span data-ttu-id="2e57a-185">900</span><span class="sxs-lookup"><span data-stu-id="2e57a-185">900</span></span> |<span data-ttu-id="2e57a-186">60 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-186">60,000,000</span></span> |<span data-ttu-id="2e57a-187">3 600 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-187">3,600,000,000</span></span> |
| <span data-ttu-id="2e57a-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="2e57a-188">DW3000</span></span> |<span data-ttu-id="2e57a-189">22,5</span><span class="sxs-lookup"><span data-stu-id="2e57a-189">22.5</span></span> |<span data-ttu-id="2e57a-190">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-190">60</span></span> |<span data-ttu-id="2e57a-191">1 350</span><span class="sxs-lookup"><span data-stu-id="2e57a-191">1,350</span></span> |<span data-ttu-id="2e57a-192">90 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-192">90,000,000</span></span> |<span data-ttu-id="2e57a-193">5 400 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-193">5,400,000,000</span></span> |
| <span data-ttu-id="2e57a-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="2e57a-194">DW6000</span></span> |<span data-ttu-id="2e57a-195">45</span><span class="sxs-lookup"><span data-stu-id="2e57a-195">45</span></span> |<span data-ttu-id="2e57a-196">60</span><span class="sxs-lookup"><span data-stu-id="2e57a-196">60</span></span> |<span data-ttu-id="2e57a-197">2 700</span><span class="sxs-lookup"><span data-stu-id="2e57a-197">2,700</span></span> |<span data-ttu-id="2e57a-198">180 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-198">180,000,000</span></span> |<span data-ttu-id="2e57a-199">10 800 000 000</span><span class="sxs-lookup"><span data-stu-id="2e57a-199">10,800,000,000</span></span> |

<span data-ttu-id="2e57a-200">limite de taille de transaction Hello est appliquée par la transaction ou l’opération.</span><span class="sxs-lookup"><span data-stu-id="2e57a-200">hello transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="2e57a-201">Elle n’est pas appliquée à toutes les transactions simultanées.</span><span class="sxs-lookup"><span data-stu-id="2e57a-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="2e57a-202">Par conséquent, chaque transaction est autorisée toowrite cette quantité de données toohello journal.</span><span class="sxs-lookup"><span data-stu-id="2e57a-202">Therefore each transaction is permitted toowrite this amount of data toohello log.</span></span> 

<span data-ttu-id="2e57a-203">toooptimize et réduire les données écrites toohello journal hello reportez-vous toohello [Transactions meilleures pratiques] [ Transactions best practices] l’article.</span><span class="sxs-lookup"><span data-stu-id="2e57a-203">toooptimize and minimize hello amount of data written toohello log please refer toohello [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="2e57a-204">Hello maximale de taille de la transaction ne peut être obtenue pour le hachage ou de tables ROUND_ROBIN distribués où hello propager de bienvenue des données est la même.</span><span class="sxs-lookup"><span data-stu-id="2e57a-204">hello maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where hello spread of hello data is even.</span></span> <span data-ttu-id="2e57a-205">Si la transaction de hello écrit les données de manière asymétrique toohello distributions, hello limite est probablement toobe atteint taille de transaction maximal toohello préalable.</span><span class="sxs-lookup"><span data-stu-id="2e57a-205">If hello transaction is writing data in a skewed fashion toohello distributions then hello limit is likely toobe reached prior toohello maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="2e57a-206">État des transactions</span><span class="sxs-lookup"><span data-stu-id="2e57a-206">Transaction state</span></span>
<span data-ttu-id="2e57a-207">SQL Data Warehouse utilise hello XACT_STATE() fonction tooreport Échec d’une transaction à l’aide de la valeur de hello -2.</span><span class="sxs-lookup"><span data-stu-id="2e57a-207">SQL Data Warehouse uses hello XACT_STATE() function tooreport a failed transaction using hello value -2.</span></span> <span data-ttu-id="2e57a-208">Cela signifie que les transactions hello a échoué et sont marquée pour la restauration uniquement</span><span class="sxs-lookup"><span data-stu-id="2e57a-208">This means that hello transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="2e57a-209">l’utilisation de -2 Hello par hello XACT_STATE fonction toodenote un ordinateur Échec de la transaction représente un comportement différent tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e57a-209">hello use of -2 by hello XACT_STATE function toodenote a failed transaction represents different behavior tooSQL Server.</span></span> <span data-ttu-id="2e57a-210">SQL Server utilise la valeur -1 de hello toorepresent une transaction non validable.</span><span class="sxs-lookup"><span data-stu-id="2e57a-210">SQL Server uses hello value -1 toorepresent an un-committable transaction.</span></span> <span data-ttu-id="2e57a-211">SQL Server peut tolérer des erreurs à l’intérieur d’une transaction sans qu’il ait toobe marqué comme non validable.</span><span class="sxs-lookup"><span data-stu-id="2e57a-211">SQL Server can tolerate some errors inside a transaction without it having toobe marked as un-committable.</span></span> <span data-ttu-id="2e57a-212">Par exemple, la valeur `SELECT 1/0` entraîne une erreur, mais ne fait pas passer une transaction à l’état non validable.</span><span class="sxs-lookup"><span data-stu-id="2e57a-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="2e57a-213">SQL Server permet également de lectures de transaction non validable de hello.</span><span class="sxs-lookup"><span data-stu-id="2e57a-213">SQL Server also permits reads in hello un-committable transaction.</span></span> <span data-ttu-id="2e57a-214">Mais SQL Data Warehouse ne vous le permet pas.</span><span class="sxs-lookup"><span data-stu-id="2e57a-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="2e57a-215">Si une erreur se produit à l’intérieur d’une transaction de l’entrepôt de données SQL, il insère automatiquement les état hello -2, et vous ne serez pas en mesure de toomake les autres instructions select jusqu'à ce que l’instruction de hello a été annulée.</span><span class="sxs-lookup"><span data-stu-id="2e57a-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter hello -2 state and you will not be able toomake any further select statements until hello statement has been rolled back.</span></span> <span data-ttu-id="2e57a-216">Il est donc important toocheck que votre toosee de code d’application si elle utilise XACT_STATE() comme vous pouvez être amené à toomake de modifications de code.</span><span class="sxs-lookup"><span data-stu-id="2e57a-216">It is therefore important toocheck that your application code toosee if it uses  XACT_STATE() as you may need toomake code modifications.</span></span>
> 
> 

<span data-ttu-id="2e57a-217">Dans SQL Server par exemple, vous pouvez voir une transaction ressemblant à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="2e57a-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="2e57a-218">Si vous laissez votre code, car il est au-dessus de vous obtiendrez hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="2e57a-218">If you leave your code as it is above then you will get hello following error message:</span></span>

<span data-ttu-id="2e57a-219">Msg 111233, niveau 16, état 1, ligne 1 111233 ; hello en cours a été annulée, et les modifications en attente ont été restaurées.</span><span class="sxs-lookup"><span data-stu-id="2e57a-219">Msg 111233, Level 16, State 1, Line 1 111233;hello current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="2e57a-220">Cause : une transaction à un état de restauration uniquement n’a été pas explicitement restaurée avant une instruction DDL, DML ou SELECT.</span><span class="sxs-lookup"><span data-stu-id="2e57a-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="2e57a-221">Vous obtiendrez également pas les résultats de hello de hello erreur_ * fonctions.</span><span class="sxs-lookup"><span data-stu-id="2e57a-221">You will also not get hello output of hello ERROR_* functions.</span></span>

<span data-ttu-id="2e57a-222">Dans l’entrepôt de données SQL, code de hello doit toobe légèrement modifié :</span><span class="sxs-lookup"><span data-stu-id="2e57a-222">In SQL Data Warehouse hello code needs toobe slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="2e57a-223">Hello attendu comportement est désormais prise en charge.</span><span class="sxs-lookup"><span data-stu-id="2e57a-223">hello expected behavior is now observed.</span></span> <span data-ttu-id="2e57a-224">erreur Hello dans les transactions hello est géré et hello erreur_ * fonctions fournissent des valeurs comme prévu.</span><span class="sxs-lookup"><span data-stu-id="2e57a-224">hello error in hello transaction is managed and hello ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="2e57a-225">Tout ce qui a changé est que hello `ROLLBACK` Hello transaction avait toohappen avant hello lire des informations d’erreur hello Bonjour `CATCH` bloc.</span><span class="sxs-lookup"><span data-stu-id="2e57a-225">All that has changed is that hello `ROLLBACK` of hello transaction had toohappen before hello read of hello error information in hello `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="2e57a-226">Fonction Error_Line()</span><span class="sxs-lookup"><span data-stu-id="2e57a-226">Error_Line() function</span></span>
<span data-ttu-id="2e57a-227">Il est également important de noter que SQL Data Warehouse ne pas implémenter ou prend en charge la fonction ERROR_LINE() hello.</span><span class="sxs-lookup"><span data-stu-id="2e57a-227">It is also worth noting that SQL Data Warehouse does not implement or support hello ERROR_LINE() function.</span></span> <span data-ttu-id="2e57a-228">Si vous avez cela dans votre code, vous devez tooremove il toobe compatible avec l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="2e57a-228">If you have this in your code you will need tooremove it toobe compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="2e57a-229">Utilisez à la place des étiquettes de requête dans votre code à tooimplement des fonctionnalités équivalentes.</span><span class="sxs-lookup"><span data-stu-id="2e57a-229">Use query labels in your code instead tooimplement equivalent functionality.</span></span> <span data-ttu-id="2e57a-230">Reportez-vous toohello [étiquette] [ LABEL] article pour plus d’informations sur cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2e57a-230">Please refer toohello [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="2e57a-231">Utilisation des paramètres THROW et RAISERROR</span><span class="sxs-lookup"><span data-stu-id="2e57a-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="2e57a-232">THROW est hello implémentation plus moderne pour le déclenchement d’exceptions dans l’entrepôt de données SQL mais RAISERROR est également.</span><span class="sxs-lookup"><span data-stu-id="2e57a-232">THROW is hello more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="2e57a-233">Il existe quelques différences qui méritent notre attention toohowever.</span><span class="sxs-lookup"><span data-stu-id="2e57a-233">There are a few differences that are worth paying attention toohowever.</span></span>

* <span data-ttu-id="2e57a-234">Messages d’erreur ne doit pas être Bonjour plage de 100 000 à 150 000 pour THROW défini par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2e57a-234">User defined error messages numbers cannot be in hello 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="2e57a-235">Les messages d’erreurs associés au paramètre RAISERROR sont définis sur la valeur fixe de 50 000.</span><span class="sxs-lookup"><span data-stu-id="2e57a-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="2e57a-236">L’utilisation de l’élément sys.messages n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="2e57a-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="2e57a-237">Limitations</span><span class="sxs-lookup"><span data-stu-id="2e57a-237">Limitiations</span></span>
<span data-ttu-id="2e57a-238">SQL Data Warehouse a quelques autres restrictions qui se rapportent tootransactions.</span><span class="sxs-lookup"><span data-stu-id="2e57a-238">SQL Data Warehouse does have a few other restrictions that relate tootransactions.</span></span>

<span data-ttu-id="2e57a-239">Les voici :</span><span class="sxs-lookup"><span data-stu-id="2e57a-239">They are as follows:</span></span>

* <span data-ttu-id="2e57a-240">Les transactions distribuées ne sont pas acceptées.</span><span class="sxs-lookup"><span data-stu-id="2e57a-240">No distributed transactions</span></span>
* <span data-ttu-id="2e57a-241">Les transactions imbriquées ne sont pas autorisées.</span><span class="sxs-lookup"><span data-stu-id="2e57a-241">No nested transactions permitted</span></span>
* <span data-ttu-id="2e57a-242">Les points de sauvegarde ne sont pas acceptés.</span><span class="sxs-lookup"><span data-stu-id="2e57a-242">No save points allowed</span></span>
* <span data-ttu-id="2e57a-243">Transactions sans nom</span><span class="sxs-lookup"><span data-stu-id="2e57a-243">No named transactions</span></span>
* <span data-ttu-id="2e57a-244">Transactions sans marquage</span><span class="sxs-lookup"><span data-stu-id="2e57a-244">No marked transactions</span></span>
* <span data-ttu-id="2e57a-245">Aucune prise en charge de DDL comme `CREATE TABLE` dans une transaction définie par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2e57a-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e57a-246">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e57a-246">Next steps</span></span>
<span data-ttu-id="2e57a-247">toolearn plus sur l’optimisation des transactions, consultez [Transactions meilleures pratiques][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="2e57a-247">toolearn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="2e57a-248">toolearn sur les autres pratiques recommandées SQL Data Warehouse, consultez [SQL Data Warehouse meilleures pratiques][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="2e57a-248">toolearn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
