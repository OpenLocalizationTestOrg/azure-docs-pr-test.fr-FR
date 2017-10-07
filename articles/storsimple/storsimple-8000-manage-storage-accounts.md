---
title: "aaaManage informations d’identification de votre compte de stockage StorSimple pour les appareils Microsoft Azure StorSimple 8000 series | Documents Microsoft"
description: "Explique comment vous pouvez utiliser hello tooadd de page de configuration du Gestionnaire de périphériques StorSimple, modifier, supprimer ou les clés de sécurité hello rotation pour un compte de stockage."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 132ee46509b39db4d1b97b0f1077800a253e8da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-storage-account-credentials"></a>Utilisez hello le Gestionnaire de périphériques StorSimple service toomanage vos informations d’identification du compte de stockage

## <a name="overview"></a>Vue d'ensemble

Hello **Configuration** section dans le panneau de service de gestionnaire de périphériques StorSimple hello présente tous les paramètres de service global hello qui peuvent être créés dans hello service du Gestionnaire de périphériques StorSimple. Ces paramètres peuvent être appliqués tooall hello appareils toohello service connecté et incluant :

* Informations d’identification du compte de stockage
* Modèles de bande passante 
* Enregistrements de contrôle d’accès 

Ce didacticiel explique comment tooadd, modifier ou supprimer les informations d’identification du compte de stockage ou faire tourner les clés de sécurité hello pour un compte de stockage.

 ![Liste d’informations d’identification de compte de stockage](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

Comptes de stockage contiennent les informations d’identification hello hello StorSimple périphérique utilise tooaccess votre compte de stockage avec votre fournisseur de services cloud. Pour les comptes de stockage Microsoft Azure, il s’agit des informations d’identification telles que le nom du compte hello et clé d’accès primaire hello. 

Sur hello **informations d’identification du compte de stockage** panneau, stockage de tous les comptes qui sont créés pour hello facturation d’abonnement sont affichés dans un format tabulaire contenant hello informations suivantes :

* **Nom** – hello compte toohello de nom unique attribué lors de sa création.
* **SSL activé** : indique si hello SSL est activé et la communication de l’appareil-à-cloud est sur un canal sécurisé hello.
* **Utilisé par** – hello du nombre de volumes à l’aide du compte de stockage hello.

Hello courants des tâches connexes toostorage comptes qui peuvent être effectuées sont :

* Ajout d’un compte de stockage 
* Modification d’un compte de stockage 
* Suppression d'un compte de stockage 
* Rotation des clés de comptes de stockage 

## <a name="types-of-storage-accounts"></a>Types de compte de stockage

Vous pouvez utiliser trois types de compte de stockage avec votre appareil StorSimple.

* **Les comptes de stockage généré automatiquement** – comme hello nom l’indique, ce type de compte de stockage est généré automatiquement lorsque le service de hello est créé. toolearn en savoir plus sur la création de ce compte de stockage, consultez [étape 1 : créer un nouveau service](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) dans [déployer l’appareil StorSimple local](storsimple-8000-deployment-walkthrough-u2.md). 
* **Comptes de stockage dans l’abonnement au service hello** – il s’agit des comptes de stockage Azure hello associés hello même abonnement que celui du service de hello. toolearn en savoir plus sur la façon dont ces comptes de stockage sont créés, consultez [sur les comptes de stockage Azure](../storage/common/storage-create-storage-account.md). 
* **Comptes de stockage en dehors de l’abonnement au service hello** : il s’agit des comptes de stockage Azure hello qui ne sont pas associés à votre service et probablement hello se trouvait avant le service a été créé.

## <a name="add-a-storage-account"></a>Ajout d’un compte de stockage

Vous pouvez ajouter un compte de stockage en fournissant un unique conviviales accès et le nom des informations d’identification lié toohello compte de stockage (avec le fournisseur de services de cloud computing spécifié hello). Vous avez également option hello d’activation hello sécurisé Secure sockets layer (SSL) en mode toocreate un canal sécurisé pour la communication réseau entre votre cloud hello et des appareils.

Vous pouvez créer plusieurs comptes pour un fournisseur de services cloud donné. Sachez, toutefois, qu’après la création d’un compte de stockage, vous ne pouvez pas modifier le fournisseur de services de cloud hello.

Pendant l’enregistrement de compte de stockage hello, hello service essaie de toocommunicate avec votre fournisseur de services cloud. informations d’identification Hello et les informations d’accès hello que vous avez fournies sont authentifiées à ce stade. Un compte de stockage est créé uniquement si hello authentification réussit. Si l’authentification hello échoue, un message d’erreur s’affichera.

Utilisez hello suit les informations d’identification du compte Azure storage tooadd procédures :

* tooadd une information d’identification du compte de stockage qui a hello même abonnement Azure en tant que service du Gestionnaire de périphériques hello
* tooadd une information d’identification du compte de stockage Azure qui est en dehors de l’abonnement au service Gestionnaire de périphériques hello

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="tooadd-an-azure-storage-account-credential-outside-of-hello-storsimple-device-manager-service-subscription"></a>tooadd une information d’identification du compte de stockage Azure en dehors de l’abonnement au service Gestionnaire de périphériques StorSimple hello

1. Accédez tooyour service StorSimple le Gestionnaire de périphériques, sélectionnez et double-cliquez dessus. Cette opération ouvre hello **vue d’ensemble** panneau.
2. Sélectionnez **informations d’identification du compte de stockage** dans hello **Configuration** section. Celle-ci répertorie toutes les informations d’identification de compte stockage existant associées hello service du Gestionnaire de périphériques StorSimple.
3. Cliquez sur **Add**.
4. Bonjour **ajouter une information d’identification du compte de stockage** panneau, hello suivant :
   
    1. Pour **Abonnement**, sélectionnez **Autre**.
   
    2. Fournissez le nom hello de vos informations d’identification du compte de stockage Azure.
   
    3. Bonjour **clé d’accès de compte de stockage** zone de texte, alimentation hello clé d’accès primaire pour vos informations d’identification du compte de stockage Azure. tooget cette clé, passez le service de stockage Azure toohello, vos informations d’identification du compte de stockage, puis cliquez sur **gérer les clés de compte**. Vous pouvez maintenant copier la clé d’accès primaire hello.
   
    4. tooenable SSL, cliquez sur hello **activer** bouton toocreate un canal sécurisé pour la communication réseau entre votre cloud de service et hello du Gestionnaire de périphériques StorSimple. Cliquez sur hello **désactiver** bouton uniquement si vous opérez dans un cloud privé.
   
    5. Cliquez sur **Add**. Vous êtes averti une fois les informations d’identification de compte de stockage hello sont créée avec succès.

5. informations d’identification de compte de stockage Hello nouvellement créé s’affiche dans le panneau de service de configurer le Gestionnaire de périphériques StorSimple hello sous **informations d’identification du compte de stockage**.
   


## <a name="edit-a-storage-account"></a>Modification d’un compte de stockage

Vous pouvez modifier un compte de stockage utilisé par un conteneur de volumes. Si vous modifiez un compte de stockage qui est actuellement en cours d’utilisation, hello uniquement les toomodify disponibles champ agit hello clé d’accès pour le compte de stockage hello. Vous pouvez fournir la clé d’accès de stockage de hello et enregistrer les paramètres de mise à jour de hello.

#### <a name="tooedit-a-storage-account"></a>tooedit un compte de stockage

1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour. Bonjour **Configuration** , cliquez sur **informations d’identification du compte de stockage**.

    ![Informations d’identification du compte de stockage](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. Bonjour **informations d’identification du compte de stockage** panneau, à partir de la liste de hello d’informations d’identification de compte de stockage, sélectionnez et cliquez sur une vous souhaitez tooedit hello. 

3. Vous pouvez modifier hello **activer SSL** sélection. Vous pouvez également cliquer sur **plus...**  , puis sélectionnez **toorotate clé de synchronisation accès** vos clés de l’accès de compte de stockage. Accédez trop[rotation des comptes de stockage de clé](#key-rotation-of-storage-accounts) pour plus d’informations sur la façon dont tooperform permutation des clés. Une fois que vous avez modifié les paramètres de hello, cliquez sur **enregistrer**. 

    ![Enregistrer les modifications apportées aux informations d’identification de compte de stockage](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération. 

    ![Confirmer les modifications](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

paramètres de Hello sont mis à jour et enregistrés pour votre compte de stockage. 

## <a name="delete-a-storage-account"></a>Suppression d'un compte de stockage

> [!IMPORTANT]
> Vous pouvez supprimer un compte de stockage uniquement s’il n’est pas utilisé par un conteneur de volumes. Si un compte de stockage est utilisé par un conteneur de volume, tout d’abord supprimer le conteneur de volume de hello et puis supprimez le compte de stockage hello associé.

#### <a name="toodelete-a-storage-account"></a>toodelete un compte de stockage

1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour. Bonjour **Configuration** , cliquez sur **informations d’identification du compte de stockage**.

2. Dans la liste tabulaire hello de comptes de stockage, pointez sur compte hello que toodelete. Menu contextuel de hello tooinvoke et cliquez sur **supprimer**.

    ![Supprimer les informations d’identification de compte de stockage](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. Lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui** toocontinue avec suppression des hello. la liste tabulaire Hello sera mis à jour tooreflect hello modifications.

    ![Confirmation de suppression](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a>Rotation des clés de comptes de stockage

Pour des raisons de sécurité, les centres de données exigent souvent une rotation des clés. Chaque abonnement Microsoft Azure peut être associé à un ou plusieurs comptes de stockage. comptes d’accès de toothese Hello est contrôlé par abonnement de hello et touches d’accès pour chaque compte de stockage. 

Lorsque vous créez un compte de stockage, Microsoft Azure génère deux clés d’accès de stockage de 512 bits sont utilisés pour l’authentification lors de l’accès au compte de stockage hello. Avoir deux clés d’accès de stockage vous permet de clés de hello tooregenerate avec aucun service de stockage tooyour d’interruption ou le service d’accès toothat. clé qui est actuellement en cours d’utilisation Hello est hello *principal* clé hello et la clé de sauvegarde est référencé tooas hello *secondaire* clé. Vous devez fournir une de ces deux clés lorsque votre appareil Microsoft Azure StorSimple accède à votre fournisseur de services de stockage cloud.

## <a name="what-is-key-rotation"></a>La rotation des clés, de quoi s’agit-il ?

En règle générale, les applications qu’un seul de hello clés tooaccess utilisent vos données. Après un certain temps, vous pouvez avoir vos applications pour basculer la deuxième clé de toousing hello. Après avoir basculé votre clé secondaire toohello d’applications, vous pouvez mettre hors service de la première clé de hello et puis générer une nouvelle clé. À l’aide de deux clés de hello de cette manière permet à vos données de toohello d’accès aux applications sans temps mort.

les clés de compte de stockage Hello sont toujours stockées dans le service hello sous forme chiffrée. Toutefois, elles peuvent être réinitialisées via hello service du Gestionnaire de périphériques StorSimple. service de Hello peut obtenir la clé primaire de hello et la clé secondaire pour tous les hello Bonjour même abonnement, y compris les comptes créés dans le service de stockage hello ainsi que les comptes de stockage par défaut hello généré, les comptes de stockage lorsque hello le Gestionnaire de périphériques StorSimple service de création. Hello service du Gestionnaire de périphériques StorSimple sera obtient toujours ces clés à partir de hello portail Azure classic et les stocke sous forme chiffrée.

## <a name="rotation-workflow"></a>Workflow de rotation

Un administrateur de Microsoft Azure peut régénérer ou modifier la clé primaire ou secondaire de hello en accédant directement au compte de stockage hello (via le service Microsoft Azure Storage de hello). Hello service du Gestionnaire de périphériques StorSimple ne voit pas automatiquement ce changement.

le service de gestionnaire de périphériques StorSimple tooinform hello de modification de hello, vous devez tooaccess service de gestionnaire de périphériques StorSimple hello, accéder au compte de stockage hello, puis synchroniser la clé primaire ou secondaire hello (selon l’application a été modifiée). service de Hello puis obtient la clé la plus récente hello, chiffre hello clés et envoie hello chiffré appareil de la clé toohello.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service"></a>toosynchronize des clés pour les comptes de stockage dans hello même abonnement que le service de hello 
1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour. Bonjour **Configuration** , cliquez sur **informations d’identification du compte de stockage**.
2. À partir de hello tabulaire la liste des comptes de stockage, cliquez sur hello une que vous souhaitez toomodify. 

    ![synchroniser les clés](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. Cliquez sur **... Plus** , puis sélectionnez **toorotate clé de synchronisation accès**.   

    ![synchroniser les clés](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. Bonjour service du Gestionnaire de périphériques StorSimple, vous devez clé hello tooupdate qui a été précédemment modifié Bonjour service Microsoft Azure Storage. Si la clé d’accès primaire hello a été modifiée (régénérée), sélectionnez **principal** clé. Si la clé secondaire de hello a été modifié, sélectionnez **secondaire** clé. Cliquez sur **Synchroniser la clé**.
      
      ![synchroniser les clés](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

Vous serez averti une fois la clé de hello correctement sycnhronized.

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>toosynchronize clés pour les comptes de stockage en dehors de l’abonnement au service hello
1. Sur hello **Services** , cliquez sur hello **configurer** onglet.
2. Cliquez sur **Ajouter/modifier des comptes de stockage**.
3. Dans la boîte de dialogue hello, procédez comme hello suivant :
   
   1. Sélectionnez le compte de stockage du hello avec la clé d’accès hello que vous souhaitez tooupdate.
   2. Vous devez tooupdate hello clé d’accès Bonjour service du Gestionnaire de périphériques StorSimple. Dans ce cas, vous pouvez voir la clé d’accès de stockage de hello. Entrez la nouvelle clé de hello Bonjour **clé d’accès de compte de stockage** boîte. 
   3. Enregistrez vos modifications. La clé d’accès de votre compte de stockage doit maintenant être à jour.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [sécurité StorSimple](storsimple-8000-security.md).
* En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

