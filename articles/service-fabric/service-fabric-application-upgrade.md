---
title: "mise à niveau des applications de l’ensemble fibre optique aaaService | Documents Microsoft"
description: "Cet article fournit une présentation tooupgrading une application de Service Fabric, notamment les modes de mise à niveau en choisissant l’option et effectuer des vérifications d’intégrité."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 803c9c63-373a-4d6a-8ef2-ea97e16e88dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 6f649ef4a5c0afab682522bcba7d2d66a4268ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade"></a><span data-ttu-id="ad021-103">Mise à niveau des applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ad021-103">Service Fabric application upgrade</span></span>
<span data-ttu-id="ad021-104">Une application Azure Service Fabric est une collection de services.</span><span class="sxs-lookup"><span data-stu-id="ad021-104">An Azure Service Fabric application is a collection of services.</span></span> <span data-ttu-id="ad021-105">Pendant une mise à niveau, Service Fabric compare hello nouvelle [manifeste d’application](service-fabric-application-model.md#describe-an-application) avec la version précédente de hello et détermine les services dans une application hello nécessitent des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="ad021-105">During an upgrade, Service Fabric compares hello new [application manifest](service-fabric-application-model.md#describe-an-application) with hello previous version and determines which services in hello application require updates.</span></span> <span data-ttu-id="ad021-106">Service Fabric compare version hello chiffres dans le service hello manifestes avec les numéros de version hello dans la version précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-106">Service Fabric compares hello version numbers in hello service manifests with hello version numbers in hello previous version.</span></span> <span data-ttu-id="ad021-107">Si un service n'a pas changé, ce service n'est pas mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="ad021-107">If a service has not changed, that service is not upgraded.</span></span>

## <a name="rolling-upgrades-overview"></a><span data-ttu-id="ad021-108">Vue d'ensemble des mises à niveau propagées</span><span class="sxs-lookup"><span data-stu-id="ad021-108">Rolling upgrades overview</span></span>
<span data-ttu-id="ad021-109">Dans une mise à niveau propagée d’application, la mise à niveau hello est effectuée en étapes.</span><span class="sxs-lookup"><span data-stu-id="ad021-109">In a rolling application upgrade, hello upgrade is performed in stages.</span></span> <span data-ttu-id="ad021-110">À chaque étape, mise à niveau hello est sous-ensemble tooa appliqué de nœuds de cluster hello, appelé un domaine de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="ad021-110">At each stage, hello upgrade is applied tooa subset of nodes in hello cluster, called an update domain.</span></span> <span data-ttu-id="ad021-111">Par conséquent, application hello reste disponible pour l’ensemble de la mise à niveau hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-111">As a result, hello application remains available throughout hello upgrade.</span></span> <span data-ttu-id="ad021-112">Au cours de la mise à niveau de hello, cluster de hello peut contenir une combinaison de versions anciennes et nouvelles de hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-112">During hello upgrade, hello cluster may contain a mix of hello old and new versions.</span></span>

<span data-ttu-id="ad021-113">Pour cette raison, les versions de hello deux doivent être vers l’avant et vers l’arrière compatible.</span><span class="sxs-lookup"><span data-stu-id="ad021-113">For that reason, hello two versions must be forward and backward compatible.</span></span> <span data-ttu-id="ad021-114">Si elles ne sont pas compatibles, administrateur de l’application hello est responsable de la disponibilité d’une toomaintain de mise à niveau de plusieurs phases de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="ad021-114">If they are not compatible, hello application administrator is responsible for staging a multiple-phase upgrade toomaintain availability.</span></span> <span data-ttu-id="ad021-115">Dans une mise à niveau plusieurs phases, première étape de hello est mise à niveau tooan la version intermédiaire de l’application hello qui est compatible avec la version précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-115">In a multiple-phase upgrade, hello first step is upgrading tooan intermediate version of hello application that is compatible with hello previous version.</span></span> <span data-ttu-id="ad021-116">deuxième étape de Hello est version finale tooupgrade hello qui interrompt la compatibilité avec une version mise à jour préalable hello, mais est compatible avec la version intermédiaire de hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-116">hello second step is tooupgrade hello final version that breaks compatibility with hello pre-update version, but is compatible with hello intermediate version.</span></span>

<span data-ttu-id="ad021-117">Les domaines de mise à jour sont spécifiés dans le manifeste du cluster hello lorsque vous configurez hello cluster.</span><span class="sxs-lookup"><span data-stu-id="ad021-117">Update domains are specified in hello cluster manifest when you configure hello cluster.</span></span> <span data-ttu-id="ad021-118">Les domaines de mise à jour ne reçoivent pas les mises à jour dans un ordre particulier.</span><span class="sxs-lookup"><span data-stu-id="ad021-118">Update domains do not receive updates in a particular order.</span></span> <span data-ttu-id="ad021-119">Un domaine de mise à jour est une unité logique de déploiement pour une application.</span><span class="sxs-lookup"><span data-stu-id="ad021-119">An update domain is a logical unit of deployment for an application.</span></span> <span data-ttu-id="ad021-120">Les domaines de mise à jour permettent hello services tooremain à haute disponibilité pendant une mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="ad021-120">Update domains allow hello services tooremain at high availability during an upgrade.</span></span>

<span data-ttu-id="ad021-121">Mises à niveau propagées de non sont possibles si mise à niveau de hello tooall appliqué des nœuds dans le cluster hello, qui est le cas de hello lors de l’application hello n'a qu’un seul domaine de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="ad021-121">Non-rolling upgrades are possible if hello upgrade is applied tooall nodes in hello cluster, which is hello case when hello application has only one update domain.</span></span> <span data-ttu-id="ad021-122">Cette approche n’est pas recommandée étant donné que le service de hello tombe en panne et n’est pas disponible au moment de hello de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="ad021-122">This approach is not recommended, since hello service goes down and isn't available at hello time of upgrade.</span></span> <span data-ttu-id="ad021-123">En outre, Azure ne fournit aucune garantie quand un cluster est configuré avec un seul domaine de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="ad021-123">Additionally, Azure doesn't provide any guarantees when a cluster is set up with only one update domain.</span></span>

## <a name="health-checks-during-upgrades"></a><span data-ttu-id="ad021-124">Vérifications d'intégrité pendant les mises à niveau</span><span class="sxs-lookup"><span data-stu-id="ad021-124">Health checks during upgrades</span></span>
<span data-ttu-id="ad021-125">Pour une mise à niveau, les stratégies de contrôle d’intégrité sont toobe définies (ou les valeurs par défaut peuvent être utilisées).</span><span class="sxs-lookup"><span data-stu-id="ad021-125">For an upgrade, health policies have toobe set (or default values may be used).</span></span> <span data-ttu-id="ad021-126">Une mise à niveau est appelé réussie lorsque tous les domaines de mise à jour sont mis à niveau au sein de hello spécifié des délais d’expiration, et lors de la mise à jour des domaines sont considérées comme sains.</span><span class="sxs-lookup"><span data-stu-id="ad021-126">An upgrade is termed successful when all update domains are upgraded within hello specified time-outs, and when all update domains are deemed healthy.</span></span>  <span data-ttu-id="ad021-127">Un domaine de mise à jour intègre signifie que ce domaine de mise à jour hello passé toutes les vérifications d’intégrité hello spécifiées dans la stratégie de contrôle d’intégrité hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-127">A healthy update domain means that hello update domain passed all hello health checks specified in hello health policy.</span></span> <span data-ttu-id="ad021-128">Par exemple, une stratégie d'intégrité peut imposer que tous les services dans une instance d'application doivent être *intègres*, car l'intégrité est définie par Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ad021-128">For example, a health policy may mandate that all services within an application instance must be *healthy*, as health is defined by Service Fabric.</span></span>

<span data-ttu-id="ad021-129">Pendant une mise à jour effectuée par Service Fabric, les stratégies et vérifications d'intégrité sont indépendantes du service et de l'application.</span><span class="sxs-lookup"><span data-stu-id="ad021-129">Health policies and checks during upgrade by Service Fabric are service and application agnostic.</span></span> <span data-ttu-id="ad021-130">Autrement dit, aucun test spécifique au service n'est exécuté.</span><span class="sxs-lookup"><span data-stu-id="ad021-130">That is, no service-specific tests are done.</span></span>  <span data-ttu-id="ad021-131">Par exemple, votre service peut avoir besoin de débit, mais le Service Fabric n’a pas de débit de toocheck informations hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-131">For example, your service might have a throughput requirement, but Service Fabric does not have hello information toocheck throughput.</span></span> <span data-ttu-id="ad021-132">Consultez toohello [articles de contrôle d’intégrité](service-fabric-health-introduction.md) pour les contrôles de hello sont effectuées.</span><span class="sxs-lookup"><span data-stu-id="ad021-132">Refer toohello [health articles](service-fabric-health-introduction.md) for hello checks that are performed.</span></span> <span data-ttu-id="ad021-133">les vérifications Hello qui se produisent pendant une mise à niveau d’inclure de tests pour indique si le package d’application hello a été copié correctement, si le démarrage de l’instance hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="ad021-133">hello checks that happen during an upgrade include tests for whether hello application package was copied correctly, whether hello instance was started, and so on.</span></span>

<span data-ttu-id="ad021-134">intégrité des applications Hello est un regroupement d’entités enfants de hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-134">hello application health is an aggregation of hello child entities of hello application.</span></span> <span data-ttu-id="ad021-135">En bref, l’infrastructure de Service prend la valeur intégrité hello application hello par le biais d’intégrité hello signalé sur l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-135">In short, Service Fabric evaluates hello health of hello application through hello health that is reported on hello application.</span></span> <span data-ttu-id="ad021-136">Il évalue également la santé de tous les services hello application hello hello de cette manière.</span><span class="sxs-lookup"><span data-stu-id="ad021-136">It also evaluates hello health of all hello services for hello application this way.</span></span> <span data-ttu-id="ad021-137">Service Fabric davantage évalue l’intégrité hello de services d’application hello agrégation d’intégrité de hello leurs enfants, tels que des réplicas de service hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-137">Service Fabric further evaluates hello health of hello application services by aggregating hello health of their children, such as hello service replica.</span></span> <span data-ttu-id="ad021-138">Une fois que la stratégie de contrôle d’intégrité d’application hello est satisfaite, la mise à niveau hello peut continuer.</span><span class="sxs-lookup"><span data-stu-id="ad021-138">Once hello application health policy is satisfied, hello upgrade can proceed.</span></span> <span data-ttu-id="ad021-139">Si la stratégie de contrôle d’intégrité hello est violée, mise à niveau des applications hello échoue.</span><span class="sxs-lookup"><span data-stu-id="ad021-139">If hello health policy is violated, hello application upgrade fails.</span></span>

## <a name="upgrade-modes"></a><span data-ttu-id="ad021-140">Modes de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="ad021-140">Upgrade modes</span></span>
<span data-ttu-id="ad021-141">Hello mode que nous recommandons pour la mise à niveau de l’application est hello analysé, qui est le mode hello couramment utilisée.</span><span class="sxs-lookup"><span data-stu-id="ad021-141">hello mode that we recommend for application upgrade is hello monitored mode, which is hello commonly used mode.</span></span> <span data-ttu-id="ad021-142">Analysés en mode effectue la mise à niveau hello sur le domaine de mise à jour et si toutes les vérifications passe (par hello stratégie spécifiée), déplace automatiquement sur le domaine de mise à jour suivant toohello.</span><span class="sxs-lookup"><span data-stu-id="ad021-142">Monitored mode performs hello upgrade on one update domain, and if all health checks pass (per hello policy specified), moves on toohello next update domain automatically.</span></span>  <span data-ttu-id="ad021-143">Si l’échouent des vérifications d’intégrité et/ou des délais d’expiration sont atteints, mise à niveau hello est soit restaurée pour le domaine de mise à jour hello ou mode de hello est modifié toounmonitored manuel.</span><span class="sxs-lookup"><span data-stu-id="ad021-143">If health checks fail and/or time-outs are reached, hello upgrade is either rolled back for hello update domain, or hello mode is changed toounmonitored manual.</span></span> <span data-ttu-id="ad021-144">Vous pouvez configurer toochoose de mise à niveau hello un de ces deux modes pour les mises à niveau a échoué.</span><span class="sxs-lookup"><span data-stu-id="ad021-144">You can configure hello upgrade toochoose one of those two modes for failed upgrades.</span></span> 

<span data-ttu-id="ad021-145">Le mode manuel non contrôlé doit une intervention manuelle après chaque mise à niveau sur un domaine de mise à jour, le tookick désactiver la mise à niveau de hello sur hello domaine de mise à jour suivant.</span><span class="sxs-lookup"><span data-stu-id="ad021-145">Unmonitored manual mode needs manual intervention after every upgrade on an update domain, tookick off hello upgrade on hello next update domain.</span></span> <span data-ttu-id="ad021-146">Aucune vérification de l'intégrité de Service Fabric n'est effectuée.</span><span class="sxs-lookup"><span data-stu-id="ad021-146">No Service Fabric health checks are performed.</span></span> <span data-ttu-id="ad021-147">l’administrateur Hello effectue hello des vérifications d’intégrité ou d’état avant de commencer la mise à niveau hello dans le domaine de mise à jour suivant hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-147">hello administrator performs hello health or status checks before starting hello upgrade in hello next update domain.</span></span>

## <a name="upgrade-default-services"></a><span data-ttu-id="ad021-148">Mettre à niveau les services par défaut</span><span class="sxs-lookup"><span data-stu-id="ad021-148">Upgrade default services</span></span>
<span data-ttu-id="ad021-149">Par défaut des services au sein de l’application de Service Fabric peuvent être mis à niveau pendant le processus de mise à niveau hello d’une application.</span><span class="sxs-lookup"><span data-stu-id="ad021-149">Default services within Service Fabric application can be upgraded during hello upgrade process of an application.</span></span> <span data-ttu-id="ad021-150">Services par défaut sont définis dans hello [manifeste d’application](service-fabric-application-model.md#describe-an-application).</span><span class="sxs-lookup"><span data-stu-id="ad021-150">Default services are defined in hello [application manifest](service-fabric-application-model.md#describe-an-application).</span></span> <span data-ttu-id="ad021-151">Hello des règles standard de mise à niveau des services par défaut sont :</span><span class="sxs-lookup"><span data-stu-id="ad021-151">hello standard rules of upgrading default services are:</span></span>

1. <span data-ttu-id="ad021-152">Par défaut des services Bonjour nouvelle [manifeste d’application](service-fabric-application-model.md#describe-an-application) qui n’existent pas dans le cluster de hello sont créés.</span><span class="sxs-lookup"><span data-stu-id="ad021-152">Default services in hello new [application manifest](service-fabric-application-model.md#describe-an-application) that do not exist in hello cluster are created.</span></span>
> [!TIP]
> <span data-ttu-id="ad021-153">[EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) besoins toobe définir hello de tooenable tootrue suivant les règles.</span><span class="sxs-lookup"><span data-stu-id="ad021-153">[EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) needs toobe set tootrue tooenable hello following rules.</span></span> <span data-ttu-id="ad021-154">Cette fonctionnalité est prise en charge à partir de la version 5.5.</span><span class="sxs-lookup"><span data-stu-id="ad021-154">This feature is supported from v5.5.</span></span>

2. <span data-ttu-id="ad021-155">Les services par défaut présents à la fois dans le [manifeste de l’application](service-fabric-application-model.md#describe-an-application) précédent et dans la nouvelle version sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="ad021-155">Default services existing in both previous [application manifest](service-fabric-application-model.md#describe-an-application) and new version are updated.</span></span> <span data-ttu-id="ad021-156">Descriptions de service dans la nouvelle version de hello remplacerait ceux déjà présents dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="ad021-156">Service descriptions in hello new version would overwrite those already in hello cluster.</span></span> <span data-ttu-id="ad021-157">La mise à niveau de l’application serait restaurée automatiquement en cas d’échec de mise à jour des services par défaut.</span><span class="sxs-lookup"><span data-stu-id="ad021-157">Application upgrade would rollback automatically upon updating default service failure.</span></span>
3. <span data-ttu-id="ad021-158">Par défaut des services Bonjour précédente [manifeste d’application](service-fabric-application-model.md#describe-an-application) mais pas dans la nouvelle version de hello sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="ad021-158">Default services in hello previous [application manifest](service-fabric-application-model.md#describe-an-application) but not in hello new version are deleted.</span></span> <span data-ttu-id="ad021-159">**Notez qu’il n’est pas possible de rétablir les services par défaut supprimés.**</span><span class="sxs-lookup"><span data-stu-id="ad021-159">**Note that this deleting default services can not be reverted.**</span></span>

<span data-ttu-id="ad021-160">En cas d’une application mise à niveau est annulée, services par défaut sont rétablies toohello état avant le début de la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="ad021-160">In case of an application upgrade is rolled back, default services are reverted toohello status before upgrade started.</span></span> <span data-ttu-id="ad021-161">Mais les services supprimés ne peuvent plus être créés.</span><span class="sxs-lookup"><span data-stu-id="ad021-161">But deleted services can never be created.</span></span>

## <a name="application-upgrade-flowchart"></a><span data-ttu-id="ad021-162">Organigramme de la mise à niveau d'application</span><span class="sxs-lookup"><span data-stu-id="ad021-162">Application upgrade flowchart</span></span>
<span data-ttu-id="ad021-163">Organigramme de Hello ci-dessous peut vous aider à comprendre le processus de mise à niveau hello d’une application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ad021-163">hello flowchart following this paragraph can help you understand hello upgrade process of a Service Fabric application.</span></span> <span data-ttu-id="ad021-164">En particulier, les flux hello décrit comment hello délais d’attente, y compris *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, et *UpgradeHealthCheckInterval*, permettent de contrôler lors de la mise à niveau hello dans le domaine de mise à jour est considérée comme une réussite ou échec.</span><span class="sxs-lookup"><span data-stu-id="ad021-164">In particular, hello flow describes how hello time-outs, including *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, and *UpgradeHealthCheckInterval*, help control when hello upgrade in one update domain is considered a success or a failure.</span></span>

![processus de mise à niveau Hello pour une Application Service Fabric][image]

## <a name="next-steps"></a><span data-ttu-id="ad021-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad021-166">Next steps</span></span>
<span data-ttu-id="ad021-167">[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad021-167">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="ad021-168">[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad021-168">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="ad021-169">Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="ad021-169">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="ad021-170">Rendre les mises à niveau de votre application compatible par learning comment toouse [sérialisation des données](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="ad021-170">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="ad021-171">Découvrez comment toouse des fonctionnalités avancées lors de la mise à niveau de votre application en vous reportant trop[rubriques avancées](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="ad021-171">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>

<span data-ttu-id="ad021-172">Résoudre les problèmes courants dans les mises à niveau de l’application en faisant référence à des étapes de toohello de [résolution des problèmes de mises à niveau Application](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ad021-172">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png