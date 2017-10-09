---
title: "problèmes de disponibilité aaaApplication et le service pour le FAQ de Microsoft Azure Cloud Services | Documents Microsoft"
description: "Cet article répertorie les hello Forum aux questions sur la disponibilité des applications et services pour les Services de Cloud de Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problèmes de disponibilité des applications et des services pour Azure Cloud Services : questions fréquentes (FAQ)

Cet article comprend des questions fréquentes sur les problèmes de disponibilité des applications et des services pour [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). Vous pouvez également consulter hello [page de taille de machine virtuelle de Services Cloud](cloud-services-sizes-specs.md) pour les informations de taille.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a>Mon rôle a été recyclé. Mon service cloud a-t-il fait l’objet d’une mise à jour ?
Environ une fois par mois, Microsoft publie une nouvelle version du système d’exploitation (SE) invité pour les machines virtuelles PaaS Microsoft Azure. Le système d’exploitation invité n'est qu’une telle mise à jour dans le pipeline de hello. Une publication peut être affectée par beaucoup d’autres facteurs. Par ailleurs, Azure s’exécute sur des centaines de milliers de machines. Par conséquent, il est impossible toopredict hello exacte horodatage lorsque vos rôles redémarreront. Nous mettons à jour hello invité du système d’exploitation mettre à jour les flux RSS avec hello dernières informations dont nous disposons ne, mais vous devez envisager de qui a signalé le temps toobe une valeur approximative. Nous savons que cela peut être problématique pour les clients et travaillez sur un plan toolimit ou précisément les redémarrages de temps.

Pour plus d’informations sur les dernières mises à jour du SE invité, consultez [Versions du SE invité et matrice de compatibilité du kit SDK Azure](cloud-services-guestos-update-matrix.md).

Pour obtenir des informations utiles sur les détails tootechnical redémarre et des pointeurs de mises à jour du système d’exploitation hôte et de l’invité, consultez hello du blog MSDN [rôle Instance redémarre en raison des mises à niveau de tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a>Pourquoi hello première demande toomy cloud service une fois que le service de hello a été inactif pendant un certain temps prend plu de temps ?
Lorsque hello serveur Web reçoit la première demande de hello, il tout d’abord recompile les code hello et puis traite la demande de hello. Qui est pourquoi hello première demande plus long que hello d’autres. Par défaut, le pool d’applications hello obtient arrêter en cas d’inactivité de l’utilisateur. pool d’applications Hello recycle également par défaut toutes les 1 740 minutes (29 heures).

Pools d’applications Internet Information Services (IIS) peuvent être tooavoid recyclées périodiquement des états instables qui peuvent entraîner des fuites de mémoire, des blocages ou des pannes de tooapplication.

Hello suivant documents vous aideront à comprendre et résoudre ce problème :
* [Fixing slow initial load for IIS](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis) (Remédier à la lenteur du chargement initial pour IIS)
* [IIS 7.5 web application first request after app-pool recycle very slow](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow) (Premier requête d’application web IIS 7.5 après une opération de recyclage de pool d’applications très lente)

Si vous souhaitez toochange par défaut hello d’IIS, vous devez toouse des tâches de démarrage, car si vous appliquez manuellement des instances de rôle Web toohello de modifications, les modifications de hello finalement seront perdues.

Pour plus d’informations, consultez [des tâches de démarrage tooconfigure et exécution d’un service cloud](cloud-services-startup-tasks.md).
