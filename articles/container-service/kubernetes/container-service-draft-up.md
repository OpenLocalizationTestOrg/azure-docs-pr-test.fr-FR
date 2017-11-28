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
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a><span data-ttu-id="23aa1-104">Utiliser le brouillon avec le Service de conteneur Azure et du Registre de conteneur Azure toobuild et déployer une application tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="23aa1-104">Use Draft with Azure Container Service and Azure Container Registry toobuild and deploy an application tooKubernetes</span></span>

<span data-ttu-id="23aa1-105">[Brouillon](https://aka.ms/draft) est un nouvel outil open source qui rend les applications conteneur toodevelop facile et de les déployer les clusters tooKubernetes sans connaître une grande partie sur Docker et Kubernetes--ou même de les installer.</span><span class="sxs-lookup"><span data-stu-id="23aa1-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy toodevelop container-based applications and deploy them tooKubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="23aa1-106">À l’aide des outils tels que brouillon permettre de vous et votre focus équipes application hello avec Kubernetes de génération, ne pas payer autant tooinfrastructure une attention particulière.</span><span class="sxs-lookup"><span data-stu-id="23aa1-106">Using tools like Draft let you and your teams focus on building hello application with Kubernetes, not paying as much attention tooinfrastructure.</span></span>

<span data-ttu-id="23aa1-107">Vous pouvez utiliser Draft avec n’importe quel registre d’images Docker et n’importe quel cluster Kubernetes, y compris au niveau local.</span><span class="sxs-lookup"><span data-stu-id="23aa1-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="23aa1-108">Ce didacticiel montre comment toouse ACS avec toocreate Kubernetes ACR et Azure DNS un développeur de l’élément de configuration/CD dynamique de pipeline à l’aide de brouillon.</span><span class="sxs-lookup"><span data-stu-id="23aa1-108">This tutorial shows how toouse ACS with Kubernetes, ACR, and Azure DNS toocreate a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="23aa1-109">Création d’un Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="23aa1-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="23aa1-110">Vous pouvez facilement [créer un Registre de conteneur Azure nouveau](../../container-registry/container-registry-get-started-azure-cli.md), mais hello étapes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="23aa1-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but hello steps are as follows:</span></span>

1. <span data-ttu-id="23aa1-111">Créer un toomanage de groupe de ressources Azure de votre cluster de Kubernetes de Registre et hello ACR dans ACS.</span><span class="sxs-lookup"><span data-stu-id="23aa1-111">Create a Azure resource group toomanage your ACR registry and hello Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="23aa1-112">Créez un registre d’images ACR à l’aide de la commande [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="23aa1-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="23aa1-113">Créer un service Azure Container Service avec Kubernetes</span><span class="sxs-lookup"><span data-stu-id="23aa1-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="23aa1-114">Vous êtes maintenant prêt toouse [az acs créer](/cli/azure/acs#create) cluster toocreate un services ACS à l’aide de Kubernetes comme hello `--orchestrator-type` valeur.</span><span class="sxs-lookup"><span data-stu-id="23aa1-114">Now you're ready toouse [az acs create](/cli/azure/acs#create) toocreate an ACS cluster using Kubernetes as hello `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="23aa1-115">Étant donné que Kubernetes n’est pas type d’orchestrator hello par défaut, veillez à ce que vous utilisez hello `--orchestrator-type kubernetes` basculer.</span><span class="sxs-lookup"><span data-stu-id="23aa1-115">Because Kubernetes is not hello default orchestrator type, be sure you use hello `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="23aa1-116">sortie Hello lorsque réussie recherche similaire toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="23aa1-116">hello output when successful looks similar toohello following.</span></span>

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

<span data-ttu-id="23aa1-117">Maintenant que vous disposez d’un cluster, vous pouvez importer des informations d’identification hello à l’aide de hello [az acs kubernetes get-informations d’identification](/cli/azure/acs/kubernetes#get-credentials) commande.</span><span class="sxs-lookup"><span data-stu-id="23aa1-117">Now that you have a cluster, you can import hello credentials by using hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="23aa1-118">Vous avez maintenant un fichier de configuration local pour votre cluster, ce qui est le besoin des dirigeants et le brouillon tooget leur travail.</span><span class="sxs-lookup"><span data-stu-id="23aa1-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need tooget their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="23aa1-119">Installer et configurer Draft</span><span class="sxs-lookup"><span data-stu-id="23aa1-119">Install and configure draft</span></span>
<span data-ttu-id="23aa1-120">instructions d’installation Hello pour brouillon sont Bonjour [référentiel du brouillon](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="23aa1-120">hello installation instructions for Draft are in hello [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="23aa1-121">Ils sont relativement simples, mais nécessitent-elles une configuration, car il dépend de [dirigeants](https://aka.ms/helm) toocreate et déployer un graphique dirigeants dans un cluster de Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="23aa1-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) toocreate and deploy a Helm chart into hello Kubernetes cluster.</span></span>

1. <span data-ttu-id="23aa1-122">[Téléchargez et installez Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="23aa1-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="23aa1-123">Utiliser toosearch dirigeants pour et installer `stable/traefik`et tooenable de contrôleur en entrée les demandes pour vos builds entrantes.</span><span class="sxs-lookup"><span data-stu-id="23aa1-123">Use Helm toosearch for and install `stable/traefik`, and ingress controller tooenable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="23aa1-124">Maintenant définir un espion sur hello `ingress` contrôleur toocapture hello externe IP valeur lorsqu’elle est déployée.</span><span class="sxs-lookup"><span data-stu-id="23aa1-124">Now set a watch on hello `ingress` controller toocapture hello external IP value when it is deployed.</span></span> <span data-ttu-id="23aa1-125">Cette adresse IP sera hello une [mappé tooyour déploiement domaine](#wire-up-deployment-domain) dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="23aa1-125">This IP address will be hello one [mapped tooyour deployment domain](#wire-up-deployment-domain) in hello next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="23aa1-126">Hello dans ce cas, les adresses IP externes pour hello déploiement domain est `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="23aa1-126">In this case, hello external IP for hello deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="23aa1-127">Maintenant, vous pouvez mapper votre domaine toothat adresse IP.</span><span class="sxs-lookup"><span data-stu-id="23aa1-127">Now you can map your domain toothat IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="23aa1-128">Lier le domaine de déploiement</span><span class="sxs-lookup"><span data-stu-id="23aa1-128">Wire up deployment domain</span></span>

<span data-ttu-id="23aa1-129">Draft crée une version pour chaque graphique Helm qu’il génère, autrement dit pour chaque application sur laquelle vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="23aa1-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="23aa1-130">Chacune d’elles Obtient un nom généré qui est utilisé par le projet en tant qu’un _sous-domaine_ sur la racine de hello _domaine de déploiement_ que vous contrôlez.</span><span class="sxs-lookup"><span data-stu-id="23aa1-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of hello root _deployment domain_ that you control.</span></span> <span data-ttu-id="23aa1-131">(Dans cet exemple, nous utilisons `squillace.io` en tant que domaine de déploiement hello.) tooenable ce comportement sous-domaine, vous devez créer un enregistrement A pour `'*'` vos entrées DNS pour votre domaine de déploiement, afin que chacun généré sous-domaine est routé toohello Kubernetes contrôleur d’entrée du cluster.</span><span class="sxs-lookup"><span data-stu-id="23aa1-131">(In this example, we use `squillace.io` as hello deployment domain.) tooenable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed toohello Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="23aa1-132">Le fournisseur de votre propre domaine a ses propres serveurs DNS de tooassign moyen ; trop[déléguer votre tooAzure de serveurs de noms de domaine DNS](../../dns/dns-delegate-domain-azure-dns.md), vous prenez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="23aa1-132">Your own domain provider has their own way tooassign DNS servers; too[delegate your domain nameservers tooAzure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take hello following steps:</span></span>

1. <span data-ttu-id="23aa1-133">Créez un groupe de ressources pour votre zone.</span><span class="sxs-lookup"><span data-stu-id="23aa1-133">Create a resource group for your zone.</span></span>
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

2. <span data-ttu-id="23aa1-134">Créez une zone DNS pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="23aa1-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="23aa1-135">Hello d’utilisation [créer de zone dns de réseau az](/cli/azure/network/dns/zone#create) commande tooobtain hello toodelegate de serveurs de noms DNS contrôler tooAzure DNS pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="23aa1-135">Use hello [az network dns zone create](/cli/azure/network/dns/zone#create) command tooobtain hello nameservers toodelegate DNS control tooAzure DNS for your domain.</span></span>
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
3. <span data-ttu-id="23aa1-136">Ajouter des serveurs DNS de hello que vous pouvez soit le fournisseur de domaines toohello pour votre domaine de déploiement, ce qui permet à votre domaine toorepoint Azure DNS toouse que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="23aa1-136">Add hello DNS servers you are given toohello domain provider for your deployment domain, which enables you toouse Azure DNS toorepoint your domain as you want.</span></span>
4. <span data-ttu-id="23aa1-137">Créer une entrée de jeu d’enregistrements A pour votre toohello de mappage de domaine de déploiement `ingress` IP de l’étape 2 de la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="23aa1-137">Create an A record-set entry for your deployment domain mapping toohello `ingress` IP from step 2 of hello previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="23aa1-138">sortie de Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="23aa1-138">hello output looks something like:</span></span>
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

5. <span data-ttu-id="23aa1-139">Configurer brouillon toouse votre Registre et créer des sous-domaines pour chaque graphique dirigeants qu'il crée.</span><span class="sxs-lookup"><span data-stu-id="23aa1-139">Configure Draft toouse your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="23aa1-140">tooconfigure brouillon, vous devez :</span><span class="sxs-lookup"><span data-stu-id="23aa1-140">tooconfigure Draft, you need:</span></span>
  - <span data-ttu-id="23aa1-141">Nom de votre service Azure Container Registry (dans cet exemple, `draft`)</span><span class="sxs-lookup"><span data-stu-id="23aa1-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="23aa1-142">Votre clé de Registre, ou mot de passe, à partir de `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`</span><span class="sxs-lookup"><span data-stu-id="23aa1-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="23aa1-143">domaine de déploiement Hello racine que vous avez configuré toomap toohello Kubernetes en entrée une adresse IP externe (ici, `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="23aa1-143">hello root deployment domain that you have configured toomap toohello Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="23aa1-144">Appelez `draft init` et processus de configuration hello vous invite à entrer les valeurs hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="23aa1-144">Call `draft init` and hello configuration process prompts you for hello values above.</span></span> <span data-ttu-id="23aa1-145">processus de Hello semble quelque chose suivant de hello hello première fois que vous exécutez.</span><span class="sxs-lookup"><span data-stu-id="23aa1-145">hello process looks something like hello following hello first time you run it.</span></span>
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

<span data-ttu-id="23aa1-146">Vous êtes maintenant prêt toodeploy une application.</span><span class="sxs-lookup"><span data-stu-id="23aa1-146">Now you're ready toodeploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="23aa1-147">Générer et déployer une application</span><span class="sxs-lookup"><span data-stu-id="23aa1-147">Build and deploy an application</span></span>

<span data-ttu-id="23aa1-148">Dans le référentiel de brouillon hello sont [six applications d’exemple simple](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="23aa1-148">In hello Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="23aa1-149">Cloner le référentiel de hello et utilisons hello [exemple de Python](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="23aa1-149">Clone hello repo and let's use hello [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="23aa1-150">Modifier dans le répertoire d’exemples/Python hello et tapez `draft create` application hello de toobuild.</span><span class="sxs-lookup"><span data-stu-id="23aa1-150">Change into hello examples/Python directory, and type `draft create` toobuild hello application.</span></span> <span data-ttu-id="23aa1-151">Il doit ressembler à hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="23aa1-151">It should look like hello following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

<span data-ttu-id="23aa1-152">sortie de Hello inclut un fichier Dockerfile et un graphique dirigeants.</span><span class="sxs-lookup"><span data-stu-id="23aa1-152">hello output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="23aa1-153">toobuild et le déploiement, vous tapez simplement `draft up`.</span><span class="sxs-lookup"><span data-stu-id="23aa1-153">toobuild and deploy, you just type `draft up`.</span></span> <span data-ttu-id="23aa1-154">sortie de Hello est complet, mais commence comme hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="23aa1-154">hello output is extensive, but begins like hello following example.</span></span>
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

<span data-ttu-id="23aa1-155">et à quel moment réussie se termine avec un code similaire toohello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="23aa1-155">and when successful ends with something similar toohello following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

<span data-ttu-id="23aa1-156">Tout ce qui est le nom de votre graphique, vous pouvez désormais `curl http://gangly-bronco.squillace.io` tooreceive hello réponse, par exemple `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="23aa1-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` tooreceive hello reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23aa1-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="23aa1-157">Next steps</span></span>

<span data-ttu-id="23aa1-158">Maintenant que vous avez un cluster ACS Kubernetes, vous pouvez analyser à l’aide de [Registre de conteneur Azure](../../container-registry/container-registry-intro.md) toocreate plus et différents déploiements de ce scénario.</span><span class="sxs-lookup"><span data-stu-id="23aa1-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) toocreate more and different deployments of this scenario.</span></span> <span data-ttu-id="23aa1-159">Par exemple, vous pouvez créer un jeu d’enregistrements DNS de domaine draft._basedomain.toplevel_ qui contrôle les éléments d’un sous-domaine plus profond pour des déploiements ACS spécifiques.</span><span class="sxs-lookup"><span data-stu-id="23aa1-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






