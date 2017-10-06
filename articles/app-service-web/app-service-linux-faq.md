---
title: "aaaAzure application de Service d’applications Web sur le Forum aux questions sur Linux | Documents Microsoft"
description: "FAQ de l’application web Azure App Service sur Linux."
keywords: azure app service, application web, faq, linux, oss
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="5c7a6-104">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="5c7a6-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="5c7a6-105">Avec la version hello de l’application Web sur Linux, nous travaillons sur l’ajout de fonctionnalités et de la plateforme de tooour améliorations.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-105">With hello release of Web App on Linux, we're working on adding features and making improvements tooour platform.</span></span> <span data-ttu-id="5c7a6-106">Ici sont Forum aux questions (FAQ) que nos clients ont demandé nous sur hello derniers mois.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over hello last months.</span></span>
<span data-ttu-id="5c7a6-107">Si vous avez une question, commentaire sur l’article de hello et nous répondrons il dès que possible.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-107">If you have a question, comment on hello article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="5c7a6-108">Images prédéfinies</span><span class="sxs-lookup"><span data-stu-id="5c7a6-108">Built-in images</span></span>

<span data-ttu-id="5c7a6-109">**Q :** je veux toofork hello intégrés conteneurs Docker qui hello plateforme fournit.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-109">**Q:** I want toofork hello built-in Docker containers that hello platform provides.</span></span> <span data-ttu-id="5c7a6-110">Où se trouvent ces fichiers ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-110">Where can I find those files?</span></span>

