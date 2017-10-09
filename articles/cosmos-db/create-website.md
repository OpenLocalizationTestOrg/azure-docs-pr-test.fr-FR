---
title: "aaaDeploy une application web avec un modèle - de base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment toodeploy un compte de base de données Azure Cosmos, Azure App Service Web Apps et un exemple web application à l’aide d’un modèle Azure Resource Manager."
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a>Déployer Azure Cosmos DB et Azure App Service Web Apps avec un modèle Azure Resource Manager
Ce didacticiel vous montre comment toouse un toodeploy de modèle Azure Resource Manager et intégrer [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/), un [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) application web et un exemple d’application web.

À l’aide de modèles Azure Resource Manager, vous pouvez automatiser facilement hello déployer et configurer vos ressources Azure.  Ce didacticiel montre comment toodeploy une application web et configurer automatiquement les informations de connexion de compte de base de données Azure Cosmos.

À l’issue de ce didacticiel, vous serez hello en mesure de tooanswer suivant questions :  

* Comment puis-je utiliser un toodeploy de modèle Azure Resource Manager et intégrer un compte de base de données Azure Cosmos et une application web dans Azure App Service ?
* Comment puis-je utiliser un toodeploy de modèle Azure Resource Manager et intégrer une application Web Deploy, une application web dans les applications Web App Service et un compte de base de données Azure Cosmos ?

<a id="Prerequisites"></a>

## <a name="prerequisites"></a>Composants requis
> [!TIP]
> Alors que ce didacticiel n’assume pas être familiarisé avec les modèles Azure Resource Manager ou JSON, si vous souhaitez toomodify hello référencées modèles ou les options de déploiement, puis les connaissances de chacun de ces domaines sera nécessaire.
> 
> 

Avant de suivre les instructions de hello dans ce didacticiel, assurez-vous que vous disposez des éléments suivants de hello :

* Un abonnement Azure. Azure est une plateforme disponible par abonnement.  Pour plus d'informations sur l'obtention d'un abonnement, consultez les pages [Modes d’achat d’Azure](https://azure.microsoft.com/pricing/purchase-options/), [Offres spéciales membres](https://azure.microsoft.com/pricing/member-offers/) ou [Version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/).

## <a id="CreateDB"></a>Étape 1 : Télécharger des fichiers de modèle hello
Commençons par téléchargement de fichiers de modèle hello que nous allons utiliser dans ce didacticiel.

1. Télécharger hello [créer un compte de base de données Azure Cosmos, des applications Web et déployer un exemple d’application de démonstration](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) dossier local de modèle tooa (par exemple, C:\Azure Cosmos DBTemplates). Ce modèle déploie un compte Azure Cosmos DB, une application web App Service et une application web.  Il va également automatiquement configurer le compte de base de données Azure Cosmos hello web application tooconnect toohello.
2. Télécharger hello [créer un exemple d’applications Web et un compte de base de données Azure Cosmos](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) dossier local de modèle tooa (par exemple, C:\Azure Cosmos DBTemplates). Ce modèle déploiera un compte de base de données Azure Cosmos, une application web du Service d’applications et modifiera les informations de connexion du site hello application paramètres tooeasily surfaces Azure Cosmos DB, mais n’inclut pas d’une application web.  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a>Étape 2 : Déployer le compte de base de données Azure Cosmos hello, du Service d’applications web app et démonstration exemple d’application
Maintenant, nous allons déployer notre premier modèle.

> [!TIP]
> modèle de Hello ne valide pas le nom de l’application hello web et le nom de compte de base de données Azure Cosmos entré ci-dessous sont un) valide et (b) disponible.  Il est vivement recommandé de vérifier les noms à disponibilité hello Hello planifier le déploiement de hello toosupply toosubmitting préalable.
> 
> 

