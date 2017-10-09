---
title: "aaaAzure l’infrastructure de Service de proxy inverse | Documents Microsoft"
description: "Utilisez le proxy inverse de l’architecture de Service pour toomicroservices de communication de l’intérieur et extérieur cluster de hello."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a>Proxy inverse dans Azure Service Fabric
les adresses de proxy inverse Hello qui est intégrée à Azure Service Fabric microservices Cluster Service Fabric hello qui expose les points de terminaison HTTP.

## <a name="microservices-communication-model"></a>Modèle de communication des microservices
En général, Microservices dans l’infrastructure de Service s’exécutent sur un sous-ensemble d’ordinateurs virtuels dans un cluster de hello et pouvez déplacer à partir d’un ordinateur virtuel tooanother pour diverses raisons. Par conséquent, les points de terminaison hello pour microservices peuvent changer dynamiquement. Hello modèle classique toocommunicate toohello microservice est la suivante de hello résoudre boucle :

1. Résoudre l’emplacement du service hello initialement par le biais de service d’affectation de noms de hello.
2. Se connecter toohello service.
3. Déterminer la cause de hello d’échecs de connexion et les résoudre à nouveau l’emplacement du service hello lorsque cela est nécessaire.

Ce processus implique généralement l’habillage des bibliothèques côté client communication dans une boucle de tentatives qui implémente des stratégies de résolution, puis réessayez de service hello.
Pour plus d’informations, consultez la page [Se connecter et communiquer avec les services](service-fabric-connect-and-communicate-with-services.md).

### <a name="communicating-by-using-hello-reverse-proxy"></a>Communication à l’aide de proxy inverse de hello
proxy inverse de Hello dans l’infrastructure de Service s’exécute sur tous les nœuds hello cluster de hello. Il exécute le processus de résolution d’ensemble du service hello pour un client et transmet ensuite la demande du client hello. Par conséquent, les clients qui s’exécutent sur le cluster de hello peuvent utiliser n’importe quel service cible de côté client HTTP communication bibliothèques tootalk toohello à l’aide de proxy inverse de hello que s’exécute localement sur hello même nœud.

