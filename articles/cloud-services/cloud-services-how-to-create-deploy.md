---
title: "aaaHow toocreate et déployer un service cloud | Documents Microsoft"
description: "Découvrez comment toocreate et déployer un service cloud à l’aide de la méthode de création rapide de hello dans Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Comment tooCreate et déployer un Service Cloud
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-how-to-create-deploy-portal.md)
> * [portail Azure Classic](cloud-services-how-to-create-deploy.md)
> 
> 

fournit deux façons toocreate Hello portail Azure classic et déployer un service cloud : **création rapide** et **création personnalisée**.

Cette rubrique explique comment toouse hello toocreate de méthode création rapide un nouveau service cloud, puis utilisez **télécharger** tooupload et déployer un package de service cloud dans Azure. Lorsque vous utilisez cette méthode, hello portail Azure classic rend disponibles liens pratiques pour l’achèvement de toutes les spécifications que vous avancez. Si vous êtes prêt toodeploy votre cloud service lors de sa création, vous pouvez effectuer les deux à hello même à l’aide de temps **création personnalisée**.

> [!NOTE]
> Si vous envisagez de votre service cloud à partir de Visual Studio Team Services (VSTS) toopublish, utilisez **création rapide**, puis configurez la publication de VSTS à partir **Quick Start** ou tableau de bord hello.
> 
> 

## <a name="concepts"></a>Concepts
Trois composants sont requis dans toodeploy ordre une application comme un cloud service dans Azure :

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

* Si vous souhaitez un service cloud qui utilise Secure Sockets Layer (SSL) pour le chiffrement de données, de toodeploy [configurer votre application](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) pour SSL.
* Si vous souhaitez que les instances de toorole les connexions Bureau à distance tooconfigure [configurer des rôles de hello](cloud-services-role-enable-remote-desktop.md) pour Bureau à distance.
* Si vous souhaitez tooconfigure pour votre service cloud de surveillance détaillée, activer les Diagnostics de Azure pour le service cloud hello. *Surveillance minimale* (par défaut hello niveau de surveillance) utilise des compteurs de performance collectés hello systèmes d’exploitation hôtes pour les instances de rôle (machines virtuelles). « La surveillance détaillée * rassemble des métriques supplémentaires reposant sur des données de performances de hello rôle instances tooenable une analyse plus approfondie des problèmes qui se produisent pendant le traitement de l’application. toofind comment tooenable Azure Diagnostics, reportez-vous à la section [activation des Diagnostics dans Azure](cloud-services-dotnet-diagnostics.md).

toocreate un service cloud dans des déploiements de rôles web ou de rôles de travail, vous devez [créer le package de service hello](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Avant de commencer
* Si vous n’avez pas installé hello Azure SDK, cliquez sur **installer Azure SDK** tooopen hello [page de téléchargements Azure](https://azure.microsoft.com/downloads/), puis téléchargez le Kit de développement logiciel de hello pour hello langage que vous préférez toodevelop votre code. (Vous aurez une opportunité toodo cela plus tard.)
* Si toutes les instances de rôle nécessitent un certificat, créer des certificats de hello. Les services cloud requièrent un fichier .pfx avec une clé privée. Vous pouvez [télécharger hello certificats tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) que vous créez et déployez le service de cloud computing hello.
* Si vous envisagez de groupe d’affinités de toodeploy hello cloud service tooan, créer le groupe d’affinités de hello. Vous pouvez utiliser un groupe d’affinités de toodeploy votre service cloud et autres services Azure de toohello même emplacement dans une région. Vous pouvez créer le groupe d’affinités de hello Bonjour **réseaux** zone Hello portail Azure classic sur hello **groupes d’affinités** page.

## <a name="how-to-create-a-cloud-service-using-quick-create"></a>Création d’un service cloud avec Création rapide
1. Bonjour [portail Azure classic](http://manage.windowsazure.com/), cliquez sur **nouveau**>**de calcul**>**Service Cloud** > **Création rapide**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. Dans **URL**, entrez un toouse de nom de sous-domaine dans les URL publique hello pour accéder à votre service cloud dans les déploiements de production. format d’URL Hello pour les déploiements de production : http://*myURL*. cloudapp.net.
3. Dans **région ou groupe d’affinités**, sélectionnez hello géographique région ou groupe d’affinités toodeploy hello cloud service. Sélectionnez un groupe d’affinités toodeploy votre toohello de service cloud même emplacement que les autres services Azure dans une région.
4. Cliquez sur **Create Cloud Service**.
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    Vous pouvez surveiller l’état de hello du processus de hello dans la zone de message hello bas hello de fenêtre hello.
   
    Hello **Services de cloud computing** zone s’ouvre avec le nouveau service de cloud hello affiché. Hello devient tooCreated, lors de la création du service cloud est terminée.
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a>Téléchargement d’un certificat pour un service cloud
1. Bonjour [portail Azure classic](http://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, cliquez sur nom hello du service de cloud hello, puis cliquez sur **certificats**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. Cliquez sur **Télécharger un certificat** ou sur **Télécharger**.
3. Dans **fichier**, utilisez **Parcourir** certificat de hello tooselect (fichier .pfx).
4. Dans **mot de passe**, entrez hello clé privée hello.
5. Cliquez sur **OK** (coche).
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    Vous pouvez surveiller la progression hello du téléchargement hello dans la zone de message hello, illustré ci-dessous. Lorsque hello téléchargement terminé, les certificats hello sont ajouté toohello table. Dans la zone de message hello, cliquez sur le message de type hello tooclose OK.
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a>Déploiement d’un service cloud
1. Bonjour [portail Azure classic](http://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, cliquez sur nom hello du service de cloud hello, puis cliquez sur **tableau de bord**.
2. Cliquez sur **Télécharger un nouveau déploiement de production** ou sur **Télécharger**.
3. Dans **étiquette de déploiement**, entrez un nom pour le nouveau déploiement hello - par exemple, MyCloudServicev4.
4. Dans **Package**, utilisez **Parcourir** tooselect hello service package (.cspkg) de fichier toouse.
5. Dans **Configuration**, utilisez **Parcourir** service de hello tooselect configurer toouse de fichier (.cscfg).
6. Si le service cloud hello inclut tous les rôles qu’une seule instance, sélectionnez hello **déployer même si un ou plusieurs rôles contiennent une seule instance** tooproceed de déploiement de case à cocher tooenable hello.
   
    Azure ne garantissent 99,95 % accès toohello cloud service pendant les mises à jour de maintenance et de service si chaque rôle possède au moins deux instances. Si nécessaire, vous pouvez ajouter des instances de rôle supplémentaires sur hello **échelle** page après avoir déployé le service de cloud computing hello. Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).
7. Cliquez sur **OK** déploiement du service cloud (coche) toobegin hello.
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    Vous pouvez surveiller l’état de hello du déploiement hello dans la zone de message hello. Cliquez sur le message de type hello toohide OK.
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a>Vérifier la réussite du déploiement
1. Cliquez sur **Dashboard**.
   
    Hello état doit indiquer que le service de hello est **en cours d’exécution**.
2. Sous **coup de œil rapide**, cliquez sur hello site URL tooopen votre service cloud dans un navigateur web.
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a>Étapes suivantes
* [Configuration générale de votre service cloud](cloud-services-how-to-configure.md).
* Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name.md).
* [Gérez votre service cloud](cloud-services-how-to-manage.md).
* Configurez des [certificats SSL](cloud-services-configure-ssl-certificate.md).

