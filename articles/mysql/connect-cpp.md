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
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a>Base de données Azure pour MySQL : utiliser Connecteur/C++ tooconnect et interroger des données
Ce démarrage rapide montre comment tooconnect tooan Azure de base de données MySQL à l’aide d’une application C++. Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello. Hello étapes décrites dans cet article supposent que vous êtes familiarisé avec le développement à l’aide de C++, et que vous êtes tooworking nouvelle base de données Azure pour MySQL.

## <a name="prerequisites"></a>Composants requis
Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :
- [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

Il vous faudra également :
- Installer [.NET Framework](https://www.microsoft.com/net/download)
- Installez [Visual Studio](https://www.visualstudio.com/downloads/)
- Installer [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/) 
- Installer [Boost](http://www.boost.org/)

## <a name="install-visual-studio-and-net"></a>Installer Visual Studio et .NET
étapes de Hello dans cette section supposent que vous êtes familiarisé avec le développement à l’aide de .NET.

### <a name="windows"></a>**Windows**
1. Installez Visual Studio 2017 Community, un environnement de développement intégré (IDE) complet, extensible et gratuit qui permet de créer des applications modernes pour Android, iOS et Windows, ainsi que des applications web et de base de données et des services cloud. Vous pouvez installer hello .NET Framework complet ou simplement le .NET Core. extraits de code Hello Bonjour Démarrages rapides fonctionnent avec l’option. Si vous avez déjà installé sur votre ordinateur Visual Studio, ignorez hello deux étapes suivantes.
   - Télécharger hello [programme d’installation de Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15). 
   - Exécuter le programme d’installation hello et suivez les invites d’installation hello toocomplete hello installation.

### <a name="configure-visual-studio"></a>**Configurer Visual Studio**
1. À partir de Visual Studio, la propriété projet > Propriétés de configuration > C/C++ > l’éditeur de liens > Général > répertoires de bibliothèques supplémentaires, ajouter un répertoire de lib\opt hello (par exemple : C:\Program Files (x86) \MySQL\MySQL Connecteur C++ 1.1.9\lib\opt) de hello c ++ connecteur.
2. Dans Visual Studio, sélectionnez Propriété du projet > Propriétés de configuration > C/C++ > Général > Autres répertoires Include.
   - Ajoutez le répertoire include/ du connecteur c++ (c’est-à-dire C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\).
   - Ajoutez le répertoire racine de la bibliothèque Boost (c’est-à-dire C:\boost_1_64_0\)).
3. À partir de Visual Studio, la propriété projet > Propriétés de configuration > C/C++ > Éditeur de liens > entrée > mysqlcppconn.lib ajouter des dépendances supplémentaires, dans le champ de texte hello
4. Soit mysqlcppconn.dll copie du dossier de bibliothèque connecteur hello c ++ dans l’étape 3 toohello même répertoire que l’exécutable de l’application hello ou ajoutez-la variable d’environnement toohello afin que votre application peut le trouver.

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL. Vous devez hello des informations d’identification de nom et la connexion serveur complet.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez créé, tel que **myserver4demo**.
3. Cliquez sur le nom du serveur hello.
4. Serveur hello sélectionnez **propriétés** page. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.
 ![Nom du serveur de base de données Azure pour MySQL](./media/connect-cpp/1_server-properties-name-login.png)
5. Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.

## <a name="connect-create-table-and-insert-data"></a>Se connecter, créer des tables et insérer des données
Suivante de hello utilisation tooconnect de code et chargez à l’aide de données hello **CREATE TABLE** et **INSERT INTO** instructions SQL. code de Hello utilise sql::Driver classe avec hello connect() méthode tooestablish un tooMySQL de connexion. Code de hello utilise ensuite la méthode createStatement() et execute() toorun de base de données commandes hello. 

Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello. 

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

## <a name="read-data"></a>Lire les données

Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL. code de Hello utilise sql::Driver classe avec hello connect() méthode tooestablish un tooMySQL de connexion. Ensuite, hello de code utilise la méthode prepareStatement() et executeQuery() toorun hello sélectionner des commandes. Enfin, code de hello utilise next() tooadvance toohello enregistrements dans les résultats de hello. Code de hello utilise ensuite les valeurs hello tooparse getInt() et getString() dans l’enregistrement de hello.

Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello. 

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

## <a name="update-data"></a>Mettre à jour des données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **mise à jour** instruction SQL. code de Hello utilise sql::Driver classe avec hello connect() méthode tooestablish un tooMySQL de connexion. Code de hello utilise ensuite la méthode prepareStatement() et executeQuery() toorun hello commandes update. 

Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello. 

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


## <a name="delete-data"></a>Suppression de données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL. code de Hello utilise sql::Driver classe avec hello connect() méthode tooestablish un tooMySQL de connexion. Code de hello utilise ensuite la méthode prepareStatement() et executeQuery() toorun hello supprimer des commandes.

Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello. 

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

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migrer votre tooAzure de base de données de base de données MySQL pour MySQL à l’aide de vidage et restauration](concepts-migrate-dump-restore.md)
