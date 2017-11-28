---
title: "Mise à l’échelle automatique et environnement App Service v1"
description: "Mise à l’échelle automatique et environnement App Service"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: f32affd285f3918feb0e893543f2a28f678b7b10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="22e14-103">Mise à l’échelle automatique et environnement App Service v1</span><span class="sxs-lookup"><span data-stu-id="22e14-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="22e14-104">Cet article traite de l’environnement App Service Environment v1.</span><span class="sxs-lookup"><span data-stu-id="22e14-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="22e14-105">Il existe une version plus récente de l’environnement App Service Environment, plus facile à utiliser et qui s’exécute sur des infrastructures plus puissantes.</span><span class="sxs-lookup"><span data-stu-id="22e14-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="22e14-106">Pour en savoir plus sur la nouvelle version, commencez par la [Présentation de l’environnement App Service](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="22e14-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="22e14-107">Les environnements Azure App Service prennent en charge la *mise à l’échelle automatique*.</span><span class="sxs-lookup"><span data-stu-id="22e14-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="22e14-108">Vous pouvez mettre à l’échelle automatiquement des pools de Workers individuels en fonction de mesures ou de la planification.</span><span class="sxs-lookup"><span data-stu-id="22e14-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Options de mise à l’échelle automatique d’un pool de Workers.][intro]

<span data-ttu-id="22e14-110">La mise à l’échelle automatique permet d’optimiser l’utilisation de vos ressources en agrandissant et en réduisant automatiquement un environnement App Service afin de l’adapter à votre budget et/ou à votre profil de charge.</span><span class="sxs-lookup"><span data-stu-id="22e14-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="22e14-111">Configurer la mise à l’échelle automatique du pool de Workers</span><span class="sxs-lookup"><span data-stu-id="22e14-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="22e14-112">Vous pouvez accéder à la fonctionnalité de mise à l’échelle automatique à partir de l’onglet **Paramètres** du pool de Workers.</span><span class="sxs-lookup"><span data-stu-id="22e14-112">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span></span>

![Onglet Paramètres du pool de Workers.][settings-scale]

<span data-ttu-id="22e14-114">À partir de là, l’interface doit vous paraître assez familière, car elle est similaire à celle de la mise à l’échelle d’un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="22e14-114">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span></span> 

![Paramètres de mise à l’échelle manuelle.][scale-manual]

<span data-ttu-id="22e14-116">Vous pouvez également configurer un profil de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="22e14-116">You can also configure an autoscale profile.</span></span>

![Paramètres de mise à l’échelle automatique.][scale-profile]

<span data-ttu-id="22e14-118">Les profils de mise à l’échelle automatique sont utiles pour définir des limites à votre mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="22e14-118">Autoscale profiles are useful to set limits on your scale.</span></span> <span data-ttu-id="22e14-119">Ainsi, vous pouvez obtenir des résultats satisfaisants en définissant une valeur de mise à l’échelle limite inférieure (1) et une valeur de plafonnement prévisible en définissant une limite supérieure (2).</span><span class="sxs-lookup"><span data-stu-id="22e14-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Paramètres de mise à l’échelle dans le profil.][scale-profile2]

<span data-ttu-id="22e14-121">Une fois qu’un profil est défini, vous pouvez ajouter des règles de mise à l’échelle automatique pour augmenter ou réduire le nombre d’instances dans le pool de Workers dans les limites définies par le profil.</span><span class="sxs-lookup"><span data-stu-id="22e14-121">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span></span> <span data-ttu-id="22e14-122">Les règles de mise à l’échelle automatique sont basées sur les mesures.</span><span class="sxs-lookup"><span data-stu-id="22e14-122">Autoscale rules are based on metrics.</span></span>

![Règle de mise à l’échelle.][scale-rule]

 <span data-ttu-id="22e14-124">Toutes les règles de mesure du pool de workers ou du frontend peuvent être utilisées pour définir des règles de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="22e14-124">Any worker pool or front-end metrics can be used to define autoscale rules.</span></span> <span data-ttu-id="22e14-125">Ces mesures sont les mêmes que celles que vous pouvez surveiller dans les graphiques de panneau de ressource ou pour lesquelles vous pouvez définir une alerte.</span><span class="sxs-lookup"><span data-stu-id="22e14-125">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="22e14-126">Exemple de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="22e14-126">Autoscale example</span></span>
