---
title: "aaaInternet des meilleures pratiques de sécurité des opérations | Documents Microsoft"
description: "article de Hello fournit une liste organisée de Microsoft Internet des meilleures pratiques de sécurité des éléments et des recommandations générales."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>Internet des objets (IoT) : meilleures pratiques en matière de sécurité
Infrastructure d’Internet des objets (IoT) hello sécurisation est une entreprise critique pour toute personne travaillant avec des solutions IoT. En raison de hello et nombre hello de périphériques concernés la nature distribuée de ces appareils, l’impact hello un événement de sécurité liées toocompromise de millions d’appareils IoT est non trivial et peut avoir une incidence importante.

Pour cette raison, la sécurité de l’IoT nécessite une approche en profondeur. Données besoins toobe sécurisée dans le cloud de hello et qu’elle se déplace sur des réseaux privés et publics. Les méthodes doivent toobe dans place toosecurely disposition hello appareils IoT eux-mêmes. Chaque couche, à partir de périphérique, toonetwork, toocloud principal a besoin de garanties de sécurité renforcée.

IoT meilleures pratiques peuvent être classés dans hello de configuration suivant :

* Fabricant ou intégrateur de matériel IoT
* Développeur de solutions IoT
* Responsable du déploiement de solutions IoT
* Opérateur de solutions IoT

Cet article résume les [meilleures pratiques de sécurité pour l’Internet des objets (IoT)](../iot-suite/iot-security-best-practices.md). Consultez l’article de toothat pour des informations plus détaillées.

## <a name="iot-hardware-manufacturer-or-integrator"></a>Fabricant ou intégrateur de matériel IoT
Suivez les meilleures pratiques hello ci-dessous si vous êtes un fabricant de matériel IoT ou un intégrateur de matériel :

* **Portée toominimum requise**: conception de matériel hello doit inclure les fonctionnalités minimales requises pour l’opération de matériel de hello et rien de plus. 
* **Assurez-vous matériel falsifications**: build mécanismes toodetect sabotage physique du matériel, telles que l’ouverture du capot du périphérique hello, supprimant une partie du hello, etc.. 
* **Intégrer la sécurité au matériel**: si le [coût des marchandises vendues](https://en.wikipedia.org/wiki/Cost_of_goods_sold) le permet, intégrez des fonctionnalités de sécurité, telles qu’un stockage sécurisé et chiffré, ainsi qu’une fonctionnalité de démarrage basée sur un Module de plateforme sécurisée (TPM).
* **Sécuriser les mises à niveau**: mise à jour pendant la durée de vie de l’appareil de hello est inévitable.

## <a name="iot-solution-developer"></a>Développeur de solutions IoT
Si vous êtes un développeur de solutions IoT, procédez comme meilleures pratiques hello ci-dessous :

* **Suivez la méthodologie de développement de logiciels sécurisés**: développement de logiciels sécurisés requiert des sol vous réfléchissez à la sécurité de la création de hello du projet de hello tous les mise en œuvre de hello moyen tooits, le test et déploiement.
* **Choisissez des logiciels open source avec précaution**: logiciel open source fournit une opportunité tooquickly développer des solutions.
* **Intégrer avec précaution**: nombre de failles de sécurité logicielles hello existent à la limite de hello de bibliothèques et d’API. 

## <a name="iot-solution-deployer"></a>Responsable du déploiement de solutions IoT
Suivez les meilleures pratiques hello ci-dessous si vous êtes un responsable du déploiement de la solution IoT :

* **Déployer le matériel en toute sécurité**: IoT déploiements peuvent nécessiter toobe matériel déployé dans des emplacements non sécurisés, comme dans les espaces publics ou des paramètres régionaux non supervisés.
* **Protéger les clés d’authentification**: pendant le déploiement, chaque appareil nécessite l’ID de périphérique et des clés d’authentification générés par le service de cloud computing hello associées. Protéger ces clés physiquement même après le déploiement de hello. N’importe quelle touche compromise utilisable par un toomasquerade malveillant périphérique comme un périphérique existant.

## <a name="iot-solution-operator"></a>Opérateur de solutions IoT
Suivez les meilleures pratiques hello ci-dessous si vous êtes un opérateur de solution IoT :

* **Conserver les systèmes toodate**: Assurez-vous de systèmes d’exploitation et tous les pilotes de périphérique sont les versions les plus récentes toohello mis à jour. 
* **Protection contre les activités malveillantes**: si le système d’exploitation de hello permet, placer hello dernières antivirus et anti-programme malveillant fonctionnalités sur chaque système d’exploitation. 
* **Audit fréquemment**: IoT infrastructure d’audit pour les problèmes est la clé lors de la réponse toosecurity incidents liés à la sécurité.
* **Protégez physiquement infrastructure de IoT hello**: hello pire pour lancer des attaques de sécurité contre IoT infrastructure à l’aide de l’accès physique toodevices.
* **Protéger les informations d’identification cloud**: informations d’identification de l’authentification cloud utilisées pour la configuration et l’utilisation d’un déploiement IoT sont éventuellement accès toogain moyen plus simple de hello et compromettre un système IoT. 

