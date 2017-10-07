---
title: "première web application aaaAdd fonctionnalité tooyour | Documents Microsoft"
description: "Ajouter des fonctionnalités intéressantes tooyour première application web en quelques minutes."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 542671c2-22f0-4f20-8b4b-fa477264c492
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2016
ms.author: cephalin
ms.openlocfilehash: 46c9b118c2c188508cb0a369c691a79073b7d7b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-functionality-tooyour-first-web-app"></a>Ajouter des fonctionnalités tooyour première application web
Dans [déployer votre premier tooAzure d’application web dans les cinq minutes](app-service-web-get-started-dotnet.md), vous avez déployé un exemple d’application web à [Azure App Service](../app-service/app-service-value-prop-what-is.md). Dans cet article, vous allez ajouter rapidement certaines fonctionnalités très tooyour déployé l’application web. En quelques minutes, vous allez :

* appliquer l’authentification aux utilisateurs ;
* mettre automatiquement à l’échelle votre application ;
* recevoir des alertes sur les performances de hello de votre application

Quelle que soit l’application exemple vous avez déployé dans l’article précédent de hello, peut suivre la procédure dans le didacticiel de hello.

Bonjour trois activités dans ce didacticiel sont uniquement quelques exemples de hello de nombreuses fonctionnalités utiles que vous obtenez lorsque vous mettez votre application web dans le Service d’applications. Bon nombre de hello sont disponibles dans hello **libre** couche (qui est votre première application web qui s’exécute sur), et vous pouvez utiliser votre tootry crédits d’évaluation des fonctionnalités qui nécessitent une version ultérieure des niveaux tarifaires. La certitude que le reste de votre application web dans **libre** niveau, sauf si vous change explicitement tooa autre niveau tarifaire.

