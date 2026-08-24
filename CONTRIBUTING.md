# Contributing

Thanks for wanting to contribute! This guide walks you through submitting a change, even if you've never done it before.

## How to contribute

1. **Fork this repository**
   Click the "Fork" button at the top right of this page. This creates your own copy of the repo under your GitHub account.

2. **Clone your fork to your computer**
   ```bash
   git clone https://github.com/YOUR-USERNAME/website.git
   cd website
   ```

3. **Create a new branch for your change**
   Don't work directly on `main` — give your branch a short, descriptive name.
   ```bash
   git checkout -b fix-typo-in-events-page
   ```

4. **Make your changes**
   Edit the index.html files as needed. Keep changes focused — one topic per pull request is easier to review.

5. **Commit and push your changes**
   ```bash
   git add .
   git commit -m "Fix typo on events page"
   git push origin fix-typo-in-events-page
   ```

6. **Open a pull request**
   Go to your fork on GitHub — you'll see a prompt to "Compare & pull request." Click it, fill in a short description of what you changed and why, and submit.

7. **Wait for review**
   The pull request will be reviewed by the i-UG Development Director before merging. You might be asked to make small changes — that's normal, just push additional commits to the same branch and the PR updates automatically.

## Guidelines

- Keep the site's existing style and structure where possible.
- Test your changes locally by opening the HTML file(s) in a browser before submitting.
- If you're fixing a bug or adding content, briefly explain what and why in your PR description.
- Be respectful in comments and discussion — this is a community project.

## Questions?

Open an [issue](../../issues) if you're not sure how to proceed or want to discuss an idea before building it.
