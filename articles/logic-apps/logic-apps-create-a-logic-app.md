---
title: aaaCreate votre premier flux de travail entre les applications cloud et les services de cloud computing - Azure Logic Apps | Documents Microsoft
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
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="d3be2-104">Créer votre première application logique tooautomate processus entre les applications cloud et les services de cloud computing</span><span class="sxs-lookup"><span data-stu-id="d3be2-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="d3be2-105">Vous pouvez automatiser des processus métier plus facilement et rapidement lorsque vous créez et exécutez des flux de travail et ce, sans avoir besoin d’écrire la plus petite ligne de code, grâce à [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d3be2-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="d3be2-106">Ce premier exemple montre comment toocreate un workflow d’application logique de base qui vérifie un RSS flux pour le nouveau contenu sur un site Web.</span><span class="sxs-lookup"><span data-stu-id="d3be2-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="d3be2-107">Lorsque de nouveaux éléments s’affichent dans les flux du site Web de hello, hello logique application envoie par courrier électronique à partir d’un compte Outlook ou Gmail.</span><span class="sxs-lookup"><span data-stu-id="d3be2-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="d3be2-108">toocreate et exécuter une application logique, vous avez besoin de ces éléments :</span><span class="sxs-lookup"><span data-stu-id="d3be2-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="d3be2-109">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d3be2-109">An Azure subscription.</span></span> <span data-ttu-id="d3be2-110">Si vous ne disposez d’aucun abonnement, vous pouvez [commencer par créer gratuitement un compte Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d3be2-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="d3be2-111">Sinon, vous pouvez souscrire à un [abonnement de type paiement à l’utilisation](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="d3be2-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="d3be2-112">Votre abonnement Azure est utilisé pour la facturation relative à l’utilisation des applications logiques.</span><span class="sxs-lookup"><span data-stu-id="d3be2-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="d3be2-113">Découvrez le fonctionnement du [contrôle de l’utilisation](../logic-apps/logic-apps-pricing.md) et de la [tarification](https://azure.microsoft.com/pricing/details/logic-apps) pour les applications logiques Azure.</span><span class="sxs-lookup"><span data-stu-id="d3be2-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="d3be2-114">En outre, cet exemple nécessite les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d3be2-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="d3be2-115">Un compte Gmail, Office 365 Outlook ou Outlook.com</span><span class="sxs-lookup"><span data-stu-id="d3be2-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="d3be2-116">Si vous disposez d’un [compte Microsoft](https://account.microsoft.com/account) personnel, vous possédez un compte Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="d3be2-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="d3be2-117">Sinon, si vous disposez d’un compte Azure professionnel ou scolaire, vous possédez un compte **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="d3be2-118">Un tooa lien du site Web flux RSS.</span><span class="sxs-lookup"><span data-stu-id="d3be2-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="d3be2-119">Cet exemple utilise hello [flux RSS pour les récits supérieur à partir du site Web de CNN.com hello](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="d3be2-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="d3be2-120">Ajouter un déclencheur qui démarre votre flux de travail</span><span class="sxs-lookup"><span data-stu-id="d3be2-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="d3be2-121">A [ *déclencheur* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) est un événement qui démarre le workflow d’application logique et hello premier élément qui a besoin votre application logique.</span><span class="sxs-lookup"><span data-stu-id="d3be2-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="d3be2-122">Connectez-vous à toohello [portail Azure](https://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="d3be2-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="d3be2-123">Dans le menu de gauche hello, choisissez **nouveau** > **intégration** > **application logique** comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="d3be2-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![portail Azure, nouveau, intégration d’entreprise, application logique](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="d3be2-125">Vous pouvez également choisir **nouveau**, puis dans la zone de recherche de hello, tapez `logic app`, puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="d3be2-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="d3be2-126">Ensuite, choisissez **Application logique** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="d3be2-127">Nommez votre application logique et sélectionnez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d3be2-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="d3be2-128">Créez ou sélectionnez un groupe de ressources Azure, qui permet d’organiser et de gérer des ressources Azure liées.</span><span class="sxs-lookup"><span data-stu-id="d3be2-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="d3be2-129">Enfin, sélectionnez emplacement du centre de données hello pour l’hébergement de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="d3be2-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="d3be2-130">Lorsque vous êtes prêt, choisissez **code confidentiel toodashboard** , puis **créer**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![Détails de l’application logique](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="d3be2-132">Lorsque vous sélectionnez **toodashboard du code confidentiel**, votre application logique apparaît sur hello du tableau de bord Azure après le déploiement et s’ouvre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d3be2-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="d3be2-133">Si votre application logique n’apparaît pas dans le tableau de bord hello sur hello **toutes les ressources** vignette, choisissez **consultez plus**, puis sélectionnez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="d3be2-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="d3be2-134">Ou, dans le menu de gauche hello, choisissez **davantage de services**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="d3be2-135">Sous **Intégration d’entreprise**, choisissez **Applications logiques** et sélectionnez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="d3be2-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="d3be2-136">Lorsque vous ouvrez votre logique d’application pour hello première fois, hello Concepteur de logique d’application affiche les modèles que vous pouvez utiliser tooget a démarré.</span><span class="sxs-lookup"><span data-stu-id="d3be2-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="d3be2-137">Pour l’instant, choisissez **Application logique vide**, afin de développer votre application logique à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="d3be2-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="d3be2-138">Hello Concepteur d’application logique s’ouvre et affiche les services disponibles et *déclencheurs* que vous pouvez utiliser dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="d3be2-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="d3be2-139">Dans la zone de recherche de hello, tapez `RSS`, puis sélectionnez ce déclencheur : **RSS - lorsqu’un élément de flux est publié.**</span><span class="sxs-lookup"><span data-stu-id="d3be2-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Déclencheur RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="d3be2-141">Entrez un lien de hello pour les flux RSS du site Web de hello que vous souhaitez tootrack.</span><span class="sxs-lookup"><span data-stu-id="d3be2-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="d3be2-142">Vous pouvez également modifier la **fréquence** et l’**intervalle**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="d3be2-143">Ces paramètres déterminent la fréquence à laquelle votre application logique recherche de nouveaux éléments et renvoie tous les éléments détectés pendant cet intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="d3be2-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="d3be2-144">Pour cet exemple, nous allons vérifier tous les jours pour les récits supérieur publiées du site Web CNN toohello.</span><span class="sxs-lookup"><span data-stu-id="d3be2-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![Définir un déclencheur avec le flux RSS, la fréquence et l’intervalle](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="d3be2-146">Enregistrez votre travail pour commencer</span><span class="sxs-lookup"><span data-stu-id="d3be2-146">Save your work for now.</span></span> <span data-ttu-id="d3be2-147">(Dans la barre de commandes du concepteur hello, choisissez **enregistrer**.)</span><span class="sxs-lookup"><span data-stu-id="d3be2-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![Enregistrer votre application logique](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="d3be2-149">Lorsque vous enregistrez, votre application logique soit disponible, mais actuellement, votre application logique vérifie uniquement les nouveaux éléments dans hello spécifié flux RSS.</span><span class="sxs-lookup"><span data-stu-id="d3be2-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="d3be2-150">toomake cet exemple plus utile, que nous ajoutons une action de votre application de la logique s’exécute après votre déclencheur est activé.</span><span class="sxs-lookup"><span data-stu-id="d3be2-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="d3be2-151">Ajouter une action qui répond tooyour déclencheur</span><span class="sxs-lookup"><span data-stu-id="d3be2-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="d3be2-152">Une [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) est une tâche effectuée par le flux de travail de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="d3be2-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="d3be2-153">Après avoir ajouté une application de la logique de déclencheur tooyour, vous pouvez ajouter un opérateur de tooperform action avec les données générées par ce déclencheur.</span><span class="sxs-lookup"><span data-stu-id="d3be2-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="d3be2-154">Dans notre exemple, nous permet maintenant d’ajouter une action qui envoie un e-mail lorsque de nouveaux éléments s’affichent dans le flux RSS du site Web de hello.</span><span class="sxs-lookup"><span data-stu-id="d3be2-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="d3be2-155">Dans le Concepteur de hello, sous votre déclencheur, choisissez **nouvelle étape** > **ajouter une action** comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="d3be2-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Ajouter une action](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="d3be2-157">Hello concepteur affiche [connecteurs disponibles](../connectors/apis-list.md) afin que vous puissiez sélectionner une action tooperform lorsque le déclencheur est activé.</span><span class="sxs-lookup"><span data-stu-id="d3be2-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="d3be2-158">En fonction de votre compte de messagerie, les étapes hello pour Outlook ou Gmail.</span><span class="sxs-lookup"><span data-stu-id="d3be2-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="d3be2-159">messagerie toosend à partir de votre compte Outlook, dans la zone de recherche de hello, entrez `outlook`.</span><span class="sxs-lookup"><span data-stu-id="d3be2-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="d3be2-160">Sous **Services**, choisissez **Outlook.com** pour les comptes Microsoft personnels, ou **Office 365 Outlook** pour les comptes Azure professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="d3be2-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="d3be2-161">Sous **Actions**, sélectionnez **Envoi d’un courrier électronique**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-161">Under **Actions**, select **Send an email**.</span></span>

       ![Sélectionner l’action Envoi d’un courrier électronique d’Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="d3be2-163">messagerie toosend à partir de votre compte Gmail, dans la zone de recherche de hello, entrez `gmail`.</span><span class="sxs-lookup"><span data-stu-id="d3be2-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="d3be2-164">Sous **Actions**, sélectionnez **Envoyer un e-mail**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-164">Under **Actions**, select **Send email**.</span></span>

       ![Choisissez Gmail - Envoyer un e-mail.](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="d3be2-166">Lorsque vous êtes invité à entrer les informations d’identification, connectez-vous à hello username et password pour votre compte de messagerie.</span><span class="sxs-lookup"><span data-stu-id="d3be2-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="d3be2-167">Fournir des détails de hello pour cette action, comme l’adresse de messagerie de destination hello et choisir les paramètres hello pour hello données tooinclude par courrier électronique de hello, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d3be2-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![Sélectionnez les données tooinclude par courrier électronique](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="d3be2-169">Ainsi, si vous avez choisi Outlook, votre application logique peut ressembler à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="d3be2-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Application logique terminée](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="d3be2-171">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="d3be2-171">Save your changes.</span></span> <span data-ttu-id="d3be2-172">(Dans la barre de commandes du concepteur hello, choisissez **enregistrer**.)</span><span class="sxs-lookup"><span data-stu-id="d3be2-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="d3be2-173">Vous pouvez maintenant exécuter votre application logique manuellement, à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="d3be2-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="d3be2-174">Dans la barre de commandes du concepteur hello, choisissez **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="d3be2-175">Sinon, vous pouvez laisser votre application logique vérifier hello spécifié selon une planification hello que vous définissez des flux RSS.</span><span class="sxs-lookup"><span data-stu-id="d3be2-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="d3be2-176">Si votre application logique détecte les nouveaux éléments, hello logique application envoie par courrier électronique qui inclut vos données sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="d3be2-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="d3be2-177">Si aucun nouvel élément n’est trouvé, votre application logique ignore action hello qui envoie le courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="d3be2-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="d3be2-178">toomonitor et vérification de votre application de la logique de l’exécuter et déclencher l’historique, dans le menu Application logique, choisissent **vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Surveiller et afficher l’historique de déclencheur et d’exécution de votre application logique](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="d3be2-180">Si vous ne trouvez pas les données de salutation que vous attendez, sur la barre de commandes hello, essayez de choisir **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="d3be2-181">toolearn plus en détail l’état de l’application de votre logique ou exécutez et déclencher l’historique ou toodiagnose votre application logique, consultez [dépanner votre application logique](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="d3be2-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="d3be2-182">Votre application logique poursuit son exécution jusqu’à ce que vous la désactiviez.</span><span class="sxs-lookup"><span data-stu-id="d3be2-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="d3be2-183">tooturn hors de votre application pour l’instant, dans le menu Application logique, choisissez **vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="d3be2-184">Dans la barre de commandes hello, choisissez **désactiver**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="d3be2-185">Félicitations ! Vous venez de configurer et d’exécuter votre première application logique de base.</span><span class="sxs-lookup"><span data-stu-id="d3be2-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="d3be2-186">Vous avez également appris comment créer des flux de travaux qui automatisent les processus et intégrer des services cloud et applications cloud, aisément et sans rédiger la moindre ligne de code.</span><span class="sxs-lookup"><span data-stu-id="d3be2-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="d3be2-187">Gérer votre application logique</span><span class="sxs-lookup"><span data-stu-id="d3be2-187">Manage your logic app</span></span>

<span data-ttu-id="d3be2-188">toomanage votre application, vous pouvez effectuer des tâches telles que vérifier l’état de hello, modifier, afficher l’historique, désactiver ou supprimer votre application logique.</span><span class="sxs-lookup"><span data-stu-id="d3be2-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="d3be2-189">Connectez-vous à toohello [portail Azure](https://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="d3be2-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="d3be2-190">Dans le menu de gauche hello, choisissez **davantage de services**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="d3be2-191">Sous **Intégration d’entreprise**, choisissez **Applications logiques**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="d3be2-192">Sélectionnez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="d3be2-192">Select your logic app.</span></span> 

   <span data-ttu-id="d3be2-193">Dans le menu d’application hello logique, vous pouvez trouver ces tâches de gestion d’application logique :</span><span class="sxs-lookup"><span data-stu-id="d3be2-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="d3be2-194">Task</span><span class="sxs-lookup"><span data-stu-id="d3be2-194">Task</span></span>|<span data-ttu-id="d3be2-195">Étapes</span><span class="sxs-lookup"><span data-stu-id="d3be2-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="d3be2-196">Afficher l’historique d’exécution et l’état de votre application, ainsi que des informations générales</span><span class="sxs-lookup"><span data-stu-id="d3be2-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="d3be2-197">Choisissez **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="d3be2-198">Modifier votre application</span><span class="sxs-lookup"><span data-stu-id="d3be2-198">Edit your app</span></span> | <span data-ttu-id="d3be2-199">Choisissez **Concepteur d’application logique**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="d3be2-200">Afficher la définition JSON du flux de travail de votre application</span><span class="sxs-lookup"><span data-stu-id="d3be2-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="d3be2-201">Choisissez **Affichage du code de l’application logique**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="d3be2-202">Afficher les opérations effectuées sur votre application logique</span><span class="sxs-lookup"><span data-stu-id="d3be2-202">View operations performed on your logic app</span></span> | <span data-ttu-id="d3be2-203">Choisissez **Journal d’activité**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="d3be2-204">Afficher les anciennes versions de votre application logique</span><span class="sxs-lookup"><span data-stu-id="d3be2-204">View past versions for your logic app</span></span> | <span data-ttu-id="d3be2-205">Choisissez **Versions**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="d3be2-206">Désactiver votre application temporairement</span><span class="sxs-lookup"><span data-stu-id="d3be2-206">Turn off your app temporarily</span></span> | <span data-ttu-id="d3be2-207">Choisissez **vue d’ensemble**, puis dans la barre de commandes hello, choisissez **désactiver**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="d3be2-208">Supprimer votre application</span><span class="sxs-lookup"><span data-stu-id="d3be2-208">Delete your app</span></span> | <span data-ttu-id="d3be2-209">Choisissez **vue d’ensemble**, puis dans la barre de commandes hello, choisissez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="d3be2-210">Entrez le nom de votre application logique et choisissez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="d3be2-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="d3be2-211">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="d3be2-211">Get help</span></span>

<span data-ttu-id="d3be2-212">tooask questions, répondre aux questions et savoir quels autres Azure Logic Apps font les utilisateurs, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="d3be2-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="d3be2-213">toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="d3be2-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3be2-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3be2-214">Next steps</span></span>

*  [<span data-ttu-id="d3be2-215">Ajouter des conditions et exécuter des flux de travail</span><span class="sxs-lookup"><span data-stu-id="d3be2-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="d3be2-216">Configuration d’un flux de travail à l’aide d’un modèle prédéfini pour démarrer rapidement</span><span class="sxs-lookup"><span data-stu-id="d3be2-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="d3be2-217">Créer une application logique à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="d3be2-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
