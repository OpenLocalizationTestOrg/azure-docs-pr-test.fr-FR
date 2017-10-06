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
# <a name="enable-communication-for-role-instances-in-azure"></a>Activer la communication pour les instances de rôle dans Azure
Les rôles de service cloud communiquent via des connexions internes et externes. Les connexions externes sont appelées **points de terminaison d’entrée** tandis que les connexions internes sont appelées **points de terminaison internes**. Cette rubrique décrit comment toomodify hello [définition de service](cloud-services-model-and-package.md#csdef) toocreate de points de terminaison.

## <a name="input-endpoint"></a>Point de terminaison d’entrée
point de terminaison d’entrée Hello est utilisé lorsque vous souhaitez tooexpose un toohello de port à l’extérieur. Vous spécifiez le type de protocole hello et port hello du point de terminaison hello qui s’applique ensuite pour les deux ports de hello internes et externes pour le point de terminaison hello. Si vous le souhaitez, vous pouvez spécifier un autre port interne pour le point de terminaison hello avec hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribut.

point de terminaison d’entrée Hello peut utiliser hello suivant protocoles : **http, https, tcp, udp**.

toocreate un point de terminaison d’entrée, ajoutez hello **InputEndpoint** toohello d’élément enfant **points de terminaison** élément du rôle d’un site ou un processus de travail.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a>Point de terminaison d’entrée d’instance
Instance de points de terminaison d’entrée sont des points de terminaison tooinput similaires mais vous permet de mapper les ports publics spécifiques pour chaque instance de rôle individuel à l’aide de réacheminement de port sur l’équilibrage de charge hello. Vous pouvez spécifier un seul port public ou une plage de ports.

point de terminaison d’entrée Hello instance peut uniquement utiliser **tcp** ou **udp** en tant que protocole de hello.

toocreate une instance point de terminaison, ajouter hello **InstanceInputEndpoint** toohello d’élément enfant **points de terminaison** élément du rôle d’un site ou un processus de travail.

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a>Point de terminaison interne
Les points de terminaison internes sont disponibles pour la communication d’instance à instance. Hello port est facultatif et cas d’omission, un port dynamique est affecté toohello le point de terminaison. Une plage de ports peut être utilisée. Le nombre de points de terminaison internes est limité à cinq par rôle.

point de terminaison interne Hello peut utiliser hello suivant protocoles : **http, tcp, udp, n’importe quel**.

toocreate un point de terminaison d’entrée interne, ajouter hello **InternalEndpoint** toohello d’élément enfant **points de terminaison** élément du rôle d’un site ou un processus de travail.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

Vous pouvez également utiliser une plage de ports.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a>Rôles de travail et Rôles web
Les points de terminaison présentent une légère différence lorsque vous travaillez avec des rôles de travail et des rôles Web. Hello rôle web doit disposer au minimum un seul point de terminaison d’entrée à l’aide de hello **HTTP** protocole.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a>À l’aide de hello .NET SDK tooaccess un point de terminaison
Hello bibliothèque managée Azure fournit des méthodes pour toocommunicate d’instances de rôle lors de l’exécution. À partir du code en cours d’exécution au sein d’une instance de rôle, vous pouvez récupérer plus d’informations sur l’existence de hello d’autres instances de rôle et de leurs points de terminaison, ainsi que des informations sur l’instance de rôle actuelle hello.

> [!NOTE]
> Vous pouvez uniquement récupérer des informations sur les instances de rôle s’exécutant dans votre service cloud et qui définissent au moins un point de terminaison interne. Vous ne pouvez pas obtenir de données sur les instances de rôle s’exécutant dans un autre service.
> 
> 

Vous pouvez utiliser hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) instances tooretrieve de propriété d’un rôle. Tout d’abord utiliser hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn un rôle en cours de toohello de référence d’instance et ensuite utiliser hello [rôle](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) propriété tooreturn un rôle de toohello référence lui-même.

Lorsque vous vous connectez instance de rôle tooa par programmation via hello .NET SDK, il est relativement facile de tooaccess des informations de point de terminaison hello. Par exemple, une fois que vous vous êtes déjà connecté environnement de rôle spécifique tooa, vous pouvez obtenir le port hello d’un point de terminaison spécifique avec ce code :

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

