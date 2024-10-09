# Go Azure Function

This repository contains a sample Azure Function implemented in Go. The function includes a health check endpoint and a customizable greeting endpoint.

## Prerequisites

- [Go](https://golang.org/dl/) 1.23.2 or later
- [Visual Studio Code](https://code.visualstudio.com/)
- [Azure Functions Core Tools](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local)
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)

## Project Structure

- `handler.go`: Contains the main logic for the Azure Function.
- `go.mod`: Go module file.
- `.vscode/`: Contains VS Code configuration files for debugging and tasks.
- `HttpExample/function.json`: Configuration for the HTTP trigger.

## Setup

1. Clone the repository:
    ```sh
    git clone https://github.com/yourusername/go-azure-function.git
    cd go-azure-function
    ```

2. Install dependencies:
    ```sh
    go mod tidy
    ```

3. Run the function locally:
    ```sh
    func start
    ```

## Endpoints

### Health Check

- **URL**: `/health`
- **Method**: `GET`
- **Response**: `Healthy`

### Hello

- **URL**: `/HttpExample/{name}`
- **Method**: `GET`, `POST`
- **Response**: 
  - If `name` is provided: `Hello, {name}. This HTTP triggered function executed successfully.`
  - If `name` is not provided: `This HTTP triggered function executed successfully. Pass a name in the query string for a personalized response.`

## Configuration

### VS Code Extensions

Recommended extensions in `.vscode/extensions.json`:
```json
{
  "recommendations": [
    "ms-azuretools.vscode-azurefunctions"
  ]
}
```

### VS Code Settings

Settings in `.vscode/settings.json`:
```json
{
    "azureFunctions.deploySubpath": ".",
    "azureFunctions.projectLanguage": "Custom",
    "azureFunctions.projectRuntime": "~4",
    "debug.internalConsoleOptions": "neverOpen"
}
```

### Launch Configuration

Launch configuration in `.vscode/launch.json`:
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch Package",
            "type": "go",
            "request": "launch",
            "mode": "auto",
            "program": "${fileDirname}"
        }
    ]
}
```

### Tasks Configuration

Tasks configuration in `.vscode/tasks.json`:
```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "func",
            "label": "func: host start",
            "command": "host start",
            "problemMatcher": "$func-watch",
            "isBackground": true
        }
    ]
}
```

## Deployment

To deploy the function to Azure, use the following command:
```sh
az functionapp deployment source config-zip --src <zip-file-path> --name <function-app-name> --resource-group <resource-group-name>
```

## License

This project is licensed under the MIT License.