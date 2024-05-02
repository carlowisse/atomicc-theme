# HOW TO CREATE A COLOR THEME

## REQUIREMENTS
* Git
* Node.JS
* npm
* yo
* generator-code
* vsce
* [Azure DevOps Account](https://dev.azure.com/)

## SETUP
```bash
npm install -g yo generator-code vsce

yo code
```

1. Select New Color Theme
1. Select No, start fresh
1. Enter the name of your extension
2. Enter your extension identifier (`{publisher-name}.{identifier}` | just press enter and use the default)
3. Write a short description of what the theme represents or what the idea behind the theme is
4. Enter the name (case sensitive) as you want it to appear in the marketplace (This is the extension display name)
5. Select a base theme to be used as a starting point

```bash
cd THEME_NAME
code .
```

## DEVELOPMENT
* Edit `themes/[THEME_NAME].json`
* To test your theme, press `F5`
* This opens a new vscode instance with your theme loaded and is hot-reloaded on save
* View syntax token scopes
  * `Ctrl+Shift+P` -> `Developer: Inspect Editor Tokens and Scopes`
* [Color Theme Reference](https://code.visualstudio.com/api/references/theme-color)

## AZURE DEVOPS, MARKETPLACE & PUBLISHING
### INITIAL SETUP
* [Create an Organization](https://learn.microsoft.com/azure/devops/organizations/accounts/create-organization)
* [Create Personal Access Token](https://dev.azure.com/)
  * Click on User Settings (second icon from the top right)
  * Click Personal Access Tokens
  * Click New Token
  * Details:
    * Name: vsce
    * Organization: All accessible organizations
    * Expiration: Never
    * Scopes: Custom defined
      * Click Show all scopes
      * Scroll down to Marketplace
      * Check Manage
  * Click Create
* [Create Publisher](https://marketplace.visualstudio.com/manage)
  * Login with the same account as the Personal Access Token
  * Click on Create Publisher
  * Enter the publisher name
    * ID: the unique identifier for your publisher in Marketplace that will be used in your extension URLs
    * Name: the unique name of your publisher that will be displayed in Marketplace
  * Click Create
  * Verify the newly created publisher using `vsce`
    * vsce login [PUBLISHER_ID]

### PERSONAL ACCESS TOKEN
* Go to https://dev.azure.com/[ORGANIZATION]
* Login
* Click on User Settings (second icon from the top right)
* Click Personal Access Tokens
* Select the token you want to use
* Click Regenerate

### PACKAGING
> Creates a .vsix file for manual uploading to the marketplace
```bash
vsce package
```

### PUBLISHING
> Automatically uploads the .vsix file to the marketplace (initially)
```bash
vsce login [PUBLISHER_ID]
vsce publish
```

### UPDATING
> Updates the version number in package.json and uploads it to the marketplace
```bash
vsce login [PUBLISHER_ID]

vsce publish patch

vsce publish minor

vsce publish major
```
