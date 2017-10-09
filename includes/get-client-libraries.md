### <a name="install-via-composer"></a><span data-ttu-id="97182-101">Installation via Composer</span><span class="sxs-lookup"><span data-stu-id="97182-101">Install via Composer</span></span>
1. <span data-ttu-id="97182-102">[Installez Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="97182-102">[Install Git][install-git].</span></span> <span data-ttu-id="97182-103">Notez que sous Windows, vous devez également ajouter variable d’environnement PATH tooyour exécutable hello Git.</span><span class="sxs-lookup"><span data-stu-id="97182-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="97182-104">Créez un fichier nommé **composer.json** hello racine de votre projet et ajouter hello suivant tooit de code :</span><span class="sxs-lookup"><span data-stu-id="97182-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="97182-105">Téléchargez **[composer.phar][composer-phar]** à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="97182-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="97182-106">Ouvrez une invite de commandes et exécutez hello suivant de commande dans la racine du projet</span><span class="sxs-lookup"><span data-stu-id="97182-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
