---
title: "aaaDeploy votre tooCloud application première Foundry sur Microsoft Azure | Documents Microsoft"
description: "Déployer une application de tooCloud Foundry sur Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a><span data-ttu-id="51e7b-103">Déployer votre premier tooCloud d’application Foundry sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="51e7b-103">Deploy your first app tooCloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="51e7b-104">[Cloud Foundry](http://cloudfoundry.org) est une plateforme d’applications open source populaire disponible sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="51e7b-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="51e7b-105">Dans cet article, nous montrons comment toodeploy et gérer une application sur le Cloud Foundry dans un environnement Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="51e7b-105">In this article, we show how toodeploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="51e7b-106">Création d’un environnement Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="51e7b-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="51e7b-107">Il existe plusieurs façons de créer un environnement Cloud Foundry sur Azure :</span><span class="sxs-lookup"><span data-stu-id="51e7b-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="51e7b-108">Hello d’utilisation [offre de pivot Cloud Foundry] [ pcf-azuremarketplace] dans Azure Marketplace de hello toocreate un environnement standard qui inclut PCF Operations Manager et hello Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="51e7b-108">Use hello [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in hello Azure Marketplace toocreate a standard environment that includes PCF Ops Manager and hello Azure Service Broker.</span></span> <span data-ttu-id="51e7b-109">Vous pouvez trouver [instructions complètes] [ pcf-azuremarketplace-pivotaldocs] pour le déploiement de marketplace de hello proposer dans hello documentation pivot.</span><span class="sxs-lookup"><span data-stu-id="51e7b-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying hello marketplace offer in hello Pivotal documentation.</span></span>
- <span data-ttu-id="51e7b-110">Créez un environnement personnalisé en [déployant manuellement Pivotal Cloud Foundry][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="51e7b-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="51e7b-111">[Déployer des packages de Cloud Foundry hello open source directement] [ oss-cf-bosh] en configurant un [BOSH](http://bosh.io) directeur, une machine virtuelle qui coordonne déploiement hello d’environnement de Cloud Foundry hello.</span><span class="sxs-lookup"><span data-stu-id="51e7b-111">[Deploy hello open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates hello deployment of hello Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="51e7b-112">Si vous déployez PCF de hello Azure Marketplace, prenez note de hello SYSTEMDOMAINURL et informations d’identification d’administrateur de hello nécessaire tooaccess hello pivot Gestionnaire d’applications, qui sont décrites dans le guide de déploiement hello marketplace.</span><span class="sxs-lookup"><span data-stu-id="51e7b-112">If you are deploying PCF from hello Azure Marketplace, make a note of hello SYSTEMDOMAINURL and hello admin credentials required tooaccess hello Pivotal Apps Manager, both of which are described in hello marketplace deployment guide.</span></span> <span data-ttu-id="51e7b-113">Ils est nécessaire toocomplete ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="51e7b-113">They are needed toocomplete this tutorial.</span></span> <span data-ttu-id="51e7b-114">Pour les déploiements de marketplace, hello SYSTEMDOMAINURL est hello formulaire https://system. *-adresse ip*. cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="51e7b-114">For marketplace deployments, hello SYSTEMDOMAINURL is in hello form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-toohello-cloud-controller"></a><span data-ttu-id="51e7b-115">Se connecter toohello contrôleur de Cloud</span><span class="sxs-lookup"><span data-stu-id="51e7b-115">Connect toohello Cloud Controller</span></span>

<span data-ttu-id="51e7b-116">Hello contrôleur de Cloud est environnement de Cloud Foundry point tooa hello entrée de serveur principal pour le déploiement et la gestion des applications.</span><span class="sxs-lookup"><span data-stu-id="51e7b-116">hello Cloud Controller is hello primary entry point tooa Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="51e7b-117">le cœur de Hello API de contrôleur de Cloud (CCAPI) est une API REST, mais il est accessible via différents outils.</span><span class="sxs-lookup"><span data-stu-id="51e7b-117">hello core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="51e7b-118">Dans ce cas, vous interagissez avec elle via hello [Cloud Foundry CLI][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="51e7b-118">In this case, we interact with it through hello [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="51e7b-119">Vous pouvez installer hello CLI sur Linux, Mac OS ou Windows, mais si vous préférez pas les tooinstall il, il est disponible préinstallé Bonjour [Azure Cloud Shell][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="51e7b-119">You can install hello CLI on Linux, MacOS, or Windows, but if you'd prefer not tooinstall it at all, it is available pre-installed in hello [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="51e7b-120">toolog, ajouter `api` toohello SYSTEMDOMAINURL que vous avez obtenue à partir de déploiement de marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="51e7b-120">toolog in, prepend `api` toohello SYSTEMDOMAINURL that you obtained from hello marketplace deployment.</span></span> <span data-ttu-id="51e7b-121">Étant donné que le déploiement par défaut de hello utilise un certificat auto-signé, vous devez également inclure hello `skip-ssl-validation` basculer.</span><span class="sxs-lookup"><span data-stu-id="51e7b-121">Since hello default deployment uses a self-signed certificate, you should also include hello `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="51e7b-122">Vous êtes invité à toolog dans toohello contrôleur de Cloud.</span><span class="sxs-lookup"><span data-stu-id="51e7b-122">You are prompted toolog in toohello Cloud Controller.</span></span> <span data-ttu-id="51e7b-123">Utilisez hello admin informations d’identification que vous avez obtenue à partir des étapes de déploiement hello marketplace.</span><span class="sxs-lookup"><span data-stu-id="51e7b-123">Use hello admin account credentials that you acquired from hello marketplace deployment steps.</span></span>

<span data-ttu-id="51e7b-124">Cloud Foundry fournit *les organisations* et *espaces* en tant que les équipes de hello tooisolate espaces de noms et des environnements au sein d’un déploiement partagé.</span><span class="sxs-lookup"><span data-stu-id="51e7b-124">Cloud Foundry provides *orgs* and *spaces* as namespaces tooisolate hello teams and environments within a shared deployment.</span></span> <span data-ttu-id="51e7b-125">Hello déploiement de marketplace PCF inclut par défaut de hello *système* org et un ensemble d’espaces créé toocontain des composants de base hello, telles que le service d’échelle hello et service broker de service Azure hello.</span><span class="sxs-lookup"><span data-stu-id="51e7b-125">hello PCF marketplace deployment includes hello default *system* org and a set of spaces created toocontain hello base components, like hello autoscaling service and hello Azure service broker.</span></span> <span data-ttu-id="51e7b-126">Pour l’instant, choisissez hello *système* espace.</span><span class="sxs-lookup"><span data-stu-id="51e7b-126">For now, choose hello *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="51e7b-127">Création d’une organisation et d’un espace</span><span class="sxs-lookup"><span data-stu-id="51e7b-127">Create an org and space</span></span>

<span data-ttu-id="51e7b-128">Si vous tapez `cf apps`, vous voyez un ensemble d’applications de système qui ont été déployés dans l’espace de système de hello dans hello, système org.</span><span class="sxs-lookup"><span data-stu-id="51e7b-128">If you type `cf apps`, you see a set of system applications that have been deployed in hello system space within hello system org.</span></span> 

<span data-ttu-id="51e7b-129">Vous devez conserver hello *système* org réservé pour les applications du système, créez un toohouse org et espace notre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="51e7b-129">You should keep hello *system* org reserved for system applications, so create an org and space toohouse our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="51e7b-130">Utilisez hello cible commande tooswitch toohello nouvelle organisation et l’espace :</span><span class="sxs-lookup"><span data-stu-id="51e7b-130">Use hello target command tooswitch toohello new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="51e7b-131">Désormais, lorsque vous déployez une application, il est automatiquement créé dans l’espace et d’organisation nouvelle hello.</span><span class="sxs-lookup"><span data-stu-id="51e7b-131">Now, when you deploy an application, it is automatically created in hello new org and space.</span></span> <span data-ttu-id="51e7b-132">ne type de tooconfirm il n’y a aucune application dans l’espace/hello nouvelle organisation, `cf apps` à nouveau.</span><span class="sxs-lookup"><span data-stu-id="51e7b-132">tooconfirm that there are currently no apps in hello new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="51e7b-133">Pour plus d’informations sur les organisations et des espaces et comment elles peuvent être utilisées pour le contrôle d’accès basé sur un rôle (RBAC), consultez hello [documentation du Cloud Foundry][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="51e7b-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see hello [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="51e7b-134">Déployer une application</span><span class="sxs-lookup"><span data-stu-id="51e7b-134">Deploy an application</span></span>

<span data-ttu-id="51e7b-135">Nous allons utiliser un exemple d’application Cloud Foundry appelée Hello ressort Cloud, ce qui est écrit en Java et en fonction de hello [Spring Framework](http://spring.io) et [ressort démarrage](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="51e7b-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on hello [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-hello-hello-spring-cloud-repository"></a><span data-ttu-id="51e7b-136">Cloner le référentiel de Hello ressort Cloud hello</span><span class="sxs-lookup"><span data-stu-id="51e7b-136">Clone hello Hello Spring Cloud repository</span></span>

<span data-ttu-id="51e7b-137">Hello, exemple d’application Hello ressort Cloud est disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="51e7b-137">hello Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="51e7b-138">Cloner tooyour environnement et les modifier dans le répertoire hello :</span><span class="sxs-lookup"><span data-stu-id="51e7b-138">Clone it tooyour environment and change into hello new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a><span data-ttu-id="51e7b-139">Générez l’application hello</span><span class="sxs-lookup"><span data-stu-id="51e7b-139">Build hello application</span></span>

<span data-ttu-id="51e7b-140">À l’aide de build hello application [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="51e7b-140">Build hello app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a><span data-ttu-id="51e7b-141">Déployer l’application hello avec cf push</span><span class="sxs-lookup"><span data-stu-id="51e7b-141">Deploy hello application with cf push</span></span>

<span data-ttu-id="51e7b-142">Vous pouvez déployer la plupart des applications tooCloud Foundry à l’aide de hello `push` commande :</span><span class="sxs-lookup"><span data-stu-id="51e7b-142">You can deploy most applications tooCloud Foundry using hello `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="51e7b-143">Lorsque vous *push* une application Cloud Foundry détecte le type de hello d’application (dans ce cas, une application Java) et identifie ses dépendances (dans ce cas, framework de ressort hello).</span><span class="sxs-lookup"><span data-stu-id="51e7b-143">When you *push* an application, Cloud Foundry detects hello type of application (in this case, a Java app) and identifies its dependencies (in this case, hello Spring framework).</span></span> <span data-ttu-id="51e7b-144">Ensuite, il empaquète tous les éléments requis toorun votre code dans une image de conteneur autonome, appelée un *GOUTTELETTES*.</span><span class="sxs-lookup"><span data-stu-id="51e7b-144">It then packages everything required toorun your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="51e7b-145">Enfin, les planifications de Cloud Foundry hello application sur l’un des ordinateurs dans votre environnement hello et crée une URL où vous pouvez l’atteindre, qui est disponible dans la sortie de hello de commande hello.</span><span class="sxs-lookup"><span data-stu-id="51e7b-145">Finally, Cloud Foundry schedules hello application on one of hello available machines in your environment and creates a URL where you can reach it, which is available in hello output of hello command.</span></span>

![Sortie de la commande cf push][cf-push-output]

<span data-ttu-id="51e7b-147">application de toosee hello hello-spring-cloud, URL ouverte hello fourni dans votre navigateur :</span><span class="sxs-lookup"><span data-stu-id="51e7b-147">toosee hello hello-spring-cloud application, open hello provided URL in your browser:</span></span>

![Interface utilisateur par défaut pour Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="51e7b-149">toolearn plus d’informations sur le déroulement de `cf push`, consultez [comment les Applications sont transférées] [ cf-push-docs] Bonjour documentation de Cloud Foundry.</span><span class="sxs-lookup"><span data-stu-id="51e7b-149">toolearn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in hello Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="51e7b-150">Affichage des journaux des applications</span><span class="sxs-lookup"><span data-stu-id="51e7b-150">View application logs</span></span>

<span data-ttu-id="51e7b-151">Vous pouvez utiliser les journaux de tooview hello Cloud Foundry CLI pour une application par son nom :</span><span class="sxs-lookup"><span data-stu-id="51e7b-151">You can use hello Cloud Foundry CLI tooview logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="51e7b-152">Par défaut, hello enregistre la commande utilise *fin*, qui montre les nouveaux journaux qu’ils sont écrits.</span><span class="sxs-lookup"><span data-stu-id="51e7b-152">By default, hello logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="51e7b-153">toosee nouveaux journaux apparaissent, actualiser application hello-spring-cloud de hello dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="51e7b-153">toosee new logs appear, refresh hello hello-spring-cloud app in hello browser.</span></span>

<span data-ttu-id="51e7b-154">ajouter des journaux tooview qui ont déjà été écrits, hello `recent` commutateur :</span><span class="sxs-lookup"><span data-stu-id="51e7b-154">tooview logs that have already been written, add hello `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a><span data-ttu-id="51e7b-155">Application hello de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="51e7b-155">Scale hello application</span></span>

<span data-ttu-id="51e7b-156">Par défaut, la commande `cf push` crée une seule instance de votre application.</span><span class="sxs-lookup"><span data-stu-id="51e7b-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="51e7b-157">tooensure haute disponibilité et activer montée en puissance parallèle pour un débit plus élevé, vous voulez généralement que toorun, et plusieurs instances de vos applications.</span><span class="sxs-lookup"><span data-stu-id="51e7b-157">tooensure high availability and enable scale out for higher throughput, you generally want toorun more than one instance of your applications.</span></span> <span data-ttu-id="51e7b-158">Vous pouvez faire évoluer facilement des applications déjà déployées à l’aide de hello `scale` commande :</span><span class="sxs-lookup"><span data-stu-id="51e7b-158">You can easily scale out already deployed applications using hello `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="51e7b-159">En cours d’exécution hello `cf app` commande sur l’application hello montre que Cloud Foundry crée une autre instance de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="51e7b-159">Running hello `cf app` command on hello application shows that Cloud Foundry is creating another instance of hello application.</span></span> <span data-ttu-id="51e7b-160">Une fois démarrée, application hello Cloud Foundry démarre automatiquement tooit de trafic d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="51e7b-160">Once hello application has started, Cloud Foundry automatically starts load balancing traffic tooit.</span></span>


## <a name="next-steps"></a><span data-ttu-id="51e7b-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51e7b-161">Next steps</span></span>

- <span data-ttu-id="51e7b-162">[Hello de lecture documentation de Cloud Foundry][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="51e7b-162">[Read hello Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="51e7b-163">[Configurer les plug-in de Visual Studio Team Services hello pour Cloud Foundry][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="51e7b-163">[Set up hello Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="51e7b-164">[Configurer hello buse d’Analytique de journal de Microsoft pour le Cloud Foundry][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="51e7b-164">[Configure hello Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png