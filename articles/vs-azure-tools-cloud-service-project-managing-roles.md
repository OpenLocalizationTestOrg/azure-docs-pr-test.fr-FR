---
title: "rôles aaaManaging dans Azure cloud services avec Visual Studio | Documents Microsoft"
description: "Découvrez comment tooadd et supprimer des rôles dans Azure cloud services avec Visual Studio."
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
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Gestion des rôles dans Azure Cloud Services avec Visual Studio
Après avoir créé votre service cloud Azure, vous pouvez ajouter de nouveaux rôles tooit ou supprimer des rôles existants. Vous pouvez également importer un projet existant et convertissez-le tooa rôle. Par exemple, vous pouvez importer une application web ASP.NET et la désigner comme rôle web.

## <a name="adding-a-role-tooan-azure-cloud-service"></a>Ajout d’un rôle de tooan service cloud Azure
Hello suit vous guide tout au long de l’ajout d’un web ou travail tooan Azure cloud service projet de rôle dans Visual Studio.

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, développez le nœud de projet hello

1. Avec le bouton hello **rôles** menu contextuel du nœud toodisplay hello. Dans le menu contextuel de hello, sélectionnez **ajouter**, puis sélectionnez un rôle web existant ou un rôle de travail à partir de la solution actuelle de hello ou créer un projet de rôle web ou de travail. Vous pouvez également sélectionner un projet approprié, par exemple un projet d’application web ASP.NET, et l’associer à un projet de rôle.

    ![Options de menu tooadd un projet de service cloud Azure rôle tooan](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Suppression d’un rôle à partir d’un service cloud Azure
Hello étapes suivantes vous guident suppression d’un rôle web ou de travail à partir d’un projet de service cloud Azure dans Visual Studio.

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, développez le nœud de projet hello

1. Développez hello **rôles** nœud.

1. Nœud de hello contextuel vous souhaitez tooremove et, dans le menu contextuel de hello, sélectionnez **supprimer**. 

    ![Options de menu tooadd un tooan de rôle service de cloud computing Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a>Readding d’un projet de service cloud Azure rôle tooan
Si vous supprimez un rôle à partir de votre projet de service cloud, mais décidez ultérieurement de rôle hello tooadd toohello project, seuls déclaration de rôle hello et les attributs de base, tels que les points de terminaison et de diagnostics, sont ajoutés. Aucune des ressources supplémentaires ou des références ne sont ajoutées toohello `ServiceDefinition.csdef` fichier ou toohello `ServiceConfiguration.cscfg` fichier. Si vous souhaitez tooadd ces informations, vous devez toomanually ajouter à nouveau à ces fichiers.

Par exemple, vous pouvez supprimer un rôle de service web et décider ultérieurement de tooadd sauvegarde de ce rôle dans votre solution. Dans ce cas, une erreur se produit. tooprevent cette erreur, vous avez tooadd hello `<LocalResources>` élément présenté dans hello suivant XML soit de nouveau hello `ServiceDefinition.csdef` fichier. Utiliser le nom de rôle du service web hello que vous avez ajouté au projet de hello dans le cadre de l’attribut de nom hello pour hello hello  **<LocalStorage>**  élément. Dans cet exemple, le nom hello du rôle de service web hello est **WCFServiceWebRole1**.

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
- [Configurer des rôles de hello pour un service cloud Azure avec Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md)
