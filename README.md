
## <img src="https://app.amlwatcher.com/img/single-logo.4cbf1b85.svg" alt="AML Watcher Logo" width="200"> 


This README provides detailed documentation for the AML Watcher MCP server configuration, focusing on the environment arguments used in the `claude_desktop_config.json` file. It explains each argument, how to set or modify its values, and how to add new arguments if needed.

## Overview

The MCP server is configured to run a Docker container for AML (Anti-Money Laundering) screening. The configuration is defined in the `claude_desktop_config.json` file, which specifies the Docker command, arguments, and environment variables. The environment variables (`env`) control the behavior of the AML screening process, such as search parameters, filtering options, and monitoring settings.

## ⚙️ Configuration
### 📝 Sign Up
  
  - If you **already have an account**, Visit the [**AML Watcher Developer Portal**](https://app.amlwatcher.com/login).
  - If you **don’t have an account**, please [**click here to contact us**](https://amlwatcher.com/contact-us/).


## 🔑 How to Generate Your API Key
- Navigate to the [**AML Watcher Developer Portal**](https://app.amlwatcher.com/login).
- Click on **“API Key”** and copy it.


## 🖥️ Usage with Claude Desktop
Add this to your `claude_desktop_config.json`:
### 🐳 Docker
```json
{
  "mcpServers": {
    "aml": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e", "API_KEY",
        "-e", "PER_PAGE",
        "-e", "MATCH_SCORE",
        "-e", "CATEGORIES",
        "-e", "ALIAS_SEARCH",
        "-e", "RCA_SEARCH",
        "-e", "COUNTRIES",
        "aml_watcher_mcp"
      ],
      "env": {
        "API_KEY": "api_key",
        "PER_PAGE": "5"
      }
    }
  }
}
```
- After this integration, the user has to provide a username.

## 🌐 Environment Arguments

Below is a detailed explanation of each environment argument specified in the `env` section of the `claude_desktop_config.json`. Each argument includes its purpose, type, default value, constraints, and instructions for setting or modifying its value.

| Argument       | Type    | Required | Default Value | Description                                                                 |
|----------------|---------|----------|----------------|----------------------------------------------------------------------------|
| `API_KEY`      | String  | Yes      | N/A            | The API key for authentication.                                            |
| `COUNTRIES`    | Array   | No       | N/A            | Array of countries to filter reports. **Note**: ISO 3166-1 alpha-2 country codes are supported. **Example**: `[\"CA\", \"IN\"]`. <a href="https://doc.amlwatcher.com/docs/Technical-appendicies/supported-countries/" target="_blank" rel="noopener noreferrer">See supported countries</a> |
| `PER_PAGE`     | Integer | No       | 5              | The maximum number of results to return.                                   |
| `MATCH_SCORE`  | Integer | No       | 70             | Match accuracy level (0–100). Not applicable for "Adverse Media" category. |
| `CATEGORIES`   | Array   | Yes      | N/A            | Filters reports by categories (e.g., `[\"SIP\", \"PEP Level 1\"]`). <a href="https://doc.amlwatcher.com/docs/Technical-appendicies/categories/" target="_blank" rel="noopener noreferrer" >See available categories</a> |
| `RCA_SEARCH`   | Boolean | No       | True           | Whether to search within Relatives and Close Associates (RCA).             |
| `ALIAS_SEARCH` | Boolean | No       | True           | Whether to search within aliases.                                          |

You can define custom parameters inside the `env` section of your configuration file. These parameters are passed to the Docker container as environment variables.

### 🛠️ How to Add Environment Variables
Each variable listed in the `args` array using `-e` must have a matching key in the `env` section.
If a variable is not defined in the `env` block, the system may use a **default value**.

For example, if your `args` list contains:

```json
"args": [
  "-e", "PER_PAGE",
  "-e", "MATCH_SCORE"
]
```

Then your env should include:
```json
"env": {
  "PER_PAGE": "5",
  "MATCH_SCORE": "90"
}
```

💡Tip : If you want to manually set the value of a variable, make sure to use the exact same name as listed in the args section. Variable names must match exactly, otherwise the Docker container won't receive the value correctly.