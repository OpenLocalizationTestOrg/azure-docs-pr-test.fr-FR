---
title: "Sécuriser des communications pour les services dans Azure Service Fabric | Microsoft Docs"
description: "Vue d’ensemble de la sécurisation des communications pour Reliable Services en cours d’exécution dans un cluster Azure Service Fabric."
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
ms.openlocfilehash: 53119244f8f09c0c6c43f43761af1cc074f8d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="7e241-103">Sécurisation des communications pour les services dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7e241-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7e241-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="7e241-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="7e241-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="7e241-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="7e241-106">La sécurité est un des aspects les plus importants de la communication.</span><span class="sxs-lookup"><span data-stu-id="7e241-106">Security is one of the most important aspects of communication.</span></span> <span data-ttu-id="7e241-107">L’infrastructure d’application Reliable Services fournit quelques piles et outils de communication prédéfinis afin d’améliorer la sécurité.</span><span class="sxs-lookup"><span data-stu-id="7e241-107">The Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use to improve security.</span></span> <span data-ttu-id="7e241-108">Cet article vous explique comment améliorer la sécurité quand vous utilisez la communication à distance des services et la pile de communication Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="7e241-108">This article talks about how to improve security when you're using service remoting and the Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="7e241-109">Sécurisation d’un service lors de l’utilisation de la communication à distance des services</span><span class="sxs-lookup"><span data-stu-id="7e241-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="7e241-110">Nous utilisons un [exemple](service-fabric-reliable-services-communication-remoting.md) existant qui explique comment configurer la communication à distance pour Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="7e241-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="7e241-111">Pour sécuriser un service lors de l’utilisation de la communication à distance des services, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7e241-111">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="7e241-112">Créez une interface, `IHelloWorldStateful`, qui définit les méthodes disponibles pour l'appel de procédure distante sur votre service.</span><span class="sxs-lookup"><span data-stu-id="7e241-112">Create an interface, `IHelloWorldStateful`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="7e241-113">Votre service utilisera `FabricTransportServiceRemotingListener`, qui est déclaré dans l’espace de noms `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime`.</span><span class="sxs-lookup"><span data-stu-id="7e241-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="7e241-114">Il s'agit d'une implémentation `ICommunicationListener` qui fournit des fonctionnalités de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="7e241-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="7e241-115">Ajoutez des paramètres de l’écouteur et des informations d’identification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="7e241-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="7e241-116">Assurez-vous le certificat que vous souhaitez utiliser pour sécuriser les communications de votre service est installé sur tous les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="7e241-116">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="7e241-117">Vous pouvez fournir les paramètres de l’écouteur et les informations d’identification de sécurité de deux manières :</span><span class="sxs-lookup"><span data-stu-id="7e241-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="7e241-118">Directement dans le code de service :</span><span class="sxs-lookup"><span data-stu-id="7e241-118">Provide them directly in the service code:</span></span>

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
   2. <span data-ttu-id="7e241-119">À l'aide d’un [package de configuration](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="7e241-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="7e241-120">Ajoutez une section `TransportSettings` dans le fichier settings.xml.</span><span class="sxs-lookup"><span data-stu-id="7e241-120">Add a `TransportSettings` section in the settings.xml file.</span></span>

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

       <span data-ttu-id="7e241-121">Dans ce cas, la méthode `CreateServiceReplicaListeners` se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="7e241-121">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

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

        <span data-ttu-id="7e241-122">Si vous ajoutez une section `TransportSettings` dans le fichier settings.xml, `FabricTransportRemotingListenerSettings ` charge par défaut tous les paramètres de cette section.</span><span class="sxs-lookup"><span data-stu-id="7e241-122">If you add a `TransportSettings` section in the settings.xml file , `FabricTransportRemotingListenerSettings ` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="7e241-123">Dans ce cas, la méthode `CreateServiceReplicaListeners` se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="7e241-123">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

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
3. <span data-ttu-id="7e241-124">Lorsque vous appelez des méthodes sur un service sécurisé à l’aide de la pile de communication à distance, au lieu d’utiliser la classe `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` pour créer un proxy de service, utilisez `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="7e241-124">When you call methods on a secured service by using the remoting stack, instead of using the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class to create a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="7e241-125">Transmettez `FabricTransportRemotingSettings`, qui contient `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="7e241-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

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

    <span data-ttu-id="7e241-126">Si le code client s’exécute dans le cadre d’un service, vous pouvez charger `FabricTransportRemotingSettings` à partir du fichier settings.xml.</span><span class="sxs-lookup"><span data-stu-id="7e241-126">If the client code is running as part of a service, you can load `FabricTransportRemotingSettings` from the settings.xml file.</span></span> <span data-ttu-id="7e241-127">Créez une section HelloWorldClientTransportSettings similaire au code de service, comme illustré précédemment.</span><span class="sxs-lookup"><span data-stu-id="7e241-127">Create a HelloWorldClientTransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="7e241-128">Apportez les modifications suivantes au code du client :</span><span class="sxs-lookup"><span data-stu-id="7e241-128">Make the following changes to the client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="7e241-129">Si le client n’est pas exécuté dans le cadre d’un service, vous pouvez créer un fichier client_name.settings.xml dans le même emplacement que le fichier client_name.exe.</span><span class="sxs-lookup"><span data-stu-id="7e241-129">If the client is not running as part of a service, you can create a client_name.settings.xml file in the same location where the client_name.exe is.</span></span> <span data-ttu-id="7e241-130">Créez ensuite une section TransportSettings dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="7e241-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="7e241-131">Comme pour le service, si vous ajoutez une section `TransportSettings` dans le fichier client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` charge par défaut tous les paramètres de cette section.</span><span class="sxs-lookup"><span data-stu-id="7e241-131">Similar to the service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all the settings from this section by default.</span></span>

    <span data-ttu-id="7e241-132">Dans ce cas, le code précédent est encore davantage simplifié :</span><span class="sxs-lookup"><span data-stu-id="7e241-132">In that case, the earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="7e241-133">Sécuriser un service lorsque vous utilisez une pile de communication basée sur WCF</span><span class="sxs-lookup"><span data-stu-id="7e241-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="7e241-134">Nous utilisons un [exemple](service-fabric-reliable-services-communication-wcf.md) existant qui explique comment configurer une pile de communication basée sur WCF pour Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="7e241-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how to set up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="7e241-135">Pour sécuriser un service lorsque vous utilisez une pile de communication basée sur WCF, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7e241-135">To help secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="7e241-136">Pour le service, vous devez sécuriser l'écouteur de communication WCF (`WcfCommunicationListener`) que vous créez.</span><span class="sxs-lookup"><span data-stu-id="7e241-136">For the service, you need to help secure the WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="7e241-137">Pour cela, modifiez la méthode `CreateServiceReplicaListeners` .</span><span class="sxs-lookup"><span data-stu-id="7e241-137">To do this, modify the `CreateServiceReplicaListeners` method.</span></span>

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

        // Add certificate details in the ServiceHost credentials.
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
2. <span data-ttu-id="7e241-138">Dans le client, la classe `WcfCommunicationClient` que nous avons créée dans l’ [exemple](service-fabric-reliable-services-communication-wcf.md) précédent reste inchangée.</span><span class="sxs-lookup"><span data-stu-id="7e241-138">In the client, the `WcfCommunicationClient` class that was created in the previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="7e241-139">Cependant, vous devez remplacer la méthode `CreateClientAsync` de `WcfCommunicationClientFactory` :</span><span class="sxs-lookup"><span data-stu-id="7e241-139">But you need to override the `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

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
            // Add certificate details to the ChannelFactory credentials.
            // These credentials will be used by the clients created by
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

    <span data-ttu-id="7e241-140">Utilisez `SecureWcfCommunicationClientFactory` pour créer un client de communication WCF (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="7e241-140">Use `SecureWcfCommunicationClientFactory` to create a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="7e241-141">Utilisez le client pour appeler les méthodes de service.</span><span class="sxs-lookup"><span data-stu-id="7e241-141">Use the client to invoke service methods.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7e241-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e241-142">Next steps</span></span>
* [<span data-ttu-id="7e241-143">API Web avec OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7e241-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
