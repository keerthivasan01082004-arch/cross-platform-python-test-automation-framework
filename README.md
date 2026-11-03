# Cross-Platform Python Test Automation Framework

A modular Python framework for building maintainable automated tests across web applications, mobile apps, desktop applications, and APIs.

The framework combines the Page Object Model, reusable driver and action helpers, API abstractions, pytest fixtures, remote-browser integrations, and reporting utilities in one extensible test-automation foundation.

## What it supports

- **Web UI testing** with Selenium and pytest.
- **Mobile testing** with Appium for Android and iOS workflows.
- **Windows desktop testing** with Appium and WinAppDriver.
- **API testing** through reusable endpoint definitions and an API player/interface layer.
- **Page Object Model** design for maintainable UI test suites.
- **Local and remote execution** across browsers and operating systems.
- **Parallel test execution** with pytest-xdist.
- **Screenshots, logs, HTML summaries, and external reporting integrations.**

## Framework architecture

```text
┌───────────────────────────────┐
│            Tests              │
│  UI · Mobile · Windows · API  │
└───────────────┬───────────────┘
                ▼
┌───────────────────────────────┐
│          Page Objects          │
│     PageFactory · components   │
└───────────────┬───────────────┘
                ▼
┌───────────────────────────────┐
│       Core Automation          │
│ drivers · actions · fixtures  │
└───────┬───────────────┬───────┘
        ▼               ▼
┌───────────────┐ ┌───────────────┐
│ API Endpoints  │ │ Integrations  │
│ player/client  │ │ cloud/report  │
└───────────────┘ └───────────────┘
```

## Core components

### Page Object Model

The `page_objects/` package contains reusable page abstractions and examples for common workflows. Encapsulating locators and interactions keeps test cases focused on behavior instead of implementation details.

### Driver and action helpers

The `core_helpers/` package provides driver creation, browser options, mobile helpers, screenshots, logging, remote execution support, and reusable Selenium actions.

### API automation

The `endpoints/` package provides base API abstractions, endpoint definitions, an API interface, and an API player for testing service contracts alongside UI workflows.

### Integrations and reporting

The `integrations/` package contains integrations for remote browser providers, test reporting systems, Slack notifications, email reporting, and other execution services.

## Repository structure

```text
cross-platform-python-test-automation-framework/
├── conf/                 # Browser, device, environment, and test configuration
├── core_helpers/         # Drivers, actions, logging, screenshots, and fixtures
├── endpoints/            # API interfaces, players, and endpoint definitions
├── integrations/         # Remote browsers and reporting integrations
├── page_objects/         # PageFactory and reusable page object examples
├── tests/                # Web, mobile, desktop, accessibility, and API tests
├── utils/                # Logging, comparison, snapshots, reports, and helpers
├── conftest.py           # Shared pytest configuration and fixtures
├── pytest.ini            # Pytest settings and custom options
├── requirements.txt      # Python dependencies
├── tox.ini               # Tox automation configuration
└── entrypoint.sh         # Container or environment entry point
```

## Installation

```bash
git clone https://github.com/keerthivasan01082004-arch/cross-platform-python-test-automation-framework.git
cd cross-platform-python-test-automation-framework
python -m venv .venv
source .venv/bin/activate       # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

For environment-specific settings, review the provided configuration templates such as `env_conf`, `env_remote`, and `env_ssh_conf`. Keep credentials and private service tokens outside version control.

## Running tests

Run the complete local suite:

```bash
python -m pytest
```

Run a specific test file:

```bash
python -m pytest tests/test_example_form.py
```

Run tests against a selected application URL:

```bash
python -m pytest --app_url http://localhost:3000
```

Run tests in parallel:

```bash
python -m pytest -n 3 -v
```

Run tests against a selected browser:

```bash
python -m pytest tests/test_example_form.py --browser Chrome
```

Run remote-browser tests when the relevant provider configuration is available:

```bash
python -m pytest -s --remote_flag Y --app_url https://example.com
```

Use `python -m pytest -h` to see the complete list of framework-specific options, including mobile, Windows, reporting, interactive, and remote execution flags.

## Writing a page object

A typical page object should encapsulate locators and user actions while exposing business-readable methods to the test layer:

```python
from page_objects.PageFactory import PageFactory


class ExamplePage(PageFactory):
    def open_example(self):
        self.driver.get("https://example.com")

    def page_title(self):
        return self.driver.title
```

Keep test cases focused on scenarios and assertions. Put selectors, synchronization, and interaction details in page objects or shared helpers.

## Test categories

Example suites cover:

- Form and table workflows
- Accessibility checks
- API endpoint testing
- Mobile application flows
- Windows desktop workflows
- Snapshot and visual comparisons
- Successive form creation
- Remote and cross-browser execution

## CI and external services

The framework can be connected to remote browser platforms and reporting services when credentials and provider configuration are available. Configure these integrations through environment variables and the files under `conf/` and `integrations/` rather than committing secrets.

## Design principles

- Prefer reusable abstractions over duplicated test steps.
- Keep test data and environment configuration separate from test logic.
- Make local execution possible before adding remote execution.
- Capture logs and screenshots when failures occur.
- Use stable page-object methods instead of brittle locator usage in tests.
- Keep API and UI automation in the same test strategy when validating end-to-end behavior.
