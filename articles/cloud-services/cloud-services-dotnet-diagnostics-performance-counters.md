---
title: Utiliser les compteurs de performances dans Azure Diagnostics | Microsoft Docs
description: "Les compteurs de performance dans les services ou les machines virtuelles de cloud Azure permettent de trouver les goulots d’étranglement et d’ajuster les performances."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: 2cf765cb034725199127c547a9b8b997a4a6089c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="fe1f4-103">Créer et utiliser des compteurs de performances dans une application Azure</span><span class="sxs-lookup"><span data-stu-id="fe1f4-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="fe1f4-104">Cet article décrit les avantages et la façon de placer des compteurs de performance dans votre application Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-104">This article describes the benefits of and how to put performance counters into your Azure application.</span></span> <span data-ttu-id="fe1f4-105">Vous pouvez les utiliser pour collecter des données, détecter les goulots d’étranglement et régler les performances système et des applications.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-105">You can use them to collect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="fe1f4-106">Les compteurs de performances disponibles pour Windows Server, IIS et ASP.NET peuvent être recueillis et utilisés pour déterminer l’état de vos rôles Azure web, worker et machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used to determine the health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="fe1f4-107">Vous pouvez également créer et utiliser des compteurs de performance personnalisés.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="fe1f4-108">Vous pouvez examiner les données du compteur de performances</span><span class="sxs-lookup"><span data-stu-id="fe1f4-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="fe1f4-109">Directement sur l’hôte d’application avec l’outil d’analyse des performances auquel on accède à l’aide de Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="fe1f4-109">Directly on the application host with the Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="fe1f4-110">Avec System Center Operations Manager en utilisant le Pack d’administration Azure</span><span class="sxs-lookup"><span data-stu-id="fe1f4-110">With System Center Operations Manager using the Azure Management Pack</span></span>
3. <span data-ttu-id="fe1f4-111">Avec d’autres outils d’analyse ayant accès aux données de diagnostic transférées vers le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-111">With other monitoring tools that access the diagnostic data transferred to Azure storage.</span></span> <span data-ttu-id="fe1f4-112">Voir [Stocker et afficher des données de diagnostic dans Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="fe1f4-113">Pour plus d’informations sur la configuration des performances de votre application dans le [portail Azure](http://portal.azure.com/), consultez la page [Surveillance des services cloud](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="fe1f4-113">For more information on monitoring the performance of your application in the [Azure portal](http://portal.azure.com/), see [How to Monitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="fe1f4-114">Pour obtenir d'autres instructions détaillées sur la création d'une stratégie de journalisation et de suivi, et sur l'utilisation des diagnostics et des autres techniques pour résoudre les problèmes et optimiser les applications Azure, consultez la page [Meilleures pratiques de dépannage pour développer des applications Azure](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe1f4-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques to troubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="fe1f4-115">Activer la surveillance du compteur de performance</span><span class="sxs-lookup"><span data-stu-id="fe1f4-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="fe1f4-116">Les compteurs de performance ne sont pas activés par défaut.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="fe1f4-117">Votre application ou une tâche de démarrage doit modifier la configuration de l’agent de diagnostics par défaut pour y inclure les compteurs de performances spécifiques que vous souhaitez surveiller pour chaque instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-117">Your application or a startup task must modify the default diagnostics agent configuration to include the specific performance counters that you wish to monitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="fe1f4-118">Compteurs de performances disponibles pour Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fe1f4-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="fe1f4-119">Azure fournit un sous-ensemble des compteurs de performances disponibles pour Windows Server, IIS et la pile ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-119">Azure provides a subset of the performance counters available for Windows Server, IIS and the ASP.NET stack.</span></span> <span data-ttu-id="fe1f4-120">Le tableau suivant répertorie certains des compteurs de performance présentant un intérêt particulier pour les applications Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-120">The following table lists some of the performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="fe1f4-121">Catégorie de compteur : Objet (Instance)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="fe1f4-122">Nom de compteur</span><span class="sxs-lookup"><span data-stu-id="fe1f4-122">Counter Name</span></span> | <span data-ttu-id="fe1f4-123">Référence</span><span class="sxs-lookup"><span data-stu-id="fe1f4-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fe1f4-124">Exceptions CLR .NET (*Global*)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="fe1f4-125">Nombre d’exceptions levées/s</span><span class="sxs-lookup"><span data-stu-id="fe1f4-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="fe1f4-126">Compteurs de performance des exceptions</span><span class="sxs-lookup"><span data-stu-id="fe1f4-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="fe1f4-127">Mémoire CLR .NET (*Global*)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="fe1f4-128">% de temps dans GC</span><span class="sxs-lookup"><span data-stu-id="fe1f4-128">% Time in GC</span></span> |<span data-ttu-id="fe1f4-129">Compteurs de performance mémoire</span><span class="sxs-lookup"><span data-stu-id="fe1f4-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="fe1f4-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-130">ASP.NET</span></span> |<span data-ttu-id="fe1f4-131">L’application redémarre</span><span class="sxs-lookup"><span data-stu-id="fe1f4-131">Application Restarts</span></span> |<span data-ttu-id="fe1f4-132">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-133">ASP.NET</span></span> |<span data-ttu-id="fe1f4-134">Durée d’exécution de la demande</span><span class="sxs-lookup"><span data-stu-id="fe1f4-134">Request Execution Time</span></span> |<span data-ttu-id="fe1f4-135">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-136">ASP.NET</span></span> |<span data-ttu-id="fe1f4-137">Requêtes déconnectées</span><span class="sxs-lookup"><span data-stu-id="fe1f4-137">Requests Disconnected</span></span> |<span data-ttu-id="fe1f4-138">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-139">ASP.NET</span></span> |<span data-ttu-id="fe1f4-140">Redémarrage du processus Worker</span><span class="sxs-lookup"><span data-stu-id="fe1f4-140">Worker Process Restarts</span></span> |<span data-ttu-id="fe1f4-141">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-142">Applications ASP.NET (**Total**)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="fe1f4-143">Nombre Total de demandes</span><span class="sxs-lookup"><span data-stu-id="fe1f4-143">Requests Total</span></span> |<span data-ttu-id="fe1f4-144">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-145">Applications ASP.NET (**Total**)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="fe1f4-146">Demandes/s</span><span class="sxs-lookup"><span data-stu-id="fe1f4-146">Requests/Sec</span></span> |<span data-ttu-id="fe1f4-147">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="fe1f4-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="fe1f4-149">Durée d’exécution de la demande</span><span class="sxs-lookup"><span data-stu-id="fe1f4-149">Request Execution Time</span></span> |<span data-ttu-id="fe1f4-150">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="fe1f4-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="fe1f4-152">Délai d’attente de demande</span><span class="sxs-lookup"><span data-stu-id="fe1f4-152">Request Wait Time</span></span> |<span data-ttu-id="fe1f4-153">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="fe1f4-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="fe1f4-155">Demandes actuelles</span><span class="sxs-lookup"><span data-stu-id="fe1f4-155">Requests Current</span></span> |<span data-ttu-id="fe1f4-156">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="fe1f4-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="fe1f4-158">Demandes en file d’attente</span><span class="sxs-lookup"><span data-stu-id="fe1f4-158">Requests Queued</span></span> |<span data-ttu-id="fe1f4-159">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="fe1f4-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="fe1f4-161">Demandes rejetées</span><span class="sxs-lookup"><span data-stu-id="fe1f4-161">Requests Rejected</span></span> |<span data-ttu-id="fe1f4-162">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-163">Mémoire</span><span class="sxs-lookup"><span data-stu-id="fe1f4-163">Memory</span></span> |<span data-ttu-id="fe1f4-164">Nombre d’octets disponibles</span><span class="sxs-lookup"><span data-stu-id="fe1f4-164">Available MBytes</span></span> |<span data-ttu-id="fe1f4-165">Compteurs de performance mémoire</span><span class="sxs-lookup"><span data-stu-id="fe1f4-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="fe1f4-166">Mémoire</span><span class="sxs-lookup"><span data-stu-id="fe1f4-166">Memory</span></span> |<span data-ttu-id="fe1f4-167">Octets dédiés</span><span class="sxs-lookup"><span data-stu-id="fe1f4-167">Committed Bytes</span></span> |<span data-ttu-id="fe1f4-168">Compteurs de performance mémoire</span><span class="sxs-lookup"><span data-stu-id="fe1f4-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="fe1f4-169">Processor(_Total)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-169">Processor(_Total)</span></span> |<span data-ttu-id="fe1f4-170">% temps processeur</span><span class="sxs-lookup"><span data-stu-id="fe1f4-170">% Processor Time</span></span> |<span data-ttu-id="fe1f4-171">Compteurs de performances pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fe1f4-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fe1f4-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="fe1f4-172">TCPv4</span></span> |<span data-ttu-id="fe1f4-173">Échecs de connexion</span><span class="sxs-lookup"><span data-stu-id="fe1f4-173">Connection Failures</span></span> |<span data-ttu-id="fe1f4-174">Objet TCP</span><span class="sxs-lookup"><span data-stu-id="fe1f4-174">TCP Object</span></span> |
| <span data-ttu-id="fe1f4-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="fe1f4-175">TCPv4</span></span> |<span data-ttu-id="fe1f4-176">Connexions établies</span><span class="sxs-lookup"><span data-stu-id="fe1f4-176">Connections Established</span></span> |<span data-ttu-id="fe1f4-177">Objet TCP</span><span class="sxs-lookup"><span data-stu-id="fe1f4-177">TCP Object</span></span> |
| <span data-ttu-id="fe1f4-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="fe1f4-178">TCPv4</span></span> |<span data-ttu-id="fe1f4-179">Connexions réinitialisées</span><span class="sxs-lookup"><span data-stu-id="fe1f4-179">Connections Reset</span></span> |<span data-ttu-id="fe1f4-180">Objet TCP</span><span class="sxs-lookup"><span data-stu-id="fe1f4-180">TCP Object</span></span> |
| <span data-ttu-id="fe1f4-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="fe1f4-181">TCPv4</span></span> |<span data-ttu-id="fe1f4-182">Segments envoyés/s</span><span class="sxs-lookup"><span data-stu-id="fe1f4-182">Segments Sent/sec</span></span> |<span data-ttu-id="fe1f4-183">Objet TCP</span><span class="sxs-lookup"><span data-stu-id="fe1f4-183">TCP Object</span></span> |
| <span data-ttu-id="fe1f4-184">Interface réseau(*)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-184">Network Interface(*)</span></span> |<span data-ttu-id="fe1f4-185">Octets reçus/s</span><span class="sxs-lookup"><span data-stu-id="fe1f4-185">Bytes Received/sec</span></span> |<span data-ttu-id="fe1f4-186">Objet d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="fe1f4-186">Network Interface Object</span></span> |
| <span data-ttu-id="fe1f4-187">Interface réseau(*)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-187">Network Interface(*)</span></span> |<span data-ttu-id="fe1f4-188">Octets envoyés/s</span><span class="sxs-lookup"><span data-stu-id="fe1f4-188">Bytes Sent/sec</span></span> |<span data-ttu-id="fe1f4-189">Objet d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="fe1f4-189">Network Interface Object</span></span> |
| <span data-ttu-id="fe1f4-190">Interface réseau(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="fe1f4-191">Octets reçus/s</span><span class="sxs-lookup"><span data-stu-id="fe1f4-191">Bytes Received/sec</span></span> |<span data-ttu-id="fe1f4-192">Objet d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="fe1f4-192">Network Interface Object</span></span> |
| <span data-ttu-id="fe1f4-193">Interface réseau(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="fe1f4-194">Octets envoyés/s</span><span class="sxs-lookup"><span data-stu-id="fe1f4-194">Bytes Sent/sec</span></span> |<span data-ttu-id="fe1f4-195">Objet d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="fe1f4-195">Network Interface Object</span></span> |
| <span data-ttu-id="fe1f4-196">Interface réseau(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="fe1f4-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="fe1f4-197">Nombre total d’octets/s</span><span class="sxs-lookup"><span data-stu-id="fe1f4-197">Bytes Total/sec</span></span> |<span data-ttu-id="fe1f4-198">Objet d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="fe1f4-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-to-your-application"></a><span data-ttu-id="fe1f4-199">Créer et ajouter des compteurs de performance personnalisés à votre application</span><span class="sxs-lookup"><span data-stu-id="fe1f4-199">Create and add custom performance counters to your application</span></span>
<span data-ttu-id="fe1f4-200">Azure assure la prise en charge pour créer et modifier des compteurs de performance personnalisés pour les rôles web et worker.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-200">Azure has support to create and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="fe1f4-201">Les compteurs peuvent être utilisés pour suivre et surveiller le comportement spécifique à l’application.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-201">The counters may be used to track and monitor application-specific behavior.</span></span> <span data-ttu-id="fe1f4-202">Vous pouvez créer et supprimer des catégories de compteurs de performance personnalisés et spécificateurs depuis une tâche de démarrage, un rôle web ou un rôle de travail avec des autorisations de niveau élevé.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="fe1f4-203">Les codes qui modifient des compteurs de performance personnalisés doivent avoir des autorisations élevées pour s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-203">Code that makes changes to custom performance counters must have elevated permissions to run.</span></span> <span data-ttu-id="fe1f4-204">Si le code est dans un rôle web ou un rôle de travail, le rôle doit inclure la balise <Runtime executionContext="elevated" /> dans le fichier ServiceDefinition.csdef pour que le rôle s’initialise correctement.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-204">If the code is in a web role or worker role, the role must include the tag <Runtime executionContext="elevated" /> in the ServiceDefinition.csdef file for the role to initialize properly.</span></span>
>
>

<span data-ttu-id="fe1f4-205">Vous pouvez envoyer des données de compteurs de performance personnalisés vers le stockage Azure grâce à l’agent de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-205">You can send custom performance counter data to Azure storage using the diagnostics agent.</span></span>

<span data-ttu-id="fe1f4-206">Les données de compteur de performance standard sont générées par les processus Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-206">The standard performance counter data is generated by the Azure processes.</span></span> <span data-ttu-id="fe1f4-207">Les données du compteur de performance personnalisé doivent être créées par votre rôle web ou votre application de travail.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="fe1f4-208">Voir [Types de compteurs de performance](https://msdn.microsoft.com/library/z573042h.aspx) pour plus d’informations sur les types de données pouvant être stockées dans des compteurs de performance personnalisés.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on the types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="fe1f4-209">Voir [Exemple de compteurs de performance](http://code.msdn.microsoft.com/azure/) pour obtenir un exemple créant et définissant les données de compteurs de performance personnalisés dans un rôle web.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="fe1f4-210">Stockez et affichez les données de compteur de performance</span><span class="sxs-lookup"><span data-stu-id="fe1f4-210">Store and view performance counter data</span></span>
<span data-ttu-id="fe1f4-211">Azure met en mémoire cache les données de compteur de performance avec d’autres informations de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="fe1f4-212">Ces données sont disponibles pour la surveillance à distance pendant l’exécution de l’instance de rôle à l’aide d’un accès du Bureau à distance pour afficher les outils de l’Analyseur de performances.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-212">This data is available for remote monitoring while the role instance is running using remote desktop access to view tools such as Performance Monitor.</span></span> <span data-ttu-id="fe1f4-213">Pour conserver les données en dehors de l’instance de rôle, l’agent de diagnostic doit transférer les données vers le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-213">To persist the data outside of the role instance, the diagnostics agent must transfer the data to Azure storage.</span></span> <span data-ttu-id="fe1f4-214">La limite de taille des données du compteur de performances mises en cache peut être configurée dans l’agent de diagnostics, ou il peut être configuré pour faire partie d’une limite partagée pour toutes les données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-214">The size limit of the cached performance counter data can be configured in the diagnostics agent, or it may be configured to be part of a shared limit for all the diagnostic data.</span></span> <span data-ttu-id="fe1f4-215">Pour plus d’informations sur la définition de la taille de la mémoire tampon, consultez [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) et [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe1f4-215">For more information about setting the buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="fe1f4-216">Voir [Stocker et afficher les données de diagnostic dans Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) pour une vue d’ensemble de la configuration de l’agent de diagnostic pour transférer des données vers un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up the diagnostics agent to transfer data to a storage account.</span></span>

<span data-ttu-id="fe1f4-217">Chaque instance de compteur de performance configurée est enregistrée à un taux d’échantillonnage spécifié et les données échantillonnées sont transférées au compte de stockage par demande de transfert planifiée ou demande de transfert à la demande.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-217">Each configured performance counter instance is recorded at a specified sampling rate, and the sampled data is transferred to the storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="fe1f4-218">Les transferts automatiques peuvent être planifiés au maximum une fois par minute.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="fe1f4-219">Les données de compteur de performance transférées par l’agent de diagnostics sont stockées dans un tableau, WADPerformanceCountersTable, dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-219">Performance counter data transferred by the diagnostics agent is stored in a table, WADPerformanceCountersTable, in the storage account.</span></span> <span data-ttu-id="fe1f4-220">Cette table peut-être accessible et interrogée avec les méthodes de l’API standard de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="fe1f4-221">Voir [Exemple de compteur de performance Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) pour obtenir un exemple d’interrogation et d’affichage des données de compteur de performances du tableau WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from the WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="fe1f4-222">Selon la fréquence de transfert de l’agent de diagnostics et de la latence de la file d’attente, les données de compteur de performance les plus récentes du compte de stockage peuvent être obsolètes pendant plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-222">Depending on the diagnostics agent transfer frequency and queue latency, the most recent performance counter data in the storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="fe1f4-223">Activer les compteurs de performance à l’aide du fichier de configuration de diagnostics</span><span class="sxs-lookup"><span data-stu-id="fe1f4-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="fe1f4-224">Utilisez la procédure suivante pour activer les compteurs de performances dans votre application Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-224">Use the following procedure to enable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe1f4-225">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="fe1f4-225">Prerequisites</span></span>
<span data-ttu-id="fe1f4-226">Cette section part du principe que vous avez importé le moniteur de diagnostics dans votre application et que vous avez ajouté le fichier de configuration de diagnostic à votre solution Visual Studio (diagnostics.wadcfg dans le kit de développement logiciel 2.4 et version antérieure ou diagnostics.wadcfgx dans le kit de développement logiciel 2.5 et ultérieur).</span><span class="sxs-lookup"><span data-stu-id="fe1f4-226">This section assumes that you have imported the Diagnostics monitor into your application and added the diagnostics configuration file to your Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="fe1f4-227">Voir les étapes 1 et 2 dans [Activation de Diagnostics dans Azure Cloud Services et Virtual Machines](cloud-services-dotnet-diagnostics.md)pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="fe1f4-228">Étape 1 : collecte et stockage de données de compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="fe1f4-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="fe1f4-229">Après avoir ajouté le fichier diagnostics à votre solution Visual Studio, vous pouvez configurer la collecte et le stockage de données de compteurs de performances dans une application Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-229">After you have added the diagnostics file to your Visual Studio solution, you can configure the collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="fe1f4-230">Pour cela, vous devez ajouter des compteurs de performances au fichier diagnostics.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-230">This is done by adding performance counters to the diagnostics file.</span></span> <span data-ttu-id="fe1f4-231">Dans un premier temps, les données de diagnostic, y compris les compteurs de performances, sont collectées au niveau de l'instance.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-231">Diagnostics data, including performance counters, is first collected on the instance.</span></span> <span data-ttu-id="fe1f4-232">Sachant que les données sont conservées dans la table WADPerformanceCountersTable du service de Table Azure, vous serez également amené à spécifier le compte de stockage dans votre application.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-232">The data is then persisted to the WADPerformanceCountersTable table in the Azure Table service, so you will also need to specify the storage account in your application.</span></span> <span data-ttu-id="fe1f4-233">Si vous testez votre application en local dans l'émulateur de calcul, vous pouvez également stocker les données de diagnostic en local dans l'émulateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-233">If you're testing your application locally in the Compute Emulator, you can also store diagnostics data locally in the Storage Emulator.</span></span> <span data-ttu-id="fe1f4-234">Avant de stocker les données de diagnostic, vous devez accéder au [portail Azure](http://portal.azure.com/) et créer un compte de stockage classique.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-234">Before you store diagnostics data, you must first go to the [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="fe1f4-235">La meilleure pratique consiste à placer votre compte de stockage au même emplacement géographique que votre application Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-235">A best practice is to locate your storage account in the same geo-location as your Azure application.</span></span> <span data-ttu-id="fe1f4-236">En conservant l’application Windows Azure et votre compte de stockage dans le même emplacement géographique, vous évitez les coûts de bande passante externes et réduisez la latence.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-236">By keeping the Azure application and storage account are in the same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-to-the-diagnostics-file"></a><span data-ttu-id="fe1f4-237">Ajouter des compteurs de performances au fichier de diagnostics</span><span class="sxs-lookup"><span data-stu-id="fe1f4-237">Add performance counters to the diagnostics file</span></span>
<span data-ttu-id="fe1f4-238">Il existe de nombreux compteurs que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-238">There are many counters you can use.</span></span> <span data-ttu-id="fe1f4-239">L’exemple suivant montre plusieurs compteurs de performances qui sont recommandés pour la surveillance des rôles web et worker.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-239">The following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="fe1f4-240">Ouvrez le fichier de diagnostics (diagnostics.wadcfg dans le Kit de développement logiciel 2.4 et antérieur ou diagnostics.wadcfgx dans le kit de développement logiciel 2.5 et versions ultérieures) et ajoutez le code suivant à l’élément DiagnosticMonitorConfiguration :</span><span class="sxs-lookup"><span data-stu-id="fe1f4-240">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use the Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use the Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="fe1f4-241">L'attribut bufferQuotaInMB spécifie la capacité maximale de stockage du système du fichiers disponible pour le type de collecte de données (journaux Azure, journaux IIS, etc.).</span><span class="sxs-lookup"><span data-stu-id="fe1f4-241">The bufferQuotaInMB attribute, which specifies the maximum amount of file system storage that is available for the data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="fe1f4-242">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-242">The default is 0.</span></span> <span data-ttu-id="fe1f4-243">Lorsque le quota est atteint, les données les plus anciennes sont supprimées à mesure que de nouvelles données sont ajoutées.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-243">When the quota is reached, the oldest data is deleted as new data is added.</span></span> <span data-ttu-id="fe1f4-244">La somme de toutes les propriétés bufferQuotaInMB doit être supérieure à la valeur de l'attribut OverallQuotaInMB.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-244">The sum of all the bufferQuotaInMB properties must be greater than the value of the OverallQuotaInMB attribute.</span></span> <span data-ttu-id="fe1f4-245">Pour plus d'informations sur la façon de déterminer la quantité de stockage nécessaire à la collecte de données de diagnostic, consultez la section Configuration de WAD de la page [Meilleures pratiques de dépannage pour développer des applications Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe1f4-245">For a more detailed discussion of determining how much storage will be required for the collection of diagnostics data, see the Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="fe1f4-246">L'attribut scheduledTransferPeriod spécifie le délai entre les transferts de données planifiés, arrondi à la minute supérieure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-246">The scheduledTransferPeriod attribute, which specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span> <span data-ttu-id="fe1f4-247">Dans les exemples suivants, il est défini à PT30M (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="fe1f4-247">In the following examples, it is set to PT30M (30 minutes).</span></span> <span data-ttu-id="fe1f4-248">Si la définition d'une période de transfert plus courte, par exemple 1 minute, peut avoir des conséquences néfastes sur les performances de l'application en production, cela peut s'avérer utile en phase de test pour obtenir des diagnostics rapides.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-248">Setting the transfer period to a small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="fe1f4-249">La période de transfert planifiée doit être suffisamment courte pour éviter que les données de diagnostic soient remplacées au niveau de l'instance, mais suffisamment longue pour qu'elle n'ait pas d'incidence sur les performances de votre application.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-249">The scheduled transfer period should be small enough to ensure that diagnostic data is not overwritten on the instance, but large enough that it will not impact the performance of your application.</span></span>

<span data-ttu-id="fe1f4-250">L’attribut counterSpecifier spécifie le compteur de performances à relever.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-250">The counterSpecifier attribute specifies the performance counter to collect.</span></span> <span data-ttu-id="fe1f4-251">L’attribut sampleRate spécifie le taux auquel le compteur de performance est échantillonné, dans ce cas, 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-251">The sampleRate attribute specifies the rate at which the performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="fe1f4-252">Une fois que vous avez ajouté les compteurs de performances à collecter, enregistrez vos modifications dans le fichier diagnostics.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-252">Once you've added the performance counters that you want to collect, save your changes to the diagnostics file.</span></span> <span data-ttu-id="fe1f4-253">Ensuite, vous devez spécifier le compte de stockage dans lequel les données de diagnostic seront conservées.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-253">Next, you need to specify the storage account that the diagnostics data will be persisted to.</span></span>

### <a name="specify-the-storage-account"></a><span data-ttu-id="fe1f4-254">Spécification du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="fe1f4-254">Specify the storage account</span></span>
<span data-ttu-id="fe1f4-255">Pour conserver vos informations de diagnostic dans votre compte Azure Storage, vous devez spécifier une chaîne de connexion dans le fichier de configuration (ServiceConfiguration.cscfg) de votre service.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-255">To persist your diagnostics information to your Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="fe1f4-256">Dans le kit de développement logiciel (SDK) Azure 2.5, le compte de stockage peut être spécifié dans le fichier diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-256">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="fe1f4-257">Ces instructions s’appliquent uniquement au kit de développement logiciel Azure 2.4 et versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-257">These instructions only apply to Azure SDK 2.4 and below.</span></span> <span data-ttu-id="fe1f4-258">Dans le kit de développement logiciel (SDK) Azure 2.5, le compte de stockage peut être spécifié dans le fichier diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-258">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="fe1f4-259">Pour définir les chaînes de connexion :</span><span class="sxs-lookup"><span data-stu-id="fe1f4-259">To set the connection strings:</span></span>

1. <span data-ttu-id="fe1f4-260">Ouvrez le fichier ServiceConfiguration.Cloud.cscfg à l’aide de l’éditeur de texte de votre choix, puis définissez la chaîne de connexion de votre stockage.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-260">Open the ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set the connection string for your storage.</span></span> <span data-ttu-id="fe1f4-261">Les valeurs *AccountName* et *AccountKey* figurent dans le portail Azure, sur le tableau de bord du compte de stockage, sous Clés d’accès.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-261">The *AccountName* and *AccountKey* values are found in the Azure portal in the storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="fe1f4-262">Enregistrez le fichier ServiceConfiguration.Cloud.cscfg.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-262">Save the ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="fe1f4-263">Ouvrez le fichier ServiceConfiguration.Local.cscfg et vérifiez que la valeur de UseDevelopmentStorage est définie sur true.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-263">Open the ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set to true.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="fe1f4-264">Dès lors que les chaînes de connexion sont définies, une fois déployée, votre application conserve les données de diagnostic dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-264">Now that the connection strings are set, your application will persist diagnostics data to your storage account when your application is deployed.</span></span>
4. <span data-ttu-id="fe1f4-265">Enregistrez et générez votre projet, puis déployez votre application.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="fe1f4-266">Étape 2 : (facultatif) création de compteurs de performances personnalisés</span><span class="sxs-lookup"><span data-stu-id="fe1f4-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="fe1f4-267">Outre les compteurs de performances prédéfinis, vous pouvez ajouter les vôtres pour surveiller les rôles Web ou de travail.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-267">In addition to the pre-defined performance counters, you can add your own custom performance counters to monitor web or worker roles.</span></span> <span data-ttu-id="fe1f4-268">Les compteurs de performances personnalisés permettent de suivre et de surveiller le comportement propre à une application. Vous pouvez les créer ou les supprimer dans une tâche de démarrage, un rôle Web ou un rôle de travail avec des autorisations élevées.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-268">Custom performance counters may be used to track and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="fe1f4-269">Étape 2 : L’agent de diagnostics Azure actualise la configuration du compteur de performance à partir du fichier .wadcfg une minute après le démarrage.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-269">The Azure diagnostics agent refreshes the performance counter configuration from the .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="fe1f4-270">Si vous créez des compteurs de performance personnalisés dans la méthode OnStart et vos tâches de démarrage prennent plus d’une minute pour s’exécuter, vos compteurs de performance personnalisés ne seront pas créés lorsque l’agent de Diagnostics Microsoft Azure tente de les charger.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-270">If you create custom performance counters in the OnStart method and your startup tasks take longer than one minute to execute, your custom performance counters will not have been created when the Azure Diagnostics agent tries to load them.</span></span>  <span data-ttu-id="fe1f4-271">Dans ce scénario, vous verrez qu’Azure Diagnostics capture correctement toutes les données de diagnostic, excepté les compteurs de performance personnalisés.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="fe1f4-272">Pour résoudre ce problème, créez les compteurs de performance dans une tâche de démarrage ou déplacez certaines de vos tâches de démarrage vers la méthode OnStart après avoir créé les compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-272">To resolve this issue, create the performance counters in a startup task or move some of your startup task work to the OnStart method after creating the performance counters.</span></span>

<span data-ttu-id="fe1f4-273">Pour créer un simple compteur de performances personnalisé nommé « \MyCustomCounterCategory\MyButton1Counter », procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fe1f4-273">Perform the following steps to create a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="fe1f4-274">Ouvrez le fichier de définition de service (CSDEF) de votre application.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-274">Open the service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="fe1f4-275">Ajoutez l'élément Runtime à l'élément WebRole ou WorkerRole pour permettre une exécution avec des privilèges élevés :</span><span class="sxs-lookup"><span data-stu-id="fe1f4-275">Add the Runtime element to the WebRole or WorkerRole element to allow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="fe1f4-276">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="fe1f4-276">Save the file.</span></span>
4. <span data-ttu-id="fe1f4-277">Ouvrez le fichier de diagnostics (diagnostics.wadcfg dans le Kit de développement logiciel 2.4 et antérieur ou diagnostics.wadcfgx dans le kit de développement logiciel 2.5 et versions ultérieures) et ajoutez le code suivant à DiagnosticMonitorConfiguration :</span><span class="sxs-lookup"><span data-stu-id="fe1f4-277">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="fe1f4-278">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="fe1f4-278">Save the file.</span></span>
6. <span data-ttu-id="fe1f4-279">Créez la catégorie de compteur de performances personnalisée dans la méthode OnStart de votre rôle avant d'appeler base.OnStart.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-279">Create the custom performance counter category in the OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="fe1f4-280">L'exemple C# suivant permet de créer une catégorie personnalisée, si elle n'existe pas déjà :</span><span class="sxs-lookup"><span data-stu-id="fe1f4-280">The following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="fe1f4-281">Mettez à jour les compteurs dans l'application.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-281">Update the counters within your application.</span></span> <span data-ttu-id="fe1f4-282">Dans l'exemple suivant, un compteur de performances personnalisé est mis à jour lors d'événements Button1_Click :</span><span class="sxs-lookup"><span data-stu-id="fe1f4-282">The following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="fe1f4-283">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="fe1f4-283">Save the file.</span></span>  

<span data-ttu-id="fe1f4-284">Les données du compteur de performances personnalisé vont être collectées par le moniteur de diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-284">Custom performance counter data will now be collected by the Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="fe1f4-285">Étape 3 : interrogation des données de compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="fe1f4-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="fe1f4-286">Une fois votre application déployée et exécutée, le moniteur de diagnostics commence à collecter les compteurs de performances et à conserver ces données dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-286">Once your application is deployed and running, the Diagnostics monitor will begin collecting performance counters and persisting that data to Azure storage.</span></span> <span data-ttu-id="fe1f4-287">Pour examiner les données des compteurs de performances dans la table WADPerformanceCountersTable, vous pouvez utiliser des outils tels que l’Explorateur de serveurs de Visual Studio, [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/) ou [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) de Cerebrata.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata to view the performance counters data in the WADPerformanceCountersTable table.</span></span> <span data-ttu-id="fe1f4-288">Vous pouvez également interroger le service de Table par programme en utilisant [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md) ou [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="fe1f4-288">You can also programmatically query the Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="fe1f4-289">Dans l'exemple C# suivant, une requête basique est exécutée sur la table WADPerformanceCountersTable et les données de diagnostic sont enregistrées dans un fichier CSV.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-289">The following C# example shows a basic query against the WADPerformanceCountersTable table and saves the diagnostics data to a CSV file.</span></span> <span data-ttu-id="fe1f4-290">Une fois que les compteurs de performances sont enregistrés dans un fichier CSV, vous pouvez visualiser les données à l'aide des fonctionnalités de création de graphiques de Microsoft Excel ou d'un autre outil.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-290">Once the performance counters are saved to a CSV file, you can use the graphing capabilities in Microsoft Excel or some other tool to visualize the data.</span></span> <span data-ttu-id="fe1f4-291">Veillez à ajouter une référence à Microsoft.WindowsAzure.Storage.dll, qui figure dans le Kit de développement logiciel (SDK) Azure pour .NET d'octobre 2012 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-291">Be sure to add a reference to Microsoft.WindowsAzure.Storage.dll, which is included in the Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="fe1f4-292">L’assembly est installé dans le répertoire %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-292">The assembly is installed to the %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get the connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using the Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use the CloudConfigurationManager type
// to retrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store the connection string in your web.config or app.config file.
// Use the ConfigurationManager type to retrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference to the storage account using the connection string.  You can also use the development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create the table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute the table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process the query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="fe1f4-293">Les entités mappent vers les objets C# en utilisant une classe personnalisée dérivée d’une **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="fe1f4-293">Entities map to C# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="fe1f4-294">Le code suivant permet de définir une classe d'entité qui représente un compteur de performances dans la table **WADPerformanceCountersTable** .</span><span class="sxs-lookup"><span data-stu-id="fe1f4-294">The following code defines an entity class that represents a performance counter in the **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="fe1f4-295">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe1f4-295">Next Steps</span></span>
[<span data-ttu-id="fe1f4-296">Afficher d’autres articles sur les diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="fe1f4-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
