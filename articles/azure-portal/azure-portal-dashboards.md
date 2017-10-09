---
title: aaaCreate et partager des tableaux de bord de portail Azure | Documents Microsoft
description: Cet article explique comment toocreate et modifier des tableaux de bord dans hello portail Azure.
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a>Créer et partager des tableaux de bord dans hello portail Azure
Vous pouvez créer plusieurs tableaux de bord et les partager avec d’autres personnes ont accès tooyour Azure abonnements.  Cet article passe par les principes fondamentaux de hello de création, modification, la publication et la gestion des accès toodashboards.

## <a name="create-a-dashboard"></a>Création d’un tableau de bord
toocreate un tableau de bord, sélectionnez hello **nouveau tableau de bord** bouton nom de la prochaine toohello actuel du tableau de bord.  

![créer un tableau de bord](./media/azure-portal-dashboards/new-dashboard.png)

Cette action crée un nouveau tableau de bord privé vide, et vous fait passer en mode de personnalisation. Vous pouvez alors renommer votre tableau de bord et ajouter ou réorganiser les mosaïques.  Dans ce mode, hello réductible vignette prend de la galerie sur le menu de navigation gauche hello.  Hello vignette galerie vous permet de rechercher les mosaïques pour vos ressources Azure de différentes manières : vous pouvez parcourir en [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups), par type de ressource, par [balise](../azure-resource-manager/resource-group-using-tags.md), ou en effectuant une recherche par nom pour votre ressource.  

![personnaliser un tableau de bord](./media/azure-portal-dashboards/customize-dashboard.png)

Ajouter des vignettes en faisant glisser et en les déposant sur la surface du tableau de bord hello où vous le souhaitez.

