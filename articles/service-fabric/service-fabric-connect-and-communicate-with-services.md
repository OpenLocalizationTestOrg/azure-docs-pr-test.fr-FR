---
title: aaaConnect et communiquer avec les services dans Azure Service Fabric | Documents Microsoft
description: "Découvrez comment tooresolve, se connecter et communiquer avec les services dans l’infrastructure de Service."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>Se connecter aux services et communiquer avec eux dans Service Fabric.
Dans Service Fabric, un service s’exécute quelque part dans un cluster Service Fabric, généralement réparti sur plusieurs machines virtuelles. Elle peut être déplacée à partir d’un seul emplacement tooanother, soit par le propriétaire du service hello, ou automatiquement par l’infrastructure de Service. Les services ne sont pas un ordinateur particulier tooa statiquement liée ou l’adresse.

Une application Service Fabric est généralement composée de nombreux services différents qui effectuent chacun une tâche spécialisée. Ces services peuvent communiquer avec eux tooform une fonction complète, telles que les différentes parties de rendu d’une application web. Il existe également des applications qui se connectent tooand communiquent avec les services de client. Ce document explique comment tooset la communication avec et entre vos services dans l’infrastructure de Service.

Cette vidéo Microsoft Virtual Academy aborde également la communication de service :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>Apportez votre propre protocole
L’infrastructure de service vous permet de gérer des hello du cycle de vie de vos services, mais il n’apporte décisions sur le rôle de vos services. Cela inclut la communication. Lorsque votre service est ouvert par l’infrastructure de Service, qui est tooset d’opportunité de votre service un point de terminaison pour les demandes entrantes, à l’aide de toute pile de communication ou de protocole souhaité. Votre service écoute sur une adresse **IP:port** normale à l’aide d’un schéma d’adressage quelconque, tel qu’un URI. Plusieurs instances de service ou les réplicas peuvent partager un processus hôte, auquel cas ils seront devez toouse des ports différents ou utilisent un mécanisme de partage de ports, tels que des pilotes de noyau http.sys hello dans Windows. Dans les deux cas, chaque instance de service ou réplica dans un processus hôte doit être adressable de manière unique.

![points de terminaison de service][1]

## <a name="service-discovery-and-resolution"></a>Détection et résolution de service
Dans un système distribué, les services peuvent déplacer à partir d’un ordinateur tooanother au fil du temps. Cela peut se produire pour diverses raisons, y compris l’équilibrage des ressources, les mises à niveau, les basculements ou l’augmentation des tailles des instances. Cela signifie que de modifier les adresses de point de terminaison de service comme service de hello déplace toonodes avec des adresses IP différentes et peut s’ouvrir sur des ports différents, si le service de hello utilise un port sélectionné de manière dynamique.

![Répartition des services][7]

L’infrastructure de service fournit une découverte et la résolution de service appelé hello Naming Service. Hello Naming Service conserve une table qui mappe nommés instances de service ils écoutent des adresses de point de terminaison toohello. Toutes les instances de service nommées dans Service Fabric ont des noms uniques représentés par les URI. Par exemple : `"fabric:/MyApplication/MyService"`. nom de Hello du service de hello ne change pas sur la durée de vie hello du service de hello, seules les adresses de point de terminaison hello qui peuvent changer lorsque vous déplacement des services. Il s’agit de toowebsites analogue qui ont des URL constants, mais où l’adresse IP de hello peut changer. Et tooDNS similaires sur web hello, qui résout les adresses de tooIP URL de site Web, Service Fabric a un bureau d’enregistrement qui mappe l’adresse de point de terminaison de service noms tootheir.

![points de terminaison de service][2]

Résolution et la connexion tooservices implique hello s’exécuter dans une boucle comme suit :

* **Résoudre**: point de terminaison Get hello un service publié à partir de hello Naming Service.
* **Se connecter**: se connecter toohello service sur tout ce qui les utilise sur ce point de terminaison de protocole.
* **Recommencez**: une tentative de connexion peut échouer pour plusieurs raisons, par exemple, si le service de hello a été déplacé, car l’adresse du point de terminaison hello hello dernière heure a été résolu. Dans ce cas, hello précédant la résolution et connectez-vous étapes doivent toobe retentée, et ce cycle se répète jusqu'à ce que la connexion de hello réussit.

