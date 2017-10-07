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
# <a name="dns-service-in-azure-service-fabric"></a>Service DNS dans Azure Service Fabric
Hello Service DNS est un service système facultatif que vous pouvez activer dans votre cluster de toodiscover autres services utilisant le protocole DNS hello.

De nombreux services, en particulier en conteneur services, peuvent avoir un nom d’URL existant et qui est en mesure de tooresolve les à l’aide du protocole DNS standard de hello (plutôt que de protocole du Service de dénomination hello) est souhaitable, en particulier dans les scénarios « de courbes d’élévation et MAJ ». Hello service DNS permet de vous toomap noms tooa service nom DNS et donc résoudre les adresses IP de point de terminaison. 

Hello service DNS mappe les noms de tooservice de noms DNS, qui à son tour, sont résolues par le point de terminaison de service hello Naming Service tooreturn hello. nom DNS de Hello pour le service de hello est fournie au moment de la création de hello. 

![points de terminaison de service][0]

## <a name="enabling-hello-dns-service"></a>L’activation du service DNS hello
Vous devez d’abord le service DNS tooenable hello dans votre cluster. Obtenir le modèle de hello pour le cluster de hello que vous souhaitez toodeploy. Vous pouvez soit hello utilisation [exemples de modèles](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) ou créer un modèle de gestionnaire de ressources. Vous pouvez activer le service DNS hello avec hello comme suit :

1. Vérifiez que hello `apiversion` est défini trop`2017-07-01-preview` pour hello `Microsoft.ServiceFabric/clusters` ressource et dans le cas contraire, mettez-le à jour comme indiqué dans hello suivant extrait de code :

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. À présent activer le service DNS hello en ajoutant des éléments suivants de hello `addonFeatures` section après hello `fabricSettings` section comme indiqué dans hello suivant extrait de code : 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. Une fois que vous avez mis à jour votre modèle de cluster avec hello précédant les modifications, appliquez-les et laisser hello mise à niveau terminée. Une fois terminé, hello du service DNS système commence à s’exécuter dans votre cluster est appelé `fabric:/System/DnsService` sous la section du service système dans l’Explorateur de Service Fabric hello. 

Vous pouvez également activer hello service DNS via le portail de hello lors de la création du cluster hello. Hello service DNS peut être activé en vérifiant la zone hello pour `Include DNS service` Bonjour `Cluster configuration` menu comme indiqué dans hello suivant capture d’écran :

![L’activation du service DNS via le portail de hello][2]


## <a name="setting-hello-dns-name-for-your-service"></a>Paramètre de nom DNS de hello pour votre service
Une fois hello service DNS est en cours d’exécution dans votre cluster, vous pouvez définir un nom DNS pour vos services de façon déclarative pour les services par défaut Bonjour `ApplicationManifest.xml` ou de commandes Powershell.

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a>Nom DNS de hello pour un service par défaut du paramètre Bonjour ApplicationManifest.xml
Ouvrez votre projet dans Visual Studio ou votre éditeur favori, puis ouvrez les hello `ApplicationManifest.xml` fichier. Consultez la section de services toohello par défaut et pour chaque hello d’ajouter service `ServiceDnsName` attribut. Bonjour à l’exemple suivant montre comment tooset hello nom DNS du service de hello trop`service1.application1`

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
Une fois que l’application hello est déployée, instance de service hello Bonjour Service Fabric explorer affiche le nom DNS de hello pour cette instance, comme indiqué dans la figure suivante de hello : 

![points de terminaison de service][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a>Définition du nom DNS de hello pour un service à l’aide de Powershell
Vous pouvez définir le nom DNS de hello pour un service lors de la création à l’aide de hello `New-ServiceFabricService` Powershell. Hello exemple suivant crée un nouveau service sans état avec le nom DNS de hello`service1.application1`

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

## <a name="using-dns-in-your-services"></a>Utilisation de DNS dans vos services
Si vous déployez plusieurs services, vous pouvez trouver des points de terminaison de hello d’autres toocommunicate services avec à l’aide d’un nom DNS. Hello service DNS n’est applicable toostateless services, puisque hello protocole DNS ne peut pas communiquer avec les services avec état. Pour les services avec état, vous pouvez utiliser proxy inverse intégrés de hello pour toocall des appels http une partition de service particulier.

Hello de code suivant montre comment toocall un autre service, qui est simplement une régulier http appeler dans laquelle vous fournissez les port hello et n’importe quel chemin d’accès facultatif dans le cadre de l’URL de hello.

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

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur la communication avec le service cluster hello avec [se connecter et de communiquer avec les services](service-fabric-connect-and-communicate-with-services.md)

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