<span data-ttu-id="22e14-127">La mise à l’échelle automatique d’un environnement App Service est mieux illustrée par un scénario.</span><span class="sxs-lookup"><span data-stu-id="22e14-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="22e14-128">Cet article décrit tous les éléments à prendre en compte lorsque vous configurez la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="22e14-128">This article explains all the necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="22e14-129">L’article vous guide tout au long des interactions qui ont lieu lorsque vous réalisez une mise à l’échelle automatique d’environnements App Service hébergés dans un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="22e14-129">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="22e14-130">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="22e14-130">Scenario introduction</span></span>
<span data-ttu-id="22e14-131">Frank est administrateur système pour une entreprise. Il a migré une partie des charges de travail qu’il gère vers un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="22e14-131">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span></span>

<span data-ttu-id="22e14-132">L’environnement App Service est configuré sur mise à l’échelle manuelle, comme suit :</span><span class="sxs-lookup"><span data-stu-id="22e14-132">The App Service environment is configured to manual scale as follows:</span></span>

* <span data-ttu-id="22e14-133">**Serveurs frontaux** : 3</span><span class="sxs-lookup"><span data-stu-id="22e14-133">**Front ends:** 3</span></span>
* <span data-ttu-id="22e14-134">**Pool de Workers 1**: 10</span><span class="sxs-lookup"><span data-stu-id="22e14-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="22e14-135">**Pool de Workers 2**: 5</span><span class="sxs-lookup"><span data-stu-id="22e14-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="22e14-136">**Pool de Workers 3**: 5</span><span class="sxs-lookup"><span data-stu-id="22e14-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="22e14-137">Le pool de Workers 1 est utilisé pour les charges de travail, tandis que le pool de Workers 2 et le pool de Workers 3 sont utilisés pour les charges de travail de développement et d’assurance qualité.</span><span class="sxs-lookup"><span data-stu-id="22e14-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="22e14-138">Les plans App Service pour l’assurance qualité et le développement sont configurés pour la mise à l’échelle manuelle.</span><span class="sxs-lookup"><span data-stu-id="22e14-138">The App Service plans for QA and dev are configured to manual scale.</span></span> <span data-ttu-id="22e14-139">Le plan App Service de production est configuré pour la mise à l’échelle automatique afin de gérer les variations de charge et de trafic.</span><span class="sxs-lookup"><span data-stu-id="22e14-139">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span></span>

<span data-ttu-id="22e14-140">Frank connaît bien l’application.</span><span class="sxs-lookup"><span data-stu-id="22e14-140">Frank is very familiar with the application.</span></span> <span data-ttu-id="22e14-141">Il sait que les heures de pointe de charge sont situées entre 9 h et 18 h, car il s’agit d’une application métier (LOB) utilisée par les employés lorsqu’ils sont au bureau.</span><span class="sxs-lookup"><span data-stu-id="22e14-141">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span></span> <span data-ttu-id="22e14-142">Le taux d’utilisation chute une fois que les utilisateurs ont fini leur journée de travail.</span><span class="sxs-lookup"><span data-stu-id="22e14-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="22e14-143">En dehors des heures de pointe, il existe toujours une charge, car les utilisateurs peuvent accéder à distance à l’application via leurs appareils mobiles ou leurs ordinateurs personnels.</span><span class="sxs-lookup"><span data-stu-id="22e14-143">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="22e14-144">Le plan App Service de production est déjà configuré sur la mise à l’échelle automatique basée sur le taux d’utilisation du processeur avec les règles suivantes :</span><span class="sxs-lookup"><span data-stu-id="22e14-144">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span></span>

![Paramètres spécifiques pour une application métier.][asp-scale]

