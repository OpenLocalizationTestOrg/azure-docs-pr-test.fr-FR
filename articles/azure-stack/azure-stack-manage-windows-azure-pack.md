---
title: "virtuels aaaManage Windows Azure Pack à partir de la pile de Azure | Documents Microsoft"
description: "Découvrez comment toomanage machines virtuelles de Windows Azure Pack (WAP) à partir du portail de l’utilisateur dans la pile de Azure hello."
services: azure-stack
documentationcenter: 
author: walterov
manager: byronr
editor: 
ms.assetid: 213c2792-d404-4b44-8340-235adf3f8f0b
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: walterov
ms.openlocfilehash: 97dbe34055667a72fddc8507ae389562e885a32e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-azure-pack-virtual-machines-from-azure-stack"></a>Gérer des machines virtuelles Windows Azure Pack à partir d’Azure Stack
Bonjour Kit de développement de pile Azure, vous pouvez activer l’accès à partir d’ordinateurs virtuels hello Azure pile utilisateur portail tootenant en cours d’exécution sur Windows Azure Pack. Locataires peuvent utiliser toomanage de portail Azure pile hello leurs des machines virtuelles IaaS existantes et les réseaux virtuels. Ces ressources sont disponibles sur Windows Azure Pack via les composants de Service Provider Foundation (SPF) et Virtual Machine Manager (VMM) sous-jacent hello. Plus précisément, les locataires peuvent :

* Parcourir les ressources
* Examiner les valeurs de configuration
* Démarrer ou arrêter une machine virtuelle
* Se connecter tooa virtuels via protocole RDP (Remote Desktop)
* Créer et gérer des points de contrôle
* Supprimer des réseaux virtuels et des machines virtuelles

Cette fonctionnalité est fournie par hello connecteur du Pack Windows Azure pour la pile de Azure (aperçu). Cet article explique comment tooconfigure hello connector pour un environnement de la pile d’Azure à nœud unique.

Pour cette version préliminaire du connecteur de hello, tenez compte des éléments suivants de hello :
* Utilisez hello Windows Azure Pack connecteur uniquement dans les environnements de test (pour la pile d’Azure et Windows Azure Pack) et non dans les déploiements de production.
* Vous devez avoir Windows Azure Pack Update Rollup (UR) 9.1 ou ultérieur et System Center SPF et VMM UR 9 ou ultérieur.
* Hello VMM et les composants de SPF peuvent être System Center 2012 R2 ou System Center 2016.
* Vous devez effectuer les étapes de configuration à la fois sur Azure Stack et sur Windows Azure Pack.
* instructions de Hello s’appliquent à des environnements toonon-Cloud Platform System (CPS).
* tooreview hello problèmes connus, consultez [dépannage de Microsoft Azure pile](azure-stack-troubleshooting.md).


## <a name="architecture"></a>Architecture
Hello diagramme suivant montre hello principaux composants de hello connecteur du Pack Windows Azure.

![composants du connecteur du Pack Windows Azure Hello](media/azure-stack-manage-wap/image1.png)

Notez hello les détails suivants :
* portail de l’utilisateur Azure pile Hello accède à des informations sur les ressources hello dans les deux clouds (pile de Azure et Windows Azure Pack).
* utilisateur de Hello doit posséder un compte qui est valide dans les deux environnements.
* portail de l’utilisateur Azure pile Hello doit avoir des composants d’accès réseau toohello en cours d’exécution sur Windows Azure Pack.
* Bonjour **WAP** section hello diagramme de, vous pouvez afficher hello nouveau connecteur de Windows Azure Pack (WAP Extension et connecteur) et hello existant API Windows Azure Pack client avec les composants de SPF et de VMM.


## <a name="identity-management"></a>Gestion des identités
Hello API du locataire Windows Azure Pack doit approuver hello service Azure pile de jeton de sécurité (STS).

