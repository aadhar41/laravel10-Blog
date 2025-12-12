
# **Laravel 10 Practice & Tutorial Repository 🚀**

![Laravel](https://img.shields.io/badge/Laravel-10.0-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-8.1-777BB4?style=for-the-badge&logo=php&logoColor=white)
![GitHub Stars](https://img.shields.io/github/stars/aadhar41/laravel10?style=for-the-badge)
![GitHub Forks](https://img.shields.io/github/forks/aadhar41/laravel10?style=for-the-badge)
![GitHub Issues](https://img.shields.io/github/issues/aadhar41/laravel10?style=for-the-badge)

**A comprehensive Laravel 10 practice repository** featuring authentication, blog functionality, real-time events, and modern development practices. Perfect for learning Laravel 10 features, implementing best practices, and building production-ready applications.

---

## **✨ Features**

* **Complete Authentication System** - Registration, login, password reset, and email verification
* **Blog Platform** - Create, read, update, and delete blog posts with rich text editing
* **Real-time Comments** - Live comment updates using Laravel Events and Broadcasting
* **User Profiles** - Customizable profiles with avatar uploads
* **Tag System** - Organize posts with tags and filter content
* **Modern UI** - Bootstrap 5 and Vite-based frontend with SASS
* **API Resources** - RESTful API endpoints with JSON responses
* **Testing** - Unit and feature tests with PHPUnit
* **Caching** - Advanced caching strategies with tags
* **Localization** - Multi-language support with locale middleware
* **Image Handling** - File uploads and storage management
* **Security** - CSRF protection, authentication middleware, and input validation

---

## **🛠️ Tech Stack**

* **Primary Language:** PHP 8.1+
* **Framework:** Laravel 10
* **Frontend:** Bootstrap 5, Vite, SASS
* **Database:** MySQL
* **Testing:** PHPUnit
* **Package Manager:** Composer
* **Build Tool:** Vite
* **Authentication:** Laravel Sanctum
* **Real-time:** Laravel Events & Broadcasting
* **Caching:** Redis/Memcached

**Development Tools:**
- Laravel Debugbar
- Laravel Sail (Docker)
- Laravel Pint (Code Style)
- Pest (Testing)
- Faker (Data Generation)

---

## **📦 Installation**

### **Prerequisites**

Before you begin, ensure you have the following installed:
- [PHP](https://www.php.net/downloads.php) (8.1 or higher)
- [Composer](https://getcomposer.org/download/)
- [Node.js](https://nodejs.org/) (v16 or higher)
- [MySQL](https://dev.mysql.com/downloads/) (or any other supported database)
- [Git](https://git-scm.com/downloads)

### **Quick Start**

1. **Clone the repository:**
   ```bash
   git clone https://github.com/aadhar41/laravel10.git
   cd laravel10
   ```

2. **Install dependencies:**
   ```bash
   composer install
   npm install
   ```

3. **Set up environment:**
   ```bash
   cp .env.example .env
   php artisan key:generate
   ```

4. **Configure your database** in the `.env` file:
   ```ini
   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=laravel
   DB_USERNAME=root
   DB_PASSWORD=
   ```

5. **Run migrations and seed the database:**
   ```bash
   php artisan migrate
   php artisan db:seed
   ```

6. **Compile assets:**
   ```bash
   npm run dev
   ```

7. **Start the development server:**
   ```bash
   php artisan serve
   ```

### **Using Docker (Alternative)**

If you prefer using Docker, you can leverage Laravel Sail:

1. **Install Docker and Docker Compose**
2. **Start the containers:**
   ```bash
   ./vendor/bin/sail up
   ```
3. **Run migrations:**
   ```bash
   ./vendor/bin/sail artisan migrate
   ```
4. **Access the application:**
   ```bash
   ./vendor/bin/sail artisan serve --host=0.0.0.0 --port=8000
   ```

---

## **🎯 Usage**

### **Basic Authentication Flow**

1. **Register a new user:**
   ```php
   // Example registration request
   $response = Http::post('/register', [
       'name' => 'John Doe',
       'email' => 'john@example.com',
       'password' => 'password123',
       'password_confirmation' => 'password123'
   ]);
   ```

2. **Login:**
   ```php
   // Example login request
   $response = Http::post('/login', [
       'email' => 'john@example.com',
       'password' => 'password123'
   ]);
   ```

3. **Create a blog post:**
   ```php
   // Example post creation request
   $response = Http::withHeaders([
       'Authorization' => 'Bearer ' . $token
   ])->post('/posts', [
       'title' => 'My First Post',
       'content' => 'This is the content of my first blog post.',
       'thumbnail' => $file // Uploaded file
   ]);
   ```

### **Advanced Features**

#### **Real-time Comments**

The application uses Laravel Events to broadcast new comments in real-time:

```php
// Dispatch a new comment event
event(new CommentPosted($comment));
```

#### **Caching with Tags**

The blog posts are cached with tags for efficient invalidation:

```php
// Cache a blog post with tags
$blogPost = Cache::tags(['blog-post'])->remember("blog-post-{$id}", 60, function () use ($id) {
    return BlogPost::with(['comments', 'comments.user', 'user', 'tags'])->findOrFail($id);
});
```

#### **Localization**

The application supports multiple languages through the locale middleware:

```php
// Set locale for a user
$user->locale = 'es'; // Spanish
$user->save();
```

---

## **📁 Project Structure**

```
laravel10/
├── app/
│   ├── Contracts/          # Contracts and interfaces
│   ├── Events/             # Event classes
│   ├── Facades/            # Facade classes
│   ├── Http/               # HTTP controllers, middleware, requests, and resources
│   ├── Models/             # Eloquent models
│   └── Providers/          # Service providers
├── bootstrap/              # Bootstrap files
├── config/                 # Configuration files
├── database/               # Database migrations and seeders
├── public/                 # Publicly accessible files
├── resources/              # Views and assets
│   ├── js/                 # JavaScript files
│   ├── sass/               # SASS stylesheets
│   └── views/              # Blade templates
├── routes/                 # Route definitions
├── tests/                  # Test cases
├── vendor/                 # Composer dependencies
├── .env.example            # Environment variables template
├── composer.json           # Composer dependencies
├── package.json            # Node.js dependencies
└── README.md               # This file
```

---

## **🔧 Configuration**

### **Environment Variables**

Copy `.env.example` to `.env` and configure your environment:

```ini
# Application settings
APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:...
APP_DEBUG=true
APP_URL=http://localhost

# Database settings
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=

# Mail settings
MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"
```

### **Customization Options**

1. **Change the default locale:**
   ```php
   // In AppServiceProvider.php
   public function boot()
   {
       App::setLocale(config('app.locale'));
   }
   ```

2. **Modify the blog post model:**
   ```php
   // In app/Models/BlogPost.php
   protected $fillable = [
       'title', 'content', 'user_id', 'thumbnail_path'
   ];
   ```

3. **Add new tags:**
   ```bash
   php artisan make:model Tag -m
   php artisan migrate
   ```

---


### **Register Page**
![alt text](https://raw.githubusercontent.com/aadhar41/laravel10/dev/public/screens/register-page.png)

### **Login Page**
![alt text](https://raw.githubusercontent.com/aadhar41/laravel10/dev/public/screens/login-page.png)

### **User Profile**
![alt text](https://raw.githubusercontent.com/aadhar41/laravel10/dev/public/screens/user-profile.png)

### **User Profile Edit**
![alt text](https://raw.githubusercontent.com/aadhar41/laravel10/dev/public/screens/user-profile-edit.png)

### **Posts**
![alt text](https://raw.githubusercontent.com/aadhar41/laravel10/dev/public/screens/posts.jpg)

### **Post Create**
![alt text](https://raw.githubusercontent.com/aadhar41/laravel10/dev/public/screens/posts-create.png)

### **Post Edit**
![alt text](https://raw.githubusercontent.com/aadhar41/laravel10/dev/public/screens/post-edit.png)

### **Post View**
![alt text](https://raw.githubusercontent.com/aadhar41/laravel10/dev/public/screens/post-view.png)

---

## **🤝 Contributing**

We welcome contributions from the community! Here's how you can contribute:

### **Development Setup**

1. **Fork the repository**
2. **Clone your fork:**
   ```bash
   git clone https://github.com/yourusername/laravel10.git
   cd laravel10
   ```
3. **Install dependencies:**
   ```bash
   composer install
   npm install
   ```
4. **Set up your environment:**
   ```bash
   cp .env.example .env
   php artisan key:generate
   ```

### **Code Style Guidelines**

- Follow **PSR-12** coding standards
- Use **PHP 8.1** features
- Write **comprehensive tests**
- Use **Laravel Pint** for code style consistency:
  ```bash
  composer require laravel/pint --dev
  ./vendor/bin/pint
  ```

### Pull Request Process

1. **Create a new branch:**
   ```bash
   git checkout -b feature/your-feature
   ```
2. **Make your changes**
3. **Commit your changes:**
   ```bash
   git commit -m "Add some feature"
   ```
4. **Push to the branch:**
   ```bash
   git push origin feature/your-feature
   ```
5. **Open a Pull Request** on GitHub

---

## **📝 License**

This project is open-sourced under the **MIT License**.

See the [LICENSE](LICENSE) file for more information.

---

## **👥 Authors & Contributors**

**Maintainer:**
- [Aadhar](https://github.com/aadhar41)

**Contributors:**
- [List of contributors](https://github.com/aadhar41/laravel10/graphs/contributors)

---

## **🐛 Issues & Support**

### **Reporting Issues**

If you encounter any issues or have feature requests, please open an issue on GitHub:

1. **Search existing issues** to avoid duplicates
2. **Create a new issue** with:
   - A clear title
   - Detailed description
   - Steps to reproduce (if applicable)
   - Screenshots or logs (if applicable)

### **Getting Help**

- **Laravel Forums:** [https://laravel.io](https://laravel.io)
- **Laravel Discord:** [https://discord.gg/laravel](https://discord.gg/laravel)
- **Stack Overflow:** [https://stackoverflow.com/questions/tagged/laravel](https://stackoverflow.com/questions/tagged/laravel)

---

## **🗺️ Roadmap**

### **Planned Features**

- **User Activity Tracking:** Log user actions and events
- **Rich Text Editor:** Implement a more advanced editor for blog posts
- **API Documentation:** Generate Swagger/OpenAPI documentation
- **Advanced Search:** Implement full-text search capabilities
- **Testing Framework:** Expand test coverage with more scenarios

### **Known Issues**

- **Issue #1:** [Description of the issue](link-to-issue)
- **Issue #2:** [Description of the issue](link-to-issue)

---

## **💡 Tips & Tricks**

### **Using Laravel Tinker**

Explore your application quickly with Laravel Tinker:

```bash
php artisan tinker
```

**Examples:**
```php
>>> $user = User::find(1)
>>> $user->posts()->create(['title' => 'New Post', 'content' => 'Content...'])
>>> BlogPost::with(['comments.user'])->get()
```

### **Debugging with Laravel Debugbar**

The Laravel Debugbar is included for debugging:

1. **Install dependencies:**
   ```bash
   composer require barryvdh/laravel-debugbar --dev
   ```
2. **Publish the config:**
   ```bash
   php artisan vendor:publish --provider="Barryvdh\Debugbar\ServiceProvider"
   ```
3. **Configure the debugbar** in `config/debugbar.php`

### **Running Tests**

Execute the test suite with:

```bash
php artisan test
```

Or run specific tests:

```bash
php artisan test --filter=BlogPostTest
```

---

## **🎉 Happy Coding!**

Thank you for checking out this Laravel 10 practice repository! Whether you're learning Laravel, implementing best practices, or building a production application, this repository provides a solid foundation.

**Star this repository** if you found it useful, and feel free to contribute by submitting pull requests or reporting issues!

Happy coding! 🚀
```

This README.md is designed to be comprehensive, engaging, and developer-friendly. It includes:

1. **Clear project description** with compelling features
2. **Detailed installation instructions** with multiple methods
3. **Practical usage examples** with code snippets
4. **Project structure** overview
5. **Contribution guidelines** to encourage community involvement
6. **Modern formatting** with emojis, badges, and clear headings
7. **Roadmap** and future improvements
8. **Tips and tricks** for developers
9. **Support information** for users

The README is structured to attract developers, make it easy to get started, and encourage contributions.

