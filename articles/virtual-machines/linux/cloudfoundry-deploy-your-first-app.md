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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="deploy-your-first-app-to-cloud-foundry-on-microsoft-azure"></a>Déployer votre première application dans Cloud Foundry sur Microsoft Azure

[Cloud Foundry](http://cloudfoundry.org) est une plateforme d’applications open source populaire disponible sur Microsoft Azure. Dans cet article, nous montrons comment déployer et gérer une application dans Cloud Foundry dans un environnement Azure.

## <a name="create-a-cloud-foundry-environment"></a>Création d’un environnement Cloud Foundry

Il existe plusieurs façons de créer un environnement Cloud Foundry sur Azure :

- Utilisez [l’offre Pivotal Cloud Foundry][pcf-azuremarketplace] disponible sur la Place de marché Microsoft Azure pour créer un environnement standard qui inclut PCF Ops Manager et Azure Service Broker. Vous trouverez des [instructions complètes][pcf-azuremarketplace-pivotaldocs] pour déployer l’offre de la Place de marché dans la documentation Pivotal.
- Créez un environnement personnalisé en [déployant manuellement Pivotal Cloud Foundry][pcf-custom].
- [Déployez les packages open source Cloud Foundry directement][oss-cf-bosh] en configurant un directeur [BOSH](http://bosh.io) (une machine virtuelle qui coordonne le déploiement de l’environnement Cloud Foundry).

> [!IMPORTANT] 
> Si vous déployez PCF à partir de la Place de marché Microsoft Azure, notez l’URL SYSTEMDOMAINURL et les informations d’identification administrateur requises pour accéder à Pivotal Apps Manager. Elles sont décrites dans le guide de déploiement de la Place de marché. Elles sont nécessaires pour suivre ce didacticiel. Pour les déploiements de la Place de marché, l’URL SYSTEMDOMAINURL se présente sous la forme https://system.*adresse-ip*.cf.pcfazure.com.

## <a name="connect-to-the-cloud-controller"></a>Connexion au Cloud Controller

Le Cloud Controller est le point d’entrée principal vers un environnement Cloud Foundry pour déployer et gérer des applications. L’API principale du Cloud Controller (CCAPI) est une API REST, mais elle est accessible par le biais de différents outils. Dans le cas présent, nous interagissons avec cette API par le biais de [l’interface CLI Cloud Foundry][cf-cli]. Vous pouvez installer l’interface CLI sur Linux, MacOS ou Windows, mais si vous préférez ne pas l’installer, elle est disponible en version pré-installée dans [Azure Cloud Shell][cloudshell-docs].

Pour vous connecter, ajoutez le préfixe `api` à l’URL SYSTEMDOMAINURL que vous avez obtenue à partir du déploiement de la Place de marché. Étant donné que le déploiement par défaut utilise un certificat auto-signé, vous devez également inclure le commutateur `skip-ssl-validation`.

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

Vous êtes invité à vous connecter au Cloud Controller. Utilisez les informations d’identification du compte Administrateur que vous avez obtenues à partir de la procédure de déploiement de la Place de marché.

Cloud Foundry fournit les *organisations* et *espaces* en tant qu’espaces de noms pour isoler les équipes et les environnements dans un déploiement partagé. Le déploiement de Place de marché de PCF inclut l’organisation *système* par défaut et un ensemble d’espaces créés pour contenir les composants de base, notamment le service de mise à l’échelle automatique et Azure Service Broker. Pour l’instant, choisissez l’espace *système*.


## <a name="create-an-org-and-space"></a>Création d’une organisation et d’un espace

Si vous tapez `cf apps`, vous voyez un ensemble d’applications système qui ont été déployées dans l’espace système au sein de l’organisation système. 

Comme vous devez réserver l’organisation *système* aux applications système, créez une organisation et un espace pour accueillir notre exemple d’application.

```bash
cf create-org myorg
cf create-space dev -o myorg
```

Utilisez la commande target pour basculer vers la nouvelle organisation et le nouvel espace :

```bash
cf target -o testorg -s dev
```

Désormais, lorsque vous déployez une application, elle est automatiquement créée dans la nouvelle organisation et le nouvel espace. Pour vérifier qu’il n’existe actuellement aucune application dans la nouvelle organisation/le nouvel espace, tapez `cf apps` à nouveau.

> [!NOTE] 
> Pour plus d’informations sur les organisations et les espaces et sur la façon dont ils peuvent être utilisés pour le contrôle d’accès en fonction du rôle (RBAC, role-based access control), consultez la [documentation Cloud Foundry][cf-orgs-spaces-docs].

## <a name="deploy-an-application"></a>Déployer une application

Nous allons utiliser un exemple d’application Cloud Foundry appelée Hello Spring Cloud. Cette application est écrite en langage Java et basée sur le [Spring Framework](http://spring.io) et le [Spring Boot](http://projects.spring.io/spring-boot/).

### <a name="clone-the-hello-spring-cloud-repository"></a>Clonage du référentiel Hello Spring Cloud

L’exemple d’application Hello Spring Cloud est disponible sur GitHub. Clonez-la dans votre environnement et basculez vers le nouveau répertoire :

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-the-application"></a>Création de l'application

Générez l’application à l’aide [d’Apache Maven](http://maven.apache.org).

```bash
mvn clean package
```

### <a name="deploy-the-application-with-cf-push"></a>Déploiement de l’application avec la commande cf push

Vous pouvez déployer la plupart des applications dans Cloud Foundry à l’aide de la commande `push` :

```bash
cf push
```

Lorsque vous utilisez la méthode *push* pour une application, Cloud Foundry détecte le type d’application (dans ce cas, une application Java) et identifie ses dépendances (dans ce cas, Spring Framework). Ensuite, il empaquette tous les éléments requis pour exécuter votre code dans une image de conteneur autonome, appelée *gouttelette*. Enfin, Cloud Foundry planifie l’application sur l’une des machines disponibles dans votre environnement et crée une URL vous permettant d’y accéder, disponible dans la sortie de la commande.

![Sortie de la commande cf push][cf-push-output]

Pour afficher l’application hello-spring-cloud, ouvrez l’URL fournie dans votre navigateur :

![Interface utilisateur par défaut pour Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> Pour plus d’informations sur les effets de la commande `cf push`, consultez [How Applications Are Staged][cf-push-docs] (Indexation des applications) dans la documentation Cloud Foundry.

## <a name="view-application-logs"></a>Affichage des journaux des applications

Vous pouvez utiliser l’interface CLI de Cloud Foundry pour afficher les journaux d’une application par son nom :

```bash
cf logs hello-spring-cloud
```

Par défaut, la commande logs utilise une *fin*, qui montre les nouveaux journaux à mesure qu’ils sont écrits. Pour afficher les nouveaux journaux, actualisez l’application hello-spring-cloud dans le navigateur.

Pour afficher les journaux déjà écrits, ajoutez le commutateur `recent` :

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-the-application"></a>Mise à l’échelle de l’application

Par défaut, la commande `cf push` crée une seule instance de votre application. Pour garantir une haute disponibilité et permettre l’augmentation de la taille des instances en vue d’accroître le débit, il est courant d’exécuter plusieurs instances de vos applications. Vous pouvez facilement augmenter la taille des instances des applications déjà déployées à l’aide de la commande `scale` :

```bash
cf scale -i 2 hello-spring-cloud
```

L’exécution de la commande `cf app` sur l’application montre que Cloud Foundry crée une autre instance de l’application. Une fois l’application démarrée, Cloud Foundry démarre automatiquement l’équilibrage de la charge du trafic sur l’application.


## <a name="next-steps"></a>Étapes suivantes

- [Lisez la documentation Cloud Foundry][cloudfoundry-docs].
- [Configurez le plug-in Visual Studio Team Services pour Cloud Foundry][vsts-plugin].
- [Configurez l’injecteur Microsoft Log Analytics pour Cloud Foundry][loganalytics-nozzle].

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