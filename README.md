# Writeurl  

## An Online Collaborative Editor  

Writeurl is a simple and flexible collaborative text editor.  

### Key Features  
- **Collaborative Editing**: Writeurl is a client-server system.  
- **Frontend**: Built in pure JavaScript with no frameworks.  
- **Backend**: Powered by a Node.js application.  
- **Real-Time Communication**: The client and server use WebSocket connections.  
- **Offline Support**: Changes are saved locally in your browser and synced to the server when a connection is available.  

### Document Sharing  
Writeurl makes sharing documents easy with a URL-based structure:  
- **Editable Document**:  
  `www.writeurl.com/text/id/read-password/write-password`  
- **Read-Only Document**:  
  `www.writeurl.com/text/id/read-password`  

No user registration is required. Just share the URL to collaborate or provide read-only access.  

---  

## Using Writeurl  

### Online Service  
Writeurl is available as an online service at [www.writeurl.com](https://www.writeurl.com).  
The online service runs the same code as provided in the Writeurl GitHub repository.  

### Local Installation  
You can install and run Writeurl locally as an alternative to the online service.  

#### Installation Instructions  

##### Dependencies  
- **Node.js**: Use version 8 or higher.  
- **Modules**: All required modules are listed in `package.json`.  

##### Steps to Install  
1. **Clone the Repository**:  
   ```bash
   git clone https://github.com/morten-krogh/writeurl.git
   ```  
2. **Install Node.js Modules**:  
   ```bash
   npm install
   ```  
3. **Build the Browser Code**:  
   Navigate to the `writeurl` directory and run:  
   ```bash
   bash build.sh browser
   ```  
   The browser code will be available in `build/release/browser/`.  

4. **Configure the Server**:  
   - Server code is located in `server-nodejs-express`.  
   - Create a configuration file (`config.yaml`) based on the example provided:  
     ```yaml
     port: 9000
     release:
       public: /path/to/build/release/browser
     debug:
       host: debug.writeurl.localhost
       public: /path/to/build/debug/browser
     documents:
       path: /path/to/document/storage
     publish:
       public: /path/to/publish/storage
     logger:
       level: trace
     ```  

5. **Start the Server**:  
   Navigate to the `server-nodejs-express` directory and run:  
   ```bash
   node writeurl-server.js config.yaml
   ```  

6. **Start Writing**:  
   Open your browser and go to `http://localhost:9000` to start using Writeurl.  

---  

## Example Production Setup  

For production use, it’s recommended to:  
1. Use a reverse proxy with TLS (e.g., Nginx).  
2. Daemonize the Writeurl server using a process manager like PM2 or systemd.  

### Example Nginx Configuration  
An example `nginx.conf` file is available [here](https://github.com/morten-krogh/writeurl/blob/master/documentation/nginx.conf).  

### Example systemd Unit File  
```ini
[Unit]
Description=Writeurl Server
After=network.target

[Service]
Type=simple
User=www
ExecStart=/path/to/node /path/to/writeurl/server-nodejs-express/writeurl-server.js /path/to/config.yaml
Restart=on-failure

[Install]
WantedBy=multi-user.target
```  

---  

## Backup  

The server can be backed up by saving the directories specified in the `documents` and `publish` sections of `config.yaml`.  
- **Backup Options**: Any file backup tool can be used (e.g., `rsync`).  
- **Live Backups**: Backups can be created while the server is running, as long as no files are modified during the process.  
- **Restoration**: To restore from a backup, place the backed-up directories in the locations specified in `config.yaml`.  

---  

## Embedding Writeurl  

Writeurl can be embedded into other applications or websites.  
- See the [embedding documentation](https://github.com/morten-krogh/writeurl/blob/master/html/embed/index.html) for details.  
- The online service includes an embedding example at [https://www.writeurl.com/embed](https://www.writeurl.com/embed).  

---  

# HOW TO CONTRIBUTE
- Fork the Repository: Click the "Fork" button to create your own copy of the repository.
- Clone the Repository: Use the command git clone <your-forked-repo-url> to download it locally.
- Create a New Branch: Run git checkout -b <branch-name> to work on a separate branch.
- Make Your Changes: Modify code, fix bugs, or update documentation as needed.
- Commit Your Changes: Use git commit -m "Descriptive message about your changes" to save your changes locally.
- Push to GitHub: Push the changes to your forked repository with git push origin <branch-name>.
- Create a Pull Request (PR): Go to the original repository and open a pull request explaining your changes.
- Address Feedback: Be ready to discuss and make additional changes if needed during the review process.