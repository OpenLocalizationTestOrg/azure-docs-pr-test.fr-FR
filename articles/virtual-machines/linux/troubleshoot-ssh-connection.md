---
title: "la connexion SSH aaaTroubleshoot émet tooan machine virtuelle Azure | Documents Microsoft"
description: "Comment tootroubleshoot problèmes tels que « Échoué de la connexion SSH » ou « A refusé la connexion SSH » pour une machine virtuelle Azure exécutant Linux."
keywords: "connexion ssh refusée, erreur ssh, ssh azure, échec de connexion SSH"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="842aa-104">Résoudre les problèmes de tooan des connexions SSH Azure Linux VM qui échoue, les erreurs, ou est refusée</span><span class="sxs-lookup"><span data-stu-id="842aa-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="842aa-105">Il existe différentes raisons que vous rencontrez des erreurs de SSH (Secure Shell), les échecs de connexion SSH ou SSH est refusée lorsque vous essayez de tooconnect tooa Linux virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="842aa-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="842aa-106">Cet article vous permet de rechercher et problèmes de hello correct.</span><span class="sxs-lookup"><span data-stu-id="842aa-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="842aa-107">Vous pouvez utiliser hello portail Azure, Azure CLI ou Extension d’accès aux ordinateurs virtuels pour Linux tootroubleshoot et résoudre les problèmes de connexion.</span><span class="sxs-lookup"><span data-stu-id="842aa-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="842aa-108">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello forums MSDN Azure et le débordement de pile](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="842aa-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="842aa-109">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="842aa-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="842aa-110">Accédez toohello [site de support technique Azure](http://azure.microsoft.com/support/options/) et sélectionnez **obtenir un support technique**.</span><span class="sxs-lookup"><span data-stu-id="842aa-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="842aa-111">Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="842aa-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="842aa-112">Étapes de dépannage rapide</span><span class="sxs-lookup"><span data-stu-id="842aa-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="842aa-113">Après chaque étape de résolution des problèmes, essayez de vous reconnecter toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="842aa-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="842aa-114">Réinitialiser la configuration SSH de hello.</span><span class="sxs-lookup"><span data-stu-id="842aa-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="842aa-115">Réinitialiser les informations d’identification de hello pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="842aa-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="842aa-116">Vérifiez que hello [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) règles autorisent le trafic SSH.</span><span class="sxs-lookup"><span data-stu-id="842aa-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="842aa-117">Assurez-vous qu’une règle de groupe de sécurité réseau existe toopermit SSH trafic (par défaut, le port TCP 22).</span><span class="sxs-lookup"><span data-stu-id="842aa-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="842aa-118">Vous ne pouvez pas utiliser la redirection / mappage de port sans utiliser un équilibreur de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="842aa-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="842aa-119">Vérifiez hello [contrôle d’intégrité de machine virtuelle](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="842aa-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="842aa-120">Vérifiez que hello VM rapports comme étant sain.</span><span class="sxs-lookup"><span data-stu-id="842aa-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="842aa-121">Si vous avez activés les diagnostics de démarrage, vérifiez hello VM ne signale pas d’erreurs de démarrage dans les journaux hello.</span><span class="sxs-lookup"><span data-stu-id="842aa-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="842aa-122">Redémarrez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="842aa-122">Restart hello VM.</span></span>
6. <span data-ttu-id="842aa-123">Redéployez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="842aa-123">Redeploy hello VM.</span></span>

<span data-ttu-id="842aa-124">Si vous cherchez des procédures de dépannage plus détaillées et des explications, poursuivez la lecture.</span><span class="sxs-lookup"><span data-stu-id="842aa-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="842aa-125">Problèmes de connexion SSH méthodes disponibles tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="842aa-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="842aa-126">Vous pouvez réinitialiser les informations d’identification ou la configuration SSH à l’aide d’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="842aa-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="842aa-127">[Portail Azure](#use-the-azure-portal) - great si vous avez besoin de tooquickly réinitialiser la configuration SSH de hello ou clé SSH et que vous n’avez hello Windows Azure tools installés.</span><span class="sxs-lookup"><span data-stu-id="842aa-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="842aa-128">[Azure CLI 2.0](#use-the-azure-cli-20) : Si vous êtes déjà sur la ligne de commande hello rapidement réinitialisation hello SSH configuration ou les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="842aa-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="842aa-129">Vous pouvez également utiliser hello [Azure CLI 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="842aa-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="842aa-130">[L’extension VMAccessForLinux Azure](#use-the-vmaccess-extension) - création et la réutilisation de json définition fichiers tooreset hello SSH configuration ou références utilisateur.</span><span class="sxs-lookup"><span data-stu-id="842aa-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="842aa-131">Après chaque étape de dépannage, réessayez de vous connecter tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="842aa-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="842aa-132">Si vous ne pouvez toujours pas vous connecter, essayez l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="842aa-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="842aa-133">Utilisez hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="842aa-133">Use hello Azure portal</span></span>
<span data-ttu-id="842aa-134">Hello portail Azure fournit un Bonjour de tooreset rapidement des informations d’identification utilisateur ou de la configuration SSH sans installer les outils sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="842aa-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="842aa-135">Bonjour portail Azure, sélectionnez votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="842aa-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="842aa-136">Défiler toohello **prise en charge + dépannage** section et sélectionnez **réinitialisation de mot de passe** comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="842aa-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![Réinitialiser la configuration SSH ou les informations d’identification dans hello portail Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="842aa-138">Réinitialiser la configuration SSH de hello</span><span class="sxs-lookup"><span data-stu-id="842aa-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="842aa-139">Dans un premier temps, sélectionnez `Reset configuration only` de hello **Mode** menu déroulant comme dans hello précédant la capture d’écran, puis cliquez sur hello **réinitialiser** bouton.</span><span class="sxs-lookup"><span data-stu-id="842aa-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="842aa-140">Une fois cette opération terminée, réessayez tooaccess votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="842aa-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="842aa-141">Réinitialisation des informations d’identification SSH d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="842aa-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="842aa-142">informations d’identification de hello tooreset d’un utilisateur existant, sélectionnez `Reset SSH public key` ou `Reset password` de hello **Mode** menu déroulant comme hello précédant la capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="842aa-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="842aa-143">Spécifiez le nom d’utilisateur hello et une clé SSH ou un nouveau mot de passe, puis cliquez sur hello **réinitialiser** bouton.</span><span class="sxs-lookup"><span data-stu-id="842aa-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="842aa-144">Vous pouvez également créer un utilisateur avec des privilèges sudo sur hello machine virtuelle à partir de ce menu.</span><span class="sxs-lookup"><span data-stu-id="842aa-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="842aa-145">Entrez un nouveau nom d’utilisateur et le mot de passe associé ou la clé SSH, puis cliquez sur hello **réinitialiser** bouton.</span><span class="sxs-lookup"><span data-stu-id="842aa-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="842aa-146">Utilisez hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="842aa-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="842aa-147">Si vous n’avez pas encore, installez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="842aa-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="842aa-148">Si vous avez créé et téléchargé une image de disque Linux personnalisée, vérifiez que hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 ou version ultérieure est installé.</span><span class="sxs-lookup"><span data-stu-id="842aa-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="842aa-149">Pour les machines virtuelles créées à l’aide d’images de la galerie, cette extension de l’accès est déjà installée et configurée.</span><span class="sxs-lookup"><span data-stu-id="842aa-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="842aa-150">Réinitialisation de la configuration SSH</span><span class="sxs-lookup"><span data-stu-id="842aa-150">Reset SSH configuration</span></span>
<span data-ttu-id="842aa-151">Vous pouvez initialement try réinitialisation hello SSH toodefault les valeurs de configuration et en cours de redémarrage serveur SSH hello hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="842aa-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="842aa-152">Notez que cela ne modifie pas le nom de compte d’utilisateur hello, mot de passe ou des clés SSH.</span><span class="sxs-lookup"><span data-stu-id="842aa-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="842aa-153">Hello exemple suivant utilise [réinitialisation de l’utilisateur az vm-ssh](/cli/azure/vm/user#reset-ssh) configuration SSH tooreset hello hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="842aa-154">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="842aa-155">Réinitialisation des informations d’identification SSH d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="842aa-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="842aa-156">Hello exemple suivant utilise [mise à jour des utilisateur de machine virtuelle az](/cli/azure/vm/user#update) tooreset hello informations d’identification pour `myUsername` valeur toohello spécifiée dans `myPassword`, sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="842aa-157">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="842aa-158">Si vous utilisez l’authentification par clé SSH, vous pouvez réinitialiser la clé SSH hello pour un utilisateur donné.</span><span class="sxs-lookup"><span data-stu-id="842aa-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="842aa-159">Hello exemple suivant utilise **az vm accéder set-linux-user** tooupdate hello SSH clé stockée dans `~/.ssh/id_rsa.pub` d’utilisateur hello nommé `myUsername`, sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="842aa-160">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="842aa-161">Utilisez l’extension VMAccess hello</span><span class="sxs-lookup"><span data-stu-id="842aa-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="842aa-162">Hello Extension d’accès aux ordinateurs virtuels pour Linux lit dans un fichier json qui définit toocarry actions out. Ces actions incluent la réinitialisation SSHD, la réinitialisation d’une clé SSH ou l’ajout d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="842aa-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="842aa-163">Vous utilisez toujours toocall hello extension VMAccess de hello CLI d’Azure, mais vous pouvez réutiliser des fichiers au format json hello dans plusieurs machines virtuelles, si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="842aa-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="842aa-164">Cette approche vous permet de toocreate un référentiel de fichiers json qui peut ensuite être appelée pour compte tenu des scénarios.</span><span class="sxs-lookup"><span data-stu-id="842aa-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="842aa-165">Réinitialiser SSHD</span><span class="sxs-lookup"><span data-stu-id="842aa-165">Reset SSHD</span></span>
<span data-ttu-id="842aa-166">Créez un fichier nommé `settings.json` avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="842aa-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="842aa-167">À l’aide de hello CLI d’Azure, puis appelez hello `VMAccessForLinux` extension tooreset votre connexion SSHD en spécifiant votre fichier json.</span><span class="sxs-lookup"><span data-stu-id="842aa-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="842aa-168">Hello exemple suivant utilise [az vm extension ensemble](/cli/azure/vm/extension#set) tooreset SSHD sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="842aa-169">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="842aa-170">Réinitialisation des informations d’identification SSH d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="842aa-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="842aa-171">Se SSHD toofunction correctement, vous pouvez réinitialiser les informations d’identification de hello pour un utilisateur lui-même.</span><span class="sxs-lookup"><span data-stu-id="842aa-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="842aa-172">mot de passe tooreset hello pour un utilisateur, créez un fichier nommé `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="842aa-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="842aa-173">Hello exemple suivant réinitialise les informations d’identification de hello pour `myUsername` valeur toohello spécifiée dans `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="842aa-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="842aa-174">Entrez hello suivant des lignes dans votre `settings.json` fichier, à l’aide de vos propres valeurs :</span><span class="sxs-lookup"><span data-stu-id="842aa-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="842aa-175">Ou tooreset hello clé SSH pour un utilisateur, commencez par créer un fichier nommé `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="842aa-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="842aa-176">Hello exemple suivant réinitialise les informations d’identification de hello pour `myUsername` valeur toohello spécifiée dans `myPassword`, sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="842aa-177">Entrez hello suivant des lignes dans votre `settings.json` fichier, à l’aide de vos propres valeurs :</span><span class="sxs-lookup"><span data-stu-id="842aa-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="842aa-178">Après avoir créé votre fichier json, utilisez hello de toocall CLI d’Azure hello `VMAccessForLinux` tooreset d’extension d’informations d’identification de votre utilisateur SSH en spécifiant votre fichier json.</span><span class="sxs-lookup"><span data-stu-id="842aa-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="842aa-179">Hello exemple suivant réinitialise les informations d’identification sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="842aa-180">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="842aa-181">Utilisez hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="842aa-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="842aa-182">Si vous n’avez pas déjà fait, [installer hello Azure CLI 1.0 et se connecter tooyour abonnement Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="842aa-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="842aa-183">Assurez-vous d’utiliser le mode Resource Manager comme indiqué ci-après :</span><span class="sxs-lookup"><span data-stu-id="842aa-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="842aa-184">Si vous avez créé et téléchargé une image de disque Linux personnalisée, vérifiez que hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 ou version ultérieure est installé.</span><span class="sxs-lookup"><span data-stu-id="842aa-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="842aa-185">Pour les machines virtuelles créées à l’aide d’images de la galerie, cette extension de l’accès est déjà installée et configurée.</span><span class="sxs-lookup"><span data-stu-id="842aa-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="842aa-186">Réinitialisation de la configuration SSH</span><span class="sxs-lookup"><span data-stu-id="842aa-186">Reset SSH configuration</span></span>
<span data-ttu-id="842aa-187">configuration de SSHD Hello lui-même peut être mal configurée ou service de hello a rencontré une erreur.</span><span class="sxs-lookup"><span data-stu-id="842aa-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="842aa-188">Vous pouvez réinitialiser toomake SSHD que la configuration SSH hello lui-même est valide.</span><span class="sxs-lookup"><span data-stu-id="842aa-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="842aa-189">La réinitialisation SSHD doit être hello première étape de dépannage que vous prenez.</span><span class="sxs-lookup"><span data-stu-id="842aa-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="842aa-190">Hello exemple suivant réinitialise SSHD sur un ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="842aa-191">Utilisez vos propres noms de machine virtuelle et de groupe de ressources comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="842aa-192">Réinitialisation des informations d’identification SSH d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="842aa-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="842aa-193">Se SSHD toofunction correctement, vous pouvez réinitialiser le mot de passe hello pour un utilisateur lui-même.</span><span class="sxs-lookup"><span data-stu-id="842aa-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="842aa-194">Hello exemple suivant réinitialise les informations d’identification de hello pour `myUsername` valeur toohello spécifiée dans `myPassword`, sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="842aa-195">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="842aa-196">Si vous utilisez l’authentification par clé SSH, vous pouvez réinitialiser la clé SSH hello pour un utilisateur donné.</span><span class="sxs-lookup"><span data-stu-id="842aa-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="842aa-197">Hello après les mises à jour de l’exemple hello stockée dans la clé SSH `~/.ssh/id_rsa.pub` d’utilisateur hello nommé `myUsername`, sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="842aa-198">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="842aa-199">Redémarrer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="842aa-199">Restart a VM</span></span>
<span data-ttu-id="842aa-200">Si vous avez réinitialisé les informations d’identification utilisateur et de configuration de SSH hello ou a rencontré une erreur en faisant cela, vous pouvez essayer de redémarrer tooaddress de machine virtuelle hello sous-jacente des problèmes de calcul.</span><span class="sxs-lookup"><span data-stu-id="842aa-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="842aa-201">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="842aa-201">Azure portal</span></span>
<span data-ttu-id="842aa-202">une machine virtuelle à l’aide de toorestart hello sélectionnez portail, Azure hello de votre machine virtuelle et cliquez sur **redémarrer** bouton comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="842aa-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![Redémarrer une machine virtuelle Bonjour portail Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="842aa-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="842aa-204">Azure CLI 1.0</span></span>
<span data-ttu-id="842aa-205">Hello après le redémarrage de l’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="842aa-206">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="842aa-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="842aa-207">Azure CLI 2.0</span></span>
<span data-ttu-id="842aa-208">Hello exemple suivant utilise [redémarrage de machine virtuelle az](/cli/azure/vm#restart) toorestart hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="842aa-209">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="842aa-210">Redéploiement d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="842aa-210">Redeploy a VM</span></span>
<span data-ttu-id="842aa-211">Vous pouvez redéployer un nœud de tooanother de machine virtuelle dans Azure, ce qui peut résoudre les problèmes de mise en réseau sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="842aa-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="842aa-212">Pour plus d’informations sur la redéployer une machine virtuelle, consultez [redéployer la machine virtuelle toonew nœud Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="842aa-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="842aa-213">Une fois cette opération terminée, disque éphémère, les données seront perdues et les adresses IP dynamiques associés à la machine virtuelle de hello seront mise à jour.</span><span class="sxs-lookup"><span data-stu-id="842aa-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="842aa-214">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="842aa-214">Azure portal</span></span>
<span data-ttu-id="842aa-215">une machine virtuelle à l’aide de tooredeploy hello Azure sélectionnez portail, votre machine virtuelle et faites défiler toohello **prise en charge + dépannage** section.</span><span class="sxs-lookup"><span data-stu-id="842aa-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="842aa-216">Cliquez sur hello **redéployer** bouton comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="842aa-216">Click hello **Redeploy** button as in hello following example:</span></span>

![Redéployer une machine virtuelle dans hello portail Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="842aa-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="842aa-218">Azure CLI 1.0</span></span>
<span data-ttu-id="842aa-219">Hello suivant redéploiements ultérieurs d’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="842aa-220">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="842aa-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="842aa-221">Azure CLI 2.0</span></span>
<span data-ttu-id="842aa-222">Hello après utilisation de l’exemple [redéploiement de machine virtuelle az](/cli/azure/vm#redeploy) tooredeploy hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="842aa-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="842aa-223">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="842aa-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="842aa-224">Machines virtuelles créées à l’aide du modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="842aa-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="842aa-225">Essayez ces étapes tooresolve hello courants SSH échecs de connexion pour les ordinateurs virtuels qui ont été créés à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="842aa-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="842aa-226">Après chaque étape, essayez de vous reconnecter toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="842aa-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="842aa-227">Réinitialisez l’accès à distance à partir de hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="842aa-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="842aa-228">Sur hello portail Azure, votre machine virtuelle puis cliquez sur hello **réinitialiser à distance...**  bouton.</span><span class="sxs-lookup"><span data-stu-id="842aa-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="842aa-229">Redémarrez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="842aa-229">Restart hello VM.</span></span> <span data-ttu-id="842aa-230">Sur hello [portail Azure](https://portal.azure.com), sélectionnez votre machine virtuelle et cliquez sur hello **redémarrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="842aa-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="842aa-231">Redéployez le nœud Azure nouvelle machine virtuelle tooa hello.</span><span class="sxs-lookup"><span data-stu-id="842aa-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="842aa-232">Pour plus d’informations sur la façon tooredeploy une machine virtuelle, consultez [redéployer la machine virtuelle toonew nœud Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="842aa-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="842aa-233">Une fois cette opération terminée, disque éphémère, les données seront perdues et les adresses IP dynamiques associés à la machine virtuelle de hello seront mise à jour.</span><span class="sxs-lookup"><span data-stu-id="842aa-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="842aa-234">Suivez les instructions de hello dans [comment tooreset un mot de passe ou de SSH pour les ordinateurs virtuels basés sur Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) à :</span><span class="sxs-lookup"><span data-stu-id="842aa-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="842aa-235">Réinitialiser le mot de passe hello ou clé SSH.</span><span class="sxs-lookup"><span data-stu-id="842aa-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="842aa-236">créer un nouveau compte utilisateur *sudo* ;</span><span class="sxs-lookup"><span data-stu-id="842aa-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="842aa-237">Réinitialiser la configuration SSH de hello.</span><span class="sxs-lookup"><span data-stu-id="842aa-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="842aa-238">Vérifiez l’intégrité des ressources de machine virtuelle hello pour les problèmes de plateforme.</span><span class="sxs-lookup"><span data-stu-id="842aa-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="842aa-239">Sélectionnez votre machine virtuelle et faites défiler jusqu’à **Paramètres** > **Vérifier l’intégrité**.</span><span class="sxs-lookup"><span data-stu-id="842aa-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="842aa-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="842aa-240">Additional resources</span></span>
* <span data-ttu-id="842aa-241">Si vous ne parvenez toujours pas tooSSH tooyour machine virtuelle après suivant hello après les étapes, consultez [plus d’étapes de dépannage](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview supplémentaire étapes tooresolve votre problème.</span><span class="sxs-lookup"><span data-stu-id="842aa-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="842aa-242">Pour plus d’informations sur la résolution des problèmes d’accès aux applications, consultez [application tooan de résoudre les accès en cours d’exécution sur une machine virtuelle Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="842aa-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="842aa-243">Pour plus d’informations sur le dépannage des ordinateurs virtuels qui ont été créés à l’aide du modèle de déploiement classique de hello, consultez [comment tooreset un mot de passe ou de SSH pour les ordinateurs virtuels basés sur Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="842aa-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

