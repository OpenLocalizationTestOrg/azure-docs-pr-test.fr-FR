---
title: "FAQ de l’application web Azure App Service sur Linux | Microsoft Docs"
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
ms.openlocfilehash: 6122f28b35d143ec26a379ae9aa8aee9bdaaff9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="0bbed-104">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="0bbed-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="0bbed-105">Avec la mise en production de l’application web sur Linux, nous travaillons à l’ajout de fonctionnalités et à l’amélioration de notre plateforme.</span><span class="sxs-lookup"><span data-stu-id="0bbed-105">With the release of Web App on Linux, we're working on adding features and making improvements to our platform.</span></span> <span data-ttu-id="0bbed-106">Voici quelques-unes des questions courantes que nos clients nous ont posées au cours des derniers mois.</span><span class="sxs-lookup"><span data-stu-id="0bbed-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over the last months.</span></span>
<span data-ttu-id="0bbed-107">Si vous avez une question, commentez l’article ; nous vous répondrons dès que possible.</span><span class="sxs-lookup"><span data-stu-id="0bbed-107">If you have a question, comment on the article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="0bbed-108">Images prédéfinies</span><span class="sxs-lookup"><span data-stu-id="0bbed-108">Built-in images</span></span>

<span data-ttu-id="0bbed-109">**Q :** Je veux répliquer les conteneurs Docker prédéfinis fournis par la plateforme.</span><span class="sxs-lookup"><span data-stu-id="0bbed-109">**Q:** I want to fork the built-in Docker containers that the platform provides.</span></span> <span data-ttu-id="0bbed-110">Où se trouvent ces fichiers ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-110">Where can I find those files?</span></span>

