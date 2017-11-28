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
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="c844b-103">Configurer la connectivité SSL dans la base de données Azure pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="c844b-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="c844b-104">Base de données Azure pour PostgreSQL préfère connexion votre toohello d’applications client service PostgreSQL à l’aide de Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="c844b-104">Azure Database for PostgreSQL prefers connecting your client applications toohello PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="c844b-105">Application des connexions SSL entre le serveur de base de données et de vos applications clientes vous aide à protéger contre les attaques de « l’homme au milieu de hello » en chiffrant les flux de données hello entre le serveur de hello et votre application.</span><span class="sxs-lookup"><span data-stu-id="c844b-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

<span data-ttu-id="c844b-106">Par défaut, hello service de base de données PostgreSQL est toorequire configuré SSL connexion.</span><span class="sxs-lookup"><span data-stu-id="c844b-106">By default, hello PostgreSQL database service is configured toorequire SSL connection.</span></span> <span data-ttu-id="c844b-107">Si vous le souhaitez, vous pouvez désactiver l’utilisation de SSL pour la connexion de service de base de données tooyour si votre application cliente ne prend pas en charge la connectivité SSL.</span><span class="sxs-lookup"><span data-stu-id="c844b-107">Optionally, you can disable requiring SSL for connecting tooyour database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="c844b-108">Appliquer les connexions SSL</span><span class="sxs-lookup"><span data-stu-id="c844b-108">Enforcing SSL connections</span></span>
<span data-ttu-id="c844b-109">Pour toutes les données de Azure pour les serveurs PostgreSQL approvisionnés via hello portail Azure et CLI, mise en œuvre de connexions SSL est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="c844b-109">For all Azure Database for PostgreSQL servers provisioned through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="c844b-110">De même, les chaînes de connexion qui sont prédéfinis dans les paramètres de « Chaînes de connexion » hello sous votre serveur Bonjour Azure portal incluent des paramètres de hello requis courantes langues tooconnect tooyour serveur de base de l’utilisation de SSL.</span><span class="sxs-lookup"><span data-stu-id="c844b-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="c844b-111">Hello paramètre SSL varie en fonction de connecteur de hello, par exemple « ssl = true » ou « sslmode = nécessitent » ou « sslmode = requis » et d’autres variations.</span><span class="sxs-lookup"><span data-stu-id="c844b-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="c844b-112">Configuration de l’application du protocole SSL</span><span class="sxs-lookup"><span data-stu-id="c844b-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="c844b-113">Si vous le souhaitez, vous pouvez désactiver l’application de la connectivité SSL.</span><span class="sxs-lookup"><span data-stu-id="c844b-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="c844b-114">Microsoft Azure vous recommande d’activer la tooalways **connexion SSL d’appliquer** définition pour renforcer la sécurité.</span><span class="sxs-lookup"><span data-stu-id="c844b-114">Microsoft Azure recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="c844b-115">À l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c844b-115">Using hello Azure portal</span></span>
<span data-ttu-id="c844b-116">Accédez à votre serveur de base de données Azure pour PostgreSQL et cliquez sur **Sécurité de la connexion**.</span><span class="sxs-lookup"><span data-stu-id="c844b-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="c844b-117">Utilisez tooenable de bouton bascule hello ou désactiver hello **connexion SSL d’appliquer** paramètre.</span><span class="sxs-lookup"><span data-stu-id="c844b-117">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="c844b-118">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c844b-118">Then click **Save**.</span></span> 

