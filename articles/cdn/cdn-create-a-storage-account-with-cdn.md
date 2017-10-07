---
title: aaaIntegrate un compte de stockage Azure avec Azure CDN | Documents Microsoft
description: "Découvrez comment le contenu toouse hello réseau de distribution de contenu (CDN) Azure toodeliver à large bande passante en mettant en cache les objets BLOB depuis le stockage Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a>Intégrer un compte de stockage Azure à Azure CDN
CDN peut être activé toocache de contenu à partir de votre stockage Azure. Elle offre aux développeurs une solution globale pour la diffusion de contenu haut débit en mettant en cache des objets BLOB et le contenu statique des instances de calcul sur des nœuds physiques dans hello États-Unis, Europe, Asie, en Australie et en Amérique du Sud.

## <a name="step-1-create-a-storage-account"></a>Étape 1 : création d’un compte de stockage
Utilisez hello suivant la procédure toocreate un nouveau compte de stockage pour un abonnement Azure. Un compte de stockage donne accès aux services de stockage Azure. compte de stockage Hello représente le niveau le plus élevé de l’espace de noms hello pour accéder à chacun des composants de service de stockage Azure hello hello : services, les services de file d’attente et les services de la Table d’objets Blob. Pour plus d’informations, consultez toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).

toocreate un compte de stockage, vous devez être administrateur de service hello ou un coadministrateur pour hello associé abonnement.

> [!NOTE]
> Il existe plusieurs méthodes que vous pouvez utiliser toocreate un compte de stockage, y compris hello portail Azure et Powershell.  Pour ce didacticiel, nous utiliserons hello portail Azure.  
> 
> 

**toocreate un compte de stockage pour un abonnement Azure**

1. Connectez-vous à toohello [Azure Portal](https://portal.azure.com).
2. Dans le coin supérieur gauche hello, sélectionnez **nouveau**. Bonjour **nouveau** boîte de dialogue, sélectionnez **données + stockage**, puis cliquez sur **compte de stockage**.
    
    Hello **créer le compte de stockage** panneau s’affiche.   

    ![Créer un compte de stockage][create-new-storage-account]  

3. Bonjour **nom** , tapez un nom de sous-domaine. Cette entrée peut être composée de 3 à 24 lettres minuscules et chiffres.
   
    Cette valeur devient le nom d’hôte hello dans hello URI qui est utilisé pour adresser des objets Blob, file d’attente ou Table de ressources pour l’abonnement de hello. Pour répondre à une ressource de conteneur Bonjour service Blob, vous utiliseriez un URI Bonjour suivant le format, où  *&lt;StorageAccountLabel&gt;*  fait référence vous avez tapé une valeur toohello **entrer une URL**:
   
    http://*&lt;LibelléCompteStockage&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*
   
    **Important :** hello sous-domaine de hello URL étiquette forms hello du compte de stockage URI et doit être unique parmi tous les services hébergés dans Azure.
   
    Cette valeur est également utilisée comme nom hello de ce compte de stockage dans le portail de hello, ou lors de l’accès par programme de ce compte.
4. Laisser les valeurs par défaut hello pour **modèle de déploiement**, **compte kind**, **performances**, et **réplication**. 
5. Sélectionnez hello **abonnement** que compte de stockage hello est utilisée avec.
6. Sélectionnez ou créez un **groupe de ressources**.  Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Sélectionnez l’emplacement de votre compte de stockage.
8. Cliquez sur **Créer**. Hello de création de compte de stockage hello peut durer plusieurs minutes toocomplete.

## <a name="step-2-enable-cdn-for-hello-storage-account"></a>Étape 2 : Activer le CDN pour le compte de stockage hello

Avec l’intégration les plus récents de hello, vous pouvez maintenant activer CDN pour votre compte de stockage sans quitter votre extension de portail de stockage. 

1. Sélectionnez le compte de stockage hello, rechercher « CDN » ou faites défiler vers le bas à partir du menu de navigation gauche hello, puis cliquez sur « Azure CDN ».
    
    Hello **Azure CDN** panneau s’affiche.

    ![cdn enable navigation][cdn-enable-navigation]
    
2. Créer un nouveau point de terminaison en entrant les informations hello requis
    - **Profil CDN** : vous pouvez en créer un nouveau ou utiliser un profil existant.
    - **Niveau de tarification**: vous ne devez tooselect une tarification niveau si vous créez un nouveau profil CDN.
    - **Nom du point de terminaison CDN** : entrez le nom de point de terminaison de votre choix.

    > [!TIP]
    > point de terminaison CDN Hello créé utilise le nom d’hôte hello de votre compte de stockage comme origine par défaut.

    ![cdn new endpoint creation][cdn-new-endpoint-creation]

3. Après la création, le nouveau point de terminaison hello s’afficheront dans la liste de point de terminaison hello ci-dessus.

    ![cdn storage new endpoint][cdn-storage-new-endpoint]

> [!NOTE]
> Vous pouvez également passer tooAzure CDN extension tooenable CDN. [Didacticiel](#Tutorial-cdn-create-profile).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a>Étape 3 : Activer d’autres fonctionnalités du CDN

À partir du Panneau de « Azure CDN » de compte de stockage, cliquez sur le point de terminaison CDN hello à partir du Panneau de configuration hello liste tooopen CDN. Vous pouvez activer des fonctionnalités supplémentaires du CDN pour la livraison, comme la compression, la chaîne de requête et le filtrage géographique. Vous pouvez également ajouter le point de terminaison CDN domaine personnalisé mappage tooyour et activer HTTPS de domaine personnalisé.
    
![Configuration CDN stockage CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a>Étape 4 : accès au contenu du CDN
Utilisez hello URL du CDN tooaccess mis en cache le contenu sur hello CDN, fourni dans le portail de hello. adresse Hello pour un objet blob mis en cache sera similaire toohello suivantes :

http://<*nom_point_de_terminaison*\>.azureedge.net/<*MonConteneurPublic*\>/<*Nom_blob*\>

> [!NOTE]
> Une fois que vous activez le compte de stockage de tooa accès CDN, tous les objets disponibles publiquement sont éligibles pour la mise en cache de périmètre CDN. Si vous modifiez un objet qui est actuellement mis en cache hello CDN, hello nouveau contenu n’est plus disponible via hello CDN jusqu'à ce que hello CDN actualise son contenu lors de la période de durée de vie contenu hello mis en cache expire.
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a>Étape 5 : Supprimer le contenu à partir de hello CDN
Si vous ne souhaitez plus toocache un objet Bonjour Azure réseau CDN (Content Delivery), vous pouvez effectuer l’une des hello comme suit :

* Vous pouvez rendre hello privé de conteneur au lieu de public. Consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](../storage/blobs/storage-manage-access-to-resources.md) pour plus d’informations.
* Vous pouvez désactiver ou supprimer le point de terminaison CDN hello à l’aide du portail de gestion de hello.
* Vous pouvez modifier votre toorequests plus de temps de réponse service hébergé toono pour l’objet de hello.

Un objet déjà mis en cache dans hello CDN reste dans le cache jusqu'à ce que hello time-to-live pour l’objet de hello expire ou jusqu'à ce que le point de terminaison hello est purgée. Lors de l’expiration de la période de durée de vie de hello, hello CDN vérifiera toosee indique si le point de terminaison CDN hello est toujours valide et objet hello toujours accessible de manière anonyme. Si elle n’est pas le cas, puis les objet hello sont ne sont plus mises en cache.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Comment tooa de contenu CDN tooMap un domaine personnalisé](cdn-map-content-to-custom-domain.md)
* [Activer HTTPS pour votre domaine personnalisé](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
