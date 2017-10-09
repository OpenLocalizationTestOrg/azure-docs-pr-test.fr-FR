---
title: "aaaInstall un contrôleur de domaine Active Directory réplica dans Azure | Documents Microsoft"
description: "Un didacticiel qui explique comment tooinstall un contrôleur de domaine à partir d’un annuaire local Active Directory de la forêt sur une machine virtuelle Azure."
services: virtual-network
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8c9ebf1b-289a-4dd6-9567-a946450005c0
ms.service: virtual-network
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 74876fce2ca2a29f02c2828f9b3a21227248233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-replica-active-directory-domain-controller-in-an-azure-virtual-network"></a>Installation d’un contrôleur de domaine Active Directory de réplication dans un réseau virtuel Azure
Cette rubrique montre comment tooinstall autres contrôleurs de domaine (également appelé réplica de contrôleurs de domaine) pour un domaine d’Active Directory local sur les machines virtuelles Azure (VM) dans un réseau virtuel Azure.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.

Les rubriques suivantes peuvent également vous intéresser :

* Vous pouvez, si vous le souhaitez, installer une nouvelle forêt Active Directory sur un réseau virtuel Azure. Dans ce cas, consultez la page [Installation d’une nouvelle forêt Active Directory sur un réseau virtuel Azure](active-directory-new-forest-virtual-machine.md).
* Pour obtenir des recommandations sur l'installation d’AD DS (Active Directory Domain Services) sur un réseau virtuel Azure, consultez la page [Recommandations en matière de déploiement de Windows Server Active Directory sur des machines virtuelles Microsoft Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Schéma du scénario
Dans ce scénario, les utilisateurs externes doivent tooaccess les applications qui s’exécutent sur des serveurs joints au domaine. Hello machines virtuelles qui exécutent des serveurs d’applications hello et hello des contrôleurs de domaine réplica sont installés dans un réseau virtuel Azure. Hello réseau virtuel peut être réseau local de toohello connectés par un [VPN de site à site](../vpn-gateway/vpn-gateway-site-to-site-create.md) connexion, comme indiqué dans les éléments suivants de hello diagramme, ou vous pouvez utiliser [ExpressRoute](../expressroute/expressroute-locations-providers.md) pour une connexion plus rapide.

