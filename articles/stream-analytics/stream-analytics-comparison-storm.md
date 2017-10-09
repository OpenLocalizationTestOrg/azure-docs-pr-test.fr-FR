---
title: "Les plateformes Analytique : Apache Storm comparaison tooStream Analytique | Documents Microsoft"
description: "Obtenez des conseils en choisissant une plateforme en nuage analytique à l’aide d’un tooStream de comparaison d’Apache Storm Analytique. Découvrez les fonctionnalités et les différences."
keywords: "plateforme d’analyse, plateformes d’analyse, plateforme d’analyse cloud, comparaison avec storm"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="bf714-105">Choix d’une plateforme d’analyse de flux : comparaison d’Apache Storm et d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bf714-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="bf714-106">Azure fournit plusieurs solutions pour analyser les données de flux : [Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/) et [Apache Storm sur Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span><span class="sxs-lookup"><span data-stu-id="bf714-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="bf714-107">Les deux plateformes analytique offrent des avantages de hello d’une solution PaaS.</span><span class="sxs-lookup"><span data-stu-id="bf714-107">Both analytics platforms provide hello benefits of a PaaS solution.</span></span> <span data-ttu-id="bf714-108">Mais les plateformes hello aient des différences significatives dans leurs fonctionnalités, ainsi que dans la façon dont vous configurez et les gérez.</span><span class="sxs-lookup"><span data-stu-id="bf714-108">But hello platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="bf714-109">Cet article offre une comparaison côte-à-côte toohelp fonctionnalités que vous choisissez entre Apache Storm et Analytique de flux de données Azure comme plateforme cloud analytique.</span><span class="sxs-lookup"><span data-stu-id="bf714-109">This article provides a side-by-side comparison of features toohelp you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="bf714-110">Fonctionnalités générales</span><span class="sxs-lookup"><span data-stu-id="bf714-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-111">
                    <strong></strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="bf714-112">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="bf714-113">
                    <strong>Apache Storm sur HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-114">
                    <strong>Open Source ?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-115">Non.</span><span class="sxs-lookup"><span data-stu-id="bf714-115">No.</span></span> <span data-ttu-id="bf714-116">Azure Stream Analytics est une offre propriétaire de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bf714-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-117">Oui.</span><span class="sxs-lookup"><span data-stu-id="bf714-117">Yes.</span></span> <span data-ttu-id="bf714-118">Apache Storm est une technologie sous licence Apache.</span><span class="sxs-lookup"><span data-stu-id="bf714-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-119">
                    <strong>Support Microsoft ?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-120">Oui</span><span class="sxs-lookup"><span data-stu-id="bf714-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-121">Oui</span><span class="sxs-lookup"><span data-stu-id="bf714-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-122">
                    <strong>Configuration matérielle requise</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-123">Aucune.</span><span class="sxs-lookup"><span data-stu-id="bf714-123">None.</span></span> <span data-ttu-id="bf714-124">Azure Stream Analytics est un service Azure.</span><span class="sxs-lookup"><span data-stu-id="bf714-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-125">Aucune.</span><span class="sxs-lookup"><span data-stu-id="bf714-125">None.</span></span> <span data-ttu-id="bf714-126">Apache Storm est un service Azure.</span><span class="sxs-lookup"><span data-stu-id="bf714-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-127">
                    <strong>Unité de niveau supérieur</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-128">Les utilisateurs déploient et surveillent les travaux de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="bf714-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-129">Les utilisateurs déploient et surveillent un cluster entier, qui peut héberger plusieurs travaux Storm ainsi que d’autres charges de travail (notamment le traitement).</span><span class="sxs-lookup"><span data-stu-id="bf714-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-130">
                    <strong>Tarification</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-131">Prix par volume de données traitées et nombre de hello d’unités de diffusion requis par heure qui hello de travail est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bf714-131">Priced by volume of data processed and hello number of streaming units required per hour that hello job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="bf714-132">Pour plus d’informations, voir <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Tarification de Stream Analytics </a>.</span><span class="sxs-lookup"><span data-stu-id="bf714-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-133">unité Hello d’achat est basé sur le cluster et est facturée en fonction hello exécution de cluster de hello, indépendante des tâches de déploiement.</span><span class="sxs-lookup"><span data-stu-id="bf714-133">hello unit of purchase is cluster-based, and is charged based on hello time hello cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="bf714-134">Pour plus d’informations, voir <a href="http://azure.microsoft.com/pricing/details/hdinsight/">Tarification de HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="bf714-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="bf714-135">Création</span><span class="sxs-lookup"><span data-stu-id="bf714-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-136">
                    <strong></strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="bf714-137">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="bf714-138">
                    <strong>Apache Storm sur HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-139">
                    <strong>Fonctionnalités : langage DSL SQL ?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-140">Oui.</span><span class="sxs-lookup"><span data-stu-id="bf714-140">Yes.</span></span> <span data-ttu-id="bf714-141">Stream Analytics fournit un langage de type SQL pour créer des transformations.</span><span class="sxs-lookup"><span data-stu-id="bf714-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-142">Non.</span><span class="sxs-lookup"><span data-stu-id="bf714-142">No.</span></span> <span data-ttu-id="bf714-143">Les utilisateurs écrivent du code en Java ou en C#, ou ils utilisent les API Trident.</span><span class="sxs-lookup"><span data-stu-id="bf714-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-144">
                    <strong>Fonctionnalités : opérateurs temporels ?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-145">Les agrégats fenêtrés et les jointures temporelles sont pris en charge par défaut.</span><span class="sxs-lookup"><span data-stu-id="bf714-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-146">Opérateurs temporels doivent être implémentées par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="bf714-146">Temporal operators must be implemented by hello user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-147">
                    <strong>Expérience de développement</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-148">Les utilisateurs peuvent créer, déboguer et surveiller les travaux via hello portail Azure, à l’aide des exemples de données dérivés d’un flux en direct.</span><span class="sxs-lookup"><span data-stu-id="bf714-148">Users can create, debug, and monitor jobs through hello Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-149">À l’aide de .NET, les utilisateurs peuvent développer, déboguer et surveiller au moyen de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf714-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="bf714-150">Utilisateurs à l’aide de Java ou autres langages peuvent utiliser hello IDE de leur choix.</span><span class="sxs-lookup"><span data-stu-id="bf714-150">Users using Java or other languages can use hello IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-151">
                    <strong>Prise en charge du débogage</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-152">Les journaux d’état et les opérations de base de travail sont disponibles toohelp debug.</span><span class="sxs-lookup"><span data-stu-id="bf714-152">Basic job status and operations logs are available toohelp debug.</span></span> <span data-ttu-id="bf714-153">Analytique de flux de données actuellement ne permet pas aux utilisateurs spécifier quel contenu ou la quantité de contenu est inclus dans les journaux hello (autrement dit, le mode détaillé).</span><span class="sxs-lookup"><span data-stu-id="bf714-153">Stream Analytics currently does not let users specify what content or how much content is included in hello logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-154">Des journaux détaillés sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="bf714-154">Detailed logs are available.</span></span> <span data-ttu-id="bf714-155">Les utilisateurs peuvent accéder à des journaux dans Visual Studio ou en vous connectant toohello cluster et accéder directement aux journaux de hello.</span><span class="sxs-lookup"><span data-stu-id="bf714-155">Users can access logs in Visual Studio or by logging in toohello cluster and accessing hello logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-156">
                    <strong>Extensibilité à l’aide de code personnalisé ?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-157">Prend partiellement en charge les fonctions JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bf714-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="bf714-158">Pour plus d’informations, voir <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">Intégration d’UDF JavaScript</a>.</span><span class="sxs-lookup"><span data-stu-id="bf714-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-159">Oui.</span><span class="sxs-lookup"><span data-stu-id="bf714-159">Yes.</span></span> <span data-ttu-id="bf714-160">Les utilisateurs peuvent écrire du code personnalisé en C#, Java ou dans tout autre langage pris en charge sur Storm.</span><span class="sxs-lookup"><span data-stu-id="bf714-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="bf714-161">Sources de données (entrées) et sorties</span><span class="sxs-lookup"><span data-stu-id="bf714-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-162">
                    <strong></strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="bf714-163">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="bf714-164">
                    <strong>Apache Storm sur HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-165">
                 <strong>Sources de données d’entrée</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="bf714-166">Azure Event Hubs et stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="bf714-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-167">Des connecteurs sont disponibles pour Azure Event Hubs, Azure Service Bus, Kafka, etc.</span><span class="sxs-lookup"><span data-stu-id="bf714-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="bf714-168">Les utilisateurs peuvent créer des connecteurs supplémentaires à l’aide de code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="bf714-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-169">
                    <strong>Formats de données d’entrée</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-170">Avro, JSON, CSV</span><span class="sxs-lookup"><span data-stu-id="bf714-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-171">Les utilisateurs peuvent implémenter tout format à l’aide de code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="bf714-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-172">
                    <strong>Sorties</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-173">Un travail de diffusion en continu peut compter plusieurs sorties.</span><span class="sxs-lookup"><span data-stu-id="bf714-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="bf714-174">Sorties prises en charge : Azure Event Hubs, stockage Blob Azure, stockage Table Azure, Azure SQL DB et Power BI.</span><span class="sxs-lookup"><span data-stu-id="bf714-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-175">Storm prend en charge de nombreuses sorties dans une topologie, et chacune peut disposer d’une logique personnalisée pour le traitement en aval.</span><span class="sxs-lookup"><span data-stu-id="bf714-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="bf714-176">Storm inclut des connecteurs pour Power BI, Azure Event Hubs, le stockage Blob Azure, Azure Cosmos DB, SQL et HBase.</span><span class="sxs-lookup"><span data-stu-id="bf714-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="bf714-177">Les utilisateurs peuvent créer des connecteurs supplémentaires à l’aide de code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="bf714-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-178">
                    <strong>Formats d’encodage des données</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-179">Les données doivent être formatées à l’aide de UTF-8.</span><span class="sxs-lookup"><span data-stu-id="bf714-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-180">Les utilisateurs peuvent implémenter tout format d’encodage des données à l’aide de code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="bf714-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="bf714-181">Gestion et opérations</span><span class="sxs-lookup"><span data-stu-id="bf714-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-182">
                    <strong></strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="bf714-183">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="bf714-184">
                    <strong>Apache Storm sur HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-185">
                    <strong>Modèle de déploiement de travail</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-186">Portail Azure, PowerShell et interfaces API REST.</span><span class="sxs-lookup"><span data-stu-id="bf714-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-187">Portail Azure, PowerShell, Visual Studio et interfaces API REST.</span><span class="sxs-lookup"><span data-stu-id="bf714-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-188">
                    <strong>Analyse (statistiques, compteurs, etc.)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-189">L’analyse est implémentée via le portail Azure et les interfaces API REST.</span><span class="sxs-lookup"><span data-stu-id="bf714-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="bf714-190">Les utilisateurs peuvent également configurer des alertes Azure.</span><span class="sxs-lookup"><span data-stu-id="bf714-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-191">Analyse est implémentée à l’aide de hello Storm UI et l’API REST.</span><span class="sxs-lookup"><span data-stu-id="bf714-191">Monitoring is implemented using hello Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-192">
                    <strong>Extensibilité</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-193">L’évolutivité est déterminée par le nombre de hello d’unités de diffusion en continu (SUs) pour chaque tâche.</span><span class="sxs-lookup"><span data-stu-id="bf714-193">Scalability is determined by hello number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="bf714-194">Chaque unité de diffusion en continu traite des too1 Mo par seconde, avec une capacité maximale de 50.</span><span class="sxs-lookup"><span data-stu-id="bf714-194">Each Streaming Unit processes up too1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="bf714-195">Pour plus d’informations, consultez <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">débit tooincrease de mise à l’échelle</a>.</span><span class="sxs-lookup"><span data-stu-id="bf714-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-196">L’évolutivité est déterminée par le nombre de hello de nœuds de cluster HDInsight Storm de hello.</span><span class="sxs-lookup"><span data-stu-id="bf714-196">Scalability is determined by hello number of nodes in hello HDInsight Storm cluster.</span></span> <span data-ttu-id="bf714-197">Hello supérieur hello nombre limite de nœuds est définie par le quota de l’utilisateur hello Azure.</span><span class="sxs-lookup"><span data-stu-id="bf714-197">hello top limit on hello number of nodes is defined by hello user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-198">
                    <strong>Limites de traitement des données</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-199">Les utilisateurs peuvent augmenter le traitement des données ou optimiser les coûts en augmentant ou diminuant le nombre de hello d’unités de diffusion en continu, avec une limite supérieure de 1 Go par seconde.</span><span class="sxs-lookup"><span data-stu-id="bf714-199">Users can increase data processing or optimize costs by increasing or decreasing hello number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-200">Les utilisateurs peuvent mettre à l’échelle la taille du cluster en l’augmentant ou en la réduisant.</span><span class="sxs-lookup"><span data-stu-id="bf714-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-201">
                    <strong>Arrêt/Reprise</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-202">Arrêt et reprise à partir du dernier arrêt.</span><span class="sxs-lookup"><span data-stu-id="bf714-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-203">Arrêt et reprise à partir du dernier arrêt basé sur un filigrane.</span><span class="sxs-lookup"><span data-stu-id="bf714-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-204">
                    <strong>Mise à jour de service et d’infrastructure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-205">Mise à jour corrective automatique sans temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="bf714-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-206">Mise à jour corrective automatique sans temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="bf714-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-207">
                    <strong>Continuité d’activité via un service hautement disponible avec contrats SLA garantis</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="bf714-208">Contrat SLA de temps d’activité de 99,9 %</span><span class="sxs-lookup"><span data-stu-id="bf714-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="bf714-209">Récupération automatique des défaillances</span><span class="sxs-lookup"><span data-stu-id="bf714-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="bf714-210">Récupération intégrée des opérateurs temporels avec état</span><span class="sxs-lookup"><span data-stu-id="bf714-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-211">Contrat SLA de 99,9 % de cluster de Storm hello.</span><span class="sxs-lookup"><span data-stu-id="bf714-211">SLA of 99.9% uptime of hello Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="bf714-212">Apache Storm est une plateforme de diffusion en continu à tolérance de panne.</span><span class="sxs-lookup"><span data-stu-id="bf714-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="bf714-213">Toutefois, il est tooensure de responsabilité de l’utilisateur hello que de diffusion en continu exécution des travaux sans interruption.</span><span class="sxs-lookup"><span data-stu-id="bf714-213">However, it is hello user's responsibility tooensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="bf714-214">Fonctionnalités avancées</span><span class="sxs-lookup"><span data-stu-id="bf714-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-215">
                    <strong></strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="bf714-216">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="bf714-217">
                    <strong>Apache Storm sur HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-218">
                    <strong>Arrivée tardive et gestion des événements de manière désordonnée</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-219">Des stratégies configurables intégrées peuvent réorganiser et supprimer des événements ou régler leur heure.</span><span class="sxs-lookup"><span data-stu-id="bf714-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-220">Les utilisateurs doivent implémenter logique toohandle ce scénario.</span><span class="sxs-lookup"><span data-stu-id="bf714-220">Users must implement logic toohandle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-221">
                    <strong>Données de référence</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-222">Les données de référence sont disponibles à partir du stockage Blob Azure avec un maximum de 100 Mo de cache en mémoire.</span><span class="sxs-lookup"><span data-stu-id="bf714-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="bf714-223">Les données de référence sont actualisées par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="bf714-223">Reference data is refreshed by hello service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-224">Aucune limitation de la taille des données.</span><span class="sxs-lookup"><span data-stu-id="bf714-224">No limits on data size.</span></span> <span data-ttu-id="bf714-225">Des connecteurs sont disponibles pour HBase, Azure Cosmos DB, SQL Server et Azure.</span><span class="sxs-lookup"><span data-stu-id="bf714-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="bf714-226">Les utilisateurs peuvent créer des connecteurs supplémentaires à l’aide de code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="bf714-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="bf714-227">Les données de référence doivent être actualisées à l’aide de code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="bf714-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="bf714-228">
                    <strong>Intégration à Machine Learning</strong>
                </span><span class="sxs-lookup"><span data-stu-id="bf714-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="bf714-229">Les modèles Azure Machine Learning publiés peuvent être configurés en tant que fonctions lors de la création d’un travail.</span><span class="sxs-lookup"><span data-stu-id="bf714-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="bf714-230">Pour plus d’informations, voir <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Mettre à l’échelle pour les fonctions Machine Learning</a>.</span><span class="sxs-lookup"><span data-stu-id="bf714-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="bf714-231">Disponible via Storm Bolts.</span><span class="sxs-lookup"><span data-stu-id="bf714-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
