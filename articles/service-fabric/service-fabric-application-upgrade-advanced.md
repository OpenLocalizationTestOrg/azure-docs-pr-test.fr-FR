---
title: "Rubriques de mise à niveau d’application avancée | Microsoft Docs"
description: "Cet article traite de sujets avancés se rapportant à la mise à niveau d’une application Service Fabric."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: 8d3b922f3d50b645ac9db2cc879a319df1262e0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="339ee-103">Mise à niveau d’une application Service Fabric : rubriques avancées</span><span class="sxs-lookup"><span data-stu-id="339ee-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="339ee-104">Ajout ou suppression de services pendant la mise à niveau d'une application</span><span class="sxs-lookup"><span data-stu-id="339ee-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="339ee-105">Si un service est ajouté à une application déjà déployée et publiée en tant que mise à niveau, le nouveau service est ajouté à l’application déployée.</span><span class="sxs-lookup"><span data-stu-id="339ee-105">If a new service is added to an application that is already deployed, and published as an upgrade, the new service is added to the deployed application.</span></span>  <span data-ttu-id="339ee-106">Une telle mise à niveau n’affecte pas les services faisant déjà partie de l’application.</span><span class="sxs-lookup"><span data-stu-id="339ee-106">Such an upgrade does not affect any of the services that were already part of the application.</span></span> <span data-ttu-id="339ee-107">Cependant, une instance du service ajouté doit être démarrée pour activer le nouveau service (à l’aide de l’applet de commande `New-ServiceFabricService` ).</span><span class="sxs-lookup"><span data-stu-id="339ee-107">However, an instance of the service that was added must be started for the new service to be active (using the `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="339ee-108">Des services peuvent également être supprimés d’une application dans le cadre d’une mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="339ee-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="339ee-109">Toutefois, toutes les instances en cours du service à supprimer doivent être arrêtées avant de procéder à la mise à niveau (à l’aide de l’applet de commande `Remove-ServiceFabricService` ).</span><span class="sxs-lookup"><span data-stu-id="339ee-109">However, all current instances of the to-be-deleted service must be stopped before proceeding with the upgrade (using the `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="339ee-110">Mode de mise à niveau manuelle</span><span class="sxs-lookup"><span data-stu-id="339ee-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="339ee-111">Le mode manuel non surveillé ne peut être envisagé que pour une mise à niveau ayant échoué ou suspendue.</span><span class="sxs-lookup"><span data-stu-id="339ee-111">The unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="339ee-112">Le mode surveillé est le mode de mise à niveau recommandé pour les applications Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="339ee-112">The monitored mode is the recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="339ee-113">Azure Service Fabric fournit plusieurs modes de mise à niveau pour prendre en charge les clusters de développement et de production.</span><span class="sxs-lookup"><span data-stu-id="339ee-113">Azure Service Fabric provides multiple upgrade modes to support development and production clusters.</span></span> <span data-ttu-id="339ee-114">Les options de déploiement choisies peuvent être différentes pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="339ee-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="339ee-115">La mise à niveau d’application propagée surveillée est la mise à niveau la plus courante à utiliser dans l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="339ee-115">The monitored rolling application upgrade is the most typical upgrade to use in the production environment.</span></span> <span data-ttu-id="339ee-116">Quand la stratégie de mise à niveau est spécifiée, Service Fabric s'assure que l'application est saine avant que la mise à niveau ne se poursuive.</span><span class="sxs-lookup"><span data-stu-id="339ee-116">When the upgrade policy is specified, Service Fabric ensures that the application is healthy before the upgrade proceeds.</span></span>

 <span data-ttu-id="339ee-117">L’administrateur d’application peut utiliser le mode de mise à niveau d’application propagée manuelle pour contrôler totalement la progression de la mise à niveau à travers les différents domaines de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="339ee-117">The application administrator can use the manual rolling application upgrade mode to have total control over the upgrade progress through the various upgrade domains.</span></span> <span data-ttu-id="339ee-118">Ce mode est utile lorsqu’une stratégie d’évaluation d’intégrité personnalisée ou complexe est nécessaire ou dans le cas d’une mise à niveau non conventionnelle (par exemple, l’application est déjà dans une situation de perte de données).</span><span class="sxs-lookup"><span data-stu-id="339ee-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, the application is already in data loss).</span></span>

<span data-ttu-id="339ee-119">Enfin, la mise à niveau d’application propagée automatisée permet aux environnements de développement ou de test de fournir un cycle d’itération rapide pendant le développement du service.</span><span class="sxs-lookup"><span data-stu-id="339ee-119">Finally, the automated rolling application upgrade is useful for development or testing environments to provide a fast iteration cycle during service development.</span></span>

## <a name="change-to-manual-upgrade-mode"></a><span data-ttu-id="339ee-120">Passer en mode de mise à niveau manuelle</span><span class="sxs-lookup"><span data-stu-id="339ee-120">Change to manual upgrade mode</span></span>
<span data-ttu-id="339ee-121">**Mode manuel**: arrêter la mise à niveau de l’application au domaine de mise à niveau actuel et passer en mode de mise à niveau manuelle non surveillée.</span><span class="sxs-lookup"><span data-stu-id="339ee-121">**Manual**--Stop the application upgrade at the current UD and change the upgrade mode to Unmonitored Manual.</span></span> <span data-ttu-id="339ee-122">L’administrateur doit appeler manuellement **MoveNextApplicationUpgradeDomainAsync** pour procéder à la mise à niveau ou déclencher une restauration en initiant une nouvelle mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="339ee-122">The administrator needs to manually call **MoveNextApplicationUpgradeDomainAsync** to proceed with the upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="339ee-123">Une fois que la mise à niveau est en mode manuel, elle demeure dans ce mode jusqu'à ce qu'une nouvelle mise à niveau soit initiée.</span><span class="sxs-lookup"><span data-stu-id="339ee-123">Once the upgrade enters into the Manual mode, it stays in the Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="339ee-124">La commande **GetApplicationUpgradeProgressAsync** renvoie FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span><span class="sxs-lookup"><span data-stu-id="339ee-124">The **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="339ee-125">Effectuer une mise à niveau avec un package différentiel</span><span class="sxs-lookup"><span data-stu-id="339ee-125">Upgrade with a diff package</span></span>
<span data-ttu-id="339ee-126">Une application Service Fabric peut être mise à niveau via une mise en service avec un package d'application autonome et complet.</span><span class="sxs-lookup"><span data-stu-id="339ee-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="339ee-127">Une application peut également être mise à niveau à l’aide d’un package différentiel qui contient uniquement les fichiers d’application mis à jour, les fichiers manifeste d’application mis à jour et manifeste de service.</span><span class="sxs-lookup"><span data-stu-id="339ee-127">An application can also be upgraded by using a diff package that contains only the updated application files, the updated application manifest, and the service manifest files.</span></span>

<span data-ttu-id="339ee-128">Un package d'application complet contient tous les fichiers nécessaires pour démarrer et exécuter une application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="339ee-128">A full application package contains all the files necessary to start and run a Service Fabric application.</span></span> <span data-ttu-id="339ee-129">Un package différentiel contient uniquement les fichiers qui ont changé entre la dernière mise en service et la mise à niveau actuelle, ainsi que les fichiers manifeste d’application et manifeste de service complets.</span><span class="sxs-lookup"><span data-stu-id="339ee-129">A diff package contains only the files that changed between the last provision and the current upgrade, plus the full application manifest and the service manifest files.</span></span> <span data-ttu-id="339ee-130">Toute référence dans le manifeste d’application ou de service qui est introuvable dans la disposition de la build est recherchée dans le magasin d’images.</span><span class="sxs-lookup"><span data-stu-id="339ee-130">Any reference in the application manifest or service manifest that can't be found in the build layout is searched for in the image store.</span></span>

<span data-ttu-id="339ee-131">Des packages d’application complets sont nécessaires pour la première installation d’une application sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="339ee-131">Full application packages are required for the first installation of an application to the cluster.</span></span> <span data-ttu-id="339ee-132">Les mises à jour suivantes peuvent être un package d'application complet ou un package différentiel.</span><span class="sxs-lookup"><span data-stu-id="339ee-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="339ee-133">Situations qui se prêtent à l'utilisation d'un package différentiel :</span><span class="sxs-lookup"><span data-stu-id="339ee-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="339ee-134">Un package différentiel est préférable quand vous disposez d’un package d’application volumineux qui référence plusieurs fichiers manifeste de service et/ou plusieurs packages de code, de configuration ou de données.</span><span class="sxs-lookup"><span data-stu-id="339ee-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="339ee-135">Un package différentiel est préférable quand vous disposez d’un système de déploiement qui génère la disposition de la build directement à partir de votre processus de génération d’application.</span><span class="sxs-lookup"><span data-stu-id="339ee-135">A diff package is preferred when you have a deployment system that generates the build layout directly from your application build process.</span></span> <span data-ttu-id="339ee-136">Dans ce cas, même si le code n’a pas changé, les assemblys nouvellement générés obtiennent une somme de contrôle différente.</span><span class="sxs-lookup"><span data-stu-id="339ee-136">In this case, even though the code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="339ee-137">Si vous utilisez un package d'application complet, vous devez mettre à jour la version installée sur tous les packages de code.</span><span class="sxs-lookup"><span data-stu-id="339ee-137">Using a full application package would require you to update the version on all code packages.</span></span> <span data-ttu-id="339ee-138">Si vous utilisez un package différentiel, vous fournissez uniquement les fichiers qui ont changé et les fichiers manifeste dont la version a changé.</span><span class="sxs-lookup"><span data-stu-id="339ee-138">Using a diff package, you only provide the files that changed and the manifest files where the version has changed.</span></span>

<span data-ttu-id="339ee-139">Lorsqu'une application est mise à niveau à l'aide de Visual Studio, le package différentiel est automatiquement publié.</span><span class="sxs-lookup"><span data-stu-id="339ee-139">When an application is upgraded using Visual Studio, the diff package is published automatically.</span></span> <span data-ttu-id="339ee-140">Pour créer manuellement un package différentiel, le manifeste d’application et les manifestes de service doivent être mis à jour, mais seuls les packages modifiés doivent être inclus dans le package d’application final.</span><span class="sxs-lookup"><span data-stu-id="339ee-140">To create a diff package manually, the application manifest, and the service manifests must be updated, but only the changed packages should be included in the final application package.</span></span>

<span data-ttu-id="339ee-141">Commençons par exemple par l'application suivante (numéros de version fournis pour faciliter la compréhension) :</span><span class="sxs-lookup"><span data-stu-id="339ee-141">For example, let's start with the following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="339ee-142">Supposons à présent que vous souhaitiez mettre à jour uniquement le package de code de service1 à l'aide d'un package différentiel avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="339ee-142">Now, let's assume you wanted to update only the code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="339ee-143">À présent, votre application mise à jour présente la structure des dossiers suivante :</span><span class="sxs-lookup"><span data-stu-id="339ee-143">Now, your updated application has the following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="339ee-144">Dans ce cas, vous mettez à jour le manifeste d'application à la version 2.0.0 ainsi que le manifeste de service pour service1 afin de refléter la mise à jour du package de code.</span><span class="sxs-lookup"><span data-stu-id="339ee-144">In this case, you update the application manifest to 2.0.0, and the service manifest for service1 to reflect the code package update.</span></span> <span data-ttu-id="339ee-145">La structure des dossiers de votre package d’application serait la suivante :</span><span class="sxs-lookup"><span data-stu-id="339ee-145">The folder for your application package would have the following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="339ee-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="339ee-146">Next steps</span></span>
<span data-ttu-id="339ee-147">[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="339ee-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="339ee-148">[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="339ee-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="339ee-149">Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="339ee-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="339ee-150">Rendez les mises à niveau de votre application compatibles en apprenant à utilisez la [Sérialisation des données](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="339ee-150">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="339ee-151">Résolvez les problèmes courants de mise à niveau de l’application en vous reportant aux étapes de [Résolution des problèmes de mise à niveau des applications](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="339ee-151">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
