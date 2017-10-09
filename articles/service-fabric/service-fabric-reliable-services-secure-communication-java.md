---
title: "une communication sécurisée pour les services dans Azure Service Fabric aaaHelp | Documents Microsoft"
description: "Vue d’ensemble de la façon dont toohelp sécuriser les communications pour les services fiables qui s’exécutent dans un cluster Azure Service Fabric."
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
ms.openlocfilehash: 14db54d50c35478c1f2c156de0dba36f1427c8cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="999c2-103">Sécurisation des communications pour les services dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="999c2-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="999c2-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="999c2-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="999c2-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="999c2-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="999c2-106">Sécurisation d’un service lors de l’utilisation de la communication à distance des services</span><span class="sxs-lookup"><span data-stu-id="999c2-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="999c2-107">Nous utiliserons existant [exemple](service-fabric-reliable-services-communication-remoting-java.md) qui explique comment tooset une communication à distance pour les services fiables.</span><span class="sxs-lookup"><span data-stu-id="999c2-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="999c2-108">toohelp sécuriser un service lorsque vous utilisez la communication à distance du service, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="999c2-108">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="999c2-109">Créez une interface, `HelloWorldStateless`, qui définit les méthodes hello qui seront disponibles pour un appel de procédure distante sur votre service.</span><span class="sxs-lookup"><span data-stu-id="999c2-109">Create an interface, `HelloWorldStateless`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="999c2-110">Votre service utilisera `FabricTransportServiceRemotingListener`, qui est déclaré dans hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span><span class="sxs-lookup"><span data-stu-id="999c2-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="999c2-111">Il s'agit d'une implémentation `CommunicationListener` qui fournit des fonctionnalités de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="999c2-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="999c2-112">Ajoutez des paramètres de l’écouteur et des informations d’identification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="999c2-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="999c2-113">Assurez-vous que le certificat que vous souhaitez toohelp toouse sécuriser que votre communication avec le service est installé sur tous les nœuds hello dans un cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="999c2-113">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="999c2-114">Vous pouvez fournir les paramètres de l’écouteur et les informations d’identification de sécurité de deux manières :</span><span class="sxs-lookup"><span data-stu-id="999c2-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="999c2-115">À l'aide d’un [package de configuration](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="999c2-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="999c2-116">Ajouter un `TransportSettings` section dans le fichier settings.xml de hello.</span><span class="sxs-lookup"><span data-stu-id="999c2-116">Add a `TransportSettings` section in hello settings.xml file.</span></span>

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

       <span data-ttu-id="999c2-117">Dans ce cas, hello `createServiceInstanceListeners` méthode doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="999c2-117">In this case, hello `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="999c2-118">Si vous ajoutez un `TransportSettings` section dans le fichier settings.xml de hello sans préfixe, `FabricTransportListenerSettings` charge tous les paramètres de hello à partir de cette section par défaut.</span><span class="sxs-lookup"><span data-stu-id="999c2-118">If you add a `TransportSettings` section in hello settings.xml file without any prefix, `FabricTransportListenerSettings` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="999c2-119">Dans ce cas, hello `CreateServiceInstanceListeners` méthode doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="999c2-119">In this case, hello `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="999c2-120">Lorsque vous appelez des méthodes sur un service sécurisé à l’aide de la pile de communication à distance hello, au lieu d’utiliser hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` classe toocreate un proxy de service, utilisez `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="999c2-120">When you call methods on a secured service by using hello remoting stack, instead of using hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class toocreate a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="999c2-121">Si le code client hello est en cours d’exécution dans le cadre d’un service, vous pouvez charger `FabricTransportSettings` à partir du fichier settings.xml de hello.</span><span class="sxs-lookup"><span data-stu-id="999c2-121">If hello client code is running as part of a service, you can load `FabricTransportSettings` from hello settings.xml file.</span></span> <span data-ttu-id="999c2-122">Créer une section TransportSettings qui est le code de service toohello similaire, comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="999c2-122">Create a TransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="999c2-123">Rendre hello après les modifications de code de client toohello :</span><span class="sxs-lookup"><span data-stu-id="999c2-123">Make hello following changes toohello client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
