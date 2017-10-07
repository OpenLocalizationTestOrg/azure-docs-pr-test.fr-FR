---
title: "aaaView et gérer les alertes de Microsoft Azure StorSimple Virtual Array | Documents Microsoft"
description: "Décrit les conditions d’alerte StorSimple Virtual Array et gravité, et comment toouse hello StorSimple Manager service toomanage alertes."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 97ee25a1-0ec3-4883-9a0a-54b722598462
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0fb5b1b9064f33df1d8fa7ace45f0d72b0a1622
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-alerts-for-hello-storsimple-virtual-array"></a>Utilisez le Gestionnaire de périphérique StorSimple toomanage des alertes pour hello StorSimple Virtual Array

## <a name="overview"></a>Vue d'ensemble

fonctionnalité d’alertes Hello Bonjour le Gestionnaire de périphériques StorSimple service offre un moyen pour vous tooreview et désactivez les alertes associées tooStorSimple tableaux virtuels en temps réel. Vous pouvez utiliser les alertes hello sur hello **récapitulatif du Service** panneau toocentrally surveiller les problèmes de contrôle d’intégrité hello de vos réseaux virtuels StorSimple et hello solution globale de Microsoft Azure StorSimple.

Ce didacticiel décrit comment tooconfigure des notifications d’alerte, conditions d’alerte courantes, les niveaux de gravité d’alerte et tooview et suivre les alertes. En outre, il inclut alerte référence rapide à des tables, qui permettent de vous tooquickly localiser une alerte spécifique et réagir de façon appropriée.

![Page des alertes](./media/storsimple-virtual-array-manage-alerts/alerts1.png)

## <a name="configure-alert-settings"></a>Configuration des paramètres d'alerte

Vous pouvez choisir si vous souhaitez que toobe averti par courrier électronique des conditions d’alerte hello pour chacun de vos réseaux virtuels StorSimple. En outre, vous pouvez identifier les autres destinataires de notification d’alerte en entrant leurs adresses de messagerie Bonjour **destinataires de courrier électronique supplémentaires** zone, séparés par des points-virgules.

> [!NOTE]
> Vous pouvez entrer un maximum de 20 adresses e-mail par tableau virtuel.


Après avoir activé la notification par courrier électronique pour un groupe virtuel, les membres de la liste de notification hello recevra un message électronique chaque fois qu’une alerte critique se produit. Hello messages seront envoyés à partir de  *storsimple-alerts-noreply@mail.windowsazure.com*  et décrivent la condition d’alerte hello. Destinataires peuvent cliquer sur **Unsubscribe** tooremove eux-mêmes à partir de la liste des notifications par courrier électronique hello.

#### <a name="tooenable-email-notification-for-alerts"></a>notification par courrier électronique de tooenable pour les alertes

1. Accédez tooyour le Gestionnaire de périphériques StorSimple service et Bonjour **gestion** section, puis cliquez sur **périphériques**. À partir d’appareils affichées la liste hello, sélectionnez et cliquez sur votre appareil.
   
    ![Paramètres d’alerte](./media/storsimple-virtual-array-manage-alerts/alerts2.png)
2. Cela ouvre hello **paramètres** panneau. Bonjour **paramètres de périphérique** section, sélectionnez **général**. Cela ouvre hello **paramètres généraux** panneau.
   
    ![configuration des notifications des alertes](./media/storsimple-virtual-array-manage-alerts/alerts4.png)
