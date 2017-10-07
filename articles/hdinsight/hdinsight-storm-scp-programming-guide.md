---
title: guide de programmation aaaSCP.NET | Documents Microsoft
description: "Découvrez comment toouse SCP.NET toocreate. Topologies de Storm basée sur le réseau pour les utilisent avec Storm sur HDInsight."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="1b382-103">Guide de programmation SCP</span><span class="sxs-lookup"><span data-stu-id="1b382-103">SCP programming guide</span></span>
<span data-ttu-id="1b382-104">SCP est une plateforme toobuild en temps réel, une application de traitement de données fiable, cohérente et plus performante.</span><span class="sxs-lookup"><span data-stu-id="1b382-104">SCP is a platform toobuild real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="1b382-105">Il est construit sur [Apache Storm](http://storm.incubator.apache.org/) --un système conçu par les Communautés hello OSS de traitement du flux de données.</span><span class="sxs-lookup"><span data-stu-id="1b382-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by hello OSS communities.</span></span> <span data-ttu-id="1b382-106">Storm est conçu par Nathan Marz et diffusé en open source par Twitter.</span><span class="sxs-lookup"><span data-stu-id="1b382-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="1b382-107">Il s’appuie sur [Apache soigneur](http://zookeeper.apache.org/), Apache un autre projet tooenable coordination distribuée hautement fiable et la gestion d’état.</span><span class="sxs-lookup"><span data-stu-id="1b382-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project tooenable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="1b382-108">Non seulement les projets hello SCP déplacée Storm sur Windows, mais également le projet de hello ajouté extensions et personnalisation pour l’écosystème de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-108">Not only hello SCP project ported Storm on Windows but also hello project added extensions and customization for hello Windows ecosystem.</span></span> <span data-ttu-id="1b382-109">les extensions de Hello incluent l’expérience de développement .NET et des bibliothèques, personnalisation de hello inclut le déploiement basé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="1b382-109">hello extensions include .NET developer experience, and libraries, hello customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="1b382-110">personnalisation et extension de hello est effectuée de sorte que nous n’avez pas besoin de projets de systèmes d’exploitation toofork hello et nous avons tirer parti des écosystèmes dérivées reposant sur Storm.</span><span class="sxs-lookup"><span data-stu-id="1b382-110">hello extension and customization is done in such a way that we do not need toofork hello OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="1b382-111">Modèle de traitement</span><span class="sxs-lookup"><span data-stu-id="1b382-111">Processing model</span></span>
<span data-ttu-id="1b382-112">les données de salutation SCP sont modélisées en tant que flux continus de tuples.</span><span class="sxs-lookup"><span data-stu-id="1b382-112">hello data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="1b382-113">En général, les tuples hello flux dans une file d’attente tout d’abord, puis récupéré et transformés par la logique métier hébergée au sein d’une topologie Storm, enfin hello sortie peut être transmis en tant que système tooanother SCP de tuples, ou être validées toostores comme système de fichiers distribués ou bases de données tels que SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1b382-113">Typically hello tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally hello output could be piped as tuples tooanother SCP system, or be committed toostores like distributed file system or databases like SQL Server.</span></span>

![Un diagramme d’une file d’attente tooprocessing de données qui alimente un magasin de données d’alimentation](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="1b382-115">Dans Storm, une topologie d'application définit un graphique de calcul.</span><span class="sxs-lookup"><span data-stu-id="1b382-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="1b382-116">Chaque nœud d'une topologie contient une logique de traitement et les liens entre ces nœuds indiquent les flux de données.</span><span class="sxs-lookup"><span data-stu-id="1b382-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="1b382-117">données d’entrée tooinject nœuds Hello dans la topologie de hello sont appelées becs verseurs, qui peuvent être des données hello toosequence utilisé.</span><span class="sxs-lookup"><span data-stu-id="1b382-117">hello nodes tooinject input data into hello topology are called Spouts, which can be used toosequence hello data.</span></span> <span data-ttu-id="1b382-118">données d’entrée Hello peuvent résider dans des fichiers journaux, de la base de données transactionnelle, compteur de performance système nœuds de hello etc. avec les deux flux de données d’entrée et de sortie sont appelées boulons, lequel hello le filtrage des données réelles et les sélections et agrégation.</span><span class="sxs-lookup"><span data-stu-id="1b382-118">hello input data could reside in file logs, transactional database, system performance counter etc. hello nodes with both input and output data flows are called Bolts, which do hello actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="1b382-119">SCP prend en charge les types de traitement de données Meilleur effort, Une fois au minimum et Exactement une.</span><span class="sxs-lookup"><span data-stu-id="1b382-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="1b382-120">Dans une application distribuée de traitement de diffusion en continu, diverses erreurs peuvent se produire pendant le traitement des données, telles qu’une erreur de code utilisateur, la défaillance d’un ordinateur ou une panne du réseau. Au moins une transformation garantit que toutes les données sont traitées au moins une fois par relecture automatiquement hello données mêmes lorsqu’une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="1b382-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically hello same data when error happens.</span></span> <span data-ttu-id="1b382-121">Le type de traitement Une fois au minimum est simple et fiable et s'adapte à de nombreuses applications.</span><span class="sxs-lookup"><span data-stu-id="1b382-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="1b382-122">Toutefois, lors de l’application hello requiert le comptage exact, par exemple, au moins une est insuffisante car hello mêmes données pourraient potentiellement être lu dans la topologie de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-122">However, when hello application requires exact counting, for example, at-least-once processing is insufficient since hello same data could potentially be played in hello application topology.</span></span> <span data-ttu-id="1b382-123">Dans ce cas, exactement-une fois que le traitement est conçu toomake que résultat de hello est correct, même lorsque les données de salutation peuvent être relues et traitées plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="1b382-123">In that case, exactly-once processing is designed toomake sure hello result is correct even when hello data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="1b382-124">SCP permet d’applications de processus de données en temps réel de toodevelop pour les développeurs .NET lorsque hello de tirer parti de la Machine virtuelle Java (JVM) en fonction de Storm sous hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-124">SCP enables .NET developers toodevelop real time data process applications while leverage hello Java Virtual Machine (JVM) based Storm under hello cover.</span></span> <span data-ttu-id="1b382-125">Hello .NET et JVM communiquent via le socket TCP local.</span><span class="sxs-lookup"><span data-stu-id="1b382-125">hello .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="1b382-126">En principe chaque bec/éclair est une paire de processus .net/Java, où la logique de l’utilisateur hello s’exécute dans des processus de .net comme un plug-in.</span><span class="sxs-lookup"><span data-stu-id="1b382-126">Basically each Spout/Bolt is a .Net/Java process pair, where hello user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="1b382-127">toobuild un application par-dessus SCP de traitement des données, plusieurs étapes sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="1b382-127">toobuild a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="1b382-128">Concevoir et implémenter hello becs verseurs toopull dans les données à partir de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="1b382-128">Design and implement hello Spouts toopull in data from queue.</span></span>
* <span data-ttu-id="1b382-129">Concevoir et implémenter des données d’entrée de boulons tooprocess hello et enregistrer des magasins de données tooexternal comme base de données.</span><span class="sxs-lookup"><span data-stu-id="1b382-129">Design and implement Bolts tooprocess hello input data, and save data tooexternal stores such as Database.</span></span>
* <span data-ttu-id="1b382-130">Conception de topologie de hello, puis soumettre et exécuter la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-130">Design hello topology, then submit and run hello topology.</span></span> <span data-ttu-id="1b382-131">Hello topologie définit les sommets et les données de salutation flux entre les sommets hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-131">hello topology defines vertexes and hello data flows between hello vertexes.</span></span> <span data-ttu-id="1b382-132">SCP prend la spécification de topologie hello et déployez-le sur un cluster Storm, où chaque sommet s’exécute sur un seul nœud logique.</span><span class="sxs-lookup"><span data-stu-id="1b382-132">SCP will take hello topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="1b382-133">basculement de Hello et mise à l’échelle seront être pris en charge par le Planificateur de tâches Storm hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-133">hello failover and scaling will be taken care of by hello Storm task scheduler.</span></span>

<span data-ttu-id="1b382-134">Ce document utilise certains toowalk exemples simples via l’application de traitement des données toobuild avec SCP.</span><span class="sxs-lookup"><span data-stu-id="1b382-134">This document will use some simple examples toowalk through how toobuild data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="1b382-135">Interface de plug-in SCP</span><span class="sxs-lookup"><span data-stu-id="1b382-135">SCP Plugin Interface</span></span>
<span data-ttu-id="1b382-136">Plug-ins SCP (ou applications) sont des exécutables autonomes qui peuvent s’exécuter à l’intérieur de Visual Studio pendant la phase de développement hello et être intégrés au pipeline de Storm hello après le déploiement en production.</span><span class="sxs-lookup"><span data-stu-id="1b382-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during hello development phase, and be plugged into hello Storm pipeline after deployment in production.</span></span> <span data-ttu-id="1b382-137">L’écriture de plug-in hello SCP est simplement hello identique à celui de l’écriture de toutes les autres applications Windows standard console.</span><span class="sxs-lookup"><span data-stu-id="1b382-137">Writing hello SCP plugin is just hello same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="1b382-138">Plateforme SCP.NET déclare une interface pour bec/éclair et code de plug-in hello utilisateur doit implémenter ces interfaces.</span><span class="sxs-lookup"><span data-stu-id="1b382-138">SCP.NET platform declares some interface for spout/bolt, and hello user plugin code should implement these interfaces.</span></span> <span data-ttu-id="1b382-139">Hello principal de cette conception vise que cet utilisateur hello peut se concentrer sur leur propre logique d’entreprise et en laissant les autres toobe éléments géré par la plateforme SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="1b382-139">hello main purpose of this design is that hello user can focus on their own business logics, and leaving other things toobe handled by SCP.NET platform.</span></span>

<span data-ttu-id="1b382-140">code de plug-in Hello utilisateur doit implémenter l’une des interfaces de ce qui suit hello, varie selon que la topologie de hello est transactionnelle ou non transactionnelle, et si le composant de hello est bec ou éclair.</span><span class="sxs-lookup"><span data-stu-id="1b382-140">hello user plugin code should implement one of hello followings interfaces, depends on whether hello topology is transactional or non-transactional, and whether hello component is spout or bolt.</span></span>

* <span data-ttu-id="1b382-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="1b382-141">ISCPSpout</span></span>
* <span data-ttu-id="1b382-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="1b382-142">ISCPBolt</span></span>
* <span data-ttu-id="1b382-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="1b382-143">ISCPTxSpout</span></span>
* <span data-ttu-id="1b382-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="1b382-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="1b382-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="1b382-145">ISCPPlugin</span></span>
<span data-ttu-id="1b382-146">ISCPPlugin est l’interface commune de hello pour tous les types de plug-ins.</span><span class="sxs-lookup"><span data-stu-id="1b382-146">ISCPPlugin is hello common interface for all kinds of plugins.</span></span> <span data-ttu-id="1b382-147">Actuellement, c'est une interface factice.</span><span class="sxs-lookup"><span data-stu-id="1b382-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="1b382-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="1b382-148">ISCPSpout</span></span>
<span data-ttu-id="1b382-149">ISCPSpout est interface hello bec non transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="1b382-149">ISCPSpout is hello interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="1b382-150">Lorsque `NextTuple()` est appelée, hello C\# un ou plusieurs tuples peut émettre du code utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1b382-150">When `NextTuple()` is called, hello C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="1b382-151">Si aucune n’est tooemit, cette méthode doit retourner sans l’émission de quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="1b382-151">If there is nothing tooemit, this method should return without emitting anything.</span></span> <span data-ttu-id="1b382-152">Notez que `NextTuple()`, `Ack()` et `Fail()` sont toutes appelées dans une boucle étroite d’un thread unique dans un processus C\#.</span><span class="sxs-lookup"><span data-stu-id="1b382-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="1b382-153">Lorsqu’il n’y a aucune tooemit tuples, il est toohave courtois NextTuple veille pour un laps de temps (par exemple, les 10 millisecondes) ainsi en toowaste pas trop de ressources processeur.</span><span class="sxs-lookup"><span data-stu-id="1b382-153">When there are no tuples tooemit, it is courteous toohave NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="1b382-154">`Ack()` et `Fail()` sont appelées uniquement quand le mécanisme d’accusé de réception (ack) est activé dans le fichier spec.</span><span class="sxs-lookup"><span data-stu-id="1b382-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="1b382-155">Hello `seqId` est utilisé tooidentify hello tuple, qui est reçu ou a échoué.</span><span class="sxs-lookup"><span data-stu-id="1b382-155">hello `seqId` is used tooidentify hello tuple which is acked or failed.</span></span> <span data-ttu-id="1b382-156">Par conséquent, si l’accusé de réception est activée dans une topologie non transactionnel, hello suivant emit fonction doit être utilisé dans bec :</span><span class="sxs-lookup"><span data-stu-id="1b382-156">So if ack is enabled in non-transactional topology, hello following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="1b382-157">Si l’accusé de réception n’est pas pris en charge dans une topologie non transactionnel, hello `Ack()` et `Fail()` peut être laissée en tant que fonction vide.</span><span class="sxs-lookup"><span data-stu-id="1b382-157">If ack is not supported in non-transactional topology, hello `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="1b382-158">Hello `parms` des paramètres d’entrée de ces fonctions sont simplement vide dictionnaire, ils sont réservés à un usage ultérieur.</span><span class="sxs-lookup"><span data-stu-id="1b382-158">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="1b382-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="1b382-159">ISCPBolt</span></span>
<span data-ttu-id="1b382-160">ISCPBolt est interface hello éclair non transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="1b382-160">ISCPBolt is hello interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="1b382-161">Lors de la nouvelle tuple est disponible, hello `Execute()` fonction sera appelée tooprocess il.</span><span class="sxs-lookup"><span data-stu-id="1b382-161">When new tuple is available, hello `Execute()` function will be called tooprocess it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="1b382-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="1b382-162">ISCPTxSpout</span></span>
<span data-ttu-id="1b382-163">ISCPTxSpout est interface hello bec transactionnels.</span><span class="sxs-lookup"><span data-stu-id="1b382-163">ISCPTxSpout is hello interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="1b382-164">Tout comme leurs équivalentes non-transactionnelles, les fonctions `NextTx()`, `Ack()` et `Fail()` sont toutes appelées dans une boucle étroite d’un thread unique dans un processus C\#.</span><span class="sxs-lookup"><span data-stu-id="1b382-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="1b382-165">Lorsqu’il n’y a aucune tooemit de données, il est toohave courtois `NextTx` mise en veille pendant un court laps de temps (10 millisecondes) ainsi en toowaste pas trop de ressources processeur.</span><span class="sxs-lookup"><span data-stu-id="1b382-165">When there are no data tooemit, it is courteous toohave `NextTx` sleep for a short amount of time (10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="1b382-166">`NextTx()`est appelé toostart une nouvelle transaction, hello paramètre out `seqId` tooidentify utilisé hello transaction, qui est également utilisée dans `Ack()` et `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="1b382-166">`NextTx()` is called toostart a new transaction, hello out parameter `seqId` is used tooidentify hello transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="1b382-167">Dans `NextTx()`, utilisateur peut émettre du côté tooJava de données.</span><span class="sxs-lookup"><span data-stu-id="1b382-167">In `NextTx()`, user can emit data tooJava side.</span></span> <span data-ttu-id="1b382-168">Hello données seront stockées dans la relecture toosupport soigneur.</span><span class="sxs-lookup"><span data-stu-id="1b382-168">hello data will be stored in ZooKeeper toosupport replay.</span></span> <span data-ttu-id="1b382-169">Capacité hello soigneur étant très limitée, utilisateur doit émettre uniquement des métadonnées, pas les données en bloc dans bec transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="1b382-169">Because hello capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="1b382-170">Si une transaction échoue, Storm la relit automatiquement. Il ne faut donc pas appeler la fonction `Fail()` dans un cas normal.</span><span class="sxs-lookup"><span data-stu-id="1b382-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="1b382-171">Mais si le SCP peut vérifier les métadonnées hello émises par bec transactionnels, elle peut appeler `Fail()` lorsque les métadonnées hello ne sont pas valide.</span><span class="sxs-lookup"><span data-stu-id="1b382-171">But if SCP can check hello metadata emitted by transactional spout, it can call `Fail()` when hello metadata is invalid.</span></span>

<span data-ttu-id="1b382-172">Hello `parms` des paramètres d’entrée de ces fonctions sont simplement vide dictionnaire, ils sont réservés à un usage ultérieur.</span><span class="sxs-lookup"><span data-stu-id="1b382-172">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="1b382-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="1b382-173">ISCPBatchBolt</span></span>
<span data-ttu-id="1b382-174">ISCPBatchBolt est interface hello éclair transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="1b382-174">ISCPBatchBolt is hello interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="1b382-175">`Execute()`est appelé en cas de nouvelle tuple arrivant à éclair de hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-175">`Execute()` is called when there is new tuple arriving at hello bolt.</span></span> <span data-ttu-id="1b382-176">`FinishBatch()` est appelé quand cette transaction est terminée.</span><span class="sxs-lookup"><span data-stu-id="1b382-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="1b382-177">Hello `parms` paramètre d’entrée est réservé à un usage ultérieur.</span><span class="sxs-lookup"><span data-stu-id="1b382-177">hello `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="1b382-178">Il existe un concept important pour la topologie transactionnelle : `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="1b382-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="1b382-179">Il comporte deux champs : `TxId` et `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="1b382-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="1b382-180">`TxId`est utilisé tooidentify une transaction spécifique, et pour une transaction donnée, il peut y avoir plusieurs tentative si les transactions hello échoue et sont relu.</span><span class="sxs-lookup"><span data-stu-id="1b382-180">`TxId` is used tooidentify a specific transaction, and for a given transaction, there may be multiple attempt if hello transaction fails and is replayed.</span></span> <span data-ttu-id="1b382-181">SCP.NET sera à nouveau un autre ISCPBatchBolt objet tooprocess chaque `StormTxAttempt`, à l’instar de quel souhaitez-vous Storm côté de Java.</span><span class="sxs-lookup"><span data-stu-id="1b382-181">SCP.NET will new a different ISCPBatchBolt object tooprocess each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="1b382-182">Hello cette conception vise toosupport le traitement des transactions parallèles.</span><span class="sxs-lookup"><span data-stu-id="1b382-182">hello purpose of this design is toosupport parallel transactions processing.</span></span> <span data-ttu-id="1b382-183">Utilisateur devez la conserver à l’esprit que si la tentative de transaction est terminée et hello correspondant ISCPBatchBolt objet sera détruit par le garbage collector.</span><span class="sxs-lookup"><span data-stu-id="1b382-183">User should keep it in mind that if transaction attempt is finished, hello corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="1b382-184">Modèle objet</span><span class="sxs-lookup"><span data-stu-id="1b382-184">Object Model</span></span>
<span data-ttu-id="1b382-185">SCP.NET fournit également un ensemble simple des objets clés pour les développeurs des tooprogram avec.</span><span class="sxs-lookup"><span data-stu-id="1b382-185">SCP.NET also provides a simple set of key objects for developers tooprogram with.</span></span> <span data-ttu-id="1b382-186">Il s’agit des objets **Context**, **StateStore** et **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="1b382-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="1b382-187">Elles sont abordées dans la partie de rest hello de cette section.</span><span class="sxs-lookup"><span data-stu-id="1b382-187">They will be discussed in hello rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="1b382-188">Context</span><span class="sxs-lookup"><span data-stu-id="1b382-188">Context</span></span>
<span data-ttu-id="1b382-189">Contexte fournit une application de toohello d’environnement en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1b382-189">Context provides a running environment toohello application.</span></span> <span data-ttu-id="1b382-190">Chaque instance ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) dispose d'une instance Context correspondante.</span><span class="sxs-lookup"><span data-stu-id="1b382-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="1b382-191">fonctionnalité Hello fournie par le contexte peut être divisée en deux parties : partie statique de hello (1) qui est disponible dans hello ensemble C\# traiter, la partie dynamique de hello (2) qui est disponible uniquement pour l’instance spécifique de contexte hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-191">hello functionality provided by Context can be divided into two parts: (1) hello static part which is available in hello whole C\# process, (2) hello dynamic part which is only available for hello specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="1b382-192">Partie statique</span><span class="sxs-lookup"><span data-stu-id="1b382-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="1b382-193">`Logger` est fourni à des fins de journalisation.</span><span class="sxs-lookup"><span data-stu-id="1b382-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="1b382-194">`pluginType`est utilisé le type de plug-in tooindicate hello Hello C\# processus.</span><span class="sxs-lookup"><span data-stu-id="1b382-194">`pluginType` is used tooindicate hello plugin type of hello C\# process.</span></span> <span data-ttu-id="1b382-195">Si hello C\# processus est exécuté en mode de test local (sans Java), le type de plug-in hello est `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="1b382-195">If hello C\# process is run in local test mode (without Java), hello plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="1b382-196">`Config`est fourni à des paramètres de configuration tooget du côté de Java.</span><span class="sxs-lookup"><span data-stu-id="1b382-196">`Config` is provided tooget configuration parameters from Java side.</span></span> <span data-ttu-id="1b382-197">paramètres de Hello sont passés du côté de Java lorsque C\# plug-in est initialisé.</span><span class="sxs-lookup"><span data-stu-id="1b382-197">hello parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="1b382-198">Hello `Config` paramètres sont divisés en deux parties : `stormConf` et `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="1b382-198">hello `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="1b382-199">`stormConf`est des paramètres définis par Storm et `pluginConf` est paramètres hello définis par le SCP.</span><span class="sxs-lookup"><span data-stu-id="1b382-199">`stormConf` is parameters defined by Storm and `pluginConf` is hello parameters defined by SCP.</span></span> <span data-ttu-id="1b382-200">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1b382-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="1b382-201">`TopologyContext`est fourni le contexte de topologie tooget hello, il est particulièrement utile pour les composants avec plusieurs parallélisme.</span><span class="sxs-lookup"><span data-stu-id="1b382-201">`TopologyContext` is provided tooget hello topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="1b382-202">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="1b382-202">Here is an example:</span></span>

    //demo how tooget TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a><span data-ttu-id="1b382-203">Partie dynamique</span><span class="sxs-lookup"><span data-stu-id="1b382-203">Dynamic Part</span></span>
<span data-ttu-id="1b382-204">Hello après les interfaces est pertinente tooa certaine l’instance de contexte.</span><span class="sxs-lookup"><span data-stu-id="1b382-204">hello following interfaces are pertinent tooa certain Context instance.</span></span> <span data-ttu-id="1b382-205">l’instance de contexte Hello est créé par la plateforme SCP.NET et passé toohello le code utilisateur :</span><span class="sxs-lookup"><span data-stu-id="1b382-205">hello Context instance is created by SCP.NET platform and passed toohello user code:</span></span>

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="1b382-206">Pour bec non transactionnelle prenant en charge l’accusé de réception, hello suivant de méthode est fournie :</span><span class="sxs-lookup"><span data-stu-id="1b382-206">For non-transactional spout supporting ack, hello following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="1b382-207">Pour éclair non transactionnelle prenant en charge l’accusé de réception, il doit explicitement `Ack()` ou `Fail()` hello tuple qu’il a reçu.</span><span class="sxs-lookup"><span data-stu-id="1b382-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` hello tuple it received.</span></span> <span data-ttu-id="1b382-208">Et lors de l’émission de tuple de nouveau, il doit également spécifier ancres hello du tuple de nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-208">And when emitting new tuple, it must also specify hello anchors of hello new tuple.</span></span> <span data-ttu-id="1b382-209">Hello méthodes suivantes est fournie.</span><span class="sxs-lookup"><span data-stu-id="1b382-209">hello following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="1b382-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="1b382-210">StateStore</span></span>
<span data-ttu-id="1b382-211">`StateStore` fournit des services de métadonnées, une génération de séquence unitone et une coordination sans attente.</span><span class="sxs-lookup"><span data-stu-id="1b382-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="1b382-212">Il est possible de développer des abstractions concurrentielles distribuées et globales sur `StateStore`, notamment des verrous distribués, des files d’attente distribuées, des barrières et des services de transaction.</span><span class="sxs-lookup"><span data-stu-id="1b382-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="1b382-213">Les applications de SCP peuvent utiliser hello `State` objet toopersist certaines informations de soigneur, en particulier pour la topologie transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="1b382-213">SCP applications may use hello `State` object toopersist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="1b382-214">Ce faisant, si bec transactionnels tombe en panne et redémarrer, il peut récupérer les informations nécessaires hello soigneur et redémarrez le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-214">Doing so, if transactional spout crashes and restart, it can retrieve hello necessary information from ZooKeeper and restart hello pipeline.</span></span>

<span data-ttu-id="1b382-215">Hello `StateStore` objet comprend principalement les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b382-215">hello `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="1b382-216">Hello `State` objet comprend principalement les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b382-216">hello `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="1b382-217">Pourquoi `Commit()` la méthode simpleMode a la valeur tootrue, supprimera simplement hello correspondant ZNode dans soigneur.</span><span class="sxs-lookup"><span data-stu-id="1b382-217">For hello `Commit()` method, when simpleMode is set tootrue, it will simply delete hello corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="1b382-218">Sinon, elle supprimera hello ZNode actuel et l’ajout d’un nouveau nœud Bonjour validé\_chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="1b382-218">Otherwise, it will delete hello current ZNode, and adding a new node in hello COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="1b382-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="1b382-219">SCPRuntime</span></span>
<span data-ttu-id="1b382-220">SCPRuntime fournit deux méthodes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-220">SCPRuntime provides hello following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="1b382-221">`Initialize()`est un environnement d’exécution hello SCP tooinitialize utilisé.</span><span class="sxs-lookup"><span data-stu-id="1b382-221">`Initialize()` is used tooinitialize hello SCP runtime environment.</span></span> <span data-ttu-id="1b382-222">Dans cette méthode, hello C\# processus se connecteront à côté de Java toohello et obtient les paramètres de configuration et le contexte de la topologie.</span><span class="sxs-lookup"><span data-stu-id="1b382-222">In this method, hello C\# process will connect toohello Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="1b382-223">`LaunchPlugin()`est utilisé tookick désactiver le message de type hello du traitement de boucle.</span><span class="sxs-lookup"><span data-stu-id="1b382-223">`LaunchPlugin()` is used tookick off hello message processing loop.</span></span> <span data-ttu-id="1b382-224">Dans cette boucle, hello C\# plug-in reçoit les messages formulaire côté Java (y compris les signaux tuples et de contrôle) et traiter les messages hello, l’appel de la méthode d’interface hello peut-être fournissent par du code utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-224">In this loop, hello C\# plugin will receive messages form Java side (including tuples and control signals), and then process hello messages, perhaps calling hello interface method provide by hello user code.</span></span> <span data-ttu-id="1b382-225">paramètre d’entrée Hello pour la méthode `LaunchPlugin()` est un délégué qui peut retourner un objet qui implémente l’interface de ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="1b382-225">hello input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="1b382-226">Pour ISCPBatchBolt, nous pouvons obtenir `StormTxAttempt` de `parms`et l’utiliser toojudge s’il s’agit d’une tentative de relue.</span><span class="sxs-lookup"><span data-stu-id="1b382-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it toojudge whether it is a replayed attempt.</span></span> <span data-ttu-id="1b382-227">Cela est généralement effectué à éclair de validation hello et il est présenté dans hello `HelloWorldTx` exemple.</span><span class="sxs-lookup"><span data-stu-id="1b382-227">This is usually done at hello commit bolt, and it is demonstrated in hello `HelloWorldTx` example.</span></span>

<span data-ttu-id="1b382-228">En règle générale, hello plug-ins SCP peut-être s’exécuter dans deux modes ici :</span><span class="sxs-lookup"><span data-stu-id="1b382-228">Generally speaking, hello SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="1b382-229">Mode de Test local : Hello dans ce mode, plug-ins SCP (hello C\# code utilisateur) exécuté à l’intérieur de Visual Studio pendant la phase de développement hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-229">Local Test Mode: In this mode, hello SCP plugins (hello C\# user code) run inside Visual Studio during hello development phase.</span></span> <span data-ttu-id="1b382-230">`LocalContext`peut être utilisé dans ce mode, qui fournit une méthode tooserialize hello émis tuples toolocal fichiers et lire à nouveau toomemory.</span><span class="sxs-lookup"><span data-stu-id="1b382-230">`LocalContext` can be used in this mode, which provides method tooserialize hello emitted tuples toolocal files, and read them back toomemory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="1b382-231">Mode Normal : Dans ce mode, les plug-ins de SCP hello sont lancées par le processus java de storm.</span><span class="sxs-lookup"><span data-stu-id="1b382-231">Regular Mode: In this mode, hello SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="1b382-232">Voici un exemple de démarrage de plug-in SCP :</span><span class="sxs-lookup"><span data-stu-id="1b382-232">Here is an example of launching SCP plugin:</span></span>
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="1b382-233">Langage de spécification de topologie</span><span class="sxs-lookup"><span data-stu-id="1b382-233">Topology Specification Language</span></span>
<span data-ttu-id="1b382-234">La spécification de topologie SCP est un langage de domaine spécifique pour décrire et configurer les topologies SCP.</span><span class="sxs-lookup"><span data-stu-id="1b382-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="1b382-235">Il est basé sur Clojure DSL de Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) et est étendu par SCP.</span><span class="sxs-lookup"><span data-stu-id="1b382-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="1b382-236">Spécifications de topologie peuvent être envoyées directement toostorm de cluster pour l’exécution via hello ***runspec*** commande.</span><span class="sxs-lookup"><span data-stu-id="1b382-236">Topology specifications can be submitted directly toostorm cluster for execution via hello ***runspec*** command.</span></span>

<span data-ttu-id="1b382-237">SCP.NET a Ajouter suivez fonctions toodefine hello topologie transactionnelle :</span><span class="sxs-lookup"><span data-stu-id="1b382-237">SCP.NET has add follow functions toodefine hello Transactional Topology:</span></span>

| <span data-ttu-id="1b382-238">**Nouvelles fonctions**</span><span class="sxs-lookup"><span data-stu-id="1b382-238">**New Functions**</span></span> | <span data-ttu-id="1b382-239">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="1b382-239">**Parameters**</span></span> | <span data-ttu-id="1b382-240">**Description**</span><span class="sxs-lookup"><span data-stu-id="1b382-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b382-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="1b382-241">**tx-topolopy**</span></span> |<span data-ttu-id="1b382-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="1b382-242">topology-name</span></span><br /><span data-ttu-id="1b382-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="1b382-243">spout-map</span></span><br /><span data-ttu-id="1b382-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="1b382-244">bolt-map</span></span> |<span data-ttu-id="1b382-245">Définition d’une topologie transactionnelle avec le nom de topologie hello, &nbsp;becs verseurs amovibles de mappage de la définition et le mappage de définition de boulons hello</span><span class="sxs-lookup"><span data-stu-id="1b382-245">Define a transactional topology with hello topology name, &nbsp;spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="1b382-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="1b382-246">**scp-tx-spout**</span></span> |<span data-ttu-id="1b382-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="1b382-247">exec-name</span></span><br /><span data-ttu-id="1b382-248">args</span><span class="sxs-lookup"><span data-stu-id="1b382-248">args</span></span><br /><span data-ttu-id="1b382-249">fields</span><span class="sxs-lookup"><span data-stu-id="1b382-249">fields</span></span> |<span data-ttu-id="1b382-250">Permet de définir un spout transactionnel.</span><span class="sxs-lookup"><span data-stu-id="1b382-250">Define a transactional spout.</span></span> <span data-ttu-id="1b382-251">Il s’exécutera application hello avec ***exec-name*** à l’aide de ***args***.</span><span class="sxs-lookup"><span data-stu-id="1b382-251">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="1b382-252">Hello ***champs*** est les champs de sortie hello pour bec</span><span class="sxs-lookup"><span data-stu-id="1b382-252">hello ***fields*** is hello Output Fields for spout</span></span> |
| <span data-ttu-id="1b382-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="1b382-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="1b382-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="1b382-254">exec-name</span></span><br /><span data-ttu-id="1b382-255">args</span><span class="sxs-lookup"><span data-stu-id="1b382-255">args</span></span><br /><span data-ttu-id="1b382-256">fields</span><span class="sxs-lookup"><span data-stu-id="1b382-256">fields</span></span> |<span data-ttu-id="1b382-257">Permet de définir un lot bolt transactionnel.</span><span class="sxs-lookup"><span data-stu-id="1b382-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="1b382-258">Il s’exécutera application hello avec ***exec-name*** à l’aide de ***args.***</span><span class="sxs-lookup"><span data-stu-id="1b382-258">It will run hello application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="1b382-259">Hello champs sont hello champs de sortie pour éclair.</span><span class="sxs-lookup"><span data-stu-id="1b382-259">hello Fields is hello Output Fields for bolt.</span></span> |
| <span data-ttu-id="1b382-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="1b382-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="1b382-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="1b382-261">exec-name</span></span><br /><span data-ttu-id="1b382-262">args</span><span class="sxs-lookup"><span data-stu-id="1b382-262">args</span></span><br /><span data-ttu-id="1b382-263">fields</span><span class="sxs-lookup"><span data-stu-id="1b382-263">fields</span></span> |<span data-ttu-id="1b382-264">Permet de définir un validateur bolt transactionnel.</span><span class="sxs-lookup"><span data-stu-id="1b382-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="1b382-265">Il s’exécutera application hello avec ***exec-name*** à l’aide de ***args***.</span><span class="sxs-lookup"><span data-stu-id="1b382-265">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="1b382-266">Hello ***champs*** est les champs de sortie hello pour éclair</span><span class="sxs-lookup"><span data-stu-id="1b382-266">hello ***fields*** is hello Output Fields for bolt</span></span> |
| <span data-ttu-id="1b382-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="1b382-267">**nontx-topolopy**</span></span> |<span data-ttu-id="1b382-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="1b382-268">topology-name</span></span><br /><span data-ttu-id="1b382-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="1b382-269">spout-map</span></span><br /><span data-ttu-id="1b382-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="1b382-270">bolt-map</span></span> |<span data-ttu-id="1b382-271">Définition d’une topologie non transactionnel avec le nom de topologie hello,&nbsp; becs verseurs amovibles de mappage de la définition et le mappage de définition de boulons hello</span><span class="sxs-lookup"><span data-stu-id="1b382-271">Define a nontransactional topology with hello topology name,&nbsp; spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="1b382-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="1b382-272">**scp-spout**</span></span> |<span data-ttu-id="1b382-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="1b382-273">exec-name</span></span><br /><span data-ttu-id="1b382-274">args</span><span class="sxs-lookup"><span data-stu-id="1b382-274">args</span></span><br /><span data-ttu-id="1b382-275">fields</span><span class="sxs-lookup"><span data-stu-id="1b382-275">fields</span></span><br /><span data-ttu-id="1b382-276">Paramètres</span><span class="sxs-lookup"><span data-stu-id="1b382-276">parameters</span></span> |<span data-ttu-id="1b382-277">Permet de définir un spout non transactionnel.</span><span class="sxs-lookup"><span data-stu-id="1b382-277">Define a nontransactional spout.</span></span> <span data-ttu-id="1b382-278">Il s’exécutera application hello avec ***exec-name*** à l’aide de ***args***.</span><span class="sxs-lookup"><span data-stu-id="1b382-278">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="1b382-279">Hello ***champs*** est les champs de sortie hello pour bec</span><span class="sxs-lookup"><span data-stu-id="1b382-279">hello ***fields*** is hello Output Fields for spout</span></span><br /><br /><span data-ttu-id="1b382-280">Hello ***paramètres*** est facultatif, à l’aide d’il toospecify certains paramètres, tels que « nontransactional.ack.enabled ».</span><span class="sxs-lookup"><span data-stu-id="1b382-280">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="1b382-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="1b382-281">**scp-bolt**</span></span> |<span data-ttu-id="1b382-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="1b382-282">exec-name</span></span><br /><span data-ttu-id="1b382-283">args</span><span class="sxs-lookup"><span data-stu-id="1b382-283">args</span></span><br /><span data-ttu-id="1b382-284">fields</span><span class="sxs-lookup"><span data-stu-id="1b382-284">fields</span></span><br /><span data-ttu-id="1b382-285">Paramètres</span><span class="sxs-lookup"><span data-stu-id="1b382-285">parameters</span></span> |<span data-ttu-id="1b382-286">Permet de définir un bolt non transactionnel.</span><span class="sxs-lookup"><span data-stu-id="1b382-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="1b382-287">Il s’exécutera application hello avec ***exec-name*** à l’aide de ***args***.</span><span class="sxs-lookup"><span data-stu-id="1b382-287">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="1b382-288">Hello ***champs*** est les champs de sortie hello pour éclair</span><span class="sxs-lookup"><span data-stu-id="1b382-288">hello ***fields*** is hello Output Fields for bolt</span></span><br /><br /><span data-ttu-id="1b382-289">Hello ***paramètres*** est facultatif, à l’aide d’il toospecify certains paramètres, tels que « nontransactional.ack.enabled ».</span><span class="sxs-lookup"><span data-stu-id="1b382-289">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="1b382-290">Les mots clés suivants sont définis pour SCP.NET :</span><span class="sxs-lookup"><span data-stu-id="1b382-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="1b382-291">**Mots clés**</span><span class="sxs-lookup"><span data-stu-id="1b382-291">**Key Words**</span></span> | <span data-ttu-id="1b382-292">**Description**</span><span class="sxs-lookup"><span data-stu-id="1b382-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="1b382-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="1b382-293">**:name**</span></span> |<span data-ttu-id="1b382-294">Définir hello nom de la topologie</span><span class="sxs-lookup"><span data-stu-id="1b382-294">Define hello Topology Name</span></span> |
| <span data-ttu-id="1b382-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="1b382-295">**:topology**</span></span> |<span data-ttu-id="1b382-296">Définir hello topologie à l’aide de hello au-dessus de fonctions et générer dans celles.</span><span class="sxs-lookup"><span data-stu-id="1b382-296">Define hello Topology using hello above functions and build in ones.</span></span> |
| <span data-ttu-id="1b382-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="1b382-297">**:p**</span></span> |<span data-ttu-id="1b382-298">Définir l’indicateur de parallélisme hello pour chaque bec ou un éclair.</span><span class="sxs-lookup"><span data-stu-id="1b382-298">Define hello parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="1b382-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="1b382-299">**:config**</span></span> |<span data-ttu-id="1b382-300">Définir configurer le paramètre ou la mise à jour hello existants</span><span class="sxs-lookup"><span data-stu-id="1b382-300">Define configure parameter or update hello existing ones</span></span> |
| <span data-ttu-id="1b382-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="1b382-301">**:schema**</span></span> |<span data-ttu-id="1b382-302">Définissez hello schéma de flux de données.</span><span class="sxs-lookup"><span data-stu-id="1b382-302">Define hello Schema of Stream.</span></span> |

<span data-ttu-id="1b382-303">Et voici des paramètres fréquemment utilisés :</span><span class="sxs-lookup"><span data-stu-id="1b382-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="1b382-304">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="1b382-304">**Parameter**</span></span> | <span data-ttu-id="1b382-305">**Description**</span><span class="sxs-lookup"><span data-stu-id="1b382-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="1b382-306">**« plugin.name »**</span><span class="sxs-lookup"><span data-stu-id="1b382-306">**"plugin.name"**</span></span> |<span data-ttu-id="1b382-307">nom de fichier exe du plug-in hello c#</span><span class="sxs-lookup"><span data-stu-id="1b382-307">exe file name of hello C# plugin</span></span> |
| <span data-ttu-id="1b382-308">**« plugin.args »**</span><span class="sxs-lookup"><span data-stu-id="1b382-308">**"plugin.args"**</span></span> |<span data-ttu-id="1b382-309">Arguments du plug-in</span><span class="sxs-lookup"><span data-stu-id="1b382-309">plugin args</span></span> |
| <span data-ttu-id="1b382-310">**« output.schema »**</span><span class="sxs-lookup"><span data-stu-id="1b382-310">**"output.schema"**</span></span> |<span data-ttu-id="1b382-311">Schéma de sortie</span><span class="sxs-lookup"><span data-stu-id="1b382-311">Output schema</span></span> |
| <span data-ttu-id="1b382-312">**« nontransactional.ack.enabled »**</span><span class="sxs-lookup"><span data-stu-id="1b382-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="1b382-313">Indique si le mécanisme d'accusé de réception (ack) est activé pour la topologie non transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="1b382-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="1b382-314">commande de runspec Hello est déployé avec les bits hello, l’utilisation de hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="1b382-314">hello runspec command will be deployed together with hello bits, hello usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="1b382-315">Hello ***ressource-dir*** paramètre est facultatif, vous devez toospecify lorsque vous souhaitez tooplug C\# application et ce répertoire contiendra application hello, les dépendances de hello et les configurations.</span><span class="sxs-lookup"><span data-stu-id="1b382-315">hello ***resource-dir*** parameter is optional, you need toospecify it when you want tooplug a C\# application, and this directory will contain hello application, hello dependencies and configurations.</span></span>

<span data-ttu-id="1b382-316">Hello ***classpath*** paramètre est également facultatif.</span><span class="sxs-lookup"><span data-stu-id="1b382-316">hello ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="1b382-317">Il est utilisé toospecify hello Java classpath fichier spec de hello contient Java bec ou éclair.</span><span class="sxs-lookup"><span data-stu-id="1b382-317">It is used toospecify hello Java classpath if hello spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="1b382-318">Fonctionnalités diverses</span><span class="sxs-lookup"><span data-stu-id="1b382-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="1b382-319">Déclaration de schéma d’entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="1b382-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="1b382-320">utilisateur de Hello peut émettre du tuple dans C\# traiter, hello plate-forme doit tooserialize hello tuple en byte [], transfert tooJava côté, et Storm transférera cette cibles toohello de tuple.</span><span class="sxs-lookup"><span data-stu-id="1b382-320">hello user can emit tuple in C\# process, hello platform needs tooserialize hello tuple into byte[], transfer tooJava side, and Storm will transfer this tuple toohello targets.</span></span> <span data-ttu-id="1b382-321">Pendant ce temps, dans le composant en aval, hello C\# processus recevra le tuple de côté de java et convertir les types d’origine toohello par plateforme, toutes ces opérations sont masquées par hello plateforme.</span><span class="sxs-lookup"><span data-stu-id="1b382-321">Meanwhile in downstream component, hello C\# process will receive tuple back from java side, and convert it toohello original types by platform, all these operations are hidden by hello Platform.</span></span>

<span data-ttu-id="1b382-322">sérialisation de hello toosupport et la désérialisation, le code utilisateur a besoin de schéma de hello toodeclare de hello entrées et sorties.</span><span class="sxs-lookup"><span data-stu-id="1b382-322">toosupport hello serialization and deserialization, user code needs toodeclare hello schema of hello inputs and outputs.</span></span>

<span data-ttu-id="1b382-323">schéma de flux de données d’entrée/sortie Hello est défini en tant que dictionnaire, clé de hello est hello StreamId et hello valeur hello des Types de colonnes de hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-323">hello input/output stream schema is defined as a dictionary, hello key is hello StreamId and hello value is hello Types of hello columns.</span></span> <span data-ttu-id="1b382-324">composant de Hello peut avoir plusieurs flux de données déclaré.</span><span class="sxs-lookup"><span data-stu-id="1b382-324">hello component can have multi-streams declared.</span></span>

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


<span data-ttu-id="1b382-325">Dans l’objet de contexte, nous avons hello ajouté des API suivante :</span><span class="sxs-lookup"><span data-stu-id="1b382-325">In Context object, we have hello following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="1b382-326">Code utilisateur doit vérifier les tuples hello émis obéissent aux règles de schéma de hello défini pour ce flux de données ou système de hello lève une exception runtime.</span><span class="sxs-lookup"><span data-stu-id="1b382-326">User code must make sure hello tuples emitted obey hello schema defined for that stream, or hello system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="1b382-327">Prise en charge multiflux</span><span class="sxs-lookup"><span data-stu-id="1b382-327">Multi-Stream Support</span></span>
<span data-ttu-id="1b382-328">SCP prend en charge utilisateur tooemit de code ou de réception à partir de plusieurs flux distincts à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="1b382-328">SCP supports user code tooemit or receive from multiple distinct streams at hello same time.</span></span> <span data-ttu-id="1b382-329">prise en charge Hello reflète dans l’objet de contexte hello hello Emit méthode prend un paramètre d’ID de flux de données facultatif.</span><span class="sxs-lookup"><span data-stu-id="1b382-329">hello support reflects in hello Context object as hello Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="1b382-330">Deux méthodes dans l’objet de contexte de SCP.NET de hello ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="1b382-330">Two methods in hello SCP.NET Context object have been added.</span></span> <span data-ttu-id="1b382-331">Ils sont utilisés tooemit Tuple ou Tuples toospecify StreamId.</span><span class="sxs-lookup"><span data-stu-id="1b382-331">They are used tooemit Tuple or Tuples toospecify StreamId.</span></span> <span data-ttu-id="1b382-332">Hello StreamId est une chaîne et doit toobe cohérents dans les deux C\# et hello les spécifications de définition de topologie.</span><span class="sxs-lookup"><span data-stu-id="1b382-332">hello StreamId is a string and it needs toobe consistent in both C\# and hello Topology Definition Spec.</span></span>

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="1b382-333">flux Hello l’émission tooa non existante entraîne des exceptions runtime.</span><span class="sxs-lookup"><span data-stu-id="1b382-333">hello emitting tooa non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="1b382-334">Regroupement de champs</span><span class="sxs-lookup"><span data-stu-id="1b382-334">Fields Grouping</span></span>
<span data-ttu-id="1b382-335">Hello build dans le regroupement des champs dans Strom ne fonctionne pas correctement dans SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="1b382-335">hello build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="1b382-336">Sur le côté du Proxy Java de hello, tous les types de données des champs hello sont réellement byte [] et champs hello regroupement utilise le regroupement de hello tooperform objet hachage code hello byte [].</span><span class="sxs-lookup"><span data-stu-id="1b382-336">On hello Java Proxy side, all hello fields data types are actually byte[], and hello fields grouping uses hello byte[] object hash code tooperform hello grouping.</span></span> <span data-ttu-id="1b382-337">code de hachage de l’objet de Hello byte [] est l’adresse hello de cet objet en mémoire.</span><span class="sxs-lookup"><span data-stu-id="1b382-337">hello byte[] object hash code is hello address of this object in memory.</span></span> <span data-ttu-id="1b382-338">Regroupement de hello est donc incorrect pour deux octets [] objets que hello partage même contenu, mais pas hello même adresse.</span><span class="sxs-lookup"><span data-stu-id="1b382-338">So hello grouping will be wrong for two byte[] objects that share hello same content but not hello same address.</span></span>

<span data-ttu-id="1b382-339">SCP.NET ajoute une méthode de regroupement personnalisées, et il utilisera le contenu hello de regroupement de hello toodo hello byte [].</span><span class="sxs-lookup"><span data-stu-id="1b382-339">SCP.NET adds a customized grouping method, and it will use hello content of hello byte[] toodo hello grouping.</span></span> <span data-ttu-id="1b382-340">Dans **SPEC** fichier, syntaxe de hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="1b382-340">In **SPEC** file, hello syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="1b382-341">Ici,</span><span class="sxs-lookup"><span data-stu-id="1b382-341">Here,</span></span>

1. <span data-ttu-id="1b382-342">« scp-field-group » signifie « Regroupement de champs personnalisé implémenté par SCP ».</span><span class="sxs-lookup"><span data-stu-id="1b382-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="1b382-343">« :tx » ou « :non-tx » signifie qu’il s’agit d’une topologie transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="1b382-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="1b382-344">Nous avons besoin de ces informations depuis hello index de début est différent dans tx et non-tx topologies.</span><span class="sxs-lookup"><span data-stu-id="1b382-344">We need this information since hello starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="1b382-345">[0,1] représente un hashset d'ID de champ, commençant à 0.</span><span class="sxs-lookup"><span data-stu-id="1b382-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="1b382-346">Topologie hybride</span><span class="sxs-lookup"><span data-stu-id="1b382-346">Hybrid topology</span></span>
<span data-ttu-id="1b382-347">Hello que Storm native est écrite en langage Java.</span><span class="sxs-lookup"><span data-stu-id="1b382-347">hello native Storm is written in Java.</span></span> <span data-ttu-id="1b382-348">Et SCP.Net il bénéficie tooenable notre toowrite douane C\# code toohandle leur logique métier.</span><span class="sxs-lookup"><span data-stu-id="1b382-348">And SCP.Net has enhanced it tooenable our customs toowrite C\# code toohandle their business logic.</span></span> <span data-ttu-id="1b382-349">Mais nous prenons également en charge les topologies hybrides, qui contiennent des spouts/bolts C\#, ainsi que des spouts/bolts Java.</span><span class="sxs-lookup"><span data-stu-id="1b382-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="1b382-350">Indiquer le spout/bolt Java dans le fichier spec</span><span class="sxs-lookup"><span data-stu-id="1b382-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="1b382-351">Dans le fichier spec, « scp-bec » et « scp-éclair » peuvent également être utilisé toospecify becs verseurs amovibles de Java et boulons, Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="1b382-351">In spec file, "scp-spout" and "scp-bolt" can also be used toospecify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="1b382-352">Ici `microsoft.scp.example.HybridTopology.Generator` hello désigne hello Java bec de classe.</span><span class="sxs-lookup"><span data-stu-id="1b382-352">Here `microsoft.scp.example.HybridTopology.Generator` is hello name of hello Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="1b382-353">Spécifier le chemin d’accès des classes Java dans une commande runSpec</span><span class="sxs-lookup"><span data-stu-id="1b382-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="1b382-354">Si vous souhaitez topologie toosubmit contenant Java becs verseurs amovibles ou boulons, vous devez les hello de compilation toofirst Java becs verseurs amovibles ou boulons et obtenez les fichiers Jar hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-354">If you want toosubmit topology containing Java Spouts or Bolts, you need toofirst compile hello Java Spouts or Bolts and get hello Jar files.</span></span> <span data-ttu-id="1b382-355">Vous devez spécifier classpath java hello qui contient les fichiers Jar hello lors de la soumission de topologie.</span><span class="sxs-lookup"><span data-stu-id="1b382-355">Then you should specify hello java classpath that contains hello Jar files when submitting topology.</span></span> <span data-ttu-id="1b382-356">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="1b382-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="1b382-357">Ici **exemples\\HybridTopology\\java\\cible\\**  est le dossier de hello contenant fichier Jar de Java bec/éclair de hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-357">Here **examples\\HybridTopology\\java\\target\\** is hello folder containing hello Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="1b382-358">Sérialisation et désérialisation entre Java et C\\</span><span class="sxs-lookup"><span data-stu-id="1b382-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="1b382-359">Notre composant SCP a un côté Java et un côté C\#.</span><span class="sxs-lookup"><span data-stu-id="1b382-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="1b382-360">Dans l’ordre toointeract avec natives Java becs verseurs/boulons, la sérialisation/désérialisation doivent être effectuée entre le côté de Java et C\# côté, comme illustré dans hello suivant du graphique.</span><span class="sxs-lookup"><span data-stu-id="1b382-360">In order toointeract with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in hello following graph.</span></span>

![diagramme de composant java envoi composant tooSCP envoi tooJava composant](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="1b382-362">**Sérialisation côté Java et désérialisation côté C\#**</span><span class="sxs-lookup"><span data-stu-id="1b382-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="1b382-363">Tout d’abord, nous fournissons une implémentation par défaut pour la sérialisation côté Java et la désérialisation côté C\#.</span><span class="sxs-lookup"><span data-stu-id="1b382-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="1b382-364">méthode de sérialisation de Hello côté de Java peut être spécifiée dans le fichier SPEC :</span><span class="sxs-lookup"><span data-stu-id="1b382-364">hello serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="1b382-365">Hello méthode de désérialisation dans C\# côté doit être spécifié en C\# code utilisateur :</span><span class="sxs-lookup"><span data-stu-id="1b382-365">hello deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="1b382-366">Cette implémentation par défaut doit gérer la plupart des cas si le type de données hello n’est pas trop complexe.</span><span class="sxs-lookup"><span data-stu-id="1b382-366">This default implementation should handle most cases if hello data type is not too complex.</span></span> <span data-ttu-id="1b382-367">Dans certains cas, soit, car hello type de données utilisateur est trop complexe ou hello performances de notre implémentation par défaut ne répond pas aux hello spécification de l’utilisateur, plug-in d’utilisateur peuvent leur propre implémentation.</span><span class="sxs-lookup"><span data-stu-id="1b382-367">For certain cases, either because hello user data type is too complex, or because hello performance of our default implementation does not meet hello user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="1b382-368">Hello de sérialiser l’interface Java côté est défini en tant que :</span><span class="sxs-lookup"><span data-stu-id="1b382-368">hello serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="1b382-369">Hello désérialiser interface en C\# côté est défini en tant que :</span><span class="sxs-lookup"><span data-stu-id="1b382-369">hello deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="1b382-370">public interface ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="1b382-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="1b382-371">**Sérialisation côté C\# et désérialisation côte Java**</span><span class="sxs-lookup"><span data-stu-id="1b382-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="1b382-372">Hello la méthode de sérialisation dans C\# côté doit être spécifié en C\# code utilisateur :</span><span class="sxs-lookup"><span data-stu-id="1b382-372">hello serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="1b382-373">Hello, méthode de désérialisation du côté Java doit être spécifié dans le fichier SPEC :</span><span class="sxs-lookup"><span data-stu-id="1b382-373">hello Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="1b382-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="1b382-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="1b382-375">Nom hello de désérialiseur est « microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer » et « microsoft.scp.example.HybridTopology.Person » est que les données de salutation de classe cible hello sont désérialisées en.</span><span class="sxs-lookup"><span data-stu-id="1b382-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is hello name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is hello target class hello data is deserialized to.</span></span>
   
   <span data-ttu-id="1b382-376">L’utilisateur peut également appliquer sa propre implémentation du sérialiseur C\# et du désérialiseur Java.</span><span class="sxs-lookup"><span data-stu-id="1b382-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="1b382-377">Il s’agit d’interface hello pour C\# sérialiseur :</span><span class="sxs-lookup"><span data-stu-id="1b382-377">This is hello interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="1b382-378">Il s’agit d’interface hello pour Java désérialiseur :</span><span class="sxs-lookup"><span data-stu-id="1b382-378">This is hello interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="1b382-379">Mode d’hébergement SCP</span><span class="sxs-lookup"><span data-stu-id="1b382-379">SCP Host Mode</span></span>
<span data-ttu-id="1b382-380">Dans ce mode, utilisateur peut compiler leur tooDLL de codes et utiliser SCPHost.exe fournie par la topologie de toosubmit SCP.</span><span class="sxs-lookup"><span data-stu-id="1b382-380">In this mode, user can compile their codes tooDLL, and use SCPHost.exe provided by SCP toosubmit topology.</span></span> <span data-ttu-id="1b382-381">fichier de spécification de Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="1b382-381">hello spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="1b382-382">Ici, `plugin.name` est spécifié en tant que `SCPHost.exe` fourni par le Kit de développement logiciel (SDK) SCP.</span><span class="sxs-lookup"><span data-stu-id="1b382-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="1b382-383">SCPHost.exe accepte exactement trois paramètres :</span><span class="sxs-lookup"><span data-stu-id="1b382-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="1b382-384">Bonjour tout d’abord une est hello nom de la DLL, qui est `"HelloWorld.dll"` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="1b382-384">hello first one is hello DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="1b382-385">deuxième Hello est hello nom de la classe, qui est `"Scp.App.HelloWorld.Generator"` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="1b382-385">hello second one is hello Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="1b382-386">Hello troisième un est hello nom d’une méthode statique publique, qui peut être appelée tooget une instance de ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="1b382-386">hello third one is hello name of a public static method, which can be invoked tooget an instance of ISCPPlugin.</span></span>

<span data-ttu-id="1b382-387">En mode d'hébergement, le code utilisateur est compilé en tant que DLL, puis appelé par la plateforme SCP.</span><span class="sxs-lookup"><span data-stu-id="1b382-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="1b382-388">Par conséquent plateforme de SCP peut obtenir un contrôle total de la logique de traitement entier hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-388">So SCP platform can get full control of hello whole processing logic.</span></span> <span data-ttu-id="1b382-389">Nous vous recommandons de nos clients topologie toosubmit en mode d’hôte SCP, car elle peut simplifier l’expérience de développement hello et nous apporter plus de souplesse et une meilleure compatibilité descendante pour une version ultérieure ainsi.</span><span class="sxs-lookup"><span data-stu-id="1b382-389">So we recommend our customers toosubmit topology in SCP host mode since it can simplify hello development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="1b382-390">Exemples de programmation SCP</span><span class="sxs-lookup"><span data-stu-id="1b382-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="1b382-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="1b382-391">HelloWorld</span></span>
<span data-ttu-id="1b382-392">**HelloWorld** est un exemple très simple de tooshow un aperçu de SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="1b382-392">**HelloWorld** is a very simple example tooshow a taste of SCP.Net.</span></span> <span data-ttu-id="1b382-393">Il emploie une topologie non transactionnelle, avec un spout appelé **generator**, et deux bolts appelés **splitter** et **counter**.</span><span class="sxs-lookup"><span data-stu-id="1b382-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="1b382-394">bec de Hello **Générateur** aléatoire génère des phrases et l’émettre ces phrases trop**fractionnement**.</span><span class="sxs-lookup"><span data-stu-id="1b382-394">hello spout **generator** will randomly generate some sentences, and emit these sentences too**splitter**.</span></span> <span data-ttu-id="1b382-395">éclair de Hello **fractionnement** sera fractionnée hello phrases toowords et émettre ces mots trop**compteur** éclair.</span><span class="sxs-lookup"><span data-stu-id="1b382-395">hello bolt **splitter** will split hello sentences toowords and emit these words too**counter** bolt.</span></span> <span data-ttu-id="1b382-396">Hello éclair « counter » utilise un numéro d’occurrence dictionnaire toorecord hello de chaque mot.</span><span class="sxs-lookup"><span data-stu-id="1b382-396">hello bolt "counter" uses a dictionary toorecord hello occurrence number of each word.</span></span>

<span data-ttu-id="1b382-397">L’exemple contient deux fichiers spec, **HelloWorld.spec** et **HelloWorld\_EnableAck.spec**.</span><span class="sxs-lookup"><span data-stu-id="1b382-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="1b382-398">Bonjour C\# code, peuvent se trouver si l’accusé de réception est activé en obtenant hello pluginConf du côté de Java.</span><span class="sxs-lookup"><span data-stu-id="1b382-398">In hello C\# code, it can find out whether ack is enabled by getting hello pluginConf from Java side.</span></span>

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="1b382-399">Dans un bec hello, si l’accusé de réception est activé, un dictionnaire est utilisé toocache hello tuples qui n’ont pas été reçu.</span><span class="sxs-lookup"><span data-stu-id="1b382-399">In hello spout, if ack is enabled, a dictionary is used toocache hello tuples that have not been acked.</span></span> <span data-ttu-id="1b382-400">Si Fail() est appelée, hello tuple ayant échoué doit être réexécutée :</span><span class="sxs-lookup"><span data-stu-id="1b382-400">If Fail() is called, hello failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="1b382-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="1b382-401">HelloWorldTx</span></span>
<span data-ttu-id="1b382-402">Hello **HelloWorldTx** exemple illustre la topologie de transactionnelle tooimplement.</span><span class="sxs-lookup"><span data-stu-id="1b382-402">hello **HelloWorldTx** example demonstrates how tooimplement transactional topology.</span></span> <span data-ttu-id="1b382-403">Il contient un spout nommé **generator**, un bolt par lots nommé **partial-count** et un bolt de validation nommé **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="1b382-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="1b382-404">Il contient également trois fichiers txt : **DataSource0.txt**, **DataSource1.txt** et **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="1b382-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="1b382-405">Lors de chaque transaction, hello bec **Générateur** sera de façon aléatoire choisissez deux fichiers hello trois fichiers créé au préalable et émettre hello deux fichiers noms toohello **partielle-count** éclair.</span><span class="sxs-lookup"><span data-stu-id="1b382-405">In each transaction, hello spout **generator** will randomly choose two files from hello pre-created three files, and emit hello two file names toohello **partial-count** bolt.</span></span> <span data-ttu-id="1b382-406">éclair de Hello **partielle-count** sera tout d’abord obtenir un nom de fichier hello du tuple de salutation reçue, puis numéro de hello hello Ouvrir fichier et le nombre de mots dans ce fichier et enfin émettre toohello numéro du mot hello **somme-**éclair.</span><span class="sxs-lookup"><span data-stu-id="1b382-406">hello bolt **partial-count** will first get hello file name from hello received tuple, then open hello file and count hello number of words in this file, and finally emit hello word number toohello **count-sum** bolt.</span></span> <span data-ttu-id="1b382-407">Hello **-somme** éclair résume le nombre total de hello.</span><span class="sxs-lookup"><span data-stu-id="1b382-407">hello **count-sum** bolt will summarize hello total count.</span></span>

<span data-ttu-id="1b382-408">tooachieve **exactement une fois** sémantique, éclair de validation hello **-somme** devez toojudge s’il s’agit d’une transaction relue.</span><span class="sxs-lookup"><span data-stu-id="1b382-408">tooachieve **exactly once** semantics, hello commit bolt **count-sum** need toojudge whether it is a replayed transaction.</span></span> <span data-ttu-id="1b382-409">Dans cet exemple, il est doté d'une variable de membre statique :</span><span class="sxs-lookup"><span data-stu-id="1b382-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="1b382-410">Lorsqu’une instance de ISCPBatchBolt est créée, elle obtiendra hello `txAttempt` à partir des paramètres d’entrée :</span><span class="sxs-lookup"><span data-stu-id="1b382-410">When an ISCPBatchBolt instance is created, it will get hello `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

<span data-ttu-id="1b382-411">Lorsque `FinishBatch()` est appelée, hello `lastCommittedTxId` sera mise à jour si elle n’est pas une transaction relue.</span><span class="sxs-lookup"><span data-stu-id="1b382-411">When `FinishBatch()` is called, hello `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="1b382-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="1b382-412">HybridTopology</span></span>
<span data-ttu-id="1b382-413">Cette topologie contient un spout Java et un bolt C\#.</span><span class="sxs-lookup"><span data-stu-id="1b382-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="1b382-414">Il utilise hello par défaut sérialisation et désérialisation implémentation fournie par la plateforme de SCP.</span><span class="sxs-lookup"><span data-stu-id="1b382-414">It uses hello default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="1b382-415">Veuillez hello de ref **HybridTopology.spec** dans **exemples\\HybridTopology** dossier hello spec les données de fichier, et **SubmitTopology.bat** de procédure toospecify Java classpath.</span><span class="sxs-lookup"><span data-stu-id="1b382-415">Please ref hello **HybridTopology.spec** in **examples\\HybridTopology** folder for hello spec file details, and **SubmitTopology.bat** for how toospecify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="1b382-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="1b382-416">SCPHostDemo</span></span>
<span data-ttu-id="1b382-417">Cet exemple est fondamentalement hello identique HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="1b382-417">This example is hello same as HelloWorld in essence.</span></span> <span data-ttu-id="1b382-418">Hello seule différence est que le code utilisateur hello est compilé en tant que DLL et topologie de hello est envoyé à l’aide de SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="1b382-418">hello only difference is that hello user code is compiled as DLL and hello topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="1b382-419">Veuillez section de hello ref « Mode de hôte SCP » pour une explication plus détaillée.</span><span class="sxs-lookup"><span data-stu-id="1b382-419">Please ref hello section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b382-420">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1b382-420">Next Steps</span></span>
<span data-ttu-id="1b382-421">Pour obtenir des exemples de topologies Storm créés à l’aide de SCP, voir hello :</span><span class="sxs-lookup"><span data-stu-id="1b382-421">For examples of Storm topologies created using SCP, see hello following:</span></span>

* [<span data-ttu-id="1b382-422">Développement de topologies C# pour Apache Storm dans HDInsight à l'aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1b382-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="1b382-423">Traitement d'événements à partir d'Azure Event Hubs avec Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="1b382-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="1b382-424">Création de plusieurs flux de données dans une topologie C# Storm</span><span class="sxs-lookup"><span data-stu-id="1b382-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="1b382-425">Utiliser les données de toovisualize Power Bi à partir d’une topologie Storm</span><span class="sxs-lookup"><span data-stu-id="1b382-425">Use Power Bi toovisualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="1b382-426">Traitement des données de capteur de véhicule à partir d'Event Hubs à l'aide de Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="1b382-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="1b382-427">Extraction, transformation et chargement (ETL) à partir d’Azure Event Hubs tooHBase</span><span class="sxs-lookup"><span data-stu-id="1b382-427">Extract, Transform, and Load (ETL) from Azure Event Hubs tooHBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="1b382-428">Corrélation des événements à l’aide de Storm et HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="1b382-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

