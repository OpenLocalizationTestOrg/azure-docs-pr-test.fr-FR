---
title: "aaaManage vos modèles de bande passante StorSimple | Documents Microsoft"
description: "Décrit comment des modèles de bande passante de StorSimple toomanage qui permettent de consommation de bande passante toocontrol."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0027b90e-91a5-437d-9bd0-06b05674aa5f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: 3f767e985667121e977106e7a1f8e5a3ad25f022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-bandwidth-templates"></a>Utiliser des modèles de bande passante du service toomanage StorSimple hello StorSimple Manager
## <a name="overview"></a>Vue d'ensemble
Modèles de bande passante vous permettent d’utilisation de la bande passante réseau tooconfigure dans plusieurs planifications de l’heure de tootier hello de données à partir de hello StorSimple appareil toohello cloud.

Avec les planifications de limitation de bande passante, vous pouvez :

* Spécifier des planifications personnalisées de la bande passante en fonction des utilisations de réseau de la charge de travail hello.
* Centraliser la gestion et réutiliser les planifications hello sur plusieurs périphériques de manière simple et transparente.

> [!NOTE]
> Cette fonctionnalité est disponible uniquement pour les appareils physiques StorSimple et pas pour les appareils virtuels.
> 
> 

Tous les modèles de bande passante hello pour votre service sont affichent dans un format tabulaire et contient hello informations suivantes :

* **Nom** : un modèle de bande passante toohello nom unique attribué lors de sa création.
* **Planification** – hello nombre de planifications contenues dans un modèle de bande passante donnée.
* **Utilisé par** – hello du nombre de volumes à l’aide de modèles de bande passante hello.

Vous utilisez le service StorSimple Manager hello **configurer** page Modèles de bande passante toomanage de portail classique Azure hello.

Vous pouvez également trouver des informations supplémentaires toohelp configurer des modèles de bande passante dans :

* Questions et réponses sur les modèles de bande passante
* Meilleures pratiques pour les modèles de bande passante

## <a name="add-a-bandwidth-template"></a>Ajouter un modèle de bande passante
Effectuer hello suivant les étapes toocreate un nouveau modèle de bande passante.

#### <a name="tooadd-a-bandwidth-template"></a>tooadd un modèle de bande passante
1. Sur hello service StorSimple Manager **configurer** , cliquez sur **Ajouter/modifier un modèle de bande passante**.
2. Bonjour **Ajouter/modifier un modèle de bande passante** boîte de dialogue :
   
   1. À partir de hello **modèle** la liste déroulante, sélectionnez **nouvel** tooadd un nouveau modèle de bande passante.
   2. Spécifiez un nom unique pour votre modèle de bande passante.
3. Définissez une **Planification de la bande passante**. toocreate une planification :
   
   1. À partir de la liste déroulante hello, choisissez jours hello de planification de hello hello semaine est configuré pour. Vous pouvez sélectionner plusieurs jours en sélectionnant les cases à cocher situées avant jours respectifs de hello dans la liste de hello hello.
   2. Sélectionnez hello **toute la journée** option si la planification de hello est appliquée pour la journée entière de hello. Lorsque cette option est cochée, vous ne pouvez plus spécifier une **Heure de début** ou une **Heure de fin**. planification de Hello s’exécute à partir de 12:00 AM too11 : 59 PM.
   3. Dans la liste déroulante hello, sélectionnez un **l’heure de début**. Il s’agit lors de la planification de hello commencera.
   4. Dans la liste déroulante hello, sélectionnez un **heure de fin**. C’est lors de la planification de hello s’arrête.
      
      > [!NOTE]
      > Les planifications qui se chevauchent ne sont pas autorisées. Si hello heures de début et de fin entraîne un chevauchement, vous verrez un effet de toothat message erreur.
      > 
      > 
   5. Spécifiez hello **taux de bande passante**. Il s’agit de la bande passante hello en mégabits par seconde (Mbits/s) utilisé par votre appareil StorSimple dans les opérations impliquant le cloud hello (téléchargements et téléchargements). Fournissez un nombre compris entre 1 et 1 000 pour ce champ.
   6. Cliquez sur une icône de coche hello ![coche](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png). modèle Hello que vous avez créé sera ajouté toohello la liste des modèles de bande passante sur le service de hello **configurer** page.
      
      ![Créer un modèle de bande passante](./media/storsimple-manage-bandwidth-templates/HCS_CreateNewBT1.png)
