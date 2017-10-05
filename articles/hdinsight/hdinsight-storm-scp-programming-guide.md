---
title: Guide de programmation SCP.NET | Microsoft Docs
description: "Découvrez comment utiliser SCP.NET pour créer des topologies Storm basées sur .NET en vue d’une utilisation avec Storm sur HDInsight."
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
ms.openlocfilehash: 3d76aebd2a1fd729c8e0639e6afcbde4c3fb752b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="13657-103">Guide de programmation SCP</span><span class="sxs-lookup"><span data-stu-id="13657-103">SCP programming guide</span></span>
<span data-ttu-id="13657-104">SCP est une plateforme permettant de développer des applications de traitement de données en temps réel, fiables, cohérentes et aux performances élevées.</span><span class="sxs-lookup"><span data-stu-id="13657-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="13657-105">Elle est basée sur [Apache Storm](http://storm.incubator.apache.org/) , système de traitement par flux conçu par la communauté OSS.</span><span class="sxs-lookup"><span data-stu-id="13657-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="13657-106">Storm est conçu par Nathan Marz et diffusé en open source par Twitter.</span><span class="sxs-lookup"><span data-stu-id="13657-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="13657-107">Il exploite [Apache ZooKeeper](http://zookeeper.apache.org/), un autre projet Apache pour fournir une coordination et une gestion d’état très fiables.</span><span class="sxs-lookup"><span data-stu-id="13657-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="13657-108">Le projet SCP ne se contente pas de faire migrer Storm sur Windows : il permet également d'étendre et de personnaliser l'écosystème Windows.</span><span class="sxs-lookup"><span data-stu-id="13657-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="13657-109">Ses extensions améliorent l’expérience des développeurs .NET et les bibliothèques, tandis que sa capacité de personnalisation permet un déploiement basé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="13657-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="13657-110">Grâce à ces capacités d'extension et de personnalisation, vous n'aurez pas à répliquer vos projets OSS tout en tirant partie des écosystèmes dérivés basés sur Storm.</span><span class="sxs-lookup"><span data-stu-id="13657-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="13657-111">Modèle de traitement</span><span class="sxs-lookup"><span data-stu-id="13657-111">Processing model</span></span>
<span data-ttu-id="13657-112">Les données de SCP sont modélisées en tant que flux de tuples continus.</span><span class="sxs-lookup"><span data-stu-id="13657-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="13657-113">Généralement, les tuples sont d'abord diffusés en file d'attente, puis récupérés et transformés par une logique métier dans une topologie Storm. Puis le résultat peut être redirigé en tant que tuples vers un autre système SCP ou être validés pour des magasins tels qu'un système de fichiers distribués ou des bases de données comme SQL Server.</span><span class="sxs-lookup"><span data-stu-id="13657-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![Diagramme d’une file d’attente fournissant des données à traiter, destinées à une banque de données](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="13657-115">Dans Storm, une topologie d'application définit un graphique de calcul.</span><span class="sxs-lookup"><span data-stu-id="13657-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="13657-116">Chaque nœud d'une topologie contient une logique de traitement et les liens entre ces nœuds indiquent les flux de données.</span><span class="sxs-lookup"><span data-stu-id="13657-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="13657-117">Les nœuds permettant d'injecter des données d'entrée dans la topologie sont nommés des « Spouts ». Ils permettent de séquencer les données.</span><span class="sxs-lookup"><span data-stu-id="13657-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="13657-118">Les données d’entrée peuvent résider dans des fichiers journaux, une base de données transactionnelle, un compteur de performances système, etc. Les nœuds avec à la fois des flux de données d’entrée et de sortie sont appelés bolts ; ces derniers assurent les opérations de filtrage et de sélection des données, ainsi que d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="13657-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="13657-119">SCP prend en charge les types de traitement de données Meilleur effort, Une fois au minimum et Exactement une.</span><span class="sxs-lookup"><span data-stu-id="13657-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="13657-120">Dans une application distribuée de traitement de diffusion en continu, diverses erreurs peuvent se produire pendant le traitement des données, telles qu’une erreur de code utilisateur, la défaillance d’un ordinateur ou une panne du réseau. Le type de traitement Une fois au minimum garantit que toutes les données sont traitées au moins une fois en relisant automatiquement les mêmes données quand une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="13657-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="13657-121">Le type de traitement Une fois au minimum est simple et fiable et s'adapte à de nombreuses applications.</span><span class="sxs-lookup"><span data-stu-id="13657-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="13657-122">Cependant, lorsqu'une application requiert un comptage exact, le traitement Une fois au minimum n'est pas suffisant, car les mêmes données peuvent potentiellement être lues dans la topologie de l'application.</span><span class="sxs-lookup"><span data-stu-id="13657-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="13657-123">Dans ce cas, le type de traitement Exactement une est conçu pour garantir l'exactitude du résultat, même lorsque les données peuvent être relues et traitées plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="13657-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="13657-124">SCP permet aux développeurs .NET de développer des applications de traitement de données en temps réel tout en exploitant le projet Storm basé sur JVM (Java Virtual Machine).</span><span class="sxs-lookup"><span data-stu-id="13657-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="13657-125">.NET et JVM communiquent via un socket local TCP.</span><span class="sxs-lookup"><span data-stu-id="13657-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="13657-126">Fondamentalement, chaque Spout/Bolt constitue une paire de processus .Net/Java, où la logique utilisateur s'exécute dans un processus .Net en tant que plug-in.</span><span class="sxs-lookup"><span data-stu-id="13657-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="13657-127">Pour générer une application de traitement de données sur SCP, vous devez suivre plusieurs étapes :</span><span class="sxs-lookup"><span data-stu-id="13657-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="13657-128">Concevez et implémentez les Spouts pour intégrer des données en file d'attente.</span><span class="sxs-lookup"><span data-stu-id="13657-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="13657-129">Concevez et implémentez des Bolts pour traiter les données d'entrée, puis enregistrez les données vers des magasins externes tels que des bases de données.</span><span class="sxs-lookup"><span data-stu-id="13657-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="13657-130">Concevez la topologie, puis validez-la et exécutez-la.</span><span class="sxs-lookup"><span data-stu-id="13657-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="13657-131">La topologie définit les points et les flux de données entre ces points.</span><span class="sxs-lookup"><span data-stu-id="13657-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="13657-132">SCP récupère alors la spécification de la topologie et la déploie dans un cluster Storm, où chaque point est exécuté sur un nœud logique.</span><span class="sxs-lookup"><span data-stu-id="13657-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="13657-133">Le planificateur de tâches de Storm s'occupe du basculement et de la mise à l'échelle.</span><span class="sxs-lookup"><span data-stu-id="13657-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="13657-134">Ce document présente quelques exemples pour illustrer le développement d'applications de traitement des données avec SCP.</span><span class="sxs-lookup"><span data-stu-id="13657-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="13657-135">Interface de plug-in SCP</span><span class="sxs-lookup"><span data-stu-id="13657-135">SCP Plugin Interface</span></span>
<span data-ttu-id="13657-136">Les plug-ins (ou applications) SCP sont des exécutables (.EXE) autonomes que vous pouvez exécuter dans Visual Studio durant le développement, puis brancher sur le pipeline Storm après le déploiement dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="13657-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="13657-137">L'écriture d'un plug-in SCP est identique à celle de n'importe quelle application console Windows standard.</span><span class="sxs-lookup"><span data-stu-id="13657-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="13657-138">La plateforme SCP.NET déclare certaines interfaces pour spout/bolt, et le code du plug-in utilisateur doit implémenter ces interfaces.</span><span class="sxs-lookup"><span data-stu-id="13657-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="13657-139">L'objectif principal de cette conception est de permettre à l'utilisateur de se concentrer sur ses propres logiques métier, en laissant la plateforme SCP.NET s'occuper du reste.</span><span class="sxs-lookup"><span data-stu-id="13657-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="13657-140">Le code du plug-in utilisateur doit implémenter l'une des interfaces suivantes, selon que la topologie soit transactionnelle ou non, et que le composant soit spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="13657-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="13657-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="13657-141">ISCPSpout</span></span>
* <span data-ttu-id="13657-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="13657-142">ISCPBolt</span></span>
* <span data-ttu-id="13657-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="13657-143">ISCPTxSpout</span></span>
* <span data-ttu-id="13657-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="13657-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="13657-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="13657-145">ISCPPlugin</span></span>
<span data-ttu-id="13657-146">ISCPPlugin est l'interface la plus répandue pour tous les types de plug-in.</span><span class="sxs-lookup"><span data-stu-id="13657-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="13657-147">Actuellement, c'est une interface factice.</span><span class="sxs-lookup"><span data-stu-id="13657-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="13657-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="13657-148">ISCPSpout</span></span>
<span data-ttu-id="13657-149">ISCPSpout est l'interface pour les composants spout non transactionnels.</span><span class="sxs-lookup"><span data-stu-id="13657-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="13657-150">Quand `NextTuple()` est appelé, le code utilisateur C\# peut émettre un ou plusieurs tuples.</span><span class="sxs-lookup"><span data-stu-id="13657-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="13657-151">S'il n'y a rien à émettre, cette méthode doit effectuer un renvoi sans émettre quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="13657-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="13657-152">Notez que `NextTuple()`, `Ack()` et `Fail()` sont toutes appelées dans une boucle étroite d’un thread unique dans un processus C\#.</span><span class="sxs-lookup"><span data-stu-id="13657-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="13657-153">Quand il n'y a aucun tuple à émettre, il est recommandé de mettre NextTuple en veille pour un bref instant (10 millisecondes par exemple) pour ne pas gaspiller trop de ressources processeur.</span><span class="sxs-lookup"><span data-stu-id="13657-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="13657-154">`Ack()` et `Fail()` sont appelées uniquement quand le mécanisme d’accusé de réception (ack) est activé dans le fichier spec.</span><span class="sxs-lookup"><span data-stu-id="13657-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="13657-155">`seqId` est utilisé pour identifier le tuple qui a été reçu ou qui a échoué.</span><span class="sxs-lookup"><span data-stu-id="13657-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="13657-156">Donc, si l'accusé de réception est activé dans une topologie non transactionnelle, la fonction d'émission suivante doit être utilisée dans Spout :</span><span class="sxs-lookup"><span data-stu-id="13657-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="13657-157">Si l’accusé de réception n’est pas pris en charge dans une topologie non transactionnelle, les fonctions `Ack()` et `Fail()` peuvent être laissées vides.</span><span class="sxs-lookup"><span data-stu-id="13657-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="13657-158">Les paramètres d’entrée `parms` de ces fonctions correspondent simplement à un Dictionnaire vide, ils seront utilisés plus tard.</span><span class="sxs-lookup"><span data-stu-id="13657-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="13657-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="13657-159">ISCPBolt</span></span>
<span data-ttu-id="13657-160">ISCPBolt est l'interface pour les composants bolt non transactionnels.</span><span class="sxs-lookup"><span data-stu-id="13657-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="13657-161">Quand un nouveau tuple est disponible, la fonction `Execute()` est appelée pour son traitement.</span><span class="sxs-lookup"><span data-stu-id="13657-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="13657-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="13657-162">ISCPTxSpout</span></span>
<span data-ttu-id="13657-163">ISCPTxSpout est l'interface pour les composants spout transactionnels.</span><span class="sxs-lookup"><span data-stu-id="13657-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="13657-164">Tout comme leurs équivalentes non-transactionnelles, les fonctions `NextTx()`, `Ack()` et `Fail()` sont toutes appelées dans une boucle étroite d’un thread unique dans un processus C\#.</span><span class="sxs-lookup"><span data-stu-id="13657-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="13657-165">Quand il n’y a aucune donnée à émettre, il est recommandé de mettre `NextTx` en veille pour un bref instant (10 millisecondes par exemple) pour ne pas gaspiller trop de ressources processeur.</span><span class="sxs-lookup"><span data-stu-id="13657-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="13657-166">`NextTx()` est appelée pour démarrer une nouvelle transaction, le paramètre de sortie `seqId` est utilisé pour identifier la transaction, qui est également utilisée dans les fonctions `Ack()` et `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="13657-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="13657-167">Dans `NextTx()`, l’utilisateur peut émettre des données vers le côté Java.</span><span class="sxs-lookup"><span data-stu-id="13657-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="13657-168">Les données seront stockées dans ZooKeeper pour prendre en charge la relecture.</span><span class="sxs-lookup"><span data-stu-id="13657-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="13657-169">Comme la capacité de ZooKeeper est très limitée, l'utilisateur doit seulement émettre des métadonnées, et non pas des données en bloc dans un spout transactionnel.</span><span class="sxs-lookup"><span data-stu-id="13657-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="13657-170">Si une transaction échoue, Storm la relit automatiquement. Il ne faut donc pas appeler la fonction `Fail()` dans un cas normal.</span><span class="sxs-lookup"><span data-stu-id="13657-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="13657-171">Mais si SCP peut contrôler les métadonnées émises par un spout transactionnel, il peut appeler la fonction `Fail()` quand les métadonnées ne sont pas correctes.</span><span class="sxs-lookup"><span data-stu-id="13657-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="13657-172">Les paramètres d’entrée `parms` de ces fonctions correspondent simplement à un Dictionnaire vide, ils seront utilisés plus tard.</span><span class="sxs-lookup"><span data-stu-id="13657-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="13657-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="13657-173">ISCPBatchBolt</span></span>
<span data-ttu-id="13657-174">ISCPBatchBolt est l'interface pour les composants bolt transactionnels.</span><span class="sxs-lookup"><span data-stu-id="13657-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="13657-175">`Execute()` est appelé quand un nouveau tuple arrive sur le bolt.</span><span class="sxs-lookup"><span data-stu-id="13657-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="13657-176">`FinishBatch()` est appelé quand cette transaction est terminée.</span><span class="sxs-lookup"><span data-stu-id="13657-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="13657-177">Le paramètre d’entrée `parms` est réservé à un usage futur.</span><span class="sxs-lookup"><span data-stu-id="13657-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="13657-178">Il existe un concept important pour la topologie transactionnelle : `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="13657-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="13657-179">Il comporte deux champs : `TxId` et `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="13657-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="13657-180">`TxId` est utilisé pour identifier une transaction spécifique. Si une transaction donnée échoue et est relue, il peut y avoir plusieurs tentatives.</span><span class="sxs-lookup"><span data-stu-id="13657-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="13657-181">SCP.NET va créer un objet ISCPBatchBolt différent pour traiter chaque `StormTxAttempt`, tout comme le ferait Storm côté Java.</span><span class="sxs-lookup"><span data-stu-id="13657-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="13657-182">Cette conception permet de prendre en charge le traitement des transactions parallèles.</span><span class="sxs-lookup"><span data-stu-id="13657-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="13657-183">L'utilisateur ne doit pas oublier que si la tentative de transaction est terminée, l'objet ISCPBatchBolt correspondant sera détruit et récupéré par le garbage collector.</span><span class="sxs-lookup"><span data-stu-id="13657-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="13657-184">Modèle objet</span><span class="sxs-lookup"><span data-stu-id="13657-184">Object Model</span></span>
<span data-ttu-id="13657-185">SCP.NET fournit également un ensemble d'objets clés pour les développeurs.</span><span class="sxs-lookup"><span data-stu-id="13657-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="13657-186">Il s’agit des objets **Context**, **StateStore** et **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="13657-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="13657-187">Ils seront présentés dans la suite de cette section.</span><span class="sxs-lookup"><span data-stu-id="13657-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="13657-188">Context</span><span class="sxs-lookup"><span data-stu-id="13657-188">Context</span></span>
<span data-ttu-id="13657-189">L'objet Context fournit un environnement d'exécution pour l'application.</span><span class="sxs-lookup"><span data-stu-id="13657-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="13657-190">Chaque instance ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) dispose d'une instance Context correspondante.</span><span class="sxs-lookup"><span data-stu-id="13657-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="13657-191">La fonctionnalité fournie par un objet Context peut être divisée en deux : (1) une partie statique qui est disponible dans l’ensemble du processus C\#, (2) une partie dynamique qui est uniquement disponible pour l’instance Context spécifique.</span><span class="sxs-lookup"><span data-stu-id="13657-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="13657-192">Partie statique</span><span class="sxs-lookup"><span data-stu-id="13657-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="13657-193">`Logger` est fourni à des fins de journalisation.</span><span class="sxs-lookup"><span data-stu-id="13657-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="13657-194">`pluginType` permet d’indiquer le type de plug-in du processus C\#.</span><span class="sxs-lookup"><span data-stu-id="13657-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="13657-195">Si le processus C\# est exécuté dans un mode de test local (sans Java), le type de plug-in est `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="13657-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="13657-196">`Config` est fourni pour obtenir des paramètres de configuration côté Java.</span><span class="sxs-lookup"><span data-stu-id="13657-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="13657-197">Les paramètres sont transférés à partir du côté Java lors de l’initialisation du plug-in C\#.</span><span class="sxs-lookup"><span data-stu-id="13657-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="13657-198">Les paramètres `Config` sont divisés en deux parties : `stormConf` et `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="13657-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="13657-199">`stormConf` correspond aux paramètres définis par Storm, tandis que `pluginConf` correspond aux paramètres définis par SCP.</span><span class="sxs-lookup"><span data-stu-id="13657-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="13657-200">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="13657-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="13657-201">`TopologyContext` est fourni pour obtenir le contexte de topologie et est plus utile pour les composants dotés de plusieurs parallélismes.</span><span class="sxs-lookup"><span data-stu-id="13657-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="13657-202">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="13657-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
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

### <a name="dynamic-part"></a><span data-ttu-id="13657-203">Partie dynamique</span><span class="sxs-lookup"><span data-stu-id="13657-203">Dynamic Part</span></span>
<span data-ttu-id="13657-204">Les interfaces suivantes sont pertinentes pour une instance de l'objet Context bien précise.</span><span class="sxs-lookup"><span data-stu-id="13657-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="13657-205">Cette instance de l'objet Context est créée par la plateforme SCP.NET, puis transmise vers le code utilisateur :</span><span class="sxs-lookup"><span data-stu-id="13657-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="13657-206">La méthode suivante est fournie pour les spouts non transactionnels prenant en charge le mécanisme d'accusé de réception (ack) :</span><span class="sxs-lookup"><span data-stu-id="13657-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="13657-207">Dans le cas des bolts non transactionnels prenant en charge le mécanisme d’accusé de réception (ack), la fonction `Ack()` ou `Fail()` est appliquée de façon explicite au tuple reçu.</span><span class="sxs-lookup"><span data-stu-id="13657-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="13657-208">Puis, lors de l'émission d'un nouveau tuple, les signets du nouveau tuple doivent également être spécifiés.</span><span class="sxs-lookup"><span data-stu-id="13657-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="13657-209">Les méthodes suivantes sont fournies.</span><span class="sxs-lookup"><span data-stu-id="13657-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="13657-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="13657-210">StateStore</span></span>
<span data-ttu-id="13657-211">`StateStore` fournit des services de métadonnées, une génération de séquence unitone et une coordination sans attente.</span><span class="sxs-lookup"><span data-stu-id="13657-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="13657-212">Il est possible de développer des abstractions concurrentielles distribuées et globales sur `StateStore`, notamment des verrous distribués, des files d’attente distribuées, des barrières et des services de transaction.</span><span class="sxs-lookup"><span data-stu-id="13657-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="13657-213">Les applications SCP peuvent utiliser l’objet `State` pour conserver des informations dans ZooKeeper, notamment la topologie transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="13657-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="13657-214">Ainsi, si un spout transactionnel se bloque et redémarre, il peut récupérer les informations nécessaires à partir de ZooKeeper, puis redémarrer le pipeline.</span><span class="sxs-lookup"><span data-stu-id="13657-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="13657-215">L’objet `StateStore` dispose principalement de ces méthodes :</span><span class="sxs-lookup"><span data-stu-id="13657-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
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
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="13657-216">L’objet `State` dispose principalement de ces méthodes :</span><span class="sxs-lookup"><span data-stu-id="13657-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="13657-217">Dans le cas de la méthode `Commit()` , quand simpleMode est défini sur true, cela entraîne simplement la suppression du ZNode correspondant dans ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="13657-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="13657-218">Sinon, le ZNode en cours est supprimé, puis un nouveau nœud est ajouté au COMMITTED\_PATH.</span><span class="sxs-lookup"><span data-stu-id="13657-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="13657-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="13657-219">SCPRuntime</span></span>
<span data-ttu-id="13657-220">SCPRuntime fournit les deux méthodes suivantes.</span><span class="sxs-lookup"><span data-stu-id="13657-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="13657-221">`Initialize()` permet d’initialiser l’environnement de runtime de SCP.</span><span class="sxs-lookup"><span data-stu-id="13657-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="13657-222">Dans cette méthode, le processus C\# se connecte au côté Java et obtient les paramètres de configuration ainsi que le contexte de topologie.</span><span class="sxs-lookup"><span data-stu-id="13657-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="13657-223">`LaunchPlugin()` permet d’envoyer la boucle de traitement du message.</span><span class="sxs-lookup"><span data-stu-id="13657-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="13657-224">Dans cette boucle, le plug-in C\# reçoit des messages depuis le côté Java (notamment les tuples et les signaux de contrôle), puis il traite les messages, en appelant par exemple la méthode d’interface fournie par le code utilisateur.</span><span class="sxs-lookup"><span data-stu-id="13657-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="13657-225">Le paramètre d’entrée pour la méthode `LaunchPlugin()` est un délégué qui peut renvoyer un objet implémentant l’interface ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="13657-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="13657-226">Pour ISCPBatchBolt, nous pouvons obtenir `StormTxAttempt` à partir de `parms` et l’utiliser pour savoir s’il s’agit d’une tentative relue.</span><span class="sxs-lookup"><span data-stu-id="13657-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="13657-227">Ceci est généralement fait sur le bolt de validation, puis il est montré dans l’exemple `HelloWorldTx` .</span><span class="sxs-lookup"><span data-stu-id="13657-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="13657-228">De façon générale, les plug-ins peuvent s'exécuter dans les deux modes suivants :</span><span class="sxs-lookup"><span data-stu-id="13657-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="13657-229">Mode de test local : dans ce mode, les plug-ins SCP (le code utilisateur C\#) s’exécutent dans Visual Studio durant la phase de développement.</span><span class="sxs-lookup"><span data-stu-id="13657-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="13657-230">`LocalContext` dans ce mode, qui fournit une méthode pour sérialiser les tuples émis vers des fichiers locaux, puis les lire une fois qu’ils retournent à la mémoire.</span><span class="sxs-lookup"><span data-stu-id="13657-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="13657-231">Mode ordinaire : dans ce mode, les plug-ins SCP sont démarrés par un processus Java Storm.</span><span class="sxs-lookup"><span data-stu-id="13657-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="13657-232">Voici un exemple de démarrage de plug-in SCP :</span><span class="sxs-lookup"><span data-stu-id="13657-232">Here is an example of launching SCP plugin:</span></span>
   
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
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="13657-233">Langage de spécification de topologie</span><span class="sxs-lookup"><span data-stu-id="13657-233">Topology Specification Language</span></span>
<span data-ttu-id="13657-234">La spécification de topologie SCP est un langage de domaine spécifique pour décrire et configurer les topologies SCP.</span><span class="sxs-lookup"><span data-stu-id="13657-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="13657-235">Il est basé sur Clojure DSL de Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) et est étendu par SCP.</span><span class="sxs-lookup"><span data-stu-id="13657-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="13657-236">Vous pouvez envoyer directement des spécifications de topologie vers le cluster Storm pour les exécuter via la commande ***runspec***.</span><span class="sxs-lookup"><span data-stu-id="13657-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="13657-237">SCP.NET a ajouté les fonctions suivantes pour définir la topologie transactionnelle :</span><span class="sxs-lookup"><span data-stu-id="13657-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="13657-238">**Nouvelles fonctions**</span><span class="sxs-lookup"><span data-stu-id="13657-238">**New Functions**</span></span> | <span data-ttu-id="13657-239">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="13657-239">**Parameters**</span></span> | <span data-ttu-id="13657-240">**Description**</span><span class="sxs-lookup"><span data-stu-id="13657-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13657-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="13657-241">**tx-topolopy**</span></span> |<span data-ttu-id="13657-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="13657-242">topology-name</span></span><br /><span data-ttu-id="13657-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="13657-243">spout-map</span></span><br /><span data-ttu-id="13657-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="13657-244">bolt-map</span></span> |<span data-ttu-id="13657-245">Permet de définir une topologie transactionnelle avec un nom de topologie, &nbsp;une carte de définition de spouts et une carte de définition de bolts.</span><span class="sxs-lookup"><span data-stu-id="13657-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="13657-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="13657-246">**scp-tx-spout**</span></span> |<span data-ttu-id="13657-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="13657-247">exec-name</span></span><br /><span data-ttu-id="13657-248">args</span><span class="sxs-lookup"><span data-stu-id="13657-248">args</span></span><br /><span data-ttu-id="13657-249">fields</span><span class="sxs-lookup"><span data-stu-id="13657-249">fields</span></span> |<span data-ttu-id="13657-250">Permet de définir un spout transactionnel.</span><span class="sxs-lookup"><span data-stu-id="13657-250">Define a transactional spout.</span></span> <span data-ttu-id="13657-251">Exécutera l’application avec ***exec-name*** en utilisant ***args***.</span><span class="sxs-lookup"><span data-stu-id="13657-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="13657-252">***fields*** correspond aux champs de sortie du spout.</span><span class="sxs-lookup"><span data-stu-id="13657-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="13657-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="13657-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="13657-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="13657-254">exec-name</span></span><br /><span data-ttu-id="13657-255">args</span><span class="sxs-lookup"><span data-stu-id="13657-255">args</span></span><br /><span data-ttu-id="13657-256">fields</span><span class="sxs-lookup"><span data-stu-id="13657-256">fields</span></span> |<span data-ttu-id="13657-257">Permet de définir un lot bolt transactionnel.</span><span class="sxs-lookup"><span data-stu-id="13657-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="13657-258">Exécutera l’application avec ***exec-name*** en utilisant ***args.***</span><span class="sxs-lookup"><span data-stu-id="13657-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="13657-259">Le paramètre Fields correspond aux champs de sortie du bolt.</span><span class="sxs-lookup"><span data-stu-id="13657-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="13657-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="13657-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="13657-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="13657-261">exec-name</span></span><br /><span data-ttu-id="13657-262">args</span><span class="sxs-lookup"><span data-stu-id="13657-262">args</span></span><br /><span data-ttu-id="13657-263">fields</span><span class="sxs-lookup"><span data-stu-id="13657-263">fields</span></span> |<span data-ttu-id="13657-264">Permet de définir un validateur bolt transactionnel.</span><span class="sxs-lookup"><span data-stu-id="13657-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="13657-265">Exécutera l’application avec ***exec-name*** en utilisant ***args***.</span><span class="sxs-lookup"><span data-stu-id="13657-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="13657-266">***fields*** correspond aux champs de sortie du bolt.</span><span class="sxs-lookup"><span data-stu-id="13657-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="13657-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="13657-267">**nontx-topolopy**</span></span> |<span data-ttu-id="13657-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="13657-268">topology-name</span></span><br /><span data-ttu-id="13657-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="13657-269">spout-map</span></span><br /><span data-ttu-id="13657-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="13657-270">bolt-map</span></span> |<span data-ttu-id="13657-271">Permet de définir une topologie non transactionnelle avec un nom de topologie,&nbsp; une carte de définition de spouts et une carte de définition de bolts.</span><span class="sxs-lookup"><span data-stu-id="13657-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="13657-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="13657-272">**scp-spout**</span></span> |<span data-ttu-id="13657-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="13657-273">exec-name</span></span><br /><span data-ttu-id="13657-274">args</span><span class="sxs-lookup"><span data-stu-id="13657-274">args</span></span><br /><span data-ttu-id="13657-275">fields</span><span class="sxs-lookup"><span data-stu-id="13657-275">fields</span></span><br /><span data-ttu-id="13657-276">Paramètres</span><span class="sxs-lookup"><span data-stu-id="13657-276">parameters</span></span> |<span data-ttu-id="13657-277">Permet de définir un spout non transactionnel.</span><span class="sxs-lookup"><span data-stu-id="13657-277">Define a nontransactional spout.</span></span> <span data-ttu-id="13657-278">Exécutera l’application avec ***exec-name*** en utilisant ***args***.</span><span class="sxs-lookup"><span data-stu-id="13657-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="13657-279">***fields*** correspond aux champs de sortie du spout.</span><span class="sxs-lookup"><span data-stu-id="13657-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="13657-280">***parameters*** est facultatif, il permet de spécifier certains paramètres tels que « nontransactional.ack.enabled ».</span><span class="sxs-lookup"><span data-stu-id="13657-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="13657-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="13657-281">**scp-bolt**</span></span> |<span data-ttu-id="13657-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="13657-282">exec-name</span></span><br /><span data-ttu-id="13657-283">args</span><span class="sxs-lookup"><span data-stu-id="13657-283">args</span></span><br /><span data-ttu-id="13657-284">fields</span><span class="sxs-lookup"><span data-stu-id="13657-284">fields</span></span><br /><span data-ttu-id="13657-285">Paramètres</span><span class="sxs-lookup"><span data-stu-id="13657-285">parameters</span></span> |<span data-ttu-id="13657-286">Permet de définir un bolt non transactionnel.</span><span class="sxs-lookup"><span data-stu-id="13657-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="13657-287">Exécutera l’application avec ***exec-name*** en utilisant ***args***.</span><span class="sxs-lookup"><span data-stu-id="13657-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="13657-288">***fields*** correspond aux champs de sortie du bolt.</span><span class="sxs-lookup"><span data-stu-id="13657-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="13657-289">***parameters*** est facultatif, il permet de spécifier certains paramètres tels que « nontransactional.ack.enabled ».</span><span class="sxs-lookup"><span data-stu-id="13657-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="13657-290">Les mots clés suivants sont définis pour SCP.NET :</span><span class="sxs-lookup"><span data-stu-id="13657-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="13657-291">**Mots clés**</span><span class="sxs-lookup"><span data-stu-id="13657-291">**Key Words**</span></span> | <span data-ttu-id="13657-292">**Description**</span><span class="sxs-lookup"><span data-stu-id="13657-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="13657-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="13657-293">**:name**</span></span> |<span data-ttu-id="13657-294">Permet de définir le nom de la topologie.</span><span class="sxs-lookup"><span data-stu-id="13657-294">Define the Topology Name</span></span> |
| <span data-ttu-id="13657-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="13657-295">**:topology**</span></span> |<span data-ttu-id="13657-296">Permet de définir la topologie en utilisant les fonctions précédentes et d'en intégrer d'autres.</span><span class="sxs-lookup"><span data-stu-id="13657-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="13657-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="13657-297">**:p**</span></span> |<span data-ttu-id="13657-298">Permet de définir l'indicateur de parallélisme pour chaque spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="13657-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="13657-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="13657-299">**:config**</span></span> |<span data-ttu-id="13657-300">Permet de définir le paramètre de configuration ou de mettre à jour celui existant.</span><span class="sxs-lookup"><span data-stu-id="13657-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="13657-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="13657-301">**:schema**</span></span> |<span data-ttu-id="13657-302">Permet de définir le schéma de flux.</span><span class="sxs-lookup"><span data-stu-id="13657-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="13657-303">Et voici des paramètres fréquemment utilisés :</span><span class="sxs-lookup"><span data-stu-id="13657-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="13657-304">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="13657-304">**Parameter**</span></span> | <span data-ttu-id="13657-305">**Description**</span><span class="sxs-lookup"><span data-stu-id="13657-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="13657-306">**« plugin.name »**</span><span class="sxs-lookup"><span data-stu-id="13657-306">**"plugin.name"**</span></span> |<span data-ttu-id="13657-307">Nom du fichier .exe du plug-in C#</span><span class="sxs-lookup"><span data-stu-id="13657-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="13657-308">**« plugin.args »**</span><span class="sxs-lookup"><span data-stu-id="13657-308">**"plugin.args"**</span></span> |<span data-ttu-id="13657-309">Arguments du plug-in</span><span class="sxs-lookup"><span data-stu-id="13657-309">plugin args</span></span> |
| <span data-ttu-id="13657-310">**« output.schema »**</span><span class="sxs-lookup"><span data-stu-id="13657-310">**"output.schema"**</span></span> |<span data-ttu-id="13657-311">Schéma de sortie</span><span class="sxs-lookup"><span data-stu-id="13657-311">Output schema</span></span> |
| <span data-ttu-id="13657-312">**« nontransactional.ack.enabled »**</span><span class="sxs-lookup"><span data-stu-id="13657-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="13657-313">Indique si le mécanisme d'accusé de réception (ack) est activé pour la topologie non transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="13657-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="13657-314">La commande runspec sera déployée avec les octets. Elle s'utilise comme ceci :</span><span class="sxs-lookup"><span data-stu-id="13657-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="13657-315">Le paramètre ***resource-dir*** est facultatif, vous devez le spécifier lorsque vous voulez brancher une application C\#. Ce répertoire contient l’application, ses dépendances et sa configuration.</span><span class="sxs-lookup"><span data-stu-id="13657-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="13657-316">Le paramètre ***classpath*** est également facultatif.</span><span class="sxs-lookup"><span data-stu-id="13657-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="13657-317">Il permet de spécifier le chemin d'accès des classes Java si le fichier spec contient un spout ou un bolt Java.</span><span class="sxs-lookup"><span data-stu-id="13657-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="13657-318">Fonctionnalités diverses</span><span class="sxs-lookup"><span data-stu-id="13657-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="13657-319">Déclaration de schéma d’entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="13657-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="13657-320">L’utilisateur peut émettre un tuple dans le processus C\#, la plateforme doit sérialiser ce tuple dans byte[], le transférer côté Java, avant que Storm ne le transfère vers les cibles.</span><span class="sxs-lookup"><span data-stu-id="13657-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="13657-321">Pendant ce temps dans le composant en aval, le processus C\# reçoit le tuple à partir du côté Java, puis le convertit vers les types d’origine de chaque plateforme. Toutes ces opérations sont masquées par la plateforme.</span><span class="sxs-lookup"><span data-stu-id="13657-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="13657-322">Pour prendre en charge la sérialisation et la désérialisation, le code utilisateur doit déclarer le schéma des entrées et sorties.</span><span class="sxs-lookup"><span data-stu-id="13657-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="13657-323">Le schéma de flux d'entrée/sortie est défini en tant que dictionnaire, la clé est le StreamId et la valeur correspond aux types des colonnes.</span><span class="sxs-lookup"><span data-stu-id="13657-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="13657-324">Le multiflux peut être déclaré pour le composant.</span><span class="sxs-lookup"><span data-stu-id="13657-324">The component can have multi-streams declared.</span></span>

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


<span data-ttu-id="13657-325">Les API suivantes sont ajoutées à l'objet Context :</span><span class="sxs-lookup"><span data-stu-id="13657-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="13657-326">Le code utilisateur doit garantir que les tuples émis respectent le schéma défini pour ce flux, ou le système génère une exception de runtime.</span><span class="sxs-lookup"><span data-stu-id="13657-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="13657-327">Prise en charge multiflux</span><span class="sxs-lookup"><span data-stu-id="13657-327">Multi-Stream Support</span></span>
<span data-ttu-id="13657-328">SCP prend en charge le code utilisateur pour émettre ou recevoir depuis plusieurs flux en même temps.</span><span class="sxs-lookup"><span data-stu-id="13657-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="13657-329">La prise en charge s'affiche dans l'objet Context lorsque la méthode Emit possède un paramètre ID de flux facultatif.</span><span class="sxs-lookup"><span data-stu-id="13657-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="13657-330">Deux méthodes ont été ajoutées dans l'objet Context de SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="13657-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="13657-331">Elles permettent d'émettre un ou plusieurs tuples pour spécifier StreamId.</span><span class="sxs-lookup"><span data-stu-id="13657-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="13657-332">StreamId est une chaîne et elle doit être cohérente dans C\# et la spécification de définition de topologie.</span><span class="sxs-lookup"><span data-stu-id="13657-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="13657-333">L'émission vers un flux qui n'existe pas entraînera des exceptions de runtime.</span><span class="sxs-lookup"><span data-stu-id="13657-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="13657-334">Regroupement de champs</span><span class="sxs-lookup"><span data-stu-id="13657-334">Fields Grouping</span></span>
<span data-ttu-id="13657-335">Le regroupement de champs intégré à Storm ne fonctionne pas correctement dans SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="13657-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="13657-336">Sur le côté du proxy Java, tous les types de données de champs correspondent à la sémantique byte[], et le regroupement de champs utilise le code de hachage d’objet byte pour effectuer le regroupement.</span><span class="sxs-lookup"><span data-stu-id="13657-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="13657-337">Le code de hachage d'objet byte[] correspond à l'adresse de cet objet en mémoire.</span><span class="sxs-lookup"><span data-stu-id="13657-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="13657-338">Le regroupement sera donc incorrect pour deux objets byte[] partageant le même contenu mais pas la même adresse.</span><span class="sxs-lookup"><span data-stu-id="13657-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="13657-339">SCP.NET ajoute une méthode de regroupement personnalisée et utilise le contenu de byte[] pour procéder au regroupement.</span><span class="sxs-lookup"><span data-stu-id="13657-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="13657-340">Dans le fichier **SPEC** , la syntaxe correspond à :</span><span class="sxs-lookup"><span data-stu-id="13657-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="13657-341">Ici,</span><span class="sxs-lookup"><span data-stu-id="13657-341">Here,</span></span>

1. <span data-ttu-id="13657-342">« scp-field-group » signifie « Regroupement de champs personnalisé implémenté par SCP ».</span><span class="sxs-lookup"><span data-stu-id="13657-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="13657-343">« :tx » ou « :non-tx » signifie qu’il s’agit d’une topologie transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="13657-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="13657-344">Nous avons besoin de cette information, car l'index de démarrage est différent si la topologie est tx ou non-tx.</span><span class="sxs-lookup"><span data-stu-id="13657-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="13657-345">[0,1] représente un hashset d'ID de champ, commençant à 0.</span><span class="sxs-lookup"><span data-stu-id="13657-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="13657-346">Topologie hybride</span><span class="sxs-lookup"><span data-stu-id="13657-346">Hybrid topology</span></span>
<span data-ttu-id="13657-347">Le Storm natif est écrit en Java.</span><span class="sxs-lookup"><span data-stu-id="13657-347">The native Storm is written in Java.</span></span> <span data-ttu-id="13657-348">En outre, SCP.Net l’a amélioré pour permettre à nos clients d’écrire du code C\# pour gérer leur logique métier.</span><span class="sxs-lookup"><span data-stu-id="13657-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="13657-349">Mais nous prenons également en charge les topologies hybrides, qui contiennent des spouts/bolts C\#, ainsi que des spouts/bolts Java.</span><span class="sxs-lookup"><span data-stu-id="13657-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="13657-350">Indiquer le spout/bolt Java dans le fichier spec</span><span class="sxs-lookup"><span data-stu-id="13657-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="13657-351">Vous pouvez également utiliser « scp-spout » et « scp-bolt » dans le fichier spec pour spécifier les spouts et les bolts Java. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="13657-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="13657-352">Ici `microsoft.scp.example.HybridTopology.Generator` est le nom de la classe Spout Java.</span><span class="sxs-lookup"><span data-stu-id="13657-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="13657-353">Spécifier le chemin d’accès des classes Java dans une commande runSpec</span><span class="sxs-lookup"><span data-stu-id="13657-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="13657-354">Si vous voulez envoyer une topologie contenant des spouts ou des bolts Java, vous devez d’abord compiler les spouts ou bolts Java et récupérer les fichiers Jar.</span><span class="sxs-lookup"><span data-stu-id="13657-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="13657-355">Puis, vous devez spécifier le chemin d’accès des classes Java contenant les fichiers Jar au moment de l’envoi de la topologie.</span><span class="sxs-lookup"><span data-stu-id="13657-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="13657-356">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="13657-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="13657-357">Ici **examples\\HybridTopology\\java\\target\\** correspond au dossier contenant le fichier Jar spout/bolt Java.</span><span class="sxs-lookup"><span data-stu-id="13657-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="13657-358">Sérialisation et désérialisation entre Java et C\\</span><span class="sxs-lookup"><span data-stu-id="13657-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="13657-359">Notre composant SCP a un côté Java et un côté C\#.</span><span class="sxs-lookup"><span data-stu-id="13657-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="13657-360">Pour interagir avec des spouts/bolts Java natifs, la sérialisation/désérialisation doit intervenir entre le côté Java et le côté C\#, comme l’illustre le graphique suivant.</span><span class="sxs-lookup"><span data-stu-id="13657-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![Diagramme d’un flux entre un composant Java et un composant SCP, et inversement](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="13657-362">**Sérialisation côté Java et désérialisation côté C\#**</span><span class="sxs-lookup"><span data-stu-id="13657-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="13657-363">Tout d’abord, nous fournissons une implémentation par défaut pour la sérialisation côté Java et la désérialisation côté C\#.</span><span class="sxs-lookup"><span data-stu-id="13657-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="13657-364">La méthode de sérialisation côté Java peut être spécifiée dans le fichier SPEC :</span><span class="sxs-lookup"><span data-stu-id="13657-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="13657-365">La méthode de désérialisation côté C\# doit être spécifiée dans le code utilisateur C\# :</span><span class="sxs-lookup"><span data-stu-id="13657-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="13657-366">Cette implémentation par défaut peut gérer la plupart des cas si le type de données n'est pas trop complexe.</span><span class="sxs-lookup"><span data-stu-id="13657-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="13657-367">Dans certains cas, soit parce que le type de données utilisateur est trop complexe, soit parce que les performances de notre implémentation par défaut ne répondent pas aux besoins de l'utilisateur, ce dernier peut utiliser sa propre implémentation en plug-in.</span><span class="sxs-lookup"><span data-stu-id="13657-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="13657-368">L'interface de sérialisation côté Java se définit comme suit :</span><span class="sxs-lookup"><span data-stu-id="13657-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="13657-369">L’interface de désérialisation côté C\# se définit comme suit :</span><span class="sxs-lookup"><span data-stu-id="13657-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="13657-370">public interface ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="13657-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="13657-371">**Sérialisation côté C\# et désérialisation côte Java**</span><span class="sxs-lookup"><span data-stu-id="13657-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="13657-372">La méthode de sérialisation côté C\# doit être spécifiée dans le code utilisateur C\# :</span><span class="sxs-lookup"><span data-stu-id="13657-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="13657-373">La méthode de désérialisation côté Java doit être spécifiée dans le fichier SPEC :</span><span class="sxs-lookup"><span data-stu-id="13657-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="13657-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="13657-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="13657-375">Ici « microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer » est le nom du désérialiseur, tandis que « microsoft.scp.example.HybridTopology.Person » est la classe cible vers laquelle les données sont désérialisées.</span><span class="sxs-lookup"><span data-stu-id="13657-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="13657-376">L’utilisateur peut également appliquer sa propre implémentation du sérialiseur C\# et du désérialiseur Java.</span><span class="sxs-lookup"><span data-stu-id="13657-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="13657-377">Voici l’interface du sérialiseur C\# :</span><span class="sxs-lookup"><span data-stu-id="13657-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="13657-378">Voici l’interface du désérialiseur Java :</span><span class="sxs-lookup"><span data-stu-id="13657-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="13657-379">Mode d’hébergement SCP</span><span class="sxs-lookup"><span data-stu-id="13657-379">SCP Host Mode</span></span>
<span data-ttu-id="13657-380">Dans ce mode, l'utilisateur peut compiler ses codes en DLL, puis utiliser le fichier SCPHost.exe fourni par SCP pour l'envoi de topologie.</span><span class="sxs-lookup"><span data-stu-id="13657-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="13657-381">Le fichier spec ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="13657-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="13657-382">Ici, `plugin.name` est spécifié en tant que `SCPHost.exe` fourni par le Kit de développement logiciel (SDK) SCP.</span><span class="sxs-lookup"><span data-stu-id="13657-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="13657-383">SCPHost.exe accepte exactement trois paramètres :</span><span class="sxs-lookup"><span data-stu-id="13657-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="13657-384">Le premier est le nom DLL ( `"HelloWorld.dll"` dans notre exemple).</span><span class="sxs-lookup"><span data-stu-id="13657-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="13657-385">Le second est le nom de la classe ( `"Scp.App.HelloWorld.Generator"` dans notre exemple).</span><span class="sxs-lookup"><span data-stu-id="13657-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="13657-386">Le troisième est le nom de la méthode statique publique, qui peut être appelée pour obtenir une instance de ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="13657-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="13657-387">En mode d'hébergement, le code utilisateur est compilé en tant que DLL, puis appelé par la plateforme SCP.</span><span class="sxs-lookup"><span data-stu-id="13657-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="13657-388">La plateforme SCP peut donc contrôler complètement l'ensemble de la logique de traitement.</span><span class="sxs-lookup"><span data-stu-id="13657-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="13657-389">Nous recommandons donc à nos clients d'envoyer la topologie en mode d'hébergement SCP, car elle peut simplifier le développement et améliorer la flexibilité et la compatibilité descendante pour les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="13657-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="13657-390">Exemples de programmation SCP</span><span class="sxs-lookup"><span data-stu-id="13657-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="13657-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="13657-391">HelloWorld</span></span>
<span data-ttu-id="13657-392">**HelloWorld** est un exemple très simple qui offre un avant-goût de SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="13657-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="13657-393">Il emploie une topologie non transactionnelle, avec un spout appelé **generator**, et deux bolts appelés **splitter** et **counter**.</span><span class="sxs-lookup"><span data-stu-id="13657-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="13657-394">Le spout **generator** va générer des phrases aléatoirement, avant de les émettre vers **splitter**.</span><span class="sxs-lookup"><span data-stu-id="13657-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="13657-395">Le bolt **splitter** va diviser les phrases en mots et les émettre vers le bolt **counter**.</span><span class="sxs-lookup"><span data-stu-id="13657-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="13657-396">Le bolt « counter » utilise un dictionnaire pour enregistrer le nombre d’occurrences de chaque mot.</span><span class="sxs-lookup"><span data-stu-id="13657-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="13657-397">L’exemple contient deux fichiers spec, **HelloWorld.spec** et **HelloWorld\_EnableAck.spec**.</span><span class="sxs-lookup"><span data-stu-id="13657-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="13657-398">Dans le code C\#, vous pouvez savoir si le mécanisme d'accusé de réception (ack) est activé en récupérant le pluginConf côté Java.</span><span class="sxs-lookup"><span data-stu-id="13657-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="13657-399">Dans le spout, si le ack est activé, un dictionnaire est utilisé pour mettre en cache les tuples n'ayant pas été reçus.</span><span class="sxs-lookup"><span data-stu-id="13657-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="13657-400">Si Fail() est appelée, les tuples ayant échoué sont relus :</span><span class="sxs-lookup"><span data-stu-id="13657-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="13657-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="13657-401">HelloWorldTx</span></span>
<span data-ttu-id="13657-402">L’exemple **HelloWorldTx** illustre l’implémentation d’une topologie transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="13657-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="13657-403">Il contient un spout nommé **generator**, un bolt par lots nommé **partial-count** et un bolt de validation nommé **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="13657-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="13657-404">Il contient également trois fichiers txt : **DataSource0.txt**, **DataSource1.txt** et **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="13657-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="13657-405">Dans chaque transaction, le spout **generator** sélectionne deux des trois fichiers txt de façon aléatoire, avant de les émettre vers le bolt **partial-count**.</span><span class="sxs-lookup"><span data-stu-id="13657-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="13657-406">Le bolt **partial-count** va d’abord récupérer le nom du fichier à partir du tuple reçu, puis ouvrir le fichier et compter le nombre de mots qu’il contient, avant d’émettre ce résultat vers le bolt **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="13657-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="13657-407">Le bolt **count-sum** résume le résultat total.</span><span class="sxs-lookup"><span data-stu-id="13657-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="13657-408">Pour mener à bien la sémantique **Une fois au minimum**, le bolt de validation **count-sum** doit décider s’il s’agit d’une transaction relue.</span><span class="sxs-lookup"><span data-stu-id="13657-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="13657-409">Dans cet exemple, il est doté d'une variable de membre statique :</span><span class="sxs-lookup"><span data-stu-id="13657-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="13657-410">Au moment de la création d’une instance ISCPBatchBolt, `txAttempt` est récupéré à partir des paramètres d’entrée :</span><span class="sxs-lookup"><span data-stu-id="13657-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
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

<span data-ttu-id="13657-411">Quand `FinishBatch()` est appelé, `lastCommittedTxId` est mis à jour s’il ne s’agit pas d’une transaction relue.</span><span class="sxs-lookup"><span data-stu-id="13657-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="13657-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="13657-412">HybridTopology</span></span>
<span data-ttu-id="13657-413">Cette topologie contient un spout Java et un bolt C\#.</span><span class="sxs-lookup"><span data-stu-id="13657-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="13657-414">Elle utilise l'implémentation de sérialisation et de désérialisation par défaut fournie par la plateforme SCP.</span><span class="sxs-lookup"><span data-stu-id="13657-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="13657-415">Consultez **HybridTopology.spec** dans le dossier **examples\\HybridTopology** pour obtenir les détails du fichier spec et **SubmitTopology.bat** pour savoir comment spécifier le chemin d’accès des classes Java.</span><span class="sxs-lookup"><span data-stu-id="13657-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="13657-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="13657-416">SCPHostDemo</span></span>
<span data-ttu-id="13657-417">Cet exemple est sensiblement identique à HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="13657-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="13657-418">Les seules différences sont que le code utilisateur est compilé en tant que DLL et que la topologie est envoyée en utilisant SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="13657-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="13657-419">Pour en savoir plus, consultez la section « Mode d’hébergement SCP ».</span><span class="sxs-lookup"><span data-stu-id="13657-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13657-420">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13657-420">Next Steps</span></span>
<span data-ttu-id="13657-421">Pour obtenir des exemples de topologies Storm créées à l’aide de SCP, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="13657-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="13657-422">Développement de topologies C# pour Apache Storm dans HDInsight à l'aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13657-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="13657-423">Traitement d'événements à partir d'Azure Event Hubs avec Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="13657-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="13657-424">Création de plusieurs flux de données dans une topologie C# Storm</span><span class="sxs-lookup"><span data-stu-id="13657-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="13657-425">Utiliser Power BI pour visualiser les données d’une topologie Storm</span><span class="sxs-lookup"><span data-stu-id="13657-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="13657-426">Traitement des données de capteur de véhicule à partir d'Event Hubs à l'aide de Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="13657-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="13657-427">Extraction, transformation et chargement (ETL) à partir d’Azure Event Hubs dans HBase</span><span class="sxs-lookup"><span data-stu-id="13657-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="13657-428">Corrélation des événements à l’aide de Storm et HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="13657-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

