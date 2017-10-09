---
title: configuration aaaUsing PM2 pour Node.js dans Azure Web App sur Linux | Documents Microsoft
description: "Utilisation de la configuration PM2 pour Node.js dans l’application web Azure sur Linux"
keywords: azure app service, application web, nodejs, pm2, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a>Utiliser la configuration PM2 pour Node.js dans l’application web Azure sur Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Si vous définissez tooNode.js de pile application hello pour l’application Web Azure sous Linux, vous obtenez hello option tooset un fichier de démarrage Node.js comme indiqué dans hello suivant l’image :

![Définir un fichier de démarrage Node.js][1]

Vous pouvez utiliser cette option toodo une Hello tâches suivantes :

* Spécifier le script de démarrage hello pour votre application Node.js (par exemple : /bin/server.js).
* Spécifiez toouse de fichier de configuration hello PM2 pour votre application Node.js (par exemple : /foo/process.json).
  
  > [!NOTE]
  > Si vous souhaitez que votre toorestart de processus Node.js automatiquement lorsque certains fichiers sont modifiées, utilisez la configuration de PM2 hello. Sinon, votre application ne redémarrera pas lorsqu’elle recevra des notifications de modification (par exemple, en cas de modification du code de votre application).
  > 
  > 

Vous pouvez vérifier hello Node.js [traiter la documentation du fichier](http://pm2.keymetrics.io/docs/usage/application-declaration/) pour tous les hello options, mais voici un exemple de ce que vous pouvez utiliser en tant que votre fichier process.json :

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

Toonote points importants dans cette configuration sont les suivantes :

* propriété de « script » Hello Spécifie le script de démarrage de votre application.
* propriété « instances » de Hello Spécifie le nombre d’instances de hello nœud processus toolaunch. Si vous exécutez votre application sur des machines virtuelles plus grandes plusieurs cœurs, il est une bonne idée toomaximize vos ressources en définissant une valeur plus élevée ici.
* Hello « espion » tableau spécifie tous les fichiers de processus de nœud toorestart hello pour quand ils changent.
* Pourquoi « watch_options », vous devez actuellement toospecify « usePolling » en tant que la valeur true en raison de façon hello que votre contenu de l’application est monté.

## <a name="next-steps"></a>Étapes suivantes
* [Qu’est-ce que l’application web Azure sur Linux ?](app-service-linux-intro.md)
* [FAQ Application web Azure App Service sur Linux](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
