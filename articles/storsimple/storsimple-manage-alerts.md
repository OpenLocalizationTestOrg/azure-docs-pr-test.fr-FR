---
title: "aaaView et gérer les alertes StorSimple | Documents Microsoft"
description: "Décrit les conditions d’alerte StorSimple et gravité, comment tooconfigure des notifications d’alertes, et comment toouse hello StorSimple Manager service toomanage alertes."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bee49253-9ac7-4131-95f6-6bf0e72b8438
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: anbacker
ms.openlocfilehash: d322c88b565606538a3acb61ff939ec1fbe2f3cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-alerts"></a>Utilisez hello StorSimple Manager service tooview et gérer les alertes StorSimple
## <a name="overview"></a>Vue d'ensemble
Hello **alertes** onglet Bonjour service StorSimple Manager offre un moyen pour vous tooreview et désactivez les alertes StorSimple liée à un appareil en temps réel. Dans cet onglet, vous pouvez centraliser surveiller les problèmes de contrôle d’intégrité hello de vos appareils StorSimple et hello solution globale de Microsoft Azure StorSimple.

Ce didacticiel décrit les conditions courantes d’alerte, les niveaux de gravité d’alerte et comment tooconfigure des notifications d’alertes. En outre, il inclut alerte référence rapide à des tables, qui permettent de vous tooquickly localiser une alerte spécifique et réagir de façon appropriée.

![Page des alertes](./media/storsimple-manage-alerts/HCS_AlertsPage.png)

## <a name="common-alert-conditions"></a>Conditions d’alerte courantes
Votre appareil StorSimple génère des alertes dans diverses tooa réponse conditions. Hello Voici les types courants de hello des États d’alerte :

* **Problèmes liés au matériel** – ces alertes vous indiquent sur intégrité hello de votre matériel. Elles vous permettent de savoir si les mises à niveau des microprogrammes sont nécessaires, si une interface réseau rencontre des problèmes ou s'il existe un problème avec l’un de vos lecteurs de données.
* **Problèmes de connectivité** : ces alertes se produisent lorsque des difficultés surviennent dans le transfert de données. Problèmes de communication peuvent se produire pendant le transfert de données tooand de compte de stockage Azure hello ou échéance toolack de connectivité entre les appareils hello et le service StorSimple Manager hello. Problèmes de communication sont des toofix plus difficile de hello, car il existe de nombreux points de défaillance. Vous devez toujours tout d’abord vérifier que les accès à Internet et la connectivité réseau sont disponibles avant de continuer sur toomore un dépannage avancé. Pour vous aider à résoudre, accédez trop[dépannage avec l’applet de commande Test-Connection de hello](storsimple-troubleshoot-deployment.md).
* **Problèmes de performances** : ces alertes sont dues aux performances de votre système qui ne sont pas optimales, notamment lorsqu’il est soumis à des conditions de surcharge.

En outre, vous verrez toosecurity connexes des alertes, les mises à jour ou les échecs des tâches.

## <a name="alert-severity-levels"></a>Niveaux de gravité des alertes
Alertes ont différents niveaux de gravité, en fonction de l’impact de hello hello situation d’alerte et d’hello nécessaire pour une alerte toohello de réponse. niveaux de gravité Hello sont :

* **Critique** – cette alerte est en état de tooa de réponse qui affecte les performances de réussite hello de votre système. Action est requise tooensure que le service de StorSimple hello n’est pas interrompu.
* **Avertissement** : cette condition peut devenir critique si elle n’est pas résolue. Vous devez examiner hello situation et prendre n’importe quel problème de hello tooclear action requise.
* **Information** : cette alerte contient des informations qui peuvent être utiles pour le suivi et la gestion de votre système.

## <a name="configure-alert-settings"></a>Configuration des paramètres d'alerte
Vous pouvez choisir si vous souhaitez que toobe averti par courrier électronique des États d’alerte pour chacun de vos appareils StorSimple. En outre, vous pouvez identifier les autres destinataires de notification d’alerte en entrant leurs adresses de messagerie Bonjour **autres destinataires de courrier électronique** zone, séparés par des points-virgules.

> [!NOTE]
> Vous pouvez entrer un maximum de 20 adresses e-mail par appareil.
> 
> 

