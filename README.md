#  # GitHub Actions CI/CD for iOS

A hands-on iOS project created to learn and implement **CI/CD using GitHub Actions from scratch**.

The goal of this repository is to understand how a real iOS project can be automatically built, tested, and validated whenever code changes are pushed to GitHub.

This project focuses on practical CI/CD implementation along with understanding the concepts required to confidently discuss iOS CI/CD workflows in technical interviews.

---

## 🎯 Project Goals

This project is being developed incrementally to understand:

- Continuous Integration (CI)
- Continuous Delivery / Deployment (CD)
- GitHub Actions
- Workflow automation
- macOS GitHub-hosted runners
- Xcode command-line builds
- Automated unit testing
- Code quality checks
- Code coverage
- Build artifacts
- Dependency caching
- GitHub Secrets
- Pull Request validation
- Branch-based workflows
- iOS signing and deployment concepts

---

## 🏗 Current CI Pipeline

The current pipeline automatically runs whenever code is pushed to the repository.

```text
Developer pushes code
        ↓
GitHub receives push
        ↓
GitHub Actions workflow triggers
        ↓
Xcode 27 runner starts
        ↓
Repository is checked out
        ↓
Xcode environment is verified
        ↓
xcodebuild builds the project
        ↓
Build validation
        ↓
BUILD SUCCEEDED ✅
```

---

## ⚙️ Current GitHub Actions Workflow

The workflow is located at:

```text
.github/workflows/ios-ci.yml
```

The current workflow performs the following operations:

1. Triggers automatically on a Git push
2. Starts an Xcode 27 GitHub Actions runner
3. Checks out the repository
4. Verifies the runner environment
5. Checks the installed Xcode version
6. Builds the iOS application using `xcodebuild`
7. Uses the iOS Simulator SDK so physical-device signing is not required

Example build command:

```bash
xcodebuild build \
  -project GitHubActionsDemo.xcodeproj \
  -scheme GitHubActionsDemo \
  -sdk iphonesimulator \
  CODE_SIGNING_ALLOWED=NO
```

---

## ✅ Completed So Far

### CI/CD Fundamentals

- [x] Understand Continuous Integration (CI)
- [x] Understand Continuous Delivery / Deployment (CD)
- [x] Understand the role of GitHub Actions in CI/CD
- [x] Understand the basic GitHub Actions architecture

```text
Event → Workflow → Job → Runner → Steps
```

### GitHub Actions Setup

- [x] Create `.github/workflows`
- [x] Create an iOS CI workflow
- [x] Understand basic YAML syntax
- [x] Understand `uses:` vs `run:`
- [x] Configure `push` as a workflow trigger
- [x] Use `actions/checkout`
- [x] Run shell commands on the CI runner
- [x] Inspect workflow execution and logs

### Xcode & iOS CI

- [x] Understand why iOS CI requires a macOS/Xcode environment
- [x] Use `xcodebuild` from the command line
- [x] Discover Xcode targets and schemes using `xcodebuild -list`
- [x] Verify Xcode version inside CI
- [x] Build an iOS application from GitHub Actions
- [x] Build against the iOS Simulator SDK
- [x] Disable unnecessary code signing for simulator CI builds

### CI Debugging

- [x] Debug GitHub Actions workflow failures
- [x] Identify local vs CI Xcode version mismatch
- [x] Diagnose Xcode project-format compatibility issues
- [x] Inspect Xcode versions available on GitHub runners
- [x] Configure an Xcode 27 runner
- [x] Successfully build the application in CI

---

## 🚧 Remaining Implementation

The following topics will be added incrementally.

### Automated Testing

- [ ] Run unit tests using `xcodebuild test`
- [ ] Automatically fail CI when tests fail
- [ ] Understand test destinations / simulators
- [ ] Inspect test results in GitHub Actions

### Code Coverage

- [ ] Enable code coverage
- [ ] Generate coverage information during CI
- [ ] Understand how coverage can be used as a quality signal

### Code Quality

