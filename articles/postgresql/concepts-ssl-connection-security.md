---
title: "la connectivité SSL aaaConfigure dans la base de données Azure pour PostgreSQL | Documents Microsoft"
description: "Des instructions et des informations tooconfigure base de données Azure pour PostgreSQL et les applications associées tooproperly utilisent des connexions SSL."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a>Configurer la connectivité SSL dans la base de données Azure pour PostgreSQL
Base de données Azure pour PostgreSQL préfère connexion votre toohello d’applications client service PostgreSQL à l’aide de Secure Sockets Layer (SSL). Application des connexions SSL entre le serveur de base de données et de vos applications clientes vous aide à protéger contre les attaques de « l’homme au milieu de hello » en chiffrant les flux de données hello entre le serveur de hello et votre application.

Par défaut, hello service de base de données PostgreSQL est toorequire configuré SSL connexion. Si vous le souhaitez, vous pouvez désactiver l’utilisation de SSL pour la connexion de service de base de données tooyour si votre application cliente ne prend pas en charge la connectivité SSL. 

## <a name="enforcing-ssl-connections"></a>Appliquer les connexions SSL
Pour toutes les données de Azure pour les serveurs PostgreSQL approvisionnés via hello portail Azure et CLI, mise en œuvre de connexions SSL est activé par défaut. 

De même, les chaînes de connexion qui sont prédéfinis dans les paramètres de « Chaînes de connexion » hello sous votre serveur Bonjour Azure portal incluent des paramètres de hello requis courantes langues tooconnect tooyour serveur de base de l’utilisation de SSL. Hello paramètre SSL varie en fonction de connecteur de hello, par exemple « ssl = true » ou « sslmode = nécessitent » ou « sslmode = requis » et d’autres variations.

## <a name="configure-enforcement-of-ssl"></a>Configuration de l’application du protocole SSL
Si vous le souhaitez, vous pouvez désactiver l’application de la connectivité SSL. Microsoft Azure vous recommande d’activer la tooalways **connexion SSL d’appliquer** définition pour renforcer la sécurité.

### <a name="using-hello-azure-portal"></a>À l’aide de hello portail Azure
Accédez à votre serveur de base de données Azure pour PostgreSQL et cliquez sur **Sécurité de la connexion**. Utilisez tooenable de bouton bascule hello ou désactiver hello **connexion SSL d’appliquer** paramètre. Cliquez ensuite sur **Enregistrer**. 

