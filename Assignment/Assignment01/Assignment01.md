# Assignment 01: Git, Gitea, GitHub, Git LFS, and GitHub Pages

**Course:** Cloud Computing (BSE-410) | **Class:** BS(SE)-V | **Department:** Software Engineering, Fatima Jinnah Women University
**Deadline:** 10 October 2026 | **Total marks:** 10
**Submission repository:** `CC` | **Submission directory:** `Assignments/Assignment01`
**Screenshot directory:** `Assignments/Assignment01/screenshots`
**Required assignment files:** 3 | **Required screenshots:** 12

| Task | Description | CLO | Mapped PLO(s) | BT Level |
|---|---|---|---|---|
| Task 1 | Install Gitea and push a repository from the Ubuntu server | CLO1 | PLO1, PLO4 | C3 (Apply) |
| Task 2 | Push the same repository to GitHub | CLO2 | PLO1, PLO3, PLO4 | C4 (Analyze) |
| Task 3 | Track three large files with Git LFS | CLO3 | PLO1, PLO4 | C3 (Apply) |
| Task 4 | Create a Portfolio/CV with GitHub Pages | CLO4, CLO5 | PLO3, PLO4, PLO5 | C5 (Evaluate) |
| Submission Checklist | Submit assignment files, screenshots, and links | CLO5 | PLO5, PLO6 | C6 (Create) |

Complete all practical work using the environment specified for each task. Submit the required evidence to your existing public GitHub repository named exactly `CC` using this structure:

```text
CC/
└── Assignments/
    └── Assignment01/
        ├── Assignment01.md
        ├── Assignment01_Solution.docx
        ├── Assignment01_Solution.pdf
        └── screenshots/
            ├── task1_gitea_running.png
            ├── task1_gitea_push.png
            ├── task1_gitea_repository.png
            ├── task2_remotes.png
            ├── task2_github_push.png
            ├── task2_github_repository.png
            ├── task3_lfs_setup.png
            ├── task3_lfs_files.png
            ├── task3_lfs_push.png
            ├── task4_pages_repository.png
            ├── task4_pages_deployment.png
            └── task4_portfolio_live.png
```

## Assignment Objective

In this assignment, you install and run Gitea on your Ubuntu server, create and manage a Git repository from the same server, push that repository to Gitea and GitHub, manage large files with Git LFS, and publish a portfolio or CV with GitHub Pages.

By the end of this assignment, you will be able to:

- Install, run, and access a Gitea service on an Ubuntu server.
- Create and manage a Git repository from an Ubuntu server.
- Work with multiple Git remotes.
- Authenticate safely without exposing credentials.
- Track and push large files with Git LFS.
- Publish a static portfolio or CV with GitHub Pages.

## Required Working Environments

| Work | Required environment |
|---|---|
| Install and run the Gitea service | Ubuntu server |
| Perform Git terminal work for Tasks 1, 2, and 3 | Ubuntu server |
| Use Gitea and GitHub web pages | Web browser |
| Store assignment evidence | Existing GitHub repository named `CC` |

The Ubuntu terminal prompt must show your registered GitHub username and the hostname `ubuntu`: `<github-username>@ubuntu:~$`

## Task List

- Getting Started
- Task 1: Install Gitea and Push a Repository from the Ubuntu Server
- Task 2: Push the Same Repository to GitHub
- Task 3: Track Three Large Files with Git LFS
- Task 4: Create a Portfolio or CV with GitHub Pages
- Assignment Summary
- Final Submission Checklist

## Getting Started

1. Inside your existing `CC` repository, create the screenshot directory: `mkdir -p Assignments/Assignment01/screenshots`
2. Confirm the Ubuntu prompt follows `<github-username>@ubuntu:~$`.
3. Confirm Git and Git LFS are installed on the Ubuntu server. Docker and Docker Compose are installed in Task 1.
4. Read all four tasks before beginning.
5. Create `Assignment01_Solution.docx` and `Assignment01_Solution.pdf` inside `Assignments/Assignment01/` and add evidence as you complete each task.

## Task 1: Install Gitea and Push a Repository from the Ubuntu Server

### Step 1.1: Install and Run Gitea

1. Connect to the Ubuntu server and install Docker Engine and curl (`docker.io`).
2. Create `/usr/local/lib/docker/cli-plugins` and download the Docker Compose plug-in for x86_64.
3. Start Docker, add your user to the `docker` group, then fully sign out and reconnect.
4. Verify `git --version`, `docker --version`, `docker compose version`.
5. Clone `https://github.com/WaqasSaleem97/Gitea.git`, use the existing `compose.yaml` unchanged, and run `docker compose up -d`.
6. Confirm both containers with `docker compose ps` and test `curl http://127.0.0.1:3000/`. Show the IP with `ip addr`.
7. Open `http://<ubuntu-server-ip>:3000/` and use these installer settings:

| Setting | Required value |
|---|---|
| Database type | PostgreSQL |
| Database host | `db:5432` |
| Database username | `gitea` |
| Database password | `gitea` |
| Database name | `gitea` |
| Server domain | `<ubuntu-server-ip>` |
| Gitea base URL | `http://<ubuntu-server-ip>:3000/` |

8. Create the Gitea administrator account. Do not show any password or token in a screenshot.

