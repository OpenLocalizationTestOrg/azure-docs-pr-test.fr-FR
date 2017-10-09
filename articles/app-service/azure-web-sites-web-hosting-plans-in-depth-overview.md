---
title: "vue d’ensemble approfondie des plans aaaAzure du Service d’applications | Documents Microsoft"
description: "Découvrez comment fonctionnent les plans Azure App Service et comment ils peuvent améliorer votre gestion."
keywords: "app service, azure app service, mise à l'échelle, évolutif, plan app service, coût d'app service"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Présentation détaillée des plans Azure App Service

Plans de Service d’application représentent collection hello de ressources physiques utilisées toohost vos applications.

Les plans App Service définissent :

- Région (ouest des États-Unis, est des États-Unis, etc.)
- Comptage (un, deux, trois instances, etc.)
- La taille d’instance (« Petit », « Moyen », « Grand »)
- Référence (SKU) (gratuit, partagé, basique, standard, premium)

Les Web Apps, les Mobile Apps, les API Apps, et les Function Apps dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), fonctionnent toutes dans un plan App Service.  Applications Bonjour même abonnement et région peuvent partager un plan App Service. 

Toutes les applications affectées tooan **plan App Service** partagent des ressources hello qu’elle. Ce partage permet de réaliser des économies lors de l’hébergement de plusieurs applications dans un seul plan App Service.

Votre **plan App Service** peut évoluer de **libre** et **Shared** références trop**base**, **Standard**, et **Premium** références (SKU), vous pouvez ainsi accéder aux ressources de la toomore et de fonctionnalités le long de hello moyen.

Si votre plan App Service est défini trop**base** référence (SKU) ou une version ultérieure, puis vous pouvez contrôler hello **taille** et d’augmenter le nombre de machines virtuelles de hello.

Par exemple, si votre plan est configuré toouse deux les instances « petite » dans le niveau de service standard hello, toutes les applications qui sont associées à ce plan s’exécuter sur les deux instances. Les applications ont également des fonctionnalités de niveau d’accès toohello service standard. Les instances de plans sur lesquelles sont exécutées des applications sont entièrement gérées et hautement disponibles.

> [!IMPORTANT]
> Hello **référence (SKU)** et **échelle** Hello du Service d’applications plan détermine hello coût et hello pas le numéro d’applications qu’elle contient.

Cet article explore hello principales caractéristiques, telles que le niveau et mise à l’échelle d’un plan App Service et comment ils entrent en jeu lors de la gestion de vos applications.

## <a name="apps-and-app-service-plans"></a>Applications et plans App Service

Une application App Service ne peut être associée qu'à un seul plan App Service à la fois.

Les applications et les plans sont contenus dans un **groupe de ressources**. Un groupe de ressources sert de limite de cycle de vie hello pour toutes les ressources qu’il contient. Vous pouvez utiliser toomanage de groupes de ressources tous les éléments hello d’une application.

Comme un seul groupe de ressources peut avoir plusieurs plans de services d’application, vous pouvez affecter à différentes applications toodifferent des ressources physiques.

Par exemple, vous pouvez répartir les ressources entre les environnements de développement, de test et de production. Avoir des environnements de production et de développement/test distincts permet d’isoler des ressources. De cette façon, test de charge sur une nouvelle version de vos applications n’est pas en concurrence pour hello même ressources en tant que vos applications de production, qui servent à nos clients.

Lorsque vous avez plusieurs plans au sein d’un même groupe de ressources, vous pouvez également définir une application disponible pour plusieurs régions géographiques.

Par exemple, une application hautement disponible qui s’exécute dans deux régions inclut au moins deux plans, un pour chaque région, et une application associée à chaque plan. Dans ce cas, toutes les copies de hello d’application hello puis contenus dans un seul groupe de ressources. Avoir un groupe de ressources avec plusieurs plans et plusieurs applications en fait toomanage facile, le contrôle et afficher l’intégrité de hello de l’application hello.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>Créer un plan App Service ou utiliser un plan existant

Lorsque vous créez une application, vous devez penser à créer un groupe de ressources. Sur hello autre part, si cette application est un composant pour une application plus importante, créez-le dans groupe de ressources hello qui est allouée pour cette application supérieure.

Si l’application hello est un entièrement nouvelle application ou une partie d’une plus grande, vous pouvez choisir toouse un toohost de plan existant qu’il ou créez-en un. Cette décision relève plus d’une question de capacité et de charge attendue.

Nous vous recommandons d’isoler votre application dans un nouveau plan App Service si :

- L’application consomme beaucoup de ressources.
- Application dispose de différents facteurs d’échelle à partir de hello autres applications hébergées dans un plan existant.
- L’application a besoin de ressources dans une région géographique différente.

De cette façon, vous pouvez allouer un nouveau jeu de ressources pour votre application et mieux contrôler vos applications.

## <a name="create-an-app-service-plan"></a>Créer un plan App Service