| <span data-ttu-id="22e14-146">**Profil de la mise à l’échelle automatique – Jours de semaine – Plan App Service**</span><span class="sxs-lookup"><span data-stu-id="22e14-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="22e14-147">**Profil de la mise à l’échelle automatique – Week-ends – Plan App Service**</span><span class="sxs-lookup"><span data-stu-id="22e14-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="22e14-148">**Nom :** profil jour de semaine</span><span class="sxs-lookup"><span data-stu-id="22e14-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="22e14-149">**Nom :** profil week-end</span><span class="sxs-lookup"><span data-stu-id="22e14-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="22e14-150">**Mise à l’échelle selon :** Planification et règles de performances</span><span class="sxs-lookup"><span data-stu-id="22e14-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="22e14-151">**Mise à l’échelle selon :** Planification et règles de performances</span><span class="sxs-lookup"><span data-stu-id="22e14-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="22e14-152">**Profil :** jours de la semaine</span><span class="sxs-lookup"><span data-stu-id="22e14-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="22e14-153">**Profil :** week-end</span><span class="sxs-lookup"><span data-stu-id="22e14-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="22e14-154">**Type :** périodicité</span><span class="sxs-lookup"><span data-stu-id="22e14-154">**Type:** Recurrence</span></span> |<span data-ttu-id="22e14-155">**Type :** périodicité</span><span class="sxs-lookup"><span data-stu-id="22e14-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="22e14-156">**Plage cible :** 5 à 20 instances</span><span class="sxs-lookup"><span data-stu-id="22e14-156">**Target range:** 5 to 20 instances</span></span> |<span data-ttu-id="22e14-157">**Plage cible :** 3 à 10 instances</span><span class="sxs-lookup"><span data-stu-id="22e14-157">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="22e14-158">**Jours :** lundi, mardi, mercredi, jeudi, vendredi</span><span class="sxs-lookup"><span data-stu-id="22e14-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="22e14-159">**Jours :** samedi, dimanche</span><span class="sxs-lookup"><span data-stu-id="22e14-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="22e14-160">**Heure de début :** 9 h</span><span class="sxs-lookup"><span data-stu-id="22e14-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="22e14-161">**Heure de début :** 9 h</span><span class="sxs-lookup"><span data-stu-id="22e14-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="22e14-162">**Fuseau horaire :** UTC-08</span><span class="sxs-lookup"><span data-stu-id="22e14-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="22e14-163">**Fuseau horaire :** UTC-08</span><span class="sxs-lookup"><span data-stu-id="22e14-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="22e14-164">**Règle de mise à l’échelle automatique (mise à l’échelle supérieure)**</span><span class="sxs-lookup"><span data-stu-id="22e14-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="22e14-165">**Règle de mise à l’échelle automatique (mise à l’échelle supérieure)**</span><span class="sxs-lookup"><span data-stu-id="22e14-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="22e14-166">**Ressource :** Production (environnement App Service)</span><span class="sxs-lookup"><span data-stu-id="22e14-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="22e14-167">**Ressource :** Production (environnement App Service)</span><span class="sxs-lookup"><span data-stu-id="22e14-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="22e14-168">**Mesure :** % d’utilisation de l’unité centrale</span><span class="sxs-lookup"><span data-stu-id="22e14-168">**Metric:** CPU %</span></span> |<span data-ttu-id="22e14-169">**Mesure :** % d’utilisation de l’unité centrale</span><span class="sxs-lookup"><span data-stu-id="22e14-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="22e14-170">**Fonctionnement :** supérieur à 60 %</span><span class="sxs-lookup"><span data-stu-id="22e14-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="22e14-171">**Fonctionnement :** supérieur à 80 %</span><span class="sxs-lookup"><span data-stu-id="22e14-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="22e14-172">**Durée :** 5 minutes</span><span class="sxs-lookup"><span data-stu-id="22e14-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="22e14-173">**Durée :** 10 minutes</span><span class="sxs-lookup"><span data-stu-id="22e14-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="22e14-174">**Agrégation de temps :** moyenne</span><span class="sxs-lookup"><span data-stu-id="22e14-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="22e14-175">**Agrégation de temps :** moyenne</span><span class="sxs-lookup"><span data-stu-id="22e14-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="22e14-176">**Action :** augmenter le nombre de 2</span><span class="sxs-lookup"><span data-stu-id="22e14-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="22e14-177">**Action :** augmenter le nombre de 1</span><span class="sxs-lookup"><span data-stu-id="22e14-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="22e14-178">**Refroidissement (minutes) :** 15</span><span class="sxs-lookup"><span data-stu-id="22e14-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="22e14-179">**Refroidissement (minutes) :** 20</span><span class="sxs-lookup"><span data-stu-id="22e14-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="22e14-180">**Règle de mise à l’échelle automatique (mise à l’échelle inférieure)**</span><span class="sxs-lookup"><span data-stu-id="22e14-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="22e14-181">**Règle de mise à l’échelle automatique (mise à l’échelle inférieure)**</span><span class="sxs-lookup"><span data-stu-id="22e14-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="22e14-182">**Ressource :** Production (environnement App Service)</span><span class="sxs-lookup"><span data-stu-id="22e14-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="22e14-183">**Ressource :** Production (environnement App Service)</span><span class="sxs-lookup"><span data-stu-id="22e14-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="22e14-184">**Mesure :** % d’utilisation de l’unité centrale</span><span class="sxs-lookup"><span data-stu-id="22e14-184">**Metric:** CPU %</span></span> |<span data-ttu-id="22e14-185">**Mesure :** % d’utilisation de l’unité centrale</span><span class="sxs-lookup"><span data-stu-id="22e14-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="22e14-186">**Fonctionnement :** inférieur à 30 %</span><span class="sxs-lookup"><span data-stu-id="22e14-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="22e14-187">**Fonctionnement :** inférieur à 20 %</span><span class="sxs-lookup"><span data-stu-id="22e14-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="22e14-188">**Durée :** 10 minutes</span><span class="sxs-lookup"><span data-stu-id="22e14-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="22e14-189">**Durée :** 15 minutes</span><span class="sxs-lookup"><span data-stu-id="22e14-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="22e14-190">**Agrégation de temps :** moyenne</span><span class="sxs-lookup"><span data-stu-id="22e14-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="22e14-191">**Agrégation de temps :** moyenne</span><span class="sxs-lookup"><span data-stu-id="22e14-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="22e14-192">**Action :** diminuer le nombre de 1</span><span class="sxs-lookup"><span data-stu-id="22e14-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="22e14-193">**Action :** diminuer le nombre de 1</span><span class="sxs-lookup"><span data-stu-id="22e14-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="22e14-194">**Refroidissement (minutes) :** 20</span><span class="sxs-lookup"><span data-stu-id="22e14-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="22e14-195">**Refroidissement (minutes) :** 10</span><span class="sxs-lookup"><span data-stu-id="22e14-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="22e14-196">Taux d’inflation du plan App Service</span><span class="sxs-lookup"><span data-stu-id="22e14-196">App Service plan inflation rate</span></span>
<span data-ttu-id="22e14-197">Les plans App Service sont configurés pour une mise à l’échelle automatique, et fonctionnent ainsi au taux maximal par heure.</span><span class="sxs-lookup"><span data-stu-id="22e14-197">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="22e14-198">Cette vitesse peut être calculée en fonction des valeurs fournies sur la règle de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="22e14-198">This rate can be calculated based on the values provided on the autoscale rule.</span></span>

