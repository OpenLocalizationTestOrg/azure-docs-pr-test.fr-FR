---
title: tooauthentication aaaIntro dans Azure Automation | Documents Microsoft
description: "Cet article fournit une vue d’ensemble de la sécurité d’Automation et hello différentes méthodes d’authentification disponibles pour les comptes Automation dans Azure Automation."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "sécurité de l’automatisation ; automation sécurisée ; authentification d’automatisation"
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 4b4409b5be010c16f7bf00a9a0f617e3617d4663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooauthentication-in-azure-automation"></a>Tooauthentication introduction dans Azure Automation  
Azure Automation vous permet de tâches tooautomate par rapport aux ressources dans Azure, sur site et avec d’autres fournisseurs de cloud comme Amazon Web Services (AWS).  Dans l’ordre pour un tooperform runbook ses actions requises, il ressources doit être autorisations toosecurely accès hello doté d’autorisations minimales de hello nécessaires au sein de l’abonnement de hello.

Cet article couvre hello différents scénarios d’authentification pris en charge par Azure Automation et indiquent comment tooget démarrer basée sur les environnement hello ou les environnements vous devez toomanage.  

## <a name="automation-account-overview"></a>Présentation du compte Automation
Lorsque vous démarrez Azure Automation pour hello première fois, vous devez créer au moins un compte Automation. Comptes Automation vous permettent de tooisolate vos ressources Automation (runbooks, éléments multimédias, configurations) à partir de hello ressources contenues dans d’autres comptes Automation. Vous pouvez utiliser les ressources de tooseparate comptes Automation dans des environnements logiques distincts. Par exemple, vous pouvez utiliser un compte pour le développement, un autre pour la production et un autre pour l’environnement local.  Un compte Azure Automation est différent de votre compte Microsoft ou des comptes créés dans votre abonnement Azure.

ressources d’automatisation de Hello pour chaque compte Automation sont associées à une seule région Azure, mais les comptes Automation peuvent gérer toutes les ressources hello dans votre abonnement. Hello principalement toocreate des comptes Automation dans différentes régions serait si vous avez des stratégies qui requièrent des données et des ressources toobe tooa isolé une région spécifique.

> [!NOTE]
> Comptes Automation et les ressources de hello qu’ils contiennent qui sont créées dans hello portail Azure, ne sont pas accessibles dans hello portail Azure classic. Si vous souhaitez toomanage ces comptes ou leurs ressources avec Windows PowerShell, vous devez utiliser des modules du Gestionnaire de ressources Azure hello.
>

Toutes les tâches hello que vous effectuez sur les ressources à l’aide d’Azure Resource Manager et hello applets de commande Azure dans Azure Automation doivent s’authentifier tooAzure à l’aide de l’authentification Azure Active Directory d’organisation identité basée sur les informations d’identification.  L’authentification basée sur certificat méthode d’authentification d’origine hello avec le mode de gestion des services Azure, mais il toosetup complexe.  L’authentification tooAzure avec l’utilisateur Azure AD a été différée introduite dans 2014 toonot uniquement simplifier hello processus tooconfigure est un compte d’authentification, mais également prise en charge hello capacité toonon interactivement authentifier tooAzure avec un compte d’utilisateur qui a été exécutée avec Azure Resource Manager et les ressources classiques.   

Actuellement, lorsque vous créez un nouveau compte Automation dans hello portail Azure, il crée automatiquement :

* Compte d’identification qui crée une nouvelle entité de service dans Azure Active Directory, un certificat et assigne hello collaborateur basée sur le rôle de contrôle d’accès (RBAC), qui sera utilisé à l’aide de procédures opérationnelles de ressources toomanage Gestionnaire de ressources.
* Exécuter en tant que compte classique en téléchargeant un certificat de gestion, s’utilisé toomanage gestion des services Azure ou des ressources classiques à l’aide de procédures opérationnelles.  

Contrôle d’accès basé sur les rôles est disponible avec toogrant Azure Resource Manager autorisé le compte d’utilisateur Azure AD actions tooan et exécuter en tant que compte et authentifier ce principal de service.  Veuillez lire [contrôle d’accès basé sur le rôle dans l’article d’Azure Automation](automation-role-based-access-control.md) pour plus d’informations toohelp développer votre modèle pour la gestion des autorisations d’Automation.  

Procédures opérationnelles en cours d’exécution sur un Runbook Worker hybride dans votre centre de données ou par rapport à des services dans AWS informatiques ne peuvent pas utiliser hello même méthode qui est généralement utilisé pour l’authentification des ressources de tooAzure de runbooks.  Il s’agit, car ces ressources sont en cours d’exécution en dehors d’Azure et nécessitent donc leurs propres informations d’identification de sécurité définies dans Automation tooauthenticate tooresources qui leur seront accessible localement.  

## <a name="authentication-methods"></a>Méthodes d’authentification
Hello tableau suivant récapitule les hello différentes méthodes d’authentification pour chaque environnement pris en charge par Azure Automation et de l’article de hello décrivant comment toosetup l’authentification pour les procédures opérationnelles.

| Méthode | Environnement | Article |
| --- | --- | --- |
| Compte d’utilisateur Azure AD |Azure Resource Manager et gestion des services Azure |[Authentifier des Runbooks avec un compte d’utilisateur Azure AD](automation-create-aduser-account.md) |
| Compte d’identification Azure |Azure Resource Manager |[Authentifier des Runbooks avec un compte d’identification Azure](automation-sec-configure-azure-runas-account.md) |
| Compte d’identification Azure Classic |Gestion des services Azure |[Authentifier des Runbooks avec un compte d’identification Azure](automation-sec-configure-azure-runas-account.md) |
| Authentification Windows |Centre de données local |[Authentifier des Runbooks pour des Runbook Workers hybrides](automation-hybrid-runbook-worker.md) |
| Informations d'identification AWS |Amazon Web Services |[Authentifier des Runbooks avec Amazon Web Services (AWS)](automation-config-aws-account.md) |