Lorsqu’un utilisateur effectue une action via le portail d’Azure pile hello qui cible les ressources Windows Azure Pack, portail de hello utilise hello API du locataire Windows Azure Pack. Par conséquent, le jeton d’authentification utilisateur hello fournie doit provenir d’un STS approuvé. Consultez hello suivant schéma :

![Diagramme d’authentification du connecteur Windows Azure Pack](media/azure-stack-manage-wap/image2.png)

Dans l’environnement de kit de développement hello, Windows Azure Pack et Azure pile ont les fournisseurs d’identité indépendant. Les utilisateurs qui accèdent à ces deux environnements à partir du portail de pile de Azure hello doivent avoir hello nom de même nom d’utilisateur principal (UPN) dans les deux fournisseurs d’identité. Par exemple, hello compte  *azurestackadmin@azurestack.local*  doit également exister Bonjour STS pour Windows Azure Pack. Où AD FS n’est pas configuré de relations d’approbation sortante toosupport, vous établissez une approbation à partir de l’instance de pile de Azure hello Windows Azure Pack (API du locataire) des composants toohello d’AD FS.

## <a name="prerequisites"></a>Composants requis

### <a name="download-hello-windows-azure-pack-connector"></a>Télécharger hello connecteur du Pack Windows Azure
Sur hello [Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc), téléchargez le fichier .exe de hello et extrayez-le tooyour les ordinateur local. Une version ultérieure, vous copiez hello contenu tooa de l’ordinateur qui peut accéder à votre environnement Windows Azure Pack.

### <a name="deployment-option-requirement"></a>Options de déploiement requises
toointegrate avec Windows Azure Pack, vous pouvez déployer Azure pile à l’aide d’option de hello AD FS ou hello Azure Active Directory.

### <a name="connectivity-requirements"></a>Connectivité requise
1. À partir de l’ordinateur hello sur lequel vous accéder au portail de l’utilisateur Azure pile hello, assurez-vous que vous avez accès portail des locataires Windows Azure Pack hello via un navigateur web de hello.
2. machine virtuelle de Hello AzS-WASP01 sur la pile d’Azure doit être l’ordinateur portail du locataire Windows Azure Pack toohello tooconnect en mesure de. Utiliser une connexion de réseau tooverify Ping.exe. 
3.  Vous devez disposer des certificats valides pour les nouveaux services de connecteur hello. Ces certificats SSL doivent être émis par une autorité de certification approuvée. Vous ne pouvez pas utiliser de certificats auto-signés. les certificats SSL Hello doivent être approuvés par la pile de Azure (spécifiquement hello AzS-WASP01 VM) et tout autre ordinateur hello client peut utiliser le portail de l’utilisateur Azure pile tooaccess hello.
 
    >[!NOTE]
    AzS-WASP01 s’exécutant Windows Server avec l’option d’installation Server Core de hello, vous pouvez utiliser un outil de ligne de commande telles que le certificat Certutil.ext tooimport hello. Par exemple, votre peut copier tooc:\temp de fichier .cer hello sur AzS-WASP01, puis exécutez la commande hello **certutil - addstore « AC », « c:\temp\certname.cer »**.

4.  tooestablish RDP connectivité tooWindows virtuels Azure Pack client via le portail d’Azure pile hello, environnement de Windows Azure Pack hello doit autoriser les ordinateurs virtuels clients toohello le trafic de bureau à distance.
5.  Pour la connectivité entre les ordinateurs virtuels du locataire Azure pile et les ordinateurs virtuels du locataire Windows Azure Pack, leurs adresses IP externes doivent être routables entre les deux environnements de hello. Cette connexion peut également inclure l’association d’un nom de machine virtuelle DNS server tooresolve entre les environnements de hello.

