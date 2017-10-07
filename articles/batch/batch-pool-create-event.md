---
title: "AAA « événement créer un pool de traitement par lots Azure | Documents Microsoft »"
description: "Référence pour l’événement de création de pool Batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: ad31251969af553baa21e8c533d8ea95d3eeaf91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-create-event"></a>Événement de création de pool

 Cet événement est émis après la création d’un pool. le contenu du journal de hello Hello expose des informations générales sur le pool de hello. Notez que si la taille de cible de hello du pool de hello est supérieure à 0 des nœuds de calcul, un événement de début de redimensionnement de pool suit immédiatement après cet événement.

 Hello suivant montre les corps hello d’un pool de créer un événement pour un pool créé à l’aide de la propriété de CloudServiceConfiguration hello.

```
{
    "id": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "3",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoScale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

|Élément|Type|Remarques|
|-------------|----------|-----------|
|id|String|id de Hello du pool de hello.|
|displayName|String|Hello affiche le nom du pool de hello.|
|vmSize|String|taille de Hello d’ordinateurs virtuels hello dans le pool de hello. Tous les ordinateurs virtuels dans un pool sont hello même taille. <br/><br/> Pour plus d’informations sur les tailles disponibles de machines virtuelles pour les pools de Services Cloud (pools créés avec cloudServiceConfiguration), voir [Tailles de Services Cloud](http://azure.microsoft.com/documentation/articles/cloud-services-sizes-specs/). Le service Batch prend en charge toutes les tailles de machines virtuelles des Services Cloud, à l’exception de `ExtraSmall`.<br/><br/> Pour plus d’informations sur la machine virtuelle disponible tailles pour les pools à l’aide des images à partir de hello Marketplace de Machines virtuelles (pools créés avec virtualMachineConfiguration) consultez [tailles des Machines virtuelles](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-sizes/) (Linux) ou [pour des tailles Machines virtuelles](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) (Windows). Le service Batch prend en charge l’ensemble des tailles de machine virtuelle Azure, à l’exception de `STANDARD_A0` et de celles comprises dans Premium Storage (série `STANDARD_GS`, `STANDARD_DS`, et `STANDARD_DSV2`).|
|[cloudServiceConfiguration](#bk_csconf)|Type complexe|configuration du service de cloud Hello pour le pool de hello.|
|[virtualMachineConfiguration](#bk_vmconf)|Type complexe|configuration d’ordinateur virtuel Hello pour le pool de hello.|
|[networkConfiguration](#bk_netconf)|Type complexe|configuration du réseau Hello pour le pool de hello.|
|resizeTimeout|Temps|délai d’expiration de Hello pour l’allocation de pool de toohello de nœuds de calcul spécifié pour la dernière opération de redimensionnement hello sur le pool de hello.  (hello initiale de dimensionnement lors hello création du pool nombres comme un redimensionnement).|
|targetDedicated|Int32|nombre de Hello de nœuds de calcul qui sont demandées pour le pool de hello.|
|enableAutoScale|Bool|Spécifie si taille du pool hello s’ajuste automatiquement au fil du temps.|
|enableInterNodeCommunication|Bool|Spécifie si le pool de hello est configuré pour la communication directe entre les nœuds.|
|isAutoPool|Bool|Spécifie si le pool de hello a été créé via le mécanisme de pool automatique d’un travail.|
|maxTasksPerNode|Int32|nombre maximal de Hello de tâches pouvant s’exécuter simultanément sur un nœud de calcul unique dans le pool de hello.|
|vmFillType|String|Définit comment hello service Batch distribue les tâches entre les nœuds de calcul dans le pool de hello. Les valeurs valides sont Spread ou Pack.|

###  <a name="bk_csconf"></a> cloudServiceConfiguration

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|osFamily|String|Hello du système d’exploitation invité de Azure famille toobe installé sur les ordinateurs virtuels de hello dans le pool de hello.<br /><br /> Les valeurs possibles sont les suivantes :<br /><br /> **2** – 2 de famille du système d’exploitation, équivalent tooWindows Server 2008 R2 SP1.<br /><br /> **3** – système d’exploitation de famille 3, équivalente tooWindows Server 2012.<br /><br /> **4** – famille 4, équivalent tooWindows Server 2012 R2.<br /><br /> Pour plus d’informations, voir [Publications de système d’exploitation invité d’Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|
|targetOSVersion|String|Hello toobe de version du système d’exploitation invité de Azure installé sur des machines virtuelles de hello dans le pool de hello.<br /><br /> la valeur par défaut Hello est  **\***  qui spécifie la dernière version de système d’exploitation hello pour hello spécifié famille.<br /><br /> Pour les autres valeurs autorisées, voir [Publications de système d’exploitation invité d’Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|

###  <a name="bk_vmconf"></a> virtualMachineConfiguration

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|[imageReference](#bk_imgref)|Type complexe|Spécifie des informations sur la plateforme de hello ou toouse d’image Marketplace.|
|nodeAgentSKUId|String|Hello référence (SKU) de l’agent du nœud au niveau lot hello configuré sur le nœud de calcul hello.|
|[windowsConfiguration](#bk_winconf)|Type complexe|Spécifie les paramètres de système d’exploitation Windows sur l’ordinateur virtuel de hello. Cette propriété ne doit pas être spécifié si hello imageReference fait référence à une image de système d’exploitation Linux.|

###  <a name="bk_imgref"></a> imageReference

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|publisher|String|serveur de publication Hello d’image de hello.|
|offer|String|offre de Hello d’image de hello.|
|sku|String|Hello référence (SKU) de l’image de hello.|
|version|String|version de Hello d’image de hello.|

###  <a name="bk_winconf"></a> windowsConfiguration

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|enableAutomaticUpdates|Boolean|Indique si machine virtuelle de hello est activé pour les mises à jour automatiques. Si cette propriété n’est pas spécifiée, la valeur par défaut de hello est true.|

###  <a name="bk_netconf"></a> networkConfiguration

|Nom de l'élément|Type|Remarques|
|------------------|--------------|----------|
|subnetId|String|Spécifie l’identificateur de ressource de hello du sous-réseau hello dans le calcul de quel pool hello nœuds sont créés.|
