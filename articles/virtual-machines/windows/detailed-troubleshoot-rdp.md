---
title: "Bureau à distance d’aaaDetailed dépannage dans Azure | Documents Microsoft"
description: "Passez en revue les étapes de dépannage détaillées pour les erreurs de bureau distant où vous ne pouvez pas les machines virtuelles tooa Windows Azure"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "Impossible de se connecter tooremote bureau, résoudre les problèmes de bureau à distance, Bureau à distance ne peut pas se connecter, les erreurs de bureau à distance, le dépannage du Bureau à distance, des problèmes de bureau à distance"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a>Les étapes de dépannage détaillées pour la connexion Bureau à distance émet tooWindows machines virtuelles dans Azure
Cet article fournit des étapes de dépannage détaillées toodiagnose et résoudre les erreurs de bureau à distance complexes pour les machines virtuelles basées sur Windows.

> [!IMPORTANT]
> tooeliminate hello erreurs Bureau à distance plus courantes, vérifiez les tooread que [article de dépannage de base de hello pour Bureau à distance](troubleshoot-rdp-connection.md) avant de continuer.

Vous pouvez rencontrer un message d’erreur qui ne ressemble pas à un des messages d’erreur spécifiques hello traité dans Bureau à distance [hello base Bureau à distance, guide de dépannage](troubleshoot-rdp-connection.md). Suivez ces toodetermine étapes pourquoi client du Bureau à distance (RDP) hello est service RDP toohello tooconnect impossible sur hello machine virtuelle Azure.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello MSDN Azure et hello forums de débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de Support technique Azure](https://azure.microsoft.com/support/options/) et cliquez sur **Get Support**. Pour plus d’informations sur l’utilisation de prise en charge d’Azure, lisez hello [FAQ du Support Microsoft Azure](https://azure.microsoft.com/support/faq/).

## <a name="components-of-a-remote-desktop-connection"></a>Composants d’une connexion Bureau à distance
Hello suivant des composants est impliqué dans une connexion RDP :

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

Avant de continuer, il peut être intéressant toomentally examiner ce qui a changé depuis hello dernière réussite Bureau à distance connexion toohello machine virtuelle. Par exemple :

* Hello d’adresse IP publique de hello machine virtuelle ou hello service cloud contenant hello VM (également appelée adresse IP virtuelle de hello [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) a changé. Hello échec RDP peut être dû à votre cache de client DNS a toujours hello *ancienne adresse IP* inscrit pour le nom DNS de hello. Vider votre cache de client DNS et réessayez de vous connecter hello machine virtuelle. Ou essayez de vous connecter directement avec la nouvelle adresse VIP de hello.
* Vous utilisez une application tierce de toomanage vos connexions Bureau à distance au lieu d’utiliser la connexion hello générée par hello portail Azure. Vérifiez que configuration de l’application hello inclut hello TCP port approprié pour hello le trafic du Bureau à distance. Vous pouvez vérifier ce port pour un ordinateur virtuel classique Bonjour [portail Azure](https://portal.azure.com), en cliquant sur les paramètres de la machine virtuelle hello > points de terminaison.

## <a name="preliminary-steps"></a>Étapes préliminaires
Avant de continuer toohello de dépannage détaillées,

* Vérifier l’état de hello de machine virtuelle de hello Bonjour portail Azure pour tout problème évident.
* Suivez hello [correction rapide des étapes pour les erreurs courantes de RDP dans le dépannage de base hello](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).

Essayez de vous reconnecter toohello machine virtuelle via le Bureau à distance après ces étapes.

## <a name="detailed-troubleshooting-steps"></a>Étapes de dépannage détaillées
client du Bureau à distance Hello n’est peut-être pas en mesure de tooreach service de bureau à distance hello sur hello Azure VM tooissues due à hello les sources suivantes :

* [ordinateur client de Bureau à distance ;](#source-1-remote-desktop-client-computer)
* [périphérique de périmètre intranet de l’entreprise ;](#source-2-organization-intranet-edge-device)
* [point de terminaison de service cloud et liste de contrôle d’accès (ACL) ;](#source-3-cloud-service-endpoint-and-acl)
* [Groupes de sécurité réseau](#source-4-network-security-groups)
* [Machine virtuelle Windows sur Azure](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a>Source 1 : Ordinateur client de Bureau à distance
Vérifiez que votre ordinateur peut créer un bureau à distance connexions tooanother local, l’ordinateur Windows.

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

Si vous ne pouvez pas rechercher hello suivant les paramètres de votre ordinateur :

* un paramètre de pare-feu local qui bloque le trafic de Bureau à distance ;
* un logiciel proxy client installé localement qui empêche les connexions Bureau à distance ;
* un logiciel de surveillance réseau installé localement qui empêche les connexions Bureau à distance ;
* d’autres types de logiciel de sécurité qui analysent le trafic ou autorisent/interdisent des types spécifiques de trafic empêchant les connexions Bureau à distance.

Dans tous ces cas, temporairement désactiver le logiciel de hello et tooconnect tooan local ordinateur via Bureau à distance. Si vous trouverez cause réelle de hello de cette façon, fonctionne avec vos connexions réseau administrateur toocorrect hello logiciel paramètres tooallow Bureau à distance.

## <a name="source-2-organization-intranet-edge-device"></a>Source 2 : Périphérique de périmètre intranet de l’entreprise
Vérifiez qu’un ordinateur connecté directement toohello Qu'internet peut rendre tooyour des connexions Bureau à distance machine virtuelle Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

Si vous n’avez pas d’un ordinateur qui est directement connecté toohello Internet, créer et tester avec un nouvel ordinateur virtuel Azure dans un service cloud ou le groupe de ressources. Pour plus d’informations, consultez [Création d’une machine virtuelle exécutant Windows dans Azure](../virtual-machines-windows-hero-tutorial.md). Vous pouvez supprimer la machine virtuelle de hello et groupe de ressources hello ou un service de cloud hello, après hello testé.

Si vous pouvez créer une connexion Bureau à distance avec un ordinateur relié directement toohello Internet, vérifiez votre périphérique de périmètre intranet organisation pour :

* Un pare-feu bloque toohello des connexions HTTPS Internet.
* un serveur proxy qui empêche les connexions Bureau à distance ;
* un logiciel de détection d’intrusion ou de surveillance réseau s’exécutant sur les appareils de votre réseau de périmètre et qui empêche les connexions Bureau à distance.

Travailler avec vos paramètres de hello de toocorrect d’administrateur réseau de votre organisation intranet bord périphérique tooallow basée sur HTTPS de bureau à distance connexions toohello Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Source 3 : Point de terminaison de service cloud et liste de contrôle d’accès
Pour les machines virtuelles créées à l’aide du modèle de déploiement classique hello, vérifiez qu’une autre machine virtuelle de Azure est Bonjour même service cloud ou réseau virtuel peut rendre tooyour des connexions Bureau à distance machine virtuelle Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> Pour les ordinateurs virtuels créés dans le Gestionnaire des ressources, ignorez trop[Source 4 : groupes de sécurité réseau](#source-4-network-security-groups).

Si vous n’avez pas d’un autre ordinateur virtuel dans hello même service cloud ou réseau virtuel, créez-en un. Suivez les étapes de hello dans [créer une machine virtuelle exécutant Windows dans Azure](../virtual-machines-windows-hero-tutorial.md). Supprimer l’ordinateur virtuel de test hello après que hello test est terminé.

Même si vous pouvez vous connecter via le Bureau à distance tooa virtual machine Bonjour de cloud service ou de réseau virtuel, vérifiez ces paramètres :

* configuration de point de terminaison Hello pour le trafic de bureau à distance sur la cible de hello VM : le port TCP privé hello du point de terminaison hello doit correspondre à quels hello service Bureau à distance de la machine virtuelle écoute le port TCP hello (valeur par défaut est 3389).
* Hello ACL pour point de terminaison du trafic hello Bureau à distance sur la cible de hello VM : des ACL toospecify autorisés ou non le trafic entrant à partir d’Internet en fonction de son adresse IP de source de hello. ACL mal configurée peut empêcher le point de terminaison toohello entrant Bureau à distance le trafic. Vérifiez votre tooensure ACL que le trafic entrant à partir de vos adresses IP publiques de votre serveur proxy ou un autre serveur edge est autorisé. Pour plus d’informations, consultez [Qu’est-ce qu’une liste de contrôle d’accès (ACL) réseau ?](../../virtual-network/virtual-networks-acl.md)

toocheck si le point de terminaison hello est source hello problème de hello, supprimez le point de terminaison actuel hello et créez-en un, en choisissant un port aléatoire dans la plage hello 49152 à 65535 pour le numéro de port externe hello. Pour plus d’informations, consultez [comment tooset des points de terminaison tooa virtuels](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="source-4-network-security-groups"></a>Source 4 : groupes de sécurité réseau
Les groupes de sécurité réseau vous permettent de contrôler plus précisément le trafic entrant et sortant autorisé. Vous pouvez créer des règles qui s’étendent aux sous-réseaux et aux services cloud d’un réseau virtuel Azure.

Utilisez [les flux IP vérifier](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm si une règle dans un groupe de sécurité réseau bloque tooor le trafic à partir d’un ordinateur virtuel. Vous pouvez également examiner les règles tooensure entrant « Autoriser » NSG règle existe et qu’il est hiérarchisé pour le port RDP (valeur par défaut 3389) de groupe de sécurité efficace. Pour plus d’informations, consultez [le trafic en utilisant les règles de sécurité efficace tootroubleshoot VM](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

## <a name="source-5-windows-based-azure-vm"></a>Source 5 : Machine virtuelle Azure Windows
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

Suivez les instructions de hello dans [cet article](reset-rdp.md). Cet article réinitialise le service de bureau à distance hello sur l’ordinateur virtuel de hello :

* Activer la règle par défaut de « Bureau à distance » le pare-feu Windows hello (port TCP 3389).
* Activer les connexions Bureau à distance en définissant too0 de valeur de Registre de HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections hello.

Essayez de hello connexion à partir de votre ordinateur. Si vous ne parvenez toujours pas tooconnect via le Bureau à distance, vérifiez hello les problèmes possibles suivants :

* Hello service Bureau à distance n’est pas exécuté sur la cible de hello machine virtuelle.
* Hello service Bureau à distance n’est pas à l’écoute sur le port TCP 3389.
* Le pare-feu Windows ou un autre pare-feu local comporte une règle sortante qui empêche le trafic du Bureau à distance.
* Détection d’intrusion ou des logiciels en cours d’exécution sur la machine virtuelle Azure de hello d’analyse réseau empêche les connexions Bureau à distance.

Pour les machines virtuelles créées à l’aide du modèle de déploiement classique de hello, vous pouvez utiliser un toohello de session Azure PowerShell à distance machine virtuelle Azure. Vous devez tout d’abord, tooinstall un certificat de service l’ordinateur virtuel de hello d’hébergement cloud. Accédez trop[configurer accès distant sécurisé PowerShell tooAzure virtuels](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) et télécharger hello **InstallWinRMCertAzureVM.ps1** ordinateur local du tooyour fichier script.

Installez ensuite Azure PowerShell si ce n’est pas déjà fait. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

Ensuite, ouvrez une invite de commandes Azure PowerShell et modifier hello actuel toohello emplacement du dossier de hello **InstallWinRMCertAzureVM.ps1** fichier de script. toorun un script Azure PowerShell, vous devez définir de stratégie d’exécution correcte de hello. Exécutez hello **Get-ExecutionPolicy** commande toodetermine votre niveau de stratégie actuel. Pour plus d’informations sur la définition du niveau approprié de hello, consultez [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).

Ensuite, renseignez le nom de votre abonnement Azure, nom du service cloud hello et votre nom d’ordinateur virtuel (en supprimant hello < et >), puis exécutez ces commandes.

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

Vous pouvez obtenir le nom de l’abonnement approprié hello de hello *SubscriptionName* propriété d’affichage hello Hello **Get-AzureSubscription** commande. Vous pouvez obtenir le nom du service de cloud pour la machine virtuelle de hello hello de hello *ServiceName* colonne dans l’affichage de hello Hello **Get-AzureVM** commande.

Vérifiez si vous disposez d’un nouveau certificat hello. Ouvrir un composant logiciel enfichable Certificats pour l’utilisateur actuel de hello et Regarder dans hello **intermédiaires\certificats de Certification racine de confiance** dossier. Vous devez voir un certificat portant le nom DNS de hello de votre service cloud dans hello délivré toocolumn (exemple : cloudservice4testing.cloudapp.net).

Lancez ensuite une session Azure PowerShell distante à l’aide de ces commandes.

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

Après avoir entré les informations d’identification administrateur valides, vous devez voir quelque chose de similaire toohello après l’invite de commandes Azure PowerShell :

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

Hello première partie de ce message est le nom de votre service cloud qui contient les cibles de hello machine virtuelle, ce qui peut être différent de « cloudservice4testing.cloudapp.net ». Vous pouvez maintenant émettre des commandes Azure PowerShell pour ce cloud des problèmes hello service tooinvestigate mentionnés et corriger la configuration de hello.

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a>toomanually corriger hello Services Bureau à distance à l’écoute du port TCP
À l’invite de session Azure PowerShell à distance hello, exécutez cette commande.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Hello propriété PortNumber indique le numéro de port actuel hello. Si nécessaire, modifiez hello Bureau à distance port numéro tooits différé par défaut (3389) à l’aide de cette commande.

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

Vérifiez que le port de hello a été too3389 modifiées à l’aide de cette commande.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Quittez la session Azure PowerShell à distance de hello à l’aide de cette commande.

```powershell
Exit-PSSession
```

Vérifiez que ce point de terminaison Bureau à distance pour hello Azure VM hello utilise également le port TCP 3398 comme son port interne. Redémarrez hello Azure VM et essayez à nouveau les connexion Bureau à distance hello.

## <a name="additional-resources"></a>Ressources supplémentaires
[Comment tooreset un mot de passe ou hello Bureau à distance du service pour les machines virtuelles Windows](reset-rdp.md)

[Comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview)

[Résoudre les problèmes de SSH (Secure Shell) connexions tooa basés sur Linux machine virtuelle Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Résoudre les problèmes d’accès tooan application est en cours d’exécution sur une machine virtuelle Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

