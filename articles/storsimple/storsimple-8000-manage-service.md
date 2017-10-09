---
title: "aaaDeploy hello service Gestionnaire de périphériques StorSimple dans Azure | Documents Microsoft"
description: "Explique comment toocreate et delete hello service Gestionnaire de périphériques StorSimple Bonjour portail Azure et décrit comment toomanage hello clé d’inscription de service."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>Déployer le service du Gestionnaire de périphériques StorSimple hello pour les unités StorSimple 8000 series

## <a name="overview"></a>Vue d'ensemble

Hello le Gestionnaire de périphériques StorSimple service s’exécute dans Microsoft Azure et connecte les appareils StorSimple toomultiple. Après avoir créé le service de hello, vous pouvez utiliser il toomanage tous les périphériques hello connecté toohello StorSimple le Gestionnaire de périphériques de service à partir d’un emplacement unique et centralisé, réduisant les tâches administratives.

Ce didacticiel décrit les étapes de hello requis pour la création de hello, la suppression, la migration du service de hello et la gestion de hello de clé d’inscription de service hello. les informations de Hello contenues dans cet article sont applicable uniquement tooStorSimple 8000 series pour les appareils. Pour plus d’informations sur les réseaux virtuels StorSimple, consultez trop[déployer un service StorSimple le Gestionnaire de périphériques de votre tableau virtuel StorSimple](storsimple-virtual-array-manage-service.md).

## <a name="create-a-service"></a>Créer un service
toocreate un service Gestionnaire de périphériques StorSimple, vous devez toohave :

* Un abonnement avec un contrat Entreprise
* Un compte de stockage Microsoft Azure actif
* informations de facturation sont utilisées pour la gestion de l’accès de Hello

Hello uniquement les abonnements avec un contrat entreprise sont autorisés. Hello portail Azure ne prend pas en charge les abonnements Microsoft Sponsorship qui étaient autorisées dans hello portail Azure classic. Vous verrez hello message suivant lors de l’utilisation d’un abonnement non pris en charge :

