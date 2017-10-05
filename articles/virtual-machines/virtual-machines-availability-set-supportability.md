---
title: "Possibilité de prise en charge de l’ajout de machines virtuelles Azure à un groupe à haute disponibilité | Microsoft Docs"
description: "Possibilité de prise en charge de l’ajout de machines virtuelles Azure à un groupe à haute disponibilité."
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
ms.openlocfilehash: 3ce9b8a79108cb9e57df14bcb3354cc637193233
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="supportability-of-adding-azure-vms-to-an-existing-availability-set"></a>Possibilité de prise en charge de l’ajout de machines virtuelles Azure à un groupe à haute disponibilité

Vous pouvez parfois rencontrer des limitations lorsque vous ajoutez des machines virtuelles à un groupe à haute disponibilité. Le tableau suivant détaille les séries de machines virtuelles que vous pouvez combiner dans le même groupe à haute disponibilité.

Voici la matrice de possibilité de prise en charge pour combiner différents types de machines virtuelles :

Série et groupe à haute disponibilité|Deuxième machine virtuelle|A|Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Première machine virtuelle|||||||
|A||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

Les autres séries ne pourraient pas être dans le même groupe à haute disponibilité, car elles nécessitent un matériel spécifique.