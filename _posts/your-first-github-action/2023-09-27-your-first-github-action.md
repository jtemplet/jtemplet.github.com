---
title: Getting Started with CI/CD - Creating Your First GitHub Action for a Ruby on Rails Repo
date: 2023-09-27 20:58:47 +07:00
tags: [ci/cd, rails]
description: A gentle introduction to GitHub Actions
image: "/apa-itu-shell/shell_evolution.png"
---

Welcome to my very first blog post on continuous integration for Ruby on Rails repositories! In this tutorial, we'll be diving into the world of GitHub Actions, a powerful tool that can streamline your development workflow.

### Why GitHub Actions?

GitHub Actions are an essential part of modern software development, allowing you to automate tasks, run tests, and deploy your applications seamlessly. The best part? GitHub offers runners for free, as long as you stay under a certain threshold, making it accessible for hobbyists, side hustles and teams that are on a tight budget.

### Setting Up Your GitHub Action

Let's get started with creating our first job that runs RSpec for our Ruby on Rails project. Note (1): This first example will be assuming you don't need a database to run your tests.
Note (2): Additionally, the following example will be assuming that Node is required to run said tests

#### Step 1: Adding a GitHub Action File

Begin by creating a new directory named `.github/workflows` in the root of your project. Inside this directory, create a file named `rspec.yml`. This is where we'll define our GitHub Action.

#### Step 2: Defining the Action

Inside `rspec.yml`, add the following content:

```yaml
name: Run RSpec Tests

on:
  push:
    branches:
      - main
    pull_request:
        types:
        - opened
        - reopened
        - synchronize

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Set Up Ruby Environment
        uses: actions/setup-ruby@v2

      - name: Set Up Node
        uses: actions/setup-node@v3
        with:         
         node-version-file: '.nvmrc'
         registry-url: 'https://registry.npmjs.org'

      - name: Install Dependencies
        run: bundle install --jobs 4 --retry 3          

      - name: Run RSpec
        run: bundle exec rspec
```

Let's break down what each step does:
- **On Push Branches**: This is one of the trigger events to run the job, in this instance it's when you merge the PR to `main`
- **pull_request types** - Another set of trigger events to run this job, in these instances it's when a PR is open, reopened or you merge one branch into this one
- **Checkout Repository**: This step ensures that your repository is available to subsequent steps.
- **Set Up Ruby Environment**: This action sets up the specified version of Ruby for your project.
- **Set Up Node**: We need Node.js for some Rails functionalities, so we set it up here.
- **Install Dependencies**: This step installs both Ruby and Node.js dependencies.
- **Run RSpec**: Finally, we run RSpec using `bundle exec`.

#### Step 3a: Testing Locally with `act` (optional)

I initially tried to use (act)[https://github.com/nektos/act], a tool for testing GitHub Actions locally. However, I encountered a strange issue related to a missing `NODE_PATH` environment variable. I'll be sure to update this post once I've resolved that.

#### Step 3b: Testing Remotely on GitHub
Create a git commit of your recent changes and push the branch to GitHub. Create a Pull Request and you should see at the bottom of the PR (on the Conversation tab), a GHA job that is running the rspec job we created. If all the rspec tests passed you should see something like the image below.
<img src="/your-first-github-action/Screenshot.png" alt="GHA Job Result">

### Wrapping Up

Congratulations! You've just created your first GitHub Action for your Ruby on Rails project. This action will now automatically run your RSpec tests whenever you create a PR, reopen a PR or merge to the `main` branch.

Remember, GitHub Actions are highly customizable. You can tweak the workflow to suit your specific needs and even add deployment steps in the future.

I hope you found this tutorial helpful. Stay tuned for more articles on CI/CD and other exciting topics in the world of software engineering. Happy coding!

---

I hope this blog post template helps you in creating your tutorial! If you have any further questions or need additional details, feel free to ask.