3. Bonjour **paramètres généraux** panneau, accédez trop**paramètres d’alerte** section et définir hello :
   
   1. Bonjour **activer la notification par courrier électronique** champ, sélectionnez **Oui**.
   2. Bonjour **administrateurs de service de messagerie** champ, sélectionnez **Oui** si vous le souhaitez administrateur de service toohave hello et tous les coadministrateurs reçoivent des notifications d’alerte hello.
   3. Bonjour **destinataires de courrier électronique supplémentaires** , entrez les adresses de messagerie hello de tous les autres destinataires qui doivent recevoir des notifications d’alerte hello. Entrez les noms au format de hello  *someone@somewhere.com* . Utiliser des adresses de messagerie des points-virgules tooseparate hello. Vous pouvez configurer un maximum de 20 adresses e-mail par appareil virtuel.
      
       ![configuration des notifications des alertes](./media/storsimple-virtual-array-manage-alerts/alerts6.png)
   4. toosend une notification par courrier électronique de test, cliquez sur **envoyer par courrier électronique de test**. Hello service du Gestionnaire de périphériques StorSimple affiche des messages d’état pendant qu’il transmet la notification de test hello.
      
       ![E-mail de notification de test des alertes envoyé](./media/storsimple-virtual-array-manage-alerts/alerts7.png)
      
      > [!NOTE]
      > Si hello test message de notification ne peut pas être envoyé, service du Gestionnaire de périphériques StorSimple hello affiche un message approprié. Cliquez sur **OK**, patientez quelques minutes, puis réessayez toosend votre message de notification de test.
      > 
      > 
   5. Au bas de hello de page de hello, cliquez sur **enregistrer** toosave votre configuration. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.
      
      ![E-mail de notification de test des alertes envoyé](./media/storsimple-virtual-array-manage-alerts/alerts10.png)

## <a name="common-alert-conditions"></a>Conditions d’alerte courantes

Votre StorSimple Virtual Array génère des alertes dans diverses tooa réponse conditions. Hello Voici les types courants de hello des États d’alerte :

* **Problèmes de connectivité** : ces alertes se produisent lorsque des difficultés surviennent dans le transfert de données. Problèmes de communication peuvent se produire pendant le transfert de données tooand de compte de stockage Azure hello ou échéance toolack de connectivité entre les périphériques virtuels hello et le service du Gestionnaire de périphériques StorSimple hello. Problèmes de communication sont des toofix plus difficile de hello, car il existe de nombreux points de défaillance. Vous devez toujours tout d’abord vérifier que les accès à Internet et la connectivité réseau sont disponibles avant de continuer sur toomore un dépannage avancé. Pour plus d’informations sur les ports et les paramètres de pare-feu, consultez trop[requise StorSimple Virtual Array](storsimple-ova-system-requirements.md). Pour vous aider à résoudre, accédez trop[dépannage avec l’applet de commande Test-Connection de hello](storsimple-troubleshoot-deployment.md).
* **Problèmes de performances** : ces alertes sont dues aux performances de votre système qui ne sont pas optimales, notamment lorsqu’il est soumis à des conditions de surcharge.

En outre, vous verrez toosecurity connexes des alertes, les mises à jour ou les échecs des tâches.

## <a name="alert-severity-levels"></a>Niveaux de gravité des alertes

Alertes ont différents niveaux de gravité, en fonction de l’impact de hello hello situation d’alerte et d’hello nécessaire pour une alerte toohello de réponse. niveaux de gravité Hello sont :

* **Critique** – cette alerte est en état de tooa de réponse qui affecte les performances de réussite hello de votre système. Action est requise tooensure que le service de StorSimple hello n’est pas interrompu.
* **Avertissement** : cette condition peut devenir critique si elle n’est pas résolue. Vous devez examiner hello situation et prendre n’importe quel problème de hello tooclear action requise.
* **Information** : cette alerte contient des informations qui peuvent être utiles pour le suivi et la gestion de votre système.

## <a name="view-and-track-alerts"></a>Afficher et effectuer le suivi des alertes

panneau Résumé du service Gestionnaire de périphériques StorSimple Hello vous donne un coup de œil au numéro hello d’alertes sur vos appareils virtuels, organisés par niveau de gravité.

![Tableau de bord des alertes](./media/storsimple-virtual-array-manage-alerts/alerts14.png)

Cliquez sur hello de tooopen au niveau de gravité hello **alertes** panneau. les résultats de Hello incluent uniquement les alertes de hello qui correspondent à ce niveau de gravité.

![Rapport d’alertes portée tooalert type](./media/storsimple-virtual-array-manage-alerts/alerts15.png)

Cliquez sur une alerte dans hello liste tooget des détails supplémentaires pour l’alerte hello, y compris hello heure de la dernière alerte de hello a été signalée, nombre de hello d’occurrences d’alerte hello sur l’appareil de hello et alerte de hello tooresolve hello action recommandée.

![Liste des alertes et détails](./media/storsimple-virtual-array-manage-alerts/alerts16.png)

