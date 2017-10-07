---
title: "contenu de la page dans le portail des développeurs dans Gestion des API Azure hello aaaModify | Documents Microsoft"
description: "Découvrez comment tooedit page de contenu sur le portail des développeurs dans Gestion des API Azure hello."
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: fd5a854e900d9512518643e593b1b59a0952621f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-content-and-layout-of-pages-on-hello-developer-portal-in-azure-api-management"></a>Modifier le contenu de hello et la disposition des pages sur le portail des développeurs hello dans Gestion des API Azure
Il existe trois méthodes fondamentales toocustomize hello portail destiné aux développeurs dans Gestion des API Azure :

* [Modifier les pages statiques et des éléments de mise en page contenu hello] [ modify-content-layout] (présentés dans ce guide)
* [Mettre à jour les styles de hello utilisés pour les éléments de la page sur le portail des développeurs hello][customize-styles]
* [Modifier les modèles hello utilisés pour les pages générées par le portail de hello] [ portal-templates] (par exemple, documents de l’API, produits, l’authentification des utilisateurs, etc.)

## <a name="page-structure"></a>Structure des pages du portail des développeurs

portail des développeurs Hello est basée sur un système de gestion de contenu. mise en page Hello de chaque page s’appuie sur l’ensemble d’éléments de page petit appelé widgets :

![Structure de page du portail des développeurs][api-management-customization-widget-structure]

Tous les widgets sont modifiables. 
* page individuelle de Hello core contenu tooeach spécifiques se trouvent dans le widget de « Contenu » hello. Modification d’une page signifie que la modification de contenu hello ce widget.
* Tous les éléments de mise en page sont contenus dans les widgets restantes hello. Modifications apportées aux widgets de toothese appliquera tooall pages. Ils seront tooas référencé « widgets disposition ».

Dans la page quotidienne une modification généralement modifie uniquement le widget de contenu hello qui ont un contenu différent pour chaque page.

## <a name="modify-layout-widget"></a>Modifier le contenu de hello d’un widget de disposition

Contenu dans le portail des développeurs hello est modifié via le portail de publication hello qui est accessible à partir de hello portail Azure. tooreach, cliquez sur **portail de publication** à partir de la barre d’outils du service hello de votre instance de la gestion des API.

![Portail des éditeurs][api-management-management-console]

Cliquez sur le contenu de hello tooedit de ce widget, **Widgets** de hello **portail des développeurs** menu à gauche de hello. Pour cet exemple vous permet de modifier le contenu hello du widget d’en-tête hello. Sélectionnez hello **en-tête** widget à partir de la liste de hello.

![Widgets header][api-management-widgets-header]

contenu Hello de hello est modifiable à partir de hello **corps** champ. Modifier le texte hello comme vous le souhaitez, puis cliquez sur **enregistrer** bas hello de page de hello.

Vous devez maintenant être en mesure de toosee hello nouvel en-tête sur chaque page de portail des développeurs hello.

> Cliquez sur le portail des développeurs hello tooopen tandis que dans le portail de publication hello, **portail des développeurs** dans la barre supérieure de hello.
> 
> 

## <a name="edit-page-contents"></a>Modifier le contenu de hello d’une page

liste de hello toosee de toutes les pages de contenu existantes, cliquez sur **contenu** de hello **portail des développeurs** menu dans le portail de publication hello.

![Manage content][api-management-customization-manage-content]

Cliquez sur hello **Bienvenue** page tooedit ce qui est affiché sur la page d’accueil de hello du portail des développeurs hello. Apporter des modifications de hello, afficher un aperçu si nécessaire, puis cliquez **publier maintenant** toomake les tooeveryone visible.

> page d’accueil Hello utilise une disposition spéciale qui lui permet de toodisplay une bannière haut hello. Cette bannière ne peut pas être modifiable à partir de hello **contenu** section. tooedit ce bannière, cliquez sur **Widgets** de hello **portail des développeurs** menu, sélectionnez **page d’accueil** de hello **couche actuelle** liste déroulante liste, puis ouvrez hello **bannière** élément sous hello **proposées section**. contenu Hello ce widget est modifiables comme toute autre page.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Mettre à jour les styles de hello utilisés pour les éléments de la page sur le portail des développeurs hello][customize-styles]
* [Modifier les modèles hello utilisés pour les pages générées par le portail de hello] [ portal-templates] (par exemple, documents de l’API, produits, l’authentification des utilisateurs, etc.)

[Structure of developer portal pages]: #page-structure
[Modifying hello contents of a layout widget]: #modify-layout-widget
[Edit hello contents of a page]: #edit-page-contents
[Next steps]: #next-steps

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customization-widget-structure]: ./media/api-management-modify-content-layout/portal-widget-structure.png
[api-management-management-console]: ./media/api-management-modify-content-layout/api-management-management-console.png
[api-management-widgets-header]: ./media/api-management-modify-content-layout/api-management-widgets-header.png
[api-management-customization-manage-content]: ./media/api-management-modify-content-layout/api-management-customization-manage-content.png
