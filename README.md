# How to install Laravel10 on Linux distros such as Debian, Kali Linux and Ubuntu ?

To install Laravel on Kali Linux, you'll need to follow these general steps. Please note that software and package versions may have changed since my last knowledge update in September 2021, so make sure to adapt these steps to the latest versions and recommendations.

1. **Install Required Software**:
   Before installing Laravel, you need to have a web server, PHP, Composer (a PHP dependency manager), and other necessary components installed.

   ```bash
   sudo apt update
   sudo apt install apache2 php php-cli php-mbstring php-xml composer
   ```

2. **Install MySQL or MariaDB** (Optional):
   Laravel typically uses a database to store data. You can choose between MySQL or MariaDB. Install one of them based on your preference.

   ```bash
   sudo apt install mysql-server
   # OR
   sudo apt install mariadb-server
   ```

3. **Configure Database**:
   If you installed a database, you need to set it up. This includes setting the root password and creating a database for your Laravel project.

   ```bash
   sudo mysql_secure_installation
   mysql -u root -p

   # Inside MySQL/MariaDB shell
   CREATE DATABASE laravel_db;
   CREATE USER 'laravel_user'@'localhost' IDENTIFIED BY 'your_password';
   GRANT ALL ON laravel_db.* TO 'laravel_user'@'localhost';
   FLUSH PRIVILEGES;
   EXIT;
   ```

4. **Install Laravel**:
   Navigate to the directory where you want to install your Laravel project and run the following commands:

   ```bash
   composer global require laravel/installer
   laravel new your-project-name
   cd your-project-name
   ```
When executing `laravel new projectName` command, this will appear:

```
Would you like to install a starter kit? ────────────────────┐
 │ › ● No starter kit                                           │
 │   ○ Laravel Breeze                                           │
 │   ○ Laravel Jetstream  
```
The meaning of any is given below.
It seems like you're in the process of setting up a new Laravel project and you're being asked to choose a starter kit. Starter kits are pre-configured templates that help you bootstrap your project with common features and functionality. Here's a brief overview of the options you're presented with:

- **No starter kit**: Selecting this option means you'll start with a clean slate and manually configure your project's structure and features as needed. This can be a good choice if you want full control over your project's setup.

- **Laravel Breeze**: Laravel Breeze is a lightweight starter kit that provides basic authentication features like registration, login, and password reset. It's suitable for simple projects that require user authentication without complex features.

- **Laravel Jetstream**: Laravel Jetstream is a more feature-rich starter kit that offers various authentication options including team collaboration, API support, and more advanced features. It provides both Livewire and Inertia.js stacks for front-end interactions.

The choice of starter kit depends on the requirements of your project:

- If you need a simple authentication setup, Laravel Breeze might be sufficient.
- If you need more advanced authentication options, teams, and API support, Laravel Jetstream could be a better fit.
- If you want complete control over setting up your project, you can choose the "No starter kit" option and build your project from scratch.

Consider your project's needs and the features provided by each starter kit when making your selection. You can always refer to the official Laravel documentation for more details on each option and how to proceed with your chosen starter kit.

Sometimes, when you install `laravel`, the files are in a dot directory such as `/home/your_username/.config/composer/vendor/laravel/installer/bin/`
If it is the case,you may make this path global for that laravel be executed from everywhere.

4.1. **Making laravel installation path global**

To allow the Laravel installer located in `/home/user/.config/composer/vendor/laravel/installer/bin/` to be launched from anywhere in the terminal, you need to add the directory to your system's PATH. Here's how you can do that:

4.1.1. **Edit Your Shell Configuration File**:
   Depending on the shell you're using (e.g., Bash, Zsh), you'll need to edit the appropriate configuration file. Commonly used shells are Bash and Zsh. If you're unsure which shell you're using, you can check by running `echo $SHELL`.

   - If you're using Bash, edit the `~/.bashrc` file.
   - If you're using Zsh, edit the `~/.zshrc` file.

   Use a text editor to open the appropriate file. For example, using `nano`:

   ```bash
   nano ~/.bashrc
   # OR
   nano ~/.zshrc
   ```

4.1.2. **Add the Directory to PATH**:
   In the configuration file, you'll need to add a line that adds the Laravel installer's `bin` directory to your PATH. Add the following line at the end of the file:

   ```bash
   export PATH="$PATH:/home/user/.config/composer/vendor/laravel/installer/bin/"
   ```

   Make sure to replace `/home/user` with your actual home directory path.

