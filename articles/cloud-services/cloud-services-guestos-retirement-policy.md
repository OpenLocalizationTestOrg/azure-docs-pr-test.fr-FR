---
title: "guide de stratégie aaaSupportability et de retrait pour le système d’exploitation invité de Azure | Documents Microsoft"
description: "Fournit des informations sur ce que Microsoft prend en charge en ce qui concerne les toohello système d’exploitation invité de Azure utilisés par les Services de cloud computing."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 919dd781-4dc6-4e50-bda8-9632966c5458
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/26/2017
ms.author: raiye
ms.openlocfilehash: 6a86c42ac95d12bbf116d900b7afb26fc3fe34e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-supportability-and-retirement-policy"></a>Prise en charge et stratégie de suppression du SE invité d’Azure
Hello plus d’informations sur cette page concerne le système de d’exploitation invité Azure toohello ([système d’exploitation invité](cloud-services-guestos-update-matrix.md)) pour les rôles web et de travail des Services de Cloud (PaaS). Il ne s’applique pas tooVirtual Machines (IaaS).

Microsoft dispose d’un rapport publié [politique de support pour le système d’exploitation invité de hello](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq). page Hello que vous lisez décrit maintenant comment la stratégie de hello est implémenté.

stratégie de Hello est

1. Microsoft prendra en charge **hello au moins les deux dernières familles du système d’exploitation invité de hello**. Lorsqu’une famille est supprimée, les clients ont 12 mois à partir de hello officielle de suppression date tooupdate tooa famille plus récente du système d’exploitation invité.
2. Microsoft prendra en charge **hello au moins les deux dernières versions des familles de système d’exploitation invité hello pris en charge**.
3. Microsoft prendra en charge **hello au moins les deux dernières versions de hello Azure SDK**. Lorsqu’une version de hello que Kit de développement logiciel est mis hors service, les clients ont 12 mois à partir de la version plus récente tooa du tooupdate date hello officielle de suppression.

Plus de deux familles ou versions peuvent parfois être prises en charge. Les informations officielles de prise en charge du système d’exploitation invité seront affiche sur hello [versions de système d’exploitation invité Azure et matrice de compatibilité SDK](cloud-services-guestos-update-matrix.md).

## <a name="when-a-guest-os-family-or-version-is-retired"></a>Lorsqu'une version ou une famille de systèmes d'exploitation invités est supprimée
Un nouveau système d’exploitation invité **famille** est introduit un certain temps après la mise en production hello d’une nouvelle version officielle du système d’exploitation de serveur Windows hello. Chaque fois qu’une nouvelle famille de système d’exploitation invité est présentée, Microsoft retirera famille de système d’exploitation invité hello plus ancien.

Nouveau système d’exploitation invité **versions** sont introduits sur chaque mois tooincorporate hello dernières mises à jour MSRC. En raison de hello régulières mises à jour mensuelles, une version de système d’exploitation invité est généralement désactivée 60 jours après sa publication. Cette activité permet de conserver au moins deux versions de système d'exploitation invité pour chaque famille à disposition.

### <a name="process-during-a-guest-os-family-retirement"></a>Processus de suppression d'une famille de SE invités
Une fois que hello retrait annoncé, les clients ont une période de 12 mois « transition » avant de la famille plus ancienne de hello soit officiellement supprimée du service. Cette durée de transition peut être étendue à la discrétion de hello de Microsoft. Les mises à jour seront publiées sur hello [versions de système d’exploitation invité Azure et matrice de compatibilité SDK](cloud-services-guestos-update-matrix.md).

Un processus de retrait progressif commence six (6) mois à la période de transition hello. Pendant cette période :

1. Microsoft informe les clients de mise hors service hello.
2. version plus récente de Hello Hello Azure SDK ne prend en charge la famille de système d’exploitation invité hello mis hors service.
3. Ne pourra de nouveaux déploiements et redéploiements de Services Cloud sur la famille de hello mis hors service

Microsoft continuera à toointroduce nouvelle version du système d’exploitation invité incorporant les mises à jour MSRC dernière hello jusqu'à hello dernier jour de la période de transition hello, appelée hello « date d’expiration ». Sur la date d’expiration de hello, Services de Cloud en cours d’exécution sera pris en charge sous hello contrat SLA Azure. Microsoft a hello discrétion tooforce mise à niveau, supprimer ou arrêter ces services après cette date.

