---
title: "aaaCommunication pour les rôles dans les Services de cloud computing | Documents Microsoft"
description: "Instances de rôle dans les Services de cloud computing peuvent avoir des points de terminaison (http, https, tcp et udp) définis pour eux qui communiquent avec hello à l’extérieur ou entre les autres instances de rôle."
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
ms.openlocfilehash: 1fb39215ceb8a3f0381ef5e108c1149de115ff8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="39f69-103">Activer la communication pour les instances de rôle dans Azure</span><span class="sxs-lookup"><span data-stu-id="39f69-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="39f69-104">Les rôles de service cloud communiquent via des connexions internes et externes.</span><span class="sxs-lookup"><span data-stu-id="39f69-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="39f69-105">Les connexions externes sont appelées **points de terminaison d’entrée** tandis que les connexions internes sont appelées **points de terminaison internes**.</span><span class="sxs-lookup"><span data-stu-id="39f69-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="39f69-106">Cette rubrique décrit comment toomodify hello [définition de service](cloud-services-model-and-package.md#csdef) toocreate de points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="39f69-106">This topic describes how toomodify hello [service definition](cloud-services-model-and-package.md#csdef) toocreate endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="39f69-107">Point de terminaison d’entrée</span><span class="sxs-lookup"><span data-stu-id="39f69-107">Input endpoint</span></span>
<span data-ttu-id="39f69-108">point de terminaison d’entrée Hello est utilisé lorsque vous souhaitez tooexpose un toohello de port à l’extérieur.</span><span class="sxs-lookup"><span data-stu-id="39f69-108">hello input endpoint is used when you want tooexpose a port toohello outside.</span></span> <span data-ttu-id="39f69-109">Vous spécifiez le type de protocole hello et port hello du point de terminaison hello qui s’applique ensuite pour les deux ports de hello internes et externes pour le point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="39f69-109">You specify hello protocol type and hello port of hello endpoint which then applies for both hello external and internal ports for hello endpoint.</span></span> <span data-ttu-id="39f69-110">Si vous le souhaitez, vous pouvez spécifier un autre port interne pour le point de terminaison hello avec hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribut.</span><span class="sxs-lookup"><span data-stu-id="39f69-110">If you want, you can specify a different internal port for hello endpoint with hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="39f69-111">point de terminaison d’entrée Hello peut utiliser hello suivant protocoles : **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="39f69-111">hello input endpoint can use hello following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="39f69-112">toocreate un point de terminaison d’entrée, ajoutez hello **InputEndpoint** toohello d’élément enfant **points de terminaison** élément du rôle d’un site ou un processus de travail.</span><span class="sxs-lookup"><span data-stu-id="39f69-112">toocreate an input endpoint, add hello **InputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="39f69-113">Point de terminaison d’entrée d’instance</span><span class="sxs-lookup"><span data-stu-id="39f69-113">Instance input endpoint</span></span>
<span data-ttu-id="39f69-114">Instance de points de terminaison d’entrée sont des points de terminaison tooinput similaires mais vous permet de mapper les ports publics spécifiques pour chaque instance de rôle individuel à l’aide de réacheminement de port sur l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="39f69-114">Instance input endpoints are similar tooinput endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on hello load balancer.</span></span> <span data-ttu-id="39f69-115">Vous pouvez spécifier un seul port public ou une plage de ports.</span><span class="sxs-lookup"><span data-stu-id="39f69-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="39f69-116">point de terminaison d’entrée Hello instance peut uniquement utiliser **tcp** ou **udp** en tant que protocole de hello.</span><span class="sxs-lookup"><span data-stu-id="39f69-116">hello instance input endpoint can only use **tcp** or **udp** as hello protocol.</span></span>

