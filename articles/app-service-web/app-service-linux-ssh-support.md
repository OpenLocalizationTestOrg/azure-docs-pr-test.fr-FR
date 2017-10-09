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
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="50e69-104">Prise en charge SSH pour Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="50e69-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="50e69-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="50e69-105">Overview</span></span>

<span data-ttu-id="50e69-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) est un protocole réseau de chiffrement qui permet d’utiliser les services réseau en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="50e69-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="50e69-107">Il est toolog couramment utilisée dans un système à distance en toute sécurité à partir d’une ligne de commande et exécuter des commandes d’administration à distance.</span><span class="sxs-lookup"><span data-stu-id="50e69-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="50e69-108">Web application sur Linux prend en charge SSH dans le conteneur d’application hello avec chacune des images Docker intégrées hello utilisés pour hello pile de Runtime de nouvelles applications web.</span><span class="sxs-lookup"><span data-stu-id="50e69-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![Piles d’exécution](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="50e69-110">Vous pouvez également utiliser SSH avec vos images Docker personnalisées, y compris le serveur SSH hello dans le cadre de l’image de hello en configurant comme décrit dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="50e69-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="50e69-111">Établissement d’une connexion avec un client</span><span class="sxs-lookup"><span data-stu-id="50e69-111">Making a client connection</span></span>

<span data-ttu-id="50e69-112">toomake une connexion client SSH, site principal de hello doit être démarré.</span><span class="sxs-lookup"><span data-stu-id="50e69-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="50e69-113">Collez le point de terminaison de gestion de contrôle de code Source (SCM) hello pour votre application web dans votre navigateur à l’aide de hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="50e69-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="50e69-114">Si vous n’êtes pas authentifié, vous êtes tooauthenticate requis tooconnect de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="50e69-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![Connexion SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="50e69-116">Prise en charge SSH avec des images Docker personnalisées</span><span class="sxs-lookup"><span data-stu-id="50e69-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="50e69-117">Dans l’ordre pour personnalisé Docker image toosupport SSH communication entre le conteneur de hello et client hello Bonjour portail Azure, effectuez hello comme suit pour votre image Docker.</span><span class="sxs-lookup"><span data-stu-id="50e69-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="50e69-118">Ces étapes sont figurent dans hello référentiel du Service d’applications Azure comme exemple [ici](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="50e69-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="50e69-119">Inclure hello `openssh-server` installation dans [ `RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) hello Dockerfile de votre image et définir un mot de passe hello pour le compte de racine hello trop`"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="50e69-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="50e69-120">Cette configuration n’autorise pas le conteneur toohello de connexions externes.</span><span class="sxs-lookup"><span data-stu-id="50e69-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="50e69-121">SSH est accessible uniquement via hello Kudu / SCM Site, qui est authentifié à l’aide de hello des informations d’identification de publication.</span><span class="sxs-lookup"><span data-stu-id="50e69-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="50e69-122">Ajouter un [ `COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy un [sshd_config](http://man.openbsd.org/sshd_config) toohello de fichiers */etc/ssh/* active.</span><span class="sxs-lookup"><span data-stu-id="50e69-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="50e69-123">Votre fichier de configuration doit être basé sur notre fichier sshd_config dans le référentiel GitHub de Service d’applications Azure de hello [ici](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="50e69-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="50e69-124">Hello *sshd_config* fichier doit hello suivants ou hello connexion échoue :</span><span class="sxs-lookup"><span data-stu-id="50e69-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="50e69-125">`Ciphers`doit inclure au moins un des éléments suivants de hello : `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="50e69-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="50e69-126">`MACs`doit inclure au moins un des éléments suivants de hello : `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="50e69-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="50e69-127">Inclure le port 2222 Bonjour [ `EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) pour hello Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="50e69-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="50e69-128">Bien que le mot de passe racine hello est connu, le port 2222 ne sont pas accessibles à partir de hello internet.</span><span class="sxs-lookup"><span data-stu-id="50e69-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="50e69-129">Il s’agit d’un port uniquement interne accessible uniquement par les conteneurs au sein du réseau de pont hello d’un réseau virtuel privé.</span><span class="sxs-lookup"><span data-stu-id="50e69-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="50e69-130">Assurez-vous que toostart hello ssh de service.</span><span class="sxs-lookup"><span data-stu-id="50e69-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="50e69-131">exemple de Hello [ici](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) utilise un script shell dans */bin* active.</span><span class="sxs-lookup"><span data-stu-id="50e69-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="50e69-132">Hello Dockerfile utilise hello [ `CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) script de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="50e69-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="50e69-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50e69-133">Next steps</span></span>
<span data-ttu-id="50e69-134">Consultez hello suivant les liens pour plus d’informations sur l’application Web sur Linux.</span><span class="sxs-lookup"><span data-stu-id="50e69-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="50e69-135">Vous pouvez poser des questions et signaler vos préoccupations sur [notre forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="50e69-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="50e69-136">Comment toouse une Docker personnalisée de l’image pour l’application Web de Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="50e69-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="50e69-137">Utilisation de la configuration PM2 pour Node.js dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="50e69-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="50e69-138">Utilisation de .NET Core dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="50e69-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="50e69-139">Utilisation de Ruby dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="50e69-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="50e69-140">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="50e69-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

