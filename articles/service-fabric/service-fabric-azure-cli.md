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
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a><span data-ttu-id="f5701-103">À l’aide de hello XPlat CLI toointeract avec un cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f5701-103">Using hello XPlat CLI toointeract with a Service Fabric cluster</span></span>

<span data-ttu-id="f5701-104">Vous pouvez interagir avec le cluster Service Fabric à partir d’ordinateurs Linux à l’aide de hello XPlat CLI sur Linux.</span><span class="sxs-lookup"><span data-stu-id="f5701-104">You can interact with Service Fabric cluster from Linux machines using hello XPlat CLI on Linux.</span></span>

<span data-ttu-id="f5701-105">première étape de Hello est obtenir la dernière version de hello Hello CLI à partir de rep de git hello et ensemble dans votre chemin d’accès à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="f5701-105">hello first step is get hello latest version of hello CLI from hello git rep and set it up in your path using hello following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="f5701-106">Pour chaque commande, il prend en charge, vous pouvez taper le nom de hello de hello commande tooobtain hello d’aide pour cette commande.</span><span class="sxs-lookup"><span data-stu-id="f5701-106">For each command, it supports, you can type hello name of hello command tooobtain hello help for that command.</span></span>
<span data-ttu-id="f5701-107">La saisie semi-automatique est pris en charge pour les commandes hello.</span><span class="sxs-lookup"><span data-stu-id="f5701-107">Auto-completion is supported for hello commands.</span></span> <span data-ttu-id="f5701-108">Par exemple, hello suivant donne de commande que vous aide pour toutes les commandes d’application hello.</span><span class="sxs-lookup"><span data-stu-id="f5701-108">For example, hello following command gives you help for all hello application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="f5701-109">Vous pouvez filtrer davantage d’aide tooa spécifique la commande hello comme hello suivant montre l’exemple :</span><span class="sxs-lookup"><span data-stu-id="f5701-109">You can further filter hello help tooa specific command, as hello following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="f5701-110">tooenable la saisie semi-automatique dans hello CLI, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="f5701-110">tooenable auto-completion in hello CLI, run hello following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="f5701-111">Hello suivant les commandes connecter toohello cluster et afficher hello de nœuds de cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="f5701-111">hello following commands connect toohello cluster and show you hello nodes in hello cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="f5701-112">toouse de paramètres nommés et de trouver ce qu’ils sont, vous pouvez taper--aide après une commande.</span><span class="sxs-lookup"><span data-stu-id="f5701-112">toouse named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="f5701-113">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f5701-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="f5701-114">Lors de la connexion de cluster de plusieurs ordinateurs tooa à partir d’un ordinateur **qui ne fait pas partie du cluster de hello**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5701-114">When connecting tooa multi-machine cluster from a machine **that is not part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="f5701-115">Remplacer la balise de PublicIPorFQDN hello avec l’adresse IP réelle de hello ou le nom de domaine complet comme il convient.</span><span class="sxs-lookup"><span data-stu-id="f5701-115">Replace hello PublicIPorFQDN tag with hello real IP or FQDN as appropriate.</span></span> <span data-ttu-id="f5701-116">Lors de la connexion de cluster de plusieurs ordinateurs tooa à partir d’un ordinateur **qui fait partie du cluster de hello**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5701-116">When connecting tooa multi-machine cluster from a machine **that is part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="f5701-117">Vous pouvez utiliser PowerShell ou toointeract CLI avec votre Cluster Linux Service Fabric créé via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f5701-117">You can use PowerShell or CLI toointeract with your Linux Service Fabric Cluster created through hello Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="f5701-118">Ces clusters non sécurisés, par conséquent, vous pouvez ouvrir votre boîte de dialogue un en ajoutant l’adresse IP publique de hello dans le manifeste du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f5701-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding hello public IP address in hello cluster manifest.</span></span>

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a><span data-ttu-id="f5701-119">À l’aide de hello cluster Service Fabric de XPlat CLI tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="f5701-119">Using hello XPlat CLI tooconnect tooa Service Fabric cluster</span></span>

