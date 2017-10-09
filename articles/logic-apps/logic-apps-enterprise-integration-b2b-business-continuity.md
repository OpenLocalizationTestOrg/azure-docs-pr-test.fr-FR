---
title: "récupération d’aaaDisaster pour le compte d’intégration B2B - Azure Logic Apps | Documents Microsoft"
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
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="b6871-103">Récupération d’urgence inter-régions Logic Apps B2B</span><span class="sxs-lookup"><span data-stu-id="b6871-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="b6871-104">Les charges de travail B2B impliquent des transactions monétaires telles que des commandes et des factures.</span><span class="sxs-lookup"><span data-stu-id="b6871-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="b6871-105">Lors d’un événement d’urgence, il est essentiel pour un Bonjour de toomeet business tooquickly récupérer au niveau de l’entreprise SLA convenu avec leurs partenaires.</span><span class="sxs-lookup"><span data-stu-id="b6871-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="b6871-106">Cet article explique comment planifier des toobuild une continuité des activités pour les charges de travail B2B.</span><span class="sxs-lookup"><span data-stu-id="b6871-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="b6871-107">Préparation à la récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="b6871-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="b6871-108">Basculer la région toosecondary pendant un événement d’urgence</span><span class="sxs-lookup"><span data-stu-id="b6871-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="b6871-109">Revenir tooprimary région après un sinistre</span><span class="sxs-lookup"><span data-stu-id="b6871-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="b6871-110">Préparation à la récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="b6871-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="b6871-111">Identifiez une zone secondaire et créez un [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) dans la région secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="b6871-112">Ajouter des partenaires, des schémas et des accords pour le flux de messages hello requis où hello statut d’exécution doit toobe répliquée toosecondary région intégration compte.</span><span class="sxs-lookup"><span data-stu-id="b6871-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="b6871-113">Assurez-vous que la convention de dénomination d’artefact hello intégration compte est la cohérence entre les régions.</span><span class="sxs-lookup"><span data-stu-id="b6871-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="b6871-114">hello toopull état d’exécution à partir de la région principale de hello, créez une application de logique dans la région secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="b6871-115">L’application logique doit disposer d’un *déclencheur* et d’une *action*.</span><span class="sxs-lookup"><span data-stu-id="b6871-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="b6871-116">déclencheur de Hello doit connecter des compte d’intégration tooprimary région, et action de hello doit au compte d’intégration toosecondary région.</span><span class="sxs-lookup"><span data-stu-id="b6871-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="b6871-117">En fonction de l’intervalle de temps hello, le déclencheur de hello interroge la table d’état région principale exécuter hello et extrait les nouveaux enregistrements de hello, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="b6871-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="b6871-118">Hello met à jour leur compte d’intégration toosecondary région.</span><span class="sxs-lookup"><span data-stu-id="b6871-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="b6871-119">Cela permet d’état d’exécution incrémentielle du tooget à partir de la région de toosecondary région principale.</span><span class="sxs-lookup"><span data-stu-id="b6871-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="b6871-120">Continuité des activités dans les applications de la logique de compte d’intégration est conçu toosupport basée sur des protocoles B2B - X12, AS2 et EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="b6871-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="b6871-121">toofind les étapes détaillées, sélectionnez hello les liens correspondants.</span><span class="sxs-lookup"><span data-stu-id="b6871-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="b6871-122">Hello recommandation est toodeploy toutes les ressources de région principale dans une région secondaire de trop.</span><span class="sxs-lookup"><span data-stu-id="b6871-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="b6871-123">Ressources de la région principale incluent la base de données SQL Azure ou base de données Azure Cosmos, Azure Service Bus et concentrateurs d’événements Azure utilisé pour la messagerie, la gestion des API Azure et la fonctionnalité d’Azure Logic Apps hello dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b6871-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="b6871-124">Établir une connexion à partir d’une région secondaire tooa de région principale.</span><span class="sxs-lookup"><span data-stu-id="b6871-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="b6871-125">hello toopull état d’exécution à partir d’une région primaire, créez une application de logique dans une région secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="b6871-126">application de la logique de Hello doit avoir un déclencheur et une action.</span><span class="sxs-lookup"><span data-stu-id="b6871-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="b6871-127">déclencheur de Hello doit se connecter à compte d’intégration tooa région principale.</span><span class="sxs-lookup"><span data-stu-id="b6871-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="b6871-128">action de Hello doit se connecter à compte d’intégration tooa région secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="b6871-129">En fonction de l’intervalle de temps hello, le déclencheur de hello interroge la table d’état région principale exécuter hello et extrait les nouveaux enregistrements de hello, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="b6871-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="b6871-130">Hello met à jour leur compte d’intégration tooa région secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="b6871-131">Ce processus permet d’état d’exécution incrémentielle du tooget à partir de la région de hello région principale toohello secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="b6871-132">Continuité des activités dans un compte d’intégration Logic Apps fournit la prise en charge basée sur des protocoles B2B de hello X12, AS2 et EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="b6871-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="b6871-133">Pour obtenir des instructions détaillées sur l’utilisation de X12 et AS2, consultez les sections de cet articles consacrées à [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) et [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2).</span><span class="sxs-lookup"><span data-stu-id="b6871-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="b6871-134">Basculer la région secondaire tooa pendant un événement d’urgence</span><span class="sxs-lookup"><span data-stu-id="b6871-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="b6871-135">Lors d’un événement d’urgence, lorsque la région principale de hello n’est pas disponible pour la continuité des activités, région secondaire toohello de diriger le trafic.</span><span class="sxs-lookup"><span data-stu-id="b6871-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="b6871-136">Vous aide à une région secondaire un toorecover entreprise fonctions rapidement toomeet hello RPO/RTO convenu par leurs partenaires.</span><span class="sxs-lookup"><span data-stu-id="b6871-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="b6871-137">Elle réduit également efforts toofail sur à partir de la région de tooanother d’une région.</span><span class="sxs-lookup"><span data-stu-id="b6871-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="b6871-138">Il existe une latence attendue lors de la copie des numéros de contrôle à partir d’une région secondaire tooa de région principale.</span><span class="sxs-lookup"><span data-stu-id="b6871-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="b6871-139">tooavoid envoi contrôle généré en double chiffres toopartners pendant un événement d’urgence, de recommandation de hello est tooincrement des numéros de contrôle hello dans les contrats de région secondaire hello à l’aide de [applets de commande PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="b6871-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="b6871-140">Revenir à des événements de post-incident tooa région principale</span><span class="sxs-lookup"><span data-stu-id="b6871-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="b6871-141">région principale toofall tooa arrière lorsqu’il est disponible, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b6871-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="b6871-142">Arrêter d’accepter les messages de partenaires dans la région secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="b6871-143">Incrémenter les numéros de contrôle hello généré pour tous les contrats de région principale hello à l’aide de [applets de commande PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="b6871-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="b6871-144">Trafic directement à partir de la région principale du toohello hello région secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="b6871-145">Vérifiez que cette application logique de hello créée dans la région secondaire de hello pour extraire l’état d’exécution à partir de la région principale de hello est activée.</span><span class="sxs-lookup"><span data-stu-id="b6871-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="b6871-146">X 12</span><span class="sxs-lookup"><span data-stu-id="b6871-146">X12</span></span> 