<span data-ttu-id="22e14-199">La compréhension et le calcul du *taux d’inflation du plan App Service* sont importants pour la mise à l’échelle du pool de Workers de l’environnement App Service, car les modifications d’un pool de Workers ne sont pas instantanées.</span><span class="sxs-lookup"><span data-stu-id="22e14-199">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span></span>

<span data-ttu-id="22e14-200">Le taux d’inflation du plan App Service est calculé comme suit :</span><span class="sxs-lookup"><span data-stu-id="22e14-200">The App Service plan inflation rate is calculated as follows:</span></span>

![Calcul du taux d’inflation du plan App Service.][ASP-Inflation]

<span data-ttu-id="22e14-202">Si l’on prend la règle Mise à l’échelle automatique – Mise à l’échelle supérieure du profil Jour de semaine pour le plan App Service de production :</span><span class="sxs-lookup"><span data-stu-id="22e14-202">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span></span>

![Taux d’inflation du plan App Service pour les jours de la semaine selon la règle Mise à l’échelle automatique – Mise à l’échelle supérieure.][Equation1]

<span data-ttu-id="22e14-204">Dans le cas de la règle Mise à l’échelle automatique – Mise à l’échelle supérieure pour le profil Week-end, la formule du plan App Service de production se présentera ainsi :</span><span class="sxs-lookup"><span data-stu-id="22e14-204">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>

