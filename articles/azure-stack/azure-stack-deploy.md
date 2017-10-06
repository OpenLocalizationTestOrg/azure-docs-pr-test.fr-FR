---
title: "conditions préalables au déploiement d’aaaAzure Kit de développement de pile | Documents Microsoft"
description: "Environnement de hello de vue et la configuration matérielle requise pour le Kit de développement Azure pile (opérateur de cloud)."
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
ms.openlocfilehash: 126c851651354b6f3d61c4627ab0c1de9da12ba9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-deployment-prerequisites"></a>Prérequis pour le déploiement Azure Stack
Avant de déployer Azure pile [Kit de développement](azure-stack-poc.md), assurez-vous que votre ordinateur répond aux hello suivant les exigences :


## <a name="hardware"></a>Matériel
| Composant | Minimale | Recommandé |
| --- | --- | --- |
| Lecteurs de disque : système d’exploitation |1 disque de système d’exploitation avec un minimum de 200 Go disponibles pour la partition système (SSD ou HDD) |1 disque de système d’exploitation avec un minimum de 200 Go disponibles pour la partition système (SSD ou HDD) |
| Lecteurs de disque : données générales du Kit de développement* |4 disques. Chaque disque doit avoir une capacité d’au moins 140 Go (SSD ou HDD). Tous les disques disponibles seront utilisés. |4 disques. Chaque disque doit avoir une capacité d’au moins 250 Go (SSD ou HDD). Tous les disques disponibles seront utilisés. |
| Calcul : UC |Double socket : 12 cœurs physiques (total) |Double socket : 16 cœurs physiques (total) |
| Calcul : mémoire |96 Go de RAM |128 Go de RAM (il s’agit de fournisseurs de ressources hello toosupport minimale PaaS).|
| Calcul : BIOS |Compatible Hyper-V (avec prise en charge de SLAT) |Compatible Hyper-V (avec prise en charge de SLAT) |
| Réseau : Carte réseau |Certification Windows Server 2012 R2 nécessaire pour la carte réseau ; pas de fonctionnalités spécialisées requises |Certification Windows Server 2012 R2 nécessaire pour la carte réseau ; pas de fonctionnalités spécialisées requises |
| Logo de certification du matériel |[Certifié pour Windows Server 2012 R2](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |[Certifié pour Windows Server 2012 R2](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |

\*Vous aurez besoin plus que cette opération capacité recommandée si vous prévoyez d’ajouter de nombreux hello [d’éléments du marketplace](azure-stack-download-azure-marketplace-item.md) à partir d’Azure.

**Configuration du lecteur de disque de données :** hello de données de tous les disques doivent être de même type (uniquement des disques SAS ou SATA toutes les) et la capacité. Si les disques SAS sont utilisés, les lecteurs de disque hello doit être connectés via un chemin d’accès unique (aucune fonctionnalité MPIO, prise en charge multi-path n’est fourni).

**Options de configuration HBA**

* (Recommandé) HBA simple
* HBA RAID : la carte doit être configurée en mode Pass Through
* HBA RAID : les disques doivent être configurés en tant que disque unique, RAID-0

**Combinaisons bus/type de support prises en charge**

* DISQUE DUR SATA
* DISQUE DUR SAS
* DISQUE DUR RAID
* RAID SSD (si le type de média hello est non spécifié/inconnu\*)
* DISQUE SSD SATA + DISQUE DUR SATA
* DISQUE SSD SAS + DISQUE DUR SAS

\*Les contrôleurs RAID sans fonction pass-through ne peut pas reconnaître le type de média hello. Ces contrôleurs marqueront à la fois les disques durs et les disques SSD comme Non spécifiés. Dans ce cas, hello SSD servira au lieu de la mise en cache des périphériques de stockage permanent. Par conséquent, vous pouvez déployer le kit de développement hello sur ces disques SSD.

**Exemples d’HBA**: LSI 9207-8i, LSI-9300-8i ou LSI-9265-8i en mode pass-through

Des exemples de configurations OEM sont disponibles.

## <a name="operating-system"></a>Système d’exploitation
|  | **Configuration requise** |
| --- | --- |
| **Version du SE** |Windows Server 2012 R2 ou version ultérieure. version du système d’exploitation Hello n’est pas critique avant le démarrage de déploiement de hello, car vous allez démarrer l’ordinateur hôte hello en hello disque dur virtuel qui est inclus dans l’installation de Azure pile hello. Hello du système d’exploitation et tous les correctifs requis sont déjà intégrés dans l’image de hello. N’utilisez pas les tooactivate clés utilisés par toutes les instances de Windows Server dans le kit de développement hello. |

## <a name="deployment-requirements-check-tool"></a>Outil de vérification des prérequis pour le déploiement
Après avoir installé le système d’exploitation de hello, vous pouvez utiliser hello [vérificateur de déploiement pour Azure pile](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) tooconfirm que votre matériel répond à toutes les exigences de hello.

## <a name="account-requirements"></a>Exigences pour les comptes
En général, vous déployez le kit de développement hello avec une connexion internet, où vous pouvez vous connecter tooMicrosoft Azure. Dans ce cas, vous devez configurer un kit de développement Azure Active Directory (Azure AD) compte toodeploy hello.

Si votre environnement n’est pas connecté toohello internet, ou si vous ne souhaitez pas toouse Azure AD, vous pouvez déployer Azure pile à l’aide des Services de fédération Active Directory (AD FS). kit de développement Hello inclut ses propres instances AD FS et les Services de domaine Active Directory. Si vous déployez à l’aide de cette option, vous n’avez tooset des comptes à l’avance.

>[!NOTE]
Si vous déployez à l’aide d’option de hello AD FS, vous devez redéployer tooAzure tooswitch de pile d’Azure AD.

### <a name="azure-active-directory-accounts"></a>Comptes Azure Active Directory
toodeploy pile d’Azure à l’aide d’un compte Azure AD, vous devez préparer un compte Azure AD avant d’exécuter le script PowerShell de déploiement hello. Ce compte devient hello administrateur Global pour le locataire Azure AD de hello. Il a utilisé des applications tooprovision et le délégué et les principaux de service pour tous les services Azure pile qui interagissent avec Azure Active Directory et l’API Graph. Il est également utilisé en tant que propriétaire hello d’abonnement de fournisseur par défaut hello (qui vous pouvez modifier ultérieurement). Vous pouvez consigner dans le portail de l’administrateur du système tooyour Azure pile à l’aide de ce compte.

1. Créer un compte Azure AD qui est administrateur d’annuaire hello pour au moins un Azure AD. Si vous en avez déjà un, vous pouvez l’utiliser. Sinon, créez gratuitement un compte Azure à partir de la page [http://azure.microsoft.com/fr-fr/pricing/free-trial/](http://azure.microsoft.com/pricing/free-trial/) (en Chine, accédez à la page <http://go.microsoft.com/fwlink/?LinkID=717821>). Si vous envisagez de toolater [inscrire la pile d’Azure avec Azure](azure-stack-register.md), vous devez également avoir un abonnement de ce nouveau compte.
   
    Enregistrer ces informations d’identification pour une utilisation à l’étape 6 de [déployer le kit de développement hello](azure-stack-run-powershell-script.md#deploy-the-development-kit). Vous pouvez utiliser ce compte *d’administrateur de services fédérés* pour configurer et gérer les clouds de ressources, les comptes d’utilisateur, les plans de locataire, les quotas et les tarifs. Dans le portail hello, celui-ci peut créent des clouds de site Web, les clouds privés de machines virtuelles, créer des plans et gérer les abonnements des utilisateurs.
2. [Créer](azure-stack-add-new-user-aad.md) au moins un compte afin que vous pouvez vous connecter dans le kit de développement toohello en tant que client.
   
   | **Compte Active Directory Azure** | **Pris en charge ?** |
   | --- | --- |
   | Compte professionnel ou scolaire avec un abonnement Azure public valide |Oui |
   | Compte Microsoft avec abonnement Azure public valide |Oui |
   | Compte professionnel ou scolaire avec un abonnement Azure en Chine valide |Oui |
   | Compte professionnel ou scolaire avec un abonnement Azure pour le gouvernement américain valide |Oui |

## <a name="network"></a>Réseau
### <a name="switch"></a>Switch
Un port disponible sur un commutateur d’ordinateur de kit de développement hello.  

ordinateur de kit de développement Hello prend en charge le port de l’accès de connexion tooa commutateur ou trunk. Aucune des fonctionnalités spécialisées ne sont requis sur le commutateur de hello. Si vous utilisez un port trunk ou si vous avez besoin d’un ID de VLAN de tooconfigure, vous avez tooprovide hello ID VLAN comme un paramètre de déploiement. Vous pouvez voir des exemples dans hello [la liste des paramètres de déploiement](azure-stack-run-powershell-script.md).

### <a name="subnet"></a>Sous-réseau
Ne vous connectez pas hello development kit machine toohello suivant sous-réseaux :

* 192.168.200.0/24
* 192.168.100.0/27
* 192.168.101.0/26
* 192.168.102.0/24
* 192.168.103.0/25
* 192.168.104.0/25

Ces sous-réseaux est réservées aux réseaux internes de hello au sein de l’environnement de kit de développement hello.

### <a name="ipv4ipv6"></a>IPv4/IPv6
Seul le protocole IPv4 est pris en charge. Il est impossible de créer des réseaux IPv6.

### <a name="dhcp"></a>DHCP
Assurez-vous que vous disposez d’un serveur DHCP disponible sur le réseau de hello que hello à que carte réseau se connecte. Si DHCP n’est pas disponible, vous devez préparer un réseau IPv4 statique supplémentaire outre hello celui utilisé par l’hôte. Vous devez fournir cette adresse IP et la passerelle comme paramètre de déploiement. Vous pouvez voir des exemples dans hello [la liste des paramètres de déploiement](azure-stack-run-powershell-script.md).

### <a name="internet-access"></a>Accès à Internet
Pile Azure nécessite toohello d’accès Internet, directement ou via un proxy transparent. Pile Azure ne prend pas en charge la configuration hello d’un tooenable de proxy web accès à Internet. IP de l’hôte hello et hello nouvelle adresse IP affectée toohello que MAS-BGPNAT01 (par DHCP ou des adresses IP statiques) doit être en mesure de tooaccess Internet. Les ports 80 et 443 sont utilisés sous des domaines graph.windows.net et login.microsoftonline.com hello.

## <a name="telemetry"></a>Télémétrie

La télémétrie nous aide à concevoir les versions futures d’Azure Stack. Il nous permet de répondre rapidement toofeedback, fournit de nouvelles fonctionnalités et améliorer la qualité. Microsoft Azure Stack inclut Windows Server 2016 et SQL Server 2014. Aucun de ces produits sont modifiés à partir des paramètres par défaut et les deux sont décrites par hello déclaration de confidentialité de Microsoft Enterprise. Pile Azure contient également des logiciels open source qui n’a pas été modifié toosend télémétrie tooMicrosoft. Voici quelques exemples de données de télémétrie collectées pour Azure Stack :

- Informations sur l’inscription d’un déploiement
- Date et heure de l’ouverture et la fermeture d’une alerte
- nombre de Hello des ressources réseau

flux de données de télémétrie toosupport, le port 443 (HTTPS) doit être ouvert dans votre réseau. point de terminaison client Hello est https://vortex-win.data.microsoft.com.

Si vous ne souhaitez pas tooprovide télémétrie pour la pile de Azure, vous pouvez le désactiver sur l’hôte de kit de développement de hello et hello infrastructure virtuels comme expliqué ci-dessous.

### <a name="turn-off-telemetry-on-hello-development-kit-host-optional"></a>Désactiver la télémétrie sur l’hôte de kit de développement hello (facultatif)

>[!NOTE]
Si vous souhaitez tooturn désactiver la télémétrie pour l’hôte de kit de développement hello, vous devez le faire avant d’exécuter le script de déploiement hello.

Avant de [exécutant hello asdk-installer.ps1 script]() hôte de kit de développement de hello toodeploy, démarrage en hello CloudBuilder.vhdx et suivantes de hello exécution du script dans une fenêtre PowerShell avec élévation de privilèges :
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

Paramètre **AllowTelemetry** too0 désactive la télémétrie pour le déploiement de Windows et de pile de Azure. Seuls les événements critiques de sécurité à partir du système d’exploitation de hello sont envoyés. Hello contrôle les données de télémétrie Windows sur tous les hôtes et les machines virtuelles d’infrastructure et est réappliqué les toonew nœuds/machines virtuelles lorsque des opérations de montée en puissance parallèle se produisent.


### <a name="turn-off-telemetry-on-hello-infrastructure-virtual-machines-optional"></a>Désactiver la télémétrie sur des machines virtuelles d’infrastructure hello (facultatif)

Après avoir hello le déploiement est réussi, exécutez hello suivant script dans une fenêtre PowerShell avec élévation de privilèges (hello AzureStack\AzureStackAdmin utilisateur) sur l’hôte de kit de développement hello :

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

tooconfigure télémétrie de SQL Server, consultez [comment tooconfigure SQL Server 2016](https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft).

### <a name="usage-reporting"></a>Rapports d’utilisation

Via l’inscription, la pile de Azure est également configuré tooforward l’utilisation des informations tooAzure. Les rapports d’utilisation sont contrôlés indépendamment de la télémétrie. Vous pouvez désactiver l’utilisation de la création de rapports lorsque [inscription](azure-stack-register.md) à l’aide du script de hello sur Github. Simplement ensemble hello **$reportUsage** paramètre trop**$false**.

Les données d’utilisation sous la forme hello détaillée dans [tooAzure de données d’utilisation de rapport Azure pile](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-usage-reporting). L’utilisation du Kit de développement Azure Stack n’est pas soumise à facturation. Cette fonctionnalité est incluse dans le kit de développement hello afin que vous puissiez tester toosee fonctionne du rapport d’utilisation. 


## <a name="next-steps"></a>Étapes suivantes
[Télécharger le package de déploiement kit de développement hello Azure pile](https://azure.microsoft.com/overview/azure-stack/try/?v=try)

[Déployer le Kit de développement Azure Stack](azure-stack-run-powershell-script.md)

