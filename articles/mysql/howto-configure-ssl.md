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
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a><span data-ttu-id="7b929-103">Configurer SSL tooAzure de base de données de connexion de connectivité dans votre application de toosecurely pour MySQL</span><span class="sxs-lookup"><span data-stu-id="7b929-103">Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL</span></span>
<span data-ttu-id="7b929-104">Base de données Azure pour MySQL prend en charge la connexion de votre base de données Azure pour les applications tooclient de MySQL server à l’aide de Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="7b929-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="7b929-105">Application des connexions SSL entre le serveur de base de données et de vos applications clientes vous aide à protéger contre les attaques de « l’homme au milieu de hello » en chiffrant les flux de données hello entre le serveur de hello et votre application.</span><span class="sxs-lookup"><span data-stu-id="7b929-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="7b929-106">Étape 1 : obtention d’un certificat SSL</span><span class="sxs-lookup"><span data-stu-id="7b929-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="7b929-107">Télécharger hello certificat nécessaire toocommunicate via le protocole SSL avec votre base de données Azure pour le serveur MySQL de [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) et enregistrez tooyour de fichier de certificat hello local lecteur (dans ce didacticiel, nous avons utilisé c:\ssl).</span><span class="sxs-lookup"><span data-stu-id="7b929-107">Download hello certificate needed toocommunicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save hello certificate file tooyour local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="7b929-108">**Pour Microsoft Internet Explorer et Microsoft Edge :** après hello téléchargement terminé, renommez hello certificat tooBaltimoreCyberTrustRoot.crt.pem.</span><span class="sxs-lookup"><span data-stu-id="7b929-108">**For Microsoft Internet Explorer and Microsoft Edge:** After hello download has completed, rename hello certificate tooBaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="7b929-109">Étape 2 : création d’une liaison SSL</span><span class="sxs-lookup"><span data-stu-id="7b929-109">Step 2: Bind SSL</span></span>
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a><span data-ttu-id="7b929-110">Connexion tooserver à l’aide de hello banc d’essai MySQL via le protocole SSL</span><span class="sxs-lookup"><span data-stu-id="7b929-110">Connecting tooserver using hello MySQL Workbench over SSL</span></span>
<span data-ttu-id="7b929-111">Configurer le banc d’essai MySQL tooconnect en toute sécurité via le protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="7b929-111">Configure MySQL Workbench tooconnect securely over SSL.</span></span> <span data-ttu-id="7b929-112">Accédez toohello **SSL** onglet Bonjour banc d’essai MySQL sur hello boîte de dialogue de connexion de nouveau le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="7b929-112">Navigate toohello **SSL** tab in hello MySQL Workbench on hello Setup New Connection dialogue.</span></span> <span data-ttu-id="7b929-113">Entrez l’emplacement du fichier hello Hello **BaltimoreCyberTrustRoot.crt.pem** Bonjour **fichier d’autorité de certification SSL :** champ.</span><span class="sxs-lookup"><span data-stu-id="7b929-113">Enter hello file location of hello **BaltimoreCyberTrustRoot.crt.pem** in hello **SSL CA File:** field.</span></span>
<span data-ttu-id="7b929-114">![Enregistrement d’une mosaïque personnalisée](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="7b929-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a><span data-ttu-id="7b929-115">Connexion tooserver à l’aide de hello MySQL CLI via le protocole SSL</span><span class="sxs-lookup"><span data-stu-id="7b929-115">Connecting tooserver using hello MySQL CLI over SSL</span></span>
<span data-ttu-id="7b929-116">À l’aide d’une interface de ligne hello MySQL, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7b929-116">Using hello MySQL command-line interface, execute hello following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="7b929-117">Étape 3 : application des connexions SSL dans Azure</span><span class="sxs-lookup"><span data-stu-id="7b929-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="7b929-118">En passant par le portail Azure</span><span class="sxs-lookup"><span data-stu-id="7b929-118">Using Azure portal</span></span>
<span data-ttu-id="7b929-119">À l’aide de hello portail Azure, rendez-vous sur votre base de données Azure pour MySQL server et cliquez sur **sécurité de connexion**.</span><span class="sxs-lookup"><span data-stu-id="7b929-119">Using hello Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="7b929-120">Utilisez tooenable de bouton bascule hello ou désactiver hello **connexion SSL d’appliquer** paramètre.</span><span class="sxs-lookup"><span data-stu-id="7b929-120">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="7b929-121">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7b929-121">Then click **Save**.</span></span> <span data-ttu-id="7b929-122">Microsoft vous recommande d’activer la tooalways **connexion SSL d’appliquer** définition pour renforcer la sécurité.</span><span class="sxs-lookup"><span data-stu-id="7b929-122">Microsoft recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="7b929-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="7b929-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="7b929-124">Utilisation de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="7b929-124">Using Azure CLI</span></span>
<span data-ttu-id="7b929-125">Vous pouvez activer ou désactiver hello **mise en œuvre de ssl** paramètre à l’aide des valeurs activé ou désactivé, respectivement dans CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="7b929-125">You can enable or disable hello **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="7b929-126">Étape 4 : vérification de votre connexion SSL</span><span class="sxs-lookup"><span data-stu-id="7b929-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="7b929-127">Exécutez hello mysql **état** tooverify de commande que vous avez connecté tooyour MySQL server à l’aide de SSL :</span><span class="sxs-lookup"><span data-stu-id="7b929-127">Execute hello mysql **status** command tooverify that you have connected tooyour MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="7b929-128">Vérifiez la connexion de hello est chiffrée en examinant la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="7b929-128">Confirm hello connection is encrypted by reviewing hello output.</span></span> <span data-ttu-id="7b929-129">Elle doit indiquer : **SSL: Cipher in use is AES256-SHA** (SSL : le chiffrement utilisé est AES256-SHA).</span><span class="sxs-lookup"><span data-stu-id="7b929-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="7b929-130">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="7b929-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="7b929-131">PHP</span><span class="sxs-lookup"><span data-stu-id="7b929-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="7b929-132">Python</span><span class="sxs-lookup"><span data-stu-id="7b929-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="7b929-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7b929-133">Next steps</span></span>
<span data-ttu-id="7b929-134">Passez en revue les différentes options de connectivité d’application de la rubrique [Bibliothèques de connexions pour Azure Database pour MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="7b929-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
