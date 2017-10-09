---
title: "aaaCreate et gérer des tâches élastiques à l’aide de PowerShell | Documents Microsoft"
description: "PowerShell utilisé toomanage les pools de base de données SQL Azure"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="babe8-103">Création et gestion de tâches de bases de données SQL élastiques à l’aide de PowerShell (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="babe8-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="babe8-104">Hello PowerShell APIs pour **des travaux de base de données élastique** (en version préliminaire) vous permettent de définir un groupe de bases de données par rapport à laquelle les scripts sont exécutés.</span><span class="sxs-lookup"><span data-stu-id="babe8-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="babe8-105">Cet article explique comment toocreate et gérer **des travaux de base de données élastique** à l’aide des applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="babe8-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="babe8-106">Voir [Vue d’ensemble des tâches de base de données élastiques](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="babe8-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="babe8-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="babe8-107">Prerequisites</span></span>
* <span data-ttu-id="babe8-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="babe8-108">An Azure subscription.</span></span> <span data-ttu-id="babe8-109">Pour obtenir un essai gratuit, voir [Version d'évaluation d'un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="babe8-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="babe8-110">Un ensemble de bases de données créées avec les outils de base de données élastique hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="babe8-111">Voir [Prise en main des outils de base de données élastiques](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="babe8-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="babe8-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="babe8-112">Azure PowerShell.</span></span> <span data-ttu-id="babe8-113">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="babe8-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="babe8-114">**tâches de bases de données élastiques** : voir [Installing tâches de bases de données élastiques](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="babe8-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="babe8-115">Sélectionner votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="babe8-115">Select your Azure subscription</span></span>
<span data-ttu-id="babe8-116">abonnement de hello tooselect vous avez besoin de votre Id d’abonnement (**- SubscriptionId**) ou le nom de l’abonnement (**- SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="babe8-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="babe8-117">Si vous avez plusieurs abonnements, vous pouvez exécuter hello **Get-AzureRmSubscription** hello applet de commande et copie souhaité des informations d’abonnement à partir du jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="babe8-118">Une fois vos informations d’abonnement, exécutez hello suivant l’applet de commande tooset cet abonnement comme valeur par défaut de hello, à savoir hello cible pour la création et la gestion des travaux :</span><span class="sxs-lookup"><span data-stu-id="babe8-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="babe8-119">Hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) est recommandée pour l’utilisation toodevelop et exécuter des scripts PowerShell sur des tâches de base de données élastique hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="babe8-120">Objets des tâches de bases de données élastiques</span><span class="sxs-lookup"><span data-stu-id="babe8-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="babe8-121">Hello après le tableau répertorie tous les types d’objet hello de **des travaux de base de données élastique** , ainsi que sa description et ses APIs PowerShell correspondantes.</span><span class="sxs-lookup"><span data-stu-id="babe8-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="babe8-122">Type d'objet</span><span class="sxs-lookup"><span data-stu-id="babe8-122">Object Type</span></span></th>
    <th><span data-ttu-id="babe8-123">Description</span><span class="sxs-lookup"><span data-stu-id="babe8-123">Description</span></span></th>
    <th><span data-ttu-id="babe8-124">API PowerShell correspondantes</span><span class="sxs-lookup"><span data-stu-id="babe8-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="babe8-125">Informations d'identification</span><span class="sxs-lookup"><span data-stu-id="babe8-125">Credential</span></span></td>
    <td><span data-ttu-id="babe8-126">Nom d’utilisateur et mot de passe toouse lors de la connexion toodatabases pour l’exécution de scripts ou l’application de dacpac.</span><span class="sxs-lookup"><span data-stu-id="babe8-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="babe8-127">mot de passe Hello est chiffré avant d’envoyer tooand le stockage de base de données des travaux de base de données élastique hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="babe8-128">mot de passe Hello est déchiffrée par hello service élastique travaux de base de données via les informations d’identification hello créé et téléchargé à partir du script d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="babe8-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="babe8-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="babe8-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="babe8-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="babe8-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="babe8-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="babe8-132">Script</span><span class="sxs-lookup"><span data-stu-id="babe8-132">Script</span></span></td>
    <td><span data-ttu-id="babe8-133">Toobe de script Transact-SQL utilisée pour l’exécution entre bases de données.</span><span class="sxs-lookup"><span data-stu-id="babe8-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="babe8-134">script de Hello doit être créé toobe idempotent, car le service de hello va tenter de l’exécution du script hello lors de défaillances.</span><span class="sxs-lookup"><span data-stu-id="babe8-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="babe8-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="babe8-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="babe8-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="babe8-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="babe8-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="babe8-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="babe8-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="babe8-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="babe8-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="babe8-139">DACPAC</span></span></td>
    <td><span data-ttu-id="babe8-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Application de couche données </a> toobe appliquée sur des bases de données du package.</span><span class="sxs-lookup"><span data-stu-id="babe8-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="babe8-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="babe8-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="babe8-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="babe8-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="babe8-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="babe8-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="babe8-144">Base de données cible</span><span class="sxs-lookup"><span data-stu-id="babe8-144">Database Target</span></span></td>
    <td><span data-ttu-id="babe8-145">Base de données et serveur nom pointage tooan base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="babe8-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="babe8-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="babe8-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="babe8-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="babe8-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="babe8-148">Carte de partitions cible</span><span class="sxs-lookup"><span data-stu-id="babe8-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="babe8-149">Combinaison d’une cible de la base de données et un toobe d’informations d’identification utilisée toodetermine les informations stockées dans une carte de partitions de base de données élastique.</span><span class="sxs-lookup"><span data-stu-id="babe8-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="babe8-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="babe8-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="babe8-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="babe8-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="babe8-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="babe8-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="babe8-153">Cible de la collection personnalisée</span><span class="sxs-lookup"><span data-stu-id="babe8-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="babe8-154">Un groupe défini de bases de données toocollectively utiliser pour l’exécution.</span><span class="sxs-lookup"><span data-stu-id="babe8-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="babe8-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="babe8-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="babe8-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="babe8-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="babe8-157">Cible enfant de la collection personnalisée</span><span class="sxs-lookup"><span data-stu-id="babe8-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="babe8-158">Cible de la base de données qui est référencée à partir d'une collection personnalisée.</span><span class="sxs-lookup"><span data-stu-id="babe8-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="babe8-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="babe8-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="babe8-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="babe8-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="babe8-161">Travail</span><span class="sxs-lookup"><span data-stu-id="babe8-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="babe8-162">Définition des paramètres d’une tâche qui peut être utilisé tootrigger exécution ou toofulfill une planification.</span><span class="sxs-lookup"><span data-stu-id="babe8-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="babe8-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="babe8-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="babe8-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="babe8-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="babe8-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="babe8-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="babe8-166">Exécution des tâches</span><span class="sxs-lookup"><span data-stu-id="babe8-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="babe8-167">Conteneur de toofulfill nécessaire de tâches soit exécuter un script ou de l’application d’une cible de tooa DACPAC à l’aide des informations d’identification pour les connexions de base de données avec des erreurs gérées dans la stratégie d’exécution tooan conformément.</span><span class="sxs-lookup"><span data-stu-id="babe8-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="babe8-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="babe8-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="babe8-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="babe8-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="babe8-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="babe8-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="babe8-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="babe8-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="babe8-172">Exécution d’une tâche</span><span class="sxs-lookup"><span data-stu-id="babe8-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="babe8-173">Unité de travail toofulfill un travail.</span><span class="sxs-lookup"><span data-stu-id="babe8-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="babe8-174">Si une tâche n’est pas en mesure de toosuccessfully exécuter, message d’exception résultant hello est consignée et une nouvelle tâche de travail correspondant est créée et exécutée dans toohello conformément spécifié stratégie d’exécution.</span><span class="sxs-lookup"><span data-stu-id="babe8-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="babe8-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="babe8-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="babe8-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="babe8-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="babe8-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="babe8-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="babe8-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="babe8-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="babe8-179">Stratégie d’exécution des tâches</span><span class="sxs-lookup"><span data-stu-id="babe8-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="babe8-180">Contrôle les délais d’expiration d’une tâche, les limites du nombre de tentatives et les intervalles entre les tentatives.</span><span class="sxs-lookup"><span data-stu-id="babe8-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="babe8-181">Les tâches de bases de données incluent une stratégie d’exécution de tâche par défaut qui entraîne essentiellement un nombre infini de nouvelles tentatives de défaillances de tâches avec une interruption exponentielle des intervalles entre chaque tentative.</span><span class="sxs-lookup"><span data-stu-id="babe8-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="babe8-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="babe8-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="babe8-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="babe8-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="babe8-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="babe8-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="babe8-185">Planification</span><span class="sxs-lookup"><span data-stu-id="babe8-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="babe8-186">Heure de base relatives à la place de tootake d’exécution sur un intervalle de récurrent ou à une seule fois.</span><span class="sxs-lookup"><span data-stu-id="babe8-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="babe8-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="babe8-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="babe8-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="babe8-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="babe8-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="babe8-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="babe8-190">Déclencheur de tâches</span><span class="sxs-lookup"><span data-stu-id="babe8-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="babe8-191">Un mappage entre une tâche et une planification tootrigger l’exécution du travail en fonction de la planification de toohello.</span><span class="sxs-lookup"><span data-stu-id="babe8-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="babe8-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="babe8-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="babe8-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="babe8-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="babe8-194">Types de groupe des tâches de bases de données élastiques prises en charge</span><span class="sxs-lookup"><span data-stu-id="babe8-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="babe8-195">Hello s’exécute des scripts Transact-SQL (T-SQL) ou l’application de dacpac sur un groupe de bases de données.</span><span class="sxs-lookup"><span data-stu-id="babe8-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="babe8-196">Lorsqu’une tâche est soumis toobe exécutée dans un groupe de bases de données, les travaux hello » développe « hello en tâches enfants effectuent hello où chacun a demandé l’exécution par rapport à une base de données dans le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="babe8-197">Vous pouvez créer deux types de groupes :</span><span class="sxs-lookup"><span data-stu-id="babe8-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="babe8-198">[Carte de partitions](sql-database-elastic-scale-shard-map-management.md) groupe : lorsqu’une tâche est soumis tootarget une carte de partitions, les travaux hello interroge toodetermine de carte de partitions hello son ensemble de partitions et qu’il crée ensuite des travaux pour chaque partition enfant dans la carte de partitions hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="babe8-199">Groupe Collection personnalisée : un ensemble défini de bases de données personnalisées.</span><span class="sxs-lookup"><span data-stu-id="babe8-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="babe8-200">Lorsqu’un projet cible une collection personnalisée, il crée enfant travaux pour chaque base de données actuellement dans un regroupement personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="babe8-201">tooset hello connexion des travaux de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="babe8-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="babe8-202">Une connexion a besoin de définir des travaux de toohello toobe *base de données de contrôle* toousing préalable hello travaux API.</span><span class="sxs-lookup"><span data-stu-id="babe8-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="babe8-203">Cette applet de commande en cours d’exécution déclenche un toopop de la fenêtre d’informations d’identification de la demande de nom d’utilisateur hello et le mot de passe créé lors de l’installation des travaux de base de données élastique.</span><span class="sxs-lookup"><span data-stu-id="babe8-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="babe8-204">Tous les exemples fournis dans cette rubrique partent du principe que cette première étape a déjà été effectuée.</span><span class="sxs-lookup"><span data-stu-id="babe8-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="babe8-205">Ouvrir une base de données élastique toohello connexion :</span><span class="sxs-lookup"><span data-stu-id="babe8-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="babe8-206">Informations d’identification chiffrées dans les travaux de base de données élastique hello</span><span class="sxs-lookup"><span data-stu-id="babe8-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="babe8-207">Informations d’identification de la base de données peuvent être insérées dans les travaux de hello *base de données contrôle* avec son mot de passe chiffré.</span><span class="sxs-lookup"><span data-stu-id="babe8-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="babe8-208">Il est nécessaire de toostore informations d’identification tooenable travaux toobe exécutée ultérieurement, (à l’aide de planifications de travaux).</span><span class="sxs-lookup"><span data-stu-id="babe8-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="babe8-209">Le chiffrement fonctionne via un certificat créé dans le cadre du script d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="babe8-210">script d’installation Hello crée et téléchargements hello certificat hello Azure Cloud Service pour le déchiffrement de hello stockée mots de passe chiffrés.</span><span class="sxs-lookup"><span data-stu-id="babe8-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="babe8-211">Bonjour Azure Cloud Service ultérieurement stocke la clé publique de hello dans les travaux de hello *base de données contrôle* qui permet l’interface de PowerShell API ou le portail classique Azure hello tooencrypt un mot de passe fourni sans nécessiter le certificat de hello toobe installé localement.</span><span class="sxs-lookup"><span data-stu-id="babe8-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="babe8-212">les mots de passe Hello d’informations d’identification sont chiffrées et sécurisée des utilisateurs avec accès en lecture seule tooElastic de base de données travaux des objets.</span><span class="sxs-lookup"><span data-stu-id="babe8-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="babe8-213">Mais il est possible pour un utilisateur malveillant avec accès en lecture-écriture tooElastic travaux de base de données objets tooextract un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="babe8-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="babe8-214">Informations d’identification sont conçu toobe réutilisée dans les exécutions de travaux.</span><span class="sxs-lookup"><span data-stu-id="babe8-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="babe8-215">Informations d’identification sont passées des bases de données tootarget lors de l’établissement de connexions.</span><span class="sxs-lookup"><span data-stu-id="babe8-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="babe8-216">Il n’existe actuellement aucune restriction sur les bases de données cibles hello utilisés pour chaque information d’identification, l’utilisateur malveillant pourrait ajouter une cible de la base de données pour une base de données sous contrôle de l’utilisateur malveillant hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="babe8-217">utilisateur de Hello par la suite a pu démarrer un travail de ciblage de mot de passe de cette base de données toogain hello informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="babe8-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="babe8-218">Voici quelques bonnes pratiques de sécurité pour les tâches de bases de données élastiques :</span><span class="sxs-lookup"><span data-stu-id="babe8-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="babe8-219">Limiter l’utilisation de personnes de tootrusted API hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="babe8-220">Informations d’identification doivent avoir hello moins tâche hello tooperform nécessaire des privilèges.</span><span class="sxs-lookup"><span data-stu-id="babe8-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="babe8-221">Pour plus d’informations, consultez l’article MSDN [Autorisations](https://msdn.microsoft.com/library/bb669084.aspx) sur SQL Server.</span><span class="sxs-lookup"><span data-stu-id="babe8-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="babe8-222">toocreate informations d’identification chiffrées pour l’exécution du travail entre les bases de données</span><span class="sxs-lookup"><span data-stu-id="babe8-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="babe8-223">toocreate une nouvelle chiffrée des informations d’identification, hello [ **applet de commande Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) vous invite à spécifier un nom d’utilisateur et un mot de passe qui peut être passée toohello [ **AzureSqlJobCredential de nouveau applet de commande**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="babe8-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="babe8-224">informations d’identification tooupdate</span><span class="sxs-lookup"><span data-stu-id="babe8-224">tooupdate credentials</span></span>
<span data-ttu-id="babe8-225">Lors de la modification de mots de passe, utilisez hello [ **applet de commande Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) et ensemble hello **CredentialName** paramètre.</span><span class="sxs-lookup"><span data-stu-id="babe8-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="babe8-226">toodefine une cible de carte de partitions de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="babe8-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="babe8-227">tooexecute une tâche sur toutes les bases de données dans un ensemble de partitions (créé à l’aide de [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md)), utilisez une carte de partitions en tant que cible de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="babe8-228">Cet exemple requiert une application partitionnée créée à l’aide de la bibliothèque cliente de base de données élastique hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="babe8-229">Voir [Prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="babe8-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="babe8-230">base de données du gestionnaire Hello partition carte doit être défini en tant que base de données cible et puis carte de partitions spécifiques de hello doit être spécifié en tant que cible.</span><span class="sxs-lookup"><span data-stu-id="babe8-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="babe8-231">Créez un script T-SQL pour l’exécuter sur des bases de données</span><span class="sxs-lookup"><span data-stu-id="babe8-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="babe8-232">Lorsque vous créez des scripts T-SQL pour l’exécution, il est vivement recommandé de toobuild les toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) et résilientes contre les défaillances.</span><span class="sxs-lookup"><span data-stu-id="babe8-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="babe8-233">Les travaux de base de données élastiques effectuera une nouvelle tentative d’exécution d’un script chaque fois que l’exécution rencontre une défaillance, quelle que soit la classification hello de défaillance de hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="babe8-234">Hello d’utilisation [ **applet de commande New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate et enregistrer un script pour l’exécution et définir hello **- ContentName** et **- CommandText**paramètres.</span><span class="sxs-lookup"><span data-stu-id="babe8-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="babe8-235">Créer un script à partir d'un fichier</span><span class="sxs-lookup"><span data-stu-id="babe8-235">Create a new script from a file</span></span>
<span data-ttu-id="babe8-236">Si hello script T-SQL est définie dans un fichier, utilisez ce script de hello tooimport :</span><span class="sxs-lookup"><span data-stu-id="babe8-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="babe8-237">script tooupdate T-SQL pour l’exécution entre bases de données</span><span class="sxs-lookup"><span data-stu-id="babe8-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="babe8-238">Cette mise à jour du script PowerShell hello texte de la commande T-SQL pour un script existant.</span><span class="sxs-lookup"><span data-stu-id="babe8-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="babe8-239">Hello ensemble définition toobe ensemble de variables tooreflect hello souhaité script suivant :</span><span class="sxs-lookup"><span data-stu-id="babe8-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="babe8-240">script de tooan de définition hello tooupdate existant</span><span class="sxs-lookup"><span data-stu-id="babe8-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="babe8-241">toocreate un tooexecute de travail un script sur une carte de partitions</span><span class="sxs-lookup"><span data-stu-id="babe8-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="babe8-242">Ce script PowerShell démarre une tâche pour l’exécution d’un script sur chaque partition dans la carte de partitions d’une infrastructure élastique.</span><span class="sxs-lookup"><span data-stu-id="babe8-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="babe8-243">Hello ensemble suivant hello tooreflect de variables souhaitée de script et la cible :</span><span class="sxs-lookup"><span data-stu-id="babe8-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="babe8-244">tooexecute un travail</span><span class="sxs-lookup"><span data-stu-id="babe8-244">tooexecute a job</span></span>
<span data-ttu-id="babe8-245">Ce script PowerShell exécute une tâche existante :</span><span class="sxs-lookup"><span data-stu-id="babe8-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="babe8-246">Mettre à jour hello suivant tooreflect variable hello souhaité travail nom toohave exécutée :</span><span class="sxs-lookup"><span data-stu-id="babe8-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="babe8-247">état de hello tooretrieve de l’exécution d’une tâche unique</span><span class="sxs-lookup"><span data-stu-id="babe8-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="babe8-248">Hello d’utilisation [ **applet de commande Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) et ensemble hello **JobExecutionId** état de hello tooview de paramètre de l’exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="babe8-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="babe8-249">Utilisez hello même **Get-AzureSqlJobExecution** applet de commande avec hello **IncludeChildren** état de hello tooview paramètre d’exécutions de travail enfant, hello à savoir un état spécifique pour chaque exécution du travail sur chaque base de données ciblée par le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="babe8-250">état de hello tooview sur plusieurs exécutions du travail</span><span class="sxs-lookup"><span data-stu-id="babe8-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="babe8-251">Hello [ **applet de commande Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) ayant plusieurs paramètres facultatifs qui peuvent être utilisé toodisplay plusieurs exécutions du travail, filtrées par le biais des paramètres de hello fourni.</span><span class="sxs-lookup"><span data-stu-id="babe8-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="babe8-252">suivant de Hello présente quelques-unes des façons possibles de hello toouse Get-AzureSqlJobExecution :</span><span class="sxs-lookup"><span data-stu-id="babe8-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="babe8-253">Récupérez toutes les exécutions de tâches de niveau supérieur actives :</span><span class="sxs-lookup"><span data-stu-id="babe8-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="babe8-254">Récupérez toutes les exécutions de tâches de niveau supérieur, y compris les exécutions de tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="babe8-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="babe8-255">Récupérez toutes les exécutions de tâches enfants d'un ID d'exécution de tâches fourni, y compris les exécutions de tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="babe8-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="babe8-256">Récupérez toutes les exécutions de tâches créées à l'aide d'une planification/combinaison de tâches, y compris les tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="babe8-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="babe8-257">Récupérez toutes les tâches ciblant une carte de partitions spécifiée, y compris les tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="babe8-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="babe8-258">Récupérez toutes les tâches ciblant une collecte personnalisée spécifiée, y compris les tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="babe8-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="babe8-259">Récupérer la liste de hello d’exécutions de tâches de travail au sein de l’exécution d’une tâche spécifique :</span><span class="sxs-lookup"><span data-stu-id="babe8-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="babe8-260">Récupérez les détails d’exécution de tâches de travail :</span><span class="sxs-lookup"><span data-stu-id="babe8-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="babe8-261">Hello PowerShell script suivant peut être utilisé tooview les détails de hello une tâche d’exécution des tâches, qui est particulièrement utile lors du débogage des erreurs d’exécution.</span><span class="sxs-lookup"><span data-stu-id="babe8-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="babe8-262">échecs de tooretrieve dans les exécutions de tâches de travail</span><span class="sxs-lookup"><span data-stu-id="babe8-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="babe8-263">Hello **JobTaskExecution objet** inclut une propriété pour hello du cycle de vie de la tâche hello avec une propriété de message.</span><span class="sxs-lookup"><span data-stu-id="babe8-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="babe8-264">Si une exécution de tâches de travail a échoué, propriété de cycle de vie hello sera définie trop*n’a pas pu* et propriété de message hello sera définie message d’exception résultant toohello et sa pile.</span><span class="sxs-lookup"><span data-stu-id="babe8-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="babe8-265">Si une tâche n’a pas réussi, il est important tooview les détails de hello des tâches de travail qui n’a pas réussi pour un travail donné.</span><span class="sxs-lookup"><span data-stu-id="babe8-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="babe8-266">toowait pour un toocomplete de l’exécution du travail</span><span class="sxs-lookup"><span data-stu-id="babe8-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="babe8-267">Hello PowerShell script suivant peut être utilisé toowait pour un toocomplete de tâche de travail :</span><span class="sxs-lookup"><span data-stu-id="babe8-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="babe8-268">Créez une stratégie d'exécution personnalisée</span><span class="sxs-lookup"><span data-stu-id="babe8-268">Create a custom execution policy</span></span>
<span data-ttu-id="babe8-269">Tâches de bases de données prend en charge la création de stratégies d'exécution personnalisées qui peuvent être appliquées lors du démarrage des tâches.</span><span class="sxs-lookup"><span data-stu-id="babe8-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="babe8-270">Les stratégies d'exécution permettent de définir :</span><span class="sxs-lookup"><span data-stu-id="babe8-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="babe8-271">Nom : L’identificateur de la stratégie d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="babe8-272">Délai d’attente de la tâche : délai avant l’annulation d’une tâche par Tâches de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="babe8-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="babe8-273">Intervalle de nouvelle tentative initial : Toowait d’intervalle avant la première nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="babe8-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="babe8-274">Intervalle maximal de tentatives : L’extrémité de toouse des intervalles de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="babe8-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="babe8-275">Coefficient d’interruption d’intervalle de nouvelle tentative : Coefficient utilisé toocalculate hello prochain intervalle entre les nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="babe8-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="babe8-276">Hello formule suivante est utilisée : (intervalle avant nouvelle tentative initiale) * Math.pow (intervalle interruption Coefficient (), (nombre de tentatives de) - 2).</span><span class="sxs-lookup"><span data-stu-id="babe8-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="babe8-277">Nombre maximal de tentatives : hello nombre maximal de tooperform de tentatives de nouvelle tentative au sein d’un travail.</span><span class="sxs-lookup"><span data-stu-id="babe8-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="babe8-278">stratégie d’exécution par défaut Hello utilise hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="babe8-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="babe8-279">Le nom : la stratégie d'exécution par défaut</span><span class="sxs-lookup"><span data-stu-id="babe8-279">Name: Default execution policy</span></span>
* <span data-ttu-id="babe8-280">Délai d’attente de la tâche : 1 semaine</span><span class="sxs-lookup"><span data-stu-id="babe8-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="babe8-281">Intervalle avant nouvelle tentative initiale : 100 millisecondes</span><span class="sxs-lookup"><span data-stu-id="babe8-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="babe8-282">Intervalle maximal avant nouvelle tentative : 30 minutes</span><span class="sxs-lookup"><span data-stu-id="babe8-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="babe8-283">Coefficient de l'intervalle avant nouvelle tentative : 2</span><span class="sxs-lookup"><span data-stu-id="babe8-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="babe8-284">Nombre maximal de tentatives : 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="babe8-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="babe8-285">Créer la stratégie d’exécution hello souhaité :</span><span class="sxs-lookup"><span data-stu-id="babe8-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="babe8-286">Mettez à jour une stratégie d'exécution personnalisée</span><span class="sxs-lookup"><span data-stu-id="babe8-286">Update a custom execution policy</span></span>
<span data-ttu-id="babe8-287">Hello de mise à jour souhaitée tooupdate de stratégie d’exécution :</span><span class="sxs-lookup"><span data-stu-id="babe8-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="babe8-288">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="babe8-288">Cancel a job</span></span>
<span data-ttu-id="babe8-289">La fonctionnalité Tâches de bases de données élastiques prend en charge les demandes d'annulation de tâches.</span><span class="sxs-lookup"><span data-stu-id="babe8-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="babe8-290">Si les travaux de base de données élastique détecte une demande d’annulation d’une tâche en cours d’exécution, il tentera de travail de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="babe8-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="babe8-291">La fonctionnalité Tâches de bases de données élastiques peut effectuer une annulation de deux manières différentes :</span><span class="sxs-lookup"><span data-stu-id="babe8-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="babe8-292">Annuler les tâches en cours d’exécution : si une annulation est détectée pendant une tâche est en cours d’exécution, l’annulation sera tentée dans hello aspect de la tâche hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="babe8-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="babe8-293">Par exemple : en l’absence d’une requête longue en cours d’exécution lorsqu’une annulation est tentée, il y aura une requête de hello toocancel tentative.</span><span class="sxs-lookup"><span data-stu-id="babe8-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="babe8-294">L’annulation de nouvelles tentatives de tâche : si une annulation est détectée par le thread de contrôle hello avant de lancer une tâche pour l’exécution, thread de contrôle hello éviter de lancer la tâche hello et déclarer la demande de hello comme annulée.</span><span class="sxs-lookup"><span data-stu-id="babe8-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="babe8-295">Si une annulation de tâche est demandée pour un travail parent, demande d’annulation hello sera respectée pour la tâche parente de hello et pour toutes ses tâches enfants.</span><span class="sxs-lookup"><span data-stu-id="babe8-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="babe8-296">toosubmit une demande d’annulation, utilisez hello [ **applet de commande Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) et ensemble hello **JobExecutionId** paramètre.</span><span class="sxs-lookup"><span data-stu-id="babe8-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="babe8-297">toodelete une tâche et l’historique des travaux en mode asynchrone</span><span class="sxs-lookup"><span data-stu-id="babe8-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="babe8-298">Tâches de bases de données élastiques prend en charge la suppression des tâches asynchrone.</span><span class="sxs-lookup"><span data-stu-id="babe8-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="babe8-299">Un travail peut être marqué pour suppression et hello système supprime le travail de hello et son historique une fois que toutes les exécutions de la tâche s’est terminé pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="babe8-300">système de Hello n’est pas automatiquement annulé exécutions de travail actif.</span><span class="sxs-lookup"><span data-stu-id="babe8-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="babe8-301">Appeler [ **Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel les exécutions de travail actif.</span><span class="sxs-lookup"><span data-stu-id="babe8-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="babe8-302">suppression du travail tootrigger, utilisez hello [ **applet de commande Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) et ensemble hello **JobName** paramètre.</span><span class="sxs-lookup"><span data-stu-id="babe8-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="babe8-303">toocreate une cible de la base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="babe8-303">toocreate a custom database target</span></span>
<span data-ttu-id="babe8-304">Vous pouvez définir des cibles de bases de données personnalisées pour une exécution directe ou pour une inclusion dans un groupe de bases de données personnalisées.</span><span class="sxs-lookup"><span data-stu-id="babe8-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="babe8-305">Par exemple, étant donné que **pools élastiques** sont pas encore directement pris en charge à l’aide de PowerShell APIs, vous pouvez créer une cible de la base de données personnalisée et la cible de collection de base de données personnalisée qui englobe toutes les bases de données hello dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="babe8-306">Définissez hello suit les informations de base de données de variables tooreflect hello souhaité :</span><span class="sxs-lookup"><span data-stu-id="babe8-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="babe8-307">toocreate une cible de collection de base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="babe8-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="babe8-308">Hello d’utilisation [ **New-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine de l’applet de commande de base de données personnalisée collection cible tooenable l’exécution d’une sur plusieurs cibles de base de données.</span><span class="sxs-lookup"><span data-stu-id="babe8-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="babe8-309">Après avoir créé un groupe de la base de données, les bases de données peuvent être associés à la cible de collection personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="babe8-310">Définissez hello variables tooreflect hello collection personnalisée souhaitée cible configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="babe8-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="babe8-311">cible de collecte des base de données personnalisée tooa tooadd bases de données</span><span class="sxs-lookup"><span data-stu-id="babe8-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="babe8-312">tooadd un regroupement personnalisé spécifique de base de données tooa utiliser hello [ **Add-AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="babe8-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="babe8-313">Passez en revue les bases de données hello dans une cible de collection de base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="babe8-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="babe8-314">Hello d’utilisation [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) applet de commande tooretrieve hello enfant bases de données d’une cible de collection de base de données personnalisée.</span><span class="sxs-lookup"><span data-stu-id="babe8-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="babe8-315">Créer un travail tooexecute un script sur une cible de collection personnalisé de la base de données</span><span class="sxs-lookup"><span data-stu-id="babe8-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="babe8-316">Hello d’utilisation [ **New-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate de l’applet de commande un travail par rapport à un groupe de bases de données définies par une cible de collection de base de données personnalisée.</span><span class="sxs-lookup"><span data-stu-id="babe8-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="babe8-317">Les travaux de base de données élastiques développera les travaux hello en plusieurs tâches enfants chaque base de données tooa correspondante associée cible de collecte de base de données personnalisée hello et assurez-vous que le script de hello est exécutée sur chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="babe8-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="babe8-318">Là encore, il est important que les scripts sont tooretries résilient de toobe idempotent.</span><span class="sxs-lookup"><span data-stu-id="babe8-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="babe8-319">Collecte de données sur les bases de données</span><span class="sxs-lookup"><span data-stu-id="babe8-319">Data collection across databases</span></span>
<span data-ttu-id="babe8-320">Vous pouvez utiliser un travail de tooexecute une requête sur un groupe de bases de données et envoyer hello tooa spécifiques résultant.</span><span class="sxs-lookup"><span data-stu-id="babe8-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="babe8-321">table de Hello peut être interrogée après les résultats de la requête hello hello faits toosee à partir de chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="babe8-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="babe8-322">Cela fournit une méthode asynchrone de tooexecute d’une requête entre plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="babe8-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="babe8-323">Les tentatives ayant échoué sont gérées automatiquement par l’exécution de nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="babe8-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="babe8-324">table de destination spécifiée Hello sera automatiquement créée si elle n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="babe8-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="babe8-325">nouvelle table de Hello correspond au schéma hello Hello retourné de jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="babe8-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="babe8-326">Si un script retourne plusieurs jeux de résultats, les tâches de base de données élastique n’envoie première table de destination toohello hello.</span><span class="sxs-lookup"><span data-stu-id="babe8-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="babe8-327">Bonjour script PowerShell suivant exécute un script et collecte ses résultats dans une table spécifiée.</span><span class="sxs-lookup"><span data-stu-id="babe8-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="babe8-328">Ce script part du principe qu’un script T-SQL, qui génère un jeu de résultats unique, et une cible de collecte de base de données personnalisée ont été créés.</span><span class="sxs-lookup"><span data-stu-id="babe8-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="babe8-329">Ce script utilise hello [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="babe8-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="babe8-330">Définir les paramètres de hello pour le script, informations d’identification et la cible de l’exécution :</span><span class="sxs-lookup"><span data-stu-id="babe8-330">Set hello parameters for script, credentials, and execution target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="babe8-331">toocreate et démarrer un travail pour les scénarios de collecte de données</span><span class="sxs-lookup"><span data-stu-id="babe8-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="babe8-332">Ce script utilise hello [ **Start-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="babe8-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="babe8-333">tooschedule un déclencheur de l’exécution du travail</span><span class="sxs-lookup"><span data-stu-id="babe8-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="babe8-334">Hello PowerShell script suivant peut être utilisé toocreate une planification périodique.</span><span class="sxs-lookup"><span data-stu-id="babe8-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="babe8-335">Ce script utilise un intervalle de minutes, mais [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) prend également en charge les paramètres -DayInterval, - HourInterval, - MonthInterval et - WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="babe8-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="babe8-336">Les planifications qui ne s'exécutent qu'une seule fois peuvent être créées en transmettant  - OneTime.</span><span class="sxs-lookup"><span data-stu-id="babe8-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="babe8-337">Créez une nouvelle planification :</span><span class="sxs-lookup"><span data-stu-id="babe8-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="babe8-338">tootrigger une tâche s’exécutée selon une planification</span><span class="sxs-lookup"><span data-stu-id="babe8-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="babe8-339">Un déclencheur de tâche peut être défini toohave un travail exécuté conformément tooa Calendrier.</span><span class="sxs-lookup"><span data-stu-id="babe8-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="babe8-340">Hello PowerShell script suivant peut être utilisé toocreate un déclencheur de tâche.</span><span class="sxs-lookup"><span data-stu-id="babe8-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="babe8-341">Utilisez [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) et en jeu hello suivant variables toocorrespond toohello souhaitée travail et planification :</span><span class="sxs-lookup"><span data-stu-id="babe8-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="babe8-342">tooremove un travail de toostop association planifiée à partir de l’exécution de la planification</span><span class="sxs-lookup"><span data-stu-id="babe8-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="babe8-343">toodiscontinue qui se reproduit l’exécution du travail via un déclencheur de tâche, le déclencheur de tâche hello peut être supprimée.</span><span class="sxs-lookup"><span data-stu-id="babe8-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="babe8-344">Supprimer un toostop de déclencheur de tâche un travail à partir d’en cours d’exécution en fonction tooa planification, à l’aide de hello [ **applet de commande Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="babe8-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="babe8-345">Récupérer la planification de temps de travail déclencheurs tooa liée</span><span class="sxs-lookup"><span data-stu-id="babe8-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="babe8-346">Hello PowerShell script suivant peut être tooobtain utilisé et afficher les hello planning déclencheurs tooa inscrits moment donné.</span><span class="sxs-lookup"><span data-stu-id="babe8-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="babe8-347">les déclencheurs de tâche tooretrieve lié tooa travail</span><span class="sxs-lookup"><span data-stu-id="babe8-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="babe8-348">Utilisez [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain et affichage des planifications contenant un travail inscrit.</span><span class="sxs-lookup"><span data-stu-id="babe8-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="babe8-349">toocreate une application de couche données (DACPAC) pour l’exécution entre bases de données</span><span class="sxs-lookup"><span data-stu-id="babe8-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="babe8-350">toocreate un DACPAC, consultez [applications de couche données](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="babe8-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="babe8-351">toodeploy un DACPAC, utilisez hello [applet de commande New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="babe8-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="babe8-352">Hello DACPAC doit être accessible toohello service.</span><span class="sxs-lookup"><span data-stu-id="babe8-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="babe8-353">Il est recommandé tooupload un tooAzure DACPAC créé stockage et de créer un [Signature d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md) pour hello DACPAC.</span><span class="sxs-lookup"><span data-stu-id="babe8-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="babe8-354">tooupdate une application de couche données (DACPAC) pour l’exécution entre bases de données</span><span class="sxs-lookup"><span data-stu-id="babe8-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="babe8-355">Dacpac existantes, enregistrées dans les travaux de base de données élastique peut être mis à jour toopoint toonew URI.</span><span class="sxs-lookup"><span data-stu-id="babe8-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="babe8-356">Hello d’utilisation [ **applet de commande Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI sur existant enregistré DACPAC :</span><span class="sxs-lookup"><span data-stu-id="babe8-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="babe8-357">toocreate un tooapply de travail une application de couche données (DACPAC) sur les bases de données</span><span class="sxs-lookup"><span data-stu-id="babe8-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="babe8-358">Une fois un DACPAC a été créé dans les tâches de base de données élastique, un travail peut être créé tooapply hello DACPAC sur un groupe de bases de données.</span><span class="sxs-lookup"><span data-stu-id="babe8-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="babe8-359">Hello PowerShell script suivant peut être utilisé toocreate un travail DACPAC sur un regroupement personnalisé des bases de données :</span><span class="sxs-lookup"><span data-stu-id="babe8-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
