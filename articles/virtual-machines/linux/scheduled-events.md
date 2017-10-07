---
title: "aaaScheduled événements pour les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Événements planifiés à l’aide du service de métadonnées de Azure hello pour sur vos machines virtuelles de Linux."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: e153c8854725330acefd67d0ef542f6149170a7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a>Service de métadonnées Azure : Événements planifiés (préversion) pour les machines virtuelles Linux

> [!NOTE] 
> Aperçus deviennent tooyou disponible sur condition hello que vous acceptez les conditions d’utilisation de toohello. Pour plus d’informations, consultez [Conditions d’Utilisation Supplémentaires relatives aux Évaluations Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Les événements planifiés est un des sous-Services hello sous hello Azure métadonnées de Service. Ce sous-service est responsable de la mise à disposition des informations concernant les événements à venir (par exemple un redémarrage), pour que votre application puisse s’y préparer et limiter ainsi l’interruption. Il est disponible pour tous types de machines virtuelles Azure, notamment PaaS et IaaS. Les événements planifiés donne à vos tâches de prévention tooperform de temps Machine virtuelle que hello toominimize un événement. 

Le sous-service des événements planifiés est disponible pour les machines virtuelles Windows et Linux. Pour plus d’informations sur les événements planifiés sur Windows, consultez [Événements planifiés pour les machines virtuelles Windows](../windows/scheduled-events.md).

## <a name="why-scheduled-events"></a>Pourquoi choisir les événements planifiés ?

Les événements planifiés, vous pouvez suivre des étapes impact de hello toolimit de maintenance de la plateforme-intiated ou des actions effectuées par l’utilisateur sur votre service. 

Les charges de travail à plusieurs instances, qui utilisent l’état de réplication techniques toomaintain, peuvent être vulnérables toooutages se produit sur plusieurs instances. Ces pannes peuvent entraîner de tâches coûteuses (par exemple, la reconstruction des index) ou même une perte de réplica. 

Dans de nombreux autres cas, hello globale disponibilité du service peut être améliorée en effectuant une séquence d’arrêt approprié comme fin (ou annulation) les transactions en cours, en réaffectant des tâches tooother machines virtuelles dans le cluster hello (manuel de basculement), ou la suppression de hello Machine virtuelle à partir d’un pool d’équilibrage de charge réseau. 

Il existe des cas où notifiant un administrateur sur un événement à venir ou de journalisation d’un tel événement aider à améliorer la facilité de maintenance de hello des applications hébergées dans le cloud de hello.

Cas d’usage Azure Metadata Service surfaces événements planifiés suivant de hello :
-   La plateforme a lancé une maintenance (par exemple, le déploiement du système d’exploitation hôte)
-   L’utilisateur a lancé des appels (par exemple, un utilisateur redémarre ou redéploie une machine virtuelle)


## <a name="hello-basics"></a>principes de base Hello  

Service de métadonnées Azure expose des informations sur les ordinateurs virtuels à l’aide d’un point de terminaison reste accessible à partir de hello machine virtuelle en cours d’exécution. informations de Hello sont disponibles via une adresse IP non routable afin que n’est pas exposée à l’extérieur de hello machine virtuelle.

### <a name="scope"></a>Scope
Les événements planifiés sont tooall chaque bande les ordinateurs virtuels dans un service cloud ou tooall Machines virtuelles dans un ensemble de disponibilité. Par conséquent, vous devez vérifier hello `Resources` champ tooidentify d’événement hello qui machines virtuelles vont toobe concerné. 

### <a name="discovering-hello-endpoint"></a>Découverte de point de terminaison hello
Dans les cas de hello où un ordinateur virtuel est créé dans un réseau virtuel (VNet), service de métadonnées hello est disponible à partir d’une adresse IP non routable statique, `169.254.169.254`.
Si hello Machine virtuelle n’est pas créé dans un réseau virtuel, le cas par défaut de hello pour les services de cloud computing et machines virtuelles de classiques, une logique supplémentaire est toouse de point de terminaison hello toodiscover requis. Consultez Comment trop de toothis exemple toolearn[découvrir le point de terminaison hello hôte](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).

### <a name="versioning"></a>Contrôle de version 
Hello Service de métadonnées de l’Instance est créée. Les versions sont obligatoires et la version actuelle de hello est `2017-03-01`.

> [!NOTE] 
> Versions précédentes de l’aperçu des événements planifiés pris en charge {dernière} en tant que version d’api hello. Ce format n’est plus pris en charge et sera déconseillé dans hello futures.

### <a name="using-headers"></a>Utilisation d’en-têtes
Lorsque vous interrogez hello Metadata Service, vous devez fournir l’en-tête de hello `Metadata: true` demande de hello tooensure n’a pas été redirigée involontairement.

### <a name="enabling-scheduled-events"></a>Activation des événements planifiés
Hello première fois que vous faites une demande pour les événements planifiés, Azure Active implicitement la fonction hello sur votre Machine virtuelle. Par conséquent, attendez-vous à retarder la réponse de votre premier appel de haut tootwo minutes.

### <a name="user-initiated-maintenance"></a>Maintenance initiée par l’utilisateur
Maintenance des ordinateurs virtuels via hello portail Azure, API, CLI, initiée par l’utilisateur ou de PowerShell entraîne un événement planifié. Cela vous permet de logique de préparation maintenance tootest hello dans votre application et tooprepare de votre application pour une maintenance initiée par l’utilisateur.

Le redémarrage d’une machine virtuelle planifie un événement de type `Reboot`. Le redéploiement d’une machine virtuelle planifie un événement de type `Redeploy`.

> [!NOTE] 
> Actuellement, 10 opérations maximum de maintenance initiée par l’utilisateur peuvent être planifiées simultanément. Cette limite sera assouplie avant la disponibilité générale des Événements planifiés.

> [!NOTE] 
> Actuellement, la maintenance initiée par l’utilisateur qui résulte dans des Événements planifiés n’est pas configurable. La possibilité de configuration est prévue pour une version ultérieure.

## <a name="using-hello-api"></a>À l’aide des API de hello

### <a name="query-for-events"></a>Rechercher des événements
Vous pouvez rechercher les événements planifiés simplement en effectuant les hello suivant à appeler :

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

Une réponse contient un tableau d’événements planifiés. Un tableau vide signifie qu’il n’y a actuellement aucun événement planifié.
Dans le cas de hello où il existe les événements planifiés, réponse de hello contient un tableau d’événements : 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>Propriétés d’événement
|Propriété  |  Description |
| - | - |
| EventId | GUID pour cet événement. <br><br> Exemple : <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| EventType | Impact provoqué par cet événement. <br><br> Valeurs : <br><ul><li> `Freeze`: hello Machine virtuelle est planifiée toopause pendant quelques secondes. Hello du processeur est suspendue, mais il n’existe aucun impact sur la mémoire, les fichiers ouverts ou les connexions réseau. <li>`Reboot`: hello Machine virtuelle est planifiée pour le redémarrage (mémoire non persistant est perdu). <li>`Redeploy`: hello Machine virtuelle est planifiée toomove tooanother nœud (disques éphémères sont perdues). |
| ResourceType | Type de ressource affecté par cet événement. <br><br> Valeurs : <ul><li>`VirtualMachine`|
| Ressources| Liste des ressources affectées par cet événement. Cela est assurée au plus un toocontain machines [domaine de mise à jour](manage-availability.md), mais ne peut ne pas contenir toutes les machines de hello UD. <br><br> Exemple : <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| Event Status | État de cet événement. <br><br> Valeurs : <ul><li>`Scheduled`: Cet événement est planifiée toostart tard hello spécifié dans hello `NotBefore` propriété.<li>`Started` : cet événement a démarré.</ul> Ne `Completed` ou état similaire est déjà fourni ; les événements hello seront n’est plus renvoyée lors de l’événement de hello est terminée.
| NotBefore| Heure après laquelle cet événement peut démarrer. <br><br> Exemple : <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Planification d’événement
Chaque événement est planifié une quantité minimale de temps Bonjour futures basé sur le type d’événement. Cette heure est reflétée dans la propriété `NotBefore` d’un événement. 

|EventType  | Préavis minimal |
| - | - |
| Freeze| 15 minutes |
| Reboot | 15 minutes |
| Redeploy | 10 minutes |

### <a name="starting-an-event"></a>Démarrage d’un événement 

Une fois que vous avez appris d’un événement à venir et terminé votre logique pour l’arrêt approprié, vous pouvez approuver les événements en attente hello en effectuant un `POST` appeler le service de métadonnées toohello avec hello `EventId`. Cela indique tooAzure qu’il peut raccourcir la notification de minimale hello heure (si possible). 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> Accuse réception d’un événement permet de hello événement tooproceed pour tous les `Resources` dans l’événement de hello, pas seulement hello machine virtuelle qui accuse réception des événements de hello. Vous pouvez donc choisir tooelect un leader toocoordinate hello accusé de réception, ce qui peut être aussi simple que la première machine de hello Bonjour `Resources` champ.




## <a name="python-sample"></a>Exemple de code Python 

Hello exemples de requêtes suivants hello du service de métadonnées pour les événements planifiés et approuve chaque événement en attente.

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Étapes suivantes 

- En savoir plus sur les API disponibles dans hello de hello [service de métadonnées de l’Instance](instance-metadata-service.md).
- Découvrez plus d’informations sur la [maintenance planifiée pour les machines virtuelles Linux dans Azure](planned-maintenance.md).
