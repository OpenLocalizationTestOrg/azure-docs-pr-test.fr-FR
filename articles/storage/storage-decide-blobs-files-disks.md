---
title: "aaaDeciding lorsque les objets BLOB de Azure toouse, des fichiers de Azure ou des disques de données Azure"
description: "En savoir plus sur hello différentes façons toostore et accéder aux données dans Azure toohelp que vous décidez quels toouse technologie."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: robinsh
ms.openlocfilehash: 6109affe41e98ed459616a4f91064ded0c74428d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deciding-when-toouse-azure-blobs-azure-files-or-azure-data-disks"></a>Déterminer à quel moment les objets BLOB de Azure toouse, des fichiers de Azure ou des disques de données Azure

Microsoft Azure fournit plusieurs fonctionnalités dans le stockage Azure pour stocker et accéder à vos données dans le cloud de hello. Cet article traite des fichiers Azure, les objets BLOB et les disques de données et est conçu toohelp vous choisissez entre ces fonctionnalités.

## <a name="scenarios"></a>Scénarios

Bonjour tableau suivant compare les fichiers, les objets BLOB et les disques de données et présente des exemples de scénarios appropriés pour chacun.

| Fonctionnalité | Description | Lorsque toouse |
|--------------|-------------|-------------|
| **Azure Files** | Fournit une interface SMB, les bibliothèques clientes et un [interface REST](/rest/api/storageservices/file-service-rest-api) qui autorise l’accès à partir de n’importe quel emplacement les fichiers toostored. | Vous souhaitez trop « de courbes d’élévation et MAJ » un nuage de toohello d’application qui utilise déjà hello natif API tooshare données entre elle et d’autres applications s’exécutant dans Azure.<br/><br/>Vous souhaitez toostore développement et outils de débogage qui doivent toobe accessible à partir de nombreux ordinateurs virtuels. |
| **Objets blob Azure** | Fournit des bibliothèques clientes et un [interface REST](/rest/api/storageservices/blob-service-rest-api) qui permet à des données non structurées trop être stockées et accessibles à une grande échelle dans les objets BLOB de blocs. | Vous souhaitez que votre diffusion en continu de toosupport application et les scénarios d’accès aléatoire.<br/><br/>Vous souhaitez toobe en mesure de tooaccess des données d’application à partir de n’importe quel endroit. |
| **Disques de données Azure** | Fournit des bibliothèques clientes et un [interface REST](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) qui permet de données toobe persistante stockées et accessibles à partir d’un disque dur virtuel attaché. | Vous souhaitez toolift et déplacer les applications qui utilisent des tooread d’API de système de fichiers natif et écrire des disques de données toopersistent.<br/><br/>Vous souhaitez que les données toostore qui ne sont pas requis toobe accessible à partir du disque de hello toowhich hello extérieur ordinateur virtuel sont attachées. |

## <a name="comparison-files-and-blobs"></a>Comparaison : fichiers et objets blob

Hello tableau suivant compare les fichiers Azure aux objets BLOB Azure.  
  
||||  
|-|-|-|  
|**Attribut**|**Objets blob Azure**|**Azure Files**|  
|Options de durabilité|LRS, ZRS, GRS (et RA-GRS pour une disponibilité supérieure)|LRS, GRS|  
|Accessibilité|API REST|API REST<br /><br /> SMB 2.1 et SMB 3.0 (API du système de fichiers standard)|  
|Connectivité|API REST : monde entier|API REST : monde entier<br /><br /> SMB 2.1 : région<br /><br /> SMB 3.0 : monde entier|  
|Endpoints|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|Répertoires|Espace de noms plat|Vrais objets d’annuaire|  
|Sensibilité des noms à la casse|Respect de la casse|Non sensible à la casse, mais la casse est conservée|  
|Capacity|Les conteneurs de to too500|Partages de fichiers de 5 To|  
|Throughput|Des too60 Mo/s par objet blob de blocs|Des too60 Mo/s par partage|  
|Taille de l’objet|Les objets blob de too200 Go/bloc|Too1TB/fichier|  
|Capacité facturée|En fonction des octets écrits|En fonction de la taille de fichier|  
|Bibliothèques clientes|Plusieurs langages|Plusieurs langages|  
  
## <a name="comparison-files-and-data-disks"></a>Comparaison : fichiers et disques de données

Les fichiers Azure complètent les disques de données Azure. Un disque de données ne peut être attaché tooone Machine virtuelle Azure à une heure. Disques de données sont des disques durs virtuels de format fixe stockés en tant qu’objets BLOB de pages dans le stockage Azure et sont utilisés par les données durables de toostore de machine virtuelle hello. Partages de fichiers dans des fichiers Azure sont accessibles dans hello même façon que le disque local de hello est accessible (en utilisant les API du système de fichiers natif) et peut être partagé entre plusieurs machines virtuelles.  
 
Hello tableau suivant compare les fichiers Azure aux disques de données Azure.  
 
||||  
|-|-|-|  
|**Attribut**|**Disques de données Azure**|**Azure Files**|  
|Scope|Machine virtuelle unique de tooa exclusif|Accès partagé entre plusieurs machines virtuelles|  
|Captures instantanées et copie|Oui|Non|  
|Configuration|Connecté au démarrage de l’ordinateur virtuel de hello|Connecté après le démarrage de l’ordinateur virtuel de hello|  
|Authentification|Intégration|Configuration avec net use|  
|Nettoyage|Automatique|Manuel|  
|Accès à l’aide de REST|Fichiers hello disque dur virtuel ne sont pas accessibles|Les fichiers stockés dans un partage sont accessibles|  
|Taille maximale|Disque de 1 To|Partage de fichiers de 5 To et fichier de 1 To au sein du partage|  
|E/S par seconde de 8 Ko max.|500 E/S par seconde|1 000 E/S par seconde|  
|Throughput|Des too60 Mo/s par disque|Des too60 Mo/s par partage de fichiers|  

## <a name="next-steps"></a>Étapes suivantes

Lors de décisions sur comment vos données sont stockées et accessibles, vous devez également envisager les coûts de hello impliqués. Pour plus d’informations, consultez [Tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage/).
  
Certaines fonctionnalités SMB ne sont pas applicables toohello cloud. Pour plus d’informations, consultez [fonctionnalités non prises en charge par hello Azure File service](/rest/api/storageservices/features-not-supported-by-the-azure-file-service).
  
Pour plus d’informations sur les disques de données, consultez [gestion des disques et images](storage-about-disks-and-vhds-linux.md) et [comment tooAttach un tooa de disque de données Machine virtuelle Windows](../virtual-machines/windows/classic/attach-disk.md).
