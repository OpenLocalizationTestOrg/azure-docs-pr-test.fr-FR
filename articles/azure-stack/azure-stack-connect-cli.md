---
title: "aaaConnect tooAzure pile avec l’interface CLI | Documents Microsoft"
description: "Découvrez comment toouse hello (CLI) d’une interface de ligne inter-plateformes toomanage et déployer des ressources sur la pile de Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: ffb1ffd2b7784e188487bef98fe5b2add8e96784
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-cli-for-use-with-azure-stack"></a><span data-ttu-id="4f445-103">Installer et configurer l’interface CLI pour une utilisation avec Azure Stack</span><span class="sxs-lookup"><span data-stu-id="4f445-103">Install and configure CLI for use with Azure Stack</span></span>

<span data-ttu-id="4f445-104">Dans ce document, nous vous guidera hello d’utilisation des ressources de Kit de développement Azure pile toomanage Azure Interface de ligne de commande (CLI) à partir de plateformes de client Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="4f445-104">In this document, we guide you through hello process of using Azure Command-line Interface (CLI) toomanage Azure Stack Development Kit resources from Linux and Mac client platforms.</span></span> 

## <a name="export-hello-azure-stack-ca-root-certificate"></a><span data-ttu-id="4f445-105">Exporter le certificat de hello Azure pile autorité de certification racine</span><span class="sxs-lookup"><span data-stu-id="4f445-105">Export hello Azure Stack CA root certificate</span></span>

<span data-ttu-id="4f445-106">Si vous utilisez l’interface CLI à partir d’un ordinateur virtuel qui est en cours d’exécution dans l’environnement du Kit de développement de pile Azure hello, certificat racine de pile de Azure hello est déjà installé dans l’ordinateur virtuel de hello afin de récupérer directement.</span><span class="sxs-lookup"><span data-stu-id="4f445-106">If you are using CLI from a virtual machine that is running within hello Azure Stack Development Kit environment, hello Azure Stack root certificate is already installed within hello virtual machine so you can directly retrieve.</span></span> <span data-ttu-id="4f445-107">Alors que si vous utilisez CLI à partir d’une station de travail à l’extérieur du kit de développement hello, vous devez exporter le certificat de hello Azure pile autorité de certification racine du kit de développement hello et ajoutez-le toohello Python magasin de certificats de votre station de travail de développement (externe Linux ou Mac plateforme ).</span><span class="sxs-lookup"><span data-stu-id="4f445-107">Whereas if you are use CLI from a workstation outside hello development kit, you must export hello Azure Stack CA root certificate from hello development kit and add it toohello Python certificate store of your development workstation(external Linux or Mac platform).</span></span> 

<span data-ttu-id="4f445-108">Se connecter dans le kit de développement tooyour et exécutez hello suivant script tooexport hello Azure pile certificat au format PEM :</span><span class="sxs-lookup"><span data-stu-id="4f445-108">Sign in tooyour development kit and run hello following script tooexport hello Azure Stack root certificate in PEM format:</span></span>

```powershell
   $label = "AzureStackSelfSignedRootCert"
   Write-Host "Getting certificate from hello current user trusted store with subject CN=$label"
   $root = Get-ChildItem Cert:\CurrentUser\Root | Where-Object Subject -eq "CN=$label" | select -First 1
   if (-not $root)
   {
       Log-Error "Cerficate with subject CN=$label not found"
       return
   }

   Write-Host "Exporting certificate"
   Export-Certificate -Type CERT -FilePath root.cer -Cert $root

   Write-Host "Converting certificate tooPEM format"
   certutil -encode root.cer root.pem
```

## <a name="install-cli"></a><span data-ttu-id="4f445-109">Installer l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="4f445-109">Install CLI</span></span>

<span data-ttu-id="4f445-110">Ensuite, vous devez vous connecter une station de travail de développement tooyour et installer l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="4f445-110">Next you should sign in tooyour development workstation and install CLI.</span></span> <span data-ttu-id="4f445-111">Pile Azure nécessite une version 2.0 de hello du CLI d’Azure, vous pouvez installer à l’aide des étapes hello Bonjour [installer Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) l’article.</span><span class="sxs-lookup"><span data-stu-id="4f445-111">Azure Stack requires hello 2.0 version of Azure CLI, which you can install by using hello steps described in hello [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) article.</span></span> <span data-ttu-id="4f445-112">tooverify si l’installation de hello a réussi, ouvrez un terminal ou une fenêtre d’invite de commandes et leur exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4f445-112">tooverify if hello installation was successful, open a terminal or a command prompt window and run hello following command:</span></span>

```azurecli
az --version
```

<span data-ttu-id="4f445-113">Vous devez voir version hello de CLI d’Azure et d’autres bibliothèques dépendantes sont installés sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4f445-113">You should see hello version of Azure CLI and other dependent libraries that are installed on your computer.</span></span>

