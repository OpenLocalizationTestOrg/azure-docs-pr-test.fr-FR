---
title: "contrôle d’accès aaaRole dans Azure Automation | Documents Microsoft"
description: "Le contrôle d’accès en fonction du rôle (RBAC) permet de gérer les accès des ressources Azure. Cet article décrit comment tooset de RBAC dans Azure Automation."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "rbac automation, contrôle d’accès en fonction du rôle, azure rbac"
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Contrôle d’accès en fonction du rôle dans Azure Automation
## <a name="role-based-access-control"></a>Contrôle d’accès en fonction du rôle
Le contrôle d’accès en fonction du rôle (RBAC) permet de gérer les accès des ressources Azure. À l’aide de [RBAC](../active-directory/role-based-access-control-configure.md), vous pouvez séparer les droits au sein de votre équipe et grant hello uniquement la quantité toousers d’accès, les groupes et les applications dont ils ont besoin tooperform leur travail. Accès en fonction du rôle peuvent être accordé toousers à l’aide de hello portail Azure, les outils de ligne de commande Azure ou les API de gestion Azure.

## <a name="rbac-in-automation-accounts"></a>RBAC dans les comptes Automation
Dans Azure Automation, l’accès est accordé en assignant hello toousers du rôle RBAC approprié, les groupes et les applications hello étendue du compte Automation. Suivantes sont hello rôles intégrés pris en charge par un compte Automation :  

| **Rôle** | **Description** |
|:--- |:--- |
| Propriétaire |rôle de propriétaire Hello permet tooall d’accéder aux ressources et les actions au sein d’un compte Automation en fournissant aussi accès tooother utilisateurs, groupes et applications toomanage hello compte Automation. |
| Collaborateur |rôle de collaborateur Hello vous permet de toomanage tout sauf la modification d’un autre utilisateur compte Automation de tooan autorisations d’accès. |
| Lecteur |rôle de lecteur Hello vous permet de tooview toutes les ressources hello dans un objet Automation compte mais ne peuvent pas apporter de modifications. |
| Opérateur Automation |rôle d’opérateur de Automation Hello vous permet de tooperform les tâches opérationnelles telles que Démarrer, arrêter, suspendre, reprendre et planifier des travaux. Ce rôle est utile si vous souhaitez que tooprotect vos ressources de compte Automation comme ressources d’informations d’identification et les runbooks d’être affichés ou modifiés, mais autoriser les membres de votre organisation de tooexecute ces procédures opérationnelles. |
| Administrateur de l'accès utilisateur |rôle d’administrateur de l’accès utilisateur Hello vous permet des comptes Automation tooAzure toomanage utilisateur accès. |

> [!NOTE]
> Vous ne pouvez pas accorder d’accès droits tooa spécifiques ou des runbook, que des ressources de toohello et des actions dans hello compte Automation.  
> 
> 

Dans cet article nous aideront vous tooset des RBAC dans Azure Automation. Mais tout d’abord, nous allons prendre plus en détail examiner hello des autorisations individuelles accordées toohello collaborateur, lecteur, l’opérateur d’Automation et administrateur de l’accès utilisateur afin que nous avons une bonne compréhension avant l’octroi de toute personne droits compte Automation de toohello.  Dans le cas contraire, les conséquences risquent d’être inattendues ou indésirables.     

## <a name="contributor-role-permissions"></a>Autorisations du rôle Collaborateur
Hello tableau suivant présente les actions spécifiques hello qui peuvent être effectuées par le rôle de collaborateur hello dans Automation.

