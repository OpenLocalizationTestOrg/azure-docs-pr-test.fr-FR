---
title: aaaSecure votre Internet of Things (IoT) dans Azure | Documents Microsoft
description: " Les services Azure IoT (Internet des objets) offrent un large éventail de fonctionnalités. Cet article vous aidera à comprendre comment toosecure vos solutions IoT dans Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a>Présentation de la sécurité de l’Internet des objets
Les services Azure IoT (Internet des objets) offrent un large éventail de fonctionnalités. Ces services de niveau professionnel vous permettent d’effectuer les tâches suivantes :

* Collecter des données à partir des appareils
* Analyser les flux de données en mouvement
* Stocker et interroger des jeux de données volumineux
* Visualiser les données historiques et en temps réel
* Intégrer des systèmes back-office

toodeliver ensemble de ces fonctionnalités, Azure IoT Suite packages Azure plusieurs services avec des extensions personnalisées en tant que solutions préconfigurées. Ces solutions préconfigurées sont des implémentations de base des modèles de solution IoT courants qui aident à tooreduce hello le temps vous toodeliver vos solutions IoT. À l’aide de kits de développement logiciel hello IoT, vous pouvez personnaliser et étendre ces toomeet solutions vos propres exigences. Vous pouvez également utiliser ces solutions comme des exemples ou modèles lorsque vous développez de nouvelles solutions IoT.

Bonjour Azure IoT suite est une solution efficace à vos besoins IoT. Toutefois, il est d’importance parlé que vos solutions IoT conçues avec la sécurité en tenant compte du début de hello. En raison du nombre élevé de hello des appareils IoT, un incident de sécurité peut rapidement devenir un événement généralisée avec lourdes conséquences.

toohelp vous comprenez comment toosecure vos solutions IoT, nous avons hello informations suivantes.

## <a name="security-architecture"></a>Architecture de la sécurité
Lorsque vous concevez un système, il est important toounderstand les menaces potentielles hello toothat système et ajouter les défenses en conséquence, comme système de hello est conçu et mise en œuvre. Il est important de toodesign hello produit à partir du début de hello avec la sécurité à l’esprit, car vous assurer que les solutions d’atténuation appropriées sont en place à partir du début de hello permet de comprendre comment un intrus peut être en mesure de toocompromise un système.

Vous pouvez en savoir plus sur architecture de sécurité IoT en lisant l’article [Architecture de sécurité de l’Internet des objets](../iot-suite/iot-security-architecture.md).

Cet article traite hello rubriques suivantes :

* [La sécurité commence par un modèle de menace](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [Sécurité des solutions IoT](../iot-suite/iot-security-architecture.md#security-in-iot)
* [Hello de modélisation de menace Architecture de référence Azure IoT](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a>Hello d’arrière-plan la sécurité
Hello IoT pose unique sécurité, confidentialité et la conformité défis toobusinesses dans le monde entier. Contrairement à la technologie cyber traditionnel où ces problèmes sont axés sur les logiciels et la façon dont il est implémenté, IoT concerne que se passe-t-il quand les cyber hello et des mondes physique hello convergent. Protection IoT solutions requiert vous être assuré de la configuration sécurisée des appareils, une connectivité sécurisée entre ces appareils et hello cloud et protection des données sécurisées dans le cloud de hello pendant le traitement et de stockage. Cependant, les appareils avec contraintes de ressources, la répartition géographique des déploiements et un grand nombre d’appareils au sein d’une solution limitent ces fonctionnalités.

Vous pouvez apprendre comment sécurité toohandle dans ces domaines en lisant [hello d’arrière-plan la sécurité Internet of Things](../iot-suite/securing-iot-ground-up.md).

Hello explique hello rubriques suivantes :

* [Infrastructure de sécurité à partir de hello d’arrière-plan](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [Microsoft Azure : une infrastructure IoT sécurisée pour votre entreprise](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a>Meilleures pratiques
La sécurisation d’une infrastructure IoT implique la mise en œuvre d’une stratégie de sécurité complète et rigoureuse. À partir de la sécurisation des données dans le cloud de hello, protéger l’intégrité des données pendant que pendant leur transit sur hello internet public, les appareils de configuration toosecurely, chaque couche crée une plus grande assurance de sécurité hello infrastructure globale.

Vous pouvez en savoir plus sur les meilleures pratiques de sécurité de l’Internet des objets en lisant [Internet des objets (IoT) : meilleures pratiques en matière de sécurité](../iot-suite/iot-security-best-practices.md).

Hello explique hello rubriques suivantes :

* [Fabricant/intégrateur de matériel IoT](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [Développeur de solutions IoT](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [Responsable du déploiement de solutions IoT](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [Opérateur de solutions IoT](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