<span data-ttu-id="0bbed-111">**R :** vous trouverez tous les fichiers Docker sur [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="0bbed-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="0bbed-112">Vous trouverez tous les conteneurs Docker sur [Docker Hub](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="0bbed-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="0bbed-113">**Q :** Quelles sont les valeurs attendues de la section Fichier de démarrage lorsque je configure la pile d’exécution ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-113">**Q:** What are the expected values for the Startup File section when I configure the runtime stack?</span></span>

<span data-ttu-id="0bbed-114">**R :** Pour Node.Js, vous spécifiez le fichier de configuration PM2 ou votre fichier de script.</span><span class="sxs-lookup"><span data-stu-id="0bbed-114">**A:** For Node.Js, you specify the PM2 configuration file or your script file.</span></span> <span data-ttu-id="0bbed-115">Pour .NET Core, vous spécifiez le nom de votre DLL compilée.</span><span class="sxs-lookup"><span data-stu-id="0bbed-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="0bbed-116">Pour Ruby, vous pouvez spécifier le script Ruby avec lequel initialiser votre application.</span><span class="sxs-lookup"><span data-stu-id="0bbed-116">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="0bbed-117">Gestion</span><span class="sxs-lookup"><span data-stu-id="0bbed-117">Management</span></span>

<span data-ttu-id="0bbed-118">**Q :** Que se passe-t-il lorsque j’appuie sur le bouton Redémarrer dans le portail Azure ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-118">**Q:** What happens when I press the restart button in the Azure portal?</span></span>

<span data-ttu-id="0bbed-119">**R :** Cela revient à redémarrer Docker.</span><span class="sxs-lookup"><span data-stu-id="0bbed-119">**A:** This is the equivalent of Docker restart.</span></span>

<span data-ttu-id="0bbed-120">**Q :** Puis-je utiliser Secure Shell (SSH) pour me connecter à la machine virtuelle du conteneur d’application ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-120">**Q:** Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?</span></span>

<span data-ttu-id="0bbed-121">**R :** Oui, vous pouvez le faire via le site SCM,. Consultez l’article suivant pour en savoir plus sur [la prise en charge SSH pour l’application Web sur Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="0bbed-121">**A:** Yes, you can do that through the SCM site, check the following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="0bbed-122">**Q :** Je souhaite créer un plan App Service Linux via le Kit SDK ou un modèle ARM, comment faire ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-122">**Q:** I want to create a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="0bbed-123">**R :** Vous devez définir le champ `reserved` du service d’application sur `true`.</span><span class="sxs-lookup"><span data-stu-id="0bbed-123">**A:** You need to set the `reserved` field of the app service to `true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="0bbed-124">Intégration/Déploiement en continu</span><span class="sxs-lookup"><span data-stu-id="0bbed-124">Continuous integration/deployment</span></span>

<span data-ttu-id="0bbed-125">**Q :** Mon application web utilise toujours une ancienne image de conteneur Docker après la mise à jour de l’image sur DockerHub.</span><span class="sxs-lookup"><span data-stu-id="0bbed-125">**Q:** My web app still uses an old Docker container image after I've updated the image on Docker Hub.</span></span> <span data-ttu-id="0bbed-126">Prenez-vous en charge l’intégration continue / le déploiement continu de conteneurs personnalisés ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="0bbed-127">**R :** Pour configurer l’intégration/le déploiement en continu des images Azure Container Registry ou DockerHub, consultez l’article [Déploiement continu avec l’application web Azure sur Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="0bbed-127">**A:** To set up continuous integration/deployment for Azure Container Registry or DockerHub images by check the following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="0bbed-128">Pour les registres privés, vous pouvez actualiser le conteneur en arrêtant puis démarrant votre application web.</span><span class="sxs-lookup"><span data-stu-id="0bbed-128">For private registries, you can refresh the container by stopping and then starting your web app.</span></span> <span data-ttu-id="0bbed-129">Vous pouvez également modifier ou ajouter un paramètre d’application factice pour forcer une actualisation de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="0bbed-129">Or you can change or add a dummy application setting to force a refresh of your container.</span></span>

<span data-ttu-id="0bbed-130">**Q :** Prenez-vous en charge les environnements intermédiaires ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="0bbed-131">**R :** Oui.</span><span class="sxs-lookup"><span data-stu-id="0bbed-131">**A:** Yes.</span></span>

<span data-ttu-id="0bbed-132">**Q :** Puis-je utiliser le **déploiement web** pour déployer mon application web ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-132">**Q:** Can I use **web deploy** to deploy my web app?</span></span>

<span data-ttu-id="0bbed-133">**R :** Oui, vous devez définir le paramètre d’application `WEBSITE_WEBDEPLOY_USE_SCM` sur `false`.</span><span class="sxs-lookup"><span data-stu-id="0bbed-133">**A:** Yes, you need to set an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` to `false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="0bbed-134">Support multilingue</span><span class="sxs-lookup"><span data-stu-id="0bbed-134">Language support</span></span>

<span data-ttu-id="0bbed-135">**Q :** Prenez-vous en charge les applications .NET Core non compilées ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="0bbed-136">**R :** Oui.</span><span class="sxs-lookup"><span data-stu-id="0bbed-136">**A:** Yes.</span></span>

<span data-ttu-id="0bbed-137">**Q :** Prenez-vous en charge Composer en tant que gestionnaire de dépendances pour les applications PHP ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="0bbed-138">**R :** Oui.</span><span class="sxs-lookup"><span data-stu-id="0bbed-138">**A:** Yes.</span></span> <span data-ttu-id="0bbed-139">Lors d’un déploiement Git, Kudu doit détecter que vous déployez une application PHP (grâce à la présence d’un fichier composer.json) et déclenchera une installation Composer pour vous.</span><span class="sxs-lookup"><span data-stu-id="0bbed-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks to the presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="0bbed-140">Conteneurs personnalisés</span><span class="sxs-lookup"><span data-stu-id="0bbed-140">Custom containers</span></span>

<span data-ttu-id="0bbed-141">**Q :** J’utilise mon propre conteneur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0bbed-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="0bbed-142">Mon application se trouve dans le répertoire `\home\`, mais je ne trouve pas mes fichiers lorsque je parcours le contenu avec le [site SCM](https://github.com/projectkudu/kudu) ou un client FTP.</span><span class="sxs-lookup"><span data-stu-id="0bbed-142">My app resides in the `\home\` directory, but I can't find my files when I browse the content by using the [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="0bbed-143">Où sont mes fichiers ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-143">Where are my files?</span></span>

<span data-ttu-id="0bbed-144">**R :** Nous montons un partage SMB dans le répertoire `\home\`.</span><span class="sxs-lookup"><span data-stu-id="0bbed-144">**A:** We mount an SMB share to the `\home\` directory.</span></span> <span data-ttu-id="0bbed-145">Cela remplace tout le contenu qui s’y trouve.</span><span class="sxs-lookup"><span data-stu-id="0bbed-145">This will override any content that's there.</span></span>

<span data-ttu-id="0bbed-146">**Q :** J’utilise mon propre conteneur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0bbed-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="0bbed-147">Je ne souhaite pas que la plateforme monte un partage SMB sur `\home\`.</span><span class="sxs-lookup"><span data-stu-id="0bbed-147">I don't want the platform to mount an SMB share to the `\home\`.</span></span>

<span data-ttu-id="0bbed-148">**R :** Pour cela, définissez le paramètre d’application `WEBSITES_ENABLE_APP_SERVICE_STORAGE` sur `false`.</span><span class="sxs-lookup"><span data-stu-id="0bbed-148">**A:** You can do that by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span>

<span data-ttu-id="0bbed-149">**Q :** Mon conteneur personnalisé met longtemps à démarrer, et la plateforme le redémarre avant qu’il ait terminé.</span><span class="sxs-lookup"><span data-stu-id="0bbed-149">**Q:** My custom container takes a long time to start, and the platform restart the container before it finishes starting up.</span></span>

<span data-ttu-id="0bbed-150">**R :** Vous pouvez configurer le temps d’attente de la plateforme avant le redémarrage de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="0bbed-150">**A:** You can configure the time the platform will wait before restarting your container.</span></span> <span data-ttu-id="0bbed-151">Pour cela, définissez le paramètre d’application `WEBSITES_CONTAINER_START_TIME_LIMIT` sur la valeur souhaitée en secondes.</span><span class="sxs-lookup"><span data-stu-id="0bbed-151">This can be done by setting the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting to the desired value in seconds.</span></span> <span data-ttu-id="0bbed-152">La valeur par défaut est de 230 secondes, la valeur maximale de 600 secondes.</span><span class="sxs-lookup"><span data-stu-id="0bbed-152">The default is 230 seconds, and the max is 600 seconds.</span></span>

<span data-ttu-id="0bbed-153">**Q :** Quel est le format de l’URL du serveur de registre privé ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-153">**Q:** What is the format for private registry server url?</span></span>

<span data-ttu-id="0bbed-154">**R :** Vous devez fournir l’URL de registre complète, y compris `http://` ou `https://`.</span><span class="sxs-lookup"><span data-stu-id="0bbed-154">**A:** You need to provide the full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="0bbed-155">**Q :** Quel est le format du nom d’image dans l’option de registre privé ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-155">**Q:** What is the format for the image name in private registry option?</span></span>

<span data-ttu-id="0bbed-156">**R :** Vous devez ajouter le nom d’image complet, y compris l’URL de registre privé (par exemple :</span><span class="sxs-lookup"><span data-stu-id="0bbed-156">**A:** You need to add the full image name including the private registry url (eg.</span></span> <span data-ttu-id="0bbed-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="0bbed-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="0bbed-158">**Q :** Je veux exposer plusieurs ports sur l’image de mon conteneur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0bbed-158">**Q:** I want to expose more than one port on my custom container image.</span></span> <span data-ttu-id="0bbed-159">Est-ce possible ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-159">Is that possible?</span></span>

<span data-ttu-id="0bbed-160">**R :** Cela n’est actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0bbed-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="0bbed-161">**Q :** Puis-je apporter mon propre système de stockage ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="0bbed-162">**R :** Cela n’est pas actuellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0bbed-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="0bbed-163">**Q :** Je n’arrive pas à parcourir le système de fichiers de mon conteneur personnalisé à partir du site SCM.</span><span class="sxs-lookup"><span data-stu-id="0bbed-163">**Q:** I can't browse my custom container's file system or running processes from the SCM site.</span></span> <span data-ttu-id="0bbed-164">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-164">Why is that?</span></span>

<span data-ttu-id="0bbed-165">**R :** Le site SCM s’exécute dans un conteneur distinct.</span><span class="sxs-lookup"><span data-stu-id="0bbed-165">**A:** The SCM site runs in a separate container.</span></span> <span data-ttu-id="0bbed-166">Vous ne pouvez pas vérifier le système de fichiers ou les processus en cours d’exécution du conteneur d’application.</span><span class="sxs-lookup"><span data-stu-id="0bbed-166">You can't check the file system or running processes of the app container.</span></span>

<span data-ttu-id="0bbed-167">**Q :** Mon conteneur personnalisé écoute un autre port que le port 80.</span><span class="sxs-lookup"><span data-stu-id="0bbed-167">**Q:** My custom container listens to a port other than port 80.</span></span> <span data-ttu-id="0bbed-168">Comment puis-je configurer mon application pour acheminer les demandes vers ce port ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-168">How can I configure my app to route the requests to that port?</span></span>

<span data-ttu-id="0bbed-169">**R :** La détection automatique du port est activée, mais vous pouvez aussi spécifier un paramètre d’application appelé **WEBSITES_PORT** et lui attribuer la valeur du numéro de port attendu.</span><span class="sxs-lookup"><span data-stu-id="0bbed-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it the value of the expected port number.</span></span> <span data-ttu-id="0bbed-170">Auparavant, la plateforme utilisait le paramètre d’application `PORT`, mais nous envisageons de déconseiller l’utilisation de ce paramètre d’application pour recommander une utilisation exclusive de `WEBSITES_PORT`.</span><span class="sxs-lookup"><span data-stu-id="0bbed-170">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="0bbed-171">**Q :** Dois-je implémenter HTTPS dans mon conteneur personnalisé ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-171">**Q:** Do I need to implement HTTPS in my custom container.</span></span>

<span data-ttu-id="0bbed-172">**R :** Non, la plateforme gère l’annulation HTTPS au niveau des serveurs frontaux partagés.</span><span class="sxs-lookup"><span data-stu-id="0bbed-172">**A:** No, the platform handles HTTPS termination at the shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="0bbed-173">Tarifs et contrat SLA</span><span class="sxs-lookup"><span data-stu-id="0bbed-173">Pricing and SLA</span></span>

<span data-ttu-id="0bbed-174">**Q :** Quelle est la tarification pour l’utilisation de la préversion publique ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-174">**Q:** What's the pricing while you're using the public preview?</span></span>

<span data-ttu-id="0bbed-175">**R :** La moitié du nombre d’heures d’exécution de votre application vous est facturée, à la tarification Azure App Service normale.</span><span class="sxs-lookup"><span data-stu-id="0bbed-175">**A:** You are charged half the number of hours that your app runs, with the normal Azure App Service pricing.</span></span> <span data-ttu-id="0bbed-176">Cela signifie que vous bénéficiez d’une remise de 50 pour cent sur la tarification normale d’Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0bbed-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="0bbed-177">Autres</span><span class="sxs-lookup"><span data-stu-id="0bbed-177">Other</span></span>

<span data-ttu-id="0bbed-178">**Q :** Quels sont les caractères pris en charge dans les noms de paramètres d’application ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-178">**Q:** What are the supported characters in application settings names?</span></span>

<span data-ttu-id="0bbed-179">**R :** Vous ne pouvez utiliser que les caractères A-Z, a-z, 0-9 et le trait de soulignement pour les paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="0bbed-179">**A:** You can only use A-Z, a-z, 0-9, and the underscore for application settings.</span></span>

<span data-ttu-id="0bbed-180">**Q :** Où puis-je demander de nouvelles fonctionnalités ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="0bbed-181">**R :** Vous pouvez proposer votre idée sur le [Forum de commentaires pour Web Apps](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="0bbed-181">**A:** You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="0bbed-182">Ajoutez « [Linux] » au titre de votre idée.</span><span class="sxs-lookup"><span data-stu-id="0bbed-182">Add "[Linux]" to the title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bbed-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0bbed-183">Next steps</span></span>
* [<span data-ttu-id="0bbed-184">Qu’est-ce qu’Azure Web App sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="0bbed-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="0bbed-185">Prise en charge SSH pour Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="0bbed-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="0bbed-186">Configurer des environnements intermédiaires dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0bbed-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="0bbed-187">Déploiement continu avec l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="0bbed-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
