---
title: "aaaUnderstand et résoudre les erreurs WebHCat sur HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment les erreurs courantes tooabout retourné par WebHCat sur HDInsight et tooresolve les."
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
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="311bd-103">Compréhension et résolution des erreurs reçues à partir de WebHCat sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="311bd-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="311bd-104">En savoir plus sur les erreurs reçues lors de l’utilisation de WebHCat hdinsight et comment tooresolve les.</span><span class="sxs-lookup"><span data-stu-id="311bd-104">Learn about errors received when using WebHCat with HDInsight, and how tooresolve them.</span></span> <span data-ttu-id="311bd-105">WebHCat est utilisée en interne par les outils côté client telles que Azure PowerShell et hello Data Lake Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="311bd-105">WebHCat is used internally by client-side tools such as Azure PowerShell and hello Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="311bd-106">Présentation de WebHCat</span><span class="sxs-lookup"><span data-stu-id="311bd-106">What is WebHCat</span></span>

<span data-ttu-id="311bd-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) est une API REST pour [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), une couche de gestion du stockage et des tables pour Hadoop.</span><span class="sxs-lookup"><span data-stu-id="311bd-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="311bd-108">WebHCat est activé par défaut sur les clusters HDInsight et est utilisé par les travaux de toosubmit différents outils, obtenir l’état du travail, etc. sans session toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="311bd-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools toosubmit jobs, get job status, etc. without logging in toohello cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="311bd-109">Modification de la configuration</span><span class="sxs-lookup"><span data-stu-id="311bd-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="311bd-110">Plusieurs erreurs de hello répertoriées dans ce document se produire si une configuration maximale a été dépassée.</span><span class="sxs-lookup"><span data-stu-id="311bd-110">Several of hello errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="311bd-111">Lors de l’étape de résolution hello mentionne que vous pouvez modifier une valeur, vous devez utiliser une des hello suivant tooperform hello modification :</span><span class="sxs-lookup"><span data-stu-id="311bd-111">When hello resolution step mentions that you can change a value, you must use one of hello following tooperform hello change:</span></span>

