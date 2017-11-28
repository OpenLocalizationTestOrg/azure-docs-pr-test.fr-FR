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
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="2f50e-104">Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="2f50e-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="2f50e-105">App Service fournit des piles d’applications prédéfinies sur Linux avec la prise en charge de versions spécifiques, comme PHP 7.0 et Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="2f50e-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="2f50e-106">Service d’applications sur Linux utilise des conteneurs Docker toohost ces intégrées dans les piles d’application.</span><span class="sxs-lookup"><span data-stu-id="2f50e-106">App Service on Linux uses Docker containers toohost these pre-built application stacks.</span></span> <span data-ttu-id="2f50e-107">Vous pouvez également utiliser un toodeploy d’image Docker personnalisé à votre pile l’application web application tooan qui n’est pas déjà défini dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2f50e-107">You can also use a custom Docker image toodeploy your web app tooan application stack that is not already defined in Azure.</span></span> <span data-ttu-id="2f50e-108">Les images Docker personnalisées peuvent être hébergées sur un référentiel Docker public ou privé.</span><span class="sxs-lookup"><span data-stu-id="2f50e-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="2f50e-109">Comment : définir une image Docker personnalisée pour une application web</span><span class="sxs-lookup"><span data-stu-id="2f50e-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="2f50e-110">Vous pouvez définir hello Docker image personnalisée pour les nouvelles et les applications Web existantes.</span><span class="sxs-lookup"><span data-stu-id="2f50e-110">You can set hello custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="2f50e-111">Lorsque vous créez une application web sur Linux Bonjour [portail Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), cliquez sur **configurer conteneur** tooset une image Docker personnalisée :</span><span class="sxs-lookup"><span data-stu-id="2f50e-111">When you create a web app on Linux in hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** tooset a custom Docker image:</span></span>

