---
title: aaaUse brouillon avec le Service de conteneur Azure et du Registre de conteneur Azure | Documents Microsoft
description: "Créer un cluster ACS Kubernetes et un toocreate de Registre de conteneur Azure votre première application dans Azure avec un brouillon."
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: Docker, Containers, microservices, Kubernetes, Draft, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a>Utiliser le brouillon avec le Service de conteneur Azure et du Registre de conteneur Azure toobuild et déployer une application tooKubernetes

[Brouillon](https://aka.ms/draft) est un nouvel outil open source qui rend les applications conteneur toodevelop facile et de les déployer les clusters tooKubernetes sans connaître une grande partie sur Docker et Kubernetes--ou même de les installer. À l’aide des outils tels que brouillon permettre de vous et votre focus équipes application hello avec Kubernetes de génération, ne pas payer autant tooinfrastructure une attention particulière.

Vous pouvez utiliser Draft avec n’importe quel registre d’images Docker et n’importe quel cluster Kubernetes, y compris au niveau local. Ce didacticiel montre comment toouse ACS avec toocreate Kubernetes ACR et Azure DNS un développeur de l’élément de configuration/CD dynamique de pipeline à l’aide de brouillon.


## <a name="create-an-azure-container-registry"></a>Création d’un Azure Container Registry
Vous pouvez facilement [créer un Registre de conteneur Azure nouveau](../../container-registry/container-registry-get-started-azure-cli.md), mais hello étapes sont les suivantes :

1. Créer un toomanage de groupe de ressources Azure de votre cluster de Kubernetes de Registre et hello ACR dans ACS.
      ```azurecli
      az group create --name draft --location eastus
      ```

2. Créez un registre d’images ACR à l’aide de la commande [az acr create](/cli/azure/acr#create).
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>Créer un service Azure Container Service avec Kubernetes

Vous êtes maintenant prêt toouse [az acs créer](/cli/azure/acs#create) cluster toocreate un services ACS à l’aide de Kubernetes comme hello `--orchestrator-type` valeur.
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> Étant donné que Kubernetes n’est pas type d’orchestrator hello par défaut, veillez à ce que vous utilisez hello `--orchestrator-type kubernetes` basculer.

sortie Hello lorsque réussie recherche similaire toohello suivant.

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

Maintenant que vous disposez d’un cluster, vous pouvez importer des informations d’identification hello à l’aide de hello [az acs kubernetes get-informations d’identification](/cli/azure/acs/kubernetes#get-credentials) commande. Vous avez maintenant un fichier de configuration local pour votre cluster, ce qui est le besoin des dirigeants et le brouillon tooget leur travail.

## <a name="install-and-configure-draft"></a>Installer et configurer Draft
instructions d’installation Hello pour brouillon sont Bonjour [référentiel du brouillon](https://github.com/Azure/draft/blob/master/docs/install.md). Ils sont relativement simples, mais nécessitent-elles une configuration, car il dépend de [dirigeants](https://aka.ms/helm) toocreate et déployer un graphique dirigeants dans un cluster de Kubernetes hello.

1. [Téléchargez et installez Helm](https://aka.ms/helm#install).
2. Utiliser toosearch dirigeants pour et installer `stable/traefik`et tooenable de contrôleur en entrée les demandes pour vos builds entrantes.
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    Maintenant définir un espion sur hello `ingress` contrôleur toocapture hello externe IP valeur lorsqu’elle est déployée. Cette adresse IP sera hello une [mappé tooyour déploiement domaine](#wire-up-deployment-domain) dans la section suivante de hello.

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    Hello dans ce cas, les adresses IP externes pour hello déploiement domain est `13.64.108.240`. Maintenant, vous pouvez mapper votre domaine toothat adresse IP.

## <a name="wire-up-deployment-domain"></a>Lier le domaine de déploiement

Draft crée une version pour chaque graphique Helm qu’il génère, autrement dit pour chaque application sur laquelle vous travaillez. Chacune d’elles Obtient un nom généré qui est utilisé par le projet en tant qu’un _sous-domaine_ sur la racine de hello _domaine de déploiement_ que vous contrôlez. (Dans cet exemple, nous utilisons `squillace.io` en tant que domaine de déploiement hello.) tooenable ce comportement sous-domaine, vous devez créer un enregistrement A pour `'*'` vos entrées DNS pour votre domaine de déploiement, afin que chacun généré sous-domaine est routé toohello Kubernetes contrôleur d’entrée du cluster.

Le fournisseur de votre propre domaine a ses propres serveurs DNS de tooassign moyen ; trop[déléguer votre tooAzure de serveurs de noms de domaine DNS](../../dns/dns-delegate-domain-azure-dns.md), vous prenez hello comme suit :

1. Créez un groupe de ressources pour votre zone.
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. Créez une zone DNS pour votre domaine.
Hello d’utilisation [créer de zone dns de réseau az](/cli/azure/network/dns/zone#create) commande tooobtain hello toodelegate de serveurs de noms DNS contrôler tooAzure DNS pour votre domaine.
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. Ajouter des serveurs DNS de hello que vous pouvez soit le fournisseur de domaines toohello pour votre domaine de déploiement, ce qui permet à votre domaine toorepoint Azure DNS toouse que vous le souhaitez.
4. Créer une entrée de jeu d’enregistrements A pour votre toohello de mappage de domaine de déploiement `ingress` IP de l’étape 2 de la section précédente de hello.
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
sortie de Hello ressemble à ceci :
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. Configurer brouillon toouse votre Registre et créer des sous-domaines pour chaque graphique dirigeants qu'il crée. tooconfigure brouillon, vous devez :
  - Nom de votre service Azure Container Registry (dans cet exemple, `draft`)
  - Votre clé de Registre, ou mot de passe, à partir de `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`
  - domaine de déploiement Hello racine que vous avez configuré toomap toohello Kubernetes en entrée une adresse IP externe (ici, `squillace.io`)

  Appelez `draft init` et processus de configuration hello vous invite à entrer les valeurs hello ci-dessus. processus de Hello semble quelque chose suivant de hello hello première fois que vous exécutez.
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

Vous êtes maintenant prêt toodeploy une application.


## <a name="build-and-deploy-an-application"></a>Générer et déployer une application

Dans le référentiel de brouillon hello sont [six applications d’exemple simple](https://github.com/Azure/draft/tree/master/examples). Cloner le référentiel de hello et utilisons hello [exemple de Python](https://github.com/Azure/draft/tree/master/examples/python). Modifier dans le répertoire d’exemples/Python hello et tapez `draft create` application hello de toobuild. Il doit ressembler à hello l’exemple suivant.
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

sortie de Hello inclut un fichier Dockerfile et un graphique dirigeants. toobuild et le déploiement, vous tapez simplement `draft up`. sortie de Hello est complet, mais commence comme hello l’exemple suivant.
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

et à quel moment réussie se termine avec un code similaire toohello l’exemple suivant.
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

Tout ce qui est le nom de votre graphique, vous pouvez désormais `curl http://gangly-bronco.squillace.io` tooreceive hello réponse, par exemple `Hello World!`.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez un cluster ACS Kubernetes, vous pouvez analyser à l’aide de [Registre de conteneur Azure](../../container-registry/container-registry-intro.md) toocreate plus et différents déploiements de ce scénario. Par exemple, vous pouvez créer un jeu d’enregistrements DNS de domaine draft._basedomain.toplevel_ qui contrôle les éléments d’un sous-domaine plus profond pour des déploiements ACS spécifiques.






