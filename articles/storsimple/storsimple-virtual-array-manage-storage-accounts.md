---
title: "informations d’identification du compte stockage StorSimple Virtual Array aaaManage | Documents Microsoft"
description: "Explique comment vous pouvez utiliser hello tooadd de page de configuration du Gestionnaire de périphériques StorSimple, modifier, supprimer ou les clés de sécurité hello rotation d’identification de compte de stockage associée hello StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a>Informations d’identification du compte de stockage toomanage d’utiliser le Gestionnaire de périphériques StorSimple pour StorSimple Virtual Array

## <a name="overview"></a>Vue d'ensemble
Hello **Configuration** section du Panneau de service hello StorSimple le Gestionnaire de périphériques de votre tableau virtuel StorSimple présente les paramètres de service global hello qui peuvent être créés dans hello service StorSimple Manager. Ces paramètres peuvent être appliqués tooall hello appareils toohello service connecté et incluant :

* Informations d’identification du compte de stockage
* Enregistrements de contrôle d’accès
  
  ![Tableau de bord du service StorSimple Device Manager](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

Ce didacticiel vous explique comment ajouter, modifier ou supprimer les informations d’identification du compte de stockage pour votre instance StorSimple Virtual Array. informations Hello dans ce didacticiel s’applique uniquement à toohello StorSimple Virtual Array. Pour plus d’informations sur la façon dont les comptes de stockage de toomanage dans la 8000 série, consultez [utilisez hello toomanage du service StorSimple Manager de votre compte de stockage](storsimple-manage-storage-accounts.md).

Compte de stockage informations d’identification contiennent des informations d’identification de hello qui hello périphérique utilise tooaccess votre compte de stockage avec votre fournisseur de services cloud. Pour les comptes de stockage Microsoft Azure, il s’agit des informations d’identification telles que le nom du compte hello et clé d’accès primaire hello.

Sur hello **informations d’identification du compte de stockage** panneau, le compte de stockage de toutes les informations d’identification qui sont créées pour hello facturation d’abonnement sont affichées dans un format tabulaire contenant hello informations suivantes :

* **Nom** – hello compte toohello de nom unique attribué lors de sa création.
* **SSL activé** : indique si hello SSL est activé et la communication de l’appareil-à-cloud est sur un canal sécurisé hello.
  
  ![Section de configuration](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

les tâches les plus courantes Hello liés toostorage d’identification qui peuvent être effectuées sur hello **informations d’identification du compte de stockage** panneau sont :

* Ajout des informations d’identification de compte de stockage
* Modification des informations d’identification de compte de stockage
* Suppression des informations d’identification de compte de stockage

## <a name="types-of-storage-account-credentials"></a>Types d’informations d’identification de compte de stockage
Il existe trois types d’informations d’identification de compte de stockage pouvant être utilisées avec votre appareil StorSimple.

* **Informations d’identification du compte de stockage généré automatiquement** – comme hello nom l’indique, ce type d’informations d’identification du compte de stockage est généré automatiquement lorsque le service de hello est créé. toolearn en savoir plus sur la façon dont ces informations d’identification du compte de stockage sont créée, consultez [créer un nouveau service](storsimple-virtual-array-manage-service.md#create-a-service).
* **informations d’identification du compte de stockage dans l’abonnement au service hello** – il s’agit de compte de stockage Azure hello informations d’identification qui sont associées hello même abonnement que celui du service de hello. toolearn en savoir plus sur la façon dont ces informations d’identification du compte de stockage sont créées, consultez [sur les comptes de stockage Azure](../storage/common/storage-create-storage-account.md).
* **informations d’identification du compte de stockage en dehors de l’abonnement au service hello** : il s’agit de hello stockage Azure d’identification qui n’est pas associées à votre service et probablement hello se trouvait avant le service a été créé.

## <a name="add-a-storage-account-credential"></a>Ajout des informations d’identification de compte de stockage
Vous pouvez ajouter une configuration de service de stockage compte d’identification tooyour StorSimple le Gestionnaire de périphériques en fournissant une valeur unique conviviales accès et le nom des informations d’identification lié compte de stockage toohello. Vous avez également option hello d’activation hello sécurisé Secure sockets layer (SSL) en mode toocreate un canal sécurisé pour la communication réseau entre votre cloud hello et des appareils.

Vous pouvez créer plusieurs comptes pour un fournisseur de services cloud donné. Pendant l’enregistrement des informations d’identification de compte de stockage hello, hello service essaie de toocommunicate avec votre fournisseur de services cloud. informations d’identification Hello et les informations d’accès hello que vous avez fournies sont authentifiées à ce moment-là. Une information d’identification du compte de stockage est créée uniquement si hello authentification réussit. Si l’authentification hello échoue, un message d’erreur approprié s’affiche.

Utilisez hello suit les informations d’identification du compte Azure storage tooadd procédures :

* tooadd une information d’identification du compte de stockage qui a hello même abonnement Azure en tant que service du Gestionnaire de périphériques hello
* tooadd une information d’identification du compte de stockage Azure qui est en dehors de l’abonnement au service Gestionnaire de périphériques hello

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd une information d’identification du compte de stockage qui a hello même abonnement Azure en tant que service du Gestionnaire de périphériques hello

1. Accédez tooyour service Gestionnaire de périphériques, sélectionnez et double-cliquez dessus. Cette opération ouvre hello **vue d’ensemble** panneau.
2. Sélectionnez **informations d’identification du compte de stockage** dans hello **Configuration** section.
3. Cliquez sur **Add**.
4. Bonjour **ajouter un compte de stockage** panneau, hello suivant :
   
    1. Pour **Abonnement**, sélectionnez **Actuel**.
    2. Fournissez le nom hello de votre compte de stockage Azure.
    3. Sélectionnez **activer** toocreate un canal sécurisé pour la communication réseau entre votre cloud de hello et des appareils StorSimple. Sélectionnez **Désactiver** uniquement si vous évoluez au sein d’un cloud privé.
    4. Cliquez sur **Add**. Vous êtes averti une fois le compte de stockage hello est créé avec succès.<br></br>
   
        ![Ajouter une information d’identification de compte de stockage existant](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a>tooadd une information d’identification du compte de stockage Azure qui est en dehors de l’abonnement au service Gestionnaire de périphériques hello

1. Accédez tooyour service Gestionnaire de périphériques, sélectionnez et double-cliquez dessus. Cette opération ouvre hello **vue d’ensemble** panneau.
2. Sélectionnez **informations d’identification du compte de stockage** dans hello **Configuration** section. Celle-ci répertorie toutes les informations d’identification de compte stockage existant associées hello service du Gestionnaire de périphériques StorSimple.
3. Cliquez sur **Add**.
4. Bonjour **ajouter un compte de stockage** panneau, hello suivant :
   
    1. Pour **Abonnement**, sélectionnez **Autre**.
   
    2. Fournissez le nom hello de vos informations d’identification du compte de stockage Azure.
   
    3. Bonjour **clé d’accès de compte de stockage** zone de texte, alimentation hello clé d’accès primaire pour vos informations d’identification du compte de stockage Azure. tooget cette clé, passez le service de stockage Azure toohello, vos informations d’identification du compte de stockage, puis cliquez sur **gérer les clés de compte**. Vous pouvez maintenant copier la clé d’accès primaire hello.
   
    4. tooenable SSL, cliquez sur hello **activer** bouton toocreate un canal sécurisé pour la communication réseau entre votre cloud de service et hello du Gestionnaire de périphériques StorSimple. Cliquez sur hello **désactiver** bouton uniquement si vous opérez dans un cloud privé.
   
    5. Cliquez sur **Add**. Vous êtes averti une fois les informations d’identification de compte de stockage hello sont créée avec succès.

5. informations d’identification de compte de stockage Hello nouvellement créé s’affiche dans le panneau de service de configurer le Gestionnaire de périphériques StorSimple hello sous **informations d’identification du compte de stockage**.
   
    ![Ajouter une information d’identification du compte de stockage en dehors de l’abonnement au service Gestionnaire de périphériques de hello](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a>Modification des informations d’identification de compte de stockage
Vous pouvez modifier des informations d’identification du compte de stockage utilisées par votre appareil. Si vous modifiez une information d’identification du compte de stockage qui est actuellement en cours d’utilisation, toomodify de hello champs disponibles sont la clé d’accès hello et le mode SSL hello pour les informations d’identification de compte de stockage hello. Vous pouvez fournir hello nouvelle clé d’accès ou modifier hello **activer le mode SSL** sélection et d’enregistrer les paramètres de mise à jour de hello.

#### <a name="tooedit-a-storage-account-credential"></a>tooedit une information d’identification du compte de stockage
1. Accédez tooyour service Gestionnaire de périphériques, sélectionnez et double-cliquez dessus. Cette opération ouvre hello **vue d’ensemble** panneau.
2. Sélectionnez **informations d’identification du compte de stockage** dans hello **Configuration** section. Celle-ci répertorie toutes les informations d’identification de compte stockage existant associées hello service du Gestionnaire de périphériques StorSimple.
3. Dans la liste tabulaire hello d’informations d’identification du compte de stockage, sélectionnez et double-cliquez sur compte hello que vous souhaitez toomodify.
4. Dans informations d’identification de compte de stockage hello **propriétés** panneau, hello suivant :
   
   1. Si nécessaire, vous pouvez modifier hello **activer SSL** sélection du mode.
   2. Vous pouvez choisir tooregenerate votre clés des accès des informations d’identification de compte de stockage. Pour plus d’informations, consultez [régénérer les clés de compte de stockage hello](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys). Fournir la clé d’informations d’identification de compte de hello nouveau stockage. Pour un compte de stockage Azure, il s’agit de la clé d’accès primaire hello.
   3. Cliquez sur **enregistrer** haut hello hello **propriétés** paramètres du panneau toosave hello. paramètres de Hello sont mis à jour sur hello **informations d’identification du compte de stockage** panneau.
      
      ![Modification des informations d’identification de compte de stockage](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a>Suppression des informations d’identification de compte de stockage
> [!IMPORTANT]
> Vous ne pouvez pas supprimer des informations d’identification d’un compte de stockage en cours d’utilisation. Si les informations d’identification du compte de stockage sont en cours d’utilisation, vous en êtes informé.
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a>toodelete une information d’identification du compte de stockage
1. Accédez tooyour service Gestionnaire de périphériques, sélectionnez et double-cliquez dessus. Cette opération ouvre hello **vue d’ensemble** panneau.
2. Sélectionnez **informations d’identification du compte de stockage** dans hello **Configuration** section. Celle-ci répertorie toutes les informations d’identification de compte stockage existant associées hello service du Gestionnaire de périphériques StorSimple.
3. Dans la liste tabulaire hello d’informations d’identification du compte de stockage, sélectionnez et double-cliquez sur compte hello que vous souhaitez toodelete.
4. Dans informations d’identification de compte de stockage hello **propriétés** panneau, hello suivant :
   
   1. Cliquez sur **supprimer** informations d’identification de toodelete hello.
   2. Lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui** toocontinue avec suppression des hello. la liste tabulaire Hello est mise à jour tooreflect hello modifications.
      
      ![Suppression des informations d’identification de compte de stockage](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a>Synchronisation des clés des informations d’identification du compte de stockage
Pour des raisons de sécurité, les centres de données exigent souvent une rotation des clés. Un administrateur de Microsoft Azure peut régénérer ou modifier la clé primaire ou secondaire de hello en accédant directement aux informations d’identification du compte de stockage hello (via le service Microsoft Azure Storage de hello). Hello service du Gestionnaire de périphériques StorSimple ne voit pas automatiquement ce changement.

le service de gestionnaire de périphériques StorSimple tooinform hello de modification de hello, vous devez tooaccess hello StorSimple Device Manager service, accès hello stockage d’informations d’identification de compte, puis synchroniser la clé primaire ou secondaire hello (selon l’application a été modifiée). service de Hello puis obtient la clé la plus récente hello, chiffre hello clés et envoie hello chiffré appareil de la clé toohello.

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a>toosynchronize des clés pour les informations d’identification du compte de stockage dans hello même abonnement que le service hello (Azure uniquement)
1. Dans Panneau de lancement du service hello, sélectionnez votre service, double-cliquez sur hello nom du service et puis Bonjour **Configuration** , cliquez sur **informations d’identification du compte de stockage**.
2. Sur hello **informations d’identification du compte de stockage** panneau, dans la liste hello des informations d’identification du compte de stockage, sélectionnez informations d’identification de compte de stockage hello dont les clés que vous souhaitez toosynchronize.
3. Bonjour **propriétés** panneau pour hello sélectionné les informations d’identification du compte de stockage, procédez comme hello suivant :
   
    1. Cliquez sur **Plus**, puis sur **Synchroniser la clé d’accès**.
   
    2. Lorsque vous êtes invité à confirmer l’opération, cliquez sur **synchroniser la clé** synchronisation de hello toocomplete.
    
4. Bonjour service du Gestionnaire de périphériques StorSimple, vous devez clé hello tooupdate qui a été précédemment modifié Bonjour service Microsoft Azure Storage. Bonjour **clé de compte de stockage synchroniser** panneau, si la clé d’accès primaire hello a été modifiée (régénérée), cliquez sur primaire, puis cliquez sur **synchroniser la clé**. Si la clé secondaire de hello a été modifié, cliquez sur **secondaire**, puis cliquez sur **synchroniser la clé**.
   
    ![Synchroniser la clé d’accès](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[administrer votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

