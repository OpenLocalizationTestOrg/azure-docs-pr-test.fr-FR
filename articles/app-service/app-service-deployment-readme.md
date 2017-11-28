---
title: "Applications d’aaaDeploying tooAzure du Service d’applications"
description: Analyser le fonctionnement des applications de tooDeploy tooApp Service
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
ms.openlocfilehash: 925341e12daf3cb05b25199f5c5218e82f062f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="c3224-104">Vue d’ensemble du déploiement d’Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c3224-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="c3224-105">Service d’applications Azure fournit un riche et la fonctionnalité intégrée toosupport création de workflows de déploiement puissant et flexible.</span><span class="sxs-lookup"><span data-stu-id="c3224-105">Azure App Service provides a rich and integrated feature set toosupport creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="c3224-106">Le déploiement d’applications peut tirer parti d’options, notamment de l’intégration continue ou de la publication du contrôle de code source local, de WebDeploy et du FTP.</span><span class="sxs-lookup"><span data-stu-id="c3224-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="c3224-107">Hello recommandé de méthode pour le déploiement d’applications de production est échange d’emplacement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c3224-107">hello recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="c3224-108">Les emplacements de déploiement représentent les environnements intermédiaires et d’intégration associés aux applications de production.</span><span class="sxs-lookup"><span data-stu-id="c3224-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="c3224-109">Les emplacements de déploiement peuvent être configurés et ciblés avec le trafic web pour la validation et le trafic peut être transférée à la demande pour tooproduction de déploiement sans temps mort bas et automatisée de préchauffage.</span><span class="sxs-lookup"><span data-stu-id="c3224-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment tooproduction with no down time and automated warm-up.</span></span> <span data-ttu-id="c3224-110">étapes Hello d’un flux de travail de déploiement peuvent être facilement automatisées via la version des produits de gestion telles que la gestion de version de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3224-110">hello steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="c3224-111">Cela est utile pour la coordination avec d’autres ressources de la solution (par exemple, la banque de données), la périodicité et la réplication entre plusieurs unités de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c3224-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

