---
title: aaaAzure Windows Virtual Machine DotNet Core didacticiel 1 | Documents Microsoft
description: Didacticiel sur DotNet Core pour les machines virtuelles Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 14d5f250-1f76-49d4-898f-07b58fd39e7c
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8df69c496f44acb02d8afc45695349ec1f558f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toowindows-virtual-machines"></a>Automatisation des applications déploiements tooWindows Machines virtuelles

Cette série en quatre parties détaille le déploiement et la configuration des ressources et applications Azure à l’aide de modèles Azure Resource Manager. Dans cette série, un exemple de modèle est déployé et hello examinée de modèle de déploiement. objectif de Hello de cette série est tooeducate sur la relation hello entre les ressources Azure et tooprovide véritable expérience pratique sur les modèles Azure Resource Manager entièrement intégrée de déploiement. Ce document suppose que le lecteur dispose d’un niveau de connaissance élémentaire concernant Azure Resource Manager. Avant de commencer ce didacticiel, nous vous recommandons de vous familiariser avec les concepts de base d’Azure Resource Manager.

## <a name="music-store-application"></a>Application du Store musique
Hello exemple utilisé dans cette série est .net application Core en simulant un magasin de musique expérience d’achat. Cette application peut être déployée tooeither un système virtuel Windows ou Linux, exemple déploiements ont été créés pour les deux. application Hello inclut une application web et une base de données SQL. Avant de lire les articles de cette série de hello, déployez une application hello à l’aide du bouton de déploiement hello trouvé sur cette page. Lorsque le déploiement complet, hello architecture application / Azure ressemble à hello suivant schéma. 

modèle de gestionnaire de ressources de magasin de musique Hello se trouve ici, [modèle Windows de magasin de musique](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)

![Application du Store musique](./media/dotnet-core-1-landing/music-store.png)

Chacun de ces composants, y compris hello associez-y un modèle JSON est examiné dans hello suivant quatre articles.

* [**Architecture de l’application** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : les composants d’Application tels que les sites web et bases de données doivent toobe hébergé sur des ressources de l’ordinateur Azure tels que les ordinateurs virtuels et des bases de données SQL Azure. Ce document décrit la nécessité de calcul de mappage, les ressources de tooAzure et déploiement de ces ressources avec un modèle Azure Resource Manager. 
* [**Accès et sécurité** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – lors de l’hébergement d’applications dans Azure, il est nécessaire tooconsider application hello est accessible et découvrez comment les différents composants d’applications les uns aux autres. Ce document décrit en détail fournissant et sécurisation internet access tooan accès aux applications et entre les composants de l’application.
* [**Disponibilité et l’échelle** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : disponibilité et l’échelle reportez-vous toostay de capacité toohello applications en cours d’exécution pendant l’arrêt de l’infrastructure et hello capacité tooscale de calcul à la demande de ressources toomeet application. Ce document détails hello les composants nécessaires toodeploy à charge équilibrée et application hautement disponible.
* [**Déploiement d’application** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : quand le déploiement d’applications sur des Machines virtuelles Azure, méthode hello par le hello les fichiers binaires d’application sont installés sur hello Machine virtuelle doit être prises en compte. Ce document détaille l’automatisation de l’installation d’applications à l’aide d’extensions de script personnalisé pour machine virtuelle Azure.

Hello lors du développement de modèles Azure Resource Manager vise déploiement de hello tooautomate d’Infrastructure Azure et l’installation de hello et configuration de toutes les applications hébergées sur cette infrastructure Azure. Ces articles fournissent un exemple de cette expérience.

## <a name="deploy-hello-music-store-application"></a>Déployer l’application de magasin de musique hello
Hello application de magasin de musique peut être déployé à l’aide de ce bouton.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-windows%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/>
</a>

modèle de gestionnaire de ressources Azure Hello requiert hello des valeurs de paramètre suivantes.

| Nom du paramètre | Description |
| --- | --- |
| ADMINUSERNAME |Nom d’utilisateur Admin qui est utilisé sur l’ordinateur virtuel de hello et hello de base de données SQL Azure. |
| ADMINPASSWORD |Mot de passe qui est utilisé sur hello Machine virtuelle Azure et base de données SQL. |
| NUMBEROFINSTANCES |nombre de Hello de toobe d’ordinateurs virtuels créé. Chacune de ces applications web, machines virtuelles hôte hello magasin de musique et tout le trafic sont équilibrée entre elles. |
| PUBLICIPADDRESSDNSNAME |Nom DNS global unique associé hello adresse IP publique. |

Lorsque le déploiement d’un modèle hello terminée, accédez à toohello d’adresses IP publique à l’aide de n’importe quel navigateur internet. Hello .net site Core musique s’affiche.

## <a name="next-steps"></a>Étapes suivantes
<hr>

[Étape 1 : architecture d’application avec les modèles Azure Resource Manager](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Étape 2 : accès et sécurité dans les modèles Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Étape 3 : disponibilité et mise à l’échelle dans les modèles Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Étape 4 : déploiement d’application avec des modèles Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

