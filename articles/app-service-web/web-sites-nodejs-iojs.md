---
title: io.js de toouse aaaHow avec Azure App Service Web Apps
description: "Découvrez comment toouse une application web dans Azure App Service avec io.js."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>Comment io.js toouse avec Azure App Service Web Apps
branchement de nœud populaires Hello [io.js] fonctionnalités de projet de Node.js de tooJoyent différences différents, y compris un modèle de gouvernance plus ouvert, un cycle de publication plus rapide et une adoption plus rapide de nouvelles fonctionnalités JavaScript expérimentales.

Bien que de nombreuses versions de Node.js soient préinstallées dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps, il accepte aussi les binaires Node.js fournis par les utilisateurs. Cet article décrit deux méthodes l’activation hello de io.js sur les applications Web App Service : hello l’utilisation d’un script de déploiement étendue, qui configure automatiquement la version la plus récente disponible io.js toouse Azure hello, ainsi que le chargement manuel d’un fichier binaire io.js hello. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Utilisation d'un script de déploiement
Lors du déploiement d’une application Node.js, les applications Web App Service s’exécute un nombre de petites commandes tooensure qui hello environnement est correctement configuré. À l’aide d’un script de déploiement, ce processus peut être téléchargement de hello tooinclude personnalisé et de la configuration de io.js.

Hello [io.js Script de déploiement](https://github.com/felixrieseberg/iojs-azure) est disponible sur GitHub. io.js tooenable sur votre application web, il suffit de copier **.deployment**, **deploy.cmd** et **IISNode.yml** racine toohello de votre dossier d’application et déployer des applications de tooWeb.  

premier fichier de Hello, **.deployment**, fait en sorte que les applications Web toorun **deploy.cmd** lors du déploiement. Ce script s’exécute toutes les étapes habituelles hello pour une application Node.js, mais télécharge aussi la version la plus récente de io.js hello. Enfin, **IISNode.yml** Configure Web Apps toouse hello simplement téléchargé io.js binaire au lieu d’un binaire Node.js préinstallé.

> [!NOTE]
> tooupdate hello utilisé io.js binaire, simplement redéployez l’application - script de hello télécharge une nouvelle version de io.js que chaque application hello de temps unique est déployée.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Utilisation de l'installation manuelle
une installation manuelle d’une version personnalisée io.js Hello comprend uniquement deux étapes. Commencez par télécharger hello **win-x64** binaire directement à partir de hello [io.js distribution]. Deux fichiers sont nécessaires : **iojs.exe** et **iojs.lib**. Enregistrer les deux fichiers dossier tooa à l’intérieur de votre application web, par exemple dans **bin/iojs**.

tooconfigure Web Apps toouse **iojs.exe** au lieu d’une version préinstallée de nœud, créez un **IISNode.yml** à la racine de hello de votre application et ajoutez hello ligne suivante.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment io.js toouse avec les applications Web App Service, à l’aide fournie scripts de déploiement, ainsi que l’installation manuelle. 

> [!NOTE]
> io.js fait l'objet d'un développement intense et est plus souvent mis à jour que Node.js. Il est possible qu’un certain nombre de modules Node.js ne fonctionnent pas avec io.js. Consultez la rubrique consacrée à [io.js sur GitHub] pour résoudre les problèmes éventuels.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

[io.js]: https://iojs.org
[io.js distribution]: https://iojs.org/dist/
[io.js sur GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