> [!TIP]
> Si vous avez un environnement App Service, vous pouvez consulter hello documentation spécifique tooApp environnements Service ici : [créer un plan de Service d’applications dans un environnement App Service](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

Vous pouvez créer un plan App Service vide de hello expérience de navigation de plan de Service d’applications ou dans le cadre de la création de l’application.

Bonjour [portail Azure](https://portal.azure.com), cliquez sur **nouveau** > **Web + mobile**, puis sélectionnez **Web App** ou autre type d’application de Service d’applications.

![Créer une application Bonjour portail Azure.][createWebApp]

Vous pouvez ensuite sélectionner ou créer hello plan App Service pour hello nouvelle application.

 ![Créer un plan App Service.][createASP]

toocreate un plan App Service, cliquez sur **[+] Create New**, hello de type **plan App Service** nom, puis sélectionnez un **emplacement**. Cliquez sur **niveau tarifaire**, puis sélectionnez un niveau de tarification approprié pour le service de hello. Sélectionnez **afficher toutes les** tooview plus tarification options, telles que **libre** et **partagé**. Après avoir sélectionné hello niveau tarifaire, cliquez sur hello **sélectionnez** bouton.

## <a name="move-an-app-tooa-different-app-service-plan"></a>Déplacer un plan de Service d’applications application tooa différents

Vous pouvez déplacer un plan de Service d’applications différentes application tooa Bonjour [portail Azure](https://portal.azure.com). Vous pouvez déplacer des applications entre les plans tant que plans de hello sont Bonjour même groupe de ressources et de la région géographique.

toomove un plan de tooanother d’application :

- Accédez application toohello que vous souhaitez toomove.
- Bonjour **Menu**, recherchez hello **du Plan App Service** section.
- Sélectionnez **plan App Service de modification** processus de hello toostart.

**Plan App Service de modification** ouvre hello **plan App Service** sélecteur. À ce stade, vous pouvez choisir un toomove de plan existant cette application dans.

> [!IMPORTANT]
> l’interface utilisateur le plan App Service sélectionnez Hello est filtré par hello suivant des critères :
> - Existe dans hello même groupe de ressources
> - Existe dans hello même région géographique
> - Existe dans hello même espace Web
>
> Un espace Web est une construction logique au sein d’App Service qui définit un regroupement de ressources du serveur. Une région géographique (par exemple, ouest des États-Unis) contient des espaces Web de nombreux clients tooallocate de commande à l’aide du Service d’applications. Actuellement, les ressources du Service d’applications ne sont pas en mesure de toobe déplacé entre des espaces Web.
>

![Sélecteur de plan App Service.][change]

Chaque plan a son propre niveau de tarification. Par exemple, le déplacement d’un site à partir d’un niveau Standard de niveau gratuit tooa, Active toutes les applications affectées des fonctionnalités de tooit toouse hello et ressources de niveau Standard de hello.

## <a name="clone-an-app-tooa-different-app-service-plan"></a>Cloner un plan de Service d’applications application tooa différents

Si vous souhaitez toomove hello application tooa autre région, une solution consiste à application le clonage. Le clonage crée une copie de votre application dans un plan App Service, nouveau ou existant, dans n’importe quelle région.

Vous pouvez trouver **le clonage d’application** Bonjour **outils de développement** section du menu de hello.

> [!IMPORTANT]
> Pour plus d’informations sur les limites du clonage, voir [Clonage de l’application Azure App Service à l’aide du portail Azure](../app-service-web/app-service-web-app-cloning-portal.md).

## <a name="scale-an-app-service-plan"></a>Mettre à l’échelle un plan App Service

Il existe trois façons tooscale un plan :

- **Niveau de tarification du planning hello**. Un plan de niveau de base hello peut être convertie tooStandard, et toutes les applications affectées tooit toouse fonctionnalités hello de niveau Standard de hello.
- **Modifier la taille des instances du plan hello**. Par exemple, un plan de niveau de base hello qui utilise de petites instances peut être modifiées toouse les instances de grande taille. Toutes les applications qui sont associées à ce plan maintenant peuvent utiliser plus de mémoire hello et les ressources qui hello offres de taille plus grandes instance.
- **Modifier le nombre d’instances du plan hello**. Par exemple, un plan Standard est remonté toothree instances peut être mis à l’échelle too10 instances. Un plan Premium la montée en puissance too20 instances (objet tooavailability). Toutes les applications qui sont associées à ce plan maintenant peuvent utiliser plus de mémoire hello et les ressources qui hello plus grande offre de nombre d’instance.

Vous pouvez modifier hello tarification de couche et instance de la taille en cliquant sur hello **mise à l’échelle** élément sous Paramètres hello plan App Service ou application hello. Modifications s’appliquent toohello plan App Service et concernent toutes les applications qu’il héberge.

 ![Définissez tooscale de valeurs d’une application.][pricingtier]

## <a name="app-service-plan-cleanup"></a>Nettoyage du plan App Service

> [!IMPORTANT]
> **Plans de Service d’applications** qui n’ont aucun toothem applications associées peut toujours occasionner des frais, car ils continuent de capacité de calcul tooreserve hello.

tooavoid inattendues frais, lors de l’application dernière hello est hébergée dans un plan App Service est supprimée, hello vide résultant plan App Service est également supprimé.

## <a name="summary"></a>Résumé

Les plans App Service représentent un ensemble de fonctionnalités et de capacités que vous pouvez partager entre vos différentes applications. Les plans de Service d’applications vous hello ensemble de tooa flexibilité tooallocate des applications spécifiques de ressources et optimisez votre utilisation des ressources Azure. De cette manière, si vous souhaitez toosave money sur votre environnement de test, vous pouvez partager un plan entre plusieurs applications. Vous pouvez également augmenter le débit de votre environnement de production en le mettant à l'échelle dans plusieurs régions et plusieurs plans.

## <a name="whats-changed"></a>Changements apportés

- Pour une modification de toohello guide à partir de sites Web tooApp Service, consultez : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
