---
title: aaaCreate un environnement externe Azure App Service
description: "Explique comment toocreate un environnement App Service pendant que vous créez une application ou un autonome"
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
ms.openlocfilehash: f8619534ddd889ea65063733ac6ec11b206e799c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-external-app-service-environment"></a>Créer un environnement App Service externe #

Un environnement Azure App Service est un déploiement d’Azure App Service dans un sous-réseau de réseau virtuel Azure. Il existe deux façons toodeploy un environnement App Service (ASE) :

- avec une adresse IP virtuelle sur une adresse IP externe, solution souvent appelée ASE externe ;
- Avec hello VIP sur une adresse IP interne, souvent appelé un environnement app service Équilibrage de charge interne, car le point de terminaison interne hello est un équilibreur de charge interne (ILB).

Cet article vous montre comment toocreate ASE externe. Pour une vue d’ensemble de hello ASE, consultez [un environnement App Service de toohello introduction][Intro]. Pour plus d’informations sur comment toocreate un équilibrage de charge interne ASE, consultez [créer et utiliser un environnement app service Équilibrage de charge interne][MakeILBASE].

## <a name="before-you-create-your-ase"></a>Avant de créer votre ASE ##

Après avoir créé votre ASE, vous ne pouvez pas modifier suivant de hello :

- Lieu
- Abonnement
- Groupe de ressources
- Réseau virtuel utilisé
- Sous-réseau utilisé
- Taille du sous-réseau

> [!NOTE]
> Lorsque vous sélectionnez un réseau virtuel et que vous spécifiez un sous-réseau, assurez-vous qu’il s’agit d’une croissance future tooaccommodate suffisante. Nous vous recommandons une taille de `/25` avec 128 adresses.
>

## <a name="three-ways-toocreate-an-ase"></a>Trois méthodes toocreate ASE ##

Il existe trois façons toocreate ASE :

- **Dans le cadre d’un plan App Service**. Cette méthode crée hello ASE et hello plan App Service en une seule étape.
- **De façon autonome**. Avec cette méthode, seul l’environnement App Service est créé. Cette méthode est un toocreate de processus ASE plus avancée. Vous utilisez toocreate ASE avec un équilibrage de charge interne.
- **À l’aide d’un modèle Azure Resource Manager**. Cette méthode est destinée aux utilisateurs expérimentés. Pour plus d’informations, consultez [Création d’un environnement ASE à l’aide des modèles Azure Resource Manager][MakeASEfromTemplate].

Un environnement app service externe a une adresse IP virtuelle publique, ce qui signifie que toutes les applications de toohello le trafic HTTP/HTTPS Bonjour ASE accède à une adresse IP accessible via internet. Un environnement app service avec un équilibrage de charge interne possède une adresse IP du sous-réseau hello utilisé par hello ASE. Hello applications hébergées dans un environnement app service Équilibrage de charge interne ne sont pas exposées directement toohello internet.

## <a name="create-an-ase-and-an-app-service-plan-together"></a>Créer un ASE et un plan App Service ensemble ##

Hello plan App Service est un conteneur d’applications. Lorsque vous créez une application dans App Service, vous devez sélectionner ou créer un plan App Service. environnements de modèle de conteneur Hello contiennent les plans de Service d’applications et les plans App Service applications.

toocreate ASE pendant que vous créez un plan App Service :

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez **nouveau** > **Web + Mobile** > **application Web**.

    ![Création d’une application web][1]

2. Sélectionnez votre abonnement. application Hello et hello ASE sont créés dans hello même abonnements.

3. Sélectionnez ou créez un groupe de ressources. Vous pouvez utiliser des groupes de ressources pour gérer des ressources Azure connexes en tant qu’unité. Les groupes de ressources sont également utiles lorsque vous souhaitez établir des règles de contrôle d’accès en fonction du rôle (RBAC) pour vos applications. Pour plus d’informations, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure][ARMOverview].

4. Sélectionnez hello plan App Service, puis **créer un nouveau**.

    ![Nouveau plan App Service][2]

5. Bonjour **emplacement** liste déroulante, sélectionnez hello la région où toocreate hello ASE. Si vous sélectionnez un environnement App Service existant, aucun environnement App Service n’est créé. Hello plan App Service est créé dans hello ASE que vous avez sélectionné. 

