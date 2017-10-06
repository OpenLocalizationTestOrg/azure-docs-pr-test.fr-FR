---
title: aaaCreate autonome compte Azure Automation | Documents Microsoft
description: "Didacticiel qui vous guide à l’aide de la création, le test et exemple hello principal d’authentification de sécurité dans Azure Automation."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 1500d25d9565d4082768933834303a17c5e84234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-azure-automation-account"></a>Création d’un compte Azure Automation autonome
Cette rubrique vous montre comment toocreate un compte Automation à partir de hello portail Azure, si vous souhaitez tooevaluate et que vous découvrez Azure Automation sans inclure les solutions de gestion supplémentaires hello ou intégration à l’Analytique des journaux OMS tooprovide surveillance avancée de tâches de runbook.  Vous pouvez ajouter ces solutions de gestion ou intégrer Analytique de journal à tout moment dans hello futures.  Hello compte Automation, vous êtes runbooks tooauthenticate en mesure de gérer les ressources dans Azure Resource Manager ou d’un déploiement classique Azure.

Lorsque vous créez un compte Automation Bonjour portail Azure, il crée automatiquement :

* Compte d’identification, ce qui crée une nouvelle entité de service dans Azure Active Directory, un certificat, et assigne hello de contrôle d’accès en fonction du rôle de collaborateur (RBAC), qui est utilisé à l’aide de procédures opérationnelles de ressources toomanage Gestionnaire de ressources.   
* Classique compte d’identification en téléchargeant un certificat de gestion, qui est utilisé toomanage classique de ressources à l’aide de procédures opérationnelles.  

Cela simplifie le processus de hello pour vous et vous aide à commencer rapidement à créer et déployer des procédures opérationnelles toosupport votre automatisation a besoin.  

## <a name="permissions-required-toocreate-automation-account"></a>Autorisations toocreate requis compte Automation
toocreate ou mise à jour un compte Automation, vous devez avoir hello suivant des privilèges spécifiques et des autorisations requises toocomplete de cette rubrique.   
 
