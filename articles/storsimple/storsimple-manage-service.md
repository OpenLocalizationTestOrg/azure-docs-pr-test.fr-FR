---
title: aaaDeploy hello service StorSimple Manager | Documents Microsoft
description: "Explique comment toocreate et delete hello service StorSimple Manager Bonjour portail Azure classic et décrit comment toomanage hello clé d’inscription de service."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>Déployer le service StorSimple Manager hello Bonjour portail Azure classic

## <a name="overview"></a>Vue d'ensemble
Hello service StorSimple Manager s’exécute dans Microsoft Azure et connecte les appareils StorSimple toomultiple. Après avoir créé le service de hello, vous pouvez l’utiliser appareils hello toomanage hello Microsoft Azure classic portail s’exécutant dans un navigateur. Cela vous permet de toomonitor tous les périphériques hello connecté toohello StorSimple Manager de service à partir d’un emplacement unique et centralisé, réduisant les tâches administratives.

page d’accueil du gestionnaire StorSimple Hello répertorie tous les services de StorSimple Manager hello que vous pouvez utiliser toomanage vos périphériques de stockage StorSimple. Pour chaque service StorSimple Manager, hello informations suivantes s’affichent sur la page du gestionnaire StorSimple hello :

* **Nom** – nom hello qui a été affecté le service StorSimple Manager tooyour lors de sa création. **Impossible de modifier le nom du service Hello après que hello service est créé. Cela vaut également pour les autres entités telles que des appareils, des volumes, des conteneurs de volumes et des stratégies de sauvegarde ne peut pas être renommées dans hello portail Azure classic.**
* **État** – hello l’état du service hello, qui peut être **Active**, **création**, ou **Online**.
* **Emplacement** – hello emplacement géographique dans le hello StorSimple appareil sera déployé.
* **Abonnement** : hello abonnement associé à votre service de facturation.

tâches courantes Hello qui peuvent être effectuées via la page du gestionnaire StorSimple hello sont :

* Créer un service
* Supprimer un service
* Obtenir la clé d’inscription hello
* Régénérer la clé d’inscription hello

Ce didacticiel décrit comment tooperform de ces tâches.

## <a name="create-a-service"></a>Créer un service
Hello d’utilisation **création rapide** option toocreate un service StorSimple Manager si vous souhaitez toodeploy votre appareil StorSimple. toocreate un service, vous devez toohave :

* Un abonnement avec un contrat Entreprise
* Un compte de stockage Microsoft Azure actif
* informations de facturation sont utilisées pour la gestion de l’accès de Hello

Vous pouvez également choisir de toogenerate un compte de stockage par défaut lorsque vous créez le service de hello.

Un seul service peut gérer plusieurs appareils. Cependant, un appareil ne peut pas couvrir plusieurs services. Une grande entreprise peut avoir plusieurs toowork d’instances de service avec différents abonnements, organisations ou emplacements de déploiement. Notez que vous avez besoin des instances distinctes d’unités StorSimple Manager service toomanage StorSimple 8000 series et les tableaux de virtuel StorSimple.

> [!IMPORTANT] 
> Si vous avez un service inutilisé créé (aucun périphérique opérations ont été effectuées sur cette ressource) tooAugust préalable 2016, il ne peut pas être géré via le portail Azure ou le portail Azure classic. Nous vous recommandons de créer un nouveau service Bonjour portail Azure.

Effectuer hello suivant les étapes toocreate un service.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>Supprimer un service
Avant de supprimer un service, assurez-vous qu’aucun appareil connecté ne l’utilise. Si le service de hello est en cours d’utilisation, désactiver les périphériques de hello connecté. Hello désactiver l’opération sera le serveur de connexion hello entre l’appareil de hello et service de hello, mais conserver les données d’appareil hello dans le cloud de hello.

> [!IMPORTANT] 
> Après la suppression d’un service, opération de hello ne peut pas être annulée. N’importe quel appareil qui utilise hello service devez toobe usine avant de pouvoir être utilisé avec un autre service. Dans ce scénario, les données locales de hello sur le périphérique de hello, ainsi que la configuration de hello, seront perdues.

Effectuer hello suivant les étapes toodelete un service.

### <a name="toodelete-a-service"></a>toodelete un service
1. Sur hello **service StorSimple Manager** page service hello select que vous souhaitez toodelete.
2. Cliquez sur **supprimer** bas hello de page de hello.
3. Cliquez sur **Oui** dans la notification de confirmation hello. Il peut prendre quelques minutes pour hello service toobe est supprimé.

## <a name="get-hello-service-registration-key"></a>Obtenir la clé d’inscription hello
Une fois que vous avez créé un service, vous devez tooregister votre appareil StorSimple hello service. tooregister votre premier appareil StorSimple, vous devez serez hello clé d’inscription de service. tooregister autres périphériques avec un service StorSimple existant, vous devez la clé d’enregistrement hello et hello clé de chiffrement (qui est généré sur le premier périphérique de hello lors de l’inscription). Pour plus d’informations sur la clé de chiffrement de données de service hello, consultez [sécurité StorSimple](storsimple-security.md). Vous pouvez obtenir la clé d’inscription de hello en accédant à **clé d’inscription** sur hello **Services** page.

Effectuer hello après la clé d’inscription étapes tooget hello.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

Conservez la clé d’inscription hello dans un emplacement sûr. Vous devez cette clé, comme clé de chiffrement de données de service de hello, tooregister des appareils supplémentaires auprès de ce service. Après avoir obtenu la clé d’inscription hello, vous devez tooconfigure votre appareil via hello Windows PowerShell pour StorSimple interface.

Pour plus d’informations sur la façon de toouse cette clé, pour identifier l’enregistrement [étape 3 : configurer et inscrire l’appareil hello via Windows PowerShell pour StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Régénérer la clé d’inscription hello
Si vous êtes tooperform requis la rotation des clés ou si la liste hello des administrateurs de service a changé, vous devez tooregenerate une clé d’inscription de service. Lorsque vous régénérez la clé de hello, clé hello est utilisé uniquement pour l’inscription des appareils suivants. appareils Hello déjà inscrites ne sont pas affectés par ce processus.

Effectuer hello suivant les étapes tooregenerate une clé d’inscription de service.

### <a name="tooregenerate-hello-service-registration-key"></a>clé d’inscription tooregenerate hello
1. Sur hello **service StorSimple Manager** , cliquez sur **clé d’inscription**.
2. Bonjour **clé d’inscription de Service** boîte de dialogue, cliquez sur **régénérer**.
3. Un message de confirmation s’affiche. Cliquez sur **OK** toocontinue avec la régénération de hello.
4. Une nouvelle clé d’inscription du service s’affiche.
5. Copiez cette clé et sauvegardez-la pour enregistrer tout nouvel appareil auprès de ce service.
6. Cliquez sur une icône de coche hello ![Icône en forme de coche](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose cette boîte de dialogue.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur hello [processus de déploiement StorSimple](storsimple-deployment-walkthrough-u2.md).
* En savoir plus sur la [gestion de votre compte de stockage StorSimple](storsimple-manage-storage-accounts.md).
* En savoir plus sur la façon trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).
