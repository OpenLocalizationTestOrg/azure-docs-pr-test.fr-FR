### <a name="install-via-composer"></a>Installation via Composer
1. [Installez Git][install-git]. Notez que sous Windows, vous devez également ajouter variable d’environnement PATH tooyour exécutable hello Git. 
2. Créez un fichier nommé **composer.json** hello racine de votre projet et ajouter hello suivant tooit de code :
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. Téléchargez **[composer.phar][composer-phar]** à la racine du projet.
4. Ouvrez une invite de commandes et exécutez hello suivant de commande dans la racine du projet
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
