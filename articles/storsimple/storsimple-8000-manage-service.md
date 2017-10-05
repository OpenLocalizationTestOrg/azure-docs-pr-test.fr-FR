---
title: "Déployer le service StorSimple Device Manager dans Azure | Microsoft Docs"
description: "Cet article décrit comment créer et supprimer le service StorSimple Device Manager dans le Portail Azure, ainsi que la procédure de gestion de la clé d’inscription du service."
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
ms.openlocfilehash: 22bb4a32f006d7e49356743c2a87eb622a61d18e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>Déployer le service StorSimple Device Manager pour les appareils de la gamme StorSimple 8000

## <a name="overview"></a>Vue d'ensemble

Le service StorSimple Device Manager s’exécute dans Microsoft Azure et se connecte à plusieurs appareils StorSimple. Après avoir créé le service, vous pouvez l’utiliser pour gérer tous les appareils qui y sont connectés à partir d’un emplacement central unique, ce qui réduit la charge administrative.

Ce didacticiel décrit les étapes requises pour la création, la suppression, la migration du service et la gestion de la clé d’inscription du service. Les informations contenues dans cet article s’appliquent uniquement aux appareils de la gamme StorSimple 8000. Pour plus d’informations sur StorSimple Virtual Arrays, accédez à [Déployer le service StorSimple Device Manager pour StorSimple Virtual Array](storsimple-virtual-array-manage-service.md).

## <a name="create-a-service"></a>Créer un service
Pour créer un service StorSimple Device Manager, vous avez besoin des éléments suivants :

* Un abonnement avec un contrat Entreprise
* Un compte de stockage Microsoft Azure actif
* Les informations de facturation utilisées pour la gestion des accès

Seuls les abonnements avec un contrat Entreprise sont autorisés. Les abonnements Microsoft Azure Sponsorship qui étaient autorisés dans le portail Azure classique ne sont pas pris en charge dans le portail Azure. Le message suivant s’affiche quand vous utilisez un abonnement non pris en charge :

