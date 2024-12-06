## Project Structure

The project follows a multi-module Maven architecture, organized as follows:

```plaintext
blog/
│
├── config-server/                              # Centralized configuration server
│   └── src/
│       └── main/
│           ├── java/io/github/mouhamethfadal/blog/config/
│           │   └── ConfigServerApplication.java
│           └── resources/
│               └── application.yml
│
├── blog-backend/                               # Main application module
│   └── src/
│       ├── main/
│       │   ├── java/io/github/mouhamethfadal/blog/
│       │   │   ├── BlogApplication.java
│       │   │   │
│       │   │   ├── config/                    # Application configurations
│       │   │   │   ├── MongoConfig.java
│       │   │   │   ├── SecurityConfig.java
│       │   │   │   ├── SwaggerConfig.java
│       │   │   │   └── FileStorageConfig.java
│       │   │   │
│       │   │   ├── controller/                # API endpoints
│       │   │   │   ├── admin/
│       │   │   │   │   ├── AdminPostController.java
│       │   │   │   │   └── AdminImageController.java
│       │   │   │   ├── public/
│       │   │   │   │   ├── PostController.java
│       │   │   │   │   └── ImageController.java
│       │   │   │   └── AuthController.java
│       │   │   │
│       │   │   ├── domain/                    # Core business entities
│       │   │   │   ├── Post.java
│       │   │   │   ├── Image.java
│       │   │   │   └── Admin.java
│       │   │   │
│       │   │   ├── dto/                       # Data transfer objects
│       │   │   │   ├── mapper/
│       │   │   │   │   ├── PostMapper.java
│       │   │   │   │   └── ImageMapper.java
│       │   │   │   ├── request/
│       │   │   │   │   ├── PostRequest.java
│       │   │   │   │   ├── ImageRequest.java
│       │   │   │   │   └── LoginRequest.java
│       │   │   │   └── response/
│       │   │   │       ├── PostResponse.java
│       │   │   │       ├── ImageResponse.java
│       │   │   │       └── JwtResponse.java
│       │   │   │
│       │   │   ├── exception/                 # Error handling
│       │   │   │   ├── GlobalExceptionHandler.java
│       │   │   │   ├── ResourceNotFoundException.java
│       │   │   │   └── StorageException.java
│       │   │   │
│       │   │   ├── repository/                # Data access layer
│       │   │   │   ├── PostRepository.java
│       │   │   │   └── ImageRepository.java
│       │   │   │
│       │   │   ├── security/                  # Security components
│       │   │   │   ├── JwtTokenProvider.java
│       │   │   │   ├── JwtAuthenticationFilter.java
│       │   │   │   └── AdminDetailsService.java
│       │   │   │
│       │   │   ├── service/                   # Business logic
│       │   │   │   ├── impl/
│       │   │   │   │   ├── PostServiceImpl.java
│       │   │   │   │   └── ImageServiceImpl.java
│       │   │   │   ├── PostService.java
│       │   │   │   └── ImageService.java
│       │   │   │
│       │   │   └── util/                      # Utility classes
│       │   │       ├── FileUtils.java
│       │   │       └── MarkdownUtils.java
│       │   │
│       │   └── resources/
│       │       ├── bootstrap.yml
│       │       └── application.yml
│       │
│       └── test/
│           └── java/io/github/mouhamethfadal/blog/
│               ├── controller/
│               ├── service/
│               └── repository/
│
├── blog-config/                                # Configuration repository
│   ├── blog-backend/
│   │   ├── application.yml
│   │   ├── blog-backend-development.yml
│   │   ├── blog-backend-staging.yml
│   │   └── blog-backend-production.yml
│   └── README.md
│
└── pom.xml                                     # Parent POM file
````

## Module Descriptions

### Config Server

The configuration server module serves as the centralized configuration management system for the entire application. It acts as a dedicated Spring Cloud Config Server that interfaces with the blog-config repository to provide dynamic property management across different environments. This module ensures consistent and secure handling of configuration properties while enabling runtime updates without application restarts.

### Blog Backend

The main application module implements the blog's core functionality through a carefully structured layered architecture that ensures clear separation of concerns. The architecture comprises several key layers:

The API Layer contains controllers that handle all incoming HTTP requests and define the application's endpoints, providing a clean interface for both public and administrative operations.

The Service Layer houses the core business logic and domain operations, ensuring that business rules are properly enforced and domain operations are executed consistently.

The Data Layer utilizes MongoDB repositories to manage data persistence, providing efficient storage and retrieval of blog posts, images, and user data.

The Security Layer implements JWT-based authentication and authorization, ensuring that administrative operations are properly secured while maintaining public access to blog content.

### Configuration Repository

The configuration repository functions as a dedicated Git repository that maintains environment-specific configuration files for the application. This separation provides several important benefits:

Environment-specific property management enables tailored configurations for development, staging, and production environments, ensuring appropriate settings for each context.

Secure handling of sensitive data allows for proper management of credentials and security configurations while maintaining separation from application code.

Version-controlled configuration changes provide an audit trail and enable rollback capabilities for configuration modifications, enhancing system reliability.

Dynamic configuration updates allow for runtime property changes without requiring application restarts, improving system flexibility and maintainability.