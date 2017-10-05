---
title: IT Service Management Connector dans OMS | Microsoft Docs
description: "Utilisez IT Service Management Connector pour surveiller et gérer de manière centralisée les éléments de travail ITSM dans OMS, et résoudre rapidement les problèmes éventuels."
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
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="bcd2d-103">Gérer de manière centralisée les éléments de travail ITSM à l’aide d’IT Service Management Connector (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="bcd2d-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Symbole d’IT Service Management Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="bcd2d-105">Vous pouvez utiliser IT Service Management Connector (ITSMC) dans OMS Log Analytics pour surveiller et gérer de manière centralisée les éléments de travail de vos produits/services ITSM.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-105">You can use the IT Service Management Connector (ITSMC) in OMS Log Analytics to centrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="bcd2d-106">IT Service Management Connector intègre vos produits et services de gestion des services informatiques (ITSM) existants avec OMS Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-106">The IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="bcd2d-107">La solution offre une intégration bidirectionnelle avec les produits/services ITSM afin de fournir aux utilisateurs OMS une option pour créer des incidents, des alertes ou des événements dans une solution ITSM.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-107">The solution has bidirectional integration with ITSM products/services, where it provides the OMS users an option to create incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="bcd2d-108">Le connecteur importe également des données telles que les incidents et les demandes de modification à partir de la solution ITSM vers OMS Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-108">The connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="bcd2d-109">IT Service Management Connector vous offre de nombreuses possibilités :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="bcd2d-110">Surveiller et gérer de manière centralisée des éléments de travail pour les produits/services ITSM utilisés au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="bcd2d-111">Créer des éléments de travail ITSM (tels que des alertes, des événements et des incidents) dans ITSM à partir des alertes OMS et via la fonctionnalité de recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="bcd2d-112">Lire les incidents et les demandes de modification de votre solution ITSM et les mettre en corrélation avec les données de journal pertinentes dans l’espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="bcd2d-113">Identifier les événements inattendus et inhabituels et les résoudre avant même que les utilisateurs ne les signalent au support technique.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-113">Find any unexpected and unusual events and resolve them, even before the end users call and report them to the helpdesk.</span></span>
  - <span data-ttu-id="bcd2d-114">Importer des données d’éléments de travail dans Log Analytics et créer des rapports d’indicateurs de performance clés.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="bcd2d-115">Grâce à ces rapports, vous pouvez identifier, analyser et agir sur plusieurs éléments importants tels que l’évaluation des programmes malveillants.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="bcd2d-116">Afficher des tableaux de bord spécialement conçus pour fournir des informations plus détaillées sur les incidents, les demandes de modification et les systèmes concernés.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="bcd2d-117">Résoudre plus rapidement les problèmes en mettant les données en corrélation avec d’autres solutions de gestion de l’espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-117">Troubleshoot faster by correlating with other management solutions in the Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bcd2d-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bcd2d-118">Prerequisites</span></span>

<span data-ttu-id="bcd2d-119">Pour importer les éléments de travail ITSM dans OMS Log Analytics, la solution requiert une connexion entre le connecteur IT Service Management Connector dans OMS et le produit/service ITSM à partir duquel vous importez les éléments de travail.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-119">To import the ITSM work items into OMS Log Analytics, the solution requires a connection between the IT Service Management Connector in the OMS and the IT SM product/service from which you import the work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="bcd2d-120">Configuration</span><span class="sxs-lookup"><span data-stu-id="bcd2d-120">Configuration</span></span>

<span data-ttu-id="bcd2d-121">Ajoutez la solution IT Service Management Connector dans votre espace de travail OMS en suivant la procédure décrite dans [Ajouter des solutions Log Analytics à partir de la galerie de solutions](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="bcd2d-121">Add the IT Service Management Connector solution to your OMS work space, using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="bcd2d-122">Vignette IT Service Management Connector apparaissant dans la galerie de solutions :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-122">IT Service Management Connector tile as you see in the Solutions gallery:</span></span>

![vignette du connecteur](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="bcd2d-124">Une fois ajoutée, la solution IT Service Management Connector s’affiche sous **OMS** > **Paramètres** > **Sources connectées**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-124">After successful addition, you will see the IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC connecté](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="bcd2d-126">Par défaut, IT Service Management Connector actualise les données de la connexion une fois dans toutes les 24 heures.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-126">By default, the IT Service Management Connector refreshes the connection's data once in every 24 hours.</span></span> <span data-ttu-id="bcd2d-127">Pour actualiser instantanément les données de votre connexion en rapport avec des modifications ou mises à jour de modèle que vous apportez, cliquez sur le bouton d’actualisation en regard de votre connexion.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-127">To refresh your connection's data instantly for any edits or template updates that you make, click the refresh button displayed next to your connection.</span></span>

 ![Actualisation d’ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="bcd2d-129">Packs d’administration</span><span class="sxs-lookup"><span data-stu-id="bcd2d-129">Management packs</span></span>
<span data-ttu-id="bcd2d-130">Cette solution ne requiert aucun pack d’administration.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="bcd2d-131">Sources connectées</span><span class="sxs-lookup"><span data-stu-id="bcd2d-131">Connected sources</span></span>

<span data-ttu-id="bcd2d-132">Les produits/services ITSM suivants sont pris en charge par le connecteur IT Service Management Connector :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-132">The following ITSM products/services are supported by the IT Service Management Connector:</span></span>

- [<span data-ttu-id="bcd2d-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="bcd2d-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="bcd2d-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="bcd2d-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="bcd2d-135">Provance</span><span class="sxs-lookup"><span data-stu-id="bcd2d-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="bcd2d-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="bcd2d-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a><span data-ttu-id="bcd2d-137">Utilisation de la solution</span><span class="sxs-lookup"><span data-stu-id="bcd2d-137">Using the solution</span></span>

<span data-ttu-id="bcd2d-138">Une fois que vous avez connecté la solution OMS IT Service Management Connector à votre service ITSM, le service Log Analytics commence à collecter des données à partir des services/produits ITSM connectés.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-138">Once you connect the OMS IT Service Management Connector with your ITSM service, the Log Analytics services starts gathering the data from the connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="bcd2d-139">Les données importées par la solution IT Service Management Connector s’affichent dans Log Analytics en tant qu’événements nommés **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="bcd2d-140">Chaque événement contient un champ nommé **ServiceDeskWorkItemType_s**</span><span class="sxs-lookup"><span data-stu-id="bcd2d-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="bcd2d-141">qui est défini sur Incident ou Demande de modification selon les données de l’élément de travail contenues dans l’événement **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-141">which can take its value as incident, or change request, depending on the work item data contained in the **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="bcd2d-142">Données d’entrée</span><span class="sxs-lookup"><span data-stu-id="bcd2d-142">Input data</span></span>
<span data-ttu-id="bcd2d-143">Éléments de travail importés à partir des produits/services ITSM.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-143">Work items imported from the ITSM products/services.</span></span>

<span data-ttu-id="bcd2d-144">Les informations suivantes présentent des exemples de données collectées par IT Service Management Connector :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-144">The following information shows examples of data gathered by the IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="bcd2d-145">Selon le type d’élément de travail importé dans Log Analytics, l’événement **ServiceDesk_CL** contient les champs suivants :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-145">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="bcd2d-146">**Élément de travail :** **Incidents**</span><span class="sxs-lookup"><span data-stu-id="bcd2d-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="bcd2d-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="bcd2d-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="bcd2d-148">**Champs**</span><span class="sxs-lookup"><span data-stu-id="bcd2d-148">**Fields**</span></span>

- <span data-ttu-id="bcd2d-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="bcd2d-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="bcd2d-150">ID du service d’assistance</span><span class="sxs-lookup"><span data-stu-id="bcd2d-150">Service Desk ID</span></span>
- <span data-ttu-id="bcd2d-151">State</span><span class="sxs-lookup"><span data-stu-id="bcd2d-151">State</span></span>
- <span data-ttu-id="bcd2d-152">Urgence</span><span class="sxs-lookup"><span data-stu-id="bcd2d-152">Urgency</span></span>
- <span data-ttu-id="bcd2d-153">Impact</span><span class="sxs-lookup"><span data-stu-id="bcd2d-153">Impact</span></span>
- <span data-ttu-id="bcd2d-154">Priorité</span><span class="sxs-lookup"><span data-stu-id="bcd2d-154">Priority</span></span>
- <span data-ttu-id="bcd2d-155">Escalade</span><span class="sxs-lookup"><span data-stu-id="bcd2d-155">Escalation</span></span>
- <span data-ttu-id="bcd2d-156">Créé par</span><span class="sxs-lookup"><span data-stu-id="bcd2d-156">Created By</span></span>
- <span data-ttu-id="bcd2d-157">Résolu par</span><span class="sxs-lookup"><span data-stu-id="bcd2d-157">Resolved By</span></span>
- <span data-ttu-id="bcd2d-158">Fermé par</span><span class="sxs-lookup"><span data-stu-id="bcd2d-158">Closed By</span></span>
- <span data-ttu-id="bcd2d-159">Source</span><span class="sxs-lookup"><span data-stu-id="bcd2d-159">Source</span></span>
- <span data-ttu-id="bcd2d-160">Affecté à</span><span class="sxs-lookup"><span data-stu-id="bcd2d-160">Assigned To</span></span>
- <span data-ttu-id="bcd2d-161">Catégorie</span><span class="sxs-lookup"><span data-stu-id="bcd2d-161">Category</span></span>
- <span data-ttu-id="bcd2d-162">Intitulé</span><span class="sxs-lookup"><span data-stu-id="bcd2d-162">Title</span></span>
- <span data-ttu-id="bcd2d-163">Description</span><span class="sxs-lookup"><span data-stu-id="bcd2d-163">Description</span></span>
- <span data-ttu-id="bcd2d-164">Date de création</span><span class="sxs-lookup"><span data-stu-id="bcd2d-164">Created Date</span></span>
- <span data-ttu-id="bcd2d-165">Date de fermeture</span><span class="sxs-lookup"><span data-stu-id="bcd2d-165">Closed Date</span></span>
- <span data-ttu-id="bcd2d-166">Date de résolution</span><span class="sxs-lookup"><span data-stu-id="bcd2d-166">Resolved Date</span></span>
- <span data-ttu-id="bcd2d-167">Date de dernière modification</span><span class="sxs-lookup"><span data-stu-id="bcd2d-167">Last Modified Date</span></span>
- <span data-ttu-id="bcd2d-168">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="bcd2d-168">Computer</span></span>


<span data-ttu-id="bcd2d-169">**Élément de travail :** **Demandes de modification**</span><span class="sxs-lookup"><span data-stu-id="bcd2d-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="bcd2d-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="bcd2d-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="bcd2d-171">**Champs**</span><span class="sxs-lookup"><span data-stu-id="bcd2d-171">**Fields**</span></span>
- <span data-ttu-id="bcd2d-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="bcd2d-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="bcd2d-173">ID du service d’assistance</span><span class="sxs-lookup"><span data-stu-id="bcd2d-173">Service Desk ID</span></span>
- <span data-ttu-id="bcd2d-174">Créé par</span><span class="sxs-lookup"><span data-stu-id="bcd2d-174">Created By</span></span>
- <span data-ttu-id="bcd2d-175">Fermé par</span><span class="sxs-lookup"><span data-stu-id="bcd2d-175">Closed By</span></span>
- <span data-ttu-id="bcd2d-176">Source</span><span class="sxs-lookup"><span data-stu-id="bcd2d-176">Source</span></span>
- <span data-ttu-id="bcd2d-177">Affecté à</span><span class="sxs-lookup"><span data-stu-id="bcd2d-177">Assigned To</span></span>
- <span data-ttu-id="bcd2d-178">Intitulé</span><span class="sxs-lookup"><span data-stu-id="bcd2d-178">Title</span></span>
- <span data-ttu-id="bcd2d-179">Type</span><span class="sxs-lookup"><span data-stu-id="bcd2d-179">Type</span></span>
- <span data-ttu-id="bcd2d-180">Catégorie</span><span class="sxs-lookup"><span data-stu-id="bcd2d-180">Category</span></span>
- <span data-ttu-id="bcd2d-181">State</span><span class="sxs-lookup"><span data-stu-id="bcd2d-181">State</span></span>
- <span data-ttu-id="bcd2d-182">Escalade</span><span class="sxs-lookup"><span data-stu-id="bcd2d-182">Escalation</span></span>
- <span data-ttu-id="bcd2d-183">État conflictuel</span><span class="sxs-lookup"><span data-stu-id="bcd2d-183">Conflict Status</span></span>
- <span data-ttu-id="bcd2d-184">Urgence</span><span class="sxs-lookup"><span data-stu-id="bcd2d-184">Urgency</span></span>
- <span data-ttu-id="bcd2d-185">Priorité</span><span class="sxs-lookup"><span data-stu-id="bcd2d-185">Priority</span></span>
- <span data-ttu-id="bcd2d-186">Risque</span><span class="sxs-lookup"><span data-stu-id="bcd2d-186">Risk</span></span>
- <span data-ttu-id="bcd2d-187">Impact</span><span class="sxs-lookup"><span data-stu-id="bcd2d-187">Impact</span></span>
- <span data-ttu-id="bcd2d-188">Affecté à</span><span class="sxs-lookup"><span data-stu-id="bcd2d-188">Assigned To</span></span>
- <span data-ttu-id="bcd2d-189">Date de création</span><span class="sxs-lookup"><span data-stu-id="bcd2d-189">Created Date</span></span>
- <span data-ttu-id="bcd2d-190">Date de fermeture</span><span class="sxs-lookup"><span data-stu-id="bcd2d-190">Closed Date</span></span>
- <span data-ttu-id="bcd2d-191">Date de dernière modification</span><span class="sxs-lookup"><span data-stu-id="bcd2d-191">Last Modified Date</span></span>
- <span data-ttu-id="bcd2d-192">Date de la demande</span><span class="sxs-lookup"><span data-stu-id="bcd2d-192">Requested Date</span></span>
- <span data-ttu-id="bcd2d-193">Date de début prévue</span><span class="sxs-lookup"><span data-stu-id="bcd2d-193">Planned Start Date</span></span>
- <span data-ttu-id="bcd2d-194">Date de fin prévue</span><span class="sxs-lookup"><span data-stu-id="bcd2d-194">Planned End Date</span></span>
- <span data-ttu-id="bcd2d-195">Date de début du travail</span><span class="sxs-lookup"><span data-stu-id="bcd2d-195">Work Start Date</span></span>
- <span data-ttu-id="bcd2d-196">Date de fin du travail</span><span class="sxs-lookup"><span data-stu-id="bcd2d-196">Work End Date</span></span>
- <span data-ttu-id="bcd2d-197">Description</span><span class="sxs-lookup"><span data-stu-id="bcd2d-197">Description</span></span>
- <span data-ttu-id="bcd2d-198">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="bcd2d-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="bcd2d-199">Données de sortie pour un incident ServiceNow</span><span class="sxs-lookup"><span data-stu-id="bcd2d-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="bcd2d-200">Champ OMS</span><span class="sxs-lookup"><span data-stu-id="bcd2d-200">OMS field</span></span> | <span data-ttu-id="bcd2d-201">Champ ITSM</span><span class="sxs-lookup"><span data-stu-id="bcd2d-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="bcd2d-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-202">ServiceDeskId_s</span></span>| <span data-ttu-id="bcd2d-203">Number</span><span class="sxs-lookup"><span data-stu-id="bcd2d-203">Number</span></span> |
| <span data-ttu-id="bcd2d-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-204">IncidentState_s</span></span> | <span data-ttu-id="bcd2d-205">State</span><span class="sxs-lookup"><span data-stu-id="bcd2d-205">State</span></span> |
| <span data-ttu-id="bcd2d-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-206">Urgency_s</span></span> |<span data-ttu-id="bcd2d-207">Urgence</span><span class="sxs-lookup"><span data-stu-id="bcd2d-207">Urgency</span></span> |
| <span data-ttu-id="bcd2d-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-208">Impact_s</span></span> |<span data-ttu-id="bcd2d-209">Impact</span><span class="sxs-lookup"><span data-stu-id="bcd2d-209">Impact</span></span>|
| <span data-ttu-id="bcd2d-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-210">Priority_s</span></span> | <span data-ttu-id="bcd2d-211">Priorité</span><span class="sxs-lookup"><span data-stu-id="bcd2d-211">Priority</span></span> |
| <span data-ttu-id="bcd2d-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-212">CreatedBy_s</span></span> | <span data-ttu-id="bcd2d-213">Ouvert par</span><span class="sxs-lookup"><span data-stu-id="bcd2d-213">Opened by</span></span> |
| <span data-ttu-id="bcd2d-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-214">ResolvedBy_s</span></span> | <span data-ttu-id="bcd2d-215">Résolu par</span><span class="sxs-lookup"><span data-stu-id="bcd2d-215">Resolved by</span></span>|
| <span data-ttu-id="bcd2d-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-216">ClosedBy_s</span></span>  | <span data-ttu-id="bcd2d-217">Fermé par</span><span class="sxs-lookup"><span data-stu-id="bcd2d-217">Closed by</span></span> |
| <span data-ttu-id="bcd2d-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-218">Source_s</span></span>| <span data-ttu-id="bcd2d-219">Type de contact</span><span class="sxs-lookup"><span data-stu-id="bcd2d-219">Contact type</span></span> |
| <span data-ttu-id="bcd2d-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-220">AssignedTo_s</span></span> | <span data-ttu-id="bcd2d-221">Affecté à</span><span class="sxs-lookup"><span data-stu-id="bcd2d-221">Assigned to</span></span>  |
| <span data-ttu-id="bcd2d-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-222">Category_s</span></span> | <span data-ttu-id="bcd2d-223">Catégorie</span><span class="sxs-lookup"><span data-stu-id="bcd2d-223">Category</span></span> |
| <span data-ttu-id="bcd2d-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-224">Title_s</span></span>|  <span data-ttu-id="bcd2d-225">Brève description</span><span class="sxs-lookup"><span data-stu-id="bcd2d-225">Short description</span></span> |
| <span data-ttu-id="bcd2d-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-226">Description_s</span></span>|  <span data-ttu-id="bcd2d-227">Remarques</span><span class="sxs-lookup"><span data-stu-id="bcd2d-227">Notes</span></span> |
| <span data-ttu-id="bcd2d-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="bcd2d-228">CreatedDate_t</span></span>|  <span data-ttu-id="bcd2d-229">Ouvert</span><span class="sxs-lookup"><span data-stu-id="bcd2d-229">Opened</span></span> |
| <span data-ttu-id="bcd2d-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="bcd2d-230">ClosedDate_t</span></span>| <span data-ttu-id="bcd2d-231">Fermé</span><span class="sxs-lookup"><span data-stu-id="bcd2d-231">closed</span></span>|
| <span data-ttu-id="bcd2d-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="bcd2d-232">ResolvedDate_t</span></span>|<span data-ttu-id="bcd2d-233">Résolu</span><span class="sxs-lookup"><span data-stu-id="bcd2d-233">Resolved</span></span>|
| <span data-ttu-id="bcd2d-234">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="bcd2d-234">Computer</span></span>  | <span data-ttu-id="bcd2d-235">Élément de configuration</span><span class="sxs-lookup"><span data-stu-id="bcd2d-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="bcd2d-236">Données de sortie pour une demande de modification ServiceNow</span><span class="sxs-lookup"><span data-stu-id="bcd2d-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="bcd2d-237">Champ OMS</span><span class="sxs-lookup"><span data-stu-id="bcd2d-237">OMS field</span></span> | <span data-ttu-id="bcd2d-238">Champ ITSM</span><span class="sxs-lookup"><span data-stu-id="bcd2d-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="bcd2d-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-239">ServiceDeskId_s</span></span>| <span data-ttu-id="bcd2d-240">Number</span><span class="sxs-lookup"><span data-stu-id="bcd2d-240">Number</span></span> |
| <span data-ttu-id="bcd2d-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-241">CreatedBy_s</span></span> | <span data-ttu-id="bcd2d-242">Demandé par</span><span class="sxs-lookup"><span data-stu-id="bcd2d-242">Requested by</span></span> |
| <span data-ttu-id="bcd2d-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-243">ClosedBy_s</span></span> | <span data-ttu-id="bcd2d-244">Fermé par</span><span class="sxs-lookup"><span data-stu-id="bcd2d-244">Closed by</span></span> |
| <span data-ttu-id="bcd2d-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-245">AssignedTo_s</span></span> | <span data-ttu-id="bcd2d-246">Affecté à</span><span class="sxs-lookup"><span data-stu-id="bcd2d-246">Assigned to</span></span>  |
| <span data-ttu-id="bcd2d-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-247">Title_s</span></span>|  <span data-ttu-id="bcd2d-248">Brève description</span><span class="sxs-lookup"><span data-stu-id="bcd2d-248">Short description</span></span> |
| <span data-ttu-id="bcd2d-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-249">Type_s</span></span>|  <span data-ttu-id="bcd2d-250">Type</span><span class="sxs-lookup"><span data-stu-id="bcd2d-250">Type</span></span> |
| <span data-ttu-id="bcd2d-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-251">Category_s</span></span>|  <span data-ttu-id="bcd2d-252">Catégorie</span><span class="sxs-lookup"><span data-stu-id="bcd2d-252">Catgory</span></span> |
| <span data-ttu-id="bcd2d-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-253">CRState_s</span></span>|  <span data-ttu-id="bcd2d-254">State</span><span class="sxs-lookup"><span data-stu-id="bcd2d-254">State</span></span>|
| <span data-ttu-id="bcd2d-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-255">Urgency_s</span></span>|  <span data-ttu-id="bcd2d-256">Urgence</span><span class="sxs-lookup"><span data-stu-id="bcd2d-256">Urgency</span></span> |
| <span data-ttu-id="bcd2d-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-257">Priority_s</span></span>| <span data-ttu-id="bcd2d-258">Priorité</span><span class="sxs-lookup"><span data-stu-id="bcd2d-258">Priority</span></span>|
| <span data-ttu-id="bcd2d-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-259">Risk_s</span></span>| <span data-ttu-id="bcd2d-260">Risque</span><span class="sxs-lookup"><span data-stu-id="bcd2d-260">Risk</span></span>|
| <span data-ttu-id="bcd2d-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-261">Impact_s</span></span>| <span data-ttu-id="bcd2d-262">Impact</span><span class="sxs-lookup"><span data-stu-id="bcd2d-262">Impact</span></span>|
| <span data-ttu-id="bcd2d-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="bcd2d-263">RequestedDate_t</span></span>  | <span data-ttu-id="bcd2d-264">Date demandée</span><span class="sxs-lookup"><span data-stu-id="bcd2d-264">Requested by date</span></span> |
| <span data-ttu-id="bcd2d-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="bcd2d-265">ClosedDate_t</span></span> | <span data-ttu-id="bcd2d-266">Date de fermeture</span><span class="sxs-lookup"><span data-stu-id="bcd2d-266">Closed date</span></span> |
| <span data-ttu-id="bcd2d-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="bcd2d-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="bcd2d-268">Date de début prévue</span><span class="sxs-lookup"><span data-stu-id="bcd2d-268">Planned start date</span></span> |
| <span data-ttu-id="bcd2d-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="bcd2d-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="bcd2d-270">Date de fin prévue</span><span class="sxs-lookup"><span data-stu-id="bcd2d-270">Planned end date</span></span> |
| <span data-ttu-id="bcd2d-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="bcd2d-271">WorkStartDate_t</span></span>  | <span data-ttu-id="bcd2d-272">Date de début réelle</span><span class="sxs-lookup"><span data-stu-id="bcd2d-272">Actual start date</span></span> |
| <span data-ttu-id="bcd2d-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="bcd2d-273">WorkEndDate_t</span></span> | <span data-ttu-id="bcd2d-274">Date de fin réelle</span><span class="sxs-lookup"><span data-stu-id="bcd2d-274">Actual end date</span></span>|
| <span data-ttu-id="bcd2d-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="bcd2d-275">Description_s</span></span> | <span data-ttu-id="bcd2d-276">Description</span><span class="sxs-lookup"><span data-stu-id="bcd2d-276">Description</span></span> |
| <span data-ttu-id="bcd2d-277">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="bcd2d-277">Computer</span></span>  | <span data-ttu-id="bcd2d-278">Élément de configuration</span><span class="sxs-lookup"><span data-stu-id="bcd2d-278">Configuration Item</span></span> |

<span data-ttu-id="bcd2d-279">**Exemple d’écran Log Analytics pour les données ITSM :**</span><span class="sxs-lookup"><span data-stu-id="bcd2d-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Écran Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="bcd2d-281">IT Service Management Connector – intégration avec d’autres solutions OMS</span><span class="sxs-lookup"><span data-stu-id="bcd2d-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="bcd2d-282">IT Service Management Connector prend actuellement en charge l’intégration avec la solution Carte de service.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-282">IT Service Management Connector, currently supports integration with the Service Map solution.</span></span>

<span data-ttu-id="bcd2d-283">La solution Carte de service détecte automatiquement les composants d’application sur les systèmes Windows et Linux et mappe la communication entre les services.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-283">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="bcd2d-284">Elle vous permet d’afficher les serveurs comme des systèmes interconnectés qui fournissent des services critiques.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-284">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="bcd2d-285">Carte de service affiche les connexions entre les serveurs, les processus et les ports sur n’importe quelle architecture connectée à TCP, sans configuration requise autre que l’installation d’un agent.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="bcd2d-286">Pour en savoir plus : [Carte de service](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="bcd2d-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="bcd2d-287">Grâce à cette intégration, vous pouvez afficher les éléments de service d’assistance créés dans les solutions ITSM comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-287">With this integration, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![<span data-ttu-id="bcd2d-288">Solution intégrée</span><span class="sxs-lookup"><span data-stu-id="bcd2d-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="bcd2d-289">Créer des éléments de travail ITSM pour des alertes OMS</span><span class="sxs-lookup"><span data-stu-id="bcd2d-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="bcd2d-290">Pour les alertes OMS, vous pouvez créer des éléments de travail associés dans les sources ITSM connectées.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-290">For the OMS alerts, you can create associated work items in the connected ITSM sources.</span></span>  <span data-ttu-id="bcd2d-291">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-291">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="bcd2d-292">Dans la fenêtre **Recherche dans les journaux**, exécutez une requête de recherche dans les journaux pour afficher les données.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-292">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="bcd2d-293">Les résultats de la requête correspondent aux sources des éléments de travail.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-293">Query results are the source for work items.</span></span>
2. <span data-ttu-id="bcd2d-294">Dans **Recherche dans les journaux**, cliquez sur **Alerte** pour ouvrir la page **Ajouter une règle d’alerte**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-294">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Écran Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="bcd2d-296">Dans la fenêtre **Ajouter une règle d’alerte**, spécifiez les champs **Nom**, **Gravité**, **Requête de recherche** et **Critères d’alerte** (fenêtre de temps/mesures métriques).</span><span class="sxs-lookup"><span data-stu-id="bcd2d-296">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="bcd2d-297">Sélectionnez **Oui** pour **Actions ITSM**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="bcd2d-298">Sélectionnez votre connexion ITSM dans la liste **Sélectionner une connexion**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-298">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="bcd2d-299">Spécifiez les informations requises.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-299">Provide the details as required.</span></span>
7. <span data-ttu-id="bcd2d-300">Pour créer un élément de travail distinct pour chaque entrée de journal de cette alerte, cochez la case **Créer des éléments de travail distincts pour chaque entrée de journal**</span><span class="sxs-lookup"><span data-stu-id="bcd2d-300">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="bcd2d-301">Ou</span><span class="sxs-lookup"><span data-stu-id="bcd2d-301">Or</span></span>

    <span data-ttu-id="bcd2d-302">laissez cette case décochée pour créer un seul élément de travail pour l’ensemble des entrées de journal associées à cette alerte.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-302">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="bcd2d-303">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-303">Click **Save**.</span></span>

<span data-ttu-id="bcd2d-304">L’alerte OMS est créée sous **Alertes**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-304">The OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="bcd2d-305">Les éléments de travail de la connexion ITSM correspondante sont créés lorsque les critères de l’alerte spécifiée sont remplis.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-305">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="bcd2d-306">Créer des éléments de travail ITSM à partir de journaux OMS</span><span class="sxs-lookup"><span data-stu-id="bcd2d-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="bcd2d-307">Vous pouvez créer des éléments de travail dans les sources ITSM connectées à l’aide de la fonctionnalité de recherche dans les journaux d’OMS.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-307">You can create work items in the connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="bcd2d-308">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-308">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="bcd2d-309">Sous **Recherche dans les journaux**, recherchez les données requises, sélectionnez les informations détaillées, puis cliquez sur **Créer un élément de travail**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-309">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="bcd2d-310">La fenêtre **Créer un élément de travail ITSM** s’affiche :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-310">The **Create ITSM Work item** window appears:</span></span>

    ![Écran Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="bcd2d-312">Ajoutez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-312">Add the following details:</span></span>

  - <span data-ttu-id="bcd2d-313">**Titre de l’élément de travail** : titre de l’élément de travail.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-313">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="bcd2d-314">**Description de l’élément de travail** : description du nouvel élément de travail.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-314">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="bcd2d-315">**Ordinateur concerné** : nom de l’ordinateur sur lequel les données de journal ont été trouvées.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-315">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="bcd2d-316">**Sélectionner une connexion** : connexion ITSM dans laquelle vous souhaitez créer cet élément de travail.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-316">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="bcd2d-317">**Élément de travail** : type d’élément de travail.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="bcd2d-318">Pour utiliser un modèle d’élément de travail existant pour un incident, cliquez sur **Oui** sous **Générer l’élément de travail en fonction du modèle**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-318">To use an existing work item template for an incident, click **Yes** under **Generate work item based on the template** option and then click **Create**.</span></span>

    <span data-ttu-id="bcd2d-319">Ou,</span><span class="sxs-lookup"><span data-stu-id="bcd2d-319">Or,</span></span>

    <span data-ttu-id="bcd2d-320">Cliquez sur **Non** si vous souhaitez fournir des valeurs personnalisées.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-320">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="bcd2d-321">Indiquez les valeurs appropriées dans les zones de texte **Type de contact**, **Impact**, **Urgence**, **Catégorie** et **Sous-catégorie**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-321">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="bcd2d-322">L’élément de travail sera créé dans ITSM, que vous pouvez également afficher dans OMS.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-322">The work item will be created in the ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="bcd2d-323">Dépanner des connexions ITSM dans OMS</span><span class="sxs-lookup"><span data-stu-id="bcd2d-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="bcd2d-324">Si la connexion échoue à partir de l’interface utilisateur d’une source connectée et que le message **Erreur lors de l’enregistrement de la connexion** s’affiche, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-324">If connection fails from connected source's UI and you get the **Error in saving connection** message, do the following:</span></span>
 - <span data-ttu-id="bcd2d-325">En cas de connexions ServiceNow, Cherwell et Provance, assurez-vous de que vous avez correctement entré les nom d’utilisateur/mot de passe et ID client/Clé secrète client pour chacune des connexions.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  the username/password and  client ID/client secret  for each of the connections.</span></span> <span data-ttu-id="bcd2d-326">Si l’erreur persiste, vérifiez si vous disposez de privilèges suffisants dans le produit ITSM correspondant pour établir la connexion.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-326">If the error persists, check if you have sufficient privileges  in the corresponding ITSM product to make the connection.</span></span>
 - <span data-ttu-id="bcd2d-327">Dans le cas de Service Manager, assurez-vous que l’application Web est correctement déployée et que la connexion hybride est créée.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-327">In case of Service Manager, ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="bcd2d-328">Pour vérifier que la connexion est établie avec l’ordinateur Service Manager local, accédez à l’URL de l’application web, comme décrit dans la documentation concernant l’établissement d’une [connexion hybride](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="bcd2d-328">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="bcd2d-329">Si les données de ServiceNow ne sont pas synchronisées dans OMS, vérifiez que l’instance ServiceNow n’est pas en état de veille.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-329">If data from ServiceNow is not getting synced in OMS, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="bcd2d-330">Cela peut se produire parfois dans les instances de ServiceNow Dev en cas d’inactivité.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-330">This might sometime happen in the ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="bcd2d-331">Autrement, signalez le problème.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-331">Else, report the issue.</span></span>
3.  <span data-ttu-id="bcd2d-332">Si des alertes sont déclenchées à partir d’OMS mais que des éléments de travail ne sont pas créés dans le produit ITSM, ou si des éléments de configuration ne sont pas créés/liés à des éléments de travail, ou pour des informations générales, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcd2d-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked to work items or for any generic information, do the following:</span></span>
 -  <span data-ttu-id="bcd2d-333">La solution IT Service Management Connector dans le portail OMS pourrait être utilisée pour obtenir un résumé des connexions, éléments de travail, ordinateurs etc. Cliquez sur le message d’erreur dans le panneau d’état, accédez à **Recherche dans les journaux**, puis affichez la connexion concernée en utilisant les détails fournis dans le message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-333">IT Service Management Connector solution in OMS portal could be used to get a summary of connections/work items/computers etc. Click the error message in the status blade, navigate to **Log Search** and view the connection that has the error by using the details in the error message.</span></span>
 - <span data-ttu-id="bcd2d-334">Vous pouvez afficher les erreurs et informations associées directement dans la page **Recherche dans les journaux** en entrant *Type = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-334">you can directly view the errors/related information in the **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="bcd2d-335">Résoudre les problèmes de déploiement de l’application web Service Manager</span><span class="sxs-lookup"><span data-stu-id="bcd2d-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="bcd2d-336">En cas de problème de déploiement de l’application web, vérifiez que vous disposez des autorisations suffisantes dans l’abonnement mentionné pour créer/déployer des ressources.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="bcd2d-337">Si le message d’erreur **Référence d’objet non définie sur une instance d’un objet** s’affiche lors de l’exécution du [script](log-analytics-itsmc-service-manager-script.md), vérifiez que vous avez entré des valeurs valides dans la section **Configuration utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-337">If **Object reference not set to instance of an object** error message appears while running the [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="bcd2d-338">Si vous échouez à créer l’espace de noms du relais Service Bus, vérifiez que le fournisseur de ressources requis est inscrit dans l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-338">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="bcd2d-339">S’il n’est pas inscrit, créez-le manuellement à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-339">If not registered, manually create it from the Azure portal.</span></span> <span data-ttu-id="bcd2d-340">Vous pouvez également le créer lors de la [création de la connexion hybride](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd2d-340">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="bcd2d-341">Nous contacter</span><span class="sxs-lookup"><span data-stu-id="bcd2d-341">Contact us</span></span>

<span data-ttu-id="bcd2d-342">Pour toute question ou tout commentaire à propos de la solution IT Service Management Connector, contactez-nous à l’adresse [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="bcd2d-342">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcd2d-343">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcd2d-343">Next steps</span></span>
<span data-ttu-id="bcd2d-344">[Ajouter des produits/services ITSM à IT Service Management Connector](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="bcd2d-344">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
