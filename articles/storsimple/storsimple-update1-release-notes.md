---
title: "notes de mise à jour de série 1.2 aaaStorSimple 8000 | Documents Microsoft"
description: "Décrit les hello nouvelles fonctionnalités, des problèmes et des solutions de contournement pour StorSimple 8000 Series Update 1.2."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c9aae87-6f77-44b8-b7fa-ebbdc9d8517c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7f564b794573fc3302ab15732e8dd85632ab9243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-12-release-notes-for-your-storsimple-8000-series-device"></a>Notes de publication Update 1.2 pour votre appareil StorSimple série 8000

## <a name="overview"></a>Vue d'ensemble
Bonjour notes de publication suivantes décrivent les nouvelles fonctionnalités de hello et identifient les problèmes critiques en suspens hello pour StorSimple 8000 Series Update 1.2. Ils contiennent également une liste des logiciels de StorSimple de hello, des pilotes et des mises à jour du microprogramme de disque inclus dans cette version. 

Mise à jour 1.2 permettre être appliqués tooany l’appareil StorSimple en cours d’exécution mise en production (GA), mise à jour 0.1, mise à jour 0,2 ou logiciel mises à jour 0.3. La solution Update 1.2 n'est pas disponible si votre appareil exécute Update 1 ou Update 1.1. Si votre appareil exécute la version (GA), veuillez [contactez le Support Microsoft](storsimple-contact-microsoft-support.md) tooassist vous avec cette mise à jour.

Hello suivant versions logicielles table listes hello appareil correspondant tooUpdates 1, 1.1 et 1.2.

| Si vous exécutez la mise à jour... | voici la version de logiciel de votre appareil. |
| --- | --- |
| Update 1.2 |6.3.9600.17584 |
| Update 1.1 |6.3.9600.17521 |
| Update 1.0 |6.3.9600.17491 |

Veuillez consulter les informations de hello contenues dans la version de hello notes avant de déployer hello mettre à jour dans votre solution StorSimple. Pour plus d’informations, consultez Comment trop[installer 1.2 de mise à jour sur votre appareil StorSimple](storsimple-install-update-1.md). 

> [!IMPORTANT]
> * Il prend environ 5 à 10 heures tooinstall cette mise à jour (y compris les mises à jour de Windows hello). 
> * Update 1.2 contient des mises à jour du logiciel, du pilote LSI et du microprogramme de disque. tooinstall, suivez les instructions hello dans [installer 1.2 de mise à jour sur votre appareil StorSimple](storsimple-install-update-1.md).
> * Pour les nouvelles versions, vous ne voyiez pas les mises à jour immédiatement, car nous effectuer un déploiement échelonné des mises à jour hello. Revérifiez les mises à jour dans quelques jours, car elles seront bientôt disponibles.
> 
> 

## <a name="whats-new-in-update-12"></a>Nouveautés d'Update 1.2
Ces fonctionnalités ont été apparues avec Update 1 qui a été ensemble faite tooa disponible limité d’utilisateurs. Avec la version de hello 1.2 de mise à jour, la plupart des utilisateurs de StorSimple hello verriez hello suivant des améliorations et nouvelles fonctionnalités :

