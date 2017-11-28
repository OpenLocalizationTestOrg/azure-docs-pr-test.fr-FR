---
title: "Récupération d’urgence de compte d’intégration B2B - Azure Logic Apps | Microsoft Docs"
description: "Récupération d’urgence Logic Apps B2B"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 4896d9da456bcc17b1a4d92259ef3d57f8575d8b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="6e6ab-103">Récupération d’urgence inter-régions Logic Apps B2B</span><span class="sxs-lookup"><span data-stu-id="6e6ab-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="6e6ab-104">Les charges de travail B2B impliquent des transactions monétaires telles que des commandes et des factures.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="6e6ab-105">Pour les entreprises, une récupération rapide est essentielle pour respecter les SLA de niveau entreprise convenus avec leurs partenaires lors d’un sinistre.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-105">During a disaster event, it's critical for a business to quickly recover to meet the business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="6e6ab-106">Cet article montre comment créer un plan de continuité des activités pour les charges de travail B2B.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-106">This article demonstrates how to build a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="6e6ab-107">Préparation à la récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="6e6ab-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="6e6ab-108">Basculer vers la région secondaire lors d’un sinistre</span><span class="sxs-lookup"><span data-stu-id="6e6ab-108">Fail over to secondary region during a disaster event</span></span> 
* <span data-ttu-id="6e6ab-109">Revenir à la région primaire après sinistre</span><span class="sxs-lookup"><span data-stu-id="6e6ab-109">Fall back to primary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="6e6ab-110">Préparation à la récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="6e6ab-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="6e6ab-111">Identifiez une région secondaire et créer un [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) dans cette région.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in the secondary region.</span></span>

2. <span data-ttu-id="6e6ab-112">Ajoutez des partenaires, des schémas et des contrats pour les flux de messages requis où l’état d’exécution doit être répliqué sur le compte d’intégration de la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-112">Add partners, schemas, and agreements for the required message flows where the run status needs to be replicated to secondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="6e6ab-113">Vérifiez la cohérence entre les régions dans la convention d’affectation de noms pour les artefacts de compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-113">Make sure there's consistency in the integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="6e6ab-114">Pour extraire l’état d’exécution de la région primaire, créez une application logique dans la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-114">To pull the run status from the primary region, create a logic app in the secondary region.</span></span> 

   <span data-ttu-id="6e6ab-115">L’application logique doit disposer d’un *déclencheur* et d’une *action*.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="6e6ab-116">Le déclencheur doit se connecter au compte d’intégration de la région primaire tandis que l’action doit se connecter au compte d’intégration de la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-116">The trigger should connect to primary region integration account, and the action should connect to secondary region integration account.</span></span> 
   <span data-ttu-id="6e6ab-117">Selon l’intervalle de temps, le déclencheur interroge la table d’état d’exécution de la région primaire et extrait les nouveaux enregistrements, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-117">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span></span> <span data-ttu-id="6e6ab-118">L’action les met à jour dans le compte d’intégration de la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-118">The action updates them to secondary region integration account.</span></span> 
   <span data-ttu-id="6e6ab-119">Cela permet d’obtenir un état de runtime incrémentiel depuis la région primaire vers la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-119">This helps to get incremental runtime status from primary region to secondary region.</span></span>

4. <span data-ttu-id="6e6ab-120">La continuité des activités dans le compte d’intégration Logic Apps est conçue pour prendre en charge des protocoles basés sur B2B : X12, AS2 et EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-120">Business continuity in Logic Apps integration account is designed to support based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="6e6ab-121">Pour une procédure détaillée, sélectionnez les liens correspondants.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-121">To find detailed steps, select the respective links.</span></span>

