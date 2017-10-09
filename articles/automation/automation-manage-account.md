---
title: aaaManage compte Azure Automation | Documents Microsoft
description: "Cet article décrit comment toomanage hello configuration de votre compte Automation, telles que le renouvellement de certificat, la suppression et une configuration incorrecte."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a>Gestion d’un compte Azure Automation
À un moment donné avant l’expiration de votre compte Automation, vous devez le certificat de hello toorenew. Si vous pensez que ce compte d’identification hello a été compromise, vous pouvez supprimer et recréer. Cette section explique comment tooperform ces opérations.

## <a name="self-signed-certificate-renewal"></a>Renouvellement de certificat auto-signé
Hello un certificat auto-signé que vous avez créé pour hello exécuter en tant que compte expire un an à partir de la date de hello de création. Vous pouvez le renouveler à tout moment avant qu’il n’expire. Lors du renouvellement, il certificat valide de hello actuelle est retenue tooensure que les runbooks qui sont en attente jusqu'à ou activement en cours d’exécution, et qui s’authentifient avec hello compte d’identification, ne sont pas affectés négativement. certificat de Hello reste valide jusqu'à ce que sa date d’expiration.

> [!NOTE]
> Si vous avez configuré votre toouse de compte Automation s’exécuter en tant qu’un certificat émis par votre autorité de certification d’entreprise et que vous utilisez cette option, le certificat d’entreprise hello est remplacé par un certificat auto-signé.

toorenew hello certificat, procédez comme hello suivant :

1. Bonjour portail Azure, ouvrez le compte Automation de hello.

2. Sur hello **compte Automation** panneau, Bonjour **compte propriétés** volet, sous **les paramètres de compte**, sélectionnez **exécuter en tant que comptes**.

    ![Panneau des propriétés du compte Automation](media/automation-manage-account/automation-account-properties-pane.png)
3. Sur hello **comptes d’identification** panneau des propriétés, sélectionnez soit hello d’identification de compte ou hello classique exécuter en tant que compte de certificat de hello toorenew pour.

4. Sur hello **propriétés** panneau pourquoi le compte sélectionné, cliquez sur **renouveler certificat**.

    ![Renouveler le certificat pour le compte d’identification](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. Pendant le renouvellement de certificat de hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.

## <a name="delete-a-run-as-or-classic-run-as-account"></a>Supprimer un compte d’identification standard ou Classic
Cette section décrit comment toodelete et recréer un compte d’identification ou classique exécuter en tant que. Lorsque vous effectuez cette action, hello compte Automation est conservée. Après avoir supprimé un compte d’identification ou classique exécuter en tant que, vous pouvez le recréer dans hello portail Azure.

1. Bonjour portail Azure, ouvrez le compte Automation de hello.

2. Sur hello **compte Automation** lame, hello compte volet Propriétés, sélectionnez **exécuter en tant que comptes**.

3. Sur hello **comptes d’identification** panneau des propriétés, sélectionnez soit hello d’identification de compte ou classique exécuter en tant que le compte que vous souhaitez toodelete. Ensuite, sous hello **propriétés** panneau pourquoi le compte sélectionné, cliquez sur **supprimer**.

 ![Supprimer un compte d’identification](media/automation-manage-account/automation-account-delete-runas.png)

4. Lors de la suppression du compte de hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.

5. Une fois que le compte de hello a été supprimé, vous pouvez recréer il sur hello **comptes d’identification** option de création du panneau des propriétés en sélectionnant hello **exécuter en tant que compte Azure**.

 ![Recréez le compte d’identification Automation hello](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a>Configuration incorrecte
Certains éléments de configuration nécessaires pour toofunction de compte Exécuter en tant qu’ou classique en hello peuvent correctement ont été supprimés ou créés correctement lors de l’installation initiale. éléments de Hello sont les suivantes :

* Ressource de certificat
* Ressource de connexion
* Compte d’identification a été supprimé de rôle de collaborateur hello
* Principal du service ou application dans Azure AD

Hello précédent et les autres instances d’une configuration incorrecte, hello compte Automation détecte hello modifie et affiche l’état *incomplet* sur hello **comptes d’identification** panneau des propriétés pour hello compte.

![État Incomplet pour la configuration du compte d’identification](media/automation-manage-account/automation-account-runas-incomplete-config.png)

Lorsque vous sélectionnez le compte d’identification hello, hello compte **propriétés** volet affiche hello message d’erreur suivant :

![Message d’avertissement Incomplet pour la configuration du compte d’identification](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png).

Vous pouvez rapidement résoudre ces problèmes de compte Exécuter en tant qu’à supprimer et recréer le compte de hello.

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur les principaux de Service, voir la rubrique trop[les objets de Principal du Service et Application](../active-directory/active-directory-application-objects.md).
* Pour plus d’informations sur le contrôle d’accès basée sur les rôles dans Azure Automation, consultez trop[contrôle d’accès basé sur un rôle dans Azure Automation](automation-role-based-access-control.md).
* Pour plus d’informations sur les certificats et les services Azure, consultez trop[vue d’ensemble des certificats pour les Services de Cloud Azure](../cloud-services/cloud-services-certs-create.md).