Hello **Instances** propriété retourne une collection de **RoleInstance** objets. Cette collection contient toujours instance actuelle de hello. Si le rôle de hello ne définit pas de point de terminaison interne, collection de hello inclut instance actuelle de hello, mais aucune autre instance. Hello nombre d’instances de rôle dans la collection de hello sera toujours 1 dans les cas de hello où aucun point de terminaison interne n’est défini pour le rôle de hello. Si le rôle de hello définit un point de terminaison interne, ses instances sont détectables au moment de l’exécution et nombre de hello d’instances dans la collection de hello correspondront nombre toohello d’instances spécifié pour le rôle hello dans le fichier de configuration de service hello.

> [!NOTE]
> Hello bibliothèque managée Azure ne fournit pas un moyen permettant de déterminer l’intégrité de hello d’autres instances de rôle, mais vous pouvez implémenter ces évaluations d’intégrité vous-même si votre service a besoin de cette fonctionnalité. Vous pouvez utiliser [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain plus d’informations sur l’exécution des instances de rôle.
> 
> 

le numéro de port toodetermine hello pour un point de terminaison interne sur une instance de rôle, vous pouvez utiliser hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn propriété un objet dictionnaire qui contient les noms de point de terminaison et de son adresse IP correspondante des adresses et ports. Hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) propriété retourne l’adresse IP de hello et port pour un point de terminaison spécifié. Hello **PublicIPEndpoint** propriété retourne port hello pour un point de terminaison à charge équilibrée. partie d’adresse IP Hello Hello **PublicIPEndpoint** propriété n’est pas utilisée.

Voici un exemple d’itération d’instances de rôle.

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

Voici un exemple d’un rôle de travail qui obtient le point de terminaison hello exposé via la définition de service hello et commence à écouter les connexions.

> [!WARNING]
> Ce code ne fonctionne que pour un service déployé. Lors de l’exécution dans l’émulateur de calcul Azure de hello, qui créent des points de terminaison de port direct des éléments de configuration de service (**InstanceInputEndpoint** éléments) sont ignorés.
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

## <a name="network-traffic-rules-toocontrol-role-communication"></a>Le trafic règles toocontrol rôle entre le réseau
Après avoir défini les points de terminaison internes, vous pouvez ajouter toocontrol de règles (basés sur les points de terminaison hello que vous avez créé) le trafic réseau comment les instances de rôle peuvent communiquer avec eux. Hello diagramme suivant montre quelques scénarios courants pour contrôler la communication du rôle :

![Scénarios et règles de trafic du réseau](./media/cloud-services-enable-communication-role-instances/scenarios.png "Scénarios et règles de trafic du réseau")

Hello exemple de code suivant montre des définitions de rôles pour les rôles hello indiqués dans le diagramme précédent de hello. Chaque définition de rôle inclut au moins un point de terminaison interne défini :

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
> La communication entre les rôles peut être restreinte avec les points de terminaison internes des ports fixes et affectés automatiquement.
> 
> 

Par défaut, après avoir défini un point de terminaison interne, communication peut s’effectuer à partir de n’importe quel rôle toohello point de terminaison interne d’un rôle sans aucune restriction. une communication toorestrict, vous devez ajouter un **NetworkTrafficRules** élément toohello **ServiceDefinition** élément dans le fichier de définition de service hello.

### <a name="scenario-1"></a>Scénario 1
Autoriser uniquement le trafic réseau de **WebRole1** trop**WorkerRole1**.

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

### <a name="scenario-2"></a>Scénario 2
Autorise uniquement le trafic réseau de **WebRole1** trop**WorkerRole1** et **WorkerRole2**.

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

### <a name="scenario-3"></a>Scénario 3
Autorise uniquement le trafic réseau de **WebRole1** trop**WorkerRole1**, et **WorkerRole1** trop**WorkerRole2**.

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

### <a name="scenario-4"></a>Scénario 4
Autorise uniquement le trafic réseau de **WebRole1** trop**WorkerRole1**, **WebRole1** trop**WorkerRole2**, et  **WorkerRole1** trop**WorkerRole2**.

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

Une référence de schéma XML pour les éléments hello ci-dessus, vous pouvez trouver [ici](https://msdn.microsoft.com/library/azure/gg557551.aspx).

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello Service Cloud [modèle](cloud-services-model-and-package.md).

