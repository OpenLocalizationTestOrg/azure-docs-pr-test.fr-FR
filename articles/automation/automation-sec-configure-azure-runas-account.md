---
title: "aaaConfigure une exécution en tant que compte Azure | Documents Microsoft"
description: "Ce didacticiel vous guide à l’aide de la création, le test et exemple hello d’authentification principal de sécurité dans Azure Automation."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: nom du principal du service, setspn, authentification azure
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a>Authentifier des Runbooks avec un compte d’identification Azure
Cet article vous explique comment tooconfigure un Azure Automation compte Bonjour portail Azure. toodo par conséquent, vous utilisez hello exécuter en tant que compte fonctionnalité tooauthenticate runbooks la gestion des ressources dans le Gestionnaire de ressources Azure ou de gestion des services Azure.

Lorsque vous créez un compte Automation Bonjour portail Azure, vous créez automatiquement deux comptes :

* Compte d’identification Azure. Ce compte crée un principal de service dans Azure Active Directory (Azure AD) et un certificat. Il assigne également hello collaborateur basée sur le rôle de contrôle d’accès (RBAC), qui gère les ressources de gestionnaire de ressources à l’aide de procédures opérationnelles.
* Compte d’identification Classic. Ce compte télécharge un certificat de gestion, qui est utilisé toomanage de gestion des services ou des ressources classiques à l’aide de procédures opérationnelles.

Création d’un objet Automation compte simplifie hello pour vous et vous aide à que commencer rapidement générer et déployer des procédures opérationnelles toosupport votre automatisation a besoin.

À l’aide de comptes d’identification standard ou Classic, vous pouvez :

* Fournir une méthode standardisée de tooauthenticate avec Azure lorsque vous gérez le Gestionnaire de ressources ou des ressources de gestion de Service à partir de procédures opérationnelles Bonjour portail Azure.
* Automatisez l’utilisation de hello des procédures opérationnelles globales, vous pouvez les configurer dans Azure Alerts.

> [!NOTE]
> Hello [fonctionnalité d’intégration Azure alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) avec l’Automation des procédures opérationnelles globales nécessite un compte Automation est configuré avec un compte d’identification et classique compte d’identification. Vous pouvez sélectionner un compte Automation a déjà défini des comptes d’identification et Classic exécuter en tant que, ou vous pouvez choisir toocreate un compte Automation.
>  

Cet article explique comment toocreate un compte Automation à partir de hello portail Azure, mettre à jour un compte Automation à l’aide d’Azure PowerShell, gérer la configuration de compte hello et s’authentifier dans vos runbook.

Avant de commencer la création d’un compte Automation, elle est une bonne idée toounderstand et tenez compte hello qui suit :

* Création d’un compte Automation n’affecte pas les comptes Automation que vous avez peut-être déjà créé dans hello classique ou modèle de déploiement de gestionnaire de ressources.
* processus de Hello fonctionne uniquement pour les comptes Automation que vous créez dans hello portail Azure. Tentative de toocreate un compte à partir de hello portail Azure classic ne réplique pas hello exécuter en tant que compte configuration.
* Si vous avez déjà des procédures opérationnelles et ressources (telles que des planifications ou des variables) dans toomanage place les ressources classiques, et vous souhaitez tooauthenticate runbooks avec hello classique compte d’identification, procéder de hello suivantes :

  * toocreate classique compte d’identification, suivez les instructions de hello dans la section « Gestion de votre compte d’identification » de hello. 
  * votre compte existant, utilisez hello PowerShell tooupdate un script dans la section « Mise à jour de votre compte Automation à l’aide de PowerShell » de hello.
