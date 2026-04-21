# Gitea Theme

This should be a temporary solution until [Gitea](https://github.com/go-gitea/gitea) reinvents the `soft contrast, low light theme`. Inspired by https://github.com/go-gitea/gitea/issues/31308.


Any updates, comments, or pull requests are appreciated. At the time of the first publication, it is based on the new `gitea-dark-theme` with some color accents based on previous `arc-green-theme`.

***update:*** compatible with `release 1.26.0`

## How to Install

1. **Login to Gitea Web Interface Admin Account**  
   Identify the `Custom File Root Path`.
   
2. **Locate Server Configuration**  
   On the left panel, click `Configuration -> Summary` and look at the end of `Server Configuration`, e.g., `/var/lib/gitea/custom`.

3. **Create Folder Structure on Gitea Host Machine**  
   Create the `public/assets/css` folder structure and then change the owner and group to `git` `(sudo chown git:git css)`

4. **Copy Updated CSS File**  
   Copy `theme-arc-green-updated.css` into the newly created `public/assets/css` folder. Assign the copied file to the `git` user and group:
   ```bash
   sudo chown git:git /var/lib/gitea/custom/public/assets/css/theme-arc-green-updated.css
   ```
   do same for other files and folders: `theme-gitea-auto.css`, `chroma/dark.css`, `codemirror/dark.css`.

5. **Enable `.bas` file syntax highlighting in the editor** *(optional)*  
   `.bas` (BASIC/VBA) files are not registered in Gitea's built-in CodeMirror language list.
   A custom footer template is provided to fix this: it patches the editor configuration
   at page-load time so that `.bas` files are highlighted using the VB.NET language mode.

   Create the `templates/custom` folder structure and copy the template:
   ```bash
   mkdir -p /var/lib/gitea/custom/templates/custom
   cp templates/custom/footer.tmpl /var/lib/gitea/custom/templates/custom/footer.tmpl
   sudo chown git:git /var/lib/gitea/custom/templates/custom/footer.tmpl
   ```

   > **Note:** If you already have a custom `footer.tmpl`, merge the `<script>` block from
   > this file into your existing template.

6. **Confirm Configuration File Path**  
   If you want to make the new theme default for the login page and new users, go back to the web interface to confirm the `Configuration File Path`, e.g., `/etc/gitea/app.ini`.

7. **Make the new theme default for the login page and new users**  
   Add or update the following section in the configuration file:
   ```ini
   [ui]
   DEFAULT_THEME = arc-green-updated
   ```

8. **Restart Gitea**  
   Restart Gitea to apply the changes:
   ```bash
   sudo systemctl restart gitea
   ```
