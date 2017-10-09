---
title: "une communication sécurisée pour les services dans Azure Service Fabric aaaHelp | Documents Microsoft"
description: "Vue d’ensemble de la façon dont toohelp sécuriser les communications pour les services fiables qui s’exécutent dans un cluster Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Sécurisation des communications pour les services dans Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# sur Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java sur Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

La sécurité est un des aspects les plus importants hello de communication. infrastructure d’application des Services fiables Hello fournit quelques piles de communication prégénérée et outils que vous pouvez utiliser la sécurité de tooimprove. Cet article traite de la tooimprove sécurité lorsque vous utilisez la communication à distance du service et hello pile de communication de Windows Communication Foundation (WCF).

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Sécurisation d’un service lors de l’utilisation de la communication à distance des services
Nous utilisons un existant [exemple](service-fabric-reliable-services-communication-remoting.md) qui explique comment tooset une communication à distance pour les services fiables. toohelp sécuriser un service lorsque vous utilisez la communication à distance du service, procédez comme suit :

1. Créez une interface, `IHelloWorldStateful`, qui définit les méthodes hello qui seront disponibles pour un appel de procédure distante sur votre service. Votre service utilisera `FabricTransportServiceRemotingListener`, qui est déclaré dans hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` espace de noms. Il s'agit d'une implémentation `ICommunicationListener` qui fournit des fonctionnalités de communication à distance.

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. Ajoutez des paramètres de l’écouteur et des informations d’identification de sécurité.

    Assurez-vous que le certificat que vous souhaitez toohelp toouse sécuriser que votre communication avec le service est installé sur tous les nœuds hello dans un cluster de hello hello. Vous pouvez fournir les paramètres de l’écouteur et les informations d’identification de sécurité de deux manières :

   1. Les fournir directement dans le code de service hello :

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. À l'aide d’un [package de configuration](service-fabric-application-model.md):

       Ajouter un `TransportSettings` section dans le fichier settings.xml de hello.

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       Dans ce cas, hello `CreateServiceReplicaListeners` méthode doit ressembler à ceci :

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        Si vous ajoutez un `TransportSettings` section dans le fichier settings.xml hello `FabricTransportRemotingListenerSettings ` charge tous les paramètres de hello à partir de cette section par défaut.

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        Dans ce cas, hello `CreateServiceReplicaListeners` méthode doit ressembler à ceci :

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. Lorsque vous appelez des méthodes sur un service sécurisé à l’aide de la pile de communication à distance hello, au lieu d’utiliser hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` classe toocreate un proxy de service, utilisez `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`. Transmettez `FabricTransportRemotingSettings`, qui contient `SecurityCredentials`.

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Si le code client hello est en cours d’exécution dans le cadre d’un service, vous pouvez charger `FabricTransportRemotingSettings` à partir du fichier settings.xml de hello. Créer une section HelloWorldClientTransportSettings qui est le code de service toohello similaire, comme indiqué précédemment. Rendre hello après les modifications de code de client toohello :

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Si le client de hello ne fonctionne pas dans le cadre d’un service, vous pouvez créer un fichier client_name.settings.xml Bonjour même emplacement où hello client_name.exe. Créez ensuite une section TransportSettings dans ce fichier.

    Service toohello similaire, si vous ajoutez un `TransportSettings` client settings.xml/client_name.settings.xml, section `FabricTransportRemotingSettings` charge tous les paramètres de hello à partir de cette section par défaut.

    Dans ce cas, hello code précédent est encore simplifié :  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a>Sécuriser un service lorsque vous utilisez une pile de communication basée sur WCF
Nous utilisons un existant [exemple](service-fabric-reliable-services-communication-wcf.md) qui explique comment tooset une communication basé sur WCF de pile pour les services fiables. toohelp sécuriser un service lorsque vous utilisez une pile de communication basée sur WCF, procédez comme suit :

1. Pour le service de hello, vous avez besoin d’un écouteur de communication WCF toohelp hello sécurisé (`WcfCommunicationListener`) que vous créez. toodo, modifier hello `CreateServiceReplicaListeners` (méthode).

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in hello ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. Dans le client de hello, hello `WcfCommunicationClient` classe qui a été créé dans hello précédente [exemple](service-fabric-reliable-services-communication-wcf.md) demeure inchangée. Mais vous devez toooverride hello `CreateClientAsync` méthode `WcfCommunicationClientFactory`:

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    Utilisez `SecureWcfCommunicationClientFactory` toocreate un client de communication WCF (`WcfCommunicationClient`). Utilisez les méthodes de service tooinvoke hello client.

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a>Étapes suivantes
* [API Web avec OWIN dans Reliable Services](service-fabric-reliable-services-communication-webapi.md)
