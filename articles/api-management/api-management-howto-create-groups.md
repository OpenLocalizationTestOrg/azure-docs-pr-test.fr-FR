---
title: "comptes de développeur aaaManage à l’aide de groupes de gestion des API Azure | Documents Microsoft"
description: "Découvrez comment les développeurs toomanage comptes à l’aide groupes dans Gestion des API Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a>Le mode développeur de toomanage groupes toocreate et l’utilisation de comptes dans Gestion des API Azure
Gestion des API, les groupes sont visibilité de hello utilisé toomanage de toodevelopers de produits. Produits sont premier toogroups de visible effectuées, et ensuite les développeurs dans ces groupes peuvent afficher et s’abonner toohello les produits qui sont associés aux groupes de hello. 

Gestion des API a hello suivant groupes système immuables.

* **Administrateurs** : les administrateurs d’abonnements Azure sont membres de ce groupe. Administrateurs de gérer des instances de service de gestion des API, création hello API, opérations et produits qui sont utilisés par les développeurs.
* **Développeurs** : les utilisateurs authentifiés du portail des développeurs appartiennent à ce groupe. Les développeurs sont des clients hello générer des applications à l’aide de votre API. Les développeurs sont accordées portail des développeurs accès toohello et générer des applications qui appellent des opérations d’une API hello.
* **Invités** -non authentifié utilisateurs du portail développeur, tels que les clients potentiels en visitant le portail des développeurs hello d’une baisse d’instance gestion des API dans ce groupe. Ils peuvent bénéficier de certain accès en lecture seule, par exemple, hello capacité tooview API mais pas de les appellent.

Dans les groupes de système toothese plus, les administrateurs peuvent créer des groupes personnalisés ou [tirer parti des groupes externes dans les clients Azure Active Directory associés][leverage external groups in associated Azure Active Directory tenants]. Groupes personnalisés et externes peuvent être utilisés avec des groupes de systèmes en offrant aux développeurs une visibilité et accéder aux produits de tooAPI. Par exemple, vous pouvez créer un groupe personnalisé pour les développeurs affiliés à spécifiques à une organisation partenaire et les autoriser à accéder toohello API à partir d’un produit contenant uniquement des API pertinentes. Un utilisateur peut être membre de plusieurs groupes.

Ce guide explique comment les administrateurs de l'instance Gestion des API peuvent ajouter de nouveaux groupes et les associer à des produits et des développeurs.

> [!NOTE]
> En outre toocreating et gérer des groupes dans le portail de publication hello, vous pouvez créer et gérer vos groupes à l’aide des API REST de gestion des API de hello [groupe](https://msdn.microsoft.com/library/azure/dn776329.aspx) entité.
> 
> 

## <a name="create-group"></a>Création d’un groupe
toocreate un nouveau groupe, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API. Cela vous prend un portail de publication de gestion des API toohello.

![Portail des éditeurs][api-management-management-console]

> Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.
> 
> 

Cliquez sur **groupes** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **ajouter un groupe**.

![Ajouter un nouveau groupe][api-management-add-group]

Entrez un nom unique pour le groupe de hello et une description facultative, puis cliquez sur **enregistrer**.

![Ajouter un nouveau groupe][api-management-add-group-window]

nouveau groupe de Hello s’affiche dans Bonjour groupes onglet tooedit Bonjour **nom** ou **Description** hello groupe de, cliquez sur nom hello du groupe hello dans la liste de hello. groupe de hello toodelete, cliquez sur **supprimer**.

![Group added][api-management-new-group]

Maintenant que hello groupe est créé, il peut être associé avec les produits et les développeurs.

## <a name="associate-group-product"></a>Association d’un groupe à un produit
tooassociate un groupe avec un produit, cliquez sur **produits** de hello **gestion des API** hello menu gauche, puis cliquez sur nom hello de produit de votre choix hello.

![Set visibility][api-management-add-group-to-product]

Sélectionnez hello **visibilité** onglet tooadd et supprimer des groupes et des groupes en cours de tooview hello pour le produit de hello. tooadd ou supprimez des groupes, vérifiez ou désactivez les cases à cocher hello pour hello souhaitée des groupes et cliquez sur **enregistrer**.

![Set visibility][api-management-add-group-to-product-visibility]

> [!NOTE]
> tooadd les groupes Azure Active Directory, consultez [comment tooauthorize développeur comptes à l’aide Azure Active Directory dans la gestion des API Azure](api-management-howto-aad.md).
> 
> groupes tooconfigure hello **visibilité** pour un produit, cliquez sur **gérer les groupes**.
> 
> 

Une fois qu’un produit est associé à un groupe, les développeurs de ce groupe peuvent afficher et s’abonner toohello produit.

## <a name="associate-group-developer"></a>Association des groupes aux développeurs
groupes tooassociate avec les développeurs, cliquez sur **utilisateurs** de hello **gestion des API** menu hello gauche, puis hello case à cocher en regard des développeurs de hello vous souhaitez tooassociate avec un groupe.

![Ajouter le développeur toogroup][api-management-add-group-to-developer]

Une fois que hello souhaité les développeurs sont vérifiées, cliquez sur groupe hello Bonjour **ajouter tooGroup** liste déroulante. Les développeurs peuvent être supprimés des groupes à l’aide de hello **supprimer du groupe** liste déroulante. 

![Développeurs][api-management-add-group-to-developer-saved]

Une fois que l’association de hello est ajoutée entre le développeur de hello et groupe de hello, vous pouvez les consulter dans hello **utilisateurs** onglet.

## <a name="next-steps"></a>Étapes suivantes
* Une fois qu’un développeur est ajouté tooa groupe, ils peuvent afficher et s’abonner produits toohello associés à ce groupe. Pour plus d’informations, consultez la page [Création et publication d’un produit dans Gestion des API Azure][How create and publish a product in Azure API Management].
* En outre toocreating et gérer des groupes dans le portail de publication hello, vous pouvez créer et gérer vos groupes à l’aide des API REST de gestion des API de hello [groupe](https://msdn.microsoft.com/library/azure/dn776329.aspx) entité.

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
