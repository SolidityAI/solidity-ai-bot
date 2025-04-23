# Solidity AI - VS Code Extension

**Version:** v1.4.2  
**Contact:** [contact@solidity.bot](mailto:contact@solidity.bot)

*Credits to [Solidity Analyzer](https://solidity-analyzer.iard.solutions) for the original code*

Welcome to the **Solidity AI** Visual Studio Code extension—a powerful tool designed to identify vulnerabilities and optimize your Solidity smart contracts with comprehensive security analysis and linting.

![Solidity AI Example](images/solidity-analyzer-example.png)

## 🚀 Features

- **Security Analysis**: Automatically detect vulnerabilities and security flaws in your Solidity smart contracts.
- **Code Linting**: Identify stylistic inconsistencies, best practices, and gas optimization opportunities.
- **Detailed Reports**: Generate in-depth reports categorizing vulnerabilities by severity and confidence.
- **In-Editor Highlighting**: Clearly visualize security and linting issues with colored inline highlights directly within your code.
- **Easy Navigation**: Quickly jump to identified problem areas from the detailed report panel.
- **Configurable Filtering**: Refine analysis results based on severity, confidence, and issue type.
- **Status Bar Integration**: Monitor real-time analysis status and access results with one click from the VS Code status bar.

## 📋 Requirements

- **Visual Studio Code:** Version 1.96.0 or higher.
- **Node.js:** Version 14.0 or higher (required for linting features).

## 📥 Installation

Install via the Visual Studio Code Marketplace:

1. Launch **Visual Studio Code**.
2. Open the **Extensions** pane (`Ctrl + Shift + X`).
3. Search for **"Solidity AI"**.
4. Click **Install**.

## 🛠 Usage

To analyze Solidity code with Solidity AI:

1. Open a Solidity (`.sol`) file or workspace containing Solidity files.
2. Open the **Command Palette** (`Ctrl + Shift + P`) and type **"Solidity AI"**.
3. Choose an analysis mode:
   - **Solidity AI: Analyze Current File** – Analyze the active Solidity file.
   - **Solidity AI: Analyze All Solidity Files** – Analyze all Solidity files in your workspace.
4. Review highlighted issues directly in your code and detailed reports in the analysis panel.

### ⚡️ Quick Access

- Click the **shield icon** in the VS Code status bar to instantly analyze the current file.
- Configure automatic analysis on file save in extension settings.

### 💡 Example Workflow

## Before
```solidity
// Example vulnerable Solidity contract
contract Vulnerable {
    function withdraw(uint amount) public {
        require(amount > 0);
        msg.sender.transfer(amount); // Potential reentrancy vulnerability
    }
}
```

## After
```solidity
pragma solidity ^0.8.0;

contract Safe { // Updated to prevent reentrancy attacks
    mapping(address => uint) public balances; // Balance mapping

    function withdraw(uint _amount) public {
        require(balances[msg.sender] >= _amount, "Insufficient balance"); // Add revert reason
        balances[msg.sender] -= _amount; // State update before external call
        (bool sent,) = msg.sender.call{value: _amount}(""); // External call with no data
        require(sent, "Transfer failed"); // Provide revert reason
    }
}
```