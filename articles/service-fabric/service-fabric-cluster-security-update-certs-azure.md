---
title: certificats aaaManage dans un cluster Azure Service Fabric | Documents Microsoft
description: "Décrit comment supprimer tooadd de nouveaux certificats et certificat de substitution certificat tooor à partir d’un cluster Service Fabric."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>Ajouter ou supprimer des certificats pour un cluster Service Fabric dans Azure
Il est recommandé de vous familiariser avec la façon dont l’infrastructure de Service utilise des certificats X.509 et être familiarisé avec hello [les scénarios de sécurité du Cluster](service-fabric-cluster-security.md). Vous devez comprendre ce qu’est un certificat de cluster et quelle est son utilité avant de passer à la suite.

Sécurité de certificats de service fabric vous permet de que spécifier que deux cluster certificats, un serveur principal et secondaire, lorsque vous configurez lors de la création du cluster, dans les certificats d’addition tooclient. Consultez trop[création d’un cluster azure via le portail](service-fabric-cluster-creation-via-portal.md) ou [création d’un cluster azure via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) pour plus d’informations sur leur configuration au moment de la création. Si vous ne spécifiez qu’un seul certificat de cluster lors de la création, puis qui est utilisé en tant que certificat principal de hello. Après la création du cluster, vous pouvez ajouter un certificat en tant que certificat secondaire.

> [!NOTE]
> Pour un cluster sécurisé, vous aurez toujours besoin des certificats au moins un cluster valide (non révoqués et n’ayant pas expiré) (principaux ou secondaires) déployé (si ce n’est pas, hello cluster cesse de fonctionner). 90 jours avant que tous les certificats valides atteignent d’expiration, hello système génère un suivi d’avertissement et également un événement d’avertissement d’intégrité sur le nœud de hello. Actuellement, Service Fabric n’envoie aucun courrier électronique ou notification d’aucune sorte à ce sujet. 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a>Ajouter un certificat de cluster secondaire à l’aide du portail de hello

Certificat de cluster secondaire ne peut pas être ajouté via hello portail Azure. Vous avez toouse Azure powershell pour cela. processus de Hello est décrit plus loin dans ce document.

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a>Échanger les certificats de cluster hello à l’aide du portail de hello

Une fois que vous avez correctement déployé un certificat de cluster secondaire, si vous souhaitez tooswap hello principal et secondaire, puis accédez Panneau de sécurité toohello et sélectionnez option de « D’échange avec principal » de hello dans hello contexte menu tooswap hello secondaire cert avec certificat principal de Hello.

