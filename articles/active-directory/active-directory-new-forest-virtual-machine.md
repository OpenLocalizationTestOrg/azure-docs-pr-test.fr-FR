---
title: "aaaInstall une forêt Active Directory sur un réseau virtuel Azure | Documents Microsoft"
description: "Un didacticiel qui explique comment toocreate un nouvel annuaire Active Directory de la forêt sur un ordinateur virtuel (VM) sur un réseau virtuel Azure."
services: active-directory, virtual-network
keywords: "machine virtuelle active directory, installer une forêt active directory, vidéos azure active directory  "
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
tags: 
ms.assetid: eb7170d0-266a-4caa-adce-1855589d65d1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: joflore
ms.openlocfilehash: 08121130777cc3c206d7b5b38974982884dca1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-new-active-directory-forest-on-an-azure-virtual-network"></a>Installation d'une nouvelle forêt Active Directory sur un réseau virtuel Azure
Cette rubrique montre comment toocreate un nouveau Windows Server Active Directory environnement sur un réseau virtuel Azure sur un ordinateur virtuel (VM) sur un [réseau virtuel Azure](../virtual-network/virtual-networks-overview.md). Dans ce cas, hello réseau virtuel Azure n’est pas connecté tooan sur réseau local.

Les rubriques suivantes peuvent également vous intéresser :

