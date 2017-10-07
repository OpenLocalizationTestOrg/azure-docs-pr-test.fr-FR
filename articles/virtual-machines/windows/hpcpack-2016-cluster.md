---
title: aaaHPC Pack 2016 de cluster dans Azure | Documents Microsoft
description: "Découvrez comment toodeploy une 2016 de Pack HPC cluster dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>Déployer un cluster HPC Pack 2016 dans Azure

Suivez les étapes de hello dans cet article de toodeploy un [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster dans les machines virtuelles. HPC Pack est la solution HPC gratuite de Microsoft basée sur les technologies Microsoft Azure et Windows Server. Elle prend en charge un vaste éventail de charges de travail HPC.

Utilisez une des hello [modèles Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) cluster hello HPC Pack 2016 de toodeploy. Vous avez plusieurs options de topologie de cluster avec différents nombres de nœuds principaux de cluster et vous pouvez utiliser des nœuds de calcul Linux ou Windows.

## <a name="prerequisites"></a>Composants requis

### <a name="pfx-certificate"></a>Certificat PFX

Un cluster Microsoft HPC Pack 2016 nécessite une certificat Exchange d’informations personnelles (PFX) toosecure une communication hello entre les nœuds HPC hello. certificat de Hello doit respecter hello suivant les exigences :

* Il doit avoir une clé privée capable d’échanger des clés.
* L’utilisation de clés comprend la signature numérique et le chiffrage de clés.
* L’utilisation améliorée de la clé inclut l’authentification cliente et serveur.

Si vous n’avez pas encore un certificat qui répond à ces exigences, vous pouvez demander le certificat de hello à partir d’une autorité de certification. Vous pouvez également utiliser hello suivant de commandes toogenerate hello un certificat auto-signé fonction hello système d’exploitation sur lequel vous exécutez la commande hello et exportez un certificat PFX format hello avec la clé privée.

* **Pour Windows 10 ou Windows Server 2016**, exécutez hello intégré **New-SelfSignedCertificate** applet de commande PowerShell comme suit :

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **Pour les systèmes d’exploitation antérieurs à Windows 10 ou Windows Server 2016**, télécharger hello [générateur du certificat auto-signé](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) de hello Microsoft Script Center. Extrayez son contenu, puis exécutez hello suivant les commandes à l’invite de PowerShell :

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>Télécharger le certificat tooan coffre de clés Azure

Avant de déployer un cluster HPC de hello, télécharger hello certificat tooan [coffre de clés Azure](../../key-vault/index.md) comme un Bonjour secret et enregistrement suivant des informations pour une utilisation pendant le déploiement de hello : **nom du coffre**,  **Groupe de ressources de coffre**, **URL de certificat**, et **empreinte numérique du certificat**.

Un certificat de hello exemple PowerShell script tooupload suit. Pour plus d’informations sur le téléchargement d’un certificat de tooan coffre de clés Azure, consultez [prise en main d’Azure Key Vault](../../key-vault/key-vault-get-started.md).

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a>Topologies prises en charge

Choisissez une des hello [modèles Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) cluster hello HPC Pack 2016 de toodeploy. Voici les principales architectures des trois topologies de cluster prises en charge. Les topologies à haute disponibilité incluent plusieurs nœuds principaux de cluster.

1. Cluster haute disponibilité avec un domaine Active Directory

    ![Cluster haute disponibilité dans un domaine AD](./media/hpcpack-2016-cluster/haad.png)



2. Cluster haute disponibilité sans domaine Active Directory

    ![Cluster haute disponibilité sans domaine AD](./media/hpcpack-2016-cluster/hanoad.png)

3. Cluster avec un seul nœud principal

   ![Cluster avec un seul nœud principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>Déployer un cluster

cluster de hello toocreate, choisir un modèle et cliquez sur **déployer tooAzure**. Bonjour [portail Azure](https://portal.azure.com), spécifiez des paramètres pour le modèle de hello comme décrit dans hello comme suit. Chaque modèle crée toutes les ressources Azure requis pour l’infrastructure de cluster HPC hello. Les ressources incluent un réseau virtuel Azure, une adresse IP publique, un équilibreur de charge (uniquement pour un cluster haute disponibilité), des interfaces réseau, des groupes à haute disponibilité, des comptes de stockage et des machines virtuelles.

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>Étape 1 : Sélectionnez l’abonnement de hello, l’emplacement et groupe de ressources

Hello **abonnement** et hello **emplacement** doit être le même que vous avez spécifié lorsque vous avez téléchargé votre certificat PFX (voir la configuration requise). Nous vous recommandons de créer un **groupe de ressources** pour le déploiement de hello.

### <a name="step-2-specify-hello-parameter-settings"></a>Étape 2 : Spécifier les paramètres hello

Entrez ou modifiez les valeurs des paramètres du modèle hello. Cliquez sur le paramètre suivant tooeach hello icône pour les informations d’aide. Consultez également les conseils de hello pour [des tailles de machine virtuelle disponibles](sizes.md).

Spécifiez les valeurs hello enregistrés dans les conditions préalables de hello pour hello paramètres suivants : **nom du coffre**, **groupe de ressources de coffre**, **URL de certificat**et **Empreinte numérique du certificat**.

### <a name="step-3-review-legal-terms-and-create"></a>Étape 3. Consulter les termes et conditions et créer
Cliquez sur **passez en revue les conditions juridiques** termes du contrat de tooreview hello. Si vous acceptez, cliquez sur **achat**, puis cliquez sur **créer** déploiement de hello toostart.

## <a name="connect-toohello-cluster"></a>Se connecter toohello cluster
1. Après le déployée de cluster HPC Pack de hello, accédez à toohello [portail Azure](https://portal.azure.com). Cliquez sur **groupes de ressources**et groupe de ressources hello rechercher dans le hello cluster a été déployée. Machines virtuelles de nœud principal, vous pouvez trouver hello.

    ![Nœuds de cluster principal dans le portail de hello](./media/hpcpack-2016-cluster/clusterhns.png)

2. Cliquez sur un seul nœud principal (dans un cluster de haute disponibilité, cliquez sur un des nœuds de tête hello). Dans **Essentials**, vous pouvez trouver d’adresse IP publique de hello ou le nom DNS complet du cluster de hello.

    ![Paramètres de connexion au cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. Cliquez sur **Connect** toolog sur tooany de nœuds principaux d’hello avec votre nom d’utilisateur administrateur spécifié à l’aide de bureau à distance. Si le cluster hello vous avez déployée est dans un domaine Active Directory, le nom d’utilisateur de hello est sous forme de hello <privateDomainName> \<adminUsername > (par exemple, hpc.local\hpcadmin).

## <a name="next-steps"></a>Étapes suivantes
* Soumettre le cluster tooyour de travaux. Consultez [envoyer des travaux tooHPC un cluster HPC Pack dans Azure](hpcpack-cluster-submit-jobs.md) et [gérer un cluster HPC Pack 2016 dans Azure à l’aide d’Azure Active Directory](hpcpack-cluster-active-directory.md).

