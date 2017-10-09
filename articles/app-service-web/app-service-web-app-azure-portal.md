---
title: aaaReference pour parcourir les hello portail Azure
description: "En savoir plus hello des expériences utilisateur différent pour le Service Web de l’application entre le portail de gestion hello et hello portail Azure"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a>Référence pour la navigation hello portail Azure
Le service Sites Web Azure s’appelle désormais [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Nous mettons à tous nos tooreflect documentation jour ce nom modification et tooprovide des instructions pour hello portail Azure. Jusqu'à ce que ce processus est terminé, vous pouvez utiliser ce document comme guide pour travailler avec des applications Web dans hello portail Azure.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a>futures Hello Hello portail classique Azure
Pendant que vous remarquerez hello modifications sur hello portail classique Azure de la marque, ce portail est en cours de hello de remplacé par hello portail Azure. Comme le portail classique de hello est périmée, focus hello pour tout nouveau développement est un décalage toohello portail Azure. Toutes les nouvelles fonctionnalités à venir pour les applications Web proviendront Bonjour portail Azure. Commencer à utiliser parti de tootake portail Azure hello Hello derniers et meilleurs éléments que les applications Web ont toooffer.

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a>Différences de disposition entre hello portail classique Azure et le portail Azure
Dans le portail classique hello, tous les hello Azure services sont répertoriés sur le côté gauche de hello. Navigation dans le portail classique de hello suit une structure arborescente, où vous démarrez à partir du service de hello et naviguez dans chaque élément. Cette structure fonctionne bien lorsque vous gérez des composants indépendants. Toutefois, les applications créées à partir d'Azure sont constituées de services interconnectés, et cette arborescence n'est pas idéale pour les collections de services. 

Hello portail Azure rend facile toobuild applications de bout en bout avec les composants à partir de plusieurs services. portail de Hello est organisée en tant que *trajets*. A *voyage* est une série de *panneaux*, qui sont des conteneurs pour hello différents composants. Par exemple, la configuration de montée en puissance automatique pour une application web est un *voyage* décrites plusieurs panneaux comme indiqué dans hello l’exemple suivant : hello **site web** blade (que titre du panneau n’a pas encore été mis à jour toouse Hello la terminologie nouvelle), hello **paramètres** lame et hello **montée en puissance parallèle** panneau. Dans l’exemple de hello, mise à l’échelle automatique est défini toodepend sur l’utilisation du processeur, par conséquent, il est également un **pourcentage processeur** panneau. Hello composants hello *panneaux* sont appelés *parties*, qui se présenter comme vignettes. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Exemple de navigation : créer une application web
La création d'applications web est toujours aussi facile qu'avant. Hello suivant image affiche hello classique portail et hello portail côte-à-côte toodemonstrate qui ne disposait pas a changé dans plusieurs étapes hello nécessaire tooget de l’application web d’en cours d’exécution. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

Dans le portail de hello, vous pouvez choisir à partir des types courants de hello des applications web, y compris les applications de la galerie populaires telles que WordPress. Pour obtenir une liste complète des applications disponibles, visitez hello [Azure Marketplace].

Lorsque vous créez une application web, vous spécifiez l’URL, le plan App Service et l’emplacement dans le portail hello simplement comme vous le feriez dans le portail classique de hello. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

En outre, portail de hello vous permet de définir d’autres paramètres communs. Par exemple, [groupes de ressources](../azure-resource-manager/resource-group-overview.md) rendre toosee simple et de gérer des ressources Azure associées. 

## <a name="navigation-example-settings-and-features"></a>Exemple de navigation : paramètres et fonctionnalités
Tous les hello paramètres et fonctionnalités sont désormais regroupées logiquement dans un panneau unique, à partir de laquelle vous pouvez accéder.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

Par exemple, vous pouvez créer des domaines personnalisés en cliquant sur **les domaines personnalisés et SSL** Bonjour **paramètres** panneau.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

tooset une alerte de surveillance, cliquez sur **demandes et les erreurs** , puis **ajouter une alerte**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

tooenable diagnostics, cliquez sur **les journaux de diagnostic** Bonjour **paramètres** panneau.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

Cliquez sur les paramètres de l’application tooconfigure, **paramètres d’Application** Bonjour **paramètres** panneau. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Que le nom de marque hello, certains éléments dans le portail de hello ont été renommés ou regroupées toomake il toofind plus facilement les. Par exemple, voici une capture d’écran de la page correspondante de hello pour les paramètres de l’application (**configurer**) dans le portail classique de hello.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Autres ressources
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