![Communications internes][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a>Atteindre microservices à partir du cluster en dehors de hello
modèle de communication externe par défaut Hello pour microservices est un modèle d’abonnement dans lequel chaque service ne sont pas accessibles directement à partir de clients externes. [Équilibrage de charge Azure](../load-balancer/load-balancer-overview.md), qui est une limite réseau entre les clients externes et de microservices exécute traduction d’adresses réseau et de points de terminaison IP : port toointernal demande des transferts externe. toomake clients de tooexternal directement accessibles de point de terminaison d’un microservice, vous devez d’abord configurer équilibrage de charge de port tooeach tooforward le trafic qui hello service utilise dans un cluster de hello. En outre, la plupart des microservices, en particulier avec état microservices, ne live sur tous les nœuds du cluster de hello. Hello microservices pouvez déplacer entre les nœuds de basculement. Dans ce cas, équilibrage de charge ne peut pas déterminer efficacement d’emplacement de hello du nœud cible de hello de hello réplicas toowhich, il doit transférer le trafic.

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a>Atteindre microservices via le proxy inverse hello du cluster de hello externe
Au lieu de configurer le port hello des services individuels dans l’équilibrage de charge, vous pouvez configurer simplement hello port proxy inverse de hello dans l’équilibrage de charge. Cette configuration permet aux clients en dehors du cluster de hello de contacter les services à l’intérieur de hello cluster à l’aide de proxy inverse de hello sans configuration supplémentaire.

![Communications externes][0]

> [!WARNING]
> Lorsque vous configurez un port de proxy inverse hello dans l’équilibrage de charge, toutes les microservices dans un cluster de hello qui exposent un point de terminaison HTTP sont adressables à partir de l’extérieur hello cluster.
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a>Format d’URI pour l’adressage des services à l’aide de proxy inverse de hello
utilisations de proxy inverse Hello qu'une URI spécifique identificateur URI () format tooidentify hello partition toowhich hello entrants demande de service doit être transférée :

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* **HTTP (s) :** proxy inverse de hello peut être configuré tooaccept HTTP ou le trafic HTTPS. Pour le transfert HTTPS, consultez trop[connecter tooa le service sécurisé avec le proxy inverse hello](service-fabric-reverseproxy-configure-secure-communication.md) une fois que vous avez toolisten le programme d’installation de proxy inverse sur HTTPS.
* **Nom de domaine complet de cluster (nom de domaine complet) | adresse IP interne :** pour les clients externes, vous pouvez configurer le proxy inverse de hello afin qu’il soit accessible via le domaine du cluster hello, telles que mycluster.eastus.cloudapp.azure.com. Par défaut, le proxy inverse de hello s’exécute sur chaque nœud. Pour le trafic interne, le proxy inverse de hello peut être atteint sur localhost ou sur toutes les adresses IP internes de nœud, telle que 10.0.0.1.
* **Port :** port hello, telles que 19081, qui a été spécifié pour le proxy inverse de hello.
* **ServiceInstanceName :** Voici nom qualifié complet de hello hello déployé des instances de service que vous essayez de tooreach sans hello « fabric : / « schéma. Par exemple, tooreach hello *fabric : / myapp/myservice/* service, vous utiliseriez *myapp/myservice*.

    nom de l’instance service Hello respecte la casse. À l’aide d’une casse différente pour le nom de l’instance service hello dans les URL hello entraîne hello demandes toofail 404 (introuvable).
* **Chemin d’accès de suffixe :** Voici hello URL du chemin d’accès réel, tel que *myapi/valeurs/ajouter/3*, service hello tooconnect à souhaitées.
* **PartitionKey :** pour un service partitionné, il s’agit clé de partition calculée hello de partition hello que vous souhaitez tooreach. Notez que cela est *pas* hello GUID ID de partition. Ce paramètre n’est pas obligatoire pour les services qui utilisent le schéma de partition singleton hello.
* **PartitionKind :** schéma de partition de service hello. Il peut s’agir de Named ou Int64Range. Ce paramètre n’est pas obligatoire pour les services qui utilisent le schéma de partition singleton hello.
* **ListenerName** hello des points de terminaison de service de hello sont sous forme de hello {« Points de terminaison » : {« Listener1 » : « Endpoint1 », « Listener2 » : « Endpoint2 »...}}. Lorsque le service de hello expose plusieurs points de terminaison, il identifie le point de terminaison hello requête hello du client doit être transférée. Cela peut être omis si le service de hello n'a qu’un seul écouteur.
* **TargetReplicaSelector** spécifie comment réplica cible de hello ou une instance doit être sélectionné.
  * Lorsque le service cible de hello est avec état, hello TargetReplicaSelector peut s’agir de hello : 'PrimaryReplica', 'RandomSecondaryReplica' ou 'RandomReplica'. Lorsque ce paramètre n’est pas spécifié, la valeur par défaut de la hello est 'PrimaryReplica'.
  * Lorsque le service cible de hello est sans état, le proxy inverse récupère une instance aléatoire de hello partition tooforward hello demande de service.
* **Délai d’expiration :** cela spécifie le délai d’attente de hello pour demande de hello HTTP créée par le service de toohello hello proxy inverse pour le compte de demande du client hello. Hello par défaut est 60 secondes. Paramètre facultatif.

### <a name="example-usage"></a>Exemple d’utilisation
Par exemple, prenons hello *fabric : / MyApp/MyService* service qui ouvre un écouteur HTTP sur hello suivant l’URL :

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

Voici des ressources hello pour le service de hello :

* `/index.html`
* `/api/users/<userId>`

Si le service de hello utilise singleton hello schéma de partitionnement, hello *PartitionKey* et *PartitionKind* les paramètres de chaîne de requête ne sont pas requis, et est accessible à l’aide de passerelle hello en tant que service de hello :

* En externe : `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`
* En interne : `http://localhost:19081/MyApp/MyService`

Si le service de hello utilise hello Int64 uniforme, schéma de partitionnement, hello *PartitionKey* et *PartitionKind* les paramètres de chaîne de requête doivent être utilisé tooreach une partition de service de hello :

* En externe : `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`
* En interne : `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`

ressources hello tooreach hello exposée par service, placez simplement le chemin d’accès de ressource hello après le nom du service hello dans hello URL :

* En externe : `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`
* En interne : `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`

Hello puis envoie l’URL du service toohello de ces demandes :

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a>Traitement spécial des services de partage de port
Passerelle d’Application Azure tentatives tooresolve un service de traiter à nouveau, puis réessayez de demande de hello lorsqu’un service ne peut pas être atteint. Il s’agit d’un avantage majeur de la passerelle d’Application, car le code client ne devez tooimplement sa propre résolution de noms de service et résoudre la boucle.

En général, lorsqu’un service ne peut pas être atteinte, l’instance de service hello ou réplica a déplacé tooa autre nœud dans le cadre de son cycle de vie normal. Dans ce cas, passerelle d’Application peut recevoir un réseau connexion d’erreur indiquant qu’un point de terminaison est que sans ouvrir plus de temps sur hello résolu à l’origine d’adresse.

Toutefois, les instances de service ou réplicas peuvent partager un processus hôte, voire un port, lorsqu’ils sont hébergés par un serveur web basé sur HTTP.sys. Cela inclut :

* [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [ASP.NET Core WebListener](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [Katana](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

Dans ce cas, il est probable que le serveur web hello est disponible dans le processus hôte de hello et répondre toorequests mais hello résolu l’instance de service ou le réplica n’est plus disponible sur l’ordinateur hôte de hello. Dans ce cas, la passerelle de hello recevra une réponse HTTP 404 à partir du serveur web de hello. Par conséquent, une réponse HTTP 404 a deux sens distincts :

- Casse #1 : adresse du service hello est correcte, mais la ressource hello hello utilisateur demandé n’existe pas.
- Cas #2 : adresse du service hello est incorrect et ressource hello hello utilisateur demandée peut exister sur un autre nœud.

Hello premier cas est une erreur 404 HTTP normal, qui est considérée comme une erreur de l’utilisateur. Toutefois, dans les cas de deuxième hello, utilisateur de hello a demandé une ressource qui existe. Passerelle d’application a été toolocate impossible que car hello service lui-même a déplacé. Application besoins tooresolve hello adresse de passerelle à nouveau et demande hello de nouvelle tentative.

Passerelle d’application doit donc un toodistinguish moyen entre ces deux cas. toomake que distinction, un indicateur à partir du serveur de hello est requis.

* Par défaut, la passerelle d’Application suppose cas #2 et tente de demande de hello tooresolve et émettre à nouveau.
* tooApplication de cas #1 tooindicate passerelle, hello service doit retourner la hello suivant l’en-tête de réponse HTTP :

  `X-ServiceFabric : ResourceNotFound`

Cet en-tête de réponse HTTP indique une situation HTTP 404 normale dans le hello la ressource demandée n’existe pas, et la passerelle d’Application ne tente pas d’adresse du service tooresolve hello à nouveau.

## <a name="setup-and-configuration"></a>Installation et configuration

### <a name="enable-reverse-proxy-via-azure-portal"></a>Activer le proxy inverse via le portail Azure

Portail Azure fournit un proxy inverse de tooenable option lors de la création d’un nouveau cluster Service Fabric.
Sous **cluster créer Service Fabric**, étape 2 : Configuration du Cluster, configuration du type de nœud, cochez les cases hello trop « Activer le proxy inverse ».
Pour la configuration de proxy inverse sécurisé, le certificat SSL peut être spécifié à l’étape 3 : sécurité, configurer les paramètres de sécurité de cluster, la case à cocher Sélectionner hello trop « Incluent un certificat SSL pour le proxy inverse » et entrez les détails du certificat hello.

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a>Activer le proxy inverse via les modèles Azure Resource Manager

Vous pouvez utiliser hello [modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable hello inverse serveur proxy dans l’infrastructure de Service de cluster de hello.

Consultez trop[configurer le Proxy inverse HTTPS dans un cluster sécurisé](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) pour le Gestionnaire de ressources Azure tooconfigure un proxy inverse sécurisé avec une substitution de certificat de certificat et la gestion des exemples de modèle.

Vous obtenez tout d’abord, le modèle de hello pour le cluster de hello que vous souhaitez toodeploy. Vous pouvez utiliser des modèles d’exemple hello ou créer un modèle de gestionnaire de ressources personnalisé. Ensuite, vous pouvez activer le proxy inverse de hello à l’aide de hello comme suit :

1. Définir un port de proxy inverse de hello Bonjour [section paramètres](../azure-resource-manager/resource-group-authoring-templates.md) du modèle de hello.

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. Spécifiez le port de hello pour chacun des objets de type hello Bonjour **Cluster** [section de ressources de type](../azure-resource-manager/resource-group-authoring-templates.md).

    port de Hello est identifié par le nom du paramètre hello, reverseProxyEndpointPort.

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. tooaddress hello proxy inverse à partir de l’extérieur hello cluster Azure, configurez des règles d’équilibrage de charge Azure hello pour le port hello que vous avez spécifié à l’étape 1.

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. tooconfigure les certificats SSL sur le port proxy inverse de hello, hello ajouter hello certificat toohello ***reverseProxyCertificate*** propriété Bonjour **Cluster** [section de ressources de type](../resource-group-authoring-templates.md).

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a>Prise en charge d’un certificat de proxy inverse est différent du certificat de cluster hello
 Si le certificat de proxy inverse hello est différente de certificat hello qui sécurise le cluster de hello, puis hello précédemment spécifié certificat doit être installé sur l’ordinateur virtuel de hello et ajouté toohello liste de contrôle d’accès (ACL) afin que le Service Fabric peut y accéder. Cela est possible dans hello **virtualMachineScaleSets** [section de ressources de type](../resource-group-authoring-templates.md). Pour l’installation, ajoutez ce osProfile toohello de certificat. section d’extension Hello du modèle de hello peut mettre à jour les certificats hello Bonjour ACL.

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> Lorsque vous utilisez des certificats qui sont différentes de hello cluster certificat tooenable hello proxy inverse sur un cluster existant, installez le certificat de proxy inverse hello et mettre à jour de hello ACL sur le cluster de hello avant d’activer le proxy inverse de hello. Hello complète [modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) déploiement à l’aide de paramètres hello mentionnés précédemment avant de commencer un proxy inverse de déploiement tooenable hello dans les étapes 1 à 4.

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir un exemple de communication HTTP entre services, consultez cet [exemple de projet sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Transfert de service de toosecure HTTP avec le proxy inverse hello](service-fabric-reverseproxy-configure-secure-communication.md)
* [Appels de procédure distante avec Reliable Services à distance](service-fabric-reliable-services-communication-remoting.md)
* [API Web qui utilise OWIN dans Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Communication WCF à l’aide de Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* Pour les options de configuration supplémentaires du proxy inverse, reportez-vous à la section ApplicationGateway/Http dans [Personnaliser les paramètres de cluster Service Fabric](service-fabric-cluster-fabric-settings.md).

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
