
# 🛠️ Atlassian Agent Repository

This repository contains the `atlassian-agent.jar` file along with related configurations, intended for internal use within Focela Technologies. The agent file is essential for managing licensing requirements in Atlassian products such as Jira, Confluence, and Bamboo.

## 📂 Contents

- **☕ atlassian-agent.jar**: The core agent for license management in Atlassian products.
- **📑 LICENSE**: Terms and conditions for the use of this software, restricted for internal purposes only within Focela Technologies.

## 🚀 Usage

> **⚠️ Note**: This repository is intended for internal use only. Redistribution, sublicensing, or external sharing of this software is strictly prohibited without prior written permission from Focela Technologies.

### Step-by-Step Guide

1. **📥 Download the agent**: Use the following command to download the `atlassian-agent.jar` file:

   ```bash
   curl -L https://github.com/focela/atlassian/releases/download/v1.3.3/atlassian-agent.jar
   ```

2. **🔧 Integrate with Atlassian Products**:
   - Copy `atlassian-agent.jar` to the necessary location within your Atlassian product's installation directory.
   - Configure the Java options in your Atlassian product's startup configuration to reference this agent.

3. **⚙️ Set Java Options**:
   - In your `JAVA_OPTS` or relevant environment variable for the Atlassian product, add the following:
     ```bash
     -javaagent:/path/to/atlassian-agent.jar
     ```
   - Replace `/path/to/atlassian-agent.jar` with the actual path to the jar file.

## 📑 License

This project is licensed under the following terms:

- **© 2024 Focela Technologies**.
- Permission is granted solely for internal use by employees of Focela Technologies.
- Redistribution, sublicensing, or sharing is prohibited without explicit permission.
- Any modifications or derivative works remain the property of Focela Technologies.

For the full license text, please refer to the [LICENSE](LICENSE) file.

## ⚖️ Disclaimer

This software is provided "as is," without warranty of any kind, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, and non-infringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability arising from the use or handling of this software.

---

> Made with ❤️ by Focela Technologies
