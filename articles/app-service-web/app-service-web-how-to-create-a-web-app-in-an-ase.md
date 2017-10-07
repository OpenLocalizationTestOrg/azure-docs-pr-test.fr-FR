---
title: aaaCreate une application web dans un environnement App Service de v1
description: "Découvrez comment toocreate les applications web et les plans de service d’application dans un environnement App Service de v1"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a>Créer une application web dans un environnement App Service Environment v1

> [!NOTE]
> Cet article porte sur hello environnement App Service v1.  Il existe une version plus récente de hello environnement App Service toouse plus facile et s’exécute sur une infrastructure plus puissante. toolearn plus d’informations sur la nouvelle version de hello commencent par Bonjour [Introduction toohello environnement App Service](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel montre comment les applications web toocreate et plans de Service d’applications dans un [environnement App Service v1](app-service-app-service-environment-intro.md) (ASE). 

> [!NOTE]
> Si vous souhaitez toolearn comment toocreate une application web, mais n’avez pas besoin de toodo dans un environnement App Service, consultez [créer une application web .NET](app-service-web-get-started-dotnet.md) ou un des hello didacticiels pour d’autres langages et infrastructures.
> 
> 

## <a name="prerequisites"></a>Composants requis
Ce didacticiel part du principe que vous avez créé un environnement App Service. Si ce n’est pas encore le cas, consultez [Créer un environnement App Service](app-service-web-how-to-create-an-app-service-environment.md). 

## <a name="create-a-web-app"></a>Créer une application web
1. Bonjour [Azure Portal](https://portal.azure.com/), cliquez sur **Nouveau > Web + Mobile > application Web**. 
   
    ![][1]
2. Sélectionnez votre abonnement.  
   
    Si vous avez plusieurs abonnements n’oubliez pas que toocreate une application dans votre environnement App Service, vous devez toouse hello même abonnement que vous avez utilisé lors de la création d’environnement de hello. 
3. Sélectionnez ou créez un groupe de ressources.
   
    *Groupes de ressources* activer vous toomanage associées des ressources Azure en tant qu’unité et sont utiles lors de l’établissement *contrôle d’accès basé sur le rôle* règles (RBAC) pour vos applications. Pour plus d’informations, consultez [Présentation d’Azure Resource Manager][ResourceGroups]. 
4. Sélectionnez ou créez un plan App Service.
   
    *plans App Service* sont des ensembles gérés d’applications web.  Normalement, lorsque vous sélectionnez la tarification, pratiqué hello est appliqué toohello plan de Service d’applications plutôt que les applications individuelles toohello. Dans un environnement app service vous payez pour le calcul de hello instances allouées toohello ASE plutôt que ce que vous avez répertoriés avec vos pages ASP.  tooscale numéro hello d’instances d’une application web de l’échelle des instances de hello de votre plan App Service et il affecte toutes les applications web de hello dans ce plan.  Certaines fonctionnalités telles que les emplacements de site ou l’intégration de réseau virtuel ont également des restrictions de quantité dans le plan de hello.  Pour plus d’informations, consultez la rubrique [Présentation des plans Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)
   
    Vous pouvez identifier hello que plans de Service d’applications dans votre ASE en examinant emplacement hello qui est indiquée sous le nom du plan hello.  
   
    ![][5]
   
    Si vous souhaitez toouse un plan App Service qui existe déjà dans votre environnement App Service, sélectionnez ce plan. Si vous voulez toocreate un nouveau plan de Service d’applications, consultez hello suivant la section de ce didacticiel, [créer un plan de Service d’applications dans un environnement App Service](#createplan).
5. Entrez le nom hello pour votre application web, puis cliquez sur **créer**. 
   
    Si votre ASE utilise une URL de hello adresse IP externe d’une application dans un environnement app service est : [*sitename*]. [ *nom de votre environnement App Service*]. p.azurewebsites.net au lieu de [*sitename*]. azurewebsites.net
   
    Si votre ASE utilise une URL interne VIP puis hello d’une application dans la mesure où est ASE : [*sitename*]. [ *sous-domaine spécifié lors de la création de ASE*]   
    Après avoir sélectionné vos pages ASP lors de la création de ASE vous verrez sous-domaine de hello mettre à jour ci-dessous **nom**

## <a name="createplan"></a> Créer un plan App Service
Lorsque vous créez un plan App Service dans un environnement App Service, vos choix de travaux sont différents, car il n’existe pas de travaux partagés dans un environnement App Service.  les travailleurs Hello avoir toouse sont hello ceux qui ont été allouées toohello ASE par l’administrateur de hello.  Cela signifie que toocreate un plan, vous devez toohave plus travailleurs alloués tooyour ASE worker pool que le nombre total de hello d’instances dans l’ensemble de vos plans déjà dans ce pool de travail.  Si vous n’avez suffisamment traitements dans votre toocreate de pool de travail ASE votre plan, vous devez toowork avec votre tooget d’administration ASE que les ajouté.

Une autre différence avec les plans App Service hébergé par un environnement App Service est un manque de hello de sélection de la tarification.  Lorsque vous avez un environnement App Service vous payez pour les ressources de calcul utilisées par le système de hello et n’avez pas de frais ajoutés pour les plans de hello dans cet environnement.  Normalement lorsque vous créez un plan App Service, vous sélectionnez un niveau de tarification qui détermine votre facturation.  Un environnement App Service est essentiellement un emplacement privé où vous pouvez créer un contenu.  Vous payez pour l’environnement de hello et toohost pas votre contenu.

Hello instructions suivantes indiquent comment toocreate un Service d’application plan pendant la création d’une application web, comme expliqué dans la section précédente de hello du didacticiel de hello.

1. Cliquez sur **créer un nouveau** hello d’interface utilisateur de sélection de plan et fournir un nom pour votre plan comme vous le feriez normalement en dehors d’un environnement app service.
2. Sélectionnez ASE hello que vous souhaitez toouse dans le sélecteur de votre emplacement.
   
    Un environnement App Service étant essentiellement un emplacement de déploiement privé, il s’affiche sous Emplacement. 
   
    ![][2]
   
    Après la sélection d’un environnement app service dans le sélecteur d’emplacement hello, hello interface utilisateur de création de plan App Service met à jour.  emplacement de Hello affiche maintenant nom hello hello système de ASE et région de hello dans, et hello tarification sélecteur de plan est remplacé par un sélecteur de pool de travail.  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a>Sélection d’un pool de travail
Normalement dans Azure App Service et en dehors d’un environnement App Service, il existe 3 tailles de calcul qui sont disponibles avec la sélection d’un plan de prix dédié hello.  De la même manière, pour un environnement app service vous pouvez définir too3 les pools de threads de travail et spécifier hello calcul taille qui est utilisé pour ce pool de travail.  Cela signifie pour les clients de hello ASE est qu’au lieu de sélectionner un plan de tarification avec une taille compute pour votre plan App Service, vous sélectionnez ce que l'on appelle un *pool de travail*.  

sélection de pool de travail Hello l’interface utilisateur affiche la taille de calcul de hello utilisée pour ce pool de travail sous le nom de hello.  Hello quantité disponible fait référence toohow plusieurs instances sont disponibles pour une utilisation dans ce pool de calcul.  pool totale de Hello peut avoir plusieurs instances de ce nombre, mais cette valeur fait référence à toosimply combien n’est pas en cours d’utilisation.  Si vous avez besoin de tooadjust tooadd de votre environnement App Service plus de calcul des ressources, consultez [configuration de votre environnement App Service](app-service-web-configure-an-app-service-environment.md).

![][4]

Dans cet exemple, vous constatez que seuls deux pools de travaux sont disponibles. C’est parce qu’administrateur de ASE hello attribué uniquement des hôtes dans les pools de travail de deux.  Hello troisième s’inscrive lorsqu’il existe des ordinateurs virtuels alloués dans celui-ci.  

## <a name="after-web-app-creation"></a>Après la création d'une application web
Il existe quelques règles pour les applications web en cours d’exécution et de gérer des plans de Service d’applications dans un environnement app service qui doivent toobe pris en compte.  

Comme indiqué précédemment, propriétaire hello Hello ASE est responsable de la taille de hello du système de hello et par conséquent ils sont également responsables pour vous assurer qu’il est suffisamment hello toohost de capacité souhaité plans App Service. S’il n’y a aucune disposition des employés, à ne pas être en mesure de toocreate votre plan App Service.  C’est également true tooscaling configurer votre application web.  Si vous avez besoin de plusieurs instances, vous devez tooget votre tooadd d’administration environnement App Service davantage de traitements.

Après avoir créé votre application web et le plan App Service, il est une bonne idée tooscale, configurez-le.  Dans un environnement app service, vous devez toujours toohave au moins 2 des instances de votre Service d’applications plan tooprovide une tolérance de panne pour vos applications.  Mise à l’échelle un Service d’application plan dans un environnement app service est même hello normalement via hello le plan App Service l’interface utilisateur.  Pour plus d’informations sur la mise à l’échelle, [comment tooscale une application web dans un environnement App Service](app-service-web-scale-a-web-app-in-an-app-service-environment.md)

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