### <a name="iis-requirements"></a>Exigences relatives à IIS
ordinateur Hello qui héberge le portail de locataires Windows Azure Pack hello (qui peut être un hôte physique, un ordinateur virtuel ou plusieurs ordinateurs virtuels) doit avoir l’extension IIS de réécriture d’URL de hello sont installées. Si elle n’est pas encore installée, vous pouvez la télécharger à partir de [cette page](https://www.iis.net/downloads/microsoft/url-rewrite). Si plusieurs machines virtuelles héberger le portail de locataires hello, installer l’extension de hello sur chaque ordinateur virtuel.

## <a name="configure-azure-stack"></a>Configurer Azure Stack
Avant de configurer hello connecteur du Pack Windows Azure, vous devez activer le mode de cloud multiples dans le portail de l’utilisateur Azure pile hello. Ce mode permet de tooselect les utilisateurs à partir de quelles ressources tooaccess de cloud.

tooenable en mode de cloud multiples, vous devez exécuter le script Add-AzurePackConnector.ps1 de hello après le déploiement de la pile d’Azure. Hello tableau suivant décrit les paramètres de script hello.


|  Paramètre | Description | Exemple |   
| -------- | ------------- | ------- |  
| AzurePackClouds | URI de hello connecteurs de Windows Azure Pack. Ces URI doit correspondre à toohello des portails de locataires Windows Azure Pack. | @{CloudName = "AzurePack1"; CloudEndpoint = "https://waptenantportal1:40005"},@{CloudName = "AzurePack2"; CloudEndpoint = "https://waptenantportal2:40005"}<br><br>  (Par défaut, la valeur du port hello est 40005). |  
| AzureStackCloudName | Étiquette toorepresent hello local Azure pile cloud.| "AzureStack" |
| DisableMultiCloud | Mode commutateur toodisable cloud multiples.| N/A |
| | |

Vous pouvez exécuter le script de hello Add-AzurePackConnector.ps1 immédiatement après le déploiement, ou version ultérieure. toorun hello immédiatement après déploiement du script, utilisez hello même session Windows PowerShell où le déploiement d’Azure pile s’est terminée. Sinon, vous pouvez ouvrir une nouvelle session Windows PowerShell en tant qu’administrateur (connecté en tant que compte d’azurestackadmin hello).

1. Exécuter le script de hello Add-AzurePackConnector.ps1 à l’aide de hello suivant de commandes (avec l’environnement de tooyour spécifique de valeurs). Notez que script de Add-AzurePackConnector hello permet de vous tooadd plus d’un point de terminaison de connecteur de Windows Azure Pack.
 
 ```powershell
    $cred = New-Object System.Management.Automation.PSCredential("cloudadmin@azurestack.local", `
    (ConvertTo-SecureString -String "<password>" -AsPlainText -Force))
    $session = New-PSSession -ComputerName 'azs-ercs01' `
     -Credential $cred `
     -ConfigurationName PrivilegedEndpoint `
     -Authentication Credssp

    # Enable Multicloud
    Invoke-Command -Session $session -ScriptBlock { Add-AzurePackConnector -AzurePackClouds `
    @{CloudName = "AzurePack_1"; CloudEndpoint = "https://waptenantportal1:40005"},`
    @{CloudName = "AzurePack_2"; CloudEndpoint = "https://waptenantportal2:40005" } `
    -AzureStackCloudName "AzureStack" }

 ```
> [!NOTE]
> Hello génération en cours, il existe un problème où après hello Add-AzurePackConnector script se termine, il reste dans une boucle d’interrogation pour un certain temps (quelques minutes) jusqu'à ce que s’il se termine. Une fois que vous voyez le message de type hello **VERBOSE : étape 'Configurer le connecteur Azure Pack' état : 'Réussite'**, vous pouvez arrêter l’exécution de script hello ou patientez jusqu'à ce qu’il s’arrête en lui-même. Il ne sera pas faire la différence, car la configuration de hello a déjà réussi.

2. Prenez note des fichiers de sortie hello qui sont produites par ce script, un pour chaque environnement Windows Azure Pack que vous avez spécifié. Hello fichiers sont trouvent dans : \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput. Ces fichiers contiennent des informations hello sont requis tooconfigure hello cible Windows Azure Pack environnements. Vous passez ce fichier en tant que paramètre tooa script ultérieurement dans ces instructions. Ce fichier contient hello informations suivantes :

    * **AzurePackConnectorEndpoint**: contient le service de connecteur de Windows Azure Pack toohello hello point de terminaison.
    * **AuthenticationIdentityProviderPartner**: contient hello suivant paire valeur :
        * Jeton d’authentification de signature de certificat hello API du locataire Windows Azure Pack doit tootrust tooaccept les appels à partir de l’extension du portail Azure pile de hello.

        * Hello « Realm » associé au certificat de signature de hello. Par exemple : https://adfs.local.azurestack.global.external/adfs/c1d72562-534e-4aa5-92aa-d65df289a107/.

3.  Parcourir un dossier toohello qui contient les fichiers de sortie hello (\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) et copie hello fichiers tooyour ordinateur local. les fichiers Hello ressemblera toothis similaire : AzurePack-06-27-15-50.txt.

4.  Configuration de test hello.

    a. Ouvrez votre navigateur et connectez-vous au portail de l’utilisateur Azure pile toohello (https://portal.local.azurestack.external/).
    
    b. Après que vous être connecté en tant qu’une charge de portail locataire et hello, vous verrez des erreurs concernant n’est ne pas en mesure de toofetch abonnements ou les extensions de hello Azure Pack : cloud. Cliquez sur **OK** tooclose ces messages. (Ces messages d’erreur disparaîtront une fois que vous aurez configuré Windows Azure Pack.)

    c. Hello d’avis **Cloud** liste déroulante dans le coin supérieur gauche de hello du portail de hello.

    ![Sélecteur de cloud Hello dans l’interface utilisateur hello Azure pile](media/azure-stack-manage-wap/image3.png)

## <a name="configure-windows-azure-pack"></a>Configurer Windows Azure Pack
Pour cette préversion du connecteur uniquement, vous devez configurer Windows Azure Pack manuellement.

>[!IMPORTANT]
Pour cette version préliminaire, utilisez hello Windows Azure Pack connecteur uniquement dans les environnements de test et non dans les déploiements de production.

1.  Installer les fichiers MSI du connecteur sur l’ordinateur de virtuel portail hello Windows Azure Pack client et installer des certificats. (Si vous avez plusieurs machines virtuelles dans le portail du locataire, vous devez effectuer cette étape sur chaque machine virtuelle.)

    a. Dans l’Explorateur de fichiers, copiez hello **WAPConnector** dossier (ce que vous avez téléchargé précédemment) dossier tooa nommé **c:\temp** dans l’ordinateur virtuel du portail locataire hello.

    b. Ouvrez une Console ou RDP connexion toohello portail ordinateur virtuel du client.

    c. Remplacez les répertoires**c:\temp\wapconnector\setup\scripts**et exécution hello **Install-Connector.ps1** tooinstall trois fichiers de script. Aucun paramètre n’est nécessaire.

     ```powershell
    cd C:\temp\wapconnector\setup\scripts\

    .\Install-Connector.ps1
    ```
     d. Remplacez les répertoires**c:\inetpub** et vérifiez que les trois nouveaux sites hello sont installés :

       * MgmtSvc-Connector

       * MgmtSvc-ConnectorExtension

       * MgmtSvc-ConnectorController

    e. À partir de hello même **c:\temp\wapconnector\setup\scripts** dossier, exécutez hello **configurer-Certificates.ps1** tooinstall certificats de script. Par défaut, il utilisera hello même certificat est disponible pour le site de portail client hello dans Windows Azure Pack. Assurez-vous qu’il s’agit d’un certificat valide (approuvé par la machine virtuelle de Azure pile AzS-WASP01 hello et n’importe quel ordinateur client qui accède au portail d’Azure pile hello). Si ce n’est pas le cas, la communication ne fonctionnera pas. (Ou bien, vous pouvez transmettre explicitement un empreinte numérique du certificat en tant que paramètre à l’aide de hello - paramètre de l’empreinte.)

     ```powershell
        cd C:\temp\wapconnector\setup\scripts\

        .\Configure-Certificates.ps1
    ```

    f. configuration de hello toofinish de ces trois services, exécutez hello **WapConnector.ps1-configurer** script des paramètres du fichier Web.config tooupdate hello.

    |  Paramètre | Description | Exemple |   
    | -------- | ------------- | ------- |  
    | TenantPortalFQDN | portail de locataires Windows Azure Pack Hello nom de domaine complet. | tenant.contoso.com | 
    | TenantAPIFQDN | Hello le FQDN API locataire Windows Azure Pack. | tenantapi.contoso.com  |
    | AzureStackPortalFQDN | portail de l’utilisateur Azure pile Hello nom de domaine complet. | portal.local.azurestack.external |
    | | |
    
     ```powershell
    .\Configure-WapConnector.ps1 -TenantPortalFQDN "tenant.contoso.com" `
         -TenantAPIFQDN "tenantapi.contoso.com" `
         -AzureStackPortalFQDN "portal.local.azurestack.external"
    ```
    g. Si vous avez plusieurs machines virtuelles de portail du locataire, répétez l’étape 1 pour chacune de ces machines virtuelles.

2. Installation Bonjour nouvelle MSI d’API client sur chaque ordinateur virtuel de API du locataire Windows Azure Pack.

    a. Si un équilibreur de charge est en cours d’utilisation, vous souhaiterez toomark hello machine virtuelle comme étant hors connexion.

    b. Dans l’Explorateur de fichiers, copiez hello **WAPConnector** tooa dossier nommé **c:\temp** sur chaque ordinateur de l’API client.

    c. Copier hello AzurePackConnectorOutput.txt le fichier que vous avez enregistré précédemment, trop**c:\temp\WAPConnector**.

    d. Ouvrez une connexion Console ou RDP toohello vous avez copié les fichiers hello pour machine virtuelle de API locataire.
    
    e. Remplacez les répertoires**c:\temp\wapconnector\setup\scripts**et exécutez **TenantAPI.ps1 de mise à jour**. Cette nouvelle version de hello API des locataires WAP contient un tooenable modifier une relation d’approbation avec STS actuel de hello, mais également avec l’instance hello d’AD FS dans la pile de Azure.

     ```powershell
    cd C:\temp\wapconnector\setup\packages\

    .\Update-TenantAPI.ps1
    ```

    f.  Répétez l’étape 2 sur n’importe quel autre ordinateur virtuel en cours d’exécution hello API client.
3. À partir de **qu’une seule** Hello locataire, API machines virtuelles, exécutez tooadd de script hello TrustAzureStack.ps1 de configurer une relation d’approbation entre hello API client et l’instance de hello AD FS sur la pile de Azure. Vous devez utiliser un compte avec la base de données sysadmin accès toohello Microsoft.MgmtSvc.Store. Ce script a hello paramètres suivants :

    | Paramètre | Description | Exemple |
    | --------- | ------------| ------- |
   | SqlServer | nom Hello Hello SQL Server qui contient la base de données Microsoft.MgmtSvc.Store hello. Ce paramètre est obligatoire. | SQLServer | 
   | DataFile | fichier de sortie Hello qui a été générée lors de la configuration hello du mode de plusieurs cloud hello Azure pile précédemment. Ce paramètre est obligatoire. | AzurePack-06-27-15-50.txt | 
   | PromptForSqlCredential | Indique que le script de hello vous invite à entrer interactivement pour un toouse d’informations d’identification de l’authentification SQL lors de la connexion d’instance de SQL Server toohello. Hello fourni les informations d’identification et doit être suffisamment autorisations toouninstall bases de données, schémas, supprimer des connexions utilisateur. Si aucun n’est fourni, script de hello suppose que ce contexte de l’utilisateur actuel a accès. | Aucune valeur n’est nécessaire. |
   |  |  |

    Si vous ne connaissez pas hello SQL Server toouse, vous pouvez la découvrir. Connecter toohello API client ordinateur, utilisez hello Unprotect-MgmtSvc commande toounprotect hello client API Web.config fichier et recherchez le nom du serveur hello dans la chaîne de connexion hello. Souvenez-vous toorun MgmtSvc-protéger à nouveau fichier de locataire API Web.config tooprotect hello.

  ```powershell
  cd C:\temp\wapconnector\setup\scripts\

 .\Configure-TrustAzureStack.ps1 -SqlServer "SQLServer" `
       -DataFile "C:\temp\wapconnector\AzurePackConnectorOutput.txt"
  ```

