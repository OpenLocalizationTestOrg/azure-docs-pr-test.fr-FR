---
title: "aaaAzure Service de métadonnées de l’Instance pour les machines virtuelles Linux | Documents Microsoft"
description: "Interface rESTful tooget informations de Linux VM calcul, réseau et les événements de maintenance à venir."
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: 138822addea322c6e565b39a1b2002d7305f5fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a>Service de métadonnées d’instances Azure pour machines virtuelles Linux


Hello Service de métadonnées de l’Instance Azure fournit des informations sur les instances de machine virtuelle qui peuvent être utilisé toomanage et configurer vos ordinateurs virtuels en cours d’exécution.
Cela inclut des informations telles que la référence (SKU), la configuration réseau et les événements de maintenance à venir. Pour plus de détails sur le type des informations disponibles, voir [Catégories de métadonnées](#instance-metadata-data-categories).

Service de métadonnées de l’Instance d’Azure est un point de terminaison REST accessible tooall machines virtuelles IaaS créé via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). point de terminaison Hello est disponible sur une adresse IP non routable connue (`169.254.169.254`) qui sont accessibles uniquement à partir de hello machine virtuelle.

> [!IMPORTANT]
> Ce service est **généralement disponible** dans les régions Azure globales. Il est en disponible en préversion publique pour le secteur public, la Chine et le cloud Azure allemand. Elle reçoit régulièrement des mises à jour tooexpose nouvelles informations sur les instances de machine virtuelle. Cette page ne reflète hello à jour [des catégories de données](#instance-metadata-data-categories) disponibles.

## <a name="service-availability"></a>Disponibilité du service
service de Hello est disponible dans toutes les régions Azure Global disponibles. service de Hello est en version préliminaire publique dans les régions gouvernement, Chine ou Allemagne hello.

Régions                                        | Disponibilité ?
-----------------------------------------------|-----------------------------------------------
[Toutes les régions Azure globales généralement disponibles](https://azure.microsoft.com/regions/)     | Mise à la disposition générale 
[Azure Government](https://azure.microsoft.com/overview/clouds/government/)              | En préversion 
[Azure Chine](https://www.azure.cn/)                                                           | En préversion
[Azure Allemagne](https://azure.microsoft.com/overview/clouds/germany/)                    | En préversion

Cette table est mise à jour lorsque le service de hello devient disponible dans d’autres clouds Azure.

tootry out hello Service de métadonnées de l’Instance, créez une machine virtuelle à partir de [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) ou hello [portail Azure](http://portal.azure.com) Bonjour au-dessus des régions et suivez hello ci-après.

## <a name="usage"></a>Usage

### <a name="versioning"></a>Contrôle de version
Hello Service de métadonnées de l’Instance est créée. Les versions sont obligatoires et la version actuelle de hello est `2017-04-02`.

> [!NOTE] 
> Versions précédentes de l’aperçu des événements planifiés pris en charge {dernière} en tant que version d’api hello. Ce format n’est plus pris en charge et sera déconseillé dans hello futures.

Au fur et à mesure que nous ajoutons des versions plus récentes, les versions antérieures sont toujours accessibles pour des questions de compatibilité si vos scripts ont des dépendances sur des formats de données spécifiques. Toutefois, notez que version(2017-03-01) version préliminaire actuelle de hello ne soient pas disponibles une fois que le service de hello est généralement disponible.

### <a name="using-headers"></a>Utilisation d’en-têtes
Lorsque vous interrogez hello Service de métadonnées de l’Instance, vous devez fournir l’en-tête de hello `Metadata: true` demande de hello tooensure n’a pas été redirigée involontairement.

### <a name="retrieving-metadata"></a>Récupération des métadonnées

Les métadonnées Instance sont disponibles pour l’exécution de machines virtuelles créées/gérées à l’aide [d’Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Accéder à toutes les catégories de données pour une instance de machine virtuelle à l’aide de hello demande :

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> Toutes les requêtes de métadonnées d’instance respectent la casse.

### <a name="data-output"></a>Sortie des données
Par défaut, hello Service de métadonnées de l’Instance retourne des données au format JSON (`Content-Type: application/json`). Toutefois, différentes API peuvent retourner des données dans des formats différents si nécessaire.
Hello tableau suivant est une référence d’autres API peut prendre en charge les formats de données.

API | Format de données par défaut | Autres formats
--------|---------------------|--------------
/instance | json | texte
/scheduledevents | json | Aucun

tooaccess un format de réponse non-par défaut, spécifiez au format requis de hello comme un paramètre de chaîne de requête dans la demande hello. Par exemple :

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>Sécurité
point de terminaison de Service de métadonnées d’Instance Hello est accessible uniquement à partir de hello instance de machine virtuelle en cours d’exécution sur une adresse IP non routable. En outre, toute demande avec un `X-Forwarded-For` en-tête est refusé par le service de hello.
Nous avons besoin également les demandes toocontain un `Metadata: true` tooensure d’en-tête qui hello demande réelle a été directement prévu et ne fait pas partie de la redirection involontaire. 

### <a name="error"></a>Error
S’il existe un élément de données introuvable ou une requête mal formée, hello Service de métadonnées de l’Instance retourne des erreurs HTTP standards. Par exemple :

Code d’état HTTP | Motif
----------------|-------
200 OK |
400 Demande incorrecte | En-tête `Metadata: true` manquant
404 Introuvable | Hello n’utilise pas de l’élément demandé existe 
405 Méthode non autorisée | Seules les demandes `GET` et `POST` sont prises en charge
429 Trop de demandes | API de Hello prend actuellement en charge un maximum de 5 requêtes par seconde
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
> réponse de Hello est une chaîne JSON. Hello suivant l’exemple de réponse est automatiquement imprimé pour une meilleure lisibilité.

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
> réponse de Hello est une chaîne JSON. Hello suivant l’exemple de réponse est automatiquement imprimé pour une meilleure lisibilité.

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

Métadonnées de l’instance peuvent être récupérée dans Windows via hello PowerShell utilitaire `curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

Ou via hello `Invoke-RestMethod` applet de commande :
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**Réponse**

> [!NOTE] 
> réponse de Hello est une chaîne JSON. Hello suivant l’exemple de réponse est automatiquement imprimé pour une meilleure lisibilité.

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
Hello suivant des catégories de données est disponible via hello Service de métadonnées de l’Instance :

Données | Description
-----|------------
location | Hello de région Azure VM s’exécute dans
name | Nom de la machine virtuelle de hello 
offer | Fournissent des informations pour l’image de machine virtuelle hello. Cette valeur est uniquement présente pour les images déployées à partir de la galerie d’images Azure.
publisher | Serveur de publication de l’image de machine virtuelle hello
sku | Référence (SKU) spécifique pour l’image de machine virtuelle hello  
version | Version de l’image de machine virtuelle hello 
osType | Linux ou Windows 
platformUpdateDomain |  [Domaine de mise à jour](manage-availability.md) hello machine virtuelle est en cours d’exécution dans
platformFaultDomain | [Domaine d’erreur](manage-availability.md) hello machine virtuelle est en cours d’exécution dans
vmId | [Identificateur unique](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) pour hello machine virtuelle
vmSize | [Taille de la machine virtuelle](sizes.md)
ipv4/privateIpAddress | Adresse IPv4 locale de hello machine virtuelle 
ipv4/publicIpAddress | Adresse IPv4 publique de hello machine virtuelle
subnet/address | Adresse de sous-réseau de hello machine virtuelle
subnet/prefix | Préfixe de sous-réseau, par exemple 24
ipv6/ipAddress | Adresse IPv6 locale de hello machine virtuelle
macAddress | Adresse MAC de la machine virtuelle 
scheduledevents | Actuellement en préversion publique. Voir [scheduledevents](scheduled-events.md)

## <a name="example-scenarios-for-usage"></a>Exemples de scénarios d’utilisation  

### <a name="tracking-vm-running-on-azure"></a>Suivi de la machine virtuelle s’exécutant sur Azure

En tant qu’un fournisseur de services, vous pouvez avoir besoin de nombre de hello tootrack de machines virtuelles exécutant votre logiciel ou ont des agents nécessitant l’unicité de tootrack Hello machine virtuelle. toobe en mesure de tooget un ID unique pour une machine virtuelle, utilisez hello `vmId` champ à partir du Service de métadonnées de l’Instance.

**Requête**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**Réponse**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>Positionnement du domaine d’erreur/de mise à jour basé sur des conteneurs et des partitions de données 

Pour certains scénarios, le positionnement des différents réplicas de données est de première importance. Par exemple, [la sélection élective du réplica HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) ou l’emplacement du conteneur via une [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) nécessiter tooknow hello `platformFaultDomain` et `platformUpdateDomain` hello machine virtuelle est en cours d’exécution.
Vous pouvez interroger ces données directement via hello Service de métadonnées de l’Instance.

**Requête**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**Réponse**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>Obtenir plus d’informations sur hello VM au cours de la demande de support 

Fournisseur de service, vous pouvez obtenir un appel de la prise en charge dans laquelle vous voulez tooknow plus d’informations sur la machine virtuelle de hello. Demandant hello client tooshare hello calcul métadonnées peuvent fournir des informations de base pour tooknow professionnelle de hello prise en charge de type hello de machine virtuelle sur Azure. 

**Requête**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**Réponse**

> [!NOTE] 
> réponse de Hello est une chaîne JSON. Hello suivant l’exemple de réponse est automatiquement imprimé pour une meilleure lisibilité.

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>Exemples d’appel de service de métadonnées à l’aide de différentes langues à l’intérieur de hello machine virtuelle 

language | Exemple 
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
1. J’obtiens une erreur de hello `400 Bad Request, Required metadata header not specified`. Qu’est-ce que cela signifie ?
   * Service de métadonnées de l’Instance de Hello nécessite des en-tête de hello `Metadata: true` toobe passé dans la demande hello. Cet en-tête de passage dans l’appel REST hello permet toohello d’accès aux métadonnées de Service de l’Instance. 
2. Pourquoi je n’obtiens pas les informations de calcul pour ma machine virtuelle ?
   * Actuellement hello Service de métadonnées d’Instance prend uniquement en charge les instances créées avec Azure Resource Manager. Bonjour future, nous pouvons ajouter prise en charge pour les machines virtuelles du Service Cloud.
3. J’ai créé une machine virtuelle via Azure Resource Manager il y quelque temps déjà. Pourquoi ne puis-je pas voir les informations de métadonnées de calcul ?
   * Pour les ordinateurs virtuels créés après septembre 2016, ajoutez un [balise](../../azure-resource-manager/resource-group-using-tags.md) toostart voir calcul métadonnées. Pour les anciens VM (créée avant septembre 2016), ajouter/supprimer les données ou les extensions de métadonnées disques toohello VM toorefresh.
4. Pour quelle raison obtenez-vous erreur de hello `500 Internal Server Error`?
   * Renouvelez votre demande en fonction du système d’interruption exponentiel. Si le problème de hello persiste, contactez le support Azure.
5. Où partager des commentaires/questions supplémentaires ?
   * Envoyez vos commentaires au site http://feedback.azure.com.
7. Cela fonctionne-t-il pour l’instance de groupe de machines virtuelles identiques ?
   * Oui, le service de métadonnées est disponible pour les instances de groupe identique. 
6. Comment obtenir un support technique pour le service de hello ?
   * prise en charge de tooget pour le service de hello, créer un problème de prise en charge dans le portail Azure pour hello où vous n’êtes pas en mesure de tooget réponse des métadonnées après plusieurs tentatives longues de machine virtuelle 

   ![Support des métadonnées d’instance](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur hello [événements planifiés](scheduled-events.md) API **en version préliminaire publique** fournie par hello service de métadonnées de l’Instance.
