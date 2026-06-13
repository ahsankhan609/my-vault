---
title: How to push or pull files from Google Colab to GitHub using Personal Access Token
source: https://www.youtube.com/watch?v=I77fny4s5Rg
tags:
  - lecture
  - tools
  - github
course-url: https://www.binarystudy.com/2025/01/how-to-pushpull-files-from-google-colab-to-github.html
---
Related Stuff:
[GitHub Access Tokens - How To Use Them Properly for Private repos - NeuralNine](GitHub%20Access%20Tokens%20-%20How%20To%20Use%20Them%20Properly%20for%20Private%20repos%20-%20NeuralNine.md)

### Steps
1. Generate **Personal Access Token** at [GitHub](https://www.github.com)
	1. Click on Profile Picture
	2. Go to Settings
	3. Go Down
	4. left side -> Developer Settings
	5. Click on left side
	6. **Personal Access Token** -> Token Classic
	7. Generate New Token -> Generate New Token (Classic)
	8. Give a Name in Note Section
	9. Set Expiration
	10. Select Scopes -> repo
	11. Generate Token -> Save it some where safe, we will be unable to see it again
2. Add user **email** and **user name** to config
3. Clone the GitHub repository
4. Change Current Directory to repository name
5. Make changes and add them to commit stack
6. Commit the changes
7. Push to the GitHub
8. pull command

### COLAB Setup:

1. Generate Access Token
```python
token = "ghp_PedTT6XJx8cEZzcB3J35Xp8Q0z4fRa1PZN9t"
```

2. Add user email and name to config
```bash
!git config -- global user.email "bianrystudy21@gmail.com"
!git config -- global user.name "Shahid Akhtar"
```

```bash
!git config --list
```

![](../Attachments/Pasted%20image%2020260613123734.png)

3. Clone Repository - In which we need to do work
```python
username = "binary-study"
repo = "DemoBinary"
```

![](../Attachments/Pasted%20image%2020260613124024.png)

```bash
!git clone https://{token}@github.com/{username}/{repo}

# !git clone https://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@github.com/binary-study/DemoBinary
```

4. Change Current working directory to New Cloned repository

```bash
!pwd
```

![](../Attachments/Pasted%20image%2020260613124335.png)

```bash
%cd {repo_name}
```

![](../Attachments/Pasted%20image%2020260613124355.png)

5. Made Changes in the repo and commit them
```bash
!ls
```

```bash
!git status
```

```bash
!git add --a

# adding all files
```

```bash
!git add file_name.py

# add specific file
```

```bash
!git status
```

```bash
!git add file_name.py
```

```bash
!git status
```

6. Commit all Changes

```bash
!git commit -a -m "Commit from Google colab with new file"

# To commit a specific file use
!git commit filename -m "specific message"

!git commit colab.htm -m "Commit from Google colab with new file"

!git commit myfile.py -m "Commit from Google colab with modified file"
```

7. Push to GitHub

```bash
!git push origin main
```

8. Pull Latest changes from GitHub

```bash
!git pull origin main
```

