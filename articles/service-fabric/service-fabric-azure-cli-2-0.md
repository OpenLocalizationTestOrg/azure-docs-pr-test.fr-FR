---
title: "Prise en main de Microsoft Azure Service Fabric et d’Azure CLI 2.0"
description: "Découvrez comment utiliser le module de commandes de Microsoft Azure Service Fabric dans Azure CLI, version 2.0. Apprenez à vous connecter à un cluster et à gérer des applications."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ee3302b984ca2f5509755dc17b0a5fd06ace0afe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="a6a59-104">Microsoft Azure Service Fabric et Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a6a59-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="a6a59-105">L’outil en ligne de commande Azure (Azure CLI) version 2.0 comprend des commandes permettant de gérer les clusters Microsoft Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a6a59-105">The Azure command-line tool (Azure CLI) version 2.0 includes commands to help you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="a6a59-106">Apprenez à prendre en main Azure CLI et Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a6a59-106">Learn how to get started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="a6a59-107">Installer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a6a59-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="a6a59-108">Vous pouvez utiliser les commandes Azure CLI 2.0 pour interagir avec des clusters Service Fabric et les gérer.</span><span class="sxs-lookup"><span data-stu-id="a6a59-108">You can use Azure CLI 2.0 commands to interact with and manage Service Fabric clusters.</span></span> <span data-ttu-id="a6a59-109">Pour obtenir la dernière version d’Azure CLI, suivez les [processus d’installation standard Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a6a59-109">To get the latest version of Azure CLI, follow the [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="a6a59-110">Pour plus d’informations, consultez la [présentation d’Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6a59-110">For more information, see the [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="a6a59-111">Syntaxe d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a6a59-111">Azure CLI syntax</span></span>

<span data-ttu-id="a6a59-112">Dans Azure CLI, toutes les commandes Service Fabric incluent le préfixe `az sf`.</span><span class="sxs-lookup"><span data-stu-id="a6a59-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="a6a59-113">Pour obtenir des informations générales sur les commandes dont vous pouvez vous servir, utilisez `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="a6a59-113">For general information about the commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="a6a59-114">Pour obtenir de l’aide avec une seule commande, utilisez `az sf <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="a6a59-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="a6a59-115">Les commandes Service Fabric dans Azure CLI respectent le modèle d’affectation de noms suivant :</span><span class="sxs-lookup"><span data-stu-id="a6a59-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="a6a59-116">`<object>` est la cible de `<action>`.</span><span class="sxs-lookup"><span data-stu-id="a6a59-116">`<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="a6a59-117">Sélectionner un cluster</span><span class="sxs-lookup"><span data-stu-id="a6a59-117">Select a cluster</span></span>

<span data-ttu-id="a6a59-118">Avant d’effectuer toute opération, vous devez sélectionner un cluster auquel vous connecter.</span><span class="sxs-lookup"><span data-stu-id="a6a59-118">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="a6a59-119">Pour obtenir un exemple, consultez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="a6a59-119">For an example, see the following code.</span></span> <span data-ttu-id="a6a59-120">Le code se connecte à un cluster non sécurisé.</span><span class="sxs-lookup"><span data-stu-id="a6a59-120">The code connects to an unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="a6a59-121">N’utilisez pas de clusters Service Fabric non sécurisés dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a6a59-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="a6a59-122">Le point de terminaison de cluster doit inclure le préfixe `http` ou `https`.</span><span class="sxs-lookup"><span data-stu-id="a6a59-122">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="a6a59-123">Il doit inclure le port pour la passerelle HTTP.</span><span class="sxs-lookup"><span data-stu-id="a6a59-123">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="a6a59-124">Le port et l’adresse sont identiques à l’URL de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="a6a59-124">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="a6a59-125">Pour les clusters qui sont sécurisés avec un certificat, vous pouvez utiliser des fichiers non chiffrés .pem ou des fichiers .crt et .key.</span><span class="sxs-lookup"><span data-stu-id="a6a59-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="a6a59-126">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a6a59-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="a6a59-127">Pour plus d’informations, consultez [Se connecter à un cluster sécurisé](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a6a59-127">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a6a59-128">La commande `select` n’agit pas sur les demandes avant d’être renvoyée.</span><span class="sxs-lookup"><span data-stu-id="a6a59-128">The `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="a6a59-129">Pour vérifier que vous avez correctement spécifié un cluster, utilisez une commande similaire à `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="a6a59-129">To verify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="a6a59-130">Vérifiez que la commande ne renvoie pas d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="a6a59-130">Verify that the command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="a6a59-131">Opérations de base</span><span class="sxs-lookup"><span data-stu-id="a6a59-131">Basic operations</span></span>

<span data-ttu-id="a6a59-132">Les informations de connexion du cluster sont conservées dans plusieurs sessions d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a6a59-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="a6a59-133">Une fois qu’un cluster Service Fabric est sélectionné, vous pouvez exécuter n’importe quelle commande Service Fabric sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="a6a59-133">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="a6a59-134">Par exemple, pour obtenir l’état d’intégrité d’un cluster Service Fabric, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a6a59-134">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="a6a59-135">La commande génère la sortie suivante (en supposant que la sortie JSON est spécifiée dans la configuration d’Azure CLI) :</span><span class="sxs-lookup"><span data-stu-id="a6a59-135">The command results in the following output (assuming that JSON output is specified in the Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="a6a59-136">Conseils et résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a6a59-136">Tips and troubleshooting</span></span>

<span data-ttu-id="a6a59-137">Vous estimerez peut-être les informations suivantes utiles si vous rencontrez des problèmes en utilisant les commandes Service Fabric dans Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a6a59-137">You might find the following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="a6a59-138">Convertir un certificat au format PFX en PEM</span><span class="sxs-lookup"><span data-stu-id="a6a59-138">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="a6a59-139">Azure CLI prend en charge les certificats côté client comme les fichiers PEM (extension .pem).</span><span class="sxs-lookup"><span data-stu-id="a6a59-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="a6a59-140">Si vous utilisez des fichiers PFX à partir de Windows, vous devez convertir ces certificats au format PEM.</span><span class="sxs-lookup"><span data-stu-id="a6a59-140">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="a6a59-141">Pour convertir un fichier PFX en fichier PEM, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a6a59-141">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="a6a59-142">Pour plus d’informations, consultez la [documentation OpenSSL](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="a6a59-142">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="a6a59-143">Problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="a6a59-143">Connection issues</span></span>

<span data-ttu-id="a6a59-144">Certaines opérations peuvent générer le message suivant :</span><span class="sxs-lookup"><span data-stu-id="a6a59-144">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="a6a59-145">Vérifiez que le point de terminaison du cluster spécifié est disponible et à l’écoute.</span><span class="sxs-lookup"><span data-stu-id="a6a59-145">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="a6a59-146">Vérifiez également que l’interface utilisateur de Service Fabric Explorer est disponible au niveau de cet hôte et de ce port.</span><span class="sxs-lookup"><span data-stu-id="a6a59-146">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="a6a59-147">Utilisez `az sf cluster select` pour mettre à jour le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="a6a59-147">To update the endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="a6a59-148">Journaux détaillés</span><span class="sxs-lookup"><span data-stu-id="a6a59-148">Detailed logs</span></span>

<span data-ttu-id="a6a59-149">Les journaux détaillés peuvent souvent être utiles lorsque vous déboguez ou signalez un problème.</span><span class="sxs-lookup"><span data-stu-id="a6a59-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="a6a59-150">Azure CLI propose un indicateur `--debug` global qui augmente le niveau de détail des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="a6a59-150">Azure CLI offers a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="a6a59-151">Aide et syntaxe de commande</span><span class="sxs-lookup"><span data-stu-id="a6a59-151">Command help and syntax</span></span>

<span data-ttu-id="a6a59-152">Les commandes Service Fabric suivent les mêmes conventions qu’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a6a59-152">Service Fabric commands follow the same conventions as Azure CLI.</span></span> <span data-ttu-id="a6a59-153">Pour obtenir de l’aide sur une commande spécifique ou un groupe de commandes, utilisez l’indicateur `-h` :</span><span class="sxs-lookup"><span data-stu-id="a6a59-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="a6a59-154">Voici un autre exemple :</span><span class="sxs-lookup"><span data-stu-id="a6a59-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
