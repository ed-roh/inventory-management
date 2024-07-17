# EC2 Setup Instructions

## 1. Connect to EC2 Instance via EC2 Instance Connect

## 2. Install Node Version Manager (nvm) and Node.js

- **Switch to superuser and install nvm:**

```
sudo su -
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

- **Activate nvm:**

```
. ~/.nvm/nvm.sh
```

- **Install the latest version of Node.js using nvm:**

```
nvm install node
```

- **Verify that Node.js and npm are installed:**

```
node -v
npm -v
```

## 3. Install Git

- **Update the system and install Git:**

```
sudo yum update -y
sudo yum install git -y
```

- **Check Git version:**

```
git --version
```

- **Clone your code repository from GitHub:**

```
git clone [your-github-link]
```

- **Navigate to the directory and install packages:**

```
cd inventory-management
npm i
```

- **Create Env File and Port 80:**

```
echo "PORT=80" > .env
```

- **Start the application:**

```
npm start
```

## 4. Install pm2 (Production Process Manager for Node.js)

- **Install pm2 globally:**

```
npm i pm2 -g
```

- **Create a pm2 ecosystem configuration file (inside server directory):**

```
module.exports = { apps : [{ name: 'inventory-management', script: 'npm', args: 'run dev', env: { NODE_ENV: 'development', ENV_VAR1: 'environment-variable', } }], };
```

- **Modify the ecosystem file if necessary:**

```
nano ecosystem.config.js
```

- **Set pm2 to restart automatically on system reboot:**

```
sudo env PATH=$PATH:$(which node) $(which pm2) startup systemd -u $USER --hp $(eval echo ~$USER)
```

- **Start the application using the pm2 ecosystem configuration:**

```
pm2 start ecosystem.config.js
```

- **Useful pm2 commands:**

  - **Stop all processes:**

  ```
  pm2 stop all
  ```

  - **Delete all processes:**

  ```
  pm2 delete all
  ```

  - **Check status of processes:**

  ```
  pm2 status
  ```

  - **Monitor processes:**

  ```
  pm2 monit
  ```