<span data-ttu-id="f5701-120">Hello suivant des commandes CLI d’Azure décrire comment tooconnect tooa sécuriser le cluster.</span><span class="sxs-lookup"><span data-stu-id="f5701-120">hello following Azure CLI commands describe how tooconnect tooa secure cluster.</span></span> <span data-ttu-id="f5701-121">Détails du certificat Hello doivent correspondre à un certificat sur les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f5701-121">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="f5701-122">Si votre certificat a des autorités de certification (CA), vous avez besoin de paramètre de l’autorité de certification---cert-path tooadd hello comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f5701-122">If your certificate has Certificate Authorities (CAs), you need tooadd hello --ca-cert-path parameter like hello following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="f5701-123">Si vous avez plusieurs autorités de certification, utilisez une virgule comme délimiteur de hello.</span><span class="sxs-lookup"><span data-stu-id="f5701-123">If you have multiple CAs, use a comma as hello delimiter.</span></span>

<span data-ttu-id="f5701-124">Si votre nom commun hello certificat ne correspond pas de point de terminaison de connexion hello, vous pouvez utiliser le paramètre hello `--strict-ssl-false` toobypass hello vérification comme indiqué dans hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5701-124">If your Common Name in hello certificate does not match hello connection endpoint, you could use hello parameter `--strict-ssl-false` toobypass hello verification as shown in hello following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="f5701-125">Si vous souhaitez que la vérification de tooskip hello autorité de certification, vous pouvez ajouter hello--paramètre false rejet non autorisé comme indiqué dans hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5701-125">If you would like tooskip hello CA verification, you could add hello --reject-unauthorized-false parameter as shown in hello following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="f5701-126">Une fois que vous vous connectez, vous devez être en mesure de toorun autres toointeract de commandes CLI avec cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f5701-126">After you connect, you should be able toorun other CLI commands toointeract with hello cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="f5701-127">Déploiement de votre application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f5701-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="f5701-128">Exécutez hello suivant les commandes toocopy, inscrire et démarrer l’application hello service fabric :</span><span class="sxs-lookup"><span data-stu-id="f5701-128">Execute hello following commands toocopy, register, and start hello service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="f5701-129">Mettre à niveau votre application</span><span class="sxs-lookup"><span data-stu-id="f5701-129">Upgrading your application</span></span>

