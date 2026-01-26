# Gitea Theme

This should be a temporary solution until [Gitea](https://github.com/go-gitea/gitea) reinvents the `soft contrast, low light theme`. Inspired by https://github.com/go-gitea/gitea/issues/31308.


Any updates, comments, or pull requests are appreciated. At the time of the first publication, it is based on the new `gitea-dark-theme` with some color accents based on previous `arc-green-theme`.

***update:*** compatible with `release 1.25.4`

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

5. **Confirm Configuration File Path**  
   If you want to make the new theme default for the login page and new users, go back to the web interface to confirm the `Configuration File Path`, e.g., `/etc/gitea/app.ini`.

6. **Make the new theme default for the login page and new users**  
   Add or update the following section in the configuration file:
   ```ini
   [ui]
   DEFAULT_THEME = arc-green-updated
   ```

7. **Restart Gitea**  
   Restart Gitea to apply the changes:
   ```bash
   sudo systemctl restart gitea
   ```
