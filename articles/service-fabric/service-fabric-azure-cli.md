---
title: "Prise en main de l’interface de ligne de commande Azure Service Fabric XPlat"
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
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a><span data-ttu-id="8ddb4-103">Utilisation de l’interface de ligne de commande XPlat pour interagir avec un cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8ddb4-103">Using the XPlat CLI to interact with a Service Fabric cluster</span></span>

<span data-ttu-id="8ddb4-104">Vous pouvez interagir avec le cluster Service Fabric à partir de machines Linux par le biais de l’interface de ligne de commande XPlat sous Linux.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-104">You can interact with Service Fabric cluster from Linux machines using the XPlat CLI on Linux.</span></span>

<span data-ttu-id="8ddb4-105">La première étape consiste à obtenir la dernière version de l’interface de ligne de commande à partir de la représentation git et à l’installer dans votre chemin d’accès à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-105">The first step is get the latest version of the CLI from the git rep and set it up in your path using the following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="8ddb4-106">Pour chaque commande prise en charge, vous pouvez taper le nom de la commande pour obtenir de l’aide de cette commande.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-106">For each command, it supports, you can type the name of the command to obtain the help for that command.</span></span>
<span data-ttu-id="8ddb4-107">La saisie semi-automatique est prise en charge pour les commandes.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-107">Auto-completion is supported for the commands.</span></span> <span data-ttu-id="8ddb4-108">Par exemple, la commande suivante vous aide pour toutes les commandes de l’application.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-108">For example, the following command gives you help for all the application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="8ddb4-109">Vous pouvez filtrer davantage l’aide pour une commande spécifique, comme le montre l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-109">You can further filter the help to a specific command, as the following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="8ddb4-110">Pour activer la saisie semi-automatique dans l’interface de ligne de commande, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-110">To enable auto-completion in the CLI, run the following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="8ddb4-111">Les commandes suivantes se connectent au cluster et vous montrent les nœuds du cluster :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-111">The following commands connect to the cluster and show you the nodes in the cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="8ddb4-112">Pour utiliser des paramètres nommés et trouver à quoi ils correspondent, vous pouvez taper --aide après une commande.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-112">To use named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="8ddb4-113">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="8ddb4-114">Lors de la connexion à un cluster de plusieurs ordinateurs à partir d’un ordinateur **qui ne fait pas partie du cluster**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-114">When connecting to a multi-machine cluster from a machine **that is not part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="8ddb4-115">Remplacez la balise PublicIPorFQDN avec l’IP réelle ou le nom de domaine complet comme il convient.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-115">Replace the PublicIPorFQDN tag with the real IP or FQDN as appropriate.</span></span> <span data-ttu-id="8ddb4-116">Lors de la connexion à un cluster de plusieurs ordinateurs à partir d’un ordinateur **qui fait partie du cluster**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-116">When connecting to a multi-machine cluster from a machine **that is part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="8ddb4-117">Vous pouvez utiliser PowerShell ou l’interface de ligne de commende pour interagir avec votre cluster Service Fabric Linux créé via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-117">You can use PowerShell or CLI to interact with your Linux Service Fabric Cluster created through the Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="8ddb4-118">Ces clusters ne sont pas sécurisés, par conséquent, vous pouvez ouvrir votre boîtier unique en ajoutant l’adresse IP publique dans le manifeste de cluster.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding the public IP address in the cluster manifest.</span></span>

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a><span data-ttu-id="8ddb4-119">Utilisation de l’interface de ligne de commande XPlat pour se connecter à un cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8ddb4-119">Using the XPlat CLI to connect to a Service Fabric cluster</span></span>

<span data-ttu-id="8ddb4-120">Les commandes de l’interface de ligne de commande Azure ci-après expliquent comment se connecter à un cluster sécurisé.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-120">The following Azure CLI commands describe how to connect to a secure cluster.</span></span> <span data-ttu-id="8ddb4-121">Les détails du certificat doivent correspondre à un certificat sur les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-121">The certificate details must match a certificate on the cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="8ddb4-122">Si votre certificat est associé à des autorités de certification, vous devez ajouter le paramètre --ca-cert-path comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-122">If your certificate has Certificate Authorities (CAs), you need to add the --ca-cert-path parameter like the following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="8ddb4-123">Si vous saisissez plusieurs autorités de certification, utilisez des virgules comme délimiteurs.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-123">If you have multiple CAs, use a comma as the delimiter.</span></span>

<span data-ttu-id="8ddb4-124">Si le nom commun du certificat ne correspond pas au point de terminaison de connexion, vous pouvez utiliser le paramètre `--strict-ssl-false` pour ignorer la vérification, comme indiqué dans la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-124">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification as shown in the following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="8ddb4-125">Si vous souhaitez ignorer l’étape de vérification de l’autorité de certification, vous pouvez ajouter le paramètre --reject-unauthorized-false, comme indiqué dans la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-125">If you would like to skip the CA verification, you could add the --reject-unauthorized-false parameter as shown in the following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="8ddb4-126">Une fois que vous vous êtes connecté, vous devez être en mesure d’exécuter d’autres commandes d’interface de ligne de commande pour interagir avec le cluster.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-126">After you connect, you should be able to run other CLI commands to interact with the cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="8ddb4-127">Déploiement de votre application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8ddb4-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="8ddb4-128">Exécutez les commandes suivantes pour copier, inscrire et démarrer l’application Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-128">Execute the following commands to copy, register, and start the service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="8ddb4-129">Mettre à niveau votre application</span><span class="sxs-lookup"><span data-stu-id="8ddb4-129">Upgrading your application</span></span>

