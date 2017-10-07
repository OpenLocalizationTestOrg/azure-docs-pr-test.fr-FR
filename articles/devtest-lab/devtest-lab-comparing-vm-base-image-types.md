---
title: "aaaComparing des images personnalisées et les formules de DevTest Labs | Documents Microsoft"
description: "En savoir plus sur les différences de hello entre des images personnalisées et les formules comme base la machine virtuelle afin de décider laquelle correspond le mieux à votre environnement."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a>Comparaison entre les images personnalisées et les formules dans DevTest Labs
Les [images personnalisées](devtest-lab-create-template.md) et les [formules](devtest-lab-manage-formulas.md) peuvent toutes deux être utilisées comme bases pour [créer des machines virtuelles](devtest-lab-add-vm-with-artifacts.md). Toutefois, hello différence majeure entre des images personnalisées et les formules est qu’une image personnalisée est simplement une image basée sur un disque dur virtuel, tandis que la formule est une image basée sur un disque dur virtuel *à* préconfiguré paramètres - telles que la taille de machine virtuelle, un réseau virtuel, sous-réseau et les artefacts. Ces paramètres préconfigurés sont configurés avec les valeurs par défaut qui peuvent être remplacées au moment de hello de création d’ordinateurs virtuels. Cet article décrit certains des avantages de hello (pros) et inconvénients (cons) toousing des images et à l’aide de formules personnalisées.

## <a name="custom-image-pros-and-cons"></a>Avantages et inconvénients des images personnalisées
Images personnalisées fournissent un toocreate de façon statique, immuable machines virtuelles à partir d’un environnement de votre choix. 

**Avantages**

* Machine virtuelle à partir d’une image personnalisée de configuration est rapide que rien ne change après hello que machine virtuelle est lancé à partir de l’image de hello. En d’autres termes, il n’existe aucune tooapply paramètres comme image personnalisée de hello est simplement une image sans paramètres. 
* Les machines virtuelles créées à partir d’une même image personnalisée sont identiques.

**Inconvénients**

* Si vous devez tooupdate certains aspects de l’image personnalisée de hello, image de hello doit être recréé.  

## <a name="formula-pros-and-cons"></a>Avantages et inconvénients des formules
Les formules fournissent des machines virtuelles un toocreate de façon dynamique à partir des paramètres de la configuration souhaitée de hello.

**Avantages**

* Modifications dans l’environnement de hello peuvent être capturées à volée hello via les artefacts. Par exemple, si vous souhaitez une machine virtuelle installée avec les éléments les plus récents à partir de votre version de pipeline hello ou inscrivez le dernier code de hello à partir de votre référentiel, vous pouvez spécifier simplement un artefact qui déploie les éléments les plus récents hello ou inscrit le dernier code de hello dans la formule hello avec un image de base cible. Chaque fois que cette formule est utilisée toocreate VMs, hello derniers bits/code sont déployés/inscrite toohello machine virtuelle. 
* Les formules, à la différence des images personnalisées, peuvent définir des paramètres par défaut, par exemple la taille des machines virtuelles et les paramètres de réseau virtuel. 
* paramètres de Hello enregistrés dans une formule sont affichés sous forme de valeurs par défaut, mais peuvent être modifiées lors de la création de hello machine virtuelle. 

**Inconvénients**

* La création d’une machine virtuelle à partir d’une formule peut prendre plus de temps qu’à partir d’une image personnalisée.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Billets de blog connexes
* [Images personnalisées ou formules ?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Étapes suivantes
- [FAQ DevTest Labs](devtest-lab-faq.md)