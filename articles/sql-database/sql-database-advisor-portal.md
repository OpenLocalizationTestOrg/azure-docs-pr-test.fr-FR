---
title: "recommandations relatives aux performances aaaApply - base de données SQL Azure | Documents Microsoft"
description: "Vous pouvez utiliser hello toofind portail Azure recommandations relatives aux performances que vous pouvez optimiser les performances de votre base de données SQL Azure ou de toocorrect un problème identifié dans votre charge de travail."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="ecef8-103">Rechercher et appliquer les recommandations en matière de performances</span><span class="sxs-lookup"><span data-stu-id="ecef8-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="ecef8-104">Vous pouvez utiliser hello toofind portail Azure recommandations relatives aux performances que vous pouvez optimiser les performances de votre base de données SQL Azure ou de toocorrect un problème identifié dans votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="ecef8-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="ecef8-105">**Recommandation de performances** page du portail Azure vous permet de meilleures recommandations toofind hello en fonction de leur impact potentiel.</span><span class="sxs-lookup"><span data-stu-id="ecef8-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="ecef8-106">Affichage des recommandations</span><span class="sxs-lookup"><span data-stu-id="ecef8-106">Viewing recommendations</span></span>

<span data-ttu-id="ecef8-107">tooview et appliquer les recommandations relatives aux performances, vous devez hello correct [contrôle d’accès basé sur le rôle](../active-directory/role-based-access-control-what-is.md) autorisations dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ecef8-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="ecef8-108">**Lecteur**, **collaborateur de base de données SQL** autorisations sont requises tooview recommandations, et **propriétaire**, **collaborateur de base de données SQL** autorisations sont requises tooexecute toutes les actions ; créer ou supprimer des index et annuler la création d’index.</span><span class="sxs-lookup"><span data-stu-id="ecef8-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="ecef8-109">Utilisez hello suivant les recommandations relatives aux performances d’étapes toofind de portail Azure :</span><span class="sxs-lookup"><span data-stu-id="ecef8-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="ecef8-110">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ecef8-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ecef8-111">Accédez trop**davantage de services** > **bases de données SQL**, sélectionnez votre base de données.</span><span class="sxs-lookup"><span data-stu-id="ecef8-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="ecef8-112">Accédez trop**recommandation de performances** tooview des recommandations disponibles pour la base de données sélectionnée hello.</span><span class="sxs-lookup"><span data-stu-id="ecef8-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="ecef8-113">Recommandations relatives aux performances sont shonw dans toohello similaire hello table celui affiché sur hello figure suivante :</span><span class="sxs-lookup"><span data-stu-id="ecef8-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![Recommandations](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="ecef8-115">Recommandations sont triées par leur impact potentiel sur les performances en hello suivant des catégories :</span><span class="sxs-lookup"><span data-stu-id="ecef8-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="ecef8-116">Impact</span><span class="sxs-lookup"><span data-stu-id="ecef8-116">Impact</span></span> | <span data-ttu-id="ecef8-117">Description</span><span class="sxs-lookup"><span data-stu-id="ecef8-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ecef8-118">Élevé</span><span class="sxs-lookup"><span data-stu-id="ecef8-118">High</span></span> |<span data-ttu-id="ecef8-119">Recommandations de fort impact doivent fournir l’impact sur les performances significatives hello.</span><span class="sxs-lookup"><span data-stu-id="ecef8-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="ecef8-120">Moyenne</span><span class="sxs-lookup"><span data-stu-id="ecef8-120">Medium</span></span> |<span data-ttu-id="ecef8-121">Les recommandations ayant un impact moyen améliorent les performances, mais pas de manière substantielle.</span><span class="sxs-lookup"><span data-stu-id="ecef8-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="ecef8-122">Faible</span><span class="sxs-lookup"><span data-stu-id="ecef8-122">Low</span></span> |<span data-ttu-id="ecef8-123">Les recommandations ayant un faible impact fournissent de meilleures performances, mais les améliorations ne sont toutefois pas significatives.</span><span class="sxs-lookup"><span data-stu-id="ecef8-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="ecef8-124">Base de données SQL Azure doit toomonitor activités au moins un jour dans l’ordre tooidentify quelques recommandations.</span><span class="sxs-lookup"><span data-stu-id="ecef8-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="ecef8-125">Hello, base de données SQL Azure peut optimiser plus facilement des modèles de requête cohérente que possible pour les pics inégale aléatoires d’activité.</span><span class="sxs-lookup"><span data-stu-id="ecef8-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="ecef8-126">Si les recommandations ne sont pas Joins disponibles, hello **recommandation de performances** page affiche un message en explique la raison.</span><span class="sxs-lookup"><span data-stu-id="ecef8-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="ecef8-127">Vous pouvez également afficher des opérations historiques hello état hello.</span><span class="sxs-lookup"><span data-stu-id="ecef8-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="ecef8-128">Sélectionnez un toosee recommandation ou état plus de détails.</span><span class="sxs-lookup"><span data-stu-id="ecef8-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="ecef8-129">Voici un exemple de « Créer un index » de recommandation dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ecef8-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![Création d’index](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="ecef8-131">Application des recommandations</span><span class="sxs-lookup"><span data-stu-id="ecef8-131">Applying recommendations</span></span>
<span data-ttu-id="ecef8-132">Base de données SQL Azure vous offre un contrôle total sur la façon dont les recommandations sont activées à l’aide de hello trois options suivantes :</span><span class="sxs-lookup"><span data-stu-id="ecef8-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="ecef8-133">Appliquer les recommandations individuelles une à la fois.</span><span class="sxs-lookup"><span data-stu-id="ecef8-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="ecef8-134">Activer hello tooautomatically paramétrage automatique appliquer les recommandations.</span><span class="sxs-lookup"><span data-stu-id="ecef8-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="ecef8-135">tooimplement une recommandation exécuter manuellement, hello recommandé de script T-SQL sur votre base de données.</span><span class="sxs-lookup"><span data-stu-id="ecef8-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="ecef8-136">Sélectionnez n’importe quel tooview recommandation ses détails, puis cliquez **afficher le script** tooreview hello des informations précises concernant la création de recommandation de hello.</span><span class="sxs-lookup"><span data-stu-id="ecef8-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="ecef8-137">base de données Hello reste en ligne pendant que la recommandation de hello est appliquée, à l’aide de la recommandation de performances ou le paramétrage automatique jamais met une base de données hors connexion.</span><span class="sxs-lookup"><span data-stu-id="ecef8-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="ecef8-138">Appliquer une recommandation individuelle</span><span class="sxs-lookup"><span data-stu-id="ecef8-138">Apply an individual recommendation</span></span>
<span data-ttu-id="ecef8-139">Vous pouvez consulter et accepter les recommandations une à la fois.</span><span class="sxs-lookup"><span data-stu-id="ecef8-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="ecef8-140">Sur hello **recommandations** panneau, sélectionnez une recommandation.</span><span class="sxs-lookup"><span data-stu-id="ecef8-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="ecef8-141">Sur hello **détails** cliquez sur le panneau **appliquer** bouton.</span><span class="sxs-lookup"><span data-stu-id="ecef8-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![Appliquer une recommandation](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="ecef8-143">Recommandation sélectionnée est appliquée sur la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="ecef8-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="ecef8-144">Suppression de recommandations à partir de la liste de hello</span><span class="sxs-lookup"><span data-stu-id="ecef8-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="ecef8-145">Si votre liste de recommandations contient les éléments que vous souhaitez tooremove à partir de la liste de hello, vous pouvez ignorer la recommandation de hello :</span><span class="sxs-lookup"><span data-stu-id="ecef8-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="ecef8-146">Sélectionnez une recommandation dans la liste des hello **recommandations** détails de hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="ecef8-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="ecef8-147">Cliquez sur **ignorer** sur hello **détails** panneau.</span><span class="sxs-lookup"><span data-stu-id="ecef8-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="ecef8-148">Si vous le souhaitez, vous pouvez ajouter des éléments rejetés sauvegarder toohello **recommandations** liste :</span><span class="sxs-lookup"><span data-stu-id="ecef8-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="ecef8-149">Sur hello **recommandations** cliquez sur le panneau **vue ignorée**.</span><span class="sxs-lookup"><span data-stu-id="ecef8-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="ecef8-150">Sélectionnez un élément ignoré hello liste tooview ses détails.</span><span class="sxs-lookup"><span data-stu-id="ecef8-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="ecef8-151">Si vous le souhaitez, cliquez sur **Annuler ignorer** tooadd hello index différé toohello liste principale de **recommandations**.</span><span class="sxs-lookup"><span data-stu-id="ecef8-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="ecef8-152">Activer le réglage automatique</span><span class="sxs-lookup"><span data-stu-id="ecef8-152">Enable automatic tuning</span></span>
<span data-ttu-id="ecef8-153">Vous pouvez définir automatiquement les recommandations de tooimplement de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ecef8-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="ecef8-154">Dès qu’une recommandation est disponible, elle est automatiquement appliquée.</span><span class="sxs-lookup"><span data-stu-id="ecef8-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="ecef8-155">Comme avec toutes les recommandations sont gérées par hello service si l’impact sur les performances hello est recommandation de hello négatif vont être annulée.</span><span class="sxs-lookup"><span data-stu-id="ecef8-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="ecef8-156">Sur hello **recommandations** panneau, cliquez sur **automatiser**:</span><span class="sxs-lookup"><span data-stu-id="ecef8-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![Paramètres du conseiller](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="ecef8-158">Sélectionnez les actions tooautomate :</span><span class="sxs-lookup"><span data-stu-id="ecef8-158">Select actions tooautomate:</span></span>
   
    ![Index recommandés](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="ecef8-160">Exécuter manuellement hello recommandé de script T-SQL</span><span class="sxs-lookup"><span data-stu-id="ecef8-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="ecef8-161">Sélectionnez une recommandation, puis cliquez sur **Afficher le script**.</span><span class="sxs-lookup"><span data-stu-id="ecef8-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="ecef8-162">Exécutez ce script sur votre base de données toomanually appliquer la recommandation de hello.</span><span class="sxs-lookup"><span data-stu-id="ecef8-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="ecef8-163">*Index qui sont exécutés manuellement ne sont pas surveillées et validés pour l’impact sur les performances par le service de hello* donc il est recommandé de surveiller ces index après la création tooverify qu’ils fournissent des gains de performance et ajuster ou supprimez-les nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ecef8-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="ecef8-164">Pour plus d’informations sur la création d’index, consultez [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecef8-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="ecef8-165">Annulation de recommandations</span><span class="sxs-lookup"><span data-stu-id="ecef8-165">Canceling recommendations</span></span>
<span data-ttu-id="ecef8-166">Les recommandations ayant l’état **En attente**, **En cours de vérification** ou **Réussite** peuvent être annulées.</span><span class="sxs-lookup"><span data-stu-id="ecef8-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="ecef8-167">Les recommandations avec l'état **En cours d'exécution** ne peuvent pas être annulées.</span><span class="sxs-lookup"><span data-stu-id="ecef8-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="ecef8-168">Sélectionnez une recommandation Bonjour **de paramétrage de l’historique** hello tooopen de zone **les détails des recommandations** panneau.</span><span class="sxs-lookup"><span data-stu-id="ecef8-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="ecef8-169">Cliquez sur **Annuler** tooabort hello consistant à appliquer la recommandation de hello.</span><span class="sxs-lookup"><span data-stu-id="ecef8-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="ecef8-170">Surveillance des opérations</span><span class="sxs-lookup"><span data-stu-id="ecef8-170">Monitoring operations</span></span>
<span data-ttu-id="ecef8-171">L’application d’une recommandation ne se produit pas toujours instantanément.</span><span class="sxs-lookup"><span data-stu-id="ecef8-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="ecef8-172">portail de Hello fournit des détails concernant l’état de hello de recommandation.</span><span class="sxs-lookup"><span data-stu-id="ecef8-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="ecef8-173">Hello Voici les états possibles que peut contenir un index :</span><span class="sxs-lookup"><span data-stu-id="ecef8-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="ecef8-174">État</span><span class="sxs-lookup"><span data-stu-id="ecef8-174">Status</span></span> | <span data-ttu-id="ecef8-175">Description</span><span class="sxs-lookup"><span data-stu-id="ecef8-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ecef8-176">Pending</span><span class="sxs-lookup"><span data-stu-id="ecef8-176">Pending</span></span> |<span data-ttu-id="ecef8-177">La commande Appliquer la recommandation a été reçue et son exécution est planifiée.</span><span class="sxs-lookup"><span data-stu-id="ecef8-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="ecef8-178">En cours d'exécution</span><span class="sxs-lookup"><span data-stu-id="ecef8-178">Executing</span></span> |<span data-ttu-id="ecef8-179">recommandation de Hello est appliquée.</span><span class="sxs-lookup"><span data-stu-id="ecef8-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="ecef8-180">Vérification</span><span class="sxs-lookup"><span data-stu-id="ecef8-180">Verifying</span></span> |<span data-ttu-id="ecef8-181">Recommandation a été correctement appliquée et le service de hello mesure les avantages de hello.</span><span class="sxs-lookup"><span data-stu-id="ecef8-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="ecef8-182">Succès</span><span class="sxs-lookup"><span data-stu-id="ecef8-182">Success</span></span> |<span data-ttu-id="ecef8-183">La recommandation a été correctement appliquée et les avantages ont été évalués.</span><span class="sxs-lookup"><span data-stu-id="ecef8-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="ecef8-184">Error</span><span class="sxs-lookup"><span data-stu-id="ecef8-184">Error</span></span> |<span data-ttu-id="ecef8-185">Une erreur s’est produite pendant le processus hello de l’application de la recommandation de hello.</span><span class="sxs-lookup"><span data-stu-id="ecef8-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="ecef8-186">Cela peut être un problème temporaire, ou éventuellement une table de toohello de modifications de schéma et hello script n’est plus valide.</span><span class="sxs-lookup"><span data-stu-id="ecef8-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="ecef8-187">Annulation</span><span class="sxs-lookup"><span data-stu-id="ecef8-187">Reverting</span></span> |<span data-ttu-id="ecef8-188">recommandation de Hello a été appliquée, mais il a été jugée non performantes et est en cours de rétablissement automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ecef8-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="ecef8-189">Annulée</span><span class="sxs-lookup"><span data-stu-id="ecef8-189">Reverted</span></span> |<span data-ttu-id="ecef8-190">recommandation de Hello a été annulée.</span><span class="sxs-lookup"><span data-stu-id="ecef8-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="ecef8-191">Cliquez sur une recommandation dans le processus de hello liste toosee plus de détails :</span><span class="sxs-lookup"><span data-stu-id="ecef8-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![Index recommandés](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="ecef8-193">Annulation d'une recommandation</span><span class="sxs-lookup"><span data-stu-id="ecef8-193">Reverting a recommendation</span></span>
<span data-ttu-id="ecef8-194">Si vous avez utilisé la recommandation de hello hello performances recommandations tooapply (ce qui signifie que vous n’avez exécuté pas manuellement les script hello T-SQL) il est automatiquement rétabli il s’il en trouve hello performance impact toobe négatif.</span><span class="sxs-lookup"><span data-stu-id="ecef8-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="ecef8-195">Si pour une raison quelconque vous souhaitez simplement toorevert une recommandation faire suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="ecef8-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="ecef8-196">Sélectionnez une recommandation appliquée correctement Bonjour **paramétrage historique** zone.</span><span class="sxs-lookup"><span data-stu-id="ecef8-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="ecef8-197">Cliquez sur **Revert** sur hello **détails de la recommandation** panneau.</span><span class="sxs-lookup"><span data-stu-id="ecef8-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![Index recommandés](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="ecef8-199">Analyse de l’impact des recommandations d’index sur les performances</span><span class="sxs-lookup"><span data-stu-id="ecef8-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="ecef8-200">Une fois que les recommandations sont correctement mises en œuvre (actuellement, les opérations d’index et paramétrer des recommandations de requêtes uniquement) vous pouvez cliquer sur **analyse des requêtes** sur hello recommandation détails panneau tooopen [requête Analyse des performances](sql-database-query-performance.md) et voir l’impact sur les performances hello de vos requêtes principales.</span><span class="sxs-lookup"><span data-stu-id="ecef8-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![Surveiller l’impact sur les performances](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="ecef8-202">Résumé</span><span class="sxs-lookup"><span data-stu-id="ecef8-202">Summary</span></span>
<span data-ttu-id="ecef8-203">Azure SQL Database fournit des recommandations pour améliorer les performances des bases de données SQL.</span><span class="sxs-lookup"><span data-stu-id="ecef8-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="ecef8-204">Les scripts T-SQL, ainsi que les options individuelles et entièrement automatiques, facilitent l’optimisation de votre base de données, avec à la clé une amélioration des performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="ecef8-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecef8-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ecef8-205">Next steps</span></span>
<span data-ttu-id="ecef8-206">Surveiller vos recommandations et continuer tooapply les performances de toorefine.</span><span class="sxs-lookup"><span data-stu-id="ecef8-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="ecef8-207">Les charges de travail d’une base de données sont dynamiques et évoluent en permanence.</span><span class="sxs-lookup"><span data-stu-id="ecef8-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="ecef8-208">Base de données SQL Azure seront continuer toomonitor et fournir des recommandations qui peuvent permettre d’améliorer les performances de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="ecef8-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="ecef8-209">Consultez [le paramétrage automatique](sql-database-automatic-tuning.md) toolearn savoir plus sur hello réglage automatique dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ecef8-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="ecef8-210">Consultez [Recommandations en matière de performances](sql-database-advisor.md) pour obtenir une vue d’ensemble des recommandations relatives aux performances Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ecef8-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="ecef8-211">Consultez [analyse des performances des requêtes](sql-database-query-performance.md) toolearn sur l’affichage des performances hello de vos requêtes principales.</span><span class="sxs-lookup"><span data-stu-id="ecef8-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ecef8-212">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ecef8-212">Additional resources</span></span>
* [<span data-ttu-id="ecef8-213">Magasin de requêtes</span><span class="sxs-lookup"><span data-stu-id="ecef8-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="ecef8-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="ecef8-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="ecef8-215">Contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="ecef8-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

