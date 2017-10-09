---
title: "aaaHow toocreate et déployer un service cloud | Documents Microsoft"
description: "Découvrez comment toocreate et déployer un service cloud à l’aide de hello portail Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Comment toocreate et déployer un service cloud
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-how-to-create-deploy-portal.md)
> * [portail Azure Classic](cloud-services-how-to-create-deploy.md)
>
>

fournit deux façons toocreate Hello portail Azure et déployer un service cloud : *création rapide* et *création personnalisée*.

Cet article explique comment toouse hello toocreate de méthode création rapide un nouveau service cloud, puis utilisez **télécharger** tooupload et déployer un package de service cloud dans Azure. Lorsque vous utilisez cette méthode, hello portail Azure rend disponibles liens pratiques pour l’achèvement de toutes les spécifications que vous avancez. Si vous êtes prêt toodeploy votre cloud service lors de sa création, vous pouvez effectuer les deux à hello simultanément à l’aide de la création personnalisée.

> [!NOTE]
> Si vous envisagez de toopublish votre service cloud à partir de Visual Studio Team Services (VSTS), utilisez Création rapide, puis configurer la publication de VSTS à partir de tableau de bord Azure Quickstart ou hello hello. Pour plus d’informations, consultez [tooAzure de livraison continue à l’aide de Visual Studio Team Services][TFSTutorialForCloudService], ou consultez l’aide de hello **Quick Start** page.
>
>

## <a name="concepts"></a>Concepts
Trois composants sont requis toodeploy une application comme un service cloud dans Azure :

* **Définition de service**  
  fichier de définition Hello cloud service (.csdef) définit le modèle de service hello, y compris le nombre de rôles hello.
* **Configuration de service**  
  fichier de configuration du service cloud Hello (.cscfg) fournit des paramètres de configuration de service de cloud computing hello et les rôles individuels, y compris le nombre hello d’instances de rôle.
* **Package de service**  
  package de service Hello (.cspkg) contient le code de l’application hello et les configurations et les fichiers de définition de service hello.

Vous pouvez en savoir plus sur ces et comment toocreate un package [ici](cloud-services-model-and-package.md).

## <a name="prepare-your-app"></a>Préparation de votre application
Avant de pouvoir déployer un service cloud, vous devez créer le package de service cloud hello (.cspkg) à partir de votre code d’application et un fichier de configuration de service cloud (.cscfg). Bonjour Azure SDK fournit des outils pour la préparation de ces fichiers de déploiement requis. Permet d’installer le Kit de développement logiciel de hello hello [téléchargements Azure](https://azure.microsoft.com/downloads/) page, dans le langage hello que vous préférez toodevelop votre code d’application.

Trois fonctions du service cloud nécessitent une configuration spécifique avant d'exporter le package de service :

* Si vous souhaitez un service cloud qui utilise Secure Sockets Layer (SSL) pour le chiffrement de données, de toodeploy [configurer votre application](cloud-services-configure-ssl-certificate-portal.md#modify) pour SSL.
* Si vous souhaitez que les instances de toorole les connexions Bureau à distance tooconfigure [configurer des rôles de hello](cloud-services-role-enable-remote-desktop-new-portal.md) pour Bureau à distance.
* Si vous souhaitez tooconfigure pour votre service cloud de surveillance détaillée, activer les Diagnostics de Azure pour le service cloud hello. *Surveillance minimale* (par défaut hello niveau de surveillance) utilise des compteurs de performance collectés hello systèmes d’exploitation hôtes pour les instances de rôle (machines virtuelles). *La surveillance détaillée* regroupe des métriques supplémentaires reposant sur des données de performances de hello rôle instances tooenable une analyse plus approfondie des problèmes qui se produisent pendant le traitement de l’application. toofind comment tooenable Azure Diagnostics, reportez-vous à la section [activation des diagnostics dans Azure](cloud-services-dotnet-diagnostics.md).

toocreate un service cloud dans des déploiements de rôles web ou de rôles de travail, vous devez [créer le package de service hello](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Avant de commencer
* Si vous n’avez pas installé hello Azure SDK, cliquez sur **installer Azure SDK** tooopen hello [page de téléchargements Azure](https://azure.microsoft.com/downloads/), puis téléchargez le Kit de développement logiciel de hello pour hello langage que vous préférez toodevelop votre code. (Vous aurez une opportunité toodo cela plus tard.)
* Si toutes les instances de rôle nécessitent un certificat, créer des certificats de hello. Les services cloud requièrent un fichier .pfx avec une clé privée. Vous pouvez télécharger hello certificats tooAzure que vous créez et déployez le service de cloud computing hello.

## <a name="create-and-deploy"></a>Création et déploiement
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Cliquez sur **Nouveau > calcul**, puis faites défiler vers le bas tooand cliquez **Service Cloud**.

    ![Publier votre service cloud](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. Bonjour nouvelle **Service Cloud** panneau, entrez une valeur pour hello **nom DNS**.
4. Créez un **groupe de ressources** ou sélectionnez-en un.
5. Sélectionnez un **emplacement**.
6. Cliquez sur **Package**. Cela ouvre hello **télécharger un package** panneau. Renseignez les champs hello requis. Si l’un de vos rôles contient une seule et même instance, vérifiez que l’option **Déployer même si un ou plusieurs rôles ne contiennent qu’une seule et même instance** est sélectionnée.
7. Vérifiez que l’option **Démarrer le déploiement** est sélectionnée.
8. Cliquez sur **OK** qui entraîne la fermeture hello **télécharger un package** panneau.
9. Si vous n’avez pas de n’importe quel tooadd de certificats, cliquez sur **créer**.

    ![Publier votre service cloud](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>Téléchargement d'un certificat
Si votre package de déploiement a été [configuré les certificats toouse](cloud-services-configure-ssl-certificate-portal.md#modify), vous pouvez télécharger le certificat de hello maintenant.

1. Sélectionnez **certificats**et sur hello **ajouter des certificats** panneau, sélectionnez le fichier de certificat .pfx hello SSL et fournissez hello **mot de passe** certificat hello
2. Cliquez sur **attacher certificat**, puis cliquez sur **OK** sur hello **ajouter des certificats** panneau.
3. Cliquez sur **créer** sur hello **Service Cloud** panneau. Lorsque le déploiement de hello a atteint hello **prêt** état, vous pouvez passer aux étapes toohello.

    ![Publier votre service cloud](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>Vérifier la réussite du déploiement
1. Cliquez sur instance du service cloud hello.

    Hello état doit indiquer que le service de hello est **en cours d’exécution**.
2. Sous **Essentials**, cliquez sur hello **URL du Site** tooopen du service de votre cloud dans un navigateur web.

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>Étapes suivantes
* [Configuration générale de votre service cloud](cloud-services-how-to-configure-portal.md).
* Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name-portal.md).
* [Gérez votre service cloud](cloud-services-how-to-manage-portal.md).
* Configurez des [certificats SSL](cloud-services-configure-ssl-certificate-portal.md).
