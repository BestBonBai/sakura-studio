
## My Sakura Studio
- Demo link: [sakura.bestbonbai.me](https://sakura.bestbonbai.me )
- [Powered by Hexo-theme-Sakura](https://docs.hojun.cn/sakura/docs/)

## To do list:
- [x] try using Travis CI to publish Hexo blog to Github Automatically
- [x] set github pages
- [x] use new tech called workflow to  GitHub Actions to deploy Github Pages. 

## method

### pre. click `Actions` of your repository, then create a `.github/workflows/pages.yml' file

### 1. add `.github/workflows/pages.yml` file to your repo with the following content:
```yml
.github/workflows/pages.yml # don't need this line


name: Pages

on:
  push:
    branches:
      - master  # default branch

jobs:
  pages:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js 12.x
        uses: actions/setup-node@v1
        with:
          node-version: '12.x'
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: gh-pages  # deploying branch
```
### 2. Once the deployment is finished, the generated pages can be found in the master branch of your repository
### 3. In your GitHub repo’s setting, navigate to “GitHub Pages” section and change Source to master branch.
### 4. Check the webpage at username.github.io.
### Note:  if you specify a custom domain name with a `CNAME`, you need to add the `CNAM`E file to the `source/` folder.

## Reference
- [hexo help](https://hexo.io/docs/github-pages.html)
