[add SSH from Linux to GitHub](add%20SSH%20from%20Linux%20to%20GitHub.md)

![PAT](https://www.youtube.com/watch?v=IuiH6cBtc58)

![Setup SSH for Github Account](https://www.youtube.com/watch?v=A4usVjplxbU)
### How to setup Private Access Token on GitHub?
1. Click your profile picture (top-right corner of GitHub)
2. Click "Settings" (near the bottom of the dropdown)
3. Scroll all the way down the left sidebar to "Developer settings" (very last item)
4. In the new page, click "Personal access tokens" in the left sidebar
5. Click "Tokens (classic)"
6. Click "Generate new token" → "Generate new token (classic)"
![Pasted image 20260528111934.png](../Attachments/Pasted%20image%2020260528111934.png)
Add new fine-grained token to give access to particular private repo:
![Pasted image 20260528113439.png](../Attachments/Pasted%20image%2020260528113439.png)
Now generate token
![Pasted image 20260528113652.png](../Attachments/Pasted%20image%2020260528113652.png)
now it will generate token here
>[!warning]
>Now save it somewhere safe. because its not going to show it here again
![Pasted image 20260528113734.png](../Attachments/Pasted%20image%2020260528113734.png)

Now get repo link again - add token to the link
![Pasted image 20260528114029.png](../Attachments/Pasted%20image%2020260528114029.png)
![Pasted image 20260528114131.png](../Attachments/Pasted%20image%2020260528114131.png)

### How to handle tokens properly?
Great question. Here's what to do:

Right now:
1. Go to https://github.com/settings/tokens
2. Find the token you just created and click Delete — this immediately invalidates it so no one can use it

For future pushes, use Git Credential Manager instead of pasting tokens in chat:

> [!warning]
> Git Credential Manager (GCM) is already bundled with Git for Windows. It securely stores your credentials in Windows Credential Manager so you never have to type/paste a token again.

Run this once in your terminal:
`! git config --global credential.helper manager`

Then the next ==time you push==, Git will open a browser window asking you to log into GitHub — it handles the token automatically behind the scenes and saves it securely.

To test it:
`! git push origin main`

A browser login window should pop up. After you log in once, it remembers your credentials permanently.

This way your token is stored securely in Windows and never has to touch a chat window.
