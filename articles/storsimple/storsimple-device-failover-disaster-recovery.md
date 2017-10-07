---
title: "aaaStorSimple basculement et récupération d’urgence | Documents Microsoft"
description: "Découvrez comment toofail sur votre tooitself de périphérique StorSimple, une autre unité physique ou un périphérique virtuel."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5751598e-49c8-42b3-8121-fea5857a7d83
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/16/2016
ms.author: alkohli
ms.openlocfilehash: 00ce365f8a9095d1f0292e665d7f9eaa844b44ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-device"></a>Basculement et récupération d’urgence pour votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Ce didacticiel décrit toofail requis des étapes de hello sur un appareil StorSimple dans l’événement hello de sinistre. Un basculement vous permettra de toomigrate vos données à partir d’un périphérique source dans hello tooanother de centre de données physique ou même un périphérique virtuel situé dans hello même ou à un emplacement géographique différent. 

La récupération d’urgence (DR) est orchestrée via la fonctionnalité de basculement d’appareil hello et est lancée à partir de hello **périphériques** page. Cette page classifie tous les hello StorSimple périphériques connectés tooyour le service StorSimple Manager. Pour chaque périphérique, nom convivial de hello, état, la capacité configurée et maximale, le type et le modèle sont affichés.

![Page Appareils](./media/storsimple-device-failover-disaster-recovery/IC740972.png)

conseils Hello dans ce didacticiel s’applique les périphériques physiques et virtuels tooStorSimple sur toutes les versions de logiciels.

## <a name="disaster-recovery-dr-and-device-failover"></a>Récupération d’urgence et basculement d’appareil
Dans un scénario de récupération d’urgence, périphérique principal de hello cesse de fonctionner. Dans ce cas, vous pouvez déplacer les données de cloud de hello associées hello ayant échoué tooanother un périphérique à l’aide de périphérique principal de hello en hello *source* et en spécifiant un autre périphérique en tant que hello *cible*. Vous pouvez sélectionner un ou plusieurs volumes conteneurs toomigrate toohello équipement. Ce processus est référencé tooas hello *basculement*. 

Pendant le basculement de hello, conteneurs de volumes hello à partir de l’appareil source de hello changent de propriétaire et sont transférés toohello du périphérique cible. Une fois que les conteneurs de volumes hello modifier la propriété, ceux-ci sont supprimés à partir de l’appareil source de hello. Après que la suppression de hello est terminée, hello cible peut ensuite être Échec de l’unité précédent.

En général, une récupération d’urgence, la sauvegarde la plus récente hello est le périphérique cible toohello toorestore utilisé hello données. Toutefois, s’il existe plusieurs stratégies de sauvegarde pour hello même volume, puis stratégie de sauvegarde hello avec hello plus grand nombre de volumes est récupéré et sauvegarde la plus récente à partir de cette stratégie hello donnée utilisé toorestore hello sur le périphérique cible de hello.

Par exemple, s’il existe deux stratégies de sauvegarde (une valeur par défaut et un personnalisée) *defaultPol*, *customPol* avec hello les détails suivants :

* *defaultPol* : un seul volume, *vol1*, s’exécute tous les jours à 22 h 30.
* *customPol* : quatre volumes, *vol1*, *vol2*, *vol3* et *vol4*, s’exécutent tous les jours à 22 h 00.

Dans ce cas, *customPol* sera utilisée, car elle a plus de volumes et nous lui donnons la priorité pour des raisons de cohérence en cas d’incident. sauvegarde la plus récente de cette stratégie Hello donnée toorestore utilisé.

## <a name="considerations-for-device-failover"></a>Considérations relatives au basculement d’appareil
En cas de hello de sinistre, vous pouvez choisir toofail sur votre appareil StorSimple :

* périphérique physique de tooa 
* tooitself
* tooa un appareil virtuel

Pour un basculement de l’appareil, gardez suivante de hello l’esprit :

