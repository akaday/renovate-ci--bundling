# Renovate CI Bundling

This repository is set up to automate dependency updates using Renovate and a CI pipeline.

## Getting Started

### Prerequisites

- Git
- GitHub Account
- Renovate GitHub App

### Installation

1. **Clone the repository**:
    ```bash
    git clone https://github.com/akaday/renovate-ci--bundling.git
    cd renovate-ci--bundling
    ```

2. **Install Renovate**:
    - Go to the Renovate GitHub App and install it on your repository.

### Configuration

- **Renovate Configuration**:
    The `renovate.json` file contains the configuration for Renovate. It is set up to group all dependencies into a single pull request.

    ```json
    {
      "extends": [
        "config:base"
      ],
      "packageRules": [
        {
          "matchPackagePatterns": ["*"],
          "groupName": "all dependencies",
          "groupSlug": "all-dependencies"
        }
      ],
      "gitAuthor": "Your Name <your-email@example.com>",
      "platform": "github",
      "repositories": [
        "your-username/renovate-ci-bundling"
      ]
    }
    ```

- **CI Pipeline**:
    The `.github/workflows/renovate.yml` file sets up a GitHub Actions workflow to run Renovate.

    ```yaml
    name: Renovate
    on:
      schedule:
        - cron: "0 0 * * *"
      workflow_dispatch:
    jobs:
      renovate:
        runs-on: ubuntu-latest
        steps:
          - name: Checkout code
            uses: actions/checkout@v2
          - name: Run Renovate
            uses: renovatebot/github-action@v32.0.0
            with:
              token: ${{ secrets.GITHUB_TOKEN }}
    ```

### Usage

- **Trigger Renovate**:
    You can manually trigger the Renovate workflow or wait for the scheduled run. Renovate will scan your repository for dependencies and create pull requests to update them.

### Contributing

Feel free to open issues or submit pull requests if you have any improvements or suggestions.

### License

This project is licensed under the MIT License - see the LICENSE file for details.