![Échange de certificat][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a>Suppression d’un certificat de cluster à l’aide du portail de hello

Pour un cluster sécurisé, vous devez toujours au moins une valid (non révoqué et n’ayant pas expiré) certificat (principal ou secondaire) déployé dans le cas contraire, hello cluster cesse de fonctionner.

tooremove un certificat secondaire d’être utilisés pour la sécurité du cluster, panneau de sécurité toohello naviguer et sélectionnez hello 'Delete' option à partir du menu contextuel de hello sur certificat secondaire de hello.

Si votre objectif est de certificat hello tooremove qui est marqué comme principal, vous devez tooswap avec hello secondaire tout d’abord, puis supprimer hello secondaire après la mise à niveau hello a.

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>Ajouter un certificat secondaire à l’aide de Resource Manager PowerShell

Ces étapes supposent que vous êtes familiarisé avec le fonctionnement du Gestionnaire de ressources et avez déployé au moins un cluster Service Fabric à l’aide d’un modèle de gestionnaire de ressources et modèle hello que vous avez utilisé tooset cluster hello pratique. Il est également supposé que vous maîtrisez l’utilisation de JSON.

> [!NOTE]
> Si vous cherchez un exemple de modèle et les paramètres que vous pouvez utiliser toofollow le long ou comme point de départ, puis le télécharger à partir de ce [-référentiel git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample). 
> 
> 

### <a name="edit-your-resource-manager-template"></a>Modifier votre modèle Resource Manager

Pour faciliter le suivre, exemple 5-VM-1-NodeTypes-Secure_Step2.JSON contient toutes les modifications de hello que nous allons. exemple Hello est disponible à l’adresse [-référentiel git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).

**Assurez-vous que toofollow toutes les étapes de hello**

**Étape 1 :** ouvrez le modèle de gestionnaire de ressources hello utilisé toodeploy mettre en Cluster. (Si vous avez téléchargé l’exemple hello de hello au-dessus de référentiel, puis utilisez 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy un cluster sécurisé et puis ouvrir ce modèle).

**Étape 2 :** ajouter **deux nouveaux paramètres** « secCertificateThumbprint » et « secCertificateUrlValue » de type « chaîne » toohello section des paramètres de votre modèle. Vous pouvez copier hello suivant extrait de code et l’ajouter toohello modèle. En fonction de la source de hello de votre modèle, vous avez peut déjà que ces défini, cas dans ce déplacer l’étape suivante de toohello. 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**Étape 3 :** apporter des modifications toohello **Microsoft.ServiceFabric/clusters** ressource, recherchez la définition de ressource « Microsoft.ServiceFabric/clusters » hello dans votre modèle. Sous les propriétés de cette définition, vous trouverez « Certificate » JSON balise, qui doit ressembler à hello suivant extrait de code JSON :

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Ajoutez une nouvelle balise « thumbprintSecondary » et donnez-lui la valeur « [parameters(’secCertificateThumbprint’)] ».  

Maintenant la définition de ressource hello doit ressembler à hello suivante (selon votre source de modèle de hello, il peut être pas exactement comme hello d’extrait de code ci-dessous). 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Si vous souhaitez trop**cert hello de substitution**, puis spécifiez le nouveau certificat de hello en tant que principal actuel de hello principal et le déplacement en tant que base de données secondaire. Cela entraîne la substitution de hello de votre actuel certificat principal toohello nouveau certificat en une seule étape de déploiement.

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**Étape 4 :** apporter des modifications trop**tous les** hello **Microsoft.Compute/virtualMachineScaleSets** définitions de ressources - recherchez hello Microsoft.Compute/virtualMachineScaleSets ressource définition. Faites défiler toohello « éditeur » : « Microsoft.Azure.ServiceFabric », sous « virtualMachineProfile ».

Dans Paramètres du serveur de publication hello service fabric, vous devez voir quelque chose comme ceci.

![Json_Pub_Setting1][Json_Pub_Setting1]

Ajouter hello nouveau certificat entrées tooit

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

propriétés de Hello doivent maintenant ressembler à ceci

![Json_Pub_Setting2][Json_Pub_Setting2]

Si vous souhaitez trop**cert hello de substitution**, puis spécifiez le nouveau certificat de hello en tant que principal actuel de hello principal et le déplacement en tant que base de données secondaire. Cela entraîne la substitution hello de votre actuel certificat toohello nouveau certificat en une seule étape de déploiement. 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
propriétés de Hello doivent maintenant ressembler à ceci

![Json_Pub_Setting3][Json_Pub_Setting3]


**Étape 5 :** apporter des modifications trop**tous les** hello **Microsoft.Compute/virtualMachineScaleSets** définitions de ressources - recherchez hello Microsoft.Compute/virtualMachineScaleSets ressource définition. Faites défiler toohello « vaultCertificates » :, sous « OSProfile ». Elle devrait ressembler à ceci :


![Json_Pub_Setting4][Json_Pub_Setting4]

Ajoutez hello secCertificateUrlValue tooit. Utilisez hello suivant extrait de code :

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
Maintenant hello résultant Json doit ressembler à ceci.
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> Assurez-vous que vous avez répété étapes 4 et 5 pour toutes les définitions de ressource Nodetypes/Microsoft.Compute/virtualMachineScaleSets hello dans votre modèle. Si vous omettez un d’eux, les certificats hello ne seront pas installés sur cette mise et avoir des résultats inattendus dans votre cluster, y compris le cluster hello en panne (si vous vous retrouvez avec aucun certificat valide que ce cluster hello peut utiliser pour la sécurité. Vérifiez donc bien que vous n’en avez oublié aucune avant de continuer.
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a>Modifier votre modèle fichier tooreflect hello nouveaux paramètres que vous avez ajouté ci-dessus
Si vous utilisez l’exemple hello de hello [-référentiel git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow, vous pouvez démarrer toomake modifications dans l’exemple hello 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON 

Modifier votre paramètre de modèle de gestionnaire de ressources du fichier, ajoutez hello deux nouveaux paramètres pour secCertificateThumbprint et secCertificateUrlValue. 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a>Déployer hello modèle tooAzure

- Vous est désormais prêt toodeploy tooAzure de votre modèle. Ouvrez une invite de commande Azure PS version 1 ou ultérieure.
- Connectez-vous à tooyour compte Azure et sélectionnez l’abonnement azure spécifique de hello. Il s’agit d’une étape importante pour les personnes qui ont toomore d’accès à un seul abonnement azure.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

Test toodeploying préalable du modèle hello il. Utilisez hello même groupe de ressources actuellement déployé sur votre cluster.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

Déployer le groupe de ressources tooyour hello modèle. Utilisez hello même groupe de ressources actuellement déployé sur votre cluster. Exécutez la commande New-AzureRmResourceGroupDeployment de hello. Vous n’avez pas besoin de mode de hello toospecify, étant donné que la valeur par défaut de hello est **incrémentielle**.

> [!NOTE]
> Si vous définissez le Mode tooComplete, vous pouvez supprimer par inadvertance des ressources qui ne sont pas dans votre modèle. Par conséquent, ne l’utilisez pas dans ce scénario.
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

Voici un remplie exemple Hello même powershell.

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

Une fois le déploiement de hello est terminée, se connecter à l’aide du cluster tooyour hello nouveau certificat et effectuer des requêtes. Si vous êtes en mesure de toodo. Vous pouvez supprimer l’ancien certificat de hello. 

Si vous utilisez un certificat auto-signé, n’oubliez pas de tooimport dans votre magasin de certificats local TrustedPeople.

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
Pour référence rapide ici est cluster sécurisée de hello commande tooconnect tooa 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
Pour référence rapide ici est l’intégrité du cluster tooget hello commande

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a>Déploiement de cluster de toohello Application certificats.

Vous pouvez utiliser hello même étapes comme indiqué dans les étapes 5 ci-dessus toohave hello certificats est déployées à partir d’un toohello keyvault nœuds. Vous devez simplement définir et utiliser des paramètres différents.


## <a name="adding-or-removing-client-certificates"></a>Ajout ou suppression de certificats clients

Dans les certificats de cluster toohello plus, vous pouvez ajouter des opérations de gestion de tooperform de certificats de client sur un cluster service fabric.

Vous pouvez ajouter deux types de certificats clients : administrateur ou en lecture seule. Ceux-ci peuvent ensuite être opérations d’administration utilisé toocontrol accès toohello et les opérations de requête sur le cluster de hello. Par défaut, les certificats de cluster de hello sont ajoutés toohello Admin certificats liste autorisée.

Vous pouvez spécifier autant de certificats clients que vous souhaitez. Chaque ajout ou de suppression des résultats dans un cluster de configuration mise à jour toohello service fabric


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>Ajout d’un certificat client administrateur ou en lecture seule via le portail

1. Accédez Panneau de sécurité toohello et sélectionnez hello '+ authentification' bouton sur le panneau de sécurité hello.
2. Dans le panneau de « Authentification ajouter » hello, choisissez hello 'Type d’authentification' - 'Client en lecture seule' ou 'Administrateur client'
3. Choisir d’une méthode hello. Cela indique tooService Fabric si elle doit rechercher ce certificat à l’aide de nom du sujet hello ou l’empreinte numérique hello. En règle générale, il n’est pas une méthode d’autorisation sécurité pratique toouse hello, du nom de l’objet. 

![Ajout de certificat client][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a>Suppression de certificats Client - Admin ou en lecture seule à l’aide hello portail

tooremove un certificat secondaire d’être utilisés pour la sécurité du cluster, panneau de sécurité toohello naviguer et sélectionnez hello 'Delete' option à partir du menu contextuel de hello sur certificat spécifique de hello.



## <a name="next-steps"></a>Étapes suivantes
Lisez les articles suivants pour plus d’informations sur la gestion des clusters :

* [Processus de mise à niveau du cluster Service Fabric et attentes à votre égard](service-fabric-cluster-upgrade.md)
* [Configurer l’accès en fonction du rôle pour les clients](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