6. Sélectionnez **niveau tarifaire**, sélectionnez une des hello **isolé** tarification références (SKU). Si vous choisissez une carte de référence SKU **Isolé** et un emplacement autre qu’un environnement App Service, un nouvel environnement App Service est créé à cet emplacement. toostart hello processus toocreate ASE, sélectionnez **sélectionnez**. Hello **isolé** référence (SKU) n’est disponible qu’en association avec un environnement app service. Vous ne pouvez pas utiliser une autre référence SKU de tarification dans un environnement App Service qui n’est pas **Isolé**.

    ![Sélection du niveau tarifaire][3]

7. Entrez le nom hello pour votre ASE. Ce nom est utilisé dans le nom de hello adressable pour vos applications. Si le nom de hello ASE hello est _appsvcenvdemo_, nom de domaine hello est *. appsvcenvdemo.p.azurewebsites.net*. Si vous créez une application nommée *mytestapp*, elle est adressable à l’adresse mytestapp.appsvcenvdemo.p.azurewebsites.net. Vous ne pouvez pas utiliser un espace blanc dans le nom de hello. Si vous utilisez des caractères majuscules, nom de domaine hello est hello total version en minuscule du même nom.

    ![Nom du nouveau plan App Service][4]

8. Spécifiez les informations concernant votre réseau virtuel Azure. Choisissez **Créer un nouveau** ou **Sélectionner**. Hello option tooselect un réseau virtuel existant est disponible uniquement si vous avez un réseau virtuel dans une région de hello sélectionnée. Si vous sélectionnez **créer un nouveau**, entrez un nom pour hello réseau virtuel. Un nouveau réseau virtuel Resource Manager portant ce nom est alors créé. Il utilise l’espace d’adressage hello `192.168.250.0/23` dans une région de hello sélectionnée. Si vous choisissez **Sélectionner**, vous devez :

    a. Sélectionner un bloc d’adresses réseau virtuel hello, si vous avez plusieurs.

    b. Entrer un nom pour le nouveau sous-réseau

    c. Sélectionnez la taille du sous-réseau de hello hello. *N’oubliez pas de tooselect une taille suffisamment grande tooaccommodate une croissance future de votre ASE.* Nous recommandons `/25`, qui comprend 128 adresses et peut gérer un environnement App Service de taille maximale. Par exemple, `/28` est déconseillé, car 16 adresses seulement sont disponibles. L’infrastructure utilise au moins cinq adresses. Dans un sous-réseau `/28`, vous vous retrouvez avec une mise à l’échelle maximale de 11 instances.

    d. Sélectionnez plage IP de sous-réseau hello.

9. Sélectionnez **créer** toocreate hello ASE. Ce processus crée également le plan App Service hello et application hello. Hello ASE, plan App Service et application sont tous sous hello même abonnement et également dans hello même groupe de ressources. Si votre ASE a besoin d’un groupe de ressources distinct, ou si vous avez besoin d’un environnement app service Équilibrage de charge interne, suivez hello étapes toocreate ASE par lui-même.

## <a name="create-an-ase-by-itself"></a>Créer un ASE autonome ##

Lorsque vous créez un environnement App Service autonome, celui-ci est vide. ASE vide entraîne toujours des frais mensuels pour l’infrastructure de hello. Suivez ces étapes de toocreate ASE avec un équilibrage de charge interne ou toocreate ASE dans son propre groupe de ressources. Après avoir créé votre ASE, vous pouvez créer des applications qu’il contient à l’aide du processus normal de hello. Sélectionnez votre nouvelle ASE en tant qu’emplacement de hello.

1. Recherche hello Azure Marketplace pour **environnement App Service**, ou sélectionnez **nouveau** > **Web Mobile** > **du Service d’applications Environnement**. 

2. Entrez le nom hello de votre ASE. Ce nom est utilisé pour les applications hello créées Bonjour ASE. Si le nom hello est *mynewdemoase*, le nom de sous-domaine hello est *. mynewdemoase.p.azurewebsites.net*. Si vous créez une application nommée *mytestapp*,celle-ci est adressable à l’adresse mytestapp.mynewdemoase.p.azurewebsites.net. Vous ne pouvez pas utiliser un espace blanc dans le nom de hello. Si vous utilisez des caractères majuscules, nom de domaine hello est hello total version en minuscule du nom de hello. Si vous utilisez un équilibreur de charge interne (ILB), le nom de votre environnement App Service n’est pas utilisé dans votre sous-domaine, mais il est explicitement indiqué lors de la création de l’environnement App Service.

    ![Attribution d’un nom à l’environnement App Service][5]

