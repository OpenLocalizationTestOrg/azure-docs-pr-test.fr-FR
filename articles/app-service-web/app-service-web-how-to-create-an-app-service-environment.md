---
title: aaaHow tooCreate un v1 environnement App Service
description: "Description du flux de création pour un environnement App Service Environment v1"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>Comment tooCreate un v1 environnement App Service 

> [!NOTE]
> Cet article porte sur hello environnement App Service v1. Il existe une version plus récente de hello environnement App Service toouse plus facile et s’exécute sur une infrastructure plus puissante. toolearn plus d’informations sur la nouvelle version de hello commencent par Bonjour [Introduction toohello environnement App Service](../app-service/app-service-environment/intro.md).
> 

### <a name="overview"></a>Vue d'ensemble
Hello environnement de Service d’application (ASE) est une option de service Premium d’Azure App Service qui offre une fonctionnalité d’amélioration de la configuration qui n’est pas disponible dans les tampons d’architecture mutualisée hello. fonctionnalité de ASE Hello déploie essentiellement hello du Service d’applications Azure dans le réseau virtuel du client. toogain une meilleure compréhension des fonctionnalités de hello offertes par les environnements App Service lire hello [qu’est un environnement App Service] [ WhatisASE] documentation.

### <a name="before-you-create-your-ase"></a>Avant de créer votre ASE
Il est important toobe prenant en charge les éléments hello que vous ne pouvez pas modifier. Voici les aspects que vous ne pouvez pas modifier concernant votre ASE après sa création :

* Lieu
* Abonnement
* Groupe de ressources
* Réseau virtuel utilisé
* Sous-réseau utilisé 
* Taille du sous-réseau

Lorsqu’un réseau virtuel de prélèvement et spécification d’un sous-réseau, vérifier qu’il est assez grand tooaccomodate toute croissance future. 

### <a name="creating-an-app-service-environment-v1"></a>Création d’un environnement App Service Environment v1
toocreate un v1 environnement App Service que vous avez besoin de toosearch hello Azure Marketplace pour ***environnement App Service v1***, ou en passant par le nouveau -> Web + Mobile -> environnement App Service. toocreate un ASEv1 :

1. Fournir le nom hello de votre ASE. nom de Hello est spécifié pour hello ASE servira pour les applications hello créées Bonjour ASE. Si le nom de hello ASE est appsvcenvdemo nom de sous-domaine hello serait. *appsvcenvdemo.p.azurewebsites.net*. Par conséquent, si vous créez une application nommée *mytestapp*, elle est adressable à l’adresse *mytestapp.appsvcenvdemo.p.azurewebsites.net*. Vous ne pouvez pas utiliser un espace blanc dans le nom de votre ASE de hello. Si vous utilisez des caractères majuscules dans le nom de hello, nom de domaine hello sera hello total version en minuscule du même nom. Si vous utilisez un ILB, le nom de votre ASE n’est pas utilisé dans votre sous-domaine mais explicitement indiqué lors de la création de l’ASE.
   
    ![][1]
2. Sélectionnez votre abonnement. abonnement Hello utilisée pour votre ASE est également hello une qui seront créées avec toutes les applications dans ce ASE. Vous ne pouvez pas placer votre ASE dans un réseau virtuel qui se trouve dans un autre abonnement.
3. Sélectionnez ou spécifiez un nouveau groupe de ressources. groupe de ressources Hello utilisée pour votre ASE même qui est utilisée pour votre réseau virtuel doit être hello. Si vous sélectionnez un réseau virtuel existant, sélection du groupe de ressources pour votre ASE hello tooreflect mis à jour de votre réseau virtuel.
   
    ![][2]
