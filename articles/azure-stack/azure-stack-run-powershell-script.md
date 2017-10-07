---
title: "aaaDeploy hello Kit de développement de pile Azure | Documents Microsoft"
description: "Découvrez comment tooprepare hello Kit de développement Azure pile et exécution hello PowerShell script toodeploy il."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 0ad02941-ed14-4888-8695-b82ad6e43c66
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/17/2017
ms.author: erikje
ms.openlocfilehash: a96879fb91000f6b3d3aac3089861e8a573ebead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-azure-stack-development-kit"></a>Déployer hello Kit de développement de pile Azure
kit de développement hello toodeploy, vous devez effectuer hello comme suit :

1. [Télécharger le package de déploiement hello](https://azure.microsoft.com/overview/azure-stack/try/?v=try) tooget hello Cloudbuilder.vhdx.
2. [Préparer hello cloudbuilder.vhdx](#prepare-the-development-kit-host) par en cours d’exécution hello asdk-installer.ps1 script tooconfigure hello ordinateur (hôte de kit de développement hello) sur lequel vous souhaitez que le kit de développement tooinstall. Après cette étape, hôte de kit de développement hello démarrera toohello Cloudbuilder.vhdx.
3. [Déployer le kit de développement hello](#deploy-the-development-kit) sur l’hôte de kit de développement hello.

> [!NOTE]
> Pour de meilleurs résultats, même si vous voulez toouse un environnement déconnecté de la pile d’Azure, il est meilleure toodeploy toohello connecté lors de l’internet. De cette façon, la version d’évaluation de Windows Server 2016 de hello peut être activée au moment du déploiement. Si la version d’évaluation de Windows Server 2016 de hello n’est pas activée dans les 10 jours, il s’arrête.
> 
> 

## <a name="download-and-extract-hello-development-kit"></a>Téléchargez et installez le kit de développement hello
1. Avant de commencer, téléchargement de hello, assurez-vous que votre ordinateur répond à hello suivant des conditions préalables :

   * ordinateur de Hello doit avoir au moins 60 Go d’espace disque libre.
   * [.NET Framework 4.6 (ou ultérieur)](https://aka.ms/r6mkiy) doit être installé.

2. [Page de mise en route accédez toohello](https://azure.microsoft.com/overview/azure-stack/try/?v=try), indiquez vos informations, puis cliquez sur **Submit**.
3. Sous **télécharger le logiciel de hello**, cliquez sur **Kit de développement Azure pile**.
4. Exécutez hello téléchargé AzureStackDownloader.exe fichier.
5. Bonjour **téléchargeur de Kit de développement Azure pile** fenêtre, suivez les étapes 1 à 5.
6. Une fois hello téléchargement terminé, cliquez sur **exécuter** toolaunch hello MicrosoftAzureStackPOC.exe.
7. Examinez l’écran du contrat de licence hello et les informations de hello Self-Extractor Assistant, puis **suivant**.
8. Passez en revue l’écran de déclaration de confidentialité hello et informations de hello Self-Extractor Assistant, puis **suivant**.
9. Sélectionnez hello toobe extrait des fichiers de Destination pour hello, cliquez sur **suivant**.
   * valeur par défaut Hello est : <drive letter>:\<dossier actif > \Microsoft Azure pile
10. Passez en revue écran emplacement de Destination hello et informations de hello Self-Extractor Assistant, puis cliquez sur **extraire** tooextract hello CloudBuilder.vhdx (environ 25 Go) et les fichiers ThirdPartyLicenses.rtf. Ce processus prendra quelques toocomplete de temps.

> [!NOTE]
> Après avoir extrait les fichiers hello, vous pouvez supprimer hello exe et bin fichiers toorecover de l’espace sur l’ordinateur de hello. Ou bien, vous pouvez déplacer ces fichiers tooanother afin que si vous avez besoin de tooredeploy vous n’avez pas besoin les fichiers hello toodownload à nouveau.
> 
> 

## <a name="prepare-hello-development-kit-host"></a>Préparer l’hôte de kit de développement hello
1. Assurez-vous que vous pouvez physiquement connecter l’hôte de kit de développement toohello, ou avoir accès à la console physique (par exemple, KVM). Vous devez disposer de ce type d’accès une fois que vous redémarrez l’hôte de kit de développement hello à l’étape 13 ci-dessous.
2. Vérifiez que hello répond à l’hôte de kit de développement hello [configuration minimale requise](azure-stack-deploy.md). Vous pouvez utiliser hello [vérificateur de déploiement pour Azure pile](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) tooconfirm vos besoins.
3. Connectez-vous en tant que hello hôte de kit de développement tooyour d’administrateur Local.
4. Copiez ou déplacez racine hello CloudBuilder.vhdx fichier toohello hello le lecteur C:\ (C:\CloudBuilder.vhdx).
5. Exécutez hello suivant du dossier de c:\AzureStack_Installer toohello fichier (asdk-installer.ps1) d’installer des kit de développement de script toodownload hello sur votre hôte de kit de développement.
    ```powershell
    # Variables
    $Uri = 'https://raw.githubusercontent.com/Azure/AzureStack-Tools/master/Deployment/asdk-installer.ps1'
    $LocalPath = 'c:\AzureStack_Installer'

    # Create folder
    New-Item $LocalPath -Type directory

    # Download file
    Invoke-WebRequest $uri -OutFile ($LocalPath + '\' + 'asdk-installer.ps1')
    ```
6. Ouvrez une console PowerShell avec élévation de privilèges > exécuter hello C:\AzureStack_Installer\asdk-installer.ps1 script > cliquez sur **préparer vhdx**.
7. Sur hello **Cloudbuilder de sélectionner vhdx** page du programme d’installation Bonjour, parcourir tooand fichier hello sélectionnez cloudbuilder.vhdx que vous avez téléchargé dans les étapes précédentes hello.
8. Facultatif : Vérification hello **ajouter des pilotes** zone toospecify un dossier contenant les pilotes supplémentaires que vous souhaitez sur l’hôte de hello.
9. Sur hello **paramètres facultatifs** , fournissez le compte d’administrateur local hello pour l’hôte de kit de développement hello. Si vous ne fournissez pas ces informations d’identification, vous devez l’hôte de toohello accès KVM pendant le processus d’installation hello ci-dessous.
10. Également sur hello **paramètres facultatifs** page, vous avez hello de tooset option hello suivant :
    - **Nom_Ordinateur**: cette option définit le nom de hello pour l’hôte de kit de développement hello. nom de Hello doit satisfaire aux exigences de nom de domaine complet et doit être de 15 caractères ou moins. valeur par défaut Hello est un nom d’ordinateur aléatoire généré par Windows.
    - **Fuseau horaire**: jeux hello fuseau horaire de l’hôte de kit de développement hello. valeur par défaut Hello est (UTC-8:00) Pacifique (États-Unis et Canada).
    - **Configuration IP statique**: définit votre déploiement toouse une adresse IP statique. Dans le cas contraire, lorsque le programme d’installation hello redémarre en hello cloudbuilder.vhx, les interfaces réseau hello sont configurés avec le protocole DHCP.
11. Cliquez sur **Suivant**.
12. Si vous avez choisi une configuration IP statique à l’étape précédente de hello, vous devez maintenant :
    - Sélectionner une carte réseau. Assurez-vous que vous pouvez vous connecter à un adaptateur de toohello avant de cliquer sur **suivant**.
    - Vérifiez que hello **adresse IP**, **passerelle**, et **DNS** valeurs sont correctes, puis **suivant**.
13. Cliquez sur **suivant** processus de préparation toostart hello.
14. Lorsque la préparation de hello indique **terminé**, cliquez sur **suivant**.
15. Cliquez sur **redémarrer maintenant** tooboot dans hello cloudbuilder.vhdx et continuer le processus de déploiement hello.

## <a name="deploy-hello-development-kit"></a>Déployer le kit de développement hello
1. Connectez-vous en tant que hello hôte de kit de développement toohello d’administrateur Local. Utilisez les informations d’identification de l’hello spécifiées dans les étapes précédentes hello.

    > [!IMPORTANT]
    > Pour les déploiements d’Active Directory de Azure, Azure pile nécessite toohello d’accès Internet, directement ou via un proxy transparent. déploiement de Hello prend en charge une seule carte réseau de mise en réseau. Si vous avez plusieurs cartes réseau, assurez-vous que seul l’un est activé (et tous les autres sont désactivés) avant d’exécuter le script de déploiement hello dans la section suivante de hello.
    
2. Ouvrez une console PowerShell avec élévation de privilèges > exécuter le script de \AzureStack_Installer\asdk-installer.ps1 hello (qui peut être sur un autre lecteur Bonjour Cloudbuilder.vhdx) > cliquez sur **installer**.
3. Bonjour **Type** boîte, sélectionnez **Azure Cloud** ou **ADFS**.
    - **Cloud Azure**: Azure Active Directory est le fournisseur d’identité hello. Utilisez ce paramètre de toospecify un répertoire spécifique où hello AAD compte ne dispose d’autorisations d’administrateur global. Nom complet d’un client d’annuaire AAD dans le format hello. onmicrosoft.com. 
    - **AD FS**: tampon par défaut de hello Service d’annuaire est le fournisseur d’identité hello, hello toosign de compte par défaut avec azurestackadmin@azurestack.local, et toouse de mot de passe hello est hello vous fourni dans le cadre du programme d’installation hello.
4. Sous **mot de passe administrateur Local**, Bonjour **mot de passe** boîte, de type hello mot passe administrateur local (qui doit correspondre au mot de passe administrateur local hello actuel configuré), puis cliquez sur  **Suivant**.
5. Sélectionnez un toouse de carte réseau pour le kit de développement hello puis **suivant**.
6. Sélectionnez DHCP ou la configuration réseau statique pour l’ordinateur virtuel de BGPNAT01 hello.
    - **DHCP** (par défaut) : hello virtuels Obtient la configuration de réseau IP hello à partir du serveur DHCP de hello.
    - **Statique**: utilisez cette option uniquement si DHCP ne peut pas attribuer une adresse IP valide pour la pile de Azure tooaccess hello Internet. Une adresse IP statique doit être spécifiée avec la longueur du masque de sous-réseau hello (par exemple, 10.0.0.5/24).
7. Si vous le souhaitez, définissez hello valeurs suivantes :
    - **ID de VLAN**: jeux hello ID VLAN. Utilisez cette option uniquement si hello hôte et AzS-BGPNAT01 doit configurer l’ID de VLAN tooaccess réseau physique de hello (et Internet). 
    - **Redirecteur DNS**: un serveur DNS est créé dans le cadre de hello déploiement de la pile de Azure. ordinateurs tooallow dans les noms de tooresolve solution hello en dehors de l’horodatage de hello, fournissez votre serveur DNS d’infrastructure existante. serveur DNS dans l’horodatage Hello transfère serveur de toothis de demandes de résolution de nom inconnu.
    - **Serveur de temps**: définit un serveur de temps spécifique. 
8. Cliquez sur **Suivant**. 
9. Sur hello **vérification des propriétés de carte d’interface réseau** page, vous verrez une barre de progression. 
    - Si elle indique **une mise à jour ne peuvent pas être téléchargée**, suivez les instructions hello sur la page de hello.
    - Quand elle indique **Terminé**, cliquez sur **Suivant**.
10. Dans la page **Récapitulatif**, cliquez sur **Déployer**.
11. Si vous utilisez un déploiement d’Azure Active Directory, vous serez invité tooenter vos informations d’identification du compte d’administrateur général Azure Active Directory.
12. processus de déploiement Hello peut prendre quelques heures, pendant laquelle hello système redémarre automatiquement une seule fois.
   
   > [!IMPORTANT]
   > Si vous souhaitez que la progression du déploiement toomonitor hello, connectez-vous en tant qu’azurestack\AzureStackAdmin. Si vous connecter qu’un administrateur local une fois l’ordinateur de hello jointe toohello domaine, vous ne voyez pas la progression du déploiement hello. Ne réexécutez pas le déploiement, à la place de connexion en tant que toovalidate azurestack\AzureStackAdmin qu’il est en cours d’exécution.
   > 
   > 
   
    Lors de la réussite du déploiement de hello, console PowerShell de hello affiche : **terminé : l’Action « Déploiement »**.
   
Si le déploiement de hello échoue, vous pouvez utiliser hello suite du script PowerShell exécuter à nouveau à partir de hello même fenêtre PowerShell avec élévation de privilèges :

```powershell
cd c:\CloudDeployment\Setup
.\InstallAzureStackPOC.ps1 -Rerun
```

Ce script va redémarrer le déploiement hello à hello dernière étape qui a réussi.

Vous pouvez aussi [redéployer](azure-stack-redeploy.md) à partir de zéro.


## <a name="reset-hello-password-expiration-too180-days"></a>Réinitialiser les jours de too180 avant expiration de mot de passe hello

toomake que ce mot de passe hello pour l’hôte de kit de développement hello n’expire jamais trop tôt, suivez ces étapes après avoir déployé :

1. Sur l’hôte du kit de développement de hello, ouvrez **gestion des stratégies de groupe** et accédez trop**gestion des stratégies de groupe** – **forêt : azurestack.local** – **domaines**  – **azurestack.local**.
2. Cliquez avec le bouton droit sur **MemberServer** et cliquez sur **Modifier**.
3. Bonjour éditeur de gestion de stratégie de groupe, accédez trop**Configuration ordinateur** – **stratégies** – **paramètres Windows** – **paramètres de sécurité**– **Stratégies de comptes** – **stratégie de mot de passe**.
4. Dans le volet droit de hello, double-cliquez sur **de vie maximale du mot de passe**.
5. Bonjour **de vie maximale du mot de passe propriétés** boîte de dialogue, modification hello **mot de passe va expirer dans** too180 de valeur, puis cliquez sur **OK**.


## <a name="next-steps"></a>Étapes suivantes
[Inscrire Azure Stack auprès de votre abonnement Azure](azure-stack-register.md)

[Se connecter tooAzure pile](azure-stack-connect-azure-stack.md)

