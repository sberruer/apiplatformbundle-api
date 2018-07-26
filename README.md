# Projet de test de FOSRestBundle

## Création du projet

    composer create-project symfony/skeleton apiplatformbundle-api
    composer require monolog
    composer require orm
    composer require profiler --dev
    composer require server --dev
    composer require maker --dev
    composer require symfony/var-dumper --dev
    composer require api
    
Vérifier que le bundle est bien déclaré dans le fichier `config/bundles.php`

## Configuration PHP

Vérifier que le module PostgreSQL est présent dans le `php.ini`

    extension=pdo_pgsql

## Développement

### Démarrage de la base

### Configuration de la base de données
    
Modifier le fichier `doctrine.yml`

    doctrine:
        dbal:
            # configure these for your database server
            driver: 'pdo_pgsql'
            server_version: '10'
            charset: utf8
            default_table_options:
                charset: utf8
                collate: utf8_unicode_ci

Modifier le fichier `.env`

    DATABASE_URL=pgsql://postgres:admin@127.0.0.1:5432/fosrestbundle-api
    
Créer le schéma
 
    php bin/console doctrine:database:create

### Ajout des entités
    
Créer les entités

    php bin/console make:entity
    php bin/console make:migration
    php bin/console doctrine:migrations:migrate
        
### Configuration de API Platform

Ajouter l'annotation sur l'entitée

    use ApiPlatform\Core\Annotation\ApiResource;
    
    /**
     * @ORM\Entity(repositoryClass="App\Repository\CommuneRepository")
     *
     * @ApiResource(collectionOperations={"get"})
     */

### Execution

    php bin/console server:run
    

