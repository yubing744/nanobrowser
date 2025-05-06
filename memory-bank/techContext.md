# Technical Context: Nanobrowser

## Technology Stack

### Frontend
- **TypeScript**: Primary programming language
- **React**: UI component library for the side panel and options pages
- **Tailwind CSS**: Utility-first CSS framework for styling

### Extension Architecture
- **Chrome Extension Manifest V3**: Base extension framework
- **Background Service Worker**: For persistent operations and agent coordination
- **Content Scripts**: For web page interaction and DOM manipulation
- **Side Panel API**: For UI that persists across tab navigation

### Package Management
- **pnpm**: Package manager with workspace support
- **Turbo**: Build system for monorepo management

### Build Tools
- **Vite**: Modern build tool and dev server
- **esbuild**: JavaScript bundler used within Vite
- **TypeScript**: For static typing and type safety

### Testing
- **eslint**: Static code analysis
- **prettier**: Code formatting

### AI/LLM Integration
- **LangChain Core**: Framework for working with language models
- **zod**: Schema validation for LLM outputs
- **JSON Schema**: For structuring LLM inputs and outputs

## Development Environment

### Prerequisites
- Node.js v22.12.0+
- pnpm v9.15.1+
- Chrome browser for testing

### Repository Structure
```
/chrome-extension    # Core extension code
  /src
    /background      # Background service worker
      /agent         # Multi-agent system components
      /browser       # Browser interaction utilities
      /dom           # DOM handling and manipulation
    /content         # Content scripts

/packages            # Shared libraries and utilities
  /dev-utils         # Development utilities
  /hmr               # Hot module replacement
  /i18n              # Internationalization support
  /schema-utils      # Schema validation utilities
  /shared            # Shared components and hooks
  /storage           # Storage management
  /ui                # UI components library

/pages               # Extension pages
  /content           # Content script-related pages
  /options           # Extension options page
  /side-panel        # Side panel UI
```

### Build Process
1. `pnpm install`: Install dependencies
2. `pnpm build`: Build for production
3. `pnpm dev`: Run in development mode with hot reloading
4. `pnpm zip`: Package for distribution

## Technical Constraints

### Browser Extension Limitations
- **Service Worker Lifecycle**: Background service workers have specific lifecycle limitations
- **Content Script Isolation**: Content scripts run in isolated contexts with limited access to page JavaScript
- **API Restrictions**: Limited access to certain browser APIs due to security constraints
- **Resource Limits**: Constraints on memory usage and performance

### LLM Integration Challenges
- **Token Limits**: Each LLM provider has different input/output token limits
- **Response Formatting**: Variations in how different models format structured outputs
- **Error Handling**: Must account for various API error scenarios and rate limits
- **Cost Management**: Need to optimize token usage to control user API costs

### Browser Compatibility
- **Primary**: Chrome/Chromium-based browsers (primary target)
- **Secondary**: Firefox (requires adjustments for manifest differences)
- **Limitations**: Safari does not support required extensions APIs

## Dependencies and Integrations

### LLM Providers
- **OpenAI**: GPT-4o, GPT-4o-mini models
- **Anthropic**: Claude 3.5 Haiku, Claude 3.7 Sonnet models
- **Google**: Gemini 2.0 Flash models
- **Ollama**: Local model support through Ollama API
- **Custom**: Support for OpenAI-compatible API providers

### Browser APIs
- **chrome.scripting**: For executing scripts in web page contexts
- **chrome.tabs**: For tab management and navigation
- **chrome.storage**: For persistent data storage
- **chrome.sidePanel**: For the persistent side panel UI
- **chrome.debugger**: For advanced web page interactions

### External Libraries
- **React**: v18.3.1 for UI components
- **Tailwind CSS**: For UI styling
- **LangChain Core**: For LLM chain creation and management
- **zod**: For schema validation and type safety

## Deployment Process
1. Build the extension using `pnpm build`
2. Package using `pnpm zip` to create distributable ZIP
3. For Chrome Web Store:
   - Upload the ZIP to the Chrome Web Store Developer Dashboard
   - Submit for review (can take 1-2 weeks)
4. For manual distribution:
   - Host the ZIP file on a website or GitHub releases
   - Users download and install in developer mode

## Version Control and CI/CD
- **Git**: Version control system
- **GitHub**: Repository hosting and collaboration
- **GitHub Actions**: For CI/CD workflows (not yet fully implemented)

## Technical Debt and Challenges
- **DOM Representation**: Creating accurate DOM representations for agents is complex
- **Error Recovery**: Improving recovery from failed actions
- **Model Compatibility**: Ensuring compatibility with a wide range of LLM providers
- **Performance Optimization**: Reducing token usage and improving response times