Vous pouvez copier le fichier de texte tooa hello détails de l’alerte si vous avez besoin toosend hello informations tooMicrosoft prise en charge. Après avoir suivi les recommandations hello et résolu hello condition d’alerte locale, vous devez effacer l’alerte hello à partir de la liste de hello. Sélectionnez l’alerte de hello à partir de la liste de hello, puis cliquez **clair**. tooclear plusieurs alertes, sélectionnez chaque alerte, cliquez sur n’importe quelle colonne, à l’exception de hello **alerte** colonne, puis cliquez sur **clair** après avoir sélectionné tous les hello toobe alertes effacée.

Lorsque vous cliquez sur **clair**, vous aurez des commentaires de tooprovide d’opportunité hello sur l’alerte de hello et étapes hello que vous avez suivies tooresolve hello problème. 

![commentaires d’alerte](./media/storsimple-virtual-array-manage-alerts/alerts17.png)

Certains événements sont effacés par le système de hello si un autre événement est déclenché avec de nouvelles informations. 

## <a name="sort-and-review-alerts"></a>Tri et vérification des alertes

Hello **alertes** panneau peut afficher des alertes de too250. Si vous avez dépassé le nombre d’alertes, toutes les alertes seront affichera dans la vue par défaut de hello. Vous pouvez combiner hello suivant toocustomize champs les alertes sont affichées :

* **État** : vous pouvez afficher des alertes **Actives** ou **Effacées**. Alertes actives sont encore déclenchées sur votre système, tandis que les alertes effacées ont été effacées manuellement par un administrateur ou d’effacer par programmation, car le système de hello mis à jour la condition d’alerte hello avec de nouvelles informations.
* **Gravité** : vous pouvez afficher des alertes de tous les niveaux de gravité (critique, avertissement, information), ou seulement celles d’une certaine gravité, par exemple les alertes critiques uniquement.
* **Source** : vous pouvez afficher les alertes de toutes les sources, ou limiter hello alertes toothose provenant du service de hello ou un ou tous les hello périphériques virtuels.
* **Intervalle de temps** : en spécifiant hello **de** et **à** date et heure de création, vous pouvez examiner les alertes pendant hello laps de temps qui vous intéressez.

## <a name="alerts-quick-reference"></a>Référence rapide des alertes

Hello les tableaux suivants répertorie certaines des alertes hello StorSimple que vous pouvez rencontrer, ainsi que des recommandations et des informations supplémentaires lorsqu’elles sont disponibles. Les alertes StorSimple Virtual Array se répartissent dans hello suivant des catégories :

