---
title: "aaaResources, rôles et contrôle d’accès dans Azure Application Insights | Documents Microsoft"
description: "Propriétaires, collaborateurs et lecteurs des perspectives de votre organisation."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Contrôle d’accès, rôles et ressources dans Application Insights
Vous pouvez contrôler qui a lu et mettre à jour des données de tooyour d’accès dans Azure [Application Insights][start], à l’aide de [contrôle d’accès basé sur un rôle dans Microsoft Azure](../active-directory/role-based-access-control-configure.md).

> [!IMPORTANT]
> Affecter toousers accès Bonjour **groupe de ressources ou d’un abonnement** toowhich votre ressource application appartienne - pas de ressource hello elle-même. Affecter hello **contributeur de composant Application Insights** rôle. Cela garantit uniform contrôle d’accès tooweb tests et des alertes, ainsi que des ressources de votre application. [En savoir plus](#access).
> 
> 

## <a name="resources-groups-and-subscriptions"></a>Ressources, groupes et abonnements
Quelques définitions pour commencer :

* **Ressource** : une instance d’un service Microsoft Azure. Votre ressource Application Insights collecte, analyse et affiche les données de télémétrie hello envoyées à partir de votre application.  Les autres types de ressources Azure incluent des applications Web, des bases de données et des machines virtuelles.
  
    Ouvrez de vos ressources, toosee hello [Azure Portal][portal], connectez-vous, puis cliquez sur toutes les ressources. toofind une ressource, tapez une partie de son nom dans le champ de filtre hello.
  
    ![Liste des ressources Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [**Groupe de ressources** ] [ group] -chaque ressource appartient tooone groupe. Un groupe est un moyen toomanage liées à des ressources, en particulier pour le contrôle d’accès. Par exemple, dans une ressource de groupe, vous pouvez placer une application Web, une application de hello de toomonitor ressource Application Insights et un tookeep de ressource de stockage données exportées.

    ![Cliquez sur Parcourir, Groupes de ressources, puis choisissez un groupe](./media/app-insights-resources-roles-access-control/11-group.png)

* [**Abonnement** ](https://manage.windowsazure.com) -toouse Application Insights ou autres ressources Azure, vous vous connectez tooan abonnement Azure. Chaque groupe de ressources appartient tooone abonnement Azure, où vous choisissez votre package de prix et, s’il s’agit d’un abonnement de l’organisation, choisissez les membres hello et leurs autorisations d’accès.
* [**Compte Microsoft** ] [ account] -hello nom d’utilisateur et mot de passe que vous utilisez toosign dans tooMicrosoft Azure abonnements, XBox Live, Outlook.com et autres services Microsoft.

## <a name="access"></a>Contrôler l’accès dans le groupe de ressources hello
Il est important toounderstand que dans la ressource de toohello plus que vous avez créé pour votre application, il existe également de séparer des ressources masqués pour les alertes et les tests web. Ils sont attaché toohello même [groupe de ressources](#resource-group) que votre application. Vous pouvez également placer d’autres services Azure ici, comme des sites Web ou du stockage.

![Ressources dans Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

toocontrol accéder aux ressources toothese qu'il est donc recommandé :

* Contrôler l’accès au hello **groupe de ressources ou d’un abonnement** niveau.
* Affecter hello **contributeur de composant d’Application Insights** toousers de rôle. Cela leur permet de tooedit des tests web, les alertes et les ressources Application Insights, sans fournir d’autres services dans le groupe de hello tooany d’accès.

## <a name="tooprovide-access-tooanother-user"></a>tooprovide tooanother utilisateur
Vous devez disposer d’abonnement de toohello de droits de propriétaire ou un groupe de ressources hello.

Hello utilisateur doit avoir un [Account Microsoft][account], ou accéder aux tootheir [Account Microsoft](../active-directory/sign-up-organization.md). Vous pouvez fournir tooindividuals d’accès, ainsi que les groupes toouser définis dans Azure Active Directory.

#### <a name="navigate-toohello-resource-group"></a>Parcourir le groupe de ressources toohello
Ajouter un utilisateur hello.

![Dans le panneau des ressources de votre application, ouvrez Essentials, ouvrez le groupe de ressources hello et sélectionner les utilisateurs/paramètres. Cliquez sur Ajouter.](./media/app-insights-resources-roles-access-control/01-add-user.png)

Ou vous pouvez aller plus loin et ajouter hello utilisateur toohello abonnement.

#### <a name="select-a-role"></a>Sélectionnez un rôle
![Sélectionnez un rôle pour le nouvel utilisateur de hello](./media/app-insights-resources-roles-access-control/03-role.png)

| Rôle | Dans le groupe de ressources hello |
| --- | --- |
| Propriétaire |Peut tout modifier, y compris l’accès utilisateur |
| Collaborateur |Peut tout modifier, y compris l’ensemble des ressources |
| collaborateur de composants Application Insights |Peut modifier les ressources, les tests Web et les alertes Application Insights |
| Lecteur |Peut afficher les éléments, mais ne peut rien modifier |

Une « modification » inclut la création, la suppression et la mise à jour des éléments suivants :

* Ressources
* Tests web
* Alertes
* Exportation continue

#### <a name="select-hello-user"></a>Sélectionnez hello utilisateur

Si l’utilisateur hello souhaité n’est pas dans le répertoire de hello, vous pouvez inviter toute personne disposant d’un compte Microsoft.
(Si elle utilise des services comme Outlook.com, OneDrive, Windows Phone ou XBox Live, elle dispose d’un compte Microsoft.)

## <a name="related-content"></a>Contenu connexe

* [Contrôle d’accès en fonction du rôle dans Azure](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
