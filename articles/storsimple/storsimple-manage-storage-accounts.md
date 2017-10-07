---
title: aaaManage votre compte de stockage StorSimple | Documents Microsoft
description: "Explique comment vous pouvez utiliser hello tooadd de page de configuration de StorSimple Manager, modifier, supprimer ou les clés de sécurité hello rotation pour un compte de stockage."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 78f408818ee8532dfaac445200048145547c987c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-storage-account"></a>Utilisez hello StorSimple Manager service toomanage votre compte de stockage
## <a name="overview"></a>Vue d'ensemble
Hello **configurer** page présente tous les paramètres de service global hello qui peuvent être créés dans hello service StorSimple Manager. Ces paramètres peuvent être appliqués tooall hello appareils toohello service connecté et incluant :

* Comptes de stockage 
* Modèles de bande passante 
* Enregistrements de contrôle d’accès 

Ce didacticiel explique comment vous pouvez utiliser hello **configurer** page tooadd, modifier ou supprimer les comptes de stockage ou la rotation des clés de sécurité hello pour un compte de stockage.

 ![Page Configurer](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

Comptes de stockage contiennent les informations d’identification hello hello périphérique utilise tooaccess votre compte de stockage avec votre fournisseur de services cloud. Pour les comptes de stockage Microsoft Azure, il s’agit des informations d’identification telles que le nom du compte hello et clé d’accès primaire hello. 

Sur hello **configurer** page, le stockage de tous les comptes qui sont créés pour hello facturation d’abonnement sont affichés dans un format tabulaire contenant hello informations suivantes :

* **Nom** – hello compte toohello de nom unique attribué lors de sa création.
* **SSL activé** : indique si hello SSL est activé et la communication de l’appareil-à-cloud est sur un canal sécurisé hello.
* **Utilisé par** – hello du nombre de volumes à l’aide du compte de stockage hello.

les tâches les plus courantes Hello liées toostorage les comptes qui peuvent être effectuées sur hello **configurer** sont :

* Ajout d’un compte de stockage 
* Modification d’un compte de stockage 
* Suppression d'un compte de stockage 
* Rotation des clés de comptes de stockage 

## <a name="types-of-storage-accounts"></a>Types de compte de stockage
Vous pouvez utiliser trois types de compte de stockage avec votre appareil StorSimple.

* **Les comptes de stockage généré automatiquement** – comme hello nom l’indique, ce type de compte de stockage est généré automatiquement lorsque le service de hello est créé. toolearn en savoir plus sur la création de ce compte de stockage, consultez [étape 1 : créer un nouveau service](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service) dans [déployer l’appareil StorSimple local](storsimple-deployment-walkthrough.md). 
* **Comptes de stockage dans l’abonnement au service hello** – il s’agit des comptes de stockage Azure hello associés hello même abonnement que celui du service de hello. toolearn en savoir plus sur la façon dont ces comptes de stockage sont créés, consultez [sur les comptes de stockage Azure](../storage/common/storage-create-storage-account.md). 
* **Comptes de stockage en dehors de l’abonnement au service hello** : il s’agit des comptes de stockage Azure hello qui ne sont pas associés à votre service et probablement hello se trouvait avant le service a été créé.

## <a name="add-a-storage-account"></a>Ajout d’un compte de stockage
Vous pouvez ajouter un compte de stockage en fournissant un unique conviviales accès et le nom des informations d’identification lié toohello compte de stockage (avec le fournisseur de services de cloud computing spécifié hello). Vous avez également option hello d’activation hello sécurisé Secure sockets layer (SSL) en mode toocreate un canal sécurisé pour la communication réseau entre votre cloud hello et des appareils.

Vous pouvez créer plusieurs comptes pour un fournisseur de services cloud donné. Sachez, toutefois, qu’après la création d’un compte de stockage, vous ne pouvez pas modifier le fournisseur de services de cloud hello.

Pendant l’enregistrement de compte de stockage hello, hello service essaie de toocommunicate avec votre fournisseur de services cloud. informations d’identification Hello et les informations d’accès hello que vous avez fournies sont authentifiées à ce stade. Un compte de stockage est créé uniquement si hello authentification réussit. Si l’authentification hello échoue, un message d’erreur s’affichera.

Les comptes de stockage Resource Manager créés dans le portail Azure sont également pris en charge dans StorSimple. Hello, comptes de stockage seront afficheront pas dans la liste déroulante de hello pour la sélection lors de la tentative de toocreate un conteneur de volumes, le Gestionnaire de ressources hello uniquement stockage comptes créés dans le portail Azure classic de hello seront affichera. Les comptes de stockage de gestionnaire de ressources devez toobe ajouté à l’aide de hello procédure tooadd est un compte de stockage décrites ci-dessous.

> [!NOTE]
> procédure de Hello pour l’ajout d’un compte de stockage varie en fonction de la version du logiciel StorSimple hello que vous utilisez. Être vraiment toofollow hello procédure correcte pour votre version de StorSimple.
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a>Modification d’un compte de stockage
Vous pouvez modifier un compte de stockage utilisé par un conteneur de volumes. Si vous modifiez un compte de stockage qui est actuellement en cours d’utilisation, hello uniquement les toomodify disponibles champ agit hello clé d’accès pour le compte de stockage hello. Vous pouvez fournir la clé d’accès de stockage de hello et enregistrer les paramètres de mise à jour de hello.

#### <a name="tooedit-a-storage-account"></a>tooedit un compte de stockage
1. Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur le nom du service hello, puis cliquez sur **configurer**.
2. Cliquez sur **Ajouter/modifier des comptes de stockage**.
3. Bonjour **Ajouter/modifier les comptes de stockage** boîte de dialogue :
   
   1. Dans la liste déroulante de hello de **comptes de stockage**, choisissez un compte existant que vous aimeriez toomodify. Cela peut également inclure des comptes de stockage hello qui ont été générés automatiquement lors de la création du service hello.
   2. Si nécessaire, vous pouvez modifier hello **activer le Mode SSL** sélection.
   3. Vous pouvez choisir toorotate vos clés de l’accès de compte de stockage. Consultez [rotation des comptes de stockage de clé](#key-rotation-of-storage-accounts) pour plus d’informations sur la façon dont tooperform permutation des clés.
   4. Cliquez sur une icône de coche hello ![icône de coche](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) toosave les paramètres hello. paramètres de Hello seront mise à jour sur hello **configurer** page. Cliquez sur **enregistrer** toosave hello qui vient d’être mis à jour que les paramètres.
      
      ![Modification d’un compte de stockage](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a>Suppression d'un compte de stockage
> [!IMPORTANT]
> Vous pouvez supprimer un compte de stockage uniquement s’il n’est pas utilisé par un conteneur de volumes. Si un compte de stockage est utilisé par un conteneur de volume, tout d’abord supprimer le conteneur de volume de hello et puis supprimez le compte de stockage hello associé.
> 
> 

#### <a name="toodelete-a-storage-account"></a>toodelete un compte de stockage
1. Sur la page d’accueil hello StorSimple Manager service, sélectionnez votre service, double-cliquez sur le nom du service hello, puis cliquez sur **configurer**.
2. Dans la liste tabulaire hello de comptes de stockage, pointez sur compte hello que toodelete.
3. Une icône de suppression (**x**) apparaît dans la colonne de droite extrêmes hello pour ce compte de stockage. Cliquez sur hello **x** informations d’identification d’icône toodelete hello.
4. Lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui** toocontinue avec suppression des hello. la liste tabulaire Hello sera mis à jour tooreflect hello modifications.

## <a name="key-rotation-of-storage-accounts"></a>Rotation des clés de comptes de stockage
Pour des raisons de sécurité, les centres de données exigent souvent une rotation des clés. 

> [!NOTE]
> Hello, suivant la procédure de rotation de la rotation des clés hello et les informations s’appliquent uniquement des comptes de stockage Azure tooMicrosoft. Si vous utilisez un autre fournisseur de services cloud, vous pouvez gérer les clés de compte de stockage via le tableau de bord de ce fournisseur.
> 
> 

Chaque abonnement Microsoft Azure peut être associé à un ou plusieurs comptes de stockage. comptes d’accès de toothese Hello est contrôlé par abonnement de hello et touches d’accès pour chaque compte de stockage. 

Lorsque vous créez un compte de stockage, Microsoft Azure génère deux clés d’accès de stockage de 512 bits sont utilisés pour l’authentification lors de l’accès au compte de stockage hello. Avoir deux clés d’accès de stockage vous permet de clés de hello tooregenerate avec aucun service de stockage tooyour d’interruption ou le service d’accès toothat. clé qui est actuellement en cours d’utilisation Hello est hello *principal* clé hello et la clé de sauvegarde est référencé tooas hello *secondaire* clé. Vous devez fournir une de ces deux clés lorsque votre appareil Microsoft Azure StorSimple accède à votre fournisseur de services de stockage cloud.

## <a name="what-is-key-rotation"></a>La rotation des clés, de quoi s’agit-il ?
En règle générale, les applications qu’un seul de hello clés tooaccess utilisent vos données. Après un certain temps, vous pouvez avoir vos applications pour basculer la deuxième clé de toousing hello. Après avoir basculé votre clé secondaire toohello d’applications, vous pouvez mettre hors service de la première clé de hello et puis générer une nouvelle clé. À l’aide de deux clés de hello de cette manière permet à vos données de toohello d’accès aux applications sans temps mort.

les clés de compte de stockage Hello sont toujours stockées dans le service hello sous forme chiffrée. Toutefois, elles peuvent être réinitialisées via hello service StorSimple Manager. service de Hello peut obtenir la clé primaire de hello et la clé secondaire pour tous les hello Bonjour même abonnement, y compris les comptes créés dans le service de stockage hello ainsi que les comptes de stockage par défaut hello généré, les comptes de stockage lorsque hello service StorSimple Manager création du service. Hello service du service StorSimple Manager sera obtient toujours ces clés à partir de hello portail Azure classic et les stocke sous forme chiffrée.

## <a name="rotation-workflow"></a>Workflow de rotation
Un administrateur de Microsoft Azure peut régénérer ou modifier la clé primaire ou secondaire de hello en accédant directement au compte de stockage hello (via le service Microsoft Azure Storage de hello). Hello service StorSimple Manager ne voit pas automatiquement ce changement.

le service de StorSimple Manager tooinform hello de modification de hello, vous devez le service StorSimple Manager tooaccess hello, accéder au compte de stockage hello, puis synchroniser la clé primaire ou secondaire hello (selon l’application a été modifiée). service de Hello puis obtient la clé la plus récente hello, chiffre hello clés et envoie hello chiffré appareil de la clé toohello.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service-azure-only"></a>toosynchronize des clés pour les comptes de stockage dans hello même abonnement que le service hello (Azure uniquement)
1. Sur hello **Services** , cliquez sur hello **configurer** onglet.
2. Cliquez sur **Ajouter/modifier des comptes de stockage**.
3. Dans la boîte de dialogue hello, procédez comme hello suivant :
   
   1. Sélectionnez le compte de stockage du hello avec la clé de hello que vous souhaitez toosynchronize. les clés de compte de stockage Hello sont chiffrés lorsqu’ils sont affichés.
   2. Bonjour service StorSimple Manager, vous devez clé hello tooupdate qui a été précédemment modifié Bonjour service Microsoft Azure Storage. Si la clé d’accès primaire hello a été modifiée (régénérée), cliquez sur **synchroniser la clé primaire**. Si la clé secondaire de hello a été modifié, cliquez sur **synchroniser la clé secondaire**.
      
      ![synchroniser les clés](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>toosynchronize clés pour les comptes de stockage en dehors de l’abonnement au service hello
1. Sur hello **Services** , cliquez sur hello **configurer** onglet.
2. Cliquez sur **Ajouter/modifier des comptes de stockage**.
3. Dans la boîte de dialogue hello, procédez comme hello suivant :
   
   1. Sélectionnez le compte de stockage du hello avec la clé d’accès hello que vous souhaitez tooupdate.
   2. Vous devez tooupdate hello clé d’accès Bonjour service StorSimple Manager. Dans ce cas, vous pouvez voir la clé d’accès de stockage de hello. Entrez la nouvelle clé de hello Bonjour **clé d’accès de compte de stockage**zone y. 
   3. Enregistrez vos modifications. La clé d’accès de votre compte de stockage doit maintenant être à jour.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [sécurité StorSimple](storsimple-security.md).
* En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).

