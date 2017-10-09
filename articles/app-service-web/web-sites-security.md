---
title: aaaSecure une application dans Azure App Service
description: "Découvrez comment toosecure une application web, un serveur principal d’application mobile ou une application API dans Azure App Service."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 5ce560b4-42d7-4b20-935c-0445fd539e39
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: fceef7963b29516f33602dcd50591d14309bf188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Sécurisation d'une application dans Azure App Service
Cet article vous aide à démarrer la sécurisation de votre application web, de votre serveur principal d’application mobile ou de votre application API dans Azure App Service. 

Il existe deux niveaux de sécurité dans Azure App Service. 

* **Plateforme et l’infrastructure de sécurité** -approbation toohave Azure hello services que vous avez besoin des éléments de tooactually exécuter en toute sécurité dans le cloud de hello.
* **Sécurité des applications** -vous avez besoin en toute sécurité les application hello toodesign proprement dit. Cela inclut la façon dont vous intégrez avec Azure Active Directory, comment gérer des certificats et comment vous assurer que vous pouvez communiquer en toute sécurité avec toodifferent services. 

#### <a name="infrastructure-and-platform-security"></a>Sécurité de la plateforme et de l’infrastructure
Car le Service d’applications conserve hello machines virtuelles Azure, stockage, connexions réseau, infrastructures web, la gestion et les fonctionnalités d’intégration et bien plus encore, il est activement sécurisé et renforcé et traverse énergiquement conformité et que des contrôles sur un toomake de façon continue qui :

* Vos applications de Service d’applications sont isolées les deux hello Internet et à partir de hello ressources Azure d’autres clients.
* la communication de clés secrètes (par exemple, des chaînes de connexion) entre votre application App Service et d’autres ressources Azure (par exemple, la base de données SQL) dans un groupe de ressources reste dans Azure et ne franchit par les limites du réseau. Les clés secrètes sont toujours chiffrées ;
* toutes les communications entre votre application App Service et des ressources externes, telles que la gestion de PowerShell, une interface de ligne de commande, des kits de développement logiciel Azure, des API REST et des connexions hybrides, sont correctement chiffrés ;
* la gestion continue des menaces protège les ressources App Service contre les programmes malveillants, le déni de service distribué (DDoS), les attaques de l’intercepteur (man-in-the-middle, MITM) et bien d’autres menaces. 