- [ ] Integrate SwiftLint
- [ ] Run lint checks automatically in CI
- [ ] Make CI detect code-quality violations

### Pull Request CI

- [ ] Trigger workflows for Pull Requests
- [ ] Validate changes before merge
- [ ] Understand CI checks in the PR workflow
- [ ] Explore branch-based workflow rules

### Artifacts

- [ ] Understand GitHub Actions artifacts
- [ ] Generate useful build/test outputs
- [ ] Upload artifacts from workflow runs
- [ ] Download and inspect generated artifacts

### Dependency Caching

- [ ] Understand why caching is useful in CI
- [ ] Configure dependency caching
- [ ] Reduce unnecessary work between workflow runs

### Secrets

- [ ] Understand GitHub Secrets
- [ ] Store sensitive configuration securely
- [ ] Access secrets from GitHub Actions
- [ ] Understand why credentials should never be committed to source control

### Workflow Improvements

- [ ] Reduce unnecessary workflow steps
- [ ] Improve workflow readability
- [ ] Understand environment variables
- [ ] Understand job dependencies
- [ ] Explore multiple jobs
- [ ] Understand failure handling
- [ ] Build a more production-like CI pipeline

---

## 📦 Planned Final CI Flow

As the project progresses, the workflow will evolve toward something similar to:

```text
Code Push / Pull Request
           ↓
    GitHub Actions
           ↓
      Checkout Code
           ↓
   Configure Environment
           ↓
        Build App
           ↓
      Run Unit Tests
           ↓
     Code Coverage
           ↓
       SwiftLint
           ↓
   Generate Artifacts
           ↓
      CI Validation
           ↓
     Ready for Merge
```

---

## 🚀 CD / TestFlight

A complete production iOS CD pipeline can extend the workflow further:

```text
CI Validation
      ↓
Archive Application
      ↓
Code Signing
      ↓
Export IPA
      ↓
App Store Connect
      ↓
TestFlight
```

Actual App Store / TestFlight deployment requires Apple Developer and App Store Connect credentials.

This repository currently focuses on implementing the parts of the CI/CD pipeline that can be practiced without an Apple Developer account. Signing, provisioning, App Store Connect authentication, and TestFlight deployment will be studied conceptually unless the required developer infrastructure becomes available.

---

## 🧠 Real-World Issue Encountered

During the initial CI setup, the project was created locally using **Xcode 27**, while the initial GitHub Actions macOS runner selected **Xcode 26.6**.

The CI build failed because the older Xcode version could not read the newer project file format.

The issue was diagnosed by:

- Checking the local Xcode version
- Checking the CI Xcode version
- Inspecting the project's `objectVersion`
- Inspecting installed Xcode versions on the runner
- Identifying the environment compatibility mismatch

The workflow was then configured to use an Xcode 27-compatible runner.

This demonstrates an important CI principle:

> A CI environment should be compatible with the development environment and project configuration.

---

## 🛠 Technologies

- Swift
- iOS
- Xcode
- XCTest
- Git
- GitHub
- GitHub Actions
- YAML
- `xcodebuild`
- macOS CI runners

---

## 📚 Learning Status

Current progress:

```text
CI/CD Fundamentals       ✅
GitHub Actions Basics    ✅
Workflow Creation        ✅
GitHub Push Trigger      ✅
macOS / Xcode Runner     ✅
Automated iOS Build      ✅
CI Debugging             ✅

Unit Testing             ⏳ Next
Code Coverage            ⏳
SwiftLint                ⏳
Pull Request CI          ⏳
Artifacts                ⏳
Caching                  ⏳
Secrets                  ⏳
Advanced Workflows       ⏳
CD / TestFlight Concepts ⏳
```

---

## 📌 Purpose of This Repository

This repository is primarily a **hands-on CI/CD learning project**.

Instead of only studying CI/CD theoretically, each concept is being implemented incrementally in a real iOS project, including debugging actual CI environment and build issues.

The final goal is to understand not only **how to configure a CI/CD pipeline**, but also **why each part of the pipeline exists and how it fits into a real iOS development workflow**.

