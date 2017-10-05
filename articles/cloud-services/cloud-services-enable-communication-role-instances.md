---
title: "Communication pour les rôles dans les services cloud | Microsoft Docs"
description: "Dans Cloud Services, des points de terminaison (http, https, tcp, udp) peuvent être associés aux instances de rôle pour faciliter la communication avec l’extérieur ou entre instances de rôle."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 8e171d56bb67c971337fa383014988074ec828b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="68806-103">Activer la communication pour les instances de rôle dans Azure</span><span class="sxs-lookup"><span data-stu-id="68806-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="68806-104">Les rôles de service cloud communiquent via des connexions internes et externes.</span><span class="sxs-lookup"><span data-stu-id="68806-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="68806-105">Les connexions externes sont appelées **points de terminaison d’entrée** tandis que les connexions internes sont appelées **points de terminaison internes**.</span><span class="sxs-lookup"><span data-stu-id="68806-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="68806-106">Cette rubrique explique comment modifier la [définition de service](cloud-services-model-and-package.md#csdef) pour créer des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="68806-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="68806-107">Point de terminaison d’entrée</span><span class="sxs-lookup"><span data-stu-id="68806-107">Input endpoint</span></span>
<span data-ttu-id="68806-108">Le point de terminaison d’entrée est utilisé lorsque vous souhaitez exposer un port à l’extérieur.</span><span class="sxs-lookup"><span data-stu-id="68806-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="68806-109">Vous spécifiez le type de protocole et le port du point de terminaison qui s’applique ensuite aux ports internes et externes du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="68806-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="68806-110">Si vous le souhaitez, vous pouvez spécifier un autre port interne pour le point de terminaison avec l’attribut [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) .</span><span class="sxs-lookup"><span data-stu-id="68806-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="68806-111">Le point de terminaison d’entrée peut utiliser les protocoles suivants : **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="68806-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="68806-112">Pour créer un point de terminaison d’entrée, ajoutez l’élément enfant **InputEndpoint** à l’élément **Endpoints** d’un rôle web ou de travail.</span><span class="sxs-lookup"><span data-stu-id="68806-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="68806-113">Point de terminaison d’entrée d’instance</span><span class="sxs-lookup"><span data-stu-id="68806-113">Instance input endpoint</span></span>
<span data-ttu-id="68806-114">Les points de terminaison d’entrée d’instance sont similaires aux points de terminaison d’entrées. Cependant, ils vous permettent de mapper des ports publics spécifiques pour chaque instance de rôle individuelle en utilisant le réacheminement de port sur l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="68806-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="68806-115">Vous pouvez spécifier un seul port public ou une plage de ports.</span><span class="sxs-lookup"><span data-stu-id="68806-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="68806-116">Le point de terminaison d’entrée d’instance peut utiliser uniquement le protocole **tcp** ou **udp**.</span><span class="sxs-lookup"><span data-stu-id="68806-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="68806-117">Pour créer un point de terminaison d’entrée d’instance, ajoutez l’élément enfant **InstanceInputEndpoint** à l’élément **Endpoints** d’un rôle web ou de travail.</span><span class="sxs-lookup"><span data-stu-id="68806-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="68806-118">Point de terminaison interne</span><span class="sxs-lookup"><span data-stu-id="68806-118">Internal endpoint</span></span>
<span data-ttu-id="68806-119">Les points de terminaison internes sont disponibles pour la communication d’instance à instance.</span><span class="sxs-lookup"><span data-stu-id="68806-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="68806-120">Le port est facultatif et, en cas d’omission, un port dynamique est affecté au point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="68806-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="68806-121">Une plage de ports peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="68806-121">A port range can be used.</span></span> <span data-ttu-id="68806-122">Le nombre de points de terminaison internes est limité à cinq par rôle.</span><span class="sxs-lookup"><span data-stu-id="68806-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="68806-123">Le point de terminaison interne peut utiliser les protocoles suivants : **http, tcp, udp, any**.</span><span class="sxs-lookup"><span data-stu-id="68806-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="68806-124">Pour créer un point de terminaison d’entrée interne, ajoutez l’élément enfant **InternalEndpoint** à l’élément **Endpoints** d’un rôle web ou de travail.</span><span class="sxs-lookup"><span data-stu-id="68806-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="68806-125">Vous pouvez également utiliser une plage de ports.</span><span class="sxs-lookup"><span data-stu-id="68806-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="68806-126">Rôles de travail et Rôles web</span><span class="sxs-lookup"><span data-stu-id="68806-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="68806-127">Les points de terminaison présentent une légère différence lorsque vous travaillez avec des rôles de travail et des rôles Web.</span><span class="sxs-lookup"><span data-stu-id="68806-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="68806-128">Avec le rôle Web, au moins un point de terminaison d’entrée doit utiliser le protocole **HTTP** .</span><span class="sxs-lookup"><span data-stu-id="68806-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="68806-129">Utilisation du Kit de développement logiciel (SDK) .NET pour accéder à un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="68806-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="68806-130">La bibliothèque managée Azure fournit des méthodes permettant aux instances de rôle de communiquer au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="68806-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="68806-131">À partir du code s’exécutant dans une instance de rôle, vous pouvez récupérer des informations sur l’existence d’autres instances de rôle et leurs points de terminaison, ainsi que des informations sur l’instance de rôle actuelle.</span><span class="sxs-lookup"><span data-stu-id="68806-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="68806-132">Vous pouvez uniquement récupérer des informations sur les instances de rôle s’exécutant dans votre service cloud et qui définissent au moins un point de terminaison interne.</span><span class="sxs-lookup"><span data-stu-id="68806-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="68806-133">Vous ne pouvez pas obtenir de données sur les instances de rôle s’exécutant dans un autre service.</span><span class="sxs-lookup"><span data-stu-id="68806-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="68806-134">Vous pouvez utiliser la propriété [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) pour récupérer les instances d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="68806-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="68806-135">Utilisez d’abord la propriété [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) pour renvoyer une référence à l’instance de rôle actuelle, puis la propriété [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) pour retourner une référence au rôle lui-même.</span><span class="sxs-lookup"><span data-stu-id="68806-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="68806-136">Lorsque vous vous connectez à une instance de rôle par programme via le Kit de développement logiciel (SDK) .NET, il est relativement facile d’accéder aux informations de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="68806-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="68806-137">Par exemple, une fois que vous êtes connecté à un environnement de rôle spécifique, vous pouvez obtenir le port d’un point de terminaison spécifique avec ce code :</span><span class="sxs-lookup"><span data-stu-id="68806-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="68806-138">La propriété **Instances** renvoie une collection d’objets **RoleInstance**.</span><span class="sxs-lookup"><span data-stu-id="68806-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="68806-139">Cette collection contient toujours l’instance actuelle.</span><span class="sxs-lookup"><span data-stu-id="68806-139">This collection always contains the current instance.</span></span> <span data-ttu-id="68806-140">Si le rôle ne définit pas de point de terminaison interne, la collection contient l’instance actuelle mais aucune autre instance.</span><span class="sxs-lookup"><span data-stu-id="68806-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="68806-141">Lorsqu’aucun point de terminaison interne n’est défini pour le rôle, la collection contient toujours une seule instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="68806-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="68806-142">Si le rôle définit un point de terminaison interne, ses instances sont détectables lors de l’exécution et le nombre d’instances dans la collection correspond au nombre d’instances spécifiées pour le rôle dans le fichier de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="68806-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="68806-143">La bibliothèque managée Azure ne fournit aucun moyen de déterminer l’intégrité des autres instances de rôle. Cependant, vous pouvez implémenter ces évaluations d’intégrité vous-même si votre service a besoin de cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="68806-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="68806-144">Vous pouvez utiliser les [diagnostics Azure](cloud-services-dotnet-diagnostics.md) pour obtenir des informations sur l’exécution des instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="68806-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="68806-145">Pour déterminer le numéro de port d’un point de terminaison interne sur une instance de rôle, vous pouvez utiliser la propriété [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) pour renvoyer un objet Dictionnaire qui contient les noms des points de terminaison et les adresses IP et ports correspondants.</span><span class="sxs-lookup"><span data-stu-id="68806-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="68806-146">La propriété [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) renvoie l’adresse IP et le port pour un point de terminaison spécifié.</span><span class="sxs-lookup"><span data-stu-id="68806-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="68806-147">La propriété **PublicIPEndpoint** renvoie le port pour un point de terminaison à charge équilibrée.</span><span class="sxs-lookup"><span data-stu-id="68806-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="68806-148">La partie de la propriété **PublicIPEndpoint** relative à l’adresse IP n’est pas utilisée.</span><span class="sxs-lookup"><span data-stu-id="68806-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="68806-149">Voici un exemple d’itération d’instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="68806-149">Here is an example that iterates role instances.</span></span>

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

