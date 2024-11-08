# .npmrc

![npmrc logo](npmrc.png '# NPM logo with .npmrc text overlayed')

The .npmrc file is a configuration file used by the Node Package Manager (npm) to customize and configure various settings for how npm behaves. This file can be located in the user's home directory or at the project level to override default settings.

---

## Example from Playwright repository

```.npmrc
registry=<https://nexus.xbav.io/repository/npm/>

# Disable "npm notice New minor version of npm available!" message
update-notifier=false

# Pay close attention to the engine specifications in the package.json
engine-strict=true

# Hide the message at the end of each npm install acknowledging the number of dependencies looking for funding
fund=false
```
