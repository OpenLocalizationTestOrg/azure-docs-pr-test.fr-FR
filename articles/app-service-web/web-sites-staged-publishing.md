---
title: "Configurer des environnements intermédiaires pour les applications web dans Azure App Service | Microsoft Docs"
description: "Découvrez comment utiliser la publication intermédiaire pour les applications web dans Azure App Service."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: ca27c55eaaceb3109b1450c550330dfc416fdf55
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="c467d-103">Configurer des environnements intermédiaires dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c467d-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="c467d-104">Lorsque vous déployez votre application web, application web sur Linux, principale mobile ou API dans [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), vous pouvez cibler un autre emplacement de déploiement que l’emplacement de production par défaut en mode **Standard** ou **Premium**.</span><span class="sxs-lookup"><span data-stu-id="c467d-104">When you deploy your web app, web app on Linux, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="c467d-105">Les emplacements de déploiement sont en fait des applications dynamiques pourvues de leur propre nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="c467d-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="c467d-106">Les éléments de contenu et de configuration des applications peuvent être échangés entre deux emplacements de déploiement, y compris l’emplacement de production.</span><span class="sxs-lookup"><span data-stu-id="c467d-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="c467d-107">Le déploiement de votre application sur un emplacement de déploiement présente les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c467d-107">Deploying your application to a deployment slot has the following benefits:</span></span>

* <span data-ttu-id="c467d-108">Vous pouvez valider les modifications d’une application dans un emplacement de déploiement intermédiaire avant de l’échanger avec l’emplacement de production.</span><span class="sxs-lookup"><span data-stu-id="c467d-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span></span>
* <span data-ttu-id="c467d-109">Déployer d’abord une application vers un emplacement et la basculer ensuite en production garantit que toutes les instances de l’emplacement sont initialisées avant d’être basculées en production.</span><span class="sxs-lookup"><span data-stu-id="c467d-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="c467d-110">Cela permet d’éliminer les temps d’arrêt lors du déploiement de l’application.</span><span class="sxs-lookup"><span data-stu-id="c467d-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="c467d-111">La redirection du trafic est transparente et aucune demande n'est abandonnée durant les opérations de basculement.</span><span class="sxs-lookup"><span data-stu-id="c467d-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="c467d-112">Ce flux de travail peut être entièrement automatisé en configurant [Échange automatique](#Auto-Swap) lorsqu’aucune validation n’est requise avant l’échange.</span><span class="sxs-lookup"><span data-stu-id="c467d-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="c467d-113">Après basculement, la précédente application de production se retrouve dans l’emplacement de l’application précédemment intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="c467d-113">After a swap, the slot with previously staged app now has the previous production app.</span></span> <span data-ttu-id="c467d-114">Si les modifications basculées en production ne vous conviennent pas, vous pouvez effectuer le même basculement afin de récupérer immédiatement le contenu du précédent site qui vous plaisait.</span><span class="sxs-lookup"><span data-stu-id="c467d-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span></span>

