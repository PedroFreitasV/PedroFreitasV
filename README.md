### Olá! Sou Pedro de Freitas 👋

##

<h1>Mais sobre mim</h1>

- 🔭 Estou trabalhando como front-end!
- 🌱 Estou estudando React e Typescript!
- 😄 Pronomes: Ele/Dele

##
<div align="center">
  <a href="https://github.com/PedroFreitasV">
    <img height="180em" src="https://github-readme-stats.vercel.app/api?username=PedroFreitasV&show_icons=true&theme=date_night&include_all_commits=true&count_private=true"/>
  </a>
</div>

##

<div align="center">
  <a href="https://github.com/PedroFreitasV"></a>
  <img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=PedroFreitasV&layout=compact&langs_count=7&theme=date_night"/>
</div>

##

<div style="display: inline_block;"><br>
  <h1>Minhas Skills 🔥</h1>
  <p align="center">
    <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white">
    <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white">
    <img src="https://img.shields.io/badge/JavaScript-323330?style=for-the-badge&logo=javascript&logoColor=F7DF1E">
    <img src="https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white">
    <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB">
    <img src="https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white">
    <img src="https://img.shields.io/badge/Netlify-00C7B7?style=for-the-badge&logo=netlify&logoColor=white">
    <img src="https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white">
  </p>
</div>

##
 
<div> 
  <h2>Fale Comigo</h2>
  <a href="https://www.instagram.com/thisispedrodefreitas/" target="_blank">
    <img src="https://img.shields.io/badge/-Instagram-%23E4405F?style=for-the-badge&logo=instagram&logoColor=white" target="_blank">
  </a>
  <a href="https://api.whatsapp.com/send?phone=5581986189572" target="_blank">
    <img src="https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" target="_blank">
  </a>
</div>

# GitHub Action for generating a contribution graph with a snake eating your contributions.

# ![snake gif](https://github.com/your-user-name/your-user-name/blob/output/github-contribution-grid-snake.gif)

name: Generate Snake

# Controls when the action will run.
on:
  schedule:
      # every 12 hours
    - cron: "0 */12 * * *"

  # This command allows us to run the Action automatically from the Actions tab.
  workflow_dispatch:
  
  # Also run on every push on the master branch
  push:
    branches:
    - main

# The sequence of runs in this workflow:
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      - name: Clone repo
        uses: actions/checkout@v3
    
      - name: Generate the snake files in './dist/'
        uses: Platane/snk@v3
        id: snake-gif
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |     
            dist/github-contribution-grid-snake.gif
            dist/github-contribution-grid-snake.svg
        env:
           GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Show build status
        run: git status

      - name: Push new files to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
          commit_message: Update snake animations
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