## <a name="connecting-tooother-services"></a>Connecter les services tooother
Services connexion tooeach autres à l’intérieur d’un cluster généralement pouvez accéder directement aux points de terminaison hello d’autres services hello les nœuds dans un cluster étant sur hello même réseau local. toomake est tooconnect plus facilement entre les services, Service Fabric fournit des services supplémentaires qui utilisent hello Naming Service. un service DNS et un service de proxy inverse.


### <a name="dns-service"></a>Service DNS
Étant donné que de nombreux services, en particulier en conteneur services, peuvent avoir un nom d’URL existant, qui est en mesure de tooresolve à l’aide de hello protocole DNS standard (plutôt que hello Naming Service protocol) sont très pratiques, en particulier dans l’application « de courbes d’élévation et MAJ » scénarios. C’est exactement quel service DNS hello. Il permet de vous toomap noms tooa service nom DNS et donc résoudre les adresses IP de point de terminaison. 

Comme indiqué dans hello diagramme suivant, hello service DNS, en cours d’exécution dans le cluster Service Fabric de hello, mappe les noms de tooservice de noms DNS qui sont alors résolus en adresses hello Naming Service tooreturn hello point de terminaison tooconnect à. nom DNS de Hello pour le service de hello est fournie au moment de la création de hello. 

![points de terminaison de service][9]

Pour plus d’informations sur comment toouse hello service DNS voir [service DNS dans Azure Service Fabric](service-fabric-dnsservice.md) l’article.

### <a name="reverse-proxy-service"></a>Service de proxy inverse
les adresses de proxy inverse de Hello services cluster hello qui expose les points de terminaison HTTP, y compris le protocole HTTPS. proxy inverse de Hello simplifie considérablement l’appeler d’autres services et leurs méthodes en ayant spécifique à un format d’URI et handles hello résoudre, se connecter, les étapes de nouvelles tentatives requises pour toocommunicate un service avec un autre à l’aide de hello transmet au service d’affectation de noms. En d’autres termes, elle masque hello Service d’affectation de noms vous lors de l’appel d’autres services en ce qui en fait aussi simple que l’appel d’une URL.

![points de terminaison de service][10]

Pour plus d’informations sur comment toouse hello inverser le service de proxy, consultez [proxy dans Azure Service Fabric inverse](service-fabric-reverseproxy.md) l’article.

## <a name="connections-from-external-clients"></a>Connexions des clients externes
Services connexion tooeach autres à l’intérieur d’un cluster généralement pouvez accéder directement aux points de terminaison hello d’autres services hello les nœuds dans un cluster étant sur hello même réseau local. Cependant, dans certains environnements, un cluster peut se trouver derrière un équilibrage de charge. Celui-ci achemine le trafic d’entrée externe à travers un ensemble limité de ports. Dans ces cas, les services peuvent toujours communiquer entre eux et résoudre les adresses à l’aide de hello d’affectation de noms de Service, mais des étapes supplémentaires doivent être prises tooallow les clients externes tooconnect tooservices.

## <a name="service-fabric-in-azure"></a>Service Fabric dans Azure
Un cluster Service Fabric dans Azure est placé derrière un équilibrage de charge Azure. Tous les clusters de toohello trafic externe doit traverser d’équilibrage de charge hello. Hello équilibrage de charge automatiquement transfère le trafic entrant sur un port donné de tooa aléatoire *nœud* qui a hello ouvrir le même port. Hello équilibrage de charge Azure ne reconnaît que les ports ouverts sur hello *nœuds*, il ne connaît pas ouvrir les ports par personne *services*.

![Topologie d’équilibrage de charge Azure et de Service Fabric][3]

Par exemple, dans l’ordre tooaccept externe du trafic sur le port **80**, hello suit les éléments doit être configuré :

1. Écrivez un service qui écoute sur le port 80. Configurer le port 80 dans ServiceManifest.xml du service hello et ouvrir un écouteur service hello, par exemple, un serveur web auto-hébergé.

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. Créer un Cluster Service Fabric dans Azure et spécifier le port **80** comme un port de point de terminaison personnalisé pour le type de nœud hello qui hébergera le service de hello. Si vous avez plusieurs types de nœud, vous pouvez configurer un *contrainte de placement* sur hello tooensure de service qu’il s’exécute uniquement sur le type de nœud hello qui a le port du point de terminaison personnalisé hello ouvert.

    ![Ouvrir un port sur un type de nœud][4]
3. Une fois que le cluster de hello a été créé, configurez hello équilibrage de charge Azure dans le trafic tooforward de groupe de ressources du cluster hello sur le port 80. Lorsque vous créez un cluster via hello portail Azure, il est configuré automatiquement pour chaque port de point de terminaison personnalisé qui a été configuré.

    ![Transférer le trafic Bonjour équilibrage de charge Azure][5]
