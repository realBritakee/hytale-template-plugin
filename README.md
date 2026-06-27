# Hytale Plugin Template

A minimal, ready-to-use template for creating Hytale plugins with modern build tools and automated testing.

> **✨ Builds immediately without any changes!** Clone and run `./gradlew shadowJar` to get a working plugin JAR.

## Features

✅ **Modern Build System** - Gradle with Groovy DSL  
✅ **Automated Testing** - Custom Gradle plugin for one-command server testing  
✅ **Java 25** - Latest Java features  
✅ **ShadowJar** - Automatic dependency bundling  
✅ **CI/CD Ready** - GitHub Actions workflow included  
✅ **Minimal Structure** - Only essential files, write your own code

---

## Quick Start

### Prerequisites

- **Java 25 JDK** - [Download here](https://www.oracle.com/java/technologies/downloads/)
- **IntelliJ IDEA** - [Download here](https://www.jetbrains.com/idea/download/) (Community Edition is fine)
- **Git** - [Download here](https://git-scm.com/)

### 1. Clone or Download

```bash
git clone https://github.com/realBritakee/hytale-template-plugin.git
cd hytale-plugin-template
```

**The template builds immediately without any changes!**  
You can customize it later when you're ready to develop your plugin.

### 2. Build Immediately (No Changes Needed!)

The template works out-of-the-box:

```bash
# Windows
gradlew.bat shadowJar

# Linux/Mac
./gradlew shadowJar
```

Your plugin JAR will be in: `build/libs/TemplatePlugin-1.0.0.jar`

### 3. Customize Your Plugin (Optional)

When ready to customize, edit these files:

**`settings.gradle`:**

```groovy
rootProject.name = "your-plugin-name"
```

**`gradle.properties`:**

```properties
pluginGroup=com.yourname
pluginVersion=1.0.0
pluginDescription=Your plugin description
```

**`src/main/resources/manifest.json`:**

```json
{
  "Group": "YourName",
  "Name": "YourPluginName",
  "Main": "com.yourname.yourplugin.YourPlugin"
}
```

**Rename the main plugin class:**

- Rename `src/main/java/com/example/templateplugin/TemplatePlugin.java`
- Update package name to match your `pluginGroup`

### 4. Build Your Plugin

```bash
# Windows
gradlew.bat shadowJar

# Linux/Mac
./gradlew shadowJar
```

Your plugin JAR will be in: `build/libs/YourPluginName-1.0.0.jar`

### 5. Implement Your Plugin

Write your plugin code in `src/main/java/`:

- Commands
- Event listeners
- Services
- Storage
- Utilities

See our [documentation](../Documentation/) for examples and patterns.

### 6. Test Your Plugin (Automated!)

```bash
# Windows
gradlew.bat runServer

# Linux/Mac
./gradlew runServer
```

This will:

1. Download the Hytale server (cached for future runs)
2. Build your plugin
3. Copy it to the server's mods folder
4. Start the server with interactive console

---

## Project Structure

```
TemplatePlugin/
├── .github/workflows/
│   └── build.yml                    # CI/CD workflow
├── buildSrc/
│   ├── build.gradle.kts             # Custom plugin configuration
│   └── src/main/kotlin/
│       └── RunHytalePlugin.kt       # Automated server testing
├── src/main/
│   ├── java/com/example/templateplugin/
│   │   └── TemplatePlugin.java      # Minimal main class (example)
│   └── resources/
│       └── manifest.json            # Plugin metadata
├── .gitignore                       # Git ignore rules
├── build.gradle                     # Build configuration
├── gradle.properties                # Project properties
├── settings.gradle                  # Project settings
├── LICENSE                          # MIT License
└── README.md                        # This file
```

**Note:** This is a minimal template. Create your own folder structure:

- `commands/` - For command implementations
- `listeners/` - For event listeners
- `services/` - For business logic
- `storage/` - For data persistence
- `utils/` - For utility classes
- `config/` - For configuration management

---

## Development Workflow

### Building

```bash
# Compile only
./gradlew compileJava

# Build plugin JAR
./gradlew shadowJar

# Clean and rebuild
./gradlew clean shadowJar
```

### Testing

```bash
# Run server with your plugin
./gradlew runServer

# Run unit tests
./gradlew test

# Clean test server
rm -rf run/
```

### Debugging

```bash
# Run server in debug mode
./gradlew runServer -Pdebug

# Then connect your IDE debugger to localhost:5005
```

---

## Customization

### Adding Dependencies

Edit `build.gradle`:

```groovy
dependencies {
    // Hytale API (provided by server)
    compileOnly(files("./HytaleServer.jar"))

    // Your dependencies (will be bundled)
    implementation("com.google.code.gson:gson:2.10.1")

    // Test dependencies
    testImplementation("org.junit.jupiter:junit-jupiter:5.10.0")
}
```

### Configuring Server Testing

**Run Hytale Server** - A Gradle plugin to download and run a Hytale server for development and testing purposes. The server files will be located in the `run/` directory of the project. Before starting the server it will compile (shadowJar task) and copy the plugin jar to the server's `mods/` folder.

**Usage:**

Edit `build.gradle`:

```groovy
runHytale {
    jarUrl = "url to hytale server jar"
}
```

Run the server with:

```bash
# Windows
gradlew.bat runServer

# Linux/Mac
./gradlew runServer
```

**Features:**

- ✅ Automatic server JAR download and caching
- ✅ Compiles and deploys your plugin automatically
- ✅ Starts server with interactive console
- ✅ One-command workflow: `./gradlew runServer`
- ✅ Server files in `run/` directory (gitignored)

### Implementing Your Plugin

**Recommended folder structure:**

```
src/main/java/com/yourname/yourplugin/
├── YourPlugin.java          # Main class
├── commands/                # Commands
├── listeners/               # Event listeners
├── services/                # Business logic
├── storage/                 # Data persistence
├── config/                  # Configuration
└── utils/                   # Utilities
```

**See our documentation for examples:**

- [Getting Started with Plugins](https://britakee-studios.gitbook.io/hytale-modding-documentation/plugins-java-development/07-getting-started-with-plugins)
- [Advanced Plugin Patterns](https://britakee-studios.gitbook.io/hytale-modding-documentation/plugins-java-development/12-advanced-plugin-patterns)
- [Common Plugin Features](https://britakee-studios.gitbook.io/hytale-modding-documentation/plugins-java-development/14-common-plugin-features)

---

## CI/CD

This template includes a GitHub Actions workflow that:

1. ✅ Builds your plugin on every push
2. ✅ Runs tests
3. ✅ Uploads artifacts
4. ✅ Creates releases (when you tag)

### Creating a Release

```bash
git tag v1.0.0
git push origin v1.0.0
```

GitHub Actions will automatically build and create a release with your plugin JAR.

---

## Best Practices

### ✅ DO:

- Use the Service-Storage pattern for data management
- Write unit tests for your business logic
- Use structured logging (not `System.out.println`)
- Handle errors gracefully
- Document your public API
- Version your releases semantically (1.0.0, 1.1.0, etc.)

### ❌ DON'T:

- Hardcode configuration values
- Block the main thread with heavy operations
- Ignore exceptions
- Use deprecated APIs
- Commit sensitive data (API keys, passwords)

---

## Troubleshooting

### Build Fails

```bash
# Clean and rebuild
./gradlew clean build --refresh-dependencies
```

### Server Won't Start

1. Check that `jarUrl` in `build.gradle` is correct
2. Verify Java 25 is installed: `java -version`
3. Check logs in `run/logs/`

### Plugin Not Loading

1. Verify `manifest.json` has correct `Main` class
2. Check server logs for errors
3. Ensure all dependencies are bundled in JAR

---

## Documentation

For detailed guides on plugin development, see:

- [Hytale Modding Documentation](https://github.com/yourusername/hytale-modding/tree/main/Documentation)
- [Getting Started with Plugins](../Documentation/07-getting-started-with-plugins.md)
- [Advanced Plugin Patterns](../Documentation/12-advanced-plugin-patterns.md)
- [Common Plugin Features](../Documentation/14-common-plugin-features.md)

---

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## License

This template is released under the MIT License. You are free to use it for any purpose.

---

## Support

- **Issues:** [GitHub Issues](https://github.com/yourusername/hytale-plugin-template/issues)
- **Documentation:** [Hytale Modding Docs](https://github.com/yourusername/hytale-modding)
- **Community:** Join the Hytale modding community

---

## Credits

Created by the Hytale modding community.

Based on best practices from production Hytale plugins.

---

**Happy Modding! 🎮**
