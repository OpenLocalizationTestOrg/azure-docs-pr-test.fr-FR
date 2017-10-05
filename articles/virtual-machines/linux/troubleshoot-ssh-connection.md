---
title: "Résolution de problèmes de connexion SSH à une machine virtuelle Azure | Microsoft Docs"
description: "Dépannage d’erreurs SSH telles que l’échec de connexion SSH ou le refus de connexion SSH pour une machine virtuelle Azure exécutant Linux."
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
ms.openlocfilehash: 3a282c8b2c2ba2749de6a2d3688bd57d75703b22
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-ssh-connections-to-an-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="60129-104">Dépannage d’une connexion SSH à une machine virtuelle Linux Azure défaillante, qui génère une erreur ou qui est refusée</span><span class="sxs-lookup"><span data-stu-id="60129-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="60129-105">Il existe différentes raisons pour lesquelles des erreurs SSH (Secure Shell) se produisent, la connexion SSH échoue ou cette connexion est refusée lorsque vous tentez de vous connecter à une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="60129-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span></span> <span data-ttu-id="60129-106">Cet article vous aide à identifier et à corriger ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="60129-106">This article helps you find and correct the problems.</span></span> <span data-ttu-id="60129-107">Vous pouvez utiliser le portail Azure, l’interface de ligne de commande Azure ou l’extension d’accès aux machines virtuelles pour Linux pour dépanner et résoudre des problèmes de connexion.</span><span class="sxs-lookup"><span data-stu-id="60129-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="60129-108">Si vous avez besoin d’une aide supplémentaire à quelque étape que ce soit dans cet article, vous pouvez contacter les experts Azure sur les [forums MSDN Azure et Stack Overflow](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="60129-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="60129-109">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="60129-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="60129-110">Accédez au [site du support Azure](http://azure.microsoft.com/support/options/) , puis cliquez sur **Obtenir un support**.</span><span class="sxs-lookup"><span data-stu-id="60129-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="60129-111">Pour plus d’informations sur l’utilisation du support Azure, lisez le [FAQ du support Microsoft Azure](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="60129-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="60129-112">Étapes de dépannage rapide</span><span class="sxs-lookup"><span data-stu-id="60129-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="60129-113">Après chaque étape de résolution des problèmes, essayez de vous reconnecter à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60129-113">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="60129-114">réinitialiser la configuration SSH.</span><span class="sxs-lookup"><span data-stu-id="60129-114">Reset the SSH configuration.</span></span>
2. <span data-ttu-id="60129-115">Réinitialisation des informations d'identification pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="60129-115">Reset the credentials for the user.</span></span>
3. <span data-ttu-id="60129-116">Vérifiez les règles du [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) autorise le trafic SSH.</span><span class="sxs-lookup"><span data-stu-id="60129-116">Verify the [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="60129-117">Vérifiez l’existence d’une règle de groupe de sécurité réseau pour autoriser le trafic SSH (par défaut, le port TCP 22).</span><span class="sxs-lookup"><span data-stu-id="60129-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="60129-118">Vous ne pouvez pas utiliser la redirection / mappage de port sans utiliser un équilibreur de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="60129-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="60129-119">Vérifiez [l’intégrité des ressources de la machine virtuelle](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="60129-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="60129-120">Assurez-vous que la machine virtuelle est intègre.</span><span class="sxs-lookup"><span data-stu-id="60129-120">Ensure that the VM reports as being healthy.</span></span>
   * <span data-ttu-id="60129-121">Si vous avez des diagnostics de démarrage activés, vérifiez que la machine virtuelle ne signale pas les erreurs de démarrage dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="60129-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span></span>
5. <span data-ttu-id="60129-122">Redémarrez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60129-122">Restart the VM.</span></span>
6. <span data-ttu-id="60129-123">Redéployez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60129-123">Redeploy the VM.</span></span>

<span data-ttu-id="60129-124">Si vous cherchez des procédures de dépannage plus détaillées et des explications, poursuivez la lecture.</span><span class="sxs-lookup"><span data-stu-id="60129-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-to-troubleshoot-ssh-connection-issues"></a><span data-ttu-id="60129-125">Méthodes disponibles pour résoudre les problèmes de connexion SSH</span><span class="sxs-lookup"><span data-stu-id="60129-125">Available methods to troubleshoot SSH connection issues</span></span>
<span data-ttu-id="60129-126">Vous pouvez réinitialiser les informations d’identification ou la configuration SSH avec l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="60129-126">You can reset credentials or SSH configuration using one of the following methods:</span></span>

* <span data-ttu-id="60129-127">[Portail Azure](#use-the-azure-portal) : utile si vous devez rapidement réinitialiser la configuration SSH ou la clé SSH et que vous n’avez pas installé les outils Azure.</span><span class="sxs-lookup"><span data-stu-id="60129-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="60129-128">[Azure CLI 2.0](#use-the-azure-cli-20) : si vous êtes déjà en ligne de commande, réinitialisez rapidement la configuration SSH ou les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="60129-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span></span> <span data-ttu-id="60129-129">Vous pouvez aussi utiliser [Azure CLI 1.0](#use-the-azure-cli-10).</span><span class="sxs-lookup"><span data-stu-id="60129-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="60129-130">[L’extension VMAccessForLinux Azure](#use-the-vmaccess-extension) : création et réutilisation de fichiers de définition json pour réinitialiser la configuration SSH ou les informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="60129-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span></span>

<span data-ttu-id="60129-131">Après chaque étape de résolution des problèmes, essayez de nouveau de vous connecter à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60129-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="60129-132">Si vous ne parvenez toujours pas à vous connecter, essayez l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="60129-132">If you still cannot connect, try the next step.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="60129-133">Utilisation du portail Azure</span><span class="sxs-lookup"><span data-stu-id="60129-133">Use the Azure portal</span></span>
<span data-ttu-id="60129-134">Le portail Azure offre un moyen rapide de réinitialiser la configuration SSH ou les informations d’identification utilisateur sans installer d’outils sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="60129-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="60129-135">Sélectionnez votre machine virtuelle dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="60129-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="60129-136">Faites défiler jusqu'à la section **Support + dépannage** et sélectionnez **Réinitialiser le de mot de passe** comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="60129-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span></span>

![Réinitialisation de la configuration SSH ou des informations d’identification dans le portail Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-the-ssh-configuration"></a><span data-ttu-id="60129-138">Réinitialisation de la configuration SSH</span><span class="sxs-lookup"><span data-stu-id="60129-138">Reset the SSH configuration</span></span>
<span data-ttu-id="60129-139">Dans un premier temps, sélectionnez `Reset configuration only` dans le menu déroulant **Mode** comme illustré dans la capture d’écran précédente, puis cliquez sur le bouton **Réinitialiser**.</span><span class="sxs-lookup"><span data-stu-id="60129-139">As a first step, select `Reset configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span></span> <span data-ttu-id="60129-140">Une fois cette opération terminée, essayez de nouveau d’accéder à votre machine Virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60129-140">Once this action has completed, try to access your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="60129-141">Réinitialisation des informations d’identification SSH d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="60129-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="60129-142">Pour réinitialiser les informations d’identification d’un utilisateur existant, sélectionnez `Reset SSH public key` ou `Reset password` dans le menu de **Mode** comme dans la capture d’écran précédente.</span><span class="sxs-lookup"><span data-stu-id="60129-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span></span> <span data-ttu-id="60129-143">Spécifiez le nom d’utilisateur et une clé SSH ou un nouveau mot de passe, puis cliquez sur le bouton **Réinitialiser**.</span><span class="sxs-lookup"><span data-stu-id="60129-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span></span>

<span data-ttu-id="60129-144">Vous pouvez également créer un utilisateur avec des privilèges sudo sur la machine virtuelle à partir de ce menu.</span><span class="sxs-lookup"><span data-stu-id="60129-144">You can also create a user with sudo privileges on the VM from this menu.</span></span> <span data-ttu-id="60129-145">Entrez un nouveau nom d’utilisateur et un mot de passe ou une clé SSH qui correspond, puis cliquez sur le bouton **Réinitialiser**.</span><span class="sxs-lookup"><span data-stu-id="60129-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span></span>

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="60129-146">Utiliser Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="60129-146">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="60129-147">Si ce n’est déjà fait, installez la dernière version [d’Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à votre compte Azure avec [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="60129-147">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="60129-148">Si vous avez créé et téléchargé une image de disque Linux personnalisée, assurez-vous que le [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 ou ultérieure est installé.</span><span class="sxs-lookup"><span data-stu-id="60129-148">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="60129-149">Pour les machines virtuelles créées à l’aide d’images de la galerie, cette extension de l’accès est déjà installée et configurée.</span><span class="sxs-lookup"><span data-stu-id="60129-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="60129-150">Réinitialisation de la configuration SSH</span><span class="sxs-lookup"><span data-stu-id="60129-150">Reset SSH configuration</span></span>
<span data-ttu-id="60129-151">Vous pouvez initialement essayer de réinitialiser la configuration SSH aux valeurs par défaut et de redémarrer le serveur SSH sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60129-151">You can initially try resetting the SSH configuration to default values and rebooting the SSH server on the VM.</span></span> <span data-ttu-id="60129-152">Notez que cela ne change pas le nom du compte d’utilisateur, le mot de passe, ou les clés SSH.</span><span class="sxs-lookup"><span data-stu-id="60129-152">Note that this does not change the user account name, password, or SSH keys.</span></span>
<span data-ttu-id="60129-153">L’exemple suivant utilise [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) pour réinitialiser la configuration SSH sur la machine virtuelle nommée `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-153">The following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) to reset the SSH configuration on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="60129-154">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="60129-155">Réinitialisation des informations d’identification SSH d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="60129-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="60129-156">L’exemple suivant utilise [az vm user update](/cli/azure/vm/user#update) pour réinitialiser les informations d’identification pour `myUsername` à la valeur spécifiée dans `myPassword`, sur la machine virtuelle `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-156">The following example uses [az vm user update](/cli/azure/vm/user#update) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="60129-157">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="60129-158">Si vous utilisez l’authentification par clé SSH, vous pouvez réinitialiser la clé SSH pour un utilisateur donné.</span><span class="sxs-lookup"><span data-stu-id="60129-158">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="60129-159">L’exemple suivant utilise **az vm access set-linux-user** pour mettre à jour la clé SSH stockée dans `~/.ssh/id_rsa.pub` pour l’utilisateur `myUsername`, sur la machine virtuelle `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-159">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="60129-160">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-the-vmaccess-extension"></a><span data-ttu-id="60129-161">Utilisation de l’extension VMAccess</span><span class="sxs-lookup"><span data-stu-id="60129-161">Use the VMAccess extension</span></span>
<span data-ttu-id="60129-162">L’extension d’accès de machine virtuelle pour Linux lit dans un fichier json qui définit les actions à effectuer. Ces actions incluent la réinitialisation SSHD, la réinitialisation d’une clé SSH ou l’ajout d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="60129-162">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="60129-163">Vous utilisez toujours l’interface de ligne de commande Azure pour appeler l’extension VMAccess, mais vous pouvez réutiliser les fichiers json sur plusieurs machines virtuelles si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="60129-163">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span></span> <span data-ttu-id="60129-164">Cette approche vous permet de créer un référentiel de fichiers json que vous pouvez ensuite appeler en fonction des scénarios.</span><span class="sxs-lookup"><span data-stu-id="60129-164">This approach allows you to create a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="60129-165">Réinitialiser SSHD</span><span class="sxs-lookup"><span data-stu-id="60129-165">Reset SSHD</span></span>
<span data-ttu-id="60129-166">Créez un fichier nommé `settings.json` avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="60129-166">Create a file named `settings.json` with the following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="60129-167">À l’aide de l’interface de ligne de commande Azure, appelez ensuite l’extension `VMAccessForLinux` pour réinitialiser votre connexion SSHD en spécifiant votre fichier json.</span><span class="sxs-lookup"><span data-stu-id="60129-167">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="60129-168">L’exemple suivant utilise [az vm extension set](/cli/azure/vm/extension#set) pour réinitialiser SSHD sur la machine virtuelle nommée `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-168">The following example uses [az vm extension set](/cli/azure/vm/extension#set) to reset SSHD on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="60129-169">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="60129-170">Réinitialisation des informations d’identification SSH d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="60129-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="60129-171">Si SSHD semble fonctionner correctement, vous pouvez réinitialiser les informations d’identification d’un utilisateur donné.</span><span class="sxs-lookup"><span data-stu-id="60129-171">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span></span> <span data-ttu-id="60129-172">Pour réinitialiser le mot de passe pour un utilisateur, créez un fichier nommé `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="60129-172">To reset the password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="60129-173">L’exemple suivant réinitialise les informations d’identification pour `myUsername` sur la valeur spécifiée dans `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="60129-173">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span></span> <span data-ttu-id="60129-174">Entrez les lignes suivantes dans votre fichier `settings.json` en utilisant vos propres valeurs :</span><span class="sxs-lookup"><span data-stu-id="60129-174">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="60129-175">Pour réinitialiser la clé SSH pour un utilisateur, créez tout d’abord un fichier nommé `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="60129-175">Or to reset the SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="60129-176">L’exemple suivant réinitialise les informations d’identification pour `myUsername` sur la valeur spécifiée dans `myPassword` sur la machine virtuelle nommée `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-176">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="60129-177">Entrez les lignes suivantes dans votre fichier `settings.json` en utilisant vos propres valeurs :</span><span class="sxs-lookup"><span data-stu-id="60129-177">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="60129-178">Après avoir créé votre fichier json, utilisez l’interface de ligne de commande Azure pour appeler l’extension `VMAccessForLinux` pour réinitialiser vos informations d’identification d’utilisateur SSH en spécifiant votre fichier json.</span><span class="sxs-lookup"><span data-stu-id="60129-178">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="60129-179">L’exemple suivant réinitialise les informations d’identification sur la machine virtuelle nommée `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-179">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="60129-180">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="60129-181">Utilisation de la CLI Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="60129-181">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="60129-182">Si ce n’est déjà fait, [installez la CLI Azure 1.0 et connectez-vous à votre abonnement Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="60129-182">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="60129-183">Assurez-vous d’utiliser le mode Resource Manager comme indiqué ci-après :</span><span class="sxs-lookup"><span data-stu-id="60129-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="60129-184">Si vous avez créé et téléchargé une image de disque Linux personnalisée, assurez-vous que le [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 ou ultérieure est installé.</span><span class="sxs-lookup"><span data-stu-id="60129-184">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="60129-185">Pour les machines virtuelles créées à l’aide d’images de la galerie, cette extension de l’accès est déjà installée et configurée.</span><span class="sxs-lookup"><span data-stu-id="60129-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="60129-186">Réinitialisation de la configuration SSH</span><span class="sxs-lookup"><span data-stu-id="60129-186">Reset SSH configuration</span></span>
<span data-ttu-id="60129-187">Il est possible que la configuration SSHD soit mal configurée ou que le service ait rencontré une erreur.</span><span class="sxs-lookup"><span data-stu-id="60129-187">The SSHD configuration itself may be misconfigured or the service encountered an error.</span></span> <span data-ttu-id="60129-188">Vous pouvez réinitialiser SSHD pour vous assurer que la configuration SSH elle-même est valide.</span><span class="sxs-lookup"><span data-stu-id="60129-188">You can reset SSHD to make sure the SSH configuration itself is valid.</span></span> <span data-ttu-id="60129-189">La réinitialisation du SSHD doit être la première étape de dépannage que vous effectuez.</span><span class="sxs-lookup"><span data-stu-id="60129-189">Resetting SSHD should be the first troubleshooting step you take.</span></span>

<span data-ttu-id="60129-190">L’exemple suivant redémarre le SSHD nommé `myVM` dans le groupe de ressources nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-190">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="60129-191">Utilisez vos propres noms de machine virtuelle et de groupe de ressources comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="60129-192">Réinitialisation des informations d’identification SSH d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="60129-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="60129-193">Si SSHD semble fonctionner correctement, vous pouvez réinitialiser le mot de passe d’un utilisateur donné.</span><span class="sxs-lookup"><span data-stu-id="60129-193">If SSHD appears to function correctly, you can reset the password for a giver user.</span></span> <span data-ttu-id="60129-194">L’exemple suivant réinitialise les informations d’identification pour `myUsername` sur la valeur spécifiée dans `myPassword` sur la machine virtuelle nommée `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-194">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="60129-195">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="60129-196">Si vous utilisez l’authentification par clé SSH, vous pouvez réinitialiser la clé SSH pour un utilisateur donné.</span><span class="sxs-lookup"><span data-stu-id="60129-196">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="60129-197">L’exemple suivant met à jour la clé SSH stockée dans `~/.ssh/id_rsa.pub` pour l’utilisateur nommé `myUsername` sur la machine virtuelle nommée `myVM` dans `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-197">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="60129-198">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="60129-199">Redémarrer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="60129-199">Restart a VM</span></span>
<span data-ttu-id="60129-200">Si vous avez réinitialisé la configuration SSH et les informations d’identification utilisateur, ou si une erreur a été générée lors de cette opération, vous pouvez essayer de redémarrer la machine virtuelle à l’adresse liée aux problèmes de calcul.</span><span class="sxs-lookup"><span data-stu-id="60129-200">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="60129-201">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="60129-201">Azure portal</span></span>
<span data-ttu-id="60129-202">Pour redémarrer une machine virtuelle à l’aide du portail Azure, sélectionnez votre machine virtuelle, puis cliquez sur le bouton **Redémarrer** comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="60129-202">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span></span>

![Redémarrage d’une machine virtuelle dans le portail Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="60129-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="60129-204">Azure CLI 1.0</span></span>
<span data-ttu-id="60129-205">L’exemple suivant redémarre la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-205">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="60129-206">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="60129-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="60129-207">Azure CLI 2.0</span></span>
<span data-ttu-id="60129-208">L’exemple suivant utilise [az vm restart](/cli/azure/vm#restart) pour redémarrer la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-208">The following example uses [az vm restart](/cli/azure/vm#restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="60129-209">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="60129-210">Redéploiement d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="60129-210">Redeploy a VM</span></span>
<span data-ttu-id="60129-211">Vous pouvez redéployer une machine virtuelle vers un autre nœud dans Azure, ce qui peut permettre de résoudre les problèmes de mise en réseau sous-jacents.</span><span class="sxs-lookup"><span data-stu-id="60129-211">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="60129-212">Pour en savoir plus sur le redéploiement d’une machine virtuelle, consultez [Redéployer une machine virtuelle vers un nouveau nœud Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60129-212">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="60129-213">Une fois cette opération terminée, les données de disque éphémères sont perdues et les adresses IP dynamiques associées à la machine virtuelle sont mises à jour.</span><span class="sxs-lookup"><span data-stu-id="60129-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="60129-214">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="60129-214">Azure portal</span></span>
<span data-ttu-id="60129-215">Pour redéployer une machine virtuelle à l’aide du portail Azure, sélectionnez votre machine virtuelle et faites défiler jusqu'à la section **Support + dépannage**.</span><span class="sxs-lookup"><span data-stu-id="60129-215">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="60129-216">Cliquez sur le bouton **Redéployer** comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="60129-216">Click the **Redeploy** button as in the following example:</span></span>

![Redéploiement de la machine virtuelle dans le portail Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="60129-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="60129-218">Azure CLI 1.0</span></span>
<span data-ttu-id="60129-219">L’exemple suivant redéploie la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-219">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="60129-220">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="60129-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="60129-221">Azure CLI 2.0</span></span>
<span data-ttu-id="60129-222">L’exemple suivant utilise [az vm redeploy](/cli/azure/vm#redeploy) pour redéployer la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="60129-222">The following example use [az vm redeploy](/cli/azure/vm#redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="60129-223">Utilisez vos propres valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="60129-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-the-classic-deployment-model"></a><span data-ttu-id="60129-224">Machines virtuelles créées à l’aide du modèle de déploiement Classic</span><span class="sxs-lookup"><span data-stu-id="60129-224">VMs created by using the Classic deployment model</span></span>
<span data-ttu-id="60129-225">Procédez comme suit pour résoudre les problèmes de connexion SSH les plus courants sur les machines virtuelles créées à l’aide du modèle de déploiement Classic.</span><span class="sxs-lookup"><span data-stu-id="60129-225">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="60129-226">Après chaque étape, essayez de vous reconnecter à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60129-226">After each step, try reconnecting to the VM.</span></span>

* <span data-ttu-id="60129-227">Réinitialisez l’accès à distance à partir du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60129-227">Reset remote access from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="60129-228">Dans le portail Azure, sélectionnez votre machine virtuelle et cliquez sur le bouton **Réinitialiser à distance...**.</span><span class="sxs-lookup"><span data-stu-id="60129-228">On the Azure portal, select your VM and click the **Reset Remote...** button.</span></span>
* <span data-ttu-id="60129-229">Redémarrez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60129-229">Restart the VM.</span></span> <span data-ttu-id="60129-230">Dans le [portail Azure](https://portal.azure.com), sélectionnez votre machine virtuelle et cliquez sur le bouton **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="60129-230">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span></span>
    
* <span data-ttu-id="60129-231">Redéployez la machine virtuelle vers un nouveau nœud Azure.</span><span class="sxs-lookup"><span data-stu-id="60129-231">Redeploy the VM to a new Azure node.</span></span> <span data-ttu-id="60129-232">Pour en savoir plus sur le redéploiement d’une machine virtuelle, consultez [Redéployer une machine virtuelle vers un nouveau nœud Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60129-232">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="60129-233">Une fois cette opération terminée, les données de disque éphémères sont perdues et les adresses IP dynamiques associées à la machine virtuelle sont mises à jour.</span><span class="sxs-lookup"><span data-stu-id="60129-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
* <span data-ttu-id="60129-234">Suivez les instructions dans [Comment réinitialiser le service Bureau à distance ou son mot de passe de connexion dans une machine virtuelle Windows](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) pour :</span><span class="sxs-lookup"><span data-stu-id="60129-234">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="60129-235">réinitialiser le mot de passe ou la clé SSH ;</span><span class="sxs-lookup"><span data-stu-id="60129-235">Reset the password or SSH key.</span></span>
  * <span data-ttu-id="60129-236">créer un nouveau compte utilisateur *sudo* ;</span><span class="sxs-lookup"><span data-stu-id="60129-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="60129-237">réinitialiser la configuration SSH.</span><span class="sxs-lookup"><span data-stu-id="60129-237">Reset the SSH configuration.</span></span>
* <span data-ttu-id="60129-238">Vérifiez l’intégrité des ressources de la ressource de machine virtuelle et recherchez s’il existe des problèmes liés à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="60129-238">Check the VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="60129-239">Sélectionnez votre machine virtuelle et faites défiler jusqu’à **Paramètres** > **Vérifier l’intégrité**.</span><span class="sxs-lookup"><span data-stu-id="60129-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60129-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="60129-240">Additional resources</span></span>
* <span data-ttu-id="60129-241">Si vous ne parvenez toujours pas à établir une connexion SSH à votre machine virtuelle une fois ces étapes effectuées, suivez les [étapes supplémentaires de dépannage détaillées](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour découvrir des étapes supplémentaires susceptibles de résoudre votre problème.</span><span class="sxs-lookup"><span data-stu-id="60129-241">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span></span>
* <span data-ttu-id="60129-242">Pour plus d’informations sur la résolution des problèmes d’accès aux applications, consultez la page [Résolution des problèmes d’accès à une application exécutée sur une machine virtuelle Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="60129-242">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="60129-243">Pour plus d’informations sur la résolution des problèmes liés aux machines virtuelles créées à l’aide du modèle de déploiement Classic, consultez [Réinitialisation d’un mot de passe ou de SSH pour les machines virtuelles basées sur Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60129-243">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

