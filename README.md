# OVEC Plugin System POC

## Overview

This repository contains a **Proof of Concept (POC)** for the plugin system of the OVEC (Open Verbal Chatbot) project. OVEC is a modular framework focused on providing customizable, privacy-conscious verbal interactions with AI models. This POC demonstrates the backend framework for managing plugins, implementing hooks, and providing a basic Command Line Interface (CLI) for plugin control.

The goal of this POC is to explore the structure, technologies, and challenges of implementing a flexible, extensible plugin system. While this POC is functional, it is not intended to be a complete implementation.

---

## Features

### Implemented Features:
- **Plugin Scanning**: Automatically detects plugins in the `node_modules` directory and retrieves their configuration.
- **Plugin Management**:
  - Install and uninstall plugins via the CLI.
  - Enable and disable plugins.
- **Hooks**:
  - One hook is implemented (`init`).
  - Plugins can attach actions to hooks, which modify or interact with the application's context.
- **Action Execution**: Executes plugin actions associated with hooks in priority order.
- **Command Line Interface (CLI)**:
  - View installed, enabled, or uninstalled plugins.
  - Manage plugin lifecycle: install, uninstall, enable, and disable plugins.
  - Trigger hook execution.

---

## Commands

The POC provides a CLI application named `ovec` for interacting with the plugin system. Below are the available commands:

### General
- **`ovec --help`**: Displays help information for all commands.
- **`ovec --version`**: Shows the current version of the CLI.

### Plugin Management
- **`ovec list`**: Lists all plugins.
  - Options:
    - `-e, --enabled`: Show only enabled plugins.
    - `-i, --installed`: Show only installed plugins.
    - `-d, --disabled`: Show only disabled plugins.
    - `-u, --uninstalled`: Show only uninstalled plugins.
- **`ovec install <plugin>`**: Installs a plugin by its NPM name.
- **`ovec uninstall <plugin>`**: Uninstalls a plugin by its name.
- **`ovec enable <plugin>`**: Enables a plugin, allowing it to attach actions to hooks.
- **`ovec disable <plugin>`**: Disables a plugin, removing its actions from hooks.

### Hooks
- **`ovec fire`**: Executes all actions attached to the `init` hook.

---

## How It Works

### 1. Plugin Scanning
The POC scans the `node_modules` directory for OVEC plugins. Each plugin is expected to have a configuration file, which defines its name, version, and whether it is enabled. This configuration is used for further processing.

### 2. Hooks and Actions
- **Hooks** are events in the application that plugins can attach functions (actions) to.
- **Actions** are functions that accept the app's context, potentially modify it, and return it.

### 3. Dependency Injection (DI)
This POC uses a DI container (`inversify`) to manage dependencies, making it easy to inject and test services like the PluginManager and HookService.