<span data-ttu-id="c467d-115">Chaque mode de plan App Service prend en charge un nombre différent d’emplacements de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c467d-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="c467d-116">Pour connaître le nombre d’emplacements pris en charge par le mode de votre application, consultez la page [Tarification d’App Service](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="c467d-116">To find out the number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="c467d-117">Si votre application dispose de plusieurs emplacements, vous ne pouvez pas changer de mode.</span><span class="sxs-lookup"><span data-stu-id="c467d-117">When your app has multiple slots, you cannot change the mode.</span></span>
* <span data-ttu-id="c467d-118">La mise à l'échelle est uniquement disponible pour les emplacements de site de production.</span><span class="sxs-lookup"><span data-stu-id="c467d-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="c467d-119">La gestion des ressources liées est uniquement prise en charge pour les emplacements de site de production.</span><span class="sxs-lookup"><span data-stu-id="c467d-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="c467d-120">Dans le [portail Azure](http://go.microsoft.com/fwlink/?LinkId=529715) uniquement, vous pouvez éviter cet impact potentiel sur un emplacement de production en déplaçant temporairement l’emplacement autre que de production vers un autre mode de plan App Service.</span><span class="sxs-lookup"><span data-stu-id="c467d-120">In the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving the non-production slot to a different App Service plan mode.</span></span> <span data-ttu-id="c467d-121">Notez que l’emplacement autre que de production doit une fois encore partager le même mode que l’emplacement de production avant que vous ne puissiez échanger les deux emplacements.</span><span class="sxs-lookup"><span data-stu-id="c467d-121">Note that the non-production slot must once again share the same mode with the production slot before you can swap the two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="c467d-122">Ajouter un emplacement de déploiement</span><span class="sxs-lookup"><span data-stu-id="c467d-122">Add a deployment slot</span></span>
<span data-ttu-id="c467d-123">Pour que vous puissiez activer plusieurs emplacements de déploiement, l’application doit s’exécuter en mode **Standard** ou **Premium**.</span><span class="sxs-lookup"><span data-stu-id="c467d-123">The app must be running in the **Standard** or **Premium** mode in order for you to enable multiple deployment slots.</span></span>

1. <span data-ttu-id="c467d-124">Dans le [portail Azure](https://portal.azure.com/), ouvrez le [panneau de ressources](../azure-resource-manager/resource-group-portal.md#manage-resources) de votre application.</span><span class="sxs-lookup"><span data-stu-id="c467d-124">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="c467d-125">Choisissez l’option **Emplacements de déploiement**, puis cliquez sur **Ajouter un emplacement**.</span><span class="sxs-lookup"><span data-stu-id="c467d-125">Choose the **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Add a new deployment slot][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="c467d-127">Si l’application ne s’exécute pas en mode **Standard** ou **Premium**, vous recevez un message indiquant les modes pris en charge pour l’activation de la publication intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="c467d-127">If the app is not already in the **Standard** or **Premium** mode, you will receive a message indicating the supported modes for enabling staged publishing.</span></span> <span data-ttu-id="c467d-128">À ce stade, vous pouvez sélectionner **Mettre à niveau** et accéder à l’onglet **Mettre à l’échelle** de votre application avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="c467d-128">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="c467d-129">Dans le panneau **Ajouter un emplacement**, nommez l’emplacement, puis indiquez si vous souhaitez cloner la configuration de l’application à partir d’un autre emplacement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c467d-129">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="c467d-130">Cliquez sur la coche pour continuer.</span><span class="sxs-lookup"><span data-stu-id="c467d-130">Click the check mark to continue.</span></span>
   
    ![Source de configuration][ConfigurationSource1]
   
    <span data-ttu-id="c467d-132">La première fois que vous ajoutez un emplacement, vous avez uniquement deux choix : cloner la configuration à partir de l’emplacement par défaut en production ou ne rien cloner du tout.</span><span class="sxs-lookup"><span data-stu-id="c467d-132">The first time you add a slot, you will only have two choices: clone configuration from the default slot in production or not at all.</span></span>
    <span data-ttu-id="c467d-133">Après avoir créé plusieurs emplacements, vous pourrez cloner la configuration depuis un emplacement autre que l'emplacement de production :</span><span class="sxs-lookup"><span data-stu-id="c467d-133">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span></span>
   
    ![Sources de configuration][MultipleConfigurationSources]
4. <span data-ttu-id="c467d-135">Dans le panneau des ressources de votre application, cliquez sur **Emplacements de déploiement**, puis cliquez sur un emplacement de déploiement pour ouvrir le panneau des ressources correspondant. Comme pour toute autre application, celui-ci contient un ensemble de mesures et de paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="c467d-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="c467d-136">Le nom de l’emplacement est indiqué en haut du panneau pour vous rappeler que c’est l’emplacement de déploiement qui affiché.</span><span class="sxs-lookup"><span data-stu-id="c467d-136">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span></span>
   
    ![Titre de l'emplacement de déploiement][StagingTitle]
5. <span data-ttu-id="c467d-138">Cliquez sur l’URL de l’application dans le panneau de l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="c467d-138">Click the app URL in the slot's blade.</span></span> <span data-ttu-id="c467d-139">Notez que l’emplacement de déploiement possède son propre nom d’hôte et qu’il s’agit d’une application dynamique.</span><span class="sxs-lookup"><span data-stu-id="c467d-139">Notice the deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="c467d-140">Pour limiter l’accès public à l’emplacement de déploiement, consultez la page [Application web App Service : bloquer l’accès web aux emplacements de déploiement autres que de production](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="c467d-140">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="c467d-141">Il n’existe pas de contenu après la création de l’emplacement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c467d-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="c467d-142">Vous pouvez effectuer un déploiement sur l'emplacement d'une autre branche référentielle, ou d'un référentiel complètement différent.</span><span class="sxs-lookup"><span data-stu-id="c467d-142">You can deploy to the slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="c467d-143">Vous pouvez également modifier la configuration de l'emplacement.</span><span class="sxs-lookup"><span data-stu-id="c467d-143">You can also change the slot's configuration.</span></span> <span data-ttu-id="c467d-144">Utilisez le profil de publication ou les informations d'identification associées à l'emplacement de déploiement pour les mises à jour de contenu.</span><span class="sxs-lookup"><span data-stu-id="c467d-144">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span></span>  <span data-ttu-id="c467d-145">Par exemple, vous pouvez [publier sur cet emplacement avec Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c467d-145">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="c467d-146">Configuration d’emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="c467d-146">Configuration for deployment slots</span></span>
<span data-ttu-id="c467d-147">Lorsque vous clonez la configuration depuis un autre emplacement de déploiement, celle-ci est modifiable.</span><span class="sxs-lookup"><span data-stu-id="c467d-147">When you clone configuration from another deployment slot, the cloned configuration is editable.</span></span> <span data-ttu-id="c467d-148">Par ailleurs, après un échange, certains éléments de configuration suivent le contenu (éléments non propres à un emplacement) tandis que d’autres restent dans le même emplacement (éléments propres à un emplacement).</span><span class="sxs-lookup"><span data-stu-id="c467d-148">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span></span> <span data-ttu-id="c467d-149">Les listes suivantes présentent la configuration changée lorsque vous effectuez des basculements d'emplacements.</span><span class="sxs-lookup"><span data-stu-id="c467d-149">The following lists show the configuration that will change when you swap slots.</span></span>

<span data-ttu-id="c467d-150">**Paramètres échangés**:</span><span class="sxs-lookup"><span data-stu-id="c467d-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="c467d-151">Paramètres généraux, par exemple versions d’infrastructure, 32/64 bits, sockets web</span><span class="sxs-lookup"><span data-stu-id="c467d-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="c467d-152">Paramètres d’application (peuvent être configurés pour respecter un emplacement)</span><span class="sxs-lookup"><span data-stu-id="c467d-152">App settings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="c467d-153">Chaînes de connexion (peuvent être configurées pour respecter un emplacement)</span><span class="sxs-lookup"><span data-stu-id="c467d-153">Connection strings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="c467d-154">Mappages de gestionnaires</span><span class="sxs-lookup"><span data-stu-id="c467d-154">Handler mappings</span></span>
* <span data-ttu-id="c467d-155">Paramètres de surveillance et de diagnostics</span><span class="sxs-lookup"><span data-stu-id="c467d-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="c467d-156">Contenu WebJobs</span><span class="sxs-lookup"><span data-stu-id="c467d-156">WebJobs content</span></span>

<span data-ttu-id="c467d-157">**Paramètres non échangés**:</span><span class="sxs-lookup"><span data-stu-id="c467d-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="c467d-158">Points de terminaison de publication</span><span class="sxs-lookup"><span data-stu-id="c467d-158">Publishing endpoints</span></span>
* <span data-ttu-id="c467d-159">Noms de domaine personnalisés</span><span class="sxs-lookup"><span data-stu-id="c467d-159">Custom Domain Names</span></span>
* <span data-ttu-id="c467d-160">Certificats SSL et liaisons</span><span class="sxs-lookup"><span data-stu-id="c467d-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="c467d-161">Paramètres de mise à l'échelle</span><span class="sxs-lookup"><span data-stu-id="c467d-161">Scale settings</span></span>
* <span data-ttu-id="c467d-162">Planificateurs WebJobs</span><span class="sxs-lookup"><span data-stu-id="c467d-162">WebJobs schedulers</span></span>

<span data-ttu-id="c467d-163">Pour lier un paramètre d’application ou une chaîne de connexion à un emplacement (aucun échange), accédez au panneau **Paramètres de l’application** d’un emplacement, puis cochez la case **Paramètre d’emplacement** correspondant aux éléments de configuration à lier à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="c467d-163">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span></span> <span data-ttu-id="c467d-164">Notez que si vous marquez un élément de configuration comme propre à un emplacement, cet élément ne pourra pas être échangé entre tous les emplacements de déploiement associés à l’application.</span><span class="sxs-lookup"><span data-stu-id="c467d-164">Note that marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span></span>

![Paramètres d’emplacement][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="c467d-166">Échanger des emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="c467d-166">Swap deployment slots</span></span> 
<span data-ttu-id="c467d-167">Vous pouvez échanger des emplacements de déploiement dans la vue **Vue d’ensemble** ou **Emplacements de déploiement** du panneau de ressources de votre application.</span><span class="sxs-lookup"><span data-stu-id="c467d-167">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c467d-168">Avant de basculer une application à partir d’un emplacement de déploiement vers un emplacement de production, assurez-vous que tous les paramètres non propres à un emplacement sont configurés comme vous le souhaitez dans la cible de l’échange.</span><span class="sxs-lookup"><span data-stu-id="c467d-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span></span>
> 
> 

1. <span data-ttu-id="c467d-169">Pour échanger des emplacements de déploiement, cliquez sur le bouton **Échanger** dans la barre de commandes de l’application ou dans celle d’un emplacement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c467d-169">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span></span>
   
    ![Bouton Swap][SwapButtonBar]

2. <span data-ttu-id="c467d-171">Assurez-vous que la source et la cible de l’échange sont définies correctement.</span><span class="sxs-lookup"><span data-stu-id="c467d-171">Make sure that the swap source and swap target are set properly.</span></span> <span data-ttu-id="c467d-172">En règle générale, la cible de l’échange correspond à l’emplacement de production.</span><span class="sxs-lookup"><span data-stu-id="c467d-172">Usually, the swap target is the production slot.</span></span> <span data-ttu-id="c467d-173">Cliquez sur **OK** pour terminer l’opération.</span><span class="sxs-lookup"><span data-stu-id="c467d-173">Click **OK** to complete the operation.</span></span> <span data-ttu-id="c467d-174">À l’issue de l’opération, les emplacements de déploiement ont été échangés.</span><span class="sxs-lookup"><span data-stu-id="c467d-174">When the operation finishes, the deployment slots have been swapped.</span></span>

    ![Échange effectué](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="c467d-176">Pour le type d’échange **Échange avec aperçu**, consultez [Échange avec aperçu (échange multiphase)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="c467d-176">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="c467d-177">Échange avec aperçu (échange multiphase)</span><span class="sxs-lookup"><span data-stu-id="c467d-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="c467d-178">L’échange avec l’aperçu, ou échange multiphase, simplifie la validation des éléments de configuration spécifiques d’un emplacement, tels que les chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="c467d-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="c467d-179">Pour les charges de travail stratégiques, il est souhaitable de vérifier que l’application se comporte comme prévu lorsque la configuration de l’emplacement de production est appliquée, et cette vérification doit être effectuée *avant* le basculement de l’application en production.</span><span class="sxs-lookup"><span data-stu-id="c467d-179">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span></span> <span data-ttu-id="c467d-180">C’est précisément ce que l’échange avec aperçu permet de faire.</span><span class="sxs-lookup"><span data-stu-id="c467d-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="c467d-181">L’échange avec l’aperçu n’est pas pris en charge dans les applications web sous Linux.</span><span class="sxs-lookup"><span data-stu-id="c467d-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="c467d-182">Lorsque vous utilisez l’option **Échange avec aperçu** (voir [Échanger des emplacements de déploiement](#Swap)), App Service :</span><span class="sxs-lookup"><span data-stu-id="c467d-182">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span></span>

- <span data-ttu-id="c467d-183">Laisse l’emplacement de destination inchangé, de sorte que la charge de travail existante dans cet emplacement (de production, par exemple) n’est pas affectée.</span><span class="sxs-lookup"><span data-stu-id="c467d-183">Keeps the destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="c467d-184">Applique les éléments de configuration de l’emplacement de destination à l’emplacement source, y compris les chaînes de connexion spécifiques de l’emplacement et les paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="c467d-184">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="c467d-185">Redémarre les processus de travail dans l’emplacement source à l’aide des éléments de configuration mentionnés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="c467d-185">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="c467d-186">Lorsque vous effectuez l’échange : transfère l’emplacement source préinitialisé dans l’emplacement de destination.</span><span class="sxs-lookup"><span data-stu-id="c467d-186">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span></span> <span data-ttu-id="c467d-187">L’emplacement de destination est transféré dans l’emplacement source, comme dans le cadre d’un échange manuel.</span><span class="sxs-lookup"><span data-stu-id="c467d-187">The destination slot is moved into the source slot as in a manual swap.</span></span>
- <span data-ttu-id="c467d-188">Lorsque vous annulez l’échange : réapplique les éléments de configuration de l’emplacement source à l’emplacement source.</span><span class="sxs-lookup"><span data-stu-id="c467d-188">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span></span>

<span data-ttu-id="c467d-189">Vous pouvez prévisualiser le comportement précis de l’application avec la configuration de l’emplacement de destination.</span><span class="sxs-lookup"><span data-stu-id="c467d-189">You can preview exactly how the app will behave with the destination slot's configuration.</span></span> <span data-ttu-id="c467d-190">Une fois la validation terminée, vous effectuez l’échange dans le cadre d’une étape distincte.</span><span class="sxs-lookup"><span data-stu-id="c467d-190">Once you complete validation, you complete the swap in a separate step.</span></span> <span data-ttu-id="c467d-191">L’avantage de cette étape est que l’emplacement source est déjà initialisé avec la configuration souhaitée et que les clients ne seront pas confrontés à des temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="c467d-191">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="c467d-192">Des exemples pour les applets de commande Azure PowerShell disponibles pour l’échange multiphase figurent dans les applets de commande Azure PowerShell de la section des emplacements de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c467d-192">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="c467d-193">Configurer l’échange automatique</span><span class="sxs-lookup"><span data-stu-id="c467d-193">Configure Auto Swap</span></span>
<span data-ttu-id="c467d-194">L’échange automatique simplifie les scénarios d’opérations de développement impliquant un déploiement de l’application en continu sans démarrage à froid ni temps d’arrêt pour les clients finaux.</span><span class="sxs-lookup"><span data-stu-id="c467d-194">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span></span> <span data-ttu-id="c467d-195">Si un emplacement de déploiement est configuré pour l’échange automatique en production, chaque fois que vous envoyez une mise à jour de votre code par une transmission de type push vers cet emplacement, App Service échange automatiquement l’application en production après l’avoir initialisée dans l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="c467d-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c467d-196">Lorsque vous activez l’échange automatique pour un emplacement, vérifiez que la configuration de l’emplacement est exactement celle que vous souhaitez pour l’emplacement cible (en général, l’emplacement de production).</span><span class="sxs-lookup"><span data-stu-id="c467d-196">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="c467d-197">L’échange automatique n’est pas pris en charge dans les applications web sous Linux.</span><span class="sxs-lookup"><span data-stu-id="c467d-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="c467d-198">La configuration de l’échange automatique pour un emplacement est facile.</span><span class="sxs-lookup"><span data-stu-id="c467d-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="c467d-199">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c467d-199">Follow the steps below:</span></span>

1. <span data-ttu-id="c467d-200">Dans **Emplacements de déploiement**, sélectionnez un emplacement autre que de production et choisissez **Paramètres de l’application** dans le panneau de ressources de cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="c467d-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="c467d-201">Sélectionnez **Activé** dans **Échange automatique**, ainsi que l’emplacement cible souhaité dans **Emplacement d’échange automatique**, puis cliquez sur **Enregistrer** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="c467d-201">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span></span> <span data-ttu-id="c467d-202">Assurez-vous que la configuration de l’emplacement est celle que vous souhaitez pour l’emplacement cible.</span><span class="sxs-lookup"><span data-stu-id="c467d-202">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span></span>
   
    <span data-ttu-id="c467d-203">Dans l’onglet **Notifications**, la mention **RÉUSSITE** clignote en vert une fois l’opération terminée.</span><span class="sxs-lookup"><span data-stu-id="c467d-203">The **Notifications** tab will flash a green **SUCCESS** once the operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="c467d-204">Pour tester l’échange automatique avec votre application, commencez par sélectionner un emplacement cible autre que de production dans **Emplacement d’échange automatique** afin de vous familiariser avec la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c467d-204">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="c467d-205">Exécutez une transmission de code de type push vers cet emplacement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c467d-205">Execute a code push to that deployment slot.</span></span> <span data-ttu-id="c467d-206">L’échange automatique se produit peu après, et la mise à jour est appliquée dans l’URL de votre emplacement cible.</span><span class="sxs-lookup"><span data-stu-id="c467d-206">Auto Swap will happen after a short time and the update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="to-rollback-a-production-app-after-swap"></a><span data-ttu-id="c467d-207">Pour rétablir une application de production après un échange</span><span class="sxs-lookup"><span data-stu-id="c467d-207">To rollback a production app after swap</span></span>
<span data-ttu-id="c467d-208">Si vous identifiez des erreurs de production après un basculement d'emplacements, rétablissez ces deux emplacements comme ils étaient, en les intervertissant immédiatement.</span><span class="sxs-lookup"><span data-stu-id="c467d-208">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="c467d-209">Mise en route personnalisée avant la permutation</span><span class="sxs-lookup"><span data-stu-id="c467d-209">Custom warm-up before swap</span></span>
<span data-ttu-id="c467d-210">Certaines applications peuvent nécessiter des actions personnalisées de mise en route.</span><span class="sxs-lookup"><span data-stu-id="c467d-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="c467d-211">L’élément de configuration `applicationInitialization` du fichier web.config vous permet de spécifier les actions d’initialisation personnalisées à exécuter avant la réception d’une demande.</span><span class="sxs-lookup"><span data-stu-id="c467d-211">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span></span> <span data-ttu-id="c467d-212">L'opération de permutation attendra la fin de cette mise en route personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c467d-212">The swap operation will wait for this custom warm-up to complete.</span></span> <span data-ttu-id="c467d-213">Voici un exemple de fragment web.config.</span><span class="sxs-lookup"><span data-stu-id="c467d-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="to-delete-a-deployment-slot"></a><span data-ttu-id="c467d-214">Pour supprimer un emplacement de déploiement</span><span class="sxs-lookup"><span data-stu-id="c467d-214">To delete a deployment slot</span></span>
<span data-ttu-id="c467d-215">Ouvrez le panneau d’un emplacement de déploiement, cliquez sur **Vue d’ensemble** (page par défaut), puis cliquez sur **Supprimer** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="c467d-215">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span></span>  

![Supprimer un emplacement de déploiement][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="c467d-217">Cmdlets Azure PowerShell pour les emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="c467d-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="c467d-218">Azure PowerShell est un module qui fournit des applets de commande pour gérer Azure via Windows PowerShell, notamment la prise en charge de la gestion des emplacements de déploiement des applications dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c467d-218">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="c467d-219">Pour plus d’informations sur l’installation et la configuration d’Azure PowerShell et sur l’authentification d’Azure PowerShell avec votre abonnement Azure, consultez la page [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c467d-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="c467d-220">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="c467d-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="c467d-221">Créer un emplacement de déploiement</span><span class="sxs-lookup"><span data-stu-id="c467d-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a><span data-ttu-id="c467d-222">Initialiser un échange avec aperçu (échange multiphase) et appliquer la configuration de l’emplacement de destination à l’emplacement source</span><span class="sxs-lookup"><span data-stu-id="c467d-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration to source slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="c467d-223">Annuler un échange en attente (échange avec aperçu) et restaurer la configuration de l’emplacement source</span><span class="sxs-lookup"><span data-stu-id="c467d-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="c467d-224">Échanger des emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="c467d-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="c467d-225">Supprimer un emplacement de déploiement</span><span class="sxs-lookup"><span data-stu-id="c467d-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="c467d-226">Commandes de l’interface de ligne de commande Azure pour les emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="c467d-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="c467d-227">L’interface de ligne de commande (CLI) Azure fournit des commandes interplateformes fonctionnant avec Azure, notamment la prise en charge de la gestion des emplacements de déploiement d’App Service.</span><span class="sxs-lookup"><span data-stu-id="c467d-227">The Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="c467d-228">Pour obtenir des instructions sur l’installation et la configuration de l’interface de ligne de commande Azure, et notamment des informations sur la connexion de cette dernière à votre abonnement Azure, consultez la rubrique [Installation et configuration de l’interface de ligne de commande Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c467d-228">For instructions on installing and configuring the Azure CLI, including information on how to connect Azure CLI to your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="c467d-229">Pour répertorier les commandes disponibles pour Azure App Service dans l’interface de ligne de commande Azure, appelez `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="c467d-229">To list the commands available for Azure App Service in the Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="c467d-230">Pour connaître les commandes de l’interface [Azure CLI 2.0](https://github.com/Azure/azure-cli) pour les emplacements de déploiement, consultez l’article [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="c467d-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="c467d-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="c467d-231">azure site list</span></span>
<span data-ttu-id="c467d-232">Pour plus d’informations sur les applications de l’abonnement actuel, appelez **azure site list**, comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c467d-232">For information about the apps in the current subscription, call **azure site list**, as in the following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="c467d-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="c467d-233">azure site create</span></span>
<span data-ttu-id="c467d-234">Pour créer un emplacement de déploiement, appelez **azure site create** et spécifiez le nom d’une application et de l’emplacement à créer, comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c467d-234">To create a deployment slot, call **azure site create** and specify the name of an existing app and the name of the slot to create, as in the following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="c467d-235">Pour activer le contrôle de code source pour le nouvel emplacement, utilisez l'option **--git** , comme dans l'exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c467d-235">To enable source control for the new slot, use the **--git** option, as in the following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="c467d-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="c467d-236">azure site swap</span></span>
<span data-ttu-id="c467d-237">Pour appliquer l’emplacement de déploiement mis à jour à l’application de production, utilisez la commande **azure site swap** pour effectuer un échange, comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c467d-237">To make the updated deployment slot the production app, use the **azure site swap** command to perform a swap operation, as in the following example.</span></span> <span data-ttu-id="c467d-238">L’application de production ne subira ni temps d’arrêt, ni démarrage à froid.</span><span class="sxs-lookup"><span data-stu-id="c467d-238">The production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="c467d-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="c467d-239">azure site delete</span></span>
<span data-ttu-id="c467d-240">Pour supprimer un emplacement de déploiement dont vous n'avez plus besoin, utilisez la commande **azure site delete** , comme dans l'exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c467d-240">To delete a deployment slot that is no longer needed, use the **azure site delete** command, as in the following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="c467d-241">Visualisez une application web en action.</span><span class="sxs-lookup"><span data-stu-id="c467d-241">See a web app in action.</span></span> <span data-ttu-id="c467d-242">[Essayez App Service](https://azure.microsoft.com/try/app-service/) dès maintenant et créez une première application temporaire. Aucune carte de crédit ni aucun engagement ne sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="c467d-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c467d-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c467d-243">Next Steps</span></span>
<span data-ttu-id="c467d-244">[Application web Azure App Service : bloquer l’accès web aux emplacements de déploiement hors production](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction à App Service sur Linux](./app-service-linux-intro.md)
[Essai gratuit de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="c467d-244">[Azure App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction to App Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

