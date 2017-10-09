---
title: "aaaCreate votre première application de web Java dans Azure"
description: "Découvrez comment toorun web des applications dans le Service d’applications en déployant une application Java de base."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a>Créer votre première application web Java dans Azure

Hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fonctionnalité de [Azure App Service](../app-service/app-service-value-prop-what-is.md) fournit une service d’hébergement web hautement évolutif et correction automatique. Ce démarrage rapide montre comment toodeploy Java web application tooApp Service à l’aide de hello [IDE Eclipse pour développeurs Java EE](http://www.eclipse.org/).

![« Hello Azure ! » Exemple d’application web](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>Composants requis

toocomplete ce démarrage rapide, installer :

* Hello libre [IDE Eclipse pour développeurs Java EE](http://www.eclipse.org/downloads/). Ce démarrage rapide utilise Eclipse Neon.
* Hello [boîte à outils Azure pour Eclipse](/azure/azure-toolkit-for-eclipse-installation).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>Créer un projet web dynamique dans Eclipse

Dans Eclipse, sélectionnez **File (Fichier)** > **New (Nouveau)** > **Dynamic Web Project (Projet web dynamique)**.

Bonjour **nouveau projet Web dynamique** boîte de dialogue, les projets de hello nom **MyFirstJavaOnAzureWebApp**, puis sélectionnez **Terminer**.
   
![Boîte de dialogue Projet web dynamique](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>Ajouter une page JSP

Si l’Explorateur de projets n’est pas affiché, restaurez-le.

![Espace de travail Java EE pour Eclipse](./media/app-service-web-get-started-java/pe.png)

Dans l’Explorateur de projets, développez hello **MyFirstJavaOnAzureWebApp** projet.
Cliquez avec le bouton droit sur **WebContent**, puis sélectionnez **New (Nouveau)** > **JSP File (Fichier JSP)**.

![Menu d’un nouveau fichier JSP dans l’Explorateur de projets](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

Bonjour **nouveau fichier JSP** boîte de dialogue :

* Nom de fichier hello **index.jsp**.
* Sélectionnez **Terminer**.

  ![Boîte de dialogue New JSP File (Nouveau fichier JSP)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

Dans le fichier index.jsp de hello, remplacez hello `<body></body>` élément avec hello suivant de balisage :

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Enregistrer les modifications de hello.

## <a name="publish-hello-web-app-tooazure"></a>Publier hello web application tooAzure

Dans l’Explorateur de projets, cliquez sur le projet de hello et sélectionnez **Azure** > **publier en tant qu’application Web Azure**.

![Menu contextuel Publish as Azure Web App (Publier en tant qu’application web Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

Bonjour **Azure Sign In** boîte de dialogue, gardez hello **Interactive** option et sélectionnez **connectez-vous**.

Suivez hello connectez-vous instructions.

### <a name="deploy-web-app-dialog-box"></a>Boîte de dialogue Déployer une application web

Une fois que vous avez connecté tooyour compte Azure, hello **déployer l’application Web** boîte de dialogue s’affiche.

Sélectionnez **Créer**.

![Boîte de dialogue Déployer une application web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>Boîte de dialogue Créer App Service

Hello **créer un Service application** boîte de dialogue s’affiche avec les valeurs par défaut. nombre de Hello **170602185241** illustré hello suivant image est différente dans votre boîte de dialogue.

![Boîte de dialogue Créer App Service](./media/app-service-web-get-started-java/cas1.png)

Bonjour **créer un Service application** boîte de dialogue :

* Conservez le nom hello généré pour l’application web de hello. Ce nom doit être unique au sein d’Azure. nom de Hello fait partie de l’adresse URL de hello pour l’application web de hello. Par exemple : si le nom de l’application web hello est **MyJavaWebApp**, hello URL est *myjavawebapp.azurewebsites.net*.
* Conserver le conteneur de web hello par défaut.
* Sélectionnez un abonnement Azure.
* Sur hello **plan App service** onglet :

  * **Créer de nouveaux**: conserver la valeur par défaut de hello, qui est le nom hello Hello plan App Service.
  * **Emplacement** : sélectionnez **Europe de l’Ouest** ou un emplacement près de chez vous.
  * **Niveau de tarification**: sélectionnez hello option disponible. Pour plus d’informations sur les fonctionnalités, consultez la page [Tarification de App Service](https://azure.microsoft.com/pricing/details/app-service/).

   ![Boîte de dialogue Créer App Service](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>Onglet Groupe de ressources

Sélectionnez hello **groupe de ressources** onglet. Conservez hello générée par défaut pour le groupe de ressources hello.

![Onglet Groupe de ressources](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Sélectionnez **Créer**.

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

Hello boîte à outils Azure crée l’application web hello et affiche une boîte de dialogue de progression.

![Boîte de dialogue indiquant la progression de la création du service App Service](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>Boîte de dialogue Déployer une application web

Bonjour **déployer l’application Web** boîte de dialogue, sélectionnez **déployer tooroot**. Si vous avez un service d’application à *wingtiptoys.azurewebsites.net* et vous ne déployez pas toohello racine, l’application hello web nommée **MyFirstJavaOnAzureWebApp** est déployé trop *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.

![Boîte de dialogue Déployer une application web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

zone de boîte de dialogue Hello indique Bonjour Azure JDK et les sélections web conteneur.

Sélectionnez **déployer** toopublish hello web application tooAzure.

Une fois la publication hello, sélectionnez hello **publié** lien Bonjour **journal des activités Azure** boîte de dialogue.

![Boîte de dialogue Journal d’activité Azure](./media/app-service-web-get-started-java/aal.png)

Félicitations ! Vous avez correctement déployé votre tooAzure d’application web. 

![« Hello Azure ! » Exemple d’application web](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>Mettre à jour de l’application web hello

Modifier un exemple JSP code tooa autre message de type hello.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Enregistrer les modifications de hello.

Dans l’Explorateur de projets, cliquez sur le projet de hello et sélectionnez **Azure** > **publier en tant qu’application Web Azure**.

Hello **déployer l’application Web** boîte de dialogue apparaît et affiche hello du service d’applications que vous avez créé précédemment. 

> [!NOTE]
> Sélectionnez **déployer tooroot** chaque fois que vous publiez.
>

Sélectionnez l’application web hello **déployer**, qui publie les modifications hello.

Hello lorsque **publication** lien s’affiche, sélectionner l’application web toobrowse toohello et voir les modifications hello.

## <a name="manage-hello-web-app"></a>Gérer l’application hello web

Accédez toohello <a href="https://portal.azure.com" target="_blank">portail Azure</a> toosee hello web application que vous avez créé.

Dans le menu de gauche hello, sélectionnez **groupes de ressources**.

![Groupes de navigation du portail tooresource](media/app-service-web-get-started-java/rg.png)

Sélectionnez le groupe de ressources hello. page de Hello montre les ressources hello que vous avez créé dans ce démarrage rapide.

![Groupe de ressources myResourceGroup](media/app-service-web-get-started-java/rg2.png)

Sélectionnez hello web app (**webapp-170602193915** Bonjour précédant l’image).

Hello **vue d’ensemble** page s’affiche. Cette page vous donne un aperçu du faire des application hello. Elle vous permet d’exécuter des tâches de gestion de base, telles que parcourir, arrêter, démarrer, redémarrer et supprimer. affichent les onglets Hello sur le côté gauche de hello de page de hello hello différentes configurations que vous pouvez ouvrir. 

![Page App Service du Portail Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Mapper un domaine personnalisé](app-service-web-tutorial-custom-domain.md)
