---
title: "aaaConnect tooDynamics 365 (en ligne) à partir d’Azure Logic Apps | Documents Microsoft"
description: "Créer des workflows d’application qui gèrent des entités (en ligne) de Dynamics 365 via hello API fournie par le connecteur de hello Dynamics 365 logique"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a><span data-ttu-id="a45b9-103">Se connecter tooDynamics 365 à partir de flux de travail logique application</span><span class="sxs-lookup"><span data-stu-id="a45b9-103">Connect tooDynamics 365 from logic app workflows</span></span>

<span data-ttu-id="a45b9-104">Avec les applications de la logique, vous pouvez connecter tooDynamics 365 (en ligne) et créer des flux métier qui créent des enregistrements, mettre à jour des éléments ou retournent une liste d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="a45b9-104">With Logic Apps, you can connect tooDynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="a45b9-105">Avec le connecteur de hello Dynamics 365, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="a45b9-105">With hello Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="a45b9-106">Générer des flux de votre entreprise en fonction des données hello que vous obtenez à partir de Dynamics 365 (en ligne).</span><span class="sxs-lookup"><span data-stu-id="a45b9-106">Build your business flow based on hello data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="a45b9-107">Utiliser des actions qui obtient une réponse, puis rendez sortie de hello disponible pour d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="a45b9-107">Use actions that get a response and then make hello output available for other actions.</span></span> <span data-ttu-id="a45b9-108">Par exemple, quand un élément est mis à jour dans Dynamics 365 (Online), vous pouvez envoyer un courrier électronique à l’aide d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="a45b9-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="a45b9-109">Cette rubrique vous montre comment une application de la logique de toocreate qui crée une tâche dans Dynamics 365 chaque fois qu’un nouveau prospect est créé dans Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="a45b9-109">This topic shows you how toocreate a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a45b9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a45b9-110">Prerequisites</span></span>
* <span data-ttu-id="a45b9-111">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="a45b9-111">An Azure account.</span></span>
* <span data-ttu-id="a45b9-112">Un compte Dynamics 365 (Online).</span><span class="sxs-lookup"><span data-stu-id="a45b9-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="a45b9-113">Créer une tâche lorsqu’un prospect est créé dans Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="a45b9-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="a45b9-114">[Connectez-vous à tooAzure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a45b9-114">[Sign in tooAzure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="a45b9-115">Dans la zone de recherche Azure hello, tapez `Logic apps`, puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="a45b9-115">In hello Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Rechercher Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="a45b9-117">Sous **Logic Apps**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp - Ajouter](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="a45b9-119">application de la logique toocreate hello, hello complète **nom**, **abonnement**, **groupe de ressources**, et **emplacement** champs, puis cliquez sur  **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-119">toocreate hello logic app, complete hello **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="a45b9-120">Sélectionnez Application logique de la nouvelle hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-120">Select hello new logic app.</span></span> <span data-ttu-id="a45b9-121">Lorsque vous recevez hello **déploiement a réussi** notification, cliquez sur **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-121">When you receive hello **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="a45b9-122">Sous **Outils de développement**, cliquez sur **Concepteur d’application logique**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="a45b9-123">Dans la liste des modèles hello, cliquez sur **application logique vide**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-123">In hello template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="a45b9-124">Dans la zone de recherche de hello, tapez `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="a45b9-124">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="a45b9-125">À partir de hello Dynamics 365 déclenche la liste, sélectionnez **Dynamics 365 – lors de la création d’un enregistrement**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-125">From hello Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="a45b9-126">Si vous êtes invité à toosign dans tooDynamics 365, faites-le maintenant.</span><span class="sxs-lookup"><span data-stu-id="a45b9-126">If you are prompted toosign in tooDynamics 365, do so now.</span></span>

9.  <span data-ttu-id="a45b9-127">Dans Détails du déclencheur hello, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a45b9-127">In hello trigger details, enter hello following information:</span></span>

  * <span data-ttu-id="a45b9-128">**Nom de l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-128">**Organization Name**.</span></span> <span data-ttu-id="a45b9-129">Sélectionnez instance Dynamics 365 hello hello logique application toolisten à souhaitées.</span><span class="sxs-lookup"><span data-stu-id="a45b9-129">Select hello Dynamics 365 instance that you want hello logic app toolisten to.</span></span>

  * <span data-ttu-id="a45b9-130">**Nom de l’entité**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-130">**Entity Name**.</span></span> <span data-ttu-id="a45b9-131">Sélectionnez hello entité toolisten à.</span><span class="sxs-lookup"><span data-stu-id="a45b9-131">Select hello entity that you want toolisten to.</span></span> <span data-ttu-id="a45b9-132">Cet événement agit comme une application de la logique de déclencheur toostart hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-132">This event acts as a trigger toostart hello logic app.</span></span> 
  <span data-ttu-id="a45b9-133">Dans cette procédure pas à pas, **Prospects** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="a45b9-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="a45b9-134">**La fréquence à laquelle vous souhaitez toocheck pour les éléments ?**</span><span class="sxs-lookup"><span data-stu-id="a45b9-134">**How often do you want toocheck for items?**</span></span> <span data-ttu-id="a45b9-135">Ces valeurs de définir la fréquence à laquelle hello logique application vérifie déclencheur toohello connexes de mises à jour.</span><span class="sxs-lookup"><span data-stu-id="a45b9-135">These values set how often hello logic app checks for updates related toohello trigger.</span></span> <span data-ttu-id="a45b9-136">par défaut Hello est toocheck des mises à jour toutes les trois minutes.</span><span class="sxs-lookup"><span data-stu-id="a45b9-136">hello default setting is toocheck for updates every three minutes.</span></span>

    * <span data-ttu-id="a45b9-137">**Fréquence**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-137">**Frequency**.</span></span> <span data-ttu-id="a45b9-138">Sélectionnez les secondes, les minutes, les heures ou les jours.</span><span class="sxs-lookup"><span data-stu-id="a45b9-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="a45b9-139">**Intervalle**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-139">**Interval**.</span></span> <span data-ttu-id="a45b9-140">Entrez un nombre hello de secondes, minutes, heures ou jours que vous souhaitez toopass avant la prochaine vérification de hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-140">Enter hello number of seconds, minutes, hours, or days that you want toopass before hello next check.</span></span>

      ![Application logique - Détails sur le déclencheur](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="a45b9-142">Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="a45b9-143">Dans la zone de recherche de hello, tapez `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="a45b9-143">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="a45b9-144">Dans la liste d’actions hello, sélectionnez **Dynamics 365 – créer un nouvel enregistrement**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-144">From hello actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="a45b9-145">Entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a45b9-145">Enter hello following information:</span></span>

    * <span data-ttu-id="a45b9-146">**Nom de l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-146">**Organization Name**.</span></span> <span data-ttu-id="a45b9-147">Sélectionnez l’instance hello Dynamics 365 où vous souhaitez l’enregistrement de hello flux toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-147">Select hello Dynamics 365 instance where you want hello flow toocreate hello record.</span></span> 
    <span data-ttu-id="a45b9-148">Notez que cette instance n’a toobe hello même instance où les événements de hello est déclenchée à partir de.</span><span class="sxs-lookup"><span data-stu-id="a45b9-148">Notice that this instance doesn’t have toobe hello same instance where hello event is triggered from.</span></span>

    * <span data-ttu-id="a45b9-149">**Nom de l’entité**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-149">**Entity Name**.</span></span> <span data-ttu-id="a45b9-150">Sélectionnez hello entité que toocreate un enregistrement lorsque hello est déclenché.</span><span class="sxs-lookup"><span data-stu-id="a45b9-150">Select hello entity that you want toocreate a record when hello event is triggered.</span></span> 
    <span data-ttu-id="a45b9-151">Dans cette procédure pas à pas, **Tâches** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="a45b9-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="a45b9-152">Cliquez sur Bonjour **sujet** zone qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a45b9-152">Click in hello **Subject** box that appears.</span></span> <span data-ttu-id="a45b9-153">À partir de hello dynamique contenu liste qui s’affiche, vous pouvez sélectionner un de ces champs :</span><span class="sxs-lookup"><span data-stu-id="a45b9-153">From hello dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="a45b9-154">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-154">**Last Name**.</span></span> <span data-ttu-id="a45b9-155">Ce champ insère hello nom hello prospect champ d’objet hello pour la tâche hello, lors de l’enregistrement de tâche hello est créé.</span><span class="sxs-lookup"><span data-stu-id="a45b9-155">Selecting this field inserts hello last name for hello lead into hello Subject field for hello task, when hello task record is created.</span></span>
    * <span data-ttu-id="a45b9-156">**Rubrique**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-156">**Topic**.</span></span> <span data-ttu-id="a45b9-157">La sélection de ce champ insertions hello rubrique prospect hello dans le champ d’objet hello pour la tâche hello lorsque hello tâche enregistrement est créé.</span><span class="sxs-lookup"><span data-stu-id="a45b9-157">Selecting this field inserts hello Topic field for hello lead into hello Subject field for hello task, when hello task record is created.</span></span> 
    <span data-ttu-id="a45b9-158">Cliquez sur **rubrique** tooadd que toohello **sujet** boîte.</span><span class="sxs-lookup"><span data-stu-id="a45b9-158">Click **Topic** tooadd that toohello **Subject** box.</span></span>

      ![Application logique - Détails Créer un enregistrement](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="a45b9-160">Dans la barre d’outils du Concepteur de la logique d’application hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-160">On hello Logic App Designer toolbar, click **Save**.</span></span>

    ![Barre d’outils du Concepteur d’application logique - Enregistrer](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="a45b9-162">toostart hello logique d’application, cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-162">toostart hello Logic App, click **Run**.</span></span>

    ![Barre d’outils du Concepteur d’application logique - Enregistrer](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="a45b9-164">Créez maintenant un enregistrement de prospect dans Dynamics 365 pour les ventes et observez votre flux en action !</span><span class="sxs-lookup"><span data-stu-id="a45b9-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="a45b9-165">Définir les options avancées d’une étape d’application logique</span><span class="sxs-lookup"><span data-stu-id="a45b9-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="a45b9-166">toospecify comment toofilter les données dans une étape d’application logique, cliquez sur **Show advanced options** dans cette étape, puis ajoutez un filtre ou une commande par requête.</span><span class="sxs-lookup"><span data-stu-id="a45b9-166">toospecify how toofilter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="a45b9-167">Par exemple, vous pouvez utiliser un filtre requête tooget uniquement les comptes actifs et trier par nom de compte hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-167">For example, you can use a filter query tooget only active accounts and order by hello account name.</span></span> <span data-ttu-id="a45b9-168">tooperform cette tâche, entrez la requête de filtre OData hello `statuscode eq 1`, puis sélectionnez **nom de compte** à partir de la liste de contenu dynamique hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-168">tooperform this task, enter hello OData filter query `statuscode eq 1`, and select **Account Name** from hello dynamic content list.</span></span> <span data-ttu-id="a45b9-169">Plus d’informations : [MSDN : $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) et [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="a45b9-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Application logique - Options avancées](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="a45b9-171">Meilleures pratiques lors de l’utilisation des options avancées</span><span class="sxs-lookup"><span data-stu-id="a45b9-171">Best practices when using advanced options</span></span>

<span data-ttu-id="a45b9-172">Lorsque vous ajoutez un champ de valeur de tooa, vous devez correspondre au type de champ hello si vous tapez une valeur ou sélectionnez une valeur dans la liste de contenu dynamique hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-172">When you add a value tooa field, you must match hello field type whether you type a value or select a value from hello dynamic content list.</span></span>

<span data-ttu-id="a45b9-173">Type de champ</span><span class="sxs-lookup"><span data-stu-id="a45b9-173">Field type</span></span>  |<span data-ttu-id="a45b9-174">Comment toouse</span><span class="sxs-lookup"><span data-stu-id="a45b9-174">How toouse</span></span>  |<span data-ttu-id="a45b9-175">Où toofind</span><span class="sxs-lookup"><span data-stu-id="a45b9-175">Where toofind</span></span>  |<span data-ttu-id="a45b9-176">Nom</span><span class="sxs-lookup"><span data-stu-id="a45b9-176">Name</span></span>  |<span data-ttu-id="a45b9-177">Type de données</span><span class="sxs-lookup"><span data-stu-id="a45b9-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="a45b9-178">Champs de texte</span><span class="sxs-lookup"><span data-stu-id="a45b9-178">Text fields</span></span>|<span data-ttu-id="a45b9-179">Les champs de texte nécessitent une seule ligne de texte ou du contenu dynamique qui est un champ de type texte.</span><span class="sxs-lookup"><span data-stu-id="a45b9-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="a45b9-180">Champs de catégorie et sous-catégorie hello sont des exemples.</span><span class="sxs-lookup"><span data-stu-id="a45b9-180">Examples include hello Category and Sub-Category fields.</span></span>|<span data-ttu-id="a45b9-181">Paramètres > personnalisations > Personnaliser hello système > entités > tâches > champs</span><span class="sxs-lookup"><span data-stu-id="a45b9-181">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="a45b9-182">category</span><span class="sxs-lookup"><span data-stu-id="a45b9-182">category</span></span> |<span data-ttu-id="a45b9-183">Ligne de texte unique</span><span class="sxs-lookup"><span data-stu-id="a45b9-183">Single Line of Text</span></span>        
<span data-ttu-id="a45b9-184">Champs de type entier</span><span class="sxs-lookup"><span data-stu-id="a45b9-184">Integer fields</span></span> | <span data-ttu-id="a45b9-185">Certains champs nécessitent un entier ou un contenu dynamique qui est un champ de type entier.</span><span class="sxs-lookup"><span data-stu-id="a45b9-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="a45b9-186">Exemples : Pourcentage achevé et Durée.</span><span class="sxs-lookup"><span data-stu-id="a45b9-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="a45b9-187">Paramètres > personnalisations > Personnaliser hello système > entités > tâches > champs</span><span class="sxs-lookup"><span data-stu-id="a45b9-187">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="a45b9-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="a45b9-188">percentcomplete</span></span> |<span data-ttu-id="a45b9-189">Nombre entier</span><span class="sxs-lookup"><span data-stu-id="a45b9-189">Whole Number</span></span>         
<span data-ttu-id="a45b9-190">Champs de date</span><span class="sxs-lookup"><span data-stu-id="a45b9-190">Date fields</span></span> | <span data-ttu-id="a45b9-191">Certains champs nécessitent qu’une date soit saisie au format mm/jj/aaaa ou un contenu dynamique qui est un champ de type date.</span><span class="sxs-lookup"><span data-stu-id="a45b9-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="a45b9-192">Exemples : Créé le, Date de début, Début réel, Dernière durée de suspension, Fin réelle et Date d’échéance.</span><span class="sxs-lookup"><span data-stu-id="a45b9-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="a45b9-193">Paramètres > personnalisations > Personnaliser hello système > entités > tâches > champs</span><span class="sxs-lookup"><span data-stu-id="a45b9-193">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="a45b9-194">createdon</span><span class="sxs-lookup"><span data-stu-id="a45b9-194">createdon</span></span> |<span data-ttu-id="a45b9-195">Date et heure</span><span class="sxs-lookup"><span data-stu-id="a45b9-195">Date and Time</span></span>
<span data-ttu-id="a45b9-196">Champs qui nécessitent à la fois un ID d’enregistrement et un type de recherche</span><span class="sxs-lookup"><span data-stu-id="a45b9-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="a45b9-197">Certains champs qui font référence à un autre enregistrement d’entité nécessitent l’ID d’enregistrement hello et type de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-197">Some fields that reference another entity record require both hello record ID and hello lookup type.</span></span> |<span data-ttu-id="a45b9-198">Paramètres > personnalisations > Personnaliser hello système > entités > compte > champs</span><span class="sxs-lookup"><span data-stu-id="a45b9-198">Settings > Customizations > Customize hello System > Entities > Account > Fields</span></span>  | <span data-ttu-id="a45b9-199">accountid</span><span class="sxs-lookup"><span data-stu-id="a45b9-199">accountid</span></span>  | <span data-ttu-id="a45b9-200">Clé primaire</span><span class="sxs-lookup"><span data-stu-id="a45b9-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="a45b9-201">Exemples de champs supplémentaires nécessitant un ID d’enregistrement et un type de recherche</span><span class="sxs-lookup"><span data-stu-id="a45b9-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="a45b9-202">Développement sur le tableau précédent de hello, Voici plusieurs exemples de champs qui ne fonctionnent pas avec les valeurs sélectionnées à partir de la liste de contenu dynamique hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-202">Expanding on hello previous table, here are more examples of fields that don't work with values selected from hello dynamic content list.</span></span> <span data-ttu-id="a45b9-203">Au lieu de cela, ces champs nécessitent les deux ID et recherche de type d’enregistrement entré dans les champs de hello dans PowerApps.</span><span class="sxs-lookup"><span data-stu-id="a45b9-203">Instead, these fields require both a record ID and lookup type entered into hello fields in PowerApps.</span></span>  
* <span data-ttu-id="a45b9-204">Propriétaire et Type de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="a45b9-204">Owner and Owner Type.</span></span> <span data-ttu-id="a45b9-205">champ de Hello propriétaire doit être un ID d’enregistrement utilisateur ou de l’équipe valide</span><span class="sxs-lookup"><span data-stu-id="a45b9-205">hello Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="a45b9-206">Hello Type propriétaire doit être **systemusers** ou **équipes**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-206">hello Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="a45b9-207">Client et Type de client.</span><span class="sxs-lookup"><span data-stu-id="a45b9-207">Customer and Customer Type.</span></span> <span data-ttu-id="a45b9-208">champ de Hello client doit être un compte valide ou ID de l’enregistrement de contact.</span><span class="sxs-lookup"><span data-stu-id="a45b9-208">hello Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="a45b9-209">Hello Type propriétaire doit être **comptes** ou **contacts**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-209">hello Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="a45b9-210">Concernant et Type Concernant.</span><span class="sxs-lookup"><span data-stu-id="a45b9-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="a45b9-211">Hello concernant le champ doit être un ID d’enregistrement valide, tel qu’un compte ou ID de l’enregistrement de contact.</span><span class="sxs-lookup"><span data-stu-id="a45b9-211">hello Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="a45b9-212">Hello en ce qui concerne le Type doit être le type de recherche hello pour l’enregistrement de hello, tel que **comptes** ou **contacts**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-212">hello Regarding Type must be hello lookup type for hello record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="a45b9-213">Hello exemple action de création de tâche suivant ajoute un enregistrement de compte correspondant ID d’enregistrement toohello ajoutant toohello concernant le champ de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-213">hello following task creation action example adds an account record that corresponds toohello record ID adding it toohello regarding field of hello task.</span></span>

![Flux : ID d’enregistrement et type de compte](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="a45b9-215">Cet exemple affecte également hello tooa spécifique utilisateur de la tâche en fonction de l’ID d’enregistrement. de l’utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="a45b9-215">This example also assigns hello task tooa specific user based on hello user's record ID.</span></span>

![Flux : ID d’enregistrement et type de compte](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="a45b9-217">toofind un enregistrement de l’ID, consultez hello suivant la section : *rechercher l’ID d’enregistrement hello*</span><span class="sxs-lookup"><span data-stu-id="a45b9-217">toofind a record's ID, see hello following section: *Find hello record ID*</span></span>

## <a name="find-hello-record-id"></a><span data-ttu-id="a45b9-218">Rechercher l’ID d’enregistrement hello</span><span class="sxs-lookup"><span data-stu-id="a45b9-218">Find hello record ID</span></span>

1. <span data-ttu-id="a45b9-219">Ouvrez un enregistrement, comme un enregistrement de compte.</span><span class="sxs-lookup"><span data-stu-id="a45b9-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="a45b9-220">Dans la barre d’outils de hello actions, cliquez sur **sortir** ![enregistrement de la fenêtre indépendante](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="a45b9-220">On hello actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="a45b9-221">Vous pouvez également hello actions la barre d’outils toocopy hello une URL complète dans votre programme de messagerie par défaut, cliquez sur **par courrier électronique un lien**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-221">Alternatively, on hello actions toolbar, toocopy hello full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="a45b9-222">ID d’enregistrement Hello est affichée entre hello % 7 b et %7 d’encodage des caractères de l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-222">hello record ID is displayed in between hello %7b and %7d encoding characters of hello URL.</span></span>

   ![Flux : ID d’enregistrement et type de compte](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="a45b9-224">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a45b9-224">Troubleshooting</span></span>
<span data-ttu-id="a45b9-225">tootroubleshoot Échec d’une étape dans une application logique, afficher les détails de statut hello d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-225">tootroubleshoot a failed step in a logic app, view hello status details of hello event.</span></span>

1. <span data-ttu-id="a45b9-226">Dans la zone **Logic Apps**, sélectionnez votre application logique, puis cliquez sur **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="a45b9-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="a45b9-227">Hello zone de récapitulatif est affiché et fournit l’état de hello exécuter pour l’application de la logique de hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-227">hello Summary area is shown and provides hello run status for hello logic app.</span></span> 

   ![État d’exécution de l’application logique](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="a45b9-229">tooview plus d’informations sur toutes les séries ayant échouées, cliquez sur hello Échec de l’événement.</span><span class="sxs-lookup"><span data-stu-id="a45b9-229">tooview more information about any failed runs, click hello failed event.</span></span> <span data-ttu-id="a45b9-230">tooexpand Échec d’une étape, cliquez sur cette étape.</span><span class="sxs-lookup"><span data-stu-id="a45b9-230">tooexpand a failed step, click that step.</span></span>

   ![Développer l’étape qui a échoué](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="a45b9-232">Détails de l’étape Hello apparaissent et peuvent aider à résoudre la cause hello de défaillance de hello.</span><span class="sxs-lookup"><span data-stu-id="a45b9-232">hello step details appear and can help troubleshoot hello cause of hello failure.</span></span>

   ![Détails de l’étape qui a échoué](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="a45b9-234">Pour plus d’informations sur la résolution des problèmes relatifs aux applications logiques, consultez [Diagnostic des échecs d’applications logiques](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="a45b9-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="a45b9-235">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="a45b9-235">Connector-specific details</span></span>

<span data-ttu-id="a45b9-236">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="a45b9-236">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a45b9-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a45b9-237">Next steps</span></span>
<span data-ttu-id="a45b9-238">Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a45b9-238">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
