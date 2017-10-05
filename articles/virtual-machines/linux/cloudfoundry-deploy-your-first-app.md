---
title: "Déployer votre première application dans Cloud Foundry sur Microsoft Azure | Microsoft Docs"
description: "Déployer une application dans Cloud Foundry sur Azure"
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
ms.openlocfilehash: b617127fc0a3f8dcae293e356ea669edcfa5deff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-your-first-app-to-cloud-foundry-on-microsoft-azure"></a><span data-ttu-id="2c525-103">Déployer votre première application dans Cloud Foundry sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2c525-103">Deploy your first app to Cloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="2c525-104">[Cloud Foundry](http://cloudfoundry.org) est une plateforme d’applications open source populaire disponible sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2c525-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="2c525-105">Dans cet article, nous montrons comment déployer et gérer une application dans Cloud Foundry dans un environnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2c525-105">In this article, we show how to deploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="2c525-106">Création d’un environnement Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="2c525-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="2c525-107">Il existe plusieurs façons de créer un environnement Cloud Foundry sur Azure :</span><span class="sxs-lookup"><span data-stu-id="2c525-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="2c525-108">Utilisez [l’offre Pivotal Cloud Foundry][pcf-azuremarketplace] disponible sur la Place de marché Microsoft Azure pour créer un environnement standard qui inclut PCF Ops Manager et Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="2c525-108">Use the [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in the Azure Marketplace to create a standard environment that includes PCF Ops Manager and the Azure Service Broker.</span></span> <span data-ttu-id="2c525-109">Vous trouverez des [instructions complètes][pcf-azuremarketplace-pivotaldocs] pour déployer l’offre de la Place de marché dans la documentation Pivotal.</span><span class="sxs-lookup"><span data-stu-id="2c525-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying the marketplace offer in the Pivotal documentation.</span></span>
- <span data-ttu-id="2c525-110">Créez un environnement personnalisé en [déployant manuellement Pivotal Cloud Foundry][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="2c525-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="2c525-111">[Déployez les packages open source Cloud Foundry directement][oss-cf-bosh] en configurant un directeur [BOSH](http://bosh.io) (une machine virtuelle qui coordonne le déploiement de l’environnement Cloud Foundry).</span><span class="sxs-lookup"><span data-stu-id="2c525-111">[Deploy the open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates the deployment of the Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2c525-112">Si vous déployez PCF à partir de la Place de marché Microsoft Azure, notez l’URL SYSTEMDOMAINURL et les informations d’identification administrateur requises pour accéder à Pivotal Apps Manager. Elles sont décrites dans le guide de déploiement de la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="2c525-112">If you are deploying PCF from the Azure Marketplace, make a note of the SYSTEMDOMAINURL and the admin credentials required to access the Pivotal Apps Manager, both of which are described in the marketplace deployment guide.</span></span> <span data-ttu-id="2c525-113">Elles sont nécessaires pour suivre ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2c525-113">They are needed to complete this tutorial.</span></span> <span data-ttu-id="2c525-114">Pour les déploiements de la Place de marché, l’URL SYSTEMDOMAINURL se présente sous la forme https://system.*adresse-ip*.cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="2c525-114">For marketplace deployments, the SYSTEMDOMAINURL is in the form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-to-the-cloud-controller"></a><span data-ttu-id="2c525-115">Connexion au Cloud Controller</span><span class="sxs-lookup"><span data-stu-id="2c525-115">Connect to the Cloud Controller</span></span>

<span data-ttu-id="2c525-116">Le Cloud Controller est le point d’entrée principal vers un environnement Cloud Foundry pour déployer et gérer des applications.</span><span class="sxs-lookup"><span data-stu-id="2c525-116">The Cloud Controller is the primary entry point to a Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="2c525-117">L’API principale du Cloud Controller (CCAPI) est une API REST, mais elle est accessible par le biais de différents outils.</span><span class="sxs-lookup"><span data-stu-id="2c525-117">The core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="2c525-118">Dans le cas présent, nous interagissons avec cette API par le biais de [l’interface CLI Cloud Foundry][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="2c525-118">In this case, we interact with it through the [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="2c525-119">Vous pouvez installer l’interface CLI sur Linux, MacOS ou Windows, mais si vous préférez ne pas l’installer, elle est disponible en version pré-installée dans [Azure Cloud Shell][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="2c525-119">You can install the CLI on Linux, MacOS, or Windows, but if you'd prefer not to install it at all, it is available pre-installed in the [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="2c525-120">Pour vous connecter, ajoutez le préfixe `api` à l’URL SYSTEMDOMAINURL que vous avez obtenue à partir du déploiement de la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="2c525-120">To log in, prepend `api` to the SYSTEMDOMAINURL that you obtained from the marketplace deployment.</span></span> <span data-ttu-id="2c525-121">Étant donné que le déploiement par défaut utilise un certificat auto-signé, vous devez également inclure le commutateur `skip-ssl-validation`.</span><span class="sxs-lookup"><span data-stu-id="2c525-121">Since the default deployment uses a self-signed certificate, you should also include the `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="2c525-122">Vous êtes invité à vous connecter au Cloud Controller.</span><span class="sxs-lookup"><span data-stu-id="2c525-122">You are prompted to log in to the Cloud Controller.</span></span> <span data-ttu-id="2c525-123">Utilisez les informations d’identification du compte Administrateur que vous avez obtenues à partir de la procédure de déploiement de la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="2c525-123">Use the admin account credentials that you acquired from the marketplace deployment steps.</span></span>

<span data-ttu-id="2c525-124">Cloud Foundry fournit les *organisations* et *espaces* en tant qu’espaces de noms pour isoler les équipes et les environnements dans un déploiement partagé.</span><span class="sxs-lookup"><span data-stu-id="2c525-124">Cloud Foundry provides *orgs* and *spaces* as namespaces to isolate the teams and environments within a shared deployment.</span></span> <span data-ttu-id="2c525-125">Le déploiement de Place de marché de PCF inclut l’organisation *système* par défaut et un ensemble d’espaces créés pour contenir les composants de base, notamment le service de mise à l’échelle automatique et Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="2c525-125">The PCF marketplace deployment includes the default *system* org and a set of spaces created to contain the base components, like the autoscaling service and the Azure service broker.</span></span> <span data-ttu-id="2c525-126">Pour l’instant, choisissez l’espace *système*.</span><span class="sxs-lookup"><span data-stu-id="2c525-126">For now, choose the *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="2c525-127">Création d’une organisation et d’un espace</span><span class="sxs-lookup"><span data-stu-id="2c525-127">Create an org and space</span></span>

<span data-ttu-id="2c525-128">Si vous tapez `cf apps`, vous voyez un ensemble d’applications système qui ont été déployées dans l’espace système au sein de l’organisation système.</span><span class="sxs-lookup"><span data-stu-id="2c525-128">If you type `cf apps`, you see a set of system applications that have been deployed in the system space within the system org.</span></span> 

<span data-ttu-id="2c525-129">Comme vous devez réserver l’organisation *système* aux applications système, créez une organisation et un espace pour accueillir notre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="2c525-129">You should keep the *system* org reserved for system applications, so create an org and space to house our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="2c525-130">Utilisez la commande target pour basculer vers la nouvelle organisation et le nouvel espace :</span><span class="sxs-lookup"><span data-stu-id="2c525-130">Use the target command to switch to the new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="2c525-131">Désormais, lorsque vous déployez une application, elle est automatiquement créée dans la nouvelle organisation et le nouvel espace.</span><span class="sxs-lookup"><span data-stu-id="2c525-131">Now, when you deploy an application, it is automatically created in the new org and space.</span></span> <span data-ttu-id="2c525-132">Pour vérifier qu’il n’existe actuellement aucune application dans la nouvelle organisation/le nouvel espace, tapez `cf apps` à nouveau.</span><span class="sxs-lookup"><span data-stu-id="2c525-132">To confirm that there are currently no apps in the new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="2c525-133">Pour plus d’informations sur les organisations et les espaces et sur la façon dont ils peuvent être utilisés pour le contrôle d’accès en fonction du rôle (RBAC, role-based access control), consultez la [documentation Cloud Foundry][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="2c525-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see the [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="2c525-134">Déployer une application</span><span class="sxs-lookup"><span data-stu-id="2c525-134">Deploy an application</span></span>

<span data-ttu-id="2c525-135">Nous allons utiliser un exemple d’application Cloud Foundry appelée Hello Spring Cloud. Cette application est écrite en langage Java et basée sur le [Spring Framework](http://spring.io) et le [Spring Boot](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="2c525-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on the [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-the-hello-spring-cloud-repository"></a><span data-ttu-id="2c525-136">Clonage du référentiel Hello Spring Cloud</span><span class="sxs-lookup"><span data-stu-id="2c525-136">Clone the Hello Spring Cloud repository</span></span>

<span data-ttu-id="2c525-137">L’exemple d’application Hello Spring Cloud est disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="2c525-137">The Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="2c525-138">Clonez-la dans votre environnement et basculez vers le nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="2c525-138">Clone it to your environment and change into the new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-the-application"></a><span data-ttu-id="2c525-139">Création de l'application</span><span class="sxs-lookup"><span data-stu-id="2c525-139">Build the application</span></span>

<span data-ttu-id="2c525-140">Générez l’application à l’aide [d’Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="2c525-140">Build the app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-the-application-with-cf-push"></a><span data-ttu-id="2c525-141">Déploiement de l’application avec la commande cf push</span><span class="sxs-lookup"><span data-stu-id="2c525-141">Deploy the application with cf push</span></span>

<span data-ttu-id="2c525-142">Vous pouvez déployer la plupart des applications dans Cloud Foundry à l’aide de la commande `push` :</span><span class="sxs-lookup"><span data-stu-id="2c525-142">You can deploy most applications to Cloud Foundry using the `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="2c525-143">Lorsque vous utilisez la méthode *push* pour une application, Cloud Foundry détecte le type d’application (dans ce cas, une application Java) et identifie ses dépendances (dans ce cas, Spring Framework).</span><span class="sxs-lookup"><span data-stu-id="2c525-143">When you *push* an application, Cloud Foundry detects the type of application (in this case, a Java app) and identifies its dependencies (in this case, the Spring framework).</span></span> <span data-ttu-id="2c525-144">Ensuite, il empaquette tous les éléments requis pour exécuter votre code dans une image de conteneur autonome, appelée *gouttelette*.</span><span class="sxs-lookup"><span data-stu-id="2c525-144">It then packages everything required to run your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="2c525-145">Enfin, Cloud Foundry planifie l’application sur l’une des machines disponibles dans votre environnement et crée une URL vous permettant d’y accéder, disponible dans la sortie de la commande.</span><span class="sxs-lookup"><span data-stu-id="2c525-145">Finally, Cloud Foundry schedules the application on one of the available machines in your environment and creates a URL where you can reach it, which is available in the output of the command.</span></span>

![Sortie de la commande cf push][cf-push-output]

<span data-ttu-id="2c525-147">Pour afficher l’application hello-spring-cloud, ouvrez l’URL fournie dans votre navigateur :</span><span class="sxs-lookup"><span data-stu-id="2c525-147">To see the hello-spring-cloud application, open the provided URL in your browser:</span></span>

![Interface utilisateur par défaut pour Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="2c525-149">Pour plus d’informations sur les effets de la commande `cf push`, consultez [How Applications Are Staged][cf-push-docs] (Indexation des applications) dans la documentation Cloud Foundry.</span><span class="sxs-lookup"><span data-stu-id="2c525-149">To learn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in the Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="2c525-150">Affichage des journaux des applications</span><span class="sxs-lookup"><span data-stu-id="2c525-150">View application logs</span></span>

<span data-ttu-id="2c525-151">Vous pouvez utiliser l’interface CLI de Cloud Foundry pour afficher les journaux d’une application par son nom :</span><span class="sxs-lookup"><span data-stu-id="2c525-151">You can use the Cloud Foundry CLI to view logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="2c525-152">Par défaut, la commande logs utilise une *fin*, qui montre les nouveaux journaux à mesure qu’ils sont écrits.</span><span class="sxs-lookup"><span data-stu-id="2c525-152">By default, the logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="2c525-153">Pour afficher les nouveaux journaux, actualisez l’application hello-spring-cloud dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="2c525-153">To see new logs appear, refresh the hello-spring-cloud app in the browser.</span></span>

<span data-ttu-id="2c525-154">Pour afficher les journaux déjà écrits, ajoutez le commutateur `recent` :</span><span class="sxs-lookup"><span data-stu-id="2c525-154">To view logs that have already been written, add the `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-the-application"></a><span data-ttu-id="2c525-155">Mise à l’échelle de l’application</span><span class="sxs-lookup"><span data-stu-id="2c525-155">Scale the application</span></span>

<span data-ttu-id="2c525-156">Par défaut, la commande `cf push` crée une seule instance de votre application.</span><span class="sxs-lookup"><span data-stu-id="2c525-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="2c525-157">Pour garantir une haute disponibilité et permettre l’augmentation de la taille des instances en vue d’accroître le débit, il est courant d’exécuter plusieurs instances de vos applications.</span><span class="sxs-lookup"><span data-stu-id="2c525-157">To ensure high availability and enable scale out for higher throughput, you generally want to run more than one instance of your applications.</span></span> <span data-ttu-id="2c525-158">Vous pouvez facilement augmenter la taille des instances des applications déjà déployées à l’aide de la commande `scale` :</span><span class="sxs-lookup"><span data-stu-id="2c525-158">You can easily scale out already deployed applications using the `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="2c525-159">L’exécution de la commande `cf app` sur l’application montre que Cloud Foundry crée une autre instance de l’application.</span><span class="sxs-lookup"><span data-stu-id="2c525-159">Running the `cf app` command on the application shows that Cloud Foundry is creating another instance of the application.</span></span> <span data-ttu-id="2c525-160">Une fois l’application démarrée, Cloud Foundry démarre automatiquement l’équilibrage de la charge du trafic sur l’application.</span><span class="sxs-lookup"><span data-stu-id="2c525-160">Once the application has started, Cloud Foundry automatically starts load balancing traffic to it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2c525-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2c525-161">Next steps</span></span>

- <span data-ttu-id="2c525-162">[Lisez la documentation Cloud Foundry][cloudfoundry-docs].</span><span class="sxs-lookup"><span data-stu-id="2c525-162">[Read the Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="2c525-163">[Configurez le plug-in Visual Studio Team Services pour Cloud Foundry][vsts-plugin].</span><span class="sxs-lookup"><span data-stu-id="2c525-163">[Set up the Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="2c525-164">[Configurez l’injecteur Microsoft Log Analytics pour Cloud Foundry][loganalytics-nozzle].</span><span class="sxs-lookup"><span data-stu-id="2c525-164">[Configure the Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

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