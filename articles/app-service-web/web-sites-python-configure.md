---
title: aaaConfiguring de Python avec Azure App Service Web Apps
description: "Ce didacticiel décrit les options relatives à la création et à la configuration d’une application Python compatible WSGI (Web Server Gateway Interface) de base dans Azure App Service Web Apps."
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a>Configuration de Python dans Azure App Service Web Apps
Ce didacticiel décrit les options relatives à la création et à la configuration d’une application Python compatible WSGI (Web Server Gateway Interface) de base dans [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Il décrit les fonctions supplémentaires associées au déploiement Git, telles que l’environnement virtuel et l’installation de packages à l’aide de fichier requirements.txt.

## <a name="bottle-django-or-flask"></a>Bottle, Django ou Flask ?
Bonjour Azure Marketplace contient des modèles pour les infrastructures d’eau, Django et ballon hello. Si vous développez votre première application web dans Azure App Service, ou vous n’êtes pas familiarisé avec Git, nous vous recommandons de suivre une de ces didacticiels, qui incluent des instructions pas à pas pour la création d’une application à partir de la galerie hello à l’aide du déploiement Git à partir de Windows ou Mac :

* [Création d’applications web avec Bottle](web-sites-python-create-deploy-bottle-app.md)
* [Création d’applications web avec Django](web-sites-python-create-deploy-django-app.md)
* [Création d’applications web avec Flask](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a>Création d’applications web sur le portail Azure
Ce didacticiel suppose un existant Azure abonnement et accès toohello portail Azure.

Si vous ne disposez pas d’une application web existante, vous pouvez en créer un à partir de hello [Azure Portal](https://portal.azure.com).  Cliquez sur bouton Nouveau hello hello en haut à gauche, puis cliquez sur **Web + Mobile** > **application Web**.

## <a name="git-publishing"></a>Publication Git
Configurer la publication Git de votre application web qui vient d’être créé en suivant les instructions de hello sur [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md). Ce didacticiel utilise Git toocreate, gérer et publier notre tooAzure d’application Python web du Service d’applications.

Une fois la publication Git configurée, un référentiel Git est créé et associé à votre application web. les URL du référentiel Hello s’affiche et peut être dorénavant utilisés toopush des données du cloud de toohello environnement hello développement local. applications toopublish via Git, assurez-vous qu’un client Git est également installé et suivez les instructions hello fourni toopush votre tooAzure de contenu d’application du Service d’applications web.

## <a name="application-overview"></a>Vue d’ensemble de l’application
Dans les sections suivantes hello, hello fichiers suivants est créé. Ils doivent être placés dans la racine de hello du référentiel Git de hello.

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a>Gestionnaire WSGI
Wsgi sous est une norme de Python décrite par [PEP 3333](http://www.python.org/dev/peps/pep-3333/) définissant une interface entre le serveur web de hello et Python. Elle fournit une interface normalisée pour la rédaction de diverses applications et infrastructures Web à l'aide de Python. Des infrastructures Web Python connues utilisent aujourd’hui WSGI. Azure permet d’application de Service Web Apps que vous prenez en charge pour les versions de .NET Framework ; en outre, les utilisateurs expérimentés peuvent même créer leurs propres tant que gestionnaire personnalisé de hello suit les directives de spécification de wsgi sous hello.

Voici un exemple de `app.py` définissant un gestionnaire personnalisé :

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

Vous pouvez exécuter l’application localement avec `python app.py`, puis recherchez trop`http://localhost:5555` dans votre navigateur web.

## <a name="virtual-environment"></a>Environnement virtuel
Bien que l’application d’exemple hello ci-dessus ne nécessite pas les packages externes, il est probable que votre application nécessite certaines.

toohelp gérer les dépendances du package externe, Azure Git déploiement prend en charge la création d’environnements virtuels hello.

Quand Azure détecte un requirements.txt racine hello du référentiel de hello, il crée automatiquement un environnement virtuel nommé `env`. Cela se produit uniquement sur le premier déploiement de hello, ou pendant un déploiement après hello sélectionné runtime Python a changé.

Vous aurez probablement besoin de toocreate un environnement virtuel localement pour le développement, mais ne pas inclure dans votre référentiel Git.

## <a name="package-management"></a>Gestion des packages
Packages répertoriés dans requirements.txt seront automatiquement installés dans un environnement virtuel de hello l’utilisation de pip. Cette opération intervient à chaque déploiement, mais pip ignorera l’installation si un package est déjà installé.

Exemple `requirements.txt`:

    azure==0.8.4


## <a name="python-version"></a>Version de Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

Exemple `runtime.txt`:

    python-2.7


## <a name="webconfig"></a>Web.config
Vous devez toocreate un toospecify du fichier web.config comment les serveur hello doivent gérer les requêtes.

Notez que si vous disposez d’un fichier web.x.y.config dans votre référentiel où x.y correspond à hello sélectionné runtime Python, puis Azure copie automatiquement le fichier approprié de hello en tant que fichier web.config.

Hello exemples web.config suivants s’appuient sur un script de proxy environnement virtuel qui est décrit dans la section suivante de hello.  Elles fonctionnent avec le gestionnaire wsgi sous hello utilisé dans l’exemple de hello `app.py` ci-dessus.

Exemple `web.config` pour Python 2.7 :

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


Exemple `web.config` pour Python 3.4 :

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


Fichiers statiques doivent être gérés par le serveur web de hello directement, sans passer par le code Python, pour améliorer les performances.

Bonjour exemples ci-dessus, emplacement hello des fichiers statiques de hello sur le disque doit correspondre à emplacement hello dans les URL hello. Cela signifie qu’une demande de `http://pythonapp.azurewebsites.net/static/site.css` servira fichier hello sur le disque à `\static\site.css`.

`WSGI_ALT_VIRTUALENV_HANDLER`est où vous spécifiez le Gestionnaire de wsgi sous hello. Bonjour au-dessus des exemples, il a `app.wsgi_app` , car le Gestionnaire de hello est une fonction nommée `wsgi_app` dans `app.py` dans le dossier racine de hello.

`PYTHONPATH`peut être personnalisé, mais si vous installez toutes les dépendances dans un environnement virtuel de hello en les spécifiant dans requirements.txt, vous ne devez toochange il.

## <a name="virtual-environment-proxy"></a>Proxy d’environnement virtuel
Hello script suivant est associé au gestionnaire utilisé tooretrieve hello wsgi sous, activer les erreurs de journaux et d’environnement virtuels hello. Il est conçu toobe générique et utilisé sans modification.

Contenu de `ptvs_virtualenv_proxy.py`:

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a>Personnalisation du déploiement Git
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a>Résolution des problèmes - Installation des packages
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Résolution des problèmes - Environnement virtuel
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement Python](/develop/python/).

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

