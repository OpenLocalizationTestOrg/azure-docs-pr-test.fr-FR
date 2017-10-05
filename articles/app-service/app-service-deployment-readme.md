---
title: "Déploiement d’applications vers Azure App Service"
description: "Découvrir le fonctionnement du déploiement d’applications vers App Service"
keywords: "app service, azure app service, déployer, déploiement"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 347e8b5177eac8e08ab0dea701b736b86d23904a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="82c61-104">Vue d’ensemble du déploiement d’Azure App Service</span><span class="sxs-lookup"><span data-stu-id="82c61-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="82c61-105">Azure App Service fournit un ensemble de fonctionnalités enrichies et intégrées destiné à prendre en charge la création de flux de travail de déploiement puissants et flexibles.</span><span class="sxs-lookup"><span data-stu-id="82c61-105">Azure App Service provides a rich and integrated feature set to support creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="82c61-106">Le déploiement d’applications peut tirer parti d’options, notamment de l’intégration continue ou de la publication du contrôle de code source local, de WebDeploy et du FTP.</span><span class="sxs-lookup"><span data-stu-id="82c61-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="82c61-107">La méthode recommandée pour le déploiement des applications de production est l’échange des emplacements de déploiement.</span><span class="sxs-lookup"><span data-stu-id="82c61-107">The recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="82c61-108">Les emplacements de déploiement représentent les environnements intermédiaires et d’intégration associés aux applications de production.</span><span class="sxs-lookup"><span data-stu-id="82c61-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="82c61-109">Ils peuvent être configurés et ciblés avec le trafic web pour la validation, et le trafic peut être échangé à la demande pour le déploiement vers la production, sans temps d’arrêt ni mise en route automatisée.</span><span class="sxs-lookup"><span data-stu-id="82c61-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment to production with no down time and automated warm-up.</span></span> <span data-ttu-id="82c61-110">Les étapes d’un flux de travail de déploiement peuvent être facilement automatisées via les produits de gestion des mises en production comme Visual Studio Release Management.</span><span class="sxs-lookup"><span data-stu-id="82c61-110">The steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="82c61-111">Cela est utile pour la coordination avec d’autres ressources de la solution (par exemple, la banque de données), la périodicité et la réplication entre plusieurs unités de déploiement.</span><span class="sxs-lookup"><span data-stu-id="82c61-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

