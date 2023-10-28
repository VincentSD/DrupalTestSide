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

4. Change directory into the project and install database.
    `lando db-import drupal10.2023-10-28-1698490302.sql.gz`
    Replace the db dump with the one you with to import.

5. Start the project.
    `lando start`

6. Visit the local dev site and login.
    - Use any of the urls provided after lando start
    - Use username = `admin` and password = `password`

7. Get in touch for next steps and lets party!!!
