---
title: aaaSpecifying une Version de Node.js
description: "Découvrez comment toospecify hello version de Node.js utilisé par les Sites Web Azure et les Services de Cloud"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>Spécification d'une version Node.js dans une application Azure
Lorsque vous hébergez une application Node.js, vous souhaiterez peut-être tooensure que votre application utilise une version spécifique de Node.js. Il existe plusieurs façons tooaccomplish cela pour les applications hébergées sur Azure.

## <a name="default-versions"></a>Versions par défaut
Hello Node.js versions fournies par Azure sont constamment mises à jour. Sauf indication contraire, hello version par défaut qui est spécifiée dans hello `WEBSITE_NODE_DEFAULT_VERSION` variable d’environnement sera utilisée. toooverride cette valeur par défaut, suivez les étapes hello dans les sections suivantes de cet article

> [!NOTE]
> Si vous hébergez votre application dans un Service de Cloud Azure (rôle web ou de travail), et il est hello la première fois que vous avez déployé application hello, Azure tentera toouse hello la même version de Node.js que vous avez installé sur votre environnement de développement si il correspond à une des versions par défaut de hello disponibles sur Azure.
>
>

## <a name="versioning-with-packagejson"></a>Contrôle de version avec package.json
Vous pouvez spécifier la version de hello de toobe Node.js utilisée en ajoutant hello suivant tooyour **package.json** fichier :

    "engines":{"node":version}

Où *version* est toouse numéro de version spécifique de hello. Vous pouvez spécifier des conditions plus complexes, telles que :

    "engines":{"node": "0.6.22 || 0.8.x"}

Étant donné que 0.6.22 n’est pas une des versions hello disponibles dans l’environnement d’hébergement de hello, hello version la plus récente de hello 0,8 série disponible sera utilisé à la place - 0.8.4.

## <a name="versioning-websites-with-app-settings"></a>Contrôle de version des sites web avec les paramètres d'application
Si vous hébergez une application hello dans un site Web, vous pouvez définir la variable d’environnement hello **WEBSITE_NODE_DEFAULT_VERSION** toohello les version souhaitée.

## <a name="versioning-cloud-services-with-powershell"></a>Contrôle de version des services cloud avec PowerShell
Si vous hébergez l’application hello dans un Service Cloud et que vous déployez application hello à l’aide d’Azure PowerShell, vous pouvez remplacer la version de Node.js hello par défaut à l’aide de hello **Set-AzureServiceProjectRole** applet de commande PowerShell. Par exemple :

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

Paramètres de hello Bonjour ci-dessus instruction respectent la casse.  Vous pouvez vérifier la version correcte de hello de Node.js a été sélectionnée en vérifiant hello **moteurs** propriété de votre rôle **package.json**.

Vous pouvez également utiliser hello **Get-AzureServiceProjectRoleRuntime** tooretrieve une liste des versions de Node.js disponibles pour les applications hébergées en tant qu’un Service Cloud.  Vérifiez toujours la version hello de Node.js dépend de votre projet est dans cette liste.

## <a name="using-a-custom-version-with-azure-websites"></a>Utilisation d'une version personnalisée avec Azure Websites
Azure fournit plusieurs versions par défaut de Node.js, vous souhaiterez toouse une version qui n’est pas fournie par défaut. Si votre application est hébergée comme un site Web Azure, vous pouvez le faire à l’aide de hello **iisnode.yml** fichier. Hello suit Guide hello processus d’à l’aide d’une version personnalisée de Node.Js avec un site Web Azure :

1. Créer un nouveau répertoire et créez ensuite un **server.js** fichier dans le répertoire de hello. Hello **server.js** fichier doit contenir les éléments suivants de hello :

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    Cette action affiche la version de Node.js hello utilisée lorsque vous parcourez le site Web de hello.
2. Créer un nouveau site Web et le nom de la note hello du site de hello. Par exemple, suivant de hello utilise hello [des outils de ligne de commande Azure] toocreate un site Web Azure nommé **monsiteweb**et que vous activez un référentiel Git pour le site Web de hello.

        azure site create mywebsite --git
3. Créer un nouveau répertoire nommé **bin** en tant qu’enfant du répertoire hello contenant hello **server.js** fichier.
4. Télécharger une version spécifique de hello **node.exe** (version de Windows hello) que vous souhaitez toouse avec votre application. Par exemple, hello suivant utilise **curl** version de toodownload 0.8.1 :

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    Enregistrer hello **node.exe** fichier hello **bin** dossier créé précédemment.
5. Créer un **iisnode.yml** fichier Bonjour même répertoire que hello **server.js** et puis ajoutez hello suivant toohello contenu **iisnode.yml** fichier :

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    Ce chemin d’accès est où hello **node.exe** fichier au sein de votre projet se trouve une fois que vous avez publié votre application de toohello site Web Azure.
6. Publiez votre application. Par exemple, étant donné que j’ai créé un nouveau site Web avec le paramètre hello--git précédemment, hello commandes suivantes seront ajoutez hello application fichiers toomy référentiel Git et les transmettre de référentiel de site Web toohello :

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    Après la publication de l’application hello, ouvrez le site Web de hello dans un navigateur. Le message suivant doit apparaître : « Hello from Azure running node version: v0.8.1 ».

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous comprenez comment la version de hello toospecify de Node.js utilisées par votre application, découvrez comment trop[fonctionnent avec les modules], [générer et déployer un Site Web de Node.js](app-service-web/app-service-web-get-started-nodejs.md), et [comment toouse hello Azure Outils de ligne de commande pour Mac et Linux].

Pour plus d’informations, consultez hello [centre de développement Node.js](https://azure.microsoft.com/develop/nodejs/).

[comment toouse hello Azure Outils de ligne de commande pour Mac et Linux]:cli-install-nodejs.md
[des outils de ligne de commande Azure]:cli-install-nodejs.md
[fonctionnent avec les modules]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
