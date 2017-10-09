En raison d’un développement continu, version du Kit de développement logiciel Android hello installée dans Android Studio ne peut pas correspondre version hello dans le code hello. Hello du SDK Android référencés dans ce didacticiel est hello 23, de version plus récente au moment de hello de l’écriture. numéro de version Hello peut augmenter en tant que de nouvelles versions de hello SDK s’affichent, et nous recommandons à l’aide de la version la plus récente hello disponible.

Deux symptômes permettent d'identifier des versions différentes :

- Lorsque vous générez ou régénérez le projet de hello, vous risquez d’obtenir des messages d’erreur Gradle comme «**Échec de la cible de toofind Google Inc.:Google APIs:n**».
- Les objets Android standard du code dont la résolution doit reposer sur les instructions `import` peuvent générer des messages d'erreur.

Si une de ces s’affiche, version hello Hello Android SDK installés dans Android Studio ne peut pas correspondre cible du Kit de développement logiciel hello du projet de hello téléchargé. version de hello tooverify, rendre hello modifications suivantes :

1. Dans Android Studio, cliquez sur **Outils** > **Android** > **Gestionnaire de Kit de développement (SDK)**. Si vous n’avez pas installé hello dernière version de hello plateforme du Kit de développement logiciel, puis cliquez sur tooinstall il. Prenez note du numéro de version hello.
2. Sur hello **Explorateur de projets** sous l’onglet sous **Gradle Scripts**, ouvrez le fichier de hello **build.gradle (modeule : application)**. Vérifiez que hello **compileSdkVersion** et **buildToolsVersion** sont définies toohello dernière version SDK installée. les balises Hello peuvent ressembler à ceci :

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. Bonjour Explorateur de projets Android Studio, nœud de projet hello avec le bouton droit, choisissez **propriétés**, puis dans la colonne de gauche hello **Android**. Vérifiez que hello **cible de Build de projet** a la valeur toohello même version du Kit de développement logiciel en tant que hello **targetSdkVersion**.

Dans Android Studio, les fichiers manifeste hello ne sont plus utilisé toospecify hello cible SDK et les version minimale de kit de développement logiciel, contrairement aux cas de hello avec Eclipse.
