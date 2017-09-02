En raison des développements en cours, la version du Kit de développement logiciel (SDK) Android installée dans Android Studio peut être différente de celle du code. Le kit de développement logiciel (SDK) Android utilisé dans ce didacticiel correspond à la version 23, dernière version disponible au moment de la rédaction de ce document. Le numéro de version peut augmenter à mesure que de nouvelles versions du Kit de développement logiciel (SDK) apparaissent. Nous vous recommandons d’utiliser la dernière version disponible.

Deux symptômes permettent d'identifier des versions différentes :

- Quand vous générez ou régénérez le projet, vous pouvez obtenir des messages d’erreur Gradle comme « **Impossible de trouver la cible Google Inc.:Google APIs:n** ».
- Les objets Android standard du code dont la résolution doit reposer sur les instructions `import` peuvent générer des messages d'erreur.

Dans ce cas, la version du Kit de développement logiciel (SDK) Android installée dans Android Studio peut différer de celle du Kit de développement logiciel (SDK) cible du projet téléchargé. Pour vérifier la version, apportez les modifications suivantes :

1. Dans Android Studio, cliquez sur **Outils** > **Android** > **Gestionnaire de Kit de développement (SDK)**. Si vous n'avez pas installé la dernière version de la plateforme de Kit de développement logiciel (SDK), cliquez pour l'installer. Prenez note du numéro de la version.
2. Dans l’onglet **Explorateur de projets**, sous **Scripts Gradle**, ouvrez le fichier **build.gradle (module : app)**. Vérifiez que les versions **compileSdkVersion** et **buildToolsVersion** sont définies sur la dernière version installée du Kit de développement logiciel (SDK). Les balises peuvent se présenter comme suit :

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. Dans l’Explorateur de projets d’Android Studio, cliquez avec le bouton droit sur le nœud de projet, choisissez **Propriétés**, puis, dans la colonne de gauche, choisissez **Android**. Vérifiez que la version du Kit de développement logiciel (SDK) définie pour **Project Build Target** est identique à celle de **targetSdkVersion**.

Dans Android Studio, le fichier manifeste ne permet plus de spécifier le Kit de développement (SDK) cible et la version minimale du Kit de développement logiciel (SDK), contrairement à Eclipse.
