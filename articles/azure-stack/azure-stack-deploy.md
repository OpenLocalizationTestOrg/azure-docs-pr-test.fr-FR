---
title: "Prérequis pour le déploiement du Kit de développement Azure Stack | Microsoft Docs"
description: "Examinez la configuration du matériel et de l’environnement requise pour le Kit de développement Azure Stack (opérateur cloud)."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 32a21d9b-ee42-417d-8e54-98a7f90f7311
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/11/2017
ms.author: erikje
ms.openlocfilehash: e4e2293149b64056d1ec9d1900119e9f4f511d06
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-stack-deployment-prerequisites"></a>Prérequis pour le déploiement Azure Stack
Avant de déployer le [Kit de développement](azure-stack-poc.md) Azure Stack, assurez-vous que votre ordinateur présente la configuration suivante :


## <a name="hardware"></a>Matériel
| Composant | Minimale | Recommandé |
| --- | --- | --- |
| Lecteurs de disque : système d’exploitation |1 disque de système d’exploitation avec un minimum de 200 Go disponibles pour la partition système (SSD ou HDD) |1 disque de système d’exploitation avec un minimum de 200 Go disponibles pour la partition système (SSD ou HDD) |
| Lecteurs de disque : données générales du Kit de développement* |4 disques. Chaque disque doit avoir une capacité d’au moins 140 Go (SSD ou HDD). Tous les disques disponibles seront utilisés. |4 disques. Chaque disque doit avoir une capacité d’au moins 250 Go (SSD ou HDD). Tous les disques disponibles seront utilisés. |
| Calcul : UC |Double socket : 12 cœurs physiques (total) |Double socket : 16 cœurs physiques (total) |
| Calcul : mémoire |96 Go de RAM |128 Go de RAM (minimum nécessaire pour la prise en charge des fournisseurs de ressources PaaS)|
| Calcul : BIOS |Compatible Hyper-V (avec prise en charge de SLAT) |Compatible Hyper-V (avec prise en charge de SLAT) |
| Réseau : Carte réseau |Certification Windows Server 2012 R2 nécessaire pour la carte réseau ; pas de fonctionnalités spécialisées requises |Certification Windows Server 2012 R2 nécessaire pour la carte réseau ; pas de fonctionnalités spécialisées requises |
| Logo de certification du matériel |[Certifié pour Windows Server 2012 R2](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |[Certifié pour Windows Server 2012 R2](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |

\*Vous aurez besoin d’une plus grande capacité que cette capacité recommandée si vous prévoyez d’ajouter de nombreux [éléments de la Place de marché](azure-stack-download-azure-marketplace-item.md) Azure.

**Configuration des lecteurs de disque de données :** tous les lecteurs de données doivent être de même type (soit SAS, soit SATA) et avoir la même capacité. Si vous utilisez des lecteurs de disque SAS, vous devez les joindre par le biais d’un chemin d’accès unique (aucune prise en charge de MPIO ou des chemins d’accès multiples n’est fournie).

**Options de configuration HBA**

* (Recommandé) HBA simple
* HBA RAID : la carte doit être configurée en mode Pass Through
* HBA RAID : les disques doivent être configurés en tant que disque unique, RAID-0

**Combinaisons bus/type de support prises en charge**

* DISQUE DUR SATA
* DISQUE DUR SAS
* DISQUE DUR RAID
* SSD RAID (si le type de support n’est pas spécifié ou connu\*)
* DISQUE SSD SATA + DISQUE DUR SATA
* DISQUE SSD SAS + DISQUE DUR SAS

\*Les contrôleurs RAID sans fonctionnalité Pass Through ne peuvent pas reconnaître le type de support. Ces contrôleurs marqueront à la fois les disques durs et les disques SSD comme Non spécifiés. Dans ce cas, le disque SSD servira de stockage persistant et non de périphériques de mise en cache. Vous pouvez alors déployer le Kit de développement sur ces disques SSD.

**Exemples d’HBA**: LSI 9207-8i, LSI-9300-8i ou LSI-9265-8i en mode pass-through

Des exemples de configurations OEM sont disponibles.

## <a name="operating-system"></a>Système d’exploitation
|  | **Configuration requise** |
| --- | --- |
| **Version du SE** |Windows Server 2012 R2 ou version ultérieure. La version du système d’exploitation n’est pas critique avant le démarrage du déploiement, car vous allez démarrer l’ordinateur hôte sur le disque VHD qui est fourni dans l’installation Azure Stack. Le système d’exploitation et tous les correctifs nécessaires sont déjà intégrés dans l’image. N’utilisez pas de clés pour activer les instances Windows Server utilisées dans le Kit de développement. |

## <a name="deployment-requirements-check-tool"></a>Outil de vérification des prérequis pour le déploiement
Après avoir installé le système d’exploitation, vous pouvez utiliser le [vérificateur de déploiement Azure Stack](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) pour vérifier que votre matériel a la configuration requise.

## <a name="account-requirements"></a>Exigences pour les comptes
En général, vous déployez le Kit de développement avec une connexion Internet pour pouvoir vous connecter à Microsoft Azure. Dans ce cas, configurez un compte Azure Active Directory (Azure AD) pour déployer le Kit de développement.

Si votre environnement n’est pas connecté à Internet, ou si vous ne souhaitez pas utiliser Azure AD, vous pouvez déployer Azure Stack à l’aide des services de fédération Active Directory (AD FS). Le Kit de développement inclut ses propres instances AD FS et AD DS (Active Directory Domain Services). Si vous choisissez cette option de déploiement, vous n’avez pas besoin de configurer des comptes au préalable.

>[!NOTE]
Si vous effectuez le déploiement avec l’option AD FS, vous devez redéployer Azure Stack pour utiliser Azure AD à la place.

### <a name="azure-active-directory-accounts"></a>Comptes Azure Active Directory
Pour déployer Azure Stack en utilisant un compte Azure AD, vous devez préparer ce compte avant d’exécuter le script de déploiement PowerShell. Ce compte devient administrateur général pour le locataire Azure AD. Il est utilisé pour provisionner et déléguer des applications et des principaux de service pour tous les services Azure Stack qui interagissent avec Azure Active Directory et l’API Graph. Il est également propriétaire de l’abonnement du fournisseur par défaut (vous pouvez changer ce paramètre ultérieurement). Vous pouvez utiliser ce compte pour vous connecter au portail de l’administrateur de votre système Azure Stack.

1. Créez un compte Azure AD qui est administrateur d’au moins un annuaire Azure AD. Si vous en avez déjà un, vous pouvez l’utiliser. Sinon, créez gratuitement un compte Azure à partir de la page [http://azure.microsoft.com/fr-fr/pricing/free-trial/](http://azure.microsoft.com/pricing/free-trial/) (en Chine, accédez à la page <http://go.microsoft.com/fwlink/?LinkID=717821>). Si vous prévoyez [d’inscrire Azure Stack auprès d’Azure](azure-stack-register.md) ultérieurement, vous devez également avoir un abonnement avec ce nouveau compte.
   
    Enregistrez ces informations d’identification, car vous en aurez besoin à l’étape 6 de la procédure [Déployer le Kit de développement](azure-stack-run-powershell-script.md#deploy-the-development-kit). Vous pouvez utiliser ce compte *d’administrateur de services fédérés* pour configurer et gérer les clouds de ressources, les comptes d’utilisateur, les plans de locataire, les quotas et les tarifs. Dans le portail, il peut créer des clouds de sites web, des clouds privés de machine virtuelle, des plans et gérer les abonnements des utilisateurs.
2. [Créez](azure-stack-add-new-user-aad.md) au moins un compte avec lequel vous pouvez vous connecter au Kit de développement en tant que locataire.
   
   | **Compte Active Directory Azure** | **Pris en charge ?** |
   | --- | --- |
   | Compte professionnel ou scolaire avec un abonnement Azure public valide |Oui |
   | Compte Microsoft avec abonnement Azure public valide |Oui |
   | Compte professionnel ou scolaire avec un abonnement Azure en Chine valide |Oui |
   | Compte professionnel ou scolaire avec un abonnement Azure pour le gouvernement américain valide |Oui |

## <a name="network"></a>Réseau
### <a name="switch"></a>Switch
Un port disponible sur un commutateur de la machine du Kit de développement.  

La machine du Kit de développement prend en charge la connexion à un port d’accès de commutateur ou de jonction. Aucune fonctionnalité spéciale n’est requise pour le commutateur. Si vous utilisez un port de jonction ou si vous devez configurer un ID de réseau local virtuel, vous devez fournir cet ID de réseau local virtuel comme paramètre de déploiement. Des exemples sont fournis dans la [liste des paramètres de déploiement](azure-stack-run-powershell-script.md).

### <a name="subnet"></a>Sous-réseau
Ne connectez pas la machine du Kit de développement aux sous-réseaux suivants :

* 192.168.200.0/24
* 192.168.100.0/27
* 192.168.101.0/26
* 192.168.102.0/24
* 192.168.103.0/25
* 192.168.104.0/25

Ces sous-réseaux sont réservés aux réseaux internes au sein de l’environnement du Kit de développement.

### <a name="ipv4ipv6"></a>IPv4/IPv6
Seul le protocole IPv4 est pris en charge. Il est impossible de créer des réseaux IPv6.

### <a name="dhcp"></a>DHCP
Assurez-vous que le serveur DHCP est disponible sur le réseau auquel la carte réseau se connecte. Si DHCP n’est pas disponible, vous devez préparer un réseau IPv4 statique supplémentaire en plus de celui que l’hôte utilise. Vous devez fournir cette adresse IP et la passerelle comme paramètre de déploiement. Des exemples sont fournis dans la [liste des paramètres de déploiement](azure-stack-run-powershell-script.md).

### <a name="internet-access"></a>Accès à Internet
Azure Stack nécessite un accès à Internet, directement ou via un proxy transparent. Azure Stack ne prend pas en charge la configuration d’un proxy web pour l’accès à Internet. L’adresse IP de l’hôte et la nouvelle adresse IP assignée à MAS-BGPNAT01 (par DHCP ou IP statique) doivent pouvoir accéder à Internet. Les ports 80 et 443 sont utilisés sous les domaines graph.windows.net et login.microsoftonline.com.

## <a name="telemetry"></a>Télémétrie

La télémétrie nous aide à concevoir les versions futures d’Azure Stack. Elle nous permet de répondre rapidement aux commentaires des utilisateurs, de fournir de nouvelles fonctionnalités et d’améliorer la qualité du produit. Microsoft Azure Stack inclut Windows Server 2016 et SQL Server 2014. Ces deux produits sont fournis avec leurs paramètres par défaut et sont régis par la déclaration de confidentialité de Microsoft Enterprise. Azure Stack contient également des logiciels open source qui n’ont pas été modifiés pour envoyer des données de télémétrie à Microsoft. Voici quelques exemples de données de télémétrie collectées pour Azure Stack :

- Informations sur l’inscription d’un déploiement
- Date et heure de l’ouverture et la fermeture d’une alerte
- Nombre de ressources réseau

Pour prendre en charge le flux des données de télémétrie, le port 443 (HTTPS) doit être ouvert sur votre réseau. Le point de terminaison client est https://vortex-win.data.microsoft.com.

Si vous ne souhaitez pas fournir de données de télémétrie pour Azure Stack, vous pouvez désactiver cette fonctionnalité sur l’hôte du Kit de développement et sur les machines virtuelles de l’infrastructure, comme expliqué ci-dessous.

### <a name="turn-off-telemetry-on-the-development-kit-host-optional"></a>Désactiver la télémétrie sur l’hôte du Kit de développement (facultatif)

>[!NOTE]
Si vous souhaitez désactiver la télémétrie sur l’hôte du Kit de développement, vous devez le faire avant d’exécuter le script de déploiement.

Avant [d’exécuter le script asdk-installer.ps1]() pour déployer l’hôte du Kit de développement, démarrez la machine sur CloudBuilder.vhdx et exécutez le script suivant dans une fenêtre PowerShell avec des privilèges élevés :
```powershell
### Get current AllowTelmetry value on DVM Host
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
### Set & Get updated AllowTelemetry value for ASDK-Host 
Set-ItemProperty-Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name "AllowTelemetry" -Value '0'  
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
```

Définissez le paramètre **AllowTelemetry** à la valeur 0 pour désactiver la télémétrie relative au déploiement Windows et Azure Stack. Seuls les événements de sécurité critiques du système d’exploitation seront envoyés. Le paramètre contrôle la télémétrie Windows sur tous les hôtes et toutes les machines virtuelles de l’infrastructure. Il est réappliqué aux nouveaux nœuds et machines virtuelles après une augmentation de la taille des instances.


### <a name="turn-off-telemetry-on-the-infrastructure-virtual-machines-optional"></a>Désactiver la télémétrie sur les machines virtuelles de l’infrastructure (facultatif)

Quand vous avez terminé le déploiement, exécutez le script suivant dans une fenêtre PowerShell avec des privilèges élevés (en tant qu’utilisateur AzureStack\AzureStackAdmin) sur l’hôte du Kit de développement :

```powershell
$AzSVMs= get-vm |  where {$_.Name -like "AzS-*"}
### Show current AllowTelemetry value for all AzS-VMs
invoke-command -computername $AzSVMs.name {(Get-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name AllowTelemetry).AllowTelemetry}
### Set & Get updated AllowTelemetry value for all AzS-VMs
invoke-command -computername $AzSVMs.name {Set-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name "AllowTelemetry" -Value '0'}
invoke-command -computername $AzSVMs.name {(Get-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name AllowTelemetry).AllowTelemetry}
```

Pour configurer la télémétrie SQL Server, consultez [Guide pratique pour configurer SQL Server 2016](https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft).

### <a name="usage-reporting"></a>Rapports d’utilisation

Lors de l’inscription, Azure Stack est également configuré pour transmettre certaines informations sur l’utilisation à Azure. Les rapports d’utilisation sont contrôlés indépendamment de la télémétrie. Vous pouvez désactiver les rapports d’utilisation au moment de [l’inscription](azure-stack-register.md) en utilisant le script sur Github. Définissez simplement le paramètre **$reportUsage** sur **$false**.

Les données d’utilisation sont mises en forme comme cela est décrit dans [Envoyer des données sur l’utilisation d’Azure Stack à Azure](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-usage-reporting). L’utilisation du Kit de développement Azure Stack n’est pas soumise à facturation. Cette fonctionnalité est fournie dans le Kit de développement pour vous permettre de tester le fonctionnement des rapports d’utilisation. 


## <a name="next-steps"></a>Étapes suivantes
[Télécharger le package de déploiement du Kit de développement Azure Stack](https://azure.microsoft.com/overview/azure-stack/try/?v=try)

[Déployer le Kit de développement Azure Stack](azure-stack-run-powershell-script.md)
