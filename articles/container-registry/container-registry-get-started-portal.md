---
title: "Registre Docker privé aaaCreate - portail Azure | Documents Microsoft"
description: "Commencer à créer et gérer des registres de conteneur Docker privés avec hello portail Azure"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a>Créer un Registre de conteneur Docker privé à l’aide de hello portail Azure
Hello toocreate portail Azure un Registre de conteneur et gérer ses paramètres. Vous pouvez également créer et gérer des registres de conteneur à l’aide de hello [Azure CLI 2.0 commandes](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) ou par programme avec hello Registre de conteneur [l’API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).

Pour des informations et des concepts, consultez [hello vue d’ensemble](container-registry-intro.md).

## <a name="create-a-container-registry"></a>Créer un registre de conteneur
1. Bonjour [portail Azure](https://portal.azure.com), cliquez sur **+ nouveau**.
2. Marketplace hello de recherche pour **Registre de conteneur Azure**.
3. Sélectionnez **Azure Container Registry**, avec l’éditeur **Microsoft**.
    ![Service Container Registry dans Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. Cliquez sur **Créer**. Hello **Registre de conteneur Azure** panneau s’affiche.

    ![Paramètres de Container Registry](./media/container-registry-get-started-portal/container-registry-settings.png)
5. Bonjour **Registre de conteneur Azure** panneau, entrez hello informations suivantes. Une fois ces opérations effectuées, cliquez sur **Créer**.

    a. **Nom du registre** : Un nom de domaine global unique et de niveau supérieur pour votre registre spécifique. Dans cet exemple, le nom de Registre hello est *myRegistry01*, mais remplacer par un nom unique de votre choix. nom de Hello peut contenir que des lettres et des chiffres.

    b. **Groupe de ressources**: sélectionnez un existant [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) ou nom du type hello pour un nouveau.

    c. **Emplacement**: sélectionnez un emplacement de centre de données Azure où le service de hello est [disponible](https://azure.microsoft.com/regions/services/), tel que **Amérique du Sud**.

    d. **L’utilisateur Admin**: Si vous le souhaitez, activer un Registre de hello tooaccess admin utilisateur. Vous pouvez modifier ce paramètre après avoir créé le Registre de hello.

      > [!IMPORTANT]
      > En outre tooproviding accéder via un compte d’utilisateur administrateur, les registres de conteneur prend en charge l’authentification soutenue par des principaux du service Azure Active Directory. Pour plus d’informations et pour connaître les éléments à prendre en considération, consultez la section relative à [l’authentification auprès d’un conteneur](container-registry-authentication.md).
      >

    e. **Compte de stockage**: utiliser toocreate de paramètre par défaut hello un [compte de stockage](../storage/common/storage-introduction.md), ou sélectionnez un compte de stockage existant dans hello même emplacement. Pour l’instant, l’offre Stockage Premium n’est pas prise en charge.

## <a name="manage-registry-settings"></a>Gérer les paramètres du registre
Après avoir créé le Registre de hello, recherche hello paramètres du Registre en partant de hello **conteneur registres** panneau dans le portail de hello. Par exemple, vous devrez peut-être toolog de paramètres hello dans le Registre de tooyour, ou peut souhaité tooenable ou désactiver l’utilisateur admin hello.

1. Sur hello **conteneur registres** panneau, cliquez sur nom hello de votre Registre.

    ![Panneau Container Registry](./media/container-registry-get-started-portal/container-registry-blade.png)
2. Cliquez sur les paramètres d’accès toomanage, **clé d’accès**.

    ![Accès à Container Registry](./media/container-registry-get-started-portal/container-registry-access.png)
3. Notez hello suivant les paramètres :

   * **Serveur de connexion** -nom qualifié complet de hello vous utilisez toolog dans le Registre de toohello. Dans cet exemple, il s’agit de `myregistry01.azurecr.io`.
   * **L’utilisateur Admin** - activer/désactiver tooenable ou désactiver le compte d’utilisateur admin du Registre hello.
   * **Nom d’utilisateur** et **mot de passe** -hello les informations d’identification du compte d’utilisateur administrateur hello (si activé) vous pouvez utiliser toolog dans le Registre de toohello. Vous pouvez éventuellement régénérer les mots de passe hello. Deux mots de passe sont créés afin que vous pouvez maintenir Registre toohello de connexions à l’aide d’un mot de passe pendant la régénération de hello autre mot de passe. tooauthenticate avec un principal de service au lieu de cela, consultez [authentifier avec un Registre de conteneur Docker privé](container-registry-authentication.md).

## <a name="next-steps"></a>Étapes suivantes
* [Push de votre première image à l’aide de hello Docker CLI](container-registry-get-started-docker-cli.md)
