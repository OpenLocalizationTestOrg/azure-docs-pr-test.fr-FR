---
title: "aaaAzure service DNS de l’infrastructure de Service | Documents Microsoft"
description: "Utiliser le service dns pour la détection des microservices à partir du Service Fabric à l’intérieur du cluster de hello."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/27/2017
ms.author: msfussell
ms.openlocfilehash: fa536f0e41f52c4942702d0a1bdcd3ed7d418d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="329fb-103">Service DNS dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="329fb-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="329fb-104">Hello Service DNS est un service système facultatif que vous pouvez activer dans votre cluster de toodiscover autres services utilisant le protocole DNS hello.</span><span class="sxs-lookup"><span data-stu-id="329fb-104">hello DNS Service is an optional system service that you can enable in your cluster toodiscover other services using hello DNS protocol.</span></span>

<span data-ttu-id="329fb-105">De nombreux services, en particulier en conteneur services, peuvent avoir un nom d’URL existant et qui est en mesure de tooresolve les à l’aide du protocole DNS standard de hello (plutôt que de protocole du Service de dénomination hello) est souhaitable, en particulier dans les scénarios « de courbes d’élévation et MAJ ».</span><span class="sxs-lookup"><span data-stu-id="329fb-105">Many services, especially containerized services, can have an existing URL name, and being able tooresolve them using hello standard DNS protocol (rather than hello Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="329fb-106">Hello service DNS permet de vous toomap noms tooa service nom DNS et donc résoudre les adresses IP de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="329fb-106">hello DNS service enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="329fb-107">Hello service DNS mappe les noms de tooservice de noms DNS, qui à son tour, sont résolues par le point de terminaison de service hello Naming Service tooreturn hello.</span><span class="sxs-lookup"><span data-stu-id="329fb-107">hello DNS service maps DNS names tooservice names, which in turn are resolved by hello Naming Service tooreturn hello service endpoint.</span></span> <span data-ttu-id="329fb-108">nom DNS de Hello pour le service de hello est fournie au moment de la création de hello.</span><span class="sxs-lookup"><span data-stu-id="329fb-108">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![points de terminaison de service][0]

## <a name="enabling-hello-dns-service"></a><span data-ttu-id="329fb-110">L’activation du service DNS hello</span><span class="sxs-lookup"><span data-stu-id="329fb-110">Enabling hello DNS service</span></span>
<span data-ttu-id="329fb-111">Vous devez d’abord le service DNS tooenable hello dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="329fb-111">First you need tooenable hello DNS service in your cluster.</span></span> <span data-ttu-id="329fb-112">Obtenir le modèle de hello pour le cluster de hello que vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="329fb-112">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="329fb-113">Vous pouvez soit hello utilisation [exemples de modèles](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) ou créer un modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="329fb-113">You can either use hello [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="329fb-114">Vous pouvez activer le service DNS hello avec hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="329fb-114">You can enable hello DNS service with hello following steps:</span></span>

1. <span data-ttu-id="329fb-115">Vérifiez que hello `apiversion` est défini trop`2017-07-01-preview` pour hello `Microsoft.ServiceFabric/clusters` ressource et dans le cas contraire, mettez-le à jour comme indiqué dans hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="329fb-115">Check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in hello following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="329fb-116">À présent activer le service DNS hello en ajoutant des éléments suivants de hello `addonFeatures` section après hello `fabricSettings` section comme indiqué dans hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="329fb-116">Now enable hello DNS service by adding hello following `addonFeatures` section after hello `fabricSettings` section as shown in hello following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="329fb-117">Une fois que vous avez mis à jour votre modèle de cluster avec hello précédant les modifications, appliquez-les et laisser hello mise à niveau terminée.</span><span class="sxs-lookup"><span data-stu-id="329fb-117">Once you have updated your cluster template with hello preceding changes, apply them and let hello upgrade complete.</span></span> <span data-ttu-id="329fb-118">Une fois terminé, hello du service DNS système commence à s’exécuter dans votre cluster est appelé `fabric:/System/DnsService` sous la section du service système dans l’Explorateur de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="329fb-118">Once complete, hello DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in hello Service Fabric explorer.</span></span> 

<span data-ttu-id="329fb-119">Vous pouvez également activer hello service DNS via le portail de hello lors de la création du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="329fb-119">Alternatively, you can enable hello DNS service through hello portal at hello time of cluster creation.</span></span> <span data-ttu-id="329fb-120">Hello service DNS peut être activé en vérifiant la zone hello pour `Include DNS service` Bonjour `Cluster configuration` menu comme indiqué dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="329fb-120">hello DNS service can be enabled by checking hello box for `Include DNS service` in hello `Cluster configuration` menu as shown in hello following screenshot:</span></span>

![L’activation du service DNS via le portail de hello][2]


## <a name="setting-hello-dns-name-for-your-service"></a><span data-ttu-id="329fb-122">Paramètre de nom DNS de hello pour votre service</span><span class="sxs-lookup"><span data-stu-id="329fb-122">Setting hello DNS name for your service</span></span>
<span data-ttu-id="329fb-123">Une fois hello service DNS est en cours d’exécution dans votre cluster, vous pouvez définir un nom DNS pour vos services de façon déclarative pour les services par défaut Bonjour `ApplicationManifest.xml` ou de commandes Powershell.</span><span class="sxs-lookup"><span data-stu-id="329fb-123">Once hello DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in hello `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a><span data-ttu-id="329fb-124">Nom DNS de hello pour un service par défaut du paramètre Bonjour ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="329fb-124">Setting hello DNS name for a default service in hello ApplicationManifest.xml</span></span>
<span data-ttu-id="329fb-125">Ouvrez votre projet dans Visual Studio ou votre éditeur favori, puis ouvrez les hello `ApplicationManifest.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="329fb-125">Open your project in Visual Studio, or your favorite editor, and open hello `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="329fb-126">Consultez la section de services toohello par défaut et pour chaque hello d’ajouter service `ServiceDnsName` attribut.</span><span class="sxs-lookup"><span data-stu-id="329fb-126">Go toohello default services section, and for each service add hello `ServiceDnsName` attribute.</span></span> <span data-ttu-id="329fb-127">Bonjour à l’exemple suivant montre comment tooset hello nom DNS du service de hello trop`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="329fb-127">hello following example shows how tooset hello DNS name of hello service too`service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="329fb-128">Une fois que l’application hello est déployée, instance de service hello Bonjour Service Fabric explorer affiche le nom DNS de hello pour cette instance, comme indiqué dans la figure suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="329fb-128">Once hello application is deployed, hello service instance in hello Service Fabric explorer shows hello DNS name for this instance, as shown in hello following figure:</span></span> 

![points de terminaison de service][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="329fb-130">Définition du nom DNS de hello pour un service à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="329fb-130">Setting hello DNS name for a service using Powershell</span></span>
<span data-ttu-id="329fb-131">Vous pouvez définir le nom DNS de hello pour un service lors de la création à l’aide de hello `New-ServiceFabricService` Powershell.</span><span class="sxs-lookup"><span data-stu-id="329fb-131">You can set hello DNS name for a service when creating it using hello `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="329fb-132">Hello exemple suivant crée un nouveau service sans état avec le nom DNS de hello`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="329fb-132">hello following example creates a new stateless service with hello DNS name `service1.application1`</span></span>

```powershell
    New-ServiceFabricService `
    -Stateless `
    -PartitionSchemeSingleton `
    -ApplicationName `fabric:/application1 `
    -ServiceName fabric:/application1/service1 `
    -ServiceTypeName Service1Type `
    -InstanceCount 1 `
    -ServiceDnsName service1.application1
```

## <a name="using-dns-in-your-services"></a><span data-ttu-id="329fb-133">Utilisation de DNS dans vos services</span><span class="sxs-lookup"><span data-stu-id="329fb-133">Using DNS in your services</span></span>
<span data-ttu-id="329fb-134">Si vous déployez plusieurs services, vous pouvez trouver des points de terminaison de hello d’autres toocommunicate services avec à l’aide d’un nom DNS.</span><span class="sxs-lookup"><span data-stu-id="329fb-134">If you deploy more than one service, you can find hello endpoints of other services toocommunicate with  by using a DNS name.</span></span> <span data-ttu-id="329fb-135">Hello service DNS n’est applicable toostateless services, puisque hello protocole DNS ne peut pas communiquer avec les services avec état.</span><span class="sxs-lookup"><span data-stu-id="329fb-135">hello DNS service is only applicable toostateless services, since hello DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="329fb-136">Pour les services avec état, vous pouvez utiliser proxy inverse intégrés de hello pour toocall des appels http une partition de service particulier.</span><span class="sxs-lookup"><span data-stu-id="329fb-136">For stateful services, you can use hello built-in reverse proxy for http calls toocall a particular service partition.</span></span>

<span data-ttu-id="329fb-137">Hello de code suivant montre comment toocall un autre service, qui est simplement une régulier http appeler dans laquelle vous fournissez les port hello et n’importe quel chemin d’accès facultatif dans le cadre de l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="329fb-137">hello following code shows how toocall another service, which is simply a regular http call where you provide hello port and any optional path as part of hello URL.</span></span>

```csharp
public class ValuesController : Controller
{
    // GET api
    [HttpGet]
    public async Task<string> Get()
    {
        string result = "";
        try
        {
            Uri uri = new Uri("http://service1.application1:8080/api/values");
            HttpClient client = new HttpClient();
            var response = await client.GetAsync(uri);
            result = await response.Content.ReadAsStringAsync();
            
        }
        catch (Exception e)
        {
            Console.Write(e.Message);
        }

        return result;
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="329fb-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="329fb-138">Next steps</span></span>
<span data-ttu-id="329fb-139">En savoir plus sur la communication avec le service cluster hello avec [se connecter et de communiquer avec les services](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="329fb-139">Learn more about service communication within hello cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