4. Cliquez sur **enregistrer** bas hello hello page, puis sur **Oui** lorsque vous êtes invité à confirmer l’opération. Cette action va enregistrer les modifications de configuration de hello que vous avez apportées.

## <a name="edit-a-bandwidth-template"></a>Modifier un modèle de bande passante
Effectuer hello suivant les étapes tooedit un modèle de bande passante.

### <a name="tooedit-a-bandwidth-template"></a>tooedit un modèle de bande passante
1. Cliquez sur **Ajouter/modifier des modèles de bande passante**.
2. Bonjour **Ajouter/modifier un modèle de bande passante** boîte de dialogue :
   
   1. À partir de hello **modèle** liste déroulante, sélectionnez une bande passante existante que vous souhaitez toomodify de modèle.
   2. Complétez vos modifications. (Vous pouvez modifier les paramètres existants de hello.)
   3. Cliquez sur une icône de coche hello ![Icône en forme de coche](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png). Vous verrez hello le modèle modifié dans la liste hello des modèles de bande passante sur la page de configuration de service hello.
3. toosave vos modifications, cliquez sur **enregistrer** bas hello de page de hello. Cliquez sur **Oui** lorsque vous êtes invité à confirmer l’opération.

> [!NOTE]
> Vous ne pas être autorisé toosave planifier de vos modifications si hello les planification modifiée chevauchement une existante dans le modèle de bande passante hello que vous modifiez.
> 
> 

## <a name="delete-a-bandwidth-template"></a>Supprimer un modèle de bande passante
Effectuer hello suivant les étapes toodelete un modèle de bande passante.

#### <a name="toodelete-a-bandwidth-template"></a>toodelete un modèle de bande passante
1. Dans hello tabulaire la liste des modèles de bande passante hello pour votre service, sélectionnez le modèle hello que vous souhaitez toodelete. Une icône de suppression (**x**) apparaîtra toohello extrême droite du modèle sélectionné de hello. Cliquez sur hello **x** modèle de hello toodelete icône.
2. Vous êtes invité à confirmer l’opération. Cliquez sur **OK** tooproceed.

Si le modèle de hello est en cours d’utilisation par un ou plusieurs volumes, vous ne pas être autorisé toodelete il. Vous verrez un message d’erreur indiquant que ce modèle hello est en cours d’utilisation. Une boîte de dialogue d’erreur message s’affiche vous indiquant que tous les modèles de toohello hello références doivent être supprimés.

Vous pouvez supprimer tous les modèles de toohello références hello en accédant à hello **conteneurs de volumes** page et la modification des conteneurs de volumes hello qui utilisent ce modèle afin qu’ils utilisent un autre modèle ou une bande de passante personnalisée ou illimitée paramètre. Lorsque toutes les références hello ont été supprimés, vous pouvez supprimer le modèle de hello.

## <a name="use-a-default-bandwidth-template"></a>Utiliser un modèle de bande passante par défaut
Un modèle de bande passante par défaut est fourni et est utilisé par les conteneurs de volumes par défaut tooenforce les contrôles de bande passante lors de l’accès hello cloud. modèle par défaut de Hello sert également de référence prête pour les utilisateurs qui créent leurs propres modèles. Hello les détails de ce modèle par défaut sont :

* **Nom** : nombre illimité de nuit et de week-ends
* **Planification** – une seule planification du lundi tooFriday qui applique un taux de bande passante de 1 Mbit/s entre 8 h 00 et 17 h 00 heure de l’appareil. la bande passante Hello a la valeur tooUnlimited pour reste hello de la semaine de hello.

modèle de Hello par défaut peut être modifié. l’utilisation de Hello de ce modèle (y compris les versions modifiées) est suivie.

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a>Créer un modèle de bande passante sur une journée entière qui commence à une heure spécifiée
Suivez cette procédure de toocreate une planification qui démarre à une heure spécifiée et exécute tous les jours. Dans l’exemple de hello, planification de hello commence à 9 heures matin de hello et s’exécute jusqu'à ce que hello de 9 : 00 lendemain matin. Il est important toonote qui hello début et heure de fin pour une planification donnée doit être contenues sur hello 24 heures planifier et ne peut pas couvrir plusieurs jours. Si vous avez besoin de tooset des modèles de bande passante qui s’étendent sur plusieurs jours, vous devez toouse plusieurs planifications (comme indiqué dans l’exemple de hello).

