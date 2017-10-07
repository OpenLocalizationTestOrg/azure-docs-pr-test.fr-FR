---
title: aaaCannot se connecter avec RDP tooa Windows VM dans Azure | Documents Microsoft
description: "Résoudre les problèmes lorsque vous ne pouvez pas vous connecter tooyour Windows machine virtuelle Azure à l’aide du Bureau à distance"
keywords: "Erreur du Bureau à distance, une erreur de connexion Bureau à distance, ne peut pas se connecter tooVM, dépannage de bureau à distance"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a>Résoudre les problèmes de connexions de bureau à distance tooan machine virtuelle Azure
Hello protocole RDP (Remote Desktop) connexion tooyour basé sur Windows Azure virtual machine (VM) peut échouer pour diverses raisons, vous laissant tooaccess Impossible de votre machine virtuelle. problème de Hello peut être hello service Bureau à distance sur hello VM, hello connexion réseau ou client de bureau à distance hello sur votre ordinateur hôte. Cet article vous guide tout au long de certaines hello courants méthodes tooresolve RDP problèmes de connexion. 

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/support/options/) et sélectionnez **obtenir prend en charge**.

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a>Étapes de dépannage rapide
Après chaque étape de résolution des problèmes, essayez de vous reconnecter toohello machine virtuelle :

1. Réinitialisez la configuration du Bureau à distance.
2. Vérifiez les règles de groupe de sécurité réseau / de point de terminaison de services cloud.
3. Examinez les journaux de console de la machine virtuelle.
4. Réinitialiser hello NIC pour machine virtuelle de hello.
5. Hello de vérification d’intégrité de ressource de machine virtuelle.
6. Réinitialisez le mot de passe de votre machine virtuelle.
7. Redémarrez votre machine virtuelle.
8. Redéployez votre machine virtuelle.