* Hello conditions préalables pour la récupération d’urgence sont que tous les volumes hello dans des conteneurs de volume hello sont hors connexion et les conteneurs de volumes hello ont associé à un instantané cloud. 
* Hello des périphériques de cibles disponibles pour la récupération d’urgence sont possédant suffisamment d’espace tooaccommodate hello conteneurs de volumes sélectionnés. 
* Hello périphériques qui sont connecté tooyour de service, mais ne répondent pas aux critères de hello de suffisantes espace ne sera pas disponible en tant que périphériques cibles.
* Après une récupération d’urgence, pour une durée limitée, performances d’accès aux données hello peuvent être affectées de manière significative, en tant que périphérique de hello sera peut-être tooaccess hello données hello cloud et stocker localement.

#### <a name="device-failover-across-software-versions"></a>Basculement de l'appareil entre les versions du logiciel
Un service StorSimple Manager dans un déploiement peut avoir plusieurs appareils physiques et virtuels, exécutant tous des versions différentes du logiciel. Selon la version du logiciel hello, hello volume types sur les appareils hello peuvent également être différents. Par exemple, un appareil exécutant Update 2 ou une version ultérieure aurait des volumes épinglés localement à plusieurs niveaux (l’archivage étant un sous-ensemble des niveaux). Un appareil avant de la mise à jour 2 sur hello autre part peut avoir plusieurs niveaux et les volumes de l’archivage. 

Utilisez hello suivant toodetermine de la table si vous pouvez basculer l’appareil tooanother un comportement de version et hello logiciels différents de types de volumes en cours d’exécution pendant la récupération d’urgence.

| Basculer à partir de | Autorisé pour un appareil physique | Autorisé pour un appareil virtuel |
| --- | --- | --- |
| Mise à jour 2 toopre-1 (version, 0.1, 0,2 et 0,3) |Non |Non |
| Mise à jour 2 tooUpdate 1 (1, 1.1, 1.2) |Oui <br></br>Si épinglé localement ou à plusieurs niveaux de volumes ou une combinaison des deux, hello volumes sont basculés toujours en tant que niveaux. |Oui<br></br>En cas d'utilisation de volumes épinglés localement, ceux-ci sont basculés sous la forme à plusieurs niveaux. |
| Mise à jour 2 tooUpdate 2 (version ultérieure) |Oui<br></br>Si vous utilisez des volumes localement épinglés ou à plusieurs niveaux ou une combinaison des deux, les volumes de hello sont basculés toujours comme hello à partir du type de volume ; à plusieurs niveaux à plusieurs niveaux et attaché localement attaché localement. |Oui<br></br>En cas d'utilisation de volumes épinglés localement, ceux-ci sont basculés sous la forme à plusieurs niveaux. |

#### <a name="partial-failover-across-software-versions"></a>Basculement partiel entre les versions du logiciel
Suivez ces instructions si vous envisagez de tooperform un basculement partiels à l’aide d’un appareil StorSimple en cours d’exécution cible 1 tooa de mise à jour avant l’exécution de Update 1 ou version ultérieure. 

| Basculement partiel à partir de | Autorisé pour un appareil physique | Autorisé pour un appareil virtuel |
| --- | --- | --- |
| Mettre à jour préalable de 1 (version, 0.1, 0,2 et 0,3) tooUpdate 1 ou version ultérieure |Oui, voir ci-dessous pour Conseil pratique de la meilleure hello. |Oui, voir ci-dessous pour Conseil pratique de la meilleure hello. |

> [!TIP]
> Une modification des métadonnées du cloud et du format des données dans la Mise à jour 1 et les versions ultérieures. Par conséquent, nous ne recommandons pas un basculement partiel à partir de la mise à jour avant de 1 tooUpdate 1 ou versions ultérieures. Si vous avez besoin d’un basculement partiels de tooperform, nous vous recommandons d’abord appliquer la mise à jour 1 ou version ultérieure sur les deux périphériques hello (source et cible) et de poursuivre le basculement de hello. 
> 
> 

