---
title: "technologies d’aaaOpen source Foire aux questions pour Azure web apps | Documents Microsoft"
description: "Obtenir elles sonttrop des réponses aux questions sur les technologies open source dans la fonctionnalité d’applications Web hello du Service d’applications Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a>FAQ sur les technologies open source pour Azure Web Apps

Cet article a elles sonttrop des réponses aux questions (FAQ) sur les problèmes avec les technologies open source pour hello [fonctionnalité des applications Web d’Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a>Ma base de données ClearDB est hors service. Comment résoudre ce problème ?

Contactez le [support ClearDB](https://www.cleardb.com/developers/help/support) pour tout problème lié à la base de données. 

Pour les réponses toocommon questions ClearDB, consultez [ClearDB FAQ](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a>Pourquoi ma base de données ClearDB pas n’est pas répertorié dans le portail de hello ?

Si vous créez une base de données ClearDB Bonjour [portail Azure](http://portal.azure.com/), base de données hello n’apparaît pas dans hello [portail Azure classic](http://manage.windowsazure.com/). toowork contourner ce problème, vous pouvez lier manuellement votre application web de toohello de base de données.

De même, si vous créez une base de données ClearDB Bonjour [portail Azure classic](http://manage.windowsazure.com/), vous ne voyez pas votre base de données Bonjour [portail Azure](http://portal.azure.com/). Dans ce cas, aucune solution de contournement n’est disponible. 

Pour plus d’informations, consultez [FAQ sur les bases de données MySQL ClearDB avec Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a>Pourquoi ma base de données ClearDB n’a-t-elle pas été migrée pendant la migration de mon abonnement ?

Lorsque vous effectuez la migration de ressources entre différents abonnements, certaines limitations s’appliquent. Une base de données MySQL ClearDB est un service tiers. Elle n’est donc pas migrée lors de la migration d’un abonnement Azure.

Si vous ne gérez pas la migration de votre base de données MySQL hello avant de migrer vos ressources Azure, votre base de données ClearDB MySQL peut être indisponible. tooavoid cela, tout d’abord, migrer manuellement votre base de données ClearDB et migrer hello abonnement Azure pour votre application web.

Pour plus d’informations, consultez [FAQ sur les bases de données MySQL ClearDB avec Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a>Comment activer PHP journalisation des problèmes PHP tootroubleshoot ?

tooturn journalisation de PHP :

1. Connectez-vous à tooyour [site Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Dans le menu supérieur de hello, sélectionnez **Console de débogage** > **CMD**.
3. Sélectionnez hello **Site** dossier.
4. Sélectionnez hello **wwwroot** dossier.
5. Sélectionnez hello  **+**  icône, puis sélectionnez **nouveau fichier**.
6. Définir le nom de fichier hello trop**. user.ini**.
7. Sélectionnez le crayon hello suivant trop**. user.ini**.
8. Dans le fichier de hello, ajoutez ce code :`log_errors=on`
9. Sélectionnez **Enregistrer**.
10. Sélectionnez le crayon hello suivant trop**wp-config.PHP**.
11. Modifiez toohello de texte hello suivant de code :
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. Bonjour portail Azure, dans le menu application hello web, redémarrez votre application web.

Pour plus d’informations, consultez [Activer les journaux d’erreurs WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a>Comment journaliser les erreurs d’application Python dans des applications hébergées dans App Service ?

erreurs d’application toocapture Python :

1. Bonjour portail Azure, dans votre application web, sélectionnez **paramètres**.
2. Sur hello **paramètres** onglet, sélectionnez **paramètres de l’Application**.
3. Sous **paramètres de l’application**, entrez hello suivant la paire clé/valeur :
    * Clé : WSGI_LOG
    * Valeur : D:\home\site\wwwroot\logs.txt (entrez le nom de fichier de votre choix)

Vous devez maintenant voir des erreurs dans le fichier de logs.txt hello dans le dossier wwwroot de hello.

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a>Comment modifier les version hello Hello application Node.js qui est hébergée dans le Service d’applications ?

version hello toochange hello application Node.js, vous pouvez utiliser une des options suivantes de hello :

*   Bonjour portail Azure, utilisez **paramètres de l’application**.
    1. Dans hello portail Azure, accédez à l’application web tooyour.
    2. Sur hello **paramètres** panneau, sélectionnez **paramètres de l’Application**.
    3. Dans **paramètres de l’application**, vous pouvez inclure WEBSITE_NODE_DEFAULT_VERSION en tant que clé de hello et hello version de Node.js souhaitée en tant que valeur de hello.
    4. Accédez tooyour [console de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
    5. toocheck hello Node.js version, entrez hello de commande suivante :  
   ```
   node -v
   ```
*   Modifier le fichier de iisnode.yml hello. Version de Node.js hello modification dans le fichier de iisnode.yml hello définit uniquement l’environnement d’exécution hello qu’iisnode utilise. Votre cmd Kudu et autres encore utiliseront version Node.js hello qui est définie dans **paramètres de l’application** Bonjour portail Azure.

    tooset hello iisnode.yml créer manuellement un fichier iisnode.yml dans votre dossier racine de l’application. Dans le fichier de hello, inclure hello ligne suivante :
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   Fichier de iisnode.yml hello d’ensemble à l’aide de package.json durant le déploiement de contrôle de code source.
    Hello, processus de déploiement du contrôle source Azure implique hello comme suit :
    1. Déplace le contenu toohello Azure web app.
    2. Crée un script de déploiement par défaut, s’il n’existe pas (deploy.cmd, les fichiers .deployment) dans le dossier racine de hello web app.
    3. Exécute un script de déploiement dans lequel il crée un fichier iisnode.yml si vous indiquez hello Node.js version dans le fichier de package.json hello > moteur`"engines": {"node": "5.9.1","npm": "3.7.3"}`
    4. fichier de iisnode.yml Hello a hello ligne de code suivante :
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a>Je vois le message « Erreur de l’établissement d’une connexion de base de données » de type hello dans mon application WordPress qui est hébergée dans le Service d’applications. Comment puis-je résoudre ce problème ?

Si vous voyez cette erreur dans votre application de Azure WordPress, tooenable php_errors.log et debug.log, les étapes de hello complète détaillées dans [WordPress d’activer les journaux d’erreurs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

Lorsque les journaux de hello sont activées, reproduire l’erreur de hello et vérifiez hello journaux toosee si vous manquez de connexions :
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

Si vous voyez cette erreur dans vos fichiers debug.log ou php_errors.log, votre application dépasse le nombre hello de connexions. Si vous hébergez sur ClearDB, vérifiez le nombre hello de connexions qui sont disponibles dans votre [le plan de service](https://www.cleardb.com/pricing.view).

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a>Comment déboguer une application Node.js hébergée dans App Service ?

1.  Accédez tooyour [console de Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).
2.  Dossier de journaux d’application accédez tooyour (D:\home\LogFiles\Application).
3.  Dans le fichier de logging_errors.txt hello, recherchez le contenu.

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a>Comment installer des modules Python natifs dans une application web App Service ou une application API ?

Certains packages ne peuvent pas être installés à l’aide de PIP dans Azure. package de Hello ne peut-être pas être disponible sur hello Python Package Index ou un compilateur peut être nécessaire (un compilateur n’est pas disponible sur l’ordinateur hello qui exécute l’application hello web dans le Service d’applications). Pour plus d’informations sur l’installation des modules natifs dans App Service Web Apps et API Apps, consultez [Installer des modules Python dans App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a>Comment déployer un tooApp d’application Django Service à l’aide de Git et hello la nouvelle version de Python ?

Pour plus d’informations sur l’installation de Django, consultez [déploiement d’un tooApp d’application Django Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).

## <a name="where-are-hello-tomcat-log-files-located"></a>Où sont hello Tomcat, ces fichiers ?

Pour les déploiements personnalisés et la Place de marché Azure :

* Emplacement du dossier : D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs
* Fichiers d’intérêt :
    * catalina.*aaaa-mm-jj*.log
    * host-manager.*aaaa-mm-jj*.log
    * localhost.*aaaa-mm-jj*.log
    * manager.*aaaa-mm-jj*.log
    * site_access_log.*aaaa-mm-jj*.log


Pour les déploiements **Paramètres de l’application** dans le portail :

* Emplacement du dossier : D:\home\LogFiles
* Fichiers d’intérêt :
    * catalina.*aaaa-mm-jj*.log
    * host-manager.*aaaa-mm-jj*.log
    * localhost.*aaaa-mm-jj*.log
    * manager.*aaaa-mm-jj*.log
    * site_access_log.*aaaa-mm-jj*.log

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a>Comment résoudre les erreurs de connexion du pilote JDBC ?

Vous pouvez voir hello message dans vos journaux Tomcat suivant :

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

Erreur de hello tooresolve :

1. Supprimer le fichier sqljdbc*.jar de hello à partir de votre dossier de bibliothèque d’applications.
2. Si vous utilisez hello Tomcat ou Azure Marketplace Tomcat serveur web personnalisé, copiez ce dossier lib de .jar fichier toohello Tomcat.
3. Si vous activez Java à partir de hello portail Azure (sélectionnez **Java 1.8** > **serveur Tomcat**), fichier de copie hello sqljdbc.* jar dans le dossier hello parallèle tooyour application. Ensuite, ajoutez hello classpath paramètre toohello web.config fichier suivant :

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a>Pourquoi voir des erreurs lorsque je tente de fichiers de journal à la volée toocopy ?

Si vous essayez de fichiers de journal à la volée toocopy pour une application Java (par exemple, Tomcat), vous pouvez rencontrer cette erreur FTP :

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

message d’erreur Hello peut-être varier en fonction du client de hello FTP.

Ce problème de verrouillage concerne toutes les applications Java. Kudu uniquement prend en charge le téléchargement de ce fichier lors de l’application hello est en cours d’exécution.

Arrêt application hello autorise l’accès FTP des fichiers de toothese.

Une autre solution consiste à toowrite une tâche Web qui s’exécute selon une planification et copie ces répertoire de différents fichiers tooa. Pour un exemple de projet, consultez hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) projet.

## <a name="where-do-i-find-hello-log-files-for-jetty"></a>Où trouver des fichiers de journaux hello pour Jetty ?

Pour les déploiements personnalisés et de marché, fichier de journal hello est dans le dossier de D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs hello. Notez qu’emplacement du dossier hello varie selon la version hello de Jetty que vous utilisez. Par exemple, le chemin d’accès de hello fournies ici de Jetty 9.1.2. Recherchez jetty_*AAAA_MM_JJ*.stderrout.log.

Pour les déploiements de paramètre d’application de portail, fichier de journal hello est D:\home\LogFiles. Recherchez jetty_*AAAA_MM_JJ*.stderrout.log

## <a name="can-i-send-email-from-my-azure-web-app"></a>Puis-je envoyer un e-mail à partir de mon application web Azure ?

App Service ne dispose pas d’une fonctionnalité de messagerie intégrée. Consultez cette [discussion sur le dépassement de capacité de la file](http://stackoverflow.com/questions/17666161/sending-email-from-azure) afin d’obtenir des solutions alternatives pour envoyer un e-mail à partir de votre application.

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a>Pourquoi mon site WordPress ne redirige pas les URL tooanother ?

Si vous avez récemment migré tooAzure, WordPress peut rediriger toohello ancienne URL du domaine. Cela est dû à un paramètre dans la base de données MySQL hello.

WordPress Buddy + est une Extension de Site Azure que vous pouvez utiliser l’URL de redirection hello tooupdate directement dans la base de données hello. Pour plus d’informations sur l’utilisation de WordPress Buddy+, consultez [Outils WordPress et migration MySQL avec WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

Vous pouvez également, si vous préférez des URL de redirection hello toomanually mise à jour à l’aide de requêtes SQL ou PHPMyAdmin, consultez [WordPress : redirection des URL de toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a>Comment modifier mon mot de passe de connexion à WordPress ?

Si vous avez oublié votre mot de passe de connexion de le WordPress, vous pouvez utiliser WordPress Buddy + tooupdate il. tooreset votre mot de passe, installez hello WordPress Buddy + Extension de Site Azure et les étapes de hello puis complète décrite dans [WordPress outils et migration de MySQL avec WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a>Je ne parviens pas à se connecter tooWordPress. Comment résoudre ce problème ?

Si vous ne pouvez pas accéder à WordPress après l’installation d’un plug-in, celui-ci est peut-être défectueux. WordPress Buddy+ est une extension de site Azure qui peut vous aider à désactiver des plug-ins dans WordPress. Pour plus d’informations, consultez [Outils WordPress et migration MySQL avec WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="how-do-i-migrate-my-wordpress-database"></a>Comment migrer ma base de données WordPress ?

Vous avez plusieurs options pour la migration hello MySQL de base de données qui est le site Web de WordPress tooyour connecté :

* Développeurs : Hello d’utilisation [invite de commandes ou PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)
* Utilisateurs autres que des développeurs : utilisez [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)

## <a name="how-do-i-help-make-wordpress-more-secure"></a>Comment sécuriser davantage WordPress ?

toolearn sur les meilleures pratiques de sécurité pour WordPress, consultez [meilleures pratiques pour la sécurité de WordPress dans Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a>J’essaie de toouse PHPMyAdmin, et que je vois hello message « Accès refusé ». Comment résoudre ce problème ?

Vous pouvez rencontrer ce problème si la fonctionnalité de hello MySQL dans l’application n’est pas encore exécuté dans cette instance du Service d’applications. tooresolve hello problème, essayez de tooaccess votre site Web. Cela démarre le processus hello requis, y compris les processus hello MySQL dans l’application. tooverify que MySQL dans l’application est en cours d’exécution, dans l’Explorateur de processus, assurez-vous que mysqld.exe est répertorié dans le processus de hello.

Après que vous être assuré que MySQL dans l’application s’exécute, essayez de toouse PHPMyAdmin.

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a>J’obtiens une erreur HTTP 403 lors essayez tooimport ou exporter ma base de données MySQL dans l’application à l’aide de PHPMyadmin. Comment résoudre ce problème ?

Si vous utilisez une version antérieure de Chrome, vous rencontrez sans doute un bogue connu. problème de hello tooresolve, tooa mise à niveau la version plus récente de Chrome. Essayez également à l’aide d’un autre navigateur, comme Internet Explorer ou Edge, où hello ne se produit pas.