* Pour obtenir une vidéo qui montre ces étapes, consultez [comment tooinstall un nouvel annuaire Active Directory de la forêt sur un réseau virtuel Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* Vous pouvez éventuellement [configurer un VPN de site à site](../vpn-gateway/vpn-gateway-site-to-site-create.md) puis installer une nouvelle forêt ou étendre un tooan de forêt locale réseau virtuel Azure. Dans ce cas, consultez la page [Installation d'un réplica de contrôleur de domaine Active Directory dans un réseau virtuel Azure](active-directory-install-replica-active-directory-domain-controller.md).
* Pour obtenir des recommandations sur l'installation des services de domaine Active Directory (AD DS) sur un réseau virtuel Azure, consultez la page [Recommandations en matière de déploiement de Windows Server Active Directory sur des machines virtuelles Microsoft Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Schéma du scénario
Dans ce scénario, les utilisateurs externes doivent tooaccess les applications qui s’exécutent sur des serveurs joints au domaine. machines virtuelles Hello qui exécutent des serveurs d’applications hello et machines virtuelles hello qui exécutent des contrôleurs de domaine sont installés dans leur propre service de cloud dans un réseau virtuel Azure. Elles sont également incluses dans un groupe à haute disponibilité pour une meilleure tolérance de panne.

![Forêt Active Directory sur une machine virtuelle dans Azure Virtual Network][1] 7

## <a name="how-does-this-differ-from-on-premises"></a>Quelles sont les différences par rapport à une installation locale ?
Les différences entre l'installation d'un contrôleur de domaine dans Azure ou localement sont minimes. principales différences de Hello sont répertoriées dans hello tableau suivant.

| tooconfigure... | Local | réseau virtuel Azure |
| --- | --- | --- |
| **Adresse IP pour le contrôleur de domaine hello** |Attribuez une adresse IP statique sur les propriétés de la carte réseau hello |Exécutez tooassign d’applet de commande Set-AzureStaticVNetIP hello une adresse IP statique |
| **Programme de résolution du client DNS** |Définir les Favoris et l’autre serveur DNS adresse du serveur sur hello propriétés des cartes réseau des membres du domaine |Définir l’adresse du serveur DNS sur les propriétés de réseau virtuel hello hello |
| **Stockage de base de données Active Directory** |Si vous le souhaitez modifier emplacement de stockage par défaut hello à partir de C:\ |Vous devez toochange emplacement de stockage par défaut à partir de C:\ |

## <a name="create-an-azure-virtual-network"></a>Création d'un réseau virtuel Azure
1. Se connecter toohello portail Azure classic.
2. Créez un réseau virtuel. Cliquez sur **Réseaux** > **Create a virtual network**. Utilisez les valeurs hello hello suivant table toocomplete hello Assistant.

   | Sur cette page de l'Assistant... | Spécifiez les valeurs suivantes |
   | --- | --- |
   |  **Détails du réseau virtuel** |<p>Nom : entrez le nom du réseau virtuel</p><p>Région : Choisissez la région de hello le plus proche</p> |
   |  **DNS et VPN** |<p>N'indiquez pas de serveur DNS</p><p>Ne sélectionnez pas d'option VPN</p> |
   |  **Espaces d’adressage du réseau virtuel** |<p>Nom du sous-réseau : entrez le nom du sous-réseau</p><p>Adresse IP de départ : <b>10.0.0.0</b></p><p>CIDR : <b>/24 (256)</b></p> |

## <a name="create-vms-toorun-hello-domain-controller-and-dns-server-roles"></a>Créer le contrôleur de domaine de machines virtuelles toorun hello et les rôles de serveur DNS
Répétez hello suivant les étapes toocreate rôle de contrôleur de domaine machines virtuelles toohost hello en fonction des besoins. Vous devez déployer au moins deux contrôleurs de domaine tooprovide une tolérance de panne et la redondance virtuel. Si hello réseau virtuel Azure comprend au moins deux contrôleurs de domaine qui sont configurés de la même façon (autrement dit, ils sont à la fois des catalogues globaux, exécution serveur DNS, et aucun contient n’importe quel rôle FSMO et ainsi de suite) puis, placez des machines virtuelles hello qui s’exécutent les contrôleurs de domaine dans un groupe à haute disponibilité pour une meilleure tolérance.

toocreate hello machines virtuelles à l’aide de Windows PowerShell au lieu de hello l’interface utilisateur, consultez [toocreate d’utiliser Azure PowerShell et préconfigurer des Machines virtuelles basées sur Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. Dans le portail classique hello, cliquez sur **nouveau** > **de calcul** > **virtuels** > **à partir de la galerie**. Utilisez hello suivant valeurs toocomplete hello Assistant. Acceptez la valeur de par défaut de hello pour un paramètre, sauf si une autre valeur est suggérée ou requis.

   | Sur cette page de l'Assistant... | Spécifiez les valeurs suivantes |
   | --- | --- |
   |  **Choix d’une image** |Windows Server 2012 R2 Datacenter |
   |  **Configuration de la machine virtuelle** |<p>Nom de machine virtuelle : Tapez un nom en une seule partie (par exemple, AzureDC1).</p><p>Nouveau nom d’utilisateur : Hello nom de Type utilisateur. Cet utilisateur sera un membre du groupe Administrateurs local de hello sur hello machine virtuelle. Vous devez toosign de ce nom dans toohello machine virtuelle pour hello première fois. compte intégré de Hello nommé administrateur ne fonctionnera pas.</p><p>Nouveau mot de passe/confirmation : saisissez un mot de passe</p> |
   |  **Configuration de la machine virtuelle** |<p>Service de cloud computing : Choisissez <b>créer un service cloud</b> pourquoi la première machine virtuelle et cliquez sur ce même nom de service de cloud lorsque vous créez plusieurs machines virtuelles qui hébergeront hello rôle de contrôleur de domaine.</p><p>Nom DNS du service cloud : indiquez un nom global unique</p><p>Région/groupe d’affinités/réseau virtuel : spécifiez le nom de réseau virtuel hello (par exemple, WestUSVNet).</p><p>Compte de stockage : Choisissez <b>utiliser un compte de stockage généré automatiquement</b> pourquoi la première machine virtuelle et sélectionnez ce nom de compte de stockage lorsque vous créez plusieurs machines virtuelles qui hébergeront hello rôle de contrôleur de domaine.</p><p>Groupe à haute disponibilité : Choisissez <b>Créer un groupe à haute disponibilité</b>.</p><p>Nom de groupe à haute disponibilité : Type de nom hello groupe à haute disponibilité lorsque vous créez hello première machine virtuelle et puis sélectionnez que même nom lorsque vous créez plusieurs machines virtuelles.</p> |
   |  **Configuration de la machine virtuelle** |<p>Sélectionnez <b>hello d’installer l’Agent de machine virtuelle</b> et toutes les autres extensions que vous avez besoin.</p> |
2. Attacher un machine virtuelle qui exécutera le rôle de serveur de contrôleur de domaine hello du tooeach disque. disque supplémentaire de Hello est la base de données nécessaires toostore hello AD, les journaux et SYSVOL. Spécifiez une taille de disque hello (par exemple, 10 Go), laissez hello **préférences de Cache hôte** défini trop**aucun**. Pour connaître les étapes hello, consultez [comment tooAttach un tooa de disque de données Machine virtuelle Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Après la première connexion au toohello machine virtuelle, ouvrez **le Gestionnaire de serveur** > **File and Storage Services** toocreate un volume sur ce disque à l’aide de NTFS.
4. Réserver une adresse IP statique pour les ordinateurs virtuels qui exécuteront le rôle de contrôleur de domaine hello. tooreserve une adresse IP statique, télécharger hello Microsoft Web Platform Installer et [installer Azure PowerShell](/powershell/azure/overview) et exécutez l’applet de commande Set-AzureStaticVNetIP de hello. Par exemple :

    `Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM`

Pour plus d’informations sur la configuration d’une adresse IP, consultez [Configuration d’une adresse IP interne statique pour une machine virtuelle](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-windows-server-active-directory"></a>installation de Windows Server Active Directory
Utilisez hello même routine trop[installer les services AD DS](https://technet.microsoft.com/library/jj574166.aspx) que vous utilisez locale (autrement dit, vous pouvez utiliser hello l’interface utilisateur, un fichier de réponses ou Windows PowerShell). Vous devez tooprovide administrateur informations d’identification tooinstall une nouvelle forêt. emplacement hello toospecify hello de base de données Active Directory, les journaux et SYSVOL, modifier l’emplacement de stockage par défaut hello à partir du disque hello système d’exploitation lecteur toohello des données supplémentaires que vous avez attaché toohello machine virtuelle.

Après l’installation du contrôleur de domaine de hello, reconnectez-vous toohello machine virtuelle et connectez-vous à toohello contrôleur de domaine. N’oubliez pas d’informations d’identification de domaine toospecify.

## <a name="reset-hello-dns-server-for-hello-azure-virtual-network"></a>Réinitialiser le serveur DNS hello hello réseau virtuel Azure
1. Réinitialisez le paramètre du redirecteur DNS hello hello nouveau contrôleur de domaine/serveur DNS.
   1. Dans le Gestionnaire de serveur, cliquez sur **Outils** > **DNS**.
   2. Dans **Gestionnaire DNS**, cliquez sur le nom hello du serveur DNS de hello et cliquez sur **propriétés**.
   3. Sur hello **redirecteurs** onglet, cliquez sur l’adresse IP du redirecteur de hello hello et cliquez sur **modifier**.  Sélectionnez l’adresse IP de hello et cliquez sur **supprimer**.
   4. Cliquez sur **OK** tooclose l’éditeur hello et **Ok** nouveau tooclose hello propriétés du serveur DNS.
2. Mettre à jour du paramètre de serveur DNS hello pour le réseau virtuel de hello.
   1. Cliquez sur **réseaux virtuels** > Double-cliquez sur le réseau virtuel hello vous avez créé > **configurer** > **serveurs DNS**, tapez le nom de hello et hello DIP de l’un des Hello machines virtuelles qui s’exécute le rôle de serveur DNS/contrôleur de domaine hello et cliquez sur **enregistrer**.
   2. Sélectionnez hello machine virtuelle et cliquez sur **redémarrer** tootrigger hello VM tooconfigure DNS paramètres du résolveur avec l’adresse IP de hello du serveur DNS de la nouvelle hello.

## <a name="create-vms-for-domain-members"></a>Création de machines virtuelles pour les membres du domaine
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

## <a name="see-also"></a>Voir aussi
* [Comment tooinstall un nouvel annuaire Active Directory de la forêt sur un réseau virtuel Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* [Instructions pour le déploiement de Windows Server Active Directory sur Azure Virtual Machines](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Configuration d’un réseau VPN de site à site](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Installation d’un réplica de contrôleur de domaine Active Directory dans un réseau virtuel Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Iaas des professionnels de l’informatique Microsoft Azure : principes de base des machines virtuelles (01)](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Iaas des professionnels de l’informatique Microsoft Azure :(05) Création de réseaux virtuels pour la connectivité entre différents locaux](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Présentation du réseau virtuel.](../virtual-network/virtual-networks-overview.md)
* [Comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Guide de référence des cmdlets Azure](/powershell/azure/get-started-azureps)
* [Définition de l'adresse IP statique d'une machine virtuelle Azure](http://windowsitpro.com/windows-azure/set-azure-vm-static-ip-address)
* [Comment tooassign une adresse IP statique tooAzure machine virtuelle](http://www.bhargavs.com/index.php/2014/03/13/how-to-assign-static-ip-to-azure-vm/)
* [Installation d'une nouvelle forêt Active Directory](https://technet.microsoft.com/library/jj574166.aspx)
* [Introduction tooActive Directory Domain Services (AD DS) Virtualization (niveau 100)](https://technet.microsoft.com/library/hh831734.aspx)

<!--Image references-->
[1]: ./media/active-directory-new-forest-virtual-machine/AD_Forest.png
