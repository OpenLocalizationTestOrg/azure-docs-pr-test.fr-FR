---
title: "aaaOperations gestion Suite de sécurité et la sécurité des données d’Audit solutions | Documents Microsoft"
description: "Ce document explique de quelle manière les données sont gérées et protégées dans la solution de sécurité et d’audit d’Operations Management Suite."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a>Solution de sécurité et d’audit d’Operations Management Suite - Sécurité des données
les clients toohelp empêcher, détecter et répondre toothreats, [Operations Management Suite (OMS) Solution de sécurité et d’Audit](operations-management-suite-overview.md) recueille et traite les données sur vos ressources, notamment :

* Journaux des événements de sécurité
* Suivi d’événements pour les événements Windows (ETW)
* Événements d’audit AppLocker
* Journal du pare-feu Windows
* Événements Advanced Threat Analytics
* Résultats de l’évaluation de la base de référence
* Résultats de l’analyse anti-programme malveillant
* Résultats de l’évaluation des correctifs/mises à jour
* Flux auditées qui sont explicitement activés sur l’agent de hello

Nous faisons de confidentialité de hello tooprotect engagements forts et sécurité de ces données. Microsoft respecte les instructions de sécurité et de conformité toostrict : du codage toooperating un service.
Cet article explique comment les données sont gérées et protégées dans la solution de sécurité et d’audit d’Operations Management Suite (OMS).

## <a name="data-sources"></a>Sources de données
OMS Solution de sécurité et d’Audit analyser les données à partir de vos Machines virtuelles et les ordinateurs physiques où hello OMS Agent est installé. Elle peut collecter les informations de configuration relatives aux événements de sécurité, tels que les journaux IIS, les journaux d’audit et les journaux des événements Windows, ainsi que les messages syslog. Il peut s’agir des données suivantes : type et version de système d’exploitation, processus en cours d’exécution, nom de machine, adresses IP, utilisateur connecté et ID de locataire.  

## <a name="data-protection"></a>Protection des données
**La segmentation des données**: données sont maintenues séparées logiquement sur chaque composant dans le service de hello. Toutes les données sont balisées en fonction de l'organisation. Ce balisage est conservé tout au long du cycle de vie des données hello, et elle est appliquée à chaque couche de service de hello. 

**Accès aux données**: recommandations de sécurité tooprovide et examiner les menaces de sécurité potentielles, le personnel de Microsoft peut accéder aux informations collectées ou analysé par les services. Nous respecter toohello [termes du contrat de Services en ligne Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) et [déclaration de confidentialité](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), état que Microsoft ne sera pas utiliser les données clients ou dériver des informations à partir de celui-ci pour toute publication ou similaires à des fins commerciales. recommandations de sécurité tooprovide et examiner les menaces de sécurité potentielles, le personnel de Microsoft peut accéder aux informations collectées ou analysé par les services. Nous utilisent uniquement les données client comme requis tooprovide vous avec Azure services, y compris à des fins compatible avec la fourniture de ces services. Vous conservez tous les droits tooyour possédant des données.

**Utilisation des données**: Microsoft utilise des modèles et menaces vu sur plusieurs locataires tooenhance nos fonctions de détection et la prévention ; nous faire conformément aux engagements de confidentialité hello décrites dans nos [confidentialité Instruction](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

> [!NOTE]
> Emplacement des données est configuré au niveau d’espace de travail OMS hello, lors de la création d’espace de travail hello, qui fait partie hello initiale OMS sécurité et Audit du processus de configuration.
> 
> 

## <a name="see-also"></a>Voir aussi
Ce document explique comment les données sont gérées et protégées dans OMS. toolearn en savoir plus sur OMS solution de sécurité et d’Audit, consultez :

* [Présentation - Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Surveillance et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit](oms-security-responding-alerts.md)
* [Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-monitoring-resources.md)