### <a name="process-during-a-guest-os-version-retirement"></a>Processus de suppression d'une version de SE invité
Si les clients définir leur mise à jour de système d’exploitation invité tooautomatically, ils n’ont jamais tooworry sur le traitement des versions de système d’exploitation invité. Il utilisera toujours dernière version de système d’exploitation invité hello.

Les versions de SE invité sont publiées chaque mois. En raison de la fréquence de hello des versions normales, chaque version a un cycle de vie fixe.

Après 60 jours à la durée de vie hello, est une version «*désactivé*». « Désactivé » signifie que la version hello est supprimée hello portail. version de Hello ne peut plus être définie à partir du fichier de configuration CSCFG hello. Les déploiements existants continuent d’être exécutés. Mais les nouveaux déploiements et code et la configuration des déploiements tooexisting mises à jour ne seront pas autorisées.

Après devient « disabled, » hello version du système d’exploitation invité »*expiration*» et toutes les installations qui exécutent encore cette version sont obligatoirement mis à niveau et de définir tooautomatically hello de mise à jour du système d’exploitation invité dans hello futures. L’expiration intervient en lots période hello de désactivation tooexpiration permettre varier.

Ces périodes peuvent être allongées aux transitions des clients tooease discrétion de Microsoft. Toutes les modifications sont communiquées sur hello [versions de système d’exploitation invité Azure et matrice de compatibilité SDK](cloud-services-guestos-update-matrix.md).

### <a name="notifications-during-retirement"></a>Notifications pendant la suppression
* **Suppression de famille** <br>Microsoft utilise les billets de blog et la notification du portail. Les clients qui utilisent encore une famille de système d’exploitation invité supprimée seront notifiées via les administrateurs de service tooassigned communication directe (courrier électronique, messages de portail, appel téléphonique). Toutes les modifications sont validées toothis page et hello flux RSS répertorié au début de hello de cette page.
* **Suppression de version** <br>Toutes les modifications et les dates hello qu’ils se produisent seront publiées toothis page et hello flux RSS répertorié au début de hello de cette page, y compris la mise en production, désactivé et l’expiration. Les administrateurs de services recevront des e-mails s'ils ont des déploiements en cours d'exécution sur une version ou une famille de systèmes d'exploitation invités désactivée. minutage Hello de ces messages électroniques peut varier. En général, ils sont envoyés au moins un mois avant la désactivation, bien que ce délai ne soit pas officiellement fixé.

## <a name="frequently-asked-questions"></a>Forum Aux Questions
**Comment puis-je atténuer les impacts hello de la migration ?**

Nous vous recommandons d’utiliser la famille la plus récente de SE invités pour concevoir vos services cloud.

1. Commencez la planification de votre famille plus récente de migration tooa tôt.
2. Définir votre Service Cloud en cours d’exécution sur la nouvelle famille de hello tootest des déploiements de test temporaire.
3. Définissez votre version de système d’exploitation invité trop**automatique** (osVersion = * Bonjour [.cscfg](cloud-services-model-and-package.md#cscfg) fichier) afin que les versions de système d’exploitation invité hello migration toonew se produise automatiquement.

**Que se passe-t-il si mon application web nécessite une intégration plus étroite avec hello du système d’exploitation ?**

Si votre architecture d’application web dépend des fonctionnalités sous-jacentes du système d’exploitation de hello, utilisez les fonctionnalités de la plateforme prise en charge tels que [tâches de démarrage](cloud-services-startup-tasks.md) ou d’autres mécanismes d’extensibilité. Ou bien, vous pouvez également utiliser [des Machines virtuelles Azure](https://azure.microsoft.com/documentation/scenarios/virtual-machines/) (IaaS – Infrastructure en tant que Service), où vous êtes responsable de hello sous-jacente du système d’exploitation.

## <a name="next-steps"></a>Étapes suivantes
Hello révision dernières [mises à jour de système d’exploitation invité](cloud-services-guestos-update-matrix.md).