<span data-ttu-id="39f69-117">toocreate une instance point de terminaison, ajouter hello **InstanceInputEndpoint** toohello d’élément enfant **points de terminaison** élément du rôle d’un site ou un processus de travail.</span><span class="sxs-lookup"><span data-stu-id="39f69-117">toocreate an instance input endpoint, add hello **InstanceInputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="39f69-118">Point de terminaison interne</span><span class="sxs-lookup"><span data-stu-id="39f69-118">Internal endpoint</span></span>
<span data-ttu-id="39f69-119">Les points de terminaison internes sont disponibles pour la communication d’instance à instance.</span><span class="sxs-lookup"><span data-stu-id="39f69-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="39f69-120">Hello port est facultatif et cas d’omission, un port dynamique est affecté toohello le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="39f69-120">hello port is optional and if omitted, a dynamic port is assigned toohello endpoint.</span></span> <span data-ttu-id="39f69-121">Une plage de ports peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="39f69-121">A port range can be used.</span></span> <span data-ttu-id="39f69-122">Le nombre de points de terminaison internes est limité à cinq par rôle.</span><span class="sxs-lookup"><span data-stu-id="39f69-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="39f69-123">point de terminaison interne Hello peut utiliser hello suivant protocoles : **http, tcp, udp, n’importe quel**.</span><span class="sxs-lookup"><span data-stu-id="39f69-123">hello internal endpoint can use hello following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="39f69-124">toocreate un point de terminaison d’entrée interne, ajouter hello **InternalEndpoint** toohello d’élément enfant **points de terminaison** élément du rôle d’un site ou un processus de travail.</span><span class="sxs-lookup"><span data-stu-id="39f69-124">toocreate an internal input endpoint, add hello **InternalEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="39f69-125">Vous pouvez également utiliser une plage de ports.</span><span class="sxs-lookup"><span data-stu-id="39f69-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="39f69-126">Rôles de travail et Rôles web</span><span class="sxs-lookup"><span data-stu-id="39f69-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="39f69-127">Les points de terminaison présentent une légère différence lorsque vous travaillez avec des rôles de travail et des rôles Web.</span><span class="sxs-lookup"><span data-stu-id="39f69-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="39f69-128">Hello rôle web doit disposer au minimum un seul point de terminaison d’entrée à l’aide de hello **HTTP** protocole.</span><span class="sxs-lookup"><span data-stu-id="39f69-128">hello web role must have at minimum a single input endpoint using hello **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a><span data-ttu-id="39f69-129">À l’aide de hello .NET SDK tooaccess un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="39f69-129">Using hello .NET SDK tooaccess an endpoint</span></span>
<span data-ttu-id="39f69-130">Hello bibliothèque managée Azure fournit des méthodes pour toocommunicate d’instances de rôle lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="39f69-130">hello Azure Managed Library provides methods for role instances toocommunicate at runtime.</span></span> <span data-ttu-id="39f69-131">À partir du code en cours d’exécution au sein d’une instance de rôle, vous pouvez récupérer plus d’informations sur l’existence de hello d’autres instances de rôle et de leurs points de terminaison, ainsi que des informations sur l’instance de rôle actuelle hello.</span><span class="sxs-lookup"><span data-stu-id="39f69-131">From code running within a role instance, you can retrieve information about hello existence of other role instances and their endpoints, as well as information about hello current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="39f69-132">Vous pouvez uniquement récupérer des informations sur les instances de rôle s’exécutant dans votre service cloud et qui définissent au moins un point de terminaison interne.</span><span class="sxs-lookup"><span data-stu-id="39f69-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="39f69-133">Vous ne pouvez pas obtenir de données sur les instances de rôle s’exécutant dans un autre service.</span><span class="sxs-lookup"><span data-stu-id="39f69-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="39f69-134">Vous pouvez utiliser hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) instances tooretrieve de propriété d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="39f69-134">You can use hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property tooretrieve instances of a role.</span></span> <span data-ttu-id="39f69-135">Tout d’abord utiliser hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn un rôle en cours de toohello de référence d’instance et ensuite utiliser hello [rôle](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) propriété tooreturn un rôle de toohello référence lui-même.</span><span class="sxs-lookup"><span data-stu-id="39f69-135">First use hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn a reference toohello current role instance, and then use hello [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property tooreturn a reference toohello role itself.</span></span>

<span data-ttu-id="39f69-136">Lorsque vous vous connectez instance de rôle tooa par programmation via hello .NET SDK, il est relativement facile de tooaccess des informations de point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="39f69-136">When you connect tooa role instance programmatically through hello .NET SDK, it's relatively easy tooaccess hello endpoint information.</span></span> <span data-ttu-id="39f69-137">Par exemple, une fois que vous vous êtes déjà connecté environnement de rôle spécifique tooa, vous pouvez obtenir le port hello d’un point de terminaison spécifique avec ce code :</span><span class="sxs-lookup"><span data-stu-id="39f69-137">For example, after you've already connected tooa specific role environment, you can get hello port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="39f69-138">Hello **Instances** propriété retourne une collection de **RoleInstance** objets.</span><span class="sxs-lookup"><span data-stu-id="39f69-138">hello **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="39f69-139">Cette collection contient toujours instance actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="39f69-139">This collection always contains hello current instance.</span></span> <span data-ttu-id="39f69-140">Si le rôle de hello ne définit pas de point de terminaison interne, collection de hello inclut instance actuelle de hello, mais aucune autre instance.</span><span class="sxs-lookup"><span data-stu-id="39f69-140">If hello role does not define an internal endpoint, hello collection includes hello current instance but no other instances.</span></span> <span data-ttu-id="39f69-141">Hello nombre d’instances de rôle dans la collection de hello sera toujours 1 dans les cas de hello où aucun point de terminaison interne n’est défini pour le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="39f69-141">hello number of role instances in hello collection will always be 1 in hello case where no internal endpoint is defined for hello role.</span></span> <span data-ttu-id="39f69-142">Si le rôle de hello définit un point de terminaison interne, ses instances sont détectables au moment de l’exécution et nombre de hello d’instances dans la collection de hello correspondront nombre toohello d’instances spécifié pour le rôle hello dans le fichier de configuration de service hello.</span><span class="sxs-lookup"><span data-stu-id="39f69-142">If hello role defines an internal endpoint, its instances are discoverable at runtime, and hello number of instances in hello collection will correspond toohello number of instances specified for hello role in hello service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="39f69-143">Hello bibliothèque managée Azure ne fournit pas un moyen permettant de déterminer l’intégrité de hello d’autres instances de rôle, mais vous pouvez implémenter ces évaluations d’intégrité vous-même si votre service a besoin de cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="39f69-143">hello Azure Managed Library does not provide a means of determining hello health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="39f69-144">Vous pouvez utiliser [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain plus d’informations sur l’exécution des instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="39f69-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="39f69-145">le numéro de port toodetermine hello pour un point de terminaison interne sur une instance de rôle, vous pouvez utiliser hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn propriété un objet dictionnaire qui contient les noms de point de terminaison et de son adresse IP correspondante des adresses et ports.</span><span class="sxs-lookup"><span data-stu-id="39f69-145">toodetermine hello port number for an internal endpoint on a role instance, you can use hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property tooreturn a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="39f69-146">Hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) propriété retourne l’adresse IP de hello et port pour un point de terminaison spécifié.</span><span class="sxs-lookup"><span data-stu-id="39f69-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns hello IP address and port for a specified endpoint.</span></span> <span data-ttu-id="39f69-147">Hello **PublicIPEndpoint** propriété retourne port hello pour un point de terminaison à charge équilibrée.</span><span class="sxs-lookup"><span data-stu-id="39f69-147">hello **PublicIPEndpoint** property returns hello port for a load balanced endpoint.</span></span> <span data-ttu-id="39f69-148">partie d’adresse IP Hello Hello **PublicIPEndpoint** propriété n’est pas utilisée.</span><span class="sxs-lookup"><span data-stu-id="39f69-148">hello IP address portion of hello **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="39f69-149">Voici un exemple d’itération d’instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="39f69-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="39f69-150">Voici un exemple d’un rôle de travail qui obtient le point de terminaison hello exposé via la définition de service hello et commence à écouter les connexions.</span><span class="sxs-lookup"><span data-stu-id="39f69-150">Here is an example of a worker role that gets hello endpoint exposed through hello service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="39f69-151">Ce code ne fonctionne que pour un service déployé.</span><span class="sxs-lookup"><span data-stu-id="39f69-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="39f69-152">Lors de l’exécution dans l’émulateur de calcul Azure de hello, qui créent des points de terminaison de port direct des éléments de configuration de service (**InstanceInputEndpoint** éléments) sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="39f69-152">When running in hello Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

        // Bind socket listener toointernal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block hello thread and wait for a client request
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
      // Set hello maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-toocontrol-role-communication"></a><span data-ttu-id="39f69-153">Le trafic règles toocontrol rôle entre le réseau</span><span class="sxs-lookup"><span data-stu-id="39f69-153">Network traffic rules toocontrol role communication</span></span>
<span data-ttu-id="39f69-154">Après avoir défini les points de terminaison internes, vous pouvez ajouter toocontrol de règles (basés sur les points de terminaison hello que vous avez créé) le trafic réseau comment les instances de rôle peuvent communiquer avec eux.</span><span class="sxs-lookup"><span data-stu-id="39f69-154">After you define internal endpoints, you can add network traffic rules (based on hello endpoints that you created) toocontrol how role instances can communicate with each other.</span></span> <span data-ttu-id="39f69-155">Hello diagramme suivant montre quelques scénarios courants pour contrôler la communication du rôle :</span><span class="sxs-lookup"><span data-stu-id="39f69-155">hello following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="39f69-156">![Scénarios et règles de trafic du réseau](./media/cloud-services-enable-communication-role-instances/scenarios.png "Scénarios et règles de trafic du réseau")</span><span class="sxs-lookup"><span data-stu-id="39f69-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="39f69-157">Hello exemple de code suivant montre des définitions de rôles pour les rôles hello indiqués dans le diagramme précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="39f69-157">hello following code example shows role definitions for hello roles shown in hello previous diagram.</span></span> <span data-ttu-id="39f69-158">Chaque définition de rôle inclut au moins un point de terminaison interne défini :</span><span class="sxs-lookup"><span data-stu-id="39f69-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="39f69-159">La communication entre les rôles peut être restreinte avec les points de terminaison internes des ports fixes et affectés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="39f69-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="39f69-160">Par défaut, après avoir défini un point de terminaison interne, communication peut s’effectuer à partir de n’importe quel rôle toohello point de terminaison interne d’un rôle sans aucune restriction.</span><span class="sxs-lookup"><span data-stu-id="39f69-160">By default, after an internal endpoint is defined, communication can flow from any role toohello internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="39f69-161">une communication toorestrict, vous devez ajouter un **NetworkTrafficRules** élément toohello **ServiceDefinition** élément dans le fichier de définition de service hello.</span><span class="sxs-lookup"><span data-stu-id="39f69-161">toorestrict communication, you must add a **NetworkTrafficRules** element toohello **ServiceDefinition** element in hello service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="39f69-162">Scénario 1</span><span class="sxs-lookup"><span data-stu-id="39f69-162">Scenario 1</span></span>
<span data-ttu-id="39f69-163">Autoriser uniquement le trafic réseau de **WebRole1** trop**WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="39f69-163">Only allow network traffic from **WebRole1** too**WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="39f69-164">Scénario 2</span><span class="sxs-lookup"><span data-stu-id="39f69-164">Scenario 2</span></span>
<span data-ttu-id="39f69-165">Autorise uniquement le trafic réseau de **WebRole1** trop**WorkerRole1** et **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="39f69-165">Only allows network traffic from **WebRole1** too**WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="39f69-166">Scénario 3</span><span class="sxs-lookup"><span data-stu-id="39f69-166">Scenario 3</span></span>
<span data-ttu-id="39f69-167">Autorise uniquement le trafic réseau de **WebRole1** trop**WorkerRole1**, et **WorkerRole1** trop**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="39f69-167">Only allows network traffic from **WebRole1** too**WorkerRole1**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="39f69-168">Scénario 4</span><span class="sxs-lookup"><span data-stu-id="39f69-168">Scenario 4</span></span>
<span data-ttu-id="39f69-169">Autorise uniquement le trafic réseau de **WebRole1** trop**WorkerRole1**, **WebRole1** trop**WorkerRole2**, et  **WorkerRole1** trop**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="39f69-169">Only allows network traffic from **WebRole1** too**WorkerRole1**, **WebRole1** too**WorkerRole2**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

<span data-ttu-id="39f69-170">Une référence de schéma XML pour les éléments hello ci-dessus, vous pouvez trouver [ici](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="39f69-170">An XML schema reference for hello elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="39f69-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39f69-171">Next steps</span></span>
<span data-ttu-id="39f69-172">En savoir plus sur hello Service Cloud [modèle](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="39f69-172">Read more about hello Cloud Service [model](cloud-services-model-and-package.md).</span></span>

