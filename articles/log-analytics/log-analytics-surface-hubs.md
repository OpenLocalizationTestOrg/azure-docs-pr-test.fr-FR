---
title: "Surveiller les Surface Hubs avec Azure Log Analytics | Microsoft Docs"
description: "La solution Surface Hub permet de suivre l’intégrité de vos Surface Hubs et de comprendre comment ils sont utilisés."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6ecd0d09589fec85c1633f528afc1165c346b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-to-track-their-health"></a><span data-ttu-id="bf018-103">Surveiller les Surface Hubs avec Log Analytics pour suivre leur intégrité</span><span class="sxs-lookup"><span data-stu-id="bf018-103">Monitor Surface Hubs with Log Analytics to track their health</span></span>

![Symbole de Surface Hub](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="bf018-105">Cet article décrit comment utiliser la solution Surface Hub dans Log Analytics pour surveiller des appareils Microsoft Surface Hub avec Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="bf018-105">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="bf018-106">Log Analytics vous aide à suivre l’intégrité de vos Surface Hubs ainsi qu’à comprendre comment ils sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="bf018-106">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="bf018-107">Chaque Surface Hub a un Microsoft Monitoring Agent installé.</span><span class="sxs-lookup"><span data-stu-id="bf018-107">Each Surface Hub has the Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="bf018-108">C’est via cet agent que vous pouvez envoyer des données de votre Surface Hub à OMS.</span><span class="sxs-lookup"><span data-stu-id="bf018-108">Its through the agent that you can send data from your Surface Hub to OMS.</span></span> <span data-ttu-id="bf018-109">Les fichiers journaux sont lus à partir de vos Surface Hubs, puis envoyés au Service OMS.</span><span class="sxs-lookup"><span data-stu-id="bf018-109">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span></span> <span data-ttu-id="bf018-110">Des problèmes tels que des serveurs hors connexion, un calendrier qui ne se synchronise pas, ou un compte d’appareil incapable de se connecter à Skype s’affichent sur le tableau de bord Surface Hub d’OMS.</span><span class="sxs-lookup"><span data-stu-id="bf018-110">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span></span> <span data-ttu-id="bf018-111">Les données du tableau de bord vous permettent d’identifier les appareils qui ne sont pas en cours d’exécution ou qui rencontrent d’autres problèmes, voire d’appliquer des correctifs pour les problèmes détectés.</span><span class="sxs-lookup"><span data-stu-id="bf018-111">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="bf018-112">Installation et configuration de la solution</span><span class="sxs-lookup"><span data-stu-id="bf018-112">Installing and configuring the solution</span></span>
<span data-ttu-id="bf018-113">Utilisez les informations suivantes pour installer et configurer la solution.</span><span class="sxs-lookup"><span data-stu-id="bf018-113">Use the following information to install and configure the solution.</span></span> <span data-ttu-id="bf018-114">Pour gérer vos Surface Hubs à partir de Microsoft Operations Management Suite (OMS), vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bf018-114">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span></span>

* <span data-ttu-id="bf018-115">Un abonnement valide à [OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="bf018-115">A valid subscription to [OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="bf018-116">Un niveau d’[abonnement OMS](https://azure.microsoft.com/pricing/details/log-analytics/) prenant en charge le nombre d’appareils à analyser.</span><span class="sxs-lookup"><span data-stu-id="bf018-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span></span> <span data-ttu-id="bf018-117">La tarification d’OMS varie selon le nombre d’appareils inscrits et la quantité de données traitées.</span><span class="sxs-lookup"><span data-stu-id="bf018-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="bf018-118">Vous devez prendre cela en compte lors de la planification de votre déploiement de Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="bf018-118">You'll want to take this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="bf018-119">Ensuite, vous allez soit ajouter un abonnement OMS à votre abonnement Microsoft Azure, soit créer un espace de travail directement via le portail OMS.</span><span class="sxs-lookup"><span data-stu-id="bf018-119">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span></span> <span data-ttu-id="bf018-120">Pour des instructions détaillées sur ces deux méthodes, voir [Prise en main de Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bf018-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="bf018-121">Une fois l’abonnement OMS créé, vous pouvez inscrire vos appareils Surface Hub de deux façons :</span><span class="sxs-lookup"><span data-stu-id="bf018-121">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span></span>

* <span data-ttu-id="bf018-122">automatiquement via Intune ;</span><span class="sxs-lookup"><span data-stu-id="bf018-122">Automatically through Intune</span></span>
* <span data-ttu-id="bf018-123">manuellement, via les **Paramètres** de votre appareil Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="bf018-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="bf018-124">Configurez l’analyse</span><span class="sxs-lookup"><span data-stu-id="bf018-124">Set up monitoring</span></span>
<span data-ttu-id="bf018-125">Vous pouvez analyser l’intégrité et l’activité de votre Surface Hub à l’aide de Log Analytics dans OMS.</span><span class="sxs-lookup"><span data-stu-id="bf018-125">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="bf018-126">Vous pouvez inscrire le Surface Hub dans OMS via Intune, ou localement via les **Paramètres** du Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="bf018-126">You can enroll the Surface Hub in OMS by using Intune, or locally by using **Settings** on the Surface Hub.</span></span>

## <a name="connect-surface-hubs-to-oms-through-intune"></a><span data-ttu-id="bf018-127">Connecter des Surface Hubs à OMS via Intune</span><span class="sxs-lookup"><span data-stu-id="bf018-127">Connect Surface Hubs to OMS through Intune</span></span>
<span data-ttu-id="bf018-128">Vous devez disposer de l’ID et de la clé de l’espace de travail OMS devant gérer vos Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="bf018-128">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="bf018-129">Vous pouvez les obtenir à partir du portail OMS.</span><span class="sxs-lookup"><span data-stu-id="bf018-129">You can get those from the OMS portal.</span></span>

<span data-ttu-id="bf018-130">Intune est un produit Microsoft permettant de gérer de manière centralisée les paramètres de configuration OMS appliqués à un ou plusieurs de vos appareils.</span><span class="sxs-lookup"><span data-stu-id="bf018-130">Intune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span></span> <span data-ttu-id="bf018-131">Pour configurer vos appareils via Intune, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf018-131">Follow these steps to configure your devices through Intune:</span></span>

1. <span data-ttu-id="bf018-132">Connectez-vous à Intune.</span><span class="sxs-lookup"><span data-stu-id="bf018-132">Sign in to Intune.</span></span>
2. <span data-ttu-id="bf018-133">Accédez à **Paramètres** > **Sources connectées**.</span><span class="sxs-lookup"><span data-stu-id="bf018-133">Navigate to **Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="bf018-134">Créez ou modifiez une stratégie basée sur le modèle Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="bf018-134">Create or edit a policy based on the Surface Hub template.</span></span>
4. <span data-ttu-id="bf018-135">Accédez à la section OMS (Azure Operational Insights) de la stratégie, puis ajoutez l’*ID de l’espace de travail* et la *Clé de l’espace de travail* à la stratégie.</span><span class="sxs-lookup"><span data-stu-id="bf018-135">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span></span>
5. <span data-ttu-id="bf018-136">Enregistrez la stratégie.</span><span class="sxs-lookup"><span data-stu-id="bf018-136">Save the policy.</span></span>
6. <span data-ttu-id="bf018-137">Associez la stratégie au groupe approprié d’appareils.</span><span class="sxs-lookup"><span data-stu-id="bf018-137">Associate the policy with the appropriate group of devices.</span></span>

   ![Stratégie Intune](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="bf018-139">Intune synchronise ensuite les paramètres OMS avec les appareils du groupe cible en inscrivant ceux-ci dans votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="bf018-139">Intune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-to-oms-using-the-settings-app"></a><span data-ttu-id="bf018-140">Connecter des Surface Hubs à OMS en utilisant l’application Paramètres</span><span class="sxs-lookup"><span data-stu-id="bf018-140">Connect Surface Hubs to OMS using the Settings app</span></span>
<span data-ttu-id="bf018-141">Vous devez disposer de l’ID et de la clé de l’espace de travail OMS devant gérer vos Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="bf018-141">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="bf018-142">Vous pouvez les obtenir à partir du portail OMS.</span><span class="sxs-lookup"><span data-stu-id="bf018-142">You can get those from the OMS portal.</span></span>

<span data-ttu-id="bf018-143">Si vous n’utilisez pas Intune pour gérer votre environnement, vous pouvez inscrire des appareils manuellement via les **Paramètres** de chaque Surface Hub :</span><span class="sxs-lookup"><span data-stu-id="bf018-143">If you don't use Intune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="bf018-144">Sur votre Surface Hub, ouvrez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="bf018-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="bf018-145">Entrez les informations d’identification d’administrateur de l’appareil lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="bf018-145">Enter the device admin credentials when prompted.</span></span>
3. <span data-ttu-id="bf018-146">Cliquez sur **Cet appareil**, puis, sous **Analyse**, cliquez sur **Configurer les paramètres OMS**.</span><span class="sxs-lookup"><span data-stu-id="bf018-146">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="bf018-147">Sélectionnez **Activer l’analyse**.</span><span class="sxs-lookup"><span data-stu-id="bf018-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="bf018-148">Dans la boîte de dialogue Paramètres OMS, tapez l’**ID de l’espace de travail** et la **Clé de l’espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="bf018-148">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span></span>  
   <span data-ttu-id="bf018-149">![Paramètres](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="bf018-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="bf018-150">Cliquez sur **OK** pour achever la configuration.</span><span class="sxs-lookup"><span data-stu-id="bf018-150">Click **OK** to complete the configuration.</span></span>

<span data-ttu-id="bf018-151">Une confirmation s’affiche, vous indiquant si la configuration OMS a été correctement appliquée à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="bf018-151">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span></span> <span data-ttu-id="bf018-152">Si c’est le cas, un message s’affiche, indiquant que l’agent est bien connecté au service OMS.</span><span class="sxs-lookup"><span data-stu-id="bf018-152">If it was, a message appears stating that the agent successfully connected to the OMS service.</span></span> <span data-ttu-id="bf018-153">L’appareil commence alors à envoyer des données à OMS, où vous pouvez les consulter et les utiliser.</span><span class="sxs-lookup"><span data-stu-id="bf018-153">The device then starts sending data to OMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="bf018-154">Analyser les Surface Hubs</span><span class="sxs-lookup"><span data-stu-id="bf018-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="bf018-155">L’analyse de vos Surface Hubs à l’aide d’OMS est très similaire à l’analyse d’autres appareils inscrits.</span><span class="sxs-lookup"><span data-stu-id="bf018-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="bf018-156">Connectez-vous au portail OMS.</span><span class="sxs-lookup"><span data-stu-id="bf018-156">Sign in to the OMS portal.</span></span>
2. <span data-ttu-id="bf018-157">Accédez au tableau de bord du pack de solutions Surface.</span><span class="sxs-lookup"><span data-stu-id="bf018-157">Navigate to the Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="bf018-158">L’intégrité de votre appareil s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bf018-158">Your device's health is displayed.</span></span>

   ![Tableau de bord de Surface Hub](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="bf018-160">Vous pouvez créer des [alertes](log-analytics-alerts.md) basées sur des recherches de journal existantes ou personnalisées.</span><span class="sxs-lookup"><span data-stu-id="bf018-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="bf018-161">En utilisant les données qu’OMS collecte à partir de vos Surface Hubs, vous pouvez rechercher des problèmes et générer des alertes sur les conditions que vous définissez pour vos appareils.</span><span class="sxs-lookup"><span data-stu-id="bf018-161">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf018-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf018-162">Next steps</span></span>
* <span data-ttu-id="bf018-163">Utiliser des [recherches de journal dans Log Analytics](log-analytics-log-searches.md) pour afficher des données détaillées de Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="bf018-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span></span>
* <span data-ttu-id="bf018-164">Créer des [alertes](log-analytics-alerts.md) pour être averti en cas de problèmes avec vos Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="bf018-164">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span></span>
