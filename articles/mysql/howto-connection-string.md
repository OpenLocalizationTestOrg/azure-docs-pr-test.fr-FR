---
title: "applications d’aaaConnect tooAzure base de données MySQL | Documents Microsoft"
description: "Ce document répertorie les chaînes de connexion hello actuellement pris en charge pour les applications tooconnect avec la base de données Azure pour MySQL, y compris ADO.NET (c#), JDBC, Node.js, ODBC, PHP, Python et Ruby."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a><span data-ttu-id="d11a4-103">Comment tooconnect applications tooAzure de base de données MySQL</span><span class="sxs-lookup"><span data-stu-id="d11a4-103">How tooconnect applications tooAzure Database for MySQL</span></span>
<span data-ttu-id="d11a4-104">Ce document répertorie les types de chaîne de connexion de hello sont pris en charge par la base de données Azure pour MySQL, ainsi que des modèles et des exemples.</span><span class="sxs-lookup"><span data-stu-id="d11a4-104">This document lists hello connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="d11a4-105">Vous pouvez avoir des paramètres et des réglages différents dans votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="d11a4-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="d11a4-106">certificat de hello tooobtain, consultez [comment tooconfigure SSL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="d11a4-106">tooobtain hello certificate, see [How tooconfigure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="d11a4-107">{votre_hôte} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="d11a4-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="d11a4-108">{votre_utilisateur}@{nomserveur} = format ID utilisateur pour une authentification correcte.</span><span class="sxs-lookup"><span data-stu-id="d11a4-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="d11a4-109">L’utilisation de simplement hello userID entraîne hello authentification toofail.</span><span class="sxs-lookup"><span data-stu-id="d11a4-109">Using just hello userID will cause hello authentication toofail.</span></span>

## <a name="adonet"></a><span data-ttu-id="d11a4-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="d11a4-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="d11a4-111">Dans cet exemple, le nom du serveur hello est `myserver4demo`, nom de la base de données est `wpdb`, nom d’utilisateur est `WPAdmin`, et le mot de passe est `mypassword!2`.</span><span class="sxs-lookup"><span data-stu-id="d11a4-111">In this example, hello server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="d11a4-112">Ensuite, la chaîne de connexion hello doit être :</span><span class="sxs-lookup"><span data-stu-id="d11a4-112">Then, hello connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="d11a4-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="d11a4-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="d11a4-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="d11a4-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="d11a4-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="d11a4-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="d11a4-116">PHP</span><span class="sxs-lookup"><span data-stu-id="d11a4-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="d11a4-117">Python</span><span class="sxs-lookup"><span data-stu-id="d11a4-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="d11a4-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="d11a4-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a><span data-ttu-id="d11a4-119">Obtenir des détails de la chaîne de connexion de hello de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d11a4-119">Get hello connection string details from hello Azure portal</span></span>
<span data-ttu-id="d11a4-120">Bonjour [portail Azure](https://portal.azure.com), accédez tooyour base de données Azure pour le serveur MySQL, puis cliquez sur **les chaînes de connexion** tooget votre chaîne de liste de l’instance : ![volet de chaînes de connexion hello Bonjour Portail Azure](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="d11a4-120">In hello [Azure portal](https://portal.azure.com), go tooyour Azure Database for MySQL server, and then click **Connection strings** tooget your string list for your instance: ![hello Connection strings pane in hello Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="d11a4-121">chaîne de Hello fournit des détails tels que les pilotes de hello, serveur et autres paramètres de connexion de base de données.</span><span class="sxs-lookup"><span data-stu-id="d11a4-121">hello string provides details such as hello driver, server, and other database connection parameters.</span></span> <span data-ttu-id="d11a4-122">Modifiez ces exemples en utilisant vos propres paramètres, tels que le nom de la base de données, le mot de passe, etc.</span><span class="sxs-lookup"><span data-stu-id="d11a4-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="d11a4-123">Vous pouvez ensuite utiliser ce serveur de toohello tooconnect chaîne à partir de votre code et les applications.</span><span class="sxs-lookup"><span data-stu-id="d11a4-123">You can then use this string tooconnect toohello server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d11a4-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d11a4-124">Next steps</span></span>
- <span data-ttu-id="d11a4-125">Pour plus d’informations sur les bibliothèques de connexions, consultez [Concepts - Bibliothèques de connexions](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="d11a4-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
