---
title: services de Service Fabric aaaPartitioning | Documents Microsoft
description: "Décrit comment les services avec état toopartition Service Fabric. Partitions Active le stockage des données sur les ordinateurs locaux hello données et calcul peuvent être mis à l’ensemble."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a>Partitionnement des services fiables Service Fabric
Cet article fournit une toohello présentation des concepts de base du partitionnement des services fiables Azure Service Fabric. Hello code source utilisé dans l’article de hello est également disponible sur [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="partitioning"></a>Partitionnement
Le partitionnement n’est pas unique tooService l’ensemble fibre optique. En réalité, il s’agit d’un modèle de base de création de services évolutifs. Dans un sens large, nous pouvons considérer comme un concept de la division de l’état (données) de partitionnement et de calcul dans les performances et l’évolutivité de plus petite unités accessible tooimprove. Le [partitionnement des données][wikipartition] constitue une forme bien connue de partitionnement.

### <a name="partition-service-fabric-stateless-services"></a>Partitionnement des services sans état Service Fabric
Pour les services sans état, vous pouvez considérer une partition comme une unité logique contenant une ou plusieurs instances d’un service. La figure 1 illustre un service sans état avec cinq instances distribuées sur un cluster à l’aide d’une seule partition.

![Service sans état](./media/service-fabric-concepts-partitioning/statelessinstances.png)

Il existe en réalité deux types de solutions de service sans état. Hello tout d’abord un est un service qui rend son état persistant en externe, par exemple dans une base de données SQL Azure (par exemple, un site Web qui stocke les données et les informations de session hello). Hello seconde est services calcul uniquement (comme un réduire en vignettes calculatrice ou image) qui ne gèrent pas tout état persistant.

Dans les deux cas, le partitionnement d’un service sans état constitue un scénario extrêmement rare. L’évolutivité et la disponibilité passent normalement par une augmentation du nombre d’instances. Hello uniquement heure tooconsider plusieurs partitions pour les instances de service sans état est lorsque vous devez toomeet spécial routage des demandes.

Par exemple, imaginez un cas de figure où des utilisateurs dont les identifiants sont compris dans une certaine plage doivent être uniquement pris en charge par une instance de service particulière. Un autre exemple de lorsque vous pouvez partitionner un service sans état est lorsque vous avez un backend réellement partitionné (par exemple, un partitionnée SQL de base de données) et que vous souhaitez toocontrol quelle instance de service doit écrire des partitions de base de données toohello--ou effectuer d’autres tâches de préparation dans Hello service sans état nécessitant hello même informations de partitionnement est utilisé dans le service principal hello. Ces types de scénarios peuvent également être résolus de différentes façons et n’impliquent pas nécessairement un partitionnement du service.

reste Hello de cette procédure pas à pas se concentre sur les services avec état.

### <a name="partition-service-fabric-stateful-services"></a>Partitionnement des services avec état Service Fabric
Service Fabric rend toodevelop facilement des services évolutifs avec état en offrant un moyen de première classe toopartition état (données). Point de vue conceptuel, vous pouvez considérer une partition d’un service avec état comme une unité d’échelle hautement fiable via [réplicas](service-fabric-availability-services.md) qui sont distribuées et équilibrée entre les nœuds hello dans un cluster.

Partitionnement dans le contexte de hello des services avec état de l’infrastructure de Service, toohello les processus permettant de déterminer qu’une partition de service particulier est chargée pour une partie de l’état du service de hello hello fait référence. (Comme indiqué précédemment, une partition est un ensemble de [réplicas](service-fabric-availability-services.md)). Une bonne chose sur le Service Fabric est qu’il place les partitions hello sur différents nœuds. Cela leur permet de limite de ressource du nœud toogrow tooa. Comme les données de salutation besoins augmentent, la croissance des partitions et Service Fabric rééquilibrage des partitions sur les nœuds. Cela garantit hello suite à une utilisation efficace des ressources matérielles.

toogive vous obtenir un exemple, vous dites commencent par un cluster à 5 nœuds et un service qui est configuré toohave 10 partitions et une cible de trois réplicas. Dans ce cas, l’infrastructure de Service serait équilibrer et distribuer des réplicas de hello sur le cluster de hello--et vous obtenez des deux principaux [réplicas](service-fabric-availability-services.md) par nœud.
Si vous devez maintenant tooscale des nœuds de cluster de too10 hello, Service Fabric serait rééquilibrer hello principal [réplicas](service-fabric-availability-services.md) sur tous les nœuds de 10. De même, si vous à l’échelle les nœuds too5 arrière, Service Fabric serait rééquilibrer tous les réplicas hello entre les nœuds hello 5.  

Figure 2 montre la distribution hello de 10 partitions avant et après la mise à l’échelle de cluster de hello.

![Service avec état](./media/service-fabric-concepts-partitioning/partitions.png)

Par conséquent, hello montée en puissance parallèle est possible dans la mesure où les demandes des clients sont réparties sur plusieurs ordinateurs, les performances globales de l’application hello sont améliorée et la contention sur toochunks d’accès de données est réduite.

## <a name="plan-for-partitioning"></a>Planification du partitionnement
Avant d’implémenter un service, vous devez toujours envisager hello stratégie est requise tooscale out de partitionnement. Il existe différentes manières, mais tous les se concentrent sur l’application hello doit tooachieve. Pour le contexte de hello de cet article, prenons l’exemple hello certains aspects les plus importants.

Une bonne approche est toothink sur la structure hello d’état hello toobe partitionnée, en tant que première étape de hello.

Prenons un exemple simple : Si vous étiez toobuild un service pour un sondage countywide, vous pouvez créer une partition pour chaque ville dans la région de hello. Ensuite, vous pouvez stocker des votes hello pour chaque personne dans Ville hello dans partition hello correspondant toothat ville. La figure 3 illustre un ensemble de personnes et hello ville dans lesquels ils résident.

![Partition simple](./media/service-fabric-concepts-partitioning/cities.png)

Comme la population hello des villes varie largement, vous risquez avec certaines partitions qui contiennent un grand nombre de données (par exemple, Seattle) et des autres partitions avec très peu état (par exemple, Kirkland). Qu’est impact hello d’avoir des partitions avec des volumes irréguliers d’état ?

Si vous pensez à nouveau sur hello exemple, vous pouvez facilement voir que partition hello contient hello des votes pour Seattle obtenez davantage de trafic que Kirkland hello une. Par défaut, l’infrastructure de Service permet de s’assurer qu’il existe sur hello même nombre de réplicas principaux et secondaires sur chaque nœud. Par conséquent, vous pouvez obtenir des nœuds qui contiennent des réplicas qui servent plus de trafic et d’autres qui en servent moins. Vous pourriez préférence tooavoid à chaud et à froid taches comme suit dans un cluster.

Dans commande tooavoid cela, vous devez faire deux choses, d’un point de vue de partitionnement :

* Essayez d’état de hello toopartition afin qu’elle est répartie équitablement entre toutes les partitions.
* Charge de rapports à partir de chacun des réplicas hello pour le service de hello. (Pour plus d'informations sur la procédure à suivre, consultez cet article sur [Métriques et charge](service-fabric-cluster-resource-manager-metrics.md)). Service Fabric fournit la charge de tooreport hello capacité consommée par les services, tels que la quantité de mémoire ou le nombre d’enregistrements. En fonction de mesures hello signalées, Service Fabric détecte que certaines partitions servent des charges plus élevées que d’autres rééquilibre cluster hello par déplacement réplicas toomore approprié nœuds, afin que globalement aucun nœud n’est surchargé.

Il arrive que la quantité de données dans une partition donnée ne soit pas connue. Par conséquent, une recommandation générale est toodo à la fois--tout d’abord, en adoptant une stratégie de partitionnement qui répartit hello données uniformément sur les partitions hello et, ensuite, par charge de création de rapports.  méthode première Hello empêche les situations décrites dans hello vote exemple, alors que hello ensuite permet de lisser les différences temporaires de l’accès ou de la charge au fil du temps.

Un autre aspect de la planification de la partition est le nombre correct de hello toochoose de toobegin de partitions avec.
Du point de vue de Service Fabric, rien ne vous empêche de commencer par un nombre de partitions plus élevé que prévu pour votre scénario.
En fait, en supposant que le nombre maximal de hello de partitions est une approche valide.

Bien que ces cas soient rares, il peut arriver que vous ayez besoin de plus de partitions que prévu. Vous ne pouvez pas modifier le nombre de partitions hello après les faits hello, vous devez tooapply certaines approches partition avancées, telles que la création d’une nouvelle instance de service de hello même type de service. Vous devez également tooimplement une logique côté client qui achemine hello toohello correct instance de service, en fonction des connaissances côté client que votre code client doit gérer les demandes.

Une autre considération pour le partitionnement de planification est ressources de l’ordinateur disponible hello. État de hello besoins toobe accès et au stockage, vous êtes toofollow liée :

* Les limites de bande passante du réseau
* Les limites de mémoire système
* Les limites de stockage du disque

Que se passe-t-il si vous rencontrez des contraintes de ressources dans un cluster en cours d’exécution ? les réponses Hello sont que vous pouvez simplement faire évoluer hello tooaccommodate hello nouvelle configuration requise des clusters.

[guide de planification de capacité Hello](service-fabric-capacity-planning.md) propose des conseils sur la manière de toodetermine le nombre de nœuds a besoin de votre cluster.

## <a name="get-started-with-partitioning"></a>Prise en main du partitionnement
Cette section décrit comment tooget démarrer avec le partitionnement de votre service.

Service Fabric propose trois schémas de partition, au choix :

* Partitionnement par plage (également appelé UniformInt64Partition).
* Partitionnement nommé. Les applications qui utilisent ce modèle comportent généralement des données qui peuvent être compartimentées au sein d’un ensemble limité. Les régions, les codes postaux, les groupes de clients ou les autres limites de l’entreprise constituent des exemples courants de champs de données utilisés comme clés de partition nommées.
* Partitionnement singleton. Les partitions singleton sont généralement utilisées lorsque le service de hello ne nécessite pas un routage supplémentaires. Par exemple, les services sans état utilisent ce schéma de partitionnement par défaut.

Les schémas de partitionnement nommé et singleton sont des formes spéciales de partitions par plage. Par défaut, les modèles de Visual Studio hello pour une utilisation de l’infrastructure de Service trouver le partitionnement, car il s’agit de hello celle la plus courante et utile. reste Hello de cet article se concentre sur le schéma de partitionnement méthode hello.

### <a name="ranged-partitioning-scheme"></a>Schéma de partitionnement par plage
Il s’agit de toospecify utilisé entier plage (identifiées par une clé faible et une clé haute) et un nombre de partitions (n). Il crée des partitions n, chacun d'entre eux une sous-plage sans chevauchement de hello globale de plage de clés de partition. Par exemple, un schéma de partitionnement par plage doté d’une clé basse de 0, d’une clé haute de 99 et d’un nombre total de 4 créera quatre partitions, telles qu’elles sont illustrées ci-dessous.

![Partitionnement par plage](./media/service-fabric-concepts-partitioning/range-partitioning.png)

Une approche courante consiste à toocreate un hachage basé sur une clé unique dans le jeu de données hello. Un numéro d’immatriculation de véhicule, l’identifiant d’un d’employé ou une chaîne unique sont des exemples courants de clés. À l’aide de cette clé unique, vous puis génère un code de hachage, plage de clés modulo hello toouse comme clé. Vous pouvez spécifier hello supérieur et les limites inférieures de hello autorisée plage de clés.

### <a name="select-a-hash-algorithm"></a>Sélection d’un algorithme de hachage
Une partie importante du hachage consiste à sélectionner l'algorithme de hachage. Un facteur important n’est l’objectif de hello toogroup des clés similaires proches (localité sensibles hachage)--ou si l’activité doit être distribuée globalement sur toutes les partitions (hachage de distribution), ce qui est plus courant.

caractéristiques de Hello un bonne distribution d’algorithme de hachage sont qu’il est facile toocompute, il est peu de collisions, et il distribue uniformément les clés de hello. Un bon exemple d’un algorithme de hachage efficace est hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) algorithme de hachage.

Une bonne ressource pour le choix d’algorithme de code de hachage général est hello [page Wikipedia sur les fonctions de hachage](http://en.wikipedia.org/wiki/Hash_function).

## <a name="build-a-stateful-service-with-multiple-partitions"></a>Création d’un service avec état avec plusieurs partitions
Nous allons créer le premier service fiable avec état à plusieurs partitions. Dans cet exemple, vous allez générer une application très simple où vous souhaitez toostore tous les noms qui commencent par Bonjour identique Bonjour même partition.

Avant d’écrire de code, vous devez toothink sur les partitions hello et les clés de partition. Vous avez besoin de 26 partitions (une pour chaque lettre dans l’alphabet de hello), mais comment faire sur hello clés haute et basse ?
Comme nous voulons littéralement toohave une seule partition par lettre, nous pouvons utiliser 0 comme clé basse de hello et 25 en tant que clé haute de hello, car chaque lettre est sa propre clé.

> [!NOTE]
> Il s’agit d’un scénario simplifié, comme dans la réalité, distribution de hello serait irréguliers. Noms commençant par les lettres hello « S » ou « M » sont plus courantes que hello ceux commençant par « X » ou « Y ».
> 
> 

1. Ouvrez **Visual Studio** > **Fichier** > **Nouveau** > **Projet**.
2. Bonjour **nouveau projet** boîte de dialogue, choisissez l’application de Service Fabric hello.
3. Appelez le projet de hello « AlphabetPartitions ».
4. Bonjour **créer un Service** boîte de dialogue, choisissez **avec état** de service et appelez-le « Alphabet.Processing » comme indiqué dans l’image hello ci-dessous.
       ![Boîte de dialogue Nouveau service dans Visual Studio][1]

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. Définir le nombre hello de partitions. Fichier Applicationmanifest.xml de hello ouvrir situé dans hello dossier ApplicationPackageRoot hello AlphabetPartitions mise à jour et projet hello du paramètre de Processing_PartitionCount too26 comme indiqué ci-dessous.
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    Vous devez également tooupdate hello LowKey et HighKey des propriétés d’élément de StatefulService hello Bonjour ApplicationManifest.xml comme indiqué ci-dessous.
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. Pour toobe de service hello accessible, ouvrez un point de terminaison sur un port en ajoutant l’élément de point de terminaison hello de ServiceManifest.xml (situé dans le dossier de PackageRoot hello) pour hello Alphabet.Processing service comme indiqué ci-dessous :
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    Service de hello est désormais un point de terminaison configuré toolisten tooan interne avec 26 partitions.
7. Ensuite, vous devez toooverride hello `CreateServiceReplicaListeners()` méthode de classe de traitement hello.
   
   > [!NOTE]
   > Pour cet exemple, supposons que vous utilisiez un HttpCommunicationListener simple. Pour plus d’informations sur la communication fiable, consultez [modèle de communication de Service fiable hello](service-fabric-reliable-services-communication.md).
   > 
   > 
8. Un modèle recommandé pour les URL hello qui écoute un réplica est hello suivant le format : `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.
    Vous pouvez tooconfigure votre toolisten d’écouteur de communication sur les points de terminaison corrects hello et avec ce modèle.
   
    Plusieurs réplicas de ce service peuvent être hébergés sur hello même ordinateur, par conséquent, cette adresse doit toobe toohello unique réplica. C’est pourquoi l’ID de partition + ID de réplica est dans l’URL de hello. HttpListener peut écouter sur plusieurs adresses hello que même port tant que préfixe d’URL hello est unique.
   
    Hello qu'existe-t-il GUID supplémentaire pour des cas où les réplicas secondaires écoutent également pour les demandes en lecture seule. Lorsque c’est le cas de hello, vous souhaitez toomake qu’une nouvelle adresse unique est utilisé lors du passage d’une adresse de principal toosecondary tooforce clients toore résoudre hello. '+' est utilisée comme adresse hello ici afin que hello réplica écoute sur tous les ordinateurs hôtes disponibles (IP, FQDM, localhost, etc.) hello de code ci-dessous montre un exemple.
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    Il est également important de noter que hello publié URL est légèrement différente de préfixe d’URL hello écoute.
    URL d’écoute Hello est donné tooHttpListener. Hello que publiée URL est hello qui est publiée toohello Service Naming Service Fabric, qui est utilisé pour la découverte de service. Les clients demanderont cette adresse via ce service de découverte. adresse Hello que les clients obtiennent des besoins toohave hello réel l’adresse IP ou nom de domaine complet du nœud de hello dans l’ordre tooconnect. Par conséquent, vous devez tooreplace '+' avec hello du nœud à l’adresse IP ou nom de domaine complet comme indiqué ci-dessus.
9. dernière étape de Hello est hello tooadd logique toohello service comme indiqué ci-dessous de traitement.
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    `ProcessInternalRequest`lectures hello valeurs hello requête chaîne paramètre utilisé toocall hello partition et les appels `AddUserAsync` dictionnaire fiable de tooadd hello lastname toohello `dictionary`.
10. Vous allez ajouter un toosee de projet de service sans état toohello comment vous pouvez appeler une partition particulière.
    
    Ce service sert à une interface web simple qui accepte lastname hello comme paramètre de chaîne de requête, détermine la clé de partition hello et il envoie le service de Alphabet.Processing toohello pour le traitement.
11. Bonjour **créer un Service** boîte de dialogue, choisissez **Stateless** de service et appelez-le « Alphabet.Web » comme indiqué ci-dessous.
    
    ![Capture d’écran de service sans état](./media/service-fabric-concepts-partitioning/createnewstateless.png).
12. Mettre à jour les informations de point de terminaison hello Bonjour ServiceManifest.xml de hello Alphabet.WebApi service tooopen configuration d’un port comme indiqué ci-dessous.
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. Vous devez tooreturn une collection de ServiceInstanceListeners dans la classe de hello Web. Là encore, vous pouvez choisir tooimplement un HttpCommunicationListener simple.
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. Vous devez maintenant la logique de traitement tooimplement hello. Hello HttpCommunicationListener appelle `ProcessInputRequest` lorsqu’une demande arrive. Par conséquent, commençons et ajoutez le code hello ci-dessous.
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    Voici la procédure pas à pas. code de Hello lit hello première lettre du paramètre de chaîne de requête hello `lastname` en char. Ensuite, il détermine la clé de partition hello pour cette lettre en soustrayant la valeur hexadécimale hello `A` à partir de la valeur hexadécimale hello initiales des noms de famille hello.
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    N’oubliez pas que, dans cet exemple, nous utilisons 26 partitions avec une seule clé de partition par partition.
    Ensuite, nous obtenons la partition de service hello `partition` pour cette clé à l’aide de hello `ResolveAsync` méthode sur hello `servicePartitionResolver` objet. `servicePartitionResolver` est défini comme
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    Hello `ResolveAsync` méthode prend hello URI du service, clé de partition hello et un jeton d’annulation en tant que paramètres. Hello URI du service de service de traitement de hello est `fabric:/AlphabetPartitions/Processing`. Ensuite, nous obtenons le point de terminaison hello de partition de hello.
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    Enfin, nous générer des URL de point de terminaison hello plus hello querystring et appeler le service de traitement de hello.
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    Une fois que le traitement de hello est terminé, nous réécrire les sortie hello.
15. dernière étape de Hello est service de hello tootest. Visual Studio utilise les paramètres d’application pour un déploiement local et sur le cloud. service de hello tootest avec des 26 partitions localement, vous devez tooupdate hello `Local.xml` fichier dans le dossier de ApplicationParameters de hello du projet de AlphabetPartitions hello, comme indiqué ci-dessous :
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. Une fois que vous avez terminé le déploiement, vous pouvez vérifier le service de hello et toutes ses partitions Bonjour Service Fabric Explorer.
    
    ![Capture d’écran de l’explorateur Service Fabric](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. Dans un navigateur, vous pouvez tester hello partitionnement logique en entrant `http://localhost:8081/?lastname=somename`. Vous verrez que chaque nom qui commence par hello même lettre sont stockée dans hello même partition.
    
    ![Capture d’écran du navigateur](./media/service-fabric-concepts-partitioning/samplerunning.png)

code source entière de Hello de l’exemple hello est disponible sur [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les concepts de l’infrastructure de Service, voir hello :

* [Disponibilité des services Service Fabric](service-fabric-availability-services.md)
* [Extensibilité des services Service Fabric](service-fabric-concepts-scalability.md)
* [Planification de la capacité pour les applications Service Fabric](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png