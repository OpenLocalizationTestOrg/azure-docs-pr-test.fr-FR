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
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="9e98d-104">Microsoft Azure Service Fabric et Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9e98d-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="9e98d-105">Bonjour Azure outil de ligne de commande (CLI d’Azure) version 2.0 inclut toohelp commandes vous gérez les clusters Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e98d-105">hello Azure command-line tool (Azure CLI) version 2.0 includes commands toohelp you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="9e98d-106">Découvrez comment tooget main CLI d’Azure et Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e98d-106">Learn how tooget started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="9e98d-107">Installer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9e98d-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="9e98d-108">Vous pouvez utiliser toointeract de commandes Azure CLI 2.0 avec et gérer des clusters Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e98d-108">You can use Azure CLI 2.0 commands toointeract with and manage Service Fabric clusters.</span></span> <span data-ttu-id="9e98d-109">version la plus récente hello tooget de CLI d’Azure, suivez hello [processus d’installation standard Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9e98d-109">tooget hello latest version of Azure CLI, follow hello [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="9e98d-110">Pour plus d’informations, consultez hello [vue d’ensemble de Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e98d-110">For more information, see hello [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="9e98d-111">Syntaxe d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9e98d-111">Azure CLI syntax</span></span>

<span data-ttu-id="9e98d-112">Dans Azure CLI, toutes les commandes Service Fabric incluent le préfixe `az sf`.</span><span class="sxs-lookup"><span data-stu-id="9e98d-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="9e98d-113">Pour obtenir des informations générales sur les commandes hello que vous pouvez utiliser, utilisez `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="9e98d-113">For general information about hello commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="9e98d-114">Pour obtenir de l’aide avec une seule commande, utilisez `az sf <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="9e98d-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="9e98d-115">Les commandes Service Fabric dans Azure CLI respectent le modèle d’affectation de noms suivant :</span><span class="sxs-lookup"><span data-stu-id="9e98d-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="9e98d-116">`<object>`est la cible de hello pour `<action>`.</span><span class="sxs-lookup"><span data-stu-id="9e98d-116">`<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="9e98d-117">Sélectionner un cluster</span><span class="sxs-lookup"><span data-stu-id="9e98d-117">Select a cluster</span></span>

<span data-ttu-id="9e98d-118">Avant d’effectuer des opérations, vous devez sélectionner un tooconnect de cluster à.</span><span class="sxs-lookup"><span data-stu-id="9e98d-118">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="9e98d-119">Pour obtenir un exemple, consultez hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="9e98d-119">For an example, see hello following code.</span></span> <span data-ttu-id="9e98d-120">code de Hello connecte tooan des clusters non sécurisés.</span><span class="sxs-lookup"><span data-stu-id="9e98d-120">hello code connects tooan unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="9e98d-121">N’utilisez pas de clusters Service Fabric non sécurisés dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9e98d-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="9e98d-122">point de terminaison Hello cluster doit être préfixé par `http` ou `https`.</span><span class="sxs-lookup"><span data-stu-id="9e98d-122">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="9e98d-123">Il doit inclure le port hello pour la passerelle HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="9e98d-123">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="9e98d-124">adresse et le port de hello sont hello identique hello URL de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="9e98d-124">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="9e98d-125">Pour les clusters qui sont sécurisés avec un certificat, vous pouvez utiliser des fichiers non chiffrés .pem ou des fichiers .crt et .key.</span><span class="sxs-lookup"><span data-stu-id="9e98d-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="9e98d-126">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9e98d-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="9e98d-127">Pour plus d’informations, consultez [cluster Azure Service Fabric sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9e98d-127">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9e98d-128">Hello `select` commande n’agir sur toutes les demandes avant d’être retournée.</span><span class="sxs-lookup"><span data-stu-id="9e98d-128">hello `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="9e98d-129">tooverify que vous avez spécifié un cluster correctement, utilisez une commande similaire à `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="9e98d-129">tooverify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="9e98d-130">Vérifiez la commande hello ne retourne pas les erreurs.</span><span class="sxs-lookup"><span data-stu-id="9e98d-130">Verify that hello command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="9e98d-131">Opérations de base</span><span class="sxs-lookup"><span data-stu-id="9e98d-131">Basic operations</span></span>

<span data-ttu-id="9e98d-132">Les informations de connexion du cluster sont conservées dans plusieurs sessions d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9e98d-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="9e98d-133">Après avoir sélectionné un cluster Service Fabric, vous pouvez exécuter n’importe quelle commande de l’infrastructure de Service sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9e98d-133">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="9e98d-134">Par exemple, tooget hello état d’intégrité de cluster Service Fabric, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9e98d-134">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="9e98d-135">commande Hello résultat suivant hello (en supposant que la sortie JSON est spécifiée dans la configuration d’Azure CLI hello) de sortie :</span><span class="sxs-lookup"><span data-stu-id="9e98d-135">hello command results in hello following output (assuming that JSON output is specified in hello Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="9e98d-136">Conseils et résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="9e98d-136">Tips and troubleshooting</span></span>

<span data-ttu-id="9e98d-137">Vous constaterez peut-être hello suivant des informations utiles si vous rencontrez des problèmes lors de l’utilisation des commandes de Service Fabric dans CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="9e98d-137">You might find hello following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="9e98d-138">Convertir un certificat PFX tooPEM format</span><span class="sxs-lookup"><span data-stu-id="9e98d-138">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="9e98d-139">Azure CLI prend en charge les certificats côté client comme les fichiers PEM (extension .pem).</span><span class="sxs-lookup"><span data-stu-id="9e98d-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="9e98d-140">Si vous utilisez des fichiers PFX à partir de Windows, vous devez convertir ces format tooPEM de certificats.</span><span class="sxs-lookup"><span data-stu-id="9e98d-140">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="9e98d-141">tooconvert un fichier PEM de tooa du fichier PFX, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9e98d-141">tooconvert a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="9e98d-142">Pour plus d’informations, consultez hello [OpenSSL documentation](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="9e98d-142">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="9e98d-143">Problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="9e98d-143">Connection issues</span></span>

<span data-ttu-id="9e98d-144">Certaines opérations peuvent générer hello message suivant :</span><span class="sxs-lookup"><span data-stu-id="9e98d-144">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="9e98d-145">Vérifiez que hello spécifié de point de terminaison de cluster est disponible et à l’écoute.</span><span class="sxs-lookup"><span data-stu-id="9e98d-145">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="9e98d-146">En outre, vérifiez que hello que l’interface utilisateur de Service Fabric Explorer est disponible à l’hôte et le port.</span><span class="sxs-lookup"><span data-stu-id="9e98d-146">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="9e98d-147">point de terminaison de hello tooupdate, utilisez `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="9e98d-147">tooupdate hello endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="9e98d-148">Journaux détaillés</span><span class="sxs-lookup"><span data-stu-id="9e98d-148">Detailed logs</span></span>

<span data-ttu-id="9e98d-149">Les journaux détaillés peuvent souvent être utiles lorsque vous déboguez ou signalez un problème.</span><span class="sxs-lookup"><span data-stu-id="9e98d-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="9e98d-150">CLI Azure offre global `--debug` indicateur qui augmente de détail hello de fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="9e98d-150">Azure CLI offers a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="9e98d-151">Aide et syntaxe de commande</span><span class="sxs-lookup"><span data-stu-id="9e98d-151">Command help and syntax</span></span>

<span data-ttu-id="9e98d-152">Suivre des commandes de service Fabric hello les mêmes conventions que CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="9e98d-152">Service Fabric commands follow hello same conventions as Azure CLI.</span></span> <span data-ttu-id="9e98d-153">Pour l’aide sur une commande spécifique ou un groupe de commandes, utilisez hello `-h` indicateur :</span><span class="sxs-lookup"><span data-stu-id="9e98d-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="9e98d-154">Voici un autre exemple :</span><span class="sxs-lookup"><span data-stu-id="9e98d-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
