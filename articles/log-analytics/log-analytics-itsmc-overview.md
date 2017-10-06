---
title: aaaIT connecteur de gestion de Service dans OMS | Documents Microsoft
description: "Utiliser le moniteur de toocentrally hello connecteur de gestion du Service informatique et gérer des éléments de travail ITSM hello dans OMS et résoudre les problèmes rapidement."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="f181c-103">Gérer de manière centralisée les éléments de travail ITSM à l’aide d’IT Service Management Connector (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="f181c-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Symbole d’IT Service Management Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="f181c-105">Vous pouvez utiliser hello connecteur de gestion de Service informatique (ITSMC) dans le moniteur de toocentrally Analytique des journaux OMS et gérer des éléments de travail sur votre ITSM produits/services.</span><span class="sxs-lookup"><span data-stu-id="f181c-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="f181c-106">Connecteur de gestion du Service informatique de Hello intègre Analytique des journaux OMS vos produits de gestion de services informatiques (ITSM) existants et les services.</span><span class="sxs-lookup"><span data-stu-id="f181c-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="f181c-107">solution de Hello offre une intégration bidirectionnelle avec ITSM produits/services, où il fournit hello utilisateurs d’OMS un incident de toocreate option, les alertes ou les événements dans les solutions ITSM.</span><span class="sxs-lookup"><span data-stu-id="f181c-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="f181c-108">connecteur de Hello importe également les données, tels que les incidents et les demandes de modification à partir de la solution ITSM dans Analytique de journal d’OMS.</span><span class="sxs-lookup"><span data-stu-id="f181c-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="f181c-109">IT Service Management Connector vous offre de nombreuses possibilités :</span><span class="sxs-lookup"><span data-stu-id="f181c-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="f181c-110">Surveiller et gérer de manière centralisée des éléments de travail pour les produits/services ITSM utilisés au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="f181c-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="f181c-111">Créer des éléments de travail ITSM (tels que des alertes, des événements et des incidents) dans ITSM à partir des alertes OMS et via la fonctionnalité de recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="f181c-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="f181c-112">Lire les incidents et les demandes de modification de votre solution ITSM et les mettre en corrélation avec les données de journal pertinentes dans l’espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f181c-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="f181c-113">Retrouver des événements inattendus et inhabituels et résolvez-les avant même que les utilisateurs finaux de hello appeler et les signaler du support technique toohello.</span><span class="sxs-lookup"><span data-stu-id="f181c-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="f181c-114">Importer des données d’éléments de travail dans Log Analytics et créer des rapports d’indicateurs de performance clés.</span><span class="sxs-lookup"><span data-stu-id="f181c-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="f181c-115">Grâce à ces rapports, vous pouvez identifier, analyser et agir sur plusieurs éléments importants tels que l’évaluation des programmes malveillants.</span><span class="sxs-lookup"><span data-stu-id="f181c-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="f181c-116">Afficher des tableaux de bord spécialement conçus pour fournir des informations plus détaillées sur les incidents, les demandes de modification et les systèmes concernés.</span><span class="sxs-lookup"><span data-stu-id="f181c-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="f181c-117">Résoudre les problèmes plus rapidement en mettant en corrélation avec d’autres solutions de gestion dans l’espace de travail hello Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="f181c-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f181c-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f181c-118">Prerequisites</span></span>

<span data-ttu-id="f181c-119">éléments de travail ITSM tooimport hello dans Analytique des journaux OMS, solution de hello requiert une connexion entre hello connecteur de gestion du Service informatique Bonjour OMS et hello informatique SM produits et services à partir duquel vous importez des éléments de travail hello.</span><span class="sxs-lookup"><span data-stu-id="f181c-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="f181c-120">Configuration</span><span class="sxs-lookup"><span data-stu-id="f181c-120">Configuration</span></span>

<span data-ttu-id="f181c-121">Ajouter hello espace de travail du connecteur de gestion du Service informatique solution tooyour OMS, à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="f181c-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="f181c-122">Connecteur de gestion du Service informatique vignette que vous voyez dans la galerie des Solutions hello :</span><span class="sxs-lookup"><span data-stu-id="f181c-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![vignette du connecteur](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="f181c-124">Après avoir été ajoutée avec succès, vous verrez hello connecteur de gestion de Service informatique sous **OMS** > **paramètres** > **Sources connectées.**</span><span class="sxs-lookup"><span data-stu-id="f181c-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC connecté](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="f181c-126">Par défaut, hello connecteur de gestion du Service informatique actualise les données de la connexion hello qu’une seule fois dans toutes les 24 heures.</span><span class="sxs-lookup"><span data-stu-id="f181c-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="f181c-127">toorefresh données de votre connexion instantanément pour les modifications ou d’un modèle de mises à jour que vous apportez, cliquez sur la connexion suivante tooyour hello actualisation bouton affiché.</span><span class="sxs-lookup"><span data-stu-id="f181c-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![Actualisation d’ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="f181c-129">Packs d’administration</span><span class="sxs-lookup"><span data-stu-id="f181c-129">Management packs</span></span>
<span data-ttu-id="f181c-130">Cette solution ne requiert aucun pack d’administration.</span><span class="sxs-lookup"><span data-stu-id="f181c-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="f181c-131">Sources connectées</span><span class="sxs-lookup"><span data-stu-id="f181c-131">Connected sources</span></span>

<span data-ttu-id="f181c-132">Hello ITSM produits/services suivants sont pris en charge par hello connecteur de gestion du Service informatique :</span><span class="sxs-lookup"><span data-stu-id="f181c-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- [<span data-ttu-id="f181c-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="f181c-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="f181c-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="f181c-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="f181c-135">Provance</span><span class="sxs-lookup"><span data-stu-id="f181c-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="f181c-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="f181c-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="f181c-137">À l’aide de la solution de hello</span><span class="sxs-lookup"><span data-stu-id="f181c-137">Using hello solution</span></span>

<span data-ttu-id="f181c-138">Lorsque vous connectez hello connecteur de gestion du Service OMS informatique avec votre service ITSM, services d’Analytique de journal hello démarre collecte des données de hello de hello connecté ITSM produits/service.</span><span class="sxs-lookup"><span data-stu-id="f181c-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="f181c-139">Les données importées par la solution IT Service Management Connector s’affichent dans Log Analytics en tant qu’événements nommés **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="f181c-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="f181c-140">Chaque événement contient un champ nommé **ServiceDeskWorkItemType_s**</span><span class="sxs-lookup"><span data-stu-id="f181c-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="f181c-141">qui peut prendre sa valeur comme un incident, ou la demande de modification, selon hello d’élément de travail données contenues dans hello **ServiceDesk_CL** événement.</span><span class="sxs-lookup"><span data-stu-id="f181c-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="f181c-142">Données d’entrée</span><span class="sxs-lookup"><span data-stu-id="f181c-142">Input data</span></span>
<span data-ttu-id="f181c-143">Éléments de travail importés à partir de hello ITSM produits/services.</span><span class="sxs-lookup"><span data-stu-id="f181c-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="f181c-144">Hello informations suivantes montre des exemples de données collectées par le connecteur de gestion des services informatiques hello :</span><span class="sxs-lookup"><span data-stu-id="f181c-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="f181c-145">En fonction de hello type élément de travail importé dans le journal Analytique, **ServiceDesk_CL** contient hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="f181c-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="f181c-146">**Élément de travail :****Incidents**</span><span class="sxs-lookup"><span data-stu-id="f181c-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="f181c-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="f181c-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="f181c-148">**Champs**</span><span class="sxs-lookup"><span data-stu-id="f181c-148">**Fields**</span></span>

- <span data-ttu-id="f181c-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="f181c-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="f181c-150">ID du service d’assistance</span><span class="sxs-lookup"><span data-stu-id="f181c-150">Service Desk ID</span></span>
- <span data-ttu-id="f181c-151">State</span><span class="sxs-lookup"><span data-stu-id="f181c-151">State</span></span>
- <span data-ttu-id="f181c-152">Urgence</span><span class="sxs-lookup"><span data-stu-id="f181c-152">Urgency</span></span>
- <span data-ttu-id="f181c-153">Impact</span><span class="sxs-lookup"><span data-stu-id="f181c-153">Impact</span></span>
- <span data-ttu-id="f181c-154">Priorité</span><span class="sxs-lookup"><span data-stu-id="f181c-154">Priority</span></span>
- <span data-ttu-id="f181c-155">Escalade</span><span class="sxs-lookup"><span data-stu-id="f181c-155">Escalation</span></span>
- <span data-ttu-id="f181c-156">Créé par</span><span class="sxs-lookup"><span data-stu-id="f181c-156">Created By</span></span>
- <span data-ttu-id="f181c-157">Résolu par</span><span class="sxs-lookup"><span data-stu-id="f181c-157">Resolved By</span></span>
- <span data-ttu-id="f181c-158">Fermé par</span><span class="sxs-lookup"><span data-stu-id="f181c-158">Closed By</span></span>
- <span data-ttu-id="f181c-159">Source</span><span class="sxs-lookup"><span data-stu-id="f181c-159">Source</span></span>
- <span data-ttu-id="f181c-160">Affecté à</span><span class="sxs-lookup"><span data-stu-id="f181c-160">Assigned To</span></span>
- <span data-ttu-id="f181c-161">Catégorie</span><span class="sxs-lookup"><span data-stu-id="f181c-161">Category</span></span>
- <span data-ttu-id="f181c-162">Intitulé</span><span class="sxs-lookup"><span data-stu-id="f181c-162">Title</span></span>
- <span data-ttu-id="f181c-163">Description</span><span class="sxs-lookup"><span data-stu-id="f181c-163">Description</span></span>
- <span data-ttu-id="f181c-164">Date de création</span><span class="sxs-lookup"><span data-stu-id="f181c-164">Created Date</span></span>
- <span data-ttu-id="f181c-165">Date de fermeture</span><span class="sxs-lookup"><span data-stu-id="f181c-165">Closed Date</span></span>
- <span data-ttu-id="f181c-166">Date de résolution</span><span class="sxs-lookup"><span data-stu-id="f181c-166">Resolved Date</span></span>
- <span data-ttu-id="f181c-167">Date de dernière modification</span><span class="sxs-lookup"><span data-stu-id="f181c-167">Last Modified Date</span></span>
- <span data-ttu-id="f181c-168">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="f181c-168">Computer</span></span>


<span data-ttu-id="f181c-169">**Élément de travail :****Demandes de modification**</span><span class="sxs-lookup"><span data-stu-id="f181c-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="f181c-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="f181c-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="f181c-171">**Champs**</span><span class="sxs-lookup"><span data-stu-id="f181c-171">**Fields**</span></span>
- <span data-ttu-id="f181c-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="f181c-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="f181c-173">ID du service d’assistance</span><span class="sxs-lookup"><span data-stu-id="f181c-173">Service Desk ID</span></span>
- <span data-ttu-id="f181c-174">Créé par</span><span class="sxs-lookup"><span data-stu-id="f181c-174">Created By</span></span>
- <span data-ttu-id="f181c-175">Fermé par</span><span class="sxs-lookup"><span data-stu-id="f181c-175">Closed By</span></span>
- <span data-ttu-id="f181c-176">Source</span><span class="sxs-lookup"><span data-stu-id="f181c-176">Source</span></span>
- <span data-ttu-id="f181c-177">Affecté à</span><span class="sxs-lookup"><span data-stu-id="f181c-177">Assigned To</span></span>
- <span data-ttu-id="f181c-178">Intitulé</span><span class="sxs-lookup"><span data-stu-id="f181c-178">Title</span></span>
- <span data-ttu-id="f181c-179">Type</span><span class="sxs-lookup"><span data-stu-id="f181c-179">Type</span></span>
- <span data-ttu-id="f181c-180">Catégorie</span><span class="sxs-lookup"><span data-stu-id="f181c-180">Category</span></span>
- <span data-ttu-id="f181c-181">State</span><span class="sxs-lookup"><span data-stu-id="f181c-181">State</span></span>
- <span data-ttu-id="f181c-182">Escalade</span><span class="sxs-lookup"><span data-stu-id="f181c-182">Escalation</span></span>
- <span data-ttu-id="f181c-183">État conflictuel</span><span class="sxs-lookup"><span data-stu-id="f181c-183">Conflict Status</span></span>
- <span data-ttu-id="f181c-184">Urgence</span><span class="sxs-lookup"><span data-stu-id="f181c-184">Urgency</span></span>
- <span data-ttu-id="f181c-185">Priorité</span><span class="sxs-lookup"><span data-stu-id="f181c-185">Priority</span></span>
- <span data-ttu-id="f181c-186">Risque</span><span class="sxs-lookup"><span data-stu-id="f181c-186">Risk</span></span>
- <span data-ttu-id="f181c-187">Impact</span><span class="sxs-lookup"><span data-stu-id="f181c-187">Impact</span></span>
- <span data-ttu-id="f181c-188">Affecté à</span><span class="sxs-lookup"><span data-stu-id="f181c-188">Assigned To</span></span>
- <span data-ttu-id="f181c-189">Date de création</span><span class="sxs-lookup"><span data-stu-id="f181c-189">Created Date</span></span>
- <span data-ttu-id="f181c-190">Date de fermeture</span><span class="sxs-lookup"><span data-stu-id="f181c-190">Closed Date</span></span>
- <span data-ttu-id="f181c-191">Date de dernière modification</span><span class="sxs-lookup"><span data-stu-id="f181c-191">Last Modified Date</span></span>
- <span data-ttu-id="f181c-192">Date de la demande</span><span class="sxs-lookup"><span data-stu-id="f181c-192">Requested Date</span></span>
- <span data-ttu-id="f181c-193">Date de début prévue</span><span class="sxs-lookup"><span data-stu-id="f181c-193">Planned Start Date</span></span>
- <span data-ttu-id="f181c-194">Date de fin prévue</span><span class="sxs-lookup"><span data-stu-id="f181c-194">Planned End Date</span></span>
- <span data-ttu-id="f181c-195">Date de début du travail</span><span class="sxs-lookup"><span data-stu-id="f181c-195">Work Start Date</span></span>
- <span data-ttu-id="f181c-196">Date de fin du travail</span><span class="sxs-lookup"><span data-stu-id="f181c-196">Work End Date</span></span>
- <span data-ttu-id="f181c-197">Description</span><span class="sxs-lookup"><span data-stu-id="f181c-197">Description</span></span>
- <span data-ttu-id="f181c-198">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="f181c-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="f181c-199">Données de sortie pour un incident ServiceNow</span><span class="sxs-lookup"><span data-stu-id="f181c-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="f181c-200">Champ OMS</span><span class="sxs-lookup"><span data-stu-id="f181c-200">OMS field</span></span> | <span data-ttu-id="f181c-201">Champ ITSM</span><span class="sxs-lookup"><span data-stu-id="f181c-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="f181c-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="f181c-202">ServiceDeskId_s</span></span>| <span data-ttu-id="f181c-203">Number</span><span class="sxs-lookup"><span data-stu-id="f181c-203">Number</span></span> |
| <span data-ttu-id="f181c-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="f181c-204">IncidentState_s</span></span> | <span data-ttu-id="f181c-205">State</span><span class="sxs-lookup"><span data-stu-id="f181c-205">State</span></span> |
| <span data-ttu-id="f181c-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="f181c-206">Urgency_s</span></span> |<span data-ttu-id="f181c-207">Urgence</span><span class="sxs-lookup"><span data-stu-id="f181c-207">Urgency</span></span> |
| <span data-ttu-id="f181c-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="f181c-208">Impact_s</span></span> |<span data-ttu-id="f181c-209">Impact</span><span class="sxs-lookup"><span data-stu-id="f181c-209">Impact</span></span>|
| <span data-ttu-id="f181c-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="f181c-210">Priority_s</span></span> | <span data-ttu-id="f181c-211">Priorité</span><span class="sxs-lookup"><span data-stu-id="f181c-211">Priority</span></span> |
| <span data-ttu-id="f181c-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="f181c-212">CreatedBy_s</span></span> | <span data-ttu-id="f181c-213">Ouvert par</span><span class="sxs-lookup"><span data-stu-id="f181c-213">Opened by</span></span> |
| <span data-ttu-id="f181c-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="f181c-214">ResolvedBy_s</span></span> | <span data-ttu-id="f181c-215">Résolu par</span><span class="sxs-lookup"><span data-stu-id="f181c-215">Resolved by</span></span>|
| <span data-ttu-id="f181c-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="f181c-216">ClosedBy_s</span></span>  | <span data-ttu-id="f181c-217">Fermé par</span><span class="sxs-lookup"><span data-stu-id="f181c-217">Closed by</span></span> |
| <span data-ttu-id="f181c-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="f181c-218">Source_s</span></span>| <span data-ttu-id="f181c-219">Type de contact</span><span class="sxs-lookup"><span data-stu-id="f181c-219">Contact type</span></span> |
| <span data-ttu-id="f181c-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="f181c-220">AssignedTo_s</span></span> | <span data-ttu-id="f181c-221">Trop d’assigné</span><span class="sxs-lookup"><span data-stu-id="f181c-221">Assigned too</span></span> |
| <span data-ttu-id="f181c-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="f181c-222">Category_s</span></span> | <span data-ttu-id="f181c-223">Catégorie</span><span class="sxs-lookup"><span data-stu-id="f181c-223">Category</span></span> |
| <span data-ttu-id="f181c-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="f181c-224">Title_s</span></span>|  <span data-ttu-id="f181c-225">Brève description</span><span class="sxs-lookup"><span data-stu-id="f181c-225">Short description</span></span> |
| <span data-ttu-id="f181c-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="f181c-226">Description_s</span></span>|  <span data-ttu-id="f181c-227">Remarques</span><span class="sxs-lookup"><span data-stu-id="f181c-227">Notes</span></span> |
| <span data-ttu-id="f181c-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="f181c-228">CreatedDate_t</span></span>|  <span data-ttu-id="f181c-229">Ouvert</span><span class="sxs-lookup"><span data-stu-id="f181c-229">Opened</span></span> |
| <span data-ttu-id="f181c-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="f181c-230">ClosedDate_t</span></span>| <span data-ttu-id="f181c-231">Fermé</span><span class="sxs-lookup"><span data-stu-id="f181c-231">closed</span></span>|
| <span data-ttu-id="f181c-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="f181c-232">ResolvedDate_t</span></span>|<span data-ttu-id="f181c-233">Résolu</span><span class="sxs-lookup"><span data-stu-id="f181c-233">Resolved</span></span>|
| <span data-ttu-id="f181c-234">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="f181c-234">Computer</span></span>  | <span data-ttu-id="f181c-235">Élément de configuration</span><span class="sxs-lookup"><span data-stu-id="f181c-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="f181c-236">Données de sortie pour une demande de modification ServiceNow</span><span class="sxs-lookup"><span data-stu-id="f181c-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="f181c-237">Champ OMS</span><span class="sxs-lookup"><span data-stu-id="f181c-237">OMS field</span></span> | <span data-ttu-id="f181c-238">Champ ITSM</span><span class="sxs-lookup"><span data-stu-id="f181c-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="f181c-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="f181c-239">ServiceDeskId_s</span></span>| <span data-ttu-id="f181c-240">Number</span><span class="sxs-lookup"><span data-stu-id="f181c-240">Number</span></span> |
| <span data-ttu-id="f181c-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="f181c-241">CreatedBy_s</span></span> | <span data-ttu-id="f181c-242">Demandé par</span><span class="sxs-lookup"><span data-stu-id="f181c-242">Requested by</span></span> |
| <span data-ttu-id="f181c-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="f181c-243">ClosedBy_s</span></span> | <span data-ttu-id="f181c-244">Fermé par</span><span class="sxs-lookup"><span data-stu-id="f181c-244">Closed by</span></span> |
| <span data-ttu-id="f181c-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="f181c-245">AssignedTo_s</span></span> | <span data-ttu-id="f181c-246">Trop d’assigné</span><span class="sxs-lookup"><span data-stu-id="f181c-246">Assigned too</span></span> |
| <span data-ttu-id="f181c-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="f181c-247">Title_s</span></span>|  <span data-ttu-id="f181c-248">Brève description</span><span class="sxs-lookup"><span data-stu-id="f181c-248">Short description</span></span> |
| <span data-ttu-id="f181c-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="f181c-249">Type_s</span></span>|  <span data-ttu-id="f181c-250">Type</span><span class="sxs-lookup"><span data-stu-id="f181c-250">Type</span></span> |
| <span data-ttu-id="f181c-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="f181c-251">Category_s</span></span>|  <span data-ttu-id="f181c-252">Catégorie</span><span class="sxs-lookup"><span data-stu-id="f181c-252">Catgory</span></span> |
| <span data-ttu-id="f181c-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="f181c-253">CRState_s</span></span>|  <span data-ttu-id="f181c-254">State</span><span class="sxs-lookup"><span data-stu-id="f181c-254">State</span></span>|
| <span data-ttu-id="f181c-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="f181c-255">Urgency_s</span></span>|  <span data-ttu-id="f181c-256">Urgence</span><span class="sxs-lookup"><span data-stu-id="f181c-256">Urgency</span></span> |
| <span data-ttu-id="f181c-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="f181c-257">Priority_s</span></span>| <span data-ttu-id="f181c-258">Priorité</span><span class="sxs-lookup"><span data-stu-id="f181c-258">Priority</span></span>|
| <span data-ttu-id="f181c-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="f181c-259">Risk_s</span></span>| <span data-ttu-id="f181c-260">Risque</span><span class="sxs-lookup"><span data-stu-id="f181c-260">Risk</span></span>|
| <span data-ttu-id="f181c-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="f181c-261">Impact_s</span></span>| <span data-ttu-id="f181c-262">Impact</span><span class="sxs-lookup"><span data-stu-id="f181c-262">Impact</span></span>|
| <span data-ttu-id="f181c-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="f181c-263">RequestedDate_t</span></span>  | <span data-ttu-id="f181c-264">Date demandée</span><span class="sxs-lookup"><span data-stu-id="f181c-264">Requested by date</span></span> |
| <span data-ttu-id="f181c-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="f181c-265">ClosedDate_t</span></span> | <span data-ttu-id="f181c-266">Date de fermeture</span><span class="sxs-lookup"><span data-stu-id="f181c-266">Closed date</span></span> |
| <span data-ttu-id="f181c-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="f181c-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="f181c-268">Date de début prévue</span><span class="sxs-lookup"><span data-stu-id="f181c-268">Planned start date</span></span> |
| <span data-ttu-id="f181c-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="f181c-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="f181c-270">Date de fin prévue</span><span class="sxs-lookup"><span data-stu-id="f181c-270">Planned end date</span></span> |
| <span data-ttu-id="f181c-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="f181c-271">WorkStartDate_t</span></span>  | <span data-ttu-id="f181c-272">Date de début réelle</span><span class="sxs-lookup"><span data-stu-id="f181c-272">Actual start date</span></span> |
| <span data-ttu-id="f181c-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="f181c-273">WorkEndDate_t</span></span> | <span data-ttu-id="f181c-274">Date de fin réelle</span><span class="sxs-lookup"><span data-stu-id="f181c-274">Actual end date</span></span>|
| <span data-ttu-id="f181c-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="f181c-275">Description_s</span></span> | <span data-ttu-id="f181c-276">Description</span><span class="sxs-lookup"><span data-stu-id="f181c-276">Description</span></span> |
| <span data-ttu-id="f181c-277">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="f181c-277">Computer</span></span>  | <span data-ttu-id="f181c-278">Élément de configuration</span><span class="sxs-lookup"><span data-stu-id="f181c-278">Configuration Item</span></span> |

<span data-ttu-id="f181c-279">**Exemple d’écran Log Analytics pour les données ITSM :**</span><span class="sxs-lookup"><span data-stu-id="f181c-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Écran Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="f181c-281">IT Service Management Connector – intégration avec d’autres solutions OMS</span><span class="sxs-lookup"><span data-stu-id="f181c-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="f181c-282">Connecteur de gestion du Service informatique, prend actuellement en charge l’intégration avec hello solutions de carte de Service.</span><span class="sxs-lookup"><span data-stu-id="f181c-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="f181c-283">Carte de service découvre automatiquement les hello des composants de l’application sur Windows et les mappages et les systèmes Linux hello la communication entre les services.</span><span class="sxs-lookup"><span data-stu-id="f181c-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="f181c-284">Il vous permet de tooview vos serveurs en tant que vous les – considérer comme des réseaux interconnectés qui fournissent des services critiques.</span><span class="sxs-lookup"><span data-stu-id="f181c-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="f181c-285">Carte de service affiche les connexions entre les serveurs, les processus et les ports sur n’importe quelle architecture connectée à TCP, sans configuration requise autre que l’installation d’un agent.</span><span class="sxs-lookup"><span data-stu-id="f181c-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="f181c-286">Pour en savoir plus : [Carte de service](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="f181c-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="f181c-287">Avec cette intégration, vous pouvez afficher les éléments de support de service hello créés dans les solutions ITSM hello comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f181c-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="f181c-288">Solution intégrée</span><span class="sxs-lookup"><span data-stu-id="f181c-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="f181c-289">Créer des éléments de travail ITSM pour des alertes OMS</span><span class="sxs-lookup"><span data-stu-id="f181c-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="f181c-290">Pour les alertes d’OMS hello, vous pouvez créer des éléments de travail associés dans les sources de ITSM hello connecté.</span><span class="sxs-lookup"><span data-stu-id="f181c-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="f181c-291">toodo, hello utilisez procédure :</span><span class="sxs-lookup"><span data-stu-id="f181c-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="f181c-292">À partir de **recherche de journal** fenêtre, exécutez une données tooview journal des requêtes.</span><span class="sxs-lookup"><span data-stu-id="f181c-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="f181c-293">Résultats de la requête sont source de hello pour les éléments de travail.</span><span class="sxs-lookup"><span data-stu-id="f181c-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="f181c-294">Dans **recherche de journal**, cliquez sur **alerte** tooopen hello **ajouter une règle d’alerte** page.</span><span class="sxs-lookup"><span data-stu-id="f181c-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Écran Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="f181c-296">Sur hello **ajouter une règle d’alerte** fenêtre, fournissent des détails hello requis pour **nom**, **gravité**, **recherche**, et  **Critères d’alerte** (mesure fenêtre/métrique de temps).</span><span class="sxs-lookup"><span data-stu-id="f181c-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="f181c-297">Sélectionnez **Oui** pour **Actions ITSM**.</span><span class="sxs-lookup"><span data-stu-id="f181c-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="f181c-298">Sélectionnez votre connexion ITSM hello **sélectionner une connexion** liste.</span><span class="sxs-lookup"><span data-stu-id="f181c-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="f181c-299">Fournir des détails hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="f181c-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="f181c-300">toocreate un élément de travail distinct pour chaque entrée de journal de hello de cette alerte, sélectionnez **créer des éléments de travail pour chaque entrée de journal** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="f181c-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="f181c-301">Ou</span><span class="sxs-lookup"><span data-stu-id="f181c-301">Or</span></span>

    <span data-ttu-id="f181c-302">Laissez cet case à cocher toocreate non sélectionnées uniquement un élément de travail pour n’importe quel nombre d’entrées de journal sous cette alerte.</span><span class="sxs-lookup"><span data-stu-id="f181c-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="f181c-303">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f181c-303">Click **Save**.</span></span>

<span data-ttu-id="f181c-304">alerte d’OMS Hello est créé sous **alertes**.</span><span class="sxs-lookup"><span data-stu-id="f181c-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="f181c-305">Bonjour le travail de la connexion correspondante ITSM éléments sont créés lorsque condition l’alerte spécifiée hello est remplie.</span><span class="sxs-lookup"><span data-stu-id="f181c-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="f181c-306">Créer des éléments de travail ITSM à partir de journaux OMS</span><span class="sxs-lookup"><span data-stu-id="f181c-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="f181c-307">Vous pouvez créer des éléments de travail dans les sources de ITSM hello connecté à l’aide de recherche de journal d’OMS.</span><span class="sxs-lookup"><span data-stu-id="f181c-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="f181c-308">toodo, hello utilisez procédure :</span><span class="sxs-lookup"><span data-stu-id="f181c-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="f181c-309">À partir de **recherche de journal**, rechercher les données de salutation requis, sélectionnez les détails de hello, puis cliquez sur **élément de travail de création**.</span><span class="sxs-lookup"><span data-stu-id="f181c-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="f181c-310">Hello **élément de travail de ITSM créer** fenêtre s’affiche :</span><span class="sxs-lookup"><span data-stu-id="f181c-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Écran Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="f181c-312">Ajoutez hello les détails suivants :</span><span class="sxs-lookup"><span data-stu-id="f181c-312">Add hello following details:</span></span>

  - <span data-ttu-id="f181c-313">**Titre de l’élément de travail**: titre de l’élément de travail hello.</span><span class="sxs-lookup"><span data-stu-id="f181c-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="f181c-314">**Description de l’élément de travail**: Description pour le nouvel élément de travail hello.</span><span class="sxs-lookup"><span data-stu-id="f181c-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="f181c-315">**Impact sur ordinateur**: nom de l’ordinateur hello où les données de journal a été trouvées.</span><span class="sxs-lookup"><span data-stu-id="f181c-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="f181c-316">**Sélectionnez la connexion**: connexion ITSM dans lequel vous souhaitez toocreate cet élément de travail.</span><span class="sxs-lookup"><span data-stu-id="f181c-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="f181c-317">**Élément de travail** : type d’élément de travail.</span><span class="sxs-lookup"><span data-stu-id="f181c-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="f181c-318">toouse un modèle d’élément de travail existant d’un incident, cliquez sur **Oui** sous **élément de travail de génération basé sur le modèle de hello** option, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="f181c-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="f181c-319">Ou,</span><span class="sxs-lookup"><span data-stu-id="f181c-319">Or,</span></span>

    <span data-ttu-id="f181c-320">Cliquez sur **non** si vous souhaitez tooprovide vos valeurs personnalisées.</span><span class="sxs-lookup"><span data-stu-id="f181c-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="f181c-321">Entrez les valeurs appropriées hello Bonjour **Type de Contact**, **Impact**, **urgence**, **catégorie**, et **sous-catégorie**  zones de texte, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="f181c-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="f181c-322">élément de travail Hello sera créé dans hello ITSM, que vous pouvez également afficher dans OMS.</span><span class="sxs-lookup"><span data-stu-id="f181c-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="f181c-323">Dépanner des connexions ITSM dans OMS</span><span class="sxs-lookup"><span data-stu-id="f181c-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="f181c-324">Si connexion échoue à partir de l’interface utilisateur de la source connecté et que vous obtenez hello **erreur lors de l’enregistrement de connexion** message, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f181c-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="f181c-325">En cas de connexions de ServiceNow, Cherwell et Provance, vérifiez que vous entré correctement hello client et le nom d’utilisateur/mot de passe ID/question secrète du client pour chacune des connexions de hello.</span><span class="sxs-lookup"><span data-stu-id="f181c-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="f181c-326">Si hello erreur persiste, vérifiez si vous disposez de privilèges suffisants dans hello correspondant ITSM produit toomake hello de connexion.</span><span class="sxs-lookup"><span data-stu-id="f181c-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="f181c-327">En cas de Service Manager, vérifiez que hello Web application est déployée avec succès et que la connexion hybride est créée.</span><span class="sxs-lookup"><span data-stu-id="f181c-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="f181c-328">tooverify hello connexion est correctement établie avec ordinateur de Service Manager local hello, visitez les URL de l’application hello Web comme indiqué dans la documentation hello de fabrication hello [connexion hybride](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="f181c-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="f181c-329">Si les données issues de ServiceNow ne sont pas mise en route synchronisées dans OMS, assurez-vous qu’une instance ServiceNow hello n’est pas en sommeil.</span><span class="sxs-lookup"><span data-stu-id="f181c-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="f181c-330">Cela peut être plus tard dans hello instances ServiceNow Dev, lorsqu’il est inactif.</span><span class="sxs-lookup"><span data-stu-id="f181c-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="f181c-331">Else, signaler un problème technique hello.</span><span class="sxs-lookup"><span data-stu-id="f181c-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="f181c-332">Si les alertes sont mise en route déclenchés à partir d’OMS, mais ne sont pas des éléments de travail créé dans ITSM produits ou de configuration ne pas obtenir les éléments toowork de créé/lié ou pour des informations générales, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f181c-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="f181c-333">Solution de connecteur de gestion des services informatiques dans le portail OMS peut être utilisé tooget un récapitulatif des connexions/le travail des éléments/ordinateurs, etc.. Cliquez sur le message d’erreur hello dans le panneau d’état hello, accédez trop**recherche de journal** et afficher hello connexion qui possède l’erreur de hello dans le message d’erreur hello à l’aide des détails de hello.</span><span class="sxs-lookup"><span data-stu-id="f181c-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="f181c-334">Vous pouvez afficher directement les hello erreurs/informations Bonjour **recherche de journal** à l’aide de la page *Type = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="f181c-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="f181c-335">Résoudre les problèmes de déploiement de l’application web Service Manager</span><span class="sxs-lookup"><span data-stu-id="f181c-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="f181c-336">En cas de tout problème avec le déploiement de l’application web, assurez-vous d’avoir des autorisations suffisantes dans l’abonnement de hello mentionné toocreate/déployer des ressources.</span><span class="sxs-lookup"><span data-stu-id="f181c-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="f181c-337">Si **tooinstance d’un objet exclut la référence d’objet** message d’erreur apparaît lors de l’exécution hello [script](log-analytics-itsmc-service-manager-script.md) vous assurer que vous avez entré des valeurs valides sous **Configuration de l’utilisateur**section.</span><span class="sxs-lookup"><span data-stu-id="f181c-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="f181c-338">Si vous ne parvenez pas d’espace de noms relais toocreate service bus, vérifiez que hello requis de fournisseur de ressources est inscrit dans l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="f181c-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="f181c-339">Si ne pas inscrit, le créer manuellement à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f181c-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="f181c-340">Vous pouvez également créer tandis que [création de la connexion hybride hello](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f181c-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="f181c-341">Nous contacter</span><span class="sxs-lookup"><span data-stu-id="f181c-341">Contact us</span></span>

<span data-ttu-id="f181c-342">Pour toutes les requêtes ou des commentaires sur le connecteur de gestion du Service informatique de hello, contactez-nous à l’adresse [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f181c-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f181c-343">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f181c-343">Next steps</span></span>
<span data-ttu-id="f181c-344">[Ajouter tooIT de produits/services ITSM connecteur de Service Management](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="f181c-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