![Taux d’inflation du plan App Service pour les week-ends selon la règle Mise à l’échelle automatique – Mise à l’échelle supérieure.][Equation2]

<span data-ttu-id="22e14-206">Cette valeur peut également être calculée pour les opérations de réduction.</span><span class="sxs-lookup"><span data-stu-id="22e14-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="22e14-207">Selon la règle Mise à l’échelle automatique - Mise à l’échelle inférieure pour le profil Jour de semaine, le plan App Service de production se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="22e14-207">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span></span>

![Taux d’inflation du plan App Service pour les jours de la semaine selon la règle Mise à l’échelle automatique – Mise à l’échelle inférieure.][Equation3]

<span data-ttu-id="22e14-209">Dans le cas de la règle Mise à l’échelle automatique – Mise à l’échelle inférieure pour le profil Week-end, la formule du plan App Service de production se présentera ainsi :</span><span class="sxs-lookup"><span data-stu-id="22e14-209">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>  

![Taux d’inflation du plan App Service pour les week-ends selon la règle Mise à l’échelle automatique – Mise à l’échelle inférieure.][Equation4]

<span data-ttu-id="22e14-211">Le plan App Service de production peut augmenter d’un taux maximal de huit instances/heure durant la semaine et de quatre instances/heure durant le week-end.</span><span class="sxs-lookup"><span data-stu-id="22e14-211">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span></span> <span data-ttu-id="22e14-212">Il peut libérer des instances à un taux maximal de quatre instances/heure durant la semaine et de six instances/heure durant les week-ends.</span><span class="sxs-lookup"><span data-stu-id="22e14-212">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span></span>

<span data-ttu-id="22e14-213">Si plusieurs plans App Service sont hébergés dans un pool de workers, vous devez calculer le *taux total d’inflation* en fonction de la somme du taux d’inflation de tous les plans App Service hébergés dans ce pool de workers.</span><span class="sxs-lookup"><span data-stu-id="22e14-213">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span></span>

![Calcul du taux d’inflation total pour plusieurs plans App Service hébergés dans un pool de workers.][ASP-Total-Inflation]

### <a name="use-the-app-service-plan-inflation-rate-to-define-worker-pool-autoscale-rules"></a><span data-ttu-id="22e14-215">Utilisation du taux d’inflation du plan App Service pour définir des règles de mise à l’échelle automatique du pool de workers</span><span class="sxs-lookup"><span data-stu-id="22e14-215">Use the App Service plan inflation rate to define worker pool autoscale rules</span></span>
<span data-ttu-id="22e14-216">Les pools de workers qui hébergent des plans App Service configurés pour la mise à l’échelle automatique doivent disposer d’une mémoire tampon adaptée.</span><span class="sxs-lookup"><span data-stu-id="22e14-216">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="22e14-217">La mémoire tampon permet aux opérations de mise à l’échelle automatique d’augmenter et de réduire le plan App Service en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="22e14-217">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="22e14-218">La mémoire tampon minimale correspond au taux total d’inflation du plan App Service calculé.</span><span class="sxs-lookup"><span data-stu-id="22e14-218">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="22e14-219">Comme les opérations de mise à l’échelle de l’environnement App Service prennent un certain temps, toute modification doit tenir compte des demandes de modification pouvant se produire lorsqu’une opération de mise à l’échelle est en cours.</span><span class="sxs-lookup"><span data-stu-id="22e14-219">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="22e14-220">Pour ce faire, nous recommandons l’utilisation du taux d’inflation du plan App Service total calculé en tant que nombre minimal d’instances ajoutées pour chaque opération de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="22e14-220">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="22e14-221">Grâce à ces informations, Frank peut définir le profil et les règles de mise à l’échelle automatique suivants :</span><span class="sxs-lookup"><span data-stu-id="22e14-221">With this information, Frank can define the following autoscale profile and rules:</span></span>