* Dans l’ordre toocreate un compte Automation, votre compte d’utilisateur Active Directory doit être toobe tooa ajouté rôle rôle de propriétaire de toohello équivalent d’autorisations pour les ressources Microsoft.Automation comme indiqué dans l’article [contrôle d’accès basé sur un rôle dans Azure Automation ](automation-role-based-access-control.md).  
* Si les inscriptions d’application hello paramètre est défini trop**Oui**, les utilisateurs non administrateurs dans votre locataire Azure AD peuvent [inscrire des applications AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Si les inscriptions d’application hello paramètre est défini trop**non**, utilisateur hello effectuer cette action doit être un administrateur global dans Azure AD. 

Si vous n’êtes pas un membre d’instance d’Active Directory de l’abonnement hello avant que vous êtes ajouté toohello global administrateur ou le co-administrateur rôle d’abonnement de hello, vous êtes ajouté tooActive active en tant qu’invité. Dans ce cas, vous recevez un « vous n’avez pas toocreate autorisations... » avertissement sur hello **ajouter un compte Automation** panneau. Les utilisateurs qui ont été ajoutées toohello global administrateur ou le co-administrateur rôle tout d’abord peut être supprimé à partir de l’instance d’Active Directory de l’abonnement hello et a toomake les un utilisateur complète dans Active Directory. tooverify cette situation, hello **Azure Active Directory** volet Bonjour portail Azure, sélectionnez **utilisateurs et groupes**, sélectionnez **tous les utilisateurs** et, après avoir sélectionné hello utilisateur spécifique, sélectionnez **profil**. Hello valeur Hello **type utilisateur** attribut sous le profil de l’utilisateur hello doit être **invité**.

## <a name="create-a-new-automation-account-from-hello-azure-portal"></a>Créer un nouveau compte Automation à partir de hello portail Azure
Dans cette section, effectuer hello suivant les étapes toocreate un compte Azure Automation Bonjour portail Azure.    

1. Se connecter toohello portail Azure avec un compte qui est membre du rôle des administrateurs d’abonnements hello et coadministrateur de l’abonnement de hello.
2. Cliquez sur **Nouveau**.<br><br> ![Sélection de l’option Nouveau dans le portail Azure](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  
3. Recherchez **Automation** et puis Bonjour résultats de recherche sélectionnez **Automation & contrôle***.<br><br> ![Recherche et sélection d’Automation à partir de la Place de marché](media/automation-create-standalone-account/automation-marketplace-select-create-automationacct.png)<br> 
3. Dans le panneau de comptes Automation hello, cliquez sur **ajouter**.<br><br>![Ajouter un compte Automation](media/automation-create-standalone-account/automation-create-automationacct-properties.png)
   
   > [!NOTE]
   > Si vous voyez hello suivant avertissement Bonjour **ajouter un compte Automation** panneau, il est, car votre compte n’est pas membre du rôle des administrateurs d’abonnements hello et co-admin d’abonnement de hello.<br><br>![Avertissement Ajouter un compte Automation](media/automation-create-standalone-account/create-account-without-perms.png)
   > 
   > 
4. Bonjour **ajouter un compte Automation** panneau, Bonjour **nom** tapez un nom pour votre nouveau compte Automation.
5. Si vous avez plusieurs abonnements, spécifiez un nouveau compte de hello, nouveau ou existant **groupe de ressources** et un centre de données Azure **emplacement**.
6. Vérifier la valeur de hello **Oui** est sélectionné pour hello **créer Azure exécuter en tant que compte** , puis cliquez sur hello **créer** bouton.  
   
   > [!NOTE]
   > Si vous choisissez toonot créer le compte d’identification hello en sélectionnant l’option de hello **non**, vous voyez s’afficher un message d’avertissement Bonjour **ajouter un compte Automation** panneau.  Pendant la création de compte de hello Bonjour portail Azure, il ne possède une identité d’authentification correspondant au sein de votre classique ou service d’annuaire abonnement Gestionnaire de ressources et par conséquent, aucune tooresources accès sur votre abonnement.  Cela empêche les runbooks faisant référence à ce compte ne soient pas en mesure de tooauthenticate et effectuer des tâches sur des ressources dans les modèles de déploiement.
   > 
   > ![Avertissement Ajouter un compte Automation](media/automation-create-standalone-account/create-account-decline-create-runas-msg.png)<br>
   > Lorsque le principal du service hello n’est pas créé le rôle de collaborateur hello n’est pas affecté.
   > 

7. Alors que Azure crée le compte d’automatisation hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.

### <a name="resources-included"></a>Ressources incluses
Lorsque hello compte Automation a été créé, plusieurs ressources sont automatiquement créées pour vous.  Hello tableau suivant résume les ressources pour hello compte d’identification.<br>

| Ressource | Description |
| --- | --- |
| Runbook AzureAutomationTutorial |Runbook graphique exemple qui montre comment l’à l’aide de tooauthenticate hello compte d’identification et obtient toutes les ressources du Gestionnaire de ressources hello. |
| Runbook AzureAutomationTutorialScript |Un exemple de runbook PowerShell qui montre comment l’à l’aide de tooauthenticate hello compte d’identification et obtient toutes les ressources du Gestionnaire de ressources hello. |
| AzureRunAsCertificate |Ressource de certificat automatiquement créé lors de la création du compte Automation ou à l’aide du script PowerShell de hello ci-dessous pour un compte existant.  Il vous permet de tooauthenticate avec Azure afin que vous puissiez gérer les ressources Azure Resource Manager à partir de procédures opérationnelles.  Ce certificat a une durée de vie d’un an. |
| AzureRunAsConnection |Ressource de connexion automatiquement créé lors de la création du compte Automation ou à l’aide du script PowerShell de hello ci-dessous pour un compte existant. |

Hello tableau suivant résume les ressources pour hello classique compte d’identification.<br>

| Ressource | Description |
| --- | --- |
| Runbook AzureClassicAutomationTutorial |Exemple graphique de runbook, qui obtient toutes les machines virtuelles classique de hello un abonnement à l’aide de hello classique compte d’identification (certificat), puis exporte l’état et le nom de machine virtuelle hello. |
| Runbook AzureClassicAutomationTutorialScript |Exemple PowerShell de runbook, qui obtient toutes les machines virtuelles classique de hello un abonnement à l’aide de hello classique compte d’identification (certificat), puis exporte l’état et le nom de machine virtuelle hello. |
| AzureClassicRunAsCertificate |Ressource de certificat créé automatiquement qui est utilisée tooauthenticate avec Azure afin que vous puissiez gérer les ressources classiques Azure à partir de procédures opérationnelles.  Ce certificat a une durée de vie d’un an. |
| AzureClassicRunAsConnection |Ressource de connexion automatiquement créée qui est utilisée tooauthenticate avec Azure afin que vous puissiez gérer les ressources classiques Azure à partir de procédures opérationnelles. |


## <a name="next-steps"></a>Étapes suivantes
* toolearn plus sur la création de graphiques, consultez [de création graphique dans Azure Automation](automation-graphical-authoring-intro.md).
* tooget main runbook PowerShell, consultez [mon runbook PowerShell premier](automation-first-runbook-textual-powershell.md).
* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md).
