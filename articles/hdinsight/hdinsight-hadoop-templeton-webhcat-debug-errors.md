---
title: "Comprendre et résoudre des erreurs WebHCat sur HDInsight - Azure | Documents Microsoft"
description: "Découvrez quelles sont les erreurs courantes renvoyées par WebHCat sur HDInsight et comment les résoudre."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 6d8162e0d64ec9fc42690392b7c822593c0c2767
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="58f19-103">Compréhension et résolution des erreurs reçues à partir de WebHCat sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="58f19-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="58f19-104">Découvrez les erreurs reçues lors de l’utilisation de WebHCat avec HDInsight et comment les résoudre.</span><span class="sxs-lookup"><span data-stu-id="58f19-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span></span> <span data-ttu-id="58f19-105">WebHCat est utilisé en interne par les outils côté client tels qu’Azure PowerShell et Data Lake Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58f19-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="58f19-106">Présentation de WebHCat</span><span class="sxs-lookup"><span data-stu-id="58f19-106">What is WebHCat</span></span>

<span data-ttu-id="58f19-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) est une API REST pour [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), une couche de gestion du stockage et des tables pour Hadoop.</span><span class="sxs-lookup"><span data-stu-id="58f19-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="58f19-108">WebHCat est activé par défaut sur les clusters HDInsight et est utilisé par différents outils pour envoyer des tâches, obtenir le statut d’une tâche, etc. sans se connecter au cluster.</span><span class="sxs-lookup"><span data-stu-id="58f19-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="58f19-109">Modification de la configuration</span><span class="sxs-lookup"><span data-stu-id="58f19-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58f19-110">Plusieurs des erreurs répertoriées dans ce document se produisent car une limite maximale configurée a été dépassée.</span><span class="sxs-lookup"><span data-stu-id="58f19-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="58f19-111">Lorsque l’étape de résolution mentionne que vous pouvez modifier une valeur, vous devez utiliser l’une des méthodes suivantes pour effectuer cette modification :</span><span class="sxs-lookup"><span data-stu-id="58f19-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span></span>

* <span data-ttu-id="58f19-112">Pour les clusters **Windows** : utilisez une action de script pour configurer la valeur lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="58f19-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span></span> <span data-ttu-id="58f19-113">Pour en savoir plus, consultez la rubrique [Développement d’actions de script avec HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="58f19-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="58f19-114">Pour les clusters **Linux** : utilisez Ambari (API REST ou web) pour modifier la valeur.</span><span class="sxs-lookup"><span data-stu-id="58f19-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span></span> <span data-ttu-id="58f19-115">Pour en savoir plus, consultez la rubrique [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="58f19-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58f19-116">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="58f19-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="58f19-117">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="58f19-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="58f19-118">Configuration par défaut</span><span class="sxs-lookup"><span data-stu-id="58f19-118">Default configuration</span></span>

<span data-ttu-id="58f19-119">Le dépassement des valeurs par défaut suivantes peut entraîner une baisse des performances de WebHCat ou des erreurs :</span><span class="sxs-lookup"><span data-stu-id="58f19-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="58f19-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="58f19-120">Setting</span></span> | <span data-ttu-id="58f19-121">Résultat</span><span class="sxs-lookup"><span data-stu-id="58f19-121">What it does</span></span> | <span data-ttu-id="58f19-122">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="58f19-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58f19-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="58f19-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="58f19-124">Nombre maximal de tâches pouvant être actives simultanément (en attente ou en cours d’exécution)</span><span class="sxs-lookup"><span data-stu-id="58f19-124">The maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="58f19-125">10 000</span><span class="sxs-lookup"><span data-stu-id="58f19-125">10,000</span></span> |
| <span data-ttu-id="58f19-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="58f19-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="58f19-127">Nombre maximal de demandes pouvant être traitées simultanément</span><span class="sxs-lookup"><span data-stu-id="58f19-127">The maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="58f19-128">20</span><span class="sxs-lookup"><span data-stu-id="58f19-128">20</span></span> |
| <span data-ttu-id="58f19-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="58f19-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="58f19-130">Nombre de jours pendant lesquels l’historique des tâches est conservé.</span><span class="sxs-lookup"><span data-stu-id="58f19-130">The number of days that job history are retained</span></span> |<span data-ttu-id="58f19-131">7 jours</span><span class="sxs-lookup"><span data-stu-id="58f19-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="58f19-132">Trop de demandes</span><span class="sxs-lookup"><span data-stu-id="58f19-132">Too many requests</span></span>