Après avoir activé la notification par courrier électronique pour un périphérique, les membres de la liste de notification hello recevra un message électronique chaque fois qu’une alerte critique se produit. Hello messages seront envoyés à partir de  *storsimple-alerts-noreply@mail.windowsazure.com*  et décrivent la condition d’alerte hello. Destinataires peuvent cliquer sur **Unsubscribe** tooremove eux-mêmes à partir de la liste des notifications par courrier électronique hello.

#### <a name="tooenable-email-notification-of-alerts-for-a-device"></a>notification par courrier électronique de tooenable d’alertes pour un appareil
1. Accédez trop**périphériques** > **configurer** pour appareil de hello.
2. Sous **paramètres d’alerte**, définir hello :
   
   1. Bonjour **envoyer une notification par courrier électronique** champ, sélectionnez **Oui**.
   2. Bonjour **administrateurs de service de messagerie** champ, sélectionnez **Oui** si vous le souhaitez administrateur de service toohave hello et tous les coadministrateurs reçoivent des notifications d’alerte hello.
   3. Bonjour **autres destinataires de courrier électronique** , entrez les adresses de messagerie hello de tous les autres destinataires qui doivent recevoir des notifications d’alerte hello. Entrez les noms au format de hello  *someone@somewhere.com* . Utiliser des adresses de messagerie des points-virgules tooseparate hello. Vous pouvez configurer un maximum de 20 adresses e-mail par appareil. 
      
       ![Configuration des notifications des alertes](./media/storsimple-manage-alerts/AlertNotify.png)
3. toosend une notification par courrier électronique de test, cliquez sur icône de flèche hello suivant trop**envoyer par courrier électronique de test**. Hello service StorSimple Manager affiche des messages d’état pendant qu’il transmet la notification de test hello. 
4. Hello message suivant s’affiche, cliquez sur **OK**. 
   
    ![E-mail de notification de test des alertes envoyé](./media/storsimple-manage-alerts/HCS_AlertNotificationConfig3.png)
   
   > [!NOTE]
   > Si hello message de notification de test ne peut pas être envoyé, hello service StorSimple Manager affichera un message approprié. Cliquez sur **OK**, patientez quelques minutes, puis réessayez toosend votre message de notification de test. 
   > 
   > 

## <a name="view-and-track-alerts"></a>Afficher et effectuer le suivi des alertes
tableau de bord de service Hello StorSimple Manager vous donne un coup de œil au numéro hello d’alertes sur vos appareils, organisés par niveau de gravité.

![Tableau de bord des alertes](./media/storsimple-manage-alerts/admin_alerts_dashboard.png)

Cliquez sur un niveau de gravité hello ouvre hello **alertes** résultats de hello onglet incluent uniquement les alertes de hello qui correspondent à ce niveau de gravité.

![Rapport d’alertes portée tooalert type](./media/storsimple-manage-alerts/admin_alerts_scoped.png)

En cliquant sur une alerte dans la liste de hello vous fournit des détails supplémentaires pour l’alerte de hello, y compris hello la dernière heure hello alerte a été signalée, hello nombre occurrences d’alerte hello sur le périphérique de hello et hello recommandé de tooresolve alerte hello. S’il s’agit d’une alerte matérielle, il identifie également le composant matériel hello.

