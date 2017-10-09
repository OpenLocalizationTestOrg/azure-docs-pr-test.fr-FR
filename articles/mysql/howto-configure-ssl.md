---
title: "aaaConfigure SSL connectivité toosecurely connecter tooAzure de base de données de MySQL | Documents Microsoft"
description: "Instructions pour comment tooproperly configurer la base de données Azure pour toocorrectly d’applications associées et de MySQL utilisent des connexions SSL"
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 8c37c19d4c101abfb730f429a19441e94e52fc85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a>Configurer SSL tooAzure de base de données de connexion de connectivité dans votre application de toosecurely pour MySQL
Base de données Azure pour MySQL prend en charge la connexion de votre base de données Azure pour les applications tooclient de MySQL server à l’aide de Secure Sockets Layer (SSL). Application des connexions SSL entre le serveur de base de données et de vos applications clientes vous aide à protéger contre les attaques de « l’homme au milieu de hello » en chiffrant les flux de données hello entre le serveur de hello et votre application.

## <a name="step-1-obtain-ssl-certificate"></a>Étape 1 : obtention d’un certificat SSL
Télécharger hello certificat nécessaire toocommunicate via le protocole SSL avec votre base de données Azure pour le serveur MySQL de [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) et enregistrez tooyour de fichier de certificat hello local lecteur (dans ce didacticiel, nous avons utilisé c:\ssl).
**Pour Microsoft Internet Explorer et Microsoft Edge :** après hello téléchargement terminé, renommez hello certificat tooBaltimoreCyberTrustRoot.crt.pem.

## <a name="step-2-bind-ssl"></a>Étape 2 : création d’une liaison SSL
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a>Connexion tooserver à l’aide de hello banc d’essai MySQL via le protocole SSL
Configurer le banc d’essai MySQL tooconnect en toute sécurité via le protocole SSL. Accédez toohello **SSL** onglet Bonjour banc d’essai MySQL sur hello boîte de dialogue de connexion de nouveau le programme d’installation. Entrez l’emplacement du fichier hello Hello **BaltimoreCyberTrustRoot.crt.pem** Bonjour **fichier d’autorité de certification SSL :** champ.
![Enregistrement d’une mosaïque personnalisée](./media/howto-configure-ssl/mysql-workbench-ssl.png)

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a>Connexion tooserver à l’aide de hello MySQL CLI via le protocole SSL
À l’aide d’une interface de ligne hello MySQL, exécutez hello de commande suivante :
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a>Étape 3 : application des connexions SSL dans Azure 
### <a name="using-azure-portal"></a>En passant par le portail Azure
À l’aide de hello portail Azure, rendez-vous sur votre base de données Azure pour MySQL server et cliquez sur **sécurité de connexion**. Utilisez tooenable de bouton bascule hello ou désactiver hello **connexion SSL d’appliquer** paramètre. Cliquez ensuite sur **Enregistrer**. Microsoft vous recommande d’activer la tooalways **connexion SSL d’appliquer** définition pour renforcer la sécurité.
![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)

### <a name="using-azure-cli"></a>Utilisation de l’interface de ligne de commande Azure
Vous pouvez activer ou désactiver hello **mise en œuvre de ssl** paramètre à l’aide des valeurs activé ou désactivé, respectivement dans CLI d’Azure.
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a>Étape 4 : vérification de votre connexion SSL
Exécutez hello mysql **état** tooverify de commande que vous avez connecté tooyour MySQL server à l’aide de SSL :
```dos
mysql> status
```
Vérifiez la connexion de hello est chiffrée en examinant la sortie de hello. Elle doit indiquer : **SSL: Cipher in use is AES256-SHA** (SSL : le chiffrement utilisé est AES256-SHA). 

## <a name="sample-code"></a>Exemple de code
### <a name="php"></a>PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a>Python
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a>Étapes suivantes
Passez en revue les différentes options de connectivité d’application de la rubrique [Bibliothèques de connexions pour Azure Database pour MySQL](concepts-connection-libraries.md)
