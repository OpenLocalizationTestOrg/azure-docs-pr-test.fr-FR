---
title: "rubriques relatives à la mise à niveau des applications d’aaaAdvanced | Documents Microsoft"
description: "Cet article décrit certaines rubriques avancées relatives tooupgrading une application de Service Fabric."
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
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="1c9a5-103">Mise à niveau d’une application Service Fabric : rubriques avancées</span><span class="sxs-lookup"><span data-stu-id="1c9a5-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="1c9a5-104">Ajout ou suppression de services pendant la mise à niveau d'une application</span><span class="sxs-lookup"><span data-stu-id="1c9a5-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="1c9a5-105">Si un nouveau service est ajouté application tooan qui est déjà déployée et publiée une mise à niveau, hello nouveau service est ajouté toohello déployé application.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-105">If a new service is added tooan application that is already deployed, and published as an upgrade, hello new service is added toohello deployed application.</span></span>  <span data-ttu-id="1c9a5-106">Une mise à niveau n’affecte pas un des services hello faisant déjà partie d’une application hello.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-106">Such an upgrade does not affect any of hello services that were already part of hello application.</span></span> <span data-ttu-id="1c9a5-107">Toutefois, une instance de service hello qui a été ajouté doit être démarrée pour toobe service hello nouvelle active (à l’aide de hello `New-ServiceFabricService` applet de commande).</span><span class="sxs-lookup"><span data-stu-id="1c9a5-107">However, an instance of hello service that was added must be started for hello new service toobe active (using hello `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="1c9a5-108">Des services peuvent également être supprimés d’une application dans le cadre d’une mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="1c9a5-109">Toutefois, toutes les instances en cours du service de hello à supprimer doivent être arrêtés avant de poursuivre la mise à niveau hello (à l’aide de hello `Remove-ServiceFabricService` applet de commande).</span><span class="sxs-lookup"><span data-stu-id="1c9a5-109">However, all current instances of hello to-be-deleted service must be stopped before proceeding with hello upgrade (using hello `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="1c9a5-110">Mode de mise à niveau manuelle</span><span class="sxs-lookup"><span data-stu-id="1c9a5-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="1c9a5-111">mode manuel de Hello non contrôlée doit être considéré uniquement pour une mise à niveau a échoué ou suspendue.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-111">hello unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="1c9a5-112">le mode surveillé Hello est hello recommandé en mode de mise à niveau pour les applications de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-112">hello monitored mode is hello recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="1c9a5-113">Azure Service Fabric fournit plusieurs modes de mise à niveau des clusters de développement et de production toosupport.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-113">Azure Service Fabric provides multiple upgrade modes toosupport development and production clusters.</span></span> <span data-ttu-id="1c9a5-114">Les options de déploiement choisies peuvent être différentes pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="1c9a5-115">mise à niveau application propagée Hello analysé est hello toouse de mise à niveau plus classique dans l’environnement de production hello.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-115">hello monitored rolling application upgrade is hello most typical upgrade toouse in hello production environment.</span></span> <span data-ttu-id="1c9a5-116">Lors de la mise à niveau de hello stratégie est spécifiée, Service Fabric garantit qu’application hello est saine avant de la mise à niveau hello se poursuit.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-116">When hello upgrade policy is specified, Service Fabric ensures that hello application is healthy before hello upgrade proceeds.</span></span>

 <span data-ttu-id="1c9a5-117">administrateur de l’application Hello peut utiliser manuel hello propagée application en mode de mise à niveau toohave contrôle total sur la progression de mise à niveau hello via hello différents domaines de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-117">hello application administrator can use hello manual rolling application upgrade mode toohave total control over hello upgrade progress through hello various upgrade domains.</span></span> <span data-ttu-id="1c9a5-118">Ce mode est utile lorsqu’une stratégie d’évaluation d’intégrité personnalisé ou complexe est nécessaire, ou une mise à niveau non conventionnelle se produit (par exemple, application hello est déjà une perte de données).</span><span class="sxs-lookup"><span data-stu-id="1c9a5-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, hello application is already in data loss).</span></span>

<span data-ttu-id="1c9a5-119">Enfin, hello automatisée mise à niveau propagée d’application est utile pour le développement ou de test des environnements tooprovide une itération rapide cycle pendant le développement du service.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-119">Finally, hello automated rolling application upgrade is useful for development or testing environments tooprovide a fast iteration cycle during service development.</span></span>

## <a name="change-toomanual-upgrade-mode"></a><span data-ttu-id="1c9a5-120">Changement du mode de mise à niveau toomanual</span><span class="sxs-lookup"><span data-stu-id="1c9a5-120">Change toomanual upgrade mode</span></span>
<span data-ttu-id="1c9a5-121">**Manuel**--arrêt hello application mise à niveau à Bonjour Bonjour actuel UD et modification de niveau tooUnmonitored de mode manuel.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-121">**Manual**--Stop hello application upgrade at hello current UD and change hello upgrade mode tooUnmonitored Manual.</span></span> <span data-ttu-id="1c9a5-122">administrateur Hello doit toomanually appel **MoveNextApplicationUpgradeDomainAsync** tooproceed avec hello mise à niveau ou d’un déclencheur d’une restauration en lançant une nouvelle mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-122">hello administrator needs toomanually call **MoveNextApplicationUpgradeDomainAsync** tooproceed with hello upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="1c9a5-123">Une fois la mise à niveau hello entrée en mode manuel de hello, elle reste en mode manuel de hello jusqu'à ce qu’une nouvelle mise à niveau est déclenché.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-123">Once hello upgrade enters into hello Manual mode, it stays in hello Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="1c9a5-124">Hello **GetApplicationUpgradeProgressAsync** commande retourne l’ensemble fibre optique\_APPLICATION\_mise à niveau\_état\_propagées\_par progression\_en attente.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-124">hello **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="1c9a5-125">Effectuer une mise à niveau avec un package différentiel</span><span class="sxs-lookup"><span data-stu-id="1c9a5-125">Upgrade with a diff package</span></span>
<span data-ttu-id="1c9a5-126">Une application Service Fabric peut être mise à niveau via une mise en service avec un package d'application autonome et complet.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="1c9a5-127">Une application peut également être mis à niveau à l’aide d’un package de comparaison qui contient les fichiers d’application hello mis à jour uniquement, hello mis à jour le manifeste d’application et les fichiers manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-127">An application can also be upgraded by using a diff package that contains only hello updated application files, hello updated application manifest, and hello service manifest files.</span></span>