## <a name="example"></a>Exemple
Hello suivant montre un déploiement complet de connecteur de Windows Azure Pack sur une configuration de la pile d’Azure à nœud unique et les deux installations de Windows Azure Pack Express. (Chaque installation d’Express se trouve sur un ordinateur unique, avec des noms d’exemple hello *wapcomputer1* et*wapcomputer2*.)

```powershell
# Run hello following script on hello Azure Stack host
$cred = New-Object System.Management.Automation.PSCredential("cloudadmin@azurestack.local",`
     (ConvertTo-SecureString -String "p@ssw0rd" -AsPlainText -Force))
$session = New-PSSession -ComputerName 'azs-ercs01' -Credential $cred `
     -ConfigurationName PrivilegedEndpoint -Authentication Credssp
 
# Enable Multicloud
invoke-command -Session $session -ScriptBlock { Add-AzurePackConnector -AzurePackClouds `
     @{CloudName = "AzurePack_1"; CloudEndpoint = "https://wapcomputer1.contoso.com:40005"},`
     @{CloudName = "AzurePack_2"; CloudEndpoint = "https://wapcomputer2.contoso.com:40005"}`
     -AzureStackCloudName "AzureStack" }  

```
Téléchargez le fichier .exe de hello de hello [Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc), extrayez-le et copiez hello WAPConnector dossier tooa **c:\temp** dossier sur l’ordinateur de Windows Azure Pack hello. Copiez les fichiers hello qui ont été générées en tant que sortie dans le script précédent de hello (situé dans \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) toohello **c:\temp\WAPConnector** dossier. (les fichiers hello sera semble similaire toothis : AzurePack-06-27-15-50.txt.) Ensuite, exécutez hello script, une fois par instance de Windows Azure Pack suivant :

 ```powershell
