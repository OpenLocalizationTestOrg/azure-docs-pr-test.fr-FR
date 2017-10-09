---
title: "Se connecter tooAzure de base de données de MySQL à partir de C++ | Documents Microsoft"
description: "Ce démarrage rapide fournit un exemple de code C++, vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour MySQL."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a><span data-ttu-id="fac4b-103">Base de données Azure pour MySQL : utiliser Connecteur/C++ tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="fac4b-103">Azure Database for MySQL: Use Connector/C++ tooconnect and query data</span></span>
<span data-ttu-id="fac4b-104">Ce démarrage rapide montre comment tooconnect tooan Azure de base de données MySQL à l’aide d’une application C++.</span><span class="sxs-lookup"><span data-stu-id="fac4b-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="fac4b-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="fac4b-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="fac4b-106">Hello étapes décrites dans cet article supposent que vous êtes familiarisé avec le développement à l’aide de C++, et que vous êtes tooworking nouvelle base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="fac4b-106">hello steps in this article assume that you are familiar with developing using C++, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fac4b-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fac4b-107">Prerequisites</span></span>
<span data-ttu-id="fac4b-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="fac4b-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="fac4b-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="fac4b-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="fac4b-110">Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fac4b-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="fac4b-111">Il vous faudra également :</span><span class="sxs-lookup"><span data-stu-id="fac4b-111">You also need to:</span></span>
- <span data-ttu-id="fac4b-112">Installer [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="fac4b-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="fac4b-113">Installez [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="fac4b-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="fac4b-114">Installer [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="fac4b-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="fac4b-115">Installer [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="fac4b-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="fac4b-116">Installer Visual Studio et .NET</span><span class="sxs-lookup"><span data-stu-id="fac4b-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="fac4b-117">étapes de Hello dans cette section supposent que vous êtes familiarisé avec le développement à l’aide de .NET.</span><span class="sxs-lookup"><span data-stu-id="fac4b-117">hello steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="fac4b-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="fac4b-118">**Windows**</span></span>
1. <span data-ttu-id="fac4b-119">Installez Visual Studio 2017 Community, un environnement de développement intégré (IDE) complet, extensible et gratuit qui permet de créer des applications modernes pour Android, iOS et Windows, ainsi que des applications web et de base de données et des services cloud.</span><span class="sxs-lookup"><span data-stu-id="fac4b-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="fac4b-120">Vous pouvez installer hello .NET Framework complet ou simplement le .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fac4b-120">You can install either hello full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="fac4b-121">extraits de code Hello Bonjour Démarrages rapides fonctionnent avec l’option.</span><span class="sxs-lookup"><span data-stu-id="fac4b-121">hello code snippets in hello Quickstart work with either.</span></span> <span data-ttu-id="fac4b-122">Si vous avez déjà installé sur votre ordinateur Visual Studio, ignorez hello deux étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="fac4b-122">If you already have Visual Studio installed on your machine, skip hello next two steps.</span></span>
   - <span data-ttu-id="fac4b-123">Télécharger hello [programme d’installation de Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="fac4b-123">Download hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="fac4b-124">Exécuter le programme d’installation hello et suivez les invites d’installation hello toocomplete hello installation.</span><span class="sxs-lookup"><span data-stu-id="fac4b-124">Run hello installer and follow hello installation prompts toocomplete hello installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="fac4b-125">**Configurer Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="fac4b-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="fac4b-126">À partir de Visual Studio, la propriété projet > Propriétés de configuration > C/C++ > l’éditeur de liens > Général > répertoires de bibliothèques supplémentaires, ajouter un répertoire de lib\opt hello (par exemple : C:\Program Files (x86) \MySQL\MySQL Connecteur C++ 1.1.9\lib\opt) de hello c ++ connecteur.</span><span class="sxs-lookup"><span data-stu-id="fac4b-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add hello lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of hello c++ connector.</span></span>
2. <span data-ttu-id="fac4b-127">Dans Visual Studio, sélectionnez Propriété du projet > Propriétés de configuration > C/C++ > Général > Autres répertoires Include.</span><span class="sxs-lookup"><span data-stu-id="fac4b-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="fac4b-128">Ajoutez le répertoire include/ du connecteur c++ (c’est-à-dire C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\).</span><span class="sxs-lookup"><span data-stu-id="fac4b-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="fac4b-129">Ajoutez le répertoire racine de la bibliothèque Boost (c’est-à-dire C:\boost_1_64_0\)).</span><span class="sxs-lookup"><span data-stu-id="fac4b-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="fac4b-130">À partir de Visual Studio, la propriété projet > Propriétés de configuration > C/C++ > Éditeur de liens > entrée > mysqlcppconn.lib ajouter des dépendances supplémentaires, dans le champ de texte hello</span><span class="sxs-lookup"><span data-stu-id="fac4b-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into hello text field</span></span>
4. <span data-ttu-id="fac4b-131">Soit mysqlcppconn.dll copie du dossier de bibliothèque connecteur hello c ++ dans l’étape 3 toohello même répertoire que l’exécutable de l’application hello ou ajoutez-la variable d’environnement toohello afin que votre application peut le trouver.</span><span class="sxs-lookup"><span data-stu-id="fac4b-131">Either copy mysqlcppconn.dll from hello c++ connector library folder in step 3 toohello same directory as hello application executable or add it toohello environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="fac4b-132">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="fac4b-132">Get connection information</span></span>
<span data-ttu-id="fac4b-133">Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="fac4b-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="fac4b-134">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="fac4b-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="fac4b-135">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fac4b-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fac4b-136">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez créé, tel que **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="fac4b-136">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="fac4b-137">Cliquez sur le nom du serveur hello.</span><span class="sxs-lookup"><span data-stu-id="fac4b-137">Click hello server name.</span></span>
4. <span data-ttu-id="fac4b-138">Serveur hello sélectionnez **propriétés** page.</span><span class="sxs-lookup"><span data-stu-id="fac4b-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="fac4b-139">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="fac4b-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="fac4b-140">![Nom du serveur de base de données Azure pour MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="fac4b-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="fac4b-141">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="fac4b-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="fac4b-142">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="fac4b-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="fac4b-143">Suivante de hello utilisation tooconnect de code et chargez à l’aide de données hello **CREATE TABLE** et **INSERT INTO** instructions SQL.</span><span class="sxs-lookup"><span data-stu-id="fac4b-143">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="fac4b-144">code de Hello utilise sql::Driver classe avec hello connect() méthode tooestablish un tooMySQL de connexion.</span><span class="sxs-lookup"><span data-stu-id="fac4b-144">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="fac4b-145">Code de hello utilise ensuite la méthode createStatement() et execute() toorun de base de données commandes hello.</span><span class="sxs-lookup"><span data-stu-id="fac4b-145">Then hello code uses method createStatement() and execute() toorun hello database commands.</span></span> 

<span data-ttu-id="fac4b-146">Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="fac4b-146">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a><span data-ttu-id="fac4b-147">Lire les données</span><span class="sxs-lookup"><span data-stu-id="fac4b-147">Read data</span></span>

<span data-ttu-id="fac4b-148">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="fac4b-148">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="fac4b-149">code de Hello utilise sql::Driver classe avec hello connect() méthode tooestablish un tooMySQL de connexion.</span><span class="sxs-lookup"><span data-stu-id="fac4b-149">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="fac4b-150">Ensuite, hello de code utilise la méthode prepareStatement() et executeQuery() toorun hello sélectionner des commandes.</span><span class="sxs-lookup"><span data-stu-id="fac4b-150">Then hello code uses method prepareStatement() and executeQuery() toorun hello select commands.</span></span> <span data-ttu-id="fac4b-151">Enfin, code de hello utilise next() tooadvance toohello enregistrements dans les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="fac4b-151">Finally hello code uses next() tooadvance toohello records in hello results.</span></span> <span data-ttu-id="fac4b-152">Code de hello utilise ensuite les valeurs hello tooparse getInt() et getString() dans l’enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="fac4b-152">Then hello code uses getInt() and getString() tooparse hello values in hello record.</span></span>

<span data-ttu-id="fac4b-153">Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="fac4b-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="fac4b-154">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="fac4b-154">Update data</span></span>
<span data-ttu-id="fac4b-155">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **mise à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="fac4b-155">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="fac4b-156">code de Hello utilise sql::Driver classe avec hello connect() méthode tooestablish un tooMySQL de connexion.</span><span class="sxs-lookup"><span data-stu-id="fac4b-156">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="fac4b-157">Code de hello utilise ensuite la méthode prepareStatement() et executeQuery() toorun hello commandes update.</span><span class="sxs-lookup"><span data-stu-id="fac4b-157">Then hello code uses method prepareStatement() and executeQuery() toorun hello update commands.</span></span> 

<span data-ttu-id="fac4b-158">Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="fac4b-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="fac4b-159">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="fac4b-159">Delete data</span></span>
<span data-ttu-id="fac4b-160">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="fac4b-160">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="fac4b-161">code de Hello utilise sql::Driver classe avec hello connect() méthode tooestablish un tooMySQL de connexion.</span><span class="sxs-lookup"><span data-stu-id="fac4b-161">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="fac4b-162">Code de hello utilise ensuite la méthode prepareStatement() et executeQuery() toorun hello supprimer des commandes.</span><span class="sxs-lookup"><span data-stu-id="fac4b-162">Then hello code uses method prepareStatement() and executeQuery() toorun hello delete commands.</span></span>

<span data-ttu-id="fac4b-163">Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="fac4b-163">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="fac4b-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fac4b-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fac4b-165">Migrer votre tooAzure de base de données de base de données MySQL pour MySQL à l’aide de vidage et restauration</span><span class="sxs-lookup"><span data-stu-id="fac4b-165">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
