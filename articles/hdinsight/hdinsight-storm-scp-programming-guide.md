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
# <a name="scp-programming-guide"></a>Guide de programmation SCP
SCP est une plateforme toobuild en temps réel, une application de traitement de données fiable, cohérente et plus performante. Il est construit sur [Apache Storm](http://storm.incubator.apache.org/) --un système conçu par les Communautés hello OSS de traitement du flux de données. Storm est conçu par Nathan Marz et diffusé en open source par Twitter. Il s’appuie sur [Apache soigneur](http://zookeeper.apache.org/), Apache un autre projet tooenable coordination distribuée hautement fiable et la gestion d’état. 

Non seulement les projets hello SCP déplacée Storm sur Windows, mais également le projet de hello ajouté extensions et personnalisation pour l’écosystème de Windows hello. les extensions de Hello incluent l’expérience de développement .NET et des bibliothèques, personnalisation de hello inclut le déploiement basé sur Windows. 

personnalisation et extension de hello est effectuée de sorte que nous n’avez pas besoin de projets de systèmes d’exploitation toofork hello et nous avons tirer parti des écosystèmes dérivées reposant sur Storm.

## <a name="processing-model"></a>Modèle de traitement
les données de salutation SCP sont modélisées en tant que flux continus de tuples. En général, les tuples hello flux dans une file d’attente tout d’abord, puis récupéré et transformés par la logique métier hébergée au sein d’une topologie Storm, enfin hello sortie peut être transmis en tant que système tooanother SCP de tuples, ou être validées toostores comme système de fichiers distribués ou bases de données tels que SQL Server.

![Un diagramme d’une file d’attente tooprocessing de données qui alimente un magasin de données d’alimentation](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

Dans Storm, une topologie d'application définit un graphique de calcul. Chaque nœud d'une topologie contient une logique de traitement et les liens entre ces nœuds indiquent les flux de données. données d’entrée tooinject nœuds Hello dans la topologie de hello sont appelées becs verseurs, qui peuvent être des données hello toosequence utilisé. données d’entrée Hello peuvent résider dans des fichiers journaux, de la base de données transactionnelle, compteur de performance système nœuds de hello etc. avec les deux flux de données d’entrée et de sortie sont appelées boulons, lequel hello le filtrage des données réelles et les sélections et agrégation.

SCP prend en charge les types de traitement de données Meilleur effort, Une fois au minimum et Exactement une. Dans une application distribuée de traitement de diffusion en continu, diverses erreurs peuvent se produire pendant le traitement des données, telles qu’une erreur de code utilisateur, la défaillance d’un ordinateur ou une panne du réseau. Au moins une transformation garantit que toutes les données sont traitées au moins une fois par relecture automatiquement hello données mêmes lorsqu’une erreur se produit. Le type de traitement Une fois au minimum est simple et fiable et s'adapte à de nombreuses applications. Toutefois, lors de l’application hello requiert le comptage exact, par exemple, au moins une est insuffisante car hello mêmes données pourraient potentiellement être lu dans la topologie de l’application hello. Dans ce cas, exactement-une fois que le traitement est conçu toomake que résultat de hello est correct, même lorsque les données de salutation peuvent être relues et traitées plusieurs fois.

SCP permet d’applications de processus de données en temps réel de toodevelop pour les développeurs .NET lorsque hello de tirer parti de la Machine virtuelle Java (JVM) en fonction de Storm sous hello. Hello .NET et JVM communiquent via le socket TCP local. En principe chaque bec/éclair est une paire de processus .net/Java, où la logique de l’utilisateur hello s’exécute dans des processus de .net comme un plug-in.

toobuild un application par-dessus SCP de traitement des données, plusieurs étapes sont nécessaires :

* Concevoir et implémenter hello becs verseurs toopull dans les données à partir de la file d’attente.
* Concevoir et implémenter des données d’entrée de boulons tooprocess hello et enregistrer des magasins de données tooexternal comme base de données.
* Conception de topologie de hello, puis soumettre et exécuter la topologie de hello. Hello topologie définit les sommets et les données de salutation flux entre les sommets hello. SCP prend la spécification de topologie hello et déployez-le sur un cluster Storm, où chaque sommet s’exécute sur un seul nœud logique. basculement de Hello et mise à l’échelle seront être pris en charge par le Planificateur de tâches Storm hello.

Ce document utilise certains toowalk exemples simples via l’application de traitement des données toobuild avec SCP.

## <a name="scp-plugin-interface"></a>Interface de plug-in SCP
Plug-ins SCP (ou applications) sont des exécutables autonomes qui peuvent s’exécuter à l’intérieur de Visual Studio pendant la phase de développement hello et être intégrés au pipeline de Storm hello après le déploiement en production. L’écriture de plug-in hello SCP est simplement hello identique à celui de l’écriture de toutes les autres applications Windows standard console. Plateforme SCP.NET déclare une interface pour bec/éclair et code de plug-in hello utilisateur doit implémenter ces interfaces. Hello principal de cette conception vise que cet utilisateur hello peut se concentrer sur leur propre logique d’entreprise et en laissant les autres toobe éléments géré par la plateforme SCP.NET.

code de plug-in Hello utilisateur doit implémenter l’une des interfaces de ce qui suit hello, varie selon que la topologie de hello est transactionnelle ou non transactionnelle, et si le composant de hello est bec ou éclair.

* ISCPSpout
* ISCPBolt
* ISCPTxSpout
* ISCPBatchBolt

### <a name="iscpplugin"></a>ISCPPlugin
ISCPPlugin est l’interface commune de hello pour tous les types de plug-ins. Actuellement, c'est une interface factice.

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a>ISCPSpout
ISCPSpout est interface hello bec non transactionnelle.

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

Lorsque `NextTuple()` est appelée, hello C\# un ou plusieurs tuples peut émettre du code utilisateur. Si aucune n’est tooemit, cette méthode doit retourner sans l’émission de quoi que ce soit. Notez que `NextTuple()`, `Ack()` et `Fail()` sont toutes appelées dans une boucle étroite d’un thread unique dans un processus C\#. Lorsqu’il n’y a aucune tooemit tuples, il est toohave courtois NextTuple veille pour un laps de temps (par exemple, les 10 millisecondes) ainsi en toowaste pas trop de ressources processeur.

`Ack()` et `Fail()` sont appelées uniquement quand le mécanisme d’accusé de réception (ack) est activé dans le fichier spec. Hello `seqId` est utilisé tooidentify hello tuple, qui est reçu ou a échoué. Par conséquent, si l’accusé de réception est activée dans une topologie non transactionnel, hello suivant emit fonction doit être utilisé dans bec :

    public abstract void Emit(string streamId, List<object> values, long seqId); 

Si l’accusé de réception n’est pas pris en charge dans une topologie non transactionnel, hello `Ack()` et `Fail()` peut être laissée en tant que fonction vide.

Hello `parms` des paramètres d’entrée de ces fonctions sont simplement vide dictionnaire, ils sont réservés à un usage ultérieur.

### <a name="iscpbolt"></a>ISCPBolt
ISCPBolt est interface hello éclair non transactionnelle.

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

Lors de la nouvelle tuple est disponible, hello `Execute()` fonction sera appelée tooprocess il.

### <a name="iscptxspout"></a>ISCPTxSpout
ISCPTxSpout est interface hello bec transactionnels.

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

Tout comme leurs équivalentes non-transactionnelles, les fonctions `NextTx()`, `Ack()` et `Fail()` sont toutes appelées dans une boucle étroite d’un thread unique dans un processus C\#. Lorsqu’il n’y a aucune tooemit de données, il est toohave courtois `NextTx` mise en veille pendant un court laps de temps (10 millisecondes) ainsi en toowaste pas trop de ressources processeur.

`NextTx()`est appelé toostart une nouvelle transaction, hello paramètre out `seqId` tooidentify utilisé hello transaction, qui est également utilisée dans `Ack()` et `Fail()`. Dans `NextTx()`, utilisateur peut émettre du côté tooJava de données. Hello données seront stockées dans la relecture toosupport soigneur. Capacité hello soigneur étant très limitée, utilisateur doit émettre uniquement des métadonnées, pas les données en bloc dans bec transactionnelle.

Si une transaction échoue, Storm la relit automatiquement. Il ne faut donc pas appeler la fonction `Fail()` dans un cas normal. Mais si le SCP peut vérifier les métadonnées hello émises par bec transactionnels, elle peut appeler `Fail()` lorsque les métadonnées hello ne sont pas valide.

Hello `parms` des paramètres d’entrée de ces fonctions sont simplement vide dictionnaire, ils sont réservés à un usage ultérieur.

### <a name="iscpbatchbolt"></a>ISCPBatchBolt
ISCPBatchBolt est interface hello éclair transactionnelle.

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

`Execute()`est appelé en cas de nouvelle tuple arrivant à éclair de hello. `FinishBatch()` est appelé quand cette transaction est terminée. Hello `parms` paramètre d’entrée est réservé à un usage ultérieur.

Il existe un concept important pour la topologie transactionnelle : `StormTxAttempt`. Il comporte deux champs : `TxId` et `AttemptId`. `TxId`est utilisé tooidentify une transaction spécifique, et pour une transaction donnée, il peut y avoir plusieurs tentative si les transactions hello échoue et sont relu. SCP.NET sera à nouveau un autre ISCPBatchBolt objet tooprocess chaque `StormTxAttempt`, à l’instar de quel souhaitez-vous Storm côté de Java. Hello cette conception vise toosupport le traitement des transactions parallèles. Utilisateur devez la conserver à l’esprit que si la tentative de transaction est terminée et hello correspondant ISCPBatchBolt objet sera détruit par le garbage collector.

## <a name="object-model"></a>Modèle objet
SCP.NET fournit également un ensemble simple des objets clés pour les développeurs des tooprogram avec. Il s’agit des objets **Context**, **StateStore** et **SCPRuntime**. Elles sont abordées dans la partie de rest hello de cette section.

### <a name="context"></a>Context
Contexte fournit une application de toohello d’environnement en cours d’exécution. Chaque instance ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) dispose d'une instance Context correspondante. fonctionnalité Hello fournie par le contexte peut être divisée en deux parties : partie statique de hello (1) qui est disponible dans hello ensemble C\# traiter, la partie dynamique de hello (2) qui est disponible uniquement pour l’instance spécifique de contexte hello.

### <a name="static-part"></a>Partie statique
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

`Logger` est fourni à des fins de journalisation.

`pluginType`est utilisé le type de plug-in tooindicate hello Hello C\# processus. Si hello C\# processus est exécuté en mode de test local (sans Java), le type de plug-in hello est `SCP_NET_LOCAL`.

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

`Config`est fourni à des paramètres de configuration tooget du côté de Java. paramètres de Hello sont passés du côté de Java lorsque C\# plug-in est initialisé. Hello `Config` paramètres sont divisés en deux parties : `stormConf` et `pluginConf`.

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

`stormConf`est des paramètres définis par Storm et `pluginConf` est paramètres hello définis par le SCP. Par exemple :

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

`TopologyContext`est fourni le contexte de topologie tooget hello, il est particulièrement utile pour les composants avec plusieurs parallélisme. Voici un exemple :

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

### <a name="dynamic-part"></a>Partie dynamique
Hello après les interfaces est pertinente tooa certaine l’instance de contexte. l’instance de contexte Hello est créé par la plateforme SCP.NET et passé toohello le code utilisateur :

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

Pour bec non transactionnelle prenant en charge l’accusé de réception, hello suivant de méthode est fournie :

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

Pour éclair non transactionnelle prenant en charge l’accusé de réception, il doit explicitement `Ack()` ou `Fail()` hello tuple qu’il a reçu. Et lors de l’émission de tuple de nouveau, il doit également spécifier ancres hello du tuple de nouveau hello. Hello méthodes suivantes est fournie.

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a>StateStore
`StateStore` fournit des services de métadonnées, une génération de séquence unitone et une coordination sans attente. Il est possible de développer des abstractions concurrentielles distribuées et globales sur `StateStore`, notamment des verrous distribués, des files d’attente distribuées, des barrières et des services de transaction.

Les applications de SCP peuvent utiliser hello `State` objet toopersist certaines informations de soigneur, en particulier pour la topologie transactionnelle. Ce faisant, si bec transactionnels tombe en panne et redémarrer, il peut récupérer les informations nécessaires hello soigneur et redémarrez le pipeline de hello.

Hello `StateStore` objet comprend principalement les méthodes suivantes :

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

Hello `State` objet comprend principalement les méthodes suivantes :

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

Pourquoi `Commit()` la méthode simpleMode a la valeur tootrue, supprimera simplement hello correspondant ZNode dans soigneur. Sinon, elle supprimera hello ZNode actuel et l’ajout d’un nouveau nœud Bonjour validé\_chemin d’accès.

### <a name="scpruntime"></a>SCPRuntime
SCPRuntime fournit deux méthodes suivantes de hello.

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

`Initialize()`est un environnement d’exécution hello SCP tooinitialize utilisé. Dans cette méthode, hello C\# processus se connecteront à côté de Java toohello et obtient les paramètres de configuration et le contexte de la topologie.

`LaunchPlugin()`est utilisé tookick désactiver le message de type hello du traitement de boucle. Dans cette boucle, hello C\# plug-in reçoit les messages formulaire côté Java (y compris les signaux tuples et de contrôle) et traiter les messages hello, l’appel de la méthode d’interface hello peut-être fournissent par du code utilisateur hello. paramètre d’entrée Hello pour la méthode `LaunchPlugin()` est un délégué qui peut retourner un objet qui implémente l’interface de ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

Pour ISCPBatchBolt, nous pouvons obtenir `StormTxAttempt` de `parms`et l’utiliser toojudge s’il s’agit d’une tentative de relue. Cela est généralement effectué à éclair de validation hello et il est présenté dans hello `HelloWorldTx` exemple.

En règle générale, hello plug-ins SCP peut-être s’exécuter dans deux modes ici :

1. Mode de Test local : Hello dans ce mode, plug-ins SCP (hello C\# code utilisateur) exécuté à l’intérieur de Visual Studio pendant la phase de développement hello. `LocalContext`peut être utilisé dans ce mode, qui fournit une méthode tooserialize hello émis tuples toolocal fichiers et lire à nouveau toomemory.
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. Mode Normal : Dans ce mode, les plug-ins de SCP hello sont lancées par le processus java de storm.
   
    Voici un exemple de démarrage de plug-in SCP :
   
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

## <a name="topology-specification-language"></a>Langage de spécification de topologie
La spécification de topologie SCP est un langage de domaine spécifique pour décrire et configurer les topologies SCP. Il est basé sur Clojure DSL de Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) et est étendu par SCP.

Spécifications de topologie peuvent être envoyées directement toostorm de cluster pour l’exécution via hello ***runspec*** commande.

SCP.NET a Ajouter suivez fonctions toodefine hello topologie transactionnelle :

| **Nouvelles fonctions** | **Paramètres** | **Description** |
| --- | --- | --- |
| **tx-topolopy** |topology-name<br />spout-map<br />bolt-map |Définition d’une topologie transactionnelle avec le nom de topologie hello, &nbsp;becs verseurs amovibles de mappage de la définition et le mappage de définition de boulons hello |
| **scp-tx-spout** |exec-name<br />args<br />fields |Permet de définir un spout transactionnel. Il s’exécutera application hello avec ***exec-name*** à l’aide de ***args***.<br /><br />Hello ***champs*** est les champs de sortie hello pour bec |
| **scp-tx-batch-bolt** |exec-name<br />args<br />fields |Permet de définir un lot bolt transactionnel. Il s’exécutera application hello avec ***exec-name*** à l’aide de ***args.***<br /><br />Hello champs sont hello champs de sortie pour éclair. |
| **scp-tx-commit-bolt** |exec-name<br />args<br />fields |Permet de définir un validateur bolt transactionnel. Il s’exécutera application hello avec ***exec-name*** à l’aide de ***args***.<br /><br />Hello ***champs*** est les champs de sortie hello pour éclair |
| **nontx-topolopy** |topology-name<br />spout-map<br />bolt-map |Définition d’une topologie non transactionnel avec le nom de topologie hello,&nbsp; becs verseurs amovibles de mappage de la définition et le mappage de définition de boulons hello |
| **scp-spout** |exec-name<br />args<br />fields<br />Paramètres |Permet de définir un spout non transactionnel. Il s’exécutera application hello avec ***exec-name*** à l’aide de ***args***.<br /><br />Hello ***champs*** est les champs de sortie hello pour bec<br /><br />Hello ***paramètres*** est facultatif, à l’aide d’il toospecify certains paramètres, tels que « nontransactional.ack.enabled ». |
| **scp-bolt** |exec-name<br />args<br />fields<br />Paramètres |Permet de définir un bolt non transactionnel. Il s’exécutera application hello avec ***exec-name*** à l’aide de ***args***.<br /><br />Hello ***champs*** est les champs de sortie hello pour éclair<br /><br />Hello ***paramètres*** est facultatif, à l’aide d’il toospecify certains paramètres, tels que « nontransactional.ack.enabled ». |

Les mots clés suivants sont définis pour SCP.NET :

| **Mots clés** | **Description** |
| --- | --- |
| **:name** |Définir hello nom de la topologie |
| **:topology** |Définir hello topologie à l’aide de hello au-dessus de fonctions et générer dans celles. |
| **:p** |Définir l’indicateur de parallélisme hello pour chaque bec ou un éclair. |
| **:config** |Définir configurer le paramètre ou la mise à jour hello existants |
| **:schema** |Définissez hello schéma de flux de données. |

Et voici des paramètres fréquemment utilisés :

| **Paramètre** | **Description** |
| --- | --- |
| **« plugin.name »** |nom de fichier exe du plug-in hello c# |
| **« plugin.args »** |Arguments du plug-in |
| **« output.schema »** |Schéma de sortie |
| **« nontransactional.ack.enabled »** |Indique si le mécanisme d'accusé de réception (ack) est activé pour la topologie non transactionnelle. |

commande de runspec Hello est déployé avec les bits hello, l’utilisation de hello est similaire à :

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

Hello ***ressource-dir*** paramètre est facultatif, vous devez toospecify lorsque vous souhaitez tooplug C\# application et ce répertoire contiendra application hello, les dépendances de hello et les configurations.

Hello ***classpath*** paramètre est également facultatif. Il est utilisé toospecify hello Java classpath fichier spec de hello contient Java bec ou éclair.

## <a name="miscellaneous-features"></a>Fonctionnalités diverses
### <a name="input-and-output-schema-declaration"></a>Déclaration de schéma d’entrée et de sortie
utilisateur de Hello peut émettre du tuple dans C\# traiter, hello plate-forme doit tooserialize hello tuple en byte [], transfert tooJava côté, et Storm transférera cette cibles toohello de tuple. Pendant ce temps, dans le composant en aval, hello C\# processus recevra le tuple de côté de java et convertir les types d’origine toohello par plateforme, toutes ces opérations sont masquées par hello plateforme.

sérialisation de hello toosupport et la désérialisation, le code utilisateur a besoin de schéma de hello toodeclare de hello entrées et sorties.

schéma de flux de données d’entrée/sortie Hello est défini en tant que dictionnaire, clé de hello est hello StreamId et hello valeur hello des Types de colonnes de hello. composant de Hello peut avoir plusieurs flux de données déclaré.

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


Dans l’objet de contexte, nous avons hello ajouté des API suivante :

    public void DeclareComponentSchema(ComponentStreamSchema schema)

Code utilisateur doit vérifier les tuples hello émis obéissent aux règles de schéma de hello défini pour ce flux de données ou système de hello lève une exception runtime.

### <a name="multi-stream-support"></a>Prise en charge multiflux
SCP prend en charge utilisateur tooemit de code ou de réception à partir de plusieurs flux distincts à hello même temps. prise en charge Hello reflète dans l’objet de contexte hello hello Emit méthode prend un paramètre d’ID de flux de données facultatif.

Deux méthodes dans l’objet de contexte de SCP.NET de hello ont été ajoutés. Ils sont utilisés tooemit Tuple ou Tuples toospecify StreamId. Hello StreamId est une chaîne et doit toobe cohérents dans les deux C\# et hello les spécifications de définition de topologie.

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

flux Hello l’émission tooa non existante entraîne des exceptions runtime.

### <a name="fields-grouping"></a>Regroupement de champs
Hello build dans le regroupement des champs dans Strom ne fonctionne pas correctement dans SCP.NET. Sur le côté du Proxy Java de hello, tous les types de données des champs hello sont réellement byte [] et champs hello regroupement utilise le regroupement de hello tooperform objet hachage code hello byte []. code de hachage de l’objet de Hello byte [] est l’adresse hello de cet objet en mémoire. Regroupement de hello est donc incorrect pour deux octets [] objets que hello partage même contenu, mais pas hello même adresse.

SCP.NET ajoute une méthode de regroupement personnalisées, et il utilisera le contenu hello de regroupement de hello toodo hello byte []. Dans **SPEC** fichier, syntaxe de hello est similaire à :

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


Ici,

1. « scp-field-group » signifie « Regroupement de champs personnalisé implémenté par SCP ».
2. « :tx » ou « :non-tx » signifie qu’il s’agit d’une topologie transactionnelle. Nous avons besoin de ces informations depuis hello index de début est différent dans tx et non-tx topologies.
3. [0,1] représente un hashset d'ID de champ, commençant à 0.

### <a name="hybrid-topology"></a>Topologie hybride
Hello que Storm native est écrite en langage Java. Et SCP.Net il bénéficie tooenable notre toowrite douane C\# code toohandle leur logique métier. Mais nous prenons également en charge les topologies hybrides, qui contiennent des spouts/bolts C\#, ainsi que des spouts/bolts Java.

### <a name="specify-java-spoutbolt-in-spec-file"></a>Indiquer le spout/bolt Java dans le fichier spec
Dans le fichier spec, « scp-bec » et « scp-éclair » peuvent également être utilisé toospecify becs verseurs amovibles de Java et boulons, Voici un exemple :

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

Ici `microsoft.scp.example.HybridTopology.Generator` hello désigne hello Java bec de classe.

### <a name="specify-java-classpath-in-runspec-command"></a>Spécifier le chemin d’accès des classes Java dans une commande runSpec
Si vous souhaitez topologie toosubmit contenant Java becs verseurs amovibles ou boulons, vous devez les hello de compilation toofirst Java becs verseurs amovibles ou boulons et obtenez les fichiers Jar hello. Vous devez spécifier classpath java hello qui contient les fichiers Jar hello lors de la soumission de topologie. Voici un exemple :

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

Ici **exemples\\HybridTopology\\java\\cible\\**  est le dossier de hello contenant fichier Jar de Java bec/éclair de hello.

### <a name="serialization-and-deserialization-between-java-and-c"></a>Sérialisation et désérialisation entre Java et C\
Notre composant SCP a un côté Java et un côté C\#. Dans l’ordre toointeract avec natives Java becs verseurs/boulons, la sérialisation/désérialisation doivent être effectuée entre le côté de Java et C\# côté, comme illustré dans hello suivant du graphique.

![diagramme de composant java envoi composant tooSCP envoi tooJava composant](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. **Sérialisation côté Java et désérialisation côté C\#**
   
   Tout d’abord, nous fournissons une implémentation par défaut pour la sérialisation côté Java et la désérialisation côté C\#. méthode de sérialisation de Hello côté de Java peut être spécifiée dans le fichier SPEC :
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   Hello méthode de désérialisation dans C\# côté doit être spécifié en C\# code utilisateur :
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   Cette implémentation par défaut doit gérer la plupart des cas si le type de données hello n’est pas trop complexe. Dans certains cas, soit, car hello type de données utilisateur est trop complexe ou hello performances de notre implémentation par défaut ne répond pas aux hello spécification de l’utilisateur, plug-in d’utilisateur peuvent leur propre implémentation.
   
   Hello de sérialiser l’interface Java côté est défini en tant que :
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   Hello désérialiser interface en C\# côté est défini en tant que :
   
   public interface ICustomizedInteropCSharpDeserializer
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. **Sérialisation côté C\# et désérialisation côte Java**
   
   Hello la méthode de sérialisation dans C\# côté doit être spécifié en C\# code utilisateur :
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   Hello, méthode de désérialisation du côté Java doit être spécifié dans le fichier SPEC :
   
     (scp-spout
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   Nom hello de désérialiseur est « microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer » et « microsoft.scp.example.HybridTopology.Person » est que les données de salutation de classe cible hello sont désérialisées en.
   
   L’utilisateur peut également appliquer sa propre implémentation du sérialiseur C\# et du désérialiseur Java. Il s’agit d’interface hello pour C\# sérialiseur :
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   Il s’agit d’interface hello pour Java désérialiseur :
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a>Mode d’hébergement SCP
Dans ce mode, utilisateur peut compiler leur tooDLL de codes et utiliser SCPHost.exe fournie par la topologie de toosubmit SCP. fichier de spécification de Hello ressemble à ceci :

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

Ici, `plugin.name` est spécifié en tant que `SCPHost.exe` fourni par le Kit de développement logiciel (SDK) SCP. SCPHost.exe accepte exactement trois paramètres :

1. Bonjour tout d’abord une est hello nom de la DLL, qui est `"HelloWorld.dll"` dans cet exemple.
2. deuxième Hello est hello nom de la classe, qui est `"Scp.App.HelloWorld.Generator"` dans cet exemple.
3. Hello troisième un est hello nom d’une méthode statique publique, qui peut être appelée tooget une instance de ISCPPlugin.

En mode d'hébergement, le code utilisateur est compilé en tant que DLL, puis appelé par la plateforme SCP. Par conséquent plateforme de SCP peut obtenir un contrôle total de la logique de traitement entier hello. Nous vous recommandons de nos clients topologie toosubmit en mode d’hôte SCP, car elle peut simplifier l’expérience de développement hello et nous apporter plus de souplesse et une meilleure compatibilité descendante pour une version ultérieure ainsi.

## <a name="scp-programming-examples"></a>Exemples de programmation SCP
### <a name="helloworld"></a>HelloWorld
**HelloWorld** est un exemple très simple de tooshow un aperçu de SCP.Net. Il emploie une topologie non transactionnelle, avec un spout appelé **generator**, et deux bolts appelés **splitter** et **counter**. bec de Hello **Générateur** aléatoire génère des phrases et l’émettre ces phrases trop**fractionnement**. éclair de Hello **fractionnement** sera fractionnée hello phrases toowords et émettre ces mots trop**compteur** éclair. Hello éclair « counter » utilise un numéro d’occurrence dictionnaire toorecord hello de chaque mot.

L’exemple contient deux fichiers spec, **HelloWorld.spec** et **HelloWorld\_EnableAck.spec**. Bonjour C\# code, peuvent se trouver si l’accusé de réception est activé en obtenant hello pluginConf du côté de Java.

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

Dans un bec hello, si l’accusé de réception est activé, un dictionnaire est utilisé toocache hello tuples qui n’ont pas été reçu. Si Fail() est appelée, hello tuple ayant échoué doit être réexécutée :

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

### <a name="helloworldtx"></a>HelloWorldTx
Hello **HelloWorldTx** exemple illustre la topologie de transactionnelle tooimplement. Il contient un spout nommé **generator**, un bolt par lots nommé **partial-count** et un bolt de validation nommé **count-sum**. Il contient également trois fichiers txt : **DataSource0.txt**, **DataSource1.txt** et **DataSource2.txt**.

Lors de chaque transaction, hello bec **Générateur** sera de façon aléatoire choisissez deux fichiers hello trois fichiers créé au préalable et émettre hello deux fichiers noms toohello **partielle-count** éclair. éclair de Hello **partielle-count** sera tout d’abord obtenir un nom de fichier hello du tuple de salutation reçue, puis numéro de hello hello Ouvrir fichier et le nombre de mots dans ce fichier et enfin émettre toohello numéro du mot hello **somme-**éclair. Hello **-somme** éclair résume le nombre total de hello.

tooachieve **exactement une fois** sémantique, éclair de validation hello **-somme** devez toojudge s’il s’agit d’une transaction relue. Dans cet exemple, il est doté d'une variable de membre statique :

    public static long lastCommittedTxId = -1; 

Lorsqu’une instance de ISCPBatchBolt est créée, elle obtiendra hello `txAttempt` à partir des paramètres d’entrée :

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

Lorsque `FinishBatch()` est appelée, hello `lastCommittedTxId` sera mise à jour si elle n’est pas une transaction relue.

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


### <a name="hybridtopology"></a>HybridTopology
Cette topologie contient un spout Java et un bolt C\#. Il utilise hello par défaut sérialisation et désérialisation implémentation fournie par la plateforme de SCP. Veuillez hello de ref **HybridTopology.spec** dans **exemples\\HybridTopology** dossier hello spec les données de fichier, et **SubmitTopology.bat** de procédure toospecify Java classpath.

### <a name="scphostdemo"></a>SCPHostDemo
Cet exemple est fondamentalement hello identique HelloWorld. Hello seule différence est que le code utilisateur hello est compilé en tant que DLL et topologie de hello est envoyé à l’aide de SCPHost.exe. Veuillez section de hello ref « Mode de hôte SCP » pour une explication plus détaillée.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des exemples de topologies Storm créés à l’aide de SCP, voir hello :

* [Développement de topologies C# pour Apache Storm dans HDInsight à l'aide de Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Traitement d'événements à partir d'Azure Event Hubs avec Storm dans HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [Création de plusieurs flux de données dans une topologie C# Storm](hdinsight-storm-twitter-trending.md)
* [Utiliser les données de toovisualize Power Bi à partir d’une topologie Storm](hdinsight-storm-power-bi-topology.md)
* [Traitement des données de capteur de véhicule à partir d'Event Hubs à l'aide de Storm dans HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [Extraction, transformation et chargement (ETL) à partir d’Azure Event Hubs tooHBase](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [Corrélation des événements à l’aide de Storm et HBase sur HDInsight](hdinsight-storm-correlation-topology.md)

