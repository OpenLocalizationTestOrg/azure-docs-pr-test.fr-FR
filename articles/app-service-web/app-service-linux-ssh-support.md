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
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="d7cef-104">Prise en charge SSH pour Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="d7cef-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="d7cef-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d7cef-105">Overview</span></span>

<span data-ttu-id="d7cef-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) est un protocole réseau de chiffrement qui permet d’utiliser les services réseau en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="d7cef-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="d7cef-107">Il est couramment utilisé pour se connecter au système à distance de façon sécurisée à partir d’une ligne de commande et exécuter des commandes administratives à distance.</span><span class="sxs-lookup"><span data-stu-id="d7cef-107">It is most commonly used to log into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="d7cef-108">L’application web sur Linux assure la prise en charge SSH dans le conteneur d’application avec chacune des images Docker intégrées utilisées pour la pile d’exécution des nouvelles applications web.</span><span class="sxs-lookup"><span data-stu-id="d7cef-108">Web App on Linux provides SSH support into the app container with each of the built-in Docker images used for the Runtime Stack of new web apps.</span></span> 

![Piles d’exécution](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="d7cef-110">Vous pouvez également utiliser SSH avec vos images Docker personnalisées en incluant le serveur SSH dans le cadre de l’image et en le configurant comme indiqué dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="d7cef-110">You can also use SSH with your custom Docker images by including the SSH server as part of the image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="d7cef-111">Établissement d’une connexion avec un client</span><span class="sxs-lookup"><span data-stu-id="d7cef-111">Making a client connection</span></span>

<span data-ttu-id="d7cef-112">Pour établir une connexion avec un client SSH, le site principal doit être démarré.</span><span class="sxs-lookup"><span data-stu-id="d7cef-112">To make an SSH client connection, the main site must be started.</span></span> 

<span data-ttu-id="d7cef-113">Collez le point de terminaison de gestion de contrôle de code source de votre application web dans votre navigateur sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="d7cef-113">Paste the Source Control Management (SCM) endpoint for your web app into your browser using the following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="d7cef-114">Si vous n’êtes pas déjà authentifié, vous devez le faire à l’aide de votre abonnement Azure pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="d7cef-114">If you are not already authenticated, you are required to authenticate with your Azure subscription to connect.</span></span>

![Connexion SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="d7cef-116">Prise en charge SSH avec des images Docker personnalisées</span><span class="sxs-lookup"><span data-stu-id="d7cef-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="d7cef-117">Pour qu’une image Docker personnalisée prenne en charge la communication entre le conteneur et le client dans le portail Azure, procédez comme suit pour votre image Docker.</span><span class="sxs-lookup"><span data-stu-id="d7cef-117">In order for a custom Docker image to support SSH communication between the container and the client in the Azure portal, perform the following steps for your Docker image.</span></span> 

<span data-ttu-id="d7cef-118">Cette procédure est affichée dans le référentiel Azure App Service en tant qu’exemple [ici](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="d7cef-118">These steps are are shown in the Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="d7cef-119">Incluez l’installation `openssh-server` dans [l’instruction `RUN`](https://docs.docker.com/engine/reference/builder/#run) au sein du fichier Dockerfile de votre image et définissez le mot de passe du compte racine sur `"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="d7cef-119">Include the `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in the Dockerfile for your image and set the password for the root account to `"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="d7cef-120">Cette configuration n’autorise pas les connexions externes avec le conteneur.</span><span class="sxs-lookup"><span data-stu-id="d7cef-120">This configuration does not allow external connections to the container.</span></span> <span data-ttu-id="d7cef-121">SSH est accessible uniquement via le site Kudu/SCM, authentifié à l’aide des informations d’identification de publication.</span><span class="sxs-lookup"><span data-stu-id="d7cef-121">SSH can only be accessed via the Kudu / SCM Site, which is authenticated using the publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="d7cef-122">Ajoutez une [instruction `COPY`](https://docs.docker.com/engine/reference/builder/#copy) au fichier Dockerfile pour copier un fichier [sshd_config](http://man.openbsd.org/sshd_config) dans le répertoire */etc/ssh/*.</span><span class="sxs-lookup"><span data-stu-id="d7cef-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) to the Dockerfile to copy a [sshd_config](http://man.openbsd.org/sshd_config) file to the */etc/ssh/* directory.</span></span> <span data-ttu-id="d7cef-123">Votre fichier de configuration doit être basé sur notre fichier sshd_config dans le référentiel GitHub Azure-App-Service [ici](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="d7cef-123">Your configuration file should be based on our sshd_config file in the Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d7cef-124">Le fichier *sshd_config* doit inclure les éléments suivants pour éviter que la connexion échoue :</span><span class="sxs-lookup"><span data-stu-id="d7cef-124">The *sshd_config* file must include the following or the connection fails:</span></span> 
    > * <span data-ttu-id="d7cef-125">`Ciphers` doit inclure au moins un des éléments suivants : `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="d7cef-125">`Ciphers` must include at least one of the following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="d7cef-126">`MACs` doit inclure au moins un des éléments suivants : `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="d7cef-126">`MACs` must include at least one of the following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="d7cef-127">Incluez le port 2222 dans [l’instruction `EXPOSE`](https://docs.docker.com/engine/reference/builder/#expose) pour le fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="d7cef-127">Include port 2222 in the [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for the Dockerfile.</span></span> <span data-ttu-id="d7cef-128">Bien que le mot de passe racine soit connu, le port 2222 n’est pas accessible à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="d7cef-128">Although the root password is known, port 2222 cannot be accessed from the internet.</span></span> <span data-ttu-id="d7cef-129">Il s’agit seulement d’un port interne accessible uniquement par les conteneurs au sein du réseau de pont d’un réseau privé virtuel.</span><span class="sxs-lookup"><span data-stu-id="d7cef-129">It is an internal only port accessible only by containers within the bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="d7cef-130">Veillez à démarrer le service ssh.</span><span class="sxs-lookup"><span data-stu-id="d7cef-130">Make sure to start the ssh service.</span></span> <span data-ttu-id="d7cef-131">L’exemple [ici](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) utilise un script shell dans le répertoire */bin*.</span><span class="sxs-lookup"><span data-stu-id="d7cef-131">The example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="d7cef-132">Le fichier Dockerfile utilise le [l’instruction `CMD`](https://docs.docker.com/engine/reference/builder/#cmd) pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="d7cef-132">The Dockerfile uses the [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) to run the script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="d7cef-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7cef-133">Next steps</span></span>
<span data-ttu-id="d7cef-134">Pour plus d’informations sur l’application web sur Linux, consultez les liens suivants.</span><span class="sxs-lookup"><span data-stu-id="d7cef-134">See the following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="d7cef-135">Vous pouvez poser des questions et signaler vos préoccupations sur [notre forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="d7cef-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="d7cef-136">Comment utiliser une image Docker personnalisé pour Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="d7cef-136">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="d7cef-137">Utiliser la configuration PM2 pour Node.js dans Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="d7cef-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="d7cef-138">Utilisation de .NET Core dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="d7cef-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="d7cef-139">Utilisation de Ruby dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="d7cef-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="d7cef-140">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="d7cef-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