![Abonnement non valide](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

Vous pouvez également choisir de générer un compte de stockage par défaut lorsque vous créez le service.

Un seul service peut gérer plusieurs appareils. Cependant, un appareil ne peut pas couvrir plusieurs services. Une grande entreprise peut avoir plusieurs instances de service pour utiliser différents abonnements, organisations ou même emplacements de déploiement. 

> [!NOTE]
> Vous devez créer des instances distinctes du service StorSimple Device Manager pour gérer les appareils de la gamme StorSimple 8000 et les baies StorSimple Virtual Array.

Procédez comme suit pour créer un service.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


Pour chaque service StorSimple Device Manager, les attributs suivants existent :

* **Nom** : le nom assigné à votre service StorSimple Device Manager lors de sa création. **Impossible de modifier le nom du service une fois que le service a été créé. Cela vaut également pour les autres entités telles que les appareils, les volumes, les conteneurs de volumes et les stratégies de sauvegarde qui ne peuvent pas être renommés dans le portail Azure.**
* **État** : l’état du service, qui peut être **Actif**, **Création en cours** ou **En ligne**.
* **Emplacement** : l’emplacement géographique sur lequel l’appareil StorSimple sera déployé.
* **Abonnement** : l’abonnement de facturation associé à votre service.

## <a name="move-a-service-to-azure-portal"></a>Déplacer un service vers le portail Azure
Les appareils de la gamme StorSimple 8000 peuvent désormais être gérés dans le portail Azure. Si vous avez un service existant pour gérer les appareils StorSimple, nous vous recommandons de déplacer votre service vers le portail Azure. Le portail Azure classique pour le service StorSimple Manager n’est pas disponible après le 30 septembre 2017.

L’option de migration vers le portail Azure est disponible en plusieurs phases. Si vous ne voyez aucune option de migration vers le portail Azure, mais que vous souhaitez déplacer et examiner l’impact de la migration, détaillé dans [Considérations relatives à la transition](#considerations-for-transition), vous pouvez [faire une requête](https://aka.ms/ss8000-cx-signup).

### <a name="considerations-for-transition"></a>Considérations relatives à la transition

Examinez l’impact de la migration vers le nouveau portail Azure avant de déplacer le service.

#### <a name="before-you-transition"></a>Avant la transition

* Votre appareil exécute Update 3.0 ou version ultérieure. Si votre appareil exécute une version antérieure, installez les dernières mises à jour. Pour plus d’informations, accédez à [Install Update 4 on your StorSimple device](storsimple-8000-install-update-4.md) (Installer Update 4 sur votre appareil StorSimple). Si vous utilisez StorSimple Cloud Appliance (8010/8020), créez une appliance cloud avec Update 4.0. 

* Une fois la transition effectuée vers le nouveau portail Azure, vous ne pouvez pas utiliser le portail Azure classique pour gérer votre appareil StorSimple.

* La transition se fait sans interruption de service et l’appareil ne subit pas de temps d’arrêt.

* Tous les services StorSimple Device Manager appartenant à l’abonnement spécifié font l’objet de la transition.

#### <a name="during-the-transition"></a>Au cours de la transition

* Vous ne pouvez pas gérer votre appareil à partir du portail.
* Les opérations telles que les sauvegardes planifiées et de hiérarchisation continuent d’être effectuées.
* Ne supprimez pas les anciens services StorSimple Device Manager pendant que la transition est en cours.

#### <a name="after-the-transition"></a>Après la transition

* Vous ne pouvez plus gérer vos appareils à partir du portail classique.

* Les cmdlets PowerShell Azure Service Management (ASM) ne sont pas pris en charge. Mettez à jour les scripts pour gérer vos appareils via Azure Resource Manager.

* La configuration de votre service et de votre appareil est conservée. Tous vos volumes et sauvegardes font également l’objet de la transition vers le portail Azure.

### <a name="begin-transition"></a>Commencer la transition

Procédez comme suit pour effectuer la transition de votre service vers le portail Azure.

1. Accédez à votre service StorSimple Manager dans le portail classique.

2. Vous voyez une notification qui vous informe que le service StorSimple Device Manager est désormais disponible dans le portail Azure. Notez que dans le portail Azure, le service est appelé service StorSimple Device Manager.

    ![Notification de la migration](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. Assurez-vous de bien avoir examiné l’impact total de la migration.
    2. Passez en revue la liste des services StorSimple Device Manager qui seront déplacés à partir du portail classique.

3. Cliquez sur **Migrer**. La transition commence, et se termine après quelques minutes.

Une fois la transition terminée, vous pouvez gérer vos appareils via le service StorSimple Device Manager dans le portail Azure.

Seuls les appareils StorSimple exécutant Update 3.0 et des versions ultérieures sont pris en charge dans le portail Azure. La prise en charge des appareils exécutant des versions antérieures est limitée. Le tableau suivant récapitule les opérations prises en charge sur l’appareil exécutant des versions antérieures à Update 3.0, une fois que vous avez effectué la migration du portail classique vers le portail Azure.

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
| Cloner vers un appareil exécutant Update 3.0 et versions ultérieures <br> L’appareil source exécute une version antérieure à Update 3.0.                                | Oui            |
| Cloner vers un appareil exécutant des versions antérieures à Update 3.0                                                                          | Non             |
| Basculer en tant qu’appareil source <br> (à partir d’un appareil exécutant une version antérieure à Update 3.0 vers un appareil exécutant Update 3.0 et versions ultérieures)                                                               | Oui            |
| Basculer en tant qu’appareil cible <br> (vers un appareil exécutant une version logicielle antérieure à Update 3.0)                                                                                   | Non             |
| Supprimer une alerte                                                                                                                  | Oui            |
| Afficher les stratégies de sauvegarde, le catalogue de sauvegarde, les volumes, les conteneurs de volumes, les graphiques de surveillance, les travaux et les alertes créés dans le portail classique | Oui            |
| Activer et désactiver des contrôleurs d’appareils                                                                                              | Oui            |


## <a name="delete-a-service"></a>Supprimer un service

Avant de supprimer un service, assurez-vous qu’aucun appareil connecté ne l’utilise. Si le service est en cours d’utilisation, désactivez les appareils connectés. L’opération de désactivation rompt la connexion entre l’appareil et le service, mais conserve les données de l’appareil dans le cloud.

> [!IMPORTANT]
> Après qu’un service a été supprimé, l’opération ne peut pas être annulée. Un appareil qui utilisait le service doit être réinitialisé aux paramètres d’usine par défaut avant de pouvoir être utilisé avec un autre service. Dans ce scénario, les données locales de l’appareil, ainsi que la configuration, sont perdues.

Pour supprimer un service, procédez comme suit.

### <a name="to-delete-a-service"></a>Pour supprimer un service

1. Recherchez le service que vous souhaitez supprimer. Cliquez sur l’icône **Ressources** et entrez les termes appropriés à rechercher. Dans les résultats de la recherche, cliquez sur le service que vous souhaitez supprimer.

    ![Rechercher le service à supprimer](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. Cela vous renvoie vers le panneau du service StorSimple Device Manager. Cliquez sur **Supprimer**.

    ![Suppression du service](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. Cliquez sur **Oui** dans la notification de confirmation. La suppression du service peut nécessiter quelques minutes.

    ![Confirmer la suppression](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-the-service-registration-key"></a>Obtenir la clé d’inscription du service

Une fois que vous avez créé un service, vous devez inscrire votre appareil StorSimple auprès du service. Pour inscrire votre premier appareil StorSimple, vous avez besoin de la clé d’inscription du service. Pour inscrire des appareils supplémentaires auprès d’un service StorSimple existant, vous avez besoin de la clé d’inscription et de la clé de chiffrement des données de service (générée sur le premier appareil lors de l’inscription). Pour plus d’informations sur la clé de chiffrement des données du service, consultez la rubrique [Sécurité StorSimple](storsimple-8000-security.md). Vous pouvez obtenir la clé d’inscription en accédant à **Clés** sur le panneau de votre service StorSimple Device Manager.

Procédez comme suit pour obtenir la clé d’inscription du service.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Conservez la clé d’inscription du service dans un emplacement sûr. Vous aurez besoin de cette clé, ainsi que de la clé de chiffrement des données du service, pour enregistrer des appareils supplémentaires auprès du service. Après avoir obtenu la clé d’inscription du service, vous devez configurer votre appareil via l’interface Windows PowerShell pour StorSimple.

Pour plus d’informations sur l’utilisation de la clé d’inscription, consultez [Étape 3 : configure et inscrire l’appareil via Windows PowerShell pour StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-the-service-registration-key"></a>Régénérer la clé d’inscription du service
Vous devez régénérer une clé d’inscription du service si vous êtes amené à effectuer une rotation des clés ou si la liste des administrateurs de services fédérés a changé. Lorsque vous régénérez la clé, la nouvelle clé est utilisée uniquement pour l’enregistrement des appareils suivants. Les appareils déjà enregistrés ne sont pas affectés par ce processus.

Procédez comme suit pour régénérer une clé d’inscription du service.

### <a name="to-regenerate-the-service-registration-key"></a>Pour régénérer la clé d’inscription du service
1. Dans le panneau **Instance de StorSimple Device Manager**, accédez à **Gestion &gt;** **Clés**.
    
    ![Panneau Clés](./media/storsimple-8000-manage-service/regenregkey2.png)

2. Dans le panneau **Clés**, cliquez sur **Régénérer**.

    ![Cliquer sur Régénérer](./media/storsimple-8000-manage-service/regenregkey3.png)
3. Dans le panneau **Régénérer la clé d’inscription du service**, vérifiez l’action requise lors de la régénération des clés. Tous les appareils qui seront inscrits auprès de ce service par la suite utilisent la nouvelle clé d’inscription. Cliquez sur **Régénérer** pour confirmer l’opération. Une fois la régénération terminée, vous en êtes informé.

    ![Confirmer la régénération](./media/storsimple-8000-manage-service/regenregkey4.png)

4. Une nouvelle clé d’inscription du service s’affiche.

5. Copiez cette clé et sauvegardez-la pour enregistrer tout nouvel appareil auprès de ce service.



## <a name="change-the-service-data-encryption-key"></a>Modifier la clé de chiffrement des données de service
Les clés de chiffrement des données de service permettent de chiffrer les données client confidentielles, telles que les identifiants du compte de stockage, qui sont envoyées à partir votre service StorSimple Manager sur le périphérique StorSimple. Vous devrez modifier ces clés périodiquement si votre service informatique applique une politique de rotation des clés sur les périphériques de stockage. Le processus de modification de la clé peut être légèrement différent selon qu'il y a un ou plusieurs périphériques gérés par le service StorSimple Manager. Pour plus d’informations, accédez à [StorSimple security and data protection](storsimple-8000-security.md) (Sécurité et protection des données StorSimple).

La modification de la clé de chiffrement est un processus en 3 étapes :

1. À l’aide des scripts Windows PowerShell pour Azure Resource Manager, autorisez un appareil à modifier la clé de chiffrement des données de service.
2. Utiliser Windows PowerShell pour StorSimple pour démarrer la modification de la clé de chiffrement des données du service.
3. Si vous avez plusieurs périphériques StorSimple, mettez à jour la clé de chiffrement des données sur les autres périphériques.

### <a name="step-1-use-windows-powershell-script-to-authorize-a-device-to-change-the-service-data-encryption-key"></a>Étape 1 : Utiliser un script Windows PowerShell pour autoriser un appareil à modifier la clé de chiffrement des données de service
En règle générale, l’administrateur de l’appareil demande que l’administrateur du service autorise un appareil à modifier les clés de chiffrement des données du service. Ensuite, l’administrateur du service autorise l’appareil à modifier la clé.

Cette étape est effectuée en utilisant le script basé sur Azure Resource Manager. L’administrateur de services fédérés peut sélectionner un appareil pouvant être autorisé. Après cela, l’appareil est autorisé à démarrer le processus de modification de la clé de chiffrement des données du service. 

Pour plus d’informations sur l’utilisation du script, accédez à [Authorize-ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1).

#### <a name="which-devices-can-be-authorized-to-change-service-data-encryption-keys"></a>Quels appareils peuvent être autorisés à modifier les clés de chiffrement des données du service ?
Un appareil doit respecter les critères suivants avant d’être autorisé à démarrer des modifications de clé de chiffrement des données du service :

* L’appareil doit être en ligne pour bénéficier de l’autorisation de modification de clé de chiffrement des données du service.
* Si le changement de clé n’a pas été démarré, vous devez attendre 30 minutes avant d’autoriser à nouveau le même appareil.
* Vous pouvez autoriser un autre appareil, sous réserve que la modification de la clé n’a pas été démarrée par l’appareil précédemment autorisé. Une fois le nouvel appareil autorisé, l’ancien appareil ne peut plus démarrer la modification.
* Vous ne pouvez pas autoriser un appareil alors que la substitution de la clé de chiffrement des données du service est en cours.
* Vous pouvez autoriser un appareil lorsque certains appareils inscrits auprès du service ont substitué le chiffrement tandis que d’autres ne l’ont pas fait. 

### <a name="step-2-use-windows-powershell-for-storsimple-to-initiate-the-service-data-encryption-key-change"></a>Étape 2 : utiliser Windows PowerShell pour StorSimple pour démarrer la modification de la clé de chiffrement des données du service
Cette étape s’effectue dans l’interface Windows PowerShell pour StorSimple, sur l’appareil StorSimple autorisé.

> [!NOTE]
> Aucune opération ne peut être effectuée dans le portail Azure de votre service StorSimple Manager avant la fin de la substitution de la clé.
> 
> 

Si vous utilisez la console série de l’appareil pour vous connecter à l’interface Windows PowerShell, procédez comme suit.

#### <a name="to-initiate-the-service-data-encryption-key-change"></a>Pour démarrer la modification de la clé de chiffrement des données du service
1. Sélectionnez Option 1 pour vous connecter avec un accès complet.
2.  À l’invite de commandes, tapez :
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Une fois l’applet de commande terminée, vous obtenez une nouvelle clé de chiffrement des données du service. Copiez et enregistrez cette clé pour l’utiliser lors de l’étape 3 de cette procédure. Cette clé permet de mettre à jour tous les appareils restants inscrits auprès du service StorSimple Manager.
   
   > [!NOTE]
   > Ce processus doit être démarré dans les quatre heures suivant l’autorisation d’un appareil StorSimple.
   > 
   > 
   
   Cette nouvelle clé est ensuite envoyée au service pour être transmise à tous les appareils inscrits auprès du service. Une alerte s’affiche alors sur le tableau de bord du service. Le service désactive toutes les opérations sur les appareils inscrits et l’administrateur de l’appareil doit alors mettre à jour la clé de chiffrement des données du service sur les autres appareils. Toutefois, les E/S (hôtes envoyant des données vers le cloud) ne sont pas interrompues.
   
   Si vous avez un seul appareil inscrit auprès de votre service, le processus de substitution est maintenant terminé et vous pouvez ignorer l’étape suivante. Si vous avez plusieurs appareils inscrits auprès de votre service, passez à l’étape 3.

### <a name="step-3-update-the-service-data-encryption-key-on-other-storsimple-devices"></a>Étape 3 : mettre à jour la clé de chiffrement sur les autres appareils StorSimple
Si vous avez plusieurs appareils inscrits auprès du service StorSimple Manager, cette procédure s’effectue dans l’interface Windows PowerShell de votre appareil StorSimple. La clé que vous avez obtenue à l’étape 2 doit être utilisée pour mettre à jour tous les appareils StorSimple restant inscrits auprès du service StorSimple Manager.

Procédez comme suit pour mettre à jour le chiffrement des données du service sur votre appareil.

#### <a name="to-update-the-service-data-encryption-key"></a>Pour mettre à jour la clé de chiffrement des données du service
1. Utilisez Windows PowerShell pour StorSimple pour vous connecter à la console. Sélectionnez Option 1 pour vous connecter avec un accès complet.
2.  À l’invite de commandes, tapez :
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Entrez la clé de chiffrement des données du service obtenue lors de l’ [Étape 2 : utiliser Windows PowerShell pour StorSimple pour démarrer la modification de la clé de chiffrement des données du service](#to-initiate-the-service-data-encryption-key-change).


## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur le [processus de déploiement StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
* En savoir plus sur la [gestion de votre compte de stockage StorSimple](storsimple-8000-manage-storage-accounts.md).
* En savoir plus sur [l’utilisation du service StorSimple Device Manager pour gérer votre appareil StorSimple](storsimple-8000-manager-service-administration.md).
