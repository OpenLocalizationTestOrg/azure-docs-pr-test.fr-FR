## <a name="install-wordpress"></a><span data-ttu-id="0b0c7-101">Installer WordPress</span><span class="sxs-lookup"><span data-stu-id="0b0c7-101">Install WordPress</span></span>

<span data-ttu-id="0b0c7-102">Si vous souhaitez essayer votre pile, installez un exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-102">If you want to try your stack, install a sample app.</span></span> <span data-ttu-id="0b0c7-103">Ainsi, les étapes suivantes installent la plateforme open source [WordPress](https://wordpress.org/) pour créer des sites web et des blogs.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-103">As an example, the following steps install the open source [WordPress](https://wordpress.org/) platform to create websites and blogs.</span></span> <span data-ttu-id="0b0c7-104">Les autres charges de travail à essayer incluent [Drupal](http://www.drupal.org) et [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="0b0c7-104">Other workloads to try include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="0b0c7-105">Ce programme d’installation de WordPress est pour la preuve de concept.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="0b0c7-106">Consultez la [documentation WordPress](https://codex.wordpress.org/Main_Page)pour obtenir plus d’informations et de paramètres sur l’installation de production.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-106">For more information and settings for production installation, see the [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-the-wordpress-package"></a><span data-ttu-id="0b0c7-107">Installez le package WordPress</span><span class="sxs-lookup"><span data-stu-id="0b0c7-107">Install the WordPress package</span></span>

<span data-ttu-id="0b0c7-108">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0b0c7-108">Run the following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="0b0c7-109">Configurer WordPress</span><span class="sxs-lookup"><span data-stu-id="0b0c7-109">Configure WordPress</span></span>

<span data-ttu-id="0b0c7-110">Configurer WordPress pour utiliser PHP et MySQL.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-110">Configure WordPress to use MySQL and PHP.</span></span> <span data-ttu-id="0b0c7-111">Exécutez la commande suivante pour ouvrir un éditeur de texte de votre choix et créer le fichier `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="0b0c7-111">Run the following command to open a text editor of your choice and create the file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="0b0c7-112">Copiez les lignes suivantes dans le fichier, en remplaçant votre mot de passe de base de données par *votreMotdePasse* (laissez les autres valeurs inchangées).</span><span class="sxs-lookup"><span data-stu-id="0b0c7-112">Copy the following lines to the file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="0b0c7-113">Puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-113">Then save the file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="0b0c7-114">Dans un répertoire de travail, créez un fichier texte `wordpress.sql` pour configurer la base de données WordPress :</span><span class="sxs-lookup"><span data-stu-id="0b0c7-114">In a working directory, create a text file `wordpress.sql` to configure the WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="0b0c7-115">Ajoutez les commandes suivantes, en remplaçant votre mot de passe de base de données par *votreMotdePasse* (laissez les autres valeurs inchangées).</span><span class="sxs-lookup"><span data-stu-id="0b0c7-115">Add the following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="0b0c7-116">Puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-116">Then save the file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
TO wordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="0b0c7-117">Exécutez la commande suivante pour créer la base de données :</span><span class="sxs-lookup"><span data-stu-id="0b0c7-117">Run the following command to create the database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="0b0c7-118">Une fois la commande terminée, supprimez le fichier `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-118">After the command completes, delete the file `wordpress.sql`.</span></span>

<span data-ttu-id="0b0c7-119">Déplacez l’installation de WordPress à la racine du document du serveur web :</span><span class="sxs-lookup"><span data-stu-id="0b0c7-119">Move the WordPress installation to the web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="0b0c7-120">Vous pouvez désormais terminer l’installation de WordPress et publier sur la plateforme.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-120">Now you can complete the WordPress setup and publish on the platform.</span></span> <span data-ttu-id="0b0c7-121">Ouvrez un navigateur web et accédez à `http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-121">Open a browser and go to `http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="0b0c7-122">Remplacez l’adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-122">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="0b0c7-123">Elle doit ressembler à cette image.</span><span class="sxs-lookup"><span data-stu-id="0b0c7-123">It should look similar to this image.</span></span>

![Page d’installation de WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)