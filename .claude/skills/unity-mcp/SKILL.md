# unity-mcp Development Patterns

> Auto-generated skill from repository analysis

## Overview

The unity-mcp repository is a Unity package that provides Model Context Protocol (MCP) integration for Unity Editor. It consists of a C# Unity package (`MCPForUnity`) that communicates with a Python server backend to enable AI-powered development tools within Unity. The codebase follows a dual-language architecture with Unity C# components for the editor interface and Python services for MCP protocol handling.

## Coding Conventions

### File Naming
- **C# Unity Files**: Use PascalCase for class files
  ```
  MCPForUnity/Editor/Clients/Configurators/ClaudeConfigurator.cs
  MCPForUnity/Editor/Tools/UnityMCPTool.cs
  ```

### Project Structure
- Unity package files in `MCPForUnity/`
- Python server code in `Server/src/`
- Tests split between Unity (`TestProjects/`) and Python (`Server/tests/`)
- Documentation in multiple languages (`docs/i18n/`)

### Commit Conventions
- Use conventional commit format: `type: description`
- Common types: `chore`, `fix`, `feat`
- Keep messages around 62 characters
- Examples:
  ```
  chore: bump version to 0.2.1-beta.15
  fix: resolve client configuration issue
  ```

## Workflows

### Beta Version Release
**Trigger:** When preparing a new beta release
**Command:** `/release-beta`

1. Update version in `MCPForUnity/package.json`
   ```json
   {
     "version": "0.2.1-beta.16"
   }
   ```
2. Create pull request for beta version bump
3. Review and merge pull request
4. Repeat for next beta increment (typically 15 releases per month)

### Client Configurator Addition
**Trigger:** When integrating a new AI client service
**Command:** `/add-client`

1. Create new configurator C# file in `MCPForUnity/Editor/Clients/Configurators/`
   ```csharp
   // NewServiceConfigurator.cs
   public class NewServiceConfigurator : IClientConfigurator
   {
       // Implementation
   }
   ```
2. Generate corresponding `.cs.meta` file for Unity
3. Update `README.md` with new client documentation
4. Update `docs/i18n/README-zh.md` for Chinese documentation
5. Test configurator integration

### Major Feature Development
**Trigger:** When implementing substantial new functionality
**Command:** `/add-feature`

1. Implement feature in `MCPForUnity/Editor/Tools/`
   ```csharp
   public class NewFeatureTool : EditorWindow
   {
       // Unity Editor tool implementation
   }
   ```
2. Create corresponding Python service in `Server/src/services/tools/`
   ```python
   class NewFeatureService:
       def handle_request(self, request):
           # MCP service implementation
   ```
3. Add integration tests in `Server/tests/integration/`
4. Add Unity edit-mode tests in `TestProjects/UnityMCPTests/Assets/Tests/EditMode/`
5. Update skill documentation in `.claude/skills/` and `unity-mcp-skill/`
6. Update README.md and other documentation
7. Update `Server/uv.lock` dependencies if needed

### Version Sync and Release
**Trigger:** When releasing a stable version from main to beta
**Command:** `/sync-release`

1. Bump version numbers in multiple files:
   - `MCPForUnity/package.json`
   - `Server/pyproject.toml`
   - `manifest.json`
2. Sync changes from main branch into beta
3. Create release pull request
4. Merge and set next beta version number

### Bug Fix with Tests
**Trigger:** When fixing identified bugs or issues
**Command:** `/fix-bug`

1. Identify and fix implementation in relevant files:
   - C# files: `MCPForUnity/Editor/**/*.cs`
   - Python files: `Server/src/**/*.py`
2. Add or update tests to verify fix:
   - Unity tests: `TestProjects/UnityMCPTests/Assets/Tests/**/*.cs`
   - Python tests: `Server/tests/**/*.py`
3. Run integration tests to ensure no regressions
4. Create pull request with descriptive commit message

## Testing Patterns

### Unity Testing
- Edit-mode tests in `TestProjects/UnityMCPTests/Assets/Tests/EditMode/`
- Use Unity Test Framework for C# component testing
- Test files follow pattern: `*Test.cs`

### Python Testing
- Integration tests in `Server/tests/integration/`
- Test files follow pattern: `test_*.py`
- Focus on MCP protocol compliance and service functionality

### Test Coverage
- Each new feature should include both Unity and Python tests
- Integration tests verify end-to-end functionality
- Unit tests cover individual component behavior

## Commands

| Command | Purpose |
|---------|---------|
| `/release-beta` | Create new beta version release |
| `/add-client` | Add new AI client configurator |
| `/add-feature` | Implement major new functionality |
| `/sync-release` | Sync main branch to beta with version bump |
| `/fix-bug` | Fix bugs with corresponding tests |