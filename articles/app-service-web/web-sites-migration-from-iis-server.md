---
title: "aaaMigrate un tooAzure d’application enterprise web du Service d’applications"
description: "Montre comment tooquickly de l’Assistant Migration de Web Apps toouse migrer tooAzure de sites Web IIS existant App Service Web Apps"
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a>Migrer un ordinateur enterprise web application tooAzure du Service d’applications
Vous pouvez facilement migrer vos sites Web existante qui s’exécutent sur Internet Information Services (IIS) 6 ou version ultérieure trop[App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). 

> [!IMPORTANT]
> La fin du support de Windows Server 2003 est intervenue le 14 juillet 2015. Si vous hébergez vos sites Web sur un serveur IIS qui est Windows Server 2003, les applications Web est un moyen de faible risque, économique et problèmes tookeep vos sites Web en ligne et l’Assistant Migration de Web Apps peuvent aider à automatiser les processus de migration de hello pour vous. 
> 
> 

[Web Assistant de Migration applications](https://www.movemetothecloud.net/) peut analyser votre installation de serveur IIS, identifier les sites qui peuvent être migré tooApp Service, mettez en surbrillance tous les éléments qui ne peuvent pas être migrés ou sont non pris en charge sur la plateforme de hello et puis migrez vos sites Web et tooAzure de bases de données associées.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>Éléments vérifiés au cours de l’analyse de compatibilité
Hello, l’Assistant Migration crée un tooidentify de rapport de disponibilité entraîne de tout risque de poser problème ou des problèmes de blocage qui empêchent la réussite d’une migration à partir de local IIS tooAzure App Service Web Apps. Certaines des toobe des éléments clés hello prenant en charge de sont :

* Liaisons de port : Web Apps prend uniquement en charge le port 80 pour le trafic HTTP et le port 443 pour le trafic HTTPS. Configurations de port différent seront ignorées et le trafic sera routé too80 ou 443. 
* Authentification : Web Apps prend en charge l’authentification anonyme par défaut et l’authentification par formulaire lorsqu’une application le spécifie. L'authentification Windows peut être utilisée uniquement en cas d'intégration à Azure Active Directory et ADFS. Aucune des autres formes d’authentification, telles que l’authentification de base, n’est prise en charge pour l’instant. 
* Global Assembly Cache (GAC) : hello GAC n’est pas pris en charge dans les applications Web. Si votre application fait référence à des assemblys dont vous déployez généralement toohello GAC, vous devez toodeploy toohello bin dossier d’application dans les applications Web. 
* Mode de compatibilité IIS5 : non pris en charge dans Web Apps. 
* Pools d’applications – dans les applications Web, de chaque site et de ses applications enfants s’exécutent dans hello même pool d’applications. Si votre site comporte plusieurs applications enfant utilisant plusieurs pools d’applications, les consolider le pool d’applications unique tooa avec des paramètres communs ou migrer chaque application web distinct de tooa application.
* Des composants COM : Web Apps n’autorise pas l’inscription de hello de composants COM sur la plateforme de hello. Si vos applications ou sites Web disposer de tous les composants COM, vous devez les réécrire dans le code managé et les déployer avec le site Web de hello ou application.
* Extensions ISAPI – Web Apps peut prend en charge hello Extensions ISAPI. Toodo, hello éléments suivants sont nécessaires :
  
  * déployer la DLL hello avec votre application web 
  * inscrire la DLL hello à l’aide de [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * Placez un fichier applicationHost.xdt dans la racine du site hello avec contenu hello décrit dans « Chargée autorisant arbitrart ISAPI extensions toobe » [section de cet article](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    Pour plus d’informations toouse des Transformations de documents XML avec votre site Web, consultez [transformer votre Site Web de Microsoft Azure](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).
* La migration ne concerne pas les autres composants comme SharePoint, les extensions serveur FrontPage (FPSE), les serveurs FTP et les certificats SSL.

## <a name="how-toouse-hello-web-apps-migration-assistant"></a>Comment toouse hello l’Assistant Migration de Web Apps
Cette section parcourt un tootoomigrate exemple plusieurs sites Web qui utilisent une base de données SQL Server et en cours d’exécution sur un ordinateur local, Windows Server 2003 R2 (IIS 6.0) :

1. Sur hello IIS server ou votre ordinateur client Accédez trop[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. Installez l’Assistant Migration d’applications Web en cliquant sur hello **dédié le serveur IIS** bouton. Plus d’options sera options Bonjour futur proche. 
3. Cliquez sur hello **Install Tool** bouton tooinstall Assistant de Migration les applications Web sur votre ordinateur.
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > Vous pouvez également cliquer sur **télécharger pour installation hors connexion** toodownload un fichier ZIP de fichiers de l’installation sur des serveurs non connectée toohello internet. Vous pouvez également cliquer sur **télécharger un rapport de préparation de migration existant**, qui est un toowork option avancée avec un migration préparation rapport existant que vous avez créé précédemment (expliqué plus loin).
   > 
   > 
4. Bonjour **Application installer** , cliquez sur **installer** tooinstall sur votre ordinateur. Cette opération installe également les dépendances associées telles que Web Deploy, DacFX et IIS, le cas échéant. 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   Une fois installé, l’Assistant Migration Web Apps démarre automatiquement.
5. Choisissez **migrer des sites et des bases de données à partir d’un serveur distant de tooAzure**. Entrez les informations d’identification administratives hello pour le serveur distant de hello et cliquez sur **continuer**. 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   Vous pouvez bien sûr choisir toomigrate à partir du serveur local de hello. option de Hello à distance est utile lorsque vous souhaitez que les sites Web de toomigrate à partir d’un serveur IIS de production.
   
   À ce stade inspecte l’outil de migration hello hello la configuration de votre serveur IIS, telles que des Sites, des Applications, des Pools d’applications et des dépendances tooidentify candidat sites Web pour la migration. 
6. capture d’écran Hello ci-dessous montre trois des sites Web – **Site Web par défaut**, **TimeTracker**, et **CommerceNet4**. Une base de données associée que nous souhaitons toomigrate disposent de. Sélectionnez tous les sites hello vous comme tooassess et puis cliquez sur **suivant**.
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. Cliquez sur **télécharger** rapport de disponibilité du tooupload hello. Si vous cliquez sur **enregistrer le fichier localement**, vous pouvez exécuter l’outil de migration hello plus tard et téléchargement hello enregistré le rapport Disponibilité du comme indiqué précédemment.
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   Une fois que vous téléchargez des rapports de disponibilité hello, Azure effectue analyse de disponibilité du et les affiche hello de résultats. Lire les détails d’évaluation hello pour chaque site Web et assurez-vous que vous comprenez ou avez traité tous les problèmes avant de continuer. 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. Cliquez sur **commencer la Migration** toostart la migration hello. Vous serez maintenant redirigé tooAzure toolog à votre compte. Il est important que vous vous connectiez à un compte dont l’abonnement Azure est actif. Si vous n’avez pas de compte Azure, vous pouvez vous inscrire [ici](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_) pour bénéficier d’un essai gratuit. 
9. Sélectionnez le compte client hello, abonnement Azure et toouse de région pour vos applications web Azure migrés et les bases de données, puis cliquez sur **commencer la Migration**. Vous pouvez sélectionner toomigrate de sites Web hello plus tard.
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. Sur l’écran suivant de hello vous pouvez modifier les paramètres de migration par défaut toohello, telles que :
    
    * utiliser une base de données SQL Azure existante ou créer une base de données SQL Azure et configurer ses informations d'identification ;
    * Sélectionnez toomigrate de sites Web hello
    * définir des noms pour les applications web Azure hello et leurs bases de données SQL liés
    * personnaliser les paramètres globaux hello et les paramètres au niveau du site
    
    capture d’écran Hello ci-dessous montre tous les sites Web de hello sélectionnés pour la migration avec les paramètres par défaut de hello.
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > Hello **activer Azure Active Directory** case à cocher dans les paramètres personnalisés s’intègre l’application web Azure hello [Azure Active Directory](../active-directory/active-directory-whatis.md) (hello **répertoire par défaut**). Pour plus d’informations sur la synchronisation d’Azure Active Directory avec votre annuaire Azure Directory local, consultez la page [Intégration d’annuaire](http://msdn.microsoft.com/library/jj573653).
    > 
    > 
11. Une fois que vous apportez toutes les modifications de hello souhaité, cliquez sur **créer** processus de migration toostart hello. outil de migration Hello créer une application de web de base de données SQL Azure et Azure hello et publier des bases de données et le contenu du site Web de hello. progression de la migration Hello est clairement indiquée dans l’outil de migration hello, et vous verrez un écran récapitulatif fin hello, les sites de hello détails migrés, si elles ont échoué, les liens toohello nouvellement créé Azure web apps. 
    
    Si une erreur se produit pendant la migration, hello outil de migration va clairement indiquer des changements de hello échec et l’annulation de hello. Vous serez également le rapport d’erreurs en mesure de toosend hello directement l’équipe d’ingénierie toohello de l’équipe en cliquant sur hello **envoyer le rapport d’erreur** bouton, avec la pile des appels capturée échec hello et créer le corps du message. 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    Si migrer aboutit sans erreur, vous pouvez également cliquer sur hello **commenter** bouton, tooprovide de vos commentaires directement. 
12. Cliquez sur hello liens toohello Azure web apps et vérifiez que la migration de hello a réussi.
13. Vous pouvez désormais gérer hello migrer des applications web dans Azure App Service. toodo, connectez-vous à hello [Azure Portal](https://portal.azure.com).
14. Bonjour portail Azure, ouvrez hello Web Apps panneau toosee vos sites migrés (représenté par les applications web), puis cliquez sur l’un d’eux toostart gestion hello web application, telles que la configuration de publication, création de sauvegardes, échelle et surveillance de l’utilisation continue ou performances.
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

