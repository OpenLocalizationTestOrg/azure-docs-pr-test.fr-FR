---
title: "aaaGetting démarré avec Foundry Cloud sur Microsoft Azure | Documents Microsoft"
description: "Exécuter OSS ou Pivotal Cloud Foundry sur Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a>Cloud Foundry sur Azure

Cloud Foundry est une solution de type plate-forme en tant que service (PaaS) open source pour la génération, le déploiement et l’exploitation d’applications 12 facteurs développées dans plusieurs langages et infrastructures. Ce document décrit les options hello pour Cloud Foundry en cours d’exécution sur Azure et comment vous pouvez commencer.

## <a name="cloud-foundry-offerings"></a>Offres Cloud Foundry

Il existe deux formes de Cloud Foundry de toorun disponible sur Azure : Cloud Foundry (CF OSS) et le pivot Cloud Foundry (PCF) open source. Systèmes d’exploitation CF est un entièrement [open source](https://github.com/cloudfoundry) version de Cloud géré par hello Cloud Foundry Foundation. Pivot Foundry de Cloud est une distribution de l’entreprise de Cloud de pivot Software Inc. Nous examinons quelques-unes des différences de hello entre les deux offres de hello.

### <a name="open-source-cloud-foundry"></a>Cloud Foundry open source

Vous pouvez déployer Foundry de Cloud de systèmes d’exploitation sur Azure en premier déploiement d’un directeur de BOSH et de déploiement Cloud Foundry, à l’aide de hello [instructions fournies sur GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md). toolearn plus sur l’utilisation de systèmes d’exploitation CF, consultez hello [documentation](https://docs.cloudfoundry.org/) fournie par hello Cloud Foundry Foundation.

Microsoft prend en charge meilleur effort OSS CF via hello suivant des canaux de la Communauté :

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a>Canal bosh-azure-cpi sur [Cloud Foundry Slack](https://slack.cloudfoundry.org/)
- [Liste de diffusion cf-bosh](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- Problèmes de GitHub pour hello [IPC](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) et [broker de service](https://github.com/Azure/meta-azure-service-broker/issues)

>[!NOTE]
> niveau de Hello de prise en charge pour vos ressources Azure, telles que des ordinateurs virtuels de hello sur lequel vous exécutez Foundry du Cloud, est basé sur votre contrat de support Azure. Prise en charge de la Communauté de mieux s’applique uniquement à des composants toohello Foundry propres au Cloud.

### <a name="pivotal-cloud-foundry"></a>Pivotal Cloud Foundry

Pivot Cloud Foundry inclut hello même plate-forme de base en tant que distribution hello OSS, ainsi qu’un ensemble d’outils de gestion et de prise en charge de l’entreprise. toorun PCF sur Azure, vous devez acheter une licence à partir de Pivotal. proposer PCF Hello hello Azure marketplace inclut une licence d’évaluation de 90 jours.

Hello, citons [pivot Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), une application web qui simplifie le déploiement et la gestion d’une Fondation Foundry du Cloud, et [pivot applications Manager](https://docs.pivotal.io/pivotalcf/console/), une application web de gestion les utilisateurs et applications.

En outre les canaux de support toohello répertoriés pour CF OSS ci-dessus, une licence PCF donne droit vous toocontact Pivotal pour la prise en charge. Microsoft et Pivotal ont également activé des parties d’assistance prise en charge des flux de travail qui vous permettre de toocontact et votre demande de router correctement selon où se trouve le problème de hello.

## <a name="azure-service-broker"></a>Azure Service Broker

Cloud Foundry encourage hello [« facteur de douze app »](https://12factor.net/) méthodologie, ce qui favorise une séparation nette de processus d’application sans état et avec état de la sauvegarde des services. [Service courtiers](https://docs.cloudfoundry.org/services/api.html) offrent une moyen cohérent de tooprovision et lier tooapplications des services de stockage. Hello [broker de service Azure](https://github.com/Azure/meta-azure-service-broker) certaines hello propose des principaux services Azure via ce canal, y compris le stockage Azure et SQL Azure.

Si vous utilisez pivot Cloud Foundry, service broker de service hello est également [disponible sous forme de vignette](https://docs.pivotal.io/azure-sb/installing.html) de hello réseau pivot.

## <a name="related-resources"></a>Ressources associées

### <a name="visual-studio-team-services-plugin"></a>Plug-in Visual Studio Team Services

Cloud Foundry est parfaitement tooagile développement de logiciels, y compris l’utilisation de hello d’intégration continue (CI) et de livraison continue (CD). Si vous utilisez Visual Studio Team Services (VSTS) toomanage vos projets et que vous aimeriez tooset un pipeline de l’élément de configuration/CD ciblage Foundry du Cloud, vous pouvez utiliser hello [extension de génération VSTS Cloud Foundry](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension). rend simple tooconfigure Hello plug-in et automatiser les déploiements tooCloud Foundry, qu’il s’exécute dans Azure ou un autre environnement.

## <a name="next-steps"></a>Étapes suivantes

- [Déployer pivot Cloud Foundry de hello Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [Déployer une application de tooCloud Foundry dans Azure](./cloudfoundry-deploy-your-first-app.md)
