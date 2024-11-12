## Hi there 👋
<!-- GitHub stats -->
<b>⚡ My Dev Statistics</b>


<p>
<!-- GitHub Stats -->
<img height="180em" src="https://github-readme-stats.vercel.app/api?username=lisamarie245&show_icons=true&hide_border=true" />


<!-- Most Used Languages -->
<img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=kmhmubin&exclude_repo=KNN-Image-Classification&show_icons=true&hide_border=true&layout=compact&langs_count=8"/>

</p>

name: Get Top Followers
  
 on:
  push:
  branches:
   - master
  schedule:
  - cron: '0 20 * * *'
  
 jobs:
  top-followers:
  runs-on: ubuntu-latest
  steps:
   - uses: actions/checkout@v2
   - name: Setup python
    uses: actions/setup-python@v2
    with:
     python-version: 3.8
   - name: Install requests
    run: pip install requests
   - name: Update README
    run: python src/getTopFollowers.py ${{ github.repository_owner }} ${{ secrets.GITHUB_TOKEN }} README.md
   - name: Commit changes
    run: |
     git config --local user.email "action@github.com"
     git config --local user.name "GitHub Action"
     git add -A
     git diff-index --quiet HEAD || git commit -m "Update top followers"
   - name: Pull changes
    run: git pull -r
   - name: Push changes
    uses: ad-m/github-push-action@master
    with:
     github_token: ${{ secrets.GITHUB_TOKEN }}
