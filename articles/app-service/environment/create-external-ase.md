---
title: "Créer un environnement Azure App Service externe"
description: "Explique comment créer un environnement App Service dans le cadre d’un plan App Service ou de manière autonome."
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 70c43b25aea364d7254137b46af31f851dcf8bc6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="create-an-external-app-service-environment"></a>Créer un environnement App Service externe #

Un environnement Azure App Service est un déploiement d’Azure App Service dans un sous-réseau d’un réseau virtuel Azure. Il existe deux façons de déployer un environnement App Service (ASE, App Service Environment) :

- À l’aide d’une adresse IP virtuelle définie sur une adresse IP externe. On parle alors d’environnement App Service externe.
- À l’aide d’une adresse IP virtuelle définie sur une adresse IP interne. On parle alors d’environnement App Service ILB, car le point de terminaison interne est un équilibreur de charge interne (ILB, Internal Load Balancer).

Cet article vous explique comment créer un ASE externe. Pour une présentation de l’environnement App Service, consultez [Présentation de l’environnement App Service Environment][Intro]. Pour plus d’informations sur la création d’un environnement App Service ILB, consultez [Créer et utiliser un équilibreur de charge interne avec un environnement Azure App Service Environment][MakeILBASE].

## <a name="before-you-create-your-ase"></a>Avant de créer votre ASE ##

Une fois l’environnement App Service créé, les éléments suivants ne peuvent plus être modifiés :

- Lieu
- Abonnement
- Groupe de ressources
- Réseau virtuel utilisé
- Sous-réseau utilisé
- Taille du sous-réseau

> [!NOTE]
> Quand vous choisissez un réseau virtuel et spécifiez un sous-réseau, vérifiez que leur taille leur permet de prendre en compte les évolutions futures. Nous vous recommandons une taille de `/25` avec 128 adresses.
>

## <a name="three-ways-to-create-an-ase"></a>Trois façons de créer un ASE ##

Il existe trois façons de créer un environnement App Service :

- **Dans le cadre d’un plan App Service**. Avec cette méthode, l’environnement App Service et le plan App Service sont créés lors de la même étape.
- **De façon autonome**. Avec cette méthode, seul l’environnement App Service est créé. Le processus de création est plus avancé et permet de créer un environnement App Service avec un équilibreur de charge interne (ILB).
- **À l’aide d’un modèle Azure Resource Manager**. Cette méthode est destinée aux utilisateurs expérimentés. Pour plus d’informations, consultez [Création d’un environnement ASE à l’aide des modèles Azure Resource Manager][MakeASEfromTemplate].

Un environnement App Service externe a une adresse IP virtuelle publique, ce qui signifie que le trafic HTTP/HTTPS entrant dans les applications de l’environnement App Service atteint une adresse IP accessible via Internet. Un environnement App Service avec un équilibreur de charge interne (ILB) a une adresse IP issue du sous-réseau utilisé par l’environnement App Service. Les applications hébergées dans un environnement App Service ILB ne sont pas exposées directement à Internet.

## <a name="create-an-ase-and-an-app-service-plan-together"></a>Créer un ASE et un plan App Service ensemble ##

Le plan App Service est un conteneur d’applications. Lorsque vous créez une application dans App Service, vous devez sélectionner ou créer un plan App Service. Les environnements du modèle de conteneur contiennent les plans App Service, et les plans App Service contiennent les applications.

Pour créer un environnement App Service en même temps que le plan App Service :

