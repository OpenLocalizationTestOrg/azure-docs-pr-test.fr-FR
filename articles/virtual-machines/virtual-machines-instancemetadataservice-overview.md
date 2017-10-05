---
title: "Vue d’ensemble du service de métadonnées Instance Azure | Microsoft Docs"
description: "Interface RESTful permettant d’obtenir des informations sur le calcul, le réseau et les événements de maintenance à venir de la machine virtuelle."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: d601d8fdb92bf2d3253ba99cdeee10e09591689c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-instance-metadata-service"></a>Service de métadonnées d’instance Azure 


Le service de métadonnées d’instance Azure fournit des informations sur les instances de machine virtuelle en cours d’exécution qui peuvent être utilisées pour gérer et configurer vos machines virtuelles.
Cela inclut des informations telles que la référence (SKU), la configuration réseau et les événements de maintenance à venir. Pour plus de détails sur le type des informations disponibles, voir [Catégories de métadonnées](#instance-metadata-data-categories).

Le service de métadonnées d’instance d’Azure est un point de terminaison REST accessible à toutes les machines virtuelles IaaS créées via [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Le point de terminaison est disponible à une adresse IP non routable bien connue (`169.254.169.254`) accessible uniquement à partir de la machine virtuelle.

### <a name="important-information"></a>Informations importantes

Ce service est **généralement disponible** dans les régions Azure globales. Il est en disponible en préversion publique pour le secteur public, la Chine et le cloud Azure allemand. Il reçoit régulièrement des mises à jour pour exposer de nouvelles informations sur les instances de machine virtuelle. Cette page ne reflète les [catégories de données](#instance-metadata-data-categories) à jour disponibles.

## <a name="service-availability"></a>Disponibilité des services
Le service est disponible dans toutes les régions Azure globales disponibles. Il est en disponible en préversion publique dans les régions Secteur public, Chine et Allemagne.

Régions                                        | Disponibilité ?
-----------------------------------------------|-----------------------------------------------
[Toutes les régions Azure globales généralement disponibles](https://azure.microsoft.com/en-us/regions/)     | Mise à la disposition générale 
[Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)              | En préversion 
[Azure Chine](https://www.azure.cn/)                                                           | En préversion
[Azure Allemagne](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | En préversion

Ce tableau est mis à jour lorsque le service devient disponible dans d’autres clouds Azure.

Pour tester le service de métadonnées d’instance, créez une machine virtuelle à partir d’[Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) ou du [portail Azure](http://portal.azure.com) dans les régions ci-dessus, puis suivez les exemples ci-dessous.

## <a name="usage"></a>Usage

### <a name="versioning"></a>Contrôle de version
Le service de métadonnées Instance fait l’objet d’une gestion de version. Les versions sont obligatoires et la version actuelle est `2017-04-02`.

> [!NOTE] 
> Les préversions précédentes des événements planifiés prenaient en charge {dernière version} en tant que version de l’api. Ce format n’est plus pris en charge et sera déconseillé à l’avenir.

Au fur et à mesure que nous ajoutons des versions plus récentes, les versions antérieures sont toujours accessibles pour des questions de compatibilité si vos scripts ont des dépendances sur des formats de données spécifiques. Notez cependant que la préversion actuelle (2017-03-01) ne sera peut-être pas disponible lors de la mise à la disposition générale du service.

### <a name="using-headers"></a>Utilisation d'en-têtes
Quand vous interrogez le service de métadonnées d’instance, vous devez fournir l’en-tête `Metadata: true` pour garantir que la demande n’a pas été redirigée involontairement.

### <a name="retrieving-metadata"></a>Récupération des métadonnées

Les métadonnées Instance sont disponibles pour l’exécution de machines virtuelles créées/gérées à l’aide [d’Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Accédez à toutes les catégories de données pour une instance de machine virtuelle à l’aide de la demande suivante :

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> Toutes les requêtes de métadonnées d’instance respectent la casse.

### <a name="data-output"></a>Sortie des données
Par défaut, le service de métadonnées d’instance retourne des données au format JSON (`Content-Type: application/json`). Toutefois, différentes API peuvent retourner des données dans des formats différents si nécessaire.
Le tableau suivant répertorie les autres formats de données que les API peuvent prendre en charge.

API | Format de données par défaut | Autres formats
--------|---------------------|--------------
/instance | json | texte
/scheduledevents | json | Aucun

Pour accéder à un format de réponse autre que le format par défaut, spécifiez le format demandé en tant que paramètre de chaîne de requête dans la demande. Par exemple :

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>Sécurité
Le point de terminaison du service de métadonnées d’instance est accessible uniquement à partir de l’instance de machine virtuelle active sur une adresse IP non routable. En outre, toute demande contenant un en-tête `X-Forwarded-For` est rejetée par le service.
Nous exigeons également que toute demande contienne un en-tête `Metadata: true` garantissant que la demande est réellement intentionnelle et ne fait pas partie d’une redirection involontaire. 

### <a name="error"></a>Error
S’il existe un élément de données introuvable ou une requête mal formée, le service de métadonnées d’instance retourne des erreurs HTTP standard. Par exemple :

Code d’état HTTP | Motif
----------------|-------
200 OK |
400 Demande incorrecte | En-tête `Metadata: true` manquant
404 Introuvable | L’élément demandé n’existe pas 
405 Méthode non autorisée | Seules les demandes `GET` et `POST` sont prises en charge
429 Trop de demandes | L’API prend actuellement en charge un maximum de 5 requêtes par seconde
500 Erreur de service     | Recommencez l’opération plus tard

### <a name="examples"></a>Exemples

> [!NOTE] 
> Toutes les réponses de l’API sont des chaînes JSON. Tous les exemples de réponses suivants sont imprimés avec soin par souci de lisibilité.

#### <a name="retrieving-network-information"></a>Récupération des informations réseau

**Requête**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**Réponse**

> [!NOTE] 
> La réponse est une chaîne JSON. L’exemple de réponse suivant est imprimé avec soin par souci de lisibilité.

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>Récupération de l’adresse IP publique

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>Récupération de toutes les métadonnées d’une instance

**Requête**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**Réponse**

> [!NOTE] 
> La réponse est une chaîne JSON. L’exemple de réponse suivant est imprimé avec soin par souci de lisibilité.

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>Récupération de métadonnées dans une machine virtuelle Windows

**Requête**

Les métadonnées d’instance peuvent être récupérées dans Windows via l’utilitaire Powershell `curl` : 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

Ou via l’applet de commande `Invoke-RestMethod` :
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**Réponse**

> [!NOTE] 
> La réponse est une chaîne JSON. L’exemple de réponse suivant est imprimé avec soin par souci de lisibilité.

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>Catégories de données de métadonnées Instance
Les catégories de données suivantes sont disponibles via le service de métadonnées d’instance :

Données | Description
-----|------------
location | Région Azure dans laquelle la machine virtuelle est en cours d’exécution
name | Nom de la machine virtuelle 
offer | Offrent des informations pour l’image de machine virtuelle. Cette valeur est uniquement présente pour les images déployées à partir de la galerie d’images Azure.
publisher | Éditeur de l’image de machine virtuelle
sku | Référence (SKU) spécifique pour l’image de machine virtuelle  
version | Version de l’image de machine virtuelle 
osType | Linux ou Windows 
platformUpdateDomain |  [Domaine de mise à jour](virtual-machines-windows-manage-availability.md) dans lequel la machine virtuelle est en cours d’exécution
platformFaultDomain | [Domaine par défaut](virtual-machines-windows-manage-availability.md) dans lequel la machine virtuelle est en cours d’exécution
vmId | [Identificateur unique](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) de la machine virtuelle
vmSize | [Taille de la machine virtuelle](virtual-machines-windows-sizes.md)
ipv4/privateIpAddress | Adresse IPv4 locale de la machine virtuelle 
ipv4/publicIpAddress | Adresse IPv4 publique de la machine virtuelle
subnet/address | Adresse de sous-réseau de la machine virtuelle
subnet/prefix | Préfixe de sous-réseau, par exemple 24
ipv6/ipAddress | Adresse IPv6 locale de la machine virtuelle
macAddress | Adresse MAC de la machine virtuelle 
scheduledevents | Actuellement en préversion publique. Voir [scheduledevents](virtual-machines-scheduled-events.md)

## <a name="example-scenarios-for-usage"></a>Exemples de scénarios d’utilisation  

### <a name="tracking-vm-running-on-azure"></a>Suivi de la machine virtuelle s’exécutant sur Azure

En tant que fournisseur de service, vous aurez peut-être besoin de suivre le nombre de machines virtuelles s’exécutant sur votre logiciel ou de disposer d’agents effectuant le suivi de l’unicité de la machine virtuelle. Pour pouvoir obtenir un ID unique pour une machine virtuelle, utilisez le champ `vmId` du service de métadonnées d’instance.

**Requête**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**Réponse**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>Positionnement des conteneurs, partitions de données en fonction du domaine par défaut/de mise à jour 

Pour certains scénarios, le positionnement des différents réplicas de données est de première importance. Par exemple, pour le [positionnement du réplica HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) ou pour le positionnement des conteneurs via un [orchestrateur](https://kubernetes.io/docs/user-guide/node-selection/), vous devez connaître les domaines `platformFaultDomain` et `platformUpdateDomain` sur lesquels la machine virtuelle s’exécute.
Vous pouvez interroger ces données directement via le service de métadonnées d’instance.

**Requête**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**Réponse**

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a>Obtenir plus d’informations sur la machine virtuelle pour le dossier de support 

En tant que fournisseur de services, vous recevrez peut-être un appel du support pour lequel vous devrez connaître les informations de la machine virtuelle. Demandez au client de partager les métadonnées de calcul afin que l’équipe du support dispose des informations de base concernant le type de machine virtuelle sur Azure. 

**Requête**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**Réponse**

> [!NOTE] 
> La réponse est une chaîne JSON. L’exemple de réponse suivant est imprimé avec soin par souci de lisibilité.

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a>Exemples d’appels du service de métadonnées utilisant différents langages à l’intérieur de la machine virtuelle 

Langage | Exemple 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb
Go Lan   | https://github.com/Microsoft/azureimds/blob/master/imdssample.go            
python   | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py
C++      | https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp
C#       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs
JavaScript | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js
PowerShell | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh
    

## <a name="faq"></a>Forum Aux Questions
1. J’obtiens l’erreur `400 Bad Request, Required metadata header not specified`. Qu’est-ce que cela signifie ?
   * Le service de métadonnées d’instance requiert que l’en-tête `Metadata: true` soit transmis dans cette demande. La transmission de cet en-tête dans l’appel REST permet d’accéder au service de métadonnées d’instance. 
2. Pourquoi je n’obtiens pas les informations de calcul pour ma machine virtuelle ?
   * Actuellement, le service de métadonnées d’instance prend uniquement en charge les instances créées avec Azure Resource Manager. À l’avenir, il se peut que nous ajoutions la prise en charge de machines virtuelles du service cloud.
3. J’ai créé une machine virtuelle via Azure Resource Manager il y quelque temps déjà. Pourquoi ne puis-je pas voir les informations de métadonnées de calcul ?
   * Pour les machines virtuelles créées après septembre 2016, ajoutez une [balise](../azure-resource-manager/resource-group-using-tags.md) pour commencer à voir les métadonnées de calcul. Pour une machine virtuelle plus ancienne (créée avant septembre 2016), ajoutez/supprimez des extensions ou des disques de données à la machine virtuelle pour actualiser les métadonnées.
4. Pourquoi l’erreur `500 Internal Server Error` ?
   * Renouvelez votre demande en fonction du système d’interruption exponentiel. Si le problème persiste, contactez le support Azure.
5. Où partager des commentaires/questions supplémentaires ?
   * Envoyez vos commentaires au site http://feedback.azure.com.
7. Cela fonctionne-t-il pour l’instance de groupe de machines virtuelles identiques ?
   * Oui, le service de métadonnées est disponible pour les instances de groupe identique. 
6. Comment obtenir un support technique pour le service ?
   * Pour obtenir un support technique pour le service, créez un problème de support dans le portail Azure pour la machine virtuelle sur laquelle vous ne pouvez pas obtenir de réponse de métadonnées après plusieurs tentatives longues. 

   ![Support des métadonnées d’instance](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur l’API [scheduledevents](virtual-machines-scheduled-events.md) en **préversion publique** fournie par le service de métadonnées d’instance.