<span data-ttu-id="b6871-147">La continuité des activités pour les documents EDI X12 documents repose sur les numéros de contrôle :</span><span class="sxs-lookup"><span data-stu-id="b6871-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="b6871-148">Vous pouvez également utiliser hello [X12 rapide démarrer modèle](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logique applications.</span><span class="sxs-lookup"><span data-stu-id="b6871-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="b6871-149">Création de comptes d’intégration principaux et secondaires est des conditions préalables toouse hello par modèle.</span><span class="sxs-lookup"><span data-stu-id="b6871-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="b6871-150">Hello modèle permet de toocreate deux applications de logique, une pour les numéros de contrôle reçu et l’autre pour les numéros de contrôle généré.</span><span class="sxs-lookup"><span data-stu-id="b6871-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="b6871-151">Actions et déclencheurs respectifs sont créées dans les applications logique hello, connexion hello déclencheur toohello principal compte d’intégration et le compte d’intégration secondaire toohello hello action.</span><span class="sxs-lookup"><span data-stu-id="b6871-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="b6871-152">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="b6871-152">**Prerequisites**</span></span>

<span data-ttu-id="b6871-153">tooenable la récupération d’urgence pour les messages entrants, sélectionnez les paramètres de vérification des doublons de hello dans les paramètres de réception de l’accord hello X12.</span><span class="sxs-lookup"><span data-stu-id="b6871-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![Sélectionnez les paramètres de vérification des doublons](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="b6871-155">Créez une [application logique](../logic-apps/logic-apps-create-a-logic-app.md) dans la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="b6871-156">Lancez une recherche sur **X12** et sélectionnez **X12 - Lors de la modification d’un numéro de contrôle**.</span><span class="sxs-lookup"><span data-stu-id="b6871-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Recherchez X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="b6871-158">déclencheur de Hello invite tooestablish un compte de connexion d’intégration tooan.</span><span class="sxs-lookup"><span data-stu-id="b6871-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="b6871-159">Hello déclencheur doit être connecté de compte d’intégration tooa région principale.</span><span class="sxs-lookup"><span data-stu-id="b6871-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="b6871-160">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région principale* de hello liste, puis choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="b6871-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![Nom du compte d’intégration de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="b6871-162">Hello **toostart DateTime synchronisation des numéro de contrôle** paramètre est facultatif.</span><span class="sxs-lookup"><span data-stu-id="b6871-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="b6871-163">Hello **fréquence** peut être défini trop**jour**, **heure**, **Minute**, ou **deuxième** avec un intervalle.</span><span class="sxs-lookup"><span data-stu-id="b6871-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Date/heure et fréquence](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="b6871-165">Sélectionnez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="b6871-165">Select **New step** > **Add an action**.</span></span>

   ![Nouvelle étape, puis Ajouter une action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="b6871-167">Lancez une recherche sur **X12** et sélectionnez **X12 - Ajouter ou mettre à jour des numéros de contrôle**.</span><span class="sxs-lookup"><span data-stu-id="b6871-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Ajoutez ou mettez à jour les numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="b6871-169">tooconnect compte d’action tooa région secondaire intégration, sélectionnez **modifier la connexion** > **ajouter une nouvelle connexion** pour obtenir la liste des comptes d’intégration disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="b6871-170">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région secondaire* de hello liste, puis choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="b6871-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![Nom du compte d’intégration de la région secondaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="b6871-172">Basculez tooraw entrées en cliquant sur l’icône de hello dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="b6871-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Commutateur tooraw entrées](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="b6871-174">Sélectionnez corps dans le sélecteur de contenu dynamique hello et enregistrez l’application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![Champs de contenu dynamique](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="b6871-176">En fonction de l’intervalle de temps hello, le déclencheur de hello interroge la table numéro de contrôle de région primaire reçue hello et extrait les nouveaux enregistrements de hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="b6871-177">action de Hello met à jour les enregistrements de hello dans le compte d’intégration hello région secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="b6871-178">S’il n’y a aucune mise à jour, l’état de déclencheur hello apparaît comme **ignoré**.</span><span class="sxs-lookup"><span data-stu-id="b6871-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![Table des numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="b6871-180">État d’exécution incrémentielle du hello selon l’intervalle de temps hello, réplique à partir d’une région secondaire tooa de région principale.</span><span class="sxs-lookup"><span data-stu-id="b6871-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="b6871-181">Lors d’un événement d’urgence, lorsque la région primaire hello n’est pas région secondaire de toohello du trafic direct disponible pour la continuité d’activité.</span><span class="sxs-lookup"><span data-stu-id="b6871-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="b6871-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="b6871-182">EDIFACT</span></span> 

<span data-ttu-id="b6871-183">La continuité des activités pour les documents EDI EDIFACT repose sur les numéros de contrôle.</span><span class="sxs-lookup"><span data-stu-id="b6871-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="b6871-184">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="b6871-184">**Prerequisites**</span></span>

<span data-ttu-id="b6871-185">tooenable la récupération d’urgence pour les messages entrants, sélectionnez les paramètres de vérification des doublons hello dans les paramètres de réception de votre accord EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="b6871-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Sélectionnez les paramètres de vérification des doublons](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="b6871-187">Créez une [application logique](../logic-apps/logic-apps-create-a-logic-app.md) dans la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="b6871-188">Lancez une recherche sur **EDIFACT** et sélectionnez **EDIFACT - Lors de la modification d’un numéro de contrôle**.</span><span class="sxs-lookup"><span data-stu-id="b6871-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Recherchez EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="b6871-190">déclencheur de Hello invite tooestablish un compte de connexion d’intégration tooan.</span><span class="sxs-lookup"><span data-stu-id="b6871-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="b6871-191">Hello déclencheur doit être connecté de compte d’intégration tooa région principale.</span><span class="sxs-lookup"><span data-stu-id="b6871-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="b6871-192">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région principale* de hello liste, puis choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="b6871-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![Nom du compte d’intégration de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="b6871-194">Hello **toostart DateTime synchronisation des numéro de contrôle** paramètre est facultatif.</span><span class="sxs-lookup"><span data-stu-id="b6871-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="b6871-195">Hello **fréquence** peut être défini trop**jour**, **heure**, **Minute**, ou **deuxième** avec un intervalle.</span><span class="sxs-lookup"><span data-stu-id="b6871-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![Date/heure et fréquence](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="b6871-197">Sélectionnez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="b6871-197">Select **New step** > **Add an action**.</span></span>    

   ![Nouvelle étape, puis Ajouter une action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="b6871-199">Lancez une recherche sur **EDIFACT** et sélectionnez **EDIFACT - Ajouter ou mettre à jour des numéros de contrôle**.</span><span class="sxs-lookup"><span data-stu-id="b6871-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Ajoutez ou mettez à jour les numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="b6871-201">tooconnect compte d’action tooa région secondaire intégration, sélectionnez **modifier la connexion** > **ajouter une nouvelle connexion** pour obtenir la liste des comptes d’intégration disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="b6871-202">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région secondaire* de hello liste, puis choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="b6871-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nom du compte d’intégration de la région secondaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="b6871-204">Basculez tooraw entrées en cliquant sur l’icône de hello dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="b6871-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Commutateur tooraw entrées](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="b6871-206">Sélectionnez corps dans le sélecteur de contenu dynamique hello et enregistrez l’application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Champs de contenu dynamique](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="b6871-208">En fonction de l’intervalle de temps hello, le déclencheur de hello interroge la table numéro de contrôle de région primaire reçue hello et extrait les nouveaux enregistrements de hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="b6871-209">action de Hello met à jour le compte d’intégration hello enregistrements toohello région secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="b6871-210">S’il n’y a aucune mise à jour, l’état de déclencheur hello apparaît comme **ignoré**.</span><span class="sxs-lookup"><span data-stu-id="b6871-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![Table des numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="b6871-212">État d’exécution incrémentielle du hello selon l’intervalle de temps hello, réplique à partir d’une région secondaire tooa de région principale.</span><span class="sxs-lookup"><span data-stu-id="b6871-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="b6871-213">Lors d’un événement d’urgence, lorsque la région primaire hello n’est pas région secondaire de toohello du trafic direct disponible pour la continuité d’activité.</span><span class="sxs-lookup"><span data-stu-id="b6871-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="b6871-214">AS2</span><span class="sxs-lookup"><span data-stu-id="b6871-214">AS2</span></span> 

<span data-ttu-id="b6871-215">Continuité des activités pour les documents qui utilisent le protocole de AS2 hello est basée sur les ID de message hello et la valeur MIC hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="b6871-216">Vous pouvez également utiliser hello [modèle de démarrage rapide AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logique applications.</span><span class="sxs-lookup"><span data-stu-id="b6871-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="b6871-217">Création de comptes d’intégration principaux et secondaires est des conditions préalables toouse hello par modèle.</span><span class="sxs-lookup"><span data-stu-id="b6871-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="b6871-218">modèle de Hello permet de créer une application de la logique qui a un déclencheur et une action.</span><span class="sxs-lookup"><span data-stu-id="b6871-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="b6871-219">application de la logique de Hello crée une connexion à partir d’un compte d’intégration principal tooa déclencheur et un compte d’action tooa intégration secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="b6871-220">Créer un [application logique](../logic-apps/logic-apps-create-a-logic-app.md) dans la région secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="b6871-221">Recherchez **AS2** et sélectionnez **AS2 - Lorsqu’une valeur MIC est créée**.</span><span class="sxs-lookup"><span data-stu-id="b6871-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Recherchez AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="b6871-223">Un déclencheur vous invite tooestablish un compte de connexion d’intégration tooan.</span><span class="sxs-lookup"><span data-stu-id="b6871-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="b6871-224">Hello déclencheur doit être connecté de compte d’intégration tooa région principale.</span><span class="sxs-lookup"><span data-stu-id="b6871-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="b6871-225">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région principale* de hello liste, puis choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="b6871-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nom du compte d’intégration de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="b6871-227">Hello **synchronisation de valeur DateTime toostart MIC** paramètre est facultatif.</span><span class="sxs-lookup"><span data-stu-id="b6871-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="b6871-228">Hello **fréquence** peut être défini trop**jour**, **heure**, **Minute**, ou **deuxième** avec un intervalle.</span><span class="sxs-lookup"><span data-stu-id="b6871-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Date/heure et fréquence](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="b6871-230">Sélectionnez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="b6871-230">Select **New step** > **Add an action**.</span></span>  

   ![Nouvelle étape, puis Ajouter une action](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="b6871-232">Recherchez **AS2** et sélectionnez **AS2 - Ajouter ou mettre à jour les contenus MIC**.</span><span class="sxs-lookup"><span data-stu-id="b6871-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Ajout ou mise à jour d’un MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="b6871-234">tooconnect compte secondaire intégration tooa d’action, sélectionnez **modifier la connexion** > **ajouter une nouvelle connexion** pour obtenir la liste des comptes d’intégration disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="b6871-235">Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région secondaire* de hello liste, puis choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="b6871-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nom du compte d’intégration de la région secondaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="b6871-237">Basculez tooraw entrées en cliquant sur l’icône de hello dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="b6871-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Commutateur tooraw entrées](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="b6871-239">Sélectionnez corps dans le sélecteur de contenu dynamique hello et enregistrez l’application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Contenu dynamique](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="b6871-241">En fonction de l’intervalle de temps hello, le déclencheur de hello interroge la table de région principale hello et extrait les nouveaux enregistrements de hello.</span><span class="sxs-lookup"><span data-stu-id="b6871-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="b6871-242">Hello met à jour leur compte d’intégration toohello région secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="b6871-243">S’il n’y a aucune mise à jour, l’état de déclencheur hello apparaît comme **ignoré**.</span><span class="sxs-lookup"><span data-stu-id="b6871-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![Table de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="b6871-245">État d’exécution incrémentielle du hello selon l’intervalle de temps hello, réplique à partir de la région de hello région principale toohello secondaire.</span><span class="sxs-lookup"><span data-stu-id="b6871-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="b6871-246">Lors d’un événement d’urgence, lorsque la région primaire hello n’est pas région secondaire de toohello du trafic direct disponible pour la continuité d’activité.</span><span class="sxs-lookup"><span data-stu-id="b6871-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b6871-247">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6871-247">Next steps</span></span>

[<span data-ttu-id="b6871-248">Surveiller les messages B2B</span><span class="sxs-lookup"><span data-stu-id="b6871-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

