---
title: "aaaGetting main d’Azure Service Fabric XPlat CLI"
description: "Prise en main de l’interface de ligne de commande Azure Service Fabric XPlat"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a>À l’aide de hello XPlat CLI toointeract avec un cluster Service Fabric

Vous pouvez interagir avec le cluster Service Fabric à partir d’ordinateurs Linux à l’aide de hello XPlat CLI sur Linux.

première étape de Hello est obtenir la dernière version de hello Hello CLI à partir de rep de git hello et ensemble dans votre chemin d’accès à l’aide de hello suivant de commandes :

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Pour chaque commande, il prend en charge, vous pouvez taper le nom de hello de hello commande tooobtain hello d’aide pour cette commande.
La saisie semi-automatique est pris en charge pour les commandes hello. Par exemple, hello suivant donne de commande que vous aide pour toutes les commandes d’application hello. 

```sh
 azure servicefabric application 
```

Vous pouvez filtrer davantage d’aide tooa spécifique la commande hello comme hello suivant montre l’exemple :

```sh
 azure servicefabric application  create
```

tooenable la saisie semi-automatique dans hello CLI, exécutez hello suivant de commandes :

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

Hello suivant les commandes connecter toohello cluster et afficher hello de nœuds de cluster de hello :

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

toouse de paramètres nommés et de trouver ce qu’ils sont, vous pouvez taper--aide après une commande. Par exemple :

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

Lors de la connexion de cluster de plusieurs ordinateurs tooa à partir d’un ordinateur **qui ne fait pas partie du cluster de hello**, utilisez hello de commande suivante :

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

Remplacer la balise de PublicIPorFQDN hello avec l’adresse IP réelle de hello ou le nom de domaine complet comme il convient. Lors de la connexion de cluster de plusieurs ordinateurs tooa à partir d’un ordinateur **qui fait partie du cluster de hello**, utilisez hello de commande suivante :

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

Vous pouvez utiliser PowerShell ou toointeract CLI avec votre Cluster Linux Service Fabric créé via hello portail Azure.

> [!WARNING]
> Ces clusters non sécurisés, par conséquent, vous pouvez ouvrir votre boîte de dialogue un en ajoutant l’adresse IP publique de hello dans le manifeste du cluster hello.

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a>À l’aide de hello cluster Service Fabric de XPlat CLI tooconnect tooa

Hello suivant des commandes CLI d’Azure décrire comment tooconnect tooa sécuriser le cluster. Détails du certificat Hello doivent correspondre à un certificat sur les nœuds de cluster hello.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Si votre certificat a des autorités de certification (CA), vous avez besoin de paramètre de l’autorité de certification---cert-path tooadd hello comme hello l’exemple suivant : 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Si vous avez plusieurs autorités de certification, utilisez une virgule comme délimiteur de hello.

Si votre nom commun hello certificat ne correspond pas de point de terminaison de connexion hello, vous pouvez utiliser le paramètre hello `--strict-ssl-false` toobypass hello vérification comme indiqué dans hello de commande suivante :

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

Si vous souhaitez que la vérification de tooskip hello autorité de certification, vous pouvez ajouter hello--paramètre false rejet non autorisé comme indiqué dans hello de commande suivante : 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

Une fois que vous vous connectez, vous devez être en mesure de toorun autres toointeract de commandes CLI avec cluster de hello.

## <a name="deploying-your-service-fabric-application"></a>Déploiement de votre application Service Fabric

Exécutez hello suivant les commandes toocopy, inscrire et démarrer l’application hello service fabric :

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Mettre à niveau votre application

les processus Hello sont similaire toohello [processus dans Windows](service-fabric-application-upgrade-tutorial-powershell.md)).

Construisez, copiez, enregistrez et créez votre application à partir du répertoire racine du projet. Si votre instance de l’application se nomme `fabric:/MySFApp`et le type de hello est MySFApp, commandes hello serait comme suit :

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Apportez hello modification tooyour application et régénérer hello modifié service.  Hello de mise à jour modifié fichier manifeste du service (ServiceManifest.xml) avec les versions de mise à jour de hello pour hello Service (et Code ou configuration ou les données selon le cas). En outre modifier le manifeste de l’application hello (ApplicationManifest.xml) avec le numéro de version hello mis à jour pour l’application hello et hello service modifié.  Maintenant, copier et enregistrer votre application mis à jour à l’aide de hello suivant de commandes :

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

Vous pouvez désormais mise à niveau des applications hello avec hello de commande suivante :

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Vous pouvez désormais analyser mise à niveau de l’application hello à l’aide de SFX. Dans quelques minutes, application hello serait ont été mis à jour. Vous pouvez également essayer d’une application de mise à jour avec une erreur et vérifier la fonctionnalité de restauration automatique hello dans l’infrastructure de service.

## <a name="converting-from-pfx-toopem-and-vice-versa"></a>Conversion de PFX tooPEM et vice versa

Vous devrez peut-être tooinstall un certificat de vos clusters de sécurisé tooaccess ordinateur local (Windows ou Linux) qui peuvent être dans un autre environnement. Par exemple, lors de l’accès à un cluster sécurisé de Linux à partir d’un ordinateur Windows et vice versa vous devrez peut-être tooconvert votre certificat PFX tooPEM et vice versa. 

tooconvert d’un fichier dans PEM fichier tooa PFX, hello utilisez commande suivante :

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

tooconvert d’un fichier PEM de la tooa d’un fichier PFX, hello utilisez commande suivante :

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Consultez trop[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) pour plus d’informations.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Résolution des problèmes


### <a name="copying-of-hello-application-package-does-not-succeed"></a>Copie du package d’application hello ne réussit pas

Vérifiez si `openssh` est installé. Par défaut, cet élément n’est pas installé sur le bureau Ubuntu. Installer à l’aide de hello de commande suivante :

```sh
sudo apt-get install openssh-server openssh-client**
```

Si hello problème persiste, essayez de désactiver PAM pour ssh en modifiant hello `sshd_config` fichier à l’aide de hello suivant de commandes :

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

Si hello problème persiste, essayez de nombre hello croissant de ssh sessions en exécutant hello suivant de commandes :

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

À l’aide de clés pour ssh authentification (en opposition toopasswords) n’est pas encore prise en charge (comme plateforme de hello utilise ssh toocopy packages), par conséquent, utilisez l’authentification du mot de passe à la place.

## <a name="next-steps"></a>Étapes suivantes

[Configuration d’environnement de développement hello et déployer un cluster de Service Fabric application tooa Linux.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>Articles connexes

* [Prise en main de Service Fabric et d’Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