* <span data-ttu-id="311bd-112">Pour **Windows** clusters : utilisez une valeur de script action tooconfigure hello lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="311bd-112">For **Windows** clusters: Use a script action tooconfigure hello value during cluster creation.</span></span> <span data-ttu-id="311bd-113">Pour en savoir plus, consultez la rubrique [Développement d’actions de script avec HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="311bd-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="311bd-114">Pour **Linux** clusters : valeur de hello toomodify Ambari d’utilisation (web ou l’API REST).</span><span class="sxs-lookup"><span data-stu-id="311bd-114">For **Linux** clusters: Use Ambari (web or REST API) toomodify hello value.</span></span> <span data-ttu-id="311bd-115">Pour en savoir plus, consultez la rubrique [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="311bd-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="311bd-116">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="311bd-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="311bd-117">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="311bd-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="311bd-118">Configuration par défaut</span><span class="sxs-lookup"><span data-stu-id="311bd-118">Default configuration</span></span>

<span data-ttu-id="311bd-119">Si hello les valeurs par défaut suivantes est dépassé, il peut dégrader les performances de WebHCat ou de provoquer des erreurs :</span><span class="sxs-lookup"><span data-stu-id="311bd-119">If hello following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="311bd-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="311bd-120">Setting</span></span> | <span data-ttu-id="311bd-121">Résultat</span><span class="sxs-lookup"><span data-stu-id="311bd-121">What it does</span></span> | <span data-ttu-id="311bd-122">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="311bd-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="311bd-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="311bd-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="311bd-124">nombre maximal de tâches pouvant être actives simultanément de Hello (en attente ou en cours d’exécution)</span><span class="sxs-lookup"><span data-stu-id="311bd-124">hello maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="311bd-125">10 000</span><span class="sxs-lookup"><span data-stu-id="311bd-125">10,000</span></span> |
| <span data-ttu-id="311bd-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="311bd-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="311bd-127">nombre maximal de Hello de demandes qui peuvent être traités simultanément</span><span class="sxs-lookup"><span data-stu-id="311bd-127">hello maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="311bd-128">20</span><span class="sxs-lookup"><span data-stu-id="311bd-128">20</span></span> |
| <span data-ttu-id="311bd-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="311bd-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="311bd-130">nombre de Hello de jours pendant lesquels l’historique des travaux est conservé.</span><span class="sxs-lookup"><span data-stu-id="311bd-130">hello number of days that job history are retained</span></span> |<span data-ttu-id="311bd-131">7 jours</span><span class="sxs-lookup"><span data-stu-id="311bd-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="311bd-132">Trop de demandes</span><span class="sxs-lookup"><span data-stu-id="311bd-132">Too many requests</span></span>

<span data-ttu-id="311bd-133">**Code d’état HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="311bd-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="311bd-134">Cause :</span><span class="sxs-lookup"><span data-stu-id="311bd-134">Cause</span></span> | <span data-ttu-id="311bd-135">Résolution :</span><span class="sxs-lookup"><span data-stu-id="311bd-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="311bd-136">Vous avez dépassé les requêtes simultanées maximales hello pris en charge par WebHCat par minute (valeur par défaut 20)</span><span class="sxs-lookup"><span data-stu-id="311bd-136">You have exceeded hello maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="311bd-137">Réduire votre tooensure de charge de travail que vous ne pas envoyer plus de hello nombre maximal de demandes simultanées ou augmenter la limite de demandes simultanées hello en modifiant `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="311bd-137">Reduce your workload tooensure that you do not submit more than hello maximum number of concurrent requests or increase hello concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="311bd-138">Pour en savoir plus, consultez la section [Modification de la configuration](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="311bd-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="311bd-139">Serveur non disponible</span><span class="sxs-lookup"><span data-stu-id="311bd-139">Server unavailable</span></span>

<span data-ttu-id="311bd-140">**Code d’état HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="311bd-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="311bd-141">Cause :</span><span class="sxs-lookup"><span data-stu-id="311bd-141">Cause</span></span> | <span data-ttu-id="311bd-142">Résolution :</span><span class="sxs-lookup"><span data-stu-id="311bd-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="311bd-143">Ce code d’état se produit généralement lors du basculement entre hello principaux et secondaires nœud principal de cluster de hello</span><span class="sxs-lookup"><span data-stu-id="311bd-143">This status code usually occurs during failover between hello primary and secondary HeadNode for hello cluster</span></span> |<span data-ttu-id="311bd-144">Patientez deux minutes, puis recommencez l’opération de hello</span><span class="sxs-lookup"><span data-stu-id="311bd-144">Wait two minutes, then retry hello operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="311bd-145">Contenu de demande erroné : impossible de trouver la tâche</span><span class="sxs-lookup"><span data-stu-id="311bd-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="311bd-146">**Code d’état HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="311bd-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="311bd-147">Cause :</span><span class="sxs-lookup"><span data-stu-id="311bd-147">Cause</span></span> | <span data-ttu-id="311bd-148">Résolution :</span><span class="sxs-lookup"><span data-stu-id="311bd-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="311bd-149">Détails de la tâche ont été nettoyés par l’historique des travaux hello nettoyeur</span><span class="sxs-lookup"><span data-stu-id="311bd-149">Job details have been cleaned up by hello job history cleaner</span></span> |<span data-ttu-id="311bd-150">période de rétention par défaut Hello pour l’historique des travaux est de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="311bd-150">hello default retention period for job history is 7 days.</span></span> <span data-ttu-id="311bd-151">période de rétention par défaut Hello peut être changée en modifiant `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="311bd-151">hello default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="311bd-152">Pour en savoir plus, consultez la section [Modification de la configuration](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="311bd-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="311bd-153">Tâche qui a été supprimée en raison du basculement de tooa</span><span class="sxs-lookup"><span data-stu-id="311bd-153">Job has been killed due tooa failover</span></span> |<span data-ttu-id="311bd-154">Réessayer la soumission de travaux pour les tootwo minutes</span><span class="sxs-lookup"><span data-stu-id="311bd-154">Retry job submission for up tootwo minutes</span></span> |
| <span data-ttu-id="311bd-155">L’ID de cette tâche n’est pas valide</span><span class="sxs-lookup"><span data-stu-id="311bd-155">An Invalid job id was used</span></span> |<span data-ttu-id="311bd-156">Vérifiez si l’id de tâche hello est correct</span><span class="sxs-lookup"><span data-stu-id="311bd-156">Check if hello job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="311bd-157">Passerelle incorrecte</span><span class="sxs-lookup"><span data-stu-id="311bd-157">Bad gateway</span></span>

<span data-ttu-id="311bd-158">**Code d’état HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="311bd-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="311bd-159">Cause :</span><span class="sxs-lookup"><span data-stu-id="311bd-159">Cause</span></span> | <span data-ttu-id="311bd-160">Résolution :</span><span class="sxs-lookup"><span data-stu-id="311bd-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="311bd-161">Nettoyage de la mémoire interne se produit dans hello WebHCat processus</span><span class="sxs-lookup"><span data-stu-id="311bd-161">Internal garbage collection is occurring within hello WebHCat process</span></span> |<span data-ttu-id="311bd-162">Attendez que le garbage collection toofinish ou redémarrez le service WebHCat de hello</span><span class="sxs-lookup"><span data-stu-id="311bd-162">Wait for garbage collection toofinish or restart hello WebHCat service</span></span> |
| <span data-ttu-id="311bd-163">Délai d’attente en attente sur une réponse de hello ResourceManager service.</span><span class="sxs-lookup"><span data-stu-id="311bd-163">Time out waiting on a response from hello ResourceManager service.</span></span> <span data-ttu-id="311bd-164">Cette erreur peut se produire lorsque plusieurs hello applications actives devient maximum de hello configuré (par défaut 10 000)</span><span class="sxs-lookup"><span data-stu-id="311bd-164">This error can occur when hello number of active applications goes hello configured maximum (default 10,000)</span></span> |<span data-ttu-id="311bd-165">Attendez que toocomplete de travaux en cours d’exécution ou augmenter la limite de travaux simultanés hello en modifiant `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="311bd-165">Wait for currently running jobs toocomplete or increase hello concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="311bd-166">Pour plus d’informations, consultez hello [modification configuration](#modifying-configuration) section.</span><span class="sxs-lookup"><span data-stu-id="311bd-166">For more information, see hello [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="311bd-167">Tentative de toutes les tâches via hello tooretrieve [/Jobs GET](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) appel alors `Fields` est défini trop`*`</span><span class="sxs-lookup"><span data-stu-id="311bd-167">Attempting tooretrieve all jobs through hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set too`*`</span></span> |<span data-ttu-id="311bd-168">Ne récupérez pas *tous* les détails des tâches.</span><span class="sxs-lookup"><span data-stu-id="311bd-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="311bd-169">Utilisez à la place `jobid` tooretrieve les détails des tâches supérieurs uniquement à certain id de tâche. Ou n’utilisez pas `Fields`</span><span class="sxs-lookup"><span data-stu-id="311bd-169">Instead use `jobid` tooretrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="311bd-170">Hello service WebHCat est arrêté pendant le basculement de nœud principal</span><span class="sxs-lookup"><span data-stu-id="311bd-170">hello WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="311bd-171">Patientez deux minutes et recommencez l’opération de hello</span><span class="sxs-lookup"><span data-stu-id="311bd-171">Wait for two minutes and retry hello operation</span></span> |
| <span data-ttu-id="311bd-172">Plus de 500 tâches en attente ont été envoyées via WebHCat</span><span class="sxs-lookup"><span data-stu-id="311bd-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="311bd-173">Veuillez patienter le temps que les tâches en attente se terminent avant d’envoyer d’autres tâches</span><span class="sxs-lookup"><span data-stu-id="311bd-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
