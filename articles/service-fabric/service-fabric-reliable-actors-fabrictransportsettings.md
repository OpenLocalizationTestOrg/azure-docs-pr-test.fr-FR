---
title: "paramètres FabricTransport aaaChange microservices Azure | Documents Microsoft"
description: "Découvrez comment configurer les paramètres de communication d’un intervenant Azure Service Fabric."
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: e312b475407eb95a435b93d80c0f2e9618b9ea1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="1136e-103">Configuration des paramètres de FabricTransport pour Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="1136e-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="1136e-104">Voici les paramètres hello que vous pouvez configurer :</span><span class="sxs-lookup"><span data-stu-id="1136e-104">Here are hello settings that you can configure:</span></span>
- <span data-ttu-id="1136e-105">C# : [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="1136e-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="1136e-106">Java : [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="1136e-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="1136e-107">Vous pouvez modifier la configuration par défaut de hello de FabricTransport des manières suivantes.</span><span class="sxs-lookup"><span data-stu-id="1136e-107">You can modify hello default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="1136e-108">Attribut d’assembly</span><span class="sxs-lookup"><span data-stu-id="1136e-108">Assembly attribute</span></span>

<span data-ttu-id="1136e-109">Hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) toobe appliquée sur les assemblys de service des clients et l’acteur de hello acteur a besoin d’attribut.</span><span class="sxs-lookup"><span data-stu-id="1136e-109">hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs toobe applied on hello actor client and actor service assemblies.</span></span>

<span data-ttu-id="1136e-110">Hello, l’exemple suivant montre comment toochange hello FabricTransport OperationTimeout paramètres par défaut :</span><span class="sxs-lookup"><span data-stu-id="1136e-110">hello following example shows how toochange hello default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="1136e-111">Le deuxième exemple modifie les valeurs par défaut de FabricTransport MaxMessageSize et OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="1136e-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="1136e-112">Package de configuration</span><span class="sxs-lookup"><span data-stu-id="1136e-112">Config package</span></span>

<span data-ttu-id="1136e-113">Vous pouvez utiliser un [package de configuration](service-fabric-application-model.md) configuration par défaut de hello toomodify.</span><span class="sxs-lookup"><span data-stu-id="1136e-113">You can use a [config package](service-fabric-application-model.md) toomodify hello default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-hello-actor-service"></a><span data-ttu-id="1136e-114">Configurer les paramètres de FabricTransport pour le service d’acteur hello</span><span class="sxs-lookup"><span data-stu-id="1136e-114">Configure FabricTransport settings for hello actor service</span></span>

<span data-ttu-id="1136e-115">Ajoutez une section TransportSettings dans le fichier settings.xml de hello.</span><span class="sxs-lookup"><span data-stu-id="1136e-115">Add a TransportSettings section in hello settings.xml file.</span></span>

<span data-ttu-id="1136e-116">Par défaut, le code de l’intervenant cherche SectionName en tant que « &lt;ActorName&gt;TransportSettings ».</span><span class="sxs-lookup"><span data-stu-id="1136e-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="1136e-117">S’il est introuvable, il recherche SectionName en tant que « TransportSettings ».</span><span class="sxs-lookup"><span data-stu-id="1136e-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-hello-actor-client-assembly"></a><span data-ttu-id="1136e-118">Configurer les paramètres de FabricTransport pour l’assembly de client hello acteur</span><span class="sxs-lookup"><span data-stu-id="1136e-118">Configure FabricTransport settings for hello actor client assembly</span></span>

<span data-ttu-id="1136e-119">Si le client de hello ne fonctionne pas dans le cadre d’un service, vous pouvez créer un «&lt;nom de l’exécutable Client&gt;. settings.xml « fichier Bonjour même emplacement que le fichier .exe de client hello.</span><span class="sxs-lookup"><span data-stu-id="1136e-119">If hello client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in hello same location as hello client .exe file.</span></span> <span data-ttu-id="1136e-120">Ajoutez ensuite une section TransportSettings à ce fichier.</span><span class="sxs-lookup"><span data-stu-id="1136e-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="1136e-121">SectionName doit être « TransportSettings ».</span><span class="sxs-lookup"><span data-stu-id="1136e-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="1136e-122">Configurer les paramètres FabricTransport pour sécuriser le service d’acteur/client avec un certificat secondaire.</span><span class="sxs-lookup"><span data-stu-id="1136e-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="1136e-123">Les informations du certificat secondaire peuvent être ajoutées en ajoutant le paramètre CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="1136e-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="1136e-124">Voici un exemple hello pour hello TransportSettings d’écouteur.</span><span class="sxs-lookup"><span data-stu-id="1136e-124">Below is hello example for hello Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="1136e-125">Voici un exemple hello pour hello TransportSettings du Client.</span><span class="sxs-lookup"><span data-stu-id="1136e-125">Below is hello example for hello Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="1136e-126">Configurer les paramètres FabricTransport pour sécuriser le service d’acteur/client avec un nom de l’objet.</span><span class="sxs-lookup"><span data-stu-id="1136e-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="1136e-127">Utilisateur besoins tooprovide findType comme FindBySubjectName, ajouter des valeurs CertificateIssuerThumbprints et CertificateRemoteCommonNames.</span><span class="sxs-lookup"><span data-stu-id="1136e-127">User needs tooprovide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="1136e-128">Voici un exemple hello pour hello TransportSettings d’écouteur.</span><span class="sxs-lookup"><span data-stu-id="1136e-128">Below is hello example for hello Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="1136e-129">Voici un exemple hello pour hello TransportSettings du Client.</span><span class="sxs-lookup"><span data-stu-id="1136e-129">Below is hello example for hello Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
