---
title: "aaaCreate compte d’utilisateur Active Directory de Azure | Documents Microsoft"
description: "Cet article décrit comment toocreate un compte Azure AD des informations d’identification pour les runbooks dans tooauthenticate Azure Automation dans Azure et Azure classic."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "utilisateur azure active directory, azure service management, compte d’utilisateur azure ad"
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a>Authentification des Runbooks avec le déploiement Azure Classic et Resource Manager
Cet article décrit la procédure à hello qu'effectuer tooconfigure un compte d’utilisateur Active Directory de Azure pour les runbooks Azure Automation en cours d’exécution sur le modèle de déploiement classique Azure ou les ressources Azure Resource Manager.  Pendant ce processus poursuit toobe une identité d’authentification pris en charge pour votre gestionnaire de ressources Azure en fonction des procédures opérationnelles, hello recommandé que vous pouvez utiliser un compte d’identification Azure.       

## <a name="create-a-new-azure-active-directory-user"></a>Création d’un nouvel utilisateur Azure Active Directory
1. Ouvrez une session dans le portail Azure Classic de toohello en tant qu’administrateur du service pour hello abonnement Azure que vous souhaitez toomanage.
2. Sélectionnez **Active Directory**, puis sélectionnez le nom hello du répertoire de votre organisation.
3. Sélectionnez hello **utilisateurs** et puis, dans la zone de commande hello, sélectionnez **ajouter un utilisateur**.
4. Sur hello **faites-nous part de cet utilisateur** sous **Type d’utilisateur**, sélectionnez **nouvel utilisateur dans votre organisation**.
5. Entrez un nom d’utilisateur.  
6. Sélectionnez le nom du répertoire hello est associé à votre abonnement Azure sur la page d’Active Directory hello.
7. Sur hello **profil utilisateur** , fournissez les premier et dernier nom, un nom convivial et utilisateur à partir de hello **rôles** liste.  Ne sélectionnez pas la case à cocher **Activer l’authentification multifacteur**.
8. Notez le nom complet et mot de passe temporaire de l’utilisateur hello.
9. Sélectionnez **Paramètres > Administrateurs > Ajouter**.
10. Type hello nom d’utilisateur complet de l’utilisateur hello que vous avez créé.
11. Sélectionnez hello abonnement hello toomanage de l’utilisateur.
12. Déconnectez-vous d’Azure et connectez-vous avec un compte hello que vous venez de créer. Vous serez invité à toochange hello mot de passe utilisateur.

## <a name="create-an-automation-account-in-azure-classic-portal"></a>Création d’un compte Automation dans le portail Azure Classic
Dans cette section, vous effectuer hello suivant les étapes toocreate un compte Azure Automation Bonjour portail Azure pour une utilisation avec les procédures opérationnelles la gestion des ressources dans un déploiement classique Azure.  

> [!NOTE]
> Comptes Automation créés avec le portail Azure Classic de hello peuvent être gérés par hello Azure Classic et portail Azure et l’ensemble d’applets de commande. Une fois que le compte de hello est créé, il ne fait aucune différence comment créer et gérer des ressources au sein du compte de hello. Si vous envisagez de portail Azure Classic toocontinue toouse hello, vous devez utiliser à la place de hello Azure toocreate portail des comptes Automation.
> 
> 

1. Ouvrez une session dans le portail Azure Classic de toohello en tant qu’administrateur du service pour hello abonnement Azure que vous souhaitez toomanage.
2. Sélectionnez **Automation**.
3. Sur hello **Automation** page, sélectionnez **créer un compte Automation**.
4. Bonjour **créer un compte Automation** , tapez un nom pour votre nouveau compte Automation et sélectionnez un **région** à partir de la liste déroulante de hello.  
5. Cliquez sur **OK** tooaccept vos paramètres et créer le compte de hello.
6. Après sa création, il sera répertorié sur hello **Automation** page.
7. Cliquez sur le compte de hello et il affiche la page tableau de bord toohello.  
8. Sur la page du tableau de bord Automation hello, sélectionnez **actifs**.
9. Sur hello **actifs** page, sélectionnez **ajouter des paramètres** situé en bas de hello de page de hello.
10. Sur hello **ajouter des paramètres** page, sélectionnez **ajouter les informations d’identification**.
11. Sur hello **définir les informations d’identification** page, sélectionnez **informations d’identification de Windows PowerShell** de hello **Type d’informations d’identification** déroulante liste et fournir un nom pour les informations d’identification hello.
12. Suivant le hello **définir les informations d’identification** page type de nom d’utilisateur hello hello AD du compte d’utilisateur créé précédemment dans hello **nom d’utilisateur** hello et champ de mot de passe dans hello **mot de passe**et **confirmer le mot de passe** champs. Cliquez sur **OK** toosave vos modifications.