3. Sélectionnez votre abonnement. Cet abonnement est également hello un type qui utilisent de toutes les applications Bonjour ASE. Vous ne pouvez pas placer votre environnement App Service dans un réseau virtuel se trouvant dans un autre abonnement.

4. Sélectionnez ou spécifiez un nouveau groupe de ressources. groupe de ressources Hello utilisée pour votre ASE doit être hello même que celui qui est utilisé pour votre réseau virtuel. Si vous sélectionnez un réseau virtuel existant, sélection du groupe de ressources pour votre ASE hello est tooreflect mis à jour de votre réseau virtuel. *Vous pouvez créer un environnement app service avec un groupe de ressources qui est différent du groupe de ressources du réseau virtuel hello si vous utilisez un modèle de gestionnaire de ressources.* toocreate ASE à partir d’un modèle, consultez [créer un environnement App Service à partir d’un modèle][MakeASEfromTemplate].

    ![Sélection du groupe de ressources][6]

5. Sélectionnez le réseau virtuel et l’emplacement. Vous pouvez créer un réseau virtuel ou sélectionner un réseau virtuel existant : 

    * Si vous sélectionnez un nouveau réseau virtuel, vous pouvez spécifier un nom et un emplacement. Hello nouveau réseau virtuel a hello adresse plage 192.168.250.0/23 et un sous-réseau nommé par défaut. sous-réseau de Hello est défini comme 192.168.250.0/24. Vous pouvez uniquement sélectionner un réseau virtuel Resource Manager. Hello **Type d’adresse IP virtuelle** sélection détermine si votre ASE est directement accessible à partir de hello internet (externe) ou si elle utilise un équilibrage de charge interne. toolearn savoir plus sur ces options, consultez [créer et utiliser un équilibreur de charge interne avec un environnement App Service][MakeILBASE]. 

      * Si vous sélectionnez **externe** pour hello **Type d’adresse IP virtuelle**, vous pouvez sélectionner le système de hello d’adresses IP externes combien est créée avec fins SSL basé sur IP. 
    
      * Si vous sélectionnez **interne** pour hello **Type d’adresse IP virtuelle**, vous devez spécifier le domaine de hello votre ASE utilise. Vous pouvez déployer un environnement App Service dans un réseau virtuel qui utilise des plages d’adresses publiques ou privées. toouse un réseau virtuel avec une plage d’adresses publiques, vous devez toocreate hello réseau virtuel à l’avance. 
    
    * Si vous sélectionnez un réseau virtuel existant, un nouveau sous-réseau est créé lors de la création de hello ASE. *Vous ne pouvez pas utiliser un sous-réseau créé au préalable dans le portail de hello. Si vous utilisez un modèle Resource Manager, vous pouvez créer un environnement App Service avec un sous-réseau existant.* toocreate ASE à partir d’un modèle, consultez [créer un environnement App Service à partir d’un modèle][MakeASEfromTemplate].

## <a name="app-service-environment-v1"></a>Environnement App Service v1 ##

Vous pouvez toujours créer des instances de la première version de hello d’environnement App Service (ASEv1). toostart qui traitent, hello de recherche Marketplace pour **environnement App Service v1**. Vous créez hello ASE Bonjour même façon que vous créez hello autonome ASE. Une fois créée, votre instance d’ASEv1 comprend deux front-ends et deux Workers. Avec ASEv1, vous devez gérer les processus de travail et frontaux hello. Ils ne sont pas ajoutés automatiquement lors de la création de vos plans App Service. frontaux Hello agisse en tant que points de terminaison HTTP/HTTPS hello et envoyer le trafic toohello travailleurs. les travailleurs Hello sont des rôles hello hébergent vos applications. Vous pouvez ajuster la quantité de hello des serveurs frontaux et des travailleurs après avoir créé votre ASE. 

toolearn en savoir plus sur ASEv1, consultez [Introduction toohello environnement App Service v1][ASEv1Intro]. Pour plus d’informations sur la mise à l’échelle, gérer et surveiller ASEv1, consultez [comment tooconfigure un environnement App Service][ConfigureASEv1].

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
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