* [Alertes de connectivité au cloud](#cloud-connectivity-alerts)
* [Alertes de configuration](#configuration-alerts)
* [Alertes d'échec de tâche](#job-failure-alerts)
* [Alertes de performances](#performance-alerts)
* [Alertes de sécurité](#security-alerts)
* [Alertes de mise à jour](#update-alerts)

### <a name="cloud-connectivity-alerts"></a>Alertes de connectivité au cloud

| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| APPAREIL  *<device name>*  est pas connecté toohello cloud. |Hello nommé périphérique ne peut pas se connecter à toohello cloud. |Impossible de connecter toohello cloud. Cela peut être dû tooone suivants de hello :<ul><li>Il peut y avoir un problème avec les paramètres de réseau hello sur votre appareil.</li><li>Il peut y avoir un problème avec les informations d’identification de compte de stockage hello.</li></ul>Pour plus d’informations sur la résolution des problèmes de connectivité, accédez à toohello [interface utilisateur web locale](storsimple-ova-web-ui-admin.md) du périphérique de hello. |

### <a name="configuration-alerts"></a>Alertes de configuration

| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| La configuration d’un appareil virtuel local n’est pas prise en charge. |Performances lentes. |configuration actuelle de Hello peut entraîner une dégradation des performances. Assurez-vous que votre serveur répond aux exigences de la configuration minimale de hello. Pour plus d’informations, consultez trop[StorSimple Virtual Array exigences](storsimple-ova-system-requirements.md). |
| Vous n’avez presque plus d’espace disque approvisionné sur <*nom de l’appareil*>. |Avertissement d’espace disque. |Vous n’avez presque plus d’espace disque approvisionné. toofree d’espace, considérez le déplacement des charges de travail tooanother volume ou partage ou de la suppression des données. |

### <a name="job-failure-alerts"></a>Alertes d'échec de tâche

| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Impossible d’effectuer la sauvegarde de <*nom de l’appareil*>. |Échec du travail de sauvegarde. |Impossible de créer une sauvegarde. Tenez compte des valeurs hello suivantes :<ul><li>Problèmes de connectivité peuvent empêcher hello opération de sauvegarde réussie. Vérifiez qu’il n’existe aucun problème de connectivité. Pour plus d’informations sur la résolution des problèmes de connectivité, accédez à toohello [interface utilisateur web locale](storsimple-ova-web-ui-admin.md) pour votre appareil virtuel.</li><li>Vous avez atteint la limite de stockage disponible hello. toofree d’espace, supprimez toutes les sauvegardes qui ne sont plus nécessaires.</li></ul> Résoudre les problèmes de hello, désactivez l’alerte de hello et recommencez l’opération de hello. |
| Impossible d’effectuer le clonage de <*nom de l’appareil*>. |Échec du travail de clonage. |La création d’un clone a échoué. Tenez compte des valeurs hello suivantes :<ul><li>Votre liste de sauvegarde n’est peut-être pas valide. Actualiser hello tooverify de liste est toujours valide.</li><li>Problèmes de connectivité peuvent empêcher clonage hello à partir de l’achèvement. Vérifiez qu’il n’existe aucun problème de connectivité.</li><li>Vous avez atteint la limite de stockage disponible hello. toofree d’espace, supprimez toutes les sauvegardes qui ne sont plus nécessaires.</li></ul>Résoudre les problèmes de hello, désactivez l’alerte de hello et recommencez l’opération de hello. |

### <a name="performance-alerts"></a>Alertes de performances

| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Vous rencontrez des retards inattendus dans le transfert de données. |Transfert de données lent. |Erreurs de limitation se produisent quand vous dépassez les objectifs d’évolutivité hello d’un service de stockage. service de stockage Hello fait cette tooensure que sans un client ou un client peut utiliser hello service à des frais de hello d’autres personnes. Pour plus d’informations sur la résolution de votre compte de stockage Azure, consultez trop[moniteur, diagnostiquer et résoudre les problèmes de Microsoft Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md). |
| Vous n’avez presque plus d’espace disque de réservation locale sur <*nom de l’appareil*>. |Temps de réponse lent. |la taille approvisionnée pour nombre total de 10 % de hello <*nom de l’appareil*> est réservée sur hello appareil local et que vous êtes en train de manquer d’hello d’espace réservé. charge de travail Hello <*nom de l’appareil*> génère un degré plus élevé taux d’évolution du code ou que vous peut avoir migré récemment une grande quantité de données. Les performances peuvent s’en trouver réduites. Considérez l’une des hello suivants actions tooresolve cela :<ul><li>Augmentez l’unité de toothis hello cloud la bande passante.</li><li>Réduisez ou déplacez des charges de travail tooanother volume ou partage.</li></ul> |

### <a name="security-alerts"></a>Alertes de sécurité

| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Le mot de passe pour <*nom de l’appareil*> expirera dans <*nombre*> jours. |Avertissement de mot de passe. |Votre mot de passe expire dans <nombre> jours. Pensez à le changer. Pour plus d’informations, consultez trop[modification hello StorSimple Virtual Array administrateur mot de passe](storsimple-virtual-array-change-device-admin-password.md). |

### <a name="update-alerts"></a>Alertes de mise à jour

| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| De nouvelles mises à jour sont disponibles pour votre appareil. |Les mises à jour toohello StorSimple Virtual Array sont disponibles. |Vous pouvez installer les nouvelles mises à jour à partir de hello **Maintenance** page. |
| Impossible de rechercher de nouvelles mises à jour sur <*nom de l’appareil*>. |Échec de la mise à jour. |Une erreur s’est produite lors de l’installation de nouvelles mises à jour. Vous pouvez installer manuellement les mises à jour hello. Si hello problème persiste, contactez [Support technique de Microsoft](storsimple-contact-microsoft-support.md). |

## <a name="next-steps"></a>Étapes suivantes

* [En savoir plus sur hello StorSimple Virtual Array](storsimple-ova-overview.md).