<span data-ttu-id="58f19-133">**Code d’état HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="58f19-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="58f19-134">Cause :</span><span class="sxs-lookup"><span data-stu-id="58f19-134">Cause</span></span> | <span data-ttu-id="58f19-135">Résolution :</span><span class="sxs-lookup"><span data-stu-id="58f19-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="58f19-136">Vous avez dépassé le nombre maximal de demandes simultanées prises en charge par WebHCat par minute (20 par défaut)</span><span class="sxs-lookup"><span data-stu-id="58f19-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="58f19-137">Réduisez votre charge de travail pour vérifier que vous n’avez pas dépassé le nombre maximal de demandes simultanées ou pour augmenter la limite de demandes simultanées en modifiant `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="58f19-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="58f19-138">Pour en savoir plus, consultez la section [Modification de la configuration](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="58f19-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="58f19-139">Serveur non disponible</span><span class="sxs-lookup"><span data-stu-id="58f19-139">Server unavailable</span></span>

<span data-ttu-id="58f19-140">**Code d’état HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="58f19-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="58f19-141">Cause :</span><span class="sxs-lookup"><span data-stu-id="58f19-141">Cause</span></span> | <span data-ttu-id="58f19-142">Résolution :</span><span class="sxs-lookup"><span data-stu-id="58f19-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="58f19-143">Ce code d’état se produit généralement lors du basculement entre le HeadNode principal et secondaire du cluster.</span><span class="sxs-lookup"><span data-stu-id="58f19-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span></span> |<span data-ttu-id="58f19-144">Veuillez patienter deux minutes, puis recommencez l’opération.</span><span class="sxs-lookup"><span data-stu-id="58f19-144">Wait two minutes, then retry the operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="58f19-145">Contenu de demande erroné : impossible de trouver la tâche</span><span class="sxs-lookup"><span data-stu-id="58f19-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="58f19-146">**Code d’état HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="58f19-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="58f19-147">Cause :</span><span class="sxs-lookup"><span data-stu-id="58f19-147">Cause</span></span> | <span data-ttu-id="58f19-148">Résolution :</span><span class="sxs-lookup"><span data-stu-id="58f19-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="58f19-149">Les informations détaillées de la tâche ont été nettoyées par la tâche de nettoyage de l’historique</span><span class="sxs-lookup"><span data-stu-id="58f19-149">Job details have been cleaned up by the job history cleaner</span></span> |<span data-ttu-id="58f19-150">La période de conservation par défaut de l’historique des tâches est de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="58f19-150">The default retention period for job history is 7 days.</span></span> <span data-ttu-id="58f19-151">La période de rétention par défaut peut être changée en modifiant `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="58f19-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="58f19-152">Pour en savoir plus, consultez la section [Modification de la configuration](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="58f19-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="58f19-153">La tâche a été arrêtée en raison d’un basculement</span><span class="sxs-lookup"><span data-stu-id="58f19-153">Job has been killed due to a failover</span></span> |<span data-ttu-id="58f19-154">Veuillez patienter deux minutes avant de renvoyer la tâche</span><span class="sxs-lookup"><span data-stu-id="58f19-154">Retry job submission for up to two minutes</span></span> |
| <span data-ttu-id="58f19-155">L’ID de cette tâche n’est pas valide</span><span class="sxs-lookup"><span data-stu-id="58f19-155">An Invalid job id was used</span></span> |<span data-ttu-id="58f19-156">Veuillez vérifier si l’ID de cette tâche est correct</span><span class="sxs-lookup"><span data-stu-id="58f19-156">Check if the job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="58f19-157">Passerelle incorrecte</span><span class="sxs-lookup"><span data-stu-id="58f19-157">Bad gateway</span></span>

<span data-ttu-id="58f19-158">**Code d’état HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="58f19-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="58f19-159">Cause :</span><span class="sxs-lookup"><span data-stu-id="58f19-159">Cause</span></span> | <span data-ttu-id="58f19-160">Résolution :</span><span class="sxs-lookup"><span data-stu-id="58f19-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="58f19-161">Le nettoyage de la mémoire interne coïncide avec le processus de WebHCat</span><span class="sxs-lookup"><span data-stu-id="58f19-161">Internal garbage collection is occurring within the WebHCat process</span></span> |<span data-ttu-id="58f19-162">Veuillez attendre que le nettoyage de la mémoire se termine ou redémarrez le service WebHCat</span><span class="sxs-lookup"><span data-stu-id="58f19-162">Wait for garbage collection to finish or restart the WebHCat service</span></span> |
| <span data-ttu-id="58f19-163">Le délai d’attente d’une réponse du service ResourceManager a expiré.</span><span class="sxs-lookup"><span data-stu-id="58f19-163">Time out waiting on a response from the ResourceManager service.</span></span> <span data-ttu-id="58f19-164">Cette erreur peut se produire lorsque le nombre d’applications actives dépasse le nombre maximal configuré (10 000 par défaut)</span><span class="sxs-lookup"><span data-stu-id="58f19-164">This error can occur when the number of active applications goes the configured maximum (default 10,000)</span></span> |<span data-ttu-id="58f19-165">Veuillez attendre que les tâches en cours d’exécution se terminent ou augmentez la limite de tâches simultanées en modifiant `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="58f19-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="58f19-166">Pour en savoir plus, consultez la section [Modification de la configuration](#modifying-configuration).</span><span class="sxs-lookup"><span data-stu-id="58f19-166">For more information, see the [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="58f19-167">Tentative de récupération de toutes les tâches par le biais de l’appel [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) lorsque `Fields` est défini sur `*`</span><span class="sxs-lookup"><span data-stu-id="58f19-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span></span> |<span data-ttu-id="58f19-168">Ne récupérez pas *tous* les détails des tâches.</span><span class="sxs-lookup"><span data-stu-id="58f19-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="58f19-169">Utilisez plutôt `jobid` pour récupérer uniquement les détails des tâches dont l’ID est supérieur à un ID de tâche particulier.</span><span class="sxs-lookup"><span data-stu-id="58f19-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id.</span></span> <span data-ttu-id="58f19-170">Ou n’utilisez pas `Fields`</span><span class="sxs-lookup"><span data-stu-id="58f19-170">Or, do not use `Fields`</span></span> |
| <span data-ttu-id="58f19-171">Le service WebHCat est arrêté pendant le basculement du HeadNode</span><span class="sxs-lookup"><span data-stu-id="58f19-171">The WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="58f19-172">Veuillez patienter deux minutes, puis recommencez l’opération</span><span class="sxs-lookup"><span data-stu-id="58f19-172">Wait for two minutes and retry the operation</span></span> |
| <span data-ttu-id="58f19-173">Plus de 500 tâches en attente ont été envoyées via WebHCat</span><span class="sxs-lookup"><span data-stu-id="58f19-173">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="58f19-174">Veuillez patienter le temps que les tâches en attente se terminent avant d’envoyer d’autres tâches</span><span class="sxs-lookup"><span data-stu-id="58f19-174">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