| **Type de ressource** | **Lire** | **Écrire** | **Supprimer** | **Autres actions** |
|:--- |:--- |:--- |:--- |:--- |
| Compte Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |
| Ressource de certificat Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |
| Ressource de connexion Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |
| Ressource de type de connexion Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |
| Ressource d'identification Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |
| Ressource de planification Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |
| Ressource variable Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |
| Configuration de l’état souhaité Automation | | | |![État vert](media/automation-role-based-access-control/green-checkmark.png) |
| Type de ressource du Runbook Worker hybride |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |
| Travail Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |![État vert](media/automation-role-based-access-control/green-checkmark.png) |
| Flux de travail Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Planification du travail Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |
| Module Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |
| Runbook Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |
| Brouillon de Runbook Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | |![État vert](media/automation-role-based-access-control/green-checkmark.png) |
| Travail de test de brouillon de Runbook Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |![État vert](media/automation-role-based-access-control/green-checkmark.png) |
| Webhook Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>Autorisations du rôle Lecteur
Hello tableau suivant présente les actions spécifiques hello qui peuvent être effectuées par le rôle de lecteur hello dans Automation.

| **Type de ressource** | **Lire** | **Écrire** | **Supprimer** | **Autres actions** |
|:--- |:--- |:--- |:--- |:--- |
| Administrateur d’abonnements classiques |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Verrou de gestion |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Autorisation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Opérations de fournisseur |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Affectation de rôle |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Définition de rôle |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>Autorisations du rôle Opérateur Automation
Hello tableau suivant présente les actions spécifiques hello qui peuvent être effectuées par le rôle d’opérateur de Automation hello dans Automation.

| **Type de ressource** | **Lire** | **Écrire** | **Supprimer** | **Autres actions** |
|:--- |:--- |:--- |:--- |:--- |
| Compte Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ressource de certificat Automation | | | | |
| Ressource de connexion Automation | | | | |
| Ressource de type de connexion Azure Automation | | | | |
| Ressource d'identification Automation | | | | |
| Ressource de planification Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | |
| Ressource variable Automation | | | | |
| Configuration de l’état souhaité Automation | | | | |
| Type de ressource du Runbook Worker hybride | | | | |
| Travail Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | |![État vert](media/automation-role-based-access-control/green-checkmark.png) |
| Flux de travail Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Planification du travail Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | |
| Module Automation | | | | |
| Runbook Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Brouillon de Runbook Automation | | | | |
| Travail de test de brouillon de Runbook Automation | | | | |
| Webhook Automation | | | | |