serveurs d’applications Hello et contrôleurs de domaine hello sont déployés au sein des services cloud distincts toodistribute calculer le traitement et, dans [haute disponibilité](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour une meilleure tolérance.
les contrôleurs de domaine Hello répliquent entre eux et avec les contrôleurs de domaine local à l’aide de la réplication Active Directory. Aucun outil de synchronisation n'est nécessaire.

![Schéma d’un contrôleur de domaine Active Directory de réplication dans un réseau virtuel Azure][1]

## <a name="create-an-active-directory-site-for-hello-azure-virtual-network"></a>Créer un site Active Directory pour hello réseau virtuel Azure
Il s’agit d’une bonne idée de toocreate un site dans Active Directory qui représente hello réseau région toohello réseau virtuel associé. Cela aide à optimiser l'authentification, la réplication et d'autres opérations de localisation du contrôleur de domaine. Hello étapes suivantes expliquent comment toocreate un site et pour plus d’informations, consultez [ajouter un nouveau Site](https://technet.microsoft.com/library/cc781496.aspx).

1. Ouvrez Sites et services Active Directory : **Gestionnaire de serveur** > **Outils** > **Sites et services Active Directory**.
2. Créer une région de hello toorepresent site où vous avez créé un réseau virtuel Azure : cliquez sur **Sites** > **Action** > **nouveau site** > type nom de Hello de hello nouveau site, tels que Azure région ouest des États-Unis > sélectionnez un lien de site > **OK**.
3. Créer un sous-réseau et l’associer à un nouveau site de hello : double-cliquez sur **Sites** > avec le bouton droit **sous-réseaux** > **nouveau sous-réseau** > type de plage d’adresses IP hello réseau virtuel de Hello (par exemple, 10.1.0.0/16 dans le schéma du scénario hello) > sélectionnez hello nouveau site Azure > **OK**.

## <a name="create-an-azure-virtual-network"></a>Création d'un réseau virtuel Azure
1. Bonjour [portail Azure classic](https://manage.windowsazure.com), cliquez sur **nouveau** > **Services réseau** > **réseau virtuel**  >  **Création personnalisée** et Assistant de hello toocomplete des valeurs suivantes de hello d’utilisation.

   | Sur cette page de l'Assistant... | Spécifiez les valeurs suivantes |
   | --- | --- |
   |  **Détails du réseau virtuel** |<p>Nom : Tapez un nom pour le réseau virtuel hello, telles que WestUSVNet.</p><p>Région : Choisissez la région hello le plus proche.</p> |
   |  **Connectivité DNS et VPN** |<p>Serveurs DNS : Spécifiez le nom de hello et adresse IP d’un ou plusieurs serveurs DNS local.</p><p>Connectivité : sélectionnez **Configuration d'un VPN de site à site**.</p><p>Réseau Local : Spécifier un nouveau réseau local.</p><p>Si vous utilisez ExpressRoute au lieu d’un VPN, consultez [Configuration d’une connexion ExpressRoute via un fournisseur Exchange](../expressroute/expressroute-locations-providers.md).</p> |
   |  **Connectivité de site à site** |<p>Nom : Entrez un nom pour le réseau local de hello.</p><p>Adresse IP du périphérique VPN : spécifiez hello adresse IP publique du périphérique hello qui se connecteront toohello des réseaux virtuels. périphérique VPN de Hello ne peut pas se trouver derrière un NAT.</p><p>Adresse : Spécifiez les plages d’adresses hello pour votre réseau local (par exemple 192.168.0.0/16 dans le schéma du scénario hello).</p> |
   |  **Espaces d’adressage du réseau virtuel** |<p>Espace d’adressage : Spécifiez la plage d’adresses IP hello pour les machines virtuelles que vous souhaitez toorun Bonjour réseau virtuel Azure (par exemple, 10.1.0.0/16 dans le schéma du scénario hello). Cette plage d’adresses ne peuvent pas chevaucher les plages d’adresses hello de réseau local de hello.</p><p>Sous-réseaux : Spécifiez un nom et une adresse pour un sous-réseau pour les serveurs d’applications hello (tels que serveur frontal, 10.1.1.0/24) et pourquoi les contrôleurs de domaine (comme principal, 10.1.2.0/24).</p><p>Cliquez sur **Ajouter un sous-réseau de passerelle**.</p> |
2. Ensuite, vous devez configurer toocreate de passerelle de réseau virtuel hello une connexion VPN de site à site sécurisée. Consultez [configurer une passerelle de réseau virtuel](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) pour obtenir des instructions hello.
3. Créer la connexion de VPN de site à site hello entre le réseau virtuel hello et un appareil VPN sur site. Consultez [configurer une passerelle de réseau virtuel](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) pour obtenir des instructions hello.

## <a name="create-azure-vms-for-hello-dc-roles"></a>Créer des machines virtuelles Azure hello pour les rôles de contrôleur de domaine
Répétez hello suivant les étapes toocreate rôle de contrôleur de domaine machines virtuelles toohost hello en fonction des besoins. Vous devez déployer au moins deux contrôleurs de domaine tooprovide une tolérance de panne et la redondance virtuel. Si hello réseau virtuel Azure comprend au moins deux contrôleurs de domaine qui sont configurés de la même façon (autrement dit, ils sont à la fois des catalogues globaux, exécution serveur DNS, et aucun contient n’importe quel rôle FSMO et ainsi de suite) puis, placez des machines virtuelles hello qui s’exécutent les contrôleurs de domaine dans un groupe à haute disponibilité pour une meilleure tolérance.
toocreate hello machines virtuelles à l’aide de Windows PowerShell au lieu de hello l’interface utilisateur, consultez [toocreate d’utiliser Azure PowerShell et préconfigurer des Machines virtuelles basées sur Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. Bonjour [portail Azure classic](https://manage.windowsazure.com), cliquez sur **nouveau** > **de calcul** > **virtuels**  >  **à partir de la galerie**. Utilisez hello suivant valeurs toocomplete hello Assistant. Acceptez la valeur de par défaut de hello pour un paramètre, sauf si une autre valeur est suggérée ou requis.

   | Sur cette page de l'Assistant... | Spécifiez les valeurs suivantes |
   | --- | --- |
   |  **Choix d’une image** |Windows Server 2012 R2 Datacenter |
   |  **Configuration de la machine virtuelle** |<p>Nom de machine virtuelle : Tapez un nom en une seule partie (par exemple, AzureDC1).</p><p>Nouveau nom d’utilisateur : Hello nom de Type utilisateur. Cet utilisateur sera un membre du groupe Administrateurs local de hello sur hello machine virtuelle. Vous devez toosign de ce nom dans toohello machine virtuelle pour hello première fois. compte intégré de Hello nommé administrateur ne fonctionnera pas.</p><p>Nouveau mot de passe/confirmation : saisissez un mot de passe</p> |
   |  **Configuration de la machine virtuelle** |<p>Service de cloud computing : Choisissez <b>créer un service cloud</b> pourquoi la première machine virtuelle et cliquez sur ce même nom de service de cloud lorsque vous créez plusieurs machines virtuelles qui hébergeront hello rôle de contrôleur de domaine.</p><p>Nom DNS du service cloud : indiquez un nom global unique</p><p>Région/groupe d’affinités/réseau virtuel : spécifiez le nom de réseau virtuel hello (par exemple, WestUSVNet).</p><p>Compte de stockage : Choisissez <b>utiliser un compte de stockage généré automatiquement</b> pourquoi la première machine virtuelle et sélectionnez ce nom de compte de stockage lorsque vous créez plusieurs machines virtuelles qui hébergeront hello rôle de contrôleur de domaine.</p><p>Groupe à haute disponibilité : Choisissez <b>Créer un groupe à haute disponibilité</b>.</p><p>Nom de groupe à haute disponibilité : Type de nom hello groupe à haute disponibilité lorsque vous créez hello première machine virtuelle et puis sélectionnez que même nom lorsque vous créez plusieurs machines virtuelles.</p> |
   |  **Configuration de la machine virtuelle** |<p>Sélectionnez <b>hello d’installer l’Agent de machine virtuelle</b> et toutes les autres extensions que vous avez besoin.</p> |
2. Attacher un machine virtuelle qui exécutera le rôle de serveur de contrôleur de domaine hello du tooeach disque. disque supplémentaire de Hello est la base de données nécessaires toostore hello AD, les journaux et SYSVOL. Spécifiez une taille de disque hello (par exemple, 10 Go), laissez hello **préférences de Cache hôte** défini trop**aucun**. Pour connaître les étapes hello, consultez [comment tooAttach un tooa de disque de données Machine virtuelle Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Après la première connexion au toohello machine virtuelle, ouvrez **le Gestionnaire de serveur** > **File and Storage Services** toocreate un volume sur ce disque à l’aide de NTFS.
4. Réserver une adresse IP statique pour les ordinateurs virtuels qui exécuteront le rôle de contrôleur de domaine hello. tooreserve une adresse IP statique, télécharger hello Microsoft Web Platform Installer et [installer Azure PowerShell](/powershell/azure/overview) et exécutez l’applet de commande Set-AzureStaticVNetIP de hello. Par exemple :

    'Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 Set-AzureStaticVNetIP -IPAddress 10.0.0.4 Update-AzureVM

Pour plus d’informations sur la configuration d’une adresse IP, consultez [Configuration d’une adresse IP interne statique pour une machine virtuelle](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-ad-ds-on-azure-vms"></a>Installation des services AD DS sur des machines virtuelles Azure
Connectez-vous à tooa machine virtuelle, puis vérifiez que vous avez connectivité entre hello site-à-site VPN ou ExpressRoute connexion tooresources sur votre réseau local. Installez les services AD DS sur hello machines virtuelles Azure. Vous pouvez utiliser le même processus que vous utilisez tooinstall un autre contrôleur de domaine sur votre réseau local (l’interface utilisateur, Windows PowerShell ou un fichier de réponses). Lorsque vous installez les services AD DS, assurez-vous que vous spécifiez le nouveau volume de hello pour l’emplacement de hello Hello de base de données Active Directory, les journaux et SYSVOL. Si vous avez besoin d’un rappel concernant l’installation des services AD DS, consultez [Installer les services de domaine Active Directory (Niveau 100)](https://technet.microsoft.com/library/hh472162.aspx) ou [Installer un contrôleur de domaine de réplication Windows Server 2012 dans un domaine existant (Niveau 200)](https://technet.microsoft.com/library/jj574134.aspx).

## <a name="reconfigure-dns-server-for-hello-virtual-network"></a>Reconfigurer le serveur DNS pour le réseau virtuel de hello
1. Bonjour [portail Azure](https://portal.azure.com), Bonjour **recherche les ressources** , entrez *réseaux virtuels*, puis cliquez sur **des réseaux virtuels (classiques)** dans résultats de la recherche Hello. Cliquez sur nom hello du réseau virtuel de hello, puis [reconfigurer hello DNS adresses IP de votre réseau virtuel](../virtual-network/virtual-network-manage-network.md#dns-servers) des adresses IP statiques toouse hello affecté toohello contrôleurs de domaine réplica à la place des adresses IP hello d’un serveur DNS local serveurs.
2. tooensure que le réplica hello toutes les machines virtuelles de contrôleur de domaine sur le réseau virtuel de hello sont configurés avec les serveurs DNS toouse hello réseau virtuel, et cliquez sur **virtuels**et cliquez sur colonne d’état hello pour chaque ordinateur virtuel, puis cliquez sur **redémarrer** . Attendez que hello machine virtuelle s’affiche **en cours d’exécution** état avant d’essayer de toosign dans celui-ci.

## <a name="create-vms-for-application-servers"></a>création de machines virtuelles pour les serveurs d'applications
1. Répétez hello suivant les étapes toocreate machines virtuelles toorun en tant que serveurs d’applications. Acceptez la valeur de par défaut de hello pour un paramètre, sauf si une autre valeur est suggérée ou requis.

   | Sur cette page de l'Assistant... | Spécifiez les valeurs suivantes |
   | --- | --- |
   |  **Choix d’une image** |Windows Server 2012 R2 Datacenter |
   |  **Configuration de la machine virtuelle** |<p>Nom de machine virtuelle : Tapez un nom en une seule partie (par exemple, AppServer1).</p><p>Nouveau nom d’utilisateur : Hello nom de Type utilisateur. Cet utilisateur sera un membre du groupe Administrateurs local de hello sur hello machine virtuelle. Vous devez toosign de ce nom dans toohello machine virtuelle pour hello première fois. compte intégré de Hello nommé administrateur ne fonctionnera pas.</p><p>Nouveau mot de passe/confirmation : saisissez un mot de passe</p> |
   |  **Configuration de la machine virtuelle** |<p>Service de cloud computing : Choisissez **créer un service cloud** pour hello premier ordinateur virtuel et sélectionnez même de cloud nom du service lorsque vous créez plusieurs machines virtuelles qui hébergera application hello.</p><p>Nom DNS du service cloud : indiquez un nom global unique</p><p>Région/groupe d’affinités/réseau virtuel : spécifiez le nom de réseau virtuel hello (par exemple, WestUSVNet).</p><p>Compte de stockage : Choisissez **utiliser un compte de stockage généré automatiquement** pour hello premier ordinateur virtuel et sélectionnez ce nom de compte de stockage lorsque vous créez plusieurs machines virtuelles qui hébergera application hello.</p><p>Groupe à haute disponibilité : Choisissez **Créer un groupe à haute disponibilité**.</p><p>Nom de groupe à haute disponibilité : Type de nom hello groupe à haute disponibilité lorsque vous créez hello première machine virtuelle et puis sélectionnez que même nom lorsque vous créez plusieurs machines virtuelles.</p> |
   |  **Configuration de la machine virtuelle** |<p>Sélectionnez <b>hello d’installer l’Agent de machine virtuelle</b> et toutes les autres extensions que vous avez besoin.</p> |
2. Une fois que chaque machine virtuelle est configurée, connectez-vous et le joindre toohello domaine. Dans le **Gestionnaire de serveur**, cliquez sur **Serveur Local** > **GROUPE DE TRAVAIL** > **MODIFIER...** puis sélectionnez **domaine** et nom du type hello de votre domaine local. Informations d’identification d’un utilisateur de domaine et redémarrez jonction de domaine hello VM toocomplete hello.

toocreate hello machines virtuelles à l’aide de Windows PowerShell au lieu de hello l’interface utilisateur, consultez [toocreate d’utiliser Azure PowerShell et préconfigurer des Machines virtuelles basées sur Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Pour plus d'informations sur l'utilisation de Windows PowerShell, consultez [Bien démarrer avec les applets de commande Azure](/powershell/azure/overview) et le [Guide de référence des applets de commande Azure](/powershell/azure/get-started-azureps).

## <a name="additional-resources"></a>Ressources supplémentaires
* [Instructions pour le déploiement de Windows Server Active Directory sur Azure Virtual Machines](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Comment tooupload locales existantes tooAzure de contrôleurs de domaine de Hyper-V à l’aide d’Azure PowerShell](http://support.microsoft.com/kb/2904015)
* [Installer une nouvelle forêt Active Directory sur un réseau virtuel Azure](active-directory-new-forest-virtual-machine.md)
* [Azure Virtual Network](../virtual-network/virtual-networks-overview.md)
* [Iaas des professionnels de l’informatique Microsoft Azure : principes de base des machines virtuelles (01)](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Iaas des professionnels de l’informatique Microsoft Azure :(05) Création de réseaux virtuels pour la connectivité entre différents locaux](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Azure PowerShell](/powershell/azure/overview)
* [Applets de commande de gestion Azure](/powershell/module/azurerm.compute/#virtual_machines)

<!--Image references-->
[1]: ./media/active-directory-install-replica-active-directory-domain-controller/ReplicaDCsOnAzureVNet.png