<span data-ttu-id="8ddb4-130">Le processus est similaire au [processus dans Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="8ddb4-130">The process is similar to the [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="8ddb4-131">Construisez, copiez, enregistrez et créez votre application à partir du répertoire racine du projet.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="8ddb4-132">Si votre instance d’application se nomme `fabric:/MySFApp` et si le type est MySFApp, les commandes se présentent comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-132">If your application instance is named `fabric:/MySFApp`, and the type is MySFApp, the commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="8ddb4-133">Modifiez votre application et reconstruisez le service modifié.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-133">Make the change to your application and rebuild the modified service.</span></span>  <span data-ttu-id="8ddb4-134">Mettez à jour le fichier manifeste du service modifié (ServiceManifest.xml) avec les versions mises à jour du Service (Code, Config ou Données comme il convient).</span><span class="sxs-lookup"><span data-stu-id="8ddb4-134">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="8ddb4-135">Modifiez également le manifeste de l’application (ApplicationManifest.xml) avec le numéro de version mis à jour de l’application et le service modifié.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-135">Also modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application, and the modified service.</span></span>  <span data-ttu-id="8ddb4-136">Copiez et enregistrez votre application mise à jour en utilisant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-136">Now, copy and register your updated application using the following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="8ddb4-137">Vous pouvez désormais démarrer la mise à niveau de l’application avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-137">Now, you can start the application upgrade with the following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="8ddb4-138">Vous pouvez contrôler la mise à niveau de l’application à l’aide de SFX.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-138">You can now monitor the application upgrade using SFX.</span></span> <span data-ttu-id="8ddb4-139">Dans quelques minutes, l’application aura été mise à jour.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-139">In a few minutes, the application would have been updated.</span></span> <span data-ttu-id="8ddb4-140">Vous pouvez également essayer une application mise à jour avec une erreur et vérifiez la fonctionnalité de restauration automatique dans Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-140">You can also try an updated app with an error and check the auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a><span data-ttu-id="8ddb4-141">Conversion de PFX vers PEM et vice versa</span><span class="sxs-lookup"><span data-stu-id="8ddb4-141">Converting from PFX to PEM and vice versa</span></span>

<span data-ttu-id="8ddb4-142">Vous devrez peut-être installer un certificat sur votre ordinateur local (avec Windows ou Linux) pour accéder aux clusters sécurisés dans un environnement différent.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-142">You might need to install a certificate in your local machine (with Windows or Linux) to access secure clusters that may be in a different environment.</span></span> <span data-ttu-id="8ddb4-143">Par exemple, lorsque vous accédez à un cluster Linux sécurisé à partir d’un ordinateur Windows et vice versa, vous devrez convertir votre certificat du format PFX vers PEM et vice versa.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need to convert your certificate from PFX to PEM and vice versa.</span></span> 

<span data-ttu-id="8ddb4-144">Pour convertir un fichier PEM en fichier PFX, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-144">To convert from a PEM file to a PFX file, use the following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="8ddb4-145">Pour convertir un fichier PFX en fichier PEM, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-145">To convert from a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="8ddb4-146">Reportez-vous à la [documentation OpenSSL](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-146">Refer to [OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="8ddb4-147">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="8ddb4-147">Troubleshooting</span></span>


### <a name="copying-of-the-application-package-does-not-succeed"></a><span data-ttu-id="8ddb4-148">Échec de la copie du package d’application</span><span class="sxs-lookup"><span data-stu-id="8ddb4-148">Copying of the application package does not succeed</span></span>

<span data-ttu-id="8ddb4-149">Vérifiez si `openssh` est installé.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="8ddb4-150">Par défaut, cet élément n’est pas installé sur le bureau Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="8ddb4-151">Installez-le en utilisant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-151">Install it using the following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="8ddb4-152">Si le problème persiste, essayez de désactiver PAM pour ssh en modifiant le fichier `sshd_config` à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-152">If the problem persists, try disabling PAM for ssh by changing the `sshd_config` file using the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="8ddb4-153">Si le problème persiste, essayez d’augmenter le nombre de sessions ssh en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ddb4-153">If the problem still persists, try increasing the number of ssh sessions by executing the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="8ddb4-154">L’utilisation des clés pour l’authentification ssh (par opposition aux mots de passe) n’étant pas encore prise en charge (puisque la plate-forme utilise ssh pour copier les packages), utilisez plutôt l’authentification par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-154">Using keys for ssh authentication (as opposed to passwords) isn't yet supported (since the platform uses ssh to copy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ddb4-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ddb4-155">Next steps</span></span>

[<span data-ttu-id="8ddb4-156">Configurez l’environnement de développement et déployez une application Service Fabric vers un cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="8ddb4-156">Set up the development environment and deploy a Service Fabric application to a Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="8ddb4-157">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="8ddb4-157">Related articles</span></span>

* [<span data-ttu-id="8ddb4-158">Prise en main de Service Fabric et d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ddb4-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