## <a name="fail-over-tooanother-physical-device"></a>Basculer le périphérique physique de tooanother
Effectuer hello suivant les étapes toorestore périphérique tooa cible appareil physique.

1. Vérifiez que hello conteneur de volume toofail sur a associé à des instantanés cloud.
2. Sur hello **périphériques** , cliquez sur hello **conteneurs de volumes** onglet.
3. Sélectionnez un conteneur de volumes que vous aimeriez toofail sur tooanother appareil. Cliquez sur hello volume conteneur toodisplay hello liste des volumes de ce conteneur. Sélectionnez un volume, puis cliquez sur **mettre hors connexion** tootake le volume hello hors connexion. Répétez ce processus pour tous les volumes hello dans le conteneur de volume hello.
4. Étape précédente de hello Répétez ces étapes pour tous les hello conteneurs de volumes vous aimeriez toofail sur tooanother appareil.
5. Sur hello **périphériques** , cliquez sur **basculement**.
6. Dans l’Assistant hello qui s’ouvre, sous **choisir toofail conteneur de volume sur**:
   
   1. Dans la liste de hello des conteneurs de volumes, sélectionnez vous aimeriez toofail sur les conteneurs de volumes hello.
      **Hello uniquement les conteneurs de volumes avec des instantanés cloud associés et les volumes hors connexion sont affichés.**
   2. Sous **choisir un appareil cible** pour les volumes hello dans les conteneurs hello sélectionné, sélectionnez un périphérique cible à partir de la liste déroulante de hello de périphériques disponibles. Seuls les appareils hello ayant une capacité disponible de hello sont affichés dans la liste déroulante de hello.
   3. Enfin, passez en revue tous les paramètres de basculement hello sous **confirmer le basculement**. Cliquez sur une icône de coche hello ![coche](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
7. Un travail de basculement est créé qui peut être analysé via hello **travaux** page. Si le conteneur de volume hello ayant basculé possède des volumes locaux, vous verrez des travaux de restauration individuels pour chaque volume local (et non de volumes hiérarchisés) dans le conteneur de hello. Ces travaux de restauration peut prendre un certain toocomplete de temps. Il est probable que ce travail de basculement hello peut terminer plus tôt. Notez que ces volumes aura garanties locales uniquement après que les travaux de restauration hello est terminées. Une fois hello basculement terminé, accédez à toohello **périphériques** page.                                            
   
   1. Sélectionnez le périphérique hello qui a été utilisé en tant que périphérique cible de hello pour les processus de basculement hello.
   2. Accédez toohello **conteneurs de volumes** page. Tous les conteneurs de volume hello, ainsi que les volumes hello à partir de l’ancien périphérique de hello, doivent être répertoriés.

## <a name="failover-using-a-single-device"></a>Basculement à l’aide d’un seul appareil
Effectuer hello comme suit si vous disposez d’un seul tooperform de périphérique et la nécessité de basculement.

1. Prendre des instantanés de cloud de tous les volumes hello dans votre appareil.
2. Réinitialiser votre toofactory d’appareil. Suivez hello des instructions dans [comment tooreset un toofactory de périphérique StorSimple les paramètres par défaut](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Configurez votre appareil et réenregistrez-le avec votre service StorSimple Manager.
4. Sur hello **périphériques** page, l’ancien périphérique de hello doit apparaître comme étant **hors connexion**. Hello appareil nouvellement inscrit doit apparaître comme étant **Online**.
5. Nouvelle unité de hello, effectuer la configuration minimale de hello de périphérique de hello en premier. 
   
   > [!IMPORTANT]
   > **Si la configuration minimale hello n’est pas terminée tout d’abord, la récupération d’urgence échoue en raison d’un bogue dans l’implémentation actuelle de hello. Ce problème sera résolu dans une version ultérieure.**
   > 
   > 
6. Sélectionnez le périphérique de hello ancien (état hors connexion) et cliquez sur **basculement**. Dans l’Assistant hello qui s’affiche, basculer sur cet appareil et équipement hello comme appareil nouvellement inscrit de hello. Pour obtenir des instructions détaillées, voir la rubrique trop[basculer sur un périphérique physique de tooanother](#fail-over-to-another-physical-device).
7. Un travail de restauration du périphérique sera créé que vous pouvez surveiller de hello **travaux** page.
8. Une fois le travail de hello terminé, accéder au nouveau périphérique de hello et accédez toohello **conteneurs de volumes** page. Tous les conteneurs de volumes hello à partir de l’ancien périphérique de hello doivent maintenant être migrés toohello nouveau périphérique.

## <a name="fail-over-tooa-storsimple-virtual-device"></a>Basculer l’appareil virtuel StorSimple tooa
Vous devez disposer d’un StorSimple périphérique virtuel créé et configuré toorunning préalable cette procédure. Si la mise à jour 2 en cours d’exécution, envisagez d’utiliser un périphérique virtuel 8020 pour hello récupération d’urgence qui possède 64 To et utilise le stockage Premium. 

Effectuer hello suivant les étapes toorestore hello appareil tooa cible un appareil virtuel StorSimple.

1. Vérifiez que hello conteneur de volume toofail sur a associé à des instantanés cloud.
2. Sur hello **périphériques** , cliquez sur hello **conteneurs de volumes** onglet.
3. Sélectionnez un conteneur de volumes que vous aimeriez toofail sur tooanother appareil. Cliquez sur hello volume conteneur toodisplay hello liste des volumes de ce conteneur. Sélectionnez un volume, puis cliquez sur **mettre hors connexion** tootake le volume hello hors connexion. Répétez ce processus pour tous les volumes hello dans le conteneur de volume hello.
4. Étape précédente de hello Répétez ces étapes pour tous les hello conteneurs de volumes vous aimeriez toofail sur tooanother appareil.
5. Sur hello **périphériques** , cliquez sur **basculement**.
6. Dans l’Assistant hello qui s’ouvre, sous **choisissez toofailover de conteneur de volume**, suivez hello suivantes :
   
    a. Dans la liste de hello des conteneurs de volumes, sélectionnez vous aimeriez toofail sur les conteneurs de volumes hello.
   
    **Hello uniquement les conteneurs de volumes avec des instantanés cloud associés et les volumes hors connexion sont affichés.**
   
    b. Sous **choisir un appareil cible pour les volumes hello dans les conteneurs hello sélectionné**, sélectionnez hello périphérique virtuel StorSimple à partir de la liste déroulante de hello de périphériques disponibles. **Seuls les appareils hello ayant une capacité sont affichés dans la liste déroulante de hello.**  
7. Enfin, passez en revue tous les paramètres de basculement hello sous **confirmer le basculement**. Cliquez sur une icône de coche hello ![coche](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
8. Une fois hello basculement terminé, accédez à toohello **périphériques** page.
   
    a. Sélectionnez le périphérique virtuel hello StorSimple qui a été utilisé en tant que périphérique cible de hello pour les processus de basculement hello.
   
    b. Accédez toohello **conteneurs de volumes** page. Tous les conteneurs de volume hello, ainsi que les volumes hello à partir de l’ancien périphérique de hello doivent maintenant être affichés.

![Vidéo disponible](./media/storsimple-device-failover-disaster-recovery/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment vous pouvez restaurer un échec sur le périphérique virtuel de tooa périphérique physique dans le cloud de hello, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/storsimple-and-disaster-recovery/).

## <a name="failback"></a>Restauration automatique
Pour Update 3 et les versions ultérieures, StorSimple prend également en charge la restauration automatique. Une fois terminée, hello basculement hello actions suivantes se produisent :

* conteneurs de volumes Hello ayant basculé sont nettoyées à partir de l’appareil source de hello.
* Une tâche en arrière-plan par conteneur de volumes (basculé) est lancée sur le périphérique source de hello. Si vous essayez de toofailback alors que le travail de hello est en cours, vous recevrez un effet toothat de notification. Vous devez toowait jusqu'à ce que le travail de hello est la restauration automatique de hello toostart terminée. 
  
    Hello temps toocomplete hello la suppression de conteneurs de volumes dépend de divers facteurs tels que la quantité de données, la durée de vie de données de hello, nombre de sauvegardes et hello la bande passante disponible pour l’opération de hello. Si vous envisagez de tester les basculements / restaurations, nous vous recommandons de tester des conteneurs de volumes comprenant moins de données (Go). Dans la plupart des cas, vous pouvez démarrer la restauration automatique hello 24 heures après que le basculement de hello est terminé. 

## <a name="frequently-asked-questions"></a>Forum Aux Questions
Q : **Que se passe-t-il si hello récupération d’urgence échoue ou succès partiel ?**

R : En cas de récupération d’urgence de hello, nous vous recommandons d’essayer à nouveau. Hello deuxième fois, récupération d’urgence sait que tout a été effectué et lorsque les processus hello bloqué hello première fois. Hello, processus de récupération d’urgence démarre à partir de ce point et les versions ultérieures. 

Q : **Puis-je supprimer une unité pendant que le basculement de l’appareil hello est en cours ?**

R : Vous ne pouvez pas supprimer un appareil lorsqu’une récupération d’urgence est en cours. Vous pouvez uniquement supprimer votre appareil après que hello récupération d’urgence est terminée.

Q :    **Lorsque le garbage collection de hello ne démarre pas sur l’appareil source de hello afin que les données locales de hello sur l’appareil source sont supprimées ?**

R : Le garbage collection sera activé sur l’appareil source de hello uniquement après que l’appareil de hello est complètement nettoyé. nettoyage de Hello inclut le nettoyage des objets qui ont échoué sur périphérique source de hello tels que des volumes, des objets de sauvegarde (pas de données), des conteneurs de volumes et des stratégies.

Q : **Que se passe-t-il si hello supprimer le travail associé à des conteneurs de volumes hello dans l’appareil source de hello échoue ?**

R :  Si hello supprimer un travail échoue, vous devez toomanually suppression de hello déclencheur hello de conteneurs de volumes. Bonjour **périphériques** page, sélectionnez votre appareil source, cliquez sur **conteneurs de volumes**. Cliquez sur les conteneurs de volumes hello SELECT qui vous a échoué sur et en bas de hello de page de hello, **supprimer**. Une fois que vous avez supprimé tous les hello a échoué sur les conteneurs de volumes sur l’appareil source de hello, vous pouvez démarrer la restauration automatique hello.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Continuité d’activité et récupération d’urgence (Business Continuity Disaster Recovery - BCDR)
Un scénario de récupération d’urgence d’entreprise la continuité des activités se produit lorsque le centre de données Azure entier hello cesse de fonctionner. Cela peut affecter votre service StorSimple Manager et hello associés appareils StorSimple.

S’il existe des appareils StorSimple qui ont été inscrits juste avant un incident, ces appareils StorSimple peut-être tooundergo une réinitialisation. Après sinistre de hello, l’appareil StorSimple hello s’affichera comme étant hors connexion. l’appareil StorSimple Hello doit être supprimé à partir du portail de hello, et une réinitialisation des paramètres doit être effectuée, suivie d’une nouvelle inscription.

## <a name="next-steps"></a>Étapes suivantes
* Une fois que vous avez effectué un basculement, vous devrez peut-être trop[désactiver ou supprimer votre appareil StorSimple](storsimple-deactivate-and-delete-device.md).
* Pour plus d’informations sur la façon dont toouse hello StorSimple Manager service, accédez trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

