---
title: options - Services de cloud computing de calcul aaaAzure | Documents Microsoft
description: "Découvrez les options hébergement de calcul Azure et leur fonctionnement : App Service, Cloud Services et Virtual Machines"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
ms.assetid: ed7ad348-6018-41bb-a27d-523accd90305
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: e7f109a54c61cc2f37644d39a61d2d932a374587
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-choose-cloud-services-or-something-else"></a>Dois-je choisir Cloud Services ou un autre service ?
Constitue le choix de hello de Services de cloud computing de Azure pour vous ? Azure propose différents modèles d’hébergement d’applications. Chacun d’eux fournit un ensemble de services différent, donc celui que vous choisissez dépend d’exactement ce que vous essayez toodo.

[!INCLUDE [compute-table](../../includes/compute-options-table.md)]

<a name="tellmecs"></a>

## <a name="tell-me-about-cloud-services"></a>En savoir plus sur Cloud Services
Cloud Services est un exemple de [platform as a service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS). Comme [du Service d’applications](../app-service-web/app-service-web-overview.md), cette technologie est conçue toosupport des applications évolutives, fiables et toooperate bon marché. Tout comme un Service d’application est hébergé sur des machines virtuelles, par conséquent, sont également des Services de cloud computing, toutefois, vous avez davantage de contrôle sur les machines virtuelles de hello. Vous pouvez installer votre logiciel sur des machines virtuelles de Cloud Service et vous y connecter à distance.

![cs_diagram](./media/cloud-services-choose-me/diagram.png)

Un contrôle supérieur signifie également une convivialité réduite. Sauf si vous avez besoin d’options de contrôle supplémentaires hello, c’est généralement plus rapide et plus facile de tooget une application web et en cours d’exécution dans les applications Web dans le Service d’applications par rapport à tooCloud Services.

Il existe deux types de rôle de service cloud. Bonjour seule différence entre hello deux est comment votre rôle est hébergé sur l’ordinateur virtuel de hello.

* **Rôle Web**  
Déploie et héberge automatiquement votre application, via IIS.

* **Rôle de travail**  
Exécute votre application de façon autonome, sans utiliser IIS.

Par exemple, une application simple peut utiliser un rôle web unique, servant un site web. Une application plus complexe peut utiliser un toohandle de rôle web les demandes entrantes provenant d’utilisateurs, puis passer ces demandes sur le rôle de travail tooa pour le traitement. (Cette communication pourrait utiliser [Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md) ou les [files d’attente Azure](../storage/common/storage-introduction.md).)

En tant que hello suggère la figure précédente, tous hello des machines virtuelles dans une application unique qui s’exécutent dans hello même service cloud. Utilisateurs accès hello application via une adresse IP publique unique, avec les requêtes automatiquement la charge équilibrée sur les machines virtuelles de l’application hello. plateforme de Hello [met à l’échelle et déploie](cloud-services-how-to-scale.md) hello des machines virtuelles dans une application de Services de cloud computing d’une façon qui permet d’éviter un point unique d’une défaillance matérielle.

Bien que les applications s’exécutent sur des machines virtuelles, il est important toounderstand que Services de cloud computing offre PaaS, pas IaaS. Voici une façon toothink concernant : avec IaaS, telles que des Machines virtuelles Azure, vous tout d’abord créer et configurer l’environnement hello exécute votre application, puis déployer votre application dans cet environnement. Vous êtes chargé de gérer une grande partie de ce monde, faire les choses telles que le déploiement de nouvelles versions de correctifs de système d’exploitation hello chaque machine virtuelle. Dans PaaS, en revanche, il est comme si hello environnement existe déjà. Tout ce que vous avez toodo est de déployer votre application. Gestion de plateforme hello qu'il s’exécute, y compris pour déployer de nouvelles versions du système d’exploitation de hello, est traitée pour vous.

## <a name="scaling-and-management"></a>Mise à l'échelle et gestion
Avec Cloud Services, vous ne créez pas de machines virtuelles. Au lieu de cela, vous fournissez un fichier de configuration qui indique à Azure de leur nombre souhaité, tel que **trois instances de rôle web** et **deux instances de rôle de travail**, et la plateforme de hello crée pour vous.  Vous continuez de choisir [la taille](cloud-services-sizes-specs.md) que doivent avoir ces machines virtuelles de stockage, mais vous ne les créez pas vous-même de manière explicite. Si votre application doit toohandle une charge plus importante, vous pouvez demander davantage d’ordinateurs virtuels et Azure crée ces instances. Si la charge de hello diminue, vous pouvez arrêter ces instances et arrêter la payer pour eux.

Une application de Services de cloud computing est généralement établie toousers disponible via un processus en deux étapes. Un développeur de première [téléchargements hello application](cloud-services-how-to-create-deploy.md) toohello plate-forme de zone de transfert. Lorsque le développeur de hello est prêt application hello de toomake live, ils utilisent intermédiaire de Azure tooswap portail hello avec la production. Cela [basculer d’un intermédiaire et de production](cloud-services-nodejs-stage-application.md) peut être effectuée sans temps mort, ce qui permet à une application en cours d’exécution d’être mis à niveau tooa une nouvelle version sans porter atteinte à ses utilisateurs.

## <a name="monitoring"></a>Surveillance
Cloud Services fournit également la surveillance. Comme des Machines virtuelles Azure, il détecte un serveur physique ayant échoué et redémarre les machines virtuelles hello en cours d’exécution sur ce serveur sur un nouvel ordinateur. Mais Cloud Services détecte aussi les échecs des machines virtuelles et des applications, et pas seulement les défaillances matérielles. Contrairement aux Machines virtuelles, il dispose d’un agent à l’intérieur de chaque rôle web et de travail, et il est donc en mesure de toostart nouvelles machines virtuelles et instances de l’application lorsque des erreurs se produisent.

Hello nature PaaS des Services Cloud a des autres conséquences, trop. Une des hello plus important est que les applications basées sur cette technologie doivent être écrit toorun correctement en cas d’échec de n’importe quelle instance de rôle web ou de travail. tooachieve cela, une application ne doit pas tenir à jour des Services de cloud computing dans l’état hello du système de fichiers de ses propres machines virtuelles. Contrairement aux ordinateurs virtuels créés avec des Machines virtuelles Azure, écritures effectuées tooCloud, Services de machines virtuelles ne sont pas persistants ; Il est nothing, comme un disque de données de Machines virtuelles. Au lieu de cela, une application doit explicitement des Services de cloud computing écrire tous les tooSQL état de la base de données, les objets BLOB, tables, ou un autre stockage externe. Création d’applications de cette manière, les rend tooscale plus facile et plus résistant toofailure, les deux principaux objectifs des Services Cloud.

## <a name="next-steps"></a>Étapes suivantes
[Créer une application de service cloud dans .NET](cloud-services-dotnet-get-started.md)  
[Créer une application de service cloud dans Node.js](cloud-services-nodejs-develop-deploy-app.md)  
[Créer une application de service cloud dans PHP](../cloud-services-php-create-web-role.md)  
[Création d’une application de service cloud dans Python](cloud-services-python-ptvs.md)