![Règles de profil de mise à l’échelle automatique pour un exemple d’application métier.][Worker-Pool-Scale]

| <span data-ttu-id="22e14-223">**Profil de mise à l’échelle automatique – Jours de la semaine**</span><span class="sxs-lookup"><span data-stu-id="22e14-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="22e14-224">**Profil de mise à l’échelle automatique – Week-ends**</span><span class="sxs-lookup"><span data-stu-id="22e14-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="22e14-225">**Nom :** profil jour de semaine</span><span class="sxs-lookup"><span data-stu-id="22e14-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="22e14-226">**Nom :** profil week-end</span><span class="sxs-lookup"><span data-stu-id="22e14-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="22e14-227">**Mise à l’échelle selon :** Planification et règles de performances</span><span class="sxs-lookup"><span data-stu-id="22e14-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="22e14-228">**Mise à l’échelle selon :** Planification et règles de performances</span><span class="sxs-lookup"><span data-stu-id="22e14-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="22e14-229">**Profil :** jours de la semaine</span><span class="sxs-lookup"><span data-stu-id="22e14-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="22e14-230">**Profil :** week-end</span><span class="sxs-lookup"><span data-stu-id="22e14-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="22e14-231">**Type :** périodicité</span><span class="sxs-lookup"><span data-stu-id="22e14-231">**Type:** Recurrence</span></span> |<span data-ttu-id="22e14-232">**Type :** périodicité</span><span class="sxs-lookup"><span data-stu-id="22e14-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="22e14-233">**Plage cible :** 13 à 25 instances</span><span class="sxs-lookup"><span data-stu-id="22e14-233">**Target range:** 13 to 25 instances</span></span> |<span data-ttu-id="22e14-234">**Plage cible :** 6 à 15 instances</span><span class="sxs-lookup"><span data-stu-id="22e14-234">**Target range:** 6 to 15 instances</span></span> |
| <span data-ttu-id="22e14-235">**Jours :** lundi, mardi, mercredi, jeudi, vendredi</span><span class="sxs-lookup"><span data-stu-id="22e14-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="22e14-236">**Jours :** samedi, dimanche</span><span class="sxs-lookup"><span data-stu-id="22e14-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="22e14-237">**Heure de début :** 7 h</span><span class="sxs-lookup"><span data-stu-id="22e14-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="22e14-238">**Heure de début :** 9 h</span><span class="sxs-lookup"><span data-stu-id="22e14-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="22e14-239">**Fuseau horaire :** UTC-08</span><span class="sxs-lookup"><span data-stu-id="22e14-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="22e14-240">**Fuseau horaire :** UTC-08</span><span class="sxs-lookup"><span data-stu-id="22e14-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="22e14-241">**Règle de mise à l’échelle automatique (mise à l’échelle supérieure)**</span><span class="sxs-lookup"><span data-stu-id="22e14-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="22e14-242">**Règle de mise à l’échelle automatique (mise à l’échelle supérieure)**</span><span class="sxs-lookup"><span data-stu-id="22e14-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="22e14-243">**Ressource :** pool de Workers 1</span><span class="sxs-lookup"><span data-stu-id="22e14-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="22e14-244">**Ressource :** pool de Workers 1</span><span class="sxs-lookup"><span data-stu-id="22e14-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="22e14-245">**Mesure :** Employés disponibles</span><span class="sxs-lookup"><span data-stu-id="22e14-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="22e14-246">**Mesure :** Employés disponibles</span><span class="sxs-lookup"><span data-stu-id="22e14-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="22e14-247">**Fonctionnement :** inférieur à 8</span><span class="sxs-lookup"><span data-stu-id="22e14-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="22e14-248">**Fonctionnement :** inférieur à 3</span><span class="sxs-lookup"><span data-stu-id="22e14-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="22e14-249">**Durée :** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="22e14-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="22e14-250">**Durée :** 30 minutes</span><span class="sxs-lookup"><span data-stu-id="22e14-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="22e14-251">**Agrégation de temps :** moyenne</span><span class="sxs-lookup"><span data-stu-id="22e14-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="22e14-252">**Agrégation de temps :** moyenne</span><span class="sxs-lookup"><span data-stu-id="22e14-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="22e14-253">**Action :** augmenter le nombre de 8</span><span class="sxs-lookup"><span data-stu-id="22e14-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="22e14-254">**Action :** augmenter le nombre de 3</span><span class="sxs-lookup"><span data-stu-id="22e14-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="22e14-255">**Refroidissement (minutes) :** 180</span><span class="sxs-lookup"><span data-stu-id="22e14-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="22e14-256">**Refroidissement (minutes) :** 180</span><span class="sxs-lookup"><span data-stu-id="22e14-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="22e14-257">**Règle de mise à l’échelle automatique (mise à l’échelle inférieure)**</span><span class="sxs-lookup"><span data-stu-id="22e14-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="22e14-258">**Règle de mise à l’échelle automatique (mise à l’échelle inférieure)**</span><span class="sxs-lookup"><span data-stu-id="22e14-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="22e14-259">**Ressource :** pool de Workers 1</span><span class="sxs-lookup"><span data-stu-id="22e14-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="22e14-260">**Ressource :** pool de Workers 1</span><span class="sxs-lookup"><span data-stu-id="22e14-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="22e14-261">**Mesure :** Employés disponibles</span><span class="sxs-lookup"><span data-stu-id="22e14-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="22e14-262">**Mesure :** Employés disponibles</span><span class="sxs-lookup"><span data-stu-id="22e14-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="22e14-263">**Fonctionnement :** supérieur à 8</span><span class="sxs-lookup"><span data-stu-id="22e14-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="22e14-264">**Fonctionnement :** supérieur à 3</span><span class="sxs-lookup"><span data-stu-id="22e14-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="22e14-265">**Durée :** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="22e14-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="22e14-266">**Durée :** 15 minutes</span><span class="sxs-lookup"><span data-stu-id="22e14-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="22e14-267">**Agrégation de temps :** moyenne</span><span class="sxs-lookup"><span data-stu-id="22e14-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="22e14-268">**Agrégation de temps :** moyenne</span><span class="sxs-lookup"><span data-stu-id="22e14-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="22e14-269">**Action :** diminuer le nombre de 2</span><span class="sxs-lookup"><span data-stu-id="22e14-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="22e14-270">**Action :** diminuer le nombre de 3</span><span class="sxs-lookup"><span data-stu-id="22e14-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="22e14-271">**Refroidissement (minutes) :** 120</span><span class="sxs-lookup"><span data-stu-id="22e14-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="22e14-272">**Refroidissement (minutes) :** 120</span><span class="sxs-lookup"><span data-stu-id="22e14-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="22e14-273">La plage cible définie dans le profil est calculée par le nombre d’instances minimales du profil pour le plan App Service + la mémoire tampon.</span><span class="sxs-lookup"><span data-stu-id="22e14-273">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span></span>

