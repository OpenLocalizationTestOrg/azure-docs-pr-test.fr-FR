---
title: aaaIntroduction tooAzure stockage de la pile
description: En savoir plus sur le stockage Azure Stack
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 092aba28-04bc-44c0-90e1-e79d82f4ff42
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/19/2017
ms.author: xiaofmao
ms.openlocfilehash: 8e156584dafb8b084bfc69b9dbe7cbaa78717135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-stack-storage"></a>Introduction tooAzure stockage de la pile

## <a name="overview"></a>Vue d'ensemble
Le stockage Azure Stack est un ensemble de services de stockage cloud, y compris des objets blob, des tables et des files d’attente, qui sont compatibles avec les services de stockage Azure.

## <a name="azure-stack-storage-services"></a>Services de stockage Azure Stack
Le stockage Azure pile fournit hello suivant trois services :

* **Stockage d’objets blob** 

    Le stockage Blob stocke les données d’objets non structurées. Un objet blob peut correspondre à n'importe quel type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d'installation d'application.
* **Stockage de table** 

    Le stockage de tables stocke les jeux de données structurés. Stockage de table est un magasin de données d’attribut de clé NoSQL, qui permet un développement rapide et quantités de toolarge un accès rapide des données.
* **Stockage de files d’attente** 

    Le stockage de files d’attente fournit une messagerie fiable pour le traitement du workflow et pour la communication entre les composants des services cloud.

Un compte de stockage Azure pile est un compte sécurisé qui vous donne accès tooservices dans le stockage Azure pile. Votre compte de stockage fournit l’espace de noms unique hello pour vos ressources de stockage. Hello diagramme suivant montre les relations entre hello hello des ressources de stockage Azure pile dans un compte de stockage :

![Vue d’ensemble du stockage Azure Stack](media/azure-stack-storage-overview/AzureStackStorageOverview.png)


### <a name="blob-storage"></a>Stockage d'objets blob

Pour les utilisateurs avec une grande quantité de toostore de données d’objet non structurées dans le cloud de hello, stockage d’objets Blob offre une solution efficace et évolutive. Vous pouvez utiliser le contenu toostore stockage Blob tels que :

* Documents
* Données sociales telles que photos, vidéos, musique et blogs
* Sauvegardes de fichiers, d'ordinateurs, de bases de données et d'appareils
* Images et textes pour applications Web
* Données de configuration pour applications cloud
* Big Data tels que journaux et autres jeux de données volumineux

Chaque objet blob est organisé dans un conteneur. Les conteneurs fournissent également un toogroups de stratégies de sécurité de tooassign moyen utile d’objets. Un compte de stockage peut contenir n’importe quel nombre de conteneurs, et un conteneur peut contenir n’importe quel nombre d’objets BLOB, de la limite de toohello du compte de stockage.

Le stockage Blob offre trois types d’objets blob : 
* **Objets blob de blocs** 

    Les objets blob de bloc sont optimisés pour la diffusion en continu et le stockage d’objets cloud. Ils constituent une solution de choix pour stocker des documents, des fichiers multimédias, des sauvegardes, etc.
* **Objets blob d’ajout** 

    Ajouter des objets BLOB sont des objets BLOB de tooblock similaire, mais sont optimisés pour les opérations d’ajout. Un objet blob d’ajout peut être mis à jour qu’en ajoutant une nouvelle fin toohello de bloc. Ajouter les objets BLOB sont un bon choix pour les scénarios tels que la journalisation, où les nouvelles données doivent toobe écrit uniquement toohello fin de l’objet blob de hello.
* **Objets blob de pages** 

    Objets BLOB de pages est optimisées pour la représentation des disques de IaaS et aléatoire de prise en charge d’écritures jusqu'à to too1 taille. Un disque IaaS attaché à une machine virtuelle Azure Stack est un disque dur virtuel stocké comme un objet blob de pages.


### <a name="table-storage"></a>Stockage de tables
Les applications modernes exigent souvent des magasins de données avec plus d'évolutivité et de souplesse que ne l'exigeaient les précédentes générations de logiciels. Stockage de table offre un stockage hautement disponible et très évolutif, afin que votre application peut automatiquement mettre à l’échelle à la demande de toomeet utilisateur. Le Stockage Table est le magasin de clés/attributs NoSQL de Microsoft ; il a une conception sans schéma, ce en quoi il diffère des bases de données relationnelles classiques. Avec un magasin de données schemaless, il est facile tooadapt d’evolve de votre application a besoin de vos données en tant que hello. Stockage de table étant toouse simple, les développeurs peuvent créer rapidement des applications.

Le stockage de tables est un magasin de clés/attributs : cela signifie que chaque valeur dans une table est stockée avec un nom de propriété typé. nom de la propriété Hello peut être utilisé pour le filtrage et la spécification des critères de sélection. Une collection de propriétés et leurs valeurs constituent une entité. Étant donné que le stockage de Table est schemaless, deux entités dans hello même table peut contenir différents ensembles de propriétés, et ces propriétés peuvent être de types différents.

Vous pouvez utiliser la Table stockage toostore flexible jeux de données, telles que les données utilisateur pour les applications web, carnets d’adresses, les informations de périphérique et tout autre type de métadonnées nécessaires à votre service. Pour les applications d’aujourd'hui basés sur Internet, tels que le stockage de Table, les bases de données NoSQL offrent un tootraditional autre populaires bases de données relationnelles.

Un compte de stockage peut contenir n’importe quel nombre de tables, et une table peut contenir n’importe quel nombre d’entités, des limites de capacité toohello hello du compte de stockage.

### <a name="queue-storage"></a>Stockage de files d'attente
Lors de la conception d'applications pour la mise à l'échelle, des composants d'application sont souvent découplés, de sorte qu'ils peuvent être mis à l'échelle indépendamment. Stockage de file d’attente fournit une solution de messagerie fiable pour la communication asynchrone entre les composants d’application, qu’elles s’exécutent dans le cloud hello, sur le bureau de hello, sur un serveur local ou sur un appareil mobile. Le Stockage File d'attente prend également en charge la gestion des tâches asynchrones et la création des workflows de processus.

Un compte de stockage peut contenir n’importe quel nombre de files d’attente et une file d’attente peut contenir n’importe quel nombre de messages, des limites de capacité toohello hello du compte de stockage. Les messages individuels peuvent être des too64 Ko.

## <a name="next-steps"></a>Étapes suivantes
* [Stockage Azure : Différences et considérations](azure-stack-acs-differences.md)

* toolearn en savoir plus sur le stockage Azure, consultez [Introduction tooMicrosoft stockage Azure](../storage/common/storage-introduction.md)