Il existe une nouvelle catégorie appelée **Général** , qui regroupe les mosaïques qui ne sont pas associées à une ressource particulière.  Dans cet exemple, nous épingler la vignette de promotions hello.  Vous utilisez ce tableau de bord de mosaïque tooadd tooyour contenu personnalisé.  Hello vignette prend en charge en texte brut, [syntaxe Markdown](https://daringfireball.net/projects/markdown/syntax)et un ensemble limité de HTML.  (Pour la sécurité, vous ne pouvez pas faire injecter `<script>` balises ou utiliser certaine élément de style de feuille de style CSS peut interférer avec le portail de hello.) 

![ajouter markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a>Modifier un tableau de bord
Après avoir créé votre tableau de bord, vous pouvez épingler des vignettes à partir de la galerie de vignette hello ou représentation sous forme de vignette hello de lames. Nous allons épingler la représentation sous forme de hello notre du groupe de ressources. Vous pouvez épingler lorsque vous parcourez hello élément, ou à partir du panneau des ressources de groupe hello. Les deux méthodes génèrent l’épinglage de représentation sous forme de vignette hello hello du groupe de ressources.

![Code confidentiel toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

Après épinglage d’élément de hello, il apparaît sur votre tableau de bord.

![afficher le tableau de bord](./media/azure-portal-dashboards/view-dashboard.png)

Maintenant que nous avons une vignette de promotions et un tableau de bord du toohello épinglés du groupe de ressources, nous pouvons redimensionner et réorganiser des mosaïques de hello dans une organisation acceptable.

En pointant et en sélectionnant «... » ou en cliquant sur une vignette, vous pouvez voir toutes les commandes contextuelles hello pour cette vignette. Par défaut, deux options sont disponibles :

1. **Supprimer du tableau de bord** – vignette de hello supprime du tableau de bord hello
2. **Personnaliser** : passe en mode de personnalisation

![personnaliser une mosaïque](./media/azure-portal-dashboards/customize-tile.png)

Si vous sélectionnez Personnaliser, vous pouvez redimensionner et réorganiser les mosaïques. tooresize une vignette, sélectionnez hello nouvelle taille à partir du menu contextuel de hello, comme indiqué dans hello suivant l’image.

![redimensionner une mosaïque](./media/azure-portal-dashboards/resize-tile.png)

Ou, si la vignette de hello prend en charge n’importe quelle taille, vous pouvez faire glisser taille toohello souhaité de hello en bas à droite.

![redimensionner une mosaïque](./media/azure-portal-dashboards/resize-corner.png)

Après avoir redimensionné vignettes, afficher le tableau de bord de hello.

![afficher la mosaïque](./media/azure-portal-dashboards/view-tile.png)

Une fois que vous avez terminé de personnaliser un tableau de bord, sélectionnez simplement hello **fait personnalisation** tooexit en mode de personnalisation ou avec le bouton droit et sélectionnez **fait personnalisation** à partir du menu contextuel de hello.

## <a name="publish-a-dashboard-and-manage-access-control"></a>Publier un tableau de bord et gérer le contrôle d’accès
Lorsque vous créez un tableau de bord, il est privé par défaut, ce qui signifie que vous êtes seul hello qui peut le voir.  toomake il tooothers visibles, utilisez hello **partage** bouton qui apparaît à côté de hello autres commandes de tableau de bord.

![partager un tableau de bord](./media/azure-portal-dashboards/share-dashboard.png)

Vous êtes invité toochoose sur qu'un groupe d’abonnement et de ressources pour votre tableau de bord de toobe publié. tooseamlessly intégrer des tableaux de bord dans l’écosystème de hello, nous avons implémenté des tableaux de bord partagés en tant que ressources Azure (de sorte que vous ne pouvez pas partager en tapant une adresse de messagerie).  Accéder aux informations de toohello affiché par la plupart des vignettes hello dans le portail de hello sont régies par [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md). Du point de vue du contrôle d’accès, les tableaux de bord partagés sont traités de la même manière qu’une machine virtuelle ou un compte de stockage.  

Supposons que vous avez un abonnement Azure et de membres de votre équipe ont été affectés des rôles de hello de **propriétaire**, **collaborateur**, ou **lecteur** d’abonnement de hello.  Les utilisateurs qui sont propriétaires ou collaborateurs sont en mesure de toolist, afficher, créer, modifier ou supprimer des tableaux de bord au sein de cet abonnement.  Les utilisateurs qui sont des lecteurs sont en mesure de toolist et afficher des tableaux de bord, mais ne peut pas modifier ou les supprimer.  Les utilisateurs avec accès en lecture sont des tableaux de bord partagés de la tooa de toomake en mesure de modifications locales, mais sont toopublish n’a pas pu ces server toohello arrière de modifications.  Toutefois, ils peuvent apporter une copie privée d’un tableau de bord hello pour leur propre usage.  Comme toujours, des vignettes sur le tableau de bord hello appliquent leurs propres règles de contrôle d’accès en fonction des ressources hello qu'auxquelles elles correspondent.  

Pour plus de commodité, portail de hello de publication du guides expérience vous vers un modèle où placer les tableaux de bord dans un groupe de ressources appelé **tableaux de bord**.  

![publier un tableau de bord](./media/azure-portal-dashboards/publish-dashboard.png)

Vous pouvez également choisir toopublish un groupe de ressources tooa du tableau de bord.  contrôle d’accès Hello pour ce tableau de bord correspond au contrôle d’accès hello pour le groupe de ressources hello.  Les utilisateurs qui peuvent gérer des ressources hello dans ce groupe de ressources ont également accès toohello tableaux de bord.

![publier du tableau de bord tooresource groupe](./media/azure-portal-dashboards/publish-to-resource-group.png)

Après la publication de votre tableau de bord, hello **partage + accès** volet de contrôle s’actualiser et affichent des informations sur le tableau de bord publié hello, y compris un bord de lien toomanage utilisateur accès toohello.  Ce lien lance hello Role Based Access Control panneau utilisé toomanage accès standard pour n’importe quelle ressource Azure.  Vous pouvez toujours revenir toothis vue en sélectionnant **partage**.

![gérer le contrôle d’accès](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a>Étapes suivantes
* toomanage des ressources, consultez [des ressources de gestion de Azure via le portail](../azure-resource-manager/resource-group-portal.md).
* toodeploy des ressources, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et le portail Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).