![Abonnement non valide](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

Vous pouvez également choisir de toogenerate un compte de stockage par défaut lorsque vous créez le service de hello.

Un seul service peut gérer plusieurs appareils. Cependant, un appareil ne peut pas couvrir plusieurs services. Une grande entreprise peut avoir plusieurs toowork d’instances de service avec différents abonnements, organisations ou emplacements de déploiement. 

> [!NOTE]
> Vous avez besoin des instances distinctes d’unités de gestionnaire de périphériques StorSimple service toomanage StorSimple 8000 series et les tableaux de virtuel StorSimple.

Effectuer hello suivant les étapes toocreate un service.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


Pour chaque service de gestionnaire de périphériques StorSimple, hello suivant d’attributs existe :

* **Nom** – nom hello attribué tooyour le Gestionnaire de périphériques StorSimple service lorsqu’il a été créé. **Impossible de modifier le nom du service Hello après que hello service est créé. Cela vaut également pour les autres entités telles que des appareils, des volumes, des conteneurs de volumes et des stratégies de sauvegarde ne peut pas être renommées dans hello portail Azure.**
* **État** – hello l’état du service hello, qui peut être **Active**, **création**, ou **Online**.
* **Emplacement** – hello emplacement géographique dans le hello StorSimple appareil sera déployé.
* **Abonnement** : hello abonnement associé à votre service de facturation.

## <a name="move-a-service-tooazure-portal"></a>Déplacer un portail tooAzure
Série StorSimple 8000 peut être gérés maintenant Bonjour portail Azure. Si vous avez un service toomanage hello StorSimple les périphériques existants, nous vous recommandons de déplacer votre toohello service portail Azure. Hello portail classique Azure pourquoi le service StorSimple Manager n’est pas disponible après 30 septembre 2017.

Hello option toomigrate toohello portail Azure est disponible en plusieurs phases. Si vous ne voyez pas un portail de tooAzure toomigrate option, mais que vous souhaitez toomove et que vous avez consulté impact hello de migration décrites dans hello [considérations relatives à la transition](#considerations-for-transition), vous pouvez [soumettre une demande de](https://aka.ms/ss8000-cx-signup).

### <a name="considerations-for-transition"></a>Considérations relatives à la transition

Vérifiez l’impact hello de migration toohello nouveau portail Azure avant de déplacer les service hello.

#### <a name="before-you-transition"></a>Avant la transition

* Votre appareil exécute Update 3.0 ou version ultérieure. Si votre appareil exécute une version antérieure, installez les dernières mises à jour de hello. Pour plus d’informations, consultez trop[installer une mise à jour 4](storsimple-8000-install-update-4.md). Si vous utilisez StorSimple Cloud Appliance (8010/8020), créez une appliance cloud avec Update 4.0. 

* Une fois que vous êtes passé toohello de nouveau portail Azure, vous ne pouvez pas utiliser votre appareil StorSimple hello toomanage de portail classique Azure.

* transition de Hello est sans interruption de service et il n’existe aucun temps d’arrêt pour appareil de hello.

* Tous les gestionnaires d’appareil StorSimple hello sous hello spécifié abonnement sont transférées.

#### <a name="during-hello-transition"></a>Au cours de la transition de hello

* Vous ne pouvez pas gérer votre appareil à partir du portail de hello.
* Opérations, telles que les sauvegardes planifiées et de hiérarchisation continuent toooccur.
* Ne supprimez pas hello ancien gestionnaires d’appareil StorSimple pendant la transition de hello.

#### <a name="after-hello-transition"></a>Après la transition de hello

* Vous ne pouvez plus gérer vos appareils à partir du portail classique de hello.

* applets de commande PowerShell de gestion de Service Azure (ASM) existantes Hello ne sont pas pris en charge. Mettre à jour hello scripts toomanage vos appareils via hello Azure Resource Manager.

* La configuration de votre service et de votre appareil est conservée. Tous les volumes et les sauvegardes sont également passé toohello portail Azure.

### <a name="begin-transition"></a>Commencer la transition

Effectuer hello suivant les étapes tootransition votre toohello service portail Azure.

1. Accédez à tooyour le service StorSimple Manager existant dans le portail classique de hello.

2. Vous voyez une notification qui vous informe que service du Gestionnaire de périphériques StorSimple hello est désormais disponible dans hello portail Azure. Notez que dans hello portail Azure, service de hello est référencé tooas service du Gestionnaire de périphériques StorSimple.

    ![Notification de la migration](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. Vérifiez que vous avez consulté impact hello de la migration.
    2. Passez en revue la liste hello de gestionnaires de périphériques StorSimple qui seront déplacées à partir du portail classique de hello.

3. Cliquez sur **Migrer**. transition de Hello commence et prend quelques minutes toocomplete.

Une fois la transition de hello est terminée, vous pouvez gérer vos appareils via hello service Gestionnaire de périphériques StorSimple Bonjour portail Azure.

Bonjour portail Azure, hello uniquement les appareils StorSimple 3.0 de la mise à jour en cours d’exécution et une version ultérieure sont pris en charge. prise en charge les périphériques de Hello qui exécutent des versions antérieures est limitée. Hello suivant summrizes table quelles opérations sont prises en charge sur l’appareil hello en cours d’exécution tooUpdate préalable de versios 3.0, une fois que vous avez migré à partir de toohello classique de hello portail Azure.

| Opération                                                                                                                       | Pris en charge      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| Inscrire un appareil                                                                                                               | Oui            |
| Configurer les paramètres d’un appareil, tels que les paramètres généraux, réseau et de sécurité                                                                | Oui            |
| Analyser, télécharger et installer des mises à jour                                                                                             | Oui            |
| Désactiver un appareil                                                                                                               | Oui            |
| Supprimer un appareil                                                                                                                   | Oui            |
| Créer, modifier et supprimer un conteneur de volumes                                                                                   | Non             |
| Créer, modifier et supprimer un volume                                                                                             | Non             |
| Créer, modifier et supprimer une stratégie de sauvegarde                                                                                      | Non             |
| Exécuter une sauvegarde manuelle                                                                                                            | Non             |
| Exécuter une sauvegarde planifiée                                                                                                         | Non applicable |
| Restaurer à partir d’un jeu de sauvegarde                                                                                                        | Non             |
| Cloner le périphérique tooa mise à jour en cours d’exécution 3.0 et versions ultérieures <br> Appareil de Hello source est en cours d’exécution tooUpdate préalable de version 3.0.                                | Oui            |
| Cloner le périphérique tooa tooUpdate de précédentes versions 3.0 en cours d’exécution                                                                          | Non             |
| Basculer en tant qu’appareil source <br> (à partir d’un appareil exécute version antérieure tooUpdate 3.0 tooa appareil est en cours d’exécution Update 3.0 et versions ultérieures)                                                               | Oui            |
| Basculer en tant qu’appareil cible <br> (appareil tooa préalable tooUpdate 3.0 de la version des logiciels en cours d’exécution)                                                                                   | Non             |
| Supprimer une alerte                                                                                                                  | Oui            |
| Afficher les stratégies de sauvegarde, le catalogue de sauvegarde, les volumes, les conteneurs de volumes, les graphiques de surveillance, les travaux et les alertes créés dans le portail classique | Oui            |
| Activer et désactiver des contrôleurs d’appareils                                                                                              | Oui            |


## <a name="delete-a-service"></a>Supprimer un service

Avant de supprimer un service, assurez-vous qu’aucun appareil connecté ne l’utilise. Si le service de hello est en cours d’utilisation, désactiver les périphériques de hello connecté. Hello désactiver l’opération sera le serveur de connexion hello entre l’appareil de hello et service de hello, mais conserver les données d’appareil hello dans le cloud de hello.

> [!IMPORTANT]
> Après la suppression d’un service, opération de hello ne peut pas être annulée. N’importe quel appareil qui utilise hello service doit toobe paramètres toofactory par défaut avant de pouvoir être utilisé avec un autre service. Dans ce scénario, les données locales de hello sur le périphérique de hello, ainsi que la configuration de hello, sont perdues.

Effectuer hello suivant les étapes toodelete un service.

### <a name="toodelete-a-service"></a>toodelete un service

1. Recherche de service de hello souhaité toodelete. Cliquez sur **ressources** puis entrée et l’icône hello toosearch de conditions appropriées. Dans les résultats de recherche hello, cliquez sur le service hello toodelete.

    ![Toodelete de service de recherche](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. Vous accédez Panneau de service de gestionnaire de périphériques StorSimple toohello. Cliquez sur **Supprimer**.

    ![Suppression du service](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. Cliquez sur **Oui** dans la notification de confirmation hello. Il peut prendre quelques minutes pour hello service toobe est supprimé.

    ![Confirmer la suppression](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a>Obtenir la clé d’inscription hello

Une fois que vous avez créé un service, vous devez tooregister votre appareil StorSimple hello service. tooregister votre premier appareil StorSimple, vous devez serez hello clé d’inscription de service. tooregister autres périphériques avec un service StorSimple existant, vous devez la clé d’enregistrement hello et hello clé de chiffrement (qui est généré sur le premier périphérique de hello lors de l’inscription). Pour plus d’informations sur la clé de chiffrement de données de service hello, consultez [sécurité StorSimple](storsimple-8000-security.md). Vous pouvez obtenir la clé d’inscription de hello en accédant à **clés** sur le panneau de votre gestionnaire de périphériques StorSimple.

Effectuer hello après la clé d’inscription étapes tooget hello.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Conservez la clé d’inscription hello dans un emplacement sûr. Vous devez cette clé, comme clé de chiffrement de données de service de hello, tooregister des appareils supplémentaires auprès de ce service. Après avoir obtenu la clé d’inscription hello, vous devez configurer votre appareil via hello Windows PowerShell pour StorSimple interface.

Pour plus d’informations sur la façon de toouse cette clé, pour identifier l’enregistrement [étape 3 : configurer et inscrire l’appareil hello via Windows PowerShell pour StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Régénérer la clé d’inscription hello
Vous devez tooregenerate une clé d’inscription de service si vous êtes tooperform requis la rotation des clés ou si la liste hello des administrateurs de service a changé. Lorsque vous régénérez la clé de hello, clé hello est utilisé uniquement pour l’inscription des appareils suivants. appareils Hello déjà inscrites ne sont pas affectés par ce processus.

Effectuer hello suivant les étapes tooregenerate une clé d’inscription de service.

### <a name="tooregenerate-hello-service-registration-key"></a>clé d’inscription tooregenerate hello
1. Bonjour **le Gestionnaire de périphériques StorSimple** panneau, accédez trop**gestion &gt;**  **clés**.
    
    ![Panneau Clés](./media/storsimple-8000-manage-service/regenregkey2.png)

2. Bonjour **clés** panneau, cliquez sur **régénérer**.

    ![Cliquer sur Régénérer](./media/storsimple-8000-manage-service/regenregkey3.png)
3. Bonjour **clé d’inscription régénérer** panneau, révision hello action requise lorsque hello les clés sont régénérées. Tous les périphériques suivants hello qui sont inscrits auprès de ce service utilisent la nouvelle clé d’inscription de hello. Cliquez sur **régénérer** tooconfirm. Vous êtes averti une fois la régénération de hello est terminée.

    ![Confirmer la régénération](./media/storsimple-8000-manage-service/regenregkey4.png)

4. Une nouvelle clé d’inscription du service s’affiche.

5. Copiez cette clé et sauvegardez-la pour enregistrer tout nouvel appareil auprès de ce service.



## <a name="change-hello-service-data-encryption-key"></a>Modifier la clé de chiffrement de données de service hello
Clés de chiffrement de données de service sont des données client confidentielles tooencrypt utilisés, tels que les informations d’identification compte stockage qui sont envoyées à partir de votre appareil de StorSimple de toohello service StorSimple Manager. Vous devez toochange ces clés périodiquement si votre organisation a une stratégie de rotation des clés sur les périphériques de stockage hello. Hello processus de modification de la clé peut être légèrement différente selon qu’il existe un ou plusieurs périphériques gérés par hello service StorSimple Manager. Pour plus d’informations, consultez trop[StorSimple sécurité et protection des données](storsimple-8000-security.md).

Modification hello clé de chiffrement est un processus en 3 étapes :

1. À l’aide de scripts Windows PowerShell pour Azure Resource Manager, d’autoriser une périphérique toochange hello clé de chiffrement.
2. À l’aide de Windows PowerShell pour StorSimple, de lancer le changement de clé de chiffrement de hello service données.
3. Si vous avez plusieurs périphériques StorSimple, mettre à jour hello clé de chiffrement sur hello autres périphériques.

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a>Étape 1 : Utiliser Windows PowerShell script tooAuthorize une clé de chiffrement des données de service appareil toochange hello
En règle générale, administrateur du périphérique hello demande qu’administrateur de service hello autoriser un clés de chiffrement de données de périphérique toochange service. administrateur de service Hello autorise ensuite clé de hello périphérique toochange hello.

Cette étape est effectuée à l’aide du script de base Azure Resource Manager hello. administrateur du service Hello peut sélectionner un périphérique qui est éligible toobe autorisé. Appareil de Hello est le processus de modification de clé de chiffrement de données autorisés toostart hello service. 

Pour plus d’informations sur l’utilisation de script de hello, accédez trop[ServiceEncryptionRollover.ps1-autoriser](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Les appareils qui peuvent être autorisés des clés de chiffrement de données de service toochange ?
Un appareil doit respecter hello suivant des critères avant de pouvoir être changements de chiffrement de données service tooinitiate autorisés clés :

* Appareil de Hello doit être en ligne toobe éligible pour l’autorisation de modification de la clé de chiffrement de données service.
* Vous pouvez autoriser hello même périphérique à nouveau après 30 minutes si la modification de la clé de hello n’a pas démarré.
* Vous pouvez autoriser un autre appareil, pour autant que la modification de la clé hello n’a pas été initialisée par périphérique précédemment autorisé de hello. Une fois le nouveau périphérique de hello a été autorisé, hello ancienne ne peut plus lancer les modifications hello.
* Vous ne pouvez pas autoriser un périphérique lors de la substitution de hello de clé de chiffrement de données de service hello est en cours.
* Vous pouvez autoriser un périphérique lorsque certains périphériques hello inscrits avec le service de hello ont annulées via le chiffrement hello tandis que d’autres pas. 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Étape 2 : Utiliser Windows PowerShell pour StorSimple tooinitiate hello service modification chiffrement des données clée
Cette étape s’effectue dans hello Windows PowerShell pour StorSimple interface hello autorisé de l’appareil StorSimple.

> [!NOTE]
> Aucun opérations ne peuvent être effectuées dans hello portail Azure de votre service StorSimple Manager avant la fin de la substitution de clé hello.
> 
> 

Si vous utilisez l’interface Windows PowerShell de hello appareil console série tooconnect toohello, effectuer hello comme suit.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>modification de la clé de chiffrement des données tooinitiate hello service
1. Sélectionnez l’option 1 toolog sur avec un accès complet.
2. À l’invite de commandes hello, tapez :
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Une fois que l’applet de commande hello terminé, vous obtenez une nouvelle clé de chiffrement de données de service. Copiez et enregistrez cette clé pour l’utiliser lors de l’étape 3 de cette procédure. Cette clé sera utilisée tooupdate tous les hello restant appareils inscrits avec le service StorSimple Manager hello.
   
   > [!NOTE]
   > Ce processus doit être démarré dans les quatre heures suivant l’autorisation d’un appareil StorSimple.
   > 
   > 
   
   Cette nouvelle clé est ensuite envoyée toohello toobe envoyée tooall hello périphériques de service qui sont inscrits avec le service de hello. Une alerte apparaîtront dans le tableau de bord de service hello. Hello service désactive toutes les opérations de hello sur les appareils inscrits de hello et administrateur de l’appareil hello puis devez tooupdate hello clé de chiffrement sur hello autres périphériques. Toutefois, hello e/s (hôtes expédiant des données dans le cloud toohello) ne seront pas interrompues.
   
   Si vous avez un seul appareil inscrit tooyour service, les processus de substitution hello sont maintenant terminée et vous pouvez ignorer la prochaine étape de hello. Si vous avez plusieurs service inscrit tooyour de périphériques, passez toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Étape 3 : Mettre à jour la clé de chiffrement de données de service hello sur d’autres appareils StorSimple
Ces étapes doivent être effectuées dans l’interface Windows PowerShell de votre appareil StorSimple hello si vous avez plusieurs périphériques inscrits tooyour StorSimple Manager service. clé Hello que vous avez obtenue à l’étape 2 doit être utilisé tooupdate tous hello restants de l’appareil StorSimple enregistré avec hello service StorSimple Manager.

Effectuer hello suite de chiffrement de données de service étapes tooupdate hello sur votre appareil.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>clé de chiffrement de données tooupdate hello service
1. Utiliser Windows PowerShell pour StorSimple tooconnect toohello console. Sélectionnez l’option 1 toolog sur avec un accès complet.
2. À l’invite de commandes hello, tapez :
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Fournir hello clé de chiffrement que vous avez obtenue dans [étape 2 : utiliser Windows PowerShell pour StorSimple tooinitiate hello service modification chiffrement des données clée](#to-initiate-the-service-data-encryption-key-change).


## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur hello [processus de déploiement StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
* En savoir plus sur la [gestion de votre compte de stockage StorSimple](storsimple-8000-manage-storage-accounts.md).
* En savoir plus sur la façon trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).