5. <span data-ttu-id="6e6ab-122">Il est recommandé de déployer toutes les ressources de la région primaire dans une région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-122">The recommendation is to deploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="6e6ab-123">Les ressources de la région primaire incluent Azure SQL Database ou Azure Cosmos DB, Azure Service Bus/Azure Event Hubs (utilisés pour la messagerie), la gestion des API Azure et la fonctionnalité Logic Apps d’Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and the Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="6e6ab-124">Établissez une connexion entre la région primaire et la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-124">Establish a connection from a primary region to a secondary region.</span></span> <span data-ttu-id="6e6ab-125">Pour extraire l’état d’exécution d’une région primaire, créez une application logique dans une région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-125">To pull the run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="6e6ab-126">L’application logique doit disposer d’un déclencheur et d’une action.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-126">The logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="6e6ab-127">Le déclencheur doit se connecter au compte d’intégration d’une région primaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-127">The trigger should connect to a primary region integration account.</span></span> 
   <span data-ttu-id="6e6ab-128">Le déclencheur doit se connecter au compte d’intégration d’une région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-128">The action should connect to a secondary region integration account.</span></span> 
   <span data-ttu-id="6e6ab-129">Selon l’intervalle de temps, le déclencheur interroge la table d’état d’exécution de la région primaire et extrait les nouveaux enregistrements, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-129">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span></span> 
   <span data-ttu-id="6e6ab-130">L’action les met à jour dans le compte d’intégration de la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-130">The action updates them to a secondary region integration account.</span></span> 
   <span data-ttu-id="6e6ab-131">Ce processus permet d’obtenir un état de runtime incrémentiel depuis la région primaire vers la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-131">This process helps to get incremental runtime status from the primary region to the secondary region.</span></span>

<span data-ttu-id="6e6ab-132">La continuité des activités dans le compte d’intégration Logic Apps prend en charge les protocoles B2B X12, AS2 et EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-132">Business continuity in a Logic Apps integration account provides support based on the B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="6e6ab-133">Pour obtenir des instructions détaillées sur l’utilisation de X12 et AS2, consultez les sections de cet articles consacrées à [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) et [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2).</span><span class="sxs-lookup"><span data-stu-id="6e6ab-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-to-a-secondary-region-during-a-disaster-event"></a><span data-ttu-id="6e6ab-134">Basculer vers une région secondaire lors d’un sinistre</span><span class="sxs-lookup"><span data-stu-id="6e6ab-134">Fail over to a secondary region during a disaster event</span></span>

<span data-ttu-id="6e6ab-135">Lors d’un sinistre, lorsque la région primaire n’est pas disponible pour la continuité des activités, dirigez le trafic vers la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-135">During a disaster event, when the primary region is not available for business continuity, direct traffic to the secondary region.</span></span> <span data-ttu-id="6e6ab-136">Une région secondaire permet à une entreprise de récupérer rapidement ses fonctions de manière à respecter ses objectifs de point de récupération et de temps de récupération convenus avec ses partenaires.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-136">A secondary region helps a business to recover functions quickly to meet the RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="6e6ab-137">Elle contribue en outre à réduire les efforts nécessaires pour basculer d’une région à l’autre.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-137">It also minimizes efforts to fail over from one region to another region.</span></span> 

<span data-ttu-id="6e6ab-138">Il existe une latence attendue lorsque des numéros de contrôle sont copiés depuis une région primaire vers une région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-138">There is an expected latency while copying control numbers from a primary region to a secondary region.</span></span> <span data-ttu-id="6e6ab-139">Pour éviter d’envoyer des numéros de contrôle générés en double aux partenaires lors d’un sinistre, il est recommandé d’augmenter les numéros de contrôle dans les accords de région secondaire au moyen [d’applets de commande PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="6e6ab-139">To avoid sending duplicate generated control numbers to partners during a disaster event, the recommendation is to increment the control numbers in the secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-to-a-primary-region-post-disaster-event"></a><span data-ttu-id="6e6ab-140">Revenir à une région primaire après un sinistre</span><span class="sxs-lookup"><span data-stu-id="6e6ab-140">Fall back to a primary region post-disaster event</span></span>

<span data-ttu-id="6e6ab-141">Pour revenir à une région primaire lorsqu’elle est de nouveau disponible, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e6ab-141">To fall back to a primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="6e6ab-142">Cessez d’accepter les messages des partenaires dans la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-142">Stop accepting messages from partners in the secondary region.</span></span>  

