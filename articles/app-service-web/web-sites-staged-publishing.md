---
title: "aaaSet des environnements intermédiaires pour applications web dans Azure App Service | Documents Microsoft"
description: "Découvrez comment toouse intermédiaire à la publication d’applications web dans Azure App Service."
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
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="ca4ba-103">Configurer des environnements intermédiaires dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ca4ba-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="ca4ba-104">Lorsque vous déployez votre application web, une application web sur Linux, mobile back-end et application API trop[du Service d’applications](http://go.microsoft.com/fwlink/?LinkId=529714), vous pouvez déployer tooa emplacement de déploiement distinct au lieu de l’emplacement de production par défaut hello lors de l’exécution dans hello **Standard**ou **Premium** en mode plan de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-104">When you deploy your web app, web app on Linux, mobile back end, and API app too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy tooa separate deployment slot instead of hello default production slot when running in hello **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="ca4ba-105">Les emplacements de déploiement sont en fait des applications dynamiques pourvues de leur propre nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="ca4ba-106">Éléments de contenu et les configurations application peuvent être échangés entre deux emplacements de déploiement, y compris l’emplacement de production hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-106">App content and configurations elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="ca4ba-107">Déploiement de votre emplacement de déploiement d’application tooa a hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ca4ba-107">Deploying your application tooa deployment slot has hello following benefits:</span></span>

* <span data-ttu-id="ca4ba-108">Vous pouvez valider la modification de l’application dans un emplacement de déploiement intermédiaire avant d’échanger celui-ci avec l’emplacement de production hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-108">You can validate app changes in a staging deployment slot before swapping it with hello production slot.</span></span>
* <span data-ttu-id="ca4ba-109">Déploiement d’un emplacement de l’application tooa tout d’abord et permuter vers la production garantissent que toutes les instances de l’emplacement de hello sont préparées avant d’être permutés en production.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-109">Deploying an app tooa slot first and swapping it into production ensures that all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="ca4ba-110">Cela permet d’éliminer les temps d’arrêt lors du déploiement de l’application.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="ca4ba-111">redirection du trafic Hello est transparente, et aucune demande n’est supprimés à la suite d’opérations de permutation.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-111">hello traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="ca4ba-112">Ce flux de travail peut être entièrement automatisé en configurant [Échange automatique](#Auto-Swap) lorsqu’aucune validation n’est requise avant l’échange.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="ca4ba-113">Une fois un échange, emplacement hello avec application précédemment intermédiaire a hello précédente application de production.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-113">After a swap, hello slot with previously staged app now has hello previous production app.</span></span> <span data-ttu-id="ca4ba-114">Si les modifications de hello permutées dans l’emplacement de production hello sont pas comme prévu, vous pouvez effectuer hello que même échange immédiatement tooget votre « dernier site connu » sauvegarder.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-114">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good site" back.</span></span>

<span data-ttu-id="ca4ba-115">Chaque mode de plan App Service prend en charge un nombre différent d’emplacements de déploiement.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="ca4ba-116">toofind nombre hello d’emplacements prend en charge par le mode de votre application, consultez [tarification de Service application](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="ca4ba-116">toofind out hello number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="ca4ba-117">Lorsque votre application a plusieurs emplacements, vous ne pouvez pas modifier le mode hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-117">When your app has multiple slots, you cannot change hello mode.</span></span>
* <span data-ttu-id="ca4ba-118">La mise à l'échelle est uniquement disponible pour les emplacements de site de production.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="ca4ba-119">La gestion des ressources liées est uniquement prise en charge pour les emplacements de site de production.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="ca4ba-120">Bonjour [portail Azure](http://go.microsoft.com/fwlink/?LinkId=529715) uniquement, vous pouvez éviter cet impact potentiel sur un emplacement de production en déplaçant temporairement le mode de plan App Service différents hello emplacement de production non tooa.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-120">In hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving hello non-production slot tooa different App Service plan mode.</span></span> <span data-ttu-id="ca4ba-121">Notez que cet emplacement de production non hello doit partager à nouveau hello même mode avec l’emplacement de production hello avant que vous pouvez échanger des emplacements de hello deux.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-121">Note that hello non-production slot must once again share hello same mode with hello production slot before you can swap hello two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="ca4ba-122">Ajouter un emplacement de déploiement</span><span class="sxs-lookup"><span data-stu-id="ca4ba-122">Add a deployment slot</span></span>
<span data-ttu-id="ca4ba-123">application Hello doit s’exécuter dans hello **Standard** ou **Premium** dans le mode de commande pour vous tooenable plusieurs emplacements de déploiement.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-123">hello app must be running in hello **Standard** or **Premium** mode in order for you tooenable multiple deployment slots.</span></span>

1. <span data-ttu-id="ca4ba-124">Bonjour [Azure Portal](https://portal.azure.com/), ouvrez votre application [panneau des ressources](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="ca4ba-124">In hello [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="ca4ba-125">Choisissez hello **les emplacements de déploiement** option, puis cliquez sur **ajouter un emplacement**.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-125">Choose hello **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Add a new deployment slot][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="ca4ba-127">Si l’application hello n’est pas déjà hello **Standard** ou **Premium** mode, vous recevrez un message indiquant que les modes de hello pris en charge pour l’activation de publication intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-127">If hello app is not already in hello **Standard** or **Premium** mode, you will receive a message indicating hello supported modes for enabling staged publishing.</span></span> <span data-ttu-id="ca4ba-128">À ce stade, vous avez hello option tooselect **mise à niveau** et accédez toohello **échelle** onglet de votre application avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-128">At this point, you have hello option tooselect **Upgrade** and navigate toohello **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="ca4ba-129">Bonjour **ajouter un emplacement** panneau, donnez un nom à emplacement de hello, puis sélectionnez si tooclone configuration de l’application à partir d’un autre emplacement de déploiement existant.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-129">In hello **Add a slot** blade, give hello slot a name, and select whether tooclone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="ca4ba-130">Cliquez sur toocontinue de case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-130">Click hello check mark toocontinue.</span></span>
   
    ![Source de configuration][ConfigurationSource1]
   
    <span data-ttu-id="ca4ba-132">Hello première fois que vous ajoutez un emplacement, vous aurez seulement deux choix : configuration de clonage depuis l’emplacement par défaut de hello en production ou pas du tout.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-132">hello first time you add a slot, you will only have two choices: clone configuration from hello default slot in production or not at all.</span></span>
    <span data-ttu-id="ca4ba-133">Une fois que vous avez créé plusieurs connecteurs, vous sera en mesure de tooclone à partir d’un emplacement autre que hello une en production :</span><span class="sxs-lookup"><span data-stu-id="ca4ba-133">After you have created several slots, you will be able tooclone configuration from a slot other than hello one in production:</span></span>
   
    ![Sources de configuration][MultipleConfigurationSources]
4. <span data-ttu-id="ca4ba-135">Dans le panneau des ressources de votre application, cliquez sur **les emplacements de déploiement**, puis cliquez sur un tooopen d’emplacement de déploiement panneau des ressources de cet emplacement, avec un ensemble de mesures et la configuration comme toute autre application.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot tooopen that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="ca4ba-136">Hello nom du connecteur de hello est affiché en haut de hello de hello panneau tooremind que vous visualisez hello emplacement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-136">hello name of hello slot is shown at hello top of hello blade tooremind you that you are viewing hello deployment slot.</span></span>
   
    ![Titre de l'emplacement de déploiement][StagingTitle]
5. <span data-ttu-id="ca4ba-138">Cliquez sur URL de l’application hello dans le panneau de l’emplacement hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-138">Click hello app URL in hello slot's blade.</span></span> <span data-ttu-id="ca4ba-139">Notez l’emplacement de déploiement hello a son propre nom d’hôte et est également une application en temps réel.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-139">Notice hello deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="ca4ba-140">emplacement de déploiement toohello toolimit accès public, consultez [application de Service d’applications Web – bloquer les emplacements de déploiement web accès toonon-production](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="ca4ba-140">toolimit public access toohello deployment slot, see [App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="ca4ba-141">Il n’existe pas de contenu après la création de l’emplacement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="ca4ba-142">Vous pouvez déployer le connecteur toohello à partir d’une branche de référentiel différent ou un référentiel complètement différent.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-142">You can deploy toohello slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="ca4ba-143">Vous pouvez également modifier la configuration de l’emplacement hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-143">You can also change hello slot's configuration.</span></span> <span data-ttu-id="ca4ba-144">Hello d’utiliser les informations d’identification profil ou au déploiement associées avec l’emplacement de déploiement hello pour les mises à jour de publication.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-144">Use hello publish profile or deployment credentials associated with hello deployment slot for content updates.</span></span>  <span data-ttu-id="ca4ba-145">Par exemple, vous pouvez [publier emplacement toothis avec git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="ca4ba-145">For example, you can [publish toothis slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="ca4ba-146">Configuration d’emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="ca4ba-146">Configuration for deployment slots</span></span>
<span data-ttu-id="ca4ba-147">Lorsque vous clonez configuration à partir d’un autre emplacement de déploiement, configuration clonée de hello est modifiable.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-147">When you clone configuration from another deployment slot, hello cloned configuration is editable.</span></span> <span data-ttu-id="ca4ba-148">En outre, certains éléments de configuration suit le contenu hello sur un échange (non spécifique à l’emplacement) alors que les autres éléments de configuration seront conservée dans le même emplacement après un échange (spécifique à l’emplacement) de hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-148">Furthermore, some configuration elements will follow hello content across a swap (not slot specific) while other configuration elements will stay in hello same slot after a swap (slot specific).</span></span> <span data-ttu-id="ca4ba-149">Hello listes suivantes présentent configuration hello qui change lorsque vous échangez des emplacements.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-149">hello following lists show hello configuration that will change when you swap slots.</span></span>

<span data-ttu-id="ca4ba-150">**Paramètres échangés**:</span><span class="sxs-lookup"><span data-stu-id="ca4ba-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="ca4ba-151">Paramètres généraux, par exemple versions d’infrastructure, 32/64 bits, sockets web</span><span class="sxs-lookup"><span data-stu-id="ca4ba-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="ca4ba-152">Paramètres de l’application (peut être pas configuré toostick tooa emplacement)</span><span class="sxs-lookup"><span data-stu-id="ca4ba-152">App settings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="ca4ba-153">Chaînes de connexion (peut être pas configuré toostick tooa emplacement)</span><span class="sxs-lookup"><span data-stu-id="ca4ba-153">Connection strings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="ca4ba-154">Mappages de gestionnaires</span><span class="sxs-lookup"><span data-stu-id="ca4ba-154">Handler mappings</span></span>
* <span data-ttu-id="ca4ba-155">Paramètres de surveillance et de diagnostics</span><span class="sxs-lookup"><span data-stu-id="ca4ba-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="ca4ba-156">Contenu WebJobs</span><span class="sxs-lookup"><span data-stu-id="ca4ba-156">WebJobs content</span></span>

<span data-ttu-id="ca4ba-157">**Paramètres non échangés**:</span><span class="sxs-lookup"><span data-stu-id="ca4ba-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="ca4ba-158">Points de terminaison de publication</span><span class="sxs-lookup"><span data-stu-id="ca4ba-158">Publishing endpoints</span></span>
* <span data-ttu-id="ca4ba-159">Noms de domaine personnalisés</span><span class="sxs-lookup"><span data-stu-id="ca4ba-159">Custom Domain Names</span></span>
* <span data-ttu-id="ca4ba-160">Certificats SSL et liaisons</span><span class="sxs-lookup"><span data-stu-id="ca4ba-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="ca4ba-161">Paramètres de mise à l'échelle</span><span class="sxs-lookup"><span data-stu-id="ca4ba-161">Scale settings</span></span>
* <span data-ttu-id="ca4ba-162">Planificateurs WebJobs</span><span class="sxs-lookup"><span data-stu-id="ca4ba-162">WebJobs schedulers</span></span>

<span data-ttu-id="ca4ba-163">tooconfigure une connexion ou le paramètre de chaîne toostick tooa l’emplacement d’application (ne pas permuté), hello d’accès **paramètres de l’Application** panneau pour un emplacement spécifique, puis sélectionnez hello **paramètre d’emplacement** boîte pour hello éléments de configuration qui est préférable de conserver les emplacement hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-163">tooconfigure an app setting or connection string toostick tooa slot (not swapped), access hello **Application Settings** blade for a specific slot, then select hello **Slot Setting** box for hello configuration elements that should stick hello slot.</span></span> <span data-ttu-id="ca4ba-164">Notez que le marquage un élément de configuration spécifique à l’emplacement a effet hello d’établissement de cet élément comme échangeables pas sur tous les emplacements de déploiement hello associés application hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-164">Note that marking a configuration element as slot specific has hello effect of establishing that element as not swappable across all hello deployment slots associated with hello app.</span></span>

![Paramètres d’emplacement][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="ca4ba-166">Échanger des emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="ca4ba-166">Swap deployment slots</span></span> 
<span data-ttu-id="ca4ba-167">Vous pouvez permuter les emplacements de déploiement Bonjour **vue d’ensemble** ou **les emplacements de déploiement** vue du panneau des ressources de votre application.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-167">You can swap deployment slots in hello **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca4ba-168">Avant que vous remplacez une application à partir d’un emplacement de déploiement en production, assurez-vous que tous les connecteurs non spécifique est configuré exactement comme vous le souhaitez toohave dans la cible de l’échange hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want toohave it in hello swap target.</span></span>
> 
> 

1. <span data-ttu-id="ca4ba-169">tooswap les emplacements de déploiement, cliquez sur hello **échanger** bouton dans la barre de commandes hello de l’application hello ou dans la barre de commandes hello d’un emplacement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-169">tooswap deployment slots, click hello **Swap** button in hello command bar of hello app or in hello command bar of a deployment slot.</span></span>
   
    ![Bouton Swap][SwapButtonBar]

2. <span data-ttu-id="ca4ba-171">Assurez-vous que cette cible de source et de changer l’échange hello sont correctement définis.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-171">Make sure that hello swap source and swap target are set properly.</span></span> <span data-ttu-id="ca4ba-172">Généralement, la cible de l’échange hello est l’emplacement de production hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-172">Usually, hello swap target is hello production slot.</span></span> <span data-ttu-id="ca4ba-173">Cliquez sur **OK** opération hello de toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-173">Click **OK** toocomplete hello operation.</span></span> <span data-ttu-id="ca4ba-174">Fin de l’opération de hello, emplacements de déploiement hello ont été permutées.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-174">When hello operation finishes, hello deployment slots have been swapped.</span></span>

    ![Échange effectué](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="ca4ba-176">Pourquoi **échange avec aperçu** permuter le type, consultez [échange avec aperçu (MULTIPHASE swap)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="ca4ba-176">For hello **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="ca4ba-177">Échange avec aperçu (échange multiphase)</span><span class="sxs-lookup"><span data-stu-id="ca4ba-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="ca4ba-178">L’échange avec l’aperçu, ou échange multiphase, simplifie la validation des éléments de configuration spécifiques d’un emplacement, tels que les chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="ca4ba-179">Pour les charges de travail critiques, vous souhaitez toovalidate qui hello application se comporte comme prévu lors de la configuration de l’emplacement de production hello est appliquée, et vous devez effectuer cette validation *avant* application hello est échangée en production.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-179">For mission-critical workloads, you want toovalidate that hello app behaves as expected when hello production slot's configuration is applied, and you must perform such validation *before* hello app is swapped into production.</span></span> <span data-ttu-id="ca4ba-180">C’est précisément ce que l’échange avec aperçu permet de faire.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="ca4ba-181">L’échange avec l’aperçu n’est pas pris en charge dans les applications web sous Linux.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="ca4ba-182">Lorsque vous utilisez hello **l’échange avec aperçu** option (consultez [d’échanger les emplacements de déploiement](#Swap)), du Service d’applications hello suivant :</span><span class="sxs-lookup"><span data-stu-id="ca4ba-182">When you use hello **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does hello following:</span></span>

- <span data-ttu-id="ca4ba-183">Conserve hello destination emplacement inchangée, charge de travail existante sur cet emplacement (par exemple, production) n’est pas affectée.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-183">Keeps hello destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="ca4ba-184">Applique des éléments de configuration hello de hello emplacement toohello source l’emplacement de destination, notamment les chaînes de connexion spécifiques à l’emplacement de hello et les paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-184">Applies hello configuration elements of hello destination slot toohello source slot, including hello slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="ca4ba-185">Redémarre le processus de travail hello sur l’emplacement de source de hello à l’aide de ces éléments de configuration susmentionnés.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-185">Restarts hello worker processes on hello source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="ca4ba-186">Quand vous terminez d’échange hello : emplacement de pré-warmed-up source hello se déplace dans l’emplacement de destination hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-186">When you complete hello swap: Moves hello pre-warmed-up source slot into hello destination slot.</span></span> <span data-ttu-id="ca4ba-187">l’emplacement de destination Hello est déplacé dans l’emplacement de source de hello comme dans un échange manuel.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-187">hello destination slot is moved into hello source slot as in a manual swap.</span></span>
- <span data-ttu-id="ca4ba-188">Lorsque vous annulez l’échange de hello : réapplique les éléments de configuration hello de hello source emplacement toohello source emplacement.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-188">When you cancel hello swap: Reapplies hello configuration elements of hello source slot toohello source slot.</span></span>

<span data-ttu-id="ca4ba-189">Vous pouvez afficher un aperçu exactement comment l’application hello se comporte avec la configuration de l’emplacement de destination hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-189">You can preview exactly how hello app will behave with hello destination slot's configuration.</span></span> <span data-ttu-id="ca4ba-190">Après avoir terminé la validation, vous terminez swap hello dans une étape distincte.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-190">Once you complete validation, you complete hello swap in a separate step.</span></span> <span data-ttu-id="ca4ba-191">Cette étape a hello avantage que hello source est déjà préparée avec la configuration souhaitée de hello, et les clients ne rencontrerez aucun temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-191">This step has hello added advantage that hello source slot is already warmed up with hello desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="ca4ba-192">Exemples pour hello applets de commande Azure PowerShell disponibles pour l’échange de plusieurs phase sont incluses dans hello applets de commande Azure PowerShell pour la section des emplacements de déploiement.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-192">Samples for hello Azure PowerShell cmdlets available for multi-phase swap are included in hello Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="ca4ba-193">Configurer l’échange automatique</span><span class="sxs-lookup"><span data-stu-id="ca4ba-193">Configure Auto Swap</span></span>
<span data-ttu-id="ca4ba-194">Auto Swap rationalisation DevOps scénarios où vous toocontinuously déployer votre application avec zéro démarrage à froid et sans interruption pour les clients de fin de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-194">Auto Swap streamlines DevOps scenarios where you want toocontinuously deploy your app with zero cold start and zero downtime for end customers of hello app.</span></span> <span data-ttu-id="ca4ba-195">Lorsqu’un emplacement de déploiement est configuré pour l’échange automatique en production, chaque fois que vous effectuez un push votre emplacement de toothat de mise à jour de code, du Service d’applications échangera automatiquement application hello en production une fois qu’il a déjà préparée dans l’emplacement de hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update toothat slot, App Service will automatically swap hello app into production after it has already warmed up in hello slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca4ba-196">Lorsque vous activez l’échange automatique pour un emplacement, vérifiez que hello emplacement configuration est exactement hello prévu pour l’emplacement cible de hello (généralement un emplacement de production hello).</span><span class="sxs-lookup"><span data-stu-id="ca4ba-196">When you enable Auto Swap for a slot, make sure hello slot configuration is exactly hello configuration intended for hello target slot (usually hello production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="ca4ba-197">L’échange automatique n’est pas pris en charge dans les applications web sous Linux.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="ca4ba-198">La configuration de l’échange automatique pour un emplacement est facile.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="ca4ba-199">Suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ca4ba-199">Follow hello steps below:</span></span>

1. <span data-ttu-id="ca4ba-200">Dans **Emplacements de déploiement**, sélectionnez un emplacement autre que de production et choisissez **Paramètres de l’application** dans le panneau de ressources de cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="ca4ba-201">Sélectionnez **sur** pour **échange automatique**, sélectionnez emplacement cible souhaitée hello **emplacement d’échange automatique**, puis cliquez sur **enregistrer** dans la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-201">Select **On** for **Auto Swap**, select hello desired target slot in **Auto Swap Slot**, and click **Save** in hello command bar.</span></span> <span data-ttu-id="ca4ba-202">Assurez-vous que la configuration de l’emplacement de hello est exactement hello prévu pour l’emplacement cible de hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-202">Make sure configuration for hello slot is exactly hello configuration intended for hello target slot.</span></span>
   
    <span data-ttu-id="ca4ba-203">Hello **Notifications** un vert clignote en onglet **réussite** une fois l’opération hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-203">hello **Notifications** tab will flash a green **SUCCESS** once hello operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="ca4ba-204">tootest échange automatique pour votre application, vous pouvez d’abord sélectionner un emplacement hors production cible dans **emplacement d’échange automatique** toobecome familiarisé avec la fonctionnalité de hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-204">tootest Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** toobecome familiar with hello feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="ca4ba-205">Exécuter un emplacement de déploiement de code push toothat.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-205">Execute a code push toothat deployment slot.</span></span> <span data-ttu-id="ca4ba-206">Échange automatique se produit après une courte période et mise à jour hello est répercutée à l’URL de l’emplacement de votre cible.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-206">Auto Swap will happen after a short time and hello update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a><span data-ttu-id="ca4ba-207">toorollback une application de production après l’échange</span><span class="sxs-lookup"><span data-stu-id="ca4ba-207">toorollback a production app after swap</span></span>
<span data-ttu-id="ca4ba-208">Si des erreurs sont identifiées dans la production après un échange d’emplacement, restaurer les emplacements hello tootheir arrière swap préliminaire États en échangeant les emplacements de hello deux mêmes immédiatement.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-208">If any errors are identified in production after a slot swap, roll hello slots back tootheir pre-swap states by swapping hello same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="ca4ba-209">Mise en route personnalisée avant la permutation</span><span class="sxs-lookup"><span data-stu-id="ca4ba-209">Custom warm-up before swap</span></span>
<span data-ttu-id="ca4ba-210">Certaines applications peuvent nécessiter des actions personnalisées de mise en route.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="ca4ba-211">Hello `applicationInitialization` permet d’élément de configuration dans le fichier web.config vous toospecify d’initialisation personnalisées actions toobe effectuée avant une demande est reçue.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-211">hello `applicationInitialization` configuration element in web.config allows you toospecify custom initialization actions toobe performed before a request is received.</span></span> <span data-ttu-id="ca4ba-212">opération d’échange Hello attendra ce toocomplete préchauffage personnalisé.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-212">hello swap operation will wait for this custom warm-up toocomplete.</span></span> <span data-ttu-id="ca4ba-213">Voici un exemple de fragment web.config.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a><span data-ttu-id="ca4ba-214">toodelete un emplacement de déploiement</span><span class="sxs-lookup"><span data-stu-id="ca4ba-214">toodelete a deployment slot</span></span>
<span data-ttu-id="ca4ba-215">Dans le panneau hello pour un emplacement de déploiement, le panneau de l’emplacement de déploiement hello ouvert, cliquez sur **vue d’ensemble** (page par défaut de hello), puis cliquez sur **supprimer** dans la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-215">In hello blade for a deployment slot, open hello deployment slot's blade, click **Overview** (hello default page), and click **Delete** in hello command bar.</span></span>  

![Supprimer un emplacement de déploiement][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="ca4ba-217">Cmdlets Azure PowerShell pour les emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="ca4ba-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="ca4ba-218">Azure PowerShell est un module qui fournit des applets de commande toomanage Azure via Windows PowerShell, y compris la prise en charge pour la gestion des emplacements de déploiement dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-218">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="ca4ba-219">Pour plus d’informations sur l’installation et configuration d’Azure PowerShell et sur l’authentification d’Azure PowerShell avec votre abonnement Azure, consultez [comment tooinstall et configurer Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ca4ba-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How tooinstall and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="ca4ba-220">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="ca4ba-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="ca4ba-221">Créer un emplacement de déploiement</span><span class="sxs-lookup"><span data-stu-id="ca4ba-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a><span data-ttu-id="ca4ba-222">Lancer un échange avec révision (MULTIPHASE swap) et s’appliquent à l’emplacement de destination emplacement configuration toosource</span><span class="sxs-lookup"><span data-stu-id="ca4ba-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration toosource slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="ca4ba-223">Annuler un échange en attente (échange avec aperçu) et restaurer la configuration de l’emplacement source</span><span class="sxs-lookup"><span data-stu-id="ca4ba-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="ca4ba-224">Échanger des emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="ca4ba-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="ca4ba-225">Supprimer un emplacement de déploiement</span><span class="sxs-lookup"><span data-stu-id="ca4ba-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="ca4ba-226">Commandes de l’interface de ligne de commande Azure pour les emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="ca4ba-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="ca4ba-227">Hello CLI d’Azure fournit les commandes inter-plateformes pour travailler avec Azure, y compris la prise en charge pour la gestion des emplacements de déploiement du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-227">hello Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="ca4ba-228">Pour obtenir des instructions sur l’installation et la configuration hello CLI d’Azure, y compris des informations sur la façon de tooconnect CLI d’Azure tooyour abonnement Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ca4ba-228">For instructions on installing and configuring hello Azure CLI, including information on how tooconnect Azure CLI tooyour Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="ca4ba-229">commandes de hello toolist disponibles pour le Service d’applications Azure dans hello CLI d’Azure, appelez `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-229">toolist hello commands available for Azure App Service in hello Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="ca4ba-230">Pour connaître les commandes de l’interface [Azure CLI 2.0](https://github.com/Azure/azure-cli) pour les emplacements de déploiement, consultez l’article [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="ca4ba-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="ca4ba-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="ca4ba-231">azure site list</span></span>
<span data-ttu-id="ca4ba-232">Pour plus d’informations sur les applications hello dans l’abonnement actif de hello, appelez **liste des sites azure**, comme dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-232">For information about hello apps in hello current subscription, call **azure site list**, as in hello following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="ca4ba-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="ca4ba-233">azure site create</span></span>
<span data-ttu-id="ca4ba-234">toocreate un emplacement de déploiement, appelez **créer de site azure** et spécifiez le nom hello d’une application existante et nom hello de hello emplacement toocreate, comme dans l’exemple suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-234">toocreate a deployment slot, call **azure site create** and specify hello name of an existing app and hello name of hello slot toocreate, as in hello following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="ca4ba-235">contrôle de code source tooenable pour le nouvel emplacement hello, utilisez hello **--git** option, comme hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-235">tooenable source control for hello new slot, use hello **--git** option, as in hello following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="ca4ba-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="ca4ba-236">azure site swap</span></span>
<span data-ttu-id="ca4ba-237">toomake hello application de production de déploiement mis à jour emplacement hello, utilisez hello **échange de site azure** commande tooperform une opération d’échange, comme dans l’exemple suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-237">toomake hello updated deployment slot hello production app, use hello **azure site swap** command tooperform a swap operation, as in hello following example.</span></span> <span data-ttu-id="ca4ba-238">application de production Hello ne feront pas tout temps mort, ni subiront un démarrage à froid.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-238">hello production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="ca4ba-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="ca4ba-239">azure site delete</span></span>
<span data-ttu-id="ca4ba-240">toodelete un emplacement de déploiement qui n’est plus nécessaire, utilisez hello **supprimer le site azure** commande, comme dans l’exemple suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-240">toodelete a deployment slot that is no longer needed, use hello **azure site delete** command, as in hello following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="ca4ba-241">Visualisez une application web en action.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-241">See a web app in action.</span></span> <span data-ttu-id="ca4ba-242">[Essayez App Service](https://azure.microsoft.com/try/app-service/) dès maintenant et créez une première application temporaire. Aucune carte de crédit ni aucun engagement ne sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="ca4ba-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ca4ba-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ca4ba-243">Next Steps</span></span>
<span data-ttu-id="ca4ba-244">[Azure App Service Web application – bloquer les emplacements de déploiement de production de toonon accès web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service sur Linux](./app-service-linux-intro.md)
[version d’évaluation gratuite de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="ca4ba-244">[Azure App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service on Linux](./app-service-linux-intro.md)
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

