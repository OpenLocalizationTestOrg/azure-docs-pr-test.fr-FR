---
title: aaaGet en main de relais WCF de relais Azure dans .NET | Documents Microsoft
description: "Découvrez comment toouse Azure relais WCF transmet tooconnect deux applications hébergées dans des emplacements différents."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a>Comment toouse Azure relais WCF des relais avec .NET
Cet article décrit comment toouse hello service de relais d’Azure. exemples de Hello sont écrites en c# et utilisent des API de Windows Communication Foundation (WCF) hello avec extensions contenues dans hello assembly Service Bus. Pour plus d’informations sur les relais Azure, consultez hello [vue d’ensemble de Azure relais](relay-what-is-it.md).

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a>Qu’est-ce que WCF Relay ?

Bonjour Azure [ *WCF relais* ](relay-what-is-it.md) service vous permet de toobuild d’applications hybrides qui s’exécutent dans un centre de données Azure et votre propre environnement d’entreprise local. Cela facilite le service de relais Hello en vous toosecurely exposer des services Windows Communication Foundation (WCF) qui résident dans un cloud entreprise réseau toohello public, sans avoir tooopen connexion via un pare-feu ou l’exigence infrastructure de réseau d’entreprise tooa modifications contraignant.

![Concepts du service WCF Relay](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

Relais Azure vous permet de toohost les services WCF au sein de votre environnement d’entreprise existante. Vous pouvez ensuite déléguer à l’écoute entrant sessions et demandes toothese services toohello service de relais WCF qui s’exécutent dans Azure. Ainsi, vous tooexpose ces code tooapplication des services en cours d’exécution dans Azure, ou toomobile traitements ou les environnements de partenaires de l’extranet. Relais vous permet de contrôler de toosecurely qui permettre accéder à ces services à un niveau de granularité fin. Il fournit une fonctionnalité puissante et sécurisée de l’application tooexpose et les données à partir de vos solutions d’entreprise existantes et de tirer parti de celui-ci à partir du cloud de hello.

Cet article explique comment toouse Azure relais toocreate un service web WCF, exposés à l’aide d’une liaison de canal TCP, qui implémente une conversation sécurisée entre deux parties.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a>Obtenir hello du package NuGet Service Bus
Hello [package NuGet Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) est hello de tooget de façon plus simple hello API Service Bus et tooconfigure votre application avec toutes les dépendances du Service Bus hello. package de NuGet tooinstall hello dans votre projet, procédez comme hello suivant :

1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Références**, puis cliquez sur **Gérer les packages NuGet**.
2. Recherche de « Service Bus » et sélectionnez hello **Microsoft Azure Service Bus** élément. Cliquez sur **installer** toocomplete hello installation, puis fermez hello suivant la boîte de dialogue :
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a>Exposer et consommer un service web SOAP avec TCP
tooexpose un service web de SOAP WCF existant pour la consommation externe, vous devez vous modifications toohello service liaisons et les adresses. Cette opération peut nécessiter le fichier de configuration de tooyour de modifications, ou elle peut nécessiter des modifications du code, selon la façon dont vous avez installé et configuré vos services WCF. Notez que WCF vous permet de toohave plusieurs points de terminaison de réseau sur hello même service, afin que vous puissiez conserver hello existante des points de terminaison internes lors de l’ajout de points de terminaison de relais externe d’accès à hello même temps.

Dans cette tâche, vous générez un service WCF simple et ajoutez un tooit d’écouteur de relais. Cet exercice une connaissance de Visual Studio et donc ne pas parcourt tous les détails de hello de création d’un projet. Au lieu de cela, il se concentre sur le code de hello.

Avant de commencer cette procédure, effectuez hello suivant tooset procédure de votre environnement :

1. Dans Visual Studio, créez une application console qui contient deux projets, « Client » et « Service », au sein de la solution de hello.
2. Ajouter les projets de tooboth de package NuGet Service Bus hello. Ce package ajoute tous les projets de tooyour références hello assembly nécessaires.

### <a name="how-toocreate-hello-service"></a>Comment toocreate hello service
Commencez par créer service hello proprement dit. Un service WCF se compose d'au moins trois parties distinctes :

* Définition d’un contrat qui décrit les messages sont échangés et les opérations toobe appelé.
* Implémentation de ce contrat.
* Hôte qui héberge le service WCF de hello et expose plusieurs points de terminaison.

les exemples de code Hello dans cette section adresse chacun de ces composants.

contrat de Hello définit une seule opération, `AddNumbers`, qui ajoute deux nombres et retourne le résultat de hello. Hello `IProblemSolverChannel` toomore de client hello interface permet de gérer facilement la durée de vie de proxy hello. Il est recommandé de créer une interface de ce type. Il s’agit d’une bonne idée tooput cette définition dans un fichier distinct du contrat de sorte que vous pouvez référencer ce fichier à partir de projets à la fois votre « Client » et « Service », mais vous pouvez également copier le code de hello dans les deux projets.

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

Avec le contrat hello en place, mise en œuvre hello est la suivante :

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a>Configurer un hôte de service par programme
Avec le contrat de hello et l’implémentation en place, vous pouvez maintenant héberger le service de hello. Hébergement se produit à l’intérieur d’un [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) de l’objet, qui prend en charge la gestion des instances du service de hello et hôtes hello des points de terminaison qui écoutent les messages. Hello de code suivant configure hello service avec un point de terminaison local régulière et un aspect de hello tooillustrate relais point de terminaison, côte à côte, des points de terminaison internes et externes. Remplacez la chaîne de hello *espace de noms* de votre espace de noms et *yourKey* avec la clé SAS hello obtenu à l’étape d’installation précédente de hello.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

Dans l’exemple de hello, vous créez deux points de terminaison qui se trouvent sur hello même implémentation de contrat. L’un est local et l’autre projeté via Azure Relay. Hello principales différences entre eux sont des liaisons de hello ; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) pour hello local et [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) pour le point de terminaison de relais hello et les adresses de hello. point de terminaison local Hello possède une adresse de réseau local avec un port distinct. point de terminaison de relais Hello possède une adresse de point de terminaison composée d’une chaîne de hello `sb`, votre nom d’espace de noms et le chemin d’accès de hello « solveur. » Cela entraîne hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifiant le point de terminaison de service hello comme un point de terminaison TCP de Service Bus (relais) avec un nom DNS externe qualifié complet. Si vous placez le code hello en remplaçant les espaces réservés de hello en hello `Main` fonction Hello **Service** application, vous aurez un service fonctionnel. Si vous souhaitez que votre toolisten service exclusivement sur les relais hello, supprimez la déclaration de point de terminaison local hello.

