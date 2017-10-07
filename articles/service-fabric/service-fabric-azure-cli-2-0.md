---
title: "aaaGet main d’Azure Service Fabric et Azure CLI 2.0"
description: "Découvrez le fonctionnement des commandes toouse hello Azure Service Fabric module CLI d’Azure, version 2.0. Découvrez comment tooconnect tooa cluster et la manière dont les applications toomanage."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a>Microsoft Azure Service Fabric et Azure CLI 2.0

Bonjour Azure outil de ligne de commande (CLI d’Azure) version 2.0 inclut toohelp commandes vous gérez les clusters Azure Service Fabric. Découvrez comment tooget main CLI d’Azure et Service Fabric.

## <a name="install-azure-cli-20"></a>Installer Azure CLI 2.0

Vous pouvez utiliser toointeract de commandes Azure CLI 2.0 avec et gérer des clusters Service Fabric. version la plus récente hello tooget de CLI d’Azure, suivez hello [processus d’installation standard Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

Pour plus d’informations, consultez hello [vue d’ensemble de Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="azure-cli-syntax"></a>Syntaxe d’Azure CLI

Dans Azure CLI, toutes les commandes Service Fabric incluent le préfixe `az sf`. Pour obtenir des informations générales sur les commandes hello que vous pouvez utiliser, utilisez `az sf -h`. Pour obtenir de l’aide avec une seule commande, utilisez `az sf <command> -h`.

Les commandes Service Fabric dans Azure CLI respectent le modèle d’affectation de noms suivant :

```azurecli
az sf <object> <action>
```

`<object>`est la cible de hello pour `<action>`.

## <a name="select-a-cluster"></a>Sélectionner un cluster

Avant d’effectuer des opérations, vous devez sélectionner un tooconnect de cluster à. Pour obtenir un exemple, consultez hello suivant de code. code de Hello connecte tooan des clusters non sécurisés.

> [!WARNING]
> N’utilisez pas de clusters Service Fabric non sécurisés dans un environnement de production.

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

point de terminaison Hello cluster doit être préfixé par `http` ou `https`. Il doit inclure le port hello pour la passerelle HTTP hello. adresse et le port de hello sont hello identique hello URL de Service Fabric Explorer.

Pour les clusters qui sont sécurisés avec un certificat, vous pouvez utiliser des fichiers non chiffrés .pem ou des fichiers .crt et .key. Par exemple :

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Pour plus d’informations, consultez [cluster Azure Service Fabric sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md).

> [!NOTE]
> Hello `select` commande n’agir sur toutes les demandes avant d’être retournée. tooverify que vous avez spécifié un cluster correctement, utilisez une commande similaire à `az sf cluster health`. Vérifiez la commande hello ne retourne pas les erreurs.

## <a name="basic-operations"></a>Opérations de base

Les informations de connexion du cluster sont conservées dans plusieurs sessions d’Azure CLI. Après avoir sélectionné un cluster Service Fabric, vous pouvez exécuter n’importe quelle commande de l’infrastructure de Service sur le cluster de hello.

Par exemple, tooget hello état d’intégrité de cluster Service Fabric, utilisez hello de commande suivante :

```azurecli
az sf cluster health
```

commande Hello résultat suivant hello (en supposant que la sortie JSON est spécifiée dans la configuration d’Azure CLI hello) de sortie :

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

Vous constaterez peut-être hello suivant des informations utiles si vous rencontrez des problèmes lors de l’utilisation des commandes de Service Fabric dans CLI d’Azure.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Convertir un certificat PFX tooPEM format

Azure CLI prend en charge les certificats côté client comme les fichiers PEM (extension .pem). Si vous utilisez des fichiers PFX à partir de Windows, vous devez convertir ces format tooPEM de certificats. tooconvert un fichier PEM de tooa du fichier PFX, utilisez hello de commande suivante :

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Pour plus d’informations, consultez hello [OpenSSL documentation](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Problèmes de connexion

Certaines opérations peuvent générer hello message suivant :

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Vérifiez que hello spécifié de point de terminaison de cluster est disponible et à l’écoute. En outre, vérifiez que hello que l’interface utilisateur de Service Fabric Explorer est disponible à l’hôte et le port. point de terminaison de hello tooupdate, utilisez `az sf cluster select`.

### <a name="detailed-logs"></a>Journaux détaillés

Les journaux détaillés peuvent souvent être utiles lorsque vous déboguez ou signalez un problème. CLI Azure offre global `--debug` indicateur qui augmente de détail hello de fichiers journaux.

### <a name="command-help-and-syntax"></a>Aide et syntaxe de commande

Suivre des commandes de service Fabric hello les mêmes conventions que CLI d’Azure. Pour l’aide sur une commande spécifique ou un groupe de commandes, utilisez hello `-h` indicateur :

```azurecli
az sf application -h
```

Voici un autre exemple :

```azurecli
az sf application create -h
```
