---
title: "aaaGet vos données de centre de sécurité Azure avec Power BI | Documents Microsoft"
description: "Hello pack de contenu Azure Security Center Power BI rend les alertes de sécurité toofind facile, recommandations, effectuées sur des ressources et des tendances, basé sur un jeu de données qui a été créé pour vos rapports."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a>Obtenir des informations à partir des données du Centre de sécurité Azure à l’aide de Power BI
Hello [le tableau de bord Power BI](http://aka.ms/azure-security-center-power-bi) d’Azure Security Center vous permet de toovisualize, analyser et filtrer les recommandations et les alertes de sécurité à partir de n’importe où, y compris de votre appareil mobile. Utilisez les tendances tooreveal du tableau de bord de Power BI hello et modèles - afficher les alertes de sécurité par la ressource ou l’adresse IP source et les risques de sécurité unaddressed par âge ou la ressource d’attaque.

Vous pouvez par ailleurs combiner de diverses manières les recommandations et alertes de sécurité d’Azure Security Center avec d’autres données, en utilisant , par exemple, les données des [journaux d’audit Azure](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) et [d’audit Azure SQL Database](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/). Les deux offrent des tableaux de bord Power BI, et vous pouvez également exporter cette tooExcel de données de création de rapports facile sur l’état de la sécurité de vos ressources de cloud hello.

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a>À l’aide du tableau de bord de centre de sécurité Azure tooaccess Power BI
Vous pouvez également utiliser les rapports Power BI tooaccess hello Azure Security Center du tableau de bord. Suivez hello étapes tooperform cette tâche :

1. Bonjour **Azure Security Center** tableau de bord, cliquez sur **Power BI** bouton.

    ![Se connecter tooAzure centre de sécurité à l’aide de Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. Hello **Power BI** panneau s’ouvre sur le côté droit de hello, comme indiqué dans hello suivant l’écran :

    ![Se connecter tooAzure centre de sécurité à l’aide de Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. Si vous créez du tableau de bord Power BI hello pour hello première fois, vous pouvez choisir une des suivantes de hello options Bonjour **Explorer dans Power BI** panneau :

   * **Tableau de bord de sécurité insights**: choisissez cette option si vous voulez toocreate un tableau de bord qui inclut l’état de la sécurité, les threads et les détections. Il s’agit d’une option plus courante pour le rôle DevOps responsable de l’analyse de l’état de protection et de la détection des alertes sur les différents abonnements.
   * **Tableau de bord de gestion des stratégie**: choisissez cette option si vous souhaitez que la stratégie de gestion et l’application tooexplore.  Il s’agit d’une option plus courante pour l’équipe informatique centrale qui est davantage axée sur la gouvernance. Ils peuvent utiliser cette visibilité toogain de tableau de bord et les analyses de conformité de stratégie de sécurité de leur organisation.
   * Si vous disposez déjà d’un tableau de bord Power BI, cliquez sur **Go tooyour Power BI tableau de bord actuel**.
4. Pour les besoins de cet exemple, cliquez sur l’option **Tableau de bord des informations de sécurité** . S’il s’agit hello première fois, vous créez un tableau de bord Power BI pour le centre de sécurité que vous êtes invité à entrer le pack de contenu tooinstall hello. Cliquez sur **obtenir** bouton Bonjour **packs de contenu pour Power BI** fenêtre, comme indiqué dans hello suivant d’écran :

    ![Tableau de bord des informations de sécurité du centre de sécurité Azure](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. Hello **connecter tooAzure sécurité Centre de sécurité Insights** fenêtre s’affiche. Vérifiez que hello **authentification** méthode est **oAuth2** comme indiqué ci-dessous et cliquez sur **connectez-vous** bouton.

    ![Authentification](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. Vous pouvez être invité tooauthenticate à nouveau vos informations d’identification Azure. Une fois l’authentification effectuée, votre tableau de bord est créé. Après la création d’un tableau de bord hello vous consultez un rapport ayant une structure similaire hello comme indiqué dans hello suivant d’écran :

    ![tableau de bord Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> Une actualisation du rapport de hello se place tootake planifiée quotidiennement. En cas de panne sur cette actualisation, lire [actualiser les problèmes potentiels hello Azure Security Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), pour plus d’informations sur la façon de tootroubleshoot.
>
>

Vous trouverez ici nombre hello des alertes de sécurité et des recommandations, ainsi que hello nombre de machines virtuelles, bases de données SQL Azure et les ressources réseau en cours d’analyse par le centre de sécurité Azure.

Un centre de sécurité de tooAzure lien redirige toohello portail Azure. graphiques de Hello rendent toovisualize facile d’informations sur les recommandations de sécurité et d’alertes, y compris :

* État de sécurité des ressources
* Recommandations en attente
* Recommandations pour les machines virtuelles
* Nombre d’alertes dans le temps
* Ressources ciblées par des attaques
* Adresses IP ciblées par des attaques

Chaque graphique recèle des informations supplémentaires. Sélectionnez une vignette toosee plus d’informations. Par exemple, hello **état de sécurité de ressource** vignette affiche vous des détails supplémentaires sur en attente de recommandations par les ressources comme indiqué dans hello suivant l’écran :

![Recommandations](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

Si vous cliquez sur n’importe quelle ligne de ce graphique, hello autres utilisateurs doivent toogray out et vous concentrer uniquement sur hello que celle que vous avez sélectionné. tableau de bord toohello tooreturn, cliquez sur **Azure Security Center** sous hello **tableaux de bord** option dans le volet gauche de hello de cette page.

> [!NOTE]
> Si vous souhaitez que toocustomize vos rapports en ajoutant des champs supplémentaires ou en modifiant des éléments visuels existants, vous pouvez le modifier hello. Pour plus d’informations, consultez la page [Interagir avec un rapport en mode Édition dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) .
>
>

Hello **alertes au fil du temps, une attaque de ressources** et **attaquant IPs** vignettes ont une sortie similaire hello lorsque vous cliquez sur chacune d’elle. Cela se produit car les rapports hello réunit des informations concernant ces trois variables et appelle **ressources attaque** comme indiqué dans hello suivant d’écran :

![Ressources visées](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

À ce stade vous pouvez également enregistrer une copie de ce rapport, imprimer ou publier sur hello web à l’aide des options de hello disponibles dans hello **fichier** menu.

![Menu Fichier](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a>Explorer les données du Centre de sécurité Azure à l’aide des services Power BI
Se connecter toohello [Pack de contenu Power BI Services](https://msit.powerbi.com/groups/me/getdata/services) dans Power BI et exécutez hello comme suit :

1. Bonjour **Pack de contenu pour Power BI** fenêtre, vous verrez deux options, comme illustré ci-dessous.

    ![Pack de contenu pour Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > Si déjà exécutée hello première partie de cet article, vous verrez qu’une seule option, qui est la gestion des stratégies de centre de sécurité Azure.
   >
   >
2. Pour les besoins de hello de cet exemple, cliquez sur **obtenir** Bonjour **gestion des stratégies de centre de sécurité Azure** vignette.
3. Bonjour **tooAzure gestion des stratégies de centre de sécurité de connexion** (fenêtre), vérifiez les tooselect que **oAuth2** sous **méthode d’authentification** déplacer vers le bas comme indiqué ci-dessous et cliquez sur **Connectez-vous** bouton.

    ![Fenêtre Gestion des stratégies](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. Vous serez redirigé tooan page d’authentification où, vous devez taper les informations d’identification de hello que vous utilisez le centre de sécurité tooconnect tooAzure. Après authentification hello est terminé, Power BI pour commencer l’importation des données toobuild vos rapports. Pendant ce temps, vous pouvez voir hello suivant un message sur le coin droit de hello de votre navigateur :

    ![Se connecter tooAzure centre de sécurité à l’aide de Power BI](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > Lorsque le tableau de bord hello est en cours de création pour hello première peut prendre plu de temps, surtout pour les scénarios où vous avez plusieurs abonnements.
   >
   >
5. Une fois que hello est terminée, votre tableau de bord Azure Security Center Power BI sera chargé avec hello **gestion des stratégies de** rapports toohello comme illustré ci-dessous :

    ![Tableau de bord de gestion des stratégies](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris comment toouse Power BI dans Azure Security Center. toolearn en savoir plus sur Azure Security Center, voir hello :

* [Azure Security Center Guide de planification et opérations](security-center-planning-and-operations-guide.md) — Découvrez comment tooplan adoption du centre de sécurité Azure.
* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) : en savoir comment tooconfigure les paramètres de sécurité dans le centre de sécurité Azure
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) : en savoir comment les alertes toosecurity toomanage et y répondre
* [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.
