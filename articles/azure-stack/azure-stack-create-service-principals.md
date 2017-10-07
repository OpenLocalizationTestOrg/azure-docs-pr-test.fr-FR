---
title: aaaCreate un Principal de Service pour la pile de Azure | Documents Microsoft
description: "Décrit comment toocreate un principal de service qui peut être utilisé avec le contrôle d’accès basé sur rôle hello dans Azure Resource Manager toomanage accès tooresources."
services: azure-resource-manager
documentationcenter: na
author: heathl17
manager: byronr
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: f090ceed941abe9255bc35ec966bc43df3bb2955
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provide-applications-access-tooazure-stack"></a>Fournir des applications accès tooAzure pile
Lorsqu’une application a besoin d’accès toodeploy ou configurer des ressources par le biais du Gestionnaire de ressources Azure dans la pile d’Azure, vous créez un service principal, qui est une information d’identification pour votre application.  Vous pouvez ensuite déléguer uniquement hello autorisations nécessaires toothat principal du service.  

Par exemple, vous avez peut-être un outil de gestion de configuration qui utilise Azure Resource Manager tooinventory ressources Azure.  Dans ce scénario, vous pouvez créer un principal de service, accorder lecteur de hello service toothat de rôle principal et limiter hello gestion outil tooread uniquement accès à la configuration. 

Principaux de service sont application hello de toorunning préférable avec vos propres informations d’identification, car :

* Vous pouvez affecter des autorisations toohello principal du service qui sont différentes des autorisations de votre propre compte. En règle générale, ces autorisations sont limitée tooexactly quelle application hello doit toodo.
* Vous n’avez pas les informations d’identification de l’application toochange hello si vos responsabilités changent.
* Vous pouvez utiliser une authentification de tooautomate certificat lors de l’exécution d’un script sans assistance.  

## <a name="getting-started"></a>Prise en main