# Install Connector components
cd C:\temp\WAPConnector\Setup\Scripts
.\Install-Connector.ps1

# Configure Certificates for hello new Connector services
.\Configure-Certificates.ps1

# Configure hello Connector services
.\Configure-WapConnector.ps1 -TenantPortalFQDN "wapcomputer1.contoso.com" `
     -TenantAPIFQDN "wapcomputer1.contoso.com" `
     -AzureStackPortalFQDN "portal.local.azurestack.external"

# Install hello updated TenantAPI
.\Update-TenantAPI.ps1

# Establish trust with hello Azure Stack AD FS
.\Configure-TrustAzureStack.ps1 -SqlServer "wapcomputer1" `
     -DataFile "C:\temp\wapconnector\AzurePack-06-27-15-50.txt" 

```
## <a name="troubleshooting-tips"></a>Conseils de dépannage
1.  Vérifiez la connectivité réseau entre Azure Stack et Windows Azure Pack. Cette connexion doit être entre n’importe quel ordinateur client qui accède au portail d’Azure pile hello et un hello Windows Azure Pack client portail virtual machine exécutant des nouveaux services de connecteur hello.
2.  Vérifiez que tous les noms de domaine complets spécifiés sont corrects.
3.  Assurez-vous que les certificats SSL hello utilisés dans les nouveaux services de connecteur hello sont approuvés par pile de Azure (spécifiquement hello AzS-WASP01 VM) et un autre client de hello ordinateur peut utiliser le portail de l’utilisateur Azure pile tooaccess hello.
4. Pour plus d’informations sur les problèmes connus, consultez [Dépannage de Microsoft Azure Stack](azure-stack-troubleshooting.md).


## <a name="next-steps"></a>Étapes suivantes
[À l’aide des portails d’administrateur et utilisateur hello dans la pile de Azure](azure-stack-manage-portals.md)
