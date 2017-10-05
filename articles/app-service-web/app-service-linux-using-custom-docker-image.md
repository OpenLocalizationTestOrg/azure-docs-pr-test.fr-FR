---
title: "Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux | Microsoft Docs"
description: "Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux."
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
ms.openlocfilehash: 1458217a31c4781b28877c030a665f5b22819e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="57319-104">Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="57319-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="57319-105">App Service fournit des piles d’applications prédéfinies sur Linux avec la prise en charge de versions spécifiques, comme PHP 7.0 et Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="57319-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="57319-106">App Service sur Linux utilise des conteneurs Docker pour héberger ces piles d’applications prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="57319-106">App Service on Linux uses Docker containers to host these pre-built application stacks.</span></span> <span data-ttu-id="57319-107">Vous pouvez également utiliser une image Docker personnalisée pour déployer votre application web sur une pile d’applications qui n’est pas encore définie dans Azure.</span><span class="sxs-lookup"><span data-stu-id="57319-107">You can also use a custom Docker image to deploy your web app to an application stack that is not already defined in Azure.</span></span> <span data-ttu-id="57319-108">Les images Docker personnalisées peuvent être hébergées sur un référentiel Docker public ou privé.</span><span class="sxs-lookup"><span data-stu-id="57319-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="57319-109">Comment : définir une image Docker personnalisée pour une application web</span><span class="sxs-lookup"><span data-stu-id="57319-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="57319-110">Vous pouvez définir une image Docker personnalisée pour les applications web nouvelles et existantes.</span><span class="sxs-lookup"><span data-stu-id="57319-110">You can set the custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="57319-111">Lorsque vous créez une application web sur Linux dans le [portail Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), cliquez sur **Configurer le conteneur** pour définir une image Docker personnalisée :</span><span class="sxs-lookup"><span data-stu-id="57319-111">When you create a web app on Linux in the [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** to set a custom Docker image:</span></span>

![Image Docker personnalisée pour une nouvelle application web sur Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="57319-113">Comment : utiliser une image Docker personnalisée à partir de Docker Hub</span><span class="sxs-lookup"><span data-stu-id="57319-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="57319-114">Pour utiliser une image Docker personnalisée à partir de Docker Hub :</span><span class="sxs-lookup"><span data-stu-id="57319-114">To use a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="57319-115">Dans le [portail Azure](https://portal.azure.com), localisez votre application web sur Linux, puis dans **Paramètres** cliquez sur **Conteneur Docker**.</span><span class="sxs-lookup"><span data-stu-id="57319-115">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="57319-116">Sélectionnez **Docker Hub** comme **source de l’image**, puis cliquez sur **Public** ou **Privé** et tapez le **nom de l’image et de la balise facultative**, par exemple `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="57319-116">Select **Docker Hub** as the **Image source**, then click either **Public** or **Private** and type the **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="57319-117">La **commande de démarrage** est définie automatiquement en fonction de ce qui est défini dans le fichier d’image Docker, mais vous pouvez définir vos propres commandes.</span><span class="sxs-lookup"><span data-stu-id="57319-117">The **Startup command** is set automatically based on what is defined in the Docker image file, but you can set your own commands.</span></span>  

    ![Configuration de l’image de référentiel public Docker Hub][2]

    <span data-ttu-id="57319-119">Lorsque votre image est issue d’un référentiel privé, vous devez également entrer les informations d’identification Docker Hub (**Nom d’utilisateur** et **Mot de passe**) du référentiel privé Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="57319-119">When your image is from a private repository, you also need to enter the Docker Hub credentials as (**Login username** and **Password**) for the private Docker Hub repository.</span></span>

    ![Configuration de l’image de référentiel public Docker Hub][3]

3. <span data-ttu-id="57319-121">Une fois le conteneur configuré, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="57319-121">After you have configured the container, click **Save**.</span></span>

## <a name="how-to-use-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="57319-122">Utilisation d’une image Docker à partir d’un registre d’images privé</span><span class="sxs-lookup"><span data-stu-id="57319-122">How to use a Docker image from a private image registry</span></span> ##
<span data-ttu-id="57319-123">Pour utiliser une image Docker personnalisée à partir d’un registre d’images privé :</span><span class="sxs-lookup"><span data-stu-id="57319-123">To use a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="57319-124">Dans le [portail Azure](https://portal.azure.com), localisez votre application web sur Linux, puis dans **Paramètres** cliquez sur **Conteneur Docker**.</span><span class="sxs-lookup"><span data-stu-id="57319-124">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="57319-125">Cliquez sur **Registre privé** comme **source de l’image**.</span><span class="sxs-lookup"><span data-stu-id="57319-125">Click **Private registry** as the **Image source**.</span></span> <span data-ttu-id="57319-126">Entrez l**’image et le nom facultatif de la balise**, l**’URL du serveur** du registre privé, ainsi que les informations d’identification (**nom d’utilisateur** et **mot de passe**).</span><span class="sxs-lookup"><span data-stu-id="57319-126">Enter the **Image and optional tag name**, **Server URL** for the private registry, along with the credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="57319-127">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="57319-127">Click **Save**.</span></span>

    ![Configuration de l’image Docker à partir du registre privé][4]


## <a name="how-to-set-the-port-used-by-your-docker-image"></a><span data-ttu-id="57319-129">Comment : définir le port utilisé par votre image Docker</span><span class="sxs-lookup"><span data-stu-id="57319-129">How to: set the port used by your Docker image</span></span> ##

<span data-ttu-id="57319-130">Lorsque vous utilisez une image Docker personnalisée pour votre application web, vous pouvez utiliser la variable d’environnement `WEBSITES_PORT` dans votre ficher Docker, qui est ajoutée au conteneur généré.</span><span class="sxs-lookup"><span data-stu-id="57319-130">When you use a custom Docker image for your web app, you can use the `WEBSITES_PORT` environment variable in your Dockerfile, which gets added to the generated container.</span></span> <span data-ttu-id="57319-131">Prenons l’exemple suivant d’un fichier Docker pour une application Ruby :</span><span class="sxs-lookup"><span data-stu-id="57319-131">Consider the following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="57319-132">Sur la dernière ligne de commande, la variable d’environnement WEBSITES_PORT est transmise au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="57319-132">On last line of the command, you can see that the WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="57319-133">N’oubliez pas les commandes sont sensibles à la casse.</span><span class="sxs-lookup"><span data-stu-id="57319-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="57319-134">Auparavant, la plateforme utilisait le paramètre d’application `PORT`, mais nous envisageons de déconseiller l’utilisation de ce paramètre d’application pour recommander une utilisation exclusive de `WEBSITES_PORT`.</span><span class="sxs-lookup"><span data-stu-id="57319-134">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="57319-135">Si vous utilisez une image Docker existante créée par une autre personne, vous devrez peut-être spécifier un port autre que le port 80 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="57319-135">When you use an existing Docker image built by someone else, you may need to specify a port other than port 80 for the application.</span></span> <span data-ttu-id="57319-136">Pour configurer le port, ajoutez un paramètre d’application nommé `WEBSITES_PORT` avec la valeur, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="57319-136">To configure the port, add an application setting named `WEBSITES_PORT` with the value as shown below:</span></span>

![Configuration du paramètre d’application PORT pour une image Docker personnalisée][6]

## <a name="how-to-set-the-startup-time-for-your-docker-image"></a><span data-ttu-id="57319-138">Guide pratique : définir l’heure de démarrage d’une image Docker</span><span class="sxs-lookup"><span data-stu-id="57319-138">How to: set the startup time for your Docker image</span></span> ##

<span data-ttu-id="57319-139">Par défaut, si votre conteneur ne démarre pas avant 230 secondes, la plateforme le redémarre.</span><span class="sxs-lookup"><span data-stu-id="57319-139">By default, if your container does not start before 230 seconds, the platform will restart your container.</span></span> <span data-ttu-id="57319-140">Si votre image Docker personnalisée met plus de 230 secondes à démarrer, vous pouvez utiliser le paramètre d’application `WEBSITES_CONTAINER_START_TIME_LIMIT`. La valeur de ce paramètre, exprimée en secondes, permet à la plateforme de maintenir votre conteneur en cours d’exécution avant de le redémarrer.</span><span class="sxs-lookup"><span data-stu-id="57319-140">If your custom Docker image starts in more than 230 seconds, you can use the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, the value for this setting is in seconds, this will allow the platform keep your container running before restarting it.</span></span> <span data-ttu-id="57319-141">La valeur par défaut est de 230 secondes, la valeur maximale autorisée de 600 secondes.</span><span class="sxs-lookup"><span data-stu-id="57319-141">The default value is 230 seconds, and the max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-the-platform-provided-storage"></a><span data-ttu-id="57319-142">Guide pratique : démonter le stockage fourni par la plateforme</span><span class="sxs-lookup"><span data-stu-id="57319-142">How to: unmount the platform provided storage</span></span> ##

<span data-ttu-id="57319-143">Par défaut, la plateforme monte un partage de stockage persistant sur le répertoire `\home\`.</span><span class="sxs-lookup"><span data-stu-id="57319-143">By default, the platform will mount a persistent storage share to the `\home\` directory.</span></span> <span data-ttu-id="57319-144">Si votre image conteneur n’a pas besoin d’un partage persistant, vous pouvez désactiver le montage de ce stockage en définissant le paramètre d’application `WEBSITES_ENABLE_APP_SERVICE_STORAGE` sur `false`.</span><span class="sxs-lookup"><span data-stu-id="57319-144">If your container image does not need a persistent share, you can disable mounting that storage by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span> <span data-ttu-id="57319-145">Vous aurez toujours accès à ce stockage à partir du site scm, et tous les journaux Docker (s’ils sont activés) seront écrits dans les fichiers journaux générés par la plateforme.</span><span class="sxs-lookup"><span data-stu-id="57319-145">You will still have access to that storage from the scm site, and all Docker logs (if enabled) will be written to the log files generated by the platform.</span></span>

## <a name="how-to-switch-back-to-using-a-built-in-image"></a><span data-ttu-id="57319-146">Comment : revenir à l’utilisation d’une image intégrée</span><span class="sxs-lookup"><span data-stu-id="57319-146">How to: Switch back to using a built-in image</span></span> ##

<span data-ttu-id="57319-147">Pour passer d’une image personnalisée à une image intégrée :</span><span class="sxs-lookup"><span data-stu-id="57319-147">To switch from using a custom image to using a built-in image:</span></span>

1. <span data-ttu-id="57319-148">Dans le [portail Azure](https://portal.azure.com), localisez votre application web sur Linux, puis dans **Paramètres** cliquez sur **App Service**.</span><span class="sxs-lookup"><span data-stu-id="57319-148">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="57319-149">Sélectionnez la **pile d’exécution** à utiliser pour l’image intégrée, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="57319-149">Select your **Runtime Stack** to use for the built-in image, then click **Save**.</span></span> 

![Configuration de l’image Docker intégrée][5]


## <a name="troubleshooting"></a><span data-ttu-id="57319-151">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="57319-151">Troubleshooting</span></span> ##

<span data-ttu-id="57319-152">Si le démarrage de l’application échoue avec une image Docker personnalisée, consultez les journaux Docker dans le répertoire LogFiles.</span><span class="sxs-lookup"><span data-stu-id="57319-152">When your application fails to start with your custom Docker image, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="57319-153">Vous pouvez accéder à ce répertoire par le biais de votre site SCM ou d’un FTP.</span><span class="sxs-lookup"><span data-stu-id="57319-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="57319-154">Pour journaliser `stdout` et `stderr` à partir de votre conteneur, vous devez activer **Journalisation de conteneur Docker** sous **Journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="57319-154">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Activation de la journalisation][8]

![Affichage des journaux Docker avec Kudu][7]

<span data-ttu-id="57319-157">Vous pouvez accéder au site SCM à partir d’**Outils avancés** dans le menu **Outils de développement**.</span><span class="sxs-lookup"><span data-stu-id="57319-157">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57319-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57319-158">Next Steps</span></span> ##

<span data-ttu-id="57319-159">Suivez les liens ci-après pour vous familiariser avec Web App sur Linux.</span><span class="sxs-lookup"><span data-stu-id="57319-159">Follow the following links to get started with Web App on Linux.</span></span>   

* [<span data-ttu-id="57319-160">Présentation d’Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="57319-160">Introduction to Azure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="57319-161">Utiliser la configuration PM2 pour Node.js dans Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="57319-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="57319-162">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="57319-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="57319-163">Posez des questions et indiquez vos préoccupations sur [notre forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="57319-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
