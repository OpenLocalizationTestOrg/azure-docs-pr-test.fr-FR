## <a name="install-wordpress"></a><span data-ttu-id="a1b14-101">Installer WordPress</span><span class="sxs-lookup"><span data-stu-id="a1b14-101">Install WordPress</span></span>

<span data-ttu-id="a1b14-102">Si vous souhaitez tootry votre pile, installez un exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="a1b14-102">If you want tootry your stack, install a sample app.</span></span> <span data-ttu-id="a1b14-103">Par exemple, hello suit installer ouvrir la source de hello [WordPress](https://wordpress.org/) plateforme toocreate des sites Web et des blogs.</span><span class="sxs-lookup"><span data-stu-id="a1b14-103">As an example, hello following steps install hello open source [WordPress](https://wordpress.org/) platform toocreate websites and blogs.</span></span> <span data-ttu-id="a1b14-104">Inclure d’autres charges de travail de tootry [Drupal](http://www.drupal.org) et [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="a1b14-104">Other workloads tootry include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="a1b14-105">Ce programme d’installation de WordPress est pour la preuve de concept.</span><span class="sxs-lookup"><span data-stu-id="a1b14-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="a1b14-106">Pour plus d’informations et des paramètres pour l’installation de production, consultez hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="a1b14-106">For more information and settings for production installation, see hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-hello-wordpress-package"></a><span data-ttu-id="a1b14-107">Installer le package de WordPress hello</span><span class="sxs-lookup"><span data-stu-id="a1b14-107">Install hello WordPress package</span></span>

<span data-ttu-id="a1b14-108">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a1b14-108">Run hello following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="a1b14-109">Configurer WordPress</span><span class="sxs-lookup"><span data-stu-id="a1b14-109">Configure WordPress</span></span>

<span data-ttu-id="a1b14-110">Configurer WordPress toouse MySQL et PHP.</span><span class="sxs-lookup"><span data-stu-id="a1b14-110">Configure WordPress toouse MySQL and PHP.</span></span> <span data-ttu-id="a1b14-111">Exécutez hello suivant commande tooopen un éditeur de texte de votre choix et créer le fichier de hello `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="a1b14-111">Run hello following command tooopen a text editor of your choice and create hello file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="a1b14-112">Hello copie le fichier toohello lignes suivant, en remplaçant votre mot de passe de base de données *votreMotdePasse* (laissez les autres valeurs inchangées).</span><span class="sxs-lookup"><span data-stu-id="a1b14-112">Copy hello following lines toohello file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="a1b14-113">Puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="a1b14-113">Then save hello file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="a1b14-114">Dans un répertoire de travail, créez un fichier texte `wordpress.sql` base de données tooconfigure hello WordPress :</span><span class="sxs-lookup"><span data-stu-id="a1b14-114">In a working directory, create a text file `wordpress.sql` tooconfigure hello WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="a1b14-115">Ajouter hello suivant de commandes, en remplaçant votre mot de passe de base de données *votreMotdePasse* (laissez les autres valeurs inchangées).</span><span class="sxs-lookup"><span data-stu-id="a1b14-115">Add hello following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="a1b14-116">Puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="a1b14-116">Then save hello file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="a1b14-117">Exécutez hello suivant de base de données de commande toocreate hello :</span><span class="sxs-lookup"><span data-stu-id="a1b14-117">Run hello following command toocreate hello database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="a1b14-118">Après la commande hello, supprimez-le hello `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="a1b14-118">After hello command completes, delete hello file `wordpress.sql`.</span></span>

<span data-ttu-id="a1b14-119">Déplacer la racine du document hello WordPress installation toohello web server :</span><span class="sxs-lookup"><span data-stu-id="a1b14-119">Move hello WordPress installation toohello web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="a1b14-120">Maintenant, vous pouvez terminer l’installation de WordPress hello et publier sur la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="a1b14-120">Now you can complete hello WordPress setup and publish on hello platform.</span></span> <span data-ttu-id="a1b14-121">Ouvrez un navigateur et allez trop`http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="a1b14-121">Open a browser and go too`http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="a1b14-122">Remplacez hello adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a1b14-122">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="a1b14-123">Il doit se présenter une image toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="a1b14-123">It should look similar toothis image.</span></span>

![Page d’installation de WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)