---
title: "prise en charge d’aaaSSH pour Azure App Service Web App sur Linux | Documents Microsoft"
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
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Prise en charge SSH pour Azure Web App sur Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Vue d'ensemble

[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) est un protocole réseau de chiffrement qui permet d’utiliser les services réseau en toute sécurité. Il est toolog couramment utilisée dans un système à distance en toute sécurité à partir d’une ligne de commande et exécuter des commandes d’administration à distance.

Web application sur Linux prend en charge SSH dans le conteneur d’application hello avec chacune des images Docker intégrées hello utilisés pour hello pile de Runtime de nouvelles applications web. 

![Piles d’exécution](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

Vous pouvez également utiliser SSH avec vos images Docker personnalisées, y compris le serveur SSH hello dans le cadre de l’image de hello en configurant comme décrit dans cette rubrique.



## <a name="making-a-client-connection"></a>Établissement d’une connexion avec un client

toomake une connexion client SSH, site principal de hello doit être démarré. 

Collez le point de terminaison de gestion de contrôle de code Source (SCM) hello pour votre application web dans votre navigateur à l’aide de hello suivant du formulaire :

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Si vous n’êtes pas authentifié, vous êtes tooauthenticate requis tooconnect de votre abonnement Azure.

![Connexion SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Prise en charge SSH avec des images Docker personnalisées

Dans l’ordre pour personnalisé Docker image toosupport SSH communication entre le conteneur de hello et client hello Bonjour portail Azure, effectuez hello comme suit pour votre image Docker. 

Ces étapes sont figurent dans hello référentiel du Service d’applications Azure comme exemple [ici](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Inclure hello `openssh-server` installation dans [ `RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) hello Dockerfile de votre image et définir un mot de passe hello pour le compte de racine hello trop`"Docker!"`. 

    > [!NOTE] 
    > Cette configuration n’autorise pas le conteneur toohello de connexions externes. SSH est accessible uniquement via hello Kudu / SCM Site, qui est authentifié à l’aide de hello des informations d’identification de publication.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Ajouter un [ `COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy un [sshd_config](http://man.openbsd.org/sshd_config) toohello de fichiers */etc/ssh/* active. Votre fichier de configuration doit être basé sur notre fichier sshd_config dans le référentiel GitHub de Service d’applications Azure de hello [ici](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > Hello *sshd_config* fichier doit hello suivants ou hello connexion échoue : 
    > * `Ciphers`doit inclure au moins un des éléments suivants de hello : `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs`doit inclure au moins un des éléments suivants de hello : `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Inclure le port 2222 Bonjour [ `EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) pour hello Dockerfile. Bien que le mot de passe racine hello est connu, le port 2222 ne sont pas accessibles à partir de hello internet. Il s’agit d’un port uniquement interne accessible uniquement par les conteneurs au sein du réseau de pont hello d’un réseau virtuel privé.

    ```docker
    EXPOSE 2222 80
    ```

4. Assurez-vous que toostart hello ssh de service. exemple de Hello [ici](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) utilise un script shell dans */bin* active.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Hello Dockerfile utilise hello [ `CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) script de hello toorun.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Étapes suivantes
Consultez hello suivant les liens pour plus d’informations sur l’application Web sur Linux. Vous pouvez poser des questions et signaler vos préoccupations sur [notre forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Comment toouse une Docker personnalisée de l’image pour l’application Web de Azure sur Linux](app-service-linux-using-custom-docker-image.md)
* [Utilisation de la configuration PM2 pour Node.js dans l’application web Azure sur Linux](app-service-linux-using-nodejs-pm2.md)
* [Utilisation de .NET Core dans l’application web Azure sur Linux](app-service-linux-using-dotnetcore.md)
* [Utilisation de Ruby dans l’application web Azure sur Linux](app-service-linux-ruby-get-started.md)
* [FAQ de l’application web Azure App Service sur Linux](app-service-linux-faq.md)

