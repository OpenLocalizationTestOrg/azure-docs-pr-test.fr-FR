---
title: "toodo aaaWhat dans les cas de hello d’une interruption de service Azure qui affecte le coffre de clés Azure | Documents Microsoft"
description: "Découvrez quels toodo dans les cas de hello d’une interruption de service Azure qui affecte le coffre de clés Azure."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a>Disponibilité et redondance d’Azure Key Vault
Coffre de clés Azure propose plusieurs couches de toomake redondance sûr que vos clés et les clés secrètes restent disponibles tooyour application hello des composants de service échouent.

Hello contenu de votre coffre de clés est répliquées dans la région de hello et la région secondaire tooa au moins 150 miles immédiatement, mais dans hello même geography. Cela maintient une durabilité élevée de vos clés et secrets. Consultez hello [Azure associés régions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document pour plus d’informations sur les paires de région spécifique.

Si des composants individuels dans le service de coffre de clés hello échouent, des composants de substitution dans une région de hello étape tooserve votre toomake demande qu’il n’existe aucune dégradation des fonctionnalités. Vous n’avez pas besoin tootake tout tootrigger action cela. Il se produit automatiquement et sera tooyou transparent.

Dans l’événement rare de hello qu’un ensemble de la région Azure n’est pas disponible, hello que vous apportez d’Azure Key Vault dans cette région sont automatiquement routées (*basculé*) tooa la région secondaire. Lors de la région principale de hello est à nouveau disponible, les demandes sont routées précédent (*échec précédent*) toohello la région principale. Là encore, il est inutile tootake n’importe quelle action, car cela se produit automatiquement.

Il existe quelques avertissements toobe prenant en charge de :

* Dans l’événement hello d’un basculement de la région, il peut prendre quelques minutes pour hello service toofail. Les demandes qui sont effectuées pendant ce temps risque d’échouer jusqu'à ce que le basculement de hello est terminé.
* Après basculement, votre Key Vault est en lecture seule. Les demandes prises en charge dans ce mode sont les suivantes :
  * List key vaults (Afficher la liste des Key Vaults)
  * Get properties of key vaults (Obtenir les propriétés des Key Vaults)
  * List secrets (Afficher la liste des secrets)
  * Get secrets (Obtenir les secrets)
  * List keys (Afficher la liste des clés)
  * Get (properties of) keys (Obtenir les propriétés des clés)
  * Encrypt (Chiffrer)
  * Decrypt (Déchiffrer)
  * Wrap (Encapsuler)
  * Unwrap (Désencapsuler)
  * Verify (Vérifier)
  * Sign (Signer)
  * Backup (Sauvegarder)
* Une fois le basculement restauré, tous les types de demandes (y compris de lecture -read- *et* d’écriture write-) sont disponibles.

