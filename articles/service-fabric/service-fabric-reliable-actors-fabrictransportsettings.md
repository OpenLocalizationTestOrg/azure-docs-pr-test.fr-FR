---
title: "Modifier les paramètres de Fabric Transport dans les microservices Azure | Microsoft Docs"
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
ms.openlocfilehash: 75bdd4644f4ccc583271b9169c50a375e2cd6629
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="eede5-103">Configuration des paramètres de FabricTransport pour Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="eede5-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="eede5-104">Voici les paramètres que vous pouvez configurer :</span><span class="sxs-lookup"><span data-stu-id="eede5-104">Here are the settings that you can configure:</span></span>
- <span data-ttu-id="eede5-105">C# : [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="eede5-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="eede5-106">Java : [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="eede5-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="eede5-107">Vous pouvez modifier la configuration par défaut de FabricTransport des manières suivantes.</span><span class="sxs-lookup"><span data-stu-id="eede5-107">You can modify the default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="eede5-108">Attribut d’assembly</span><span class="sxs-lookup"><span data-stu-id="eede5-108">Assembly attribute</span></span>

<span data-ttu-id="eede5-109">L’attribut [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) doit être appliqué au niveau des assemblys du client et du service de l’intervenant.</span><span class="sxs-lookup"><span data-stu-id="eede5-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span></span>

<span data-ttu-id="eede5-110">L’exemple suivant montre comment modifier la valeur par défaut des paramètres de FabricTransport OperationTimeout :</span><span class="sxs-lookup"><span data-stu-id="eede5-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="eede5-111">Le deuxième exemple modifie les valeurs par défaut de FabricTransport MaxMessageSize et OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="eede5-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="eede5-112">Package de configuration</span><span class="sxs-lookup"><span data-stu-id="eede5-112">Config package</span></span>

<span data-ttu-id="eede5-113">Vous pouvez utiliser un [package de configuration](service-fabric-application-model.md) pour modifier la configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="eede5-113">You can use a [config package](service-fabric-application-model.md) to modify the default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-the-actor-service"></a><span data-ttu-id="eede5-114">Configurer les paramètres de FabricTransport pour le service de l’intervenant</span><span class="sxs-lookup"><span data-stu-id="eede5-114">Configure FabricTransport settings for the actor service</span></span>

<span data-ttu-id="eede5-115">Ajoutez une section TransportSettings dans le fichier settings.xml.</span><span class="sxs-lookup"><span data-stu-id="eede5-115">Add a TransportSettings section in the settings.xml file.</span></span>

<span data-ttu-id="eede5-116">Par défaut, le code de l’intervenant cherche SectionName en tant que « &lt;ActorName&gt;TransportSettings ».</span><span class="sxs-lookup"><span data-stu-id="eede5-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="eede5-117">S’il est introuvable, il recherche SectionName en tant que « TransportSettings ».</span><span class="sxs-lookup"><span data-stu-id="eede5-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

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

### <a name="configure-fabrictransport-settings-for-the-actor-client-assembly"></a><span data-ttu-id="eede5-118">Configurer les paramètres de FabricTransport pour l’assembly du client de l’intervenant</span><span class="sxs-lookup"><span data-stu-id="eede5-118">Configure FabricTransport settings for the actor client assembly</span></span>

<span data-ttu-id="eede5-119">Si le client n’est pas exécuté dans le cadre d’un service, vous pouvez créer un fichier « &lt;Nom de l’exe du client&gt;.settings.xml » au même endroit que le fichier .exe du client.</span><span class="sxs-lookup"><span data-stu-id="eede5-119">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span></span> <span data-ttu-id="eede5-120">Ajoutez ensuite une section TransportSettings à ce fichier.</span><span class="sxs-lookup"><span data-stu-id="eede5-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="eede5-121">SectionName doit être « TransportSettings ».</span><span class="sxs-lookup"><span data-stu-id="eede5-121">SectionName should be "TransportSettings".</span></span>

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

  * <span data-ttu-id="eede5-122">Configurer les paramètres FabricTransport pour sécuriser le service d’acteur/client avec un certificat secondaire.</span><span class="sxs-lookup"><span data-stu-id="eede5-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="eede5-123">Les informations du certificat secondaire peuvent être ajoutées en ajoutant le paramètre CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="eede5-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="eede5-124">Voici l’exemple pour l’écouteur TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="eede5-124">Below is the example for the Listener TransportSettings.</span></span>

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
     <span data-ttu-id="eede5-125">Voici l’exemple pour le client TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="eede5-125">Below is the example for the Client TransportSettings.</span></span>

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
    * <span data-ttu-id="eede5-126">Configurer les paramètres FabricTransport pour sécuriser le service d’acteur/client avec un nom de l’objet.</span><span class="sxs-lookup"><span data-stu-id="eede5-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="eede5-127">Vous devez définir findType sur FindBySubjectName, ajouter les valeurs CertificateIssuerThumbprints et CertificateRemoteCommonNames.</span><span class="sxs-lookup"><span data-stu-id="eede5-127">User needs to provide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="eede5-128">Voici l’exemple pour l’écouteur TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="eede5-128">Below is the example for the Listener TransportSettings.</span></span>

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
  <span data-ttu-id="eede5-129">Voici l’exemple pour le client TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="eede5-129">Below is the example for the Client TransportSettings.</span></span>

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