![Sécurité de connexion - Désactiver l’application de la connexion SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

Vous pouvez vérifier le paramètre de hello en consultant hello **vue d’ensemble** hello toosee de page **SSL appliquer état** indicateur.

### <a name="using-azure-cli"></a>Utilisation de l’interface de ligne de commande Azure
Vous pouvez activer ou désactiver hello **mise en œuvre de ssl** à l’aide du paramètre `Enabled` ou `Disabled` valeurs respectivement dans CLI d’Azure.

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>Vérification que votre application ou votre infrastructure prend en charge les connexions SSL
De nombreuses infrastructures d’applications courantes qui utilisent des services de base de données PostgreSQL, notamment Drupal et Django, n’activent pas le protocole SSL par défaut lors de l’installation. L’activation de la connectivité SSL doit être effectuée après l’installation ou via l’application de toohello spécifique de commandes CLI. Si votre serveur PostgreSQL est en appliquant des connexions SSL et application hello associé n’est pas configurée correctement, application hello peut échouer le serveur de base de données tooconnect tooyour. Toolearn de documentation de votre application, consultez Comment tooenable des connexions SSL.


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>Applications nécessitant la vérification du certificat pour la connectivité SSL
Dans certains cas, les applications nécessitent un fichier de certificat local généré à partir d’un tooconnect de fichier (.cer) du certificat autorité de certification (CA) approuvée en toute sécurité. Consultez hello étapes tooobtain hello .cer fichier suivant, décoder un certificat de hello et liez-le tooyour application.

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a>Télécharger le fichier de certificat hello de hello autorité de certification (CA) 
Hello certificat nécessaire toocommunicate via le protocole SSL avec votre base de données Azure pour PostgreSQL serveur se trouve [ici](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt). Téléchargez le fichier de certificat hello localement.

### <a name="download-and-install-openssl-on-your-machine"></a>Télécharger et installer OpenSSL sur un ordinateur 
fichier de certificat hello toodecode nécessaire pour votre application tooconnect en toute sécurité tooyour serveur de base de données, vous devez tooinstall OpenSSL sur votre ordinateur local.

#### <a name="for-linux-os-x-or-unix"></a>Pour Linux, OS X ou Unix
les bibliothèques OpenSSL Hello sont fournis dans le code source directement à partir de hello [OpenSSL Software Foundation](http://www.openssl.org). Hello instructions suivantes vous guident hello étapes tooinstall nécessaire OpenSSL sur votre ordinateur Linux. Cet article utilise les commandes connus toowork sur Ubuntu 12.04 et versions ultérieures.

Ouvrez une session de terminal et installez OpenSSL.
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
Extraire les fichiers de hello du package de téléchargement hello
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
Entrez le répertoire de hello où les fichiers hello ont été extraits. Par défaut, le résultat se présente ainsi.

```bash
cd openssl-1.1.0e
```
Configurez OpenSSL en exécutant hello commande suivante. Si vous souhaitez que les fichiers hello dans un dossier différent de celui /usr/local/openssl, rendre suivant de hello toochange que le cas échéant.

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
OpenSSL est correctement configuré, vous devez toocompile il tooconvert votre certificat. toocompile, exécutez hello de commande suivante :

```bash
make
```
Une fois la compilation terminée, vous êtes prêt tooinstall OpenSSL comme un fichier exécutable en exécutant hello de commande suivante :
```bash
make install
```
tooconfirm que vous avez correctement installé OpenSSL sur votre système, commande de hello exécution suivante et vérifiez toomake que vous avez hello même sortie.

```bash
/usr/local/openssl/bin/openssl version
```
En cas de réussite, vous devez voir hello message suivant.
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a>Pour Windows
L’installation OpenSSL sur un PC Windows peut être effectué dans hello suivant façons :
1. **(Recommandé)**  à l’aide de hello Bash pour Windows fonctionnalités intégrées de Windows 10 et versions ultérieures, OpenSSL est installé par défaut. Obtenir des instructions sur la façon dont vous trouverez tooenable fonctionnalité Bash pour Windows dans Windows 10 [ici](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).
2. Par le biais du téléchargement une application Win32/64 fournie par la Communauté de hello. Bien que hello OpenSSL Software Foundation ne pas fournir ou recommander des programmes d’installation Windows spécifiques, ils fournissent une liste de programmes d’installation disponibles [ici](https://wiki.openssl.org/index.php/Binaries)

### <a name="decode-your-certificate-file"></a>Décoder le fichier de certificat
Hello téléchargé le fichier est dans un format chiffré de l’autorité de certification racine. Utilisez le fichier de certificat OpenSSL toodecode hello. toodo, exécutez la commande OpenSSL :

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a>TooAzure connexion de base de données PostgreSQL SSL avec authentification par certificat
Maintenant que vous avez correctement décodés votre certificat, vous pouvez maintenant vous connecter serveur de base de données tooyour en toute sécurité via le protocole SSL. vérification de certificat de serveur tooallow, certificat de hello doit être placé dans hello fichier ~/.postgresql/root.crt dans le répertoire de base de l’utilisateur hello. (Sur le fichier de Microsoft Windows hello est nommé % APPDATA%\postgresql\root.crt.). suivant de Hello fournit des instructions pour connecter tooAzure de base de données PostgreSQL.

> [!NOTE]
> Actuellement, il existe un problème connu si vous utilisez « sslmode = vérifier-full » dans votre service toohello de connexion, connexion de hello échouera avec hello l’erreur suivante : _certificat de serveur pour «&lt;région&gt;. Control.Database.Windows.NET » (et les autres noms de 7) ne correspondent pas de nom d’hôte «&lt;nom_serveur&gt;. postgres.database.azure.com »._
> Si « sslmode = vérifier-full » est requis, veuillez utiliser la convention d’affectation de noms de serveur hello  **&lt;nom_serveur&gt;. database.windows.net** en tant que nom hôte de votre chaîne de connexion. Nous prévoyons de tooremove cette limitation Bonjour futures. Connexions à l’aide d’autres [les modes SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) doit continuer de convention d’affectation de noms de toouse hello préféré hôte  **&lt;nom_serveur&gt;. postgres.database.azure.com**.

#### <a name="using-psql-command-line-utility"></a>Avec l’utilitaire de ligne de commande psql
Bonjour à l’exemple suivant vous montre comment toosuccessfully connecter tooyour PostgreSQL serveur est à l’aide d’utilitaire de ligne de commande de psql hello. Hello d’utilisation `root.crt` fichier créé et hello `sslmode=verify-ca` ou `sslmode=verify-full` option.

À l’aide d’une interface de ligne hello PostgreSQL, exécutez hello de commande suivante :
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
En cas de réussite, vous recevez hello suivant de sortie :
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a>Avec l’outil d’interface graphique utilisateur pgAdmin
La configuration pgAdmin 4 tooconnect en toute sécurité via le protocole SSL nécessite tooset hello `SSL mode = Verify-CA` ou `SSL mode = Verify-Full` comme suit :

![Capture d’écran de pgAdmin - connexion - conditions du mode SSL](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a>Étapes suivantes
Passez en revue les différentes options de connectivité d’application de la page [Bibliothèques de connexions de la base de données Azure pour PostgreSQL](concepts-connection-libraries.md).