Pour plus d’informations sur la sécurité de l’infrastructure et de la plateforme dans Azure, consultez [Centre de gestion de la confidentialité Azure](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Sécurité des applications
Azure est responsable de la sécurisation d’infrastructure de hello et la plateforme que votre application s’exécute sur, mais il est toosecure de votre responsabilité l’application elle-même. En d’autres termes, vous devez toodevelop, déployer et gérer votre code d’application et le contenu de manière sécurisée. Sans cela, votre code d’application ou le contenu peut toujours être vulnérables toothreats tel que :

* l’injection de code SQL ;
* le piratage de session ;
* l’exécution de scripts de site à site ;
* les attaques de l’intercepteur au niveau des applications ;
* le déni de service distribué au niveau des applications.

La description complète de considérations de sécurité pour les applications web est abordée dans ce document hello. Comme point de départ pour obtenir des instructions sur la sécurisation de votre application, consultez hello [ouvrir Web Application sécurité projet (OWASP avoir)](https://www.owasp.org/index.php/Main_Page), spécifiquement hello [top 10 projet.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), qui répertorie hello 10 premiers actuel critique web application failles de sécurité, comme déterminé par les membres d’OWASP avoir.

## <a name="perform-penetration-testing-on-your-app"></a>Réalisation de tests d’intrusion sur votre application
Un des hello plus simple façons tooget main des tests pour des vulnérabilités dans votre application de Service d’applications est toouse hello [intégration à Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) vulnérabilité d’un clic tooperform analyse sur votre application. Vous pouvez afficher les résultats des tests hello dans un rapport facile à comprendre et découvrez comment toofix chaque problème de sécurité avec des instructions pas à pas.

Si vous préférez tooperform votre propre intrusion des tests ou souhaitez toouse une autre suite de l’analyseur ou fournisseur, vous devez suivre hello [intrusion Azure tester le processus d’approbation](https://security-forms.azure.com/penetration-testing/terms) et d’obtenir ce type de préalable tooperform hello souhaité tests.

## <a name="https"></a> Sécurisation des communications avec les clients
Si vous utilisez hello  **\*. azurewebsites.net** nom de domaine créé pour votre application de Service de l’application, vous pouvez immédiatement utiliser HTTPS, car un certificat SSL n’est fourni pour tous les  **\*. azurewebsites.net** les noms de domaine. Si votre site utilise un [nom de domaine personnalisé](app-service-web-tutorial-custom-domain.md), vous pouvez télécharger un certificat SSL trop[activer HTTPS](app-service-web-tutorial-custom-ssl.md) pour le domaine personnalisé de hello.

L’activation de [HTTPS](https://en.wikipedia.org/wiki/HTTPS) peut vous protéger contre les attaques de l’intercepteur sur la communication de hello entre votre application et ses utilisateurs.

## <a name="secure-data-tier"></a>Sécurisation de la couche Données
Service d’applications hautement intègre avec la base de données SQL, de sorte que toutes les chaînes de connexion hello sont chiffrés sur tableau de hello et sont déchiffrées uniquement sur la machine virtuelle de hello cette application hello s’exécute sur *et* uniquement hello lorsque les exécutions de l’application. En outre, la base de données SQL Azure inclut nombreux toohelp de fonctionnalités de sécurité vous sécuriser vos données d’application à partir de menaces informatiques, y compris [chiffrement au repos](https://msdn.microsoft.com/library/dn948096.aspx), [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx), [ Masquage dynamique des données](../sql-database/sql-database-dynamic-data-masking-get-started.md), et [détection de menaces](../sql-database/sql-database-threat-detection.md). Si vous avez des données sensibles ou des exigences de conformité, consultez [sécurisation de votre base de données SQL](../sql-database/sql-database-security-overview.md) pour plus d’informations sur la façon de toosecure vos données.

Si vous utilisez un fournisseur de base de données de tiers, tels que ClearDB, vous devez consulter avec la documentation du fournisseur hello directement sur les meilleures pratiques de sécurité.  

## <a name="develop"></a> Déploiement et développement sécurisés
### <a name="publishing-profiles-and-publish-settings"></a>Profils et paramètres de publication
Lors du développement d’applications, effectuer des tâches de gestion, ou automatiser des tâches à l’aide d’utilitaires tels que **Visual Studio**, **Web Matrix**, **Azure PowerShell** ou hello **Azure Interface de ligne (Azure)**, vous pouvez utiliser un *paramètres de publication* fichier ou un *profil de publication*. Les deux types de fichiers vous authentifient avec Azure et doivent être sécurisées à l’accès tooprevent non autorisé.

* Un fichier de **paramètres de publication** contient :
  
  * L'identifiant de votre abonnement Azure.
  * Un certificat de gestion qui vous permet de tooperform les tâches de gestion pour votre abonnement *sans avoir tooprovide nom de compte ou mot de passe*.
* Un fichier de **profil de publication** contient :
  
  * Informations pour la publication d’application de tooyour

Si vous utilisez un utilitaire qui utilise un fichier de paramètres de publication ou d’un fichier de profil de publication, importer le fichier hello contenant les paramètres de publication hello ou Profiler dans l’utilitaire de hello, puis **supprimer** fichier de hello. Si vous devez conserver le fichier de hello, tooshare avec d’autres fonctionne sur le projet de hello, par exemple, stockez-le dans un emplacement sécurisé comme un *chiffrées* répertoire avec des autorisations restreintes.

En outre, il se peut que vous devez vous assurer que les informations d’identification de hello importé sont sécurisées. Par exemple, **Azure PowerShell** et hello **Azure Interface de ligne (Azure)** à la fois stockent les informations importées dans votre **répertoire** ( *~*  sur les systèmes Linux ou OS X et */users/votre_nom_utilisateur* sur les systèmes Windows.) Pour plus de sécurité, vous souhaiterez peut-être trop**chiffrer** ces emplacements à l’aide des outils de chiffrement disponibles pour votre système d’exploitation.

### <a name="configuration-settings-and-connection-strings"></a>Paramètres de configuration et chaînes de connexion
Il s’agit des chaînes de connexion de toostore pratique courantes, les informations d’authentification et les autres informations sensibles dans les fichiers de configuration. Malheureusement, ces fichiers peuvent être exposés sur votre site web, ou déposés dans un référentiel public, exposant ces informations. Une recherche simple sur [GitHub](https://github.com), par exemple, peut révéler les innombrables des fichiers de configuration comportant des secrets exposés dans les référentiels publics hello.

Il est recommandé de Hello est tookeep ces informations en dehors des fichiers de configuration de votre application. Service d’applications vous permet de stocker des informations de configuration dans le cadre de l’environnement d’exécution hello en tant que **paramètres de l’application** et **les chaînes de connexion**. les valeurs Hello sont tooyour exposé à l’application lors de l’exécution via *variables d’environnement* pour la plupart des langages de programmation. Pour les applications .NET, ces valeurs sont injectées dans votre configuration .NET au moment de l’exécution. En dehors de ces situations, ces paramètres de configuration seront chiffrées, sauf si vous affichez ou configurez les à l’aide de hello [portail Azure](https://portal.azure.com) ou utilitaires, tels que PowerShell ou hello CLI d’Azure. 

Le stockage des informations de configuration dans le Service d’applications rend possible pour toolock d’administrateur de l’application hello des informations sensibles pour les applications de production hello. Les développeurs peuvent utiliser un ensemble distinct de paramètres de configuration pour le développement d’applications et les paramètres de hello peuvent être remplacées automatiquement par les paramètres hello configurés dans le Service d’applications. Les développeurs de hello même pas besoin des secrets de hello tooknow configurés pour l’application de production hello. Pour plus d’informations sur la configuration des paramètres d’application et des chaînes de connexion dans App Service, consultez [Configuration des applications web](web-sites-configure.md).

### <a name="ftps"></a>FTPS
Azure App Service fournit un système de fichiers toohello de l’accès FTP sécurisé pour votre application via **FTPS**. Cela vous permet de code d’application hello toosecurely accès sur l’application hello web ainsi que les diagnostics des journaux. Il est recommandé de toujours utiliser FTPS au lieu de FTP. 

lien FTPS Hello pour votre application se trouve avec hello comme suit :

1. Ouvrez hello [Azure Portal](https://portal.azure.com).
2. Sélectionnez **Parcourir tout**.
3. À partir de hello **Parcourir** panneau, sélectionnez **des Services d’application**.
4. À partir de hello **des Services d’application** panneau, sélectionnez hello des application souhaitée.
5. Dans le panneau de l’application hello, sélectionnez **tous les paramètres**.
6. À partir de hello **paramètres** panneau, sélectionnez **propriétés**.
7. les liens FTP et FTPS Hello sont fournis sur hello **paramètres** panneau. 

Pour plus d'informations sur FTPS, consultez la page [Protocole FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la sécurité de hello Hello plateforme Azure, les informations sur les rapports d’un **incident de sécurité ou les abus**, ou tooinform Microsoft que vous allez effectuer **des tests d’intrusion** de votre de site, consultez la section sécurité hello hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Pour plus d’informations sur les fichiers **web.config** ou **applicationhost.config** des applications App Service, consultez la page [Options de configuration déverrouillées dans les applications web Azure App Service](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/).

Pour plus d’informations sur la journalisation des informations des applications App Service, également utile pour détecter les attaques, consultez la page [Activer la journalisation des diagnostics](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

