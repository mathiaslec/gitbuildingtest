The page is available here: https://mathiaslec.github.io/gitbuildingtest/  
  
To have gitbuilding stuff in a separated folder, and allow a github page, here are modifications I added :  
- The path ".github/workflows " was placed at the root of the gitbuilding folder (instead of inside), so it looks like this :   
├── .github  
│   └── workflows  
│       └── gitbuilding.yml  
├── .gitignore  
├── README.md  
└── gitbuilding  
- The paths inside 'gitbuilding.yml' were modify as follow:    

```
name: Deploy Gitbuilding Project to Github Pages

on: [push]

jobs:
  build_and_deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
      - name: Install Python 3
        uses: actions/setup-python@v1
        with:
          python-version: "3.7"
      - name: Build
        run: |
          pip install gitbuilding
          **cd gitbuilding/**
          gitbuilding build-html
      - name: Deploy
        uses: JamesIves/github-pages-deploy-action@3.7.1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          BRANCH: gh-pages
          FOLDER: gitbuilding/_site/
          # Automatically remove deleted files from the deploy branch
          CLEAN: true
```
  
Questions :
- Do you need to use gitbuilding build?  
- Do you need to use gitbuilding build-html?  
