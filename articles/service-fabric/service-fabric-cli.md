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
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="bb472-104">Ligne de commande Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bb472-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="bb472-105">Bonjour Azure Service Fabric CLI (sfctl) est un utilitaire de ligne de commande pour l’interaction et de la gestion des entités de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb472-105">hello Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="bb472-106">Sfctl peut être utilisé avec des clusters Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="bb472-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="bb472-107">Sfctl s’exécute sur toute plateforme prenant en charge python.</span><span class="sxs-lookup"><span data-stu-id="bb472-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb472-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bb472-108">Prerequisites</span></span>

<span data-ttu-id="bb472-109">Tooinstallation préalable, assurez-vous que votre environnement a python et pip installé.</span><span class="sxs-lookup"><span data-stu-id="bb472-109">Prior tooinstallation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="bb472-110">Pour plus d’informations, examinez hello [pip documentation de démarrage rapide](https://pip.pypa.io/en/latest/quickstart/)et officiel [python installer la documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span><span class="sxs-lookup"><span data-stu-id="bb472-110">For more information, take a look at hello [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="bb472-111">Si les deux python 2.7 et 3.6 est prises en charge, il est recommandé de toouse python 3.6.</span><span class="sxs-lookup"><span data-stu-id="bb472-111">While both python 2.7 and 3.6 are supported, it is recommended toouse python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="bb472-112">Installer</span><span class="sxs-lookup"><span data-stu-id="bb472-112">Install</span></span>

<span data-ttu-id="bb472-113">Bonjour Azure Service Fabric CLI (sfctl) est fourni comme un package python.</span><span class="sxs-lookup"><span data-stu-id="bb472-113">hello Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="bb472-114">tooinstall hello version la plus récente s’exécuter :</span><span class="sxs-lookup"><span data-stu-id="bb472-114">tooinstall hello latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="bb472-115">Après l’installation, exécutez `sfctl -h` tooget plus d’informations sur les commandes disponibles.</span><span class="sxs-lookup"><span data-stu-id="bb472-115">After installation, run `sfctl -h` tooget information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="bb472-116">Syntaxe d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb472-116">CLI syntax</span></span>

<span data-ttu-id="bb472-117">Les commandes sont toujours préfixées avec `sfctl`.</span><span class="sxs-lookup"><span data-stu-id="bb472-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="bb472-118">Pour obtenir des informations générales sur les commandes dont vous pouvez vous servir, utilisez `sfctl -h`.</span><span class="sxs-lookup"><span data-stu-id="bb472-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="bb472-119">Pour obtenir de l’aide avec une seule commande, utilisez `sfctl <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="bb472-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="bb472-120">Commandes suivent une structure reproductible, avec une cible de hello hello de commandes de verbe de hello ou l’action précédente :</span><span class="sxs-lookup"><span data-stu-id="bb472-120">Commands follow a repeatable structure, with hello target of hello command preceding hello verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="bb472-121">Dans cet exemple, `<object>` est cible hello pour `<action>`.</span><span class="sxs-lookup"><span data-stu-id="bb472-121">In this example, `<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="bb472-122">Sélectionner un cluster</span><span class="sxs-lookup"><span data-stu-id="bb472-122">Select a cluster</span></span>

<span data-ttu-id="bb472-123">Avant d’effectuer des opérations, vous devez sélectionner un tooconnect de cluster à.</span><span class="sxs-lookup"><span data-stu-id="bb472-123">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="bb472-124">Par exemple, exécutez hello suivant tooselect et se connecter toohello cluster avec le nom de hello `testcluster.com`.</span><span class="sxs-lookup"><span data-stu-id="bb472-124">For example, run hello following tooselect and connect toohello cluster with hello name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="bb472-125">N’utilisez pas de clusters Service Fabric non sécurisés dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bb472-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="bb472-126">point de terminaison Hello cluster doit être préfixé par `http` ou `https`.</span><span class="sxs-lookup"><span data-stu-id="bb472-126">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="bb472-127">Il doit inclure le port hello pour la passerelle HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="bb472-127">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="bb472-128">adresse et le port de hello sont hello identique hello URL de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="bb472-128">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="bb472-129">Pour les clusters qui sont sécurisés avec un certificat, vous pouvez spécifier un certificat PEM encodé.</span><span class="sxs-lookup"><span data-stu-id="bb472-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="bb472-130">certificat de Hello peut être spécifié en tant qu’un seul fichier ou le certificat et la paire de clés.</span><span class="sxs-lookup"><span data-stu-id="bb472-130">hello certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="bb472-131">Pour plus d’informations, consultez [cluster Azure Service Fabric sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="bb472-131">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="bb472-132">Opérations de base</span><span class="sxs-lookup"><span data-stu-id="bb472-132">Basic operations</span></span>

<span data-ttu-id="bb472-133">Les informations de connexion du cluster persistent dans plusieurs sessions sfctl.</span><span class="sxs-lookup"><span data-stu-id="bb472-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="bb472-134">Après avoir sélectionné un cluster Service Fabric, vous pouvez exécuter n’importe quelle commande de l’infrastructure de Service sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="bb472-134">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="bb472-135">Par exemple, tooget hello état d’intégrité de cluster Service Fabric, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bb472-135">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="bb472-136">résultats de la commande Hello Bonjour suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="bb472-136">hello command results in hello following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="bb472-137">Conseils et résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="bb472-137">Tips and troubleshooting</span></span>

<span data-ttu-id="bb472-138">Quelques suggestions et conseils pour la résolution des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="bb472-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="bb472-139">Convertir un certificat PFX tooPEM format</span><span class="sxs-lookup"><span data-stu-id="bb472-139">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="bb472-140">Hello Service Fabric CLI prend en charge les certificats côté client en tant que les fichiers PEM (extension .pem).</span><span class="sxs-lookup"><span data-stu-id="bb472-140">hello Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="bb472-141">Si vous utilisez des fichiers PFX à partir de Windows, vous devez convertir ces format tooPEM de certificats.</span><span class="sxs-lookup"><span data-stu-id="bb472-141">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="bb472-142">tooconvert un fichier PEM de tooa du fichier PFX, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bb472-142">tooconvert a PFX file tooa PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="bb472-143">Pour plus d’informations, consultez hello [OpenSSL documentation](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="bb472-143">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="bb472-144">Problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="bb472-144">Connection issues</span></span>

<span data-ttu-id="bb472-145">Certaines opérations peuvent générer hello message suivant :</span><span class="sxs-lookup"><span data-stu-id="bb472-145">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="bb472-146">Vérifiez que hello spécifié de point de terminaison de cluster est disponible et à l’écoute.</span><span class="sxs-lookup"><span data-stu-id="bb472-146">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="bb472-147">En outre, vérifiez que hello que l’interface utilisateur de Service Fabric Explorer est disponible à l’hôte et le port.</span><span class="sxs-lookup"><span data-stu-id="bb472-147">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="bb472-148">point de terminaison de hello tooupdate, utilisez `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="bb472-148">tooupdate hello endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="bb472-149">Journaux détaillés</span><span class="sxs-lookup"><span data-stu-id="bb472-149">Detailed logs</span></span>

<span data-ttu-id="bb472-150">Les journaux détaillés peuvent souvent être utiles lorsque vous déboguez ou signalez un problème.</span><span class="sxs-lookup"><span data-stu-id="bb472-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="bb472-151">Il existe un global `--debug` indicateur qui augmente de détail hello de fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="bb472-151">There is a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="bb472-152">Aide et syntaxe de commande</span><span class="sxs-lookup"><span data-stu-id="bb472-152">Command help and syntax</span></span>

<span data-ttu-id="bb472-153">Pour l’aide sur une commande spécifique ou un groupe de commandes, utilisez hello `-h` indicateur :</span><span class="sxs-lookup"><span data-stu-id="bb472-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="bb472-154">Autre exemple :</span><span class="sxs-lookup"><span data-stu-id="bb472-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="bb472-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bb472-155">Next steps</span></span>

* [<span data-ttu-id="bb472-156">Déployer une application avec hello CLI d’Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bb472-156">Deploy an application with hello Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="bb472-157">Prise en main de Service Fabric sur Linux</span><span class="sxs-lookup"><span data-stu-id="bb472-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
