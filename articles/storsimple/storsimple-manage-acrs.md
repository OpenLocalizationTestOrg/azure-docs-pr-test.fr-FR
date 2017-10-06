---
title: "enregistrements de contrôle d’accès aaaManage dans StorSimple | Documents Microsoft"
description: "Décrit comment le contrôle d’accès toouse enregistre toodetermine (ACR) les hôtes qui peuvent se connecter volume tooa sur l’appareil StorSimple hello."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Utiliser des enregistrements de contrôle d’accès hello StorSimple Manager service toomanage
## <a name="overview"></a>Vue d'ensemble
Enregistrements de contrôle d’accès (ACR) permettent de toospecify les hôtes qui peuvent se connecter volume tooa sur l’appareil StorSimple hello. ACR sont définies les volume spécifique tooa et contenir hello iSCSI (IQN) de noms qualifiés d’hôtes de hello. Quand un hôte tente de tooconnect tooa volume, les appareils hello vérifie hello QU'ACR associé à ce volume pour le nom IQN de hello et si une correspondance est trouvée, hello est établie. la section sur hello des enregistrements de contrôle d’accès Hello **configurer** page affiche tous les enregistrements de contrôle d’accès hello avec hello correspondant iqn des hôtes de hello.

Ce didacticiel explique hello suivant ACR tâches :

* Ajouter un enregistrement de contrôle d’accès 
* Modifier un enregistrement de contrôle d’accès 
* Supprimer un enregistrement de contrôle d’accès 

> [!IMPORTANT]
> * Lorsque vous affectez un volume de tooa ACR, prenez soin que volume de hello n'est pas accédé simultanément par plus d’un hôte non cluster, car cela peut endommager le volume de hello. 
> * Lorsque vous supprimez un ACR d’un volume, assurez-vous que cet hôte correspondant hello n’accède pas aux volumes de hello, car la suppression de hello pourrait entraîner une interruption en lecture-écriture.
> 
> 

## <a name="add-an-access-control-record"></a>Ajouter un enregistrement de contrôle d’accès
Vous utilisez le service StorSimple Manager hello **configurer** page tooadd ACR. En général, vous associez un enregistrement de contrôle d’accès à un volume.

Effectuer hello suivant les étapes tooadd un ACR.

#### <a name="tooadd-an-access-control-record"></a>tooadd un enregistrement de contrôle d’accès
1. Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur le nom du service hello, puis cliquez sur hello **configurer** onglet.
2. Bonjour tabulaire sous **enregistrements de contrôle d’accès**, fournissez un **nom** pour votre ACR.
3. Fournissez le nom IQN de hello de votre hôte Windows sous **nom de l’initiateur iSCSI**. tooget hello IQN de votre hôte Windows Server, procédez comme hello suivant :
   
   * Démarrez l’initiateur iSCSI Microsoft hello sur votre hôte Windows.
   * Bonjour **propriétés de l’initiateur iSCSI** fenêtre hello **Configuration** , sélectionnez et copiez les chaîne hello de hello **nom de l’initiateur** champ.
   * Collez cette chaîne Bonjour **nom de l’initiateur iSCSI** champ sur la table d’ACR hello Bonjour portail Azure classic.
4. Cliquez sur **enregistrer** hello toosave nouvellement créé ACR. Hello tabulaires liste va être mis à jour tooreflect cet ajout.

## <a name="edit-an-access-control-record"></a>Modifier un enregistrement de contrôle d’accès
Vous utilisez hello **configurer** page Bonjour tooedit de portail classique Azure ACR. 

> [!NOTE]
> Vous pouvez modifier uniquement les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation. tooedit qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.
> 
> 

Effectuer hello suivant les étapes tooedit un ACR.

#### <a name="tooedit-an-access-control-record"></a>tooedit un enregistrement de contrôle d’accès
1. Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur le nom du service hello, puis cliquez sur hello **configurer** onglet.
2. Dans hello tabulaire la liste des enregistrements de contrôle d’accès hello, pointez sur hello ACR que vous souhaitez toomodify.
3. Fournir un nouveau nom et/ou le nom IQN hello ACR.
4. Cliquez sur **enregistrer** toosave hello modifié ACR. Hello tabulaires liste va être mis à jour tooreflect cette modification.

## <a name="delete-an-access-control-record"></a>Supprimer un enregistrement de contrôle d’accès
Vous utilisez hello **configurer** page Bonjour toodelete de portail classique Azure ACR. 

> [!NOTE]
> Vous pouvez uniquement supprimer les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation. toodelete qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.
> 
> 

Effectuer hello suivant les étapes toodelete un enregistrement de contrôle d’accès.

#### <a name="toodelete-an-access-control-record"></a>toodelete un enregistrement de contrôle d’accès
1. Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur le nom du service hello, puis cliquez sur hello **configurer** onglet.
2. Dans hello tabulaire la liste des enregistrements de contrôle d’accès (ACR) hello, pointez sur hello ACR que vous souhaitez toodelete.
3. Une icône de suppression (**x**) apparaît dans la colonne de droite extrêmes hello pour hello ACR que vous sélectionnez. Cliquez sur hello **x** hello de toodelete icône ACR.
4. Lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui** toocontinue avec suppression des hello. la liste tabulaire Hello sera mis à jour tooreflect hello suppression.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [gestion des volumes StorSimple](storsimple-manage-volumes.md).
* En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).