2. <span data-ttu-id="6e6ab-143">Augmentez les numéros de contrôle générés pour tous les accords de région primaire au moyen [d’applets de commande PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="6e6ab-143">Increment the generated control numbers for all the primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="6e6ab-144">Dirigez le trafic de la région secondaire vers la région primaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-144">Direct traffic from the secondary region to the primary region.</span></span>

4. <span data-ttu-id="6e6ab-145">Vérifiez que l’application logique créée dans la région secondaire pour extraire l’état d’exécution de la région primaire est activée.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-145">Check that the logic app created in the secondary region for pulling run status from the primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="6e6ab-146">X 12</span><span class="sxs-lookup"><span data-stu-id="6e6ab-146">X12</span></span> 

<span data-ttu-id="6e6ab-147">La continuité des activités pour les documents EDI X12 documents repose sur les numéros de contrôle :</span><span class="sxs-lookup"><span data-stu-id="6e6ab-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="6e6ab-148">Vous pouvez également utiliser le [modèle de démarrage rapide X12](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) pour créer des applications logiques.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-148">You can also use the [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) to create logic apps.</span></span> <span data-ttu-id="6e6ab-149">La création d’un compte d’intégration primaire et d’un compte d’intégration secondaire est nécessaire pour utiliser le modèle.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-149">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span> <span data-ttu-id="6e6ab-150">Le modèle permet de créer deux applications logiques, une pour les numéros de contrôle reçus et l’autre pour les numéros de contrôle générés.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-150">The template helps to create two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="6e6ab-151">Les déclencheurs et actions respectifs sont créés dans les applications logiques, ce qui permet de connecter le déclencheur connecté au compte d’intégration primaire et de connecter l’action au compte d’intégration secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-151">Respective triggers and actions are created in the logic apps, connecting the trigger to the primary integration account and the action to the secondary integration account.</span></span>

<span data-ttu-id="6e6ab-152">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="6e6ab-152">**Prerequisites**</span></span>

<span data-ttu-id="6e6ab-153">Pour activer la récupération d’urgence pour les messages entrants, sélectionnez les options de vérification de doublons dans les paramètres de réception de l’accord X12.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-153">To enable disaster recovery for inbound messages, select the duplicate check settings in the X12 agreement's Receive Settings.</span></span>

![Sélectionnez les paramètres de vérification des doublons](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="6e6ab-155">Créez une [application logique](../logic-apps/logic-apps-create-a-logic-app.md) dans la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="6e6ab-156">Lancez une recherche sur **X12** et sélectionnez **X12 - Lors de la modification d’un numéro de contrôle**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Recherchez X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="6e6ab-158">Le déclencheur vous invite à établir une connexion à un compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-158">The trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="6e6ab-159">Le déclencheur doit être connecté au compte d’intégration d’une région primaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-159">The trigger should be connected to a primary region integration account.</span></span>

3. <span data-ttu-id="6e6ab-160">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de la région primaire* dans la liste et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-160">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>   

   ![Nom du compte d’intégration de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="6e6ab-162">Le paramètre **DateTime pour démarrer la synchronisation des numéros de contrôle** est facultatif.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-162">The **DateTime to start control number sync** setting is optional.</span></span> <span data-ttu-id="6e6ab-163">La **Fréquence** peut être définie sur **Jour**, **Heure**, **Minute** ou **Seconde** avec un intervalle.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-163">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Date/heure et fréquence](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="6e6ab-165">Sélectionnez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-165">Select **New step** > **Add an action**.</span></span>

   ![Nouvelle étape, puis Ajouter une action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="6e6ab-167">Lancez une recherche sur **X12** et sélectionnez **X12 - Ajouter ou mettre à jour des numéros de contrôle**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Ajoutez ou mettez à jour les numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="6e6ab-169">Pour connecter une action à un compte d’intégration d’une région secondaire, sélectionnez **Modifier la connexion** > **Ajouter une nouvelle connexion** pour obtenir la liste des comptes d’intégration disponibles.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-169">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="6e6ab-170">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de la région secondaire* dans la liste et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-170">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span> 

   ![Nom du compte d’intégration de la région secondaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="6e6ab-172">Basculez vers les entrées brutes en cliquant sur l’icône située dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-172">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Basculez vers des entrées brutes](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="6e6ab-174">Sélectionnez le corps à partir du sélecteur de contenu dynamique et enregistrez l’application logique.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-174">Select Body from the dynamic content picker, and save the logic app.</span></span>

   ![Champs de contenu dynamique](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="6e6ab-176">Selon l’intervalle de temps, le déclencheur interroge la table des numéros de contrôle de la région primaire et extrait les nouveaux enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-176">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span></span> 
   <span data-ttu-id="6e6ab-177">L’action les met à jour dans le compte d’intégration de la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-177">The action updates the records in the secondary region integration account.</span></span> 
   <span data-ttu-id="6e6ab-178">S’il n’y a aucune mise à jour, le déclencheur affiche l’état **Ignoré**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-178">If there are no updates, the trigger status appears as **Skipped**.</span></span>   

   ![Table des numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="6e6ab-180">En fonction de l’intervalle de temps, l’état d’exécution incrémentiel est dupliqué d’une région primaire à une région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-180">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span></span> <span data-ttu-id="6e6ab-181">Lors d’un sinistre, lorsque la région primaire n’est pas disponible, dirigez le trafic vers la région secondaire pour la continuité des activités.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-181">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="6e6ab-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="6e6ab-182">EDIFACT</span></span> 

<span data-ttu-id="6e6ab-183">La continuité des activités pour les documents EDI EDIFACT repose sur les numéros de contrôle.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="6e6ab-184">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="6e6ab-184">**Prerequisites**</span></span>

<span data-ttu-id="6e6ab-185">Pour activer la récupération d’urgence pour les messages entrants, sélectionnez les options de vérification de doublons dans les paramètres de réception de l’accord EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-185">To enable disaster recovery for inbound messages, select the duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Sélectionnez les paramètres de vérification des doublons](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="6e6ab-187">Créez une [application logique](../logic-apps/logic-apps-create-a-logic-app.md) dans la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="6e6ab-188">Lancez une recherche sur **EDIFACT** et sélectionnez **EDIFACT - Lors de la modification d’un numéro de contrôle**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Recherchez EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="6e6ab-190">Le déclencheur vous invite à établir une connexion à un compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-190">The trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="6e6ab-191">Le déclencheur doit être connecté au compte d’intégration d’une région primaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-191">The trigger should be connected to a primary region integration account.</span></span> 

3. <span data-ttu-id="6e6ab-192">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de la région primaire* dans la liste et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-192">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>    

   ![Nom du compte d’intégration de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="6e6ab-194">Le paramètre **DateTime pour démarrer la synchronisation des numéros de contrôle** est facultatif.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-194">The **DateTime to start control number sync** setting is optional.</span></span> <span data-ttu-id="6e6ab-195">La **Fréquence** peut être définie sur **Jour**, **Heure**, **Minute** ou **Seconde** avec un intervalle.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-195">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![Date/heure et fréquence](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="6e6ab-197">Sélectionnez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-197">Select **New step** > **Add an action**.</span></span>    

   ![Nouvelle étape, puis Ajouter une action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="6e6ab-199">Lancez une recherche sur **EDIFACT** et sélectionnez **EDIFACT - Ajouter ou mettre à jour des numéros de contrôle**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Ajoutez ou mettez à jour les numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="6e6ab-201">Pour connecter une action à un compte d’intégration d’une région secondaire, sélectionnez **Modifier la connexion** > **Ajouter une nouvelle connexion** pour obtenir la liste des comptes d’intégration disponibles.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-201">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="6e6ab-202">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de la région secondaire* dans la liste et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-202">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span>

   ![Nom du compte d’intégration de la région secondaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="6e6ab-204">Basculez vers les entrées brutes en cliquant sur l’icône située dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-204">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Basculez vers des entrées brutes](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="6e6ab-206">Sélectionnez le corps à partir du sélecteur de contenu dynamique et enregistrez l’application logique.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-206">Select Body from the dynamic content picker, and save the logic app.</span></span>   

   ![Champs de contenu dynamique](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="6e6ab-208">Selon l’intervalle de temps, le déclencheur interroge la table des numéros de contrôle de la région primaire et extrait les nouveaux enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-208">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span></span>
   <span data-ttu-id="6e6ab-209">L’action les met à jour dans le compte d’intégration de la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-209">The action updates the records to the secondary region integration account.</span></span> 
   <span data-ttu-id="6e6ab-210">S’il n’y a aucune mise à jour, le déclencheur affiche l’état **Ignoré**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-210">If there are no updates, the trigger status appears as **Skipped**.</span></span>

   ![Table des numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="6e6ab-212">En fonction de l’intervalle de temps, l’état d’exécution incrémentiel est dupliqué d’une région primaire à une région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-212">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span></span> <span data-ttu-id="6e6ab-213">Lors d’un sinistre, lorsque la région primaire n’est pas disponible, dirigez le trafic vers la région secondaire pour la continuité des activités.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-213">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="6e6ab-214">AS2</span><span class="sxs-lookup"><span data-stu-id="6e6ab-214">AS2</span></span> 

<span data-ttu-id="6e6ab-215">La continuité des activités pour les documents qui utilisent le protocole AS2 est basée sur l’ID de message et la valeur MIC.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-215">Business continuity for documents that use the AS2 protocol is based on the message ID and the MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="6e6ab-216">Vous pouvez également utiliser le [modèle de démarrage rapide AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) pour créer des applications logiques.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-216">You can also use the [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) to create logic apps.</span></span> <span data-ttu-id="6e6ab-217">La création d’un compte d’intégration primaire et d’un compte d’intégration secondaire est nécessaire pour utiliser le modèle.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-217">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span> <span data-ttu-id="6e6ab-218">Ce modèle permet de créer une application logique qui comporte un déclencheur et une action.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-218">The template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="6e6ab-219">L’application logique crée une connexion entre le déclencheur et un compte d’intégration primaire et entre l’action et un compte d’intégration secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-219">The logic app creates a connection from a trigger to a primary integration account and an action to a secondary integration account.</span></span>

1. <span data-ttu-id="6e6ab-220">Créez une [application logique](../logic-apps/logic-apps-create-a-logic-app.md) dans la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region.</span></span>  

2. <span data-ttu-id="6e6ab-221">Recherchez **AS2** et sélectionnez **AS2 - Lorsqu’une valeur MIC est créée**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Recherchez AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="6e6ab-223">Un déclencheur vous invite à établir une connexion à un compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-223">A trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="6e6ab-224">Le déclencheur doit être connecté au compte d’intégration d’une région primaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-224">The trigger should be connected to a primary region integration account.</span></span> 
   
3. <span data-ttu-id="6e6ab-225">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de la région primaire* dans la liste et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-225">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>

   ![Nom du compte d’intégration de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="6e6ab-227">Le paramètre **DateTime de démarrage de la synchronisation des valeurs MIC** est facultatif.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-227">The **DateTime to start MIC value sync** setting is optional.</span></span> <span data-ttu-id="6e6ab-228">La **Fréquence** peut être définie sur **Jour**, **Heure**, **Minute** ou **Seconde** avec un intervalle.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-228">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Date/heure et fréquence](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="6e6ab-230">Sélectionnez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-230">Select **New step** > **Add an action**.</span></span>  

   ![Nouvelle étape, puis Ajouter une action](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="6e6ab-232">Recherchez **AS2** et sélectionnez **AS2 - Ajouter ou mettre à jour les contenus MIC**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Ajout ou mise à jour d’un MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="6e6ab-234">Pour connecter une action à un compte d’intégration secondaire, sélectionnez **Modifier la connexion** > **Ajouter une nouvelle connexion** pour obtenir la liste des comptes d’intégration disponibles.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-234">To connect an action to a secondary integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="6e6ab-235">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de la région secondaire* dans la liste et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-235">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span>

   ![Nom du compte d’intégration de la région secondaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="6e6ab-237">Basculez vers les entrées brutes en cliquant sur l’icône située dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-237">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Basculez vers des entrées brutes](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="6e6ab-239">Sélectionnez le corps à partir du sélecteur de contenu dynamique et enregistrez l’application logique.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-239">Select Body from the dynamic content picker, and save the logic app.</span></span>   

   ![Contenu dynamique](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="6e6ab-241">Selon l’intervalle de temps, le déclencheur interroge la table de la région primaire et extrait les nouveaux enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-241">Based on the time interval, the trigger polls the primary region table and pulls the new records.</span></span> <span data-ttu-id="6e6ab-242">L’action les met à jour dans le compte d’intégration de la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-242">The action updates them to the secondary region integration account.</span></span> 
   <span data-ttu-id="6e6ab-243">S’il n’y a aucune mise à jour, le déclencheur affiche l’état **Ignoré**.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-243">If there are no updates, the trigger status appears as **Skipped**.</span></span>  

   ![Table de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="6e6ab-245">En fonction de l’intervalle de temps, l’état d’exécution incrémentiel est dupliqué de la région primaire à la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-245">Based on the time interval, the incremental runtime status replicates from the primary region to the secondary region.</span></span> <span data-ttu-id="6e6ab-246">Lors d’un sinistre, lorsque la région primaire n’est pas disponible, dirigez le trafic vers la région secondaire pour la continuité des activités.</span><span class="sxs-lookup"><span data-stu-id="6e6ab-246">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6e6ab-247">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e6ab-247">Next steps</span></span>

[<span data-ttu-id="6e6ab-248">Surveiller les messages B2B</span><span class="sxs-lookup"><span data-stu-id="6e6ab-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