4.1.3. **Save and Apply Changes**:
   After adding the line to the configuration file, save the file and exit the text editor.

   - In `nano`, press `Ctrl` + `O` to save and `Ctrl` + `X` to exit.
   - In other text editors, follow their respective save and exit commands.

4.1.4. **Apply Changes to the Current Session**:
   To apply the changes immediately to your current terminal session, you can run the following command (assuming you're using Bash):

   ```bash
   source ~/.bashrc
   ```

   If you're using Zsh, use the following command:

   ```bash
   source ~/.zshrc
   ```

4.1.5. **Verify**:
   You can now test if the Laravel installer can be launched from anywhere in the terminal by typing `laravel`:

   ```bash
   laravel
   ```

   If the command works without specifying the full path, then the PATH configuration was successful.

Now you should be able to run the Laravel installer command (`laravel`) from any directory in the terminal without needing to provide the full path to the executable.


5. **Configure .env File**:
   Copy the `.env.example` file to `.env` and update the database configuration with the credentials you set earlier.

   ```bash
   cp .env.example .env
   nano .env
   ```

6. **Generate Application Key**:
   Run the following command to generate the application key, which is used for encryption and other security purposes.

   ```bash
   php artisan key:generate
   ```

7. **Configure Apache**:
   Create a new Apache site configuration file or edit the default one to point to your Laravel project directory. Here's an example of what it might look like:

   ```apache
   <VirtualHost *:80>
       ServerName your-project.local
       DocumentRoot /path/to/your-project/public
       <Directory /path/to/your-project/public>
           AllowOverride All
           Require all granted
       </Directory>
   </VirtualHost>
   ```

   Make sure to replace `/path/to/your-project` with the actual path to your Laravel project.

8. **Enable the Site and Restart Apache**:

   ```bash
   sudo a2ensite your-site.conf
   sudo systemctl restart apache2
   ```

9. **Add Host Entry**:
   Add an entry to your `/etc/hosts` file to associate the chosen hostname (e.g., `your-project.local`) with the localhost IP address.

   ```bash
   sudo nano /etc/hosts
   ```

   Add a line like this:

   ```
   127.0.0.1   your-project.local
   ```

10. **Access Your Laravel Project**:
    Open a web browser and navigate to the address you set up (e.g., `http://your-project.local`). You should see your Laravel application running.

Remember that these steps provide a basic setup for Laravel on Kali Linux. Depending on your needs and the specifics of your project, you might need to make further configurations or install additional packages. Always refer to the Laravel documentation and Kali Linux documentation for the latest and most accurate instructions.




[FRENCH VERSION]

Pour installer Laravel sur Kali Linux, vous devrez suivre ces étapes générales. Veuillez noter que les versions des logiciels et des packages peuvent avoir changé depuis ma dernière mise à jour des connaissances en septembre 2021, alors assurez-vous d'adapter ces étapes aux dernières versions et recommandations.

1. **Installez le logiciel requis** :
    Avant d'installer Laravel, vous devez avoir installé un serveur Web, PHP, Composer (un gestionnaire de dépendances PHP) et d'autres composants nécessaires.

    ```bash
    mise à jour sudo apt
    sudo apt installer apache2 php php-cli php-mbstring php-xml composer
    ```

2. **Installez MySQL ou MariaDB** (facultatif) :
    Laravel utilise généralement une base de données pour stocker des données. Vous pouvez choisir entre MySQL ou MariaDB. Installez l'un d'entre eux en fonction de vos préférences.

    ```bash
    sudo apt installer mysql-server
    # OU
    sudo apt installer mariadb-server
    ```

3. **Configurer la base de données** :
    Si vous avez installé une base de données, vous devez la configurer. Cela inclut la définition du mot de passe root et la création d'une base de données pour votre projet Laravel.

    ```bash
    sudo mysql_secure_installation
    mysql -u racine -p

    # À l'intérieur du shell MySQL/MariaDB
    CRÉER UNE BASE DE DONNÉES laravel_db ;
    CRÉER UN UTILISATEUR 'laravel_user'@'localhost' IDENTIFIÉ PAR 'votre_mot de passe' ;
    GRANT ALL ON laravel_db.* TO 'laravel_user'@'localhost' ;
    PRIVILÈGES FLUSH ;
    SORTIE;
    ```

4. **Installez Laravel** :
    Accédez au répertoire où vous souhaitez installer votre projet Laravel et exécutez les commandes suivantes :

    ```bash
    compositeur global nécessite laravel/installer
    laravel nouveau nom de votre projet
    cd nom-de-votre-projet
    ```
Lors de l'exécution de la commande `laravel new projectName`, ceci apparaîtra :

```
Vous souhaitez installer un kit de démarrage ? ────────────────────┐
  │ › ● Pas de kit de démarrage │
  │ ○ Laravel Brise │
  │ ○ Laravel Jetstream
```
La signification de any est donnée ci-dessous.
Il semble que vous soyez en train de mettre en place un nouveau projet Laravel et qu'on vous demande de choisir un kit de démarrage. Les kits de démarrage sont des modèles préconfigurés qui vous aident à démarrer votre projet avec des fonctionnalités et fonctionnalités communes. Voici un bref aperçu des options qui vous sont présentées :

- **Aucun kit de démarrage** : la sélection de cette option signifie que vous commencerez avec une table rase et que vous configurerez manuellement la structure et les fonctionnalités de votre projet selon vos besoins. Cela peut être un bon choix si vous voulez un contrôle total sur la configuration de votre projet.

- **Laravel Breeze** : Laravel Breeze est un kit de démarrage léger qui fournit des fonctionnalités d'authentification de base telles que l'enregistrement, la connexion et la réinitialisation du mot de passe. Il convient aux projets simples qui nécessitent une authentification de l'utilisateur sans fonctionnalités complexes.

- **Laravel Jetstream** : Laravel Jetstream est un kit de démarrage plus riche en fonctionnalités qui offre diverses options d'authentification, notamment la collaboration en équipe, la prise en charge de l'API et des fonctionnalités plus avancées. Il fournit à la fois des piles Livewire et Inertia.js pour les interactions frontales.

Le choix du kit de démarrage dépend des exigences de votre projet :

- Si vous avez besoin d'une configuration d'authentification simple, Laravel Breeze peut suffire.
- Si vous avez besoin d'options d'authentification, d'équipes et d'une prise en charge d'API plus avancées, Laravel Jetstream pourrait être mieux adapté.
- Si vous souhaitez un contrôle total sur la configuration de votre projet, vous pouvez choisir l'option "Pas de kit de démarrage" et créer votre projet à partir de zéro.

Tenez compte des besoins de votre projet et des fonctionnalités fournies par chaque kit de démarrage lors de votre sélection. Vous pouvez toujours vous référer à la documentation officielle de Laravel pour plus de détails sur chaque option et comment procéder avec le kit de démarrage que vous avez choisi.

Parfois, lorsque vous installez `laravel`, les fichiers se trouvent dans un répertoire de points tel que `/home/your_username/.config/composer/vendor/laravel/installer/bin/`
Si c'est le cas, vous pouvez rendre ce chemin global pour que laravel soit exécuté de partout.

4.1. ** Rendre le chemin d'installation de laravel global **

Pour permettre au programme d'installation de Laravel situé dans `/home/user/.config/composer/vendor/laravel/installer/bin/` d'être lancé de n'importe où dans le terminal, vous devez ajouter le répertoire au PATH de votre système. Voici comment procéder :

4.1.1. **Modifiez votre fichier de configuration Shell** :
    Selon le shell que vous utilisez (par exemple, Bash, Zsh), vous devrez modifier le fichier de configuration approprié. Les shells couramment utilisés sont Bash et Zsh. Si vous ne savez pas quel shell vous utilisez, vous pouvez vérifier en exécutant `echo $SHELL`.

    - Si vous utilisez Bash, éditez le fichier `~/.bashrc`.
    - Si vous utilisez Zsh, éditez le fichier `~/.zshrc`.

    Utilisez un éditeur de texte pour ouvrir le fichier approprié. Par exemple, en utilisant `nano` :

    ```bash
    nano ~/.bashrc
    # OU
    nano ~/.zshrc
    ```

4.1.2. **Ajouter le répertoire à PATH** :
    Dans le fichier de configuration, vous devrez ajouter une ligne qui ajoute le répertoire `bin` du programme d'installation de Laravel à votre PATH. Ajoutez la ligne suivante à la fin du fichier :

    ```bash
    export PATH="$PATH:/home/user/.config/composer/vendor/laravel/installer/bin/"
    ```

    Assurez-vous de remplacer `/home