#### <a name="toocreate-an-all-day-bandwidth-template"></a>toocreate un modèle de bande passante sur une journée entière
1. Créer une planification qui commence à 9 heures matin de hello et s’exécute jusqu'à minuit.
2. Ajoutez une autre planification. Configurer hello deuxième planification toorun comprise entre minuit et se termine 9 heures matin de hello.
3. Enregistrez le modèle de bande passante hello.

planification composite de Hello puis démarre à la fois de votre choix et couvrira toute la journée.

## <a name="questions-and-answers-about-bandwidth-templates"></a>Questions et réponses sur les modèles de bande passante
**Q**. Que passe-t-il toobandwidth contrôles entre deux planifications de hello ? (Une planification est terminée et une autre n’a pas encore démarré).

**R**. Dans ce cas, aucun contrôle de bande passante n’est utilisé. Cela signifie que cet appareil hello peut utiliser une bande passante illimitée lors de la hiérarchisation des données toohello dans le cloud.

**Q**. Peut modifier les modèles de bande passante sur un périphérique hors connexion ?

**R**. Vous ne serez pas en mesure de toomodify des modèles de bande passante sur les conteneurs de volumes si l’unité de hello correspondante est hors connexion.

**Q**. Vous pouvez modifier un modèle de bande passante associé à un conteneur de volumes lorsque les volumes hello associé sont hors connexion ?

**R**. Vous pouvez modifier un modèle de bande passante associé à un conteneur de volumes dont les volumes associés sont hors connexion ? Notez que lorsque les volumes sont hors connexion, aucune donnée n’est transmise à partir de hello appareil toohello cloud.

**Q**. Peut-on supprimer un modèle par défaut ?

**R**. Mais vous pouvez supprimer un modèle par défaut, il n’est pas une bonne idée toodo donc. l’utilisation de Hello d’un modèle par défaut, y compris les versions modifiées, est suivie. Hello des données de suivi est analysé et fil hello temps, est le modèle par défaut de hello tooimprove utilisé.

**Q**. Comment déterminer que vos modèles de bande passante doivent toobe modifié ?

**R**. Un des hello signes que vous avez besoin de modèles de bande passante toomodify hello sont lorsque vous démarrez voir réseau de hello ralentissent ou être plusieurs fois par jour. Si cela se produit, analyse réseau de stockage et d’utilisation de hello en examinant les graphiques de performances d’e/s et le débit du réseau hello.

À partir des données de débit du réseau hello, identifiez les heure hello et hello conteneurs de volumes dans le hello goulot d’étranglement réseau se produit. Si cela se produit lorsque des données en nuage de toohello à plusieurs niveaux (obtenir ces informations à partir des performances d’e/s pour tous les conteneurs de volume pour le périphérique toocloud), vous devez les modèles de bande passante hello toomodify associés à vos conteneurs de volumes.

Une fois hello modifié les modèles sont en cours d’utilisation, vous devez réseau de hello toomonitor à nouveau pour déceler les latences importantes. Si celles-ci existent toujours, puis vous devez toorevisit vos modèles de bande passante.

**Q**. Que se passe-t-il si vous disposez de plusieurs conteneurs de volumes sur mon appareil planifications qui se chevauchent, mais des limites différentes s’appliquent tooeach ?

**R**. Supposons que vous disposiez d’un appareil avec 3 conteneurs de volumes. Hello planifications associées à ces conteneurs complètement se chevauchent. Pour chacun de ces conteneurs, les limites de bande passante hello utilisées sont respectivement 5, 10 et 15 Mbits/s. Lorsque les e/s se produisent sur l’ensemble de ces conteneurs de hello même temps, les limites de bande passante hello 3 au minimum hello peut être appliqué : dans ce cas, 5 Mbits/s en tant que ces sortant de partage de demandes d’e/s hello même file d’attente.

## <a name="best-practices-for-bandwidth-templates"></a>Meilleures pratiques pour les modèles de bande passante
Suivez ces meilleures pratiques pour votre appareil StorSimple :

* Configurer des modèles de bande passante sur votre appareil tooenable limitation variable du débit du réseau hello par périphérique de hello à différents moments de la journée de hello. Ces modèles de bande passante lorsqu’ils sont utilisés avec les planifications de sauvegarde peuvent exploiter efficacement une bande passante réseau supplémentaire pour les opérations de cloud pendant les heures creuses.
* Calculez la bande passante réelle hello requise pour un déploiement particulier en fonction de la taille de hello du déploiement de hello et hello requis temps de récupération (RTO).

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).

