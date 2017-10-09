Azure déterminera la version hello de toouse Python pour son environnement virtuel avec hello suivant de priorité :

1. version spécifiée dans runtime.txt dans le dossier racine de hello
2. version spécifiée par le paramètre de Python dans la configuration de l’application web hello (hello **paramètres** > **paramètres de l’Application** panneau pour votre application web hello portail Azure)
3. Python 2.7 est par défaut de hello si hello ci-dessus sont spécifiés

Valeurs valides pour le contenu de hello de 

    \runtime.txt

sont :

* python-2.7
* python-3.4

Si les version micro hello (le troisième chiffre) est spécifié, il est ignoré.

