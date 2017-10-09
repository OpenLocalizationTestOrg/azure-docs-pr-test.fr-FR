---
title: "Stockage Azure Stack : différences et points à prendre en compte"
description: "Comprendre les différences de hello entre Azure pile de stockage et le stockage Azure, ainsi que des considérations relatives au déploiement de pile de Azure."
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/22/2017
ms.author: xiaofmao
ms.openlocfilehash: a1f8e2180b046b835c89fd658e2dbaff004b8786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-storage-differences-and-considerations"></a>Stockage Azure Stack : différences et points à prendre en compte
Stockage Azure de pile est ensemble hello des services de cloud de stockage dans la pile de Microsoft Azure. Le stockage Azure Stack fournit des fonctionnalités de gestion des objets blob, des tables, des files d’attente et des comptes avec une sémantique Azure cohérente.

Cet article résume les hello connu des différences de pile le stockage Azure à partir du stockage Azure. Il récapitule également les autres tookeep considérations à l’esprit lorsque vous déployez Azure pile. toolearn sur les principales différences entre la pile d’Azure et d’Azure, consultez hello [considérations relatives à la clé](azure-stack-considerations.md) rubrique.

## <a name="cheat-sheet-storage-differences"></a>Aide-mémoire : différences entre les stockages

| Fonctionnalité | Azure (global) | Azure Stack |
| --- | --- | --- |
|Stockage Fichier|Partages de fichiers SMB sur le cloud pris en charge|Pas encore pris en charge
|Chiffrement des données au repos|Chiffrement AES 256 bits|Pas encore pris en charge
|Type de compte de stockage|Comptes de stockage à usage général et comptes de stockage d’objets blob Azure|À usage général uniquement
|Options de réplication|Stockage localement redondant, stockage géoredondant, stockage géoredondant avec accès en lecture et stockage redondant dans une zone|Stockage localement redondant
|Stockage Premium|Entièrement pris en charge|Peut être approvisionné, mais sans limite ni garantie de performances
|Disques gérés|Premium et standard pris en charge|Pas encore pris en charge
|Nom de l’objet blob|1 024 caractères (2 048 octets)|880 caractères (1 760 octets)
|Taille maximale d’un objet blob de blocs|4,75 To (100 Mo X 50 000 blocs)|50 000 X 4 Mo (195 Go environ)
|Copie d’instantané incrémentiel d’objet blob de pages|Objets blob de pages Azure Premium et standard pris en charge|Pas encore pris en charge
|Taille maximale d’un objet blob de pages|8 To|1 To
|Taille de page d’un objet blob de pages|512 octets|4 Ko
|Taille de la clé de ligne et de la clé de partition de table|1 024 caractères (2 048 octets)|400 caractères (800 octets)

### <a name="metrics"></a>Mesures
Il existe également des différences sur le plan des métriques de stockage :
* les données de transaction Hello dans des indicateurs de stockage ne fait aucune distinguent la bande passante du réseau interne ou externe.
* les données de transaction Hello dans les mesures de stockage n’incluent pas de disques de machine virtuelle accès toohello monté.

## <a name="api-version"></a>Version de l'API
Hello versions suivantes est prises en charge avec le stockage de pile Azure :

* Services de données du stockage Azure : [version du 05-04-2015 de l’API REST](https://docs.microsoft.com/en-us/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)
* Services de gestion du stockage Azure : [préversion du 01-05-2015, version du 15-06-2015 et version du 01-01-2016](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN) 

## <a name="next-steps"></a>Étapes suivantes

* [Bien démarrer avec les outils de développement du stockage Azure Stack](azure-stack-storage-dev.md)
* [Introduction tooAzure pile de stockage](azure-stack-storage-overview.md)