<span data-ttu-id="f5701-130">les processus Hello sont similaire toohello [processus dans Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="f5701-130">hello process is similar toohello [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="f5701-131">Construisez, copiez, enregistrez et créez votre application à partir du répertoire racine du projet.</span><span class="sxs-lookup"><span data-stu-id="f5701-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="f5701-132">Si votre instance de l’application se nomme `fabric:/MySFApp`et le type de hello est MySFApp, commandes hello serait comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5701-132">If your application instance is named `fabric:/MySFApp`, and hello type is MySFApp, hello commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="f5701-133">Apportez hello modification tooyour application et régénérer hello modifié service.</span><span class="sxs-lookup"><span data-stu-id="f5701-133">Make hello change tooyour application and rebuild hello modified service.</span></span>  <span data-ttu-id="f5701-134">Hello de mise à jour modifié fichier manifeste du service (ServiceManifest.xml) avec les versions de mise à jour de hello pour hello Service (et Code ou configuration ou les données selon le cas).</span><span class="sxs-lookup"><span data-stu-id="f5701-134">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="f5701-135">En outre modifier le manifeste de l’application hello (ApplicationManifest.xml) avec le numéro de version hello mis à jour pour l’application hello et hello service modifié.</span><span class="sxs-lookup"><span data-stu-id="f5701-135">Also modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application, and hello modified service.</span></span>  <span data-ttu-id="f5701-136">Maintenant, copier et enregistrer votre application mis à jour à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="f5701-136">Now, copy and register your updated application using hello following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="f5701-137">Vous pouvez désormais mise à niveau des applications hello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5701-137">Now, you can start hello application upgrade with hello following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="f5701-138">Vous pouvez désormais analyser mise à niveau de l’application hello à l’aide de SFX.</span><span class="sxs-lookup"><span data-stu-id="f5701-138">You can now monitor hello application upgrade using SFX.</span></span> <span data-ttu-id="f5701-139">Dans quelques minutes, application hello serait ont été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="f5701-139">In a few minutes, hello application would have been updated.</span></span> <span data-ttu-id="f5701-140">Vous pouvez également essayer d’une application de mise à jour avec une erreur et vérifier la fonctionnalité de restauration automatique hello dans l’infrastructure de service.</span><span class="sxs-lookup"><span data-stu-id="f5701-140">You can also try an updated app with an error and check hello auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-toopem-and-vice-versa"></a><span data-ttu-id="f5701-141">Conversion de PFX tooPEM et vice versa</span><span class="sxs-lookup"><span data-stu-id="f5701-141">Converting from PFX tooPEM and vice versa</span></span>

<span data-ttu-id="f5701-142">Vous devrez peut-être tooinstall un certificat de vos clusters de sécurisé tooaccess ordinateur local (Windows ou Linux) qui peuvent être dans un autre environnement.</span><span class="sxs-lookup"><span data-stu-id="f5701-142">You might need tooinstall a certificate in your local machine (with Windows or Linux) tooaccess secure clusters that may be in a different environment.</span></span> <span data-ttu-id="f5701-143">Par exemple, lors de l’accès à un cluster sécurisé de Linux à partir d’un ordinateur Windows et vice versa vous devrez peut-être tooconvert votre certificat PFX tooPEM et vice versa.</span><span class="sxs-lookup"><span data-stu-id="f5701-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need tooconvert your certificate from PFX tooPEM and vice versa.</span></span> 

<span data-ttu-id="f5701-144">tooconvert d’un fichier dans PEM fichier tooa PFX, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5701-144">tooconvert from a PEM file tooa PFX file, use hello following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="f5701-145">tooconvert d’un fichier PEM de la tooa d’un fichier PFX, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5701-145">tooconvert from a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="f5701-146">Consultez trop[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="f5701-146">Refer too[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="f5701-147">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="f5701-147">Troubleshooting</span></span>


### <a name="copying-of-hello-application-package-does-not-succeed"></a><span data-ttu-id="f5701-148">Copie du package d’application hello ne réussit pas</span><span class="sxs-lookup"><span data-stu-id="f5701-148">Copying of hello application package does not succeed</span></span>

<span data-ttu-id="f5701-149">Vérifiez si `openssh` est installé.</span><span class="sxs-lookup"><span data-stu-id="f5701-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="f5701-150">Par défaut, cet élément n’est pas installé sur le bureau Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f5701-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="f5701-151">Installer à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5701-151">Install it using hello following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="f5701-152">Si hello problème persiste, essayez de désactiver PAM pour ssh en modifiant hello `sshd_config` fichier à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="f5701-152">If hello problem persists, try disabling PAM for ssh by changing hello `sshd_config` file using hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="f5701-153">Si hello problème persiste, essayez de nombre hello croissant de ssh sessions en exécutant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="f5701-153">If hello problem still persists, try increasing hello number of ssh sessions by executing hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="f5701-154">À l’aide de clés pour ssh authentification (en opposition toopasswords) n’est pas encore prise en charge (comme plateforme de hello utilise ssh toocopy packages), par conséquent, utilisez l’authentification du mot de passe à la place.</span><span class="sxs-lookup"><span data-stu-id="f5701-154">Using keys for ssh authentication (as opposed toopasswords) isn't yet supported (since hello platform uses ssh toocopy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5701-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f5701-155">Next steps</span></span>

[<span data-ttu-id="f5701-156">Configuration d’environnement de développement hello et déployer un cluster de Service Fabric application tooa Linux.</span><span class="sxs-lookup"><span data-stu-id="f5701-156">Set up hello development environment and deploy a Service Fabric application tooa Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="f5701-157">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="f5701-157">Related articles</span></span>

* [<span data-ttu-id="f5701-158">Prise en main de Service Fabric et d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f5701-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