## <a name="trust-hello-azure-stack-ca-root-certificate"></a><span data-ttu-id="4f445-114">Certificat de hello Azure pile autorité de certification racine de confiance</span><span class="sxs-lookup"><span data-stu-id="4f445-114">Trust hello Azure Stack CA root certificate</span></span>

<span data-ttu-id="4f445-115">tootrust hello Azure pile certificat racine, vous devez l’ajouter de certificat de python toohello existant.</span><span class="sxs-lookup"><span data-stu-id="4f445-115">tootrust hello Azure Stack CA root certificate, you should append it toohello existing python certificate.</span></span> <span data-ttu-id="4f445-116">Si vous exécutez CLI à partir d’un ordinateur Linux est créé dans l’environnement de Azure pile hello, suivante d’exécution hello bash commande :</span><span class="sxs-lookup"><span data-stu-id="4f445-116">If you are running CLI from a Linux machine that is created within hello Azure Stack environment, run hello following bash command:</span></span>

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

<span data-ttu-id="4f445-117">Si vous exécutez à partir d’un ordinateur en dehors de l’environnement de Azure sac hello CLI, vous devez tout d’abord configurer [tooAzure de connectivité VPN pile](azure-stack-connect-azure-stack.md).</span><span class="sxs-lookup"><span data-stu-id="4f445-117">If you are running CLI from a machine outside hello Azure Sack environment, you must first set up [VPN connectivity tooAzure Stack](azure-stack-connect-azure-stack.md).</span></span> <span data-ttu-id="4f445-118">Maintenant, copiez hello PEM certificat que vous avez exporté précédemment sur votre station de travail de développement et exécutez hello suivant de commandes en fonction du système d’exploitation de votre station de travail développement :</span><span class="sxs-lookup"><span data-stu-id="4f445-118">Now copy hello PEM certificate that you exported earlier onto your development workstation and run hello following commands depending on your development workstation's OS,:</span></span>

### <a name="linux"></a><span data-ttu-id="4f445-119">Linux</span><span class="sxs-lookup"><span data-stu-id="4f445-119">Linux</span></span>

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="macos"></a><span data-ttu-id="4f445-120">macOS</span><span class="sxs-lookup"><span data-stu-id="4f445-120">macOS</span></span>

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="windows"></a><span data-ttu-id="4f445-121">Windows</span><span class="sxs-lookup"><span data-stu-id="4f445-121">Windows</span></span>

```powershell
$pemFile = "<Fully qualified path toohello PEM certificate Ex: C:\Users\user1\Downloads\root.pem>"

$root = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$root.Import($pemFile)

Write-Host "Extracting needed information from hello cert file"
$md5Hash=(Get-FileHash -Path $pemFile -Algorithm MD5).Hash.ToLower()
$sha1Hash=(Get-FileHash -Path $pemFile -Algorithm SHA1).Hash.ToLower()
$sha256Hash=(Get-FileHash -Path $pemFile -Algorithm SHA256).Hash.ToLower()

$issuerEntry = [string]::Format("# Issuer: {0}", $root.Issuer)
$subjectEntry = [string]::Format("# Subject: {0}", $root.Subject)
$labelEntry = [string]::Format("# Label: {0}", $root.Subject.Split('=')[-1])
$serialEntry = [string]::Format("# Serial: {0}", $root.GetSerialNumberString().ToLower())
$md5Entry = [string]::Format("# MD5 Fingerprint: {0}", $md5Hash)
$sha1Entry  = [string]::Format("# SHA1 Finterprint: {0}", $sha1Hash)
$sha256Entry = [string]::Format("# SHA256 Fingerprint: {0}", $sha256Hash)
$certText = (Get-Content -Path root.pem -Raw).ToString().Replace("`r`n","`n")

$rootCertEntry = "`n" + $issuerEntry + "`n" + $subjectEntry + "`n" + $labelEntry + "`n" + `
$serialEntry + "`n" + $md5Entry + "`n" + $sha1Entry + "`n" + $sha256Entry + "`n" + $certText

Write-Host "Adding hello certificate content tooPython Cert store"
Add-Content "${env:ProgramFiles(x86)}\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem" $rootCertEntry

Write-Host "Python Cert store was updated for allowing hello azure stack CA root certificate"
```

## <a name="set-up-hello-virtual-machine-aliases-endpoint"></a><span data-ttu-id="4f445-122">Définir des points de terminaison alias hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4f445-122">Set up hello virtual machine aliases endpoint</span></span>