* tooauthenticate à l’aide de hello nouveau compte d’identification et compte classique exécuter en tant que Automation, vous devez toomodify vos runbooks existants avec hello l’exemple de code fourni dans la section de hello [exemples de code d’authentification](#authentication-code-examples).

    >[!NOTE]
    >Exécuter en tant que compte de Hello est pour l’authentification par rapport aux ressources du Gestionnaire de ressources à l’aide de principal du service de basée sur certificat hello. est de Hello classique compte d’identification pour s’authentifier auprès des ressources de gestion de Service avec un certificat de gestion.

## <a name="create-an-automation-account-from-hello-azure-portal"></a>Créer un compte Automation à partir de hello portail Azure
Dans cette section, vous créer un compte Azure Automation à partir de hello portail Azure, qui crée ensuite un compte d’identification et classique compte d’identification.

>[!NOTE]
>toocreate un compte Automation, vous devez être membre du rôle des administrateurs de Service hello ou coadministrateur de l’abonnement hello qui accorde l’accès toohello abonnement. Vous devez également être ajouté en tant qu’instance d’Active Directory d’un abonnement toothat utilisateur par défaut. compte de Hello n’a pas besoin toobe affecté un rôle privilégié.
>
>Si vous n’êtes pas un membre d’instance d’Active Directory de l’abonnement hello avant que vous êtes ajouté le rôle de coadministrateur toohello d’abonnement de hello, vous ajouterez tooActive active en tant qu’invité. Dans ce cas, vous recevrez un « vous n’avez pas toocreate autorisations... » avertissement sur hello **ajouter un compte Automation** panneau.
>
>Les utilisateurs qui ont été ajoutés tout d’abord, rôle de coadministrateur toohello peut être supprimé de l’instance d’Active Directory de l’abonnement hello et rajouté toomake les un utilisateur complète dans Active Directory. tooverify cette situation hello **Azure Active Directory** volet Bonjour portail Azure en sélectionnant **utilisateurs et groupes**, en sélectionnant **tous les utilisateurs** et, après avoir sélectionné utilisateur spécifique de Hello, en sélectionnant **profil**. Hello valeur Hello **type utilisateur** attribut sous le profil de l’utilisateur hello doit être **invité**.
>

1. Connectez-vous toohello portail Azure avec un compte qui est membre du rôle Administrateurs d’abonnement hello et coadministrateur de l’abonnement de hello.

2. Sélectionnez **Comptes Automation**.

3. Sur hello **comptes Automation** panneau, cliquez sur **ajouter**.
Hello **ajouter un compte Automation** panneau s’ouvre.

 ![panneau de « Ajouter un compte Automation » Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > Si votre compte n’est pas membre du rôle Administrateurs d’abonnement aux hello et coadministrateur de l’abonnement de hello, hello suivant d’avertissement s’affiche sur hello **ajouter un compte Automation** panneau :
   >
   >![Avertissement Ajouter un compte Automation](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. Sur hello **ajouter un compte Automation** panneau, Bonjour **nom** , tapez un nom pour votre nouveau compte Automation.

5. Si vous avez plusieurs abonnements, procédez comme hello suivant :

    a. Sous **abonnement**, spécifiez un nouveau compte de hello.

    b. Sous **Groupe de ressources**, cliquez sur **Créer** ou **Utiliser l’existant**.

    c. Sous **Emplacement**, indiquez un centre de données Azure.

6. Sous **Créer un compte d’identification Azure**, sélectionnez **Oui**, puis cliquez sur **Créer**.

   > [!NOTE]
   > Si vous ne choisissez pas toocreate hello compte d’identification en sélectionnant **non**, un message d’avertissement s’affiche hello **ajouter un compte Automation** panneau. Bien que le compte de hello est créé dans hello portail Azure, il n’a pas une identité d’authentification correspondant au sein de votre classique ou le service d’annuaire abonnement Gestionnaire de ressources. En conséquence, le compte de hello n’a aucune tooresources d’accès dans votre abonnement. Ce scénario empêche tous les Runbooks faisant référence à ce compte de pouvoir s’authentifier et d’effectuer des tâches sur les ressources de ces modèles de déploiement.
   >
   > ![Message d’avertissement sur le panneau de « Ajouter un compte Automation » hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > En outre, étant donné que le principal du service hello n’est pas créée, rôle de collaborateur hello n’est pas affecté.
   >

7. Alors que Azure crée le compte d’automatisation hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.

### <a name="resources"></a>Ressources
Lorsque hello compte Automation a été créé, plusieurs ressources sont automatiquement créées pour vous. ressources de Hello sont résumées dans hello les deux tableaux suivants :

#### <a name="run-as-account-resources"></a>Ressources de compte d’identification

| Ressource | Description |
| --- | --- |
| Runbook AzureAutomationTutorial | Runbook graphique exemple qui montre comment tooauthenticate à l’aide de hello compte d’identification et obtient toutes les ressources du Gestionnaire de ressources hello. |
| Runbook AzureAutomationTutorialScript | Un exemple de runbook PowerShell qui montre comment tooauthenticate à l’aide de hello compte d’identification et obtient toutes les ressources du Gestionnaire de ressources hello. |
| AzureRunAsCertificate | ressource de certificat Hello qui est créé automatiquement lorsque vous créez un compte Automation ou que vous utilisez hello suite du script PowerShell pour un compte existant. certificat de Hello vous permet de tooauthenticate avec Azure afin que vous puissiez gérer les ressources Azure Resource Manager à partir de procédures opérationnelles. certificat de Hello a une durée de vie d’un an. |
| AzureRunAsConnection | ressource de connexion Hello qui est créé automatiquement lorsque vous créez un compte Automation ou utilisez un script PowerShell de hello pour un compte existant. |

#### <a name="classic-run-as-account-resources"></a>Ressources de compte d’identification Classic

| Ressource | Description |
| --- | --- |
| Runbook AzureClassicAutomationTutorial | Exemple de runbook graphique qui obtient tous les ordinateurs virtuels de hello qui sont créés à l’aide du modèle de déploiement classique hello dans un abonnement à l’aide de hello classique compte d’identification (certificat), puis écrit l’état et le nom de machine virtuelle hello. |
| Runbook AzureClassicAutomationTutorialScript | Exemple de runbook PowerShell qui obtient tous les hello classiques machines virtuelles dans un abonnement à l’aide de hello classique compte d’identification (certificat), puis écritures hello état et le nom de la machine virtuelle. |
| AzureClassicRunAsCertificate | ressource de certificat Hello créé automatiquement utiliser tooauthenticate avec Azure afin que vous puissiez gérer les ressources classiques Azure à partir de procédures opérationnelles. certificat de Hello a une durée de vie d’un an. |
| AzureClassicRunAsConnection | ressource de connexion créés automatiquement de Hello utiliser tooauthenticate avec Azure afin que vous puissiez gérer les ressources classiques Azure à partir de procédures opérationnelles. |

## <a name="verify-run-as-authentication"></a>Vérifier l’authentification d’identification
Effectuer un tooconfirm de test peu que vous pouvez vous authentifier avec succès à l’aide de hello nouveau compte d’identification.

1. Bonjour portail Azure, ouvrez le compte Automation hello que vous avez créé précédemment.

2. Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.

3. Sélectionnez hello **AzureAutomationTutorialScript** runbook, puis cliquez sur **Démarrer** toostart hello runbook. Hello suivant des événements se produire :
 * A [tâche du runbook](automation-runbook-execution.md) est créé, hello **travail** panneau s’affiche, et état de la tâche hello est affiché dans hello **récapitulatif** vignette.
 * état de la tâche Hello commence en tant que **en file d’attente**, indiquant qu’il est en attente d’un runbook worker dans hello toobecome de cloud disponible.
 * l’état de Hello devient **départ** lorsqu’un travailleur de revendications travail de hello.
 * l’état de Hello devient **en cours d’exécution** lorsque hello runbook démarre l’exécution.
 * Lors de la tâche du runbook hello est terminée, vous devez voir un état de **terminé**.

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. toosee hello les résultats détaillés de hello runbook, cliquez sur hello **sortie** vignette.  
Hello **sortie** panneau s’affiche, indiquant que runbook hello a authentifié et a renvoyé une liste de toutes les ressources disponibles dans le groupe de ressources hello.

5. Fermer hello **sortie** panneau tooreturn toohello **récapitulatif** panneau.

6. Fermer hello **récapitulatif** lame et hello correspondant **AzureAutomationTutorialScript** panneau runbook.

## <a name="verify-classic-run-as-authentication"></a>Vérifier l’authentification d’identification Classic
Effectuer un petit semblables tests tooconfirm que vous pouvez vous authentifier avec succès à l’aide de hello classique compte d’identification.

1. Bonjour portail Azure, ouvrez le compte Automation hello que vous avez créé précédemment.

2. Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.

3. Sélectionnez hello **AzureClassicAutomationTutorialScript** runbook, puis cliquez sur **Démarrer** trop démarrer hello runbook. Hello suivant des événements se produire :

 * A [tâche du runbook](automation-runbook-execution.md) est créé, hello **travail** panneau s’affiche, et état de la tâche hello est affiché dans hello **récapitulatif** vignette.
 * état de la tâche Hello commence en tant que **en file d’attente**, indiquant qu’il est en attente d’un runbook worker dans hello toobecome de cloud disponible.
 * l’état de Hello devient **départ** lorsqu’un travailleur de revendications travail de hello.
 * l’état de Hello devient **en cours d’exécution** lorsque hello runbook démarre l’exécution.
 * Lors de la tâche du runbook hello est terminée, vous devez voir un état de **terminé**.

    ![Test de Runbook du principal de sécurité](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. toosee hello les résultats détaillés de hello runbook, cliquez sur hello **sortie** vignette.  
Hello **sortie** panneau s’affiche, indiquant que runbook hello a authentifié et retourné une liste de toutes les machines virtuelles classiques dans l’abonnement de hello.

5. Fermer hello **sortie** panneau tooreturn toohello **récapitulatif** panneau.

6. Fermer hello **récapitulatif** lame et hello correspondant **AzureAutomationTutorialScript** panneau runbook.

## <a name="managing-your-run-as-account"></a>Gestion de votre compte d’identification
À un moment donné avant l’expiration de votre compte Automation, vous devez le certificat de hello toorenew. Si vous pensez que ce compte d’identification hello a été compromise, vous pouvez supprimer et recréer. Cette section explique comment tooperform ces opérations.

### <a name="self-signed-certificate-renewal"></a>Renouvellement de certificat auto-signé
Hello un certificat auto-signé que vous avez créé pour hello exécuter en tant que compte expire un an à partir de la date de hello de création. Vous pouvez le renouveler à tout moment avant qu’il n’expire. Lors du renouvellement, il certificat valide de hello actuelle est retenue tooensure que les runbooks qui sont en attente jusqu'à ou activement en cours d’exécution, et qui s’authentifient avec hello compte d’identification, ne sont pas affectés négativement. certificat de Hello reste valide jusqu'à ce que sa date d’expiration.

> [!NOTE]
> Si vous avez configuré votre toouse de compte Automation s’exécuter en tant qu’un certificat émis par votre autorité de certification d’entreprise et que vous utilisez cette option, le certificat d’entreprise hello est remplacé par un certificat auto-signé.

toorenew hello certificat, procédez comme hello suivant :

1. Bonjour portail Azure, ouvrez le compte Automation de hello.

2. Sur hello **compte Automation** panneau, Bonjour **compte propriétés** volet, sous **les paramètres de compte**, sélectionnez **exécuter en tant que comptes**.

    ![Panneau des propriétés du compte Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. Sur hello **comptes d’identification** panneau des propriétés, sélectionnez soit hello d’identification de compte ou hello classique exécuter en tant que compte de certificat de hello toorenew pour.

4. Sur hello **propriétés** panneau pourquoi le compte sélectionné, cliquez sur **renouveler certificat**.

    ![Renouveler le certificat pour le compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. Pendant le renouvellement de certificat de hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.

### <a name="delete-a-run-as-or-classic-run-as-account"></a>Supprimer un compte d’identification standard ou Classic
Cette section décrit comment toodelete et recréer un compte d’identification ou classique exécuter en tant que. Lorsque vous effectuez cette action, hello compte Automation est conservée. Après avoir supprimé un compte d’identification ou classique exécuter en tant que, vous pouvez le recréer dans hello portail Azure.

1. Bonjour portail Azure, ouvrez le compte Automation de hello.

2. Sur hello **compte Automation** lame, hello compte volet Propriétés, sélectionnez **exécuter en tant que comptes**.

3. Sur hello **comptes d’identification** panneau des propriétés, sélectionnez soit hello d’identification de compte ou classique exécuter en tant que le compte que vous souhaitez toodelete. Ensuite, sous hello **propriétés** panneau pourquoi le compte sélectionné, cliquez sur **supprimer**.

 ![Supprimer un compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. Lors de la suppression du compte de hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.

5. Une fois que le compte de hello a été supprimé, vous pouvez recréer il sur hello **comptes d’identification** option de création du panneau des propriétés en sélectionnant hello **exécuter en tant que compte Azure**.

 ![Recréez le compte d’identification Automation hello](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a>Configuration incorrecte
Certains éléments de configuration nécessaires pour toofunction de compte Exécuter en tant qu’ou classique en hello peuvent correctement ont été supprimés ou créés correctement lors de l’installation initiale. éléments de Hello sont les suivantes :

* Ressource de certificat
* Ressource de connexion
* Compte d’identification a été supprimé de rôle de collaborateur hello
* Principal du service ou application dans Azure AD

Hello précédent et les autres instances d’une configuration incorrecte, hello compte Automation détecte hello modifie et affiche l’état *incomplet* sur hello **comptes d’identification** panneau des propriétés pour hello compte.

![État Incomplet pour la configuration du compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

Lorsque vous sélectionnez le compte d’identification hello, hello compte **propriétés** volet affiche hello message d’erreur suivant :

![Message d’avertissement Incomplet pour la configuration du compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png).

Vous pouvez rapidement résoudre ces problèmes de compte Exécuter en tant qu’à supprimer et recréer le compte de hello.

## <a name="update-your-automation-account-by-using-powershell"></a>Mise à jour de votre compte Automation à l’aide de PowerShell
Vous pouvez utiliser PowerShell tooupdate votre compte Automation existant si :

* Vous créez un compte Automation mais refusez toocreate hello exécuter en tant que compte.
* Vous utilisez déjà une ressources de gestionnaire de ressources toomanage compte Automation et que vous souhaitez tooupdate hello tooinclude hello exécuter en tant que compte pour l’authentification de runbook.
* Vous utilisez déjà une Automation compte toomanage les ressources classiques et tooupdate il toouse hello classique compte d’identification au lieu de créer un compte et la migration de votre tooit runbooks et ressources.   
* Vous souhaitez que toocreate une identification et classique compte d’identification à l’aide d’un certificat émis par votre autorité de certification d’entreprise (CA).

script de Hello a hello suivant des conditions préalables :

* script de Hello peut exécuter uniquement sur Windows 10 et Windows Server 2016 avec des modules Azure Resource Manager 2.01 et versions ultérieures. Il n’est pas pris en charge dans les versions antérieures de Windows.
* Azure PowerShell 1.0 et versions ultérieures. Pour plus d’informations sur la mise en production hello PowerShell 1.0, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
* Un compte Automation, qui est référencé en tant que valeur hello pour hello *– AutomationAccountName* et *- ApplicationDisplayName* paramètres Bonjour suite du script PowerShell.

les valeurs tooget hello pour *SubscriptionID*, *ResourceGroup*, et *AutomationAccountName*, qui sont des paramètres requis pour les scripts de hello, procédez comme hello suivant :
1. Dans l’hello portail Azure, sélectionnez votre compte Automation sur hello **compte Automation** panneau, puis sélectionnez **tous les paramètres**. 
2. Sur hello **tous les paramètres** panneau, sous **les paramètres de compte**, sélectionnez **propriétés**. 
3. Notez les valeurs hello sur hello **propriétés** panneau.

![Panneau de Hello Automation compte « Propriétés »](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a>Créer le script PowerShell d’un compte d’identification
Ce script PowerShell prend en charge hello suivant configurations :

* Créez un compte d’identification à l’aide d’un certificat auto-signé.
* Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé.
* Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise.
* Créer un compte d’identification et classique compte d’identification à l’aide d’un certificat auto-signé Bonjour cloud d’Azure Government.

En fonction de l’option de configuration hello sélectionnée, le script de hello crée hello éléments suivants.

**Pour les comptes d’identification :**

* Crée un Azure AD application toobe exporté avec soit hello auto-signé ou clé publique du certificat enterprise, crée un compte de principal du service pour l’application hello dans Azure AD, et assigne hello compte hello dans votre rôle de collaborateur abonnement. Vous pouvez modifier ce paramètre tooOwner ou tout autre rôle. Pour plus d’informations, voir [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).
* Crée une ressource de certificat Automation nommée *AzureRunAsCertificate* Bonjour spécifié le compte Automation. ressource de certificat Hello conserve la clé privée hello certificat utilisé par l’application hello Azure AD.
* Crée une ressource de connexion d’Automation nommée *AzureRunAsConnection* Bonjour spécifié le compte Automation. ressource de connexion Hello conserve hello applicationId, tenantId, ID d’abonnement et l’empreinte numérique du certificat.

**Pour les comptes d’identification Classic :**

* Crée une ressource de certificat Automation nommée *AzureClassicRunAsCertificate* Bonjour spécifié le compte Automation. ressource de certificat Hello conserve la clé privée du certificat hello utilisé par le certificat de gestion hello.
* Crée une ressource de connexion d’Automation nommée *AzureClassicRunAsConnection* Bonjour spécifié le compte Automation. ressource de connexion Hello conserve hello abonnement nom, ID d’abonnement et nom de ressource de certificat.

>[!NOTE]
> Si vous sélectionnez l’option de création d’un compte classique exécuter en tant qu’après l’exécution de script de hello, téléchargement hello publique magasin de certificats de gestion de toohello (extension de nom de fichier .cer) pour l’abonnement de hello que hello compte Automation a été créé dans.
> 

tooexecute hello script et télécharger le certificat de hello, hello suivant :

1. Enregistrez hello script suivant sur votre ordinateur. Dans cet exemple, enregistrez-le sous le nom de fichier hello *New-RunAsAccount.ps1*.

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. Sur votre ordinateur, cliquez sur **Démarrer**, puis démarrez **Windows PowerShell** avec des droits de l’utilisateur élevés.

3. À partir de hello élevé PowerShell interpréteur de commandes, accédez toohello dossier qui contient le script hello créé à l’étape 1.

4. Exécuter le script de hello à l’aide des valeurs de paramètre hello pour configuration hello que vous avez besoin.

    **Créer un compte d’identification à l’aide d’un certificat auto-signé**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Créer un compte d’identification et classique compte d’identification à l’aide d’un certificat auto-signé Bonjour cloud d’Azure Government**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Après l’exécution de script de hello, vous serez invité à tooauthenticate avec Azure. Connectez-vous avec un compte qui est membre du rôle Administrateurs d’abonnement hello et coadministrateur de l’abonnement de hello.
    >
    >

Une fois le script de hello a été exécutée correctement, notez hello qui suit :
* Si vous avez créé un classique compte d’identification avec un certificat auto-signé de public (fichier .cer), le script de hello crée et enregistre toohello dossier des fichiers temporaires sur votre ordinateur sous le profil utilisateur hello *%USERPROFILE%\AppData\Local\Temp*, que vous avez utilisé la session de PowerShell tooexecute hello.
* Si vous avez créé un compte d’identification Classic avec un certificat public d’entreprise (fichier .cer), utilisez ce certificat. Suivez les instructions de hello pour [téléchargement un toohello de certificat d’API de gestion portail Azure classic](../azure-api-management-certs.md), puis validez de configuration des informations d’identification hello avec les ressources de gestion des services à l’aide de hello [exemple de code tooauthenticate avec le Service de gestion des ressources](#sample-code-to-authenticate-with-service-management-resources). 
* Si vous l’avez fait *pas* créer classique compte d’identification, de s’authentifier auprès des ressources du Gestionnaire de ressources et de valider la configuration des informations d’identification hello à l’aide de hello [exemple de code pour s’authentifier auprès de gestion des services ressources](#sample-code-to-authenticate-with-resource-manager-resources).

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a>Tooauthenticate de code d’exemple avec des ressources du Gestionnaire de ressources
Vous pouvez utiliser suivante hello mis à jour exemple de code, obtenue à partir de hello *AzureAutomationTutorialScript* exemple de runbook, tooauthenticate à l’aide des ressources de gestionnaire de ressources de toomanage hello exécuter en tant que compte avec les procédures opérationnelles.

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

toohelp vous tooeasily de travail entre plusieurs abonnements, script de hello inclut deux lignes supplémentaires de code qui prennent en charge le référencement d’un contexte de l’abonnement. Une ressource de variable nommée *SubscriptionId* contient hello des ID d’abonnement de hello. Après avoir hello `Add-AzureRmAccount` instruction de l’applet de commande, hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) applet de commande est établi avec le jeu de paramètres hello *- SubscriptionId*. Si le nom de la variable hello est trop générique, vous pouvez réviser tooinclude un préfixe ou utiliser un autre toomake de convention d’affectation de noms il tooidentify plus facile. Vous pouvez également utiliser le jeu de paramètres hello *- SubscriptionName* au lieu de *- SubscriptionId* avec une ressource de variable correspondante.

Hello applet de commande que vous utilisez pour l’authentification dans les runbook hello, `Add-AzureRmAccount`, utilise hello *ServicePrincipalCertificate* jeu de paramètres. Il s’authentifie à l’aide du certificat hello service principal, pas hello informations d’identification.

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a>Tooauthenticate de code d’exemple avec les ressources de gestion des services
Vous pouvez utiliser hello après mise à jour des exemples de code provient de hello *AzureClassicAutomationTutorialScript* exemple de runbook, tooauthenticate à l’aide de hello classique exécuter en tant que compte toomanage ressources classiques avec votre procédures opérationnelles.

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a>Étapes suivantes
* [Objets application et principal du service dans Azure AD](../active-directory/active-directory-application-objects.md)
* [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md)
* [Vue d’ensemble des certificats pour Azure Cloud Services](../cloud-services/cloud-services-certs-create.md)
