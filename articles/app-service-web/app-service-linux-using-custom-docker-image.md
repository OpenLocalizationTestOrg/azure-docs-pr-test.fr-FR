---
title: "aaaHow toouse une image Docker personnalisée pour l’application Web Azure sous Linux | Documents Microsoft"
description: "Comment toouse une Docker personnalisée de l’image pour l’application Web de Azure sur Linux."
keywords: azure app service, application web, linux, docker, conteneur
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


App Service fournit des piles d’applications prédéfinies sur Linux avec la prise en charge de versions spécifiques, comme PHP 7.0 et Node.js 4.5. Service d’applications sur Linux utilise des conteneurs Docker toohost ces intégrées dans les piles d’application. Vous pouvez également utiliser un toodeploy d’image Docker personnalisé à votre pile l’application web application tooan qui n’est pas déjà défini dans Azure. Les images Docker personnalisées peuvent être hébergées sur un référentiel Docker public ou privé.


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>Comment : définir une image Docker personnalisée pour une application web
Vous pouvez définir hello Docker image personnalisée pour les nouvelles et les applications Web existantes. Lorsque vous créez une application web sur Linux Bonjour [portail Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), cliquez sur **configurer conteneur** tooset une image Docker personnalisée :

![Image Docker personnalisée pour une nouvelle application web sur Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>Comment : utiliser une image Docker personnalisée à partir de Docker Hub ##
toouse une image personnalisée de Docker à partir du Hub d’ancrage :

1. Bonjour [portail Azure](https://portal.azure.com), localisez votre application web sur Linux, puis dans **paramètres** cliquez sur **conteneur Docker**.

2.  Sélectionnez **Hub Docker** comme hello **source de l’Image**, puis cliquez sur **Public** ou **privé** et type Bonjour **Image et nom de la balise facultatif**, tel que `node:4.5`. Hello **commande de démarrage** est jeu automatiquement selon ce qui est défini dans le fichier d’image hello Docker, mais vous pouvez définir vos propres commandes.  

    ![Configuration de l’image de référentiel public Docker Hub][2]

    Lorsque votre image est d’un référentiel privé, vous devez également les informations d’identification du Hub d’ancrage tooenter hello comme (**nom d’utilisateur** et **mot de passe**) pour le référentiel de Hub d’ancrage hello privé.

    ![Configuration de l’image de référentiel public Docker Hub][3]

3. Une fois que vous avez configuré le conteneur de hello, cliquez sur **enregistrer**.

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a>Comment toouse une Docker de l’image à partir d’un Registre de l’image privée ##
toouse une image personnalisée de Docker à partir d’un Registre de l’image privée :

1. Bonjour [portail Azure](https://portal.azure.com), localisez votre application web sur Linux, puis dans **paramètres** cliquez sur **conteneur Docker**.

2.  Cliquez sur **Registre privé** comme hello **source de l’Image**. Entrez hello **Image et le nom de la balise facultatif**, **URL du serveur** Registre privé hello, ainsi que des informations d’identification hello (**nom d’utilisateur** et **mot de passe** ). Cliquez sur **Enregistrer**.

    ![Configuration de l’image Docker à partir du registre privé][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a>Comment : définir le port hello utilisé par votre image de Docker ##

Lorsque vous utilisez une image Docker personnalisée pour votre application web, vous pouvez utiliser hello `WEBSITES_PORT` variable d’environnement dans votre fichier Dockerfile, qui est également ajouté toohello généré conteneur. Tenez compte des hello exemple d’un fichier de docker pour une application Ruby suivant :

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

Sur la dernière ligne de commande hello, vous pouvez voir que cette variable d’environnement WEBSITES_PORT hello est passée de l’exécution. N’oubliez pas les commandes sont sensibles à la casse.

Précédemment a été à l’aide de la plateforme de hello `PORT` application définissant, nous planifiez toodeprecate hello utiliser cette application définissant et déplacer toousing `WEBSITES_PORT` exclusivement.

Lorsque vous utilisez une image Docker existante créée par quelqu'un d’autre, vous devrez peut-être toospecify un port autre que le port 80 pour l’application hello. tooconfigure hello port, ajoutez une paramètre d’application nommé `WEBSITES_PORT` avec la valeur hello comme indiqué ci-dessous :

![Configuration du paramètre d’application PORT pour une image Docker personnalisée][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a>Comment : définir l’heure de démarrage de hello pour votre image de Docker ##

Par défaut, si votre conteneur ne démarre pas avant 230 secondes, plateforme de hello redémarrera votre conteneur. Si votre image personnalisée de Docker démarre en plus de 230 secondes, vous pouvez utiliser hello `WEBSITES_CONTAINER_START_TIME_LIMIT` application paramètre, valeur hello pour ce paramètre est exprimé en secondes, cela permettra hello plateforme conserver votre conteneur en cours d’exécution avant de le redémarrer. Hello par défaut est secondes 230 et hello maximum valeur est de 600 secondes.

## <a name="how-to-unmount-hello-platform-provided-storage"></a>Comment : décharger le stockage de la plateforme fourni hello ##

Par défaut, la plateforme de hello monte un toohello de partage du stockage persistant `\home\` active. Si votre image de conteneur ne doit pas un partage persistant, vous pouvez désactiver le montage que le stockage en définissant un hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` application aussi un paramètre`false`. Vous aurez toujours accès toothat stockage à partir du site de scm hello et tous les journaux de Docker (si activé) seront écrit les fichiers de journaux toohello générés par la plateforme de hello.

## <a name="how-to-switch-back-toousing-a-built-in-image"></a>Comment : Revenez toousing une image intégrée ##

tooswitch d’utiliser une image personnalisée de toousing une image intégrée :

1. Bonjour [portail Azure](https://portal.azure.com), localisez votre application web sur Linux, puis dans **paramètres** cliquez sur **du Service d’applications**.

2. Sélectionnez votre **pile de Runtime** toouse pour l’image intégrée de hello, puis cliquez sur **enregistrer**. 

![Configuration de l’image Docker intégrée][5]


## <a name="troubleshooting"></a>Résolution des problèmes ##

Lorsque votre application échoue toostart avec votre image personnalisée de Docker, vérifiez hello que docker enregistre dans le répertoire des fichiers journaux hello. Vous pouvez accéder à ce répertoire par le biais de votre site SCM ou d’un FTP.
toolog hello `stdout` et `stderr` à partir de votre conteneur, vous devez tooenable **journalisation du conteneur Docker** sous **les journaux de diagnostic**.

![Activation de la journalisation][8]

![Utilisation des journaux de Kudu tooview Docker][7]

Vous pouvez accéder à site SCM hello **outils avancés** Bonjour **outils de développement** menu.

## <a name="next-steps"></a>Étapes suivantes ##

Suivez hello suivant tooget liens en main de l’application Web sur Linux.   

* [Introduction tooAzure application Web sur Linux](./app-service-linux-intro.md)
* [Utilisation de la configuration PM2 pour Node.js dans l’application web Azure sur Linux](./app-service-linux-using-nodejs-pm2.md)
* [FAQ de l’application web Azure App Service sur Linux](app-service-linux-faq.md)

Posez des questions et indiquez vos préoccupations sur [notre forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
