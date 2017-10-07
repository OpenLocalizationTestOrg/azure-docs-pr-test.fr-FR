---
title: "aaaGet main d’Azure Service Fabric CLI (sfctl)"
description: "Découvrez comment toouse hello CLI d’Azure Service Fabric. Découvrez comment tooconnect tooa cluster et la manière dont les applications toomanage."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a>Ligne de commande Azure Service Fabric

Bonjour Azure Service Fabric CLI (sfctl) est un utilitaire de ligne de commande pour l’interaction et de la gestion des entités de Azure Service Fabric. Sfctl peut être utilisé avec des clusters Windows ou Linux. Sfctl s’exécute sur toute plateforme prenant en charge python.

## <a name="prerequisites"></a>Composants requis

Tooinstallation préalable, assurez-vous que votre environnement a python et pip installé. Pour plus d’informations, examinez hello [pip documentation de démarrage rapide](https://pip.pypa.io/en/latest/quickstart/)et officiel [python installer la documentation](https://wiki.python.org/moin/BeginnersGuide/Download).

Si les deux python 2.7 et 3.6 est prises en charge, il est recommandé de toouse python 3.6.

## <a name="install"></a>Installer

Bonjour Azure Service Fabric CLI (sfctl) est fourni comme un package python. tooinstall hello version la plus récente s’exécuter :

```bash
pip install sfctl
```

Après l’installation, exécutez `sfctl -h` tooget plus d’informations sur les commandes disponibles.

## <a name="cli-syntax"></a>Syntaxe d’Azure CLI

Les commandes sont toujours préfixées avec `sfctl`. Pour obtenir des informations générales sur les commandes dont vous pouvez vous servir, utilisez `sfctl -h`. Pour obtenir de l’aide avec une seule commande, utilisez `sfctl <command> -h`.

Commandes suivent une structure reproductible, avec une cible de hello hello de commandes de verbe de hello ou l’action précédente :

```azurecli
sfctl <object> <action>
```

Dans cet exemple, `<object>` est cible hello pour `<action>`.

## <a name="select-a-cluster"></a>Sélectionner un cluster

Avant d’effectuer des opérations, vous devez sélectionner un tooconnect de cluster à. Par exemple, exécutez hello suivant tooselect et se connecter toohello cluster avec le nom de hello `testcluster.com`.

> [!WARNING]
> N’utilisez pas de clusters Service Fabric non sécurisés dans un environnement de production.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

point de terminaison Hello cluster doit être préfixé par `http` ou `https`. Il doit inclure le port hello pour la passerelle HTTP hello. adresse et le port de hello sont hello identique hello URL de Service Fabric Explorer.

Pour les clusters qui sont sécurisés avec un certificat, vous pouvez spécifier un certificat PEM encodé. certificat de Hello peut être spécifié en tant qu’un seul fichier ou le certificat et la paire de clés.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Pour plus d’informations, consultez [cluster Azure Service Fabric sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md).

## <a name="basic-operations"></a>Opérations de base

Les informations de connexion du cluster persistent dans plusieurs sessions sfctl. Après avoir sélectionné un cluster Service Fabric, vous pouvez exécuter n’importe quelle commande de l’infrastructure de Service sur le cluster de hello.

Par exemple, tooget hello état d’intégrité de cluster Service Fabric, utilisez hello de commande suivante :

```azurecli
sfctl cluster health
```

résultats de la commande Hello Bonjour suivant de sortie :

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a>Conseils et résolution des problèmes

Quelques suggestions et conseils pour la résolution des problèmes courants.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Convertir un certificat PFX tooPEM format

Hello Service Fabric CLI prend en charge les certificats côté client en tant que les fichiers PEM (extension .pem). Si vous utilisez des fichiers PFX à partir de Windows, vous devez convertir ces format tooPEM de certificats. tooconvert un fichier PEM de tooa du fichier PFX, utilisez la commande suivante :

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Pour plus d’informations, consultez hello [OpenSSL documentation](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Problèmes de connexion

Certaines opérations peuvent générer hello message suivant :

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Vérifiez que hello spécifié de point de terminaison de cluster est disponible et à l’écoute. En outre, vérifiez que hello que l’interface utilisateur de Service Fabric Explorer est disponible à l’hôte et le port. point de terminaison de hello tooupdate, utilisez `sfctl cluster select`.

### <a name="detailed-logs"></a>Journaux détaillés

Les journaux détaillés peuvent souvent être utiles lorsque vous déboguez ou signalez un problème. Il existe un global `--debug` indicateur qui augmente de détail hello de fichiers journaux.

### <a name="command-help-and-syntax"></a>Aide et syntaxe de commande

Pour l’aide sur une commande spécifique ou un groupe de commandes, utilisez hello `-h` indicateur :

```azurecli
sfctl application -h
```

Autre exemple :

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a>Étapes suivantes

* [Déployer une application avec hello CLI d’Azure Service Fabric](service-fabric-application-lifecycle-sfctl.md)
* [Prise en main de Service Fabric sur Linux](service-fabric-get-started-linux.md)