<span data-ttu-id="68806-150">Voici un exemple de rôle de travail avec lequel le point de terminaison est exposé via la définition de service et commence à écouter les connexions.</span><span class="sxs-lookup"><span data-stu-id="68806-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="68806-151">Ce code ne fonctionne que pour un service déployé.</span><span class="sxs-lookup"><span data-stu-id="68806-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="68806-152">Lorsqu’ils sont exécutés dans l’émulateur de calcul Azure, les éléments de configuration de service qui créent des points de terminaison de port directs (éléments**InstanceInputEndpoint** ) sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="68806-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="68806-153">Règles de trafic réseau pour contrôler la communication entre les rôles</span><span class="sxs-lookup"><span data-stu-id="68806-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="68806-154">Après avoir défini les points de terminaison internes, vous pouvez ajouter des règles de trafic réseau (basées sur les points de terminaison que vous avez créés) pour contrôler la façon dont les instances de rôle peuvent communiquer entre elles.</span><span class="sxs-lookup"><span data-stu-id="68806-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="68806-155">Le diagramme suivant montre quelques scénarios courants relatifs au contrôle de la communication entre les rôles :</span><span class="sxs-lookup"><span data-stu-id="68806-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="68806-156">![Scénarios et règles de trafic du réseau](./media/cloud-services-enable-communication-role-instances/scenarios.png "Scénarios et règles de trafic du réseau")</span><span class="sxs-lookup"><span data-stu-id="68806-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="68806-157">L’exemple de code suivant montre des définitions de rôles pour les rôles illustrés dans le diagramme précédent.</span><span class="sxs-lookup"><span data-stu-id="68806-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="68806-158">Chaque définition de rôle inclut au moins un point de terminaison interne défini :</span><span class="sxs-lookup"><span data-stu-id="68806-158">Each role definition includes at least one internal endpoint defined:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> <span data-ttu-id="68806-159">La communication entre les rôles peut être restreinte avec les points de terminaison internes des ports fixes et affectés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="68806-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="68806-160">Par défaut, une fois un point de terminaison interne défini, la communication peut s’effectuer à partir de n’importe quel rôle vers le point de terminaison interne d’un rôle sans restriction.</span><span class="sxs-lookup"><span data-stu-id="68806-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="68806-161">Pour restreindre la communication, vous devez ajouter un élément **NetworkTrafficRules** à l’élément **ServiceDefinition** dans le fichier de définition de service.</span><span class="sxs-lookup"><span data-stu-id="68806-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="68806-162">Scénario 1</span><span class="sxs-lookup"><span data-stu-id="68806-162">Scenario 1</span></span>
<span data-ttu-id="68806-163">Autoriser uniquement le trafic réseau de **WebRole1** à **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="68806-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a><span data-ttu-id="68806-164">Scénario 2</span><span class="sxs-lookup"><span data-stu-id="68806-164">Scenario 2</span></span>
<span data-ttu-id="68806-165">Autoriser uniquement le trafic réseau de **WebRole1** à **WorkerRole1** et **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="68806-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a><span data-ttu-id="68806-166">Scénario 3</span><span class="sxs-lookup"><span data-stu-id="68806-166">Scenario 3</span></span>
<span data-ttu-id="68806-167">Autoriser uniquement le trafic réseau de **WebRole1** à **WorkerRole1** et de **WorkerRole1** à **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="68806-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a><span data-ttu-id="68806-168">Scénario 4</span><span class="sxs-lookup"><span data-stu-id="68806-168">Scenario 4</span></span>
<span data-ttu-id="68806-169">Autoriser uniquement le trafic réseau de **WebRole1** à **WorkerRole1**, de **WebRole1** à **WorkerRole2** et de **WorkerRole1** à **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="68806-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

<span data-ttu-id="68806-170">Vous trouverez une référence de schéma XML pour les éléments ci-dessus [ici](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="68806-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="68806-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68806-171">Next steps</span></span>
<span data-ttu-id="68806-172">En savoir plus sur le [modèle](cloud-services-model-and-package.md)de service cloud.</span><span class="sxs-lookup"><span data-stu-id="68806-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>

