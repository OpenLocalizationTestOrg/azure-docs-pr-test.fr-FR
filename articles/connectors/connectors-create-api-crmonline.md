---
title: "Se connecter à Dynamics 365 (Online) à partir de vos applications Azure Logic Apps | Microsoft Docs"
description: "Créer des flux de travail d’application logique qui gèrent des entités Dynamics 365 (Online) via l’API fournie par le connecteur Dynamics 365"
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
ms.openlocfilehash: d35647921ff540167a3a591fb489d3bab031a5c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-dynamics-365-from-logic-app-workflows"></a><span data-ttu-id="5abc5-103">Se connecter à Dynamics 365 à partir de flux de travail d’application logique</span><span class="sxs-lookup"><span data-stu-id="5abc5-103">Connect to Dynamics 365 from logic app workflows</span></span>

<span data-ttu-id="5abc5-104">Avec les applications Logic Apps, vous pouvez vous connecter à Dynamics 365 (Online) et créer des flux d’activité utiles qui génèrent des enregistrements, mettent à jour les éléments ou renvoient une liste d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="5abc5-104">With Logic Apps, you can connect to Dynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="5abc5-105">Avec le connecteur Dynamics 365, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5abc5-105">With the Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="5abc5-106">Créer votre flux d’activité en fonction des données que vous obtenez de Dynamics 365 (Online).</span><span class="sxs-lookup"><span data-stu-id="5abc5-106">Build your business flow based on the data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="5abc5-107">Utiliser les actions qui obtiennent une réponse, puis mettent la sortie à la disposition d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="5abc5-107">Use actions that get a response and then make the output available for other actions.</span></span> <span data-ttu-id="5abc5-108">Par exemple, quand un élément est mis à jour dans Dynamics 365 (Online), vous pouvez envoyer un courrier électronique à l’aide d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="5abc5-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="5abc5-109">Cette rubrique vous explique comment créer une application logique qui génère une tâche dans Dynamics 365 lorsqu’un prospect est créé dans Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="5abc5-109">This topic shows you how to create a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5abc5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5abc5-110">Prerequisites</span></span>
* <span data-ttu-id="5abc5-111">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="5abc5-111">An Azure account.</span></span>
* <span data-ttu-id="5abc5-112">Un compte Dynamics 365 (Online).</span><span class="sxs-lookup"><span data-stu-id="5abc5-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="5abc5-113">Créer une tâche lorsqu’un prospect est créé dans Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="5abc5-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="5abc5-114">[Connectez-vous à Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5abc5-114">[Sign in to Azure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="5abc5-115">Dans la zone de recherche Azure, tapez `Logic apps` et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="5abc5-115">In the Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Rechercher Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="5abc5-117">Sous **Logic Apps**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp - Ajouter](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="5abc5-119">Pour créer l’application logique, renseignez les champs **Nom**, **Abonnement**, **Groupe de ressources** et **Emplacement**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-119">To create the logic app, complete the **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="5abc5-120">Sélectionnez la nouvelle application logique.</span><span class="sxs-lookup"><span data-stu-id="5abc5-120">Select the new logic app.</span></span> <span data-ttu-id="5abc5-121">Lorsque vous recevez la notification **Déploiement réussi**, cliquez sur **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-121">When you receive the **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="5abc5-122">Sous **Outils de développement**, cliquez sur **Concepteur d’application logique**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="5abc5-123">Dans la liste des modèles, cliquez sur **Application logique vide**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-123">In the template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="5abc5-124">Dans la zone de recherche, tapez `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="5abc5-124">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="5abc5-125">Dans la liste des déclencheurs Dynamics 365, sélectionnez **Dynamics 365 – Lorsqu'un enregistrement est créé**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-125">From the Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="5abc5-126">Si vous êtes invité à vous connecter à Dynamics 365, faites-le maintenant.</span><span class="sxs-lookup"><span data-stu-id="5abc5-126">If you are prompted to sign in to Dynamics 365, do so now.</span></span>

9.  <span data-ttu-id="5abc5-127">Entrez les informations suivantes dans les détails du déclencheur :</span><span class="sxs-lookup"><span data-stu-id="5abc5-127">In the trigger details, enter the following information:</span></span>

  * <span data-ttu-id="5abc5-128">**Nom de l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-128">**Organization Name**.</span></span> <span data-ttu-id="5abc5-129">Sélectionnez l’instance de Dynamics 365 que l’application logique doit écouter.</span><span class="sxs-lookup"><span data-stu-id="5abc5-129">Select the Dynamics 365 instance that you want the logic app to listen to.</span></span>

  * <span data-ttu-id="5abc5-130">**Nom de l’entité**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-130">**Entity Name**.</span></span> <span data-ttu-id="5abc5-131">Sélectionnez l’entité que vous souhaitez écouter.</span><span class="sxs-lookup"><span data-stu-id="5abc5-131">Select the entity that you want to listen to.</span></span> <span data-ttu-id="5abc5-132">Cet événement agit comme un déclencheur pour démarrer l’application logique.</span><span class="sxs-lookup"><span data-stu-id="5abc5-132">This event acts as a trigger to start the logic app.</span></span> 
  <span data-ttu-id="5abc5-133">Dans cette procédure pas à pas, **Prospects** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="5abc5-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="5abc5-134">**How often do you want to check for items?** (À quelle fréquence souhaitez-vous rechercher des éléments ?)</span><span class="sxs-lookup"><span data-stu-id="5abc5-134">**How often do you want to check for items?**</span></span> <span data-ttu-id="5abc5-135">Ces valeurs définissent la fréquence à laquelle l’application logique recherche des mises à jour pour le déclencheur.</span><span class="sxs-lookup"><span data-stu-id="5abc5-135">These values set how often the logic app checks for updates related to the trigger.</span></span> <span data-ttu-id="5abc5-136">Le paramètre par défaut consiste à rechercher des mises à jour toutes les trois minutes.</span><span class="sxs-lookup"><span data-stu-id="5abc5-136">The default setting is to check for updates every three minutes.</span></span>

    * <span data-ttu-id="5abc5-137">**Fréquence**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-137">**Frequency**.</span></span> <span data-ttu-id="5abc5-138">Sélectionnez les secondes, les minutes, les heures ou les jours.</span><span class="sxs-lookup"><span data-stu-id="5abc5-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="5abc5-139">**Intervalle**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-139">**Interval**.</span></span> <span data-ttu-id="5abc5-140">Entrez le nombre de secondes, de minutes, d’heures ou de jours qui doivent s’écouler avant la recherche suivante.</span><span class="sxs-lookup"><span data-stu-id="5abc5-140">Enter the number of seconds, minutes, hours, or days that you want to pass before the next check.</span></span>

      ![Application logique - Détails sur le déclencheur](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="5abc5-142">Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="5abc5-143">Dans la zone de recherche, tapez `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="5abc5-143">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="5abc5-144">Dans la liste des actions, sélectionnez **Dynamics 365 – Créer un enregistrement**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-144">From the actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="5abc5-145">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5abc5-145">Enter the following information:</span></span>

    * <span data-ttu-id="5abc5-146">**Nom de l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-146">**Organization Name**.</span></span> <span data-ttu-id="5abc5-147">Sélectionnez l’instance de Dynamics 365 dans laquelle vous souhaitez que le flux crée l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="5abc5-147">Select the Dynamics 365 instance where you want the flow to create the record.</span></span> 
    <span data-ttu-id="5abc5-148">Notez qu’il ne s’agit pas nécessairement de la même instance que celle depuis laquelle l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="5abc5-148">Notice that this instance doesn’t have to be the same instance where the event is triggered from.</span></span>

    * <span data-ttu-id="5abc5-149">**Nom de l’entité**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-149">**Entity Name**.</span></span> <span data-ttu-id="5abc5-150">Sélectionnez l’entité dans laquelle vous souhaitez créer un enregistrement lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="5abc5-150">Select the entity that you want to create a record when the event is triggered.</span></span> 
    <span data-ttu-id="5abc5-151">Dans cette procédure pas à pas, **Tâches** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="5abc5-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="5abc5-152">Cliquez sur le champ **Objet** qui apparaît.</span><span class="sxs-lookup"><span data-stu-id="5abc5-152">Click in the **Subject** box that appears.</span></span> <span data-ttu-id="5abc5-153">Dans la liste de contenu dynamique qui s’affiche, vous pouvez sélectionner un de ces champs :</span><span class="sxs-lookup"><span data-stu-id="5abc5-153">From the dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="5abc5-154">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-154">**Last Name**.</span></span> <span data-ttu-id="5abc5-155">Sélectionner ce champ permettra d’insérer le nom du prospect dans le champ Objet de la tâche, lorsque l’enregistrement de la tâche est créé.</span><span class="sxs-lookup"><span data-stu-id="5abc5-155">Selecting this field inserts the last name for the lead into the Subject field for the task, when the task record is created.</span></span>
    * <span data-ttu-id="5abc5-156">**Rubrique**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-156">**Topic**.</span></span> <span data-ttu-id="5abc5-157">Sélectionner ce champ permettra d’insérer le champ Rubrique dans le champ Objet de la tâche, lorsque l’enregistrement de la tâche est créé.</span><span class="sxs-lookup"><span data-stu-id="5abc5-157">Selecting this field inserts the Topic field for the lead into the Subject field for the task, when the task record is created.</span></span> 
    <span data-ttu-id="5abc5-158">Cliquez sur **Rubrique** pour l’ajouter à la zone **Objet**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-158">Click **Topic** to add that to the **Subject** box.</span></span>

      ![Application logique - Détails Créer un enregistrement](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="5abc5-160">Dans la barre d’outils du Concepteur d’application logique, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-160">On the Logic App Designer toolbar, click **Save**.</span></span>

    ![Barre d’outils du Concepteur d’application logique - Enregistrer](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="5abc5-162">Pour démarrer l’application logique, cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-162">To start the Logic App, click **Run**.</span></span>

    ![Barre d’outils du Concepteur d’application logique - Enregistrer](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="5abc5-164">Créez maintenant un enregistrement de prospect dans Dynamics 365 pour les ventes et observez votre flux en action !</span><span class="sxs-lookup"><span data-stu-id="5abc5-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="5abc5-165">Définir les options avancées d’une étape d’application logique</span><span class="sxs-lookup"><span data-stu-id="5abc5-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="5abc5-166">Pour spécifier comment filtrer les données dans une étape d’application logique, cliquez sur **Afficher les options avancées** dans cette étape, puis ajoutez un filtre ou une commande par requête.</span><span class="sxs-lookup"><span data-stu-id="5abc5-166">To specify how to filter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="5abc5-167">Par exemple, vous pouvez utiliser une requête de filtre pour obtenir uniquement les comptes actifs et trier par nom du compte.</span><span class="sxs-lookup"><span data-stu-id="5abc5-167">For example, you can use a filter query to get only active accounts and order by the account name.</span></span> <span data-ttu-id="5abc5-168">Pour effectuer cette tâche, entrez la requête de filtre OData `statuscode eq 1` et sélectionnez **Nom de compte** dans la liste de contenu dynamique.</span><span class="sxs-lookup"><span data-stu-id="5abc5-168">To perform this task, enter the OData filter query `statuscode eq 1`, and select **Account Name** from the dynamic content list.</span></span> <span data-ttu-id="5abc5-169">Plus d’informations : [MSDN : $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) et [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="5abc5-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Application logique - Options avancées](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="5abc5-171">Meilleures pratiques lors de l’utilisation des options avancées</span><span class="sxs-lookup"><span data-stu-id="5abc5-171">Best practices when using advanced options</span></span>

<span data-ttu-id="5abc5-172">Lorsque vous ajoutez une valeur à un champ, vous devez faire correspondre le type de champ si vous saisissez une valeur ou sélectionner une valeur dans la liste de contenu dynamique.</span><span class="sxs-lookup"><span data-stu-id="5abc5-172">When you add a value to a field, you must match the field type whether you type a value or select a value from the dynamic content list.</span></span>

<span data-ttu-id="5abc5-173">Type de champ</span><span class="sxs-lookup"><span data-stu-id="5abc5-173">Field type</span></span>  |<span data-ttu-id="5abc5-174">Utilisation</span><span class="sxs-lookup"><span data-stu-id="5abc5-174">How to use</span></span>  |<span data-ttu-id="5abc5-175">Comment y accéder</span><span class="sxs-lookup"><span data-stu-id="5abc5-175">Where to find</span></span>  |<span data-ttu-id="5abc5-176">Nom</span><span class="sxs-lookup"><span data-stu-id="5abc5-176">Name</span></span>  |<span data-ttu-id="5abc5-177">Type de données</span><span class="sxs-lookup"><span data-stu-id="5abc5-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="5abc5-178">Champs de texte</span><span class="sxs-lookup"><span data-stu-id="5abc5-178">Text fields</span></span>|<span data-ttu-id="5abc5-179">Les champs de texte nécessitent une seule ligne de texte ou du contenu dynamique qui est un champ de type texte.</span><span class="sxs-lookup"><span data-stu-id="5abc5-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="5abc5-180">Exemples : Catégorie et Sous-catégorie.</span><span class="sxs-lookup"><span data-stu-id="5abc5-180">Examples include the Category and Sub-Category fields.</span></span>|<span data-ttu-id="5abc5-181">Paramètres > Personnalisations > Personnaliser le système > Entités > Tâche > Champs</span><span class="sxs-lookup"><span data-stu-id="5abc5-181">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="5abc5-182">category</span><span class="sxs-lookup"><span data-stu-id="5abc5-182">category</span></span> |<span data-ttu-id="5abc5-183">Ligne de texte unique</span><span class="sxs-lookup"><span data-stu-id="5abc5-183">Single Line of Text</span></span>        
<span data-ttu-id="5abc5-184">Champs de type entier</span><span class="sxs-lookup"><span data-stu-id="5abc5-184">Integer fields</span></span> | <span data-ttu-id="5abc5-185">Certains champs nécessitent un entier ou un contenu dynamique qui est un champ de type entier.</span><span class="sxs-lookup"><span data-stu-id="5abc5-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="5abc5-186">Exemples : Pourcentage achevé et Durée.</span><span class="sxs-lookup"><span data-stu-id="5abc5-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="5abc5-187">Paramètres > Personnalisations > Personnaliser le système > Entités > Tâche > Champs</span><span class="sxs-lookup"><span data-stu-id="5abc5-187">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="5abc5-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="5abc5-188">percentcomplete</span></span> |<span data-ttu-id="5abc5-189">Nombre entier</span><span class="sxs-lookup"><span data-stu-id="5abc5-189">Whole Number</span></span>         
<span data-ttu-id="5abc5-190">Champs de date</span><span class="sxs-lookup"><span data-stu-id="5abc5-190">Date fields</span></span> | <span data-ttu-id="5abc5-191">Certains champs nécessitent qu’une date soit saisie au format mm/jj/aaaa ou un contenu dynamique qui est un champ de type date.</span><span class="sxs-lookup"><span data-stu-id="5abc5-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="5abc5-192">Exemples : Créé le, Date de début, Début réel, Dernière durée de suspension, Fin réelle et Date d’échéance.</span><span class="sxs-lookup"><span data-stu-id="5abc5-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="5abc5-193">Paramètres > Personnalisations > Personnaliser le système > Entités > Tâche > Champs</span><span class="sxs-lookup"><span data-stu-id="5abc5-193">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="5abc5-194">createdon</span><span class="sxs-lookup"><span data-stu-id="5abc5-194">createdon</span></span> |<span data-ttu-id="5abc5-195">Date et heure</span><span class="sxs-lookup"><span data-stu-id="5abc5-195">Date and Time</span></span>
<span data-ttu-id="5abc5-196">Champs qui nécessitent à la fois un ID d’enregistrement et un type de recherche</span><span class="sxs-lookup"><span data-stu-id="5abc5-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="5abc5-197">Certains champs qui font référence à un autre enregistrement d’entité nécessitent l’ID d’enregistrement et le type de recherche.</span><span class="sxs-lookup"><span data-stu-id="5abc5-197">Some fields that reference another entity record require both the record ID and the lookup type.</span></span> |<span data-ttu-id="5abc5-198">Paramètres > Personnalisations > Personnaliser le système > Entités > Compte > Champs</span><span class="sxs-lookup"><span data-stu-id="5abc5-198">Settings > Customizations > Customize the System > Entities > Account > Fields</span></span>  | <span data-ttu-id="5abc5-199">accountid</span><span class="sxs-lookup"><span data-stu-id="5abc5-199">accountid</span></span>  | <span data-ttu-id="5abc5-200">Clé primaire</span><span class="sxs-lookup"><span data-stu-id="5abc5-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="5abc5-201">Exemples de champs supplémentaires nécessitant un ID d’enregistrement et un type de recherche</span><span class="sxs-lookup"><span data-stu-id="5abc5-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="5abc5-202">Pour compléter le tableau précédent, voici des exemples de champs supplémentaires qui ne fonctionnent pas avec les valeurs sélectionnées dans la liste de contenu dynamique.</span><span class="sxs-lookup"><span data-stu-id="5abc5-202">Expanding on the previous table, here are more examples of fields that don't work with values selected from the dynamic content list.</span></span> <span data-ttu-id="5abc5-203">À la place, ces champs nécessitent un ID d’enregistrement et un type de recherche saisis dans les champs de PowerApps.</span><span class="sxs-lookup"><span data-stu-id="5abc5-203">Instead, these fields require both a record ID and lookup type entered into the fields in PowerApps.</span></span>  
* <span data-ttu-id="5abc5-204">Propriétaire et Type de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="5abc5-204">Owner and Owner Type.</span></span> <span data-ttu-id="5abc5-205">Le champ Propriétaire doit être un ID d’enregistrement d’utilisateur ou d’équipe valide.</span><span class="sxs-lookup"><span data-stu-id="5abc5-205">The Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="5abc5-206">Le champ Type de propriétaire doit être **systemusers** ou **équipes**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-206">The Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="5abc5-207">Client et Type de client.</span><span class="sxs-lookup"><span data-stu-id="5abc5-207">Customer and Customer Type.</span></span> <span data-ttu-id="5abc5-208">Le champ Client doit être un ID d’enregistrement de compte ou de contact valide.</span><span class="sxs-lookup"><span data-stu-id="5abc5-208">The Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="5abc5-209">Le champ Type de propriétaire doit être **comptes** ou **contacts**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-209">The Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="5abc5-210">Concernant et Type Concernant.</span><span class="sxs-lookup"><span data-stu-id="5abc5-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="5abc5-211">Le champ Concernant doit être un ID d’enregistrement valide, tel qu’un ID d’enregistrement de contact ou de compte.</span><span class="sxs-lookup"><span data-stu-id="5abc5-211">The Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="5abc5-212">Le champ Type Concernant doit être le type de recherche pour l’enregistrement, tel que **comptes** ou **contacts**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-212">The Regarding Type must be the lookup type for the record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="5abc5-213">L’exemple d’action de création de tâche suivant ajoute un enregistrement de compte qui correspond à l’ID d’enregistrement en l’ajoutant au champ Concernant de la tâche.</span><span class="sxs-lookup"><span data-stu-id="5abc5-213">The following task creation action example adds an account record that corresponds to the record ID adding it to the regarding field of the task.</span></span>

![Flux : ID d’enregistrement et type de compte](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="5abc5-215">Cet exemple affecte également la tâche à un utilisateur spécifique en fonction de l’ID d’enregistrement d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5abc5-215">This example also assigns the task to a specific user based on the user's record ID.</span></span>

![Flux : ID d’enregistrement et type de compte](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="5abc5-217">Pour rechercher un ID d’enregistrement, consultez la section suivante : *Recherche de l’ID d’enregistrement*</span><span class="sxs-lookup"><span data-stu-id="5abc5-217">To find a record's ID, see the following section: *Find the record ID*</span></span>

## <a name="find-the-record-id"></a><span data-ttu-id="5abc5-218">Recherche de l’ID d’enregistrement</span><span class="sxs-lookup"><span data-stu-id="5abc5-218">Find the record ID</span></span>

1. <span data-ttu-id="5abc5-219">Ouvrez un enregistrement, comme un enregistrement de compte.</span><span class="sxs-lookup"><span data-stu-id="5abc5-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="5abc5-220">Dans la barre d’outils d’actions, cliquez sur **Ouvrir dans une nouvelle fenêtre** ![enregistrement - fenêtre indépendante](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="5abc5-220">On the actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="5abc5-221">Vous pouvez également cliquer sur **ENVOYER UN LIEN PAR COURRIER ÉLECTRONIQUE** dans la barre d’outils d’actions pour copier l’URL complète dans votre programme de messagerie par défaut.</span><span class="sxs-lookup"><span data-stu-id="5abc5-221">Alternatively, on the actions toolbar, to copy the full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="5abc5-222">L’ID d’enregistrement est affiché entre les caractères d’encodage %7b et %7d de l’URL.</span><span class="sxs-lookup"><span data-stu-id="5abc5-222">The record ID is displayed in between the %7b and %7d encoding characters of the URL.</span></span>

   ![Flux : ID d’enregistrement et type de compte](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="5abc5-224">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="5abc5-224">Troubleshooting</span></span>
<span data-ttu-id="5abc5-225">Pour résoudre les problèmes qui peuvent se produire lors d’une étape dans une application logique, affichez les détails de l’état de l’événement.</span><span class="sxs-lookup"><span data-stu-id="5abc5-225">To troubleshoot a failed step in a logic app, view the status details of the event.</span></span>

1. <span data-ttu-id="5abc5-226">Dans la zone **Logic Apps**, sélectionnez votre application logique, puis cliquez sur **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="5abc5-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="5abc5-227">La zone Résumé s’affiche et indique l’état d’exécution de l’application logique.</span><span class="sxs-lookup"><span data-stu-id="5abc5-227">The Summary area is shown and provides the run status for the logic app.</span></span> 

   ![État d’exécution de l’application logique](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="5abc5-229">Pour afficher plus d’informations sur les exécutions qui ont échoué, cliquez sur l’événement ayant rencontré des problèmes.</span><span class="sxs-lookup"><span data-stu-id="5abc5-229">To view more information about any failed runs, click the failed event.</span></span> <span data-ttu-id="5abc5-230">Pour développer une étape qui a échoué, cliquez sur cette étape.</span><span class="sxs-lookup"><span data-stu-id="5abc5-230">To expand a failed step, click that step.</span></span>

   ![Développer l’étape qui a échoué](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="5abc5-232">Les détails de l’étape s’affichent et peuvent aider à résoudre la cause du problème.</span><span class="sxs-lookup"><span data-stu-id="5abc5-232">The step details appear and can help troubleshoot the cause of the failure.</span></span>

   ![Détails de l’étape qui a échoué](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="5abc5-234">Pour plus d’informations sur la résolution des problèmes relatifs aux applications logiques, consultez [Diagnostic des échecs d’applications logiques](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="5abc5-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="5abc5-235">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="5abc5-235">Connector-specific details</span></span>

<span data-ttu-id="5abc5-236">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="5abc5-236">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5abc5-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5abc5-237">Next steps</span></span>
<span data-ttu-id="5abc5-238">Explorez les autres connecteurs disponibles dans les applications logiques en consultant notre [liste d’API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5abc5-238">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
