Brings Symfony 1.4 project:deploy command to Symfony2.

## Installation 2.0.X

###  Add DeployBundle to your deps

    [HpatoioDeployBundle]
      git=git://github.com/hpatoio/DeployBundle.git
      target=/bundles/Hpatoio/DeployBundle
      
### Add DeployBundle to your application kernel

    // app/AppKernel.php
    public function registerBundles()
    {
        return array(
            // ...
            new Hpatoio\DeployBundle\DeployBundle(),
            // ...
        );
    }
    
### Register the namespace in autoload.php

    'Hpatoio'     => __DIR__.'/../vendor/bundles',
    
run 

    bin/vendors install
    
## Installation 2.1

###  Add DeployBundle to your composer.json

     "hpatoio/deploy-bundle": "dev-master"
      
### Add DeployBundle to your application kernel

    // app/AppKernel.php
    public function registerBundles()
    {
        $bundles = array(
            // ...
            new Hpatoio\DeployBundle\DeployBundle(),
            // ...
        );
    }
    
run 

    composer update

### Configure

    # app/config/config.yml
    deploy:
      prod:
        host: 127.0.0.1 // or the hostname
        user: root
        dir: /path/to/dir
        port: 22
      stage:
        host: 127.0.0.1 // or the hostname
        user: root2
        dir: /path/to/dir
        port: 22
    
### Rsync Exclude

Create a rsync_exclude.txt file under app/config to exclude files in your deployments.

### Use

Deployment is easy: 

    php app/console project:deploy --go prod

Simulate deployment

    php app/console project:deploy prod
    
Cache warmup with --cache-warmup option. With this option once the deploy has finished cache:warmup command is run on the destination server.   

    php app/console project:deploy --go --cache-warmup prod
    
Custom parameters for rsync (default -azC --force --delete --progress -h) 

    php app/console project:deploy --rsync-options="-azChdl" prod

## Feedbacks

For any feedback open an issue here on Github or comment here http://www.iliveinperego.com/2012/03/symfony2-deploy-like-symfony-1-4/    