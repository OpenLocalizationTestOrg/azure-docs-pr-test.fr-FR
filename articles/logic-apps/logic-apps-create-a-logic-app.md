---
title: "Créer votre premier flux de travail entre des applications cloud et des services cloud : Azure Logic Apps| Microsoft Docs"
description: "Automatisez les processus d’entreprise dans le cas de scénarios d’intégration des systèmes et des Applications d’Entreprise (IAE) en créant et en exécutant des flux de travail dans Azure Logic Apps."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "flux de travail, applications cloud, services cloud, processus d’entreprise, intégration de systèmes, intégration d’applications d’entreprise, IAE"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 204bf123509729b60b55c306050cef54aa7fecc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-logic-app-workflow-to-automate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="9b32e-104">Créer votre premier flux de travail d’application logique pour automatiser les processus entre les applications cloud et les services cloud</span><span class="sxs-lookup"><span data-stu-id="9b32e-104">Create your first logic app workflow to automate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="9b32e-105">Vous pouvez automatiser des processus métier plus facilement et rapidement lorsque vous créez et exécutez des flux de travail et ce, sans avoir besoin d’écrire la plus petite ligne de code, grâce à [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="9b32e-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="9b32e-106">Le premier exemple indique comment créer un flux de travail d’application logique de base, qui vérifie la présence éventuelle de nouveau contenu dans un flux RSS, sur un site web.</span><span class="sxs-lookup"><span data-stu-id="9b32e-106">This first example shows how to create a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="9b32e-107">Lorsque de nouveaux éléments s’affichent dans le flux du site web, l’application logique envoie un e-mail depuis un compte Outlook ou Gmail.</span><span class="sxs-lookup"><span data-stu-id="9b32e-107">When new items appear in the website's feed, the logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="9b32e-108">Pour créer et exécuter une application logique, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9b32e-108">To create and run a logic app, you need these items:</span></span>

* <span data-ttu-id="9b32e-109">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9b32e-109">An Azure subscription.</span></span> <span data-ttu-id="9b32e-110">Si vous ne disposez d’aucun abonnement, vous pouvez [commencer par créer gratuitement un compte Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9b32e-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="9b32e-111">Sinon, vous pouvez souscrire à un [abonnement de type paiement à l’utilisation](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="9b32e-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="9b32e-112">Votre abonnement Azure est utilisé pour la facturation relative à l’utilisation des applications logiques.</span><span class="sxs-lookup"><span data-stu-id="9b32e-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="9b32e-113">Découvrez le fonctionnement du [contrôle de l’utilisation](../logic-apps/logic-apps-pricing.md) et de la [tarification](https://azure.microsoft.com/pricing/details/logic-apps) pour les applications logiques Azure.</span><span class="sxs-lookup"><span data-stu-id="9b32e-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="9b32e-114">En outre, cet exemple nécessite les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9b32e-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="9b32e-115">Un compte Gmail, Office 365 Outlook ou Outlook.com</span><span class="sxs-lookup"><span data-stu-id="9b32e-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="9b32e-116">Si vous disposez d’un [compte Microsoft](https://account.microsoft.com/account) personnel, vous possédez un compte Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="9b32e-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="9b32e-117">Sinon, si vous disposez d’un compte Azure professionnel ou scolaire, vous possédez un compte **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="9b32e-118">Un lien vers le flux RSS d’un site web.</span><span class="sxs-lookup"><span data-stu-id="9b32e-118">A link to a website's RSS feed.</span></span> <span data-ttu-id="9b32e-119">Cet exemple utilise le [flux RSS pour les témoignages du site web CNN.com](http://rss.cnn.com/rss/cnn_topstories.rss) : `http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="9b32e-119">This example uses the [RSS feed for top stories from the CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="9b32e-120">Ajouter un déclencheur qui démarre votre flux de travail</span><span class="sxs-lookup"><span data-stu-id="9b32e-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="9b32e-121">Un [*déclencheur*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) est un événement qui démarre le flux de travail de votre application logique. Il s’agit du premier élément requis par votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9b32e-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is the first item that your logic app needs.</span></span>

1. <span data-ttu-id="9b32e-122">Connectez-vous au [portail Azure](https://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="9b32e-122">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="9b32e-123">Dans le menu de gauche, choisissez **Nouveau** > **Intégration d’entreprise** > **Application logique**, comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="9b32e-123">From the left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![portail Azure, nouveau, intégration d’entreprise, application logique](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="9b32e-125">Vous pouvez également sélectionner **Nouveau**, puis dans la zone de recherche, tapez `logic app`, puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="9b32e-125">You can also choose **New**, then in the search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="9b32e-126">Ensuite, choisissez **Application logique** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="9b32e-127">Nommez votre application logique et sélectionnez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9b32e-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="9b32e-128">Créez ou sélectionnez un groupe de ressources Azure, qui permet d’organiser et de gérer des ressources Azure liées.</span><span class="sxs-lookup"><span data-stu-id="9b32e-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="9b32e-129">Enfin, sélectionnez l’emplacement du centre de données pour l’hébergement de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9b32e-129">Finally, select the datacenter location for hosting your logic app.</span></span> <span data-ttu-id="9b32e-130">Lorsque vous êtes prêt, choisissez **Épingler au tableau de bord**, puis **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-130">When you're ready, choose **Pin to dashboard** and then **Create**.</span></span>

     ![Détails de l’application logique](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="9b32e-132">Lorsque vous sélectionnez l’option **Épingler au tableau de bord**, votre application logique s’affiche dans le tableau de bord Azure après le déploiement et s’ouvre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="9b32e-132">When you select **Pin to dashboard**, your logic app appears on the Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="9b32e-133">Si votre application logique ne figure pas dans le tableau de bord, accédez à la mosaïque **Toutes les ressources**, choisissez **En savoir plus**, puis sélectionnez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9b32e-133">If your logic app doesn't appear on the dashboard, on the **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="9b32e-134">Vous pouvez également cliquer sur **Plus de services** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="9b32e-134">Or on the left menu, choose **More services**.</span></span> <span data-ttu-id="9b32e-135">Sous **Intégration d’entreprise**, choisissez **Applications logiques** et sélectionnez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9b32e-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="9b32e-136">Lorsque vous ouvrez votre application logique pour la première fois, le Concepteur d’application logique affiche les modèles que vous pouvez utiliser pour commencer.</span><span class="sxs-lookup"><span data-stu-id="9b32e-136">When you open your logic app for the first time, the Logic App Designer shows templates that you can use to get started.</span></span> <span data-ttu-id="9b32e-137">Pour l’instant, choisissez **Application logique vide**, afin de développer votre application logique à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="9b32e-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="9b32e-138">Le Concepteur d’application logique s’ouvre et affiche des services disponibles et *déclencheurs* que vous pouvez utiliser dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9b32e-138">The Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="9b32e-139">Dans la zone de recherche, saisissez `RSS`, puis sélectionnez le déclencheur suivant : **RSS - Lors de la publication d’un élément de flux**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-139">In the search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Déclencheur RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="9b32e-141">Indiquez le lien vers le flux RSS du site web dont vous souhaitez effectuer un suivi.</span><span class="sxs-lookup"><span data-stu-id="9b32e-141">Enter the link for the website's RSS feed that you want to track.</span></span> 

     <span data-ttu-id="9b32e-142">Vous pouvez également modifier la **fréquence** et l’**intervalle**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="9b32e-143">Ces paramètres déterminent la fréquence à laquelle votre application logique recherche de nouveaux éléments et renvoie tous les éléments détectés pendant cet intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="9b32e-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="9b32e-144">Pour les besoins de cet exemple, nous allons rechercher tous les jours les témoignages publiés sur le site web CNN.</span><span class="sxs-lookup"><span data-stu-id="9b32e-144">For this example, let's check every day for   top stories posted to the CNN website.</span></span>

     ![Définir un déclencheur avec le flux RSS, la fréquence et l’intervalle](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="9b32e-146">Enregistrez votre travail pour commencer</span><span class="sxs-lookup"><span data-stu-id="9b32e-146">Save your work for now.</span></span> <span data-ttu-id="9b32e-147">(dans la barre de commandes du concepteur, choisissez **Enregistrer**.)</span><span class="sxs-lookup"><span data-stu-id="9b32e-147">(On the designer command bar, choose **Save**.)</span></span>

   ![Enregistrer votre application logique](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="9b32e-149">Lorsque vous l’enregistrez, votre application logique est mise en service. À l’heure actuelle, elle vérifie uniquement la présence de nouveaux éléments dans le flux RSS spécifié.</span><span class="sxs-lookup"><span data-stu-id="9b32e-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in the specified RSS feed.</span></span> 
   <span data-ttu-id="9b32e-150">Pour rendre cet exemple plus utile, nous ajoutons une action que votre application logique exécute après l’activation de votre déclencheur.</span><span class="sxs-lookup"><span data-stu-id="9b32e-150">To make this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-to-your-trigger"></a><span data-ttu-id="9b32e-151">Ajouter une action de réaction à votre déclencheur</span><span class="sxs-lookup"><span data-stu-id="9b32e-151">Add an action that responds to your trigger</span></span>

<span data-ttu-id="9b32e-152">Une [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) est une tâche effectuée par le flux de travail de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9b32e-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="9b32e-153">Après avoir ajouté un déclencheur à votre application logique, vous pouvez ajouter une action permettant d’effectuer des opérations avec les données générées par ce déclencheur.</span><span class="sxs-lookup"><span data-stu-id="9b32e-153">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="9b32e-154">Dans notre exemple, nous ajoutons maintenant une action qui envoie un e-mail lorsque de nouveaux éléments apparaissent dans le flux RSS du site web.</span><span class="sxs-lookup"><span data-stu-id="9b32e-154">For our example, we now add an action that sends email when new items appear in the website's RSS feed.</span></span>

1. <span data-ttu-id="9b32e-155">Dans le concepteur, sous votre déclencheur, choisissez **Nouvelle étape** > **Ajouter une action**, comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="9b32e-155">In the designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Ajouter une action](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="9b32e-157">Le concepteur affiche les [connecteurs disponibles](../connectors/apis-list.md), afin que vous puissiez sélectionner une action à exécuter lorsque votre déclencheur est activé.</span><span class="sxs-lookup"><span data-stu-id="9b32e-157">The designer shows [available connectors](../connectors/apis-list.md) so that you can select an action to perform when your trigger fires.</span></span>

2. <span data-ttu-id="9b32e-158">En fonction de votre compte de messagerie, suivez les étapes relatives à Outlook ou Gmail.</span><span class="sxs-lookup"><span data-stu-id="9b32e-158">Based on your email account, follow the steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="9b32e-159">Pour envoyer un e-mail à partir de votre compte Outlook, saisissez `outlook` dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="9b32e-159">To send email from your Outlook account, in the search box, enter `outlook`.</span></span> <span data-ttu-id="9b32e-160">Sous **Services**, choisissez **Outlook.com** pour les comptes Microsoft personnels, ou **Office 365 Outlook** pour les comptes Azure professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="9b32e-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="9b32e-161">Sous **Actions**, sélectionnez **Envoi d’un courrier électronique**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-161">Under **Actions**, select **Send an email**.</span></span>

       ![Sélectionner l’action Envoi d’un courrier électronique d’Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="9b32e-163">Pour envoyer un e-mail à partir de votre compte Gmail, saisissez `gmail` dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="9b32e-163">To send email from your Gmail account, in the search box, enter `gmail`.</span></span> 
   <span data-ttu-id="9b32e-164">Sous **Actions**, sélectionnez **Envoyer un e-mail**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-164">Under **Actions**, select **Send email**.</span></span>

       ![Choisissez Gmail - Envoyer un e-mail.](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="9b32e-166">Lorsque vous êtes invité à saisir des informations d’identification, connectez-vous avec le nom d’utilisateur et le mot de passe de votre compte de messagerie.</span><span class="sxs-lookup"><span data-stu-id="9b32e-166">When you're prompted for credentials, sign in with the username and password for your email account.</span></span> 

4. <span data-ttu-id="9b32e-167">Fournissez les détails de cette action, comme l’adresse de messagerie de destination, et choisissez les paramètres relatifs aux données à inclure dans l’e-mail, par exemple :</span><span class="sxs-lookup"><span data-stu-id="9b32e-167">Provide the details for this action, like the destination email address, and choose the parameters for the data to include in the email, for example:</span></span>

   ![Sélectionner les données à inclure dans l’e-mail](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="9b32e-169">Ainsi, si vous avez choisi Outlook, votre application logique peut ressembler à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="9b32e-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Application logique terminée](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="9b32e-171">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="9b32e-171">Save your changes.</span></span> <span data-ttu-id="9b32e-172">(dans la barre de commandes du concepteur, choisissez **Enregistrer**.)</span><span class="sxs-lookup"><span data-stu-id="9b32e-172">(On the designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="9b32e-173">Vous pouvez maintenant exécuter votre application logique manuellement, à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="9b32e-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="9b32e-174">Dans la barre de commandes du concepteur, choisissez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-174">On the designer command bar, choose **Run**.</span></span> <span data-ttu-id="9b32e-175">Sinon, vous pouvez laisser votre application logique vérifier le flux RSS spécifié selon la planification que vous avez configurée.</span><span class="sxs-lookup"><span data-stu-id="9b32e-175">Otherwise, you can let your logic app check the specified RSS feed based on the schedule that you set up.</span></span>

   <span data-ttu-id="9b32e-176">Si votre application logique détecte de nouveaux éléments, l’application logique envoie un e-mail qui inclut vos données sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="9b32e-176">If your logic app finds new items, the logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="9b32e-177">Si aucun nouvel élément n’est détecté, votre application logique ignore l’action qui envoie un e-mail.</span><span class="sxs-lookup"><span data-stu-id="9b32e-177">If no new items are found, your logic app skips the action that sends email.</span></span>

7. <span data-ttu-id="9b32e-178">Pour surveiller et vérifier l’historique de déclencheur et d’exécution de votre application logique, choisissez **Vue d’ensemble** dans le menu de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9b32e-178">To monitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Surveiller et afficher l’historique de déclencheur et d’exécution de votre application logique](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="9b32e-180">Si vous ne trouvez pas les données que vous attendez, choisissez **Actualiser** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="9b32e-180">If you don't find the data that you expect, on the command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="9b32e-181">Pour en savoir plus sur l’état de votre application logique ou de l’historique de déclencheur et d’exécution correspondant, ou pour diagnostiquer les échecs de votre application logique, voir [Diagnostiquer des échecs d’applications logiques](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="9b32e-181">To learn more about your logic app's status or run and trigger history, or to diagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="9b32e-182">Votre application logique poursuit son exécution jusqu’à ce que vous la désactiviez.</span><span class="sxs-lookup"><span data-stu-id="9b32e-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="9b32e-183">Pour désactiver votre application de façon temporaire, choisissez **Vue d’ensemble** dans le menu de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9b32e-183">To turn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="9b32e-184">Choisissez **Désactiver** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="9b32e-184">On the command bar, choose **Disable**.</span></span>

<span data-ttu-id="9b32e-185">Félicitations ! Vous venez de configurer et d’exécuter votre première application logique de base.</span><span class="sxs-lookup"><span data-stu-id="9b32e-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="9b32e-186">Vous avez également appris comment créer des flux de travaux qui automatisent les processus et intégrer des services cloud et applications cloud, aisément et sans rédiger la moindre ligne de code.</span><span class="sxs-lookup"><span data-stu-id="9b32e-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="9b32e-187">Gérer votre application logique</span><span class="sxs-lookup"><span data-stu-id="9b32e-187">Manage your logic app</span></span>

<span data-ttu-id="9b32e-188">Vous pouvez effectuer des tâches telles que la vérification de l’état, la modification, l’affichage de l’historique, la désactivation ou la suppression de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9b32e-188">To manage your app, you can perform tasks like check the status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="9b32e-189">Connectez-vous au [portail Azure](https://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="9b32e-189">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="9b32e-190">Cliquez sur l’option **Plus de services** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="9b32e-190">On the left menu, choose **More services**.</span></span> <span data-ttu-id="9b32e-191">Sous **Intégration d’entreprise**, choisissez **Applications logiques**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="9b32e-192">Sélectionnez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9b32e-192">Select your logic app.</span></span> 

   <span data-ttu-id="9b32e-193">Dans le menu de l’application logique, vous pouvez accéder à ces tâches de gestion de l’application logique :</span><span class="sxs-lookup"><span data-stu-id="9b32e-193">In the logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="9b32e-194">Task</span><span class="sxs-lookup"><span data-stu-id="9b32e-194">Task</span></span>|<span data-ttu-id="9b32e-195">Étapes</span><span class="sxs-lookup"><span data-stu-id="9b32e-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="9b32e-196">Afficher l’historique d’exécution et l’état de votre application, ainsi que des informations générales</span><span class="sxs-lookup"><span data-stu-id="9b32e-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="9b32e-197">Choisissez **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="9b32e-198">Modifier votre application</span><span class="sxs-lookup"><span data-stu-id="9b32e-198">Edit your app</span></span> | <span data-ttu-id="9b32e-199">Choisissez **Concepteur d’application logique**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="9b32e-200">Afficher la définition JSON du flux de travail de votre application</span><span class="sxs-lookup"><span data-stu-id="9b32e-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="9b32e-201">Choisissez **Affichage du code de l’application logique**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="9b32e-202">Afficher les opérations effectuées sur votre application logique</span><span class="sxs-lookup"><span data-stu-id="9b32e-202">View operations performed on your logic app</span></span> | <span data-ttu-id="9b32e-203">Choisissez **Journal d’activité**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="9b32e-204">Afficher les anciennes versions de votre application logique</span><span class="sxs-lookup"><span data-stu-id="9b32e-204">View past versions for your logic app</span></span> | <span data-ttu-id="9b32e-205">Choisissez **Versions**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="9b32e-206">Désactiver votre application temporairement</span><span class="sxs-lookup"><span data-stu-id="9b32e-206">Turn off your app temporarily</span></span> | <span data-ttu-id="9b32e-207">Choisissez **Vue d’ensemble** et, dans la barre de commandes, sélectionnez **Désactiver**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-207">Choose **Overview**, then on the command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="9b32e-208">Supprimer votre application</span><span class="sxs-lookup"><span data-stu-id="9b32e-208">Delete your app</span></span> | <span data-ttu-id="9b32e-209">Choisissez **Vue d’ensemble** et, dans la barre de commandes, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-209">Choose **Overview**, then on the command bar, choose **Delete**.</span></span> <span data-ttu-id="9b32e-210">Entrez le nom de votre application logique et choisissez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="9b32e-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="9b32e-211">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="9b32e-211">Get help</span></span>

<span data-ttu-id="9b32e-212">Pour poser des questions ou y répondre et voir ce que font les autres utilisateurs d’Azure Logic Apps, visitez le [Forum Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="9b32e-212">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="9b32e-213">Afin d’améliorer Azure Logic Apps ainsi que les connecteurs, votez pour des idées ou soumettez-en sur le [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="9b32e-213">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b32e-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b32e-214">Next steps</span></span>

*  [<span data-ttu-id="9b32e-215">Ajouter des conditions et exécuter des flux de travail</span><span class="sxs-lookup"><span data-stu-id="9b32e-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="9b32e-216">Configuration d’un flux de travail à l’aide d’un modèle prédéfini pour démarrer rapidement</span><span class="sxs-lookup"><span data-stu-id="9b32e-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="9b32e-217">Créer une application logique à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="9b32e-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