1. Connexion toohello [Azure Portal](https://portal.azure.com), cliquez sur Nouveau et recherchez « Déploiement de modèle ».
    ![Capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment1.png)
2. Sélectionnez l’élément de déploiement de modèle hello et cliquez sur **créer** ![capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment2.png)
3. Cliquez sur **modifier un modèle de**, collez le contenu hello hello DocDBWebsiteTodo.json du fichier de modèle, puis cliquez sur **enregistrer**.
   ![Capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment3.png)
4. Cliquez sur **modifier les paramètres**, fournir des valeurs pour chacun des paramètres obligatoires de hello, puis cliquez sur **OK**.  paramètres de Hello sont les suivantes :
   
   1. SITENAME : Spécifie hello nom de l’application du Service d’applications web et les URL de hello tooconstruct utilisé que vous allez utiliser l’application web tooaccess hello (par exemple, si vous spécifiez « mydemodocdbwebapp », URL hello par lequel vous allez accéder à l’application web hello sera mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME : Spécifie le nom hello de toocreate du plan d’hébergement du Service d’applications.
   3. EMPLACEMENT : Spécifie hello emplacement Azure dans les ressources d’application toocreate hello web et de la base de données Azure Cosmos.
   4. DATABASEACCOUNTNAME : Spécifie le nom hello de toocreate de compte de base de données Azure Cosmos hello.   
      
      ![Capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment4.png)
5. Choisissez un groupe de ressources existant ou fournir un nom toomake un groupe de ressources et choisir un emplacement pour le groupe de ressources hello.

    ![Capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment5.png)
6. Cliquez sur **passez en revue les conditions juridiques**, **achat**, puis cliquez sur **créer** déploiement de hello toobegin.  Sélectionnez **toodashboard du code confidentiel** déploiement résultant de hello est facilement visible sur votre page d’accueil de portail Azure.
   ![Capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment6.png)
7. Une fois le déploiement de hello, panneau de groupe de ressources hello s’ouvre.
   ![Capture d’écran du Panneau de groupe de ressources hello](./media/create-website/TemplateDeployment7.png)  
8. toouse hello application, accédez simplement les URL de l’application web toohello (dans l’exemple hello ci-dessus, les URL hello serait http://mydemodocdbwebapp.azurewebsites.net).  Vous verrez hello après l’application web :
   
   ![Exemple d’application Todo](./media/create-website/image2.png)
9. Continuez et créer quelques tâches dans l’application web hello et puis retourner le panneau des ressources de groupe toohello Bonjour portail Azure. Cliquez sur la ressource de compte de base de données Azure Cosmos hello dans la liste des ressources hello **requête Explorer**.
    ![Capture d’écran de hello de résumé de l’objectif à l’application web de hello mis en surbrillance](./media/create-website/TemplateDeployment8.png)  
10. Exécuter des requêtes par défaut hello, « sélectionnez * à partir de c » et examiner les résultats hello.  Notez que cette requête hello a récupéré la représentation JSON de hello hello des éléments de tâche créée à l’étape 7 ci-dessus.  Vous pouvez tooexperiment libre avec des requêtes ; par exemple, essayez d’exécuter SELECT * à partir de c WHERE c.isComplete = true tooreturn tous les éléments de tâche qui ont été marquées comme étant terminés.
    
    ![Capture d’écran de lames hello Explorer de requête et les résultats montrant des résultats de la requête hello](./media/create-website/image5.png)
11. Sentir tooexplore libre hello expérience du portail Azure Cosmos DB ou modifier l’exemple d’application de Todo hello.  Lorsque vous êtes prêt, nous allons déployer un autre modèle.

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a>Étape 3 : Déployer hello compte du Document et l’exemple d’application web
Maintenant nous allons déployer notre deuxième modèle.  Ce modèle est utile tooshow comment vous pouvez injecter des informations de connexion de base de données Azure Cosmos tels que le point de terminaison de compte et la clé principale dans une application web en tant que paramètres de l’application ou comme une chaîne de connexion personnalisée. Par exemple, vous disposez de votre propre application web que vous comme toodeploy avec un compte de base de données Azure Cosmos et que les informations de connexion hello remplies automatiquement pendant le déploiement.

> [!TIP]
> modèle de Hello ne valide pas le nom de l’application hello web et le nom de compte de base de données Azure Cosmos entré ci-dessous sont un) valide et (b) disponible.  Il est vivement recommandé de vérifier les noms à disponibilité hello Hello planifier le déploiement de hello toosupply toosubmitting préalable.
> 
> 

1. Bonjour [Azure Portal](https://portal.azure.com), cliquez sur Nouveau et recherchez « Déploiement de modèle ».
    ![Capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment1.png)
2. Sélectionnez l’élément de déploiement de modèle hello et cliquez sur **créer** ![capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment2.png)
3. Cliquez sur **modifier un modèle de**, collez le contenu hello hello DocDBWebSite.json du fichier de modèle, puis cliquez sur **enregistrer**.
   ![Capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment3.png)
4. Cliquez sur **modifier les paramètres**, fournir des valeurs pour chacun des paramètres obligatoires de hello, puis cliquez sur **OK**.  paramètres de Hello sont les suivantes :
   
   1. SITENAME : Spécifie hello nom de l’application du Service d’applications web et les URL de hello tooconstruct utilisé que vous allez utiliser l’application web tooaccess hello (par exemple, si vous spécifiez « mydemodocdbwebapp », URL hello par lequel vous allez accéder à l’application web hello sera mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME : Spécifie le nom hello de toocreate du plan d’hébergement du Service d’applications.
   3. EMPLACEMENT : Spécifie hello emplacement Azure dans les ressources d’application toocreate hello web et de la base de données Azure Cosmos.
   4. DATABASEACCOUNTNAME : Spécifie le nom hello de toocreate de compte de base de données Azure Cosmos hello.   
      
      ![Capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment4.png)
5. Choisissez un groupe de ressources existant ou fournir un nom toomake un groupe de ressources et choisir un emplacement pour le groupe de ressources hello.

    ![Capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment5.png)
6. Cliquez sur **passez en revue les conditions juridiques**, **achat**, puis cliquez sur **créer** déploiement de hello toobegin.  Sélectionnez **toodashboard du code confidentiel** déploiement résultant de hello est facilement visible sur votre page d’accueil de portail Azure.
   ![Capture d’écran de déploiement de modèle hello l’interface utilisateur](./media/create-website/TemplateDeployment6.png)
7. Une fois le déploiement de hello, panneau de groupe de ressources hello s’ouvre.
   ![Capture d’écran du Panneau de groupe de ressources hello](./media/create-website/TemplateDeployment7.png)  
8. Cliquez sur la ressource d’application Web hello dans la liste des ressources hello **paramètres de l’Application** ![capture d’écran hello du groupe de ressources](./media/create-website/TemplateDeployment9.png)  
9. Notez les paramètres d’application pour le point de terminaison de base de données Azure Cosmos hello et chacune des clés principales de base de données Azure Cosmos hello.

    ![Capture d’écran des paramètres de l’application](./media/create-website/TemplateDeployment10.png)  
10. Pensez toocontinue libre exploration hello portail Azure, ou suivez l’une de notre base de données Azure Cosmos [exemples](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate votre propre application de base de données Azure Cosmos.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Étapes suivantes
Félicitations ! Vous avez déployé Azure Cosmos DB, une application web App Service et un exemple d’application web avec les modèles Azure Resource Manager.

* toolearn savoir plus sur la base de données Azure Cosmos, cliquez sur [ici](http://azure.com/docdb).
* toolearn en savoir plus sur les applications de Service Web de l’application Azure, cliquez sur [ici](http://go.microsoft.com/fwlink/?LinkId=325362).
* toolearn savoir plus sur les modèles Azure Resource Manager, cliquez sur [ici](https://msdn.microsoft.com/library/azure/dn790549.aspx).

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)
* Pour un toohello guide consultez Modification de l’ancien portail du nouveau portail toohello hello : [référence pour parcourir les hello portail classique Azure](http://go.microsoft.com/fwlink/?LinkId=529715)

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](http://go.microsoft.com/fwlink/?LinkId=523751), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