<span data-ttu-id="22e14-274">La plage maximale est la somme du maximum de toutes les plages pour tous les plans App Service hébergés dans le pool de workers.</span><span class="sxs-lookup"><span data-stu-id="22e14-274">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span></span>

<span data-ttu-id="22e14-275">L’augmentation correspondant aux règles de mise à l’échelle doit être définie comme au moins 1 fois le taux d’inflation du plan App Service pour la mise à l’échelle supérieure.</span><span class="sxs-lookup"><span data-stu-id="22e14-275">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="22e14-276">La réduction correspondant aux règles de mise à l’échelle doit être définie sur un chiffre compris entre 1/2 fois et 1 fois le taux d’inflation du plan App Service pour une mise à l’échelle inférieure.</span><span class="sxs-lookup"><span data-stu-id="22e14-276">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="22e14-277">Mise à l’échelle automatique du pool frontend</span><span class="sxs-lookup"><span data-stu-id="22e14-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="22e14-278">Les règles de mise à l’échelle automatique des frontends sont plus simples que pour les pools de workers.</span><span class="sxs-lookup"><span data-stu-id="22e14-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="22e14-279">Le plus important est de</span><span class="sxs-lookup"><span data-stu-id="22e14-279">Primarily, you should</span></span>  
<span data-ttu-id="22e14-280">vous assurer que la durée de la mesure et des temps de recharge prend en compte le fait que les opérations de mise à l’échelle sur un plan App Service ne sont pas instantanées.</span><span class="sxs-lookup"><span data-stu-id="22e14-280">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="22e14-281">Pour ce scénario, Frank sait que le taux d’erreur augmente après que les frontends ont atteint un taux d’utilisation du processeur de 80 %, et il définit la règle de mise à l’échelle automatique pour augmenter le nombre d’instances comme suit :</span><span class="sxs-lookup"><span data-stu-id="22e14-281">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span></span>