<span data-ttu-id="1c9a5-128">Un package d’application complet contient tous les hello fichiers nécessaires toostart et exécuter une application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-128">A full application package contains all hello files necessary toostart and run a Service Fabric application.</span></span> <span data-ttu-id="1c9a5-129">Un package diff contient uniquement les fichiers de hello changé entre la dernière disposition de hello et mise à niveau actuel de hello, plus les fichiers manifestes de manifeste de l’application complète hello et service de hello.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-129">A diff package contains only hello files that changed between hello last provision and hello current upgrade, plus hello full application manifest and hello service manifest files.</span></span> <span data-ttu-id="1c9a5-130">Toute référence dans le manifeste d’application hello ou service qui ne figure pas dans la disposition de build hello est recherché dans le magasin d’images hello.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-130">Any reference in hello application manifest or service manifest that can't be found in hello build layout is searched for in hello image store.</span></span>

<span data-ttu-id="1c9a5-131">Les packages d’application complet sont requis pour hello première installation d’un cluster de toohello d’application.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-131">Full application packages are required for hello first installation of an application toohello cluster.</span></span> <span data-ttu-id="1c9a5-132">Les mises à jour suivantes peuvent être un package d'application complet ou un package différentiel.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="1c9a5-133">Situations qui se prêtent à l'utilisation d'un package différentiel :</span><span class="sxs-lookup"><span data-stu-id="1c9a5-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="1c9a5-134">Un package différentiel est préférable quand vous disposez d’un package d’application volumineux qui référence plusieurs fichiers manifeste de service et/ou plusieurs packages de code, de configuration ou de données.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="1c9a5-135">Un package de comparaison est préférable lorsque vous disposez d’un système de déploiement qui génère la disposition de build hello directement à partir de votre processus de génération d’application.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-135">A diff package is preferred when you have a deployment system that generates hello build layout directly from your application build process.</span></span> <span data-ttu-id="1c9a5-136">Dans ce cas, même si le code de hello n’a pas changé, assemblys nouvellement générés obtenir une somme de contrôle différents.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-136">In this case, even though hello code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="1c9a5-137">À l’aide d’un package d’application complet nécessiterait vous tooupdate hello version sur tous les packages de code.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-137">Using a full application package would require you tooupdate hello version on all code packages.</span></span> <span data-ttu-id="1c9a5-138">À l’aide d’un package de comparaison, vous fournissez uniquement les fichiers hello modifiés et les fichiers de manifeste de hello dont la version de hello a changé.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-138">Using a diff package, you only provide hello files that changed and hello manifest files where hello version has changed.</span></span>

<span data-ttu-id="1c9a5-139">Lorsqu’une application est mise à niveau à l’aide de Visual Studio, il se peut que hello diff package est publié automatiquement.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-139">When an application is upgraded using Visual Studio, hello diff package is published automatically.</span></span> <span data-ttu-id="1c9a5-140">toocreate un package diff hello manuellement, le manifeste d’application et hello manifestes doivent être mis à jour, mais uniquement les packages hello modifié doivent figurer dans le package d’application finale hello.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-140">toocreate a diff package manually, hello application manifest, and hello service manifests must be updated, but only hello changed packages should be included in hello final application package.</span></span>

<span data-ttu-id="1c9a5-141">Par exemple, commençons par hello suite de l’application (numéros de version fournies pour faciliter la compréhension) :</span><span class="sxs-lookup"><span data-stu-id="1c9a5-141">For example, let's start with hello following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="1c9a5-142">Maintenant, supposons que vous souhaitiez tooupdate uniquement hello package de code de service1 à l’aide d’un package de comparaison à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-142">Now, let's assume you wanted tooupdate only hello code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="1c9a5-143">À présent, votre application mise à jour a hello suivant la structure de dossiers :</span><span class="sxs-lookup"><span data-stu-id="1c9a5-143">Now, your updated application has hello following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="1c9a5-144">Dans ce cas, vous mettez à jour too2.0.0 de manifeste application hello et manifeste du service de mise à jour du package de code hello service1 tooreflect hello.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-144">In this case, you update hello application manifest too2.0.0, and hello service manifest for service1 tooreflect hello code package update.</span></span> <span data-ttu-id="1c9a5-145">dossier Hello pour votre package d’application a hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="1c9a5-145">hello folder for your application package would have hello following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="1c9a5-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1c9a5-146">Next steps</span></span>
<span data-ttu-id="1c9a5-147">[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="1c9a5-148">[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c9a5-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="1c9a5-149">Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="1c9a5-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="1c9a5-150">Rendre les mises à niveau de votre application compatible par learning comment toouse [sérialisation des données](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="1c9a5-150">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="1c9a5-151">Résoudre les problèmes courants dans les mises à niveau de l’application en faisant référence à des étapes de toohello de [résolution des problèmes de mises à niveau Application](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1c9a5-151">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
