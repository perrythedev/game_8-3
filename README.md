# String Transformer Application

A Flask web application that transforms strings based on predefined patterns with access control and administrative features.

## Overview

The String Transformer application allows users to submit strings and receive transformed versions based on predefined patterns. Key features include:

- **One-Time Access**: Once a transformed string has been viewed, it cannot be accessed again
- **IP-Based Restrictions**: Prevents multiple views from the same IP address
- **Admin Dashboard**: Manage string patterns, users, and view access logs
- **Blueprint Architecture**: Modular code structure for better maintainability
- **Proxy Support**: Properly handles real client IP addresses when behind proxies like Nginx
- **Maintenance Utilities**: Integrated tools for maintenance and troubleshooting
- **Mobile Support**: Dedicated mobile interface with optimized user experience

## Installation

### Prerequisites

- Python 3.6+ 
- pip (Python package manager)
- Git (optional)

### Quick Setup

1. Clone the repository or download the source code:
   ```bash
   git clone https://github.com/huythedev/game_8-3.git
   cd game_8-3
   ```

2. Create a virtual environment:
   ```bash
   python -m venv venv
   ```
   or
   ```bash
   python3 -m venv venv
   ```

3. Activate the virtual environment:
   - Windows: `venv\Scripts\activate`
   - Linux/macOS: `source venv/bin/activate`

4. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```
   or
   ```bash
   pip3 install -r requirements.txt
   ```

5. Create a `.env` file from the template:
   ```bash
   cp .env.example .env
   ```
   
6. Edit the `.env` file to configure your installation.

7. Run the application:
   ```bash
   python app.py
   ```
   or
   ```bash
   python3 app.py
   ```
   
## Configuration

Configuration is managed through environment variables, which can be set in a `.env` file:

| Variable | Description | Default |
|----------|-------------|---------|
| SECRET_KEY | Flask secret key for session security | Random generated |
| DATABASE_URI | SQLAlchemy database URI | sqlite:///strings.db |
| SECURE_COOKIES | Enable secure cookies | True |
| HOST | Host address to bind | 127.0.0.1 |
| PORT | Port number | 8000 |
| DEBUG | Flask debug mode | False |
| BEHIND_PROXY | Whether app is behind a proxy | False |

## Admin Access

After installation, you can access the admin interface at `/admin/login` with these default credentials:

- **Username**: admin
- **Password**: 123

*Important: Change this password immediately after first login!*

## Maintenance Utilities

The application includes a comprehensive maintenance utility that can help fix common issues:

```bash
python maintenance.py
```

This provides a menu-driven interface for:

1. Resetting the database
2. Fixing database issues
3. Fixing route issues
4. Checking critical templates
5. Performing a quick fix of all systems

## Production Deployment

### Using Waitress

```bash
python -m waitress --host=0.0.0.0 --port=8000 wsgi:application
```
or
```bash
python3 -m waitress --host=0.0.0.0 --port=8000 wsgi:application
```

### Nginx Configuration

When using Nginx as a reverse proxy, ensure you have the correct configuration to forward client IP addresses:

```nginx
location / {
    proxy_pass http://127.0.0.1:8000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

Also, set `BEHIND_PROXY=True` in your `.env` file.

## Troubleshooting

### Common Issues

- **Database Errors**: Run the maintenance utility and choose "Fix Database Issues" or "Reset Database" option.
- **Permission Denied**: Ensure the directory has proper write permissions for log files.
- **Missing Templates**: Use the "Fix Critical Templates" option in the maintenance menu.
- **Route Issues**: Select "Fix Route Issues" from the maintenance menu.

## Development

### Virtual Environment

Always use a virtual environment for development:

```bash
python -m venv venv
source venv/bin/activate  # Linux/macOS
venv\Scripts\activate     # Windows
```

### Installing Development Dependencies

```bash
pip install -r requirements-dev.txt
```

### Running Tests

```bash
pytest
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Security Considerations

- The application restricts access to transformed strings based on IP addresses.
- Admin pages require authentication.
- Be cautious about exposing the application directly to the internet without proper security measures.
- Consider changing the default admin password immediately after installation.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request