> [!NOTE]
> vous avez créé avec l’interface CLI d’Azure Hello l’application web s’exécute dans **libre** niveau, qui autorise uniquement une instance de machine virtuelle partagée avec des quotas de ressources. Pour plus d’informations sur ce que vous pouvez obtenir avec le niveau **Gratuit** , consultez la section [Limites App Service](../azure-subscription-service-limits.md#app-service-limits).
> 
> 

## <a name="authenticate-your-users"></a>Authentifiez vos utilisateurs
Maintenant, vous allez voir combien il est facile tooadd authentification tooyour application (à [d’authentification/autorisation du Service application](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)).

1. Dans le panneau de portail hello pour votre application, que vous venez ouverte, cliquez sur **paramètres** > **l’authentification / autorisation**.  
    ![Authentification - panneau Paramètres](./media/app-service-web-get-started/aad-login-settings.png)
2. Cliquez sur **sur** tooturn sur l’authentification.  
3. Sous **Fournisseurs d’authentification**, cliquez sur **Azure Active Directory**.  
    ![Authentification - sélectionner Azure AD](./media/app-service-web-get-started/aad-login-config.png)
4. Bonjour **paramètres Azure Active Directory** panneau, cliquez sur **Express**, puis cliquez sur **OK**. Hello paramètres par défaut créer une application Azure AD dans votre répertoire par défaut.  
    ![Authentification - configuration express](./media/app-service-web-get-started/aad-login-express.png)
5. Cliquez sur **Save**.  
    ![Authentification - enregistrer la configuration](./media/app-service-web-get-started/aad-login-save.png)
   
    Une fois la modification de hello est réussie, vous verrez cloche de notification hello vert, ainsi que d’un message convivial.
6. Dans le panneau de portail hello de votre application, cliquez sur hello **URL** lien (ou **Parcourir** dans la barre de menus hello). lien de Hello est une adresse HTTP.  
    ![Authentifier - Parcourir tooURL](./media/app-service-web-get-started/aad-login-browse-click.png)  
    Mais une fois qu’il ouvre l’application hello dans un nouvel onglet, hello URL de redirection case plusieurs fois et à la fin de votre application avec une adresse HTTPS. Que vous voyez tooyour abonnement Azure est que vous êtes déjà connecté, et vous êtes authentifié automatiquement dans l’application hello.  
    ![Authentification - connecté](./media/app-service-web-get-started/aad-login-browse-http-postclick.png)  
    Si vous ouvrez maintenant une session non authentifiée dans un autre navigateur, vous verrez un écran de connexion lorsque vous accédez toohello même URL.  
    <!-- ![Authenticate - login page](./media/app-service-web-get-started/aad-login-browse.png)  -->
    Si vous n’avez jamais utilisé Azure Active Directory, le répertoire par défaut peut ne pas contenir d’utilisateurs Azure AD. Dans ce cas, probablement hello seul compte là est hello compte Microsoft avec votre abonnement Azure. Qui a raison pour laquelle vous étiez connecté automatiquement dans l’application toohello dans hello même navigateur précédemment.
    Vous pouvez utiliser ce même toolog de compte Microsoft dans sur cette page de connexion ainsi.

Félicitations, vous vous authentifiez tout le trafic tooyour web app.

Vous avez peut-être remarqué Bonjour **l’authentification / autorisation** panneau que vous pouvez faire beaucoup plus d’informations, telles que :

* activer la connexion à partir de réseaux sociaux ;
* activer plusieurs options de connexion ;
* Modifier le comportement par défaut de hello lorsque personnes accédez d’abord tooyour application

Service d’applications fournit qu'une solution clés en main pour une partie de l’authentification commune de hello a besoin, vous n’avez pas besoin logique d’authentification tooprovide hello vous-même.
Pour plus d’informations, consultez [App Service Authentication/Authorization](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/) (Authentification/autorisation App Service).

## <a name="scale-your-app-automatically-based-on-demand"></a>Mettez automatiquement à l’échelle votre application en fonction de la demande
Ensuite, nous allons mise à l’échelle votre application afin qu’elle s’il ajuste automatiquement à la demande de capacité toorespond toouser (informations supplémentaires à [l’échelle votre application dans Azure](web-sites-scale.md) et [nombre d’instances à l’échelle manuellement ou automatiquement](../monitoring-and-diagnostics/insights-how-to-scale.md)).

En bref, vous pouvez adapter la taille de votre application web de deux manières :

* [Monter en puissance](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling) : vous offre plus de capacité d’UC, de mémoire et d’espace disque. Obtenez également davantage de fonctionnalités, telles que des machines virtuelles dédiées, des domaines et des certificats personnalisés, des emplacements intermédiaires, la mise à l’échelle automatique et bien plus encore. Monter en modifiant hello tarification du plan de Service d’applications qu'auquel appartient votre application.
* [Montée en puissance parallèle](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): augmenter le nombre hello des instances de machine virtuelle qui exécutent votre application.
  Vous pouvez faire évoluer tooas comme 50 instances, selon votre niveau tarifaire.

Sans plus attendre, préparons à présent la mise à l’échelle automatique.

1. Tout d’abord, nous allons l’échelle tooenable échelle. Dans le panneau de portail hello de votre application, cliquez sur **paramètres** > **mise à l’échelle de la boîte de dialogue (Plan App Service)**.  
    ![Monter en puissance - panneau Paramètres](./media/app-service-web-get-started/scale-up-settings.png)
2. Faites défiler et sélectionnez hello **Standard S1** niveau, hello plus bas niveau qui prend en charge d’échelle (entouré de capture d’écran), puis cliquez sur **sélectionnez**.  
    ![Monter en puissance - choisir un niveau](./media/app-service-web-get-started/scale-up-select.png)
   
    Vous avez terminé la montée en puissance.
   
   > [!IMPORTANT]
   > Ce niveau épuise votre crédit d’essai gratuit. Si vous avez un compte de paiement à l’utilisation, elle implique le compte de frais tooyour.
   > 
   > 
3. Ensuite, nous allons configurer la mise à l’échelle automatique. Dans le panneau de portail hello de votre application, cliquez sur **paramètres** > **monter en charge (Plan App Service)**.  
    ![Augmenter la taille des instances - panneau Paramètres](./media/app-service-web-get-started/scale-out-settings.png)
4. Modification **l’échelle** trop**pourcentage processeur**. curseurs Hello en dessous de la liste déroulante de hello mettre à jour en conséquence. Ensuite, définissez une plage d’**Instances** comprise entre **1** et **2** et une **Plage cible** entre **40** et **80**. Cela en tapant dans les zones hello ou en déplaçant des curseurs de hello.  
    ![Augmenter la taille des instances - configurer la mise à l’échelle automatique](./media/app-service-web-get-started/scale-out-configure.png)
   
    Selon cette configuration, votre application se met à l’échelle automatiquement lorsque l’utilisation de l’UC est supérieure à 80 % (augmentation de la taille des instances) et inférieure à 40 % (diminution de la taille des instances).
5. Cliquez sur **enregistrer** dans la barre de menus hello.

Félicitations, votre application se met à l’échelle automatiquement.

Vous avez peut-être remarqué Bonjour **paramètres d’échelle** panneau que vous pouvez faire beaucoup plus d’informations, telles que :

* Mettre à l’échelle tooa un certain nombre d’instances manuellement
* la mise à l’échelle selon d’autres mesures de performance, telles que le pourcentage de mémoire ou la longueur de la file d’attente de disque ;
* la personnalisation du comportement de mise à l’échelle lorsqu’une règle de performance est déclenchée ;
* la mise à l’échelle automatique selon un calendrier prévu ;
* le réglage du comportement de mise à l’échelle automatique pour un événement ultérieur.

Pour plus d’informations sur la mise à l’échelle de votre application, consultez [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md). Pour plus d’informations sur l’augmentation de la taille des instances, voir [Mise à l’échelle manuelle ou automatique du nombre d’instances](../monitoring-and-diagnostics/insights-how-to-scale.md).

## <a name="receive-alerts-for-your-app"></a>Recevoir des alertes pour votre application
Maintenant que votre application est l’échelle automatique, que se passe-t-il lorsqu’il atteint le nombre maximal d’instances de hello (2) et du processeur est supérieure utilisation souhaitée (80 %) ?
Vous pouvez configurer une alerte (informations supplémentaires à [recevoir des notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)) tooinform vous de cette situation afin que vous pouvez les mettre à l’échelle d’entrée/sortie de votre application, par exemple. Nous allons rapidement configurer une alerte pour ce scénario.

1. Dans le panneau de portail hello de votre application, cliquez sur **outils** > **alertes**.  
    ![Alertes - panneau Paramètres](./media/app-service-web-get-started/alert-settings.png)
2. Cliquez sur **Ajouter une alerte**. Ensuite, dans hello **ressource** boîte de ressource hello select qui se termine par **(serverfarms)**. C’est votre plan App Service.  
    ![Alertes - ajouter une alerte pour un plan App Service](./media/app-service-web-get-started/alert-add.png)
3. Définissez **Nom** sur `CPU Maxed`, **Métrique** sur **Pourcentage UC**, et **Seuil** sur `90`, puis sélectionnez **Envoyer des e-mails aux propriétaires, contributeurs et lecteurs** et cliquez sur **OK**.   
    ![Alertes - configurer une alerte](./media/app-service-web-get-started/alert-configure.png)
   
    Après la création d’alerte de hello par Azure, vous le verrez Bonjour **alertes** panneau.  
    ![Alertes - vue finale](./media/app-service-web-get-started/alert-done.png)

Félicitations, vous recevez désormais des alertes.

Ce paramètre d’alerte vérifie l’utilisation de l’UC toutes les cinq minutes. Si celle-ci dépasse 90 %, vous (ainsi que toute personne autorisée) recevrez un message d’alerte. toosee tous les utilisateurs est autorisé tooreceive hello alerts, accédez toohello le panneau portail de votre application de sauvegarde sur hello **accès** bouton.  
![Afficher qui reçoit des alertes](./media/app-service-web-get-started/alert-rbac.png)

Vous devez voir que **administrateurs d’abonnements** sont déjà hello **propriétaire** de l’application hello. Ce groupe vous inclurez si vous êtes administrateur de compte hello de votre abonnement Azure (par exemple, votre abonnement d’essai). Pour plus d’informations sur le contrôle d’accès en fonction du rôle Azure, consultez [Contrôle d’accès en fonction du rôle Azure](../active-directory/role-based-access-control-configure.md).

> [!NOTE]
> Règles d’alerte est une fonctionnalité Azure. Pour plus d’informations, consultez [Réception de notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Sur votre hello tooconfigure de façon alerte, vous avez peut-être remarqué un rich ensemble d’outils Bonjour **outils** panneau. Ici, vous pouvez résoudre les problèmes, de surveiller les performances, vérifier la présence de vulnérabilités, gérer les ressources, interagir avec la console des ordinateurs virtuels hello et ajouter des extensions utiles. Nous vous invitons tooclick sur chacun de ces outils toodiscover hello simples mais puissantes outils sur vos conseils doigt.

Découvrez comment toodo plus avec votre application déployée. Voici une liste partielle :

* [Acheter et configurer un nom de domaine personnalisé](custom-dns-web-site-buydomains-web-app.md) : achetez un domaine attrayant pour votre application web à la place du domaine *.azurewebsites.net. Ou utilisez un domaine que vous possédez déjà.
* [Configurer l’environnement intermédiaire](web-sites-staged-publishing.md) -déployer votre tooa application intermédiaire URL avant sa mise en production. Mettez à jour votre application web en ligne en toute confiance. Configurez une solution DevOps élaborée avec plusieurs emplacements de déploiement.
* [Configurer le déploiement continu](app-service-continuous-deployment.md) : intégrez le déploiement d’applications à votre système de contrôle de code source. Effectuez le déploiement vers Azure avec chaque validation.
* [Accéder à des ressources locales](web-sites-hybrid-connection-get-started.md) : accédez à une base de données locale ou un système CRM existants.
* [Sauvegarder votre application](web-sites-backup.md) : définissez la sauvegarde et la restauration de votre application web. Anticipez les défaillances inattendues et récupérez vos données après leur survenue.
* [Activer les journaux de diagnostic](web-sites-enable-diagnostic-log.md) -hello de lecture IIS se connecte à partir des traces Azure ou de l’applications. Lisez-les dans un flux, téléchargez-les ou déplacez-les dans [Application Insights](../application-insights/app-insights-overview.md) pour une analyse clé en main.
* [Analyser votre application à la recherche de vulnérabilités](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)-
  Analysez votre application pour la protéger contre les menaces modernes à l’aide du service fourni par [Tinfoil Security](https://www.tinfoilsecurity.com/).
* [Exécuter des travaux en arrière-plan](../azure-functions/functions-overview.md) : exécutez des tâches pour le traitement de données, la création de rapports, etc.
* [Découvrir le fonctionnement d’App Service](../app-service/app-service-how-works-readme.md)