* **Migration à partir d’appareils de séries 5000-7000 series too8000** – cette version introduit une nouvelle fonctionnalité de migration qui permet de hello StorSimple 7000 de 5000 série appliance utilisateurs toomigrate leur appareil physique de données tooa StorSimple 8000 series ou un équipement virtuel. fonctionnalité de migration Hello a deux propositions de valeur de clé :                                                                  
  
  * **Continuité des activités**, en activant la migration des données existantes sur les matériels de la gamme too8000 équipements série 7000 de 5000.
  * **Amélioration des offres de la fonctionnalité d’équipements de série hello 8000**, telles que la gestion centralisée efficace de plusieurs applications par le service StorSimple Manager, une meilleure classe du matériel et mise à jour de microprogramme, équipements virtuels, mobilité des données et fonctionnalités dans les futurs hello.
    
    Consultez toohello [guide de migration](http://www.microsoft.com/download/details.aspx?id=47322) pour plus d’informations sur la façon de toomigrate un appareil de série StorSimple 7000 de 5000 série tooan 8000. 
* **Disponibilité Bonjour Azure Government portail** – StorSimple est désormais disponible dans le portail d’administration d’Azure hello. Consultez Comment trop[déployer un appareil StorSimple Bonjour Azure Government Portal](storsimple-deployment-walkthrough-gov.md).
* **Prise en charge d’autres fournisseurs de services cloud** : hello autres fournisseurs de services cloud pris en charge sont Amazon S3, S3 Amazon avec les enregistrements de ressources, HP et OpenStack (bêta).
* **Mettre à jour les API de stockage de toolatest** – avec cette version, StorSimple a été mis à jour de service de stockage Azure dernière toohello API. Les unités StorSimple 8000 series qui exécutent des versions des logiciels avant de la mise à jour 1 (version, 0.1, 0,2 et 0,3) utilisent des versions de hello API de Service de stockage Azure antérieures à 17 juillet 2009. Comme indiqué dans la mise à jour de hello [annonce sur la suppression des versions de service de stockage](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx), par le 1er août 2016, ces API sera déconseillé. Il est impératif que vous appliquez tooAugust préalable de hello StorSimple 8000 Series Update 1 1, 2016. Si vous ne toodo par conséquent, les appareils StorSimple cesser de fonctionner correctement.
* **Prend en charge pour la Zone redondant stockage (ZRS)** : hello toohello mise à niveau dernière version de hello API de stockage, les séries hello StorSimple 8000 prendra en charge Zone Redundant Storage (ZRS) dans Ajout tooLocally stockage redondant (LRS) et géo-redondant Stockage (GRS). Consultez toothis [l’article sur les options de redondance de stockage Azure](../storage/common/storage-redundancy.md) pour plus d’informations ZRS.
* **Améliorer l’expérience de déploiement et de mise à jour initiale** : dans cette version, hello installation et le processus de mise à jour ont été améliorées. installation Hello via l’Assistant d’installation hello est utilisateur de toohello tooprovide améliorée des commentaires si les paramètres de pare-feu et de configuration de réseau hello sont incorrects. Les applets de commande de diagnostic supplémentaires ont été fournis toohelp vous résolution des problèmes de mise en réseau du périphérique de hello. Consultez hello [dépannage des déploiement](storsimple-troubleshoot-deployment.md) pour plus d’informations sur les applets de commande diagnostic nouvelle hello utilisé pour le dépannage.

## <a name="issues-fixed-in-update-12"></a>Problèmes résolus dans Update 1.2
Hello tableau suivant fournit un résumé des problèmes qui ont été résolus dans les mises à jour 1, 1.1 et 1.2.    

| Non. | Fonctionnalité | Problème | Résolu dans Update | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- | --- |
| 1 |Windows PowerShell pour StorSimple |Lorsqu’un utilisateur accessible à distance de l’appareil StorSimple hello à l’aide de Windows PowerShell pour StorSimple, puis démarré Assistant hello, un incident se produise dès que Data 0 IP a été entré. Ce bogue a été corrigé dans Update 1. |Update 1 |Oui |Oui |
| 2 |Réinitialisation aux paramètres d’usine |Dans certains cas, lorsque vous avez effectué une réinitialisation des paramètres, l’appareil StorSimple hello est bloqué et affiche ce message : **toofactory de réinitialisation est en cours (phase 8)**. Ceci se produire si vous avez appuyé sur CTRL + C lors de l’applet de commande hello était en cours. Ce bogue a été corrigé. |Update 1 |Oui |Non |
| 3 |Réinitialisation aux paramètres d’usine |Après la réinitialisation d’une fabrique de contrôleur double ayant échoué, vous étaient autorisés tooproceed avec l’inscription du périphérique. Cela entraînait la mise en place d’une configuration système non prise en charge. Dans Update 1, un message d’erreur s’affiche et l’inscription de l’appareil présentant un échec de réinitialisation aux paramètres d’usine est bloquée. |Update 1 |Oui |Non |
| 4 |Réinitialisation aux paramètres d’usine |Dans certains cas, des alertes d’incompatibilité illégitimes étaient émises. Les alertes illégitimes d’incompatibilité ne seront plus générées sur les appareils exécutant Update 1. |Update 1 |Oui |Non |
| 5 |Réinitialisation aux paramètres d’usine |Si une réinitialisation des paramètres a été interrompue toocompletion préalable, hello appareil entré en mode de récupération et n’a pas permis vous tooaccess Windows PowerShell pour StorSimple. Ce bogue a été corrigé. |Update 1 |Oui |Non |
| 6 |Récupération d'urgence |Un bogue de reprise après incident a été résolu : récupération d’urgence échoue pendant la découverte de hello des sauvegardes sur le périphérique cible de hello. |Update 1 |Oui |Oui |
| 7 |LED de contrôle |Dans certains cas, la DEL de surveillance à hello arrière appliance n’indiquent pas état correct. DEL de Hello bleu a été mis hors tension. Les LED de DATA 0 et DATA 1 clignotaient, même lorsque ces interfaces n’étaient pas configurées. Hello problème a été résolu et LED de surveillance indique désormais état correct de hello. |Update 1 |Oui |Non |
| 8 |LED de contrôle |Dans certains cas, après avoir appliqué la mise à jour 1, lumière hello bleu sur le contrôleur actif de hello désactivé ce qui le rend contrôleur actif de disque dur tooidentify hello. Ce problème a été résolu dans cette version du correctif. |Update 1.2 |Oui |Non |
| 9 |Interfaces réseau |Dans les versions précédentes, un appareil StorSimple configuré avec une passerelle non routable pouvait se déconnecter. Dans cette version, métrique de routage hello pour Data 0 a été effectuée hello plus bas ; Par conséquent, même si d’autres interfaces réseau soient activé pour le cloud, hello cloud trafic à partir de l’appareil de hello sera routé via Data 0. |Update 1 |Oui |Oui |
| 10 |Sauvegardes |Un bogue dans la mise à jour 1, ce qui a provoqué sauvegardes toofail après 24 jours a été résolu dans le correctif de hello version 1.1 de la mise à jour. |Update 1.1 |Oui |Oui |
| 11 |Sauvegardes |Un bogue dans les versions précédentes entraînait une baisse des performances pour les instantanés cloud avec un taux de modification faible. Ce bogue a été résolu dans cette version du correctif. |Update 1.2 |Oui |Oui |
| 12 |Mises à jour |Un bogue dans la mise à jour 1 qui a signalé un échec de la mise à niveau et a provoqué hello contrôleurs toogo en mode de récupération a été résolu dans cette version du correctif. |Update 1.2 |Oui |Oui |

## <a name="known-issues-in-update-12"></a>Problèmes connus dans Update 1.2
Hello tableau suivant fournit un résumé des problèmes connus dans cette version.

| Non. | Fonctionnalité | Problème | Commentaires/solution de contournement | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- | --- |
| 1 |Disque quorum |Dans de rares cas, si la majorité de hello des disques du boîtier EBOD de hello d’un appareil 8600 se déconnectent et où aucun quorum de disque, puis pool de stockage hello sera hors connexion. Il restera hors connexion, même si les disques hello sont reconnectés. |Vous devrez le périphérique de hello tooreboot. Si hello problème persiste, contactez le Support technique de Microsoft pour les étapes suivantes. |Oui |Non |
| 2 |ID de contrôleur incorrect |Lorsqu’un contrôleur est remplacé, le contrôleur 0 peut apparaître comme contrôleur 1. Pendant le remplacement de contrôleur, lors de l’image de hello est chargée à partir du nœud d’homologue hello, ID de contrôleur hello permettre s’afficher d’abord en tant qu’ID. du contrôleur hello homologue Dans de rares cas, ce comportement peut également se produire après un redémarrage du système. |Aucune action utilisateur n’est requise. Cette situation se résoudra de lui-même après le remplacement du contrôleur hello. |Oui |Non |
| 3 |Comptes de stockage |À l’aide du compte de stockage du service toodelete hello hello stockage est un scénario non pris en charge. Cela entraîne une situation tooa dans lequel les données de l’utilisateur ne peut pas être récupérées. |Oui |Oui | |
| 4 |Basculement de l’appareil |Basculements multiples d’un conteneur de volume à partir de hello même équipements toodifferent appareil source n’est pas pris en charge. Basculement de l’appareil à partir d’un seul morts toomultiple périphériques rend les conteneurs de volumes hello sur hello appareil basculé tout d’abord perdent la propriété de données. Après un tel basculement, ces conteneurs de volumes apparaît ou se comportent différemment lorsque vous les affichez dans hello portail Azure classic. | |Oui |Non |
| 5 |Installation |Au cours de l’adaptateur StorSimple pour l’installation de SharePoint, vous devez tooprovide une adresse IP dans l’ordre pour hello installation toofinish appareil avec succès. | |Oui |Non |
| 6 |Proxy web |Si votre configuration du proxy web a HTTPS comme hello spécifié de protocole, puis votre appareil au service communication est affectée et les appareils de hello passera en mode hors connexion. Prise en charge les packages sont également générés dans le processus de hello, consomment des ressources importantes sur votre appareil. |Assurez-vous que les URL du proxy web hello a HTTP comme hello protocole spécifié. Pour plus d’informations, consultez trop[configurer un proxy web pour votre appareil](storsimple-configure-web-proxy.md). |Oui |Non |
| 7 |Proxy web |Si vous configurez et activez le proxy web sur un appareil inscrit, puis vous devez contrôleur actif de toorestart hello sur votre appareil. | |Oui |Non |
| 8 |Latence de cloud élevée et charge de travail d’E/S élevée |Lorsque votre appareil StorSimple rencontre une combinaison de latences cloud très élevées (ordre de secondes) et la charge de travail d’e/s élevée, volumes du dispositif hello passe dans un état dégradé et hello e/s peut-être échouer avec une erreur « appareil non prêt ». |Vous devez contrôleurs d’appareil toomanually redémarrage hello ou effectuer une toorecover de basculement de périphérique à partir de cette situation. |Oui |Non |
| 9 |Azure PowerShell |Lorsque vous utilisez l’applet de commande StorSimple hello **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - tout d’abord 1 - attente** tooselect hello premier objet afin que vous pouvez créer un nouveau **VolumeContainer** de l’objet, hello applet de commande retourne tous les objets de hello. |Retour à la ligne hello applet de commande entre parenthèses comme suit : **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - tout d’abord 1 - attente** |Oui |Oui |
| 10 |Migration |Lorsque plusieurs conteneurs de volumes sont transmis pour la migration, hello ATE pour la sauvegarde la plus récente est exacte uniquement pour le premier conteneur de volume hello. En outre, la migration parallèle démarre une fois hello 4 premières sauvegardes dans le conteneur de volume premier hello sont migrés. |Nous vous recommandons de migrer un seul conteneur de volumes à la fois. |Oui |Non |
| 11 |Migration |Après la restauration de hello, les volumes ne sont pas ajoutés toohello sauvegarde hello ou stratégie de groupe de disque virtuel. |Vous devez tooadd ces stratégie de sauvegarde tooa volumes dans les sauvegardes de toocreate de commande. |Oui |Oui |
| 12 |Migration |Une fois la migration de hello terminée, appareil de série hello 5000/7000 ne doit pas accéder hello migrés des conteneurs de données. |Nous vous recommandons de supprimer hello migré les conteneurs de données après la migration hello est terminé et validé. |Oui |Non |
| 13. |Clonage et récupération d’urgence |Un appareil StorSimple 1 de la mise à jour en cours d’exécution ne peut pas cloner ou effectuer d’appareil tooa de récupération d’urgence avant mise à jour des 1 logiciels en cours d’exécution. |Vous devez tooupdate hello cible appareil tooUpdate 1 tooallow ces opérations |Oui |Oui |
| 14 |Migration |La sauvegarde de la configuration pour la migration peut être mise en échec sur un appareil de série 5000-7000 lorsqu’aucun volume n’est associé à certains groupes de volumes. |Supprimer tous les groupes de volumes vides hello avec aucun des volumes associés, puis réessayez sauvegarde de configuration hello. |Oui |Non |

## <a name="physical-device-updates-in-update-12"></a>Mises à jour des appareils physiques dans Update 1.2
Si la mise à jour de correctif 1.2 est appliqué tooa périphérique physique (en cours d’exécution tooUpdate de précédentes versions 1), version du logiciel hello change too6.3.9600.17584.

## <a name="controller-and-firmware-updates-in-update-12"></a>Mises à jour du contrôleur et du microprogramme dans Update 1.2
Cette version met à jour le pilote de hello et de microprogramme de disque hello sur votre appareil.

* Pour plus d’informations sur la mise à jour du contrôleur hello SAS, consultez [1 de mise à jour pour les contrôleurs SAS LSI dans Microsoft Azure StorSimple Appliance](https://support.microsoft.com/kb/3043005). 
* Pour plus d’informations sur la mise à jour de microprogramme de disque hello, consultez [du disque 1 de mise à jour pour Microsoft Azure StorSimple Appliance](https://support.microsoft.com/kb/3063416).

## <a name="virtual-device-updates-in-update-12"></a>Mises à jour des appareils virtuels dans Update 1.2
Cette mise à jour ne peut pas être appliqué toohello un appareil virtuel. Nouveaux périphériques virtuels devez toobe créé. 

## <a name="next-steps"></a>Étapes suivantes
* [Installer Update 1.2 sur votre appareil](storsimple-install-update-1.md).

