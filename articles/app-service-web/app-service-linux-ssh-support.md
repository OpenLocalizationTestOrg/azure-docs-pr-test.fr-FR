---
title: "Prise en charge SSH pour l’application web Azure App Service sur Linux | Microsoft Docs"
description: "Apprenez à utiliser SSH avec Azure Web App sur Linux."
keywords: azure app service, application web, linux, oss
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: feee7a5c91d213a6b0bfdaf264a4da4d9e79cbe7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Prise en charge SSH pour Azure Web App sur Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Vue d'ensemble

[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) est un protocole réseau de chiffrement qui permet d’utiliser les services réseau en toute sécurité. Il est couramment utilisé pour se connecter au système à distance de façon sécurisée à partir d’une ligne de commande et exécuter des commandes administratives à distance.

L’application web sur Linux assure la prise en charge SSH dans le conteneur d’application avec chacune des images Docker intégrées utilisées pour la pile d’exécution des nouvelles applications web. 

![Piles d’exécution](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

Vous pouvez également utiliser SSH avec vos images Docker personnalisées en incluant le serveur SSH dans le cadre de l’image et en le configurant comme indiqué dans cette rubrique.



## <a name="making-a-client-connection"></a>Établissement d’une connexion avec un client

Pour établir une connexion avec un client SSH, le site principal doit être démarré. 

Collez le point de terminaison de gestion de contrôle de code source de votre application web dans votre navigateur sous la forme suivante :

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Si vous n’êtes pas déjà authentifié, vous devez le faire à l’aide de votre abonnement Azure pour vous connecter.

![Connexion SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Prise en charge SSH avec des images Docker personnalisées

Pour qu’une image Docker personnalisée prenne en charge la communication entre le conteneur et le client dans le portail Azure, procédez comme suit pour votre image Docker. 

Cette procédure est affichée dans le référentiel Azure App Service en tant qu’exemple [ici](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Incluez l’installation `openssh-server` dans [l’instruction `RUN`](https://docs.docker.com/engine/reference/builder/#run) au sein du fichier Dockerfile de votre image et définissez le mot de passe du compte racine sur `"Docker!"`. 

    > [!NOTE] 
    > Cette configuration n’autorise pas les connexions externes avec le conteneur. SSH est accessible uniquement via le site Kudu/SCM, authentifié à l’aide des informations d’identification de publication.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Ajoutez une [instruction `COPY`](https://docs.docker.com/engine/reference/builder/#copy) au fichier Dockerfile pour copier un fichier [sshd_config](http://man.openbsd.org/sshd_config) dans le répertoire */etc/ssh/*. Votre fichier de configuration doit être basé sur notre fichier sshd_config dans le référentiel GitHub Azure-App-Service [ici](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > Le fichier *sshd_config* doit inclure les éléments suivants pour éviter que la connexion échoue : 
    > * `Ciphers` doit inclure au moins un des éléments suivants : `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs` doit inclure au moins un des éléments suivants : `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Incluez le port 2222 dans [l’instruction `EXPOSE`](https://docs.docker.com/engine/reference/builder/#expose) pour le fichier Dockerfile. Bien que le mot de passe racine soit connu, le port 2222 n’est pas accessible à partir d’Internet. Il s’agit seulement d’un port interne accessible uniquement par les conteneurs au sein du réseau de pont d’un réseau privé virtuel.

    ```docker
    EXPOSE 2222 80
    ```

4. Veillez à démarrer le service ssh. L’exemple [ici](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) utilise un script shell dans le répertoire */bin*.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Le fichier Dockerfile utilise le [l’instruction `CMD`](https://docs.docker.com/engine/reference/builder/#cmd) pour exécuter le script.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’application web sur Linux, consultez les liens suivants. Vous pouvez poser des questions et signaler vos préoccupations sur [notre forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Comment utiliser une image Docker personnalisé pour Azure Web App sur Linux](app-service-linux-using-custom-docker-image.md)
* [Utiliser la configuration PM2 pour Node.js dans Azure Web App sur Linux](app-service-linux-using-nodejs-pm2.md)
* [Utilisation de .NET Core dans l’application web Azure sur Linux](app-service-linux-using-dotnetcore.md)
* [Utilisation de Ruby dans l’application web Azure sur Linux](app-service-linux-ruby-get-started.md)
* [FAQ de l’application web Azure App Service sur Linux](app-service-linux-faq.md)

