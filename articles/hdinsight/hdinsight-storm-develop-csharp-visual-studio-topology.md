---
title: topologies de Storm aaaApache avec Visual Studio et c# - Azure HDInsight | Documents Microsoft
description: "Découvrez comment les topologies Storm toocreate en c#. Créer une topologie de nombre simple word dans Visual Studio à l’aide des outils de Hadoop hello pour Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a>Développer des topologies c# pour Visual Studio à l’aide des outils de Data Lake hello d’Apache Storm

Découvrez comment toocreate une topologie c# Storm à l’aide de hello Azure Data Lake (Hadoop) des outils pour Visual Studio. Ce document décrit hello processus de création d’un projet de Storm dans Visual Studio, tester localement et son déploiement tooan Apache Storm sur cluster Azure HDInsight.

Vous apprendrez également comment les topologies toocreate hybride qui utilisent des composants de c# et Java.

> [!NOTE]
> Étapes hello dans ce document reposent sur un environnement de développement Windows avec Visual Studio, projet compilé de hello sont soumis tooeither un cluster HDInsight de basés sur Windows ou Linux. Seuls les clusters basés sur Linux créés après le 28 octobre 2016 prennent en charge les topologies SCP.NET.

topologie toouse c# avec un cluster basé sur Linux, vous devez mettre à jour hello Microsoft.SCP.Net.SDK NuGet package utilisé par votre projet de tooversion 0.10.0.6 ou version ultérieur. version Hello du package de hello doit également correspondre version majeure de hello de Storm installé sur HDInsight.

| Version de HDInsight | Version de Storm | Version de SCP.NET | Version Mono par défaut |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| 3.3 |0.10.x |0.10.x.x</br>(uniquement sur HDInsight basé sur Windows) | N/D |
| 3.4 | 0.10.0.x | 0.10.0.x | 3.2.8 |
| 3,5 | 1.0.2.x | 1.0.0.x | 4.2.1 |
| 3.6 | 1.1.0.x | 1.0.0.x | 4.2.8 |

> [!IMPORTANT]
> Topologies c# sur des clusters basés sur Linux doivent utiliser .NET 4.5 et utiliser toorun Mono sur le cluster HDInsight de hello. Pour identifier des incompatibilités éventuelles, voir la page relative à la [compatibilité de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

## <a name="install-visual-studio"></a>Installation de Visual Studio

Vous pouvez développer les topologies c# avec SCP.NET en utilisant l’une de hello versions de Visual Studio suivantes :

* Visual Studio 2012 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)

* Visual Studio 2013 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)

* Visual Studio 2015 ou [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)

* Visual Studio 2017 (toute édition)

## <a name="install-data-lake-tools-for-visual-studio"></a>Installer Data Lake Tools pour Visual Studio