Selon la façon dont vous avez déployé Azure Stack, commencez par créer un principal de service.  Ce document vous guide tout au long de la création d’un principal de service à la fois pour [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) et pour [Active Directory Federation Services (AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).  Une fois que vous avez créé hello principal du service, un ensemble d’étapes de tooboth common AD FS et l’Azure Active Directory sont utilisées trop[déléguer des autorisations](azure-stack-create-service-principals.md#assign-role-to-service-principal) toohello rôle.     

## <a name="create-service-principal-for-azure-ad"></a>Créer un principal de service pour Azure AD

Si vous avez déployé la pile de Azure à l’aide de Azure AD en tant que magasin d’identités hello, vous pouvez créer des principaux de service comme vous le feriez pour Azure.  Cette section vous montre comment les étapes tooperform hello via le portail de hello.  Vérifiez que vous avez hello [AD Azure autorisations requises](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) avant de commencer.

### <a name="create-service-principal"></a>Créer un principal du service
Dans cette section, vous allez créer une application (principal de service) dans Azure AD qui représentera votre application.

1. Connectez-vous à tooyour compte Azure via hello [portail Azure](https://portal.azure.com).
2. Sélectionnez **Azure Active Directory** > **Enregistrement d’applications** > **Ajouter**.   
3. Fournissez un nom et une URL pour l’application hello. Sélectionnez **application Web / API** ou **natif** de type hello d’application, vous souhaitez toocreate. Après avoir défini les valeurs hello, sélectionnez **créer**.

Vous avez créé un principal de service pour votre application.

### <a name="get-credentials"></a>Récupérer les informations d’identification
Lors de la connexion par programme, vous utilisez hello ID pour votre application et une clé d’authentification. tooget ces valeurs, hello utilisation comme suit :

1. Dans **Inscriptions d’applications** dans Active Directory, sélectionnez votre application.

2. Hello de copie **ID d’Application** et stockez-le dans votre code d’application. Hello applications Bonjour [exemples d’applications](#sample-applications) section font référence à valeur toothis en tant qu’id de client hello.

     ![ID CLIENT](./media/azure-stack-create-service-principal/image12.png)
3. toogenerate une clé d’authentification, sélectionnez **clés**.

4. Fournir une description de la clé de hello et une durée de clé de hello. Lorsque vous avez terminé, sélectionnez **Enregistrer**.

Après avoir enregistré la clé de hello, hello clé de hello est affichée. Copiez cette valeur, car vous sont pas en mesure de tooretrieve hello clé plus tard. Vous fournissez les valeur de clé hello hello application ID toosign en tant qu’application hello. Stockez la valeur de clé hello où votre application peut les récupérer.

![clé enregistrée](./media/azure-stack-create-service-principal/image15.png)


Une fois terminé, passez trop[affectation d’un rôle de votre application](azure-stack-create-service-principals.md#assign-role-to-service-principal).

## <a name="create-service-principal-for-ad-fs"></a>Créer un principal de service pour AD FS
Si vous avez déployé la pile d’Azure avec AD FS, vous pouvez utiliser PowerShell toocreate un principal de service, attribuez un rôle pour l’accès et de connexion à partir de PowerShell à l’aide de cette identité.

### <a name="before-you-begin"></a>Avant de commencer

[Téléchargez toowork requis de hello outils avec l’ordinateur local de Azure pile tooyour.](azure-stack-powershell-download.md)

### <a name="import-hello-identity-powershell-module"></a>Module PowerShell de l’identité d’importation hello
Après avoir téléchargé les outils hello, accédez toohello téléchargé dossier et d’importation du module PowerShell de l’identité de hello à l’aide de hello de commande suivante :

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

Lorsque vous importez le module de hello, vous pouvez recevoir une erreur indiquant que « AzureStack.Connect.psm1 n’est pas numériquement signé. script de Hello s’exécute pas sur le système de hello ». tooresolve ce problème, vous pouvez définir tooallow de stratégie de l’exécution du script de hello en cours d’exécution avec la commande suivante dans une session PowerShell avec élévation de privilèges de hello :

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-hello-service-principal"></a>Créer hello principal de service
Vous pouvez créer un Principal de Service en exécutant hello suit commande, effectuant que tooupdate hello *DisplayName* paramètre :
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a>Attribuer un rôle
Une fois hello Principal du Service est créé, vous devez [lui attribue le rôle de tooa](azure-stack-create-service-principals.md#assign-role-to-service-principal)

### <a name="sign-in-through-powershell"></a>Se connecter avec PowerShell
Une fois que vous avez affecté un rôle, vous pouvez vous connecter tooAzure pile à l’aide de principal du service hello avec hello de commande suivante :

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-tooservice-principal"></a>Affecter le rôle tooservice principal
tooaccess des ressources dans votre abonnement, vous devez attribuer le rôle de tooa application hello. Décider quel rôle représente les autorisations de droite hello pour une application hello. toolearn sur les rôles disponibles de hello, consultez [RBAC : générées dans les rôles](../active-directory/role-based-access-built-in-roles.md).

Vous pouvez définir l’étendue de hello au niveau hello d’abonnement de hello, groupe de ressources ou ressource. Les autorisations sont héritées toolower des niveaux de portée. Par exemple, ajout d’un rôle de lecteur application toohello pour un groupe de ressources signifie qu’il peut lire toutes les ressources qu’il contient et groupe de ressources hello.

1. Dans le portail Azure pile hello, accédez au niveau du toohello de portée qu'application hello tooassign vous le souhaitez. Par exemple, tooassign un rôle au niveau de l’étendue de l’abonnement hello, sélectionnez **abonnements**. Vous pouvez également sélectionner un groupe de ressources ou une ressource.

2. Sélectionnez un abonnement spécifique (groupe de ressources ou ressource) tooassign hello application hello pour.

     ![sélectionner l’abonnement pour l’affectation](./media/azure-stack-create-service-principal/image16.png)

3. Sélectionnez **Contrôle d’accès (IAM)**.

     ![sélectionner l’accès](./media/azure-stack-create-service-principal/image17.png)

4. Sélectionnez **Ajouter**.

5. Sélectionnez le rôle hello vous souhaitez tooassign toohello application.

6. Recherchez votre application et sélectionnez-la.

7. Sélectionnez **OK** toofinish affectation hello rôle. Vous consultez votre application dans la liste de hello des utilisateurs affectés du rôle tooa pour cette étendue.

Maintenant que vous avez créé un principal de service et affecté un rôle, vous pouvez commencer à l’aide de ce au sein de votre application de tooaccess ressources de la pile de Azure.  

## <a name="next-steps"></a>Étapes suivantes

[Ajouter des utilisateurs pour ADFS](azure-stack-add-users-adfs.md)
[Gérer les autorisations des utilisateurs](azure-stack-manage-permissions.md)