<span data-ttu-id="5c7a6-111">**R :** vous trouverez tous les fichiers Docker sur [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="5c7a6-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="5c7a6-112">Vous trouverez tous les conteneurs Docker sur [Docker Hub](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="5c7a6-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="5c7a6-113">**Q :** quelles sont les valeurs attendues hello pour hello section du fichier de démarrage lors de la configuration de la pile d’exécution hello ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-113">**Q:** What are hello expected values for hello Startup File section when I configure hello runtime stack?</span></span>

<span data-ttu-id="5c7a6-114">**R :** pour Node.Js, vous spécifiez au fichier de configuration hello PM2 ou votre fichier de script.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-114">**A:** For Node.Js, you specify hello PM2 configuration file or your script file.</span></span> <span data-ttu-id="5c7a6-115">Pour .NET Core, vous spécifiez le nom de votre DLL compilée.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="5c7a6-116">Pour Ruby, vous pouvez spécifier hello Ruby script que vous souhaitez tooinitialize votre application avec.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-116">For Ruby, you can specify hello Ruby script that you want tooinitialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="5c7a6-117">Gestion</span><span class="sxs-lookup"><span data-stu-id="5c7a6-117">Management</span></span>

<span data-ttu-id="5c7a6-118">**Q :** que se passe-t-il quand je bouton hello redémarrage Bonjour portail Azure ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-118">**Q:** What happens when I press hello restart button in hello Azure portal?</span></span>

<span data-ttu-id="5c7a6-119">**R :** cela est hello équivalents au redémarrage de Docker.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-119">**A:** This is hello equivalent of Docker restart.</span></span>

<span data-ttu-id="5c7a6-120">**Q :** puis-je utiliser Secure Shell (SSH) tooconnect toohello application conteneur machine virtuelle (VM) ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-120">**Q:** Can I use Secure Shell (SSH) tooconnect toohello app container virtual machine (VM)?</span></span>

<span data-ttu-id="5c7a6-121">**R :** Oui, vous pouvez effectuer que via le site SCM hello, cocher hello article suivant pour plus d’informations [prise en charge SSH pour l’application Web sur Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="5c7a6-121">**A:** Yes, you can do that through hello SCM site, check hello following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="5c7a6-122">**Q :** je veux toocreate un plan de Service d’applications Linux via le Kit de développement logiciel ou un modèle ARM, comment puis-je effectuer cette opération ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-122">**Q:** I want toocreate a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="5c7a6-123">**R :** vous devez tooset hello `reserved` trop de champs de l’application hello service`true`.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-123">**A:** You need tooset hello `reserved` field of hello app service too`true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="5c7a6-124">Intégration/Déploiement en continu</span><span class="sxs-lookup"><span data-stu-id="5c7a6-124">Continuous integration/deployment</span></span>

<span data-ttu-id="5c7a6-125">**Q :** mon application web utilise toujours une ancienne image de conteneur Docker une fois que j’ai mis à jour image hello sur le Hub d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-125">**Q:** My web app still uses an old Docker container image after I've updated hello image on Docker Hub.</span></span> <span data-ttu-id="5c7a6-126">Prenez-vous en charge l’intégration continue / le déploiement continu de conteneurs personnalisés ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="5c7a6-127">**R :** tooset d’intégration/déploiement continu pour les images docker Hub ou de Registre de conteneur Azure par hello de vérification de l’article suivant [déploiement continu avec l’application Web Azure sous Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="5c7a6-127">**A:** tooset up continuous integration/deployment for Azure Container Registry or DockerHub images by check hello following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="5c7a6-128">Pour les registres privés, vous pouvez actualiser le conteneur de hello en arrêtant et avant de démarrer votre application web.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-128">For private registries, you can refresh hello container by stopping and then starting your web app.</span></span> <span data-ttu-id="5c7a6-129">Ou vous pouvez modifier ou ajouter une paramètre tooforce une actualisation de votre conteneur d’application factice.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-129">Or you can change or add a dummy application setting tooforce a refresh of your container.</span></span>

<span data-ttu-id="5c7a6-130">**Q :** Prenez-vous en charge les environnements intermédiaires ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="5c7a6-131">**R :** Oui.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-131">**A:** Yes.</span></span>

<span data-ttu-id="5c7a6-132">**Q :** puis-je utiliser **déploiement web** toodeploy mon application web ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-132">**Q:** Can I use **web deploy** toodeploy my web app?</span></span>

<span data-ttu-id="5c7a6-133">**R :** Oui, vous avez besoin de tooset une application appelé `WEBSITE_WEBDEPLOY_USE_SCM` trop`false`.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-133">**A:** Yes, you need tooset an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` too`false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="5c7a6-134">Support multilingue</span><span class="sxs-lookup"><span data-stu-id="5c7a6-134">Language support</span></span>

<span data-ttu-id="5c7a6-135">**Q :** Prenez-vous en charge les applications .NET Core non compilées ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="5c7a6-136">**R :** Oui.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-136">**A:** Yes.</span></span>

<span data-ttu-id="5c7a6-137">**Q :** Prenez-vous en charge Composer en tant que gestionnaire de dépendances pour les applications PHP ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="5c7a6-138">**R :** Oui.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-138">**A:** Yes.</span></span> <span data-ttu-id="5c7a6-139">Lors d’un déploiement Git, Kudu doit détecter que vous déployez une application PHP (Merci de toohello présence d’un fichier composer.json) et déclenchera une installation composer pour vous.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks toohello presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="5c7a6-140">Conteneurs personnalisés</span><span class="sxs-lookup"><span data-stu-id="5c7a6-140">Custom containers</span></span>

<span data-ttu-id="5c7a6-141">**Q :** J’utilise mon propre conteneur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="5c7a6-142">Mon application réside dans hello `\home\` active, mais je ne trouvons pas mes fichiers lorsque je parcourir le contenu de hello à l’aide de hello [site SCM](https://github.com/projectkudu/kudu) ou un client FTP.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-142">My app resides in hello `\home\` directory, but I can't find my files when I browse hello content by using hello [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="5c7a6-143">Où sont mes fichiers ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-143">Where are my files?</span></span>

<span data-ttu-id="5c7a6-144">**R :** nous monter une toohello de partage SMB `\home\` active.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-144">**A:** We mount an SMB share toohello `\home\` directory.</span></span> <span data-ttu-id="5c7a6-145">Cela remplace tout le contenu qui s’y trouve.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-145">This will override any content that's there.</span></span>

<span data-ttu-id="5c7a6-146">**Q :** J’utilise mon propre conteneur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="5c7a6-147">Je ne souhaite pas hello plateforme toomount un toohello de partage SMB `\home\`.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-147">I don't want hello platform toomount an SMB share toohello `\home\`.</span></span>

<span data-ttu-id="5c7a6-148">**R :** vous suffit de définition de hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` application aussi un paramètre`false`.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-148">**A:** You can do that by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span>

<span data-ttu-id="5c7a6-149">**Q :** mon conteneur personnalisé prend un toostart beaucoup de temps, et la fin de conteneur de hello hello plateforme redémarrage avant son démarrage.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-149">**Q:** My custom container takes a long time toostart, and hello platform restart hello container before it finishes starting up.</span></span>

<span data-ttu-id="5c7a6-150">**R :** vous pouvez configurer hello plateforme de hello attendra avant le redémarrage de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-150">**A:** You can configure hello time hello platform will wait before restarting your container.</span></span> <span data-ttu-id="5c7a6-151">Cela est possible en définissant les hello `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello de paramètre d’application de valeur souhaitée en secondes.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-151">This can be done by setting hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting toohello desired value in seconds.</span></span> <span data-ttu-id="5c7a6-152">valeur par défaut Hello est 230 secondes et hello maximale est de 600 secondes.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-152">hello default is 230 seconds, and hello max is 600 seconds.</span></span>

<span data-ttu-id="5c7a6-153">**Q :** What format hello pour l’url du serveur de Registre privé ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-153">**Q:** What is hello format for private registry server url?</span></span>

<span data-ttu-id="5c7a6-154">**R :** vous avez besoin d’y compris les url Registre complet de hello de tooprovide `http://` ou `https://`.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-154">**A:** You need tooprovide hello full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="5c7a6-155">**Q :** What format hello pour le nom de l’image hello dans l’option de Registre privé ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-155">**Q:** What is hello format for hello image name in private registry option?</span></span>

<span data-ttu-id="5c7a6-156">**R :** vous devez tooadd hello complet nom de l’image, notamment hello Registre privé url (par exemple).</span><span class="sxs-lookup"><span data-stu-id="5c7a6-156">**A:** You need tooadd hello full image name including hello private registry url (eg.</span></span> <span data-ttu-id="5c7a6-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="5c7a6-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="5c7a6-158">**Q :** souhaitée tooexpose plusieurs ports sur mon image de conteneur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-158">**Q:** I want tooexpose more than one port on my custom container image.</span></span> <span data-ttu-id="5c7a6-159">Est-ce possible ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-159">Is that possible?</span></span>

<span data-ttu-id="5c7a6-160">**R :** Cela n’est actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="5c7a6-161">**Q :** Puis-je apporter mon propre système de stockage ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="5c7a6-162">**R :** Cela n’est pas actuellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="5c7a6-163">**Q :** je ne peux pas naviguer sur fichier système ou en cours d’exécution des processus du mon conteneur personnalisé à partir du site SCM hello.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-163">**Q:** I can't browse my custom container's file system or running processes from hello SCM site.</span></span> <span data-ttu-id="5c7a6-164">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-164">Why is that?</span></span>

<span data-ttu-id="5c7a6-165">**R :** site SCM hello s’exécute dans un conteneur distinct.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-165">**A:** hello SCM site runs in a separate container.</span></span> <span data-ttu-id="5c7a6-166">Vous ne peut pas vérifier le système de fichiers hello ou de l’exécution du processus de conteneur d’application hello.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-166">You can't check hello file system or running processes of hello app container.</span></span>

<span data-ttu-id="5c7a6-167">**Q :** mon conteneur personnalisé écoute le port tooa autre que le port 80.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-167">**Q:** My custom container listens tooa port other than port 80.</span></span> <span data-ttu-id="5c7a6-168">Comment puis-je configurer mon port toothat de demandes application tooroute hello ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-168">How can I configure my app tooroute hello requests toothat port?</span></span>

<span data-ttu-id="5c7a6-169">**R :** nous avons la détection automatique du port, vous pouvez également spécifier une application appelé **WEBSITES_PORT**et lui donner la valeur hello du numéro de port hello attendu.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it hello value of hello expected port number.</span></span> <span data-ttu-id="5c7a6-170">Précédemment a été à l’aide de la plateforme de hello `PORT` application définissant, nous planifiez toodeprecate hello utiliser cette application définissant et déplacer toousing `WEBSITES_PORT` exclusivement.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-170">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="5c7a6-171">**Q :** dois-je tooimplement HTTPS dans mon conteneur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-171">**Q:** Do I need tooimplement HTTPS in my custom container.</span></span>

<span data-ttu-id="5c7a6-172">**R :** non, plateforme de hello gère arrêt du protocole HTTPS pour les serveurs frontaux hello partagé.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-172">**A:** No, hello platform handles HTTPS termination at hello shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="5c7a6-173">Tarifs et contrat SLA</span><span class="sxs-lookup"><span data-stu-id="5c7a6-173">Pricing and SLA</span></span>

<span data-ttu-id="5c7a6-174">**Q :** quel est hello le prix pendant que vous utilisez une version préliminaire publique de hello ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-174">**Q:** What's hello pricing while you're using hello public preview?</span></span>

<span data-ttu-id="5c7a6-175">**R :** vous êtes facturé moitié nombre hello d’heures pendant lesquelles votre application s’exécute avec la tarification de Azure App Service normal hello.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-175">**A:** You are charged half hello number of hours that your app runs, with hello normal Azure App Service pricing.</span></span> <span data-ttu-id="5c7a6-176">Cela signifie que vous bénéficiez d’une remise de 50 pour cent sur la tarification normale d’Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="5c7a6-177">Autres</span><span class="sxs-lookup"><span data-stu-id="5c7a6-177">Other</span></span>

<span data-ttu-id="5c7a6-178">**Q :** quels sont les caractères hello pris en charge dans les noms de paramètres d’application ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-178">**Q:** What are hello supported characters in application settings names?</span></span>

<span data-ttu-id="5c7a6-179">**R :** vous pouvez uniquement utiliser A-Z, a-z, 0-9 et hello trait de soulignement pour les paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-179">**A:** You can only use A-Z, a-z, 0-9, and hello underscore for application settings.</span></span>

<span data-ttu-id="5c7a6-180">**Q :** Où puis-je demander de nouvelles fonctionnalités ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="5c7a6-181">**R :** vous pouvez soumettre votre idée à hello [forum de commentaires d’applications Web](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="5c7a6-181">**A:** You can submit your idea at hello [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="5c7a6-182">Ajouter un titre de toohello « [Linux] » de votre idée.</span><span class="sxs-lookup"><span data-stu-id="5c7a6-182">Add "[Linux]" toohello title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c7a6-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c7a6-183">Next steps</span></span>
* [<span data-ttu-id="5c7a6-184">Qu’est-ce qu’Azure Web App sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="5c7a6-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="5c7a6-185">Prise en charge SSH pour Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="5c7a6-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="5c7a6-186">Configurer des environnements intermédiaires dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5c7a6-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="5c7a6-187">Déploiement continu avec l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="5c7a6-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