<span data-ttu-id="4f445-123">Avant que les utilisateurs peuvent créer des machines virtuelles à l’aide de CLI, administrateur du cloud hello doit définir un point de terminaison accessible publiquement qui contiennent des alias d’image de machine virtuelle et inscrire ce point de terminaison avec le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="4f445-123">Before users can create virtual machines by using CLI, hello cloud administrator should set up a publicly accessible endpoint that contains virtual machine image aliases and register this endpoint with hello cloud.</span></span> <span data-ttu-id="4f445-124">Hello `endpoint-vm-image-alias-doc` paramètre Bonjour `az cloud register` commande est utilisée à cet effet.</span><span class="sxs-lookup"><span data-stu-id="4f445-124">hello `endpoint-vm-image-alias-doc` parameter in hello `az cloud register` command is used for this purpose.</span></span> <span data-ttu-id="4f445-125">Les administrateurs de cloud doivent télécharger marketplace d’Azure pile hello image toohello avant de leur point de terminaison tooimage alias l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="4f445-125">Cloud administrators must download hello image toohello Azure Stack marketplace before they add it tooimage aliases endpoint.</span></span>
   
<span data-ttu-id="4f445-126">Par exemple, Azure utilise l’URI suivant : https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json.</span><span class="sxs-lookup"><span data-stu-id="4f445-126">For example, Azure contains uses following URI: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json.</span></span> <span data-ttu-id="4f445-127">Hello cloud administrateur doit configurer un point de terminaison similaire pour la pile d’Azure avec des images hello qui sont disponibles dans le marketplace d’Azure pile hello.</span><span class="sxs-lookup"><span data-stu-id="4f445-127">hello cloud administrator should set up a similar endpoint for Azure Stack with hello images that are available in hello Azure Stack marketplace.</span></span>

## <a name="connect-tooazure-stack"></a><span data-ttu-id="4f445-128">Se connecter tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="4f445-128">Connect tooAzure Stack</span></span>

<span data-ttu-id="4f445-129">Utilisez hello suivant les étapes tooconnect tooAzure pile :</span><span class="sxs-lookup"><span data-stu-id="4f445-129">Use hello following steps tooconnect tooAzure Stack:</span></span>

1. <span data-ttu-id="4f445-130">Inscrire votre environnement Azure pile en exécutant la commande de Registre hello az cloud.</span><span class="sxs-lookup"><span data-stu-id="4f445-130">Register your Azure Stack environment by running hello az cloud register command.</span></span>
   
   <span data-ttu-id="4f445-131">a.</span><span class="sxs-lookup"><span data-stu-id="4f445-131">a.</span></span> <span data-ttu-id="4f445-132">tooregister hello **cloud administration** environnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f445-132">tooregister hello **cloud administrative** environment, use:</span></span>

   ```azurecli
   az cloud register \ 
     -n AzureStackAdmin \ 
     --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

   <span data-ttu-id="4f445-133">b.</span><span class="sxs-lookup"><span data-stu-id="4f445-133">b.</span></span> <span data-ttu-id="4f445-134">tooregister hello **utilisateur** environnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f445-134">tooregister hello **user** environment, use:</span></span>

   ```azurecli
   az cloud register \ 
     -n AzureStackUser \ 
     --endpoint-resource-manager "https://management.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

2. <span data-ttu-id="4f445-135">Ensemble hello environnement actif à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="4f445-135">Set hello active environment by using hello following commands:</span></span>

   <span data-ttu-id="4f445-136">a.</span><span class="sxs-lookup"><span data-stu-id="4f445-136">a.</span></span> <span data-ttu-id="4f445-137">Pourquoi **cloud administration** environnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f445-137">For hello **cloud administrative** environment, use:</span></span>

   ```azurecli
   az cloud set \
     -n AzureStackAdmin
   ```

   <span data-ttu-id="4f445-138">b.</span><span class="sxs-lookup"><span data-stu-id="4f445-138">b.</span></span> <span data-ttu-id="4f445-139">Pourquoi **utilisateur** environnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f445-139">For hello **user** environment, use:</span></span>

   ```azurecli
   az cloud set \
     -n AzureStackUser
   ```

3. <span data-ttu-id="4f445-140">Mettre à jour votre hello de toouse configuration environnement profil version API spécifique de pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f445-140">Update your environment configuration toouse hello Azure Stack specific API version profile.</span></span> <span data-ttu-id="4f445-141">configuration de hello tooupdate, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4f445-141">tooupdate hello configuration, run hello following command:</span></span>

   ```azurecli
   az cloud update \
     --profile 2017-03-09-profile
   ```