![Exemple d'alerte de matériel](./media/storsimple-manage-alerts/admin_alerts_hardware.png)

Vous pouvez copier le fichier de texte tooa hello détails de l’alerte si vous avez besoin toosend hello informations tooMicrosoft prise en charge. Après avoir suivi les recommandations hello et résolu hello condition d’alerte locale, vous devez effacer l’alerte hello à partir de l’appareil de hello en sélectionnant l’alerte de hello Bonjour **alertes** onglet et en cliquant sur **effacer**. tooclear plusieurs alertes, sélectionnez chaque alerte, cliquez sur n’importe quelle colonne, à l’exception de hello **alerte** colonne, puis cliquez sur **clair** après avoir sélectionné tous les hello toobe alertes effacée. Notez que certaines alertes sont automatiquement désactivées lorsque hello problème est résolu ou lorsque le système de hello met à jour l’alerte de hello avec de nouvelles informations.

Lorsque vous cliquez sur **clair**, vous aurez des commentaires de tooprovide d’opportunité hello sur l’alerte de hello et étapes hello que vous avez suivies tooresolve hello problème. Certains événements sont effacés par le système de hello si un autre événement est déclenché avec de nouvelles informations. Dans ce cas, vous verrez hello message suivant.

![Message de suppression de l'alerte](./media/storsimple-manage-alerts/admin_alerts_system_clear.png)

## <a name="sort-and-review-alerts"></a>Tri et vérification des alertes
Il peut s’avérer plus efficace de rapports toorun sur les alertes afin que vous pouvez consulter et les effacer en groupes. En outre, hello **alertes** onglet peut afficher des alertes de too250. Si vous avez dépassé le nombre d’alertes, toutes les alertes seront affichera dans la vue par défaut de hello. Vous pouvez combiner hello suivant toocustomize champs les alertes sont affichées :

* **État** : vous pouvez afficher des alertes **Actives** ou **Effacées**. Alertes actives sont encore déclenchées sur votre système, tandis que les alertes effacées ont été effacées manuellement par un administrateur ou d’effacer par programmation, car le système de hello mis à jour la condition d’alerte hello avec de nouvelles informations.
* **Gravité** : vous pouvez afficher des alertes de tous les niveaux de gravité (critique, avertissement, information), ou seulement celles d’une certaine gravité, par exemple les alertes critiques uniquement.
* **Source** – vous pouvez afficher les alertes de toutes les sources, ou limiter hello alertes toothose provenant soit hello service ou à un ou tous les appareils hello.
* **Intervalle de temps** : en spécifiant hello **de** et **à** date et heure de création, vous pouvez examiner les alertes pendant hello laps de temps qui vous intéressez.

## <a name="alerts-quick-reference"></a>Référence rapide des alertes
Hello les tableaux suivants répertorie certaines des alertes Microsoft Azure StorSimple hello que vous pouvez rencontrer, ainsi que des recommandations et des informations supplémentaires lorsqu’elles sont disponibles. Alerte d’appareil StorSimple se répartissent dans hello suivant des catégories :

* [Alertes de connectivité au cloud](#cloud-connectivity-alerts)
* [Alertes de cluster](#cluster-alerts)
* [Alertes de récupération d'urgence](#disaster-recovery-alerts)
* [Alertes de matériel](#hardware-alerts)
* [Alertes d'échec de tâche](#job-failure-alerts)
* [Alertes de volume épinglé localement](#locally-pinned-volume-alerts)
* [Alertes de réseau](#networking-alerts)
* [Alertes de performances](#performance-alerts)
* [Alertes de sécurité](#security-alerts)
* [Alertes du package de prise en charge](#support-package-alerts)

### <a name="cloud-connectivity-alerts"></a>Alertes de connectivité au cloud
| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Connectivité trop <*nom des informations d’identification cloud*> ne peut pas être établie. |Impossible de connecter le compte de stockage toohello. |Il se peut qu'il y ait un problème de connectivité avec votre appareil. Exécutez hello `Test-HcsmConnection` applet de commande hello Interface Windows PowerShell pour StorSimple sur votre appareil tooidentify et résoudre les problème de hello. Si les paramètres de hello sont corrects, problème de hello peut être avec informations d’identification hello hello du compte de stockage pour lequel l’alerte de hello a été générée. Dans ce cas, utilisez hello `Test-HcsStorageAccountCredential` toodetermine d’applet de commande si des problèmes que vous pouvez résoudre.<ul><li>Vérifiez vos paramètres réseau.</li><li>Vérifiez les informations d’identification de votre compte de stockage.</li></ul> |
| Nous n’avons pas reçu une pulsation à partir de votre appareil pour hello dernière <*nombre*> minutes. |Impossible de se connecter toodevice. |Il semble qu'il y ait un problème de connectivité avec votre appareil. Utilisez hello `Test-HcsmConnection` applet de commande hello Interface Windows PowerShell pour StorSimple sur votre appareil tooidentify et résoudre les problème hello ou contactez votre administrateur réseau. |

### <a name="storsimple-behavior-when-cloud-connectivity-fails"></a>Comportement de StorSimple en cas d’échec de connexion au cloud
Que se passe-t-il en cas d'échec de connexion au cloud pour mon appareil StorSimple en cours d'exécution en production ?

En cas de connectivité cloud sur votre appareil de production de StorSimple, puis en fonction de l’état de hello de votre périphérique, suivant de hello peut se produire : 

* **Pour les données locales hello sur votre appareil**: pendant un certain temps, il n’y aura aucune interruption de service et les lectures continueront toobe pris en charge. Toutefois, comme nombre hello d’e/s en attente augmente et dépasse la limite, les lectures hello a pu démarrer toofail. 
  
    Selon la quantité de hello de données sur votre appareil, hello écrit également continue toooccur pour hello premières heures après une interruption hello de connectivité du cloud hello. écritures de Hello seront puis ralentir et éventuellement démarrer toofail si la connectivité de cloud hello est interrompue pendant plusieurs heures. (Il correspond au stockage temporaire sur l’appareil hello pour les données qui sont toobe envoyées toohello cloud. Cette zone est vidée lorsque les données hello sont envoyées. Si la connexion échoue, les données dans cette zone de stockage ne seront pas poussées toohello cloud et e/s ne pourra pas.)   
* **Pour les données dans le cloud de hello hello**: pour la plupart des erreurs de connectivité cloud, une erreur est retournée. Une fois que la connectivité de hello est rétablie, hello IOs sont repris sans hello utilisateur volume de hello toobring en ligne. Dans de rares cas, l’intervention de l’utilisateur peut être volume hello arrière toobring requis en ligne à partir de hello portail Azure classic. 
* **Pour les instantanés cloud en cours**: opération de hello est retentée plusieurs fois au sein de 4 à 5 heures et si la connectivité de hello n’est pas restaurée, les instantanés de cloud hello échouera.

### <a name="cluster-alerts"></a>Alertes de cluster
| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| L’appareil a basculé trop <*nom de l’appareil*>. |L’appareil est en mode Maintenance. |L’appareil a basculé en raison de tooentering ou le fait de quitter le mode maintenance. Ceci est normal et aucune action n'est nécessaire. Une fois que vous avez accepté cette alerte, effacez-la de la page des alertes hello. |
| L’appareil a basculé trop <*nom de l’appareil*>. |Le microprogramme ou le logiciel de l’appareil vient d’être mis à jour. |Un basculement de cluster en raison de la mise à jour tooan s’est produite. Ceci est normal et aucune action n'est nécessaire. Une fois que vous avez accepté cette alerte, effacez-la de la page des alertes hello. |
| L’appareil a basculé trop <*nom de l’appareil*>. |Le contrôleur a été arrêté ou redémarré. |Appareil a basculé, car le contrôleur actif de hello a été arrêté ou redémarré par un administrateur. Aucune action n'est nécessaire. Une fois que vous avez accepté cette alerte, effacez-la de la page des alertes hello. |
| L’appareil a basculé trop <*nom de l’appareil*>. |Basculement planifié. |Vérifiez qu’il s’agissait d’un basculement planifié. Une fois que vous avez pris les mesures appropriées, désactivez cette alerte à partir de la page des alertes hello. |
| L’appareil a basculé trop <*nom de l’appareil*>. |Basculement non planifié. |StorSimple est conçu tooautomatically les récupérer à partir de basculements non planifiés. Si vous voyez un grand nombre de ces alertes, contactez le Support Microsoft. |
| L’appareil a basculé trop <*nom de l’appareil*>. |Autre cause/cause inconnue. |Si vous voyez un grand nombre de ces alertes, contactez le Support Microsoft. Après avoir résolu le problème de hello, désactivez cette alerte à partir de la page des alertes hello. |
| Un service d’appareil critique indique l’état En échec. |Échec du service du chemin d’accès des données. |Contactez le Support Microsoft pour obtenir de l’assistance. |
| L’adresse IP virtuelle de l’interface réseau <*DONNÉES*> indique l’état en échec. |Autre cause/cause inconnue. |Les conditions temporaires peuvent parfois provoquer ces alertes. Si c’est le cas de hello, puis cette alerte est automatiquement supprimée après un certain temps. Si hello problème persiste, contactez le Support Microsoft. |
| L’adresse IP virtuelle de l’interface réseau <*DONNÉES*> indique l’état en échec. |Nom de l’interface : <*données #*> adresse IP <IP address> ne peut pas être mis en ligne, car une adresse IP dupliquée a été détectée sur le réseau de hello. |Assurez-vous que l’adresse IP dupliquée de hello est supprimée à partir du réseau de hello ou reconfigurer interface hello avec une autre adresse IP. |

### <a name="disaster-recovery-alerts"></a>Alertes de récupération d'urgence
| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Les opérations de récupération n’a pas pu restaurer tous les paramètres de hello pour ce service. Les données de configuration d’appareil sont dans un état incohérent pour certains appareils. |Incohérence de données détectée après la récupération d'urgence. |Les données chiffrées sur le service de hello ne sont pas synchronisées avec que sur l’appareil de hello. Autoriser l’appareil de hello <*nom de l’appareil*> StorSimple Manager toostart hello processus de synchronisation. Hello utilisez Interface Windows PowerShell pour StorSimple toorun hello `Restore-HcsmEncryptedServiceData` sur périphérique <*nom de l’appareil*> applet de commande, en fournissant ancien mot de passe hello comme une entrée toothis profil de sécurité d’applet de commande toorestore hello. Puis exécutez hello `Invoke-HcsmServiceDataEncryptionKeyChange` applet de commande tooupdate hello clé de chiffrement. Une fois que vous avez pris les mesures appropriées, désactivez cette alerte à partir de la page des alertes hello. |

### <a name="hardware-alerts"></a>Alertes de matériel
| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Le composant matériel <*ID composant*> indique l’état <*état*>. | |Les conditions temporaires peuvent parfois provoquer ces alertes. Dans ce cas, l’alerte est automatiquement effacée après un certain temps. Si hello problème persiste, contactez le Support Microsoft. |
| Dysfonctionnement du contrôleur passif. |contrôleur (secondaire) de Hello passif ne fonctionne pas. |Votre appareil est opérationnel, mais l’un de vos contrôleurs est défectueux. Essayez de redémarrer ce contrôleur. Si le problème de hello n’est pas résolu, contactez le Support Microsoft. |
| Panne de disque imminente détectée. | Panne de disque imminente détectée. |Nous avons détecté une défaillance imminente du lecteur pour le composant matériel hello ' lecteur dans l’emplacement <*ID d’emplacement*>, boîtier <*boîtier ID*>'. Envisagez de remplacer le disque. <br> Avant de commencer, remplacement de disque hello, passez en revue hello informations suivantes.<br><br>Si votre appareil a plusieurs disques défectueux, ne retirez jamais en même temps plusieurs disques SSD ou disques durs. Ceci peut entraîner la perte de données.<br><br>Veillez à placer un disque SSD de remplacement à un emplacement qui contenait auparavant un disque SSD. Hello même a la valeur true pour un disque dur.<br><br>Les emplacements sont numérotés de 0 too11. Un disque en panne dans l’emplacement 2 mappe tooa disque en panne dans l’emplacement 3 du périphérique de hello (à partir de hello haut à gauche).<br><br>Pour plus d’informations sur le remplacement de disque, consultez toohttps://go.microsoft.com/fwlink/?linkid=838653. Si le problème persiste, contactez le support technique Microsoft via https://go.microsoft.com/fwlink/?linkid=838654. |

### <a name="job-failure-alerts"></a>Alertes d'échec de tâche
| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Échec de la sauvegarde de <*ID du groupe de volumes source*>. |Échec de la sauvegarde de la tâche. |Problèmes de connectivité peuvent empêcher hello opération de sauvegarde réussie. S’il n’y a aucun problème de connectivité, il pouvez que vous avez atteint nombre maximal de hello de sauvegardes. Supprimer toutes les sauvegardes qui ne sont plus nécessaires et recommencez l’opération de hello. Une fois que vous avez pris les mesures appropriées, désactivez cette alerte à partir de la page des alertes hello. |
| Clonage de <*source ID d’élément de sauvegarde*> trop <*numéros de série de volume de destination*> a échoué. |Échec du clonage de la tâche. |Actualisation hello liste de sauvegarde tooverify qui hello sauvegarde est toujours valide. Si la sauvegarde de hello est valide, il est possible que les problèmes de connectivité au cloud empêchent hello clone opération de. S’il n’y a aucun problème de connectivité, vous avez peut-être atteint limite de stockage hello. Supprimer toutes les sauvegardes qui ne sont plus nécessaires et recommencez l’opération de hello. Après avoir pris des problème de hello tooresolve mesures appropriées, désactivez cette alerte à partir de la page des alertes hello. |
| Échec de la restauration de <*ID des éléments de sauvegarde source*>. |Échec de la restauration de la tâche. |Actualisation hello liste de sauvegarde tooverify qui hello sauvegarde est toujours valide. Si la sauvegarde de hello est valide, il est possible que les problèmes de connectivité au cloud empêchent hello restauration à partir de l’achèvement. S’il n’y a aucun problème de connectivité, vous avez peut-être atteint limite de stockage hello. Supprimer toutes les sauvegardes qui ne sont plus nécessaires et recommencez l’opération de hello. Après avoir pris des problème de hello tooresolve mesures appropriées, désactivez cette alerte à partir de la page des alertes hello. |

### <a name="locally-pinned-volume-alerts"></a>Alertes de volume épinglé localement
| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Échec de la création du volume local <*nom du volume*>. |Échec de la tâche de création de volume Hello. <*Code d’erreur d’échec de toohello correspondant du message erreur*>. |Problèmes de connectivité peuvent empêcher opération de création d’espace hello à partir de l’achèvement. Les volumes attachés localement sont approvisionnés et processus hello de création d’espace implique le débordement de cloud de toohello volumes hiérarchisés. S’il n’y a aucun problème de connectivité, vous avez peut-être épuisé hello local d’espace sur les appareils hello. Déterminer si les espace existe sur l’appareil de hello avant de recommencer cette opération. |
| Échec de l’expansion du volume local <*nom du volume*>. |travail de modification du volume Hello a échoué en raison de trop <*toohello correspondant du message erreur Échec de code d’erreur*>. |Problèmes de connectivité peuvent empêcher hello volume d’expansion opération. Les volumes attachés localement sont approvisionnés et processus hello d’étendre un espace existant hello implique le débordement de cloud de toohello volumes hiérarchisés. S’il n’y a aucun problème de connectivité, vous avez peut-être épuisé hello local d’espace sur les appareils hello. Déterminer si les espace existe sur l’appareil de hello avant de recommencer cette opération. |
| Échec de la conversion du volume <*nom de volume*>. |Échec de Hello volume travail tooconvert hello volume type de conversion à partir de tootiered attaché localement. |Conversion du volume de hello de tootiered de type attaché localement n’a pas pu aboutir. Assurez-vous qu’il n’y a aucun problème de connectivité empêche l’opération hello de s’exécuter correctement. Pour la résolution des problèmes de connectivité problèmes accédez trop[dépannage avec l’applet de commande Test-HcsmConnection de hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>volume de Hello d’origine attaché localement a maintenant été marquée comme un volume hiérarchisé, car certaines données hello à partir du volume de hello attaché localement a répandues toohello cloud lors de la conversion de hello. volume de hiérarchisé résultant Hello occupe toujours l’espace local sur l’appareil pour les volumes locaux futures hello qui ne peut pas être récupéré.<br>Résoudre les problèmes de connectivité, effacez l’alerte de hello et convertir cette tooensure de type de volume attaché localement d’origine volume arrière toohello toutes les données hello redevient disponible localement. |
| Échec de la conversion du volume <*nom de volume*>. |Hello conversion travail tooconvert hello volume type de volume de hiérarchisé toolocally épinglé a échoué. |Conversion du volume de hello du type hiérarchisé toolocally épinglé n’a pas pu aboutir. Assurez-vous qu’il n’y a aucun problème de connectivité empêche l’opération hello de s’exécuter correctement. Pour la résolution des problèmes de connectivité problèmes accédez trop[dépannage avec l’applet de commande Test-HcsmConnection de hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>volume hiérarchisé d’origine Hello désormais marqué comme un volume attaché localement comme partie du processus de conversion hello continue des données toohave résidant dans le cloud de hello, tandis que hello approvisionnés espace sur l’appareil hello pour ce volume peut n’est plus récupéré ultérieure local volumes.<br>Résoudre les problèmes de connectivité, alerte d’effacer hello et des convertir ce volume toohello arrière d’origine volume hiérarchisé type tooensure local espace approvisionné sur l’appareil de hello pouvant être récupérée. |
| Consommation d’espace local proche de sa limite pour les instantanés locaux du <*nom du groupe de volumes*> |Instantanés locaux pour la stratégie de sauvegarde hello peuvent bientôt manquer d’espace et être invalidé tooavoid échecs d’écriture hôte. |Instantanés locaux fréquents conjugués à une évolution importante des données dans les volumes hello sont associés à ce groupe de stratégie de sauvegarde sont à l’origine un espace local sur hello appareil toobe est consommé rapidement. Supprimez les instantanés locaux qui ne sont plus nécessaires. En outre, mettre à jour vos planifications des instantanés locaux pour cette tootake de stratégie de sauvegarde moins fréquents instantanés locaux et que les instantanés cloud soient pris régulièrement. Si ces actions ne sont pas prises, espace local pour ces instantanés est peut-être bientôt épuisé et système de hello sera automatiquement les supprimer tooensure écritures de l’hôte continuer toobe traité avec succès. |
| Les instantanés locaux du <*nom du groupe de volumes*> ont été invalidés. |Hello instantanés locaux pour <*nom groupe de volumes*> ont été invalidés et ensuite supprimé, car ils ont été supérieure à un espace local sur l’appareil de hello hello. |tooensure ne se répète pas Bonjour future, passez en revue les planifications des instantanés locaux hello pour cette stratégie de sauvegarde et supprimez les instantanés locaux qui ne sont plus nécessaires. Instantanés locaux fréquents conjugués à une évolution importante des données dans les volumes hello sont associés à ce groupe de stratégie de sauvegarde font que l’espace local sur hello appareil toobe est consommé rapidement. |
| Échec de la restauration de <*ID des éléments de sauvegarde source*>. |travail de restauration Hello a échoué. |Si vous avez attaché localement ou un mélange de volumes localement épinglés et à plusieurs niveaux dans la stratégie de sauvegarde, actualisation hello liste de sauvegarde tooverify qui hello sauvegarde est toujours valide. Si la sauvegarde de hello est valide, il est possible que les problèmes de connectivité au cloud empêchent hello restauration à partir de l’achèvement. Hello localement épinglé des volumes qui ont été restaurées comme partie de ce groupe de capture instantanée n’ont pas toutes de leur appareil toohello téléchargé de données et, si vous avez un mélange de volumes attachés localement et hiérarchisés dans ce groupe de capture instantanée, ils ne seront pas synchronisés entre eux. toosuccessfully terminer l’opération de restauration hello, prendre des volumes de hello dans ce groupe hors connexion sur l’ordinateur hôte de hello et recommencez l’opération de restauration hello. Notez que toutes les données de volume de toohello de modifications qui ont été effectuées au cours de hello des processus de restauration seront perdue. |

### <a name="networking-alerts"></a>Alertes de réseau
| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Impossible de démarrer les services StorSimple. |Erreur de chemin d’accès des données |Si hello problème persiste, contactez le Support Microsoft. |
| Adresse IP en double détectée pour « Data0 ». | |système de Hello a détecté un conflit d’adresse IP '10.0.0.1'. Hello 'Data0' de la ressource réseau sur l’appareil de hello  *<device1>*  est hors connexion. Assurez-vous que cette adresse IP n’est pas utilisée par une autre entité de ce réseau. tootroubleshoot des problèmes de réseau, accédez trop[dépannage avec l’applet de commande Get-NetAdapter de hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). Pour obtenir de l’aide sur la résolution de ce problème, contactez votre administrateur réseau. Si hello problème persiste, contactez le Support Microsoft. |
| Adresse IPv4 (ou IPv6) de « Data0 » hors connexion. | |ressource de réseau Hello « Data0 » avec l’adresse IP '10.0.0.1.' le préfixe de longueur '22' sur l’appareil de hello  *<device1>*  est hors connexion. Assurez-vous que toowhich de ports de commutateur hello cette interface est connectée sont opérationnels. tootroubleshoot des problèmes de réseau, accédez trop[dépannage avec l’applet de commande Get-NetAdapter de hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). |

### <a name="performance-alerts"></a>Alertes de performances
| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Hello charge de l’appareil a dépassé <*seuil*>. |Plus lent que le temps de réponse attendu. |Votre appareil indique que l'utilisation d'entrée/sortie est surchargée. Cela peut entraîner votre travail de toonot appareil ainsi comme il le devrait. Passez en revue les charges de travail hello que vous avez connecté toohello périphérique et déterminez s’il existe un qui peut être déplacée tooanother appareil ou qui ne sont plus nécessaires.<br>toounderstand hello actuels, accédez trop[utilisation hello toomonitor du service StorSimple Manager de votre appareil](storsimple-monitor-device.md) |

### <a name="security-alerts"></a>Alertes de sécurité
| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| La session du Support Microsoft a commencé. |Session du support accédée par des tiers. |Veuillez confirmer que cet accès est autorisé. Une fois que vous avez pris les mesures appropriées, désactivez cette alerte à partir de la page des alertes hello. |
| Le mot de passe pour <*élément*> arrivera à expiration dans <*période de temps*>. |L’expiration du mot de passe est proche. |Modifiez votre mot de passe avant son expiration. |
| Les informations de configuration de sécurité sont manquantes pour <*ID de l’élément*>. | |Hello volumes associés à ce conteneur de volume ne peut pas être utilisé tooreplicate votre configuration StorSimple. tooensure que vos données sont stockées en sécurité, nous vous recommandons de supprimer conteneur de volume hello et tous les volumes associés au conteneur de volume hello. Une fois que vous avez pris les mesures appropriées, désactivez cette alerte à partir de la page des alertes hello. |
| Échec de <*nombre*> tentatives de connexion pour <*ID de l’élément*>. |Échec de plusieurs tentatives de connexion. |Votre appareil peut être attaque ou un utilisateur non autorisé tente de tooconnect avec un mot de passe incorrect.<ul><li>Contactez vos utilisateurs autorisés et vérifiez que ces tentatives proviennent d’une source légitime. Si vous continuez toosee un grand nombre de tentatives de connexion ayant échoué, envisagez de désactiver la gestion à distance et contactez votre administrateur réseau. Une fois que vous avez pris les mesures appropriées, désactivez cette alerte à partir de la page des alertes hello.</li><li>Vérifiez que votre gestionnaire d’instantanés sont configurées avec le mot de passe correct hello. Une fois que vous avez pris les mesures appropriées, désactivez cette alerte à partir de la page des alertes hello.</li></ul>Pour plus d’informations, consultez trop[modifier un mot de passe expiré](storsimple-snapshot-manager-manage-devices.md#change-an-expired-device-password). |
| Un ou plusieurs échecs s’est produite lors du changement de clé de chiffrement de données de service hello. | |Erreurs se sont produites lors de la modification de clé de chiffrement de données de service hello. Après vous être occupé des conditions d’erreur hello, exécutez hello `Invoke-HcsmServiceDataEncryptionKeyChange` hello Interface Windows PowerShell pour StorSimple sur votre service de hello tooupdate appareil applet de commande. Si ce problème persiste, contactez le support technique Microsoft. Après avoir résolu le problème de hello, désactivez cette alerte à partir de la page des alertes hello. |

### <a name="support-package-alerts"></a>Alertes du package de prise en charge
| Texte d'alerte | Événement | Plus d'informations/actions recommandées |
|:--- |:--- |:--- |
| Échec de la création du package de prise en charge. |StorSimple n’a pas pu générer le package de hello. |Retentez l'opération. Si hello problème persiste, contactez le Support Microsoft. Une fois que vous avez résolu le problème de hello, désactivez cette alerte à partir de la page des alertes hello. |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les [erreurs de StorSimple et la résolution des problèmes d’un appareil opérationnel](storsimple-troubleshoot-operational-device.md).

