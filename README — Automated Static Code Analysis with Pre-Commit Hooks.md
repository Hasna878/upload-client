📘 README — Automated Static Code Analysis with Pre-Commit Hooks
🔄 Pre-Commit Hook Integration

To ensure that static code analysis is automatically executed before every commit, this project integrates pre-commit hooks using the pre-commit
 framework.

The hook runs Checkstyle through Maven before Git finalizes any commit.
If Checkstyle reports violations, the commit is blocked, enforcing consistent code quality.

📁 Pre-Commit Configuration File

The hook configuration is stored at the root of the project in:

.pre-commit-config.yaml

Content of the configuration:
repos:
  - repo: local
    hooks:
      - id: maven-checkstyle
        name: Maven Checkstyle (pre-commit)
        entry: mvn -q -DskipTests checkstyle:check
        language: system
        pass_filenames: false

Explanation

repo: local → we define a custom hook using a local command.

entry → the command run before each commit:

mvn -q -DskipTests checkstyle:check
Runs the Checkstyle plugin configured inside pom.xml.

language: system → use the system’s Maven installation.

pass_filenames: false → Checkstyle does not accept file paths as arguments.

This ensures Checkstyle executes automatically on every commit.

⚙️ Installation and Setup
1. Install pre-commit (one time per machine)
pip install pre-commit

2. Install hooks inside the repository

From the project root (upload-client/):

pre-commit install


This installs a .git/hooks/pre-commit script that runs automatically before each git commit.

▶️ How It Works During a Commit

After installation, any git commit triggers:

Stash unstaged changes

Execute the configured hook

Equivalent to running:

mvn -q -DskipTests checkstyle:check


If Checkstyle passes → commit succeeds

If Checkstyle fails → commit is rejected with an error message

Example output when passing:

Maven Checkstyle (pre-commit).....................................Passed
[main ab85c9c] Configure pre-commit hook with Maven Checkstyle


This guarantees that all committed code respects the Checkstyle rules defined in:

config/checkstyle/checkstyle.xml
