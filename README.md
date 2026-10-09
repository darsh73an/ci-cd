# Simple CI/CD with GitHub Actions

A tiny calculator. The code is not the point: the two files in
`.github/workflows/` are.

```
app/calculator.js         the code
app/index.html            a web page that uses it
test/calculator.test.js   the tests
.github/workflows/ci.yml  run tests on every push / PR
.github/workflows/cd.yml  test, then publish the site
```

## Try it locally

Needs Node 20+.

```bash
npm test
```

## Do it on GitHub (10 minutes)

1. Create an empty repo on github.com, then:
   ```bash
   git init
   git add .
   git commit -m "first commit"
   git branch -M main
   git remote add origin https://github.com/YOUR-NAME/simple-cicd.git
   git push -u origin main
   ```
2. Open the **Actions** tab. You'll see CI and CD running.
3. For CD to work, enable Pages once:
   **Settings > Pages > Source: GitHub Actions**, then re-run the CD workflow.
   Your site appears at `https://YOUR-NAME.github.io/simple-cicd/`.

## Exercises

1. **See it fail:** in `app/calculator.js` change `a + b` to `a - b` and push.
   CI goes red and CD does NOT deploy.
2. **Fix it:** change it back and push. Green again, site updates.
3. **Pull request flow:** make a branch, break something, open a PR.
   The PR shows a red X. Fix it and it turns green.
4. **Add a function and a test** (e.g. `power`), push, watch it run.
5. **Badge:** add this to the top of the README (use your name):
   `![CI](https://github.com/YOUR-NAME/simple-cicd/actions/workflows/ci.yml/badge.svg)`
6. **Protect main:** Settings > Branches > require the `test` check before merging.

## Key ideas

- **Workflow**: a YAML file in `.github/workflows/`.
- **Trigger (`on`)**: what starts it (push, pull request, schedule...).
- **Job**: a group of steps on one fresh machine. Jobs run in parallel
  unless you use `needs`.
- **Step**: either `uses:` (a ready-made action) or `run:` (a shell command).
- **CI**: check every change. **CD**: ship it automatically after checks pass.
