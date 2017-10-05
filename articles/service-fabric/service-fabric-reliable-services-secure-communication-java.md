---
title: "Sécuriser des communications pour les services dans Azure Service Fabric | Microsoft Docs"
description: "Vue d’ensemble de la sécurisation des communications pour Reliable Services en cours d’exécution dans un cluster Azure Service Fabric."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: c4634e3d8efb1745fffcfe3e647e43d867038716
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="7fc18-103">Sécurisation des communications pour les services dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7fc18-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7fc18-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="7fc18-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="7fc18-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="7fc18-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="7fc18-106">Sécurisation d’un service lors de l’utilisation de la communication à distance des services</span><span class="sxs-lookup"><span data-stu-id="7fc18-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="7fc18-107">Nous allons utiliser un [exemple](service-fabric-reliable-services-communication-remoting-java.md) existant qui explique comment configurer la communication à distance pour Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="7fc18-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="7fc18-108">Pour sécuriser un service lors de l’utilisation de la communication à distance des services, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7fc18-108">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="7fc18-109">Créez une interface, `HelloWorldStateless`, qui définit les méthodes disponibles pour l'appel de procédure distante sur votre service.</span><span class="sxs-lookup"><span data-stu-id="7fc18-109">Create an interface, `HelloWorldStateless`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="7fc18-110">Votre service utilisera `FabricTransportServiceRemotingListener`, qui est déclaré dans le package `microsoft.serviceFabric.services.remoting.fabricTransport.runtime`.</span><span class="sxs-lookup"><span data-stu-id="7fc18-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="7fc18-111">Il s'agit d'une implémentation `CommunicationListener` qui fournit des fonctionnalités de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="7fc18-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="7fc18-112">Ajoutez des paramètres de l’écouteur et des informations d’identification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="7fc18-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="7fc18-113">Assurez-vous le certificat que vous souhaitez utiliser pour sécuriser les communications de votre service est installé sur tous les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="7fc18-113">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="7fc18-114">Vous pouvez fournir les paramètres de l’écouteur et les informations d’identification de sécurité de deux manières :</span><span class="sxs-lookup"><span data-stu-id="7fc18-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="7fc18-115">À l'aide d’un [package de configuration](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="7fc18-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="7fc18-116">Ajoutez une section `TransportSettings` dans le fichier settings.xml.</span><span class="sxs-lookup"><span data-stu-id="7fc18-116">Add a `TransportSettings` section in the settings.xml file.</span></span>

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       <span data-ttu-id="7fc18-117">Dans ce cas, la méthode `createServiceInstanceListeners` se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="7fc18-117">In this case, the `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="7fc18-118">Si vous ajoutez une section `TransportSettings` dans le fichier settings.xml sans aucun préfixe, `FabricTransportListenerSettings` charge par défaut tous les paramètres de cette section.</span><span class="sxs-lookup"><span data-stu-id="7fc18-118">If you add a `TransportSettings` section in the settings.xml file without any prefix, `FabricTransportListenerSettings` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="7fc18-119">Dans ce cas, la méthode `CreateServiceInstanceListeners` se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="7fc18-119">In this case, the `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="7fc18-120">Lorsque vous appelez des méthodes sur un service sécurisé à l’aide de la pile de communication à distance, au lieu d’utiliser la classe `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` pour créer un proxy de service, utilisez `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="7fc18-120">When you call methods on a secured service by using the remoting stack, instead of using the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class to create a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="7fc18-121">Si le code client s’exécute dans le cadre d’un service, vous pouvez charger `FabricTransportSettings` à partir du fichier settings.xml.</span><span class="sxs-lookup"><span data-stu-id="7fc18-121">If the client code is running as part of a service, you can load `FabricTransportSettings` from the settings.xml file.</span></span> <span data-ttu-id="7fc18-122">Créez une section TransportSettings similaire au code de service, comme illustré précédemment.</span><span class="sxs-lookup"><span data-stu-id="7fc18-122">Create a TransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="7fc18-123">Apportez les modifications suivantes au code du client :</span><span class="sxs-lookup"><span data-stu-id="7fc18-123">Make the following changes to the client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