![Sécurité de connexion - Désactiver l’application de la connexion SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="c844b-120">Vous pouvez vérifier le paramètre de hello en consultant hello **vue d’ensemble** hello toosee de page **SSL appliquer état** indicateur.</span><span class="sxs-lookup"><span data-stu-id="c844b-120">You can confirm hello setting by viewing hello **Overview** page toosee hello **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="c844b-121">Utilisation de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c844b-121">Using Azure CLI</span></span>
<span data-ttu-id="c844b-122">Vous pouvez activer ou désactiver hello **mise en œuvre de ssl** à l’aide du paramètre `Enabled` ou `Disabled` valeurs respectivement dans CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="c844b-122">You can enable or disable hello **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="c844b-123">Vérification que votre application ou votre infrastructure prend en charge les connexions SSL</span><span class="sxs-lookup"><span data-stu-id="c844b-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="c844b-124">De nombreuses infrastructures d’applications courantes qui utilisent des services de base de données PostgreSQL, notamment Drupal et Django, n’activent pas le protocole SSL par défaut lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="c844b-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="c844b-125">L’activation de la connectivité SSL doit être effectuée après l’installation ou via l’application de toohello spécifique de commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="c844b-125">Enabling SSL connectivity must be done after installation or through CLI commands specific toohello application.</span></span> <span data-ttu-id="c844b-126">Si votre serveur PostgreSQL est en appliquant des connexions SSL et application hello associé n’est pas configurée correctement, application hello peut échouer le serveur de base de données tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="c844b-126">If your PostgreSQL server is enforcing SSL connections and hello associated application is not configured properly, hello application may fail tooconnect tooyour database server.</span></span> <span data-ttu-id="c844b-127">Toolearn de documentation de votre application, consultez Comment tooenable des connexions SSL.</span><span class="sxs-lookup"><span data-stu-id="c844b-127">Consult your application's documentation toolearn how tooenable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="c844b-128">Applications nécessitant la vérification du certificat pour la connectivité SSL</span><span class="sxs-lookup"><span data-stu-id="c844b-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="c844b-129">Dans certains cas, les applications nécessitent un fichier de certificat local généré à partir d’un tooconnect de fichier (.cer) du certificat autorité de certification (CA) approuvée en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="c844b-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) tooconnect securely.</span></span> <span data-ttu-id="c844b-130">Consultez hello étapes tooobtain hello .cer fichier suivant, décoder un certificat de hello et liez-le tooyour application.</span><span class="sxs-lookup"><span data-stu-id="c844b-130">See hello following steps tooobtain hello .cer file, decode hello certificate and bind it tooyour application.</span></span>

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a><span data-ttu-id="c844b-131">Télécharger le fichier de certificat hello de hello autorité de certification (CA)</span><span class="sxs-lookup"><span data-stu-id="c844b-131">Download hello certificate file from hello Certificate Authority (CA)</span></span> 
<span data-ttu-id="c844b-132">Hello certificat nécessaire toocommunicate via le protocole SSL avec votre base de données Azure pour PostgreSQL serveur se trouve [ici](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="c844b-132">hello certificate needed toocommunicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="c844b-133">Téléchargez le fichier de certificat hello localement.</span><span class="sxs-lookup"><span data-stu-id="c844b-133">Download hello certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="c844b-134">Télécharger et installer OpenSSL sur un ordinateur</span><span class="sxs-lookup"><span data-stu-id="c844b-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="c844b-135">fichier de certificat hello toodecode nécessaire pour votre application tooconnect en toute sécurité tooyour serveur de base de données, vous devez tooinstall OpenSSL sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="c844b-135">toodecode hello certificate file needed for your application tooconnect securely tooyour database server, you need tooinstall OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="c844b-136">Pour Linux, OS X ou Unix</span><span class="sxs-lookup"><span data-stu-id="c844b-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="c844b-137">les bibliothèques OpenSSL Hello sont fournis dans le code source directement à partir de hello [OpenSSL Software Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="c844b-137">hello OpenSSL libraries are provided in source code directly from hello [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="c844b-138">Hello instructions suivantes vous guident hello étapes tooinstall nécessaire OpenSSL sur votre ordinateur Linux.</span><span class="sxs-lookup"><span data-stu-id="c844b-138">hello following instructions guide you through hello steps necessary tooinstall OpenSSL on your Linux PC.</span></span> <span data-ttu-id="c844b-139">Cet article utilise les commandes connus toowork sur Ubuntu 12.04 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="c844b-139">This article uses commands known toowork on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="c844b-140">Ouvrez une session de terminal et installez OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="c844b-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="c844b-141">Extraire les fichiers de hello du package de téléchargement hello</span><span class="sxs-lookup"><span data-stu-id="c844b-141">Extract hello files from hello download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="c844b-142">Entrez le répertoire de hello où les fichiers hello ont été extraits.</span><span class="sxs-lookup"><span data-stu-id="c844b-142">Enter hello directory where hello files were extracted.</span></span> <span data-ttu-id="c844b-143">Par défaut, le résultat se présente ainsi.</span><span class="sxs-lookup"><span data-stu-id="c844b-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="c844b-144">Configurez OpenSSL en exécutant hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="c844b-144">Configure OpenSSL by executing hello following command.</span></span> <span data-ttu-id="c844b-145">Si vous souhaitez que les fichiers hello dans un dossier différent de celui /usr/local/openssl, rendre suivant de hello toochange que le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="c844b-145">If you want hello files in a folder different than /usr/local/openssl, make sure toochange hello following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="c844b-146">OpenSSL est correctement configuré, vous devez toocompile il tooconvert votre certificat.</span><span class="sxs-lookup"><span data-stu-id="c844b-146">Now that OpenSSL is configured properly, you need toocompile it tooconvert your certificate.</span></span> <span data-ttu-id="c844b-147">toocompile, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c844b-147">toocompile, run hello following command:</span></span>

```bash
make
```
<span data-ttu-id="c844b-148">Une fois la compilation terminée, vous êtes prêt tooinstall OpenSSL comme un fichier exécutable en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c844b-148">Once compiling is complete, you're ready tooinstall OpenSSL as an executable by running hello following command:</span></span>
```bash
make install
```
<span data-ttu-id="c844b-149">tooconfirm que vous avez correctement installé OpenSSL sur votre système, commande de hello exécution suivante et vérifiez toomake que vous avez hello même sortie.</span><span class="sxs-lookup"><span data-stu-id="c844b-149">tooconfirm that you've successfully installed OpenSSL on your system, run hello following command and check toomake sure you get hello same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="c844b-150">En cas de réussite, vous devez voir hello message suivant.</span><span class="sxs-lookup"><span data-stu-id="c844b-150">If successful you should see hello following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="c844b-151">Pour Windows</span><span class="sxs-lookup"><span data-stu-id="c844b-151">For Windows</span></span>
<span data-ttu-id="c844b-152">L’installation OpenSSL sur un PC Windows peut être effectué dans hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="c844b-152">Installing OpenSSL on a Windows PC can be done in hello following ways:</span></span>
1. <span data-ttu-id="c844b-153">**(Recommandé)**  à l’aide de hello Bash pour Windows fonctionnalités intégrées de Windows 10 et versions ultérieures, OpenSSL est installé par défaut.</span><span class="sxs-lookup"><span data-stu-id="c844b-153">**(Recommended)** Using hello built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="c844b-154">Obtenir des instructions sur la façon dont vous trouverez tooenable fonctionnalité Bash pour Windows dans Windows 10 [ici](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="c844b-154">Instructions on how tooenable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="c844b-155">Par le biais du téléchargement une application Win32/64 fournie par la Communauté de hello.</span><span class="sxs-lookup"><span data-stu-id="c844b-155">Through downloading a Win32/64 application provided by hello community.</span></span> <span data-ttu-id="c844b-156">Bien que hello OpenSSL Software Foundation ne pas fournir ou recommander des programmes d’installation Windows spécifiques, ils fournissent une liste de programmes d’installation disponibles [ici](https://wiki.openssl.org/index.php/Binaries)</span><span class="sxs-lookup"><span data-stu-id="c844b-156">While hello OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="c844b-157">Décoder le fichier de certificat</span><span class="sxs-lookup"><span data-stu-id="c844b-157">Decode your certificate file</span></span>
<span data-ttu-id="c844b-158">Hello téléchargé le fichier est dans un format chiffré de l’autorité de certification racine.</span><span class="sxs-lookup"><span data-stu-id="c844b-158">hello downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="c844b-159">Utilisez le fichier de certificat OpenSSL toodecode hello.</span><span class="sxs-lookup"><span data-stu-id="c844b-159">Use OpenSSL toodecode hello certificate file.</span></span> <span data-ttu-id="c844b-160">toodo, exécutez la commande OpenSSL :</span><span class="sxs-lookup"><span data-stu-id="c844b-160">toodo so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="c844b-161">TooAzure connexion de base de données PostgreSQL SSL avec authentification par certificat</span><span class="sxs-lookup"><span data-stu-id="c844b-161">Connecting tooAzure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="c844b-162">Maintenant que vous avez correctement décodés votre certificat, vous pouvez maintenant vous connecter serveur de base de données tooyour en toute sécurité via le protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="c844b-162">Now that you have successfully decoded your certificate, you can now connect tooyour database server securely over SSL.</span></span> <span data-ttu-id="c844b-163">vérification de certificat de serveur tooallow, certificat de hello doit être placé dans hello fichier ~/.postgresql/root.crt dans le répertoire de base de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="c844b-163">tooallow server certificate verification, hello certificate must be placed in hello file ~/.postgresql/root.crt in hello user's home directory.</span></span> <span data-ttu-id="c844b-164">(Sur le fichier de Microsoft Windows hello est nommé % APPDATA%\postgresql\root.crt.).</span><span class="sxs-lookup"><span data-stu-id="c844b-164">(On Microsoft Windows hello file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="c844b-165">suivant de Hello fournit des instructions pour connecter tooAzure de base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c844b-165">hello following provides instructions for connecting tooAzure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="c844b-166">Actuellement, il existe un problème connu si vous utilisez « sslmode = vérifier-full » dans votre service toohello de connexion, connexion de hello échouera avec hello l’erreur suivante : _certificat de serveur pour «&lt;région&gt;. Control.Database.Windows.NET » (et les autres noms de 7) ne correspondent pas de nom d’hôte «&lt;nom_serveur&gt;. postgres.database.azure.com »._</span><span class="sxs-lookup"><span data-stu-id="c844b-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection toohello service, hello connection will fail with hello following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="c844b-167">Si « sslmode = vérifier-full » est requis, veuillez utiliser la convention d’affectation de noms de serveur hello  **&lt;nom_serveur&gt;. database.windows.net** en tant que nom hôte de votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="c844b-167">If "sslmode=verify-full" is required, please use hello server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="c844b-168">Nous prévoyons de tooremove cette limitation Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="c844b-168">We plan tooremove this limitation in hello future.</span></span> <span data-ttu-id="c844b-169">Connexions à l’aide d’autres [les modes SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) doit continuer de convention d’affectation de noms de toouse hello préféré hôte  **&lt;nom_serveur&gt;. postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="c844b-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue toouse hello preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="c844b-170">Avec l’utilitaire de ligne de commande psql</span><span class="sxs-lookup"><span data-stu-id="c844b-170">Using psql command-line utility</span></span>
<span data-ttu-id="c844b-171">Bonjour à l’exemple suivant vous montre comment toosuccessfully connecter tooyour PostgreSQL serveur est à l’aide d’utilitaire de ligne de commande de psql hello.</span><span class="sxs-lookup"><span data-stu-id="c844b-171">hello following example shows you how toosuccessfully connect tooyour PostgreSQL server using hello psql command-line utility.</span></span> <span data-ttu-id="c844b-172">Hello d’utilisation `root.crt` fichier créé et hello `sslmode=verify-ca` ou `sslmode=verify-full` option.</span><span class="sxs-lookup"><span data-stu-id="c844b-172">Use hello `root.crt` file created and hello `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="c844b-173">À l’aide d’une interface de ligne hello PostgreSQL, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c844b-173">Using hello PostgreSQL command-line interface, execute hello following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="c844b-174">En cas de réussite, vous recevez hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="c844b-174">If successful, you receive hello following output:</span></span>
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

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="c844b-175">Avec l’outil d’interface graphique utilisateur pgAdmin</span><span class="sxs-lookup"><span data-stu-id="c844b-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="c844b-176">La configuration pgAdmin 4 tooconnect en toute sécurité via le protocole SSL nécessite tooset hello `SSL mode = Verify-CA` ou `SSL mode = Verify-Full` comme suit :</span><span class="sxs-lookup"><span data-stu-id="c844b-176">Configuring pgAdmin 4 tooconnect securely over SSL requires you tooset hello `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Capture d’écran de pgAdmin - connexion - conditions du mode SSL](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="c844b-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c844b-178">Next steps</span></span>
<span data-ttu-id="c844b-179">Passez en revue les différentes options de connectivité d’application de la page [Bibliothèques de connexions de la base de données Azure pour PostgreSQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="c844b-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