Si vous avez besoin de procédures plus détaillées et d’explications, poursuivez la lecture. Vérifiez que l’équipement réseau local, notamment les routeurs et les pare-feu, ne bloque pas le port TCP 3389 sortant, comme indiqué dans les [scénarios détaillés de dépannage RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!TIP]
> Si hello **Connect** bouton pour votre machine virtuelle est grisée dans le portail de hello et vous n’êtes pas connecté tooAzure via un [Express Route](../../expressroute/expressroute-introduction.md) ou [VPN de Site à Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connexion, vous devez toocreate et affecter votre machine virtuelle une adresse IP publique d’adresses que vous peuvent utiliser RDP. Pour en savoir plus sur les adresses IP publiques dans Azure, consultez [cet article](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).


## <a name="ways-tootroubleshoot-rdp-issues"></a>Problèmes de façons tootroubleshoot RDP
Vous pouvez résoudre les machines virtuelles créées à l’aide du modèle de déploiement du Gestionnaire de ressources hello à l’aide d’une des méthodes suivantes de hello :

* [Portail Azure](#using-the-azure-portal) - great si vous avez besoin de tooquickly réinitialiser hello des informations d’identification utilisateur ou de la configuration de RDP et que vous n’avez hello Windows Azure tools installés.
* [Azure PowerShell](#using-azure-powershell) : Si vous êtes rapidement à l’aise avec une invite PowerShell, réinitialisation hello RDP configuration utilisateur informations d’identification ou à l’aide des applets de commande PowerShell Azure hello.

Vous trouverez également les étapes de résolution des problèmes des machines virtuelles créées à l’aide de hello [modèle de déploiement classique](#troubleshoot-vms-created-using-the-classic-deployment-model).

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a>Dépannage à l’aide de hello portail Azure
Après chaque étape de dépannage, réessayez de vous connecter tooyour machine virtuelle. Si vous ne pouvez toujours pas vous connecter, essayez l’étape suivante de hello.

1. **Réinitialisez votre connexion RDP**. Cette étape de dépannage réinitialise la configuration de RDP hello lorsque les connexions distantes sont désactivées ou les règles de pare-feu Windows bloquent le protocole RDP, par exemple.
   
    Bonjour portail Azure, sélectionnez votre machine virtuelle. Défiler hello paramètres volet toohello **prise en charge + dépannage** section vers le bas de la liste de hello. Cliquez sur hello **réinitialisation de mot de passe** bouton. Ensemble hello **Mode** trop**uniquement à la configuration de réinitialisation** puis cliquez sur hello **mise à jour** bouton :
   
    ![Réinitialiser la configuration de RDP hello Bonjour portail Azure](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. **Vérifiez les règles du groupe de sécurité réseau**. Utilisez [les flux IP vérifier](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm si une règle dans un groupe de sécurité réseau bloque tooor le trafic à partir d’un ordinateur virtuel. Vous pouvez également examiner les règles tooensure entrant « Autoriser » NSG règle existe et qu’il est hiérarchisé pour le port RDP (valeur par défaut 3389) de groupe de sécurité efficace. Pour plus d’informations, consultez [le trafic en utilisant les règles de sécurité efficace tootroubleshoot VM](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

3. **Passez en revue les diagnostics de démarrage de la machine virtuelle**. Cette étape de dépannage passe en revue les toodetermine de journaux de console de machine virtuelle hello si hello VM signale un problème. Les diagnostics de démarrage ne sont pas activés sur toutes les machines virtuelles et cette étape de dépannage peut être facultative.
   
    Étapes de dépannage spécifiques sortent du cadre hello de cet article, mais il peuvent indiquer un problème plus large qui affecte la connectivité RDP. Pour plus d’informations sur l’examen des journaux de la console hello et de capture d’écran de la machine virtuelle, consultez [Diagnostics de démarrage pour les machines virtuelles](boot-diagnostics.md).

4. **Réinitialisation hello NIC pour machine virtuelle de hello**. Pour plus d’informations, consultez [comment tooreset NIC pour machine virtuelle de Windows Azure](reset-network-interface.md).
5. **Vérifiez hello contrôle d’intégrité de machine virtuelle**. Cette étape de dépannage vérifie il n’y a aucun problème connu avec hello plateforme Azure peut avoir un impact sur connectivité toohello machine virtuelle.
   
    Bonjour portail Azure, sélectionnez votre machine virtuelle. Défiler hello paramètres volet toohello **prise en charge + dépannage** section vers le bas de la liste de hello. Cliquez sur hello **l’intégrité des ressources** bouton. Une machine virtuelle saine est indiquée comme étant **Disponible** :
   
    ![Vérifier l’intégrité des ressources VM Bonjour portail Azure](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. **Réinitialisez les informations d’identification de l’utilisateur**. Cette étape de dépannage réinitialise le mot de passe hello sur un compte d’administrateur local lorsque vous n’êtes pas sûr ou que vous avez oublié les informations d’identification hello.
   
    Bonjour portail Azure, sélectionnez votre machine virtuelle. Défiler hello paramètres volet toohello **prise en charge + dépannage** section vers le bas de la liste de hello. Cliquez sur hello **réinitialisation de mot de passe** bouton. Vérifiez que hello **Mode** est défini trop**réinitialisation de mot de passe** , puis entrez votre nom d’utilisateur et un mot de passe. Enfin, cliquez sur hello **mise à jour** bouton :
   
    ![Réinitialiser les informations d’identification utilisateur de hello Bonjour portail Azure](./media/troubleshoot-rdp-connection/reset-password.png)
7. **Redémarrez votre machine virtuelle**. Cette étape de dépannage peut corriger les problèmes sous-jacents rencontre hello machine virtuelle proprement dite.
   
    Sélectionnez votre machine virtuelle hello portail Azure, cliquez sur hello **vue d’ensemble** onglet. Cliquez sur hello **redémarrer** bouton :
   
    ![Redémarrez hello VM Bonjour portail Azure](./media/troubleshoot-rdp-connection/restart-vm.png)
8. **Redéployez votre machine virtuelle**. Cette étape de dépannage redéploie votre hôte tooanother de machine virtuelle dans Azure toocorrect les problèmes de mise en réseau ou de la plateforme sous-jacente.
   
    Bonjour portail Azure, sélectionnez votre machine virtuelle. Défiler hello paramètres volet toohello **prise en charge + dépannage** section vers le bas de la liste de hello. Cliquez sur hello **redéployer** bouton, puis cliquez sur **redéployer**:
   
    ![Redéployer hello VM Bonjour portail Azure](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    Une fois cette opération terminée, données disque éphémère sont perdus et dynamiques adresses IP qui sont associés à hello machine virtuelle sont mises à jour.

Si vous rencontrez toujours des problèmes liés au protocole RDP, vous pouvez [ouvrir une demande de support](https://azure.microsoft.com/support/options/) ou lire [des concepts et des étapes de résolution des problèmes RDP plus détaillés](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-using-azure-powershell"></a>Résolution des problèmes à l’aide d’Azure PowerShell
Si vous n’avez pas déjà fait, [installer et configurer hello la dernière version d’Azure PowerShell](/powershell/azure/overview).

Hello exemples suivants utilisent les variables telles que `myResourceGroup`, `myVM`, et `myVMAccessExtension`. Remplacez ces noms de variables et les emplacements par vos propres valeurs.

> [!NOTE]
> Vous réinitialisez les informations d’identification utilisateur de hello et configuration de RDP hello à l’aide de hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) applet de commande PowerShell. Bonjour, suivez les exemples, `myVMAccessExtension` est un nom que vous spécifiez dans le cadre du processus de hello. Si vous avez déjà travaillé avec hello VMAccessAgent, vous pouvez obtenir le nom hello d’extension existante de hello à l’aide de `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` toocheck des propriétés de hello Hello machine virtuelle. nom de hello tooview, voir sous la section hello « Extensions » de la sortie de hello.

Après chaque étape de dépannage, réessayez de vous connecter tooyour machine virtuelle. Si vous ne pouvez toujours pas vous connecter, essayez l’étape suivante de hello.

1. **Réinitialisez votre connexion RDP**. Cette étape de dépannage réinitialise la configuration de RDP hello lorsque les connexions distantes sont désactivées ou les règles de pare-feu Windows bloquent le protocole RDP, par exemple.
   
    exemple de suivi de Hello réinitialise la connexion RDP de hello sur un ordinateur virtuel nommé `myVM` Bonjour `WestUS` emplacement et dans le groupe de ressources hello nommé `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. **Vérifiez les règles du groupe de sécurité réseau**. Cette étape de dépannage vérifie que vous disposez d’une règle dans votre trafic RDP de toopermit groupe de sécurité réseau. port par défaut Hello RDP est le port TCP 3389. Un trafic RDP de toopermit règle ne peut-être pas être créé automatiquement lorsque vous créez votre machine virtuelle.
   
    Tout d’abord, affectez toutes les données de configuration hello pour votre groupe de sécurité réseau de toohello `$rules` variable. Hello exemple suivant obtient des informations sur hello groupe de sécurité réseau nommé `myNetworkSecurityGroup` dans le groupe de ressources hello nommé `myResourceGroup`:
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    Maintenant, hello les règles de vue qui sont configurés pour ce groupe de sécurité réseau. Vérifiez qu’il existe une règle tooallow le port TCP 3389 pour les connexions entrantes comme suit :
   
    ```powershell
    $rules.SecurityRules
    ```
   
    Hello suivant montre une règle de sécurité qui autorise le trafic RDP. Vous pouvez voir que `Protocol`, `DestinationPortRange`, `Access` et `Direction` sont correctement configurés :
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    Si vous ne disposez pas de règle autorisant le trafic RDP, [créez une règle de groupe de sécurité réseau](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Autorisez le port TCP 3389.
3. **Réinitialisez les informations d’identification de l’utilisateur**. Cette étape de dépannage réinitialise le mot de passe hello sur le compte d’administrateur local hello que vous spécifiez lorsque vous ne connaissez pas, ou que vous avez oublié, informations d’identification hello.
   
    Spécifiez d’abord hello nom d’utilisateur et un mot de passe en assignant des informations d’identification toohello `$cred` variable comme suit :
   
    ```powershell
    $cred=Get-Credential
    ```
   
    À présent, mettez à jour les informations d’identification hello sur votre machine virtuelle. Hello exemple suivant met à jour les informations d’identification hello sur un ordinateur virtuel nommé `myVM` Bonjour `WestUS` emplacement et dans le groupe de ressources hello nommé `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. **Redémarrez votre machine virtuelle**. Cette étape de dépannage peut corriger les problèmes sous-jacents rencontre hello machine virtuelle proprement dite.
   
    Hello après le redémarrage de l’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. **Redéployez votre machine virtuelle**. Cette étape de dépannage redéploie votre hôte tooanother de machine virtuelle dans Azure toocorrect les problèmes de mise en réseau ou de la plateforme sous-jacente.
   
    Hello suivant redéploiements ultérieurs d’exemple hello ordinateur virtuel nommé `myVM` Bonjour `WestUS` emplacement et dans le groupe de ressources hello nommé `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

Si vous rencontrez toujours des problèmes liés au protocole RDP, vous pouvez [ouvrir une demande de support](https://azure.microsoft.com/support/options/) ou lire [des concepts et des étapes de résolution des problèmes RDP plus détaillés](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a>Résoudre les problèmes des machines virtuelles créées à l’aide du modèle de déploiement classique de hello
Après chaque étape de résolution des problèmes, essayez de vous reconnecter toohello machine virtuelle.

1. **Réinitialisez votre connexion RDP**. Cette étape de dépannage réinitialise la configuration de RDP hello lorsque les connexions distantes sont désactivées ou les règles de pare-feu Windows bloquent le protocole RDP, par exemple.
   
    Bonjour portail Azure, sélectionnez votre machine virtuelle. Cliquez sur hello **... Plus** , puis cliquez sur **réinitialiser l’accès à distance**:
   
    ![Réinitialiser la configuration de RDP hello Bonjour portail Azure](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. **Vérifiez les points de terminaison des Services cloud**. Cette étape de dépannage vérifie que vous avez des points de terminaison dans le trafic RDP de toopermit Services de cloud computing. port par défaut Hello RDP est le port TCP 3389. Un trafic RDP de toopermit règle ne peut-être pas être créé automatiquement lorsque vous créez votre machine virtuelle.
   
   Bonjour portail Azure, sélectionnez votre machine virtuelle. Cliquez sur hello **points de terminaison** bouton des points de terminaison hello tooview actuellement configurées pour votre machine virtuelle. Vérifiez la présence de points de terminaison autorisant le trafic RDP sur le port TCP 3389.
   
   Hello, l’exemple suivant montre les points de terminaison valides qui autorisent le trafic RDP :
   
   ![Vérifiez les points de terminaison de Services de cloud computing dans hello portail Azure](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   Si vous ne disposez pas d’un point de terminaison autorisant le trafic RDP, [créez un point de terminaison de Services cloud](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Autoriser TCP tooprivate le port 3389.
3. **Passez en revue les diagnostics de démarrage de la machine virtuelle**. Cette étape de dépannage passe en revue les toodetermine de journaux de console de machine virtuelle hello si hello VM signale un problème. Les diagnostics de démarrage ne sont pas activés sur toutes les machines virtuelles et cette étape de dépannage peut être facultative.
   
    Étapes de dépannage spécifiques sortent du cadre hello de cet article, mais il peuvent indiquer un problème plus large qui affecte la connectivité RDP. Pour plus d’informations sur l’examen des journaux de la console hello et de capture d’écran de la machine virtuelle, consultez [Diagnostics de démarrage pour les machines virtuelles](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).
4. **Vérifiez hello contrôle d’intégrité de machine virtuelle**. Cette étape de dépannage vérifie il n’y a aucun problème connu avec hello plateforme Azure peut avoir un impact sur connectivité toohello machine virtuelle.
   
    Bonjour portail Azure, sélectionnez votre machine virtuelle. Défiler hello paramètres volet toohello **prise en charge + dépannage** section vers le bas de la liste de hello. Cliquez sur hello **l’intégrité des ressources** bouton. Une machine virtuelle saine est indiquée comme étant **Disponible** :
   
    ![Vérifier l’intégrité des ressources VM Bonjour portail Azure](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. **Réinitialisez les informations d’identification de l’utilisateur**. Cette étape de dépannage réinitialise le mot de passe hello sur le compte d’administrateur local hello que vous spécifiez lorsque vous n’êtes pas sûr ou que vous avez oublié les informations d’identification hello.
   
    Bonjour portail Azure, sélectionnez votre machine virtuelle. Défiler hello paramètres volet toohello **prise en charge + dépannage** section vers le bas de la liste de hello. Cliquez sur hello **réinitialisation de mot de passe** bouton. Entrez votre nom d’utilisateur et un nouveau mot de passe. Enfin, cliquez sur hello **enregistrer** bouton :
   
    ![Réinitialiser les informations d’identification utilisateur de hello Bonjour portail Azure](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. **Redémarrez votre machine virtuelle**. Cette étape de dépannage peut corriger les problèmes sous-jacents rencontre hello machine virtuelle proprement dite.
   
    Sélectionnez votre machine virtuelle hello portail Azure, cliquez sur hello **vue d’ensemble** onglet. Cliquez sur hello **redémarrer** bouton :
   
    ![Redémarrez hello VM Bonjour portail Azure](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

Si vous rencontrez toujours des problèmes liés au protocole RDP, vous pouvez [ouvrir une demande de support](https://azure.microsoft.com/support/options/) ou lire [des concepts et des étapes de résolution des problèmes RDP plus détaillés](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-specific-rdp-errors"></a>Dépannage d’erreurs RDP spécifiques
Vous pouvez rencontrer un message d’erreur spécifique lors de la tentative de tooconnect tooyour machine virtuelle via RDP. Hello Voici les messages d’erreur les plus courants hello :

* [session à distance de Hello a été déconnectée, car il n’y a aucun tooprovide disponible aux serveurs de licences bureau à distance une licence](troubleshoot-specific-rdp-errors.md#rdplicense).
* [Bureau à distance ne peut pas trouver hello « nom de l’ordinateur »](troubleshoot-specific-rdp-errors.md#rdpname).
* [Une erreur d’authentification s’est produite. Hello autorité de sécurité locale ne peut pas être contactée](troubleshoot-specific-rdp-errors.md#rdpauth).
* [Message d’erreur de sécurité Windows : Vos informations d’identification n’ont pas fonctionné](troubleshoot-specific-rdp-errors.md#wincred).
* [Cet ordinateur ne peut pas se connecter l’ordinateur distant de toohello](troubleshoot-specific-rdp-errors.md#rdpconnect).

## <a name="additional-resources"></a>Ressources supplémentaires
Si aucune de ces erreurs s’est produite et vous ne pouvez pas vous connecter toohello machine virtuelle via le Bureau à distance, lisez hello détaillée [guide de dépannage pour le Bureau à distance](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Pour le dépannage des étapes de l’accès aux applications en cours d’exécution sur une machine virtuelle, consultez [application tooan de résoudre les accès en cours d’exécution sur une machine virtuelle Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Si vous rencontrez des problèmes à l’aide de SSH (Secure Shell) tooconnect tooa Linux VM dans Azure, consultez [tooa dépanner SSH connexions VM Linux dans Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

