---
title: didacticiel de Service Bus Relay WCF aaaAzure | Documents Microsoft
description: "Créez une application cliente et un service Service Bus à l’aide de WCF Relay."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Didacticiel Azure WCF Relay

Ce didacticiel décrit comment toobuild relayer un service WCF simple application cliente et le service à l’aide de relais d’Azure. Pour obtenir un didacticiel similaire utilisant la [messagerie Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consultez [Bien démarrer avec les files d’attente Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

Ce didacticiel vous donne une présentation des étapes hello toocreate requis une application client et le service de relais de WCF. À l’instar de leurs homologues WCF d’origine, un service est une construction qui expose un ou plusieurs points de terminaison, chacun d’entre eux exposant une ou plusieurs opérations de service. point de terminaison Hello d’un service spécifie une adresse où le service de hello peut être trouvé, une liaison qui contient des informations de hello qu’un client doit communiquer avec le service hello et un contrat qui définit les fonctionnalités de hello fournies par les clients du service tooits hello. Hello principale différence entre WCF et WCF relais est que ce point de terminaison hello est exposé dans le cloud hello et non localement sur votre ordinateur.

Une fois que vous travaillez via la séquence hello de rubriques dans ce didacticiel, vous devez un service en cours d’exécution et un client qui peut appeler des opérations du service de hello hello. Hello première rubrique Comment tooset un compte. les étapes suivantes Hello décrivent comment toodefine un service qui utilise un contrat, comment tooimplement hello service, et comment tooconfigure hello service dans le code. Elles décrivent également comment toohost et exécuter le service hello. Hello service qui est créé est auto-hébergé et hello client et le service exécutent sur hello même ordinateur. Vous pouvez configurer le service de hello à l’aide de code ou un fichier de configuration.

trois étapes finales de Hello décrivent comment toocreate une application cliente, configurez l’application cliente de hello et créer et utiliser un client que vous pouvez accéder aux fonctionnalités hello d’hôte de hello.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, vous devez hello suivant :

* [Microsoft Visual Studio 2015 ou une version ultérieure](http://visualstudio.com). Ce didacticiel utilise Visual Studio 2017.
* Un compte Azure actif. Si vous n’en avez pas, vous pouvez créer un compte gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/free/).

## <a name="create-a-service-namespace"></a>Création d'un espace de noms de service

première étape de Hello est toocreate un espace de noms et tooobtain un [Signature d’accès partagé (SAS)](../service-bus-messaging/service-bus-sas.md) clé. Un espace de noms fournit une limite d’application pour chaque application exposée via le service de relais hello. Une clé SAS est générée automatiquement par le système de hello lors de la création d’un espace de noms de service. combinaison de Hello d’espace de noms de service et la clé SAP fournit des informations d’identification de hello pour l’application de tooan tooauthenticate Azure access. Suivez hello [ici les instructions](relay-create-namespace-portal.md) toocreate un espace de noms de relais.

## <a name="define-a-wcf-service-contract"></a>Définition d’un contrat de service WCF

contrat de service Hello spécifie quelles opérations (hello web service la terminologie des méthodes ou des fonctions) hello service prend en charge. Les contrats sont créés en définissant une interface C++, C# ou Visual Basic. Chaque méthode dans l’interface hello correspond l’opération de service spécifique tooa. Chaque interface doit avoir hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribut appliqué tooit, et chaque opération doit avoir hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit de l’attribut est appliqué. Si une méthode dans une interface qui possède hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribut n’a pas de hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) d’attribut, cette méthode n’est pas exposée. code Hello pour ces tâches est fourni dans l’exemple hello hello procédure. Pour obtenir une présentation plus large des contrats et des services, consultez [conception et implémentation de Services](https://msdn.microsoft.com/library/ms729746.aspx) Bonjour documentation WCF.

### <a name="create-a-relay-contract-with-an-interface"></a>Création d’un contrat de relais avec une interface

1. Ouvrez Visual Studio en tant qu’administrateur en cliquant sur le programme hello Bonjour **Démarrer** menu et en sélectionnant **exécuter en tant qu’administrateur**.
2. Créez un projet d’application de console. Cliquez sur hello **fichier** menu et sélectionnez **nouveau**, puis cliquez sur **projet**. Bonjour **nouveau projet** boîte de dialogue, cliquez sur **Visual C#** (si **Visual C#** n’apparaît pas, regardez sous **autres langages**). Cliquez sur hello **l’application Console (.NET Framework)** modèle et nommez-le **EchoService**. Cliquez sur **OK** projet hello de toocreate.

    ![][2]

3. Installez le package NuGet Service Bus de hello. Ce package ajoute automatiquement des références toohello Service Bus bibliothèques, ainsi que hello WCF **System.ServiceModel**. [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) est l’espace de noms hello qui vous permet de tooprogrammatically accès hello fonctionnalités de base de WCF. Service Bus utilise de nombreux hello objets et attributs WCF toodefine de contrats de service.

    Dans l’Explorateur de solutions, cliquez sur le projet de hello, puis cliquez sur **gérer les Packages NuGet...** . Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`. Vérifiez que nom du projet hello est sélectionné dans hello **versions** boîte. Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.

    ![][3]
4. Dans l’Explorateur de solutions, double-cliquez sur tooopen de fichier Program.cs hello il dans l’éditeur de hello, s’il n’est pas déjà ouvert.
5. Ajoutez hello qui suit à l’aide d’instructions haut hello du fichier de hello :

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. Nom d’espace de noms hello modification de son nom par défaut de **EchoService** trop**Microsoft.ServiceBus.Samples**.

   > [!IMPORTANT]
   > Ce didacticiel utilise l’espace de noms hello c# **Microsoft.ServiceBus.Samples**, qui est l’espace de noms hello Hello basé sur le contrat de type est utilisé dans le fichier de configuration hello Bonjour managé [configurer le client WCF hello](#configure-the-wcf-client) étape. Vous pouvez spécifier n’importe quel espace de noms lorsque vous générez cet exemple ; Toutefois, didacticiel de hello ne fonctionnera pas, sauf si vous modifiez hello des espaces de noms de contrat de hello et le service en conséquence, dans le fichier de configuration d’application hello. espace de noms Hello spécifié dans hello App.config fichier doit être même hello comme espace de noms hello spécifié dans vos fichiers c#.
   >
   >
7. Directement après hello `Microsoft.ServiceBus.Samples` déclaration d’espace de noms, mais dans l’espace de noms hello, définir une nouvelle interface nommée `IEchoContract` et appliquer hello `ServiceContractAttribute` interface de toohello d’attribut avec une valeur de l’espace de noms de `http://samples.microsoft.com/ServiceModel/Relay/`. valeur d’espace de noms Hello diffère de l’espace de noms hello que vous utilisez dans la portée de votre code hello. Au lieu de cela, la valeur d’espace de noms hello est utilisé comme identificateur unique pour ce contrat. Une spécification explicite de l’espace de noms hello empêche l’espace de noms par défaut hello Ajout toohello le nom de contrat. Collez hello après le code après la déclaration d’espace de noms hello :

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > En général, les noms de contrat de service hello contient un schéma d’affectation de noms qui inclut des informations de version. Y compris les informations de version dans les noms de contrat de service hello permet des principales modifications apportées aux services tooisolate en définissant un nouveau contrat de service avec un espace de noms et d’exposer sur un point de terminaison. De cette manière, les clients peuvent continuer toouse hello ancien contrat de service sans avoir toobe mis à jour. Les informations de version peuvent se composer d’une date ou un numéro de version. Pour plus d’informations, consultez la rubrique [Contrôle de version des services](http://go.microsoft.com/fwlink/?LinkID=180498). Pour des raisons de hello de ce didacticiel, hello jeu de noms de contrat de service hello d’affectation de noms ne contient pas d’informations de version.
   >
   >
8. Au sein de hello `IEchoContract` l’interface, déclarez une méthode pour hello d’opération unique hello `IEchoContract` expose contrat Bonjour interface et appliquez hello `OperationContractAttribute` attribut toohello méthode tooexpose dans le cadre de hello relais WCF public contrat, comme suit :

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. Directement après hello `IEchoContract` définition d’interface, déclarez un canal qui hérite à la fois `IEchoContract` et également toohello `IClientChannel` de l’interface, comme indiqué ici :

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    Un canal est l’objet WCF de hello via lequel clients et hôtes de hello transmettent informations tooeach autres. Une version ultérieure, vous écrirez du code par rapport aux informations de tooecho hello canal entre deux applications de hello.
10. À partir de hello **générer** menu, cliquez sur **générer la Solution** ou appuyez sur **Ctrl + Maj + B** précision de hello tooconfirm de votre travail jusqu'à présent.

### <a name="example"></a>Exemple

Hello suivant de code montre une interface de base qui définit un contrat WCF relais.

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Maintenant que hello interface est créée, vous pouvez implémenter l’interface de hello.

## <a name="implement-hello-wcf-contract"></a>Contrat de mettre en œuvre hello WCF

Création d’un relais Azure nécessite que vous créez tout d’abord le contrat hello, qui est défini à l’aide d’une interface. Pour plus d’informations sur la création d’interface de hello, reportez-vous à l’étape précédente de hello. étape suivante de Hello est interface de hello tooimplement. Cela implique la création d’une classe nommée `EchoService` qui implémente hello défini par l’utilisateur `IEchoContract` interface. Une fois que vous implémentez hello interface, vous configurez interface hello à l’aide d’un fichier de configuration App.config. fichier de configuration Hello contient les informations nécessaires pour l’application hello, telles que nom hello du service de hello, nom hello du contrat de hello et type hello du protocole est toocommunicate utilisé avec le service de relais hello. code de Hello utilisé pour ces tâches est fourni dans l’exemple hello hello procédure. Pour une description plus générale comment tooimplement un service de contrat, consultez [implémentation de contrats de Service](https://msdn.microsoft.com/library/ms733764.aspx) Bonjour documentation WCF.

1. Créer une nouvelle classe nommée `EchoService` directement après la définition de hello Hello `IEchoContract` interface. Hello `EchoService` classe implémente hello `IEchoContract` interface.

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    Implémentations d’interface tooother similaires, vous pouvez implémenter la définition de hello dans un autre fichier. Toutefois, pour ce didacticiel, hello se trouve dans le même fichier de définition d’interface hello et hello de hello `Main` (méthode).
2. Appliquer hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribut toohello `IEchoContract` interface. attribut de Hello Spécifie l’espace de noms et le nom du service hello. Après cela, hello `EchoService` classe se présente comme suit :

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. Hello d’implémenter `Echo` méthode définie dans hello `IEchoContract` interface Bonjour `EchoService` classe.

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. Cliquez sur **générer**, puis cliquez sur **générer la Solution** précision de hello tooconfirm de votre travail.

### <a name="define-hello-configuration-for-hello-service-host"></a>Définir la configuration de hello pour l’hôte de service hello

1. fichier de configuration Hello est un fichier de configuration WCF tooa très similaire. Il inclut le nom du service hello, point de terminaison (autrement dit, la location de hello qui expose des relais de Azure pour les clients et les hôtes toocommunicate entre eux) et hello liaison (type hello du protocole qui est utilisé toocommunicate). Hello principale différence est que ce point de terminaison de service configuré fait référence tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) liaison, ce qui ne fait pas partie de hello .NET Framework. [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) est une des liaisons de hello définies par le service de hello.
2. Dans **l’Explorateur de solutions**, double-cliquez sur tooopen de fichier App.config hello dans l’éditeur de Visual Studio hello.
3. Bonjour `<appSettings>` élément, remplacez les espaces réservés de hello par nom de hello de votre espace de noms de service et hello clé SAP que vous avez copié dans une étape antérieure.
4. Au sein de hello `<system.serviceModel>` balises, ajoutez un `<services>` élément. Vous pouvez définir plusieurs applications de relais dans un même fichier de configuration. Toutefois, ce didacticiel n’en définit qu’un seul.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. Au sein de hello `<services>` élément, ajouter un `<service>` nom_élément toodefine hello du service de hello.

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. Au sein de hello `<service>` élément, définir l’emplacement hello de contrat de point de terminaison hello et également hello type de liaison pour le point de terminaison hello.

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    point de terminaison Hello définit où les clients hello recherche hello hôte application. Plus tard, le didacticiel de hello utilise cette toocreate étape un URI qui expose entièrement hôte hello via Azure relais. liaison de Hello déclare que nous utilisons comme hello toocommunicate protocole avec le service de relais hello.
7. À partir de hello **générer** menu, cliquez sur **générer la Solution** précision de hello tooconfirm de votre travail.

### <a name="example"></a>Exemple

Hello de code suivant illustre implémentation hello hello du contrat de service.

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

Hello de code suivant montre hello de base format de fichier App.config hello avec hôte de service hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a>Héberger et exécuter un tooregister de service web de base avec le service de relais hello

Cette étape décrit comment toorun Azure relais service.

### <a name="create-hello-relay-credentials"></a>Créer des informations d’identification de relais hello

1. Dans `Main()`, créez deux variables dans l’espace de noms toostore hello et hello clé SAP qui sont lus à partir de la fenêtre de console hello.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    la clé SAS Hello sera utilisé tooaccess ultérieure de votre projet. espace de noms Hello est passé en tant que paramètre trop`CreateServiceUri` toocreate un URI de service.
2. À l’aide un [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) d’objet, déclarez que vous utiliserez une clé SAP en tant que type d’informations d’identification hello. Ajoutez hello après le code directement après le code hello ajoutée dans la dernière étape de hello.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a>Créer une adresse de base pour le service de hello

Après le code hello ajouté dans la dernière étape de hello, créer un `Uri` instance hello adresse de base du service de hello. Cet URI Spécifie le modèle de Service Bus hello, espace de noms hello et un chemin d’accès de hello d’interface de service hello.

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

« sb » est une abréviation pour le schéma de Service Bus hello et indique que nous utilisons TCP comme protocole de hello. Cela était aussi indiqué précédemment dans le fichier de configuration hello lorsque [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) a été spécifié en tant que liaison de hello.

Pour ce didacticiel, hello URI est `sb://putServiceNamespaceHere.windows.net/EchoService`.

### <a name="create-and-configure-hello-service-host"></a>Créer et configurer l’hôte de service hello

1. Définir le mode de connectivité hello trop`AutoDetect`.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    mode de connectivité Hello décrit hello protocole hello service utilise toocommunicate avec le service de relais hello ; HTTP ou TCP. À l’aide du paramètre par défaut de hello `AutoDetect`, service de hello tente tooconnect tooAzure relais via HTTP, TCP, si elle est disponible et si TCP n’est pas disponible. Notez que cela diffère de service du protocole de hello hello spécifie pour la communication client. Ce protocole est déterminé par la liaison hello utilisée. Par exemple, un service peut utiliser hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) liaison, ce qui indique que son point de terminaison communique avec les clients via HTTP. Que le même service pourrait spécifier **ConnectivityMode.AutoDetect** afin que le service de hello communique avec Azure relais sur TCP.
2. Créer un hôte de service hello, à l’aide de hello QU'URI créé précédemment dans cette section.

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    hôte de service Hello est un objet hello WCF qui instancie le service de hello. Ici, vous lui passez le type de hello du service, vous souhaitez toocreate (un `EchoService` type) et également les adresses toohello auquel vous souhaitez que le service de hello tooexpose.
3. Haut hello du fichier Program.cs de hello, ajoutez des références trop[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) et [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. Dans `Main()`, configurer le point de terminaison hello tooenable un accès public.

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    Cette étape informe service de relais hello que votre application peut être trouvée publiquement en examinant le flux ATOM de hello pour votre projet. Si vous définissez **DiscoveryType** trop**privé**, un client sera toujours les service de hello en mesure de tooaccess. Toutefois, les service hello apparaîtrait pas lorsqu’il recherche l’espace de noms de relais hello. Au lieu de cela, les clients hello aurait le chemin d’accès au point de terminaison tooknow hello au préalable.
5. Appliquer les service hello toohello points de terminaison de service définis dans le fichier App.config hello les informations d’identification :

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Comme indiqué dans l’étape précédente de hello, vous pouvez avoir déclaré plusieurs services et les points de terminaison dans le fichier de configuration hello. Si vous aviez, ce code traversent fichier de configuration hello et de recherche pour chaque point de terminaison toowhich, il doit s’appliquer à vos informations d’identification. Toutefois, pour ce didacticiel, fichier de configuration hello a uniquement un point de terminaison.

### <a name="open-hello-service-host"></a>Hôte de service hello ouvert

1. Ouvrez hello service.

    ```csharp
    host.Open();
    ```
2. Informer l’utilisateur hello hello service est en cours d’exécution et expliquez comment tooshut service de hello.

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Lorsque vous avez terminé, fermez l’hôte de service hello.

    ```csharp
    host.Close();
    ```
4. Appuyez sur **Ctrl + Maj + B** projet hello de toobuild.

### <a name="example"></a>Exemple

Une fois terminé, votre code de service doit se présenter ainsi. code de Hello inclut contrat de service hello et l’implémentation des étapes précédentes dans le didacticiel de hello et hôtes hello service dans une application console.

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a>Créer un client WCF hello contrat de service

étape suivante de Hello est toocreate une application cliente et définir le contrat de service hello vous allez implémenter dans les étapes ultérieures. Notez que plusieurs de ces étapes ressemblent aux étapes de hello utilisées toocreate un service : définition d’un contrat, la modification d’un fichier App.config de fichiers, à l’aide du service de relais tooconnect toohello informations d’identification et ainsi de suite. code de Hello utilisé pour ces tâches est fourni dans l’exemple hello hello procédure.

1. Créez un projet dans la solution Visual Studio actuelle de hello pour les clients hello de manière hello suivante :

   1. Dans l’Explorateur de solutions, dans hello même solution qui contient le service de hello, cliquez sur la solution actuelle de hello (pas le projet hello), puis cliquez sur **ajouter**. Puis cliquez sur **Nouveau projet**.
   2. Bonjour **ajouter un nouveau projet** boîte de dialogue, cliquez sur **Visual C#** (si **Visual C#** n’apparaît pas, regardez sous **autres langages**), sélectionnez hello **L’application console (.NET Framework)** modèle et nommez-le **EchoClient**.
   3. Cliquez sur **OK**.
      <br />
2. Dans l’Explorateur de solutions, double-cliquez sur le fichier Program.cs hello hello **EchoClient** tooopen dans l’éditeur hello, s’il n’est pas déjà ouvrir de projet.
3. Nom d’espace de noms hello modification de son nom par défaut de `EchoClient` trop`Microsoft.ServiceBus.Samples`.
4. Installer hello [package NuGet Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus): dans l’Explorateur de solutions, cliquez sur hello **EchoClient** de projet, puis cliquez sur **gérer les Packages NuGet**. Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`. Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.

    ![][3]
5. Ajouter un `using` instruction pour hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) espace de noms dans le fichier Program.cs de hello.

    ```csharp
    using System.ServiceModel;
    ```
6. Ajouter des noms de toohello de définition de contrat de service de hello, comme indiqué dans hello l’exemple suivant. Notez que cette définition est identique toohello utilisé Bonjour **Service** projet. Vous devez ajouter ce code en haut de hello Hello `Microsoft.ServiceBus.Samples` espace de noms.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. Appuyez sur **Ctrl + Maj + B** client de hello toobuild.

### <a name="example"></a>Exemple

Hello de code suivant affiche hello état actuel du fichier Program.cs de hello Bonjour **EchoClient** projet.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a>Configurer le client WCF de hello

Dans cette étape, vous créez un fichier App.config pour une application cliente de base qui accède au service hello créé précédemment dans ce didacticiel. Ce fichier App.config définit le nom du point de terminaison hello, liaison et contrat de hello. code de Hello utilisé pour ces tâches est fourni dans l’exemple hello hello procédure.

1. Dans l’Explorateur de solutions, Bonjour **EchoClient** de projet, double-cliquez sur **App.config** fichier hello de tooopen dans l’éditeur de Visual Studio hello.
2. Bonjour `<appSettings>` élément, remplacez les espaces réservés de hello par nom de hello de votre espace de noms de service et hello clé SAP que vous avez copié dans une étape antérieure.
3. Dans l’élément de system.serviceModel hello, ajoutez un `<client>` élément.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    Cette étape montre que vous définissez une application client de type WCF.
4. Au sein de hello `client` élément, définissez le nom de hello, contrat et type de liaison pour le point de terminaison hello.

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    Cette étape définit le nom de hello du point de terminaison hello, contrat hello défini dans le service de hello et faits hello que hello d’application cliente utilise TCP toocommunicate avec Azure relais. Hello nom de point de terminaison est utilisé dans hello étape suivante toolink cette configuration de point de terminaison avec l’URI du service hello.
5. Cliquez sur **Fichier**, puis sur **Tout enregistrer**.

## <a name="example"></a>Exemple

Hello de code suivant montre fichier App.config de hello pour le client de Echo hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a>Client de mettre en œuvre hello WCF
Dans cette étape, vous implémentez une application cliente de base qui accède au service hello que vous avez créé précédemment dans ce didacticiel. Service de toohello similaires, les clients hello effectue la plupart des hello même operations tooaccess Azure relais :

1. Définit le mode de connectivité hello.
2. Crée hello URI qui localise le service hôte de hello.
3. Définit les informations d’identification de sécurité hello.
4. Applique la connexion de toohello hello informations d’identification.
5. Établit une connexion hello.
6. Effectue des tâches spécifiques à l’application hello.
7. Ferme la connexion de hello.

Toutefois, une des principales différences de hello est que hello client application utilise un service de relais de canal tooconnect toohello, tandis que le service de hello utilise un appel trop**ServiceHost**. code de Hello utilisé pour ces tâches est fourni dans l’exemple hello hello procédure.

### <a name="implement-a-client-application"></a>Implémentation d’une application cliente
1. Définir le mode de connectivité hello trop**AutoDetect**. Ajouter hello suivant du code à l’intérieur de hello `Main()` méthode Hello **EchoClient** application.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. Définissez toohold hello les valeurs des variables pour l’espace de noms de service hello et la clé SAP qui sont lus à partir de la console de hello.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. Créer hello URI qui définit l’emplacement de hello d’hôte de hello dans votre projet de relais.

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. Créer un objet d’informations d’identification hello pour votre point de terminaison de service espace de noms.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. Créer la fabrication de canal hello qui charge la configuration hello décrite dans le fichier App.config hello.

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    Une fabrique de canaux est un objet WCF qui crée un canal via lequel communiquent hello service et les applications clientes.
6. Appliquer les informations d’identification hello.

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. Créez et ouvrez hello canal toohello service.

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. Écrire une interface utilisateur de base de hello et les fonctionnalités de l’écho de hello.

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    Notez que les code hello utilise instance hello d’objet de canal hello en tant que proxy pour le service de hello.
9. Fermer le canal de hello et fermer hello factory.

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>Exemple

Votre code terminé doit apparaître comme suit, montrant comment toocreate une application cliente, comment toocall hello les opérations du service de hello et comment tooclose hello client après l’opération de hello appellent est terminée.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a>Exécuter des applications de hello

1. Appuyez sur **Ctrl + Maj + B** solution de hello toobuild. Cela génère le projet de client hello et de projet de service hello que vous avez créé dans les étapes précédentes hello.
2. Avant l’application de client hello en cours d’exécution, il se peut que vous devez vous assurer que l’application de service hello s’exécute. Dans l’Explorateur de solutions dans Visual Studio, avec le bouton droit hello **EchoService** solution, puis cliquez sur **propriétés**.
3. Dans la boîte de dialogue de propriétés de solution de hello, cliquez sur **projet de démarrage**, puis cliquez sur hello **plusieurs projets de démarrage** bouton. Assurez-vous que **EchoService** apparaît en premier dans la liste de hello.
4. Ensemble hello **Action** zone pour les deux hello **EchoService** et **EchoClient** projets trop**Démarrer**.

    ![][5]
5. Cliquez sur **Dépendances du projet**. Bonjour **projets** boîte, sélectionnez **EchoClient**. Bonjour **dépend** zone, assurez-vous que **EchoService** est activée.

    ![][6]
6. Cliquez sur **OK** toodismiss hello **propriétés** boîte de dialogue.
7. Appuyez sur **F5** toorun les deux projets.
8. Les deux fenêtres de console ouvrant et vous demander de nom d’espace de noms hello. Hello service doit s’exécuter en premier lieu, dans hello **EchoService** fenêtre console, entrez l’espace de noms hello et appuyez sur **entrée**.
9. Ensuite, vous êtes invité à fournir votre clé SAS. Entrez la clé SAS hello et appuyez sur ENTRÉE.

    Voici un exemple de sortie à partir de la fenêtre de console hello. Notez que les valeurs de hello fournies ici sont par exemple uniquement.

    `Your Service Namespace: myNamespace``Your SAS Key: <SAS key value>`

    application de service Hello imprime toohello console fenêtre hello adresse sur lequel il est à l’écoute, comme dans hello l’exemple suivant.

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/``Press [Enter] tooexit`
10. Bonjour **EchoClient** fenêtre console, entrez hello les mêmes informations que vous avez entrées précédemment pour l’application de service hello. Suivez hello tooenter étapes précédentes de hello même espace de noms de service et les associations de sécurité des valeurs pour l’application cliente de hello de clé.
11. Après avoir entré ces valeurs, client de hello ouvre un canal toohello service et vous invite à entrer vous tooenter du texte comme indiqué dans hello exemple de sortie de console suivant.

    `Enter text tooecho (or [Enter] tooexit):`

    Entrez une application de service de texte toosend toohello et appuyez sur ENTRÉE. Ce texte est envoyé à service toohello via une opération de service Echo de hello et apparaît dans la fenêtre de console de service hello comme hello suivant l’exemple de sortie.

    `Echoing: My sample text`

    application cliente de Hello reçoit la valeur de retour de hello Hello `Echo` opération, qui est le texte d’origine hello et imprime tooits fenêtre de console. Hello Voici la sortie de la fenêtre de console cliente hello.

    `Server echoed: My sample text`
12. Vous pouvez continuer à envoyer des messages texte à partir du service de toohello hello client de cette manière. Lorsque vous avez terminé, appuyez sur entrée dans hello client et service console windows tooend les deux applications.

## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel a montré comment toobuild une application cliente de relais d’Azure et à l’aide du service hello fonctionnalités WCF relais du Bus de Service. Pour obtenir un didacticiel similaire utilisant la [messagerie Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consultez [Bien démarrer avec les files d’attente Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

toolearn en savoir plus sur Azure relais, consultez hello rubriques suivantes.

* [Présentation de l’architecture d’Azure Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Vue d’ensemble d’Azure Relay](relay-what-is-it.md)
* [Comment toouse hello WCF de relais service avec .NET](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
