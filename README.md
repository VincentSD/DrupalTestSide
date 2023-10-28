# vfi
Versified Fix It - household service provider

1. Prerequisites:
    - Ensure that Git is installed on the local machine.
    - Make sure you have Docker and Lando installed and set up correctly.

    `https://github.com/lando/lando/releases ` 

    `https://docs.docker.com/desktop/install/windows-install/`

2. Create local directory:
    - Create a folder in your working directory for this project and navigate to that folder. Example;

    `mkdir -p ~/Sites/Drupal/vfi && cd ~/Sites/Drupal/vfi/`

3. Clone repository into directory
    `git clone https://github.com/versitechgh/vfi.git .`

4. Start the project.
    `lando start`

5. Change directory into the project and install database.
    `lando db-import db-vfi.gz`
    Replace the db dump with the one you with to import. We have a sample db in this repo as an example [`db-vfi.gz`]

6. Visit the local dev site and login.
    - Use any of the urls provided after lando start
    - Use username = `admin` and password = `password`

7. Get in touch for next steps and lets party!!!





The next few steps are for disabling Drupal's aggressive caching during development
1.  Navigate to the sub-folder “web”. 
    - Inside this folder you should see “core”, “modules”, and “sites” amongst other folders and files. 
    - Go into the “sites” folder
    - Then (if it doesn’t already exist) create a new file called development.services.yml. This file should be located at the same level as the folder “default”

    - Once created, open the file and add the following settings.
    ```
    # Local development services.
    parameters:
    http.response.debug_cacheability_headers: true
    twig.config:
        debug: true
        auto_reload: true
        cache: false
    services:
    cache.backend.null:
        class: Drupal\Core\Cache\NullBackendFactory
    ```

    - This will disable a number of settings preventing Drupal’s caching mechanism from being overly aggressive during development.

2. Duplicate the file “example.settings.local.php” and rename the duplicated file to “settings.local.php” and drag it into the default folder (Tip: if it's not in the default folder, it will not be gitignored)
    - Open the file in your text editor of choice. Inside the file, uncomment these 3 lines.
        - $settings['cache']['bins']['render'] = 'cache.backend.null';
        - $settings['cache']['bins']['page'] = 'cache.backend.null';
        - $settings['cache']['bins']['dynamic_page_cache'] = 'cache.backend.null';

    - This is the second half of disabling the various caches that Drupal utilizes.

3. Next uncomment these lines at the end of the default.settings.php file
    ```
    if (file_exists($app_root . '/' . $site_path . '/settings.local.php')) {
    include $app_root . '/' . $site_path . '/settings.local.php';
    }
    ```

4. Using Drupal’s CLI tool, Drush, we now need to flush / rebuild the cache stores. This can be done by using the Lando alias. 
Run command `lando drush cache:rebuild` or for short `lando drush cr`


That then sets you up for theming too. Now when you inspect any page at the front end, you would see the directory for the page and the suggested Drupal naming patterns to be used for theme overrides.



