---
title: aaaHow tooconfigure un service cloud (portail classique) | Documents Microsoft
description: "Découvrez comment tooconfigure cloud services dans Azure. En savoir plus de la configuration du service cloud tooupdate hello et configurer les instances de toorole d’accès à distance."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 1ea2320f97f667153f7984e4d61d373a6344cf6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>Comment les Services de cloud computing tooConfigure
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-how-to-configure-portal.md)
> * [portail Azure Classic](cloud-services-how-to-configure.md)
> 
> 

Vous pouvez configurer les paramètres de hello couramment utilisé pour un service cloud dans hello portail Azure classic. Ou, si vous aimez tooupdate vos fichiers de configuration directement, téléchargez un tooupdate de fichier de configuration de service, puis téléchargez hello mise à jour de service de cloud de hello de fichier et de mise à jour avec les modifications de configuration hello. Dans les deux cas, les mises à jour configuration hello sont émis tooall les instances de rôle.

Hello portail classique Azure vous permet également de trop[activer la connexion Bureau à distance pour un rôle dans Azure Cloud Services](cloud-services-role-enable-remote-desktop.md)

Azure assurer disponibilité de service 99,95 % au cours de hello mises à jour de la configuration si vous disposez d’au moins deux instances de rôle pour chaque rôle. Qui permet de demandes de client d’ordinateur virtuel tooprocess pendant hello autres est en cours de mise à jour. Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Modification d'un service cloud
1. Bonjour [portail Azure classic](http://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, cliquez sur nom hello du service de cloud hello, puis cliquez sur **configurer**.
   
    ![Page de configuration](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    Sur hello **configurer** page, vous pouvez configurer la surveillance, mise à jour des paramètres de rôle et choisir hello de systèmes d’exploitation et de la famille pour les instances de rôle. 
2. Dans **analyse**, hello ensemble tooVerbose au niveau de surveillance ou minimale et configurer les chaînes de connexion de diagnostic hello qui sont requises pour la surveillance détaillée.
3. Pour les rôles de service (regroupés par rôle), vous pouvez mettre à jour hello suivant les paramètres :
   
    * **Paramètres** modifier les valeurs hello divers paramètres de configuration sont spécifiés dans hello *ConfigurationSettings* éléments hello service (.cscfg) du fichier de configuration.

    * **Certificats**  
        Modifier l’empreinte numérique du certificat hello est utilisé dans le chiffrement SSL pour un rôle. toochange un certificat, vous devez tout d’abord télécharger le nouveau certificat de hello (sur hello **certificats** page). Puis mettez à jour l’empreinte numérique hello dans la chaîne de certificat hello affiché dans les paramètres de rôle hello.
4. Dans **système d’exploitation**, vous pouvez modifier la version pour les instances de rôle ou la famille de système d’exploitation hello ou choisir **automatique** tooenable les mises à jour automatiques de la version de système d’exploitation actuel hello. paramètres de système d’exploitation Hello appliquent tooweb rôles et des rôles de travail, mais n’affectent pas les ordinateurs virtuels.
   
    Au cours du déploiement, version de système d’exploitation plus récent hello est installée sur toutes les instances de rôle et les systèmes d’exploitation hello sont mis à jour automatiquement par défaut. 
   
    Si vous avez besoin pour votre toorun de service cloud sur une version différente du système d’exploitation en raison des exigences de compatibilité dans votre code, vous pouvez choisir une famille de système d’exploitation et la version. Lorsque vous choisissez une version spécifique du système d’exploitation, les mises à jour automatique du système d’exploitation pour le service cloud hello sont suspendus. Vous devez tooensure les systèmes d’exploitation hello reçoivent les mises à jour.
   
    Si vous résolvez tous les problèmes de compatibilité dont vos applications avec la version de système d’exploitation plus récent hello, vous pouvez activer les mises à jour automatique du système d’exploitation en définissant une version de système d’exploitation hello trop**automatique**. 
   
    ![Paramètres du système d'exploitation](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. toosave vos paramètres de configuration et les placer des instances de rôle toohello, cliquez sur **enregistrer**. (Cliquez sur **ignorer** modifications de hello toocancel.) **Enregistrer** et **ignorer** sont ajoutés barre de commandes toohello après avoir modifié un paramètre.

## <a name="update-a-cloud-service-configuration-file"></a>Mise à jour d'un fichier de configuration de service cloud
1. Télécharger un fichier de configuration de service cloud (.cscfg) avec la configuration actuelle de hello. Sur hello **configurer** pour le service cloud hello, cliquez sur **télécharger**. Puis cliquez sur **enregistrer**, ou cliquez sur **Enregistrer sous** fichier hello de toosave.
2. Une fois que vous mettez à jour le fichier de configuration de service hello, télécharger et appliquer les mises à jour de la configuration hello :
   
   1. Sur hello **configurer** , cliquez sur **télécharger**.
      
       ![Télécharger une configuration](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. Dans **fichier de Configuration**, utilisez **Parcourir** tooselect hello mis à jour le fichier .cscfg.
   3. Si votre service cloud contient tous les rôles qui ont une seule instance, sélectionnez hello **appliquer configuration même si un ou plusieurs rôles contiennent une seule instance** mises à jour de configuration de case à cocher tooenable hello pour hello rôles tooproceed.
      
       Si vous n'avez pas défini au moins deux instances de chaque rôle, Azure n'est pas en mesure de garantir au moins 99,95 % de disponibilité pour votre service cloud pendant les mises à jour de la configuration du service. Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).
   4. Cliquez sur **OK** (coche). 

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[déployer un service cloud](cloud-services-how-to-create-deploy.md).
* Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name.md).
* [Gérez votre service cloud](cloud-services-how-to-manage.md).
* [Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services](cloud-services-role-enable-remote-desktop.md)
* Configurez des [certificats SSL](cloud-services-configure-ssl-certificate.md).

