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
# <a name="azure-app-service-web-app-on-linux-faq"></a>FAQ de l’application web Azure App Service sur Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Avec la version hello de l’application Web sur Linux, nous travaillons sur l’ajout de fonctionnalités et de la plateforme de tooour améliorations. Ici sont Forum aux questions (FAQ) que nos clients ont demandé nous sur hello derniers mois.
Si vous avez une question, commentaire sur l’article de hello et nous répondrons il dès que possible.

## <a name="built-in-images"></a>Images prédéfinies

**Q :** je veux toofork hello intégrés conteneurs Docker qui hello plateforme fournit. Où se trouvent ces fichiers ?

**R :** vous trouverez tous les fichiers Docker sur [GitHub](https://github.com/azure-app-service). Vous trouverez tous les conteneurs Docker sur [Docker Hub](https://hub.docker.com/u/appsvc/).

**Q :** quelles sont les valeurs attendues hello pour hello section du fichier de démarrage lors de la configuration de la pile d’exécution hello ?

**R :** pour Node.Js, vous spécifiez au fichier de configuration hello PM2 ou votre fichier de script. Pour .NET Core, vous spécifiez le nom de votre DLL compilée. Pour Ruby, vous pouvez spécifier hello Ruby script que vous souhaitez tooinitialize votre application avec.

## <a name="management"></a>Gestion

**Q :** que se passe-t-il quand je bouton hello redémarrage Bonjour portail Azure ?

**R :** cela est hello équivalents au redémarrage de Docker.

**Q :** puis-je utiliser Secure Shell (SSH) tooconnect toohello application conteneur machine virtuelle (VM) ?

**R :** Oui, vous pouvez effectuer que via le site SCM hello, cocher hello article suivant pour plus d’informations [prise en charge SSH pour l’application Web sur Linux](./app-service-linux-ssh-support.md)

**Q :** je veux toocreate un plan de Service d’applications Linux via le Kit de développement logiciel ou un modèle ARM, comment puis-je effectuer cette opération ?

**R :** vous devez tooset hello `reserved` trop de champs de l’application hello service`true`.

## <a name="continuous-integrationdeployment"></a>Intégration/Déploiement en continu

**Q :** mon application web utilise toujours une ancienne image de conteneur Docker une fois que j’ai mis à jour image hello sur le Hub d’ancrage. Prenez-vous en charge l’intégration continue / le déploiement continu de conteneurs personnalisés ?

**R :** tooset d’intégration/déploiement continu pour les images docker Hub ou de Registre de conteneur Azure par hello de vérification de l’article suivant [déploiement continu avec l’application Web Azure sous Linux](./app-service-linux-ci-cd.md). Pour les registres privés, vous pouvez actualiser le conteneur de hello en arrêtant et avant de démarrer votre application web. Ou vous pouvez modifier ou ajouter une paramètre tooforce une actualisation de votre conteneur d’application factice.

**Q :** Prenez-vous en charge les environnements intermédiaires ?

**R :** Oui.

**Q :** puis-je utiliser **déploiement web** toodeploy mon application web ?

**R :** Oui, vous avez besoin de tooset une application appelé `WEBSITE_WEBDEPLOY_USE_SCM` trop`false`.

## <a name="language-support"></a>Support multilingue

**Q :** Prenez-vous en charge les applications .NET Core non compilées ?

**R :** Oui.

**Q :** Prenez-vous en charge Composer en tant que gestionnaire de dépendances pour les applications PHP ?

**R :** Oui. Lors d’un déploiement Git, Kudu doit détecter que vous déployez une application PHP (Merci de toohello présence d’un fichier composer.json) et déclenchera une installation composer pour vous.

## <a name="custom-containers"></a>Conteneurs personnalisés

**Q :** J’utilise mon propre conteneur personnalisé. Mon application réside dans hello `\home\` active, mais je ne trouvons pas mes fichiers lorsque je parcourir le contenu de hello à l’aide de hello [site SCM](https://github.com/projectkudu/kudu) ou un client FTP. Où sont mes fichiers ?

**R :** nous monter une toohello de partage SMB `\home\` active. Cela remplace tout le contenu qui s’y trouve.

**Q :** J’utilise mon propre conteneur personnalisé. Je ne souhaite pas hello plateforme toomount un toohello de partage SMB `\home\`.

**R :** vous suffit de définition de hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` application aussi un paramètre`false`.

**Q :** mon conteneur personnalisé prend un toostart beaucoup de temps, et la fin de conteneur de hello hello plateforme redémarrage avant son démarrage.

**R :** vous pouvez configurer hello plateforme de hello attendra avant le redémarrage de votre conteneur. Cela est possible en définissant les hello `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello de paramètre d’application de valeur souhaitée en secondes. valeur par défaut Hello est 230 secondes et hello maximale est de 600 secondes.

**Q :** What format hello pour l’url du serveur de Registre privé ?

**R :** vous avez besoin d’y compris les url Registre complet de hello de tooprovide `http://` ou `https://`.

**Q :** What format hello pour le nom de l’image hello dans l’option de Registre privé ?

**R :** vous devez tooadd hello complet nom de l’image, notamment hello Registre privé url (par exemple). myacr.azurecr.io/dotnet:latest)

