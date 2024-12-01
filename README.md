# Sync-Github-Nginx

A lightweight CI/CD pipeline that automatically synchronizes a GitHub repository with an Nginx web server. The system continuously monitors your GitHub repository for changes and automatically deploys updates to your web server.

## Features

- Real-time monitoring of GitHub repository changes
- Automatic deployment to Nginx web server
- SHA-based commit tracking to prevent redundant updates
- Simple logging system for tracking deployments
- Bash-based wrapper scripts for easy automation
- Minimal configuration required

## Prerequisites

- Linux-based operating system
- Python 3.x installed
- Git installed
- Nginx web server configured
- Sudo privileges on the server
- GitHub repository access

## Requirements

```bash
pip install requests
```

## Directory Structure

```
Sync-Github-Nginx/
├── check_github.py
├── ci_cd_wrapper.sh
├── update_website.sh
├── index.html
└── last_commit.txt
```

## Installation & Setup

1. Clone the repository to your Nginx web directory:
```bash
cd /var/www/html
git clone https://github.com/aakashrawat1910/Sync-Github-Nginx.git
```

2. Make the scripts executable:
```bash
chmod +x ci_cd_wrapper.sh update_website.sh
```

3. Update the configuration in `check_github.py`:
```python
REPO_OWNER = 'your-username'
REPO_NAME = 'your-repo-name'
```

4. Set up a cron job to run the wrapper script periodically:
```bash
crontab -e
# Add the following line to run every minute:
* * * * * /var/www/html/Sync-Github-Nginx/ci_cd_wrapper.sh >> /var/www/html/Sync-Github-Nginx/ci_cd.log 2>&1
```

## How It Works

1. The system periodically checks your GitHub repository for new commits
2. When changes are detected, it:
   - Pulls the latest changes from GitHub
   - Updates the local files
   - Restarts Nginx if necessary
   - Logs the deployment status

## Sample Output

### When No Changes Are Detected
```bash
$ ./ci_cd_wrapper.sh
No new changes
```

### When Changes Are Detected
```bash
$ ./ci_cd_wrapper.sh
New changes detected
From https://github.com/username/Sync-Github-Nginx
 * branch            main       -> FETCH_HEAD
Updating 72bc70d..1f9c866
Fast-forward
 index.html | 1 +
 1 file changed, 1 insertion(+)
Website updated successfully
```

## Common Issues and Troubleshooting

1. **Python Script Not Found Error**
```
python3: can't open file './check_github.py': [Errno 2] No such file or directory
```
Solution: Ensure you're using the full path to the script in your cron job or when executing manually.

2. **Sudo Password Prompt**
```
sudo: a terminal is required to read the password
```
Solution: Configure sudo to allow Nginx restart without password, or use appropriate system permissions.

## Screenshots

Since this is a command-line tool, the main visual output is through the terminal. Here's what you might see:

```
Terminal Output Example:
----------------------
$ ./ci_cd_wrapper.sh
New changes detected
Website updated successfully
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is open source and available under the MIT License.