### <a name="configure-a-service-host-in-hello-appconfig-file"></a>Configurer un hôte de service dans le fichier App.config hello
Vous pouvez également configurer hôte hello à l’aide du fichier App.config de hello. service Hello dans ce cas le code d’hébergement s’affiche dans l’exemple suivant de hello.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

définitions de point de terminaison Hello déplacement dans le fichier App.config de hello. package NuGet de Hello a déjà ajouté une plage d’un fichier de définitions toohello App.config, qui sont des extensions de configuration hello requis pour le relais de Azure. Hello suivant l’exemple, qui est hello exacte équivalent du code précédent de hello, doit apparaître directement sous hello **system.serviceModel** élément. Cet exemple de code suppose que l’espace de noms C# de votre projet se nomme **Service**.
Remplacez les espaces réservés de hello avec votre nom d’espace de noms de relais et de la clé SAS.

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

Après avoir apporté ces modifications, les service hello démarre comme avant, mais avec deux points de terminaison dynamiques : un utilisateur local et un à l’écoute dans le cloud de hello.

### <a name="create-hello-client"></a>Créer hello client
#### <a name="configure-a-client-programmatically"></a>Configuration d’un client par programme
service de hello tooconsume, vous pouvez construire un client WCF à l’aide un [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) objet. Service Bus utilise un modèle de sécurité basée sur un jeton, implémenté à l'aide de SAS. Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) classe représente un fournisseur de jetons de sécurité avec les méthodes de fabrique intégrées qui retournent des fournisseurs de jeton bien connus. exemple Hello utilise hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) acquisition de hello toohandle méthode de jeton SAS approprié de hello. clé et le nom hello sont celles obtenues à partir du portail hello comme décrit dans la section précédente de hello.

First, de référence ou de copie hello `IProblemSolver` de contrat de code à partir du service de hello dans votre projet client.

Ensuite, remplacez le code hello Bonjour `Main` méthode hello du client de, à nouveau en remplaçant texte hello avec votre espace de noms de relais et de la clé SAS.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

Vous pouvez à présent générer client de hello et service hello, exécutez-les (exécution de service de hello tout d’abord), et les clients hello appelle hello service et imprime **9**. Vous pouvez exécuter hello client et le serveur sur des ordinateurs différents, même sur des réseaux, et les communications hello continueront de fonctionner. Hello client code peut également s’exécuter localement ou dans le cloud de hello.

#### <a name="configure-a-client-in-hello-appconfig-file"></a>Configuration d’un client dans le fichier App.config hello
Hello suivant de code montre comment le client de hello tooconfigure à l’aide de hello fichier App.config.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

définitions de point de terminaison Hello déplacement dans le fichier App.config de hello. exemple suivant, qui est hello même en tant que code hello répertoriée précédemment, Hello doit apparaître directement sous hello `<system.serviceModel>` élément. Ici, comme auparavant, vous devez remplacer des espaces réservés hello avec votre espace de noms de relais et de la clé SAS.

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de relais d’Azure, suivez ces liens de toolearn plus.

* [Qu’est-ce qu’Azure Relay ?](relay-what-is-it.md)
* [Azure Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* Télécharger les exemples de Service Bus à partir [exemples Azure] [ Azure samples] ou consultez hello [vue d’ensemble des exemples de Service Bus][overview of Service Bus samples].

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
