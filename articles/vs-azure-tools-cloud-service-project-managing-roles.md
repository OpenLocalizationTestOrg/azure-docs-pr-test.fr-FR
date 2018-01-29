---
title: "Gestion des rôles dans Azure Cloud Services avec Visual Studio | Microsoft Docs"
description: "Découvrez comment ajouter et supprimer des rôles dans Azure Cloud Services avec Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 6ed857b857cf8c14506ca39725c214a7fea4fc95
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Gestion des rôles dans Azure Cloud Services avec Visual Studio
Après avoir créé votre projet de service cloud Azure, vous pouvez ajouter de nouveaux rôles ou supprimer des rôles existants. Vous pouvez également importer un projet existant et le convertir à un rôle. Par exemple, vous pouvez importer une application web ASP.NET et la désigner comme rôle web.

## <a name="adding-a-role-to-an-azure-cloud-service"></a>Ajout d’un rôle à un service cloud Azure
Les étapes suivantes vous guident dans le processus d’ajout d’un rôle web ou de travail à un projet de service cloud Azure dans Visual Studio.

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, développez le nœud du projet

1. Cliquez sur le nœud **Rôles** pour afficher le menu contextuel. Dans le menu contextuel, sélectionnez **Ajouter**, puis sélectionnez un rôle web ou un rôle de travail existant à partir de la solution actuelle, ou créez un projet de rôle web ou de travail. Vous pouvez également sélectionner un projet approprié, par exemple un projet d’application web ASP.NET, et l’associer à un projet de rôle.

    ![Options de menu pour ajouter un rôle à un projet de service cloud Azure](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Suppression d’un rôle à partir d’un service cloud Azure
Les étapes suivantes vous guident dans le processus de suppression d’un rôle web ou de travail à partir d’un projet de service cloud Azure dans Visual Studio.

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, développez le nœud du projet

1. Développez le nœud **Rôles**.

1. Cliquez avec le bouton droit sur le nœud que vous souhaitez supprimer, puis, dans le menu contextuel, sélectionnez **Supprimer**. 

    ![Options de menu pour ajouter un rôle à un service cloud Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-to-an-azure-cloud-service-project"></a>Réajout d’un rôle à un projet de service cloud Azure
Si vous supprimez un rôle dans votre projet de service cloud mais décidez ultérieurement de rétablir le rôle dans le projet, seuls la déclaration de rôle et les attributs de base, tels que les informations de diagnostic et les points de terminaison, sont ajoutés. Aucune ressource ou référence supplémentaire n’est ajoutée au fichier `ServiceDefinition.csdef` ou au fichier `ServiceConfiguration.cscfg`. Si vous souhaitez ajouter ces informations, vous devez les ajouter manuellement à ces fichiers.

Par exemple, vous pouvez supprimer un rôle de service web et décider ultérieurement de rétablir ce rôle dans votre solution. Dans ce cas, une erreur se produit. Pour éviter cette erreur, vous devez rajouter l’élément `<LocalResources>` indiqué dans le code XML suivant au fichier `ServiceDefinition.csdef`. Utilisez le nom du rôle de service web que vous avez rajouté au projet comme partie de l’attribut de nom pour l’élément **<LocalStorage>** . Dans cet exemple, le nom du rôle de service web est **WCFServiceWebRole1**.

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>Étapes suivantes
- [Configuration des rôles pour un service cloud Azure avec Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md)