1. Dans le [portail Azure](https://portal.azure.com/), sélectionnez **Nouveau** > **Web + Mobile** > **Application web**.

    ![Création d’une application web][1]

2. Sélectionnez votre abonnement. L’application et l’environnement App Service sont créés dans les mêmes abonnements.

3. Sélectionnez ou créez un groupe de ressources. Vous pouvez utiliser des groupes de ressources pour gérer des ressources Azure connexes en tant qu’unité. Les groupes de ressources sont également utiles lorsque vous souhaitez établir des règles de contrôle d’accès en fonction du rôle (RBAC) pour vos applications. Pour plus d’informations, consultez [Présentation d’Azure Resource Manager][ARMOverview].

4. Cliquez sur le plan App Service, puis sélectionnez **Créer un nouveau**.

    ![Nouveau plan App Service][2]

5. Dans la liste déroulante **Emplacement**, sélectionnez la région où vous souhaitez créer l’environnement App Service. Si vous sélectionnez un environnement App Service existant, aucun environnement App Service n’est créé. Le plan App Service est créé dans l’environnement App Service que vous avez sélectionné. 

6. Sélectionnez **Niveau tarifaire**, puis choisissez l’une des références SKU de tarification **Isolé**. Si vous choisissez une carte de référence SKU **Isolé** et un emplacement autre qu’un environnement App Service, un nouvel environnement App Service est créé à cet emplacement. Pour démarrer le processus de création d’un environnement App Service, cliquez sur **Sélectionner**. La référence SKU **Isolé** n’est disponible qu’avec un environnement App Service. Vous ne pouvez pas utiliser une autre référence SKU de tarification dans un environnement App Service qui n’est pas **Isolé**.

    ![Sélection du niveau tarifaire][3]

7. Indiquez le nom de votre ASE. Ce nom est utilisé dans le nom adressable de vos applications. Si le nom de l’environnement App Service est _appsvcenvdemo_, le nom du domaine est *.appsvcenvdemo.p.azurewebsites.net*. Si vous créez une application nommée *mytestapp*, elle est adressable à l’adresse mytestapp.appsvcenvdemo.p.azurewebsites.net. Vous ne pouvez pas utiliser d’espace blanc dans le nom. Si vous utilisez des majuscules dans le nom, le nom de domaine correspond à la version complète de ce nom en minuscules.

    ![Nom du nouveau plan App Service][4]

8. Spécifiez les informations concernant votre réseau virtuel Azure. Choisissez **Créer un nouveau** ou **Sélectionner**. L’option permettant de sélectionner un réseau virtuel existant est disponible uniquement si un réseau virtuel se trouve dans la région sélectionnée. Si vous sélectionnez **Créer un nouveau**, entrez un nom pour le réseau virtuel. Un nouveau réseau virtuel Resource Manager portant ce nom est alors créé. Il utilise l’espace d’adressage `192.168.250.0/23` dans la région sélectionnée. Si vous choisissez **Sélectionner**, vous devez :

    a. Sélectionner le bloc d’adresses du réseau virtuel, si vous en avez plusieurs

    b. Entrer un nom pour le nouveau sous-réseau

    c. Sélectionner la taille du sous-réseau. *Veillez à définir une taille de sous-réseau suffisamment grande pour s’adapter à toute future croissance de votre environnement App Service.* Nous recommandons `/25`, qui comprend 128 adresses et peut gérer un environnement App Service de taille maximale. Par exemple, `/28` est déconseillé, car 16 adresses seulement sont disponibles. L’infrastructure utilise au moins cinq adresses. Dans un sous-réseau `/28`, vous vous retrouvez avec une mise à l’échelle maximale de 11 instances.

    d. Sélectionner la plage IP du sous-réseau

9. Sélectionnez **Créer** pour créer l’environnement App Service. Ce processus crée également le plan App Service et l’application. L’environnement App Service, le plan App Service et l’application sont regroupés au sein du même abonnement et du même groupe de ressources. Si votre environnement App Service a besoin d’un groupe de ressources distinct, ou si vous avez besoin d’un environnement App Service ILB, procédez aux étapes permettant de créer un environnement App Service de manière autonome.

## <a name="create-an-ase-by-itself"></a>Créer un ASE autonome ##

Lorsque vous créez un environnement App Service autonome, celui-ci est vide. Même vide, un environnement App Service occasionne des frais mensuels pour l’infrastructure. Effectuez les étapes permettant de créer un environnement App Service ILB ou un environnement App Service dans son propre groupe de ressources. Une fois l’environnement App Service créé, vous pouvez y créer des applications à l’aide de la procédure normale. Sélectionnez votre nouvel environnement App Service comme emplacement.

1. Recherchez **App Service Environment** dans la Place de marché, ou sélectionnez **Nouveau** > **Web + mobile** > **App Service Environment**. 

2. Entrez le nom de votre environnement App Service. Ce nom est utilisé pour les applications créées dans l’environnement App Service. Si le nom est *mynewdemoase*, le nom du sous-domaine est *.mynewdemoase.p.azurewebsites.net*. Si vous créez une application nommée *mytestapp*,celle-ci est adressable à l’adresse mytestapp.mynewdemoase.p.azurewebsites.net. Vous ne pouvez pas utiliser d’espace blanc dans le nom. Si vous utilisez des majuscules dans le nom, le nom de domaine correspond à la version complète de ce nom en minuscules. Si vous utilisez un équilibreur de charge interne (ILB), le nom de votre environnement App Service n’est pas utilisé dans votre sous-domaine, mais il est explicitement indiqué lors de la création de l’environnement App Service.

    ![Attribution d’un nom à l’environnement App Service][5]

3. Sélectionnez votre abonnement. Cet abonnement est également celui que toutes les applications de l’environnement App Service utilisent. Vous ne pouvez pas placer votre environnement App Service dans un réseau virtuel se trouvant dans un autre abonnement.

4. Sélectionnez ou spécifiez un nouveau groupe de ressources. Le groupe de ressources utilisé pour votre environnement App Service doit être le même que celui utilisé pour votre réseau virtuel. Si vous sélectionnez un réseau virtuel existant, la sélection du groupe de ressources pour votre environnement App Service est mise à jour pour refléter celle de votre réseau virtuel. *Si vous utilisez un modèle Resource Manager, vous pouvez créer un environnement App Service avec un groupe de ressources différent de celui du réseau virtuel.* Pour créer un environnement App Service à partir d’un modèle, consultez [Création d’un environnement ASE à l’aide des modèles Azure Resource Manager][MakeASEfromTemplate].

    ![Sélection du groupe de ressources][6]

5. Sélectionnez le réseau virtuel et l’emplacement. Vous pouvez créer un réseau virtuel ou sélectionner un réseau virtuel existant : 

    * Si vous sélectionnez un nouveau réseau virtuel, vous pouvez spécifier un nom et un emplacement. Le nouveau réseau virtuel se voit affecter la plage d’adresses 192.168.250.0/23 et un sous-réseau nommé default. Le sous-réseau reçoit la plage d’adresses 192.168.250.0/24. Vous pouvez uniquement sélectionner un réseau virtuel Resource Manager. La sélection du **type d’adresse IP virtuelle** détermine si votre environnement App Service est accessible directement à partir d’Internet (externe) ou s’il utilise un équilibreur de charge interne (ILB). Pour plus d’informations, consultez [Créer et utiliser un équilibreur de charge interne avec un environnement Azure App Service Environment][MakeILBASE]. 

      * Si vous sélectionnez un **Type d’adresse IP virtuelle** **Externe**, vous pouvez choisir le nombre d’adresses IP externes avec lesquelles est créé le système, en vue d’une utilisation du protocole SSL basé sur IP. 
    
      * Si vous sélectionnez un **Type d’adresse IP virtuelle** **Interne**, vous devez spécifier le domaine que votre environnement App Service utilise. Vous pouvez déployer un environnement App Service dans un réseau virtuel qui utilise des plages d’adresses publiques ou privées. Pour utiliser un réseau virtuel avec une plage d’adresses publiques, vous devez créer le réseau virtuel à l’avance. 
    
    * Si vous sélectionnez un réseau virtuel existant, un nouveau sous-réseau est créé en même temps que l’environnement App Service. *Vous ne pouvez pas utiliser un sous-réseau créé au préalable dans le portail. Si vous utilisez un modèle Resource Manager, vous pouvez créer un environnement App Service avec un sous-réseau existant.* Pour créer un environnement App Service à partir d’un modèle, consultez [Création d’un environnement ASE à l’aide des modèles Azure Resource Manager][MakeASEfromTemplate].

## <a name="app-service-environment-v1"></a>Environnement App Service v1 ##

Vous pouvez toujours créer des instances de la première version d’App Service Environment (ASEv1). Pour commencer, recherchez **App Service Environment v1** dans la Place de marché. Créez l’environnement App Service de la même façon que pour un environnement App Service autonome. Une fois créée, votre instance d’ASEv1 comprend deux front-ends et deux Workers. Avec ASEv1, vous devez gérer les front-ends et les Workers. Ils ne sont pas ajoutés automatiquement lors de la création de vos plans App Service. Les front-ends servent de points de terminaison HTTP/HTTPS et envoient le trafic aux Workers. Les Workers correspondent aux rôles qui hébergent vos applications. Vous pouvez ajuster la quantité de front-ends et de Workers après la création de l’environnement App Service. 

Pour plus d’informations sur ASEv1, consultez [Présentation de l’environnement App Service v1][ASEv1Intro]. Pour plus d’informations sur la mise à l’échelle, la gestion et la surveillance d’ASEv1, consultez [Configuration d’un environnement App Service][ConfigureASEv1].

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: app-service-app-service-environment-intro.md
[webapps]: ../app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