## <a name="create-an-automation-account-in-hello-azure-portal"></a>Créer un compte Automation Bonjour portail Azure
Dans cette section, effectuer hello suivant les étapes toocreate un compte Azure Automation Bonjour portail Azure pour une utilisation avec les procédures opérationnelles la gestion des ressources en mode Azure Resource Manager.  

1. Ouvrez une session dans toohello portail Azure en tant qu’administrateur du service pour hello abonnement Azure que vous souhaitez toomanage.
2. Sélectionnez **Comptes Automation**.
3. Dans le panneau de comptes Automation hello, cliquez sur **ajouter**.<br><br>![Ajouter un compte Automation](media/automation-create-aduser-account/add-automation-acct-properties.png)
4. Bonjour **ajouter un compte Automation** panneau, Bonjour **nom** tapez un nom pour votre nouveau compte Automation.
5. Si vous avez plusieurs abonnements, spécifiez un hello pour le nouveau compte de hello, mais aussi un nouveau ou existant **groupe de ressources** et un centre de données Azure **emplacement**.
6. Sélectionnez la valeur de hello **Oui** pour hello **créer Azure exécuter en tant que compte** , puis cliquez sur hello **créer** bouton.  
   
    > [!NOTE]
    > Si vous choisissez toonot créer le compte d’identification hello en sélectionnant l’option de hello **non**, vous verrez un message d’avertissement Bonjour **ajouter un compte Automation** panneau.  Alors que hello compte est créé et affecté toohello **collaborateur** rôle dans l’abonnement de hello, il n’a pas une identité d’authentification correspondant au sein de votre service d’annuaire abonnements et par conséquent, aucun accès ressources de votre abonnement.  Cela empêchera les runbooks faisant référence à ce compte ne soient pas en mesure de tooauthenticate et effectuer des tâches sur des ressources d’Azure Resource Manager.
    > 
    >

    <br>![Avertissement Ajouter un compte Automation](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. Alors que Azure crée le compte d’automatisation hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.

Lors de la création des informations d’identification hello hello est terminée, vous devez toocreate un hello de tooassociate Asset des informations d’identification du compte Automation avec hello compte d’utilisateur Active Directory créé précédemment.  N’oubliez pas, nous avons créé uniquement compte Automation de hello et il n’est pas associé à une identité de l’authentification.  Effectuez les étapes de hello présentées dans hello [actifs dans l’article d’Azure Automation des informations d’identification](automation-credentials.md#creating-a-new-credential-asset) et entrez la valeur hello pour **nom d’utilisateur** au format de hello **domaine\utilisateur**.

## <a name="use-hello-credential-in-a-runbook"></a>Utiliser les informations d’identification hello dans un runbook
Vous pouvez récupérer les informations d’identification de hello dans un runbook à l’aide de hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) activité et l’utiliser avec [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour abonnement Azure. Si les informations d’identification de hello sont un administrateur de plusieurs abonnements Azure, vous devez également utiliser [Select-AzureSubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify hello correct. Cela est illustré dans l’exemple hello Windows PowerShell ci-dessous qui apparaît généralement en haut de hello de la plupart des runbooks Azure Automation.

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

Vous devez répéter ces lignes après tout [point de contrôle](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) dans votre Runbook. Si hello runbook est interrompu, puis reprend sur un autre travail, il doit à nouveau l’authentification tooperform hello.

## <a name="next-steps"></a>Étapes suivantes
* Révision hello runbook différents types et les étapes de création de vos propres runbooks à partir de hello article suivant [types de runbook Azure Automation](automation-runbook-types.md)

