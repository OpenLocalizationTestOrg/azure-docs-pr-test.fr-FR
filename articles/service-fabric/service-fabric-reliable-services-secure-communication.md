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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="bff4f-103">Sécurisation des communications pour les services dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bff4f-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bff4f-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="bff4f-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="bff4f-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="bff4f-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="bff4f-106">La sécurité est un des aspects les plus importants hello de communication.</span><span class="sxs-lookup"><span data-stu-id="bff4f-106">Security is one of hello most important aspects of communication.</span></span> <span data-ttu-id="bff4f-107">infrastructure d’application des Services fiables Hello fournit quelques piles de communication prégénérée et outils que vous pouvez utiliser la sécurité de tooimprove.</span><span class="sxs-lookup"><span data-stu-id="bff4f-107">hello Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use tooimprove security.</span></span> <span data-ttu-id="bff4f-108">Cet article traite de la tooimprove sécurité lorsque vous utilisez la communication à distance du service et hello pile de communication de Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="bff4f-108">This article talks about how tooimprove security when you're using service remoting and hello Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="bff4f-109">Sécurisation d’un service lors de l’utilisation de la communication à distance des services</span><span class="sxs-lookup"><span data-stu-id="bff4f-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="bff4f-110">Nous utilisons un existant [exemple](service-fabric-reliable-services-communication-remoting.md) qui explique comment tooset une communication à distance pour les services fiables.</span><span class="sxs-lookup"><span data-stu-id="bff4f-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="bff4f-111">toohelp sécuriser un service lorsque vous utilisez la communication à distance du service, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bff4f-111">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="bff4f-112">Créez une interface, `IHelloWorldStateful`, qui définit les méthodes hello qui seront disponibles pour un appel de procédure distante sur votre service.</span><span class="sxs-lookup"><span data-stu-id="bff4f-112">Create an interface, `IHelloWorldStateful`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="bff4f-113">Votre service utilisera `FabricTransportServiceRemotingListener`, qui est déclaré dans hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` espace de noms.</span><span class="sxs-lookup"><span data-stu-id="bff4f-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="bff4f-114">Il s'agit d'une implémentation `ICommunicationListener` qui fournit des fonctionnalités de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="bff4f-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="bff4f-115">Ajoutez des paramètres de l’écouteur et des informations d’identification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="bff4f-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="bff4f-116">Assurez-vous que le certificat que vous souhaitez toohelp toouse sécuriser que votre communication avec le service est installé sur tous les nœuds hello dans un cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="bff4f-116">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="bff4f-117">Vous pouvez fournir les paramètres de l’écouteur et les informations d’identification de sécurité de deux manières :</span><span class="sxs-lookup"><span data-stu-id="bff4f-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="bff4f-118">Les fournir directement dans le code de service hello :</span><span class="sxs-lookup"><span data-stu-id="bff4f-118">Provide them directly in hello service code:</span></span>

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
   2. <span data-ttu-id="bff4f-119">À l'aide d’un [package de configuration](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="bff4f-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="bff4f-120">Ajouter un `TransportSettings` section dans le fichier settings.xml de hello.</span><span class="sxs-lookup"><span data-stu-id="bff4f-120">Add a `TransportSettings` section in hello settings.xml file.</span></span>

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

       <span data-ttu-id="bff4f-121">Dans ce cas, hello `CreateServiceReplicaListeners` méthode doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="bff4f-121">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

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

        <span data-ttu-id="bff4f-122">Si vous ajoutez un `TransportSettings` section dans le fichier settings.xml hello `FabricTransportRemotingListenerSettings ` charge tous les paramètres de hello à partir de cette section par défaut.</span><span class="sxs-lookup"><span data-stu-id="bff4f-122">If you add a `TransportSettings` section in hello settings.xml file , `FabricTransportRemotingListenerSettings ` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="bff4f-123">Dans ce cas, hello `CreateServiceReplicaListeners` méthode doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="bff4f-123">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

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
3. <span data-ttu-id="bff4f-124">Lorsque vous appelez des méthodes sur un service sécurisé à l’aide de la pile de communication à distance hello, au lieu d’utiliser hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` classe toocreate un proxy de service, utilisez `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="bff4f-124">When you call methods on a secured service by using hello remoting stack, instead of using hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class toocreate a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="bff4f-125">Transmettez `FabricTransportRemotingSettings`, qui contient `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="bff4f-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

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

    <span data-ttu-id="bff4f-126">Si le code client hello est en cours d’exécution dans le cadre d’un service, vous pouvez charger `FabricTransportRemotingSettings` à partir du fichier settings.xml de hello.</span><span class="sxs-lookup"><span data-stu-id="bff4f-126">If hello client code is running as part of a service, you can load `FabricTransportRemotingSettings` from hello settings.xml file.</span></span> <span data-ttu-id="bff4f-127">Créer une section HelloWorldClientTransportSettings qui est le code de service toohello similaire, comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="bff4f-127">Create a HelloWorldClientTransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="bff4f-128">Rendre hello après les modifications de code de client toohello :</span><span class="sxs-lookup"><span data-stu-id="bff4f-128">Make hello following changes toohello client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="bff4f-129">Si le client de hello ne fonctionne pas dans le cadre d’un service, vous pouvez créer un fichier client_name.settings.xml Bonjour même emplacement où hello client_name.exe.</span><span class="sxs-lookup"><span data-stu-id="bff4f-129">If hello client is not running as part of a service, you can create a client_name.settings.xml file in hello same location where hello client_name.exe is.</span></span> <span data-ttu-id="bff4f-130">Créez ensuite une section TransportSettings dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="bff4f-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="bff4f-131">Service toohello similaire, si vous ajoutez un `TransportSettings` client settings.xml/client_name.settings.xml, section `FabricTransportRemotingSettings` charge tous les paramètres de hello à partir de cette section par défaut.</span><span class="sxs-lookup"><span data-stu-id="bff4f-131">Similar toohello service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all hello settings from this section by default.</span></span>

    <span data-ttu-id="bff4f-132">Dans ce cas, hello code précédent est encore simplifié :</span><span class="sxs-lookup"><span data-stu-id="bff4f-132">In that case, hello earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="bff4f-133">Sécuriser un service lorsque vous utilisez une pile de communication basée sur WCF</span><span class="sxs-lookup"><span data-stu-id="bff4f-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="bff4f-134">Nous utilisons un existant [exemple](service-fabric-reliable-services-communication-wcf.md) qui explique comment tooset une communication basé sur WCF de pile pour les services fiables.</span><span class="sxs-lookup"><span data-stu-id="bff4f-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how tooset up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="bff4f-135">toohelp sécuriser un service lorsque vous utilisez une pile de communication basée sur WCF, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bff4f-135">toohelp secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="bff4f-136">Pour le service de hello, vous avez besoin d’un écouteur de communication WCF toohelp hello sécurisé (`WcfCommunicationListener`) que vous créez.</span><span class="sxs-lookup"><span data-stu-id="bff4f-136">For hello service, you need toohelp secure hello WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="bff4f-137">toodo, modifier hello `CreateServiceReplicaListeners` (méthode).</span><span class="sxs-lookup"><span data-stu-id="bff4f-137">toodo this, modify hello `CreateServiceReplicaListeners` method.</span></span>

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
2. <span data-ttu-id="bff4f-138">Dans le client de hello, hello `WcfCommunicationClient` classe qui a été créé dans hello précédente [exemple](service-fabric-reliable-services-communication-wcf.md) demeure inchangée.</span><span class="sxs-lookup"><span data-stu-id="bff4f-138">In hello client, hello `WcfCommunicationClient` class that was created in hello previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="bff4f-139">Mais vous devez toooverride hello `CreateClientAsync` méthode `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="bff4f-139">But you need toooverride hello `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

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

    <span data-ttu-id="bff4f-140">Utilisez `SecureWcfCommunicationClientFactory` toocreate un client de communication WCF (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="bff4f-140">Use `SecureWcfCommunicationClientFactory` toocreate a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="bff4f-141">Utilisez les méthodes de service tooinvoke hello client.</span><span class="sxs-lookup"><span data-stu-id="bff4f-141">Use hello client tooinvoke service methods.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bff4f-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bff4f-142">Next steps</span></span>
* [<span data-ttu-id="bff4f-143">API Web avec OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bff4f-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
