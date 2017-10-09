## <a name="install-wordpress"></a>Installer WordPress

Si vous souhaitez tootry votre pile, installez un exemple d’application. Par exemple, hello suit installer ouvrir la source de hello [WordPress](https://wordpress.org/) plateforme toocreate des sites Web et des blogs. Inclure d’autres charges de travail de tootry [Drupal](http://www.drupal.org) et [Moodle](https://moodle.org/). 

Ce programme d’installation de WordPress est pour la preuve de concept. Pour plus d’informations et des paramètres pour l’installation de production, consultez hello [WordPress documentation](https://codex.wordpress.org/Main_Page). 



### <a name="install-hello-wordpress-package"></a>Installer le package de WordPress hello

Exécutez hello de commande suivante :

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>Configurer WordPress

Configurer WordPress toouse MySQL et PHP. Exécutez hello suivant commande tooopen un éditeur de texte de votre choix et créer le fichier de hello `/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
Hello copie le fichier toohello lignes suivant, en remplaçant votre mot de passe de base de données *votreMotdePasse* (laissez les autres valeurs inchangées). Puis enregistrez le fichier de hello.

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

Dans un répertoire de travail, créez un fichier texte `wordpress.sql` base de données tooconfigure hello WordPress : 

```bash
sudo sensible-editor wordpress.sql
```

Ajouter hello suivant de commandes, en remplaçant votre mot de passe de base de données *votreMotdePasse* (laissez les autres valeurs inchangées). Puis enregistrez le fichier de hello.

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


Exécutez hello suivant de base de données de commande toocreate hello :

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

Après la commande hello, supprimez-le hello `wordpress.sql`.

Déplacer la racine du document hello WordPress installation toohello web server :

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

Maintenant, vous pouvez terminer l’installation de WordPress hello et publier sur la plateforme de hello. Ouvrez un navigateur et allez trop`http://yourPublicIPAddress/wordpress`. Remplacez hello adresse IP publique de votre machine virtuelle. Il doit se présenter une image toothis similaire.

![Page d’installation de WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)