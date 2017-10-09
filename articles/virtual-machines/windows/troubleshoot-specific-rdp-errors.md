---
title: "messages d’erreur aaaSpecific RDP pour les machines virtuelles Azure | Documents Microsoft"
description: "Comprendre les messages d’erreur spécifiques que vous pouvez recevoir lors de la tentative d’utilisent machine virtuelle de bureau à distance connexion tooa Windows dans Azure"
keywords: "Erreur du Bureau à distance, une erreur de connexion Bureau à distance, ne peut pas se connecter tooVM, dépannage de bureau à distance"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a>Résolution des problèmes spécifique tooa de messages d’erreur RDP ordinateur virtuel Windows Azure
Vous pouvez recevoir un message d’erreur spécifique lors de l’utilisation de la machine virtuelle (VM) de bureau à distance connexion tooa Windows dans Azure. Cet article explique certaines des hello rencontrés avec tooresolve d’étapes de résolution des problèmes des messages d’erreur courants les. Si vous rencontrez des problèmes de connexion tooyour machine virtuelle à l’aide de RDP mais ne pas rencontrer un message d’erreur spécifiques, consultez hello [guide de dépannage pour le Bureau à distance](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Pour plus d’informations sur les messages d’erreur spécifiques, voir hello :

* [session à distance de Hello a été déconnectée, car il n’y a aucun tooprovide disponible aux serveurs de licences bureau à distance une licence](#rdplicense).
* [Bureau à distance ne peut pas trouver hello « nom de l’ordinateur »](#rdpname).
* [Une erreur d’authentification s’est produite. Hello autorité de sécurité locale ne peut pas être contactée](#rdpauth).
* [Message d'erreur de sécurité Windows : Vos informations d'identification n'ont pas fonctionné](#wincred).
* [Cet ordinateur ne peut pas se connecter l’ordinateur distant de toohello](#rdpconnect).

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a>session à distance de Hello a été déconnectée, car il n’y a aucune tooprovide disponible du serveur de licences bureau à distance une licence.
Cause : hello 120 jours licence période de grâce pour le rôle de serveur Bureau à distance hello a expiré et vous avez besoin de licences de tooinstall.

Pour résoudre ce problème, enregistrez une copie locale du fichier RDP de hello à partir du portail de hello et à un tooconnect d’invite de commandes PowerShell, exécutez cette commande. Cette étape ne désactive la licence que pour cette connexion :

        mstsc <File name>.RDP /admin

Si vous ne devez pas réellement plus de deux toohello de connexions Bureau à distance simultanées machine virtuelle, vous pouvez utiliser le rôle de serveur Bureau à distance hello tooremove du Gestionnaire de serveur.

Pour plus d’informations, voir blog de hello [Azure VM échoue avec « Aucune serveurs Bureau à distance licence disponibles »](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a>Bureau à distance ne peut pas trouver l’ordinateur hello « name ».
Cause : client de bureau à distance hello sur votre ordinateur ne peut pas résoudre le nom hello d’ordinateur hello dans les paramètres du fichier RDP de hello hello.

Solutions possibles :

* Si vous êtes sur l’intranet d’une organisation, assurez-vous que l’ordinateur serveur proxy d’accès toohello et peut envoyer tooit du trafic HTTPS.
* Si vous utilisez un fichier RDP stocké localement, essayez d’utiliser hello une qui est généré par le portail de hello. Cette étape permet de s’assurer que vous disposez de nom DNS correct de hello pour machine virtuelle de hello, ou service de cloud computing hello et le port du point de terminaison hello Hello machine virtuelle. Voici un exemple de fichier RDP généré par le portail de hello :
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

partie Hello de ce fichier RDP a :

* Hello nom de domaine complet du service de cloud hello contenant hello machine virtuelle (« tailspin-azdatatier.cloudapp.net » dans cet exemple).
* Hello externe le port TCP du point de terminaison hello pour le trafic de bureau à distance (55919).

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a>Une erreur d’authentification s’est produite. Hello autorité de sécurité locale ne peut pas être contacté.
Cause : cible de hello machine virtuelle ne peut pas localiser d’autorité de sécurité hello dans la partie du nom d’utilisateur hello de vos informations d’identification.

Lorsque votre nom d’utilisateur est sous forme de hello *système de sécurité*\\*nom d’utilisateur* (exemple : CORP\User1), hello *système de sécurité* partie est soit hello machine virtuelle nom de l’ordinateur (pour l’autorité de sécurité locale hello) ou un nom de domaine Active Directory.

Solutions possibles :

* Si le compte de hello est toohello local machine virtuelle, assurez-vous que ce nom de machine virtuelle hello est correctement orthographié.
* Si le compte de hello se trouve sur un domaine Active Directory, vérifier l’orthographe de hello hello du nom de domaine.
* S’il s’agit d’un compte de domaine Active Directory et le nom de domaine hello est correctement orthographié, vérifiez qu’un contrôleur de domaine est disponible dans ce domaine. Dans les réseaux virtuels Azure qui contiennent des contrôleurs de domaine, il est courant qu’un contrôleur de domaine soit indisponible, car il n’a pas démarré. Pour contourner ce problème, vous pouvez utiliser un compte d’administrateur local, plutôt qu’un compte de domaine.

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a>Message d’erreur de sécurité Windows : Vos informations d’identification n’ont pas fonctionné.
Cause : la cible de hello machine virtuelle ne peut pas valider votre nom de compte et un mot de passe.

Un ordinateur basé sur Windows peut valider des informations d’identification de hello d’un compte local ou un compte de domaine.

* Pour les comptes locaux, utilisez hello *Nom_Ordinateur*\\*nom d’utilisateur* syntaxe (exemple : SQL1\Admin4798).
* Pour les comptes de domaine, utilisez hello *DomainName*\\*nom d’utilisateur* syntaxe (exemple : CONTOSO\peterodman).

Si vous avez promu votre contrôleur de domaine tooa machine virtuelle dans une nouvelle forêt Active Directory, le compte d’administrateur local de hello vous connecter est converti tooan équivalent compte avec hello même mot de passe dans hello nouvelle forêt et le domaine. compte local de Hello est supprimé.

Par exemple, si vous connectez avec un compte local de hello DC1\DCAdmin et ensuite promu hello virtual machine en tant que contrôleur de domaine dans une nouvelle forêt pour le domaine corp.contoso.com hello, hello DC1\DCAdmin compte local sera supprimé et un compte de domaine (CORP\DCAdmin ) est créé avec hello même mot de passe.

Assurez-vous que ce nom de compte hello est un nom que hello virtual machine peut vérifier comme un compte valide, et ce mot de passe hello est correcte.

Si vous avez besoin d’un mot de passe hello toochange de compte d’administrateur local hello, consultez [comment tooreset un mot de passe ou hello Bureau à distance du service pour les machines virtuelles Windows](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a>Cet ordinateur ne peut pas se connecter à toohello les ordinateur distant.
Cause : le compte hello qui a utilisé tooconnect n’a pas de droits de connexion Bureau à distance.

Chaque ordinateur Windows possède un groupe local utilisateurs du Bureau à distance, qui contient les comptes de hello et les groupes qui peuvent vous connectez à distance. Les membres du groupe Administrateurs local de hello ont également accès, même si ces comptes ne figurent pas dans le groupe local des utilisateurs du Bureau à distance hello. Pour les ordinateurs joints au domaine, groupe d’administrateurs locaux hello contient également les administrateurs de domaine hello pour le domaine de hello.

Assurez-vous que hello votre compte tooconnect avec dispose des droits de connexion Bureau à distance. Pour résoudre ce problème, utilisez un domaine ou un tooconnect de compte d’administrateur local sur le Bureau à distance. tooadd hello du groupe local des utilisateurs du Bureau à distance toohello compte souhaité, utilisez le composant logiciel enfichable Microsoft Management Console hello (**système Outils > utilisateurs et groupes locaux > groupes > Remote Desktop Users**).

## <a name="next-steps"></a>Étapes suivantes
Si aucune de ces erreurs s’est produite et que vous avez un problème inconnu avec la connexion à l’aide du protocole RDP, consultez hello [guide de dépannage pour le Bureau à distance](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Pour le dépannage des étapes de l’accès aux applications en cours d’exécution sur une machine virtuelle, consultez [application tooan de résoudre les accès en cours d’exécution sur une machine virtuelle Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Si vous rencontrez des problèmes à l’aide de SSH (Secure Shell) tooconnect tooa Linux VM dans Azure, consultez [tooa dépanner SSH connexions VM Linux dans Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