4. <span data-ttu-id="4f445-142">Se connecter dans l’environnement de Azure pile tooyour à l’aide de hello **ouverture de session az** commande.</span><span class="sxs-lookup"><span data-stu-id="4f445-142">Sign in tooyour Azure Stack environment by using hello **az login** command.</span></span> <span data-ttu-id="4f445-143">Vous pouvez vous connecter dans l’environnement de Azure pile toohello en tant qu’un utilisateur ou un [principal du service](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects).</span><span class="sxs-lookup"><span data-stu-id="4f445-143">You can sign in toohello Azure Stack environment either as a user or as a [service principal](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects).</span></span> 

   * <span data-ttu-id="4f445-144">Connectez-vous en tant qu’un **utilisateur**: vous pouvez spécifier le nom d’utilisateur hello et un mot de passe directement dans la commande de connexion az hello ou authentifier à l’aide d’un navigateur.</span><span class="sxs-lookup"><span data-stu-id="4f445-144">Sign in as a **user**: You can either specify hello username and password directly within hello az login command or authenticate using a browser.</span></span> <span data-ttu-id="4f445-145">Vous devriez hello toodo ce dernier cas, si votre compte dispose de l’authentification multifacteur activée.</span><span class="sxs-lookup"><span data-stu-id="4f445-145">You would have toodo hello latter, if your account has multi-factor authentication enabled.</span></span>

   ```azurecli
   az login \
     -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
   ```

   > [!NOTE]
   > <span data-ttu-id="4f445-146">Si votre compte d’utilisateur a l’authentification multifacteur activée, vous pouvez utiliser la commande de connexion hello az sans fournir le paramètre -u de hello.</span><span class="sxs-lookup"><span data-stu-id="4f445-146">If your user account has Multi factor authentication enabled, you can use hello az login command without providing hello -u parameter.</span></span> <span data-ttu-id="4f445-147">Commande hello en cours d’exécution, vous donne une URL et un code que vous devez utiliser tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="4f445-147">Running hello command gives you a URL and a code that you must use tooauthenticate.</span></span>
   
   * <span data-ttu-id="4f445-148">Connectez-vous en tant qu’un **principal du service**: avant de vous connecter, [créer un principal de service via hello portail Azure](azure-stack-create-service-principals.md) ou l’interface CLI et lui attribuer un rôle.</span><span class="sxs-lookup"><span data-stu-id="4f445-148">Sign in as a **service principal**: Before you sign in, [Create a service principal through hello Azure portal](azure-stack-create-service-principals.md) or CLI and assign it a role.</span></span> <span data-ttu-id="4f445-149">Maintenant, connectez-vous à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4f445-149">Now, log in by using hello following command:</span></span>

   ```azurecli
   az login \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
     --service-principal \
     -u <Application Id of hello Service Principal> \
     -p <Key generated for hello Service Principal>
   ```

## <a name="test-hello-connectivity"></a><span data-ttu-id="4f445-150">Tester la connectivité hello</span><span class="sxs-lookup"><span data-stu-id="4f445-150">Test hello connectivity</span></span>

<span data-ttu-id="4f445-151">Maintenant que nous avons tout ce que le programme d’installation, nous allons utiliser les ressources de toocreate CLI au sein de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f445-151">Now that we've got everything setup, let's use CLI toocreate resources within Azure Stack.</span></span> <span data-ttu-id="4f445-152">Par exemple, vous pouvez créer un groupe de ressources pour une application et ajouter une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4f445-152">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="4f445-153">Hello utilisation suivant commande toocreate un groupe de ressources nommé « MyResourceGroup » :</span><span class="sxs-lookup"><span data-stu-id="4f445-153">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```azurecli
az group create \
  -n MyResourceGroup -l local
```

<span data-ttu-id="4f445-154">Si le groupe de ressources hello est créé avec succès, commande précédente hello génère hello propriétés de ressource de hello nouvellement créé suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f445-154">If hello resource group is created successfully, hello previous command outputs hello following properties of hello newly created resource:</span></span>

![Sortie de la création du groupe de ressources](media/azure-stack-connect-cli/image1.png)

<span data-ttu-id="4f445-156">Il existe certains problèmes connus lors de l’utilisation de CLI 2.0 dans Azure pile, toolearn sur ces problèmes, consultez hello [problèmes connus dans Azure pile CLI](azure-stack-troubleshooting.md#cli) rubrique.</span><span class="sxs-lookup"><span data-stu-id="4f445-156">There are some known issues when using CLI 2.0 in Azure Stack, toolearn about these issues, see hello [Known issues in Azure Stack CLI](azure-stack-troubleshooting.md#cli) topic.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4f445-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4f445-157">Next steps</span></span>

[<span data-ttu-id="4f445-158">Déployer des modèles avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4f445-158">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="4f445-159">Se connecter avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f445-159">Connect with PowerShell</span></span>](azure-stack-connect-powershell.md)

[<span data-ttu-id="4f445-160">Gérer les autorisations utilisateur</span><span class="sxs-lookup"><span data-stu-id="4f445-160">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

