# Static Files PHP Example

This example demonstrates serving PHP files directly from a directory structure instead of embedding them.

## Features

- Serves PHP files directly from the `www` directory
- No embedding or file extraction required
- Edit PHP files directly without recompiling
- Supports a complete directory structure
- Handles static files seamlessly
- Supports both development and production modes

## Files

- `main.go` - The Go application that serves PHP files
- `www/index.php` - Home page with links to other pages
- `www/about.php` - Information about the example
- `www/contact.php` - Contact form with POST handling
- `www/counter.php` - Session-based counter example

## Running the Application

### Development Mode (Default)

For instant file change detection and no caching:

```bash
cd playground/static-files
CGO_CFLAGS="-I/usr/local/include/php -I/usr/local/include/php/main -I/usr/local/include/php/Zend -I/usr/local/include/php/TSRM -I/usr/local/include/php/ext" \
CGO_LDFLAGS="-L/usr/local/lib -lphp" \
PORT=8082 go run -tags=nowatcher .
```

### Production Mode

For better performance with caching:

```bash
cd playground/static-files
CGO_CFLAGS="-I/usr/local/include/php -I/usr/local/include/php/main -I/usr/local/include/php/Zend -I/usr/local/include/php/TSRM -I/usr/local/include/php/ext" \
CGO_LDFLAGS="-L/usr/local/lib -lphp" \
PHP_PRODUCTION=1 PORT=8082 go run -tags=nowatcher .
```

You can change the port by setting a different value for the `PORT` environment variable.

## Modes Explained

1. **Development Mode**:
   - Detects file changes immediately
   - Disables PHP opcache
   - Adds no-cache headers to responses
   - Displays timestamps for debugging
   - Best for active development

2. **Production Mode**:
   - Checks for file changes less frequently (every 5 seconds)
   - Enables PHP opcache
   - Allows browser caching (60 seconds)
   - Better performance for production use

## Accessing the Application

Once running, you can access the application at:

http://localhost:8082

## Key Advantages

1. **Development Workflow**: Edit PHP files directly without recompiling Go code
2. **No Temporary Files**: PHP files are served from their original location
3. **Full Directory Support**: Supports complex directory structures
4. **Natural PHP Development**: Works like a traditional PHP server 