outils de Data Lake tooinstall pour Visual Studio, suivez les étapes de hello dans [prise en main des outils de LAC de données pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a name="install-java"></a>Installer Java

Lorsque vous soumettez une topologie Storm à partir de Visual Studio, SCP.NET génère un fichier zip qui contient les dépendances et la topologie de hello. Java est toocreate utilisé ces fichiers, de zip, car elle utilise un format qui n’est plus compatible avec les clusters basés sur Linux.

1. Installez hello Kit de développement Java (JDK) 7 ou version ultérieure sur votre environnement de développement. Vous pouvez obtenir hello JDK Oracle à partir de [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html). Vous pouvez également utiliser d’[autres distributions Java](http://openjdk.java.net/).

2. Hello `JAVA_HOME` environnement variable doit toohello de point de répertoire qui contient Java.

3. Hello `PATH` variable d’environnement doit inclure hello `%JAVA_HOME%\bin` active.

Vous pouvez utiliser hello suivant c# console les tooverify d’application que Java et hello JDK sont correctement installés :

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a>Modèles Storm

outils de Data Lake Hello pour Visual Studio fournissent des hello suivant de modèles :

| Type de projet | Illustre le |
| --- | --- |
| Application Storm |Projet de topologie Storm vide |
| Exemple d’enregistreur SQL Azure Storm |Comment toowrite tooAzure base de données SQL. |
| Exemple de lecteur Azure Cosmos DB Storm |Comment tooread à partir de la base de données Azure Cosmos. |
| Exemple d’enregistreur Azure Cosmos DB Storm |Comment toowrite tooAzure Cosmos DB. |
| Exemple de lecteur EventHub Storm |Comment tooread à partir d’Azure Event Hubs. |
| Exemple d’enregistreur EventHub Storm |Comment toowrite tooAzure concentrateurs d’événements. |
| Exemple de lecteur HBase Storm |Comment tooread HBase sur HDInsight à partir de clusters. |
| Exemple d’enregistreur HBase Storm |Comment les clusters tooHBase toowrite sur HDInsight. |
| Exemple Storm hybride |Comment toouse un composant Java. |
| Exemple Storm |Topologie de comptage de mots de base |

> [!WARNING]
> Tous les modèles ne fonctionnent pas avec HDInsight basé sur Linux. Les packages NuGet utilisés par les modèles hello n’est peut-être pas compatibles avec Mono. Vérifiez hello [compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/) de document et utiliser hello [Analyseur de portabilité .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify des problèmes potentiels.

Dans les étapes de hello dans ce document, vous utilisez hello base Storm Application projet type toocreate une topologie.

### <a name="hbase-templates-notes"></a>Remarques sur les modèles HBase

Hello HBase lecteur et les modèles de writer utilisent hello API REST HBase pas hello API Java HBase toocommunicate avec un HBase sur le cluster HDInsight.

### <a name="eventhub-templates-notes"></a>Remarques sur les modèles EventHub

> [!IMPORTANT]
> Hello basée sur Java de EventHub bec composant inclus dans le modèle d’EventHub lecteur peuvent ne pas fonctionne avec Storm sur HDInsight version 3.5 ou version ultérieure de hello. Une version mise à jour de ce composant est disponible dans la page [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).

Pour un exemple de topologie utilisant ce composant et fonctionnant avec Storm sur HDInsight 3.5, voir [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

## <a name="create-a-c-topology"></a>Création d’une topologie C#

1. Ouvrez Visual Studio, sélectionnez **Fichier** > **Nouveau**, puis **Projet**.

2. À partir de hello **nouveau projet** fenêtre, développez **installé** > **modèles**, puis sélectionnez **Azure Data Lake**. Dans la liste hello des modèles, sélectionnez **Storm Application**. Bas hello écran hello, entrez **WordCount** comme nom de l’application hello de hello.

    ![Capture d’écran de la fenêtre Nouveau projet](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. Une fois que vous avez créé le projet de hello, vous devez avoir hello fichiers suivants :

   * **Program.cs**: ce fichier définit la topologie hello pour votre projet. Par défaut, une topologie consistant en un seul spout et un seul bolt est créée.

   * **Spout.cs**: un spout d’exemple émettant des nombres aléatoires.

   * **Bolt.cs**: un éclair exemple qui conserve le nombre de numéros émis par bec de hello.

     Lorsque vous créez le projet de hello, téléchargements de NuGet hello dernières [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a>BEC hello de mettre en œuvre

1. Ouvrez **Spout.cs**. Becs verseurs sont données tooread utilisé dans une topologie à partir d’une source externe. composants principaux de Hello pour un bec sont :

   * **NextTuple**: appelé par Storm lorsque bec de hello est autorisé tooemit nouveaux tuples.

   * **L’accusé de réception** (topologie transactionnelle uniquement) : gère les accusés de réception initiées par d’autres composants dans une topologie hello pour les tuples envoyés à partir de bec de hello. Accuse réception d’un tuple informe bec de hello qu’il a été correctement traité par les composants en aval.

   * **Échec de** (topologie transactionnelle uniquement) : gère les tuples qui sont fail-le traitement des autres composants de la topologie de hello. Implémentation d’une méthode de basculement vous permet de toore-émettre hello tuple afin qu’elle peut être traitée à nouveau.

2. Remplacez le contenu hello Hello **bec** classe avec hello après le texte. Cet bec émet au hasard une phrase dans la topologie de hello.

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a>Implémentez hello boulons

1. Supprimer hello existant **Bolt.cs** fichier de projet de hello.

2. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **ajouter** > **un nouvel élément**. Dans la liste hello, sélectionnez **Storm éclair**, puis entrez **Splitter.cs** comme nom de hello. Répétez cette toocreate processus nommé d’un deuxième éclair **Counter.cs**.

   * **Splitter.cs** : implémente un bolt qui fractionne les phrases en mots et émet un nouveau flux de mots.

   * **Counter.cs**: implémente un éclair qui compte chaque mot et émet un flux de données de mots et le nombre de hello pour chaque mot.

     > [!NOTE]
     > Ces boulons lire et écrire des toostreams, mais vous pouvez également utiliser un toocommunicate éclair avec sources telles que la base de données ou service.

3. Ouvrez **Splitter.cs**. Il n’a qu’une seule méthode par défaut : **Execute**. Hello méthode Execute est appelée lorsque les éclair hello reçoit un tuple pour le traitement. Ici, vous pouvez lire et traiter des tuples entrants et émettre des tuples sortants.

4. Remplacer le contenu hello Hello **fractionnement** classe avec hello suivant de code :

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. Ouvrez **Counter.cs**et remplacez le contenu de classe hello par qui suit hello :

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a>Définir la topologie de hello

Becs verseurs et boulons sont organisés dans un graphique, qui définit comment les données de salutation transitent entre les composants. Dans cette topologie, le graphique de hello est la suivante :

![Diagramme illustrant l’organisation des composants](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

Les phrases sont émis à partir de bec de hello et sont distribuées tooinstances d’éclair de fractionnement hello. éclair de fractionnement Hello divise les phrases hello en mots, qui sont éclair de compteur toohello distribuée.

Étant donné que le nombre de mots est conservé localement dans l’instance de compteur hello, nous souhaitons toomake que par des mots spécifiques de flux toohello même instance de compteur d’éclair. afin de garantir que chaque instance suit un mot donné. Étant donné qu’éclair de fractionnement hello ne conserve aucun état, vraiment peu quelle instance de séparateur de hello reçoit le phrase.

Ouvrez **Program.cs**. méthode important Hello est **GetTopologyBuilder**, qui est la topologie de hello toodefine utilisé est soumis tooStorm. Remplacez le contenu hello de **GetTopologyBuilder** avec hello suivant la topologie de hello tooimplement code décrit précédemment :

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a>Envoyer de topologie hello

1. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **envoyer tooStorm sur HDInsight**.

   > [!NOTE]
   > Si vous y êtes invité, entrez les informations d’identification de l’hello pour votre abonnement Azure. Si vous avez plusieurs abonnements, connectez-vous toohello qui contient votre Storm sur le cluster HDInsight.

2. Sélectionnez votre Storm sur le cluster HDInsight à partir de hello **Cluster Storm** liste déroulante et sélectionnez **Submit**. Vous pouvez surveiller si l’envoi de hello réussit à l’aide de hello **sortie** fenêtre.

3. Lors de la topologie de hello a été envoyé avec succès, hello **Storm Topologies** pour le cluster de hello doit apparaître. Sélectionnez hello **WordCount** topologie de hello liste tooview informations hello topologie en cours d’exécution.

   > [!NOTE]
   > Vous pouvez également afficher les **Topologies Storm** dans l’**Explorateur de serveurs**. Développez **Azure** > **HDInsight**, cliquez avec le bouton droit sur un Storm sur le cluster HDInsight, puis sélectionnez **Afficher les topologies Storm**.

    tooview plus d’informations sur les composants de hello de topologie de hello, double-cliquez sur composant hello dans le diagramme de hello.

4. À partir de hello **récapitulatif de la topologie** afficher, cliquez sur **Kill** topologie de hello toostop.

   > [!NOTE]
   > Les topologies Storm continuer toorun jusqu'à ce qu’ils sont désactivés ou cluster de hello est supprimé.

## <a name="transactional-topology"></a>Topologie transactionnelle

topologie de précédente Hello est non transactionnelle. composants Hello dans la topologie de hello n’implémentent pas de messages tooreplaying de fonctionnalité. Pour obtenir un exemple d’une topologie transactionnelle, créez un projet et sélectionnez **Storm exemple** en tant que type de projet hello.

Topologies transactionnelles implémentent hello suivant toosupport la relecture des données :

* **La mise en cache des métadonnées**: bec de hello doit stocker des métadonnées sur les données de salutation émises, afin que les données de salutation peuvent être récupérées et émises à nouveau si une défaillance se produit. Étant donné que les données hello émises par exemple hello sont petites, les données brutes de hello pour chaque tuple sont stockées dans un dictionnaire pour la relecture.

* **L’accusé de réception**: chaque éclair dans une topologie de hello peut appeler `this.ctx.Ack(tuple)` tooacknowledge qu’il a correctement traité un tuple. Lorsque tous les boulons ont reçu hello tuple, hello `Ack` méthode de bec de hello est appelée. Hello `Ack` méthode permet de hello bec tooremove données qui a été mis en cache pour la relecture.

* **Échec de**: chaque éclair peut appeler `this.ctx.Fail(tuple)` tooindicate que le traitement a échoué pour un tuple. Échec de Hello propage toohello `Fail` méthode bec hello, où hello tuple puisse être relue à l’aide des métadonnées mises en cache.

* **ID de séquence** : lors de l’émission d’un tuple, un ID de séquence unique peut être spécifié. Cette valeur identifie un tuple hello pour le traitement de relecture (accusé de réception et échec). Par exemple, hello bec Bonjour **Storm exemple** projet utilise suivant de hello lors de l’émission de données :

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    Ce code émet un tuple qui contient un flux par défaut de toohello phrase, dont la valeur d’ID de séquence hello contenue dans **lastSeqId**. Dans cet exemple, **lastSeqId** est incrémenté pour chaque tuple émis.

Comme illustré dans hello **Storm exemple** projet d’équipe, si un composant est transactionnels peut être définie lors de l’exécution, en fonction de configuration.

## <a name="hybrid-topology-with-c-and-java"></a>Topologie hybride avec C# et Java

Vous pouvez également utiliser les outils de LAC de données pour les topologies Visual Studio toocreate hybride, où certains composants sont c# et d’autres sont Java.

Pour un exemple de topologie hybride, créez un projet, puis sélectionnez **Exemple Storm hybride**. Ce type de l’exemple montre comment hello suivant concepts :

* **Spout Java** et **bolt C#** : définis dans **HybridTopology_javaSpout_csharpBolt**.

    * Une version transactionnelle est définie dans **HybridTopologyTx_javaSpout_csharpBolt**.

* **Spout C#** et **bolt Java** : définis dans **HybridTopology_csharpSpout_javaBolt**.

    * Une version transactionnelle est définie dans **HybridTopologyTx_csharpSpout_javaBolt**.

  > [!NOTE]
  > Cette version montre également comment toouse Clojure code à partir d’un fichier texte comme un composant Java.


topologie hello tooswitch qui est utilisé lorsque le projet de hello est envoyé, il suffit de déplacer hello `[Active(true)]` instruction toohello topologie toouse, avant de le soumettre toohello cluster.

> [!NOTE]
> Tous les fichiers Java hello requises sont fournies dans le cadre de ce projet Bonjour **JavaDependency** dossier.

Considérez les éléments suivants de hello lorsque vous créez et envoi d’une topologie hybride :

* Vous devez utiliser **JavaComponentConstructor** toocreate une instance de hello classe Java pour un bec ou un éclair.

* Vous devez utiliser **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON les objets de données de tooserialize dans ou en dehors des composants Java à partir de Java.

* Lorsque vous soumettez un serveur de toohello hello topologie, vous devez utiliser hello **des configurations supplémentaires** hello de toospecify option **chemins d’accès de Java**. chemin d’accès Hello spécifié doit être le répertoire hello qui contient les fichiers JAR hello qui contiennent vos classes Java.

### <a name="azure-event-hubs"></a>Hubs d'événements Azure

SCP.NET version 0.9.4.203 introduit une nouvelle classe et la méthode spécifiquement pour l’utilisation avec bec de concentrateur d’événements hello (bec Java qui lit à partir de concentrateurs d’événements). Lorsque vous créez une topologie qui utilise un bec concentrateur d’événements, utilisez hello méthodes suivantes :

* **EventHubSpoutConfig** classe : crée un objet qui contient la configuration de hello de composant de bec hello.

* **TopologyBuilder.SetEventHubSpout** méthode : ajoute la topologie de toohello hello concentrateur d’événements bec de composant.

> [!NOTE]
> Vous devez toujours utiliser hello **CustomizedInteropJSONSerializer** tooserialize données produites par bec de hello.

## <a id="configurationmanager"></a>Utiliser ConfigurationManager

N’utilisez pas **ConfigurationManager** tooretrieve configuration des valeurs à partir de boulon et bec de composants. Cela est susceptible d’entraîner une exception de pointeur null. Au lieu de cela, la configuration hello pour votre projet est passée dans une topologie de Storm hello comme une paire clé / valeur dans le contexte de topologie hello. Chaque composant qui s’appuie sur des valeurs de configuration doit les récupérer à partir du contexte de hello lors de l’initialisation.

Hello de code suivant montre comment tooretrieve ces valeurs :

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

Si vous utilisez un `Get` tooreturn méthode une instance de votre composant, vous devez vous assurer qu’il passe à la fois hello `Context` et `Dictionary<string, Object>` constructeur toohello de paramètres. exemple Hello est un base `Get` méthode qui se passe correctement les valeurs suivantes :

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a>Comment tooupdate SCP.NET

Les dernières versions de SCP.NET prennent en charge la mise à niveau du package via NuGet. Vous recevez une notification de mise à niveau dès qu’une nouvelle mise à jour est disponible. vérification de toomanually pour une mise à niveau, procédez comme suit :

1. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **gérer les Packages NuGet**.

2. Dans le Gestionnaire de package hello, sélectionnez **mises à jour**. Si une mise à jour est disponible, elle est affichée. Cliquez sur **mise à jour** pour hello package tooinstall il.

> [!IMPORTANT]
> Si votre projet a été créé avec une version antérieure de SCP.NET qui n’utilise pas de NuGet, vous devez effectuer hello suivant la version la plus récente tooa tooupdate comme suit :
>
> 1. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **gérer les Packages NuGet**.
> 2. À l’aide de hello **recherche** champ, recherchez et ajoutez, **Microsoft.SCP.Net.SDK** toohello projet.

## <a name="troubleshoot-common-issues-with-topologies"></a>Dépanner des problèmes courants avec les topologies

### <a name="null-pointer-exceptions"></a>Exceptions de pointeur null

Lorsque vous utilisez une topologie c# avec un cluster HDInsight de basés sur Linux, boulon et bec des composants qui utilisent **ConfigurationManager** tooread les paramètres de configuration lors de l’exécution peuvent retourner des exceptions de pointeur null.

configuration Hello pour votre projet est passée dans la topologie de Storm hello comme une paire clé / valeur dans le contexte de topologie hello. Il peut être récupéré à partir de l’objet dictionnaire hello passé tooyour composants lorsqu’elles sont initialisées.

Pour plus d’informations, consultez hello [ConfigurationManager](#configurationmanager) section de ce document.

### <a name="systemtypeloadexception"></a>System.TypeLoadException

Lorsque vous utilisez une topologie c# avec un cluster HDInsight de basés sur Linux, vous pouvez rencontrer hello l’erreur suivante :

    System.TypeLoadException: Failure has occurred while loading a type.

Cette erreur se produit lorsque vous utilisez un fichier binaire qui n’est pas compatible avec la version de hello de .NET Mono prend en charge.

Pour les clusters HDInsight basés sur Linux, vous devez vous assurer que votre projet utilise des fichiers binaires compilés pour .NET 4.5.

### <a name="test-a-topology-locally"></a>Test local d’une topologie

Bien qu’il soit facile toodeploy un cluster de tooa topologie, dans certains cas, vous devrez peut-être tootest une topologie localement. Utilisez hello suivant les étapes toorun et tester l’exemple de topologie hello dans ce didacticiel localement dans votre environnement de développement.

> [!WARNING]
> Le test local fonctionne uniquement pour les topologies exclusivement C# de base. Vous ne pouvez pas employer le test local pour les topologies hybrides ou celles qui utilisent plusieurs flux de données.

1. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **propriétés**. Dans Propriétés du projet hello, modifiez hello **type de sortie** trop**Application Console**.

    ![Capture d’écran des propriétés du projet, avec le type de sortie en surbrillance](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > N’oubliez pas de toochange hello **type de sortie** sauvegarder trop**bibliothèque de classes** avant de déployer hello topologie tooa cluster.

2. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **ajouter** > **un nouvel élément**. Sélectionnez **classe**, puis entrez **LocalTest.cs** en tant que nom de la classe hello. Enfin, cliquez sur **Ajouter**.

3. Ouvrez **LocalTest.cs**et ajoutez hello suivant **à l’aide de** instruction hello début :

    ```csharp
    using Microsoft.SCP;
    ```

4. Suivant de hello d’utilisation de code en tant que contenu hello Hello **LocalTest** classe :

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    Prendre un tooread moment par le biais des commentaires de code hello. Ce code utilise **LocalContext** toorun des composants de hello dans l’environnement de développement hello et il persiste le flux de données hello entre composants tootext fichiers sur le disque local hello.

1. Ouvrez **Program.cs**et ajoutez hello suivant toohello **Main** méthode :

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. Enregistrer les modifications de hello, puis cliquez sur **F5** ou sélectionnez **déboguer** > **démarrer le débogage** projet hello de toostart. Une fenêtre de console doit apparaître et l’état du journal en tant que la progression des tests hello. Lorsque **Tests terminé** s’affiche, appuyez sur n’importe quelle fenêtre de hello tooclose clé.

3. Utilisez **l’Explorateur Windows** directory hello toolocate qui contient votre projet. Par exemple : **C:\Utilisateurs\<votre_nom_utilisateur>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**. Dans ce répertoire, ouvrez **Bin**, puis cliquez sur **Débogage**. Vous devez voir les fichiers de texte hello qui ont été générés lors de l’exécution de tests de hello : sentences.txt, counter.txt et splitter.txt. Ouvrez chaque fichier texte et inspecter les données de salutation.

   > [!NOTE]
   > Les chaînes de données sont conservées sous forme de tableau de valeurs décimales dans ces fichiers. Par exemple, \[[97,103,111]] Bonjour **splitter.txt** fichier hello est *et*.

> [!NOTE]
> Être vraiment tooset hello **type de projet** sauvegarder trop**bibliothèque de classes** avant de déployer tooa Storm sur le cluster HDInsight.

### <a name="log-information"></a>Enregistrement d’informations

Vous pouvez facilement enregistrer des informations à partir de vos composants de topologie à l’aide de `Context.Logger`. Par exemple, suivant de hello crée une entrée de journal d’information :

```csharp
Context.Logger.Info("Component started");
```

Informations enregistrées peuvent être consultées dans hello **journal du Service Hadoop**, qui se trouve dans **l’Explorateur de serveurs**. Entrée de hello pour votre Storm sur le cluster HDInsight, puis **journal du Service Hadoop**. Enfin, sélectionnez tooview de fichier journal hello.

> [!NOTE]
> Hello journaux sont stockés dans hello compte de stockage Azure qui est utilisé par votre cluster. journaux de hello tooview dans Visual Studio, vous devez vous connecter toohello abonnement Azure propriétaire du compte de stockage hello.

### <a name="view-error-information"></a>Afficher les informations relatives aux erreurs

tooview les erreurs qui se sont produites dans une topologie en cours d’exécution, utilisez hello comme suit :

1. À partir de **l’Explorateur de serveurs**, avec le bouton droit hello Storm sur le cluster HDInsight, puis sélectionnez **topologies de vue Storm**.

2. Pourquoi **bec** et **boulons**, hello **dernière erreur** colonne contienne des informations sur la dernière erreur de hello.

3. Sélectionnez hello **Id de bec** ou **éclair Id** pour le composant hello qui comporte une erreur répertoriée. Sur page de détails hello erreur affichée, d’autres informations sont répertoriées dans hello **erreurs** section bas hello de page de hello.

4. tooobtain plus d’informations, sélectionnez un **Port** de hello **exécuteurs** section de la page de hello, journal toosee hello Storm travail hello dernières minutes.

### <a name="errors-submitting-topologies"></a>Erreurs lors de la soumission des topologies

Si vous rencontrez des erreurs soumettant une tooHDInsight topologie, vous trouverez les journaux pour les composants côté serveur hello qui gèrent la soumission de topologie sur votre cluster HDInsight. tooretrieve ces journaux, hello utilisez commande suivante à partir d’une ligne de commande :

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

Remplacez __sshuser__ avec hello compte d’utilisateur SSH pour le cluster de hello. Remplacez __clustername__ avec nom hello du cluster HDInsight de hello. Pour en savoir plus sur l’utilisation de `scp` et de `ssh` avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Les envois peuvent échouer pour plusieurs raisons :

* JDK n’est pas installé ou n’est pas dans le chemin d’accès hello.
* Dépendances de Java requises ne sont pas inclus dans l’envoi de hello.
* Dépendances incompatibles.
* Dupliquer les noms de topologie.

Si hello `hdinsight-scpwebapi.out` journal contient un `FileNotFoundException`, cela peut être dû à hello conditions suivantes :

* Hello JDK n’est pas un chemin d’accès de hello sur l’environnement de développement hello. Vérifiez que hello JDK est installé dans l’environnement de développement hello et que `%JAVA_HOME%/bin` est dans le chemin d’accès hello.
* Il manque une dépendance Java. Assurez-vous que vous incluez tous les fichiers .jar requis dans le cadre de l’envoi de hello.

## <a name="next-steps"></a>Étapes suivantes

Pour un exemple de traitement des données à partir des Event Hubs, voir [Traiter des événements d’Azure Event Hubs avec Storm sur HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).

Pour obtenir un exemple de topologie C# qui fractionne les données de flux en plusieurs flux de données, consultez la rubrique [Exemple c# Storm](https://github.com/Blackmist/csharp-storm-example).

toodiscover plus d’informations sur la création de topologies de c#, consultez [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).

Pour plus toowork manières avec HDInsight et Storm plus sur les échantillons de HDInsight, consultez hello suivant des documents :

**Microsoft SCP.NET**

* [Guide de programmation SCP](hdinsight-storm-scp-programming-guide.md)

**Apache Storm sur HDInsight**

* [Déploiement et analyse des topologies avec Apache Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology.md)
* [Exemples de topologies pour Storm dans HDInsight](hdinsight-storm-example-topology.md)

**Apache Hadoop sur HDInsight**

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)

**Apache HBase sur HDInsight**

* [Prise en main de HBase sur HDInsight](hdinsight-hbase-tutorial-get-started.md)
