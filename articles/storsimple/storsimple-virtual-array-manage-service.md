---
title: "aaaDeploy service du Gestionnaire de périphériques StorSimple | Documents Microsoft"
description: "Explique comment toocreate et delete hello service Gestionnaire de périphériques StorSimple Bonjour portail Azure et décrit comment toomanage hello clé d’inscription de service."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>Déployer le service du Gestionnaire de périphériques StorSimple hello pour StorSimple Virtual Array
## <a name="overview"></a>Vue d'ensemble

Hello le Gestionnaire de périphériques StorSimple service s’exécute dans Microsoft Azure et connecte les appareils StorSimple toomultiple. Après avoir créé le service de hello, vous pouvez l’utiliser appareils hello toomanage hello Microsoft Azure portail s’exécutant dans un navigateur. Cela vous permet de toomonitor tous les périphériques hello connecté toohello StorSimple le Gestionnaire de périphériques de service à partir d’un emplacement unique et centralisé, réduisant les tâches administratives.

Hello courantes tâches connexes tooa service du Gestionnaire de périphériques StorSimple sont les suivantes :

* Créer un service
* Supprimer un service
* Obtenir la clé d’inscription hello
* Régénérer la clé d’inscription hello

Ce didacticiel explique comment tooperform de hello les tâches précédentes. informations Hello contenues dans cet article sont applicable uniquement tooStorSimple réseaux virtuels. Pour plus d’informations sur la série StorSimple 8000, accédez trop[déployer un service StorSimple Manager](storsimple-manage-service.md).

## <a name="create-a-service"></a>Créer un service

toocreate un service, vous devez toohave :

* Un abonnement avec un contrat Entreprise
* Un compte de stockage Microsoft Azure actif
* informations de facturation sont utilisées pour la gestion de l’accès de Hello

Vous pouvez également choisir de toogenerate un compte de stockage lorsque vous créez le service de hello.

Un seul service peut gérer plusieurs appareils. Cependant, un appareil ne peut pas couvrir plusieurs services. Une grande entreprise peut avoir plusieurs toowork d’instances de service avec différents abonnements, organisations ou emplacements de déploiement.

> [!NOTE]
> Vous avez besoin des instances distinctes d’unités de gestionnaire de périphériques StorSimple service toomanage StorSimple 8000 series et les tableaux de virtuel StorSimple.


Effectuer hello suivant les étapes toocreate un service.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>Supprimer un service

Avant de supprimer un service, assurez-vous qu’aucun appareil connecté ne l’utilise. Si le service de hello est en cours d’utilisation, désactiver les périphériques de hello connecté. Hello désactiver l’opération sera le serveur de connexion hello entre l’appareil de hello et service de hello, mais conserver les données d’appareil hello dans le cloud de hello.

> [!IMPORTANT]
> Après la suppression d’un service, opération de hello ne peut pas être annulée. N’importe quel appareil qui utilise hello service devez toobe usine avant de pouvoir être utilisé avec un autre service. Dans ce scénario, les données locales de hello sur le périphérique de hello, ainsi que la configuration de hello, seront perdues.
 

Effectuer hello suivant les étapes toodelete un service.

#### <a name="toodelete-a-service"></a>toodelete un service

1. Accédez trop**toutes les ressources**. Recherchez votre service StorSimple Device Manager. Sélectionnez service hello que vous souhaitez toodelete.
   
    ![Sélectionnez service toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. Accédez tooensure de tableau de bord de service tooyour il n’y aucun périphérique connecté toohello service. S’il n’y a aucun appareil inscrit auprès de ce service, vous verrez également un effet de toohello de message de bannière. Cliquez sur **Supprimer**.
   
    ![Suppression du service](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. Lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui** dans la notification de confirmation hello. 
   
    ![Confirmer la suppression du service](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. Il peut prendre quelques minutes pour hello service toobe est supprimé. Une fois hello service est correctement supprimé, vous serez averti.
   
    ![Suppression du service réussie](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

liste Hello des services va être actualisée.

 ![Liste des services mise à jour](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>Obtenir la clé d’inscription hello
Une fois que vous avez créé un service, vous devez tooregister votre appareil StorSimple hello service. tooregister votre premier appareil StorSimple, vous devez serez hello clé d’inscription de service. tooregister autres périphériques avec un service StorSimple existant, vous devez la clé d’enregistrement hello et hello clé de chiffrement (qui est généré sur le premier périphérique de hello lors de l’inscription). Pour plus d’informations sur la clé de chiffrement de données de service hello, consultez [sécurité StorSimple](storsimple-security.md). Vous pouvez obtenir la clé d’inscription de hello en accédant à hello **clés** panneau pour votre service.

Effectuer hello après la clé d’inscription étapes tooget hello.

#### <a name="tooget-hello-service-registration-key"></a>clé d’inscription tooget hello
1. Bonjour **le Gestionnaire de périphériques StorSimple** panneau, accédez trop**gestion &gt;**  **clés**.
   
   ![Panneau Clés](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. Bonjour **clés** blade, une clé d’inscription de service apparaît. Copiez la clé d’inscription de hello à l’aide d’icône de copie hello. 

Conservez la clé d’inscription hello dans un emplacement sûr. Vous devez cette clé, comme clé de chiffrement de données de service de hello, tooregister des appareils supplémentaires auprès de ce service. Après avoir obtenu la clé d’inscription hello, vous devez tooconfigure votre appareil via hello Windows PowerShell pour StorSimple interface.

## <a name="regenerate-hello-service-registration-key"></a>Régénérer la clé d’inscription hello
Si vous êtes tooperform requis la rotation des clés ou si la liste hello des administrateurs de service a changé, vous devez tooregenerate une clé d’inscription de service. Lorsque vous régénérez la clé de hello, clé hello est utilisé uniquement pour l’inscription des appareils suivants. appareils Hello déjà inscrites ne sont pas affectés par ce processus.

Effectuer hello suivant les étapes tooregenerate une clé d’inscription de service.

#### <a name="tooregenerate-hello-service-registration-key"></a>clé d’inscription tooregenerate hello
1. Bonjour **le Gestionnaire de périphériques StorSimple** panneau, accédez trop**gestion &gt;**  **clés**.
   
   ![Panneau Clés](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. Bonjour **clés** panneau, cliquez sur **régénérer**.
   
   ![Cliquer sur Régénérer](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. Bonjour **clé d’inscription régénérer** panneau, révision hello action requise lorsque hello les clés sont régénérées. Tous les périphériques suivants hello qui sont inscrits auprès de ce service utilise la nouvelle clé d’inscription de hello. Cliquez sur **régénérer** tooconfirm. Vous serez averti une fois l’inscription de hello est terminée.
   
   ![Confirmer la régénération de la clé](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. Une nouvelle clé d’inscription du service s’affiche.
   
    ![Confirmer la régénération de la clé](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   Copiez cette clé et sauvegardez-la pour enregistrer tout nouvel appareil auprès de ce service.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[prise en main](storsimple-virtual-array-deploy1-portal-prep.md) avec un tableau virtuel StorSimple.
* Découvrez comment trop[administrer votre appareil StorSimple](storsimple-ova-web-ui-admin.md).

