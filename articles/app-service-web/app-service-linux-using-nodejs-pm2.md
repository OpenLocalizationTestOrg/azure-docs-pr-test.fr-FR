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
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="6ff1f-104">Utiliser la configuration PM2 pour Node.js dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="6ff1f-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="6ff1f-105">Si vous définissez tooNode.js de pile application hello pour l’application Web Azure sous Linux, vous obtenez hello option tooset un fichier de démarrage Node.js comme indiqué dans hello suivant l’image :</span><span class="sxs-lookup"><span data-stu-id="6ff1f-105">If you set hello application stack tooNode.js for Azure Web App on Linux, you get hello option tooset a Node.js startup file as shown in hello following image:</span></span>

![Définir un fichier de démarrage Node.js][1]

<span data-ttu-id="6ff1f-107">Vous pouvez utiliser cette option toodo une Hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="6ff1f-107">You can use this option toodo one of hello following tasks:</span></span>

* <span data-ttu-id="6ff1f-108">Spécifier le script de démarrage hello pour votre application Node.js (par exemple : /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="6ff1f-108">Specify hello startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="6ff1f-109">Spécifiez toouse de fichier de configuration hello PM2 pour votre application Node.js (par exemple : /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="6ff1f-109">Specify hello PM2 configuration file toouse for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6ff1f-110">Si vous souhaitez que votre toorestart de processus Node.js automatiquement lorsque certains fichiers sont modifiées, utilisez la configuration de PM2 hello.</span><span class="sxs-lookup"><span data-stu-id="6ff1f-110">If you want your Node.js processes toorestart automatically when certain files are modified, use hello PM2 configuration.</span></span> <span data-ttu-id="6ff1f-111">Sinon, votre application ne redémarrera pas lorsqu’elle recevra des notifications de modification (par exemple, en cas de modification du code de votre application).</span><span class="sxs-lookup"><span data-stu-id="6ff1f-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="6ff1f-112">Vous pouvez vérifier hello Node.js [traiter la documentation du fichier](http://pm2.keymetrics.io/docs/usage/application-declaration/) pour tous les hello options, mais voici un exemple de ce que vous pouvez utiliser en tant que votre fichier process.json :</span><span class="sxs-lookup"><span data-stu-id="6ff1f-112">You can check hello Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all hello options, but following is a sample of what you can use as your process.json file:</span></span>

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

<span data-ttu-id="6ff1f-113">Toonote points importants dans cette configuration sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6ff1f-113">Important things toonote in this configuration are:</span></span>

* <span data-ttu-id="6ff1f-114">propriété de « script » Hello Spécifie le script de démarrage de votre application.</span><span class="sxs-lookup"><span data-stu-id="6ff1f-114">hello "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="6ff1f-115">propriété « instances » de Hello Spécifie le nombre d’instances de hello nœud processus toolaunch.</span><span class="sxs-lookup"><span data-stu-id="6ff1f-115">hello "instances" property specifies how many instances of hello node process toolaunch.</span></span> <span data-ttu-id="6ff1f-116">Si vous exécutez votre application sur des machines virtuelles plus grandes plusieurs cœurs, il est une bonne idée toomaximize vos ressources en définissant une valeur plus élevée ici.</span><span class="sxs-lookup"><span data-stu-id="6ff1f-116">If you are running your application on larger VMs that have multiple cores, it's a good idea toomaximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="6ff1f-117">Hello « espion » tableau spécifie tous les fichiers de processus de nœud toorestart hello pour quand ils changent.</span><span class="sxs-lookup"><span data-stu-id="6ff1f-117">hello "watch" array specifies all files that you want toorestart hello node process for when they change.</span></span>
* <span data-ttu-id="6ff1f-118">Pourquoi « watch_options », vous devez actuellement toospecify « usePolling » en tant que la valeur true en raison de façon hello que votre contenu de l’application est monté.</span><span class="sxs-lookup"><span data-stu-id="6ff1f-118">For hello "watch_options", you currently need toospecify "usePolling" as true because of hello way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ff1f-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6ff1f-119">Next steps</span></span>
* [<span data-ttu-id="6ff1f-120">Qu’est-ce que l’application web Azure sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="6ff1f-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="6ff1f-121">FAQ Application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="6ff1f-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
