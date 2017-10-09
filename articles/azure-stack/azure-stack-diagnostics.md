---
title: aaaDiagnostics dans la pile de Azure | Documents Microsoft
description: "Fonctionnement des fichiers de journal de toocollect pour obtenir des diagnostics dans la pile d’Azure"
services: azure-stack
documentationcenter: 
author: adshar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: adshar
ms.openlocfilehash: a4a5ddf29e75df710e9fae366d6ac16e6fb36d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-diagnostics-tools"></a>Outils de diagnostics Azure Stack
 
Azure Stack est une grande collection de composants qui fonctionnent ensemble et interagissent. Tous ces composants génèrent leurs propres journaux uniques, ce qui signifie que diagnostiquer les problèmes peut rapidement devenir une tâche difficile, en particulier pour les erreurs provenant de plusieurs composants Azure Stack qui interagissent. 

Nos outils de diagnostic vous assurer mécanisme de collecte de journal hello est facile et efficace. Hello diagramme suivant affiche comment ouvrir une session outils de collecte dans le travail de la pile de Azure :

![Outils de collecte de journaux](media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a>Collecteur de traces
 
le collecteur de traces de Hello est activée par défaut. Il continue s’exécute en arrière-plan de hello et collecte tous les journaux de suivi d’événements pour Windows (ETW) à partir des services de composants sur la pile d’Azure et les stocke sur un partage local commun. 

Hello Voici tooknow points importants sur hello le collecteur de traces :
 
* le collecteur de traces de Hello s’exécute en permanence avec les limites de taille par défaut. taille maximale par défaut est autorisée pour chaque fichier (200 Mo) est de Hello **pas** une taille limite. Une vérification de la taille se produit régulièrement (actuellement toutes les 10 minutes) et si le fichier en cours de hello est > = 200 Mo, il est enregistré et un nouveau fichier est généré. Il existe également une limite de 8 Go (configurable) sur hello taille totale du fichier généré par la session d’événements. Une fois cette limite est atteinte, les fichiers les plus anciens hello sont supprimés comme de nouveaux fichiers sont créés.
* Il existe une limite d’âge de 5 jours sur les journaux de hello. Cette limite est également configurable. 
* Chaque composant définit les propriétés de configuration de trace hello via un fichier JSON. Hello JSON fichiers sont stockés dans `C:\TraceCollector\Configuration`. Si nécessaire, ces fichiers peuvent être modifiés toochange hello taille limites d’âge et de hello collecte des journaux. Modifications toothese fichiers nécessitent un redémarrage de hello *le collecteur de traces de pile de Microsoft Azure* service pour hello modifie tootake effet.
* Hello exemple suivant est un fichier de JSON de la configuration de trace pour les opérations de FabricRingServices de hello XRP VM : 

```
{
    "LogFile": 
    {
        "SessionName": "FabricRingServicesOperationsLogSession",
        "FileName": "\\\\SU1FileServer\\SU1_ManagementLibrary_1\\Diagnostics\\FabricRingServices\\Operations\\AzureStack.Common.Infrastructure.Operations.etl",
        "RollTimeStamp": "00:00:00",
        "MaxDaysOfFiles": "5",
        "MaxSizeInMB": "200",
        "TotalSizeInMB": "5120"
    },
    "EventSources":
    [
        {"Name": "Microsoft-AzureStack-Common-Infrastructure-ResourceManager" },
        {"Name": "Microsoft-OperationManager-EventSource" },
        {"Name": "Microsoft-Operation-EventSource" }
    ]
}
```

* **MaxDaysOfFiles**

    Ce paramètre contrôle âge hello de tookeep de fichiers. Les fichiers journaux plus anciens sont supprimés.
* **MaxSizeInMB**

    Ce paramètre contrôle le seuil de taille hello pour un seul fichier. Si la taille de hello est atteinte, un nouveau fichier .etl est créé.
* **TotalSizeInMB**

    Ce paramètre contrôle la taille totale de hello des fichiers .etl de hello généré à partir d’une session d’événements. Si la taille totale des fichiers de hello est supérieure à la valeur de ce paramètre, les fichiers plus anciens sont supprimés.
  
## <a name="log-collection-tool"></a>Outil de collecte de journaux
 
Hello de commande PowerShell `Get-AzureStackLog` peut être journaux toocollect utilisé à partir de tous les composants de hello dans un environnement de la pile de Azure. Elle les enregistre dans des fichiers zip à un emplacement défini par l’utilisateur. Si notre technique prennent en charge les besoins de l’équipe votre toohelp journaux résoudre un problème, ils peuvent vous demander toorun cet outil.

> [!CAUTION]
> Ces fichiers journaux peuvent contenir des informations d’identification personnelle. Pensez-y avant de publier des fichiers journaux publiquement.
 
Actuellement, nous collectons hello les types de journaux suivants :
*   **Journaux de déploiement Azure Stack**
*   **Journaux des événements Windows**
*   **Journaux Panther**

     problèmes de création de machine virtuelle tootroubleshoot.
*   **Journaux de cluster**
*   **Journaux de diagnostics de stockage**
*   **Journaux ETW**

    Celles-ci sont collectées par le collecteur de traces de hello et stockés dans un partage à partir de laquelle `Get-AzureStackLog` les récupère.
 
tooidentify tous hello journaux sont collectés à partir de tous les composants de hello, consultez toohello `<Logs>` balises dans un fichier de configuration de client hello situé à `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.
 
### <a name="toorun-get-azurestacklog"></a>toorun Get-AzureStackLog
1.  Connectez-vous en tant que AzureStack\AzureStackAdmin sur l’ordinateur hôte de hello.
2.  Ouvrez une fenêtre PowerShell en tant qu’administrateur.
3.  Exécutez `Get-AzureStackLog`.  

    **Exemples**

    - Collecter tous les journaux pour tous les rôles :

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs`

    - Collecter les journaux à partir des rôles VirtualMachines et BareMetal :

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - Collecter les journaux à partir de rôles de machines virtuelles et BareMetal, avec la date de filtrage pour les fichiers journaux pour hello dernières heures 8 :

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

Si hello `FromDate` et `ToDate` paramètres ne sont pas spécifiés, les journaux sont collectés pour hello passées de 4 heures par défaut.

Actuellement, vous pouvez utiliser hello `FilterByRole` collecte de journaux paramètre toofilter par hello suivant des rôles :

|   |   |   |
| - | - | - |
| `ACSMigrationService`     | `ACSMonitoringService`   | `ACSSettingsService` |
| `ACS`                     | `ACSFabric`              | `ACSFrontEnd`        |
| `ACSTableMaster`          | `ACSTableServer`         | `ACSWac`             |
| `ADFS`                    | `ASAppGateway`           | `BareMetal`          |
| `BRP`                     | `CA`                     | `CPI`                |
| `CRP`                     | `DeploymentMachine`      | `DHCP`               |
|`Domain`                   | `ECE`                    | `ECESeedRing`        |        
| `FabricRing`              | `FabricRingServices`     | `FRP`                |
|` Gateway`                 | `HealthMonitoring`       | `HRP`                |               
| `IBC`                     | `InfraServiceController` | `KeyVaultAdminResourceProvider`|
| `KeyVaultControlPlane`    | `KeyVaultDataPlane`      | `NC`                 |            
| `NonPrivilegedAppGateway` | `NRP`                    | `SeedRing`           |
| `SeedRingServices`        | `SLB`                    | `SQL`                |     
| `SRP`                     | `Storage`                | `StorageController`  |
| `URP`                     | `UsageBridge`            | `VirtualMachines`    |  
| `WAS`                     | `WASPUBLIC`              | `WDS`                |


Quelques éléments toonote :

* Cette commande de collecte de journaux prend un certain temps, en fonction des journaux de rôles qui sont recueillis. Facteurs incluent hello durée spécifiée pour la collecte de journaux et les nombres hello de nœuds dans un environnement de Azure pile hello.
* Une fois la collecte de journaux est terminée, vérifiez hello nouveau dossier créé dans hello `-OutputPath` paramètre spécifié dans la commande hello.
* Un fichier appelé `Get-AzureStackLog_Output.log` est créé dans le dossier hello contenant des fichiers zip hello et inclut la sortie de commande hello, qui peut être utilisé pour résoudre les erreurs dans la collection de journaux.
* Les journaux de chaque rôle se trouvent à l’intérieur d’un fichier zip individuel. 
* tooinvestigate un échec spécifique, les journaux peuvent être nécessaires à partir de plusieurs composants.
    -   Système et les journaux des événements pour tous les ordinateurs virtuels d’infrastructure sont collectés dans hello *machines virtuelles* rôle.
    -   Système et les journaux des événements pour tous les hôtes sont collectés dans hello *BareMetal* rôle.
    -   Journaux des événements de Cluster de basculement et Hyper-V sont collectés dans hello *stockage* rôle.
    -   Les journaux des services ACS sont collectés dans hello *stockage* et *ACS* rôles.
* Pour plus d’informations, vous pouvez consulter le fichier de configuration de client toohello. Examiner hello `<Logs>` des balises pour les différents rôles de hello.

> [!NOTE]
> Nous sommes en appliquant taille et âge limite toohello les journaux collectés comme il est essentiel tooensure une utilisation efficace de vos toomake d’espace de stockage que vous ne trouverez pas saturation des journaux des. Ceci dit, lorsque vous diagnostiquez un problème, que vous devez souvent les journaux n’existe peut-être plus en raison des limites de toothese appliquées. Par conséquent, il est **hautement recommandé** que vous décharger de votre espace de stockage externe tooan journaux (un compte de stockage dans Azure publique, un périphérique de stockage local supplémentaires etc.) toutes les 8 heures too12 et les conserver pendant 1 à 3 mois en fonction de vos besoins.


## <a name="next-steps"></a>Étapes suivantes
[Dépannage de Microsoft Azure Stack](azure-stack-troubleshooting.md)
