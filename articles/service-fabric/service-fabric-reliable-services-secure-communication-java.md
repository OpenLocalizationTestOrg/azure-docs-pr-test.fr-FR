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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Sécurisation des communications pour les services dans Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# sur Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java sur Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Sécurisation d’un service lors de l’utilisation de la communication à distance des services
Nous utiliserons existant [exemple](service-fabric-reliable-services-communication-remoting-java.md) qui explique comment tooset une communication à distance pour les services fiables. toohelp sécuriser un service lorsque vous utilisez la communication à distance du service, procédez comme suit :

1. Créez une interface, `HelloWorldStateless`, qui définit les méthodes hello qui seront disponibles pour un appel de procédure distante sur votre service. Votre service utilisera `FabricTransportServiceRemotingListener`, qui est déclaré dans hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package. Il s'agit d'une implémentation `CommunicationListener` qui fournit des fonctionnalités de communication à distance.

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
2. Ajoutez des paramètres de l’écouteur et des informations d’identification de sécurité.

    Assurez-vous que le certificat que vous souhaitez toohelp toouse sécuriser que votre communication avec le service est installé sur tous les nœuds hello dans un cluster de hello hello. Vous pouvez fournir les paramètres de l’écouteur et les informations d’identification de sécurité de deux manières :

   1. À l'aide d’un [package de configuration](service-fabric-application-model.md):

       Ajouter un `TransportSettings` section dans le fichier settings.xml de hello.

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

       Dans ce cas, hello `createServiceInstanceListeners` méthode doit ressembler à ceci :

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        Si vous ajoutez un `TransportSettings` section dans le fichier settings.xml de hello sans préfixe, `FabricTransportListenerSettings` charge tous les paramètres de hello à partir de cette section par défaut.

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        Dans ce cas, hello `CreateServiceInstanceListeners` méthode doit ressembler à ceci :

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. Lorsque vous appelez des méthodes sur un service sécurisé à l’aide de la pile de communication à distance hello, au lieu d’utiliser hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` classe toocreate un proxy de service, utilisez `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.

    Si le code client hello est en cours d’exécution dans le cadre d’un service, vous pouvez charger `FabricTransportSettings` à partir du fichier settings.xml de hello. Créer une section TransportSettings qui est le code de service toohello similaire, comme indiqué précédemment. Rendre hello après les modifications de code de client toohello :

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
