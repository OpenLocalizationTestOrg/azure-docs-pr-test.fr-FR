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
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a>Déployer votre premier tooCloud d’application Foundry sur Microsoft Azure

[Cloud Foundry](http://cloudfoundry.org) est une plateforme d’applications open source populaire disponible sur Microsoft Azure. Dans cet article, nous montrons comment toodeploy et gérer une application sur le Cloud Foundry dans un environnement Windows Azure.

## <a name="create-a-cloud-foundry-environment"></a>Création d’un environnement Cloud Foundry

Il existe plusieurs façons de créer un environnement Cloud Foundry sur Azure :

- Hello d’utilisation [offre de pivot Cloud Foundry] [ pcf-azuremarketplace] dans Azure Marketplace de hello toocreate un environnement standard qui inclut PCF Operations Manager et hello Azure Service Broker. Vous pouvez trouver [instructions complètes] [ pcf-azuremarketplace-pivotaldocs] pour le déploiement de marketplace de hello proposer dans hello documentation pivot.
- Créez un environnement personnalisé en [déployant manuellement Pivotal Cloud Foundry][pcf-custom].
- [Déployer des packages de Cloud Foundry hello open source directement] [ oss-cf-bosh] en configurant un [BOSH](http://bosh.io) directeur, une machine virtuelle qui coordonne déploiement hello d’environnement de Cloud Foundry hello.

> [!IMPORTANT] 
> Si vous déployez PCF de hello Azure Marketplace, prenez note de hello SYSTEMDOMAINURL et informations d’identification d’administrateur de hello nécessaire tooaccess hello pivot Gestionnaire d’applications, qui sont décrites dans le guide de déploiement hello marketplace. Ils est nécessaire toocomplete ce didacticiel. Pour les déploiements de marketplace, hello SYSTEMDOMAINURL est hello formulaire https://system. *-adresse ip*. cf.pcfazure.com.

## <a name="connect-toohello-cloud-controller"></a>Se connecter toohello contrôleur de Cloud

Hello contrôleur de Cloud est environnement de Cloud Foundry point tooa hello entrée de serveur principal pour le déploiement et la gestion des applications. le cœur de Hello API de contrôleur de Cloud (CCAPI) est une API REST, mais il est accessible via différents outils. Dans ce cas, vous interagissez avec elle via hello [Cloud Foundry CLI][cf-cli]. Vous pouvez installer hello CLI sur Linux, Mac OS ou Windows, mais si vous préférez pas les tooinstall il, il est disponible préinstallé Bonjour [Azure Cloud Shell][cloudshell-docs].

toolog, ajouter `api` toohello SYSTEMDOMAINURL que vous avez obtenue à partir de déploiement de marketplace hello. Étant donné que le déploiement par défaut de hello utilise un certificat auto-signé, vous devez également inclure hello `skip-ssl-validation` basculer.

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

Vous êtes invité à toolog dans toohello contrôleur de Cloud. Utilisez hello admin informations d’identification que vous avez obtenue à partir des étapes de déploiement hello marketplace.

Cloud Foundry fournit *les organisations* et *espaces* en tant que les équipes de hello tooisolate espaces de noms et des environnements au sein d’un déploiement partagé. Hello déploiement de marketplace PCF inclut par défaut de hello *système* org et un ensemble d’espaces créé toocontain des composants de base hello, telles que le service d’échelle hello et service broker de service Azure hello. Pour l’instant, choisissez hello *système* espace.


## <a name="create-an-org-and-space"></a>Création d’une organisation et d’un espace

Si vous tapez `cf apps`, vous voyez un ensemble d’applications de système qui ont été déployés dans l’espace de système de hello dans hello, système org. 

Vous devez conserver hello *système* org réservé pour les applications du système, créez un toohouse org et espace notre exemple d’application.

```bash
cf create-org myorg
cf create-space dev -o myorg
```

Utilisez hello cible commande tooswitch toohello nouvelle organisation et l’espace :

```bash
cf target -o testorg -s dev
```

Désormais, lorsque vous déployez une application, il est automatiquement créé dans l’espace et d’organisation nouvelle hello. ne type de tooconfirm il n’y a aucune application dans l’espace/hello nouvelle organisation, `cf apps` à nouveau.

> [!NOTE] 
> Pour plus d’informations sur les organisations et des espaces et comment elles peuvent être utilisées pour le contrôle d’accès basé sur un rôle (RBAC), consultez hello [documentation du Cloud Foundry][cf-orgs-spaces-docs].

## <a name="deploy-an-application"></a>Déployer une application

Nous allons utiliser un exemple d’application Cloud Foundry appelée Hello ressort Cloud, ce qui est écrit en Java et en fonction de hello [Spring Framework](http://spring.io) et [ressort démarrage](http://projects.spring.io/spring-boot/).

### <a name="clone-hello-hello-spring-cloud-repository"></a>Cloner le référentiel de Hello ressort Cloud hello

Hello, exemple d’application Hello ressort Cloud est disponible sur GitHub. Cloner tooyour environnement et les modifier dans le répertoire hello :

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a>Générez l’application hello

À l’aide de build hello application [Apache Maven](http://maven.apache.org).

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a>Déployer l’application hello avec cf push

Vous pouvez déployer la plupart des applications tooCloud Foundry à l’aide de hello `push` commande :

```bash
cf push
```

Lorsque vous *push* une application Cloud Foundry détecte le type de hello d’application (dans ce cas, une application Java) et identifie ses dépendances (dans ce cas, framework de ressort hello). Ensuite, il empaquète tous les éléments requis toorun votre code dans une image de conteneur autonome, appelée un *GOUTTELETTES*. Enfin, les planifications de Cloud Foundry hello application sur l’un des ordinateurs dans votre environnement hello et crée une URL où vous pouvez l’atteindre, qui est disponible dans la sortie de hello de commande hello.

![Sortie de la commande cf push][cf-push-output]

application de toosee hello hello-spring-cloud, URL ouverte hello fourni dans votre navigateur :

![Interface utilisateur par défaut pour Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> toolearn plus d’informations sur le déroulement de `cf push`, consultez [comment les Applications sont transférées] [ cf-push-docs] Bonjour documentation de Cloud Foundry.

## <a name="view-application-logs"></a>Affichage des journaux des applications

Vous pouvez utiliser les journaux de tooview hello Cloud Foundry CLI pour une application par son nom :

```bash
cf logs hello-spring-cloud
```

Par défaut, hello enregistre la commande utilise *fin*, qui montre les nouveaux journaux qu’ils sont écrits. toosee nouveaux journaux apparaissent, actualiser application hello-spring-cloud de hello dans le navigateur de hello.

ajouter des journaux tooview qui ont déjà été écrits, hello `recent` commutateur :

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a>Application hello de mise à l’échelle

Par défaut, la commande `cf push` crée une seule instance de votre application. tooensure haute disponibilité et activer montée en puissance parallèle pour un débit plus élevé, vous voulez généralement que toorun, et plusieurs instances de vos applications. Vous pouvez faire évoluer facilement des applications déjà déployées à l’aide de hello `scale` commande :

```bash
cf scale -i 2 hello-spring-cloud
```

En cours d’exécution hello `cf app` commande sur l’application hello montre que Cloud Foundry crée une autre instance de l’application hello. Une fois démarrée, application hello Cloud Foundry démarre automatiquement tooit de trafic d’équilibrage de charge.


## <a name="next-steps"></a>Étapes suivantes

- [Hello de lecture documentation de Cloud Foundry][cloudfoundry-docs]
- [Configurer les plug-in de Visual Studio Team Services hello pour Cloud Foundry][vsts-plugin]
- [Configurer hello buse d’Analytique de journal de Microsoft pour le Cloud Foundry][loganalytics-nozzle]

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