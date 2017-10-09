---
title: "aaaSupportability d’ajout de machines virtuelles Azure tooan à haute disponibilité existant | Documents Microsoft"
description: "Prise en charge de l’ajout de machines virtuelles Azure tooan à haute disponibilité existant."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>Prise en charge de l’ajout de machines virtuelles Azure tooan à haute disponibilité existant

Vous pouvez parfois rencontrer des limitations lorsque vous ajoutez de nouvelles machines virtuelles (VM) tooan à haute disponibilité existant. Hello suivant détaille graphique les séries de machines virtuelles que vous pouvez combiner dans hello même groupe à haute disponibilité.

Voici hello prise en charge matrice toomix différents types d’ordinateurs virtuels :

Série et groupe à haute disponibilité|Deuxième machine virtuelle|A|Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Première machine virtuelle|||||||
|A||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

Toutes les autres séries n’a pas pu être Bonjour groupe à haute disponibilité de même, car elles nécessitent un matériel spécifique.
