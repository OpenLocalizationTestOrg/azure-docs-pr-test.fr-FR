---
title: "aaaAzure informations d’identification de déploiement de Service application | Documents Microsoft"
description: "Découvrez comment toouse hello les informations d’identification de déploiement du Service d’applications Azure."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a>Configurer les informations d’identification de déploiement pour Azure App Service
[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) prend en charge deux types d’informations d’identification pour le [déploiement Git local](app-service-deploy-local-git.md) et le [déploiement FTP/S](app-service-deploy-ftp.md). Ceux-ci ne sont pas hello identique à vos informations d’identification Azure Active Directory.

* **Informations d’identification au niveau utilisateur**: un ensemble d’informations d’identification pour l’intégralité du compte Azure hello. Il peut être utilisé toodeploy tooApp Service pour n’importe quelle application, dans n’importe quel abonnement hello compte Azure a tooaccess d’autorisation. Il s’agit de jeu d’informations d’identification de par défaut hello que vous configurez dans **des Services d’application** > **&lt;nom_application >** > **informations d’identification de déploiement**. Cela est hello également l’ensemble par défaut qui apparaît dans le portail hello l’interface graphique utilisateur (par exemple hello **vue d’ensemble** et **propriétés** de votre application [panneau des ressources](../azure-resource-manager/resource-group-portal.md#manage-resources)).

    > [!NOTE]
    > Lorsque vous déléguez accéder aux ressources de tooAzure via le contrôle d’accès en fonction rôle (RBAC) ou des autorisations de coadministrateur, chaque utilisateur de Azure qui reçoit l’accès tooan application peut utiliser ses informations d’identification au niveau utilisateur personnelles jusqu'à ce que l’accès est révoqué. Ces informations d’identification de déploiement ne doivent pas être partagées avec d’autres utilisateurs Azure.
    >
    >

* **Informations d’identification au niveau de l’application** : un seul ensemble d’informations d’identification pour chaque application. Il peut être utilisé toodeploy toothat application uniquement. informations d’identification Hello pour chaque application est générée automatiquement lors de la création de l’application et se trouve dans l’application hello profil de publication. Vous ne pouvez pas configurer manuellement les informations d’identification de hello, mais vous pouvez le réinitialiser à tout moment pour une application.

    > [!NOTE]
    > Dans l’ordre toogive quelqu'un d’informations d’identification de toothese via basé accès contrôle rôle (RBAC) d’accès, vous devez toomake les collaborateurs ou une version ultérieure sur hello Web App. Lecteurs toopublish ne sont pas autorisés et par conséquent, ne peut pas accéder à ces informations d’identification.
    >
    >

## <a name="userscope"></a>Définir et réinitialiser les informations d’identification au niveau de l’utilisateur

Vous pouvez configurer vos informations d’identification au niveau de l’utilisateur dans le [panneau Ressources](../azure-resource-manager/resource-group-portal.md#manage-resources) d’une application. Quel que soit dans l’application, vous configurez ces informations d’identification, il applique les applications tooall et pour tous les abonnements dans votre Azure compte. 

tooconfigure vos informations d’identification au niveau de l’utilisateur :

1. Bonjour [portail Azure](https://portal.azure.com), cliquez sur le Service d’applications >  **&lt;any_app >** > **informations d’identification de déploiement**.

    > [!NOTE]
    > Dans le portail hello, vous devez disposer au moins une application avant que vous pouvez accéder au panneau informations d’identification de déploiement hello. Toutefois, avec hello [CLI d’Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), vous pouvez configurer les informations d’identification au niveau de l’utilisateur sans une application existante.

2. Configurer le nom d’utilisateur hello et le mot de passe, puis cliquez sur **enregistrer**.

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

Une fois que vous avez défini vos informations d’identification de déploiement, vous pouvez trouver hello *Git* nom d’utilisateur de déploiement dans votre application **vue d’ensemble**,

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

et le nom d’utilisateur de déploiement *FTP* dans les **propriétés** de votre application.

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> Azure n’affiche pas votre mot de passe du déploiement au niveau de l’utilisateur. Si vous oubliez le mot de passe hello, vous ne pouvez pas le récupérer. Toutefois, vous pouvez réinitialiser vos informations d’identification en suivant les étapes de hello dans cette section.
>
>  

## <a name="appscope"></a>Obtenir et réinitialiser les informations d’identification au niveau de l’application
Pour chaque application de Service de l’application, ses informations d’identification au niveau de l’application sont stockées dans hello XML le profil de publication.

informations d’identification de tooget hello au niveau de l’application :

1. Bonjour [portail Azure](https://portal.azure.com), cliquez sur le Service d’applications >  **&lt;any_app >** > **vue d’ensemble**.

2. Cliquez sur **...Plus** > **Obtenir le profil de publication**. Le téléchargement du fichier .PublishSettings démarre.

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. Ouvrez hello. Paramètres de publication de fichiers et recherche hello `<publishProfile>` balise avec l’attribut de hello `publishMethod="FTP"`. Obtenez ensuite ses attributs `userName` et `password`.
Il s’agit des informations d’identification de niveau de l’application hello.

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    Informations d’identification d’utilisateur au niveau de toohello similaire, nom d’utilisateur du déploiement hello FTP est format hello `<app_name>\<username>`, et le nom d’utilisateur du déploiement hello Git est simplement `<username>` sans hello précédent `<app_name>\`.

informations d’identification de tooreset hello au niveau de l’application :

1. Bonjour [portail Azure](https://portal.azure.com), cliquez sur le Service d’applications >  **&lt;any_app >** > **vue d’ensemble**.

2. Cliquez sur **...Plus** > **Réinitialiser le profil de publication**. Cliquez sur **Oui** tooconfirm hello réinitialiser.

    l’action reset Hello invalide les précédemment téléchargés. Fichiers de paramètres de publication.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toouse ces informations d’identification toodeploy votre application à partir de [Git local](app-service-deploy-local-git.md) ou à l’aide de [FTP/S](app-service-deploy-ftp.md).
