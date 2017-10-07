---
ms.assetid: 
title: "environnements de sécurité du coffre de clés aaaAzure | Documents Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a>Mondes de sécurité Azure Key Vault et limites géographiques

Azure Key Vault est un service mutualisé qui utilise un pool de modules de sécurité matériel (HSM) dans chaque emplacement Azure. 

Tous les modules de sécurité matériels à des emplacements Azure Bonjour même région géographique partagent hello même limite de services de chiffrement (monde de sécurité Thales). Par exemple, est des États-Unis et l’ouest des États-Unis partager Bonjour même sécurité car elles appartiennent géolocalisation toohello des États-Unis. De même, tous les emplacements Azure dans le partage de Japon hello même monde de sécurité et de tous les emplacements Azure en Australie, Inde et ainsi de suite. 

## <a name="backup-and-restore-behavior"></a>Comportement de sauvegarde et de restauration

Une sauvegarde d’une clé à partir d’un coffre de clés dans un emplacement Azure peut être restauré tooa le coffre de clés dans un autre emplacement Azure, tant que ces deux conditions sont remplies :

- Les deux hello Azure emplacements appartiennent toohello même emplacement géographique
- De coffres de clé hello appartenir toohello même abonnement Azure

Par exemple, une sauvegarde effectuée par un abonnement donné d’une clé dans un coffre de clés dans l’ouest de l’Inde, peut être uniquement de coffre de clés tooanother restaurée Bonjour même abonnement et l’emplacement géographique ; Ouest de l’Inde, Inde centrale ou Inde du Sud.

## <a name="regions-and-products"></a>Régions et produits

- [Régions Azure](https://azure.microsoft.com/regions/)
- [Produits Microsoft par région](https://azure.microsoft.com/regions/services/)

Les régions sont mappés toosecurity mondes, affichés en tant qu’en-têtes principales dans les tables de hello :

Dans les produits hello par l’article de la région, par exemple, hello **Americas** onglet contient EAST US, centre des États-Unis, ouest des États-Unis tous les mappage toohello Americas région. 

>[!NOTE]
>US DOD EAST et US DOD CENTRAL sont des exceptions, dans la mesure où ils possèdent leurs propres mondes de sécurité. 

De même, sur hello **Europe** sous l’onglet EUROPE du Nord et EUROPE de l’ouest mappent tous les deux toohello la région Europe. Hello vaut également sur hello **Asie Pacifique** onglet.