![Paramètres de mise à l’échelle automatique du pool frontend.][Front-End-Scale]

| <span data-ttu-id="22e14-283">**Profil de l’échelle automatique : frontends**</span><span class="sxs-lookup"><span data-stu-id="22e14-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="22e14-284">**Nom :** Mise à l’échelle automatique – Frontends</span><span class="sxs-lookup"><span data-stu-id="22e14-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="22e14-285">**Mise à l’échelle selon :** Planification et règles de performances</span><span class="sxs-lookup"><span data-stu-id="22e14-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="22e14-286">**Profil :** tous les jours</span><span class="sxs-lookup"><span data-stu-id="22e14-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="22e14-287">**Type :** périodicité</span><span class="sxs-lookup"><span data-stu-id="22e14-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="22e14-288">**Plage cible :** 3 à 10 instances</span><span class="sxs-lookup"><span data-stu-id="22e14-288">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="22e14-289">**Jours :** tous les jours</span><span class="sxs-lookup"><span data-stu-id="22e14-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="22e14-290">**Heure de début :** 9 h</span><span class="sxs-lookup"><span data-stu-id="22e14-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="22e14-291">**Fuseau horaire :** UTC-08</span><span class="sxs-lookup"><span data-stu-id="22e14-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="22e14-292">**Règle de mise à l’échelle automatique (mise à l’échelle supérieure)**</span><span class="sxs-lookup"><span data-stu-id="22e14-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="22e14-293">**Ressource :** Pool frontend</span><span class="sxs-lookup"><span data-stu-id="22e14-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="22e14-294">**Mesure :** % d’utilisation de l’unité centrale</span><span class="sxs-lookup"><span data-stu-id="22e14-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="22e14-295">**Fonctionnement :** supérieur à 60 %</span><span class="sxs-lookup"><span data-stu-id="22e14-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="22e14-296">**Durée :** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="22e14-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="22e14-297">**Agrégation de temps :** moyenne</span><span class="sxs-lookup"><span data-stu-id="22e14-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="22e14-298">**Action :** augmenter le nombre de 3</span><span class="sxs-lookup"><span data-stu-id="22e14-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="22e14-299">**Refroidissement (minutes) :** 120</span><span class="sxs-lookup"><span data-stu-id="22e14-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="22e14-300">**Règle de mise à l’échelle automatique (mise à l’échelle inférieure)**</span><span class="sxs-lookup"><span data-stu-id="22e14-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="22e14-301">**Ressource :** pool de Workers 1</span><span class="sxs-lookup"><span data-stu-id="22e14-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="22e14-302">**Mesure :** % d’utilisation de l’unité centrale</span><span class="sxs-lookup"><span data-stu-id="22e14-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="22e14-303">**Fonctionnement :** inférieur à 30 %</span><span class="sxs-lookup"><span data-stu-id="22e14-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="22e14-304">**Durée :** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="22e14-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="22e14-305">**Agrégation de temps :** moyenne</span><span class="sxs-lookup"><span data-stu-id="22e14-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="22e14-306">**Action :** diminuer le nombre de 3</span><span class="sxs-lookup"><span data-stu-id="22e14-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="22e14-307">**Refroidissement (minutes) :** 120</span><span class="sxs-lookup"><span data-stu-id="22e14-307">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
