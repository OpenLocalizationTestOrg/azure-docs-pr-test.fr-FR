---
title: "aaaTroubleshoot un appareil StorSimple déployé | Documents Microsoft"
description: "Décrit comment toodiagnose et résoudre les erreurs qui se produisent sur un appareil StorSimple qui est actuellement déployée et opérationnel."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ea5d89ae-e379-423f-b68b-53785941d9d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: b48433055e05e3fb27575b88dca9f6b23c649ca2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-operational-storsimple-device"></a>Résolution des problèmes d'un appareil StorSimple opérationnel
## <a name="overview"></a>Vue d'ensemble
Cet article fournit des conseils de dépannage pour résoudre les problèmes de configuration que vous pouvez rencontrer une fois votre appareil StorSimple déployé et opérationnel. Il décrit les problèmes courants, les causes possibles et toohelp les étapes recommandées que résoudre les problèmes que vous pouvez rencontrer lorsque vous exécutez Microsoft Azure StorSimple. Ces informations s’appliquent appareil physique de tooboth hello StorSimple local et un appareil virtuel StorSimple hello.

À fin hello de cet article, que vous trouverez une liste des codes d’erreur que vous pouvez rencontrer au cours de l’opération de Microsoft Azure StorSimple, ainsi que des étapes, vous pouvez prendre les erreurs tooresolve hello. 

## <a name="setup-wizard-process-for-operational-devices"></a>Processus de l'Assistant Installation pour les appareils opérationnels
Utiliser l’Assistant de configuration hello ([Invoke-HcsSetupWizard][1]) toocheck hello de configuration de l’appareil et prenez les mesures correctives si nécessaire.

Lorsque vous exécutez l’Assistant Installation de hello sur un appareil précédemment configuré et opérationnel, les flux de processus hello est différent. Vous pouvez modifier uniquement hello suivant entrées :

* Adresse IP, Masque de sous-réseau et Passerelle
* Serveur DNS principal
* Serveur NTP principal
* Configuration du proxy web (facultatif)

Assistant Installation de Hello n’effectue pas hello opérations connexes toopassword collection et inscription de l’appareil.

## <a name="errors-that-occur-during-subsequent-runs-of-hello-setup-wizard"></a>Erreurs qui se produisent lors des exécutions suivantes de l’Assistant Installation de hello
Hello tableau suivant décrit les erreurs de hello que vous pouvez rencontrer lorsque vous exécutez l’Assistant Installation de hello sur un appareil opérationnel, les causes possibles pour les erreurs de hello et les actions recommandées tooresolve les. 

| Non. | Message d'erreur ou condition | Causes possibles | Action recommandée |
|:--- |:--- |:--- |:--- |
| 1 |Erreur 350032 : cet appareil a déjà été désactivé. |Vous recevez cette erreur si vous exécutez l’Assistant Installation de hello sur un périphérique qui est désactivé. |[contactez le support technique Microsoft](storsimple-contact-microsoft-support.md) . Un appareil désactivé ne peut pas être mis en service. Une réinitialisation des paramètres peut être nécessaire avant de l’appareil de hello peut être réactivé. |
| 2 |Invoke-HcsSetupWizard : ERROR_INVALID_FUNCTION(exception de HRESULT: 0x80070001) |mise à jour du serveur Hello DNS échoue. Les paramètres DNS sont des paramètres globaux et sont appliquées à toutes les interfaces réseau de hello activée. |Activer l’interface de hello et appliquez à nouveau les paramètres DNS de hello. Cela peut perturber le réseau hello pour les autres interfaces activées, car ces paramètres sont globaux. |
| 3 |Appareil de Hello apparaît toobe en ligne dans le portail du service StorSimple Manager hello, mais lorsque vous essayez de programme d’installation minimale de toocomplete hello et enregistrez la configuration de hello, hello échoue. |Pendant l’installation initiale, le proxy web hello n’était pas configuré, même s’il était un serveur proxy réel en place. |Hello d’utilisation [applet de commande Test-HcsmConnection] [ 2] erreur de hello toolocate. [Contactez le Support Microsoft](storsimple-contact-microsoft-support.md) en cas de problème de hello toocorrect impossible. |
| 4 |Invoke-HcsSetupWizard : Valeur n’est pas comprise dans la plage de hello attendu. |Cette erreur est générée par un masque de sous-réseau incorrect. Les causes possibles sont :  <ul><li> masque de sous-réseau Hello est manquant ou vide.</li><li>format de préfixe Ipv6 Hello est incorrect.</li><li>interface de Hello est activé pour le cloud, mais la passerelle de hello est manquant ou incorrect.</li></ul>Notez que DATA 0 est automatiquement activé pour le cloud si configuré via l’Assistant d’installation hello. |problème de hello toodetermine, utilisez sous-réseau 0.0.0.0 ou 256.256.256.256, puis regardez dans la sortie de hello. Entrez les valeurs correctes pour le masque de sous-réseau hello, la passerelle et préfixe Ipv6, en fonction des besoins. |

## <a name="error-codes"></a>Codes d’erreur
Les erreurs sont répertoriées dans l'ordre numérique.

| Numéro d'erreur | Description ou texte d’erreur | Action de l'utilisateur recommandée |
|:--- |:--- |:--- |
| 10502 |Une erreur s'est produite lors de l'accès à votre compte de stockage. |Patientez quelques minutes et réessayez. Si hello erreur persiste, veuillez contacter le Support Microsoft pour les étapes suivantes. |
| 40017 |opération de sauvegarde Hello a échoué car un volume spécifié dans la stratégie de sauvegarde hello est introuvable sur l’appareil de hello. |Renouvelez l’opération de sauvegarde hello, si hello erreur persiste, contactez le Support Microsoft. pour la suite de la procédure. |
| 40018 |opération de sauvegarde Hello a échoué car aucun des volumes hello spécifiés dans la stratégie de sauvegarde hello introuvables sur l’appareil de hello. |Renouvelez l’opération de sauvegarde hello, si hello erreur persiste, contactez le Support Microsoft. pour la suite de la procédure. |
| 390061 |système de Hello est occupé ou indisponible. |Patientez quelques minutes et réessayez. Si hello erreur persiste, veuillez contacter le Support Microsoft pour les étapes suivantes. |
| 390143 |Une erreur s'est produite avec le code d'erreur 390143. (Erreur inconnue.) |Si hello erreur persiste, contactez le Support technique de Microsoft pour les étapes suivantes. |

## <a name="next-steps"></a>Étapes suivantes
Si vous êtes problème hello Impossible tooresolve [contactez le Support Microsoft](storsimple-contact-microsoft-support.md) pour obtenir une assistance. 

[1]: https://technet.microsoft.com/en-us/%5Clibrary/Dn688135(v=WPS.630).aspx
[2]: https://technet.microsoft.com/en-us/%5Clibrary/Dn715782(v=WPS.630).aspx