Pour plus d’informations, hello [actions de l’opérateur Automation](../active-directory/role-based-access-built-in-roles.md#automation-operator) listes hello prises en charge par le rôle d’opérateur Automation hello sur le compte d’automatisation hello et ses ressources.

## <a name="user-access-administrator-role-permissions"></a>Autorisations du rôle Administrateur de l’accès utilisateur
Hello tableau suivant présente les actions spécifiques hello qui peuvent être effectuées par le rôle d’administrateur de l’accès utilisateur hello dans Automation.

| **Type de ressource** | **Lire** | **Écrire** | **Supprimer** | **Autres actions** |
|:--- |:--- |:--- |:--- |:--- |
| Compte Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ressource de certificat Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ressource de connexion Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ressource de type de connexion Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ressource d'identification Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ressource de planification Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ressource variable Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Configuration de l’état souhaité Automation | | | | |
| Type de ressource du Runbook Worker hybride |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Travail Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Flux de travail Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Planification du travail Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Module Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Runbook Azure Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Brouillon de Runbook Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Travail de test de brouillon de Runbook Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Webhook Automation |![État vert](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>Configurer RBAC pour votre compte Automation à l’aide du portail Azure
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) et ouvrez votre compte Automation à partir du Panneau de comptes Automation hello.  
2. Cliquez sur hello **accès** contrôle hello coin supérieur droit. Cette opération ouvre hello **utilisateurs** panneau où vous pouvez ajouter nouvelle toomanage d’utilisateurs, des groupes et des applications de votre compte Automation et afficher les rôles existants qui peuvent être configurées pour hello compte Automation.  
   
   ![Bouton Accéder](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **Les administrateurs d’abonnements** existe déjà en tant qu’utilisateur par défaut de hello. groupe de Hello abonnement administrateurs Active Directory inclut les administrateurs de service hello et co-administrator(s) pour votre abonnement Azure. Hello Service admin est propriétaire de hello de votre abonnement Azure et ses ressources, et est ont rôle de propriétaire hello héritées pour les comptes automation hello trop. Cela signifie que l’accès de hello est **Inherited** pour **administrateurs et coadministrateurs du service** d’un abonnement et **affecté** pour tous les hello d’autres utilisateurs. Cliquez sur **administrateurs d’abonnements** tooview plus d’informations sur leurs autorisations.  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>Ajouter un nouvel utilisateur et affecter un rôle
1. Dans le panneau des utilisateurs hello, cliquez sur **ajouter** tooopen hello **panneau d’accès ajouter** où vous pouvez ajouter un utilisateur, un groupe ou une application et affecter un toothem de rôle.  
   
   ![Ajouter un utilisateur](media/automation-role-based-access-control/automation-02-add-user.png)  
2. Sélectionnez un rôle à partir de la liste de hello des rôles disponibles. Nous allons choisir hello **lecteur** rôle, mais vous pouvez choisir tout hello disponible rôles intégrés prenant en charge un compte Automation ou n’importe quel rôle personnalisé définie.  
   
   ![Sélectionner un rôle](media/automation-role-based-access-control/automation-03-select-role.png)  
3. Cliquez sur **ajouter des utilisateurs** tooopen hello **ajouter des utilisateurs** panneau. Si vous avez ajouté les toomanage les utilisateurs, groupes ou applications votre abonnement puis ces utilisateurs sont répertoriés et vous pouvez les sélectionner tooadd accès. S’il n’existe pas tous les utilisateurs répertoriés, ou si l’utilisateur hello vous êtes intéressé par l’ajout n’est pas répertorié puis cliquez sur **inviter** tooopen hello **inviter un invité** panneau, où vous pouvez inviter un utilisateur avec un compte Microsoft valide adresse de messagerie tels que Outlook.com, OneDrive ou Xbox Live ID. Une fois que vous avez entré l’adresse de messagerie hello d’utilisateur de hello, cliquez sur **sélectionnez** tooadd hello utilisateur, puis cliquez sur **OK**. 
   
   ![Ajouter des utilisateurs](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   Maintenant vous devriez voir utilisateur hello ajouté toohello **utilisateurs** panneau avec hello **lecteur** rôle attribué.  
   
   ![Répertorier les utilisateurs](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   Vous pouvez également assigner un utilisateur toohello rôle hello **rôles** panneau. 
4. Cliquez sur **rôles** de Bonjour utilisateurs panneau tooopen Bonjour **Panneau de rôles**. À partir de ce panneau, vous pouvez afficher le nom hello du rôle hello, nombre hello des utilisateurs et groupes toothat de rôle.
   
    ![Affecter un rôle à partir du panneau Utilisateurs](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > Contrôle d’accès basé sur le rôle peut uniquement être défini au hello au niveau du compte Automation et pas dans n’importe quelle ressource ci-dessous hello compte Automation.
   > 
   > 
   
    Vous pouvez attribuer plusieurs rôles tooa utilisateur, groupe ou application. Par exemple, si nous ajoutons hello **Automation opérateur** rôle ainsi que de hello **rôle Lecteur** toohello utilisateur, puis ils peuvent afficher toutes les ressources d’automatisation hello, ainsi qu’exécuter les travaux de runbook hello. Vous pouvez développer hello déroulante tooview une liste des rôles attribués toohello utilisateur.  
   
    ![Afficher plusieurs rôles](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>Supprimer un utilisateur
Vous pouvez supprimer l’autorisation d’accès pour un utilisateur qui n’est pas la gestion hello compte Automation, ou qui ne fonctionne plus pour l’organisation de hello hello. Suivantes sont hello étapes tooremove un utilisateur : 

1. À partir de hello **utilisateurs** panneau, l’attribution de rôle hello select que vous souhaitez tooremove.
2. Cliquez sur hello **supprimer** bouton dans le panneau de détails de l’attribution de hello.
3. Cliquez sur **Oui** tooconfirm suppression. 
   
   ![Supprimer des utilisateurs](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>Utilisateur affecté à un rôle
Lorsqu’un rôle d’utilisateur attribué tooa tootheir compte Automation se connecte, ils peuvent maintenant voir compte du propriétaire hello répertorié dans la liste des hello **par défaut des répertoires**. Bonjour tooview de l’ordre qu’ils ont été ajoutés au compte d’automatisation, ils doivent basculer active de valeur par défaut du propriétaire toohello hello par défaut active.  

![Annuaire par défaut](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>Expérience utilisateur pour le rôle d’opérateur Automation
Lorsqu’un utilisateur, qui est assignée vues de rôle d’opérateur d’Automation toohello compte Automation de hello à qu'ils sont attribués, ils peuvent uniquement afficher de la liste de hello des procédures opérationnelles, les planifications et les travaux créés dans hello compte Automation, mais ne peut pas afficher leur définition. Ils peuvent démarrer, arrêter, suspendre, reprendre ou planifier la tâche du runbook hello. utilisateur de Hello n’aura pas accès tooother Automation ressources telles que des configurations, des groupes de travail hybride ou de nœuds DSC.  

![Aucun tooresourcres d’accès](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

Lorsque l’utilisateur de hello clique sur hello runbook, hello commandes tooview hello source ou modifier les runbook hello ne sont pas fournies comme rôle d’opérateur hello Automation n’autorise pas l’accès toothem.  

![Aucun runbook de tooedit d’accès](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

utilisateur de Hello ont accès les planifications tooview et toocreate mais pas aura accès tooany autre type de ressource.  

![Aucun tooassets d’accès](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

Cet utilisateur ne dispose accès tooview hello webhooks associé à un runbook

![Aucun toowebhooks d’accès](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>Configurer RBAC pour votre compte Automation à l’aide d’Azure PowerShell
Accès en fonction du rôle peut également être configuré tooan compte Automation utilisant hello [applets de commande Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).

• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) répertorie tous les rôles RBAC qui sont disponibles dans Azure Active Directory. Vous pouvez utiliser cette commande, ainsi que de hello **nom** toolist propriété tous hello des actions qui peuvent être effectuées par un rôle spécifique.  
    **Exemple :**  
    ![Obtenir la définition de rôle](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [Get-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) répertorie les attributions de rôle Azure AD RBAC à hello spécifié étendue. Sans paramètres, cette commande retourne toutes les attributions de rôle hello effectuées dans l’abonnement de hello. Hello d’utilisation **ExpandPrincipalGroups** affectations de paramètre toolist accès pour hello spécifiés utilisateur ainsi que des groupes de hello hello utilisateur est membre.  
    **Exemple :** suivant de hello utilisez commande toolist tous les utilisateurs de hello et leurs rôles au sein d’un compte automation.

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![Obtenir l’affectation de rôle](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

• [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign toousers, les groupes et les applications tooa particulier étendue d’accès.  
    **Exemple :** suivant de hello utilisez commande tooassign hello « Opérateur Automation » rôle de l’utilisateur dans hello étendue du compte Automation.

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![Nouvelle affectation de rôle](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• Utilisez [Remove-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) tooremove l’accès d’un utilisateur spécifié, le groupe ou l’application à partir d’une étendue particulière.  
    **Exemple :** suivant de hello utilisez commande utilisateur de hello tooremove hello « Automation rôle opérateur de « dans hello étendue du compte Automation.

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

Bonjour exemples ci-dessus, remplacez **connectez-vous Id**, **Id d’abonnement**, **nom de groupe de ressources** et **nom du compte Automation** avec votre Détails du compte. Choisissez **Oui** lorsque vous êtes invité tooconfirm avant de poursuivre l’attribution de rôle d’utilisateur tooremove.   

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur les différentes façons tooconfigure RBAC pour Azure Automation, consultez trop[gérer RBAC avec Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).
* Pour plus d’informations sur les différentes façons toostart un runbook, consultez [démarrage d’un runbook](automation-starting-a-runbook.md)
* Pour plus d’informations sur les types de l’autre, consultez trop[types de runbook Azure Automation](automation-runbook-types.md)

