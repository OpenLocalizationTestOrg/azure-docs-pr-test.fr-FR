---
title: "aaaHow tooUse contrôle d’accès en fonction du rôle dans la gestion des API Azure | Documents Microsoft"
description: "Découvrez comment toouse hello rôles intégrés et créer des rôles personnalisés dans Gestion des API Azure"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>Comment tooUse en fonction du rôle de contrôle d’accès dans la gestion des API Azure
Gestion des API Azure s’appuie sur la gestion de l’accès affinée tooenable du contrôle d’accès (RBAC) pour les services de gestion des API et des entités (par exemple, API, des stratégies). Cet article vous donne une vue d’ensemble des rôles intégrés et personnalisés de hello dans Gestion des API. Si vous souhaitez plus d’informations sur la gestion de l’accès Bonjour portail Azure, consultez [commencer avec la gestion des accès Bonjour portail Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>Rôles intégrés
Actuellement, gestion des API fournit 3 rôles intégrés et ajoute 2 rôles plus Bonjour futur proche. Ces rôles peuvent être affectés à différentes étendues, notamment l’abonnement, le groupe de ressources et chacune des instances Gestion des API. Par exemple, si rôle de « Azure API Management Service lecteur » hello est désignée comme utilisateur tooan au niveau de groupe de ressources hello, puis hello utilisateur aura accès en lecture tooall gestion des API instances à l’intérieur du groupe de ressources hello. 

Hello tableau suivant fournit de brèves descriptions de hello rôles intégrés. Vous pouvez attribuer ces rôles à l’aide de hello portail Azure ou autres outils y compris Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [une interface de ligne](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), et [API REST](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Pour plus d’informations sur la façon tooassign des rôles intégrés, consultez [utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).

| Rôle          | Accès en lecture<sup>[1]</sup> | Accès en écriture<sup>[2]</sup> | Création, suppression et mise à l’échelle d’un service, configuration d’un VPN et d’un domaine personnalisé | Accès toolegacy Publsiher Portal | Description
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Collaborateur du service Gestion des API Azure | ✓ | ✓  | ✓  | ✓ | Super utilisateur. A complète des services de gestion de CRUD accès tooAPI et des entités (par exemple, les API, les stratégies). Possède l’accès toohello publisher hérité portail. |
| Lecteur du service Gestion des API Azure | ✓ | | || A des entités et des services de gestion tooAPI accès en lecture seule. |
| Opérateur du service Gestion des API Azure | ✓ | | ✓ | | Peut gérer les services Gestion des API, mais pas les entités.|
| Éditeur du service Gestion des API Azure<sup>*</sup> | ✓ | ✓ | |  | Peut gérer les entités Gestion des API, mais pas les services.|
| Gestionnaire de contenu Gestion des API Azure<sup>*</sup> | ✓ | | | ✓ | Peut gérer le portail des développeurs. Accès en lecture seule tooservices et des entités.|

<sup>[1] services de gestion de tooAPI l’accès en lecture et d’entités (par exemple, API, des stratégies)</sup>

<sup>Services de gestion de l’accès en écriture [2] tooAPI et des entités à l’exception suivantes opeartions : (1) Instance création, suppression et la mise à l’échelle de paramétrage de nom de domaine 2) VPN configuration personnalisée (3)</sup>

<sup>\*rôle de l’éditeur de Service Hello sera disponible après que nous migré toutes les interface utilisateur d’administration de hello existant publisher portail toohello portail Azure. Hello rôle Gestionnaire de contenu seront disponible une fois le portail de publication hello est refactorisé tooonly contiennent le portail des développeurs fonctionnalités connexes toomanaging hello.</sup>  


## <a name="custom-roles"></a>Rôles personnalisés
Si aucun des rôles intégrés de hello répondent à vos besoins spécifiques, des rôles personnalisés peuvent être créés tooprovide plus granulaire accéder à la gestion des entités de gestion des API. Par exemple, vous pouvez créer un rôle personnalisé qui a accès en lecture seule tooan service de gestion des API, mais d’API spécifique de tooone un accès en écriture. toolearn plus d’informations sur les rôles personnalisés, consultez [des rôles personnalisés dans Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles). 

Lorsque vous créez un rôle personnalisé, il est plus facile toostart avec l’un des rôles intégrés de hello. Modifier hello attributs tooadd hello Actions, NotActions ou AssignableScopes, puis enregistrer les modifications de hello sous un nouveau rôle. Hello exemple suivant commence par le rôle de « Azure API Management Service lecteur » hello et crée un rôle personnalisé appelé « Éditeur d’API calculatrice ». rôle personnalisé de Hello peut être affecté uniquement tooa QU'API spécifique sera donc uniquement a accès toothat API. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>Regarder une vidéo de présentation

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>Étapes suivantes

* En savoir plus sur le contrôle d’accès en fonction du rôle dans Azure
  * [Prise en main Bonjour Azure portail de gestion de l’accès](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Rôles personnalisés dans le contrôle d’accès en fonction du rôle (RBAC) Azure](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