4. Hello, utilisations d’équilibrage de charge Azure un toodetermine sonde si ou toosend pas le trafic de nœud particulier de tooa. Hello sonde vérifie périodiquement un point de terminaison sur chaque toodetermine nœud répondent ou non les nœud hello. En cas de sonde de hello tooreceive une réponse après un nombre de fois configuré, équilibrage de charge hello cesse d’envoyer de nœud toothat de trafic. Lorsque vous créez un cluster via hello portail Azure, une sonde est configurée automatiquement pour chaque port de point de terminaison personnalisé qui a été configuré.

    ![Transférer le trafic Bonjour équilibrage de charge Azure][8]

Il est important tooremember que hello équilibrage de charge Azure et sonde de hello seulement connaissent pas hello *nœuds*, pas hello *services* en cours d’exécution sur les nœuds hello. Hello équilibrage de charge Azure envoie toujours toonodes le trafic qui répondent toohello sonde, afin de veiller tooensure services sont disponibles sur les nœuds hello qui sont en mesure de toorespond toohello sonde.

## <a name="reliable-services-built-in-communication-api-options"></a>Reliable Services : options d’API de communication intégrées
infrastructure de Services fiables Hello est fourni avec plusieurs options de communication avant génération. décision Hello sur lequel un est la mieux vous dépend des choix hello Hello hello vos services sont écrites en langage de programmation, infrastructure de communication hello et modèle de programmation.

* **Aucun protocole spécifique :** si vous n’avez pas un choix particulier de l’infrastructure de communication, mais vous souhaitez tooget quelque chose haut et en cours d’exécution rapidement, option idéale de hello d’est [la communication à distance du service](service-fabric-reliable-services-communication-remoting.md), ce qui permet de fortement typée de procédure distante appelle pour des Services fiables et Reliable Actors. Il s’agit de hello plus simple et plus rapide tooget de façon démarré communication avec le service. Le service à distance gère la résolution des adresses de service ainsi que la connexion, les nouvelles tentatives et la gestion des erreurs. Il est disponible pour les applications C# et Java.
* **HTTP** : pour la communication sans langage spécifié, HTTP fournit un choix normalisé avec des outils et des serveurs HTTP disponibles dans plusieurs langues, le tout pris en charge par Service Fabric. Les services peuvent utiliser n’importe quelle pile HTTP, notamment l[’API web ASP.NET](service-fabric-reliable-services-communication-webapi.md) pour les applications C#. Les clients écrits en c# peuvent tirer parti de hello `ICommunicationClient` et `ServicePartitionClient` des classes, alors que pour Java, utilisez hello `CommunicationClient` et `FabricServicePartitionClient` classes, [de résolution de service, les connexions HTTP et les boucles de nouvelle tentative](service-fabric-reliable-services-communication.md).
* **WCF**: Si vous avez un code existant qui utilise WCF en tant que votre infrastructure de communication, vous pouvez ensuite utiliser hello `WcfCommunicationListener` pour SSI hello et `WcfCommunicationClient` et `ServicePartitionClient` des classes pour les clients hello. Cela n’est possible que pour les applications C# sur des clusters basés sur Windows. Pour plus d’informations, consultez cet article sur [basé sur WCF d’implémentation de pile de communication hello](service-fabric-reliable-services-communication-wcf.md).

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>Utilisation des protocoles personnalisés et d’autres infrastructures de communication
Les services peuvent utiliser un protocole ou une infrastructure quelconque pour la communication, qu’il s’agisse d’un protocole binaire personnalisé passant par des sockets TCP ou d’événements de diffusion passant par [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) ou [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/). Service Fabric fournit des API que vous pouvez connecter votre pile de communication, tandis que hello tous les toodiscover de travail et vous connecter de communication vous est abstrait. Consultez cet article sur hello [modèle de communication de Service fiable](service-fabric-reliable-services-communication.md) pour plus d’informations.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les concepts de hello et les API disponibles dans hello [modèle de communication des Services fiables](service-fabric-reliable-services-communication.md), puis commencer rapidement avec [la communication à distance du service](service-fabric-reliable-services-communication-remoting.md) ou accédez toolearn approfondie comment toowrite un écouteur de communication à l’aide [API Web avec OWIN auto-hébergement](service-fabric-reliable-services-communication-webapi.md).

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
