---
title: "Connexion d’applications à la base de données Azure pour MySQL | Microsoft Docs"
description: "Ce document répertorie les chaînes de connexion actuellement prises en charge pour les applications qui se connectent à la base de données Azure pour MySQL, notamment ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python et Ruby."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: 2f40da41bcfda7e35f6fc63ead5d055246ab390c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-applications-to-azure-database-for-mysql"></a><span data-ttu-id="472e5-103">Connexion d’applications à Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="472e5-103">How to connect applications to Azure Database for MySQL</span></span>
<span data-ttu-id="472e5-104">Ce document répertorie les types de chaînes de connexion pris en charge par la base de données Azure pour MySQL, ainsi que des modèles et des exemples.</span><span class="sxs-lookup"><span data-stu-id="472e5-104">This document lists the connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="472e5-105">Vous pouvez avoir des paramètres et des réglages différents dans votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="472e5-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="472e5-106">Pour obtenir le certificat, consultez [Configuration de la connectivité SSL dans votre application pour se connecter en toute sécurité à la base de données Azure pour MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="472e5-106">To obtain the certificate, see [How to configure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="472e5-107">{votre_hôte} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="472e5-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="472e5-108">{votre_utilisateur}@{nomserveur} = format ID utilisateur pour une authentification correcte.</span><span class="sxs-lookup"><span data-stu-id="472e5-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="472e5-109">L’authentification échouera si vous utilisez uniquement l’ID utilisateur.</span><span class="sxs-lookup"><span data-stu-id="472e5-109">Using just the userID will cause the authentication to fail.</span></span>

## <a name="adonet"></a><span data-ttu-id="472e5-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="472e5-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="472e5-111">Dans cet exemple, le nom du serveur est `myserver4demo`, le nom de la base de données est `wpdb`, le nom d’utilisateur est `WPAdmin` et le mot de passe est `mypassword!2`.</span><span class="sxs-lookup"><span data-stu-id="472e5-111">In this example, the server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="472e5-112">La chaîne de connexion devrait être :</span><span class="sxs-lookup"><span data-stu-id="472e5-112">Then, the connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="472e5-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="472e5-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="472e5-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="472e5-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="472e5-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="472e5-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="472e5-116">PHP</span><span class="sxs-lookup"><span data-stu-id="472e5-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="472e5-117">Python</span><span class="sxs-lookup"><span data-stu-id="472e5-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="472e5-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="472e5-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-the-connection-string-details-from-the-azure-portal"></a><span data-ttu-id="472e5-119">Obtenir les détails de la chaîne de connexion dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="472e5-119">Get the connection string details from the Azure portal</span></span>
<span data-ttu-id="472e5-120">Dans le [portail Azure](https://portal.azure.com), accédez à la base de données Azure pour MySQL Server, puis cliquez sur **Chaînes de connexion** pour obtenir la liste des chaînes de votre instance : ![Le panneau Chaînes de connexion dans le portail Azure](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="472e5-120">In the [Azure portal](https://portal.azure.com), go to your Azure Database for MySQL server, and then click **Connection strings** to get your string list for your instance: ![The Connection strings pane in the Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="472e5-121">La chaîne fournit des détails tels que le pilote, le serveur et d’autres paramètres de connexion de base de données.</span><span class="sxs-lookup"><span data-stu-id="472e5-121">The string provides details such as the driver, server, and other database connection parameters.</span></span> <span data-ttu-id="472e5-122">Modifiez ces exemples en utilisant vos propres paramètres, tels que le nom de la base de données, le mot de passe, etc.</span><span class="sxs-lookup"><span data-stu-id="472e5-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="472e5-123">Vous pouvez ensuite utiliser cette chaîne pour vous connecter au serveur à partir de votre code et de vos applications.</span><span class="sxs-lookup"><span data-stu-id="472e5-123">You can then use this string to connect to the server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="472e5-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="472e5-124">Next steps</span></span>
- <span data-ttu-id="472e5-125">Pour plus d’informations sur les bibliothèques de connexions, consultez [Concepts - Bibliothèques de connexions](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="472e5-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