Screenshot: `task1_gitea_running.png`

### Step 1.2: Create and Push the Initial Repository

1. In Gitea, create an empty public repository named exactly `Assignment01` (no README, .gitignore, or license).
2. On the server, create a separate local repository outside the Gitea directory and `CC`: `cd ~ && mkdir Assignment01 && cd Assignment01 && git init && git branch -M main`
3. Create `README.md` with your full name and registration number, then commit it (`Add student information`).
4. In Gitea, generate a token named `ubuntu-server-token` with `write:repository` permission. Never put it in a command, URL, or screenshot.
5. Add the remote (username only, no token): `git remote add gitea http://<gitea-username>@127.0.0.1:3000/<gitea-username>/Assignment01.git`
6. Verify with `git remote -v`, then `git push -u gitea main`. Paste the token at the password prompt.

Screenshot: `task1_gitea_push.png`

### Step 1.3: Verify the Gitea Repository

Open the repository in Gitea; owner, name, public status, rendered README (name and registration number) and the URL must be visible.

Screenshot: `task1_gitea_repository.png`

## Task 2: Push the Same Repository to GitHub

### Step 2.1: Create the GitHub Repository and Verify Both Remotes

Create an empty public GitHub repository `Assignment01`, then:

```bash
cd ~/Assignment01
git remote add github https://github.com/<your-github-username>/Assignment01.git
git remote -v
```

Both `gitea` and `github` must show fetch and push URLs with no token or password.

Screenshot: `task2_remotes.png`

### Step 2.2: Push to GitHub

```bash
git push -u github main
```

Screenshot: `task2_github_push.png`

### Step 2.3: Verify the GitHub Repository

Open `https://github.com/<your-github-username>/Assignment01`; owner, name, public status and rendered README must be visible.

Screenshot: `task2_github_repository.png`

## Task 3: Track Three Large Files with Git LFS

### Step 3.1: Configure Git LFS

```bash
cd ~/Assignment01
git lfs install
git lfs version
git lfs track "*.bin"
cat .gitattributes
```

Screenshot: `task3_lfs_setup.png`

### Step 3.2: Create and Verify Three LFS Files

```bash
truncate -s 101M large-file-1.bin
truncate -s 102M large-file-2.bin
truncate -s 103M large-file-3.bin
git add .gitattributes large-file-1.bin large-file-2.bin large-file-3.bin
git lfs ls-files --size
```

All three files must be listed and each must be larger than 100 MiB.

Screenshot: `task3_lfs_files.png`

### Step 3.3: Commit and Push the LFS Files

```bash
git commit -m "Add three files using Git LFS"
git push github main
```

Capture the first successful upload, preferably 100% (3/3).

Screenshot: `task3_lfs_push.png`

## Task 4: Create a Portfolio or CV with GitHub Pages

### Step 4.1: Create and Push the Portfolio Repository

1. Create a public GitHub repository named `<your-github-username>.github.io`.
2. Build the portfolio with HTML and CSS (at least `index.html` and `styles.css`).
3. It must visibly contain: About Me, Education, Skills, Projects.
4. Commit and push to `main`. Keep owner, repo name, `index.html` and `styles.css` visible.

Screenshot: `task4_pages_repository.png`

### Step 4.2: Publish with GitHub Pages

Settings → Pages → Build and deployment → **Deploy from a branch** → `main` and `/ (root)` → Save. Wait until the site is live. The page must show GitHub Pages, the live status and your `github.io` URL.

Screenshot: `task4_pages_deployment.png`

### Step 4.3: Verify the Live Portfolio

Open `https://<your-github-username>.github.io/`; the full URL and at least one required section must be visible.

Screenshot: `task4_portfolio_live.png`

## Final Submission Checklist

- [ ] I completed the assignment individually.
- [ ] `Assignment01.md` is inside `CC/Assignments/Assignment01/`.
- [ ] `Assignment01_Solution.docx` is inside `CC/Assignments/Assignment01/` and opens correctly.
- [ ] `Assignment01_Solution.pdf` is inside `CC/Assignments/Assignment01/`, matches the Word solution, and opens correctly.
- [ ] My `CC` repository contains `Assignments/Assignment01/screenshots/`.
- [ ] All 12 required screenshots are present and readable.
- [ ] Every screenshot was captured immediately after the requested step.
- [ ] Every screenshot was created from my own work.
- [ ] My GitHub username is visible in every Ubuntu server terminal screenshot.
- [ ] Every terminal screenshot shows the required command and its relevant result.
- [ ] Every browser screenshot shows the required repository, URL, page, or status.
- [ ] No screenshot contains a token, password, private key, or other credential.
- [ ] My `CC`, GitHub `Assignment01`, and `<username>.github.io` repositories are public.
- [ ] My Gitea `Assignment01` repository was created and pushed from the Ubuntu server.
- [ ] All repositories use the `main` branch.
- [ ] I pushed the complete `Assignments/Assignment01` directory before the deadline.
- [ ] I uploaded all three required assignment files to Google Classroom.
- [ ] I submitted the three required links on Google Classroom.

## Academic Integrity

Marks are awarded for completing and demonstrating the required process, not only for showing a final result. You may be asked to explain or demonstrate any submitted step. Copied work, copied screenshots, or evidence that does not belong to the submitting student will not receive credit.
