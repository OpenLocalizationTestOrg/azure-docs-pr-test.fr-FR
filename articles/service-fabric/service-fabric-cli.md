---
title: "Prise en main de l’interface de ligne de commande Azure Service Fabric (sfctl)"
description: "Découvrez comment utiliser l’interface de ligne de commande Azure Service Fabric. Apprenez à vous connecter à un cluster et à gérer des applications."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: 5ce9adf6c82e3a5521883c5de1e0689d5bf0d94e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="7c49b-104">Ligne de commande Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7c49b-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="7c49b-105">L’interface de ligne de commande Azure Service Fabric (sfctl) est un utilitaire de la ligne de commande pour l’interaction et de la gestion des entités Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7c49b-105">The Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="7c49b-106">Sfctl peut être utilisé avec des clusters Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="7c49b-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="7c49b-107">Sfctl s’exécute sur toute plateforme prenant en charge python.</span><span class="sxs-lookup"><span data-stu-id="7c49b-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c49b-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7c49b-108">Prerequisites</span></span>

<span data-ttu-id="7c49b-109">Avant l’installation, vérifiez que python et pip sont installés dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="7c49b-109">Prior to installation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="7c49b-110">Pour plus d’informations, examinez la [documentation de démarrage rapide de pip](https://pip.pypa.io/en/latest/quickstart/)et la [documentation d’installation officielle de python](https://wiki.python.org/moin/BeginnersGuide/Download).</span><span class="sxs-lookup"><span data-stu-id="7c49b-110">For more information, take a look at the [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="7c49b-111">Il est recommandé d’utiliser python 3.6 même si python 2.7 et 3.6 sont tous deux pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7c49b-111">While both python 2.7 and 3.6 are supported, it is recommended to use python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="7c49b-112">Installer</span><span class="sxs-lookup"><span data-stu-id="7c49b-112">Install</span></span>

<span data-ttu-id="7c49b-113">L’ interface de ligne de commande Azure Service Fabric (sfctl) est empaquetée en tant que package python.</span><span class="sxs-lookup"><span data-stu-id="7c49b-113">The Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="7c49b-114">Pour installer la version la plus récente, exécutez :</span><span class="sxs-lookup"><span data-stu-id="7c49b-114">To install the latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="7c49b-115">Après l’installation, exécutez `sfctl -h` pour obtenir des informations sur les commandes disponibles.</span><span class="sxs-lookup"><span data-stu-id="7c49b-115">After installation, run `sfctl -h` to get information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="7c49b-116">Syntaxe d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7c49b-116">CLI syntax</span></span>

<span data-ttu-id="7c49b-117">Les commandes sont toujours préfixées avec `sfctl`.</span><span class="sxs-lookup"><span data-stu-id="7c49b-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="7c49b-118">Pour obtenir des informations générales sur les commandes dont vous pouvez vous servir, utilisez `sfctl -h`.</span><span class="sxs-lookup"><span data-stu-id="7c49b-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="7c49b-119">Pour obtenir de l’aide avec une seule commande, utilisez `sfctl <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="7c49b-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="7c49b-120">Les commandes suivent une structure renouvelée, avec la cible de la commande qui précède le verbe ou l’action :</span><span class="sxs-lookup"><span data-stu-id="7c49b-120">Commands follow a repeatable structure, with the target of the command preceding the verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="7c49b-121">Dans cet exemple, `<object>` est la cible de `<action>`.</span><span class="sxs-lookup"><span data-stu-id="7c49b-121">In this example, `<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="7c49b-122">Sélectionner un cluster</span><span class="sxs-lookup"><span data-stu-id="7c49b-122">Select a cluster</span></span>

<span data-ttu-id="7c49b-123">Avant d’effectuer toute opération, vous devez sélectionner un cluster auquel vous connecter.</span><span class="sxs-lookup"><span data-stu-id="7c49b-123">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="7c49b-124">Vous pouvez par exemple exécuter la commande suivante pour sélectionner un cluster et vous y connecter avec le nom `testcluster.com`.</span><span class="sxs-lookup"><span data-stu-id="7c49b-124">For example, run the following to select and connect to the cluster with the name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="7c49b-125">N’utilisez pas de clusters Service Fabric non sécurisés dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7c49b-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="7c49b-126">Le point de terminaison de cluster doit inclure le préfixe `http` ou `https`.</span><span class="sxs-lookup"><span data-stu-id="7c49b-126">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="7c49b-127">Il doit inclure le port pour la passerelle HTTP.</span><span class="sxs-lookup"><span data-stu-id="7c49b-127">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="7c49b-128">Le port et l’adresse sont identiques à l’URL de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="7c49b-128">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="7c49b-129">Pour les clusters qui sont sécurisés avec un certificat, vous pouvez spécifier un certificat PEM encodé.</span><span class="sxs-lookup"><span data-stu-id="7c49b-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="7c49b-130">Le certificat peut être spécifié en tant que fichier unique ou en tant qu’ensemble de cert et de clé.</span><span class="sxs-lookup"><span data-stu-id="7c49b-130">The certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="7c49b-131">Pour plus d’informations, consultez [Se connecter à un cluster sécurisé](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="7c49b-131">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="7c49b-132">Opérations de base</span><span class="sxs-lookup"><span data-stu-id="7c49b-132">Basic operations</span></span>

<span data-ttu-id="7c49b-133">Les informations de connexion du cluster persistent dans plusieurs sessions sfctl.</span><span class="sxs-lookup"><span data-stu-id="7c49b-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="7c49b-134">Une fois qu’un cluster Service Fabric est sélectionné, vous pouvez exécuter n’importe quelle commande Service Fabric sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="7c49b-134">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="7c49b-135">Par exemple, pour obtenir l’état d’intégrité d’un cluster Service Fabric, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c49b-135">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="7c49b-136">La commande débouche sur le résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="7c49b-136">The command results in the following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="7c49b-137">Conseils et résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="7c49b-137">Tips and troubleshooting</span></span>

<span data-ttu-id="7c49b-138">Quelques suggestions et conseils pour la résolution des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="7c49b-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="7c49b-139">Convertir un certificat au format PFX en PEM</span><span class="sxs-lookup"><span data-stu-id="7c49b-139">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="7c49b-140">L’interface de ligne de commande Service Fabric prend en charge les certificats côté client en tant que fichiers PEM (extension .pem).</span><span class="sxs-lookup"><span data-stu-id="7c49b-140">The Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="7c49b-141">Si vous utilisez des fichiers PFX à partir de Windows, vous devez convertir ces certificats au format PEM.</span><span class="sxs-lookup"><span data-stu-id="7c49b-141">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="7c49b-142">Pour convertir un fichier PFX en fichier PEM, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c49b-142">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="7c49b-143">Pour plus d’informations, consultez la [documentation OpenSSL](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="7c49b-143">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="7c49b-144">Problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="7c49b-144">Connection issues</span></span>

<span data-ttu-id="7c49b-145">Certaines opérations peuvent générer le message suivant :</span><span class="sxs-lookup"><span data-stu-id="7c49b-145">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="7c49b-146">Vérifiez que le point de terminaison du cluster spécifié est disponible et à l’écoute.</span><span class="sxs-lookup"><span data-stu-id="7c49b-146">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="7c49b-147">Vérifiez également que l’interface utilisateur de Service Fabric Explorer est disponible au niveau de cet hôte et de ce port.</span><span class="sxs-lookup"><span data-stu-id="7c49b-147">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="7c49b-148">Utilisez `sfctl cluster select` pour mettre à jour le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7c49b-148">To update the endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="7c49b-149">Journaux détaillés</span><span class="sxs-lookup"><span data-stu-id="7c49b-149">Detailed logs</span></span>

<span data-ttu-id="7c49b-150">Les journaux détaillés peuvent souvent être utiles lorsque vous déboguez ou signalez un problème.</span><span class="sxs-lookup"><span data-stu-id="7c49b-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="7c49b-151">Il existe un indicateur `--debug` général qui accroît les commentaires des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="7c49b-151">There is a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="7c49b-152">Aide et syntaxe de commande</span><span class="sxs-lookup"><span data-stu-id="7c49b-152">Command help and syntax</span></span>

<span data-ttu-id="7c49b-153">Pour obtenir de l’aide sur une commande spécifique ou un groupe de commandes, utilisez l’indicateur `-h` :</span><span class="sxs-lookup"><span data-stu-id="7c49b-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="7c49b-154">Autre exemple :</span><span class="sxs-lookup"><span data-stu-id="7c49b-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="7c49b-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c49b-155">Next steps</span></span>

* [<span data-ttu-id="7c49b-156">Déployer une application avec l’interface de ligne de commande Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7c49b-156">Deploy an application with the Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="7c49b-157">Prise en main de Service Fabric sur Linux</span><span class="sxs-lookup"><span data-stu-id="7c49b-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