**Q :** souhaitée tooexpose plusieurs ports sur mon image de conteneur personnalisée. Est-ce possible ?

**R :** Cela n’est actuellement pas pris en charge.

**Q :** Puis-je apporter mon propre système de stockage ?

**R :** Cela n’est pas actuellement pris en charge.

**Q :** je ne peux pas naviguer sur fichier système ou en cours d’exécution des processus du mon conteneur personnalisé à partir du site SCM hello. Pourquoi ?

**R :** site SCM hello s’exécute dans un conteneur distinct. Vous ne peut pas vérifier le système de fichiers hello ou de l’exécution du processus de conteneur d’application hello.

**Q :** mon conteneur personnalisé écoute le port tooa autre que le port 80. Comment puis-je configurer mon port toothat de demandes application tooroute hello ?

**R :** nous avons la détection automatique du port, vous pouvez également spécifier une application appelé **WEBSITES_PORT**et lui donner la valeur hello du numéro de port hello attendu. Précédemment a été à l’aide de la plateforme de hello `PORT` application définissant, nous planifiez toodeprecate hello utiliser cette application définissant et déplacer toousing `WEBSITES_PORT` exclusivement.

**Q :** dois-je tooimplement HTTPS dans mon conteneur personnalisé.

**R :** non, plateforme de hello gère arrêt du protocole HTTPS pour les serveurs frontaux hello partagé.

## <a name="pricing-and-sla"></a>Tarifs et contrat SLA

**Q :** quel est hello le prix pendant que vous utilisez une version préliminaire publique de hello ?

**R :** vous êtes facturé moitié nombre hello d’heures pendant lesquelles votre application s’exécute avec la tarification de Azure App Service normal hello. Cela signifie que vous bénéficiez d’une remise de 50 pour cent sur la tarification normale d’Azure App Service.

## <a name="other"></a>Autres

**Q :** quels sont les caractères hello pris en charge dans les noms de paramètres d’application ?

**R :** vous pouvez uniquement utiliser A-Z, a-z, 0-9 et hello trait de soulignement pour les paramètres de l’application.

**Q :** Où puis-je demander de nouvelles fonctionnalités ?

**R :** vous pouvez soumettre votre idée à hello [forum de commentaires d’applications Web](https://aka.ms/webapps-uservoice). Ajouter un titre de toohello « [Linux] » de votre idée.

## <a name="next-steps"></a>Étapes suivantes
* [Qu’est-ce qu’Azure Web App sur Linux ?](app-service-linux-intro.md)
* [Prise en charge SSH pour Azure Web App sur Linux](./app-service-linux-ssh-support.md)
* [Configurer des environnements intermédiaires dans Azure App Service](./web-sites-staged-publishing.md)
* [Déploiement continu avec l’application web Azure sur Linux](./app-service-linux-ci-cd.md)
