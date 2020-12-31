# Formation Symfony
## On Commence
1. Préparation de l’environnement

  - Installer [Visual C++ Redistribuable Packages](https://wampserver.aviatechno.net) (Requirement)
    - Si votre système est 32bits installer tous les packages x86 seulement
    - Si votre système est 64bits installer tous les packages x86 et x64
  - Installer [WampServer 3.2](https://wampserver.aviatechno.net) selon votre système 32bit ou 64bit et configurer le version **PHP 7.4.*** dans le path de variable d’enivrement de système . Lancez une recherche et sélectionnez : Système (Panneau de configuration). Cliquez sur le lien Paramètres système avancés. Cliquez sur Variables d'environnement. Dans la section Variables système, recherchez la variable d'environnement **PATH** et sélectionnez-la. Cliquez sur Modifier. Ajouter le chemin de votre version PHP et cliquer sur OK, Lancer la commande `php -v` pour vérifier
  - Installer [Composer](https://getcomposer.org/download/) et ou cours de l’installation choisir votre version PHP7.4.* , Lancer la commande `composer --version`
  - Installer [Git](https://git-scm.com/), Lancer la commande `git --version` pour vérifier
  - Installer [Symfony CLI](https://symfony.com/download), Lancer la commande `symfony` pour vérifier
  - Installer l’éditeur [VSCode](https://code.visualstudio.com/) ou [PHPStorm](https://www.jetbrains.com/fr-fr/phpstorm/download/#section=windows)
  
2. Création d'un nouveau projet Symfony

  - Lancer la commande : `composer create-project symfony/website-skeleton my_project_name`
  - Exécuter l'application avec la commande : `symfony serve`
  
##  Découverte de l'application Symfony

1. Structure de symfony
```
your-project/
├─ assets/
├─ bin/
│  └─ console
├─ config/
├─ public/
│  └─ index.php
├─ src/
│  └─ ...
├─ templates/
├─ tests/
├─ translations/
├─ var/
│  ├─ cache/
│  ├─ log/
│  └─ ...
└─ vendor/

```
2. Controller

On peut crée un controller avec la commande `php bin/console make:controller HomeController`

Dans le Controller on a les importations, les routes, les fonctions et les variables

```php
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;

class HomeController extends AbstractController
{
    /**
     * @Route("/home", name="home")
     */
    public function index()
    {
        return new Response('Bonjour tous le monde');
        //return new Response('<h1>Bonjour tous le monde</h1>');
        /* return new Response("<html>
        <head>
        <title>Mon Application</title>
        </head>
        <body>
        <h1>Bonjour tous le monde </h1>
        <p>c'est ma première page Symfony</p>
        </body>
        </html>
        ");*/
        //return $this->render('home/index.html.twig');
        /*return $this->render('home/index.html.twig',[
            'title' => 'Bonjour à tous!'
        ]);*/
    }
}
```
3. Twig
  - Le variable `{{ title }}`
  - Le condition [if](https://twig.symfony.com/doc/3.x/tags/if.html) 
  ```twig
{% set age = 10 %}
{% if age >= 18 %}
  <p>vous êtes un adulte</p>
{% elseif age >= 12  %}
  <p> vous êtes un adolescent<p>
{% else %}
  <p>vous êtes un enfant</p>
{% endif %}
  ```
  - Le boucle [for](https://twig.symfony.com/doc/3.x/tags/for.html)
  ```php
$joueurs=["Ali" => 31,"Salem"=>12,"Youssef"=>40,"Karim"=>9];
return $this->render('home/index.html.twig',['joueurs' => $joueurs]);
  ```
  ```twig
    {% for prenom, age in joueurs %}
       <p>(Joueur numéro {{loop.index}} ): {{prenom}} a {{age}} ans</p>  {# {{loop.first}}  {{loop.last}}#}
    {% endfor %}
  ```
  - Les commentaires   `{# Voici c’est un commentaire twig  #}`
  - Les [filtres](https://twig.symfony.com/doc/3.x/filters/index.html) `{{ nom|upper }} {{ minitext|title }} {{ paragraphe|capitalize }}`
  - Le URL  `<a href="{{ path('url_name') }}">ce moi</a>`
  - L’héritage Twig extends
4. Entity
  - Configuration de base de données depuis le fichier **.env** 
  - Création de la base de données `php bin/console doctrine:database:create`
  - Création d'une entité `php bin/console make:entity Post` 
  - Migrer l'entité créé  `php bin/console make:migration` et exécuter `php bin/console doctrine:migrations:migrate` 
  - Générer crud (create, read, update, delete) `php bin/console make:crud Post`
5. Template
  - Integration de [Bootstrap](https://getbootstrap.com/docs/4.5/getting-started/introduction/)
