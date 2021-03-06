<!-- TITLE: Install -->
<!-- SUBTITLE: How to install Wiki.js on your server -->
![Wiki.js](/uploads/page-icons/logo.png "Logo"){.pagelogo}
# Prerequisites
Make sure you have read the [prerequisites](/wiki/prerequisites) page to ensure your server meets the minimum requirements.

# Installation
**Create an empty folder** where Wiki.js should be installed.

From this folder, in a command prompt, **run** the following command (exactly as displayed):
```bash
npm install wiki.js@latest
```

**Wait** for the installation to complete. If you see any error(s) in red, make sure you fix them first. Wiki.js will most likely crash or refuse to start if all dependencies are not properly installed. Note that you can safely ignore warnings (in yellow).

> **Behind a proxy?**
> 
> No problem. You can download the `wiki-js.tar.gz` file directly from the [GitHub Releases](https://github.com/Requarks/wiki/releases) and place the archive to the root of the folder where Wiki.js should be installed (do not extract!). Then run the command above to complete the installation. The install script will use the local archive instead of downloading it from the internet.
> 
> Note that you must have preconfigured npm to use your proxy first, as dependencies are still fetching from the internet.

> **Yarn**
> 
> Do not install Wiki.js using yarn. Installation progress will not be displayed correctly and you may not be able to use the interactive selection screen at the end of the installation process.
{.is-warning}

# Configuration
Once the installation is completed, you'll be prompted to run the configuration wizard. Use the arrow keys to choose the desired port on which to run the configuration wizard. By default, port 3000 will be used.

> If using a non-interactive terminal, you'll need to start the configuration wizard manually by running the command `node wiki configure`.  
> To use a custom port, use the following command: `node wiki configure 1234` where 1234 is the custom port.

Using your web browser, navigate to http://localhost:3000/ (replace `localhost` with the IP of your server / custom port if applicable) and follow the on-screen instructions.

All settings entered during the configuration wizard are saved in the file `config.yml`. See the [Configuration File](/wiki/install/configuration) guide for all the possible options you can use.

# Run Wiki.js
The configuration wizard will automatically start Wiki.js for you.

To start Wiki.js manually, in a command prompt, **run** the following command: `node wiki start`  
	- If using a Powershell prompt (default on Windows 10), you can instead use the `.\wiki start` command.  
	- **Wait** for the command to complete. This can take several seconds.  
	- **Browse** to your Wiki from your browser. You should see the Wiki.js welcome screen.

> Wiki.js runs as a background process, using [pm2](http://pm2.keymetrics.io/) as its process manager.

# Notes
### Stop Wiki.js
To stop Wiki.js, run the command: 
```bash
# On Linux, Mac and Windows running a terminal / traditional command prompt:
node wiki stop

# On Windows, if using a Powershell prompt, you can instead use the following syntax:
.\wiki stop
```

### Restart Wiki.js
To restart Wiki.js, run the command: 
```bash
# On Linux, Mac and Windows running a terminal / traditional command prompt:
node wiki restart

# On Windows, if using a Powershell prompt, you can instead use the following syntax:
.\wiki restart
```

### Run at startup

By default, Wiki.js will not start automatically following a system reboot. In order to make it start on boot, we need to setup pm2 as a global npm module and set it as a startup service:

1. Still in a command prompt, **install pm2** globally by running the following command: `npm install -g pm2`
	- Wait for the installation to complete.
2. We now need to tell pm2 to configure itself **as a startup service**.
	- On Linux/macOS, simply run the following command: `pm2 startup`
		- pm2 will generate a command for you to execute. Copy the command and execute it.
	- On Windows, we need to install an additional dependency:
		- Run the command: `npm install pm2-windows-startup -g`
		- Once finished, run the command: `pm2-startup install`
3. Finally, **save the current pm2 configuration** by running the command: `pm2 save`

### View installed version
To view the currently installed version, run the command:  
```bash
# On Linux, Mac and Windows running a terminal / traditional command prompt:
node wiki -V

# On Windows, if using a Powershell prompt, you can instead use the following syntax:
.\wiki -V
```