4. Effectuez vos sélections de réseau virtuel et d’emplacement. Vous pouvez choisir toocreate un nouveau réseau virtuel ou sélectionnez un réseau virtuel existant. Si vous sélectionnez un réseau virtuel, vous pouvez indiquer un nom et un emplacement. Hello nouveau réseau virtuel aura hello adresse plage 192.168.250.0/23 et un sous-réseau nommé **par défaut** qui est défini en tant que 192.168.250.0/24. Vous pouvez aussi simplement sélectionner un réseau virtuel préexistant classique ou du Gestionnaire de ressources. sélection du Type d’adresse IP virtuelle de Hello détermine si votre ASE est directement accessible à partir de hello internet (externe) ou si elle utilise un équilibrage de charge interne (ILB). toolearn plus d’informations sur les lire [à l’aide d’un équilibreur de charge interne avec un environnement App Service][ILBASE]. Si vous sélectionnez un type d’adresse IP virtuelle d’externes vous pouvez sélectionner le système de hello d’adresses IP externes combien est créée avec fins IPSSL. Si vous sélectionnez interne vous devez sous-domaine hello toospecify que votre ASE utilisera. Les ASE peuvent être déployés dans les réseaux virtuels qui utilisent *soit* des plages d’adresses publiques, *soit* des espaces d’adressage RFC1918 (par exemple, des adresses privées). Dans l’ordre toouse un réseau virtuel avec une plage d’adresses publiques, vous devez toocreate hello réseau virtuel à l’avance. Lorsque vous sélectionnez un réseau virtuel existant vous devez toocreate un nouveau sous-réseau lors de la création de ASE. **Vous ne pouvez pas utiliser un sous-réseau créé au préalable dans le portail de hello. Vous pouvez créer un ASE avec un sous-réseau pré-existant si vous le créez à l’aide d’un modèle Resource Manager.** toocreate ASE à partir d’un modèle Aidez-vous hello ici, [création d’un environnement App Service à partir du modèle] [ ILBAseTemplate] et ici, [création d’un environnement d’équilibrage de charge interne App Service à partir du modèle] [ASEfromTemplate].

### <a name="details"></a>Détails
Un ASE est créé avec 2 serveur frontaux et 2 travaux. Frontaux Hello agir en tant que points de terminaison HTTP/HTTPS hello et envoyer le trafic toohello les traitements qui sont des rôles hello qui hébergent vos applications. Vous pouvez ajuster la quantité de hello après la création de ASE et peut même configurer des règles de mise à l’échelle de ces pools de ressources. Pour plus d’informations sur la mise à l’échelle manuelle, gestion et surveillance d’un environnement App Service ici : [comment tooconfigure un environnement App Service][ASEConfig] 

Uniquement les un ASE hello peuvent exister dans le sous-réseau hello utilisé par hello ASE. sous-réseau de Hello ne peut pas être utilisé pour autre chose qu’hello ASE

### <a name="after-app-service-environment-v1-creation"></a>Après la création d’un environnement App Service Environment v1
Après la création d'un ASE, vous pouvez ajuster les éléments suivants :

* Quantité de serveurs frontaux (minimum : 2)
* Quantité de travaux (minimum : 2)
* Quantité d’adresses IP disponibles pour IP SSL
* Les tailles de ressources utilisées par hello frontaux ou threads de travail de calcul (la taille minimale du serveur frontal est P2)

Il existe plus de détails sur manuel Mise à l’échelle, gestion et surveillance des environnements de Service d’application ici : [comment tooconfigure un environnement App Service][ASEConfig] 

Pour plus d’informations sur l’échelle automatique est un guide ici : [comment échelle tooconfigure pour un environnement App Service][ASEAutoscale]

Il existe des dépendances supplémentaires qui ne sont pas disponibles pour la personnalisation, telles que la base de données hello et de stockage. Celles-ci sont gérées par Azure et sont fournis avec le système de hello. Hello système stockage prend en charge des Go too500 pour hello l’intégralité de l’environnement App Service et la base de données hello est ajustée par Azure, si nécessaire par l’échelle hello du système de hello.

## <a name="getting-started"></a>Prise en main
Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

tooget a démarré avec l’environnement App Service v1, consultez [Introduction toohello environnement App Service v1][WhatisASE]

Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