![Image Docker personnalisée pour une nouvelle application web sur Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="2f50e-113">Comment : utiliser une image Docker personnalisée à partir de Docker Hub</span><span class="sxs-lookup"><span data-stu-id="2f50e-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="2f50e-114">toouse une image personnalisée de Docker à partir du Hub d’ancrage :</span><span class="sxs-lookup"><span data-stu-id="2f50e-114">toouse a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="2f50e-115">Bonjour [portail Azure](https://portal.azure.com), localisez votre application web sur Linux, puis dans **paramètres** cliquez sur **conteneur Docker**.</span><span class="sxs-lookup"><span data-stu-id="2f50e-115">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="2f50e-116">Sélectionnez **Hub Docker** comme hello **source de l’Image**, puis cliquez sur **Public** ou **privé** et type Bonjour **Image et nom de la balise facultatif**, tel que `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="2f50e-116">Select **Docker Hub** as hello **Image source**, then click either **Public** or **Private** and type hello **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="2f50e-117">Hello **commande de démarrage** est jeu automatiquement selon ce qui est défini dans le fichier d’image hello Docker, mais vous pouvez définir vos propres commandes.</span><span class="sxs-lookup"><span data-stu-id="2f50e-117">hello **Startup command** is set automatically based on what is defined in hello Docker image file, but you can set your own commands.</span></span>  

    ![Configuration de l’image de référentiel public Docker Hub][2]

    <span data-ttu-id="2f50e-119">Lorsque votre image est d’un référentiel privé, vous devez également les informations d’identification du Hub d’ancrage tooenter hello comme (**nom d’utilisateur** et **mot de passe**) pour le référentiel de Hub d’ancrage hello privé.</span><span class="sxs-lookup"><span data-stu-id="2f50e-119">When your image is from a private repository, you also need tooenter hello Docker Hub credentials as (**Login username** and **Password**) for hello private Docker Hub repository.</span></span>

    ![Configuration de l’image de référentiel public Docker Hub][3]

3. <span data-ttu-id="2f50e-121">Une fois que vous avez configuré le conteneur de hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2f50e-121">After you have configured hello container, click **Save**.</span></span>

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="2f50e-122">Comment toouse une Docker de l’image à partir d’un Registre de l’image privée</span><span class="sxs-lookup"><span data-stu-id="2f50e-122">How toouse a Docker image from a private image registry</span></span> ##
<span data-ttu-id="2f50e-123">toouse une image personnalisée de Docker à partir d’un Registre de l’image privée :</span><span class="sxs-lookup"><span data-stu-id="2f50e-123">toouse a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="2f50e-124">Bonjour [portail Azure](https://portal.azure.com), localisez votre application web sur Linux, puis dans **paramètres** cliquez sur **conteneur Docker**.</span><span class="sxs-lookup"><span data-stu-id="2f50e-124">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="2f50e-125">Cliquez sur **Registre privé** comme hello **source de l’Image**.</span><span class="sxs-lookup"><span data-stu-id="2f50e-125">Click **Private registry** as hello **Image source**.</span></span> <span data-ttu-id="2f50e-126">Entrez hello **Image et le nom de la balise facultatif**, **URL du serveur** Registre privé hello, ainsi que des informations d’identification hello (**nom d’utilisateur** et **mot de passe** ).</span><span class="sxs-lookup"><span data-stu-id="2f50e-126">Enter hello **Image and optional tag name**, **Server URL** for hello private registry, along with hello credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="2f50e-127">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2f50e-127">Click **Save**.</span></span>

    ![Configuration de l’image Docker à partir du registre privé][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a><span data-ttu-id="2f50e-129">Comment : définir le port hello utilisé par votre image de Docker</span><span class="sxs-lookup"><span data-stu-id="2f50e-129">How to: set hello port used by your Docker image</span></span> ##

<span data-ttu-id="2f50e-130">Lorsque vous utilisez une image Docker personnalisée pour votre application web, vous pouvez utiliser hello `WEBSITES_PORT` variable d’environnement dans votre fichier Dockerfile, qui est également ajouté toohello généré conteneur.</span><span class="sxs-lookup"><span data-stu-id="2f50e-130">When you use a custom Docker image for your web app, you can use hello `WEBSITES_PORT` environment variable in your Dockerfile, which gets added toohello generated container.</span></span> <span data-ttu-id="2f50e-131">Tenez compte des hello exemple d’un fichier de docker pour une application Ruby suivant :</span><span class="sxs-lookup"><span data-stu-id="2f50e-131">Consider hello following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="2f50e-132">Sur la dernière ligne de commande hello, vous pouvez voir que cette variable d’environnement WEBSITES_PORT hello est passée de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="2f50e-132">On last line of hello command, you can see that hello WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="2f50e-133">N’oubliez pas les commandes sont sensibles à la casse.</span><span class="sxs-lookup"><span data-stu-id="2f50e-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="2f50e-134">Précédemment a été à l’aide de la plateforme de hello `PORT` application définissant, nous planifiez toodeprecate hello utiliser cette application définissant et déplacer toousing `WEBSITES_PORT` exclusivement.</span><span class="sxs-lookup"><span data-stu-id="2f50e-134">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="2f50e-135">Lorsque vous utilisez une image Docker existante créée par quelqu'un d’autre, vous devrez peut-être toospecify un port autre que le port 80 pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2f50e-135">When you use an existing Docker image built by someone else, you may need toospecify a port other than port 80 for hello application.</span></span> <span data-ttu-id="2f50e-136">tooconfigure hello port, ajoutez une paramètre d’application nommé `WEBSITES_PORT` avec la valeur hello comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2f50e-136">tooconfigure hello port, add an application setting named `WEBSITES_PORT` with hello value as shown below:</span></span>

![Configuration du paramètre d’application PORT pour une image Docker personnalisée][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a><span data-ttu-id="2f50e-138">Comment : définir l’heure de démarrage de hello pour votre image de Docker</span><span class="sxs-lookup"><span data-stu-id="2f50e-138">How to: set hello startup time for your Docker image</span></span> ##

<span data-ttu-id="2f50e-139">Par défaut, si votre conteneur ne démarre pas avant 230 secondes, plateforme de hello redémarrera votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="2f50e-139">By default, if your container does not start before 230 seconds, hello platform will restart your container.</span></span> <span data-ttu-id="2f50e-140">Si votre image personnalisée de Docker démarre en plus de 230 secondes, vous pouvez utiliser hello `WEBSITES_CONTAINER_START_TIME_LIMIT` application paramètre, valeur hello pour ce paramètre est exprimé en secondes, cela permettra hello plateforme conserver votre conteneur en cours d’exécution avant de le redémarrer.</span><span class="sxs-lookup"><span data-stu-id="2f50e-140">If your custom Docker image starts in more than 230 seconds, you can use hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, hello value for this setting is in seconds, this will allow hello platform keep your container running before restarting it.</span></span> <span data-ttu-id="2f50e-141">Hello par défaut est secondes 230 et hello maximum valeur est de 600 secondes.</span><span class="sxs-lookup"><span data-stu-id="2f50e-141">hello default value is 230 seconds, and hello max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-hello-platform-provided-storage"></a><span data-ttu-id="2f50e-142">Comment : décharger le stockage de la plateforme fourni hello</span><span class="sxs-lookup"><span data-stu-id="2f50e-142">How to: unmount hello platform provided storage</span></span> ##

<span data-ttu-id="2f50e-143">Par défaut, la plateforme de hello monte un toohello de partage du stockage persistant `\home\` active.</span><span class="sxs-lookup"><span data-stu-id="2f50e-143">By default, hello platform will mount a persistent storage share toohello `\home\` directory.</span></span> <span data-ttu-id="2f50e-144">Si votre image de conteneur ne doit pas un partage persistant, vous pouvez désactiver le montage que le stockage en définissant un hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` application aussi un paramètre`false`.</span><span class="sxs-lookup"><span data-stu-id="2f50e-144">If your container image does not need a persistent share, you can disable mounting that storage by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span> <span data-ttu-id="2f50e-145">Vous aurez toujours accès toothat stockage à partir du site de scm hello et tous les journaux de Docker (si activé) seront écrit les fichiers de journaux toohello générés par la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="2f50e-145">You will still have access toothat storage from hello scm site, and all Docker logs (if enabled) will be written toohello log files generated by hello platform.</span></span>

## <a name="how-to-switch-back-toousing-a-built-in-image"></a><span data-ttu-id="2f50e-146">Comment : Revenez toousing une image intégrée</span><span class="sxs-lookup"><span data-stu-id="2f50e-146">How to: Switch back toousing a built-in image</span></span> ##

<span data-ttu-id="2f50e-147">tooswitch d’utiliser une image personnalisée de toousing une image intégrée :</span><span class="sxs-lookup"><span data-stu-id="2f50e-147">tooswitch from using a custom image toousing a built-in image:</span></span>

1. <span data-ttu-id="2f50e-148">Bonjour [portail Azure](https://portal.azure.com), localisez votre application web sur Linux, puis dans **paramètres** cliquez sur **du Service d’applications**.</span><span class="sxs-lookup"><span data-stu-id="2f50e-148">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="2f50e-149">Sélectionnez votre **pile de Runtime** toouse pour l’image intégrée de hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2f50e-149">Select your **Runtime Stack** toouse for hello built-in image, then click **Save**.</span></span> 

![Configuration de l’image Docker intégrée][5]


## <a name="troubleshooting"></a><span data-ttu-id="2f50e-151">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="2f50e-151">Troubleshooting</span></span> ##

<span data-ttu-id="2f50e-152">Lorsque votre application échoue toostart avec votre image personnalisée de Docker, vérifiez hello que docker enregistre dans le répertoire des fichiers journaux hello.</span><span class="sxs-lookup"><span data-stu-id="2f50e-152">When your application fails toostart with your custom Docker image, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="2f50e-153">Vous pouvez accéder à ce répertoire par le biais de votre site SCM ou d’un FTP.</span><span class="sxs-lookup"><span data-stu-id="2f50e-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="2f50e-154">toolog hello `stdout` et `stderr` à partir de votre conteneur, vous devez tooenable **journalisation du conteneur Docker** sous **les journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="2f50e-154">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Activation de la journalisation][8]

![Utilisation des journaux de Kudu tooview Docker][7]

<span data-ttu-id="2f50e-157">Vous pouvez accéder à site SCM hello **outils avancés** Bonjour **outils de développement** menu.</span><span class="sxs-lookup"><span data-stu-id="2f50e-157">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f50e-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f50e-158">Next Steps</span></span> ##

<span data-ttu-id="2f50e-159">Suivez hello suivant tooget liens en main de l’application Web sur Linux.</span><span class="sxs-lookup"><span data-stu-id="2f50e-159">Follow hello following links tooget started with Web App on Linux.</span></span>   

* [<span data-ttu-id="2f50e-160">Introduction tooAzure application Web sur Linux</span><span class="sxs-lookup"><span data-stu-id="2f50e-160">Introduction tooAzure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="2f50e-161">Utilisation de la configuration PM2 pour Node.js dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="2f50e-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="2f50e-162">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="2f50e-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="2f50e-163">Posez des questions et indiquez vos préoccupations sur [notre forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="2f50e-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
