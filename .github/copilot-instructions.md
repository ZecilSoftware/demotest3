# Copilot Instructions for Advent DALL-E Project

## Project Overview
This is a **WinUI3 C# desktop application** called "Advent DALL-E" created for C# Advent 2023. The app demonstrates AI-powered image generation by:
1. Using **GPT-4** to create optimized prompts from user input
2. Using **DALL-E 3** to generate Christmas-themed images
3. Allowing users to save both generated images and prompts

## Architecture & Technologies

### Core Technologies
- **Framework**: .NET 6.0 with WinUI3 (`net6.0-windows10.0.19041.0`)
- **UI Framework**: WinUI3 with XAML
- **AI Services**: Azure OpenAI SDK (`Azure.AI.OpenAI`)
- **Target Platforms**: Windows 10/11 (x86, x64, ARM64)

### Key Dependencies
- `Azure.AI.OpenAI` (version 1.0.0-beta.11) - For GPT-4 and DALL-E 3 integration
- `Microsoft.WindowsAppSDK` - For WinUI3 functionality
- `Windows.Storage` - For file system operations

## Project Structure

### Main Files
- `MainWindow.xaml` - UI layout with Grid-based responsive design
- `MainWindow.xaml.cs` - Main application logic and AI integration
- `App.xaml.cs` - Application entry point
- `Assets/` - Contains background image and app icons
- `Package.appxmanifest` - Windows app manifest

### Key Classes & Methods
- `MainWindow` - Main window class with AI integration
  - `GeneratePrompt()` - Uses GPT-4 to enhance user prompts
  - `GenerateImage()` - Uses DALL-E 3 to create images
  - `Save_Click()` - Saves images and prompts to Pictures folder
  - UI state management methods (`WorkingState`, `FinishedState`)

## Coding Standards & Patterns

### Code Style Guidelines
- Use **PascalCase** for public methods and properties
- Use **camelCase** for private fields (prefixed with underscore: `_currentImage`)
- Use **UPPER_CASE** for constants (`OPENAI_KEY`, `SAVE_FOLER`)
- Follow async/await pattern for all API calls
- Use `using` statements for disposable resources

### UI Patterns
- Grid-based layout with responsive row definitions
- Progress indication during async operations
- State management for button enable/disable
- TeachingTip for user notifications
- Background image with overlay content

### Error Handling
- The application currently has minimal error handling
- When adding features, implement proper try-catch blocks around API calls
- Validate user input before sending to APIs
- Handle network failures gracefully

## AI Integration Details

### OpenAI Configuration
- API key stored as constant (should be moved to secure configuration)
- Uses deployment names: `"gpt-4"` and `"dall-e-3"`
- GPT-4 parameters: Temperature=1, MaxTokens=256
- DALL-E 3 parameters: Size=1792x1024, ImageCount=1

### Prompt Engineering
- System message guides GPT-4 to create Christmas-themed prompts
- User input is treated as inspiration for prompt generation
- Generated prompts are displayed temporarily during image generation

## Development Guidelines

### When Adding Features
1. **Maintain the Christmas/Holiday theme** - This is a seasonal demo app
2. **Keep UI simple and focused** - Single-window design pattern
3. **Handle async operations properly** - Update UI state during long operations
4. **Follow existing naming conventions** - Especially for XAML elements
5. **Test with various input lengths** - User prompts can vary significantly

### Common Tasks
- **Adding new UI elements**: Update MainWindow.xaml and add corresponding code-behind
- **API integration**: Follow existing async patterns with proper error handling
- **File operations**: Use Windows.Storage APIs for file system access
- **Image handling**: Use BitmapImage for WinUI3 compatibility

### Known Issues to be Aware Of
- `SAVE_FOLER` constant has a typo (should be "FOLDER")
- OpenAI API key is hardcoded (security concern)
- Limited error handling for API failures
- Uses deprecated WebClient for image download

## Build & Deployment
- Requires Windows development environment with WinUI3 SDK
- MSIX packaging enabled for Windows Store deployment
- Multi-platform targeting (x86, x64, ARM64)
- Application manifest includes necessary permissions

## API Usage Notes
- This project uses **Azure OpenAI SDK beta version** - be aware of potential breaking changes
- GPT-4 and DALL-E 3 API calls require valid OpenAI credentials
- Rate limiting and cost considerations apply to API usage
- Generated images are temporarily hosted by OpenAI (URLs expire)

## Security Considerations
- Never commit API keys to source control
- Consider using Azure Key Vault or secure configuration for production
- Validate and sanitize user input before sending to AI services
- Be mindful of content policy compliance for generated images