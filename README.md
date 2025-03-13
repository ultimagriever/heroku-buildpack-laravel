# Heroku Buildpack for Laravel >=11

A Heroku buildpack designed specifically for Laravel >=11 applications with asset building support. This buildpack handles PHP dependencies, Node.js installation, asset compilation, and proper Laravel configuration for production deployment.

## Features

- PHP 8.2+ support
- Node.js 22.7.0 for asset building
- Automatic composer dependency installation
- npm dependency management
- Asset compilation using Vite
- Laravel optimization and caching
- Proper directory permissions setup
- Apache configuration with SSL support

## Requirements

Your Laravel application must have:

- PHP 8.2 or higher
- Laravel >= 11
- `composer.json` file
- `package.json` file
- `.env.example` file
- Valid Vite configuration (default Laravel 11 setup)

## Usage

### 1. Create a New Heroku App

```bash
heroku create your-app-name
```

### 2. Add Buildpacks

```bash
# Add this buildpack
heroku buildpacks:set https://github.com/ultimagriever/heroku-buildpack-laravel.git

# Add the official PHP buildpack
heroku buildpacks:add heroku/php
```

### 3. Configure Environment Variables

```bash
heroku config:set APP_NAME="Your App Name"
heroku config:set APP_ENV=production
heroku config:set APP_DEBUG=false
heroku config:set APP_URL=https://your-app-name.herokuapp.com
```

### 4. Deploy Your Application

```bash
git push heroku main
```

## Configuration

### Required Files in Your Laravel Project

1. `composer.json`:
```json
{
    "require": {
        "php": "^8.2",
        "laravel/framework": "^11.0"
    }
}
```

2. `package.json`:
```json
{
    "private": true,
    "scripts": {
        "dev": "vite",
        "build": "vite build"
    },
    "devDependencies": {
        "vite": "^5.0.0"
    }
}
```

3. `Procfile`:
```
web: heroku-php-apache2 public/
```

### Apache Configuration

The buildpack includes a default Apache configuration with:
- SSL enforcement
- Proper routing for Laravel
- Security headers
- Static file handling

## Build Process

1. Detects Laravel application
2. Installs Composer
3. Installs PHP dependencies
4. Installs Node.js and npm
5. Installs npm dependencies
6. Builds assets using Vite
7. Sets up storage directories
8. Creates environment file
9. Generates application key
10. Optimizes Laravel for production

## Troubleshooting

### Common Issues

1. **Build Fails During Asset Compilation**
    - Ensure all required npm dependencies are in `package.json`
    - Check if Vite configuration is correct
    - Verify Node.js compatibility

2. **Application Error After Deploy**
    - Check Heroku logs: `heroku logs --tail`
    - Verify environment variables are set
    - Ensure storage directory permissions are correct

3. **Database Connection Issues**
    - Configure database URL in Heroku config vars
    - Verify database credentials in `.env`

### Debug Mode

To enable debug mode temporarily:

```bash
heroku config:set APP_DEBUG=true
```

Remember to disable it in production:

```bash
heroku config:set APP_DEBUG=false
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support, please:
1. Check existing issues or create a new one
2. Provide detailed information about your setup
3. Include relevant logs and error messages

## Security

If you discover any security-related issues, please email your-email@example.com instead of using the issue tracker.

## Acknowledgments

- Laravel Team
- Heroku Team
- All contributors and maintainers
